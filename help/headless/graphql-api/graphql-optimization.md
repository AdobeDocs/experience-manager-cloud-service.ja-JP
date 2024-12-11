---
title: GraphQL クエリの最適化
description: ヘッドレスコンテンツ配信用の Adobe Experience Manager as a Cloud Service でコンテンツフラグメントをフィルタリング、ページング、並べ替える際に、GraphQL クエリを最適化する方法について説明します。
exl-id: 67aec373-4e1c-4afb-9c3f-a70e463118de
feature: Headless, Content Fragments,GraphQL API
role: Admin, Developer
source-git-commit: e8f992df5a270e7335af466a524daa013bff5f42
workflow-type: tm+mt
source-wordcount: '1824'
ht-degree: 100%

---

# GraphQLクエリの最適化 {#optimizing-graphql-queries}

>[!NOTE]
>
>これらの最適化のレコメンデーションを適用する前に、最高のパフォーマンスを実現するには、[GraphQL フィルタリングでのページングと並べ替えの際にコンテンツフラグメントを更新](/help/headless/graphql-api/graphql-optimized-filtering-content-update.md)することを検討してください。

これらのガイドラインは、GraphQL クエリでのパフォーマンスの問題を防ぐために提供されています。

## GraphQL のチェックリスト {#graphql-checklist}

次のチェックリストは、Adobe Experience Manager (AEM) as a Cloud Service での GraphQL の設定と使用を最適化するのに役立ちます。

### 第 1 原則 {#first-principles}

#### 永続的な GraphQL クエリを使用 {#use-persisted-graphql-queries}

**レコメンデーション**

永続的な GraphQL クエリの使用を強くお勧めします。

永続的な GraphQL クエリは、コンテンツ配信ネットワーク（CDN）を利用することで、クエリの実行パフォーマンスを低減するのに役立ちます。クライアントアプリケーションは、高速なエッジ対応の実行を実現するために、GET リクエストを使用して永続クエリをリクエストします。

**その他の参照**

以下を参照してください。

* [永続的な GraphQL クエリ](/help/headless/graphql-api/persisted-queries.md)。
* [AEM での GraphQL の使用方法 - サンプルコンテンツとサンプルクエリ](/help/headless/graphql-api/sample-queries.md)

### キャッシュ方法 {#cache-strategy}

キャッシュの様々な方法の最適化に使用することもできます。

#### AEM Dispatcher のキャッシュを有効化する {#enable-aem-dispatcher-caching}

**レコメンデーション**

[AEM Dispatcher](/help/implementing/dispatcher/overview.md) は、CDN キャッシュの前の AEM サービス内の第 1 レベルのキャッシュです。

**その他の参照**

以下を参照してください。

* [GraphQL の永続クエリ - Dispatcher でのキャッシュの有効化](/help/headless/deployment/dispatcher-caching.md)

#### コンテンツ配信ネットワーク（CDN）の使用 {#use-cdn}

**レコメンデーション**

GraphQL クエリとその JSON 応答は、CDN を使用する場合、`GET` リクエストとしてターゲットを設定すればキャッシュできます。これに対し、キャッシュされていないリクエストは、（リソースが）非常に高コストで処理に時間がかかる場合があり、元のリソースにさらに悪影響を及ぼす可能性があります。

**その他の参照**

以下を参照してください。

* [AEM as a Cloud Service での CDN](/help/implementing/dispatcher/cdn.md)

#### HTTP キャッシュ制御ヘッダーを設定する {#set-http-cache-control-headers}

**レコメンデーション**

永続的な GraphQL クエリを CDN で使用する場合は、適切な HTTP キャッシュ制御ヘッダーを設定することをお勧めします。

永続化された各クエリには、独自のキャッシュ制御ヘッダーのセットを設定できます。ヘッダーは、[GraphQL API](/help/headless/graphql-api/content-fragments.md) または [AEM GraphiQL IDE](/help/headless/graphql-api/graphiql-ide.md) で設定できます。

**その他の参照**

以下を参照してください。

