---
title: Query Builder の述語リファレンス
description: クエリビルダーAPIの述語参照。
translation-type: tm+mt
source-git-commit: 90b635cb31af910e08bdee7925cec0c7beb05318
workflow-type: tm+mt
source-wordcount: '2221'
ht-degree: 16%

---


# Query Builder の述語リファレンス {#query-builder-predicate-reference}

## 一般 {#general}

### root {#root}

これは、root predicateグループです。 グループのすべての機能をサポートし、グローバルクエリパラメーターを設定できます。

「root」という名前は暗黙的で、クエリでは使用されません。

#### プロパティ {#properties-18}

* **`p.offset`**  — 結果ページの開始を示す数値（スキップする項目数）
* **`p.limit`**  — ページサイズを示す番号
* **`p.guessTotal`**  — 推奨：コストのかかる結果の総計を計算しないようにする。最大カウント総数を示す数値（1000など、粗いサイズに対する十分なフィードバックと小さい結果を求める正確な数値）または必要な最小限 `true` の数 `p.offset` +  `p.limit`
* **`p.excerpt`**  — に設定した場合、結果に全文の抜粋 `true`を含めます。
* **`p.hits`**  — （JSONサーブレットの場合のみ）ヒットをJSONとして書き込む方法を選択します。標準の方法は次のとおりです（ResultHitWriterサービスを介して拡張可能）。
   * **`simple`** -  `path`、 `title`、 `lastmodified`、 `excerpt` （設定されている場合）など、最小の項目
   * **`full`**  — ヒットのパスを `jcr:path` 示す、ノードのsling JSONレンダリング：デフォルトでは、リストの直接的なプロパティだけがノードのより深いツリーを含めます。0は `p.nodedepth=N`無限サブツリー全体を意味します。特定 `p.acls=true` の結果アイテム(マッピング： `create` =  `add_node`、 `modify` =  `set_property`、 `delete` =  `remove`)
   * **`selective`**  — で指定されたプロパティのみ `p.properties`。スペース区切り(URL `+` で使用)の相対パスのリスト。相対パスに深さがある場合、 `>1` これらは子オブジェクトとして表されます。特別な `jcr:path` プロパティには、ヒットのパスが含まれます

### グループ {#group}

この述語は、ネストされた条件を構築できます。 グループにはネストされたグループを含めることができます。クエリビルダークエリ内のすべてはルートグループ内で暗黙的に行われます。ルートグループには`p.or`パラメーターと`p.not`パラメーターを含めることもできます。

次の例では、2つのプロパティのいずれか1つを値と照合します。

```text
group.p.or=true
group.1_property=jcr:title
group.1_property.value=My Page
group.2_property=navTitle
group.2_property.value=My Page
```

これは概念的には`(1_property` OR `2_property)`です。

以下は、ネストグループの例です。

```text
fulltext=Management
group.p.or=true
group.1_group.path=/content/wknd/ch/de
group.1_group.type=cq:Page
group.2_group.path=/content/dam/wknd
group.2_group.type=dam:Asset
```

これは、`/content/wknd/ch/de`のページ内または`/content/dam/wknd`のアセット内のページ内で、**Management**&#x200B;という語を検索します。

これは概念的に`fulltext AND ( (path AND type) OR (path AND type) )`です。 このようなOR結合は、パフォーマンス上の理由から適切なインデックスを必要とすることに注意してください。

#### プロパティ {#properties-6}

* **`p.or`**  — に設定した場合 `true`は、グループ内の1つの述語のみが一致する必要があります。デフォルトは`false`です。つまり、すべてが
* **`p.not`**  — に設定すると、グループ `true`を無効にします(デフォルトは `false`)。
* **`<predicate>`**  — ネストされた述語を追加します
* **`N_<predicate>`** -  `1_property, 2_property, ...`

### orderby {#orderby}

この述語は、結果を並べ替えることができます。 複数のプロパティで順序付けが必要な場合は、`1_orderby=first`、`2_oderby=second`のように、数値のプレフィックスを使用して、この述語を複数回追加する必要があります。

#### プロパティ {#properties-13}

