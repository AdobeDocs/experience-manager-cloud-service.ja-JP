---
title: コンテンツ更新ジョブ
description: Brand Experience Agentのコンテンツ更新ジョブとは何か、およびそれがユーザーに対して何ができるかを説明します。
feature: Edge Delivery Services, Agentic AI
role: User, Admin, Developer
exl-id: e2d1dae8-38de-4357-bb14-ad35acb71aee
source-git-commit: dcf2b9f2966144fac969563a395a72fa81ce2751
workflow-type: tm+mt
source-wordcount: '1109'
ht-degree: 1%

---


# コンテンツ更新ジョブ {#content-update}

[Experience Production Agent](/help/ai-in-aem/agents/brand-experience/experience-production/overview.md)のコンテンツ更新ジョブは、Adobe Experience Manager（AEM）as a Cloud ServiceとEdge Delivery Servicesの日常的な作業を高速化するために、コンテンツ制作を自動化します。

## 概要 {#overview}

コンテンツ更新ジョブは、コンテンツフラグメント、ページ、フォーム、アセットなどの既存のコンテンツを更新します。 コンテンツ要素の更新、削除、置換、追加などのアクションを実行し、エクスペリエンスを正確かつ最新の状態に保つことができます。 入力は自然言語の説明にすることができ、Jira PDFやスクリーンショットを使用して使用する場合も入力を提供できます。

