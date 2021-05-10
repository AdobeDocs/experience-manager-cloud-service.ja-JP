---
title: AEM AssetsAPIを使用したコンテンツの更新方法
description: AEMヘッドレス開発者ジャーニーのこの部分では、REST APIを使用してコンテンツフラグメントのコンテンツにアクセスし、更新する方法を説明します。
hide: true
hidefromtoc: true
index: false
exl-id: 8d133b78-ca36-4c3b-815d-392d41841b5c
translation-type: tm+mt
source-git-commit: 787af0d4994bf1871c48aadab74d85bd7c3c94fb
workflow-type: tm+mt
source-wordcount: '1668'
ht-degree: 68%

---

# AEM AssetsAPIを使用したコンテンツの更新方法{#update-your-content}

>[!CAUTION]
>
>作業中 — このドキュメントの作成は現在進行中で、完全なもの、最終的なもの、または実稼働目的で使用するものとして理解してはなりません。

[AEMヘッドレス開発者ジャーニーのこの部分では、](overview.md)がREST APIを使用してコンテンツフラグメントのコンテンツにアクセスし、更新する方法を学びます。

## {#story-so-far}

以前のドキュメントのAEM headlessジャーニーでは、[AEM配信APIを介したコンテンツへのアクセス方法](access-your-content.md)で、AEM GraphQL APIを介したAEMのheadlessコンテンツへのアクセス方法を学び、次の点に注意してください。

* GraphQLについて高レベルの理解を得る。
* AEM GraphQL APIの仕組みを理解します。
* 実際的なサンプルクエリをいくつか理解します。

この記事は、これらの基本事項に基づいて構築されているので、REST APIを使用してAEMの既存のヘッドレスコンテンツを更新する方法を理解しています。

## 目的 {#objective}

* **オーディエンス**:詳細
* **目的**:REST APIを使用してコンテンツフラグメントのコンテンツにアクセスし、更新する方法を説明します。
   * AEM AssetsHTTP APIを紹介します。
   * APIでコンテンツフラグメントのサポートを紹介し、ディスカッションを行います。
   * APIの詳細を説明します。

<!--
  * Look at sample code to see how things work in practice.
-->

## コンテンツフラグメントにアセットHTTP APIが必要な理由{#why-http-api}

ヘッドレスジャーニーの前の段階では、AEM GraphQL APIを使用してクエリを使用してコンテンツを取得する方法を学びました。

では、なぜ別のAPIが必要なのでしょうか。

Assets HTTP APIではコンテンツを&#x200B;**読み取り**&#x200B;できますが、**作成**、**更新**、**削除**&#x200B;コンテンツ（GraphQL APIでは不可能）も実行できます。

Assets REST API は、最新の Adobe Experience Manager as a Cloud Service バージョンの標準インストールで利用できます。

## Assets HTTP API {#assets-http-api}

[Assets HTTP API](/help/assets/mac-api-assets.md) には次の API が含まれます。

* Assets REST API
* コンテンツフラグメントをサポートしています。

現在の Assets HTTP API の実装は、**REST** アーキテクチャスタイルに基づいています。

Assets REST APIを使用すると、開発者はCloud ServiceとしてAdobe Experience Managerのコンテンツ(AEMに保存されている)に、**CRUD**&#x200B;操作（作成、読み取り、更新、削除）経由で直接アクセスできます。

この操作により、APIはJavaScriptフロントエンドアプリケーションにContent Servicesを提供することで、ヘッドレスCMS(コンテンツ管理システム)としてAdobe Experience ManagerをCloud Serviceとして操作できます。 または、HTTP リクエストを実行して JSON 応答を処理できる他のどのようなアプリケーションにもすることができます。例えば、単一ページアプリ(SPA)、フレームワークベースまたはカスタムの場合、API経由で提供されるコンテンツは、多くの場合JSON形式で提供する必要があります。

>[!NOTE]
>
>Assets REST API からの JSON 出力はカスタマイズできません。

Assets REST API は、

* HATEOAS の原則に従っています。
* SIREN 形式を実装しています。

## 主要な概念 {#key-concepts}

アセットREST APIオファーは、AEMインスタンス内に保存されたアセットにREST形式でアクセスします。

`/api/assets` エンドポイントを使用しており、アクセスするにはアセットのパス（先頭の `/content/dam` を除く）が必要です。

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


