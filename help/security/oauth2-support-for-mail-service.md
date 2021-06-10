---
title: メールサービスのOAuth2サポート
description: Adobe Experience Manager as a Mail ServiceのOauth2サポート
source-git-commit: b46062697b25aa8d3f215a8a4249f5203bec268e
workflow-type: tm+mt
source-wordcount: '674'
ht-degree: 0%

---


# OAuth2によるメールサービスのサポート{#oauth2-support-for-the-mail-service}

AEM as a Cloud Serviceは、組織が安全な電子メール要件に準拠できるように、OAuth2で統合メールサービスをサポートしています。

OAuthは複数のEメールプロバイダーに対して設定できます。 Microsoft Office 365 OutlookでOAuth2を介して認証するようにAEM Mail Serviceを設定する手順を、以下に示します。 他のベンダーも同様の方法で設定できます。

AEM as a Email Serviceの詳細については、「[電子メールの送信](/help/implementing/developing/introduction/development-guidelines.md#sending-email)」を参照してください。

## Microsoft Outlook {#microsoft-outlook}

1. [https://portal.azure.com/](https://portal.azure.com/)に移動し、ログインします。
1. 検索バーで&#x200B;**Azure Active Directory**&#x200B;を検索し、結果をクリックします。 または、[https://portal.azure.com/#blade/Microsoft_AAD_IAM/ActiveDirectoryMenuBlade/Overview](https://portal.azure.com/#blade/Microsoft_AAD_IAM/ActiveDirectoryMenuBlade/Overview)を直接参照することもできます。
1. **アプリの登録** - **新しい登録**&#x200B;をクリックします。

   ![](assets/oauth-outlook1.png)

1. 必要に応じて情報を入力し、**登録**&#x200B;をクリックします。
1. 新しく作成されたアプリに移動し、**API権限**&#x200B;を選択します。
1. **権限**&#x200B;を追加 — **グラフ権限** - **委任権限**&#x200B;に移動します。
1. アプリに対して以下の権限を選択し、「**権限を追加**」をクリックします。
   * `SMTP.Send`
   * `Mail.Read`
   * `Mail.Send`
   * `openid`
   * `offline_access`
1. **認証** - **プラットフォーム** - **Web**&#x200B;を追加し、「**リダイレクトURL**」セクションで、次のURLを1つ（スラッシュなし）追加します。
   * `http://localhost/`
   * `http://localhost`
1. 各URLを追加した後、**Configure**&#x200B;を押し、必要に応じて設定を指定します
1. 次に、「**証明書とシークレット**」に移動し、「**新しいクライアントシークレット**」をクリックし、画面の手順に従ってシークレットを作成します。 後で使用するために、必ずこの秘密を書き留めてください
1. 左側のウィンドウで&#x200B;**Overview**&#x200B;を押し、後で使用するために、**Application (client) ID**&#x200B;および&#x200B;**Directory (tenant) ID**&#x200B;の値をコピーします。

まとめるには、次の情報を使用して、AEM側のMailサービスのOAuth2を設定する必要があります。

* 認証URL。テナントIDを使用して構築されます。 次の形式になります。`https://login.microsoftonline.com/<tenantID>/oauth2/v2.0/authorize`
* トークンURL。テナントIDを使用して構築されます。 次の形式になります。`https://login.microsoftonline.com/<tenantID>/oauth2/v2.0/token`
* 更新URL。テナントIDを使用して構築されます。 次の形式になります。`https://login.microsoftonline.com/<tenantID>/oauth2/v2.0/token`
* クライアントID
* クライアント秘密鍵

### 更新トークン{#generating-the-refresh-token}の生成

次に、更新トークンを生成する必要があります。これは、後続の手順でOSGi設定に含まれます。

次の手順に従って実行できます。

1. `clientID`と`tenantID`を自分のアカウントに固有の値に置き換えてから、ブラウザーで次のURLを開きます。`https://login.microsoftonline.com/<tenantID>/oauth2/v2.0/authorize?client_id=<clientId>&response_type=code&redirect_uri=http://localhost&response_mode=query&scope=https%3A%2F%2Foutlook.office365.com%2FSMTP.Send%20EWS.AccessAsUser.All%20https%3A%2F%2Foutlook.office365.com%2FSMTP.Send%20https%3A%2F%2Foutlook.office365.com%2FMail.Read%20https%3A%2F%2Foutlook.office365.com%2FMail.Send%20openid%20offline_access&state=12345`
1. 要求時に権限を許可
1. URLは、新しい場所にリダイレクトされます。この場所は次の形式で構成されます。`http://localhost/?code=<code>&state=12345&session_state=4f984c6b-cc1f-47b9-81b2-66522ea83f81#`
1. 上記の例の`<code>`の値をコピーします
1. 次のcURLコマンドを使用して、 refreshTokenを取得します。 tenantID、clientID、clientSecretを、アカウントの値と`<code>`の値で置き換える必要があります。

   `curl --location --request POST 'https://login.microsoftonline.com/<tenantId>/oauth2/v2.0/token' \
--header 'Content-Type: application/x-www-form-urlencoded' \
--header 'Cookie: buid=0.ARgAep0nU49DzUGmoP2wnvyIkcQjsx26HEpOnvHS0akqXQgYAAA.AQABAAEAAAD--DLA3VO7QrddgJg7Wevry9XPJSKbGVlPt5NWYxLtTl3K1W0LwHXelrffApUo_K02kFrkvmGm94rfBT94t25Zq4bCd5IM3yFOjWb3V22yDM7-rl112sLzbBQBRCL3QAAgAA; esctx=AQABAAAAAAD--DLA3VO7QrddgJg7Wevr4a8wBjYcNbBXRievdTOd15caaeAsQdXeBAQA3tjVQaxmrOXFGkKaE7HBzsJrzA-ci4RRpor-opoo5gpGLh3pj_iMZuqegQPEb1V5sUVQV8_DUEbBv5YFV2eczS5EAhLBAwAd1mHx6jYOL8LwZNDFvd2-MhVXwPd6iKPigSuBxMogAA; x-ms-gateway-slice=estsfd; stsservicecookie=estsfd; fpc=Auv6lTuyAP1FuOOCfj9w0U_5vR5dAQAAALDXP9gOAAAAwIpkkQEAAACT2T_YDgAAAA' \
--data-urlencode 'client_id=<clientID>' \
--data-urlencode 'scope=https://outlook.office365.com/SMTP.Send https://outlook.office365.com/Mail.Read https://outlook.office365.com/Mail.Send openid' \
--data-urlencode 'redirect_uri=http://localhost' \
--data-urlencode 'grant_type=authorization_code' \
--data-urlencode 'client_secret=<clientSecret>' \
--data-urlencode 'code=<code>'`

1. refreshTokenとaccessTokenをメモしておきます。

### トークンの検証{#validating-the-tokens}

AEM側でOAuthを設定する前に、次の手順でaccessTokenとrefreshTokenの両方を検証してください。

1. 前の手順で生成したrefreshTokenを使用して、 accessTokenを生成します。 次のcurlを使用してこれを実現できます。`<client_id>`、`<client_secret>`および`<refreshToken>`の値を置き換えます。

   `curl --location --request POST 'https://login.microsoftonline.com/<tenetId>/oauth2/v2.0/token' \
--header 'Content-Type: application/x-www-form-urlencoded' \
--header 'Cookie: buid=0.ARgAep0nU49DzUGmoP2wnvyIkcQjsx26HEpOnvHS0akqXQgYAAA.AQABAAEAAAD--DLA3VO7QrddgJg7Wevry9XPJSKbGVlPt5NWYxLtTl3K1W0LwHXelrffApUo_K02kFrkvmGm94rfBT94t25Zq4bCd5IM3yFOjWb3V22yDM7-rl112sLzbBQBRCL3QAAgAA; esctx=AQABAAAAAAD--DLA3VO7QrddgJg7Wevr4a8wBjYcNbBXRievdTOd15caaeAsQdXeBAQA3tjVQaxmrOXFGkKaE7HBzsJrzA-ci4RRpor-opoo5gpGLh3pj_iMZuqegQPEb1V5sUVQV8_DUEbBv5YFV2eczS5EAhLBAwAd1mHx6jYOL8LwZNDFvd2-MhVXwPd6iKPigSuBxMogAA; x-ms-gateway-slice=estsfd; stsservicecookie=estsfd; fpc=Auv6lTuyAP1FuOOCfj9w0U_IezHLAQAAAPeNSdgOAAAA' \
--data-urlencode 'client_id=<client_id>' \
--data-urlencode 'scope=https://outlook.office365.com/SMTP.Send https://outlook.office365.com/Mail.Read https://outlook.office365.com/Mail.Send openid' \
--data-urlencode 'redirect_uri=http://localhost' \
--data-urlencode 'grant_type=refresh_token' \
--data-urlencode 'client_secret=<client_secret>' \
--data-urlencode 'refresh_token=<refreshToken>'`

1. accessTokenを使用してメールを送信し、が正しく動作しているかどうかを確認します。

>[!NOTE]
>
> [この場所](https://docs.microsoft.com/en-us/azure/active-directory/develop/v2-oauth2-auth-code-flow)からPostman APIコレクションを取得できます。

### AEM as aCloud Service{#integration-with-aem-as-a-cloud-service}との統合

1. `com.day.cq.mailer.oauth.impl.OAuthConfigurationProviderImpl.cfg.json`という名前のOSGIプロパティファイルを`/apps/<my-project>/osgiconfig/config`の下に次の構文で作成します。

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
       refreshUrl: "<Refresh token Url>",
       refreshToken: "$[secret:SECRET_SMTP_OAUTH_REFRESH_TOKEN]"
   }
   ```

1. 前の節で説明したように、 `authUrl` 、 `tokenUrl` 、 `refreshURL`を作成して入力します。
1. 次のスコープを構成に追加します。
   * `openid`
   * `offline_access`
   * `https://outlook.office365.com/Mail.Send`
   * `https://outlook.office365.com/Mail.Read`
   * `https://outlook.office365.com/SMTP.Send`
1. OSGIプロパティファイル`called com.day.cq.mailer.impl.DefaultMailService.cfg.json`を作成します。
under 
`/apps/<my-project>/osgiconfig/config`  を次の構文に置き換えます。

   ```
   {
    "smtp.host": "<smtp hostname>"
    "smtp.user": "<user account that logged into get the oauth tokens>",
    "smtp.password": "value not used",
    "smtp.port": 587,
    "from.address": "<from address used for sending>"
    "smtp.ssl": false,
    "smtp.starttls": true,
    "smtp.requiretls": true,
    "debug.email": false,
    "oauth.flow": true
   }
   ```

1. Outlookの場合、`smtp.host`設定値は`smtp.office365.com`です
1. 実行時に、[ここ](/help/implementing/deploying/configuring-osgi.md#setting-values-via-api)で説明しているように、Cloud Manager変数APIを使用して`refreshToken values`および`clientSecret`シークレットを渡します。 変数`SECRET_SMTP_OAUTH_REFRESH_TOKEN`と`SECRET_SMTP_OAUTH_CLIENT_SECRET`の値を定義する必要があります。

### トラブルシューティング {#troubleshooting}

メールサービスが正常に動作しない場合は、ほとんどの場合、前述のように`refreshToken`を再生成し、Cloud Manager APIを介して新しい値を渡す必要があります。 新しい値がデプロイされるまで数分かかります。
