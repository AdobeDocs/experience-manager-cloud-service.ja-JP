---
title: Adobe Experience Manager as a Cloud Service の Cloud Manager 2024.4.0 のリリースノート
description: AEM as a Cloud Service の Cloud Manager 2024.4.0 のリリースノートです。
feature: Release Information
exl-id: 9c73d7ab-c2c2-4803-a07b-e9054220c6b2
source-git-commit: f1d8778f3cfb6868740141d008fd0217839e9103
workflow-type: ht
source-wordcount: '706'
ht-degree: 100%

---


# Adobe Experience Manager as a Cloud Service の Cloud Manager 2024.4.0 のリリースノート {#release-notes}

このページは、AEM as a Cloud Service の Cloud Manager リリース 2024.4.0 のリリースノートです。

>[!NOTE]
>
>Adobe Experience Manager as a Cloud Service の最新のリリースノートについては、[こちらのページ](/help/release-notes/release-notes-cloud/release-notes-current.md)を参照してください。

## リリース日 {#release-date}

AEM as a Cloud Service の Cloud Manager リリース 2024.4.0 のリリース日は 2024年4月10日（PT）です。次回のリリースは 2024年5月9日（PT）に予定されています。

## 新機能 {#what-is-new}

* [Edge Delivery](/help/edge/overview.md) web サイトの削除操作は、そのサイトに関連するプログラムからドメインマッピングを更新することで改善されました。
   * マッピングされる Sites がこれ以上ない場合、マッピングは削除されます。
* AEM インスタンスの重要な起動フェーズ中にリアルタイムのステータス更新を提供することで、デプロイメントのトラッキングが強化されました。
   * この機能により、デプロイメントの進行状況を完全に把握できるので、意思決定と運用効率が向上します。
* [ネットワークインフラストラクチャ](/help/security/configuring-advanced-networking.md)リストが強化され、地域ベースのフィルタリングを行わずに接続されたすべての環境を表示し、より包括的な表示を提供できるようになりました。
* コード構築の問題に関するエラーメッセージが強化され、根本的な原因と次に実行可能な手順の特定が容易になりました。

## 早期導入プログラム {#early-adoption}

将来の機能をテストする機会を得るには、Adobe の早期導入プログラムに参加してください。

### 実ユーザーモニタリング（RUM）によるクライアントサイドのコレクション {#rum}

[実ユーザーモニタリング（RUM）データサービス](/help/implementing/cloud-manager/content-requests.md#cliendside-collection)を活用して、AEM as a Cloud Service のクライアントサイドのコレクションを有効にすることができます。

実ユーザーモニタリング（RUM）データサービスは、ユーザーインタラクションをより正確に反映し、web サイトのエンゲージメントの信頼性の高い測定を保証します。 ページのパフォーマンスに関する高度なインサイトを取得する絶好の機会です。 これは、アドビが管理する CDN やアドビ以外が管理する CDN を使用するお客様にとって有益です。 アドビ以外が管理する CDN を使用しているお客様は、自動トラフィックレポートを有効にできるようになり、トラフィックレポートをアドビと共有する必要がなくなります。

この新機能をテストしてフィードバックを共有することに興味がある場合は、Adobe ID に関連付けられたメールアドレスから `aemcs-rum-adopter@adobe.com` にメールを送信してください。 メールには実稼動環境、ステージ環境、開発環境のドメイン名を含めてください。  この機能の早期導入プログラムの使用は制限されています。

### 独自の GitHub の導入 {#byo-github}

GitHub を使用してリポジトリを管理している場合は、[Cloud Manager を通じて GitHub リポジトリ内でコードを直接検証できるようになりました。](/help/implementing/cloud-manager/managing-code/byo-github.md)この統合により、コードを Adobe リポジトリと一貫して同期する必要がなくなり、プルリクエストをメインブランチに結合する前に検証できるようになります。この機能は、パブリック GitHub 専用です。自己ホスト型 GitHub のサポートは利用できません。

この新機能をテストしてフィードバックを共有することに興味がある場合は、Adobe ID に関連付けられたメールアドレスから `Grp-CloudManager_BYOG@adobe.com` にメールを送信します。

### セルフサービスコンテンツの復元 {#content-restore}

[新しいセルフサービスコンテンツの復元機能](/help/operations/restore.md)では、最大 7 日間のバックアップ復元機能が提供され、早期導入者は次の機能を評価目的で使用できます。

* 過去 24 時間のポイントインタイムバックアップの復元
* 最長 7 日間の固定時間の復元

この新機能をテストしてフィードバックを共有することに興味がある場合は、Adobe ID に関連付けられたメールアドレスから `aemcs-restorefrombackup-adopter@adobe.com` にメールを送信してください。

* 早期導入プログラムは、開発環境のみに制限されています。
* この機能の早期導入プログラムの使用は制限されています。
* この機能は、誤って削除したコンテンツを回復するためのもので、障害回復を目的としたものではありません。

### エクスペリエンス監査ダッシュボード {#experience-audit-dashboard}

[Cloud Manager エクスペリエンス監査ダッシュボード](/help/implementing/cloud-manager/experience-audit-dashboard.md)には、ページのパフォーマンススコアのトレンド表示と、スコアの改善に役立つインサイトとレコメンデーションが含まれています。 エクスペリエンス監査は、Cloud Manager 実稼動パイプラインのステップとして含まれます。

このダッシュボードは、Web アプリの品質を向上させるためのオープンソースの自動ツールである Google Lighthouse を使用しています。 公開されている web ページや認証が必要な web ページに対して実行できます。 パフォーマンス、アクセシビリティ、プログレッシブ web アプリ、SEO などの監査が行われます。

新しいダッシュボードのテストに興味がありますか？ 開始するには、Adobe ID に関連付けられたメールアドレスから `aem-lighthouse-pilot@adobe.com` にメールを送信します。

## バグの修正 {#bug-fixes}

* Cloud Manager が誤ったコミットハッシュでアーティファクトを再利用するバグを修正しました。
