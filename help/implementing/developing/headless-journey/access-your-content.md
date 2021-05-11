---
title: AEM配信APIを使用したコンテンツへのアクセス方法
description: AEMヘッドレス開発者ジャーニーのこの部分では、GraphQLクエリを使用してコンテンツフラグメントのコンテンツにアクセスする方法を説明します。
hide: true
hidefromtoc: true
index: false
exl-id: 5ef557ff-e299-4910-bf8c-81c5154ea03f
translation-type: tm+mt
source-git-commit: 4a36cd3206784c0e4e3ed3d7007c83f44f1d5ee0
workflow-type: tm+mt
source-wordcount: '1381'
ht-degree: 18%

---

# AEM配信APIを使用したコンテンツへのアクセス方法{#access-your-content}

>[!CAUTION]
>
>作業中 — このドキュメントの作成は現在進行中で、完全なもの、最終的なもの、または実稼働目的で使用するものとして理解してはなりません。

[AEMヘッドレス開発者ジャーニーのこの部分では、](overview.md)GraphQLクエリを使用してコンテンツフラグメントのコンテンツにアクセスし、アプリに送る方法(ヘッドレス配信)を学習できます。

## {#story-so-far}

以前のドキュメントのAEMヘッドレスジャーニー[How to Model Your Content](model-your-content.md)では、AEMでコンテンツモデリングの基本を学習したので、コンテンツ構造のモデル化方法を理解し、AEMコンテンツフラグメントモデルとコンテンツフラグメントを使用してこの構造を実現する必要があります。

