---
Title: How to send data to a SharePoint List storage on submission of an Adaptive Form?
Description: Learn how to send data from your Adaptive Form to a SharePoint storage like a SharePoint list when you submit the form.
keywords: アダプティブフォームでSharePoint リストを接続する方法、SharePointに送信する方法、SharePoint リスト設定を作成する方法、アダプティブフォームで「SharePointに送信」送信アクションを使用する方法、アダプティブフォームをMicrosoft&reg; SharePoint リストに接続する方法を説明します。
feature: Adaptive Forms, Core Components, Foundation Components, Edge Delivery Services
title: アダプティブフォームの送信アクションの設定方法
role: User, Developer
exl-id: 9ac3e7be-c6fa-4dbc-9aba-b81741ba6c55
source-git-commit: 64edcfe1bf94638ae5d9510a5a6ac660cf1bcd0a
workflow-type: tm+mt
source-wordcount: '438'
ht-degree: 87%

---

# アダプティブフォームを Microsoft® SharePoint リストに接続 {#connect-af-sharepoint-list}

>[!VIDEO](https://video.tv.adobe.com/v/3424820/connect-aem-adaptive-form-to-sharepointlist/?quality=12&learn=on)

アダプティブフォームで「[!UICONTROL SharePoint リストに送信]」送信アクションを使用するには、次の手順に従います。

1. [SharePoint リスト設定を作成](#1-create-a-sharepoint-list-configuration)：AEM Forms を Microsoft® Sharepoint リストストレージに接続します。
1. [アダプティブフォームで「フォームデータモデル（FDM）を使用して送信」を使用](#2-use-the-submit-using-form-data-model-fdm-in-an-adaptive-form-use-submit-using-fdm)：アダプティブフォームを設定済みの Microsoft® SharePoint に接続します。

## &#x200B;1. SharePoint リスト設定の作成

AEM Forms を Microsoft® Sharepoint リストに接続するには、次の手順に従います。

1. **[!UICONTROL ツール]**／**[!UICONTROL クラウドサービス]**／**[!UICONTROL Microsoft® SharePoint]** に移動します。
1. **設定コンテナ**&#x200B;を選択します。設定は、選択した設定コンテナに保存されます。
1. クリック **[!UICONTROL 作成]** > **[!UICONTROL SharePoint List]** 」をドロップダウンリストから選択します。 SharePoint 設定ウィザードが表示されます。
1. 「**[!UICONTROL タイトル]**」、「**[!UICONTROL クライアント ID]**」、「**[!UICONTROL クライアント秘密鍵]**」および「**[!UICONTROL OAuth URL]**」を指定します。OAuth URL のクライアント ID、クライアントの秘密鍵、テナント ID を取得する方法について詳しくは、[Microsoft® のドキュメント](https://learn.microsoft.com/ja-jp/graph/auth-register-app-v2)を参照してください。
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


## &#x200B;2. アダプティブフォームでフォームデータモデル（FDM）を使用して送信を使用する {#use-submit-using-fdm}

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
