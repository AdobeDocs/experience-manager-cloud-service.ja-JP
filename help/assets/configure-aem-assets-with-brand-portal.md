---
title: AEM Assets Cloud Service と Brand Portal の統合の設定
description: Brand Portal で AEM Assets Cloud Service を設定します。
contentOwner: Vishabh Gupta
translation-type: tm+mt
source-git-commit: 00e37e9493bc3dde8a4d83c562a889a67587ada0
workflow-type: tm+mt
source-wordcount: '1336'
ht-degree: 99%

---


# AEM Assets と Brand Portal の連携の設定 {#configure-aem-assets-with-brand-portal}

Adobe Experience Manager（AEM）Assets と Brand Portal の連携が、Adobe I/O を通じて設定されます。Adobe I/O は Brand Portal テナントの認証用の IMS トークンを取得します。

## 前提条件 {#prerequisites}

AEM Assets と Brand Portal の連携を設定するには以下が必要です。

* AEM Assets クラウドインスタンスの起動および実行
* Brand Portal テナント URL
* Brand Portal テナントの IMS 組織に対するシステム管理者権限を持つユーザー

**詳しいクエリについては、カスタマーケアにお問い合わせ** ください。

## 設定の作成 {#create-new-configuration}

Adobe I/O で設定を作成し、AEM Assets クラウドインスタンスを Brand Portal で設定できます。

