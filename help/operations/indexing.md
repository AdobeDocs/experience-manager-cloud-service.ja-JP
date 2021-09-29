---
title: コンテンツの検索とインデックス作成
description: コンテンツの検索とインデックス作成
exl-id: 4fe5375c-1c84-44e7-9f78-1ac18fc6ea6b
source-git-commit: 6e8ea8c4db2004ed26ee0cd6c5c3d047c3a1815b
workflow-type: tm+mt
source-wordcount: '2061'
ht-degree: 85%

---

# コンテンツの検索とインデックス作成 {#indexing}

## AEM as a Cloud Service の変更点 {#changes-in-aem-as-a-cloud-service}

AEM as a Cloud Service によって、アドビは AEM インスタンス中心モデルから、Cloud Manager の CI/CD パイプラインによって駆動される、n-x AEM コンテナを持つサービスベースの表示に移行します。単一の AEM インスタンスでインデックスを設定および保守する代わりに、デプロイメントの前にインデックス設定を指定する必要があります。本番環境での設定変更は、CI/CD のポリシーを明らかに破るものです。インデックスの変更についても同じことが言えます。実稼働環境に移行する前にテストおよび再インデックスを指定しない場合、システムの安定性とパフォーマンスに影響を及ぼす可能性があるからです。

AEM 6.5 以前のバージョンと比較した主な変更点のリストを以下に示します。

1. 単一の AEM インスタンスのインデックスマネージャーにアクセスできなくなり、インデックスのデバッグ、設定、または維持ができなくなります。ローカルデプロイメントおよびオンプレミスデプロイメントにのみ使用されます。

1. 単一の AEM インスタンスのインデックスを変更したり、整合性チェックや再インデックスについて心配する必要はありません。

1. 一般に、Cloud Manager の CI/CD パイプラインの品質の高いゲートウェイを迂回せず、実稼働環境のビジネス KPI に影響を与えないように、インデックスの変更は実稼働環境に移行する前に開始されます。

1. 実稼働環境での検索パフォーマンスを含むすべての関連指標は、検索とインデックスのトピックの全体的な表示を提供するために、実行時に顧客が利用できます。

1. 顧客は、必要に応じてアラートを設定できます。

1. SRE はシステムの正常性を 24 時間 365 日監視しており、必要に応じて可能な限り早急に対処します。

1. インデックスの設定は、デプロイメントを介して変更されます。インデックス定義の変更は、他のコンテンツの変更と同様に設定されます。

