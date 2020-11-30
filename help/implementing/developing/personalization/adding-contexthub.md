---
title: ページへの ContextHub の追加とストアへのアクセス
description: ContextHub 機能を有効にし、ContextHub JavaScript ライブラリにリンクするには、ContextHub をページに追加します
translation-type: tm+mt
source-git-commit: 3277d7470c1abdcc1f759c87e2c1a7ffb3390f47
workflow-type: tm+mt
source-wordcount: '927'
ht-degree: 100%

---


# ページへの ContextHub の追加とストアへのアクセス {#adding-contexthub-to-pages-and-accessing-stores}

ContextHub 機能を有効にし、ContextHub JavaScript ライブラリにリンクするには、ContextHub をページに追加します。

ContextHub JavaScript API を使用すると、ContextHub が管理するコンテキストデータにアクセスできます。このページでは、コンテキストデータにアクセスおよび操作するための API の主な機能について簡単に説明します。詳細情報とコードのサンプルは、API リファレンスドキュメントへのリンクから確認できます。

## ページコンポーネントへの ContextHub の追加 {#adding-contexthub-to-a-page-component}

ContextHub 機能を有効にし、ContextHub JavaScript ライブラリにリンクするには、ページの `head` セクションに `contexthub` コンポーネントを含めます。ページコンポーネントの HTL コードは、次の例のようになります。

```xml
<sly data-sly-resource="${'contexthub' @ resourceType='granite/contexthub/components/contexthub'}"/>
```

