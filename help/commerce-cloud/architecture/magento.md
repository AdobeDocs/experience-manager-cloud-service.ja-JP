---
title: Commerce Integration Frameworkを使用したAEMとMagentoの統合
description: AEMとMagentoは、Commerce Integration Framework(CIF)を使用してシームレスに統合されます。 CIFを使用すると、AEMはMagentoインスタンスにアクセスし、GraphQLを介してMagentoと通信できます。 また、AEM作成者は、製品とカテゴリの選択機能と製品コンソールを使用して、Magentoからオンデマンドで取得した製品とカテゴリのデータを参照できます。 さらに、CIFには標準搭載のストアフロントが用意されており、これによりコマースプロジェクトの迅速化に役立ちます。
thumbnail: aem-magento-architecture.jpg
translation-type: tm+mt
source-git-commit: 72d98c21a3c02b98bd2474843b36f499e8d75a03
workflow-type: tm+mt
source-wordcount: '403'
ht-degree: 2%

---


# AEM and Magento Integration using Commerce Integration Framework {#aem-magento-framework}

AEMとMagentoは、Commerce Integration Framework(CIF)を使用してシームレスに統合されます。 CIFを使用すると、AEMはMagentoインスタンスにアクセスし、GraphQLを介してMagentoと通信できます。 また、AEM作成者は、製品とカテゴリの選択機能と製品コンソールを使用して、Magentoからオンデマンドで取得した製品とカテゴリのデータを参照できます。 さらに、CIFには標準搭載のストアフロントが用意されており、これによりコマースプロジェクトの迅速化に役立ちます。

## アーキテクチャの概要 {#overview}

アーキテクチャ全体を次に示します。

![CIFアーキテクチャの概要](../assets/AEM_Magento_Architecture.JPG)

CIFはGraphQLのサポートに基づいて構築されます。 AEMとMagento間の主な通信チャネルは、Magentoの [GraphQL API](https://devdocs.magento.com/guides/v2.4/graphql/) APIです。 Cloud ServiceとMagentoの間で通信を設定する方法は異なります。詳しくは、 [「はじめに](../getting-started.md) 」ページを参照してください。

CIF内では、サーバー側とクライアント側の通信パターンがサポートされます。
サーバー側API呼び出しは、組み込みの汎用 [GraphQLクライアント](https://github.com/adobe/commerce-cif-graphql-client) 、およびMagentoGraphQLスキーマ用に生成されたデータモデル [の](https://github.com/adobe/commerce-cif-magento-graphql) セットを組み合わせて使用して実装されます。 また、GraphQLクエリやGQL形式の変異も使用できます。

Reactを使用して構築されるクライアント側コンポーネントの場合は [、](https://reactjs.org/)Apollo Client [](https://www.apollographql.com/docs/react/) (Apollo Client)が使用されます。

## AEM CIFコアコンポーネントのアーキテクチャ {#cif-core-components}

![AEM CIFコアコンポーネントのアーキテクチャ](../assets/cif-component-architecture.jpg)

[AEM CIFコアコンポーネント](https://github.com/adobe/aem-core-cif-components) は、 [AEM WCMコアコンポーネントと同様の設計パターンとベストプラクティスに従っています](https://github.com/adobe/aem-core-wcm-components)。

AEM CIFコアコンポーネントのMagentoとのビジネスロジックとバックエンドの通信は、Slingモデルに実装されます。 プロジェクト固有の要件を満たすためにこのロジックをカスタマイズする必要がある場合は、Slingモデルの委任パターンを使用できます。

>[!TIP]
>
>AEM CIFコアコンポーネントの [](../customizing/customize-cif-components.md) カスタマイズページには、CIFコアコンポーネントのカスタマイズ方法に関する詳細な例とベストプラクティスが記載されています。

プロジェクト内では、AEM CIFコアコンポーネントとカスタムプロジェクトコンポーネントは、Sling Context-Aware設定を使用して、AEMページに関連付けられたMagentoストア用に設定されたクライアントを簡単に取得できます。
