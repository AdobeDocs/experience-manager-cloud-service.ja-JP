---
title: コマース統合フレームワークを使用した、AEM と Magento の統合
description: AEM と Magento は、コマース統合フレームワーク（CIF）を使用してシームレスに統合されます。CIF を使用すると、AEM は Magento インスタンスにアクセスし、GraphQL を介して Magento と通信できます。また、AEM オーサーは、製品とカテゴリの選択機能と製品コンソールを使用して、Magento からオンデマンドで取得した製品とカテゴリデータを参照できます。さらに、CIF には標準搭載のストアフロントが用意されており、コマースプロジェクトの迅速化に役立ちます。
thumbnail: aem-magento-architecture.jpg
translation-type: tm+mt
source-git-commit: 72d98c21a3c02b98bd2474843b36f499e8d75a03
workflow-type: tm+mt
source-wordcount: '403'
ht-degree: 100%

---


# コマース統合フレームワークを使用した、AEM と Magento の統合 {#aem-magento-framework}

AEM と Magento は、コマース統合フレームワーク（CIF）を使用してシームレスに統合されます。CIF を使用すると、AEM は Magento インスタンスにアクセスし、GraphQL を介して Magento と通信できます。また、AEM オーサーは、製品とカテゴリの選択機能と製品コンソールを使用して、Magento からオンデマンドで取得した製品とカテゴリデータを参照できます。さらに、CIF には標準搭載のストアフロントが用意されており、コマースプロジェクトの迅速化に役立ちます。

## アーキテクチャの概要 {#overview}

全体的なアーキテクチャは次のとおりです。

![CIF アーキテクチャの概要](../assets/AEM_Magento_Architecture.JPG)

CIF は GraphQL のサポートに基づいて構築されます。AEM と Magento 間の主な通信チャネルは、Magento の [GraphQL API](https://devdocs.magento.com/guides/v2.4/graphql/) API です。AEM as a Cloud Service と Magento 間で通信を設定する方法は異なります。詳しくは、[はじめに](../getting-started.md)ページを参照してください。

CIF 内では、サーバーサイドとクライアントサイドの通信パターンがサポートされます。
サーバーサイド API 呼び出しは、組み込みの汎用 [GraphQL クライアント](https://github.com/adobe/commerce-cif-graphql-client)と、Magento GraphQL スキーマ用に[生成されたデータモデルセット](https://github.com/adobe/commerce-cif-magento-graphql)を組み合わせたものを使用して実装されます。また、GraphQL クエリや GQL 形式のミューテーションも使用できます。

[React](https://reactjs.org/) を使用して構築されるクライアントサイドコンポーネントの場合は、[Apollo Client](https://www.apollographql.com/docs/react/) が使用されます。

## AEM CIF コアコンポーネントのアーキテクチャ {#cif-core-components}

![AEM CIF コアコンポーネントのアーキテクチャ](../assets/cif-component-architecture.jpg)

[AEM CIF コアコンポーネント](https://github.com/adobe/aem-core-cif-components)は、[AEM WCM コアコンポーネント](https://github.com/adobe/aem-core-wcm-components)と同様の設計パターンとベストプラクティスに従っています。

AEM CIF コアコンポーネントの Magento とのビジネスロジックとバックエンドの通信は、Sling Model で実装されます。プロジェクト固有の要件を満たすために、このロジックをカスタマイズする必要がある場合は、Sling モデルの委任パターンを使用できます。

>[!TIP]
>
>[AEM CIF コアコンポーネントのカスタマイズ](../customizing/customize-cif-components.md)ページには、CIF コアコンポーネントのカスタマイズ方法に関する詳細な例とベストプラクティスが記載されています。

プロジェクト内では、AEM CIF コアコンポーネントとカスタムプロジェクトコンポーネントは、Sling Context-Aware 設定を使用して、AEM ページに関連付けられた Magento ストア用に設定されたクライアントを簡単に取得できます。
