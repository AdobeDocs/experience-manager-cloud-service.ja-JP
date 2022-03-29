---
title: Adobe Sign と AEM Forms の統合方法
description: ' [!DNL AEM Forms]  as a Cloud Service 用に Adobe Sign を設定する方法'
feature: Adaptive Forms
role: User
level: Intermediate
exl-id: 609c3072-1c3d-43fa-898a-b4e62db8483b
source-git-commit: 7163eb2551f5e644f6d42287a523a7dfc626c1c4
workflow-type: tm+mt
source-wordcount: '983'
ht-degree: 100%

---

# [!DNL Adobe Sign] の [!DNL AEM Forms] as a Cloud Service との統合  {#integrate-adobe-sign-with-aem-forms}

[!DNL Adobe Sign] により、アダプティブフォームの電子サインワークフローを有効にできます。電子サインを使用すると、法務、販売、給与、人事管理など、様々な分野におけるドキュメント処理ワークフローが改善されます。

[!DNL Adobe Sign] とアダプティブフォームの一般的なシナリオでは、ユーザーがアダプティブフォームに入力してサービスを申し込みます。例えば、クレジットカードの申込フォームや住民サービスフォームなどです。ユーザーが申込フォームの入力、送信、署名を行うと、サービスプロバイダーにそのフォームが送信され、追加の処理が実行されます。サービスプロバイダーは受信した申込フォームを確認し、[!DNL Adobe Sign] を使用して申請を承認します。同様のシナリオで電子サインワークフローを有効にするには、[!DNL Adobe Sign] を [!DNL AEM Forms] に統合します。

[!DNL AEM Forms] で [!DNL Adobe Sign] を使用するには、AEM Cloud Services で [!DNL Adobe Sign] を設定します。

## 前提条件 {#prerequisites}

[!DNL Adobe Sign] を [!DNL AEM Forms] に統合するには、以下のものが必要になります。

