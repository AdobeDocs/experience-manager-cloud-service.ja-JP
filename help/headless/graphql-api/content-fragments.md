---
title: コンテンツフラグメントと共に使用する AEM GraphQL API
description: Adobe Experience Manager（AEM）as a Cloud Service のコンテンツフラグメントを AEM GraphQL API と共に使用してヘッドレスコンテンツ配信を実現する方法を説明します。
feature: Content Fragments,GraphQL API
exl-id: bdd60e7b-4ab9-4aa5-add9-01c1847f37f6
source-git-commit: e90b400d37cb380476a941c526fdadcd615c118a
workflow-type: tm+mt
source-wordcount: '4174'
ht-degree: 58%

---


# コンテンツフラグメントと共に使用する AEM GraphQL API {#graphql-api-for-use-with-content-fragments}

Adobe Experience Manager（AEM）as a Cloud Service のコンテンツフラグメントを AEM GraphQL API と共に使用してヘッドレスコンテンツ配信を実現する方法を説明します。

コンテンツフラグメントと共に使用する AEM as a Cloud Service GraphQL API は、オープンソースの標準 GraphQL API に大きく依存しています。

AEM の GraphQL API を使用すると、ヘッドレス CMS 実装の JavaScript クライアントにコンテンツフラグメントを効率的に配信できます。

* REST で API リクエストの反復を回避
* 特定の要件に限定された配信を確保
* 1 つの API クエリへの応答としてレンダリングに必要なものだけを一括配信

>[!NOTE]
>
>GraphQL は現在、Adobe Experience Manager（AEM）as a Cloud Service の、2 つの（個別の）シナリオで使用されています。
>
>* [AEM Commerce が、GraphQL 経由でコマースプラットフォームのデータを使用する](/help/commerce-cloud/integrating/magento.md)。
>* AEM コンテンツフラグメントが、AEM GraphQL API（標準の GraphQL に基づくカスタム実装）と連携して、アプリケーションで使用するための構造化コンテンツを配信する。


## GraphQL API {#graphql-api}

GraphQL とは次のことを意味します。

