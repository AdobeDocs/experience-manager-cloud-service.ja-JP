---
Title: How to send data to a SharePoint storage on submission of an Adaptive Form?
Description: Learn how to send data from your Adaptive Form to a SharePoint storage like a SharePoint list or Document library when you submit the form.
keywords: アダプティブフォームの SharePoint リストの接続方法？、アダプティブフォームの SharePoint ドキュメントライブラリの接続方法、SharePoint への送信、SharePoint ドキュメントライブラリ設定の作成、アダプティブフォームでの SharePoint への送信アクションの使用、Microsoft® SharePoint リストへのアダプティブフォームの接続。
feature: Adaptive Forms, Core Components
exl-id: e925a750-5fb5-4950-afd3-78551eec985d
title: 「アダプティブフォームの送信アクションの設定方法」
role: User, Developer
source-git-commit: 2b76f1be2dda99c8638deb9633055e71312fbf1e
workflow-type: tm+mt
source-wordcount: '1052'
ht-degree: 100%

---

# アダプティブフォームを Microsoft® SharePoint に接続

「**[!UICONTROL SharePoint に送信]**」の送信アクションにより、アダプティブフォームと Microsoft® SharePoint ストレージをシームレスに接続できます。フォームを送信した後、選択した SharePoint ストレージにフォームデータが送信されます。

AEM as a Cloud Service では、フォーム送信を処理するための様々な送信アクションが標準で提供されます。これらのオプションについて詳しくは、[アダプティブフォーム送信アクション](/help/forms/configure-submit-actions-core-components.md)の記事をご覧ください。

## メリット

アダプティブフォームから SharePoint ストレージにデータを送信する利点の一部を次に示します。

* フォームデータを SharePoint に直接送信し、情報を一元的に保存および管理できるようにします。
* SharePoint のアクセス制御機能と権限機能を適用すると、権限のある個人のみが送信されたデータを表示または変更できるようになります。

「**[!UICONTROL SharePoint に送信]**」を使用して、次の操作を実行できます。

