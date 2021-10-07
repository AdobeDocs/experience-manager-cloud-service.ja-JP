---
title: Query Builder の述語リファレンス
description: Query Builder API の述語リファレンスです。
exl-id: 77118ef7-4d29-470d-9c4b-20537a408940
source-git-commit: 08559417c8047c592f2db54321afe68836b75bd1
workflow-type: tm+mt
source-wordcount: '2218'
ht-degree: 99%

---

# Query Builder の述語リファレンス {#query-builder-predicate-reference}

## 一般 {#general}

### root {#root}

これはルート述語グループです。グループのすべての機能に対応し、グローバルクエリパラメーターを設定できます。

「root」という名前は暗黙的で、クエリでは使用されません。

#### プロパティ {#properties-18}

* **`p.offset`** - 結果ページの開始を表す数値（スキップする項目数）
* **`p.limit`** - ページのサイズを表す数値
* **`p.guessTotal`** - 推奨：負荷が大きくなる場合があるので、結果をすべて計算することは避けるようにしてください。カウントする最大数（1000 など、大まかなサイズに関する十分なフィードバックが得られ、結果が比較的少数の場合は正確な量がわかる数値）、または最低限必要な数値（`p.offset` + `p.limit`）までをカウントする場合は `true`
* **`p.excerpt`** - `true` に設定した場合は、完全なテキストの抜粋が結果に含まれます
* **`p.hits`** - （JSON サーブレット専用）ヒットを JSON として記述する方法を、次の標準的なものの中から選択します（ResultHitWriter サービスを使用して拡張可能）
   * **`simple`** - `path`、`title`、`lastmodified`、`excerpt`（設定されている場合）などの最小限の項目
   * **`full`** - ノードの Sling JSON レンダリング。`jcr:path` はヒットのパスを示します。デフォルトではノードの直属のプロパティのみをリストし、`p.nodedepth=N` で指定された深さのツリーが含まれます（0 は無制限のサブツリー全体を表します）。`p.acls=true` を追加すると、特定の結果項目の現在のセッションの JCR 権限が含まれます（マッピング：`create` = `add_node`、`modify` = `set_property`、`delete` = `remove`）
   * **`selective`** - `p.properties` で指定されたプロパティのみ。相対パスのスペース区切り（URL では `+` を使用）のリストになります。相対パスの深さが `>1` の場合は、子オブジェクトとして表現されます。特殊な `jcr:path` プロパティにはヒットのパスが含まれます

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

これは概念上は `(1_property` OR `2_property)` になります。

以下は、ネストされたグループの例です。

```text
fulltext=Management
group.p.or=true
group.1_group.path=/content/wknd/ch/de
group.1_group.type=cq:Page
group.2_group.path=/content/dam/wknd
group.2_group.type=dam:Asset
```

この例では、`/content/wknd/ch/de` のページ内または `/content/dam/wknd` のアセット内で **Management** という語句を検索します。

これは概念上は `fulltext AND ( (path AND type) OR (path AND type) )` になります。このような OR 結合では、パフォーマンス上の理由から適切なインデックスが必要です。

#### プロパティ {#properties-6}

* **`p.or`** - `true` に設定した場合は、一致する必要があるのはグループ内の 1 つの述語のみになります。デフォルトは `false` です。この場合は、すべてが一致する必要があります。
* **`p.not`** - `true` に設定されている場合は、グループを否定します（デフォルトは `false`）
* **`<predicate>`** - ネストされた述語を追加します
* **`N_<predicate>`** - `1_property, 2_property, ...` など、複数のネストされた述語をまとめて追加します。

### orderby {#orderby}

この述語を使用すると、結果を並べ替えることができます。複数のプロパティ別に並べ替える必要がある場合は、`1_orderby=first`、`2_oderby=second` などの数字のプレフィックスを使用して、この述語を複数回追加する必要があります。

#### プロパティ {#properties-13}

* **`orderby`** - 並べ替えの基準となる、先頭が @ の JCR プロパティ名（例：`@jcr:lastModified`、`@jcr:content/jcr:title`）またはクエリ内の別の述語（例：`2_property`）
* **`sort`** - 並べ替えの方向。降順の場合は `desc`、昇順の場合は `asc`（デフォルト）です
* **`case`** - `ignore` に設定すると、並べ替えで大文字と小文字が区別されなくなります（`a` が `B` の前になります）。空白または未指定の場合は、並べ替えで大文字と小文字が区別されます（`B` が `a` の前になります）

