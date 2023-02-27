---
title: ' [!DNL AEM Forms] as a Cloud Service の概要'
description: AEM Forms を理解し、ビジネスに適したドキュメントやコンテンツの作成にどのように役立つのかを学びます。サービスとしてのプラットフォーム（PaaS）、エンタープライズクラスのデジタルフォームとビジネスプロセスを管理する方法、現在のデータソースに Forms を接続する方法について学びます。
landing-page-description: AEM as a Cloud Service でのフォームの使用方法を理解します。
exl-id: aa5ef10c-ba78-4a9d-8b2b-a72a7a306888
source-git-commit: 2f9c4d85c55ee63a769c0137d4a70b2126228d5b
workflow-type: tm+mt
source-wordcount: '1144'
ht-degree: 25%

---

# はじめに {#introduction}

Adobe [!DNL Experience Manager Forms as a Cloud Service] は、複雑なデジタルフォームを作成、管理、公開、更新しながら、送信データをバックエンドプロセス、ビジネスルール、外部データストアに保存する、クラウドネイティブのサービスとしてのプラットフォーム（PaaS）ソリューションを提供します。このサービスは常に最新で、常に利用可能で、常に学習可能です。

このサービスを使用して、インタラクティブで魅力的なデジタルフォームを作成し、展開できます。例えば、顧客登録ジャーニーのデジタル化を検討している組織について考えてみます。既存の顧客データを持つ複数のデータソースがあります。フォームに事前入力したり、フォームの電子サインを追加したり、入力済みのフォームを PDF ファイルとしてアーカイブしたりすることを検討しています。さらに、組織には複数の印刷フォーム（PDF フォーム）があり、すべての印刷フォームをデジタルフォームに変換することも検討しています。



組織は、[!DNL AEM Forms] as a Cloud Service を使用して、デジタルフォームを作成したり、フォームを既存のデータソースに接続したり、フォームを [!DNL Adobe Sign] と統合して電子サインをフォームに追加したり、送信されたフォームを PDF ファイルとしてアーカイブするためにレコードのドキュメント（DoR）を生成したりできます。また、このサービスを使用して、既存の PDF フォームをデジタルフォームに変換することもできます。

組織は、[!DNL AEM Forms] as a Cloud Service を使用して、ローカルインフラストラクチャを必要とせずに、クラウド内のこれらすべての機能を取得できます。また、このサービスは常に最新の機能を備えているので、複雑なアップグレードサイクルから組織を解放します。

## 主な機能 {#key-features}

<!-- 
>[!BEGINTABS]

>[!TAB Adaptive Forms]

Adaptive Forms allows businesses to create and manage interactive, data-driven forms for their websites and other digital channels responsive, mobile-friendly forms without. </br> </br> Adaptive Forms in AEM also include a drag-and-drop form builder, which enables non-technical users to easily create and customize forms using pre-built form components such as text boxes, dropdown menus, and date pickers. This enables faster form creation and eliminates the need for extensive coding and development. </br> </br> In addition, AEM Adaptive Forms offer several other features, including: <ul><li>Advanced workflows for routing, approval, and submission of form data Real-time validation and error checking to ensure data accuracy </li><li>Integration with third-party data sources and APIs for pre-filling form fields or validating data </li><li>Advanced analytics and reporting capabilities to track form usage, conversion rates, and other key metrics </li><li>Integration with Adobe Sign and DocuSign for e-signatures </li>

>[!TAB Automated Forms Conversion Service]

Automated Forms Conversion Service allows businesses to convert legacy PDF-based forms into interactive, digital forms that can be easily managed and distributed online. The service helps: <ul><li>Save manual effort required to convert print forms to adaptive forms.</li><li>Applies patterns and appropriate validations during conversion</li><li>Generate Document of Record during conversion </li><li>Group commonly occurring fields into reusable form fragments </li> <li>Enables Adobe Analytics during conversion</li>

>[!TAB Communications API (Document Services)]

