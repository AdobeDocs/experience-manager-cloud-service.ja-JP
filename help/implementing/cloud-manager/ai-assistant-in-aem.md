---
title: AEM の AI アシスタント
description: AI アシスタントを使用して回答を見つけ、Adobe Experience Manager で使用可能なソリューションのトラブルシューティングを行います。
solution: Experience Manager
feature: Authoring, AI Assistant, AI Tools
role: Admin, Architect, Developer, User
exl-id: 81e7b1ac-50d0-4547-8622-bf145ebc3dc0
source-git-commit: b0570595a05f311a16f2522cabc0661e5f1db15e
workflow-type: tm+mt
source-wordcount: '1280'
ht-degree: 5%

---

# AEM の AI アシスタント {#about-ai-assistant-in-aem}

Adobe Experience Manager（AEM）の AI アシスタントは、AEM関連のクエリに対する回答の検索を合理化するように設計された対話型インターフェイスを提供します。 AEM製品に関する質問に即座に回答したり（*すべてのユーザーが利用できます*）、サポートチケットの自動作成を行ったり（*サポート管理者が利用できます*。

AI アシスタントは、次のソリューションを含むAEM as a Cloud Serviceをサポートします。

* Experience Hubの概要ページ
* Edge Delivery Services
* Sites
* Assets
* Forms
* Dynamic Media
* Cloud Manager


AEM に直接埋め込まれ、AEM Experience Hub、Cloud Manager、オーサー UI からアクセスできます。

次の 3 分 25 秒のビデオでは、AEMの AI アシスタントについて順を追って説明します。