* 「*...API のクエリ言語と、既存のデータを使用してこれらのクエリを満たすランタイムです。GraphQL は、API のデータの完全で理解可能な説明を提供し、必要なものを正確に要求する力をクライアントに与え、API の長期的な発展を促し、強力な開発ツールの実現を可能にします。*」

   [GraphQL.org](https://graphql.org) を参照

* 「*...柔軟な API レイヤー用のオープンな仕様。GraphQL を既存のバックエンドに重ね合わせて、以前に比べて迅速に製品を構築…。*」

   「[Explore GraphQL](https://www.graphql.com)」を参照

* *「...2012 年に Facebook 社内で開発されたデータクエリ言語および仕様です。その後、2015 年には公式にオープンソースとなりました。開発者の生産性を高め、転送データの量を最小限に抑えるために、REST ベースのアーキテクチャに代わる手段を提供します。GraphQL は、あらゆる規模の数百の組織により実稼働環境で使用されています...」*

   [GraphQL Foundation](https://foundation.graphql.org/) を参照してください。

<!--
"*Explore GraphQL is maintained by the Apollo team. Our goal is to give developers and technical leaders around the world all of the tools they need to understand and adopt GraphQL.*". 
-->

GraphQL API の詳細については、（多くのリソースの中でも特に）以下を参照してください。

* [graphql.org](https://graphql.org)：

   * [GraphQL の概要](https://graphql.org/learn)

   * [GraphQL の仕様](https://spec.graphql.org/)

* [graphql.com](https://graphql.com)：

   * [ガイド](https://www.graphql.com/guides/)

   * [チュートリアル](https://www.graphql.com/tutorials/)

   * [導入事例](https://www.graphql.com/case-studies/)

AEM 用 GraphQL の実装は、標準の GraphQL Java ライブラリをベースにしています。以下を参照してください。

* [graphQL.org - Java](https://graphql.org/code/#java)

* [GitHub の GraphQL Java](https://github.com/graphql-java)

### GraphQL 用語 {#graphql-terminology}

GraphQL では次を使用します。

* **[クエリ](https://graphql.org/learn/queries/)**

* **[スキーマとタイプ](https://graphql.org/learn/schema/)**：

   * スキーマは、コンテンツフラグメントモデルに基づいて AEM で生成されます。
   * GraphQL では、スキーマを使用して、AEM 用 GraphQL の実装で使用可能なタイプと操作を提供します。

* **[フィールド](https://graphql.org/learn/queries/#fields)**

* **[GraphQL エンドポイント](graphql-endpoint.md)**
   * GraphQL クエリに応答し、GraphQL スキーマへのアクセスを提供する AEM 内のパス。

   * 詳しくは、[GraphQL エンドポイントの有効化](graphql-endpoint.md)を参照してください。

[ベストプラクティス](https://graphql.org/learn/best-practices/)を含む包括的な詳細については、「[(GraphQL.org) GraphQL の概要](https://graphql.org/learn/)」を参照してください。

### GraphQL クエリタイプ {#graphql-query-types}

GraphQL では、次のいずれかを返すクエリを実行できます。

* **1 つのエントリ**

* **[エントリのリスト](https://graphql.org/learn/schema/#lists-and-non-null)**

AEMは、クエリ（両方のタイプ）をに変換する機能を提供します。 [キャッシュ可能な永続クエリ](/help/headless/graphql-api/persisted-queries.md) Dispatcher と CDN によって

### GraphQLクエリのベストプラクティス（Dispatcher と CDN） {#graphql-query-best-practices}

この [永続クエリ](/help/headless/graphql-api/persisted-queries.md) パブリッシュインスタンスでは、次のように使用することをお勧めします。

* キャッシュされます
* AEM as a Cloud Service で一元管理されます

>[!NOTE]
>
>通常、オーサー環境には Dispatcher/CDN がないので、そこでの永続化されたクエリの使用に利益はありません。テスト以外に

POST要求を使用するGraphQLクエリはキャッシュされないので、お勧めしません。そのため、デフォルトインスタンスでは、Dispatcher は、このようなクエリをブロックするように設定されています。

GraphQLはGETリクエストもサポートしますが、これらの制限（URL の長さなど）に達して、永続化クエリを使用するのを避けることができます。

>[!NOTE]
>
>Dispatcher での直接クエリや POST クエリを許可するには、システム管理者に次の操作を依頼してください。
>
>* の作成 [Cloud Manager 環境変数](/help/implementing/cloud-manager/environment-variables.md) 呼び出し `ENABLE_GRAPHQL_ENDPOINT`
>* （値：`true`）


>[!NOTE]
>
>直接クエリを実行する機能は、将来、廃止される可能性があります。

### GraphiQL IDE {#graphiql-ide}

また、[GraphiQL IDE](/help/headless/graphql-api/graphiql-ide.md) を使用して、GraphQL クエリのテストとデバッグを行うこともできます。

## オーサー環境とパブリッシュ環境の使用例 {#use-cases-author-publish-environments}

使用例は、AEM as a Cloud Service 環境のタイプに応じて異なる場合があります。

* パブリッシュ環境の使用目的：
   * JS アプリケーションのデータのクエリ（標準の使用例）

* オーサー環境の使用目的：
   * 「コンテンツ管理用」のデータのクエリ：
      * AEM as a Cloud Service の GraphQL は現在読み取り専用の API です。
      * REST API は、CR(U)D の操作に使用できます。

## 権限 {#permission}

Assets へのアクセスに必要な権限です。

GraphQLクエリは、基になるリクエストのAEMユーザーの権限で実行されます。 一部のフラグメント（Assets として保存）への読み取りアクセス権を持っていない場合、ユーザーは結果セットに含まれません。

また、GraphQLクエリを実行するには、ユーザーがGraphQLエンドポイントにアクセスできる必要があります。

## スキーマ生成 {#schema-generation}

GraphQL は、厳密に型指定された API です。つまり、データは型別に明確に構造化され編成される必要があります。

GraphQL の仕様には、特定のインスタンス上のデータをクエリするための堅牢な API を作成する方法に関する一連のガイドラインが用意されています。そのタスクを行うには、クライアントは[スキーマ](#schema-generation)を取得する必要があります。この中には、クエリに必要なすべての型が定義されています。

コンテンツフラグメントの場合、GraphQL スキーマ（構造とタイプ）は、**有効**&#x200B;な[コンテンツフラグメントモデル](/help/sites-cloud/administering/content-fragments/content-fragments-models.md)とそれらのデータタイプに基づいています。

>[!CAUTION]
>
>（**有効**&#x200B;になっているコンテンツフラグメントモデルから派生した）すべての GraphQL スキーマは、GraphQL エンドポイントを通じて読み取り可能です。
>
>つまり、漏洩するおそれがあるので、機密データが使用可能になっていないことを確認する必要があります。例えば、これには、モデル定義のフィールド名として存在する可能性のある情報が含まれます。

例えば、ユーザーが `Article`を生成した場合、AEMはGraphQLタイプを生成します `ArticleModel`. この型に含まれるフィールドは、モデルで定義されているフィールドとデータ型に対応しています。さらに、このタイプに対して動作するクエリのエントリポイント（例： ）が作成されます。 `articleByPath` または `articleList`.

1. コンテンツフラグメントモデル：

   ![GraphQL で使用するコンテンツフラグメントモデル](assets/cfm-graphqlapi-01.png "GraphQL で使用するコンテンツフラグメントモデル")

1. 対応する GraphQL スキーマ（GraphiQL 自動生成ドキュメントからの出力）:
   ![コンテンツフラグメントモデルに基づく GraphQL スキーマ](assets/cfm-graphqlapi-02.png "コンテンツフラグメントモデルに基づく GraphQL スキーマ")

   この図では、生成された型 `ArticleModel` に複数の[フィールド](#fields)が含まれていることがわかります。

   * そのうちの 3 つ（`author`、`main`、`referencearticle`）は、ユーザーが管理しています。

   * その他のフィールドはAEMによって自動的に追加され、特定のコンテンツフラグメントに関する情報を提供する便利な方法を示します。この例では、 [ヘルパーフィールド](#helper-fields)) `_path`, `_metadata`, `_variations`.

1. ユーザーが Article モデルに基づいてコンテンツフラグメントを作成すると、GraphQL を使用してそれをクエリできます。例については、（[GraphQL で使用するコンテンツフラグメント構造のサンプル](/help/headless/graphql-api/sample-queries.md#content-fragment-structure-graphql)に基づいた）[サンプルクエリ](/help/headless/graphql-api/sample-queries.md#graphql-sample-queries)を参照してください。

AEM 用 GraphQL では、スキーマには柔軟性があります。つまり、コンテンツフラグメントモデルを作成、更新、削除するたびに、スキーマが自動生成されます。また、コンテンツフラグメントモデルを更新すると、データスキーマキャッシュも更新されます。

<!-- move the following to a separate "in depth" page -->

また、コンテンツフラグメントモデルを更新すると、データスキーマキャッシュも更新されます。

Sites GraphQL サービスは、コンテンツフラグメントモデルに対する変更を（バックグラウンドで）リッスンします。更新が検出されると、スキーマのその部分だけが再生成されます。この最適化により、時間が節約され、安定性も確保されます。

例えば、次のようになります。

1. `Content-Fragment-Model-1` と `Content-Fragment-Model-2` を含んだパッケージをインストールすると、

   1. `Model-1` と `Model-2` の GraphQL 型が生成されます。

1. 次に `Content-Fragment-Model-2` を変更すると、

   1. `Model-2` GraphQL 型だけが更新されます。

   1. 一方、`Model-1` は同じままです。

>[!NOTE]
>
>REST API を使用してコンテンツフラグメントモデルの一括更新を行う場合などには、この点に留意することが大切です。

スキーマは、GraphQL クエリと同じエンドポイントを通じて提供され、クライアントはスキーマが拡張子 `GQLschema` で呼び出されることに対処します。例えば、`/content/cq:graphql/global/endpoint.GQLschema` で単純な `GET` リクエストを実行すると、`text/x-graphql-schema;charset=iso-8859-1` の Content-type を持つスキーマが出力されます。

<!-- move through to here to a separate "in depth" page -->

### スキーマの生成 - 未公開のモデル {#schema-generation-unpublished-models}

コンテンツフラグメントがネストされると、親のコンテンツフラグメントモデルは公開されますが、参照モデルは公開されません。

>[!NOTE]
>
>AEM UI はこのような問題を回避しますが、プログラムを使用して、またはコンテンツパッケージを使用して公開すると、この問題が発生する可能性があります。

この場合、AEM は親コンテンツフラグメントモデルの&#x200B;*不完全な*&#x200B;スキーマを生成します。つまり、非公開のモデルに依存するフラグメント参照がスキーマから削除されます。

## フィールド {#fields}

スキーマ内には、次の 2 つの基本的なカテゴリに属する個々のフィールドがあります。

* ユーザーが生成するフィールド

   次の項目を選択： [データタイプ](#Data-types) は、コンテンツフラグメントモデルの設定方法に基づいてフィールドを作成するために使用します。 フィールド名は **プロパティ名** フィールド **データタイプ** タブをクリックします。

   * また、 **レンダリング形式** ユーザーが特定のデータタイプを設定できるので、考慮に入れるように設定する必要があります。 例えば、1 行のテキストフィールドに複数の 1 行のテキストを含めるように設定するには、「 `multifield` をドロップダウンから選択します。

* AEM 用 GraphQL が生成する多数の[ヘルパーフィールド](#helper-fields)

### データタイプ {#data-types}

AEM 用 GraphQL では一連のタイプをサポートしています。サポートされているすべてのコンテンツフラグメントモデルデータ型と、それに対応する GraphQL 型を以下の表に示します。

| コンテンツフラグメントモデル - データ型 | GraphQL の型 | 説明 |
|--- |--- |--- |
| 1 行のテキスト | String、[String] |  作成者名、場所名などの単純な文字列に使用します。 |
| 複数行テキスト | String, [String] |  記事の本文などのテキストを出力するために使用します |
| Number |  Float、[Float] | 浮動小数点数と整数を表示するために使用します |
| Boolean |  Boolean |  チェックボックスを表示するために使用します（単純な真／偽のステートメント） |
| 日時 | Calendar |  日時を ISO 8086 形式で表示するために使用します。選択したタイプに応じて、AEM GraphQL で使用できるフレーバーは、`onlyDate`、`onlyTime`、`dateTime` の 3 つです。 |
| 定義済みリスト |  String |  モデルの作成時に定義されたオプションのリストに含まれるオプションを表示するために使用します |
|  タグ |  [String] |  AEM で使用されているタグを表す文字列のリストを表示するために使用します |
| コンテンツ参照 |  文字列, [文字列] |  AEM 内の別のアセットへのパスを表示するために使用します |
| フラグメント参照 |  *モデルタイプ* |  特定のモデルタイプの別のコンテンツフラグメントを参照するために使用します（モデルの作成時に定義されます） |

### ヘルパーフィールド {#helper-fields}

ユーザー生成フィールドのデータ型に加えて、AEM 用 GraphQL では、コンテンツフラグメントの識別やコンテンツフラグメントに関する追加情報の提供に役立つ多数の&#x200B;*ヘルパー*&#x200B;フィールドも生成されます。

これらの[ヘルパーフィールド](#helper-fields)は、ユーザーが定義したものと自動生成されたものを区別するために、先頭に `_` が付いています。

#### パス  {#path}

パスフィールドは、AEM GraphQLで識別子として使用されます。 これは、AEM リポジトリ内のコンテンツフラグメントアセットのパスを表します。コンテンツフラグメントの識別子としてこれを選択したのは、次の理由からです。

* AEM 内で一意である
* 取得しやすい

次のコードは、コンテンツフラグメントモデルに基づいて作成されたすべてのコンテンツフラグメントのパスを表示します `Author`（ WKND チュートリアルで提供される）

```graphql
{
  authorList {
    items {
      _path
    }
  }
}
```

特定のタイプのコンテンツフラグメントを 1 つ取得するには、まずそのパスも決定する必要があります。次に例を示します。

```graphql
{
  authorByPath(_path: "/content/dam/wknd-shared/en/contributors/sofia-sj-berg") {
    item {
      _path
      firstName
      lastName
    }
  }
}
```

[サンプルクエリ - 1 つの特定の都市フラグメント](/help/headless/graphql-api/sample-queries.md#sample-single-specific-city-fragment)を参照してください。

#### メタデータ {#metadata}

また、AEM では GraphQL を通じて、コンテンツフラグメントのメタデータも公開します。メタデータは、コンテンツフラグメントのタイトル、サムネールのパス、コンテンツフラグメントの説明、作成日など、コンテンツフラグメントを説明する情報です。

メタデータはスキーマエディターで生成され、特定の構造を持たないので、コンテンツフラグメントのメタデータを公開するために GraphQL 型 `TypedMetaData` が実装されました。`TypedMetaData` では、次のスカラー型でグループ化された情報を公開します。

| フィールド |
|--- |
| `stringMetadata:[StringMetadata]!` |
| `stringArrayMetadata:[StringArrayMetadata]!` |
| `intMetadata:[IntMetadata]!` |
| `intArrayMetadata:[IntArrayMetadata]!` |
| `floatMetadata:[FloatMetadata]!` |
| `floatArrayMetadata:[FloatArrayMetadata]!` |
| `booleanMetadata:[BooleanMetadata]!` |
| `booleanArrayMetadata:[booleanArrayMetadata]!` |
| `calendarMetadata:[CalendarMetadata]!` |
| `calendarArrayMetadata:[CalendarArrayMetadata]!` |

各スカラー型は、名前と値の 1 つのペアを表すか、名前と値のペアの配列を表します。このペアの値は、グループ化されたときの型になります。

例えば、コンテンツフラグメントのタイトルを取得する場合は、このプロパティが String 型プロパティであることがわかっているので、すべての String 型メタデータをクエリすることになります。

メタデータをクエリするには、次のようにします。

```graphql
{
  authorByPath(_path: "/content/dam/wknd-shared/en/contributors/sofia-sj-berg") {
    item {
      _metadata {
        stringMetadata {
          name
          value
        }
      }
    }
  }
}
```

生成された GraphQL スキーマを表示するには、すべてのメタデータ GraphQL 型を表示します。すべてのモデルタイプは同じ `TypedMetaData` を持ちます。

>[!NOTE]
>
>**標準メタデータと配列メタデータの違い**：
>`StringMetadata` と `StringArrayMetadata` はどちらも、リポジトリに格納されているものについての指定であり、その取得手段についての指定ではありません。
>
>例えば、`stringMetadata` フィールドを呼び出すと、リポジトリに `String` として格納されているすべてのメタデータの配列を受け取ることになります。一方、`stringArrayMetadata` を呼び出すと、リポジトリに `String[]` として格納されているすべてのメタデータの配列を受け取ります。

詳しくは、[メタデータのサンプルクエリ - 「GB」という賞のメタデータのリスト](/help/headless/graphql-api/sample-queries.md#sample-metadata-awards-gb)を参照してください。

#### バリエーション {#variations}

コンテンツフラグメントのバリエーションに対するクエリを簡略化するために、`_variations` フィールドが実装されています。次に例を示します。

```graphql
{
  authorByPath(_path: "/content/dam/wknd-shared/en/contributors/ian-provo") {
    item {
      _variations
    }
  }
}
```

>[!NOTE]
>
>なお、 `_variations` フィールドに次の値が含まれていない `master` バリエーション ( 技術的には元のデータ ( *マスター* （UI 内）は、明示的なバリエーションとは見なされません。

詳しくは、[サンプルクエリ - 名前付きバリエーションを持つすべての都市](/help/headless/graphql-api/sample-queries.md#sample-cities-named-variation)を参照してください。

>[!NOTE]
>
>コンテンツフラグメントに対して指定されたバリエーションが存在しない場合は、元のデータ（マスターバリエーションとも呼ばれます）が（フォールバック）デフォルトとして返されます。

<!--
## Security Considerations {#security-considerations}
-->

## GraphQL 変数 {#graphql-variables}

GraphQL では、クエリに変数を含めることができます。詳しくは、[GraphQL の変数に関するドキュメント](https://graphql.org/learn/queries/#variables)を参照してください。

例えば、すべてのタイプのコンテンツフラグメントを取得するには、次のようにします。 `Author` 特定のバリエーション（使用可能な場合）で、引数を指定できます `variation` （GraphiQL 内）

![GraphQL 変数](assets/cfm-graphqlapi-03.png "GraphQL 変数")

**クエリ**:

```graphql
query($variation: String!) {
  authorList(variation: $variation) {
    items {
      _variation
      lastName
      firstName
    }
  }
}
```

**クエリ変数**:

```json
{
  "variation": "another"
}
```

このクエリは、作成者の完全なリストを返します。 作成者 ( `another` バリエーションは元のデータ (`_variation` レポートの作成 `master` （この場合）。

指定したバリエーションを提供する作成者にリストを制限する場合（および元のデータにフォールバックされる作成者をスキップする場合）、 [フィルター](#filtering):

```graphql
query($variation: String!) {
  authorList(variation: $variation, filter: {
    _variation: {
      _expressions: {
        value: $variation
      }
    }
  }) {
    items {
      _variation
      lastName
      firstName
    }
  }
}
```

## GraphQL ディレクティブ {#graphql-directives}

GraphQL では、GraphQL ディレクティブと呼ばれる変数に基づいてクエリを変更する可能性があります。

例えば、変数 `includePrice` に基づいて、すべての `AdventureModels` のクエリに `adventurePrice` フィールドを含めることができます。

![GraphQL ディレクティブ](assets/cfm-graphqlapi-04.png "GraphQL ディレクティブ")

**クエリ**:

```graphql
query GetAdventureByType($includePrice: Boolean!) {
  adventureList {
    items {
      title
      price @include(if: $includePrice)
    }
  }
}
```

**クエリ変数**:

```json
{
    "includePrice": true
}
```

## フィルタリング {#filtering}

GraphQL クエリでフィルタリングを使用して、特定のデータを返すこともできます。

フィルタリングでは、論理演算子と論理式に基づいた構文を使用します。

最も原子的な部分は、特定のフィールドの内容に適用できる単一の式です。 フィールドの内容を指定された定数値と比較します。

例えば、式

```graphql
{
  value: "some text"
  _op: EQUALS
}
```

フィールドの内容と値を比較します `some text` コンテンツが値と等しい場合にが成功します。 そうしないと、式は失敗します。

 

次の演算子を使用して、フィールドを特定の値と比較できます。

| 演算子 | タイプ | 次の場合、式は成功します。 |
|--- |--- |--- |
| `EQUALS` | `String`、`ID`、`Boolean` | 値はフィールドの内容とまったく同じです |
| `EQUALS_NOT` | `String`、`ID` | 値は *not* フィールドのコンテンツと同じ |
| `CONTAINS` | `String` | ...フィールドのコンテンツに値 (`{ value: "mas", _op: CONTAINS }` 一致する `Christmas`, `Xmas`, `master`, ...) |
| `CONTAINS_NOT` | `String` | ...フィールドの内容は次の処理を行います。 *not* 値を含む |
| `STARTS_WITH` | `ID` | ID が特定の値 (`{ value: "/content/dam/", _op: STARTS_WITH` 一致する `/content/dam/path/to/fragment`ではなく `/namespace/content/dam/something` |
| `EQUAL` | `Int`、`Float` | 値はフィールドの内容とまったく同じです |
| `UNEQUAL` | `Int`、`Float` | 値は *not* フィールドのコンテンツと同じ |
| `GREATER` | `Int`、`Float` | フィールドの内容が値より大きい |
| `GREATER_EQUAL` | `Int`、`Float` | フィールドの内容が値以上です |
| `LOWER` | `Int`、`Float` | フィールドの内容が値より小さい |
| `LOWER_EQUAL` | `Int`、`Float` | フィールドの内容が値以下です |
| `AT` | `Calendar`、`Date`、`Time` | フィールドの内容は、値と完全に同じです（タイムゾーン設定を含む）。 |
| `NOT_AT` | `Calendar`、`Date`、`Time` | ...フィールドの内容は次のとおりです。 *not* 値と同じ |
| `BEFORE` | `Calendar`、`Date`、`Time` | ...値で示されるポイントインタイムが、フィールドのコンテンツで示されるポイントインタイムの前にある場合。 |
| `AT_OR_BEFORE` | `Calendar`、`Date`、`Time` | ...値で示される時点が、フィールドのコンテンツで示される同じ時点の前または前にある |
| `AFTER` | `Calendar`、`Date`、`Time` | ...値で示されるポイントインタイムが、フィールドのコンテンツで示されるポイントインタイムの後になっている。 |
| `AT_OR_AFTER` | `Calendar`、`Date`、`Time` | ...値で示される時点が、フィールドのコンテンツで示される時点の後または同じ時点にある |

また、式の評価方法を変更する追加のオプションを指定できるタイプもあります。

| オプション | タイプ | 説明 |
|--- |--- |--- |
| `_ignoreCase` | `String` | 文字列の大文字と小文字を無視します ( 例： `time` 一致する `TIME`, `time`, `tImE`, ... |
| `_sensitiveness` | `Float` | 特定の利益を `float` 同じと見なされる値（内部表現による技術的な制限を回避するため） `float` 値；このオプションはパフォーマンスに悪影響を与える可能性があるので、避ける必要があります |

式は、論理演算子 (`_logOp`):

* `OR`  — 少なくとも 1 つの式が成功した場合、式のセットは成功します
* `AND`  — すべての式が成功した場合、式のセットは成功します（デフォルト）

各フィールドは、独自の式のセットでフィルタリングできます。 フィルター引数で指定されたすべてのフィールドの式セットは、最終的に独自の論理演算子で結合されます。

フィルター定義 ( `filter` 引数をクエリに渡す ) には、次が含まれます。

* 各フィールドのサブ定義 ( フィールド名を使用してアクセスできます ( 例： `lastName` フィールドの `lastName` データ（フィールド）タイプのフィールド
* 各サブ定義には、 `_expressions` 配列を作成し、式セットと `_logOp` 式を組み合わせる論理演算子を定義するフィールド
* 各式は、値 (`value` フィールド ) と演算子 (`_operator` フィールド ) フィールドの内容を比較する必要があります

省略できます `_logOp` 項目を `AND` および `_operator` 等価を確認する場合は、これらがデフォルト値になるので、等価を確認します。

次の例は、 `lastName` / `Provo` または含む `sjö`（この場合とは無関係）。

```graphql
{
  authorList(filter: {
    lastname: {
      _logOp: OR
      _expressions: [
        {
          value: "sjö",
          _operator: CONTAINS,
          _ignoreCase: true
        },
        {
          value: "Provo"
        }
      ]
    }
  }) {
    items {
      lastName
      firstName
    }
  }
}
```

ネストされたフィールドに対してフィルタを適用することもできますが、パフォーマンスの問題を引き起こす可能性があるので、お勧めしません。

その他の例については、以下を参照してください。

* [AEM 用 GraphQL の拡張機能](#graphql-extensions)の詳細

* [このサンプルコンテンツおよび構造を使用したサンプルクエリ](/help/headless/graphql-api/sample-queries.md#graphql-sample-queries-sample-content-fragment-structure)

   * さらに、サンプルクエリ用に準備されている[サンプルコンテンツおよび構造](/help/headless/graphql-api/sample-queries.md#content-fragment-structure-graphql)

* [WKND プロジェクトに基づいたサンプルクエリ](/help/headless/graphql-api/sample-queries.md#sample-queries-using-wknd-project)

## 並べ替え {#sorting}

この機能を使用すると、指定したフィールドに従ってクエリ結果を並べ替えることができます。

並べ替え条件：

* は、フィールドパスを表す値のコンマ区切りリストです
   * リストの最初のフィールドでは主な並べ替え順が定義され、2 番目のフィールドでは主な並べ替え条件の 2 つの値が等しい場合に、3 番目のフィールドでは最初の 2 つの条件が等しい場合などに使用されます。
   * ドット表記（field1.subfield.subfield など）
* オプションの注文方向
   * ASC （昇順）または DESC （降順）;デフォルトの ASC が適用されるので
   * 方向は、フィールドごとに指定できます。つまり、あるフィールドを昇順で、別のフィールドを降順 (name、firstName DESC) で並べ替えることができます

次に例を示します。

```graphql
query {
  authorList(sort: "lastName, firstName") {
    items {
      firstName
      lastName
    }
  }
}
```

また、次のこともおこないます。

```graphql
{
  authorList(sort: "lastName DESC, firstName DESC") {
    items {
        lastName
        firstName
    }
  }
}
```

<!-- to be included? -->

ネストされたフラグメント内のフィールドでは、 `nestedFragmentname.fieldname`.

>[!NOTE]
>
>これは、パフォーマンスに悪影響を与える可能性があります。

次に例を示します。

```graphql
query {
  articleList(sort: "authorFragment.lastName")  {
    items {
      title
      authorFragment {
        firstName
        lastName
        birthDay
      }
      slug
    }
  }
}
```

## ページング {#paging}

この機能を使用すると、リストを返すクエリタイプに対してページングを実行できます。 次の 2 つの方法が用意されています。

* `offset` および `limit` 内 `List` クエリ
* `first` および `after` 内 `Paginated` クエリ

### リストクエリ — オフセットと制限 {#list-offset-limit}

内 `...List`使用できるクエリ `offset` および `limit` 特定の結果サブセットを返すには、次の手順に従います。

* `offset`:返す最初のデータセットを指定します
* `limit`:返すデータセットの最大数を指定します

例えば、最大 5 つの記事を含む結果のページを、 *完了* 結果リスト：

```graphql
query {
   articleList(offset: 5, limit: 5) {
    items {
      authorFragment {
        lastName
        firstName
      }
    }
  }
}
```

<!-- When available link to BP and replace "JCR query level" with a more neutral term. -->

<!-- When available link to BP and replace "JCR query result set" with a more neutral term. -->

>[!NOTE]
>
>* ページングでは、同じ結果セットの異なるページをリクエストする複数のクエリで正しく機能するには、安定した並べ替え順が必要です。 デフォルトでは、結果セットの各アイテムのリポジトリパスを使用して、順序が常に同じであることを確認します。 異なる並べ替え順を使用し、その並べ替えを JCR クエリレベルで実行できない場合、ページを決定する前に結果セット全体をメモリに読み込む必要があるので、パフォーマンスに悪影響が出ます。
>
>* オフセットが高いほど、JCR クエリの結果セット全体から項目をスキップするのに時間がかかります。 大きな結果セットに対する代替の解決策は、ページ分割されたクエリを `first` および `after` メソッド。


### ページ分割されたクエリ — 最初と次の後 {#paginated-first-after}

この `...Paginated` クエリタイプは、ほとんどの `...List` クエリタイプ機能（フィルタリング、並べ替え）を使用する代わりに、 `offset`/`limit` 引数の場合は、 `first`/`after` で定義された引数 [GraphQL Cursor Connections の仕様](https://relay.dev/graphql/connections.htm). より正式でない紹介は、 [GraphQLはじめに](https://graphql.org/learn/pagination/#pagination-and-edges).

* `first`:この `n` 返す最初の項目。
デフォルトは、`50` です。最大値はです。 `100`.
* `after`:リクエストされたページの先頭を決定するカーソル。カーソルで表される項目は結果セットに含まれないことに注意してください。項目のカーソルは、 `cursor` フィールド `edges` 構造。

例えば、最大 5 つの冒険を含む結果のページを、 *完了* 結果リスト：

```graphql
query {
    adventurePaginated(first: 5, after: "ODg1MmMyMmEtZTAzMy00MTNjLThiMzMtZGQyMzY5ZTNjN2M1") {
        edges {
          cursor
          node {
            title
          }
        }
        pageInfo {
          endCursor
          hasNextPage
        }
    }
}
```

<!-- When available link to BP -->
<!-- Due to internal technical constraints, performance will degrade if sorting and filtering is applied on nested fields. Therefore it is recommended to use filter/sort fields stored at root level. For more information, see the [Best Practices document](link). -->

>[!NOTE]
>
>* デフォルトでは、ページングでは、結果の順序が常に同じになるように、フラグメントを表すリポジトリノードの UUID を使用して順序を指定します。 条件 `sort` が使用されている場合、UUID は暗黙的に使用されて一意の並べ替えがおこなわれます。同じ並べ替えキーを持つ 2 つの項目の場合も同様です。
>
>* ネストされたフィールドに並べ替えとフィルタリングが適用されている場合、内部の技術的制約により、パフォーマンスが低下します。 したがって、ルートレベルで保存されたフィールドのフィルター/並べ替えを使用することをお勧めします。 また、大きなページ分割された結果セットに対してクエリを実行する場合は、この方法をお勧めします。


## AEM 用の GraphQL - 拡張機能の概要 {#graphql-extensions}

AEM 用の GraphQL でのクエリの基本操作は、標準の GraphQL 仕様に従います。AEM での GraphQL クエリには、次のような拡張機能があります。

* 結果のリストを想定している場合：
   * モデル名に `List` を付け加えます（例：`cityList`）
   * [サンプルクエリ - すべての都市に関するすべての情報](/help/headless/graphql-api/sample-queries.md#sample-all-information-all-cities)を参照してください

   これにより、以下のことが可能になります。

   * [結果の並べ替え](#sorting)

      * `ASC` : 昇順
      * `DESC` : 降順
   * 次のいずれかを使用して、結果のページを返します。

      * [オフセットと制限を含むリストクエリ](#list-offset-limit)
      * [最初と次の後にページ分割されたクエリ](#paginated-first-after)
   * [サンプルクエリ - すべての都市に関するすべての情報](/help/headless/graphql-api/sample-queries.md#sample-all-information-all-cities)を参照してください



* 結果が 1 つだけ必要な場合：
   * モデル名（例：city）を使用します

* 結果のリストを想定している場合：
   * モデル名に `List` を付け加えます（例：`cityList`）
   * [サンプルクエリ - すべての都市に関するすべての情報](/help/headless/graphql-api/sample-queries.md#sample-all-information-all-cities)を参照してください

* 論理和（OR）を使用する場合：
   * ` _logOp: OR` を使用します
   * [サンプルクエリ - 「Jobs」または「Smith」という名前を持つすべての人物](/help/headless/graphql-api/sample-queries.md#sample-all-persons-jobs-smith)を参照してください

* 論理積（AND）も存在しますが、（多くの場合）暗黙的です

* コンテンツフラグメントモデル内のフィールドに対応するフィールド名に対してクエリを実行できます
   * [サンプルクエリ - ある会社の CEO と従業員の詳細](/help/headless/graphql-api/sample-queries.md#sample-full-details-company-ceos-employees)を参照してください

* モデルのフィールドに加えて、次のようなシステム生成フィールドがあります（フィールド名の先頭にアンダースコアが付きます）。

   * コンテンツの場合：

      * `_locale`：言語を表示します（言語マネージャーに基づく）
         * [特定ロケールの複数のコンテンツフラグメントのサンプルクエリ](/help/headless/graphql-api/sample-queries.md#sample-wknd-multiple-fragments-given-locale)を参照してください
      * `_metadata`：フラグメントのメタデータを表示します
         * [メタデータのサンプルクエリ - 「GB」という賞のメタデータのリスト](/help/headless/graphql-api/sample-queries.md#sample-metadata-awards-gb)を参照してください
      * `_model`：コンテンツフラグメントモデル（パスとタイトル）のクエリを許可します
         * [モデルからのコンテンツフラグメントモデルのサンプルクエリ](/help/headless/graphql-api/sample-queries.md#sample-wknd-content-fragment-model-from-model)を参照してください
      * `_path`：リポジトリ内のコンテンツフラグメントへのパス
         * [サンプルクエリ - 1 つの特定の都市フラグメント](/help/headless/graphql-api/sample-queries.md#sample-single-specific-city-fragment)を参照してください
      * `_reference`：参照（リッチテキストエディターでのインライン参照など）を表示します
         * [プリフェッチされた参照を含んだ複数のコンテンツフラグメントのサンプルクエリ](/help/headless/graphql-api/sample-queries.md#sample-wknd-multiple-fragments-prefetched-references)を参照してください
      * `_variation`：コンテンツフラグメント内の特定のバリエーションを表示します

         >[!NOTE]
         >
         >指定されたバリエーションがコンテンツフラグメントに対して存在しない場合、マスターバリエーションが（フォールバック）デフォルトとして返されます。

         * [サンプルクエリ - 名前付きバリエーションを持つすべての都市](#sample-cities-named-variation)を参照してください
   * 操作の場合：

      * `_operator`：特定の演算子（`EQUALS`、`EQUALS_NOT`、`GREATER_EQUAL`、`LOWER`、`CONTAINS`、`STARTS_WITH`）を適用します
         * [サンプルクエリ - 「Jobs」という名前を持たないすべての人物](/help/headless/graphql-api/sample-queries.md#sample-all-persons-not-jobs)を参照してください
         * [サンプルクエリ - `_path` が特定のプレフィックスで始まるすべてのアドベンチャーを参照してください](/help/headless/graphql-api/sample-queries.md#sample-wknd-all-adventures-cycling-path-filter)
      * `_apply`：特定の条件（例：`AT_LEAST_ONCE`）を適用します
         * [サンプルクエリ - 少なくとも 1 回は現れる項目を含んだ配列をフィルタリング](/help/headless/graphql-api/sample-queries.md#sample-array-item-occur-at-least-once)を参照してください
      * `_ignoreCase`：クエリの実行時に大文字と小文字を区別しません
         * [サンプルクエリ - 名前に SAN が含まれるすべての都市（大文字と小文字を区別しない場合）](/help/headless/graphql-api/sample-queries.md#sample-all-cities-san-ignore-case)を参照してください









* GraphQL のユニオン型がサポートされています

   * `... on` を使用します
      * [特定モデルのコンテンツフラグメントのうちコンテンツ参照を含んだものを取得するサンプルクエリ](/help/headless/graphql-api/sample-queries.md#sample-wknd-fragment-specific-model-content-reference)を参照してください

* ネストされたフラグメントに対するクエリ時のフォールバック：

   * 任意のバリエーションがネストされたフラグメントに存在しない場合、**マスター**&#x200B;バリエーションが返されます。

## 外部 web サイトからの GraphQL エンドポイントのクエリ {#query-graphql-endpoint-from-external-website}

外部 web サイトから GraphQL エンドポイントにアクセスするには、次の項目を設定する必要があります。

* [CORS フィルター](/help/headless/deployment/cross-origin-resource-sharing.md)
* [リファラーフィルター](/help/headless/deployment/referrer-filter.md)

## 認証 {#authentication}

[コンテンツフラグメントに対するリモート AEM GraphQL クエリの認証](/help/headless/security/authentication.md)を参照してください。

## FAQ {#faqs}

次のような質問が寄せられました。

1. **Q**：「*AEM 用 GraphQL API と Query Builder API の違いは何ですか？*」

   * **A**：「AEM GraphQL API *は JSON 出力の完全な制御が可能であり、コンテンツをクエリするための業界標準になっています。今後、AEM GraphQL API への投資が計画されています。*」

## チュートリアル - AEM ヘッドレスと GraphQL をはじめる前に {#tutorial}

実践的なチュートリアルを探している場合は、AEM の GraphQL API を使用し、外部アプリで使用するコンテンツをヘッドレス CMS シナリオで構築して公開する方法を示す「[AEM ヘッドレスと GraphQL をはじめる前に](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/graphql/overview.html?lang=ja)」のエンドツーエンドのチュートリアルをご覧ください。
