---
title: AEM の AI アシスタント
description: AI アシスタントを使用して回答を見つけ、Adobe Experience Manager で使用可能なソリューションのトラブルシューティングを行います。
solution: Experience Manager
feature: Authoring, AI Assistant, AI Tools
role: Admin, Developer, User
exl-id: 81e7b1ac-50d0-4547-8622-bf145ebc3dc0
source-git-commit: fa8035f826a4d08c18bc0d2b7664015c6fc82698
workflow-type: tm+mt
source-wordcount: '1280'
ht-degree: 5%

---

# AEM の AI アシスタント {#about-ai-assistant-in-aem}

ADOBE EXPERIENCE MANAGERのAI アシスタント（AEM）は、AEM関連の質問に対する回答を効率的に見つけるように設計された、会話型のインターフェイスを提供します。 この機能を使用すると、AEM製品関連の質問（*すべてのユーザーが利用できます*）、サポートチケットの作成（*サポート管理者が利用できます*）を自動化できます。

AI アシスタントは、次のソリューションを含むAEM as a Cloud Serviceをサポートしています。

* Experience Hubの概要ページ
* Edge Delivery Services
* Sites
* Assets
* Forms
* Dynamic Media
* Cloud Manager


AEM に直接埋め込まれ、AEM Experience Hub、Cloud Manager、オーサー UI からアクセスできます。

次の3分25秒のビデオでは、AEMのAI アシスタントのステップバイステップのチュートリアルを提供します。

