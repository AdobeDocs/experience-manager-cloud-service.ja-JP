---
title: AEM AssetsAPIを使用したコンテンツの更新方法
description: AEMヘッドレス開発者ジャーニーのこの部分では、REST APIを使用してコンテンツフラグメントのコンテンツにアクセスし、更新する方法を説明します。
hide: true
hidefromtoc: true
index: false
exl-id: 8d133b78-ca36-4c3b-815d-392d41841b5c
translation-type: tm+mt
source-git-commit: 0c47dec1e96fc3137d17fc3033f05bf1ae278141
workflow-type: tm+mt
source-wordcount: '1657'
ht-degree: 71%

---

# AEM AssetsAPIを使用したコンテンツの更新方法{#update-your-content}

>[!CAUTION]
>
>作業中 — このドキュメントの作成は現在進行中で、完全なもの、最終的なもの、または実稼働目的で使用するものとして理解してはなりません。

[AEMヘッドレス開発者ジャーニーのこの部分では、](overview.md)がREST APIを使用してコンテンツフラグメントのコンテンツにアクセスし、更新する方法を学びます。

## {#story-so-far}

以前のドキュメントのAEM headlessジャーニーでは、[AEM配信APIを介したコンテンツへのアクセス方法](access-your-content.md)で、AEM GraphQL APIを介したAEMのheadlessコンテンツへのアクセス方法を学び、次の点に注意してください。

* GraphQLについて高レベルの理解を得る。
* AEM GraphQL APIの仕組みを理解します。
* 実際的なサンプルクエリをいくつか理解します。

この記事は、これらの基本事項に基づいて構築されているので、REST APIを使用してAEMの既存のヘッドレスコンテンツを更新する方法を理解しています。

## 目的 {#objective}

* **オーディエンス**:詳細
* **目的**:REST APIを使用してコンテンツフラグメントのコンテンツにアクセスし、更新する方法を説明します。
   * AEM AssetsHTTP APIを紹介します。
   * APIでコンテンツフラグメントのサポートを紹介し、ディスカッションを行います。
   * APIの詳細を説明します。

<!--
  * Look at sample code to see how things work in practice.
-->

## コンテンツフラグメントにアセットHTTP APIが必要な理由{#why-http-api}

ヘッドレスジャーニーの前の段階では、AEM GraphQL APIを使用してクエリを使用してコンテンツを取得する方法を学びました。

では、なぜ別のAPIが必要なのでしょうか。

Assets HTTP APIではコンテンツを&#x200B;**読み取り**&#x200B;できますが、**作成**、**更新**、**削除**&#x200B;コンテンツ（GraphQL APIでは不可能）も実行できます。

## Assets HTTP API {#assets-http-api}

[Assets HTTP API](/help/assets/mac-api-assets.md) には次の API が含まれます。

* Assets REST API
* コンテンツフラグメントをサポートしています。

現在の Assets HTTP API の実装は、**REST** アーキテクチャスタイルに基づいています。

Assets REST APIを使用すると、開発者はCloud ServiceとしてAdobe Experience Managerのコンテンツ(AEMに保存されている)に、**CRUD**&#x200B;操作（作成、読み取り、更新、削除）経由で直接アクセスできます。

この API では、コンテンツサービスを JavaScript フロントエンドアプリケーションに提供することで、Adobe Experience Manager as a Cloud Service をヘッドレス CMS（コンテンツ管理システム）として動作させることができます。または、HTTP リクエストを実行して JSON 応答を処理できる他のどのようなアプリケーションにもすることができます。

例えば、単一ページアプリ(SPA)、フレームワークベースまたはカスタムの場合、API経由で提供されるコンテンツは、多くの場合JSON形式で提供する必要があります。

AEM コアコンポーネントは、この目的に必要な読み取り操作を提供できる非常に包括的で柔軟性の高いカスタマイズ可能な API を提供し、その JSON 出力もカスタマイズできますが、実装には AEM WCM（Web コンテンツ管理）のノウハウが必要です。専用の AEM テンプレートに基づいた（API）ページでこれらのコンポーネントをホストする必要があるからです。すべての SPA 開発組織が、こうした知識にアクセスできるわけではありません。

これが可能なのは、Assets REST API が使用できる場合です。この場合は、アセット（画像やコンテンツフラグメントなど）に直接アクセスでき、その際に、ページにアセットを埋め込んでからコンテンツをシリアル化 JSON 形式で配信する必要はありません

>[!NOTE]
>
>Assets REST API からの JSON 出力はカスタマイズできません。

また、Assets REST API を使用すると、アセット、コンテンツフラグメント、フォルダーの新規作成、更新、削除のいずれかの操作でコンテンツを変更することもできます。

Assets REST API は、

* HATEOAS の原則に従っています。
* SIREN 形式を実装しています。

## 前提条件 {#prerequisites}

Assets REST API は、最新の Adobe Experience Manager as a Cloud Service バージョンの標準インストールで利用できます。

## 主要な概念 {#key-concepts}

