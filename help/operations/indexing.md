---
title: コンテンツの検索とインデックス作成
description: コンテンツの検索とインデックス作成
translation-type: tm+mt
source-git-commit: 093883d0afe62bf9d1d08f82180eccd3f75bca05
workflow-type: tm+mt
source-wordcount: '1475'
ht-degree: 3%

---


# コンテンツの検索とインデックス作成 {#indexing}

## Cloud ServiceとしてのAEMの変更点 {#changes-in-aem-as-a-cloud-service}

AEMをCloud Serviceとして使用する場合、アドビでは、AEMインスタンス中心モデルから、Cloud ManagerのCI/CDパイプラインによって駆動される、n-xのAEMコンテナを持つサービスベースの表示に移行します。 単一のAEMインスタンスでインデックスの設定と管理を行う代わりに、インデックスの設定を指定してからデプロイメントを行う必要があります。 本番環境での設定の変更は、CI/CDのポリシーを明確に破っています。 インデックスの変更についても同じことが言えます。システムの安定性とパフォーマンスに影響を及ぼす可能性があるのは、指定しない場合は、実稼働環境に移行する前にテストおよび再インデックスを実行する必要があるからです。

次に、AEM 6.5以前のバージョンと比較した主な変更点のリストを示します。

1. ユーザーは、単一のAEMインスタンスのインデックスマネージャーにアクセスして、インデックスのデバッグ、設定または維持を行うことができなくなります。 ローカル開発およびオンプレムデプロイメントにのみ使用されます。

1. ユーザーは、1つのAEMインスタンスのインデックスを変更したり、整合性チェックや再インデックスに関する心配をなくします。

1. 一般に、Cloud ManagerのCI/CDパイプラインの品質の高いゲートウェイを迂回し、実稼働環境のビジネスKPIに影響を与えないように、インデックスの変更は実稼働環境に移行する前に開始されます。

1. 実稼働環境での検索パフォーマンスを含むすべての関連指標は、検索とインデックスのトピックの全体的な表示を提供するために、実行時にお客様が利用できます。

1. お客様は、ニーズに応じてアラートを設定できます。

1. SREはシステムの正常性を24時間365日監視しており、必要に応じて早期に対処する予定です。

1. インデックスの構成は、配置を介して変更されます。 インデックス定義の変更は、他のコンテンツの変更と同様に設定されます。