>[!VIDEO](https://video.tv.adobe.com/v/3475357/?learn=on&enablevpops)

## AEMのAI アシスタントを利用すれば{#get-access}

AEMのAI アシスタントにアクセスするには、次の要件を満たしている必要があります。

* AEMのAI アシスタントを使用して製品知識を得る権限。 この権限を持つユーザーは、AI アシスタントのチャットで製品関連の質問をすることができます。 この権限を有効にする必要があります。
* サポートチケットを開く権限。これには&#x200B;**サポート管理者**&#x200B;の役割が必要です。

>[!NOTE]
>
>AEMのAI アシスタントのリクエストは、Adobe Identity Managementサービス（IMS）を通じて認証されます。 詳しくは、[Adobe Identity Management サービスの概要](https://www.adobe.com/content/dam/cc/en/trust-center/ungated/whitepapers/corporate/adobe-identity-management-services-security-overview.pdf)を参照してください。

**AEMのAI アシスタントにアクセスするには：**

1. Adobe Experience ManagerのAIを活用したエージェント機能のほとんどにアクセスするには、お客様は追加契約を締結する必要があります。 詳しくは、Adobe担当者にお問い合わせください。

1. AEMでAI アシスタントを使用するには、AI アシスタントを通じて製品情報にアクセスする権限が必要です。 この権限はデフォルトでオンになっています。

   製品情報にアクセスできるユーザーを制御するには、Adobe IDに関連付けられている電子メールアドレスから[aemaiassistant@adobe.com](mailto:aemaiassistant@adobe.com)に電子メールを送信します。 Adobeでは、ユーザーレベルのアクセス制御を有効にできます。 有効にすると、管理者は[AEMのAI アシスタントの設定](/help/implementing/cloud-manager/ai-assistant-in-aem-admin.md)の手順に従って、ユーザーレベルのアクセス権を付与できます。

## 範囲 {#scope}

AEMのAI アシスタントの現在の範囲は、AEM as a Cloud Serviceの製品知識に関する質問への対応に重点を置いています。 このスコープには、主要分野に対する包括的なサポートが含まれます。<!--, such as Sites, Assets, Forms, Edge Delivery Services, Dynamic Media, and Cloud Manager. -->

* **サーフェス**: AEM Experience Hub、オーサーUI、Cloud Manager全体で使用可能です。
* **機能**：トラブルシューティングとガイダンス、サポートチケットの自動作成と参照のための製品知識とファーストストストップ。
* **値**：時間を節約し、学習と価値実現までの時間を短縮し、サポートチケットを手動で作成する必要性を減らし、サポートチケットの作成の効率を向上させます。

## プライバシー、セキュリティ、ガバナンス{#privacy-security-governance}

AEMのAI アシスタントは、プライバシー、セキュリティ、ガバナンスを重視して設計されています。

この記事では、AEMのAI アシスタントが提供する、信頼の向上を重視した機能の概要を説明します。

* AEMのAI アシスタントでは、トレーニング目的を含め、個人データは使用されません。
* AEMのAI アシスタントは、消費者データにアクセスできません。
* AEMのAI アシスタントを利用するには、明示的な権限が必要です。
* ユーザーが提供したプロンプト（質問、クエリなど）は、他の顧客と共有されません。

<!-- See also [Security at Adobe whitepaper](). NEED ACTIVE LINK FROM ADRIAN NICOLAE TANASE. CURRENTLY 404. -->

## AEMのAI アシスタントを利用して、製品ナレッジと自動サポートチケット作成について学ぶ {#ai-prod-insights}

製品知識には、Adobe Experience League ドキュメントから派生した概念とトピックが含まれます。 これらの質問は、次のサブグループに分類できます。


| 製品知識 | すべてのユーザーが利用できます<br>例 |
| :--- | :--- |
| ターゲットを絞った学習 | <ul><li>ユニバーサルエディターとは？</li><li>Cloud Managerでプログラムを作成するにはどうすればよいですか？</li></ul> |
| オープン検出 | <ul><li>ユニバーサルエディターの使用方法を教えてください。</li><li>ある環境から別の環境にコンテンツをコピーする方法はありますか？</li></ul> |
| トラブルシューティング | <ul><li>ユニバーサルエディターにアクセスできないのはなぜですか？</li><li>パイプラインが失敗する理由</li></ul> |
| **チケット作成をサポート** | **サポート管理者のみが利用できます&#x200B;**<br>**例** |
| AI アシスタントのチャット履歴とコンテキストを取得した自動サポートチケット作成 | <ul><li>サポートチケットを作成する。</li></ul> |
| サポートチケットのステータスの取得 | <ul><li>私が開いたサポートチケットをすべて見せてください。</li><li>チケット「E---------- – 」のステータスを表示</li></ul> |

{style="table-layout:auto"}


## 質問を作成する方法 {#ai-craft-questions}

AEMのAI アシスタントから最も正確な回答を得るには、質問を明確かつ文脈に沿って表現することが重要です。 次のヒントを使用して、クエリが明確かつ適切に構造化されていることを確認します。

* タスクや質問を簡潔に明確に伝える。
* あいまいな表現や複雑すぎる構文を避けて、理解を深めましょう。
* AEMのAI アシスタントがより正確で関連性の高い回答を提供するのに役立つため、タスクや質問に関する関連コンテキストを含めることができます。
例えば、プロンプトでは、使用しているAEM ソリューション（Sites、Assets、Dynamic Media、Edge Delivery Services、Cloud Manager、Forms）の名前を付けます。

### サポートされていない質問の例 {#ai-unsupported-questions}

| 領域 | 例 |
| --- | --- |
| 運用上のインサイト | <ul><li>テナントに存在する開発環境の数</li><li>最後の実稼動パイプラインを開始したのは誰ですか？</li></ul> |
| トラブルシューティング | <ul><li>実稼動パイプラインが失敗するのはなぜですか？</li></ul> |
| タスクと自動化 | <ul><li>開発ブランチからコード品質パイプラインを設定します。</li></ul> |


## AEMのAI アシスタントを活用して {#ai-use}

<!--
 UNHIDE AFTER BETA or at GA
### Enable AI Assistant in AEM access through Admin Console 

To use AI Assistant in AEM, your organization must opt in at the Admin Console level. A product administrator creates (or chooses) a user group and grants it the new "AI Assistant" permission. Anyone added to that group instantly gains access to the Assistant across AEM. If the goal is company-wide availability, the admin simply assigns all users to that group.

![AI Assistant in AEM in the Admin Console](/help/implementing/cloud-manager/assets/ai-assistant-admin-console.png)

From an employee's perspective, the process is straightforward: identify the product administrator for Adobe Experience Manager in your organization and request to be added to the AI-enabled user group. Once you appear in that group, the Assistant icon shows up automatically the next time you sign in.

Administrators should keep normal Cloud Manager governance in mind. Hold product administrator rights in the Admin Console to create profiles, manage user groups, or edit permissions. If users also need the Assistant's built-in **Create Support Ticket** feature, add the standard **Support Admin** role (standard Admin Console role) to the same individuals or group.

![Technical support ticket creation in AI Assistant in AEM of the Admin Console](/help/implementing/cloud-manager/assets/ai-assistant-admin-console-support-ticket.png)

For a guided walkthrough of setting up users and groups in AEM as a Cloud Service, see [Configuring access to AEM as a Cloud Service ](https://experienceleague.adobe.com/en/docs/experience-manager-learn/cloud-service/accessing/overview). 

See also [Custom Permissions](/help/implementing/cloud-manager/custom-permissions.md).
-->


### AEMでAI アシスタントを起動する

AEMのAI アシスタントをリセットして、トピックを変更する場合に新しい会話を開始できます。 この機能は、失敗しているクエリや誤った情報を提供しているクエリのトラブルシューティングに特に役立ちます。

**AEMの会話でAI アシスタントを開始するには：**

1. AEM ユーザーインターフェイスの右上隅付近（Cloud Manager ページまたはAEM環境のオーサーインスタンス）で、**AI アシスタント** アイコンをクリックします。

   ![ ツールバーのAI アシスタント アイコン ](/help/implementing/cloud-manager/assets/ai-assistant-icon.png)

1. 下部付近の&#x200B;**AI アシスタント** パネルのテキストボックスに、質問またはプロンプトを入力し、`Enter`を押すか、![送信アイコン ](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Send_18_N.svg)をクリックします。

   >[!NOTE]
   >
   >個人データは入力に含めないでください。このツールを使用する場合は不要です。

   ![AI アシスタントパネルの下部にあるテキストボックス ](/help/implementing/cloud-manager/assets/ai-assistant-prompt-text-box.png)

1. 新しい会話（新しいトピックまたはトピックの変更）を開始するには、![詳細アイコン ](https://spectrum.adobe.com/static/icons/workflow_18/Smock_More_18_N.svg)/**新しい会話を開始**&#x200B;をクリックします。

   ![省略記号アイコンからAI アシスタントで新しい会話を開始](/help/implementing/cloud-manager/assets/ai-assistant-start-new-conversation.png)

### カテゴリー別のプロンプトを見つける

AEMのAI アシスタントには、サポートされているトピックやカテゴリーを調べるのに役立つ見つけやすさ機能が搭載されています。

**カテゴリ別にプロンプトを見つけるには：**

1. AI アシスタントパネルで、![学習アイコン ](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Learn_18_N.svg)をクリックして、プロンプト検出パネルをオンにします。

   ![AI アシスタントのカテゴリ別にプロンプトを検索できるパネル ](/help/implementing/cloud-manager/assets/ai-assistant-discover-prompts.png)
   AI アシスタントのプロンプトカテゴリを表示する&#x200B;*パネル。*

1. カテゴリを選択して、関連するプロンプトのリストを表示します。
1. プロンプトを選択すると、AI アシスタントが回答できる質問の種類の例が表示されます。

1. プロンプト検出パネルを非表示にするには、![学習アイコン ](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Learn_18_N.svg)をもう一度クリックします。

### AEMのAI アシスタントに関するフィードバックを共有する

Adobeは、AI アシスタントのパフォーマンスと正確性を向上させるのに役立ちます。

次のオプションを通じて、AEMのAI アシスタントとエクスペリエンスに関するフィードバックを共有します。

![親指を上げる、親指を下げる、フラグのアイコン ](/help/implementing/cloud-manager/assets/ai-assistant-feedback-icons.png)

| Click | 説明 |
| --- | --- |
| ![ アウトラインの上にサムズアップ アイコン ](https://spectrum.adobe.com/static/icons/workflow_18/Smock_ThumbUpOutline_18_N.svg) | 何がうまくいったかを示し、肯定的なフィードバックを共有します。 |
| ![ アウトラインの下の親指アイコン ](https://spectrum.adobe.com/static/icons/workflow_18/Smock_ThumbDownOutline_18_N.svg) | 改善策の提案： 毎日レビューされる、エクスペリエンスに関する具体的なコメントを追加します。 |
| ![ フラグアイコン ](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Flag_18_N.svg) | AEMのAI アシスタントを使用して、顧客の懸念を報告したり、やり取りに関する詳細なフィードバックを提供したりできます。 |

## AEMのAI アシスタントに関するよくある質問 {#ai-faq}

ここでは、AI アシスタントに関するよくある質問に対する回答を紹介します。

* **AEMのAI アシスタントがリアルタイムで提供する情報ですか？**\
  いいえ。AI アシスタントは、Adobe Experience Leagueのドキュメントからコンテンツを調達しています。 コンテンツの更新が応答に反映されるまでに時間がかかる場合があります。
* **AEMのAI アシスタントでサポートされているAdobe アプリケーションはどれですか？**\
  現在、AI アシスタントは、Sites、Assets、Dynamic Media、Cloud Manager、Formsなど、AEM as a Cloud Serviceでの製品知識の問い合わせをサポートしています。
* **AEMのAI アシスタントの機能は何ですか？**\
  AEMのAI アシスタントは、Adobeの製品情報に関する質問に答えるために設計されています。
* **AEMのAI アシスタントは、トレーニング データに個人情報を使用していますか？**\
  いいえ。AEMのAI アシスタントは、トレーニング目的で個人情報を使用しません。 AEMのAI アシスタントを使用して、氏名や連絡先情報など、自身や他者に関する個人情報を共有することは避けます。

<!--
 IS THE DOCUMENTATION BELOW STILL NEEDED? IF SO, GO AHEAD AND DELETE THE COMMENT TAGS!!

## AEM Forms AI Assistant (Forms Experience Builder) {#ai-forms-builder}

In addition to the general AI Assistant in AEM for product knowledge, AEM offers a specialized **[AEM Forms AI Assistant (Forms Experience Builder)](/help/edge/docs/forms/forms-ai-assistant.md)**. This enhanced assistant can actively help you create and configure forms through natural language prompts and answer questions specific to forms.

### Key capabilities

The AEM Forms AI Assistant provides:

* **Form Creation**: Create new forms from scratch using natural language descriptions.
* **Design Import**: Convert existing designs (PDF, Figma, images) into functional AEM Forms. 
* **Form Configuration**: Add fields, panels, validation rules, and conditional logic.
* **Layout Management**: Organize form structure and optimize for different devices.
* **Integration Setup**: Configure form submissions and data handling.
* **Product Knowledge**: Answer questions about AEM Forms features and best practices.

### Where to access

The AEM Forms AI Assistant is available in the following:

* **Universal Editor**: For Edge Delivery Services forms with visual editing capabilities.
* **Adaptive Forms Editor**: For detailed form configuration and advanced features.
* **Forms Management UI**: For high-level form creation and management tasks.

### Getting started

>[!NOTE]
>
> The AEM Forms AI Assistant (Forms Experience Builder) is available under the private beta program. Send an email from your work address to [aem-forms-ea@adobe.com](mailto:aem-forms-ea@adobe.com) to request access.

To learn more about using the AEM Forms AI Assistant , see the [AEM Forms AI Assistant](/help/edge/docs/forms/forms-ai-assistant.md) documentation.

### Example Use Cases

* **"Create a customer feedback form with name, email, rating, and comments fields"**
* **"Convert this uploaded PDF application form into a digital adaptive form"**  
* **"Add conditional logic to show spouse information only when marital status is 'Married'"**
* **"Configure this form to submit data to the Customer Relationship Management system"**

This specialized AEM Forms AI Assistant represents the next evolution in form building, combining the power of AI with AEM's robust forms capabilities to streamline your form creation workflow.
-->
