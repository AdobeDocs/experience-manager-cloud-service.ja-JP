---
title: シンプルなアプリでのコンテンツのレンダリング
description: CodePen サンプルアプリと JavaScript 用 AEM ヘッドレスクライアントを使用して、体験版環境から JSON コンテンツを取得する方法を説明します。
hidefromtoc: true
index: false
exl-id: b7dc70f2-74a2-49f7-ae7e-776eab9845ae
source-git-commit: b9b9cf79173a0ae486bd5d8fcbc1fec48c0b2bc8
workflow-type: tm+mt
source-wordcount: '977'
ht-degree: 54%

---


# シンプルなアプリでのコンテンツのレンダリング {#render-content-simple-app}

>[!CONTEXTUALHELP]
>id="aemcloud_sites_trial_fetch_json_with_javascript"
>title="シンプルなアプリでのコンテンツのレンダリング"
>abstract="CodePen サンプルアプリと JavaScript 用 AEM ヘッドレスクライアントを使用して、体験版環境から JSON コンテンツを取得する方法を説明します。"

>[!CONTEXTUALHELP]
>id="aemcloud_sites_trial_fetch_json_with_javascript_guide"
>title="サンプル CodePen アプリの起動"
>abstract="このガイドでは、体験版環境から基本的な JavaScript web アプリへの JSON データのクエリについて説明します。前の学習モジュールでモデル化して作成したコンテンツフラグメントを使用します。必要に応じて、まずこれらのガイドを参照してから、このガイドに進んでください。"

>[!CONTEXTUALHELP]
>id="aemcloud_sites_trial_fetch_json_with_javascript_guide_footer"
>title="このモジュールでは、JavaScript 用 AEM ヘッドレスクライアントを使用して、GraphQL 永続クエリを使用して体験版環境から JSON データを取得する方法を説明します。<br><br>これで、このクライアントを使用して独自の web アプリケーション内からデータを使用する方法を理解できます。"
>abstract=""

## CodePen {#codepen}

