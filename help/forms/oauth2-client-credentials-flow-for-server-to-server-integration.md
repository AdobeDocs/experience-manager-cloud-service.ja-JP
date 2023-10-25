---
title: OAuth 2.0 クライアントの資格情報フローを使用してAEM Formsと Salesforce を統合する方法を教えてください。
description: OAuth 2.0 クライアント資格情報フローを使用して、Salesforce とAEM Formsを統合する方法を説明します。
Keywords: Integration of Salesforce using OAuth 2.0 client credential flow, salesforce integration with oauth2 using client credential flow, salesforce and client credential integration
exl-id: 2c2029ab-6fb4-41a6-846c-175c3a79d921
source-git-commit: f70e18b1c21fd530587694f91c3969e831cfc640
workflow-type: tm+mt
source-wordcount: '422'
ht-degree: 33%

---

# OAuth 2.0 クライアント資格情報フローを使用してアダプティブフォームを Salesforce に接続 {#configure-salesforce-with-ouath-2.0-client-credential}

| バージョン | 記事リンク |
| -------- | ---------------------------- |
| AEM 6.5 | [ここをクリックしてください](https://experienceleague.adobe.com/docs/experience-manager-65/forms/form-data-model/oauth2-client-credentials-flow-for-server-to-server-integration.html) |
| AEM as a Cloud Service | この記事 |

OAuth 2.0 クライアント資格情報を使用して、AEM Formsを Salesforce アプリケーションと統合できます。 OAuth 2.0 クライアント資格情報は、ユーザーの関与なしに直接通信するための標準で安全な方法です。

![AEM Formsと Salesforce アプリケーション間の通信を設定する際のワークフロー](/help/forms/assets/salesforce-workflow.png)

AEM Formsが、Salesforce 接続アプリケーションで定義されたクライアント資格情報（消費者キーと消費者の秘密鍵）を交換して、アクセストークンを取得します。

認証コードフロー認証を使用した認証に OAuth 2.0 クライアント資格情報を使用すると、次のような複数のメリットがあります。

* OAuth 2.0 クライアント資格情報認証では、1 人のユーザーにつき 5 つ以上の接続を使用できます。
* AEMデータソースの設定は、AEMユーザーの非アクティブ化、アクセスの変更、パスワードの更新に対して引き続き機能します。

## 前提条件 {#prerequisites}

Salesforce アプリケーションとAEM環境間の通信を設定する前に、次の手順を実行します。

* の作成 [OAuth 2.0 クライアント資格情報フローを使用した Salesforce 接続アプリ](https://help.salesforce.com/s/articleView?id=sf.connected_app_client_credentials_setup.htm&amp;type=5) と組織の API のみのユーザーを含め、アプリの消費者キーと消費者の秘密鍵を取得します。

* Swagger ファイルが組織の API に合わせて適切に設定されていることを確認します。 または、 [Swagger ファイルを作成する](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/forms/integrate-with-salesforce/describe-rest-api.html?lang=ja) 最初から、AEM環境での使用に合わせてカスタマイズされます。


## OAuth 2.0 クライアント資格情報フローを使用した Salesforce アプリケーションの設定 {#steps-to-create-aem-datasource-configuration}

OAuth 2.0 クライアント資格情報認証設定を使用してアダプティブフォームを Salesforce アプリケーションに接続するには、次の手順を実行します。

1. オーサーインスタンスにログインします。
1. **[!UICONTROL ツール]**／**[!UICONTROL クラウドサービス]**／**[!UICONTROL データソース]**&#x200B;に移動します。
1. 設定フォルダーを選択します。
1. 「**[!UICONTROL 作成]**」をクリックします。**[!UICONTROL データソース設定を作成]**&#x200B;が表示されます。
1. **[!UICONTROL タイトル]**&#x200B;を指定し、**[!UICONTROL サービスタイプ]**&#x200B;に「**[!UICONTROL RESTful サービス]**」を選択します。
1. 「**[!UICONTROL 次へ]**」をクリックします。
1. **[!UICONTROL Swagger ソース]**&#x200B;に「**[!UICONTROL ファイル]」を選択します。**

   >[!NOTE]
   >
   > Swagger ファイルを選択すると、Scheme、Host name、Base パスが自動的に設定されます。

1. 「**[!UICONTROL 参照]**」をクリックして、作成した Swagger ファイルをローカルマシンからアップロードします。
1. **[!UICONTROL 認証タイプ]**&#x200B;に「**[!UICONTROL OAuth 2.0]**」を選択します。**[!UICONTROL 認証設定]**&#x200B;パネルが表示されます。
1. を選択します。 **[!UICONTROL 付与タイプ]** as **[!UICONTROL クライアント資格情報]**.
1. Salesforce 接続アプリから取得した&#x200B;**[!UICONTROL クライアント ID]** と&#x200B;**[!UICONTROL クライアント秘密鍵]**&#x200B;を指定します。
1. **[!UICONTROL アクセストークンの URL]** を次の形式で指定します
   `https://[MyDomainName].my.salesforce.com/services/oauth2/token`。

   >[!NOTE]
   >
   > 各組織には独自の固有のドメイン名があります。

1. 「**[!UICONTROL 接続をテスト]**」をクリックします。
1. 接続に成功した場合は、「**[!UICONTROL 作成]**」ボタンをクリックします。

次に、以下を実行できます。 [フォームデータモデルの作成](/help/forms/create-form-data-models.md) アダプティブフォームを Salesforce アプリケーションに送信する


