---
title: アダプティブフォーム、PDF forms、およびその他のアセットの読み込み、書き出し、整理
seo-title: Learn to import, export, and organize Adaptive Forms, PDF forms, and other assets on an[!DNL AEM Forms] instance
description: 'アダプティブフォームとアセットを AEM インスタンス間で移行したいと考えていますか？ここでは、 [!DNL AEM Forms]  インスタンスからアダプティブフォーム、PDF フォーム、テーマおよびその他のサポートするアセットを読み込んだり書き出したりする方法を説明します。 '
seo-description: Looking to migrate Adaptive Forms and assets to and from an AEM instances? Learn here how to import and export Adaptive Forms, PDF forms, themes, and other supporting assets from an [!DNL AEM Forms] instance.
topic-tags: forms-manager
exl-id: f5105fb7-b8c0-4656-8095-b21d392746c0
source-git-commit: 7163eb2551f5e644f6d42287a523a7dfc626c1c4
workflow-type: tm+mt
source-wordcount: '1211'
ht-degree: 100%

---

# アダプティブフォーム、PDF フォームおよびその他のアセットの読み込み、書き出し、整理{#importing-and-exporting-assets-to-aem-forms}

アダプティブフォームと関連アセット（アダプティブフォームテーマ、フォームデータモデル、アダプティブフォームテンプレート、ドキュメントフラグメント、PDF フォームなど）を、[!DNL AEM Forms] インスタンス間で移動できます。CRX パッケージまたはバイナリファイル形式のアセットの読み込みと書き出しを行うことができます。

