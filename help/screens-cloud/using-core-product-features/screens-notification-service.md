---
title: Screens の Screens 通知サービス (as a Cloud Service)
description: ここでは、Screens で通知サービスを設定するas a Cloud Service方法について説明します。
index: true
exl-id: 74215a70-45c8-4b7f-ba30-60c332de07e9
source-git-commit: 69798b1ac3758d37c4e2f480ccc23bae24d6a814
workflow-type: tm+mt
source-wordcount: '200'
ht-degree: 5%

---

# Screens 通知サービス {#notification-service}

## はじめに {#introduction}

### 概要

AEM Screens通知サービスを使用すると、管理者は、E メールで設定可能な期間 ping を送信しなかったすべてのAEM Screensプレーヤーのリストを含むレポートを受け取ることができます。

### 設定方法

AEM Screens Cloud では、お客様は次の情報を含むサポートチケットを作成することで、デバイスの無操作状態に関するレポートをリクエストできます。

* 顧客名
* IMS OrgID
* スケジュールの頻度：このモニターが電子メールを送信する時間または頻度を時間単位（1 など）で指定します。
* ping タイムアウト：デバイスが到達不能と見なされるまでの時間を分単位で指定します。
* 電子メール ID ：レポートの送信先の電子メール ID

>[!NOTE]
>E メールの生成時に、指定された ping タイムアウトに対して ping が送信されていないデバイスの場合にのみ、E メールでプレーヤーがレポートされます。

### 使用例

レポート時間を午前 5 時、ping タイムアウトを 1 時間に設定した場合、Screens デバイスが午前 4 時～午前 5 時の間に ping を送信しなかった場合、デバイスが無操作状態であることを確認する電子メール通知が届きます。
