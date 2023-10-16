---
title: Query Builder の述語リファレンス
description: AEM as a Cloud Serviceの Query Builder API の述語リファレンス。
exl-id: 77118ef7-4d29-470d-9c4b-20537a408940
source-git-commit: e10c39c1d7fa05b738dd8f25662617a3a9568f83
workflow-type: tm+mt
source-wordcount: '2295'
ht-degree: 56%

---

# Query Builder の述語リファレンス {#query-builder-predicate-reference}

## 一般 {#general}

### root {#root}

ルート述語グループ。 グループのすべての機能に対応し、グローバルクエリパラメーターを設定できます。

「root」という名前は、暗黙的なクエリでは使用されません。

#### プロパティ {#properties-18}

* **`p.offset`**  — 結果ページの開始（スキップする項目数）を示す数値。
* **`p.limit`** - ページのサイズを表す数値.
* **`p.guessTotal`**  — 推奨：結果の全体を計算するのを避けます。これはコストのかかる場合があります。最大数を示す数値（例：1000）で、大まかなサイズと小さい結果を得るための正確な数値に関する十分なフィードバックをユーザーに提供する数値 )。または、 `true` 必要最小限の数まで数える `p.offset` + `p.limit`.
* **`p.excerpt`**  — 設定されている場合は `true`、結果に完全なテキストの抜粋を含めます。
* **`p.indexTag`**  — 設定すると、クエリにインデックスタグオプションが含まれます ( [クエリオプションインデックスタグ](https://jackrabbit.apache.org/oak/docs/query/query-engine.html#query-option-index-tag)) をクリックします。
* **`p.facetStrategy`**  — 設定されている場合は `oak`、Query Builder はファセット抽出を Oak に委任します ( [ファセット](https://jackrabbit.apache.org/oak/docs/query/query-engine.html#facets)) をクリックします。
* **`p.hits`** - （JSON サーブレットのみ）ヒットが JSON として記述される方法を、これらの標準の方法で選択します（ResultHitWriter サービスを介して拡張可能）。
   * **`simple`**  — のような最小の項目 `path`, `title`, `lastmodified`, `excerpt` （設定されている場合）。
   * **`full`**  — ノードの sling JSON レンダリング（を使用） `jcr:path` ヒットのパスを示します。デフォルトでは、ノードの直接プロパティのリストのみが表示され、 `p.nodedepth=N`（0 はサブツリー全体を表し、無限サブツリーを表します）追加 `p.acls=true` 指定した結果項目に対する現在のセッションの JCR 権限を含めるには ( マッピング： `create` = `add_node`, `modify` = `set_property`, `delete` = `remove`) をクリックします。
   * **`selective`**  — 指定されたプロパティのみ `p.properties`：スペースで区切られた `+` （URL の）相対パスのリスト。 相対パスに深さがある場合 `>1`の場合、これらのプロパティは子オブジェクトとして表されます。 特別な `jcr:path` プロパティには、ヒットのパスが含まれます。

### group {#group}

この述語を使用すると、ネストされた条件を作成できます。グループにはネストされたグループを含めることができます。Query Builder クエリのすべての要素は、暗黙的にルートグループに含まれます。ルートグループでは、`p.or` および `p.not` パラメーターも指定できます。

次の例では、2 つのプロパティのいずれか 1 つを値と照合しています。

```text
group.p.or=true
group.1_property=jcr:title
group.1_property.value=My Page
group.2_property=navTitle
group.2_property.value=My Page
```

概念上は、 `(1_property` または `2_property)`.

以下は、ネストされたグループの例です。

```text
fulltext=Management
group.p.or=true
group.1_group.path=/content/wknd/ch/de
group.1_group.type=cq:Page
group.2_group.path=/content/dam/wknd
group.2_group.type=dam:Asset
```

用語の検索 **管理** ページ内 `/content/wknd/ch/de` または内のアセット `/content/dam/wknd`.

概念上は、 `fulltext AND ( (path AND type) OR (path AND type) )`. このような OR 結合は、パフォーマンス上の理由から、適切なインデックスが必要です。

#### プロパティ {#properties-6}

* **`p.or`** - `true` に設定した場合は、一致する必要があるのはグループ内の 1 つの述語のみになります。デフォルトはです。 `false`は、すべてが一致する必要があります。
* **`p.not`** - `true` に設定されている場合は、グループを否定します（デフォルトは `false`）
* **`<predicate>`** - ネストされた述語を追加します
* **`N_<predicate>`** - `1_property, 2_property, ...` など、複数のネストされた述語をまとめて追加します。

### orderby {#orderby}

この述語を使用すると、結果を並べ替えることができます。複数のプロパティによる並べ替えが必要な場合は、数値のプレフィックスを使用して、この述語を複数回追加する必要があります（例： ）。 `1_orderby=first`, `2_oderby=second`.

#### プロパティ {#properties-13}

* **`orderby`** - 並べ替えの基準となる、先頭が @ の JCR プロパティ名（例：`@jcr:lastModified`、`@jcr:content/jcr:title`）またはクエリ内の別の述語（例：`2_property`）
* **`sort`** - 並べ替えの方向。降順の場合は `desc`、昇順の場合は `asc`（デフォルト）です
* **`case`**  — 設定されている場合は `ignore`の場合、並べ替えでは大文字と小文字が区別されません。つまり、 `a` 次より前： `B`；空の場合または除外された場合、並べ替えでは大文字と小文字が区別されます。 `B` 次より前： `a`

## 述語 {#predicates}

### boolproperty {#boolproperty}

JCR ブール値プロパティと照合されます。受け入れられる値は `true` と `false` のみです。値が `false`を返した場合、プロパティの値が `false`、またはまったく存在しない場合は。 この述語は、有効な場合にのみ設定されるブール型フラグを確認する場合に役立ちます。

継承される `operation` パラメーターには意味はありません。

この述語はファセットの抽出に対応しており、`true` または `false` の値ごとにバケットを提供しますが、それは既存のプロパティの場合に限ります。

#### プロパティ {#properties}

* **`boolproperty`** - プロパティの相対パス（例：`myFeatureEnabled`、`jcr:content/myFeatureEnabled`）
* **`value`** - プロパティでチェックする値（`true` または `false`）

### contentfragment {#contentfragment}

結果をコンテンツフラグメントに限定します。

* フィルターには対応していません。
* ファセットの抽出には対応していません。

#### プロパティ {#properties-1}

* **`contentfragment`** - 任意の値と併用してコンテンツフラグメントをチェックできます。

### `dateComparison` {#datecomparison}

2 つの JCR 日付プロパティを比較します。等しい、等しくない、より大きいか等しいかをテストできます。

フィルターのみの述語で、検索インデックスは使用できません。

#### プロパティ {#properties-2}

* **`property1`** - 1 つ目の日付プロパティのパス
* **`property2`** - 2 つ目の日付プロパティのパス
* **`operation`**
   * `=`：完全一致（デフォルト）
   * `!=`：不等比較
   * `>`：`property1` は `property2` より大きい
   * `>=`：`property1` は `property2` 以上

### daterange {#daterange}

JCR 日付プロパティを日時の間隔と照合します。日時に ISO8601 形式を使用します (`YYYY-MM-DDTHH:mm:ss.SSSZ`) や、などの部分表現も許可します。 `YYYY-MM-DD`. あるいは、タイムスタンプを POSIX 時間として指定することもできます。

2 つのタイムスタンプの間や、特定の日付より前または後のものを検索できるほか、両値を含めるか含めないかを選択することもできます。

ファセットの抽出に対応しており、`today`、`this week`、`this month`、`last 3 months`、`this year`、`last year`、`earlier than last year` の各バケットを提供します。

フィルターには対応していません。

#### プロパティ {#properties-3}

* **`property`** - `DATE` プロパティの相対パス（例：`jcr:lastModified`）
* **`lowerBound`** - プロパティでチェックする日付の下限（例：`2014-10-01`）
* **`lowerOperation`** - `>`（より後）または `>=`（以降）。`lowerBound` に適用されます。デフォルトは `>` です
* **`upperBound`** - プロパティでチェックする日付の上限（例：`2014-10-01T12:15:00`）
* **`upperOperation`** - `<`（より前）または `<=`（以前）。`upperBound` に適用されます。デフォルトは `<` です
* **`timeZone`** - ISO-8601 の日付文字列で指定されていない場合に使用するタイムゾーンの ID。デフォルトは、システムのデフォルトタイムゾーンです。

### excludepaths {#excludepaths}

パスが正規表現に一致するノードを結果から除外します。

フィルターのみの述語で、検索インデックスは使用できません。

ファセットの抽出には対応していません。

#### プロパティ {#properties-4}

* **`excludepaths`** - 結果のパスと照合される正規表現。一致したパスは結果から除外されます。

### fulltext {#fulltext}

フルテキストインデックス内の用語を検索します。

フィルターには対応していません。

ファセットの抽出には対応していません。

#### プロパティ {#properties-5}

* **`fulltext`**  — 全文検索用語
* **`relPath`** - プロパティまたはサブノードの検索の相対パス。このプロパティはオプションです。

### hasPermission {#haspermission}

指定された [JCR 権限](https://developer.adobe.com/experience-manager/reference-materials/spec/jcr/2.0/16_Access_Control_Management.html#16.2.3%20Standard%20Privileges)が現在のセッションに含まれる項目に、結果を制限します。

フィルターのみの述語で、検索インデックスは使用できません。 ファセットの抽出には対応していません。

#### プロパティ {#properties-7}

* **`hasPermission`**  — 現在のユーザーセッションが対象のノードに対して持つ必要がある、すべてのコンマ区切りの JCR 権限。 例： `jcr:write`, `jcr:modifyAccessControl`

### language {#language}

特定の言語の AEM ページを検索します。ページ言語プロパティと、最上位のサイト構造に言語やロケールを含むページパスの両方を確認します。

フィルターのみの述語で、検索インデックスは使用できません。

ファセットの抽出に対応しており、一意の言語コードごとにバケットを提供します。

#### プロパティ {#properties-8}

* **`language`** - ISO 言語コード（例：`de`）

### mainasset {#mainasset}

ノードがサブアセットではなく、DAM メインアセットであるかどうかをチェックします。基本的に、サブアセットノード内にないすべてのノードです。 これは、 `dam:Asset` ノードタイプ。 この述語を使用するには、 `mainasset=true` または `mainasset=false`. 他にプロパティはありません。

フィルターのみの述語で、検索インデックスは使用できません。

ファセットの抽出に対応しており、メインアセットとサブアセット用に 2 つのバケットを提供します。

#### プロパティ {#properties-9}

* **`mainasset`** - ブール値。メインアセットの場合は `true`、サブアセットの場合は `false` です

### memberOf {#memberof}

特定の [Sling リソースコレクション](https://developer.adobe.com/experience-manager/reference-materials/cloud-service/javadoc/org/apache/sling/resource/collection/ResourceCollection.html)のメンバーである項目を検索します。

フィルターのみの述語で、検索インデックスは使用できません。

ファセットの抽出には対応していません。

#### プロパティ {#properties-10}

* **`memberOf`** - Sling リソースコレクションのパス

### nodename {#nodename}

JCR ノード名と照合されます。

ファセットの抽出に対応しており、一意の各ノード名（ファイル名）ごとにバケットを提供します。

#### プロパティ {#properties-11}

* **`nodename`** - ワイルドカードを使用できるノード名パターン：`*` は 0 個以上の任意の文字、`?` は任意の文字、`[abc]` は角括弧内の文字のみ

### notexpired {#notexpired}

JCR 日付プロパティが現在のサーバー時間より後か同じかをチェックすることで項目を照合します。これを使用して、 `expiresAt` の値を指定し、結果をまだ期限切れ (`notexpired=true`)、または既に期限切れ (`notexpired=false`) をクリックします。

フィルターには対応していません。

[`daterange`](#daterange) 述語と同じように、ファセットの抽出に対応しています。

#### プロパティ {#properties-12}

* **`notexpired`** - ブール値。有効期限が切れていない（日付が現在以降である）場合は `true`、有効期限が切れている（日付が過去である）場合は `false` です（必須）
* **`property`** - チェックする `DATE` プロパティの相対パス（必須）

### path {#path}

指定されたパス内を検索します。

ファセットの抽出には対応していません。

#### プロパティ {#properties-14}

* **`path`**  — パスパターンを定義します。
   * に応じて `exact` プロパティの場合は、サブツリー全体が一致する ( `//*` xpath では、ベースパスが含まれないことに注意してください )。または完全に一致するパスのみが一致し、ワイルドカード (`*`) をクリックします。
      * デフォルトは `true`.
&lt;!— * `self`プロパティが設定されている場合、ベースノードを含むサブツリー全体が検索されます。—>
* **`exact`** - if `exact` 次に該当 `true`、完全に一致するパスにする必要がありますが、単純なワイルドカード (`*`)、名前に一致するが一致しない `/`；の場合は `false` （デフォルト）すべての子孫が含まれます（オプション）。
* **`flat`**  — 直接の子のみを検索します ( `/*` xpath で )( `exact` が true ではない（オプション）。
* **`self`**  — サブツリーを検索しますが、パスとして指定されたベースノードが含まれます（ワイルドカードは使用できません）。
   * *重要な注意*：問題が `self` プロパティを使用してクエリを実行すると、正しい検索結果が生成されない場合があります。 現在のの実装の変更 `self` また、プロパティに依存する既存のアプリケーションが壊れる可能性があるので、プロパティは実行できません。 この機能により、 `self` プロパティは非推奨になりました。使用しないようにお勧めします。

### property {#property}

JCR プロパティおよびその値と照合されます。

ファセットの抽出に対応しており、結果の一意のプロパティ値ごとにバケットを提供します。

#### プロパティ {#properties-15}

* **`property`** - プロパティへの相対パス。例： `jcr:title`.
* **`value`** - プロパティでチェックする値。JCR プロパティタイプから文字列への変換に従います.
* **`N_value`**  — 使用 `1_value`, `2_value`、...複数の値をチェックします ( `OR` デフォルトでは、 `AND` if `and=true`) をクリックします。
* **`and`** - 複数の値（`N_value`）を `AND` で結合する場合は `true` に設定
* **`operation`**
   * `equals`：完全一致（デフォルト）。
   * `unequals` 不等式の比較用。
   * `like` を使用する場合 `jcr:like` xpath 関数（オプション）を使用します。
   * `not` 一致しない場合 ( 例： `not(@prop)` xpath では、値パラメーターは無視されます )。
   * `exists` 存在を確認するために。
      * `true` プロパティが存在する必要があります。
      * `false` はと同じです。 `not` がデフォルトです。
* **`depth`**  — プロパティ/相対パスが存在できるワイルドカードレベルの数 ( 例： `property=size depth=2` checks `node/size`, `node/*/size`、および `node/*/*/size`) をクリックします。

### rangeproperty {#rangeproperty}

JCR プロパティを間隔と照合します。次のような線形タイプのプロパティに適用されます。 `LONG`, `DOUBLE`、および `DECIMAL`. の場合 `DATE`を参照し、 [`daterange`](#daterange) 最適化された日付形式の入力を持つ述語。

下限、上限またはその両方を定義できます。また、下限と上限に対して、操作（例えば、より小さい、より小さい）を個別に指定することもできます。

ファセットの抽出には対応していません。

#### プロパティ {#properties-16}

* **`property`** - プロパティの相対パス
* **`lowerBound`** - プロパティでチェックする下限
* **`lowerOperation`** - `>`（デフォルト）または `>=`。`lowerValue` に適用されます
* **`upperBound`** - プロパティでチェックする上限
* **`upperOperation`** - `<`（デフォルト）または `<=`。`lowerValue` に適用されます
* **`decimal`** - チェックされたプロパティのタイプが Decimal の場合は `true`

### relativedaterange {#relativedaterange}

`JCR DATE` プロパティを日時の間隔と照合します（現在のサーバー時間に対する時間オフセットを使用します）。ミリ秒値または Bugzilla 構文 `1s 2m 3h 4d 5w 6M 7y`（それぞれ 1 秒、2 分、3 時間、4 日、5 週間、6 か月、7 年）を使用して、`lowerBound` と `upperBound` を指定できます。先頭に `-` を付けると、オフセットが現在の時間より前のマイナスであることを意味します。次のみを指定した場合、 `lowerBound` または `upperBound`を使用する場合、もう 1 つはデフォルトでに設定されます。 `0`：現在の時刻を表します。

次に例を示します。

* `upperBound=1h` を指定（`lowerBound` を指定しない）：次の 1 時間以内の時刻を選択
* `lowerBound=-1d` を指定（`upperBound` を指定しない）：過去 24 時間以内の時刻を選択
* `lowerBound=-6M` と `upperBound=-3M` を指定：過去 3～6 か月以内の時刻を選択
* `lowerBound=-1500` と `upperBound=5500` を指定：1500 ミリ秒前から 5500 ミリ秒後の間の時刻を選択
* `lowerBound=1d` と `upperBound=2d` を指定：明後日の時刻を選択

うるう年は考慮されず、すべての月が 30 日です。

フィルターには対応していません。

[`daterange`](#daterange) 述語と同じように、ファセットの抽出に対応しています。

#### プロパティ {#properties-17}

* **`upperBound`** - 現在のサーバー時間を基準とした日付の上限。ミリ秒単位または `1s 2m 3h 4d 5w 6M 7y`（それぞれ 1 秒、2 分、3 時間、4 日、5 週間、6 か月、7 年）で指定します。オフセットがマイナスの場合は `-` を使用します
* **`lowerBound`** - 現在のサーバー時間を基準とした日付の下限。ミリ秒単位または `1s 2m 3h 4d 5w 6M 7y`（それぞれ 1 秒、2 分、3 時間、4 日、5 週間、6 か月、7 年）で指定します。オフセットがマイナスの場合は `-` を使用します。

### savedquery {#savedquery}

永続的な Query Builder クエリのすべての述語を、サブグループの述語として現在のクエリに含めます。

追加のクエリは実行せず、現在のクエリを拡張します。

クエリは `QueryBuilder#storeQuery()` を使用してプログラムで永続化できます。複数行の形式を指定できます `String` プロパティまたは `nt:file` クエリをテキストファイルとして Java™プロパティ形式で含むノード。

保存済みクエリの述語のファセット抽出には対応していません。

#### プロパティ {#properties-19}

* **`savedquery`** - 保存済みクエリのパス（`String` プロパティまたは `nt:file` ノード）

### similar {#similar}

JCR XPath の `rep:similar()` を使用した類似性検索です。

フィルターにもファセットの抽出にも対応していません。

#### プロパティ {#properties-20}

* **`similar`** - 類似ノードを検索するノードの絶対パス
* **`local`** - 下位ノードの相対パスまたは現在のノードの `.`（オプション、デフォルトは `.`）

### tag {#tag}

タグタイトルのパスを指定して、タグが付けられているコンテンツを検索します。

ファセットの抽出に対応しており、現在のタグタイトルのパスを使用して一意のタグごとにバケットを提供します。

#### プロパティ {#properties-21}

* **`tag`** - 検索するタグタイトルのパス（例：`properties:orientation/landscape`）
* **`N_value`** - `1_value`、`2_value` などを使用して複数のタグ（デフォルトで `OR` で結合、`and=true` の場合は `AND` で結合）をチェックします
* **`property`** - 検索するプロパティまたはプロパティの相対パス（デフォルトは `cq:tags`）

### tagid {#tagid}

タグ ID を指定して、タグが付けられているコンテンツを検索します。

ファセットの抽出に対応しており、現在のタグ ID を使用して一意のタグごとにバケットを提供します。

#### プロパティ {#properties-22}

* **`tagid`** - 検索するタグ ID（例：`properties:orientation/landscape`）
* **`N_value`** - `1_value`、`2_value` などを使用して複数のタグ ID（デフォルトで `OR` で結合、`and=true` の場合は `AND` で結合）をチェックします
* **`property`** - 検索するプロパティまたはプロパティの相対パス（デフォルトは `cq:tags`）

### tagsearch {#tagsearch}

キーワードを指定して、タグが付けられているコンテンツを検索します。まず、タイトルにこれらのキーワードを含むタグを検索し、その結果を、これらのキーワードでタグ付けされた項目のみに制限します。

ファセットの抽出には対応していません。

#### プロパティ {#Properties-1}

* **`tagsearch`** - タグタイトル内で検索するキーワード
* **`property`** - 考慮するプロパティまたはプロパティの相対パス（デフォルトは `cq:tags`）
* **`lang`** - 特定の言語にローカライズされたタグタイトルのみを対象に検索する（例：`de`）
* **`all`**  — タグの全文、つまりすべてのタイトルや説明などを検索する（が優先される）ブール値 `lang`)

### type {#type}

この述語は、結果を特定の JCR ノードタイプ ( プライマリノードタイプまたは `mixin` タイプ。 また、そのノードタイプのサブタイプも検索します。 リポジトリ検索インデックスでは、効率的に実行するために、ノードタイプをカバーする必要があります。

ファセットの抽出に対応しており、結果の一意の型ごとにバケットを提供します。

#### プロパティ {#Properties-2}

* **`type`**`mixin` - 検索するノードタイプまたは 名（例：`cq:Page`）