ContextHub ツールバーをプレビューモードで表示するかどうかも設定する必要があります。[ContextHub UI の表示／非表示](configuring-contexthub.md#showing-and-hiding-the-contexthub-ui)を参照してください。

## ContextHub ストアについて {#about-contexthub-stores}

コンテキストデータを保持するには、ContextHub ストアを使用します。ContextHub には、すべてのストアタイプの基礎となる次のタイプのストアが用意されています。

* [PersistedStore](contexthub-api.md#contexthub-store-persistedstore)
* [SessionStore](contexthub-api.md#contexthub-store-sessionstore)
* [JSONPStore](contexthub-api.md#contexthub-store-persistedjsonpstore)
* [PersistedJSONPStore](contexthub-api.md#contexthub-store-persistedstore)

すべてのストアタイプは、[`ContextHub.Store.Core`](contexthub-api.md#contexthub-store-core) クラスの拡張です。新しいストアタイプの作成については、[カスタムストアの作成](extending-contexthub.md#creating-custom-store-candidates)を参照してください。ストアタイプのサンプルについては、[ContextHub ストア候補のサンプル](sample-stores.md)を参照してください。

### 永続モード {#persistence-modes}

ContextHub ストアは、次のいずれかの永続モードを使用します。

* **ローカル：** HTML5 localStorage を使用してデータを保持します。ローカルストレージは、セッションをまたがってブラウザー上に保持されます。
* **セッション：** HTML5 sessionStorage を使用してデータを保持します。セッションストレージは、ブラウザーセッションが持続する間、保持され、すべてのブラウザーウィンドウで使用可能です。
* **Cookie：**&#x200B;ブラウザーのデータストレージ用 cookie のネイティブサポートを使用します。cookie データは、HTTP 要求としてサーバーとの間で送受信されます。
* **Window.name：** window.name プロパティを使用してデータを保持します。
* **メモリ：** JavaScript オブジェクトを使用してデータを保持します。

デフォルトでは、ContextHub は「ローカル」永続モードを使用します。ブラウザーが HTML5 localStorage をサポートまたは許可していない場合は、「セッション」永続モードが使用されます。ブラウザーが HTML5 sessionStorage をサポートまたは許可していない場合は、「Window.name」永続モードが使用されます。

### ストアデータ {#store-data}

ストアデータは内部的にツリー構造を形成しており、値をプライマリタイプまたは複合オブジェクトとして追加できます。複合オブジェクトをストアに追加すると、オブジェクトのプロパティがデータツリーにブランチを形成します。例えば、次の複合オブジェクトを location という名前の空のストアに追加します。

```javascript
Object {
   number: 321,
   data: {
      city: "Basel",
      country: "Switzerland",
      details: {
         population: 173330,
         elevation: 260
      }
   }
}
```

ストアデータのツリー構造は、次のように概念化できます。

```text
/
|- number
|- data
      |- city
      |- country
      |- details
            |- population
            |- elevation
```

ツリー構造は、ストア内のデータ項目をキーと値のペアとして定義します。上記の例では、キー `/number` が値 `321` に対応し、キー `/data/country` が値 `Switzerland` に対応しています。

### オブジェクトの操作 {#manipulating-objects}

ContextHub には、JavaScript オブジェクトを操作するための [`ContextHub.Utils.JSON.tree`](contexthub-api.md#contexthub-utils-json-tree) クラスが用意されています。JavaScript オブジェクトをストアに追加する前またはストアから取得した後に、このクラスの関数を使用して JavaScript オブジェクトを操作します。

さらに、[`ContextHub.Utils.JSON`](contexthub-api.md#contexthub-utils-json) クラスには、オブジェクトを文字列にシリアライズしたり、文字列をオブジェクトにデシリアライズしたりするための関数があります。`JSON.parse` 関数および `JSON.stringify` 関数をネイティブに含まないブラウザーをサポートするには、このクラスを使用して JSON データを処理します。

## ContextHub ストアとのやり取り {#interacting-with-contexthub-stores}

ストアを JavaScript オブジェクトとして取得するには、[`ContextHub`](contexthub-api.md#ui-event-constants) JavaScript オブジェクトを使用します。ストアオブジェクトを取得したら、そのストアに格納されているデータを操作できます。ストアを取得するには、[`getAllStores`](contexthub-api.md#getallstores) 関数または [`getStore`](contexthub-api.md#getstore-name) 関数を使用します。

### ストアデータへのアクセス {#accessing-store-data}

[`ContexHub.Store.Core`](contexthub-api.md#contexthub-store-core) JavaScript クラスは、ストアデータとやり取りするための関数を定義します。次の関数は、オブジェクトに格納されている複数のデータ項目を保存および取得します。

* [addAllItems](contexthub-api.md#addallitems-tree-options)
* [getTree](contexthub-api.md#gettree-includeinternals)

個々のデータ項目は、一連のキーと値のペアとして保存されます。値を保存および取得するには、対応するキーを指定します。

* [getItem](contexthub-api.md#getitem-key)
* [setItem](contexthub-api.md#setitem-key-value-options)

カスタムストア候補は、ストアデータへのアクセスを提供する追加の関数を定義できます。

>[!NOTE]
>
>ContextHub は、デフォルトでは、パブリッシュサーバーを使用した現在のログインを認識しません。そうしたユーザーは ContextHub では「匿名」と見なされます。
>
>プロファイルストアを読み込むことで、ContextHub にログインユーザーを認識させることができます。[GitHub](https://github.com/Adobe-Marketing-Cloud/aem-sample-we-retail/blob/master/ui.apps/src/main/content/jcr_root/apps/weretail/components/structure/header/clientlib/js/utilities.js) でサンプルコードを参照してください。

### ContextHub のイベンティング {#contexthub-eventing}

ContextHub には、ストアイベントに自動的に対処できるようにするイベントフレームワークが含まれています。各ストアオブジェクトには、ストアの [`ContextHub.Utils.Eventing`](contexthub-api.md#contexthub-utils-eventing) プロパティとして使用できる [`eventing`](contexthub-api.md#eventing) オブジェクトが含まれています。JavaScript 関数をストアイベントにバインドするには、[`on`](contexthub-api.md#on-name-handler-selector-triggerforpastevents) 関数または [`once`](contexthub-api.md#once-name-handler-selector-triggerforpastevents) 関数を使用します。

## ContextHub を使用した cookie の操作 {#using-context-hub-to-manipulate-cookies}

ContextHub JavaScript API には、ブラウザー cookie を処理するためのクロスブラウザーサポートがあります。[`ContextHub.Utils.Cookie`](contexthub-api.md#contexthub-utils-cookie) 名前空間は、Cookie を作成、操作、削除するための関数を定義します。

## 解決された ContextHub セグメントの特定 {#determining-resolved-contexthub-segments}

ContextHub のセグメントエンジンを使用して、現在のコンテキストで解決された登録済みセグメントを特定できます。解決されたセグメントを取得するには、[`ContextHub.SegmentEngine.SegmentManager`](contexthub-api.md#contexthub-segmentengine-segmentmanager) クラスの getResolvedSegments 関数を使用します。その後で、`getName` クラスの `getPath` 関数または [`ContextHub.SegmentEngine.Segment`](contexthub-api.md#contexthub-segmentengine-segment) 関数を使用して、セグメントをテストします。

### ContextHub セグメント {#contexthub-segments}

ContextHub のセグメントは、`/conf/<site>/settings/wcm/segments` ノードの下にインストールされます。

次のセグメントは、[WKND チュートリアルサイト](/help/implementing/developing/introduction/develop-wknd-tutorial.md)でインストールされます。

* summer（夏）
* winter（冬）

これらのセグメントの解決に使用されるルールを要約すると次のようになります。

* まず、[位置情報ストア](sample-stores.md#contexthub-geolocation-sample-store-candidate)を使用して、ユーザの緯度を決定します。
* 次に、[surferinfo ストア](sample-stores.md#contexthub-surferinfo-sample-store-candidate)の月のデータ項目が、その緯度での季節を決定します。

>[!WARNING]
>
>インストールされたセグメントは、プロジェクト用の独自の専用設定を構築するのに役立つリファレンス設定として提供されています。直接使用しないでください。

## ContextHub のデバッグ {#debugging-contexthub}

ログの生成を含め、ContextHub をデバッグするためには多くのオプションがあります。詳しくは、「[ContextHub の設定](configuring-contexthub.md#logging-debug-messages-for-contexthub)」を参照してください。

## ContextHub フレームワークの概要の確認 {#see-an-overview-of-the-contexthub-framework}

ContextHub には、ContextHub フレームワークの概要を確認できる[診断ページ](contexthub-diagnostics.md)があります。
