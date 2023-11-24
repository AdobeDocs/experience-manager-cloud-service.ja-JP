---
title: ' [!DNL Assets] の開発者向けリファレンス'
description: 「[!DNL Assets] API と開発者向けリファレンスコンテンツを使用すると、バイナリファイル、メタデータ、レンディション、コメント、 [!DNL Content Fragments] を管理できます」
contentOwner: AG
feature: APIs,Assets HTTP API
role: Developer,Architect,Admin
exl-id: c75ff177-b74e-436b-9e29-86e257be87fb
source-git-commit: a63a237e8da9260fa5f88060304b8cf9f508da7f
workflow-type: ht
source-wordcount: '1899'
ht-degree: 100%

---

# [!DNL Adobe Experience Manager Assets] デベロッパー向けの使用例、API、参考資料 {#assets-cloud-service-apis}

このドキュメントは、[!DNL Assets] as a [!DNL Cloud Service] の開発者向けレコメンデーション、リファレンス資料およびリソースが含まれています。新しいアップロードモジュール、API リファレンス、後処理ワークフローで提供されるサポートに関する情報が含まれています。

## [!DNL Experience Manager Assets] API と操作 {#use-cases-and-apis}

[!DNL Assets] as a [!DNL Cloud Service] には、デジタルアセットをプログラミングで操作するためのいくつかの API が用意されています。各 API は、以下の表に示すように、特定の使用例をサポートしています。[!DNL Assets] ユーザーインターフェイス、[!DNL Experience Manager] デスクトップアプリ、[!DNL Adobe Asset Link] は、すべての操作または一部の操作をサポートしています。

>[!CAUTION]
>
>一部の API は引き続き存在しますが、アクティブにサポートされていません（x で示されます）。可能な限り、これらの API は使用しないでください。

| サポートレベル | 説明 |
| ------------- | --------------------------- |
| ✓ | サポート対象 |
| × | サポートされていない。使用しないでください。 |
| - | 使用不可 |

