---
title: Microsoft Dynamics 365 の標準フォームデータモデルをアダプティブForms用に設定する方法
description: Microsoft Dynamics 365 をアダプティブFormsと統合する方法を説明します。
feature: Adaptive Forms, Form Data Model
role: User, Developer
exl-id: 29ee324c-cd4c-403b-bb3d-b1eda8e8ad88
source-git-commit: 76301ca614ae2256f5f8b00c41399298c761ee33
workflow-type: tm+mt
source-wordcount: '915'
ht-degree: 16%

---


# AEM Forms用Microsoft® Dynamics 365 の設定

Adobe Experience Manager Forms Data Integration は、フォームをMicrosoft Dynamics サーバーと統合するためのクラウドサービス設定を提供します。 これにより、Microsoft Dynamics サービスで定義されたエンティティ、属性、サービスに基づいて、フォームデータモデル（FDM）を作成できるようになります。 フォームデータモデル（FDM）を使用して、Microsoft Dynamics サーバーと連携するアダプティブ Formsを作成すると、ビジネスワークフローを使用できるようになります。 例：
* Microsoft Dynamics サーバーに対してデータに関するクエリを実行し、アダプティブFormsに事前入力する。
* アダプティブフォームの送信時に、データをMicrosoft Dynamicsに書き込む。
* フォームデータモデル（FDM）で定義したカスタムエンティティを使用して、Microsoft Dynamicsにデータを書き込む。

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
>Microsoft&reg; Dynamics 365 cloud services and Form Data Model (FDM) are available out of the box only if you set up an [!DNL Experience Manager Forms] as a [!DNL Cloud Service] project based on [AEM Archetype 30](https://github.com/adobe/aem-project-archetype/releases/tag/aem-project-archetype-30) or later.-->

## 前提条件

[!DNL Microsoft® Dynamics 365] をAEM Forms as a Cloud Serviceと統合する前に、次の手順を実行したことを確認します。


1. **Microsoft Dynamics 365 でのアカウントの設定**

   ビデオで説明されている手順に従って、Microsoft Dynamics 365 アカウントを設定します。 このビデオでは、デモ用に体験版アカウントを作成します。

   >[!VIDEO](https://video.tv.adobe.com/v/3444389/)

1. **Power Platform Admin Center でのアカウントの作成**
**Power Platform Admin Center** で次のアカウントを作成します。
   * Dataverse を追加
   * Microsoft Dynamics 365 アプリケーションの有効化

   ビデオの手順に従って、Power Platform Admin Center でアカウントを作成します。 このビデオでは、デモ目的で体験版アカウントを作成しています。

   >[!VIDEO](https://video.tv.adobe.com/v/3444388)

1. **Azure Active Directory での [!DNL Microsoft® Dynamics 365] のアプリケーションの登録**

   ビデオの手順に従って、Azure Active Directory に [!DNL Microsoft® Dynamics 365] のアプリケーションを登録します。

   >[!VIDEO](https://video.tv.adobe.com/v/3444369/dynamics365integration-microsoftdynamics-apiaccess-azuread-appregistration)

   >[!NOTE]
   >
   > * 接続された [!DNL Microsoft® Dynamics 365] アプリケーションを作成するには、プラットフォームとして **Web** を選択し、次の形式で **リダイレクト URI** を指定します：`https://'[server]:[port]'/libs/fd/fdm/gui/components/admin/fdmcloudservice/fdm.html`。
   > * 後で参照できるように、クライアント ID （アプリケーション ID とも呼ばれます）とクライアントの秘密鍵を必ず保存してください。

## FormsをMicrosoft® Dynamics 365 に接続する

上記の前提条件を設定したら、アダプティブ FormsとMicrosoft® Dynamics 365 の統合に進むことができます。 フォーム送信時にデータをMicrosoft® Dynamics 365 に送信するには、次の手順に従います。

[1. Microsoft Dynamicsのクラウドサービス設定を行う](#1-configure-cloud-service-configuration-for-microsoft-dynamics)

[2. フォームデータモデル（FDM）を作成する](#2-create-form-data-model-fdm)

### 1. Microsoft Dynamicsのクラウドサービス設定を行う

>[!VIDEO](https://video.tv.adobe.com/v/3444370/cloudconfiguration-dataintegration-adobeexperiencemanager-aemforms-microsoftdynamics)

[!DNL Microsoft® Dynamics 365] クラウドサービス設定を指定するには、以下の手順を実行します。

1. オーサーインスタンスで、**[!UICONTROL ツール]**![ ハンマー ](assets/hammer.png)/**[!UICONTROL クラウドサービス]**/**[!UICONTROL データソース]**&#x200B;[!DNL AEM Forms] 移動します。

   ![ クラウドデータSourceを選択 ](/help/forms/assets/dynamics-data-source.png)
1. 設定コンテナを選択します。 設定は、選択した設定コンテナに保存されます。
1. 「**[!UICONTROL 作成]**」をクリックします。

   ![ クラウド設定の作成 ](/help/forms/assets/dynamics-select-configuration.png)

   **Data Source設定を作成** 設定ウィザードが表示されます。

   ![Data Source設定を作成ウィザード ](/help/forms/assets/dynamics-create-data-configuration.png)

1. **[!UICONTROL タイトル]**、**[!UICONTROL 名前]** を指定し、**[!UICONTROL サービスタイプ]** を **OData サービス** として選択します。
1. 「**[!UICONTROL 次へ]**」をクリックします。「**認証**」タブが表示されます。

   ![ 「認証」タブ ](/help/forms/assets/dynamics-authentication-tab.png)

1. 「**[!UICONTROL サービスルート]**」フィールドの値を指定します。

   **Power Platform 管理センター** の Dynamics インスタンスに移動し、[ 開発者リソース ](https://docs.microsoft.com/ja-jp/powerapps/developer/data-platform/view-download-developer-resources) に移動して **サービスルート** の値を表示します。 **Web API エンドポイント** は、アダプティブ Formsと統合する Dynamics インスタンスの **サービスルート** 値を表します。 **サービスルート** URL は次の形式です。`https://<tenant-name>.dynamics.com/api/data/v9.1/`

   ![ サービスルートフィールド ](/help/forms/assets/dynamics-service-root.png)

1. **[!UICONTROL 認証タイプ]** を **OAuth2.0** として選択します。
1. 接続アプリケーションの **クライアント ID** （アプリケーション ID）と **クライアントの秘密鍵** を指定します。
**クライアント ID** と **クライアントシークレット** は、Azure Active Directory アプリケーションから取得できます。

   ![ クライアント ID とクライアント秘密鍵 ](/help/forms/assets/dynamics-azure-app-resgistration.png)

1. 「**[!UICONTROL OAuth URL]**」、「**[!UICONTROL 更新トークン URL]**」、「**[!UICONTROL アクセストークン URL]**」の各フィールドに以下を指定します。
**[!UICONTROL OAuth URL]**、**[!UICONTROL 更新トークン URL]**、および **[!UICONTROL アクセストークン URL]** は、Azure Active Directory アプリケーションの **エンドポイント** セクションから取得できます。

   ![Azure アプリエンドポイント ](/help/forms/assets/dynamics-azure-app-endpoints.png)

1. `openid` の認証プロセス用の「**[!UICONTROL 認証範囲」フィールドで]**、「[!DNL Microsoft® Dynamics 365]」を指定します。
1. フォームデータモデル（FDM）で [!DNL Microsoft® Dynamics 365] を設定するには、Dynamics インスタンスの URL を「**[!UICONTROL リソース]**」フィールドに指定します。
**Power Platform 管理センター** から **環境 URL** をコピーするか、**サービスルート** URL を使用して Dynamics インスタンス URL を取得できます。 リソース URL の形式は `https://<tenant-name>.dynamics.com` です。

   ![ 電源アプリケーション リソース フィールド ](/help/forms/assets/dynamics-resource-field.png)

1. [!DNL Microsoft® Dynamics 365] の資格情報を使用してログインし、クラウドサービス設定を使用して [!DNL Microsoft® Dynamics 365] サービスに接続することに同意します。接続に成功すると、[!DNL Microsoft® Dynamics 365] クラウドサービス設定ページにリダイレクトされ、成功メッセージが表示されます。
1. 「**[!UICONTROL 作成]**」を選択して、設定を保存します。

### 2. フォームデータモデル（FDM）を作成する

>[!VIDEO](https://video.tv.adobe.com/v/3444367/aemforms-adobeexperiencemanager-formdatamodel--dataintegration-digitalforms)

作成した [!DNL Microsoft® Dynamics 365] クラウド設定を使用して、フォームデータモデル（FDM）を作成できます。 フォームデータモデルを作成するには、以下の手順を実行します。

1. **[!UICONTROL Adobe Experience Manager]** / **[!UICONTROL Forms]** / **[!UICONTROL Data Integrations]** に移動します。
   ![フォームデータモデルを作成](/help/forms/assets/dynamics-create-fdm.png)

1. **[!UICONTROL 作成]** をクリックし、「**[!UICONTROL フォームデータモデル]**」を選択します。
   ![ フォームデータモデルを選択 ](/help/forms/assets/dynamics-select-fdm.png)

   **フォームデータモデルを作成** ウィザードが表示されます。
1. 「**[!UICONTROL 次へ]**」をクリックします。
1. **データソースを選択** タブから、作成したクラウド設定を選択します。
   ![ クラウド設定を選択 ](/help/forms/assets/dynamics-select-cloud-config.png)

1. 編集 ![ 編集 ](assets/edit.png) アイコンをクリックして、フォームデータモデル（FDM）を表示および設定します。

次に、[ フォームデータモデル（FDM）を設定 ](/help/forms/work-with-form-data-model.md#configure-services) して、次のような様々なアダプティブフォームの使用例で使用できます。

* [!DNL Microsoft Dynamics] のエンティティとサービスに対してクエリを実行し、取得した情報を使用してアダプティブフォームに事前入力する
* アダプティブフォームのルールを使用して、フォームデータモデル（FDM）内で定義された [!DNL Microsoft Dynamics] サーバーの操作を呼び出す
* 送信されたフォームデータを [!DNL Microsoft Dynamics] のエンティティに書き込む
* アダプティブフォームのフォームデータモデル送信アクションを、[!DNL Microsoft Dynamics] にデータを送信するように設定できます。

その後、（アダプティブフォーム [ で「フォームデータモデル（FDM）を使用して送信 ](/help/forms/using-form-data-model.md) オプションを使用して、フォームから設定済みのフ [!DNL Microsoft® Dynamics 365] ームにデータを転送 **できます。**


>[!MORELIKETHIS]
>
>* [AEM Forms のデータソースを設定](/help/forms/configure-data-sources.md)
>* [AEM Forms の Azure ストレージを設定](/help/forms/configure-azure-storage.md)
>  [AEM Sites ページへのフォームポータルの追加](/help/forms/configure-forms-portal.md)
