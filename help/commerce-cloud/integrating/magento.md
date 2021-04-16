---
title: Commerce Integration Frameworkを使用したAEMおよびAdobeコマース(Magento)統合
description: AEMとAdobeコマース(Magento)は、Commerce Integration Framework(CIF)を使用してシームレスに統合されます。 CIF を使用すると、AEM は Magento インスタンスにアクセスし、GraphQL を介して Magento と通信できます。また、AEM オーサーは、製品とカテゴリの選択機能と製品コンソールを使用して、Magento からオンデマンドで取得した製品とカテゴリデータを参照できます。さらに、CIF には標準搭載のストアフロントが用意されており、コマースプロジェクトの迅速化に役立ちます。
thumbnail: aem-magento-architecture.jpg
exl-id: 1cdfda88-a728-432f-b24a-f81347572bcf
translation-type: tm+mt
source-git-commit: a4e53fdcb33eab8afabcb13d651155cd247bda1f
workflow-type: tm+mt
source-wordcount: '392'
ht-degree: 37%

---

# Commerce Integration Frameworkを使用したAEMとAdobeコマース(Magento)の統合{#aem-magento-framework}

Experience ManagerとAdobeコマース(Magento)は、Commerce Integration Framework(CIF)を使用してシームレスに統合されます。 CIFを使用すると、AEMはAdobeコマースの[GraphQL API](https://devdocs.magento.com/guides/v2.4/graphql/)を使用して、コマースインスタンスに直接アクセスし、通信できます。

>[!NOTE]
>
>GraphQLは現在、Adobe Experience Manager(AEM)の2つの（個別の）シナリオでCloud Serviceとして使用されています。
>
>* このシナリオでは、CIFがGraphQLを介してコマースと通信します。
>* [AEMコンテンツフラグメントは、AEM GraphQL API（標準のGraphQLに基づいてカスタマイズされた実装）と連携して、アプリケーションで使用する構造化コンテンツを配信します](/help/assets/content-fragments/graphql-api-content-fragments.md)。


## アーキテクチャの概要 {#overview}

全体的なアーキテクチャは次のとおりです。

![CIF アーキテクチャの概要](../assets/AEM_Magento_Architecture.png)

CIF 内では、サーバーサイドとクライアントサイドの通信パターンがサポートされます。
サーバ側のAPI呼び出しは、ビルドインの汎用[GraphQLクライアント](https://github.com/adobe/commerce-cif-graphql-client)とコマースGraphQLスキーマ用の[生成されたデータモデル](https://github.com/adobe/commerce-cif-magento-graphql)のセットを組み合わせて使用して実装されます。

[React](https://reactjs.org/) を使用して構築されるクライアントサイドコンポーネントの場合は、[Apollo Client](https://www.apollographql.com/docs/react/) が使用されます。

## AEM CIF コアコンポーネントのアーキテクチャ {#cif-core-components}

![AEM CIF コアコンポーネントのアーキテクチャ](../assets/cif-component-architecture.jpg)

[AEM CIFコア](https://github.com/adobe/aem-core-cif-components) コンポーネントは、 [AEM WCMコアコンポーネントと非常に似た設計パターンとベストプラクティスに従っています](https://github.com/adobe/aem-core-wcm-components)。

AEM CIFコアコンポーネント用のビジネスロジックとAdobeコマースとのバックエンド通信は、Slingモデルに実装されます。 プロジェクト固有の要件を満たすためにこのロジックをカスタマイズする必要がある場合は、Slingモデルの委任パターンを使用できます。

>[!TIP]
>
>[AEM CIF コアコンポーネントのカスタマイズ](../customizing/customize-cif-components.md)ページには、CIF コアコンポーネントのカスタマイズ方法に関する詳細な例とベストプラクティスが記載されています。

プロジェクト内では、AEM CIFコアコンポーネントとカスタムプロジェクトコンポーネントは、Sling Context-Aware設定を使用して、AEMページに関連付けられたAdobeコマースストア用に設定されたクライアントを簡単に取得できます。
