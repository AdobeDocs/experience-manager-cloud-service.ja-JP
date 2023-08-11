---
title: Adobe Experience Manager as a Cloud Service の Cloud Manager 2023.8.0 のリリースノート
description: AEM as a Cloud Service の Cloud Manager 2023.8.0 のリリースノートです。
feature: Release Information
exl-id: 9c73d7ab-c2c2-4803-a07b-e9054220c6b2
source-git-commit: 99772a1a3faa454a9b07dd92c9e7622ddb37ce2d
workflow-type: tm+mt
source-wordcount: '540'
ht-degree: 21%

---


# Adobe Experience Manager as a Cloud Service の Cloud Manager 2023.8.0 のリリースノート {#release-notes}

このページは、AEM as a Cloud Service の Cloud Manager リリース 2023.8.0 のリリースノートです。

>[!NOTE]
>
>詳しくは、 [このページ](/help/release-notes/release-notes-cloud/release-notes-current.md) (Adobe Experience Manager as a Cloud Serviceの最新のリリースノート )

## リリース日 {#release-date}

AEM as a Cloud Service の Cloud Manager 2023.8.0 のリリース日は 2023年8月10日（PT）です。次回のリリースは 2023年7月9日（PT）に予定されています。

## 新機能 {#what-is-new}

* コンテンツセットを [コンテンツをコピー](/help/implementing/developing/tools/content-copy.md) [コンテキスト対応の設定](/help/implementing/developing/introduction/configurations.md) が UI のコンテンツセットで許可されるようになりました。
* Cloud Manager UI でのエラーメッセージの理解しやすく表示を改善するための機能強化がおこなわれました。

## 早期採用プログラム {#early-adoption}

初期の採用プログラムに参加し、今後の機能をテストする機会を得ることができます。

### セルフ・サービス・コンテンツのリストア {#content-restore}

[新しいセルフ・サービス・コンテンツ・リストア機能](/help/operations/restore.md) は、最大 7 日間のバックアップ復元を提供し、次の機能を備えた評価用に早期導入者が利用できるようになりました。

* 過去 24 時間のポイント・イン・タイム・バックアップのリストア
* 最大 7 日間の固定時間の復元

この新機能のテストとフィードバックの共有に関心がある場合は、に電子メールを送信してください。 `aemcs-restorefrombackup-adopter@adobe.com` Adobe IDに関連付けられた電子メールから。 注：

* アーリーアダプタープログラムは開発環境のみに限定されます。
* この機能のアーリーアダプタープログラムの提供は制限されています。
* この機能は、誤って削除されたコンテンツをリカバリするためのもので、災害復旧を目的としたものではありません。

### エクスペリエンス監査ダッシュボード {#experience-audit-dashboard}

[Cloud Manager Experience Audit ダッシュボード](/help/implementing/cloud-manager/experience-audit-dashboard.md) には、ページのパフォーマンススコアのトレンド表示と、改善に役立つインサイトおよびレコメンデーションが含まれています。 エクスペリエンス監査は、Cloud Manager 実稼動パイプラインのステップとして含まれます。

このダッシュボードでは、Web アプリの品質を向上させるためのオープンソースの自動ツールであるGoogle Lighthouse を利用します。 これは、任意の Web ページに対して実行できます。公開または認証が必要です。 パフォーマンス、アクセシビリティ、プログレッシブ Web アプリ、SEO などに関する監査を実施しています。

新しいダッシュボードのテストと運用に興味がある場合は、 次の宛先にメールを送信してください： `aem-lighthouse-pilot@adobe.com` Adobe IDに関連付けられたメールから、すぐに使い始めることができます。

## バグの修正 {#bug-fixes}

* The **環境** トリガー後にメニューが閉じるようになりました **[コンテンツをコピー](/help/implementing/developing/tools/content-copy.md)** モーダルです。
* [パイプラインの再実行](/help/implementing/cloud-manager/deploy-code.md#reexecute-deployment) は、以前の実行に `commitId` ビルドフェーズの状態に設定します。
* ユーザーが **アクティビティ** または **パイプライン** スクリーン。
* The `contentSetName` の値がログになくなり、の開始時に入力で提供されるようになりました。 [コンテンツコピー](/help/implementing/developing/tools/content-copy.md) 操作。
* まれな状況で、同じパイプラインから 2 回の実行を開始して「停止」状態になると、実行できなくなりました。
* 証明書の有効期限が切れると、証明書に関連付けられているドメイン名と IP 許可リストは CDN から削除されなくなります。
   * このような場合でも、サイトには引き続きアクセスできます。
   * [](/help/implementing/cloud-manager/managing-ssl-certifications/introduction.md)Cloud Manager UI には、SSL 証明書の有効期限が近づいていることを示す事前警告がよりわかりやすく表示されます。
* Sites が Assets 専用プログラムのソリューションとして追加された場合に、AEMが公開エンドポイントへのアクセスを失う問題が修正されました。
