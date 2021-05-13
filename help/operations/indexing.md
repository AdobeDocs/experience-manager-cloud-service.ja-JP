---
title: コンテンツの検索とインデックス作成
description: コンテンツの検索とインデックス作成
exl-id: 4fe5375c-1c84-44e7-9f78-1ac18fc6ea6b
source-git-commit: 16afabcd80f9014684a5d3428a65d8b2c41c69c8
workflow-type: tm+mt
source-wordcount: '1829'
ht-degree: 69%

---

# コンテンツの検索とインデックス作成 {#indexing}

## AEM as a Cloud Service の変更点 {#changes-in-aem-as-a-cloud-service}

AEMをCloud Serviceとして使用すると、Adobeは、AEMインスタンス中心のモデルから、n-x AEMコンテナを持つサービスベースの表示に移行し、Cloud ManagerのCI/CDパイプラインによって駆動されます。 単一の AEM インスタンスでインデックスを設定および保守する代わりに、デプロイメントの前にインデックス設定を指定する必要があります。本番環境での設定変更は、CI/CD のポリシーを明らかに破るものです。インデックスの変更についても同じことが言えます。システムの安定性とパフォーマンスに影響を与える可能性があるのは、実稼働環境に移行する前に、テストおよび再インデックスを指定しない場合です。

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

1. 制限事項：現在、AEM as a Cloud Service のインデックス管理は、lucene 型のインデックスに対してのみサポートされています。

## 使用方法 {#how-to-use}

インデックスの定義は、次の3つの使用例で構成できます。

1. 新しい顧客インデックス定義の追加
1. 既存のインデックス定義の更新。これは、既存のインデックス定義の新しいバージョンを追加することを意味します
1. 冗長または古い既存のインデックスの削除。

上記のポイント 1 と 2 の両方について、それぞれの Cloud Manager リリーススケジュールで、カスタムコードベースの一部として新しいインデックス定義を作成する必要があります。詳しくは、[AEM as a Cloud Service へのデプロイ](/help/implementing/deploying/overview.md)ドキュメントを参照してください。

### 新しいインデックス定義の準備{#preparing-the-new-index-definition}

>[!NOTE]
>
>初期設定のインデックス（例：`damAssetLucene-6`）をカスタマイズする場合は、*Cloud Service環境*&#x200B;から初期設定のインデックス定義の最新のものをコピーし、カスタマイズ内容を上に追加してください。 例えば、`/oak:index/damAssetLucene-6/tika`の下の`tika`ノードは必須のノードで、カスタマイズしたインデックスの一部にする必要があり、Cloud SDKには存在しません。

次の命名パターンに従って、実際のインデックス定義を含む新しいインデックス定義パッケージを準備する必要があります。

`<indexName>[-<productVersion>]-custom-<customVersion>`

それらは `ui.apps/src/main/content/jcr_root` の下に置く必要があります。現在、サブルートフォルダーはサポートされていません。

上記のサンプルのパッケージは、`com.adobe.granite:new-index-content:zip:1.0.0-SNAPSHOT` としてビルドされます。

>[!NOTE]
>
>インデックス定義を含むコンテンツパッケージは、コンテンツパッケージのプロパティファイル内の`/META-INF/vault/properties.xml`に次のプロパティを設定する必要があります。
>
>`noIntermediateSaves=true`

### 索引定義のデプロイ {#deploying-index-definitions}

>[!NOTE]
>
>Jackrabbit Filevault Maven パッケージプラグインバージョン **1.1.0** には既知の問題があり、`<packageType>application</packageType>` のモジュール `oak:index` に追加できません。この問題に対処するには、バージョン **1.0.4 を使用してください**。

インデックス定義は、カスタムおよびバージョン付きとしてマークされるようになりました。

* インデックス定義自体（例 `/oak:index/ntBaseLucene-custom-1`）

したがって、インデックスをデプロイするには、インデックス定義（`/oak:index/definitionname`）を Git および Cloud Manager のデプロイメントプロセスを使用して `ui.apps` 経由で配信する必要があります。

新しいインデックス定義を追加したら、Cloud Manager を使用して新しいアプリケーションをデプロイする必要があります。デプロイメントを開始すると、2 つのジョブが開始され、それぞれ MongoDB と Azure Segment Store にオーサー用とパブリッシュ用のインデックス定義を追加（また必要に応じて結合）します。Blue-Green スイッチが起こる前に、基になるリポジトリのインデックスが新しいインデックス定義で再作成されています。

