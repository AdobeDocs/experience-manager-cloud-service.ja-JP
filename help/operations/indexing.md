---
title: コンテンツの検索とインデックス作成
description: コンテンツの検索とインデックス作成
exl-id: 4fe5375c-1c84-44e7-9f78-1ac18fc6ea6b
source-git-commit: 1994b90e3876f03efa571a9ce65b9fb8b3c90ec4
workflow-type: tm+mt
source-wordcount: '2427'
ht-degree: 42%

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
1. AEMas a Cloud Serviceの概要と、 [ローリングデプロイメントモデル](#index-management-using-rolling-deployments)には、2 組のインデックスが存在します。1 つは古いバージョン用、もう 1 つは新しいバージョン用です。
1. Cloud Manager のビルドページで、インデックス作成ジョブが完了したかどうかを確認できます。新しいバージョンでトラフィックを引き受ける準備ができたら、通知を受け取ります。

制限事項：

* 現在、AEM as a Cloud Service のインデックス管理は、`lucene` 型のインデックスに対してのみサポートされています。
* 標準のアナライザーのみがサポートされます（つまり、製品に付属しているアナライザー）。 カスタムアナライザーはサポートされていません。
* 内部的には、他のインデックスがクエリに設定され使用される可能性があります。例えば、`damAssetLucene` インデックスに対して記述されたクエリは、Skyline 上では実際には、このインデックスの Elasticsearch バージョンに対して実行される可能性があります。この違いは、通常、アプリケーションとユーザーには表示されませんが、 `explain` 機能は、別のインデックスをレポートします。 Lucene インデックスと Elasticsearch インデックスの違いについては、[Apache Jackrabbit Oak の Elastic 関連ドキュメント](https://jackrabbit.apache.org/oak/docs/query/elastic.html)を参照してください。お客様は、Elasticsearchインデックスを直接設定する必要はなく、または設定できません。

## 使用方法 {#how-to-use}

インデックスの定義は、次の 3 つの使用例で構成できます。

1. 顧客インデックス定義の追加。
1. 既存のインデックス定義の更新。この更新は、既存のインデックス定義の新しいバージョンが追加されることを意味します。
1. 冗長または古い既存のインデックスの削除。

上記のポイント 1 と 2 の両方で、それぞれの Cloud Manager リリーススケジュールで、カスタムコードベースの一部としてインデックス定義を作成する必要があります。 詳しくは、 [AEMへのデプロイas a Cloud Serviceドキュメント](/help/implementing/deploying/overview.md).

## インデックス名 {#index-names}

インデックスの定義は、以下のいずれかになります。

1. 標準提供のインデックス。例として、`/oak:index/cqPageLucene-2` があります。
1. 標準提供のインデックスのカスタマイズ。お客様がカスタマイズを定義できます。例として、`/oak:index/cqPageLucene-2-custom-1` があります。
1. 完全なカスタムインデックス。例として、`/oak:index/acme.product-1-custom-2` があります。名前の競合を避けるために、Adobeでは、完全なカスタムインデックスにプレフィックスが付いている必要があります（例： ）。 `acme.`

標準提供のインデックスと完全カスタムインデックスの両方をカスタマイズする場合は、にが含まれている必要があります `-custom-`. 完全なカスタムインデックスのみ、プレフィックスで始める必要があります。

## 新しいインデックス定義の準備 {#preparing-the-new-index-definition}

>[!NOTE]
>
>標準提供のインデックスをカスタマイズする場合（例： ） `damAssetLucene-6`に設定する場合は、そのまま使用できる最新のインデックス定義を *Cloud Service環境* CRX DE パッケージマネージャー (`/crx/packmgr/`) ) をクリックします。 次に、設定の名前を `damAssetLucene-6-custom-1` などに変更し、その上にカスタマイズを追加します。このプロセスにより、必要な設定が誤って削除されるのを防ぎます。 例えば、`/oak:index/damAssetLucene-6/tika` 下のノード `tika` は、Cloud Service のカスタマイズ済みインデックスに必要です。Cloud SDK に存在しません。

次の命名パターンに従って、実際のインデックス定義を含むインデックス定義パッケージを準備します。

`<indexName>[-<productVersion>]-custom-<customVersion>`

それは、次の下に置く必要があります `ui.apps/src/main/content/jcr_root`. カスタマイズされたカスタムインデックス定義は、すべて以下に保存する必要があります。 `/oak:index`.

パッケージのフィルターは、（標準提供のインデックス）既存のインデックスが保持されるように設定する必要があります。 ファイル内 `ui.apps/src/main/content/META-INF/vault/filter.xml`に設定する場合、各カスタム（またはカスタマイズされた）インデックスを次のようにリストする必要があります。 `<filter root="/oak:index/damAssetLucene-6-custom-1"/>`. インデックスのバージョンを後で変更する場合は、フィルターを調整する必要があります。

<!-- Alexandru: temporarily drafting this statement due to CQDOC-17701

The package from the above sample is built as `com.adobe.granite:new-index-content:zip:1.0.0-SNAPSHOT`. -->

>[!NOTE]
>
>インデックス定義を含むコンテンツパッケージでは、次のプロパティをコンテンツパッケージのプロパティファイル ( ) で設定する必要があります。 `/META-INF/vault/properties.xml`:
>
>`noIntermediateSaves=true`

## 索引定義のデプロイ {#deploying-index-definitions}

インデックス定義は、カスタムおよびバージョン付きとしてマークされます。

* インデックス定義自体（例 `/oak:index/ntBaseLucene-custom-1`）

カスタムインデックスまたはカスタマイズされたインデックスを展開するには、インデックス定義 (`/oak:index/definitionname`) は、 `ui.apps` Git および Cloud Manager のデプロイメントプロセスを通じて。 FileVault フィルター、例えば `ui.apps/src/main/content/META-INF/vault/filter.xml` では、カスタムおよびカスタマイズ済みの各インデックスを、`<filter root="/oak:index/damAssetLucene-7-custom-1"/>` のように個別にリストします。その後、カスタムまたはカスタマイズされたインデックス定義自体がファイルに保存されます `ui.apps/src/main/content/jcr_root/_oak_index/damAssetLucene-7-custom-1/.content.xml`、次のようにします。

```xml
<?xml version="1.0" encoding="UTF-8"?>
<jcr:root xmlns:oak="https://jackrabbit.apache.org/oak/ns/1.0" xmlns:dam="http://www.day.com/dam/1.0" xmlns:jcr="http://www.jcp.org/jcr/1.0" xmlns:nt="http://www.jcp.org/jcr/nt/1.0" xmlns:rep="internal"
        jcr:primaryType="oak:QueryIndexDefinition"
        async="[async,nrt]"
        compatVersion="{Long}2"
        ...
        </indexRules>
        <tika jcr:primaryType="nt:unstructured">
            <config.xml jcr:primaryType="nt:file"/>
        </tika>
</jcr:root>
```

上記の例には、Apache Tika の設定が含まれています。Tika 設定ファイルは、`ui.apps/src/main/content/jcr_root/_oak_index/damAssetLucene-7-custom-1/tika/config.xml` に保存されます。

### プロジェクト設定

Jackrabbit Filevault Maven パッケージプラグインを使用するバージョンに応じて、プロジェクトでさらに設定が必要になります。Jackrabbit Filevault Maven パッケージプラグインバージョンの使用時 **1.1.6** またはそれ以降の場合は、ファイル `pom.xml` には、 `filevault-package-maven-plugin`、 `configuration/validatorsSettings` ( `jackrabbit-nodetypes`):

```xml
<jackrabbit-packagetype>
    <options>
        <immutableRootNodeNames>apps,libs,oak:index</immutableRootNodeNames>
    </options>
</jackrabbit-packagetype>
```

また、この場合、 `vault-validation` バージョンを新しいバージョンにアップグレードする必要があります：

```xml
<dependency>
    <groupId>org.apache.jackrabbit.vault</groupId>
    <artifactId>vault-validation</artifactId>
    <version>3.5.6</version>
</dependency>
```

次に、 `ui.apps.structure/pom.xml` および `ui.apps/pom.xml`、 `filevault-package-maven-plugin` は、 `allowIndexDefinitions` および `noIntermediateSaves` 有効。 オプション `noIntermediateSaves` は、インデックス設定が自動的に追加されることを保証します。

```xml
<groupId>org.apache.jackrabbit</groupId>
    <artifactId>filevault-package-maven-plugin</artifactId>
    <configuration>
        <allowIndexDefinitions>true</allowIndexDefinitions>
        <properties>
            <cloudManagerTarget>none</cloudManagerTarget>
            <noIntermediateSaves>true</noIntermediateSaves>
        </properties>
    ...
```

In `ui.apps.structure/pom.xml`、 `filters` このプラグインのセクションには、次のようにフィルタルートを含める必要があります。

```xml
<filter><root>/oak:index</root></filter>
```

新しいインデックス定義を追加した後、新しいアプリケーションは Cloud Manager を使用してデプロイされます。 デプロイメント時には、オーサー用とパブリッシュ用の MongoDB と Azure Segment Store に、それぞれインデックス定義を追加（必要に応じて結合）する 2 つのジョブが開始されます。 スイッチが実行される前に、基になるリポジトリのインデックスが新しいインデックス定義で再作成されます。

### メモ

失敗の検証で次のエラーが発生した場合 <br>
`[ERROR] ValidationViolation: "jackrabbit-nodetypes: Mandatory child node missing: jcr:content [nt:base] inside node with types [nt:file]"` <br>
その後、次のいずれかの手順に従って問題を修正できます。 <br>

1. filevault をバージョン 1.0.4 にダウングレードし、次の内容を最上位 pom に追加します。

```xml
<allowIndexDefinitions>true</allowIndexDefinitions>
```

以下に、上記の設定を POM 内のどこに配置するかの例を示します。

```xml
<plugin>
    <groupId>org.apache.jackrabbit</groupId>
    <artifactId>filevault-package-maven-plugin</artifactId>
    <configuration>
        <properties>
        ...
        </properties>
        ...
        <allowIndexDefinitions>true</allowIndexDefinitions>
        <repositoryStructurePackages>
        ...
        </repositoryStructurePackages>
        <dependencies>
        ...
        </dependencies>
    </configuration>
</plugin>
```

1. ノードタイプ検証を無効にします。 filevault プラグインの設定の jackrabbit-nodetypes セクションで、次のプロパティを設定します。

```xml
<isDisabled>true</isDisabled>
```

以下に、上記の設定を POM 内のどこに配置するかの例を示します。

```xml
<plugin>
    <groupId>org.apache.jackrabbit</groupId>
    <artifactId>filevault-package-maven-plugin</artifactId>
    ...
    <configuration>
    ...
        <validatorsSettings>
        ...
            <jackrabbit-nodetypes>
                <isDisabled>true</isDisabled>
            </jackrabbit-nodetypes>
        </validatorsSettings>
    </configuration>
</plugin>
```

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

ローリングデプロイメントでは、ダウンタイムは発生しません。 更新中のしばらくの間、アプリケーションの古いバージョン（バージョン 1 など）と新しいバージョン（バージョン 2 など）の両方が、同じリポジトリに対して同時に実行されます。 バージョン 1 で特定のインデックスを使用可能にする必要がある場合は、バージョン 2 でこのインデックスを削除しないでください。後でインデックスを削除する必要があります（例：バージョン 3）。その時点で、アプリケーションのバージョン 1 が実行されなくなります。 また、バージョン 2 が実行中で、バージョン 2 のインデックスが使用可能でも、バージョン 1 が正常に動作するようにアプリケーションを作成してください。

新しいバージョンへのアップグレードが完了した後、システムが古いインデックスをガベージコレクションできます。古いインデックスは、ロールバックを高速化するために、しばらくの間保持される場合があります（ロールバックが必要な場合）。

次の表に、5 つのインデックス定義を示します。インデックス `cqPageLucene` は両方のバージョンで使用され、インデックス `damAssetLucene-custom-1` はバージョン 2 でのみ使用されます。

>[!NOTE]
>
>この `<indexName>-custom-<customerVersionNumber>` は、既存のインデックスの代わりとしてマークするためにAEM as a Cloud Serviceで必要です。

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

インデックス管理は、型のインデックスに対してのみサポートされます `lucene`を `compatVersion` に設定 `2`. 内部的には、例えば Elasticsearch インデックスなどの他のインデックスが設定され、クエリに使用される場合があります。`damAssetLucene` インデックスに対して書き込まれるクエリは、AEM as a Cloud Serviceでは、実際には、このインデックスの Elasticsearch バージョンに対して実行される場合があります。 この違いは、アプリケーションのエンドユーザーには見えませんが、 `explain` 機能は、異なるインデックスをレポートします。 Lucene インデックスと Elasticsearch インデックスの違いについては、[Apache Jackrabbit Oak の Elasticsearch ドキュメント](https://jackrabbit.apache.org/oak/docs/query/elastic.html)を参照してください。顧客が Elasticsearch インデックスを直接設定することはできず、またその必要もありません。

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

インデックス定義の変更を元に戻す必要が生じる場合があります。 誤って変更が加えられたり、変更が不要になったなどの理由によります。例えば、インデックス定義 `damAssetLucene-8-custom-3` は誤って作成され、既にデプロイされているとします。そのため、以前のインデックス定義 `damAssetLucene-8-custom-2` に戻す必要があります。これをおこなうには、 `damAssetLucene-8-custom-4` 前のインデックスの定義を含む `damAssetLucene-8-custom-2`.

### インデックスの削除 {#removing-an-index}

次の操作は、カスタムインデックスにのみ適用されます。製品インデックスは AEM で使用されるので、削除できません。

新しいバージョンのアプリケーションでインデックスが削除された場合は、新しい名前で空のインデックス（使用されることがなく、データを含まない空のインデックス）を定義できます。 この例では、 `/oak:index/acme.product-custom-3`. この名前は、インデックスを置き換えます `/oak:index/acme.product-custom-2`. 後 `/oak:index/acme.product-custom-2` がシステムによって削除された場合、空のインデックス `/oak:index/acme.product-custom-3` その後、を削除できます。 このような空のインデックスの例を次に示します。

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