* 有効な [Adobe Sign 開発者アカウント](https://acrobat.adobe.com/jp/ja/sign/developer-form.html)。
* [Adobe Sign API アプリケーション](https://www.adobe.io/apis/documentcloud/sign/docs.html#!adobedocs/adobe-sign/master/gstarted/create_app.md)。
* [!DNL Adobe Sign] API アプリケーションの資格情報（クライアント ID およびクライアントの秘密鍵）。
* オーサーインスタンスとパブリッシュインスタンスには、[同一の暗号キー](https://experienceleague.adobe.com/docs/experience-manager-65/administering/security/security-checklist.html?lang=ja#make-sure-you-properly-replicate-encryption-keys-when-needed)を使用します。
* （Government ID に基づいた認証の場合のみ）[Government ID 認証による認証方法](https://helpx.adobe.com/jp/sign/using/adobesign-authentication-government-id.html#AuditReport)を有効にします。

## [!DNL Adobe Sign] での [!DNL AEM Forms] の設定 {#configure-adobe-sign-with-aem-forms}

上記の前提条件の準備が完了したら、以下の手順により、オーサーインスタンス上の [!DNL AEM Forms] を使用して [!DNL Adobe Sign] を設定します。

1. AEM Forms のオーサーインスタンスで、**[!UICONTROL ツール]** ![ハンマー](assets/hammer.png)／**[!UICONTROL 一般]**／**[!UICONTROL 設定ブラウザー]**&#x200B;に移動します。
1. **[!UICONTROL 設定ブラウザー]**&#x200B;ページで「**[!UICONTROL 作成]**」をタップします。
1. **[!UICONTROL 設定を作成]**&#x200B;ダイアログで、設定の&#x200B;**[!UICONTROL タイトル]**&#x200B;を指定し、「**[!UICONTROL クラウド設定]**」を有効にして「**[!UICONTROL 作成]**」をタップします。これにより、Cloud Services 用の設定コンテナが作成されます。フォルダー名にスペースが含まれていないことを確認します。
1. **[!UICONTROL ツール]** ![ハンマー](assets/hammer.png)／**[!UICONTROL Cloud Services]**／**[!UICONTROL Adobe Sign]** に移動し、上記の手順で作成した設定コンテナを開くします。

   >[!NOTE]
   >
   >アダプティブフォームを作成する際に、**[!UICONTROL 設定コンテナ]**&#x200B;フィールドにコンテナ名を指定します。

1. 設定ページで「**[!UICONTROL 作成]**」をタップして、AEM Forms 内に [!DNL Adobe Sign] の設定を作成します。
1. **[!UICONTROL Adobe Sign 設定を作成]**&#x200B;ページの「**[!UICONTROL 一般]**」タブで、設定の&#x200B;**[!UICONTROL 名前]**&#x200B;を指定して「**[!UICONTROL 次へ]**」をタップします。必要に応じて&#x200B;**[!UICONTROL タイトル]**&#x200B;を指定し、設定の&#x200B;**[!UICONTROL サムネ―ル]**&#x200B;を参照して選択することもできます。

1. 現在のブラウザーウィンドウの URL をメモ帳にコピーします。この URL は、後の手順で [!DNL AEM Forms] と [!DNL Adobe Sign] アプリケーションを設定する際に必要です。

1. 以下の手順に従って、[!DNL Adobe Sign] アプリケーションの OAuth 設定を指定します。

   1. ブラウザーウィンドウを開き、[!DNL Adobe Sign] 開発者アカウントにログインします。
   1. [!DNL AEM Forms] 用に設定されているアプリケーションを選択し、「**[!UICONTROL アプリケーションの OAuth を設定]**」をタップします。
   1. 上記の手順でコピーした URL を「**[!UICONTROL リダイレクト URL]**」ボックスに追加して「**[!UICONTROL 保存]**」をクリックします。
   1. [!DNL Adobe Sign] アプリケーションに対して以下の OAuth 設定を有効にして、「**[!UICONTROL 保存]**」をクリックします。
   * [!DNL aggrement_read]
   * [!DNL aggrement_write]
   * [!DNL aggrement_send]
   * [!DNL widget_read]
   * [!DNL widget_write]
   * [!DNL workflow_read]

   [!DNL Adobe Sign] アプリケーション用に OAuth 設定を構成してキーを取得するための詳しい手順については、開発者用ドキュメントの[アプリケーション用に OAuth 設定を構成する](https://www.adobe.io/apis/documentcloud/sign/docs.html#!adobedocs/adobe-sign/master/gstarted/configure_oauth.md)を参照してください。

   ![OAuth 設定](assets/oauthconfig_new.png)

1. **[!UICONTROL Adobe Sign 設定を作成]**&#x200B;ページに戻ります。「**[!UICONTROL 設定]**」タブで、「**[!UICONTROL OAuth URL]**」フィールドにデフォルトの URL が表示されます。URL は次のような形式になります。

   `https://<shard>/public/oAuth/v2`

   次に例を示します。
   `https://secure.na1.echosign.com/public/oauth/v2`

   各パラメーターの意味は次のとおりです。

   **na1** は、デフォルトのデータベースシャードを参照します。データベースシャードの値を更新することができます。[!DNL Adobe Sign] クラウド設定で、[正しいシャード](https://helpx.adobe.com/jp/sign/using/identify-account-shard.html)をポイントしていることを確認します。

   別の [!DNL Adobe Sign] 設定を Adobe Experience Manager の機能またはコンポーネント用に作成する場合は、すべての [!DNL Adobe Sign] クラウド設定が同じシャードをポイントしていることを確認してください。

1. **[!UICONTROL クライアント ID]**（アプリケーション ID）と&#x200B;**[!UICONTROL クライアントの秘密鍵]**&#x200B;の値を指定します。前の手順で作成した Adobe Sign アプリケーションのクライアント ID とクライアントの秘密鍵を使用します。

1. 「**[!UICONTROL 添付ファイルの Adobe Sign を有効にする]**」オプションを選択すると、アダプティブフォームに添付されているファイルが、署名用に送信された対応する [!DNL Adobe Sign] ドキュメントに添付されます。

1. 「**[!UICONTROL Adobe Sign に接続]**」をタップします。資格情報の入力画面が表示されたら、[!DNL Adobe Sign] アプリケーションの作成時に使用したユーザー名とパスワードを入力します。`your developer account` へのアクセスを確認するメッセージが表示されたら、「**[!UICONTROL アクセスを許可]**」をクリックします。資格情報が正しく、[!DNL AEM Forms] が [!DNL Adobe Sign] 開発者アカウントにアクセスできるようにした場合は、次のような成功メッセージが表示されます。

   ![Adobe Sign クラウド設定成功](assets/adobe-sign-cloud-configuration-success.png)

1. 「**[!UICONTROL 作成]**」をタップして、[!DNL Adobe Sign] 設定を作成します。

1. 設定を選択し、「**[!UICONTROL 公開]**」をクリックします&#x200B;**[!UICONTROL 。]**&#x200B;これにより、対応するパブリッシュ環境に設定が複製されます。

1. 開発者、ステージ、実稼働用のインスタンス（残っているいずれか）で上記の手順をすべて繰り返し、お使いの環境用に [!DNL Adobe Sign] を [!DNL AEM Forms] で設定する作業を完了します。

これで、[アダプティブフォーム](working-with-adobe-sign.md)に Adobe Sign フィールドを追加する機能を使用できるようになりました。[!DNL Adobe Sign] 用に有効化するすべてのアダプティブフォームに、Cloud Service に使用する設定コンテナを追加してください。設定コンテナは、アダプティブフォームのプロパティから指定できます。

## （AEM ワークフローのみ）[!DNL Adobe Sign]スケジューラーを設定して、署名ステータスを同期します  {#configure-adobe-sign-scheduler-to-sync-the-signing-status}

[!DNL Adobe Sign] ワークフローステップを使用してアダプティブフォームに署名する場合、ワークフローステップの設定に応じて、フォームを順番に署名者に渡すか、すべての署名者に同時送信することができます。[!DNL Adobe Sign] が有効なアダプティブフォームは、すべての署名者が署名プロセスを完了した後にのみ、Experience Manager Forms サーバーに送信されます。

デフォルトでは、[!DNL Adobe Sign] スケジューラーサービスは、24 時間ごとに署名者の応答を確認（ポーリング）します。現在の環境に合わせて、このデフォルト値を変更することができます。

デフォルトの間隔を変更するには、**Adobe Sign 設定サービス**&#x200B;の設定の **sign.status.exp** プロパティに [cron 式](https://en.wikipedia.org/wiki/Cron#CRON_expression)を指定します。

例えば、毎日午前 0 時に設定サービスを実行するには、**Adobe Sign 設定サービス**&#x200B;設定の **sign.status.exp** プロパティを `0 0 0 1/1 * ? *` に指定します。次の JSON ファイルに、設定サービスを毎日午前 0 時に実行するサンプルを示します。

```json
{
  "sign.status.exp":"0 0 0 1/1 * ? *"
}
```

設定の値をセットするには、[AEM SDK を使用して OSGi 設定を生成](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/deploying/configuring-osgi.html?lang=ja#generating-osgi-configurations-using-the-aem-sdk-quickstart)し、Cloud Service インスタンスに[設定をデプロイ](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/deploy-code.html?lang=ja#deployment-process)します。

<!-- , perform the following steps:

1. Log in to [!DNL AEM Forms] Server with admin credentials and navigate to **[!UICONTROL Tools]** &gt;**[!UICONTROL Operations]** &gt; **[!UICONTROL Web Console]**.

   You can also open the following URL in a browser window:
   `https://server/system/console/configMgr`

1. Locate and open the **[!UICONTROL Adobe Sign Configuration Service]** option. Specify a [cron expression](https://en.wikipedia.org/wiki/Cron#CRON_expression) in the **Status Update Scheduler Expression** field and click **Save**. For example, to run the configuration service daily at 00:00 am, specify `0 0 0 1/1 * ? *` in the **Status Update Scheduler Expression** field.

Default interval to sync status of [!DNL Adobe Sign] is now changed. -->

## 関連記事 {#related-articles}

* [アダプティブフォームでの Adobe Sign の使用](working-with-adobe-sign.md)

* [アダプティブフォームでの Adobe Sign 使用に関するベストプラクティス](https://medium.com/adobetech/using-adobe-sign-to-e-sign-an-adaptive-form-heres-the-best-way-to-do-it-dc3e15f9b684)
