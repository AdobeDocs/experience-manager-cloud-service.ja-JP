---
title: フォーム作成ジョブ
description: Brand Experience Agent のフォーム作成ジョブと、自然言語を使用してゼロからフォームを作成する方法について説明します。
feature: Edge Delivery Services, Agentic AI
role: User, Admin, Architect, Developer
exl-id: 24ad5f36-405b-4ea2-9819-de6aea856a7a
source-git-commit: baf12e49dadc7b25f5169279a52d5712380445de
workflow-type: tm+mt
source-wordcount: '508'
ht-degree: 0%

---


# フォーム作成ジョブ {#form-creation-job}

フォーム作成ジョブは、自然言語プロンプトを使用してフォームを開発するように設計された [Experience Production Agent](/help/ai-in-aem/agents/brand-experience/experience-production/overview.md) の一部です。 このジョブは、適切なフォーム構造とフィールドタイプを自動的に生成します。 AI アシスタントを使用してジョブを表示します。

フォーム作成ジョブの主なメリットには、次のようなものがあります。

* **フォーム開発の高速化**：シンプルな自然言語コマンドを使用してフォームを迅速に作成し、従来の製品インターフェイスを学習する必要がなくなります。
* **一貫したオンブランドエクスペリエンス**：承認済みのテンプレートとスタイルを使用して、組織のブランディング、テンプレート、スタイルガイドラインに従ったフォームを作成します。
* **技術的な障壁の軽減**：ビジネスユーザーは、高度な技術や深い製品の専門知識がなくても、簡単にフォームを作成できます。

## 機能 {#capabilities}

* **プレーンテキストプロンプトを使用した新しいフォームの作成**：要件をプレーン言語で送信することで、フォームを作成できます。 スキルは、自然言語の説明と指定したテンプレートに基づいて、適切なフォーム構造、フィールドタイプ、オンブランドのエクスペリエンスを自動的に生成します。 この機能により、ブランドとコンプライアンスの標準を維持しながら、フォームの作成を高速化できます。

* **PDF ドキュメントを読み込んでフォームに変換**：既存のPDF ドキュメントを読み込んでフォームに変換できます。 このスキルは、アップロードされたコンテンツを分析して、ブランドとコンプライアンスの標準を維持しながら、フィールドタイプを検出し、レイアウトを保持し、レスポンシブデザインと検証ロジックでフォームを強化します。

これらの機能のいずれかを使用すると、作成するフォームのタイプを選択するように求められます。 コアコンポーネントベースのアダプティブフォームテンプレートまたはEdge Delivery Servicesベースのアダプティブフォームテンプレートのいずれかを指定し、フォームを保存する希望のパスを指定します。 Edge Delivery Servicesに基づいてフォームを作成する場合は、リポジトリの GitHub URL を指定することもできます。


### サンプルプロンプト {#sample-prompts}

* *名前、メール、メッセージの各フィールドを使用して、フィードバック収集用のフォームを作成する*
* *製品評価（1 ～ 5 つ星マーク）、コメントフィールド、オプションのメールを含む、顧客フィードバックフォームを作成します*
* *名前、メール、件名のドロップダウン、メッセージフィールドを含んだ連絡先フォームを作成する*
* *個人情報、アカウント設定、条件への同意を含む登録フォームの作成*
* *`https://[aem-author-url]/path/to/pdf/file`* で入手可能なPDF ファイルを読み込んで、クレジットカード申請フォームを作成します。
* *`https://github.com/wkndforms/wesecure`* のボイラープレートを使用したフィードバックフォームの作成

## フォームを調整 {#refine-with-forms-experience-builder}

AI アシスタントを使用して初期フォーム構造を作成した後、Forms Experience Builder を使用して以下を行うことができます。

* **フォームの更新**：必要に応じて、ビジュアルエディターを使用して、フィールドの追加や変更、フィールドタイプの調整、スタイル設定の更新を行います。

* **レイアウトの更新**：セクション、グループ、フィールドの配置を変更したり、間隔を調整したり、視覚的な階層を変更して操作性を高めたり、フォームがオーディエンスにとって明確で直感的なものになるようにします。

* **ビジネスロジックの追加**：条件付きロジックの作成、ルールの表示/非表示、フィールドの依存関係、検証ルールの定義をおこないます。

* **送信を設定**：メール通知、ワークフローとの統合、外部システムへの接続の設定など、フォームデータが送信される場所を設定します。

詳しくは、[Forms Experience Builder ドキュメントを参照してください。](/help/forms/experience-builder/product-overview.md)

## アクティベーション {#activation}

[ プレイグラウンド ](https://www.aem.live/developer/aem-playground) を通じてAEM エージェントを参照したり、CSM や TAM と連携して Agentic SKU 経由でのアクセスについて話し合ったりできます。

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
