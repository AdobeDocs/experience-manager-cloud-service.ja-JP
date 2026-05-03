---
title: AI翻訳統合の設定
description: Translation Cloud サービスとTranslation Integration Frameworkを使用して、Adobe Experience ManagerをAzure OpenAIに接続してエージェンティック翻訳を行う方法について説明します。
feature: Language Copy
role: Admin
badgeSaas: label="AEM Sites" type="Positive" tooltip="AEM Sitesに適用）。"
solution: Experience Manager Sites
source-git-commit: cb7dcc07a5913d6c7e88e0eec03f0003f1e3997a
workflow-type: tm+mt
source-wordcount: '624'
ht-degree: 0%

---

# AI翻訳統合の設定 {#ai-translation-integration}

AI翻訳の統合により、Adobe Experience Managerで作成したコンテンツの翻訳サービスとして&#x200B;**大規模言語モデル（LLM）**&#x200B;を使用できます。 AEMをLLM プロバイダー（Microsoft Azure OpenAI以降）に接続し、他のコネクタと同じ[翻訳ワークフロー](/help/sites-cloud/administering/translation/overview.md)を再利用し、オプションで&#x200B;**翻訳スタイルガイド**&#x200B;をアップロードすることで、AEMがロケール間でトーン、用語、ブランド言語の一貫性を維持するルールを生成できるようにします。

翻訳プロジェクト、クラウド設定、および翻訳統合フレームワークの背景については、[多言語サイトのコンテンツの翻訳](overview.md)および[翻訳統合フレームワークの設定](integration-framework.md)を参照してください。

## AEMでAI翻訳を利用する方法 {#how-ai-translation-fits-in-aem}

大規模言語モデルは、文脈的な一語一句置換ではなく、文脈、トーン、イディオムに注意を払って全文を翻訳できます。 AI翻訳の統合を設定する場合、LLMは、AEMを介して接続する他のプロバイダーと同じ方法で&#x200B;**サードパーティ翻訳サービス**&#x200B;として機能します。 LLM サービスの&#x200B;**独自のライセンスと資格情報**&#x200B;を指定します。

初期サポートは、AEMを&#x200B;**Azure OpenAI**&#x200B;に接続します。 Adobeでは、今後のリリースでさらに多くのプロバイダーをサポートする予定です。

LLM接続とオプションのスタイルガイドの両方を、他の翻訳設定と並行して&#x200B;**翻訳クラウドサービス**&#x200B;で設定します。 様々な[ クラウド設定](/help/sites-cloud/administering/translation/integration-framework.md#creating-a-translation-integration-configuration)に対して異なる翻訳サービスを使用できます。例えば、ある設定ではAI翻訳を使用し、別の設定では従来の機械翻訳コネクタを使用できます。

## 翻訳クラウドサービスの設定 {#configure-translation-cloud-services}

他の翻訳クラウド設定を管理する領域と同じ領域でAI翻訳を設定します。

1. [ グローバルナビゲーションメニュー](/help/sites-cloud/authoring/basic-handling.md#global-navigation)で、**ツール**/**クラウドサービス**/**翻訳クラウドサービス**&#x200B;を選択します。
1. AI翻訳を有効にする設定を開くか作成します（機能が広く適用される必要がある場合は`/conf/global`を含みます）。

![翻訳設定の管理場所を示す翻訳クラウドサービスコンソール。](assets/ai-translation-integration/aem_ai-translation_translation-cloud-services.png)

## LLM接続の設定 {#configure-the-llm-connection}

**Agentic Translation Configuration** エクスペリエンスには、プロバイダーを接続する&#x200B;**LLM Config** セクションが含まれています。

1. Translation Cloud Services エントリのAI翻訳設定を開きます。
1. **[!UICONTROL LLM Config]**&#x200B;を選択します。
1. プロバイダーを選択します（例：**Azure OpenAI**）。
1. サブスクリプションに必要な資格情報とエンドポイントの詳細を入力します（**API Key**、**API Version**、**Base Path**、**Deployment Name**、およびプロバイダーが必要とするその他のフィールド）。
1. 設定を保存します。

![Agentic Translation Configurationの画面。LLM Config タブとAzure OpenAI フィールド。](assets/ai-translation-integration/aem_ai-translation_agentic-translation-llm-config.png)

## 翻訳スタイルガイドと生成ルールの追加 {#add-translation-style-guides-and-generated-rules}

**翻訳スタイルガイド**&#x200B;件のドキュメント（通常はターゲット言語ごとに1件）をアップロードできます。 AEMは各ガイドを分析し、ブランドと言語的な期待値に合わせてアウトプットを調整するために&#x200B;**翻訳ルール**&#x200B;を生成します。

1. **エージェント翻訳設定**&#x200B;で、**[!UICONTROL LLM ガイドライン]**&#x200B;を選択します。
1. ロケールを選択し、**[!UICONTROL アップロード]**&#x200B;を使用して、その言語のスタイルガイドドキュメントを追加します。
1. AEMがガイドを処理している間、ステータスインジケーターに進行状況が表示されます（**処理中**、**完了**、または&#x200B;**中断**）。
1. 生成されたルールをエディターで確認または編集します（例えば、トーン、用語、例をキャプチャするJSON）。

選択した言語のロケールリストと生成された翻訳ルールを表示する![LLM ガイドライン タブ。](assets/ai-translation-integration/aem_ai-translation_agentic-translation-llm-guidelines.png)

## フレームワークでのデフォルトの翻訳方法の設定 {#set-the-default-translation-method-in-the-framework}

クラウド設定が保存されたら、翻訳プロジェクトを作成する際に[翻訳統合フレームワーク ](integration-framework.md)設定で&#x200B;**エージェント翻訳**&#x200B;をデフォルトの動作として登録します。 必要に応じて、プロジェクトごとにメソッドを変更できます。

エージェント型翻訳を含む翻訳方法オプションを表示する![翻訳統合フレームワークのサイト タブ。](assets/ai-translation-integration/aem_ai-translation_translation-integration-framework-default.png)

## 翻訳プロジェクトの実行 {#run-translation-projects}

AI翻訳を設定してページに関連付けると、他の翻訳プロバイダーと同じように[翻訳プロジェクトを作成して実行](managing-projects.md)できます。 ページ、コンテンツフラグメント、アセットのコンテンツは、翻訳ルールとフレームワークの設定に従います。

>[!NOTE]
>
>AI翻訳の統合は、Adobe Experience Manager](/help/implementing/cloud-manager/ai-assistant-in-aem.md) チャット UIの[AI アシスタントまたはExperience Production Agent インターフェイスから利用できる&#x200B;**not**&#x200B;です。 この記事で説明されている翻訳ワークフローとコンソールを使用します。

