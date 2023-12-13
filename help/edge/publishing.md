---
title: Edge Delivery Services用コンテンツの公開
description: コンテンツの公開がEdge Delivery Servicesと連携する仕組みと、AEMコンテンツをEdge Delivery Servicesと共に公開する方法について説明します。
feature: Edge Delivery Services
source-git-commit: f6e1c5de57ee0297abdf6b03faf550a266dfac32
workflow-type: tm+mt
source-wordcount: '201'
ht-degree: 0%

---


# Edge Delivery Services用コンテンツの公開 {#publishing-edge}

Edge Delivery Servicesを使用すれば、コンテンツソースに関係なく、コンテンツの公開がシームレスに行われます。

* ドキュメントベースのコンテンツ — 詳しくは、 [セクションを公開](https://www.aem.live/docs/#publish) Edge Delivery Servicesドキュメント。
* AEMコンテンツ — 詳しくは、以下を参照してください。

## AEMからのフローの公開 {#publishing-flow}

ユニバーサルエディターを使用してAEMコンテンツをオーサリングする場合、公開は、 **公開** 」ボタンをクリックします。 ドキュメントを参照してください [ユニバーサルエディターを使用したコンテンツの公開。](/help/implementing/universal-editor/publishing.md)

公開時の情報の流れは次のとおりです。 作成者が公開を開始すると、このフローは自動的に適用され、ここで説明します。

![AEMからEdge Delivery Servicesに公開する際の情報のフロー](assets/publishing-flow.png)

1. コンテンツ作成者は、ユニバーサルエディターでAEMコンテンツを公開します。
1. 公開イベントがAdobeパイプラインキューにプッシュされます。
1. Edge 配信公開サービスは、関連するイベントを Edge Delivery Admin API に転送します。
1. Edge 配信は、AEMオーサーからセマンティックHTMLを取り込みます。
1. AEMが公開ステータスで更新されます。

## 使用の手引き {#how-to-get-started}

この機能にアクセスするには、Adobe担当者にお問い合わせください。
