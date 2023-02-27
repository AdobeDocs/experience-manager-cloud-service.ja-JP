---
title: Adobe Experience Manager(AEM)Formsas a Cloud Serviceの最新の革新
description: «の最新の機能を理解する [!DNL AEM Forms] エンタープライズクラスのフォームとビジネスプロセスの作成、管理、公開をas a Cloud Serviceできます。」
exl-id: 3a90b0aa-369a-4350-9904-79ef656b0f9a
source-git-commit: d77b8d389be4b5c0ffa262ad6f1ff8b4d899e82b
workflow-type: tm+mt
source-wordcount: '678'
ht-degree: 0%

---

<!-- # Introduction to [!DNL AEM Forms] as a Cloud Service {#overview}

Adobe Experience Manager Forms as a Cloud Service offers a cloud-native, Platform as a Service (PaaS) solution for businesses to create, manage, publish, and update complex digital forms while integrating submitted data with back-end processes, business rules, and saving data in an external data store. The service is always current, always available, and always learning.

You can use the service to create and rollout  interactive and engaging digital forms. For example, an organization is looking to digitize their customer enrollment journey. They have multiple data sources with existing customer data, they are looking to pre-populate forms, add e-sign their forms, and archive filled forms as PDF files. Besides, the organization has multiple print forms (PDF forms), they are also looking to convert all of their print forms to digital forms.

The organization can use [!DNL AEM Forms] as a Cloud Service to create digital forms, connect forms to existing data sources, integrate forms with [!DNL Adobe Sign] to add e-signatures to forms, and generate Document of Record (DoR) to archive filled forms as PDF files. The organization can also use the service to convert their existing PDF forms to digital forms. 

An organization can sign up for [!DNL AEM Forms] as a Cloud Service and start using all these features without waiting to buy and set up a local infrastructure. The service also frees the organizations from the cycle of upgrades as it is always up to date and always offers the latest feature.  -->


# 最新のイノベーション {#latest-innovations}

AEM Formsas a Cloud Serviceの最新のイノベーションの一部を次に示します。

