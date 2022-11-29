---
title: Adobe Experience Manager as a Cloud Service の Cloud Manager 2022.12.0 のリリースノート
description: AEM as a Cloud Service の Cloud Manager 2022.12.0 のリリースノートです。
feature: Release Information
exl-id: 9c73d7ab-c2c2-4803-a07b-e9054220c6b2
source-git-commit: aa7f2175e2a43a318a6171e622d292ed3a8e958b
workflow-type: tm+mt
source-wordcount: '202'
ht-degree: 38%

---


# Adobe Experience Manager as a Cloud Service の Cloud Manager 2022.12.0 のリリースノート {#release-notes}

このページは、AEM as a Cloud Service の Cloud Manager 2022.12.0 のリリースノートです。

>[!NOTE]
>
>Adobe Experience Manager as a Cloud Service の最新のリリースノートについては、[このページ](/help/release-notes/release-notes-cloud/release-notes-current.md) を参照してください。

## リリース日 {#release-date}

AEM as a Cloud Serviceの Cloud Manager リリース2022.12.0のリリース日は 2022 年 11 月 29 日です。 次回のリリースは 2023 年 1 月 19 日に予定されています。

## 新機能 {#what-is-new}

* の通知 [AEMメンテナンスの更新](/help/overview/what-is-new-and-different.md#aem-updates) が Cloud Manager UI で表示されます。 この変更は、2022.12.0リリース後の数週間で段階的に実施される予定です。
* を使用してインジェストする場合 [コンテンツ転送ツール (CTT)](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/overview-content-transfer-tool.md) が進行中の場合、開発者コンソールと Cloud Manager の両方で環境ステータスが「 `Ingestion in Progress`.
* の可用性と信頼性の向上 [Cloud Manager のパイプライン](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md) 作成された

## バグの修正 {#bug-fixes}

* 防ぐために変更が加えられました [フロントエンドパイプライン](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md#front-end) 同じ環境でパイプライン実行が進行中の間に実行されるまで
* を防ぐために変更が加えられました `PATCH /program//environment//variables` を含む環境のリクエスト `FAILED` ステータス。
