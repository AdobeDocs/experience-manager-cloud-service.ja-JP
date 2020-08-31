---
title: AEMでのSPAの使用の手引き(React)
description: この記事では、サンプルのSPAアプリケーションを紹介し、SPAの組み合わせ方法を説明し、Reactフレームワークを使用して独自のSPAを使用して迅速に運用を開始できます。
translation-type: tm+mt
source-git-commit: 4652ab5a064d1ad397eb8eebd9dd92f7c8bb1c21
workflow-type: tm+mt
source-wordcount: '1145'
ht-degree: 37%

---


# AEMでのSPAの使用の手引き(React) {#getting-started-with-spas-in-aem-using-react}

単一ページアプリケーション（SPA）により、Web サイトのユーザーに魅力的なエクスペリエンスを提供することができます。開発者は SPA フレームワークを使用してサイトを構築したいと考え、作成者はそうして構築されたサイトのコンテンツを AEM 内でシームレスに編集したいと考えています。

SPA オーサリング機能には、AEM 内で SPA をサポートするための包括的なソリューションが用意されています。この記事では、ReactフレームワークのシンプルなSPAアプリケーションを紹介し、その組み合わせ方法を説明します。これにより、独自のSPAを使用してすばやく作業を開始できます。

>[!NOTE]
>
>この記事はReactフレームワークに基づいています。 Angularフレームワークの対応するドキュメントについては、AEMのSPAの [使用の手引き — Angularを参照してください](getting-started-angular.md)。

## 概要 {#introduction}

この記事では、シンプルな SPA の基本的な機能と、SPA を運用するための最低条件の概要を説明します。

AEMでのSPAの動作方法の詳細については、次のドキュメントを参照してください。

* [SPAの概要とチュートリアル](introduction.md)
* [SPA エディターの概要](editor-overview.md)
* [SPA ブループリント](blueprint.md)

>[!NOTE]
>
>SPA内でコンテンツをオーサリングするには、コンテンツをAEMに格納し、コンテンツモデルによって公開する必要があります。
>
>AEM以外で開発されたSPAは、コンテンツモデル契約に従わない場合は認証できません。

このドキュメントでは、Reactフレームワークを使用して作成されたシンプルなSPAの構造を順を追って説明し、その仕組みを説明して、この理解を独自のSPAに適用します。

## 依存関係、設定、ビルド {#dependencies-configuration-and-building}

サンプルの SPA では、必要な React の依存関係以外に、追加のライブラリも利用して SPA の作成を効率化できます。

### 依存関係 {#dependencies}

この `package.json` ファイルは、SPAパッケージ全体の要件を定義します。 動作中のSPAに対するAEMの最小依存関係を以下に示します。

```
  "dependencies": {
    "@adobe/cq-react-editable-components": "~1.0.3",
    "@adobe/cq-spa-component-mapping": "~1.0.3",
    "@adobe/cq-spa-page-model-manager": "~1.0.4"
  }
```

このサンプルは React フレームワークに基づいているので、`package.json` ファイルには必須となる React 固有の依存関係が 2 つあります。

```
 react
 react-dom
```

The `aem-clientlib-generator` is leveraged to make the creation of client libraries automatic as part of the build process.

`"aem-clientlib-generator": "^1.4.1",`