CodePen は、フロントエンド web 開発用のオンラインコードエディターおよびプレイグラウンドです。これにより、HTML、CSS、JavaScript コードをブラウザーに記述して、作業の結果をほぼ瞬時に確認できます。 作業内容を保存して他のユーザーと共有することもできます。Adobeは、を使用して体験環境から JSON データを取得できる CodePen でアプリを作成しました。 [JavaScript 用AEMヘッドレスクライアント](https://github.com/adobe/aem-headless-client-js). このアプリをそのまま使用するか、自分の CodePen アカウントにフォークしてカスタマイズを加えることもできます。

クリック **サンプルの CodePen アプリケーションを起動します。** ボタンをクリックすると、CodePen のアプリが表示されます。 このアプリは、JavaScript を使用して JSON データを取得する最小限の例として機能します。サンプルアプリは、基になるコンテンツフラグメントモデルの構造に関係なく、返される JSON コンテンツをレンダリングするように設計されています。デフォルトでは、デスクトップアプリケーションは `aem-demo-assets` 試用環境に含まれる永続的なクエリ。 次のような JSON 応答が表示されます。

```json
{
  "data": {
    "adventureList": {
      "items": [
        {
          "_path": "/content/dam/aem-demo-assets/en/adventures/bali-surf-camp/bali-surf-camp",
          "title": "Bali Surf Camp",
          "price": "$5000 USD",
          ...
```

代わりにエラーが発生した場合は、ブラウザーコンソールで詳細を確認するか、詳しくは [電子メールで](mailto:aem-headless-trials-support@adobe.com?subject=AEM%20Trials%20support%20request).

CodePen について少し理解できたので、次に、前のモジュールで作成した永続クエリからデータを取得するようにアプリを設定します。

## JavaScript コードのチュートリアル {#code-walkthrough}

この **JS** ペインの右側にある CodePen には、サンプルアプリケーションの JavaScript が含まれています。 2 行目から、JavaScript 用AEMヘッドレスクライアントを Skypack CDN から読み込みます。 Skypack を使用すると、ビルド手順を必要とせずに開発を容易化できますが、独自のプロジェクトで AEM ヘッドレスクライアントと NPM または Yarn を使用することもできます。詳細については、[README](https://github.com/adobe/aem-headless-client-js#aem-headless-client-for-javascript) の使用手順を参照してください。

```javascript
import AdobeAemHeadlessClientJs from 'https://cdn.skypack.dev/@adobe/aem-headless-client-js@v3.2.0';
```

6 行目で、パブリッシュホストの詳細が `publishHost` クエリパラメーター。 このパラメーターは、AEMヘッドレスクライアントがデータを取得するホストです。 この機能は通常、アプリにコード化されますが、CodePen アプリが異なる環境で簡単に動作できるように、クエリパラメーターを使用します。

12 行目でAEM Headless Client を設定します。

```javascript
const aemHeadlessClient = new AdobeAemHeadlessClientJs({
  // Use a proxy to avoid CORS issues
  serviceURL: 'https://102588-505tanocelot.adobeioruntime.net/api/v1/web/aem/proxy',
  headers: {
    'aem-url': publishHost
  }
});
```

>[!NOTE]
>
>この **serviceURL** は、CORS の問題を回避するために、Adobe I/O Runtimeのプロキシ機能を使用するように設定されています。 このプロキシは、独自のプロジェクトには必要ありませんが、CodePen アプリが体験環境で動作するには必要です。 プロキシ関数は、クエリパラメーターで指定された **publishHost** 値を使用するように設定されています。

最後に、関数 `fetchJsonFromGraphQL()` を使用して、AEM ヘッドレスクライアントを使用して取得リクエストを実行します。この呼び出しは、コードが変更されるたびに実行されます。または、**再取得**&#x200B;リンクをクリックしてトリガーすることもできます。実際の `aemHeadlessClient.runPersistedQuery(..)` 呼び出しは 34 行目で行われます。少し後で、この JSON データのレンダリング方法を変更しますが、今は、に印刷します。 `#output` div を `resultToPreTag(queryResult)` 関数に置き換えます。

## 永続クエリからのデータの取得 {#use-persisted-query}

行 25 で、アプリがデータを取得する必要がある、永続化されたGraphQLのクエリを指定します。 永続化されたクエリ名は、エンドポイントの名前 ( `your-project` または `aem-demo-assets`) に続いてスラッシュを付け、次にクエリ名を付けます。 前のモジュールの指示に正確に従った場合、作成した永続化されたクエリは、 `your-project` endpoint.

1. を更新します。 `persistedQueryName` 変数を使用するので、前のモジュールで作成した永続化されたクエリを使用します。 命名の提案に従った場合は、`your-project` エンドポイントに `adventure-list` という名前の永続クエリを作成し、`persistedQueryName` 変数を `your-project/adventure-list` に設定することになります。

   ```javascript
   //
   // TODO: Use your persisted query here
   //
   persistedQueryName = 'your-project/adventure-list';
   ```

1. この変更が行われると、アプリが自動的に更新され、永続クエリからの生の JSON 応答が `#output` div に出力されます。エラーメッセージが表示された場合は、コンソールで詳細を確認してください。詳細 [電子メールで](mailto:aem-headless-trials-support@adobe.com?subject=AEM%20Trials%20support%20request) この手順でまだ問題が発生している場合は、をクリックします。

1. この JSON には、アプリで必要な正確なプロパティが含まれていますか？含まれていない場合は、[GraphQL API を使用したコンテンツの抽出](https://experience.adobe.com/experiencemanager/learn/extract_content_using_graphql)学習ガイドに戻って変更を加えてください。完了したら、必ずクエリを保存して公開してください。

## JSON レンダリングの変更 {#change-rendering}

JSON は、そのまま `pre` タグに貼り付けます。このタグはクリエイティブすぎません。 CodePen を切り替えて、 `resultToDom()` 関数を使用して、より興味深い結果を生成するために JSON 応答を繰り返し処理する方法を説明する代わりに、関数を使用する必要があります。

1. この変更を行うには、37 行目をコメントアウトし、40 行目からコメントを削除します。

   ```javascript
   // Output the results to a pre tag
   //resultToPreTag(queryResult);
   
   // Alternatively, build a colorful div structure with the JSON results and render images inline
   resultToDom(queryResult);
   ```

1. この関数は、JSON 応答に含まれる画像を、 `img` タグを使用します。 作成した **Adventure** コンテンツフラグメントに画像が含まれていない場合は、25 行目を変更して `aem-demo-assets/adventures-all` 永続クエリを使用するように切り替えてみることができます。

   ```javascript
   persistedQueryName = 'aem-demo-assets/adventures-all';
   ```

このクエリは、画像を含む JSON 応答を生成し、 `resultToDom()` 関数は、それらをインラインでレンダリングします。

![adventures-all クエリと resultToDom レンダリング関数の結果](assets/do-not-localize/adventures-all-query-result.png)

モデルとクエリの構築作業が完了したので、コンテンツチームは簡単に引き継ぐことができます。 次のモジュールでは、コンテンツ作成者のフローを表示します。
