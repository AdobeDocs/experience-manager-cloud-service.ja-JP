---
title: アダプティブForms用のMicrosoft Dynamics 365のフォームデータモデルを設定する方法を教えてください。
description: Microsoft Dynamics 365とアダプティブFormsの統合方法について説明します。
feature: Adaptive Forms, Form Data Model
role: User, Developer
badgeSaas: label="AEM Forms" type="Positive" tooltip="AEM Formsに適用）。"
exl-id: 29ee324c-cd4c-403b-bb3d-b1eda8e8ad88
source-git-commit: fa8035f826a4d08c18bc0d2b7664015c6fc82698
workflow-type: tm+mt
source-wordcount: '921'
ht-degree: 16%

---


# Microsoft® Dynamics 365 for AEM Formsの設定

Adobe Experience Manager Forms Data Integrationでは、Microsoft Dynamics serverにフォームを統合するためのクラウドサービス設定を提供します。 これにより、Microsoft Dynamics サービスで定義されたエンティティ、属性、サービスに基づいてフォームデータモデル（FDM）を作成できます。 フォームデータモデル（FDM）を使用すると、Microsoft Dynamics サーバーと対話してビジネスワークフローを有効にするアダプティブ Formsを作成できます。 例：

* Microsoft Dynamics Serverにデータをクエリし、アダプティブ Formsを事前入力します。
* アダプティブフォーム送信時にMicrosoft Dynamicsにデータを書き込みます。
* フォームデータモデル（FDM）で定義されたカスタムエンティティを使用して、Microsoft Dynamicsでデータを書き込みます。

AEM as a Cloud Service では、フォーム送信を処理するための様々な送信アクションが標準で提供されます。これらのオプションについて詳しくは、 [アダプティブフォーム送信アクション](/help/forms/configure-submit-actions-core-components.md)の記事を参照してください。

<!-- 
[[!DNL Experience Manager Forms] Data Integration](data-integration.md) provides [!DNL Microsoft&reg; Dynamics 365] Cloud Services to integrate Adaptive Forms with out of the box Form Data Model (FDM). The Adaptive Forms can then interact with [!DNL Microsoft&reg; Dynamics 365] servers to enable business workflows. For example:

* Write data into [!DNL Microsoft&reg; Dynamics 365] on Adaptive Form submission.
* Write data in [!DNL Microsoft&reg; Dynamics 365] through custom entities defined in Form Data Model (FDM) and conversely.
* Query [!DNL Microsoft&reg; Dynamics 365]server for data and prepopulate Adaptive Forms.
* Read data from [!DNL Microsoft&reg; Dynamics 365] server.

