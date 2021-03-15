---
title: コンテンツフラグメントに対するリモート AEM GraphQL クエリの認証
description: リモート AEM GraphQL クエリに必要な認証について説明します。
translation-type: tm+mt
source-git-commit: 42ca0c70f7018a6e3c9be68ef13adefafc987864
workflow-type: tm+mt
source-wordcount: '217'
ht-degree: 100%

---


# コンテンツフラグメントに対するリモート AEM GraphQL クエリの認証 {#authentication-for-remote-aem-graphql-queries-on-content-fragments}

[コンテンツフラグメント配信用の Adobe Experience Manager as a Cloud Service（AEM）GraphQL API](/help/assets/content-fragments/graphql-api-content-fragments.md) の主な使用例は、サードパーティのアプリケーションやサービスからリモートクエリを受け入れることです。これらのリモートクエリには、認証済み API アクセスが必要な場合があります。

>[!NOTE]
>
>テストおよび開発の場合は、[GraphiQL インターフェイス](/help/assets/content-fragments/graphql-api-content-fragments.md#graphiql-interface)を使用して AEM GraphQL API に直接アクセスすることもできます。

認証のために、サードパーティのサービスは[アクセストークン](#access-token)を使用する必要があります。その後、このトークンは [GraphQL リクエストで使用](#use-access-token-in-graphql-request)できます。

## アクセストークンの取得 {#retrieving-access-token}

詳しくは、[サーバー側 API のアクセストークンの生成](/help/implementing/developing/introduction/generating-access-tokens-for-server-side-apis.md)を参照してください。

## GraphQL リクエストでのアクセストークンの使用 {#use-access-token-in-graphql-request}

サードパーティのサービスが AEM インスタンスに接続するには、*アクセストークン*&#x200B;が必要です。サービスは次に、このトークンを POST リクエストの `Authorization` ヘッダーに追加する必要があります。

例えば、GraphQL の Authorization ヘッダーは次のようになります。

```xml
Authorization: Bearer <access_token>
```

## 権限の要件 {#permission-requirements}

アクセストークンを使用しておこなわれるすべてのリクエストは、実際には、*そのトークンを生成したユーザーアカウントによって*&#x200B;おこなわれます。

つまり、GraphQL クエリの実行に必要な権限がアカウントにあることを確認する必要があります。

この確認は、ローカルインスタンスで GraphiQL を使用しておこなえます。
