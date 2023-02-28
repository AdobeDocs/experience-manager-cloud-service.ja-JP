---
title: AEM 6.5 Forms と AEM Cloud Services の間での変更点
description: Experience Manager Forms のユーザーで、Adobe Experience Manager Forms as aCloud Service にアップグレードする予定ですか？Cloud Service にアップグレードまたは移行する前に、最も重要な変更点を説明します。
exl-id: 46fcc1b4-8fd5-40e1-b0fc-d2bc9df3802e
contentOwner: khsingh
source-git-commit: 2a464a0a11396a1948ba7211d5c0534769e6659c
workflow-type: tm+mt
source-wordcount: '1177'
ht-degree: 25%

---

# 既存のAdobe Experience Manager 6.5 Formsユーザーの主な変更点  {#notable-changes-for-existing-AEM-Forms-users}

Adobe Experience Manager Forms as a Cloud Serviceは、Adobe Experience Manager Formsオンプレミスおよび [!DNL Adobe-Managed Service] 環境。 主な違いを以下に示します。

| 機能/機能 | [!DNL AEM Forms] as a Cloud Service | AEM 6.5 Forms |
|---|---|---|
| クラウドネイティブなアーキテクチャ | ✅ | ⛌ |
| 負荷に基づく自動スケーリング | ✅ | ⛌ |
| アップグレードのダウンタイムなし | ✅ | ⛌ |
| 機能のロールアウト頻度 | アジャイル* | 毎四半期 |
| CDN（コンテンツ配信ネットワーク）を含む | ✅ | ⛌ |
| 耐障害性と効率性を最大限に高めるために最適化されたトポロジ | ✅ | ⛌ |
| クラウドネイティブ開発環境 | ✅ | ⛌ |
| Cloud Manager を介したセルフサービス | ✅ | ⛌ |
| 継続的統合および継続的配信 (CI/CD) による自動アップグレード | ✅ | ⛌ |
| [!DNL Micosoft Power Automate] との統合 | ✅ | ⛌ |
| [!DNL DocuSign] との統合 | ✅ | ⛌ |
| Microsoft Dynamics と Salesforce との簡単な接続 | ✅ | ⛌ |
| Microsoft Azure データストアとの簡単な接続 | ✅ | ⛌ |
| 堅牢化されたルールエディター | ✅ | ⛌ |
| フォーム作成ウィザード | ✅ | ⛌ |
| レコードのドキュメントのカスタム XCI のサポート | ✅ | ⛌ |
| アダプティブForms <sup>1</sup> | ✅ | ✅ |
| 通信 API(Document Services) <sup>2,3</sup> | ✅ | ✅ |
| automated forms conversionサービス <sup>4</sup> | ✅ | ✅ |
| Forms Portal <sup>5</sup> | ✅ | ✅ |
| Forms Data Model <sup>6</sup> | ✅ | ✅ |
| HTML5 Forms <sup>7</sup> | ⛌ | ✅ |
| Document Security | ⛌ | ✅ |

本サービスを進める前に、以下の例外事例を考慮してください。

+++ 1.アダプティブForms

