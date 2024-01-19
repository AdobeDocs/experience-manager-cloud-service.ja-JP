---
title: Adobe Experience Manager as a Cloud Service の Cloud Manager 2024.1.0 のリリースノート
description: AEM as a Cloud Service の Cloud Manager 2024.1.0 のリリースノートです。
feature: Release Information
exl-id: 9c73d7ab-c2c2-4803-a07b-e9054220c6b2
source-git-commit: 06f534e6541bd04e005f3acf1edbb3e372c1cd0d
workflow-type: tm+mt
source-wordcount: '673'
ht-degree: 53%

---


# Adobe Experience Manager as a Cloud Service の Cloud Manager 2024.1.0 のリリースノート {#release-notes}

このページは、AEM as a Cloud Service の Cloud Manager リリース 2024.1.0 のリリースノートです。

>[!NOTE]
>
>Adobe Experience Manager as a Cloud Service の最新のリリースノートについては、[こちらのページ](/help/release-notes/release-notes-cloud/release-notes-current.md)を参照してください。

## リリース日 {#release-date}

AEM as a Cloud Serviceの Cloud Manager リリース 2024.1.0 のリリース日は 2024 年 1 月 18 日です。 次回のリリースは 2024 年 2 月 16 日に予定されています。

## 新機能 {#what-is-new}

* Cloud Manager で、メインのの有効期限だけでなく、有効期限も検証されるようになりました。 [証明書](/help/implementing/cloud-manager/managing-ssl-certifications/introduction.md) 中間証明書の場合も同様です。
* CDN [logs](/help/implementing/cloud-manager/manage-logs.md) が圧縮形式で返されるようになりました。

## 早期導入プログラム {#early-adoption}

将来の機能をテストする機会を得るには、Adobe の早期導入プログラムに参加してください。

### Real User Monitoring(RUM) を介したクライアント側の収集 {#rum}

次の条件を満たす場合に、 [Real User Monitoring(RUM) データ・サービス](/help/implementing/cloud-manager/content-requests.md#cliendside-collection) AEMas a Cloud Serviceのクライアント側のコレクションを有効にする

Real User Monitoring(RUM) データサービスは、ユーザーの操作をより正確に反映し、Web サイトのエンゲージメントを確実に測定できます。 これは、ページのパフォーマンスに関する高度なインサイトを得る絶好の機会です。 これは、Adobe管理 CDN と非Adobe管理 CDN のどちらを使用する場合にも便利です。 Adobeが管理していない CDN を使用するお客様は、自動トラフィックレポートを有効にできるようになったので、Adobeとトラフィックレポートを共有する必要がなくなりました。

この新機能のテストとフィードバックの共有に関心がある場合は、に電子メールを送信してください。 `aemcs-rum-adopter@adobe.com` Adobe IDに関連付けられた電子メールアドレスから。 実稼動、ステージ、開発環境のドメイン名を電子メールに含めてください。  この機能の早期導入プログラムの使用は制限されています。

### 独自の GitHub の導入 {#byo-github}

GitHub を使用してリポジトリを管理している場合は、[Cloud Manager を通じて GitHub リポジトリ内でコードを直接検証できるようになりました。](/help/implementing/cloud-manager/managing-code/byo-github.md)ここの統合により、コードを Adobe リポジトリと一貫して同期する必要がなくなり、プルリクエストをメインブランチに結合する前に検証できるようになります。

この新機能のテストとフィードバックの共有に関心がある場合は、に電子メールを送信してください。 `Grp-CloudManager_BYOG@adobe.com` Adobe IDに関連付けられた電子メールアドレスから。

### セルフサービスコンテンツの復元 {#content-restore}

[新しいセルフサービスコンテンツの復元機能](/help/operations/restore.md)では、最大 7 日間のバックアップ復元機能が提供され、早期導入者は次の機能を評価目的で使用できます。

* 過去 24 時間のポイントインタイムバックアップの復元
* 最長 7 日間の固定時間の復元

この新機能をテストしてフィードバックを共有することに興味がある場合は、Adobe ID に関連付けられたメールアドレスから `aemcs-restorefrombackup-adopter@adobe.com` にメールを送信してください。

* 早期導入プログラムは、開発環境のみに制限されています。
* この機能の早期導入プログラムの使用は制限されています。
* この機能は、誤って削除したコンテンツを回復するためのもので、障害回復を目的としたものではありません。

### エクスペリエンス監査ダッシュボード {#experience-audit-dashboard}

[Cloud Manager エクスペリエンス監査ダッシュボード](/help/implementing/cloud-manager/experience-audit-dashboard.md)には、ページのパフォーマンススコアのトレンド表示と、スコアの改善に役立つインサイトとレコメンデーションが含まれています。エクスペリエンス監査は、Cloud Manager 実稼動パイプラインのステップとして含まれます。

このダッシュボードは、Web アプリの品質を向上させるためのオープンソースの自動ツールである Google Lighthouse を使用しています。公開されている web ページや認証が必要な web ページに対して実行できます。パフォーマンス、アクセシビリティ、プログレッシブ web アプリ、SEO などの監査が行われます。

新しいダッシュボードのテストに興味がありますか？利用を開始するには、次の宛先に電子メールを送信します： `aem-lighthouse-pilot@adobe.com` Adobe IDに関連付けられた電子メールから。

## バグの修正 {#bug-fixes}

* 設定ファイルの場所が正しく設定されていない場合にエラーメッセージが表示され、ビルド手順で設定パイプラインが失敗するエラーが修正されました。 エラーメッセージが明確になり、設定ファイルの場所が正しいことをユーザーが確認する必要があることを示すようになりました。
* ビルドステップが「 」ステータスで終了したとき `FAILED` 原因は `BUILD_MAVEN_TRANSFER_ARTIFACT_ERROR`の場合、宛先ブランチとの結合の競合が原因でエラーとして適切に説明されるようになりました。
