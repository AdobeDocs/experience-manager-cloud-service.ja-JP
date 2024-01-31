---
title: UI のカスタマイズ
description: コンテンツ作成者のニーズに合わせてユニバーサルエディターの UI をカスタマイズできる様々な拡張ポイントについて説明します。
exl-id: 8d6523c8-b266-4341-b301-316d5ec224d7
source-git-commit: 1bc65e65e6ce074a050e21137ce538b5c086665f
workflow-type: tm+mt
source-wordcount: '194'
ht-degree: 0%

---


# UI のカスタマイズ {#customizing-ui}

コンテンツ作成者のニーズに合わせてユニバーサルエディターの UI をカスタマイズできる様々な拡張ポイントについて説明します。

## 公開の無効化 {#disable-publish}

特定のオーサリングワークフローでは、コンテンツを公開する前に確認する必要があります。 このような場合、どの作成者も公開オプションを使用できません。

The **公開** 次のメタデータを追加することで、アプリ内でボタンを完全に抑制できます。

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
