---
title: Forms ポータルコンポーネントを使用してAdobe Experience Manager Sites ページ上のフォームを一覧表示する方法
description: AEM Sites ページ上でフォームを一覧表示する方法を説明します。
feature: Adaptive Forms, Core Components
role: User, Developer
source-git-commit: 31f18027d856cbd161457c4a01d6c7c17d1c2b89
workflow-type: tm+mt
source-wordcount: '673'
ht-degree: 14%

---


# Sites ページでのフォームの一覧表示

口座開設フォームを求めて銀行のウェブサイトにアクセスするユーザーを想像してみてください。 この銀行では、Formsポータルコンポーネントを使用して、特定のキーワードを入力したり、「新規口座」や「パーソナルバンキング」などのカテゴリでフィルタリングしたりして、フォームをすばやく見つけられるようにします。また、長いリストをスクロールしなくても、目的のフォームを簡単に見つけることができます。

Forms ポータルの **検索とリスター** コンポーネントを使用すると、Sites ページにフォームを表示して一覧表示できます。 ユーザーは、組織の要件を満たすために、特定の条件に基づいてフォームの包括的なリストを設定および表示できます。 匿名ユーザーは、Sites ページにアクセスして、使用可能なフォームを表示および参照できます。 画面の右上隅にある **並べ替え** ドロップダウンオプションを使用して、リストされたフォームを昇順または降順で並べ替えることができます。

![検索とリスターアイコン](assets/search-and-lister-component.png)

## 前提条件

Forms ポータルコンポーネントの様々な機能を調べる前に、お使いの環境でコアコンポーネントが有効になっていることを確認してください。 お使いの環境でコアコンポーネントを有効にする方法について詳しくは、[ ここをクリック ](/help/forms/enable-adaptive-forms-core-components.md) してください。

<!--
## Enable Forms Portal components for your existing environment

To enable out-of-the-box Forms Portal components on existing AEM Forms as a Cloud Service, perform the following steps:

