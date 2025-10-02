---
title: Cloud Manager テストの概要
description: カスタムコードの品質を確保するためにCloud Managerが自動的に実行する 3 種類のテストの概要を説明します。
exl-id: 5f5c97b1-4180-4f49-af8b-257d4744766e
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
source-git-commit: ac918008c3f99d74e01be59c9841083abf3604aa
workflow-type: tm+mt
source-wordcount: '165'
ht-degree: 62%

---


# Cloud Manager テストの概要 {#overview}

Cloud Manager の Cloud Services パイプラインでサポートされるテストには、次の 3 つの大きなカテゴリがあります。

1. [コード品質テスト](/help/implementing/cloud-manager/code-quality-testing.md)

   * コード品質テストでは、アプリケーションコードの品質を評価します。
   * コード品質パイプラインは、実稼動環境および実稼動環境以外のすべてのパイプラインのビルド手順の直後に実行されます。
   * Cloud Manager で実行される[カスタムコード品質ルール](/help/implementing/cloud-manager/custom-code-quality-rules.md)は、AEM エンジニアリングチームのベストプラクティスに基づいて作成されます。

1. [機能テスト](/help/implementing/cloud-manager/functional-testing.md)

   * 機能テストは、[&#x200B; 実稼動パイプライン &#x200B;](/help/implementing/cloud-manager/configuring-pipelines/configuring-production-pipelines.md) のステージテスト段階で実行されます。 また、必要に応じて、（実稼動以外のパイプライン [&#x200B; のテスト段階で実行するこ &#x200B;](/help/implementing/cloud-manager/configuring-pipelines/configuring-non-production-pipelines.md) もできます。

1. [エクスペリエンス監査テスト](/help/implementing/cloud-manager/reports/report-experience-audit.md)

   * エクスペリエンスの監査テストは、すべてのCloud Manager実稼動パイプラインで有効になっており、スキップできません。

以下のテストがあります。

* 顧客が記述
* アドビが記述
* オープンソースツールで作成

>[!NOTE]
>
> 顧客が記述したテストも、アドビが記述したテストも、これらのテストを実行するためのコンテナ化されたインフラストラクチャで実行されます。