| 使用例 | [aem-upload](https://github.com/adobe/aem-upload) | [Experience Manager／Sling／JCR](https://www.adobe.io/experience-manager/reference-materials/cloud-service/javadoc/index.html) Java API | [Asset Compute Service](https://experienceleague.adobe.com/docs/asset-compute/using/extend/understand-extensibility.html?lang=ja) | [[!DNL Assets] HTTP API](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/assets/admin/mac-api-assets.html?lang=ja#create-an-asset) | Sling [GET](https://sling.apache.org/documentation/bundles/rendering-content-default-get-servlets.html)／[POST](https://sling.apache.org/documentation/bundles/manipulating-content-the-slingpostservlet-servlets-post.html) サーブレット | [GraphQL](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/graphql/overview.html?lang=ja) |
| ----------------|:---:|:---:|:---:|:---:|:---:|:---:|
| **元のバイナリ** |  |  |  |  |  |  |
| オリジナルを作成 | ✓ | × | - | × | × | - |
| オリジナルを読む | - | × | ✓ | ✓ | ✓ | - |
| オリジナルをアップデート | ✓ | × | ✓ | × | × | - |
| オリジナルを削除 | - | ✓ | - | ✓ | ✓ | - |
| オリジナルをコピー | - | ✓ | - | ✓ | ✓ | - |
| オリジナルを移動 | - | ✓ | - | ✓ | ✓ | - |
| **メタデータ** |  |  |  |  |  |  |
| メタデータを作成 | - | ✓ | ✓ | ✓ | ✓ | - |
| メタデータを読み取り | - | ✓ | - | ✓ | ✓ | - |
| メタデータを更新 | - | ✓ | ✓ | ✓ | ✓ | - |
| メタデータを削除 | - | ✓ | ✓ | ✓ | ✓ | - |
| メタデータをコピー | - | ✓ | - | ✓ | ✓ | - |
| メタデータを移動 | - | ✓ | - | ✓ | ✓ | - |
| **コンテンツフラグメント（CF）** |  |  |  |  |  |  |
| CF を作成 | - | ✓ | - | ✓ | - | - |
| CF を読み取り | - | ✓ | - | ✓ | - | ✓ |
| CF を更新 | - | ✓ | - | ✓ | - | - |
| CF を削除 | - | ✓ | - | ✓ | - | - |
| CF をコピー | - | ✓ | - | ✓ | - | - |
| CF を移動 | - | ✓ | - | ✓ | - | - |
| **バージョン** |  |  |  |  |  |  |
| バージョンを作成 | ✓ | ✓ | - | - | - | - |
| バージョンを読み取り | - | ✓ | - | - | - | - |
| バージョンを削除 | - | ✓ | - | - | - | - |
| **フォルダー** |  |  |  |  |  |  |
| フォルダーを作成 | ✓ | ✓ | - | ✓ | - | - |
| フォルダーを読み取り | - | ✓ | - | ✓ | - | - |
| フォルダーを削除 | ✓ | ✓ | - | ✓ | - | - |
| フォルダーをコピー | ✓ | ✓ | - | ✓ | - | - |
| フォルダーを移動 | ✓ | ✓ | - | ✓ | - | - |

## アセットのアップロード {#asset-upload}

[!DNL Experience Manager] as a [!DNL Cloud Service] では、HTTP API を使用して、アセットをクラウドストレージに直接アップロードできます。バイナリファイルをアップロードする手順は次のとおりです。これらの手順は、[!DNL Experience Manager] JVM 内ではなく、外部アプリケーションで実行します。

1. [HTTP リクエストを送信します](#initiate-upload)。その結果、新しいバイナリをアップロードする意図が [!DNL Experience Manage]r デプロイメントに通知されます。
1. [開始リクエストで提供される 1 つ以上の URI にバイナリのコンテンツを PUT 送信します。](#upload-binary)
1. [HTTP リクエストを送信して、バイナリのコンテンツが正常にアップロードされたことをサーバーに通知します。](#complete-upload)

![直接バイナリアップロードプロトコルの概要](assets/add-assets-technical.png)

>[!IMPORTANT]
>
上記の手順は、[!DNL Experience Manager] JVM 内ではなく、外部アプリケーションで実行します。

このアプローチで、アセットのアップロードをスケーラブルかつより効率的に処理できます。[!DNL Experience Manager] 6.5 と比較した場合の違いは次のとおりです。

* バイナリは [!DNL Experience Manager] を経由しません。AEM は、デプロイメント用に設定されたバイナリクラウドストレージを使用するアップロードプロセスを調整するだけです。
* バイナリクラウドストレージは、コンテンツ配信ネットワーク（CDN）または Edge ネットワークと連携します。CDN は、クライアントに近いアップロードエンドポイントを選択します。特に地理的に分散したチームでは、データが近くのエンドポイントに転送される距離が短いほど、アップロードのパフォーマンスとユーザーエクスペリエンスが向上します。

>[!NOTE]
>
この方法を実装するクライアントコードを確認するには、オープンソースの [aem-upload ライブラリ](https://github.com/adobe/aem-upload)を参照してください。
>
[!IMPORTANT]
>
特定の状況では、Cloud Service 内のストレージの一貫性が最終的に維持されるので、Experience Manager に対するリクエスト間で変更が完全に反映されない場合があります。これにより、必要なフォルダー作成が反映されないので、アップロード呼び出しを開始または完了するための応答が 404 になります。クライアントは 404 応答を想定し、バックオフ戦略を使用して再試行を実装することでそれらを処理する必要があります。

### アップロードの開始 {#initiate-upload}

HTTP POST リクエストを目的のフォルダーに送信します。このフォルダーでアセットが作成または更新されます。このリクエストがバイナリファイルのアップロードを開始するものであることを示すセレクター `.initiateUpload.json` を含めます。例えば、アセットが作成されるフォルダーのパスが `/assets/folder` の場合、POST リクエストは `POST https://[aem_server]:[port]/content/dam/assets/folder.initiateUpload.json` のようになります。

リクエスト本文のコンテンツタイプは、次のフィールドを含んだ `application/x-www-form-urlencoded` 形式のデータにする必要があります。

* `(string) fileName`：必須。Adobe [!DNL Experience Manager] に表示されるアセットの名前
* `(number) fileSize`：必須。アップロードされるアセットのファイルサイズ（バイト単位）

各バイナリに必須フィールドが含まれている限り、単一のリクエストを使用して複数のバイナリのアップロードを開始できます。成功した場合は、リクエストへの応答として、`201` ステータスコードと、次の形式の JSON データを含んだ本文が返されます。

```json
{
    "completeURI": "(string)",
    "folderPath": "(string)",
    "files": [
        {
            "fileName": "(string)",
            "mimeType": "(string)",
            "uploadToken": "(string)",
            "uploadURIs": [
                "(string)"
            ],
            "minPartSize": (number),
            "maxPartSize": (number)
        }
    ]
}
```

* `completeURI`（文字列）：バイナリのアップロードが完了したら、この URI を呼び出します。URI は絶対 URI でも相対 URI でも構いません。クライアントはどちらでも処理できるはずです。つまり、値は `"https://[aem_server]:[port]/content/dam.completeUpload.json"` または `"/content/dam.completeUpload.json"` でも構いません。[アップロードの完了](#complete-upload)を参照してください。
* `folderPath`（文字列）：バイナリがアップロードされるフォルダーの完全なパス。
* `(files)`（配列）：開始リクエストで提供されるバイナリ情報のリストの長さと順序に一致する要素のリスト。
* `fileName`（文字列）：対応するバイナリの名前（開始リクエストで指定されたもの）。この値は、完了リクエストに含まれます。
* `mimeType`（文字列）：対応するバイナリの MIME タイプ（開始リクエストで指定されたもの）。この値は、完了リクエストに含まれます。
* `uploadToken`（文字列）：対応するバイナリのアップロードトークン。この値は、完了リクエストに含まれます。
* `uploadURIs`（配列）：バイナリコンテンツのアップロード先となる完全な URI を表す文字列のリストです（[バイナリのアップロード](#upload-binary)を参照）。
* `minPartSize`（数字）：複数の URI がある場合にいずれかの `uploadURIs` に提供されるデータの最小長（バイト単位）。
* `maxPartSize`（数字）：複数の URI がある場合にいずれかの `uploadURIs` に提供されるデータの最大長（バイト単位）。

### バイナリのアップロード {#upload-binary}

アップロードを開始した場合の出力には、1 つ以上のアップロード URI 値が含まれています。複数の URI を指定した場合、クライアント側でバイナリを複数のパーツに分割し、各パーツの PUT リクエストを、提供されたアップロード URI に順に送信する場合があります。バイナリを複数に分割する場合は、次のガイドラインに従ってください。

* 分割したパーツのサイズは、最後のものを除き、`minPartSize`.以上でなければなりません。
* 各パーツのサイズは `maxPartSize`.以下でなければなりません。
* バイナリのサイズが `maxPartSize` を超えた場合は、バイナリを複数のパーツに分割してアップロードします。
* すべての URI を使用する必要はありません。

バイナリのサイズが `maxPartSize` 以下の場合は、バイナリ全体を単一のアップロード URI にアップロードすることもできます。複数のアップロード URI が指定された場合、最初のアップロード URI を使用し、残りは無視します。すべての URI を使用する必要はありません。

CDN エッジノードを使用すると、要求されたバイナリアップロードを高速化できます。

これを行う最も簡単な方法は、パーツサイズとして `maxPartSize` を使用することです。API 契約は、この値をパーツサイズとして使用する場合、バイナリをアップロードするのに十分なアップロード URI があることを保証します。これを行うには、各パーツに対して 1 つの URI を順に使用して、バイナリを `maxPartSize` サイズのパーツに分割します。最後の部分は、`maxPartSize` 以下の任意のサイズにできます。例えば、バイナリの合計サイズが 20,000 バイトで、`minPartSize` は 5,000 バイト、`maxPartSize` は 8,000 バイト、アップロード URI の数は 5 だとします。以下の手順を実行します。

* 最初のアップロード URI を使用して、バイナリの最初の 8,000 バイトをアップロードします。
* 2 番目のアップロード URI を使用して、バイナリの 2 番目の 8,000 バイトをアップロードします。
* 3 番目のアップロード URI を使用して、バイナリの最後の 4,000 バイトをアップロードします。これが最後のパーツなので、`minPartSize`.以上の大きさにする必要はありません。
* 最後の 2 つのアップロード URI を使用する必要はありません。無視して構いません。

よくあるエラーは、API で提供されるアップロード URI の数に基づいて各部分のサイズを計算することです。API 契約では、この方法が機能するとは保証されず、実際には、`minPartSize` と `maxPartSize` の範囲外のパーツサイズになる場合があります。その結果、バイナリのアップロードに失敗する可能性があります。

繰り返しますが、最も簡単で安全な方法は、単に `maxPartSize`.と同じサイズのパーツを使用することです。

アップロードに成功した場合、サーバーは各リクエストへの応答として `201` ステータスコードを返します。

>[!NOTE]
>
アップロードアルゴリズムについて詳しくは、[公式機能ドキュメント](https://jackrabbit.apache.org/oak/docs/features/direct-binary-access.html#Upload)および Apache Jackrabbit Oak プロジェクトの [API ドキュメント](https://jackrabbit.apache.org/oak/docs/apidocs/org/apache/jackrabbit/api/binary/BinaryUpload.html)を参照してください。

### アップロードの完了 {#complete-upload}

バイナリファイルのすべての部分がアップロードされたら、開始データから提供される完全な URI に HTTP POST リクエストを送信します。リクエスト本文のコンテンツタイプは、次のフィールドを含んだ `application/x-www-form-urlencoded` 形式のデータにする必要があります。

| フィールド | 型 | 必須／未指定 | 説明 |
|---|---|---|---|
| `fileName` | String | 必須 | アセットの名前（開始データで提供されたもの）。 |
| `mimeType` | String | 必須 | バイナリの HTTP コンテンツタイプ（開始データで提供されたもの）。 |
| `uploadToken` | String | 必須 | バイナリのアップロードトークン（開始データで提供されたもの）。 |
| `createVersion` | Boolean | オプション | これが `True` で、指定した名前のアセットが存在する場合、Adobe [!DNL Experience Manager] はアセットの新しいバージョンを作成します。 |
| `versionLabel` | String | オプション | 新しいバージョンが作成される場合、アセットの新しいバージョンに関連付けられるラベル。 |
| `versionComment` | String | オプション | 新しいバージョンが作成される場合、そのバージョンに関連付けられたコメント。 |
| `replace` | Boolean | オプション | これが `True` で指定した名前のアセットが存在する場合、Adobe [!DNL Experience Manager] はそのアセットを削除し、再作成します。 |
| `uploadDuration` | Number | オプション | ファイル全体がアップロードされるまでの合計時間（ミリ秒単位）。これを指定した場合、アップロード時間は転送レートの分析用にシステムのログファイルに記録されます。 |
| `fileSize` | Number | オプション | ファイルのサイズ（バイト単位）。これを指定した場合、ファイルサイズは転送レートの分析用にシステムのログファイルに記録されます。 |

>[!NOTE]
>
アセットが存在し、`createVersion` も `replace` も指定されていない場合、Adobe [!DNL Experience Manager] はアセットの現在のバージョンを新しいバイナリで更新します。

開始プロセスと同様に、完了リクエストデータには、複数のファイルに関する情報が含まれる場合があります。

バイナリのアップロードプロセスは、ファイルの完了 URL が呼び出されるまで実行されません。アセットは、アップロードプロセスの完了後に処理されます。アセットのバイナリファイルが完全にアップロードされても、アップロードプロセスが完了していなければ、処理は開始しません。アップロードが正常に完了した場合、サーバーは応答として `200` ステータスコードを返します。

### オープンソースアップロードライブラリ {#open-source-upload-library}

アップロードアルゴリズムの詳細を調べたり、独自のアップロードスクリプトやツールを作成する場合に役立つように、アドビでは、次のオープンソースライブラリおよびツールを提供しています。

* [オープンソース aem-upload ライブラリ](https://github.com/adobe/aem-upload)。
* [オープンソースコマンドラインツール](https://github.com/adobe/aio-cli-plugin-aem)。

>[!NOTE]
>
aem-upload ライブラリとコマンドラインツールの両方で、[node-httptransfer ライブラリ](https://github.com/adobe/node-httptransfer/)を使用します

### 非推奨（廃止予定）のアセットアップロード API {#deprecated-asset-upload-api}

<!-- #ENGCHECK review / update the list of deprecated APIs below. -->

新しいアップロード方法は、[!DNL Adobe Experience Manager] as a [!DNL Cloud Service] の場合のみサポートされます。[!DNL Adobe Experience Manager] 6.5 の API は非推奨（廃止予定）となりました。アセットやレンディションのアップロードまたは更新（あらゆるバイナリアップロード）に関連するメソッドは、次の API で非推奨（廃止予定）となりました。

* [Adobe Experience Manager Assets HTTP API](mac-api-assets.md)
* `AssetManager`Java API（`AssetManager.createAsset(..)`、`AssetManager.createAssetForBinary(..)`、`AssetManager.getAssetForBinary(..)`、`AssetManager.removeAssetForBinary(..)`、`AssetManager.createOrUpdateAsset(..)`、`AssetManager.createOrReplaceAsset(..)` など）

>[!MORELIKETHIS]
>
* [オープンソース aem-upload ライブラリ](https://github.com/adobe/aem-upload)。
* [オープンソースコマンドラインツール](https://github.com/adobe/aio-cli-plugin-aem)。
* [直接アップロード用の Apache Jackrabbit Oak ドキュメント](https://jackrabbit.apache.org/oak/docs/features/direct-binary-access.html#Upload)。

## アセット処理ワークフローとアセット後処理ワークフロー {#post-processing-workflows}

[!DNL Experience Manager] でのアセット処理は、[アセットマイクロサービス](asset-microservices-configure-and-use.md#get-started-using-asset-microservices)を使用する&#x200B;**[!UICONTROL 処理プロファイル]**&#x200B;設定に基づいて行われます。処理には、開発者用の拡張機能は必要ありません。

後処理ワークフローの設定には、カスタム手順を指定した標準ワークフローを使用します。

## 後処理ワークフローでのワークフローステップのサポート {#post-processing-workflows-steps}

Adobe [!DNL Experience Manager] の以前のバージョンからアップグレードした場合は、アセットマイクロサービスを使用してアセットを処理できます。クラウドネイティブのアセットマイクロサービスは、設定と使用が簡単です。以前のバージョンの [!UICONTROL DAM アセットの更新]ワークフローで使用されるワークフロー手順の一部はサポートされていません。サポートされているクラスについて詳しくは、[Java API リファレンスか Javadoc](https://www.adobe.io/experience-manager/reference-materials/cloud-service/javadoc/index.html) を参照してください。

次のテクニカルワークフローモデルは、アセットマイクロサービスに置き換わっているか、サポートされていません。

* `com.day.cq.dam.cameraraw.process.CameraRawHandlingProcess`
* `com.day.cq.dam.core.process.CommandLineProcess`
* `com.day.cq.dam.pdfrasterizer.process.PdfRasterizerHandlingProcess`
* `com.day.cq.dam.core.process.AddPropertyWorkflowProcess`
* `com.day.cq.dam.core.process.CreateSubAssetsProcess`
* `com.day.cq.dam.core.process.DownloadAssetProcess`
* `com.day.cq.dam.word.process.ExtractImagesProcess`
* `com.day.cq.dam.word.process.ExtractPlainProcess`
* `com.day.cq.dam.ids.impl.process.IDSJobProcess`
* `com.day.cq.dam.indd.process.INDDMediaExtractProcess`
* `com.day.cq.dam.indd.process.INDDPageExtractProcess`
* `com.day.cq.dam.core.impl.lightbox.LightboxUpdateAssetProcess`
* `com.day.cq.dam.pim.impl.sourcing.upload.process.ProductAssetsUploadProcess`
* `com.day.cq.dam.core.process.SendDownloadAssetEmailProcess`
* `com.day.cq.dam.similaritysearch.internal.workflow.smarttags.StartTrainingProcess`
* `com.day.cq.dam.similaritysearch.internal.workflow.smarttags.TransferTrainingDataProcess`
* `com.day.cq.dam.switchengine.process.SwitchEngineHandlingProcess`
* `com.day.cq.dam.core.process.GateKeeperProcess`
* `com.day.cq.dam.s7dam.common.process.DMEncodeVideoWorkflowCompletedProcess`
* `com.day.cq.dam.core.process.DeleteImagePreviewProcess`
* `com.day.cq.dam.video.FFMpegTranscodeProcess`
* `com.day.cq.dam.core.process.ThumbnailProcess`
* `com.day.cq.dam.video.FFMpegThumbnailProcess`
* `com.day.cq.dam.core.process.CreateWebEnabledImageProcess`
* `com.day.cq.dam.core.process.CreatePdfPreviewProcess`
* `com.day.cq.dam.s7dam.common.process.VideoUserUploadedThumbnailProcess`
* `com.day.cq.dam.s7dam.common.process.VideoThumbnailDownloadProcess`
* `com.day.cq.dam.s7dam.common.process.VideoProxyServiceProcess`
* `com.day.cq.dam.scene7.impl.process.Scene7UploadProcess`
* `com.day.cq.dam.s7dam.common.process.S7VideoThumbnailProcess`
* `com.day.cq.dam.core.process.MetadataProcessorProcess`
* `com.day.cq.dam.core.process.AssetOffloadingProcess`
* `com.adobe.cq.dam.dm.process.workflow.DMImageProcess`

<!-- Commenting the previous list documented at the time of GA. Replacing it with the updated list via cqdoc-18231.

* `com.day.cq.dam.core.process.DeleteImagePreviewProcess`
* `com.day.cq.dam.s7dam.common.process.DMEncodeVideoWorkflowCompletedProcess`
* `com.day.cq.dam.core.process.GateKeeperProcess`
* `com.day.cq.dam.core.process.AssetOffloadingProcess`
* `com.day.cq.dam.core.process.MetadataProcessorProcess`
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
-->

<!-- PPTX source: slide in add-assets.md - overview of direct binary upload section of
https://adobe-my.sharepoint.com/personal/gklebus_adobe_com/_layouts/15/guestaccess.aspx?guestaccesstoken=jexDC5ZnepXSt6dTPciH66TzckS1BPEfdaZuSgHugL8%3D&docid=2_1ec37f0bd4cc74354b4f481cd420e07fc&rev=1&e=CdgElS
-->

**関連情報**

* [アセットを翻訳](translate-assets.md)
* [Assets HTTP API](mac-api-assets.md)
* [AEM Assets as a Cloud Service でサポートされているファイル形式](file-format-support.md)
* [アセットを検索](search-assets.md)
* [接続されたアセット](use-assets-across-connected-assets-instances.md)
* [アセットレポート](asset-reports.md)
* [メタデータスキーマ](metadata-schemas.md)
* [アセットをダウンロード](download-assets-from-aem.md)
* [メタデータを管理](manage-metadata.md)
* [検索ファセット](search-facets.md)
* [コレクションを管理](manage-collections.md)
* [メタデータの一括読み込み](metadata-import-export.md)

>[!MORELIKETHIS]
>
* [[!DNL Experience Cloud] as a [!DNL Cloud Service] SDK](/help/implementing/developing/introduction/aem-as-a-cloud-service-sdk.md)。