Communications APIs are a set of RESTful APIs (Application Programming Interfaces) that enable businesses to automate the creation, management, and delivery of personalized, data-driven communications. </br> </br> These APIs also enable businesses to integrate their communications workflows with third-party systems and data sources, allowing them to create highly targeted and personalized messages that are triggered by specific events or user behaviors. Some key features of AEM Forms Communications APIs include:<ul><li> Dynamic content delivery: The APIs allow businesses to create and deliver dynamic content that is tailored to individual users based on their preferences, behaviors, and past interactions with the business.</li> <li>Personalized messaging: The APIs enable businesses to personalize their communications by including user-specific data such as names, addresses, and purchase history.</li><li>Integration with back-end systems: The APIs can be integrated with a wide range of back-end systems, including CRMs, databases, and marketing automation platforms.</li><li> Generate Pixel Perfect PDF documents: The APIs generate pixel-perfect PDF documents that are customized with user-specific data and content. This feature enables businesses to create highly professional and polished documents, such as invoices, contracts, and statements, that are delivered to users in PDF format.

>[!TAB Advanced Analytics]

The service provides OOTB support to connect with Adobe Analytics. Connecting forms with Adobe Analytics provides several benefits for businesses, including: <ul><li> Improved understanding of user behavior: By connecting forms with Adobe Analytics, businesses can gain a deeper understanding of how users are interacting with their forms. This includes insights into user engagement, conversion rates, drop-off points, and other key metrics that can help businesses identify areas for improvement and optimize their forms for better user experiences. </li><li>Better targeting of marketing efforts: By analyzing user behavior on forms, businesses can gain valuable insights into user preferences and interests. This information can be used to better target marketing efforts and create more effective campaigns that drive engagement and conversions. </li><li> Reduced error rate: By integrating forms with Adobe Analytics, you can find insights about field with most errors and improve data quality, leading to better decision-making and more accurate insights. </li><li> Improved ROI: By optimizing forms based on insights gained from Adobe Analytics, businesses can improve conversion rates and drive more revenue from their digital channels. This can lead to a higher return on investment (ROI) for marketing and digital initiatives, helping businesses to achieve their goals and drive growth.</li>


>[!ENDTABS] -->

| アダプティブフォーム | 通信 API | 自動フォーム変換サービス | Forms Workflow | E 署名 | Forms Analytics | データモデル |
|---|---|---|---|---|---| ---|
| Web サイト、アプリ、その他のデジタルチャネルや印刷チャネル向けの、インタラクティブで動的で、レスポンシブで、モバイルに適した、データ駆動型のフォームを作成および管理します。 | RESTful API(Application Programming Interfaces) とのパーソナライズされたデータ駆動型通信の作成、管理、および配信を、オンデマンドで、またはスケジュールされた間隔で自動化します。 | 従来のPDFベースのフォームを、オンラインで容易に管理および配布できるアダプティブFormsに変換する。 | フォームとドキュメントサービスに関するビジネスプロセスを自動化します。 ビジネスプロセスの様々な段階を進めるにつれ、フォームとドキュメントの割り当て、ルーティング、確認、承認を行います。 | Adobe Signや DocuSign と統合して、電子署名用にFormsとドキュメントを簡単にユーザーに送信できます。 | Adobe Analyticsを使用して、ユーザーの行動と環境設定に関する貴重なインサイトを得ます。 | フォームとドキュメントを外部データソースと簡単に接続して、データを取得して送信します。 |

