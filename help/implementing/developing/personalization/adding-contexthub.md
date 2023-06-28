---
title: ページへの ContextHub の追加とストアへのアクセス
description: ContextHub 機能を有効にし、ContextHub JavaScript ライブラリにリンクするには、ContextHub をページに追加します。
exl-id: 8bfe2cff-3944-4e86-a95c-ebf1cb13913c
source-git-commit: 1994b90e3876f03efa571a9ce65b9fb8b3c90ec4
workflow-type: tm+mt
source-wordcount: '926'
ht-degree: 58%

---

# ページへの ContextHub の追加とストアへのアクセス {#adding-contexthub-to-pages-and-accessing-stores}

ContextHub 機能を有効にし、ContextHub JavaScript ライブラリにリンクするには、ContextHub をページに追加します。

ContextHub JavaScript API を使用すると、ContextHub が管理するコンテキストデータにアクセスできます。このページでは、コンテキストデータにアクセスおよび操作するための API の主な機能について簡単に説明します。詳細情報とコードのサンプルは、API リファレンスドキュメントへのリンクから確認できます。

## ページコンポーネントへの ContextHub の追加 {#adding-contexthub-to-a-page-component}

ContextHub 機能を有効にし、ContextHub JavaScript ライブラリにリンクするには、 ページの `head` セクションに `contexthub` コンポーネントを含めます。ページコンポーネントの HTL コードは、次の例のようになります。

```xml
<sly data-sly-resource="${'contexthub' @ resourceType='granite/contexthub/components/contexthub'}"/>
```

