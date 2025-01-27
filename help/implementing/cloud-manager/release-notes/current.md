---
title: Adobe Experience Manager as a Cloud Service の Cloud Manager 2025.1.0 のリリースノート
description: AEM as a Cloud Service の Cloud Manager 2025.1.0 のリリースについて説明します。
feature: Release Information
role: Admin
exl-id: 24d9fc6f-462d-417b-a728-c18157b23bbe
source-git-commit: befb092169e2278a9e84c183d342003ef325c71e
workflow-type: tm+mt
source-wordcount: '841'
ht-degree: 9%

---

# Adobe Experience Manager as a Cloud Service の Cloud Manager 2025.1.0 のリリースノート {#release-notes}

<!-- https://wiki.corp.adobe.com/pages/viewpage.action?pageId=3389843928 -->

AEM（Adobe Experience Manager）as a Cloud Service の Cloud Manager 2025.1.0 のリリースについて説明します。

>[!NOTE]
>
>詳しくは、[Adobe Experience Manager as a Cloud Service の最新のリリースノート](/help/release-notes/release-notes-cloud/release-notes-current.md)を参照してください。

## リリース日 {#release-date}

AEM as a Cloud ServiceのCloud Manager 2025.1.0 のリリース日は 2025 年 1 月 22 日（水）です。

次回のリリース予定は 2025年2月13日（PT）です。


## 新機能 {#what-is-new}

