---
title: Cloud Manager テストの概要
description: カスタムコードの品質を確保するために Cloud Manager が自動的に実行する 3 種類のテストの概要を説明します。
exl-id: 5f5c97b1-4180-4f49-af8b-257d4744766e
source-git-commit: 5ad33f0173afd68d8868b088ff5e20fc9f58ad5a
workflow-type: tm+mt
source-wordcount: '162'
ht-degree: 91%

---


# Cloud Manager テストの概要 {#overview}

Cloud Manager の Cloud Services パイプラインでサポートされるテストには、次の 3 つの大きなカテゴリがあります。

1. [コード品質テスト](/help/implementing/cloud-manager/code-quality-testing.md)

   * コード品質テストでは、アプリケーションコードの品質を評価します。
   * コード品質パイプラインは、実稼動環境および実稼動環境以外のすべてのパイプラインのビルド手順の直後に実行されます。
   * Cloud Manager で実行される[カスタムコード品質ルール](/help/implementing/cloud-manager/custom-code-quality-rules.md)は、AEM エンジニアリングチームのベストプラクティスに基づいて作成されます。

1. [機能テスト](/help/implementing/cloud-manager/functional-testing.md)

   * 機能テストは、[実稼動パイプライン](/help/implementing/cloud-manager/configuring-pipelines/configuring-production-pipelines.md)のテスト段階の一部ですが、オプションとして、[実稼動以外のパイプライン](/help/implementing/cloud-manager/configuring-pipelines/configuring-non-production-pipelines.md)のテスト段階に含めることもできます。

1. [エクスペリエンス監査テスト](/help/implementing/cloud-manager/experience-audit-testing.md)

   * エクスペリエンス監査テストは、すべての Cloud Manager 実稼動パイプラインで有効になっているので、スキップできません。

以下のテストがあります。

* 顧客が記述
* アドビが記述
* オープンソースツールで作成

>[!NOTE]
>
> 顧客が記述したテストも、アドビが記述したテストも、これらのテストを実行するためのコンテナ化されたインフラストラクチャで実行されます。
