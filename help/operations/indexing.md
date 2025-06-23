---
title: コンテンツの検索とインデックス作成
description: AEM as a Cloud Service でのコンテンツの検索とインデックス作成について説明します。
exl-id: 4fe5375c-1c84-44e7-9f78-1ac18fc6ea6b
feature: Operations
role: Admin
source-git-commit: 8d881caf5181e9c3cdc6dcb69f0deabc2d5eeed8
workflow-type: ht
source-wordcount: '2918'
ht-degree: 100%

---

# コンテンツの検索とインデックス作成 {#indexing}

## AEM as a Cloud Service の変更点 {#changes-in-aem-as-a-cloud-service}

AEM as a Cloud Service によって、アドビは AEM インスタンス中心モデルから、Cloud Manager の CI/CD パイプラインによって駆動される、n-x AEM コンテナを持つサービスベースの表示に移行します。単一の AEM インスタンスでインデックスを設定および保守する代わりに、デプロイメントの前にインデックス設定を指定する必要があります。本番環境での設定変更は、CI/CD のポリシーに違反しています。インデックスの変更についても同じことが言えます。インデックスの変更は、本番環境に導入する前に指定、テスト、インデックスの再作成を行わないと、システムの安定性とパフォーマンスに影響を及ぼす可能性があります。

AEM 6.5 以前のバージョンと比較した主な変更点のリストを以下に示します。