* [永続クエリのキャッシュ](/help/headless/graphql-api/persisted-queries.md#caching-persisted-queries)
* [永続クエリのキャッシュの管理](/help/headless/graphql-api/graphiql-ide.md#managing-cache)

### GraphQL クエリの最適化 {#graphql-query-optimization}

同じモデルを共有するコンテンツフラグメントが多数ある AEM インスタンスでは、GraphQL のリストクエリに（リソースの点で）コストがかかる場合があります。

これは、GraphQL クエリ内で使用されているモデルを共有する&#x200B;*すべての*&#x200B;フラグメントを、メモリに読み込む必要があるためです。これは時間とメモリの両方を消費します。 結果セット全体をメモリに読み込んだ&#x200B;**後に**&#x200B;のみ、（最終的な）結果セット内の項目数を減らす可能性のあるフィルタリングを適用できます。

これにより、小さな結果セットでもパフォーマンスが低下するというインプレッションを与える可能性があります。ただし、実際には、フィルタリングを適用する前に内部で処理する必要があるので、初期結果セットのサイズが原因で速度が低下します。

パフォーマンスとメモリの問題を減らすには、この初期結果セットをできるだけ小さく保つ必要があります。

AEM には、GraphQL クエリを最適化する 2 つの方法があります。

* [ハイブリッドフィルタリング](#use-aem-graphql-hybrid-filtering)
* [ページング](#use-aem-graphql-pagination)（またはページネーション）

   * [並べ替え](#use-graphql-sorting)は、最適化に直接関連していませんが、ページングに関連しています

各アプローチには、独自のユースケースと制限があります。 このセクションでは、ハイブリッドフィルターとページングに関する情報と、GraphQL クエリの最適化で使うための[ベストプラクティス](#best-practices)をいくつか紹介します。

#### AEM GraphQL ハイブリッドフィルタリングを使用する {#use-aem-graphql-hybrid-filtering}

**レコメンデーション**

ハイブリッドフィルタリングは、JCR フィルタリングと AEM フィルタリングを組み合わせます。

結果セットを AEM フィルタリング用のメモリに読み込む前に、（クエリ制約の形式で）JCR フィルターを適用します。 これは、JCR フィルターによって余分な結果が先に削除されるので、メモリに読み込まれる結果セットを減らすためです。

>[!NOTE]
>
>技術的な理由（柔軟性、フラグメントのネストなど）により、AEM はフィルタリング全体を JCR に委任できません。

この方法では、GraphQL フィルターが提供する柔軟性を維持しながら、可能な限り多くのフィルタリングを JCR に委任できます。

>[!NOTE]
>
>AEM ハイブリッドフィルタリングを使用するには、既存のコンテンツフラグメントを更新する必要があります

**その他の参照**

以下を参照してください。

* [GraphQL フィルタリングでのページングと並べ替えのためのコンテンツフラグメントの更新](/help/headless/graphql-api/graphql-optimized-filtering-content-update.md)
* [_tags ID でフィルタリングされた（バリエーションを除く）サンプルクエリ](/help/headless/graphql-api/sample-queries.md#sample-filtering-tag-not-variations)

#### GraphQL のページネーションを使用する {#use-aem-graphql-pagination}

**レコメンデーション**

大きな結果セットを持つ複雑なクエリの応答時間は、GraphQL 標準のページネーションを使用して応答をチャンクにセグメント化することで、改善できます。

AEM の GraphQL では、次の 2 種類のページネーションに対応しています。

* [制限／オフセットベースのページネーション](/help/headless/graphql-api/content-fragments.md#list-offset-limit)
これは、リストクエリに使用されます。これらは `List` の値で終わります（例：`articleList`）。
これを使用するには、最初に返す項目（`offset`）と返す項目の数（`limit` またはページサイズ）を指定する必要があります。

* [カーソルベースのページネーション](/help/headless/graphql-api/content-fragments.md#paginated-first-after)（`first` および `after` で表される）
これにより、項目ごとに一意の ID が提供されます。「カーソル」とも呼ばれます。
クエリでは、前のページの最後の項目のカーソルとページサイズ（返される項目の最大数）を指定します。

  カーソルベースのページネーションはリストベースのクエリのデータ構造内に収まらないので、AEM では `Paginated` クエリタイプ（例： `articlePaginated`）を導入しました。 使用するデータ構造とパラメーターは、[GraphQL Cursor ConnectionSpecification](https://relay.dev/graphql/connections.htm) に準拠します。

  >[!NOTE]
  >
  >AEM は現在、前方ページングをサポートしています（`after`/`first` パラメーターを使用）。
  >
  >後方ページング（`before`/`last` パラメーターを使用）はサポートされていません。

**その他の参照**

以下を参照してください。

* [first と after を使用したサンプルページネーションクエリ](/help/headless/graphql-api/sample-queries.md#sample-pagination-first-after)

#### GraphQL の並べ替えを使用する {#use-graphql-sorting}

**レコメンデーション**

また、GraphQL 標準の並べ替え機能を使用すると、クライアントは JSON コンテンツを並べ替えられた順序で受け取ることができます。これにより、クライアント上でのさらなる処理の必要性が減少します。

並べ替えは、すべての並べ替え条件が最上位のフラグメントに関連している場合にのみ効率的です。

並べ替え順に、ネストされたフラグメントに配置された 1 つ以上のフィールドが含まれている場合、最上位モデルを共有するすべてのフラグメントをメモリに読み込む必要があります。 これにより、パフォーマンスが低下します。

>[!NOTE]
>
>最上位フィールドでの並べ替えも、（小さくても）パフォーマンスに影響を与えます。

**その他の参照**

以下を参照してください。

* [_tags ID でフィルタリングし、バリエーションを除外し、名前で並べ替えられたクエリの例](/help/headless/graphql-api/sample-queries.md#sample-filtering-tag-not-variations)

## ベストプラクティス {#best-practices}

すべての最適化レコメンデーションでの主な目的は、初期結果セットを減らすことです。ここに示すベストプラクティスで、その方法を説明します。 組み合わせることができます（推奨）。

### 最上位のプロパティのみをフィルター {#filter-top-level-properties-only}

現在、JCR レベルでのフィルタリングは、最上位のフラグメントに対してのみ機能します。

フィルターがネストされたフラグメントのフィールドに対応する場合、AEM はフォールバックして、基になるモデルを共有するすべてのフラグメントを（メモリに）読み込む必要があります。

最上位のフラグメントのフィールドとネストされたフラグメントのフィールドのフィルター式を、[AND 演算子](#logical-operations-in-filter-expressions)と組み合わせることで、このような GraphQL クエリを引き続き最適化できます。

### コンテンツ構造の使用 {#use-content-structure}

AEM では、通常、リポジトリ構造を使用して、処理するコンテンツの範囲を絞り込むことをお勧めします。

この方法は、GraphQL クエリにも適用する必要があります。

これを実行するには、最上位フラグメントの `_path` フィールドにフィルターを適用します。

```graphql
{
  someList(filter: {
    _path: {
      _expressions: [ 
        {
          value: "/content/dam/some/sub/path/",
          _operator: STARTS_WITH
        }
      ]
    }
  }) {
    items {
      # ...
    }
  }
}
```

>[!NOTE]
>
>最高のパフォーマンスを得るには、`value` の末尾に `/` を付ける必要があります。

### ページングの使用 {#use-paging}

ページングを使用して、初期の結果セットを減らすこともできます（特に、リクエストでフィルタリングと並べ替えを使用しない場合）。

ネストされたフラグメントをフィルターまたは並べ替える場合でも、AEM は大量のフラグメントをメモリに読み込む必要があるので、ページ分割されたクエリの処理に時間がかかる場合があります。 したがって、フィルタリングとページングを組み合わせる場合は、（前述のように）フィルタリングのルールを考慮してください。

ページングの場合、ページ分割された結果が常に明示的または暗黙的に並べ替えられるので、並べ替えも同様に重要です。

最初の数ページのみを取得したい場合、`...List` クエリと `...Paginated` クエリの使用に大きな違いはありません。 ただし、アプリケーションで 1～2 ページ以上のページを読みたい場合は、`...Paginated` クエリを使用することをお勧めします。後のページで、パフォーマンスが著しく向上します。

### フィルター式の論理演算 {#logical-operations-in-filter-expressions}

ネストされたフラグメントをフィルタリングする場合でも、`AND` 演算子を使用して組み合わされた最上位フィールドに付随するフィルターを提供して、JCR フィルタリングを適用できます。

一般的なユースケースは、最上位フラグメントの `_path` フィールドでフィルターを使用してクエリの範囲を制限し、最上位またはネストされたフラグメント上の追加フィールドでフィルタリングすることです。

この場合、様々なフィルター式が `AND` で組み合わされます。したがって、`_path` のフィルターにより、初期の結果セットが効果的に制限されます。 最上位フィールドのその他すべてのフィルターも、`AND` で組み合わせた場合を除き、初期結果セットを減らすのに役立ちます。

ネストされたフラグメントが含まれている場合、`OR` で組み合わされたフィルター式を最適化できません。`OR` 式は、ネストされたフラグメントが含まれて&#x200B;*いない*&#x200B;場合にのみ最適化できます。

### 複数行のテキストフィールドに対するフィルタリングの回避 {#avoid-filtering-multiline-textfields}

複数行のテキストフィールド（html、markdown、plaintext、json）のフィールドは、JCR クエリでフィルタリングできません。これらのフィールドの内容をその場で計算する必要があるからです。

それでも複数行のテキストフィールドに対してフィルタリングする必要がある場合は、フィルター式を追加して、初期の結果セットのサイズを制限し、`AND` と組み合わせることを検討してください。`_path` フィールドに対してフィルタリングして範囲を制限することも、適切なアプローチです。

### 仮想フィールドに対するフィルタリングの回避 {#avoid-filtering-virtual-fields}

仮想フィールド（`_` で始まるほとんどのフィールド）は、GraphQL クエリの実行中に計算されるので、JCR ベースのフィルタリングの範囲外です。

重要な例外は `_path` フィールです。コンテンツが適切に構造化されている場合は、初期結果セットのサイズを効果的に削減するために使用できます（[コンテンツ構造の使用](#use-content-structure)を参照）。

### ：フィルタリング除外 {#filtering-exclusions}

JCR レベルでフィルター式を評価できない場合が他にもいくつかあります（したがって、最高のパフォーマンスを実現するには回避する必要があります）。

* `_sensitiveness` フィルターオプションを使用し、`_sensitiveness` が `0.0` 以外に設定されている `Float` 値の式をフィルタリングします。

* `_ignoreCase` フィルターオプションを使用して、`String` 値の式をフィルタリングします。

* `null` 値のフィルタリング。

* `_apply: ALL_OR_EMPTY` を使用して配列をフィルタリングします。

* `_apply: INSTANCES`、`_instances: 0` を使用して配列をフィルタリングします。

* `CONTAINS_NOT` 演算子を使用して式をフィルタリングします。 

* `NOT_AT` 演算子を使用する `Calendar`、`Date` または `Time` 値の式をフィルタリングします。

### コンテンツフラグメントのネストを最小化する {#minimize-content-fragment-nesting}

コンテンツフラグメントのネストは、カスタムコンテンツ構造をモデル化する優れた方法です。ネストされたフラグメントを含むフラグメントを持つこともできます。そのフラグメントには、ネストされたフラグメントも含まれ、その中に…などが含まれています。

ただし、レベルが多すぎる構造を作成すると、GraphQL はネストされたすべてのコンテンツフラグメントの階層全体をトラバースする必要があるので、GraphQL クエリの処理時間が長くなる可能性があります。

深いネストは、コンテンツガバナンスに悪影響を与える可能性もあります。一般に、コンテンツフラグメントのネストは、5 レベルまたは 6 レベル未満に制限することをお勧めします。

### すべての形式を出力しない（複数行テキストの要素） {#do-not-output-all-formats}

AEM GraphQL は、複数の形式（リッチテキスト、シンプルテキスト、マークダウン）の&#x200B;**[複数行テキスト](/help/sites-cloud/administering/content-fragments/content-fragment-models.md#data-types)**&#x200B;データタイプで記述されるテキストを返すことができます。

3 つの形式をすべて出力すると、JSON で出力されるテキストのサイズが 3 倍になります。これを非常に広範なクエリからの大きな結果セットと組み合わせると、生成される JSON 応答が非常に大きくなり、計算に長い時間がかかることになります。そのため、コンテンツのレンダリングに必要なテキスト形式のみに出力を制限することをお勧めします。

### コンテンツフラグメントの変更 {#modifying-content-fragments}

AEM UI または API を使用して、コンテンツフラグメントとそれらのリソースを変更します。JCR で直接、変更を行わないでください。

### クエリをテストする {#test-your-queries}

GraphQL クエリの処理は検索クエリの処理と似ており、単純な GET-all-content API リクエストよりも大幅に複雑です。

管理対象の非実稼動環境でクエリを慎重に計画、テスト、最適化することが、後で実稼動環境で使用する際に成功するための鍵となります。
