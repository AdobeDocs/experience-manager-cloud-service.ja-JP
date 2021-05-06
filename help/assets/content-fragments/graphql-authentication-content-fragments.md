---
title: コンテンツフラグメントに対するリモート AEM GraphQL クエリの認証
description: ヘッドレスコンテンツ配信を保護するために、リモートAEM GraphQLクエリに必要な認証を理解します。
feature: コンテンツフラグメント，GraphQL API
exl-id: dfeae661-06a1-4001-af24-b52ae12d625f
translation-type: tm+mt
source-git-commit: dab4c9393c26f5c3473e96fa96bf7ec51e81c6c5
workflow-type: tm+mt
source-wordcount: '235'
ht-degree: 75%

---

# コンテンツフラグメントに対するリモート AEM GraphQL クエリの認証 {#authentication-for-remote-aem-graphql-queries-on-content-fragments}

[コンテンツフラグメント配信用の Adobe Experience Manager as a Cloud Service（AEM）GraphQL API](/help/assets/content-fragments/graphql-api-content-fragments.md) の主な使用例は、サードパーティのアプリケーションやサービスからリモートクエリを受け入れることです。これらのリモートクエリは、ヘッドレスコンテンツの配信を保護するために、認証済みのAPIアクセスが必要になる場合があります。

>[!NOTE]
>
>テストおよび開発の場合は、[GraphiQL インターフェイス](/help/assets/content-fragments/graphql-api-content-fragments.md#graphiql-interface)を使用して AEM GraphQL API に直接アクセスすることもできます。

認証の場合、サードパーティのサービスはアクセストークン[を取得する必要があります。取得したは、GraphQL要求](#use-access-token-in-graphql-request)で[使用できます。](#retrieving-access-token)

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
