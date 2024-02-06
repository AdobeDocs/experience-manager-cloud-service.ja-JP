---
title: ユニバーサルエディターオーサリングエクスペリエンスのカスタマイズ
description: コンテンツ作成者のニーズに合わせてユニバーサルエディターの UI をカスタマイズできる、様々な拡張ポイントやその他の機能について説明します。
exl-id: 8d6523c8-b266-4341-b301-316d5ec224d7
source-git-commit: f04ab32093371ff425c4e196872738867d9ed528
workflow-type: tm+mt
source-wordcount: '302'
ht-degree: 0%

---


# ユニバーサルエディターオーサリングエクスペリエンスのカスタマイズ {#customizing-ue}

コンテンツ作成者のニーズに合わせてユニバーサルエディターのオーサリングエクスペリエンスをカスタマイズできる様々な拡張ポイントおよびその他の機能について説明します。

## 公開の無効化 {#disable-publish}

特定のオーサリングワークフローでは、コンテンツを公開する前に確認する必要があります。 このような場合、どの作成者も公開オプションを使用できません。

The **公開** 次のメタデータを追加することで、ボタンを完全にアプリ内で抑制できます。

```html
<meta name="urn:adobe:aue:config:disable" content="publish"/>
```

## コンポーネントのフィルタリング {#filtering-components}

ユニバーサルエディターを使用する場合、コンテナコンポーネントごとに使用可能なコンポーネントを制限できます。 これをおこなうには、フィルター定義を指す追加のスクリプトタグを導入する必要があります。

```html
<script type="application/vnd.adobe.aue.filter+json" src="/static/filter-definition.json"></script>
```

フィルター定義は次のようになり、コンテナの追加を制限して、テキストと画像の追加のみを許可します。

```json
[
  {
    "id": "container-filter",
     "components": ["text", "image"]
   }
]
```

次に、プロパティを追加して、コンテナコンポーネントからフィルター定義を参照できます `data-aue-filter`、前に定義したフィルターの ID を渡します。

```html
data-aue-filter="container-filter"
```

の設定 `components` フィルター定義の属性 `null` は、フィルターがない場合と同様に、すべてのコンポーネントを許可します。

```json
[
  {
    "id": "another-container-filter",
     "components": null
   }
]
```

## プロパティパネルでのコンポーネントの条件付き表示と非表示 {#conditionally-hide}

コンポーネントまたはコンポーネントは、作成者が一般に利用できる場合がありますが、意味のない状況が発生する場合もあります。 このような場合、プロパティパネルで `condition` 属性 [コンポーネントモデルのフィールド。](/help/implementing/universal-editor/field-types.md#fields)

条件は、 [JsonLogic スキーマ。](https://jsonlogic.com/) 条件が true の場合、フィールドが表示されます。 条件が false の場合、フィールドは非表示になります。

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
