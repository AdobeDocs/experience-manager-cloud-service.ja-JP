---
title: コンテンツの検索とインデックス作成
description: コンテンツの検索とインデックス作成
translation-type: tm+mt
source-git-commit: 610615534cb5a798e37d34fadb9a3bf341565526
workflow-type: tm+mt
source-wordcount: '1521'
ht-degree: 100%

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

1. 制限事項：現在、AEM as a Cloud Service のインデックス管理は、lucene 型のインデックスに対してのみサポートされています。

<!-- ## Sizing Considerations {#sizing-considerations}

AEM as a Cloud Service comes with a default capacity model to provide sufficient performance for average web applications. This "average" measure relates to the repository size and even more relevant to the indexing size. If we have reasons to believe that we need extended capacity for a specific customer project, an evaluation with SREs and Engineering will take place to determine the required capacity settings.

AS NOTE: the above is internal for now.

-->

## 使用方法 {#how-to-use}

インデックスの定義は、次の 3 つのユースケース で構成できます。

1. 新しい顧客インデックス定義の追加
1. 既存のインデックス定義の更新。これは、既存のインデックス定義の新しいバージョンを追加することを意味します
1. 冗長または古い既存のインデックスの削除。

上記のポイント 1 と 2 の両方について、それぞれの Cloud Manager リリーススケジュールで、カスタムコードベースの一部として新しいインデックス定義を作成する必要があります。詳しくは、[AEM as a Cloud Service へのデプロイ](/help/implementing/deploying/overview.md)ドキュメントを参照してください。

### 新しいインデックス定義の準備 {#preparing-the-new-index-definition}

次の命名パターンに従って、実際のインデックス定義を含む新しいインデックス定義パッケージを準備する必要があります。

`<indexName>[-<productVersion>]-custom-<customVersion>`

それらは `ui.apps/src/main/content/jcr_root` の下に置く必要があります。現在、サブルートフォルダーはサポートされていません。

<!-- need to review and link info on naming convention from https://wiki.corp.adobe.com/display/WEM/Merging+Customer+and+OOTB+Index+Changes?focusedCommentId=1784917629#comment-1784917629 -->

上記のサンプルのパッケージは、`com.adobe.granite:new-index-content:zip:1.0.0-SNAPSHOT` としてビルドされます。

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

アドビが「damAssetLucene」や「cqPageLucene」のような標準提供のインデックスを変更すると、`damAssetLucene-2` または `cqPageLucene-2` という名前の新しいインデックスが作成されます。また、インデックスが既にカスタマイズされている場合は、次のように、カスタマイズされたインデックス定義が標準提供のインデックス変更と結合されます。変更のマージは自動的におこなわれます。つまり、標準提供のインデックスが変更された場合、何もする必要はありません。ただし、後でインデックスを再びカスタマイズすることは可能です。

| 索引 | 標準提供インデックス | バージョン 2 で使用 | バージョン 3 で使用 |
|---|---|---|---|
| /oak:index/damAssetLucene-custom-1 | 可（カスタマイズ） | 可 | 不可 |
| /oak:index/damAssetLucene-2-custom-1 | はい（damAssetLucene-custom-1 および damAssetLucene-2 から自動的に結合） | 不可 | 可 |
| /oak:index/cqPageLucene | 可 | 可 | 不可 |
| /oak:index/cqPageLucene-2 | 可 | 不可 | 可 |

### 制限事項 {#limitations}

インデックス管理は、現在、`lucene` 型のインデックスに対してのみサポートされています。

### インデックスの削除 {#removing-an-index}

新しいバージョンのアプリケーションでインデックスを削除する場合は、空のインデックス（インデックスを作成するデータのないインデックス）を新しい名前で定義できます。例えば、`/oak:index/acme.product-custom-3` と名前を付けることができます。これにより、`/oak:index/acme.product-custom-2` インデックスが置き換えられます。システムによって `/oak:index/acme.product-custom-2` が削除された後は、空のインデックス `/oak:index/acme.product-custom-3` も削除できます。

### インデックスの追加 {#adding-an-index}

新しいバージョン以降のアプリケーションで使用する「/oak:index/acme.product-custom-1」という名前のインデックスを追加するには、インデックスを次のように設定する必要があります。

`acme.product-1-custom-1`

これは、インデックス名の前にカスタム識別子を付け、その後にドット（**`.`**）を付けることで機能します。識別子の長さは 2～5 文字です。

これにより、新しいバージョンのアプリケーションでのみインデックスが使用されます。

### インデックスの変更 {#changing-an-index}

既存のインデックスを変更する場合は、変更したインデックス定義を使用して新しいインデックスを追加する必要があります。例えば、既存のインデックス「/oak:index/acme.product-custom-1」が変更されるとします。古いインデックスは `/oak:index/acme.product-custom-1` 下に、新しいインデックスは `/oak:index/acme.product-custom-2` 下に格納されます。

アプリケーションの古いバージョンでは、次の設定を使用します。

`/oak:index/acme.product-custom-1`

新しいバージョンのアプリケーションでは、次の（変更された）設定が使用されます。

`/oak:index/acme.product-custom-2`

### インデックスの使用可能性／フォールトトレランス {#index-availability}

インデックスの破損や予期しないイベントが発生した場合に、クエリに応答するためのフォールバックインデックスが使用できるように、非常に重要な機能のために重複インデックスを作成することをお勧めします（前述のインデックスの命名規則を考慮）。
