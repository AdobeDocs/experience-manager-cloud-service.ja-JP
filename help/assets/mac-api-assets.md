---
title: Assets HTTP API
description: ' [!DNL Experience Manager Assets] の HTTP API を使用した、デジタルアセットの作成、読み取り、更新、削除、管理について説明します。'
contentOwner: AG
feature: Assets HTTP API、API
role: Developer,Architect,Admin
exl-id: a3b7374d-f24b-4d6f-b6db-b9c9c962bb8d
source-git-commit: a2c2a1f4ef4a8f0cf1afbba001d24782a6a2a24e
workflow-type: ht
source-wordcount: '1519'
ht-degree: 100%

---

# [!DNL Adobe Experience Manager Assets] HTTP API {#assets-http-api}

## 概要 {#overview}

[!DNL Assets] HTTP API を使用すれば、デジタルアセット（メタデータ、レンディション、コメントのほか、[!DNL Experience Manager] コンテンツフラグメントを使用した構造化コンテンツも含む）に対して作成、読み取り、更新、削除（CRUD）操作を実行できます。この API は `/api/assets` で公開されており、REST API として実装されています。[コンテンツフラグメントをサポート](/help/assets/content-fragments/assets-api-content-fragments.md)しています。

この API にアクセスするには、次の手順を実行します。

1. API サービスドキュメント（`https://[hostname]:[port]/api.json`）を開きます。
1. `https://[hostname]:[server]/api/assets.json` への [!DNL Assets] サービスリンクをクリックします。

API の応答は、一部の MIME タイプに対する JSON ファイル、およびすべての MIME タイプに対する応答コードです。JSON 応答はオプションであり、PDF ファイルなどでは利用できない場合があります。詳細な分析やアクションを行う場合は、応答コードを利用します。