* [アダプティブフォームを SharePoint ドキュメントライブラリに接続](#connect-af-sharepoint-doc-library)
* [アダプティブフォームを SharePoint リストに接続](#connect-af-sharepoint-list)

## アダプティブフォームを SharePoint ドキュメントライブラリに接続 {#connect-af-sharepoint-doc-library}

アダプティブフォームで「**[!UICONTROL SharePoint ドキュメントライブラリに送信]**」送信アクションを使用するには、次の手順に従います。

1. [SharePoint ドキュメントライブラリ設定の作成](#create-a-sharepoint-configuration-create-sharepoint-configuration)：AEM フォームを Microsoft Sharepoint ストレージに接続します。
2. [アダプティブフォームでの「SharePoint に送信」送信アクションの使用](#use-sharepoint-configuartion-in-af)：アダプティブフォームを設定済みの Microsoft® SharePoint に接続します。

### SharePoint ドキュメントライブラリの設定を作成 {#create-sharepoint-configuration}

AEM Forms を Microsoft® Sharepoint ドキュメントライブラリストレージに接続するには、次の手順に従います。

1. **AEM Forms オーサー**&#x200B;インスタンス／**[!UICONTROL ツール]**／**[!UICONTROL Cloud Services]**／**[!UICONTROL Microsoft® SharePoint]** に移動します。
1. **[!UICONTROL Microsoft® SharePoint]** を選択すると、**[!UICONTROL SharePoint ブラウザー]**&#x200B;にリダイレクトされます。
1. **設定コンテナ**&#x200B;を選択します。設定は、選択した設定コンテナに保存されます。
1. クリック **[!UICONTROL 作成]** > **[!UICONTROL SharePoint Document Library]** 」をドロップダウンリストから選択します。 SharePoint 設定ウィザードが表示されます。

   ![SharePoint の設定](/help/forms/assets/sharepoint_configuration.png)
1. 「**[!UICONTROL タイトル]**」、「**[!UICONTROL クライアント ID]**」、「**[!UICONTROL クライアント秘密鍵]**」および「**[!UICONTROL OAuth URL]**」を指定します。OAuth URL のクライアント ID、クライアントの秘密鍵、テナント ID を取得する方法について詳しくは、[Microsoft® のドキュメント](https://learn.microsoft.com/en-us/graph/auth-register-app-v2)を参照してください。
   * アプリの `Client ID` と `Client Secret` は Microsoft® Azure Portal から取得できます。
   * Microsoft® Azure Portal で、リダイレクト URI を `https://[author-instance]/libs/cq/sharepoint/content/configurations/wizard.html` として追加します。`[author-instance]` をオーサーインスタンスの URL に置き換えます。
   * API 権限 `offline_access` および `Sites.Manage.All` を追加して、読み取り／書き込み権限を付与します。
   * OAuth URL `https://login.microsoftonline.com/tenant-id/oauth2/v2.0/authorize` を使用します。`<tenant-id>` を Microsoft® Azure Portal のアプリの `tenant-id` に置き換えます。

   >[!NOTE]
   >
   > **クライアント秘密鍵**&#x200B;フィールドは、Azure Active Directory アプリケーションの設定に応じて、必須またはオプションになります。アプリケーションでクライアント秘密鍵を使用するように設定されている場合は、クライアントの秘密鍵を指定する必要があります。

1. 「**[!UICONTROL 接続]**」をクリックします。接続に成功した場合、`Connection Successful` のメッセージが表示されます。

1. **SharePoint サイト**／**ドキュメントライブラリ**／**SharePoint フォルダー**&#x200B;を選択して、データを保存します。

   >[!NOTE]
   >
   >* デフォルトでは、`forms-ootb-storage-adaptive-forms-submission` は選択した SharePoint サイトに存在します。
   >* 選択した SharePoint サイトの `Documents` ライブラリにまだ存在しない場合は、「**フォルダーを作成**」をクリックして、フォルダーを `forms-ootb-storage-adaptive-forms-submission` として作成します。

アダプティブフォームの送信アクションに、この SharePoint サイト設定を使用できるようになりました。

### アダプティブフォームでの SharePoint ドキュメントライブラリ設定の使用 {#use-sharepoint-configuartion-in-af}

作成した SharePoint ドキュメントライブラリ設定をアダプティブフォーム内で使用すると、データや生成済みレコードのドキュメントを SharePoint フォルダーに保存できます。 アダプティブフォームで SharePoint ドキュメントライブラリストレージ設定を使用するには、次の手順を実行します。

1. 「[アダプティブフォーム](/help/forms/creating-adaptive-form-core-components.md)」を作成します。

   >[!NOTE]
   >
   > * SharePoint ドキュメントライブラリストレージを作成したアダプティブフォームと同じ[!UICONTROL 設定コンテナ]を選択します。
   > * [!UICONTROL 設定コンテナ]が選択されていない場合、グローバルな[!UICONTROL ストレージ設定]フォルダーが送信アクションのプロパティウィンドウに表示されます。

1. 「**送信アクション**」を「**[!UICONTROL SharePoint に送信]**」として選択します。
   ![SharePoint GIF](/help/forms/assets/sharedrive-video.gif)
1. データを保存する場所に「**[!UICONTROL ストレージ設定]**」を選択します。
1. 「**[!UICONTROL 保存]**」をクリックして、送信設定を保存します。

フォームを送信すると、データは指定した Microsoft® Sharepoint ドキュメントライブラリストレージに保存されます。
データを保存するフォルダー構造は `/folder_name/form_name/year/month/date/submission_id/data` です。

## アダプティブフォームを Microsoft® SharePoint リストに接続 {#connect-af-sharepoint-list}

>[!VIDEO](https://video.tv.adobe.com/v/3424820/connect-aem-adaptive-form-to-sharepointlist/?quality=12&learn=on)

アダプティブフォームで「[!UICONTROL SharePoint リストに送信]」送信アクションを使用するには、次の手順に従います。

1. [SharePoint リスト設定を作成](#create-sharepoint-list-configuration)：AEM Forms を Microsoft® Sharepoint リストストレージに接続します。
1. [アダプティブフォームで「フォームデータモデル（FDM）を使用して送信」を使用](#use-submit-using-fdm)：アダプティブフォームを設定済みの Microsoft® SharePoint に接続します。

### SharePoint リスト設定を作成 {#create-sharepoint-list-configuration}

AEM Forms を Microsoft® Sharepoint リストに接続するには、次の手順に従います。

1. **[!UICONTROL ツール]**／**[!UICONTROL クラウドサービス]**／**[!UICONTROL Microsoft® SharePoint]** に移動します。
1. **設定コンテナ**&#x200B;を選択します。設定は、選択した設定コンテナに保存されます。
1. クリック **[!UICONTROL 作成]** > **[!UICONTROL SharePoint List]** 」をドロップダウンリストから選択します。 SharePoint 設定ウィザードが表示されます。
1. 「**[!UICONTROL タイトル]**」、「**[!UICONTROL クライアント ID]**」、「**[!UICONTROL クライアント秘密鍵]**」および「**[!UICONTROL OAuth URL]**」を指定します。OAuth URL のクライアント ID、クライアントの秘密鍵、テナント ID を取得する方法について詳しくは、[Microsoft® のドキュメント](https://learn.microsoft.com/en-us/graph/auth-register-app-v2)を参照してください。
   * アプリの `Client ID` と `Client Secret` は Microsoft® Azure Portal から取得できます。
   * Microsoft® Azure Portal で、リダイレクト URI を `https://[author-instance]/libs/cq/sharepointlist/content/configurations/wizard.html` として追加します。`[author-instance]` をオーサーインスタンスの URL に置き換えます。
   * API 権限の追加 `offline_access` および `Sites.Manage.All` （内） **Microsoft® Graph** タブを使用して、読み取り/書き込み権限を設定します。 追加 `AllSites.Manage` の権限 **SharePoint** タブをクリックして、SharePointデータをリモートで操作します。
   * OAuth URL `https://login.microsoftonline.com/tenant-id/oauth2/v2.0/authorize` を使用します。`<tenant-id>` を Microsoft® Azure Portal のアプリの `tenant-id` に置き換えます。

     >[!NOTE]
     >
     > **クライアント秘密鍵**&#x200B;フィールドは、Azure Active Directory アプリケーションの設定に応じて、必須またはオプションになります。アプリケーションでクライアント秘密鍵を使用するように設定されている場合は、クライアントの秘密鍵を指定する必要があります。

1. 「**[!UICONTROL 接続]**」をクリックします。接続に成功した場合、`Connection Successful` のメッセージが表示されます。
1. 選択 **[!UICONTROL SharePoint Site]** および **[!UICONTROL SharePoint List]** 」をドロップダウンリストから選択します。
1. 「**[!UICONTROL 作成]**」を選択して、Microsoft® SharePointList 用のクラウド設定を作成します。


### アダプティブフォームで「フォームデータモデル（FDM）を使用して送信」を使用 {#use-submit-using-fdm}

作成した SharePoint リスト設定をアダプティブフォーム内で使用すると、データや生成済みのレコードのドキュメントを SharePoint リストに保存できます。アダプティブフォームで SharePoint リストを使用するには、次の手順を実行します。

1. [Microsoft を使用してフォームデータモデル（FDM）を作成する](/help/forms/create-form-data-models.md)
1. [データを取得して送信するためのフォームデータモデル（FDM）を設定する](/help/forms/work-with-form-data-model.md#configure-services)
1. [アダプティブフォームを作成します](/help/forms/creating-adaptive-form-core-components.md)
1. [フォームデータモデル（FDM）を使用して送信アクションを設定する](/help/forms/using-form-data-model.md)

フォームを送信すると、データは指定した Microsoft® Sharepoint リストストレージに保存されます。

>[!NOTE]
>
> Microsoft® SharePointリストでは、次の列タイプはサポートされていません。
> * 画像列
> * メタデータ列
> * ユーザー列
> * 外部データ列

## 関連記事

{{af-submit-action}}
