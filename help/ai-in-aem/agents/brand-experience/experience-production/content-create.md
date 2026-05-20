---
title: コンテンツ作成ジョブ
description: Brand Experience Agentのコンテンツ作成ジョブとは何か、およびそれがユーザーに対して何を可能にするかについて説明します。
feature: Edge Delivery Services, Agentic AI
role: User, Admin, Developer
source-git-commit: 5d1a560b4eb386d0c3795d6634742ffce8ef4c71
workflow-type: tm+mt
source-wordcount: '787'
ht-degree: 1%

---


# コンテンツ作成ジョブ {#content-create}

Content Create ジョブは、[Experience Production Agent](/help/ai-in-aem/agents/brand-experience/experience-production/overview.md)の一部であり、自然言語、マーケティング概要、およびAEM テンプレートを使用して、ブランドに即した新しいページを作成します。 Adobe Experience Manager（AEM）as a Cloud ServiceとEdge Delivery Servicesのページ制作を高速化します。

<!-- see Limitations too and update when appropriate -->

>[!NOTE]
>
>コンテンツ作成ジョブは現在、制限付き可用性です。 参加を希望される場合は、公式メールアドレスから[experience-production-agent@adobe.com](mailto:experience-production-agent@adobe.com)にリクエストを送信してください。

## 概要 {#overview}

コンテンツ作成ジョブは、マーケティングブリーフとAEMテンプレートとともに、自然言語を使用してブランドに即した新しいページを生成します。

コンテンツ作成ジョブには、次の場所からアクセスできます。

