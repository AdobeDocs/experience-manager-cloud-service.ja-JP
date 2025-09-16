---
title: OAuth 2.0 クライアントの資格情報フローを使用した Salesforce と AEM Forms の統合方法。
description: OAuth 2.0 クライアント資格情報フローを使用した Salesforce と AEM Forms の統合方法について説明します。AEM Forms Salesforce 統合の手順が表示されます。
Keywords: Integration of Salesforce using OAuth 2.0 client credential flow, salesforce integration with oauth2 using client credential flow, salesforce and client credential integration, AEM Forms Salesforce integration
feature: Adaptive Forms, Form Data Model
role: User, Developer
exl-id: 2c2029ab-6fb4-41a6-846c-175c3a79d921
source-git-commit: 9eb15dda5f56938d686d0b863cb1ffa841f8228b
workflow-type: ht
source-wordcount: '552'
ht-degree: 100%

---

# アダプティブフォームと Salesforce の統合 {#configure-salesforce-with-ouath-2.0-client-credential}

| バージョン | 記事リンク |
| -------- | ---------------------------- |
| AEM 6.5 | [ここをクリックしてください](https://experienceleague.adobe.com/docs/experience-manager-65/forms/form-data-model/oauth2-client-credentials-flow-for-server-to-server-integration.html?lang=ja) |
| AEM as a Cloud Service | この記事 |

Adobe Experience Manager（AEM）Forms と Salesforce の統合により、組織はフォームの作成および管理機能を Salesforce プラットフォームに接続してプロセスを効率化できます。アダプティブフォームを Salesforce に接続すると、2 つのプラットフォーム間でシームレスなデータ交換が可能になります。ユーザーがフォームを送信すると、データは自動的に Salesforce と同期されます。すべての顧客情報が最新の状態に保持され、システム内で一元化されます。

OAuth 2.0 クライアント資格情報を使用して、AEM Forms を Salesforce アプリケーションと統合できます。OAuth 2.0 クライアント資格情報は、ユーザーの関与なしに直接通信するための標準で安全な方法です。

![AEM Forms と Salesforce アプリケーション間の通信を設定する際のワークフロー](/help/forms/assets/salesforce-workflow.png)

AEM Forms が、Salesforce 接続アプリケーションで定義されたクライアント資格情報（Consumer key と Consumer secret）を交換して、アクセストークンを取得します。

AEM as a Cloud Service では、フォーム送信を処理するための様々な送信アクションが標準で提供されます。これらのオプションについて詳しくは、[アダプティブフォーム送信アクション](/help/forms/configure-submit-actions-core-components.md)の記事を参照してください。

認証コードフロー認証を使用した認証に OAuth 2.0 クライアント資格情報を使用すると、次のような複数のメリットがあります。

* OAuth 2.0 クライアント資格情報認証では、1 人のユーザーにつき 5 つ以上の接続を使用できます。
* AEM データソースの設定は、AEM ユーザーの非アクティブ化、アクセスの変更、パスワードの更新に対して引き続き機能します。

## 前提条件 {#prerequisites}

Salesforce アプリケーションと AEM 環境間の通信を設定する前に、次の手順を実行します。

* [OAuth 2.0 クライアント資格情報フローを使用した Salesforce 接続アプリ](https://help.salesforce.com/s/articleView?id=sf.connected_app_client_credentials_setup.htm&type=5)および組織の API のみのユーザーを作成し、アプリの Consumer key と Consumer secret を取得します。

* Swagger ファイルが組織の API に合わせて適切に設定されていることを確認します。または、最初から [Swagger ファイルを作成](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/forms/integrate-with-salesforce/describe-rest-api.html?lang=ja)することで、AEM 環境での使用に合わせてカスタマイズできます。


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
   > Swagger ファイルが選択されている場合、スキーム、ホスト名、ベースパスが自動的に設定されます。

1. 「**[!UICONTROL 参照]**」をクリックして、作成した Swagger ファイルをローカルマシンからアップロードします。
1. **[!UICONTROL 認証タイプ]**&#x200B;に「**[!UICONTROL OAuth 2.0]**」を選択します。**[!UICONTROL 認証設定]**&#x200B;パネルが表示されます。
1. 「**[!UICONTROL 付与タイプ]**」を「**[!UICONTROL クライアント資格情報]**」として選択します。
1. Salesforce 接続アプリから取得した&#x200B;**[!UICONTROL クライアント ID]** と&#x200B;**[!UICONTROL クライアント秘密鍵]**&#x200B;を指定します。
1. **[!UICONTROL アクセストークンの URL]** を次の形式で指定します
   `https://[MyDomainName].my.salesforce.com/services/oauth2/token`。

   >[!NOTE]
   >
   > 各組織には独自の固有のドメイン名があります。

1. 「**[!UICONTROL 接続をテスト]**」をクリックします。
1. 接続に成功した場合は、「**[!UICONTROL 作成]**」ボタンをクリックします。


Salesforce アプリケーションを設定した後は、フォームデータモデル（FDM）の作成中にこの設定を使用できます。詳しくは、[フォームデータモデル（FDM）の作成](create-form-data-models.md)を参照してください。アダプティブフォームの[フォームデータモデルの送信アクションを設定](/help/forms/using-form-data-model.md)を行って、Salesforce アプリケーションにデータを送信します。

ビジネスワークフローでのフォームデータモデル（FDM）の作成および使用について詳しくは、[データ統合](data-integration.md)を参照してください。

## 関連記事

{{af-submit-action}}


