---
title: Salesforceの標準のフォームデータモデルをアダプティブForms用に設定する方法
description: SalesforceをアダプティブFormsと統合する方法について説明します。
feature: Adaptive Forms, Form Data Model
role: User, Developer
source-git-commit: 3a12fff170f521f6051f0c24a4eb28a12439eec1
workflow-type: tm+mt
source-wordcount: '489'
ht-degree: 71%

---


# AEM Forms用のSalesforceの設定 {#configure-azure-storage}

[[!DNL Experience Manager Forms]  データ統合 &#x200B;](data-integration.md) は、アダプティブFormsを OOTB フォームデータモデル（FDM）と統合するための [!DNL Salesforce] Cloud Services を提供します。 その結果、アダプティブFormsは [!DNL Salesforce] サーバーとやり取りして、ビジネスワークフローを有効にすることができます。 次に例を示します。

* アダプティブフォームの送信時に、データを [!DNL Salesforce] に書き込む。
* フォームデータモデル（FDM）で定義されているカスタムエンティティを通じて、データを [!DNL Salesforce] に書き込みます（またはその逆の操作）。
* [!DNL Salesforce] サーバーに対してデータに関するクエリを実行し、アダプティブフォームに事前入力する。
* [!DNL Salesforce] サーバーからデータを読み取る。

[Experience Manager アーキタイプに基づいてFormsの開発プロジェクトをセットアップ &#x200B;](setup-local-development-environment.md#forms-cloud-service-local-development-environment) すると、[!DNL Salesforce] のクラウドサービスとフォームデータモデル（FDM）が [!DNL AEM Forms] Server 上で標準で使用できるようになります。

>[!NOTE]
>
>[!DNL Salesforce] Cloud Services およびフォームデータモデル（FDM）を標準で使用できるのは、[AEM アーキタイプ 30](https://github.com/adobe/aem-project-archetype/releases/tag/aem-project-archetype-30) 以降に基づいて [!DNL Experience Manager Forms] as a [!DNL Cloud Service] プロジェクトをセットアップしたのみとなります。

## [!DNL Salesforce] クラウドサービスの設定 {#configure-salesforce-cloud-service}

[!DNL Salesforce] クラウドサービスを設定する前に、必ず次の作業を実行してください。

* [OAuth 対応の接続された [!DNL Salesforce]  アプリケーションを作成](https://help.salesforce.com/s/articleView?id=sf.connected_app_create_api_integration.htm&type=5)します。接続された [!DNL Salesforce] アプリケーションを作成する際に、次の形式でコールバック URL を指定します。

  ```
  https://'[server]:[port]'/libs/fd/fdm/gui/components/admin/fdmcloudservice/createcloudconfigwizard/cloudservices.html
  ```

  このサーバーとポートは、[!DNL AEM Forms] サーバーのホスト名とポート番号を指します。

* [!DNL Salesforce] 接続アプリケーションを作成する際に、OAuth 範囲の値として `full` と `offline_access` を指定します。

* 接続アプリケーションのクライアント ID（「コンシューマーキー」とも呼ばれます）とクライアントの秘密キー（「コンシューマーシークレット」とも呼ばれます）の値を書き留めます。

[!DNL Salesforce] クラウドサービスを設定するには、次の手順を実行します。

1. オーサーインスタンス [!DNL AEM Forms]、**[!UICONTROL ツール]** ![&#x200B; ハンマー &#x200B;](assets/hammer.png)/**[!UICONTROL Cloud Services]**/**[!UICONTROL データソース]** に移動します。
2. フォルダー名を選択し、「**[!UICONTROL Salesforce クラウド設定]**」を選択して「**[!UICONTROL プロパティ]**」を選択します。
3. 「**[!UICONTROL 認証設定]**」タブで、次のように設定します。
   1. 「**[!UICONTROL ホスト]**」フィールドに [!DNL Salesforce] ドメイン URL を指定します。例えば、[Domain-name].my.salesforce.com のように指定します。
   2. 接続アプリケーションのクライアント ID（「コンシューマーキー」とも呼ばれます）とクライアントの秘密鍵（「コンシューマーシークレット」とも呼ばれます）を指定します。
   3. 「**[!UICONTROL 認証範囲]**」フィールドに **full offline_access** を指定します（`full` と `offine_access` の値をスペースで区切る）。
   4. 「**[!UICONTROL OAuth に接続]**」を選択します。[!DNL Salesforce] のログインページにリダイレクトされます。
   5. [!DNL Salesforce] の資格情報を使用してログインし、クラウドサービス設定を使用して [!DNL Salesforce] サービスに接続することに同意します。接続に成功すると、[!DNL Salesforce] クラウドサービス設定ページにリダイレクトされ、成功メッセージが表示されます。
4. 「**[!UICONTROL 保存して閉じる]**」を選択して、設定を完了します。

### 標準の [!DNL Salesforce] フォームデータモデル（FDM）へのアクセス

[Experience Manager アーキタイプに基づいて Forms の開発プロジェクトを設定](setup-local-development-environment.md#forms-cloud-service-local-development-environment)すると、[!DNL Salesforce] フォームデータモデル（FDM）を [!DNL AEM Forms] サーバー上ですぐに使用できるようになります。

フォームデータモデル（FDM）にアクセスするには：
1. **[!UICONTROL Adobe Experience Manager]** / **[!UICONTROL Forms]** / **[!UICONTROL Data Integrations]** に移動します。
1. フォルダー名を選択して「**[!UICONTROL Salesforce データモデル]**」を選択し、編集 ![編集](assets/edit.png) アイコンをクリックしてフォームデータモデル（FDM）を表示します。

[[!DNL Salesforce] クラウド設定サービス](#configure-salesforce-cloud-service)を設定したら、アダプティブフォームと標準の [!DNL Salesforce] データモデルを統合できます。

>[!MORELIKETHIS]
>
>* [AEM Forms 用のデータソースの設定](/help/forms/configure-data-sources.md)
>* [AEM Forms の Azure ストレージを設定](/help/forms/configure-azure-storage.md)
>  [AEM Sites ページへのフォームポータルの追加](/help/forms/configure-forms-portal.md)