<!--
| | |
|---|---|
| Adaptive Forms | Adaptive Forms allows businesses to create and manage interactive, data-driven forms for their websites and other digital channels responsive, mobile-friendly forms without. </br> </br> Adaptive Forms in AEM also include a drag-and-drop form builder, which enables non-technical users to easily create and customize forms using pre-built form components such as text boxes, dropdown menus, and date pickers. This enables faster form creation and eliminates the need for extensive coding and development. </br> </br> In addition, AEM Adaptive Forms offer several other features, including: <ul><li>Advanced workflows for routing, approval, and submission of form data Real-time validation and error checking to ensure data accuracy </li><li>Integration with third-party data sources and APIs for pre-filling form fields or validating data </li><li>Advanced analytics and reporting capabilities to track form usage, conversion rates, and other key metrics </li><li>Integration with Adobe Sign and DocuSign for e-signatures </li>|
| Automated Forms Conversion Service | Automated Forms Conversion Service allows businesses to convert legacy PDF-based forms into interactive, digital forms that can be easily managed and distributed online. The service helps: <ul><li>Save manual effort required to convert print forms to adaptive forms.</li><li>Applies patterns and appropriate validations during conversion</li><li>Generate Document of Record during conversion </li><li>Group commonly occurring fields into reusable form fragments </li> <li>Enables Adobe Analytics during conversion</li>|
| Communications API (Document Services) | Communications APIs are a set of RESTful APIs (Application Programming Interfaces) that enable businesses to automate the creation, management, and delivery of personalized, data-driven communications. </br> </br> These APIs also enable businesses to integrate their communications workflows with third-party systems and data sources, allowing them to create highly targeted and personalized messages that are triggered by specific events or user behaviors. Some key features of AEM Forms Communications APIs include:<ul><li> Dynamic content delivery: The APIs allow businesses to create and deliver dynamic content that is tailored to individual users based on their preferences, behaviors, and past interactions with the business.</li> <li>Personalized messaging: The APIs enable businesses to personalize their communications by including user-specific data such as names, addresses, and purchase history.</li><li>Integration with back-end systems: The APIs can be integrated with a wide range of back-end systems, including CRMs, databases, and marketing automation platforms.</li><li> Generate Pixel Perfect PDF documents: The APIs generate pixel-perfect PDF documents that are customized with user-specific data and content. This feature enables businesses to create highly professional and polished documents, such as invoices, contracts, and statements, that are delivered to users in PDF format.|
|Advanced Analytics| The service provides OOTB support to connect with Adobe Analytics. Connecting forms with Adobe Analytics provides several benefits for businesses, including: <ul><li> Improved understanding of user behavior: By connecting forms with Adobe Analytics, businesses can gain a deeper understanding of how users are interacting with their forms. This includes insights into user engagement, conversion rates, drop-off points, and other key metrics that can help businesses identify areas for improvement and optimize their forms for better user experiences. </li><li>Better targeting of marketing efforts: By analyzing user behavior on forms, businesses can gain valuable insights into user preferences and interests. This information can be used to better target marketing efforts and create more effective campaigns that drive engagement and conversions. </li><li> Reduced error rate: By integrating forms with Adobe Analytics, you can find insights about field with most errors and improve data quality, leading to better decision-making and more accurate insights. </li><li> Improved ROI: By optimizing forms based on insights gained from Adobe Analytics, businesses can improve conversion rates and drive more revenue from their digital channels. This can lead to a higher return on investment (ROI) for marketing and digital initiatives, helping businesses to achieve their goals and drive growth.</li>|

-->

## 最新のイノベーション {#latest-innovations}

>[!BEGINTABS]

