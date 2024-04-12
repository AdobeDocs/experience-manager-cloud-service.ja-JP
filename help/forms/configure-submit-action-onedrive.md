---
Title: How to submit data from an Adaptive Form to Microsoft® OneDrive?
Description: Explore the streamlined process of connecting AEM Forms with Microsoft® OneDrive using the Submit to OneDrive Submit Action. Learn the step-by-step guide to configure OneDrive and set up submission actions for efficient data storage and retrieval
keywords: AEM Forms OneDrive との統合、Microsoft OneDrive への接続、AEM forms との OneDrive 構成セットアップ
feature: Adaptive Forms, Core Components
exl-id: dbfa4094-1b92-4a7c-a799-f66973d27054
source-git-commit: 62be3c6e98df9002cdfbeef50dd5475c4daa1576
workflow-type: ht
source-wordcount: '587'
ht-degree: 100%

---

# Microsoft® OneDrive へのアダプティブフォームの送信

「**[!UICONTROL OneDrive に送信]**」送信アクションでは、アダプティブフォームと Microsoft® OneDrive を接続します。接続されている Microsoft® OneDrive ストレージに、フォームデータ、ファイル、添付ファイル、またはレコードのドキュメントを送信できます。

AEM as a Cloud Service では、フォーム送信を処理するための様々な送信アクションが標準で提供されます。これらのオプションについて詳しくは、[アダプティブフォーム送信アクション](/help/forms/configure-submit-actions-core-components.md)の記事をご覧ください。

## メリット

AEM Forms と Microsoft® OneDrive のシームレスな統合の利点の一部を次に示します。

* OneDrive のクロスデバイスアクセシビリティにより、保存されたフォームデータを様々なプラットフォームで容易に使用できるようになります。ユーザーは、デスクトップ、ノートパソコン、タブレットおよびモバイルデバイスから送信されたデータ、添付ファイル、ドキュメントにアクセスし、アクセシビリティと柔軟性を高めることができます。
* AEM Forms と OneDrive を統合すると、信頼性と拡張性に優れたソリューションで効率的なデータストレージを実現できます。ファイル、添付ファイル、レコードのドキュメントなど、すべてのアダプティブフォーム送信を OneDrive に簡単に保存し、整理されたアクセス可能なデータを確保できます。

## アダプティブフォームへの OneDrive の接続

>[!VIDEO](https://video.tv.adobe.com/v/3424864/connect-aem-adaptive-form-to-onedrive/?quality=12&learn=on)

OneDrive for AEM Forms の送信を設定するには、次の手順を実行します。

1. [OneDrive 設定の作成](#create-a-onedrive-configuration-create-onedrive-configuration)：AEM Forms を Microsoft® OneDrive ストレージに接続します。
2. [アダプティブフォームでの「OneDrive に送信」アクションの使用](#use-onedrive-configuration-in-an-adaptive-form-use-onedrive-configuartion-in-af)：アダプティブフォームを設定済みの Microsoft® OneDrive に接続します。

### Microsoft OneDrive 設定の作成 {#create-onedrice-configuration}

AEM Forms を Microsoft® OneDrive ストレージに接続するには、以下の手順に従います。

1. **AEM Forms オーサー** インスタンス／**[!UICONTROL ツール]**／**[!UICONTROL クラウド サービス]**／**[!UICONTROL Microsoft® OneDrive]** に移動します。
1. **[!UICONTROL Microsoft® OneDrive]**&#x200B;を選択すると、**[!UICONTROL Microsoft® OneDrive ブラウザー]**&#x200B;にリダイレクトされます。
1. **設定コンテナ**&#x200B;を選択します。設定は、選択した設定コンテナに保存されます。
1. 「**[!UICONTROL 作成]**」をクリックします。OneDrive 設定ウィザードが表示されます。

   ![OneDrive 設定画面](/help/forms/assets/onedrive-configuration.png)

1. 「**[!UICONTROL タイトル]**」、「**[!UICONTROL クライアント ID]**」、「**[!UICONTROL クライアント秘密鍵]**」および「**[!UICONTROL OAuth URL]**」を指定します。OAuth URL のクライアント ID、クライアントの秘密鍵、テナント ID を取得する方法について詳しくは、[Microsoft® のドキュメント](https://learn.microsoft.com/en-us/graph/auth-register-app-v2)を参照してください。
   * アプリの `Client ID` と `Client Secret` は Microsoft® Azure Portal から取得できます。
   * Microsoft® Azure Portal で、リダイレクト URI を `https://[author-instance]/libs/cq/onedrive/content/configurations/wizard.html` として追加します。`[author-instance]` をオーサーインスタンスの URL に置き換えます。
   * API 権限 `offline_access` および `Files.ReadWrite.All` を追加して、読み取り／書き込み権限を付与します。
   * OAuth URL `https://login.microsoftonline.com/tenant-id/oauth2/v2.0/authorize` を使用します。`<tenant-id>` を Microsoft® Azure Portal のアプリの `tenant-id` に置き換えます。

   >[!NOTE]
   >
   > **クライアント秘密鍵**&#x200B;フィールドは、Azure Active Directory アプリケーションの設定に応じて、必須またはオプションになります。アプリケーションでクライアント秘密鍵を使用するように設定されている場合は、クライアントの秘密鍵を指定する必要があります。

1. 「**[!UICONTROL 接続]**」をクリックします。接続が完了すると `Connection Successful` メッセージが表示されます。

1. **[!UICONTROL OneDrive コンテナ]**／**[OneDrive フォルダー]**&#x200B;を選択して、データを保存します。

   >[!NOTE]
   >
   >* デフォルトでは、`forms-ootb-storage-adaptive-forms-submission` は OneDrive コンテナに存在します。
   > * 「**フォルダーを作成**」をクリックして、まだ存在しない場合は、フォルダーを `forms-ootb-storage-adaptive-forms-submission` として作成します。

アダプティブフォームの送信アクションに、この OneDrive ストレージ設定を使用できるようになりました。

### アダプティブフォームでの OneDrive 設定の使用 {#use-onedrive-configuartion-in-af}

アダプティブフォームで作成した OneDrive ストレージ設定を使用して、データまたは生成済みレコードのドキュメントを OneDrive フォルダーに保存できます。 アダプティブフォームで OneDrive ストレージ設定を使用するには、次の手順を実行します。
1. 「[アダプティブフォーム](/help/forms/creating-adaptive-form.md)」を作成します。

   >[!NOTE]
   >
   > * OneDrive ストレージを作成したアダプティブ フォームと同じ[!UICONTROL 設定コンテナ]を選択します。
   > * [!UICONTROL 設定コンテナ]が選択されていない場合、グローバルな[!UICONTROL ストレージ設定]フォルダーが送信アクションのプロパティウィンドウに表示されます。

1. 「**送信アクション**」を「**[!UICONTROL OneDrive に送信]**」として選択します。
   ![OneDrive GIF](/help/forms/assets/onedrive-video.gif)
1. データを保存する場所に「**[!UICONTROL ストレージ設定]**」を選択します。
1. 「**[!UICONTROL 保存]**」をクリックして、送信設定を保存します。

フォームを送信すると、指定した Microsoft® OneDrive ストレージにデータが保存されます。
データを保存するフォルダー構造は `/folder_name/form_name/year/month/date/submission_id/data` です。

## 関連記事

{{af-submit-action}}