1. Cloud ServiceとしてのAEMの高レベルでは、 [Blue-Greenデプロイメントモデルが導入され](#index-management-using-blue-green-deployments) 、2組のインデックスが存在します。 1つは古いバージョン（青）用のセット、もう1つは新しいバージョン（緑）用のセットです。

1. インデックス作成ジョブがCloud Managerのビルドページで完了したかどうかを確認でき、新しいバージョンでトラフィックを受信する準備ができたら通知を受け取ります。

1. 制限事項： 現在、Cloud ServiceとしてのAEMでのインデックス管理は、lucene型のインデックスに対してのみサポートされています。

<!-- ## Sizing Considerations {#sizing-considerations}

AEM as a Cloud Service comes with a default capacity model to provide sufficient performance for average web applications. This "average" measure relates to the repository size and even more relevant to the indexing size. If we have reasons to believe that we need extended capacity for a specific customer project, an evaluation with SREs and Engineering will take place to determine the required capacity settings.

AS NOTE: the above is internal for now.

-->

## 使用方法 {#how-to-use}

インデックスの定義は、次の3つの使用例で構成できます。

1. 新しい顧客インデックス定義の追加
1. 既存のインデックス定義を更新しています。 これは、既存のインデックス定義の新しいバージョンを追加することを意味します
1. 冗長または古い既存のインデックスを削除しています。

上記のポイント1と2の両方について、それぞれのCloud Managerリリーススケジュールで、カスタムコードベースの一部として新しいインデックス定義を作成する必要があります。 詳しくは、Cloud ServiceドキュメントとしてのAEMへの [デプロイを参照してください](/help/implementing/deploying/overview.md)。

### 新しいインデックス定義の準備 {#preparing-the-new-index-definition}

次の命名パターンに従って、実際のインデックス定義を含む新しいインデックス定義パッケージを準備する必要があります。

`<indexName>[-<productVersion>]-custom-<customVersion>`

その後は下に入る必要があ `ui.apps/src/main/content/jcr_root`る 現在、サブルートフォルダーはサポートされていません。

<!-- need to review and link info on naming convention from https://wiki.corp.adobe.com/display/WEM/Merging+Customer+and+OOTB+Index+Changes?focusedCommentId=1784917629#comment-1784917629 -->

上記のサンプルのパッケージは、としてビルドされ `com.adobe.granite:new-index-content:zip:1.0.0-SNAPSHOT`ます。

### 索引定義の配置 {#deploying-index-definitions}

>[!NOTE]
>
> Jackrabbit Filevault Mavenパッケージプラグインバージョン **1.1.0** には既知の問題があり、のモジュール `oak:index` に追加できません `<packageType>application</packageType>`。 この問題に対処するには、バージョン **1.0.4を使用してください**。

インデックス定義は、カスタムおよびバージョン付きとしてマークされるようになりました。

* インデックス定義自体(例 `/oak:index/ntBaseLucene-custom-1`)

したがって、インデックスを展開するには、インデックス定義(`/oak:index/definitionname`)をGitおよびCloud Managerの展開プロセス `ui.apps` 経由で配信する必要があります。

新しいインデックス定義を追加したら、新しいアプリケーションをCloud Managerを使用してデプロイする必要があります。 配置を開始すると、2つのジョブが開始され、それぞれMongoDBとAzure Segment Storeに作成者用と発行用のインデックス定義を追加（および必要に応じて結合）します。 Blue-Greenスイッチが発生する前に、基になるリポジトリのインデックスが新しいインデックス定義で再作成されています。

>[!TIP]
>
>Cloud ServiceとしてのAEMに必要なパッケージ構造について詳しくは、ドキュメントの [AEMプロジェクト構造を参照してください。](/help/implementing/developing/introduction/aem-project-content-package-structure.md)

## 青 — 緑の導入を使用したインデックス管理 {#index-management-using-blue-green-deployments}

### インデックス管理とは {#what-is-index-management}

インデックス管理は、インデックスの追加、削除、変更に関するものです。 インデックスの *定義の変更は高速ですが* 、変更を適用する（「インデックスの作成」、または既存のインデックスの場合は「インデックスの再構築」と呼ばれる）には時間が必要です。 即時ではありません。 インデックスを作成するデータをリポジトリでスキャンする必要があります。

### Blue-Green導入とは {#what-is-blue-green-deployment}

環境に優しい環境での導入は、ダウンタイムを短縮できます。 また、ダウンタイムをゼロにするアップグレードも可能で、高速なロールバックが可能です。 アプリケーションの古いバージョン（青）は、アプリケーションの新しいバージョン（緑）と同時に実行されます。

### 読み取り専用領域と読み取り/書き込み可能領域 {#read-only-and-read-write-areas}

リポジトリの特定の領域（リポジトリの読み取り専用の部分）は、古い（青い）バージョンと新しい（緑の）バージョンで異なる場合があります。 リポジトリの読み取り専用領域は、通常、「`/app`」と「`/libs`」です。 次の例では、読み取り専用領域に斜体を使用し、読み取り/書き込み可能領域に太字を使用します。

* **/**
* */apps（読み取り専用）*
* **/content**
* */libs （読み取り専用）*
* **/oak:index**
* **/oak:index/acme**
* **/jcr:system**
* **/system**
* **/var**

リポジトリの読み取り/書き込み領域は、アプリケーションのすべてのバージョン間で共有されますが、アプリケーションの各バージョンには、との固有のセットが `/apps` あり `/libs`ます。

### Blue-Green展開を使用しないインデックス管理 {#index-management-without-blue-green-deployment}

開発中、またはオンプレミスインストールを使用する場合は、インデックスを実行時に追加、削除または変更できます。 インデックスは、使用可能になるとすぐに使用されます。 まだ古いバージョンのアプリケーションでインデックスを使用しないはずの場合は、通常、予定されたダウンタイム中にインデックスが構築されます。 インデックスの削除時や、既存のインデックスの変更時にも同じことが起こります。 インデックスを削除すると、削除されるとすぐに使用できなくなります。

### Blue-Green展開によるインデックス管理 {#index-management-with-blue-green-deployment}

青緑色の導入では、ダウンタイムは発生しません。 ただし、インデックス管理の場合は、インデックスが特定のバージョンのアプリケーションでのみ使用される必要があります。 例えば、アプリケーションのバージョン2でインデックスを追加する場合、まだアプリケーションのバージョン1でインデックスを使用したくないとします。 逆の場合は、インデックスが削除されます。 バージョン2で削除したインデックスは、バージョン1でも必要です。 インデックス定義を変更する場合、古いバージョンのインデックスをバージョン1でのみ使用し、新しいバージョンのインデックスをバージョン2でのみ使用します。

次の表に、5つのインデックス定義を示します。 index `cqPageLucene` は両方のバージョンで使用され、index `damAssetLucene-custom-1` はバージョン2でのみ使用されます。

>[!NOTE]
>
> `<indexName>-custom-<customerVersionNumber>` は、AEMをCloud Serviceとして、既存のインデックスの代わりとしてマークする場合に必要です。

| 索引 | 標準インデックス | バージョン1で使用 | バージョン2で使用 |
|---|---|---|---|
| /oak:index/damAssetLucene | はい | はい | 不可 |
| /oak:index/damAssetLucene-custom-1 | ○（カスタマイズ） | 不可 | 可 |
| /oak:index/acmeProduct-custom-1 | 不可 | 可 | 不可 |
| /oak:index/acmeProduct-custom-2 | 不可 | 不可 | 可 |
| /oak:index/cqPageLucene | はい | 可 | はい |

バージョン番号は、インデックスが変更されるたびに増加します。 製品自体のインデックス名と衝突するカスタムインデックス名を回避するには、カスタムインデックスと、初期設定のインデックスに対する変更をで終える必要があり `-custom-<number>`ます。

### 既製のインデックスの変更 {#changes-to-out-of-the-box-indexes}

「damAssetLucene」や「cqPageLucene」のような既成のインデックスをアドビが変更すると、またはという名前の新しいインデックスが作成されます。また、インデックスが既にカスタマイズされている場合は、次のように、カスタマイズ済みのインデックス定義が既存のインデックスの変更と結合されます。 `damAssetLucene-2``cqPageLucene-2` 変更のマージは自動的に行われます。 つまり、あらかじめ用意されているインデックスが変更された場合、何もする必要はありません。 ただし、後でインデックスを再びカスタマイズすることは可能です。

| 索引 | 標準インデックス | バージョン2で使用 | バージョン3で使用 |
|---|---|---|---|
| /oak:index/damAssetLucene-custom-1 | ○（カスタマイズ） | はい | 不可 |
| /oak:index/damAssetLucene-2-custom-1 | はい（damAssetLucene-custom-1およびdamAssetLucene-2から自動的に結合） | 不可 | 可 |
| /oak:index/cqPageLucene | はい | はい | 不可 |
| /oak:index/cqPageLucene-2 | はい | 不可 | 可 |

### 制限事項 {#limitations}

インデックス管理は、現在、タイプのインデックスに対してのみサポートされて `lucene`います。

### インデックスの削除 {#removing-an-index}

新しいバージョンのアプリケーションでインデックスを削除する場合は、空のインデックス（インデックスを作成するデータのないインデックス）を新しい名前で定義できます。 例えば、名前を付けることができ `/oak:index/acmeProduct-custom-3`ます。 これにより、インデックスが置き換えられ `/oak:index/acmeProduct-custom-2`ます。 システム `/oak:index/acmeProduct-custom-2` が削除した後は、空のインデックスも削除 `/oak:index/acmeProduct-custom-3` できます。

### インデックスの追加 {#adding-an-index}

新しいバージョンのアプリケーション以降で使用する「/oak:index/acmeProduct-custom-1」という名前のインデックスを追加するには、インデックスを次のように設定する必要があります。

`*mk.*assetLuceneIndex-1-custom-1`

これは、インデックス名の前にカスタム識別子を付け、その後にドット(**.**). 識別子の長さは1 ～ 4文字である必要があります。

上記のように、これにより、新しいバージョンのアプリケーションでのみインデックスが使用されます。

### インデックスの変更 {#changing-an-index}

既存のインデックスを変更する場合は、変更したインデックス定義を使用して新しいインデックスを追加する必要があります。 例えば、既存のインデックス「/oak:index/acmeProduct-custom-1」が変更されているとします。 古いインデックスは下に、新しいインデックス `/oak:index/acmeProduct-custom-1`は下に格納され `/oak:index/acmeProduct-custom-2`ます。

アプリケーションの古いバージョンでは、次の設定を使用します。

`/oak:index/acmeProduct-custom-1`

新しいバージョンのアプリケーションでは、次の（変更された）設定が使用されます。

`/oak:index/acmeProduct-custom-2`