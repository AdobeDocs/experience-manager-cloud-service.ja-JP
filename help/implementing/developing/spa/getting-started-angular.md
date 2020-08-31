---
title: AEMでのAngularの使用の手引き
description: この記事では、サンプルのSPAアプリケーションを紹介し、その組み合わせ方法を説明し、Angularフレームワークを使用して独自のSPAをすばやく習得できます。
translation-type: tm+mt
source-git-commit: ccde1459090bb9f801d753cb7314e2bc7249f72e
workflow-type: tm+mt
source-wordcount: '995'
ht-degree: 27%

---


# AEMでのAngularの使用の手引き {#getting-started-with-spas-in-aem-using-angular}

単一ページアプリケーション（SPA）により、Web サイトのユーザーに魅力的なエクスペリエンスを提供することができます。開発者は SPA フレームワークを使用してサイトを構築したいと考え、作成者はそうして構築されたサイトのコンテンツを AEM 内でシームレスに編集したいと考えています。

SPA オーサリング機能には、AEM 内で SPA をサポートするための包括的なソリューションが用意されています。この記事では、AngularフレームワークのシンプルなSPAアプリケーションを紹介し、その組み合わせ方法を説明します。これにより、独自のSPAをすばやく使い始めることができます。

>[!NOTE]
>
>この記事はAngularフレームワークに基づいています。 対応するReactフレームワークのドキュメントについては、AEMの「SPAを使用する前に — React」を参照して [ください](getting-started-react.md)。

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

このドキュメントでは、シンプル化されたSPAの構造を順を追って説明し、その仕組みを説明して、独自のSPAに適用します。

## 依存関係、設定、ビルド {#dependencies-configuration-and-building}

サンプルSPAは、期待されるAngularディペンデンシーに加えて、追加のライブラリを利用してSPAの作成をより効率的にできます。

### 依存関係 {#dependencies}

この `package.json` ファイルは、SPAパッケージ全体の要件を定義します。 必要最小限のAEM依存関係を以下に示します。

```
"dependencies": {
  "@adobe/cq-angular-editable-components": "~1.0.3",
  "@adobe/cq-spa-component-mapping": "~1.0.3",
  "@adobe/cq-spa-page-model-manager": "~1.0.4"
}
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
    clientLibRoot: "./../content/jcr_root/apps/my-angular-app/clientlibs",

    libs: {
        name: "my-angular-app",
        allowProxy: true,
        categories: ["my-angular-app"],
        embed: ["my-angular-app.responsivegrid"],
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

`"build": "ng build --build-optimizer=false && clientlib",`

ビルドが完了したら、パッケージを AEM インスタンスにアップロードできます。

### AEM プロジェクトアーキタイプ {#aem-project-archetype}

AEMプロジェクトでは、 [AEM Project Archetype](https://docs.adobe.com/content/help/ja-JP/experience-manager-core-components/using/developing/archetype/overview.html)（ReactまたはAngularを使用するSPAプロジェクトをサポートし、SPA SDKを利用する）を活用する必要があります。

## アプリケーション構造 {#application-structure}

前述のように依存関係を含め、アプリを作成すると、AEMインスタンスにアップロードできる有効なSPAパッケージが表示されます。

このドキュメントの次のセクションでは、AEMのSPAの構造、アプリケーションを駆動する重要なファイル、およびそれらの連携方法について説明します。

例としてシンプル化された画像コンポーネントが使用されますが、アプリケーションのすべてのコンポーネントは同じ概念に基づいています。

### app.module.ts {#app-module-ts}

The entry point into the SPA is the `app.module.ts` file shown here simplified to focus on the important content.

```
// app.module.ts
import { BrowserModule, BrowserTransferStateModule } from '@angular/platform-browser';
import { NgModule } from '@angular/core';
import { AppComponent } from './app.component';
import { SpaAngularEditableComponentsModule } from '@adobe/cq-angular-editable-components';
import { AppRoutingModule } from './app-routing.module';

@NgModule({
  imports: [ BrowserModule.withServerTransition({ appId: 'my-angular-app' }),
    SpaAngularEditableComponentsModule,
    AppRoutingModule,
    BrowserTransferStateModule ],
  providers: ...,
  declarations: [ ... ],
  entryComponents: [ ... ],
  bootstrap: [ AppComponent ]
})
export class AppModule {}
```

この `app.module.ts` ファイルはアプリの開始点で、初期プロジェクト設定が含まれ、を使用してアプリをブートストラップ `AppComponent` します。

#### 静的インスタンス化 {#static-instantiation}

コンポーネントテンプレートを使用して静的にコンポーネントをインスタンス化する場合、値はモデルからコンポーネントのプロパティに渡す必要があります。 モデルの値は属性として渡され、後でコンポーネントプロパティとして使用できます。

### app.component.ts {#app-component-ts}

ブ `app.module.ts` ートストラップが完了 `AppComponent`すると、アプリを初期化できます。ここでは、重要なコンテンツに焦点を当てるためのシンプル版を示します。

```
// app.component.ts
import { Component } from '@angular/core';
import { ModelManager } from '@adobe/cq-spa-page-model-manager';
import { Constants } from "@adobe/cq-angular-editable-components";

@Component({
  selector: 'app-root',
  template: `
    <router-outlet></router-outlet>
  `
})

