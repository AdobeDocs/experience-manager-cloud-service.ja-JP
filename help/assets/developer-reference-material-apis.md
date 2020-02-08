---
title: 'クラウドサービスとしてのAdobe Experience Managerでのデジタルアセット管理のためのアセットAPI '
description: アセットAPIを使用すると、基本的なcreate-read-update-delete(CRUD)操作で、バイナリ、メタデータ、レンディション、コメント、コンテンツフラグメントなどのアセットを管理できます。
contentOwner: AG
translation-type: tm+mt
source-git-commit: 991d4900862c92684ed92c1afc081f3e2d76c7ff

---


# クラウドサービスAPIとしてのアセット {#assets-cloud-service-apis}

<!-- 
Give a list of and overview of all reference information available.
* New upload method
* Javadocs
* Assets HTTP API documented at [https://helpx.adobe.com/experience-manager/6-5/assets/using/mac-api-assets.html](https://helpx.adobe.com/experience-manager/6-5/assets/using/mac-api-assets.html)

-->

## アセットのアップロード {#asset-upload-technical}

クラウドサービスとしてのExperience Managerは、アセットをリポジトリにアップロードする新しい方法を提供します。バイナリアップロードはバイナリクラウドストレージに直接アップロードされます。 ここでは、技術概要を説明します。

### 直接バイナリアップロードの概要 {#overview-binary-upload}

バイナリをアップロードする高レベルアルゴリズムは、次のとおりです。

1. 新しいバイナリをアップロードする意図をAEMに通知するHTTPリクエストを送信します。
1. 開始要求で提供される1つ以上のURIにバイナリのコンテンツをPOSTします。
1. HTTP要求を送信して、バイナリの内容が正常にアップロードされたことをサーバーに通知します。

![直接バイナリアップロードプロトコルの概要](assets/add-assets-technical.png)

以前のバージョンのAEMとの重要な違いを次に示します。

* バイナリはAEMを通過しません。これは、アップロードプロセスをデプロイメント用に設定されたバイナリクラウドストレージと調整するだけのものです
* バイナリクラウドストレージは、コンテンツ配信ネットワーク(CDN、Edge Network)によって前面に配置され、アップロードエンドポイントがクライアントに近づくので、特に分散チームのアセットをアップロードする際のアップロードパフォーマンスとユーザーエクスペリエンスが向上します

このアプローチは、アセットのアップロードをよりスケーラブルでパフォーマンスの高い処理にする必要があります。

> !![NOTE]
この方法を実装するクライアントコードを確認するには、オープンソースの [aemアップロードライブラリを参照してください](https://github.com/adobe/aem-upload)

### アップロードの開始 {#initiate-upload}

最初の手順は、アセットを作成または更新するフォルダーにHTTP POSTリクエストを送信することです。リクエストがバイナリ `.initiateUpload.json` アップロードを開始することを示すセレクターを含めます。 例えば、アセットを作成するフォルダーのパスは次のようになりま `/assets/folder`す。

```
POST https://[aem_server]/content/dam/assets/folder.initiateUpload.json
````

リクエスト本文のコンテンツタイプは、次のフィールドを `application/x-www-form-urlencoded` 含むフォームデータである必要があります。

* `(string) fileName`: 必須. インスタンスに表示されるアセットの名前。
* `(number) fileSize`: 必須. アップロードするバイナリの合計長（バイト単位）。

各バイナリに必須フィールドが含まれている限り、単一の要求を使用して複数のバイナリのアップロードを開始できます。

成功した場合、リクエストは201ステータスコードと、次の形式のJSONデータを含む本文で応答します。

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
````

* `(string) completeURI`:バイナリのアップロードが完了したときに呼び出されるURIです。 これは絶対URIまたは相対URIで、クライアントはどちらも処理できるはずです。 例：値は、またはの場合がありま `"https://author.acme.com/content/dam.completeUpload.json"` す(アッ `"/content/dam.completeUpload.json"` プロー [ドの完了](#complete-upload))。
* `(string) folderPath`:バイナリがアップロードされるフォルダーのフルパスです。
* `(array) (files)`:要素の長さと順序が、開始要求で提供されるバイナリ情報のリストの長さと順序と一致するリストです。
* `(string) fileName`:開始要求で指定された、対応するバイナリの名前。 この値は、完了リクエストに含める必要があります。
* `(string) mimeType`:in initiate要求で指定された、対応するバイナリのMIMEタイプ。 この値は、完了リクエストに含める必要があります。
* `(string) uploadToken`:対応するバイナリのアップロードトークン。 この値は、完了リクエストに含める必要があります。
* `(array) uploadURIs`:値がバイナリのコンテンツのアップロード先となる完全なURIである文字列のリストです( [Upload binary](#upload-binary))。
* `(number) minPartSize`:複数のURIがある場合、いずれかのuploadURIに提供される可能性のあるデータの最小長（バイト）。
* `(number) maxPartSize`:複数のURIがある場合に、いずれかのuploadURIに提供されるデータの最大長（バイト）。

### バイナリのアップロード {#upload-binary}

アップロードを開始した場合の出力には、1つ以上のアップロードURI値が含まれます。 複数のURIを指定する場合、バイナリを順番に部分に「分割」し、各部分を各URIに順にPOSTするのはクライアントの責任です。 すべてのURIを使用し、各部分は、開始応答で指定された最小サイズより大きく最大サイズより小さい必要があります。 これらの要求は、バイナリのアップロードを高速化するために、CDNエッジノードによって前面に配置されます。

これを行う可能性のある方法の1つは、APIが提供するアップロードURIの数に基づいてパーツサイズを計算することです。 バイナリの合計サイズが20,000バイトで、アップロードURIの数が2の場合の例：

* 合計サイズをURI数で割ってパーツサイズを計算します。20,000 / 2 = 10,000
* アップロードURIのリストの最初のURIに対するバイナリの0 ～ 9,999のPOSTバイト範囲
* アップロードURIのリストの2番目のURIに対するバイナリのPOSTバイト範囲10,000 ～ 19,999

成功した場合、サーバーは各要求にステータスコードで応 `201` 答します。

### アップロードの完了 {#complete-upload}

バイナリのすべての部分がアップロードされたら、最後の手順は、開始データによって提供される完全なURIにHTTP POSTリクエストを送信することです。 リクエスト本文のコンテンツタイプは、次のフィールドを含む申込み`x-www-form-urlencoded` /フォームデータである必要があります。

* `(string) fileName`: 必須. 開始データによって提供された、アセットの名前。
* `(string) mimeType`: 必須. 開始データによって提供されたバイナリのHTTPコンテンツタイプです。
* `(string) uploadToken`: 必須. 開始データによって提供されたバイナリのアップロードトークン。
* `(bool) createVersion`: 任意. trueで指定した名前のアセットが既に存在する場合、インスタンスはアセットの新しいバージョンを作成します。
* `(string) versionLabel`: 任意. 新しいバージョンが作成された場合、そのバージョンに関連付けられるラベル。
* `(string) versionComment`: 任意. 新しいバージョンが作成されると、そのバージョンに関連付けられるコメントが作成されます。
* `(bool) replace`:オプション：trueで指定した名前のアセットが既に存在する場合、インスタンスはアセットを削除し、再作成します。

>!![NOTE]
>
> アセットが既に存在し、createVersionもreplaceも指定されていない場合、インスタンスは、アセットの現在のバージョンを新しいバイナリで更新します。

開始プロセスと同様に、完全な要求データには、複数のファイルに関する情報が含まれる場合があります。

バイナリのアップロード処理は、ファイルの完全なURLが呼び出されるまで実行されません。 ファイルのバイナリ全体がアップロードされても、アセットのアップロード処理が完了するまで、アセットはインスタンスによって処理されません。

成功した場合、サーバーはステータスコードで `200` 応答します。

### オープンソースアップロードライブラリ {#open-source-upload-library}

アップロードアルゴリズムの詳細や独自のアップロードスクリプトやツールを作成するために、アドビはオープンソースのライブラリやツールを基にしています。

* [ソースaemアップロードライブラリを開く](https://github.com/adobe/aem-upload)
* [オープンソースのコマンドラインツール](https://github.com/adobe/aio-cli-plugin-aem)

### 非推奨のアセットアップロードAPI {#deprecated-asset-upload-api}

<!-- #ENGCHECK please review / update the list of deprecated APIs below -->

>[!NOTE]
クラウドサービスとしてのExperience Managerでは、新しいアップロードAPIのみがサポートされます。 Experience Manager 6.5のAPIは廃止されました。

アセットやレンディションのアップロードまたは更新（バイナリアップロード）に関連するメソッドは、以下のAPIで非推奨となりました。

* [AEM Assets HTTP API](mac-api-assets.md)
* `AssetManager` Java API( `AssetManager.createAsset(..)`

>[!MORELIKETHIS]
* [ソースaemアップロードライブラリを開く](https://github.com/adobe/aem-upload)
* [オープンソースのコマンドラインツール](https://github.com/adobe/aio-cli-plugin-aem)


## アセット処理と後処理のワークフロー {#post-processing-workflows}

アセット処理のほとんどは、アセットマイクロサービスに **[!UICONTROL よる処理プロファイル]** 設定に基 [づいて実行され](asset-microservices-configure-and-use.md#get-started-using-asset-microservices)、開発者用の拡張機能は必要ありません。

後処理ワークフローの設定では、拡張機能を備えた標準のAEM Workflows（例：カスタムステップを使用できます）。 次のサブセクションを確認し、アセット後処理ワークフローで使用できるワークフロー手順を理解します。

### 後処理ワークフローのワークフロー手順 {#post-processing-workflows-steps}

>[!NOTE]
この節は、主に、以前のバージョンのAEMからクラウドサービスとしてAEMにアップデートするお客様に適用されます。

Experience Managerをクラウドサービスとして導入した新しいデプロイメントモデルにより、アセットマイクロサービスの導入前にワークフローで使用された特定のワークフロー手順が後処理ワークフローでサポートされなくなる場合があります。 `DAM Update Asset` ほとんどは、アセットマイクロサービスをより簡単に設定し、使用できるようになっています。

次に、AEMのクラウドサービスとしての技術ワークフローモデルとそのサポートレベルを示します。

### サポートされるワークフロー手順 {#supported-workflow-steps}

クラウドサービスでは、次のワークフロー手順がサポートされています。

* `com.day.cq.dam.similaritysearch.internal.workflow.process.AutoTagAssetProcess`
* `com.day.cq.dam.core.impl.process.CreateAssetLanguageCopyProcess`
* `com.day.cq.wcm.workflow.process.CreateVersionProcess`
* `com.day.cq.dam.similaritysearch.internal.workflow.smarttags.StartTrainingProcess`
* `com.day.cq.dam.similaritysearch.internal.workflow.smarttags.TransferTrainingDataProcess`
* `com.day.cq.dam.core.impl.process.TranslateAssetLanguageCopyProcess`
* `com.day.cq.dam.core.impl.process.UpdateAssetLanguageCopyProcess`
* `com.adobe.cq.workflow.replication.impl.ReplicationWorkflowProcess`
* `com.day.cq.dam.core.impl.process.DamUpdateAssetWorkflowCompletedProcess`

### サポートされていない、または置き換えられたモデル {#unsupported-replaced-models}

以下の技術ワークフローモデルは、アセットマイクロサービスに置き換えられるか、サポートが利用できません。

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
