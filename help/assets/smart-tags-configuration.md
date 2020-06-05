---
title: 拡張スマートタグ
description: Adobe Sensei の AI および ML サービスを利用して、状況に応じた説明的なビジネスタグを適用し、アセットの検出とコンテンツベロシティ（コンテンツ創出の高速化）を向上させます。
contentOwner: AG
translation-type: tm+mt
source-git-commit: bf7bb91dd488f39181a08adc592971d6314817de
workflow-type: tm+mt
source-wordcount: '1032'
ht-degree: 49%

---


# アセットのスマートタグ付けを行うためのExperience Managerの設定 {#configure-aem-for-smart-tagging}

タクソノミ制御のボキャブラリでアセットをタグ付けすると、タグベースの検索でアセットを簡単に識別および取得できます。 アドビでは、人工知能と機械学習アルゴリズムを使用して画像をトレーニングするスマートタグを提供しています。 スマートタグは、 [Adobe Senseiの人工知能フレームワークを使用して](https://www.adobe.com/sensei/experience-cloud-artificial-intelligence.html) 、タグ構造とビジネス分類に対する画像認識アルゴリズムのトレーニングを行います。

The Smart Tags functionality is available for purchase as an add-on to [!DNL Experience Manager]. 購入後、Adobe I/Oへのリンクを記載した電子メールが組織の管理者に送信されます。 管理者はリンクにアクセスし、スマートタグとAdobe I/Oを [!DNL Experience Manager] 使用して統合します。

<!-- TBD: 
1. Can a similar flowchart be created about how training works in CS? ![flowchart](assets/flowchart.gif)
2. Is there a link to buy SCS or initiate a sales call.
3. Keystroke all steps and check all screenshots.
4. Post-GA, if time permits, create a video.
-->

## Adobe I/Oとの統合 {#aio-integration}

SCSを使用して画像にタグ付けする前に、Adobe I/O [!DNL Adobe Experience Manager] を使用してSmart Tagsサービスと統合します。 バックエンドで、 [!DNL Experience Manager] サーバーは、要求をサービスに転送する前に、Adobe I/Oゲートウェイを使用してサービス資格情報を認証します。

* 公開鍵を生成す [!DNL Experience Manager] る設定をに作成します。 OAuth 統合用の公開証明書を取得します。
* Adobe I/O で統合を作成し、生成した公開鍵をアップロードします。
* Configure your [!DNL Experience Manager] instance using the API key and other credentials from Adobe I/O.
* （オプション）アセットアップロード時の自動タグ付けを有効化します。

### Adobe I/O統合の前提条件 {#prerequisite-for-aio-integration}

スマートタグを使用する前に、次の手順を実行してAdobe I/O上で統合を作成します。

* 組織の管理者権限を持つ Adobe ID アカウントがあること。
* 組織でスマートタグが有効になっています。

### Obtain a public certificate {#obtain-public-certificate}

公開証明書により、Adobe I/O でプロファイルを認証できます。

1. ユーザーインターフェイスで、 [!DNL Experience Manager] ツール **[!UICONTROL /]** クラウドサービス **[!UICONTROL /レガシーのクラウドサービスにアクセスします]******。

1. On the Cloud Services page, click **[!UICONTROL Configure Now]** under **[!UICONTROL Assets Smart Tags]**.

1. **[!UICONTROL 設定を作成]**&#x200B;ダイアログで、スマートタグ設定のタイトルと名前を指定します。「**[!UICONTROL 作成]**」をクリックします。

1. **[!UICONTROL AEM スマートコンテンツサービス]**&#x200B;ダイアログで、以下の値を使用します。

   **[!UICONTROL サービス URL]**: `https://mc.adobe.io/marketingcloud/smartcontent`

   **[!UICONTROL 認証サーバー]**: `https://ims-na1.adobelogin.com`

   その他のフィールドは現時点では空白のままにします（後で指定します）。「**[!UICONTROL OK]**」をクリックします。

   ![Experience ManagerのSmart Content ServiceダイアログでコンテンツサービスURLを指定](assets/aem_scs.png)

1. Click **[!UICONTROL Download Public Certificate for OAuth Integration]**, and download the public certificate file `AEM-SmartTags.crt`.

   ![スマートタグサービス用に作成された設定](assets/download_link.png)

### 証明書の有効期限が切れた場合に再設定する {#certrenew}

証明書の有効期限が切れると、証明書は信頼されなくなります。新しい証明書を追加するには、以下の手順に従います。期限切れの証明書は更新できません。

1. Log in your [!DNL Experience Manager] deployment as an administrator. **[!UICONTROL ツール]**／**[!UICONTROL セキュリティ]**／**[!UICONTROL ユーザー]**&#x200B;をクリックします。

1. **[!UICONTROL dam-update-service]** ユーザーを見つけてクリックします。「**[!UICONTROL キーストア]**」タブをクリックします。
1. 証明書の有効期限が切れた既存の **[!UICONTROL similaritysearch]** キーストアを削除します。「**[!UICONTROL 保存して閉じる]**」をクリックします。

   ![キーストアの既存の similaritysearch エントリを削除して新しいセキュリティ証明書を追加](assets/smarttags_delete_similaritysearch_keystore.png)

   *図： キーストアの既存の`similaritysearch`エントリを削除して、新しいセキュリティ証明書を追加します。*

1. **[!UICONTROL ツール]**／**[!UICONTROL クラウドサービス]**／**[!UICONTROL 従来のクラウドサービス]**&#x200B;に移動します。**[!UICONTROL アセットのスマートタグ]**／**[!UICONTROL 設定を表示]**／**[!UICONTROL 利用可能な設定]**&#x200B;をクリックします。必要な設定をクリックします。

1. 公開証明書をダウンロードするには、「**[!UICONTROL OAuth 統合用の公開証明書をダウンロード]**」をクリックします。

1. https://console.adobe.io [にアクセスし](https://console.adobe.io) 、プロジェクト内の既存のサービスに移動します。 新しい証明書をアップロードします。詳細については、[Adobe I/O 統合の作成](#create-aio-integration)の手順を参照してください。

### 統合の作成 {#create-aio-integration}

スマートタグAPIを使用するには、Adobe I/OでAPIキー、テクニカルアカウントID、組織IDおよびクライアントシークレットを生成する統合を作成します。

1. [https://console.adobe.io](https://console.adobe.io/) にアクセスします。
1. 適切なアカウントを選択し、関連付けられた組織の役割がシステム管理者であることを確認します。 プロジェクトを作成するか、既存のプロジェクトを開きます。 プロジェクトページで、「 **[!UICONTROL API追加」をクリックします]**。
1. API **[!UICONTROL 追加ページで、「]** Experience Cloud **[!UICONTROL 」を選択し、「]** Smart Content ****」を選択します。 「**[!UICONTROL 続行]**」をクリックします。
1. 次のページで、「**[!UICONTROL New integration]**」を選択します。「**[!UICONTROL 続行]**」をクリックします。
1. **[!UICONTROL Integration Details]** ページで、統合ゲートウェイの名前を指定し、説明を追加します。
1. 「**[!UICONTROL Public keys certificates]**」で、上記でダウンロードした `AEM-SmartTags.crt` ファイルをアップロードします。
1. 「**[!UICONTROL 統合を作成]**」をクリックします。
1. To view the integration information, click **[!UICONTROL Continue to integration details]**.

   ![「Overview」タブで、統合について指定した情報を確認できます。](assets/integration_details.png)

### スマートタグの設定 {#configure-smart-content-service}

統合を設定するには、Adobe I/O 統合のテクニカルアカウント ID、組織 ID、クライアントの秘密鍵、認証サーバーおよび API キーのフィールドの値を使用します。Creating a Smart Tags cloud configuration allows authentication of API requests from the [!DNL Experience Manager] instance.

1. In [!DNL Experience Manager], navigate to **[!UICONTROL Tools > Cloud Service > Legacy Cloud Services]** to open the [!UICONTROL Cloud Services] console.
1. 「**[!UICONTROL アセットのスマートタグ]**」で、上記で作成した設定を開きます。サービスの設定ページで、「**[!UICONTROL 編集]**」をクリックします。
1. **[!UICONTROL AEM スマートコンテンツサービス]**&#x200B;ダイアログで、「**[!UICONTROL サービス URL]**」および「**[!UICONTROL 認証サーバー]**」フィールドに事前入力された値を使用します。
1. 「**[!UICONTROL API キー]**」、「**[!UICONTROL テクニカルアカウント ID]**」、「**[!UICONTROL 組織 ID]**」、「**[!UICONTROL クライアントの秘密鍵]**」の各フィールドでは、上記で生成された値を使用します。

### 設定の検証 {#validate-the-configuration}

設定を完了したら、JMX MBean を使用して設定を検証できます。検証するには、次の手順に従います。

1. で [!DNL Experience Manager] サーバーにアクセスし `https://[aem_server]:[port]`ます。

1. **[!UICONTROL ツール／操作／Web コンソール]**&#x200B;に移動して、OSGi コンソールを開きます。**[!UICONTROL メイン／JMX]** を選択します。
1. 「**[!UICONTROL com.day.cq.dam.similaritysearch.internal.impl]**」をクリックします。**[!UICONTROL SimilaritySearch Miscellaneous Tasks]** が開きます。。
1. 「**[!UICONTROL validateConfigs()]**」をクリックします。In the **[!UICONTROL Validate Configurations]** dialog, click **[!UICONTROL Invoke]**.

   同じダイアログに検証結果が表示されます。

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

