---
title: Adobe Experience Manager as a Cloud Service の Cloud Manager 2022.6.0 のリリースノート
description: AEM as a Cloud Service の Cloud Manager 2022.6.0 のリリースノートです。
feature: Release Information
exl-id: 0a348836-74cd-4fd4-aef4-6ffbd6483c24
source-git-commit: 097c17b37cc308dc906cd4af7dc7c5d51862bdfa
workflow-type: tm+mt
source-wordcount: '348'
ht-degree: 52%

---

# Adobe Experience Manager as a Cloud Service の Cloud Manager 2022.6.0 のリリースノート {#release-notes}

このページは、AEM as a Cloud Service の Cloud Manager 2022.6.0 のリリースノートです。

>[!NOTE]
>
>Adobe Experience Manager as a Cloud Service の最新のリリースノートについては、[このページ](/help/release-notes/release-notes-cloud/release-notes-current.md) を参照してください。

## リリース日 {#release-date}

AEM as a Cloud Serviceの Cloud Manager リリース 2022.6.0 のリリース日は 2022 年 6 月 9 日です。 次回のリリースは2022年6月30日（PT）に予定されています。

## 新機能 {#what-is-new}

* Cloud Manager UI で、 [セルフサービスコンテンツの復元](/help/operations/backup.md) をAEMクラウド環境の正常な既知の状態に変更する。
   * この機能は、2022.06.0リリース以降の数週間にわたって段階的なアプローチで展開されます。
* Cloud Manager ランディングページの新しいウェルカムカードでは、テナントに関連するオンボーディングチュートリアルや進行状況指標にすばやくアクセスできます。
   * この機能は、2022.06.0 リリースの後、1 週間にわたって段階的アプローチで展開されます。
* 必要な権限を持つユーザーが新しい [ライセンスダッシュボード](/help/implementing/cloud-manager/license-dashboard.md) Cloud Manager ランディングページで、テナントが使用できる権利の詳細を表示できます。
   * AEM Sitesは、Cloud Manager ダッシュボードから可用性と使用状況の消費を提供する最初のソリューションです。
   * この機能は、2022.06.0リリース以降の数週間にわたって段階的なアプローチで展開されます。
* [New Relic サブアカウントおよびセルフサービスのユーザー管理](/help/implementing/cloud-manager/user-access-new-relic.md) は、Cloud Manager UI から使用できるようになりました。
   * この機能は、2022.06.0リリース以降の数週間にわたって段階的なアプローチで展開されます。
* Cloud Service制作プログラムのホームページ上にある新しい Go Live ウィジェットが、Go Live を成功に導くためのガイダンスを提供するようになりました。
* Git ミラーリングの使用時に、[ビルドアーティファクトを再利用できるようになりました](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/setting-up-project.md#build-artifact-reuse)。

## API の変更点 {#api-changes}

* [`List Programs`](https://developer.adobe.com/experience-cloud/cloud-manager/reference/api/#operation/getPrograms) API は非推奨（廃止予定）となりましたので、代わりに [`List Programs for Tenant`](https://developer.adobe.com/experience-cloud/cloud-manager/reference/api/#operation/getProgramsForTenant) を使用してください。
   * `List Programs` は引き続き機能しますが、この機能を使用すると、ログに警告メッセージが表示されます。
   * 3 か月後にはサポートされなくなります。
