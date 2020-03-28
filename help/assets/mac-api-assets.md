---
title: Assets HTTP API
description: Assets HTTP API の実装、データモデルおよび機能を学習します。Assets HTTP API を使用して、アセットに関する様々なタスクを実行できます。
contentOwner: AG
translation-type: tm+mt
source-git-commit: 068195919c4bf73c41b1156eadb47544e4c41e65

---


# Assets HTTP API {#assets-http-api}

## 概要 {#overview}

Assets HTTP APIを使用すると、バイナリ、メタデータ、レンディション、コメントなどのアセットに対して、AEMコンテンツフラグメントを使用して構造化されたコンテンツと共に、作成/読み取り/更新/削除(CRUD)操作を実行できます。 REST APIとして実装さ `/api/assets` れ、で公開されています。 [コンテンツフラグメントをサポート](content-fragments/content-fragments.md)しています。

この API にアクセスするには、次の手順を実行します。

1. Open the API service document at `https://[hostname]:[port]/api.json`.
1. Follow the Assets service link leading to `https://[hostname]:[server]/api/assets.json`.

API応答は、一部のMIMEタイプのJSONファイルで、すべてのMIMEタイプの応答コードです。 JSON 応答はオプションであり、PDF ファイルなどでは利用できない場合があります。詳細な分析やアクションをおこなう場合は、応答コードを利用します。

「オフ」の [!UICONTROL 後は]、アセットとそのレンディションは、アセットWebインターフェイスまたはHTTP API経由では使用できなくなります。 オン時間が未来の場合、またはオ [!UICONTROL フ時間が過去の場合] 、APIは404 [!UICONTROL エラーメッセージを返します] 。