>[!TIP]
>
>AEM as a Cloud Service を使用する場合に必要なパッケージ構造の詳細については、[AEM プロジェクト構造](/help/implementing/developing/introduction/aem-project-content-package-structure.md)ドキュメントを参照してください。

## Blue-Green デプロイメントを使用したインデックス管理 {#index-management-using-blue-green-deployments}

### インデックス管理とは {#what-is-index-management}

インデックス管理とは、インデックスの追加、削除、変更を行うことです。インデックスの&#x200B;*定義*&#x200B;変更はすぐにできますが、変更を適用する（「インデックスの構築」、または既存インデックスの場合は「インデックスの再構築」と呼ばれる）には時間が必要です。これは即時には実行されません。インデックスを作成するデータをリポジトリでスキャンする必要があります。

### Blue-Green デプロイメントとは {#what-is-blue-green-deployment}

Blue-Green デプロイメントは、ダウンタイムを短縮できます。また、ダウンタイムをゼロにするアップグレードも可能で、高速なロールバックが可能です。アプリケーションの古いバージョン（青）は、アプリケーションの新しいバージョン（緑）と同時に実行されます。

### 読み取り専用領域と読み取り／書き込み可能領域 {#read-only-and-read-write-areas}

リポジトリの特定の領域（リポジトリの読み取り専用の部分）は、古い（青い）バージョンと新しい（緑の）バージョンで異なる場合があります。リポジトリの読み取り専用領域は、通常、「`/app`」と「`/libs`」です。次の例では、読み取り専用領域に斜体を使用し、読み取り／書き込み可能領域に太字を使用します。

* **/**
* */apps（読み取り専用）*
* **/content**
* */libs（読み取り専用）*
* **/oak:index**
* **/oak:index/acme.**
* **/jcr:system**
* **/system**
* **/var**

リポジトリの読み取り/書き込み領域は、アプリケーションのすべてのバージョン間で共有されますが、アプリケーションの各バージョンには、`/apps` と `/libs` の固有のセットがあります。

### Blue-Green デプロイメントを使用しないインデックス管理 {#index-management-without-blue-green-deployment}

開発中、またはオンプレミスインストールを使用する場合は、インデックスを実行時に追加、削除または変更できます。インデックスは、利用可能になるとすぐに使用されます。まだ古いバージョンのアプリケーションでインデックスを使用することを想定していない場合は、通常、予定されたダウンタイム中にインデックスが構築されます。インデックスの削除時や、既存のインデックスの変更時にも同じことが起こります。インデックスを削除すると、ただちに使用できなくなります。

### Blue-Green デプロイメントによるインデックス管理 {#index-management-with-blue-green-deployment}

Blue-Green デプロイメントでは、ダウンタイムは発生しません。ただし、インデックス管理の場合は、インデックスが特定のバージョンのアプリケーションでのみ使用される必要があります。例えば、アプリケーションのバージョン 2 でインデックスを追加する場合に、アプリケーションのバージョン 1 ではまだインデックスを使用したくないことがあります。逆に、インデックスを削除する場合に、バージョン 2 で削除したインデックスがバージョン 1 ではまだ必要なことがあります。インデックス定義を変更する場合、古いバージョンのインデックスをバージョン 1 でのみ使用し、新しいバージョンのインデックスをバージョン 2 でのみ使用します。

次の表に、5つのインデックス定義を示します。index `cqPageLucene`は両方のバージョンで使用され、index `damAssetLucene-custom-1`はバージョン2でのみ使用されます。

>[!NOTE]
>
>`<indexName>-custom-<customerVersionNumber>` は、既存のインデックスの代わりとしてマークするために、AEM as a Cloud Service で必要です。

| 索引 | 標準提供インデックス | バージョン 1 で使用 | バージョン 2 で使用 |
|---|---|---|---|
| /oak:index/damAssetLucene | 可 | 可 | いいえ |
| /oak:index/damAssetLucene-custom-1 | 可（カスタマイズ） | 不可 | 可 |
| /oak:index/acme.product-custom-1 | 不可 | はい | いいえ |
| /oak:index/acme.product-custom-2 | 不可 | 不可 | 可 |
| /oak:index/cqPageLucene | 可 | 可 | 可 |

バージョン番号は、インデックスが変更されるたびに増加します。製品自体のインデックス名と衝突するカスタムインデックス名を避けるために、カスタムインデックスと、初期設定のインデックスの変更は`-custom-<number>`で終わる必要があります。

### 標準提供のインデックスの変更 {#changes-to-out-of-the-box-indexes}

