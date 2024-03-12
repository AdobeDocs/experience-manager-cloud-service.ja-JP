---
title: Edge Delivery Services用コンテンツの公開
description: コンテンツの公開がEdge Delivery Servicesと連携する仕組みと、AEMコンテンツをEdge Delivery Servicesと共に公開する方法について説明します。
feature: Edge Delivery Services
exl-id: 32fbb144-9175-47a9-bb5a-ca15f3fcd2d8
source-git-commit: 3ee1ba83518c3d4fba59b0c98b31e5c63a2eb6ab
workflow-type: tm+mt
source-wordcount: '295'
ht-degree: 0%

---


# Edge Delivery Services用コンテンツの公開 {#publishing-edge}

Edge Delivery Servicesを使用すれば、コンテンツソースに関係なく、コンテンツの公開がシームレスに行われます。

* ドキュメントベースのコンテンツ — 詳しくは、 [セクションを公開](/help/edge/docs/authoring.md) Edge Delivery Servicesドキュメント。
* AEMコンテンツ — 詳しくは、以下を参照してください。

## AEMからのフローの公開 {#publishing-flow}

ユニバーサルエディターを使用してAEMコンテンツをオーサリングする場合、公開は、 **公開** 」ボタンをクリックします。 ドキュメントを参照してください [ユニバーサルエディターを使用したコンテンツの公開。](/help/sites-cloud/authoring/universal-editor/publishing.md)

公開時の情報の流れは次のとおりです。 作成者が公開を開始すると、このフローは自動的に適用され、ここで説明します。

>[!NOTE]
>
>オーサリング UI またはワークフローから公開されるパスは、1 日に最大 5,000 個まで許可されます。 一括公開作業読み込みを作成する統合はサポートされていません。

![AEMからEdge Delivery Servicesに公開する際の情報のフロー](assets/publishing-flow.png)

1. コンテンツ作成者は、ユニバーサルエディターでAEMコンテンツを公開します。
1. 公開イベントがAdobeパイプラインキューにプッシュされます。
1. Edge Delivery Services公開サービスは、関連するイベントをEdge Delivery Services管理 API に転送します。
1. Edge Delivery は、AEMオーサーからセマンティックHTMLを取り込み、取り込みます。
1. AEMが公開ステータスで更新されます。

>[!NOTE]
>
>デフォルトでは、Edge Delivery Services管理 API は保護されておらず、認証なしでドキュメントを公開または非公開にするために使用できます。 管理 API の認証を設定するには、 [作成者用の認証の設定](https://www.aem.live/docs/authentication-setup-authoring)に設定する場合、プロジェクトは API_KEY でプロビジョニングされ、パブリッシュサービスへのアクセスを許可する必要があります。 [SlackのAdobeチームに連絡してください](/help/edge/docs/slack.md) 指導のために

## 使用の手引き {#how-to-get-started}

この機能にアクセスするには、Adobe担当者にお問い合わせください。
