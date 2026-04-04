---
title: Screens as a Cloud Service の Screens 通知サービス
description: このページでは、Screens as a Cloud Service で通知サービスを設定する方法について説明します。
index: true
exl-id: 74215a70-45c8-4b7f-ba30-60c332de07e9
feature: Developing Screens
role: Admin, Developer, User
source-git-commit: 81f85045212ca6fd92f2b665aeceaa0d4b92318c
workflow-type: tm+mt
source-wordcount: '202'
ht-degree: 81%

---

# Screens 通知サービス {#notification-service}

## はじめに {#introduction}

### 概要

AEM Screens 通知サービスを使用すると、管理者は、設定可能な期間に ping を送信しなかったすべての AEM Screens プレーヤーのリストを含むレポートをメールで受け取ることができます。

### 設定方法

AEM Screens クラウドでは、お客様は、次の情報を含むサポートチケットを作成することで、デバイスの無操作状態に関するレポートをリクエストできます。

* 顧客名
* IMS OrgID
* スケジュールの頻度：このモニターがメールを送信する時刻または頻度（例：1）を指定します。
* ping タイムアウト：デバイスが到達不能と見なされるまでの経過時間を分単位で指定します。
* メール ID ：レポートの送信先のメール ID

>[!NOTE]
>メールの生成時にデバイスが指定された ping タイムアウトに達しなかった場合にのみ、メールでプレーヤーがレポートされます。

### ユースケース例

レポート時間を午前5時、ping タイムアウトを1時間に設定した場合、Screens デバイスが午前4:00 ～ 5:00時の間にpingを送信しない場合は、デバイスが非アクティブであることを確認するメール通知が届きます。
