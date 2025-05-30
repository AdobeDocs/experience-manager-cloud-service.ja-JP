---
title: ユニバーサルエディターのユースケースと学習パス
description: ユニバーサルエディターの主なユースケース、その使用法を理解する最適な方法、および独自のプロジェクトに実装する方法について説明します。
exl-id: 398ad0e2-c299-4c49-9784-05c84c67bec2
feature: Developing
role: Admin, Architect, Developer
source-git-commit: c4dcb1cecb756f746ecb856fcfd65d73833a5ee0
workflow-type: ht
source-wordcount: '878'
ht-degree: 100%

---

# ユニバーサルエディターのユースケースと学習パス {#use-cases-learning-paths}

ユニバーサルエディターの主なユースケース、その使用法を詳しく理解する最適な方法、および独自のプロジェクトに実装する方法について説明します。

## 概要 {#overview}

ユニバーサルエディターは、Adobe Experience Manager Sites の一部である多用途のビジュアルエディターです。作成者が、任意のヘッドレスエクスペリエンスまたはヘッドフルエクスペリエンスを見たとおりに編集できる（WYSIWYG）機能です。

このドキュメントでは、これら 2 つのユースケースについて詳しく説明し、これらを詳しく理解し、独自のプロジェクトにユニバーサルエディターを実装する方法を示します。

>[!TIP]
>
>まだ使用したことがない場合は、[ユニバーサルエディターの概要](/help/implementing/universal-editor/introduction.md)ドキュメントを参照して、ユニバーサルエディターの完全な概要と価値を確認してください。

## ユースケース {#use-cases}

ユニバーサルエディターは、作成するコンテンツの種類に関係なく、便利で直感的なビジュアルエディターをコンテンツ作成者に提供します。主なユースケースは次の 2 つです。

* [WYSIWYG オーサリング](#wysiwyg-authoring) - AEM Sites コンソールを使用して、ユニバーサルエディターを使用して AEM 内のコンテンツとオーサーページを管理します。
* [ヘッドレスオーサリング](#headless-authoring) - ユニバーサルエディターを使用して、独自のカスタムヘッドレスアプリケーションでコンテンツをオーサリングします。

### WYSIWYG オーサリング {#wysiwyg-authoring}

AEM に既に精通している場合は、Sites コンソールを使用してページを作成および管理し、ユニバーサルエディターで編集できます。

この方法では、ページ管理（コピー、ペースト、移動）やワークフローなど、Sites コンソールで使用できるツールのメリットを享受できるだけでなく、最新のユニバーサルエディターのメリットも享受できます。

このユースケースに該当する場合は、次の手順として、以下のドキュメントを参照し、AEM でユニバーサルエディターを起動して実行する方法の完全な概要を確認してください。

1. [Edge Delivery Services を使用した WYSIWYG オーサリングの開発者向け入門ガイド](/help/edge/wysiwyg-authoring/edge-dev-getting-started.md) - AEMでの最初のユニバーサルエディタープロジェクトの基本を学びます
1. [ユニバーサルエディターで使用するために実装されたブロックの作成](/help/edge/wysiwyg-authoring/create-block.md) - ブロックを実装して、ユニバーサルエディターでコンテンツを編集可能にする方法について説明します
1. [Edge Delivery Services プロジェクトを使用した WYSIWYG オーサリング用のコンテンツモデリング](/help/edge/wysiwyg-authoring/content-modeling.md) - ユニバーサルエディターで使用するコンテンツを効果的にモデル化するためにブロックを構造化する仕組みについて詳しく説明します。

これらのドキュメントを参照したら、このページに戻って、ヘッドレスオーサリングのユースケースとユニバーサルエディターの一般的な仕組みについて学ぶことができます。

### ヘッドレスオーサリング {#headless-authoring}

既にヘッドレスアプリを使用している場合は、ユニバーサルエディターを使用してアプリのコンテンツを作成し、そのコンテンツを AEM のコンテンツフラグメントとして保持できます。唯一の要件は、アプリがユニバーサルエディターの使用を許可するように実装されていることです。

このユースケースに該当する場合は、次の手順として、以下のドキュメントを参照し、ユニバーサルエディターを使用するように実装されたヘッドレスアプリの例を確認してください。

* [ユニバーサルエディター用 SecurBank サンプルアプリ](/help/implementing/universal-editor/securbank.md)

ドキュメントを参照したら、このページに戻って、WYSIWYG オーサリングのユースケースとユニバーサルエディターの一般的な仕組みについて学ぶことができます。

{{ue-headless-auth}}

## ユニバーサルエディターの仕組み {#how-ue-works}

ユニバーサルエディターの強みは、あらゆるコンテンツをインプレースでオーサリングできる点です。コンテンツに関係なく、完全に直感的で統一された UI をコンテンツ作成者に提供します。

ユニバーサルエディターは、次のように機能します。

1. 開発者は、ユニバーサルエディターを使用するアプリまたはページを実装します。この実装によって、編集可能なコンテンツと、その保持方法がエディターに指示されます。
   * [Edge Delivery Services を使用した WYSIWYG オーサリングの開発者向け入門ガイド](/help/edge/wysiwyg-authoring/edge-dev-getting-started.md)ドキュメントに従うと、ページが自動的に実装されます。
   * ヘッドレスオーサリングの場合、アプリを簡単に実装できます。
1. コンテンツ作成者がユニバーサルエディターを読み込むと、編集用にページが読み込まれます。実装されているので、編集可能なコンテンツと、その表現および保持方法がわかります。
1. コンテンツ作成者は、直感的な WYSIWYG インターフェイスでページコンテンツを編集し、インプレースで編集します。
1. ユニバーサルエディターは、変更を自動的にデータソースに保持します。

ユニバーサルエディターのアーキテクチャについて詳しくは、[ユニバーサルエディターのアーキテクチャ](/help/implementing/universal-editor/architecture.md)ドキュメントを参照してください。

## ユニバーサルエディターの概念 {#concepts}

ページまたはアプリをユニバーサルエディターで編集できるようにするには、アプリの実装を適切に行う必要があります。

* [属性とタイプ](/help/implementing/universal-editor/attributes-types.md) - アプリまたはページをユニバーサルエディターで編集できるようにするには、アプリの実装を適切に行う必要があります。これには、エディターがアプリのコンテンツを編集できるように、適切なメタデータを含めることが含まれます。
* [モデル定義、フィールドおよびコンポーネントタイプ](/help/implementing/universal-editor/field-types.md) - メタデータが存在してコンポーネントの編集が可能になったら、エディターのプロパティパネルで操作できるフィールドとコンポーネントタイプを定義します。
* [ユニバーサルエディターイベント](/help/implementing/universal-editor/events.md) - ユニバーサルエディターがコンテンツまたは UI インタラクションで出力するイベントを使用して、アプリの編集エクスペリエンスを強化し、アプリをさらにカスタマイズできます。

また、ユニバーサルエディターは、プロジェクトのニーズに適応させることもできます。

* [ユニバーサルエディターのカスタマイズ](/help/implementing/universal-editor/customizing.md) - エディターの様々な側面をフィルタリングしたり、エディターの機能を拡張したりして、ユニバーサルエディターのエクスペリエンスを適応させることができます。
* [ユニバーサルエディターの拡張](/help/implementing/universal-editor/extending.md) - ユニバーサルエディターの UI は、プロジェクトのニーズに合わせて機能を展開することを目的に拡張できます。