詳しくは、[GitHub のこちらのページ](https://github.com/wcm-io-frontend/aem-clientlib-generator)を参照してください。

The `aem-clientlib-generator` is configured in the `clientlib.config.js` file as follows.

```
module.exports = {
    // default working directory (can be changed per 'cwd' in every asset option)
    context: __dirname,

    // path to the clientlib root folder (output)
    clientLibRoot: "./../content/jcr_root/apps/my-react-app/clientlibs",

    libs: {
        name: "my-react-app",
        allowProxy: true,
        categories: ["my-react-app"],
        embed: ["my-react-app.responsivegrid"],
        jsProcessor: ["min:gcc"],
        serializationFormat: "xml",
        assets: {
            js: [
                "dist/**/*.js"
            ],
            css: [
                "dist/**/*.css"
            ]
        }
    }
};
```

### ビルド {#building}

アプリの実際のビルドでは、クライアントライブラリの自動作成用の aem-clientlib-generator 以外に、トランスパイル用に [Webpack](https://webpack.js.org/) も利用します。そのため、build コマンドは以下のようになります。

`"build": "webpack && clientlib --verbose"`

ビルドが完了したら、パッケージを AEM インスタンスにアップロードできます。

### AEM プロジェクトアーキタイプ {#aem-project-archetype}

AEMプロジェクトでは、 [AEM Project Archetype](https://docs.adobe.com/content/help/ja-JP/experience-manager-core-components/using/developing/archetype/overview.html)（ReactまたはAngularを使用するSPAプロジェクトをサポートし、SPA SDKを利用する）を活用する必要があります。

## アプリケーション構造 {#application-structure}

前述のように依存関係を含め、アプリを作成すると、AEMインスタンスにアップロードできる有効なSPAパッケージが表示されます。

このドキュメントの次のセクションでは、AEMのSPAの構造、アプリケーションを駆動する重要なファイル、およびそれらの連携方法について説明します。

例としてシンプル化された画像コンポーネントが使用されますが、アプリケーションのすべてのコンポーネントは同じ概念に基づいています。

### index.js {#index-js}

SPA のエントリポイントはもちろん `index.js` ファイルです。このファイルの内容を以下に示していますが、重要な部分のみに焦点を当てるために簡略化されています。

```
import ReactDOM from 'react-dom';
import App from './App';
import { ModelManager, Constants } from "@adobe/cq-spa-page-model-manager";

...

ModelManager.initialize().then((pageModel) => {
ReactDOM.render(
    <App cqChildren={pageModel[Constants.CHILDREN_PROP]} cqItems={pageModel[Constants.ITEMS_PROP]} cqItemsOrder={pageModel[Constants.ITEMS_ORDER_PROP]} cqPath={ModelManager.rootPath} locationPathname={ window.location.pathname }/>
, document.getElementById('page'));

});
```

`index.js` の主要機能は、`ReactDOM.render` 関数を使用して、DOM 内でアプリケーションをインジェクトする場所を決めることです。

これは、この関数の標準的な使用方法であり、この例のアプリに固有のものではありません。

#### 静的インスタンス化 {#static-instantiation}

コンポーネントテンプレート（JSXなど）を使用して静的にコンポーネントをインスタンス化する場合は、モデルからコンポーネントのプロパティに値を渡す必要があります。

### App.js {#app-js}

アプリをレンダリングすることで、`index.js` は `App.js` を呼び出します。このファイルの内容を以下に示していますが、重要な部分のみに焦点を当てるために簡略化されています。

```
import {Page, withModel } from '@adobe/cq-react-editable-components';

...

class App extends Page {
...
}

export default withModel(App);
```

`App.js` 主に、アプリを構成するルートコンポーネントをラップする役割を果たします。 アプリのエントリポイントは、ページです。

### Page.js {#page-js}

このページをレンダリングすると、ここに示す `App.js` 呼び出しをシンプル版 `Page.js` で表示します。

```
import {Page, MapTo, withComponentMappingContext } from "@adobe/cq-react-editable-components";

...

class AppPage extends Page {
...
}

MapTo('my-react-app/components/structure/page')(withComponentMappingContext(AppPage));
```

In this example the `AppPage` class extends `Page`, which contains the inner-content methods that can then be used.

`Page` は、ページモデルの JSON 表現を取り込み、コンテンツを処理してページの各要素をラップ／デコレートします。Further details on the `Page` can be found in the document [SPA Blueprint.](blueprint.md)

### Image.js {#image-js}

ページがレンダリングされると、以下の `Image.js` などのコンポーネントがレンダリング可能になります。

```
import React, {Component} from 'react';
import {MapTo} from '@adobe/cq-react-editable-components';

require('./Image.css');

const ImageEditConfig = {

    emptyLabel: 'Image',

    isEmpty: function() {
        return !this.props || !this.props.src || this.props.src.trim().length < 1;
    }
};

class Image extends Component {

    render() {
        return (<img src={this.props.src}>);
    }
}

MapTo('my-react-app/components/content/image')(Image, ImageEditConfig);
```

AEM の SPA の中核概念は、SPA コンポーネントを AEM コンポーネントにマッピングし、コンテンツが変更されたときにコンポーネントも更新する（またはその逆も含む）というものです。この通信モデルの概要については、「ドキュメント [SPAエディタの概要](editor-overview.md) 」を参照してください。

`MapTo('my-react-app/components/content/image')(Image, ImageEditConfig);`

`MapTo` メソッドは、SPA コンポーネントを AEM コンポーネントにマッピングします。単一の文字列または文字列の配列の使用に対応しています。

`ImageEditConfig` は、エディターがプレースホルダーを生成するために必要なメタデータを提供することで、コンポーネントのオーサリング機能の有効化に関与する設定オブジェクトです。

コンテンツがない場合は、空のコンテンツを表すラベルがプレースホルダーとして提供されます。

#### 動的に渡されるプロパティ {#dynamically-passed-properties}

モデルからのデータは、コンポーネントのプロパティとして動的に渡されます。

## 編集可能コンテンツの書き出し {#exporting-editable-content}

コンポーネントをエクスポートして編集可能な状態を維持することができます。

```
import React, { Component } from 'react';
import { MapTo } from '@cq/cq-react-editable-components';

...

const EditConfig = {...}

class PageClass extends Component {...};

...

export default MapTo('my-react-app/react/components/structure/page')(PageClass, EditConfig);
```

The `MapTo` function returns a `Component` which is the result of a composition that extends the provided `PageClass` with the class names and attributes that enable the authoring. このコンポーネントは後でエクスポートし、アプリケーションのマークアップでインスタンス化できます。

When exported using the `MapTo` or `withModel` functions, the `Page` component, is wrapped with a `ModelProvider` component which provides standard components access to the latest version of the page model or a precise location in that page model.

詳しくは、[SPA ブループリントのドキュメント](blueprint.md)を参照してください。

>[!NOTE]
>
>デフォルトでは、`withModel` 関数を使用するとコンポーネントのモデル全体を受け取ります。

## SPAコンポーネント間での情報の共有 {#sharing-information-between-spa-components}

単一ページのアプリケーション内のコンポーネントが情報を共有する場合は、定期的に必要となります。 これを行う方法には、次に示すように、複雑さを増す順序でいくつか推奨されます。

* **オプション1:** 例えばReact Contextを使用して、ロジックを一元化し、必要なコンポーネントにブロードキャストします。
* **オプション2:** Reduxなどのステートライブラリを使用して、コンポーネントの状態を共有します。
* **オプション3:** コンテナコンポーネントをカスタマイズおよび拡張することで、オブジェクト階層を活用します。

## 次の手順 {#next-steps}

* [AEMでのSPAの使用の手引き](getting-started-angular.md) （Angularを使用）は、AEMでAngularを使用してSPAエディタを使用するために基本SPAを構築する方法を示しています。
* [「SPA Editor Overview](editor-overview.md) 」では、AEMとSPAの間の通信モデルの詳細について説明しています。
* [WKND SPA Project](wknd-tutorial.md) （WKND SPAプロジェクト）は、AEMで単純なSPAプロジェクトを実装するためのステップバイステップのチュートリアルです。
* [SPAの動的モデルとコンポーネントのマッピング](model-to-component-mapping.md) (DSP)では、動的モデルとコンポーネントのマッピング、およびAEMのSPA内での動作について説明しています。
* [SPA Blueprint](blueprint.md) オファーは、ReactやAngular以外のフレームワーク用にAEMでSPAを実装したり、単に理解を深めたい場合に備えて、AEM用SPA SDKの仕組みを深く掘り下げます。