* **コード品質ルール - SonarQube サーバーのアップグレード：** Cloud Manager コード品質ステップでは、2025 年 2 月 13 日（木）に予定されているCloud Manager 2025.2.0 リリースで SonarQube サーバー 9.9 の使用を開始します。

  準備のために、更新された SonarQube ルールが [ コード品質ルール ](/help/implementing/cloud-manager/code-quality-testing.md#understanding-code-quality-rules) で利用できるようになりました。

  次のパイプラインテキスト変数を設定して、新しいルールを「アーリーチェック」できます。

  `CM_BUILD_IMAGE_OVERRIDE` = `self-service-build:sonar-99-upgrade-java17or21`

  さらに、次の変数を設定して、コード品質ステップが同じコミットに対して実行されるようにします（通常、同じコ `commitId` ットに対してスキップされます）。

  `CM_DISABLE_BUILD_REUSE` = `true`

![ 変数設定ページ ](/help/implementing/cloud-manager/release-notes/assets/variables-config.png)

>[!NOTE]
>
>Adobeでは、メインの実稼動パイプラインと同じブランチに設定された新しい CI/CD コード品質パイプラインを作成することをお勧めします。 2025 年 2 月 13 日（PT）リリースより前に *適切な変数を設定し、新しく適用されたルールにブロッカーが導入されないことを検証します*。

* **Java 17 および Java 21 ビルドサポート：** お客様は、Java 17 または Java 21 を使用してビルドできるようになり、パフォーマンスの強化や新しい言語機能にアクセスできます。 Maven プロジェクトおよびライブラリのバージョンの更新など、設定手順については、[ ビルド環境 ](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/build-environment-details.md) を参照してください。 ビルドバージョンが Java 17 または Java 21 に設定されている場合、デプロイされるランタイムは Java 21 です。

   * **機能の有効化**
      * この機能は、2025 年 2 月 13 日木曜日（PT）に、新しい SonarQube バージョンのデフォルトのロールアウトと同時に、すべてのお客様に対して有効になります。
      * お客様は、上記の 2 つの変数設定を SonarQube 9.9 バージョンのアップグレードに対して設定することで *直ちに* 有効にできます。

   * **Java 21 ランタイムのデプロイメント**
      * Java 21 ランタイムは、Java 17 または Java 21 でビルドする場合にデプロイされます。
      * すべてのCloud Manager環境への段階的なロールアウトは 2 月にサンドボックスと開発環境で始まり、4 月に実稼動環境に拡張されます。
      * Java 11 を使用してビルドし、Java 21 ランタイム *以前* の導入を希望するお客様は、Adobe（[aemcs-java-adopter@adobe.com](mailto:aemcs-java-adopter@adobe.com) にお問い合わせください。

* **「CDN 設定」の名前が「ドメインマッピング」に変更されました：** AEM Cloud Managerのユーザーインターフェイスの改善の一環として、「CDN 設定」ラベルが「ドメインマッピング」に変更されました。 この変更により、用語と機能の連携が向上します。<!-- CMGR-64738 -->

  ![CDN 設定」の名前は、ユーザーインターフェイスで「ドメインマッピング」に変更されました ](/help/implementing/cloud-manager/release-notes/assets/domain-mappings.png)

* **ワンクリックでEdge Delivery サイトのプロビジョニング：** Cloud Managerで、適切な権限とライセンスを持つユーザーがワンクリックでサンプルEdge Delivery Servicesサイトを作成できるようになりました。 この合理化されたプロセスにより、次の自動機能が提供されます。

   * **GitHub 統合** – 既存の組織内に GitHub リポジトリを自動的に作成し、Edge Delivery Services用のボイラープレートテンプレートで事前設定します。
   * **AEM コード同期アプリのインストール** - AEM コード同期アプリケーションをリポジトリにインストールして、シームレスな同期とデプロイメントを確実に行います。
   * **コンテンツCollaborationの設定** - コンテンツを保存するための専用のGoogle ドライブフォルダーをリンクし、コンテンツ管理用のコラボレーション環境を提供します。
   * **コンテンツの公開** - プロビジョニングされたサイトのコンテンツをCloud Manager ユーザーインターフェイスから直接公開できるようになり、ワークフローが簡素化され、効率が向上しました。
   * **拡張Collaboration** – 複数の共同作業者をGoogle Drive コンテンツストレージフォルダーに追加して、チームワークとコンテンツの投稿を促進できます。

  これらの機能強化は、自動化の向上、設定プロセスの簡略化、Edge Delivery Servicesユーザーの共同作業の強化を目的としています。<!-- CMGR-59362 -->

  ![Edge Delivery サイトのプロビジョニング ](/help/implementing/cloud-manager/release-notes/assets/eds-one-click-60.png)

  ![Edge Delivery サイトをプロビジョニング ](/help/implementing/cloud-manager/release-notes/assets/eds-provision-60.png) ダイアログボックス

* **Edge Delivery Servicesサイトのサポートの強化：** Cloud Managerでは、最新のEdge Delivery Servicesサイトのオンボーディングをサポートするようになりました。 このアップデートには、CDN と配信スタックの包括的なリファクタリングが含まれており、堅牢性と保守性が向上しています。

* **早期導入プログラムの更新 – Bitbucket と GitLab の PR 検証のサポート：** Cloud Managerは、Bitbucket と GitLab のクラウドバージョンとセルフホストバージョンの両方で、プルリクエスト（PR）検証をサポートするようになりました。 この機能を使用すると、お客様は、PR を結合する前に、Adobeのコード品質しきい値に照らしてコードの変更をテストできます。 この機能強化により、マージ前のコード品質を高めることで、実稼動パイプラインでのコード変更の成功率が大幅に向上し、市場投入までの時間が短縮され、開発ワークフローが合理化されます。

「Bring Your Own Git」（現在は GitLab と Bitbucket がサポート）の詳細と、早期導入者として登録するには、[Cloud Manager 2024 年 10 月リリースノート ](/help/implementing/cloud-manager/release-notes/2024/2024-10-0.md##gitlab-bitbucket) を参照してください。

* **パイプラインの高度なフィルターオプション：** Cloud Managerには、パイプライン ページに高度なフィルターオプションが追加され、関連するデータにすばやくアクセスできるようになり、デプロイメントの効率が向上しました。 主な機能には、次のようなものがあります。

   * **多条件フィルタリング：** パイプライン名、環境、デプロイコードなどのフィルターを使用して、検索結果を絞り込みます。
   * **効率化されたパイプライン検索：** 特定のパイプラインを簡単に見つけることで、ナビゲーションの迅速化とワークフロー管理の向上を実現します。

  これらの機能強化により、パイプラインの管理とデプロイが全体的に効率的になり、使いやすくなります。

  ![ パイプラインフィルター機能 ](/help/implementing/cloud-manager/release-notes/assets/pipeline-filters.png)

* **Edge Delivery サービスのセルフサービス CDN 設定：** Edge Delivery サービスの新しい導入者は、Cloud Managerを通じて CDN を個別に設定できるようになりました。 この更新により、`.hlx.page/live` から新しい `.aem.page/live` へのサポートが拡張され、ユーザーに対する柔軟性が向上し、設定が合理化されます。


<!-- ## Early adoption program {#early-adoption}

Be a part of Cloud Manager's early adoption program and have a chance to test upcoming features. -->

<!-- ## Bug fixes -->




<!-- ## Known issues {#known-issues} -->