## 述語 {#predicates}

### boolproperty {#boolproperty}

JCR ブール値プロパティと照合されます。受け入れられる値は `true` と `false` のみです。`false` の場合は、プロパティの値が `false` の場合または存在しない場合に一致します。有効になっている場合のみ設定されるブール型のフラグをチェックする際に便利です。

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

2 つの JCR 日付プロパティを比較します。等しい、等しくない、より大きい、以上かどうかをテストできます。

これはフィルターのみの述語で、検索インデックスは利用できません。

#### プロパティ {#properties-2}

* **`property1`** - 1 つ目の日付プロパティのパス
* **`property2`** - 2 つ目の日付プロパティのパス
* **`operation`**
   * `=`：完全一致（デフォルト）
   * `!=`：不等比較
   * `>`：`property1` は `property2` より大きい
   * `>=`：`property1` は `property2` 以上

### daterange {#daterange}

JCR 日付プロパティを日時の間隔と照合します。ISO8601 形式の日時（`YYYY-MM-DDTHH:mm:ss.SSSZ`）を使用します。`YYYY-MM-DD` などの部分表記も可能です。あるいは、タイムスタンプを POSIX 時間として指定することもできます。

2 つのタイムスタンプの間や、特定の日付より前または後のものを検索できるほか、両値を含めるか含めないかを選択することもできます。

ファセットの抽出に対応しており、`today`、`this week`、`this month`、`last 3 months`、`this year`、`last year`、`earlier than last year` の各バケットを提供します。

フィルターには対応していません。

#### プロパティ {#properties-3}

* **`property`** - `DATE` プロパティの相対パス（例：`jcr:lastModified`）
* **`lowerBound`** - プロパティでチェックする日付の下限（例：`2014-10-01`）
* **`lowerOperation`** - `>`（より後）または `>=`（以降）。`lowerBound` に適用されます。デフォルトは `>` です
* **`upperBound`** - プロパティでチェックする日付の上限（例：`2014-10-01T12:15:00`）
* **`upperOperation`** - `<`（より前）または `<=`（以前）。`upperBound` に適用されます。デフォルトは `<` です
* **`timeZone`** - ISO-8601 の日付文字列で指定されていない場合に使用するタイムゾーンの ID。デフォルトは、システムのデフォルトのタイムゾーンです。

### excludepaths {#excludepaths}

パスが正規表現に一致するノードを結果から除外します。

これはフィルターのみの述語で、検索インデックスは利用できません。

ファセットの抽出には対応していません。

#### プロパティ {#properties-4}

* **`excludepaths`** - 結果のパスと照合される正規表現。一致したパスは結果から除外されます。

### fulltext {#fulltext}

フルテキストのインデックスの語句を検索します。

フィルターには対応していません。

ファセットの抽出には対応していません。

#### プロパティ {#properties-5}

* **`fulltext`** - フルテキストの検索語句。
* **`relPath`** - プロパティまたはサブノードの検索の相対パス。このプロパティはオプションです。

### hasPermission {#haspermission}

