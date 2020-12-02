---
title: ContextHub の拡張
description: 提供されている ContextHub ストアやモジュールのタイプがソリューションの要件を満たさない場合は、新しいタイプを定義できます
translation-type: tm+mt
source-git-commit: 1c518830f0bc9d9c7e6b11bebd6c0abd668ce040
workflow-type: tm+mt
source-wordcount: '624'
ht-degree: 100%

---


# ContextHub の拡張 {#extending-contexthub}

提供されている ContextHub ストアやモジュールのタイプがソリューションの要件を満たさない場合は、新しいタイプを定義できます。

## カスタムストア候補の作成  {#creating-custom-store-candidates}

ContextHub ストアは、登録済みのストア候補から作成します。カスタムストアを作成するには、ストア候補を作成して登録する必要があります。

ストア候補を作成して登録するコードを含む JavaScript ファイルは、[クライアントライブラリフォルダー](/help/implementing/developing/introduction/clientlibs.md)に含める必要があります。フォルダーのカテゴリは、次のパターンに一致しなければなりません。

```xml
contexthub.store.[storeType]
```

カテゴリの `storeType` 部分は、ストア候補と一緒に登録されている `storeType` です（「[ContextHub ストア候補の登録](#registering-a-contexthub-store-candidate)」を参照）。例えば、storeType が `contexthub.mystore` の場合、クライアントライブラリフォルダーのカテゴリは `contexthub.store.contexthub.mystore` でなければなりません。

### ContextHub ストア候補の作成 {#creating-a-contexthub-store-candidate}

ストア候補を作成するには、[`ContextHub.Utils.inheritance.inherit`](contexthub-api.md#inherit-child-parent) 関数を使用して、次のいずれかのベースストアを拡張します。

* [`ContextHub.Store.PersistedStore`](contexthub-api.md#contexthub-store-persistedstore)
* [`ContextHub.Store.SessionStore`](contexthub-api.md#contexthub-store-sessionstore)
* [`ContextHub.Store.JSONPStore`](contexthub-api.md#contexthub-store-jsonpstore)
* [`ContextHub.Store.PersistedJSONPStore`](contexthub-api.md#contexthub-store-persistedjsonpstore)

各ベースストアは、[`ContextHub.Store.Core`](contexthub-api.md#contexthub-store-core) ストアを拡張したものです。

次の例では、`ContextHub.Store.PersistedStore` ストア候補の最もシンプルな拡張を作成しています。

```javascript
myStoreCandidate = function(){};
ContextHub.Utils.inheritance.inherit(myStoreCandidate,ContextHub.Store.PersistedStore);
```

実際には、カスタムストア候補は追加の関数を定義するか、ストアの初期設定を上書きします。いくつかの[サンプルストア候補](sample-stores.md)が、`/libs/granite/contexthub/components/stores` の下にあるリポジトリにインストールされています。

### ContextHub ストア候補の登録 {#registering-a-contexthub-store-candidate}

ストア候補を登録して ContextHub フレームワークに統合し、ストア候補からストアを作成できるようにします。ストア候補を登録するには、[`registerStoreCandidate`](contexthub-api.md#registerstorecandidate-store-storetype-priority-applies) クラスの `ContextHub.Utils.storeCandidates` 関数を使用します。

ストア候補を登録する際に、ストアタイプの名前を指定します。候補からストアを作成するときは、ストアタイプを使用してベースとする候補を識別します。

ストア候補を登録する際に、優先度を指定します。既に登録済みのストア候補と同じストアタイプを使用してストア候補を登録した場合、優先度の高い候補が使用されます。そのため、新しいストア候補を既存のストア候補に優先させることができます。

```javascript
ContextHub.Utils.storeCandidates.registerStoreCandidate(myStoreCandidate,
                                'contexthub.mystorecandidate', 0);
```

ほとんどの場合、1 つの候補のみが必要で優先度を `0` に設定できますが、[より高度な登録](contexthub-api.md#registerstorecandidate-store-storetype-priority-applies)について学ぶことができます。これにより、少数のストア実装のうちの 1 つを javascript 条件（`applies`）と優先度の候補に基づいて選択できます。

## ContextHub UI モジュールタイプの作成 {#creating-contexthub-ui-module-types}

[ContextHub に付属してインストールされる](sample-modules.md) UI モジュールタイプが要件を満たさない場合は、カスタム UI モジュールタイプを作成できます。UI モジュールタイプを作成するには、`ContextHub.UI.BaseModuleRenderer` クラスを拡張して `ContextHub.UI` に登録し、新しい UI モジュールレンダラーを作成します。

UI モジュールレンダラーを作成するには、UI モジュールをレンダリングするロジックを格納する `Class` オブジェクトを作成します。少なくとも、このクラスは次のアクションを実行する必要があります。

* `ContextHub.UI.BaseModuleRenderer` クラスを拡張します。このクラスは、すべての UI モジュールレンダラーのベースとなる実装です。`Class` オブジェクトは、このクラスが拡張されていることを示すために使用する `extend` というプロパティを定義します。
* デフォルトの設定を指定します。`defaultConfig` プロパティを作成します。このプロパティは、[`contexthub.base`](sample-modules.md#contexthub-base-ui-module-type) UI モジュール用に定義されているプロパティと、必要なその他すべてのプロパティを含むオブジェクトです。

`ContextHub.UI.BaseModuleRenderer` のソースは `/libs/granite/contexthub/code/ui/container/js/ContextHub.UI.BaseModuleRenderer.js` にあります。レンダラーを登録するには、[`registerRenderer`](contexthub-api.md#registerrenderer-moduletype-renderer-dontrender) クラスの `ContextHub.UI` メソッドを使用します。モジュールタイプの名前を指定する必要があります。管理者がこのレンダラーをベースとして UI モジュールを作成する場合は、この名前を指定します。

レンダラークラスを作成し、自己実行型匿名関数に登録します。次の例は、`contexthub.browserinfo` UI モジュールのソースコードをベースとしています。この UI モジュールは、`ContextHub.UI.BaseModuleRenderer` クラスのシンプルな拡張です。

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

レンダラーを作成して登録するコードを含む JavaScript ファイルは、[クライアントライブラリフォルダー](/help/implementing/developing/introduction/clientlibs.md)に含める必要があります。フォルダーのカテゴリは、次のパターンに一致しなければなりません。

```javascript
contexthub.module.[moduleType]
```

カテゴリの `[moduleType]` 部分は、モジュールレンダラーの登録に使用されている `moduleType` です。例えば、`moduleType` が `contexthub.browserinfo` の場合、クライアントライブラリフォルダーのカテゴリは `contexthub.module.contexthub.browserinfo` でなければなりません。
