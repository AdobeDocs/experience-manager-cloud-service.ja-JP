---
title: Adobe Experience Manager as a Cloud Service の Cloud Manager 2023.10.0 のリリースノート
description: AEM as a Cloud Service の Cloud Manager 2023.10.0 のリリースノートです。
feature: Release Information
exl-id: 9c73d7ab-c2c2-4803-a07b-e9054220c6b2
source-git-commit: b760b3a65d89b0b4f924379fc460015a58e2ed3e
workflow-type: tm+mt
source-wordcount: '521'
ht-degree: 19%

---


# Adobe Experience Manager as a Cloud Service の Cloud Manager 2023.10.0 のリリースノート {#release-notes}

このページは、AEM as a Cloud Service の Cloud Manager リリース 2023.10.0 のリリースノートです。

>[!NOTE]
>
>Adobe Experience Manager as a Cloud Service の最新のリリースノートについては、[こちらのページ](/help/release-notes/release-notes-cloud/release-notes-current.md)を参照してください。

## リリース日 {#release-date}

AEM as a Cloud Service の Cloud Manager リリース 2023.10.0 のリリース日は 2023年10月5日（PT）です。次回のリリースは 2023年11月2日（PT）に予定されています。

## 新機能 {#what-is-new}

* の改善点 [インデックス作成](/help/operations/indexing.md) は、新しいインデックスをデプロイする際のパイプライン期間を短縮しました。
   * 改善点は、コンテンツプロファイルによって異なります。
* 自動 [開発環境向けの更新](/help/implementing/cloud-manager/manage-environments.md#updating-environments) は、新しいプログラムに対してデフォルトで有効になっているので、更新を手動で実行する時間を節約できます。
   * この更新は段階的に展開されます。
* 2023 年 10 月の Cloud Manager リリースでは、段階的なロールアウトにより Java バージョンが更新されます。
   * Java 8 および 11 および Maven のマイナーバージョンが更新され、今後 2 ヶ月間で段階的に展開される予定です。 新しいバージョンには、複数のセキュリティ修正とバグ修正が含まれています。 新しいバージョンは次のとおりです。
   * *Maven: 3.8.8*
   * *Java 8 バージョン： /usr/lib/jvm/jdk1.8.0_371*
   * *Java 11 バージョン： /usr/lib/jvm/jdk-11.0.20*
   * [OpenJDK のアドバイザリを参照](https://openjdk.org/groups/vulnerability/advisories/) セキュリティおよびバグ修正の詳細については、これらの JDK の更新を参照してください。

## 早期採用プログラム {#early-adoption}

初期の採用プログラムに参加し、今後の機能をテストする機会を得ることができます。

### カスタム権限 {#custom-permissions}

[Cloud Manager のカスタム権限](/help/implementing/cloud-manager/custom-permissions.md) では、設定可能な権限を持つ新しいカスタム権限プロファイルを作成して、Cloud Manager ユーザーのプログラム、パイプライン、環境へのアクセスを制限できます。

この新機能のテストとフィードバックの共有に関心がある場合は、電子メールでお送りください `Grp-CloudManager-custom-permissions@adobe.com` Adobe IDに関連付けられた電子メールアドレスから。

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
