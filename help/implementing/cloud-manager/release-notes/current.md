---
title: Adobe Experience Manager as a Cloud Service の Cloud Manager 2024.1.0 のリリースノート
description: AEM as a Cloud Service の Cloud Manager 2024.1.0 のリリースノートです。
feature: Release Information
exl-id: 9c73d7ab-c2c2-4803-a07b-e9054220c6b2
source-git-commit: b81c2bd5c339bce97fe5774572bf1532fc8e04df
workflow-type: ht
source-wordcount: '687'
ht-degree: 100%

---


# Adobe Experience Manager as a Cloud Service の Cloud Manager 2024.1.0 のリリースノート {#release-notes}

このページは、AEM as a Cloud Service の Cloud Manager リリース 2024.1.0 のリリースノートです。

>[!NOTE]
>
>Adobe Experience Manager as a Cloud Service の最新のリリースノートについては、[こちらのページ](/help/release-notes/release-notes-cloud/release-notes-current.md)を参照してください。

## リリース日 {#release-date}

AEM as a Cloud Service の Cloud Manager 2024.1.0 のリリース日は 2024年1月18日（PT）です。 次回のリリースは 2024年2月16日（PT）の予定です。

## 新機能 {#what-is-new}

* Cloud Manager は、メイン[証明書](/help/implementing/cloud-manager/managing-ssl-certifications/introduction.md)だけでなく中間証明書の有効期限も検証するようになりました。
* CDN [ログ](/help/implementing/cloud-manager/manage-logs.md)は、圧縮形式で返されるようになりました。

## 早期導入プログラム {#early-adoption}

将来の機能をテストする機会を得るには、Adobe の早期導入プログラムに参加してください。

### 実ユーザーモニタリング（RUM）によるクライアントサイドのコレクション {#rum}

[実ユーザーモニタリング（RUM）データサービス](/help/implementing/cloud-manager/content-requests.md#cliendside-collection)を活用して、AEM as a Cloud Service のクライアントサイドのコレクションを有効にすることができます。

実ユーザーモニタリング（RUM）データサービスは、ユーザーインタラクションをより正確に反映し、web サイトのエンゲージメントの信頼性の高い測定を保証します。 ページのパフォーマンスに関する高度なインサイトを取得する絶好の機会です。 これは、アドビが管理する CDN やアドビ以外が管理する CDN を使用するお客様にとって有益です。 アドビ以外が管理する CDN を使用しているお客様は、自動トラフィックレポートを有効にできるようになり、トラフィックレポートをアドビと共有する必要がなくなります。

この新機能をテストしてフィードバックを共有することに興味がある場合は、Adobe ID に関連付けられたメールアドレスから `aemcs-rum-adopter@adobe.com` にメールを送信してください。 メールには実稼動環境、ステージ環境、開発環境のドメイン名を含めてください。  この機能の早期導入プログラムの使用は制限されています。

### 独自の GitHub の導入 {#byo-github}

GitHub を使用してリポジトリを管理している場合は、[Cloud Manager を通じて GitHub リポジトリ内でコードを直接検証できるようになりました。](/help/implementing/cloud-manager/managing-code/byo-github.md)この統合により、コードを Adobe リポジトリと一貫して同期する必要がなくなり、プルリクエストをメインブランチに結合する前に検証できるようになります。 この機能は、パブリック GitHub 専用です。 自己ホスト型 GitHub のサポートは利用できません。

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

* 設定ファイルの場所が適切に設定されていない場合、設定パイプラインがビルドステップで失敗し、不明瞭なエラーメッセージが表示されるエラーが修正されました。 エラーメッセージが明確になり、設定ファイルの場所が正しいことをユーザーが確認する必要があることが示されるようになりました。
* `BUILD_MAVEN_TRANSFER_ARTIFACT_ERROR` によりビルドステップが `FAILED` ステータスで終了した場合、宛先分岐との結合の競合によるエラーとして、適切に記述されるようになりました。
