---
title: コマース統合フレームワークを使用した、AEM と Adobe Commerce（Magento）の統合
description: AEM と Adobe Commerce（Magento）は、コマース統合フレームワーク（CIF）を使用してシームレスに統合されます。CIF を使用すると、AEM は Magento インスタンスにアクセスし、GraphQL を介して Magento と通信できます。また、AEM オーサーは、製品とカテゴリの選択機能と製品コンソールを使用して、Magento からオンデマンドで取得した製品とカテゴリデータを参照できます。さらに、CIF には標準搭載のストアフロントが用意されており、コマースプロジェクトの迅速化に役立ちます。
thumbnail: aem-magento-architecture.jpg
exl-id: 110ceef5-2c35-4b81-8e89-26929c0da91b,1cdfda88-a728-432f-b24a-f81347572bcf
source-git-commit: 52cfd60cde3165fde6b0167783c16b0fc1efc950
workflow-type: tm+mt
source-wordcount: '413'
ht-degree: 82%

---

# コマース統合フレームワークを使用した、AEM と Adobe Commerce（Magento）の統合 {#aem-magento-framework}

Experience Manager と Adobe Commerce（Magento）は、コマース統合フレームワーク（CIF）を使用してシームレスに統合されます。CIF を使用すると、AEM は Adobe Commerce の [GraphQL API](https://devdocs.magento.com/guides/v2.4/graphql/) を使用して、コマースインスタンスに直接アクセスして通信できます。

>[!NOTE]
>
> サポートされる GraphQL API の最小バージョンは 2.3.5 です。一部の機能は、新しいバージョンでのみ、またはAdobe Commerceエディションでのみサポートされます。

>[!NOTE]
>
>GraphQL は現在、Adobe Experience Manager（AEM）as a Cloud Service の、2 つの（個別の）シナリオで使用されています。
>
>* このシナリオでは、CIF が GraphQL を使用してコマースと通信します。
>* [AEM コンテンツフラグメントは、AEM GraphQL API（標準の GraphQL に基づいてカスタマイズされた実装）と連携して、アプリケーションで使用する構造化コンテンツを配信します](/help/assets/content-fragments/graphql-api-content-fragments.md)。


## アーキテクチャの概要 {#overview}

全体的なアーキテクチャは次のとおりです。

![CIF アーキテクチャの概要](../assets/AEM_Magento_Architecture.png)

CIF 内では、サーバーサイドとクライアントサイドの通信パターンがサポートされます。

サーバー側 API 呼び出しは、組み込みの汎用 API を使用して実装されます [GraphQL クライアント](https://github.com/adobe/commerce-cif-graphql-client) ～と組み合わせて [生成されたデータモデルのセット](https://github.com/adobe/commerce-cif-magento-graphql) コマース GraphQL スキーマの場合さらに、GraphQL クエリや GQL 形式のミューテーションを使用できます。

クライアントサイドコンポーネント（を使用して構築） [React](https://reactjs.org/)、 [Apollo Client](https://www.apollographql.com/docs/react/) が使用されます。

## AEM CIF コアコンポーネントのアーキテクチャ {#cif-core-components}

![AEM CIF コアコンポーネントのアーキテクチャ](../assets/cif-component-architecture.jpg)

[AEM CIF コアコンポーネント](https://github.com/adobe/aem-core-cif-components)は、[AEM WCM コアコンポーネント](https://github.com/adobe/aem-core-wcm-components)と同様の設計パターンとベストプラクティスに従っています。

AEM CIF コアコンポーネントの Adobe Commerce とのビジネスロジックとバックエンドの通信は、Sling Model で実装されます。プロジェクト固有の要件を満たすために、このロジックをカスタマイズする必要がある場合は、Sling モデルの委任パターンを使用できます。

>[!TIP]
>
>[AEM CIF コアコンポーネントのカスタマイズ](../customizing/customize-cif-components.md)ページには、CIF コアコンポーネントのカスタマイズ方法に関する詳細な例とベストプラクティスが記載されています。

プロジェクト内では、AEM CIF コアコンポーネントとカスタムプロジェクトコンポーネントは、Sling Context-Aware 設定を使用して、AEM ページに関連付けられた Adobe Commerce ストア用に設定されたクライアントを簡単に取得できます。
