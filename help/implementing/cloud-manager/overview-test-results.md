---
title: テスト結果の概要 —Cloud Services
description: テスト結果の概要 —Cloud Services
translation-type: tm+mt
source-git-commit: 25ba5798de175b71be442d909ee5c9c37dcf10d4
workflow-type: tm+mt
source-wordcount: '112'
ht-degree: 41%

---


# 概要 {#overview}

Cloud Services 用 Cloud Manager のパイプライン実行では、ステージ環境に対するテストの実行をサポートしています。これは、ビルドおよびユニットテストステップ中に実行されるテスト（オフラインで実行され、動作中の AEM 環境にはアクセスしない）とは対照的です。

Cloud ManagerのCloud Servicesパイプラインでサポートされるテストには、次の3つの大きなカテゴリがあります。

1. [コード品質テスト](/help/implementing/cloud-manager/code-quality-testing.md)
1. [機能テスト](/help/implementing/cloud-manager/functional-testing.md)
1. [コンテンツ監査テスト](/help/implementing/cloud-manager/content-audit-testing.md)

次のテストが可能です。

* お客様が書いた
* Adobeで書かれた
* オープンソースツール（GoogleのLighthouseで動作）

   >[!NOTE]
   > お客様が作成したテストとAdobeが作成したテストは、どちらも、これらのタイプのテストを実行するために設計されたコンテナ化されたインフラストラクチャで実行されます。

