---
title: Screens の Screens 通知サービス (as a Cloud Service)
description: ここでは、Screens で通知サービスを設定するas a Cloud Service方法について説明します。
index: true
source-git-commit: 81ce7954479366e40b47325577e1450f3d7a4c29
workflow-type: tm+mt
source-wordcount: '124'
ht-degree: 4%

---


# Screens 通知サービス {#notification-service}

## はじめに {#introduction}

### 概要

AEM Screens通知サービスを使用すると、AEM Screens Player が設定可能な期間 ping を送信しなかった場合、管理者は電子メールを受け取ることができます。

### 設定方法

AEM Screens Cloud では、お客様は、次の情報を含むサポートチケットを作成することで、デバイスの無操作状態に関するアラートをリクエストできます。

* 顧客名
* IMS OrgID
* スケジュールの頻度：このモニターが電子メールを送信する時間または頻度（時間単位、1 など）を指定します。
* ping タイムアウト：デバイスが到達不能と見なされるまでの時間を分単位で指定します。
* 電子メール ID ：レポートの送信先の電子メール ID