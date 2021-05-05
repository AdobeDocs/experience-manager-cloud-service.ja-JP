---
title: AEM配信APIを使用したコンテンツへのアクセス方法
description: AEMヘッドレス開発者ジャーニーのこの部分では、GraphQLクエリを使用してコンテンツフラグメントのコンテンツにアクセスする方法を説明します。
hide: true
hidefromtoc: true
index: false
exl-id: 5ef557ff-e299-4910-bf8c-81c5154ea03f
translation-type: tm+mt
source-git-commit: 7b04ae2bfa75fe3d3af13271efe567a5fc401f49
workflow-type: tm+mt
source-wordcount: '4636'
ht-degree: 55%

---

# AEM配信APIを使用したコンテンツへのアクセス方法{#access-your-content}

>[!CAUTION]
>
>作業中 — このドキュメントの作成は現在進行中で、完全なもの、最終的なもの、または実稼働目的で使用するものとして理解してはなりません。

[AEMヘッドレス開発者ジャーニーのこの部分では、](overview.md)GraphQLクエリを使用してコンテンツフラグメントのコンテンツにアクセスする方法を学ぶことができます。

## {#story-so-far}

以前のドキュメントのAEM headlessジャーニー[How to Model Your Content](model-your-content.md)では、AEMでデータモデリングの基本を学びました。コンテンツ構造のモデル化方法を理解し、AEMコンテンツフラグメントモデルとコンテンツフラグメントを使用してこの構造を実現する必要があります。

