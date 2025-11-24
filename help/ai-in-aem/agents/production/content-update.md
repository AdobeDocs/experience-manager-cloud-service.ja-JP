---
title: Content Update Skill
description: Experience Production Agent のコンテンツ更新スキルの概要と機能について説明します。
feature: Edge Delivery Services, Agentic AI
role: User, Admin, Architect, Developer
source-git-commit: 8cd524891df550913a734a9355c1012dc11adf5b
workflow-type: tm+mt
source-wordcount: '860'
ht-degree: 1%

---


# Content Update Skill {#content-update}

Experience Production Agent のコンテンツ更新スキルは、コンテンツ作成を自動化して、Adobe Experience Manager（AEM）as a Cloud ServiceおよびEdge Delivery Servicesの日常的なタスクを高速化します。

コンテンツ更新スキルは、コンテンツフラグメント、ページ、フォーム、アセットなど、CMS全体の既存のコンテンツを更新します。 エージェントは、コンテンツ要素の更新、削除、置換、追加などのアクションを実行して、エクスペリエンスを正確かつ最新の状態に保つことができます。 入力は自然言語による説明にすることができます。Jira PDF やスクリーンショットで使用する場合は、入力も指定できます。

## 概要 {#overview}

コンテンツ更新スキルは、提供した詳細を、自然言語やビジュアルのいずれかで、ページ上のコンテンツの更新に変換します。 更新が必要なページの URL と更新が必要な内容の詳細を指定します。エージェントのスキルがタスクを完了します。

## 機能 {#capabilities}

コンテンツ更新スキルには、次の場所からアクセスできます。

* [AI アシスタント](#ai-assistant)

* [Jira](#jira)

## AI アシスタント {#ai-assistant}

AI アシスタントを介してAEM Business Agents にアクセスできます。

experience.adobe.comから AI アシスタントを開き、`Ask AI Assistant anything` フィールドを使用して自然言語でプロンプトを指定して、操作を開始します。

![ アクセス探索エージェント ](/help/ai-in-aem/agents/production/assets/content-update-ai-assistant-example.png)

### サンプルプロンプト {#sample-prompts}

コンテンツの更新を開始するには、様々な自然言語のプロンプトを指定します。 また、更新するページの公開 URL を指定する必要があります。 例：

* 次のページを変更します。https://www.your-url.com/sale メインヒーローの見出しを「ブラックフライデーメガセール – 最大 70% オフ」に更新し、カウントダウンタイマーを「48 時間以内に終了」に変更し、「更新にサインアップ」を削除し、すべての「今すぐ購入」ボタンを「取引をつかむ」に変更します

* https://www.your-url.com/laptops/your-laptop-model バナーコピーを「今すぐ 300 USD 節約」に更新し、価格を 1,299 USD から 999 USD に更新し、融資オプションバナーを削除します

* https://www.your-url.com/your-sneaker在庫ステータスを「低在庫」から「在庫に戻る – 数量限定」に更新、サイズセレクターを変更して使用可能なサイズを緑色でハイライト、「近日公開予定」バッジを削除

* https://www.your-url.com/your-sneaker新しいカラーウェイを表示するように製品画像を更新します

>[!NOTE]
>
>ファイルのアップロードは、[Jira](#jira) を使用してやり取りする際に使用できますが、AI アシスタントではサポートされていません。

## Jira {#jira}

Jira でコンテンツ更新スキルを使用すると、編集を自動化する手順を記載したチケットを作成できます。

### チケットの作成 {#create-a-ticket}

（あらゆるタイプの） Jira チケットを作成します。

チケットの **説明** フィールドには、次の 2 つの重要な詳細が必要です。

1. 編集する必要があるページの公開 URL。

1. 必要な変更。

   現在、スキルは、変更を説明するために次の様々な形式をサポートしています。

   * チケットの説明に含まれる自然言語
      * 例：「ヘッドラインを X から Y に変更」
   * 注釈付きPDFが添付されている
      * 例えば、ページのPDFを作成し、変更する内容の詳細を示すアノテーションを追加します
   * 添付されたPDFのコメント
      * 例えば、ページのPDFを作成し、変更内容の詳細をコメントを追加します
   * 添付されている注釈付きスクリーンショット
      * 例えば、ページの一部のスクリーンショットを撮り、変更したいことを詳しく説明する注釈を追加します
   * 自然言語の変更を含む、Microsoft Word ファイルが添付されています

### チケットからエージェントを呼び出します {#invoke-the-agent-from-your-ticket}

エージェントを使用するには、チケットにコメントを追加します。 コメントで、エージェントに `@` 記号と、エージェントが実行するコマンドを指定します。次に例を示します。

* `@aemagent@adobe.com process`

現在、エージェントは次のコマンドを認識しています。

* `process` - リクエストを処理
* `cancel` – 処理リクエストのキャンセル
* `retry` - リクエストの再処理
* `feedback` – 以前の世代へのフィードバックの適用
* `reprocess` – 元のリクエストを再処理

### エージェントのやり取り {#how-the-agent-interacts}

エージェントにコマンドを発行すると、Jira でコメントと共に応答します。 コメントには、エージェントの進行状況と実行されたアクションの詳細が表示されます。

トリガーの更新に `process` コマンドを使用する場合、応答は次の順序に従う可能性があります。

* 最初のコメントは、エージェントが開始されたことを確認します。

* タスクが完了したら。 エージェントは、実行されたアクションの詳細を含む別のコメントで応答します。
   * エージェントによるコンテンツの更新は非破壊的です。つまり、プレビューインスタンスに対して行われます。
   * コメントには更新内容へのリンクが含まれているので、必要に応じて確認して公開したり、責任を持つユーザーに Jira を割り当てたりできます。

* 次の画像は、コンテンツ更新スキル用の `process` コマンドをトリガーにする Jira の例を示しています。

  ![ エクスペリエンス実稼働エージェントのコンテンツ更新スキルを使用した Jira の例 ](assets/content-update-jira-example.png)

## アクティベーション {#activation}

Experience Production Agent をアクティブ化してアクセスできるようにするには、Adobeにお問い合わせください。 開始するには、以下にお問い合わせください。

* `experience-production-agent@adobe.com`
* または、アカウントチームにお問い合わせください

プロセスを迅速に実行するには、次の情報を提供すると役立ちます。

* AEM as a Cloud Service用
   * 以下を指定する必要があります。
      * 組織 ID
      * `product_id`
      * `profile_id`

   * これらの値は、次の手順を使用して確認できます。
      * 管理者が <https://adminconsole.adobe.com/> にアクセスする必要があります
      * **Adobe Experience Manager as a Cloud Service** を選択
      * 適切なAEM インスタンスを選択します
      * 対象のコンテンツの読み取りおよび書き込み操作を許可するプロファイルを選択してください
      * ブラウザー URL を取得します
      * URL から `product_id` と `profile_id` を抽出します。
例えば、<https://adminconsole.adobe.com/products/profiles/users> のように指定します。

* Edge Delivery ドキュメントのオーサリング
   * Adobe チームに次の情報を提供します。
      * 関連するドメイン
      * 関連する Github 情報：
         * 組織
         * リポジトリ
         * ブランチ

## 制限事項 {#limitations}

現在、コンテンツアップデーターには次の制限があります。

* ファイルのアップロードは、[Jira](#jira) を操作する際に使用できますが、[AI アシスタント ](#ai-assistant) を操作する際にはサポートされません。