|  |  |
|---|---|
| ヘッドレスアダプティブForms | 作成と管理 [ヘッドレスアダプティブForms](https://experienceleague.corp.adobe.com/docs/experience-manager-headless-adaptive-forms/using/overview.html) をAdobe Experience Managerプラットフォーム内で使用する。 開発者が、従来のグラフィカルユーザーインターフェイスを使用するのではなく、API を使用してアクセスし、操作できるインタラクティブフォームを作成、公開、管理できるようにします。 <br/> <br/> これらのフォームは、従来のHTMLフォームインターフェイスを使用せずに送信できるように設計されています。 つまり、フロントエンドに表示可能なフォーム要素を必要とせずに、API またはバックエンドコードを介してプログラムを使用してフォームデータを送信できます。 <br/> ![](https://experienceleague.corp.adobe.com/docs/experience-manager-headless-adaptive-forms/assets/how-headless-adaprive-forms-work.png?)<br/> ヘッドレスフォームは、シングルページアプリケーション、プログレッシブ Web アプリ、モバイルアプリケーションを構築する場合など、従来のHTMLフォームインターフェイスが必要でない場合や実用的でない場合に、様々なシナリオで役立ちます。 開発者が API やバックエンドコードを介して直接フォームデータを送信できるようにすることで、ヘッドレスフォームを利用してワークフローを合理化し、Web アプリケーションの全体的なパフォーマンスを向上させることができます。 |
| コアコンポーネント | この [アダプティブFormsコアコンポーネント](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html#features) は、Adobe Experience Manager WCM コアコンポーネントの基盤上に構築された、24 個のオープンソースの BEM 準拠コンポーネントのセットです。 これらは、アダプティブFormsの作成に使用するように特別に設計されています。アダプティブフォームとは、ユーザーのデバイス、ブラウザー、画面サイズに応じたフォームです。 <br/> <br/> これらのコンポーネントは、テキストフィールド、チェックボックス、ドロップダウンメニューなど、様々なフォームフィールドオプションを提供することで、例外的なデータ取得および登録エクスペリエンスを作成するために使用できます。 また、検証、条件付きロジック、レスポンシブデザインなどの機能も含まれ、使いやすく使いやすいフォームを作成するのに使用できます。 <br/> ![](https://experienceleague.corp.adobe.com/docs/experience-manager-cloud-service/assets/sample-core-components-based-adaptive-form.png?)<br/>  さらに、これらのコンポーネントはオープンソースなので、開発者は、組織の特定のニーズに合わせてコンポーネントを簡単にカスタマイズおよび拡張できます。 また、これらのコンポーネントは、拡張性と保守性を確保する BEM 手法に基づいて構築されます。 |
| Microsoft PowerAutomate Connector | AEM Forms Power Automate Connector を使用すると、Adobe Experience Manager(AEM)FormsをMicrosoft Power Automate( 旧称Microsoftフロー ) と統合できます。 Power Automate は、様々なアプリケーションやサービス間で自動ワークフローを作成できるクラウドベースのサービスです。  <br/> <br/> AEM Form Power Automate Connector を使用すると、アダプティブフォームの送信に基づいて自動的にトリガーを設定するワークフローを作成できます。 例えば、ユーザーがフォームを送信したときに電子メール通知を特定のユーザーに自動的に送信するワークフローや、ユーザーがフォームを完了したときにMicrosoft Planner でタスクを作成するワークフローを作成できます。  <br/> ![](https://powerusers.microsoft.com/t5/image/serverpage/image-id/182924i17C4BEA1C045D731/image-size/large/is-moderation-mode/true?v=1.0&amp;px=999) <br/> AEM Forms Power Automate Connector は、Microsoft Power Automate に接続する他のアプリケーションやサービスとアダプティブFormsを自動化および統合し、様々なツールを操作できる強力なツールです。 特定のニーズに合わせてワークフローを作成し、カスタムのアクション、条件およびトリガーを追加できます。 さらに、Power Automate では詳細な分析とレポート機能を提供し、時間の経過と共にワークフローを監視および最適化できます。 |
| Microsoft Storage Connectors | AEM Forms Microsoft Storage Connectors for <a href="https://experienceleague.corp.adobe.com/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-foundation-components/configure-submit-actions-and-metadata-submission/configuring-submit-actions.html#submit-to-sharedrive">OneDrive</a>, <a href="https://experienceleague.corp.adobe.com/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-foundation-components/configure-submit-actions-and-metadata-submission/configuring-submit-actions.html?#submit-to-sharedrive"> SharePoint </a> および <a href="https://experienceleague.corp.adobe.com/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-foundation-components/configure-submit-actions-and-metadata-submission/configuring-submit-actions.html?#submit-to-azure-blob-storage"> Azure Blob ストレージ </a> は、Adobe Experience Manager(AEM)FormsをMicrosoft OneDrive およびSharePointと統合するためのコネクタです。 このコネクタを使用すると、アダプティブFormsから直接 OneDrive とSharePointにデータファイルと添付ファイルをアップロードできます。 <br/> ![](/help/forms/assets/onedrive-and-sharepoint.jpg) <br/>OneDrive とSharePointは、CRM システム、会計ソフトウェア、プロジェクト管理ツールなど、他のビジネスアプリケーションと統合できます。 これにより、ビジネス・プロセスを合理化し、手動でのデータ入力を削減し、全体的な効率を向上させることができます。 |


<!-- 

# Key features and capabilities {#key-features}

[!DNL AEM Forms] as a Cloud Service provides several cloud-native capabilities such as a cloud-native architecture, auto-scaling, zero downtime for upgrades, a CDN (Content Delivery Network), cloud-native development environment, and ability to self-Service the environments via Cloud Manager. You can use the service to: 

* [Create Adaptive Forms](creating-adaptive-form.md#strong-create-an-adaptive-form-strong) that automatically render for a user's device and browser.

    ![Adaptive Forms](assets/rule-editor-example.gif)

* [Create pixel-perfect PDF forms](use-forms-designer.md#create-an-adaptive-form) that look almost like paper.

* Use [Automated Forms Conversion service](https://experienceleague.adobe.com/docs/aem-forms-automated-conversion-service/using/introduction.html) to convert a PDF Form to an Adaptive Form. It helps you accelerate digitization and modernization of data capture experiences of your organization.

    ![Automated Forms Conversion service](assets/pdf-to-adaptive-form-gitx50.gif)

* [Create business processes](aem-forms-workflow-step-reference.md#create-form-centric-workflows). For example, You can create and trigger an approval and rejection workflow on submission of an Adaptive Form.

In addition to above [!DNL AEM Forms] as a Cloud Service offers the following features and capabilities:

* An easy-to-use graphical user interface to let business users easily import, manage, preview, and publish forms
* A responsive forms directory with powerful search features using keywords, tags, and metadata
* Dynamic detection of a user's device and location to render the form appropriately across web and mobile channels
* [Integration with Adobe Sign](adobe-sign-integration-adaptive-forms.md) services or Scribble to electronically sign documents containing confidential information
* Ability to [connect the service to various types of data sources](data-integration.md#create-an-adaptive-form) to send and retrieve data. The service supports sending and retrieving data from RESTful web services, SOAP-based web services, and OData enabled services.
* Integration with AEM Sites. It allows to embed an adaptive form in an AEM Sites page. You can also integrate an adaptive form to any webpage. 
* Ability to create a Document of Record (DoR) to keep a record of the information that you provide and submit in an Adaptive Form so that you can refer to it later. A DoR is a PDF version of a form. It includes both a template and data. The service provides a default DoR template and tools to develop a custom template.
* Ability to create Adaptive Forms to produce schema-compliant data. It helps you submit captured data to existing processes and data sources without any or minimal modifications.
* Ability to create a prefill service to fill a form with existing customer data based on a criteria. It helps fasten the form filling process and reduce the abandon rate.


<!-- 

## Enterprise-class forms {#enterprise-class-forms}

You can create enterprise class forms (Adaptive Forms) and deliver beautiful, interactive, responsive, and personalized experiences to your customers. These forms change behavior and appearance based on the underlying device. You can also use themes and templates with Adaptive Forms to mandate a uniform structure and appearance for all the forms of an organization or a department.

![Creating custom patterns for fields in CrxDe](assets/adaptive-form.png)

## Automatic conversion of PDF forms to Adaptive Forms {#automatic-conversion-of-pdf-forms-to-adaptive-forms}

You can use Automated Forms Conversion service to convert a PDF Form to an Adaptive Form. It helps you accelerate digitization and modernization of data capture experiences of your organization.

![Creating custom patterns for fields in CrxDe](assets/pdf-to-adaptive-form-gitx50.gif)

## Data Integration {#data-integration}

You can connect the service to various types of data sources to send and retrieve data. The service supports sending and retrieving data from RESTful web services, SOAP-based web services, and OData enabled services.

![Build dynamism and interactivity to Adaptive Forms](assets/rule-editor-example.gif)

## Integration with [!DNL Adobe Sign] {#integration-with-adobe-sign}

 You can integrate the service with [!DNL Adobe Sign] and add [!DNL Adobe Sign] fields to an Adaptive Form. It allows your users to e-sign an Adaptive Form and use [!DNL Adobe Sign] with AEM Workflows. You can use AEM Workflows to develop a business logic and send forms and documents to recipients for signatures based on the business logic.

![Creating custom patterns for fields in CrxDe](assets/adobe-sign.png)


## Integration with [!DNL AEM Sites] {#integration-with-aem-sites}

You can embed an adaptive form in an AEM Sites or an external webpage. The service provides a component out of the box to integrate an adaptive forms to an AEM Sites page.

![integrate an adaptive forms to an AEM Sites page](assets/integrate.png)

## Business Processes Automation {#bpa}

You can use AEM Workflows to create business processes and automate operations. For example, You can create and trigger an approval and rejection workflow on submission of an Adaptive Form. 

![Create and trigger an approval and rejection workflow](assets/workflow.png)

## Document of Record {#dor}

You can create a Document of Record (DoR) to keep a record of the information that you provide and submit in an Adaptive Form so that you can refer to it later. A DoR is a PDF version of a form. It includes both a template and data. The service provides a default DoR template and tools to develop a custom template.

![Build dynamism and interactivity to Adaptive Forms](assets/designer.png)

## Rule editor {#rule-editor}

Rule editor empowers you to build dynamism and interactivity to Adaptive Forms. These rules define actions to trigger on form objects based on preset conditions, user inputs, and user actions on the form. It helps  streamline the form filling experience while ensuring accuracy and speed.
  
![Creating custom patterns for fields in CrxDe](assets/form-data-model.png)


## WYSIWYG editors {#wysiwyg-editor} 

The service provides several WYSIWYG editors: Adaptive Forms editor, Theme editor, and Template editor. These help you create and edit forms and related assets in WYSIWYG manner. The editors also provide out-of-the-box options to simulate views for popular mobile devices, tablets, and desktop screen configurations.

![Creating custom patterns for fields in CrxDe](assets/emulators.png)

## Schema-compliant data {#schema-complaint-data}

You can create Adaptive Forms to produce schema-compliant data. It helps you submit captured data to existing processes and data sources without any or minimal modifications.

![Build dynamism and interactivity to Adaptive Forms](assets/display-validation-error.gif)

## Prefill a form

You can create a prefill service to fill a form with existing customer data based on a criteria. It helps fasten the form filling process and reduce the abandon rate.

## Submit Actions

A Submit Action allows you to persist and process captured data. The service provides several Submit Actions out-of-the-box. You can use these Submit Actions to send submitted data to a REST endpoint, database, or an AEM Workflow. You can also email submitted data along with attachments and Document of Record(DoR). You can also develop a custom Submit Action to perform an action specific to your business.

* **Emulators:** You can view an Adaptive Form in an in-built emulator. It helps you simulate how an Adaptive Form appears on different devices to an end user. It provides out-of-the-box options to simulate views for popular mobile devices, tablets, and desktop screen configurations. 

In addition to standard [!DNL AEM Forms] features, [!DNL AEM Forms] as a Cloud Service provides several cloud-native capabilities such as a cloud-native architecture, auto-scaling, zero downtime for upgrades, a CDN (Content Delivery Network), cloud-native development environment, and ability to self-Service the environments via Cloud Manager. -->
