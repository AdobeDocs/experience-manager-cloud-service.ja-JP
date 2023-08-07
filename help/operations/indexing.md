---
title: コンテンツの検索とインデックス作成
description: AEM as a Cloud Serviceでのコンテンツの検索とインデックス作成について説明します。
exl-id: 4fe5375c-1c84-44e7-9f78-1ac18fc6ea6b
source-git-commit: 8c73805b6ed1b7a03c65b4d21a4252c1412a5742
workflow-type: tm+mt
source-wordcount: '2325'
ht-degree: 38%

---

# コンテンツの検索とインデックス作成 {#indexing}

## AEM as a Cloud Service の変更点 {#changes-in-aem-as-a-cloud-service}

AEM as a Cloud Service によって、アドビは AEM インスタンス中心モデルから、Cloud Manager の CI/CD パイプラインによって駆動される、n-x AEM コンテナを持つサービスベースの表示に移行します。単一の AEM インスタンスでインデックスを設定および保守する代わりに、デプロイメントの前にインデックス設定を指定する必要があります。本番環境での設定変更は、CI/CD のポリシーを明らかに破るものです。インデックスの変更についても同じことが言えます。実稼働環境に移行する前にテストおよび再インデックスを指定しない場合、システムの安定性とパフォーマンスに影響を及ぼす可能性があるからです。

AEM 6.5 以前のバージョンと比較した主な変更点のリストを以下に示します。

