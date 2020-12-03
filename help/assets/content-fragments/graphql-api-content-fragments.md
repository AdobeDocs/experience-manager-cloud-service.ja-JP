---
title: Cloud ServiceGraphQL APIとしてのAdobe Experience Managerとのコンテンツフラグメントを使用したコンテンツ配信
description: Adobe Experience Manager(AEM)のコンテンツフラグメントを、AEM GraphQL API for Headless Content配信とのCloud Serviceとして使用する方法を説明します。
translation-type: tm+mt
source-git-commit: 1e9596fb12a38f5c4c6e15d7c33af86e59e76083
workflow-type: tm+mt
source-wordcount: '2491'
ht-degree: 2%

---


# AEM GraphQL API for use with Content Fragments {#graphql-api-for-use-with-content-fragments}

>[!CAUTION]
>
>AEM GraphQL API(コンテンツフラグメント配信用)は、2021年の初めにリリースされます。
>
>関連ドキュメントは、既にプレビュー目的でご利用いただけます。

Cloud Service(AEM) GraphQL APIとしてのAdobe Experience Managerは、コンテンツフラグメントと共に使用される標準のオープンソースのGraphQL APIに大きく基づいています。

AEMでGraphQL APIを使用すると、ヘッドレスCMS実装のJavaScriptクライアントに対して、コンテンツフラグメントを効率的に配信できます。

* RESTと同様に、反復的なAPIリクエストの回避、
* 配信が特定の要件に限定されていることの確認、
* 単一のAPIクエリに応答してレンダリングに必要なものを一括配信できます。

## GraphQL API {#graphql-api}