アドビが「damAssetLucene」や「cqPageLucene」のような標準提供のインデックスを変更すると、`damAssetLucene-2` または `cqPageLucene-2` という名前の新しいインデックスが作成されます。また、インデックスが既にカスタマイズされている場合は、次のように、カスタマイズされたインデックス定義が標準提供のインデックス変更と結合されます。変更のマージは自動的におこなわれます。つまり、標準提供のインデックスが変更された場合、何もする必要はありません。ただし、後でインデックスを再びカスタマイズすることは可能です。

| 索引 | 標準提供インデックス | バージョン 2 で使用 | バージョン 3 で使用 |
|---|---|---|---|
| /oak:index/damAssetLucene-custom-1 | 可（カスタマイズ） | 可 | いいえ |
| /oak:index/damAssetLucene-2-custom-1 | はい（damAssetLucene-custom-1 および damAssetLucene-2 から自動的に結合） | 不可 | 可 |
| /oak:index/cqPageLucene | 可 | 可 | いいえ |
| /oak:index/cqPageLucene-2 | 可 | いいえ | 可 |

### 現在の制限{#current-limitations}

インデックス管理は、現在、`lucene` 型のインデックスに対してのみサポートされています。

### インデックスの追加 {#adding-an-index}

`/oak:index/acme.product-custom-1`という名前のインデックスを追加して、新しいバージョンのアプリケーション以降で使用するには、次のようにインデックスを設定する必要があります。

`acme.product-1-custom-1`

これは、インデックス名の前にカスタム識別子を付け、その後にドット（**`.`**）を付けることで機能します。識別子の長さは 2～5 文字です。

これにより、新しいバージョンのアプリケーションでのみインデックスが使用されます。

### インデックスの変更 {#changing-an-index}

既存のインデックスを変更する場合は、変更したインデックス定義を使用して新しいインデックスを追加する必要があります。例えば、既存のインデックス`/oak:index/acme.product-custom-1`が変更されているとします。 古いインデックスは `/oak:index/acme.product-custom-1` 下に、新しいインデックスは `/oak:index/acme.product-custom-2` 下に格納されます。

アプリケーションの古いバージョンでは、次の設定を使用します。

`/oak:index/acme.product-custom-1`

新しいバージョンのアプリケーションでは、次の（変更された）設定が使用されます。

`/oak:index/acme.product-custom-2`

>[!NOTE]
>
>AEM上のCloud Serviceとしてのインデックス定義は、ローカル開発インスタンス上のインデックス定義と完全に一致しない場合があります。 開発インスタンスにはTika設定はありませんが、AEMのCloud ServiceインスタンスにはTika設定があります。 Tika構成でインデックスをカスタマイズする場合は、Tika構成を維持してください。

### 変更の取り消し{#undoing-a-change}

インデックス定義の変更を元に戻す必要がある場合があります。 原因は、誤って変更が行われたか、変更が不要になったことです。 例えば、インデックス定義`damAssetLucene-8-custom-3`は誤って作成され、既に展開されています。 そのため、以前のインデックス定義`damAssetLucene-8-custom-2`に戻した方がよい場合があります。 これを行うには、前のインデックス`damAssetLucene-8-custom-2`の定義を含む`damAssetLucene-8-custom-4`という新しいインデックスを追加する必要があります。

### インデックスの削除 {#removing-an-index}

次の例は、カスタムインデックスにのみ当てはまります。 製品インデックスはAEMで使用されているので削除できない場合があります。

新しいバージョンのアプリケーションでインデックスを削除する場合は、空のインデックス（使用されない、データを含まない空のインデックス）を新しい名前で定義できます。 この例の目的で、`/oak:index/acme.product-custom-3`という名前を付けることができます。 これにより、`/oak:index/acme.product-custom-2` インデックスが置き換えられます。システムによって `/oak:index/acme.product-custom-2` が削除された後は、空のインデックス `/oak:index/acme.product-custom-3` も削除できます。このような空のインデックスの例を次に示します。

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

そのまま使用できるインデックスをカスタマイズする必要がなくなった場合は、そのまま使用できるインデックス定義をコピーする必要があります。 例えば、既に`damAssetLucene-8-custom-3`を展開していて、カスタマイズが不要になり、デフォルトの`damAssetLucene-8`インデックスに戻す場合は、`damAssetLucene-8`のインデックス定義を含むインデックス`damAssetLucene-8-custom-4`を追加する必要があります。

### インデックスの可用性とフォルト・トレランス{#index-availability-and-fault-tolerance}

重要な機能の重複インデックスを作成することをお勧めします（上述のインデックスの命名規則に従ってください）。インデックスの破損や予期しないイベントが発生した場合は、クエリに応答するためのフォールバックインデックスが使用できます。