コンテンツ更新ジョブは、自然言語またはビジュアルを通じて、ページのコンテンツ更新に提供する詳細を変換します。 更新が必要なページのURLと、更新が必要な内容の詳細を指定すると、エージェントジョブがタスクを完了します。 AEM as a Cloud Serviceで使用すると、ジョブは新しい[launch](/help/sites-cloud/authoring/launches/overview.md)を作成し、適用する前に更新を確認できます。 ドキュメントのオーサリングで使用すると、ジョブは新しい[&#x200B; バージョン &#x200B;](https://experienceleague.adobe.com/en/docs/experience-manager-learn/sites/document-authoring/how-to/document-versions#)を作成します。

>[!VIDEO](https://video.tv.adobe.com/v/3486418?learn=on)

## 機能 {#capabilities}

コンテンツ更新ジョブには、次の場所からアクセスできます。

* [AI アシスタント](#ai-assistant)
* [Jira](#jira)

## AI アシスタント {#ai-assistant}

AEMのジョブには、AI アシスタントからアクセスできます。

右上のツールバーから[AI アシスタント &#x200B;](/help/implementing/cloud-manager/ai-assistant-in-aem.md#ai-use)を開いて、会話を開始します。

![ツールバーの AI アシスタントアイコン](/help/ai-in-aem/agents/brand-experience/experience-production/assets/ai-assistant-icon.png)

### 公開URLの設定 {#configuring-the-publish-url}

更新を適用する場所をエージェントに指示するには、ページリンクを指定する必要があります。 オーサーURLまたはパブリッシュ URLを指定できます。

公開（公開） URLを使用するには、1回限りの設定を行う必要があります。

* 前提条件：

   * 設定を行うには、ユーザーにシステム管理者権限または製品管理者権限が必要です。

* 構成：

   1. URLのコンテンツ更新をリクエストして、コンテンツ更新ジョブを呼び出します。
   1. アシスタントが、いくつかの質問をすることによって、設定を順を追って説明します。
   1. 公開URLが設定され、使用できるようになります。

次に例を示します。

![&#x200B; コンテンツ更新ジョブ – 公開URLの設定](/help/ai-in-aem/agents/brand-experience/experience-production/assets/content-update-publish-url-configuration.png)

### プロンプト {#prompts}

コンテンツの更新を開始するには、幅広い自然言語プロンプトを使用できます。 更新するページの公開（公開） URL、またはオーサー環境URLを指定する必要があります。 サポートされている動詞の一部は、置換、更新、削除、変更、修正、調整、削除です。

### サンプルプロンプト {#sample-prompts}

プロンプトの例には、次のようなものがあります。

* `<your-publish-URL>`の更新時に、「完璧なコーヒーは4つの質問です！」と表示されます。 “ Your coffee, your way!” 「あなたのコーヒー、あなたの道」
* `<your-author-env-URL>`で画像を「holdingcup.png」から「stairhead.png」に置き換えます
* `<your-publish-URL>`の「コーヒークイズを開始」ボタンをより魅力的なバージョンに変更する
* `<your-author-env-URL>`で、「未請求の特典はギフトです！」のセクションを削除します。
* に基づいて`<your-author-env-URL>`更新されました

### AI アシスタントでのファイルアップロード {#file-upload-in-ai-assistant}

自然言語プロンプトを直接入力するだけでなく、ドキュメントをアップロードして変更をリクエストすることもできます。

プロンプトメニューの左下にある`+` アイコンを使用して、要件を指定したファイルをアップロードします。 サポートされているファイル形式には、PDF、JPG、PNG、DOCXなどがあります。

![&#x200B; コンテンツ更新ジョブ – ファイルのアップロード &#x200B;](/help/ai-in-aem/agents/brand-experience/experience-production/assets/content-update-file-upload.png)

例えば、要求された変更を指定する注釈付きPDFは次のようになります。

![&#x200B; コンテンツ更新ジョブ – 注釈付きPDF](/help/ai-in-aem/agents/brand-experience/experience-production/assets/content-update-annotated-pdf.png)

>[!VIDEO](https://video.tv.adobe.com/v/3491297?learn=on)

### Brand Governance Agentによるオーケストレーション  {#orchestration-with-the-brand-governance-agent}

組織がブランドポリシーをインポートした場合、コンテンツ更新ジョブは、エージェント型コンテンツの更新中にこのポリシーを使用します（[概要](#overview)のビデオを参照）。

次のような&#x200B;*処方箋* プロンプトの場合：

* `on <your-publish-URL> update “Your perfect coffee is four questions away!” to “Your coffee, your way!”`

コンテンツ更新ジョブは[&#x200B; ブランドガバナンスエージェント &#x200B;](/help/ai-in-aem/agents/brand-experience/overview.md)と連携し、提供されたコピーがブランドに準拠しているかどうかをユーザーに通知します。

![&#x200B; コンテンツ更新ジョブ - Brand Governance Agentとのオーケストレーション &#x200B;](/help/ai-in-aem/agents/brand-experience/experience-production/assets/content-update-brand-experience.png)

次のような抽象的なプロンプトの場合：

* `on <your-publish-env-URL> change “Take our Coffee Quiz” button to a more engaging version`

生成時に担当者は、ブランドガイドラインを利用して、出力がブランド基準に沿ったものであることを確認します。

## Jira {#jira}

Jiraでコンテンツ更新ジョブを使用すると、編集を自動化する手順を含むチケットを作成できます。

### チケットの作成 {#create-a-ticket}

（任意のタイプの） Jira チケットを作成します。 チケットの「**説明**」フィールドには、次の2つの必須の詳細が必要です。

1. 編集する必要があるページの公開向けURL。

1. 必要な変更。

   このジョブは、次の形式の範囲をサポートして、変更を記述します。

   * チケットの説明に記載されている自然言語
      * 例えば、「見出しをXからYに変更する」などです。
   * 注釈付きPDFが添付されました
      * 例えば、ページのPDFを作成し、変更する内容を詳細に説明する注釈を追加します
   * 添付のPDFのコメント
      * 例えば、ページのPDFを作成し、変更したい内容を詳細に説明するコメントを追加します
   * Annotated screenshot attached
      * 例えば、ページの一部のスクリーンショットを撮り、変更したい内容を詳細に説明する注釈を追加します
   * 自然言語の変更を含む、添付されたMicrosoft Word ファイル

### チケットからジョブを呼び出す {#invoke-the-job-from-your-ticket}

ジョブを使用するには、チケットにコメントを追加します。 コメントでは、`@`記号を含むジョブと指示について説明します。

次に例を示します。

* `@aemagent@adobe.com process this ticket`

### どのように相互作用するか {#how-the-agent-interacts}

ジョブにコマンドを発行すると、Jiraでコメントが返されます。 コメントには、ジョブの進捗状況と実行されたアクションが詳細に記載されます。

更新をトリガーする`process` コマンドの場合、応答はシーケンスに従う可能性があります。

* 最初のコメントは、ジョブが開始されたことを確認します。

* タスクが完了すると、ジョブは、実行されたアクションの詳細を含む別のコメントで応答します。
   * ジョブによって行われるコンテンツ更新は非破壊的です。つまり、プレビューインスタンスに行われます。
   * コメントには更新へのリンクが含まれているため、必要に応じてレビューして公開したり、責任を負う人にJiraを割り当てたりすることができます。

* 次の図は、コンテンツ更新ジョブの`process` コマンドをトリガーするJiraの例を示しています。

  ![Brand Experience Agentのコンテンツ更新ジョブを使用したJiraの例](assets/content-update-jira-example.png)

## オーサリングのさらなる改善 {#further-refinement-in-authoring}

AEMでページを編集することを選択すると、オーサリング環境でページが開きます（例：[&#x200B; ユニバーサルエディター](/help/sites-cloud/authoring/universal-editor/authoring.md)や[&#x200B; ページエディター](/help/sites-cloud/authoring/page-editor/introduction.md)）。

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

## その他のリソース {#additional-resources}

Experience Production Agentを引き続き検討する場合は、次のリソースが役立つ可能性があります。

* [Experience Production Agent Workbook](https://www.adobe.com/go/aem-epa-workbook)をガイド付きの実践的な手順に使用することもできます。
