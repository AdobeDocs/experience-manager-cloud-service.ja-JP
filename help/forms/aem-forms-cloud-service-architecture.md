---
title: アダプティブフォームおよび通信 API 用の AEM Forms as a Cloud Service アーキテクチャ
description: ' [!DNL AEM Forms]  as a Cloud Service のアーキテクチャを理解し、プラットフォームの拡張性、回復性、パフォーマンスの側面について学習します。'
role: Admin, Developer, User
feature: Adaptive Forms
exl-id: 9d677bee-50ca-460e-b503-6b7799900735
source-git-commit: 8f39bffd07e3b4e88bfa200fec51572e952ac837
workflow-type: tm+mt
source-wordcount: '1097'
ht-degree: 94%

---

# [!DNL AEM] Forms as a Cloud Service のアーキテクチャ {#architecture}

| バージョン | 記事リンク |
| -------- | ---------------------------- |
| AEM 6.5 | [ここをクリックしてください](https://experienceleague.adobe.com/docs/experience-manager-65/forms/install-aem-forms/jee-installation/aem-forms-jee-supported-platforms.html?lang=ja) |
| AEM as a Cloud Service | この記事 |

[!DNL Adobe Experience Manager Forms] as a Cloud Service は、企業が複雑なデジタルフォームやコミュニケーションを作成、管理、公開、更新しながら、送信データをバックエンドプロセスやビジネスルールと統合しデータを外部データストアに保存するためのクラウドネイティブなソリューションです。[!DNL Adobe Experience Manager as a Cloud Service] を拡張するものです。スケーリング、デプロイメント、環境などのインフラストラクチャについて詳しくは、[&#x200B; [!DNL Adobe Experience Manager as a Cloud Service] のアーキテクチャの概要](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/core-concepts/architecture.html?lang=ja)を参照してください。

AEM Forms as a Cloud Service では、デジタル登録とカスタマーコミュニケーションの 2 つの主要なユースケースをサポートしています。次の図は、両方のユースケースでのアーキテクチャを示しています。

## Forms デジタル登録

![Forms - デジタル登録](assets/forms-cloud-service-architecture-forms-digital-enrollment.svg)

## Forms コミュニケーション

![Forms - コミュニケーション](assets/forms-cloud-service-architecture-forms-communications.svg)

## 適用性とユースケース

### 保険

## AEM Formsは大規模な保険業務を処理できますか？

はい。Adobe Managed Servicesまたはプライベートクラウドのレコメンデーションアーキテクチャを使用してAEM Formsをデプロイすると、大量のフォーム送信と企業規模のワークロードがサポートされます。

## AEM Formsは保険データに対して安全ですか？

はい。AEM Formsは、安全なデータ転送、制御されたアクセス、エンタープライズ認証メカニズムをサポートしており、機密性の高い保険データの処理に適しています。

## コンポーネント

Forms as a Cloud Service は複数のコンポーネントで構成されています。

### CDN（コンテンツ配信ネットワーク）

すべての AEM Forms as a Cloud Service プログラムは、[ビルトイン CDN サービス](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/content-delivery/cdn.html?lang=ja)にアクセスできます。これは、Forms as a Cloud Service のライセンスに含まれています。

### オーサー

オーサーとは、標準のオーサー実行モードで動作する AEM Forms as a Cloud Service インスタンスです。このインスタンスは、内部ユーザー、フォームデザイナーおよび開発者が使用するためのものです。オーサー環境では、次の機能が有効です。

* フォームのオーサリングと管理
* 自動フォーム変換サービスへの接続による PDF または XDP フォームからアダプティブフォームへの変換
* Forms 中心のワークフローの作成と実行
* アダプティブフォームアセットの管理
* コミュニケーションアセットの管理
* ブランド指向のパーソナライズされたコミュニケーションを作成、組み立て、配信するための同期 RESTful API（リアルタイム API）とバッチ API
* PDF ドキュメントを結合、並べ替え、検証するための同期 API

### パブリッシュ

パブリッシュインスタンスとは、標準のパブリッシュ実行モードで動作する AEM Forms as a Cloud Service インスタンスです。パブリッシュインスタンスは、フォームベースのアプリケーションを使用するエンドユーザー向けのインスタンスです。例えば、公開 web サイトにアクセスしてフォームを送信するユーザーなどが、このインスタンスを使用します。次の機能が有効になります。

* エンドユーザー向けのフォームのレンダリングと送信
* 送信済みフォームの未加工データを転送してさらに処理を行い、最終的な記録システムに保存する機能
* 顧客側で管理されるストレージへの接続によるデータの保存
* Adobe Sign との接続によるアダプティブフォーム送信レコードへの電子サイン
* ブランド指向のパーソナライズされたコミュニケーションを作成、組み立て、配信するための同期 API
* PDF ドキュメントを結合、並べ替え、検証するための同期 API

リバースレプリケーションは、AEM as a Cloud Service では、コンテンツ／データをパブリッシュサービスからオーサーサービスに送信するために使用できません。ただし、パブリッシュで動作しているアダプティブフォームを、オーサー上のワークフローにデータを送信するように設定することはできます（ワークフローはオーサー上でのみ実行できます）。これは、承認ユースケースで役に立ちます。

#### Dispatcher

[Dispatcher](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/content-delivery/disp-overview.html?lang=ja) は、Adobe Experience Manager のキャッシュや負荷分散を利用するツールで、エンタープライズクラスの web サーバーと組み合わせて使用できます。

### Adobe Services

**自動フォーム変換サービス**

[自動フォーム変換サービス](https://experienceleague.adobe.com/docs/aem-forms-automated-conversion-service/using/introduction.html?lang=ja)は、PDF および XFA フォームを、使用しているデバイスに合わせて、HTML5 ベースのレスポンシブなアダプティブフォームに自動的に変換します。

**Adobe Sign**

Adobe Sign は、ユーザーがブラウザーまたはモバイルデバイスを使用して署名プロセスを送信、署名、追跡、管理できる、クラウドベースの電子サインサービスです。Adobe Sign をアダプティブフォームと統合して、署名ワークフローの自動化、単一および複数の署名プロセスの簡略化、アダプティブフォームへの電子サインを行うことができます。

<!-- **PDF Service API**
Adobe’s PDF Services API lets create, combine, export, and extract data from PDFs through powerful and flexible cloud-based APIs. -->

### 顧客側で管理されるストレージ

Forms as a Cloud Service には、BLOB ストア、データベース、ストレージサービスなどの外部ストレージシステムにコンテンツを保存するオプションが用意されています。また、機密性の高い個人データ（SPD）要素を含んだ処理中のワークフローデータ（AEM ワークフロー変数データ）を、顧客側で管理されるリポジトリーに保存して安全に処理することもできます。アドビでは、お客様が管理するストレージにのみ機密データを保存することをお勧めします。

**統合ストレージコネクタ**&#x200B;を使用して BLOB ストレージに接続したり、**フォームデータモデル（FDM）**&#x200B;を使用してデータベースまたはバックエンドサービス（RESTful、SOAP、Azure Blob Storage など）に接続したりすることができます。

### ドキュメントサービス

ドキュメントサービスは、次の要素で構成されます。

* **Output サービス（通信 - ドキュメント生成 API）**&#x200B;は、ビジネス文書、ステートメント、請求処理レター、特典通知、毎月の請求書、ウェルカムキットなど、ブランド承認済みのパーソナライズされた標準的なドキュメントを作成するのに役立ちます。

* **アセンブラーサービス（通信 - ドキュメント操作 API）**&#x200B;は、PDF ドキュメントの結合、並べ替えおよび検証に役立ちます。

* **DoR（レコードのドキュメント）サービス**&#x200B;は、DoR（レコードのドキュメント）を生成するのに役立ちます。このサービスは、Forms as a Cloud Service のオーサーインスタンスやパブリッシュインスタンスとは別の独自のポッドで動作します。これにより、パフォーマンスが向上し、負荷に応じて個別にポッドをスケーリングできます。

### Cloud Manager 

Cloud Manager は、[AEM as a Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/overview/introduction.html?lang=ja) にとって不可欠なコンポーネントです。お客様の運用および開発者ペルソナのための単一のエントリーポイントになります。AEM のプログラムと環境を管理できる場所です。Cloud Manager は、AEM as a Cloud Service の主要コンポーネントを作成および設定できるセルフサービスポータルとして進化しました。

* プログラムの作成と管理
* プログラム内での AEM 環境の作成と管理
* 顧客コードと設定を特定の環境にデプロイするためのパイプラインの作成と管理
* これらのコンポーネントに関する重要なライフサイクルイベント（例えば、更新など）の通知
Cloud Manager について詳しくは、[Adobe Cloud Manager について](https://experienceleague.adobe.com/docs/experience-manager-learn/foundation/cloud-manager/understand-cloud-manager-for-aem.html?lang=ja)および [Cloud Manager の概要](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/introduction-to-cloud-manager.html?lang=ja)を参照してください。

### デベロッパーコンソール

開発者コンソールには、実行中の各 Forms as a Cloud Service 環境の様々な詳細が表示されます。これらの詳細は、環境のデバッグに役立ちます。詳しくは、[開発者コンソールでの AEM as a Cloud Service のデバッグ](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/debugging/debugging-aem-as-a-cloud-service/developer-console.html?lang=ja)を参照してください。

<!--

+++CDN (Content Delivery Network):

Every AEM Forms as a Cloud Service program has access to Fastly CDN service. It is included in the licence of Forms as a Cloud Services.

+++

+++Adaptive Forms
Adaptive Forms enable customers to author web-friendly reflowable web forms and fragments that are used by the customers for their data capture needs. This feature enables customers to manage their complex data capture needs easily, by using multiple integrations with Adobe Sign, Document Services, Form Data Model (FDM), Automated Forms Conversion service, and more.

+++

+++Automated Forms Conversion Service (AFCS)
Automated Forms Conversion service helps accelerate digitization and modernization of data capture experience through automated conversion of PDF forms to adaptive forms. The service, powered by Adobe Sensei, automatically converts your PDF forms to device-friendly, responsive, and HTML5-based adaptive forms. While using the existing investments in PDF Forms and XFA, the service also applies appropriate validations, styling, and layout to adaptive form fields during conversion.

+++

+++Form Data Model (FDM)
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

Cloud Manager is an essential component to [AEM as a Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/overview/introduction.html?lang=ja). Each new tenant of the [!DNL AEM Forms] as a Cloud Service is first provisioned for Cloud Manager access. Cloud Manager is the single-entry point for the operations and developer persona of our customers. It is the place from where the AEM programs and environments can be managed. Cloud Manager has evolved as a self-service portal where the main components of the AEM as a Cloud Service can be created and configured:

* Creating and managing programs
* Creating and managing the AEM environments within the programs
* Creating and managing the pipelines for deploying the customer code and configuration to a particular environment
* Getting notified of important lifecycle events for these components (for example, product updates)
For more information about Cloud Manager, see [Understand Adobe Cloud Manager](https://experienceleague.adobe.com/docs/experience-manager-learn/foundation/cloud-manager/understand-cloud-manager-for-aem.html?lang=ja) and [Introduction to Cloud Manager](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/introduction-to-cloud-manager.html?lang=ja).

## Users and Authentication {#users-and-authentication}

AEM as a Cloud Service includes Admin Console support for AEM instances and Adobe Identity Management System (IMS) based authentication. The Admin Console allows administrators to centrally manage all Experience Cloud users. Users and Groups can be assigned to product profiles associated with AEM as a Cloud Service instances, allowing them to log in to that instance. For more information about users, authentication, and, and accessing an instance of AEM as a Cloud Service, see [IMS Support for [!DNL Adobe Experience Manager] as a Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/security/ims-support.html?lang=ja#introduction).

Various personas are involved in a typical [!DNL AEM Forms] project. After you log in to your [!DNL AEM Forms] as a Cloud Service instance, you can [add users in admin console](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/security/ims-support.html?lang=ja) for personas applicable to your organization or project and [assign users to built-in groups](forms-groups-privileges-tasks.md) to provide them required privileges.

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
Also, one of the most common requirements for developers is quick access to the log files of the various environments. With [!DNL AEM Cloud Service], the log files of the different nodes in the Author, Publish are made available via the Cloud Manager, either in the form of files that can be downloaded or via APIs for tailing the logs. Due to the clear separation of code and content, developers can use a particular process for updating content as part of a deployment. The typical use cases for mutable content are:
* Standard “default” content that is part of the customer project (for example, folders, templates, workflows...)
* Search index definitions
* ACLs and permissions
* Service users and user groups
Set up your development environment, [Configure your CI/CD Pipeline](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/how-to-use/configuring-pipeline.html?lang=ja), and learn to [deploy your code](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/how-to-use/deploying-code.html?lang=ja) on the environment. -->

### アダプティブフォームオーサリング {#local-development}

[!DNL AEM Forms] as a Cloud Service 環境を設定する場合は、開発環境、ステージング環境および本番環境を設定します。さらに、迅速な反復と開発を行うために、ローカル開発環境を設定します。AEM SDK と [!DNL AEM Forms] アドオン機能アーカイブをダウンロードして設定し、ローカルの [!DNL Forms] as a Cloud Service 開発環境を設定できます。手順について詳しくは、[ローカル開発環境の設定](setup-local-development-environment.md)を参照してください。

## デバッグ {#debugging}

AEM as a Cloud Service は、セルフサービスのスケーラブルなクラウドインフラストラクチャ上で実行します。AEM 開発者は、ビルドとデプロイから、実行中の AEM アプリケーションの詳細情報の取得まで、AEM as a Cloud Service の様々な側面を理解し、デバッグする必要があります。詳しくは、[AEM as a Cloud Service のデバッグ](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/debugging/debugging-aem-as-a-cloud-service/overview.html?lang=ja)を参照してください。


>[!MORELIKETHIS]
>
>* [AEM Forms as a Cloud Service の概要](/help/forms/aem-forms-cloud-service-communications-introduction.md)
>* [Forms as a Cloud Service の通信バッチ処理](/help/forms/aem-forms-cloud-service-communications-batch-processing.md)
>* [通信処理 — 同期 API](/help/forms/aem-forms-cloud-service-communications.md)
