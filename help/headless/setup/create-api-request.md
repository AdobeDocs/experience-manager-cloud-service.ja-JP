---
title: API リクエストの作成 - ヘッドレス設定
description: コンテンツフラグメントコンテンツと AEM Assets REST API のヘッドレス配信に GraphQL API を使用して、コンテンツフラグメントを管理する方法を説明します。
exl-id: 2b72f222-2ba5-4a21-86e4-40c763679c32
feature: Headless, Content Fragments,GraphQL API
role: Admin, Developer
source-git-commit: 38a4bf89e099432163163e90e08aa0f47407724f
workflow-type: tm+mt
source-wordcount: '417'
ht-degree: 92%

---

# API リクエストの作成 - ヘッドレス設定 {#accessing-delivering-content-fragments}

コンテンツフラグメントコンテンツと AEM Assets REST API のヘッドレス配信に GraphQL API を使用して、コンテンツフラグメントを管理する方法を説明します。

## GraphQL API と Assets REST API とは {#what-are-the-apis}

[コンテンツフラグメントをいくつか作成したので](create-content-fragment.md)、AEM の API を使用してヘッドレスで配信できます。

* [GraphQL](/help/headless/graphql-api/content-fragments.md) API を使用すると、コンテンツフラグメントにアクセスして配信するリクエストを作成できます。この API は、コンテンツフラグメントコンテンツのクエリと使用に最も堅牢な機能セットを提供します。
   * API を使用するには、[エンドポイントを AEM で定義して有効にし](/help/headless/graphql-api/graphql-endpoint.md)、必要に応じて [GraphiQL インターフェイスをインストール](/help/headless/graphql-api/graphiql-ide.md)します。
* 様々な [&#x200B; 構造化コンテンツ配信および管理用のAEM API](/help/headless/apis-headless-and-content-fragments.md) をコンテンツフラグメントと共に使用できます。

このガイドの残りの部分では、GraphQL へのアクセスとコンテンツフラグメントの配信について説明します。

## GraphQL エンドポイントの有効化 {#enable-graphql-endpoint}

GraphQL API を使用する前に、GraphQL エンドポイントを作成する必要があります。

詳しくは、[AEMのGraphQL エンドポイントの管理 &#x200B;](/help/headless/graphql-api/graphql-endpoint.md) を参照してください。

## GraphQL と GraphiQL を使用したクエリコンテンツ

情報アーキテクトは、チャネルエンドポイントがコンテンツを配信するためのクエリを設計します。これらのクエリは、エンドポイントごと、モデルごとに 1 回だけ検討してください。この入門ガイドでは、作成する必要があるのは 1 つだけです。

GraphiQL は IDE であり、AEM 環境に含まれています。[エンドポイントを設定](#enable-graphql-endpoint)した後、アクセス可能になり表示されます。

詳しくは、[GraphiQL IDE の使用 &#x200B;](/help/headless/graphql-api/graphiql-ide.md) を参照してください。

GraphQL を使用すると、特定のデータセットや個々のデータオブジェクトをターゲットにするだけでなく、オブジェクトの特定の要素、ネストされた結果を配信したり、クエリ変数のサポートを提供したりできる構造化クエリが可能になります。

GraphQL では、反復的な API リクエストと過剰な配信を回避でき、代わりに単一の API クエリへの応答としてレンダリングに必要なものを正確に一括配信できます。結果の JSON を使用して、他のサイトやアプリにデータを配信できます。

## 次の手順 {#next-steps}

これで作業は完了です。AEM のヘッドレスコンテンツ管理に関する基本的な内容を説明しました。利用可能な機能の包括的な理解を深めるためのリソースは他にもたくさんあります。

* **[コンテンツフラグメント](/help/sites-cloud/administering/content-fragments/managing.md)** - コンテンツフラグメントの作成と管理に関する詳細
* **[AEM Assets HTTP API でサポートされるコンテンツフラグメント](/help/assets/content-fragments/assets-api-content-fragments.md)** - CRUD 操作（作成、読み取り、更新、削除）を介して HTTP API 経由で直接 AEM コンテンツにアクセスする方法の詳細
* **[GraphQL API](/help/headless/graphql-api/content-fragments.md)** - コンテンツフラグメントをヘッドレスで配信する方法の詳細

>[!NOTE]
>
>この[コンテンツフラグメントおよびコンテンツフラグメントモデルの OpenAPI](/help/headless/content-fragment-openapis.md) も利用できます。
