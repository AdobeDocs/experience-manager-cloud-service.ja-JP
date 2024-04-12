---
title: Brand Portal を使用した AEM Assets as a  [!DNL Cloud Service]  設定
description: AEM AssetsとBrand Portalの設定方法を説明します。 この設定を使用すると、承認済みのブランドアセットをAEMインスタンスからBrand Portalに公開し、Brand Portalユーザーに配布できます。
contentOwner: AK
feature: Brand Portal,Asset Distribution,Configuration
role: Admin
exl-id: 078e522f-bcd8-4734-95db-ddc8772de785
source-git-commit: 2cb630203b818ae338fe6b7c2ff341c76e3a3958
workflow-type: ht
source-wordcount: '2566'
ht-degree: 100%

---

# Brand Portal を使用した Experience Manager Assets 設定 {#configure-aem-assets-with-brand-portal}

| バージョン | 記事リンク |
| -------- | ---------------------------- |
| AEM 6.5 | [ここをクリックしてください](https://experienceleague.adobe.com/docs/experience-manager-65/assets/brandportal/configure-aem-assets-with-brand-portal.html?lang=ja) |
| AEM as a Cloud Service | この記事 |

Adobe Experience Manager Assets Brand Portal を設定すると、承認済みのブランドアセットを Adobe Experience Manager Assets as a [!DNL Cloud Service] インスタンスから Brand Portal に公開し、Brand Portal ユーザーに配信できます。

## Cloud Manager を使用して Brand Portal をアクティベート {#activate-brand-portal}

Cloud Manager ユーザーは、Experience Manager Assets as a [!DNL Cloud Service] インスタンス用の Brand Portal をアクティブ化します。アクティブ化のワークフローでは、必要な設定（認証トークン、IMS 設定および Brand Portal クラウドサービス）がバックエンドで作成され、Cloud Manager の Brand Portal テナントのステータスが反映されます。Brand Portal をアクティブ化すると、Experience Manager Assets のユーザーが Brand Portal にアセットを公開して、Brand Portal ユーザーに配布できるようになります。

**前提条件**

Experience Manager Assets as a [!DNL Cloud Service] インスタンスで Brand Portal をアクティブ化するには、次のものが必要です。

* 稼働中の Experience Manager Assets as a [!DNL Cloud Service] インスタンス。
* Cloud Manager 製品のプロファイルに割り当てられている、Cloud Manager にアクセスできるユーザー。詳しくは、[Cloud Manager へのアクセス](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/security/ims-support.html?lang=ja#accessing-cloud-manager)を参照してください。

>[!NOTE]
>
>Brand Portal テナントに接続するには、Experience Manager Assets as a [!DNL Cloud Service] インスタンスに設定済みの実稼動環境が必要です。

**Brand Portal をアクティブ化する手順**

Brand Portal のライセンス認証は、Experience Manager Assets as a [!DNL Cloud Service] インスタンス用の実稼動環境を作成する際に行うことも、別個に行うこともできます。環境が既に作成されており、Brand Portal をライセンス認証する必要があるとします。

1. Adobe Cloud Manager にログインし、**[!UICONTROL 環境]**&#x200B;に移動します。

   **[!UICONTROL 環境]**&#x200B;ページには、既存の環境のリストが表示されます。

1. 環境の詳細を表示するリストから環境を（1 つずつ）選択します。

   Brand Portal には利用可能な環境のうちいずれかの権利が付与され、**[!UICONTROL 環境情報]**&#x200B;に反映されます。

   Brand Portal に関連付けられている環境を見つけたら、「**[!UICONTROL Brand Portal のライセンス認証]**」ボタンをクリックして、アクティベーションワークフローを開始します。

   ![Brand Portal のライセンス認証](assets/create-environment4.png)

1. アクティベーションワークフローがバックエンドで必要な設定を作成するので、Brand Portal テナントのライセンス認証に数分かかります。Brand Portal テナントがライセンス認証されると、ステータスが「アクティベート済み」に変わります。

   ![表示ステータス](assets/create-environment5.png)


>[!NOTE]
>
>Brand Portal は、Experience Manager Assets as [!DNL Cloud Service] インスタンスと同じ IMS 組織でアクティブ化する必要があります。
>
>IMS 組織（org1-existing）の Brand Portal クラウド設定が既にあり（[Adobe Developer Console](#manual-configuration) を使用して手動で設定）、Experience Manager Assets as a [!DNL Cloud Service] インスタンスが別の IMS 組織（org2-new）に設定されている場合、Cloud Manager から Brand Portal をアクティブ化すると Brand Portal の IMS 組織は `org2-new` にリセットされます。`org1-existing` で手動で設定したクラウド設定は、Experience Manager Assets のオーサーインスタンスに表示されますが、Cloud Manager で Brand Portal をアクティブ化すると使用されなくなります。
>
>既存の Brand Portal クラウド設定と Experience Manager Assets as a [!DNL Cloud Service] インスタンスが同じ IMS 組織（org1）を使用している場合は、Cloud Manager から Brand Portal をアクティブ化するだけで済みます。
>
>自動生成された設定は変更しないでください。

**関連トピック**：

* [Experience Manager Assets as a Cloud Service へのユーザーと役割の追加](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/requirements/setting-up-users-and-roles.html?lang=ja)

* [Cloud Manager での環境の管理](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/manage-environments.html?lang=ja#adding-environments)


**Brand Portal テナントにログイン**：

Cloud Manager で Brand Portal テナントをライセンス認証した後、Admin Console から、またはテナント URL を直接使用して、Brand Portal にログインできます。

Brand Portal テナントのデフォルト URL は `https://<tenant-id>.brand-portal.adobe.com/` です。

ここで、テナント ID は IMS 組織です。

ブランドポータルの URL が不明な場合は、次の手順を実行します。

1. [Admin Console](https://adminconsole.adobe.com/) にログインし、**[!UICONTROL 製品]**&#x200B;に移動します。
1. 左パネルの「**[!UICONTROL Adobe Experience Manager Brand Portal - Brand Portal]**」を選択します。
1. 「**[!UICONTROL Brand Portal に移動]**」をクリックして、ブラウザーで直接 Brand Portal を開きます。

   または、**[!UICONTROL Brand Portal へ移動]**&#x200B;リンクから Brand Portal テナント URL をコピーし、ブラウザーに貼り付けて Brand Portal インターフェイスを開きます。

   ![Brand Portal にアクセス](assets/access-bp-on-cloud.png)


**接続をテストします。**

Experience Manager Assets as a [!DNL Cloud Service] インスタンスと Brand Portal テナントとの接続を検証するには、次の手順を実行します。

1. Experience Manager Assets にログインします。

1. **ツール**&#x200B;パネルで、**[!UICONTROL デプロイメント]**／**[!UICONTROL 配布]**&#x200B;に移動します。

   ![配布オプションに移動します。](assets/test-bpconfig1.png)

   Brand Portal 配布エージェント（**[!UICONTROL bpdistributionagent0]**）は、「**[!UICONTROL Brand Portal に公開]**」の下に作成されます。

   ![配布エージェントを作成](assets/test-bpconfig2.png)

1. 「**[!UICONTROL Brand Portal に公開]**」をクリックして、配布エージェントを開きます。

   「**[!UICONTROL ステータス]**」タブに配布キューが表示されます。

   配布エージェントには、次の 2 つのキューが含まれます。
   * **processing-queue**：Brand Portal へのアセット配布用。

   * **error-queue**：配布が失敗したアセット用。

   >[!NOTE]
   >
   >エラーを確認し、**error-queue** を定期的に消去することをお勧めします。

   ![アセット配布用の処理キュー](assets/test-bpconfig3.png)

1. Experience Manager Assets as a [!DNL Cloud Service] と Brand Portal との接続を確認するには、「**[!UICONTROL 接続をテスト]**」アイコンをクリックします。

   ![AEM と Brand Portal 間の接続を検証](assets/test-bpconfig4.png)

   *テストパッケージが正常に配信された*&#x200B;ことを示すメッセージが表示されます。

   >[!NOTE]
   >
   >配布エージェントを無効にしないでください。無効にすると、（実行中のキュー内の）アセットの配布が失敗する可能性があります。

Experience Manager Assets as a [!DNL Cloud Service] インスタンスと Brand Portal テナントとの接続を確認するには、Experience Manager Assets から Brand Portal にアセットを公開します。接続に成功すると、公開されたアセットが Brand Portal インターフェイスに表示されます。


次の操作が可能になっています。

* [Experience Manager Assets から Brand Portal へのアセットの公開](publish-to-brand-portal.md)
* [Experience Manager Assets から Brand Portal へのフォルダーの公開](publish-to-brand-portal.md#publish-folders-to-brand-portal)
* [Experience Manager Assets から Brand Portal へのコレクションの公開](publish-to-brand-portal.md#publish-collections-to-brand-portal)
* [Brand Portal から Experience Manager Assets へのアセットの公開](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/asset-sourcing-in-brand-portal/brand-portal-asset-sourcing.html?lang=ja) - Brand Portal でのアセットソーシング
* [Brand Portal へのプリセット、スキーマ、ファセットの公開](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/publish/publish-schema-search-facets-presets.html?lang=ja)
* [Brand Portal へのタグの公開](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/publish/brand-portal-publish-tags.html?lang=ja)

詳しくは、 [Brand Portal ドキュメント](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/home.html?lang=ja) を参照してください。

**配布ログ**

配布エージェントのログで、アセット発行ワークフローを監視できます。

Experience Manager Assets から Brand Portal にアセットを公開して、ログを確認しましょう。

1. 「**設定のテスト**」節で示した手順（1 ～ 4）に従い、配布エージェントページに移動します。
1. 「**[!UICONTROL ログ]**」をクリックして、処理ログとエラーログを表示します。

   ![処理ログとエラーログ](assets/test-bpconfig5.png)

配布エージェントは次のログを生成します。

* 情報：これは、配布エージェントの構成が正常に完了したときにトリガーされるシステムが生成するログです。
* DSTRQ1（リクエスト 1）：テスト接続時にトリガーされます。

アセットの公開時に、次の要求および応答ログが生成されます。

**配布エージェントの要求**：

* DSTRQ2（リクエスト 2）：アセットの公開リクエストがトリガーされます。
* DSTRQ3（リクエスト 3）：システムは、アセットが存在する Experience Manager Assets フォルダーを公開する別のリクエストをトリガーし、そのフォルダーを Brand Portal に複製します。

**配布エージェントの応答**：

* queue-bpdistributionagent0（DSTRQ2）：アセットが Brand Portal に公開されます。
* queue-bpdistributionagent0（DSTRQ3）：システムは、アセットを含んだ Experience Manager Assets フォルダーを Brand Portal に複製します。

上記の例では、追加の要求と応答がトリガーされます。アセットが初めて公開されたため、システムは Brand Portal で親フォルダー（パスの追加）を見つけることができず、アセットが公開されている Brand Portal で同じ名前の親フォルダーを作成する追加リクエストをトリガーしました。

>[!NOTE]
>
>親フォルダーが Brand Portal に存在しない場合や Experience Manager Assets で変更された場合には、追加のリクエストが生成されます。

Experience Manager Assets as a [!DNL Cloud Service] で Brand Portal をアクティブ化する自動処理ワークフロー以外に、Adobe Developer Console を使用して Experience Manager Assets as a [!DNL Cloud Service] と Brand Portal の連携を手動で設定する方法もありますが、こちらの方法はお勧めしません。

>[!NOTE]
>
>Brand Portal テナントのライセンス認証中に問題が発生した場合は、カスタマーサポートにお問い合わせください。

## Adobe Developer Console を使用した手動設定 {#manual-configuration}

次の節では、Adobe Developer Console を使用して Experience Manager Assets as a [!DNL Cloud Service] と Brand Portal の連携を手動で設定する方法について説明します。

以前は、Experience Manager Assets as a [!DNL Cloud Service] と Brand Portal の連携は Adobe Developer Console を介して手動で設定されており、Brand Portal テナントの認証のために Adobe Identity Management Services（IMS）アカウントトークンを入手していました。それには、Experience Manager Assets と Adobe Developer Console の両方で設定を行う必要があります。

1. Experience Manager Assets で、IMS アカウントを作成し、公開鍵（証明書）を生成します。
1. Adobe 開発者コンソールで、Brand Portal テナント（組織）用のプロジェクトを作成します。
1. そのプロジェクトで、公開鍵で API を設定して、サービスアカウント接続を作成します。
1. サービスアカウント資格情報と JSON Web トーケン（JWT）ペイロード情報を取得します。
1. Experience Manager Assets で、サービスアカウント資格情報と JWT ペイロードを使用して IMS アカウントを設定します。
1. Experience Manager Assets で、IMS アカウントと Brand Portal エンドポイント（組織 URL）を使用して Brand Portal クラウドサービスを設定します。
1. Experience Manager Assets から Brand Portal にアセットを公開して、設定をテストします。

>[!NOTE]
>
>Experience Manager Assets as a [!DNL Cloud Service] インスタンスは、1 つの Brand Portal テナントに対してのみ設定される必要があります。

**前提条件**

Experience Manager Assets と Brand Portal の連携を設定するには、以下が必要です。

* 稼働中の Experience Manager Assets as a [!DNL Cloud Service] インスタンス
* Brand Portal テナント URL
* Brand Portal テナントの IMS 組織に対するシステム管理者権限を持つユーザー

## 設定の作成 {#create-new-configuration}

指定した順序で次の手順を実行して、Brand Portal で Experience Manager Assets を設定します。

1. [公開証明書の取得](#public-certificate)
1. [サービスアカウント（JWT）接続の作成](#createnewintegration)
1. [IMS アカウントの設定](#create-ims-account-configuration)
1. [Cloud Service の設定](#configure-the-cloud-service)

### IMS 設定の作成 {#create-ims-configuration}

IMS 設定では、Brand Portal テナントで Experience Manager as a [!DNL Cloud Service] インスタンスを認証します。

IMS 設定には、次の 2 つの手順が含まれます。

* [公開証明書の取得](#public-certificate)
* [IMS アカウントの設定](#create-ims-account-configuration)

### 公開証明書の取得 {#public-certificate}

公開鍵（証明書）は、Adobe 開発者コンソールでプロファイルを認証します。

1. Experience Manager Assets にログインします。
1. **ツール**&#x200B;パネルで、**[!UICONTROL セキュリティ]**／**[!UICONTROL Adobe IMS 設定]**&#x200B;に移動します。
1. Adobe IMS 設定ページで、「**[!UICONTROL 作成]**」をクリックします。**[!UICONTROL Adobe IMS 技術アカウント設定]**&#x200B;ページにリダイレクトされます。デフォルトでは、「**証明書**」タブが開きます。
1. 「**[!UICONTROL クラウドソリューション]**」ドロップダウンリストで「**[!UICONTROL Adobe Brand Portal]**」を選択します。
1. 「**[!UICONTROL 新しい証明書を作成]**」チェックボックスをオンにして、公開鍵の **エイリアス** を指定します。ここで入力したエイリアスが、公開鍵になります。
1. 「**[!UICONTROL 証明書を作成]**」をクリックします。「**[!UICONTROL OK]**」をクリックして公開証明書を生成します。

   ![証明書を作成](assets/ims-config2.png)

1. **[!UICONTROL 公開鍵をダウンロード]** アイコンをクリックして、公開鍵（CRT）ファイルをローカルマシンに保存します。

   この公開鍵は、Brand Portal テナントの API を設定し、Adobe 開発者コンソールでサービスアカウント資格情報を生成するために後で使用します。

   ![証明書をダウンロード](assets/ims-config3.png)

1. 「**[!UICONTROL 次へ]**」をクリックします。

   「**アカウント**」タブで、Adobe IMS アカウントが作成されます。このアカウントには、Adobe 開発者コンソールで生成されるサービスアカウント資格情報が必要です。このページは開いたままにしておきます。

   新しいタブを開き、 [Adobe 開発者コンソールでサービスアカウント（JWT）接続を作成](#createnewintegration) して、IMS アカウントを設定するための資格情報と JWT ペイロードを取得します。

### サービスアカウント（JWT）接続の作成 {#createnewintegration}

Adobe 開発者コンソールで、プロジェクトと API を Brand Portal テナント（組織）レベルで設定します。API を設定すると、サービスアカウント（JWT）接続が作成されます。API を設定するには、キーペア（秘密鍵と公開鍵）を生成する方法と、公開鍵をアップロードする方法の 2 とおりがあります。Brand Portal で Experience Manager Assets を設定するには、Experience Manager Assets で公開鍵（証明書）を生成し、その公開鍵をアップロードして Adobe Developer コンソールで資格情報を作成する必要があります。これらの資格情報は、Experience Manager Assets で IMS アカウントを設定するために必要です。IMS アカウントを設定したら、Experience Manager Assets に Brand Portal クラウドサービスを設定できます。

サービスアカウント資格情報と JWT ペイロードを生成するには、次の手順を実行します。

1. IMS 組織（Brand Portal テナント）のシステム管理者権限で Adobe Developer Console にログインします。デフォルトの URL は [https://www.adobe.com/go/devs_console_ui](https://www.adobe.com/go/devs_console_ui) です。


   >[!NOTE]
   >
   >右上隅にあるドロップダウン（組織）リストから正しい IMS 組織（Brand Portal テナント）が選択されていることを確認します。

1. 「**[!UICONTROL 新規プロジェクトを作成]**」をクリックします。システムで生成された名前を持つ空のプロジェクトが組織に対して作成されます。

   「**[!UICONTROL プロジェクトを編集]**」をクリックして、「**[!UICONTROL プロジェクトタイトル]**」と「**[!UICONTROL 説明]**」をアップデートし、「**[!UICONTROL 保存]**」をクリックします。

1. 「**[!UICONTROL プロジェクトの概要]**」タブで、「**[!UICONTROL API を追加]**」をクリックします。

1. **[!UICONTROL API を追加]**&#x200B;ウィンドウで、「**[!UICONTROL AEM Brand Portal]**」を選択し、「**[!UICONTROL 次へ]**」をクリックします。

   Experience Manager Brand Portal サービスにアクセスできることを確認します。

1. **[!UICONTROL API を設定]**&#x200B;ウィンドウで、「**[!UICONTROL 公開鍵をアップロード]**」をクリックします。次に、「**[!UICONTROL ファイルを選択]**」をクリックし、[公開証明書の取得](#public-certificate)のセクションでダウンロードした公開鍵（.crt ファイル）をアップロードします。

   「**[!UICONTROL 次へ]**」をクリックします。

   ![「公開鍵をアップロード」](assets/service-account3.png)

1. 公開鍵を確認し、「**[!UICONTROL 次へ]**」をクリックします。

1. デフォルトの製品プロファイルとして「**[!UICONTROL Assets Brand Portal]**」を選択し、「**[!UICONTROL 設定済み API を保存]**」をクリックします。

   ![製品プロファイルを選択](assets/service-account4.png)

1. API が設定されると、API の概要ページにリダイレクトされます。「**[!UICONTROL 資格情報]**」の下の左側のナビゲーションで「**[!UICONTROL サービスアカウント（JWT）]**」オプションをクリックします。

   >[!NOTE]
   >
   >* 資格情報を確認し、必要に応じて、JWT トークンの生成、資格情報の詳細のコピー、クライアントの秘密鍵の取得などのアクションを実行できます。
   >* 現在、アドビの Developer Console サービスアカウント（JWT）資格情報タイプのみがサポートされています。`OAuth Server-to-Server` 資格情報タイプは、4 月中旬にサポートされるまで使用しないでください。詳しくは、[Adobe Developer Console での JWT 資格情報の非推奨（廃止予定）](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/security/jwt-credentials-deprecation-in-adobe-developer-console.html?lang=ja)を参照してください。

1. 「**[!UICONTROL クライアント資格情報]**」タブから、**[!UICONTROL クライアント ID]** をコピーします。

   「**[!UICONTROL クライアント秘密鍵を取得]**」をクリックし、**[!UICONTROL クライアントの秘密鍵]**&#x200B;をコピーします。

   ![サービスアカウント資格情報](assets/service-account5.png)

1. 「**[!UICONTROL JWT を生成]**」タブに移動し、**[!UICONTROL JWT ペイロード]**&#x200B;情報をコピーします。

これで、クライアント ID（API キー）、クライアントシークレット、JWT ペイロードを使用して、Experience Manager Assets に [IMS アカウントを設定](#create-ims-account-configuration)できるようになりました。

<!--
1. Click **[!UICONTROL Create Integration]**.

1. Select **[!UICONTROL Access an API]**, and click **[!UICONTROL Continue]**.

   ![Create New Integration](assets/create-new-integration1.png)

1. Create an integration page. 
   
   Select your organization from the drop-down list.

   In **[!UICONTROL Experience Cloud]**, Select **[!UICONTROL AEM Brand Portal]** and click **[!UICONTROL Continue]**. 

   If the Brand Portal option is disabled for you, ensure that you have selected correct organization from the drop-down box above the **[!UICONTROL Adobe Services]** option. If you do not know your organization, contact your administrator.

   ![Create Integration](assets/create-new-integration2.png)

1. Specify a name and description for the integration. Click **[!UICONTROL Select a File from your computer]** and upload the `AEM-Adobe-IMS.crt` file downloaded in the [obtain public certificates](#public-certificate) section.

1. Select the profile of your organization. 

   Or, select the default profile **[!UICONTROL Assets Brand Portal]** and click **[!UICONTROL Create Integration]**. The integration is created.

1. Click **[!UICONTROL Continue to integration details]** to view the integration information. 

   Copy the **[!UICONTROL API Key]** 
   
   Click **[!UICONTROL Retrieve Client Secret]** and copy the Client Secret key.

   ![API Key, Client Secret, and payload information of an integration](assets/create-new-integration3.png)

1. Navigate to **[!UICONTROL JWT]** tab, and copy the **[!UICONTROL JWT payload]**.

   The API Key, Client Secret key, and JWT payload information is used to create IMS account configuration.

-->

### IMS アカウントの設定 {#create-ims-account-configuration}

次の手順を実行したことを確認します。

* [公開証明書の取得](#public-certificate)
* [サービスアカウント（JWT）接続の作成](#createnewintegration)

IMS アカウントを設定するには、次の手順を実行します。

1. IMS 設定を開き、「**[!UICONTROL アカウント]**」タブに移動します。[公開証明書の取得](#public-certificate)中も、ページは開いたままになっています。

1. IMS アカウントの&#x200B;**[!UICONTROL タイトル]**&#x200B;を指定します。

   「**[!UICONTROL 認証サーバー]**」フィールドで、URL「 [https://ims-na1.adobelogin.com/](https://ims-na1.adobelogin.com/)」を指定します。

   **[!UICONTROL API キー]**&#x200B;にクライアント ID を指定し、[サービスアカウント（JWT）接続の作成](#createnewintegration)時にコピーした&#x200B;**[!UICONTROL クライアントの秘密鍵]**&#x200B;と&#x200B;**[!UICONTROL ペイロード]**（JWT ペイロード）を貼り付けます。

   「**[!UICONTROL 作成]**」をクリックします。

   IMS アカウントが設定されます。

   ![IMS アカウントの設定](assets/create-new-integration6.png)


1. その IMS アカウント設定を選択し、「**[!UICONTROL 正常性をチェック]**」をクリックします。

   ダイアログボックスの「**[!UICONTROL チェック]**」をクリックします。正常に設定されると、*トークンが正常に取得されました*&#x200B;というメッセージが表示されます。

   ![Adobe IMSの設定が正常性をチェックします。](assets/create-new-integration5.png)

>[!CAUTION]
>
>IMS 設定は 1 つだけにする必要があります。
>
>IMS 設定がヘルスチェックに合格していることを確認します。設定がヘルスチェックに合格しない場合は無効です。削除して、別の有効な設定を作成する必要があります。

### Cloud Service の設定 {#configure-the-cloud-service}

Brand Portal Cloud Service を設定するには、次の手順を実行します。

1. Experience Manager Assets にログインします。

1. **ツール**&#x200B;パネルで、**[!UICONTROL クラウドサービス]**／**[!UICONTROL AEM Brand Portal]** に移動します。

1. Brand Portal の設定ページで、「**[!UICONTROL 作成]**」をクリックします。

1. 設定の&#x200B;**[!UICONTROL タイトル]**&#x200B;を入力します。

   [IMS アカウントの設定](#create-ims-account-configuration) 時に作成した IMS 設定を選択します。

   「**[!UICONTROL サービス URL]**」に、Brand Portal テナント（組織）URL を入力します。

   ![Brand Portal Configuration ダイアログボックス](assets/create-cloud-service.png)

1. 「**[!UICONTROL 保存して閉じる]**」をクリックします。クラウド設定が作成されます。

   これで、Experience Manager Assets as [!DNL Cloud Service] インスタンスが Brand Portal で設定されました。

これで、配信エージェントを確認し、Brand Portal にアセットを公開することで、設定をテストできます。

**セキュアプレビューが有効な場合は、SPS でエグレス IP を許可リストに登録する**
（会社に対して[セキュアプレビューが有効](#https://experienceleague.adobe.com/docs/dynamic-media-classic/using/upload-publish/testing-assets-making-them-public.html?lang=en)な状態で）Dynamic Media - Scene7 を使用する場合は、Scene7 会社管理者が SPS（Scene7 Publishing System）Flash UI を使用して、それぞれの地域の[公開エグレス IP を許可リストに登録する](#https://experienceleague.adobe.com/docs/dynamic-media-classic/using/upload-publish/testing-assets-making-them-public.html?lang=en#testing-the-secure-testing-service)ことをお勧めします。
エグレス IP は次のとおりです。

| **地域** | **エグレス IP** |
|--- |--- |
| 該当なし | 130.248.160.68, 20.94.203.130 |
| EMEA | 51.132.146.75、130.248.244.202、130.248.244.203、130.248.244.204、130.248.244.210、130.248.244.211,、130.248.244.212 |
| APAC | 63.140.44.54 |

<!--
### Test configuration {#test-configuration}

Perform the following steps to validate the configuration:

1. Login to AEM Assets.

1. From the **Tools** panel, navigate to **[!UICONTROL Deployment]** > **[!UICONTROL Distribution]**.

    ![test-bpconfig1](assets/test-bpconfig1.png)

   A Brand Portal distribution agent (**[!UICONTROL bpdistributionagent0]**) is created under **[!UICONTROL Publish to Brand Portal]**.

   ![test-bpconfig2](assets/test-bpconfig2.png)


1. Click **[!UICONTROL Publish to Brand Portal]** to open the distribution agent. 

   You can see the distribution queues under the **[!UICONTROL Status]** tab. 
   
   A distribution agent contains two queues: 
   * **processing-queue**: for the distribution of assets to Brand Portal. 

   * **error-queue**: for the assets where distribution has failed. 
   
   >[!NOTE]
   >
   >It is recommended to review the failures and  clear the **error-queue** periodically.  

   ![test-bpconfig3](assets/test-bpconfig3.png)

1. To verify the connection between AEM Assets as a [!DNL Cloud Service] and Brand Portal, click the **[!UICONTROL Test Connection]** icon.

   ![test-bpconfig4](assets/test-bpconfig4.png)

   A message appears that your *test package is successfully delivered*.

   >[!NOTE]
   >
   >Avoid disabling the distribution agent, as it can cause the distribution of the assets (running-in-queue) to fail.

You can now:

* [Publish assets from AEM Assets to Brand Portal](publish-to-brand-portal.md)
* [Publish folders from AEM Assets to Brand Portal](publish-to-brand-portal.md#publish-folders-to-brand-portal)
* [Publish collections from AEM Assets to Brand Portal](publish-to-brand-portal.md#publish-collections-to-brand-portal)
* [Publish assets from Brand Portal to AEM Assets](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/asset-sourcing-in-brand-portal/brand-portal-asset-sourcing.html) - Asset Sourcing in Brand Portal
* [Publish presets, schemas, and facets to Brand Portal](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/publish/publish-schema-search-facets-presets.html)
* [Publish tags to Brand Portal](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/publish/brand-portal-publish-tags.html)

See [Brand Portal documentation](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/home.html) for more information.

## Distribution logs {#distribution-logs}

You can monitor the distribution agent logs for the asset publishing workflow. 

For example, we have published an asset from AEM Assets to Brand Portal to validate the configuration. 

1. Follow the steps (from 1 to 4) as shown in the [Test Configuration](#test-configuration) section and navigate to the distribution agent page.
1. Click **[!UICONTROL Logs]** to view the processing and error logs.

   ![ctest-bpconfig4](assets/ctest-bpconfig4.png)

The distribution agent has generated the following logs:

* INFO: This is a system-generated log that triggers on successful configuration of the distribution agent. 
* DSTRQ1 (Request 1): Triggers on test connection.

On publishing the asset, the following request and response logs are generated:

**Distribution agent request**:

* DSTRQ2 (Request 2): The asset publishing request is triggered.
* DSTRQ3 (Request 3): The system triggers another request to publish the AEM Assets folder (in which the asset exists) and replicates the folder in Brand Portal.

**Distribution agent response**:

* queue-bpdistributionagent0 (DSTRQ2): The asset is published to Brand Portal.
* queue-bpdistributionagent0 (DSTRQ3): The system replicates the AEM Assets folder (containing the asset) in Brand Portal.

In the above example, an additional request and response is triggered. The system could not find the parent folder (Add Path) in Brand Portal because the asset was published for the first time, therefore, it triggered an additional request to create a parent folder with the same name in Brand Portal where the asset is published.  

>[!NOTE]
>
>Additional request is generated in case the parent folder does not exist in Brand Portal or has been modified in AEM Assets. 
-->

<!--

## Additional information {#additional-information}

Go to `/system/console/slingmetrics` for statistics related to the distributed content:

1. **Counter metrics**
   * sling: `mac_sync_request_failure`
   * sling: `mac_sync_request_received`
   * sling: `mac_sync_request_success`

1. **Time metrics**
   * sling: `mac_sync_distribution_duration`
   * sling: `mac_sync_enqueue_package_duration`
   * sling: `mac_sync_setup_request_duration`

-->

<!--
   Comment Type: draft

   <li> </li>
   -->

<!--
   Comment Type: draft

   <li>Step text</li>
-->

**関連情報**

* [アセットを翻訳](translate-assets.md)
* [Assets HTTP API](mac-api-assets.md)
* [AEM Assets as a Cloud Service でサポートされているファイル形式](file-format-support.md)
* [アセットを検索](search-assets.md)
* [接続されたアセット](use-assets-across-connected-assets-instances.md)
* [アセットレポート](asset-reports.md)
* [メタデータスキーマ](metadata-schemas.md)
* [アセットをダウンロード](download-assets-from-aem.md)
* [メタデータを管理](manage-metadata.md)
* [検索ファセット](search-facets.md)
* [コレクションを管理](manage-collections.md)
* [メタデータの一括読み込み](metadata-import-export.md)
