---
title: オーサリング方法の選択
description: AEMでのコンテンツの作成方法を決定する際に重要な考慮事項を説明し、コンテンツ作成者に最適な判断を下すのに役立ちます。
feature: Edge Delivery Services
role: Admin, Architect, Developer
source-git-commit: 15eef2d3790d1c0cf5414ca55b191de5b644fed0
workflow-type: tm+mt
source-wordcount: '659'
ht-degree: 0%

---


# オーサリング方法の選択 {#authoring-methods}

AEMでのコンテンツの作成方法を決定する際に重要な考慮事項を説明し、コンテンツ作成者に最適な判断を下すのに役立ちます。

## 考慮事項の概要 {#overview}

柔軟性をAEMすることで、ドキュメントベースのオーサリングと WYSIWYG オーサリングのどちらを選択した場合でも、オーサリングのニーズが確実に満たされます。 検討を開始する際は、次の点に留意してください。

* **コンテンツ作成者を常に決定に関与させます。** - コンテンツ作成者はエキスパートであり、そのインサイトは非常に重要です。
* **複数のオーサリングメソッドを実装できます。** - Adobeでは、必要に応じてシンプルなレイヤーを使い始めることをお勧めしますが、複数のオーサリング手法を組み合わせて、1 つのプロジェクトを作成することもできます。
* **オーサリング方法は、いつでも事後的に変更できます。** – あなたが決めることは何でも、あなたはロックされていません。 Adobeの自動移行ツールを利用して、ある方法から別の方法に簡単に移行できます。
* **実装の前ではなく、実装の一部として決定する必要があります。** - AEMは 1 つの統合製品なので、この重要な決定は契約ネゴシエーションの一部である必要はありません。 AEMを購入すると、すべての製品が手に入ります。 むしろ、これは実装時の決定です。

Adobeは、実装の一環として要件に最適な方法を判断するのに役立ちます。

## 1 つのサイズですべてに対応できるわけではありません {#one-size}

AEMの実装には、それぞれ独自のワークフローと目標があります。 1 つのプロジェクトには、独自のパブリケーションを作成するコンテンツ作成者を含む単純なオーサリングモデルが含まれる場合があります。 一方、別の組織では、寄稿者と承認の複雑なネットワークが存在する場合もあります。

![ 様々なオーサリングワークフロー ](assets/authoring-workflows.png)

プロジェクトが異なると、ユースケースが異なる（または複数の）場合があります。

![ ユースケース ](assets/use-cases.png)

Adobeはこれを理解しているので、万能のアプローチを提供していません。 AEMは、ニーズに最適なコンテンツ配信とコンテンツ作成に対する様々なアプローチを提供する、お客様の単一のソリューションです。

最適なアプローチを決定するには、4 つの項目を考慮する必要があります。

1. [コンテンツ配信の環境設定はありますか？](#content-delivery)
1. [コンテンツオーサリングの環境設定はありますか？](#content-authoring)
1. [プロジェクトの目標は何ですか？](#project-goals)
1. [現在、オーサリングはどのような課題に直面していますか？](#authoring-challenges)

## コンテンツ配信設定 {#content-delivery}

まず考慮すべき点は、コンテンツの配信方法です。 Edge Delivery Servicesは非常に高速なサイトを提供しますが、ヘッドレス配信に重点を置いている場合もあります。 次のデシジョンツリーは、オプションの検討に役立ちます。

![ コンテンツ配信の決定ツリー ](assets/content-delivery-decision-tree.png)

これは、必要に応じて判断するのに役立ちます。

* [ コンテンツフラグメントエディターやユニバーサルエディターを使用して ](/help/headless/introduction.md) ヘッドレス CMS としてAEM}。
* [ ドキュメントベースの編集 ](/help/edge/docs/authoring.md) または [ ユニバーサルエディターを使用した WYSIWYG オーサリング ](/help/edge/wysiwyg-authoring/authoring.md) を使用したAEM Edge Delivery Services。

## コンテンツオーサリング環境設定 {#content-authoring}

次に考慮すべき事項は、コンテンツの作成方法です。 次のデシジョンツリーは、オプションの検討に役立ちます。

![ コンテンツオーサリングの決定ツリー ](assets/content-authoring-decision-tree.png)

これは、必要に応じて判断するのに役立ちます。

* [ ドキュメントベースのAEMEdge Delivery Services ](/help/edge/docs/authoring.md) を使用した編集
* [ユニバーサルエディターを使用した WYSIWYG オーサリング](/help/edge/wysiwyg-authoring/authoring.md)

## プロジェクトの目標 {#project-goals}

オーサリングの成功はどのように見えますか？ プロジェクトの成功はどのように定義しますか？

* コンテンツを作成できるユーザーを増やす必要があるものの、新しいツールセットに関するトレーニングは避けたい場合があります。 （ドキュメントベースのオーサリングを考えてみましょう）。
* 生成するコンテンツの量を増やす必要がある場合があります。 （ドキュメントベースのオーサリングを考えてみましょう）。
* 視覚的なコンテンツのレイアウトに重点を置く必要があるものの、コーディングに関する知識の必要性が最小限に抑えられる場合があります。 （WYSIWYG オーサリングと考えてください）。

実装の最初に明確に述べたプロジェクトの目標は、オーサリング方法を十分に情報に基づいて決定するのに役立ちます。

## オーサリングの課題 {#authoring-challenges}

最後に、コンテンツのオーサリングで今日直面している具体的な課題について考えます。

* CMS 以外で作成されたコンテンツを使用して作業が重複する可能性があります。その場合は、コンテンツをインポートするか、コピー&amp;ペーストする必要があります。 （ドキュメントベースのオーサリングを考えてみましょう）。
* おそらく、CMS の使用方法に関する作成者のトレーニングに必要な時間を短縮する必要があります。 （ドキュメントベースのオーサリングを考えてみましょう）。
* 作成者は、コンテンツの視覚的なレイアウトを頻繁に編集する必要があり、開発者のサポートを常に必要とする場合があります。 （WYSIWYG オーサリングと考えてください）。