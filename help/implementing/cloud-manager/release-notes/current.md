---
title: Adobe Experience Manager as a Cloud Service の Cloud Manager 2024.8.0 のリリースノート
description: AEM as a Cloud ServiceのCloud Manager 2024.8.0 のリリースノートについて説明します。
feature: Release Information
role: Admin
source-git-commit: bf8bab5a195dde6cf15a2fd52e51d58c0215fdf3
workflow-type: tm+mt
source-wordcount: '465'
ht-degree: 31%

---


# Adobe Experience Manager as a Cloud ServiceのCloud Manager 2024.8.0 のリリースノート {#release-notes}

このページは、AEM as a Cloud Service の Cloud Manager リリース 2024.8.0 のリリースノートです。

>[!NOTE]
>
>Adobe Experience Manager as a Cloud Service の最新のリリースノートについては、[こちらのページ](/help/release-notes/release-notes-cloud/release-notes-current.md)を参照してください。

## リリース日 {#release-date}

AEM as a Cloud Service の Cloud Manager 2024.8.0 のリリース日は 2024年8月12日です。次回のリリースは 2024年9月14日（PT）に予定されています。

## 新機能 {#what-is-new}

* [ その他の公開地域 ](/help/operations/additional-publish-regions.md) および [99.99% SLA](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/creating-production-programs.md#sla) （サービスレベル契約）がAEM Formsのas a Cloud Service版で利用できるようになりました。
   * この機能強化により、稼働時間の増加および遅延の減少を伴う高い SLA を達成でき、世界中に分散しているユーザーに対してクラス最高のエクスペリエンスを提供できます。

## 早期導入プログラム {#early-adoption}

将来の機能をテストする機会を得るには、Adobe の早期導入プログラムに参加してください。

### Cloud ManagerでのEdge Delivery Servicesのサポート {#edge-delivery-services}

AEM Sitesの一部としてEdge Delivery Servicesのライセンスを取得している場合は、[Cloud Managerで直接Edge Delivery Servicesを使用してサイトをオンボーディングできるようになり ](/help/implementing/cloud-manager/edge-delivery-services.md)、ガイド付きのセルフサービスエクスペリエンスを使用して運用を開始できます。

この機能により、すべてのAEM プロパティで統一されたエクスペリエンスが提供されます。 ドメイン名の管理、SSL 証明書の管理、CDN マッピングなどの重要なワークフロー間で一貫性を確保できます。

この新機能をテストし、フィードバックを共有することに関心がある場合は、Adobe IDに関連付けられたメールアドレスから `aemcs-cmedgedelsvs-program-adopter@adobe.com` にメールを送信します。

### ドメイン検証済み（DV）証明書

Cloud Managerを使用すると、[ セルフサービス方式でドメイン検証済み（DV） SSL 証明書を生成および管理 ](/help/implementing/cloud-manager/managing-ssl-certifications/domain-validated-certificates.md) できるようになります。 この機能により、オンライン・ビジネス向けに安全な Web サイトを作成するための、最も迅速かつ容易でコスト・パフォーマンスに優れたソリューションが提供されます。

この新機能をテストし、フィードバックを提供したい場合は、Adobe IDにリンクされたメールアドレスを使用して `Grp-aemcs-dv-dert-adopter@adobe.com` にメールを送信します。

### エクスペリエンス監査ダッシュボード {#experience-audit-dashboard}

[Cloud Manager エクスペリエンス監査ダッシュボード](/help/implementing/cloud-manager/experience-audit-dashboard.md)には、ページのパフォーマンススコアのトレンド表示と、スコアの改善に役立つインサイトとレコメンデーションが含まれています。 エクスペリエンス監査は、Cloud Manager 実稼動パイプラインのステップとして含まれます。

このダッシュボードは、Web アプリの品質を向上させるためのオープンソースの自動ツールである Google Lighthouse を使用しています。 これを使用すると、公開か認証を必要とするかにかかわらず、任意の web ページを監査できます。 パフォーマンス、アクセシビリティ、プログレッシブ web アプリ、SEO などの評価を提供します。

新しいダッシュボードを試してみませんか？ まず、Adobe IDにリンクされたメールを使用して、`aem-lighthouse-pilot@adobe.com` にメールを送信します。

## バグ修正

* パイプラインが削除された後、パイプラインステップが実行中であることが判明するまれな問題を修正しました。
* 設定パイプラインで `FAILED` ステータスが誤って表示される問題が、まれに修正されました。
