---
title: 拡張スマートタグ
description: Adobe Sensei の AI および ML サービスを利用して、状況に応じた説明的なビジネスタグを適用し、アセットの検出とコンテンツベロシティ（コンテンツ創出の高速化）を向上させます。
contentOwner: AG
translation-type: tm+mt
source-git-commit: a1213a1694a50d174b4ad1e7e4ba7c71944b861a
workflow-type: tm+mt
source-wordcount: '1031'
ht-degree: 86%

---


# [!DNL Experience Manager]をアセットのスマートタグ付け用に構成{#configure-aem-for-smart-tagging}

分類に基づく統制語彙を使用してアセットをタグ付けすると、タグベースの検索でアセットを特定し、取得することが容易になります。Adobeには、人工知能と機械学習アルゴリズムを使用して画像をトレーニングするスマートタグが用意されています。 スマートタグは、[Adobe Sensei](https://www.adobe.com/jp/sensei/experience-cloud-artificial-intelligence.html) の人工知能フレームワークを使用して、タグ構造とビジネス上の分類に基づいて画像認識アルゴリズムのトレーニングをおこないます。

スマートタグ機能は、[!DNL Experience Manager] のアドオンとして購入できます。購入後、Adobe 開発者コンソールへのリンクを記載した電子メールが組織の管理者に送信されます。管理者はリンクにアクセスし、Adobe 開発者コンソールを使用してスマートタグと [!DNL Experience Manager] を統合します。

<!-- TBD: 
1. Can a similar flowchart be created about how training works in CS? ![flowchart](assets/flowchart.gif)
2. Is there a link to buy SCS or initiate a sales call.
3. Keystroke all steps and check all screenshots.
-->

>[!IMPORTANT]
>
>[!DNL Experience Manager Assets]のデプロイメントが[2020年8月のリリース](/help/release-notes/release-notes-cloud/2020/release-notes-2020-8-0.md#assets)の後に作成された場合、[!DNL Adobe Developer Console]はデフォルトで統合されます。 これにより、スマートタグ機能を迅速に設定できます。古いデプロイメントでは、管理者は次の手順を使用して手動で統合を設定できます。

## Adobe 開発者コンソールとの統合 {#aio-integration}

SCS を使用して画像にタグ付けする前に、Adobe 開発者コンソールを使用して [!DNL Adobe Experience Manager] とスマートタグサービスを統合します。バックエンドでは、サービスに要求を転送する前に、[!DNL Experience Manager] サーバーが Adobe 開発者コンソールのゲートウェイでサービスの資格情報を認証します。

* 公開鍵を生成する設定を [!DNL Experience Manager] に作成します。OAuth 統合用の[公開証明書を取得します](#obtain-public-certificate)。
* [Adobe 開発者コンソールで統合を作成](#create-aio-integration)し、生成した公開鍵をアップロードします。
* API キーやその他の Adobe 開発者コンソールの資格情報を使用して、[!DNL Experience Manager] インスタンスで[スマートタグを設定](#configure-smart-content-service)します。
* [設定をテストします](#validate-the-configuration)。
* [証明書の有効期限が切れた後に再設定します](#certrenew)。

### Adobe 開発者コンソール統合の前提条件 {#prerequisite-for-aio-integration}

Adobe 開発者コンソールで統合を作成してスマートタグを使用する前に、以下の事項を確認します。

* 組織の管理者権限を持つ Adobe ID アカウントがあること。
* お客様の組織でスマートタグが有効になっていること。

### 公開証明書の取得 {#obtain-public-certificate}

公開証明書により、Adobe 開発者コンソールでプロファイルを認証できます。証明書は、[!DNL Experience Manager] にて作成します。

1. [!DNL Experience Manager] ユーザーインターフェイスで、**[!UICONTROL ツール]**／**[!UICONTROL セキュリティ]**／**[!UICONTROL Adobe IMS 設定]**&#x200B;にアクセスします。

1. [!UICONTROL Adobe IMS 設定]ページで、「**[!UICONTROL 作成]**」をクリックします。**[!UICONTROL クラウドソリューション]**&#x200B;メニューから、「**[!UICONTROL スマートタグ]**」を選択します。

1. 「**[!UICONTROL 新しい証明書を作成]**」を選択します。名前を入力し、「**[!UICONTROL 証明書を作成]**」をクリックします。「**[!UICONTROL OK]**」をクリックします。

1. 「**[!UICONTROL 公開鍵をダウンロード]**」をクリックします。

   ![[!DNL Experience Manager] スマートタグで公開鍵を作成](assets/aem_smarttags-config1.png)

### 統合の作成 {#create-aio-integration}

スマートタグを使用するには、Adobe 開発者コンソールで統合を作成して、API キー、テクニカルアカウント ID、組織 ID およびクライアントの秘密鍵を生成します。

1. ブラウザーで [https://console.adobe.io](https://console.adobe.io/) にアクセスします。適切なアカウントを選択し、関連付けられた組織の役割がシステム管理者であることを確認します。
1. 任意の名前でプロジェクトを作成します。「**[!UICONTROL API を追加]**」をクリックします。
1. **[!UICONTROL 追加API]**&#x200B;ページで、**[!UICONTROL Experience Cloud]**&#x200B;を選択し、**[!UICONTROL スマートコンテンツ]**&#x200B;を選択します。 「**[!UICONTROL 次へ]**」をクリックします。
1. 「**[!UICONTROL 公開鍵をアップロード]**」を選択します。[!DNL Experience Manager]からダウンロードした証明書ファイルを指定します。[!UICONTROL 公開鍵が正常にアップロード]されたというメッセージが表示されます。「**[!UICONTROL 次へ]**」をクリックします。
1. [!UICONTROL 新しいサービスアカウント(JWT)] 秘密鍵証明書を作成します。ページには、サービスアカウントの公開鍵が表示されます。「**[!UICONTROL 次へ]**」をクリックします。
1. **[!UICONTROL 製品プロファイルを選択]**&#x200B;ページで、「**[!UICONTROL スマートコンテンツサービス]**」を選択します。「**[!UICONTROL 設定済み API を保存]**」をクリックします。設定に関する詳細情報がページに表示されます。[!DNL Experience Manager]でスマートタグをさらに設定する場合は、このページを開いたままにして、[!DNL Experience Manager]にこれらの値をコピーして追加します。

   ![「概要」タブで、統合について指定した情報を確認できます。](assets/integration_details.png)

### スマートタグの設定 {#configure-smart-content-service}

統合を設定するには、Adobe 開発者コンソール統合のペイロード、クライアントの秘密鍵、認証サーバーおよび API キーフィールドの値を使用します。

1. [!DNL Experience Manager] ユーザーインターフェイスで、**[!UICONTROL ツール]**／**[!UICONTROL セキュリティ]**／**[!UICONTROL Adobe IMS 設定]**&#x200B;にアクセスします。
1. **[!UICONTROL Adobe IMS テクニカルアカウント設定]**&#x200B;ページにアクセスし、必要な&#x200B;**[!UICONTROL タイトル]**&#x200B;を入力します。
1. 「**[!UICONTROL 認証サーバー]**」フィールドに `https://ims-na1.adobelogin.com` URL を入力します。
1. 「**[!UICONTROL API キー]**」フィールドに、[!DNL Adobe Developer Console] から&#x200B;**[!UICONTROL クライアント ID]** を入力します。
1. 「**[!UICONTROL クライアントの秘密鍵]**」フィールドに、[!DNL Adobe Developer Console] から&#x200B;**[!UICONTROL クライアントの秘密鍵]**&#x200B;を入力します。「**[!UICONTROL クライアントの秘密鍵を取得]**」オプションをクリックして表示します。
1. [!DNL Adobe Developer Console]のご自身のプロジェクトで、左側の余白から「**[!UICONTROL サービスアカウント（JWT）]**」をクリックします。「**[!UICONTROL JWT を生成]**」タブをクリックします。「**[!UICONTROL コピー]**」をクリックして、表示された **[!UICONTROL JWT ペイロード]**&#x200B;をコピーします。この値を、[!DNL Experience Manager] の「**[!UICONTROL ペイロード]**」フィールドに指定します。「**[!UICONTROL 作成]**」をクリックします。

### 設定の検証 {#validate-the-configuration}

設定が完了したら、次の手順に従って設定を検証します。

1. [!DNL Experience Manager] ユーザーインターフェイスで、**[!UICONTROL ツール]**／**[!UICONTROL セキュリティ]**／**[!UICONTROL Adobe IMS 設定]**&#x200B;にアクセスします。

1. 「スマートタグ設定」を選択します。ツールバーの「**[!UICONTROL 正常性をチェック]**」をクリックします。「**[!UICONTROL チェック]**」をクリックします。[!UICONTROL Healthy configuration] というメッセージを含むダイアログが表示されることで、設定が機能していることが確認できます。

![スマートタグ設定の検証](assets/smart-tag-config-validation.png)

### 証明書の有効期限が切れた場合の再設定 {#certrenew}

証明書の有効期限が切れると、証明書は信頼されなくなります。証明書を追加するには、次の手順に従います。 期限切れの証明書は更新できません。

1. [!DNL Experience Manager] デプロイメントに管理者としてログインします。**[!UICONTROL ツール]**／**[!UICONTROL セキュリティ]**／**[!UICONTROL ユーザー]**&#x200B;をクリックします。

1. **[!UICONTROL dam-update-service]** ユーザーを見つけてクリックします。「**[!UICONTROL キーストア]**」タブをクリックします。
1. 証明書の有効期限が切れた既存の **[!UICONTROL similaritysearch]** キーストアを削除します。「**[!UICONTROL 保存して閉じる]**」をクリックします。

   ![キーストアの既存の類似性検索エントリを削除して、新しいセキュリティ証明書を追加します](assets/smarttags_delete_similaritysearch_keystore.png)

   *図：キーストアの既存の `similaritysearch` エントリを削除し、セキュリティ証明書を追加します。*

1. [!DNL Experience Manager] ユーザーインターフェイスで、**[!UICONTROL ツール]**／**[!UICONTROL セキュリティ]**／**[!UICONTROL Adobe IMS 設定]**&#x200B;にアクセスします。使用可能なスマートタグ設定を開きます。公開証明書をダウンロードするには、「**[!UICONTROL 公開証明書をダウンロード]**」をクリックします。

1. [https://console.adobe.io](https://console.adobe.io) にアクセスし、プロジェクト内の既存のサービスに移動します。新しい証明書をアップロードし、設定します。設定について詳しくは、[Adobe 開発者コンソール統合の作成](#create-aio-integration)の手順を参照してください。

## アセットがアップロードされたときに自動タグ付けを有効にする（オプション） {#enable-smart-tagging-for-uploaded-assets}

1. [!DNL Experience Manager] で、**[!UICONTROL ツール／ワークフロー／モデル]**&#x200B;に移動します。
1. **[!UICONTROL ワークフローモデル]**&#x200B;ページで、「**[!UICONTROL DAM アセットの更新]**」ワークフローモデルを選択します。
1. ツールバーの「**[!UICONTROL 編集]**」をクリックします。
1. サイドパネルを展開して、ステップを表示します。「DAM ワークフロー」セクションの「**[!UICONTROL スマートタグアセット]**」ステップをドラッグして、「**[!UICONTROL サムネールを処理]**」ステップの後に配置します。

   ![「DAM アセットの更新」ワークフローで「サムネールを処理」ステップの後に「スマートタグアセット」ステップを追加](assets/chlimage_1-105.png)

   *図：「DAM アセットの更新」ワークフローで「サムネールを処理」ステップの後に「スマートタグアセット」ステップを追加。*

1. 設定する手順を開きます。「**[!UICONTROL 詳細設定]**」で、「**[!UICONTROL ハンドラー処理の設定]**」オプションが選択されていることを確認します。

   ![ワークフローの次の手順に進むハンドラーの設定。](assets/smart-tags-workflow-handler-setting.png)

1. タグの予測時にエラーを無視する場合は、「**[!UICONTROL 引数]**」タブで「**[!UICONTROL エラーを無視]**」を選択します。フォルダーでスマートタグが有効になっているかに関わらずアップロード時にアセットをタグ付けするには、「**[!UICONTROL スマートタグフラグを無視]**」を選択します。

1. 「**[!UICONTROL OK]**」をクリックします。プロセスステップを閉じます。 ワークフローを保存します。「**[!UICONTROL 同期]**」をクリックします。

>[!MORELIKETHIS]
>
>* [スマートサービスを使用したアセットのタグ付け](smart-tags.md)