1. 単一のAEMインスタンスのインデックスマネージャーにアクセスして、インデックスのデバッグ、設定、または維持を行うことはできなくなりました。 ローカルデプロイメントおよびオンプレミスデプロイメントにのみ使用されます。
1. 単一のAEMインスタンスでインデックスを変更したり、整合性チェックや再インデックスについて心配する必要はありません。
1. 一般に、インデックスの変更は、実稼動環境に移行する前に開始され、Cloud Manager の CI/CD パイプラインの品質の高いゲートウェイを迂回せず、実稼動環境のビジネス KPI には影響しません。
1. 実稼動環境での検索パフォーマンスを含むすべての関連指標は、実行時に顧客が検索とインデックス作成のトピックの全体像を提供できるようになります。
1. お客様は、ニーズに応じてアラートを設定できます。
1. SRE はシステムの正常性を監視24/7、可能な限り早く対処します。
1. インデックスの設定は、デプロイメントを介して変更されます。インデックス定義の変更は、他のコンテンツの変更と同様に設定されます。
1. AEMas a Cloud Serviceの概要と、 [ローリングデプロイメントモデル](#index-management-using-rolling-deployments)には、古いバージョン用と新しいバージョン用の 2 組のインデックスが存在します。
1. Cloud Manager のビルドページで、インデックス作成ジョブが完了したかどうかを確認できます。新しいバージョンでトラフィックを引き受ける準備ができたら、通知を受け取ります。

制限事項：

* 現在、AEM as a Cloud Service のインデックス管理は、`lucene` 型のインデックスに対してのみサポートされています。
* 標準のアナライザーのみがサポートされます（つまり、製品に付属しているアナライザー）。 カスタムアナライザーはサポートされていません。
* 内部的には、他のインデックスがクエリに設定され使用される可能性があります。例えば、`damAssetLucene` インデックスに対して記述されたクエリは、Skyline 上では実際には、このインデックスの Elasticsearch バージョンに対して実行される可能性があります。この違いは、通常、アプリケーションとユーザーには表示されませんが、 `explain` 機能は、別のインデックスをレポートします。 Lucene インデックスと Elasticsearch インデックスの違いについては、[Apache Jackrabbit Oak の Elastic 関連ドキュメント](https://jackrabbit.apache.org/oak/docs/query/elastic.html)を参照してください。お客様は、Elasticsearchインデックスを直接設定する必要はなく、または設定できません。
* 類似のフィーチャベクトル (`useInSimilarity = true`) はサポートされていません。

## 使用方法 {#how-to-use}

インデックス定義は、次のように、3 つの主な使用例に分類できます。

1. **追加** 新しいカスタムインデックス定義。
2. **更新** 新しいバージョンを追加することにより、既存のインデックス定義を作成する。
3. **削除** 不要になったインデックス定義。

上記のポイント 1 と 2 の両方について、それぞれの Cloud Manager リリーススケジュールで、カスタムコードベースの一部として新しいインデックス定義を作成する必要があります。詳しくは、 [AEMへのデプロイ (as a Cloud Service)](/help/implementing/deploying/overview.md) ドキュメント。

## インデックス名 {#index-names}

インデックス定義は、次のカテゴリのいずれかに分類できます。

1. 標準 (OOTB) インデックス。 例： `/oak:index/cqPageLucene-2` または `/oak:index/damAssetLucene-8`.

2. OOTB インデックスのカスタマイズ。 これらは以下を付加して示します。 `-custom-` 元のインデックス名に続く数値識別子。 （例：`/oak:index/damAssetLucene-8-custom-1`）。

3. 完全なカスタムインデックス：まったく新しいインデックスを最初から作成できます。 名前の競合を避けるために、名前にプレフィックスが必要です。 例： `/oak:index/acme.product-1-custom-2`( プレフィックスは `acme.`

## 新しいインデックス定義の準備 {#preparing-the-new-index-definition}

>[!NOTE]
>
>標準提供のインデックスをカスタマイズする場合（例：`damAssetLucene-8`）、CRX DE パッケージマネージャー（`/crx/packmgr/`）を使用して、最新の標準のインデックス定義を *Cloud Service 環境*&#x200B;にコピーしてください。名前をに変更します。 `damAssetLucene-8-custom-1` （またはそれ以上）、XML ファイル内にカスタマイズを追加します。 これにより、必要な設定が誤って削除されるのを防ぐことができます。 例えば、`/oak:index/damAssetLucene-8/tika` 下のノード `tika` は、Cloud Service のカスタマイズ済みインデックスに必要です。Cloud SDK には存在しません。

OOTB インデックスのカスタマイズの場合は、次の命名パターンに従う実際のインデックス定義を含む新しいパッケージを準備します。

`<indexName>-<productVersion>-custom-<customVersion>`

完全にカスタマイズされたインデックスに対して、次の命名パターンに従うインデックス定義を含む新しいインデックス定義パッケージを準備します。

`<prefix>.<indexName>-<productVersion>-custom-<customVersion>`

<!-- Alexandru: temporarily drafting this statement due to CQDOC-17701

The package from the above sample is built as `com.adobe.granite:new-index-content:zip:1.0.0-SNAPSHOT`. -->

>[!NOTE]
>
>インデックス定義を含むコンテンツパッケージには、コンテンツパッケージのプロパティファイル ( `<package_name>/META-INF/vault/properties.xml`:
>
> * `noIntermediateSaves=true`
>
> * `allowIndexDefinitions=true`

## カスタム・インデックス定義のデプロイ {#deploying-custom-index-definitions}

標準提供のインデックスのカスタマイズバージョンをデプロイする方法を説明するには `damAssetLucene-8`を使用する場合、詳細な手順を示すガイドを提供します。 この例では、名前をに変更します。 `damAssetLucene-8-custom-1`. その場合の手順は次のとおりです。

1. 新しいフォルダーを作成し、更新されたインデックス名を `ui.apps` ディレクトリ：
   * 例：`ui.apps/src/main/content/jcr_root/_oak_index/damAssetLucene-8-custom-1/`

2. 設定ファイルを追加 `.content.xml` 新しく作成されたフォルダー内のカスタム設定を使用します。 カスタマイズの例を次に示します。ファイル名： `ui.apps/src/main/content/jcr_root/_oak_index/damAssetLucene-8-custom-1/.content.xml`

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

3. の FileVault フィルタにエントリを追加する `ui.apps/src/main/content/META-INF/vault/filter.xml`:

   ```xml
   <?xml version="1.0" encoding="UTF-8"?>
   <workspaceFilter version="1.0">
       ...
       <filter root="/oak:index/damAssetLucene-8-custom-1"/> 
   </workspaceFilter>
   ```

4. Apache Tika の設定ファイルを次の場所に追加します。 `ui.apps/src/main/content/jcr_root/_oak_index/damAssetLucene-8-custom-1/tika/config.xml`:

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

5. 設定が、 [プロジェクト設定](#project-configuration) 」セクションに入力します。 必要に応じて適応を行います。

## プロジェクト設定

バージョン >=を使用することを強くお勧めします。 `1.3.2` ジャックラッビの `filevault-package-maven-plugin`. プロジェクトに組み込む手順は次のとおりです。

1. トップレベルのバージョンを更新します `pom.xml`:

   ```xml
   <plugin>
       <groupId>org.apache.jackrabbit</groupId>
           <artifactId>filevault-package-maven-plugin</artifactId>
           ...
           <version>1.3.2</version>
       ...
   </plugin>
   ```

2. トップレベルに以下を追加します。 `pom.xml`:

   ```xml
   <jackrabbit-packagetype>
       <options>   
           <immutableRootNodeNames>apps,libs,oak:index</immutableRootNodeNames>
       </options>
   </jackrabbit-packagetype>
   ```

   プロジェクトの最上位レベルのサンプルを以下に示します `pom.xml` ファイルには、前述の設定が含まれています。

   ファイル名: `pom.xml`

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

3. In `ui.apps/pom.xml` および `ui.apps.structure/pom.xml` を有効にする必要があります。 `allowIndexDefinitions` および `noIntermediateSaves` オプション `filevault-package-maven-plugin`. 有効化 `allowIndexDefinitions` では、カスタムインデックス定義を使用できます。 `noIntermediateSaves` は、設定が自動的に追加されるようにします。

   ファイル名： `ui.apps/pom.xml` および `ui.apps.structure/pom.xml`

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

4. フィルターを追加 `/oak:index` in `ui.apps.structure/pom.xml`:

   ```xml
   <filters>
       ...
       <filter><root>/oak:index</root></filter>
   </filters>
   ```

新しいインデックス定義を追加した後、Cloud Manager を使用して新しいアプリケーションをデプロイします。 このデプロイメントは 2 つのジョブを開始し、それぞれ MongoDB と Azure Segment Store に、オーサー用とパブリッシュ用のインデックス定義を追加（必要に応じて結合）します。 切り替えの前に、基になるリポジトリは、更新されたインデックス定義で再インデックスを受けます。

>[!TIP]
>
>AEM as a Cloud Serviceに必要なパッケージ構造の詳細については、このドキュメントを参照してください。 [AEM Project Structure](/help/implementing/developing/introduction/aem-project-content-package-structure.md).

## ローリングデプロイメントを使用したインデックス管理 {#index-management-using-rolling-deployments}

### インデックス管理とは {#what-is-index-management}

インデックス管理とは、インデックスの追加、削除、変更を行うことです。インデックスの&#x200B;*定義*&#x200B;変更はすぐにできますが、変更を適用する（「インデックスの構築」、または既存インデックスの場合は「インデックスの再構築」と呼ばれる）には時間が必要です。これは即時には実行されません。インデックスを作成するデータをリポジトリでスキャンする必要があります。

### ローリングデプロイメントとは {#what-are-rolling-deployments}

ローリングデプロイメントは、ダウンタイムを短縮できます。 また、ダウンタイムをゼロにするアップグレードも可能で、高速なロールバックが可能です。古いバージョンのアプリケーションは、新しいバージョンのアプリケーションと同時に実行されます。

### 読み取り専用領域と読み取り／書き込み可能領域 {#read-only-and-read-write-areas}

リポジトリの特定の領域（リポジトリの読み取り専用の部分）は、古いバージョンと新しいバージョンで異なる場合があります。 リポジトリの読み取り専用領域は通常、 `/app` および `/libs`. 次の例では、読み取り専用領域に斜体を使用し、読み取り／書き込み可能領域に太字を使用します。

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

開発時、またはオンプレミスインストールを使用する場合、インデックスは実行時に追加、削除または変更できます。 インデックスが使用可能な場合は、インデックスが使用されます。 古いバージョンのアプリケーションでインデックスがまだ使用されていない場合、インデックスは通常、予定されたダウンタイム中に構築されます。 インデックスの削除時や、既存のインデックスの変更時にも同じことが起こります。インデックスを削除すると、削除されたインデックスは使用できなくなります。

### ローリングデプロイメントによるインデックス管理 {#index-management-with-rolling-deployments}

ローリングデプロイメントでは、ダウンタイムは発生しません。 更新中のしばらくの間、アプリケーションの古いバージョン（バージョン 1 など）と新しいバージョン（バージョン 2 など）の両方が、同じリポジトリに対して同時に実行されます。 バージョン 1 で特定のインデックスを使用可能にする必要がある場合は、バージョン 2 でこのインデックスを削除しないでください。インデックスは、後で削除する必要があります（例：バージョン 3）。その時点で、アプリケーションのバージョン 1 が実行されなくなることが保証されます。 また、バージョン 2 が実行中で、バージョン 2 のインデックスが使用可能でも、バージョン 1 が正常に動作するようにアプリケーションを作成してください。

新しいバージョンへのアップグレードが完了した後、システムが古いインデックスをガベージコレクションできます。古いインデックスは、ロールバックを高速化するために、しばらくの間保持される場合があります（ロールバックが必要な場合）。

次の表に、5 つのインデックス定義を示します。インデックス `cqPageLucene` は両方のバージョンで使用され、インデックス `damAssetLucene-custom-1` はバージョン 2 でのみ使用されます。

>[!NOTE]
>
>The `<indexName>-custom-<customerVersionNumber>` は、既存のインデックスの代わりとしてマークするためにAEM as a Cloud Serviceで必要です。

| 索引 | 標準提供インデックス | バージョン 1 で使用 | バージョン 2 で使用 |
|---|---|---|---|
| /oak:index/damAssetLucene | はい | はい | いいえ |
| /oak:index/damAssetLucene-custom-1 | 可（カスタマイズ） | いいえ | はい |
| /oak:index/acme.product-custom-1 | いいえ | はい | いいえ |
| /oak:index/acme.product-custom-2 | いいえ | いいえ | はい |
| /oak:index/cqPageLucene | はい | はい | はい |

バージョン番号は、インデックスが変更されるたびに増加します。製品自体のインデックス名と衝突するカスタムインデックス名を回避するには、カスタムインデックスと、標準提供のインデックスの変更をで終える必要があります。 `-custom-<number>`.

### 標準提供のインデックスの変更 {#changes-to-out-of-the-box-indexes}

Adobeが「damAssetLucene」や「cqPageLucene」などの標準のインデックスを変更した後、という名前の新しいインデックスが作成されます。 `damAssetLucene-2` または `cqPageLucene-2` が作成されました。 また、インデックスが既にカスタマイズされている場合は、次に示すように、カスタマイズされたインデックス定義と標準のインデックスの変更が結合されます。 変更のマージは自動的に行われます。つまり、標準提供のインデックスが変更された場合、何もする必要はありません。 ただし、後でインデックスを再びカスタマイズすることは可能です。

| 索引 | 標準提供インデックス | バージョン 2 で使用 | バージョン 3 で使用 |
|---|---|---|---|
| /oak:index/damAssetLucene-custom-1 | 可（カスタマイズ） | はい | いいえ |
| /oak:index/damAssetLucene-2-custom-1 | 可（damAssetLucene-custom-1 および damAssetLucene-2 から自動的に結合） | いいえ | はい |
| /oak:index/cqPageLucene | はい | はい | いいえ |
| /oak:index/cqPageLucene-2 | はい | いいえ | はい |

### 現在の制限事項 {#current-limitations}

インデックス管理は、型のインデックスに対してのみサポートされます `lucene`、を `compatVersion` に設定 `2`. 内部的には、例えば Elasticsearch インデックスなどの他のインデックスが設定され、クエリに使用される場合があります。`damAssetLucene` インデックスに対して書き込まれるクエリは、AEM as a Cloud Serviceでは、実際には、このインデックスの Elasticsearch バージョンに対して実行される場合があります。 この違いは、アプリケーションのエンドユーザーには見えませんが、 `explain` 機能は、異なるインデックスをレポートします。 Lucene インデックスと Elasticsearch インデックスの違いについては、[Apache Jackrabbit Oak の Elasticsearch ドキュメント](https://jackrabbit.apache.org/oak/docs/query/elastic.html)を参照してください。顧客が Elasticsearch インデックスを直接設定することはできず、またその必要もありません。

組み込みのアナライザーのみがサポートされます（つまり、製品に付属しているアナライザー）。 カスタムアナライザーはサポートされていません。

最高のオペレーショナルパフォーマンスを得るには、インデックスを過度に大きくしないようにします。 すべてのインデックスの合計サイズは、ガイドとして使用できます。 開発環境で標準インデックスを調整した後、このサイズが 100%以上増加し、カスタムインデックス定義を調整する必要があります。 AEM as a Cloud Service を使用すると、システムの安定性とパフォーマンスに悪影響を与える可能性のあるインデックスのデプロイメントを防ぐことができます。

### インデックスの追加 {#adding-an-index}

という名前の完全なカスタムインデックスを追加するには `/oak:index/acme.product-custom-1`を新しいバージョンのアプリケーション以降で使用するには、インデックスを次のように設定する必要があります。

`acme.product-1-custom-1`

この設定は、インデックス名の前にカスタム識別子を付け、その後にドット (**`.`**) をクリックします。 識別子の長さは 2 ～ 5 文字にする必要があります。

上記のように、この設定では、新しいバージョンのアプリケーションでのみインデックスが使用されます。

### インデックスの変更 {#changing-an-index}

既存のインデックスを変更する場合は、変更したインデックス定義を使用して新しいインデックスを追加する必要があります。 例えば、既存のインデックス `/oak:index/acme.product-custom-1` が変更されるとします。古いインデックスは `/oak:index/acme.product-custom-1` 下に、新しいインデックスは `/oak:index/acme.product-custom-2` 下に格納されます。

アプリケーションの古いバージョンでは、次の設定を使用します。

`/oak:index/acme.product-custom-1`

新しいバージョンのアプリケーションでは、次の（変更された）設定が使用されます。

`/oak:index/acme.product-custom-2`

>[!NOTE]
>
>AEM as a Cloud Service のインデックス定義が、ローカル開発インスタンスのインデックス定義と完全には一致しない場合があります。開発インスタンスには Tika 設定がありませんが、AEMas a Cloud Serviceインスタンスには Tika 設定があります。 Tika 設定でインデックスをカスタマイズする場合は、Tika 設定を保持します。

### 変更の取り消し {#undoing-a-change}

インデックス定義の変更を取り消す必要が生じる場合があります。 これは、不注意なエラーが原因で発生するか、変更が不要になったためです。 例えば、インデックス定義を取得します。 `damAssetLucene-8-custom-3,` は誤って作成され、既にデプロイされています。 その結果、以前のインデックス定義に戻す必要が生じます。 `damAssetLucene-8-custom-2.` これをおこなうには、という名前の新しいインデックスを導入する必要があります。 `damAssetLucene-8-custom-4` 以前のインデックスから定義を組み込む `damAssetLucene-8-custom-2.`

### インデックスの削除 {#removing-an-index}

次の操作は、カスタムインデックスにのみ適用されます。製品インデックスは AEM で使用されるので、削除できません。

新しいバージョンのアプリケーションでインデックスが削除された場合は、新しい名前で空のインデックス（使用されることがなく、データを含まない空のインデックス）を定義できます。 この例では、 `/oak:index/acme.product-custom-3`. この名前は、インデックスを置き換えます。 `/oak:index/acme.product-custom-2`. 後 `/oak:index/acme.product-custom-2` がシステムによって削除された場合、空のインデックス `/oak:index/acme.product-custom-3` その後、を削除できます。 このような空のインデックスの例を次に示します。

```xml
<acme.product-custom-3
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
</acme.product-custom-3>
```

標準提供のインデックスをカスタマイズする必要がなくなった場合は、標準提供のインデックス定義をコピーする必要があります。例えば、既に `damAssetLucene-8-custom-3` をデプロイしていて、カスタマイズが不要になり、デフォルトの `damAssetLucene-8` インデックスに戻す場合は、`damAssetLucene-8` のインデックス定義を含んだインデックス `damAssetLucene-8-custom-4` を追加する必要があります。

## インデックスとクエリの最適化 {#index-query-optimizations}

Apache Jackrabbit Oak では、柔軟なインデックス設定により検索クエリを効率的に処理できます。大規模なリポジトリーでは、インデックスは特に重要です。すべてのクエリが適切なインデックスでバックアップされていることを確認します。 適切なインデックスのないクエリは、数千のノードを読み取り、警告として記録される場合があります。

詳しくは、 [このドキュメント](query-and-indexing-best-practices.md) クエリとインデックスを最適化する方法について詳しくは、を参照してください。
