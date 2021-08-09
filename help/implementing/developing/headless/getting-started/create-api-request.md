---
title: コンテンツフラグメントへのアクセスとヘッドレス配信クイック開始ガイド
description: AEM Assets REST API を使用して、コンテンツフラグメントと、コンテンツフラグメントコンテンツのヘッドレス配信用の GraphQL API を管理する方法について説明します。
exl-id: 2b72f222-2ba5-4a21-86e4-40c763679c32
source-git-commit: 90de3cf9bf1c949667f4de109d0b517c6be22184
workflow-type: ht
source-wordcount: '510'
ht-degree: 100%

---

# コンテンツフラグメントへのアクセスとヘッドレス配信クイック開始ガイド {#accessing-delivering-content-fragments}

AEM Assets REST API を使用して、コンテンツフラグメントと、コンテンツフラグメントコンテンツのヘッドレス配信用の GraphQL API を管理する方法について説明します。

## GraphQL API と Assets REST API とは何ですか {#what-are-the-apis}

[コンテンツフラグメントはいくつか作成したので、AEM API](create-content-fragment.md) を使用してそれらをヘッドレスで配信できます。

* [GraphQL](/help/assets/content-fragments/graphql-api-content-fragments.md) API を使用すると、コンテンツフラグメントにアクセスして配信するリクエストを作成できます。
* [アセット REST API](/help/assets/content-fragments/assets-api-content-fragments.md) を使用すると、コンテンツフラグメント（およびその他のアセット）を作成および変更できます。

このガイドの残りの部分では、GraphQL へのアクセスとコンテンツフラグメントの配信について説明します。

## GraphQL を使用したコンテンツフラグメントの配信方法 {#how-to-deliver-a-content-fragment}

情報アーキテクトは、コンテンツを配信するために、チャネルエンドポイント用のクエリを設計する必要があります。一般に、これらのクエリは、モデルやエンドポイントごとに 1 回だけ作成する必要があります。この「はじめる前に」ガイドの目的上、1 つだけ作成します。

<!-- Not in the UI yet - will need updating when it is -->
<!--
1. Log into AEM as a Cloud Service and from the main menu select **Tools -&gt; Assets -&gt; GraphQL** 
   * Alternatively open the page directly at `https://<host>:<port>/content/graphiql.html`.
-->

1. AEM as a Cloud Service にログインし、GraphiQL インターフェイスにアクセスします。
   * 例：`https://<host>:<port>/content/graphiql.html`

1. GraphiQL は、GraphQL のブラウザー内のクエリエディターです。クエリを構築して、コンテンツフラグメントを取得し、それらを JSON としてヘッドレスに配信できます。
   * 左側のパネルでは、クエリを作成できます。
   * 右側のパネルに結果が表示されます。
   * クエリエディターは、コード補完機能とホットキーを備えており、クエリを簡単に実行できます。
      ![GraphiQL エディター](../assets/graphiql.png)

1. 作成したモデルが `person` で `firstName`、`lastName`、`position` の各フィールドを持つ場合は、単純なクエリを構築して、コンテンツフラグメントのコンテンツを取得できます。

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

1. ページの右上にある&#x200B;**ドキュメント**リンクをクリックすると、文脈依存ドキュメントが表示され、独自のモデルに適合するクエリの構築に役立ちます。
   ![GraphiQL ドキュメント](../assets/graphiql-documentation.png)

GraphQL を使用すると、特定のデータセットや個々のデータオブジェクトだけでなく、オブジェクトの特定の要素、ネストされた結果、クエリ変数のオファーサポートなどをターゲットできる構造化クエリが可能です。

GraphQL では、反復的な API リクエストと過剰な配信を回避でき、代わりに単一の API クエリに対するレンダリングに必要なものを一括配信できます。結果の JSON を使用して、他のサイトやアプリにデータを配信できます。

## 次の手順 {#next-steps}

これで作業は完了です。AEM のヘッドレスコンテンツ管理に関する基本的な内容を説明しました。もちろん、利用可能な機能の包括的な理解を深めるためのリソースは他にもたくさんあります。 

* **設定ブラウザー** - AEM 設定ブラウザーの詳細
* **[コンテンツフラグメント](/help/assets/content-fragments/content-fragments.md)** - コンテンツフラグメントの作成と管理に関する詳細
* **[AEM Assets HTTP API でサポートされるコンテンツフラグメント](/help/assets/content-fragments/assets-api-content-fragments.md)** - CRUD 操作（作成、読み取り、更新、削除）を介して HTTP API 経由で直接 AEM コンテンツにアクセスする方法の詳細
* **[GraphQL API](/help/assets/content-fragments/graphql-api-content-fragments.md)** - コンテンツフラグメントをヘッドレスで配信する方法の詳細
