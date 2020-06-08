---
title: 'Adobe Experience Manager as a Cloud Service におけるデジタルアセット管理のための Assets API '
description: Assets API を使用すると、バイナリ、メタデータ、レンディション、コメント、コンテンツフラグメントなどのアセットを管理するための基本的な CRUD（作成、読み取り、更新、削除）操作を実行できます。
contentOwner: AG
translation-type: tm+mt
source-git-commit: 27e72bbc0d852eb2c2eb059967c91e6108613965
workflow-type: tm+mt
source-wordcount: '1249'
ht-degree: 100%

---


# AEM Assets as a Cloud Service の API {#assets-cloud-service-apis}

<!-- 
Give a list of and overview of all reference information available.
* New upload method
* Javadocs
* Assets HTTP API documented at [https://helpx.adobe.com/experience-manager/6-5/assets/using/mac-api-assets.html](https://helpx.adobe.com/experience-manager/6-5/assets/using/mac-api-assets.html)

-->

## アセットのアップロード {#asset-upload-technical}

Adobe Experience Manager as a Cloud Service では、アセットをリポジトリにアップロードする新しい方法を提供します。つまり、バイナリクラウドストレージへの直接バイナリアップロードです。ここでは、技術的概要を説明します。

### 直接バイナリアップロードの概要 {#overview-binary-upload}

バイナリをアップロードするアルゴリズムの概要は、次のとおりです。

1. 新しいバイナリをアップロードするためのインテントを AEM に通知する HTTP リクエストを送信します。
1. 開始リクエストで提供される 1 つ以上の URI にバイナリのコンテンツを POST 送信します。
1. HTTP リクエストを送信して、バイナリのコンテンツが正常にアップロードされたことをサーバーに通知します。

![直接バイナリアップロードプロトコルの概要](assets/add-assets-technical.png)

以前のバージョンの AEM との重要な違いは、次のとおりです。

* バイナリは AEM を経由しません。AEM は、デプロイメント用に設定されたバイナリクラウドストレージを使用するアップロードプロセスを調整するだけです。
* バイナリクラウドストレージの前面には、コンテンツ配信ネットワーク（CDN、Edge ネットワーク）が配置されます。これにより、アップロードエンドポイントがクライアントに近づくので、特に分散チームによるアセットのアップロードの際に、アップロードパフォーマンスとユーザーエクスペリエンスが向上します。

このアプローチで、アセットのアップロードをよりスケーラブルかつ効率的に処理できます。

> !![NOTE]
この方法を実装するクライアントコードを確認するには、オープンソースの [aem-upload ライブラリ](https://github.com/adobe/aem-upload)を参照してください。

### アップロードの開始 {#initiate-upload}

最初の手順として、アセットが作成または更新されるフォルダーに HTTP POST リクエストを送信します。その際、バイナリアップロードを開始するためのリクエストであることを示す `.initiateUpload.json` セレクターを含めます。例えば、アセットが作成されるフォルダーのパスが `/assets/folder` の場合、リクエストは次のようになります。

```
POST https://[aem_server]/content/dam/assets/folder.initiateUpload.json
```

リクエスト本文のコンテンツタイプは、次のフィールドを含んだ `application/x-www-form-urlencoded` 形式のデータにする必要があります。

* `(string) fileName`：必須。インスタンスに表示されるアセットの名前。
* `(number) fileSize`：必須。アップロードするバイナリの合計長（バイト単位）。

各バイナリに必須フィールドが含まれている限り、単一のリクエストを使用して複数のバイナリのアップロードを開始できます。成功した場合は、リクエストへの応答として、`201` ステータスコードと、次の形式の JSON データを含んだ本文が返されます。

```
{
    "completeURI": "(string)",
    "folderPath": (string)",
    "files": [
        {
            "fileName": "(string)",
            "mimeType": "(string)",
            "uploadToken": "(string)",
            "uploadURIs": [
                "(string)"
            ]
        }
    ]
}
```

* `completeURI`（文字列）：バイナリのアップロードが完了したら、この URI を呼び出します。URI は絶対 URI でも相対 URI でも構いません。クライアントはどちらでも処理できるはずです。つまり、値は `"https://author.acme.com/content/dam.completeUpload.json"` または `"/content/dam.completeUpload.json"` でも構いません。[アップロードの完了](#complete-upload)を参照してください。
* `folderPath`（文字列）：バイナリがアップロードされるフォルダーの完全なパス。
* `(files)`（配列）：開始リクエストで提供されるバイナリ情報のリストの長さと順序に一致する要素のリスト。
* `fileName`（文字列）：対応するバイナリの名前（開始リクエストで指定されたもの）。この値は、完了リクエストに含まれます。
* `mimeType`（文字列）：対応するバイナリの MIME タイプ（開始リクエストで指定されたもの）。この値は、完了リクエストに含まれます。
* `uploadToken`（文字列）：対応するバイナリのアップロードトークン。この値は、完了リクエストに含まれます。
* `uploadURIs`（配列）：バイナリコンテンツのアップロード先となる完全な URI を表す文字列のリストです（[バイナリのアップロード](#upload-binary)を参照）。
* `minPartSize`（数字）：複数の URI がある場合に各アップロード URI に提供されるデータの最小長（バイト単位）。
* `maxPartSize`（数字）：複数の URI がある場合に各アップロード URI に提供されるデータの最大長（バイト単位）。

### バイナリのアップロード {#upload-binary}

アップロードを開始した場合の出力には、1 つ以上のアップロード URI 値が含まれています。複数の URI を指定する場合は、クライアント側でバイナリを「分割」し、各部分を各 URI に順に POST 送信します。すべての URI を使用する必要があり、各部分は、開始応答で指定された最小サイズより大きく最大サイズより小さくなっている必要があります。これらのリクエストは、バイナリのアップロードを高速化するために、CDN エッジノードで受信されます。

これを実現するには、API で提供されるアップロード URI の数に基づいて各部分のサイズを計算する方法が考えられます。例えば、バイナリの合計サイズが 20,000 バイトで、アップロード URI の数が 2 の場合は次のようになります。

* 合計サイズを URI 数で除算して計算した各部分のサイズ：20,000 / 2 = 10,000
* アップロード URI リストの最初の URI にバイナリの 0～9,999 バイトを POST 送信
* アップロード URI リストの 2 番目の URI にバイナリの 10,000～19,999 バイトを POST 送信

成功した場合、サーバーは各要求への応答として `201` ステータスコードを返します。

### アップロードの完了 {#complete-upload}

バイナリファイルのすべての部分がアップロードされたら、開始データから提供される完全な URI に HTTP POST リクエストを送信します。リクエスト本文のコンテンツタイプは、次のフィールドを含んだ `application/x-www-form-urlencoded` 形式のデータにする必要があります。

| フィールド | タイプ | 必須／未指定 | 説明 |
|---|---|---|---|
| `fileName` | String | 必須 | アセットの名前（開始データで提供されたもの）。 |
| `mimeType` | String | 必須 | バイナリの HTTP コンテンツタイプ（開始データで提供されたもの）。 |
| `uploadToken` | String | 必須 | バイナリのアップロードトークン（開始データで提供されたもの）。 |
| `createVersion` | Boolean | オプション | これが `True` で、指定した名前のアセットが既に存在する場合、Experience Manager はアセットの新しいバージョンを作成します。 |
| `versionLabel` | String | オプション | 新しいバージョンが作成される場合、アセットの新しいバージョンに関連付けられるラベル。 |
| `versionComment` | String | オプション | 新しいバージョンが作成される場合、そのバージョンに関連付けられたコメント。 |
| `replace` | Boolean | オプション | これが `True` で指定した名前のアセットが既に存在する場合、Experience Manager はそのアセットを削除し、再作成します。 |

>!![NOTE]
>
> アセットが既に存在し、`createVersion` も `replace` も指定されていない場合、Experience Manager はアセットの現在のバージョンを新しいバイナリで更新します。

開始プロセスと同様に、完了リクエストデータには、複数のファイルに関する情報が含まれる場合があります。

バイナリのアップロードプロセスは、ファイルの完了 URL が呼び出されるまで実行されません。ファイルのバイナリ全体がアップロードされても、アセットのアップロードプロセスが完了するまで、アセットは処理されません。

成功した場合、サーバーは応答として `200` ステータスコードを返します。

### オープンソースアップロードライブラリ {#open-source-upload-library}

アップロードアルゴリズムの詳細を調べたり、独自のアップロードスクリプトやツールを作成する場合に役立つように、アドビでは、次のオープンソースライブラリおよびツールを出発点として提供しています。

* [オープンソース aem-upload ライブラリ](https://github.com/adobe/aem-upload)
* [オープンソースコマンドラインツール](https://github.com/adobe/aio-cli-plugin-aem)

### 非推奨（廃止予定）のアセットアップロード API {#deprecated-asset-upload-api}

<!-- #ENGCHECK review / update the list of deprecated APIs below. -->

Adobe Experience Manager as a Cloud Service では、新しいアップロード API のみサポートされています。Adobe Experience Manager 6.5 の API は非推奨（廃止予定）となりました。アセットやレンディションのアップロードまたは更新（あらゆるバイナリアップロード）に関連するメソッドは、次の API で非推奨（廃止予定）となりました。

* [AEM Assets HTTP API](mac-api-assets.md)
* `AssetManager`Java API（`AssetManager.createAsset(..)` など）

>[!MORELIKETHIS]
* [オープンソース aem-upload ライブラリ](https://github.com/adobe/aem-upload)。
* [オープンソースコマンドラインツール](https://github.com/adobe/aio-cli-plugin-aem).


## アセット処理ワークフローとアセット後処理ワークフロー {#post-processing-workflows}

Experience Manager でのアセット処理は、**[!UICONTROL アセットマイクロサービス]**&#x200B;を使用する[処理プロファイル](asset-microservices-configure-and-use.md#get-started-using-asset-microservices)設定に基づいておこなわれます。処理には、開発者用の拡張機能は必要ありません。

後処理ワークフローの設定には、カスタム手順を指定した標準ワークフローを使用します。

## 後処理ワークフローでのワークフローステップのサポート {#post-processing-workflows-steps}

以前のバージョンの Experience Manager から Experience Manager as a Cloud Service へアップグレードした顧客は、アセットの処理にアセットマイクロサービスを使用できます。クラウドネイティブのアセットマイクロサービスは、設定と使用が非常に簡単です。以前のバージョンの [!UICONTROL DAM アセットの更新]ワークフローで使用されるワークフロー手順の一部はサポートされていません。

以下のワークフロー手順は、Experience Manager as a Cloud Service でサポートされています。

* `com.day.cq.dam.similaritysearch.internal.workflow.process.AutoTagAssetProcess`
* `com.day.cq.dam.core.impl.process.CreateAssetLanguageCopyProcess`
* `com.day.cq.wcm.workflow.process.CreateVersionProcess`
* `com.day.cq.dam.similaritysearch.internal.workflow.smarttags.StartTrainingProcess`
* `com.day.cq.dam.similaritysearch.internal.workflow.smarttags.TransferTrainingDataProcess`
* `com.day.cq.dam.core.impl.process.TranslateAssetLanguageCopyProcess`
* `com.day.cq.dam.core.impl.process.UpdateAssetLanguageCopyProcess`
* `com.adobe.cq.workflow.replication.impl.ReplicationWorkflowProcess`
* `com.day.cq.dam.core.impl.process.DamUpdateAssetWorkflowCompletedProcess`

次の技術的ワークフローモデルは、アセットマイクロサービスに置き換わっているか、サポートされていません。

* `com.day.cq.dam.core.impl.process.DamMetadataWritebackWorkflowCompletedProcess`
* `com.day.cq.dam.core.process.DeleteImagePreviewProcess`
* `com.day.cq.dam.s7dam.common.process.DMEncodeVideoWorkflowCompletedProcess`
* `com.day.cq.dam.core.process.GateKeeperProcess`
* `com.day.cq.dam.core.process.AssetOffloadingProcess`
* `com.day.cq.dam.core.process.MetadataProcessorProcess`
* `com.day.cq.dam.core.process.XMPWritebackProcess`
* `com.adobe.cq.dam.dm.process.workflow.DMImageProcess`
* `com.day.cq.dam.s7dam.common.process.S7VideoThumbnailProcess`
* `com.day.cq.dam.scene7.impl.process.Scene7UploadProcess`
* `com.day.cq.dam.s7dam.common.process.VideoProxyServiceProcess`
* `com.day.cq.dam.s7dam.common.process.VideoThumbnailDownloadProcess`
* `com.day.cq.dam.s7dam.common.process.VideoUserUploadedThumbnailProcess`
* `com.day.cq.dam.core.process.CreatePdfPreviewProcess`
* `com.day.cq.dam.core.process.CreateWebEnabledImageProcess`
* `com.day.cq.dam.video.FFMpegThumbnailProcess`
* `com.day.cq.dam.core.process.ThumbnailProcess`
* `com.day.cq.dam.cameraraw.process.CameraRawHandlingProcess`
* `com.day.cq.dam.core.process.CommandLineProcess`
* `com.day.cq.dam.pdfrasterizer.process.PdfRasterizerHandlingProcess`
* `com.day.cq.dam.core.process.AddPropertyWorkflowProcess`
* `com.day.cq.dam.core.process.CreateSubAssetsProcess`
* `com.day.cq.dam.core.process.DownloadAssetProcess`
* `com.day.cq.dam.word.process.ExtractImagesProcess`
* `com.day.cq.dam.word.process.ExtractPlainProcess`
* `com.day.cq.dam.video.FFMpegTranscodeProcess`
* `com.day.cq.dam.ids.impl.process.IDSJobProcess`
* `com.day.cq.dam.indd.process.INDDMediaExtractProcess`
* `com.day.cq.dam.indd.process.INDDPageExtractProcess`
* `com.day.cq.dam.core.impl.lightbox.LightboxUpdateAssetProcess`
* `com.day.cq.dam.pim.impl.sourcing.upload.process.ProductAssetsUploadProcess`
* `com.day.cq.dam.core.process.ScheduledPublishBPProcess`
* `com.day.cq.dam.core.process.ScheduledUnPublishBPProcess`
* `com.day.cq.dam.core.process.SendDownloadAssetEmailProcess`
* `com.day.cq.dam.core.impl.process.SendTransientWorkflowCompletedEmailProcess`

<!-- PPTX source: slide in add-assets.md - overview of direct binary upload section of 
https://adobe-my.sharepoint.com/personal/gklebus_adobe_com/_layouts/15/guestaccess.aspx?guestaccesstoken=jexDC5ZnepXSt6dTPciH66TzckS1BPEfdaZuSgHugL8%3D&docid=2_1ec37f0bd4cc74354b4f481cd420e07fc&rev=1&e=CdgElS
-->