*「GraphQLは、2012年にFacebookが内部で開発したデータクエリ言語および仕様です。2015年にはGraphQLが正式にオープンソースとなる前に、Facebookが開発しました。開発者の生産性を高め、転送されるデータ量を最小限に抑える目的で、RESTベースのアーキテクチャに代わる手段を提供します。 GraphQLは、あらゆる規模の数百の組織が実稼働環境で使用しています。&quot;*[GraphQL Foundation](https://foundation.graphql.org/)を参照してください。

GraphQL APIの詳細については、以下の節を参照してください（その他多くのリソース）。

* [graphql.org](https://graphql.org):

   * [GraphQLの概要](https://graphql.org/learn)

   * [GraphQL仕様](http://spec.graphql.org/)

* [graphql.com](https://graphql.com):

   * [ガイド](https://www.graphql.com/guides/)

   * [チュートリアル](https://www.graphql.com/tutorials/)

   * [導入事例](https://www.graphql.com/case-studies/)

AEM向けのGraphQLの実装は、標準のGraphQL Javaライブラリに基づいています。 次のページを参照してください。

* [graphQL.org - Java](https://graphql.org/code/#java)

* [GraphQL Java at GitHub](https://github.com/graphql-java)

## GraphicQL Interface {#graphiql-interface}

AEM Graph APIには、標準の[GraphiQL](https://graphql.org/learn/serving-over-http/#graphiql)インターフェイスの実装が含まれています。 これにより、クエリを直接入力、テストできます。

次に例を示します。

* `http://localhost:4502/content/graphiql.html`

構文の強調表示、オートコンプリート、オートコンプリートなどの機能と、履歴およびオンラインドキュメントが提供されます。

![GraphicQL ](assets/cfm-graphiql-interface.png "InterfaceGraphiQLインタフェース")

## 作成および公開環境の使用例{#use-cases-author-publish-environments}

使用例は、Cloud Service環境としてのAEMのタイプに応じて異なります。

* 発行環境;使用目的：
   * JSアプリケーションのクエリデータ（標準の使用例）

* 作成者環境;使用目的：
   * 「コンテンツ管理目的」のクエリデータ：
      * AEMのCloud ServiceとしてのGraphQLは、現在読み取り専用APIです。
      * REST APIはCR(u)D操作に使用できます。

## スキーマ生成{#schema-generation}

GraphQLは、厳密に型指定されたAPIです。つまり、データは型別に明確に構造化、整理する必要があります。

GraphQLの仕様には、特定のインスタンスでデータを取り調べる堅牢なAPIを作成する方法に関する一連のガイドラインが記載されています。 これを行うには、クライアントは[スキーマ](#schema-generation)を取得する必要があります。この中には、クエリに必要なすべての型が含まれています。

コンテンツフラグメントの場合、GraphQLスキーマ（構造と型）は、[コンテンツフラグメントモデル](/help/assets/content-fragments/content-fragments-models.md)とそのデータ型に基づきます。

例えば、ユーザーが`Article`という名前のコンテンツフラグメントモデルを作成した場合、AEMは`ArticleModel`型のオブジェクト`article`を生成します。 この型に含まれるフィールドは、モデルで定義されているフィールドとデータ型に対応しています。

1. コンテンツフラグメントモデル：

   ![GraphQLContent Fragment Modelで使用する](assets/cfm-graphqlapi-01.png "GraphQLで使用するコンテンツフラグメントモデル")

1. 対応するGraphQLスキーマ（GraphiQL自動ドキュメントiからの出力）:
   ![Graphコンテンツフラグメントに基づくGraphQLスキーマ](assets/cfm-graphqlapi-02.png "ModelGraphコンテンツフラグメントモデルに基づくQLスキーマ")

   これは、生成された型`ArticleModel`に複数の[フィールド](#fields)が含まれていることを示します。

   * そのうちの3つは、ユーザーが制御しています。`author`、`main`、`linked_article`。

   * その他のフィールドはAEMによって自動的に追加され、特定のコンテンツフラグメントに関する情報を提供するのに役立つ方法を示します。この例では、`_path`、`_metadata`、`_variations`です。 これらの[ヘルパーフィールド](#helper-fields)は、ユーザーが定義したものと自動生成されたものを区別するために、前に`_`が付いています。

1. ユーザーが記事のモデルに基づいてコンテンツフラグメントを作成した後、GraphQLで調査できます。 例については、[サンプルクエリ](/help/assets/content-fragments/content-fragments-graphql-samples.md#graphql-sample-queries)（GraphQL](/help/assets/content-fragments/content-fragments-graphql-samples.md#content-fragment-structure-graphql)で使用する[サンプルコンテンツフラグメント構造に基づく）を参照してください。

AEM用のGraphQLでは、スキーマは柔軟です。 つまり、コンテンツフラグメントモデルを作成、更新、または削除するたびに、自動生成されます。 また、データスキーマキャッシュは、コンテンツフラグメントモデルを更新する際にも更新されます。

Sites GraphQLサービスは、コンテンツフラグメントモデルに対する変更を（バックグラウンドで）リッスンします。 更新が検出されると、スキーマのその部分のみが再生成されます。 この最適化により、時間を節約し、安定性を提供します。

例えば、次のような場合、

1. `Content-Fragment-Model-1`と`Content-Fragment-Model-2`を含むパッケージをインストールします。

   1. `Model-1`と`Model-2`のGraphQL型が生成されます。

1. 次に`Content-Fragment-Model-2`を変更します。

   1. `Model-2` GraphQLタイプのみが更新されます。

   1. `Model-1`は同じままです。

>[!NOTE]
>
>REST apiを使用してコンテンツフラグメントモデルの一括更新を行う場合や、その他の方法で行う場合に備えて、この点に注意してください。

スキーマは、GraphQLクエリと同じエンドポイントを通じて提供され、クライアントはスキーマが拡張子`GQLschema`で呼び出されたことを処理します。 例えば、`/content/graphql/endpoint.GQLschema`で単純な`GET`リクエストを実行すると、Content-typeのスキーマが出力されます。`text/x-graphql-schema;charset=iso-8859-1`。

## フィールド {#fields}

スキーマ内には2つの基本的なカテゴリから成る個々のフィールドがあります。

* 生成するフィールド。

   選択した[フィールドタイプ](#field-types)は、コンテンツフラグメントモデルの設定方法に基づいてフィールドを作成するために使用されます。 フィールド名は、**データタイプ**&#x200B;の&#x200B;**プロパティ名**&#x200B;フィールドから取得されます。

   * また、**Render As**&#x200B;プロパティも考慮する必要があります。これは、ユーザーが特定のデータ型を設定できるからです。例えば、1行のテキストや複数フィールドなどです。

* AEM用のGraphQLでも、[ヘルパーフィールド](#helper-fields)が多数生成されます。

   これらは、コンテンツフラグメントを識別するため、またはコンテンツフラグメントに関する詳細を取得するために使用されます。

### フィールドタイプ{#field-types}

AEM用のGraphQLは、タイプのリストをサポートしています。 サポートされるすべてのコンテンツフラグメントモデルのデータ型と、対応するGraphQLの型が表されます。

| コンテンツフラグメントモデル — データタイプ | GraphQL Type | 説明 |
|--- |--- |--- |
| 1 行のテキスト | 文字列， [文字列] |  作成者名、場所名などの単純な文字列に使用します。 |
| 複数行テキスト | String |  記事の本文などのテキストの出力に使用します。 |
| 数値 |  浮動小数点， [浮動小数点] | 浮動小数点数と正規数を表示するのに使用します。 |
| Boolean |  Boolean |  チェックボックスの表示に使用→単純なtrue/false文 |
| 日時 | カレンダー |  ISO 8086形式で日時を表示するために使用します。 |
| 列挙 |  String |  モデルの作成時に定義されたオプションのリストからオプションを表示するために使用します。 |
|  タグ |  [String] |  AEMで使用されるタグを表す文字列のリストを表示するために使用します。 |
| コンテンツ参照 |  文字列 |  AEMで別のアセットへのパスを表示するために使用します。 |
| フラグメント参照 |  *モデルタイプ* |  特定のモデルタイプの別のコンテンツフラグメントを参照するために使用します。モデルの作成時に定義されます。 |

### ヘルパーフィールド{#helper-fields}

ユーザー生成フィールドのデータ型に加えて、AEM用のGraphQLでは、コンテンツフラグメントの識別やコンテンツフラグメントに関する追加情報の提供に役立つために、多数の&#x200B;*ヘルパー*&#x200B;フィールドも生成されます。

#### パス {#path}

パスフィールドは、GraphQLで識別子として使用されます。 これは、AEMリポジトリ内のコンテンツフラグメントアセットのパスを表します。 コンテンツフラグメントの識別子としてこれを選択しました。理由は次のとおりです。

* はAEM内で一意です。
* 簡単に取り込める

次のコードは、コンテンツフラグメントモデル`Person`に基づいて作成されたすべてのコンテンツフラグメントのパスを表示します。

```xml
{
  persons {
    items {
      _path
    }
  }
}
```

特定の種類のコンテンツフラグメントを1つ取得するには、まずそのパスを決定する必要もあります。 次に例を示します。

```xml
{
    person(_path="/content/dam/path/to/fragment/john-doe") {
        _path
        name
        first-name
    }
}
```

[サンプルクエリ — 単一の都市フラグメント](/help/assets/content-fragments/content-fragments-graphql-samples.md#sample-single-city-fragment)を参照してください。

#### メタデータ {#metadata}

また、AEMはGraphQLを通じて、コンテンツフラグメントのメタデータを公開します。 メタデータは、コンテンツフラグメントのタイトル、サムネールパス、コンテンツフラグメントの説明、作成日など、コンテンツフラグメントを説明する情報です。

メタデータはスキーマエディターを通して生成され、特定の構造を持たないので、`TypedMetaData` GraphQL型はコンテンツフラグメントのメタデータを公開するために実装されました。 `TypedMetaData` 次のスカラー型でグループ化された情報を公開します。

| フィールド |
|--- |
| `stringMetadata:[StringMetadata]!` |
| `stringArrayMetadata:[StringArrayMetadata]!` |
| `intMetadata:[IntMetadata]!` |
| `intArrayMetadata:[IntArrayMetadata]!` |
| `floatMetadata:[FloatMetadata]!` |
| `floatArrayMetadata:[FloatArrayMetadata]!` |
| `booleanMetadata:[BooleanMetadata]!` |
| `booleanArrayMetadata:[booleanArrayMetadata]!`  |
| `calendarMetadata:[CalendarMetadata]!` |
| `calendarArrayMetadata:[CalendarArrayMetadata]!` |

各スカラ型は、名前と値のペアの1つを表すか、名前と値のペアの配列を表します。このペアの値は、グループ化された型の値です。

例えば、コンテンツフラグメントのタイトルを取得する場合、このプロパティがStringプロパティであることがわかっているので、すべての文字列メタデータをクエリします。

メタデータのクエリを作成するには：

```xml
{
  person(_path: "/content/dam/path/to/fragment/john-doe") {
    _path
    _metadata {
      stringMetadata {
        name
        value
      }
    }
  }
}
```

「Generated GraphQL」スキーマを表示する場合は、すべてのメタデータGraphQLタイプを表示できます。 すべてのモデルタイプは同じ`TypedMetaData`を持ちます。

>[!NOTE]
>
>**標準と配列のメタデータの違い**
>`StringMetadata`と`StringArrayMetadata`はどちらも、リポジトリに格納されているものを参照し、取得方法ではありません。
>
>例えば、`stringMetadata`フィールドを呼び出すと、リポジトリに格納されているすべてのメタデータの配列が`String`として受け取られ、`stringArrayMetadata`を呼び出すと、リポジトリに格納されているすべてのメタデータの配列が`String[]`として受け取られます。

詳しくは、[メタデータのサンプルクエリ — 賞のメタデータのリスト(GB](/help/assets/content-fragments/content-fragments-graphql-samples.md#sample-metadata-awards-gb))を参照してください。

#### バリエーション {#variations}

`_variations`フィールドは、コンテンツフラグメントのバリエーションに対するクエリを簡略化するために実装されました。 次に例を示します。

```xml
{
  person(_path: "/content/dam/path/to/fragment/john-doe") {
    _variations
  }
}
```

[サンプルクエリ — 名前の付いたバリエーションのあるすべての市区町村](/help/assets/content-fragments/content-fragments-graphql-samples.md#sample-cities-named-variation)を参照してください。

<!--
## Security Considerations {#security-considerations}
-->

## GraphQL変数{#graphql-variables}

GraphQLでは、変数のクエリへの配置が許可されています。 詳しくは、GraphiQL](https://graphql.org/learn/queries/#variables)の[GraphQLドキュメントを参照してください。

例えば、特定のバリエーションを持つタイプ`Article`のすべてのコンテンツフラグメントを取得するには、GraphiQLで変数`variation`を指定します。

![GraphQL ](assets/cfm-graphqlapi-03.png "VariablesGraphQL変数")

```xml
### query
query GetArticlesByVariation($variation: String!) {
    articles(variation: $variation) {
        items {
            _path
            author
        }
    }
}
 
### in query variables
{
    "variation": "uk"
}
```

## GraphQLディレクティブ{#graphql-directives}

GraphQLでは、GraphQL Directivesと呼ばれる変数に基づいてクエリを変更する可能性があります。

例えば、`adventurePrice`フィールドは、変数`includePrice`に基づいて、すべての`AdventureModels`のクエリに含めることができます。

![GraphQL ](assets/cfm-graphqlapi-04.png "DirectivesGraphQLディレクティブ")

```xml
query getAdventureByType($includePrice: Boolean!) {
  adventures {
    items {
      adventureType
      adventurePrice @include(if: $includePrice)
    }
  }
}
 
### in query variables
{
    "includePrice": true
}
```

## 持続的なクエリ（キャッシュ） {#persisted-queries-caching}

POST要求を使用してクエリを準備した後、HTTPキャッシュまたはCDNでキャッシュできるGET要求を使用して実行できます。

POSTクエリは通常キャッシュされないので、このパラメーターが必要です。クエリをパラメーターとして使用する場合、HTTPサービスや中間体にとってパラメーターが大きくなりすぎるリスクが大きくなります。

特定のクエリを保持するために必要な手順は次のとおりです。

>[!NOTE]
>これより前に、適切な設定に対して&#x200B;**GraphQL Persistenceクエリ**&#x200B;を有効にする必要があります。 詳しくは、[設定ブラウザーでコンテンツフラグメント機能を有効にする](/help/assets/content-fragments/content-fragments-configuration-browser.md#enable-content-fragment-functionality-in-configuration-browser)を参照してください。

1. 新しいエンドポイントURL `/graphql/persist.json/<config>/<persisted-label>`にPUTしてクエリを準備します。

   例えば、持続的なクエリを作成します。

   ```xml
   $ curl -X PUT \
       -H 'authorization: Basic YWRtaW46YWRtaW4=' \
       -H "Content-Type: application/json" \
       "http://localhost:4502/graphql/persist.json/wknd/plain-article-query" \
       -d \
   '{
     articleList {
       items{
           _path
           author
           main {
               json
           }
       }
     }
   }'
   ```

1. この時点で、応答を確認します。

   例えば、成功を確認します。

   ```xml
   {
     "action": "create",
     "configurationName": "wknd",
     "name": "plain-article-query",
     "shortPath": "/wknd/plain-article-query",
     "path": "/conf/wknd/settings/graphql/persistentQueries/plain-article-query"
   }
   ```

1. その後、URL `/graphql/execute.json/<shortPath>`をGETすることで、永続化されたクエリを再生できます。

   例えば、持続的なクエリを使用します。

   ```xml
   $ curl -X GET \
       http://localhost:4502/graphql/execute.json/wknd/plain-article-query
   ```

1. 永続化されたクエリを既存のクエリパスにPOSTingで更新します。

   例えば、持続的なクエリを使用します。

   ```xml
   $ curl -X POST \
       -H 'authorization: Basic YWRtaW46YWRtaW4=' \
       -H "Content-Type: application/json" \
       "http://localhost:4502/graphql/persist.json/wknd/plain-article-query" \
       -d \
   '{
     articleList {
       items{
           _path
           author
           main {
               json
           }
         referencearticle {
           _path
         }
       }
     }
   }'
   ```

1. ラップされたプレーンクエリを作成します。

   次に例を示します。

   ```xml
   $ curl -X PUT \
       -H 'authorization: Basic YWRtaW46YWRtaW4=' \
       -H "Content-Type: application/json" \
       "http://localhost:4502/graphql/persist.json/wknd/plain-article-query-wrapped" \
       -d \
   '{ "query": "{articleList { items { _path author main { json } referencearticle { _path } } } }"}'
   ```

1. キャッシュ制御を使用して、ラップされたプレーンクエリを作成します。

   次に例を示します。

   ```xml
   $ curl -X PUT \
       -H 'authorization: Basic YWRtaW46YWRtaW4=' \
       -H "Content-Type: application/json" \
       "http://localhost:4502/graphql/persist.json/wknd/plain-article-query-max-age" \
       -d \
   '{ "query": "{articleList { items { _path author main { json } referencearticle { _path } } } }", "cache-control": { "max-age": 300 }}'
   ```

1. 次のパラメーターを使用して、永続化されたクエリを作成します。

   次に例を示します。

   ```xml
   $ curl -X PUT \
       -H 'authorization: Basic YWRtaW46YWRtaW4=' \
       -H "Content-Type: application/json" \
       "http://localhost:4502/graphql/persist.json/wknd/plain-article-query-parameters" \
       -d \
   'query GetAsGraphqlModelTestByPath($apath: String!, $withReference: Boolean = true) {
     articleByPath(_path: $apath) {
       item {
         _path
           author
           main {
           plaintext
           }
           referencearticle @include(if: $withReference) {
           _path
           }
         }
       }
     }'
   ```

1. パラメーターを使用したクエリの実行

   次に例を示します。

   ```xml
   $ curl -X POST \
       -H 'authorization: Basic YWRtaW46YWRtaW4=' \
       -H "Content-Type: application/json" \
       "http://localhost:4502/graphql/execute.json/wknd/plain-article-query-parameters;apath=%2fcontent2fdam2fwknd2fen2fmagazine2falaska-adventure2falaskan-adventures;withReference=false"
   
   $ curl -X GET \
       "http://localhost:4502/graphql/execute.json/wknd/plain-article-query-parameters;apath=%2fcontent2fdam2fwknd2fen2fmagazine2falaska-adventure2falaskan-adventures;withReference=false"
   ```

1. 発行時にクエリを実行するには、関連する永続的なツリーを複製する必要があります

   * レプリケーションにPOSTを使用する：

      ```xml
      $curl -X POST   http://localhost:4502/bin/replicate.json \
        -H 'authorization: Basic YWRtaW46YWRtaW4=' \
        -F path=/conf/wknd/settings/graphql/persistentQueries/plain-article-query \
        -F cmd=activate
      ```

   * パッケージの使用：
      1. 新しいパッケージ定義を作成します。
      1. 設定を含めます（例：`/conf/wknd/settings/graphql/persistentQueries`）。
      1. パッケージをビルドします。
      1. パッケージを複製します。
   * レプリケーション/配布ツールを使用する。
      1. [配布]ツールに移動します。
      1. 設定のツリーアクティベーション（例：`/conf/wknd/settings/graphql/persistentQueries`）を選択します。
   * ワークフローの使用（ワークフローランチャーの設定を使用）:
      1. 異なるイベント（作成、変更など）に設定を複製するワークフローモデルを実行するためのワークフロー起動ルールを定義します。



1. クエリの設定が公開になると、公開エンドポイントを使用するだけで、同じ原則が適用されます。

   >[!NOTE]
   >
   >匿名アクセスの場合、システムは、ACLによって「全員」がクエリ設定へのアクセスを許可されていると想定します。
   >
   >そうでないと実行できなくなります。

   >[!NOTE]
   >
   >URL内のセミコロン(&quot;;&quot;)は、エンコードする必要があります。
   >
   >例えば、持続的なクエリを実行する要求の場合と同様に、次のように指定します。
   >
   >
   ```xml
   >curl -X GET \ "http://localhost:4502/graphql/execute.json/wknd/plain-article-query-parameters%3bapath=%2fcontent2fdam2fwknd2fen2fmagazine2falaska-adventure2falaskan-adventures;withReference=false"
   >```

## 外部WebサイトからのGraphQLエンドポイントのクエリ{#query-graphql-endpoint-from-external-website}

>[!NOTE]
>
>AEMでのCORSリソース共有ポリシーの詳細については、「[接触チャネル間のリソース共有(CORS)について](https://experienceleague.adobe.com/docs/experience-manager-learn/foundation/security/understand-cross-origin-resource-sharing.html?lang=en#understand-cross-origin-resource-sharing-(cors))」を参照してください。

サードパーティのWebサイトでJSON出力を使用できるようにするには、顧客のGitリポジトリでCORSポリシーを設定する必要があります。 これは、目的のエンドポイントに適切なOSGi CORS設定ファイルを追加することで行います。 この設定では、アクセスを許可する信頼できるWebサイト名(regex)を指定する必要があります。

* GraphQLエンドポイントへのアクセス：

   * alloworigin:[ドメイン]またはalloworiginregexp:[ドメインのregex]
   * supportedmethods:[POST]
   * allowedpaths:[&quot;/apps/graphql-enablement/content/endpoint.gql(/persisted)?&quot;]

* GraphQLで持続的なクエリエンドポイントへのアクセス：

   * alloworigin:[ドメイン]またはalloworiginregexp:[ドメインのregex]
   * supportedmethods:[GET]
   * allowedpaths:[&quot;/graphql/execute.json/.*&quot;]

>[!CAUTION]
>
>お客様は、次のことを行う責任を負います。
>
>* 信頼済みドメインへのアクセスのみを許可する
>* ワイルドカード[*]構文を使用しないGraphQLエンドポイントを世界中に公開する。



## フィルタ{#filtering}

また、GraphQLクエリでフィルタリングを使用して、特定のデータを返すこともできます。

フィルタリングでは、論理演算子と式に基づいた構文を使用します。

例えば、次を参照してください。

* aem拡張機能の[GraphQLの詳細](/help/assets/content-fragments/content-fragments-graphql-samples.md#graphql-some-extensions)

* [サンプルクエリで使用するためのサンプルコンテンツと](/help/assets/content-fragments/content-fragments-graphql-samples.md#content-fragment-structure-graphql) 構造

* [このサンプルの内容と構造を使用したクエリの例](/help/assets/content-fragments/content-fragments-graphql-samples.md#graphql-sample-queries-sample-content-fragment-structure)

* [WKNDプロジェクトに基づくサンプルクエリ](/help/assets/content-fragments/content-fragments-graphql-samples.md#sample-queries-using-wknd-project)

## 権限 {#permission}

権限は、アセットへのアクセスに必要な権限です。

<!-- to be addressed later -->

<!-- 
## Authentication {#authentication}
-->

<!-- to be addressed later -->

<!-- 
## Caching {#caching}
-->

<!-- to be addressed later -->

<!--
## Sorting {#sorting}
-->

<!-- to be addressed later -->

<!--
## Paging {#paging}
-->

## エンドポイント{#end-points}

エンドポイントは、AEM用のGraphQLへのアクセスに使用するパスです。 このパスを使用すると、次のことができます。

* GraphQLスキーマにアクセスする、
* GraphQLクエリの送信、
* (GraphQLクエリに対する)応答を受け取ります。

AEMのGraphQLサーブレットにアクセスするには、エンドポイントを設定する必要があります。 これには2つのOSGi設定も含まれます。

1. GraphQLスキーマを取得する要求に応答するSlingスキーマサーブレット：

   ![AEM SitesグラフQLスキーマサーブレット](assets/cfm-endpoint-01.png)

   * **セレクター** (`sling.servlet.selectors`)は空白のままにする必要があります。

   * **Resource Types** (`sling.servlet.resourceTypes`):GraphQLサーブレットがリスンするリソースタイプを定義します。次に例を示します。
      `graphql-enablement/components/endpoint`.

   * **Methods** (`sling.servlet.methods^)

      サーブレットがリッスンするHTTPメソッド。通常は`GET`です。

   * **拡張** (`sling.servlet.extensions`)

      スキーマサーブレットが応答する拡張子を指定します。 この場合、GraphQL仕様と互換性を持たせるために`GQLschema`が使用されます。

2. graphqlリクエストに応答するサーブレット：

   ![Apache Sling GraphQLサーブレット](assets/cfm-endpoint-02.png)

   * **セレクター** (`sling.servlet.selectors`)は空白のままにする必要があります。

   * **Resource Type** (`sling.servlet.resourceTypes`) GraphQLサーブレットが応答するリソースタイプ。例： `graphql-enablement/components/endpoint`

   * **Methods** (`sling.servlet.methods`) GraphQLサーブレットが応答する必要があるHTTPメソッド(通常は `GET` と `POST`)。

   * **拡張子** (`sling.servlet.extensions`) GraphQL要求をリッスンする拡張子です。通常はこれを受け入れ `gql`ます。

3. 次に、エンドポイント（これらの設定で定義されているsling:resourceTypeのノード）を作成する必要があります。
例えば、GraphQLスキーマを取得するためのエンドポイントを作成するには、`/apps/<my-site>/graphql`の下に新しいノードを作成します。

   * 名前：`endpoint`
   * プライマリタイプ：`nt:unstructured`
   * sling:resourceType: `graphql-enablement/components/endpoint`

## FAQ {#faqs}

次のような質問が生じました。

1. **Q**:「*GraphQL API for AEMとクエリビルダーAPIの違いは何ですか？*」

   * **A**:「AEM GraphQL API *オファーは、JSON出力の全体的な制御を行い、コンテンツのクエリを行う業界標準です。今後、AEMはAEM GraphQL APIへの投資を計画しています。*&quot;

## チュートリアル — AEMヘッドレスとGraphQLの使い始めに{#tutorial}

実践チュートリアルを探している場合 AEMのGraphQL APIを使用し、外部アプリで使用するコンテンツを、ヘッドレスCMSシナリオで構築して公開する方法を示す[AEM HeadlessとGraphQL](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/graphql/overview.html)のエンドツーエンドのチュートリアルをご覧ください。