1. ユーザーは、単一の AEM インスタンスのインデックスマネージャーにアクセスできなくなり、インデックスのデバッグ、設定または維持ができなくなります。ローカルデプロイメントおよびオンプレミスデプロイメントにのみ使用されます。
1. ユーザーは、単一の AEM インスタンスのインデックスを変更したり、整合性チェックやインデックス再作成を気にしたりする必要はありません。
1. 一般に、インデックスの変更は本番環境に移行する前に開始されます。Cloud Manager の CI／CD パイプラインの品質の高いゲートウェイを回避しないようにし、本番環境のビジネス KPI に影響を与えないようにするためです。
1. 本番環境での検索パフォーマンスを含むすべての関連指標は、実行時に顧客が利用できるので、検索とインデックスのトピックの全体的な表示を提供します。
1. 顧客は、必要に応じてアラートを設定できます。
1. SRE はシステムの正常性を常に監視し、可能な限り早期にアクションを実行します。
1. インデックスの設定は、デプロイメントを介して変更されます。インデックス定義の変更は、他のコンテンツの変更と同様に設定されます。
1. AEM as a Cloud Service の高レベルでは、[デプロイメントモデルが導入](#index-management-using-rolling-deployments)され、1 つは古いバージョン用のセット、もう 1 つは新しいバージョン用のセットの 2 組のインデックスが存在します。
1. Cloud Manager のビルドページで、顧客はインデックス作成ジョブが完了したかどうかを確認できます。新しいバージョンでトラフィックを受ける準備ができたら、通知を受け取ります。

制限事項：

* 現在、AEM as a Cloud Service でのインデックス管理は、`lucene` 型のインデックスに対してのみサポートされています。つまり、インデックスのカスタマイズはすべて `lucene` 型である必要があります。`async` プロパティには、`[async]`、`[async,nrt]`、`[fulltext-async]` のいずれかを指定できます。
* 内部的には、他のインデックスがクエリに設定され使用される可能性があります。例えば、`damAssetLucene` インデックスに対して書き込まれるクエリは、AEM as a Cloud Service では、実際には、このインデックスの Elasticsearch バージョンに対して実行される場合があります。この違いは、ユーザーには表示されません。ただし、`explain` 機能など、特定のツールでは異なるインデックスがレポートされます。Lucene インデックスと Elasticsearch インデックスの違いについては、[Apache Jackrabbit Oak の Elastic 関連ドキュメント](https://jackrabbit.apache.org/oak/docs/query/elastic.html)を参照してください。顧客は、Elasticsearch インデックスを直接設定する必要はなく、また設定できません。
* 標準のアナライザー（製品に付属しているアナライザー）のみサポートされています。カスタムアナライザーはサポートされていません。
* 類似の機能ベクトル（`useInSimilarity = true`）による検索はサポートされていません。

>[!TIP]
>
>高度な検索およびインデックス作成機能の詳細な説明など、Oak のインデックス作成とクエリの詳細については、[Apache Oak ドキュメント](https://jackrabbit.apache.org/oak/docs/query/query.html)を参照してください。


## 使用方法 {#how-to-use}

インデックス定義は、次の 3 つの主な使用例に分類できます。

1. 新しいカスタムインデックス定義を&#x200B;**追加**&#x200B;します。
2. 新しいバージョンを追加することにより、既存のインデックス定義を&#x200B;**更新**&#x200B;します。
3. 不要になったインデックス定義を&#x200B;**削除**&#x200B;します。

上記のポイント 1 と 2 の両方について、それぞれの Cloud Manager リリーススケジュールで、カスタムコードベースの一部としてインデックス定義を作成する必要があります。詳しくは、[AEM as a Cloud Service へのデプロイ](/help/implementing/deploying/overview.md)ドキュメントを参照してください。

## インデックス名 {#index-names}

インデックス定義は、次のカテゴリのいずれかに分類できます。

1. 標準（OOTB）インデックス。これらは、AEM が提供する事前定義済みのインデックスです。例：`/oak:index/cqPageLucene-2` または `/oak:index/damAssetLucene-8`。

2. OOTB インデックスのカスタマイズ。OOTB インデックスをカスタマイズするには、`-custom-` の後に数字を追加します。例えば、OOTB インデックス `/oak:index/damAssetLucene-8` のカスタマイズは `/oak:index/damAssetLucene-8-custom-1` のとおりです。カスタマイズは、通常、OOTB インデックスのコピーに加え、インデックスを作成する必要がある追加のプロパティです。

3. 完全なカスタムインデックス：まったく新しいインデックスを最初から作成できます。また、これらのインデックスは、`-custom-` およびバージョン番号で終わる必要があります。また、名前の競合を避けるために、インデックス名にプレフィックスを使用します。例：`/oak:index/acme.product-1-custom-2`。`acme.` はプレフィックスです。

>[!NOTE]
>
>`dam:Asset` ノードタイプへの新しいインデックス（特にフルテキストのインデックス）の導入は、OOTB 製品の機能と競合し、機能上およびパフォーマンス上の問題を引き起こす可能性があるため、お勧めできません。代わりに、`dam:Asset` ノードタイプでクエリのインデックスを作成する最も適切な方法は、追加のプロパティを追加して、`damAssetLucene-*` インデックスをカスタマイズすることです。これらの変更は、今後のリリースで新しい製品バージョンに自動的に結合されます。不明な場合は、アドビサポートに問い合わせてください。

## 新しいインデックス定義の準備 {#preparing-the-new-index-definition}

>[!NOTE]
>
>標準提供のインデックスをカスタマイズする場合（例：`damAssetLucene-8`）、CRX DE パッケージマネージャー（`/crx/packmgr/`）を使用して、最新の標準インデックス定義を *Cloud Service 環境*&#x200B;にコピーしてください。`damAssetLucene-8-custom-1`（またはそれ以上）に名前を変更し、XML ファイル内にカスタマイズを追加します。クラウド環境のインデックスのタイプが `elasticsearch` の場合は、さらに変更が必要です。`type` プロパティを `lucene` に変更し、`async` プロパティを `[async,nrt]` に変更し、`similarityTags` プロパティを `true` に変更します。 これにより、必要な設定が誤って削除されるのを防ぐことができます。例えば、`/oak:index/damAssetLucene-8/tika` の下の `tika` ノードは、AEM Cloud Service 環境にデプロイされたカスタマイズ済みのインデックスで必要ですが、ローカルの AEM SDK には存在しません。

OOTB インデックスをカスタマイズする場合は、カスタマイズ済みまたはカスタムインデックス定義を含む新しいパッケージを準備します。インデックス名は命名パターンに従う必要があります。

`<indexName>-<productVersion>-custom-<customVersion>`

完全にカスタマイズされたインデックスについて、次の命名パターンに従うインデックス定義を含む新しいインデックス定義パッケージを準備します。

`<prefix>.<indexName>-<productVersion>-custom-<customVersion>`

制限の節で説明したように、パッケージマネージャーを使用して抽出されたインデックス定義のタイプが異なる場合（例：`elasticsearch`）であっても、カスタマイズされたインデックス定義の `type` を常に `lucene` に設定する必要があります。
抽出されたインデックス定義が `elastic-async` に設定されている場合は、`async` プロパティも変更する必要があります。カスタマイズされたインデックス定義は、`async` プロパティを `[async]`、`[async,nrt]`、`[fulltext-async]` のいずれかに設定する必要があります。

<!-- Alexandru: temporarily drafting this statement due to CQDOC-17701

The package from the above sample is built as `com.adobe.granite:new-index-content:zip:1.0.0-SNAPSHOT`. -->

>[!NOTE]
>
>インデックス定義を含んだコンテンツパッケージには、コンテンツパッケージの `properties.xml` ファイルで次のプロパティを設定する必要があります。`properties.xml` はデフォルトで新しいパッケージに作成され、`<package_name>/META-INF/vault/properties.xml` にあります。
>
> * `noIntermediateSaves=true`
>
> * `allowIndexDefinitions=true`

## カスタムインデックス定義のデプロイ {#deploying-custom-index-definitions}

標準提供のインデックス `damAssetLucene-8` のカスタマイズバージョンをデプロイする方法を説明するために、詳細な手順を示すガイドを提供します。この例では、名前を `damAssetLucene-8-custom-1` に変更します。その場合の手順は次のとおりです。

1. `ui.apps` ディレクトリに、更新されたインデックス名で新規フォルダーを作成します。
   * 例：`ui.apps/src/main/content/jcr_root/_oak_index/damAssetLucene-8-custom-1/`

2. 作成したフォルダー内にカスタム設定を含む設定ファイル `.content.xml` を追加します。カスタマイズの例を次に示します。
ファイル名：`ui.apps/src/main/content/jcr_root/_oak_index/damAssetLucene-8-custom-1/.content.xml`

   ```xml
   <?xml version="1.0" encoding="UTF-8"?>
   <jcr:root xmlns:jcr="http://www.jcp.org/jcr/1.0" xmlns:dam="http://www.day.com/dam/1.0" xmlns:nt="http://www.jcp.org/jcr/nt/1.0" xmlns:oak="http://jackrabbit.apache.org/oak/ns/1.0" xmlns:rep="internal"
       jcr:mixinTypes="[rep:AccessControllable]"
       jcr:primaryType="oak:QueryIndexDefinition"
       async="[async,nrt]"
       compatVersion="{Long}2"
       evaluatePathRestrictions="{Boolean}true"
       includedPaths="[/content/dam]"
       maxFieldLength="{Long}100000"
       type="lucene">
       <facets
           jcr:primaryType="nt:unstructured"
           secure="statistical"
           topChildren="100"/>
       <indexRules jcr:primaryType="nt:unstructured">
           <dam:Asset jcr:primaryType="nt:unstructured">
               <properties jcr:primaryType="nt:unstructured">
                   <cqTags
                       jcr:primaryType="nt:unstructured"
                       name="jcr:content/metadata/cq:tags"
                       nodeScopeIndex="{Boolean}true"
                       propertyIndex="{Boolean}true"
                       useInSpellcheck="{Boolean}true"
                       useInSuggest="{Boolean}true"/>
               </properties>
           </dam:Asset>
       </indexRules>
       <tika jcr:primaryType="nt:folder">
           <config.xml jcr:primaryType="nt:file"/>
       </tika>
   </jcr:root>
   ```

3. `ui.apps/src/main/content/META-INF/vault/filter.xml` で、FileVault フィルターにエントリを追加します。

   ```xml
   <?xml version="1.0" encoding="UTF-8"?>
   <workspaceFilter version="1.0">
       ...
       <filter root="/oak:index/damAssetLucene-8-custom-1"/> 
   </workspaceFilter>
   ```

4. Apache Tika の設定ファイルを次の場所に追加します。`ui.apps/src/main/content/jcr_root/_oak_index/damAssetLucene-8-custom-1/tika/config.xml`：

   ```xml
   <properties>
       <detectors>
           <detector class="org.apache.tika.detect.TypeDetector"/>
       </detectors>
       <parsers>
           <parser class="org.apache.tika.parser.DefaultParser">
           <mime>text/plain</mime>
           </parser>
       </parsers>
       <service-loader initializableProblemHandler="ignore" dynamic="true"/>
   </properties>
   ```

5. 設定が「[プロジェクト設定](#project-configuration)」セクションで提供されているガイドラインに準拠していることを確認します。必要に応じて調整を行います。

## プロジェクト設定

Jackrabbit `filevault-package-maven-plugin` のバージョン >= `1.3.2` を使用することを強くお勧めします。プロジェクトに組み込む手順は次のとおりです。

1. トップレベル `pom.xml` のバージョンを更新します。

   ```xml
   <plugin>
       <groupId>org.apache.jackrabbit</groupId>
           <artifactId>filevault-package-maven-plugin</artifactId>
           ...
           <version>1.3.2</version>
       ...
   </plugin>
   ```

2. 次の項目をトップレベル `pom.xml` に追加します。

   ```xml
   <jackrabbit-packagetype>
       <options>   
           <immutableRootNodeNames>apps,libs,oak:index</immutableRootNodeNames>
       </options>
   </jackrabbit-packagetype>
   ```

   プロジェクトのトップレベル `pom.xml` ファイル（前述の設定が含まれている）のサンプルを以下に示します：

   ファイル名：`pom.xml`

   ```xml
   <plugin>
       <groupId>org.apache.jackrabbit</groupId>
           <artifactId>filevault-package-maven-plugin</artifactId>
           ...
           <version>1.3.2</version>
           <configuration>
               ...
               <validatorsSettings>
                   <jackrabbit-packagetype>
                       <options>
                           <immutableRootNodeNames>apps,libs,oak:index</immutableRootNodeNames>
                       </options>
                   </jackrabbit-packagetype>
                   ...
               ...
   </plugin>
   ```

3. `ui.apps/pom.xml` および `ui.apps.structure/pom.xml` で `filevault-package-maven-plugin` の `allowIndexDefinitions` および `noIntermediateSaves` オプションを有効にする必要があります。`allowIndexDefinitions` を有効にするとカスタムインデックス定義を使用でき、`noIntermediateSaves` では設定がアトミックに追加されます。

   ファイル名：`ui.apps/pom.xml` および `ui.apps.structure/pom.xml`

   ```xml
   <plugin>
       <groupId>org.apache.jackrabbit</groupId>
           <artifactId>filevault-package-maven-plugin</artifactId>
           <configuration>
               <allowIndexDefinitions>true</allowIndexDefinitions>
               <properties>
                   <cloudManagerTarget>none</cloudManagerTarget>
                   <noIntermediateSaves>true</noIntermediateSaves>
               </properties>
       ...
   </plugin>
   ```

4. `ui.apps.structure/pom.xml` で `/oak:index` にフィルターを追加します：

   ```xml
   <filters>
       ...
       <filter><root>/oak:index</root></filter>
   </filters>
   ```

新しいインデックス定義を追加した後、Cloud Manager を使用して新しいアプリケーションをデプロイします。このデプロイメントでは 2 つのジョブが開始され、それぞれ MongoDB と Azure Segment Store にオーサー用とパブリッシュ用のインデックス定義を追加（また必要に応じて結合）します。切り替えの前に、基になるリポジトリでは、更新されたインデックス定義でインデックスが再作成されます。。

>[!TIP]
>
>AEM as a Cloud Service を使用する場合に必要なパッケージ構造について詳しくは、[AEM プロジェクト構造](/help/implementing/developing/introduction/aem-project-content-package-structure.md)を参照してください。

## ローリングデプロイメントを使用したインデックス管理 {#index-management-using-rolling-deployments}

### インデックス管理とは {#what-is-index-management}

インデックス管理とは、インデックスの追加、削除、変更を行うことです。インデックスの&#x200B;*定義*&#x200B;変更はすぐにできますが、変更を適用する（「インデックスの構築」、または既存インデックスの場合は「インデックスの再構築」と呼ばれる）には時間が必要です。これは即時には実行されません。インデックスを作成するデータをリポジトリでスキャンする必要があります。

### ローリングデプロイメントの概要 {#what-are-rolling-deployments}

ローリングデプロイメントでは、ダウンタイムをゼロにするアップグレードも可能で、高速なロールバックが提供されます。アプリケーションの古いバージョンは、アプリケーションの新しいバージョンと同時に実行されます。

### 読み取り専用領域と読み取り／書き込み可能領域 {#read-only-and-read-write-areas}

リポジトリの特定の領域（リポジトリの読み取り専用の部分）は、古いバージョンと新しいバージョンで異なる場合があります。リポジトリの読み取り専用領域は、通常、「`/app`」と「`/libs`」です。次の例では、読み取り専用領域に斜体を使用し、読み取り／書き込み可能領域に太字を使用します。

* **/**
* */apps（読み取り専用）*
* **/content**
* */libs（読み取り専用）*
* **/oak:index**
* **/oak:index/acme.**
* **/jcr:system**
* **/system**
* **/var**

リポジトリーの読み取り／書き込み領域は、アプリケーションのすべてのバージョン間で共有されますが、アプリケーションの各バージョンには、`/apps` と `/libs` の固有のセットがあります。

### ローリングデプロイメントを使用しないインデックス管理 {#index-management-without-rolling-deployments}

開発中、またはオンプレミスインストールを使用する場合は、インデックスを実行時に追加、削除、変更できます。インデックスが使用可能な場合は、インデックスが使用されます。まだ古いバージョンのアプリケーションでインデックスを使用していない場合は、通常、予定されたダウンタイム中にインデックスが構築されます。インデックスの削除時や、既存のインデックスの変更時にも同じことが起こります。インデックスを削除すると、その時点で使用できなくなります。

### ローリングデプロイメントによるインデックス管理 {#index-management-with-rolling-deployments}

ローリングデプロイメントでは、ダウンタイムは発生しません。更新中のしばらくの間、アプリケーションの古いバージョン（例えば、バージョン 1）と新しいバージョン（バージョン 2）の両方が、同じリポジトリに対して同時に実行されます。バージョン 1 で特定のインデックスを使用可能にする必要がある場合は、バージョン 2 でこのインデックスを削除しないでください。インデックスは、後で削除する必要があります（例えば、バージョン 3 で）。その時点で、アプリケーションのバージョン 1 が実行されなくなることが保証されます。また、バージョン 2 が実行中で、バージョン 2 のインデックスが使用可能でも、バージョン 1 が正常に動作するようにアプリケーションを作成してください。

新しいバージョンへのアップグレードが完了した後、システムが古いインデックスをガベージコレクションできます。（ロールバックが必要な場合は）ロールバックを高速化するために、通常、古いインデックスが 1 週間保持されます。

次の表に、5 つのインデックス定義を示します。インデックス `cqPageLucene` は両方のバージョンで使用され、インデックス `damAssetLucene-custom-1` はバージョン 2 でのみ使用されます。

>[!NOTE]
>
>`<indexName>-custom-<customerVersionNumber>` は、既存のインデックスの代わりとしてマークするために、AEM as a Cloud Service で必要です。

| 索引 | 標準提供インデックス | バージョン 1 で使用 | バージョン 2 で使用 |
|---|---|---|---|
| /oak:index/damAssetLucene-8 | はい | はい | いいえ |
| /oak:index/damAssetLucene-8-custom-1 | 可（カスタマイズ） | いいえ | はい |
| /oak:index/acme.product-1-custom-1 | いいえ | はい | いいえ |
| /oak:index/acme.product-1-custom-2 | いいえ | いいえ | はい |
| /oak:index/cqPageLucene-2 | はい | はい | はい |

バージョン番号は、インデックスが変更されるたびに増加します。カスタムインデックス名が製品自体のインデックス名と競合しないようにするには、カスタムインデックスと、標準提供のインデックスへの変更を、`-custom-<number>` で終える必要があります。

### 標準提供のインデックスの変更 {#changes-to-out-of-the-box-indexes}

アドビが `damAssetLucene` や `cqPageLucene` などの標準提供のインデックスを変更すると、`damAssetLucene-2` や `cqPageLucene-2` という名前の新しいインデックスが作成されます。あるいは、インデックスが既にカスタマイズされている場合は、次に示すように、カスタマイズされたインデックス定義と標準提供のインデックスの変更が結合されます。変更は自動的に結合されます。つまり、標準提供のインデックスが変更された場合、何もする必要はありません。ただし、後でインデックスを再びカスタマイズすることは可能です。この場合、最新の（結合された）バージョンをベースラインとして使用することが重要です。

| 索引 | 標準提供インデックス | バージョン 2 で使用 | バージョン 3 で使用 |
|---|---|---|---|
| /oak:index/damAssetLucene-1-custom-1 | 可（カスタマイズ） | はい | いいえ |
| /oak:index/damAssetLucene-2-custom-1 | はい（damAssetLucene-1-custom-1 および damAssetLucene-2 から自動的に結合） | いいえ | はい |
| /oak:index/cqPageLucene-1 | はい | はい | いいえ |
| /oak:index/cqPageLucene-2 | はい | いいえ | はい |

環境によって AEM バージョンが異なる場合があることに注意することが重要です。例：`dev` 環境はリリース `X+1` にありますが、ステージング環境と実稼動環境はまだリリース `X` にあり、`dev` で必要なテストを実行した後、リリース `X+1` にアップグレードされる予定です。リリース `X+1` にカスタマイズされた製品インデックスの新しいバージョンが付属し、このインデックスの新しいカスタマイズが必要な場合に、AEM リリースに基づいて環境に設定する必要があるバージョンを次の表に示します。

| 環境（AEM リリースバージョン） | 製品インデックスバージョン | 既存のカスタムインデックスバージョン | 新しいカスタムインデックスバージョン |
|-----------------------------------|-----------------------|-------------------------------|----------------------------|
| 開発（X+1） | damAssetLucene-11 | damAssetLucene-11-custom-1 | damAssetLucene-11-custom-2 |
| ステージング（X） | damAssetLucene-10 | damAssetLucene-10-custom-1 | damAssetLucene-10-custom-2 |
| 実稼動（X） | damAssetLucene-10 | damAssetLucene-10-custom-1 | damAssetLucene-10-custom-2 |


### 現在の制限事項 {#current-limitations}

インデックス管理は、`compatVersion` が `2` に設定された `lucene` 型のインデックスに対してのみサポートされています。内部的には、例えば Elasticsearch インデックスなどの他のインデックスが設定され、クエリに使用される場合があります。`damAssetLucene` インデックスに対して書き込まれるクエリは、AEM as a Cloud Serviceでは実際に、このインデックスの Elasticsearch バージョンに対して実行される場合があります。この違いはアプリケーションユーザーには見えませんが、`explain` 機能などの特定のツールでは異なるインデックスがレポートされます。Lucene インデックスと Elasticsearch インデックスの違いについては、[Apache Jackrabbit Oak の Elasticsearch ドキュメント](https://jackrabbit.apache.org/oak/docs/query/elastic.html)を参照してください。顧客が Elasticsearch インデックスを直接設定することはできず、またその必要もありません。

ビルトインアナライザー（製品に付属しているアナライザー）のみがサポートされています。カスタムアナライザーはサポートされていません。

現在、`/oak:index` のコンテンツのインデックス作成はサポートされていません。

最高のオペレーショナルパフォーマンスを得るには、インデックスを過度に大きくしないようにします。すべてのインデックスの合計サイズを目安にすることができます。開発環境でカスタムインデックスを追加し、標準インデックスを調整した後に、このサイズが 100％を超えて増加する場合は、カスタムインデックスの定義を調整する必要があります。AEM as a Cloud Service を使用すると、システムの安定性とパフォーマンスに悪影響を与える可能性のあるインデックスを、デプロイされないようにしたり、削除したりすることができます。

### インデックスの追加 {#adding-an-index}

新しいバージョン以降のアプリケーションで使用する `/oak:index/acme.product-1-custom-1` という名前の完全カスタムインデックスを追加するには、インデックスを以下のように設定する必要があります。

`acme.product-1-custom-1`

この設定は、インデックス名の前にカスタム識別子を付け、その後にドット（**`.`**）を付けることで機能します。識別子の長さは 2～5 文字です。

前述のこの設定により、新しいバージョンのアプリケーションでのみインデックスが使用されます。

### インデックスの変更 {#changing-an-index}

既存のインデックスを変更する場合は、変更したインデックス定義を使用して新しいインデックスを追加する必要があります。例えば、既存のインデックス `/oak:index/acme.product-1-custom-1` が変更されるとします。古いインデックスは `/oak:index/acme.product-1-custom-1` 下に、新しいインデックスは `/oak:index/acme.product-1-custom-2` 下に格納されます。

アプリケーションの古いバージョンでは、次の設定を使用します。

`/oak:index/acme.product-1-custom-1`

新しいバージョンのアプリケーションでは、次の（変更された）設定が使用されます。

`/oak:index/acme.product-1-custom-2`

>[!NOTE]
>
>AEM as a Cloud Service のインデックス定義が、ローカル開発インスタンスのインデックス定義と完全には一致しない場合があります。開発インスタンスには Tika 設定がありませんが、AEM as a Cloud Service のインスタンスには Tika 設定があります。Tika 設定でインデックスをカスタマイズする場合は、その Tika 設定を保持してください。

### 変更の取り消し {#undoing-a-change}

エラーや、変更が不要になったなどの理由で、インデックス定義の変更を元に戻す必要が生じる場合があります。例えば、インデックス定義 `damAssetLucene-8-custom-3` に誤りがある場合は、以前の定義 `damAssetLucene-8-custom-2` に戻す必要があります。それには、前のインデックス `damAssetLucene-8-custom-2.` のコピーである `damAssetLucene-8-custom-4` という名前の新しいインデックスを作成します

### インデックスの削除 {#removing-an-index}

次の設定は、標準提供（OOTB）のインデックスのカスタマイズと、完全なカスタムインデックスにのみ適用されます。元の OOTB インデックスは AEM で使用されるので、削除することはできません。

システムの整合性と安定性を確保するには、デプロイ後は、インデックス定義を不変として扱う必要があります。カスタムインデックスまたはカスタマイズを削除する必要がある場合は、削除を効果的にシミュレートする定義を使用して、そのインデックスの新しいバージョンを作成します
（以下の例を参照）。

新しいバージョンのインデックスをデプロイすると、同じインデックスの古いバージョンはクエリで使用されなくなります。
古いバージョンはただちに環境から削除されることはありません。
ただし、定期的に実行されるクリーンアップメカニズムによって、ガベージコレクションの対象になります。
エラーが発生した場合の回復を可能にする猶予期間の後
（現在、インデックス作成が削除されてから 7 日が経過しましたが、変更される可能性があります）、
このクリーンアップメカニズムでは、未使用のインデックスデータが削除され、
古いバージョンのインデックスが環境で無効になるか、環境から削除されます。

以下では、OOTB インデックスのカスタマイズの削除と完全なカスタムインデックスの削除の 2 つのケースについて説明します。

#### 標準提供のインデックスのカスタマイズの削除

OOTB インデックスの定義を新しいバージョンとして使用して、[変更の取り消し](#undoing-a-change-undoing-a-change)で説明されている手順に従います。例えば、既に `damAssetLucene-8-custom-3` をデプロイしていて、カスタマイズが不要になり、デフォルトの `damAssetLucene-8` インデックスに戻す場合は、`damAssetLucene-8` のインデックス定義を含むインデックス `damAssetLucene-8-custom-4` を追加する必要があります。

#### 完全なカスタムインデックスの削除

ダミーインデックスを新しいバージョンとして使用して、[変更の取り消し](#undoing-a-change-undoing-a-change)で説明されている手順に従います。ダミーインデックスはクエリには使用されず、データを含んでいないので、インデックスが存在しなかった場合と効果は同じです。この例では、`/oak:index/acme.product-1-custom-3` という名前を付けることができます。この名前により、`/oak:index/acme.product-1-custom-2` インデックスが置き換えられます。このようなダミーインデックスの例を次に示します。

```xml
<acme.product-1-custom-3
        jcr:primaryType="oak:QueryIndexDefinition"
        async="async"
        compatVersion="2"
        includedPaths="/dummy"
        queryPaths="/dummy"
        type="lucene">
        <indexRules jcr:primaryType="nt:unstructured">
            <rep:root jcr:primaryType="nt:unstructured">
                <properties jcr:primaryType="nt:unstructured">
                    <dummy
                        jcr:primaryType="nt:unstructured"
                        name="dummy"
                        propertyIndex="{Boolean}true"/>
                </properties>
            </rep:root>
        </indexRules>
</acme.product-1-custom-3>
```

## インデックスとクエリの最適化 {#index-query-optimizations}

Apache Jackrabbit Oak では、柔軟なインデックス設定により検索クエリを効率的に処理できます。大規模なリポジトリーでは、インデックスは特に重要です。すべてのクエリに適切なインデックスを付与するようにしてください。適切なインデックスのないクエリを実行すると、何千ものノードが読み取られる可能性があり、その場合は警告として記録されます。

クエリとインデックスを最適化する方法については、[こちらのドキュメント](query-and-indexing-best-practices.md)を参照してください。
