---
title: アソシエイト UIの送信ワークフロー – IC PDF出力を生成
description: アソシエイト UIの送信とワークフローの仕組みを理解し、インタラクティブ通信（IC） JSONからPDFを生成するワークフローの例に従います。
products: SG_EXPERIENCEMANAGER/Cloud Service/FORMS
feature: Interactive Communication
role: User, Developer, Admin
exl-id: 9d8a33e4-e206-48e6-9daf-b15feb9c67a3
source-git-commit: 53ff71c82d35b9ec9b20b521ef469d3f0abd79df
workflow-type: tm+mt
source-wordcount: '440'
ht-degree: 1%

---

# アソシエイト UIの送信ワークフロー


この記事では、アソシエイト UIのワークフローを有効にした場合の送信とワークフローの仕組みについて説明します。 次に、送信ワークフローの設定方法を説明します。 このチュートリアルでは、例として、インタラクティブ通信（IC）ペイロードからPDFを生成する方法を使用します。他のワークフロータイプに手順を適応させることができます。

<!--
## Submission and workflow behavior {#submission-and-workflow-behavior}

When you enable **Configure Workflow for Update** for an Associate UI, submissions from the Associate UI can trigger an AEM workflow. The following explains where workflows run, who uses which environment, and how to plan for data and access.

### Where workflows run

AEM workflows always run on the **Author** instance. It does not matter whether the person submitting is an author or an associate—the workflow runs on Author. Plan your user groups and where you store workflow data with this in mind.

### Where associates use the Associate UI

Customer-facing associates use the Associate UI on the **Publish** instance only. You publish the Interactive Communication and expose the Associate UI through your Publish environment (for example, via your application or dispatcher). Associates do not use the Author instance. For step-by-step integration and how to invoke the Associate UI on the Publish instance, see [Integrate Associate UI in Your Application](/help/forms/interactive-communication/invoke-associate-ui.md).

### When an author submits from the Author instance

Authors can open the Associate UI on the Author instance—for example, to test the Interactive Communication or to submit on behalf of a customer. When they submit, the request is handled on Author and the workflow runs there. For this to work, the author must be in both **forms-associates** (to access the Associate UI) and **workflow-users** (to run the workflow).

### When an associate submits from the Publish instance

Associates open the Associate UI on the Publish instance, using the integration you set up. When they submit, the submission is sent to the Author instance and the workflow runs on Author. Associates sign in on Publish (for example, via [Microsoft Entra ID](https://www.microsoft.com/en-us/security/business/identity-access/microsoft-entra-id)) and do not need access to Author. To set up how associates open the Associate UI on Publish, see [Integrate Associate UI in Your Application](/help/forms/interactive-communication/invoke-associate-ui.md).
-->

## 送信ワークフローの設定

次の手順では、ユーザーがアソシエイト UIから送信するときに実行されるワークフローを作成する方法を示します。 ここでは、標準装備の&#x200B;**IC PDF出力をレンダリング**&#x200B;手順を使用して、**ICをPDF**&#x200B;にレンダリングする例として使用します。 ユーザーがアソシエイト UIから送信すると、ペイロードがワークフローに送信されます。この手順では、ペイロードから&#x200B;**communicationDom** （IC-JSON）を使用してPDFを生成します。

### ペイロード構造

ワークフローはJSON ペイロードを受信します。 **communicationDom** フィールドには、PDFの生成に使用されるIC-JSONが格納されます。 **IC PDF出力をレンダリング**&#x200B;手順では、それをテンプレート入力として使用します。

| フィールド | 説明 |
|-------|-------------|
| communicationDom | PDF生成用のIC-JSON |
| auditMetadata | 監査情報 |
| submitData | 送信済みフォームデータ（JSON） |
| prefillData | 事前入力データ（JSON） |
| リファラー、cookie、queryString、clientIP、userAgent、formSubmitter | リクエストメタデータ |

### ワークフローモデルの作成

1. **基本：** ワークフローモデルを作成します（例：ワークフローを&#x200B;**pdfrenderworkflow**&#x200B;として追加します）。

   ![&#x200B; ワークフローモデルの「基本」タブ &#x200B;](/help/forms/assets/associate-ui-add-workflow.png)

1. **変数：** ペイロードに一致する変数を追加し、手順：**communicationDom** （JSON）、**auditMetadata** （JSON）、**outputDocument** （Document）。

   ![&#x200B; ワークフロー変数](/help/forms/assets/associate-ui-add-variables.png)

1. **手順：** 「**IC PDF出力をレンダリング**」手順を追加します。
   ![&#x200B; ワークフローの追加ステップ &#x200B;](/help/forms/assets/associate-ui-add-step.png)

1. 「**Input**」タブで、**テンプレートを選択（JsonObject）**&#x200B;を&#x200B;**変数** → **communicationDom**&#x200B;に設定します。 ステップとモデルを保存します。

   ![IC Render PDF Output – 入力タブ &#x200B;](/help/forms/assets/associate-ui-input-variable.png)

1. 「**出力**」タブで、**テンプレートを選択（JsonObject）**&#x200B;を&#x200B;**変数** → **communicationDom**&#x200B;に設定します。 ステップとモデルを保存します。

   ![&#x200B; ワークフロー変数とキャンバス &#x200B;](/help/forms/assets/assocaite-ui-output-variable.png)

### ワークフローを接続してUIを関連付ける

[&#x200B; アソシエイト UI](/help/forms/interactive-communication/enable-configure-associate-ui.md)を有効にして設定するには、アソシエイトビューを有効にし、**ワークフロー**&#x200B;で&#x200B;**アップデート用ワークフローの設定**&#x200B;をオンにして、このワークフローモデルを選択します。 ICを公開し、[&#x200B; アソシエイト UIを統合](/help/forms/interactive-communication/invoke-associate-ui.md)して、このワークフローをトリガーに送信します。

![&#x200B; インタラクティブ通信設定 – アソシエイト UI](/help/forms/assets/associate-ui-configure-workflow.png)のワークフロー設定

**Externalize workflow data storage**&#x200B;が有効になっている場合は、Workflow dataが外部ストレージ（Azureなど）に保存されるようにexternaliserを設定します。 [&#x200B; ワークフローのデータの外部化](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/forms/create-aem-workflow/externalize-workflow.html)を参照してください。

## 関連トピック

- [インタラクティブ通信エディターでのUIの関連付け](/help/forms/interactive-communication/associate-ui-in-interactive-communication-editor.md)
- [インタラクティブ通信用のアソシエート UIの有効化と設定](/help/forms/interactive-communication/enable-configure-associate-ui.md)
- [アプリケーションにアソシエイト UIを統合する](/help/forms/interactive-communication/invoke-associate-ui.md)
- [ワークフローデータの外部化](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/forms/create-aem-workflow/externalize-workflow.html)

