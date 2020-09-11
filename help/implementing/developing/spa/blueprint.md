---
title: SPA ブループリント
description: このドキュメントでは、AEM内に編集可能なSPAコンポーネントを実装するためにSPAフレームワークが満たす必要がある、フレームワークに依存しない一般的な契約について説明します。
translation-type: tm+mt
source-git-commit: 8bdb7bbe80a4e22bb2b750c0719c6db745133392
workflow-type: tm+mt
source-wordcount: '2058'
ht-degree: 10%

---


# SPA ブループリント {#spa-blueprint}

作成者がAEM SPAエディターを使用してSPAのコンテンツを編集できるようにするには、SPAが満たす必要がある要件があります。

## 概要 {#introduction}

このドキュメントでは、AEM内に編集可能なSPAコンポーネントを実装するために、SPAフレームワークが満たす必要がある一般的な契約(AEMサポート層など)について説明します。

作成者がAEMページエディターを使用して、単一ページアプリケーションのフレームワークで公開されるデータを編集できるようにするには、AEMリポジトリ内のアプリケーション用に保存されたデータのセマンティックを表すモデルの構造を解釈できる必要があります。 この目標を達成するために、フレームワークに依存しない2つのライブラリが用意されています。と `PageModelManager` があり `ComponentMapping`ます。

>[!NOTE]
>
>以下の要件は、フレームワークには依存しません。要件が満たされると、（モジュール、コンポーネントおよびサービスで構成された）フレームワーク固有のレイヤーが提供されます。
>
>**AEMのReactフレームワークとAngularフレームワークでは、これらの要件は既に満たされています。** この青写真の要件は、AEMで使用する別のフレームワークを実装する場合にのみ適用されます。

>[!CAUTION]
>
>AEMのSPA機能はフレームワークに依存しませんが、現在、ReactフレームワークとAngularフレームワークのみがサポートされています。

## PageModelManager {#pagemodelmanager}

この `PageModelManager` ライブラリは、SPAプロジェクトで使用するNPMパッケージとして提供されます。 SPA に付属し、データモデルマネージャーとして機能します。

SPA に代わり、実際のコンテンツ構造を表す JSON 構造の取得および管理を抽象化します。また、SPAと同期して、コンポーネントを再レンダリングする必要が生じた時点を通知する必要もあります。

