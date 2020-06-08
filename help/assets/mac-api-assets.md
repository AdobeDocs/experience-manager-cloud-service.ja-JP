---
title: Assets HTTP API in [!DNL Adobe Experience Manager].
description: のHTTP APIを使用して、デジタルアセットの作成、読み取り、更新、削除、管理を行います [!DNL Adobe Experience Manager Assets]。
contentOwner: AG
translation-type: tm+mt
source-git-commit: b96e976b5a2aaff90d7317360b0325dcae21ff26
workflow-type: tm+mt
source-wordcount: '1474'
ht-degree: 42%

---


# Assets HTTP API {#assets-http-api}

## 概要 {#overview}

The Assets HTTP API allows for create-read-update-delete (CRUD) operations on digital assets, including on metadata, on renditions, and on comments, together with structured content using [!DNL Experience Manager] Content Fragments. この API は `/api/assets` で公開されており、REST API として実装されています。[コンテンツフラグメントをサポート](/help/assets/assets-api-content-fragments.md)しています。

この API にアクセスするには、次の手順を実行します。

1. API サービスドキュメント（`https://[hostname]:[port]/api.json`）を開きます。
1. `https://[hostname]:[server]/api/assets.json` への Assets サービスリンクをクリックします。

API の応答は、一部の MIME タイプに対する JSON ファイル、およびすべての MIME タイプに対する応答コードです。JSON 応答はオプションであり、PDF ファイルなどでは利用できない場合があります。詳細な分析やアクションをおこなう場合は、応答コードを利用します。

After the [!UICONTROL Off Time], an asset and its renditions are not available via the [!DNL Assets] web interface and through the HTTP API. [!UICONTROL オンタイム]が未来の場合、または[!UICONTROL オフタイム]が過去の場合、API は 404 エラーメッセージを返します。

