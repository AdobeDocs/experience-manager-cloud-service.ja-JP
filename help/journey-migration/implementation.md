---
title: 実装段階
description: クラウドに移行するためのコードとコンテンツの準備が整っていることの確認
exl-id: d124f9a5-a754-4ed0-a839-f2968c7c8faa
feature: Migration
role: Admin
source-git-commit: 913b1beceb974243f0aa7486ddd195998d5e9439
workflow-type: tm+mt
source-wordcount: '2288'
ht-degree: 99%

---

# 実装段階 {#implementation-phase}

ジャーニーの実装段階では、コードとコンテンツを AEM as a Cloud Service に移行する準備を整えるためのツールについて確認します。

## これまでの説明内容 {#story-so-far}

ジャーニーのこれまでの部分では、[AEM as a Cloud Service の変更点を理解](/help/journey-migration/getting-started.md)し、デプロイメントが[準備段階](/help/journey-migration/readiness.md)でクラウドに移行する準備ができているかどうかを判断しました。

この記事では、コードとコンテンツをクラウドに移動する準備ができていることを、アドビが提供するツールを使用して確認する方法について引き続き説明します。

## 目的 {#objective}

このドキュメントの目的は次のとおりです。

* コードを AEM as a Cloud Service にデプロイするために使用する、AEM の継続的インテグレーションと継続的デリバリーのフレームワークである Cloud Manager を紹介します。
* コンテンツ転送ツールについて詳しく説明します。
* AEM as a Cloud Service のコードを最新化するために使用する必要がある、コードリファクタリングツールについて説明します。

## Cloud Manager の使用 {#using-cloud-manager}

始める前に、Cloud Manager に習熟している必要があります。Cloud Manager は AEM as a Cloud Service にコードをデプロイするための唯一のメカニズムであるためです。

Cloud Manager を使用すると、クラウド内の AEM を組織で自己管理できるようになります。このサービスには継続的インテグレーションと継続的デリバリー（CI／CD）フレームワークが備わっているので、IT チームや実装パートナーはパフォーマンスやセキュリティを妥協することなくカスタマイズや更新を迅速に配信できます。

Cloud Manager の使い方については、以下のリソースを参照してください。

* [オンボーディングジャーニー](/help/journey-onboarding/overview.md)：Experience Manager as a Cloud Service へのオンボーディングに関するセルフヘルプリソースについて理解します

* [Git と Adobe Cloud Manager の統合](/help/implementing/cloud-manager/managing-code/integrating-with-git.md)：1 つの Git リポジトリーを使用してコードをデプロイする方法について