[!DNL Microsoft&reg; Dynamics 365] cloud services and Form Data Model (FDM) are available out of the box on the [!DNL AEM Forms] Server after you [set up a development project for Forms based on Experience Manager archetype](setup-local-development-environment.md#forms-cloud-service-local-development-environment).

>[!NOTE]
>
>Microsoft&reg; Dynamics 365 cloud services and Form Data Model (FDM) are available out of the box only if you set up an [!DNL Experience Manager Forms] as a [!DNL Cloud Service] project based on [AEM Archetype 30](https://github.com/adobe/aem-project-archetype/releases/tag/aem-project-archetype-30) or later.
-->

## 前提条件

[!DNL Microsoft® Dynamics 365]をAEM Forms as a Cloud Serviceと統合する前に、次の手順を実行していることを確認してください。


1. **Microsoft Dynamics 365**&#x200B;でアカウントを設定する

   ビデオで説明されている手順に従って、Microsoft Dynamics 365 アカウントを設定します。 このビデオでは、デモ用に体験版アカウントが作成されています。

   >[!VIDEO](https://video.tv.adobe.com/v/3444389/)

1. **Power Platform Admin Centerでアカウントを作成する**

   **Power Platform Admin Center**&#x200B;でアカウントを作成して、次の操作を行います。

   * データバースを追加
   * Microsoft Dynamics 365 アプリケーションの有効化

   ビデオの手順に従って、Power Platform Admin Centerでアカウントを作成します。 このビデオでは、デモ用に体験版アカウントが作成されています。

   >[!VIDEO](https://video.tv.adobe.com/v/3444388)

1. **Azure Active Directoryで[!DNL Microsoft® Dynamics 365]のアプリケーションを登録**

   ビデオの手順に従って、Azure Active Directoryに[!DNL Microsoft® Dynamics 365]のアプリケーションを登録します。

   >[!VIDEO](https://video.tv.adobe.com/v/3444369/dynamics365integration-microsoftdynamics-apiaccess-azuread-appregistration)

   >[!NOTE]
   >
   >* 接続された[!DNL Microsoft® Dynamics 365] アプリケーションを作成するには、プラットフォームとして&#x200B;**Web**&#x200B;を選択し、次の形式で&#x200B;**リダイレクト URI**&#x200B;を指定します：`https://'[server]:[port]'/libs/fd/fdm/gui/components/admin/fdmcloudservice/fdm.html`。
   >* 後で参照できるように、クライアント ID （アプリケーション IDとも呼ばれます）とクライアント秘密鍵を必ず保存してください。

## FormsとMicrosoft®Dynamics 365の連携

上記の前提条件を設定したら、アダプティブ FormsとMicrosoft® Dynamics 365の統合を進めることができます。 フォーム送信時にMicrosoft® Dynamics 365にデータを送信するには、次の手順に従います。

[&#x200B;1. Microsoft Dynamicsのクラウドサービス設定](#1-configure-cloud-service-configuration-for-microsoft-dynamics)

[&#x200B;2. フォームデータモデル（FDM）の作成](#2-create-form-data-model-fdm)

### &#x200B;1. Microsoft Dynamicsのクラウドサービス設定

>[!VIDEO](https://video.tv.adobe.com/v/3444370/cloudconfiguration-dataintegration-adobeexperiencemanager-aemforms-microsoftdynamics)

次の手順を実行して、[!DNL Microsoft® Dynamics 365] クラウドサービス設定を設定します。

1. **[!UICONTROL オーサーインスタンスの]** ツール ![ ](assets/hammer.png)hammer **[!UICONTROL >]** Cloud Services **[!UICONTROL >]** データソース [!DNL AEM Forms]に移動します。

   ![Cloud Data Sourceを選択](/help/forms/assets/dynamics-data-source.png)
1. 設定コンテナを選択します。 設定は、選択した設定コンテナに保存されます。
1. 「**[!UICONTROL 作成]**」をクリックします。

   ![ クラウド設定の作成](/help/forms/assets/dynamics-select-configuration.png)

   **Data Source Configuration**&#x200B;設定を作成ウィザードが表示されます。

   ![Data Source設定の作成ウィザード ](/help/forms/assets/dynamics-create-data-configuration.png)

1. **[!UICONTROL タイトル]**、**[!UICONTROL 名前]**&#x200B;を指定し、**[!UICONTROL サービスタイプ]**&#x200B;を&#x200B;**OData サービス**&#x200B;として選択します。
1. 「**[!UICONTROL 次へ]**」をクリックします。「**認証**」タブが表示されます。

   ![認証タブ ](/help/forms/assets/dynamics-authentication-tab.png)

1. 「**[!UICONTROL サービスルート]**」フィールドの値を指定します。

   **Power Platform Admin Center**&#x200B;でDynamics インスタンスに移動し、[開発者リソース ](https://docs.microsoft.com/ja-jp/powerapps/developer/data-platform/view-download-developer-resources)に移動して、**サービスルート**&#x200B;の値を表示します。 **Web API エンドポイント**&#x200B;は、アダプティブ Formsと統合するDynamics インスタンスの&#x200B;**サービスルート**&#x200B;値を表します。 **サービスルート** URLは次の形式です：`https://<tenant-name>.dynamics.com/api/data/v9.1/`

   ![ サービス ルート フィールド ](/help/forms/assets/dynamics-service-root.png)

1. **[!UICONTROL 認証タイプ]**&#x200B;を&#x200B;**OAuth2.0**&#x200B;として選択します。
1. 接続されたアプリケーションの&#x200B;**クライアント ID** （アプリケーション IDと呼ばれます）と&#x200B;**クライアントシークレット**を指定します。
**クライアント ID**&#x200B;と&#x200B;**クライアントシークレット**&#x200B;は、Azure Active Directory アプリケーションから取得できます。

   ![ クライアント IDとクライアント秘密鍵](/help/forms/assets/dynamics-azure-app-resgistration.png)

1. 「**[!UICONTROL OAuth URL]**」、「**[!UICONTROL トークン URLの更新]**」、「**[!UICONTROL アクセストークン URL]**」の各フィールドに以下を指定します。
**[!UICONTROL OAuth URL]**、**[!UICONTROL 更新トークン URL]**&#x200B;および&#x200B;**[!UICONTROL アクセストークン URL]**&#x200B;は、Azure Active Directory アプリケーションの&#x200B;**エンドポイント** セクションから取得できます。

   ![Azure アプリエンドポイント ](/help/forms/assets/dynamics-azure-app-endpoints.png)

1. `openid` の認証プロセス用の「**[!UICONTROL 認証範囲」フィールドで]**、「[!DNL Microsoft® Dynamics 365]」を指定します。
1. **[!UICONTROL をフォームデータモデル （FDM）で設定するには、]** リソース [!DNL Microsoft® Dynamics 365] フィールドでdynamics インスタンス URLを指定します。
**環境URL**&#x200B;を&#x200B;**Power Platform管理センター**&#x200B;からコピーするか、**サービスルート** URLを使用してDynamics インスタンス URLを取得できます。 リソース URLは次の形式です：`https://<tenant-name>.dynamics.com`。

   ![Power アプリ リソース フィールド ](/help/forms/assets/dynamics-resource-field.png)

1. [!DNL Microsoft® Dynamics 365] の資格情報を使用してログインし、クラウドサービス設定を使用して [!DNL Microsoft® Dynamics 365] サービスに接続することに同意します。接続に成功すると、[!DNL Microsoft® Dynamics 365] クラウドサービス設定ページにリダイレクトされ、成功メッセージが表示されます。
1. 設定を保存するには、**[!UICONTROL 作成]**&#x200B;を選択します。

### &#x200B;2. フォームデータモデル（FDM）の作成

>[!VIDEO](https://video.tv.adobe.com/v/3444367/aemforms-adobeexperiencemanager-formdatamodel--dataintegration-digitalforms)

作成した[!DNL Microsoft® Dynamics 365] クラウド設定を使用して、フォームデータモデル （FDM）を作成できます。 フォームデータモデルを作成するには、次の手順を実行します。

1. **[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL Forms]** > **[!UICONTROL Data Integrations]**に移動します。
   ![フォームデータモデルを作成](/help/forms/assets/dynamics-create-fdm.png)

1. **[!UICONTROL 作成]**&#x200B;をクリックし、**[!UICONTROL フォームデータモデル]**を選択します。
   ![フォームデータモデルを選択](/help/forms/assets/dynamics-select-fdm.png)

   「**フォームデータモデルを作成**」ウィザードが表示されます。
1. 「**[!UICONTROL 次へ]**」をクリックします。
1. 「**データソースを選択**」タブから、作成したクラウド設定を選択します。
   ![ クラウド設定を選択](/help/forms/assets/dynamics-select-cloud-config.png)

1. 「![編集](assets/edit.png)を編集」アイコンをクリックして、フォームデータモデル（FDM）を表示および設定します。

次に、[ フォームデータモデル（FDM） ](/help/forms/work-with-form-data-model.md#configure-services)を設定し、次のようなさまざまなアダプティブフォームのユースケースで使用できます。

* [!DNL Microsoft Dynamics] のエンティティとサービスに対してクエリを実行し、取得した情報を使用してアダプティブフォームに事前入力する
* アダプティブフォームのルールを使用して、フォームデータモデル（FDM）内で定義された [!DNL Microsoft Dynamics] サーバーの操作を呼び出す
* 送信されたフォームデータを [!DNL Microsoft Dynamics] のエンティティに書き込む
* アダプティブフォームのフォームデータモデル送信アクションを設定して、[!DNL Microsoft Dynamics]にデータを送信できます。

次に、[ アダプティブフォーム ](/help/forms/using-form-data-model.md)で「**フォームデータモデル（FDM）**&#x200B;を使用して送信」オプションを使用して、フォームから設定された[!DNL Microsoft® Dynamics 365]にデータを転送できます。


>[!MORELIKETHIS]
>
>* [AEM Forms のデータソースを設定](/help/forms/configure-data-sources.md)
>* [AEM Forms の Azure ストレージを設定](/help/forms/configure-azure-storage.md)
>  [AEM Sites ページへのフォームポータルの追加](/help/forms/configure-forms-portal.md)