>[!NOTE]
>
>アセットやバイナリ一般（レンディションなど）のアップロードまたは更新に関連する API 呼び出しはすべて、AEM as a Cloud Service デプロイメントでは廃止されます。バイナリをアップロードする場合は、代わりに、[直接バイナリアップロード API](developer-reference-material-apis.md#asset-upload-technical) を使用します。

## コンテンツフラグメント {#content-fragments}

[コンテンツフラグメント](/help/assets/content-fragments/content-fragments.md)は特殊なタイプのアセットです。テキスト、数値、日付などの構造化データにアクセスするために使用できます。`standard` アセット（画像やドキュメントなど）とはいくつかの違いがあるので、コンテンツフラグメントの処理にはいくつかの追加ルールが適用されます。

For further information see [Content Fragments Support in the Experience Manager Assets HTTP API](/help/assets/assets-api-content-fragments.md).

## データモデル {#data-model}

Assets HTTP API は、フォルダーとアセット（標準アセット用）という 2 つの主要要素を公開します。

さらに、コンテンツフラグメント内の構造化コンテンツを記述するカスタムデータモデルに対する詳細な要素が公開されます。詳しくは、[コンテンツフラグメントのデータモデル](/help/assets/assets-api-content-fragments.md#content-models-and-content-fragments)を参照してください。

### フォルダー {#folders}

フォルダーは、従来のファイルシステムにおけるディレクトリに似ています。フォルダーは、他のフォルダーまたはアセットのコンテナです。フォルダーには、以下のコンポーネントがあります。

**エンティティ**：フォルダーのエンティティはフォルダーの子要素で、フォルダーまたはアセットです。

**プロパティ**：

* `name` は、フォルダの名前です。 これは、URLパス内の最後のセグメントに拡張子がない場合と同じです。
* `title` は、フォルダ名の代わりに表示できるフォルダのオプションのタイトルです。

>[!NOTE]
>
>フォルダーまたはアセットの一部のプロパティは、異なるプレフィックスにマップされます。`jcr:title`、`jcr:description`、`jcr:language` の `jcr` プレフィックスは `dc` プレフィックスに置き換えられます。したがって、返された JSON コードで、`dc:title`、`dc:description` にはそれぞれ `jcr:title`、`jcr:description` の値が含まれています。

**リンク**&#x200B;フォルダーは、次の 3 つのリンクを公開します。

* `self`：自分自身へのリンク。
* `parent`: 親フォルダーにリンクします。
* `thumbnail`: （オプション）フォルダーのサムネール画像へのリンク。

### Assets {#assets}

In [!DNL Experience Manager] an asset contains the following elements:

* アセットのプロパティとメタデータ.
* オリジナルのレンディション（最初にアップロードされたアセット）、サムネール、その他の各種レンディションなど複数のレンディション。追加のレンディションには、様々なサイズの画像、ビデオエンコーディングの画像、PDFまたはAdobe InDesignファイルから抽出したページなどがあります。
* オプションのコメント.

For information about elements in Content Fragments see [Content Fragments Support in Experience Manager Assets HTTP API](/help/assets/assets-api-content-fragments.md).

In [!DNL Experience Manager] a folder has the following components:

* エンティティ： アセットの子はレンディションです。
* プロパティ.
* リンク.

Assets HTTP API には、以下の機能が含まれます。

* フォルダーのリストの取得.
* フォルダーの作成.
* アセットを作成します（非推奨）。
* アセットバイナリを更新します（非推奨）。
* アセットメタデータの更新.
* アセットレンディションの作成.
* アセットレンディションの更新.
* アセットコメントの作成.
* フォルダーまたはアセットのコピー.
* フォルダーまたはアセットの移動.
* フォルダー、アセットまたはレンディションの削除.

>[!NOTE]
>
>読みやすいように、以下の例では、すべての cURL 表記法を省略しています。In fact the notation does correlate with [Resty](https://github.com/micha/resty) which is a script wrapper for `cURL`.

<!-- TBD: The Console Manager is not available now. So how to configure the below? 

**Prerequisites**

* Go to `https://[aem_server]:[port]/system/console/configMgr`.
* Navigate to **Adobe Granite CSRF Filter**.
* Make sure the property **Filter Methods** includes: POST, PUT, DELETE.
-->

## フォルダーのリストの取得 {#retrieve-a-folder-listing}

既存のフォルダーとその子エンティティ（サブフォルダーまたはアセット）の Siren 表現を取得します。

**リクエスト**: `GET /api/assets/myFolder.json`

**応答コード**: 応答コードは次のとおりです。

* 200 - OK — 成功。
* 404 - NOT FOUND — フォルダーが存在しないか、アクセスできません。
* 500 — 内部サーバーエラー — 他の問題が発生した場合。

**応答**: 返されるエンティティのクラスは、アセットまたはフォルダーです。 含まれるエンティティのプロパティは、各エンティティの完全なプロパティセットのサブセットです。 エンティティのすべての表現を取得するために、クライアントは `rel` が `self` となっているリンクで参照される URL のコンテンツを取得する必要があります。

## フォルダーの作成 {#create-a-folder}

指定されたパスに新しい `sling`:`OrderedFolder` を作成します。If a `*` is provided instead of a node name, the servlet uses the parameter name as node name. リクエストデータとして受け入れられるのは、新しいフォルダーの Siren 表現か、`application/www-form-urlencoded` または `multipart`/`form`-`data` としてエンコードされた名前と値のペアのセットで、HTML フォームから直接フォルダーを作成するのに役立ちます。さらに、フォルダーのプロパティを URL クエリパラメーターとして指定できます。

指定されたパスの親ノードが存在しない場合、API呼び出しは `500` 応答コードで失敗します。 フォルダーが既に存在する場合、呼び出しは応答コード `409` を返します。

**パラメータ**: `name` はフォルダー名です。

**リクエスト**

* `POST /api/assets/myFolder -H"Content-Type: application/json" -d '{"class":"assetFolder","properties":{"title":"My Folder"}}'`
* `POST /api/assets/* -F"name=myfolder" -F"title=My Folder"`

**応答コード**: 応答コードは次のとおりです。

* 201 — 作成済み — 作成が成功した場合。
* 409 - CONFLICT — フォルダーが既に存在する場合。
* 412 - PRECONDITION FAILED — ルートコレクションが見つからないか、アクセスできない場合。
* 500 — 内部サーバーエラー — 他の問題が発生した場合。

## アセットの作成 {#create-an-asset}

API を使用してアセットを作成する方法については、[アセットのアップロード](developer-reference-material-apis.md)を参照してください。HTTP API を使用したアセットの作成は非推奨（廃止予定）となりました。

## アセットバイナリの更新 {#update-asset-binary}

API を使用してアセットバイナリを更新する方法については、[アセットのアップロード](developer-reference-material-apis.md)を参照してください。HTTP API を使用したアセットバイナリの更新は非推奨（廃止予定）となりました。

## アセットのメタデータの更新 {#update-asset-metadata}

アセットメタデータのプロパティを更新します。名前空間内のプロパティを更新すると、APIは `dc:` 名前空間内の同じプロパティを更新し `jcr` ます。 APIは、2つの名前空間の下のプロパティを同期しません。

**リクエスト**: `PUT /api/assets/myfolder/myAsset.png -H"Content-Type: application/json" -d '{"class":"asset", "properties":{"dc:title":"My Asset"}}'`

**応答コード**: 応答コードは次のとおりです。

* 200 - OK — アセットが正常に更新された場合。
* 404 — 見つかりません — 指定したURIでアセットが見つからなかったか、アクセスできなかった場合。
* 412 - PRECONDITION FAILED — ルートコレクションが見つからないか、アクセスできない場合。
* 500 — 内部サーバーエラー — 他の問題が発生した場合。

## アセットレンディションの作成 {#create-an-asset-rendition}

アセット用の新しいアセットレンディションを作成します。 リクエストパラメーター名が指定されない場合、ファイル名がレンディション名として使用されます。

**パラメータ**: パラメーターは、レンディション `name` の名前とファイル参照 `file` を表します。

**リクエスト**

* `POST /api/assets/myfolder/myasset.png/renditions/web-rendition -H"Content-Type: image/png" --data-binary "@myRendition.png"`
* `POST /api/assets/myfolder/myasset.png/renditions/* -F"name=web-rendition" -F"file=@myRendition.png"`

**応答コード**

* 201 — 作成済み — レンディションが正常に作成された場合。
* 404 — 見つかりません — 指定したURIでアセットが見つからなかったか、アクセスできなかった場合。
* 412 - PRECONDITION FAILED — ルートコレクションが見つからないか、アクセスできない場合。
* 500 — 内部サーバーエラー — 他の問題が発生した場合。

## アセットレンディションの更新 {#update-an-asset-rendition}

アセットレンディションをそれぞれ新しいバイナリデータで置き換えて更新します。

**リクエスト**: `PUT /api/assets/myfolder/myasset.png/renditions/myRendition.png -H"Content-Type: image/png" --data-binary @myRendition.png`

**応答コード**: 応答コードは次のとおりです。

* 200 - OK — レンディションが正常に更新された場合。
* 404 — 見つかりません — 指定したURIでアセットが見つからなかったか、アクセスできなかった場合。
* 412 - PRECONDITION FAILED — ルートコレクションが見つからないか、アクセスできない場合。
* 500 — 内部サーバーエラー — 他の問題が発生した場合。

## 資産追加に対するコメント {#create-an-asset-comment}

新しいアセットコメントを作成します。

**パラメーター**: パラメーターは、コメント `message` のメッセージ本文と、JSON形式 `annotationData` のAnnotationデータ用です。

**リクエスト**: `POST /api/assets/myfolder/myasset.png/comments/* -F"message=Hello World." -F"annotationData={}"`

**応答コード**: 応答コードは次のとおりです。

* 201 — コメントが正常に作成された場合は、作成済み。
* 404 — 見つかりません — 指定したURIでアセットが見つからなかったか、アクセスできなかった場合。
* 412 - PRECONDITION FAILED — ルートコレクションが見つからないか、アクセスできない場合。
* 500 — 内部サーバーエラー — 他の問題が発生した場合。

## フォルダーまたはアセットのコピー {#copy-a-folder-or-asset}

指定されたパスで使用可能なフォルダーまたはアセットを新しい保存先にコピーします。

**Request Headers**: パラメーターは次のとおりです。

* `X-Destination` - APIソリューションスコープ内の、リソースのコピー先となる新しい宛先URI。
* `X-Depth`  — または `infinity` のいずれか `0`。 を使用すると、リソースとそのプロパティのみがコピーされ、子はコピーされません。 `0`
* `X-Overwrite`  — 既存の宛先 `F` でアセットが上書きされないようにするために使用します。

**リクエスト**: `COPY /api/assets/myFolder -H"X-Destination: /api/assets/myFolder-copy"`

**応答コード**: 応答コードは次のとおりです。

* 201 — 作成済み — フォルダー/アセットが既存の保存先以外にコピーされた場合。
* 204 — コンテンツなし — フォルダーまたはアセットが既存の宛先にコピーされた場合。
* 412 - PRECONDITION FAILED — リクエストヘッダーが見つからない場合。
* 500 — 内部サーバーエラー — 他の問題が発生した場合。

## フォルダーまたはアセットの移動 {#move-a-folder-or-asset}

指定されたパスのフォルダーまたはアセットを新しい宛先に移動します。

**リクエストヘッダー**: パラメーターは次のとおりです。

* `X-Destination` - APIソリューションスコープ内の、リソースのコピー先となる新しい宛先URI。
* `X-Depth`  — または `infinity` のいずれか `0`。 を使用すると、リソースとそのプロパティのみがコピーされ、子はコピーされません。 `0`
* `X-Overwrite`  — 既存のリソース `T` を強制的に削除する場合、または既存のリソースを上書きしない `F` 場合に使用します。

**リクエスト**: `MOVE /api/assets/myFolder -H"X-Destination: /api/assets/myFolder-moved"`

**応答コード**: 応答コードは次のとおりです。

* 201 — 作成済み — フォルダー/アセットが既存の保存先以外にコピーされた場合。
* 204 — コンテンツなし — フォルダーまたはアセットが既存の宛先にコピーされた場合。
* 412 - PRECONDITION FAILED — リクエストヘッダーが見つからない場合。
* 500 — 内部サーバーエラー — 他の問題が発生した場合。

## フォルダー、アセットまたはレンディションの削除 {#delete-a-folder-asset-or-rendition}

指定されたパスでリソース(-tree)を削除します。

**リクエスト**

* `DELETE /api/assets/myFolder`
* `DELETE /api/assets/myFolder/myAsset.png`
* `DELETE /api/assets/myFolder/myAsset.png/renditions/original`

**応答コード**: 応答コードは次のとおりです。

* 200 - OK — フォルダーが正常に削除された場合。
* 412 - PRECONDITION FAILED — ルートコレクションが見つからないか、アクセスできない場合。
* 500 — 内部サーバーエラー — 他の問題が発生した場合。
