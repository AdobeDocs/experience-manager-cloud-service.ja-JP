---
title: メールサービスの OAuth2 サポート
description: Adobe Experience Manager as a Mail Service の Oauth2 サポート
exl-id: 93e7db8b-a8bf-4cc7-b7f0-cda481916ae9
source-git-commit: 4a5967f682d122d20528b1d904590fb82f438fa7
workflow-type: ht
source-wordcount: '674'
ht-degree: 100%

---

# メールサービスの OAuth2 サポート {#oauth2-support-for-the-mail-service}

AEM as a Cloud Service は、組織が安全な電子メール要件に準拠できるように、Oauth2 の統合メールサービスをサポートしています。

Oauth は複数のメールプロバイダーに対して設定できます。Microsoft Office 365 Outlook で Oauth2 による認証を行うように AEM メールサービスを設定する手順を以下に示します。他のベンダーも同様の方法で設定できます。

AEM as a Cloud Service のメールサービスの詳細については、[電子メールの送信](/help/implementing/developing/introduction/development-guidelines.md#sending-email)を参照してください。

## Microsoft Outlook {#microsoft-outlook}

1. [https://portal.azure.com/](https://portal.azure.com/)に移動し、ログインします。
1. 検索バーで **Azure Active Directory** を検索し、結果をクリックします。または、[https://portal.azure.com/#blade/Microsoft_AAD_IAM/ActiveDirectoryMenuBlade/Overview](https://portal.azure.com/#blade/Microsoft_AAD_IAM/ActiveDirectoryMenuBlade/Overview) を直接参照することもできます。
1. **アプリの登録**／**新しい登録**&#x200B;をクリックします。

   ![](assets/oauth-outlook1.png)

1. 必要に応じて情報を入力し、**登録**&#x200B;をクリックします。
1. 新しく作成されたアプリに移動し、**API 権限**&#x200B;を選択します。
1. **権限を追加**／**グラフ権限**／**委任権限**&#x200B;に移動します。
1. アプリに対して以下の権限を選択し、「**権限を追加**」をクリックします。
   * `SMTP.Send`
   * `Mail.Read`
   * `Mail.Send`
   * `openid`
   * `offline_access`
1. **認証**／**プラットフォームを追加** ／**Web**&#x200B;に移動し、**リダイレクト URL**&#x200B;セクションで、次の URL を追加します（スラッシュありで 1 つとスラッシュなしで 1 つ）。
   * `http://localhost/`
   * `http://localhost`
1. 各 URL を追加した後で「**設定**」を押し、必要に応じて設定を指定します
1. 次に、「**証明書とシークレット**」に移動し、「**新しいクライアントシークレット**」をクリックし、画面の手順に従ってシークレットを作成します。このシークレットは後で使用するため、必ずメモしてください
1. 左側のウィンドウで「**概要**」を押し、後で使用するために、「**アプリケーション（クライアント）ID**」および「**ディレクトリ（テナント）ID**」の値をコピーします。

まとめると、次の情報を使用して、AEM 側のメールサービスの Oauth2 を設定する必要があります。

* 認証 URLはテナント ID を使用して構築されます。次の形式になります。`https://login.microsoftonline.com/<tenantID>/oauth2/v2.0/authorize`
* トークン URL はテナント ID を使用して構築されます。次の形式になります。`https://login.microsoftonline.com/<tenantID>/oauth2/v2.0/token`
* 更新 URL はテナント ID を使用して構築されます。次の形式になります。`https://login.microsoftonline.com/<tenantID>/oauth2/v2.0/token`
* クライアント ID
* クライアント秘密鍵

### 更新トークンの生成 {#generating-the-refresh-token}

次に、更新トークンを生成する必要があります。更新トークンは、後続の手順で OSGi 設定の一部になります。

これは、次の手順で行います。

1. `clientID` と `tenantID` を自分のアカウントに固有の値に置き換えてから、ブラウザーで次の URL を開きます。`https://login.microsoftonline.com/<tenantID>/oauth2/v2.0/authorize?client_id=<clientId>&response_type=code&redirect_uri=http://localhost&response_mode=query&scope=https%3A%2F%2Foutlook.office365.com%2FSMTP.Send%20EWS.AccessAsUser.All%20https%3A%2F%2Foutlook.office365.com%2FSMTP.Send%20https%3A%2F%2Foutlook.office365.com%2FMail.Read%20https%3A%2F%2Foutlook.office365.com%2FMail.Send%20openid%20offline_access&state=12345`
1. 権限を要求されたら許可します
1. URL は、新しい場所にリダイレクトされます。この場所は次の形式で構成されます。`http://localhost/?code=<code>&state=12345&session_state=4f984c6b-cc1f-47b9-81b2-66522ea83f81#`
1. 上記の例の `<code>` の値をコピーします
1. 次の cURL コマンドを使用して、 refreshToken を取得します。tenantID、clientID、clientSecret を、アカウントの値と `<code>` の値で置き換える必要があります。

   ```
   curl --location --request POST 'https://login.microsoftonline.com/<tenantId>/oauth2/v2.0/token' \
   --header 'Content-Type: application/x-www-form-urlencoded' \
   --header 'Cookie: buid=0.ARgAep0nU49DzUGmoP2wnvyIkcQjsx26HEpOnvHS0akqXQgYAAA.AQABAAEAAAD--DLA3VO7QrddgJg7Wevry9XPJSKbGVlPt5NWYxLtTl3K1W0LwHXelrffApUo_K02kFrkvmGm94rfBT94t25Zq4bCd5IM3yFOjWb3V22yDM7-rl112sLzbBQBRCL3QAAgAA; esctx=AQABAAAAAAD--DLA3VO7QrddgJg7Wevr4a8wBjYcNbBXRievdTOd15caaeAsQdXeBAQA3tjVQaxmrOXFGkKaE7HBzsJrzA-ci4RRpor-opoo5gpGLh3pj_iMZuqegQPEb1V5sUVQV8_DUEbBv5YFV2eczS5EAhLBAwAd1mHx6jYOL8LwZNDFvd2-MhVXwPd6iKPigSuBxMogAA; x-ms-gateway-slice=estsfd; stsservicecookie=estsfd; fpc=Auv6lTuyAP1FuOOCfj9w0U_5vR5dAQAAALDXP9gOAAAAwIpkkQEAAACT2T_YDgAAAA' \
   --data-urlencode 'client_id=<clientID>' \
   --data-urlencode 'scope=https://outlook.office365.com/SMTP.Send https://outlook.office365.com/Mail.Read https://outlook.office365.com/Mail.Send openid' \
   --data-urlencode 'redirect_uri=http://localhost' \
   --data-urlencode 'grant_type=authorization_code' \
   --data-urlencode 'client_secret=<clientSecret>' \
   --data-urlencode 'code=<code>'
   ```

1. refreshToken と accessToken をメモしておきます。

### トークンの検証 {#validating-the-tokens}

AEM 側で Oauth を設定する前に、次の手順で accessToken と refreshToken の両方を検証してください。

1. 前の手順で生成した refreshToken を使用して accessToken を生成します。次の curl でこれを行えます（`<client_id>`、`<client_secret>`、`<refreshToken>` の値を置き換えます）。

   ```
   curl --location --request POST 'https://login.microsoftonline.com/<tenetId>/oauth2/v2.0/token' \
   --header 'Content-Type: application/x-www-form-urlencoded' \
   --header 'Cookie: buid=0.ARgAep0nU49DzUGmoP2wnvyIkcQjsx26HEpOnvHS0akqXQgYAAA.AQABAAEAAAD--DLA3VO7QrddgJg7Wevry9XPJSKbGVlPt5NWYxLtTl3K1W0LwHXelrffApUo_K02kFrkvmGm94rfBT94t25Zq4bCd5IM3yFOjWb3V22yDM7-rl112sLzbBQBRCL3QAAgAA; esctx=AQABAAAAAAD--DLA3VO7QrddgJg7Wevr4a8wBjYcNbBXRievdTOd15caaeAsQdXeBAQA3tjVQaxmrOXFGkKaE7HBzsJrzA-ci4RRpor-opoo5gpGLh3pj_iMZuqegQPEb1V5sUVQV8_DUEbBv5YFV2eczS5EAhLBAwAd1mHx6jYOL8LwZNDFvd2-MhVXwPd6iKPigSuBxMogAA; x-ms-gateway-slice=estsfd; stsservicecookie=estsfd; fpc=Auv6lTuyAP1FuOOCfj9w0U_IezHLAQAAAPeNSdgOAAAA' \
   --data-urlencode 'client_id=<client_id>' \
   --data-urlencode 'scope=https://outlook.office365.com/SMTP.Send https://outlook.office365.com/Mail.Read https://outlook.office365.com/Mail.Send openid' \
   --data-urlencode 'redirect_uri=http://localhost' \
   --data-urlencode 'grant_type=refresh_token' \
   --data-urlencode 'client_secret=<client_secret>' \
   --data-urlencode 'refresh_token=<refreshToken>'
   ```

1. accessToken を使用してメールを送信し、正しく動作しているかどうかを確認します。

>[!NOTE]
>
> [この場所](https://docs.microsoft.com/ja-jp/azure/active-directory/develop/v2-oauth2-auth-code-flow)から Postman API コレクションを取得できます。

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
       refreshUrl: "<Refresh token Url>",
       refreshToken: "$[secret:SECRET_SMTP_OAUTH_REFRESH_TOKEN]"
   }
   ```

1. 前の節で説明したように、 `authUrl`、 `tokenUrl`、 `refreshURL` を作成して入力します。
1. 次のスコープを設定に追加します。
   * `openid`
   * `offline_access`
   * `https://outlook.office365.com/Mail.Send`
   * `https://outlook.office365.com/Mail.Read`
   * `https://outlook.office365.com/SMTP.Send`
1. 次の構文で、OSGI プロパティファイル`called com.day.cq.mailer.impl.DefaultMailService.cfg.json`を  
`/apps/<my-project>/osgiconfig/config` に作成します。

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

1. Outlook の場合、`smtp.host` 設定値は `smtp.office365.com` です
1. 実行時に、[ここ](/help/implementing/deploying/configuring-osgi.md#setting-values-via-api)で説明しているように、Cloud Manager 変数 API を使用して `refreshToken values` および `clientSecret` シークレットを渡します。変数 `SECRET_SMTP_OAUTH_REFRESH_TOKEN` と `SECRET_SMTP_OAUTH_CLIENT_SECRET` の値を定義する必要があります。

### トラブルシューティング {#troubleshooting}

メールサービスが正常に動作しない場合は、ほとんどの場合、前述のように `refreshToken` を再生成し、Cloud Manager API を介して新しい値を渡す必要があります。新しい値がデプロイされるまで数分かかります。