* [データモデリング](#data-modeling)に関連する概念と用語を認識します。
* [ヘッドレスコンテンツ配信](#data-modeling-for-aem-headless)にデータモデリングが必要な理由を理解します。
* AEMコンテンツフラグメントモデル](#create-structure-content-fragment-models)（および[コンテンツフラグメント](#use-content-to-author-content)を含むコンテンツの作成者）を使用して、[この構造を実現する方法を理解します。
* [コンテンツのモデル化方法](#getting-started-examples)を理解します。基本的なサンプルを持つ原則

この記事は、AEM GraphQL APIを使用してAEMの既存のヘッドレスコンテンツにアクセスする方法を理解するために、これらの基本事項に基づいて構築されています。

* **オーディエンス**:初心者
* **目的**:AEM GraphQLクエリを使用してコンテンツフラグメントのコンテンツにアクセスする方法を説明します。
   * GraphQLとAEM GraphQL APIの紹介。
   * AEM GraphQL APIの詳細を確認します。
   * 実際の動作を確認するには、サンプルクエリを参照してください。

## データにアクセスしたい？{#so-youd-like-to-access-your-data}

だから…（コンテンツフラグメント内に）このようなコンテンツがすべて整然と構成され、新しいアプリが提供されるのを待っています。 問題は、そこに到達する方法です。

必要なのは、特定のコンテンツをターゲットし、必要なものを選択してアプリに返し、さらに処理する方法です。

Adobe Experience Manager(AEM)をCloud Serviceとして使用すると、AEM GraphQL APIを使用して、コンテンツフラグメントに選択的にアクセスし、必要なコンテンツのみを返すことができます。 つまり、アプリケーションで使用する構造化コンテンツのヘッドレスな配信を実現できます。

>[!NOTE]
>
>AEM GraphQL APIは、標準のGraphQLに基づいてカスタマイズされた実装です。

## GraphQL — 入門{#graphql-introduction}

GraphQLは、次の機能を提供するオープンソース仕様です。

* 構造化オブジェクトから特定のコンテンツを選択できるクエリ言語。
* 構造化コンテンツでこれらのクエリを満たすランタイム。

GraphQLは&#x200B;*厳密に*&#x200B;型指定されたAPIです。 つまり、*すべての*&#x200B;コンテンツは、タイプ別に明確に構成、整理されていなければならないので、GraphQL *は、何にアクセスし、何にアクセスするかと、どのようにしてアクセスするかを理解している必要があります。*&#x200B;データフィールドはGraphQLスキーマ内で定義され、コンテンツオブジェクトの構造を定義します。

次に、GraphQLエンドポイントは、GraphQLクエリに応答するパスを提供します。

つまり、アプリをAEMで使用する場合に必要なデータだけを、正確かつ確実に、かつ効率的に選択できます。

>[!NOTE]
>
>*GraphQL*.orgおよび&#x200B;*GraphQL*.comを参照してください。

## AEMとGraphQL {#aem-graphql}

GraphQLはAEMのさまざまな場所で使用され、例：

* Commerce
   * AEMと様々なサードパーティのコマースソリューション間にはGraphQL統合が存在し、CIFコアコンポーネントが提供する拡張フックと共に使用されます。
* コンテンツフラグメント
   * この使用事例用にカスタマイズされたAPIが開発されています。
   * これはAEM GraphQL APIです。

>[!NOTE]
>
>ヘッドレスジャーニーのこの手順は、AEM GraphQL APIとコンテンツフラグメントに関するものです。

## AEM GraphQL API {#aem-graphql-api}

AEM GraphQL APIは、標準のGraphQL APIをカスタマイズしたバージョンで、コンテンツフラグメントに対して（複雑な）クエリを実行できるように特別に設定されています。

コンテンツフラグメントは、コンテンツがコンテンツフラグメントのモデルに従って構造化されているので使用されます。 これは、GraphQLの基本的な要件を満たします。

* コンテンツフラグメントモデルは、1つ以上のフィールドで構成されています。
   * 各フィールドはデータ型に従って定義されます。
* コンテンツフラグメントモデルは、対応するAEM GraphQLスキーマの生成に使用されます。

AEM用のGraphQL（およびコンテンツ）に実際にアクセスするには、エンドポイントを使用してアクセスパスを提供します。

AEM GraphQL APIを介して返されたコンテンツは、アプリケーションで使用できます。

>[!NOTE]
>
>AEM GraphQL API の実装は、GraphQL Java ライブラリに基づいています。

### オーサー環境とパブリッシュ環境の使用例 {#use-cases-author-publish-environments}

AEM GraphQL APIの使用例は、Cloud Service環境としてのAEMのタイプに応じて異なります。

* パブリッシュ環境の使用目的：
   * JS アプリケーションのデータのクエリ（標準の使用例）

* オーサー環境の使用目的：
   * 「コンテンツ管理用」のデータのクエリ：
      * AEM as a Cloud Service の GraphQL は現在読み取り専用の API です。
      * CR（U）D 操作には REST API を使用できます。

## AEM GraphQL API で使用するコンテンツフラグメント {#content-fragments-use-with-aem-graphql-api}

コンテンツフラグメントは、AEMスキーマやクエリのGraphQLの基盤として、次のように使用できます。

* ページに依存しないコンテンツをデザイン、作成、キュレーションおよび公開できます。
* これらはコンテンツフラグメントモデルに基づいています。コンテンツフラグメントモデルでは、定義されたデータ型を使用して、結果のフラグメントの構造を事前に定義します。
* 構造の追加のレイヤーは、フラグメント参照データ型を使用して作成できます。このデータ型は、モデルの定義時に使用できます。

### コンテンツフラグメントモデル {#content-fragments-models}

コンテンツフラグメントモデルは、

* **有効**&#x200B;にされると、スキーマの生成に使用されます。

* GraphQL に必要なデータタイプとフィールドを提供します。アプリケーションが、可能なことだけを要求して期待するものを受け取るようにします。

* データタイプ&#x200B;**フラグメント参照**&#x200B;は、別のコンテンツフラグメントを参照するためにモデル内で使用できるので、構造レベルを追加します。

### フラグメント参照 {#fragment-references}

**フラグメント参照**&#x200B;は、

* GraphQL との関連で特に興味深いものです。

* コンテンツフラグメントモデルの定義時に使用できる特定のデータタイプです。

* 特定のコンテンツフラグメントモデルに依存する別のフラグメントを参照します。

* 構造化データを取得できます。

   * **マルチフィード**&#x200B;として定義した場合、複数のサブフラグメントをプライムフラグメントで参照（取得）できます。

### JSON プレビュー {#json-preview}

コンテンツフラグメントモデルの設計と開発に役立つように、コンテンツフラグメントエディターでJSON出力をプレビューできます。

## コンテンツフラグメントからのGraphQLスキーマ生成{#graphql-schema-generation-content-fragments}

GraphQL は、厳密に型指定された API です。つまり、データは型別に明確に構造化され編成される必要があります。GraphQL の仕様には、特定のインスタンス上のデータをクエリするための堅牢な API を作成する方法に関する一連のガイドラインが用意されています。そのタスクをおこなうには、クライアントはスキーマを取得する必要があります。この中には、クエリに必要なすべての型が定義されています。

コンテンツフラグメントの場合、GraphQL スキーマ（構造とタイプ）は、**有効**&#x200B;なコンテンツフラグメントモデルとそれらのデータタイプに基づいています。

>[!CAUTION]
>
>（**有効**&#x200B;になっているコンテンツフラグメントモデルから派生した）すべての GraphQL スキーマは、GraphQL エンドポイントを通じて読み取り可能です。
>
>つまり、漏洩するおそれがあるので、機密データが使用可能になっていないことを確認する必要があります。例えば、これには、モデル定義のフィールド名として存在する可能性のある情報が含まれます。

例えば、ユーザーが `Article` という名前のコンテンツフラグメントモデルを作成した場合、AEMは `ArticleModel` 型のオブジェクト `article` を生成します。この型に含まれるフィールドは、モデルで定義されているフィールドとデータ型に対応しています。

1. コンテンツフラグメントモデル：

   ![GraphQL で使用するコンテンツフラグメントモデル](assets/graphqlapi-cfmodel.png "GraphQL で使用するコンテンツフラグメントモデル")

1. 対応するGraphQLスキーマ（GraphiQLの自動ドキュメントからの出力）:
   ![コンテンツフラグメントモデルに基づく GraphQL スキーマ](assets/graphqlapi-cfm-schema.png "コンテンツフラグメントモデルに基づく GraphQL スキーマ")

   この図では、生成された型 `ArticleModel` に複数の[フィールド](#fields)が含まれていることがわかります。

   * そのうちの 3 つ（`author`、`main`、`referencearticle`）は、ユーザーが管理しています。

   * その他のフィールド（この例では `_path`、`_metadata`、`_variations`）は AEM によって自動的に追加されたもので、特定のコンテンツフラグメントに関する情報を提供する便利な手段となっています。これらの[ヘルパーフィールド](#helper-fields)は、ユーザーが定義したものと自動生成されたものを区別するために、前に`_`が付いています。

1. ユーザーが Article モデルに基づいてコンテンツフラグメントを作成すると、GraphQL を使用してそれをクエリできます。例については、Sampleクエリ.md#graphql-sample-クエリを参照してください（GraphQLで使用するサンプルコンテンツフラグメント構造に基づきます）。

AEM 用 GraphQL では、スキーマには柔軟性があります。つまり、コンテンツフラグメントモデルを作成、更新、削除するたびに、スキーマが自動生成されます。また、コンテンツフラグメントモデルを更新すると、データスキーマキャッシュも更新されます。

Sites GraphQL サービスは、コンテンツフラグメントモデルに対する変更を（バックグラウンドで）リッスンします。更新が検出されると、スキーマのその部分だけが再生成されます。この最適化により、時間を節約し、安定性を確保できます。

例えば、次のようになります。

1. `Content-Fragment-Model-1` と `Content-Fragment-Model-2` を含んだパッケージをインストールすると、

   1. `Model-1` と `Model-2` の GraphQL 型が生成されます。

1. 次に `Content-Fragment-Model-2` を変更すると、

   1. `Model-2` GraphQL 型だけが更新されます。

   1. 一方、`Model-1` は同じままです。

>[!NOTE]
>
>REST API を使用してコンテンツフラグメントモデルの一括更新をおこなう場合などには、この点に留意することが大切です。

スキーマは、GraphQL クエリと同じエンドポイントを通じて提供され、クライアントはスキーマが拡張子 `GQLschema` で呼び出されることに対処します。例えば、`/content/cq:graphql/global/endpoint.GQLschema` で単純な `GET` リクエストを実行すると、`text/x-graphql-schema;charset=iso-8859-1` の Content-type を持つスキーマが出力されます。

### スキーマの生成 — 未公開モデル{#schema-generation-unpublished-models}

コンテンツフラグメントがネストされている場合、親のコンテンツフラグメントモデルは発行されるが、参照されているモデルは発行されない可能性があります。

>[!NOTE]
>
>AEM UIはこのような状況を防ぎますが、プログラムやコンテンツパッケージを使用して公開する場合は、この状況が発生する可能性があります。

この場合、AEMは親コンテンツフラグメントモデルに対して&#x200B;*不完全な*&#x200B;スキーマを生成します。 これは、未公開のモデルに依存するフラグメント参照がスキーマから削除されることを意味します。

## AEM GraphQLエンドポイント{#aem-graphql-endpoints}

<!--
need details/examples
-->

エンドポイントは、AEM用のGraphQLへのアクセスに使用するパスです。 このパスを使用すると、以下が可能になります。

* GraphQLスキーマへのアクセス、
* GraphQL クエリの送信
* （GraphQL クエリに対する）応答の受信

AEMでは次のことが可能です。

* グローバルエンドポイント — すべてのサイトで使用できます。
* テナントエンドポイント — 指定したサイト/プロジェクトに固有の、設定可能なエンドポイント。

## 権限 {#permissions}

Assets へのアクセスに必要な権限です。

## AEM GraphicQL Interface {#aem-graphiql-interface}

クエリを直接入力し、テストする際に役立つように、標準のGraphiQLインターフェイスをAEM GraphQLで使用できます。 これは AEM と共にインストールできます。

構文の強調表示、オートコンプリート、オートコンプリートなどの機能と、履歴およびオンラインドキュメントが提供されます。

![GraphiQL インターフェイス](assets/graphiql-interface.png "GraphiQL インターフェイス")

<!--
new page?
-->

## AEM GraphQL APIの使用{#using-aem-graphiql}

### エンドポイント{#endpoints}

AEMグローバルエンドポイント用のGraphQLのリポジトリパスは、次のとおりです。

`/content/cq:graphql/global/endpoint`

アプリがリクエストURLで次のパスを使用できるようにします。

`/content/_cq_graphql/global/endpoint.json`

テナントエンドポイントのパスは次のとおり比較可能です。

`/content/cq:graphql/your-tenant/endpoint`
`/content/_cq_graphql/your-tenant/endpoint.json`

使用する前に、すべてのエンドポイントを有効にする必要があります。 AEM用のGraphQLでエンドポイント、グローバルまたはテナントを有効にするには、次の操作が必要です。

* GraphQL エンドポイントの有効化
* エンドポイントの公開

>[!CAUTION]
>
>コンテンツフラグメントエディターでは、あるテナントのコンテンツフラグメントが別のテナントのコンテンツフラグメントを（ポリシーを介して）参照できるようにします。
>
>この場合、テナント固有のエンドポイントを使用してすべてのコンテンツを取得できるわけではありません。
>
>コンテンツ作成者は、このシナリオを制御する必要があります。例えば、共有コンテンツフラグメントモデルをグローバルテナントの下に配置することを検討すると便利です。

### GraphQL エンドポイントの有効化 {#enabling-graphql-endpoint}

GraphQLエンドポイントを有効にするには、まず設定ブラウザで適切な設定を行う必要があります。

>[!CAUTION]
>
>コンテンツフラグメントモデルの使用が有効になっていない場合、「**作成**」オプションは使用できません。

対応するエンドポイントを有効にするには：

1. **ツール**、**サイト**&#x200B;に移動し、**GraphQL**&#x200B;を選択します。
1. 「**作成**」を選択します。
1. 「**新しいGraphQLエンドポイントを作成**」ダイアログが開きます。 ここで指定できる内容は次のとおりです。
   * **名前**:エンドポイントの名前；任意のテキストを入力できます。
   * **GraphQLスキーマを使用します。提供元**:ドロップダウンを使用して、必要なサイト/プロジェクトを選択します。

   >[!NOTE]
   >
   >ダイアログに次の警告が表示されます。
   >
   >* *慎重に管理しない場合、GraphQL エンドポイントによりデータのセキュリティとパフォーマンスで問題が発生する可能性があります。エンドポイントを作成した後で、適切な権限を設定するようにしてください。*


1. **作成**&#x200B;で確認します。
1. **次の手順**&#x200B;ダイアログには、セキュリティコンソールへの直接リンクが表示され、新しく作成したエンドポイントに適切な権限を持たせることができます。

   >[!CAUTION]
   >
   >エンドポイントは、すべてのユーザーがアクセスできます。そのため、GraphQL クエリがサーバーに大きな負荷をかける可能性があるので、特にパブリッシュインスタンスでは、セキュリティ上の問題が発生するおそれがあります。
   >
   >使用例に適した ACL をエンドポイントに設定できます。

### GraphQLエンドポイントの公開{#publishing-graphql-endpoint}

新しいエンドポイントを選択し、「**発行**」を選択して、すべての環境で完全に使用可能にします。

>[!CAUTION]
>
>エンドポイントは、すべてのユーザーがアクセスできます。
>
>パブリッシュインスタンスでは、GraphQLクエリがサーバに大きな負荷をかける可能性があるので、セキュリティ上の問題が生じる可能性があります。
>
>エンドポイントの使用事例に適したACLを設定する必要があります。

### AEM GraphiQL インターフェイスのインストール {#installing-graphiql-interface}

GraphiQLユーザーインターフェイスは、専用のパッケージを使用してAEMにインストールできます。[GraphiQL Content Package v0.0.6 (2021.3)](https://experience.adobe.com/#/downloads/content/software-distribution/en/aemcloud.html?package=/content/software-distribution/en/details.html/content/dam/aemcloud/public/aem-graphql/graphiql-0.0.6.zip)パッケージ。

### AEM GraphQLスキーマ{#aem-graphql-schemas}

データにアクセスするには、まず必要なコンテンツフラグメントモデルのタイプ(GraphQLスキーマで表される)を選択する必要があります。 AEM GraphQLスキーマは、コンテンツフラグメントモデルから派生します。GraphQLクエリで使用します。

<!--
Confirm is the schema city or CityModel? -->

`City`という名前のコンテンツフラグメントモデルがある場合は、`city`という名前の対応するスキーマが存在します。 次のクエリを使用して、このモデルに基づくすべてのコンテンツフラグメントの`name`をリストできます。

```xml
query {
  cityList {
    items {
      name
    }
  }
}
```

次のクエリを使用して、すべての`types`の`name`と`description`をリストし、利用可能なすべてのスキーマに対してできます。

```xml
{
  __schema {
    types {
      name
      description
    }
  }
}
```

### AEM GraphQLフィールド{#aem-graphql-fields}

必要なスキーマを選択すると、スキーマ内のフィールドに表示される特定のデータにアクセスできます。

スキーマ内には、次の 2 つの基本的なカテゴリに属する個々のフィールドがあります。

* ユーザーが生成するフィールド

   選択された[フィールドタイプ](#field-types)を使用して、コンテンツフラグメントモデルの設定方法に基づいてフィールドが作成されます。フィールド名は、**データタイプ**&#x200B;の「**プロパティ名**」フィールドから取得されます。

   * また、**レンダリング時の名前**&#x200B;プロパティも考慮する必要があります。ユーザーが特定のデータ型を、例えば、1 行のテキストか複数フィールドのどちらかとして設定できるからです。

* AEM 用 GraphQL が生成する多数のヘルパーフィールド

   これらは、コンテンツフラグメントを識別するためや、コンテンツフラグメントに関する詳細を取得するために使用されます。

### フィールドタイプ {#field-types}

AEM 用 GraphQL では一連のタイプをサポートしています。サポートされているすべてのコンテンツフラグメントモデルデータ型と、それに対応する GraphQL 型を以下の表に示します。

| コンテンツフラグメントモデル - データ型 | GraphQL の型 | 説明 |
|--- |--- |--- |
| 1行テキスト | String、[String] | 作成者名、場所名などの単純な文字列に使用します. |
| 複数行テキスト | String | 記事の本文などのテキストを出力するために使用します。 |
| 数値 | Float、[Float] | 浮動小数点数と整数を表示するために使用します |
| ブール型 | ブール型 | チェックボックスを表示するために使用します（単純な真／偽のステートメント） |
| 日時 | Calendar | 日時を ISO 8086 形式で表示するために使用します. 選択したタイプに応じて、AEM GraphQLで使用できる3つのフレーバーがあります。`onlyDate`、`onlyTime`、`dateTime` |
| 列挙 | 文字列 | モデルの作成時に定義されたオプションのリストに含まれるオプションを表示するために使用します |
| タグ | [String] | AEM で使用されているタグを表す文字列のリストを表示するために使用します |
| コンテンツ参照 | 文字列 | AEM 内の別のアセットへのパスを表示するために使用します |
| フラグメント参照 | *モデルタイプ* | 特定のモデルタイプの別のコンテンツフラグメントを参照するために使用します（モデルの作成時に定義されます） |

### ヘルパーフィールド {#helper-fields}

ユーザー生成フィールドのデータ型に加えて、AEM 用 GraphQL では、コンテンツフラグメントの識別やコンテンツフラグメントに関する追加情報の提供に役立つ多数の&#x200B;*ヘルパー*&#x200B;フィールドも生成されます。

#### パス {#path}

パスフィールドは、GraphQL で識別子として使用されます。これは、AEM リポジトリー内のコンテンツフラグメントアセットのパスを表します。これをコンテンツフラグメントの識別子として選択した理由は次のとおりです。

* AEM 内で一意である
* 取得しやすい

次のコードでは、コンテンツフラグメントモデル `Person` に基づいて作成されたすべてのコンテンツフラグメントのパスを表示します。

```xml
{
  personList {
    items {
      _path
    }
  }
}
```

特定のタイプのコンテンツフラグメントを 1 つ取得するには、まずそのパスも決定する必要があります。次に例を示します。

```xml
{
  personByPath(_path: "/content/dam/path/to/fragment/john-doe") {
    item {
      _path
      firstName
      name
    }
  }
}
```

>[!NOTE]
>
>サンプルクエリ - 1 つの特定の都市フラグメントを参照してください。

#### メタデータ {#metadata}

また、AEM では GraphQL を通じて、コンテンツフラグメントのメタデータも公開します。メタデータは、コンテンツフラグメントのタイトル、サムネールパス、コンテンツフラグメントの説明、作成日など、コンテンツフラグメントを説明する情報です。

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

```xml
{
  personByPath(_path: "/content/dam/path/to/fragment/john-doe") {
    item {
      _path
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
>`StringMetadata` と `StringArrayMetadata` はどちらも、リポジトリーに格納されているものについての指定であり、その取得手段についての指定ではありません。
>
>例えば、`stringMetadata` フィールドを呼び出すと、リポジトリーに `String` として格納されているすべてのメタデータの配列を受け取ることになります。一方、`stringArrayMetadata` を呼び出すと、リポジトリーに `String[]` として格納されているすべてのメタデータの配列を受け取ります。

>[!NOTE]
>
>メタデータのサンプルクエリ - 「GB」という賞のメタデータのリストを参照してください.

#### バリエーション {#variations}

コンテンツフラグメントのバリエーションに対するクエリを簡略化するために、`_variations` フィールドが実装されています。次に例を示します。

```xml
{
  personByPath(_path: "/content/dam/path/to/fragment/john-doe") {
    item {
      _variations
    }
  }
}
```

>[!NOTE]
>
>サンプルクエリ - 名前付きバリエーションを持つすべての都市を参照してください.

### AEM GraphQL変数{#aem-graphql-variables}

変数は、異なる値を1か所に格納できるように、任意の形式のプログラミングやクエリで役立ちます。 AEM GraphQLの場合、値ごとに個別のクエリを書き込む代わりに1つの変数に対してクエリを書き込むことができ、この変数の値は必要に応じて変化する可能性があります。

GraphQL では、クエリに変数を含めることができます。

>[!NOTE]
>
>詳しくは、変数のGraphQLドキュメントを参照してください。

例えば、特定のバリエーションを持つ `Article` タイプのコンテンツフラグメントをすべて取得するには、次のように、GraphiQL で変数 `variation` を指定します。すべてのインスタンスが`GetArticlesByVariation`で取得され、`articleList`で使用するために渡されます。

![GraphQL 変数](assets/graphqlapi-variables.png "GraphQL 変数")

```xml
### query
query GetArticlesByVariation($variation: String!) {
    articleList(variation: $variation) {
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

### AEM GraphQLディレクティブ{#aem-graphql-directives}

GraphQL では、GraphQL ディレクティブ と呼ばれる変数に基づいてクエリを変更する可能性があります。

例えば、変数 `includePrice` に基づいて、すべての `AdventureModels` のクエリに `adventurePrice` フィールドを含めることができます。

!![GraphQL Directives](assets/graphqlapi-directives .png &quot;GraphQL Directives&quot;)

```xml
### query
query GetAdventureByType($includePrice: Boolean!) {
  adventureList {
    items {
      adventureTitle
      adventurePrice @include(if: $includePrice)
    }
  }
}
 
### in query variables
{
    "includePrice": true
}
```

### AEM GraphQLフィルター{#aem-graphql-filters}

GraphQL クエリでフィルタリングを使用して、特定のデータを返すこともできます。

フィルタリングでは、論理演算子と論理式に基づいた構文を使用します。

例えば、次の（基本的な）クエリでは、`Jobs` または `Smith` という名前を持つすべての人を抜き出します。

```xml
query {
  personList(filter: {
    name: {
      _logOp: OR
      _expressions: [
        {
          value: "Jobs"
        },
        {
          value: "Smith"
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

その他の例については、以下を参照してください。

* AEM 用 GraphQL の拡張機能の詳細

* このサンプルコンテンツおよび構造を使用したサンプルクエリ

### AEM GraphQL拡張機能{#aem-graphql-extensions}

AEM 用の GraphQL でのクエリの基本操作は、標準の GraphQL 仕様に従います。AEM での GraphQL クエリには、次のような拡張機能があります。

* 結果が 1 つだけ必要な場合：
   * モデル名（例：city）を使用します

* 結果のリストを想定している場合：
   * モデル名に `List` を付け加えます（例：`cityList`）
   * [サンプルクエリ - すべての都市に関するすべての情報](#sample-all-information-all-cities)を参照してください

* 論理和（OR）を使用する場合：
   * ` _logOp: OR` を使用します
   * [サンプルクエリ - 「Jobs」または「Smith」という名前を持つすべての人物](#sample-all-persons-jobs-smith)を参照してください

* 論理積（AND）も存在しますが、（多くの場合）暗黙的です

* コンテンツフラグメントモデル内のフィールドに対応するフィールド名に対してクエリを実行できます
   * [サンプルクエリ - ある会社の CEO と従業員の詳細](#sample-full-details-company-ceos-employees)を参照してください

* モデルのフィールドに加えて、システム生成フィールドがいくつかあります（前にアンダースコアが付いています）。

   * コンテンツの場合：

      * `_locale`：言語を表示します（言語マネージャーに基づく）
         * [特定ロケールの複数のコンテンツフラグメントのサンプルクエリ](#sample-wknd-multiple-fragments-given-locale)を参照してください
      * `_metadata`：フラグメントのメタデータを表示します
         * [メタデータのサンプルクエリ - 「GB」という賞のメタデータのリスト](#sample-metadata-awards-gb)を参照してください
      * `_model`：コンテンツフラグメントモデル（パスとタイトル）のクエリを許可します
         * [モデルからのコンテンツフラグメントモデルのサンプルクエリ](#sample-wknd-content-fragment-model-from-model)を参照してください
      * `_path` :リポジトリ内のコンテンツフラグメントへのパス
         * [サンプルクエリ - 1 つの特定の都市フラグメント](#sample-single-specific-city-fragment)を参照してください
      * `_reference`：参照（リッチテキストエディターでのインライン参照など）を表示します
         * [プリフェッチされた参照を含んだ複数のコンテンツフラグメントのサンプルクエリ](#sample-wknd-multiple-fragments-prefetched-references)を参照してください
      * `_variation`：コンテンツフラグメント内の特定のバリエーションを表示します
         * [サンプルクエリ - 名前付きバリエーションを持つすべての都市](#sample-cities-named-variation)を参照してください
   * 操作の場合：

      * `_operator`：特定の演算子（`EQUALS`、`EQUALS_NOT`、`GREATER_EQUAL`、`LOWER`、`CONTAINS`）を適用します, `STARTS_WITH`
         * [サンプルクエリ - 「Jobs」という名前を持たないすべての人物](#sample-all-persons-not-jobs)を参照してください
         * [サンプルクエリ — 特定のプレフィックス](#sample-wknd-all-adventures-cycling-path-filter)を持つ`_path`開始が出現するすべての冒険を参照
      * `_apply`：特定の条件（例：`AT_LEAST_ONCE`）を適用します
         * [サンプルクエリ - 少なくとも 1 回は現れる項目を含んだ配列をフィルタリング](#sample-array-item-occur-at-least-once)を参照してください
      * `_ignoreCase`：クエリの実行時に大文字と小文字を区別しません
         * [サンプルクエリ - 名前に SAN が含まれるすべての都市（大文字と小文字を区別しない場合）](#sample-all-cities-san-ignore-case)を参照してください









* GraphQL のユニオン型がサポートされています

   * `... on` を使用します
      * [特定モデルのコンテンツフラグメントのうちコンテンツ参照を含んだものを取得するサンプルクエリ](#sample-wknd-fragment-specific-model-content-reference)を参照してください

### 永続的クエリ（キャッシュ） {#persisted-queries-caching}

POST リクエストを使用してクエリを準備した後、HTTP キャッシュまたは CDN でキャッシュできる GET リクエストを使用して、そのクエリを実行できます。

このようにする必要があるのは、POST クエリが通常はキャッシュされないからです。クエリをパラメーターとして GET を使用する場合、HTTP サービスや中間ステップにとってパラメーターが大きくなりすぎるという重大なリスクがあります。

持続的なクエリは、常に適切な（テナント）設定に関連するエンドポイントを使用する必要があります。そのため、どちらかまたは両方を使用できます。

* グローバル設定とエンドポイント
クエリは、すべてのコンテンツフラグメントモデルにアクセスできます。
* 特定のテナント構成とエンドポイント
特定のテナント構成に対して永続化されたクエリを作成するには、対応するテナント固有のエンドポイントが必要です（関連するコンテンツフラグメントモデルへのアクセスを提供するため）。
例えば、WKNDテナント専用の永続的なクエリを作成するには、対応するWKND固有のテナント構成と、WKND固有のエンドポイントを事前に作成する必要があります。

>[!NOTE]
>
>詳しくは、設定ブラウザーでのコンテンツフラグメント機能の有効化を参照してください。
>
>適切なテナント構成に対して、**GraphQL Persistenceクエリ**&#x200B;を有効にする必要があります。

例えば、`my-query`という名前の特定のクエリがあり、テナント構成`my-conf`のモデル`my-model`を使用する場合は、次のようになります。

* `my-conf`個別のエンドポイントを使用してクエリを作成すると、クエリは次のように保存されます。
   `/conf/my-conf/settings/graphql/persistentQueries/my-query`
* `global`エンドポイントを使用して同じクエリを作成できますが、クエリは次のように保存されます。
   `/conf/global/settings/graphql/persistentQueries/my-query`

>[!NOTE]
>
>これら2つは異なるクエリで、異なるパスで保存されます。
>
>同じモデルが使用されるだけで、異なる端点を介して使用されます。

特定のクエリを永続化するために必要な手順は次のとおりです。

1. 新しいエンドポイント URL `/graphql/persist.json/<config>/<persisted-label>` に PUT してクエリを準備します。

   例えば、次のようにして、永続的クエリを作成します。

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

1. この段階で、応答を確認します。

   例えば、以下が成功するかどうかを確認します。

   ```xml
   {
     "action": "create",
     "configurationName": "wknd",
     "name": "plain-article-query",
     "shortPath": "/wknd/plain-article-query",
     "path": "/conf/wknd/settings/graphql/persistentQueries/plain-article-query"
   }
   ```

1. その後、URL `/graphql/execute.json/<shortPath>` を GET して、永続的クエリを再生できます。

   例えば、次のような永続的クエリを使用します。

   ```xml
   $ curl -X GET \
       http://localhost:4502/graphql/execute.json/wknd/plain-article-query
   ```

1. 既存のクエリパスに POST して、永続的クエリを更新します。

   例えば、次のような永続的クエリを使用します。

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

1. キャッシュコントロール付きのラップされたプレーンクエリを作成します。

   次に例を示します。

   ```xml
   $ curl -X PUT \
       -H 'authorization: Basic YWRtaW46YWRtaW4=' \
       -H "Content-Type: application/json" \
       "http://localhost:4502/graphql/persist.json/wknd/plain-article-query-max-age" \
       -d \
   '{ "query": "{articleList { items { _path author main { json } referencearticle { _path } } } }", "cache-control": { "max-age": 300 }}'
   ```

1. パラメーター付きの永続的クエリを作成します。

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

1. パラメーター付きのクエリを実行します。

   次に例を示します。

   ```xml
   $ curl -X POST \
       -H 'authorization: Basic YWRtaW46YWRtaW4=' \
       -H "Content-Type: application/json" \
       "http://localhost:4502/graphql/execute.json/wknd/plain-article-query-parameters;apath=%2fcontent2fdam2fwknd2fen2fmagazine2falaska-adventure2falaskan-adventures;withReference=false"
   
   $ curl -X GET \
       "http://localhost:4502/graphql/execute.json/wknd/plain-article-query-parameters;apath=%2fcontent2fdam2fwknd2fen2fmagazine2falaska-adventure2falaskan-adventures;withReference=false"
   ```

1. パブリッシュでクエリを実行するには、関連する永続的ツリーをレプリケートする必要があります。

   * レプリケーションに POST を使用する場合：

      ```xml
      $curl -X POST   http://localhost:4502/bin/replicate.json \
        -H 'authorization: Basic YWRtaW46YWRtaW4=' \
        -F path=/conf/wknd/settings/graphql/persistentQueries/plain-article-query \
        -F cmd=activate
      ```

   * パッケージを使用する場合：
      1. 新しいパッケージ定義を作成します。
      1. 設定（例：`/conf/wknd/settings/graphql/persistentQueries`）を含めます。
      1. パッケージをビルドします。
      1. パッケージをレプリケートします。
   * レプリケーション／配布ツールを使用する場合：
      1. 配布ツールに移動します。
      1. 設定のツリーアクティベーション（例：`/conf/wknd/settings/graphql/persistentQueries`）を選択します。
   * （ワークフローランチャーの設定を通じて）ワークフローを使用する場合：
      1. 様々なイベント（例：作成、変更など）で設定をレプリケートするワークフローモデルを実行するためのワークフローランチャールールを定義します。



1. クエリの設定がいったん公開されると、パブリッシュエンドポイントを使用するだけで、同じ原則が適用されます。

   >[!NOTE]
   >
   >匿名アクセスの場合は、ACL で「全員」にクエリ設定へのアクセスが許可されているとシステムが想定します。
   >
   >そうでない場合は、実行できなくなります。

   >[!NOTE]
   >
   >URL 内のセミコロン（「;」）はすべてエンコードする必要があります。
   >
   >例えば、永続的クエリを実行するリクエストの場合と同様に、次のようにします。
   >
   >
   ```xml
   >curl -X GET \ "http://localhost:4502/graphql/execute.json/wknd/plain-article-query-parameters%3bapath=%2fcontent2fdam2fwknd2fen2fmagazine2falaska-adventure2falaskan-adventures;withReference=false"
   >```

### 外部 Web サイトからの GraphQL エンドポイントのクエリ {#query-graphql-endpoint-from-external-website}

外部WebサイトからGraphQLエンドポイントにアクセスするには、次の項目を設定する必要があります。

* CORSフィルター
* 転送者フィルタ

#### CORSフィルタ{#cors-filter}

>[!NOTE]
>
>AEM での CORS リソース共有ポリシーについて詳しくは、クロスオリジンリソース共有（CORS）についてを参照してください。

GraphQLエンドポイントにアクセスするには、お客様のGitリポジトリでCORSポリシーを設定する必要があります。 これは、目的のエンドポイントに適切なOSGi CORS設定ファイルを追加することで行います。

この設定では、アクセスを許可する必要がある信頼できるWebサイト接触チャネル`alloworigin`または`alloworiginregexp`を指定する必要があります。

例えば、`https://my.domain`のGraphQLエンドポイントと持続クエリエンドポイントへのアクセスを許可するには、次を使用します。

```xml
{
  "supportscredentials":true,
  "supportedmethods":[
    "GET",
    "HEAD",
    "POST"
  ],
  "exposedheaders":[
    ""
  ],
  "alloworigin":[
    "https://my.domain"
  ],
  "maxage:Integer":1800,
  "alloworiginregexp":[
    ""
  ],
  "supportedheaders":[
    "Origin",
    "Accept",
    "X-Requested-With",
    "Content-Type",
    "Access-Control-Request-Method",
    "Access-Control-Request-Headers"
  ],
  "allowedpaths":[
    "/content/_cq_graphql/global/endpoint.json",
    "/graphql/execute.json/.*"
  ]
}
```

エンドポイントのバニティパスを設定した場合は、`allowedpaths`でも使用できます。

#### 転送者フィルタ{#referrer-filter}

CORSの設定に加えて、サードパーティのホストからのアクセスを許可する転送者フィルターを設定する必要があります。

これは、次の適切なOSGi転送者フィルタ設定ファイルを追加することで行います。

* 信頼できるwebサイトのホスト名を指定します。`allow.hosts`または`allow.hosts.regexp`、
* このホスト名に対するアクセスを許可します。

例えば、転送者`my.domain`を使用してリクエストへのアクセスを許可するには、次の操作を行います。

```xml
{
    "allow.empty":false,
    "allow.hosts":[
      "my.domain"
    ],
    "allow.hosts.regexp":[
      ""
    ],
    "filter.methods":[
      "POST",
      "PUT",
      "DELETE",
      "COPY",
      "MOVE"
    ],
    "exclude.agents.regexp":[
      ""
    ]
}
```

>[!CAUTION]
>
>以下は顧客の責任でおこなう必要があります。
>
>* 信頼できるドメインにのみアクセスを許可する
>* 機密情報が公開されていないことを確認する
>* ワイルドカードの [*] 構文を使用しない。これを使用すると、GraphQL エンドポイントへの認証済みアクセスが無効になり、エンドポイントが世界中に公開されることになります。


>[!CAUTION]
>
>（**有効**&#x200B;になっているコンテンツフラグメントモデルから派生した）すべての GraphQL スキーマは、GraphQL エンドポイントを通じて読み取り可能です。
>
>つまり、漏洩するおそれがあるので、機密データが使用可能になっていないことを確認する必要があります。例えば、これには、モデル定義のフィールド名として存在する可能性のある情報が含まれます。

### AEM GraphQL認証{#aem-graphql-authentication}

Cloud Service(AEM) GraphQL API for Content Fragment配信としてのAdobe Experience Managerで主に使用されるのは、サードパーティのアプリケーションまたはサービスからリモートクエリを受け入れる場合です。 これらのリモートクエリは、ヘッドレスコンテンツの配信を保護するために、認証済みのAPIアクセスが必要になる場合があります。

>[!NOTE]
>
>テストおよび開発の場合は、GraphiQL インターフェイスを使用して AEM GraphQL API に直接アクセスすることもできます。

認証のために、サードパーティのサービスはアクセストークンを使用する必要があります。その後、このトークンは GraphQL リクエストで使用できます。

#### アクセストークンの取得 {#retrieving-access-token}

詳しくは、サーバー側 API のアクセストークンの生成を参照してください。

#### GraphQL リクエストでのアクセストークンの使用 {#use-access-token-in-graphql-request}

サードパーティのサービスが AEM インスタンスに接続するには、*アクセストークン*&#x200B;が必要です。サービスは次に、このトークンを POST リクエストの `Authorization` ヘッダーに追加する必要があります。

例えば、GraphQL の Authorization ヘッダーは次のようになります。

```xml
Authorization: Bearer <access_token>
```

#### 権限の要件 {#permission-requirements}

アクセストークンを使用しておこなわれるすべてのリクエストは、実際には、*そのトークンを生成したユーザーアカウントによって*&#x200B;おこなわれます。

つまり、GraphQL クエリの実行に必要な権限がアカウントにあることを確認する必要があります。

この確認は、ローカルインスタンスで GraphiQL を使用しておこなえます。

## AEM GraphQLクエリの例{#samples-aem-graphql-queries}

様々なサンプルクエリについては、「AEMでのGraphQLの使用方法 — サンプルコンテンツとクエリ」を参照してください。

<!--
## Code Samples for AEM GraphQL Queries {#code-samples-aem-graphql-queries}
-->

## 次の作業{#whats-next}

AEM GraphQL APIを使用してヘッドレスコンテンツにアクセスし、クエリする方法を学んだので、[REST APIを使用してコンテンツフラグメントのコンテンツにアクセスし、更新する方法を学ぶことができます。](/help/implementing/developing/headless-journey/update-your-content.md)

## その他のリソース {#additional-resources}

* [GraphQL.org](https://graphql.org)
   * [スキーマ](https://graphql.org/learn/schema/)
   * [変数](https://graphql.org/learn/queries/#variables)
   * [GraphQL Javaライブラリ](https://graphql.org/code/#java)
* [GraphiQL](https://graphql.org/learn/serving-over-http/#graphiql)
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
* [AEM Headless](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/graphql/overview.html?lang=ja)  — はじめに — データモデリングやGraphQLなどのAEM headless機能の使い方を簡単に説明する短いビデオチュートリアルシリーズです。
