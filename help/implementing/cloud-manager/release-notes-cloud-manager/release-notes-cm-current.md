---
title: Adobe Experience Manager as a Cloud Serviceの Cloud Manager 2022.3.0 のリリースノート
description: AEM as a Cloud Serviceの Cloud Manager 2022.3.0 のリリースノートです。
feature: Release Information
exl-id: 9c73d7ab-c2c2-4803-a07b-e9054220c6b2
source-git-commit: 428bba062fcfb44ebfbbf3c1d05ce1a4634fb429
workflow-type: tm+mt
source-wordcount: '201'
ht-degree: 2%

---


# Adobe Experience Manager as a Cloud Serviceの Cloud Manager 2022.3.0 のリリースノート {#release-notes}

このページでは、AEM as a Cloud Serviceの Cloud Manager 2022.3.0 のリリースノートについて説明します。

>[!NOTE]
>
>参照： [このページ](/help/release-notes/release-notes-cloud/release-notes-current.md) (Adobe Experience Manager as a Cloud Serviceの最新のリリースノート )

## リリース日 {#release-date}

AEM as a Cloud Service 10 2022 年 3 月 10 日にリリースされた Cloud Manager リリース 2022.3.0 のリリース日です。 次回のリリースは 2022 年 4 月 7 日に予定されています。

## 新機能 {#what-is-new}

* ユーザーが **開発者** 役割は、AEM環境ログにアクセスできるようになりました。
* [この `reliability_rating` 重要指標](/help/implementing/cloud-manager/code-quality-testing.md) は無効になっています。
* ユーザーが **パイプライン** Cloud Manager のページを参照してください。

## バグ修正 {#bug-fixes}

* 手動で作成した Git リポジトリのサブセットで、間違った名前値が使用されていたので、影響を受けました [アーティファクトの再利用機能を構築します。](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/setting-up-project.md#build-artifact-reuse) これらのリポジトリの名前は変更され、Cloud Manager API/UI で修正された名前がユーザーに表示されます。
* [コード品質パイプラインを追加または編集する場合、](/help/implementing/cloud-manager/configuring-pipelines/configuring-non-production-pipelines.md) の **重要な指標の失敗の動作** オプションは表示されなくなりました。
* 予期しないパイプライン変数設定が、ビルドステップでエラーを引き起こさなくなりました。
