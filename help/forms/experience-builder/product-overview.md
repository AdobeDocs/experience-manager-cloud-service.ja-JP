---
title: Forms Experience Builder
description: フォームフラグメントを使用した強力なフォームの迅速な作成
feature: Edge Delivery Services
hide: true
index: false
role: Admin, Developer
badgeSaas: label="AEM Forms" type="Positive" tooltip="AEM Formsに適用）。"
exl-id: 183e999c-9896-49a2-b29b-7c77da380df9
source-git-commit: 95e2216ee79433783da384134243f3688ff7797d
workflow-type: tm+mt
source-wordcount: '581'
ht-degree: 33%

---

# 概要

AEM Forms Experience Builderでは、生成AIを利用して、自然言語によるデジタルフォームの作成を高速化できます。 この強力なツールは、技術的な知識を問わず、誰もがシンプルな対話型インターフェイスを使用して、プロフェッショナルグレードのフォームをデザイン、変更、最適化できるようにします。

Forms Experience Builderなら、会話型AIを利用して、フォームを迅速に作成できます。技術的な知識を備えていない担当者でも、コーディングに関する知識がなくても高度なフォームを作成できます。 複雑なレイアウトのデザイン、検証ルールの実装、送信アクションの設定などを、シンプルな対話型コマンドを使用して実行できます。

## 主な能力

Forms Experience Builder には、強力なデジタルフォームを作成するための次の 2 つの主なワークフローが用意されています。

### AIを活用したフォーム作成

**自然言語フォーム生成**

わかりやすい英語の説明を使用して、完全なフォームをゼロから作成します。 「評価スケールとコメントフィールドを備えた顧客フィードバックフォームを作成」などの要件を記述するだけで、Forms Experience Builder により、適切なフォーム構造が生成されます。 ビジュアルエディターの Experience Builder を使用して、フィールド、検証ルール、送信ロジックを追加します。

**Dynamic Tag Management**

対話型コマンドを使用してフォームフィールドを追加、変更または削除します。 AI はコンテキストを理解し、要件に基づいてフィールドタイプ、検証ルール、ユーザーインターフェイスの改善をインテリジェントに提案できます。

**レイアウト最適化**

自然言語を通じてフォームのレイアウトと設定を更新します。 「フォームレイアウトをウィザードレイアウトに変更」などの変更をリクエストすると、Forms Experience Builder により、適切なスタイルとレイアウトの調整が適用されます。

### インテリジェントな読み込みと変換

既存のドキュメントをインタラクティブなデジタルエクスペリエンスに変換。 Forms Experience Builderは、様々なフォーマットをサポートしています。アップロードされたコンテンツを分析して、フィールドタイプを検出し、レイアウトを保持し、レスポンシブデザインと高度なロジックを使用してフォームを強化します。 サポートされる形式は次のとおりです。

- **Acroforms**：既存のフィールド構造を備えたインタラクティブな PDF フォーム
- **XFA PDF**：複雑な XML ベースのフォームアーキテクチャ
- **フラット PDF**：インタラクティブなフォームに変換した静的ドキュメント
- **画像とスクリーンショット**:JPG、PNG形式
- **手描きフォーム**：スケッチと紙のフォームの写真


## Forms Experience Builder デモ {#forms-experience-builder-demo}

>[!VIDEO](https://video.tv.adobe.com/v/3463164/)

## オンボーディングと前提条件

Experience Builderには、[ アダプティブなAEM Forms コアコンポーネント ](/help/forms/enable-adaptive-forms-core-components.md)を備えたForms as a Cloud Serviceの本番環境が必要です。

## Forms Experience Builder へのアクセス


1. **AEM/Forms/Formsとドキュメント**&#x200B;に移動します。
1. **作成**&#x200B;をクリックし、**アダプティブフォーム**&#x200B;を選択します
1. 必要に応じて、[ コアコンポーネントテンプレート ](/help/forms/creating-adaptive-form-core-components.md)または[Edge Delivery Services](/help/edge/docs/forms/universal-editor/create-forms.md) テンプレートを使用して新しいフォームを作成し、フォームを開いて編集します。
1. エディターのツールバーで&#x200B;**Forms Experience Builder** アイコンを選択して、Forms Experience Builder インターフェイスを開き、自然言語を使用してフォームを作成します。


| ![ アダプティブ Forms エディター – Forms Experience Builder](/help/edge/docs/forms/assets/adaptive-forms-editor.gif " アダプティブ Forms エディター – Forms Experience Builder") | ![ ユニバーサルエディター – Forms Experience Builder](/help/forms/assets/ue-forms-experience-builder.gif " ユニバーサルエディター – Forms Experience Builder") |
|:-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------:|:--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------:|
| *アダプティブフォームエディター* | *ユニバーサルエディター* |

<!--
 >

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
</table>
-->



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

ここでは、Forms Experience Builderの活用方法をいくつか紹介します。

- **フォームを段階的に作成**：単純なフォームから開始し、ステップバイステップで複雑さを追加します。 たとえば、基本的な問い合わせフォームを作成し、検証ルール、プレースホルダーテキスト、条件ロジックを追加します。 [詳細情報](/help/forms/experience-builder/forms-experience-builder-prompt-examples-library.md#incremental-development-examples)。

- **スマートフィールドの作成**: AIの知識を活用して、すべての国、主要空港、業界標準の役職のドロップダウンリストなど、事前入力されたコンテキストに応じたオプションを使用してフィールドを作成します。 [詳細情報](/help/forms/experience-builder/forms-experience-builder-prompt-examples-library.md#llm-enhanced-smart-fields)。

- **複雑なビジネスロジックを実装**: ユーザーの入力に基づいて、フォームセクションの表示と非表示を切り替える条件付きルールを定義します。 例えば、ユーザーの婚姻状況が「既婚」の場合にのみ「配偶者の情報」セクションを表示するルールを作成します。 [詳細情報](/help/forms/experience-builder/forms-experience-builder-prompt-examples-library.md#rule-creation--business-logic)。

- **システムとの統合**: REST APIへのデータの送信、CRMでの新しいリードの作成、クラウドストレージへのドキュメントの保存など、既存のビジネスワークフローに接続するようにフォーム送信を設定します。 [詳細情報](/help/forms/experience-builder/forms-experience-builder-prompt-examples-library.md#data-integration--submission)。

<!--
 ## Onboarding

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
