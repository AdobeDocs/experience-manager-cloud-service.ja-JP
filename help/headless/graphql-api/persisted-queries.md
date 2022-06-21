---
title: 永続的な GraphQL クエリ
description: Adobe Experience Manager as a Cloud Serviceで GraphQL クエリを保持してパフォーマンスを最適化する方法を説明します。 クライアントアプリケーションで HTTP GET メソッドを使用して永続的クエリをリクエストでき、応答を Dispatcher および CDN レイヤーにキャッシュできるので、最終的にクライアントアプリケーションのパフォーマンスが向上します。
feature: Content Fragments,GraphQL API
exl-id: 080c0838-8504-47a9-a2a2-d12eadfea4c0
source-git-commit: 6529b4b874cd7d284b92546996e2373e59075dfd
workflow-type: tm+mt
source-wordcount: '1109'
ht-degree: 30%

---

# 永続的な GraphQL クエリ {#persisted-queries-caching}

永続的なクエリは、Adobe Experience Manager(AEM)as a Cloud Serviceサーバーで作成および保存される GraphQL クエリです。 クライアントアプリケーションは、GETリクエストを使用してリクエストできます。 GET リクエストの応答は、Dispatcher および CDN レイヤーでキャッシュできるので、最終的には、要求元のクライアントアプリケーションのパフォーマンスが向上します。これは、標準の GraphQL クエリとは異なります。標準クエリは、応答を簡単にキャッシュできないPOSTリクエストを使用して実行されます。

