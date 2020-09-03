---
title: テスト結果の概要 —Cloud Services
description: テスト結果の概要 —Cloud Services
translation-type: tm+mt
source-git-commit: d03ef0afe91760e35ef4e8fb3e3f2c833cbf945c
workflow-type: tm+mt
source-wordcount: '140'
ht-degree: 2%

---


# 概要 {#overview}

Cloud ManagerのCloud Servicesパイプラインでサポートされるテストには、次の3つの大きなカテゴリがあります。

1. [コード品質テスト](/help/implementing/cloud-manager/code-quality-testing.md)

   コード品質テストは、アプリケーションコードの品質を評価します。 コード品質パイプラインは、実稼働環境と実稼働環境以外のすべてのパイプラインのビルド手順の直後に実行されます。

   The [Custom Code Quality Rules](/help/implementing/cloud-manager/custom-code-quality-rules.md) executed by Cloud Manager are created based on best practices from AEM Engineering.

1. [機能テスト](/help/implementing/cloud-manager/functional-testing.md)

   機能テストは、実稼働パイプラインのステージテスト段階の一部です。

1. [エクスペリエンス監査テスト](/help/implementing/cloud-manager/experience-audit-testing.md)

   エクスペリエンスの監査テストは、すべてのCloud Manager実稼働パイプラインで有効になっているので、スキップできません。

次のテストが可能です。

* お客様が書いた
* Adobeで書かれた
* ソースツールを開く

   >[!NOTE]
   > お客様が作成したテストとAdobeが作成したテストは、どちらも、これらのタイプのテストを実行するために設計されたコンテナ化されたインフラストラクチャで実行されます。

