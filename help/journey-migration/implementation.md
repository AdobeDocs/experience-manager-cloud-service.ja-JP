---
title: 実装段階
description: クラウドに移行するためのコードとコンテンツの準備が整っていることを確認します。
source-git-commit: b6667e19ae111685ab4832a1859a62164b4e31c5
workflow-type: tm+mt
source-wordcount: '2422'
ht-degree: 10%

---

# 実装段階 {#implementation-phase}

ジャーニーの実装段階では、コードとコンテンツをAEM as a Cloud Serviceに移行する準備を整えるためのツールについて説明します。

## これまでの説明内容 {#story-so-far}

以前のジャーニーでは、 [AEM as a Cloud Serviceの変更点の理解](/help/journey-migration/getting-started.md)を使用して、デプロイメントを [準備段階](/help/journey-migration/readiness.md).

この記事では、Adobeが提供するツールを使用して、コードとコンテンツをクラウドに移動する準備ができていることを確認する方法に関するアドバイスを引き続き説明します。

## 目的 {#objective}

このドキュメントの目的は次のとおりです。

* コードをAEM as a Cloud Serviceにデプロイするために使用する、Cloud Manager、AEMの継続的統合および配信フレームワークについて紹介します。
* コンテンツ転送ツールをすばやく使用できます
* AEM as a Cloud Serviceのコードを最新化するために使用する必要があるコードリファクタリングツールについて説明します。

## Cloud Manager の使用 {#using-cloud-manager}

AEM as a Cloud Serviceにコードをデプロイする唯一のメカニズムなので、開始する前に、 Cloud Manager について理解しておく必要があります。

Cloud Manager を使用すると、組織がクラウド内の AEM を自己管理できます。このサービスには継続的統合および継続的配信（CI／CD）フレームワークが備わっているので、IT チームや実装パートナーはパフォーマンスやセキュリティを妥協することなくカスタマイズや更新を迅速に配信できます。

Cloud Manager の使い方については、以下のリソースを参照してください。

* [Adobe Experience Manager as a Cloud Service のオンボーディング](/help/onboarding/home.md)：Adobe Experience Manager as a Cloud Service のオンボーディングに関するセルフヘルプリソースについて

* [Git と Adobe Cloud Manager の統合](/help/implementing/cloud-manager/managing-code/integrating-with-git.md)：1 つの Git リポジトリーを使用してコードをデプロイする方法について