* **XSD ベースのアダプティブForms:** このサービスは、HTML5 Forms (Mobile Forms) をサポートしていません。 XDP ベースのフォームをHTML5 Formsとしてレンダリングする場合、AEM 6.5 Forms上で引き続きこの機能を使用できます。 XDP-template を使用して、レコード用のドキュメントのテンプレートをデザインできます。 このサービスは、XFA ベースのアダプティブFormsをサポートしていません
* **アダプティブフォームテンプレートの読み込み：** ビルドパイプラインと、プログラムの対応する Git リポジトリを使用して、既存のアダプティブフォームテンプレートを読み込みます。
* **ルールエディター：** AEM Formsas a Cloud Service家は、堅固な [ルールエディター](rule-editor.md#visual-rule-editor). コードエディターは、Forms as a Cloud Serviceでは使用できません。 移行ユーティリティは、カスタムルール（コードエディターで作成）を持つフォームを移行する場合に役立ちます。 ユーティリティは、これらのルールを、Forms as a Cloud Serviceでサポートされるカスタム関数に変換します。 ルールエディタで再利用可能な関数を使用して、ルールスクリプトで取得した結果を引き続き取得できます。 `onSubmitError` または `onSubmitSuccess` 関数は、ルールエディターのアクションとして使用できるようになりました。
* **ドラフトと送信：** このサービスは、ドラフトおよび送信されたアダプティブFormsのメタデータを保持しません。
* **事前入力サービス：** デフォルトでは、事前入力サービスは、AEM 6.5 Formsでのサーバー上のデータの結合とは異なり、クライアント側でデータをアダプティブフォームに結合します。 この機能により、アダプティブフォームの事前入力に要する時間が短縮されます。 Adobe Experience Manager Forms Server で結合アクションを実行するようにをいつでも設定できます。
* **送信アクション：** この **メールをPDF** アクションは使用できません。 **メール**&#x200B;の送信アクションでは、添付ファイルを送信し、メールにレコードのドキュメント（DoR）を添付するオプションが提供されます。
* **コンポーネント**:このサービスは、フォーム内の署名機能をサポートしておらず、アダプティブFormsの概要コンポーネントと検証コンポーネントは含まれていません。



+++


+++ 2.ドキュメントサービス：ドキュメント操作 API（Assembler サービス）


このサービスは、他のサービスやアプリケーションに依存する操作をサポートしていません。

* ドキュメント形式以外のドキュメントをPDF形式に変換することはできません。 例えば、Microsoft Word からPDFへ、Microsoft Excel からPDFへ、およびPDFへのHTMLはサポートされていません。 ドキュメントが非PDF形式の場合。 Communications Document Manipulation API で使用する前に、PDF形式に変換してください。 例えば、ドキュメントがMicrosoft Office、HTML、PostScript(PS)、XDP 形式の場合、PDFドキュメントで使用する前に、これらのドキュメントをPDF形式に変換します。
* AdobeDistillerベースの変換はサポートされていません。 例えば、PostScript(PS) からPDF
* Forms Service-based Conversions はサポートされていません。 例えば、XDP からPDF forms。
* 署名付きPDFまたは透明PDFを別の形式に変換することはサポートされていません。
* Extensions Service を使用して使用権限をReaderすることはできません。
* このサービスでは、署名済みまたは透明なPDFドキュメントをPDF/A 形式に変換する機能は提供されません。

+++


+++ 3.ドキュメントサービス：ドキュメント生成 API（Output サービス）

1 回の API 呼び出しまたはバッチで、複数の DATA XML ファイルで使用できるテンプレートは 1 つだけです。 1 回の API 呼び出しで複数のデータファイルで複数のテンプレートを使用することはできません。

+++

+++ 4.Automated forms conversion業務

このサービスは、Automated forms conversionサービスのメタモデルを提供しません。 以下が可能です。 [automated forms conversionサービスドキュメントからダウンロード](https://experienceleague.adobe.com/docs/aem-forms-automated-conversion-service/using/extending-the-default-meta-model.html?lang=en#default-meta-model).

+++

+++ 5. Forms Portal

Forms Portal の匿名での使用は、標準ではサポートされていません (OOTB)。 Forms Portal をカスタマイズして、ログインしていないユーザー向けのフォームの表示を有効にすることができます。

+++

+++ 6.フォームデータモデル

* Formsデータモデルでは、データの送信に HTTP および HTTPs エンドポイントのみをサポートしています。 このサービスは、REST コネクタの相互 SSL および SOAP データソースの x509 証明書ベースの認証をサポートしていません。

* Formsas a Cloud Serviceでは、Microsoft Azure Blob、Microsoft Sharepoint、Microsoft OneDrive および一般的な CRUD（作成、読み取り、更新、削除）操作をサポートするサービスをデータストアとして使用できます。Open API 仕様 2.0 と Open API 仕様の両方がサポートされています。 また、このサービスは JDBC コネクタのサポートも提供します。

+++


+++ 7.HTML5Forms

* このサービスは、HTML5 Forms (Mobile Forms) をサポートしていません。 XDP ベースのフォームをHTML5 Formsとしてレンダリングする場合、AEM 6.5 Forms上で引き続きこの機能を使用できます。

* データをオフラインでキャプチャし、次回オンラインに戻る際に同期する使用例がある場合は、 [AEM Forms Workspace](https://experienceleague.adobe.com/docs/experience-manager-65/forms/use-aem-forms-workspace/introduction-html-workspace.html) AEM 6.5 Formsの機能

+++





+++ 8.開発環境

* クラウドネイティブの環境には、web コンソール（Configuration Manager）がありません。[[!DNL AEM Forms] as a Cloud Service SDK を使用して設定を生成](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/deploying/configuring-osgi.html?lang=ja#generating-osgi-configurations-using-the-aem-sdk-quickstart)し、Cloud Service インスタンスに[設定をデプロイ](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/deploy-code.html?lang=ja#deployment-process)するための CI／CD パイプラインを生成できます。
* メールは、デフォルトでは HTTP プロトコルおよび HTTPs プロトコルのみをサポートします。[サポートチームに問い合わせて](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/developing/development-guidelines.html?lang=ja#sending-email)、メールの送信用のポートと、環境用の SMTP プロトコルを有効にします。
* 署名付きPDFまたは透明PDFを別の形式に変換することはサポートされていません。 Forms as a Cloud Serviceで顧客バンドルを使用する前に、ローカライズされた Adaptive Formsの最新バージョンの adobe-aemfd-docmanager* URL 規則を使用してカスタムコードを再コンパイルし、URL でロケールを指定できるようになりました。 新しい URL 規則により、ローカライズされたフォームを Dispatcher または CDN にキャッシュできます。Cloud Service 環境では、`http://host:port/content/forms/af/afName.html?afAcceptLang=<locale>` の代わりに `http://host:port/content/forms/af/<afName>.<locale>.html` の URL 形式を使用して、アダプティブフォームのローカライズ版をリクエストします。アドビでは、Dispatcher または CDN キャッシュを使用することをお勧めします。これにより、事前入力されたフォームのレンダリング速度が向上します
* Adobe Experience Manager Forms a Cloud Service は、AEM プロジェクトに様々な新機能と可能性を提供します。ただし、AEM Cloud Service との互換性を保つためには、Adobe Experience Manager Maven プロジェクトにいくつかの変更が必要です。上位レベルでは、AEM は可変コンテンツと不変コンテンツの分割を考慮してコンテンツとコードを個別のサブパッケージに分離する必要があります。[Repository Modernizer](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/refactoring-tools/repo-modernizer.html?lang=ja) ツールを使用して、Adobe Experience Manager as a Cloud Service 向けに定義されているプロジェクト構造と互換性を持たせるために、コンテンツとコードを個別のパッケージに分離して、既存のプロジェクトパッケージを再構築します。


+++

<!-- 

### HTML5 Forms (Mobile Forms)

The service does not support HTML5 Forms (Mobile Forms). If you render your XDP-based forms as HTML5 Forms, you can continue using the feature on AEM 6.5 Forms.

### Adaptive Forms 

* **XSD-Based Adaptive Forms:** The service does not support HTML5 Forms (Mobile Forms). If you render your XDP-based forms as HTML5 Forms, you can continue using the feature on AEM 6.5 Forms. You can use XDP-template to design a template for Document for Record. The service does not support XFA based Adaptive Forms  
* **Importing Adaptive Form templates:** Use build pipeline and corresponding Git repository of your program to import existing Adaptive Form templates. 
*  **Rule editor:** AEM Forms as a Cloud Service provides a hardened [Rule editor](rule-editor.md#visual-rule-editor). The code editor is not available on Forms as a Cloud Service. The migration utility helps you migrate your forms that have custom rules (created in code editor). The utility converts such rules into custom functions supported on Forms as a Cloud Service. You can use the reusable functions with Rule editor to continue obtaining results obtained with rule scripts  The `onSubmitError` or `onSubmitSuccess` functions are now available as actions the Rule Editor.  
* **Drafts and submissions:** The service does not retain metadata for drafts and submitted Adaptive Forms.  
* **Prefill Service:** By default, the prefill service merges data with an Adaptive Form at client as opposed to merging data on Server in AEM 6.5 Forms. The feature helps improve the time required to prefill an Adaptive Form. You can always configure to run the merge action on the Adobe Experience Manager Forms Server. 
* **Submit actions:** The **Email as PDF** action is not available. The **Email** submit action provide options to send attachments and attach Document of Record (DoR) with email. 
* **Components**:  The service does not support in-form signing experience and does not include the Summary and Verify components for Adaptive Forms.  
* **Forms portal**: Support for anonymous use of Forms portal is not available out of the box (OOTB). You can customize the forms portal to enable displaying forms for non-logged in users.

### Form Data Model

* Forms data model supports only HTTP and HTTPs endpoints to submit data. The service does not support Mutual SSL for REST connector and x509 certificate-based authentication for SOAP data sources. * Forms as a Cloud Service allows to use Microsoft Azure Blob, Microsoft Sharepoint, Microsoft OneDrive, and services supporting general CRUD (Create, Read, Update, and Delete) operations as data stores, both Open API specification 2.0 and Open API specification are supported. The service also provides support for JDBC connector.


### Automated Forms Conversion Service     

The service does not provide meta-model for Automated Forms Conversion Service. You can [download it from Automated Forms Conversion Service documentation](https://experienceleague.adobe.com/docs/aem-forms-automated-conversion-service/using/extending-the-default-meta-model.html?lang=en#default-meta-model).


### Configurations

* Email support only HTTP and HTTPs protocols, by default. [Contact the support team](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/developing/development-guidelines.html#sending-email) to enable ports for sending emails and to enable SMTP protocol for your environment.  
* If you use custom bundles, recompile your code with latest version of adobe-aemfd-docmanager before using these bundles with Forms as a Cloud Service. 


### Document Services: Document Manipulation APIs (Assembler Service)

The service does not support operations dependent on other services or applications:  

* Conversion of documents in a non-PDF format to a PDF format is not supported. For example, Microsoft Word to PDF, Microsoft Excel to PDF, and HTML to PDF are not supported. If your documents are in a non-PDF format. Convert such documents to PDF format before using those with Communications Document Manipulation APIs. For example, if your documents are in Microsoft Office, HTML, PostScript (PS), XDP format, convert these documents to PDF format before using those with PDF documents. 
* Adobe Distiller-based conversions are not supported. For example, PostScript(PS) to PDF
* Forms Service-based conversions are not supported. For example, XDP to PDF Forms.
* The service does not support converting a Signed PDF or Transparent PDF to another PDF format.
* Applying usage rights using Reader Extensions Service is not available. 
* The service does not provide the ability to convert signed or transparent PDF Documents to PDF/A format. 

### Document Services: Document Generation APIs (Output Service)

* In a single API call or batch, you can use one template with multiple DATA XML files. Using mutiple templates with multiple data files in a single API call is not supported. 

### Other differences

* A cloud-native environment does not have web console (configuration manager). You can use [[!DNL AEM Forms] as a Cloud Service SDK to generate configurations](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/deploying/configuring-osgi.html?lang=en#generating-osgi-configurations-using-the-aem-sdk-quickstart) and CI/CD pipeline to [deploy the configuration](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/deploy-code.html?lang=en#deployment-process) to your Cloud Service instance.
* Email support only HTTP and HTTPs protocols, by default. [Contact the support team](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/developing/development-guidelines.html#sending-email) to enable ports for sending emails and to enable SMTP protocol for your environment.
* The service does not support converting a Signed PDF or Transparent PDF to another PDF format.* Before using your customer bundles with Forms as a Cloud Service, recompile your custom code with the latest version of adobe-aemfd-docmanager* URL convention of localized Adaptive Forms now supports specifying a locale in the URL. New URL convention enables caching localized forms on a Dispatcher or CDN. On Cloud Service environment, use the URL format `http://host:port/content/forms/af/<afName>.<locale>.html` to request a localized version of an Adaptive Form instead of `http://host:port/content/forms/af/afName.html?afAcceptLang=<locale>`. Adobe recommends using Dispatcher or CDN caching. It helps improve rendering speed of prefilled forms 
* Adobe Experience Manager Forms as a Cloud Service brings many new features and possibilities into your AEM Projects. However, there are some changes required to Adobe Experience Manager Maven projects to be compatible with AEM Cloud Service. At a high-level, AEM requires a separation of content and code into discrete subpackages to respect the split between mutable and immutable content. Use the [Repository Modernizer](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/refactoring-tools/repo-modernizer.html) tool to restructure existing project packages by separating content and code into discrete packages to be compatible with the project structure defined for Adobe Experience Manager as a Cloud Service.
-->




