---
title: Adobe Experience Manager as a Cloud Serviceの Cloud Manager 2022.3.0 のリリースノート
description: AEM as a Cloud Serviceの Cloud Manager 2022.3.0 のリリースノートです。
feature: Release Information
exl-id: 9c73d7ab-c2c2-4803-a07b-e9054220c6b2
source-git-commit: 0749099acf98b09d0f83bfe86c2cc4558261c029
workflow-type: tm+mt
source-wordcount: '195'
ht-degree: 3%

---


# Adobe Experience Manager as a Cloud Serviceの Cloud Manager 2022.3.0 のリリースノート {#release-notes}

このページでは、AEM as a Cloud Serviceの Cloud Manager 2022.3.0 のリリースノートについて説明します。

>[!NOTE]
>
>参照： [このページ](/help/release-notes/release-notes-cloud/release-notes-current.md) (Adobe Experience Manager as a Cloud Serviceの最新のリリースノート )

## リリース日 {#release-date}

AEM as a Cloud Service 10 2022 年 3 月 10 日にリリースされた Cloud Manager リリース 2022.3.0 のリリース日です。 次回のリリースは 2022 年 4 月 7 日に予定されています。

## 新機能 {#what-is-new}

* AEM環境ログへのアクセスは、開発者ロールを使用しておこなうことができます。

## バグ修正 {#bug-fixes}

* 手動で作成した Git リポジトリのサブセットで、誤った名前の値が返され、ビルドアーティファクトの再利用機能が有効になりませんでした。 これらのリポジトリの名前は変更され、Cloud Manager API/UI で修正された名前がユーザーに表示されます。
* 実稼動以外のパイプラインからのビルドアーティファクトが、実稼動のフルスタックパイプラインで不適切に再利用されました。
* コード品質パイプラインを追加または編集する際に、指標の失敗を処理するためのオプションが表示されなくなりました。
* 予期しない一部のパイプライン変数設定がビルドステップで原因となる場合がありました。
