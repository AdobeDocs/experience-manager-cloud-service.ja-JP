---
Title: How to integrate Adaptive Form to a SharePoint Document Library?
Description: This article explains how to send data from your Adaptive Form to a SharePoint  Document library when you submit the form.
keywords: アダプティブフォーム用にSharePoint ドキュメントライブラリを接続する方法、SharePointに送信する方法、SharePoint ドキュメントライブラリ設定を作成する方法、アダプティブフォームで「SharePointに送信」送信アクションを使用する方法、AEM Forms データモデル SharePoint ドキュメントライブラリ、Forms データモデル SharePoint ドキュメントライブラリ、Forms データモデルをSharePoint ドキュメントライブラリに統合する方法
feature: Adaptive Forms, Core Components, Foundation Components, Edge Delivery Services
role: User, Developer
exl-id: a00b4a93-2324-4c2a-824f-49146dc057b0
source-git-commit: c0df3c6eaf4e3530cca04157e1a5810ebf5b4055
workflow-type: tm+mt
source-wordcount: '964'
ht-degree: 63%

---

# Microsoft® SharePoint ドキュメントライブラリへのアダプティブフォームの接続 {#connect-af-sharepoint-doc-library}

>[!VIDEO](https://video.tv.adobe.com/v/3444368/formautomation-productivitytools-adaptiveforms--sharepointintegration-documentlibrary/?quality=12&learn=on)

アダプティブフォームで「**[!UICONTROL SharePoint ドキュメントライブラリに送信]**」送信アクションを使用するには、次の手順に従います。

1. [SharePoint ドキュメントライブラリ設定の作成](#1-create-a-sharepoint-document-library-configuration)：AEM フォームを Microsoft Sharepoint ストレージに接続します。
2. [アダプティブフォームでの「SharePoint に送信」送信アクションの使用](#2-use-sharepoint-document-library-configuration-in-an-adaptive-form)：アダプティブフォームを設定済みの Microsoft® SharePoint に接続します。

## &#x200B;1. SharePoint ドキュメントライブラリ設定を作成する

AEM Forms を Microsoft® Sharepoint ドキュメントライブラリストレージに接続するには、次の手順に従います。

1. **AEM Forms オーサー**&#x200B;インスタンス／**[!UICONTROL ツール]**／**[!UICONTROL Cloud Services]**／**[!UICONTROL Microsoft® SharePoint]** に移動します。
1. **[!UICONTROL Microsoft® SharePoint]** を選択すると、**[!UICONTROL SharePoint ブラウザー]**&#x200B;にリダイレクトされます。
1. **設定コンテナ**&#x200B;を選択します。設定は、選択した設定コンテナに保存されます。
1. クリック **[!UICONTROL 作成]** > **[!UICONTROL SharePoint Document Library]** 」をドロップダウンリストから選択します。 SharePoint 設定ウィザードが表示されます。

   ![SharePoint の設定](/help/forms/assets/sharepoint_configuration.png)

1. 「**[!UICONTROL タイトル]**」、「**[!UICONTROL クライアント ID]**」、「**[!UICONTROL クライアント秘密鍵]**」および「**[!UICONTROL OAuth URL]**」を指定します。OAuth URL のクライアント ID、クライアントの秘密鍵、テナント ID を取得する方法について詳しくは、[Microsoft® のドキュメント](https://learn.microsoft.com/ja-jp/graph/auth-register-app-v2)を参照してください。
   * アプリの `Client ID` と `Client Secret` は Microsoft® Azure Portal から取得できます。
   * Microsoft® Azure Portal で、リダイレクト URI を `https://[author-instance]/libs/cq/sharepoint/content/configurations/wizard.html` として追加します。`[author-instance]` をオーサーインスタンスの URL に置き換えます。
   * 読み取り／書き込み権限を付与するには、API 権限 `offline_access` と `Sites.Manage.All` を追加します。`Sites.Manage.All` は、Microsoft の Graph API の権限範囲で、Sites の削除や変更など、SharePoint サイトのすべての側面を管理する機能をアプリケーションに付与します。

     >[!NOTE]
     >
     > また、Microsoft の Graph API の `Sites.Selected` 権限範囲を使用して、[制限付きアクセスで SharePoint サイトを設定](/help/forms/configure-sharepoint-site-limited-access.md)することもできます。`Sites.Selected` は、SharePoint サイトへのより詳細な制限付きアクセスを可能にする Microsoft の Graph API の権限範囲です。

   * OAuth URL `https://login.microsoftonline.com/tenant-id/oauth2/v2.0/authorize` を使用します。`<tenant-id>` を Microsoft® Azure Portal のアプリの `tenant-id` に置き換えます。

     >[!NOTE]
     >
     > **クライアント秘密鍵**&#x200B;フィールドは、Azure Active Directory アプリケーションの設定に応じて、必須またはオプションになります。アプリケーションでクライアント秘密鍵を使用するように設定されている場合は、クライアントの秘密鍵を指定する必要があります。

1. Microsoft Graph API の `offline_access Sites.Selected` の権限範囲により、SharePoint サイトへのさらに詳細な制限されたアクセスが可能になります。 SharePoint サイトへのフルアクセスを可能にする、Microsoft Graph API の `offline_access Sites.Manage.All` の権限範囲。
1. 「**[!UICONTROL 接続]**」をクリックします。接続に成功した場合、`Connection Successful` のメッセージが表示されます。

1. **SharePoint サイト**／**ドキュメントライブラリ**／**SharePoint フォルダー**&#x200B;を選択して、データを保存します。

   >[!NOTE]
   >
   >* デフォルトでは、`forms-ootb-storage-adaptive-forms-submission` は選択した SharePoint サイトに存在します。
   >* 選択した SharePoint サイトの `Documents` ライブラリにまだ存在しない場合は、「**フォルダーを作成**」をクリックして、フォルダーを `forms-ootb-storage-adaptive-forms-submission` として作成します。

アダプティブフォームの送信アクションに、この SharePoint サイト設定を使用できるようになりました。

### &#x200B;2. アダプティブフォームでのSharePoint ドキュメントライブラリ設定の使用

アダプティブフォームで作成したSharePoint ドキュメントライブラリ設定を使用して、データまたは生成されたレコードのドキュメントをSharePoint フォルダーに保存できます。

>[!NOTE]
>
> * SharePoint ドキュメントライブラリストレージを作成したアダプティブフォームと同じ[!UICONTROL 設定コンテナ]を選択します。
> * [!UICONTROL 設定コンテナ]が選択されていない場合、グローバルな[!UICONTROL ストレージ設定]フォルダーが送信アクションのプロパティウィンドウに表示されます。

>[!BEGINTABS]

>[!TAB 基盤コンポーネント]

基盤コンポーネントに基づくアダプティブフォームでSharePoint ドキュメントライブラリのストレージ設定を使用するには、次の手順を実行します。

1. 編集用にアダプティブフォームを開き、アダプティブフォームのコンテナプロパティの「**[!UICONTROL 送信]**」セクションに移動します。
1. **[!UICONTROL 送信アクション]** ドロップダウンリストから、「**送信アクション**」を **[!UICONTROL SharePointに送信]** として選択します。
   ![SharePoint GIF](/help/forms/assets/submit-to-sharepoint-fc.png){width=50%}
1. データを保存する場所に「**[!UICONTROL ストレージ設定]**」を選択します。
1. 「**[!UICONTROL 保存]**」をクリックして、送信設定を保存します。

>[!NOTE]
>
> * フォームを送信すると、データは指定したMicrosoft® Sharepoint Document Library ストレージに保存されます。 データを保存するフォルダー構造は `/folder_name/form_name/year/month/date/submission_id/data` です。
> * 添付ファイルは、`/folder_name/form_name/year/month/date/submission_id/data` ディレクトリにも保存されます。ただし、「**添付ファイルを元の名前で保存**」を選択した場合、添付ファイルは元のファイル名を使用してフォルダーに保存されます。

>[!TAB コアコンポーネント]

コアコンポーネントに基づくアダプティブフォームでSharePoint ドキュメントライブラリのストレージ設定を使用するには、次の手順を実行します。

1. コンテンツブラウザーを開き、アダプティブフォームの&#x200B;**[!UICONTROL ガイドコンテナ]**&#x200B;コンポーネントを選択します。
1. ガイドコンテナプロパティ ![ガイドプロパティ](/help/forms/assets/configure-icon.svg) アイコンをクリックします。 アダプティブフォームコンテナダイアログボックスが開きます。
1. 「**[!UICONTROL 送信]**」タブをクリックします。
1. **[!UICONTROL 送信アクション]** ドロップダウンリストから、「**送信アクション**」を **[!UICONTROL SharePointに送信]** として選択します。
   ![SharePoint GIF](/help/forms/assets/sharedrive-video.gif)
1. データを保存する場所に「**[!UICONTROL ストレージ設定]**」を選択します。
1. 「**[!UICONTROL 保存]**」をクリックして、送信設定を保存します。

>[!NOTE]
>
> * フォームを送信すると、データは指定したMicrosoft® Sharepoint Document Library ストレージに保存されます。 データを保存するフォルダー構造は `/folder_name/form_name/year/month/date/submission_id/data` です。
> * 添付ファイルは、`/folder_name/form_name/year/month/date/submission_id/data` ディレクトリにも保存されます。ただし、「**添付ファイルを元の名前で保存**」を選択した場合、添付ファイルは元のファイル名を使用してフォルダーに保存されます。

>[!TAB ユニバーサルエディター]

ユニバーサルエディターで作成されたアダプティブフォームでSharePoint ドキュメントライブラリストレージ設定を使用するには、次の手順を実行します。

1. アダプティブフォームを編集用に開きます。
1. エディターで **フォームプロパティを編集** 拡張機能をクリックします。
**フォームのプロパティ** ダイアログが表示されます。

   >[!NOTE]
   >
   > * ユニバーサルエディターインターフェイスに **フォームプロパティを編集** アイコンが表示されない場合は、Extension Managerで **フォームプロパティを編集** 拡張機能を有効にします。
   > * ユニバーサルエディターで拡張機能を有効または無効にする方法については [&#128279;](https://developer.adobe.com/uix/docs/extension-manager/feature-highlights/#enablingdisabling-extensions)Extension Manager機能のハイライト &rbrace; の記事を参照してください。

1. 「**送信**」タブをクリックし、「**[!UICONTROL SharePointに送信]**」送信アクションを選択します。
   ![SharePoint GIF](/help/forms/assets/submit-to-sharepoint-ue.png)
1. データを保存する場所に「**[!UICONTROL ストレージ設定]**」を選択します。
1. **[!UICONTROL 保存して閉じる]** をクリックして、送信設定を保存します。

>[!NOTE]
>
> * フォームを送信すると、データは指定したMicrosoft® Sharepoint Document Library ストレージに保存されます。 データを保存するフォルダー構造は `/folder_name/form_name/year/month/date/submission_id/data` です。
> * 添付ファイルは、`/folder_name/form_name/year/month/date/submission_id/data` ディレクトリにも保存されます。ただし、「**添付ファイルを元の名前で保存**」を選択した場合、添付ファイルは元のファイル名を使用してフォルダーに保存されます。

>[!ENDTABS]

## 関連記事

{{af-submit-action}}