アセットREST APIオファーは、AEMインスタンス内に保存されたアセットにREST形式でアクセスします。

`/api/assets` エンドポイントを使用しており、アクセスするにはアセットのパス（先頭の `/content/dam` を除く）が必要です。

* つまり、次の場所のアセットにアクセスするには
   * `/content/dam/path/to/asset`
* 次のリクエストが必要です。
   * `/api/assets/path/to/asset`

例えば、`/content/dam/wknd/en/adventures/cycling-tuscany` にアクセスするには、`/api/assets/wknd/en/adventures/cycling-tuscany.json` をリクエストします。

>[!NOTE]
>アクセス経由：
>
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

サポートされているリクエストの正確な形式は、『API リファレンス』ドキュメントで定義されています。

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
>* CORS／AEM の説明
>* ビデオ - AEM を使用した CORS 向け開発

>



特定の認証要件がある環境では、OAuth を推奨します。

## 使用可能な機能 {#available-features}

コンテンツフラグメントは特定のアセットタイプです。コンテンツフラグメントの操作を参照してください。

API を通じて使用できる機能について詳しくは、以下を参照してください。

* Assets REST API
* エンティティタイプ。（コンテンツフラグメントに関連した）サポートされる各タイプに固有の機能について説明します。

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

### アセット {#assets}

アセットが要求されると、アセットのメタデータ（タイトルや名前など、それぞれのアセットスキーマで定義される情報）が応答で返されます。

アセットのバイナリデータは、`content` タイプの SIREN リンクとして公開されます。

アセットには複数のレンディションを含めることができます。通常、これらは子エンティティとして公開されます。ただし、サムネールレンディションは例外です。これは、`thumbnail` タイプ（`rel="thumbnail"`）のリンクとして公開されます。

### コンテンツフラグメント {#content-fragments}

コンテンツフラグメントは、特別な種類のアセットです。 コンテンツフラグメントを使用すれば、テキスト、数値、日付など様々な要素を含む構造化データにアクセスできます。

標準アセット（画像やオーディオなど）との違いがいくつかあるので、それらの処理には追加のルールが適用されます。**

#### 表現  {#representation}

コンテンツフラグメント：

* バイナリデータを公開しません。
* JSON 出力（`properties` プロパティ内）に完全に含まれます。

* アトミックと見なされます。つまり、エレメントとバリエーションは、リンクまたは子エンティティとしてではなく、フラグメントのプロパティの一部として公開されます。これにより、フラグメントのペイロードに効率的にアクセスできます。

#### コンテンツモデルとコンテンツフラグメント  {#content-models-and-content-fragments}

現在、コンテンツフラグメントの構造を定義するモデルは、HTTP API では公開されません。そのため、*コンシューマー*&#x200B;は（最低でも）フラグメントのモデルについて理解する必要があります。ただし、ほとんどの情報はペイロードから推測することができます。データタイプなどは定義の一部だからです。

新しいコンテンツフラグメントを作成するには、（内部リポジトリ）モデルのパスを指定する必要があります。

#### 関連コンテンツ {#associated-content}

関連コンテンツは現在公開されていません。

## アセットREST APIの使用{#using-aem-assets-rest-api}

AEM AssetsREST APIの使用の詳細については、次を参照してください。

* Adobe Experience ManagerアセットHTTP API
* AEM Assets HTTP API でのコンテンツフラグメントのサポート 

## 次の作業{#whats-next}

AEMヘッドレス開発者ジャーニーのこの部分が完了したら、次の作業を行う必要があります。

* AEM AssetsHTTP APIについて説明します。
* このAPIでコンテンツフラグメントがどのようにサポートされているかを理解します。

<!--
* Have experience with sample code and know how the API works in practice.
-->

AEMのヘッドレスジャーニーは、次にドキュメント[How to Put It All Togeter - Your App and Your Content in AEM Headless](put-it-all-together.md)を確認し、AEMヘッドレスプロジェクトの取り組みと運用準備を進めて行く必要があります。

## その他のリソース {#additional-resources}

* [REST](https://en.wikipedia.org/wiki/Representational_state_transfer)
* [HATEOASの原則](https://en.wikipedia.org/wiki/HATEOAS)
* [SIREN形式](https://github.com/kevinswiber/siren)
* [Assets HTTP API](/help/assets/mac-api-assets.md)
* [コンテンツフラグメント REST API](/help/assets/content-fragments/assets-api-content-fragments.md)
   * [API リファレンス](/help/assets/content-fragments/assets-api-content-fragments.md#api-reference)
* [コンテンツフラグメントの操作](/help/assets/content-fragments/content-fragments.md)
* [AEM コアコンポーネント](https://docs.adobe.com/content/help/ja/experience-manager-core-components/using/introduction.html)
* [CORS／AEM の説明](https://helpx.adobe.com/jp/experience-manager/kt/platform-repository/using/cors-security-article-understand.html)
* [ビデオ - AEM を使用した CORS 向け開発](https://helpx.adobe.com/jp/experience-manager/kt/platform-repository/using/cors-security-technical-video-develop.html)

