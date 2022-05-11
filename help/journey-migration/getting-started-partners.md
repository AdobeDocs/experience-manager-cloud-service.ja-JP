---
title: Experience Manager as a Cloud Service への移行ガイド（パートナー向け）
description: Experience Manager as a Cloud Service への移行ガイド（パートナー向け）
exl-id: 9d5a72b8-06af-4b82-ab20-e65aea7903b3
source-git-commit: 595eff9c259208754ac62ea27dfc6be7d74b79d3
workflow-type: tm+mt
source-wordcount: '2126'
ht-degree: 98%

---

# Adobe Experience Manager as a Cloud Service への移行ガイド（パートナー向け） {#Overview}

>[!CONTEXTUALHELP]
>id="aemcloud_migration_overview"
>title="AEM as a Cloud Service への移行"
>abstract="様々な Experience Manager のデプロイメントから Experience Manager as a Cloud Service まで顧客をトランジションするために推奨される段階的アプローチの概要を説明し、既存の顧客が接続された継続的なエクスペリエンスを提供できるようにします。"
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/overview/what-is-new-and-different.html?lang=ja" text="新機能と新着情報"
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/overview/introduction.html?lang=ja" text="AEM as a Cloud Service の概要"

Adobe Experience Manager（AEM）as a Cloud Service は、コンテナベースのインフラストラクチャ、API 主導の開発、およびガイド付き DevOps プロセスに基づいて構築された、Experience Manager の再構築基盤を提供し、マーケターとデベロッパーがカスタマーエクスペリエンス管理のイノベーションで常に時代を先取りできるようにします。

Cloud Service は、Adobe Experience Manager の豊富な機能と拡張性を、最新のクラウドネイティブアーキテクチャの俊敏性を組み合わせて、ブランドが消費者の絶え間ない要求に応えることを可能にします。

この概要では、様々な Experience Manager のデプロイメントから Experience Manager as a Cloud Service まで顧客をトランジションするために推奨される段階的アプローチの概要を説明し、既存の顧客が、エクスペリエンス管理という目的を持って構築された最新プラットフォームで、接続された継続的なエクスペリエンスを提供できるようにします。

<!-- It primarily focuses on:
* Getting Started with Adobe Experience Manager as a Cloud Service
* Developer Journey in Adobe Experience Manager as a Cloud Service
* Moving to Adobe Experience Manager as a Cloud Service -->

移行ジャーニーの一般的な表示については、以下の図を参照してください。

![画像](/help/journey-migration/assets/migration-process.png)

## Adobe Experience Manager as a Cloud Service について {#getting-started}