実行する操作は HTTP メソッドで決まります。

* **GET**：アセットまたはフォルダーの JSON 表現を取得します
* **POST**：新しいアセットまたはフォルダーを作成します
* **PUT**：アセットまたはフォルダーのプロパティを更新します
* **DELETE**：アセットまたはフォルダーを削除します

>[!NOTE]
>
>リクエスト本文または URL パラメーターは、これらの操作の一部を設定するために使用できます。例えば、フォルダーまたはアセットを **POST** リクエストで作成するように定義できます。

サポートされているリクエストの正確な形式は、『API リファレンス』ドキュメントで定義されています。

### トランザクション動作 {#transactional-behavior}

すべてのリクエストはアトミックです。

つまり、後続の（`write`）リクエストを結合して、単一のエンティティとして成功または失敗する単一のトランザクションにすることはできません。

### セキュリティ {#security}

特定の認証要件がない環境で Assets REST API が使用される場合は、AEM の CORS フィルターを正しく設定する必要があります。

>[!NOTE]
>
>詳しくは、次のセクションを参照してください。
>
>* CORS／AEM の説明
>* ビデオ - AEM を使用した CORS 向け開発


特定の認証要件がある環境では、OAuth を推奨します。

## 使用可能な機能 {#available-features}

コンテンツフラグメントは特定のアセットタイプです。コンテンツフラグメントの操作を参照してください。

API を通じて使用できる機能について詳しくは、以下を参照してください。

* アセットREST API（その他のリソース）
* エンティティタイプ。（コンテンツフラグメントに関連した）サポートされる各タイプに固有の機能について説明します。

### ページング {#paging}

Assets REST API では、URL パラメーターを介して（GET リクエストの）ページングをサポートしています。

* `offset` - 取得する最初の（子）エンティティの数
* `limit` - 返されるエンティティの最大数

応答には、SIREN 出力の `properties` セクションの一部としてページング情報が含まれます。この `srn:paging` プロパティには、リクエストで指定されている、（子）エンティティの総数（`total`）、オフセット（`offset`）および制限（`limit`）が含まれています。

>[!NOTE]
>
>ページングは通常、コンテナエンティティ（つまり、レンディションのあるフォルダーやアセット）に適用されます。要求されたエンティティの子に関係するからです。

#### 例：ページング {#example-paging}

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

## エンティティタイプ {#entity-types}

### フォルダー {#folders}

フォルダーは、アセットやその他のフォルダーのコンテナとして機能します。AEM コンテンツリポジトリの構造を反映しています。

Assets REST API は、フォルダーのプロパティ（名前、タイトルなど）へのアクセスを公開します。アセットは、フォルダーの子エンティティ、およびサブフォルダーとして公開されます。

>[!NOTE]
>
>子アセットとフォルダーのアセットタイプによっては、それぞれの子エンティティを定義するすべてのプロパティが、子エンティティのリストに既に含まれている場合があります。または、この子エンティティリストのエンティティに対して、一部のプロパティのみ公開される場合もあります。

### アセット {#assets}

アセットが要求されると、アセットのメタデータ（タイトルや名前など、それぞれのアセットスキーマで定義される情報）が応答で返されます。

アセットのバイナリデータは、`content` タイプの SIREN リンクとして公開されます。

アセットには複数のレンディションを含めることができます。通常、これらは子エンティティとして公開されます。ただし、サムネールレンディションは例外です。これは、`thumbnail` タイプ（`rel="thumbnail"`）のリンクとして公開されます。

### コンテンツフラグメント {#content-fragments}

コンテンツフラグメントは、特別な種類のアセットです。 コンテンツフラグメントを使用すれば、テキスト、数値、日付など様々な要素を含む構造化データにアクセスできます。

標準アセット（画像やオーディオなど）との違いがいくつかあるので、それらの処理には追加のルールが適用されます。**

#### 表現  {#representation}

コンテンツフラグメント：

* バイナリデータを公開しません。
* JSON 出力（`properties` プロパティ内）に完全に含まれます。

* アトミックと見なされます。つまり、エレメントとバリエーションは、リンクまたは子エンティティとしてではなく、フラグメントのプロパティの一部として公開されます。これにより、フラグメントのペイロードに効率的にアクセスできます。

