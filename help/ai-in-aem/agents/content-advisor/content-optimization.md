---
title: Content Optimization エージェント
description: Content Optimization Agentを使用して、自然言語の指示を適用してチャネルに対応したバリエーションを作成し、ユーザーがアセットを改良および適応する方法を説明します。
feature: Edge Delivery Services, Agentic AI
role: User, Admin, Developer
exl-id: 896fc25b-7f60-47b8-9264-2ef6b85d954c
source-git-commit: 81f85045212ca6fd92f2b665aeceaa0d4b92318c
workflow-type: tm+mt
source-wordcount: '956'
ht-degree: 0%

---


# Content Optimization エージェント {#content-optimization-agent}

[AEMのContent Advisor Agentの一部として、](/help/ai-in-aem/agents/content-advisor/overview.md)content optimization Agentは、ユーザーが自然言語の指示を適用してチャネル対応のバリエーションを作成することで、アセットを調整および調整する方法を変革します。 新しいレンディションの生成、ビジュアルプロパティの調整、背景の変更、特定のデジタルチャネル用のアセットの準備など、担当者はユーザーの意図を解釈し、複雑な編集タスクを自動的に実行します。 [content discovery agent](/help/ai-in-aem/agents/content-advisor/discovery.md)とシームレスに連携し、検索したアセットを取り込み、コア [Dynamic Media with OpenAPI機能](/help/assets/dynamic-media-open-apis-overview.md)を使用して最適化されたバリエーションを生成します。この機能は、ブランド、チャネル、キャンペーンの要件を満たしており、手動でのデザイン作業は必要ありません。

content optimization agentの主な利点は次のとおりです。

* **簡単なアセット変換**：シンプルな会話形式のプロンプトを、サイズ変更、シャープ化、ミラーリング、再配色などの正確な画像操作に変換します。専門的な編集ツールは不要になります。

* **チャネルに合わせて最適化された出力**: Instagram ストーリー、web バナー、その他のマーケティング上の顧客接点など、特定のプラットフォームに合わせてカスタマイズされたレンディションをすばやく生成し、アセットをすぐに使用できるようにします。

* **Creativeの大規模な機能強化**：背景の変更やグラフィックオーバーレイなどの視覚的な調整と機能強化を適用して、チームの作業を遅らせることなく、大規模なクリエイティブワークフローをサポートします。

* **[Content Discovery エージェントとのシームレスなコラボレーション](/help/ai-in-aem/agents/content-advisor/discovery.md)**: Content Discovery エージェントによって識別されたアセットに基づいて構築され、エンドツーエンドのアセットの取得と最適化を自然な会話で実現します。

