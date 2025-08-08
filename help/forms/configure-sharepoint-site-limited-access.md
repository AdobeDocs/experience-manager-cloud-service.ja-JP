---
title: 認証範囲を使用して制限付きアクセスでSharePoint サイトを設定する方法
description: 認証範囲を使用して、制限付きアクセスでSharePoint サイトを設定する方法を説明します。
keywords: 制限付きアクセスを使用するSharePoint サイトの設定方法、制限付きアクセスを使用するSharePointの設定方法、SharePoint サイトのアクセスを制限する認証範囲の使用方法を説明します。
feature: Adaptive Forms, Core Components
role: User, Developer
exl-id: 3230bab2-c1aa-409d-9f01-c42cf88b1135
source-git-commit: 1be7bafc1d93a65a81eeb2f7e86cac33cde7aa35
workflow-type: tm+mt
source-wordcount: '842'
ht-degree: 24%

---

<span class="preview"> この機能は、早期導入プログラムで利用できます。 早期導入プログラムに登録し、機能へのアクセスをリクエストするには、公式メール ID から aem-forms-ea@adobe.com にメールを送信してください。</span>

# 認証範囲を使用した制限付きアクセスでの SharePoint サイトの設定

制限付きまたは制限付きアクセスの目的は、管理者が特定のSharePoint サイトまたはSharePoint サイトのグループへのユーザーアクセスを制御できるようにして、セキュリティ管理を強化することです。 権限レベルは、ユーザーまたはグループに許可されていない他のSharePoint サイトの表示を許可せずに、特定のサイトへのアクセス権を付与する必要がある場合に役立ちます。

## アクセスが制限されたSharePoint サイトを設定するメリット

SharePoint サイトへの限定的なアクセスを提供するメリット：

* **セキュリティの強化**：アクセスを制限すると、権限のあるユーザーのみが機密情報を表示または操作できるようになり、不正アクセスのリスクが軽減されます。

* **最小権限の原則**：ユーザーは、職務を実行するために必要な最小限のアクセスレベル（または権限）を付与されます。 これにより、各ユーザーがネットワークの機密性の高い部分に触れる可能性が最小限に抑えられ、内部の潜在的な脅威から保護できます。

* **データ保護**：制限付きアクセスは、漏洩に対する重要なデータの保護に役立ちます。 これにより、データを表示する必要があるユーザーのみがデータにアクセスできるようになります。これは、データ保護規制の遵守に不可欠です。

* **偶発的なデータ損失の防止**：コンテンツを変更できるユーザーが減ると、重要なデータが誤って削除されたり変更されたりする可能性が大幅に低下します。

* **制御されたデータフロー**：組織内外での情報のフローを制御し、データが悪意のあるユーザーの手に渡らないようにするのに役立ちます。

## 認証範囲を使用した、制限付きアクセスによるSharePointの設定

認証範囲を使用して制限付きアクセスでSharePoint Sites を設定するには、次の手順に従います。

