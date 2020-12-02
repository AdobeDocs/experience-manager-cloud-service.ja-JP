---
title: Cloud ServiceとしてのExperience Managerへの移行に関する1ページ
description: Cloud ServiceとしてのExperience Managerへの移行に関する1ページ
translation-type: tm+mt
source-git-commit: 02e6581ec5a922d71c53e99212a1f8aecc405f6f
workflow-type: tm+mt
source-wordcount: '2085'
ht-degree: 12%

---


# Cloud Service{#Overview}としてAdobe Experience Managerへの移行

>[!CONTEXTUALHELP]
>id="aemcloud_migration-overview"
>title="クラウドサービスとしてのAEMへの移行"
>abstract="様々なExperience Managerの導入からExperience Managerまで、トランジションのお客様に対してCloud Serviceとして推奨される段階的アプローチの概要を説明し、既存のお客様が接続された継続的な経験を提供できるようにします。"
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/overview/what-is-new-and-different.html?lang=en" text="新機能と新機能"
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/overview/introduction.html?lang=en" text="AEM as a Cloud Service の概要."

Adobe Experience Manager(AEM)は、Cloud Serviceオファーとして、コンテナベースのインフラストラクチャ、API主導の開発、ガイド付きDevOpsプロセスに基づくExperience Managerの再設計基盤を構築し、マーケティング担当者や開発者は、カスタマーエクスペリエンス管理の革新性を常に先に進めます。

Cloud Serviceは、Adobe Experience Managerの豊富な機能と拡張性を、最新のクラウドネイティブアーキテクチャの俊敏性と共に統合し、ブランドは、今までない消費者の需要を満たすことができます。

この1ページでは、様々なExperience Managerの導入からExperience Managerまで、トランジションのお客様に推奨される各段階的なアプローチをCloud Serviceとしてまとめ、既存のお客様が、この目的に合った、目的に合った最新のプラットフォームで連続的な体験を提供できます。

<!-- It primarily focuses on:
* Getting Started with Adobe Experience Manager as a Cloud Service
* Developer Journey in Adobe Experience Manager as a Cloud Service
* Moving to Adobe Experience Manager as a Cloud Service -->

<br>

## Cloud ServiceとしてAdobe Experience Managerを使い始める{#getting-started}

