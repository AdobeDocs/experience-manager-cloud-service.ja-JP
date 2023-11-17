---
title: Assets HTTP API での Adobe Experience Manager as a Cloud Service コンテンツフラグメントのサポート
description: Adobe Experience Managerのヘッドレス配信機能の重要な部分である、Assets HTTP API でのコンテンツフラグメントのサポートについて説明します。
feature: Content Fragments,Assets HTTP API
exl-id: d72cc0c0-0641-4fd6-9f87-745af5f2c232
source-git-commit: e2505c0fec1da8395930f131bfc55e1e2ce05881
workflow-type: tm+mt
source-wordcount: '1791'
ht-degree: 59%

---

# AEM Assets HTTP API でのコンテンツフラグメントのサポート  {#content-fragments-support-in-aem-assets-http-api}

## 概要 {#overview}

| バージョン | 記事リンク |
| -------- | ---------------------------- |
| AEM 6.5 | [ここをクリックしてください](https://experienceleague.adobe.com/docs/experience-manager-65/assets/extending/assets-api-content-fragments.html?lang=ja) |
| AEM as a Cloud Service | この記事 |

Adobe Experience Manager(AEM) ヘッドレス配信機能の重要な要素である、Assets HTTP API でのコンテンツフラグメントのサポートについて説明します。

>[!NOTE]
>
>[Assets HTTP API](/help/assets/mac-api-assets.md) には次の API が含まれます。
>
>* Assets REST API
>* コンテンツフラグメントをサポートしています
>
>現在の Assets HTTP API の実装は、[REST](https://en.wikipedia.org/wiki/Representational_state_transfer) アーキテクチャスタイルに基づいています。

The [Assets REST API](/help/assets/mac-api-assets.md) を使用すると、Adobe Experience Manager as a Cloud Serviceの開発者は、CRUD（作成、読み取り、更新、削除）操作を使用して、HTTP API を介して (AEMに保存された ) コンテンツに直接アクセスできます。

API を使用すると、JavaScript フロントエンドアプリケーションにコンテンツサービスを提供することで、Adobe Experience Manager as a Cloud Serviceをヘッドレス CMS(Content Management System) として操作できます。 または、HTTP リクエストを実行して JSON 応答を処理できる他のどのようなアプリケーションにもすることができます。

例えば、[単一ページアプリケーション（SPA）](/help/implementing/developing/hybrid/introduction.md)では、フレームワークベースかカスタムかを問わず、HTTP API 経由で提供されるコンテンツ（多くの場合 JSON 形式）が必要です。

While [AEMコアコンポーネント](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html?lang=ja) この目的で必要な読み取り操作と、JSON 出力をカスタマイズできる API には、実装にAEM WCM(Web Content Management) のノウハウが必要です。 これは、専用のAEMテンプレートに基づくページでホストする必要があるからです。 すべての SPA 開発組織が、こうした知識にアクセスできるわけではありません。

これが可能なのは、Assets REST API が使用できる場合です。この場合は、アセット（画像やコンテンツフラグメントなど）に直接アクセスでき、その際に、ページにアセットを埋め込んでからコンテンツをシリアル化 JSON 形式で配信する必要はありません

>[!NOTE]
>
>Assets REST API からの JSON 出力はカスタマイズできません。

また、Assets REST API を使用すると、アセット、コンテンツフラグメント、フォルダーの新規作成、更新、削除を行って、コンテンツを変更できます。

Assets REST API は、

* [HATEOAS の原則](https://ja.wikipedia.org/wiki/HATEOAS)に従っています。

* [SIREN 形式](https://github.com/kevinswiber/siren)を実装しています。

## 前提条件 {#prerequisites}

Assets REST API は、最新の Adobe Experience Manager as a Cloud Service バージョンの標準インストールで利用できます。

## 主要な概念 {#key-concepts}

Assets REST API を使用すると、AEM インスタンス内に格納されたアセットに [REST](https://en.wikipedia.org/wiki/Representational_state_transfer) 形式でアクセスすることができます。

`/api/assets` エンドポイントを使用しており、アクセスするにはアセットのパス（先頭の `/content/dam` を除く）が必要です。

* つまり、次の場所のアセットにアクセスするには
   * `/content/dam/path/to/asset`
* リクエスト:
   * `/api/assets/path/to/asset`

例えば、`/content/dam/wknd/en/adventures/cycling-tuscany` にアクセスするには、`/api/assets/wknd/en/adventures/cycling-tuscany.json` をリクエストします。

>[!NOTE]
>アクセス経由：
>
>* `/api/assets` は `.model` セレクターを使用する&#x200B;**必要はありません**。
>* `/content/path/to/page` は `.model` セレクターを使用する&#x200B;**必要があります**。

実行する操作は HTTP メソッドで決まります。

* **GET**：アセットまたはフォルダーの JSON 表現を取得します
* **POST**  — アセットまたはフォルダーを作成します。
* **PUT**：アセットまたはフォルダーのプロパティを更新します
* **DELETE**：アセットまたはフォルダーを削除します

>[!NOTE]
>
>リクエスト本文または URL パラメーターは、これらの操作の一部を設定するために使用できます。例えば、フォルダーまたはアセットを **POST** リクエストで作成するように定義できます。

サポートされているリクエストの正確な形式は、[API リファレンス](/help/assets/content-fragments/assets-api-content-fragments.md#api-reference)ドキュメントで定義されています。

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
   <td>サポートされる使用例</td>
   <td>一般的用途。</td>
   <td><p>単一ページアプリケーション（SPA）またはその他の任意の（コンテンツ利用）コンテキストにおける使用に最適化されています。</p> <p>また、レイアウト情報を含めることもできます。</p> </td>
  </tr>
  <tr>
   <td>サポートされている操作</td>
   <td><p>作成、読み取り、更新、削除。</p> <p>エンティティタイプに応じて、追加の操作を使用します。</p> </td>
   <td>読み取り専用。</td>
  </tr>
  <tr>
   <td>アクセス</td>
   <td><p>直接アクセスできます。</p> <p><code>/api/assets </code> エンドポイントを使用し、（リポジトリー内の）<code>/content/dam</code>にマッピングします。</p> 
   <p>パスの例を次に示します。 <code>/api/assets/wknd/en/adventures/cycling-tuscany.json</code></p>
   </td>
    <td><p>AEMページ上のAEMコンポーネントを通じて参照する必要があります。</p> <p><code>.model</code> セレクターを使用して JSON 表現を作成します。</p> <p>パスの例を次に示します。<br/> <code>/content/wknd/language-masters/en/adventures/cycling-tuscany.model.json</code></p> 
   </td>
  </tr>
  <tr>
   <td>セキュリティ</td>
   <td><p>複数のオプションを使用できます。</p> <p>OAuth を推奨します。標準設定とは別に設定できます。</p> </td>
   <td>AEM の標準セットアップを使用します。</td>
  </tr>
  <tr>
   <td>アーキテクチャに関する補足</td>
   <td><p>書き込みアクセスは、通常、オーサーインスタンスを指します。</p> <p>読み取りは、パブリッシュインスタンスにも送られる場合があります。</p> </td>
   <td>この方法は読み取り専用なので、通常、パブリッシュインスタンスに使用されます。</td>
  </tr>
  <tr>
   <td>出力</td>
   <td>JSON ベースの SIREN 出力：詳細ながら強力です。 コンテンツ内を移動できます。</td>
   <td>JSON ベースの独自出力。Sling モデルを通じて設定可能です。コンテンツ構造内での移動は実装が困難です（ただし、必ずしも不可能ではありません）。</td>
  </tr>
 </tbody>
</table>

### セキュリティ {#security}

特定の認証要件がない環境で Assets REST API が使用される場合は、AEM CORS フィルターを正しく設定する必要があります。

>[!NOTE]
>
>詳しくは、次を参照してください。
>
>* [CORS／AEM の説明](https://experienceleague.adobe.com/docs/experience-manager-learn/foundation/security/understand-cross-origin-resource-sharing.html?lang=ja?lang=ja)
>* [ビデオ — AEM (04:06)を使用した CORS 向けの開発](https://experienceleague.adobe.com/docs/experience-manager-learn/foundation/security/develop-for-cross-origin-resource-sharing.html?lang=en)
>

特定の認証要件がある環境では、OAuth を推奨します。

## 使用可能な機能 {#available-features}

コンテンツフラグメントは特定のアセットタイプです。[コンテンツフラグメントの操作](/help/assets/content-fragments/content-fragments.md)を参照してください。

API を通じて使用できる機能について詳しくは、以下を参照してください。

* [Assets REST API](/help/assets/mac-api-assets.md)
* [エンティティタイプ](/help/assets/content-fragments/assets-api-content-fragments.md#entity-types)。（コンテンツフラグメントに関連した）サポートされる各タイプに固有の機能について説明します。

### ページング {#paging}

Assets REST API は、URL パラメーターを介して (GETリクエストに対して ) ページングをサポートします。

* `offset` - 取得する最初の（子）エンティティの数
* `limit` - 返されるエンティティの最大数

応答には、ページング情報が `properties` SIREN 出力のセクション。 この `srn:paging` プロパティには、（子）エンティティの総数 ( `total`)、オフセットおよび制限 ( `offset`, `limit`) に含まれます。

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

フォルダーは、アセットや他のフォルダーのコンテナとして機能します。 AEM コンテンツリポジトリーの構造を反映しています。

Assets REST API は、フォルダーのプロパティへのアクセスを公開します。 例えば、名前やタイトルなどです。 アセットは、フォルダーとサブフォルダーの子エンティティとして公開されます。

>[!NOTE]
>
>子アセットとフォルダーのアセットタイプに応じて、それぞれの子エンティティを定義するプロパティの完全なセットが、子エンティティのリストに既に含まれている場合があります。 または、この子エンティティリストのエンティティに対して、一部のプロパティのみ公開される場合もあります。

### Assets {#assets}

アセットが要求されると、アセットのメタデータ（タイトル、名前など、それぞれのアセットスキーマで定義された情報）が応答で返されます。

アセットのバイナリデータは、`content` タイプの SIREN リンクとして公開されます。

アセットには複数のレンディションを含めることができます。通常、これらは子エンティティとして公開されます。ただし、サムネールレンディションは例外です。これは、`thumbnail` タイプ（`rel="thumbnail"`）のリンクとして公開されます。

### コンテンツフラグメント {#content-fragments}

[コンテンツフラグメント](/help/assets/content-fragments/content-fragments.md)は特殊なタイプのアセットです。これらを使用して、テキスト、数値、日付などの構造化データにアクセスできます。

*標準*&#x200B;アセット（画像やオーディオなど）との違いがいくつかあるので、それらの処理には追加のルールが適用されます。

#### 表現 {#representation}

コンテンツフラグメント：

* バイナリデータを公開しません。
* JSON 出力 ( `properties` プロパティ ) を参照してください。

* 原子とも考えられています。 つまり、要素とバリエーションは、リンクや子エンティティとは異なり、フラグメントのプロパティの一部として公開されます。 これにより、フラグメントのペイロードに効率的にアクセスできます。

#### コンテンツモデルとコンテンツフラグメント {#content-models-and-content-fragments}

現在、コンテンツフラグメントの構造を定義するモデルは、HTTP API では公開されません。したがって、 *消費者* は、フラグメントのモデルについて（少なくとも 1 つ）把握している必要があります。ほとんどの情報はペイロードから推論できますが、データタイプなどは定義の一部です。

コンテンツフラグメントを作成するには、モデルの（内部リポジトリ）パスを指定する必要があります。

#### 関連コンテンツ {#associated-content}

関連コンテンツは公開されません。

## 使用 {#using}

使用方法は、特定の使用例に加えて、AEMオーサーを使用しているかパブリッシュ環境を使用しているかによって異なる場合があります。

* 作成をオーサーインスタンス ([現在のところ、この API を使用して公開するフラグメントをレプリケートする手段はありません。](/help/assets/content-fragments/assets-api-content-fragments.md#limitations)) をクリックします。
* AEM は要求されたコンテンツを JSON 形式でのみ提供するので、どちらからも配信できます。

   * ファイアウォールの後ろにあるメディアライブラリアプリケーションでは、AEMオーサーインスタンスからのストレージと配信で十分です。

   * ライブ Web 配信の場合は、AEMパブリッシュインスタンスを使用することをお勧めします。

>[!CAUTION]
>
>AEMクラウドインスタンス上の Dispatcher 設定により、へのアクセスがブロックされる場合があります。 `/api`.

>[!NOTE]
>
>詳細については、[API リファレンス](/help/assets/content-fragments/assets-api-content-fragments.md#api-reference)を参照してください。特に、[Adobe Experience Manager Assets API - コンテンツフラグメント](https://developer.adobe.com/experience-manager/reference-materials/cloud-service/javadoc/assets-api-content-fragments/index.html)。

## 制限事項 {#limitations}

次のように、いくつかの制限があります。

* **コンテンツフラグメントモデルは現在サポートされていません**：読み取りも作成もできません。既存のコンテンツフラグメントを作成または更新できるようにするには、開発者がコンテンツフラグメントモデルへの正しいパスを知っている必要があります。 現在のところ、これらの概要を取得するには、管理 UI を使用するしかありません。
* **参照は無視されます**。現在、既存のコンテンツフラグメントが参照されているかどうかの確認は行われません。したがって、例えば、コンテンツフラグメントを削除すると、削除されたコンテンツフラグメントへの参照を含んでいるページで問題が発生する可能性があります。
* **JSON データタイプ** の REST API 出力 *JSON データタイプ* 次に該当 *文字列ベースの出力*.

## ステータスコードとエラーメッセージ {#status-codes-and-error-messages}

関連する状況で次のステータスコードが表示されることがあります。

* **200**（OK）

  次の場合に返されます。

   * 次の方法でコンテンツフラグメントを要求する `GET`
   * 次の方法でコンテンツフラグメントを正常に更新する `PUT`

* **201**（Created）

  次の場合に返されます。

   * 次の方法でコンテンツフラグメントを正常に作成する `POST`

* **404**（Not Found）

  次の場合に返されます。

   * 要求されたコンテンツフラグメントが存在しない

* **500**（内部サーバーエラー）

  >[!NOTE]
  >
  >次の場合に返されます。
  >
  >* 特定のコードで識別できないエラーが発生した場合
  >* 指定されたペイロードが無効な場合

  以下に、このエラーステータスが返される場合の一般的なシナリオと、生成されるエラーメッセージ（等幅）を示します。

   * 親フォルダーが存在しない ( `POST`)
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

  詳細なエラーメッセージは、次の方法で返されます。

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

## API リファレンス {#api-reference}

詳細な API リファレンスについては、こちらを参照してください。

* [Adobe Experience Manager Assets API - コンテンツフラグメント](https://developer.adobe.com/experience-manager/reference-materials/cloud-service/javadoc/assets-api-content-fragments/index.html)

* [Assets HTTP API](/help/assets/mac-api-assets.md)

   * [使用可能な機能](/help/assets/mac-api-assets.md#available-features)

## その他のリソース {#additional-resources}

詳しくは、次を参照してください。

* [Assets HTTP API ドキュメント](/help/assets/mac-api-assets.md)
* [AEM Gem セッション：OAuth](https://experienceleague.adobe.com/docs/events/experience-manager-gems-recordings/gems2014/aem-oauth-server-functionality-in-aem.html?lang=en)
