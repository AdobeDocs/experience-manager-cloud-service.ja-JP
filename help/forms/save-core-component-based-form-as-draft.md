---
title: コアコンポーネントベースのアダプティブフォームをドラフトとして保存する方法
description: コアコンポーネントベースのアダプティブフォームをドラフトとして保存し、Forms ポータルを作成して、標準のコアコンポーネントをAEM Sites ページで使用する方法を説明します。
feature: Adaptive Forms, Core Components
source-git-commit: 494e90bd5822495f0619e8ebf55f373a26a3ffe6
workflow-type: tm+mt
source-wordcount: '1072'
ht-degree: 14%

---


<span class="preview"> この記事には、プレリリース機能のコンテンツが含まれています。 プレリリース機能には、 [プレリリースチャネル](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/release-notes/prerelease.html?lang=ja#new-features).

# コアコンポーネントベースのアダプティブフォームをドラフトとして保存 {#save-af-form}

アダプティブフォームをドラフトとして保存することは、ユーザーの効率と精度を高める上で不可欠な機能です。 この機能を使用すると、ユーザーは進行状況を保存し、入力した情報を失わずに後でタスクを完了するために戻ることができます。 次を提供：  `save-as-draft` オプションにより、時間の管理に関する柔軟性が確保され、データ消失のリスクが軽減され、送信の精度が維持されます。 フォームをドラフトとして保存して、後で完成させることができます。

## 考慮事項

* [お使いの環境でアダプティブ Forms コアコンポーネントを有効にします。](/help/forms/enable-adaptive-forms-core-components.md)

* 必ずを [コアコンポーネントはバージョン 3.0.24 以降に設定されています](https://github.com/adobe/aem-core-forms-components) この機能を使用するには、をクリックします。
* 以下が揃っていることを確認します。 [Azure ストレージアカウントとアクセスキー](https://learn.microsoft.com/en-us/azure/storage/common/storage-account-keys-manage?tabs=azure-portal) Azure ストレージアカウントへのアクセスを認証します。

## アダプティブフォームをドラフトとして保存

[!DNL Experience Manager Forms] データ統合（data-integration.md）は、 [!DNL Azure] フォームをと統合するためのストレージ設定 [!DNL Azure] ストレージサービス。 Forms フォームデータモデル（FDM）を使用して、 [!DNL Azure] サーバーでビジネスワークフローを有効にします。

フォームをドラフトとして保存するには、Azure ストレージアカウントと、へのアクセスを許可するためのアクセスキーがあることを確認します [!DNL Azure] ストレージアカウント。 フォームをドラフトとして保存するには、次の手順を実行します。

1. [Azure ストレージ設定の作成](#create-azure-storage-configuration)
1. [フォームポータル用統合ストレージコネクタの設定](#configure-usc-forms-portal)
1. [アダプティブフォームをドラフトとして保存するためのルールの作成](#rule-to-save-adaptive-form-as-draft)


### 1. Azure ストレージ設定の作成 {#create-azure-storage-configuration}

一度、Azure ストレージアカウントと、へのアクセスを許可するためのアクセスキーを持つことができます [!DNL Azure] ストレージアカウントを作成するには、次の手順を実行して Azure ストレージ設定を作成します。

1. **[!UICONTROL ツール]**／**[!UICONTROL クラウドサービス]**／**[!UICONTROL Azure ストレージ]**&#x200B;に移動します。

   ![Azure ストレージカードの選択](/help/forms/assets/save-form-as-draft-azure-card.png)

1. 設定フォルダーを選択して設定を作成し、を選択します **[!UICONTROL 作成]**.

   ![Azure ストレージ設定フォルダーを選択します](/help/forms/assets/save-form-as-draft-select-config-folder.png)

1. 「**[!UICONTROL タイトル]**」フィールドで設定のタイトルを指定します。
1. の名前を指定 [!DNL Azure] のストレージアカウント **[!UICONTROL Azure ストレージアカウント]** および **[!UICONTROL Azure アクセスキー]** フィールド。

   ![Azure ストレージ設定](/help/forms/assets/save-form-as-draft-azure-storage.png)

1. 「**保存**」をクリックします。

>[!NOTE]
>
> を取得できます **[!UICONTROL Azure ストレージアカウント]** および **[!UICONTROL Azure アクセスキー]** から [Microsoft Azure Portal](https://learn.microsoft.com/en-us/azure/storage/common/storage-account-keys-manage?tabs=azure-portal).


### 2. Forms ポータル用の統合ストレージコネクタの設定 {#configure-usc-forms-portal}

Azure ストレージ設定が正常に作成されたら、次の手順を使用してForms Portal 用の統合ストレージコネクタを設定します。

1. **[!UICONTROL ツール]**／**[!UICONTROL Forms]**／**[!UICONTROL 統合ストレージコネクタ]**&#x200B;に移動します。

   ![統合コネクタストレージ](/help/forms/assets/save-form-as-draft-unified-connector.png)

1. 「**[!UICONTROL フォームポータル]**」セクションで、「**[!UICONTROL ストレージ]**」ドロップダウンリストから「**[!UICONTROL Azure]**」を選択します。
1. 「**[!UICONTROL ストレージ設定パス]**」フィールドで、[Azure ストレージ設定の設定パス](#create-azure-storage-configuration)を指定します。

   ![統合コネクタストレージ設定](/help/forms/assets/save-form-as-draft-unified-connector-storage.png)

1. を選択 **[!UICONTROL 保存]** を選択してから、 **[!UICONTROL 公開]** をクリックして、設定を公開します。

### 3. アダプティブフォームをドラフトとして保存するためのルールを作成する {#rule-to-save-adaptive-form-as-draft}

フォームをドラフトとして保存するには、 **フォームを保存** ボタンなどのフォームコンポーネントに関するルール。 ボタンをクリックすると、ルールがトリガーされ、フォームがドラフトとして保存されます。 以下の手順を実行してを作成します **フォームを保存** ボタンコンポーネントに関するルール：

1. オーサーインスタンスで、アダプティブフォームを編集モードで開きます。
1. 左側のパネルで、 ![コンポーネントアイコン](assets/components_icon.png) を選択し、「**[!UICONTROL ボタン]**」コンポーネントをフォームにドラッグします。
1. 「**[!UICONTROL ボタン]**」コンポーネントを選択してから、![設定アイコン](assets/configure_icon.png) をクリックします。
1. 「**[!UICONTROL ルールを編集]**」アイコンを選択して、ルールエディターを開きます。
1. 「**[!UICONTROL 作成]**」を選択し、ルールを設定および作成します。
1. が含まれる **[!UICONTROL 条件]** セクションで選択 **クリックされた** および **[!UICONTROL その後]** セクションで、 **フォームを保存** オプション。
1. 「**[!UICONTROL 完了]**」を選択し、ルールを保存します。

![ボタンのルールを作成](/help/forms/assets/save-form-as-drfat-create-rule.png)

アダプティブフォームをプレビューするには、アダプティブフォームに入力し、 **フォームを保存** ボタンをクリックすると、フォームは後で使用するためにドラフトとして保存されます。

## ドラフト&amp;送信コンポーネントでAEM Sitesページにドラフトを一覧表示

AEM Formsは、次のものを提供します **ドラフトと送信** 保存済みフォームをAEM Sites ページに表示するためのポータルコンポーネントの標準搭載 この **ドラフトと送信** コンポーネントは、後で完了するためにドラフトとして保存されたフォームと、送信済みのフォームを表示します。 このコンポーネントは、ユーザーが作成したアダプティブFormsに関連するドラフトや送信を一覧表示することにより、ログインしているユーザーにパーソナライズされたエクスペリエンスを提供します。

標準のForms ポータルコンポーネントを使用して、AEM Sites ページにフォームドラフトを一覧表示できます。 を使用するには、次の手順を実行します **ドラフトと送信** ポータルコンポーネント：

1. [Forms ポータルコンポーネントのドラフトと送信を有効にする](#enable-component)
2. [ドラフト&amp;送信コンポーネントをAEM Sitesページに追加](#Add-drafts-submissions-component)
3. [下書きと送信コンポーネントの設定](#configure-drafts-submissions-component)

### 1. Forms ポータルコンポーネントのドラフトと送信を有効にする{#enable-component}

を有効にするには **[!UICONTROL ドラフトと送信]** コンポーネントをテンプレートポリシーに追加するには、次の手順を実行します。

1. でAEM Sitesページを開きます。 **編集** モード。
1. **[!UICONTROL ページ情報]**／**[!UICONTROL テンプレートを編集]**に移動します。
   ![テンプレートポリシーを編集](/help/forms/assets/save-form-as-draft-edit-template.png)

1. 「」をクリックします **[!UICONTROL ポリシー]** を選択し、 **[!UICONTROL ドラフトと送信]**  の下にあるチェックボックス **[AEM アーキタイププロジェクト名] - Formsとコミュニケーションポータル**.

   ![ポリシーの選択](/help/forms/assets/save-form-as-draft-enable-policy.png)

1. 「**[!UICONTROL 完了]**」をクリックします。

ポータルコンポーネントを有効にすると、AEM Sitesページのオーサーインスタンスで使用できるようになります。

### 2. AEM Sitesページでのドラフト&amp;送信コンポーネントの追加{#Add-drafts-submissions-component}

ポータルコンポーネントを追加して設定すると、AEM を使用して作成した web サイトでフォームポータルを作成してカスタマイズできます。必ずを [ドラフト&amp;送信コンポーネント：](#enable-component) AEM Sitesページで使用する前に以下を行います。

コンポーネントを追加するには、 **ドラフトと送信** コンポーネントペインをページ上のレイアウトコンテナに追加するか、レイアウトコンテナ上の追加アイコンを選択して、 **[!UICONTROL 新規コンポーネントを挿入]** ダイアログ。

![ドラフトと送信コンポーネントの追加](/help/forms/assets/save-form-as-draft-add-dns.png)

### 3. ドラフト&amp;送信コンポーネントの設定 {#configure-drafts-submissions-component}

この **ドラフトと送信** コンポーネントには、後で完成させるためにドラフトとして保存されたフォームと送信済みのフォームが表示されます。 を設定 **ドラフトと送信**&#x200B;は、次の手順を実行します。
1. 「」を選択します **ドラフトと送信** コンポーネント。
1. 「」をクリックします ![設定アイコン](assets/configure_icon.png) ダイアログボックスが表示されます。
1. が含まれる **[!UICONTROL ドラフトと送信]** ダイアログで、次の設定を行います。
   * **タイトル** Sites ページでコンポーネントを識別するために、デフォルトではコンポーネントの上にタイトルが表示されます。
   * **タイプ**：フォームを下書きまたは送信済みのフォームとして表示します。
   * **レイアウト**：ドラフトフォームまたは送信済みフォームをカード形式またはリスト形式で表示します。

   ![ドラフトおよび送信コンポーネントのプロパティ](/help/forms/assets/save-form-as-draft-dns-properties.png)

1. 「**完了**」をクリックします。

条件 **[!UICONTROL タイプを選択]** 次として選択 **ドラフトForms**を選択すると、ドラフトとして保存されたフォームが表示されます。
![下書きアイコン](assets/drafts-component.png)

条件 **[!UICONTROL タイプを選択]** 次として選択 **送信済みForms**&#x200B;送信されたフォームが表示されます。

![送信アイコン](assets/submission-listing.png)

それぞれのフォームをクリックしてフォームを開くことができます。

<!--

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

## 関連トピック {#see-also}

{{see-also}}



<!--

>[!MORELIKETHIS]
>
>* [Configure data sources for AEM Forms](/help/forms/configure-data-sources.md)
>* [Configure Azure storage for AEM Forms](/help/forms/configure-azure-storage.md)
>* [Integrate Microsoft Dynamics 365 and Salesforce with Adaptive Forms](/help/forms/configure-msdynamics-salesforce.md)

-->