リストに表示されたシーケンスで次の手順を実行します。
1. [公開証明書の取得](#public-certificate)
1. [Adobe I/O 統合環境の作成](#createnewintegration)
1. [IMS アカウント設定の作成](#create-ims-account-configuration)
1. [Cloud Service の設定](#configure-the-cloud-service)
1. [設定のテスト](#test-configuration)

### IMS 設定の作成 {#create-ims-configuration}

IMS 設定は、AEM Assets オーサーインスタンスを使用して Brand Portal テナントを認証します。

IMS 設定には、次の 2 つの手順が含まれます。

* [公開証明書の取得](#public-certificate)
* [IMS アカウント設定の作成](#create-ims-account-configuration)

### 公開証明書の取得 {#public-certificate}

公開証明書により、Adobe I/O でプロファイルを認証できます。

1. AEM Assets クラウドインスタンスにログインします。

1. **ツール**![ツール](assets/tools.png)パネルより、**[!UICONTROL セキュリティ]**／**[!UICONTROL Adobe IMS 設定]**&#x200B;に移動します。

   ![Adobe IMS アカウント設定 UI](assets/ims-configuration1.png)

1. Adobe IMS 設定ページが開きます。

   「**[!UICONTROL 作成]**」をクリックします。

   **[!UICONTROL Adobe IMS 技術アカウント設定]**&#x200B;ページが表示されます。

1. デフォルトでは、「**証明書**」タブが開きます。

   **クラウドソリューション**&#x200B;で「**[!UICONTROL Adobe Brand Portal]**」を選択します。

1. 「**[!UICONTROL 新しい証明書を作成]**」チェックボックスをチェックし、証明書の&#x200B;**エイリアス**&#x200B;を指定します。ここで入力したエイリアスが、ダイアログ名として表示されます。

1. 「**[!UICONTROL 証明書を作成]**」をクリックします。ダイアログが表示されます。「**[!UICONTROL OK]**」をクリックして公開証明書を生成します。

   ![証明書を作成](assets/ims-config2.png)

1. 「**[!UICONTROL 公開鍵をダウンロード]**」をクリックし、*AEM-Adobe-IMS.crt* 証明書ファイルをローカルマシンに保存します。この証明書ファイルは、[Adobe I/O 統合環境の作成](#createnewintegration)に使用されます。

   ![証明書をダウンロード](assets/ims-config3.png)

1. 「**[!UICONTROL 次へ]**」をクリックします。

   「**アカウント**」タブで、Adobe IMS アカウントを作成するには、統合環境の詳細が必要です。このページは開いたままにしておきます。

   新しいタブを開き、[Adobe I/O 統合環境を作成](#createnewintegration)して、IMS アカウント設定の統合環境の詳細を取得します。

### Adobe I/O 統合環境の作成{#createnewintegration}

Adobe I/O 統合環境により、API キー、クライアント秘密鍵、および IMS アカウント設定の設定で必要なペイロード（JWT）が生成されます。

1. Brand Portal テナントの IMS 組織のシステム管理者権限で Adobe I/O コンソールにログインします。

   デフォルト URL：[https://console.adobe.io/](https://console.adobe.io/)

1. 「**[!UICONTROL 統合を作成]**」をクリックします。

1. 「**[!UICONTROL API にアクセス]**」を選択し、「**[!UICONTROL 続行]**」をクリックします。

   ![新しい統合の作成](assets/create-new-integration1.png)

1. 新しい統合を作成ページを開きます。

   ドロップダウンリストからご自身の組織を選択します。

   **[!UICONTROL Experience Cloud]** で「**[!UICONTROL AEM Brand Portal]**」を選択し、「**[!UICONTROL 続行]**」をクリックします。

   「Brand Portal」オプションが無効になっている場合は、「**[!UICONTROL アドビのサービス]**」オプションの上にあるドロップダウンボックスで正しい組織が選択されているかどうかを確認してください。自分がどの組織に属しているかわからない場合は、管理者に問い合わせてください。

   ![統合の作成](assets/create-new-integration2.png)

1. 新しい統合環境の名前と説明を入力します。「**[!UICONTROL お使いのコンピューターからファイルを選択]**」をクリックし、「[公開証明書を取得する](#public-certificate)」セクションでダウンロードした `AEM-Adobe-IMS.crt` ファイルをアップロードします。

1. 組織のプロファイルを選択します。

   または、デフォルトのプロファイル **[!UICONTROL Assets Brand Portal]** を選択し、「**[!UICONTROL 統合を作成]**」をクリックします。統合環境が作成されます。

1. 「**[!UICONTROL 統合の詳細情報に進む]**」をクリックして、統合環境の詳細情報を表示します。

   **[!UICONTROL API キーのコピー]**

   「**[!UICONTROL クライアント秘密鍵を取得]**」をクリックし、クライアント秘密鍵をコピーします。

   ![統合環境の API キー、クライアント秘密鍵、ペイロード情報の表示画面](assets/create-new-integration3.png)

1. 「**[!UICONTROL JWT]**」タブに移動し、**[!UICONTROL JWT ペイロード]**&#x200B;をコピーします。

   API キー、クライアント秘密鍵、JWT ペイロード情報は、IMS アカウント設定の作成に使用されます。

### IMS アカウント設定の作成 {#create-ims-account-configuration}

次の手順を実行したことを確認します。

* [公開証明書の取得](#public-certificate)
* [Adobe I/O 統合環境の作成](#createnewintegration)

**IMS アカウント設定の作成手順：**

1. IMS 設定ページの「**[!UICONTROL アカウント]**」タブを開きます。（このページは、「[公開証明書を取得する](#public-certificate)」セクションの最後で開いたままにしておいたページです）。

1. IMS アカウントの&#x200B;**[!UICONTROL タイトル]**&#x200B;を指定します。

   「**[!UICONTROL 認証サーバー]**」に次の URL を入力します。[https://ims-na1.adobelogin.com/](https://ims-na1.adobelogin.com/)

   [Adobe I/O 統合環境の作成](#createnewintegration)の最後にコピーした API キー、クライアント秘密鍵、JWT ペイロードを貼り付けます。

   「**[!UICONTROL 作成]**」をクリックします。

   統合環境が作成されます。

   ![IMS アカウントの設定](assets/create-new-integration6.png)


1. 作成した IMS 設定を選択して「**[!UICONTROL ヘルスチェック]**」をクリックします。ダイアログボックスが表示されます。

   「**[!UICONTROL チェック]**」をクリック。接続が成功すると、*トークンが正常に取得された*&#x200B;ことを示すメッセージが表示されます。

   ![](assets/create-new-integration5.png)

>[!CAUTION]
>
>IMS 設定は 1 つだけにする必要があります。複数の IMS 設定を作成しないでください。
>
>IMS 設定がヘルスチェックに合格していることを確認します。設定がヘルスチェックに合格しない場合は無効です。削除して、新しい有効な設定を作成する必要があります。



### Cloud Service の設定{#configure-the-cloud-service}

Brand Portal クラウドサービス設定を作成するには、以下の手順を実行します。

1. AEM Assets クラウドインスタンスにログインします。

1. **ツール**![ツール](assets/tools.png)パネルで、**[!UICONTROL Cloud Services]**／**[!UICONTROL AEM Brand Portal]** に移動します。

   Brand Portal 設定ページが開きます。

1. 「**[!UICONTROL 作成]**」をクリックします。

1. 設定の&#x200B;**[!UICONTROL タイトル]**&#x200B;を入力します。

   [IMS アカウント設定の作成](#create-ims-account-configuration)手順で作成した IMS 設定を選択します。

   「**[!UICONTROL サービス URL]**」に、Brand Portal テナント URL を入力します。

   ![](assets/create-cloud-service.png)

1. 「**[!UICONTROL 保存して閉じる]**」をクリックします。クラウド設定が作成されます。AEM Assets クラウドインスタンスが Brand Portal テナントで設定されました。

### 設定のテスト{#test-configuration}

1. AEM Assets クラウドインスタンスにログインします。

1. **ツール**![ツール](assets/tools.png)パネルで、**[!UICONTROL デプロイメント]**／**[!UICONTROL 配布]**&#x200B;に移動します。

   ![](assets/test-bpconfig1.png)

1. 配布ページが表示されます。

   Brand Portal 配布エージェント `bpdistributionagent0` は、「**[!UICONTROL Brand Portal に公開]**」の下に作成されます。

   「**[!UICONTROL Brand Portal に公開]**」をクリックします。

   ![](assets/test-bpconfig2.png)

   >[!NOTE]
   >
   >デフォルトでは、Brand Portal テナント用に 1 つの配布エージェントが作成されます。

1. 配布エージェントページが開きます。デフォルトでは、「**[!UICONTROL ステータス]**」タブが開き、配布キューが設定されます。

   配布エージェントには、次の 2 つのキューが含まれます。
   * **processing-queue**：Brand Portal へのアセット配布用。

   * **error-queue**：配布が失敗したアセット用。
   >[!NOTE]
   >
   >エラーを確認し、**error-queue** を定期的に消去することをお勧めします。

   ![](assets/test-bpconfig3.png)

1. AEM Assets と Brand Portal の間の接続を検証するには、「**[!UICONTROL 接続をテスト]**」をクリックします。

   ![](assets/test-bpconfig4.png)

   テストパッケージが正常に配信されたことを示すメッセージがページの下部に表示されます。

   >[!NOTE]
   >
   >配布エージェントを無効にしないでください。無効にすると、（実行中のキュー内の）アセットの配布が失敗する可能性があります。


AEM Assets クラウドインスタンスが Brand Portal で正常に設定され、次の操作が可能になりました。

* [AEM Assets から Brand Portal へのアセットの公開](publish-to-brand-portal.md)
* [AEM Assets から Brand Portal へのフォルダーの公開](publish-to-brand-portal.md#publish-folders-to-brand-portal)
* [AEM Assets から Brand Portal へのコレクションの公開](publish-to-brand-portal.md#publish-collections-to-brand-portal)

上記に加えて、AEM Assets のメタデータスキーマ、画像プリセット、検索ファセット、タグを Brand Portal に公開することもできます。

* [Brand Portal へのプリセット、スキーマ、ファセットの公開](https://docs.adobe.com/content/help/ja-JP/experience-manager-brand-portal/using/publish/publish-schema-search-facets-presets.html)
* [Brand Portal へのタグの公開](https://docs.adobe.com/content/help/ja-JP/experience-manager-brand-portal/using/publish/brand-portal-publish-tags.html)


詳しくは、[Brand Portal ドキュメント](https://docs.adobe.com/content/help/ja-JP/experience-manager-brand-portal/using/home.html)を参照してください。


## 配布ログ {#distribution-logs}

配布エージェントで実行されたアクションの詳細については、ログを確認できます。

例えば、AEM Assets から Brand Portal にアセットを発行し、設定を確認したとします。

1. 「**[!UICONTROL 接続をテスト]**」に示す手順（手順 1 ～ 4）に従い、配布エージェントページに移動します。

1. 「**[!UICONTROL ログ]**」をクリックして、配布ログを表示します。処理ログとエラーログは、ここで確認できます。

   ![](assets/test-bpconfig5.png)

配布エージェントは次のログを生成します。

* 情報：これは、構成が正常に完了したときにトリガーされるシステムが生成するログで、配布エージェントを有効にします。
* DSTRQ1（リクエスト 1）：テスト接続時にトリガーされます。

アセットの公開時に、次の要求および応答ログが生成されます。

**配布エージェントの要求**：
* DSTRQ2（リクエスト 2）：アセットの発行要求がトリガーされます。
* DSTRQ3（リクエスト 3）：アセットが存在するフォルダーの公開と、Brand Portal でのフォルダーの複製をおこなう別の要求がトリガーされます。

**配布エージェントの応答**：
* queue-bpdistributionagent0（DSTRQ2）：アセットが Brand Portal に公開されます。
* queue-bpdistributionagent0（DSTRQ3）：システムは、Brand Portal 内のアセットを含むフォルダーを複製します。

上記の例では、追加の要求と応答がトリガーされます。アセットが初めて発行されたので、Brand Portal で親フォルダ（追加パス）が見つからなかったため、アセットが発行された Brand Portal で同じ名前の親フォルダを作成する追加の要求をトリガーします。

>[!NOTE]
>
>親フォルダーが Brand Portal に存在しない場合（上記の例）、または親フォルダーが AEM Assets で変更された場合に、追加のリクエストが生成されます。



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