| 何が違う？ | アーキテクチャの概要 |
|--------------------------|--------------------------|
| <ul><li>[モダンアーキテクチャ](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/core-concepts/architecture.html)</li><li>[自動更新](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/deploying/aem-version-updates.html?lang=en#aem-version-updates)</li><li>[Cloud Manager](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/introduction-to-cloud-manager.html)</li><li>[Asset Microservices](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/assets/asset-microservices-overview.html)</li><li>[Direct-Accessバイナリ](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/assets/asset-microservices-overview.html?lang=en#asset-upload-with-direct-binary-access)</li><li>[コードとコンテンツの分離](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/developing/aem-project-content-package-structure.html?lang=en#developing)</li><li>[サービスとしてのレプリケーション](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/operations/replication.html?lang=en)</li><li>[管理コンソール、グループ/ユーザーのメンバーシップおよびACL](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/security/ims-support.html)</li></ul> | <ul><li>[AEMアーキテクチャの概要](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/underlying-technology/introduction-architecture.html?lang=en#underlying-technology)</li><li>[環境スタック](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/core-concepts/architecture.html)</li><li>[オーサー層](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/underlying-technology/introduction-author-publish.html?lang=en#underlying-technology)</li><li>[パブリッシュ層](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/underlying-technology/introduction-author-publish.html?lang=en#underlying-technology)</li><li>[Dispatcher](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/content-delivery/disp-overview.html?lang=en#content-delivery)</li><li>[CDN](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/content-delivery/cdn.html?lang=en#content-delivery) </li><li>[Cloud Manager](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/introduction-to-cloud-manager.html) (CI/CD)</li><li>[管理コンソ](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/security/ims-support.html?lang=en#onboarding-users-in-admin-console) ールを使用したID [管理](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/security/ims-support.html)</li><li>[Asset Compute Service](https://experienceleague.adobe.com/docs/asset-compute/using/home.html)</li></ul> |

![AEM as a Cloud Service - ランタイムアーキテクチャ](/help/core-concepts/assets/concepts-03.png "AEM as a Cloud Service - ランタイムアーキテクチャ")

<br>

## Cloud ServiceとしてのAdobe Experience Managerでの開発者の遍歴{#developer-journey}

### 開発

Adobe Experience Managerでのコード開発の基本は、Adobe Experience Manager・オンプレミスやManaged Servicesのソリューションと比較してCloud Service的に似ています。

開発者はコードを書いてローカルでテストし、その後Cloud Service環境としてリモートAdobe Experience Managerに送り出します。

Cloud Serviceの導入としてのExperience Managerのカスタマイズ方法については、Cloud ServiceとしてのExperience Managerの導入に関するセルフヘルプリソースを参照してください。

| ローカル開発セットアップ | 開始の前に知っておくべきこと |
|-----------|------------|
| <ol><li>詳しくは、[Adobe Experience ManagerSDK](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/developing/aem-as-a-cloud-service-sdk.html?lang=en#developing)のドキュメントを参照してください。</li><li>[ディスパッチャーSDKのインストール](https://video.tv.adobe.com/v/30601?captions=jpn)を視聴して、ディスパッチャーSDKのインストール方法を理解してください</li><li>ディスパッチャーSDKの設定方法については、[ディスパッチャーSDKの設定](https://video.tv.adobe.com/v/30602?captions=jpn)を視聴してください</li><li>詳細については、[ローカル開発セットアップ](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/local-development-environment-set-up/overview.html?lang=en#local-development-environment-set-up)のドキュメントを参照してください</li><li>Experience Manager[ウォークスルー](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/accessing/walk-through.html?lang=en#accessing)へのアクセスの設定</li></ol> | <ol><li>[開発の基本](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/developing/aem-as-a-cloud-service-sdk.html?lang=en#developing)</li><li>[デプロイメントのガイドライン](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/developing/development-guidelines.html?lang=en#developing)</li><li>[Experience Managerプロジェクト構造について](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/developing/aem-project-content-package-structure.html?lang=en#developing)</li><li>[コアコンポーネント](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html)</li><li>[Digital Foundation Blueprint](https://solutionpartners.adobe.com/content/dam/spp_assets/restricted/community/community_31/digital_foundation_best_practices_and_documentation.zip)</li><li>[スタイルシステム](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/sites/authoring/features/style-system.html?lang=en#authoring)</li><li>[オーバーレイ](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/developing/overlays.html?lang=en#developing)</li><li>[Cloud ServiceAPIリファレンスとしてのExperience Manager](https://docs.adobe.com/content/help/en/experience-manager-cloud-service-javadoc/)</li></ol> |

>[!TIP]
> [WKNDを開発し、ローカルExperience ManagerSDKにデプロイする方法に関するチュートリアルを参照](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-wknd-tutorial-develop/overview.html?lang=en)

### デプロイ

開発者はコードを作成しローカルでテストします。コードはその後、リモートの AEM as a Cloud Service 環境にプッシュされます。

Cloud Manager（Managed Services のオプションのコンテンツ配信ツール）が必要です。これが、AEM as a Cloud Service 環境にコードをデプロイするための唯一のメカニズムになりました。

Cloud Service環境としてAEMを設定およびデプロイする方法については、セルフヘルプのリソースを参照してください。

1. [CMパイプラインを設定](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/configure-pipeline.html?lang=en#using-cloud-manager)
   * 実稼働パイプライン
   * 非実稼動パイプラインとコード品質専用パイプライン
2. [コードの導入](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/deploy-code.html?lang=en#using-cloud-manager)
3. [テスト結果について](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/test-results/overview-test-results.html?lang=en#using-cloud-manager)
4. **ログへのアクセス**
   * [CM UIを使用](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/manage-logs.html?lang=en#using-cloud-manager)
   * [adobei/o cliを使用](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/debugging/debugging-aem-as-a-cloud-service/logs.html?lang=en#debugging)
5. [運用と保守](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/operations/home.html?lang=en)
   * [OSGI設定の設定](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/deploying/configuring-osgi.html?lang=en#deploying)
   * [バックアップと復元](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/operations/backup.html?lang=en)

>[!TIP]
> [WKNDをExperience Manager Cloud Serviceにデプロイする方法のチュートリアルを参照](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/develop-wknd-tutorial.html?lang=en)

### ヘルプとリソース

1. [デバッグのヒントとテクニック](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/debugging/debugging-aem-as-a-cloud-service/overview.html?lang=en#debugging-aem-as-a-cloud-service)
2. [開発者コンソール](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/debugging/debugging-aem-as-a-cloud-service/developer-console.html?lang=en#debugging)
3. [CRXDE Lite](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/debugging/debugging-aem-as-a-cloud-service/crxde-lite.html?lang=en#debugging) (ローカルSDKおよびExperience Managerクラウド開発環境でのみ使用可能)
4. [ログとログ](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/debugging/debugging-aem-as-a-cloud-service/logs.html?lang=en#debugging)
   * [CM Logs](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/debugging/debugging-aem-as-a-cloud-service/build-and-deployment.html?lang=en#debugging) (build-unit-testing、code-scanning、build-image、deploy)
   * [Experience Manager Cloud Serviceログ](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/debugging/debugging-aem-as-a-cloud-service/logs.html?lang=en#debugging) (aemerror、aemaccess、aemrequest、aemdispatcher、httpderror、httpaccess)
   * ローカルSDKログ（host:port/crx-quickstart/logs以下）

>[!NOTE]
> その他のヘルプについては、次の操作を行ってください。
>1. [Experience Managerサポートチームに連絡する](https://experienceleague.adobe.com/docs/customer-one/using/home.html?lang=en)
>2. [Experience Managerコミュニティとフォーラム](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-manager/ct-p/adobe-experience-manager-community)を探索


<br>

## Cloud Service{#move-to-cloud}としてAdobe Experience Managerに移動

**Cloud ServiceとしてのExperience Managerは、Experience Managerサイトやアセットの拡張性、安全性、機敏性の高いテクノロジー基盤を提供し、マーケティング担当者やIT部門は、規模の大きさで効果的なエクスペリエンスを提供することに集中できます。**

Experience ManagerをCloud Serviceとして使用すると、チームは製品のアップグレードを計画する代わりに、革新に専念できます。 新しい製品機能は徹底的にテストされ、中断することなくチームに提供されるので、常に最新のアプリケーションにアクセスできます。

Cloud Service への移行プロセスには、計画、実行、運用開始後の 3 つの段階が含まれています。移行をうまくスムーズにおこなうには、適切な計画を立て、本ガイドで概要を説明しているベストプラクティスに従う必要があります。

次の図は Cloud Service への推奨される移行プロセスを示しています。

![画像](/help/move-to-cloud-service/assets/home-img1.png)

<br>

### 計画

Cloud Serviceへのトランジションの遍歴を始める前に、Cloud ServiceとしてのExperience Managerについて理解し、行われた注目すべき変更を確認し、置き換えられた機能や非推奨の機能を確認する必要があります。

<table>
<tr>
<td>プロジェクトの検出と評価</td>
<td><ul><li>Cloud ServiceとしてのAdobe Experience ManagerとExperience Manager6.xとの重要な違いを理解するには、「Experience Managerに対する注目すべき変更」をCloud Service<a href="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/release-notes/aem-cloud-changes.html?lang=en">として参照してください。</a></li><li>非推奨とマークされた機能と機能の詳細については、<a href="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/release-notes/deprecated-removed-features.html?lang=en#deprecated-features">非推奨の機能</a>を参照してください。</li><li>[Cloud Serviceの移行のみ]Cloud Serviceの準備状況の評価：ソース環境で<a href="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/best-practices-analyzer/overview-best-practices-analyzer.html?lang=en#cloud-migration">ベストプラクティスアナライザー(BPA)</a>を実行 </li><li>Experience ManagerCSの主な変更点と廃止された機能に対する評価を完了します。</li></ul></td>
</tr>
<tr>
<td>レビュー</td>
<td><ul><li>発見に基づき、作業の見積もりとリソース・エクササイズを実行</li></ul></td>
</tr>
<tr>
<td>測定</td>
<td><ul><li><a href="https://experienceleague.adobe.com/welcome/aem/part6.html">プロジェクトKPI</a>、成功基準、プロジェクト日程の確立</li></ul></td>
</tr>
</table>

>[!NOTE]
>ベストプラクティスアナライザレポートは、AEMにCloud Serviceとしてトランジションするのに必要な時間とコストを予測するプロセスを高速化します。それ以外の場合は、手動で収集して評価する必要のある情報を提供します。


<br>

### 実行

プロジェクトの実行段階を開始する前に、Cloud Serviceに対して制限を設ける必要があります。 また、Cloud Managerについて理解しておく必要があります。 これは、プロジェクトコードをExperience Manager Cloud Serviceインスタンスに配置するメカニズムです。

Cloud Managerを使用すると、組織はクラウド内のExperience Managerを自己管理できます。 ITチームや導入パートナーがパフォーマンスやセキュリティを損なうことなくカスタマイズや更新の配信を迅速に行えるようにする、継続的な統合と継続的な配信([CI/CD](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/overview/ci-cd-pipeline.html?lang=en#overview))フレームワークが含まれます。

#### コンテンツの移行

1. [コンテンツ転送ツール](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/migration/content-transfer-tool.html?lang=en#migration) :既存のコンテンツをソースAEMインスタンス（オンプレミスまたはAMS）からターゲットAEMCloud Serviceインスタンスに移動するために使用します。
2. [Package Manager](https://experienceleague.adobe.com/docs/experience-manager-65/administering/contentmanagement/package-manager.html?lang=en#package-manager) :リポジトリの可変コンテンツのインポートおよびエクスポートに使用します。


#### リファクタリング/最適化

| はじめに | コードの確認とリファクタリング | ディスパッチャーの確認 |
|---|---|---|
| <ul><li>[ローカル開発の設定](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/local-development-environment-set-up/overview.html?lang=en#local-development-environment-set-up)</li><li>[ローカルディスパッチャーの設定](https://video.tv.adobe.com/v/30602/?captions=jpn)</li><li>[SDK API jarを使用してコードをコンパイルする](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/developing/aem-as-a-cloud-service-sdk.html?lang=en#developing)</li><li>[AEM開発のガイドラインの確認](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/developing/development-guidelines.html?lang=en#developing)<ul><li>バックグラウンドタスクと長時間実行ジョブ</li><li>Slingスケジューラー</li><li>入力ストリームの使用状況など</li></ul></li></ul> | <ul><li>ソース環境で[ベストプラクティスアナライザー(BPA)](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/best-practices-analyzer/overview-best-practices-analyzer.html?lang=en#cloud-migration)を実行します。[**移行のみ**]<ul><li>プロジェクト構造の考慮事項（[クラウドのアーキタイプ](https://github.com/adobe/aem-project-archetype)を基に）<ul><li>コードとコンテンツの分離（可変と不変）</li><li>[カスタムインデックス定義](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/operations/indexing.html?lang=en#indexing)</li><li>[カスタム実行モード](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/deploying/overview.html?lang=en#runmodes)</li></ul></li></ul></li><li>必要な変更を確認し、実行する</li><li>[ローカルSDKに](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-wknd-tutorial-develop/overview.html?lang=en) 展開する</li><li>AEM SDKを使用した煙のテストの実行</li></ul> | <ul><li>[ディスパッチャー設定](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/content-delivery/disp-overview.html?lang=en#local-validation-of-dispatcher-configuration)のリファクタリングを確認</li><li>必要に応じて、[Dispatcher Converter](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/refactoring-tools/dispatcher-transformation-utility-tools.html?lang=en#introduction-dispatcher)ツールを利用します。 [**移行のみ**]</li><li>テストは[ディスパッチャーSDK](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/local-development-environment-set-up/dispatcher-tools.html?lang=en#prerequisites)を使用して実行できます</li></ul> |

>[!TIP]
> アセット顧客：[アセットクラウドの移行](https://github.com/adobe/aem-cloud-migration)ツールを使用したアセットワークフローの確認とリファクタリング


#### 導入/実稼働開始

1. [Cloud ](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/managing-code/setup-cloud-manager-git-integration.html?lang=en#managing-code) Manageritへのデプロイ
2. [Cloud Manager品質パイプライン](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/how-to-use/understand-your-test-results.html?lang=en#how-to-use)を介してカスタマーコードを実行
3. [開発環境へのデプロイ](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/debugging/debugging-aem-as-a-cloud-service/build-and-deployment.html?lang=en#debugging)
4. [**移行**] のみパッケージまたは [コンテンツ転送ツール](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/using-content-transfer-tool.html?lang=en#cloud-migration(CTT)を使用したコンテンツの転送
5. 推奨されるテストサイクル（煙、QAなど）の実行
6. Cloud Manager実稼働パイプラインへの昇格
7. 煙の検証
8. 実稼働

<br>

### Post Go-Live

運用開始後段階では、一時ファイルの確実なクリーンアップ、継続的な開発に関するベストプラクティスの確認、ログの管理が必要です。

>[!TIP]
> Cloud Service環境としてAEMのトラブルシューティングに使用できるツール
>1. [開発者コンソール](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/developing/development-guidelines.html?lang=en#aem-as-a-cloud-service-development-tools)
>2. [CRX/DE Lite](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/debugging/debugging-aem-as-a-cloud-service/crxde-lite.html?lang=en#debugging)
>3. [ログの管理](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/manage-logs.html?lang=en#using-cloud-manager)


<br>

### ツールとリソース

| 評価 | リファクタリング | Experience Manager近代化 | コンテンツの移行 |
|------------|-------------|---------------------------------|-------------------|
| <ul><li>[ベストプラクティスアナライザ](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/best-practices-analyzer/overview-best-practices-analyzer.html?lang=en#cloud-migration)</li></li> | <ul><li>[Unified Experience Plugin](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/refactoring-tools/unified-experience.html?lang=en#refactoring-tools)</li></ul> | <ul><li>[静的テンプレートから編集可能テンプレートへ](https://opensource.adobe.com/aem-modernize-tools/pages/tools/page-structure.html)</li><li>[デザイン設定からポリシーへ](https://opensource.adobe.com/aem-modernize-tools/pages/tools/policy-importer.html) <li>[基盤コンポーネントからコアコンポーネントへ](https://opensource.adobe.com/aem-modernize-tools/pages/tools/component.html)</li><li>[クラシック UI からタッチ操作対応 UI へ](https://opensource.adobe.com/aem-modernize-tools/pages/tools/dialog.html)</li></ul> | <ul><li>[コンテンツ転送ツール](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/using-content-transfer-tool.html?lang=en#cloud-migration)</li><li>[Package Manager](https://experienceleague.adobe.com/docs/experience-manager-65/administering/contentmanagement/package-manager.html?lang=en#contentmanagement)</li></ul> |

>[!NOTE]
> その他のヘルプについては、次の操作を行ってください。
>1. [Experience Managerサポートチームに連絡する](https://experienceleague.adobe.com/docs/customer-one/using/home.html?lang=en)
>2. [Experience Managerコミュニティとフォーラム](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-manager/ct-p/adobe-experience-manager-community)を探索

