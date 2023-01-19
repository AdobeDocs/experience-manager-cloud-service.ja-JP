---
title: Adobe Experience Manager as a Cloud Service の Cloud Manager 2022.12.0 のリリースノート
description: AEM as a Cloud Service の Cloud Manager 2022.12.0 のリリースノートです。
feature: Release Information
source-git-commit: 5877f3c84ab6303520dd4697144e9b18d717b74f
workflow-type: tm+mt
source-wordcount: '202'
ht-degree: 48%

---


# Adobe Experience Manager as a Cloud Service の Cloud Manager 2022.12.0 のリリースノート {#release-notes}

このページは、AEM as a Cloud Service の Cloud Manager 2022.12.0 のリリースノートです。

>[!NOTE]
>
>Adobe Experience Manager as a Cloud Service の最新のリリースノートについては、[このページ](/help/release-notes/release-notes-cloud/release-notes-current.md) を参照してください。

## リリース日 {#release-date}

AEM as a Cloud Serviceの Cloud Manager リリース2022.12.0のリリース日は 2022 年 11 月 29 日です。 次回のリリースは 2023年1月19日（PT）の予定です。

## 新機能 {#what-is-new}

* の通知 [AEMメンテナンスの更新](/help/overview/what-is-new-and-different.md#aem-updates) が Cloud Manager UI で表示されます。 この変更は、2022.12.0リリース後の数週間で段階的に実施される予定です。
* を使用してインジェストする場合 [コンテンツ転送ツール (CTT)](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/overview-content-transfer-tool.md) が進行中の場合、開発者コンソールと Cloud Manager の両方で環境ステータスが「 `Ingestion in Progress`.
* [Cloud Manager パイプライン](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md)の可用性と信頼性が向上しました。

## バグの修正 {#bug-fixes}

* 防ぐために変更が加えられました [フロントエンドパイプライン](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md#front-end) 同じ環境でパイプライン実行が進行中の間に実行されるまで
* を防ぐために変更が加えられました `PATCH /program//environment//variables` を含む環境のリクエスト `FAILED` ステータス。
