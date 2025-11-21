---
title: 概要
description: 様々なストアフロントオプションについて
thumbnail: introducing-aem-commerce.jpg
exl-id: 29410f76-a63f-4b0a-b817-2ed724ad1a3c
feature: Commerce Integration Framework
role: Admin
source-git-commit: 80f1c9548b8b87dc6280e0e95988d84a8376f7ab
workflow-type: tm+mt
source-wordcount: '628'
ht-degree: 100%

---


# コンテンツとコマース {#content-commerce}

意図に基づいたパフォーマンスの高いコマースエクスペリエンスに対する顧客の期待が高まるにつれ、ブランドは品質を犠牲にすることなく、より多くのコンテンツをより迅速に提供する必要に迫られています。Adobe Experience Manager を使用すると、ブランドは規模を拡大して革新を高速化し、没入型のコマースエクスペリエンスを作成して、より多くのトラフィックと増加するオンライン支出を獲得できます。

Adobe Experience Manager には、コンテンツが豊富でパーソナライズされたカスタマーエクスペリエンスを作成および管理するための強力なツールが用意されています。AEM を Adobe Commerce、Salesforce Commerce、SAP Commerce Cloud などのコマースソリューションと統合して、ブランドはコンテンツとコマースを統合し、チャネルをまたいでシームレスなショッピングジャーニーを実現できます。

## ストアフロントアプローチの概要 {#overview}

AEM は、顧客の状況と好みに基づいてサポートできます。次のガイダンスを使用して、適切なアプローチを選択します。

* [Edge Delivery Services の使用（推奨）](#edge)
* [独自のストアフロントの使用（ヘッドレス AEM 統合）](#own-storefront)
* [AEM CIF ストアフロントの使用](#cif)

### Edge Delivery Services の使用（推奨） {#edge}

企業が web 上で最も速く、AI 対応のストアフロントを求めており、開発者が最先端の開発者エクスペリエンスを求めている場合は、Edge Delivery Services を使用します。[](../edge/overview.md)Edge Delivery Services は、今日および今後のすべての要件を満たします。バックエンドとソリューションに応じて、次の様々なオプションがあります。

#### &#x200B;1. Adobe Commerce as a Cloud Service との統合 {#acaacs}

アドビでは、開始点として Edge Delivery と [Adobe Commerce ストアフロント](https://experienceleague.adobe.com/developer/commerce/storefront/?lang=ja)を使用することをお勧めします。ストアフロントには、Adobe Commerce サービスや API が事前に統合されたボイラープレートが付属しており、ストアフロントを迅速に作成するための様々な Commerce ドロップインコンポーネントが用意されています。

最適：Adobe Commerce as a Cloud Service を使用した一般的なストアフロントのエクスペリエンス

#### &#x200B;2. Adobe Commerce Optimizer との統合（サードパーティソリューションの場合） {#aco}

既存のコマースソリューションを統合し、カタログのパフォーマンスを向上させる場合、アドビでは、[Adobe Commerce Optimizer](https://experienceleague.adobe.com/ja/docs/commerce-learn/tutorials/adobe-commerce-optimizer/overview) を最新の統合レイヤーとして使用することをお勧めします。Commerce Optimizer は、カタログおよびマーチャンダイジング用のパフォーマンスの高い SaaS サービスによりコマースソリューションを強化します。Adobe Commerce as a Cloud Service と同様に、[Adobe Commerce ストアフロント](https://experienceleague.adobe.com/developer/commerce/storefront/?lang=ja)を標準で使用できます。

Salesforce Commerce などの商用コマースソリューションとの統合が可能です。アドビ担当者にお問い合わせください。

最適：既存のコマースソリューションを使用した一般的なストアフロントのエクスペリエンス

#### &#x200B;3. カスタム統合 {#custom}

アドビでは、カスタム統合を作成する場合にも Edge Delivery Services の使用をお勧めします。Edge Delivery ストアフロントでは、最初から開始することも、既存の JS フレームワークコマースコンポーネント（トランザクション部分など）を再利用することもできます。これにより、顧客はエージェントにとって使いやすい超高速のショッピングエクスペリエンスを得られると同時に、既存の投資を再利用して TTV を増やすことができます。開始点は、デフォルトの [Edge Delivery ボイラープレート](https://www.aem.live/developer/tutorial)です。

最適：Edge Deliery ストアフロントからの価値が低い

### 独自のストアフロントの使用（ヘッドレス AEM 統合） {#own-storefront}

既存のストアフロント（例：React JS で作成）があり、コンテンツの管理と配信（コンテンツフラグメント）、アセット、コンテキスト内編集（ユニバーサルエディター）に Adobe Experience Manager を使用したいと考えています。統合の開始点は、[ヘッドレス CMS としての Adobe Experience Manager の概要](https://experienceleague.adobe.com/ja/docs/experience-manager-cloud-service/content/headless/introduction)と [CIF アドオン](https://experienceleague.adobe.com/ja/docs/experience-manager-cloud-service/content/content-and-commerce/storefront/authoring/enrich-product-associated-content)です。CIF アドオンを使用すると、製品データを AEM にシームレスに統合し（AEM UI 内で製品を検索、参照、見つける）、コマース固有のエクスペリエンスを作成できます。

### AEM CIF ストアフロント {#cif}

アドビのレコメンデーションおよび参照アーキテクチャは、Edge Delivery Services を使用することです。AEM CIF コアコンポーネントを含む CIF ストアフロントは、現在メンテナンスモードになっており、新しいプロジェクトでは使用しないでください。参照について詳しくは、[CIF のドキュメント](/help/commerce-cloud/cif-storefront/introduction.md)を参照してください。

>[!NOTE]
>
>新しい AEM／Commerce 機能を活用したい既存の顧客は、web サイトを Edge Delivery に移行する必要があります。一般的なパターンとしては、まずページのサブセットのみを Edge Delivery に移動し、Edge Delivery と CIF ページを並行して実行します。また、AEM CIF コンポーネントを新しい [Commerce ドロップインコンポーネント](https://experienceleague.adobe.com/developer/commerce/storefront/dropins/all/introduction/?lang=ja)に置き換えて、新しい Commerce 機能を活用することもできます。
