---
title: コミュニケーション作成ジョブ
description: Experience Production Agentsのコミュニケーション作成ジョブと、自然言語を使用してインタラクティブ通信を作成する方法について説明します。
feature: Edge Delivery Services, Agentic AI
role: User, Admin, Developer
exl-id: 49111cdb-e714-4590-8b81-382377083d6e
source-git-commit: 81f85045212ca6fd92f2b665aeceaa0d4b92318c
workflow-type: tm+mt
source-wordcount: '613'
ht-degree: 0%

---


# コミュニケーション作成ジョブ {#ic-creation-skill}

<!-- UNCOMMENT ACTIVATION SECTION AT THE BOTTOM ONCE THIS IS NO LONGER ALPHA -->

>[!NOTE]
>
> コミュニケーション作成ジョブは現在アルファ版です。 参加を希望される場合は、公式メールアドレスから[aem-forms-ea@adobe.comにリクエストを送信してください。](mailto:aem-forms-ea@adobe.com)

[&#x200B; インタラクティブ コミュニケーション &#x200B;](/help/forms/introduction-to-interactive-communication.md)は、アカウント明細書、ポリシードキュメント、請求書、ウェルカムキット、特典通知など、ビジネス上の対応を目的として設計された、パーソナライズされたデータ駆動型ドキュメントです。 ユーザーから入力を収集するフォームとは異なり、インタラクティブ通信では、受信者固有の動的なコンテンツを使用して出力ドキュメントを生成します。

コミュニケーション作成ジョブは、[Experience Production Agent](/help/ai-in-aem/agents/brand-experience/experience-production/overview.md)の一部であり、自然言語プロンプトを使用してインタラクティブ通信を開発するように設計されています。 このジョブは、印刷用にパーソナライズされたデータ駆動型の通信を自動的に生成します（PDF形式）。 このジョブはAI アシスタントを通じて表示されます。

コミュニケーション作成ジョブの主な利点には、次のようなものがあります。

* **コミュニケーション開発の高速化**：簡単な自然言語コマンドを使用して迅速にコミュニケーションを作成できるため、従来の製品インターフェイスを習得する必要がありません。
* **一貫性のあるブランドに即したメッセージ**：承認済みのテンプレートとスタイルを使用して、組織のブランディング、テンプレート、スタイルガイドラインに従ったコミュニケーションを作成します。
* **技術的な障壁の軽減**：ビジネスユーザーは、高度な技術的または深い製品の専門知識を必要とせずに、簡単にコミュニケーションを作成できます。

## 機能 {#capabilities}

<!-- * **Create personalized communications with plain text prompt**: You can create communication documents for print (in PDF format) by submitting your requirements in plain language. The job automatically generates appropriate document structures, layouts, and data bindings based on your natural language description. -->

* **テンプレートから作成**：承認済みの組織テンプレートを使用して、ブランドの一貫性とコンプライアンス基準を確保できます。 このジョブは、既存のテンプレートとスタイルガイドラインを活用して、規制要件を満たすブランドに即したメッセージを作成します。

* **既存の画像とドキュメントをインタラクティブ通信に読み込んで変換する**：既存のドキュメントをインタラクティブ通信に読み込んで変換できます。 このジョブは、アップロードされたコンテンツを分析してフィールドを検出し、レイアウトを保存し、動的コンテンツ機能を使用してデータ主導の通信を作成します。 サポートされている形式には、PDF、画像（JPG、PNG）、手描きのテンプレートなどがあります。

## サンプルプロンプト {#sample-prompts}

* *テンプレート（https://[aem-author-url]/path/to/pdf/file*）を使用して、ローン明細書のコミュニケーションを作成します
* *PDFからhttps://[aem-author-url]/path/to/pdf/file*&#x200B;に通信を作成します
* *https://[aem-author-url]/path/to/image/file*&#x200B;の画像ファイルから通信を作成します
* https://[aem-author-url]/path/to/pdf/fileにあるPDF ファイルを使用してレターを作成します

## コミュニケーションを調整 {#refine-with-ic-editor}

AI アシスタントを使用して最初のコミュニケーション構造を作成したら、インタラクティブ通信エディターを使用してドキュメントを調整および強化できます。 インタラクティブ通信エディターでは、次の操作を自然言語で行うことができます。

* **フィールドとコンテンツを追加**：自然言語プロンプトを使用して、新しいフィールド、テキストブロック、画像、チャート、テーブル、その他のコンポーネントをコミュニケーションドキュメントに追加します。 ジョブは指示を解釈し、適切な構造と書式を持つ適切なエレメントを挿入します。

* **フィールドとコンテンツの編集**：会話コマンドを使用して、コミュニケーションドキュメント内の既存のフィールドとコンテンツを変更します。 フィールドプロパティの更新、テキストコンテンツの変更、データバインディングの調整、コンポーネント設定の調整を行います。

* **フィールドとコンテンツの削除**：自然言語の指示を使用して、コミュニケーションドキュメントから不要なフィールド、コンポーネント、またはセクションを削除します。 このジョブは、ドキュメント構造とレイアウトの整合性を維持しながら、指定された要素を削除します。

* **フィールドとコンテンツのスタイル設定**：自然言語プロンプトを使用して、フィールドとコンテンツに書式とスタイル設定を適用します。 ブランドガイドラインやデザイン要件に合わせて、フォント、色、配置、間隔などのビジュアルプロパティを調整できます。

### コミュニケーションを絞り込むためのサンプルプロンプト {#sample-prompts-refining}

* *自動車保険金請求決済レターの生成*
* *免責事項のテキストを斜体にする*
* *免責事項テキストのフォントサイズを12*&#x200B;に変更します
* *免責事項テキストのフォントカラーを赤に更新*
* *ヘッダーとフッターのテキストボックスの背景色を明るいグレーに更新*
* *署名フィールドと確認フィールドを含む新しい免責事項パネルを追加*
* *確認テキストフィールドを削除*
* *3列の支払詳細テーブルを追加*
* *ポリシー番号フィールドの整列を中央に更新*
* *利用条件セクションの行間を1.5*&#x200B;に変更します

インタラクティブ通信エディターの機能について詳しくは、[&#x200B; インタラクティブ通信ドキュメント &#x200B;](/help/forms/introduction-to-interactive-communication.md)を参照してください。

<!-- UNCOMMENT ONCE NO LONGER ALPHA -->

<!--
## Activation {#activation}

You can explore AEM Agents through the [Playground](https://www.aem.live/developer/aem-playground), or connect with your CSM or TAM to discuss access via the Agentic SKU.
-->
