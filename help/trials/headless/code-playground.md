---
title: シンプルなアプリでのコンテンツのレンダリング
description: CodePen サンプルアプリとAEM Headless Client for JavaScript を使用して、体験環境から JSON コンテンツを取得する方法を説明します。
hidefromtoc: true
index: false
exl-id: b7dc70f2-74a2-49f7-ae7e-776eab9845ae
source-git-commit: 3b64b909996674bcbe36f746bcfd15e1422a8a4b
workflow-type: tm+mt
source-wordcount: '1013'
ht-degree: 5%

---


# シンプルなアプリでのコンテンツのレンダリング {#render-content-simple-app}

>[!CONTEXTUALHELP]
>id="aemcloud_sites_trial_fetch_json_with_javascript"
>title="シンプルなアプリでコンテンツをレンダリング"
>abstract="CodePen サンプルアプリとAEM Headless Client for JavaScript を使用して、体験環境から JSON コンテンツを取得する方法を説明します。"

>[!CONTEXTUALHELP]
>id="aemcloud_sites_trial_fetch_json_with_javascript_guide"
>title="サンプル CodePen アプリの起動"
>abstract="このガイドでは、体験環境から基本的な JavaScript Web アプリケーションに JSON データをクエリする手順を説明します。 前の学習モジュールでモデル化して作成したコンテンツフラグメントを使用するので、このガイドに進む前に、まずこれらのガイドを参照してください。<br><br>JavaScript Web アプリからコンテンツを照会する方法を示すために、そのまま使用する CodePen を設定したり、独自のアカウントにフォークしてさらにカスタマイズしたりします。"

>[!CONTEXTUALHELP]
>id="aemcloud_sites_trial_fetch_json_with_javascript_guide_footer"
>title="このモジュールでは、JavaScript 用 AEM ヘッドレスクライアントを使用して、GraphQL 永続クエリを使用して体験版環境から JSON データを取得する方法を説明します。<br><br>これで、このクライアントを使用して独自の web アプリケーション内からデータを使用する方法を理解できます。"
>abstract=""

## CodePen {#codepen}

