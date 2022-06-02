---
title: Experience Manager [!DNL AEM Forms] as a Cloud Service のアーキテクチャ
description: ' [!DNL AEM Forms] a s a Cloud Service のアーキテクチャを理解し、プラットフォームの拡張性、回復性、パフォーマンスの側面について学習します。'
source-git-commit: cb7b417b9b4898b0656e79d6f699e8d5cd611e76
workflow-type: tm+mt
source-wordcount: '1049'
ht-degree: 25%

---


# [!DNL AEM] Formsas a Cloud Serviceアーキテクチャ {#architecture}

[!DNL Adobe Experience Manager Forms] as a Cloud Serviceは、複雑なデジタルフォームや通信を作成、管理、公開、更新し、送信したデータをバックエンドのプロセスやビジネスルールと統合し、外部データストアにデータを保存する、クラウドネイティブなソリューションです。 広がる [!DNL Adobe Experience Manager as a Cloud Service]. 拡張、導入、環境、その他のインフラストラクチャについて詳しくは、 [のアーキテクチャの概要 [!DNL Adobe Experience Manager as a Cloud Service]](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/core-concepts/architecture.html?lang=ja).

AEM Forms as a Cloud Serviceは、主に次の 2 つの使用例をサポートしています。デジタル登録と顧客コミュニケーション。 次の図は、両方の使用例のアーキテクチャを示しています。

## アーキテクチャ図とフロー図

**Forms Digital Enrollment**

![Forms — デジタル登録](assets/forms-cloud-service-architecture-forms-digital-enrollment.svg)

**Forms Communications**

![Forms-Communication](assets/forms-cloud-service-architecture-forms-communications.svg)

## コンポーネント

Forms as a Cloud Serviceは、複数のコンポーネントで構成されます。

### CDN（コンテンツ配信ネットワーク）

すべてのAEM Formsas a Cloud Serviceプログラムは、 [組み込み CDN サービス](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/content-delivery/cdn.html). これは、Forms as aCloud Servicesのライセンスに含まれます。

### 作成者

オーサーとは、標準のオーサー実行モードで動作するAEM Formsas a Cloud Serviceインスタンスです。 このサービスは、内部のユーザー、フォームデザイナー、開発者を対象としています。 オーサー環境では、次の機能を有効にします。

* フォームの作成と管理。
* automated forms conversionサービスに接続して、PDFまたは XDP フォームをアダプティブフォームに変換する。
* Forms中心のワークフローの作成と実行
* アダプティブフォームのアセットの管理
* 通信アセットの管理
* ブランド指向のパーソナライズされた通信を作成、組み立て、配信するための Synchronous RESTful API（リアルタイム API）と Batch API。
* 同期 API を使用して、同期ドキュメントを組み合わせ、並べ替え、PDFします。

### 公開

パブリッシュインスタンスは、標準のパブリッシュ実行モードで実行されるAEM Formsas a Cloud Serviceです。 パブリッシュインスタンスは、フォームベースのアプリケーションを使用するエンドユーザー向けのインスタンスです。例えば、公開 web サイトにアクセスしてフォームを送信するユーザーなどが、このインスタンスを使用します。次の機能が有効になります。

* エンドユーザー向けのフォームのレンダリングと送信。
* 送信済みのフォームデータを送信し、最終的な記録システムでさらに処理および保存する。
* お客様が管理するストレージに接続してデータを保存します。
* Adobe Signと接続して、アダプティブフォームの送信レコードに E 署名する。
* ブランド指向のパーソナライズされたコミュニケーションを作成、組み立て、提供する API を同期します。
* 同期 API を使用して、同期ドキュメントを組み合わせ、並べ替え、PDFします。

