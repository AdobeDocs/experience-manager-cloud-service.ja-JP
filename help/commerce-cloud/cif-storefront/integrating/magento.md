---
title: コマース統合フレームワークを使用した、AEM と Adobe Commerce の統合
description: AEM と Adobe Commerce は、コマース統合フレームワーク（CIF）を使用してシームレスに統合されます。CIF を使用すると、AEM は Adobe Commerce インスタンスにアクセスし、GraphQL を介して Adobe Commerce と通信できます。また、AEM オーサーは、製品とカテゴリの選択機能と製品コンソールを使用して、Adobe Commerce からオンデマンドで取得した製品とカテゴリデータを参照できます。さらに、CIF には標準搭載のストアフロントが用意されており、コマースプロジェクトの迅速化に役立ちます。
thumbnail: aem-magento-architecture.jpg
exl-id: 110ceef5-2c35-4b81-8e89-26929c0da91b
feature: Commerce Integration Framework
role: Admin
index: false
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '439'
ht-degree: 83%

---


# コマース統合フレームワークを使用した、AEM と Adobe Commerce の統合 {#aem-framework}

Experience Manager と Adobe Commerce は、コマース統合フレームワーク（CIF）を使用してシームレスに統合されます。CIFを使用すると、AEMはAdobe Commerce [GraphQL API を使用して、コマースインスタンスに直接アクセスして通信できます。](https://devdocs.magento.com/guides/v2.4/graphql/)

>[!NOTE]
>
> サポートされている GraphQL API の最小バージョンは 2.3.5 です。一部の機能は、新しいバージョンでのみ、または Adobe Commerce エディションでのみサポートされています。

>[!NOTE]
>
>GraphQL は現在、Adobe Experience Manager（AEM）as a Cloud Service の、2 つの（個別の）シナリオで使用されています。
>
>* このシナリオでは、CIF が GraphQL を使用してコマースと通信します。
>* [AEM コンテンツフラグメントは、AEM GraphQL API （標準のGraphQLに基づいてカスタマイズされた実装）と連携して、アプリケーションで使用する構造化コンテンツを配信します。](/help/headless/graphql-api/content-fragments.md)

## アーキテクチャの概要 {#overview}

全体的なアーキテクチャは次のとおりです。

![CIF アーキテクチャの概要](../assets/AEM_Magento_Architecture.png)

CIF 内では、サーバーサイドとクライアントサイドの通信パターンがサポートされます。
サーバーサイド API 呼び出しは、ビルトインの汎用的な [GraphQL クライアント](https://github.com/adobe/commerce-cif-graphql-client) と、コマース GraphQL スキーマ用に [生成された一連のデータモデル](https://github.com/adobe/commerce-cif-magento-graphql) を組み合わせたものを使用して実装されます。また、GraphQL クエリや GQL 形式のミューテーションも使用できます。

[React](https://reactjs.org/) を使用して作成されるクライアントサイドコンポーネントの場合は、[Apollo クライアント](https://www.apollographql.com/docs/react/) が使用されます。

## AEM CIF コアコンポーネントのアーキテクチャ {#cif-core-components}

![AEM CIF コアコンポーネントのアーキテクチャ](../assets/cif-component-architecture.jpg)

[AEM CIF コアコンポーネント](https://github.com/adobe/aem-core-cif-components)は、[AEM WCM コアコンポーネント](https://github.com/adobe/aem-core-wcm-components)と同様の設計パターンとベストプラクティスに従っています。

AEM CIF コアコンポーネントの Adobe Commerce とのビジネスロジックとバックエンドの通信は、Sling Model で実装されます。プロジェクト固有の要件を満たすために、このロジックをカスタマイズする必要がある場合は、Sling モデルの委任パターンを使用できます。

>[!TIP]
>
>[AEM CIF コアコンポーネントのカスタマイズ](/help/commerce-cloud/cif-storefront/customizing/customize-cif-components.md)ページには、CIF コアコンポーネントのカスタマイズ方法に関する詳細な例とベストプラクティスが記載されています。

プロジェクト内では、AEM CIF コアコンポーネントとカスタムプロジェクトコンポーネントは、Sling Context-Aware 設定を使用して、AEM ページに関連付けられた Adobe Commerce ストア用に設定されたクライアントを簡単に取得できます。

## 検索

CIFには、すぐに使用できる [&#x200B; 検索コアコンポーネント &#x200B;](https://www.aemcomponents.dev/content/core-components-examples/library/commerce/search.html) が用意されています。これは、[Commerce GraphQL API に基づくサーバーサイドのレンダリング済み検索エクスペリエンスです。Commerceのお客様 &#x200B;](https://developer.adobe.com/commerce/webapi/graphql/)、代わりに [Live Search](https://experienceleague.adobe.com/docs/commerce-merchant-services/live-search/guide-overview.html) を使用できます。 CIF とライブ検索の統合について詳しくは、この[リンク](/help/commerce-cloud/cif-storefront/integrating/live-search-plp.md)に従ってください。
