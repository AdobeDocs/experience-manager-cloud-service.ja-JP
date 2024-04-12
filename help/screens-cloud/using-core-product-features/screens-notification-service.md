---
title: Screens as a Cloud Service の Screens 通知サービス
description: このページでは、Screens as a Cloud Service で通知サービスを設定する方法について説明します。
index: true
exl-id: 74215a70-45c8-4b7f-ba30-60c332de07e9
source-git-commit: 69798b1ac3758d37c4e2f480ccc23bae24d6a814
workflow-type: ht
source-wordcount: '200'
ht-degree: 100%

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

レポート時間を午前 5 時、ping タイムアウトを 1 時間に設定した場合、Screens デバイスが午前 4:00〜5:00 まで ping を送信しなければ、デバイスが無操作状態であることを確認するメール通知が届きます。
