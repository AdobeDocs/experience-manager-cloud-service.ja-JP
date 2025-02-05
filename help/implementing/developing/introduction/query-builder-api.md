---
title: Query Builder API
description: アセット共有の Query Builder の機能は、Java API と REST API を通して公開されます。
exl-id: d5f22422-c9da-4c9d-b81c-ffa5ea7cdc87
feature: Developing
role: Admin, Architect, Developer
source-git-commit: 10580c1b045c86d76ab2b871ca3c0b7de6683044
workflow-type: tm+mt
source-wordcount: '1830'
ht-degree: 98%

---

# Query Builder API {#query-builder-api}

Query Builder を使用すると、AEM のコンテンツリポジトリへのクエリを簡単に実行できます。この機能は、Java™ API と REST API を通じて公開されます。この文書ではこれらの API について説明します。

サーバーサイド Query Builder（[`QueryBuilder`](https://developer.adobe.com/experience-manager/reference-materials/cloud-service/javadoc/com/day/cq/search/QueryBuilder.html)）はクエリの記述を受け入れ、XPath クエリを作成して実行します。必要に応じて、結果セットのフィルタリングや、ファセットの抽出も実行できます。

クエリの記述は、単に述語（[`Predicate`](https://developer.adobe.com/experience-manager/reference-materials/cloud-service/javadoc/com/day/cq/search/Predicate.html)）のセットです。例としては、XPath の `jcr:contains()` 関数に対応するフルテキスト述語などがあります。

各述語タイプに、1 つのエバリュエーターコンポーネント（[`PredicateEvaluator`](https://developer.adobe.com/experience-manager/reference-materials/cloud-service/javadoc/com/day/cq/search/eval/PredicateEvaluator.html)）があります。これらのコンポーネントは、XPath、フィルタリングおよびファセットの抽出に対してその特定の述語を処理する方法を理解しています。OSGi コンポーネントのランタイムによってプラグインされる、カスタムのエバリュエーターを作成するのは簡単です。

REST API は、JSON で送信される応答を使用して、HTTP 経由で同じ機能へのアクセスを提供します。

>[!NOTE]
>
>QueryBuilder API は、JCR API を使用して構築されます。また、OSGi バンドル内から JCR API を使用して、AEM JCR をクエリすることもできます。詳しくは、[JCR API を使用した Adobe Experience Manager データのクエリ](https://experienceleague.adobe.com/docs/experience-manager-65/developing/platform/query-builder/querybuilder-api.html?lang=ja)を参照してください。

## Gem セッション {#gem-session}

[AEM Gems](https://experienceleague.adobe.com/docs/events/experience-manager-gems-recordings/overview.html?lang=ja) は、Adobe Experience Manager を技術的に深く掘り下げるための、アドビのエキスパートによる各種セッションです。

[Query Builder 専用のセッションを確認](https://experienceleague.adobe.com/docs/events/experience-manager-gems-recordings/gems2017/aem-search-forms-using-querybuilder.html?lang=ja)し、ツールの概要と使用方法を確認できます。

## サンプルクエリ {#sample-queries}

以下のサンプルは、Java™ プロパティのスタイル表記法で示されています。これらのサンプルを Java™ API で使用するには、この後の API サンプルのように Java™ `HashMap` を使用します。

`QueryBuilder` JSON サーブレットの場合、各例には AEM インストールへのリンクの例が含まれています（デフォルトの場所：`http://<host>:<port>`）。これらのリンクを使用する前に、AEM インスタンスにログオンします。

>[!CAUTION]
>
>デフォルトでは、Query Builder JSON サーブレットは最大 10 件のヒットを表示します。
>
>次のパラメーターを追加すると、サーブレットですべてのクエリ結果を表示できます。
>
>`p.limit=-1`

>[!NOTE]
>
>返された JSON データをブラウザーで表示するのに、Firefox 用 JSONView などのプラグインを使用できます。

### すべての結果を返す {#returning-all-results}

以下のクエリは **10 件の結果を返します**（正確には最大 10 件）が、通知されるのは利用可能な&#x200B;**ヒット数**&#x200B;です。

`http://<host>:<port>/bin/querybuilder.json?path=/content&1_property=sling:resourceType&1_property.value=wknd/components/structure/page&1_property.operation=like&orderby=path`

```xml
path=/content
1_property=sling:resourceType
1_property.value=wknd/components/structure/page
1_property.operation=like
orderby=path
```

同じクエリで、パラメーター `p.limit=-1` を使用すると、**すべての結果が返されます**（インスタンスによっては非常に多くなることがあります）。

`http://<host>:<port>/bin/querybuilder.json?path=/content&1_property=sling:resourceType&1_property.value=wknd/components/structure/page&1_property.operation=like&orderby=path&p.limit=-1`

```xml
path=/content
1_property=sling:resourceType
1_property.value=wknd/components/structure/page
1_property.operation=like
p.limit=-1
orderby=path
```

### p.guessTotal を使用して結果を返す {#using-p-guesstotal-to-return-the-results}

`p.guessTotal` パラメーターの目的は、実用最小限の `p.offset` 値と `p.limit` 値を組み合わせることによって、表示できる適切な結果数を返すことです。このパラメーターを使用するメリットは、結果セットが大きい場合にパフォーマンスが向上することです。このパラメーターにより、総合計の計算（`result.getSize()` の呼び出しなど）と結果セット全体の読み込みが回避され、Oak エンジンおよびインデックスに至るまですべてが最適化されます。このプロセスは結果が 10 万件ある場合、実行時間とメモリ使用量の両方で大きな変化が見られる可能性があります。

このパラメーターのデメリットは、ユーザーには正確な合計が表示されないことです。ただし、常に最大 1000 まで読み取るよう、最小値を `p.guessTotal=1000` のように設定することもできます。この方法では、小さい結果セットの正確な合計が得られますが、結果セットがそれ以上となる場合は「およびそれ以上」しか表示できません。

以下のクエリに `p.guessTotal=true` を追加して、どのように機能するかを見てみましょう。

`http://<host>:<port>/bin/querybuilder.json?path=/content&1_property=sling:resourceType&1_property.value=wknd/components/structure/page&1_property.operation=like&p.guessTotal=true&orderby=path`

```xml
path=/content
1_property=sling:resourceType
1_property.value=wknd/components/structure/page
1_property.operation=like
p.guessTotal=true
orderby=path
```

このクエリは、`p.limit` のデフォルトである `10` 件の結果をオフセット `0` で返します。

```xml
"success": true,
"results": 10,
"total": 10,
"more": true,
"offset": 0,
```

数値を使用してカスタムの最大結果数までカウントアップすることもできます。上述と同じクエリを使用して、`p.guessTotal` の値を `50` に変更してみます。

`http://<host>:<port>/bin/querybuilder.json?path=/content&1_property=sling:resourceType&1_property.value=wknd/components/structure/page&1_property.operation=like&p.guessTotal=50&orderby=path`

このクエリは、同じデフォルトの制限である 10 件の結果をオフセット 0 で返しますが、表示されるのは最大 50 件の結果だけです。

```xml
"success": true,
"results": 10,
"total": 50,
"more": true,
"offset": 0,
```

### ページネーションの実装 {#implementing-pagination}

デフォルトでは、Query Builder はヒット数も通知します。正確な数を特定するためにアクセス制御を結果ごとに確認するので、結果のサイズによっては長い時間がかかることがあります。合計は、主としてエンドユーザー向け UI のページネーションの実装に使用されます。正確な数の特定には時間がかかることがあるので、guessTotal 機能を使用してページネーションを実装することをお勧めします。

例えば、この UI は以下の手法に適応できます。

* 100 以下の合計ヒット数の正確な数（[SearchResult.getTotalMatches()](https://developer.adobe.com/experience-manager/reference-materials/cloud-service/javadoc/com/day/cq/search/result/SearchResult.html#getTotalMatches) または `querybuilder.json` 応答の合計）を取得して表示します。
* `guessTotal` を、100 で Query Builder を呼び出すように設定します。

* 応答は、以下のような結果になります。

   * `total=43`、`more=false` - 合計ヒット数が 43 であることを意味します。UI には先頭ページの一部として 10 件の結果が表示され、続く 3 ページのページネーションが提供されます。この実装を使用して、「**43 件の結果が見つかりました**」のような説明テキストを表示することもできます。
   * `total=100`、`more=true` - 合計ヒット数が 100 を超え、正確な数が不明であることを意味します。UI には先頭ページの一部として 10 件の結果が表示され、続く 10 ページのページネーションが提供されます。この実装を使用して、「**100 件を超える結果が見つかりました**」のようなテキストを表示することもできます。ユーザーが次のページに移動すると、Query Builder への呼び出しによって `guessTotal` の制限と、`offset` パラメーターおよび `limit` パラメーターの制限が増やされます。

また、ユーザーインターフェイスが無限スクロールを使用する必要がある場合は、Query Builder によって正確なヒット数が特定されないように、`guessTotal` を使用します。

### jar ファイルを検索して新しい順に並べ替える {#find-jar-files-and-order-them-newest-first}

`http://<host>:<port>/bin/querybuilder.json?type=nt:file&nodename=*.jar&orderby=@jcr:content/jcr:lastModified&orderby.sort=desc`

```xml
type=nt:file
nodename=*.jar
orderby=@jcr:content/jcr:lastModified
orderby.sort=desc
```

### すべてのページを検索して最終変更日順で並べ替える {#find-all-pages-and-order-them-by-last-modified}

`http://<host>:<port>/bin/querybuilder.json?type=cq:Page&orderby=@jcr:content/cq:lastModified`

```xml
type=cq:Page
orderby=@jcr:content/cq:lastModified
```

### すべてのページを検索して最終変更日で降順に並べ替える {#find-all-pages-and-order-them-by-last-modified-but-descending}

`http://<host>:<port>/bin/querybuilder.json?type=cq:Page&orderby=@jcr:content/cq:lastModified&orderby.sort=desc`

```xml
type=cq:Page
orderby=@jcr:content/cq:lastModified
orderby.sort=desc
```

### フルテキスト検索（スコアで並べ替え） {#fulltext-search-ordered-by-score}

`http://<host>:<port>/bin/querybuilder.json?fulltext=Management&orderby=@jcr:score&orderby.sort=desc`

```xml
fulltext=Management
orderby=@jcr:score
orderby.sort=desc
```

### 特定のタグが付いたページの検索 {#search-for-pages-tagged-with-a-certain-tag}

`http://<host>:<port>/bin/querybuilder.json?type=cq:Page&tagid=wknd:activity/cycling&tagid.property=jcr:content/cq:tags`

```xml
type=cq:Page
tagid=wknd:activity/cycling
tagid.property=jcr:content/cq:tags
```

明確なタグ ID がわかっている場合は、例にあるように `tagid` 述語を使用します。

タグタイトルのパス（スペースなし）には、`tag` 述語を使用します。

前の例ではページ（`cq:Page` ノード）を検索しているので、`tagid.property` 述語にはそのノードからの相対パス（`jcr:content/cq:tags`）を使用します。デフォルトでは、`tagid.property` は `cq:tags` となります。

### 複数パスの検索（グループを使用） {#search-under-multiple-paths-using-groups}

`http://<host>:<port>/bin/querybuilder.json?fulltext=Experience&group.1_path=/content/wknd/us/en/magazine&group.2_path=/content/wknd/us/en/adventures&group.p.or=true`

```xml
fulltext=Experience
group.p.or=true
group.1_path=/content/wknd/us/en/magazine
group.2_path=/content/wknd/us/en/adventures
```

このクエリでは、クエリ内のサブ式を区切る役目を果たす「*グループ*」（`group`）を使用しているので、使用しています（標準的な表記法での括弧と同様）。例えば、前の例は、次のように、よりわかりやすいスタイルで表現することができます。

`"Experience" and ("/content/wknd/us/en/magazine" or "/content/wknd/us/en/adventures")`

例にあるグループの内部では、`path` 述語が複数回使用されています。この述語の 2 つのインスタンスの区別と順序付け（一部の述語では順序付けが必要）を行う場合は、述語にプレフィックス `N_` を付けます。`N` は順序を表すインデックスです。前の例では、こうして得られた述語は、`1_path` および `2_path` です。

`p.or` 内の `p` は特殊な区切り文字で、後に続くもの（このケースでは `or`）がグループの&#x200B;*パラメーター*&#x200B;であることを示します。これは、グループのサブ述語（`1_path` など）とは対照的です。

`p.or` が指定されない場合、すべての述語は AND で連結されます。つまり、各結果がすべての述語を満たすことが必要になります。

>[!NOTE]
>
>異なる述語に対してであっても、単一のクエリ内で同じ数値のプレフィックスを使用することはできません。

### プロパティの検索 {#search-for-properties}

`cq:template` プロパティを使用して、特定のテンプレートのすべてのページを検索できます。

`http://<host>:<port>/bin/querybuilder.json?property=cq%3atemplate&property.value=%2fconf%2fwknd%2fsettings%2fwcm%2ftemplates%2fadventure-page-template&type=cq%3aPageContent`

```xml
type=cq:PageContent
property=cq:template
property.value=/conf/wknd/settings/wcm/templates/adventure-page-template
```

ページ自身ではなく、ページの `jcr:content` ノードが返されるという欠点があります。この問題を解決するには、相対パスで検索します。

`http://<host>:<port>/bin/querybuilder.json?property=jcr%3acontent%2fcq%3atemplate&property.value=%2fconf%2fwknd%2fsettings%2fwcm%2ftemplates%2fadventure-page-template&type=cq%3aPage`

```xml
type=cq:Page
property=jcr:content/cq:template
property.value=/conf/wknd/settings/wcm/templates/adventure-page-template
```

### 複数のプロパティの検索 {#search-for-multiple-properties}

property 述語を複数回使用する場合、ここでも、数字のプレフィックスを付加する必要があります。

`http://<host>:<port>/bin/querybuilder.json?1_property=jcr%3acontent%2fcq%3atemplate&1_property.value=%2fconf%2fwknd%2fsettings%2fwcm%2ftemplates%2fadventure-page-template&2_property=jcr%3acontent%2fjcr%3atitle&2_property.value=Cycling%20Tuscany&type=cq%3aPage`

```xml
type=cq:Page
1_property=jcr:content/cq:template
1_property.value=/conf/wknd/settings/wcm/templates/adventure-page-template
2_property=jcr:content/jcr:title
2_property.value=Cycling Tuscany
```

### プロパティの複数の値の検索 {#search-for-multiple-property-values}

1 つのプロパティに対して複数の値を検索する場合（`"A" or "B" or "C"`）に、グループが大きくならないようにするには、`property` 述語に複数の値を指定します。

`http://<host>:<port>/bin/querybuilder.json?property=jcr%3atitle&property.1_value=Cycling%20Tuscany&property.2_value=Ski%20Touring&property.3_value=Whistler%20Mountain%20Biking`

```xml
property=jcr:title
property.1_value=Cycling Tuscany
property.2_value=Ski Touring
property.3_value=Whistler Mountain Biking
```

複数値を持つプロパティの場合、複数の値が一致することを必須にできます（`"A" and "B" and "C"`）。

`http://<host>:<port>/bin/querybuilder.json?property=jcr%3atitle&property.and=true&property.1_value=Cycling%20Tuscany&property.2_value=Ski%20Touring&property.3_value=Whistler%20Mountain%20Biking`

```xml
property=jcr:title
property.and=true
property.1_value=Cycling Tuscany
property.2_value=Ski Touring
property.3_value=Whistler Mountain Biking
```

## 返されるプロパティの絞り込み {#refining-what-is-returned}

デフォルトでは、QueryBuilder JSON サーブレットは検索結果内の各ノードに関するデフォルトのプロパティのセット（path、name、title など）を返します。返されるプロパティを制御するために、次のいずれかの操作を実行できます。

以下のように指定します

```xml
p.hits=full
```

すると、各ノードのすべてのプロパティが含まれるようになります。

`http://<host>:<port>/bin/querybuilder.json?p.hits=full&property=jcr%3atitle&property.value=Cycling%20Tuscany`

```xml
property=jcr:title
property.value=Cycling Tuscany
p.hits=full
```

以下を使用し、

```xml
p.hits=selective
```

取得するプロパティを次のように指定して

```xml
p.properties
```

スペースで区切ります。

`http://<host>:<port>/bin/querybuilder.json?p.hits=selective&p.properties=sling%3aresourceType%20jcr%3aprimaryType&property=jcr%3atitle&property.value=Cycling%20Tuscany`

```xml
property=jcr:title
property.value=Cycling Tuscany
p.hits=selective
p.properties=sling:resourceType jcr:primaryType
```

他に実行可能な方法として、Query Builder の応答に子ノードを含めることができます。以下のように指定します

```xml
p.nodedepth=n
```

ここで、`n` は、クエリが返すレベルの数です。子ノードが返されるようにするには、プロパティセレクターでそのように指定する必要があります。

```xml
p.hits=full
```

例：

`http://<host>:<port>/bin/querybuilder.json?p.hits=full&p.nodedepth=5&property=jcr%3atitle&property.value=Cycling%20Tuscany`

```xml
property=jcr:title
property.value=Cycling Tuscany
p.hits=full
p.nodedepth=5
```

## 述語の詳細 {#morepredicates}

述語の詳細については、[Query Builder の述語リファレンスのページ](query-builder-predicates.md)を参照してください。

[`PredicateEvaluator` クラスの Javadoc](https://developer.adobe.com/experience-manager/reference-materials/cloud-service/javadoc/com/day/cq/search/eval/PredicateEvaluator.html) も参照してください。これらのクラスの Javadoc ドキュメントには、使用できるプロパティのリストが含まれています。

クラス名のプレフィックス（[`SimilarityPredicateEvaluator`](https://developer.adobe.com/experience-manager/reference-materials/cloud-service/javadoc/com/day/cq/search/eval/SimilarityPredicateEvaluator.html) の `similar` など）は、クラスの&#x200B;*プリンシパルプロパティ*&#x200B;です。このプロパティは、クエリ内で使用する述語の名前（小文字で使用）でもあります。

このようなプリンシパルプロパティの場合は、クエリを短縮して、完全修飾バリアント `similar=/content/en` の代わりに `similar.similar=/content/en` を使用できます。完全修飾形式は、クラスのプリンシパルプロパティではないすべてのプロパティに対して使用する必要があります。

## Query Builder API の使用例 {#example-query-builder-api-usage}

```java
   String fulltextSearchTerm = "WKND";

    // create query description as hash map (simplest way, same as form post)
    Map<String, String> map = new HashMap<String, String>();

// create query description as hash map (simplest way, same as form post)
    map.put("path", "/content");
    map.put("type", "cq:Page");
    map.put("group.p.or", "true"); // combine this group with OR
    map.put("group.1_fulltext", fulltextSearchTerm);
    map.put("group.1_fulltext.relPath", "jcr:content");
    map.put("group.2_fulltext", fulltextSearchTerm);
    map.put("group.2_fulltext.relPath", "jcr:content/@cq:tags");

    // can be done in map or with Query methods
    map.put("p.offset", "0"); // same as query.setStart(0) below
    map.put("p.limit", "20"); // same as query.setHitsPerPage(20) below

    Query query = builder.createQuery(PredicateGroup.create(map), session);
    query.setStart(0);
    query.setHitsPerPage(20);

    SearchResult result = query.getResult();

    // paging metadata
    int hitsPerPage = result.getHits().size(); // 20 (set above) or lower
    long totalMatches = result.getTotalMatches();
    long offset = result.getStartIndex();
    long numberOfPages = totalMatches / 20;

    //Place the results in XML to return to client
    DocumentBuilderFactory factory = DocumentBuilderFactory.newInstance();
    DocumentBuilder builder = factory.newDocumentBuilder();
    Document doc = builder.newDocument();

    //Start building the XML to pass back to the AEM client
    Element root = doc.createElement( "results" );
    doc.appendChild( root );

    // iterating over the results
for (Hit hit : result.getHits()) {
       String path = hit.getPath();

      //Create a result element
      Element resultel = doc.createElement( "result" );
      root.appendChild( resultel );

      Element pathel = doc.createElement( "path" );
      pathel.appendChild( doc.createTextNode(path ) );
      resultel.appendChild( pathel );
    }
```

同じクエリが、Query Builder（JSON）サーブレットを使用して HTTP を介して実行されます。

`http://<host>:<port>/bin/querybuilder.json?path=/content&type=cq:Page&group.p.or=true&group.1_fulltext=WKND&group.1_fulltext.relPath=jcr:content&group.2_fulltext=WKND&group.2_fulltext.relPath=jcr:content/@cq:tags&p.offset=0&p.limit=20`

## クエリの保存と読み込み {#storing-and-loading-queries}

クエリはリポジトリーに保存して後で使用することができます。`QueryBuilder` には次のシグネチャを持つ `storeQuery` メソッドがあります。

```java
void storeQuery(Query query, String path, boolean createFile, Session session) throws RepositoryException, IOException;
```

[`QueryBuilder#storeQuery`](https://developer.adobe.com/experience-manager/reference-materials/cloud-service/javadoc/com/day/cq/search/QueryBuilder.html#storeQuery-com.day.cq.search.Query-java.lang.String-boolean-javax.jcr.Session-) メソッドを使用すると、指定した `Query` が、`createFile` 引数の値に応じてファイルまたはプロパティとしてリポジトリーに保存されます。次の例に、`Query` をファイルとしてパス `/mypath/getfiles` に保存する方法を示します。

```java
builder.storeQuery(query, "/mypath/getfiles", true, session);
```

以前に保存したクエリはすべて、[`QueryBuilder#loadQuery`](https://developer.adobe.com/experience-manager/reference-materials/cloud-service/javadoc/com/day/cq/search/QueryBuilder.html#loadQuery-java.lang.String-javax.jcr.Session-) メソッドを使用してリポジトリーから読み込むことができます。

```java
Query loadQuery(String path, Session session) throws RepositoryException, IOException
```

例えば、パス `/mypath/getfiles` に保存された `Query` は、次のコードによって読み込むことができます。

```java
Query loadedQuery = builder.loadQuery("/mypath/getfiles", session);
```

## テストとデバッグ {#testing-and-debugging}

Query Builder のクエリを試してみたり、デバッグしたりする場合は、次の URL にアクセスして、Query Builder Debugger コンソールを使用できます。

`http://<host>:<port>/libs/cq/search/content/querydebug.html`

または、次の URL にアクセスして、Query Builder JSON サーブレットを使用できます。

`http://<host>:<port>/bin/querybuilder.json?path=/tmp`

`path=/tmp` は一例にすぎません。

### デバッグに関する一般的なレコメンデーション {#general-debugging-recommendations}

### ログから説明可能な XPath を取得する {#obtain-explain-able-xpath-via-logging}

開発サイクルでは、設定されたターゲットインデックスに対して、**すべての**&#x200B;クエリの説明を実行します。

1. QueryBuilder の DEBUG ログを有効にして、基になる説明可能な XPath クエリを取得します。
   * `https://<host>:<port>/system/console/slinglog` に移動します。**DEBUG** に、`com.day.cq.search.impl.builder.QueryImpl` の新しいロガーを作成します。
1. 上述のクラスで DEBUG を有効にすると、Query Builder で生成された XPath がログに表示されます。
1. 関連する Query Builder クエリのログエントリから XPath クエリをコピーします。以下に例を示します。
   * `com.day.cq.search.impl.builder.QueryImpl XPath query: /jcr:root/content//element(*, cq:Page)[(jcr:contains(jcr:content, "WKND") or jcr:contains(jcr:content/@cq:tags, "WKND"))]`
1. クエリ計画を取得するための XPath として、XPath クエリをクエリの説明に貼り付けます。

### Query Builder Debugger を使用して説明可能な XPath を取得する {#obtain-explain-able-xpath-via-the-query-builder-debugger}

AEM Query Builder Debugger を使用して、説明可能な XPath クエリを生成します。

![Query Builder Debugger](assets/query-builder-debugger.png)

1. Query Builder Debugger で Query Builder クエリを指定します。
1. 検索を実行します。
1. 生成された XPath を取得します。
1. クエリ計画を取得するための XPath として、XPath クエリをクエリの説明に貼り付けます。

>[!NOTE]
>
>Query Builder 以外のクエリ（XPath、JCR-SQL2）は、クエリの説明を実行に直接指定できます。

## ログ出力付きのクエリのデバッグ {#debugging-queries-with-logging}

>[!NOTE]
>
>ロガーの設定は、ドキュメント「[ロギング](/help/implementing/developing/introduction/logging.md)」に記述されています。

前の節（テストとデバッグ [ で説明したクエリの実行時における Query Builder 実装のログ出力（情報レベル ](#testing-and-debugging)

```xml
com.day.cq.search.impl.builder.QueryImpl executing query (predicate tree):
null=group: limit=20, offset=0[
    {group=group: or=true[
        {1_fulltext=fulltext: fulltext=WKND, relPath=jcr:content}
        {2_fulltext=fulltext: fulltext=WKND, relPath=jcr:content/@cq:tags}
    ]}
    {path=path: path=/content}
    {type=type: type=cq:Page}
]
com.day.cq.search.impl.builder.QueryImpl XPath query: /jcr:root/content//element(*, cq:Page)[(jcr:contains(jcr:content, "WKND") or jcr:contains(jcr:content/@cq:tags, "WKND"))]
com.day.cq.search.impl.builder.QueryImpl no filtering predicates
com.day.cq.search.impl.builder.QueryImpl query execution took 69 ms
```

フィルタリングを行う述語エバリュエーターや、コンパレーターでカスタム順序を使用する述語エバリュエーターを使用するクエリがある場合は、クエリ内にそのことも記述されます。

```xml
com.day.cq.search.impl.builder.QueryImpl executing query (predicate tree):
null=group: [
    {nodename=nodename: nodename=*.jar}
    {orderby=orderby: orderby=@jcr:content/jcr:lastModified}
    {type=type: type=nt:file}
]
com.day.cq.search.impl.builder.QueryImpl custom order by comparator: jcr:content/jcr:lastModified
com.day.cq.search.impl.builder.QueryImpl XPath query: //element(*, nt:file)
com.day.cq.search.impl.builder.QueryImpl filtering predicates: {nodename=nodename: nodename=*.jar}
com.day.cq.search.impl.builder.QueryImpl query execution took 272 ms
```

## Javadoc リンク {#javadoc-links}

| **Javadoc** | **説明** |
|---|---|
| [com.day.cq.search](https://developer.adobe.com/experience-manager/reference-materials/cloud-service/javadoc/com/day/cq/search/package-summary.html) | 基本 Query Builder とクエリ API |
| [com.day.cq.search.result](https://developer.adobe.com/experience-manager/reference-materials/cloud-service/javadoc/com/day/cq/search/result/package-summary.html) | Result API |
| [com.day.cq.search.facets](https://developer.adobe.com/experience-manager/reference-materials/cloud-service/javadoc/com/day/cq/search/facets/package-summary.html) | ファセット |
| [com.day.cq.search.facets.buckets](https://developer.adobe.com/experience-manager/reference-materials/cloud-service/javadoc/com/day/cq/search/facets/buckets/package-summary.html) | バケット（ファセット内に含まれる） |
| [com.day.cq.search.eval](https://developer.adobe.com/experience-manager/reference-materials/cloud-service/javadoc/com/day/cq/search/eval/package-summary.html) | 述語エバリュエーター |
| [com.day.cq.search.facets.extractors](https://developer.adobe.com/experience-manager/reference-materials/cloud-service/javadoc/com/day/cq/search/facets/extractors/package-summary.html) | ファセット抽出（エバリュエーター用） |
| [com.day.cq.search.writer](https://developer.adobe.com/experience-manager/reference-materials/cloud-service/javadoc/com/day/cq/search/writer/package-summary.html) | Query Builder サーブレット用の JSON Result Hit Writer（`/bin/querybuilder.json`） |
