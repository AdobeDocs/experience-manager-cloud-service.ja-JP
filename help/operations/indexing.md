---
title: インデックス作成
description: 'インデックス作成 '
translation-type: tm+mt
source-git-commit: 83d2abd5b75e644be97de1d5420e7bca6b13e0d9

---


# インデックス作成 {#indexing}

## クラウドサービスとしてのAEMの変更点 {#changes-in-aem-as-a-cloud-service}

AEMをクラウドサービスとして使用する場合、アドビは、AEMインスタンス中心モデルから、Cloud ManagerのCI/CDパイプラインによって駆動されるn-xのAEMコンテナを含むサービスベースのビューに移行します。 単一のAEMインスタンスでインデックスを設定および維持する代わりに、デプロイメントの前にインデックス設定を指定する必要があります。 本番環境での設定の変更により、CI/CDポリシーが明らかに崩れています。 インデックスの変更も同様です。システムの安定性とパフォーマンスに影響を与える可能性があるので、実稼働環境に移行する前にテストおよび再インデックスを行う必要があります。

AEM 6.5以前のバージョンと比較した主な変更点を以下に示します。

1. ユーザーは、単一のAEMインスタンスのインデックスマネージャーにアクセスして、インデックスのデバッグ、設定、または維持を行うことができなくなります。 ローカル開発およびオンプレミングでのデプロイメントにのみ使用されます。

1. ユーザーは、1つのAEMインスタンス上のインデックスを変更したり、整合性チェックやインデックスの再作成について心配する必要はなくなります。

1. 一般に、Cloud Manager CI/CDパイプラインの品質の高いゲートウェイを迂回させ、実稼働環境のビジネスKPIに影響を与えないように、実稼働環境に移行する前にインデックスの変更が開始されます。

1. 実稼働環境での検索パフォーマンスを含むすべての関連指標は、検索とインデックスのトピックの全体像を提供するために、実行時に顧客が利用できるようになります。

1. お客様は、ニーズに応じてアラートを設定できます。

1. SREはシステムの正常性を24時間365日監視しており、必要に応じて早期に対処します。

1. インデックスの設定は、デプロイメントを通じて変更されます。 インデックス定義の変更は、他のコンテンツの変更と同様に設定されます。

