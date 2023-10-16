---
title: クエリとインデックス作成のベストプラクティス
description: アドビのベストプラクティスガイドラインに基づいてインデックスとクエリを最適化する方法を説明します。
topic-tags: best-practices
exl-id: 37eae99d-542d-4580-b93f-f454008880b1
source-git-commit: ddd67a69bea2e2109ce93a91f42e8f365424f80f
workflow-type: tm+mt
source-wordcount: '3144'
ht-degree: 46%

---

# クエリとインデックス作成のベストプラクティス {#query-and-indexing-best-practices}

AEM as a Cloud Service では、インデックス作成に関わる様々な操作はすべて自動化されています。これにより、開発者は効率的なクエリの作成とそれに対応するインデックスの定義に専念できます。

## クエリを使用する場面 {#when-to-use-queries}

クエリを使用するとコンテンツにアクセスできますが、唯一の手段ではありません。多くの場合、他の手段でもより効率的にリポジトリ内のコンテンツにアクセスできます。クエリが使用例のコンテンツにアクセスするための最善かつ最も効率的な方法であるかどうかを検討する必要があります。

### リポジトリと分類の設計 {#repository-and-taxonomy-design}

リポジトリの分類を設計する際は、いくつかの要素を考慮する必要があります。考慮すべき点には、アクセス制御、ローカリゼーション、コンポーネント、ページプロパティの継承などが含まれます。

こうした事柄に対応する分類を設計する一方で、インデックス設計の「トラバーサビリティ」についても検討することも重要です。ここで、トラバーサビリティとは、パスに基づいて予測どおりにコンテンツにアクセスできる、分類が持つ能力のことです。これにより、より効率的なシステムが実現し、複数のクエリを実行する必要があるシステムよりも保守が容易になります。

さらに分類を設計する際は、順序が重要かどうか検討することが重要です。明確な順序が不要な場合および多数の兄弟ノードが予想される場合は、`sling:Folder` や `oak:Unstructured` などの順序がないノードタイプを使用することを推奨します。順序付けが必要な場合は、`nt:unstructured` および `sling:OrderedFolder` の方が適切です。

### コンポーネント内のクエリ {#queries-in-components}

