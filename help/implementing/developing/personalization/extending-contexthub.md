---
title: ContextHub の拡張
description: 提供されている ContextHub ストアやモジュールのタイプがソリューションの要件を満たさない場合は、新しいタイプを定義できます
translation-type: tm+mt
source-git-commit: ddfdcf74977adf00bc0ab01b0b1a669781f0d730
workflow-type: tm+mt
source-wordcount: '624'
ht-degree: 66%

---


# ContextHub の拡張 {#extending-contexthub}

提供されている ContextHub ストアやモジュールのタイプがソリューションの要件を満たさない場合は、新しいタイプを定義できます。

## カスタムストア候補の作成 {#creating-custom-store-candidates}

ContextHub ストアは、登録済みのストア候補から作成します。カスタムストアを作成するには、ストア候補を作成して登録する必要があります。

<!--The javascript file that includes the code that creates and registers the store candidate must be included in a [client library folder](/help/sites-developing/clientlibs.md#creating-client-library-folders). The category of the folder must match the following pattern:-->

ストア候補を作成して登録するコードを含む JavaScript ファイルは、クライアントライブラリフォルダーに含める必要があります。フォルダーのカテゴリは、次のパターンに一致しなければなりません。

```xml
contexthub.store.[storeType]
```

The `storeType` part of the category is the `storeType` with which the store candidate is registered. （「[ContextHub ストア候補の登録](#registering-a-contexthub-store-candidate)」を参照）。例えば、storeType が `contexthub.mystore` の場合、クライアントライブラリフォルダーのカテゴリは `contexthub.store.contexthub.mystore` でなければなりません。

### ContextHub ストア候補の作成 {#creating-a-contexthub-store-candidate}

To create a store candidate, you use the [`ContextHub.Utils.inheritance.inherit`](contexthub-api.md#inherit-child-parent) function to extend one of the base stores:

* [`ContextHub.Store.PersistedStore`](contexthub-api.md#contexthub-store-persistedstore)
* [`ContextHub.Store.SessionStore`](contexthub-api.md#contexthub-store-sessionstore)
* [`ContextHub.Store.JSONPStore`](contexthub-api.md#contexthub-store-jsonpstore)
* [`ContextHub.Store.PersistedJSONPStore`](contexthub-api.md#contexthub-store-persistedjsonpstore)

Note that each base store extends the [`ContextHub.Store.Core`](contexthub-api.md#contexthub-store-core) store.

次の例では、`ContextHub.Store.PersistedStore` ストア候補の最もシンプルな拡張を作成しています。

```javascript
myStoreCandidate = function(){};
ContextHub.Utils.inheritance.inherit(myStoreCandidate,ContextHub.Store.PersistedStore);
```

実際には、カスタムストア候補は追加の関数を定義するか、ストアの初期設定を上書きします。Several [sample store candidates](sample-stores.md) are installed in the repository below `/libs/granite/contexthub/components/stores`.

### ContextHub ストア候補の登録 {#registering-a-contexthub-store-candidate}

ストア候補を登録して ContextHub フレームワークに統合し、ストア候補からストアを作成できるようにします。ストア候補を登録するには、[`registerStoreCandidate`](contexthub-api.md#registerstorecandidate-store-storetype-priority-applies) クラスの `ContextHub.Utils.storeCandidates` 関数を使用します。

ストアの候補を登録する場合は、ストアタイプの名前を指定します。 候補からストアを作成するときは、ストアタイプを使用してベースとする候補を識別します。

ストア候補を登録する際に、優先度を指定します。既登録店舗候補と同じ店舗種別で店舗候補が登録された場合には、優先度の高い候補を用いる。 そのため、新しいストア候補を既存のストア候補に優先させることができます。

```javascript
ContextHub.Utils.storeCandidates.registerStoreCandidate(myStoreCandidate,
                                'contexthub.mystorecandidate', 0);
```

ほとんどの場合、1つの候補のみが必要で優先度をに設定できますが、 `0`より高度な登録について学ぶことができます [。これにより、少数のストア実装のうちの1つをjavascript条件(](contexthub-api.md#registerstorecandidate-store-storetype-priority-applies)`applies`)と優先度の候補に基づいて選択できます。

## ContextHub UI モジュールタイプの作成 {#creating-contexthub-ui-module-types}

[ContextHub に付属してインストールされる](sample-modules.md) UI モジュールタイプが要件を満たさない場合は、カスタム UI モジュールタイプを作成できます。UI モジュールタイプを作成するには、`ContextHub.UI.BaseModuleRenderer` クラスを拡張して `ContextHub.UI` に登録し、新しい UI モジュールレンダラーを作成します。

To create a UI module renderer, create a `Class` object that contains the logic that renders the UI module. 少なくとも、このクラスは次のアクションを実行する必要があります。

* Extend the `ContextHub.UI.BaseModuleRenderer` class. このクラスは、すべての UI モジュールレンダラーのベースとなる実装です。`Class` オブジェクトは、このクラスが拡張されていることを示すために使用する `extend` というプロパティを定義します。
* デフォルトの設定を指定します。Create a `defaultConfig` property. このプロパティは、[`contexthub.base`](sample-modules.md#contexthub-base-ui-module-type) UI モジュール用に定義されているプロパティと、必要なその他すべてのプロパティを含むオブジェクトです。

のソース `ContextHub.UI.BaseModuleRenderer` はにあり `/libs/granite/contexthub/code/ui/container/js/ContextHub.UI.BaseModuleRenderer.js`ます。  レンダラーを登録するには、[`registerRenderer`](contexthub-api.md#registerrenderer-moduletype-renderer-dontrender) クラスの `ContextHub.UI` メソッドを使用します。モジュールタイプの名前を指定する必要があります。管理者がこのレンダラーをベースとして UI モジュールを作成する場合は、この名前を指定します。

レンダラークラスを作成し、自己実行型匿名関数に登録します。The following example is based on the source code for the `contexthub.browserinfo` UI module. この UI モジュールは、`ContextHub.UI.BaseModuleRenderer` クラスのシンプルな拡張です。

```javascript
;(function() {

    var SurferinfoRenderer = new Class({
        extend: ContextHub.UI.BaseModuleRenderer,

        defaultConfig: {
            icon: 'coral-Icon--globe',
            title: 'Browser/OS Information',

            storeMapping: {
                surferinfo: 'surferinfo'
            },

            template:
                '<p>{{surferinfo.browser.family}} {{surferinfo.browser.version}}</p>' +
                '<p>{{surferinfo.os.name}} {{surferinfo.os.version}}</p>'
        }
    });

    ContextHub.UI.registerRenderer('contexthub.browserinfo', new SurferinfoRenderer());

}());
```

<!--The javascript file that includes the code that creates and registers the renderer must be included in a [client library folder](/help/sites-developing/clientlibs.md#creating-client-library-folders). The category of the folder must match the following pattern:-->

レンダラーを作成し登録するコードを含むjavascriptファイルは、クライアントライブラリフォルダーに含める必要があります。 フォルダーのカテゴリは、次のパターンに一致しなければなりません。

```javascript
contexthub.module.[moduleType]
```

The `[moduleType]` part of the category is the `moduleType` with which the module renderer is registered. 例えば、`moduleType` が `contexthub.browserinfo` の場合、クライアントライブラリフォルダーのカテゴリは `contexthub.module.contexthub.browserinfo` でなければなりません。
