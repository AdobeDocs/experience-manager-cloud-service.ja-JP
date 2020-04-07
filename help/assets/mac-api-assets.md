---
title: Assets HTTP API
description: Assets HTTP API の実装、データモデルおよび機能を学習します。Assets HTTP API を使用して、アセットに関する様々なタスクを実行できます。
contentOwner: AG
translation-type: tm+mt
source-git-commit: 26833f59f21efa4de33969b7ae2e782fe5db8a14

---


# Assets HTTP API {#assets-http-api}

## 概要 {#overview}

Assets HTTP API を使用すれば、アセットに対する作成、読み取り、更新、削除（CRUD）操作を実行できます。アセットにはバイナリ、メタデータ、レンディション、コメントが含まれるほか、AEM コンテンツフラグメントを使用した構造化コンテンツも含まれます。この API は `/api/assets` で公開されており、REST API として実装されています。[コンテンツフラグメントをサポート](content-fragments/content-fragments.md)しています。

この API にアクセスするには、次の手順を実行します。

1. API サービスドキュメント（`https://[hostname]:[port]/api.json`）を開きます。
1. `https://[hostname]:[server]/api/assets.json` への Assets サービスリンクをクリックします。

API応答は、一部のMIMEタイプのJSONファイルで、すべてのMIMEタイプの応答コードです。 JSON 応答はオプションであり、PDF ファイルなどでは利用できない場合があります。詳細な分析やアクションをおこなう場合は、応答コードを利用します。

[!UICONTROL オフタイム]の経過後、アセットとそのレンディションは、Assets Web インターフェイスでも HTTP API でも使用できません。[!UICONTROL オンタイム]が未来の場合、または[!UICONTROL オフタイム]が過去の場合、API は 404 エラーメッセージを返します。

