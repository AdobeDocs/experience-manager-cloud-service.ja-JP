---
title: AEMでの GraphiQL IDE の使用
description: Adobe Experience Managerでの GraphiQL IDE の使用方法を説明します。
feature: Content Fragments,GraphQL API
exl-id: be2ebd1b-e492-4d77-b6ef-ffdea9a9c775
source-git-commit: dfcad7aab9dda7341de3dc4975eaba9bdfbd9780
workflow-type: tm+mt
source-wordcount: '964'
ht-degree: 2%

---

# GraphiQL IDE の使用 {#graphiql-ide}

標準の実装 [GraphiQL](https://graphql.org/learn/serving-over-http/#graphiql) IDE は、Adobe Experience Manager(AEM) の GraphQL API でas a Cloud Serviceして使用できます。

>[!NOTE]
>
>この機能の一部はプレリリースチャネルで利用できます。 特に、持続クエリに関連する機能です。
> 
>詳しくは、 [プレリリースチャネルドキュメント](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/release-notes/prerelease.html#enable-prerelease) を参照してください。

>[!NOTE]
>
>GraphiQL はAEMに含まれますが、デフォルトでは、 `dev-authors` 環境。

>[!NOTE]
>必ず [エンドポイントを設定済み](/help/headless/graphql-api/graphql-endpoint.md) 内 [設定ブラウザー](/help/assets/content-fragments/content-fragments-configuration-browser.md) GraphiQL IDE を使用する前に。


この **GraphiQL** ツールを使用すると、次のことを可能にして、GraphQL クエリをテストおよびデバッグできます。
* を選択します。 **エンドポイント** クエリに使用する Sites 設定に適したもの
* 新しいクエリを直接入力
* 作成し、にアクセスします。 **[永続クエリ](/help/headless/graphql-api/persisted-queries.md)**
* クエリを実行して結果をすぐに確認する
* 管理 **クエリ変数**
* 保存し、管理する **永続クエリ**
* 公開または非公開 **永続クエリ** ( 宛先/差出人 `dev-publish`)
* 参照 **履歴** 以前のクエリの
* を使用します。 **ドキュメントエクスプローラ** ドキュメントにアクセスするには、以下を実行します。使用可能な方法を学び理解するのに役立ちます。

次に例を示します。

* `http://localhost:4502/content/graphiql.html`

![GraphiQL インターフェイス](assets/cfm-graphiql-interface.png "GraphiQL インターフェイス")

開発オーサーシステムで GraphiQL を使用して、GETリクエストと公開クエリを使用してクライアントアプリケーションから要求できるようにすることができます。 実稼動環境で使用する場合は、次の操作を行う必要があります [クエリを実稼動環境に移動する](/help/headless/graphql-api/persisted-queries.md#transfer-persisted-query-production). 最初は、実稼動作成者に対して、クエリを使用して新しく作成したコンテンツを検証し、最後に実稼動公開でライブ消費を検証します。

## エンドポイントの選択 {#selecting-endpoint}

最初の手順として、 **[エンドポイント](/help/headless/graphql-api/graphql-endpoint.md)** クエリに使用する エンドポイントは、クエリに使用する Sites 設定に適しています。

これは、右上のドロップダウンリストから使用できます。

## 新しいクエリを作成し、保持する {#creating-new-query}

エディターに新しいクエリを入力できます。エディターは左中央のパネルにあり、GraphiQL ロゴのすぐ下にあります。

>[!NOTE]
>
>永続化されたクエリが既に選択されていて、エディターパネルにが表示されている場合は、「 」を選択します。 `+` ( 次の **永続クエリ**) をクリックして、新しいクエリの準備ができたエディターを空にします。

入力を始めるだけで、エディターも次のようにします。

* は、マウスオーバーを使用して要素に関する追加情報を表示します
* には、構文のハイライト表示、オートコンプリート、自動提案などの機能があります。

>[!NOTE]
>
>GraphQL クエリは通常、 `{` 文字。
>
>行の先頭に `#` は無視されます。

用途 **名前を付けて保存** をクリックして新しいクエリを保持します。

## 持続的なクエリの更新 {#updating-persisted-query}

更新するクエリを、 **永続クエリ** パネル（左端）

クエリがエディターパネルに表示されます。 必要な変更を加え、を使用します。 **保存** を使用して、更新を永続化されたクエリにコミットします。

## 実行中のクエリ {#running-queries}

新しいクエリを直ちに実行することも、永続化されたクエリを読み込んで実行することもできます。 永続化されたクエリを読み込むには、リストからクエリを選択します。クエリがエディターパネルに表示されます。

どちらの場合も、エディターパネルに表示されるクエリは、次のいずれかの場合に実行されるクエリです。

* クリックまたはタップ **クエリを実行** アイコン
* キーボードの組み合わせを使用する `Control-Enter`

## クエリ変数 {#query-variables}

<!-- more details needed here? -->

また、GraphiQL IDE では、 [クエリ変数](/help/headless/graphql-api/content-fragments.md#graphql-variables).

次に例を示します。

![GraphQL 変数](assets/cfm-graphqlapi-03.png "GraphQL 変数")

## 永続化されたクエリの公開 (dev-publish) {#publishing-persisted-queries}

リスト（左パネル）から永続化されたクエリを選択したら、 **公開** および **非公開** アクション。 これにより、開発パブリッシュ環境 (`dev-publish`) 環境を使用して、テスト時にアプリケーションから簡単にアクセスできます。

>[!NOTE]
>
>永続化されたクエリのキャッシュの定義 `Time To Live` {&quot;cache-control&quot;:&quot;parameter&quot;:value} のデフォルト値は 2 時間（7200 秒）です。

## 永続化されたクエリのキャッシュ {#caching-persisted-queries}

AEMは、デフォルトの有効期間 (TTL) に基づいてコンテンツ配信ネットワーク (CDN) キャッシュを無効にします。

この値は次の値に設定されます。

* 7200 秒が Dispatcher および CDN のデフォルトの TTL である。別名 *共有キャッシュ*
   * デフォルト：s-maxage=7200
* 60 がクライアントのデフォルトの TTL です（ブラウザーなど）。
   * デフォルト：maxage=60

GraphiQL UI で保持されたAEM GraphQL クエリは、実行時にデフォルトの TTL を使用します。 GraphLQ クエリの TTL を変更する場合は、代わりに API メソッドを使用してクエリを保持する必要があります。 これには、コマンドラインインターフェイスで CURL を使用してAEMにクエリを投稿する必要があります。

例：

```xml
curl -X PUT \
    -H 'authorization: Basic YWRtaW46YWRtaW4=' \
    -H "Content-Type: application/json" \
    "http://localhost:4502/graphql/persist.json/wknd/plain-article-query-max-age" \
    -d \
'{ "query": "{articleList { items { _path author main { json } referencearticle { _path } } } }", "cache-control": { "max-age": 300 }}'
```

この `cache-control` は、作成時 (PUT) 以降 ( 例えば、POSTリクエストなどを介 ) に設定できます。 AEMはデフォルト値を提供できるので、永続化されたクエリを作成する場合は cache-control はオプションです。 詳しくは、 [GraphQL クエリを保持する方法](/help/headless/graphql-api/persisted-queries.md#how-to-persist-query)（curl を使用してクエリを永続化する例）。

## URL をコピーしてクエリに直接アクセス {#copy-url}

この **URL をコピー** 「 」オプションを使用すると、永続化されたクエリに直接アクセスして結果を確認するために使用する URL をコピーして、クエリをシミュレートできます。 その後、これをテストに使用できます。例えば、ブラウザーでにアクセスすると、次のようになります。

<!--
  >[!NOTE]
  >
  >The URL will need [encoding before using programmatically](/help/headless/graphql-api/persisted-queries.md#encoding-query-url).
  >
  >The target environment might need adjusting, depending on your requirements.
-->

次に例を示します。

`http://localhost:4502/graphql/execute.json/global/article-list-01`

この URL をブラウザーで使用すると、結果を確認できます。

![GraphiQL - URL をコピー](assets/cfm-graphiql-copy-url.png "GraphiQL - URL をコピー")

この **URL をコピー** オプションには、持続的なクエリ名（左端のパネル）の右側の 3 つの縦並びのドットからアクセスできます。

![GraphiQL - URL をコピー](assets/cfm-graphiql-persisted-query-options.png "GraphiQL - URL をコピー")

## 永続クエリの削除 {#deleting-persisted-queries}

この **削除** オプションには、持続的なクエリ名（左端のパネル）の右側の 3 つの縦ドットからもアクセスできます。

<!-- what happens if you try to delete something that is still published? -->


## 実稼動環境への永続クエリのインストール {#installing-persisted-query-production}

GraphiQL を使用して永続的なクエリを開発およびテストした後、最終目標は次のとおりです。 [実稼動環境に転送する](/help/headless/graphql-api/persisted-queries.md#transfer-persisted-query-production) アプリケーションで使用する場合。

## ショートカットキー {#keyboard-shortcuts}

IDE のアクションアイコンに直接アクセスできるキーボードショートカットがいくつか用意されています。

* クエリを事前設定：  `Shift-Control-P`
* 結合クエリ：  `Shift-Control-M`
* クエリを実行：  `Control-Enter`
* オートコンプリート：  `Control-Space`

>[!NOTE]
>
>一部のキーボードでは `Control` キーには次のラベルが付けられます。 `Ctrl`.