#### コンテンツモデルとコンテンツフラグメント  {#content-models-and-content-fragments}

現在、コンテンツフラグメントの構造を定義するモデルは、HTTP API では公開されません。そのため、*コンシューマー*&#x200B;は（最低でも）フラグメントのモデルについて理解する必要があります。ただし、ほとんどの情報はペイロードから推測することができます。データタイプなどは定義の一部だからです。

新しいコンテンツフラグメントを作成するには、（内部リポジトリ）モデルのパスを指定する必要があります。

#### 関連コンテンツ {#associated-content}

関連コンテンツは現在公開されていません。

## アセットREST APIの使用{#using-aem-assets-rest-api}

使用方法は、特定の使用例以外にも、AEM オーサーを使用するかパブリッシュ環境を使用するかで異なることがあります。

* 作成をオーサーインスタンスに結び付けることを強くお勧めします（[現在は、この API を使用して公開するフラグメントをレプリケートする手段はありません](/help/assets/content-fragments/assets-api-content-fragments.md#limitations)）。
* 配信は、どちらからも可能です。AEM では、要求されたコンテンツを JSON 形式でのみ提供するからです。

   * ファイアウォールの背後で動作するメディアライブラリアプリケーションには、AEM オーサーインスタンスからの格納と配信で十分です。

   * ライブ Web 配信の場合は、AEM パブリッシュインスタンスをお勧めします。

>[!CAUTION]
>
>AEM クラウドインスタンス上の Dispatcher 設定により、`/api` へのアクセスがブロックされる場合があります。

>[!NOTE]
>
>詳細については、『](/help/assets/content-fragments/assets-api-content-fragments.md#api-reference)API リファレンス[』を参照してください。特に、[Adobe Experience Manager Assets API - コンテンツフラグメント](https://docs.adobe.com/content/help/en/experience-manager-cloud-service-javadoc/assets-api-content-fragments/index.html)。

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

### 更新 {#update}

使用方法は次のとおりです。

`PUT /{cfParentPath}/{cfName}`

本文には、特定コンテンツフラグメントの更新内容の JSON 表現を含める必要があります。

これには、コンテンツフラグメントのタイトルや説明、単一のエレメント、またはすべての要素値やメタデータを使用できます。

### 削除 {#delete}

使用方法は次のとおりです。

`DELETE /{cfParentPath}/{cfName}`

AEM AssetsREST APIの使用の詳細については、次を参照してください。

* Adobe Experience ManagerアセットHTTP API（その他のリソース）
* AEM AssetsHTTP APIでのコンテンツフラグメントのサポート（追加リソース）

## 次の作業{#whats-next}

AEMヘッドレス開発者ジャーニーのこの部分が完了したら、次の作業を行う必要があります。

* AEM AssetsHTTP APIの基本について説明します。
* このAPIでコンテンツフラグメントがどのようにサポートされているかを理解します。

<!--
* Have experience with sample code and know how the API works in practice.
-->

AEMのヘッドレスジャーニーは、次にドキュメント[How to Put It All Togeter - Your App and Your Content in AEM Headless](put-it-all-together.md)を確認し、AEMヘッドレスプロジェクトの取り組みと運用準備を進めて行く必要があります。

## その他のリソース {#additional-resources}

* [REST](https://en.wikipedia.org/wiki/Representational_state_transfer)
* [HATEOASの原則](https://en.wikipedia.org/wiki/HATEOAS)
* [SIREN形式](https://github.com/kevinswiber/siren)
* [Assets HTTP API](/help/assets/mac-api-assets.md)
* [コンテンツフラグメント REST API](/help/assets/content-fragments/assets-api-content-fragments.md)
   * [API リファレンス](/help/assets/content-fragments/assets-api-content-fragments.md#api-reference)
* [コンテンツフラグメントの操作](/help/assets/content-fragments/content-fragments.md)
* [AEM コアコンポーネント](https://docs.adobe.com/content/help/ja/experience-manager-core-components/using/introduction.html)
* [CORS／AEM の説明](https://helpx.adobe.com/jp/experience-manager/kt/platform-repository/using/cors-security-article-understand.html)
* [ビデオ - AEM を使用した CORS 向け開発](https://helpx.adobe.com/jp/experience-manager/kt/platform-repository/using/cors-security-technical-video-develop.html)