>[!NOTE]
>
>永続化されたクエリをお勧めします。 詳しくは、 [GraphQL クエリのベストプラクティス (Dispatcher)](/help/headless/graphql-api/content-fragments.md#graphql-query-best-practices) を参照してください。

この [GraphiQL IDE](/help/headless/graphql-api/graphiql-ide.md) は、以前にAEMで GraphQL クエリを開発、テスト、永続化できます。 [実稼動環境への移行](#transfer-persisted-query-production). カスタマイズが必要な場合 ( 例： [キャッシュのカスタマイズ](/help/headless/graphql-api/graphiql-ide.md#caching-persisted-queries)) を使用すると、API を使用できます。次に示す curl の例を参照してください： [GraphQL クエリを保持する方法](#how-to-persist-query).

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

## GraphQL クエリを永続化する方法 {#how-to-persist-query}

最初にAEMオーサー環境に対するクエリを保持し、次にその環境に対するクエリを保持することをお勧めします [クエリを転送](#transfer-persisted-query-production) を実稼動AEMパブリッシュ環境に追加します。

クエリを保持するには、次のような様々な方法があります。

* GraphiQL IDE — を参照してください。 [永続クエリの保存](/help/headless/graphql-api/graphiql-ide.md##saving-persisted-queries) （推奨される方法）
* curl — 次の例を参照してください。
* その他のツール ( [Postman](https://www.postman.com/)

GraphiQL IDE は、 **優先** メソッドを使用してクエリを保持できます。 を使用して特定のクエリを保持するには **curl** コマンドラインツール：

1. 新しいエンドポイント URL `/graphql/persist.json/<config>/<persisted-label>` に PUT してクエリを準備します。

   例えば、次のようにして、永続的クエリを作成します。

   ```shell
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

   ```json
   {
     "action": "create",
     "configurationName": "wknd",
     "name": "plain-article-query",
     "shortPath": "/wknd/plain-article-query",
     "path": "/conf/wknd/settings/graphql/persistentQueries/plain-article-query"
   }
   ```

1. その後、URL `/graphql/execute.json/<shortPath>` を GET して、永続的クエリをリクエストできます。

   例えば、次のような永続的クエリを使用します。

   ```shell
   $ curl -X GET \
       http://localhost:4502/graphql/execute.json/wknd/plain-article-query
   ```

1. 既存のクエリパスに POST して、永続的クエリを更新します。

   例えば、次のような永続的クエリを使用します。

   ```shell
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

   ```shell
   $ curl -X PUT \
       -H 'authorization: Basic YWRtaW46YWRtaW4=' \
       -H "Content-Type: application/json" \
       "http://localhost:4502/graphql/persist.json/wknd/plain-article-query-wrapped" \
       -d \
   '{ "query": "{articleList { items { _path author main { json } referencearticle { _path } } } }"}'
   ```

1. キャッシュコントロール付きのラップされたプレーンクエリを作成します。

   次に例を示します。

   ```shell
   $ curl -X PUT \
       -H 'authorization: Basic YWRtaW46YWRtaW4=' \
       -H "Content-Type: application/json" \
       "http://localhost:4502/graphql/persist.json/wknd/plain-article-query-max-age" \
       -d \
   '{ "query": "{articleList { items { _path author main { json } referencearticle { _path } } } }", "cache-control": { "max-age": 300 }}'
   ```

1. パラメーター付きの永続的クエリを作成します。

   次に例を示します。

   ```shell
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


## 永続化クエリの実行方法 {#execute-persisted-query}

永続化されたクエリを実行するには、クライアントアプリケーションは次の構文を使用してGETリクエストを実行します。

```
GET <AEM_HOST>/graphql/execute.json/<PERSISTENT_PATH>
```

ここで、 `PERSISTENT_PATH` は、永続的なクエリが保存される場所への短縮パスです。

1. 例： `wknd` は設定名で、 `plain-article-query` は、永続クエリの名前です。 クエリを実行するには：

   ```shell
   $ curl -X GET \
       https://publish-p123-e456.adobeaemcloud.com/graphql/execute.json/wknd/plain-article-query
   ```

1. パラメーター付きのクエリを実行します。

   >[!NOTE]
   >
   > クエリ変数と値は正しく設定されている必要があります [エンコード済み](#encoding-query-url) 永続クエリを実行する際。

   次に例を示します。

   ```xml
   $ curl -X GET \
       "https://publish-p123-e456.adobeaemcloud.com/graphql/execute.json/wknd/plain-article-query-parameters%3Bapath%3D%2Fcontent%2Fdam%2Fwknd%2Fen%2Fmagazine%2Falaska-adventure%2Falaskan-adventures%3BwithReference%3Dfalse
   ```

   詳しくは、 [クエリ変数](#query-variables) を参照してください。

## クエリ変数の使用 {#query-variables}

クエリ変数は、永続化クエリで使用できます。 クエリ変数は、セミコロン (`;`) を変数名と値で使用します。 複数の変数はセミコロンで区切られます。

パターンは次のようになります。

```
<AEM_HOST>/graphql/execute.json/<PERSISTENT_QUERY_PATH>;variable1=value1;variable2=value2
```

例えば、次のクエリには変数が含まれています `activity` アクティビティの値に基づいてリストをフィルターするには：

```graphql
query getAdventuresByActivity($activity: String!) {
      adventureList (filter: {
        adventureActivity: {
          _expressions: [
            {
              value: $activity
            }
          ]
        }
      }){
        items {
          _path
        adventureTitle
        adventurePrice
        adventureTripLength
      }
    }
  }
```

このクエリは、パスの下に保持できます `wknd/adventures-by-activity`. 永続化クエリを呼び出すには、次の手順に従います。 `activity=Camping` リクエストは次のようになります。

```
<AEM_HOST>/graphql/execute.json/wknd/adventures-by-activity%3Bactivity%3DCamping
```

注意： `%3B` は、 `;` および `%3D` は `=`. クエリ変数と特殊文字は、次の条件を満たす必要があります。 [適切にエンコード](#encoding-query-url) を実行します。

## アプリで使用するクエリ URL のエンコード {#encoding-query-url}

アプリケーションで使用する場合、クエリ変数を構築する際に使用される特殊文字 ( セミコロン (`;`)，等号 (`=`)、スラッシュ `/`) は、対応する UTF-8 エンコーディングを使用するように変換する必要があります。

次に例を示します。

```xml
curl -X GET \ "https://publish-p123-e456.adobeaemcloud.com/graphql/execute.json/wknd/adventure-by-path%3BadventurePath%3D%2Fcontent%2Fdam%2Fwknd%2Fen%2Fadventures%2Fbali-surf-camp%2Fbali-surf-camp"
```

URL は次の部分に分類できます。

| URL 部分 | 説明 |
|----------| -------------|
| `/graphql/execute.json` | 永続的なクエリエンドポイント |
| `/wknd/adventure-by-path` | 永続的なクエリパス |
| `%3B` | のエンコード `;` |
| `adventurePath` | クエリ変数 |
| `%3D` | のエンコード `=` |
| `%2F` | のエンコード `/` |
| `%2Fcontent%2Fdam...` | コンテンツフラグメントへのエンコードされたパス |

プレーンテキストでは、リクエスト URI は次のようになります。

```plaintext
/graphql/execute.json/wknd/adventure-by-path;adventurePath=/content/dam/wknd/en/adventures/bali-surf-camp/bali-surf-camp
```

クライアントアプリで永続化されたクエリを使用するには、AEMヘッドレスクライアント SDK を [JavaScript](https://github.com/adobe/aem-headless-client-js), [Java](https://github.com/adobe/aem-headless-client-java)または [NodeJS](https://github.com/adobe/aem-headless-client-nodejs). ヘッドレスクライアント SDK は、リクエストで任意のクエリ変数を適切にエンコードします。

## 実稼動環境への永続的なクエリの転送  {#transfer-persisted-query-production}

永続化されたクエリは、常に AEM オーサーサービスで作成してから、AEM パブリッシュサービスに公開（レプリケート）する必要があります。 多くの場合、永続化クエリは、ローカル環境や開発環境などの低レベルの環境で作成およびテストされます。 その後、永続化されたクエリを上位レベルの環境に昇格し、最終的に、クライアントアプリケーションが使用できるように、実稼動 AEM パブリッシュ環境でクエリを使用できるようにする必要があります。

### パッケージの永続的なクエリ

永続クエリは、 [AEMパッケージ](/help/implementing/developing/tools/package-manager.md). その後、AEMパッケージを別の環境にダウンロードしてインストールできます。 AEMパッケージは、AEM オーサー環境から AEM パブリッシュ環境にレプリケートすることもできます。

パッケージを作成するには：

1. に移動します。 **ツール** > **導入** > **パッケージ**.
1. をタップして新しいパッケージを作成します。 **パッケージを作成**. パッケージを定義するダイアログが開きます。
1. パッケージ定義ダイアログで、 **一般** 入力 **名前** 例えば、「wknd-persistent-queries」などです。
1. 「1.0」のようなバージョン番号を入力します。
1. の下 **フィルター** 新しい **フィルター**. パスファインダーを使用して `persistentQueries` フォルダーの下に配置されます。 例： `wknd` フルパスの設定： `/conf/wknd/settings/graphql/persistentQueries`.
1. タップ **保存** 新しいパッケージ定義を保存し、ダイアログを閉じます。
1. 次をタップします。 **ビルド** ボタンをクリックします。

パッケージが構築されたら、次の操作を実行できます。

* **ダウンロード** パッケージを別の環境に再度アップロードします。
* **複製** タップすることによるパッケージ **詳細** > **複製**. 接続された AEM パブリッシュ環境にパッケージがレプリケートされます。

<!--
1. Using replication/distribution tool:
   1. Go to the Distribution tool.
   1. Select tree activation for the configuration (for example, `/conf/wknd/settings/graphql/persistentQueries`).

* Using a workflow (via workflow launcher configuration):
  1. Define a workflow launcher rule for executing a workflow model that would replicate the configuration on different events (for example, create, modify, amongst others).
-->
