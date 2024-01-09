---
title: UI のカスタマイズ
description: コンテンツ作成者のニーズに合わせてユニバーサルエディターの UI をカスタマイズできる様々な拡張ポイントについて説明します。
source-git-commit: 65893c0c0dee37bed8ecfbb06a12e7c093c4397c
workflow-type: tm+mt
source-wordcount: '100'
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
