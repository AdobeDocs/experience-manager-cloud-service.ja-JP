---
title: Cloud Manager テストの概要
description: カスタムコードの品質を確保するために Cloud Manager が自動的に実行する 3 種類のテストの概要を説明します。
exl-id: 5f5c97b1-4180-4f49-af8b-257d4744766e
source-git-commit: a9303c659730022b7417fc9082dedd26d7cbccca
workflow-type: tm+mt
source-wordcount: '154'
ht-degree: 9%

---


# Cloud Manager テストの概要 {#overview}

Cloud Manager では、テストパイプラインに対して 3 つのカテゴリのテストがサポートされています。Cloud Servicesパイプライン

1. [コード品質テスト](/help/implementing/cloud-manager/code-quality-testing.md)

   * コード品質テストでは、アプリケーションコードの品質を評価します。
   * コード品質パイプラインは、実稼動環境および実稼動環境以外のすべてのパイプラインのビルド手順の直後に実行されます。
   * この [カスタムコード品質ルール](/help/implementing/cloud-manager/custom-code-quality-rules.md) Cloud Manager で実行されるは、AEM Engineering のベストプラクティスに基づいて作成されます。

1. [機能テスト](/help/implementing/cloud-manager/functional-testing.md)

   * 機能テストは、実稼動パイプラインのステージテスト段階の一部です。

1. [エクスペリエンス監査テスト](/help/implementing/cloud-manager/experience-audit-testing.md)

   * エクスペリエンス監査テストは、すべての Cloud Manager 実稼動パイプラインで有効になっているので、スキップできません。

以下のテストがあります。

* 顧客が記述
* アドビが記述
* オープンソースツールで作成

>[!NOTE]
>
> お客様が作成したテストとAdobeが作成したテストの両方は、このようなテストを実行するために設計された、コンテナ化されたインフラストラクチャで実行されます。
