---
title: ' [!DNL Dynamic Media]  Prime と Ultimate の有効化'
description: ' [!DNL Dynamic Media]  Prime と Ultimate のサービスを有効にする方法について説明します。'
feature: Asset Management
role: User, Admin
exl-id: 0ee161f5-bf44-41f1-928e-c07574fd43cc
source-git-commit: 42c90ae69af31b1b54f5b4ed01100df0cbe5dad2
workflow-type: tm+mt
source-wordcount: '1074'
ht-degree: 100%

---

# [!DNL Dynamic Media] Prime と Ultimate の有効化 {#enable-dynamic-media-prime-and-ultimate}

| [検索のベストプラクティス](/help/assets/search-best-practices.md) | [メタデータのベストプラクティス](/help/assets/metadata-best-practices.md) | [コンテンツハブ](/help/assets/product-overview.md) | [OpenAPI 機能を備えた Dynamic Media](/help/assets/dynamic-media-open-apis-overview.md) | [AEM Assets 開発者向けドキュメント](https://developer.adobe.com/experience-cloud/experience-manager-apis/) |
| ------------- | --------------------------- |---------|----|-----|

[!DNL Adobe Experience Manager] as a Cloud Service を使用すると、[!DNL Dynamic Media] Prime および Ultimate サービスにアクセスして、デジタルワークフローを効率化し、コンテンツ管理を最適化できます。これらのメリットと主な違いについて詳しくは、[Dynamic Media Prime と Ultimate](/help/assets/dynamic-media/dm-prime-ultimate.md) を参照してください。

この記事では、[!DNL Dynamic Media] Prime および Ultimate サービスを有効にするエンドツーエンドのワークフローについて説明します。

## [!DNL Dynamic Media] Ultimate を有効にする {#enable-dynamic-media-ultimate}

[!DNL Dynamic Media] Ultimate を有効にするには、Cloud Service 環境で次の手順を実行します。

1. [アクティベート [!DNL Dynamic Media with OpenAPI]](#activate-dynamic-media-with-openapi)
1. [ [!DNL Dynamic Media]  ソリューションを設定](#configure-dynamic-media-solutions)
1. [ [!DNL Dynamic Media]  会社を作成してリスト化](#create-and-list-dynamic-media-companies)
1. [配信層でカスタムドメインを設定](#configure-custom-domain-in-delivery-tier)

<!--
1. [Onboard API keys using the [!DNL AEM] [!DNL Dynamic Media] API card](#onboarding-api-keys)
-->

[!DNL Dynamic Media Prime] を有効にする必要がある場合は、[有効にする [!DNL Dynamic Media Prime]](#enable-dynamic-media-prime)に記載されているクイックリンクを参照してください。

### アクティベート [!DNL Dynamic Media with OpenAPI] {#activate-dynamic-media-with-openapi}

OpenAPI を備えた [!DNL Dynamic Media] 機能では、DAM をアジャイルで効率的なコンテンツサプライチェーンエコシステムのコアに置き、アセットのガバナンスと配信を確実に行います。

[!DNL Dynamic Media] Ultimate を有効にするプロセスの最初の手順は、Cloud Service 環境の OpenAPI](/help/assets/dynamic-media-open-apis-overview.md) を備えた [[!DNL Dynamic Media]  を使用してアクティベートすることです。

#### 開始する準備を整える {#prerequisites}

アクティベーションプロセスを開始する前に、次の要件を満たしていることを確認します。

1. [Cloud Manager へのアクセス権](https://experienceleague.adobe.com/ja/docs/experience-manager-cloud-service/content/onboarding/journey/cloud-manager)。
1. [プログラムに  [!DNL Dynamic Media]  ソリューションが含まれている](#configure-dynamic-media-solutions)。
1. [!DNL Dynamic Media] Prime または Ultimate ライセンスがある。

#### Cloud Service 環境での [!DNL Dynamic Media with OpenAPI] 機能を有効にする。 {#enable-dynamic-media-with-openapi-capabilites-in-your-CS-environment}

Cloud Service 環境で [!DNL Dynamic Media with OpenAPI] を有効にするには、次の手順を実行します。

1. [Cloud Manager UI に移動します](https://experienceleague.adobe.com/ja/docs/experience-manager-cloud-service/content/onboarding/journey/cloud-manager)。

1. 既存の環境にアクセスできない場合は、[環境を作成](https://experienceleague.adobe.com/ja/docs/experience-manager-cloud-service/content/onboarding/journey/create-environments)します。

1. 環境の詳細ページの「**[!UICONTROL 環境情報]**」セクションの **[!UICONTROL Dynamic Media]** 行で「**[!UICONTROL クリックしてアクティベート]**」を選択します。

   ![OpenAPI を備えた Dynamic Media 機能をアクティベート](/help/assets/assets/activate-adv-capabiliites-of-dm-openAPI.png)

1. 確認ダイアログで「**[!UICONTROL アクティベート]**」をクリックして、[!DNL Dynamic Media with OpenAPI] アクティベーションプロセスを開始します。アクティベーションが成功すると、Cloud Manager に次のステータス更新が表示されます。
   1. **[!UICONTROL 環境ステージ]**：**[!UICONTROL 実行中]**
   1. ![DM のアクティベート](/help/assets/assets/Images_icon.svg)**[!UICONTROL  Dynamic Media ]**：**[!UICONTROL  OpenAPI 機能がアクティベートされています&#x200B;]**

      ![アクティベーション成功](/help/assets/assets/activation-successful.png){width="700" align="left"}

#### アクティベーションの再試行 {#retry-activation}

アクティベーションに失敗した場合、Cloud Manager に次のステータス更新が表示されます。

* **[!UICONTROL 環境ステージ]**：**[!UICONTROL OpenAPI を使用した DM にエラーが発生しました]**
* ![DM のアクティベート](/help/assets/assets/Images_icon.svg)**[!UICONTROL  Dynamic Media ]**：**[!UICONTROL  OpenAPI 機能のアクティベートに失敗しました&#x200B;]**

  ![アクティベーションを再試行](/help/assets/assets/retry-dm-openapi-failed-activation.png){width="700" align="left"}

「**[!UICONTROL クリックして再試行]**」を選択して、アクティベーションを再開します。

または、以下の手順を実行してアクティベーションプロセスを再開します。

1. すべての環境をリスト化するページに移動します。

1. 環境行の最後にあるその他のオプション（![その他のオプション](/help/assets/assets/three-dots.svg)）をクリックします。

1. 「**[!UICONTROL OpenAPI を備えた DM のアクティベーションを再試行]**」を選択して、アクティベーションを再開します。

   ![環境の詳細ページからアクティベーションを再試行](/help/assets/assets/restart-activation-process-from-list-environment-page.png)

### [!DNL Dynamic Media] ソリューションを設定 {#configure-dynamic-media-solutions}

Cloud Manager で使用可能な既存の環境や新しい環境で [OpenAPI を備えた Dynamic Media](/help/assets/dynamic-media-open-apis-overview.md) の基本機能と高度な機能を使用するには、[!UICONTROL Dynamic Media] ソリューションを設定します。

#### 開始する準備を整える {#prerequisites-to-configure-dynamic-media-solutions}

[!UICONTROL Dynamic Media] ソリューションを設定するには、次の要件を満たしていることを確認します。

1. [Cloud Manager へのアクセス権](https://experienceleague.adobe.com/ja/docs/experience-manager-cloud-service/content/onboarding/journey/cloud-manager)。
1. [!DNL Dynamic Media] Ultimate ライセンスがある。

#### アセット配信用の [!DNL Dynamic Media] ソリューションの設定 {#configure-dynamic-media-solutions-for-asset-delivery}

次の手順を実行します。

1. [新しいプログラムを作成](https://experienceleague.adobe.com/ja/docs/experience-manager-cloud-service/content/onboarding/journey/create-program)するか、既存のプログラムに移動して「**[!UICONTROL 編集]**」をクリックします。**[!UICONTROL 実稼動環境用に設定]**&#x200B;ページに「**[!UICONTROL ソリューションとアドオン]**」タブが表示されます。

1. 「**[!UICONTROL Assets]**」、「**[!UICONTROL Assets Prime]**」、「**[!UICONTROL Assets Ultimate]**」または「**[!UICONTROL Sites]**」を選択して、**[!UICONTROL Dynamic Media]** ソリューションをプログラムに追加します。

1. **[!UICONTROL Dynamic Media]** ソリューションを選択し、「**[!UICONTROL 続行]**」をクリックして、**[!UICONTROL Dynamic Media]** ソリューションをプログラムに追加します。このアクションにより、プログラム内の既存の環境がすべて再起動され、[!DNL Dynamic Media] ソリューションが追加されます。また、プログラムで作成する新しい環境では、すべて自動的に [!DNL Dynamic Media] を取得します。

   ![実稼動環境用に設定](/help/assets/assets/set-up-for-prod.png){width="500" align="left"}

お使いの環境で OpenAPI を備えた [!DNL Dynamic Media] の機能の使用を開始するには、[アクティベート [!DNL Dynamic Media with OpenAPI]](#activate-dynamic-media-with-openapi)を参照してください。

### [!DNL Dynamic Media] 会社を作成してリスト化 {#create-and-list-dynamic-media-companies}

AEM Cloud Service 環境に [!DNL Dynamic Media] 会社を作成してリスト化し、AEM 環境内の設定を管理します。

#### 開始する準備を整える {#prerequisites-to-create-and-list-dynamic-media-companies}

IMS 組織で既存の会社（アカウント）を表示するか、新しい [!DNL Dynamic Media] 会社（アカウント）を追加するには、次の要件を満たしていることを確認します。

1. [Cloud Manager へのアクセス権](https://experienceleague.adobe.com/ja/docs/experience-manager-cloud-service/content/onboarding/journey/cloud-manager)。

1. [!DNL Dynamic Media] Ultimate ライセンスがある。

#### IMS 組織の [!DNL Dynamic Media] 会社の作成とリスト化 {#create-and-list-dynamic-media-companies-in-your-ims-organisation}

[!DNL AEM] 環境内で設定できる新しい [!DNL Dynamic Media] 会社（アカウント）を作成してリスト化するには、次の手順を実行します。

1. [Cloud Manager ライセンスページ](https://experience-stage.adobe.com/#/@ssahnichstage/cloud-manager/license)に移動します。

1. 「**[!UICONTROL 会社を追加]**」をクリックすると、**[!UICONTROL Dynamic Media 会社を作成]**&#x200B;ダイアログボックスが表示されます。

1. 一意の [!DNL Dynamic Media] 会社名を指定し、会社の地域を選択して、会社の管理者のメール ID のリストをコンマで区切って追加します。

   ![Dynamic Media 会社を作成](/help/assets/assets/create-dynamic-media-company.png){width="500" align="left"}

1. 「**[!UICONTROL 作成]**」をクリックして、会社の作成を開始します。このアクションにより、「**[!UICONTROL [!DNL Dynamic Media]会社]**」セクションに新しい行が追加され、会社の&#x200B;**[!UICONTROL ステータス]**&#x200B;に「**[!UICONTROL 設定中]**」と表示されます。

   ![Dynamic Media 会社の作成の開始](/help/assets/assets/dm-company-creation-initiated.png)

1. **オプション：**![情報アイコン](/help/assets/assets/info-icon-solid-black.svg) をクリックして、会社の詳細を表示します。会社を作成すると、**[!UICONTROL ステータス]**&#x200B;が&#x200B;**[!UICONTROL 準備完了]**&#x200B;に更新されます。

   ![Dynamic Media 会社の情報](/help/assets/assets/dm-company-information.png)

1. Dynamic Media 管理者は、[!DNL AEM] Cloud Service 環境で会社を[設定 [!DNL Dynamic Media]](/help/assets/dynamic-media/config-dm.md#architecture-diagram-of-dynamic-media)する手順のリストを含むウェルカムメールをメールボックスで確認してから開始してください。

   ![ウェルカムメール](/help/assets/assets/welcome-email.png)

#### 会社の作成の再試行 {#retry-company-creation}

[!DNL Dynamic Media] 会社の作成に失敗した場合は、失敗ステータスに基づいて次の手順を実行します。

1. **[!UICONTROL ステータス]**&#x200B;が保留中の場合、解決するにはカスタマーサポートチームに問題を報告してください。

   ![保留中ステータス](/help/assets/assets/company-creation-pending-status.png){width="350" align="left"}

1. **[!UICONTROL ステータス]**&#x200B;が失敗の場合は、失敗の理由に基づいて再試行します。

   ![失敗ステータス](/help/assets/assets/company-creation-failure-status.png){width="380" align="left"}

### オプション：配信層でカスタムドメインを設定 {#configure-custom-domain-in-delivery-tier}

AEM as a Cloud Service にはデフォルトのドメインが設定されていますが、必要に応じてカスタマイズできます。Cloud Manager を使用して、配信層にカスタムドメインを添付します。

#### 開始する準備を整える {#prerequisites-to-configure-custom-domain-in-delivery-tier}

設定プロセスを開始する前に、次の要件を満たしていることを確認します。

1. [Cloud Manager へのアクセス権](https://experienceleague.adobe.com/ja/docs/experience-manager-cloud-service/content/onboarding/journey/cloud-manager)。
1. [お使いの環境で  [!DNL Dynamic Media with OpenAPI]  が既にアクティベートされている](#activate-dynamic-media-with-openapi)。
1. 準備完了状態で [!DNL Dynamic Media with OpenAPI] が有効になっている。
1. 配信層に使用するドメインの EV または OV タイプの証明書。詳しくは、[SSL 証明書の概要](https://experienceleague.adobe.com/ja/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/manage-ssl-certificates/introduction-to-ssl-certificates)を参照してください。

#### Cloud Manager を使用した配信層でのカスタムドメインの設定 {#configure-custom-domain-in-delivery-tier-using-cloud-manager}

Cloud Manager で次の手順を実行して、配信層にカスタムドメインを設定します。

1. [顧客が管理する SSL 証明書を追加](https://experienceleague.adobe.com/ja/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/manage-ssl-certificates/add-ssl-certificate#add-customer-managed-ssl-cert)します。

1. [カスタムドメイン名を追加](https://experienceleague.adobe.com/ja/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/custom-domain-names/add-custom-domain-name#adding-cdn-settings)します。

1. 環境の詳細ページに移動して、[CDN 設定を追加](https://experienceleague.adobe.com/ja/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/cdn-configurations/add-cdn-config)します。設定を追加する際に、**[!UICONTROL CDN を設定]**&#x200B;ダイアログボックスの「**[!UICONTROL 層]**」フィールドで「**[!UICONTROL 配信]**」を選択します。

   ![CDN を設定](/help/assets/assets/select-delivery-tier-in-configure-cdn-form.png)

   設定を追加すると、**[!UICONTROL CDN 設定]**&#x200B;の&#x200B;**[!UICONTROL ステータス]**&#x200B;が「**[!UICONTROL 適用済み]**」に更新されます。

   ![CDN デプロイメントステータスを設定](/help/assets/assets/cdn-configuration-deployment-status.png)

1. 「その他のオプション」（![その他のオプション](/help/assets/assets/three-dots.svg)）をクリックし、「**[!UICONTROL 実稼動対応]**」を選択して、**[!UICONTROL 実稼動対応]**&#x200B;ダイアログボックスを表示します。

   ![実稼動対応オプション](/help/assets/assets/go-live-readiness-option.png)

1. **[!UICONTROL CNAME を設定]**&#x200B;手順を実行して、DNS サービスプロバイダーの DNS レコードに [cdn.adobeaemcloud.com](http://cdn.adobeaemcloud.com/)（CNAME レコード）をマッピングします。このマッピングにより、カスタムドメインで受信したリクエストがアドビの CDN にリダイレクトされるようになります。

   ![実稼動対応ダイアログ](/help/assets/assets/go-live-readiness-dialogbox.png){width="500" align="left"}

1. 「**[!UICONTROL OK]**」をクリックすると、**[!UICONTROL ステータス]**&#x200B;が&#x200B;**[!UICONTROL 検証済み]**&#x200B;に更新されます。これで、カスタムドメインを配信 URL で使用する準備が整いました。


   ![CDN を設定](/help/assets/assets/cdn-configurations-varified.png)



<!--
### Onboard API keys {#onboarding-api-keys}

Create an API key to access [!DNL Dynamic Media] with OpenAPIs and the delivery tier backed Asset Selector.

#### Prepare yourself for API keys onboarding process {#prerequisites-for-onboarding-api-keys} 

To start the API keys onboarding process, ensure you have:

1. [Access to Cloud Manager](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/onboarding/journey/cloud-manager).
1. [Activated [!DNL Dynamic Media with OpenAPI] in your environment](#activate-dynamic-media-with-openapi).
1. [Access to the Adobe Developer Console](https://experienceleague.adobe.com/en/docs/experience-manager-learn/cloud-service/aem-apis/invoke-openapi-based-aem-apis#create-adobe-developer-console-adc-project).

#### Onboard the API keys using [!DNL AEM Dynamic Media] API card {#onboarding-api-keys-using-aem-dynamic-media-api-card}

Use the [Adobe Developer Console](https://developer.adobe.com/developer-console/) to onboard the API keys to:

1. [Access Dynamic Media APIs](#access-dynamic-media-apis)
1. [Access Delivery tier backed Asset Selector](#access-delivery-tier-backed-asset-selector)

#### Create an API key to access [!DNL Dynamic Media] with OpenAPIs {#access-dynamic-media-apis}

Execute the following steps to create an API key to access [!DNL Dynamic Media] with OpenAPIs:

1. Navigate to the **[!UICONTROL Admin Console]**. The Admin Console displays the **[!UICONTROL author]**, **[!UICONTROL delivery]** and **[!UICONTROL publish]** instances.
![instances on admin console](/help/assets/assets/delivery-instance-admin-console.png)
1. Select the **[!UICONTROL delivery]** instance to display the product profile with **[!UICONTROL AEM Dynamic Media enable API Services]** enabled by default. The product profile looks like this: **[!UICONTROL AEM Assets DM OpenAPI Users - delivery  - Program [ID Number] - Environment [ID Number]]**. 

   ![product profile on admin console](/help/assets/assets/admin-console-product-profile.png)

   >[!NOTE]
   >
   >This delivery instance is common for [!DNL Content Hub] and [!DNL Dynamic Media] with OpenAPI capabilities.

1. Navigate to the [Adobe Developer console](https://developer.adobe.com/console) and [create a new project](https://developer.adobe.com/dep/guides/dev-console/create-project/). See [Invoke OpenAPI-based AEM APIs for server to server authentication](https://experienceleague.adobe.com/en/docs/experience-manager-learn/cloud-service/aem-apis/invoke-openapi-based-aem-apis) to learn about creating a new project.
1. Select **[!UICONTROL AEM Dynamic Media API]** to access to the [!DNL Dynamic Media with OpenAPI capabilities] and click **[!UICONTROL Next]**.
![adobe developer console](/help/assets/assets/adobe-developer-console.png)
1. Select **[!UICONTROL Server-to-Server Authentication]** and click **[!UICONTROL Next]**. See [Server to Server authentication](https://developer.adobe.com/developer-console/docs/guides/authentication/ServerToServerAuthentication/) to learn more about this authentication type.
![server-to-server-authentication](/help/assets/assets/server-to-server-authentication.png)
1. Select **[!UICONTROL OAuth Server-to-Server]**, specify a unique **[!UICONTROL Credential name]** and click **[!UICONTROL Next]**.
![oauth server to server credential](/help/assets/assets/oauth-server-server-and-credential-name.png)
1. Select your product profile (mentioned in step 2) to access the APIs using the environment's delivery endpoint and click **[!UICONTROL Save configured API]**.
![select product profile](/help/assets/assets/select-product-profile.png)
1. Select **[!UICONTROL AEM Dynamic Media API]**. Use the **[!UICONTROL OAuth Server-to-Server]** to fetch the **X-API-key** and access the token for the **authorization** header. 
![oauth server to server](/help/assets/assets/oauth-server-to-server-credentials.png)
Execute the below steps to use [Dynamic Media with OpenAPIs](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/stable/assets/delivery/) using the **[!UICONTROL OAuth Server-to-Server]** credentials. 
    1. Copy the **[!UICONTROL API KEY (Client ID)]** and replace the `X-Api-Key` in the cURL.
    1. Click **[!UICONTROL Generate access token]** to generate an access token and replace `YOUR_JWT_HERE` with the token in the cURL.

The cURL looks like this:
```
headers: {
    'Content-Type': 'application/json',
      'X-Adobe-Accept-Experimental': '1',
      Authorization: 'Bearer <YOUR_JWT_HERE>',
      'X-Api-Key': 'YOUR_API_KEY_HERE'
    `},
```
See [Search Assets API](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/assets/dynamicmedia/dynamic-media-open-apis/search-assets-api#search-assets-api-header) for more information.

### Access Delivery tier backed Asset Selector {#access-delivery-tier-backed-asset-selector}

TBD: Wiki in progress..
-->

## [!DNL Dynamic Media] Prime を有効にする {#enable-dynamic-media-prime}

[!DNL Dynamic Media] Prime を有効にするには、Cloud Service 環境で次の手順を実行します。

1. [OpenAPI を備えた Dynamic Media をアクティベート](#activate-dynamic-media-with-openapi)
1. [オプション：配信層でカスタムドメインを設定](#configure-custom-domain-in-delivery-tier)

<!--
1. [Onboard API keys using the AEM Dynamic Media API card](#onboarding-api-keys)
-->
