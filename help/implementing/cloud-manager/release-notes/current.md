---
title: Adobe Experience Manager as a Cloud Service の Cloud Manager 2024.6.0 のリリースノート
description: AEM as a Cloud Service の Cloud Manager 2024.6.0 のリリースノートです。
feature: Release Information
exl-id: 9c73d7ab-c2c2-4803-a07b-e9054220c6b2
role: Admin
source-git-commit: 5644e6f433b18408780e13057ba469e7c4926f78
workflow-type: tm+mt
source-wordcount: '702'
ht-degree: 52%

---


# Adobe Experience Manager as a Cloud Service の Cloud Manager 2024.6.0 のリリースノート {#release-notes}

このページは、AEM as a Cloud Service の Cloud Manager リリース 2024.6.0 のリリースノートです。

>[!NOTE]
>
>Adobe Experience Manager as a Cloud Service の最新のリリースノートについては、[こちらのページ](/help/release-notes/release-notes-cloud/release-notes-current.md)を参照してください。

## リリース日 {#release-date}

AEM as a Cloud Serviceの Cloud Manager リリース 2024.6.0 のリリース日は 2024 年 6 月 6 日（PT）です。 次回のリリースは 2024 年 7 月 11 日（PT）に予定されています。

## 新機能 {#what-is-new}

* これで、 [独自の GitHub リポジトリの使用](/help/implementing/cloud-manager/managing-code/private-repositories.md) フルスタックパイプラインとフロントエンドパイプラインの両方のソースとして。
   * さらに、で GitHub リポジトリを利用できます [git サブモジュール](/help/implementing/cloud-manager/managing-code/git-submodules.md) プルリクエストの検証に使用される自動生成パイプラインの制御を強化し、コードスキャン段階で重要な指標の動作を定義できるようになりました。
   * [また、次の選択肢があります](/help/implementing/cloud-manager/managing-code/github-check-config.md) github のレポート履歴を保持するには、パイプラインに名前を付け、必要に応じてパイプライン変数を設定します。
* [セルフサービスコンテンツ復元](/help/operations/restore.md) 最大 7 日間のバックアップ復元と機能を提供：
   * 過去 24 時間のポイントインタイムバックアップの復元
   * 最長 7 日間の固定時間の復元
* [新しい OakPal ルール](/help/implementing/cloud-manager/custom-code-quality-rules.md#oakpal-ui-content-package) が Cloud Manager のコード品質スキャンに追加されました。
   * 2024 年 6 月の時点で追加されたすべての新しいルールは、改行のない変更です。
   * これらの新しいルールは、Cloud Manager の 2024 年 8 月のリリース以降にパイプラインでエラーが発生する可能性があるので、できるだけ早くこれらの問題に対処することをお勧めします。

## 早期導入プログラム {#early-adoption}

将来の機能をテストする機会を得るには、Adobe の早期導入プログラムに参加してください。

### Cloud Manager でのEdge Delivery Servicesのサポート {#edge-delivery-services}

Adobe Experience Manager Sitesの一部としてEdge Delivery Servicesのライセンスを取得している場合、 [cloud Manager で直接Edge Delivery Servicesを使用してサイトをオンボーディングできるようになりました](/help/implementing/cloud-manager/edge-delivery-services.md) ガイド付きのセルフサービスエクスペリエンスを使用して運用を開始できます。

これにより、すべてのAEM プロパティでエクスペリエンスが統合され、ドメイン名の管理、SSL 証明書の管理、CDN マッピングなど、すべての重要なワークフローとの一貫性が確保されます。

この新機能のテストやフィードバックの共有に関心がある場合は、にメールを送信してください。 `aemcs-cmedgedelsvs-program-adopter@adobe.com` Adobe IDに関連付けられたメールアドレスから。

### ドメイン検証済み（DV）証明書

Cloud Manager で以下ができるようになりました。 [セルフサービスは、ドメイン検証（DV） SSL 証明書を生成および管理します。](/help/implementing/cloud-manager/managing-ssl-certifications/domain-validated-certificates.md) これにより、オンラインビジネスに安全な Web サイトを作成するための、最も迅速で簡単でコスト効率に優れたソリューションを提供します。

この新機能のテストやフィードバックの共有に関心がある場合は、にメールを送信してください。 `Grp-aemcs-dv-dert-adopter@adobe.com` Adobe IDに関連付けられたメールアドレスから。

### 実ユーザーモニタリング（RUM）によるクライアントサイドのコレクション {#rum}

[実ユーザーモニタリング（RUM）データサービス](/help/implementing/cloud-manager/content-requests.md#cliendside-collection)を活用して、AEM as a Cloud Service のクライアントサイドのコレクションを有効にすることができます。

実ユーザーモニタリング（RUM）データサービスは、ユーザーインタラクションをより正確に反映し、web サイトのエンゲージメントの信頼性の高い測定を保証します。 ページのパフォーマンスに関する高度なインサイトを取得する絶好の機会です。 これは、アドビが管理する CDN やアドビ以外が管理する CDN を使用するお客様にとって有益です。 アドビ以外が管理する CDN を使用しているお客様は、自動トラフィックレポートを有効にできるようになり、トラフィックレポートをアドビと共有する必要がなくなります。

この新機能をテストしてフィードバックを共有することに興味がある場合は、Adobe ID に関連付けられたメールアドレスから `aemcs-rum-adopter@adobe.com` にメールを送信してください。 メールには実稼動環境、ステージ環境、開発環境のドメイン名を含めてください。  この機能の早期導入プログラムの使用は制限されています。

### エクスペリエンス監査ダッシュボード {#experience-audit-dashboard}

[Cloud Manager エクスペリエンス監査ダッシュボード](/help/implementing/cloud-manager/experience-audit-dashboard.md)には、ページのパフォーマンススコアのトレンド表示と、スコアの改善に役立つインサイトとレコメンデーションが含まれています。 エクスペリエンス監査は、Cloud Manager 実稼動パイプラインのステップとして含まれます。

このダッシュボードは、Web アプリの品質を向上させるためのオープンソースの自動ツールである Google Lighthouse を使用しています。 公開されている web ページや認証が必要な web ページに対して実行できます。 パフォーマンス、アクセシビリティ、プログレッシブ web アプリ、SEO などの監査が行われます。

新しいダッシュボードのテストに興味がありますか？ 開始するには、Adobe ID に関連付けられたメールアドレスから `aem-lighthouse-pilot@adobe.com` にメールを送信します。
