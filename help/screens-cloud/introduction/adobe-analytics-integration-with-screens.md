---
title: Adobe AnalyticsとAEM Screens Cloud の統合
seo-title: Adobe Analytics Integration with AEM Screens
description: ここでは、標準で利用できる、AEM Screens と Adobe Analytics の統合について説明し、提供される再生検証機能についても紹介します。
seo-description: Follow this page to learn about out of the box integration of AEM Screens with Adobe Analytics and provides you with a proof of play.
uuid: 80d61af7-bf4d-46ca-a026-99a666c2e1a0
contentOwner: trushton
content-type: reference
products: SG_EXPERIENCEMANAGER/Cloud/SCREENS
topic-tags: administering
discoiquuid: b1a0e00e-0368-42c9-8bcd-5f00b4d0990c
docset: aem65
role: Admin, Developer
level: Intermediate
exl-id: e22242ce-e5ce-4486-bba4-e6a89ac4fb5e
source-git-commit: 75d147886c8151f8b8ac41af907e17b5deff5a9c
workflow-type: tm+mt
source-wordcount: '419'
ht-degree: 82%

---

# Adobe AnalyticsとAEM Screens Cloud の統合 {#adobe-analytics-integration-with-aem-screens}

ここでは、以下のトピックについて説明します。

* **概要**
* **アーキテクチャの詳細**

## 概要 {#overview}

***AEM Screens*** で Adobe Analytics を活用することにより、特定の場所に表示されるコンテンツと他のデータソースとの関連性を探るのに役立つユニークなクロスチャネル分析を実現できます。

AEM Screens は、標準で Adobe Analytics と統合されており、再生検証機能を提供します。

ここでは、AEM Screens プロジェクトと Adobe Analytics の連携に関係する以下の機能について説明します。

* デバイス別の再生検証レポートが可能
* アセット別の再生検証レポートが可能
* すべてのプレーヤーイベントをキャプチャしタイムスタンプを設定できる
* 再生がネットワークに接続されていない場合、すべてのプレーヤーイベントをローカルに保存できる
* フィードバックループを作成して再生イベントを経時的に追跡できる
* コンテンツ作成者が定義した成功条件に基づいてシステムがコンテンツやレイアウトを変更できる

Adobe Analytics と AEM Screens の統合により、*次の*&#x200B;目標を達成できます。

* デジタルサイネージの実装による ROI の実現
* 使用状況情報の収集と分析を将来可能にする基盤として Analytics を統合

## アーキテクチャの詳細 {#architectural-details}

AEM Screens ユーザーは、どのコンテンツが、いつ、どのくらいの時間（集計）表示されたかを把握したいと考えています。これは、サイネージソリューションの一般的な機能です。独自に分析を作成するのではなく、AEM Screens で Adobe Analytics を活用することにより、特定の場所に表示されるコンテンツと他のデータソースとの関連性を探るのに役立つユニークなクロスチャネル分析を実現できます。

次のアーキテクチャ図では、Adobe Analytics と AEM Screens の統合について説明しています。

![Adobe Analytics との統合](/help/screens-cloud/assets/analytics-architecture.png)

## AEM Screens Cloud でのAdobe Analyticsの有効化 {#enabling-adobe-analytics-in-aem-screens-cloud}

Screens Cloud でAdobe分析を有効にするには、Adobeのリレーションシップマネージャーにお問い合わせください。

## AEM Screens Cloud でのAdobe Analytics Service の使用 {#using-adobe-analytics-service-in-aem-screens}

このシナリオでは、ファームウェアや機器の Screens コアコンポーネントに実装されている Analytics サービスから REST 呼び出しを通じて Analytics API を呼び出して、特定の使用例に固有のイベントを明示的に作成および送信しつつ、カスタム開発したチャネルから任意のカスタムメッセージを Analytics に送信できる拡張性も備えています。

Analytics イベントは、IndexedDB にオフラインで保存され、後でまとめてクラウドに送信されます。

>[!NOTE]
>シーケンスとイベントの標準データモデルについて詳しくは、 [Adobe Analytics for AEM Screensの設定](https://experienceleague.adobe.com/docs/experience-manager-screens/user-guide/administering/analytics-integration/configuring-adobe-analytics-aem-screens.html) 」を参照してください。
