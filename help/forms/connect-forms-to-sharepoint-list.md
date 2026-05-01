---
title: アダプティブフォームの送信時にSharePoint リストストレージにデータを送信するにはどうすればよいですか？
Description: Learn how to send data from your Adaptive Form to a SharePoint storage like a SharePoint list when you submit the form.
keywords: アダプティブフォームのSharePoint リストを接続する方法は？、「SharePointに送信」、「SharePoint リスト設定を作成」、「アダプティブフォームでSharePointに送信」、「アダプティブフォームをMicrosoftに接続」、「SharePoint リスト」の順に選択します。
feature: Adaptive Forms, Core Components, Foundation Components, Edge Delivery Services
role: User, Developer
badgeSaas: label="AEM Forms" type="Positive" tooltip="AEM Formsに適用）。"
exl-id: 9ac3e7be-c6fa-4dbc-9aba-b81741ba6c55
source-git-commit: 0e5045b87719781301d91874c7355eda9426beef
workflow-type: tm+mt
source-wordcount: '782'
ht-degree: 54%

---

# アダプティブフォームを Microsoft® SharePoint リストに接続 {#connect-af-sharepoint-list}

>[!VIDEO](https://video.tv.adobe.com/v/3424820/connect-aem-adaptive-form-to-sharepointlist/?quality=12&learn=on)

<span>このビデオは、コアコンポーネントのみに適用されます。 UE／基盤コンポーネントについて詳しくは、記事を参照してください。</span>

アダプティブフォームで「[!UICONTROL SharePoint リストに送信]」送信アクションを使用するには、次の手順に従います。

1. [SharePoint リスト設定を作成](#1-create-a-sharepoint-list-configuration)：AEM Forms を Microsoft® Sharepoint リストストレージに接続します。
1. [アダプティブフォームで「フォームデータモデル（FDM）を使用して送信」を使用](#2-use-the-submit-using-form-data-model-fdm-in-an-adaptive-form-use-submit-using-fdm)：アダプティブフォームを設定済みの Microsoft® SharePoint に接続します。

## &#x200B;1. SharePoint リスト設定を作成

AEM Forms を Microsoft® Sharepoint リストに接続するには、次の手順に従います。

1. **[!UICONTROL ツール]**／**[!UICONTROL クラウドサービス]**／**[!UICONTROL Microsoft® SharePoint]** に移動します。
1. **設定コンテナ**&#x200B;を選択します。 設定は、選択した設定コンテナに保存されます。
1. クリック **[!UICONTROL 作成]** > **[!UICONTROL SharePoint List]** 」をドロップダウンリストから選択します。 SharePoint 設定ウィザードが表示されます。
1. 「**[!UICONTROL タイトル]**」、「**[!UICONTROL クライアント ID]**」、「**[!UICONTROL クライアント秘密鍵]**」および「**[!UICONTROL OAuth URL]**」を指定します。 OAuth URL のクライアント ID、クライアントの秘密鍵、テナント ID を取得する方法について詳しくは、[Microsoft® のドキュメント](https://learn.microsoft.com/ja-jp/graph/auth-register-app-v2)を参照してください。
   * アプリの `Client ID` と `Client Secret` は Microsoft® Azure Portal から取得できます。
   * Microsoft® Azure Portal で、リダイレクト URI を `https://[author-instance]/libs/cq/sharepointlist/content/configurations/wizard.html` として追加します。 `[author-instance]` をオーサーインスタンスの URL に置き換えます。
   * API 権限の追加 `offline_access` および `Sites.Manage.All` （内） **Microsoft® Graph** タブを使用して、読み取り/書き込み権限を設定します。 追加 `AllSites.Manage` の権限 **SharePoint** タブをクリックして、SharePointデータをリモートで操作します。
   * OAuth URL `https://login.microsoftonline.com/tenant-id/oauth2/v2.0/authorize` を使用します。 `<tenant-id>` を Microsoft® Azure Portal のアプリの `tenant-id` に置き換えます。

     >[!NOTE]
     >
     > **クライアント秘密鍵**&#x200B;フィールドは、Azure Active Directory アプリケーションの設定に応じて、必須またはオプションになります。 アプリケーションでクライアント秘密鍵を使用するように設定されている場合は、クライアントの秘密鍵を指定する必要があります。

1. 「**[!UICONTROL 接続]**」をクリックします。 接続が完了すると `Connection Successful` メッセージが表示されます。
1. 選択 **[!UICONTROL SharePoint Site]** および **[!UICONTROL SharePoint List]** 」をドロップダウンリストから選択します。
1. 「**[!UICONTROL 作成]**」を選択して、Microsoft® SharePointList 用のクラウド設定を作成します。

### 証明書ベースの認証 {#certificate-based-authentication}

SharePoint リスト設定の<span class="preview">証明書ベースの認証は、アーリーアダプタープログラムの下にあります。 早期導入プログラムに参加し、機能へのアクセスをリクエストするには、公式のメール ID で aem-forms-ea@adobe.com までメールを送信してください。</span>

SharePoint List configuration wizardで、次の操作を行います。

1. **[!UICONTROL 認証タイプ]**&#x200B;を&#x200B;**証明書ベースの認証**&#x200B;に設定します。
1. **[!UICONTROL タイトル]**、**[!UICONTROL クライアント ID]**、**[!UICONTROL 証明書エイリアス]**、**[!UICONTROL テナント Id]**&#x200B;および&#x200B;**[!UICONTROL テナント名]**&#x200B;を指定します。
1. **[!UICONTROL SharePoint サイト URL]**&#x200B;を入力し、必要に応じてサイト接続を確認して、**[!UICONTROL SharePoint リスト]**&#x200B;を選択します。
1. **[!UICONTROL 接続]**&#x200B;をクリックして接続を確認し、**[!UICONTROL 保存して閉じる]**&#x200B;をクリックして設定を保存します。

次のスクリーンショットは、**証明書ベースの認証**&#x200B;を使用したSharePoint リスト設定を示しています。

![証明書ベースの認証を使用したSharePoint リストの設定](/help/forms/assets/sharepoint-list-certificate-auth-configuration.png){width=50%, height=50%, align=center}

AEMおよびMicrosoft Azure用の証明書を準備するには、AEMで次の手順を実行し、公開証明書をMicrosoft Azureに登録します。

**AEM内**

1. **[!UICONTROL ツール]**／**[!UICONTROL セキュリティ]**／**[!UICONTROL ユーザー]**&#x200B;に移動します。
1. **[!UICONTROL fd-cloudservice]**&#x200B;を検索し、ユーザーを選択して、**[!UICONTROL プロパティ]**&#x200B;をクリックします。
1. 「**[!UICONTROL キーストア]**」タブを開きます。 キーストアがまだ作成されていない場合は、「**[!UICONTROL キーストアを作成]**」をクリックし、プロンプトに入力してキーストアのパスワードを設定します。
1. キーストアに秘密鍵を追加します：「**[!UICONTROL キーストアファイルから秘密鍵を追加]**」を展開し、**.jks** ファイルをアップロードします。
1. SharePoint リスト設定の&#x200B;**[!UICONTROL 証明書エイリアス]**&#x200B;と一致する&#x200B;**[!UICONTROL エイリアス]**&#x200B;を入力し、キー資料を送信してから、**[!UICONTROL 保存して閉じる]**&#x200B;をクリックします。

このスクリーンショットは、証明書が追加された後にキーストアを表示します。 **[!UICONTROL エイリアス]**&#x200B;は、SharePoint List クラウド設定の&#x200B;**[!UICONTROL 証明書エイリアス]**&#x200B;と一致する必要があります。

![fd-cloudservice ユーザーキーストアと証明書エイリアス &#x200B;](/help/forms/assets/fd-cloudservice-keystore-certificate.png){width=50%, height=50%, align=center}

**Microsoft Azureで**

1. アプリケーション登録を開き、**証明書と秘密鍵** > **証明書**&#x200B;に移動します。
1. 「**証明書をアップロード**」を選択し、Azureがアプリケーションに対して信頼する必要がある証明書ファイル（公開鍵）をアップロードします。

このスクリーンショットには、Azure ポータルの「**証明書**」タブが表示され、アプリ登録用の証明書をアップロードします。

![Azure アプリ登録証明書とシークレット &#x200B;](/help/forms/assets/azure-app-registration-sharepoint-certificates.png){width=50%, height=50%, align=center}

## &#x200B;2. アダプティブフォームでのフォームデータモデル（FDM）を使用した送信 {#use-submit-using-fdm}

作成した SharePoint リスト設定をアダプティブフォーム内で使用すると、データや生成済みのレコードのドキュメントを SharePoint リストに保存できます。 アダプティブフォームで SharePoint リストを使用するには、次の手順を実行します。

1. [Microsoft® SharePoint リスト設定を使用したフォームデータモデル（FDM）の作成](/help/forms/create-form-data-models.md)
1. [データを取得して送信するためのフォームデータモデル（FDM）を設定する](/help/forms/work-with-form-data-model.md#configure-services)
1. [アダプティブフォームを作成します](/help/forms/creating-adaptive-form-core-components.md)
1. [フォームデータモデル（FDM）を使用して送信アクションを設定する](/help/forms/using-form-data-model.md)

フォームを送信すると、データは指定した Microsoft® Sharepoint リストストレージに保存されます。

>[!NOTE]
>
> Microsoft® SharePointリストでは、次の列タイプはサポートされていません。
>
> * 画像列
> * メタデータ列
> * ユーザー列
> * 外部データ列

## 関連記事

{{af-submit-action}}
