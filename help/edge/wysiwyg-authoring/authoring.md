---
title: Edge Delivery Services 向けの WYSIWYG コンテンツのオーサリング
description: コンテンツのオーサリングと Edge Delivery Services を連携する方法、および Edge Delivery Services で AEM コンテンツをオーサリングする方法について説明します。
feature: Edge Delivery Services
exl-id: 963ff71a-8176-4d9d-8240-dc429405d139
role: User
source-git-commit: 10580c1b045c86d76ab2b871ca3c0b7de6683044
workflow-type: tm+mt
source-wordcount: '452'
ht-degree: 95%

---


# Edge Delivery Services 向けの WYSIWYG コンテンツのオーサリング {#authoring-edge}

Edge Delivery Services を使用すると、オーサリングが簡単、迅速、柔軟に行えます。Edge Delivery Services のコンテンツを作成する方法は 2 つあります。

* [ユニバーサルエディター](#universal-editor) - AEM 内でコンテンツをオーサリングするための最新 の What You See Is What You Get（WYSIWYG）UI
* [ドキュメントベースのオーサリング](#document-based)：Microsoft Word や Google Docs など

## ユニバーサルエディターのオーサリング {#universal-editor}

AEM as a Cloud Service で Edge Delivery Services を使用する場合、作成したコンテンツが AEM as a Cloud Service に保持されるという最も基本的なことを必ず理解しておいてください。

![WYSIWYG オーサリングと Edge Delivery Services の連携](assets/how-aem-edge-works.png)

1. [AEM Sites 環境](/help/sites-cloud/authoring/quick-start.md)は、新しいページ、エクスペリエンスフラグメント、コンテンツフラグメントの作成などのコンテンツ管理に使用されます。
   * AEM のすべての機能（ワークフロー、MSM、翻訳、起動など）を使用できます。
1. [ユニバーサルエディター](/help/sites-cloud/authoring/universal-editor/authoring.md)は、AEM で管理されるコンテンツの作成に使用されます。
   * ユニバーサルエディターには、コンテンツオーサリング用の最新の UI が用意されています。
   * オーサリング時に、AEM は HTML をレンダリングしますが、それには、Edge Delivery Services から取得したスクリプト、スタイル、アイコン、その他のリソースが含まれます。
   * ユニバーサルエディターを使用しても、すべての変更は AEM に保持されます。
   * ユニバーサルエディターは現在、AEM ページエディターと同等の機能を備えていないため、AEM の一部の機能はユニバーサルエディターで使用できない場合があります。
1. ユニバーサルエディターで作成し、AEM に保持するコンテンツは、Edge Delivery Services に公開されます。
   * コンテンツは AEM に保存されたままになります。
   * AEM は、取り込みに必要なセマンティック HTML をレンダリングします。
   * コンテンツは Edge Delivery Services に公開されます。
1. [Edge Delivery Services](/help/edge/developer/keeping-it-100.md) は 100% の Lighthouse スコアを確保します。

ブロックは、Edge Delivery Services によって配信されるページの基本的なコンポーネントです。作成者は、アドビが標準で提供するデフォルトブロック、または開発者がプロジェクト用にカスタマイズしたブロックから選択できます。

ユニバーサルエディターには、ブロックを追加および配置してコンテンツをオーサリングできる最新の直感的な GUI が用意されています。

![ユニバーサルエディターでブロックを追加および配置する](assets/blocks.png)

ブロックの詳細は、プロパティパネルで設定できます。

![ブロックプロパティの設定](assets/block-properties.png)

ユニバーサルエディターを使用したコンテンツの作成方法について詳しくは、ドキュメント [ ユニバーサルエディターを使用したコンテンツのオーサリング ](/help/sites-cloud/authoring/universal-editor/authoring.md) を参照してください。

AEM と Edge Delivery Services を使用してオーサリングする独自のプロジェクトを開始する方法について詳しくは、[Edge Delivery Services を使用した WYSIWYG オーサリングの開発者向け入門ガイド](/help/edge/wysiwyg-authoring/edge-dev-getting-started.md)を参照してください。

## その他のオーサリング方法  {#authoring-methods}

WYSIWYG オーサリングは、コンテンツ作成者向けの強力で直感的なツールです。ただし、オーサリングのユースケースは多種多様なので、AEM では追加のオーサリングソリューションを提供しています。

ドキュメントベースのオーサリングやヘッドレスなど、AEM が提供するオーサリングソリューションについて詳しくは、[オーサリング方法の選択](/help/edge/authoring-methods.md)ドキュメントを参照してください。