* コンテンツのモデリングに関連する概念と用語を認識します。
* ヘッドレスコンテンツ配信にコンテンツモデリングが必要な理由を理解します。
* AEMコンテンツフラグメントモデルを使用して(およびコンテンツフラグメントを使用してコンテンツを作成する方法を理解します。
* コンテンツのモデル化方法を理解する基本的なサンプルを持つ原則

この記事は、AEM GraphQL APIを使用してAEMの既存のヘッドレスコンテンツにアクセスする方法を理解するために、これらの基本事項に基づいて構築されています。

* **オーディエンス**:初心者
* **目的**:AEM GraphQLクエリを使用してコンテンツフラグメントのコンテンツにアクセスする方法を説明します。
   * GraphQLとAEM GraphQL APIの紹介。
   * AEM GraphQL APIの詳細を確認します。
   * 実際の動作を確認するには、サンプルクエリを参照してください。

## コンテンツにアクセスしたい？{#so-youd-like-to-access-your-content}

だから…（コンテンツフラグメント内に）このようなコンテンツがすべて整然と構成され、新しいアプリが提供されるのを待っています。 問題は、そこに到達する方法です。

必要なのは、特定のコンテンツをターゲットし、必要なものを選択してアプリに返し、さらに処理する方法です。

Adobe Experience Manager(AEM)をCloud Serviceとして使用すると、AEM GraphQL APIを使用して、コンテンツフラグメントに選択的にアクセスし、必要なコンテンツのみを返すことができます。 つまり、アプリケーションで使用する構造化コンテンツのヘッドレスな配信を実現できます。

>[!NOTE]
>
>AEM GraphQL APIは、標準のGraphQL API仕様に基づいてカスタマイズされた実装です。

## GraphQL — 入門{#graphql-introduction}

GraphQLは、次の機能を提供するオープンソース仕様です。

* 構造化オブジェクトから特定のコンテンツを選択できるクエリ言語。
* 構造化コンテンツでこれらのクエリを満たすランタイム。

GraphQLは&#x200B;*厳密に*&#x200B;型指定されたAPIです。 つまり、*すべての*&#x200B;コンテンツは、タイプ別に明確に構成、整理されていなければならないので、GraphQL *は、何にアクセスし、何にアクセスするかと、どのようにしてアクセスするかを理解している必要があります。*&#x200B;データフィールドはGraphQLスキーマ内で定義され、コンテンツオブジェクトの構造を定義します。

次に、GraphQLエンドポイントは、GraphQLクエリに応答するパスを提供します。

つまり、アプリをAEMで使用する場合に必要なコンテンツだけを、正確かつ信頼性の高い方法で効率的に選択できます。

>[!NOTE]
>
>*GraphQL*.orgおよび&#x200B;*GraphQL*.comを参照してください。

<!--
## AEM and GraphQL {#aem-graphql}

GraphQL is used in various locations in AEM; for example:

* Content Fragments
  * A customized API has been developed for this use-case (Headless Delivery to your app).
    * This is the AEM GraphQL API.
* Commerce
  * AEM Commerce consumes data from a Commerce platform via GraphQL.
  * There are GraphQL integrations between AEM and various third-party commerce solutions, used with the extension hooks provided by the CIF Core Components.
    * This does not use the AEM GraphQL API.

>[!NOTE]
>
>This step of the Headless Journey is only concerned with the AEM GraphQL API and Content Fragments.
-->

## AEM GraphQL API {#aem-graphql-api}

AEM GraphQL APIは、標準のGraphQL API仕様に基づいてカスタマイズされたバージョンで、コンテンツフラグメントに対して（複雑な）クエリを実行できるように特別に設定されています。

コンテンツフラグメントは、コンテンツがコンテンツフラグメントのモデルに従って構造化されているので使用されます。 これは、GraphQLの基本的な要件を満たします。

* コンテンツフラグメントモデルは、1つ以上のフィールドで構成されています。
   * 各フィールドはデータ型に従って定義されます。
* コンテンツフラグメントモデルは、対応するAEM GraphQLスキーマの生成に使用されます。

AEM用のGraphQL（およびコンテンツ）に実際にアクセスするには、エンドポイントを使用してアクセスパスを提供します。

AEM GraphQL APIを介して返されたコンテンツは、アプリケーションで使用できます。

クエリを直接入力し、テストする際に役立つように、標準のGraphiQLインターフェイスの実装もAEM GraphQLで使用できます(AEMと共にインストールできます)。 構文の強調表示、オートコンプリート、オートコンプリートなどの機能と、履歴およびオンラインドキュメントが提供されます。

>[!NOTE]
>
>AEM GraphQL API の実装は、GraphQL Java ライブラリに基づいています。

<!--
### Use Cases for Author and Publish Environments {#use-cases-author-publish-environments}

The use cases for the AEM GraphQL API can depend on the type of AEM as a Cloud Service environment:

* Publish environment; used to: 
  * Query content for JS application (standard use-case)

* Author environment; used to: 
  * Query content for "content management purposes":
    * GraphQL in AEM as a Cloud Service is currently a read-only API.
    * The REST API can be used for CR(u)D operations.
-->

## AEM GraphQL API で使用するコンテンツフラグメント {#content-fragments-use-with-aem-graphql-api}

コンテンツフラグメントは、AEMスキーマやクエリのGraphQLの基盤として、次のように使用できます。

* ヘッドレスに配信できるページに依存しないコンテンツのデザイン、作成、キュレーションおよび公開が可能です。
* これらはコンテンツフラグメントモデルに基づいています。コンテンツフラグメントモデルでは、選択したデータ型を使用して、結果のフラグメントの構造を事前に定義します。
* 構造の追加のレイヤーは、フラグメント参照データ型を使用して作成できます。このデータ型は、モデルの定義時に使用できます。

### コンテンツフラグメントモデル {#content-fragments-models}

コンテンツフラグメントモデルは、

* **有効**&#x200B;にされると、スキーマの生成に使用されます。
* GraphQL に必要なデータタイプとフィールドを提供します。アプリケーションが、可能なことだけを要求して期待するものを受け取るようにします。
* データタイプ&#x200B;**フラグメント参照**&#x200B;は、別のコンテンツフラグメントを参照するためにモデル内で使用できるので、構造レベルを追加します。

### フラグメント参照 {#fragment-references}

**フラグメント参照**&#x200B;は、

* は、コンテンツフラグメントモデルの定義時に使用できる特定のデータ型です。
* 特定のコンテンツフラグメントモデルに依存する別のフラグメントを参照します。
* 構造化データを作成し、取得できます。

   * **マルチフィード**&#x200B;として定義した場合、複数のサブフラグメントをプライムフラグメントで参照（取得）できます。

### JSON プレビュー {#json-preview}

コンテンツフラグメントモデルの設計と開発に役立つように、コンテンツフラグメントエディターでJSON出力をプレビューできます。

![JSON ](assets/cfm-model-json-preview.png "PreviewJSONプレビュー")

<!--
## GraphQL Schema Generation from Content Fragments {#graphql-schema-generation-content-fragments}

GraphQL is a strongly typed API, which means that content must be clearly structured and organized by type. The GraphQL specification provides a series of guidelines on how to create a robust API for interrogating content on a certain instance. To do this, a client needs to fetch the Schema, which contains all the types necessary for a query. 

For Content Fragments, the GraphQL schemas (structure and types) are based on **Enabled** Content Fragment Models and their data types.

>[!CAUTION]
>
>All the GraphQL schemas (derived from Content Fragment Models that have been **Enabled**) are readable through the GraphQL endpoint.
>
>This means that you need to ensure that no sensitive content is available, to ensure that no sensitive data is exposed via GraphQL endpoints; for example, this includes information that could be present as field names in the model definition.

For example, if a user created a Content Fragment Model called `Article`, then AEM generates the object `article` that is of a type `ArticleModel`. The fields within this type correspond to the fields and data types defined in the model.

1. A Content Fragment Model:

   ![Content Fragment Model for use with GraphQL](assets/graphqlapi-cfmodel.png "Content Fragment Model for use with GraphQL")

1. The corresponding GraphQL schema (output from GraphiQL automatic documentation):
   ![GraphQL Schema based on Content Fragment Model](assets/graphqlapi-cfm-schema.png "GraphQL Schema based on Content Fragment Model")

   This shows that the generated type `ArticleModel` contains several [fields](#fields). 
   
   * Three of them have been controlled by the user: `author`, `main` and `referencearticle`.

   * The other fields were added automatically by AEM, and represent helpful methods to provide information about a certain Content Fragment; in this example, `_path`, `_metadata`, `_variations`. These [helper fields](#helper-fields) are marked with a preceding `_` to distinguish between what has been defined by the user and what has been auto-generated.

1. After a user creates a Content Fragment based on the Article model, it can then be interrogated through GraphQL. For examples, see the Sample Queries.md#graphql-sample-queries) (based on a sample Content Fragment structure for use with GraphQL.

In GraphQL for AEM, the schema is flexible. This means that it is auto-generated each and every time a Content Fragment Model is created, updated or deleted. The data schema caches are also refreshed when you update a Content Fragment Model.

The Sites GraphQL service listens (in the background) for any modifications made to a Content Fragment Model. When updates are detected, only that part of the schema is regenerated. This optimization saves time and provides stability.

So for example, if you:

1. Install a package containing `Content-Fragment-Model-1` and `Content-Fragment-Model-2`:
 
   1. GraphQL types for `Model-1` and `Model-2` will be generated.

1. Then modify `Content-Fragment-Model-2`:

   1. Only the `Model-2` GraphQL type will get updated.

   1. Whereas `Model-1` will remain the same. 

>[!NOTE]
>
>This is important to note in case you want to do bulk updates on Content Fragment Models through the REST api, or otherwise.

The schema is served through the same endpoint as the GraphQL queries, with the client handling the fact that the schema is called with the extension `GQLschema`. For example, performing a simple `GET` request on `/content/cq:graphql/global/endpoint.GQLschema` will result in the output of the schema with the Content-type: `text/x-graphql-schema;charset=iso-8859-1`.

### Schema Generation - Unpublished Models {#schema-generation-unpublished-models}

When Content Fragments are nested it can happen that a parent Content Fragment Model is published, but a referenced model is not.

>[!NOTE]
>
>The AEM UI prevents this happening, but if publishing is made programmatically, or with content packages, it can occur.

When this happens, AEM generates an *incomplete* Schema for the parent Content Fragment Model. This means that the Fragment Reference, which is dependent on the unpublished model, is removed from the schema.

## AEM GraphQL Endpoints {#aem-graphql-endpoints}

An endpoint is the path used to access GraphQL for AEM. Using this path you (or your app) can:

* access the GraphQL schemas,
* send your GraphQL queries,
* receive the responses (to your GraphQL queries).

AEM allows for:

* A global endpoint - available for use by all sites.
* Endpoints for specific Sites configurations - that you can configure (in the Configuration Browser), specific to a specified site/project.

## Permissions {#permissions}

The permissions are those required for accessing Assets.

## The AEM GraphiQL Interface {#aem-graphiql-interface}

To help you directly input, and test queries, an implementation of the standard GraphiQL interface is available for use with AEM GraphQL. This can be installed with AEM.

>[!NOTE]
>
>GraphiQL is bound the global endpoint (and does not work with other endpoints for specific Sites configurations).

It provides features such as syntax-highlighting, auto-complete, auto-suggest, together with a history and online documentation.

![GraphiQL Interface](assets/graphiql-interface.png "GraphiQL Interface")
-->

## AEM GraphQL APIの実際の使用{#actually-using-aem-graphiql}

### 初期設定 {#initial-setup}

コンテンツのクエリを開始する前に、次の操作を行う必要があります。

* エンドポイントを有効にする
   * ツール/サイト/GraphQLを使用
   * [GraphQL エンドポイントの有効化](/help/assets/content-fragments/graphql-api-content-fragments.md#enabling-graphql-endpoint)

* GraphiQLのインストール（必要な場合）
   * 専用パッケージとしてインストール
   * [AEM GraphiQL インターフェイスのインストール](/help/assets/content-fragments/graphql-api-content-fragments.md#installing-graphiql-interface)

### サンプル構造{#sample-structure}

AEM GraphQL APIをクエリで実際に使用するには、次の2つの非常に基本的なコンテンツフラグメントモデル構造を使用します。

* 会社情報
   * 名前 — テキスト
   * CEO（人） — フラグメント参照
   * 従業員（個人） — フラグメント参照
* Person
   * 名前 — テキスト
   * 名 — テキスト

「CEO」フィールドと「従業員」フィールドは、「個人」フラグメントを参照します。

フラグメントモデルが使用されます。

* コンテンツフラグメントエディターでコンテンツを作成する場合
* クエリするGraphQLスキーマを生成するには

### クエリのテスト場所{#where-to-test-your-queries}

クエリは、GraphiciQLインターフェイスで入力できます。例えば、次のURLで入力できます。

* `http://localhost:4502/content/graphiql.html `

![GraphiQL インターフェイス](assets/graphiql-interface.png "GraphiQL インターフェイス")

### クエリ使用の手引き{#getting-Started-with-queries}

単刀直入なクエリは、会社スキーマ内のすべてのエントリの名前を返すことです。 ここでは、すべての会社名のリストをリクエストします。

```xml
query {
  companyList {
    items {
      name
    }
  }
}
```

もう少し複雑なクエリは、「ジョブ」という名前を持たないすべての人を選ぶことです。 これにより、ジョブという名前を持たないすべての人がフィルターされます。 これは、EQUALS_NOT演算子を使用して達成できます（その他多数あります）。

```xml
query {
  personList(filter: {
    name: {
      _expressions: [
        {
          value: "Jobs"
          _operator: EQUALS_NOT
        }
      ]
    }
  }) {
    items {
      name
      firstName
    }
  }
}
```

また、より複雑なクエリを作成することもできます。 例えば、「Smith」という名前の従業員が少なくとも1人いるすべての会社に対するクエリです。 次のクエリは、「Smith」という名前の任意の人のフィルター処理を示し、ネストされたフラグメント全体から情報を返します。

```xml
query {
  companyList(filter: {
    employees: {
      _match: {
        name: {
          _expressions: [
            {
              value: "Smith"
            }
          ]
        }
      }
    }
  }) {
    items {
      name
      ceo {
        name
        firstName
      }
      employees {
        name
        firstName
      }
    }
  }
}
```

<!-- need code / curl / cli examples-->

AEM GraphQL APIを使用し、必要な要素を設定する方法の詳細については、次を参照してください。

* AEMでのGraphQLの使用方法
* サンプルコンテンツフラグメント構造
* AEM での GraphQL の使用方法 - サンプルコンテンツとサンプルクエリ

## 次の作業{#whats-next}

AEM GraphQL APIを使用してヘッドレスコンテンツにアクセスし、クエリする方法を学んだので、[REST APIを使用してコンテンツフラグメントのコンテンツにアクセスし、更新する方法を学ぶことができます。](/help/implementing/developing/headless-journey/update-your-content.md)

## その他のリソース {#additional-resources}

* [GraphQL.org](https://graphql.org)
   * [スキーマ](https://graphql.org/learn/schema/)
   * [変数](https://graphql.org/learn/queries/#variables)
   * [GraphQL Javaライブラリ](https://graphql.org/code/#java)
* [GraphiQL](https://graphql.org/learn/serving-over-http/#graphiql)
* [AEMでのGraphQLの使用方法](/help/assets/content-fragments/graphql-api-content-fragments.md)
   * [GraphQL エンドポイントの有効化](/help/assets/content-fragments/graphql-api-content-fragments.md#enabling-graphql-endpoint)
   * [AEM GraphiQL インターフェイスのインストール](/help/assets/content-fragments/graphql-api-content-fragments.md#installing-graphiql-interface)
* [サンプルコンテンツフラグメント構造](/help/assets/content-fragments/content-fragments-graphql-samples.md#content-fragment-structure-graphql)
* [AEM での GraphQL の使用方法 - サンプルコンテンツとサンプルクエリ](/help/assets/content-fragments/content-fragments-graphql-samples.md)
   * [サンプルクエリ - 1 つの特定の都市フラグメント](/help/assets/content-fragments/content-fragments-graphql-samples.md#sample-single-specific-city-fragment)
   * [メタデータのサンプルクエリ - 「GB」という賞のメタデータのリスト](/help/assets/content-fragments/content-fragments-graphql-samples.md#sample-metadata-awards-gb)
   * [サンプルクエリ - 名前付きバリエーションを持つすべての都市](/help/assets/content-fragments/content-fragments-graphql-samples.md#sample-cities-named-variation)
* [設定ブラウザーでコンテンツフラグメント機能を有効にする](/help/assets/content-fragments/content-fragments-configuration-browser.md#enable-content-fragment-functionality-in-configuration-browser)
* [コンテンツフラグメントの操作](/help/assets/content-fragments/content-fragments.md)
   * [コンテンツフラグメントモデル](/help/assets/content-fragments/content-fragments-models.md)
   * [JSON 出力](/help/assets/content-fragments/content-fragments-json-preview.md)
* [接触チャネル間のリソース共有(CORS)について](https://experienceleague.adobe.com/docs/experience-manager-learn/foundation/security/understand-cross-origin-resource-sharing.html?lang=ja#understand-cross-origin-resource-sharing-(cors))
* [サーバー側 API のアクセストークンの生成](/help/implementing/developing/introduction/generating-access-tokens-for-server-side-apis.md)
* [AEM Headless](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/graphql/overview.html?lang=ja)  — はじめに — コンテンツモデリングやGraphQLなど、AEM headless機能の使用方法の概要を説明する短いビデオチュートリアルシリーズです。