* [Adobe Experience Manager as a Cloud Service の設定](/help/security/ims-support.md#aem-configuration)：Admin Console での製品とユーザーアクセスの管理

## アドビが提供するツールを使用してコンテンツとコードクラウドを準備する {#use-tools-to-make-code-and-content-cloud-ready}

Cloud Service への移行の正確な手順は、購入したシステムと準拠するソフトウェア開発ライフサイクル手法によって異なります。

次の図は、AEM as a Cloud Service で使用するコードとコンテンツを変換するフェーズについて、主な段階を示したものです。

![ コンバージョン手順 ](/help/journey-migration/assets/exec-image1.png)

以下の章では、これを実現するために必要なツールの詳細を説明します。

## コンテンツの移行 {#content-migration}

現在の AEM インスタンスから Cloud Service インスタンスにコンテンツを移行するには、アドビのコンテンツ転送ツールを使用します。

このツールを使用すると、ソース AEM インスタンスから AEM Cloud Service インスタンスに転送するコンテンツのサブセットを指定できます。

コンテンツ移行は、異なるチーム間での計画、追跡、共同作業を必要とする複数の手順で構成されるプロセスです。

ツールの仕組みと推奨される使用方法について詳しくは、[コンテンツ転送ツールのドキュメント](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/overview-content-transfer-tool.md)を参照してください。

## コードリファクタリング {#code-refactor}

### 開発用にセットアップ {#set-up-for-development}

Cloud Services と互換性を持たせるために、既存の機能のリファクタリングを開始します。

まず、基本的なツールの詳細を説明したドキュメントを参照し、コードのリファクタリングを開始します。


* 計画中は、AEM as a Cloud Service との互換性を保つためにリファクタリングが必要な領域のリストを用意しておくことをお勧めします。Cloud Service のコードをリファクタリングして最適化する方法について詳しくは、 [開発ガイドライン](/help/implementing/developing/introduction/development-guidelines.md) を確認してください。
* AEM as a Cloud Service で [設定を管理](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/developing/configurations.html?lang=ja#what-is-a-configuration) する方法を確認してください。
* [AEM as a Cloud Service SDK](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/developing/aem-as-a-cloud-service-sdk.html?lang=ja) をダウンロードして、ローカル開発環境を設定する方法を確認してください。
* 最後に、[AEM as a Cloud Service Java API](https://www.adobe.io/experience-manager/reference-materials/cloud-service/javadoc/index.html) について詳しく確認してください。

また、以下も行ってください。

* このビデオを視聴すると、Dispatcher SDK をローカルにインストールする方法を理解できます。

  >[!VIDEO](https://video.tv.adobe.com/v/30601)

* このビデオを視聴すると、Dispatcher SDK の設定方法を理解できます。

  >[!VIDEO](https://video.tv.adobe.com/v/35077?captions=jpn)

### 発想の転換 {#a-change-in-mindset}

AEM as a Cloud Service でコードを開発して実行するには、考え方を変える必要があります。インスタンスはいつ停止するかわからないので、コードには特に回復力が必要である点に留意してください。Cloud Service で実行するコードは、常にクラスター内で実行されていることを認識している必要があります。つまり、常に複数のインスタンスが実行されています。

AEM Maven プロジェクトをクラウドに対応させるためには、ある程度の変更が必要です。AEM as a Cloud Service では、 *コンテンツ* と *コード* を AEM にデプロイするには別個のパッケージに分離する必要があります。

* `/apps` および `/libs` は、AEM の起動後（つまり実行時）に変更できないため、AEM の不変領域と見なされます。これには、作成、更新、削除の操作が含まれます。実行時に不変領域を変更しようとすると失敗します。

* リポジトリ内のその他すべて（例：`/content`、`/conf`、`/var`、`/home`、`/etc`、`/oak:index`、`/system`、`/tmp`）はすべて可変領域です。つまり、実行時に変更できます。

詳しくは、 [推奨されるパッケージ構造](/help/implementing/developing/introduction/aem-project-content-package-structure.md#recommended-package-structure) のドキュメントを参照してください。


### クラウド移行ツール {#cloud-migration-tools}

アドビは、コードをリファクタリングするタスクの高速化に役立つツールをいくつか用意しています。これらのツールと解決する問題を理解することで、移行の複雑さと時間を削減できます。

* [アセットワークフロー移行](/help/journey-migration/moving-to-aem-assets/asset-workflow-migration-tool.md)：アセット処理ワークフローを自動的に移行するためのツール
* [Dispatcher コンバーター](/help/journey-migration/refactoring-tools/dispatcher-transformation-utility-tools.md)： 既存の Dispatcher 設定を、AEM as a Cloud Service に対応する形式に変換するツール。
* [Repository Modernizer](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/moving/refactoring-tools/repo-modernizer.html?lang=ja)：AEM Multimode プロジェクトを入力として取り、AEM as a Cloud Service プロジェクトに変換するツール
* [インデックスコンバーター](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/moving/refactoring-tools/index-converter.html?lang=ja)：インデックスを AEM as a Cloud Service 互換のフォームに変換するツール
* [最新化ツール](/help/journey-migration/refactoring-tools/aem-modernization-tools.md)： 従来の AEM 機能を、サポートされている最新の AEM as a Cloud Service 機能に変換するためのユーティリティスイート。

ローカル開発環境を設定したら、AEM as a Cloud Service SDK に精通するために、 [ドキュメント](/help/implementing/developing/introduction/aem-as-a-cloud-service-sdk.md) を参照してください。

### コードの凍結のスケジュール設定 {#schedule-a-code-freeze}

移行ジャーニーの一環として、アクティブな AEM 上で進行中のコード開発と、コードリファクタリングタスクを管理するには、AEM as a Cloud Service と互換性のある Maven プロジェクトの再構築が完了するまで、コードの凍結期間をスケジュール設定しておくことをお勧めします。

プロジェクトの再構築が完了したら、この新しい構造に基づいて新しいコード開発を再開できます。これにより、コードのデプロイメントおよびテスト中に発生する Cloud Manager パイプラインのエラーを減らすことができます。

>[!NOTE]
>コンテンツ転送タスクとコードリファクタリングタスクは、順番に実行しなくてもかまいません。これらのタスクは互いに独立に実行することができます。ただし、Cloud Service 環境でコンテンツが正常にレンダリングされるようにするには、正しいプロジェクト構造が必要です。

## コードのデプロイメントとテストのベストプラクティス {#best-practices}

Cloud Manager パイプラインは、ステージング環境に対するテストの実行をサポートしています。

コード品質テストに関する以下のドキュメントのベストプラクティスに従います。

* [コード品質テスト](/help/implementing/cloud-manager/code-quality-testing.md)： テストスクリプトの作成プロセスを説明し、少なくとも 50% の推奨カバレッジの概念を説明するドキュメント。
* [カスタムコード品質ルールについて](/help/implementing/cloud-manager/custom-code-quality-rules.md)：AEM Engineering のベストプラクティスに基づいて作成された Cloud Manager で実行されるカスタムコード品質ルールを説明するドキュメント。

## 運用開始の準備 {#preparing-for-go-live}

ソースシステムを準備するには、システムレベルおよび AEM 管理者レベルのタスクが必要です。開始するには、 [リビジョンのクリーンアップ](https://experienceleague.adobe.com/docs/experience-manager-65/deploying/deploying/revision-cleanup.html?lang=ja) タスクと [データストアのごみ収集](https://experienceleague.adobe.com/docs/experience-manager-65/administering/operations/data-store-garbage-collection.html?lang=ja) タスクのステータスを確認し、コンテンツリポジトリが適切に維持されている状態にあることを確認します。AEM バージョン 6.3を実行している場合は（コンテンツ転送ツールはバージョン 6.3 以降と互換性があるので）、オフライン圧縮を実行し、その後にデータストアのガベージコレクションを実行することをお勧めします。

[データ整合性チェック](https://experienceleague.adobe.com/docs/experience-manager-65/deploying/configuring/consistency-check.html?lang=ja) は、すべての AEM バージョンにわたって推奨され、コンテンツリポジトリの移行作業を適切な状態に保ちます。

[AZCopy](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/handling-large-content-repositories.md) のインストールと設定を行うには、システム管理者レベルのアクセス権が必要です

また、未使用のアセット、ページ、AEM プロジェクト、ユーザーおよびグループを確認して、移行時の時間を節約することをお勧めします。詳しくは、 [コンテンツリポジトリの正常性](#repository-health) の節を参照してください。

### コンテンツリポジトリの正常性 {#repository-health}

[実稼動クローン](#proof-of-migration) へのアクセスが設定されたら、リポジトリの正常性の確認に進みます。前の節で説明したように、移行を開始する前に、ソース上のリポジトリをクリーンアップしてコンパクト化することが目的です。この手順により、移行が開始された後の問題のトラブルシューティングに費やす時間を大幅に節約できる可能性があります。

| 作業項目 | 重要な留意点 |
|---------|----------|
| ユーザー、グループ、権限 | メンバーシップに関するユーザー、グループ、複雑さの量を理解する必要があります。移行前に、クリーンアップできる未使用のユーザーやグループがソース内にないか探します。 |
| 不完全なアセット処理 | 移行を開始する前に、ソースシステム内のアセットの処理を完了して、AEM as a Cloud Service の移行時に発生する可能性のある問題を回避します。 |
| コンテンツの正常性 | 移行を開始する前に、正しくないコンテンツを検索して除去することをお勧めします。例えば、オリジナルのレンディションがない、またはワークフロー処理でスタックしている、アセットやページを探します。[アセットの正常性](#asset-health) も参照してください。 |

## データの収集 {#gathering-data}

>[!NOTE]
> [コンテンツ移行の戦略とタイムライン](#content-strategy-and-timeline) の節では、収集したデータを推定して移行プランを作成する方法について詳しく説明します。

データの収集は、移行作業および関連タスクの計画に役立ちます。抽出と取り込みの時間は、データポイントを移行セットの特定のサイズに関連付けることができるので、特に便利です。そのため、次のデータポイントを推定して、プランを作成できます。

* [抽出](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/extracting-content.md) に要した合計時間
* [取り込み](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/ingesting-content.md) に要した合計時間
* 追加 [抽出](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/extracting-content.md#top-up-extraction-process) に要した合計時間
* 追加 [取り込み](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/ingesting-content.md#top-up-ingestion-process) に要した合計時間


<!-- Alexandru: hiding this for now

One more important datapoint is the amount of time it takes to complete the [user mapping](/help/journey-migration/content-transfer-tool/user-mapping-tool/overview-user-mapping-tool.md), if this is coupled with the content migration. You can take this data point into consideration for more realistic estimates, because it is added to the overall extraction timeline and it may not be required to run it during top-ups.

-->

これらのデータポイントは、「[KPI の設定](/help/journey-migration/readiness.md#establish-kpis)」やその他の移行関連タスクにも役立ちます。

### 移行プラン {#migration-plan}

収集したデータポイント（上記を参照）に基づいて、マクロなプロジェクトプランに統合できる移行プランを作成できます。この手順により、すべての主要な関係者が移行アクティビティを視覚化し、計画できるようになります。

次の表に、一般的な移行プランを示します。

| 移行の反復 | 開始日 | 推定終了日 | 依存関係 | 推定期間（日数） | 追加の詳細／作業項目 |
|---|---|---|---|---|---|
| PRDCLONE-AUTHOR-INITIAL-USRMAP-CSSTAGE-AUTHOR |   |   |   |   |   |
| PRDCLONE-PUBLISH-TOPUP-CSSTAGE-AUTHOR |   |   |   |   |   |

上記の表からわかるように、特定の命名形式に従って移行の反復を識別すると便利です。例：ソース AEM 環境の場合は **PRDCLONE**、AEM as a Cloud Service 環境の場合は **AUTHOR/PUBLISH**、AEM as a Cloud Service インスタンスの場合は **CSSTAGE-AUTHOR** などです。

移行プランに影響を与える重要な詳細：

**必要な抽出の合計数**

* 特定の環境でのオーサーおよびパブリッシュの抽出は、互いに独立しているので、2 つの並列抽出と見なされます。
* 特定の期間でのリポジトリの増加に基づく追加抽出の数。

**必要な取り込みの合計数**

* 抽出セットは複数の Cloud Service 環境に取り込めるので、この項目をプランに取り込むことが重要です。
* 追加取り込みの数。
* すべてのオーサーコンテンツを Cloud Service パブリッシュに取り込まないようにするためには、ベストプラクティスとして、ソースオーサーから Cloud Service オーサーインスタンス、ソースパブリッシュから Cloud Service パブリッシュにコンテンツを移行することが推奨されます。

### 移行トラッカー {#migration-tracker}

移行トラッカーを使用して、初期実行と追加実行の両方の時間をメモすることができます。これらのデータポイントは、最終的な追加の前に、現実的なコンテンツ凍結要件を策定するのに役立ちます。

トラッカーは、次の操作にも役立ちます。

* プランまたは実稼動タイムラインの調整が必要なプランナーからの逸脱を識別する
* すべての必要な通信で使用できる現実的なステータスを提供する
* 初期または将来の追加移行のプラン

次の表に、機能移行トラッカーを示します。

| ソース（環境／インスタンス／URL） | 移行先（環境／インスタンス／URL） | 移行セット名、タイプ（初期または追加） | 移行セットのサイズ（MB） | ユーザーマッピング（はい / いいえ） | 抽出期間（開始、終了、所要時間） | 取り込み時間（開始、終了、所要時間） | 問題 / 解決策 / 詳細 |
|---|---|---|---|---|---|---|---|
|   |   |   |   |   |   |   |   |

## コンテンツ移行の戦略とタイムライン {#content-strategyand-timeline}

次の節では、コンテンツ移行戦略とタイムラインの策定に使用できる重要な手順と関連タスクを示します。

![ 移行戦略の策定手順 ](/help/journey-migration/assets/content-migration2.png)

### フィットメント {#fitment}

* リビジョンのクリーンアップ、データストアのガベージコレクション、データの整合性チェックを実行します。[運用開始の準備](#preparing-for-go-live) も参照してください
* AEM ソースリポジトリに関する [統計の収集](#gathering-data)。
   * セグメントストアのサイズ
   * インデックスストアのサイズ
   * ページ数
   * アセット数
   * ユーザーとグループの数
* 次の機能が AEM ソースで有効になっているかどうかを確認します（AEM as a Cloud Service でも必要です）。
   * スマートタグ付け
   * 類似性検索
   * Word ドキュメントおよび PDF ドキュメント内のテキストを含む検索
* ベストプラクティスアナライザー [レポート](/help/journey-migration/best-practices-analyzer/overview-best-practices-analyzer.md) の収集
* [Cloud Acceleration Manager](/help/journey-migration/cloud-acceleration-manager/introduction/overview-cam.md) へのインポート
   * AEM as a Cloud Service がストレージ要件を処理できることを確認するために、自己分析によるレコメンデーションを確認します。
* 移行計画を続行する前に、不明点があればアドビサポートチケットを作成してください。

### 移行の証明 {#proof-of-migration}

* 次の実稼働クローンをリクエストします。
   * 同じネットワークゾーンにある
   * ユーザーやグループなどの実稼動コンテンツを提供
   * クローンの作成と公開 - クラスターまたは公開ファームの場合は、それぞれ 1 つのノード
* 次のことができるように、移行するコンテンツのサブセットを選択します。
   * 使用可能なすべてのコンテンツタイプの組み合わせです
   * すべてのユーザーとグループを含む
* コンテンツの 25% または最大 1 TB のコンテンツのいずれか小さい方を含みます。
* 実稼働クローンから AEM as a Cloud Service 非実稼働環境へ、完全な [追加](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/ingesting-content.md#top-up-ingestion-process) 移行を少なくとも 1 回実施します。
* 次のような潜在的な問題を解決します。
   * AEM ソースのディスク容量
   * AEM ソースと AEM as a Cloud Service 間の接続
   * あらゆる [取り込みに関連する制限](go-live.md#known-limitations)。
* [抽出と取り込み](#gathering-data) に要した時間を記録します。
   * 1 週間に追加されるコンテンツの量を把握
   * 移行の検証で測定した時間から推定して、 [移行計画](#migration-plan) を作成します。

## 次の手順 {#what-is-next}

AEM インストールをクラウドに移行する準備ができているかどうかを評価する方法を把握し、その準備に必要なツールの使用方法を確認したら、[実稼動段階](/help/journey-migration/go-live.md)に進みます。