NPMパッケージ「 [@adobe/aem-spa-model-manager」を参照してください。](https://www.npmjs.com/package/@adobe/aem-spa-model-manager)

ライブラリを初期化する `PageModelManager`とき、ライブラリは、最初に、指定されたアプリケーションのルートモデルを読み込みます（パラメーター、メタプロパティまたは現在のURLを使用）。 ライブラリが、現在のページのモデルが取得するルートモデルの一部でないことを識別し、それを子ページのモデルとして含める場合。

![ページモデルの統合](assets/page-model-consolidation.png)

### ComponentMapping {#componentmapping}

The `ComponentMapping` module is provided as an NPM package to the front-end project. フロントエンドコンポーネントが格納され、SPAがフロントエンドコンポーネントをAEMリソースタイプにマッピングする手段を提供します。 これにより、アプリケーションのJSONモデルを解析する際に、コンポーネントの動的な解決が可能になります。

モデル内の各項目には、AEMリソースタイプを表示する `:type` フィールドが含まれます。 マウントすると、フロントエンドコンポーネントは、基になるライブラリから受け取ったモデルのフラグメントを使用して自分自身をレンダリングできます。

#### 動的モデルとコンポーネントのマッピング {#dynamic-model-to-component-mapping}

AEM向けJavaScript SPA SDKでの動的モデルとコンポーネントのマッピングの発生方法について詳しくは、「SPAの [動的モデルとコンポーネントのマッピング](model-to-component-mapping.md)」を参照してください。

### フレームワーク固有の層 {#framework-specific-layer}

フロントエンドフレームワークごとに第3のレイヤーを実装する必要があります。 この3つ目のライブラリは、基礎となるライブラリとの対話を担当し、データモデルと対話するための、適切に統合され、使いやすい一連のエントリポイントを提供します。

このドキュメントの残りの部分では、この中間フレームワーク固有の層の要件を説明し、フレームワークに依存しないことを目指しています。 次の要件に従うことで、プロジェクトコンポーネントがデータモデルの管理を担当する基礎となるライブラリとやり取りするためのフレームワーク固有のレイヤーを提供できます。

## 一般的な概念 {#general-concepts}

### ページモデル {#page-model}

ページのコンテンツ構造は AEM に保存されます。ページのモデルは、SPA コンポーネントのマッピングとインスタンス化に使用されます。SPA の開発者は、SPA コンポーネントを作成して、AEM コンポーネントにマッピングします。これを行うには、リソースタイプ(またはAEMコンポーネントへのパス)を一意のキーとして使用します。

SPAコンポーネントは、ページモデルと同期していて、それに応じてコンテンツに変更を加えて更新する必要があります。 指定のページモデル構造に従って、コンポーネントをその場でインスタンス化するには、動的コンポーネントを利用したパターンを使用する必要があります。

### メタフィールド {#meta-fields}

The page model leverages the JSON Model Exporter, which is itself based on the [Sling Model](https://sling.apache.org/documentation/bundles/models.html) API. エクスポート可能なSlingモデルは、基になるライブラリがデータモデルを解釈できるようにするために、次のフィールドのリストを公開します。

* `:type`:AEMリソースのタイプ（デフォルト=リソースタイプ）
* `:children`:現在のリソースの階層の子。 子は現在のリソースの内部コンテンツに含まれていません（ページを表す項目に含まれています）
* `:hierarchyType`:リソースの階層タイプ。 は、 `PageModelManager` 現在、ページタイプをサポートしています

* `:items`:現在のリソースの子コンテンツリソース(ネストされた構造、コンテナにのみ存在)
* `:itemsOrder`:子供のリストを命じた。 JSONマップオブジェクトは、フィールドの順序を保証しません。 マップと現在の配列の両方を持つことで、APIのコンシューマは、両方の構造体の利点を持ちます。
* `:path`:項目のコンテンツパス（ページを表す項目に存在）

[AEM コンテンツサービスの利用](https://docs.adobe.com/content/help/en/experience-manager-learn/getting-started-with-aem-headless/overview.html)も参照してください。

### フレームワーク固有のモジュール {#framework-specific-module}

懸念を分けることで、プロジェクトの実装を容易にすることができます。 したがって、npm固有のパッケージを提供する必要があります。 このパッケージは、基本モジュール、サービス、コンポーネントの集積と公開を担当します。 これらのコンポーネントは、データモデルの管理ロジックをカプセル化し、プロジェクトのコンポーネントが予期するデータへのアクセスを提供する必要があります。 このモジュールは、基になるライブラリの有用なエントリポイントを推移的に公開する役割も果たします。

ライブラリの相互運用性を容易にするため、Adobeはフレームワーク固有のモジュールに対し、以下のライブラリをバンドルするよう勧告する。 必要に応じて、レイヤーは基になるAPIをカプセル化し、調整してから、プロジェクトに公開できます。

* [@adobe/aem-spa-model-manager](https://www.npmjs.com/package/@adobe/aem-spa-model-manager)
* [@adobe/aem-spa-component-mapping](https://www.npmjs.com/package/@adobe/aem-spa-component-mapping)

#### 実装 {#implementations}

#### React {#react}

npmモジュール： [@adobe/aem-react-editable-components](https://www.npmjs.com/package/@adobe/aem-react-editable-components)

#### 角 {#angular}

npmモジュール： [@adobe/aem-angular-editable-components](https://www.npmjs.com/package/@adobe/aem-angular-editable-components)

## メインサービスとコンポーネント {#main-services-and-components}

次のエンティティは、各フレームワークに固有のガイドラインに従って実装する必要があります。 フレームワークのアーキテクチャに基づいて、実装は大きく異なる場合がありますが、説明する機能を提供する必要があります。

### モデルプロバイダ {#the-model-provider}

プロジェクトコンポーネントは、モデルのフラグメントへのアクセスをモデルプロバイダーに委任する必要があります。 次に、モデルプロバイダーは、モデルの指定したフラグメントに対する変更をリッスンし、更新されたモデルを委任コンポーネントに返します。

これを行うには、モデルプロバイダがに登録する必要があり [`PageModelManager`](#pagemodelmanager)ます。 次に、変更が発生すると、その変更が受け取られ、更新されたデータが委任コンポーネントに渡されます。 慣例により、モデルのフラグメントを伝達する委任コンポーネントで使用可能にされたプロパティに名前が付けられ `cqModel`ます。 このプロパティはコンポーネントに自由に提供できますが、フレームワークアーキテクチャとの統合、検出可能性、使いやすさなどの側面を考慮する必要があります。

### コンポーネントのHTMLデコレーター {#the-component-html-decorator}

コンポーネントデコレーターは、各コンポーネントインスタンスの要素の外側のHTMLを、ページエディターで予想される一連のデータ属性とクラス名でデコレートする役割を持ちます。

#### コンポーネントの宣言 {#component-declaration}

プロジェクトのコンポーネントによって生成される外側のHTML要素に、次のメタデータを追加する必要があります。 ページエディターで対応する編集設定を取得できるようになります。

* `data-cq-data-path`:リソースへのパス。 `jcr:content`

#### 機能の宣言とプレースホルダの編集 {#editing-capability-declaration-and-placeholder}

次のメタデータとクラス名は、プロジェクトのコンポーネントによって生成される外側のHTML要素に追加する必要があります。 ページエディターでオファー関連の機能を有効にします。

* `cq-placeholder`:空のコンポーネントのプレースホルダーを識別するクラス名
* `data-emptytext`:コンポーネントインスタンスが空の場合にオーバーレイによって表示されるラベル

**空のコンポーネントのプレースホルダー**

各コンポーネントは、外側のHTML要素をデコレートする機能を使用して拡張する必要があります。この機能は、コンポーネントが空であると識別された場合に、プレースホルダーと関連オーバーレイに固有のデータ属性とクラス名を使用して実行されます。

**コンポーネントの空白について**

* コンポーネントは論理的に空ですか？
* コンポーネントが空の場合、オーバーレイに表示されるラベルは何ですか。

### コンテナ {#container}

コンテナは、子コンポーネントを内包してレンダリングするためのコンポーネントです。これを行うには、コンテナがモデルの `:itemsOrder`、 `:items` および `:children` プロパティを繰り返します。

コンテナは、ライブラリのストアから子コンポーネントを動的に取得し [`ComponentMapping`](#componentmapping) ます。 次に、コンテナは、モデルプロバイダー機能で子コンポーネントを拡張し、最後にインスタンス化します。

### ページ {#page}

コンポー `Page` ネントはコンポー `Container` ネントを拡張します。 コンテナは、子ページを含む子コンポーネントを含み、レンダリングするためのコンポーネントです。 これを行うには、コンテナがモデルの `:itemsOrder`、、 `:items`および `:children` プロパティを反復します。 コンポーネントは、ライブラリのストアから子コンポーネントを動的に取得し `Page`[`ComponentMapping`](#componentmapping) ます。 子コンポーネント `Page` をインスタンス化します。

### レスポンシブグリッド {#responsive-grid}

レスポンシブグリッドコンポーネントはコンテナです。 列を表すモデルプロバイダーの特定のバリアントが含まれます。 レスポンシブグリッドとその列は、モデルに含まれる特定のクラス名で、プロジェクトのコンポーネントの外側のHTML要素を装飾する役割を持ちます。

レスポンシブグリッドコンポーネントは、AEMの対応するコンポーネントに事前にマッピングされている必要があります。このコンポーネントは複雑で、カスタマイズされることはほとんどありません。

#### 特定のモデルフィールド {#specific-model-fields}

* `gridClassNames:` レスポンシブグリッドに指定されたクラス名
* `columnClassNames:` レスポンシブ列に指定されたクラス名

npmリソース「 [@adobe/aem-react-editable-components」も参照してください。](https://www.npmjs.com/package/@adobe/aem-react-editable-components)

#### レスポンシブグリッドのプレースホルダー {#placeholder-of-the-responsive-grid}

SPAコンポーネントはレスポンシブグリッドなどのグラフィカルコンテナにマッピングされ、コンテンツの作成時に仮想の子プレースホルダーを追加する必要があります。 When the content of the SPA is being authored by the Page Editor, that content is embedded into the editor using an iframe and the `data-cq-editor` attribute is added to the document node of that content. 属性が存在する場合、ページに新しいコンポーネントを挿入する際に作成者が操作する領域を表すHTMLElementをコンテナに含める必要があります。 `data-cq-editor`

次に例を示します。

```
<div data-cq-data-path={"path/to/the/responsivegrid/*"} className="new section aem-Grid-newComponent"/>
```

>[!NOTE]
>
>この例で使用されているクラス名は、現時点ではページエディターで必須です。
>
>* `"new section"`：現在の要素がコンテナのプレースホルダーであることを示します。
>* `"aem-Grid-newComponent"`:レイアウトオーサリング用のコンポーネントを標準化します

>



#### コンポーネントのマッピング {#component-mapping}

基になる [`Component Mapping`](#componentmapping)`MapTo` ライブラリとその関数は、カプセル化して拡張し、現在のコンポーネントクラスと共に提供される編集設定に対する相対的な機能を提供できます。

```
const EditConfig = {

    emptyLabel: 'My Component',

    isEmpty: function() {
        return !this.props || !this.props.cqModel || this.props.cqModel.isEmpty;
    }
};

class MyComponent extends Component {

    render() {
        return <div className={'my-component'}></div>;
    }
}

MapTo('component/resource/path')(MyComponent, EditConfig);
```

上記の実装では、プロジェクトコンポーネントは、 [コンポーネントマッピング](#componentmapping) ストアに実際に登録される前に、空白機能で拡張されます。 これは、ライブラリをカプセル化して拡張し、設定オブジェクトのサポートを導入するこ [`ComponentMapping`](#componentmapping) とで行い `EditConfig` ます。

```
/**
 * Configuration object in charge of providing the necessary data expected by the page editor to initiate the authoring. The provided data will be decorating the associated component
 *
 * @typedef {{}} EditConfig
 * @property {String} [dragDropName]       If defined, adds a specific class name enabling the drag and drop functionality
 * @property {String} emptyLabel           Label to be displayed by the placeholder when the component is empty. Optionally returns an empty text value
 * @property {function} isEmpty            Should the component be considered empty. The function is called using the context of the wrapper component giving you access to the component model
 */

/**
 * Map a React component with the given resource types. If an {@link EditConfig} is provided the <i>clazz</i> is wrapped to provide edition capabilities on the AEM Page Editor
 *
 * @param {string[]} resourceTypes                      - List of resource types for which to use the given <i>clazz</i>
 * @param {class} clazz                                 - Class to be instantiated for the given resource types
 * @param {EditConfig} [editConfig]                     - Configuration object for enabling the edition capabilities
 * @returns {class}                                     - The resulting decorated Class
 */
ComponentMapping.map = function map (resourceTypes, clazz, editConfig) {};
```

## ページエディターとの契約 {#contract-with-the-page-editor}

プロジェクトコンポーネントは、少なくとも次のデータ属性を生成して、エディタが操作できるようにする必要があります。

* `data-cq-data-path`:によって提供されるコンポーネントの相対パス `PageModel` (例： `"root/responsivegrid/image"`)。 この属性はページに追加しないでください。

要約すると、編集可能としてページエディターで解釈されるために、プロジェクトコンポーネントは次の契約を守る必要があります。

* フロントエンドコンポーネントインスタンスをAEMリソースに関連付けるために、必要な属性を指定します。
* 空のプレースホルダーを作成できるように、期待される一連の属性とクラス名を指定します。
* アセットのドラッグ&amp;ドロップを可能にする、期待されるクラス名を指定します。

### 一般的なHTML要素の構造 {#typical-html-element-structure}

次のフラグメントは、ページコンテンツ構造の一般的な HTML 表現です。重要なポイントをいくつか示します。

* The responsive grid element carries class names prefixed with `aem-Grid--`
* The responsive column element carries class names prefixed with `aem-GridColumn--`
* 親グリッドの列でもあるレスポンシブグリッドは、前の2つのプレフィックスが同じ要素に表示されないなど、ラップされます
* Elements corresponding to editable resources carry a `data-cq-data-path` property. このドキュメントの「ページエディタ [との契約](#contract-wtih-the-page-editor) 」の節を参照してください。

```
<div data-cq-data-path="/content/page">
    <div class="aem-Grid aem-Grid--12 aem-Grid--default--12">
        <div class="aem-container aem-GridColumn aem-GridColumn--default--12" data-cq-data-path="/content/page/jcr:content/root/responsivegrid">
            <div class="aem-Grid aem-Grid--12 aem-Grid--default--12">
                <div class="cmp-image cq-dd-image aem-GridColumn aem-GridColumn--default--12" data-cq-data-path="/root/responsivegrid/image">
                    <img src="/content/we-retail-spa-sample/react/jcr%3acontent/root/responsivegrid/image.img.jpeg/1512113734019.jpeg">
                </div>
            </div>
        </div>
    </div>
</div>
```

## ナビゲーションとルーティング {#navigation-and-routing}

アプリがルーティングを所有している。 フロントエンド開発者は、まず、ナビゲーションコンポーネント(AEMナビゲーションコンポーネントにマッピング)を実装する必要があります。 このコンポーネントは、コンテンツのフラグメントを表示または非表示にする一連のルートと組み合わせて使用するURLリンクをレンダリングします。

基になる [`PageModelManager`](#pagemodelmanager) ライブラリとその [`ModelRouter`](routing.md) モジュール（デフォルトで有効）は、特定のリソースパスに関連付けられたモデルに対し、プリフェッチおよびアクセスを行います。

2つのエンティティはルーティングの概念に関連していますが、は、現在のアプリケーションの状態と同期して構成されたデータモデル [`ModelRouter`](routing.md)[`PageModelManager`](#pagemodelmanager) を使用しての読み込みのみを行います。

詳しくは、「 [SPAモデルのルーティング](routing.md) 」を参照してください。

## SPA in Action {#spa-in-action}

シンプルなSPAの動作を確認し、次のドキュメントに進んでSPAをテストします。

* [AEMでのSPAの使用の手引き](getting-started-react.md)。
* [Angularを使用したAEMでのSPAの使用の手引き](getting-started-angular.md)。

## 参考情報 {#further-reading}

AEM での SPA について詳しくは、次のドキュメントを参照してください。

* [SPAエディタ概要](editor-overview.md) :AEMのSPAと通信モデルの概要
