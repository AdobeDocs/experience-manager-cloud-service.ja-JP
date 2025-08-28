---
title: AEM Forms インスタンスでアダプティブフォームまたは PDF フォームを読み込み、書き出し、整理する方法
description: アダプティブフォーム、PDF フォーム、テーマおよびその他のサポートアセットを、AEM インスタンスとの間で移行する方法について説明します。
topic-tags: forms-manager
role: Admin, User
feature: Adaptive Forms
exl-id: f5105fb7-b8c0-4656-8095-b21d392746c0
source-git-commit: edfefb163e2d48dc9f9ad90fa68809484ce6abb0
workflow-type: ht
source-wordcount: '1073'
ht-degree: 100%

---

# アダプティブフォームおよび AEM Forms アセットの読み込みと書き出し {#importing-and-exporting-assets-to-aem-forms}

| バージョン | 記事リンク |
| -------- | ---------------------------- |
| AEM 6.5 | [ここをクリックしてください](https://experienceleague.adobe.com/ja/docs/experience-manager-65/content/forms/manage-administer-aem-forms/import-export-forms-templates) |
| AEM as a Cloud Service | この記事 |

アダプティブフォームと関連アセット（アダプティブフォームテーマ、フォームデータモデル（FDM）、アダプティブフォームテンプレート、フラグメント、PDF forms など）を、[!DNL AEM Forms] インスタンス間で移動できます。

## アダプティブフォーム、PDF forms または関連アセットのダウンロード {#download-forms-amp-documents-assets}

フォームや関連アセットをダウンロードするには、以下の手順を実行します。

1. [!DNL Experience Manager Forms] インスタンスにログインします。
1. **[!UICONTROL フォーム]**／**[!UICONTROL フォームとドキュメント]**&#x200B;を選択します。

   ![Forms を選択](/help/forms/assets/select-forms.png)

1. アセットを選択し、上部パネルの&#x200B;**[!UICONTROL ダウンロード]**&#x200B;アイコンをクリックします。

   ![Forms をダウンロード](/help/forms/assets/download-form.png)

   フォームをダウンロードすると、**[!UICONTROL アセットをダウンロード]**&#x200B;ダイアログボックスが表示されます。

   ![Forms アセットをダウンロード](/help/forms/assets/download-form-assets.png)

1. 「**[!UICONTROL ダウンロード]**」をクリックします。

選択したアセットはアーカイブ（.zip ファイル）としてダウンロードされます。

## アダプティブフォーム、PDF forms または関連アセットのアップロード {#upload-forms-amp-documents-assets}

サポートされているアセットタイプを個別にまたは ZIP アーカイブとしてアップロードできます。ZIP ファイルの場合は、サポートされているすべてのアセットの相対パスが表示されます。ZIP 内の未サポートアセットは無視され、一覧には表示されません。ただし、ZIP アーカイブに未サポートアセットのみが含まれている場合は、エラーメッセージが表示され、ポップアップダイアログは表示されません。フォームや関連アセットをアップロードするには、以下の手順を実行します。

1. [!DNL Experience Manager Forms] インスタンスにログインします。
1. **[!UICONTROL フォーム]**／**[!UICONTROL フォームとドキュメント]**&#x200B;を選択します。

   ![Forms を選択](/help/forms/assets/select-forms.png)

1. **[!UICONTROL 作成]**／**[!UICONTROL ファイルのアップロード]**&#x200B;を選択します。ダイアログボックスが表示されます。

   ![Forms をアップロード](/help/forms/assets/form-upload.png)

1. ダイアログボックスで、読み込むパッケージまたはアーカイブを参照し、選択します。サポートされる他のファイルタイプを選択することもできます。「**[!UICONTROL 開く]**」を選択します。選択するフォルダーまたはファイル名に特殊文字を含めないでください。

   ダイアログボックスで、アップロードするアセットの詳細を確認し、「**[!UICONTROL アップロード]**」を選択します。

   既存のフォームアセットをアップロードすると、そのアセットが更新されます。

   >[!NOTE]
   >
   > 異なるリソースタイプと名前が競合する場合、パッケージをアップロードしても既存のフォルダー階層は置き換えられません。例えば、あるサーバーの `/content/dam/formsanddocuments` という場所に「Training」という名前のアダプティブフォームがあるとします。アダプティブフォームをダウンロードして、別のサーバーにフォームをアップロードできます。このアップロード先のサーバーにも、同じ `/content/dam/formsanddocuments` という場所に「Training」という名前のフォルダーがありました。アップロードは失敗します。

## テーマのダウンロード

他のプロジェクトやインスタンスで使用する [!DNL AEM Forms] のテーマを書き出すことができます。AEM では、テーマを zip ファイルとしてダウンロードし、それをインスタンスにアップロードできます。
テーマをダウンロードするには、以下の手順を実行します。

1. [!DNL Experience Manager Forms] オーサーインスタンスにログインします。
1. **[!UICONTROL フォーム]**／**[!UICONTROL テーマ]**&#x200B;を選択します。

   ![テーマを選択](/help/forms/assets/select-theme.png)

1. テーマページでテーマを選択し、上部パネルの&#x200B;**[!UICONTROL ダウンロード]**&#x200B;アイコンをクリックします。

   ![テーマをダウンロード](/help/forms/assets/download-theme.png)

   テーマをダウンロードすると、**[!UICONTROL アセットをダウンロード]**&#x200B;ダイアログボックスが表示されます。

   ![テーマアセットをダウンロード](/help/forms/assets/download-theme-asset.png)

1. 「**[!UICONTROL ダウンロード]**」をクリックします。

選択したアセットはアーカイブ（.zip ファイル）としてダウンロードされます。

## テーマをアップロード {#uploading-a-theme}

他のユーザーがフォームで作成したテーマをアップロードして使用できます。
テーマをアップロードするには、以下の手順を実行します。

1. [!DNL Experience Manager Forms] インスタンスにログインします。
1. Experience Manager で、**[!UICONTROL フォーム]**／**[!UICONTROL テーマ]**&#x200B;に移動します。

   ![テーマを選択](/help/forms/assets/select-theme.png)

1. テーマページで、**[!UICONTROL 作成]**／**[!UICONTROL ファイルをアップロード]**&#x200B;をクリックします。

   ![テーマをアップロード](/help/forms/assets/theme-upload.png)

1. コンピューター上のテーマパッケージを参照して選択し、「**[!UICONTROL アップロード]**」をクリックします。アップロードされたテーマは、テーマページで使用できるようになります。

## フォルダーを使用した、アダプティブフォーム、PDF forms および関連アセットの整理  {#folders-and-organizing-assets}

フォルダーを使用して、アセットのアレンジや整理を行うことができます。フォルダー内でドキュメントおよびアセットを整理すると、ファイルをグループ化して容易に管理できます。フォルダーを選択し、ダウンロードするか削除するかを選択できます。

### フォルダーを作成 {#create-a-folder}

フォルダーを作成するには、以下の手順を実行します。

1. [!DNL Experience Manager Forms] インスタンスにログインします。
1. **[!UICONTROL フォーム]**／**[!UICONTROL フォームとドキュメント]**&#x200B;を選択します。

   ![フォームを選択](/help/forms/assets/select-forms.png)

1. **[!UICONTROL 作成]**／**[!UICONTROL フォルダー]**&#x200B;を選択します。

   ![フォルダーを作成](/help/forms/assets/create-folder.png)

   **[!UICONTROL フォルダーを追加]**&#x200B;ダイアログボックスが表示されます。
1. **[!UICONTROL タイトル]**&#x200B;を入力します。**[!UICONTROL タイトル]**&#x200B;を入力すると、**[!UICONTROL 名前]**&#x200B;が自動的に入力されます。

   ![フォルダーを追加](/help/forms/assets/add-folder.png)

1. 「**[!UICONTROL 作成]**」をクリックします。

   >[!NOTE]
   >
   >デフォルトでは、名前フィールドの値は、タイトルから自動入力されます。名前には、英数字、ハイフン（-）、下線（_）のみを含めることができます。タイトルにその他の特殊文字を入力すると、それらは自動的にハイフンに置換され、この新しい名前を確認するよう指示されます。提示された名前をそのまま使用するか、またはそれを編集できます。

定義したタイトルを持つ新しいフォルダーは、アセットリスト内の現在の場所に表示されます。

指定した名前を持つフォルダーが既に存在する場合は、送信はエラーになり失敗します。名前フィールドの横に表示されるエラー ![aem6forms_error_alert](assets/Smock_Alert_18_N.svg) アイコンの上にマウスポインターを置くと、エラーメッセージを見ることができます。

作成されたフォルダーを選択してフォルダー内に移動し、フォルダー内でアセットまたはフォルダーを作成できます。さらに、フォルダーを選択し、ダウンロードのキューに入れるか、削除するか、名前を編集するかを選択できます。

### 1 つまたは複数のアセットのコピーを作成 {#create-copies-of-one-or-more-assets-or-letters}

既存のアセットを使用して、類似のプロパティ、コンテンツ、継承されたアセットを持つアセットをすばやく作成できます。

アセットのコピーを作成するには、以下の手順を実行します。

1. [!DNL Experience Manager Forms] インスタンスにログインします。
1. 関連するアセットページで、1 つまたは複数のアセットを選択します。UI に&#x200B;**[!UICONTROL コピー]**&#x200B;アイコンが表示されます。
1. 「**[!UICONTROL コピー]**」を選択します。UI に![ペースト](/help/forms/assets/Smock_Paste_18_N.svg)アイコンが表示されます。

   ![アセットをコピー](/help/forms/assets/copy-asset.png)

   貼り付ける前に、フォルダー内に移動することもできます。複数のフォルダーに同じ名前のアセットを保管できます。フォルダーについて詳しくは、[フォルダーとアセットの整理](#folders-and-organizing-assets)を参照してください。
1. 「**[!UICONTROL ペースト]**」を選択します。

   ![アセットをペースト](/help/forms/assets/paste-asset.png)

1. **[!UICONTROL ペースト]**&#x200B;ダイアログが表示されます。アセットの新しいコピーに自動的に名前とタイトルが生成されますが、アセットのタイトルと名前は編集できます。

   同じ場所にアセットをコピー＆ペーストする場合、`asset` の既存の名前の末尾に「-CopyXX」のサフィックスが追加されます。コピーされたアセットにタイトルが存在しない場合、自動生成されたタイトルフィールドは空白のままです。

   ![新しい場所でアセットをペースト](/help/forms/assets/paste-click-asset.png)

   必要に応じて、アセットのコピーを保存する際の&#x200B;**[!UICONTROL タイトル]**&#x200B;を編集します。**[!UICONTROL タイトル]**&#x200B;を入力すると、**[!UICONTROL 名前]**&#x200B;が自動的に入力されます。
1. 「**[!UICONTROL ペースト]**」を選択します。コピーされたアセットの新しいコピーが作成されます。

## 検索 {#search-forms}

アセットの数が多い場合、適切なアセットの検索には時間がかかります。アセットページで特定のアセットに対してテキストベースの検索を実行できます。

アセットを検索するには、以下の手順を実行します。

1. [!DNL Experience Manager Forms] インスタンスにログインします。
1. ![検索アイコン ](assets/folder-search-icon.svg) 検索アイコンをクリックします。

   ![検索フォーム](/help/forms/assets/search-form.png)

1. 検索バーに検索するアセットの名前を入力します。

1. 関連するアセットのリストが表示されます。表示されたアセットリストから目的のアセットを選択します。

   ![アセットの検索](/help/forms/assets/search-bar.png)

検索の使用に関する詳細および手順について詳しくは、[検索](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/operations/indexing.html?lang=ja)を参照してください。

<!--
## Export or create a package {#export-a-workflow-application}

You can use packages to install new content, install new functionality, transfer content between instances, and back up content.
To export or create a package:

1. Log in to your [!DNL Experience Manager Forms] instance.
1. Navigate to **[!UICONTROL Tools]** ![hammer](assets/hammer.png) &gt; **[!UICONTROL Deployment]** &gt; **[!UICONTROL Packages]**.

   ![Package Manager](/help/forms/assets/package-manager.png)

1. Click **[!UICONTROL Create Package]**.

   ![Create package](/help/forms/assets/create-package.png)   
   
   When **[!UICONTROL Create Package]** is clicked, the **[!UICONTROL New Package]** dialog box appears.
1. Specify the package name, version, and group for the package. 
   
   ![New package](/help/forms/assets/new-package.png)  

   * **Package Name** - Select a descriptive name to help you identify the contents of the package.

   * **Version** - It is a textual field to indicate a version. This is appended to the package name to form the name of the zip file.

   * **Group** - This is the target group (or folder) name. Groups help you organize your packages. A folder is created for the group if it does not already exist. If you leave the group name blank, it creates the package in the main package list.

1. Click **[!UICONTROL OK]**.

   Once the package is created, it appears at the top of the list of packages.

1. Click **[!UICONTROL Edit]**.
   
   ![Edit Package](/help/forms/assets/edit-package.png)
    
1. Open the **[!UICONTROL Filters]** tab.
   
   ![Open filter tab](/help/forms/assets/add-filter-package.png)
   
1.  Click **[!UICONTROL Add Filter]**. 
   
      ![Add filter](/help/forms/assets/add-filter.png)

      You can specify the path of the package. You can also add rules and other validations for the package.

      ![Add path](/help/forms/assets/add-path.png)

1. Click **[!UICONTROL Save]** after you are finished editing the settings.
1. Click **[!UICONTROL Build]** to create the package.
    
     ![Build path](/help/forms/assets/build-package.png)

   After the package is built, you can download the package and import it to the other server. The workflow application appears on the server where the package is uploaded.

   >[!NOTE]
   >
   >For the workflow application to work properly, also export the corresponding Adaptive Form and workflow model with the work application.

   Once a package is uploaded to AEM, you can modify its settings. You can also download or delete the package.

## Import and export assets in Correspondence Management {#import-and-export-assets-in-correspondence-management}

To share assets, such as data dictionaries, letters, and document fragments, between two different implementations of Correspondence Management, you can create and share .cmp files. A .cmp file can include one or more data dictionaries, letters, document fragments, and forms.

### Export Document Fragments, Letters, and/or Data Dictionaries {#export-document-fragments-letters-and-or-data-dictionaries}

1. In the letters, document fragments, or data dictionary pages, select and select the assets you want to export to a single package, and then select Queue For Download. The assets are lined-up for export.
1. As required, repeat the above step to add letters, document fragments, and data dictionaries.
1. Select **Download**.
1. Correspondence Management displays Download Asset(s) dialog with a list of assets in the export list.

   ![export](assets/export.png)

1. To view the dependencies that are exported, Select Resolve. Or skip to the next step. Even if you do not select resolve, the dependencies are still exported.
1. To download the .cmp file, select **OK**.
1. Correspondence Management downloads a .cmp file to your computer.

   The .cmp file includes the exported assets. You can share the .cmp file with others. Other users can import the .cmp file in a different server to get all the assets in the new server.

### Export all the Correspondence Management assets as a package {#export-all-the-correspondence-management-assets-as-a-package}

Use this option to download all the Correspondence Management assets and related dependencies as a package from an [!DNL AEM Forms] instance.

For example, if Correspondence Management has a letter that uses an image and text, the downloaded package also contains the image and the text related to the letter. All the metadata properties (including custom properties) associated with the asset are also downloaded. Once you have downloaded the package (.cmp), you can [import the package to a different [!DNL AEM Forms] instance](import-export-forms-templates.md#p-upload-forms-documents-assets-p).

To download all the Correspondence Management assets and related dependencies as a package, complete the following steps:

1. Log in to [!DNL AEM Forms] server as a forms user.
1. Select **Adobe Experience Manager** in the Global Navigation bar.
1. Select tools ( ![tools](assets/tools.png)) and then select **Forms**.
1. Select **Export Correspondence Management Assets**.

   ![publish-cmp-assets-1](assets/publish-cmp-assets-1.png)

   ( ``The Export All Correspondence Management Assets page appears and displays the information about the last time the Export process was attempted and a link to download the last successfully exported package.

   ![export-last-run-details](assets/export-last-run-details.png)

1. Select **Export** and, in the confirm message, select **OK**.

   After a batch process is complete, the last run details and the link to download the package are updated. This includes information such as the Administrator login and if the batch run successfully or failed. The assets are exported to a package and the Download Exported Package link appears.

   >[!NOTE]
   >
   >The Export All Assets process cannot be canceled once initiated. Also, while the export all operation is in process, do not create, delete, modify, or publish any assets or initiate Publish All Assets process.a

1. Select the **Download Exported Package** link to download the package file.

   To add the assets in the package to another instance of Correspondence Management, [import the package to an [!DNL AEM Forms] instance](import-export-forms-templates.md#p-upload-forms-documents-assets-p).

<!-- ### Import Document Fragments, Letters and/or Data Dictionaries into Correspondence Management {#import-document-fragments-letters-and-or-data-dictionaries-into-correspondence-management}

You can import assets that are exported into a .cmp file. A .cmp file can have one or more letters, data dictionaries, document fragments, and dependent assets.

>[!NOTE]
>
>While importing old Correspondence Management assets for migration, log in using an Admin account. For more information on Migrating old Correspondence Management assets, see [Migrate Correspondence Management assets to AEM 6.1 forms](migration-utility.md).

1. On the data dictionary, letters, or document fragments page, select **Create &gt; File Upload** and select the .cmp file.
1. Correspondence Management displays the Import Assets dialog with the list of assets that are imported. Select **Import**.

   After importing the assets, the following properties of the assets are updated while the other properties remain the same:

    * Author: Displays the ID of the user that imported the asset to the server
    * Modified: The time when the asset was imported to the server

   >[!NOTE]
   >
   >For you to be able to upload XDPs (as part of the cmp file or otherwise), you need to be a part of forms-power-users group. For access rights, contact the administrator. -->

## 関連トピック {#see-also}

{{see-also}}
