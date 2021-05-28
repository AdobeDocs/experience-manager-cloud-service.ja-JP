---
title: AEM Assets APIを使用したコンテンツの更新方法
description: AEMヘッドレス開発者ジャーニーのこのパートでは、REST APIを使用してコンテンツフラグメントのコンテンツにアクセスし、更新する方法について説明します。
source-git-commit: 856266faf4cb99056b1763383d611e9b2c3c13ea
workflow-type: tm+mt
source-wordcount: '1049'
ht-degree: 51%

---


# AEM Assets APIを使用したコンテンツの更新方法{#update-your-content}

[AEMヘッドレス開発者ジャーニーのこのパートでは、REST APIを使用してコンテンツフラグメントのコンテンツにアクセスし、更新する方法を説明します。](overview.md)

## {#story-so-far}までの話

AEMヘッドレスジャーニーの前のドキュメント、[AEM Delivery APIを使用したコンテンツへのアクセス方法](access-your-content.md)では、AEM GraphQL APIを使用したAEMのヘッドレスコンテンツへのアクセス方法を学習し、次の操作を行う必要があります。

* GraphQLについて理解を深める。
* AEM GraphQL APIの仕組みを理解します。
* 実用的なサンプルクエリを理解します。

この記事は、これらの基本事項に基づいて構築されているので、REST APIを使用してAEMの既存のヘッドレスコンテンツを更新する方法を理解できます。

## 目的 {#objective}

* **オーディエンス**:詳細
* **目的**:REST APIを使用して、コンテンツフラグメントのコンテンツにアクセスし更新する方法を説明します。
   * AEM Assets HTTP APIの紹介
   * APIでのコンテンツフラグメントのサポートを紹介し、説明します。
   * APIの詳細を説明します。

<!--
  * Look at sample code to see how things work in practice.
-->

## コンテンツフラグメント{#why-http-api}にAssets HTTP APIが必要な理由

ヘッドレスジャーニーの前の段階では、AEM GraphQL APIを使用してクエリを使用してコンテンツを取得する方法を学びました。

では、他のAPIが必要なのはなぜですか？

Assets HTTP APIを使用すると、コンテンツを&#x200B;**読み取り**&#x200B;できますが、**作成**、**更新**&#x200B;および&#x200B;**削除**&#x200B;コンテンツ — GraphQL APIでは実行できないアクションも実行できます。

Assets REST API は、最新の Adobe Experience Manager as a Cloud Service バージョンの標準インストールで利用できます。

## Assets HTTP API {#assets-http-api}

Assets HTTP API には次の API が含まれます。

* Assets REST API
* コンテンツフラグメントをサポートしています。

現在のAssets HTTP APIの実装は、**REST**&#x200B;アーキテクチャスタイルに基づいており、**CRUD**&#x200B;操作（作成、読み取り、更新、削除）を使用して(AEMに保存された)コンテンツにアクセスできます。

この操作を使用すると、JavaScriptフロントエンドアプリケーションにContent Servicesを提供することで、Adobe Experience ManagerをヘッドレスCMS(Content Management System)としてCloud Serviceとして操作できます。 または、HTTP リクエストを実行して JSON 応答を処理できる他のどのようなアプリケーションにもすることができます。例えば、単一ページアプリケーション(SPA)、フレームワークベースまたはカスタムでは、API経由で提供されるコンテンツ（多くの場合JSON形式）が必要です。

<!--
>[!NOTE]
>
>It is not possible to customize JSON output from the Assets REST API. 

The Assets REST API:

* follows the HATEOAS principle
* implements the SIREN format

## Key Concepts {#key-concepts}

The Assets REST API offers REST-style access to assets stored within an AEM instance. 

It uses the `/api/assets` endpoint and requires the path of the asset to access it (without the leading `/content/dam`). 

* This means that to access the asset at:
  * `/content/dam/path/to/asset`
* You need to request:
  * `/api/assets/path/to/asset` 

For example, to access `/content/dam/wknd/en/adventures/cycling-tuscany`, request `/api/assets/wknd/en/adventures/cycling-tuscany.json` 

>[!NOTE]
>Access over:
>
>* `/api/assets` **does not** need the use of the `.model` selector.
>* `/content/path/to/page` **does** require the use of the `.model` selector.

The HTTP method determines the operation to be executed:

* **GET** - to retrieve a JSON representation of an asset or a folder
* **POST** - to create new assets or folders
* **PUT** - to update the properties of an asset or folder
* **DELETE** - to delete an asset or folder

>[!NOTE]
>
>The request body and/or URL parameters can be used to configure some of these operations; for example, define that a folder or an asset should be created by a **POST** request.

The exact format of supported requests is defined in the API Reference documentation. 

### Transactional Behavior {#transactional-behavior}

All requests are atomic.

This means that subsequent (`write`) requests cannot be combined into a single transaction that could succeed or fail as a single entity.