CodePen は、フロントエンド Web 開発用のオンラインコードエディターで、プレイグラウンドです。 ブラウザーでHTML、CSS、JavaScript コードを記述し、作業の結果をほぼ瞬時に確認できます。 作業内容を保存して他のユーザーと共有することもできます。 CodePen でアプリを作成しました。このアプリを使用して、体験環境から JSON データを取得できます。 [JavaScript 用AEMヘッドレスクライアント](https://github.com/adobe/aem-headless-client-js). このアプリをそのまま使用するか、または独自の CodePen アカウントにフォークして、さらにカスタマイズできます。

クリック **サンプルの CodePen アプリケーションを起動します。** ボタンをクリックすると、CodePen のアプリが表示されます。 デスクトップアプリケーションは、JavaScript を使用して JSON データを取得する最小限の例として機能します。 サンプルアプリは、基になるコンテンツフラグメントモデルの構造に関係なく、返される JSON コンテンツをレンダリングするように設計されています。 デフォルトでは、アプリケーションは `aem-demo-assets` 試用環境に含まれる永続的なクエリ。 次のような JSON 応答が表示されます。

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

代わりにエラーが発生した場合は、ブラウザーコンソールで詳細を確認するか、詳しくは [Slack](https://adobe-dx-support.slack.com).

CodePen について少し理解したので、次に、前のモジュールで作成した永続化されたクエリからデータを取得するようにアプリを設定します。

## JavaScript コードのチュートリアル {#code-walkthrough}

この **JS** CodePen の右側のパネルには、サンプルアプリケーションの JavaScript が含まれています。 2 行目から、JavaScript 用AEMヘッドレスクライアントを Skypack CDN から読み込みます。 Skypack は、ビルド手順を必要とせずに開発を容易にするために使用されますが、独自のプロジェクトでAEM Headless Client と NPM または Yarn を使用することもできます。 使用手順については、 [README](https://github.com/adobe/aem-headless-client-js#aem-headless-client-for-javascript) を参照してください。

```javascript
import AdobeAemHeadlessClientJs from 'https://cdn.skypack.dev/@adobe/aem-headless-client-js@v3.2.0';
```

6 行目では、公開ホストの詳細を `publishHost` クエリパラメーター。 これは、AEMヘッドレスクライアントがデータを取得するホストです。 これは通常はアプリにコード化されますが、CodePen アプリが異なる環境で簡単に動作できるように、クエリパラメーターを使用します。

CORS の問題を回避するために、プロキシAdobeIO Runtime 関数を使用するようにAEM Headless Client を 12 行目に設定します。 これは、独自のプロジェクトに必要なわけではありませんが、CodePen アプリが体験環境で動作するために必要になります。 プロキシ関数は、 `publishHost` クエリパラメーターで指定された値。

```javascript
const aemHeadlessClient = new AdobeAemHeadlessClientJs({
  // Use a proxy to avoid CORS issues
  serviceURL: 'https://102588-505tanocelot.adobeioruntime.net/api/v1/web/aem/proxy',
  headers: {
    'aem-url': publishHost
  }
});
```

最後に、関数 `fetchJsonFromGraphQL()` は、AEMヘッドレスクライアントを使用して取得リクエストを実行するために使用されます。 この呼び出しは、コードが変更されるたびに実行されます。または、 **再取得** リンク。 実際の `aemHeadlessClient.runPersistedQuery(..)` 呼び出しは 34 行目で発生します。 少し後で、この JSON データのレンダリング方法を変更しますが、現時点では、このデータを `#output` div を使用 `resultToPreTag(queryResult)` 関数に置き換えます。

## 永続クエリからデータを取得 {#use-persisted-query}

行 25 で、アプリがデータを取得する、永続化されたGraphQLのクエリを示します。 永続化されたクエリ名は、エンドポイントの名前 ( `your-project` または `aem-demo-assets`) に続いてスラッシュを付け、次にクエリ名を付けます。 前のモジュールの指示に正確に従った場合、作成した永続化されたクエリは、 `your-project` endpoint.

1. を更新します。 `persistedQueryName` 変数を使用して、前のモジュールで作成した永続化されたクエリを使用します。 命名の提案に従った場合は、という名前の永続的なクエリを作成しました。 `adventure-list` 内 `your-project` エンドポイントを選択し、 `persistedQueryName` 変数を `your-project/adventure-list`:

   ```javascript
   //
   // TODO: Use your persisted query here
   //
   persistedQueryName = 'your-project/adventure-list';
   ```

1. この変更がおこなわれると、アプリが自動的に更新され、永続化されたクエリからに生の JSON 応答を出力します。 `#output` div. エラーメッセージが表示された場合は、コンソールで詳細を確認してください。 詳細 [Slack](https://adobe-dx-support.slack.com) この手順でまだ問題が発生している場合は、をクリックします。

1. この JSON には、アプリで必要な正確なプロパティが含まれていますか？ そうでない場合は、 [GraphQL API を使用したコンテンツの抽出](https://experience.adobe.com/experiencemanager/learn/extract_content_using_graphql) 変更を加えるための学習ガイドです。 完了したら、忘れずにクエリを保存して公開してください。

## JSON レンダリングの変更 {#change-rendering}

JSON は、そのまま `pre` タグに貼り付けます。これはあまり創造的ではありません。 CodePen を切り替えて、 `resultToDom()` 関数を使用して、より興味深い結果を生成するために JSON 応答を繰り返し処理する方法を説明する代わりに、関数を使用する必要があります。

1. この変更を行うには、37 行目をコメントアウトし、40 行目からコメントを削除します。

   ```javascript
   // Output the results to a pre tag
   //resultToPreTag(queryResult);
   
   // Alternatively, build a colorful div structure with the JSON results and render images inline
   resultToDom(queryResult);
   ```

1. また、この関数は、JSON 応答に含まれる画像を `img` タグを使用します。 この **冒険** 作成したコンテンツフラグメントには画像が含まれていません。 `aem-demo-assets/adventures-all` 行 25 を変更して永続化されたクエリ

   ```javascript
   persistedQueryName = 'aem-demo-assets/adventures-all';
   ```

このクエリにより、画像と `resultToDom()` 関数はそれらをインラインでレンダリングします。

![adventures-all クエリと resultToDom レンダリング関数の結果](assets/do-not-localize/adventures-all-query-result.png)

モデルとクエリの構築が完了したので、コンテンツチームは簡単に引き継ぐことができます。 次のモジュールでは、コンテンツ作成者のフローを示します。
