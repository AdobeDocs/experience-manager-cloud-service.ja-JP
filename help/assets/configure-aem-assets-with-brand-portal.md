---
title: AEM Assets as a [!DNL Cloud Service] と Brand Portal の連携の設定
description: AEM Assets と Brand Portal の連携を設定します。
contentOwner: Vishabh Gupta
feature: Brand Portal,Asset Distribution,Configuration
role: Admin
exl-id: 078e522f-bcd8-4734-95db-ddc8772de785
source-git-commit: d37193833d784f3f470780b8f28e53b473fd4e10
workflow-type: tm+mt
source-wordcount: '2402'
ht-degree: 98%

---

# AEM Assets as a[!DNL Cloud Service]と Brand Portal の連携の設定 {#configure-aem-assets-with-brand-portal}

Adobe Experience Manager Assets Brand Portal を設定すると、承認済みのブランドアセットを Adobe Experience Manager Assets as a [!DNL Cloud Service] インスタンスから Brand Portal に公開し、Brand Portal ユーザーに配信できます。

## Cloud Manager を使用して Brand Portal をライセンス認証する {#activate-brand-portal}

Cloud Manager ユーザーは、AEM Assets as a [!DNL Cloud Service] インスタンスで、Brand Potal をライセンス認証します。アクティベーションワークフローは、バックエンドに必要な設定（認証トークン、IMS 設定および Brand Portal クラウドサービス）を作成し、Cloud Manager の Brand Portal テナントのステータスを反映します。Brand Portal をライセンス認証すると、AEM Assets のユーザは Brand Portal にアセットを公開して、Brand Portal ユーザーに配信できます。

**前提条件**

AEM Assets as a [!DNL Cloud Service] インスタンスで Brand Portal をライセンス認証するには、以下が必要です。

