---
title: OAuth 2.0 クライアント資格情報フローを使用して、AEM Formsと Salesforce の統合を統合する方法を教えてください。
seo-title: Salesforce integration with AEM Forms using OAuth 2.0 client credential flow
description: OAuth 2.0 クライアント資格情報フローを使用して Salesforce とAEM Formsを統合する手順
seo-description: Steps to integrate Salesforce integration with AEM Forms using OAuth 2.0 client credential flow
Keywords: Integration of Salesforce using OAuth 2.0 client credential flow, salesforce integration with oauth2 using client credential flow, salesforce and client credential integration
source-git-commit: 2c0a816b61cfc17a83b24b28be1f317e9681c6c5
workflow-type: tm+mt
source-wordcount: '426'
ht-degree: 3%

---


# OAuth 2.0 クライアント資格情報フローを使用した Salesforce アプリケーションの統合 {#configure-salesforce-with-ouath-2.0-client-credential}

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

* Swagger ファイルが組織の API に合わせて適切に設定されていることを確認します。 または、 [Swagger ファイルを作成する](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/forms/integrate-with-salesforce/describe-rest-api.html) 最初から、AEM環境での使用に合わせてカスタマイズされます。


## OAuth 2.0 クライアント資格情報フローを使用した Salesforce アプリケーションの設定 {#steps-to-create-aem-datasource-configuration}

OAuth 2.0 クライアント資格情報認証設定を使用して Salesforce アプリケーションをアダプティブフォームに統合するには、次の手順を実行します。

1. オーサーインスタンスにログインします。
1. に移動します。 **[!UICONTROL ツール]** > **[!UICONTROL Cloud Services]** > **[!UICONTROL データソース]**.
1. 設定フォルダーを選択します。
1. クリック **[!UICONTROL 作成]** そして **[!UICONTROL データソース設定を作成]** が表示されます。
1. 次を指定します。 **[!UICONTROL タイトル]** をクリックし、 **[!UICONTROL サービスタイプ]** as **[!UICONTROL RESTful サービス]**.
1. 「**[!UICONTROL 次へ]**」をクリックします。
1. を選択します。 **[!UICONTROL Swagger ソース]** as **[!UICONTROL ファイル].**

   >[!NOTE]
   >
   > Swagger ファイルを選択すると、Scheme、Host name、Base パスが自動的に設定されます。

1. 作成した Swagger ファイルをローカルマシンからアップロードするには、 **[!UICONTROL 参照]**.
1. を選択します。 **[!UICONTROL 認証タイプ]** as **[!UICONTROL OAuth 2.0]** そして **[!UICONTROL 認証設定]** パネルが表示されます。
1. を選択します。 **[!UICONTROL 付与タイプ]** as **[!UICONTROL クライアント資格情報]**.
1. 次を指定します。 **[!UICONTROL クライアント ID]** および **[!UICONTROL クライアントの秘密鍵]** Salesforce 接続アプリから取得しました。
1. 次を指定します。 **[!UICONTROL トークン URL にアクセス]** 形式で
   `https://[MyDomainName].my.salesforce.com/services/oauth2/token`。

   >[!NOTE]
   >
   > 各組織には固有のドメイン名があります。

1. クリック **[!UICONTROL 接続をテスト]**.
1. 接続に成功した場合は、 **[!UICONTROL 作成]** 」ボタンをクリックします。

次に、以下を実行できます。 [フォームデータモデルの作成](/help/forms/create-form-data-models.md) 設定済みのデータソースをアダプティブフォームに統合する場合。