>[!NOTE]
>
>アセットやバイナリ一般（レンディションなど）のアップロードまたは更新に関連する API 呼び出しはすべて、[!DNL Experience Manager] as a [!DNL Cloud Service] デプロイメントでは廃止されています。バイナリをアップロードする場合は、代わりに、[直接バイナリアップロード API](developer-reference-material-apis.md#asset-upload) を使用します。

## コンテンツフラグメント {#content-fragments}

[コンテンツフラグメント](/help/assets/content-fragments/content-fragments.md)は特殊なタイプのアセットです。テキスト、数値、日付などの構造化データにアクセスするために使用できます。`standard` アセット（画像やドキュメントなど）とはいくつかの違いがあるので、コンテンツフラグメントの処理にはいくつかの追加ルールが適用されます。

詳しくは、[ [!DNL Experience Manager Assets]  HTTP API でのコンテンツフラグメントのサポート](/help/assets/content-fragments/assets-api-content-fragments.md)を参照してください。

## データモデル {#data-model}

[!DNL Assets] HTTP API は、フォルダーとアセット（標準アセット用）という 2 つの主要要素を公開します。さらに、コンテンツフラグメント内の構造化コンテンツを記述するカスタムデータモデルに対する詳細な要素が公開されます。詳しくは、[コンテンツフラグメントのデータモデル](/help/assets/content-fragments/assets-api-content-fragments.md#content-models-and-content-fragments)を参照してください。

### フォルダー {#folders}

フォルダーは、従来のファイルシステムにおけるディレクトリに似ています。フォルダーには、アセット、フォルダーのみ、またはフォルダーとアセットを含めることができます。フォルダーには、以下のコンポーネントがあります。

**エンティティ**：フォルダーのエンティティはフォルダーの子要素で、フォルダーまたはアセットです。

**プロパティ**：

* `name` はフォルダーの名前です。これは、URL パスの最後のセグメント（拡張子を除く）と同じです。
* `title` は名前の代わりに表示できるフォルダータイトル（オプション）です。

>[!NOTE]
>
>フォルダーまたはアセットの一部のプロパティは、異なるプレフィックスにマップされます。`jcr:title`、`jcr:description`、`jcr:language` の `jcr` プレフィックスは `dc` プレフィックスに置き換えられます。したがって、返された JSON コードで、`dc:title`、`dc:description` にはそれぞれ `jcr:title`、`jcr:description` の値が含まれています。

**リンク**&#x200B;フォルダーは、次の 3 つのリンクを公開します。

* `self`：自分自身へのリンク。
* `parent`：親フォルダーへのリンク。
* `thumbnail`：（オプション）フォルダーのサムネール画像へのリンク。

### Assets {#assets}

[!DNL Experience Manager] では、アセットには次の要素が含まれています。

* アセットのプロパティとメタデータ
* アセットの当初アップロードされたバイナリファイル。
* 設定に応じた複数のレンディション。サイズの異なる画像、エンコーディングが異なるビデオ、PDF または [!DNL Adobe InDesign] ファイルから抽出したページなどがあります。
* コメント（オプション）

コンテンツフラグメントの要素については、[AEM Assets HTTP API でのコンテンツフラグメントのサポート](/help/assets/content-fragments/assets-api-content-fragments.md)を参照してください。

[!DNL Experience Manager] では、フォルダーには次のコンポーネントが含まれています。

* エンティティ：アセットの子はアセットのレンディションです。
* プロパティ
* リンク

## 使用可能な機能 {#available-features}

[!DNL Assets] HTTP API には、以下の機能が含まれます。

* [フォルダーリストの取得](#retrieve-a-folder-listing)。
* [フォルダーの作成](#create-a-folder)。
* [アセットの作成（廃止）。](#create-an-asset)
* [アセットバイナリの更新（廃止）](#update-asset-binary)。
* [アセットメタデータの更新](#update-asset-metadata)。
* [アセットレンディションの作成](#create-an-asset-rendition)。
* [アセットレンディションの更新](#update-an-asset-rendition)。
* [アセットコメントの作成](#create-an-asset-comment)。
* [フォルダーまたはアセットのコピー](#copy-a-folder-or-asset)。
* [フォルダーまたはアセットの移動](#move-a-folder-or-asset)。
* [フォルダー、アセットまたはレンディションの削除](#delete-a-folder-asset-or-rendition)。

>[!NOTE]
>
>読みやすいように、以下の例では、完全な cURL 表記法を省略しています。この表記法は、cURL 用のスクリプトラッパーである [Resty](https://github.com/micha/resty) と関連があります。

<!-- TBD: The Console Manager is not available now. So how to configure the below? 

**Prerequisites**

* Go to `https://[aem_server]:[port]/system/console/configMgr`.
* Navigate to **Adobe Granite CSRF Filter**.
* Make sure the property **Filter Methods** includes: POST, PUT, DELETE.
-->

## フォルダーのリストの取得 {#retrieve-a-folder-listing}

既存のフォルダーとその子エンティティ（サブフォルダーまたはアセット）の Siren 表現を取得します。

**リクエスト**：`GET /api/assets/myFolder.json`

**応答コード**：応答コードは次のとおりです。

* 200 - OK（成功）
* 404 - NOT FOUND（フォルダーが存在しないかアクセスできない）
* 500 - INTERNAL SERVER ERROR（他に問題がある場合）

**応答**：返されるエンティティのクラスはアセットまたはフォルダーです。含まれるエンティティのプロパティは、各エンティティの完全なプロパティセットのサブセットです。エンティティのすべての表現を取得するために、クライアントは `rel` が `self` となっているリンクで参照される URL のコンテンツを取得する必要があります。

## フォルダーの作成 {#create-a-folder}

指定されたパスに `sling`:`OrderedFolder` を作成します。ノード名の代わりに「`*`」が指定されている場合、サーブレットパラメーター名がノード名として使用されます。リクエストでは、次のいずれかを受け付けます。

* 新しいフォルダーの Siren 表現
* `application/www-form-urlencoded` または `multipart`/`form` - `data` としてエンコードされた名前と値のペアのセット。これらは、HTML フォームから直接フォルダーを作成する場合に役立ちます。

また、フォルダーのプロパティを URL クエリパラメーターとして指定できます。

指定されたパスの親ノードが存在しない場合、API 呼び出しは失敗し、応答コード `500` が返されます。フォルダーが存在する場合、呼び出しは応答コード `409` を返します。

**パラメーター**：`name` はフォルダー名です。

**リクエスト**

* `POST /api/assets/myFolder -H"Content-Type: application/json" -d '{"class":"assetFolder","properties":{"title":"My Folder"}}'`
* `POST /api/assets/* -F"name=myfolder" -F"title=My Folder"`

**応答コード**：応答コードは次のとおりです。

* 201 - CREATED（作成が成功した場合）
* 409 - CONFLICT（フォルダーが存在する場合）
* 412 - PRECONDITION FAILED（ルートコレクションが見つからないかアクセスできない場合）
* 500 - INTERNAL SERVER ERROR（他に問題がある場合）

## アセットの作成 {#create-an-asset}

アセットの作成方法については、[アセットのアップロード](developer-reference-material-apis.md)を参照してください。HTTP API を使用してアセットを作成することはできません。

## アセットバイナリの更新 {#update-asset-binary}

アセットバイナリの更新方法については、[アセットのアップロード](developer-reference-material-apis.md)を参照してください。HTTP API を使用してアセットバイナリを更新することはできません。

## アセットのメタデータの更新 {#update-asset-metadata}

アセットメタデータのプロパティを更新します。`dc:` 名前空間内のプロパティを更新すると、API は `jcr` 名前空間内の同じプロパティをアップデートします。API は 2 つの名前空間内のプロパティを同期させません。

**リクエスト**：`PUT /api/assets/myfolder/myAsset.png -H"Content-Type: application/json" -d '{"class":"asset", "properties":{"dc:title":"My Asset"}}'`

**応答コード**：応答コードは次のとおりです。

* 200 - OK（アセットが正常に更新された場合）
* 404 - NOT FOUND（指定した URI でアセットが見つからなかったかアクセスできなかった場合）
* 412 - PRECONDITION FAILED（ルートコレクションが見つからないかアクセスできない場合）
* 500 - INTERNAL SERVER ERROR（他に問題がある場合）

## アセットレンディションの作成 {#create-an-asset-rendition}

アセットのレンディションを作成します。リクエストパラメーター名が指定されない場合、ファイル名がレンディション名として使用されます。

**パラメーター**：パラメーターは `name`（レンディションの名前）と `file`（ファイル参照）です。

**リクエスト**

* `POST /api/assets/myfolder/myasset.png/renditions/web-rendition -H"Content-Type: image/png" --data-binary "@myRendition.png"`
* `POST /api/assets/myfolder/myasset.png/renditions/* -F"name=web-rendition" -F"file=@myRendition.png"`

**応答コード**

* 201 - CREATED（レンディションが正常に作成された場合）
* 404 - NOT FOUND（指定した URI でアセットが見つからなかったかアクセスできなかった場合）
* 412 - PRECONDITION FAILED（ルートコレクションが見つからないかアクセスできない場合）
* 500 - INTERNAL SERVER ERROR（他に問題がある場合）

## アセットレンディションの更新 {#update-an-asset-rendition}

アセットレンディションをそれぞれ新しいバイナリデータで置き換えて更新します。

**リクエスト**：`PUT /api/assets/myfolder/myasset.png/renditions/myRendition.png -H"Content-Type: image/png" --data-binary @myRendition.png`

**応答コード**：応答コードは次のとおりです。

* 200 - OK（レンディションが正常に更新された場合）
* 404 - NOT FOUND（指定した URI でアセットが見つからなかったかアクセスできなかった場合）
* 412 - PRECONDITION FAILED（ルートコレクションが見つからないかアクセスできない場合）
* 500 - INTERNAL SERVER ERROR（他に問題がある場合）

## アセットへのコメントの追加 {#create-an-asset-comment}

**パラメーター**：パラメーターは `message`（コメントのメッセージ本文）と `annotationData`（JSON 形式の注釈データ）です。

**リクエスト**：`POST /api/assets/myfolder/myasset.png/comments/* -F"message=Hello World." -F"annotationData={}"`

**応答コード**：応答コードは次のとおりです。

* 201 - CREATED（コメントが正常に作成された場合）
* 404 - NOT FOUND（指定した URI でアセットが見つからなかったかアクセスできなかった場合）
* 412 - PRECONDITION FAILED（ルートコレクションが見つからないかアクセスできない場合）
* 500 - INTERNAL SERVER ERROR（他に問題がある場合）

## フォルダーまたはアセットのコピー {#copy-a-folder-or-asset}

指定されたパスに存在するフォルダーまたはアセットを新しい宛先にコピーします。

**リクエストヘッダー**：パラメーターは次のとおりです。

* `X-Destination` - API ソリューション範囲内の、リソースのコピー先となる新しい宛先 URI
* `X-Depth` - `infinity` か `0` のいずれか。`0` を使用すると、リソースとそのプロパティのみがコピーされ、子はコピーされません。
* `X-Overwrite` - 既存の宛先にあるアセットが上書きされないようにするには、`F` を使用します。

**リクエスト**：`COPY /api/assets/myFolder -H"X-Destination: /api/assets/myFolder-copy"`

**応答コード**：応答コードは次のとおりです。

* 201 - CREATED（フォルダーやアセットが既存でない宛先にコピーされた場合）
* 204 - NO CONTENT（フォルダーまたはアセットが既存の宛先にコピーされた場合）
* 412 - PRECONDITION FAILED（リクエストヘッダーが不明な場合）
* 500 - INTERNAL SERVER ERROR（他に問題がある場合）

## フォルダーまたはアセットの移動 {#move-a-folder-or-asset}

指定されたパスのフォルダーまたはアセットを新しい宛先に移動します。

**リクエストヘッダー**：パラメーターは次のとおりです。

* `X-Destination` - API ソリューション範囲内の、リソースのコピー先となる新しい宛先 URI
* `X-Depth` - `infinity` か `0` のいずれか。`0` を使用すると、リソースとそのプロパティのみがコピーされ、子はコピーされません。
* `X-Overwrite` - 既存のリソースを強制的に削除する場合は `T` を、既存リソースの上書きを防ぐ場合は `F` を使用します。

**リクエスト**：`MOVE /api/assets/myFolder -H"X-Destination: /api/assets/myFolder-moved"`

**応答コード**：応答コードは次のとおりです。

* 201 - CREATED（フォルダーやアセットが既存でない宛先にコピーされた場合）
* 204 - NO CONTENT（フォルダーまたはアセットが既存の宛先にコピーされた場合）
* 412 - PRECONDITION FAILED（リクエストヘッダーが不明な場合）
* 500 - INTERNAL SERVER ERROR（他に問題がある場合）

## フォルダー、アセットまたはレンディションの削除 {#delete-a-folder-asset-or-rendition}

指定されたパスのリソース（ツリー）を削除します。

**リクエスト**

* `DELETE /api/assets/myFolder`
* `DELETE /api/assets/myFolder/myAsset.png`
* `DELETE /api/assets/myFolder/myAsset.png/renditions/original`

**応答コード**：応答コードは次のとおりです。

* 200 - OK（フォルダーが正常に削除された場合）
* 412 - PRECONDITION FAILED（ルートコレクションが見つからないかアクセスできない場合）
* 500 - INTERNAL SERVER ERROR（他に問題がある場合）

## ヒント、ベストプラクティス、制限事項 {#tips-limitations}

* [!UICONTROL オフタイム]の経過後、アセットとそのレンディションは、[!DNL Assets] Web インターフェイスでも HTTP API でも使用できません。[!UICONTROL オンタイム]が未来の場合、または[!UICONTROL オフタイム]が過去の場合、API は 404 エラーメッセージを返します。

* Assets HTTP API は完全なメタデータを返しません。名前空間はハードコードされ、これらの名前空間のみが返されます。完全なメタデータについては、アセットパス `/jcr_content/metadata.json` を参照してください。

* API を使用して更新された場合、フォルダーまたはアセットの一部のプロパティは、異なるプレフィックスにマップされます。`jcr:title`、`jcr:description`、`jcr:language` の `jcr` プレフィックスは `dc` プレフィックスに置き換えられます。したがって、返された JSON コードで、`dc:title`、`dc:description` にはそれぞれ `jcr:title`、`jcr:description` の値が含まれています。

>[!MORELIKETHIS]
>
>* [開発者向けリファレンスドキュメント [!DNL Assets]](/help/assets/developer-reference-material-apis.md)

