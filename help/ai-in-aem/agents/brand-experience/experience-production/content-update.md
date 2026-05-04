---
title: コンテンツ更新ジョブ
description: Brand Experience Agentのコンテンツ更新ジョブとは何か、およびそれがユーザーに対して何ができるかを説明します。
feature: Edge Delivery Services, Agentic AI
role: User, Admin, Developer
exl-id: e2d1dae8-38de-4357-bb14-ad35acb71aee
source-git-commit: d9e892bd0f43fd32ef6c9e614273993baff2571e
workflow-type: tm+mt
source-wordcount: '866'
ht-degree: 1%

---


# コンテンツ更新ジョブ {#content-update}

[Experience Production Agent](/help/ai-in-aem/agents/brand-experience/experience-production/overview.md)のコンテンツ更新ジョブは、Adobe Experience Manager（AEM）as a Cloud ServiceとEdge Delivery Servicesの日常的な作業を高速化するために、コンテンツ制作を自動化します。

## 概要 {#overview}

コンテンツ更新ジョブは、コンテンツフラグメント、ページ、フォーム、アセットなどの既存のコンテンツを更新します。 コンテンツ要素の更新、削除、置換、追加などのアクションを実行し、エクスペリエンスを正確かつ最新の状態に保つことができます。 入力は自然言語の説明にすることができ、Jira PDFやスクリーンショットを使用して使用する場合も入力を提供できます。

コンテンツ更新ジョブは、自然言語またはビジュアルを通じて、ページのコンテンツ更新に提供する詳細を変換します。 更新が必要なページのURLと、更新が必要な内容の詳細を指定すると、エージェントスキルがタスクを完了します。 AEM as a Cloud Serviceで使用すると、ジョブは新しい[launch](/help/sites-cloud/authoring/launches/overview.md)を作成し、適用する前に更新を確認できます。 ドキュメントのオーサリングで使用すると、ジョブは新しい[&#x200B; バージョン &#x200B;](https://experienceleague.adobe.com/ja/docs/experience-manager-learn/sites/document-authoring/how-to/document-versions#)を作成します。

## 機能 {#capabilities}

コンテンツ更新スキルには、次の場所からアクセスできます。

* [AI アシスタント](#ai-assistant)
* [Jira](#jira)

## AI アシスタント {#ai-assistant}

AEMのジョブには、AI アシスタントからアクセスできます。

[`experience.adobe.com`,](https://experience.adobe.com)のAI アシスタントを開き、`Ask AI Assistant anything` フィールドを使用して自然言語でプロンプトを指定して、やり取りを開始します。

![&#x200B; コンテンツ更新ジョブ &#x200B;](/help/ai-in-aem/agents/brand-experience/experience-production/assets/content-update-ai-assistant-example.png)

### 公開URLの設定 {#configuring-the-publish-url}

公開（公開） URLを使用するには、1回限りの設定を行う必要があります。

* 前提条件：

   * 設定を行うには、ユーザーにシステム管理者権限または製品管理者権限が必要です。

* 構成：

   1. URLのコンテンツ更新をリクエストして、コンテンツ更新スキルを呼び出します。
   1. アシスタントが、いくつかの質問をすることによって、設定を順を追って説明します。
   1. 公開URLが設定され、使用できるようになります。

次に例を示します。

![&#x200B; コンテンツ更新スキル – 公開URLの設定](/help/ai-in-aem/agents/brand-experience/experience-production/assets/content-update-publish-url-configuration.png)

### プロンプト {#prompts}

コンテンツの更新を開始するには、幅広い自然言語プロンプトを使用できます。 更新するページの公開（公開） URL、またはオーサー環境URLを指定する必要があります。 サポートされている動詞の一部は、置換、更新、削除、変更、修正、調整、削除です。

>[!NOTE]
>
>ファイルのアップロードは、[Jira](#jira)を使用してやり取りする場合に使用できますが、AI アシスタントではサポートされていません。

### サンプルプロンプト {#sample-prompts}

プロンプトの例には、次のようなものがあります。

* `<your-publish-URL>`の更新時に、「完璧なコーヒーは4つの質問です！」と表示されます。 “ Your coffee, your way!” 「あなたのコーヒー、あなたの道」
* `<your-author-env-URL>`で画像を「holdingcup.png」から「stairhead.png」に置き換えます
* `<your-publish-URL>`の「コーヒークイズを開始」ボタンをより魅力的なバージョンに変更する
* `<your-author-env-URL>`で、「未請求の特典はギフトです！」のセクションを削除します。

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

## アクティベーション {#activation}

[Playground](https://www.aem.live/developer/aem-playground)からAEM Agentsを検索するか、CSMまたはTAMに接続して、Agentic SKU経由でのアクセスについて話し合うことができます。

## 制限事項 {#limitations}

次の制限事項に注意してください。

* ファイルのアップロードは、[Jira](#jira)とのやり取りには使用できますが、[AI アシスタントとのやり取りにはサポートされません。](#ai-assistant)

## その他のリソース {#additional-resources}

Experience Production Agentを引き続き検討する場合は、次のリソースが役立つ可能性があります。

* [Experience Production Agent Workbook](https://main--summit-labs--aemsites.aem.page/brand-visibility/l339/)をガイド付きの実践的な手順に使用することもできます。