また、ContextHub ツールバーをプレビューモードで表示するかどうかを設定する必要があります。 詳しくは、 [ContextHub UI の表示と非表示](configuring-contexthub.md#showing-and-hiding-the-contexthub-ui).

## ContextHub ストアについて {#about-contexthub-stores}

ContextHub ストアを使用して、コンテキストデータを保持します。 ContextHub には、すべてのストアタイプの基盤となる次のタイプのストアが用意されています。

* [PersistedStore](contexthub-api.md#contexthub-store-persistedstore)
* [SessionStore](contexthub-api.md#contexthub-store-sessionstore)
* [JSONPStore](contexthub-api.md#contexthub-store-persistedjsonpstore)
* [PersistedJSONPStore](contexthub-api.md#contexthub-store-persistedstore)

すべてのストアタイプは、[`ContextHub.Store.Core`](contexthub-api.md#contexthub-store-core) クラスの拡張です。新しいストアタイプの作成について詳しくは、 [カスタムストアの作成](extending-contexthub.md#creating-custom-store-candidates). サンプルのストアタイプについて詳しくは、 [ContextHub ストア候補のサンプル](sample-stores.md).

### 永続モード {#persistence-modes}

ContextHub ストアでは、次の永続モードのいずれかを使用します。

* **ローカル：** HTML5 localStorage を使用してデータを保持します。 ローカルストレージは、セッションをまたいでブラウザーに保持されます。
* **セッション：** HTML5 sessionStorage を使用してデータを保持します。 セッションストレージは、ブラウザーセッションの間保持され、すべてのブラウザーウィンドウで使用できます。
* **cookie:** データストレージに対するブラウザーの cookie のネイティブサポートを使用します。 Cookie データは、HTTP リクエストでサーバーとの間で送信されます。
* **Window.name：** window.name プロパティを使用してデータを保持します。
* **メモリ：** JavaScript オブジェクトを使用してデータを保持します。

デフォルトでは、Context Hub はローカル永続化モードを使用します。 ブラウザーが localStorage5 をサポートしていない場合、または許可していない場合は、HTMLの永続性が使用されます。 ブラウザーが sessionStorage をサポートしていないか、許可していない場合は、Window.name persistence が使用されます。

### ストアデータ {#store-data}

内部的には、データをツリー構造に格納し、値をプライマリ型または複雑なオブジェクトとして追加できます。 複雑なオブジェクトをストアに追加すると、オブジェクトプロパティはデータツリー内にブランチを形成します。 例えば、次の複合オブジェクトを location という名前の空のストアに追加します。

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

ツリー構造は、ストア内のデータ項目をキーと値のペアとして定義します。 上記の例では、キー `/number` が値 `321` に対応し、キー `/data/country` が値 `Switzerland` に対応しています。

### オブジェクトの操作 {#manipulating-objects}

ContextHub には、 [`ContextHub.Utils.JSON.tree`](contexthub-api.md#contexthub-utils-json-tree) JavaScript オブジェクトを操作するためのクラス。 このクラスの関数を使用して、JavaScript オブジェクトをストアに追加する前またはストアから取得した後に操作します。

さらに、[`ContextHub.Utils.JSON`](contexthub-api.md#contexthub-utils-json) クラスには、オブジェクトを文字列にシリアライズしたり、文字列をオブジェクトにデシリアライズしたりするための関数があります。`JSON.parse` 関数および `JSON.stringify` 関数をネイティブに含まないブラウザーをサポートするには、このクラスを使用して JSON データを処理します。

## ContextHub ストアとのやり取り {#interacting-with-contexthub-stores}

以下を使用： [`ContextHub`](contexthub-api.md#ui-event-constants) ストアを JavaScript オブジェクトとして取得する JavaScript オブジェクト。 ストアオブジェクトを取得したら、そのストアに格納されているデータを操作できます。ストアを取得するには、[`getAllStores`](contexthub-api.md#getallstores) 関数または [`getStore`](contexthub-api.md#getstore-name) 関数を使用します。

### ストアデータへのアクセス {#accessing-store-data}

この [`ContexHub.Store.Core`](contexthub-api.md#contexthub-store-core) JavaScript クラスは、ストアデータとやり取りするための関数を定義します。 次の関数は、オブジェクトに格納されている複数のデータ項目を保存および取得します。

* [addAllItems](contexthub-api.md#addallitems-tree-options)
* [getTree](contexthub-api.md#gettree-includeinternals)

個々のデータ項目は、キーと値のペアのセットとして保存されます。 値を保存および取得するには、対応するキーを指定します。

* [getItem](contexthub-api.md#getitem-key)
* [setItem](contexthub-api.md#setitem-key-value-options)

カスタムストア候補は、ストアデータへのアクセスを提供する追加の関数を定義できます。

>[!NOTE]
>
>ContextHub は、デフォルトでは、パブリッシュサーバーを使用した現在のログインを認識しません。そうしたユーザーは ContextHub では「匿名」と見なされます。
>
>プロファイルストアを読み込むことで、ContextHub にログインユーザーを認識させることができます。詳しくは、 [GitHub でのサンプルコードはこちら](https://github.com/Adobe-Marketing-Cloud/aem-sample-we-retail/blob/master/ui.apps/src/main/content/jcr_root/apps/weretail/components/structure/header/clientlib/js/utilities.js).

### ContextHub のイベンティング {#contexthub-eventing}

ContextHub には、ストアイベントに自動的に対処できるようにするイベントフレームワークが含まれています。各ストアオブジェクトには、ストアの [`ContextHub.Utils.Eventing`](contexthub-api.md#contexthub-utils-eventing) プロパティとして使用できる [`eventing`](contexthub-api.md#eventing) オブジェクトが含まれています。以下を使用： [`on`](contexthub-api.md#on-name-handler-selector-triggerforpastevents) または [`once`](contexthub-api.md#once-name-handler-selector-triggerforpastevents) 関数を使用して、JavaScript 関数をストアイベントにバインドします。

## ContextHub を使用した cookie の操作 {#using-context-hub-to-manipulate-cookies}

Context Hub JavaScript API には、ブラウザー cookie を処理するためのクロスブラウザーサポートが用意されています。 [`ContextHub.Utils.Cookie`](contexthub-api.md#contexthub-utils-cookie) 名前空間は、Cookie を作成、操作、削除するための関数を定義します。

## 解決された ContextHub セグメントの特定 {#determining-resolved-contexthub-segments}

ContextHub のセグメントエンジンを使用して、現在のコンテキストで解決された登録済みセグメントを特定できます。解決されたセグメントを取得するには、[`ContextHub.SegmentEngine.SegmentManager`](contexthub-api.md#contexthub-segmentengine-segmentmanager) クラスの getResolvedSegments 関数を使用します。その後で、`getName` クラスの `getPath` 関数または [`ContextHub.SegmentEngine.Segment`](contexthub-api.md#contexthub-segmentengine-segment) 関数を使用して、セグメントをテストします。

### ContextHub セグメント {#contexthub-segments}

ContextHub のセグメントは、`/conf/<site>/settings/wcm/segments` ノードの下にインストールされます。

次のセグメントが、 [WKND チュートリアルサイト](/help/implementing/developing/introduction/develop-wknd-tutorial.md).

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