* **`orderby`** - JCRプロパティ名の先頭に@が付いている名前(例：ま `@jcr:lastModified` たは `@jcr:content/jcr:title`)、またはクエリ内の別の述語(例：並べ替えの対象 `2_property`)
* **`sort`**  — 降順または昇順（デフォルト） `desc`  `asc` の並べ替え方向
* **`case`**  — をに設定すると、並べ替えで大文字と小文字が区別さ `ignore` れなくなります。つまり、前に `a` 来ま `B`す。空白または中止された場合、並べ替えでは大文字と小文字が区別されます。つまり、 `B`   `a`

## 述語 {#predicates}

### boolproperty {#boolproperty}

この述語は、JCRブール値プロパティと一致します。 `true`と`false`の値のみを受け入れます。 `false`の場合、プロパティの値が`false`であるか、値がまったく存在しない場合は、一致と見なされます。 有効になっている場合のみ設定されるブール型のフラグをチェックする際に便利です。

継承された`operation`パラメータは意味を持ちません。

この述語はファセット抽出をサポートし、`true`または`false`の値ごとにグループを提供しますが、既存のプロパティに対してのみ提供します。

#### プロパティ {#properties}

* **`boolproperty`**  — プロパティへの相対パス。例 `myFeatureEnabled` えば、  `jcr:content/myFeatureEnabled`
* **`value`**  — プロパティをチェックする値、 `true` または  `false`

### contentfragment {#contentfragment}

この述語は、結果をコンテンツフラグメントに制限します。

* フィルタリングはサポートされていません。
* ファセットの抽出には対応していません。

#### プロパティ {#properties-1}

* **`contentfragment`**  — 任意の値と組み合わせて使用して、コンテンツフラグメントを確認できます。

### `dateComparison` {#datecomparison}

この述語は、2つのJCR日付プロパティを比較します。 等しい、等しくない、より大きい、以上かどうかをテストできます。

これはフィルターのみの述語で、検索インデックスは利用できません。

#### プロパティ {#properties-2}

* **`property1`**  — 最初の日付プロパティへのパス
* **`property2`** - 2番目の日付プロパティへのパス
* **`operation`**
   * `=` 完全一致（デフォルト）
   * `!=` 不等価比較のため
   * `>` 次より `property1` 大きい  `property2`
   * `>=` 次の値 `property1` よりも大きいか等しい  `property2`

### daterange {#daterange}

この述語は、日付/時間間隔に対してJCRの日付プロパティを一致させます。 これはISO8601
日付と時間の形式(`YYYY-MM-DDTHH:mm:ss.SSSZ`)を指定し、`YYYY-MM-DD`のように部分的な表現も許可します。 あるいは、タイムスタンプをPOSIX時間として指定することもできます。

2 つのタイムスタンプの間や、特定の日付より前または後のものを検索できるほか、両値を含めるか含めないかを選択することもできます。

ファセット抽出をサポートし、グループ`today`、`this week`、`this month`、`last 3 months`、`this year`、`last year`および`earlier than last year`を提供します。

フィルタリングはサポートされていません。

#### プロパティ {#properties-3}

* **`property`** - `DATE` プロパティの相対パス（例：）  `jcr:lastModified`
* **`lowerBound`**  — 例えば、プロパティをチェックする日付の下限  `2014-10-01`
* **`lowerOperation`** -  `>` （新しい）または `>=` （新しい）は、に適用され `lowerBound`ます。デフォルトは です。`>`
* **`upperBound`**  — 例えば、プロパティをチェックする上限  `2014-10-01T12:15:00`
* **`upperOperation`** -  `<` （古い）または `<=` （古い）が適用され `upperBound`ます。デフォルトは です。`<`
* **`timeZone`** - ISO-8601日付文字列として指定されていない場合に使用するタイムゾーンのID。デフォルトは、システムのデフォルトのタイムゾーンです。

### excludepaths  {#excludepaths}

この述語は、パスが正規式と一致するノードを結果から除外します。

これはフィルターのみの述語で、検索インデックスは利用できません。

ファセットの抽出には対応していません。

#### プロパティ {#properties-4}

* **`excludepaths`**  — 結果パスに一致する正規式（結果パスから一致するものを除く）。

### fulltext {#fulltext}

この述語は、フルテキストインデックス内の用語を検索します。

