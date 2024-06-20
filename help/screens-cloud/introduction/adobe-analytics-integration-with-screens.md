---
title: AEM Screens クラウドとの Adobe Analytics の統合
description: ここでは、標準で利用できる、AEM Screens と Adobe Analytics の統合について説明し、提供される再生検証機能についても紹介します。
contentOwner: trushton
content-type: reference
products: SG_EXPERIENCEMANAGER/Cloud/SCREENS
topic-tags: administering
docset: aem65
role: Admin, Developer
level: Intermediate
exl-id: e22242ce-e5ce-4486-bba4-e6a89ac4fb5e
feature: Screens Deployments
source-git-commit: 0e328d013f3c5b9b965010e4e410b6fda2de042e
workflow-type: tm+mt
source-wordcount: '408'
ht-degree: 100%

---

# AEM Screens クラウドとの Adobe Analytics の統合 {#adobe-analytics-integration-with-aem-screens}

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

AEM Screens ユーザーは、どのコンテンツが、いつ、どのくらいの時間（集計）表示されたかを把握したいと考えています。これは、サイネージソリューションの一般的な機能です。独自に分析を作成するのではなく、AEM Screens で Adobe Analytics を使用することにより、特定の場所に表示されるコンテンツと他のデータソースとの関連性を探るのに役立つユニークなクロスチャネル分析を実現できます。

次のアーキテクチャ図では、Adobe Analytics と AEM Screens の統合について説明しています。

![Adobe Analytics との統合](/help/screens-cloud/assets/analytics-architecture.png)

## AEM Screens Cloud での Adobe Analytics の有効化 {#enabling-adobe-analytics-in-aem-screens-cloud}

担当のアドビリレーションシップマネージャーに連絡して、Screens Cloud で Adobe Analytics を有効にしてもらってください。

## AEM Screens Cloud での Adobe Analytics サービスの使用 {#using-adobe-analytics-service-in-aem-screens}

このシナリオでは、ファームウェアや機器の Screens コアコンポーネントに実装されている Analytics サービスから REST 呼び出しを通じて Analytics API を呼び出して、特定の使用例に固有のイベントを明示的に作成および送信しつつ、カスタム開発したチャネルから任意のカスタムメッセージを Analytics に送信できる拡張性も備えています。

Analytics イベントは、IndexedDB にオフラインで保存され、後でまとめてクラウドに送信されます。

>[!NOTE]
>シーケンスとイベントの標準データモデルについて詳しくは、[Adobe Analytics for AEM Screens の設定](https://experienceleague.adobe.com/docs/experience-manager-screens/user-guide/administering/analytics-integration/configuring-adobe-analytics-aem-screens.html?lang=ja)を参照してください。
