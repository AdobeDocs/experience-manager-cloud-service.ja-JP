---
title: Edge Delivery Services 向けの開発
description: Edge Delivery Services を操作するために、ブロックを開発し、AEM プロジェクトをカスタマイズする方法について説明します。
feature: Edge Delivery Services
exl-id: c356c03c-af43-43a1-a14e-45f94ccb3970
source-git-commit: becba7698afe4aa0629bf54fa0d0d26156784b5f
workflow-type: tm+mt
source-wordcount: '209'
ht-degree: 91%

---

# Edge Delivery Services 向けの開発 {#developing-edge}

Edge 配信サービスは、ブロックの概念に基づいています。AEM には、プロジェクトのニーズに合わせて拡張できる事前定義済みのブロックの包括的なライブラリが付属しています。Edge 配信サービスプロジェクトのコードは、GitHub で管理されます。

## ブロック {#blocks}

ブロックは、Edge Delivery Services で配信されるページの最も基本的な部分です。ブロックは、コンテンツページの論理コンポーネントを駆動するスタイルとコードをカプセル化します。

AEM では、プロジェクトのボイラープレート内の製品の一部として標準ブロックが用意されています。このようなブロックには、見出し、テキスト、画像、リンク、リストなどが含まれます。

<!--Please see the [Build section](/help/edge/developer/block-collection.md) of the Edge Delivery Services documentation for more details on blocks and how to develop for Edge Delivery services.-->

## Edge Delivery Services と GitHub {#github-edge}

Edge Delivery Services では GitHub を活用しているので、GitHub リポジトリから直接コードを管理およびデプロイできます。

作成者は、ドキュメントベースのオーサリングまたはユニバーサルエディターを使用したAEMでのコンテンツを使用してコンテンツを作成できます。 開発者は、作成者がコンテンツをどのように作成したかに関係なく、GitHub で CSS と JavaScript を使用してサイトの機能をカスタマイズできます。

コンテンツのプレビューから実稼動環境まで、ブランチごとに web サイトが自動的に作成されます。GitHub リポジトリに配置したすべてのリソースは、ビルドプロセスなしで web サイト上で使用できます。

<!--Please see the [Build section](/help/edge/developer/block-collection.md) of the Edge Delivery Services documentation for more details on blocks and how to develop for Edge Delivery services.-->
