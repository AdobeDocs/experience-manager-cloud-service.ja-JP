---
title: Adobe Experience Manager as a Cloud Service の Cloud Manager 2023.1.0 のリリースノート
description: AEM as a Cloud Service の Cloud Manager 2024.1.0 のリリースノートです。
feature: Release Information
exl-id: 9c73d7ab-c2c2-4803-a07b-e9054220c6b2
source-git-commit: 26a2ed4ee613b77c192652ae9afa99d5a86f72ce
workflow-type: tm+mt
source-wordcount: '207'
ht-degree: 33%

---


# Adobe Experience Manager as a Cloud Service の Cloud Manager 2023.1.0 のリリースノート {#release-notes}

このページでは、AEM as a Cloud Serviceの Cloud Manager リリース 2023.1.0 のリリースノートについて説明します。

>[!NOTE]
>
>Adobe Experience Manager as a Cloud Service の最新のリリースノートについては、[このページ](/help/release-notes/release-notes-cloud/release-notes-current.md) を参照してください。

## リリース日 {#release-date}

AEM as a Cloud Serviceの Cloud Manager リリース 2023.1.0 のリリース日は 2023 年 1 月 19 日です。 次回のリリースは 2023年2月16日（PT）の予定です。

## 新機能 {#what-is-new}

* ユーザビリティの強化は、ユーザがアクションを実行できる場所とデフォルトのポインタとを区別するカーソルスタイルを更新することで行われました。

* 環境およびパイプライン実行のリストで、個々の行をクリックして詳細にアクセスできるようになりました。

* カスタム UI テストレポートは、Cloud Manager ストレージにコピーされ、Cloud Manager API 呼び出しを介してアクセスできるようになりました。

* ユーザーは、左向き矢印を使用して、GoLive ウィジェットの状態間を移行できるようになりました。

   ![GoLive ウィジェットの切り替え](assets/go-live-transitions.gif)

* セルフサービス [HIPAA 対応プログラムの作成](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/creating-production-programs.md) 対応する権限と権限が利用可能な場合に、が使用できるようになりました。

## バグの修正 {#bug-fixes}

* Cloud Manager では、2 つのパイプライン実行が（またはほぼ同時に）同時に開始されるのを防ぐので、パイプラインのエラーを回避できます。