指定された [JCR 権限](https://www.adobe.io/experience-manager/reference-materials/spec/jcr/2.0/16_Access_Control_Management.html#16.2.3%20Standard%20Privileges)が現在のセッションに含まれる項目に、結果を制限します。

これはフィルターのみの述語で、検索インデックスは利用できません。ファセットの抽出には対応していません。

#### プロパティ {#properties-7}

* **`hasPermission`** - 対象のノードに対して現在のユーザーセッションがすべて持っている必要がある JCR 権限のコンマ区切りリスト（例：`jcr:write`,`jcr:modifyAccessControl`）

### language {#language}

特定の言語の AEM ページを検索します。ページの言語プロパティと、ページパス（一般的に最上位レベルのサイト構造に言語やロケールが含まれています）の両方を検索します。

これはフィルターのみの述語で、検索インデックスは利用できません。

ファセットの抽出に対応しており、一意の言語コードごとにバケットを提供します。

#### プロパティ {#properties-8}

* **`language`** - ISO 言語コード（例：`de`）

### mainasset {#mainasset}

ノードがサブアセットではなく、DAM メインアセットであるかどうかをチェックします。DAM メインアセットは、基本的には、サブアセットノード外のすべてのノードです。`dam:Asset` ノードタイプはチェックされません。この述語を使用するには、`mainasset=true` または `mainasset=false` を設定するだけです。他にプロパティはありません。

これはフィルターのみの述語で、検索インデックスは利用できません。

ファセットの抽出に対応しており、メインアセットとサブアセット用に 2 つのバケットを提供します。

#### プロパティ {#properties-9}

* **`mainasset`** - ブール値。メインアセットの場合は `true`、サブアセットの場合は `false` です

### memberOf {#memberof}

特定の [Sling リソースコレクション](https://docs.adobe.com/content/help/en/experience-manager-cloud-service-javadoc/org/apache/sling/resource/collection/ResourceCollection.html)のメンバーである項目を検索します。

これはフィルターのみの述語で、検索インデックスは利用できません。

ファセットの抽出には対応していません。

#### プロパティ {#properties-10}

* **`memberOf`** - Sling リソースコレクションのパス

### nodename {#nodename}

JCR ノード名と照合されます。

ファセットの抽出に対応しており、一意の各ノード名（ファイル名）ごとにバケットを提供します。

#### プロパティ {#properties-11}

* **`nodename`** - ワイルドカードを使用できるノード名パターン：`*` は 0 個以上の任意の文字、`?` は任意の文字、`[abc]` は角括弧内の文字のみ

### notexpired {#notexpired}

JCR 日付プロパティが現在のサーバー時間より後か同じかをチェックすることで項目を照合します。これは、`expiresAt` 値をチェックし、有効期限が切れていない値（`notexpired=true` の場合）または既に期限が切れている値（`notexpired=false` の場合）に結果を限定する場合に使用できます。

フィルターには対応していません。

[`daterange`](#daterange) 述語と同じように、ファセットの抽出に対応しています。

#### プロパティ {#properties-12}

* **`notexpired`** - ブール値。有効期限が切れていない（日付が現在以降である）場合は `true`、有効期限が切れている（日付が過去である）場合は `false` です（必須）
* **`property`** - チェックする `DATE` プロパティの相対パス（必須）

### path {#path}

指定されたパス内を検索します。

ファセットの抽出には対応していません。

#### プロパティ {#properties-14}

* **`path`** - パスパターンを定義します。
   * `exact` プロパティに応じて、サブツリー全体が一致する（xpath に `//*` を付加する場合と同様。ただし、ベースパスを含まない）か、完全一致のパスのみが一致します。後者の場合はワイルドカード（`*`）を含めることができます。
      * デフォルトは `true`
   * `self` プロパティが設定されている場合は、ベースノードを含むサブツリー全体が検索されます。
* **`exact`** - `exact` が `true` の場合は、パスが完全に一致する必要があります。ただし、名前に一致する簡単なワイルドカード（`*`）を含めることができます（`/` は不可）。`false`（デフォルト）の場合は、すべての下位要素が含まれます（オプション）
* **`flat`** - 直属の子（xpath に `/*` を付加した場合と同様）のみを検索します（`exact` が true ではない場合のみ使用されます。オプション）
* **`self`** - サブツリーを検索しますが、パスとして指定されたベースノードが含まれます（ワイルドカードは不可）

### property {#property}

JCR プロパティおよびその値と照合されます。

ファセットの抽出に対応しており、結果の一意のプロパティ値ごとにバケットを提供します。

#### プロパティ {#properties-15}

* **`property`** - プロパティの相対パス（例：`jcr:title`）
* **`value`** - プロパティでチェックする値。JCR プロパティタイプから文字列への変換に従います
* **`N_value`** - `1_value`、`2_value` などを使用して複数の値（デフォルトで `OR` で結合、`and=true` の場合は `AND` で結合）をチェックします
* **`and`** - 複数の値（`N_value`）を `AND` で結合する場合は `true` に設定
* **`operation`**
   * `equals`：完全一致（デフォルト）
   * `unequals`：不等比較
   * `like`：xpath 関数 `jcr:like` を使用（オプション）
   * `not`：一致しない（例：xpath の `not(@prop)` では値パラメーターが無視されます）
   * `exists`：存在するかどうかをチェック
      * `true` - プロパティが存在する必要があります
      * `false` - `not` と同じで、これがデフォルト
* **`depth`** - プロパティ／相対パスが存在するワイルドカードのレベル数（例：`property=size depth=2` の場合は `node/size`、`node/*/size`、`node/*/*/size` をチェック）

### rangeproperty {#rangeproperty}

JCR プロパティを間隔と照合します。`LONG`、`DOUBLE`、`DECIMAL` などの線形タイプのプロパティに適用されます。`DATE` に関しては、最適化された日付形式の入力情報を含む [`daterange`](#daterange) 述語を参照してください。

下限、上限またはその両方を定義できます。演算（未満や以下など）を下限と上限に個別に指定することもできます。

ファセットの抽出には対応していません。

#### プロパティ {#properties-16}

* **`property`** - プロパティの相対パス
* **`lowerBound`** - プロパティでチェックする下限
* **`lowerOperation`** - `>`（デフォルト）または `>=`。`lowerValue` に適用されます
* **`upperBound`** - プロパティでチェックする上限
* **`upperOperation`** - `<`（デフォルト）または `<=`。`lowerValue` に適用されます
* **`decimal`** - チェックされたプロパティのタイプが Decimal の場合は `true`

### relativedaterange {#relativedaterange}

`JCR DATE` プロパティを日時の間隔と照合します（現在のサーバー時間に対する時間オフセットを使用します）。ミリ秒値または Bugzilla 構文 `1s 2m 3h 4d 5w 6M 7y`（それぞれ 1 秒、2 分、3 時間、4 日、5 週間、6 か月、7 年）を使用して、`lowerBound` と `upperBound` を指定できます。先頭に `-` を付けると、オフセットが現在の時間より前のマイナスであることを意味します。`lowerBound` または `upperBound` のいずれかのみを指定する場合は、他方がデフォルトで `0`（現在の時間）になります。

次に例を示します。

* `upperBound=1h` を指定（`lowerBound` を指定しない）：次の 1 時間以内の時刻を選択
* `lowerBound=-1d` を指定（`upperBound` を指定しない）：過去 24 時間以内の時刻を選択
* `lowerBound=-6M` と `upperBound=-3M` を指定：過去 3～6 か月以内の時刻を選択
* `lowerBound=-1500` と `upperBound=5500` を指定：1500 ミリ秒前から 5500 ミリ秒後の間の時刻を選択
* `lowerBound=1d` と `upperBound=2d` を指定：明後日の時刻を選択

うるう年は考慮されず、すべての月が 30 日になる点にご注意ください。

フィルターには対応していません。

[`daterange`](#daterange) 述語と同じように、ファセットの抽出に対応しています。

#### プロパティ {#properties-17}

* **`upperBound`** - 現在のサーバー時間を基準とした日付の上限。ミリ秒単位または `1s 2m 3h 4d 5w 6M 7y`（それぞれ 1 秒、2 分、3 時間、4 日、5 週間、6 か月、7 年）で指定します。オフセットがマイナスの場合は `-` を使用します
* **`lowerBound`** - 現在のサーバー時間を基準とした日付の下限。ミリ秒単位または `1s 2m 3h 4d 5w 6M 7y`（それぞれ 1 秒、2 分、3 時間、4 日、5 週間、6 か月、7 年）で指定します。オフセットがマイナスの場合は `-` を使用します。

### savedquery {#savedquery}

永続的な Query Builder クエリのすべての述語を、サブグループの述語として現在のクエリに含めます。

これによって追加のクエリが実行されるわけではなく、現在のクエリが拡張されます。

クエリは `QueryBuilder#storeQuery()` を使用してプログラムで永続化できます。可能な形式は、複数行の `String` プロパティか、Java プロパティ形式のテキストファイルとしてクエリを含む `nt:file` ノードのいずれかです。

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

キーワードを指定して、タグが付けられているコンテンツを検索します。最初にタイトル内に対象のキーワードを含むタグを検索してから、それらのタグが付いている項目のみに結果を制限します。

ファセットの抽出には対応していません。

#### プロパティ {#Properties-1}

* **`tagsearch`** - タグタイトル内で検索するキーワード
* **`property`** - 考慮するプロパティまたはプロパティの相対パス（デフォルトは `cq:tags`）
* **`lang`** - 特定の言語にローカライズされたタグタイトルのみを対象に検索します（例：`de`）
* **`all`** - タグのフルテキスト全体（すべてのタイトル、説明など）を検索するかどうかを示すブール値（`lang` より優先）

### type {#type}

特定の JCR ノードのタイプ（プライマリノードタイプまたは Mixin タイプ）に結果を制限します。そのノードタイプのサブタイプも検索します。リポジトリーの検索インデックスでは、効率的に実行できるノードタイプに対応する必要があります。

ファセットの抽出に対応しており、結果の一意の型ごとにバケットを提供します。

#### プロパティ {#Properties-2}

* **`type`** - 検索するノードタイプまたは Mixin 名（例：`cq:Page`）
