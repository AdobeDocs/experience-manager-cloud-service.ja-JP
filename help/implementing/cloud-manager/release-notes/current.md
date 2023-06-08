---
title: Adobe Experience Manager as a Cloud Service の Cloud Manager 2023.6.0 のリリースノート
description: AEM as a Cloud Service の Cloud Manager 2023.6.0 のリリースノートです。
feature: Release Information
exl-id: 9c73d7ab-c2c2-4803-a07b-e9054220c6b2
source-git-commit: 80a5f58119dc304161d324491cd65c50e981ccd4
workflow-type: tm+mt
source-wordcount: '210'
ht-degree: 37%

---


# Adobe Experience Manager as a Cloud Service の Cloud Manager 2023.6.0 のリリースノート {#release-notes}

このページは、AEM as a Cloud Service の Cloud Manager リリース 2023.6.0 のリリースノートです。

>[!NOTE]
>
>Adobe Experience Manager as a Cloud Service の最新のリリースノートについては、[このページ](/help/release-notes/release-notes-cloud/release-notes-current.md) を参照してください。

## リリース日 {#release-date}

AEM as a Cloud Serviceの Cloud Manager リリース 2023.6.0 のリリース日は 2023 年 6 月 8 日です。 次回のリリースは 2023 年 7 月 7 日に予定されています。

## 新機能 {#what-is-new}

* 新しい [プログラムまたは環境](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/program-types.md) この名前は、英数字のみを使用でき、特殊文字の制限を受けるようになりました。
* を再開する際 [実稼動パイプライン](/help/implementing/cloud-manager/configuring-pipelines/configuring-production-pipelines.md) 承認ステップに確認ダイアログが表示されるようになりました。
* の **[顧客機能テスト](/help/implementing/cloud-manager/functional-testing.md#custom-functional-testing)** および **[カスタム UI テスト](/help/implementing/cloud-manager/ui-testing.md)** パイプラインステップ、新しい `INCOMPLETE` ステータスが可能になりました。これは、そのようなテストが存在せず、したがって実行されなかったことを示します。
   * その場合、パイプラインは失敗せず、次のステップに進みます。

## バグの修正 {#bug-fixes}

* この [web 層設定パイプライン](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md#web-tier-config-pipelines) は、Assets のみのプログラムに対して誤って有効になっていません。
* 環境のプロビジョニング中に特定の種類のエラーが発生しないように、より堅牢な検証が追加されました。