* [Adobe Experience Manager as a Cloud Service の設定](/help/security/ims-support.md#aem-configuration)：Admin Console での製品とユーザーアクセスの管理

## Adobeが提供するツールを使用して、コンテンツとコードクラウドを準備する {#use-tools-to-make-code-and-content-cloud-ready}

Cloud Serviceへの移行の正確な手順は、購入したシステムと従うソフトウェア開発ライフサイクルプラクティスによって異なります。

次の図に、AEM as a Cloud Serviceで使用するためのコードとコンテンツの変換に関するフェーズに関する主な手順を示します。

![画像](/help/journey-migration/assets/exec-image1.png)

以下の章では、これを実現するために必要なツールの詳細を説明します。

## コンテンツの移行 {#content-migration}

現在のAEMインスタンスからCloud Serviceインスタンスにコンテンツを移行するには、Adobeのコンテンツ転送ツールを使用します。

このツールを使用すると、ソース AEM インスタンスから AEM Cloud Service インスタンスに転送するコンテンツサブセットを指定できます。

コンテンツ移行は、異なるチーム間での計画、追跡、共同作業を必要とする複数の手順で構成されるプロセスです。

ツールの仕組みと使用方法について詳しくは、 [コンテンツ転送ツールドキュメント](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/overview-content-transfer-tool.md).

## コードリファクタリング {#code-refactor}

### 開発用にセットアップ {#set-up-for-development}

Cloud Servicesと互換性を持たせるために、既存の機能のリファクタリングを開始する時です。

これをおこなうには、コードのリファクタリングを開始する必要がある基本的なツールの詳細を説明したドキュメントを確認する必要があります。


* 計画中は、AEM as a Cloud Serviceとの互換性を保つためにリファクタリングが必要な領域のリストを用意することをお勧めします。 以下を確認できます： [開発ガイドライン](/help/implementing/developing/introduction/development-guidelines.md) を参照して、Cloud Serviceのためのコードのリファクタリングと最適化の方法について確認してください。
* 次の方法をお読みください。 [設定を管理](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/developing/configurations.html?lang=en#what-is-a-configuration) AEM as a Cloud Serviceの
* 次のリンクをダウンロードして、ローカル開発環境を設定する方法を説明します。 [AEMas a Cloud ServiceSDK](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/developing/aem-as-a-cloud-service-sdk.html?lang=en)
* 最後に、 [AEMas a Cloud ServiceJava API](https://www.adobe.io/experience-manager/reference-materials/cloud-service/javadoc/index.html).

また、次のこともできます。

* Dispatcher SDK をローカルにインストールする方法については、このビデオをご覧ください。

   >[!VIDEO](https://video.tv.adobe.com/v/30601)

* Dispatcher SDK の設定方法については、このビデオをご覧ください。

   >[!VIDEO](https://video.tv.adobe.com/v/30602)

### 考え方の変化 {#a-change-in-mindset}

AEM as a Cloud Serviceでコードを開発および実行するには、マインドセットを変更する必要があります。 インスタンスはいつ停止するかわからないので、コードには特に回復力が必要である点に留意してください。Cloud Service で実行するコードは、常にクラスター内で実行されていることを認識している必要があります。つまり、常に複数のインスタンスが実行されています。

クラウドとの互換性を持たせるためには、AEM Maven プロジェクトに一部の変更が必要です。 AEM as a Cloud Serviceでは *コンテンツ* および *コード* を、AEMにデプロイするための個別のパッケージに追加します。

* `/apps` および `/libs` はAEMの不変領域と見なされます。AEMの起動後（つまり実行時）に変更することはできないからです。 これには、作成、更新、削除操作が含まれます。 実行時に不変領域を変更しようとすると失敗します。

* リポジトリ内のその他すべて ( 例： `/content` , `/conf` , `/var` , `/home` , `/etc` , `/oak:index` , `/system` , `/tmp`) はすべて可変領域です。つまり、実行時に変更できます。

詳しくは、 [推奨されるパッケージ構造](/help/implementing/developing/introduction/aem-project-content-package-structure.md#recommended-package-structure) ドキュメント。


### クラウド移行ツール {#cloud-migration-tools}

Adobeには、コードリファクタリングタスクの一部を高速化するのに役立つツールがいくつか用意されています。 これらのツールと解決する問題を理解することで、移行の複雑さと時間を削減できます。

* [アセットワークフローの移行](/help/journey-migration/moving-to-aem-assets/asset-workflow-migration-tool.md)：アセット処理ワークフローを自動的に移行するために使用されるツール
* [Dispatcher コンバーター](/help/journey-migration/refactoring-tools/dispatcher-transformation-utility-tools.md)の場合に、既存の Dispatcher 設定を、AEM as a Cloud Serviceに対応する形式に変換するツール。
* [Repository Modernizer](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/moving/refactoring-tools/repo-modernizer.html?lang=en):AEM Multomode プロジェクトを入力として取り、AEM as a Cloud Serviceプロジェクトに変換するツール
* [インデックスコンバータ](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/moving/refactoring-tools/index-converter.html?lang=en)、インデックスをAEM as a Cloud Service互換のフォームに変換するツール
* [最新化ツール](/help/journey-migration/refactoring-tools/aem-modernization-tools.md)：従来のAEM機能をAEM as a Cloud Serviceの最新のサポート対象機能に変換するために使用できるユーティリティスイート。

ローカル開発環境を設定したら、AEM as a Cloud Service SDK について、 [ドキュメント](/help/implementing/developing/introduction/aem-as-a-cloud-service-sdk.md).

### コードの凍結のスケジュール設定 {#schedule-a-code-freeze}

移行プロセスの一環として、アクティブなAEM上で進行中のコード開発をコードリファクタリングタスクと共に管理するには、AEM as a Cloud Serviceとの互換性を持たせて Maven プロジェクトの再構築を完了するまで、コードをフリーズする期間を設定することをお勧めします。

プロジェクトの再構築が完了したら、この新しい構造に基づいて新しいコード開発を再開できます。 これにより、コードのデプロイメントとテスト中に Cloud Manager パイプラインのエラーが発生するのを減らします。

>[!NOTE]
>コンテンツ転送タスクとコードリファクタリングタスクは、順番に実行する必要はありません。 これらのタスクは互いに独立に実行することができます。ただし、Cloud Service 環境でコンテンツが正常にレンダリングされるようにするには、正しいプロジェクト構造が必要です。

## コードのデプロイメントとテストのベストプラクティス {#best-practices}

Cloud Manager パイプラインは、ステージ環境に対するテストの実行をサポートしています。

コード品質テストに関する以下のドキュメントのベストプラクティスに従います。

* [コード品質テスト](/help/implementing/cloud-manager/code-quality-testing.md)：テストスクリプトの作成プロセスを説明し、少なくとも 50 %の推奨カバレッジの概念を説明するドキュメント。
* [カスタムコード品質ルールについて](/help/implementing/cloud-manager/custom-code-quality-rules.md) これは、AEM Engineering のベストプラクティスに基づいて作成された Cloud Manager で実行されるカスタムコード品質ルールを説明するためのものです。

## 運用開始の準備 {#preparing-for-go-live}

移行元システムを準備するには、システムおよびAEM管理者レベルのタスクが必要です。 まず、 [リビジョンのクリーンアップ](https://experienceleague.adobe.com/docs/experience-manager-65/deploying/deploying/revision-cleanup.html?lang=ja) そして [データストアのガベージコレクション](https://experienceleague.adobe.com/docs/experience-manager-65/administering/operations/data-store-garbage-collection.html) タスクのステータス。 AEMバージョン 6.3（コンテンツ転送ツールはバージョン 6.3 以降と互換性があるので）を実行している場合は、オフライン圧縮を実行し、その後にデータストアのガベージコレクションを実行することをお勧めします。

[データ整合性チェック](https://experienceleague.adobe.com/docs/experience-manager-65/deploying/configuring/consistency-check.html) は、すべてのAEMバージョンをまたいで推奨され、コンテンツリポジトリの移行作業を適切な状態に保ちます。

インストールと設定を行うには、システム管理者レベルのアクセス権が必要です [AZCopy](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/handling-large-content-repositories.md)

また、未使用のアセット、ページ、AEMプロジェクト、ユーザーおよびグループを確認して、移行時の時間を節約することをお勧めします。 詳しくは、 [コンテンツリポジトリのヘルス](#repository-health) 」セクションに入力します。

### コンテンツリポジトリのヘルス {#repository-health}

1 回のアクセスで [実稼動クローン](#proof-of-migration) が確立され、リポジトリのヘルスを確認する処理が続行されます。 前の節で説明したように、目的は、移行を開始する前に、ソース上のリポジトリをクリーンアップし、コンパクト化することです。 この手順を使用すると、移行が開始した後に問題のトラブルシューティングに費やす時間が大幅に節約される可能性があります。

| 作業項目 | 重要な留意点 |
|---------|----------|
| ユーザー、グループ、権限 | メンバーシップに関するユーザー、グループ、複雑さの量を理解する必要があります。 移行前に、未使用のユーザー、ソース内のグループをクリーンアップする機会を探します。 |
| 不完全なアセット処理 | 移行を開始する前に、ソースシステム内のアセットの処理を完了して、AEMの移行後に発生する可能性のある問題を回避します。 |
| コンテンツの正常性 | 移行を開始する前に、正しくないコンテンツをクエリし、パージすることをお勧めします。 例えば、オリジナルのレンディションを持たないアセットや、ワークフロー処理で動かないページを探します。 関連トピック [アセットの正常性](#asset-health). |

## データの収集 {#gathering-data}

>[!NOTE]
> この [コンテンツ移行の戦略とタイムライン](#content-strategy-and-timeline) この節では、収集したデータを推定して移行計画を作成する方法について詳しく説明します。

データの収集は、移行作業および関連タスクの計画に役立ちます。 抽出と取り込みの時間は、データポイントが移行セットの特定のサイズに関連付けられるので、特に便利です。 そのため、次のデータポイントを基に計画を作成できます。

* 所要時間 [抽出](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/extracting-content.md)
* 所要時間 [取得](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/ingesting-content.md)
* 追加に要した合計時間 [抽出](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/extracting-content.md#top-up-extraction-process)
* 追加に要した合計時間 [取得](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/ingesting-content.md#top-up-ingestion-process)

もう 1 つの重要なデータポイントは、 [ユーザーマッピング](/help/journey-migration/content-transfer-tool/user-mapping-tool/overview-user-mapping-tool.md)（コンテンツ移行と組み合わせて使用する場合） このデータポイントを考慮して、より現実的な推定をおこなうことができます。これは、このデータポイントが抽出タイムライン全体に追加され、追加時に実行する必要がない場合があるからです。

これらのデータポイントは [KPI の設定](/help/journey-migration/readiness.md#establish-kpis) およびその他の移行関連タスク

### 移行プラン {#migration-plan}

収集したデータポイント（上記を参照）に基づいて、マクロプロジェクトプランに統合できる移行プランを作成できます。 この手順により、すべての主要関係者が移行アクティビティを視覚化し、計画できるようになります。

次の表に、一般的な移行計画を示します。

| 移行の反復 | 開始日 | 推定終了日 | 依存関係 | 推定期間（日数） | 追加の詳細/アクション項目 |
|---|---|---|---|---|---|
| PRDCLONE-AUTHOR-INITIAL-USRMAP-CSSTAGE-AUTHOR |  |  |  |  |  |
| PRDCLONE-PUBLISH-TOPUP-CSSTAGE-AUTHOR |  |  |  |  |  |

上の表に示すように、特定の命名形式に従って移行の繰り返しを識別すると便利です。例えば、次のようになります。 **PRDCLONE** ソースAEM環境の場合、 **作成者/発行** AEMas a Cloud Service環境の場合、 **CSSTAGE-AUTHOR** AEMas a Cloud Serviceインスタンスなどの

移行計画に影響を与える重要な詳細：

**必要な抽出の合計数**

* 特定の環境でのオーサーおよびパブリッシュの抽出は、互いに独立しているので、2 つの並列抽出と見なされます。
* 特定の期間でのリポジトリの増加に基づく追加抽出の数。

**必要なインジェスションの合計数**

* 抽出セットは複数のCloud Service環境に取り込めるので、この項目をプランに取り込むことが重要です。
* 追加インジェスションの数。
* すべてのオーサーコンテンツをCloud Serviceパブリッシュに取り込まないようにするためには、ベストプラクティスとして、ソースオーサーから Cloud Service オーサーインスタンス、ソースパブリッシュからCloud Serviceパブリッシュにコンテンツを移行することが推奨されます。

### 移行トラッカー {#migration-tracker}

移行トラッカーを使用して、初期実行と追加実行の両方の時間をメモすることができます。 これらのデータポイントは、最終的な追加がおこなわれる前に、現実的なコンテンツ凍結要件を策定するのに役立ちます。

トラッカーは、次の操作もおこなうのに役立ちます。

* 計画または実稼働タイムラインの調整が必要なプランナーからの逸脱を識別します。
* すべての必要な通信で使用できる現実的なステータスを提供する
* 初期または将来の追加移行の計画

次の表に、機能移行トラッカーを示します。

| ソース（環境/インスタンス/ URL） | 宛先（環境/インスタンス/ URL） | 移行セット名、タイプ（初期または追加） | 移行セットのサイズ (MB) | ユーザーマッピング（はい/いいえ） | 抽出期間（開始、終了、所要時間） | 取り込み時間（開始、終了、所要時間） | 問題/解決策/詳細 |
|---|---|---|---|---|---|---|---|
|  |  |  |  |  |  |  |  |

## コンテンツ移行の戦略とタイムライン {#content-strategyand-timeline}

次の節では、コンテンツ移行戦略やタイムラインの策定に使用できる重要な手順と関連タスクを示します。

![画像](/help/journey-migration/assets/content-migration2.png)

### フィットメント {#fitment}

* リビジョンのクリーンアップ、データストアのガベージコレクション、およびデータ整合性チェックを実行します。 関連トピック [運用開始の準備](#preparing-for-go-live)
* [統計の収集](#gathering-data) AEMソースリポジトリについて：
   * セグメントストアのサイズ
   * インデックスストアのサイズ
   * ページ数
   * アセット数
   * ユーザーとグループの数
* 次の機能がAEMソースで有効になっているかどうかを確認します (AEM as a Cloud Serviceでも必要 )。
   * スマートタグ付け
   * 類似性検索
   * Word および PDF ドキュメント内のテキストを含む検索
* ベストプラクティスアナライザーの収集 [レポート](/help/journey-migration/best-practices-analyzer/overview-best-practices-analyzer.md)
* を [Cloud Acceleration Manager](/help/journey-migration/cloud-acceleration-manager/introduction/overview-cam.md)
   * 自己分析の推奨事項を確認し、AEM as a Cloud Serviceがストレージ要件を処理できることを確認します。
* 移行計画を続行する前に、Adobeサポートチケットを作成して、説明を追加してください。

### 移行の検証 {#proof-of-migration}

* 次の本番クローンをリクエストします。
   * 同じネットワークゾーンに存在する
   * ユーザーやグループのような実稼動用コンテンツを提供します
   * オーサーとパブリッシュのクローンを作成します。クラスターまたはパブリッシュファームの場合は、それぞれ 1 つのノード
* 移行するコンテンツのサブセットを選択して、次の操作を実行します。
   * 使用可能なすべてのコンテンツタイプが組み合わされています
   * 大文字と小文字のすべてのユーザーとグループが含まれます [ユーザーマッピング](/help/journey-migration/content-transfer-tool/user-mapping-tool/overview-user-mapping-tool.md) 必須
* コンテンツの 25%または最大 1 TB のコンテンツのいずれか小さい方を含みます。
* 少なくとも 1 つのフルを実行し、 [トップアップ](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/ingesting-content.md#top-up-ingestion-process) 本番クローンからAEMas a Cloud Serviceの非本番環境への移行
* 以下のような潜在的な問題を解決します。
   * AEMソース上のディスク容量
   * AEMソースとAEM as a Cloud Service間の接続
   * 任意 [取得に関する制限](go-live.md#known-limitations).
* 所要時間を記録 [抽出と取り込み](#gathering-data):
   * 1 週間に追加されるコンテンツの量を把握する
   * 移行の証明から測定された時間を推定し、 [移行計画](#migration-plan).

## 次の手順 {#what-is-next}

AEMのインストールをクラウドに移行する準備ができているかどうかを評価する方法を完全に理解したら、準備に必要なツールの使用方法を学ぶため、次に [運用開始段階](/help/journey-migration/go-live.md).
