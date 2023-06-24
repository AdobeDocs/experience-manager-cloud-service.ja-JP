---
title: コンテンツフラグメントに対するリモート AEM GraphQL クエリの認証
description: ヘッドレスコンテンツ配信を保護するためにリモートAdobe Experience Manager GraphQLクエリに必要な認証を理解します。
feature: Content Fragments,GraphQL API
exl-id: dfeae661-06a1-4001-af24-b52ae12d625f
source-git-commit: 7260649eaab303ba5bab55ccbe02395dc8159949
workflow-type: tm+mt
source-wordcount: '230'
ht-degree: 26%

---

# コンテンツフラグメントに対するリモート AEM GraphQL クエリの認証 {#authentication-for-remote-aem-graphql-queries-on-content-fragments}

主な用途 [コンテンツフラグメント配信用Adobe Experience Manager as a Cloud Service (AEM)GraphQL API](/help/headless/graphql-api/content-fragments.md) は、サードパーティのアプリケーションまたはサービスからのリモートクエリを受け入れます。 これらのリモートクエリでヘッドレスコンテンツ配信を保護するには、認証済み API アクセスが必要になる場合があります。

>[!NOTE]
>
>テストおよび開発の場合は、 [GraphiQL インターフェイス](/help/headless/graphql-api/graphiql-ide.md).

認証の場合、サードパーティのサービスは [アクセストークンの取得](#retrieving-access-token) そうなれば [GraphQL Request で使用](#use-access-token-in-graphql-request).

## アクセストークンの取得 {#retrieving-access-token}

詳しくは、 [サーバー側 API 用のアクセストークンの生成](/help/implementing/developing/introduction/generating-access-tokens-for-server-side-apis.md) 詳細はこちら。

## GraphQL リクエストでのアクセストークンの使用 {#use-access-token-in-graphql-request}

サードパーティのサービスがAEMインスタンスに接続するには、次の条件が満たされている必要があります。 *アクセストークン*. サービスは次に、このトークンを POST リクエストの `Authorization` ヘッダーに追加する必要があります。

例えば、GraphQL の Authorization ヘッダーは次のようになります。

```xml
Authorization: Bearer <access_token>
```

## 権限の要件 {#permission-requirements}

アクセストークンを使用しておこなわれたすべてのリクエストがおこなわれます *トークンを生成したユーザーアカウント別*.

このユーザーアカウントは、GraphQLクエリを実行するために必要な権限がアカウントにあることを確認する必要があることを意味します。

これらの権限は、ローカルインスタンスで GraphiQL を使用して確認できます。 権限について詳しくは、[こちら](/help/headless/security/permissions.md)を参照してください。
