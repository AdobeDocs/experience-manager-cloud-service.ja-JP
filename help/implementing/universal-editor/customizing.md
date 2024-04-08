---
title: ユニバーサルエディターオーサリングエクスペリエンスのカスタマイズ
description: コンテンツ作成者のニーズに合わせてユニバーサルエディターの UI をカスタマイズできる、様々な拡張ポイントやその他の機能について説明します。
exl-id: 8d6523c8-b266-4341-b301-316d5ec224d7
source-git-commit: 11a244b7dd4810fbfec92b3effc362102e7322dc
workflow-type: tm+mt
source-wordcount: '302'
ht-degree: 100%

---


# ユニバーサルエディターオーサリングエクスペリエンスのカスタマイズ {#customizing-ue}

コンテンツ作成者のニーズに合わせてユニバーサルエディターのオーサリングエクスペリエンスをカスタマイズできる様々な拡張ポイントおよびその他の機能について説明します。

## 公開の無効化 {#disable-publish}

特定のオーサリングワークフローでは、コンテンツを公開する前に確認する必要があります。このような場合、どの作成者も公開オプションを使用できません。

次のメタデータを追加することで、「**公開**」ボタンを完全にアプリ内で抑制できます。

```html
<meta name="urn:adobe:aue:config:disable" content="publish"/>
```

## コンポーネントのフィルタリング {#filtering-components}

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

## プロパティパネルでのコンポーネントを条件付きで表示および非表示にする {#conditionally-hide}

1 つまたは複数のコンポーネントを一般的に作成者が利用できる場合がありますが、意味をなさない状況が発生する場合もあります。このような場合、`condition` 属性を[コンポーネントモデルのフィールド](/help/implementing/universal-editor/field-types.md#fields)に追加することによって、プロパティパネルでコンポーネントを非表示にすることができます。

条件は、[ JsonLogic スキーマを使用して定義できます。](https://jsonlogic.com/) 条件が true の場合、フィールドが表示されます。条件が false の場合、フィールドは非表示になります。

### サンプルモデル {#sample-model}

```json
 {
    "id": "conditionally-revealed-component",
    "fields": [
      {
        "component": "boolean",
        "label": "Shall the text field be revealed?",
        "name": "reveal",
        "valueType": "boolean"
      },
      {
        "component": "text-input",
        "label": "Hidden text field",
        "name": "hidden-text",
        "valueType": "string",
        "condition": { "===": [{"var" : "reveal"}, true] }
      }
    ]
 }
```

#### 条件 False {#false}

![非表示のテキストフィールド](assets/hidden.png)

#### 条件 True {#true}

![表示されたテキストフィールド](assets/shown.png)