>[!IMPORTANT]
>
>AIによる回答は、不正確または誤解を招く可能性があります。 修正案と回答案を再確認しましょう。
>
>[Adobe Experience Cloud生成AI ユーザーガイドライン &#x200B;](https://www.adobe.com/legal/licenses-terms/adobe-dx-gen-ai-user-guidelines.html)も参照してください。

>[!VIDEO](https://video.tv.adobe.com/v/3480078)

## 前提条件 {#prerequisites-content-optimization-agent}

画像アセットのバリエーションや最適化を生成できます。 次が必要です。

* 有効なDynamic Media ライセンス

* AEM as a Cloud Service環境でOpenAPIを有効にしたDynamic Media。

* AEM as a Cloud Service環境の[承認済み状態](/help/assets/manage-organize-assets-view.md#manage-asset-status)のアセット。

## スキル {#skills-content-optimization-agent}

コンテンツ最適化エージェントには、次のスキルが用意されています。

* **自然言語を通じて意図を理解**

  content optimization agentは、自然言語によるプロンプトからユーザーの意図を解釈し、チャネル、キャンペーン、オーディエンスのコンテキストを考慮して、最も関連性の高い最適化アクションを決定します。

* **動的コンテンツのバリエーションを生成**

  Content optimization Agentは、異なるチャネルや形式タイプに合わせてカスタマイズされた動的URLとして、最適化されたバリエーションを作成します。

* **画像コンテンツを最適化**

  コンテンツ最適化エージェントは、形式の変換、解像度の調整、切り抜き、シャープ処理などの機能強化を適用して、画質を向上させます。

* **多変量アセットの最適化**

  Content Optimization Agentは、content discovery agentから返されたアセットから、単一の自然言語プロンプトを使用して複数の最適化された画像バリエーションを生成できるため、ユーザーはチャネル対応のレンディションを迅速かつ効率的に生成できます。

## 登場人物 {#personas-content-optimization-agent}

Content Optimization Agentの主要なペルソナであるチャネルマーケターは、適切な高解像度のソースコンテンツを選択し、チャネルやオーディエンスセグメントに合わせて最適化された形式を要求できます。

地域のマーケターや代理店のスタッフも、コンテンツ最適化エージェントを使用して、より迅速で一貫性のあるコンテンツ制作をサポートする、チャネルに合わせた画像バリエーションを迅速に生成できます。

## アクセス方法 {#access-content-optimization-agent}

AI アシスタントを介して、AEMのcontent optimization エージェントにアクセスできます。 [`experience.adobe.com`](https://experience.adobe.com)にログオンすると、`Ask AI Assistant anything` フィールドを使用して自然言語でプロンプトを指定することで、AI アシスタントとのやり取りを開始できます。

![&#x200B; コンテンツ最適化エージェントにアクセス &#x200B;](/help/ai-in-aem/agents/content-advisor/assets/access-discovery-agent.png)

## 一般的なユースケースとサンプルプロンプト {#use-cases-prompts}

[content discovery エージェントを使用して適切なアセットを検索し、content optimization エージェントを使用します。](/help/ai-in-aem/agents/content-advisor/discovery.md)関連する画像が表示されると、ユーザーは検索結果から直接、1つまたは複数のアセットに対して、最適化されたバリエーションまたはチャネル固有のバリエーションを生成できます。 あるいは、事前の検索を実行することなく、プロンプトでアセットのUUIDまたはアセットパスを指定してバリエーションを生成することもできます。 このワークフローは、高品質のインプットと、常により優れた最適化結果を保証します。 [詳細については、利用可能な最適化の完全なリスト &#x200B;](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/stable/assets/delivery/)を参照してください。

* **高解像度レンディションの作成**

  エージェントは、指定された解像度と品質レベルでアセットの新しいレンディションを生成できるため、手作業での編集なしでチャネルに対応したバリエーションを簡単に準備できます。


  サンプルプロンプト：

  `2000px`のレンディションを`JPEG`として作成し、画質を`80%`にします。

  [content discovery agent](/help/ai-in-aem/agents/content-advisor/discovery.md)を使用して適切なアセットを検索し、複数の検索結果が表示された場合は、次のプロンプトを使用します。

  3つ目の検索結果の場合、`2000px`のレンディションを`JPEG`として作成し、画質を`80%`にします。

  OR

  `Asset ID`の場合、2000px レンディションを`JPEG`として生成し、画質は`80%`です

* **画像の強化**

  担当者は、シャープなどの視覚的な改善を適用することで、キャンペーン全体で使用する前に、アセットが鮮明で明確に定義されていることを確認できます。

  サンプルプロンプト：

  画像をシャープにします。


* **背景色の調整**

  エージェントは、ブランド固有のカラースキームやキャンペーン主導のビジュアルテーマをサポートする、透明なアセットの背景色を更新または置換できます。

  サンプルプロンプト：

  `PNG`の背景色を`#ff8932`に変更します。

* **方向の変換**

  また、外部の編集ツールを必要とせずに、レイアウトニーズやクリエイティブの方向性に合わせてビジュアルを反転したり、ミラーしたりすることができます。

  サンプルプロンプト：

  画像を水平方向にミラーリングします。

* **チャネルに最適化されたレンディション**

  Ai エージェントは、Instagram ストーリーなどのプラットフォーム固有の要件に合わせたレンディションを生成し、アセットが形式、比率、品質のガイドラインを自動的に満たすようにすることができます。

  サンプルプロンプト：

  `Instagram` ストーリーのレンディションを作成します。

* **ブランドオーバーレイとコンポジット生成**

  担当者は、正確な配置でプロモーショングラフィック、オーバーレイ、バッジを既存のアセットに適用でき、キャンペーン用のコンポジットの迅速な作成をサポートします。

  サンプルプロンプト：

  プロモーションバナーの上に`30%`個の割引グラフィックを配置し、中央から`100px`個配置した画像をオーバーレイします。

  >[!NOTE]
  >
  >オーバーレイの位置が正確でない場合があります。


## 最適化結果 {#content-optimization-agent-results}

最適化プロンプトを指定すると、コンテンツ最適化エージェントは、アセットタイプに基づく便利なアクセスオプションとともに、強化されたアセットを返します。

* **画像**：応答には、サムネールのプレビューと、Dynamic Media URLを開くか、最適化された画像をダウンロードするためのオプションが含まれています。

* **PDF ドキュメント**：応答には、サムネールのプレビューと、Dynamic Media URLを開くか、最適化されたファイルをダウンロードするためのオプションが含まれています。

* **ビデオ**：応答は、Dynamic Media URLを開くか、最適化されたビデオをダウンロードするためのオプションを提供します。

![&#x200B; コンテンツ最適化の結果](/help/ai-in-aem/agents/content-advisor/assets/download-content-optimization.png)

こうした結果により、最適化された出力を容易に確認し、下流のチャネルやワークフローですばやく使用することができます。


## 制限事項 {#limitations-content-optimization}

* 背景色の設定はサポートされていません。

<!--


## Prompting best Practices {#prompting-best-practices-content-optimization-agent}

The following are some prompting best practices:

* Be explicit about the enhancement you want the content optimization agent to apply. Clearly state the transformation or adjustment you expect. Precise instructions help the agent produce accurate and predictable results. For example, Instead of `Make it good quality`, specify `Create a JPEG image with 90% quality`.

* Provide detailed parameters whenever possible. The more context you give, such as dimensions, format, quality, placement, or color values, the more tailored the output is.

-->
