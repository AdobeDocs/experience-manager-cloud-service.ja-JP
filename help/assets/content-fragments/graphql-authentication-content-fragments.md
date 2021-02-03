---
title: リモートAEM GraphコンテンツフラグメントでのQLクエリの認証
description: Remote AEM GraphQLクエリに必要な認証について説明します。
translation-type: tm+mt
source-git-commit: 42ca0c70f7018a6e3c9be68ef13adefafc987864
workflow-type: tm+mt
source-wordcount: '217'
ht-degree: 0%

---


# コンテンツフラグメントでのリモートAEM GraphQLクエリの認証{#authentication-for-remote-aem-graphql-queries-on-content-fragments}

Cloud Service(AEM) GraphQL API for Content Fragment配信](/help/assets/content-fragments/graphql-api-content-fragments.md)としての[Adobe Experience Managerが、サードパーティのアプリケーションまたはサービスからリモートクエリを受け入れる場合の主な使用例です。  これらのリモートクエリには、認証済みAPIアクセスが必要な場合があります。

>[!NOTE]
>
>テストおよび開発の場合は、[GraphiQLインターフェイス](/help/assets/content-fragments/graphql-api-content-fragments.md#graphiql-interface)を使用してAEM GraphQL APIに直接アクセスすることもできます。

認証の場合、サードパーティのサービスは[アクセストークン](#access-token)を使用する必要があります。その後、[をGraphQL要求](#use-access-token-in-graphql-request)で使用できます。

## アクセストークン{#retrieving-access-token}を取得中

詳しくは、[サーバー側APIのアクセストークンの生成](/help/implementing/developing/introduction/generating-access-tokens-for-server-side-apis.md)を参照してください。

## GraphQLリクエスト{#use-access-token-in-graphql-request}でのアクセストークンの使用

サードパーティのサービスがAEMインスタンスと接続するには、*アクセストークン*&#x200B;が必要です。 次に、サービスは、このトークンをPOSTリクエストの`Authorization`ヘッダーに追加する必要があります。

例えば、GraphQL Authorization Headerは次のようになります。

```xml
Authorization: Bearer <access_token>
```

## 権限の要件{#permission-requirements}

アクセストークンを使用して行われたすべてのリクエストは、実際には、トークン&#x200B;*を生成したユーザーアカウントによって*&#x200B;行われます。

つまり、GraphQLクエリを実行するために必要な権限がアカウントにあることを確認する必要があります。

これは、ローカルインスタンスでGraphiciQLを使用して確認できます。
