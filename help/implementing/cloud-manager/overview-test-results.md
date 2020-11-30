---
title: テスト結果の概要 - Cloud Services
description: テスト結果の概要 - Cloud Services
translation-type: tm+mt
source-git-commit: d03ef0afe91760e35ef4e8fb3e3f2c833cbf945c
workflow-type: tm+mt
source-wordcount: '140'
ht-degree: 100%

---


# 概要 {#overview}

Cloud Manager の Cloud Services パイプラインでサポートされるテストには、次の 3 つの大きなカテゴリがあります。

1. [コード品質テスト](/help/implementing/cloud-manager/code-quality-testing.md)

   コード品質テストでは、アプリケーションコードの品質を評価します。コード品質パイプラインは、実稼働環境および実稼働環境以外のすべてのパイプラインのビルド手順の直後に実行されます。

   Cloud Manager で実行される[カスタムコード品質ルール](/help/implementing/cloud-manager/custom-code-quality-rules.md)は、AEM エンジニアリングチームのベストプラクティスに基づいて作成されます。

1. [機能テスト](/help/implementing/cloud-manager/functional-testing.md)

   機能テストは、実稼働パイプラインのステージテスト段階の一部です。

1. [エクスペリエンス監査テスト](/help/implementing/cloud-manager/experience-audit-testing.md)

   エクスペリエンスの監査テストは、すべての Cloud Manager 実稼働パイプラインで有効になっているので、スキップできません。

以下のテストがあります。

* 顧客が記述
* アドビが記述
* ソースツールを開く

   >[!NOTE]
   > 顧客記述テストも、アドビ記述テストも、どちらのタイプのテストも、これらのテストを実行するためのコンテナ化されたインフラストラクチャで実行されます。

