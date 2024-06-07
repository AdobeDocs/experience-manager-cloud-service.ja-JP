---
title: Adobe Experience Manager as a Cloud Service の Cloud Manager 2024.6.0 のリリースノート
description: AEM as a Cloud Service の Cloud Manager 2024.6.0 のリリースノートです。
feature: Release Information
exl-id: 9c73d7ab-c2c2-4803-a07b-e9054220c6b2
role: Admin
source-git-commit: 5644e6f433b18408780e13057ba469e7c4926f78
workflow-type: ht
source-wordcount: '702'
ht-degree: 100%

---


# Adobe Experience Manager as a Cloud Service の Cloud Manager 2024.6.0 のリリースノート {#release-notes}

このページは、AEM as a Cloud Service の Cloud Manager リリース 2024.6.0 のリリースノートです。

>[!NOTE]
>
>Adobe Experience Manager as a Cloud Service の最新のリリースノートについては、[こちらのページ](/help/release-notes/release-notes-cloud/release-notes-current.md)を参照してください。

## リリース日 {#release-date}

AEM as a Cloud Service の Cloud Manager 2024.6.0 のリリース日は 2024年6月6日（PT）です。次回のリリースは 2024年7月11日（PT）に予定されています。

## 新機能 {#what-is-new}

* フルスタックパイプラインとフロントエンドパイプラインの両方のソースとして、[独自の GitHub リポジトリを使用](/help/implementing/cloud-manager/managing-code/private-repositories.md)できるようになりました。
   * さらに、[Git サブモジュール](/help/implementing/cloud-manager/managing-code/git-submodules.md)を備えた GitHub リポジトリを活用すると、プルリクエストの検証に使用される自動生成パイプラインのコントロールが強化され、コードスキャンフェーズ中に重要な指標の動作を定義できます。
   * [また](/help/implementing/cloud-manager/managing-code/github-check-config.md)、ニーズに合わせて、GitHub にレポート履歴を保存し、パイプラインに名前を付け、パイプライン変数を設定することもできます。
* [セルフサービスコンテンツ復元](/help/operations/restore.md)では、最大 7 日間のバックアップ復元が可能で、次の機能があります。
   * 過去 24 時間のポイントインタイムバックアップの復元
   * 最長 7 日間の固定時間の復元
* [新しい OakPal ルール](/help/implementing/cloud-manager/custom-code-quality-rules.md#oakpal-ui-content-package)が、Cloud Manager コード品質スキャンに追加されました。
   * 2024年6月の時点で追加されたすべての新しいルールは、重大な変更ではありません。
   * Cloud Manager 2024年8月リリース以降、これらの新しいルールによりパイプラインでエラーが発生する可能性があるので、できるだけ早くこれらに対処することをお勧めします。

## 早期導入プログラム {#early-adoption}

将来の機能をテストする機会を得るには、Adobe の早期導入プログラムに参加してください。

### Cloud Manager での Edge Delivery Services のサポート {#edge-delivery-services}

Adobe Experience Manager Sites の一部として Edge Delivery Services のライセンスを取得している場合は、[Cloud Manager で Edge Delivery Services を使用してサイトを直接オンボード](/help/implementing/cloud-manager/edge-delivery-services.md)し、ガイド付きのセルフサービスエクスペリエンスを使用して運用開始できるようになりました。

これにより、すべての AEM プロパティに対して統一されたエクスペリエンスが実現し、ドメイン名管理、SSL 証明書管理、CDN マッピングなどのすべての重要なワークフローとの一貫性が確保されます。

この新機能をテストしてフィードバックを共有することに興味がある場合は、Adobe ID に関連付けられたメールアドレスから `aemcs-cmedgedelsvs-program-adopter@adobe.com` にメールを送信してください。

### ドメイン検証済み（DV）証明書

Cloud Manager では、[ドメイン検証（DV）SSL 証明書をセルフサービスで生成および管理できるようになりました。](/help/implementing/cloud-manager/managing-ssl-certifications/domain-validated-certificates.md)これにより、オンラインビジネス用の安全な web サイトを作成するための、最も高速かつ簡単でコスト効率に優れたソリューションが実現します。

この新機能をテストしてフィードバックを共有することに興味がある場合は、Adobe ID に関連付けられたメールアドレスから `Grp-aemcs-dv-dert-adopter@adobe.com` にメールを送信してください。

### 実ユーザーモニタリング（RUM）によるクライアントサイドのコレクション {#rum}

[実ユーザーモニタリング（RUM）データサービス](/help/implementing/cloud-manager/content-requests.md#cliendside-collection)を活用して、AEM as a Cloud Service のクライアントサイドのコレクションを有効にすることができます。

実ユーザーモニタリング（RUM）データサービスは、ユーザーインタラクションをより正確に反映し、web サイトのエンゲージメントの信頼性の高い測定を保証します。 ページのパフォーマンスに関する高度なインサイトを取得する絶好の機会です。 これは、アドビが管理する CDN やアドビ以外が管理する CDN を使用するお客様にとって有益です。 アドビ以外が管理する CDN を使用しているお客様は、自動トラフィックレポートを有効にできるようになり、トラフィックレポートをアドビと共有する必要がなくなります。

この新機能をテストしてフィードバックを共有することに興味がある場合は、Adobe ID に関連付けられたメールアドレスから `aemcs-rum-adopter@adobe.com` にメールを送信してください。 メールには実稼動環境、ステージ環境、開発環境のドメイン名を含めてください。  この機能の早期導入プログラムの使用は制限されています。

### エクスペリエンス監査ダッシュボード {#experience-audit-dashboard}

[Cloud Manager エクスペリエンス監査ダッシュボード](/help/implementing/cloud-manager/experience-audit-dashboard.md)には、ページのパフォーマンススコアのトレンド表示と、スコアの改善に役立つインサイトとレコメンデーションが含まれています。 エクスペリエンス監査は、Cloud Manager 実稼動パイプラインのステップとして含まれます。

このダッシュボードは、Web アプリの品質を向上させるためのオープンソースの自動ツールである Google Lighthouse を使用しています。 公開されている web ページや認証が必要な web ページに対して実行できます。 パフォーマンス、アクセシビリティ、プログレッシブ web アプリ、SEO などの監査が行われます。

新しいダッシュボードのテストに興味がありますか？ 開始するには、Adobe ID に関連付けられたメールアドレスから `aem-lighthouse-pilot@adobe.com` にメールを送信します。
