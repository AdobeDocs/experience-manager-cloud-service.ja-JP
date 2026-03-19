---
title: フィルター
description: フィルターを定義して、使用可能なコンポーネント、RTE オプション、アセット選択など、エディターで使用できるオプションを制限する方法を説明します。
feature: Developing
role: Admin, Developer
exl-id: eeae8d7c-c563-4d9b-8c54-1098a4e98c18
source-git-commit: 8d9d162ec5bba99afb1ae86252a49a9880be4e68
workflow-type: tm+mt
source-wordcount: '325'
ht-degree: 15%

---


# フィルター {#filters}

フィルターを定義して、使用可能なコンポーネント、RTE オプション、アセット選択など、エディターで使用できるオプションを制限する方法を説明します。

## フィルターの設定 {#configuring-filters}

ユニバーサルエディターを使用する場合、フィルターを定義することで、特定の機能に許可されるオプションを制限できます。 フィルターとは、特定のコンテキストで使用できる項目またはアクションのリストです。 例えば、コンテナに挿入できるコンポーネントをフィルタリングしたり、RTE で使用可能なオプションを [&#x200B; フィルタリングしたり &#x200B;](/help/implementing/universal-editor/configure-rte.md) アセットセレクターで [&#x200B; 使用可能なアセットを &#x200B;](/help/implementing/universal-editor/configure-assets-selector.md) フィルタリングしたりできます。

フィルターはすべて同様に定義する必要があります。

1. [フィルター定義を指すようにスクリプトタグを追加](#add-tag)
1. [フィルターの定義](#define-filter)
1. [フィルターの参照](#reference-filter)

コンテナコンポーネントごとにコンポーネントをフィルタリングする例を見てみましょう。

## 参照フィルターの定義 {#add-tag}

まず、フィルター定義を指す追加のスクリプトタグを導入します。

この例では、許可されたコンポーネントをコンテナごとにフィルタリングするために、タグは次のようになります。

```html
<script type="application/vnd.adobe.aue.filter+json" src="/static/filter-definition.json"></script>
```

## フィルターの定義 {#define-filter}

フィルター定義には、フィルターおよびフィルター条件に固有の ID を持つ JSON が含まれています。

この例では、許可されたコンポーネントをコンテナごとにフィルタリングすると、次のように表示され、コンテナはテキストと画像の追加のみを許可するように制限されます。

```json
[
  {
    "id": "container-filter",
    "components": ["text", "image"]
   }
]
```

フィルター定義の `components` 属性を `null` に設定することによって、フィルターがない場合と同様に、すべてのコンポーネントを許可します。

```json
[
  {
    "id": "another-container-filter",
     "components": null
   }
]
```

## フィルターの参照 {#reference-filter}

フィルターを使用するには、フィルター定義を参照する必要があります。 手順は次のとおりです。

* プロパティ `data-aue-filter` を追加してコンテナコンポーネントからフィルターを参照し、フィルターの ID を渡します。

  ```html
  data-aue-filter="container-filter"
  ```

* [&#x200B; コンポーネント定義 &#x200B;](/help/implementing/universal-editor/component-definition.md) からフィルターを参照し、フィルターの ID を渡します。

  ```json
  {
     "title":"My Container",
     "id":"my-container",
     "model": "my-model",
     "filter": "container-filter",
     ...
  }
  ```

## その他のリソース {#additional-resources}

ユニバーサルエディターで使用できるその他のカスタマイズおよび拡張オプションについては、次のドキュメントを参照してください。

* [ユニバーサルエディター用の RTE の設定](/help/implementing/universal-editor/configure-rte.md)
* [Assets Selector のフィルターの設定](/help/implementing/universal-editor/configure-assets-selector.md)
* [ユニバーサルエディターのカスタマイズ](/help/implementing/universal-editor/customizing.md)
* [ユニバーサルエディターの拡張](/help/implementing/universal-editor/extending.md)