>[!NOTE]
>
>アセットやバイナリ一般（レンディションなど）のアップロードまたは更新に関連する API 呼び出しはすべて、AEM as a Cloud Service デプロイメントでは廃止されます。For uploading binaries, use [direct binary upload APIs](developer-reference-material-apis.md#asset-upload-technical) instead.

## コンテンツフラグメント {#content-fragments}

[コンテンツフラグメント](content-fragments/content-fragments.md)は特殊なタイプのアセットです。テキスト、数値、日付などの構造化データにアクセスするために使用できます。`standard` アセット（画像やドキュメントなど）とはいくつかの違いがあるので、コンテンツフラグメントの処理にはいくつかの追加ルールが適用されます。

詳しくは、[AEM Assets HTTP API でのコンテンツフラグメントのサポート](content-fragments/content-fragments.md)を参照してください。

## データモデル {#data-model}

Assets HTTP API は、フォルダーとアセット（標準アセット用）という 2 つの主要要素を公開します。

さらに、コンテンツフラグメント内の構造化コンテンツを記述するカスタムデータモデルに対する詳細な要素が公開されます。詳しくは、[コンテンツフラグメントのデータモデル](content-fragments/content-fragments.md)を参照してください。

### フォルダー {#folders}

フォルダーは、従来のファイルシステムにおけるディレクトリに似ています。フォルダーは、他のフォルダーまたはアセットのコンテナです。フォルダーには、以下のコンポーネントがあります。

**エンティティ**：フォルダーのエンティティはフォルダーの子要素で、フォルダーまたはアセットです。

**プロパティ**：
* `name` -- フォルダーの名前です。これは、URL パスの最後のセグメント（拡張子を除く）と同じです。
* `title` -- 名前の代わりに表示できるフォルダータイトル（オプション）です。

>[!NOTE]
>
>フォルダーまたはアセットの一部のプロパティは、異なるプレフィックスにマップされます。`jcr:title`、`jcr:description`、`jcr:language` の `jcr` プレフィックスは `dc` プレフィックスに置き換えられます。したがって、返された JSON コードで、`dc:title`、`dc:description` にはそれぞれ `jcr:title`、`jcr:description` の値が含まれています。

**リンク**&#x200B;フォルダーは、次の 3 つのリンクを公開します。
* `self`：自分自身へのリンク
* `parent`：親フォルダーへのリンク
* `thumbnail`：（オプション）フォルダーのサムネール画像へのリンク

### アセット {#assets}

AEM では、アセットには次の要素が含まれています。

* アセットのプロパティとメタデータ
* オリジナルのレンディション（最初にアップロードされたアセット）、サムネール、その他の各種レンディションなど複数のレンディション。追加レンディションは、サイズやビデオエンコーディングの異なる画像や、PDF または InDesign から抽出されたページの場合があります。
* オプションのコメント

コンテンツフラグメントの要素については、[AEM Assets HTTP API でのコンテンツフラグメントのサポート](content-fragments/content-fragments.md)を参照してください。

AEM では、フォルダーには次のコンポーネントが含まれています。

* エンティティ：アセットの子はアセットのレンディションです。
* プロパティ
* リンク

Assets HTTP API は以下の機能を提供します。

* フォルダーのリストの取得
* フォルダーの作成
* アセットの作成（廃止予定）
* アセットバイナリの更新（廃止予定）
* アセットメタデータの更新
* アセットレンディションの作成
* アセットレンディションの更新
* アセットコメントの作成
* フォルダーまたはアセットのコピー
* フォルダーまたはアセットの移動
* フォルダー、アセットまたはレンディションの削除

>[!NOTE]
>
>読みやすいように、以下の例では、すべての cURL 表記法を省略しています。実際には、この表記法は cURL 用のスクリプトラッパーである [Resty](https://github.com/micha/resty) と関連があります。

<!-- TBD: The Console Manager is not available now. So how to configure the below? 

**Prerequisites**

* Go to `https://[aem_server]:[port]/system/console/configMgr`.
* Navigate to **Adobe Granite CSRF Filter**.
* Make sure the property **Filter Methods** includes: POST, PUT, DELETE.
-->

## フォルダーのリストの取得 {#retrieve-a-folder-listing}

既存のフォルダーとその子エンティティ（サブフォルダーまたはアセット）の Siren 表現を取得します。

**リクエスト**

```
GET /api/assets/myFolder.json
```

**応答コード**

```
200 - OK - success
404 - NOT FOUND - folder does not exist or is not accessible
500 - INTERNAL SERVER ERROR - if something else goes wrong
```

**応答**

返されるエンティティのクラスは assets/folder です。

含まれるエンティティのプロパティは、各エンティティの完全なプロパティセットのサブセットです。エンティティのすべての表現を取得するために、クライアントは `rel` が `self` となっているリンクで参照される URL のコンテンツを取得する必要があります。

## フォルダーの作成 {#create-a-folder}

指定されたパスに新しい `sling`:`OrderedFolder` を作成します。ノード名の代わりに「*」が指定されている場合、サーブレットはパラメーター名をノード名として使用します。リクエストデータとして受け入れられるのは、新しいフォルダーの Siren 表現か、`application/www-form-urlencoded` または `multipart`/`form`-`data` としてエンコードされた名前と値のペアのセットで、HTML フォームから直接フォルダーを作成するのに役立ちます。さらに、フォルダーのプロパティを URL クエリパラメーターとして指定できます。

指定されたパスの親ノードが存在しない場合、この操作は失敗し、応答コード `500` が返されます。フォルダーが既に存在する場合、応答コード `409` が返されます。

**パラメーター**

* `name` - フォルダー名

**リクエスト**

```
POST /api/assets/myFolder -H"Content-Type: application/json" -d '{"class":"assetFolder","properties":{"title":"My Folder"}}'
```

または

```
POST /api/assets/* -F"name=myfolder" -F"title=My Folder"
```

**応答コード**

```
201 - CREATED - on successful creation
409 - CONFLICT - if folder already exist
412 - PRECONDITION FAILED - if root collection cannot be found or accessed
500 - INTERNAL SERVER ERROR - if something else goes wrong
```

## アセットの作成 {#create-an-asset}

API を使用してアセットを作成する方法については、[アセットのアップロード](developer-reference-material-apis.md)を参照してください。HTTP API を使用したアセットの作成は非推奨（廃止予定）となりました。

## アセットバイナリの更新 {#update-asset-binary}

API を使用してアセットバイナリを更新する方法については、[アセットのアップロード](developer-reference-material-apis.md)を参照してください。HTTP API を使用したアセットバイナリの更新は非推奨（廃止予定）となりました。

## アセットのメタデータの更新 {#update-asset-metadata}

アセットメタデータのプロパティを更新します。

**リクエスト**

```
PUT /api/assets/myfolder/myAsset.png -H"Content-Type: application/json" -d '{"class":"asset", "properties":{"dc:title":"My Asset"}}'
```

**応答コード**

```
200 - OK - if Asset has been updated successfully
404 - NOT FOUND - if Asset could not be found or accessed at the provided URI
412 - PRECONDITION FAILED - if root collection cannot be found or accessed
500 - INTERNAL SERVER ERROR - if something else goes wrong
```

## アセットレンディションの作成 {#create-an-asset-rendition}

アセットの新しいアセットレンディションを作成します。リクエストパラメーター名が指定されない場合、ファイル名がレンディション名として使用されます。

**パラメーター**

* `name` - レンディション名
* `file` - ファイル参照

**リクエスト**

```
POST /api/assets/myfolder/myasset.png/renditions/web-rendition -H"Content-Type: image/png" --data-binary "@myRendition.png"
```

または

```
POST /api/assets/myfolder/myasset.png/renditions/* -F"name=web-rendition" -F"file=@myRendition.png"
```

**応答コード**

```
201 - CREATED - if Rendition has been created successfully
404 - NOT FOUND - if Asset could not be found or accessed at the provided URI
412 - PRECONDITION FAILED - if root collection cannot be found or accessed
500 - INTERNAL SERVER ERROR - if something else goes wrong
```

## アセットレンディションの更新 {#update-an-asset-rendition}

アセットレンディションをそれぞれ新しいバイナリデータで置き換えて更新します。

**リクエスト**

```
PUT /api/assets/myfolder/myasset.png/renditions/myRendition.png -H"Content-Type: image/png" --data-binary @myRendition.png
```

**応答コード**

```
200 - OK - if Rendition has been updated successfully
404 - NOT FOUND - if Asset could not be found or accessed at the provided URI
412 - PRECONDITION FAILED - if root collection cannot be found or accessed
500 - INTERNAL SERVER ERROR - if something else goes wrong
```

## アセットコメントの作成 {#create-an-asset-comment}

新しいアセットコメントを作成します。

**パラメーター**

* `message` - メッセージ
* `annotationData` - 注釈データ（JSON）

**リクエスト**

```
POST /api/assets/myfolder/myasset.png/comments/* -F"message=Hello World." -F"annotationData={}"
```

**応答コード**

```
201 - CREATED - if Comment has been created successfully
404 - NOT FOUND - if Asset could not be found or accessed at the provided URI
412 - PRECONDITION FAILED - if root collection cannot be found or accessed
500 - INTERNAL SERVER ERROR - if something else goes wrong
```

## フォルダーまたはアセットのコピー {#copy-a-folder-or-asset}

指定されたパスのフォルダーまたはアセットを新しい宛先にコピーします。

**リクエストヘッダー**

```
X-Destination - a new destination URI within the API solution scope to copy the resource to
X-Depth - either 'infinity' or '0'. The value '0' only copies the resource and its properties, no children.
X-Overwrite - 'F' to prevent overwriting an existing destination
```

**リクエスト**

```
COPY /api/assets/myFolder -H"X-Destination: /api/assets/myFolder-copy"
```

**応答コード**

```
201 - CREATED - if folder/asset has been copied to a non-existing destination
204 - NO CONTENT - if the folder/asset has been copied to an existing destination
412 - PRECONDITION FAILED - if a request header is missing or
500 - INTERNAL SERVER ERROR - if something else goes wrong
```

## フォルダーまたはアセットの移動 {#move-a-folder-or-asset}

指定されたパスのフォルダーまたはアセットを新しい宛先に移動します。

**リクエストヘッダー**

```
X-Destination - a new destination URI within the API solution scope to copy the resource to
X-Depth - either 'infinity' or '0'. The value '0' only copies the resource and its properties, no children.
X-Overwrite - either 'T' to force deletion of existing resources or 'F' to prevent overwriting an existing resource.
```

**リクエスト**

```
MOVE /api/assets/myFolder -H"X-Destination: /api/assets/myFolder-moved"
```

**応答コード**

```
201 - CREATED - if folder/asset has been copied to a non-existing destination
204 - NO CONTENT - if the folder/asset has been copied to an existing destination
412 - PRECONDITION FAILED - if a request header is missing or
500 - INTERNAL SERVER ERROR - if something else goes wrong
```

## フォルダー、アセットまたはレンディションの削除 {#delete-a-folder-asset-or-rendition}

指定されたパスのリソース（ツリー）を削除します。

**リクエスト**

```
DELETE /api/assets/myFolder
```

または

```
DELETE /api/assets/myFolder/myAsset.png
```

または

```xml
DELETE /api/assets/myFolder/myAsset.png/renditions/original
```

**応答コード**

```
200 - OK - if folder has been deleted successfully
412 - PRECONDITION FAILED - if root collection cannot be found or accessed
500 - INTERNAL SERVER ERROR - if something else goes wrong
```

