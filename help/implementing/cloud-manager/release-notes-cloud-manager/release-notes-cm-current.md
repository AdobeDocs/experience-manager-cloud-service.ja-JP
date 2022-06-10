---
title: Adobe Experience Manager as a Cloud Service の Cloud Manager 2022.6.0 のリリースノート
description: AEM as a Cloud Service の Cloud Manager 2022.6.0 のリリースノートです。
feature: Release Information
exl-id: 9c73d7ab-c2c2-4803-a07b-e9054220c6b2
source-git-commit: 1a6ca2647cc185ed0cb60fa75d2f5752e72f5715
workflow-type: tm+mt
source-wordcount: '348'
ht-degree: 24%

---


# Adobe Experience Manager as a Cloud Service の Cloud Manager 2022.6.0 のリリースノート {#release-notes}

このページは、AEM as a Cloud Service の Cloud Manager 2022.6.0 のリリースノートです。

>[!NOTE]
>
>Adobe Experience Manager as a Cloud Service の最新のリリースノートについては、[このページ](/help/release-notes/release-notes-cloud/release-notes-current.md) を参照してください。

## リリース日 {#release-date}

AEM as a Cloud Serviceの Cloud Manager リリース 2022.6.0 のリリース日は 2022 年 6 月 9 日です。 次回のリリースは 2022 年 6 月 30 日（PT）に予定されています。

## 新機能 {#what-is-new}

* Cloud Manager UI で、 [セルフサービスコンテンツの復元](/help/operations/backup.md) をAEMクラウド環境の正常な既知の状態に変更する。
   * この機能は、2022.06.0リリース以降の数週間にわたって段階的なアプローチで展開されます。
* Cloud Manager ランディングページの新しいウェルカムカードでは、テナントに関連するオンボーディングチュートリアルや進行状況指標にすばやくアクセスできます。
   * この機能は、2022.06.0リリース以降の週にわたって段階的なアプローチで展開されます。
* 必要な権限を持つユーザーが新しい [ライセンスダッシュボード](/help/implementing/cloud-manager/license-dashboard.md) Cloud Manager ランディングページで、テナントが使用できる権利の詳細を表示できます。
   * AEM Sitesは、Cloud Manager ダッシュボードから可用性と使用状況の消費を提供する最初のソリューションです。
   * この機能は、2022.06.0リリース以降の数週間にわたって段階的なアプローチで展開されます。
* [New Relic サブアカウントおよびセルフサービスのユーザー管理](/help/implementing/cloud-manager/user-access-new-relic.md) は、Cloud Manager UI から使用できるようになりました。
   * この機能は、2022.06.0リリース以降の数週間にわたって段階的なアプローチで展開されます。
* Cloud Service制作プログラムのホームページ上にある新しい Go Live ウィジェットが、Go Live を成功に導くためのガイダンスを提供するようになりました。
* [ビルドアーティファクトを再利用できるようになりました](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/setting-up-project.md#build-artifact-reuse) git ミラーリングを使用する場合。

## API の変更点 {#api-changes}

* この [`List Programs`](https://developer.adobe.com/experience-cloud/cloud-manager/reference/api/#operation/getPrograms) API は廃止され、 [`List Programs for Tenant`](https://developer.adobe.com/experience-cloud/cloud-manager/reference/api/#operation/getProgramsForTenant) 代わりにを使用する必要があります。
   * `List Programs` は引き続き機能しますが、この機能を使用すると、ログに警告メッセージが表示されます。
   * 3 ヶ月後はサポートされなくなります。