### Security {#security}

If the Assets REST API is used within an environment without specific authentication requirements, AEM's CORS filter needs to be configured correctly.

>[!NOTE]
>
>For further information see:
>
>* CORS/AEM explained
>* Video - Developing for CORS with AEM

In environments with specific authentication requirements, OAuth is recommended.

## Available Features {#available-features}

Content Fragments are a specific type of Asset, see Working with Content Fragments.

For further information about features available through the API see:

* The Assets REST API (Additional Resources) 
* Entity Types, where the features specific to each supported type (as relevant to Content Fragments) are explained 

### Paging {#paging}

The Assets REST API supports paging (for GET requests) via the URL parameters:

* `offset` - the number of the first (child) entity to retrieve
* `limit` - the maximum number of entities returned

The response will contain paging information as part of the `properties` section of the SIREN output. This `srn:paging` property contains the total number of (child) entities ( `total`), the offset and the limit ( `offset`, `limit`) as specified in the request.

>[!NOTE]
>
>Paging is typically applied on container entities (i.e. folders or assets with renditions), as it relates to the children of the requested entity.

#### Example: Paging {#example-paging}

`GET /api/assets.json?offset=2&limit=3`

```json
...
"properties": {
    ...
    "srn:paging": {
        "total": 7,
        "offset": 2,
        "limit": 3
    }
    ...
}
...
```

## Entity Types {#entity-types}

### Folders {#folders}

Folders act as containers for assets and other folders. They reflect the structure of the AEM content repository.

The Assets REST API exposes access to the properties of a folder; for example its name, title, etc. Assets are exposed as child entities of folders, and sub-folders.

>[!NOTE]
>
>Depending on the asset type of the child assets and folders the list of child entities may already contain the full set of properties that defines the respective child entity. Alternatively, only a reduced set of properties may be exposed for an entity in this list of child entities.

### Assets {#assets}

If an asset is requested, the response will return its metadata; such as title, name and other information as defined by the respective asset schema.

The binary data of an asset is exposed as a SIREN link of type `content`.

Assets can have multiple renditions. These are typically exposed as child entities, one exception being a thumbnail rendition, which is exposed as a link of type `thumbnail` ( `rel="thumbnail"`).
-->

## アセットのHTTP APIとコンテンツフラグメント{#assets-http-api-content-fragments}

コンテンツフラグメントはヘッドレス配信に使用され、コンテンツフラグメントは特別なタイプのアセットです。 テキスト、数値、日付など、構造化されたデータにアクセスするために使用されます。

<!--
As there are several differences to *standard* assets (such as images or audio), some additional rules apply to handling them.

### Representation {#representation}

Content fragments:

* Do not expose any binary data.
* Are completely contained in the JSON output (within the `properties` property).

* Are also considered atomic, i.e. the elements and variations are exposed as part of the fragment's properties vs. as links or child entities. This allows for efficient access to the payload of a fragment.

### Content Models and Content Fragments {#content-models-and-content-fragments}

Currently the models that define the structure of a content fragment are not exposed through an HTTP API. Therefore the *consumer* needs to know about the model of a fragment (at least a minimum) - although most information can be inferred from the payload; as data types, etc. are part of the definition.

To create a new content fragment, the (internal repository) path of the model has to be provided.

### Associated Content {#associated-content}

Associated content is currently not exposed.
-->

## Assets REST APIの使用{#using-aem-assets-rest-api}

### アクセス {#access}

Assets REST APIは`/api/assets`エンドポイントを使用し、アクセスするにはアセットのパスが必要です（先頭の`/content/dam`を除く）。

* つまり、次の場所のアセットにアクセスするには
   * `/content/dam/path/to/asset`
* 次のリクエストが必要です。
   * `/api/assets/path/to/asset`

例えば、`/content/dam/wknd/en/adventures/cycling-tuscany` にアクセスするには、`/api/assets/wknd/en/adventures/cycling-tuscany.json` をリクエストします。

>[!NOTE]
>アクセス経由：
>
>* `/api/assets` は `.model` セレクターを使用する&#x200B;**必要はありません**。
>* `/content/path/to/page` は `.model` セレクターを使用する&#x200B;**必要があります**。


### 操作 {#operation}

実行する操作は HTTP メソッドで決まります。

* **GET**：アセットまたはフォルダーの JSON 表現を取得します
* **POST**：新しいアセットまたはフォルダーを作成します
* **PUT**：アセットまたはフォルダーのプロパティを更新します
* **DELETE**：アセットまたはフォルダーを削除します

>[!NOTE]
>
>リクエスト本文または URL パラメーターは、これらの操作の一部を設定するために使用できます。例えば、フォルダーまたはアセットを **POST** リクエストで作成するように定義できます。

サポートされているリクエストの正確な形式は、『API リファレンス』ドキュメントで定義されています。

