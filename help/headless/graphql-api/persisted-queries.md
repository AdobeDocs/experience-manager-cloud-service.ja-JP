---
title: 永続的な GraphQL クエリ
description: Adobe Experience Managerで GraphQL クエリを保持してパフォーマンスを最適化する方法を説明します。 永続化されたクエリは、HTTPGETメソッドを使用してクライアントアプリケーションからリクエストでき、応答を Dispatcher および CDN レイヤーにキャッシュでき、最終的にクライアントアプリケーションのパフォーマンスが向上します。
feature: Content Fragments,GraphQL API
exl-id: 080c0838-8504-47a9-a2a2-d12eadfea4c0
source-git-commit: 940a01cd3b9e4804bfab1a5970699271f624f087
workflow-type: tm+mt
source-wordcount: '644'
ht-degree: 58%

---

# 永続的な GraphQL クエリ {#persisted-queries-caching}

永続クエリは、AEMサーバーで作成および保存される GraphQL クエリです。 標準の GraphQL クエリは、POSTリクエストを使用して実行され、応答を簡単にキャッシュすることはできません。 永続化されたクエリは、クライアントアプリケーションによるGETリクエストでリクエストできます。 GETリクエストの応答は、Dispatcher および CDN レイヤーでキャッシュできるので、最終的には、要求元のクライアントアプリケーションのパフォーマンスが向上します。

持続的なクエリでは、常に[適切な Sites 設定](graphql-endpoint.md)に関連するエンドポイントを使用する必要があるため、次のどちらかまたは両方を使用できます。

* グローバル設定とエンドポイント：
クエリは、すべてのコンテンツフラグメントモデルにアクセスできます。
* 特定の Sites 設定およびエンドポイント：
特定の Sites 設定用の永続クエリを作成するには、対応する Sites 設定固有のエンドポイント（関連するコンテンツフラグメントモデルへのアクセスを提供）が必要です。例えば、WKND Sites 設定専用の永続クエリを作成するには、対応する WKND 固有の Sites 設定と、WKND 固有のエンドポイントを事前に作成する必要があります。

>[!NOTE]
>
>詳しくは、[設定ブラウザーでのコンテンツフラグメント機能の有効化](/help/assets/content-fragments/content-fragments-configuration-browser.md#enable-content-fragment-functionality-in-configuration-browser)を参照してください。
>
>適切な Sites 設定では、**GraphQL Persistence Queries** を有効にする必要があります。

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

## GraphQL クエリを保持する方法

最初にAEMオーサー環境に対するクエリを保持し、次にその環境に対するクエリを保持することをお勧めします [クエリを公開](#publish-persisted-query) をAEMパブリッシュ環境に追加します。 次のようなツール： [Postman](https://www.postman.com/) またはコマンドラインツール [curl](https://curl.se/) を使用できます。

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

## 永続的なクエリの公開 {#publish-persisted-query}

永続化されたクエリは、AEM パブリッシュ環境に公開し、クライアントアプリケーションからリクエストできます。 パブリッシュで永続化されたクエリを使用するには、関連する永続ツリーをレプリケートする必要があります。

永続化されたクエリを公開する方法はいくつかあります。

* **レプリケーション用のPOSTの使用**:

   ```xml
   $ curl -X POST   http://localhost:4502/bin/replicate.json \
   -H 'authorization: Basic YWRtaW46YWRtaW4=' \
   -F path=/conf/wknd/settings/graphql/persistentQueries/plain-article-query \
   -F cmd=activate
   ```

* **パッケージの使用**:
   1. 新しいパッケージ定義を作成します。
   1. 設定（例：`/conf/wknd/settings/graphql/persistentQueries`）を含めます。
   1. パッケージをビルドします。
   1. パッケージをレプリケートします。

* **レプリケーション/配布ツールの使用**:
   1. 配布ツールに移動します。
   1. 設定のツリーアクティベーション（例：`/conf/wknd/settings/graphql/persistentQueries`）を選択します。

* **ワークフローの使用（ワークフローランチャー設定を使用）**:
   1. 様々なイベント（例：作成、変更など）で設定をレプリケートするワークフローモデルを実行するためのワークフローランチャールールを定義します。

クエリ設定が公開されると、同じ認証原則が適用され、公開エンドポイントを使用するだけです。

>[!NOTE]
>
>匿名アクセスの場合は、ACL で「全員」にクエリ設定へのアクセスが許可されているとシステムが想定します。
>
>そうでない場合は、実行できなくなります。

>[!NOTE]
>
>URL 内のセミコロン（「;」）はすべてエンコードする必要があります。
>
>例えば、永続的クエリを実行するリクエストの場合と同様に、次のようにします。
>
>
```xml
>curl -X GET \ "http://localhost:4502/graphql/execute.json/wknd/plain-article-query-parameters%3bapath=%2fcontent2fdam2fwknd2fen2fmagazine2falaska-adventure2falaskan-adventures;withReference=false"
>```
