---
title: Adobe Experience Manager as a Cloud Service の Cloud Manager 2024.9.0 のリリースノート
description: AEM as a Cloud ServiceのCloud Manager 2024.9.0 のリリースノートについて説明します。
feature: Release Information
role: Admin
source-git-commit: cfaa3be31195929b80310610120a779a20537c61
workflow-type: tm+mt
source-wordcount: '332'
ht-degree: 22%

---

# Adobe Experience Manager as a Cloud Service の Cloud Manager 2024.9.0 のリリースノート {#release-notes}

このページは、AEM as a Cloud Service の Cloud Manager リリース 2024.9.0 のリリースノートです。

>[!NOTE]
>
>[Adobe Experience Manager as a Cloud Serviceの最新のリリースノート ](/help/release-notes/release-notes-cloud/release-notes-current.md) を参照してください。

## リリース日 {#release-date}

AEM as a Cloud Service の Cloud Manager 2024.9.0 のリリース日は 2024年9月5日です。次回のリリースは 2024年10月3日（PT）に予定されています。

## 新機能 {#what-is-new}

* **エクスペリエンス監査ダッシュボード：**

  Google Lighthouse を活用したAdobeのCloud Manager[enhanced Experience Audit Dashboard](/help/implementing/cloud-manager/experience-audit-dashboard.md) は、主要な web バイタル、SEO、アクセシビリティ指標を評価して、AEM Sitesの品質とパフォーマンスに関するインサイトを提供します。 実用的な推奨事項を提供することで、ユーザーが改善点を特定するのに役立ち、チームがユーザーエクスペリエンス、ページ読み込み時間、サイトコンプライアンスを強化できるようになります。 このダッシュボードにより、重要なサイト指標のモニタリングが合理化され、AEM アプリケーションが高いパフォーマンスとアクセシビリティの標準を満たすことができます。

* **Adobeが生成し、管理するドメイン検証証明書：**

  Cloud Managerを使用すると、[ セルフサービスAdobeで生成および管理される DV （Domain Validation） SSL 証明書 ](/help/implementing/cloud-manager/managing-ssl-certifications/add-ssl-certificate.md) を使用できるようになります。 この機能により、オンライン組織やビジネス向けに安全な web サイトを作成するための、最も迅速で簡単でコスト効率に優れたソリューションを実現できます。<!-- CMGR-52403 -->

* Cloud Managerでの **Edge Delivery Servicesのサポート：**

  AEM Sitesの一部としてEdge Delivery Services ライセンスをお持ちの場合 [Cloud Managerを通じて直接Edge Delivery Servicesでサイトをオンボーディングできるようになりました ](/help/implementing/cloud-manager/edge-delivery-services.md)。 この機能により、ガイド付きのセルフサービスの運用開始エクスペリエンスが可能になります。 また、すべてのAEM プロパティにわたってドメイン名の管理、SSL 証明書、CDN マッピングなどの基本的なワークフローを統合し、一貫性と効率性を確保します。<!-- CMGR-49859 -->

* GitHub リポジトリを使用するお客様は、web 階層設定パイプラインを作成および使用できるようになりました。<!--( KEEP IN? SP: YES CMGR-59046 and Slack https://cq-dev.slack.com/archives/C07LFP5BZ2L/p1725407057847379 ) -->

<!--
## Early adoption program {#early-adoption}

For a chance to test some upcoming features, be a part of Adobe's early adoption program. -->


## バグ修正

* SSL 証明書テーブル表示のページネーションが期待どおりに機能するようになりました。<!-- (CMGR-60804 - [UI] Pagination doesn't work for ssl certificates) -->
* 実行から「ビルドを昇格 **ボタンを使用すると、間違ったアーティファクトバージョンが昇格され** した。<!-- ( KEEP IN? SP: YES CMGR-59519 and Slack https://cq-dev.slack.com/archives/C07LFPN2R08/p1725408253474129 ) -->

<!-- * Slack message says next release? SP: REMOVE (Leave in for now) SSL Certificates table in Cloud Manager now enables pagination in the user experience. ( https://jira.corp.adobe.com/browse/CMGR-61041 and Slack https://cq-dev.slack.com/archives/C07LFRE9QJU/p1725408553760009 ) --<>