リバースレプリケーションは、AEM as a Cloud Serviceでは、コンテンツ/データをパブリッシュサービスからオーサーサービスに送信するために使用できません。 ただし、パブリッシュ環境で実行しているアダプティブFormsを、オーサー環境のワークフローにデータを送信するように設定することはできます（ワークフローはオーサー環境でのみ実行できます）。 これは、承認の使用例で役立ちます。

#### Dispatcher

[Dispatcher](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/content-delivery/disp-overview.html) は、Adobe Experience Managerのキャッシュやロードバランシングを行うツールで、エンタープライズクラスの Web サーバーと共に使用できます。

### Adobe サービス

**automated forms conversionサービス**

[automated forms conversionサービス](https://experienceleague.adobe.com/docs/aem-forms-automated-conversion-service/using/introduction.html?lang=ja) は、PDFおよび XFA フォームを、デバイスに対応した、レスポンシブでHTML5 ベースのアダプティブフォームに自動的に変換します。

**Adobe Sign**

Adobe Signは、ユーザーがブラウザーまたはモバイルデバイスを使用して署名プロセスの送信、署名、トラッキング、管理をおこなえる、クラウドベースの e 署名サービスです。 Adobe Signをアダプティブフォームと統合して、署名ワークフローを自動化し、単一および複数の署名プロセスを簡略化し、アダプティブフォームに電子署名を行うことができます。

<!-- **PDF Service API**
Adobe’s PDF Services API lets create, combine, export, and extract data from PDFs through powerful and flexible cloud-based APIs. -->

### お客様が管理するストレージ

Forms as a Cloud Serviceには、BLOB ストア、データベース、ストレージサービスなど、外部ストレージシステムにコンテンツを保存するオプションが用意されています。 また、顧客が管理するリポジトリに、機密の個人データ (SPD) 要素を含むインプロセスワークフローデータ (AEM Workflow Variables データ ) を格納して、安全に処理することもできます。 Adobeでは、機密データをお客様が管理するストレージにのみ保存することをお勧めします。

以下を使用して、 **統合ストレージコネクタ** BLOB ストレージに接続し、 **フォームデータモデル** データベースまたはバックエンドサービス（RESTful、SOAP、Azure Blob Storage など）に接続する場合。

### ドキュメントサービス

ドキュメントサービスは、次の要素で構成されます。

* **出力サービス（通信 — ドキュメント生成 API）** は、ビジネス通信、声明書、請求処理レター、特典通知、月額請求、ウェルカムキットなど、ブランド承認、パーソナライズ、標準化されたドキュメントを作成するのに役立ちます。

* **Assembler サービス（通信 — ドキュメント操作 API）** は、PDFドキュメントの組み合わせ、並べ替え、検証に役立ちます。

* **レコードのドキュメント (DoR) サービス** は、レコードのドキュメント (DoR) を生成するのに役立ちます。 このサービスは、Formsas a Cloud Serviceのオーサーインスタンスとパブリッシュインスタンスから別々のポッドで実行されます。 これにより、パフォーマンスが向上し、負荷に応じて個別にポッドをスケーリングできます。

### Cloud Manager 

Cloud Manager は、[AEM as a Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/overview/introduction.html) にとって不可欠なコンポーネントです。これは、お客様の運用および開発者のペルソナのための単一のエントリポイントです。 AEM のプログラムと環境を管理できる場所です。Cloud Manager は、AEM as a Cloud Service の主要コンポーネントを作成および設定できるセルフサービスポータルとして進化しました。

* プログラムの作成と管理
* プログラム内での AEM 環境の作成と管理
* 顧客コードと設定を特定の環境にデプロイするためのパイプラインの作成と管理
* これらのコンポーネントに関する重要なライフサイクルイベント（製品のアップデートなど）の通知の取得 Cloud Manager について詳しくは、 [AdobeCloud Manager について](https://experienceleague.adobe.com/docs/experience-manager-learn/foundation/cloud-manager/understand-cloud-manager-for-aem.html?lang=ja) および [Cloud Manager の概要](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/introduction-to-cloud-manager.html?lang=ja).

### デベロッパーコンソール

開発者コンソールには、Forms as a Cloud Service 環境が実行されているそれぞれの詳細が表示されます。 これらの詳細は、環境のデバッグに役立ちます。 詳しくは、 [開発者コンソールでas a Cloud ServiceしたAEMのデバッグ](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/debugging/debugging-aem-as-a-cloud-service/developer-console.html?lang=ja).

<!--

+++CDN (Content Delivery Network):

Every AEM Forms as a Cloud Service program has access to Fastly CDN service. It is included in the licence of Forms as a Cloud Services.

+++

+++Adaptive Forms
Adaptive Forms enable customers to author web-friendly reflowable web forms and fragments that are used by the customers for their data capture needs. This feature enables customers to manage their complex data capture needs easily, by leveraging multiple integrations with Adobe Sign, Document Services, Form Data Model, Automated Forms Conversion service, and more.

+++

+++Automated Forms Conversion Service (AFCS)
Automated Forms Conversion service helps accelerate digitization and modernization of data capture experience through automated conversion of PDF forms to adaptive forms. The service, powered by Adobe Sensei, automatically converts your PDF forms to device-friendly, responsive, and HTML5-based adaptive forms. While leveraging the existing investments in PDF Forms and XFA, the service also applies appropriate validations, styling, and layout to adaptive form fields during conversion.

+++

+++Form Data Model
The Form Data Model (FDM) feature is the standard way of creating data integrations with external/internal data sources and using them across the different Forms as a Cloud Service features. FDM provides a rich editor for customers to integrate, define, and manage relationships between the different entities and data sources and perform operations on them. Form data is stored in a data store hosted on the customer premises. Organizations can also use blob store hosted by the cloud provider and Adobe Experince Platform to store data.

+++

+++Forms Workflows
Forms-centric workflows is an extension to the default AEM Workflow and provides our customers with additional workflow capabilities like Form Data review, task assignment, and document services invocation.

+++

+++Communications
Forms as a Cloud Service offering consists of multiple services tailored specifically for document processing.

+++

+++Document of Record
A Document of Record is a PDF version of a form. It provides an ability to keep a record of the information  that you provide and submit in an Adaptive Form in PDF fromat. The service provides a default DoR template and tools to develop a custom template.

+++

## Terminologies

<!-- ## Cloud Manager{#cloud-manager}

Cloud Manager is an essential component to [AEM as a Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/overview/introduction.html?lang=en). Each new tenant of the [!DNL AEM Forms] as a Cloud Service is first provisioned for Cloud Manager access. Cloud Manager is the single-entry point for the operations and developer persona of our customers. It is the place from where the AEM programs and environments can be managed. Cloud Manager has evolved as a self-service portal where the main components of the AEM as a Cloud Service can be created and configured:

* Creating and managing programs
* Creating and managing the AEM environments within the programs
* Creating and managing the pipelines for deploying the customer code and configuration to a particular environment
* Getting notified of important lifecycle events for these components (e.g. product updates)
For more information about Cloud Manager, see [Understand Adobe Cloud Manager](https://experienceleague.adobe.com/docs/experience-manager-learn/foundation/cloud-manager/understand-cloud-manager-for-aem.html) and [Introduction to Cloud Manager](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/introduction-to-cloud-manager.html).

## Users and Authentication {#users-and-authentication}

AEM as a Cloud Service includes Admin Console support for AEM instances and Adobe Identity Management System (IMS) based authentication. The Admin Console allows administrators to centrally manage all Experience Cloud users. Users and Groups can be assigned to product profiles associated with AEM as a Cloud Service instances, allowing them to log in to that instance. For more information about users, authentication, and, and accessing an instance of AEM as a Cloud Service, see [IMS Support for [!DNL Adobe Experience Manager] as a Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/security/ims-support.html?lang=en#introduction).

Various personas are involved in a typical [!DNL AEM Forms] project. After you log in to your [!DNL AEM Forms] as a Cloud Service instance, you can [add users in admin console](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/security/ims-support.html) for personas applicable to your organization or project and [assign users to built-in groups](forms-groups-privileges-tasks.md) to provide them required privileges.

To learn various in-built [!DNL AEM Forms] specific user groups and privileges available on [!DNL AEM Forms] as a Cloud Services instance, see [Configure, user, roles and groups](forms-groups-privileges-tasks.md). 

## Developer Experience {#developer-experience}

The new architecture supporting AEM as a Cloud Service brings some key changes to the overall developer experience. One of the major goals for the changes to developer experience is to allow migration to AEM as a Cloud Service as quickly as possible, with little modifications to existing custom code.

## Cloud development {#cloud-development}

Here are the guidelines to run your existing code smoothly on AEM as a Cloud Service environment:

* Store your code and configurations to the Git repository of the associated Cloud Manager program. It makes managing and integrating code with CI/CD a breeze.  
* Make application code and configuration compatible with the baseline [!DNL AEM Forms] images. Using the latest APIs helps to build faster and secure applications.
* Use the Cloud Manager pipeline associated with the Cloud Manager environment to build and deploy applications. It helps you bring the latest features and bug fixed for [!DNL AEM Forms] as a Cloud Service to your environment.
* Try that your custom applications pass all the code quality, security, and performance gates enforced in the pipeline. It helps build secure and better performing applications which leads to better customer experience. You can always use Cloud Manager UI to skip some checks.
This process is commonly referred to as cloud-first development. [!DNL AEM Forms] as a Cloud Service also provides an SDK to support rapid development before the pending code and configuration changes are attempted in the cloud.
Some interfaces that were previously part of the AEM QuickStart are no longer available to the users of the AEM as a Cloud Service environment. For instance, the Web Console where OSGI bundles and their associated configuration are managed. The CRXDE Lite content repository browser becomes only accessible on non-production environment types. A subset of the Web Console functionalities that developers require, especially when it comes to diagnostics and status purposes, is made available via a new developer console.
Also, one of the most common requirements for developers is quick access to the log files of the various environments. With [!DNL AEM Cloud Service], the log files of the different nodes in the Author, Publish are made available via the Cloud Manager, either in the form of files that can be downloaded or via APIs for tailing the logs. Due to the clear separation of code and content, developers can leverage a particular process for updating content as part of a deployment. The typical use cases for mutable content are:
* Standard “default” content that is part of the customer project (e.g. folders, templates, workflows...)
* Search index definitions
* ACLs and permissions
* Service users and user groups
Set up your development environment, [Configure your CI/CD Pipeline](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/how-to-use/configuring-pipeline.html), and learn to [deploy your code](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/how-to-use/deploying-code.html) on the environment. -->

### アダプティブフォームオーサリング {#local-development}

[!DNL AEM Forms] as a Cloud Service 環境を設定する場合は、開発環境、ステージング環境および実稼動環境を設定します。さらに、迅速な反復と開発を行うために、ローカル開発環境を設定します。AEM SDK と [!DNL AEM Forms] アドオン機能アーカイブをダウンロードして設定し、ローカルの [!DNL Forms] as a Cloud Service 開発環境を設定できます。手順について詳しくは、[ローカル開発環境の設定](setup-local-development-environment.md)を参照してください。

## デバッグ {#debugging}

AEM as a Cloud Service は、セルフサービスのスケーラブルなクラウドインフラストラクチャ上で実行します。ビルドやデプロイから、実行中のAEMアプリケーションの詳細の取得に至るまで、AEM開発者はAEMの様々なファセットを理解し、デバッグする必要があります。 詳しくは、[AEM as a Cloud Service のデバッグ](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/debugging/debugging-aem-as-a-cloud-service/overview.html)を参照してください。
