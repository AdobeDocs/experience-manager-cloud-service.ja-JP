---
title: メールサービスの OAuth2 サポート
description: Adobe Experience Manager as a Mail Service の Oauth2 サポート
exl-id: 93e7db8b-a8bf-4cc7-b7f0-cda481916ae9
source-git-commit: 5ad33f0173afd68d8868b088ff5e20fc9f58ad5a
workflow-type: tm+mt
source-wordcount: '679'
ht-degree: 45%

---

# メールサービスの OAuth2 サポート {#oauth2-support-for-the-mail-service}

AEM as a Cloud Serviceは、組織が安全な電子メール要件に準拠できるように、OAuth2 の統合メールサービスをサポートしています。

Oauth は複数のメールプロバイダーに対して設定できます。Microsoft® Office 365 Outlook で OAuth2 を介して認証するようにAEM Mail Service を設定する手順を以下に示します。 他のベンダーも同様の方法で設定できます。

AEM as a Cloud Service のメールサービスの詳細については、[メールの送信](/help/implementing/developing/introduction/development-guidelines.md#sending-email)を参照してください。

## Microsoft® Outlook {#microsoft-outlook}

1. [https://portal.azure.com/](https://portal.azure.com/)に移動し、ログインします。
1. を検索 **Azure Active Directory** 検索バーで、結果をクリックします。 または、[https://portal.azure.com/#blade/Microsoft_AAD_IAM/ActiveDirectoryMenuBlade/Overview](https://portal.azure.com/#blade/Microsoft_AAD_IAM/ActiveDirectoryMenuBlade/Overview) を直接参照することもできます。
1. クリック **アプリの登録** > **新規登録**.

   ![アプリ登録プロセスを開始](assets/oauth-outlook1.png)

1. 必要に応じて情報を入力し、「**登録**」をクリックします。
1. 新しく作成されたアプリに移動し、「 」を選択します。 **API 権限**.
1. クリック **権限を追加** > **グラフ権限** > **委任された権限**.
1. アプリに対して以下の権限を選択し、「**権限を追加**」をクリックします。
   * `https://outlook.office.com/SMTP.Send`
   * `https://graph.microsoft.com/Mail.Read`
   * `https://graph.microsoft.com/Mail.Send`
   * `https://graph.microsoft.com/User.Read`
   * `openid`
   * `offline_access`
   * `email`
   * `profile`
1. に移動します。 **認証** > **プラットフォームの追加** > **Web**、および **リダイレクト URL** 「 」セクションで、次の URL を追加します。1 つはスラッシュ付きで、もう 1 つはスラッシュなしです。
   * `http://localhost/`
   * `http://localhost`
1. 各 URL を追加した後で「**設定**」を押し、必要に応じて設定を指定します.
1. 次に、**証明書とシークレット**&#x200B;に移動し、「**新しいクライアントシークレット**」をクリックし、画面上の手順に従ってシークレットを作成します。このシークレットは後で使用するため、必ずメモしてください.
1. 押す **概要** 左側のウィンドウで、 **アプリケーション（クライアント） ID** および **ディレクトリ（テナント） ID** 後で使用する場合。

まとめるには、次の情報を使用して、AEM側で Mail サービスの OAuth2 を設定します。

* 認証 URL。テナント ID を使用して構築されます。 次の形式で記述します。 `https://login.microsoftonline.com/<tenantID>/oauth2/v2.0/authorize`
* トークン URL。テナント ID を使用して構築されます。 次の形式で記述します。 `https://login.microsoftonline.com/<tenantID>/oauth2/v2.0/token`
* 更新 URL。テナント ID を使用して構築されます。 次の形式で記述します。 `https://login.microsoftonline.com/<tenantID>/oauth2/v2.0/token`
* クライアント ID
* クライアント秘密鍵

### 更新トークンの生成 {#generating-the-refresh-token}

次に、次の手順で OSGi 設定の一部である更新トークンを生成します。

1. 置き換えた後、ブラウザーで次の URL を開きます `clientID` および `tenantID` アカウントに固有の値を使用： `https://login.microsoftonline.com/%3ctenantID%3e/oauth2/v2.0/authorize?client_id=%3cclientId%3e&response_type=code&redirect_uri=http://localhost&response_mode=query&scope=https://outlook.office.com/SMTP.Send%20email%20openid%20profile%20offline_access&state=12345`.
1. 尋ねられたら、許可を許可します。
1. URL は新しい場所にリダイレクトします。次の形式で構築されます。 `http://localhost/?code=<code>&state=12345&session_state=4f984c6b-cc1f-47b9-81b2-66522ea83f81#`.
1. 上記の例の `<code>` の値をコピーします.
1. 次の cURL コマンドを使用して、 refreshToken を取得します。tenantID、clientID、clientSecret を、アカウントの値と、 `<code>`:

   ```
   curl --location --request POST 'https://login.microsoftonline.com/<tenantId>/oauth2/v2.0/token' \
   --header 'Content-Type: application/x-www-form-urlencoded' \
   --header 'Cookie: buid=0.ARgAep0nU49DzUGmoP2wnvyIkcQjsx26HEpOnvHS0akqXQgYAAA.AQABAAEAAAD--DLA3VO7QrddgJg7Wevry9XPJSKbGVlPt5NWYxLtTl3K1W0LwHXelrffApUo_K02kFrkvmGm94rfBT94t25Zq4bCd5IM3yFOjWb3V22yDM7-rl112sLzbBQBRCL3QAAgAA; esctx=AQABAAAAAAD--DLA3VO7QrddgJg7Wevr4a8wBjYcNbBXRievdTOd15caaeAsQdXeBAQA3tjVQaxmrOXFGkKaE7HBzsJrzA-ci4RRpor-opoo5gpGLh3pj_iMZuqegQPEb1V5sUVQV8_DUEbBv5YFV2eczS5EAhLBAwAd1mHx6jYOL8LwZNDFvd2-MhVXwPd6iKPigSuBxMogAA; x-ms-gateway-slice=estsfd; stsservicecookie=estsfd; fpc=Auv6lTuyAP1FuOOCfj9w0U_5vR5dAQAAALDXP9gOAAAAwIpkkQEAAACT2T_YDgAAAA' \
   --data-urlencode 'client_id=<clientID>' \
   --data-urlencode 'scope=https://outlook.office.com/SMTP.Send https://graph.microsoft.com/Mail.Read https://graph.microsoft.com/Mail.Send https://graph.microsoft.com/User.Read email openid profile offline_access' \
   --data-urlencode 'redirect_uri=http://localhost' \
   --data-urlencode 'grant_type=authorization_code' \
   --data-urlencode 'client_secret=<clientSecret>' \
   --data-urlencode 'code=<code>'
   ```

1. refreshToken と accessToken をメモしておきます。

### トークンの検証 {#validating-the-tokens}

AEM 側で Oauth を設定する前に、次の手順で accessToken と refreshToken の両方を検証してください。

1. 次の curl を使用して、前の手順で作成した refreshToken を使用し、 accessToken を生成します。その際、 `<client_id>`,`<client_secret>`、および `<refreshToken>`:

   ```
   curl --location --request POST 'https://login.microsoftonline.com/<tenetId>/oauth2/v2.0/token' \
   --header 'Content-Type: application/x-www-form-urlencoded' \
   --header 'Cookie: buid=0.ARgAep0nU49DzUGmoP2wnvyIkcQjsx26HEpOnvHS0akqXQgYAAA.AQABAAEAAAD--DLA3VO7QrddgJg7Wevry9XPJSKbGVlPt5NWYxLtTl3K1W0LwHXelrffApUo_K02kFrkvmGm94rfBT94t25Zq4bCd5IM3yFOjWb3V22yDM7-rl112sLzbBQBRCL3QAAgAA; esctx=AQABAAAAAAD--DLA3VO7QrddgJg7Wevr4a8wBjYcNbBXRievdTOd15caaeAsQdXeBAQA3tjVQaxmrOXFGkKaE7HBzsJrzA-ci4RRpor-opoo5gpGLh3pj_iMZuqegQPEb1V5sUVQV8_DUEbBv5YFV2eczS5EAhLBAwAd1mHx6jYOL8LwZNDFvd2-MhVXwPd6iKPigSuBxMogAA; x-ms-gateway-slice=estsfd; stsservicecookie=estsfd; fpc=Auv6lTuyAP1FuOOCfj9w0U_IezHLAQAAAPeNSdgOAAAA' \
   --data-urlencode 'client_id=<client_id>' \
   --data-urlencode 'scope=https://outlook.office.com/SMTP.Send https://graph.microsoft.com/Mail.Read https://graph.microsoft.com/Mail.Send https://graph.microsoft.com/User.Read email openid profile offline_access' \
   --data-urlencode 'redirect_uri=http://localhost' \
   --data-urlencode 'grant_type=refresh_token' \
   --data-urlencode 'client_secret=<client_secret>' \
   --data-urlencode 'refresh_token=<refreshToken>'
   ```

1. accessToken を使用してメールを送信し、正しく機能しているかどうかを確認できます。

>[!NOTE]
>
> [この場所](https://learn.microsoft.com/en-us/azure/active-directory/develop/v2-oauth2-auth-code-flow)から Postman API コレクションを取得できます。
>
> MSFT OAuth のドキュメントを参照してください。 [ここ](https://learn.microsoft.com/ja-jp/exchange/client-developer/legacy-protocols/how-to-authenticate-an-imap-pop-smtp-application-by-using-oauth) を参照してください。

### AEM as a Cloud Service との統合 {#integration-with-aem-as-a-cloud-service}

1. `com.day.cq.mailer.oauth.impl.OAuthConfigurationProviderImpl.cfg.json` という名前の OSGI プロパティファイルを `/apps/<my-project>/osgiconfig/config` の下に次の構文で作成します。

   ```
   {
       authUrl: "<Authorization Url>",
       tokenUrl: "<Token Url>",
       clientId: "<clientID>",
       clientSecret: "$[secret:SECRET_SMTP_OAUTH_CLIENT_SECRET]",
       scopes: [
          "scope1",
          "scope2"
       ],
       authCodeRedirectUrl: "http://localhost",
       refreshUrl: "<Refresh token Url>",
       refreshToken: "$[secret:SECRET_SMTP_OAUTH_REFRESH_TOKEN]"
   }
   ```

1. 次の項目に入力： `authUrl`, `tokenUrl`、および `refreshURL` 前の節で説明したように、これらを構築します。
1. 次のスコープを設定に追加します。
   * `https://outlook.office.com/SMTP.Send`
   * `https://graph.microsoft.com/Mail.Read`
   * `https://graph.microsoft.com/Mail.Send`
   * `https://graph.microsoft.com/User.Read`
   * `openid`
   * `offline_access`
   * `email`
   * `profile`
1. 次の構文で、OSGI プロパティファイル`called com.day.cq.mailer.DefaultMailService.cfg.json`を  `/apps/<my-project>/osgiconfig/config` を次の構文で置き換えます。 The `smtp.host` および `smtp.port` の値は、詳細なネットワーク設定を反映します。詳しくは、 [電子メールサービスのチュートリアル](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/networking/examples/email-service.html?lang=en).

   ```
   {
    "smtp.host": "$[env:AEM_PROXY_HOST;default=proxy.tunnel]",
    "smtp.user": "<user account that logged into get the oauth tokens>",
    "smtp.password": "value not used",
    "smtp.port": 30465,
    "from.address": "<from address used for sending>",
    "smtp.ssl": false,
    "smtp.starttls": true,
    "smtp.requiretls": true,
    "debug.email": false,
    "oauth.flow": true
   }
   ```

1. Outlook の場合、`smtp.host` 設定値は `smtp.office365.com` です
1. 実行時に、[ここ](/help/implementing/deploying/configuring-osgi.md#setting-values-via-api)で説明しているように、Cloud Manager 変数 API を使用して `refreshToken values` および `clientSecret` シークレットを渡します。変数 `SECRET_SMTP_OAUTH_REFRESH_TOKEN` と `SECRET_SMTP_OAUTH_CLIENT_SECRET` の値を定義する必要があります。

### トラブルシューティング {#troubleshooting}

メールサービスが正しく動作していない場合は、 `refreshToken` 前述のように、Cloud Manager API を介して新しい値を渡します。 新しい値がデプロイされるまで数分かかります。
