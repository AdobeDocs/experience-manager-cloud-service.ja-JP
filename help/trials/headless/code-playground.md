---
title: JavaScript で JSON コンテンツを取得
description: CodePen アプリとAEM Headless Client for JavaScript を使用して、体験環境から JSON コンテンツを取得する方法を説明します。
hidefromtoc: true
index: false
source-git-commit: 3aff5ef2fb9ecdd815f0bc1a813d3a3982b4e0ed
workflow-type: tm+mt
source-wordcount: '800'
ht-degree: 0%

---


# JavaScript で JSON コンテンツを取得 {#fetch-json}

>[!CONTEXTUALHELP]
>id="aemcloud_sites_trial_fetch_json_with_javascript"
>title="JavaScript で JSON コンテンツを取得"
>abstract="CodePen アプリとAEM Headless Client for JavaScript を使用して、体験環境から JSON コンテンツを取得する方法を説明します。"

>[!CONTEXTUALHELP]
>id="aemcloud_sites_trial_fetch_json_with_javascript_guide"
>title="サンプルの CodePen アプリケーションを起動します。"
>abstract="最小限の CodePen アプリを組み立て、GraphQLで永続的なクエリを使用して、体験環境から JSON データを取得する方法を紹介しました。<br><br>以下をクリックして CodePen の例を起動し、このガイドに従って詳細を確認します。"

>[!CONTEXTUALHELP]
>id="aemcloud_sites_trial_fetch_json_with_javascript_guide_footer"
>title="このモジュールでは、AEM Headless Client for JavaScript を使用して、GraphQLで保持されたクエリを使用して体験環境から JSON データを取得する方法を学びました。<br><br>これで、このクライアントを使用して、独自の Web アプリケーション内からデータを使用する方法を理解できます。"
>abstract=""

## はじめに {#intro}

最初に、CodePen アプリを使用します。これは、JSON データを取得する際に、 [JavaScript 用AEMヘッドレスクライアント](https://github.com/adobe/aem-headless-client-js). サンプルアプリは、基になるコンテンツフラグメントモデルの構造に関係なく、返される JSON コンテンツをレンダリングするように設計されています。 CodePen アプリは、エラーが発生した場合に詳細を表示しようとします。そのため、アプリの下部のウィンドウに次のエラーメッセージが表示される場合があります。

```
{
  "status": "Failed to fetch persisted query: your-project/USE-YOUR-QUERY-HERE from publishHost: https://publish-p00000-e12345.adobeaemcloud.com",
  "message": "[AEMHeadless:REQUEST_ERROR] General Request error: Failed to fetch."
}
```

前のモジュールで保存して公開した、永続化されたクエリをアプリが使用するように設定されていないので、このエラーが発生すると考えられます。 次の手順で、特定のクエリからデータを取得するようにアプリを設定します。

## CodePen のチュートリアル {#code-walkthrough}

CodePen の JS(JavaScript) ペインには、サンプルアプリの脳が含まれています。 2 行目から、JavaScript 用AEMヘッドレスクライアントを Skypack CDN から読み込みます。 Skypack は、ビルド手順を必要とせずに開発を容易にするために使用されますが、独自のプロジェクトでAEM Headless Client と NPM または Yarn を使用することもできます。 使用手順については、 [README](https://github.com/adobe/aem-headless-client-js#aem-headless-client-for-javascript) を参照してください。

```
import AdobeAemHeadlessClientJs from 'https://cdn.skypack.dev/@adobe/aem-headless-client-js@v3.2.0';
```

6 行目では、公開ホストの詳細を `publishHost` クエリパラメーター。 これは、AEMヘッドレスクライアントがデータを取得するホストです。 これは通常はアプリにコード化されますが、CodePen アプリが異なる環境で簡単に動作できるように、クエリパラメーターを使用します。

CORS の問題を回避するために、プロキシAdobeIO Runtime 関数を使用するようにAEM Headless Client を 12 行目に設定します。 これは、独自のプロジェクトに必要なわけではありませんが、CodePen アプリが体験環境で動作するために必要になります。 プロキシ関数は、 `publishHost` クエリパラメーターで指定された値。

```
const aemHeadlessClient = new AdobeAemHeadlessClientJs({
  // Use a proxy to avoid CORS issues
  serviceURL: 'https://102588-505tanocelot.adobeioruntime.net/api/v1/web/aem/proxy',
  headers: {
    'aem-url': publishHost
  }
});
```

最後に、関数 `fetchJsonFromGraphQL()` は、AEMヘッドレスクライアントを使用して取得リクエストを実行するために使用されます。 コードが変更されるたびに呼び出されます。または、「Refetch」リンクを押すことでトリガーできます。 実際の `aemHeadlessClient.runPersistedQuery(..)` 呼び出しは 34 行目で発生します。 少し後で、この JSON データのレンダリング方法を変更しますが、現時点では、このデータを `#output` div を `resultToPreTag(queryResult)` 関数に置き換えます。

## 永続クエリからデータを取得 {#use-persisted-query}

行 25 で、アプリがデータを取得する、永続化されたGraphQLのクエリを示します。 永続化されたクエリ名は、プロジェクトの名前 ( `your-project`) に続いてスラッシュを付け、次にクエリ名を付けます。

を更新します。 `persistedQueryName` 変数を使用して、前のモジュールで作成した永続化されたクエリを使用します。 命名の提案に正確に従った場合は、次の名前の永続的なクエリを作成します。 `adventures` 内 `your-project` プロジェクトの場合は、 `persistedQueryName` 変数を `your-project/adventures`:

```
//
// TODO: Use your persisted query here
//
persistedQueryName = 'your-project/adventures';
```

この変更がおこなわれると、アプリが自動的に更新され、永続化されたクエリからに生の JSON 応答を出力します。 `#output` div. エラーメッセージが表示された場合は、コンソールで詳細を確認してください。

この JSON には、アプリで必要な正確なプロパティが含まれていますか？ そうでない場合は、AEM オーサー環境、ツール、GraphQL Query Editor に戻ります ( または、 `/aem/graphiql.html` パス ) を参照し、持続的なクエリに変更を加えます。 完了したら、クエリを保存して公開するのを忘れないでください。

## JSON レンダリングの変更 {#change-rendering}

現在、JSON は、 `pre` タグに貼り付けます。これはあまり創造的ではありません。 CodePen を切り替えて、 `resultToDom()` 関数を使用して、より興味深い結果を生成するために JSON 応答を繰り返し処理する方法を説明する代わりに、関数を使用する必要があります。

この変更を行うには、37 行目をコメントアウトし、40 行目からコメントを削除します。

```
// Output the results to a pre tag
//resultToPreTag(queryResult);

// Alternatively, build a colorful div structure with the JSON results and render images inline
resultToDom(queryResult);
```

また、この関数は、JSON 応答に含まれる画像を `img` タグを使用します。 作成した「アドベンチャー」コンテンツフラグメントに画像が含まれていない場合は、 `aem-demo-assets/adventures-all` 行 25 を変更して永続化されたクエリ

```
persistedQueryName = 'aem-demo-assets/adventures-all';
```

このクエリにより、画像と `resultToDom()` 関数はそれらをインラインでレンダリングします。

![adventures-all クエリと resultToDom レンダリング関数の結果](assets/do-not-localize/adventures-all-query-result.png)