1. クラウドサービスとしてのAEMの概要では、 [Blue-Greenデプロイメントモデルが導入されると](#index-management-using-blue-green-deployments) 、2組のインデックスが存在します。1つは古いバージョン（青）用、もう1つは新しいバージョン（緑）用のセットです。

使用されるインデックスのバージョンは、フラグを介してインデックス定義のフラグを使用して設定さ `useIfExist` れます。 インデックスは、1つのバージョンのアプリケーション（例えば、青または緑のみ）、または両方で使用できます。 詳細なドキュメントは、「 [Index Management using Blue-Green Deployments」で入手できます](#index-management-using-blue-green-deployments)。

1. インデックス作成ジョブがCloud Managerのビルドページで完了したかどうかを確認でき、新しいバージョンでトラフィックを受け取る準備ができたら通知を受け取ります。

1. 制限：現在、クラウドサービスとしてのAEMでのインデックス管理は、luceneタイプのインデックスに対してのみサポートされています。

<!-- ## Sizing Considerations {#sizing-considerations}

AEM as a Cloud Service comes with a default capacity model to provide sufficient performance for average web applications. This "average" measure relates to the repository size and even more relevant to the indexing size. If we have reasons to believe that we need extended capacity for a specific customer project, an evaluation with SREs and Engineering will take place to determine the required capacity settings. 

AS NOTE: the above is internal for now.

-->

## 使用方法 {#how-to-use}

インデックスの定義は、次の3つの使用例で構成できます。

1. 新しい顧客インデックス定義の追加
1. 既存のインデックス定義を更新しています。 これは、既存のインデックス定義の新しいバージョンを追加することを意味します
1. 重複しているか古い既存のインデックスを削除しています。

上記のポイント1と2の両方に対して、それぞれのCloud Managerリリーススケジュールで、カスタムコードベースの一部として新しいインデックス定義を作成する必要があります。 詳しくは、「クラウドサービスとしてのAEM [へのデプロイ」のドキュメントを参照してください](/help/implementing/deploying/overview.md)。

### 新しいインデックス定義の準備 {#preparing-the-new-index-definition}

次の命名パターンに従って、実際のインデックス定義を含む新しいインデックス定義パッケージを準備する必要があります。

`<indexName>[-<productVersion>]-custom-<customVersion>`

その後、下に行く必要があ `ui.content/src/main/content/jcr_root`る 現時点では、サブルートフォルダーはサポートされていません。

<!-- need to review and link info on naming convention from https://wiki.corp.adobe.com/display/WEM/Merging+Customer+and+OOTB+Index+Changes?focusedCommentId=1784917629#comment-1784917629 -->

上記のサンプルのパッケージは、として構築されま `com.adobe.granite:new-index-content:zip:1.0.0-SNAPSHOT`す。

### 索引定義の配置 {#deploying-index-definitions}

インデックス定義は、カスタムおよびバージョン付きとしてマークされるようになりました。

* MUTABLEコンテンツであるインデックス `/oak:index/ntBaseLucene-custom-1`定義自体（例えば）

したがって、インデックスを展開するには、インデックス定義(`/oak:index/definitionname`)を可変パッケージ(通常はGitとCloud Managerの展開プロセス ****`ui.content` )を介して配信する必要があります。

新しいインデックス定義を追加したら、Cloud Managerを使用して新しいアプリケーションをデプロイする必要があります。 配置が開始されると、2つのジョブが開始され、作成者用と発行用のインデックス定義をMongoDBとAzureセグメントストアに追加（および必要に応じて結合）します。 Blue-Greenスイッチが発生する前に、基になるリポジトリのインデックスが新しいインデックス定義で再作成されています。

## 青 — 緑のデプロイメントを使用したインデックス管理 {#index-management-using-blue-green-deployments}

### インデックス管理とは {#what-is-index-management}

インデックス管理は、インデックスの追加、削除、変更に関するものです。 インデックス *の定義の変更は* 、すばやく行えますが、変更を適用する場合(「インデックスの作成」と呼ばれることが多く、既存のインデックスの場合は「インデックスの再作成」に時間が必要です。 それは瞬時ではありません。インデックスを作成するデータをリポジトリでスキャンする必要があります。

### 青緑の導入とは {#what-is-blue-green-deployment}

環境に優しい環境での導入により、ダウンタイムを短縮できます。 また、ダウンタイムをゼロにアップグレードし、迅速なロールバックを提供します。 古いバージョンのアプリケーション（青）は、新しいバージョンのアプリケーション（緑）と同時に実行されます。

### 読み取り専用領域と読み取り/書き込み可能領域 {#read-only-and-read-write-areas}

リポジトリの特定の領域（リポジトリの読み取り専用の部分）は、古い（青）バージョンと新しい（緑）バージョンのアプリケーションで異なる場合があります。 リポジトリの読み取り専用領域は、通常、「`/app`」と「`/libs`」です。 次の例では、読み取り専用領域をマークする場合に斜体を使用し、読み取り/書き込み可能領域の場合には太字を使用します。

* **/**
* */apps（読み取り専用）*
* **/content**
* */libs （読み取り専用）*
* **/oak:index**
* **/oak:index/acme**
* **/jcr:system**
* **/system**
* **/var**

リポジトリの読み取り/書き込み領域は、アプリケーションのすべてのバージョン間で共有されますが、アプリケーションの各バージョンには、との固有のセットが `/apps` ありま `/libs`す。

### Blue-Green展開を使用しないインデックス管理 {#index-management-without-blue-green-deployment}

開発中、またはオンプレミスのインストールを使用する場合、実行時にインデックスを追加、削除、または変更できます。 インデックスは、使用可能になるとすぐに使用されます。 まだ古いバージョンのアプリケーションでインデックスを使用することが想定されていない場合、通常は予定されたダウンタイム中にインデックスが構築されます。 インデックスを削除したり、既存のインデックスを変更したりする場合も、同じことが起こります。 インデックスを削除すると、削除されるとすぐに使用できなくなります。

### 青 — 緑の導入によるインデックス管理 {#index-management-with-blue-green-deployment}

青緑色の導入では、ダウンタイムは発生しません。 ただし、インデックス管理の場合は、特定のバージョンのアプリケーションでのみインデックスが使用される必要があります。 例えば、アプリケーションのバージョン2でインデックスを追加する場合、まだアプリケーションのバージョン1でインデックスを使用しないようにします。 逆の場合は、インデックスが削除されます。バージョン2で削除されたインデックスは、バージョン1でも必要です。 インデックス定義を変更する場合は、古いバージョンのインデックスをバージョン1にのみ使用し、新しいバージョンのインデックスをバージョン2にのみ使用する必要があります。

次の表に、5つのインデックス定義を示します。indexは `cqPageLucene` 両方のバージョンで使用され、indexはバ `damAssetLucene-custom-1` ージョン2でのみ使用されます。


> [!NOTE]
> `<indexName>-custom-<customerVersionNumber>` が必要です。

| 索引 | 標準インデックス | バージョン1で使用 | バージョン2で使用 |
|---|---|---|---|
| /oak:index/damAssetLucene | 可 | 可 | いいえ |
| /oak:index/damAssetLucene-custom-1 | ○（カスタマイズ済み） | いいえ | はい |
| /oak:index/acmeProduct-custom-1 | いいえ | はい | いいえ |
| /oak:index/acmeProduct-custom-2 | いいえ | いいえ | はい |
| /oak:index/cqPageLucene | 可 | 可 | 可 |

バージョン番号は、インデックスが変更されるたびに増加します。 製品自体のインデックス名に衝突するカスタムインデックス名を避けるには、カスタムインデックスと、初期設定のインデックスの変更をで終える必要がありま `-custom-<number>`す。

### 既製のインデックスの変更 {#changes-to-out-of-the-box-indexes}

アドビが「damAssetLucene」や「cqPageLucene」など、あらかじめ用意されているインデックスを変更すると、またはという新しいインデックスが作成されます。また、インデックスが既にカスタマイズされている場合は、次に示すように、カスタマイズされたインデックス定義がそのまま使用できます。 `damAssetLucene-2``cqPageLucene-2` 変更のマージは自動的に行われます。 つまり、あらかじめ用意されているインデックスが変更された場合に、何もする必要はありません。 ただし、後でインデックスを再びカスタマイズすることは可能です。

| 索引 | 標準インデックス | バージョン2で使用 | バージョン3で使用 |
|---|---|---|---|
| /oak:index/damAssetLucene-custom-1 | ○（カスタマイズ済み） | はい | いいえ |
| /oak:index/damAssetLucene-2-custom-1 | はい（damAssetLucene-custom-1およびdamAssetLucene-2から自動的に結合） | いいえ | はい |
| /oak:index/cqPageLucene | 可 | 可 | いいえ |
| /oak:index/cqPageLucene-2 | はい | いいえ | はい |

### 制限事項 {#limitations}

インデックス管理は、現在、タイプのインデックスに対してのみサポートされていま `lucene`す。

### 索引の削除 {#removing-an-index}

新しいバージョンのアプリケーションでインデックスを削除する場合は、空のインデックス（インデックスを作成するデータのないインデックス）を新しい名前で定義できます。 例えば、名前を付けることができま `/oak:index/acmeProduct-custom-3`す。 これにより、インデックスが置き換えられ `/oak:index/acmeProduct-custom-2`ます。 システ `/oak:index/acmeProduct-custom-2` ムによって削除された空のインデックスは、削 `/oak:index/acmeProduct-custom-3` 除することもできます。

### 索引の追加 {#adding-an-index}

新しいバージョンのアプリケーション以降で使用する「/oak:index/acmeProduct-custom-1」という名前のインデックスを追加するには、インデックスを次のように設定する必要があります。

`/oak:index/acmeProduct-custom-1`

上記のように、これにより、新しいバージョンのアプリケーションでのみインデックスが使用されます。

### 索引の変更 {#changing-an-index}

既存のインデックスを変更する場合は、変更したインデックス定義で新しいインデックスを追加する必要があります。 例えば、既存のインデックス「/oak:index/acmeProduct-custom-1」が変更されているとします。 古いインデックスは下に、新 `/oak:index/acmeProduct-custom-1`しいインデックスは下に格納されま `/oak:index/acmeProduct-custom-2`す。

アプリケーションの古いバージョンでは、次の設定を使用します。

`/oak:index/acmeProduct-custom-1`

新しいバージョンのアプリケーションでは、次の（変更された）設定を使用します。

`/oak:index/acmeProduct-custom-2`