* [AI アシスタント](#access-ai-assistant)

>[!VIDEO](https://video.tv.adobe.com/v/3488436?learn=on)

コンテンツ作成ジョブを使用するには：

* [さんが](#provide-the-prompt-and-brief)を提供しました：

   * 自然言語プロンプト：ページの作成内容と保存場所を指定します。

   * 概要：

      * コンテンツ作成ジョブでは、エージェントが生成する必要のある内容を説明するマーケティング概要またはドキュメントを使用します。 ジョブは、ブリーフの幅広い形式を受け付けます。 効果的な概要では、多くの場合、目標、オーディエンス、トピック、ターゲット文字数、キーワードを指定します。

* 次に、プロンプトと概要を[送信](#submit)します
* 次に、必要なレイアウトを定義する[AEM テンプレート &#x200B;](#select-a-template)を指定します
* ジョブは、レビュー用に[&#x200B; プランを提供します](#review-the-plan)
* その後、[生成を進め](#proceed-with-generation)、必要に応じてさらに[&#x200B; オーサリングを調整できます](#further-refinement-in-authoring)

エージェントは、生成をテンプレートに合わせて調整し、概要に一致するセクションを追加または削除できます。例えば、単語数の増減が必要な場合などです。

>[!NOTE]
>
>このページでは、例を使用して、添付された概要`https://frescopa.coffee/sustainability/coffee-bean-types`に基づいて新しいページを作成します

## アクセス - AI アシスタント {#access-ai-assistant}

AEMのジョブには、AI アシスタントからアクセスできます。

[`experience.adobe.com`](https://experience.adobe.com)の右上のツールバーから[AI アシスタント &#x200B;](/help/implementing/cloud-manager/ai-assistant-in-aem.md)を開きます。

## プロンプトと概要を入力 {#provide-the-prompt-and-brief}

AI アシスタントでは、次のことをおこなう必要があります。

1. 自然言語を使ってweb サイト内のパスやURLを指定し、何をしたいかを記述したり、ページの配置場所を特定したりします。 例えば、概要に基づいて新しいページを作成します。

   * `create a new page based on the attached at https://frescopa.coffee/sustainability/coffee-bean-types`

     ![&#x200B; コンテンツ作成ジョブ – プロンプトを追加](/help/ai-in-aem/agents/brand-experience/experience-production/assets/create-content-example-create-page.png)

1. リクエストに関連する概要をアップロードします。 概要を読み込むには：

   1. AI アシスタントの左下にある&#x200B;**+**&#x200B;を選択し、**ファイルを添付**&#x200B;を選択します。

      ![&#x200B; コンテンツ作成ジョブ – ブリーフを読み込む](/help/ai-in-aem/agents/brand-experience/experience-production/assets/create-content-example-load-brief.png)

   1. 概要ファイルを追加します。 読み込まれた概要は、プロンプトダイアログの右上に表示されます。

      ![&#x200B; コンテンツ作成ジョブ – ブリーフを読み込みました](/help/ai-in-aem/agents/brand-experience/experience-production/assets/create-content-example-loaded-brief.png)

1. 準備ができたら、青い送信アイコン（青い矢印）を使用して、プロンプトと概要を送信します。

## テンプレートを選択 {#select-a-template}

その後、エージェントはテンプレートの指定をリクエストします。 このテンプレートは、エージェントにページ構造とレイアウトを提供します。 生成はそのレイアウトに準拠します。 担当者は、ブリーフに基づいて、必要に応じてセクションを追加および削除できます。たとえば、異なる単語数に対応できます。

![&#x200B; コンテンツ作成ジョブ – テンプレートを指定](/help/ai-in-aem/agents/brand-experience/experience-production/assets/create-content-example-select-template.png)

## プランを見る {#review-the-plan}

次に、担当者は、入力とブリーフの分析にもとづいて、変更の計画を立てます。 プランを調整するか、プランに進んで生成を開始することができます。

>[!NOTE]
>
> [&#x200B; ガバナンスエージェント &#x200B;](/help/ai-in-aem/agents/governance/overview.md)を使用している場合、生成はブランドガイドラインに従うことができます。

![&#x200B; コンテンツ作成ジョブ – プランを確認](/help/ai-in-aem/agents/brand-experience/experience-production/assets/create-content-example-review-plan.png)

## 生成を進める {#proceed-with-generation}

生成が完了すると、エージェントは2つのリンクを提供します。

* **プレビュー** リンク
* **編集** リンク
   * 編集リンクを使用して[AEM オーサリングサーフェス &#x200B;](#further-refinement-in-authoring)でページを開き、さらに絞り込みます。

![&#x200B; コンテンツ作成ジョブ – 生成を続行](/help/ai-in-aem/agents/brand-experience/experience-production/assets/create-content-example-proceed-generation.png)

## オーサリングのさらなる改善 {#further-refinement-in-authoring}

AEMでページを編集すると、オーサリング環境で開きます。例えば、[&#x200B; ユニバーサルエディター](/help/sites-cloud/authoring/universal-editor/authoring.md)や[&#x200B; ページエディター](/help/sites-cloud/authoring/page-editor/introduction.md)などです。

[&#x200B; ユニバーサルエディター](#universal-editor-edit-text-with-the-assistant)では、AI アシスタントは&#x200B;*コンテキスト対応*&#x200B;です。キャンバス上の要素を選択し、アシスタントと一緒に作業できます。

### ユニバーサルエディター – アシスタントでテキストを編集する {#universal-editor-edit-text-with-the-assistant}

オーサリング時にアシスタントからコピーを調整するには：

1. [&#x200B; ユニバーサルエディター](/help/sites-cloud/authoring/universal-editor/authoring.md)で要素を選択します。
1. 右上隅のAI アシスタントを開き、プロンプトを入力して送信します。

プロンプトの例：

* `Update to Explore the World of Coffee`
* `Update to be more engaging for the 30-40 year old age demographic and avid coffee drinker`

「**変更を適用** （または同等）を選択して、更新がページに表示されるようにします。

## アクティベーション {#activation}

[Playground](https://www.aem.live/developer/aem-playground)からAEM Agentsを検索するか、CSMまたはTAMに接続して、Agentic SKU経由でのアクセスについて話し合うことができます。

## 制限事項 {#limitations}

次の制限事項に注意してください。

* この機能は限定的で、参加するには手動オンボーディングが必要です。 参加を希望される場合は、公式メールアドレスから[experience-production-agent@adobe.com](mailto:experience-production-agent@adobe.com)にリクエストを送信してください。

## その他のリソース {#additional-resources}

Experience Production Agentを引き続き検討する場合は、次のリソースが役立つ可能性があります。

* [Experience Production Agent Workbook](https://www.adobe.com/go/aem-epa-workbook_jp)をガイド付きの実践的な手順に使用することもできます。
