---
title: Forms Experience Builder
description: フォームフラグメントを使用した強力なフォームの迅速な作成
feature: Edge Delivery Services
hide: true
index: false
hidefromtoc: true
role: Admin, Developer
exl-id: 183e999c-9896-49a2-b29b-7c77da380df9
source-git-commit: 1d378e6c8ac714779e77314d3457a14d40cd222f
workflow-type: tm+mt
source-wordcount: '590'
ht-degree: 32%

---

# 概要

AEM Forms Experience Builder は、生成 AI を活用して、自然言語によるデジタルフォームの作成を高速化します。 この強力なツールにより、技術ユーザーと技術者以外のユーザーの両方がシンプルで対話型のインターフェイスを使用して、プロフェッショナルグレードのフォームを設計、変更、最適化できます。

Forms Experience Builder を使用すると、会話型 AI によって迅速にフォームを作成でき、技術者以外のユーザーがコーディングに関する知識を持たずに高度なフォームを作成できるようになります。 複雑なレイアウトの設計、検証ルールの実装、送信アクションの設定を簡単な対話型コマンドで行うことができます。

## コア機能

Forms Experience Builder には、強力なデジタルフォームを作成するための次の 2 つの主なワークフローが用意されています。

### AI を活用したフォームの作成

**自然言語フォーム生成**

わかりやすい英語の説明を使用して、完全なフォームをゼロから作成します。「評価スケールとコメントフィールドを備えた顧客フィードバックフォームを作成」などの要件を記述するだけで、Forms Experience Builder により、適切なフォーム構造が生成されます。ビジュアルエディターの Experience Builder を使用して、フィールド、検証ルール、送信ロジックを追加します。

**Dynamic Tag Management**

対話型コマンドを使用してフォームフィールドを追加、変更または削除します。AI はコンテキストを理解し、要件に基づいてフィールドタイプ、検証ルール、ユーザーインターフェイスの改善をインテリジェントに提案できます。

**レイアウト最適化**

自然言語を通じてフォームのレイアウトと設定を更新します。「フォームレイアウトをウィザードレイアウトに変更」などの変更をリクエストすると、Forms Experience Builder により、適切なスタイルとレイアウトの調整が適用されます。

### インテリジェントなインポートと変換

既存のドキュメントをインタラクティブなデジタルエクスペリエンスに変換します。 Forms Experience Builder は、様々な形式をサポートしており、アップロードされたコンテンツを分析してフィールドタイプを検出し、レイアウトを保持し、レスポンシブデザインと高度なロジックを使用してフォームを強化します。 次の形式がサポートされています。

- **Acroforms**：既存のフィールド構造を備えたインタラクティブな PDF フォーム
- **XFA PDF**：複雑な XML ベースのフォームアーキテクチャ
- **フラット PDF**：インタラクティブなフォームに変換した静的ドキュメント
- **画像とスクリーンショット**:JPG、PNG 形式
- **手描きフォーム**：スケッチと紙のフォームの写真


## Forms Experience Builder デモ {#forms-experience-builder-demo}