| 何が違うのか？ | アーキテクチャの概要 |
|--------------------------|--------------------------|
| <ul><li>[最新アーキテクチャ](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/overview/architecture.html?lang=ja)</li><li>[自動更新](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/deploying/aem-version-updates.html?lang=ja#aem-version-updates)</li><li>[Cloud Manager](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/introduction-to-cloud-manager.html?lang=ja)</li><li>[アセットマイクロサービス](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/assets/asset-microservices-overview.html?lang=ja)</li><li>[Direct-Access バイナリ](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/assets/asset-microservices-overview.html?lang=ja#asset-upload-with-direct-binary-access)</li><li>[コードとコンテンツの分離](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/developing/aem-project-content-package-structure.html?lang=ja#developing)</li><li>[サービスとしてのレプリケーション](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/operations/replication.html?lang=ja)</li><li>[Admin Console、グループ／ユーザーのメンバーシップ、ACL](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/security/ims-support.html?lang=ja)</li></ul> | <ul><li>[AEM アーキテクチャの概要](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/underlying-technology/introduction-architecture.html?lang=ja#underlying-technology)</li><li>[環境スタック](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/overview/architecture.html)</li><li>[オーサー層](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/underlying-technology/introduction-author-publish.html?lang=ja#underlying-technology)</li><li>[パブリッシュ層](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/underlying-technology/introduction-author-publish.html?lang=en#underlying-technology)</li><li>[Dispatcher](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/content-delivery/disp-overview.html?lang=ja#content-delivery)</li><li>[CDN](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/content-delivery/cdn.html?lang=ja#content-delivery) </li><li>[Cloud Manager](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/introduction-to-cloud-manager.html)（CI/CD）</li><li>[Admin Console](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/security/ims-support.html) を介した [ID 管理](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/security/ims-support.html?lang=ja#onboarding-users-in-admin-console)</li><li>[Asset Compute Service](https://experienceleague.adobe.com/docs/asset-compute/using/home.html?lang=ja)</li></ul> |

![AEM as a Cloud Service - ランタイムアーキテクチャ](/help/overview/assets/concepts-03.png "AEM as a Cloud Service - ランタイムアーキテクチャ")

<br>

## Adobe Experience Manager as a Cloud Service でのデベロッパージャーニー {#developer-journey}

### 開発

Adobe Experience Manager as a Cloud Service でのコード開発の基本は、Adobe Experience Manager オンプレミスや Managed Services ソリューションの場合と同様です。

デベロッパーはコードを作成しローカルでテストします。コードはその後、リモートの Adobe Experience Manager as a Cloud Service 環境にプッシュされます。

Experience Manager as a Cloud Service のデプロイメントをカスタマイズする方法については、Experience Manager as a Cloud Service の実装に関するセルフヘルプリソースを参照してください。

| ローカル開発セットアップ | 開始する前に知っておくべきこと |
|-----------|------------|
| <ol><li>詳しくは、 [Adobe Experience Manager SDK](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/developing/aem-as-a-cloud-service-sdk.html?lang=ja#developing) のドキュメントを参照してください。</li><li>Dispatcher SDK のインストール方法については、「[Dispatcher SDK のインストール](https://video.tv.adobe.com/v/30601)」を視聴してください。</li><li>Dispatcher SDK の設定方法については、「[Dispatcher SDK の設定](https://video.tv.adobe.com/v/30602)」を視聴してください。</li><li>詳細については、 [ローカル開発セットアップ](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/local-development-environment-set-up/overview.html?lang=ja#local-development-environment-set-up) のドキュメントを参照してください。</li><li>Experience Manager [ウォークスルー](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/accessing/walk-through.html?lang=ja#accessing)へのアクセスの設定</li></ol> | <ol><li>[開発の基本](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/developing/aem-as-a-cloud-service-sdk.html?lang=en#developing)</li><li>[開発のガイドライン](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/developing/development-guidelines.html?lang=ja#developing)</li><li>[Experience Manager プロジェクト構造について](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/developing/aem-project-content-package-structure.html?lang=en#developing)</li><li>[コアコンポーネント](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html?lang=ja)</li><li>[Digital Foundation ブループリント](https://solutionpartners.adobe.com/content/dam/spp_assets/restricted/community/community_31/digital_foundation_best_practices_and_documentation.zip)</li><li>[スタイルシステム](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/sites/authoring/features/style-system.html?lang=ja#authoring)</li><li>[オーバーレイ](/help/implementing/developing/introduction/overlays.md)</li><li>[Experience Manager as a Cloud Service API レファレンス](https://www.adobe.io/experience-manager/reference-materials/cloud-service/javadoc/)</li></ol> |

>[!TIP]
> [WKND を開発し、ローカル Experience Manager SDK にデプロイする方法](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-wknd-tutorial-develop/overview.html?lang=ja)に関するチュートリアルを参照してください。

### デプロイ

開発者はコードを作成しローカルでテストします。コードはその後、リモートの AEM as a Cloud Service 環境にプッシュされます。

Cloud Manager（Managed Services のオプションのコンテンツ配信ツール）が必要です。これが、AEM as a Cloud Service 環境にコードをデプロイするための唯一のメカニズムになりました。

AEM as a Cloud Service 環境を設定およびデプロイする方法については、セルフヘルプのリソースを参照してください。

1. [CM パイプラインを設定](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/configure-pipeline.html?lang=ja#using-cloud-manager)
   * 実稼動パイプライン
   * 非実稼動パイプラインとコード品質専用パイプライン
2. [コードのデプロイ](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/deploy-code.html?lang=ja#using-cloud-manager)
3. [テスト結果について](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/test-results/overview-test-results.html?lang=ja#using-cloud-manager)
4. **ログへのアクセス**
   * [CM UI 経由](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/manage-logs.html?lang=ja#using-cloud-manager)
   * [Adobe I/O CLI 経由](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/debugging/debugging-aem-as-a-cloud-service/logs.html?lang=ja#debugging)
5. [運用と保守](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/operations/home.html?lang=ja)
   * [OSGI 設定の設定](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/deploying/configuring-osgi.html?lang=ja#deploying)
   * [バックアップと復元](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/operations/backup.html?lang=ja)

>[!TIP]
> [WKND を Experience Manager Cloud Service にデプロイする](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-wknd-tutorial-develop/overview.html)方法のチュートリアルを参照する

### ヘルプとリソース

1. [デバッグのヒントとテクニック](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/debugging/debugging-aem-as-a-cloud-service/overview.html?lang=ja#debugging-aem-as-a-cloud-service)
2. [デベロッパーコンソール](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/debugging/debugging-aem-as-a-cloud-service/developer-console.html?lang=ja#debugging)
3. [CRXDE Lite](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/debugging/debugging-aem-as-a-cloud-service/crxde-lite.html?lang=ja#debugging)（ローカル SDK および Experience Manager クラウド開発環境でのみ使用可能）
4. [ログとログ作成](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/debugging/debugging-aem-as-a-cloud-service/logs.html?lang=en#debugging)
   * [CM ログ](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/debugging/debugging-aem-as-a-cloud-service/build-and-deployment.html?lang=ja#debugging)（build-unit-testing、code-scanning、build-image、deploy）
   * [Experience Manager Cloud Service ログ](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/debugging/debugging-aem-as-a-cloud-service/logs.html?lang=en#debugging)（aemerror、aemaccess、aemrequest、aemdispatcher、httpderror、httpaccess）
   * ローカル SDK ログ（host:port/crx-quickstart/logs 下）

>[!NOTE]
> その他のヘルプについては、以下を参照してください。
>1. [Experience Manager サポートチームに問い合わせる](https://experienceleague.adobe.com/docs/customer-one/using/home.html?lang=ja)
>2. [Experience Manager コミュニティとフォーラム](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-manager/ct-p/adobe-experience-manager-community?profile.language=ja)を探索する


<br>

## Adobe Experience Manager as a Cloud Service への移行 {#move-to-cloud}

>[!CONTEXTUALHELP]
>id="aemcloud_move_to_cloud"
>title="Adobe Experience Manager as a Cloud Service への移行"
>abstract="この概要では、様々な Experience Manager のデプロイメントから Experience Manager as a Cloud Service まで顧客をトランジションするために推奨される段階的アプローチの概要を説明し、既存の顧客が、エクスペリエンス管理という目的を持って構築された最新プラットフォームで、接続された継続的なエクスペリエンスを提供できるようにします。"

**Experience Manager as a Cloud Service は、Experience Manager Sites および Assets に対する、拡張性、安全性、機敏性の高いテクノロジー基盤となるので、マーケターや IT 部門は、インパクトの強いエクスペリエンスの大規模な提供に専念できます。**

Experience Manager as a Cloud Service を使用すると、チームは製品アップグレード計画ではなく技術革新に専念できます。新しい製品機能は徹底的にテストされ、中断することなくチームに提供されるので、常に最新のアプリケーションにアクセスできます。

Cloud Service への移行プロセスには、計画、実行、運用開始後の 3 つの段階が含まれています。移行をうまくスムーズに行うには、適切な計画を立て、本ガイドで概要を説明しているベストプラクティスに従う必要があります。

次の図に、推奨されるCloud Serviceへの移行プロセスの概要を示します。

![画像](/help/journey-migration/assets/home-img1.png)

<br>

### 計画

Cloud Service への移行プロセスを開始する前に、Experience Manager as a Cloud Service に習熟し、それに対する主要な変更点を確認すると共に、置換または廃止された機能も確認する必要があります。

<table>
<tr>
<td>プロジェクトの確認と評価</td>
<td><ul><li>Adobe Experience Manager as a Cloud Service と Experience Manager 6.x との重要な違いを理解するには、「<a href="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/release-notes/aem-cloud-changes.html?lang=ja">Experience Manager as a Cloud Service の注目すべき変更</a>」を参照してください。</li><li>非推奨とマークされた機能と特徴の詳細については、「<a href="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/release-notes/deprecated-removed-features.html?lang=ja#deprecated-features">非推奨の機能</a>」を参照してください。</li><li>[Cloud Service の移行のみ] Cloud Service の準備状況の評価：ソース環境で <a href="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/best-practices-analyzer/overview-best-practices-analyzer.html?lang=en#cloud-migration">ベストプラクティスアナライザー（BPA）</a> を実行します。 </li><li>Experience Manager CS の主な変更点と廃止された機能に対する評価を完了します。</li></ul></td>
</tr>
<tr>
<td>レビュー</td>
<td><ul><li>確認に基づき、作業の見積もりとリソースエクササイズを実行します。</li></ul></td>
</tr>
<tr>
<td>測定</td>
<td><ul><li><a href="https://experienceleague.adobe.com/welcome/aem/part6.html?lang=ja">プロジェクト KPI</a>、成功基準、プロジェクト日程を確立します。</li></ul></td>
</tr>
</table>

>[!NOTE]
>ベストプラクティスアナライザーレポートを使用すれば、情報を手動で収集および評価する必要がなくなるので、AEM as a Cloud Service の移行にかかる時間とコストをすばやく見積もれるようになります。


<br>

### 実行

プロジェクトの実行段階を開始する前に、Cloud Service の利用を開始する必要があります。また、Cloud Manager について理解しておく必要があります。これは、プロジェクトコードを Experience Manager Cloud Service インスタンスに配置するための仕組みです。

Cloud Manager を使用すると、組織がクラウド内の Experience Manager を自己管理できます。このサービスには継続的統合および継続的配信（[CI／CD](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/overview/ci-cd-pipeline.html?lang=ja#overview)）のフレームワークが備わっているので、IT チームや実装パートナーはパフォーマンスやセキュリティを妥協することなくカスタマイズや更新を迅速に配信できます。

#### コンテンツの移行

1. [コンテンツ転送ツール](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/migration/content-transfer-tool.html?lang=ja#migration)：既存のコンテンツをソース AEM インスタンス（オンプレミスまたは AMS）からターゲット AEM Cloud Service インスタンスに移動するために使用します。
2. [パッケージマネージャー](https://experienceleague.adobe.com/docs/experience-manager-65/administering/contentmanagement/package-manager.html?lang=ja#package-manager)：リポジトリーの可変コンテンツのインポートおよびエクスポートに使用します。


#### リファクタリング／最適化

| はじめに | コードの確認とリファクタリング | ディスパッチャーの確認 |
|---|---|---|
| <ul><li>[ローカル開発の設定](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/local-development-environment-set-up/overview.html?lang=en#local-development-environment-set-up)</li><li>[ローカルディスパッチャーの設定](https://video.tv.adobe.com/v/30602/)</li><li>[SDK API jar を使用してコードをコンパイルする](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/developing/aem-as-a-cloud-service-sdk.html?lang=en#developing)</li><li>[AEM 開発のガイドラインの確認](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/developing/development-guidelines.html?lang=en#developing)<ul><li>バックグラウンドタスクと長時間実行ジョブ</li><li>Sling スケジューラー</li><li>入力ストリームの使用状況など</li></ul></li></ul> | <ul><li>ソース環境で [ベストプラクティスアナライザー（BPA）](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/best-practices-analyzer/overview-best-practices-analyzer.html?lang=ja#cloud-migration) を実行する。[**移行のみ**]<ul><li>プロジェクト構造の考慮事項（[クラウドのアーキタイプ](https://github.com/adobe/aem-project-archetype)を基に）<ul><li>コードとコンテンツの分離（可変と不変）</li><li>[カスタムインデックス定義](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/operations/indexing.html?lang=ja#indexing)</li><li>[カスタム実行モード](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/deploying/overview.html?lang=ja#runmodes)</li></ul></li></ul></li><li>必要な変更を確認し、実行する</li><li>ローカル SDK [にデプロイ](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-wknd-tutorial-develop/overview.html?lang=ja)する</li><li>AEM SDK を介してスモークテストを実行</li></ul> | <ul><li>[ディスパッチャー設定](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/content-delivery/disp-overview.html?lang=ja#local-validation-of-dispatcher-configuration)のリファクタリングを確認</li><li>必要に応じて、[Dispatcher コンバーター](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/refactoring-tools/dispatcher-transformation-utility-tools.html?lang=ja#introduction-dispatcher)ツールを利用する。[**移行のみ**]</li><li>テストは[ディスパッチャー SDK](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/local-development-environment-set-up/dispatcher-tools.html?lang=ja#prerequisites) を使用して実行可能</li></ul> |

>[!TIP]
> アセット顧客：[アセットクラウド移行](https://github.com/adobe/aem-cloud-migration)ツールを使用したアセットワークフローの確認とリファクタリング


#### デプロイメント／実稼働開始

1. [Cloud Manager](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/managing-code/setup-cloud-manager-git-integration.html?lang=ja#managing-code) git へのデプロイ
2. [Cloud Manager 品質パイプライン](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/how-to-use/understand-your-test-results.html?lang=ja#how-to-use)を介してカスタマーコードを実行
3. [開発環境へのデプロイ](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/debugging/debugging-aem-as-a-cloud-service/build-and-deployment.html?lang=en#debugging)
4. [**移行のみ**]&#x200B;パッケージまたは[コンテンツ転送ツール](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/getting-started-content-transfer-tool.md)（CTT）を使用したコンテンツの転送
5. 推奨されるテストサイクル（スモークテスト、QA など）の実行
6. Cloud Manager 実稼働パイプラインへの昇格
7. スモークテスト検証
8. 運用開始

<br>

### 運用開始後

運用開始後段階では、一時ファイルの確実なクリーンアップ、継続的な開発に関するベストプラクティスの確認、ログの管理が必要です。

>[!TIP]
> AEM as a Cloud Service 環境のトラブルシューティングには、ツールを使用できます。
>1. [デベロッパーコンソール](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/developing/development-guidelines.html?lang=ja#aem-as-a-cloud-service-development-tools)
>2. [CRX/DE Lite](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/debugging/debugging-aem-as-a-cloud-service/crxde-lite.html?lang=en#debugging)
>3. [ログの管理](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/manage-logs.html?lang=en#using-cloud-manager)


<br>

### ツールとリソース

| 評価 | リファクタリング | Experience Manager の最新化 | コンテンツの移行 |
|------------|-------------|---------------------------------|-------------------|
| <ul><li>[ベストプラクティスアナライザー](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/best-practices-analyzer/overview-best-practices-analyzer.html?lang=en#cloud-migration)</li></li> | <ul><li>[Unified Experience プラグイン](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/refactoring-tools/unified-experience.html?lang=ja#refactoring-tools)</li></ul> | <ul><li>[静的テンプレートから編集可能テンプレートへ](https://opensource.adobe.com/aem-modernize-tools/pages/tools/page-structure.html)</li><li>[デザイン設定からポリシーへ](https://opensource.adobe.com/aem-modernize-tools/pages/tools/policy-importer.html) <li>[基盤コンポーネントからコアコンポーネントへ](https://opensource.adobe.com/aem-modernize-tools/pages/tools/component.html)</li><li>[クラシック UI からタッチ操作対応 UI へ](https://opensource.adobe.com/aem-modernize-tools/pages/tools/dialog.html)</li></ul> | <ul><li>[コンテンツ転送ツール](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/using-content-transfer-tool.html?lang=ja#cloud-migration)</li><li>[パッケージマネージャー](https://experienceleague.adobe.com/docs/experience-manager-65/administering/contentmanagement/package-manager.html?lang=ja#contentmanagement)</li></ul> |

>[!NOTE]
> その他のヘルプについては、以下を参照してください。
>1. [Experience Manager サポートチームに問い合わせる](https://experienceleague.adobe.com/docs/customer-one/using/home.html?lang=en)
>2. [Experience Manager コミュニティとフォーラム](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-manager/ct-p/adobe-experience-manager-community)を探索する

