---
title: コンテンツフラグメントへのアクセスと配信ヘッドレスクイック開始ガイド
description: アセットREST APIを使用すると、コンテンツフラグメントを管理でき、GraphQL APIを使用すると、ヘッドレスで簡単にコンテンツフラグメントコンテンツを配信できます。
translation-type: tm+mt
source-git-commit: 259d54a225f8dee5929f62b784e28f3fc2bb794a
workflow-type: tm+mt
source-wordcount: '512'
ht-degree: 0%

---


# コンテンツフラグメントへのアクセスと配信ヘッドレスクイック開始ガイド{#accessing-delivering-content-fragments}

アセットREST APIを使用すると、コンテンツフラグメントを管理でき、GraphQL APIを使用すると、ヘッドレスで簡単にコンテンツフラグメントコンテンツを配信できます。

## GraphQLとAssets REST APIとは何ですか。{#what-are-the-apis}

[コンテンツフラグメントを作成したので、AEM API](create-content-fragment.md) を使用してそれらを無理に配信できます。

* [GraphQL ](/help/assets/content-fragments/graphql-api-content-fragments.md) APIを使用すると、コンテンツフラグメントにアクセスして配信するリクエストを作成できます。
* [アセットREST ](/help/assets/content-fragments/assets-api-content-fragments.md) APIを使用すると、コンテンツフラグメント（およびその他のアセット）を作成および変更できます。

このガイドの残りの部分では、GraphQLへのアクセスとコンテンツフラグメントの配信について説明します。

## GraphQL {#how-to-deliver-a-content-fragment}を使用したコンテンツフラグメントの配信方法

情報アーキテクトは、コンテンツを配信するために、チャネルエンドポイント用のクエリを設計する必要があります。 一般に、これらのクエリは、モデルごとにエンドポイントごとに1回だけ考慮する必要があります。 この入門ガイドの目的上、必要な作業は1つだけです。

1. AEMにCloud Serviceとしてログインし、メインメニューで&#x200B;**ツール/アセット —> GraphQL**&#x200B;を選択します。
   * または、`https://<host>:<port>/content/graphiql.html`で直接ページを開きます。

1. GraphiQLは、GraphQLのブラウザ内クエリエディタです。 クエリを構築して、コンテンツフラグメントを取得し、それらをJSONとして直接配信できます。
   * 左側のパネルでは、クエリを作成できます。
   * 右側のパネルに結果が表示されます。
   * クエリエディタは、コード補完機能とホットキーを備えており、クエリを簡単に実行できます。
      ![GraphiQLエディタ](../assets/graphiql.png)

1. 作成したモデルが`firstName`、`lastName`、`position`の各フィールドを持つ`person`と呼ばれている場合は、単純なクエリを構築して、コンテンツフラグメントのコンテンツを取得できます。

   ```text
   query {
     persons {
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
   ![GraphiQLクエリ](../assets/graphiql-query.png)

1. 「**クエリを実行**」ボタンをクリックするか、`Ctrl-Enter`ホットキーを使用すると、結果がJSONとして右側のパネルに表示されます。
   ![GraphiQLの結果](../assets/graphiql-results.png)

1. ページの右上にある&#x200B;**ドキュメント**リンクをクリックすると、文脈依存ドキュメントが表示され、独自のモデルに適合するクエリの構築に役立ちます。
   ![GraphiQLドキュメント](../assets/graphiql-documentation.png)

GraphQLを使用すると、特定のデータセットや個々のデータオブジェクトだけでなく、オブジェクトの特定の要素、ネストされた結果、クエリ変数のオファーサポートなどをターゲットできる構造化クエリが可能です。

GraphQLでは、反復的なAPIリクエストと過剰な配信を回避でき、代わりに単一のAPIクエリに対するレンダリングに必要なものを一括配信できます。 結果のJSONを使用して、他のサイトやアプリにデータを配信できます。

## 次の手順 {#next-steps}

これで作業は完了です。これで、AEMのヘッドレスコンテンツ管理に関する基本的な理解が得られます。 もちろん、利用可能な機能の包括的な理解を深めるためのリソースは他にもたくさんあります。

* **設定ブラウザ** - AEM設定ブラウザの詳細
* **[コンテンツフラグメント](/help/assets/content-fragments/content-fragments.md)**  — コンテンツフラグメントの作成と管理に関する詳細
* **[AEM AssetsHTTP APIでサポートされるコンテンツフラグメント](/help/assets/content-fragments/assets-api-content-fragments.md)** - CRUD操作（作成、読み取り、更新、削除）を介してHTTP API経由で直接AEMコンテンツにアクセスする方法の詳細
* **[GraphQL API](/help/assets/content-fragments/graphql-api-content-fragments.md)**  — コンテンツフラグメントを無理に配信する方法の詳細