>[!VIDEO](https://video.tv.adobe.com/v/3463164/)

## オンボーディングと前提条件

Forms Experience Builder は現在、早期アクセスプログラムを通じて利用できます。 アクセスを要求するには、公式メール ID から [aem-forms-ea@adobe.com](mailto:aem-forms-ea@adobe.com) にメールを送信します。

Experience Builder を使用するには、[&#x200B; アダプティブ Forms コアコンポーネント &#x200B;](/help/forms/enable-adaptive-forms-core-components.md) を備えたAEM Forms as a Cloud Service実稼動オーサー環境が必要です。

## Forms Experience Builder へのアクセス


1. **AEM/Forms/Formsとドキュメント** に移動します。
1. 「**作成**」をクリックし、「**アダプティブフォーム**」を選択します。
1. ウィザードを使用して、要件に応じて [&#x200B; コアコンポーネントテンプレート &#x200B;](/help/forms/creating-adaptive-form-core-components.md) または [Edge Delivery Services](/help/edge/docs/forms/universal-editor/create-forms.md) テンプレートを使用して新しいフォームを作成し、フォームを編集用に開きます。
1. エディターのツールバーにある **Forms Experience Builder** アイコンをクリックして、Forms Experience Builder インターフェイスを開き、自然言語を使用してフォームを作成します。


| ![&#x200B; アダプティブ Forms エディター – Forms Experience Builder](/help/edge/docs/forms/assets/adaptive-forms-editor.gif " アダプティブ Forms エディター – Forms Experience Builder") | ![&#x200B; ユニバーサルエディター – Forms Experience Builder](/help/forms/assets/ue-forms-experience-builder.gif " ユニバーサルエディター – Forms Experience Builder") |
|:-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------:|:--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------:|
| *アダプティブフォームエディター* | *ユニバーサルエディター* |

<!-- >

## Learn more on key capabilities {#key-capabilities-forms-experience-builder}

<table>
<td>
   <a href="/help/forms/experience-builder/forms-experience-builder-getting-started.md">
   <img alt="Getting started with Forms Experience Builder" src="./assets/getting-started.png" />
   </a>
   <div>
      <a href="/help/forms/experience-builder/forms-experience-builder-getting-started.md">
      <strong>Getting started with Forms Experience Builder</strong>
      </a>
   </div>
   <p>
      <em>Learn the basics of creating your first form using AI-powered capabilities.</em>
   </p>
</td>

<td>
   <a href="/help/forms/experience-builder/forms-experience-builder-llm-smart-fields.md">
   <img alt="LLM-enhanced smart fields" src="./assets/llm-smart-fields.png" />
   </a>
   <div>
      <a href="/help/forms/experience-builder/forms-experience-builder-llm-smart-fields.md">
      <strong>LLM-enhanced smart fields</strong>
      </a>
   </div>
   <p>
      <em>Learn how to create fields with pre-populated options using AI knowledge base.</em>
   </p>
</td>

<td>
   <a href="/help/forms/experience-builder/forms-experience-builder-prompt-examples-library.md">
   <img alt="AI-powered form creation" src="./assets/ai-form-creation.png" />
   </a>
   <div>
      <a href="/help/forms/experience-builder/forms-experience-builder-prompt-examples-library.md">
      <strong>AI-powered form creation</strong>
      </a>
   </div>
   <p>
      <em>Learn how to utilize natural language to create and modify forms.</em>
   </p>
</td>
</table>

<table>
<td>
   <a href="/help/forms/experience-builder/intelligent-import-conversion.md">
   <img alt="Intelligent import and conversion" src="./assets/intelligent-import.png" />
   </a>
   <div>
      <a href="/help/forms/experience-builder/intelligent-import-conversion.md">
      <strong>Intelligent import and conversion</strong>
      </a>
   </div>
   <p>
      <em>Learn how to transform existing documents into interactive digital forms</em>
   </p>
</td>

<td>
   <a href="/help/forms/experience-builder/form-submission-integration.md">
   <img alt="Form submission and integration" src="./assets/form-submission.png" />
   </a>
   <div>
      <a href="/help/forms/experience-builder/form-submission-integration.md">
      <strong>Form submission and integration</strong>
      </a>
   </div>
   <p>
      <em>Learn how to configure form submissions to integrate with your business systems.</em>
   </p>
</td>

<td>
   <a href="/help/forms/experience-builder/forms-experience-builder-frequently-asked-questions.md">
   <img alt="Forms Experience Builder frequently asked questions" src="./assets/faq-banner.jpg" />
   </a>
   <div>
      <a href="/help/forms/experience-builder/forms-experience-builder-frequently-asked-questions.md">
      <strong>Frequently asked questions</strong>
      </a>
   </div>
   <p>
      <em>Get responses to common questions about Forms Experience Builder capabilities and usage.</em>
   </p>
</td>
</table> -->



<!--
**Comprehensive Submit Action Configuration**

Configure form submissions to integrate with your existing business systems:

- **Email Integration**: Set up automated email notifications and confirmations
- **REST API Endpoints**: Connect to custom applications and services
- **Cloud Storage**: Integrate with Azure Blob Storage, SharePoint, and OneDrive
- **Workflow Automation**: Connect to Power Automate and Workfront Fusion
- **Marketing Platforms**: Direct integration with Marketo for lead management
- **AEM Workflows**: Leverage existing AEM workflow capabilities
-->


## 探索の開始

Forms Experience Builder の調査を開始する方法を以下に示します。

- **フォームを増分的に作成**：シンプルなフォームから開始して、複雑さを順を追って追加します。 例えば、基本的な連絡先フォームを作成し、検証ルール、プレースホルダーテキスト、条件付きロジックを追加します。 [詳細情報](/help/forms/experience-builder/forms-experience-builder-prompt-examples-library.md#incremental-development-examples)。

- **スマートフィールドの作成**:AI の知識を活用して、すべての国、主要空港、業界標準の役職のドロップダウンリストなど、事前入力されたコンテキストに対応するオプションを含むフィールドを作成します。 [詳細情報](/help/forms/experience-builder/forms-experience-builder-prompt-examples-library.md#llm-enhanced-smart-fields)。

- **複雑なビジネスロジックの実装**：ユーザー入力に基づいてフォームセクションを表示または非表示にする条件付きルールを定義します。 例えば、ユーザーの婚姻ステータスが「既婚」の場合にのみ「配偶者情報」セクションを表示するルールを作成します。 [詳細情報](/help/forms/experience-builder/forms-experience-builder-prompt-examples-library.md#rule-creation--business-logic)。

- **システムとの統合**:REST API へのデータの送信、CRM での新しいリードの作成、クラウドストレージへのドキュメントの保存など、既存のビジネスワークフローに接続するフォーム送信を設定します。 [詳細情報](/help/forms/experience-builder/forms-experience-builder-prompt-examples-library.md#data-integration--submission)。

<!-- ## Onboarding

The Forms Experience Builder is currently available through an Early Access Program. To request access, follow these steps:

1. **Gather your information**: You will need the following details:
    - IMS Organization ID
    - Program ID
    - Project Details (timeline, scope, use cases)
    - Your Official Work Email

   If you need help finding your IMS Organization ID and Program ID, refer to the [Adobe Experience Cloud Organization Setup Guide](/help/onboarding/cloud-manager-introduction.md) and the [Program and Environment Management](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/program-types.md) documentation.

2. **Send an access request**: Email [aem-forms-ea@adobe.com](mailto:aem-forms-ea@adobe.com) with all the information gathered in the previous step. 

    Access to the Forms Experience Builder is limited and subject to approval based on program capacity and alignment with early access criteria. 

## Getting started

To get started with the Forms Experience Builder, visit the [Forms Experience Builder documentation](/help/forms/experience-builder/forms-experience-builder-getting-started.md).

-->
