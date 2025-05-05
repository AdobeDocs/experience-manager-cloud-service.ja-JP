---
title: ' [!DNL AEM Forms]  as a Cloud Service 環境の設定方法'
description: ' [!DNL AEM Forms]  as a Cloud Service 環境のセットアップと設定方法について説明します。'
role: Admin, Developer, User
feature: Adaptive Forms
exl-id: 42f53662-fbcf-4676-9859-bf187ee9e4af
source-git-commit: 81951a9507ec3420cbadb258209bdc8e2b5e2942
workflow-type: tm+mt
source-wordcount: '610'
ht-degree: 100%

---

# [!DNL AEM Forms] as a Cloud Service へのオンボード {#overview}

| バージョン | 記事リンク |
| -------- | ---------------------------- |
| AEM 6.5 | [ここをクリックしてください](https://experienceleague.adobe.com/docs/experience-manager-65/forms/install-aem-forms/osgi-installation/installing-configuring-aem-forms-osgi.html?lang=ja) |
| AEM as a Cloud Service | この記事 |


## ペルソナの決定 {#personas-aem-forms-project}

<!-- When you sign up for the service, Adobe creates an Organization identifier for your company in the Adobe Identity Management System (IMS), where your users and their permissions can be managed. So, --> Adobe Experience Manager (AEM) Forms as a Cloud Service 環境にオンボーディングする前に、ペルソナを決定し、プロジェクトのチームを構築します。典型的な [!DNL AEM Forms] プロジェクトチームには次のペルソナがあります。

* **ユーザーエクスペリエンス（UX）デザイナー**：ユーザーエクスペリエンス（UX）デザイナーは、[!DNL AEM Forms] のアセットのスタイル、レイアウト、ブランディングを定義します。

* **Forms 担当者**：Forms 担当者は、UX デザイナーが提供するスタイル、レイアウト、ブランディングに従って、アダプティブフォーム、テーマ、テンプレートを作成します。また、担当者はアダプティブフォームを作成して、フォームデータモデル（FDM）や AEM ワークフローと統合します。Forms 担当者は、通常、フロントエンドのタスクに取り掛かります。

* **Forms 開発者**：Forms 開発者は、カスタムフォームソリューションを開発します。Forms 開発者は、通常、カスタムコンポーネント、AEM ワークフロー、事前入力サービスなどのバックエンド開発を担当します。

* **AEM 管理者**：AEM 管理者は、ユーザーの設定、環境の堅牢化、データソースの設定、メールの設定、サードパーティ製ソフトウェアなど、全体的な設定を支援します。AEM 管理者は、Adobe Analytics、Adobe Target、Adobe Sign との統合なども支援します。

* **エンドユーザー**：ユーザーは、公開されたフォームとやり取りして送信し、送信されたフォームに署名し、送信されたアプリケーションを web ポータル経由で確認し、パーソナライズされたコミュニケーションを受信します。

<!-- While onboarding to the service, assign the following AEM groups to [!DNL AEM Forms] as a Cloud Service based on their role:

| User type | AEM group |
|---|---|
| Form Practitioner | forms-users (AEM Forms Users), template-authors, workflow-user, workflow-editors, and fdm-author  |
| UX Designer| forms-users, template-authors|
| End-User| <ul> <li>When a user must login to view and submit an Adaptive Form, add such users to forms-users group. </li> <li>When no user authentication is required to access Adaptive Forms, do not assign any group to such users. </li> </ul>| -->

## サービスへのオンボード {#onboarding}

* [!DNL Adobe Experience Manager] as a Cloud Service への[オンボード](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/onboarding/journey/overview.html?lang=ja)。

* （サンドボックスのみ）サービスにオンボードした後、[作成](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/content/using/pipelines/production-pipelines.html?lang=ja)と[実行](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/content/using/code-deployment.html?lang=ja)は、実稼働用と非実稼働用の両方のパイプラインを実行します。[!DNL AEM Forms] as a Cloud Service の最新機能を有効にし、環境に提供します。

Forms as a Cloud Service を使用してアダプティブフォーム（デジタル登録）を作成したり、顧客通信を生成したりできます。[!DNL Adobe Experience Manager] as a Cloud Service の[オンボーディング](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/onboarding/journey/overview.html?lang=ja)完了後、次のいずれかの操作を実行して、デジタル登録またはカスタマーコミュニケーション機能を有効にします。<!--You can also enable both the features-->

1. Cloud Manager にログインし、AEM Forms as a Cloud Service インスタンスを開きます。
1. 「プログラムを編集」オプションを開き、「ソリューションとアドオン」タブに移動します。

   * 本番環境がある場合は、「**[!UICONTROL Forms - コミュニケーション]**」オプションを選択して、Forms - デジタル登録および Forms - コミュニケーションアドオンを有効にします。

     ![通信](assets/communications.png)

   <!-- If you have already enabled the **[!UICONTROL Forms - Digital Enrollment]** option, then select the **[!UICONTROL Forms - Communications Add-On]** option. ![Addon](assets/add-on.png) -->

   * サンドボックス環境がある場合は、「**[!UICONTROL Forms]**」を選択して、Forms - デジタル登録と Forms - コミュニケーションアドオンを有効にします。

     ![フォームデジタル登録の選択](assets/forms-digital-enrollment1.png)


1. 「**[!UICONTROL 更新]**」をクリックします。
1. ビルドパイプラインを実行します。ビルドパイプラインが正常に完了すると、お使いの環境で選択したソリューションが有効になります。

>[!NOTE]
>
> ドキュメント操作 API を有効にし設定するには、次のルールを [Dispatcher 設定](setup-local-development-environment.md#forms-specific-rules-to-dispatcher)に追加します。
>
> `# Allow Forms Doc Generation requests`
> `/0062 { /type "allow" /method "POST" /url "/adobe/forms/assembler/*" }`

## ユーザーの設定 {#config-users}

サービスへのオンボードを完了したら、[!DNL AEM Forms] as a Cloud Service 環境にログインし、オーサーインスタンスとパブリッシュインスタンスを開き、ユーザーをペルソナに基づいて Forms 固有の [AEM グループ](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/accessing/aem-users-groups-and-permissions.html?lang=ja#accessing)に追加します。次の表に、Forms 固有の AEM グループを示します。このグループは標準搭載で、対応するユーザータイプが利用可能です。また、各ユーザータイプの AEM インスタンスタイプも示します。

| ユーザータイプ（ペルソナ） | ユーザーグループ | AEM インスタンス |
|---|---|---|
| Forms 担当者／Forms 開発者 | <ul> <li> [!DNL forms-users] </li><li> [!DNL template-author] </li><li> [!DNL workflow-users] </li><li> [!DNL workflow-editors] </li><li> [!DNL fdm-authors] </li></ul> | オーサーインスタンス |
| ユーザーエクスペリエンス（UX）デザイナー | <ul> <li> [!DNL forms-users]</li><li> [!DNL template-author] </li></ul> | オーサーインスタンス |
| AEM 管理者 | <ul> <li>[!DNL aem-administrators]、</li> <li>[!DNL fd-administrators] </li> </ul> | オーサーおよびパブリッシュインスタンス |
| エンドユーザー | <ul> <li>ユーザーがアダプティブフォームを表示および送信するためにログインする必要がある場合は、ユーザを [!DNL forms-users] グループに追加します。 </li> <li>アダプティブフォームへのアクセスにユーザー認証が必要ない場合は、グループを割り当てません。 </li> </ul> | オーサーおよびパブリッシュインスタンス |

Forms 固有の AEM グループと対応する権限について詳しくは、 [グループと権限](forms-groups-privileges-tasks.md) を参照してください。

<!-- You can also create  [user groups](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/accessing/aem-users-groups-and-permissions.html?lang=ja#accessing) specific  to your organization, assign policies, and [users](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/accessing/aem-users-groups-and-permissions.html?lang=ja#accessing) to the groups. The policies help control permissions of the users that are part of the group. For information a -->

## 次の手順 {#next-steps}

[ローカル開発環境をセットアップします](setup-local-development-environment.md)。ローカル開発環境を使用して、アダプティブフォームと関連アセット（テーマ、テンプレート、カスタム送信アクション、事前入力サービスなど）を作成できます。そして、クラウド開発環境にログすることなく [PDF フォームをアダプティブフォームに変換します](https://experienceleague.adobe.com/docs/aem-forms-automated-conversion-service/using/introduction.html?lang=ja)。

<!-- ### Business unit and end-users {#business-unit-and-end-users}

| Role| Organization| Description|
|-----|-------|-----|
| UX Designer                  | Customer/System Integrator/Partner | Defines user experience design (style, layout, branding) as per organizational requirements for Adaptive Forms to allow AEM Forms practitioners to design the corresponding themes and templates.                                     |
| Forms Practitioner           | Customer                           | Authors Adaptive Forms, creates Form Data Model integrations, and creates business workflows using the Experience Manager Workflows. Typically undertakes the front-end work.                                                         |
| Business Executive - Digital | Customer                           | Responsible for business unit's product marketing strategy and revenues, main business stakeholders for digital use cases, solutions, and service offerings for the end-users, signs off on the use case implementation and delivery. |
| Customer Experience Lead     | Customer                           | Business user persona. Authors, personalizes and updates Adaptive Forms fields/rules/styling, identifies, and prioritizes business needs. Validates business use-case with SI/Partner developers/practitioners during UAT.            |
| Forms Back-Office User       | Customer                           | End-user internal to organization filling forms, participating in back-office Forms workflows such as review/approval of applications and so on.                                                                                            |
| Forms End-User               | External to customer               | Interacts with and submits the published form as end customer or citizen, signs submitted forms, tracks her applications through web portal, receives personalized interactive communications.                                        |

### Project team {#project-team}

| Role | Org | Description|
|-----|-----|-----|
| Experience Manager Administrator | System Integrator /Partner/Customer | Helps with overall installation, configures SSL certificates, configures data sources, email, and other third-party software, integrations like Adobe Analytics, Adobe Target, Automated Forms Conversion Services with Experience Manager instance. |
| Project Manager                  | System Integrator /Partner/Customer | Converts customer use-case into technical requirements, manages schedule/cost/scope for overall project.                                                                                                                                             |
| Product Owner                    | System Integrator /Partner/Customer | Prioritizes and evaluates scrum team's work for high-quality delivery on time.                                                                                                                                                                       |
| Scrum Master                     | System Integrator /Partner/Customer | Ensures agile values and processes in place to deliver on defined requirements as per prioritization by PO.                                                                                                                                          |
| Infrastructure / security expert | System Integrator /Partner/Customer | Provisions and configures best possible infrastructure, security controls and infra processes to address current and projected RASP requirements.                                                                                                    |
| Technical Architect              | System Integrator /Partner/Customer | Provides best high-level architecture and infrastructure guidance for use-case implementation and address RASP (Reliability, Availability, Scalability, and Performance) and security challenges.                                                    | -->

<!-- ## Onboard to the service {#onboarding}

[Onboard](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/onboarding/home.html?lang=ja) to the [!DNL Adobe Experience Manager] as a Cloud Service. 

After you onboard the service, configure a [local development environment](setup-local-development-environment.md). 

Administrators are responsible for managing Adobe software and services for their organization. Administrators grant access to developers in their organization to connect and use your [!DNL AEM Forms] as a Cloud Service program. When an administrator is provisioned for an organization, the administrator receives an email with title 'You now have administrator rights to manage Adobe software and services for your organization'. If you are an administrator, check your mailbox for email with previously mentioned title and proceed to [add users](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/security/ims-support.html?lang=ja#onboarding-users-in-admin-console) by way of IMS and assign [form-specific groups](forms-groups-privileges-tasks.md) to users based on their role.

## Next step {#next-steps} -->

<!-- ## Prerequisites {#prerequisites}

If you are new to AEM as a cloud service, contact your Adobe representative to create an organization identifier for your company in the Adobe Identity Management System (IMS). Once Adobe has created an organization for your company, your designated administrator is added as the first member of the organization. The administrator can setup an [!DNL AEM Forms] as a Cloud Service instance. 

## Onboard and set up a new environment {#onboard-and-setup-a-new-environment}

Log in to Cloud Manager and create a program. After the program is ready, create environments, add developers or users to environments, and run the pipeline to get the latest version of [!DNL AEM Forms] as a Cloud Service and start developing for your environment. The detailed steps are:

1. Contact your Adobe representative to create an organization identifier for your company in the Adobe Identity Management System (IMS) and provide access to an administrator in your organization.
1. Configure [Automated Forms Conversion Service](https://experienceleague.adobe.com/docs/aem-forms-automated-conversion-service/using/configure-service.html?lang=ja). After a configuration is complete, a profile for Automated Forms Conversion Service is available in [Admin Console](https://adminconsole.adobe.com/).

    If the service is not available, log in to [Admin Console](https://adminconsole.adobe.com/). Use Adobe ID of administrator provisioned to use Automated Forms Conversion Service to login. Do not use any other ID or Federated ID to login.
    1. Click **[!UICONTROL Automated Forms Conversion Service]** option.
    1. Click **[!UICONTROL New Profile]** in the Products tab.
    1. Specify **[!UICONTROL Name]**, **[!UICONTROL Display Name]**, and **[!UICONTROL Description]** for the profile. Click **[!UICONTROL Done]**. A profile is created. 
1. Log in to [Cloud Manager](https://experience.adobe.com/#/@marketinghub/experiencemanager) and [create a program](https://docs.adobe.com/content/help/ja-JP/experience-manager-cloud-service/onboarding/getting-access/cloud-service-programs/creating-a-program.html) for your organization.
1. [Create environments](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/manage-environments.html?lang=ja#adding-environments) within your program.
1. Log in to [Admin console](https://docs.adobe.com/content/help/en/experience-manager-cloud-service/onboarding/what-is-required/add-users-roles.html) and add developers or users to your organization.
1. Run the [build pipeline](https://docs.adobe.com/content/help/ja-JP/experience-manager-cloud-manager/using/how-to-use/deploying-code.html). It brings latest [!DNL Experience Manager Forms] as a Cloud Service features to your environment.
1. [Start developing](https://docs.adobe.com/content/help/ja-JP/experience-manager-cloud-service/implementing/developing/aem-project-content-package-structure.html) and creating Adaptive Forms on [!DNL Experience Manager Forms] as a Cloud Service environment.
1. Configure the [local development environment](setup-local-development-environment.md) for rapid development

## Configure dispatcher caching {#caching}

You can make dispatcher caching related configuration changes to code on your local development instance and deploy the changes to your [!DNL AEM Forms] as a Cloud Service instance. For details, see [update dispatcher configuration](setup-local-development-environment.md).
 -->
