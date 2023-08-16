---
title: API リクエストの作成 - ヘッドレス設定
description: コンテンツフラグメントコンテンツと AEM Assets REST API のヘッドレス配信に GraphQL API を使用して、コンテンツフラグメントを管理する方法を説明します。
exl-id: 2b72f222-2ba5-4a21-86e4-40c763679c32
source-git-commit: 5ad33f0173afd68d8868b088ff5e20fc9f58ad5a
workflow-type: tm+mt
source-wordcount: '651'
ht-degree: 58%

---

# API リクエストの作成 - ヘッドレス設定 {#accessing-delivering-content-fragments}

コンテンツフラグメントコンテンツと AEM Assets REST API のヘッドレス配信に GraphQL API を使用して、コンテンツフラグメントを管理する方法を説明します。

## GraphQL API と Assets REST API とは {#what-are-the-apis}

[コンテンツフラグメントはいくつか作成したので、AEM API](create-content-fragment.md) を使用してそれらをヘッドレスで配信できます。

* [GraphQL API](/help/headless/graphql-api/content-fragments.md) では、コンテンツフラグメントにアクセスして配信するリクエストを作成できます。 この API は、コンテンツフラグメントコンテンツのクエリと使用に最も堅牢な機能セットを提供します。
   * API を使用するには、 [AEMのエンドポイントの定義と有効化](/help/headless/graphql-api/graphql-endpoint.md)（必要に応じて） [GraphiQL インターフェイスがインストールされています](/help/headless/graphql-api/graphiql-ide.md).
* [Assets REST API](/help/assets/content-fragments/assets-api-content-fragments.md) では、コンテンツフラグメント（およびその他のアセット）を作成および変更できます。

このガイドでは、GraphQLへのアクセスとコンテンツフラグメントの配信について説明します。

## GraphQL エンドポイントの有効化 {#enable-graphql-endpoint}

GraphQL API を使用する前に、GraphQL エンドポイントを作成する必要があります。

1. **ツール**／**一般** に移動し、「**GraphQL**」を選択します。
1. 「**作成**」を選択します。
1. The **新しいGraphQLエンドポイントを作成** ダイアログボックスが開きます。 以下を指定します。
   * **名前**：エンドポイントの名前。任意のテキストを入力できます。
   * **使用する GraphQL スキーマの提供元**：ドロップダウンを使用して、必要な設定を選択します。
1. 「**作成**」で確定します。
1. コンソールで、 **パス** は、前に作成した設定に基づいて表示されます。 このパスは、GraphQLクエリを実行するために使用されます。

   ```
   /content/cq:graphql/<configuration-name>/endpoint
   ```

[GraphQL エンドポイントの有効化について詳しくは、こちらを参照してください](/help/headless/graphql-api/graphql-endpoint.md)。

## GraphQL と GraphiQL を使用したクエリコンテンツ

情報アーキテクトは、チャネルエンドポイントがコンテンツを配信するためのクエリを設計します。 これらのクエリは、エンドポイントごと、モデルごとに 1 回だけ考慮します。 この入門ガイドでは、作成する必要があるのは 1 つだけです。

GraphiQL は IDE であり、AEM 環境に含まれています。[エンドポイントを設定](#enable-graphql-endpoint)した後、アクセス可能になり表示されます。

1. AEM as a Cloud Service にログインし、GraphiQL インターフェイスにアクセスします。

   クエリエディターには、次のいずれかの方法でアクセスできます。

   * **ツール**／**一般**／**GraphQL クエリエディター**
   * 直接アクセス（例：`http://localhost:4502/aem/graphiql.html`）

1. GraphiQL は、GraphQL のブラウザー内のクエリエディターです。クエリを作成して、コンテンツフラグメントを取得し、それらを JSON としてヘッドレスに配信できます。
   * 右上のドロップダウンで、エンドポイントを選択できます。
   * 左端のパネルには、永続クエリが表示されます（使用可能な場合）。
   * 中央の左側のパネルを使用して、クエリを作成できます。
   * 右中央のパネルには、結果が表示されます。
   * クエリエディターは、コード補完機能とホットキーを備えており、クエリを簡単に実行できます。

   ![GraphiQL エディター](../assets/graphiql.png)

1. 作成したモデルの名前が `person` フィールド `firstName`, `lastName`、および `position`を使用すると、単純なクエリを作成して、コンテンツフラグメントのコンテンツを取得できます。

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

1. 左側のパネルにクエリを入力します。
   ![GraphiQL クエリ](../assets/graphiql-query.png)

1. 「**クエリを実行**」ボタンをクリックするか `Ctrl-Enter` ホットキーを使用すると、結果が JSON として右側のパネルに表示されます。
   ![GraphiQL の結果](../assets/graphiql-results.png)

1. ページの右上隅で、 **ドキュメント** コンテキスト内ドキュメントを表示するリンクを追加しました。
   ![GraphiQL ドキュメント](../assets/graphiql-documentation.png)

GraphQLを使用すると、特定のデータセットや個々のデータオブジェクトをターゲットにするだけでなく、オブジェクトの特定の要素やネストされた結果を配信したり、クエリ変数をサポートしたりできる構造化クエリが可能になります。

GraphQLでは、繰り返しの API リクエストや過度の配信を避けることができ、代わりに、1 つの API クエリへの応答としてレンダリングに必要なものを一括配信できます。 結果の JSON を使用して、他のサイトやアプリにデータを配信できます。

## 次の手順 {#next-steps}

これで作業は完了です。AEM のヘッドレスコンテンツ管理に関する基本的な内容を説明しました。使用可能な機能を包括的に理解するために、さらに多くのリソースを使用して、さらに深く掘り下げることができます。

* **[コンテンツフラグメント](/help/sites-cloud/administering/content-fragments/content-fragments.md)** - コンテンツフラグメントの作成と管理に関する詳細
* **[AEM Assets HTTP API でサポートされるコンテンツフラグメント](/help/assets/content-fragments/assets-api-content-fragments.md)** - CRUD 操作（作成、読み取り、更新、削除）を介して HTTP API 経由で直接 AEM コンテンツにアクセスする方法の詳細
* **[GraphQL API](/help/headless/graphql-api/content-fragments.md)** - コンテンツフラグメントをヘッドレスで配信する方法の詳細