>[!TAB ヘッドレスアダプティブForms &#x200B;]

||| |—|—| |![](https://experienceleague.corp.adobe.com/docs/experience-manager-headless-adaptive-forms/assets/how-headless-adaprive-forms-work.png?lang=en)|作成と管理 [ヘッドレス web フォーム](https://experienceleague.corp.adobe.com/docs/experience-manager-headless-adaptive-forms/using/overview.html) をAdobe Experience Managerプラットフォーム内で使用する。 開発者が、従来のグラフィカルユーザーインターフェイスを使用するのではなく、API を使用してアクセスし、操作できるインタラクティブフォームを作成、公開、管理できるようにします。 <br/> <br/> これらのフォームは、従来のHTMLフォームインターフェイスを使用せずに送信できるように設計されています。 つまり、フロントエンドに表示可能なフォーム要素を必要とせずに、API またはバックエンドコードを介してプログラムを使用してフォームデータを送信できます。 <br/> <br/> ヘッドレスフォームは、シングルページアプリケーション、プログレッシブ Web アプリ、モバイルアプリケーションを構築する場合など、従来のHTMLフォームインターフェイスが必要でない場合や実用的でない場合に、様々なシナリオで役立ちます。 開発者が API やバックエンドコードを介して直接フォームデータを送信できるようにすることで、ヘッドレスフォームはワークフローを合理化し、Web アプリケーションの全体的なパフォーマンスを向上させます。|




>[!TAB コアコンポーネント]

||| |—|—| |![](https://experienceleague.corp.adobe.com/docs/experience-manager-cloud-service/assets/sample-core-components-based-adaptive-form.png?lang=en) | [アダプティブFormsコアコンポーネント](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html#features) は、Adobe Experience Manager WCM コアコンポーネントの基盤上に構築された、24 個のオープンソースの BEM 準拠コンポーネントのセットです。 これらは、アダプティブFormsの作成に使用するように特別に設計されています。アダプティブフォームとは、ユーザーのデバイス、ブラウザー、画面サイズに応じたフォームです。 <br/> <br/> これらのコンポーネントは、テキストフィールド、チェックボックス、ドロップダウンメニューなど、様々なフォームフィールドオプションを提供することで、例外的なデータ取得および登録エクスペリエンスを作成するために使用できます。 また、検証、条件付きロジック、レスポンシブデザインなどの機能も含まれ、使いやすく使いやすいフォームを作成するのに使用できます。 <br/> <br/>  さらに、これらのコンポーネントはオープンソースなので、開発者は、組織の特定のニーズに合わせてコンポーネントを簡単にカスタマイズおよび拡張できます。 また、これらのコンポーネントは、拡張性と保守性を確保する BEM 手法に基づいて構築されています。|



>[!TAB Microsoft PowerAutomate Connector &#x200B;]

||| |—|—| |![](https://powerusers.microsoft.com/t5/image/serverpage/image-id/182924i17C4BEA1C045D731/image-size/large/is-moderation-mode/true?v=1.0&amp;px=999)| AEM Forms Power Automate Connector を使用すると、Adobe Experience Manager(AEM)FormsをMicrosoft Power Automate( 旧称Microsoftフロー ) と統合できます。 Power Automate は、様々なアプリケーションやサービス間で自動ワークフローを作成できるクラウドベースのサービスです。  <br/> <br/> AEM Form Power Automate Connector を使用すると、アダプティブフォームの送信に基づいて自動的にトリガーを設定するワークフローを作成できます。 例えば、ユーザーがフォームを送信したときに電子メール通知を特定のユーザーに自動的に送信するワークフローや、ユーザーがフォームを完了したときにMicrosoft Planner でタスクを作成するワークフローを作成できます。  <br/> <br/> AEM Forms Power Automate Connector は、Microsoft Power Automate に接続する他のアプリケーションやサービスとアダプティブFormsを自動化および統合し、様々なツールを操作できる強力なツールです。 特定のニーズに合わせてワークフローを作成し、カスタムのアクション、条件およびトリガーを追加できます。 さらに、Power Automate は詳細な分析とレポート機能を提供し、時間の経過と共にワークフローを監視および最適化できます。|


>[!TAB Microsoft Storage Connectors:OneDrive と SharePoint]

||| |—|—| |![](/help/forms/assets/onedrive-and-sharepoint.jpg)|AEM Forms Microsoft Storage Connectors for OneDrive とSharePointは、Adobe Experience Manager(AEM)FormsをMicrosoft OneDrive およびSharePointと統合するためのコネクタです。 これらのコネクタを使用すると、Microsoftのクラウドベースのストレージソリューション内にAEM Formsのデータとドキュメントを保存および管理できます。 <br/> <br/> これらのコネクタを使用すると、Microsoft OneDrive 内にAEM Formsのデータとドキュメントを保存および管理できます。 このコネクタを使用すると、データファイルと添付ファイルをAEM Formsから直接 OneDrive とSharePointにアップロードできます。 <br/> <br/> AEM Forms Microsoft Storage Connectors for OneDrive およびSharePointを使用するには、いくつかのメリットがあります。 <ul><li> **統合**:これらのコネクタを使用すると、AEM FormsとMicrosoftのクラウドベースのストレージソリューションを統合し、これらのプラットフォームの機能を活用できます。 </li> <li> **共同作業**:OneDrive とSharePointは、チームメンバーがファイルやドキュメントを共同で作業できるようにするコラボレーションプラットフォームです。 AEM Formsをこれらのプラットフォームと統合することで、コラボレーションとチームワークを改善できます。 </li> <li> **セキュリティ**:OneDrive とSharePointは堅牢なセキュリティ機能を備え、データとドキュメントを安全に保存し、安全にアクセスできます。 </li> <br/> AEM Forms Microsoft Storage Connectors for OneDrive とSharePointは、Microsoftのクラウドベースのストレージソリューション内にAEM Formsのデータとドキュメントを保存および管理し、コラボレーションとセキュリティを向上させる強力なツールです。|


>[!ENDTABS]

<!--

| | |
|---|---|
| Adaptive Forms | Adaptive Forms allows businesses to create and manage interactive, data-driven forms for their websites and other digital channels responsive, mobile-friendly forms without. </br> </br> Adaptive Forms in AEM also include a drag-and-drop form builder, which enables non-technical users to easily create and customize forms using pre-built form components such as text boxes, dropdown menus, and date pickers. This enables faster form creation and eliminates the need for extensive coding and development. </br> </br> In addition, AEM Adaptive Forms offer several other features, including: <ul><li>Advanced workflows for routing, approval, and submission of form data Real-time validation and error checking to ensure data accuracy </li><li>Integration with third-party data sources and APIs for pre-filling form fields or validating data </li><li>Advanced analytics and reporting capabilities to track form usage, conversion rates, and other key metrics </li><li>Integration with Adobe Sign and DocuSign for e-signatures </li>|
| Automated Forms Conversion Service | Automated Forms Conversion Service allows businesses to convert legacy PDF-based forms into interactive, digital forms that can be easily managed and distributed online. The service helps: <ul><li>Save manual effort required to convert print forms to adaptive forms.</li><li>Applies patterns and appropriate validations during conversion</li><li>Generate Document of Record during conversion </li><li>Group commonly occurring fields into reusable form fragments </li> <li>Enables Adobe Analytics during conversion</li>|
| Communications API (Document Services) | Communications APIs are a set of RESTful APIs (Application Programming Interfaces) that enable businesses to automate the creation, management, and delivery of personalized, data-driven communications. </br> </br> These APIs also enable businesses to integrate their communications workflows with third-party systems and data sources, allowing them to create highly targeted and personalized messages that are triggered by specific events or user behaviors. Some key features of AEM Forms Communications APIs include:<ul><li> Dynamic content delivery: The APIs allow businesses to create and deliver dynamic content that is tailored to individual users based on their preferences, behaviors, and past interactions with the business.</li> <li>Personalized messaging: The APIs enable businesses to personalize their communications by including user-specific data such as names, addresses, and purchase history.</li><li>Integration with back-end systems: The APIs can be integrated with a wide range of back-end systems, including CRMs, databases, and marketing automation platforms.</li><li> Generate Pixel Perfect PDF documents: The APIs generate pixel-perfect PDF documents that are customized with user-specific data and content. This feature enables businesses to create highly professional and polished documents, such as invoices, contracts, and statements, that are delivered to users in PDF format.|
|Advanced Analytics| The service provides OOTB support to connect with Adobe Analytics. Connecting forms with Adobe Analytics provides several benefits for businesses, including: <ul><li> Improved understanding of user behavior: By connecting forms with Adobe Analytics, businesses can gain a deeper understanding of how users are interacting with their forms. This includes insights into user engagement, conversion rates, drop-off points, and other key metrics that can help businesses identify areas for improvement and optimize their forms for better user experiences. </li><li>Better targeting of marketing efforts: By analyzing user behavior on forms, businesses can gain valuable insights into user preferences and interests. This information can be used to better target marketing efforts and create more effective campaigns that drive engagement and conversions. </li><li> Reduced error rate: By integrating forms with Adobe Analytics, you can find insights about field with most errors and improve data quality, leading to better decision-making and more accurate insights. </li><li> Improved ROI: By optimizing forms based on insights gained from Adobe Analytics, businesses can improve conversion rates and drive more revenue from their digital channels. This can lead to a higher return on investment (ROI) for marketing and digital initiatives, helping businesses to achieve their goals and drive growth.</li>|

Adaptive Forms enable organizations to quickly design and deploy responsive, mobile-friendly forms without the need for extensive coding or development. With Adaptive Forms, businesses can create complex, multi-step forms with conditional logic, validations, and integrations with back-end systems such as CRMs and databases.

Adaptive Forms in AEM also include a drag-and-drop form builder, which enables non-technical users to easily create and customize forms using pre-built form components such as text boxes, dropdown menus, and date pickers. This enables faster form creation and eliminates the need for extensive coding and development.

In addition, AEM Adaptive Forms offer several other features, including:

Advanced workflows for routing, approval, and submission of form data
Real-time validation and error checking to ensure data accuracy
Integration with third-party data sources and APIs for pre-filling form fields or validating data
Advanced analytics and reporting capabilities to track form usage, conversion rates, and other key metrics
Overall, AEM Adaptive Forms provide businesses with a powerful tool for creating and managing complex, interactive forms that can be easily integrated into their digital experiences. |




| Feature/Capability | [!DNL AEM Forms] as a Cloud Service | AEM 6.5 Forms  | 
|---|---|---|
| Cloud-native architecture | &#x2611;  | &#x2612; |
| Auto-scaling based on load | &#x2611;  | &#x2612; |
| Zero downtime for upgrades | &#x2611;  | &#x2612; |
| Feature roll-out frequency | Agile*  | Quarterly |
| CDN (content delivery network) included | &#x2611;  | &#x2612; | 
| Topologies optimized for maximum resilience and efficiency| &#x2611;  | &#x2612; | 
| Cloud-native development environment | &#x2611;  | &#x2612; | 
| Self-Service via Cloud Manager | &#x2611;  | &#x2612; | 
| Automated upgrades with Continuous Integration and Continuous Delivery (CI/CD) | &#x2611;  | &#x2612; | 
| Adaptive Forms | &#x2611; | &#x2611; | 
| Data Integration with multiple data sources| &#x2611; | &#x2611; | 
| Communications APIs (Document Services) | &#x2611;* | &#x2611; | 
| Automated Forms Conversion Service | &#x2611; | &#x2611; | 
| Integration with [!DNL Micosoft Power Automate] | &#x2611; | &#x2612; | 
| Integration with [!DNL Adobe Sign] | &#x2611; | &#x2611; | 
| Integration with [!DNL AEM Sites] | &#x2611; | &#x2611; | 
| Integration with [!DNL Adobe Launch] | &#x2611; | &#x2611; | 
| Integration with [!DNL Adobe Analytics] | &#x2611; | &#x2611; | 
| Easy connectivity with Microsoft Dynamics and Salesforce | &#x2611; | &#x2612; |
| Custom submit action for with [!DNL DocuSign] | &#x2611; | &#x2612; | 
| Microsoft Azure data store connector | &#x2611; | &#x2612; |
| Hardened Rule editor | &#x2611; | &#x2612; | 
| Forms Portal | &#x2611; | &#x2611; | 
| AEM Workflows | &#x2611; | &#x2611; | 
| Document of Record | &#x2611; | &#x2611; | 
| Adaptive Forms Wizard | &#x2611; | &#x2612; | 
| Custom XCI for Document of Record| &#x2611; | &#x2612; |
| Invisible Captcha | &#x2611; | &#x2611; |
| Reusable Form Data Model configurations | &#x2611; | &#x2611; |
| Acroform-based Document of Record | &#x2611; | &#x2611; | 
| Government ID based identity authentication for Adobe Sign enabled Adaptive Forms | &#x2611; | &#x2611; | 
| Document Security | &#x2612; | &#x2611; |


* [Notable changes in comparison to AEM 6.5 Forms](notable-changes.md)
* [Frequently asked questions](faq.md)

-->