1. [を使用したアプリケーションの作成 ](#create-an-application-with-the-limited-permission-in-the-azure-portal)
1. [AEM インスタンスでの認証範囲の設定](#set-the-authorization-scope-at-aem-instance)

### Azure portal で、制限付き権限のアプリケーションを作成します

Microsoft Graph API の [ 権限範囲を使用して ](https://portal.azure.com/#home)0}Microsoft Azure Portal} でアプリケーションを作成します。`Sites.Selected`

![SharePointが選択したサイト ](/help/forms/assets/sharepoint-selected-site.png)

`Client ID` の `Client Secret`、`Tenant ID` および `OAuth URL` を取得する方法については、[Microsoft® のドキュメント ](https://learn.microsoft.com/ja-jp/graph/auth-register-app-v2) を参照してください。
* Microsoft® Azure Portal で、リダイレクト URI を `https://[author-instance]/libs/cq/sharepoint/content/configurations/wizard.html` として追加します。`[author-instance]` をオーサーインスタンスの URL に置き換えます。
* Microsoft Graph API で `offline_access` と `Sites.Selected` の権限範囲を追加し、Sites への制限付きアクセスを提供します。
* OAuth URL の場合：`https://login.microsoftonline.com/tenant-id/oauth2/v2.0/authorize`。 `<tenant-id>` を Microsoft® Azure Portal のアプリの `tenant-id` に置き換えます。

`Sites.Selected` API 権限を使用するには、SharePoint Online Sites に適切な権限が設定された Azure portal に登録されているアプリケーションが必要です。 このセットアップにより、定義されたスコープ内でSharePoint サイトを操作するために必要な権限がアプリケーションに付与され、必要な制限付きアクセスが提供されます。

SharePoint Online Sites の権限を使用するアプリケーションの開発手順については、[ ブログ記事 – Develop Applications that use Sites.Selected permissions for SPO sites](https://techcommunity.microsoft.com/t5/microsoft-sharepoint-blog/develop-applications-that-use-sites-selected-permissions-for-spo/ba-p/3790476) を参照し `Sites.Selected` ください。

### AEM インスタンスでの認証範囲の設定

Microsoft SharePoint サイトへの制限付きアクセスを提供するには、認証範囲を正しく設定する必要があります。 認証範囲を設定し、AEM FormsをMicrosoft® SharePoint ストレージに接続するには、次の手順に従います。

1. **AEM Forms オーサー**&#x200B;インスタンス／**[!UICONTROL ツール]**／**[!UICONTROL Cloud Services]**／**[!UICONTROL Microsoft® SharePoint]** に移動します。
1. **[!UICONTROL Microsoft® SharePoint]** を選択すると、**[!UICONTROL SharePoint ブラウザー]**&#x200B;にリダイレクトされます。
1. **設定コンテナ**&#x200B;を選択します。設定は、選択した設定コンテナに保存されます。
1. クリック **[!UICONTROL 作成]** > **[!UICONTROL SharePoint Document Library]** 」をドロップダウンリストから選択します。 SharePoint 設定ウィザードが表示されます。

   ![SharePoint サイトの制限付きサイト アクセス ](/help/forms/assets/sharepoint-doc-library-limited-scopes.png)

1. **[!UICONTROL タイトル]**、**[!UICONTROL クライアント ID]** および **[!UICONTROL クライアントシークレット]** を指定します。 クライアント ID とクライアント秘密鍵の取得方法については、[Microsoft® のドキュメント ](https://learn.microsoft.com/ja-jp/graph/auth-register-app-v2) を参照してください。

1. OAuth URL を `https://login.microsoftonline.com/tenant-id/oauth2/v2.0/authorize` として使用します。 `<tenant-id>` を Microsoft® Azure Portal のアプリの `tenant-id` に置き換えます。

   >[!NOTE]
   >
   > **クライアント秘密鍵**&#x200B;フィールドは、Azure Active Directory アプリケーションの設定に応じて、必須またはオプションになります。アプリケーションでクライアント秘密鍵を使用するように設定されている場合は、クライアントの秘密鍵を指定する必要があります。

1. `offline_access Sites.Selected` フィールドに `Authorization Scope` を追加します。 `offline_access Sites.Selected` のテキストボックス フィールドに `Authorization Scope` 範囲を追加すると、`SharePoint Site ID` のテキストボックスが画面に表示されます。

1. SharePoint サイト ID を指定します。 SharePoint サイト ID を取得する方法については、[ 追加バイト ](#extra-bytes) の節を参照してください。

1. **[!UICONTROL サイト接続の確認]** をクリックします。 接続に成功した場合、`Connection Successful` のメッセージが表示されます。

1. **SharePoint サイト**／**ドキュメントライブラリ**／**SharePoint フォルダー**&#x200B;を選択して、データを保存します。

   >[!NOTE]
   >
   >* デフォルトでは、`forms-ootb-storage-adaptive-forms-submission` は選択した SharePoint サイトに存在します。
   >* 選択した SharePoint サイトの `Documents` ライブラリにまだ存在しない場合は、「**フォルダーを作成**」をクリックして、フォルダーを `forms-ootb-storage-adaptive-forms-submission` として作成します。

アダプティブフォームの送信アクションに、この [SharePoint Sites 設定を使用できるようになりました ](/help/forms/configure-submit-action-sharepoint.md#use-sharepoint-document-library-configuration-in-an-adaptive-form-use-sharepoint-configuartion-in-af)。

## 追加バイト

`SharePoint Site ID` の値を取得するには：
1. [Microsoft Graph Explorer API](https://developer.microsoft.com/en-us/graph/graph-explorer) に移動します。
1. 左側のペインの「`SharePoint Sites` API」で、「`Search for a SharePoint site by keyword`」をクリックします。
1. プレースホルダー `contoso` をSharePoint サイトの実際の名前に置き換えて、対応するサイト ID を取得します。

   ![SharePoint ドキュメント ライブラリ ID](/help/forms/assets/sharepoint-site-id.png)

「`Run Query`」ボタンをクリックすると、画面にサイト ID が表示されます。
