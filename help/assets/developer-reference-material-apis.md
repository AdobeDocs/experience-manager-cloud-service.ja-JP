---
title: 'クラウドサービスとしてのAdobe Experience Managerでのデジタルアセット管理のためのアセットAPI '
description: アセットAPIを使用すると、基本的なcreate-read-update-delete(CRUD)操作で、バイナリ、メタデータ、レンディション、コメント、コンテンツフラグメントなどのアセットを管理できます。
contentOwner: AG
translation-type: tm+mt
source-git-commit: 68b2214a4c8941365120bdef670e89b4c9058966

---


# Assets as a Cloud Service APIs {#assets-cloud-service-apis}

<!-- 
Give a list of and overview of all reference information available.
* New upload method
* Javadocs
* Assets HTTP API documented at [https://helpx.adobe.com/experience-manager/6-5/assets/using/mac-api-assets.html](https://helpx.adobe.com/experience-manager/6-5/assets/using/mac-api-assets.html)

-->

## アセットのアップロード {#asset-upload-technical}

クラウドサービスとしてのExperience Managerは、アセットをリポジトリにアップロードする新しい方法を提供します。バイナリアップロードはバイナリクラウドストレージに直接アップロードされます。 ここでは、技術概要を説明します。

### 直接バイナリアップロードの概要 {#overview-binary-upload}

バイナリをアップロードする高レベルのアルゴリズムは、次のとおりです。

1. 新しいバイナリをアップロードする意図をAEMに通知するHTTPリクエストを送信します。
1. 開始要求で提供される1つ以上のURIにバイナリの内容をPOSTします。
1. HTTP要求を送信して、バイナリの内容が正常にアップロードされたことをサーバーに通知します。

![直接バイナリアップロードプロトコルの概要](assets/add-assets-technical.png)

以前のバージョンのAEMとの重要な違いを次に示します。

* バイナリはAEMを通過しません。これは、単に、デプロイメント用に設定されたバイナリクラウドストレージとアップロードプロセスを調整するだけです
* バイナリクラウドストレージは、コンテンツ配信ネットワーク(CDN、Edge Network)によって前面に配置され、アップロードエンドポイントがクライアントに近づくので、特に分散チームのアセットをアップロードする場合に、アップロードのパフォーマンスとユーザーエクスペリエンスが向上します

このアプローチは、アセットのアップロードをより拡張性が高く、パフォーマンスの高い処理を提供する必要があります。

> !![NOTE]
この方法を実装するクライアントコードを確認するには、オープンソースの [aemアップロードライブラリを参照してください](https://github.com/adobe/aem-upload)

### アップロードの開始 {#initiate-upload}

最初の手順は、アセットの作成または更新が必要なフォルダーにHTTP POSTリクエストを送信することです。セレクターを含め `.initiateUpload.json` て、リクエストがバイナリのアップロードを開始することを示します。 例えば、アセットを作成するフォルダーのパスは次のようになりま `/assets/folder`す。

```
POST https://[aem_server]/content/dam/assets/folder.initiateUpload.json
````

要求本文のコンテンツタイプは、次のフィールドを含む `application/x-www-form-urlencoded` フォームデータである必要があります。

* `(string) fileName`: 必須. インスタンスに表示されるアセットの名前。
* `(number) fileSize`: 必須. アップロードするバイナリの合計の長さ（バイト単位）。

各バイナリに必須フィールドが含まれている限り、単一の要求を使用して複数のバイナリのアップロードを開始できます。 成功した場合、リクエストはステータスコ `201` ードとJSONデータを含む本文を次の形式で応答します。

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

* `completeURI` （文字列）:バイナリのアップロードが完了したら、このURIを呼び出します。 URIは、絶対URIまたは相対URIで指定でき、クライアントはどちらも処理できる必要があります。 つまり、値は「アップロード完了」または「完 `"https://author.acme.com/content/dam.completeUpload.json"` 了」を `"/content/dam.completeUpload.json"` 表示す [ることができます](#complete-upload)。
* `folderPath` （文字列）:バイナリがアップロードされるフォルダのフルパス。
* `(files)` （配列）:リストの長さと順序が、開始要求で提供されるバイナリ情報のリストの長さと順序と一致する要素の要素です。
* `fileName` （文字列）:開始要求で指定された、対応するバイナリの名前。 この値は、完了リクエストに含める必要があります。
* `mimeType` （文字列）:in initiateリクエストで指定された、対応するバイナリのMIMEタイプ。 この値は、完了リクエストに含める必要があります。
* `uploadToken` （文字列）:対応するバイナリのアップロードトークン。 この値は、完了リクエストに含める必要があります。
* `uploadURIs` （配列）:値がバイナリのコンテンツのアップロード先の完全なURIである文字列のリストです(バイナリのアップロードを [参照](#upload-binary))。
* `minPartSize` （数値）:複数のURIが存在する場合に、いずれかのuploadURIに提供されるデータの最小長（バイト単位）です。
* `maxPartSize` （数値）:複数のURIが存在する場合に、いずれかのuploadURIに提供されるデータの最大長（バイト単位）。

### バイナリのアップロード {#upload-binary}

アップロードを開始した場合の出力には、1つ以上のアップロードURI値が含まれます。 複数のURIを指定する場合、バイナリを各URIに順に「分割」し、各部分を各URIに順にPOSTするのは、クライアントの責任です。 すべてのURIを使用し、各部分は、開始応答で指定された最小サイズより大きく、最大サイズより小さい必要があります。 バイナリのアップロードを高速化するため、これらのリクエストはCDNエッジノードによって前面に配置されます。

これを行う可能性のある方法の1つは、APIが提供するアップロードURIの数に基づいてパーツサイズを計算することです。 バイナリの合計サイズが20,000バイトで、アップロードURIの数が2であると仮定します。

* 合計サイズをURI数で割ってパーツサイズを計算します。20,000 / 2 = 10,000
* アップロードURIのリストの最初のURIに対するバイナリの0 ～ 9,999のPOSTバイト範囲
* アップロードURIのリストで、2番目のURIに対するバイナリの10,000 ～ 19,999のPOSTバイト範囲

成功した場合、サーバーは各要求にステータスコードで応 `201` 答します。

### アップロードの完了 {#complete-upload}

バイナリのすべての部分がアップロードされたら、最後の手順は、開始データによって提供される完全なURIにHTTP POSTリクエストを送信することです。 リクエスト本文のコンテンツタイプは、次のフィールドを含む申込み`x-www-form-urlencoded` /フォームデータである必要があります。

* `(string) fileName`: 必須. 開始データによって提供された、アセットの名前。
* `(string) mimeType`: 必須. 開始データによって提供されたバイナリのHTTPコンテンツタイプ。
* `(string) uploadToken`: 必須. 開始データによって提供されたバイナリのアップロードトークン。
* `(bool) createVersion`: 任意. trueで、指定した名前のアセットが既に存在する場合、インスタンスはアセットの新しいバージョンを作成します。
* `(string) versionLabel`: 任意. 新しいバージョンが作成された場合、そのバージョンに関連付けられるラベル。
* `(string) versionComment`: 任意. 新しいバージョンが作成されると、そのバージョンに関連付けられるコメントが作成されます。
* `(bool) replace`:オプション：trueで指定した名前のアセットが既に存在する場合、インスタンスはアセットを削除し、再作成します。

>!![NOTE]
>
> アセットが既に存在し、createVersionもreplaceも指定されていない場合、インスタンスは、アセットの現在のバージョンを新しいバイナリで更新します。

開始プロセスと同様に、完全な要求データには複数のファイルに関する情報が含まれる場合があります。

バイナリのアップロード処理は、ファイルの完全なURLが呼び出されるまで行われません。 ファイルのバイナリ全体がアップロードされた場合でも、アセットのアップロード処理が完了するまで、アセットはインスタンスによって処理されません。

成功した場合、サーバーはステータスコードで応 `200` 答します。

### オープンソースアップロードライブラリ {#open-source-upload-library}

アップロードアルゴリズムの詳細や、独自のアップロードスクリプトやツールを作成するために、アドビはオープンソースのライブラリやツールを基礎として提供しています。

* [ソースAEMアップロードライブラリを開く](https://github.com/adobe/aem-upload)
* [ソースのコマンドラインツールを開く](https://github.com/adobe/aio-cli-plugin-aem)

### 非推奨のアセットアップロードAPI {#deprecated-asset-upload-api}

<!-- #ENGCHECK review / update the list of deprecated APIs below -->

>[!NOTE]
クラウドサービスとしてのExperience Managerの場合、新しいアップロードAPIのみがサポートされます。 Experience Manager 6.5のAPIは非推奨です。

アセットやレンディション（バイナリアップロード）のアップロードまたは更新に関連するメソッドは、次のAPIで非推奨となりました。

* [AEM Assets HTTP API](mac-api-assets.md)
* `AssetManager` Java API( `AssetManager.createAsset(..)`

>[!MORELIKETHIS]
* [ソースAEMアップロードライブラリを開く](https://github.com/adobe/aem-upload)
* [ソースのコマンドラインツールを開く](https://github.com/adobe/aio-cli-plugin-aem)


## アセット処理と後処理のワークフロー {#post-processing-workflows}

ほとんどのアセット処理は、アセットマイクロサービ **[!UICONTROL スによる処理プロファイル]**[の設定に基づ](asset-microservices-configure-and-use.md#get-started-using-asset-microservices)いて実行され、開発者用の拡張機能は不要です。

後処理ワークフローの設定では、拡張機能を持つ標準のAEMワークフロー（カスタム手順を使用できます）。 次のサブセクションを確認し、アセットの後処理ワークフローで使用できるワークフロー手順を理解してください。ワークフロー

### 後処理ワークフローのワークフロー手順 {#post-processing-workflows-steps}

>[!NOTE]
この節は、主に、以前のバージョンのAEMからクラウドサービスとしてAEMにアップデートするお客様に適用されます。

Experience Managerをクラウドサービスとして導入した新しい導入モデルにより、アセットマイクロサービスの導入前にワークフローで使用された特定のワークフロー手順が、後処理ワークフローでサポートされなくなる場合があります。 `DAM Update Asset` ほとんどは、アセットのマイクロサービスをより簡単に設定し、使用できる形で置き換えられます。

次に、技術ワークフローモデルのリストと、クラウドサービスとしてのAEMでのそれらのサポートレベルを示します。

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

次の技術ワークフローモデルは、アセットマイクロサービスに置き換えられるか、サポートが利用できません。

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
