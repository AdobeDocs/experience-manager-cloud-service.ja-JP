---
title: Microsoft Dynamics 365 および Salesforce の標準のフォームデータモデルをアダプティブフォーム用に設定する方法
description: Microsoft Dynamics 365 と Salesforce をアダプティブフォームに統合する方法を説明します。
feature: Adaptive Forms, Form Data Model
role: User, Developer
exl-id: 2a43b2db-2dfb-4c79-88be-ea770b44dac1
source-git-commit: 7b31a2ea016567979288c7a8e55ed5bf8dfc181d
workflow-type: tm+mt
source-wordcount: '965'
ht-degree: 72%

---

# AEM Forms 用の Microsoft® Dynamics 365 または Salesforce の設定 {#configure-azure-storage}

| バージョン | 記事リンク |
| -------- | ---------------------------- |
| AEM 6.5 | [ここをクリックしてください](https://experienceleague.adobe.com/docs/experience-manager-65/forms/form-data-model/oauth2-client-credentials-flow-for-server-to-server-integration.html) |
| AEM as a Cloud Service | この記事 |

[[!DNL Experience Manager Forms] データ統合](data-integration.md) 提供する [!DNL Microsoft® Dynamics 365] および [!DNL Salesforce] アダプティブフォームを標準のフォームデータモデル（FDM）に統合するためのクラウドサービス。 その結果、アダプティブフォームは、[!DNL Microsoft® Dynamics 365] および [!DNL Salesforce] サーバーとやり取りして、ビジネスワークフローを有効にすることができます。次に例を示します。

* アダプティブフォームの送信時にデータを [!DNL Microsoft® Dynamics 365].および [!DNL Salesforce] に書き込む。
* データをに書き込む [!DNL Microsoft® Dynamics 365] および [!DNL Salesforce] フォームデータモデル（FDM）で定義したカスタムエンティティを使用する（またはその逆の方法）。
* [!DNL Microsoft® Dynamics 365] および [!DNL Salesforce] サーバーに対してデータに関するクエリを実行し、アダプティブフォームにデータを事前入力する。
* [!DNL Microsoft® Dynamics 365] および [!DNL Salesforce] サーバーからデータを読み取る。

[!DNL Microsoft® Dynamics 365] および [!DNL Salesforce] クラウドサービスおよびフォームデータモデル（FDM）は、 [!DNL AEM Forms] 導入後のサーバ [Experience Managerアーキタイプに基づいたFormsの開発プロジェクトの設定](setup-local-development-environment.md#forms-cloud-service-local-development-environment).

>[!NOTE]
>
>Microsoft® Dynamics 365 および [!DNL Salesforce] クラウドサービスとフォームデータモデル（FDM）は、以下を設定した場合にのみ、すぐに使用できます [!DNL Experience Manager Forms] as a [!DNL Cloud Service] 基づいたプロジェクト [AEM アーキタイプ 30](https://github.com/adobe/aem-project-archetype/releases/tag/aem-project-archetype-30) またはそれ以降。

## [!DNL Salesforce] クラウドサービスの設定 {#configure-salesforce-cloud-service}

[!DNL Salesforce] クラウドサービスを設定する前に、必ず次の作業を実行してください。

* [OAuth 対応の接続された [!DNL Salesforce]  アプリケーションを作成](https://help.salesforce.com/s/articleView?id=sf.connected_app_create_api_integration.htm&amp;type=5)します。接続された [!DNL Salesforce] アプリケーションを作成する際に、次の形式でコールバック URL を指定します。

  ```
  https://'[server]:[port]'/libs/fd/fdm/gui/components/admin/fdmcloudservice/createcloudconfigwizard/cloudservices.html
  ```

  このサーバーとポートは、[!DNL AEM Forms] サーバーのホスト名とポート番号を指します。

* [!DNL Salesforce] 接続アプリケーションを作成する際に、OAuth 範囲の値として `full` と `offline_access` を指定します。

* 接続アプリケーションのクライアント ID（「コンシューマーキー」とも呼ばれます）とクライアントの秘密キー（「コンシューマーシークレット」とも呼ばれます）の値を書き留めます。

[!DNL Salesforce] クラウドサービスを設定するには、次の手順を実行します。

1. [!DNL AEM Forms] オーサーインスタンスで、**[!UICONTROL ツール]** ![ハンマーアイコン](assets/hammer.png)／**[!UICONTROL クラウドサービス]**／**[!UICONTROL データソース]**&#x200B;に移動します。使用可能なラッパーフォルダーのリストには、[AEM アーキタイププロジェクトの生成](setup-local-development-environment.md#forms-cloud-service-local-development-environment)時に `DappTitle` のタイトルを指定したフォルダーが含まれています。
1. フォルダー名を選択し、「**[!UICONTROL Salesforce クラウド設定]**」を選択して「**[!UICONTROL プロパティ]**」を選択します。
1. 「**[!UICONTROL 認証設定]**」タブで、次のように設定します。
   1. 「**[!UICONTROL ホスト]**」フィールドに [!DNL Salesforce] ドメイン URL を指定します。例えば、[Domain-name].my.salesforce.com のように指定します。
   1. 接続アプリケーションのクライアント ID（「コンシューマーキー」とも呼ばれます）とクライアントの秘密鍵（「コンシューマーシークレット」とも呼ばれます）を指定します。
   1. 「**[!UICONTROL 認証範囲]**」フィールドに **full offline_access** を指定します（`full` と `offine_access` の値をスペースで区切る）。
   1. 「**[!UICONTROL OAuth に接続]**」を選択します。[!DNL Microsoft® Dynamics] のログインページにリダイレクトされます。
   1. [!DNL Salesforce] の資格情報を使用してログインし、クラウドサービス設定を使用して [!DNL Salesforce] サービスに接続することに同意します。接続に成功すると、[!DNL Salesforce] クラウドサービス設定ページにリダイレクトされ、成功メッセージが表示されます。
1. 「**[!UICONTROL 保存して閉じる]**」を選択して、設定を完了します。

### 標準アクセス [!DNL Salesforce] フォームデータモデル（FDM）

A [!DNL Salesforce] フォームデータモデル（FDM）は、に標準で用意されています [!DNL AEM Forms] 導入後のサーバ [Experience Managerアーキタイプに基づいたFormsの開発プロジェクトの設定](setup-local-development-environment.md#forms-cloud-service-local-development-environment).

フォームデータモデル（FDM）にアクセスするには、次に移動します **[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL Forms]** > **[!UICONTROL データ統合]**. 使用可能なフォルダーのリストには、[AEM アーキタイププロジェクトの生成](setup-local-development-environment.md#forms-cloud-service-local-development-environment)時に `DappTitle` のタイトルを指定したフォルダーが含まれています。フォルダー名を選択し、 **[!UICONTROL Salesforce データモデル]**&#x200B;を選択し、「編集」を選択します ![編集](assets/edit.png) アイコンをクリックして、フォームデータモデル（FDM）を表示します。

[[!DNL Salesforce] クラウド設定サービス](#configure-salesforce-cloud-service)を設定したら、アダプティブフォームと標準の [!DNL Salesforce] データモデルを統合できます。

## [!DNL Microsoft® Dynamics 365] クラウドサービスの設定 {#configure-dynamics-cloud-service}

[!DNL Microsoft® Dynamics 365] クラウドサービスを設定する前に、必ず次の作業を実行してください。

* [ [!DNL Microsoft® Dynamics 365] のアプリケーションを Azure Active Directory に登録](https://docs.microsoft.com/ja-jp/powerapps/developer/data-platform/walkthrough-register-app-azure-active-directory)します。[!DNL Microsoft® Dynamics 365] 接続アプリケーションを作成する際に、次の形式で応答 URL を指定します。

  ```
  https://'[server]:[port]'/libs/fd/fdm/gui/components/admin/fdmcloudservice/createcloudconfigwizard/cloudservices.html
  ```

  このサーバーとポートは [!DNL AEM Forms] サーバーのホスト名とポート番号を指します。

* 接続アプリケーションのクライアント ID（「アプリケーション ID」とも呼ばれます）とクライアントの秘密鍵の値を書き留めます。

[!DNL Microsoft® Dynamics 365] クラウドサービスを設定するには、次の手順を実行します。

1. [!DNL AEM Forms] オーサーインスタンスで、**[!UICONTROL ツール]** ![ハンマーアイコン](assets/hammer.png)／**[!UICONTROL クラウドサービス]**／**[!UICONTROL データソース]**&#x200B;に移動します。使用可能なラッパーフォルダーのリストには、[AEM アーキタイププロジェクトの生成](setup-local-development-environment.md#forms-cloud-service-local-development-environment)時に `DappTitle` のタイトルを指定したフォルダーが含まれています。
1. フォルダー名を選択し、「**[!UICONTROL Microsoft® Dynamics 365 クラウド設定]**」を選択して「**[!UICONTROL プロパティ]**」を選択します。
1. 「**[!UICONTROL 認証設定]**」タブで、次のように設定します。
   1. 「**[!UICONTROL サービスルート]**」フィールドの値を入力します。Dynamics インスタンスの「[開発者向けリソース](https://docs.microsoft.com/ja-jp/powerapps/developer/data-platform/view-download-developer-resources)」に移動し、「サービスルート」フィールドの値を表示します。例：`https://<tenant-name>.dynamics.com/api/data/v9.1/`
   1. 接続アプリケーションのクライアント ID（「アプリケーション ID」とも呼ばれます）とクライアントの秘密鍵を指定します。
   1. 「**[!UICONTROL OAuth URL]**」、「**[!UICONTROL 更新トークン URL]**」、「**[!UICONTROL アクセストークン URL]**」の各フィールドの `{tenant}` をテナント ID に置き換えます。
   1. 次で Dynamics インスタンスの URL を指定 **[!UICONTROL Resource]** 設定するフィールド [!UICONTROL Microsoft® Dynamics] フォームデータモデル（FDM）を使用する。 サービスルート URL を使用して、Dynamics インスタンスの URL を取得します。（例：`https://<tenant-name>.dynamics.com`）。

   1. `openid` の認証プロセス用の「**[!UICONTROL 認証範囲」フィールドで]**、「[!DNL Microsoft® Dynamics 365]」を指定します。
   1. [!DNL Microsoft® Dynamics 365] の資格情報を使用してログインし、クラウドサービス設定を使用して [!DNL Microsoft® Dynamics 365] サービスに接続することに同意します。接続に成功すると、[!DNL Microsoft® Dynamics 365] クラウドサービス設定ページにリダイレクトされ、成功メッセージが表示されます。
1. 「**[!UICONTROL 保存して閉じる]**」を選択して、設定を完了します。

### 標準アクセス [!DNL Microsoft® Dynamics 365] フォームデータモデル（FDM）

A [!DNL Microsoft® Dynamics 365] フォームデータモデル（FDM）は、に標準で用意されています [!DNL AEM Forms] 導入後のサーバ [Experience Managerアーキタイプに基づいたFormsの開発プロジェクトの設定](setup-local-development-environment.md##forms-cloud-service-local-development-environment).

フォームデータモデル（FDM）にアクセスするには、次に移動します **[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL Forms]** > **[!UICONTROL データ統合]**. 使用可能なフォルダーのリストには、[AEM アーキタイププロジェクトの生成](setup-local-development-environment.md#forms-cloud-service-local-development-environment)時に `DappTitle` のタイトルを指定したフォルダーが含まれています。フォルダー名を選択し、 **[!UICONTROL Microsoft® Dynamics 365 データモデル]**&#x200B;を選択し、「編集」を選択します ![編集](assets/edit.png) アイコンをクリックして、フォームデータモデル（FDM）を表示します。

[[!DNL Microsoft® Dynamics 365] クラウド設定サービス](#configure-dynamics-cloud-service)を設定したら、アダプティブフォームと標準の [!DNL Microsoft® Dynamics 365] データモデルを統合できます。

>[!MORELIKETHIS]
>
>* [AEM Forms 用のデータソースの設定](/help/forms/configure-data-sources.md)
>* [AEM Forms の Azure ストレージを設定](/help/forms/configure-azure-storage.md)
>  [AEM Sites ページへのフォームポータルの追加](/help/forms/configure-forms-portal.md)
