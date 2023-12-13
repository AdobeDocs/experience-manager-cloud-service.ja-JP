---
title: Edge Delivery Services向け開発
description: ブロックを開発し、Edge Delivery Servicesと連携するようにAEMプロジェクトをカスタマイズする方法を説明します。
feature: Edge Delivery Services
source-git-commit: 22a791311c618fcbd61f321b8efa79c3a52ec65d
workflow-type: tm+mt
source-wordcount: '257'
ht-degree: 14%

---


# Edge Delivery Services向け開発 {#developing-edge}

Edge Delivery Servicesは、ブロックの概念に基づいています。 AEMには、事前定義済みのブロックの包括的なライブラリが付属しており、プロジェクトのニーズに合わせて拡張できます。 Edge Delivery Servicesプロジェクトのコードは GitHub で管理されます。

## ブロック {#blocks}

ブロックは、ページの最も基本的な部分で、Edge Delivery Servicesが配信します。 ブロックは、コンテンツページの論理コンポーネントを駆動するスタイルとコードをカプセル化します。

AEMは、プロジェクトボイラープレート内の製品の一部として、標準ブロックを提供します。 このようなブロックには、見出し、テキスト、画像、リンク、リストなどが含まれます。

詳しくは、 [ビルドセクション](/help/edge/developer/block-collection.md) Edge Delivery Servicesに関するドキュメントを参照して、ブロックの詳細と、Edge 配信サービス向けの開発方法を確認してください。

## Edge 配信サービスおよび GitHub {#github-edge}

Edge 配信では GitHub を活用するので、GitHub リポジトリから直接コードを管理およびデプロイできます。

作成者は、ドキュメントベースのオーサリングまたはユニバーサルエディターを使用したAEMでのコンテンツを使用してコンテンツを作成できます。 開発者は、作成者がコンテンツをどのように作成したかに関係なく、GitHub で CSS と JavaScript を使用して、サイトの機能をカスタマイズできます。

コンテンツのプレビューから実稼動環境まで、ブランチごとに web サイトが自動的に作成されます。GitHub リポジトリに配置したすべてのリソースは、ビルドプロセスなしで web サイト上で使用できます。

詳しくは、 [ビルドセクション](/help/edge/developer/block-collection.md) Edge Delivery Servicesに関するドキュメントを参照して、ブロックの詳細と、Edge 配信サービス向けの開発方法を確認してください。
