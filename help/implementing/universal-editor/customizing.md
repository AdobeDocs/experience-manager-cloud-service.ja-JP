---
title: UI のカスタマイズ
description: コンテンツ作成者のニーズに合わせてユニバーサルエディターの UI をカスタマイズできる様々な拡張ポイントについて説明します。
exl-id: 8d6523c8-b266-4341-b301-316d5ec224d7
source-git-commit: 7ef3efa6e074778b7b3e3a8159056200b2663b30
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
