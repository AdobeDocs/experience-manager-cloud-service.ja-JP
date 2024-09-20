---
title: Adobe Experience Manager as a Cloud Service の Cloud Manager 2024.9.0 のリリースノート
description: AEM as a Cloud Service の Cloud Manager 2024.9.0 のリリースノートについて説明します。
feature: Release Information
role: Admin
exl-id: 24d9fc6f-462d-417b-a728-c18157b23bbe
source-git-commit: b222b4384b1c2a21ecbb244d149ce7e51cc7990f
workflow-type: ht
source-wordcount: '367'
ht-degree: 100%

---

# Adobe Experience Manager as a Cloud Service の Cloud Manager 2024.9.0 のリリースノート {#release-notes}

このページは、AEM as a Cloud Service の Cloud Manager リリース 2024.9.0 のリリースノートです。

>[!NOTE]
>
>詳しくは、[Adobe Experience Manager as a Cloud Service の最新のリリースノート](/help/release-notes/release-notes-cloud/release-notes-current.md)を参照してください。

## リリース日 {#release-date}

AEM as a Cloud Service の Cloud Manager 2024.9.0 のリリース日は 2024年9月5日です。次回のリリースは 2024年10月3日（PT）に予定されています。

## 新機能 {#what-is-new}

* **エクスペリエンス監査ダッシュボード：**

  Adobe Cloud Manager の[強化されたエクスペリエンス監査ダッシュボード](/help/implementing/cloud-manager/experience-audit-dashboard.md)では、Google Lighthouse を活用し、コア web バイタル、SEO、アクセシビリティ指標を評価することで、AEM Sites の品質とパフォーマンスに関するインサイトを提供します。実用的な推奨事項を提供することで、ユーザーが改善すべき領域を特定するのに役立ち、チームがユーザーエクスペリエンス、ページ読み込み時間、サイトコンプライアンスを強化できます。このダッシュボードにより、重要なサイト指標のモニタリングが簡素化され、AEM アプリケーションが高いパフォーマンスとアクセシビリティの標準を満たすことができます。

* **アドビが生成および管理する、ドメイン検証証明書：**

  Cloud Manager では、[アドビが生成および管理する 、DV（ドメイン検証）SSL 証明書をセルフサービスで利用](/help/implementing/cloud-manager/managing-ssl-certifications/add-ssl-certificate.md)できるようになりました。この機能により、オンライン組織またはビジネス用の安全な web サイトを作成するのに最も高速かつ簡単でコスト効率に優れたソリューションが実現します。<!-- CMGR-52403 -->

  >[!NOTE]
  >
  >[コンテンツハブ](/help/assets/product-overview.md)のお客様には、段階的なロールアウトの一環として、フェーズ単位でこの機能が提供される予定です。

* **Cloud Manager での Edge Delivery Services のサポート：**

  AEM Sites の一部として Edge Delivery Services のライセンスをお持ちの場合は、[Cloud Manager で Edge Delivery Services を使用してサイトを直接オンボードできるようになりました](/help/implementing/cloud-manager/edge-delivery/introduction-to-edge-delivery-services.md)。この機能により、ガイド付きのセルフサービスの運用開始エクスペリエンスが可能になります。また、すべての AEM プロパティにわたってドメイン名の管理、SSL 証明書、CDN マッピングなどの基本的なワークフローを統合し、一貫性と効率性を確保します。<!-- CMGR-49859 -->

  >[!NOTE]
  >
  >[コンテンツハブ](/help/assets/product-overview.md)のお客様には、段階的なロールアウトの一環として、フェーズ単位でこの機能が提供される予定です。

* GitHub リポジトリを使用するお客様は、web 階層設定パイプラインを作成および使用できるようになりました。<!--( KEEP IN? SP: YES CMGR-59046 and Slack https://cq-dev.slack.com/archives/C07LFP5BZ2L/p1725407057847379 ) -->

<!--
## Early adoption program {#early-adoption}

For a chance to test some upcoming features, be a part of Adobe's early adoption program. -->


## バグ修正

* SSL 証明書テーブル表示のページネーションが期待どおりに機能するようになりました。<!-- (CMGR-60804 - [UI] Pagination doesn't work for ssl certificates) -->
* 実行から「**ビルドを昇格**」ボタンを使用した際に、間違ったアーティファクトバージョンが昇格されました。<!-- ( KEEP IN? SP: YES CMGR-59519 and Slack https://cq-dev.slack.com/archives/C07LFPN2R08/p1725408253474129 ) -->

<!-- * Slack message says next release? SP: REMOVE (Leave in for now) SSL Certificates table in Cloud Manager now enables pagination in the user experience. ( https://jira.corp.adobe.com/browse/CMGR-61041 and Slack https://cq-dev.slack.com/archives/C07LFRE9QJU/p1725408553760009 ) --<>