1. **Clone Cloud Manager Git repository on your local development instance:**  Your Cloud Manager Git repository contains a default AEM project. It is based on [AEM Archetype](https://github.com/adobe/aem-project-archetype/). Clone your Cloud Manager Git Repository using Self-Service Git Account Management from Cloud Manager UI to bring the project on your local development environment. For details on accessing the repository, see [Accessing Repositories](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/managing-code/accessing-repos.html?lang=ja).  

1. **Create [!DNL Experience Manager Forms] as a [Cloud Service] project:** Create [!DNL Experience Manager Forms] as a [Cloud Service] project based on [AEM Archetype 50](https://github.com/adobe/aem-project-archetype/releases/tag/aem-project-archetype-50) or later. The archetype help developers easily start developing for [!DNL AEM Forms] as a Cloud Service. It also includes some sample themes and templates to help you started quickly.

    To create [!DNL Experience Manager Forms] as a Cloud Service project, open the command prompt and run the below command. To include [!DNL Forms] specific configurations, themes, and templates, set `includeForms=y`.  

    ```shell
    mvn -B archetype:generate -DarchetypeGroupId=com.adobe.aem -DarchetypeArtifactId=aem-project-archetype -DarchetypeVersion=30 -DaemVersion="cloud" -DappTitle="My Site" -DappId="mysite" -DgroupId="com.mysite" -DincludeForms="y"
    ```

    Also, change `appTitle`, `appId`, and `groupId`, in the above command to reflect your environment.

    After the project is ready, update the `<core.forms.components.version>x.y.z</core.forms.components.version>` property in the top-level `pom.xml` of the Archetype project to reflect the latest version of [core-forms-components](https://github.com/adobe/aem-core-forms-components) in your `AEM Archetype` project. 
 
1. **Deploy the project to your local development environment:** You can use the following command to deploy to your local development environment

    `mvn -PautoInstallPackage clean install`

    For the complete list of commands, see [Building and Installing](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/using.html?lang=ja#building-and-installing)

1. [Deploy the archetype to your [!DNL AEM Forms] as a Cloud Service environment](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/developing/aem-project-content-package-structure.html?lang=ja#embeddeds). -->

最新のコアコンポーネントを環境にデプロイすると、オーサリング環境でForms ポータルコンポーネントにアクセスできるようになります。

## Sites ページでのフォームの一覧表示

**検索とリスター** ポータルコンポーネントを Sites ページに追加するには、次の手順を実行します。

1. AEM Sitesページを **編集** モードで開きます。
1. **[!UICONTROL ページ情報]**／**[!UICONTROL テンプレートを編集]**&#x200B;に移動します。
   ![ テンプレートポリシーを編集 ](/help/forms/assets/save-form-as-draft-edit-template.png)

1. **[!UICONTROL ポリシー]** をクリックし、**[AEM アーキタイププロジェクト名 ] - Formsとコミュニケーションポータル** の下にある **[!UICONTROL 検索とリスター]** チェックボックスを選択します。

   ![ ポリシーの選択 ](/help/forms/assets/search-lister-enable-policy.png)

1. 「**[!UICONTROL 完了]**」をクリックします。
1. オーサリングモードでAEM Sitesページを再度開きます。
1. ページエディターでForms ポータルコンポーネントを追加できるセクションを見つけます。

1. **追加** アイコンをクリックします。 アイコンは、新しいコンポーネントを追加するオプションを示すプラス記号（+）です。

   **追加** アイコンをクリックすると、**新規コンポーネントの挿入** ダイアログボックスが表示され、挿入する様々なコンポーネントが表示されます。

   >[!NOTE]
   >
   > または、コンポーネントをドラッグ&amp;ドロップすることもできます。

1. ダイアログボックスで使用可能なコンポーネントを参照し、リストから目的のコンポーネントを選択します。 例えば、**Search &amp; Lister** コンポーネントをリストから選択して、**Search &amp; Lister** Formsポータルコンポーネントを追加します。

   ![Search &amp; Lister コンポーネント ](/help/forms/assets/add-search-lister.png)

次に、**検索とリスター** コンポーネントのプロパティを設定します。

## 検索とリスターコンポーネントのプロパティについて

設定ダイアログを使用して **検索とリスター** コンポーネントのプロパティを簡単にカスタマイズし、シームレスなユーザーエクスペリエンスを実現できます。 設定するには、コンポーネントを選択してから ![設定アイコン](assets/configure_icon.png) をクリックします。**[!UICONTROL 検索とリスター]** ダイアログが開きます。

### 「表示」タブ

![ 「表示」タブ ](/help/forms/assets/search-and-lister-display-tab.png)

1. **[!UICONTROL タイトル]** で、検索とリスターコンポーネントのタイトルを指定します。特徴的なタイトルを使用すると、ユーザーはフォームのリスト全体をすばやく検索できます。
1. **[!UICONTROL レイアウト]** リストで、フォームをカード形式またはリスト形式で表すレイアウトを選択します。
1. 「**[!UICONTROL 検索を非表示]**」および「**[!UICONTROL 並べ替えを非表示]**」を選択し、検索機能と並べ替え機能を非表示にします。
1. **[!UICONTROL ツールヒント]** で、コンポーネントにカーソルを合わせたときに表示されるツールヒントを指定します。

### 「アセット」タブ

![ 「アセット」タブ ](/help/forms/assets/search-and-lister-asset-tab.png)

1. 「**[!UICONTROL アセットフォルダー]**」タブで、フォームを取得してページに一覧表示する場所を指定します。
1. **[!UICONTROL 別の場所を追加]** を使用すると、複数のフォルダーの場所を設定できます。

### 「結果」タブ

![ 「表示」タブ ](/help/forms/assets/search-and-lister-result-tab.png)

「**[!UICONTROL 結果]**」タブで、1 ページに表示するフォームの最大数を設定します。デフォルトでは、1 ページに 8 つのフォームです。

## 検索とリスターコンポーネントを使用して、Sites ページにフォームを表示する

フォームのリストを表示するには、**検索とリスター** Forms ポータルコンポーネントを使用します。 AEM Sites ページをプレビューして、画面に表示される **Assets** フォルダーのフォームのリストを確認します。 検索バーを使用して特定のフォームを検索することもできます。

![検索とリスターアイコン](assets/search-and-lister-component.png)

<!--
## Configure Azure Storage for Adaptive Forms {#configure-azure-storage-adaptive-forms}

[[!DNL Experience Manager Forms] Data Integration](data-integration.md) provides [!DNL Azure] storage configuration to integrate forms with [!DNL Azure] storage services. The Form Data Model (FDM) can be used to create Adaptive Forms that interact with [!DNL Azure] server to enable business workflows.

### Create Azure Storage Configuration {#create-azure-storage-configuration}

Before executing these steps, ensure that you have an Azure storage account and an access key to authorize access to the [!DNL Azure] storage account.

1. Navigate to **[!UICONTROL Tools]** &gt; **[!UICONTROL Cloud Services]** &gt; **[!UICONTROL Azure Storage]**.
1. Select a folder to create the configuration and select **[!UICONTROL Create]**.
1. Specify a title for the configuration in the **[!UICONTROL Title]** field.
1. Specify the name of the [!DNL Azure] storage account in the **[!UICONTROL Azure Storage Account]** field.

### Configure Unified Storage Connector for Forms Portal {#configure-usc-forms-portal}

Perform the following steps to configure Unified Storage Connector for AEM Workflows:

1. Navigate to **[!UICONTROL Tools]** &gt; **[!UICONTROL Forms]** &gt; **[!UICONTROL Unified Storage Connector]**.
1. In the **[!UICONTROL Forms Portal]** section, select **[!UICONTROL Azure]** from the **[!UICONTROL Storage]** drop-down list.
1. Specify the [configuration path for the Azure storage configuration](#create-azure-storage-configuration) in the **[!UICONTROL Storage Configuration Path]** field.
1. Select **[!UICONTROL Publish]** and then select **[!UICONTROL Save]** to save the configuration.

## Enable Forms Portal Components {#enable-forms-portal-components}

To use any core component (including the out-of-the-box portal components) in an Adobe Experience Manager (AEM) site, you must create a proxy component and enable it for your site. For creating a proxy component and enabling portal components, see [Using Core Components](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/get-started/using.html?lang=ja#create-proxy-components). 

Once a portal component is enabled, you can use it in the author instance of your sites page.

## Add and Configure Forms Portal Components {#configure-forms-portal-components}

You can create and customize Forms Portal on websites authored using AEM by adding and configuring the portal components. Ensure that the [components are enabled](#enable-forms-portal-components) before using them in the Forms Portal.

To add a component, either drag and drop the component from the Components pane to the layout container on the page, or select the add icon on the layout container and add the component from the [!UICONTROL Insert New Component] dialog.

### Configure Drafts & Submissions Component {#configure-drafts-submissions-component}

The Drafts & Submissions component displays forms that are saved as draft for completing later and submitted forms. To configure, select the component and then select the ![Configure icon](assets/configure_icon.png). In the [!UICONTROL Drafts and Submissions] dialog, specify the title to indicate the form listing as draft or submitted forms. Also select whether the component should list draft forms or submitted forms in card or list format.

![Drafts icon](assets/drafts-component.png)

![Submissions icon](assets/submission-listing.png)

### Configure Search & Lister Component {#configure-search-lister-component}

The Search & Lister component is used to list adaptive forms on a page and to implement search on the listed forms. 

![Search and Lister icon](assets/search-and-lister-component.png)

To configure, select the component and then select the ![Configure icon](assets/configure_icon.png). The [!UICONTROL Search and Lister] dialog opens.

1. In the [!UICONTROL Display] tab, configure the following:
    * In **[!UICONTROL Title]**, specify the title for the Search & Lister component. An indicative title enables the users perform quick search across the list of forms.
    * From the **[!UICONTROL Layout]** list, select the layout to represent the forms in card or list format.
    * Select **[!UICONTROL Hide Search]** and **[!UICONTROL Hide Sorting]** to hide the search and sort by features.
    * In **[!UICONTROL Tooltip]**, provide the tooltip that appears when you hover over the component. 
1. In the [!UICONTROL Asset Folder] tab, specify the location from where the forms are pulled and listed on the page. You can configure multiple folder locations.
1. In the [!UICONTROL Results] tab, configure the maximum number of forms to display per page. The default is eight forms per page.

### Configure Link Component {#configure-link-component}

The link component enables you to provide links to an adaptive form on the page. To configure, select the component and then select the ![Configure icon](assets/configure_icon.png). The [!UICONTROL Edit Link Component] dialog opens.

1. In the [!UICONTROL Display] tab, provide the link caption and tooltip to ease identification of the forms represented by the link.
1. In the [!UICONTROL Asset Info] tab, specify the repository path where the asset is stored. 
1. In the [!UICONTROL Query Params] tab, specify the additional parameters in the key-value pair format. When the link is clicked, these additional parameters and passed along with the form.

## Configure Asynchronous Form Submission Using Adobe Sign {#configure-asynchronous-form-submission-using-adobe-sign}

You can configure to submit an adaptive form only when all the recipients have completed the signing ceremony. Follow the steps below to configure the setting using Adobe Sign.

1. In the author instance, open an Adaptive Form in the edit mode.
1. From the left pane, select the Properties icon and expand the **[!UICONTROL ELECTRONIC SIGNTATURE]** option.
1. Select **[!UICONTROL Enable Adobe Sign]**. Various configuration options display. 
1. In the [!UICONTROL Submit the form] section, select the **[!UICONTROL after every recipient completes signing ceremony]** option to configure the Submit Form action, where the form is first sent to all the recipients for signing. Once all the recipients have signed the form, only then the form is submitted. 

## Save Adaptive Forms As Drafts {#save-adaptive-forms-as-drafts}

You can save forms as Drafts for completing them later. There are two ways in which a form is saved as a draft:

* Create a "Save Form" rule on a form component, for example, a button. On clicking the button, the rule triggers and the form are saved a draft.
* Enable Auto-Save feature, which saves the form as per the specified event or after a configured interval of time.

### Create Rules to Save an Adaptive Form as Draft {#rule-to-save-adaptive-form-as-draft}

To create a "Save Form" rule on a form component, for example, a button, follow the steps below:

1. In the author instance, open an Adaptive Form in edit mode.
1. From the left pane, select ![Components icon](assets/components_icon.png) and drag the [!UICONTROL Button] component to the form.
1. Select the [!UICONTROL Button] component and then select the ![Configure icon](assets/configure_icon.png). 
1. Select the [!UICONTROL Edit Rules] icon to open the Rule Editor. 
1. Select **[!UICONTROL Create]** to configure and create the rule.
1. In the [!UICONTROL When] section, select "is clicked" and in the [!UICONTROL Then] section, select the "Save Form" options.
1. Select **[!UICONTROL Done]** to save the rule.

### Enable Auto-save {#enable-auto-save}

You can configure the auto-save feature for an adaptive form as follows:

1. In the author instance, open an Adaptive Form in edit mode.
1. From the left pane, select the ![Properties icon](assets/configure_icon.png) and expand the [!UICONTROL AUTO-SAVE] option.
1. Select the **[!UICONTROL Enable]** check box to enable auto-save of the form. You can configure the following:
* By default, the [!UICONTROL Adaptive Form Event] is set to "true", which implies that the form is auto-saved after every event.
* In [!UICONTROL Trigger], configure to trigger auto-save based on the occurrence of an event or after a specific interval of time.
-->


## 次の手順

次の記事では、[ フォームをドラフトとして保存し、ドラフトと送信Forms ポータルコンポーネントを使用してサイトページに一覧表示する方法 ](/help/forms/save-core-component-based-form-as-draft.md) について説明します。

## 関連記事

{{forms-portal-see-also}}

## 関連トピック {#see-also}

{{see-also}}