アダプティブフォームを書き出しても、コンテンツポリシーとテンプレートは書き出されません。このようなアセットを書き出すには、[パッケージマネージャー](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/deploying/overview.html?lang=ja#how-rolling-deployments-work)を使用します。

## アダプティブフォーム、PDF forms または関連アセットのダウンロード {#download-forms-amp-documents-assets}

フォームや関連アセットをダウンロードするには、以下の手順を実行します。

1. [!DNL AEM Forms] インスタンスにログインします。
1. **[!UICONTROL Adobe Experience Manager]** ![adobeexperiencemanager](assets/adobeexperiencemanager.png) アイコン／**[!UICONTROL ナビゲーション]** ![コンパス](assets/Smock_Compass_18_N.svg) アイコン／**[!UICONTROL フォーム]**／**[!UICONTROL フォームとドキュメント]**&#x200B;をタップします。
1. アセットを選択し、「**[!UICONTROL ダウンロード]**」アイコンをタップします。
1. 「アセットをダウンロード」で、以下のいずれかのオプションを選択し、「**[!UICONTROL ダウンロード]**」をタップします。

   * 「**CRX パッケージとしてダウンロード**」：選択したすべてのアセットおよび関連する依存関係を [!DNL AEM Forms] インスタンスからダウンロードして、別のインスタンスに移動するオプションを使用します。AEM（アダプティブフォームおよびアダプティブフォームフラグメント）、フォームセット、フォームデータモデル、フォームテンプレート、PDF ドキュメント、参照リソース（XSD および画像）で作成されたフォームを含む、すべてのアセットとフォルダーを CRX パッケージとしてダウンロードします。
アセットをパッケージとしてダウンロードすることのメリットは、選択したアセットから参照されるアセットもダウンロードできる点です。例えば、フォームテンプレート、XSD および画像を使用するアダプティブフォームがあるとします。このアダプティブフォームを選択してパッケージとしてダウンロードする場合、ダウンロードされたパッケージには、フォームテンプレート、XSD および画像も含まれています。そのアセットに関連付けられているすべてのメタデータプロパティ（カスタムプロパティを含む）も同様にダウンロードされます。

   * 「**アセットをバイナリファイルとしてダウンロード**」：このオプションを使用して、フォームテンプレート（XDP）、PDF forms（PDF）、ドキュメント（PDF）、リソース（画像、スキーマ、スタイルシート）のみをダウンロードします。これらのアセットは、外部アプリケーションで編集できます。バイナリ（画像、PDF、その他のサポートされている形式など）を持つアセットを .zip ファイルとしてダウンロードします。
「**[!UICONTROL アセットをバイナリファイルとしてダウンロード]**」オプションを使用して、アダプティブフォーム、アダプティブフォームフラグメント、テーマおよびフォームセットをダウンロードすることはできません。これらのアセットをダウンロードするには、「**[!UICONTROL CRX パッケージとしてダウンロード]**」オプションを使用する必要があります。

   選択したアセットはアーカイブ（.zip ファイル）としてダウンロードされます。

   >[!NOTE]
   >
   >AEM パッケージとバイナリファイルはどちらもアーカイブ（.zip ファイル）としてダウンロードされます。アセットと一緒にアセット用のテンプレートがダウンロードされることはありません。アセット用のテンプレートは、個別に書き出す必要があります。

## アダプティブフォーム、PDF forms または関連アセットのアップロード {#upload-forms-amp-documents-assets}

サポートされているアセットタイプを個別にまたは ZIP アーカイブとしてアップロードできます。ZIP ファイルの場合は、サポートされているすべてのアセットの相対パスが表示されます。ZIP 内の未サポートアセットは無視され、一覧には表示されません。ただし、ZIP アーカイブに未サポートアセットのみが含まれている場合は、エラーメッセージが表示され、ポップアップダイアログは表示されません。フォームや関連アセットをアップロードするには、以下の手順を実行します。

1. [!DNL AEM Forms] インスタンスにログインします。
1. **[!UICONTROL Adobe Experience Manager]** ![adobeexperiencemanager](assets/adobeexperiencemanager.png) アイコン／**[!UICONTROL ナビゲーション]** ![コンパス](assets/Smock_Compass_18_N.svg) アイコン／**[!UICONTROL フォーム]**／**[!UICONTROL フォームとドキュメント]**&#x200B;をタップします。
1. **[!UICONTROL 作成]**／**[!UICONTROL ファイルのアップロード]**&#x200B;をタップします。ダイアログボックスが表示されます。
1. ダイアログボックスで、読み込むパッケージまたはアーカイブを参照し、選択します。サポートされる他のファイルタイプを選択することもできます。「**[!UICONTROL 開く]**」をタップします。選択するフォルダーまたはファイル名に特殊文字を含めないでください。

   ダイアログボックスで、アップロードするアセットの詳細を確認し、「**[!UICONTROL アップロード]**」をタップします。

   既存のフォームアセットをアップロードすると、そのアセットが更新されます。

   >[!NOTE]
   >
   > * 異なるリソースタイプと名前が競合する場合、パッケージをアップロードしても既存のフォルダー階層は置き換えられません。例えば、あるサーバーの /content/dam/formsanddocuments という場所に「Training」という名前のアダプティブフォームがあるとします。ユーザーがそのアダプティブフォームをダウンロードし、他のサーバー上にアップロードします。このアップロード先のサーバーにも、同じ /content/dam/formsanddocuments に「Training」という名前のフォルダーがありました。アップロードは失敗します。
   > * `form-power-user` グループのメンバーのみが XDP ファイルをアップロードできます。



## テーマのダウンロード {#downloading-a-theme}

他のプロジェクトやインスタンスで使用する [!DNL AEM Forms] のテーマを書き出すことができます。AEM では、テーマを zip ファイルとしてダウンロードし、それをインスタンスにアップロードできます。

テーマをダウンロードするには、以下の手順を実行します。

1. [!DNL AEM Forms] インスタンスにログインします。
1. **[!UICONTROL Adobe Experience Manager]** ![adobeexperiencemanager](assets/adobeexperiencemanager.png) アイコン／**[!UICONTROL ナビゲーション]** ![コンパス](assets/Smock_Compass_18_N.svg) アイコン／**[!UICONTROL フォーム]**／**[!UICONTROL テーマ]**&#x200B;をタップします。
1. テーマを選択し、「**[!UICONTROL ダウンロード]**」をタップします。テーマはアーカイブ（.zip ファイル）としてダウンロードされます。

## テーマのアップロード {#uploading-a-theme}

他のユーザーがフォームで作成したテーマをアップロードして使用できます。テーマをアップロードするには、以下の手順を実行します。

1. Experience Manager で、**[!UICONTROL フォーム]**／**[!UICONTROL テーマ]**&#x200B;に移動します。
1. テーマページで、**[!UICONTROL 作成]**／**[!UICONTROL ファイルのアップロード]**&#x200B;をクリックします。
1. ファイルのアップロードプロンプトで、コンピューター上のテーマパッケージを参照して選択し、「**[!UICONTROL アップロード]**」をクリックします。アップロードされたテーマは、テーマページで使用できます。

<!-- ## Import and export assets in Correspondence Management {#import-and-export-assets-in-correspondence-management}

To share assets, such as data dictionaries, letters, and document fragments, between two different implementations of Correspondence Management, you can create and share .cmp files. A .cmp file can include one or more data dictionaries, letters, document fragments, and forms.

### Export Document Fragments, Letters, and/or Data Dictionaries {#export-document-fragments-letters-and-or-data-dictionaries}

1. In the letters, document fragments, or data dictionary pages, tap and select the assets you want to export to a single package, and then tap Queue For Download. The assets are lined-up for export.
1. As required, repeat the above step to add letters, document fragments, and data dictionaries.
1. Tap **Download**.
1. Correspondence Management displays Download Asset(s) dialog with a list of assets in the export list.

   ![export](assets/export.png)

1. To view the dependencies that are exported, Tap Resolve. Or skip to the next step. Even if you do not tap resolve, the dependencies are still exported.
1. To download the .cmp file, tap **OK**.
1. Correspondence Management downloads a .cmp file to your computer.

   The .cmp file includes the exported assets. You can share the .cmp file with others. Other users can import the .cmp file in a different server to get all the assets in the new server.

### Export all the Correspondence Management assets as a package {#export-all-the-correspondence-management-assets-as-a-package}

Use this option to download all the Correspondence Management assets and related dependencies as a package from an [!DNL AEM Forms] instance.

For example, if Correspondence Management has a letter that uses an image and text, the downloaded package also contains the image and the text related to the letter. All the metadata properties (including custom properties) associated with the asset are also downloaded. Once you have downloaded the package (.cmp), you can [import the package to a different [!DNL AEM Forms] instance](import-export-forms-templates.md#p-upload-forms-documents-assets-p).

To download all the Correspondence Management assets and related dependencies as a package, complete the following steps:

1. Log in to [!DNL AEM Forms] server as a forms user.
1. Tap **Adobe Experience Manager** in the Global Navigation bar.
1. Tap tools ( ![tools](assets/tools.png)) and then tap **Forms**.
1. Tap **Export Correspondence Management Assets**.

   ![publish-cmp-assets-1](assets/publish-cmp-assets-1.png)

   ( ``The Export All Correspondence Management Assets page appears and displays the information about the last time the Export process was attempted and a link to download the last successfully exported package.

   ![export-last-run-details](assets/export-last-run-details.png)

1. Tap **Export** and, in the confirm message, tap **OK**.

   After a batch process is complete, the last run details and the link to download the package are updated. This includes information such as the Administrator login and if the batch run successfully or failed. The assets are exported to a package and the Download Exported Package link appears.

   >[!NOTE]
   >
   >The Export All Assets process cannot be canceled once initiated. Also, while the export all operation is in process, do not create, delete, modify, or publish any assets or initiate Publish All Assets process.a

1. Tap the **Download Exported Package** link to download the package file.

   To add the assets in the package to another instance of Correspondence Management, [import the package to an [!DNL AEM Forms] instance](import-export-forms-templates.md#p-upload-forms-documents-assets-p).

<!-- ### Import Document Fragments, Letters and/or Data Dictionaries into Correspondence Management {#import-document-fragments-letters-and-or-data-dictionaries-into-correspondence-management}

You can import assets that are exported into a .cmp file. A .cmp file can have one or more letters, data dictionaries, document fragments, and dependent assets.

>[!NOTE]
>
>While importing old Correspondence Management assets for migration, log in using an Admin account. For more information on Migrating old Correspondence Management assets, see [Migrate Correspondence Management assets to AEM 6.1 forms](migration-utility.md).

1. On the data dictionary, letters, or document fragments page, tap **Create &gt; File Upload** and select the .cmp file.
1. Correspondence Management displays the Import Assets dialog with the list of assets that are imported. Tap **Import**.

   After importing the assets, the following properties of the assets are updated while the other properties remain the same:

    * Author: Displays the ID of the user that imported the asset to the server
    * Modified: The time when the asset was imported to the server

   >[!NOTE]
   >
   >For you to be able to upload XDPs (as part of the cmp file or otherwise), you need to be a part of forms-power-users group. For access rights, contact the administrator. -->

## ワークフローアプリケーションの書き出し {#export-a-workflow-application}

パッケージマネージャーを使用して、ワークフローアプリケーションを書き出すことができます。手順を以下に示します。

1. [!DNL AEM Forms] パッケージマネージャーを開きます。パッケージマネージャーの URL は `https://[server]:[port]/crx/packmgr` です。
1. 「**[!UICONTROL パッケージを作成]**」をクリックします。**[!UICONTROL 新規パッケージ]**&#x200B;ダイアログボックスが表示されます。
1. パッケージの名前、バージョン、グループを指定します。「**[!UICONTROL OK]**」をクリックします。
1. 「**[!UICONTROL 編集]**」をクリックし、「**[!UICONTROL フィルター]**」タブを開きます。「**[!UICONTROL フィルターを追加]**」をクリックします。ワークフローアプリケーションのパスを指定します。例えば、/etc/fd/dashboard/startpoints/homemortgage などです。「**[!UICONTROL ルールを追加]**」をクリックします。

1. 「**[!UICONTROL 詳細]**」タブを開きます。ACL Handling フィールドで、「**[!UICONTROL 結合]**」または「**[!UICONTROL 上書き]**」を選択します。「**[!UICONTROL 保存]**」をクリックします。
1. 「**[!UICONTROL ビルド]**」をクリックし、パッケージを作成します。

   パッケージが作成されたら、パッケージをダウンロードして別のサーバーに読み込むことができます。パッケージがアップロードされるサーバーにワークフローアプリケーションが表示されます。

   >[!NOTE]
   >
   >ワークフローアプリケーションを正しく動作させるために、作業アプリケーションを使用して対応するアダプティブフォームとワークフローモデルも書き出します。

## フォルダーを使用した、アダプティブフォーム、PDF forms および関連アセットの整理  {#folders-and-organizing-assets}

フォルダーを使用して、アセットのアレンジや整理を行うことができます。フォルダー内でドキュメントおよびアセットを整理すると、ファイルをグループ化して容易に管理できます。フォルダーを選択し、ダウンロードするか削除するかを選択します。フォルダーを作成するには、以下の手順を実行します。

### フォルダーの作成 {#create-a-folder}

1. [!DNL AEM Forms] インスタンスにログインします。
1. Experience Manager ![adobeexperiencemanager](assets/adobeexperiencemanager.png) アイコン／ナビゲーション ![コンパス](assets/Smock_Compass_18_N.svg) アイコン／**[!UICONTROL フォーム]**／**[!UICONTROL フォームとドキュメント]**&#x200B;をタップします。
1. **[!UICONTROL 作成]**／**[!UICONTROL フォルダー]**&#x200B;をタップします。
1. 以下の詳細を入力します。

   * **[!UICONTROL タイトル]**：フォルダーの表示名
   * **[!UICONTROL 名前]**：*（必須）*&#x200B;リポジトリー内のフォルダーを保存するノード名

   >[!NOTE]
   >
   >デフォルトでは、名前フィールドの値は、タイトルから自動入力されます。名前には、英数字、ハイフン（-）、下線（_）のみを含めることができます。タイトルにその他の特殊文字を入力すると、それらは自動的にハイフンに置換され、この新しい名前を確認するよう指示されます。提示された名前をそのまま使用するか、またはそれを編集できます。

1. 定義したタイトルを持つ新しいフォルダーは、アセットリスト内の現在の場所に表示されます。

   指定した名前を持つフォルダーが既に存在する場合は、送信はエラーになり失敗します。名前フィールドの横に表示されるエラー ![aem6forms_error_alert](assets/Smock_Alert_18_N.svg) アイコンの上にマウスポインターを置くと、エラーメッセージを見ることができます。

   新しく作成されたフォルダーをタップしてフォルダー内に移動し、フォルダー内でアセットまたはフォルダーを作成できます。さらに、フォルダーを選択し、ダウンロード、削除、名前の編集用にそのフォルダーをキューに入れることができます。


<!-- ### Create copies of one or more assets or letters {#create-copies-of-one-or-more-assets-or-letters}

You can use an existing assets to quickly create an asset with similar properties, content, and inherited assets.

Complete the following steps to create copies of assets and letters:

1. On the relevant assets page, select one or more assets. The UI displays the Copy icon.
1. Tap **[!UICONTROL Copy]**. The UI displays the **[!UICONTROL Paste]** icon. You can also choose to go/navigate inside a folder before you paste. Different folders can contain assets with same names. For more information on folders, see [Folders and organizing assets](#folders-and-organizing-assets).
1. Tap **[!UICONTROL Paste]**. The **[!UICONTROL Paste]** dialog appears. The system auto generates names and titles to the new copies of assets/letters, but you can edit the titles and names of the assets/letters.

   If you are copying and pasting the assets/letters at the same place, a suffix "-CopyXX" gets added to the existing name of the asset/letter. If no title existed for the copied asset/letter, the auto generated title field remains blank.

1. If required, edit the Title and Name with which you want to save the copy of the asset/letter.
1. Tap **[!UICONTROL Paste]**. New copies of the copied assets are created.

## Search {#search-forms}

You ca use the top bar **[A]** to search your content. When you search for assets, a side panel is displayed. You can also tap ![assets-browser-content-only](assets/assets-browser-content-only.png) &gt; Filter **[B]** to invoke the side panel. Using the various filters in the side panel, you can narrow down your search. The side panel also allows you to save your searches.

![search_topbar](assets/search_topbar.png)

**A.** Search **B.** Filter

![Side panel - Filters](assets/search_sidepanel.png)

Side panel - Filters

On the side panel, you can use the following to narrow down your search results:

* Search Directory
* Tags
* Search Criteria; for example, Modified Dates, Publish Status, LiveCopy Status.

The side panel also allows you to save your search settings with names of your choice.

For more information and instructions on using search, filters, saved search, and side panel, see [Search](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/operations/indexing.html). -->
