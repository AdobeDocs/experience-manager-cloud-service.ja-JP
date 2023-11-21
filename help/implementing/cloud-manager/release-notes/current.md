---
title: Adobe Experience Manager as a Cloud Service の Cloud Manager 2023.11.0 のリリースノート
description: AEM as a Cloud Service の Cloud Manager 2023.11.0 のリリースノートです。
feature: Release Information
exl-id: 9c73d7ab-c2c2-4803-a07b-e9054220c6b2
source-git-commit: be38ca5bf79d401fc12c1422c270a2ee84bbbad2
workflow-type: tm+mt
source-wordcount: '735'
ht-degree: 25%

---


# Adobe Experience Manager as a Cloud Service の Cloud Manager 2023.11.0 のリリースノート {#release-notes}

このページは、AEM as a Cloud Service の Cloud Manager リリース 2023.11.0 のリリースノートです。

>[!NOTE]
>
>Adobe Experience Manager as a Cloud Service の最新のリリースノートについては、[こちらのページ](/help/release-notes/release-notes-cloud/release-notes-current.md)を参照してください。

## リリース日 {#release-date}

AEM as a Cloud Service の Cloud Manager 2023.11.0 のリリース日は 2023年11月14日（PT）です。次回のリリースは 2023年12月7日（PT）に予定されています。

## 新機能 {#what-is-new}

* Web アプリケーションファイアウォール — DDOS 保護 (WAF-DDOS) が、AEMのas a Cloud Serviceの使用権限と [は、セルフサービス方式で設定できます。](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/creating-production-programs.md)
* 特殊 [パイプラインの設定](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md) は、WAF ルールを含むトラフィックフィルタールールを数分以内に設定およびデプロイできるようになりました。
* [コンテンツをコピーする場合](/help/implementing/developing/tools/content-copy.md) 高度な環境から開発環境に移行すると、開発環境は容量が制限されるので、大きなコンテンツセットをコピーする際に注意が必要なメッセージが表示されるようになりました。
* [パイプライン実行の詳細ページ](/help/implementing/cloud-manager/configuring-pipelines/managing-pipelines.md#view-details) は、まだ開始されていないステップが灰色表示になっている、パイプライン実行のすべてのステップを表示します。
* 両方で **[アクティビティ](/help/implementing/cloud-manager/configuring-pipelines/managing-pipelines.md#activity)** および **[パイプライン](/help/implementing/cloud-manager/configuring-pipelines/managing-pipelines.md#pipelines)** 実行中ステータスのパイプラインを選択する際に、ページで、パイプライン実行の概要を使用できるようになりました。
* 新しい&#x200B;**期間**&#x200B;の節を[パイプラインの詳細ページ](/help/implementing/cloud-manager/configuring-pipelines/managing-pipelines.md#view-details)に追加しました。そのプログラムの過去のトレンドに基づいたパイプライン手順の平均期間が含まれます。
* 次の日： [パイプライン実行ページ](/help/implementing/cloud-manager/configuring-pipelines/managing-pipelines.md#activity-window) 完了したステップには、期間が表示されます。
* 実行数 [ビルドアーティファクトを再利用](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/setting-up-project.md#build-artifact-reuse) 次に、最初にこれらのアーティファクトを構築した実行へのリンクを表示します。
* 選択するオプション **重要な指標のエラー** 設定可能になりました。 [コード品質パイプライン](/help/implementing/cloud-manager/configuring-pipelines/configuring-non-production-pipelines.md) 同様に。


## 早期導入プログラム {#early-adoption}

将来の機能をテストする機会を得るには、Adobeの早期導入プログラムに参加してください。

### 独自の GitHub の導入 {#byo-github}

GitHub を使用してリポジトリを管理している場合は、[Cloud Manager を通じて GitHub リポジトリ内でコードを直接検証できるようになりました。](/help/implementing/cloud-manager/managing-code/byo-github.md)ここの統合により、コードを Adobe リポジトリと一貫して同期する必要がなくなり、プルリクエストをメインブランチに結合する前に検証できるようになります。

この新機能のテストとフィードバックの共有に関心がある場合は、に電子メールを送信してください。 `Grp-CloudManager_BYOG@adobe.com` Adobe IDに関連付けられた電子メールアドレスから。

### カスタム権限 {#custom-permissions}

[Cloud Manager のカスタム権限](/help/implementing/cloud-manager/custom-permissions.md) を使用すると、設定可能な権限を持つカスタム権限プロファイルを作成して、Cloud Manager ユーザーのプログラム、パイプライン、環境へのアクセスを制限できます。

この新機能のテストとフィードバックの共有に関心がある場合は、に電子メールを送信してください。 `Grp-CloudManager-custom-permissions@adobe.com` Adobe IDに関連付けられた電子メールアドレスから。

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

## 既知の問題 {#known-issues}

を防ぐ既知のバグがあります [パイプラインの設定](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md##config-deployment-pipeline) プッシュされて実稼動環境に移行する前に実行されます。

次の場合、 **実稼動にデプロイする前に一時停止します** 設定パイプラインにはオプションが必要です。バグが解決されるまで、次の回避策が推奨されます。

1. パイプラインを実行.
1. ステージング環境でコードをテストします。
1. デプロイと承認が使用可能になったら、「 **拒否**.
1. パイプラインを編集して、 **実稼動にデプロイする前に一時停止します** オプション。
1. パイプラインを再度実行して、ステージング時、その後実稼動時に再度実行できるようにします。