>[!NOTE]
>
>アセットやバイナリの一般的なアップロードまたは更新（レンディションなど）に関連するすべてのAPI呼び出しは、AEMのクラウドサービスのデプロイメント用に展開されます。 バイナリをアップロードする場合は、代わ [りに直接バイナリアップロードAPI](developer-reference-material-apis.md#asset-upload-technical) 。

## コンテンツフラグメント {#content-fragments}

[コンテンツフラグメント](content-fragments/content-fragments.md)は特殊なタイプのアセットです。テキスト、数値、日付などの構造化データにアクセスするために使用できます。As there are several differences to `standard` assets (such as images or documents), some additional rules apply to handling content fragments.

詳しくは、[AEM Assets HTTP API でのコンテンツフラグメントのサポート](content-fragments/content-fragments.md)を参照してください。

## データモデル {#data-model}

Assets HTTP API は、フォルダーとアセット（標準アセット用）という 2 つの主要要素を公開します。

さらに、コンテンツフラグメント内の構造化コンテンツを記述するカスタムデータモデルに対する詳細な要素が公開されます。詳しくは、[コンテンツフラグメントのデータモデル](content-fragments/content-fragments.md)を参照してください。

### フォルダー {#folders}

フォルダは、従来のファイルシステムのディレクトリに似ています。 フォルダーは、他のフォルダーまたはアセットのコンテナです。フォルダーには、以下のコンポーネントがあります。

**エンティティ**:フォルダのエンティティは子要素で、フォルダやアセットを指定できます。

**プロパティ**:
* `name`   — フォルダの名前。 これは、URLパス内の最後のセグメント（拡張子なし）と同じです。
* `title`  — 名前の代わりに表示できるフォルダのオプションのタイトル。

>[!NOTE]
>
>フォルダーまたはアセットの一部のプロパティは、異なるプレフィックスにマップされます。のプレフ `jcr` ィックス、およびは、プレフィックスに置き `jcr:title`換えられるプレフィックスに `jcr:description``jcr:language``dc` 置き換えられます。 Hence in the returned JSON, `dc:title` and `dc:description` contain the values of `jcr:title` and `jcr:description`, respectively.

**Links** Foldersは、次の3つのリンクを公開します。
* `self`:自身にリンク
* `parent`:親フォルダーへのリンク
* `thumbnail`:（オプション）フォルダーのサムネール画像へのリンク

### Assets {#assets}

AEMでは、アセットに次の要素が含まれます。

* アセットのプロパティとメタデータ
* オリジナルのレンディション（最初にアップロードされたアセット）、サムネール、その他の各種レンディションなど複数のレンディション。追加レンディションは、サイズやビデオエンコーディングの異なる画像や、PDF または InDesign から抽出されたページの場合があります。
* オプションのコメント

コンテンツフラグメントの要素については、[AEM Assets HTTP API でのコンテンツフラグメントのサポート](content-fragments/content-fragments.md)を参照してください。

AEMのフォルダーには、次のコンポーネントが含まれます。

* エンティティ：アセットの子はレンディションです。
* プロパティ
* リンク

Assets HTTP APIには次の機能があります。

* フォルダーの一覧の取得
* フォルダーの作成
* アセットの作成 (廃止)
* アセットバイナリの更新（非推奨）
* アセットメタデータの更新
* アセットレンディションの作成
* アセットレンディションの更新
* アセットコメントの作成
* フォルダーまたはアセットのコピー
* フォルダーまたはアセットの移動
* フォルダー、アセットまたはレンディションの削除

>[!NOTE]
>
>読みやすいように、以下の例では、すべての cURL 表記法を省略しています。In fact the notation does correlate with [Resty](https://github.com/micha/resty) which is a script wrapper for cURL.

<!-- TBD: The Console Manager is not available now. So how to configure the below? 

**Prerequisites**

* Go to `https://[aem_server]:[port]/system/console/configMgr`.
* Navigate to **Adobe Granite CSRF Filter**.
* Make sure the property **Filter Methods** includes: POST, PUT, DELETE.
-->

## フォルダーの一覧の取得 {#retrieve-a-folder-listing}

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

返されるエンティティのクラスは、assets/folderです。

含まれるエンティティのプロパティは、各エンティティの完全なプロパティセットのサブセットです。In order to obtain a full representation of the entity, clients should retrieve the contents of the URL pointed to by the link with a `rel` of `self`.

## フォルダーの作成 {#create-a-folder}

Creates a new `sling`: `OrderedFolder` at the given path. ノード名の代わりに*を指定した場合、サーブレットはノード名としてパラメータ名を使用します。 Accepted as request data is either a Siren representation of the new folder or a set of name-value pairs, encoded as `application/www-form-urlencoded` or `multipart`/ `form`- `data`, useful for creating a folder directly from an HTML form. さらに、フォルダーのプロパティを URL クエリパラメーターとして指定できます。

The operation will fail with a `500` response code if the parent node of the given path does not exist. If the folder already exists a `409` response code is returned.

**パラメーター**

* `name`  — フォルダ名

**リクエスト**

```
POST /api/assets/myFolder -H"Content-Type: application/json" -d '{"class":"assetFolder","properties":{"title":"My Folder"}}'
```

 か  のどちらかにする必要があります。

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

APIを使用し [てアセットを作成する方法については](developer-reference-material-apis.md) 、アセットのアップロードを参照してください。 HTTP APIを使用したアセットの作成は非推奨です。

## アセットバイナリの更新 {#update-asset-binary}

APIを使用し [てアセットバイナリを更新する方法については](developer-reference-material-apis.md) 、アセットのアップロードを参照してください。 HTTP APIを使用したアセットバイナリの更新は推奨されません。

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

アセットの新しいアセットレンディションを作成します。要求パラメーター名が指定されていない場合、ファイル名がレンディション名として使用されます。

**パラメーター**

* `name`  — レンディション名
* `file`  — ファイル参照

**リクエスト**

```
POST /api/assets/myfolder/myasset.png/renditions/web-rendition -H"Content-Type: image/png" --data-binary "@myRendition.png"
```

 か  のどちらかにする必要があります。

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
* `annotationData`  — 注釈データ(JSON)

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

## Copy a folder or an asset {#copy-a-folder-or-asset}

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

## Move a folder or an asset {#move-a-folder-or-asset}

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

## フォルダ、アセットまたはレンディションの削除 {#delete-a-folder-asset-or-rendition}

指定されたパスのリソース（ツリー）を削除します。

**リクエスト**

```
DELETE /api/assets/myFolder
```

 か  のどちらかにする必要があります。

```
DELETE /api/assets/myFolder/myAsset.png
```

 か  のどちらかにする必要があります。

```xml
DELETE /api/assets/myFolder/myAsset.png/renditions/original
```

**応答コード**

```
200 - OK - if folder has been deleted successfully
412 - PRECONDITION FAILED - if root collection cannot be found or accessed
500 - INTERNAL SERVER ERROR - if something else goes wrong
```

