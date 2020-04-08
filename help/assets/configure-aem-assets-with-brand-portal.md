---
title: Brand PortalでのAEM Assetsクラウドサービスの設定
description: Brand PortalでAEM Assetsクラウドサービスを設定します。
contentOwner: Vishabh Gupta
translation-type: tm+mt
source-git-commit: 8dc3270b355e9e855179f6b41602a3c28202a5b7

---


# AEM Assets と Brand Portal の連携の設定 {#configure-aem-assets-with-brand-portal}

Adobe Experience Manager（AEM）Assets と Brand Portal の連携が、Adobe I/O を通じて設定されます。Adobe I/O は Brand Portal テナントの認証用の IMS トークンを取得します。

## 前提条件 {#prerequisites}

AEM Assets と Brand Portal の連携を設定するには以下が必要です。

* AEM Assetsクラウドインスタンスの起動および実行。
* Brand Portal テナント URL
* Brand Portal テナントの IMS 組織に対するシステム管理者権限を持つユーザー

**詳細なクエリは** 、Supportにお問い合わせください。

##  設定の作成{#create-new-configuration}

Adobe I/Oで新しい設定を作成し、AEM AssetsクラウドインスタンスをBrand Portalで設定できます。

リストに表示されたシーケンスで次の手順を実行します。
1. [公開証明書の取得](#public-certificate)
1. [Adobe I/O 統合環境を作成する](#createnewintegration)
1. [IMSアカウント設定の作成](#create-ims-account-configuration)
1. [クラウドサービスの設定](#configure-the-cloud-service)
1. [テスト設定](#test-configuration)

### IMS設定の作成 {#create-ims-configuration}

IMS設定は、AEM Assetsオーサーインスタンスを使用してBrand Portalテナントを認証します。

IMS設定には、次の2つの手順が含まれます。

* [公開証明書の取得](#public-certificate)
* [IMSアカウント設定の作成](#create-ims-account-configuration)

### 公開証明書の取得 {#public-certificate}

公開証明書を使用すると、Adobe I/Oでプロファイルを認証できます。

1. AEM Assetsクラウドインスタンスにログインします。

1. ツー **ル** / ![Security](assets/tools.png) / **[!UICONTROL Adobe]** IMS Configurationsに移動し ****&#x200B;ます。

   ![Adobe IMSアカウント設定UI](assets/ims-configuration1.png)

1. Adobe IMS設定ページが開きます。

   「**[!UICONTROL 作成]**」をクリックします。

   これにより、 **[!UICONTROL Adobe IMS Technical Account Configurationページが表示されます]** 。

1. デフォルトでは、「証 **明書** 」タブが開きます。

   「 **Cloud Solution**」で「 **[!UICONTROL Adobe Brand Portal」を選択します]**。

1. 「新しい証明書を作成 **[!UICONTROL し、証明書のエイリアスを指定]** 」チェックボ **ックスを** オンにします。 ここで入力したエイリアスが、ダイアログ名として表示されます。 

1. 「**[!UICONTROL 証明書を作成]**」をクリックします。ダイアログが表示されます。「 **[!UICONTROL OK]** 」をクリックして公開証明書を生成します。

   ![証明書の作成](assets/ims-config2.png)

1. Click **[!UICONTROL Download Public Key]** and save the *AEM-Adobe-IMS.crt* certificate file on your machine. The certificate file is used to [create Adobe I/O integration](#createnewintegration).

   ![証明書のダウンロード](assets/ims-config3.png)

1. 「**[!UICONTROL 次へ]**」をクリックします。

   「アカウ **ント** 」タブで、Adobe IMSアカウントを作成しますが、統合の詳細が必要です。 このページは開いたままにしておきます。

   新しいタブを開き、Adobe I/O [統合を作成して](#createnewintegration) 、IMSアカウント設定の統合の詳細を取得します。

### Adobe I/O 統合環境を作成する{#createnewintegration}

Adobe I/O統合により、IMSアカウント設定の設定で必要なAPIキー、クライアントシークレット、ペイロード(JWT)が生成されます。

1. Brand PortalテナントのIMS組織のシステム管理者権限でAdobe I/O Consoleにログインします。

   デフォルトURL:https://console.adobe.io/ [](https://console.adobe.io/)

1. Click **[!UICONTROL Create Integration]**.

1. 「 **[!UICONTROL Access an API]**」を選択し、「 **[!UICONTROL Continue」をクリックします]**。

   ![新しい統合の作成](assets/create-new-integration1.png)

1. 新しい統合ページを作成します。

   ドロップダウンオプションから組織をリストします。

   **[!UICONTROL Experience Cloud]**、 **[!UICONTROL AEM Brand Portalを選択し、「続行]** 」をクリッ **[!UICONTROL クします]**。

   If the Brand Portal option is disabled for you, ensure that you have selected correct organization from the drop-down box above the **[!UICONTROL Adobe Services]** option. 自分がどの組織に属しているかわからない場合は、管理者に問い合わせてください。

   ![統合の作成](assets/create-new-integration2.png)

1. 統合の名前と説明を指定します。 Click **[!UICONTROL Select a File from your computer]** and upload the `AEM-Adobe-IMS.crt` file downloaded in the [obtain public certificates](#public-certificate) section.

1. 組織のプロファイルを選択します。

   または、デフォルトのプロファイル **[!UICONTROL Assets Brand Portalを選択し]** 、「統合を作成」を **[!UICONTROL クリックします]**。 統合環境が作成されます。

1. Click **[!UICONTROL Continue to integration details]** to view the integration information.

   **[!UICONTROL APIキーのコピー]**

   「 **[!UICONTROL Retrieve Client Secret]** 」をクリックし、Client Secretキーをコピーします。

   ![統合環境の API キー、クライアント秘密鍵、ペイロード情報の表示画面](assets/create-new-integration3.png)

1. 「 **[!UICONTROL JWT]** 」タブに移動し、 **[!UICONTROL JWTペイロードをコピーします]**。

   APIキー、クライアント秘密キー、JWTペイロード情報は、IMSアカウント設定の作成に使用されます。

### IMSアカウント設定の作成 {#create-ims-account-configuration}

次の手順を実行したことを確認します。

* [公開証明書の取得](#public-certificate)
* [Adobe I/O 統合環境を作成する](#createnewintegration)

**IMSアカウント設定を作成する手順：**

1. IMS設定ページの「アカウント」タ **[!UICONTROL ブを開きます]** 。 （このページは、「[公開証明書を取得する](#public-certificate)」セクションの最後で開いたままにしておいたページです）。

1. IMSアカウント **[!UICONTROL のタイトル]** を指定します。

   「認 **[!UICONTROL 証サーバー]**」にURLを入力します。https://ims-na1.adobelogin.com/ [](https://ims-na1.adobelogin.com/)

   「Adobe I/O統合の作成」の最後にコピーしたAPIキー、Client Secret、JWTペイロ [ードを貼り付けます](#createnewintegration)。

   「**[!UICONTROL 作成]**」をクリックします。

   統合が作成されます。

   ![IMSアカウントの設定](assets/create-new-integration6.png)


1. Select the IMS configuration and click **[!UICONTROL Check Health]**. ダイアログボックスが表示されます。

   [チェック **をクリック]**。 接続が成功すると、*トークンが正常に取得された*&#x200B;ことを示すメッセージが表示されます。

   ![](assets/create-new-integration5.png)

>[!CAUTION]
>
>有効なIMS設定を1つだけ作成します。 複数のIMS設定を作成しないでください。
>
> 構成が正常であることを確認します。 構成が正常でない場合は、構成を削除し、新しい正常な構成を作成します。


### Configure cloud service {#configure-the-cloud-service}

次の手順を実行して、Brand Portalクラウドサービスの設定を作成します。

1. AEM Assetsクラウドインスタンスにログインします。

1. ツール **ツー** ル ![](assets/tools.png) ・パネルで、 **[!UICONTROL Cloud Services/AEM Brand Portalに移動します]**。

   ブランドポータル設定ページが開きます。

1. 「**[!UICONTROL 作成]**」をクリックします。

1. Specify a **[!UICONTROL Title]** for the configuration.

   手順で作成したIMS設定を選択し、IMSアカウント設 [定を作成します](#create-ims-account-configuration)。

   「サー **[!UICONTROL ビスURL]**」に、ブランドポータルテナントURLを入力します。

   ![](assets/create-cloud-service.png)

1. Click **[!UICONTROL Save and Close]**. クラウド設定が作成されます。 AEM AssetsクラウドインスタンスがBrand Portalテナントで設定されました。

### Test configuration {#test-configuration}

1. AEM Assetsクラウドインスタンスにログインします。

1. **Deployment** Tools ![(配布ツール](assets/tools.png) )/ **** Distribution Tools(配布ツール **[!UICONTROL )に移]**&#x200B;動します。

   ![](assets/test-bpconfig1.png)

1. 配布ページが開きます。

   ブランドポータル配布エージェントは、「ブ `bpdistributionagent0` ランドポータルに **[!UICONTROL 公開」の下に作成されま]**&#x200B;す。

   Click **[!UICONTROL Publish to Brand Portal]**.

   ![](assets/test-bpconfig2.png)

   >[!NOTE]
   >
   >デフォルトでは、Brand Portalテナント用に1つの配布エージェントが作成されます。

1. 配布エージェントページが開きます。 デフォルトでは、「 **[!UICONTROL Status]** 」タブが開き、配布キューが設定されます。

   配布エージェントには、次の2つのキューが含まれます。
   * Brand Portalにアセットを配布するための処理キュー。
   * 配布が失敗したアセットのエラーキュー。
   個々のキューまたは設定全体をテストできます。

   ![](assets/test-bpconfig3.png)

1. AEM AssetsとBrand Portalの間の接続を確認するには、「接続をテスト」をク **[!UICONTROL リックします]**。

   ![](assets/test-bpconfig4.png)

   テストパッケージが正常に配信されたことを示すメッセージがページの下部に表示されます。

   >[!NOTE]
   >
   >配布エージェントを無効にしないでください。無効にすると、（実行中のキュー内の）アセットの配布が失敗する可能性があります。

Brand Portalは、AEM Assetsクラウドインスタンスで正常に設定されました。 次の操作が可能になりました。

* [AEM AssetsからBrand Portalへのアセットの公開](publish-to-brand-portal.md)
* [AEM AssetsからBrand Portalへのフォルダーの公開](publish-to-brand-portal.md#publish-folders-to-brand-portal)
* [AEM Assetsからブランドポータルにコレクションを公開する](publish-to-brand-portal.md#publish-collections-to-brand-portal)


## 配布ログ {#distribution-logs}

配布エージェントで実行されたアクションの詳細については、ログを確認できます。

例えば、AEM AssetsからBrand Portalにアセットを発行し、設定を確認したとします。

1. 「接続のテスト」に示す手順（手順1 ～ 4）に従 **[!UICONTROL い]** 、配布エージェントページに移動します。

1. 配布キュー **[!UICONTROL queue-bpdistributionagent0を選択し、]** 「 **[!UICONTROL Logs]** 」をクリックして配布ログを表示します。

   ![](assets/test-bpconfig5.png)

配布エージェントは次のログを生成します。

* 情報：これは、構成が正常に完了した場合にトリガーされるシステム生成ログで、配布エージェントを有効にします。
* DSTRQ1 （リクエスト1）:テスト接続時にトリガーされました。

アセットの公開時に、次の要求および応答ログが生成されます。

**配布エージェントの要求**:
* DSTRQ2 （リクエスト2）:アセットの発行要求がトリガーされます。
* DSTRQ3 （リクエスト3）:アセットが存在するフォルダーの公開と、Brand Portalでのフォルダーの複製を行う別の要求がトリガーされます。

**配布エージェントの応答**:
* queue-bpdistributionagent0 (DSTRQ2):アセットがBrand Portalに公開されます。
* queue-bpdistributionagent0 (DSTRQ3):システムは、Brand Portal内のアセットを含むフォルダーを複製します。

上記の例では、追加のリクエストと応答がトリガーされます。 アセットが初めて発行されたので、Brand Portalで親フォルダ(追加「パス」)が見つかりませんでした。そのため、アセットが発行されたBrand Portalで同じ名前の親フォルダを作成する追加の要求をトリガーします。

同じ名前の親フォルダーが存在する場合(パ追加ス)がBrand Portalで表示され、追加のリクエストはトリガーされません。

>[!NOTE]
>
>エラーログを表示するには、配布キュー **[!UICONTROL error-queue-bpdistributionagent0を選択し]** 、「 **[!UICONTROL Logs]**」をクリックします。


## 追加情報 {#additional-information}

に移動して、配 `/system/console/slingmetrics` 布されたコンテンツに関する統計を確認します。

1. **カウンター指標**
   * sling: `mac_sync_request_failure`
   * sling: `mac_sync_request_received`
   * sling: `mac_sync_request_success`

1. **時間指標**
   * sling: `mac_sync_distribution_duration`
   * sling: `mac_sync_enqueue_package_duration`
   * sling: `mac_sync_setup_request_duration`


<!--
   Comment Type: draft

   <li> </li>
   -->

<!--
   Comment Type: draft

   <li>Step text</li>
   -->