* 実行中の AEM Assets as a [!DNL Cloud Service] インスタンス。
* Cloud Manager 製品のプロファイルに割り当てられている、Cloud Manager にアクセスできるユーザー。詳しくは、[Cloud Manager へのアクセス](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/security/ims-support.html#accessing-cloud-manager)を参照してください。

>[!NOTE]
>
>AEM Assets as a [!DNL Cloud Service] インスタンスは、1 つの Brand Portal テナントとのみ接続できます。AEM Assets as a [!DNL Cloud Service] インスタンスに複数の環境（開発、実稼動、ステージ）を設定できます。この場合、Brand Portal は 1 つの環境でアクティブになります。

**Brand Portal のライセンス認証手順**

Brand Portal は、AEM Assets as a [!DNL Cloud Service] のインスタンス用に環境を作成するか、または個別に作成するときにライセンス認証できます。環境が既に作成され、Brand Portal をライセンス認証する必要があるとします。

1. Adobe Cloud Manager にログインし、「**[!UICONTROL 環境]**」に移動します。

   **[!UICONTROL 環境]**&#x200B;ページには、既存の環境のリストが表示されます。

1. 環境の詳細を表示するリストから環境を（1 つずつ）選択します。

   Brand Portal には利用可能な環境のうちいずれかの権利が付与され、**[!UICONTROL 環境情報]**&#x200B;に反映されます。

   Brand Portal に関連付けられている環境を見つけたら、「**[!UICONTROL Brand Portal のライセンス認証]**」ボタンをクリックして、アクティベーションワークフローを開始します。

   ![Brand Portal のライセンス認証](assets/create-environment4.png)

1. アクティベーションワークフローがバックエンドで必要な設定を作成するので、Brand Portal テナントのライセンス認証に数分かかります。Brand Portal テナントがライセンス認証されると、ステータスが「アクティベート済み」に変わります。

   ![表示ステータス](assets/create-environment5.png)


>[!NOTE]
>
>Brand Portal は、AEM Assets as a [!DNL Cloud Service] インスタンスと同じ IMS 組織でライセンス認証する必要があります。
>
>IMS 組織（org1-existing）に既存の Brand Portal のクラウド設定（[Adobe 開発者コンソールを使用して手動で設定](#manual-configuration)）があり、AEM Assets as a [!DNL Cloud Service]インスタンスが別の IMS 組織（org2-new）に設定されている場合、Cloud Manager から Brand Portal のライセンス認証を行うと、Brand Portal IMS 組織が `org2-new` にリセットされます。`org1-existing` で手動で設定したクラウド設定は、AEM Assets のオーサーインスタンスには表示されますが、Cloud Manager で Brand Portal をアクティベートすると使用できなくなります。
>
>既存の Brand Portal クラウド設定と AEM Assets as a [!DNL Cloud Service] インスタンスが同じ IMS 組織（org1）を使用している場合は、Cloud Manager から Brand Portal をライセンス認証するだけで済みます。
>
>自動生成された設定は変更しないでください。

**関連トピック**:
* [AEM Assets as a Cloud Service でのユーザーと役割を追加する](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/requirements/setting-up-users-and-roles.html?lang=ja)

* [Cloud Manager での環境の管理](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/manage-environments.html#adding-environments)


**Brand Portal テナントへのログイン**

Cloud Manager で Brand Portal テナントをライセンス認証した後、Admin Console から、またはテナント URL を使用して直接 Brand Portal にログインできます。

Brand Portal テナントのデフォルト URL は `https://<tenant-id>.brand-portal.adobe.com/` です。

ここで、テナント ID は IMS 組織です。

ブランドポータルの URL が不明な場合は、次の手順を実行します。

1. [Admin Console](https://adminconsole.adobe.com/)にログインし、「**[!UICONTROL 製品]**」に移動します。
1. 左パネルの「**[!UICONTROL Adobe Experience Manager Brand Portal - Brand Portal]**」を選択します。
1. 「**[!UICONTROL Brand Portal に移動]**」をクリックして、ブラウザーで直接 Brand Portal を開きます。

   または、**[!UICONTROL Brand Portal へ移動]**&#x200B;リンクから Brand Portal テナント URL をコピーし、ブラウザーに貼り付けて Brand Portal インターフェイスを開きます。

   ![Brand Portal にアクセス](assets/access-bp-on-cloud.png)


**接続をテストします。**

次の手順を実行して、AEM Assets as a [!DNL Cloud Service] インスタンスと Brand Portal テナントの接続を検証します。

1. AEM Assets にログインします。

1. **ツール**&#x200B;パネルで、**[!UICONTROL 導入]**／**[!UICONTROL 配布版]**&#x200B;に移動します。

   ![](assets/test-bpconfig1.png)

   Brand Portal 配布エージェント（**[!UICONTROL bpdistributionagent0]**）は、「**[!UICONTROL Brand Portal に公開]**」の下に作成されます。

   ![](assets/test-bpconfig2.png)


1. 「**[!UICONTROL Brand Portal に公開]**」をクリックして、配布エージェントを開きます。

   「**[!UICONTROL ステータス]**」タブに配布キューが表示されます。

   配布エージェントには、次の 2 つのキューが含まれます。
   * **processing-queue**：Brand Portal へのアセット配布用。

   * **error-queue**：配布が失敗したアセット用。
   >[!NOTE]
   >
   >エラーを確認し、**error-queue** を定期的に消去することをお勧めします。

   ![](assets/test-bpconfig3.png)

1. AEM Assets as a [!DNL Cloud Service] と Brand Portal の間の接続を確認するには、「**[!UICONTROL 接続をテスト]**」アイコンをクリックします。

   ![](assets/test-bpconfig4.png)

   *テストパッケージが正常に配信された*&#x200B;ことを示すメッセージが表示されます。

   >[!NOTE]
   >
   >配布エージェントを無効にしないでください。無効にすると、（実行中のキュー内の）アセットの配布が失敗する可能性があります。

AEM Assets as a [!DNL Cloud Service] インスタンスと Brand Portal テナントの間の接続を検証するには、AEM Assets から Brand Portal にアセットを公開します。接続に成功すると、公開されたアセットが Brand Portal インターフェイスに表示されます。


次の操作が可能になっています。

* [AEM Assets から Brand Portal へのアセットの公開](publish-to-brand-portal.md)
* [AEM Assets から Brand Portal へのフォルダーの公開](publish-to-brand-portal.md#publish-folders-to-brand-portal)
* [AEM Assets から Brand Portal へのコレクションの公開](publish-to-brand-portal.md#publish-collections-to-brand-portal)
* [Brand Portal から AEM Assets への公開](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/asset-sourcing-in-brand-portal/brand-portal-asset-sourcing.html?lang=ja) - Brand Portal でのアセットのソーシング
* [Brand Portal へのプリセット、スキーマ、ファセットの公開](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/publish/publish-schema-search-facets-presets.html?lang=ja)
* [Brand Portal へのタグの公開](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/publish/brand-portal-publish-tags.html?lang=ja)

詳しくは、[Brand Portal ドキュメント](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/home.html?lang=ja)を参照してください。

**配布ログ**

配布エージェントのログで、アセット発行ワークフローを監視できます。

次に、AEM Assets から Brand Portal にアセットを公開し、ログを確認します。

1. 「**設定のテスト**」節で示した手順（1 ～ 4）に従い、配布エージェントページに移動します。
1. 「**[!UICONTROL ログ]** 」をクリックして、処理ログとエラーログを表示します。

   ![](assets/test-bpconfig5.png)

配布エージェントは次のログを生成します。

* 情報：これは、配布エージェントの構成が正常に完了したときにトリガーされるシステムが生成するログです。
* DSTRQ1（リクエスト 1）：テスト接続時にトリガーされます。

アセットの公開時に、次の要求および応答ログが生成されます。

**配布エージェントの要求**：

* DSTRQ2（リクエスト 2）：アセットの公開リクエストがトリガーされます。
* DSTRQ3（リクエスト 3）：アセットが存在する AEM Assets フォルダーの公開と、Brand Portal でのフォルダーの複製を行う別の要求がトリガーされます。

**配布エージェントの応答**：

* queue-bpdistributionagent0（DSTRQ2）：アセットが Brand Portal に公開されます。
* queue-bpdistributionagent0（DSTRQ3）：システムは、Brand Portal 内のアセットを含む AEM Assets フォルダーを複製します。

上記の例では、追加の要求と応答がトリガーされます。アセットが初めて発行されたので、Brand Portal で親フォルダー（追加パス）が見つからなかったため、アセットが発行された Brand Portal で同じ名前の親フォルダーを作成する追加の要求をトリガーします。

>[!NOTE]
>
>親フォルダーが Brand Portal に存在しない場合や AEM Assets で変更された場合には、追加のリクエストが生成されます。

自動処理ワークフローを使用して AEM Assets as a [!DNL Cloud Service] で Brand Portal のライセンス認証を行う方法以外に、Adobe 開発者コンソールを使用して、AEM Assets as a [!DNL Cloud Service] と Brand Portal の連携を手動設定する方法もありますが、この方法は推奨されません。

>[!NOTE]
>
>Brand Portalテナントのアクティベート中に問題が発生した場合は、カスタマーサポートにお問い合わせください。

## Adobe 開発者コンソールを使用した手動設定 {#manual-configuration}

次の節では、Adobe 開発者コンソールを使用して、AEM Assets as a [!DNL Cloud Service]と Brand Portal の連携を手動で設定する方法について説明します。

AEM Assets as a [!DNL Cloud Service] と Brand Portal の連携は、Adobe 開発者コンソールを通じて設定されます。このコンソールでは、Brand Portal テナントの認証に使用する Adobe Identity Management サービス（IMS）アカウントトークンを調達します。この機能を使用するには、AEM Assets および Adobe 開発者コンソールの両方の設定が必要です。

1. AEM Assets で、IMS アカウントを作成して公開鍵（証明書）を生成します。
1. Adobe 開発者コンソールで、Brand Portal テナント（組織）用のプロジェクトを作成します。
1. そのプロジェクトで、公開鍵で API を設定して、サービスアカウント接続を作成します。
1. サービスアカウント資格情報と JSON Web トーケン（JWT）ペイロード情報を取得します。
1. AEM Assets で、サービスアカウント資格情報と JWT ペイロードを使用して IMS アカウントを設定します。
1. AEM Assets で、IMS アカウントと Brand Portal エンドポイント（組織 URL）を使用して Brand Portal Cloud Service を設定します。
1. AEM Assets から Brand Portal にアセットを公開して、設定をテストします。

>[!NOTE]
>
>AEM Assets as a [!DNL Cloud Service] インスタンスには、1 つの Brand Portal テナントとの連携のみ設定する必要があります。

**前提条件**

AEM Assets と Brand Portal の連携を設定するには以下が必要です。

* 実行中の AEM Assets as a [!DNL Cloud Service] インスタンス
* Brand Portal テナント URL
* Brand Portal テナントの IMS 組織に対するシステム管理者権限を持つユーザー

## 設定の作成 {#create-new-configuration}

指定した順序で次の手順を実行して、AEM Assets と Brand Portal の連携を設定します。

1. [公開証明書の取得](#public-certificate)
1. [サービスアカウント（JWT）接続の作成](#createnewintegration)
1. [IMS アカウントの設定](#create-ims-account-configuration)
1. [Cloud Service の設定](#configure-the-cloud-service)

### IMS 設定の作成 {#create-ims-configuration}

IMS 設定では、AEM Assets as a [!DNL Cloud Service] インスタンスと Brand Portal テナントの連携を認証します。

IMS 設定には、次の 2 つの手順が含まれます。

* [公開証明書の取得](#public-certificate)
* [IMS アカウントの設定](#create-ims-account-configuration)

### 公開証明書の取得 {#public-certificate}

公開鍵（証明書）は、Adobe 開発者コンソールでプロファイルを認証します。

1. AEM Assets にログインします。
1. **ツール**&#x200B;パネルで、**[!UICONTROL セキュリティ]**／**[!UICONTROL Adobe IMS 設定]**&#x200B;に移動します。
1. Adobe IMS 設定ページで、「**[!UICONTROL 作成]**」をクリックします。**[!UICONTROL Adobe IMS 技術アカウント設定]**&#x200B;ページにリダイレクトされます。デフォルトでは、「**証明書**」タブが開きます。
1. 「**[!UICONTROL クラウドソリューション]**」ドロップダウンリストで「**[!UICONTROL Adobe Brand Portal]**」を選択します。
1. 「**[!UICONTROL 新しい証明書を作成]**」チェックボックスをオンにして、公開鍵の&#x200B;**エイリアス**&#x200B;を指定します。ここで入力したエイリアスが、公開鍵になります。
1. 「**[!UICONTROL 証明書を作成]**」をクリックします。「**[!UICONTROL OK]**」をクリックして公開証明書を生成します。

   ![証明書を作成](assets/ims-config2.png)

1. **[!UICONTROL 公開鍵をダウンロード]**&#x200B;アイコンをクリックして、公開鍵（CRT）ファイルをローカルマシンに保存します。

   この公開鍵を後で使用して、Brand Portal テナントの API を設定し、Adobe 開発者コンソールでサービスアカウント資格情報を生成が次の値である。

   ![証明書をダウンロード](assets/ims-config3.png)

1. 「**[!UICONTROL 次へ]**」をクリックします。

   「**アカウント**」タブで、Adobe IMS アカウントが作成されます。このアカウントには、Adobe 開発者コンソールで生成されるサービスアカウント資格情報が必要です。このページは開いたままにしておきます。

   新しいタブを開き、[Adobe 開発者コンソールでサービスアカウント（JWT）接続を作成](#createnewintegration)して、IMS アカウントを設定するための資格情報と JWT ペイロードを取得します。

### サービスアカウント（JWT）接続の作成 {#createnewintegration}

Adobe 開発者コンソールで、プロジェクトと API を Brand Portal テナント（組織）レベルで設定します。API を設定すると、サービスアカウント（JWT）接続が作成されます。API を設定するには、キーペア（秘密鍵と公開鍵）を生成する方法と、公開鍵をアップロードする方法の 2 とおりがあります。AEM Assets と Brand Portal の統合を設定するには、AEM Assets で公開鍵（証明書）を生成し、その公開鍵をアップロードして Adobe 開発者コンソールで資格情報を作成する必要があります。これらの資格情報は、AEM Assets で IMS アカウントを設定するために必要です。IMS アカウントを設定したら、AEM Assets に Brand Portal Cloud Service を設定できます。

サービスアカウント資格情報と JWT ペイロードを生成するには、次の手順を実行します。

1. IMS 組織（Brand Portal テナント）のシステム管理者権限で Adobe 開発者コンソールにログインします。デフォルトの URL は [https://www.adobe.com/go/devs_console_ui](https://www.adobe.com/go/devs_console_ui) です。


   >[!NOTE]
   >
   >右上隅にあるドロップダウン（組織）リストから正しい IMS 組織（Brand Portal テナント）が選択されていることを確認します。

1. 「**[!UICONTROL 新規プロジェクトを作成]**」をクリックします。システムで生成された名前を持つ空のプロジェクトが組織に対して作成されます。

   「**[!UICONTROL プロジェクトを編集]**」をクリックして、「**[!UICONTROL プロジェクトタイトル]**」と「**[!UICONTROL 説明]**」をアップデートし、「**[!UICONTROL 保存]**」をクリックします。

1. 「**[!UICONTROL プロジェクトの概要]**」タブで、「**[!UICONTROL API を追加]**」をクリックします。

1. **[!UICONTROL API を追加]**&#x200B;ウィンドウで、「**[!UICONTROL AEM Brand Portal]**」を選択し、「**[!UICONTROL 次へ]**」をクリックします。

   AEM Brand Portal サービスにアクセスできることを確認します。

1. **[!UICONTROL API を設定]**&#x200B;ウィンドウで、「**[!UICONTROL 公開鍵をアップロード]**」をクリックします。次に、「**[!UICONTROL ファイルを選択]**」をクリックし、[公開証明書の取得](#public-certificate)のセクションでダウンロードした公開鍵（.crt ファイル）をアップロードします。

   「**[!UICONTROL 次へ]**」をクリックします。

   ![「公開鍵をアップロード」](assets/service-account3.png)

1. 公開鍵を確認し、「**[!UICONTROL 次へ]**」をクリックします。

1. デフォルトの製品プロファイルとして「**[!UICONTROL Assets Brand Portal]**」を選択し、「**[!UICONTROL 設定済み API を保存]**」をクリックします。

   <!-- 
   In Brand Portal, a default profile is created for each organization. The Product Profiles are created in admin console for assigning users to groups (based on the roles and permissions). For configuration with Brand Portal, the OAuth token is created at organization level. Therefore, you must configure the default Product Profile for your organization. 
   -->

   ![製品プロファイルを選択](assets/service-account4.png)

1. API が設定されると、API の概要ページにリダイレクトされます。左側のナビゲーションツリーで「**[!UICONTROL 資格情報]**」の下の「**[!UICONTROL サービスアカウント（JWT）]**」オプションをクリックします。

   >[!NOTE]
   >
   >資格情報を確認し、必要に応じて、JWT トークンの生成、資格情報の詳細のコピー、クライアントの秘密鍵の取得などのアクションを実行できます。

1. 「**[!UICONTROL クライアント資格情報]**」タブから、**[!UICONTROL クライアント ID]** をコピーします。

   「**[!UICONTROL クライアント秘密鍵を取得]**」をクリックし、**[!UICONTROL クライアントの秘密鍵]**&#x200B;をコピーします。

   ![サービスアカウント資格情報](assets/service-account5.png)

1. 「**[!UICONTROL JWT を生成]**」タブに移動し、**[!UICONTROL JWT ペイロード]**&#x200B;情報をコピーします。

これで、クライアント ID（API キー）、クライアントの秘密鍵、JWT ペイロードを使用して、AEM Assets に [IMS アカウントを設定](#create-ims-account-configuration)できるようになりました。

<!--
1. Click **[!UICONTROL Create Integration]**.

1. Select **[!UICONTROL Access an API]**, and click **[!UICONTROL Continue]**.

   ![Create New Integration](assets/create-new-integration1.png)

1. Create a new integration page opens. 
   
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

   The API Key, Client Secret key, and JWT payload information will be used to create IMS account configuration.

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

   ![](assets/create-new-integration5.png)

>[!CAUTION]
>
>IMS 設定は 1 つだけにする必要があります。
>
>IMS 設定がヘルスチェックに合格していることを確認します。設定がヘルスチェックに合格しない場合は無効です。削除して、新しい有効な設定を作成する必要があります。

### Cloud Service の設定 {#configure-the-cloud-service}

Brand Portal Cloud Service を設定するには、次の手順を実行します。

1. AEM Assets にログインします。

1. **ツール**&#x200B;パネルで、**[!UICONTROL クラウドサービス]**／**[!UICONTROL AEM Brand Portal]** に移動します。

1. Brand Portal の設定ページで、「**[!UICONTROL 作成]**」をクリックします。

1. 設定の&#x200B;**[!UICONTROL タイトル]**&#x200B;を入力します。

   [IMS アカウントの設定](#create-ims-account-configuration)時に作成した IMS 設定を選択します。

   「**[!UICONTROL サービス URL]**」に、Brand Portal テナント（組織）URL を入力します。

   ![](assets/create-cloud-service.png)

1. 「**[!UICONTROL 保存して閉じる]**」をクリックします。クラウド設定が作成されます。

   これで、AEM Assets as a [!DNL Cloud Service] インスタンスと Brand Portal テナントの連携が設定されました。

これで、配布エージェントを確認し、Brand Portal にアセットを公開することで、設定をテストできます。

<!--
### Test configuration {#test-configuration}

Perform the following steps to validate the configuration:

1. Log in to AEM Assets.

1. From the **Tools** panel, navigate to **[!UICONTROL Deployment]** > **[!UICONTROL Distribution]**.

    ![](assets/test-bpconfig1.png)

   A Brand Portal distribution agent (**[!UICONTROL bpdistributionagent0]**) is created under **[!UICONTROL Publish to Brand Portal]**.

   ![](assets/test-bpconfig2.png)


1. Click **[!UICONTROL Publish to Brand Portal]** to open the distribution agent. 

   You can see the distribution queues under the **[!UICONTROL Status]** tab. 
   
   A distribution agent contains two queues: 
   * **processing-queue**: for the distribution of assets to Brand Portal. 

   * **error-queue**: for the assets where distribution has failed. 
   
   >[!NOTE]
   >
   >It is recommended to review the failures and  clear the **error-queue** periodically.  

   ![](assets/test-bpconfig3.png)

1. To verify the connection between AEM Assets as a [!DNL Cloud Service] and Brand Portal, click on the **[!UICONTROL Test Connection]** icon.

   ![](assets/test-bpconfig4.png)

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

   ![](assets/test-bpconfig5.png)

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
