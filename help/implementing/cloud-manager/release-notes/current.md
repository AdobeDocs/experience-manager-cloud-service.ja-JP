---
title: Adobe Experience Manager as a Cloud Service の Cloud Manager 2023.9.0 のリリースノート
description: AEM as a Cloud Service の Cloud Manager 2023.9.0 のリリースノートです。
feature: Release Information
source-git-commit: dd52aef2f88cf64e8d9a32b1c8cafe4fcfbcb812
workflow-type: tm+mt
source-wordcount: '409'
ht-degree: 21%

---


# Adobe Experience Manager as a Cloud Service の Cloud Manager 2023.9.0 のリリースノート {#release-notes}

このページは、AEM as a Cloud Service の Cloud Manager リリース 2023.9.0 のリリースノートです。

>[!NOTE]
>
>詳しくは、 [このページ](/help/release-notes/release-notes-cloud/release-notes-current.md) (Adobe Experience Manager as a Cloud Serviceの最新のリリースノート )

## リリース日 {#release-date}

AEM as a Cloud Service の Cloud Manager 2023.9.0 のリリース日は 2023年9月7日（PT）です。次回のリリースは 2023年10月5日（PT）に予定されています。

## 新着情報 {#what-is-new}

このリリースではバグ修正に重点を置いています。

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

## バグ修正 {#bug-fixes}

* プログラムを削除すると、関連する実行中のパイプラインも削除され、パイプラインが失敗ステータスと誤って指定されないようにします。
* パイプラインの実行のすべてのステップが「完了」した場合、パイプラインのステータスが「実行中」と見なされ、停止状態になっているように見えることがあります。 「完了」と表示されます。
* コードジェネレーターアーキタイプを使用して生成されたリポジトリブランチの場合、CI/CD パイプラインは失敗します。
