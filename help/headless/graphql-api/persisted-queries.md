---
title: 永続的な GraphQL クエリ
description: Adobe Experience Manager as a Cloud Serviceで GraphQL クエリを保持してパフォーマンスを最適化する方法を説明します。 永続化されたクエリは、HTTPGETメソッドを使用してクライアントアプリケーションからリクエストでき、応答を Dispatcher および CDN レイヤーにキャッシュでき、最終的にクライアントアプリケーションのパフォーマンスが向上します。
feature: Content Fragments,GraphQL API
exl-id: 080c0838-8504-47a9-a2a2-d12eadfea4c0
source-git-commit: dfcad7aab9dda7341de3dc4975eaba9bdfbd9780
workflow-type: tm+mt
source-wordcount: '768'
ht-degree: 41%

---

# 永続的な GraphQL クエリ {#persisted-queries-caching}

永続的なクエリは、Adobe Experience Manager(AEM)as a Cloud Serviceサーバーで作成および保存される GraphQL クエリです。 クライアントアプリケーションは、GETリクエストを使用してリクエストできます。 GETリクエストの応答は、Dispatcher および CDN レイヤーでキャッシュできるので、最終的には、要求元のクライアントアプリケーションのパフォーマンスが向上します。 これは、標準の GraphQL クエリとは異なります。標準クエリは、応答を簡単にキャッシュできないPOSTリクエストを使用して実行されます。