フィルタリングはサポートされていません。

ファセットの抽出には対応していません。

#### プロパティ {#properties-5}

* **`fulltext`**  — 全文検索用語
* **`relPath`**  — プロパティまたはサブノードで検索する相対パス。このプロパティはオプションです。

### hasPermission {#haspermission}

この述語は、結果を、現在のセッションに指定された[JCR権限があるアイテムに制限します。](https://docs.adobe.com/content/docs/en/spec/jcr/2.0/16_Access_Control_Management.html#16.2.3%20Standard%20Privileges)

これはフィルターのみの述語で、検索インデックスは利用できません。ファセットの抽出には対応していません。

#### プロパティ {#properties-7}

* **`hasPermission`**  — 現在のユーザーセッションが、問題のノードに対してすべてが持つ必要があるJCR権限（カンマ区切り）。例えば、 `jcr:write`  `jcr:modifyAccessControl`

### language {#language}

この述語は、AEMページを特定の言語で検索します。 ページの言語プロパティと、ページパス（一般的に最上位レベルのサイト構造に言語やロケールが含まれています）の両方を検索します。

これはフィルターのみの述語で、検索インデックスは利用できません。

ファセット抽出をサポートし、各固有の言語コードのグループを提供します。

#### プロパティ {#properties-8}

* **`language`** - ISO言語コード例  `de`

### mainasset {#mainasset}

この述語は、ノードがDAMのメインアセットであり、サブアセットではないかどうかを確認します。 これは基本的にサブアセットノード内にないすべてのノードです。 `dam:Asset` ノードタイプはチェックされません。この述語を使用するには、`mainasset=true`または`mainasset=false`を設定します。 これ以上のプロパティはありません。

これはフィルターのみの述語で、検索インデックスは利用できません。

ファセットの抽出をサポートし、メインアセットとサブアセットに2つのグループを提供します。

#### プロパティ {#properties-9}

* **`mainasset`**  — メインアセット `true` の場合は、サブアセット `false` の場合はboolean

### memberOf {#memberof}

この述語は、特定の[スリングリソースコレクション](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/org/apache/sling/resource/collection/ResourceCollection.html)のメンバーである項目を検出します。

これはフィルターのみの述語で、検索インデックスは利用できません。

ファセットの抽出には対応していません。

#### プロパティ {#properties-10}

* **`memberOf`** - Slingリソース収集のパス

### nodename {#nodename}

この述語はJCRノード名と一致します。

ファセット抽出をサポートし、一意の各ノード名（ファイル名）のグループを提供します。

#### プロパティ {#properties-11}

* **`nodename`**  — ワイルドカードが使用できるノード名パターン： `*` =任意または文字なし、=任意の文字、 `?`  `[abc]` =角括弧内の文字のみ

### notexpired {#notexpired}

この述語は、JCRの日付プロパティが現在のサーバー時間より大きいか等しいかをチェックして項目を一致させます。 これは、`expiresAt`値をチェックし、有効期限が切れていない(`notexpired=true`)または期限が切れている(`notexpired=false`)値に結果を制限する場合に使用できます。

フィルタリングはサポートされていません。

[`daterange`](#daterange)述語と同様にファセット抽出をサポートします。

#### プロパティ {#properties-12}

* **`notexpired`**  — ブール値。まだ期限切 `true` れでない（未来の日付と等しい） `false` 、有効期限切れの（過去の日付）（必須）
* **`property`**  — 確認する `DATE` プロパティの相対パス（必須）

### パス {#path}

この述語は、指定されたパス内を検索します。

ファセットの抽出には対応していません。

#### プロパティ {#properties-14}

* **`path`**  — パスパターンを定義します。
   * `exact`プロパティに応じて、サブツリー全体が一致します（xpathに`//*`を付加する場合など）。ただし、これはベースパスを含まないことに注意してください)。または、完全一致のパスのみが一致し、ワイルドカード(`*`)を含めることができます。
      * デフォルト に設定`true`
   * `self`プロパティが設定されている場合は、ベースノードを含むサブツリー全体が検索されます。
* **`exact`**  — 一致 `exact` する場合、完全一致パスが一致する必要がありますが、一致する名前を含む単純なワイルドカード( `true`)を含めることはできますが、含めない`*` `/`;この値が `false` （デフォルト）の場合、すべての子孫が含まれます（オプション）
* **`flat`**  — 直接の子のみを検索します(xpath `/*` での追加など)(trueでない場合 `exact` にのみ使用され、オプション)
* **`self`**  — サブツリーを検索しますが、パスとして指定されたベースノードを含めます（ワイルドカードは使用できません）。

### property {#property}

この述語は、JCRプロパティとその値に一致します。

ファセット抽出をサポートし、結果の一意のプロパティ値ごとにグループを提供します。

#### プロパティ {#properties-15}

* **`property`**  — プロパティへの相対パス  `jcr:title`
* **`value`**  — プロパティをチェックする値；JCRプロパティタイプに従って文字列変換が行われます。
* **`N_value`** -  `1_value`、、 `2_value`、...を使用して、複数の値(デフォルトで `OR` はifと組み合わせて)をチェックします `AND`  `and=true`。
* **`and`**  — 複数の値( `true` `N_value`)を  `AND`
* **`operation`**
   * `equals` 完全一致（デフォルト）
   * `unequals` 不等価比較のため
   * `like` xpath関数の使用( `jcr:like` オプション)
   * `not` 一致しない場合(例： xpath `not(@prop)` では、value paramは無視されます)
   * `exists` 存在確認
      * `true` プロパティが存在する必要があります
      * `false` がと同じで、がデフォルト `not` です。
* **`depth`**  — プロパティ/相対パスが存在することのできるワイルドカードレベルの数(例えば、チェック `property=size depth=2` を行う `node/size`な `node/*/size` ど `node/*/*/size`)

### rangeproperty {#rangeproperty}

この述語は、JCRプロパティと間隔を一致させます。 これは、`LONG`、`DOUBLE`、`DECIMAL`などの線形型を持つプロパティに適用されます。 `DATE`[`daterange`](#daterange) に関しては、最適化された日付形式の入力情報を含む 述語を参照してください。

下限、上限またはその両方を定義できます。 下限と上限を個別に指定する場合は、小さいか等しい演算を指定することもできます。

ファセットの抽出には対応していません。

#### プロパティ {#properties-16}

* **`property`**  — プロパティの相対パス
* **`lowerBound`**  — プロパティのチェックに下限があります
* **`lowerOperation`** -  `>` （デフォルト）また `>=`は、  `lowerValue`
* **`upperBound`**  — プロパティをチェックする上限
* **`upperOperation`** -  `<` （デフォルト）また `<=`は、  `lowerValue`
* **`decimal`**  — チェック `true` されたプロパティのタイプが10進の場合

### relativedaterange {#relativedaterange}

この述語は、現在のサーバー時間に対する時間オフセットを使用して、`JCR DATE`プロパティと日時間間隔を一致させます。 ミリ秒値またはBugzilla構文`1s 2m 3h 4d 5w 6M 7y` （1秒、2分、3時間、4日、5週間、6か月、7年）を使用して`lowerBound`と`upperBound`を指定できます。 現在時間の前の負のオフセットを示す場合は、プリフィックス`-`を付けます。 `lowerBound`または`upperBound`のみを指定した場合、もう1つはデフォルトで`0`になり、現在の時刻を表します。

次に例を示します。

* `upperBound=1h` (そして `lowerBound`)次の時間に何も選択しない
* `lowerBound=-1d` (および `upperBound`)過去24時間の中から何も選択しない
* `lowerBound=-6M` 過去3 ～ 6か月の間に何かを `upperBound=-3M` 選択
* `lowerBound=-1500` に設定され、1500ミリ秒から5500ミリ秒の間の値が将来的に `upperBound=5500` 選択されます。
* `lowerBound=1d` そして明後日に `upperBound=2d` 何でも選択する

うるう年は考慮されず、すべての月が 30 日になる点にご注意ください。

フィルタリングはサポートされていません。

[`daterange`](#daterange)述語と同様にファセット抽出をサポートします。

#### プロパティ {#properties-17}

* **`upperBound`**  — 現在のサーバー時間を基準としたミリ秒または `1s 2m 3h 4d 5w 6M 7y` （1秒、2分、3時間、4日、5週間、6か月、7年）の上限の日付。負のオフセット `-` に使用します。
* **`lowerBound`**  — 現在のサーバー時間に対する日付範囲（ミリ秒、2分、3時間、4日、5週間、6か月、7年）がミリ秒または `1s 2m 3h 4d 5w 6M 7y` （1秒、2分、3時間、4日、5週間、6か月、7年）の範囲内で、負のオフセット `-` に使用

### savedquery {#savedquery}

この述語は、永続化されたクエリビルダークエリのすべての述語を、現在のクエリにサブグループ述語として含みます。

これによって追加のクエリが実行されることはありませんが、現在のクエリが拡張されます。

クエリは、`QueryBuilder#storeQuery()`を使用してプログラムで保持できます。 複数行の`String`プロパティまたは`nt:file`クエリを含む&lt;a1/>ノードの形式にすることができます。このノードには、Javaプロパティ形式のテキストファイルとしてノードを含めます。

保存されたクエリの述部に対するファセット抽出はサポートされません。

#### プロパティ {#properties-19}

* **`savedquery`**  — 保存されたクエリ(`String` プロパティまたは `nt:file` ノード)へのパス

### similar {#similar}

この述語は、JCR XPathの`rep:similar()`を使用した類似性検索です。

フィルターはサポートされず、ファセット抽出もサポートされません。

#### プロパティ {#properties-20}

* **`similar`**  — 類似のノードを探すノードの絶対パス
* **`local`**  — 子孫ノードまたは現在のノード `.` の相対パス(オプション、デフォルト `.`)

### tag {#tag}

この述語は、タグタイトルパスを指定して、1つ以上のタグでタグ付けされたコンテンツを検索します。

ファセット抽出をサポートし、現在のタグタイトルパスを使用して、一意の各タグにグループを提供します。

#### プロパティ {#properties-21}

* **`tag`**  — 検索するタイトルパス(例：  `properties:orientation/landscape`
* **`N_value`** -  `1_value`、、 `2_value`、...を使用して、複数のタグ(デフォルトで `OR` はifと組み合わされている)をチェックします `AND`  `and=true`。
* **`property`**  — 参照するプロパティ（またはプロパティへの相対パス）(デフォルト `cq:tags`)

### tagid {#tagid}

この述語は、タグIDを指定して、1つ以上のタグでタグ付けされたコンテンツを検索します。

ファセット抽出をサポートし、固有の各タグに対して、現在のタグIDを使用するグループを提供します。

#### プロパティ {#properties-22}

* **`tagid`**  — 検索するタグID（例：）  `properties:orientation/landscape`
* **`N_value`** -  `1_value`、、 `2_value`、...を使用して、複数のタグIDを確認します(デフォルトで、 `OR` ifと組み合わ `AND`  `and=true`せて使用)
* **`property`**  — 参照するプロパティ（またはプロパティへの相対パス）(デフォルト `cq:tags`)

### tagsearch {#tagsearch}

この述語は、1つ以上のタグでタグ付けされたコンテンツを、キーワードを指定して検索します。 これにより、まずタイトルにこれらのキーワードを含むタグが検索され、その結果がこれらのキーワードでタグ付けされた項目のみに制限されます。

ファセットの抽出には対応していません。

#### プロパティ {#Properties-1}

* **`tagsearch`**  — タグタイトルで検索するキーワード
* **`property`**  — 考慮するプロパティ（またはプロパティへの相対パス）(デフォルト `cq:tags`)
* **`lang`**  — 特定のローカライズされたタグタイトルのみを検索する場合(例： `de`)
* **`all`**  — タグ全体、つまりすべてのタイトル、説明などを検索するブール値（`lang`より優先）

### type {#type}

この述語は、結果を特定のJCRノードタイプ、両方のプライマリノードタイプまたはミックスインタイプに制限します。 また、このノードタイプのサブタイプも検索されます。 リポジトリの検索インデックスでは、効率的に実行できるノードタイプに対応する必要があります。

ファセット抽出をサポートし、結果内の一意の型ごとにグループを提供します。

#### プロパティ {#Properties-2}

* **`type`**  — 検索するノードタイプまたはmixin名。例：  `cq:Page`