export class AppComponent {
  items;
  itemsOrder;
  path;

  constructor() {
    ModelManager.initialize().then(this.updateData.bind(this));
  }

  private updateData(model) {
    this.path = model[Constants.PATH_PROP];
    this.items = model[Constants.ITEMS_PROP];
    this.itemsOrder = model[Constants.ITEMS_ORDER_PROP];
  }
}
```

### main-content.component.ts {#main-content-component-ts}

ページを処理することで、ここに示す `app.component.ts` 呼び出しを簡易版 `main-content.component.ts` で表示します。

```
import { Component } from '@angular/core';
import { ModelManagerService }     from '../model-manager.service';
import { ActivatedRoute } from '@angular/router';
import { Constants } from "@adobe/cq-angular-editable-components";

@Component({
  selector: 'app-main',
  template: `
    <aem-page class="structure-page" [attr.data-cq-page-path]="path" [cqPath]="path" [cqItems]="items" [cqItemsOrder]="itemsOrder" ></aem-page>
  `
})

export class MainContentComponent {
  items;
  itemsOrder;
  path;

  constructor( private route: ActivatedRoute,
    private modelManagerService: ModelManagerService) {
    this.modelManagerService.getData({ path: this.route.snapshot.data.path }).then((data) => {
      this.path = data[Constants.PATH_PROP];
      this.items = data[Constants.ITEMS_PROP];
      this.itemsOrder = data[Constants.ITEMS_ORDER_PROP];
    });
  }
}
```

`MainComponent` は、ページモデルの JSON 表現を取り込み、コンテンツを処理してページの各要素をラップ／デコレートします。`Page` のその他の詳細については、[SPA ブループリント](blueprint.md)のドキュメントを参照してください。

### image.component.ts {#image-component-ts}

は、コンポ `Page` ーネントで構成されています。 JSONを取り込むと、は次に示すようなコンポーネントを処理 `Page` で `image.component.ts` きます。

```
/// image.component.ts
import { Component, Input } from '@angular/core';

const ImageEditConfig = {

    emptyLabel: 'Image',

    isEmpty: function(cqModel) {
        return !cqModel || !cqModel.src || cqModel.src.trim().length < 1;
    }
};

@Component({
  selector: 'app-image',
  templateUrl: './image.component.html',
})

export class ImageComponent {
  @Input() src: string;
  @Input() alt: string;
  @Input() title: string;
}

MapTo('my-angular-app/components/image')(ImageComponent, ImageEditConfig);
```

AEM の SPA の中核概念は、SPA コンポーネントを AEM コンポーネントにマッピングし、コンテンツが変更されたときにコンポーネントも更新する（またはその逆も含む）というものです。See the document [SPA Editor Overview](editor-overview.md) for an summary of this communication model.

`MapTo('my-angular-app/components/image')(Image, ImageEditConfig);`

`MapTo` メソッドは、SPA コンポーネントを AEM コンポーネントにマッピングします。単一の文字列または文字列の配列の使用に対応しています。

`ImageEditConfig` は、エディターがプレースホルダーを生成するために必要なメタデータを提供することで、コンポーネントのオーサリング機能の有効化に関与する設定オブジェクトです。

コンテンツがない場合は、空のコンテンツを表すラベルがプレースホルダーとして提供されます。

#### 動的に渡されるプロパティ {#dynamically-passed-properties}

モデルからのデータは、コンポーネントのプロパティとして動的に渡されます。

### image.component.html {#image-component-html}

最後に、でイメージをレンダリングでき `image.component.html`ます。

```
// image.component.html
<img [src]="src" [alt]="alt" [title]="title"/>
```

## SPAコンポーネント間での情報の共有 {#sharing-information-between-spa-components}

単一ページのアプリケーション内のコンポーネントが情報を共有する場合は、定期的に必要となります。 これを行う方法には、次に示すように、複雑さを増す順序でいくつか推奨されます。

* **オプション1:** utilクラスを純粋なオブジェクト指向のソリューションとして使用するなど、ロジックを一元化し、必要なコンポーネントにブロードキャストします。
* **オプション2:** NgRxなどのステートライブラリを使用して、コンポーネントの状態を共有します。
* **オプション3:** コンテナコンポーネントをカスタマイズおよび拡張することで、オブジェクト階層を活用します。

## 次の手順 {#next-steps}

* [AEMでのSPAの使用の手引き](getting-started-react.md) （Reactを使用）では、AEMのSPAエディタで動作する基本的なSPAの構築方法を示しています。
* [「SPA Editor Overview](editor-overview.md) 」では、AEMとSPAの間の通信モデルの詳細について説明しています。
* [WKND SPA Project](wknd-tutorial.md) （WKND SPAプロジェクト）は、AEMで単純なSPAプロジェクトを実装するためのステップバイステップのチュートリアルです。
* [SPAの動的モデルとコンポーネントのマッピング](model-to-component-mapping.md) (DSP)では、動的モデルとコンポーネントのマッピング、およびAEMのSPA内での動作について説明しています。
* [SPA Blueprint](blueprint.md) オファーは、ReactやAngular以外のフレームワーク用にAEMでSPAを実装したり、単に理解を深めたい場合に備えて、AEM用SPA SDKの仕組みを深く掘り下げます。