この [GraphiQL IDE](/help/headless/graphql-api/graphiql-ide.md) はAEMで使用できます ( デフォルトでは `dev-author`) を使用して、GraphQL クエリを開発、テスト、永続化します ( [実稼動環境への移行](#transfer-persisted-query-production). カスタマイズが必要な場合 ( 例： [キャッシュのカスタマイズ](/help/headless/graphql-api/graphiql-ide.md#caching-persisted-queries)) を使用すると、API を使用できます。次に示す curl の例を参照してください： [GraphQL クエリを保持する方法](#how-to-persist-query).

## 永続的なクエリとエンドポイント {#persisted-queries-and-endpoints}

持続的なクエリでは、常に[適切な Sites 設定](graphql-endpoint.md)に関連するエンドポイントを使用する必要があるため、次のどちらかまたは両方を使用できます。

* グローバル設定とエンドポイント：
クエリは、すべてのコンテンツフラグメントモデルにアクセスできます。
* 特定の Sites 設定およびエンドポイント：
特定の Sites 設定用の永続クエリを作成するには、対応する Sites 設定固有のエンドポイント（関連するコンテンツフラグメントモデルへのアクセスを提供）が必要です。例えば、WKND Sites 設定専用の永続クエリを作成するには、対応する WKND 固有の Sites 設定と、WKND 固有のエンドポイントを事前に作成する必要があります。

>[!NOTE]
>
>詳しくは、[設定ブラウザーでのコンテンツフラグメント機能の有効化](/help/assets/content-fragments/content-fragments-configuration-browser.md#enable-content-fragment-functionality-in-configuration-browser)を参照してください。
>
>この **GraphQL 永続的なクエリ** 適切な Sites 設定に対して有効にする必要があります。

例えば、`my-query` という特定のクエリがあり、このクエリが Sites 設定 `my-conf` のモデル `my-model` を使用する場合は、次のようになります。

* 特定エンドポイント `my-conf` を使用してクエリを作成すると、クエリは次のように保存されます。
   `/conf/my-conf/settings/graphql/persistentQueries/my-query`
* `global` エンドポイントを使用して同じクエリを作成できますが、クエリは次のように保存されます。
   `/conf/global/settings/graphql/persistentQueries/my-query`

>[!NOTE]
>
>これらは 2 つの異なるクエリで、異なるパスに保存されます。
>
>同じモデルを使用していますが、異なるエンドポイントを介しています。

## GraphQL クエリを保持する方法 {#how-to-persist-query}

最初にAEMオーサー環境に対するクエリを保持し、次にその環境に対するクエリを保持することをお勧めします [クエリを転送](#transfer-persisted-query-production) を実稼動AEMパブリッシュ環境に追加します。

クエリを保持するには、次のような様々な方法があります。

* GraphiQL IDE — を参照してください。 [永続クエリの保存](/help/headless/graphql-api/graphiql-ide.md##saving-persisted-queries)
* curl — 次の例を参照してください。
* その他のツール ( [Postman](https://www.postman.com/)

次に、 **curl** コマンドラインツール：

1. 新しいエンドポイント URL `/graphql/persist.json/<config>/<persisted-label>` に PUT してクエリを準備します。

   例えば、次のようにして、永続的クエリを作成します。

   ```xml
   $ curl -X PUT \
       -H 'authorization: Basic YWRtaW46YWRtaW4=' \
       -H "Content-Type: application/json" \
       "http://localhost:4502/graphql/persist.json/wknd/plain-article-query" \
       -d \
   '{
     articleList {
       items{
           _path
           author
           main {
               json
           }
       }
     }
   }'
   ```

1. この段階で、応答を確認します。

   例えば、以下が成功するかどうかを確認します。

   ```xml
   {
     "action": "create",
     "configurationName": "wknd",
     "name": "plain-article-query",
     "shortPath": "/wknd/plain-article-query",
     "path": "/conf/wknd/settings/graphql/persistentQueries/plain-article-query"
   }
   ```

1. その後、URL を取得して、永続化されたクエリをリクエストできます `/graphql/execute.json/<shortPath>`.

   例えば、次のような永続的クエリを使用します。

   ```xml
   $ curl -X GET \
       http://localhost:4502/graphql/execute.json/wknd/plain-article-query
   ```

1. 既存のクエリパスに POST して、永続的クエリを更新します。

   例えば、次のような永続的クエリを使用します。

   ```xml
   $ curl -X POST \
       -H 'authorization: Basic YWRtaW46YWRtaW4=' \
       -H "Content-Type: application/json" \
       "http://localhost:4502/graphql/persist.json/wknd/plain-article-query" \
       -d \
   '{
     articleList {
       items{
           _path
           author
           main {
               json
           }
         referencearticle {
           _path
         }
       }
     }
   }'
   ```

1. ラップされたプレーンクエリを作成します。

   次に例を示します。

   ```xml
   $ curl -X PUT \
       -H 'authorization: Basic YWRtaW46YWRtaW4=' \
       -H "Content-Type: application/json" \
       "http://localhost:4502/graphql/persist.json/wknd/plain-article-query-wrapped" \
       -d \
   '{ "query": "{articleList { items { _path author main { json } referencearticle { _path } } } }"}'
   ```

1. キャッシュコントロール付きのラップされたプレーンクエリを作成します。

   次に例を示します。

   ```xml
   $ curl -X PUT \
       -H 'authorization: Basic YWRtaW46YWRtaW4=' \
       -H "Content-Type: application/json" \
       "http://localhost:4502/graphql/persist.json/wknd/plain-article-query-max-age" \
       -d \
   '{ "query": "{articleList { items { _path author main { json } referencearticle { _path } } } }", "cache-control": { "max-age": 300 }}'
   ```

1. パラメーター付きの永続的クエリを作成します。

   次に例を示します。

   ```xml
   $ curl -X PUT \
       -H 'authorization: Basic YWRtaW46YWRtaW4=' \
       -H "Content-Type: application/json" \
       "http://localhost:4502/graphql/persist.json/wknd/plain-article-query-parameters" \
       -d \
   'query GetAsGraphqlModelTestByPath($apath: String!, $withReference: Boolean = true) {
     articleByPath(_path: $apath) {
       item {
         _path
           author
           main {
           plaintext
           }
           referencearticle @include(if: $withReference) {
           _path
           }
         }
       }
     }'
   ```

1. パラメーター付きのクエリを実行します。

   次に例を示します。

   ```xml
   $ curl -X POST \
       -H 'authorization: Basic YWRtaW46YWRtaW4=' \
       -H "Content-Type: application/json" \
       "http://localhost:4502/graphql/execute.json/wknd/plain-article-query-parameters;apath=%2fcontent2fdam2fwknd2fen2fmagazine2falaska-adventure2falaskan-adventures;withReference=false"
   
   $ curl -X GET \
       "http://localhost:4502/graphql/execute.json/wknd/plain-article-query-parameters;apath=%2fcontent2fdam2fwknd2fen2fmagazine2falaska-adventure2falaskan-adventures;withReference=false"
   ```

## 実稼動環境への永続的なクエリの転送  {#transfer-persisted-query-production}

最終的に、持続的なクエリは、(AEMas a Cloud Serviceの ) 実稼動パブリッシュ環境上に存在し、クライアントアプリケーションからリクエストできる必要があります。 実稼動パブリッシュ環境で永続化クエリを使用するには、関連する永続ツリーをレプリケートする必要があります。

* 最初は、実稼動作成者に対して、新しく作成したコンテンツをクエリで検証するために、
* 最後に実稼動版の公開をライブ消費に

永続化されたクエリを転送するには、いくつかの方法があります。

1. パッケージを使用する場合：
   1. 新しいパッケージ定義を作成します。
   1. 設定（例：`/conf/wknd/settings/graphql/persistentQueries`）を含めます。
   1. パッケージをビルドします。
   1. パッケージを転送します（ダウンロード/アップロードまたはレプリケート）。
   1. パッケージをインストールします。

1. レプリケーションに POST を使用する場合：

   ```xml
   $ curl -X POST   http://localhost:4502/bin/replicate.json \
   -H 'authorization: Basic YWRtaW46YWRtaW4=' \
   -F path=/conf/wknd/settings/graphql/persistentQueries/plain-article-query \
   -F cmd=activate
   ```

<!--
1. Using replication/distribution tool:
   1. Go to the Distribution tool.
   1. Select tree activation for the configuration (for example, `/conf/wknd/settings/graphql/persistentQueries`).

* Using a workflow (via workflow launcher configuration):
  1. Define a workflow launcher rule for executing a workflow model that would replicate the configuration on different events (for example, create, modify, amongst others).
-->

実稼動環境のパブリッシュ環境でクエリを設定すると、同じ認証原則が適用され、パブリッシュエンドポイントを使用するだけです。

>[!NOTE]
>
>匿名アクセスの場合は、ACL で「全員」にクエリ設定へのアクセスが許可されているとシステムが想定します。
>
>そうでない場合は、実行できなくなります。

## アプリで使用するクエリ URL のエンコード {#encoding-query-url}

アプリケーションで使用する場合は、URL 内のセミコロン (&quot;;&quot;) をエンコードする必要があります。

例えば、永続的クエリを実行するリクエストの場合と同様に、次のようにします。

```xml
curl -X GET \ "http://localhost:4502/graphql/execute.json/wknd/plain-article-query-parameters%3bapath=%2fcontent2fdam2fwknd2fen2fmagazine2falaska-adventure2falaskan-adventures;withReference=false"
```

クライアントアプリで永続化されたクエリを使用するには、AEMヘッドレスクライアント SDK を使用する必要があります [JavaScript 用AEMヘッドレスクライアント](https://github.com/adobe/aem-headless-client-js).