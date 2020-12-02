---
title: Assets HTTP API での Adobe Experience Manager as a Cloud Service コンテンツフラグメントのサポート
description: Assets HTTP API での Adobe Experience Manager as a Cloud Service コンテンツフラグメントのサポートについて説明します。
translation-type: tm+mt
source-git-commit: 8aa2585e85b0ed23d68597857cda09dc301df4f6
workflow-type: tm+mt
source-wordcount: '1891'
ht-degree: 100%

---


# AEM Assets HTTP API でのコンテンツフラグメントのサポート{#content-fragments-support-in-aem-assets-http-api}

## 概要 {#overview}

>[!NOTE]
>
>[Assets HTTP API](/help/assets/mac-api-assets.md) には次の API が含まれます。
>
>* Assets REST API
>* コンテンツフラグメントをサポートしています。

>
>
現在の Assets HTTP API の実装は、[REST](https://en.wikipedia.org/wiki/Representational_state_transfer) アーキテクチャスタイルに基づいています。

[Assets REST API](/help/assets/mac-api-assets.md) を使用すると、Adobe Experience Manager as a Cloud Service の開発者は、HTTP API 経由で CRUD 操作（作成、読み取り、更新、削除）を介して、（AEM に保存された）コンテンツに直接アクセスできます。

この API では、コンテンツサービスを JavaScript フロントエンドアプリケーションに提供することで、Adobe Experience Manager as a Cloud Service をヘッドレス CMS（コンテンツ管理システム）として動作させることができます。または、HTTP リクエストを実行して JSON 応答を処理できる他のどのようなアプリケーションにもすることができます。

例えば、単一ページアプリケーション（SPA）では、フレームワークベースかカスタムかを問わず、HTTP API 経由で提供されるコンテンツ（多くの場合 JSON 形式）が必要です。

[AEM コアコンポーネント](https://docs.adobe.com/content/help/ja-JP/experience-manager-core-components/using/introduction.html)は、この目的に必要な読み取り操作を提供できる非常に包括的で柔軟性の高いカスタマイズ可能な API を提供し、その JSON 出力もカスタマイズできますが、実装には AEM WCM（Web コンテンツ管理）のノウハウが必要です。専用の AEM テンプレートに基づいた（API）ページでこれらのコンポーネントをホストする必要があるからです。すべての SPA 開発組織が、こうした知識にアクセスできるわけではありません。

これが可能なのは、Assets REST API が使用できる場合です。この場合は、アセット（画像やコンテンツフラグメントなど）に直接アクセスでき、その際に、ページにアセットを埋め込んでからコンテンツをシリアル化 JSON 形式で配信する必要はありません

>[!NOTE]
>
>Assets REST API からの JSON 出力はカスタマイズできません。

また、Assets REST API を使用すると、アセット、コンテンツフラグメント、フォルダーの新規作成、更新、削除のいずれかの操作でコンテンツを変更することもできます。

Assets REST API は、

* [HATEOAS の原則](https://en.wikipedia.org/wiki/HATEOAS)に従っています。

* [SIREN 形式](https://github.com/kevinswiber/siren)を実装しています。

## 前提条件 {#prerequisites}

Assets REST API は、最新の Adobe Experience Manager as a Cloud Service バージョンの標準インストールで利用できます。

## 主要な概念{#key-concepts}

Assets REST API を使用すると、AEM インスタンス内に格納されたアセットに [REST](https://en.wikipedia.org/wiki/Representational_state_transfer) 形式でアクセスすることができます。

`/api/assets` エンドポイントを使用しており、アクセスするにはアセットのパス（先頭の `/content/dam` を除く）が必要です。

* つまり、次の場所のアセットにアクセスするには
   * `/content/dam/path/to/asset`
* 次のリクエストが必要です。
   * `/api/assets/path/to/asset`

例えば、`/content/dam/wknd/en/adventures/cycling-tuscany` にアクセスするには、`/api/assets/wknd/en/adventures/cycling-tuscany.json` をリクエストします。

>[!NOTE]
>アクセス経由：
>* `/api/assets` は `.model` セレクターを使用する&#x200B;**必要はありません**。
>* `/content/path/to/page` は `.model` セレクターを使用する&#x200B;**必要があります**。


実行する操作は HTTP メソッドで決まります。

* **GET**：アセットまたはフォルダーの JSON 表現を取得します
* **POST**：新しいアセットまたはフォルダーを作成します
* **PUT**：アセットまたはフォルダーのプロパティを更新します
* **DELETE**：アセットまたはフォルダーを削除します

>[!NOTE]
>
>リクエスト本文または URL パラメーターは、これらの操作の一部を設定するために使用できます。例えば、フォルダーまたはアセットを **POST** リクエストで作成するように定義できます。

<!--
The exact format of supported requests is defined in the [API Reference](/help/assets/content-fragments/assets-api-content-fragments.md#api-reference) documentation.
-->

### トランザクション動作 {#transactional-behavior}

すべてのリクエストはアトミックです。

つまり、後続の（`write`）リクエストを結合して、単一のエンティティとして成功または失敗する単一のトランザクションにすることはできません。

### AEM（Assets）REST API と AEM コンポーネントの比較 {#aem-assets-rest-api-versus-aem-components}

<table>
 <thead>
  <tr>
   <td>項目</td>
   <td>Assets REST API<br/> </td>
   <td>AEM コンポーネント<br/>（Sling モデルを使用するコンポーネント）</td>
  </tr>
 </thead>
 <tbody>
  <tr>
   <td>サポートされている使用例</td>
   <td>汎用。</td>
   <td><p>単一ページアプリケーション（SPA）またはその他の任意の（コンテンツ利用）コンテキストにおける使用に最適化されています。</p> <p>レイアウト情報を含むこともできます。</p> </td>
  </tr>
  <tr>
   <td>サポートされている操作</td>
   <td><p>作成、読み取り、更新、削除。</p> <p>エンティティタイプに応じて、その他の操作も可能です。</p> </td>
   <td>読み取り専用。</td>
  </tr>
  <tr>
   <td>アクセス</td>
   <td><p>直接アクセスできます。</p> <p><code>/api/assets </code> エンドポイントを使用し、（リポジトリ内の）<code>/content/dam</code> にマッピングします。</p> 
   <p>パスの例を次に示します。 <code>/api/assets/wknd/en/adventures/cycling-tuscany.json</code></p>
   </td>
    <td><p>AEM ページ上の AEM コンポーネントを通じて参照する必要があります。</p> <p><code>.model</code> セレクターを使用して JSON 表現を作成します。</p> <p>パスの例を次に示します。<br/> <code>/content/wknd/language-masters/en/adventures/cycling-tuscany.model.json</code></p> 
   </td>
  </tr>
  <tr>
   <td>セキュリティ</td>
   <td><p>複数のオプションが可能です。</p> <p>OAuth が推奨されます。標準セットアップとは別に設定できます。</p> </td>
   <td>AEM の標準セットアップを使用します。</td>
  </tr>
  <tr>
   <td>アーキテクチャに関する補足</td>
   <td><p>書き込みアクセスは通常、オーサーインスタンスを対象にします。</p> <p>読み取りはパブリッシュインスタンスを対象にする場合もあります。</p> </td>
   <td>このアプローチは読み取り専用なので、通常はパブリッシュインスタンスに使用されます。</td>
  </tr>
  <tr>
   <td>出力</td>
   <td>JSON ベースの SIREN 出力：詳細ながら強力です。コンテンツ内のナビゲーションが可能です。</td>
   <td>JSON ベースの独自出力。Sling モデルを通じて設定可能です。コンテンツ構造のナビゲーションは実装が困難です（ただし、必ずしも不可能ではありません）。</td>
  </tr>
 </tbody>
</table>

### セキュリティ {#security}

特定の認証要件がない環境で Assets REST API が使用される場合は、AEM の CORS フィルターを正しく設定する必要があります。

>[!NOTE]
>
>詳しくは、次のセクションを参照してください。
>
>* [CORS／AEM の説明](https://helpx.adobe.com/jp/experience-manager/kt/platform-repository/using/cors-security-article-understand.html)
>* [ビデオ - AEM を使用した CORS 向け開発](https://helpx.adobe.com/jp/experience-manager/kt/platform-repository/using/cors-security-technical-video-develop.html)

>



特定の認証要件がある環境では、OAuth を推奨します。

## 使用可能な機能 {#available-features}

コンテンツフラグメントは特定のアセットタイプです。](/help/assets/content-fragments/content-fragments.md)コンテンツフラグメントの操作[を参照してください。

API を通じて使用できる機能について詳しくは、以下を参照してください。

* [Assets REST API](/help/assets/mac-api-assets.md)
* [エンティティタイプ](/help/assets/content-fragments/assets-api-content-fragments.md#entity-types)。（コンテンツフラグメントに関連した）サポートされる各タイプに固有の機能について説明します。

### ページング {#paging}

Assets REST API では、URL パラメーターを介して（GET リクエストの）ページングをサポートしています。

* `offset` - 取得する最初の（子）エンティティの数
* `limit` - 返されるエンティティの最大数

応答には、SIREN 出力の `properties` セクションの一部としてページング情報が含まれます。この `srn:paging` プロパティには、リクエストで指定されている、（子）エンティティの総数（`total`）、オフセット（`offset`）および制限（`limit`）が含まれています。

>[!NOTE]
>
>ページングは通常、コンテナエンティティ（つまり、レンディションのあるフォルダーやアセット）に適用されます。要求されたエンティティの子に関係するからです。

#### 例：ページング {#example-paging}

`GET /api/assets.json?offset=2&limit=3`

```json
...
"properties": {
    ...
    "srn:paging": {
        "total": 7,
        "offset": 2,
        "limit": 3
    }
    ...
}
...
```

## エンティティタイプ {#entity-types}

### フォルダー {#folders}

フォルダーは、アセットやその他のフォルダーのコンテナとして機能します。AEM コンテンツリポジトリの構造を反映しています。

Assets REST API は、フォルダーのプロパティ（名前、タイトルなど）へのアクセスを公開します。アセットは、フォルダーの子エンティティ、およびサブフォルダーとして公開されます。

>[!NOTE]
>
>子アセットとフォルダーのアセットタイプによっては、それぞれの子エンティティを定義するすべてのプロパティが、子エンティティのリストに既に含まれている場合があります。または、この子エンティティリストのエンティティに対して、一部のプロパティのみ公開される場合もあります。

### Assets {#assets}

アセットが要求されると、アセットのメタデータ（タイトルや名前など、それぞれのアセットスキーマで定義される情報）が応答で返されます。

アセットのバイナリデータは、`content` タイプの SIREN リンクとして公開されます。

アセットには複数のレンディションを含めることができます。通常、これらは子エンティティとして公開されます。ただし、サムネールレンディションは例外です。これは、`thumbnail` タイプ（`rel="thumbnail"`）のリンクとして公開されます。

### コンテンツフラグメント {#content-fragments}

[コンテンツフラグメント](/help/assets/content-fragments/content-fragments.md)は特殊なタイプのアセットです。コンテンツフラグメントを使用すれば、テキスト、数値、日付など様々な要素を含む構造化データにアクセスできます。

標準アセット（画像やオーディオなど）との違いがいくつかあるので、それらの処理には追加のルールが適用されます。**

#### 表現  {#representation}

コンテンツフラグメント：

* バイナリデータを公開しません。
* JSON 出力（`properties` プロパティ内）に完全に含まれます。

* アトミックと見なされます。つまり、エレメントとバリエーションは、リンクまたは子エンティティとしてではなく、フラグメントのプロパティの一部として公開されます。これにより、フラグメントのペイロードに効率的にアクセスできます。

#### コンテンツモデルとコンテンツフラグメント  {#content-models-and-content-fragments}

現在、コンテンツフラグメントの構造を定義するモデルは、HTTP API では公開されません。そのため、コンシューマーは（最低でも）フラグメントのモデルについて理解する必要があります。ただし、ほとんどの情報はペイロードから推測することができます。データタイプなど&#x200B;**&#x200B;は定義の一部だからです。

新しいコンテンツフラグメントを作成するには、（内部リポジトリ）モデルのパスを指定する必要があります。

#### 関連コンテンツ {#associated-content}

関連コンテンツは現在公開されていません。

## 使用 {#using}

使用方法は、特定の使用例以外にも、AEM オーサーを使用するかパブリッシュ環境を使用するかで異なることがあります。

* 作成をオーサーインスタンスに結び付けることを強くお勧めします（[現在は、この API を使用して公開するフラグメントをレプリケートする手段はありません](/help/assets/content-fragments/assets-api-content-fragments.md#limitations)）。
* 配信は、どちらからも可能です。AEM では、要求されたコンテンツを JSON 形式でのみ提供するからです。

   * ファイアウォールの背後で動作するメディアライブラリアプリケーションには、AEM オーサーインスタンスからの格納と配信で十分です。

   * ライブ Web 配信の場合は、AEM パブリッシュインスタンスをお勧めします。

>[!CAUTION]
>
>AEM クラウドインスタンス上の Dispatcher 設定により、`/api` へのアクセスがブロックされる場合があります。

<!--
>[!NOTE]
>
>For further details, see the [API Reference](/help/assets/content-fragments/assets-api-content-fragments.md#api-reference). In particular, [Adobe Experience Manager Assets API - Content Fragments](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/assets-api-content-fragments/index.html). 
-->

### 読み取り／配信 {#read-delivery}

使用方法は次のとおりです。

`GET /{cfParentPath}/{cfName}.json`

次に例を示します。

`http://<host>/api/assets/wknd/en/adventures/cycling-tuscany.json`

応答は、コンテンツがコンテンツフラグメントに構造化されたシリアル化 JSON です。参照は参照 URL として配信されます。

次の 2 通りの読み取り操作が可能です。

* 特定のコンテンツフラグメントをパスで読み取る。この場合は、コンテンツフラグメントの JSON 表現が返されます。
* コンテンツフラグメントのフォルダーをパスで読み取る。この場合は、フォルダー内のすべてのコンテンツフラグメントの JSON 表現が返されます。

### 作成 {#create}

使用方法は次のとおりです。

`POST /{cfParentPath}/{cfName}`

本文には、作成するコンテンツフラグメントの JSON 表現を含める必要があります。これには、コンテンツフラグメント要素に設定する必要がある初期コンテンツも含まれます。`cq:model` プロパティの設定が必須で、このプロパティが有効なコンテンツフラグメントモデルを指している必要があります。そうしないと、エラーが発生します。また、`Content-Type` ヘッダーを追加することも必要です。これは `application/json` に設定されます。

### 更新 {#update}

使用方法は次のとおりです。

`PUT /{cfParentPath}/{cfName}`

本文には、特定コンテンツフラグメントの更新内容の JSON 表現を含める必要があります。

これには、コンテンツフラグメントのタイトルや説明、単一のエレメント、またはすべての要素値やメタデータを使用できます。

### 削除 {#delete}

使用方法は次のとおりです。

`DELETE /{cfParentPath}/{cfName}`

## 制限事項 {#limitations}

次のように、いくつかの制限があります。

* **バリエーションは書き込みも更新もできません。**&#x200B;バリエーションが（更新などの）ペイロードに追加された場合は、無視されます。ただし、このバリエーションは配信（`GET`）を通じて提供されます。

* **コンテンツフラグメントモデルは現在サポートされていません。**&#x200B;読み取りも作成もできません。新しいコンテンツフラグメントを作成または既存のコンテンツフラグメントを更新できるようにするには、コンテンツフラグメントモデルの正しいパスがわかっている必要があります。現在のところ、これらの概要を取得するには、管理 UI を使用するしかありません。
* **参照は無視されます。**&#x200B;現時点では、既存のコンテンツフラグメントが参照されているかどうかはチェックされません。したがって、例えば、コンテンツフラグメントを削除すると、削除されたコンテンツフラグメントへの参照を含んでいるページで問題が発生する可能性があります。

## ステータスコードとエラーメッセージ {#status-codes-and-error-messages}

関連する状況で次のステータスコードが表示されることがあります。

* **200**（OK）

   次の場合に返されます。

   * `GET` でコンテンツフラグメントを要求する

   * `PUT` でコンテンツフラグメントを正常に更新する

* **** 201（Created）

   次の場合に返されます。

   * `POST` でコンテンツフラグメントを正常に作成する

* **404**（Not Found）

   次の場合に返されます。

   * 要求されたコンテンツフラグメントが存在しない

* **** 500（内部サーバーエラー）

   >[!NOTE]
   >
   >次の場合に返されます。
   >
   >    * 特定のコードで識別できないエラーが発生した場合
   >    * 指定されたペイロードが有効でない場合


   このエラーステータスと生成されたエラーメッセージ（等幅テキスト）が返される一般的なシナリオの一覧を以下に示します。

   * 親フォルダーが存在しない（`POST` でコンテンツフラグメントを作成する場合）
   * コンテンツフラグメントモデルが指定されていない（cq:model が見つからない）、読み取れない（パスが無効か権限の問題が原因）、または有効なフラグメントモデルがありません。

      * `No content fragment model specified`
      * `Cannot create a resource of given model '/foo/bar/qux'`
   * コンテンツフラグメントを作成できなかった（アクセス権限の問題が発生している可能性がある）。

      * `Could not create content fragment`
   * タイトルや説明を更新できなかった。

      * `Could not set value on content fragment`
   * メタデータを設定できなかった。

      * `Could not set metadata on content fragment`
   * コンテンツ要素が見つからなかったか更新できなかった

      * `Could not update content element`
      * `Could not update fragment data of element`

   通常、詳細なエラーメッセージは次のように返されます。

   ```xml
   {
     "class": "core/response",
     "properties": {
       "path": "/api/assets/foo/bar/qux",
       "location": "/api/assets/foo/bar/qux.json",
       "parentLocation": "/api/assets/foo/bar.json",
       "status.code": 500,
       "status.message": "...{error message}.."
     }
   }
   ```

## API リファレンス  {#api-reference}

詳細な API リファレンスについては、こちらを参照してください。
<!--
* [Adobe Experience Manager Assets API - Content Fragments](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/assets-api-content-fragments/index.html)
-->

* [Assets HTTP API](/help/assets/mac-api-assets.md)

   * [使用可能な機能](/help/assets/mac-api-assets.md#available-features)

## その他のリソース {#additional-resources}

詳しくは、次のセクションを参照してください。

* [Assets HTTP API ドキュメント](/help/assets/mac-api-assets.md)
* [AEM Gem セッション：OAuth](https://helpx.adobe.com/jp/experience-manager/kt/eseminars/gems/aem-oauth-server-functionality-in-aem.html)

