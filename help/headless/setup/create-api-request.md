---
title: API リクエストの作成 - ヘッドレス設定
description: コンテンツフラグメントコンテンツと AEM Assets REST API のヘッドレス配信に GraphQL API を使用して、コンテンツフラグメントを管理する方法を説明します。
exl-id: 2b72f222-2ba5-4a21-86e4-40c763679c32
feature: Headless, Content Fragments,GraphQL API
role: Admin, Developer
source-git-commit: 10580c1b045c86d76ab2b871ca3c0b7de6683044
workflow-type: tm+mt
source-wordcount: '677'
ht-degree: 97%

---

# API リクエストの作成 - ヘッドレス設定 {#accessing-delivering-content-fragments}

コンテンツフラグメントコンテンツと AEM Assets REST API のヘッドレス配信に GraphQL API を使用して、コンテンツフラグメントを管理する方法を説明します。

## GraphQL API と Assets REST API とは {#what-are-the-apis}

[ コンテンツフラグメントはいくつか作成したので ](create-content-fragment.md)、AEM API を使用してそれらをヘッドレスで配信できます。

* [GraphQL](/help/headless/graphql-api/content-fragments.md) API を使用すると、コンテンツフラグメントにアクセスして配信するリクエストを作成できます。この API は、コンテンツフラグメントコンテンツのクエリと使用に最も堅牢な機能セットを提供します。
   * API を使用するには、[エンドポイントを AEM で定義して有効にし](/help/headless/graphql-api/graphql-endpoint.md)、必要に応じて [GraphiQL インターフェイスをインストール](/help/headless/graphql-api/graphiql-ide.md)します。
* [アセット REST API](/help/assets/content-fragments/assets-api-content-fragments.md) を使用すると、コンテンツフラグメント（およびその他のアセット）を作成および変更できます。

>[!NOTE]
>
>[コンテンツフラグメントおよびコンテンツフラグメントモデルの OpenAPI](/help/headless/content-fragment-openapis.md) も利用できます。

このガイドの残りの部分では、GraphQL へのアクセスとコンテンツフラグメントの配信について説明します。

## GraphQL エンドポイントの有効化 {#enable-graphql-endpoint}

GraphQL API を使用する前に、GraphQL エンドポイントを作成する必要があります。

1. **ツール**／**一般** に移動し、「**GraphQL**」を選択します。
1. 「**作成**」を選択します。
1. **新しい GraphQL エンドポイントを作成**&#x200B;ダイアログボックスが開きます。以下を指定します。
   * **名前**：エンドポイントの名前。任意のテキストを入力できます。
   * **使用する GraphQL スキーマの提供元**：ドロップダウンリストを使用して、必要な設定を選択します。
1. 「**作成**」で確定します。
1. コンソールで、前に作成した設定に基づいて、**パス**&#x200B;が表示されます。このパスを使用して、GraphQLクエリを実行します。

   ```
   /content/cq:graphql/<configuration-name>/endpoint
   ```

GraphQL エンドポイントを有効にする方法について詳しくは、[AEM の GraphQL エンドポイントを管理](/help/headless/graphql-api/graphql-endpoint.md)を参照してください。

## GraphQL と GraphiQL を使用したクエリコンテンツ

情報アーキテクトは、チャネルエンドポイントがコンテンツを配信するためのクエリを設計します。これらのクエリは、エンドポイントごと、モデルごとに 1 回だけ検討してください。この入門ガイドでは、作成する必要があるのは 1 つだけです。

GraphiQL は IDE であり、AEM 環境に含まれています。[エンドポイントを設定](#enable-graphql-endpoint)した後、アクセス可能になり表示されます。

1. AEM as a Cloud Service にログインし、GraphiQL インターフェイスにアクセスします。

   クエリエディターには、次のいずれかの方法でアクセスできます。

   * **ツール**／**一般**／**GraphQL クエリエディター**
   * 直接アクセス（例：`http://localhost:4502/aem/graphiql.html`）

1. GraphiQL は、GraphQL のブラウザー内のクエリエディターです。クエリを作成して、コンテンツフラグメントを取得し、それらを JSON としてヘッドレスに配信できます。
   * ドロップダウンの右上を使用すると、エンドポイントを選択できます。
   * 左端のパネルには、永続クエリが表示されます（使用可能な場合）。
   * 左中央のパネルでは、クエリを作成できます。
   * 右中央のパネルには、結果が表示されます。
   * クエリエディターは、コード補完機能とホットキーを備えており、クエリを簡単に実行できます。

   ![GraphiQL エディター](../assets/graphiql.png)

1. 作成したモデルが `person` で `firstName`、`lastName`、`position` の各フィールドを持つ場合は、単純なクエリーを構築して、コンテンツフラグメントのコンテンツを取得できます。

   ```text
   query 
   {
     personList {
       items {
         _path
         firstName
         lastName
         position
       }
     }
   }
   ```

1. 左パネルにクエリを入力します。
   ![GraphiQL クエリ](../assets/graphiql-query.png)

1. 「**クエリを実行**」ボタンをクリックするか `Ctrl-Enter` ホットキーを使用すると、結果が JSON として右側のパネルに表示されます。
   ![GraphiQL の結果](../assets/graphiql-results.png)

1. ページの右上隅にある&#x200B;**ドキュメント**リンクをクリックすると、コンテキスト内のドキュメントが表示され、独自のモデルに適応するクエリを作成できます。
   ![GraphiQL ドキュメント](../assets/graphiql-documentation.png)

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
