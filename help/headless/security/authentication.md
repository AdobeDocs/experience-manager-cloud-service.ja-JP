---
title: コンテンツフラグメントに対するリモート AEM GraphQL クエリの認証
description: ヘッドレスコンテンツ配信を保護するために、Adobe Experience Manager GraphQL のリモートクエリに必要な認証について説明します。
feature: Headless, Content Fragments,GraphQL API
exl-id: dfeae661-06a1-4001-af24-b52ae12d625f
role: Admin, Developer
source-git-commit: 6719e0bcaa175081faa8ddf6803314bc478099d7
workflow-type: tm+mt
source-wordcount: '231'
ht-degree: 96%

---

# コンテンツフラグメントに対するリモート AEM GraphQL クエリの認証 {#authentication-for-remote-aem-graphql-queries-on-content-fragments}

[コンテンツフラグメント配信用の Adobe Experience Manager as a Cloud Service（AEM）GraphQL API](/help/headless/graphql-api/content-fragments.md) の主な使用例は、サードパーティのアプリケーションやサービスからリモートクエリを受け入れることです。ヘッドレスコンテンツ配信を保護するために、これらのリモートクエリには、認証済み API アクセスが必要な場合があります。

>[!NOTE]
>
>テストおよび開発の場合は、[GraphiQL インターフェイス](/help/headless/graphql-api/graphiql-ide.md)を使用して AEM GraphQL API に直接アクセスすることもできます。

認証のために、サードパーティのサービスは[アクセストークンを取得](#retrieving-access-token)する必要があります。その後、このトークンは [GraphQL リクエストで使用](#use-access-token-in-graphql-request)できます。

## アクセストークンの取得 {#retrieving-access-token}

詳しくは、[サーバーサイド API のアクセストークンの生成](/help/implementing/developing/introduction/generating-access-tokens-for-server-side-apis.md)を参照してください。

## GraphQL リクエストでのアクセストークンの使用 {#use-access-token-in-graphql-request}

サードパーティのサービスが AEM インスタンスに接続するには、*アクセストークン*&#x200B;が必要です。サービスは次に、このトークンを POST リクエストの `Authorization` ヘッダーに追加する必要があります。

例えば、GraphQL の Authorization ヘッダーは次のようになります。

```xml
Authorization: Bearer <access_token>
```

## 権限の要件 {#permission-requirements}

アクセストークンを使用して行われるすべてのリクエストは、*そのトークンを生成したユーザーアカウントによって*&#x200B;行われます。

つまり、このユーザーアカウントは、そのアカウントに GraphQL クエリの実行に必要な権限があることを確認する必要があります。

これらの権限は、ローカルインスタンスで GraphiQL を使用して確認できます。詳しくは、[ ヘッドレスコンテンツの権限に関する考慮事項 ](/help/headless/security/permissions.md) を参照してください。