使用方法は、特定の使用例以外にも、AEM オーサーを使用するかパブリッシュ環境を使用するかで異なることがあります。

* 作成をオーサーインスタンスに結び付けることを強くお勧めします（現在は、この API を使用して公開するフラグメントをレプリケートする手段はありません）。
* 配信は、どちらからも可能です。AEM では、要求されたコンテンツを JSON 形式でのみ提供するからです。

   * ファイアウォールの背後で動作するメディアライブラリアプリケーションには、AEM オーサーインスタンスからの格納と配信で十分です。

   * ライブ Web 配信の場合は、AEM パブリッシュインスタンスをお勧めします。

>[!CAUTION]
>
>AEM クラウドインスタンス上の Dispatcher 設定により、`/api` へのアクセスがブロックされる場合があります。

>[!NOTE]
>
>詳細については、『API リファレンス』を参照してください。特に、[Adobe Experience Manager Assets API - コンテンツフラグメント](https://experienceleague.adobe.com/docs/experience-manager-cloud-service-javadoc/assets-api-content-fragments/index.html)。

### 読み取り／配信 {#read-delivery}

使用方法は次のとおりです。

`GET /{cfParentPath}/{cfName}.json`

次に例を示します。

`http://<host>/api/assets/wknd/en/adventures/cycling-tuscany.json`

応答は、コンテンツがコンテンツフラグメントに構造化されたシリアル化 JSON です。参照は参照 URL として配信されます。

次の 2 通りの読み取り操作が可能です。

* 特定のコンテンツフラグメントをパスで読み取る。この場合は、コンテンツフラグメントの JSON 表現が返されます。
* コンテンツフラグメントのフォルダーをパスで読み取る。この場合は、フォルダー内のすべてのコンテンツフラグメントの JSON 表現が返されます。

### 作成 {#create}

使用方法は次のとおりです。

`POST /{cfParentPath}/{cfName}`

本文には、作成するコンテンツフラグメントの JSON 表現を含める必要があります。これには、コンテンツフラグメント要素に設定する必要がある初期コンテンツも含まれます。`cq:model` プロパティの設定が必須で、このプロパティが有効なコンテンツフラグメントモデルを指している必要があります。そうしないと、エラーが発生します。また、`Content-Type` ヘッダーを追加することも必要です。これは `application/json` に設定されます。

### アップデート {#update}

使用方法は次のとおりです。

`PUT /{cfParentPath}/{cfName}`

本文には、特定コンテンツフラグメントの更新内容の JSON 表現を含める必要があります。

これには、コンテンツフラグメントのタイトルや説明、単一のエレメント、またはすべての要素値やメタデータを使用できます。

### 削除 {#delete}

使用方法は次のとおりです。

`DELETE /{cfParentPath}/{cfName}`

AEM Assets REST APIの使用の詳細については、次を参照してください。

* Adobe Experience Manager Assets HTTP API（その他のリソース）
* AEM Assets HTTP APIでのコンテンツフラグメントのサポート（その他のリソース）

## 次の手順{#whats-next}

これで、AEMヘッドレス開発者ジャーニーのこの部分が完了し、次の作業が完了しました。

* AEM Assets HTTP APIの基本を理解します。
* このAPIでのコンテンツフラグメントのサポート方法を説明します。

<!--
* Have experience with sample code and know how the API works in practice.
-->

<!-- The "How to put it all together" page isn't going to be published until the first public release of the Headless SDK. Temporarily commenting out the reference below. -->

<!--You should continue your AEM headless journey by next reviewing the document [How to Put It All Together - Your App and Your Content in AEM Headless](put-it-all-together.md) where you learn how to take your AEM Headless project and prepare it for going live.-->

次に、『[How to Go Live with Your Headless Application](go-live.md)』(実際にAEM Headlessプロジェクトをライブにする方法)のドキュメントを確認して、AEMヘッドレスなジャーニーを続ける必要があります。

## その他のリソース {#additional-resources}

* [Assets HTTP API](/help/assets/mac-api-assets.md)
* [コンテンツフラグメント REST API](/help/assets/content-fragments/assets-api-content-fragments.md)
   * [API リファレンス](/help/assets/content-fragments/assets-api-content-fragments.md#api-reference)
* [Adobe Experience Manager Assets API - コンテンツフラグメント](https://experienceleague.adobe.com/docs/experience-manager-cloud-service-javadoc/assets-api-content-fragments/index.html)
* [コンテンツフラグメントの操作](/help/assets/content-fragments/content-fragments.md)
* [AEM コアコンポーネント](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html?lang=ja)
* [CORS／AEM の説明](https://helpx.adobe.com/jp/experience-manager/kt/platform-repository/using/cors-security-article-understand.html)
* [ビデオ - AEM を使用した CORS 向け開発](https://helpx.adobe.com/jp/experience-manager/kt/platform-repository/using/cors-security-technical-video-develop.html)
