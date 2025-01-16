---
title: コンポーネントのフィルタリング
description: コンポーネントフィルターを使用して、ユニバーサルエディターでコンテナごとに許可されたコンポーネントを制限する方法を説明します。
feature: Developing
role: Admin, Architect, Developer
source-git-commit: 48c1a109c060db4ce19bf645723357008d51c572
workflow-type: tm+mt
source-wordcount: '151'
ht-degree: 63%

---


# コンポーネントのフィルタリング {#filtering-components}

コンポーネントフィルターを使用して、ユニバーサルエディターでコンテナごとに許可されたコンポーネントを制限する方法を説明します。

## フィルター {#filters}

ユニバーサルエディターを使用する場合、コンテナコンポーネントごとに使用可能なコンポーネントを制限できます。これを行うには、フィルター定義を指す、スクリプトタグをさらに追加導入する必要があります。

```html
<script type="application/vnd.adobe.aue.filter+json" src="/static/filter-definition.json"></script>
```

フィルター定義は次のようになり、コンテナにテキストと画像の追加のみを許可するように制限します。

```json
[
  {
    "id": "container-filter",
     "components": ["text", "image"]
   }
]
```

次に、プロパティ `data-aue-filter` を追加してコンテナコンポーネントからフィルター定義を参照することができるので、以前に定義したフィルターの ID を渡します。

```html
data-aue-filter="container-filter"
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

>[!TIP]
>
>ユニバーサルエディターで使用できるその他のカスタマイズおよび拡張オプションについては、ドキュメント [ ユニバーサルエディターのカスタマイズと拡張 ](/help/implementing/universal-editor/customizing.md) を参照してください。