1. AEM as a Cloud Service の高レベルでは、[Blue-Green デプロイメントモデルが導入され](#index-management-using-blue-green-deployments)、1 つは古いバージョン用のセット（青）、もう 1 つは新しいバージョン用のセット（緑）の 2 組のインデックスが存在します。

1. Cloud Manager のビルドページで、顧客はインデックス作成ジョブが完了したかどうかを確認できます。新しいバージョンでトラフィックを引き受ける準備ができたら、通知を受け取ります。

1. 制限事項：
* 現在、AEM as aCloud Serviceのインデックス管理は、luceneタイプのインデックスに対してのみサポートされています。
* 標準のアナライザーのみがサポートされます（つまり、製品に付属しているアナライザー）。 カスタムアナライザーはサポートされていません。

## 使用方法 {#how-to-use}

インデックスの定義は、次の 3 つのユースケースで構成できます。

1. 新しい顧客インデックス定義の追加
1. 既存のインデックス定義の更新。これは、既存のインデックス定義の新しいバージョンを追加することを意味します
1. 冗長または古い既存のインデックスの削除。

上記のポイント 1 と 2 の両方について、それぞれの Cloud Manager リリーススケジュールで、カスタムコードベースの一部として新しいインデックス定義を作成する必要があります。詳しくは、[AEM as a Cloud Service へのデプロイ](/help/implementing/deploying/overview.md)ドキュメントを参照してください。

### 新しいインデックス定義の準備 {#preparing-the-new-index-definition}

>[!NOTE]
>
>標準提供のインデックス（`damAssetLucene-6`など）をカスタマイズする場合は、*Cloud Service 環境*&#x200B;から最新の標準提供インデックス定義をコピーして、それをカスタマイズしてください。これにより、必要な設定が誤って削除されることを防ぐことができます。例えば、`/oak:index/damAssetLucene-6/tika` の下の `tika` ノードは必須ノードで、カスタマイズしたインデックスにも含める必要があり、Cloud SDK には存在しません。

次の命名パターンに従って、実際のインデックス定義を含む新しいインデックス定義パッケージを準備する必要があります。

`<indexName>[-<productVersion>]-custom-<customVersion>`

それらは `ui.apps/src/main/content/jcr_root` の下に置く必要があります。現在、サブルートフォルダーはサポートされていません。

上記のサンプルのパッケージは、`com.adobe.granite:new-index-content:zip:1.0.0-SNAPSHOT` としてビルドされます。

>[!NOTE]
>
>インデックス定義を含んだコンテンツパッケージには、コンテンツパッケージのプロパティファイル（`/META-INF/vault/properties.xml`）で次のプロパティを設定する必要があります。
>
>`noIntermediateSaves=true`

### 索引定義のデプロイ {#deploying-index-definitions}

>[!NOTE]
>
>Jackrabbit Filevault Maven パッケージプラグインバージョン **1.1.0** には既知の問題があり、`<packageType>application</packageType>` のモジュール `oak:index` に追加できません。そのプラグインのより新しいバージョンに更新する必要があります。

インデックス定義は、カスタムおよびバージョン付きとしてマークされるようになりました。

* インデックス定義自体（例 `/oak:index/ntBaseLucene-custom-1`）

したがって、インデックスをデプロイするには、インデックス定義（`/oak:index/definitionname`）を Git および Cloud Manager のデプロイメントプロセスを使用して `ui.apps` 経由で配信する必要があります。

新しいインデックス定義を追加したら、Cloud Manager を使用して新しいアプリケーションをデプロイする必要があります。デプロイメントを開始すると、2 つのジョブが開始され、それぞれ MongoDB と Azure Segment Store にオーサー用とパブリッシュ用のインデックス定義を追加（また必要に応じて結合）します。Blue-Green スイッチが起こる前に、基になるリポジトリーのインデックスが新しいインデックス定義で再作成されています。

>[!TIP]
>
>AEM as a Cloud Service を使用する場合に必要なパッケージ構造の詳細については、[AEM プロジェクト構造](/help/implementing/developing/introduction/aem-project-content-package-structure.md)ドキュメントを参照してください。

## Blue-Green デプロイメントを使用したインデックス管理 {#index-management-using-blue-green-deployments}

### インデックス管理とは {#what-is-index-management}

インデックス管理とは、インデックスの追加、削除、変更を行うことです。インデックスの&#x200B;*定義*&#x200B;変更はすぐにできますが、変更を適用する（「インデックスの構築」、または既存インデックスの場合は「インデックスの再構築」と呼ばれる）には時間が必要です。これは即時には実行されません。インデックスを作成するデータをリポジトリーでスキャンする必要があります。

### Blue-Green デプロイメントとは {#what-is-blue-green-deployment}

Blue-Green デプロイメントは、ダウンタイムを短縮できます。また、ダウンタイムをゼロにするアップグレードも可能で、高速なロールバックが可能です。アプリケーションの古いバージョン（青）は、アプリケーションの新しいバージョン（緑）と同時に実行されます。

### 読み取り専用領域と読み取り／書き込み可能領域 {#read-only-and-read-write-areas}

リポジトリーの特定の領域（リポジトリーの読み取り専用の部分）は、古い（青い）バージョンと新しい（緑の）バージョンで異なる場合があります。リポジトリーの読み取り専用領域は、通常、「`/app`」と「`/libs`」です。次の例では、読み取り専用領域に斜体を使用し、読み取り／書き込み可能領域に太字を使用します。

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

### Blue-Green デプロイメントを使用しないインデックス管理 {#index-management-without-blue-green-deployment}

開発中、またはオンプレミスインストールを使用する場合は、インデックスを実行時に追加、削除または変更できます。インデックスは、利用可能になるとすぐに使用されます。まだ古いバージョンのアプリケーションでインデックスを使用することを想定していない場合は、通常、予定されたダウンタイム中にインデックスが構築されます。インデックスの削除時や、既存のインデックスの変更時にも同じことが起こります。インデックスを削除すると、ただちに使用できなくなります。

### Blue-Green デプロイメントによるインデックス管理 {#index-management-with-blue-green-deployment}

Blue-Green デプロイメントでは、ダウンタイムは発生しません。ただし、インデックス管理の場合は、インデックスが特定のバージョンのアプリケーションでのみ使用される必要があります。例えば、アプリケーションのバージョン 2 でインデックスを追加する場合に、アプリケーションのバージョン 1 ではまだインデックスを使用したくないことがあります。逆に、インデックスを削除する場合に、バージョン 2 で削除したインデックスがバージョン 1 ではまだ必要なことがあります。インデックス定義を変更する場合、古いバージョンのインデックスをバージョン 1 でのみ使用し、新しいバージョンのインデックスをバージョン 2 でのみ使用します。

次の表に、5 つのインデックス定義を示します。インデックス `cqPageLucene` は両方のバージョンで使用され、インデックス `damAssetLucene-custom-1` はバージョン 2 でのみ使用されます。

>[!NOTE]
>
>`<indexName>-custom-<customerVersionNumber>` は、既存のインデックスの代わりとしてマークするために、AEM as a Cloud Service で必要です。

| 索引 | 標準提供インデックス | バージョン 1 で使用 | バージョン 2 で使用 |
|---|---|---|---|
| /oak:index/damAssetLucene | 可 | 可 | 不可 |
| /oak:index/damAssetLucene-custom-1 | 可（カスタマイズ） | 不可 | 可 |
| /oak:index/acme.product-custom-1 | 不可 | 可 | 不可 |
| /oak:index/acme.product-custom-2 | 不可 | 不可 | 可 |
| /oak:index/cqPageLucene | 可 | 可 | 可 |

バージョン番号は、インデックスが変更されるたびに増加します。製品自体のインデックス名と衝突するカスタムインデックス名を回避するには、カスタムインデックスと、標準提供のインデックスの変更を `-custom-<number>` で終える必要があります。

### 標準提供のインデックスの変更 {#changes-to-out-of-the-box-indexes}

アドビが「damAssetLucene」や「cqPageLucene」のような標準提供のインデックスを変更すると、`damAssetLucene-2` または `cqPageLucene-2` という名前の新しいインデックスが作成されます。また、インデックスが既にカスタマイズされている場合は、次のように、カスタマイズされたインデックス定義が標準提供のインデックス変更と結合されます。変更のマージは自動的に行われます。つまり、標準提供のインデックスが変更された場合、何もする必要はありません。ただし、後でインデックスを再びカスタマイズすることは可能です。

| 索引 | 標準提供インデックス | バージョン 2 で使用 | バージョン 3 で使用 |
|---|---|---|---|
| /oak:index/damAssetLucene-custom-1 | 可（カスタマイズ） | 可 | 不可 |
| /oak:index/damAssetLucene-2-custom-1 | 可（damAssetLucene-custom-1 および damAssetLucene-2 から自動的に結合） | 不可 | 可 |
| /oak:index/cqPageLucene | 可 | 可 | 不可 |
| /oak:index/cqPageLucene-2 | 可 | 不可 | 可 |

### 現在の制限事項 {#current-limitations}

インデックス管理は、現在、`lucene` 型のインデックスに対してのみサポートされています。

### インデックスの追加 {#adding-an-index}

新しいバージョン以降のアプリケーションで使用する `/oak:index/acme.product-custom-1` という名前のインデックスを追加するには、インデックスを次のように設定する必要があります。

`acme.product-1-custom-1`

これは、インデックス名の前にカスタム識別子を付け、その後にドット（**`.`**）を付けることで機能します。識別子の長さは 2～5 文字です。

これにより、新しいバージョンのアプリケーションでのみインデックスが使用されます。

### インデックスの変更 {#changing-an-index}

既存のインデックスを変更する場合は、変更したインデックス定義を使用して新しいインデックスを追加する必要があります。例えば、既存のインデックス `/oak:index/acme.product-custom-1` が変更されるとします。古いインデックスは `/oak:index/acme.product-custom-1` 下に、新しいインデックスは `/oak:index/acme.product-custom-2` 下に格納されます。

アプリケーションの古いバージョンでは、次の設定を使用します。

`/oak:index/acme.product-custom-1`

新しいバージョンのアプリケーションでは、次の（変更された）設定が使用されます。

`/oak:index/acme.product-custom-2`

>[!NOTE]
>
>AEM as a Cloud Service のインデックス定義が、ローカル開発インスタンスのインデックス定義と完全には一致しない場合があります。開発インスタンスには Tika 設定がありませんが、AEM as a Cloud Service インスタンスには Tika 設定があります。Tika 設定でインデックスをカスタマイズする場合は、その Tika 設定を保持してください。

### 変更の取り消し {#undoing-a-change}

インデックス定義の変更を元に戻す必要が生じる場合があります。誤って変更が加えられたり、変更が不要になったなどの理由によります。例えば、インデックス定義 `damAssetLucene-8-custom-3` は誤って作成され、既にデプロイされているとします。そのため、以前のインデックス定義 `damAssetLucene-8-custom-2` に戻す必要があります。それには、前のインデックス `damAssetLucene-8-custom-2` の定義を含んだ `damAssetLucene-8-custom-4` という新しいインデックスを追加する必要があります。

### インデックスの削除 {#removing-an-index}

次の操作は、カスタムインデックスにのみ適用されます。製品インデックスは AEM で使用されるので、削除できません。

新しいバージョンのアプリケーションでインデックスを削除する場合は、新しい名前で空のインデックス（使用されることがなく、データを含まない空のインデックス）を定義できます。この例では、`/oak:index/acme.product-custom-3` という名前を付けることができます。これにより、`/oak:index/acme.product-custom-2` インデックスが置き換えられます。システムによって `/oak:index/acme.product-custom-2` が削除された後は、空のインデックス `/oak:index/acme.product-custom-3` も削除できます。このような空のインデックスの例を次に示します。

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

## インデックスの最適化

Apache Jackrabbit Oakを使用すると、柔軟なインデックス設定で検索クエリを効率的に処理できます。 インデックスは、大きなリポジトリで特に重要です。 最適化されていないインデックスとフォールバックインデックスは、できるだけ避ける必要があります。 すべてのクエリが適切なインデックスでバックアップされていることを確認してください。 適切なインデックスがないクエリは、数千のノードを読み取り、警告としてログに記録されます。 インデックス定義を最適化できるように、ログファイルを分析することで、このようなクエリを識別する必要があります。 詳しくは、[このページ](https://experienceleague.adobe.com/docs/experience-manager-65/deploying/practices/best-practices-for-queries-and-indexing.html?lang=en#tips-for-creating-efficient-indexes)を参照してください。

### AEM as aCloud ServiceのLuceneフルテキストインデックス

フルテキストインデックス`/oak:index/lucene-2`は、デフォルトでAEMリポジトリ内のすべてのノードのインデックスを作成するので、非常に大きくなる場合があります。 Luceneフルテキストインデックスは内部的に廃止され、2021年9月以降、AEMではCloud Serviceとしてデプロイされなくなります。 したがって、AEM as aCloud Serviceでは製品側で使用されなくなり、顧客コードを実行する必要がなくなりました。 共通のLuceneインデックスを持つCloud Service環境としてのAEMの場合、Adobeは、このインデックスを補い、最適化されたより優れたインデックスを使用するための調整されたアプローチをお客様と個別に提供します。 このインデックスがカスタムクエリに必要な場合は、一時的なソリューションとして、このインデックスのコピーを別の名前（例：[here](/help/operations/indexing.md)）で作成する必要があります。
`/oak:index/acme.lucene-1-custom-1`この最適化は、Adobeの指示がない限り、オンプレミスでホストされる、またはAdobe Managed Servicesで管理される他のAEM環境には適用されません。
