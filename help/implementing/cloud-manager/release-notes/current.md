---
title: Adobe Experience Manager as a Cloud Service の Cloud Manager 2023.12.0 のリリースノート
description: AEM as a Cloud Service の Cloud Manager 2023.12.0 のリリースノートです。
feature: Release Information
exl-id: 9c73d7ab-c2c2-4803-a07b-e9054220c6b2
source-git-commit: 71ce915413cd968a78a33b7a52d02e09841e1707
workflow-type: tm+mt
source-wordcount: '787'
ht-degree: 17%

---


# Adobe Experience Manager as a Cloud Service の Cloud Manager 2023.12.0 のリリースノート {#release-notes}

このページは、AEM as a Cloud Service の Cloud Manager リリース 2023.12.0 のリリースノートです。

>[!NOTE]
>
>Adobe Experience Manager as a Cloud Service の最新のリリースノートについては、[こちらのページ](/help/release-notes/release-notes-cloud/release-notes-current.md)を参照してください。

## リリース日 {#release-date}

AEM as a Cloud Serviceの Cloud Manager リリース2023.12.0のリリース日は 2023 年 12 月 14 日です。 次回のリリースは 2024 年 1 月 18 日に予定されています。

## 新機能 {#what-is-new}

* [Cloud Manager のカスタム権限](/help/implementing/cloud-manager/custom-permissions.md) を使用すると、設定可能な権限を持つカスタム権限プロファイルを作成して、Cloud Manager ユーザーのプログラム、パイプライン、環境へのアクセスを制限できます。
   * この機能は、2024 年 2 月の Cloud Manager リリースで予想される完了に伴い、段階的に展開されます。
   * 次の宛先にメールを送信してください： `Grp-CloudManager-custom-permissions@adobe.com` をAdobe IDに関連付けた電子メールアドレスから送信します（早く有効にしたい場合）。
* コンテナの作成で、の Node.js バージョン 18 がサポートされるようになりました。 [フロントエンドパイプライン。](/help/implementing/developing/introduction/developing-with-front-end-pipelines.md)
* 新しく作成した Cloud Manager プログラムの場合、 [関連するNew Relicサブアカウント](/help/implementing/cloud-manager/user-access-new-relic.md) は、デフォルトでは有効になっていません。
   * New Relicサブアカウントが 90 日以上アクセスされていない既存のプログラムの場合、非アクティブ化されます。
   * New Relicサブアカウントを使用する場合は、Cloud Manager を介してオプトインする必要があります。
* java 8 および 11 のマイナーバージョンのロールアウトと maven の更新 [10 月の Cloud Manager リリースで発表および開始された](/help/implementing/cloud-manager/release-notes/2023/2023-10-0.md) が完了しました。
   * フロントエンドおよびフルスタックパイプラインに対して、Node 18 のサポートが追加されました。
   * Java 8 のマイナーバージョンがに更新されました。 `jdk1.8.0_371`.
   * Java 11 のマイナーバージョンがに更新されました。 `jdk-11.0.20`.
   * Maven がバージョン 3.8.8 に更新されました。
      * Maven でセキュリティで保護されていないすべてのを無効化 `http://*` デフォルトではミラーされます。
      * [Adobeが推奨](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/build-environment-details.md) ユーザーは、HTTP の代わりに HTTPS を使用するように Maven リポジトリを更新します。
   * ビルドコンテナのベースイメージが Ubuntu 22.04 に更新されました。

## 早期導入プログラム {#early-adoption}

将来の機能をテストする機会を得るには、Adobeの早期導入プログラムに参加してください。

### Real User Monitoring(RUM) を介したクライアント側の収集 {#rum}

次の条件を満たす場合に、 [Real User Monitoring(RUM) データ・サービス](/help/implementing/cloud-manager/content-requests.md#cliendside-collection) AEMas a Cloud Serviceのクライアント側のコレクションを有効にする

Real User Monitoring(RUM) データサービスは、ユーザーの操作をより正確に反映し、Web サイトのエンゲージメントを確実に測定できます。 これは、ページのパフォーマンスに関する高度なインサイトを得る絶好の機会です。 これは、Adobe管理 CDN と非Adobe管理 CDN のどちらを使用する場合にも便利です。 Adobeが管理していない CDN を使用するお客様は、自動トラフィックレポートを有効にできるようになったので、Adobeとトラフィックレポートを共有する必要がなくなりました。

この新機能のテストとフィードバックの共有に関心がある場合は、に電子メールを送信してください。 `aemcs-rum-adopter@adobe.com` Adobe IDに関連付けられた電子メールアドレスから。 実稼動、ステージ、開発環境のドメイン名を電子メールに含めてください。  この機能のアーリーアダプタープログラムの提供は制限されています。

### 独自の GitHub の導入 {#byo-github}

GitHub を使用してリポジトリを管理している場合は、[Cloud Manager を通じて GitHub リポジトリ内でコードを直接検証できるようになりました。](/help/implementing/cloud-manager/managing-code/byo-github.md)ここの統合により、コードを Adobe リポジトリと一貫して同期する必要がなくなり、プルリクエストをメインブランチに結合する前に検証できるようになります。

この新機能のテストとフィードバックの共有に関心がある場合は、に電子メールを送信してください。 `Grp-CloudManager_BYOG@adobe.com` Adobe IDに関連付けられた電子メールアドレスから。

### セルフ・サービス・コンテンツのリストア {#content-restore}

[新しいセルフ・サービス・コンテンツ・リストア機能](/help/operations/restore.md) は、最大 7 日間のバックアップ復元を提供し、次の機能を備えた評価用に早期導入者が利用できるようになりました。

* 過去 24 時間のポイント・イン・タイム・バックアップのリストア
* 最大 7 日間の固定時間の復元

この新機能のテストとフィードバックの共有に関心がある場合は、に電子メールを送信してください。 `aemcs-restorefrombackup-adopter@adobe.com` Adobe IDに関連付けられた電子メールから。

* アーリーアダプタープログラムは開発環境のみに限定されます。
* この機能のアーリーアダプタープログラムの提供は制限されています。
* この機能は、誤って削除されたコンテンツをリカバリするためのもので、災害復旧を目的としたものではありません。

### エクスペリエンス監査ダッシュボード {#experience-audit-dashboard}

[Cloud Manager Experience Audit ダッシュボード](/help/implementing/cloud-manager/experience-audit-dashboard.md) には、ページのパフォーマンススコアのトレンド表示と、改善に役立つインサイトおよびレコメンデーションが含まれています。 エクスペリエンス監査は、Cloud Manager 実稼動パイプラインのステップとして含まれます。

このダッシュボードは、Web アプリの品質を向上させるためのオープンソースの自動ツール、Google Lighthouse を使用しています。 Web ページ、パブリックページ、または認証を必要とするページに対して実行できます。 パフォーマンス、アクセシビリティ、プログレッシブ Web アプリ、SEO などに関する監査を実施しています。

新しいダッシュボードのテストと運用に興味がある場合は、 利用を開始するには、次の宛先に電子メールを送信します： `aem-lighthouse-pilot@adobe.com` Adobe IDに関連付けられた電子メールから。
