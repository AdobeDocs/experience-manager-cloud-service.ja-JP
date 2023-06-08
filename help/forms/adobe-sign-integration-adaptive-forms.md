---
title: Adobe Acrobat SignとAEM Formsの統合方法
description: Adobe Acrobat Signを [!DNL AEM Forms] as a Cloud Service?
feature: Adaptive Forms
role: User
level: Intermediate
source-git-commit: 5801063c9c4c1c6b9f9e7f55ad4d66bb563e0eef
workflow-type: tm+mt
source-wordcount: '1918'
ht-degree: 46%

---

# 接続 [!DNL AEM Forms] as a Cloud Service [!DNL Adobe Acrobat Sign] {#integrate-adobe-sign-with-aem-forms}

[!DNL Adobe Acrobat Sign] アダプティブFormsおよびAEMワークフローの電子署名ワークフローを有効にします。 電子サインを使用すると、法務、販売、給与、人事管理など、様々な分野におけるドキュメント処理ワークフローが改善されます。

[!DNL Adobe Acrobat Sign] とアダプティブフォームの一般的なシナリオでは、ユーザーがアダプティブフォームに入力してサービスを申し込みます。例えば、クレジットカードの申込フォームや住民サービスフォームなどです。ユーザーが申込フォームに入力、送信、署名すると、フォームがサービスプロバイダーに送信され、さらにアクションが実行されます。 サービスプロバイダーは受信した申込フォームを確認し、[!DNL Adobe Acrobat Sign] を使用して申請を承認します。AEM Formsは、Adobe Acrobat SignとAdobe Acrobat Sign Solutionsの両方の政府機関をサポートしています。 ライセンスと要件に応じて、次のいずれかのソリューションとAEM Formsを統合または接続できます。

