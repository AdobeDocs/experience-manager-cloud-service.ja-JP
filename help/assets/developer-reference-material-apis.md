---
title: ' [!DNL Assets] の開発者向けリファレンス'
description: '[!DNL Assets] APIs and developer reference content lets you manage assets, including binary files, metadata, renditions, comments, and [!DNL Content Fragments]'
contentOwner: AG
translation-type: tm+mt
source-git-commit: 5be8ab734306ad1442804b3f030a56be1d3b5dfa
workflow-type: tm+mt
source-wordcount: '1208'
ht-degree: 97%

---


# [!DNL Assets] API と開発者向けリファレンス資料 {#assets-cloud-service-apis}

この記事には、[!DNL Assets]の開発者向けの参考資料とリソースが[!DNL Cloud Service]として含まれています。 新しいアップロード方法、API リファレンス、後処理ワークフローで提供されるサポートに関する情報が含まれています。

## アセットのアップロード {#asset-upload-technical}

[!DNL Experience Manager][!DNL Cloud Service] as a には、アセットをリポジトリーにアップロードする新しい方法が用意されています。ユーザーは、HTTP API を使用して、アセットをクラウドストレージに直接アップロードできます。バイナリファイルをアップロードする手順は次のとおりです。

1. [HTTP リクエストを送信します](#initiate-upload)。その結果、新しいバイナリをアップロードする意図が [!DNL Experience Manage]r デプロイメントに通知されます。
1. [開始リクエストで提供される 1 つ以上の URI にバイナリのコンテンツを POST 送信します。](#upload-binary)
1. [HTTP リクエストを送信して、バイナリのコンテンツが正常にアップロードされたことをサーバーに通知します。](#complete-upload)

![直接バイナリアップロードプロトコルの概要](assets/add-assets-technical.png)

このアプローチで、アセットのアップロードをスケーラブルかつより効率的に処理できます。[!DNL Experience Manager] 6.5 と比較した場合の違いは次のとおりです。

* バイナリは [!DNL Experience Manager] を経由しません。AEM は、デプロイメント用に設定されたバイナリクラウドストレージを使用するアップロードプロセスを調整するだけです。
* バイナリクラウドストレージは、コンテンツ配信ネットワーク（CDN）または Edge ネットワークと連携します。CDN は、クライアントに近いアップロードエンドポイントを選択します。特に地理的に分散したチームでは、データが近くのエンドポイントに転送される距離が短いほど、アップロードのパフォーマンスとユーザーエクスペリエンスが向上します。

>[!NOTE]
>
>この方法を実装するクライアントコードを確認するには、オープンソースの [aem-upload ライブラリ](https://github.com/adobe/aem-upload)を参照してください。

### アップロードの開始 {#initiate-upload}

HTTP POST リクエストを目的のフォルダーに送信します。このフォルダーでアセットが作成または更新されます。このリクエストがバイナリファイルのアップロードを開始するものであることを示すセレクター `.initiateUpload.json` を含めます。例えば、アセットが作成されるフォルダーのパスが `/assets/folder` の場合、POST リクエストは `POST https://[aem_server]:[port]/content/dam/assets/folder.initiateUpload.json` のようになります。

リクエスト本文のコンテンツタイプは、次のフィールドを含んだ `application/x-www-form-urlencoded` 形式のデータにする必要があります。

* `(string) fileName`：必須。Adobe [!DNL Experience Manager] に表示されるアセットの名前
* `(number) fileSize`：必須。アップロードされるアセットのファイルサイズ（バイト単位）

各バイナリに必須フィールドが含まれている限り、単一のリクエストを使用して複数のバイナリのアップロードを開始できます。成功した場合は、リクエストへの応答として、`201` ステータスコードと、次の形式の JSON データを含んだ本文が返されます。

```json
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

アップロードを開始した場合の出力には、1 つ以上のアップロード URI 値が含まれています。複数の URI を指定した場合、クライアント側でバイナリを複数の部分に分割し、各部分の POST リクエストを各 URI に順に送信します。すべての URI を使用します。各部分のサイズが、開始応答で指定された最小サイズと最大サイズの範囲内に収まっている必要があります。CDN エッジノードを使用すると、要求されたバイナリアップロードを高速化できます。

これを実現するには、API で提供されるアップロード URI の数に基づいて各部分のサイズを計算する方法があります。例えば、バイナリの合計サイズが 20,000 バイトで、アップロード URI の数が 2 だとします。この場合は次の手順に従います。

* 合計サイズを URI 数で除算して各部分のサイズを計算。20,000 / 2 = 10,000
* アップロード URI リストの最初の URI にバイナリの 0～9,999 バイトを POST 送信。
* アップロード URI リストの 2 番目の URI にバイナリの 10,000～19,999 バイトを POST 送信。

アップロードに成功した場合、サーバーは各リクエストへの応答として `201` ステータスコードを返します。

### アップロードの完了 {#complete-upload}

バイナリファイルのすべての部分がアップロードされたら、開始データから提供される完全な URI に HTTP POST リクエストを送信します。リクエスト本文のコンテンツタイプは、次のフィールドを含んだ `application/x-www-form-urlencoded` 形式のデータにする必要があります。

| フィールド | 型 | 必須／未指定 | 説明 |
|---|---|---|---|
| `fileName` | String | 必須 | アセットの名前（開始データで提供されたもの）。 |
| `mimeType` | 文字列 | 必須 | バイナリの HTTP コンテンツタイプ（開始データで提供されたもの）。 |
| `uploadToken` | 文字列 | 必須 | バイナリのアップロードトークン（開始データで提供されたもの）。 |
| `createVersion` | Boolean | オプション | これが `True` で、指定した名前のアセットが存在する場合、Adobe [!DNL Experience Manager] はアセットの新しいバージョンを作成します。 |
| `versionLabel` | 文字列 | オプション | 新しいバージョンが作成される場合、アセットの新しいバージョンに関連付けられるラベル。 |
| `versionComment` | 文字列 | オプション | 新しいバージョンが作成される場合、そのバージョンに関連付けられたコメント。 |
| `replace` | ブール値 | オプション | これが `True` で指定した名前のアセットが存在する場合、Adobe [!DNL Experience Manager] はそのアセットを削除し、再作成します。 |

>!![NOTE]
アセットが存在し、`createVersion` も `replace` も指定されていない場合、Adobe [!DNL Experience Manager] はアセットの現在のバージョンを新しいバイナリで更新します。

開始プロセスと同様に、完了リクエストデータには、複数のファイルに関する情報が含まれる場合があります。

バイナリのアップロードプロセスは、ファイルの完了 URL が呼び出されるまで実行されません。アセットは、アップロードプロセスの完了後に処理されます。アセットのバイナリファイルが完全にアップロードされても、アップロードプロセスが完了していなければ、処理は開始しません。

成功した場合、サーバーは応答として `200` ステータスコードを返します。

### オープンソースアップロードライブラリ {#open-source-upload-library}

アップロードアルゴリズムの詳細を調べたり、独自のアップロードスクリプトやツールを作成する場合に役立つように、アドビでは、次のオープンソースライブラリおよびツールを提供しています。

* [オープンソース aem-upload ライブラリ](https://github.com/adobe/aem-upload)。
* [オープンソースコマンドラインツール](https://github.com/adobe/aio-cli-plugin-aem)。

### 非推奨（廃止予定）のアセットアップロード API {#deprecated-asset-upload-api}

<!-- #ENGCHECK review / update the list of deprecated APIs below. -->

新しいアップロードメソッドは、[!DNL Cloud Service]として[!DNL Adobe Experience Manager]に対してのみサポートされます。 [!DNL Adobe Experience Manager] 6.5 の API は非推奨（廃止予定）となりました。アセットやレンディションのアップロードまたは更新（あらゆるバイナリアップロード）に関連するメソッドは、次の API で非推奨（廃止予定）となりました。

* [Adobe Experience Manager Assets HTTP API](mac-api-assets.md)
* `AssetManager`Java API（`AssetManager.createAsset(..)` など）

>[!MORELIKETHIS]
* [オープンソース aem-upload ライブラリ](https://github.com/adobe/aem-upload)。
* [オープンソースコマンドラインツール](https://github.com/adobe/aio-cli-plugin-aem)。


## アセット処理ワークフローとアセット後処理ワークフロー {#post-processing-workflows}

[!DNL Experience Manager] でのアセット処理は、[アセットマイクロサービス](asset-microservices-configure-and-use.md#get-started-using-asset-microservices)を使用する&#x200B;**[!UICONTROL 処理プロファイル]**&#x200B;設定に基づいておこなわれます。処理には、開発者用の拡張機能は必要ありません。

後処理ワークフローの設定には、カスタム手順を指定した標準ワークフローを使用します。

## 後処理ワークフローでのワークフローステップのサポート {#post-processing-workflows-steps}

Adobe [!DNL Experience Manager] の以前のバージョンからアップグレードしたユーザーは、アセットマイクロサービスを使用してアセットを処理できます。クラウドネイティブのアセットマイクロサービスは、設定と使用が非常に簡単です。以前のバージョンの [!UICONTROL DAM アセットの更新]ワークフローで使用されるワークフロー手順の一部はサポートされていません。

[!DNL Experience Manager] を [!DNL Cloud Service] サポートする次のワークフロー手順を実行します。

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

>[!MORELIKETHIS]
* [aSDKとしてのExperience Cloud [!DNL Cloud Service] です](/help/implementing/developing/introduction/aem-as-a-cloud-service-sdk.md)。