クエリは、AEM システムで実行される際の負荷が比較的大きい処理なので、コンポーネント内のクエリはできる限り避けるようにします。ページがレンダリングされるたびに複数のクエリを実行すると、システムのパフォーマンス低下につながります。コンポーネントのレンダリング時にクエリが実行されることを回避するには、**[ノードの走査](#traversing-nodes)**&#x200B;と&#x200B;**[結果の先取り](#prefetching-results)**&#x200B;という 2 つの方法があります。

### ノードの走査 {#traversing-nodes}

必要なデータの場所を事前に把握できるようにリポジトリを設計している場合は、必要なパスからこのデータを取得するコードをデプロイできます。クエリを実行して検索する必要はありません。

例として考えられるのは、特定のカテゴリに適合するコンテンツをレンダリングする場合です。これを実現する 1 つの方法は、コンテンツをカテゴリプロパティで整理し、このプロパティをクエリして、カテゴリ内のアイテムを表示するコンポーネントに割り当てることです。

もっと良い方法は、コンテンツをカテゴリ別の分類で構造化し、コンテンツを手動で取得できるようにすることです。

例えば、コンテンツが以下の場所に似た分類で格納されている場合は、

```xml
/content/myUnstructuredContent/parentCategory/childCategory/contentPiece
```

`/content/myUnstructuredContent/parentCategory/childCategory` ノードは簡単に取得でき、その子ノードを解析してコンポーネントのレンダリングに使用できます。

さらに、小規模または一様なデータセットを扱う場合は、同じ結果セットを返すためにクエリを作成するよりも、リポジトリを走査して必要なノードを収集するほうが速い場合があります。一般論として、クエリはできる限り使用せずに済ませることを推奨します。

### 結果の先取り {#prefetching-results}

コンテンツやコンポーネントの要件によっては、必要なデータを取得する方法としてノードの走査を使用できない場合があります。このような場合は、最適なパフォーマンスを保証するために、コンポーネントがレンダリングされる前に必要なクエリを実行する必要があります。

コンポーネントで必要とされる結果をオーサリング時にまとめて計算でき、さらにコンテンツがその後も変更されないとわかっている場合は、変更が行われた後にクエリを実行できます。

データまたはコンポーネントが定期的に変更される場合は、スケジュールに従って、または基礎データの更新リスナーを使用してクエリを実行できます。クエリの結果は、リポジトリ内の共有の場所に書き込むことができます。このデータを必要とするコンポーネントは、実行時にクエリを実行しなくても、この 1 つのノードから値を取り出すことが可能です。

同様の方法を使用して、メモリ内キャッシュに結果を保持することができ、起動時にデータが取り込まれ、変更が行われるたびに更新されるようにできます（JCR `ObservationListener` または Sling `ResourceChangeListener` を使用）。

## クエリの最適化 {#optimizing-queries}

Oak ドキュメントでは、[クエリの実行方法の概要が説明されています。](https://jackrabbit.apache.org/oak/docs/query/query-engine.html#query-processing) これは、このドキュメントで説明するすべての最適化アクティビティの基礎となります。

AEMas a Cloud Service [クエリパフォーマンスツール](#query-performance-tool)：効率的なクエリの実装をサポートするように設計されています。

* 実行済みのクエリと、関連するパフォーマンス特性およびクエリプランが表示されます。
* クエリプランの表示から完全なクエリの実行まで、様々なレベルでアドホッククエリを実行できます。

クエリパフォーマンスツールは、Cloud Manager の[開発者コンソールからアクセスできます。](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/debugging/debugging-aem-as-a-cloud-service/developer-console.html?lang=ja#queries) AEM as a Cloud Service のクエリパフォーマンスツールでは、AEM 6.x バージョンに対するクエリの実行に関する詳細が提供されます。

このグラフは、クエリパフォーマンスツールを使用してクエリを最適化するための一般的なフローを示しています。

![クエリ最適化フロー](assets/query-optimization-flow.png)

### インデックスの使用 {#use-an-index}

最適なパフォーマンスを実現するには、すべてのクエリでインデックスを使用する必要があります。ほとんどの場合、既存の標準提供インデックスで十分クエリを処理することができます。

時には、既存のインデックスにカスタムプロパティを追加する必要があり、インデックスを使用して追加の制約をクエリできるようになります。詳しくは、[コンテンツ検索とインデックス作成](/help/operations/indexing.md#changing-an-index)のドキュメントを参照してください。The [JCR クエリのチートシート](#jcr-query-cheatsheet) このドキュメントの節では、特定のクエリタイプをサポートするために、インデックスのプロパティ定義をどのように参照する必要があるかを説明します。

### 適切な条件を使用 {#use-the-right-criteria}

クエリの主な制約は、プロパティの一致である必要があり、これは最も効率的なタイプであるためです。プロパティ制約をさらに追加すると、結果をさらに絞り込めます。

クエリエンジンは単一のインデックスのみを考慮します。つまり、既存のインデックスは、カスタムインデックスプロパティをさらに追加することでカスタマイズでき、またそうする必要があります。

このドキュメントの [JCR クエリのチートシート](#jcr-query-cheatsheet)セクションでは、使用可能な制約を一覧表示し、インデックス定義が検出されるためにどのように見える必要があるかを説明します。[クエリパフォーマンスツール](#query-performance-tool)を使用してクエリをテストし、適切なインデックスが使用され、クエリエンジンがインデックス外の制約を評価する必要がないことを確認します。

### 順序 {#ordering}

結果が特定の順序で要求される場合、クエリエンジンでこれを実現するには、次の 2 つの方法があります。

1. インデックスは、結果を完全に正しい順序で提供できます。
   * これが機能するのは、順序付けに使用されるプロパティがインデックス定義において `ordered=true` で注釈付けされている場合です。
1. クエリエンジンが順序付けプロセスを実行します。
   * これは、クエリエンジンがインデックスの外部でフィルタリングを実行したり、または順序プロパティが `ordered=true` プロパティで注釈付けされてない場合に発生する可能性があります。
   * この場合、結果セット全体が並べ替えのためにメモリに読み込まれる必要があり、最初のオプションよりはるかに時間がかかります。

### 結果のサイズを制限 {#restrict-result-size}

クエリ結果の取得サイズは、クエリパフォーマンスの重要な要因です。結果は遅延的に取得されるので、最初の 20 件の結果の取得と 10,000 件の結果の取得を比較すると、ランタイムとメモリ使用量ともに違いが生じます。

つまり、結果セットのサイズは、すべての結果が取得された場合にのみ正しく判断できます。このため、取得する結果セットは、クエリを拡張するか（詳しくはこのドキュメントの [JCR クエリのチートシート](#jcr-query-cheatsheet)の節を参照）、または結果の読み取りを制限することで、常に制限する必要があります。

このような制限は、クエリエンジンが 100,000 のノードの&#x200B;**トラバーサルの制限**&#x200B;に達することを防ぎ、クエリを強制的に停止します。

の節を参照してください。 [大きな結果セットを持つクエリ](#queries-with-large-result-sets) を参照してください。

## クエリパフォーマンスツール {#query-performance-tool}

クエリパフォーマンスツール ( `/libs/granite/operations/content/diagnosistools/queryPerformance.html` およびは、 [Cloud Manager の開発者コンソール](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/debugging/debugging-aem-as-a-cloud-service/developer-console.html?lang=ja#queries)) には、次が含まれます。
* 「スロークエリ」のリスト。現在、5,000 行を超える読み取り/スキャンとして定義されています。
* 「一般的なクエリ」のリスト
* Oak による特定のクエリの実行方法を理解するための「クエリの説明を実行」ツール。

![クエリパフォーマンスツール](assets/query-performance-tool.png)

「低速クエリ」および「頻度の高いクエリ」テーブルには、次が含まれます。
* クエリ文自体。
* クエリを実行した最後のスレッドの詳細。クエリを実行するページまたはアプリケーション機能を識別できます。
* クエリの「最適化を読み取り」スコア。
   * これは、クエリを実行するためにスキャンされた行数/ノード数と読み取られた一致結果数の比率として計算されます。
   * インデックスですべての制限（および任意の順序）を処理できるクエリでは、通常、90%以上のスコアが割り当てられます。
* 最大行数の詳細 —
   * 読み取り — 行が結果セットの一部として含まれたことを示します。
   * スキャン — 基になるインデックスクエリの結果に行が含まれていた（インデックスクエリの場合）か、ノードストアから読み取られた（リポジトリトラバーサルの場合）ことを示します。

これらのテーブルは、完全にインデックス化されていないクエリを識別するのに役立ちます ( [インデックスの使用](#use-an-index) または読み込みが多すぎるノード ( [リポジトリトラバーサル](#repository-traversal) および [インデックストラバーサル](#index-traversal)) をクリックします。 このようなクエリは、赤でマークされた適切な問題領域と共に、ハイライト表示されます。

The `Reset Statistics` 」オプションが指定され、テーブルで収集された既存の統計をすべて削除します。 これにより、特定のクエリ（アプリケーション自体またはクエリの説明を実行ツールを使用）を実行し、実行統計を分析できます。

### クエリの説明を実行

クエリの説明を実行ツールを使用すると、開発者はクエリ実行計画を理解できます ( [クエリ実行プランの読み取り](#reading-query-execution-plan)) には、クエリの実行時に使用されるインデックスの詳細が含まれます。 これは、クエリのパフォーマンスを遡及的に予測または分析するために、クエリがどの程度効果的にインデックス付けされているかを理解するために使用できます。

#### クエリの説明

クエリに説明を付けるには、次の手順を実行します。
* 適切なクエリ言語を `Language` ドロップダウン。
* クエリ文を `Query` フィールドに入力します。
* 必要に応じて、提供されたチェックボックスを使用して、クエリを実行する方法を選択します。
   * デフォルトでは、クエリ実行計画を識別するために JCR クエリを実行する必要はありません（QueryBuilder クエリの場合は実行されません）。
   * クエリを実行するための 3 つのオプションが用意されています。
      * `Include Execution Time`  — クエリを実行しますが、結果を読み込もうとしません。
      * `Read first page of results`  — クエリを実行し、20 件の結果の最初の「ページ」を読み取ります（クエリを実行するためのベストプラクティスを複製します）。
      * `Include Node Count`  — クエリを実行し、結果セット全体を読み取ります ( 通常、これはお勧めしません。 [インデックストラバーサル](#index-traversal)) をクリックします。

#### クエリの説明ポップアップ {#query-explanation-popup}

![クエリの説明ポップアップ](./assets/query-explanation-popup.png)

選択後 `Explain`を指定した場合、ユーザーには、クエリの説明の結果（および選択されている場合は実行）を説明するポップアップが表示されます。
このポップアップには、次の詳細が含まれます。
* クエリの実行時に使用されるインデックス（クエリを使用して実行する場合はインデックスなし） [リポジトリトラバーサル](#repository-traversal)) をクリックします。
* 実行時間 ( `Include Execution Time` チェックボックスがオンの場合 ) および読み取った結果の数 ( `Read first page of results` または `Include Node Count` チェックボックスがオンになっている )。
* 実行プラン（クエリの実行方法を詳細に分析できます）。詳しくは、 [クエリ実行プランの読み取り](#reading-query-execution-plan) この解釈の仕方に関して
* 最初の 20 件のクエリ結果のパス ( `Read first page of results` チェックボックスはオンになっています )。
* クエリ計画の完全なログ。このクエリの実行で考慮されたインデックスの相対コストが表示されます（コストが最も低いインデックスが選択されます）。

#### クエリ実行プランの読み取り {#reading-query-execution-plan}

クエリ実行プランには、特定のクエリのパフォーマンスを予測（または説明）するために必要なすべてが含まれています。 元の JCR（または Query Builder）クエリでの制限と順序を、基になるインデックス（Lucene、Elastic、または Property）で実行されるクエリと比較することで、クエリがどの程度効率的に実行されるかを把握します。

次のクエリについて考えてみます。

```
/jcr:root/content/dam//element(*, dam:Asset) [jcr:content/metadata/dc:title = "My Title"] order by jcr:created
```

...次を含む —
* 3 制限
   * ノードタイプ (`dam:Asset`)
   * パス（の子孫） `/content/dam`)
   * プロパティ (`jcr:content/metadata/dc:title = "My Title"`)
* による並べ替え `jcr:created` プロパティ

このクエリを説明すると、次のプランが作成されます。

```
[dam:Asset] as [a] /* lucene:damAssetLucene-9(/oak:index/damAssetLucene-9) +:ancestors:/content/dam +jcr:content/metadata/dc:title:My Title ordering:[{ propertyName : jcr:created, propertyType : UNDEFINED, order : ASCENDING }] where ([a].[jcr:content/metadata/dc:title] = 'My Title') and (isdescendantnode([a], [/content/dam])) */
```

このプラン内では、基になるインデックスで実行されるクエリを説明する節は — です。

```
lucene:damAssetLucene-9(/oak:index/damAssetLucene-9) +:ancestors:/content/dam +jcr:content/metadata/dc:title:My Title ordering:[{ propertyName : jcr:created, propertyType : UNDEFINED, order : ASCENDING }]
```

プランのこのセクションには次の内容が含まれます。
* インデックスは、このクエリの実行に使用されます —
   * この場合、Lucene インデックス `/oak:index/damAssetLucene-9` が使用されるので、残りの情報は Lucene クエリ構文で示します。
* 3 つの制限はすべてインデックスによって処理されます —
   * ノードタイプの制限
      * 暗黙的な理由は、 `damAssetLucene-9` dam:Asset タイプのノードのみインデックスを作成します。
   * パスの制限
      * 理由： `+:ancestors:/content/dam` が Lucene クエリに表示されます。
   * プロパティの制限
      * 理由： `+jcr:content/metadata/dc:title:My Title` が Lucene クエリに表示されます。
* 順序は、インデックスによって処理されます
   * 理由： `ordering:[{ propertyName : jcr:created, propertyType : UNDEFINED, order : ASCENDING }]`  が Lucene クエリに表示されます。

インデックスクエリから返された結果は（アクセス制御フィルタリング以外に）クエリエンジンでさらにフィルタリングされないので、このようなクエリは正常に実行される可能性が高くなります。 ただし、ベストプラクティスに従っていない場合は、このようなクエリの実行に時間がかかる可能性があります。詳しくは、 [インデックストラバーサル](#index-traversal) 下

別のクエリの検討 —

```
/jcr:root/content/dam//element(*, dam:Asset) [jcr:content/metadata/myProperty = "My Property Value"] order by jcr:created
```

...次を含む —
* 3 制限
   * ノードタイプ (`dam:Asset`)
   * パス（の子孫） `/content/dam`)
   * プロパティ (`jcr:content/metadata/myProperty = "My Property Value"`)
* による並べ替え `jcr:created` property**

このクエリを説明すると、次のプランが作成されます。

```
[dam:Asset] as [a] /* lucene:damAssetLucene-9-custom-1(/oak:index/damAssetLucene-9-custom-1) :ancestors:/content/dam ordering:[{ propertyName : jcr:created, propertyType : UNDEFINED, order : ASCENDING }] where ([a].[jcr:content/metadata/myProperty] = 'My Property Value') and (isdescendantnode([a], [/content/dam])) */
```

このプラン内では、基になるインデックスで実行されるクエリを説明する節は — です。

```
lucene:damAssetLucene-9(/oak:index/damAssetLucene-9) :ancestors:/content/dam ordering:[{ propertyName : jcr:created, propertyType : UNDEFINED, order : ASCENDING }]
```

プランのこのセクションには次の内容が含まれます。
* （3 つのうち）2 つの制限のみがインデックスで処理されます —
   * ノードタイプの制限
      * 暗黙的な理由は、 `damAssetLucene-9` dam:Asset タイプのノードのみインデックスを作成します。
   * パスの制限
      * 理由： `+:ancestors:/content/dam` が Lucene クエリに表示されます。
* プロパティの制限 `jcr:content/metadata/myProperty = "My Property Value"` がインデックスで実行されるのではなく、基になる Lucene クエリの結果に対するフィルタリングとしてクエリエンジンとして適用されます。
   * これは、 `+jcr:content/metadata/myProperty:My Property Value` は Lucene クエリに表示されません。このプロパティは `damAssetLucene-9` このクエリに使用するインデックス。

このクエリ実行プランでは、 `/content/dam` インデックスから読み込まれ、クエリエンジンによってさらにフィルタリングされます（結果セットにインデックスなしのプロパティ制限に一致するもののみが含まれます）。

制限に一致するアセットがごく一部の場合でも `jcr:content/metadata/myProperty = "My Property Value"`に値を指定しない場合、要求された「ページ」の結果を満たすために（試行して）多数のノードを読み取る必要があります。 その結果、クエリのパフォーマンスが低下し、クエリのパフォーマンスが低下する可能性があります `Read Optimization` スコアを割り当ててクエリパフォーマンスツールに表示 )、大量のノードがトラバースされていることを示す WARN メッセージが表示される場合があります ( [インデックストラバーサル](#index-traversal)) をクリックします。

この 2 番目のクエリのパフォーマンスを最適化するには、 `damAssetLucene-9` インデックス (`damAssetLucene-9-custom-1`) をクリックし、次のプロパティ定義を追加します。

```
"myProperty": {
  "jcr:primaryType": "nt:unstructured",
  "propertyIndex": true,
  "name": "jcr:content/metadata/myProperty"
}
```

## JCR Query Cheat Sheet {#jcr-query-cheatsheet}

効率的な JCR クエリとインデックス定義を作成できるようにするため、開発時に [JCR クエリチートシート](https://experienceleague.adobe.com/docs/experience-manager-65/deploying/practices/best-practices-for-queries-and-indexing.html?lang=ja#jcrquerycheatsheet)をダウンロードして参照用として使用できます。

これには QueryBuilder、XPath、SQL-2 のクエリの例が収録されていて、クエリのパフォーマンスの点で異なる動作をする複数のシナリオに対応できます。また、Oak インデックスの作成またはカスタマイズ方法に関するレコメンデーションも収録されています。このチートシートの内容は、AEM as a Cloud ServiceおよびAEM 6.5 に適用されます。

## インデックス定義のベストプラクティス {#index-definition-best-practices}

インデックスを定義または拡張する際に考慮すべきベストプラクティスを以下に示します。

* 既存のインデックスを持つノードタイプ ( `dam:Asset` または `cq:Page`) は、新しいインデックスの追加よりも OOTB インデックスの拡張を優先します。
   * 新しいインデックス（特にフルテキストインデックス）を `dam:Asset` nodetype は非推奨 ( [このメモ](/help/operations/indexing.md##index-names-index-names)) をクリックします。
* 新しいインデックスを追加する場合
   * 常に「lucene」タイプのインデックスを定義します。
   * インデックス定義（および関連するクエリ）での index タグの使用 `selectionPolicy = tag` を使用して、インデックスが意図されたクエリに対してのみ使用されるようにします。
   * 確認 `queryPaths` および `includedPaths` の両方が提供されます（通常、同じ値を持ちます）。
   * 用途 `excludedPaths` をクリックして、役に立つ結果を含まないパスを除外します。
   * 用途 `analyzed` プロパティは、必要な場合にのみ使用します。例えば、そのプロパティに対してフルテキストクエリ制限を使用する必要がある場合などです。
   * 常に指定 `async = [ async, nrt ] `, `compatVersion = 2` および `evaluatePathRestrictions = true`.
   * 指定のみ `nodeScopeIndex = true` ノードスコープのフルテキストインデックスが必要な場合。

>[!NOTE]
>
>詳しくは、 [Oak Lucene Index ドキュメント](https://jackrabbit.apache.org/oak/docs/query/lucene.html).

Automated Cloud Manager パイプラインチェックでは、上記のベストプラクティスの一部を実施します。

## 大きな結果セットを持つクエリ {#queries-with-large-result-sets}

結果セットが大きくなるようなクエリを避けることが推奨されますが、大きな結果セットを処理する必要がある場合もあります。結果のサイズは事前にわからないことが多いので、処理の信頼性を高めるためには注意が必要です。

* クエリは、リクエスト内で実行しないでください。代わりに、Sling ジョブまたは AEM ワークフローの一部としてクエリを実行する必要があります。これらは、合計ランタイムに制限がなく、クエリやその結果の処理中にインスタンスが停止しても再起動されます。
* 100,000 個のノードに対するクエリ制限を克服するには、[キーセットのページネーション](https://jackrabbit.apache.org/oak/docs/query/query-engine.html#Keyset_Pagination)の使用を検討し、クエリを複数のサブクエリに分割する必要があります。

## リポジトリトラバーサル {#repository-traversal}

リポジトリをトラバースするクエリではインデックスが使用されず、次のようなメッセージでログに記録されます。

```text
28.06.2022 13:32:52.804 *WARN* [127.0.0.1 [1656415972414] POST /libs/settings/granite/operations/diagnosis/granite_queryperformance.explain.json HTTP/1.1] org.apache.jackrabbit.oak.plugins.index.Cursors$TraversingCursor Traversed 98000 nodes with filter Filter(query=select [jcr:path], [jcr:score], * from [nt:base] as a /* xpath: //* */, path=*) called by com.adobe.granite.queries.impl.explain.query.ExplainQueryServlet.getHeuristics; consider creating an index or changing the query
```

このログスニペットを使用すると、次の項目を確認できます。

* クエリ自体： `//*`
* このクエリを実行した Java コード： `com.adobe.granite.queries.impl.explain.query.ExplainQueryServlet::getHeuristics` はクエリの作成者を特定するのに役立ちます。

この情報を使用すると、このドキュメントの[クエリの最適化](#optimizing-queries)の節で説明している方法を使用して、このクエリを最適化できます。

### インデックストラバーサル {#index-traversal}

インデックスを使用するが、まだ読み込みが多いノードは、次のようなメッセージでログに記録されます ( 注意： `Index-Traversed` ではなく `Traversed`) をクリックします。

```text
05.10.2023 10:56:10.498 *WARN* [127.0.0.1 [1696502982443] POST /libs/settings/granite/operations/diagnosis/granite_queryperformance.explain.json HTTP/1.1] org.apache.jackrabbit.oak.plugins.index.search.spi.query.FulltextIndex$FulltextPathCursor Index-Traversed 60000 nodes with filter Filter(query=select [jcr:path], [jcr:score], * from [dam:Asset] as a where isdescendantnode(a, '/content/dam') order by [jcr:content/metadata/unindexedProperty] /* xpath: /jcr:root/content/dam//element(*, dam:Asset) order by jcr:content/metadata/unindexedProperty */, path=/content/dam//*)
```

これは、様々な理由で発生する場合があります。
1. インデックスでクエリのすべての制限を処理できるわけではありません。
   * この場合、最終結果セットのスーパーセットがインデックスから読み取られ、その後、クエリエンジンでフィルタリングされます。
   * これは、基になるインデックスクエリで制限を適用するよりも多くの時間がかかります。
1. クエリは、インデックス内で「ordered」とマークされていないプロパティで並べ替えられます。
   * この場合、インデックスから返されるすべての結果は、クエリエンジンで読み取られ、メモリ内で並べ替えられる必要があります。
   * これは、基になるインデックスクエリで並べ替えを適用する場合に比べて、多くの場合遅くなります。
1. クエリの実行者が、大きな結果セットの反復を試みています。
   * この状況は、次に示すように、様々な理由で発生する可能性があります。

| 原因 | 緩和策 |
|----------|--------------|
| 省略は `p.guessTotal` （または非常に大きな guessTotal を使用）を使用すると、QueryBuilder は多数の結果カウント結果を反復します。 | 提供 `p.guessTotal` 適切な値を持つ |
| Query Builder での大きな制限または無限の制限の使用 ( `p.limit=-1`) | 適切な値を `p.limit` （1000 以下が理想） |
| 基になる JCR クエリから大量の結果をフィルタリングする Query Builder でのフィルタリング用述語の使用 | フィルタリング述語を、基になる JCR クエリで適用できる制限に置き換える |
| QueryBuilder での比較器ベースの並べ替えの使用 | 基になる JCR クエリで、プロパティベースの順序に置き換えます（順序付きとしてインデックス付けされたプロパティを使用）。 |
| アクセス制御による多数の結果のフィルタリング | 追加のインデックス付きプロパティまたはパス制限をクエリに適用して、アクセス制御を反映します。 |
| 大きなオフセットを持つ「オフセットページネーション」の使用 | 使用を検討する [キーセットのページネーション](https://jackrabbit.apache.org/oak/docs/query/query-engine.html#Keyset_Pagination) |
| 多数の結果を繰り返す、または無限の数の結果 | 使用を検討する [キーセットのページネーション](https://jackrabbit.apache.org/oak/docs/query/query-engine.html#Keyset_Pagination) |
| 正しくないインデックスを選択しました | クエリとインデックス定義でタグを使用して、期待されるインデックスが確実に使用されるようにします。 |