* [AEM FormsとAdobe Acrobat Signの接続](#adobe-sign)
* [AEM FormsをAdobe Acrobat Sign Solutionsと連携して政府機関向け](#adobe-acrobat-sign-for-government)

## AEM FormsとAdobe Acrobat Signの接続 {#adobe-sign}

接続するには **[!DNL AEM Forms]** と **[!DNL Adobe Acrobat Sign]**&#x200B;を設定し、前提条件の節に示すソフトウェアとアカウントを設定して、 Forms as a Cloud ServiceオーサーインスタンスとパブリッシュインスタンスでAdobe Sign Cloud Serviceを設定します。

### AEM FormsをAdobe Acrobat Signに接続するための前提条件 {#prerequisites-for-adobe-sign}

を統合するには、次の設定が必要です。 [!DNL Adobe Acrobat Sign] と [!DNL AEM Forms]:

1. アクティブ [Adobe Acrobat Sign開発者アカウント](https://acrobat.adobe.com/jp/ja/sign/developer-form.html).
1. An [Adobe Acrobat Sign API アプリケーション](https://www.adobe.io/apis/documentcloud/sign/docs.html#!adobedocs/adobe-sign/master/gstarted/create_app.md).
1. [!DNL Adobe Acrobat Sign] API アプリケーションの資格情報（クライアント ID およびクライアントの秘密鍵）。
1. （政府機関 ID ベースの認証の場合のみ） [認証方法を有効にする](https://helpx.adobe.com/jp/sign/using/adobesign-authentication-government-id.html#AuditReport) 政府 ID 認証用。



### AEM FormsオーサーインスタンスとパブリッシュインスタンスのAdobe Acrobat Signへの接続 {#configure-adobe-sign-with-aem-forms}

上記の前提条件の準備が完了したら、以下の手順により、オーサーインスタンス上の [!DNL AEM Forms] を使用して [!DNL Adobe Acrobat Sign] を設定します。

1. AEM Forms のオーサーインスタンスで、**[!UICONTROL ツール]** ![ハンマー](assets/hammer.png)／**[!UICONTROL 一般]**／**[!UICONTROL 設定ブラウザー]**&#x200B;に移動します。
1. **[!UICONTROL 設定ブラウザー]**&#x200B;ページで「**[!UICONTROL 作成]**」をタップします。
1. **[!UICONTROL 設定を作成]**&#x200B;ダイアログで、設定の&#x200B;**[!UICONTROL タイトル]**&#x200B;を指定し、「**[!UICONTROL クラウド設定]**」を有効にして「**[!UICONTROL 作成]**」をタップします。これにより、Cloud Services 用の設定コンテナが作成されます。フォルダー名にスペースが含まれていないことを確認します。
1. に移動します。 **[!UICONTROL ツール]** ![ハンマー](assets/hammer.png) > **[!UICONTROL Cloud Services]** > **[!UICONTROL Adobe Acrobat Sign]** 前の手順で作成した設定コンテナを開きます。

   >[!NOTE]
   >
   >アダプティブフォームを作成する際に、**[!UICONTROL 設定コンテナ]**&#x200B;フィールドにコンテナ名を指定します。

1. 設定ページで「**[!UICONTROL 作成]**」をタップして、AEM Forms 内に [!DNL Adobe Acrobat Sign] の設定を作成します。
1. 内 **[!UICONTROL 一般]** タブ **[!UICONTROL Adobe Acrobat Sign設定を作成]** ページで、 **[!UICONTROL 名前]** 設定の場合は、 **[!UICONTROL 次へ]**. 必要に応じて&#x200B;**[!UICONTROL タイトル]**&#x200B;を指定し、設定の&#x200B;**[!UICONTROL サムネ―ル]**&#x200B;を参照して選択することもできます。

1. 次の操作を実行できます。 **[!UICONTROL ソリューションを選択]** 選択 [!DNL Adobe Acrobat Sign].

   ![Adobe Acrobat Sign Solutions for Government](assets/adobe-sign-solution.png)

1. 現在のブラウザウィンドウに存在する URL をメモ帳にコピーし、パーツを削除します。 `/ui#/aem` を URL から取得します。 次に、変更した URL を設定する必要があります。 [!DNL Adobe Acrobat Sign] 次を使用した適用 [!DNL AEM Forms]（後の手順） 「**[!UICONTROL 次へ]**」をタップします。

1. 「**[!UICONTROL 設定]**」タブで、「**[!UICONTROL OAuth URL]**」フィールドにはデフォルトの URL が入力されています。URL の形式は次の通りです。

   `https://<shard>/public/oAuth/v2`

   次に例を示します。
   `https://secure.na1.echosign.com/public/oauth/v2`

   各パラメーターの意味は次のとおりです。

   **na1** は、デフォルトのデータベースシャードを参照します。データベースシャードの値を更新することができます。[!DNL  Adobe Acrobat Sign] クラウド設定で、[正しいシャード](https://helpx.adobe.com/jp/sign/using/identify-account-shard.html)をポイントしていることを確認します。

   別の [!DNL Adobe Acrobat Sign] 設定を Adobe Experience Manager の機能またはコンポーネント用に作成する場合は、すべての [!DNL Adobe Acrobat Sign] クラウド設定が同じシャードをポイントしていることを確認してください。

   >[!NOTE]
   >
   > キープ **Adobe Acrobat Sign設定を作成** ページが開きます。 閉じないでください。 **クライアント ID** および&#x200B;**クライアント秘密鍵**&#x200B;は、以降の手順で説明するように、[!DNL Adobe Acrobat Sign] アプリケーションの OAuth 設定を行った後に取得できます。


1. 以下の手順により、[!DNL Adobe Acrobat Sign] アプリケーション用に OAuth 設定を構成します。

   1. ブラウザーウィンドウを開き、[!DNL Adobe Acrobat Sign] 開発者アカウントにログインします。
   1. [!DNL AEM Forms] 用に設定されているアプリケーションを選択し、「**[!UICONTROL アプリケーションの OAuth を設定]**」をタップします。
   1. 前述の手順（手順 8）でコピーした URL を「**[!UICONTROL リダイレクト URL]**」ボックスに追加して「**[!UICONTROL 保存]**」をクリックします。
   1. [!DNL Adobe Acrobat Sign] アプリケーションに対して以下の範囲を有効にして、「**[!UICONTROL 保存]**」をクリックします。
   * [!DNL aggrement_read]
   * [!DNL aggrement_write]
   * [!DNL aggrement_send]
   * [!DNL widget_read]
   * [!DNL widget_write]
   * [!DNL workflow_read]

   [!DNL Adobe Acrobat Sign] アプリケーション用に OAuth 設定を構成してキーを取得するための詳しい手順については、開発者用ドキュメントの[アプリケーション用に OAuth 設定を構成する](https://www.adobe.io/apis/documentcloud/sign/docs.html#!adobedocs/adobe-sign/master/gstarted/configure_oauth.md)を参照してください。

   ![OAuth 設定](assets/oauthconfig_new.png)

1. に戻ります。 **[!UICONTROL Adobe Acrobat Sign設定を作成]** ページ。 「**[!UICONTROL 設定]**」タブで、「**[!UICONTROL クライアント ID]**（アプリケーション ID）と&#x200B;**[!UICONTROL クライアントシークレット]**」の値を指定します。以下を使用： [Adobe Acrobat Signアプリケーションのクライアント ID およびクライアント秘密鍵](https://opensource.adobe.com/acrobat-sign/developer_guide/helloworld.html#get-the-app-id-and-secret) 前の手順で作成した。

1. を選択します。 **[!UICONTROL 添付ファイルに対してAdobe Acrobat Signを有効にする]** アダプティブフォームに添付されたファイルを、対応する [!DNL Adobe Acrobat Sign] ドキュメントが署名用に送信されました。

1. タップ **[!UICONTROL Adobe Acrobat Signに接続]**. 資格情報の入力を求められたら、 **ユーザー名** および **パスワード** 作成時に使用するアカウントの [!DNL Adobe Acrobat Sign] アプリケーション。 確認を求められたら、次の項目にアクセスします `your developer account`，クリック **[!UICONTROL アクセスを許可]**. 資格情報が正しく、[!DNL AEM Forms] が [!DNL Adobe Acrobat Sign] 開発者アカウントにアクセスできるようにした場合は、次のような成功メッセージが表示されます。

   ![Adobe Acrobat Sign Cloud 設定成功](assets/adobe-sign-cloud-configuration-success.png)

1. 「**[!UICONTROL 作成]**」をタップして、[!DNL Adobe Acrobat Sign] 設定を作成します。

1. 設定を選択し、「**[!UICONTROL 公開]**」をクリックします&#x200B;**[!UICONTROL 。]**&#x200B;これにより、対応するパブリッシュ環境に設定が複製されます。

1. 開発者、ステージ、実稼働用のインスタンス（残っているいずれか）で上記の手順をすべて繰り返し、お使いの環境用に [!DNL Adobe Acrobat Sign] を [!DNL AEM Forms] で設定する作業を完了します。

次に、以下を実行できます。 [「 Adobe Acrobat Signフィールドをアダプティブフォームに追加」を使用します。](working-with-adobe-sign.md). [!DNL Adobe Acrobat Sign] 用に有効化するすべてのアダプティブフォームに、Cloud Service に使用する設定コンテナを追加してください。設定コンテナは、アダプティブフォームのプロパティから指定できます。

## AEM FormsをAdobe Acrobat Sign Solutionsと連携して政府機関向け {#adobe-acrobat-sign-for-government}

AEM FormsとAdobe Acrobat Sign Solutions for Government の接続は、複数の手順で構成されます。 以下が含まれます。

* AEMインスタンスのリダイレクト URL の作成
* リダイレクト URL とスコープをAdobe Sign Solutions for Government チームと共有する
* Adobe Signチームからの資格情報の受信
* 受け取った資格情報を使用してAEM FormsをAdobe Acrobat Sign Solutions for Government に接続します

![](/help/forms/assets/adobe-acrobat-sign-govt-workflow.png)


AEM Formsas a Cloud Serviceは、開発環境、ステージ環境、実稼動環境を提供します。 の開発環境とAdobe Acrobat Sign Solutions for Government を接続する方法を後で開始し、ステージ環境と実稼動環境を接続する方法について説明します。

### 事前準備 {#prerequisites-for-adobe-sign-for-acrobat-sign-for-government}

AEM FormsとAdobe Acrobat Signソリューションの接続を開始する前に、 [Adobe Acrobat Sign Solutions for Government](https://opensource.adobe.com/acrobat-sign/signgov/gstarted.html#account-provisioning) アカウントがプロビジョニングされました。


### AEM Formsas a Cloud ServiceとAdobe Acrobat Sign Solutions for Government {#connect-adobe-acrobat-sign-for-government}

#### AEMインスタンスのリダイレクト URL の作成

1. Formsas a Cloud Serviceのオーサーインスタンスで、に移動します。 **[!UICONTROL ツール]** ![ハンマー](assets/hammer.png) > **[!UICONTROL 一般]** > **[!UICONTROL 設定ブラウザー]**.
1. **[!UICONTROL 設定ブラウザー]**&#x200B;ページで「**[!UICONTROL 作成]**」をタップします。
1. **[!UICONTROL 設定を作成]**&#x200B;ダイアログで、設定の&#x200B;**[!UICONTROL タイトル]**&#x200B;を指定し、「**[!UICONTROL クラウド設定]**」を有効にして「**[!UICONTROL 作成]**」をタップします。これにより、Cloud Services 用の設定コンテナが作成されます。フォルダー名にスペースが含まれていないことを確認します。
1. に移動します。 **[!UICONTROL ツール]** ![ハンマー](assets/hammer.png) > **[!UICONTROL Cloud Services]** > **[!UICONTROL Adobe Acrobat Sign]** 前の手順で作成した設定コンテナを開きます。 アダプティブフォームを作成する際に、**[!UICONTROL 設定コンテナ]**&#x200B;フィールドにコンテナ名を指定します。
1. 設定ページで「**[!UICONTROL 作成]**」をタップして、AEM Forms 内に [!DNL Adobe Acrobat Sign] の設定を作成します。
1. 現在のブラウザーウィンドウの URL をメモ帳にコピーし、を削除します。 `/ui#/aem` を URL から取得します。 この URL は `re-direct URL`. 次の節では、 `re-direct URL` および `Scopes` Adobe Signチームとリクエスト資格情報（クライアント ID とクライアント秘密鍵）を使用します。


#### リダイレクト URL とスコープをAdobe Signチームと共有し、資格情報を受け取る

Adobe Acrobat Sign for Government Solutions チームには、 `re-direct URL` Adobe Acrobat Signアプリケーション（以下に示す）でAEM Formsと政府機関向けのAdobe Acrobat Sign Solutionsとの接続を可能にする資格情報（クライアント ID とクライアント秘密鍵）を生成するために有効にするスコープ。

共有する `scopes` （以下に示す）および `re-direct URL` を作成し、前の節の最後の手順をAdobe Acrobat Sign for Government Solution 担当者 ([Adobe Professional Servicesチームメンバー](https://opensource.adobe.com/acrobat-sign/signgov/gstarted.html#password)) をクリックします。

**_スコープ_**

* [!DNL aggrement_read]
* [!DNL aggrement_write]
* [!DNL aggrement_send]
* [!DNL widget_read]
* [!DNL widget_write]
* [!DNL workflow_read]
* [!DNL offline_access]

担当者が資格情報を生成し、共有します。 次の節では、資格情報（クライアント ID とクライアントの秘密鍵）を使用して、AEM FormsをAdobe Acrobat Sign Solutionsと政府機関向けに接続します。

#### 受け取った資格情報を使用してAEM FormsをAdobe Acrobat Sign Solutions for Government に接続します

1. を開きます。 `re-direct URL` ブラウザーに表示されます。 を作成し、 `re-direct URL` の最後の段階で [AEMインスタンスでのリダイレクト URL の作成](#create-redirect-url) 」セクションに入力します。

1. **[!UICONTROL Adobe Sign 設定を作成]**&#x200B;ページの「**[!UICONTROL 一般]**」タブで、設定の&#x200B;**[!UICONTROL 名前]**&#x200B;を指定して「**[!UICONTROL 次へ]**」をタップします。必要に応じて&#x200B;**[!UICONTROL タイトル]**&#x200B;を指定し、設定の&#x200B;**[!UICONTROL サムネ―ル]**&#x200B;を参照して選択することもできます。「**[!UICONTROL 次へ]**」をクリックします。

1. 内 **[!UICONTROL 設定]** タブ **[!UICONTROL Adobe Sign設定を作成]** ページ、 **[!UICONTROL ソリューションを選択]** オプション、選択 [!DNL Adobe Acrobat Sign Solutions for Government].

   ![Adobe Acrobat Sign Solutions for Government](assets/adobe-sign-for-govt.png)

1. 内 **[!UICONTROL 電子メール]** 「 」フィールドで、Adobe Acrobat Sign Solutions for Government アカウントに関連付けられた電子メールアドレスを指定します。

1. この **[!UICONTROL OAuth URL]** フィールドは、Adobe Signデータベースシャードを指定します。 「 」フィールドにはデフォルトの URL が入力されます。 URL は変更しないでください。

1. Adobe Acrobat Signが政府機関向けのソリューション担当者 ([Adobe Professional Servicesチームメンバー]) を [**[!UICONTROL クライアント ID]** および **[!UICONTROL クライアント秘密鍵]**].

1. を選択します。 **[!UICONTROL 添付ファイルに対してAdobe Acrobat Signを有効にする]** アダプティブフォームに添付されたファイルを、対応する [!DNL Adobe Acrobat Sign] ドキュメントが署名用に送信されました。

1. 「**[!UICONTROL Adobe Sign に接続]**」をタップします。資格情報の入力画面が表示されたら、[!DNL Adobe Acrobat Sign] アプリケーションの作成時に使用したユーザー名とパスワードを入力します。`your developer account` へのアクセスを確認するメッセージが表示されたら、「**[!UICONTROL アクセスを許可]**」をクリックします。資格情報が正しく、[!DNL AEM Forms] が [!DNL Adobe Acrobat Sign] 開発者アカウントにアクセスできるようにした場合は、次のような成功メッセージが表示されます。

   ![Adobe Acrobat Sign Cloud 設定成功](assets/adobe-sign-cloud-configuration-success.png)

   <!-- > When prompted for credentials, provide username and password of the account used while creating [!DNL Adobe Acrobat Sign] application. When asked to confirm access for `your developer account`, Click **[!UICONTROL Allow Access]**. -->

1. 「**[!UICONTROL 作成]**」をタップして、 設定を作成します。

1. 設定を選択し、「**[!UICONTROL 公開]**」をクリックします&#x200B;**[!UICONTROL 。]**&#x200B;これにより、設定が対応するパブリッシュ環境にレプリケートされます。

1. 開発者、ステージ、実稼働用のインスタンス（残っているいずれか）で上記の手順をすべて繰り返し、お使いの環境用に [!DNL Adobe Acrobat Sign Solutions for Government] を [!DNL AEM Forms] で設定する作業を完了します。

次に、以下を実行できます。 [アダプティブフォームでのAdobe Acrobat Signフィールドの追加を使用します。](working-with-adobe-sign.md) または [AEM Workflow](/help/forms/aem-forms-workflow-step-reference.md#sign-document-step-sign-document-step). Cloud Service設定に使用する設定コンテナを、有効になっているすべてのアダプティブFormsに追加してください。 [!DNL Adobe Acrobat Sign]. 設定コンテナは、アダプティブフォームのプロパティから指定できます。

## （AEM ワークフローのみ）[!DNL Adobe Acrobat Sign]スケジューラーを設定して、署名ステータスを同期します  {#configure-adobe-sign-scheduler-to-sync-the-signing-status}

[!DNL Adobe Acrobat Sign] ワークフローステップを使用してアダプティブフォームに署名する場合、ワークフローステップの設定に応じて、フォームを順番に署名者に渡すか、すべての署名者に同時送信することができます。[!DNL Adobe Acrobat Sign] が有効なアダプティブフォームは、すべての署名者が署名プロセスを完了した後にのみ、Experience Manager Forms サーバーに送信されます。

デフォルトでは、[!DNL Adobe Acrobat Sign] スケジューラーサービスは、24 時間ごとに署名者の応答を確認（ポーリング）します。現在の環境に合わせて、このデフォルト値を変更することができます。

デフォルトの間隔を変更するには、 [cron 式](https://en.wikipedia.org/wiki/Cron#CRON_expression) の **sign.status.exp** プロパティ **Adobe Acrobat Sign Configuration Service** 設定。

例えば、毎日午前 0 時に設定サービスを実行するには、 **sign.status.exp** プロパティ **Adobe Acrobat Sign Configuration Service** 指定する設定 `0 0 0 1/1 * ? *`. 次の JSON ファイルに、設定サービスを毎日午前 0 時に実行するサンプルを示します。

```json
{
  "sign.status.exp":"0 0 0 1/1 * ? *"
}
```

設定の値をセットするには、[AEM SDK を使用して OSGi 設定を生成](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/deploying/configuring-osgi.html?lang=ja#generating-osgi-configurations-using-the-aem-sdk-quickstart)し、Cloud Service インスタンスに[設定をデプロイ](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/deploy-code.html?lang=ja#deployment-process)します。


## 関連記事 {#related-articles}

* [アダプティブフォームでのAdobe Acrobat Signの使用](working-with-adobe-sign.md)

* [アダプティブFormsでのAdobe Acrobat Signの使用に関するベストプラクティス](https://medium.com/adobetech/using-adobe-sign-to-e-sign-an-adaptive-form-heres-the-best-way-to-do-it-dc3e15f9b684)
