---
title: 拡張スマートタグ
description: Adobe Sensei の AI および ML サービスを利用して、状況に応じた説明的なビジネスタグを適用し、アセットの検出とコンテンツベロシティ（コンテンツ創出の高速化）を向上させます。
contentOwner: AG
translation-type: tm+mt
source-git-commit: c24fa22178914b1186b7f29bdab64d3bca765fe5
workflow-type: tm+mt
source-wordcount: '1009'
ht-degree: 21%

---


# アセットのスマートタグ付けのExperience Managerの設定 {#configure-aem-for-smart-tagging}

タクソノミ制御のボキャブラリでアセットをタグ付けすると、タグベースの検索でアセットを簡単に識別および取得できます。 アドビでは、人工知能と機械学習アルゴリズムを使用して画像をトレーニングするスマートタグを提供しています。 スマートタグは、 [Adobe Senseiの人工知能フレームワークを使用して](https://www.adobe.com/sensei/experience-cloud-artificial-intelligence.html) 、タグ構造とビジネス分類に対する画像認識アルゴリズムのトレーニングを行います。

The Smart Tags functionality is available for purchase as an add-on to [!DNL Experience Manager]. 購入後、Adobe Developer Consoleへのリンクを記載した電子メールが組織の管理者に送信されます。 管理者は、Adobe Developer Consoleを [!DNL Experience Manager] 使用してスマートタグを統合するためのリンクにアクセスします。

<!-- TBD: 
1. Can a similar flowchart be created about how training works in CS? ![flowchart](assets/flowchart.gif)
2. Is there a link to buy SCS or initiate a sales call.
3. Keystroke all steps and check all screenshots.
-->

## Adobe Developer Consoleとの連携 {#aio-integration}

SCSを使用して画像にタグ付けする前に、Adobe Developer Console [!DNL Adobe Experience Manager] を使用してSmart Tagsサービスと統合します。 At the back end, the [!DNL Experience Manager] server authenticates your service credentials with the Adobe Developer Console gateway before forwarding your request to the service.

* 公開鍵を生成す [!DNL Experience Manager] る設定をに作成します。 [OAuth 統合用の公開証明書を取得します。](#obtain-public-certificate)
* [Adobe Developer Consoleで統合を作成し](#create-aio-integration) 、生成した公開鍵をアップロードします。
* [APIキーとAdobe Developer Consoleの他の資格情報を使用して、](#configure-smart-content-service)[!DNL Experience Manager] インスタンスでスマートタグを設定します。
* [設定をテストします](#validate-the-configuration)。
* [証明書の有効期限が切れた後に再設定します](#certrenew)。

### Adobe Developer Console統合の前提条件 {#prerequisite-for-aio-integration}

スマートタグを使用する前に、次の手順に従ってAdobe Developer Consoleで統合を作成します。

* 組織の管理者権限を持つ Adobe ID アカウントがあること。
* 組織でスマートタグが有効になっています。

### Obtain a public certificate {#obtain-public-certificate}

公開証明書を使用すると、Adobe Developer Consoleでプロファイルを認証できます。 証明書は、内から作成し [!DNL Experience Manager]ます。

1. ユーザーインターフェイスで、 [!DNL Experience Manager] ツール **[!UICONTROL /]** セキュリティ **[!UICONTROL /]** Adobe IMS設定にアクセスします ****。

1. [!UICONTROL Adobe IMS設定] ページで、「 **[!UICONTROL 作成]**」をクリックします。 「 **[!UICONTROL Cloud Solution]** 」メニューで「 **[!UICONTROL スマートタグ]**」を選択します。

1. Select **[!UICONTROL Create new certificate]**. 名前を入力し、「証明書を **[!UICONTROL 作成]**」をクリックします。 「**[!UICONTROL OK]**」をクリックします。

1. Click **[!UICONTROL Download Public Key]**.

   ![Experience Managerスマートタグで公開鍵を作成](assets/aem_smarttags-config1.png)

### 統合の作成 {#create-aio-integration}

スマートタグを使用するには、Adobe Developer ConsoleでAPIキー、テクニカルアカウントID、組織IDおよびクライアントシークレットを生成する統合を作成します。

1. ブラウザ [ーでhttps://console.adobe.io](https://console.adobe.io/) にアクセスします。 適切なアカウントを選択し、関連付けられた組織の役割がシステム管理者であることを確認します。
1. 任意の名前でプロジェクトを作成します。 「 **[!UICONTROL API追加」をクリックします]**。
1. API **[!UICONTROL 追加ページで、「]** Experience Cloud **[!UICONTROL 」を選択し、「ス]** マートコンテンツ ****」を選択します。 「**[!UICONTROL 次へ]**」をクリックします。
1. 「公開鍵を **[!UICONTROL アップロード]**」を選択します。 からダウンロードした証明書ファイルを指定し [!DNL Experience Manager]ます。 正常にアップロードされた [!UICONTROL 公開鍵] （複数可）というメッセージが表示されます。 「**[!UICONTROL 次へ]**」をクリックします。
1. [!UICONTROL 新しいサービスアカウント(JWT)秘密鍵証明書を作成] (JWT)ページには、設定したサービスアカウントの公開鍵が表示されます。 「**[!UICONTROL 次へ]**」をクリックします。
1. 製品プロファイルを **[!UICONTROL 選択]** ページで、「 **[!UICONTROL Smart Content Services]**」を選択します。 「設定済みAPI **[!UICONTROL を保存]**」をクリックします。 設定に関する詳細情報がページに表示されます。 でスマートタグをさらに設定する場合は、このページを開いたままにして、これらの値をコピーし、Experience Managerに追加 [!DNL Experience Manager]します。

   ![「Overview」タブで、統合について指定した情報を確認できます。](assets/integration_details.png)

### スマートタグの設定 {#configure-smart-content-service}

統合を設定するには、Adobe Developer Console統合のペイロード、クライアントシークレット、認証サーバーおよびAPIキーフィールドの値を使用します。

1. ユーザーインターフェイスで、 [!DNL Experience Manager] ツール **[!UICONTROL /]** セキュリティ **[!UICONTROL /]** Adobe IMS設定にアクセスします ****。
1. 「 **[!UICONTROL Adobe IMSテクニカルアカウント設定]** 」ページにアクセスし、必要な **[!UICONTROL タイトルを入力します]**。
1. 「 **[!UICONTROL 認証サーバー]** 」フィールドに `https://ims-na1.adobelogin.com` URLを入力します。
1. 「 **[!UICONTROL APIキー]** 」フィールドに、 **[!UICONTROL から]**[!DNL Adobe Developer Console]クライアントIDを入力します。
1. 「 **[!UICONTROL Client Secret]** ( **[!UICONTROL クライアントシークレット)]** 」フィールドに、 [!DNL Adobe Developer Console]から「Client Secret（クライアントシークレット）」を入力します。 「 **[!UICONTROL クライアントシークレットを]** 取得」オプションをクリックして表示します。
1. プロジェクト [!DNL Adobe Developer Console]で、左側の余白から「 **[!UICONTROL サービスアカウント(JWT)]** 」をクリックします。 「JWT **[!UICONTROL を生成]** 」タブをクリックします。 「 **[!UICONTROL Copy]** 」をクリックして、表示された **[!UICONTROL JWT Payloadをコピーします]**。 この値は、の **[!UICONTROL Payload]** フィールドに指定し [!DNL Experience Manager]ます。 「**[!UICONTROL 作成]**」をクリックします。

### 設定の検証 {#validate-the-configuration}

設定が完了したら、次の手順に従って設定を検証します。

1. ユーザーインターフェイスで、 [!DNL Experience Manager] ツール **[!UICONTROL /]** セキュリティ **[!UICONTROL /]** Adobe IMS設定にアクセスします ****。

1. スマートタグ設定を選択します。 ツールバーの「 **[!UICONTROL ヘルスをチェック]** 」をクリックします。 「**[!UICONTROL チェック]**」をクリック。「 [!UICONTROL Healthy configuration] 」というメッセージが表示されたダイアログで、設定が機能していることを確認します。

![スマートタグ設定の検証](assets/smart-tag-config-validation.png)

### 証明書の有効期限が切れた場合に再設定する {#certrenew}

証明書の有効期限が切れると、証明書は信頼されなくなります。新しい証明書を追加するには、以下の手順に従います。期限切れの証明書は更新できません。

1. Log in your [!DNL Experience Manager] deployment as an administrator. **[!UICONTROL ツール]**／**[!UICONTROL セキュリティ]**／**[!UICONTROL ユーザー]**&#x200B;をクリックします。

1. **[!UICONTROL dam-update-service]** ユーザーを見つけてクリックします。「**[!UICONTROL キーストア]**」タブをクリックします。
1. 証明書の有効期限が切れた既存の **[!UICONTROL similaritysearch]** キーストアを削除します。「**[!UICONTROL 保存して閉じる]**」をクリックします。

   ![キーストアの既存の similaritysearch エントリを削除して新しいセキュリティ証明書を追加](assets/smarttags_delete_similaritysearch_keystore.png)

   *図： キーストアの既存の`similaritysearch`エントリを削除して、新しいセキュリティ証明書を追加します。*

1. ユーザーインターフェイスで、 [!DNL Experience Manager] ツール **[!UICONTROL /]** セキュリティ **[!UICONTROL /]** Adobe IMS設定にアクセスします ****。 使用可能なスマートタグ設定を開きます。 To download a public certificate, click **[!UICONTROL Download Public Certificate]**.

1. https://console.adobe.io [にアクセスし](https://console.adobe.io) 、プロジェクト内の既存のサービスに移動します。 新しい証明書をアップロードし、設定します。 設定について詳しくは、Adobe Developer Console統合の [作成の手順を参照してください](#create-aio-integration)。

## 新しくアップロードされたアセットに対するスマートタグの有効化（オプション） {#enable-smart-tagging-for-uploaded-assets}

1. で [!DNL Experience Manager]、 **[!UICONTROL ツール/ワークフロー/モデルに移動します]**。
1. **[!UICONTROL ワークフローモデル]**&#x200B;ページで、「**[!UICONTROL DAM アセットの更新]**」ワークフローモデルを選択します。
1. Click **[!UICONTROL Edit]** from the toolbar.
1. サイドパネルを展開して、ステップを表示します。「DAM ワークフロー」セクションの「**[!UICONTROL スマートタグアセット]**」ステップをドラッグして、「**[!UICONTROL サムネールを処理]**」ステップの後に配置します。

   ![「DAM アセットの更新」ワークフローで「サムネールを処理」ステップの後に「スマートタグアセット」ステップを追加](assets/chlimage_1-105.png)

   *図： DAM追加 Update Assetワークフローのプロセスサムネールの手順後のスマートタグアセットの手順です。*

1. 設定する手順を開きます。 「**[!UICONTROL 詳細設定]**」で、「**[!UICONTROL ハンドラー処理の設定]**」オプションが選択されていることを確認します。

   ![ワークフローの次の手順に進むハンドラーの設定。](assets/smart-tags-workflow-handler-setting.png)

1. タグの予測時にエラーを無視する場合は、 **[!UICONTROL 「]** 引数 **[!UICONTROL 」タブで「エラーを無視」を選択します]** 。 フォルダーでスマートタグが有効になっているかに関わらずアップロード時にアセットをタグ付けするには、「**[!UICONTROL スマートタグフラグを無視]**」を選択します。

1. Click **[!UICONTROL OK]** to close the process step, and then save the workflow. 「 **[!UICONTROL 同期]**」をクリックします。

>[!MORELIKETHIS]
>
>* [スマートサービスを使用したアセットのタグ付け](smart-tags.md)

