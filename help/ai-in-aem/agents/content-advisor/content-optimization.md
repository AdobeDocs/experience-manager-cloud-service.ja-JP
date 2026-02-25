---
title: コンテンツ最適化ジョブ
description: コンテンツ最適化ジョブを使用して、自然言語の手順を適用してチャネル対応のバリエーションを作成することで、ユーザーがアセットを調整および適応する方法を変換する方法を説明します。
feature: Edge Delivery Services, Agentic AI
role: User, Admin, Architect, Developer
exl-id: 896fc25b-7f60-47b8-9264-2ef6b85d954c
source-git-commit: a31cd8ea0ae02a51efb748097c195d68dc8b554d
workflow-type: tm+mt
source-wordcount: '933'
ht-degree: 0%

---


# コンテンツ最適化ジョブ {#content-optimization-job}

[AEMのコンテンツアドバイザーエージェントの一部であるコンテンツ最適化ジョブは &#x200B;](/help/ai-in-aem/agents/content-advisor/overview.md) 自然言語の説明を適用してチャンネルに対応するバリエーションを作成することにより、ユーザーがアセットを調整および適応する方法を変えます。 新しいレンディションの生成、視覚的なプロパティの調整、背景の変更、特定のデジタルチャネル向けのアセットの準備など、いずれの場合も、ジョブはユーザーの意図を解釈し、複雑な編集タスクを自動的に実行します。 [&#x200B; コンテンツ検出ジョブ &#x200B;](/help/ai-in-aem/agents/content-advisor/discovery.md) とシームレスに連携し、検出したアセットを取得して、コアの [Dynamic Media と OpenAPI 機能 &#x200B;](/help/assets/dynamic-media-open-apis-overview.md) を使用して最適化されたバリエーションを生成します。これにより、手動での設計の手間をかけることなく、ブランド、チャネル、キャンペーンの要件を満たすことができます。

コンテンツ最適化ジョブの主なメリットには、次のようなものがあります。

* **簡単なアセット変換**：シンプルな会話プロンプトを、サイズ変更、シャープニング、ミラーリング、再配色などの正確な画像操作に変換し、特別な編集ツールを不要にします。

* **チャネルに最適化された出力**:Instagram ストーリー、web バナー、その他のマーケティングタッチポイントなどの特定のプラットフォーム用にカスタマイズされたレンディションをすばやく生成し、アセットがすぐに使用できるようにします。

* **Creativeの大規模な機能強化**：背景の変更やグラフィックオーバーレイなどの視覚的な調整や機能強化を適用して、チームの速度を低下させることなく、大量のクリエイティブワークフローをサポートします。

* **[コンテンツ検出ジョブとのシームレスなコラボレーション](/help/ai-in-aem/agents/content-advisor/discovery.md)**：コンテンツ検出ジョブで特定されたアセットに基づいて、自然な会話によるエンドツーエンドのアセット取得と最適化が可能になります。

>[!IMPORTANT]
>
>AI によって生成された応答は、不正確であったり、誤解を招く可能性があります。 推奨される修正および回答を再確認してください。
>
>[Adobe Experience Cloud生成 AI ユーザーガイドラインも参照してください。](https://www.adobe.com/legal/licenses-terms/adobe-dx-gen-ai-user-guidelines.html)

>[!VIDEO](https://video.tv.adobe.com/v/3480078)

## 前提条件 {#prerequisites-content-optimization-job}

画像アセットのバリエーションまたは最適化を生成する。 以下が必要です。

* 有効な Dynamic Media ライセンス

* AEM as a Cloud Service環境で OpenAPI を有効にした Dynamic Media。

* AEM as a Cloud Service環境内の [&#x200B; 承認済み &#x200B;](/help/assets/manage-organize-assets-view.md#manage-asset-status) のアセット。

## スキル {#skills-content-optimization-job}

コンテンツ最適化ジョブには、次のスキルが用意されています。

* **自然言語によるインテントの理解**

  コンテンツ最適化ジョブでは、自然言語プロンプトからユーザーの意図を解釈し、チャネル、キャンペーンおよびオーディエンスコンテキストを考慮して、最も関連性の高い最適化アクションを決定します。

* **動的コンテンツのバリアントを生成**

  コンテンツ最適化ジョブは、様々なチャネルやフォーマットタイプ向けにカスタマイズされた動的 URL として、最適化されたバリアントを作成します。

* **画像コンテンツを最適化**

  コンテンツ最適化ジョブでは、形式変換、解像度の調整、切り抜き、シャープニングなどの機能強化を適用して画質を向上させます。

* **マルチバリアントアセットの最適化**

  コンテンツ最適化ジョブでは、単一の自然言語プロンプトを使用して、コンテンツ検出ジョブによって返されたアセットから最適化された複数の画像バリエーションを生成でき、ユーザーはチャネルに対応するレンディションを迅速かつ効率的に作成できます。

## 登場人物 {#personas-content-optimization-job}

コンテンツ最適化ジョブの主要なペルソナであるチャネルマーケターは、適切な高解像度ソースコンテンツを選択し、チャネルやオーディエンスセグメントに合わせて最適化された形式をリクエストできます。

また、地域のマーケターやエージェンシーワーカーは、コンテンツ最適化ジョブを使用して、チャネルに対応した画像バリエーションを迅速に生成し、迅速で一貫性のあるコンテンツ制作をサポートすることもできます。

## アクセス方法 {#access-content-optimization-job}

AI アシスタントを使用して、AEMのコンテンツ最適化ジョブにアクセスできます。 [`experience.adobe.com`](https://experience.adobe.com) にログオンし、`Ask AI Assistant anything` フィールドを使用して自然言語でプロンプトを指定することで、AI アシスタントとのやり取りを開始できます。

![&#x200B; コンテンツ最適化ジョブへのアクセス &#x200B;](/help/ai-in-aem/agents/content-advisor/assets/access-discovery-agent.png)

## 一般的なユースケースとサンプルプロンプト {#use-cases-prompts}

[&#x200B; コンテンツ検出ジョブで適切なアセットを検索して、コンテンツ最適化ジョブを使用します。](/help/ai-in-aem/agents/content-advisor/discovery.md) 関連する画像が表示されると、ユーザーは、検索結果から直接、1 つまたは複数のアセットに対して、最適化された、またはチャネル固有のバリアントを生成できます。 このワークフローにより、高品質の入力と一貫したより優れた最適化結果が保証されます。 [&#x200B; 詳しくは、使用可能な最適化の完全なリストを参照 &#x200B;](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/stable/assets/delivery/) てください。

* **高解像度レンディションの作成**

  このジョブでは、指定された解像度および品質レベルでアセットの新しいレンディションを生成できるので、手動で編集しなくても、チャネルに対応したバリエーションを簡単に準備できます。


  プロンプトの例：

  `2000px` 品質の `JPEG` レンディション `80%` 作成します。

  [&#x200B; コンテンツ検出ジョブ &#x200B;](/help/ai-in-aem/agents/content-advisor/discovery.md) を使用して適切なアセットを検索し、検索結果が複数ある場合は次のプロンプトを使用します。

  3 番目の検索結果として、`2000px` 品質の `JPEG` しいレンディションを作成 `80%` ます。

  OR

  `Asset ID` の場合は、`JPEG` 品質の `80%` に 2000 px のレンディションを生成します

* **画像の機能強化**

  このジョブでは、シャープニングなどの視覚的な改善を適用して、キャンペーン全体で使用する前にアセットが鮮明で明確に定義されたように見えるようにします。

  プロンプトの例：

  画像をシャープにします。


* **背景色の調整**

  ジョブでは、透明アセットの背景色を更新または置換し、ブランド固有のカラースキームまたはキャンペーン駆動型のビジュアルテーマをサポートできます。

  プロンプトの例：

  `PNG` の背景色を `#ff8932` に変更します。

* **方向変換**

  ジョブでは、外部の編集ツールを必要とせずに、レイアウトニーズやクリエイティブな方向性に合わせてビジュアルを反転またはミラー化できます。

  プロンプトの例：

  画像を水平方向にミラーリングします。

* **チャネルに最適化されたレンディション**

  このジョブでは、Instagram ストーリーなどプラットフォーム固有の要件に合わせてレンディションを作成し、アセットが形式、比率、品質のガイドラインを自動的に満たすようにします。

  プロンプトの例：

  `Instagram` ストーリーのレンディションを作成します。

* **ブランド化されたオーバーレイと複合生成**

  このジョブでは、プロモーショングラフィック、オーバーレイまたはバッジを正確に配置された既存のアセットに適用し、キャンペーン対応のコンポジットを迅速に作成できます。

  プロンプトの例：

  プロモーションのバナーの上に `30%` 割引グラフィックを重ねて、中央から `100px` に置きます。

  >[!NOTE]
  >
  >オーバーレイの位置が正確でない可能性があります。


## 最適化結果 {#content-optimization-job-results}

最適化プロンプトを指定すると、コンテンツ最適化ジョブは、拡張アセットと、アセットタイプに基づいた便利なアクセスオプションを返します。

* **画像**：応答には、サムネールプレビューと、Dynamic Media の URL を開くオプションまたは最適化された画像をダウンロードするオプションが含まれます。

* **PDF ドキュメント**：応答には、サムネールプレビューと、Dynamic Media の URL を開く、または最適化されたファイルをダウンロードするためのオプションが含まれます。

* **ビデオ**：応答には、Dynamic Media の URL を開くオプションや、最適化されたビデオをダウンロードするオプションが用意されています。

![&#x200B; コンテンツの最適化結果 &#x200B;](/help/ai-in-aem/agents/content-advisor/assets/download-content-optimization.png)

これらの結果により、最適化された出力を簡単に確認し、ダウンストリームチャネルやワークフローですぐに使用できます。


## 制限事項 {#limitations-content-optimization}

* 背景色の設定はサポートされていません。

<!--


## Prompting best Practices {#prompting-best-practices-content-optimization-job}

The following are some prompting best practices:

* Be explicit about the enhancement you want the content optimization job to apply. Clearly state the transformation or adjustment you expect. Precise instructions help the agent produce accurate and predictable results. For example, Instead of `Make it good quality`, specify `Create a JPEG image with 90% quality`.

* Provide detailed parameters whenever possible. The more context you give, such as dimensions, format, quality, placement, or color values, the more tailored the output is.

-->
