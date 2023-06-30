---
title: Adobe Experience Manager as a Cloud Service の Cloud Manager 2023.7.0 のリリースノート
description: AEM as a Cloud Service の Cloud Manager 2023.7.0 のリリースノートです。
feature: Release Information
exl-id: 9c73d7ab-c2c2-4803-a07b-e9054220c6b2
source-git-commit: 1b46f763903a1b103837ed7e8cc498ad08ce64f1
workflow-type: tm+mt
source-wordcount: '237'
ht-degree: 29%

---


# Adobe Experience Manager as a Cloud Service の Cloud Manager 2023.7.0 のリリースノート {#release-notes}

このページは、AEM as a Cloud Service の Cloud Manager リリース 2023.7.0 のリリースノートです。

>[!NOTE]
>
>詳しくは、 [このページ](/help/release-notes/release-notes-cloud/release-notes-current.md) (Adobe Experience Manager as a Cloud Serviceの最新のリリースノート )

## リリース日 {#release-date}

AEM as a Cloud Serviceの Cloud Manager リリース 2023.7.0 のリリース日は 2023 年 6 月 29 日です。 次回のリリースは 2023年8月10日（PT）に予定されています。

## 新機能 {#what-is-new}

* Cloud Manager ランディングページのカードに、 [セキュリティの強化](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/creating-production-programs.md) は、プログラムで有効になっています。
* 開発の場合 [パイプライン](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md) にはテスト手順が含まれていないので、ユーザーは、テスト手順を含めるオプションが追加されました ( [パイプラインを開始します。](/help/implementing/cloud-manager/configuring-pipelines/managing-pipelines.md#running-pipelines)
   * これは段階的に展開されます。
* 条件 [実行のキャンセル](/help/implementing/cloud-manager/configuring-pipelines/managing-pipelines.md#view-details) パイプライン実行の承認ステップで、キャンセルの理由をユーザーに尋ねるようになりました。
   * これは段階的に展開されます。

## バグの修正 {#bug-fixes}

* Cloud Manager からオーサリング UI に移動しても、ログイン後に統合シェルにリダイレクトに失敗しなくなりました。
* go-live ウィジェットを使用した go-live 日の編集が、 **ライブにする** タブ **セキュリティの強化** タブをクリックします。
* コピー操作を開始すると、ユーザーは、コピー操作が既に呼び出されている環境を選択できなくなります。
