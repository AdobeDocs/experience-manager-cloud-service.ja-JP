---
title: 概要
description: 様々なストアフロントオプションについて
thumbnail: introducing-aem-commerce.jpg
exl-id: 29410f76-a63f-4b0a-b817-2ed724ad1a3c
feature: Commerce Integration Framework
role: Admin
source-git-commit: 145cd4961bd9c0c7bb7e39a1d6dae67f240ecb4d
workflow-type: tm+mt
source-wordcount: '635'
ht-degree: 1%

---


# コンテンツとコマース {#content-commerce}

インテントベースの高パフォーマンスなコマースエクスペリエンスに対する顧客の期待が高まるにつれ、ブランドは品質を犠牲にすることなく、より多くのコンテンツをより迅速に提供しなければならないというプレッシャーにさらされています。 Adobe Experience Managerを使用すると、ブランドはスケーリングとイノベーションをより迅速に行い、臨場感のあるコマースエクスペリエンスを作成し、より多くのトラフィックを取り込み、増加するオンライン支出を獲得できます。

Adobe Experience Managerには、コンテンツに富み、パーソナライズされたカスタマーエクスペリエンスを作成および管理する強力なツールが用意されています。 AEMをAdobe Commerce、Salesforce Commerce、SAP Commerce Cloudなどのコマースソリューションと統合することで、ブランドはコンテンツとコマースを統合し、あらゆるチャネルにわたってシームレスなショッピングジャーニーを実現できます。

## ストアフロントのアプローチの概要 {#overview}

AEMは、状況と好みに基づいてお客様をサポートできます。 次のガイダンスを使用して、適切なアプローチを選択してください。

* [Edge Delivery Servicesの使用（推奨）](#edge)
* [独自のストアフロントの使用（ヘッドレス AEM統合）](#own-storefront)
* [AEM CIF ストアフロントの使用](#cif)

### Edge Delivery Servicesの使用（推奨） {#edge}

企業が Web 上で最も速く、AI に優しいストアフロントを求めており、開発者が最先端の開発者向けエクスペリエンスを求めている場合は、[Edge Delivery Servicesを使用してください。Edge Delivery Services](../edge/overview.md)、今日および将来の要件をすべて満たしています。 バックエンドとソリューションによっては、次のように異なるオプションがあります。

#### &#x200B;1. Adobe Commerce as a Cloud Serviceとの統合 {#acaacs}

これは、Edge Deliveryと [0}Adobe Commerce ストアフロント } を出発点として使用する場合に最適なソリューションです。 ](https://experienceleague.adobe.com/developer/commerce/storefront/)ストアフロントには、Adobe Commerce サービス、API と事前統合されたボイラープレートが付属しており、ストアフロントを迅速に構築するための様々なCommerce ドロップインコンポーネントを提供します。

サイズの適合：Adobe Commerce as a Cloud Serviceでの一般的なストアフロントのエクスペリエンス

#### &#x200B;2. Adobe Commerce Optimizerとの統合（サードパーティ製ソリューションの場合） {#aco}

既存のコマースソリューションを統合してカタログのパフォーマンスを高める場合、Adobeでは、[Adobe Commerce Optimizer](https://experienceleague.adobe.com/en/docs/commerce-learn/tutorials/adobe-commerce-optimizer/overview) を最新の統合レイヤーとして使用することをお勧めします。 Commerce Optimizerは、カタログおよびマーチャンダイジング向けの高性能な SaaS サービスを提供することで、コマースソリューションを強化します。 Adobe Commerce as a Cloud Serviceと同様、[Adobe Commerce ストアフロント ](https://experienceleague.adobe.com/developer/commerce/storefront/) もすぐに使用できます。

Salesforce Commerceなどの商用コマースソリューションとの統合が可能です。 Adobe担当者にお問い合わせください。

最適：既存のコマースソリューションを使用した一般的なストアフロントのエクスペリエンス

#### &#x200B;3. カスタム統合 {#custom}

Adobeでは、カスタム統合を構築する場合に、Edge Delivery Servicesを使用することをお勧めします。 最初から開始するか、Edge Delivery ストアフロントで既存の JS-framework コマースコンポーネント（トランザクション部分の場合など）を再利用できます。 これにより、顧客は代理店に優しい超高速のショッピングエクスペリエンスを得ることができますが、既存の投資を再利用して TTV を増やすことができます。 開始点はデフォルトの [Edge Delivery ボイラープレート ](https://www.aem.live/developer/tutorial) です。

適切なサイズ：Edge配信ストアフロントの価値が低い

### 独自のストアフロントの使用（ヘッドレス AEM統合） {#own-storefront}

既存のストアフロント（React JS で構築など）があり、コンテンツの管理と配信（コンテンツフラグメント）、アセットおよびコンテキスト内編集（ユニバーサルエディター）にAdobe Experience Managerを使用する場合。 統合の出発点は、[Adobe Experience Manager as a ヘッドレス CMSの概要 ](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/headless/introduction) および [CIF アドオン ](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/content-and-commerce/storefront/authoring/enrich-product-associated-content) です。 CIF アドオンを使用すると、商品データをAEM（AEM UI 内で商品を検索、参照、検索する）にシームレスに統合し、コマース固有のエクスペリエンスを構築できます。

### AEM CIF ストアフロント {#cif}

Adobeの推奨事項と参照アーキテクチャは、Edge Delivery Servicesを使用することです。 AEM CIF コアコンポーネントを含むCIF ストアフロントは、現在メンテナンスモードになっており、新しいプロジェクトでは使用しないでください。 参照については、[CIFのドキュメントを参照してください。](/help/commerce-cloud/cif-introduction.md)

>[!NOTE]
>
>AEMまたはCommerceの新しい機能の活用を検討している既存のお客様は、web サイトをEdge Deliveryに移行する必要があります。 一般的なパターンは、ページのサブセットのみをEdge Deliveryに移動し、Edge Deliery ページとCIF ページを並べて実行することから始めます。 また、新しいCommerce機能を活用するために、AEM CIF コンポーネントを新しい [Commerce ドロップインコンポーネント ](https://experienceleague.adobe.com/developer/commerce/storefront/dropins/all/introduction/) に置き換えることもできます。
