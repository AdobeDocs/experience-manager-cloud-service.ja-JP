---
title: フォーム作成ジョブ
description: Brand Experience Agentのフォーム作成ジョブと、自然言語を使用してゼロからフォームを作成する方法について説明します。
feature: Edge Delivery Services, Agentic AI
role: User, Admin, Developer
exl-id: 24ad5f36-405b-4ea2-9819-de6aea856a7a
source-git-commit: 81f85045212ca6fd92f2b665aeceaa0d4b92318c
workflow-type: tm+mt
source-wordcount: '508'
ht-degree: 0%

---


# フォーム作成ジョブ {#form-creation-job}

フォーム作成ジョブは、[Experience Production Agent](/help/ai-in-aem/agents/brand-experience/experience-production/overview.md)の一部であり、自然言語プロンプトを使用してフォームを開発するように設計されています。 このジョブは、適切なフォーム構造とフィールドタイプを自動的に生成します。 このジョブはAI アシスタントを通じて表示されます。

フォーム作成ジョブの主な利点は次のとおりです。

* **フォーム開発の高速化**：簡単な自然言語コマンドを使用してフォームをすばやく作成できるため、従来の製品インターフェイスを習得する必要がありません。
* **一貫性のあるブランドに即したエクスペリエンス**：承認済みのテンプレートとスタイルを使用して、組織のブランディング、テンプレート、スタイルガイドラインに従ったフォームを作成します。
* **技術的な障壁の軽減**：ビジネスユーザーは、高度な技術的または深い製品の専門知識を必要とせずに、簡単にフォームを作成できます。

## 機能 {#capabilities}

* **プレーンテキストプロンプトを使用して新しいフォームを作成する**：要件をプレーン言語で送信することで、フォームを作成できます。 このスキルは、自然言語の説明と指定されたテンプレートにもとづいて、適切なフォーム構造、フィールドタイプ、ブランドに即したエクスペリエンスを自動的に生成します。 この機能により、ブランドとコンプライアンス基準を維持しながら、フォームの作成を加速できます。

* **PDF ドキュメントを読み込んでフォームに変換**：既存のPDF ドキュメントを読み込んでフォームに変換できます。 このスキルは、アップロードされたコンテンツを分析し、ブランドとコンプライアンス基準を維持しながら、フィールドタイプの検出、レイアウトの保存、レスポンシブデザインと検証ロジックの強化を行います。

これらの機能のいずれかを使用すると、作成するフォームのタイプを選択するように求められます。 コアコンポーネントベースのアダプティブフォームテンプレートまたはEdge Delivery Services ベースのアダプティブフォームテンプレートのいずれかを指定し、フォームを保存する任意のパスを指定します。 Edge Delivery Servicesに基づいてフォームを作成する場合は、リポジトリのGitHub URLを指定することもできます。


### サンプルプロンプト {#sample-prompts}

* *名前、電子メール、メッセージのフィールドを含むフィードバック収集用のフォームを作成する*
* *製品の評価（1 ～ 5つ星）、コメントフィールド、オプションの電子メールを含む顧客フィードバックフォームを作成*
* *名前、電子メール、件名ドロップダウン、メッセージフィールドを使用して連絡先フォームを作成する*
* *個人情報、アカウントの環境設定、利用規約の同意を含む登録フォームを作成*
* *`https://[aem-author-url]/path/to/pdf/file`*&#x200B;で利用可能なPDF ファイルを読み込んで、クレジットカード申請フォームを作成する
* *`https://github.com/wkndforms/wesecure`*&#x200B;のボイラープレートを使用してフィードバックフォームを作成する

## フォームを調整 {#refine-with-forms-experience-builder}

AI アシスタントを使用して最初のフォーム構造を作成した後、Forms Experience Builderを使用して次のことを実行できます。

* **フォームを更新**：ビジュアルエディターを使用して、必要に応じてフィールドを追加または変更したり、フィールドタイプを調整したり、スタイルを更新したりします。

* **レイアウトを更新**：セクション、グループ、フィールドの並べ替え、間隔の調整、視覚的な階層の変更を行って、使いやすさを向上させ、オーディエンスに対してフォームが明確で直感的なものであることを確認します。

* **ビジネスロジックを追加**：条件付きロジックの作成、ルールの表示/非表示、フィールドの依存関係、検証ルールの定義を行います。

* **送信を設定**：電子メール通知の設定、ワークフローとの統合、外部システムへの接続など、フォームデータの送信先を設定します。

詳しくは、[Forms Experience Builder ドキュメントを参照してください。](/help/forms/experience-builder/product-overview.md)

## アクティベーション {#activation}

[Playground](https://www.aem.live/developer/aem-playground)からAEM Agentsを検索するか、CSMまたはTAMに接続して、Agentic SKU経由でのアクセスについて話し合うことができます。

<!-- 
#### Import and convert {#import-and-convert}

Transform existing documents into interactive digital forms. The agent analyzes uploaded content to detect field types, preserve layouts, and enhance forms with responsive design and validation logic. Supported formats include Acroforms, XFA PDFs, flat PDFs, images (JPG, PNG), and hand-drawn form photographs.

>[!VIDEO](https://video.tv.adobe.com/v/3474042)

**Prompt examples:**

* *Convert the attached PDF file to an adaptive form*
* *Transform this scanned form image into an interactive digital form*
* *Import the employee onboarding PDF and create an editable form*
* *Convert this paper form photograph into a digital form with validation*
-->

<!-- 
### Embed an existing form to a sites page {#embed-existing-form}

The form creation skill enables seamless integration of existing forms into any sites page through natural language commands. Rather than manually locating, copying, and embedding form components, users can simply specify which form to add and where to place it. The agent handles the technical implementation, ensuring proper rendering and functionality.

>[!VIDEO](https://video.tv.adobe.com/v/PLACEHOLDER)

**Prompt examples:**

* *Embed the contact form to the homepage*
* *Add the existing customer feedback form to the support page*
* *Insert the newsletter signup form into the footer section*
* *Place the registration form on /content/site/signup*
* *Add form "contact-us-2024" to the current page*
-->

<!-- 
### Build and add a form to an existing sites page {#build-and-add-form}

The form creation skill combines form creation and site integration in a single conversational workflow. Users can describe the form they need and specify where to add it, and the agent creates the form and embeds it into the specified page automatically. This eliminates the traditional multi-step process of creating a form separately and then manually adding it to a page.

>[!VIDEO](https://video.tv.adobe.com/v/PLACEHOLDER)

**Prompt examples:**

* *Create a newsletter signup form with email field and add it to the footer*
* *Build a quick contact form with name, email, and message, then add it to /content/about-us*
* *Add a feedback form with rating stars and comment field to this page*
* *Create a simple survey form with 5 questions and embed it on the customer portal homepage*
* *Build an event registration form with name, email, and date selection, then add it to /content/events/conference-2025*
-->
