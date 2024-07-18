---
title: Adobe Experience Manager as a Cloud Service の Cloud Manager 2024.7.0 のリリースノート
description: AEM as a Cloud Service の Cloud Manager 2024.7.0 のリリースノートです。
feature: Release Information
exl-id: 9c73d7ab-c2c2-4803-a07b-e9054220c6b2
role: Admin
source-git-commit: a5cd55bcdc6044dd8db26f009b955216cda5daee
workflow-type: tm+mt
source-wordcount: '621'
ht-degree: 58%

---


# Adobe Experience Manager as a Cloud Service の Cloud Manager 2024.7.0 のリリースノート {#release-notes}

このページは、AEM as a Cloud Service の Cloud Manager リリース 2024.7.0 のリリースノートです。

>[!NOTE]
>
>Adobe Experience Manager as a Cloud Service の最新のリリースノートについては、[こちらのページ](/help/release-notes/release-notes-cloud/release-notes-current.md)を参照してください。

## リリース日 {#release-date}

AEM as a Cloud ServiceのCloud Manager リリース 2024.7.0 のリリース日は 2024 年 7 月 18 日（PT）です。 次回のリリースは 2024 年 8 月 8 日（PT）に予定されています。

## 新機能 {#what-is-new}

* コミット時にパイプラインを開始するための [ 実稼動パイプライン ](/help/implementing/cloud-manager/configuring-pipelines/configuring-production-pipelines.md#adding-production-pipeline) および [ 実稼動以外のパイプライン ](/help/implementing/cloud-manager/configuring-pipelines/configuring-non-production-pipelines.md#adding-non-production-pipeline)トリガー&#x200B;**Git の変更時** が [ プライベートリポジトリ ](/help/implementing/cloud-manager/managing-code/private-repositories.md) で使用できるようになりました。
   * これは、8 月中旬までに完了し、段階的にロールアウトされます。
* [Adobeが管理する DV 証明書を追加する場合 ](/help/implementing/cloud-manager/managing-ssl-certifications/domain-validated-certificates.md) ドメインごとに証明書を作成する代わりに、複数のドメインに対応する 1 つの証明書を追加できるようになりました。
* [ 追加の公開地域 ](/help/operations/additional-publish-regions.md) を持たないソリューションも、プログラムに Sites またはForms ソリューションが少なくとも 1 つ適用されている限り、プログラムに追加できるようになりました。
* [99.99% SLA](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/creating-production-programs.md#sla) を持たないソリューションでも、プログラムに少なくとも Sites またはForms ソリューションが適用されている限り、プログラムに追加できるようになりました。
* [ エクスペリエンス監査ダッシュボード ](/help/implementing/cloud-manager/experience-audit-dashboard.md) が様々な方法で強化されました。
   * 以前の `.net` アプローチに代わって、CDN を介して `.com` エンドポイントに対して監査が実行されるようになりました。
      * この変更により、実際のユーザーエクスペリエンスをより正確にシミュレートでき、web サイトの管理と最適化に関して、より十分な情報に基づいた意思決定を支援します。
   * エクスペリエンス監査 UI に対して、次のような複数の機能強化が行われました。
      * パフォーマンス、ベストプラクティス、SEO およびアクセシビリティのトレンド表示が追加されました。
      * Lighthouse の生のレポートリンクが、スキャンスナップショットの詳細パネルで直接、より直感的に表示されるようになりました。
      * Lighthouse のレコメンデーションセクションが強化されました。
   * Lighthouse バージョン 12.0.0 に従ってPWA指標が削除され、この指標が削除されました。

## 早期導入プログラム {#early-adoption}

将来の機能をテストする機会を得るには、Adobe の早期導入プログラムに参加してください。

### Cloud Manager での Edge Delivery Services のサポート {#edge-delivery-services}

Adobe Experience Manager Sites の一部として Edge Delivery Services のライセンスを取得している場合は、[Cloud Manager で Edge Delivery Services を使用してサイトを直接オンボード](/help/implementing/cloud-manager/edge-delivery-services.md)し、ガイド付きのセルフサービスエクスペリエンスを使用して運用開始できるようになりました。

これにより、すべての AEM プロパティに対して統一されたエクスペリエンスが実現し、ドメイン名管理、SSL 証明書管理、CDN マッピングなどのすべての重要なワークフローとの一貫性が確保されます。

この新機能をテストしてフィードバックを共有することに興味がある場合は、Adobe ID に関連付けられたメールアドレスから `aemcs-cmedgedelsvs-program-adopter@adobe.com` にメールを送信してください。

### ドメイン検証済み（DV）証明書

Cloud Manager では、[ドメイン検証（DV）SSL 証明書をセルフサービスで生成および管理できるようになりました。](/help/implementing/cloud-manager/managing-ssl-certifications/domain-validated-certificates.md)これにより、オンラインビジネス用の安全な web サイトを作成するための、最も高速かつ簡単でコスト効率に優れたソリューションが実現します。

この新機能をテストしてフィードバックを共有することに興味がある場合は、Adobe ID に関連付けられたメールアドレスから `Grp-aemcs-dv-dert-adopter@adobe.com` にメールを送信してください。

### エクスペリエンス監査ダッシュボード {#experience-audit-dashboard}

[Cloud Manager エクスペリエンス監査ダッシュボード](/help/implementing/cloud-manager/experience-audit-dashboard.md)には、ページのパフォーマンススコアのトレンド表示と、スコアの改善に役立つインサイトとレコメンデーションが含まれています。 エクスペリエンス監査は、Cloud Manager 実稼動パイプラインのステップとして含まれます。

このダッシュボードは、Web アプリの品質を向上させるためのオープンソースの自動ツールである Google Lighthouse を使用しています。 公開されている web ページや認証が必要な web ページに対して実行できます。 パフォーマンス、アクセシビリティ、プログレッシブ web アプリ、SEO などの監査が行われます。

新しいダッシュボードのテストに興味がありますか？ 開始するには、Adobe ID に関連付けられたメールアドレスから `aem-lighthouse-pilot@adobe.com` にメールを送信します。