>[!VIDEO](https://video.tv.adobe.com/v/3475357/?learn=on&enablevpops)

## AEMの AI アシスタントにアクセスできます{#get-access}

AEMの AI アシスタントにアクセスするには、次が必要です。

* AEMの AI アシスタントを使用して製品に関する知識を得る権限。 この権限を使用すると、AI アシスタントのチャットで製品に関する質問をすることができます。 この権限を有効にする必要があります。
* サポートチケットを開く権限。これには **サポート管理者** の役割が必要です。

>[!NOTE]
>
>AEMの AI アシスタントリクエストは、Adobe Identity Management サービス（IMS）を通じて認証されます。 詳しくは、[Adobe Identity Management サービスの概要 &#x200B;](https://www.adobe.com/content/dam/cc/en/trust-center/ungated/whitepapers/corporate/adobe-identity-management-services-security-overview.pdf) を参照してください。

**AEMで AI アシスタントにアクセスするには：**

1. Adobe Experience Managerで AI を活用したエージェントによる機能のほとんどにアクセスするには、契約を締結する必要があります。 詳しくは、Adobe担当者にお問い合わせください。

1. AEMで AI アシスタントを使用するには、AI アシスタントを通じて製品ナレッジにアクセスする権限が必要です。 この権限は、デフォルトでオンになっています。

   製品ナレッジにアクセスできるユーザーを制御する場合は、Adobe IDに関連付けられた電子メールアドレスから [aemaiassistant@adobe.com](mailto:aemaiassistant@adobe.com) に電子メールを送信します。 Adobeでは、ユーザーレベルのアクセス制御を有効にできます。 これが有効になっていると、管理者は [AEMで AI アシスタントを設定する &#x200B;](/help/implementing/cloud-manager/ai-assistant-in-aem-admin.md) の手順に従って、ユーザーレベルのアクセス権を付与できます。

## 範囲 {#scope}

AEMの AI アシスタントの現在の対象範囲は、AEM as a Cloud Serviceの製品ナレッジの問題への対処に重点を置いています。 この範囲には、主要な領域に対する包括的なサポートが含まれます。<!--, such as Sites, Assets, Forms, Edge Delivery Services, Dynamic Media, and Cloud Manager. -->

* **サーフェス**:AEM Experience Hub、オーサー UI、Cloud Managerで使用可能です。
* **機能**：トラブルシューティングとガイダンスのための製品知識とファーストストップ、サポートチケットの自動作成とルックアップ。
* **価値**：時間を節約し、学習と価値を生み出すまでの時間を短縮し、サポートチケットを手動で作成する必要性を減らし、サポートチケットの作成を効率化します。

## プライバシー、セキュリティ、ガバナンス{#privacy-security-governance}

AEMの AI アシスタントは、プライバシー、セキュリティ、ガバナンスに重点を置いて設計されています。

この記事では、AEMの AI アシスタントに期待できる信頼を中心とした機能の概要を説明します。

* AEMの AI アシスタントは、トレーニング目的を含め、個人情報を使用しません。
* AEMの AI アシスタントが消費者データにアクセスできません。
* AEMで AI アシスタントとやり取りするには、明示的な権限が必要です。
* ユーザー指定のプロンプト（質問、クエリなど）は、他の顧客と共有されません。

<!-- See also [Security at Adobe whitepaper](). NEED ACTIVE LINK FROM ADRIAN NICOLAE TANASE. CURRENTLY 404. -->

## AEMの AI アシスタントの製品知識と自動サポートチケット作成について説明します {#ai-prod-insights}

製品知識には、Adobe Experience League ドキュメントから派生した概念とトピックが含まれます。 これらの質問は、次のサブグループに分類できます。


| 製品に関する知識 | すべてのユーザーが利用できる <br> 例 |
| :--- | :--- |
| 先を見越した学習 | <ul><li>ユニバーサルエディターとは</li><li>Cloud Managerでプログラムを作成するにはどうすればよいですか？</li></ul> |
| 検出を開く | <ul><li>ユニバーサルエディターの使用方法</li><li>環境間でコンテンツをコピーする方法はありますか？</li></ul> |
| トラブルシューティング | <ul><li>ユニバーサルエディターにアクセスできないのはなぜですか？</li><li>パイプラインが失敗する理由</li></ul> |
| **サポートチケットの作成** | **管理者のみをサポートできます&#x200B;**<br>**例** |
| AI アシスタントのチャット履歴とコンテキストをキャプチャする自動サポートチケット作成 | <ul><li>サポートチケットを作成する</li></ul> |
| サポートチケットのステータスの取得 | <ul><li>オープンしたサポートチケットを全て見せてください。</li><li>チケット「E---------- –」のステータスを表示</li></ul> |

{style="table-layout:auto"}


## 効果的な質問の作成方法 {#ai-craft-questions}

AEMの AI アシスタントから最も正確な回答を受け取るには、明確さとコンテキストで質問をフレーズ化することが重要です。 次のヒントを使用して、クエリが明確で適切に構造化されていることを確認します。

* タスクまたは質問を簡潔に明確に述べます。
* あいまいな表現や複雑すぎる構文を避けて、理解を深めます。
* このアプローチは、AEMの AI アシスタントがより正確で関連性の高い回答を提供するのに役立つので、タスクや質問に関する関連するコンテキストを含めます。
例えば、プロンプトでは、使用しているAEM ソリューション（Sites、Assets、Dynamic Media、Edge Delivery Services、Cloud Manager、Forms）に名前を付けるのに役立ちます。

### サポートされていない質問の例 {#ai-unsupported-questions}

| 領域 | 例 |
| --- | --- |
| 運用インサイト | <ul><li>テナントに存在する開発環境の数</li><li>最後の実稼動パイプラインを開始したのは誰ですか？</li></ul> |
| トラブルシューティング | <ul><li>実稼動パイプラインが失敗する理由</li></ul> |
| タスクと自動処理 | <ul><li>開発ブランチからコード品質パイプラインを設定します。</li></ul> |


## AEMでの AI アシスタントの使用 {#ai-use}

<!-- UNHIDE AFTER BETA or at GA
### Enable AI Assistant in AEM access through Admin Console 

To use AI Assistant in AEM, your organization must opt in at the Admin Console level. A product administrator creates (or chooses) a user group and grants it the new "AI Assistant" permission. Anyone added to that group instantly gains access to the Assistant across AEM. If the goal is company-wide availability, the admin simply assigns all users to that group.

![AI Assistant in AEM in the Admin Console](/help/implementing/cloud-manager/assets/ai-assistant-admin-console.png)

From an employee's perspective, the process is straightforward: identify the product administrator for Adobe Experience Manager in your organization and request to be added to the AI-enabled user group. Once you appear in that group, the Assistant icon shows up automatically the next time you sign in.

Administrators should keep normal Cloud Manager governance in mind. Hold product administrator rights in the Admin Console to create profiles, manage user groups, or edit permissions. If users also need the Assistant's built-in **Create Support Ticket** feature, add the standard **Support Admin** role (standard Admin Console role) to the same individuals or group.

![Technical support ticket creation in AI Assistant in AEM of the Admin Console](/help/implementing/cloud-manager/assets/ai-assistant-admin-console-support-ticket.png)

For a guided walkthrough of setting up users and groups in AEM as a Cloud Service, see [Configuring access to AEM as a Cloud Service ](https://experienceleague.adobe.com/ja/docs/experience-manager-learn/cloud-service/accessing/overview). 

See also [Custom Permissions](/help/implementing/cloud-manager/custom-permissions.md). -->


### AEMとのやり取りで AI アシスタントを開始

AEMで AI アシスタントをリセットし、トピックを変更する際に新しい会話を開始することができます。 この機能は、失敗したクエリや誤った情報が提供されたクエリのトラブルシューティングを行う場合に特に役立ちます。

**AEMでの会話で AI アシスタントを開始するには：**

1. AEM ユーザーインターフェイス（Cloud Manager ページまたはAEM環境のオーサーインスタンス）の右上隅付近にある「**AI アシスタント**」アイコンをクリックします。

   ![&#x200B; ツールバーの AI アシスタントアイコン &#x200B;](/help/implementing/cloud-manager/assets/ai-assistant-icon.png)

1. 下部の **AI アシスタント** パネルのテキストボックスに、質問またはプロンプトを入力し、`Enter` キーを押すか、![&#x200B; 送信アイコン &#x200B;](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Send_18_N.svg) をクリックします。

   >[!NOTE]
   >
   >このツールを使用する必要がないため、個人データを入力に含めないでください。

   ![AI アシスタントパネルの下部にあるテキストボックス &#x200B;](/help/implementing/cloud-manager/assets/ai-assistant-prompt-text-box.png)

1. 新しい会話（新しいトピックまたはトピック内の変更）を開始するには、![&#x200B; 詳細アイコン &#x200B;](https://spectrum.adobe.com/static/icons/workflow_18/Smock_More_18_N.svg) > **新しい会話の開始** をクリックします。

   ![&#x200B; 省略記号アイコンから AI アシスタントで新しい会話を開始する &#x200B;](/help/implementing/cloud-manager/assets/ai-assistant-start-new-conversation.png)

### カテゴリ別のプロンプトの検索

AEMの AI アシスタントには、サポートされているトピックやカテゴリを参照するのに役立つ検出機能が含まれています。

**カテゴリ別にプロンプトを検出するには：**

1. AI アシスタント パネルで ![&#x200B; 学習アイコン &#x200B;](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Learn_18_N.svg) をクリックして、プロンプト検出パネルをオンにします。

   ![AI アシスタントでカテゴリ別のプロンプトを調査できるパネル &#x200B;](/help/implementing/cloud-manager/assets/ai-assistant-discover-prompts.png)
   *AI アシスタントでプロンプトのカテゴリを表示するパネル。*

1. カテゴリを選択して、関連するプロンプトのリストを表示します。
1. プロンプトを選択して、AI アシスタントが回答できる質問のタイプの例を確認します。

1. プロンプト検出パネルを非表示にするには、もう一度 ![&#x200B; 学習アイコン &#x200B;](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Learn_18_N.svg) をクリックします。

### AEMの AI アシスタントに関するフィードバックをお寄せください

入力した情報は、Adobeが AI アシスタントを改善して、パフォーマンスと精度を向上させるのに役立ちます。

AEMの AI アシスタントでは、次のオプションを通じて、ご意見やご感想をお寄せください。

![&#x200B; サムズアップ、サムズダウン、フラグアイコン &#x200B;](/help/implementing/cloud-manager/assets/ai-assistant-feedback-icons.png)

| Click | 説明 |
| --- | --- |
| ![&#x200B; サムズアップアウトインアイコン &#x200B;](https://spectrum.adobe.com/static/icons/workflow_18/Smock_ThumbUpOutline_18_N.svg) | うまくいったことを示し、肯定的なフィードバックを共有します。 |
| ![&#x200B; サムズダウンラインアイコン &#x200B;](https://spectrum.adobe.com/static/icons/workflow_18/Smock_ThumbDownOutline_18_N.svg) | 改善のための提案を行います。 エクスペリエンスに関する特定のコメントを追加し、それを毎日確認します。 |
| ![&#x200B; フラグアイコン &#x200B;](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Flag_18_N.svg) | AEMの AI アシスタントとのインタラクションに関する懸念を報告したり、詳細なフィードバックを提供したりします。 |

## AEMの AI アシスタントに関するよくある質問（FAQ） {#ai-faq}

ここでは、AI アシスタントに関するよくある質問に対する回答を示します。

* **AEMの AI アシスタントからリアルタイムで情報が提供されますか？**\
  いいえ。AI Assistant は、Adobe Experience League のドキュメントからコンテンツを入手します。 コンテンツの更新が応答に反映されるまでに時間がかかる場合があります。
* **AEMの AI アシスタントがサポートするAdobe アプリケーションは**\
  現在、AI アシスタントは、Sites、Assets、Dynamic Media、Cloud Manager、Formsなど、AEM as a Cloud Serviceでの製品に関する知識の照会をサポートしています。
* **AEMの AI アシスタントの機能は何ですか？**\
  AEMの AI アシスタントは、Adobe製品の知識に関する質問に回答するように設計されています。
* **AEMの AI アシスタントは、個人情報をトレーニングに使用しますか？**\
  いいえ。AEMの AI アシスタントは、トレーニング目的で個人情報を使用しません。 AEMの AI アシスタントで、自分自身や他の人に関する個人情報（名前や連絡先の詳細など）を共有しないでください。

<!-- IS THE DOCUMENTATION BELOW STILL NEEDED? IF SO, GO AHEAD AND DELETE THE COMMENT TAGS!!

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
