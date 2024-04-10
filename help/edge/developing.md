---
title: Edge Delivery Services 向けの開発
description: Edge Delivery Services を操作するために、ブロックを開発し、AEM プロジェクトをカスタマイズする方法について説明します。
feature: Edge Delivery Services
exl-id: c356c03c-af43-43a1-a14e-45f94ccb3970
source-git-commit: eef58b59cd528743702e3d436acec02dbba58211
workflow-type: tm+mt
source-wordcount: '257'
ht-degree: 100%

---

# Edge Delivery Services 向けの開発 {#developing-edge}

Edge 配信サービスは、ブロックの概念に基づいています。AEM には、プロジェクトのニーズに合わせて拡張できる事前定義済みのブロックの包括的なライブラリが付属しています。Edge 配信サービスプロジェクトのコードは、GitHub で管理されます。

## ブロック {#blocks}

ブロックは、Edge Delivery Services で配信されるページの最も基本的な部分です。ブロックは、コンテンツページの論理コンポーネントを駆動するスタイルとコードをカプセル化します。

AEM では、プロジェクトのボイラープレート内の製品の一部として標準ブロックが用意されています。このようなブロックには、見出し、テキスト、画像、リンク、リストなどが含まれます。

ブロックの詳細と Edge Delivery Services 向けの開発方法については、Edge Delivery Services ドキュメントの[ビルド](/help/edge/developer/block-collection.md)の節を参照してください。

## Edge Delivery Services と GitHub {#github-edge}

Edge Delivery Services では GitHub を活用しているので、GitHub リポジトリから直接コードを管理およびデプロイできます。

作成者は、ドキュメントベースのオーサリングを使用するか、ユニバーサルエディターを使用して AEM のコンテンツを作成できます。開発者は、作成者がコンテンツをどのように作成したかに関係なく、GitHub で CSS と JavaScript を使用してサイトの機能をカスタマイズできます。

コンテンツのプレビューから実稼動環境まで、ブランチごとに web サイトが自動的に作成されます。GitHub リポジトリに配置したすべてのリソースは、ビルドプロセスなしで web サイト上で使用できます。

ブロックの詳細と Edge Delivery Services 向けの開発方法については、Edge Delivery Services ドキュメントの[ビルド](/help/edge/developer/block-collection.md)の節を参照してください。
