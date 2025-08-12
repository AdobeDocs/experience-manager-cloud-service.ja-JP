---
title: パブリッシュ層でのAEM as a Cloud Serviceの Open ID Connect サポート
description: パブリッシュ層でAEM as a Cloud Service用に Open ID Connect （OIDC）を設定する方法について説明します
feature: Security
role: Admin
exl-id: d2f30406-546c-4a2f-ba88-8046dee3e09b
source-git-commit: bf35f847f6f00d21915dfedb10cf38ea74344988
workflow-type: tm+mt
source-wordcount: '1469'
ht-degree: 4%

---

# パブリッシュ層でのAEM as a Cloud Serviceの Open ID Connect サポート

## はじめに {#introduction}

組織がデジタルエクスペリエンスを最新化する際に、安全で拡張性の高い ID 管理は基本的な要件になります。 Adobe Experience Manager（AEM）Cloud Serviceは、パブリッシュ層で OpenID Connect （OIDC）をサポートするようになり、Entra ID （Azure AD）、Google、Okta、Auth0、Ping Identity、ForgeRock、OIDC でサポートされている IDP など、主要な ID プロバイダー（IdP）とのシームレスで標準ベースの統合を可能にします。

OIDC は、OAuth 2.0 プロトコルをベースとする ID レイヤーであり、開発者のシンプルさを維持しながら、堅牢なユーザー認証を可能にします。 これは、安全なユーザーログインと ID の統合が必要な B2C （Business-to-Consumer）、イントラネット、パートナーポータルシナリオで広く採用されています。

これまで、AEMのお客様は、独自のカスタムログインロジックをパブリッシュ層に実装する責任を負っていました。これにより、開発時間が長くなり、長期的なメンテナンスとセキュリティの課題が生じました。 AEM Cloud Service では、OIDC のネイティブサポートにより、パブリッシュ環境にアクセスするエンドユーザーに対して、Adobeでサポートされる拡張可能で安全な認証メカニズムを提供することで、この負担を取り除きます。

パーソナライズされた消費者 Web サイトを提供する場合でも、認証済みの内部ポータルを提供する場合でも、パブリッシュに関する OIDC は、ID フェデレーションを簡素化し、一元化された ID ガバナンスを通じてリスクを軽減します。 また、組織が機敏性を犠牲にすることなく、最新のコンプライアンスとセキュリティの標準に準拠するのに役立ちます。

## OIDC 認証用のAEMの設定 {#configure-aem-oidc-authentication}

### 前提条件 {#prerequisits}

以下の情報が使用可能または定義されていることを前提としています。

1. AEM リポジトリ内の保護するコンテンツのパス
1. 設定する IdP の識別子。 これは任意の文字列にできます

Idp 設定からの情報：

1. IdP で設定されたクライアント ID
1. Idp で設定されたクライアント秘密鍵。 PKCE が Idp で設定されている場合、クライアントシークレットは使用できません。 設定ファイルにプレーンテキストの値を保存しないでください。 CM 秘密鍵の使用と参照
1. Idp で設定されたスコープ。 少なくともスコープ `openid` を指定する必要があります
1. IdP で PKCE が有効になっているかどうか
1. `callbackUrl` は、ポイント 1 で定義された設定済みパスの 1 つを使用し、次のサフィックスを追加して定義されます。`/j_security_check`
1. 標準の `baseUrl` ファイルにアクセスするための `.well-known` です。 例えば、よく知られている URL が `https://login.microsoftonline.com/53279d7a-438f-41cd-a6a0-fdb09efc8891/v2.0/.well-known/openid-configuration` の場合、`baseUrl` は `https://login.microsoftonline.com/53279d7a-438f-41cd-a6a0-fdb09efc8891` です。

### 設定ファイルの概要 {#overview-of-the-configuration-files}

設定が必要なファイルのリストを以下に示します。

1. **OIDC 接続**：これは、`OidcAuthenticationHandler` ーザーがユーザーを認証するために使用するか、他のコンポーネントが OAuth を使用して IdP によって保護されたリソースへのアクセスを [ 認証 ](https://github.com/apache/sling-org-apache-sling-auth-oauth-client) するために使用します。
1. **OIDC 認証ハンドラー**：これは、設定されたパスにアクセスするユーザーの認証に使用される認証ハンドラーです
1. **UserInfoProcessor**：このコンポーネントは、IdP によって受信された情報を処理します。 カスタムロジックを実装するために、顧客が拡張できます
1. [**デフォルトの同期ハンドラー**](https://jackrabbit.apache.org/oak/docs/security/authentication/external/defaultusersync.html)：このコンポーネントは、リポジトリにユーザーを作成します
1. [**ExternalLoginModule**](https://jackrabbit.apache.org/oak/docs/security/authentication/externalloginmodule.html)：このコンポーネントは、ローカルの Oak リポジトリでユーザーを認証します。

次の図は、前述の設定要素がどのようにリンクされているかを示しています。 これらは `ServiceFactory` 個のコンポーネントなので、`~uniqueid` は任意のランダムな一意の文字列にすることができます。

![OIDC の構成図 ](/help/security/assets/oidc-diagram.png)

### OIDC 接続の設定 {#configure-the-oidc-connection}

まず、OIDC 接続を設定する必要があります。 複数の OIDC 接続を構成でき、それぞれに異なる名前を付ける必要があります。

1. 設定を格納する新しい `.cfg.json` ファイルを作成します。 例えば、`org.apache.sling.auth.oauth_client.impl.OidcConnectionImpl~azure.cfg.json` を使用できます。**azure** サフィックスは、接続の一意の ID である必要があります
1. 次の例の設定形式に従います。

   ```
   {
    "name":"azure",
    "scopes":[
      "openid"
    ],
    "baseUrl":"<https://login.microsoftonline.com/53279d7a-438f-41cd-a6a0-fdb09efc8891/v2.0>",
    "clientId":"5199fc45-8000-473e-ac63-989f1a78759f",
    "clientSecret":"xxxxxx"
   }
   ```

1. そのプロパティを次のように設定します。
   * **&quot;name&quot;** は、ユーザーが定義できます
   * `baseUrl`、`clientid`、`clientSecret` は、IdP から取得される設定値です。
   * 範囲には、少なくとも値 `openid` が含まれている必要があります。

### OIDC 認証ハンドラーの設定 {#configure-oidc-authentication-handler}

次に、OIDC 認証ハンドラーを設定します。 複数の OIDC 接続を設定できます。 それぞれに異なる名前を付ける必要があります。 同じ [OAK外部 ID プロバイダー ](https://jackrabbit.apache.org/oak/docs/security/authentication/identitymanagement.html) を共有している場合、ユーザーを共有できます。

1. 設定ファイルを作成します。 この例では、`org.apache.sling.auth.oauth_client.impl.OidcConnectionImpl~azure.cfg.json` を使用します。 `azure` サフィックスは一意の ID である必要があります。 以下の設定ファイルの例を参照してください。

   ```
   {
     "path":"/content/tests/us/en/test-7",
     "callbackUri":"http://localhost:14503/content/tests/us/en/test-7/j_security_check",
     "pkceEnabled":false,
     "defaultConnectionName":"azure"
     "idp": "azure-idp"
   }
   ```

1. その後、次のようにプロパティを設定します。
   * `path`：保護されるパス
   * `callbackUri`：保護するパスに、次のサフィックスを追加します：`/j_security_check`
   * `defaultConnectionName`：前の手順で OIDC 接続に対して定義したものと同じ名前を使用してを設定します+
   * `pkceEnabled`：認証コードフローの `true` Proof Key for Code Exchange （PKCE）
   * `idp`: [OAK外部 ID プロバイダー ](https://jackrabbit.apache.org/oak/docs/security/authentication/identitymanagement.html) の名前。 異なるOAK IDP でユーザーやグループを共有することはできません

### SlingUserInfoProcessor の設定

1. 設定ファイルを作成します。 この例では、`org.apache.sling.auth.oauth_client.impl.SlingUserInfoProcessor~azure.cfg.json` を使用します。 `azure` サフィックスは一意の ID である必要があります。 以下の設定ファイルの例を参照してください。

   ```
   {
      "groupsInIdToken":true,
      "groupsClaimName": "groups",
      "connection":"azure",
      "storeAccessToken": false,
      "storeRefreshToken": false
   }
   ```

1. その後、次のようにプロパティを設定します。
   * `groupsInIdToken`：グループが ID トークンで送信される場合は、true に設定します。 値が false の場合、または指定されていない場合、グループは UserInfo エンドポイントから読み取られます。
   * `groupsClaimName`：要求の名前には、AEMで同期されるグループが含まれます。
   * `connection`：前の手順で OIDC 接続に対して定義したものと同じ名前を使用してを設定します
   * `storeAccessToken`：アクセストークンをリポジトリに格納する必要がある場合は、true。 デフォルトでは false になっています。 同じ IdP で保護される外部サーバーに保存されているユーザーの代わりにAEMがリソースにアクセスする必要がある場合にのみ、true に設定します。
   * `storeRefreshToken`：更新トークンをリポジトリに保存する必要がある場合は、true。 デフォルトでは false になっています。 同じ IdP で保護される外部サーバーに保存されているユーザーの代わりにAEMがリソースにアクセスし、IdP からトークンを更新する必要がある場合にのみ、true に設定します。
アクセストークンと更新トークンはAEMのマスターキーで暗号化されて保存されることに注意してください。


### 同期ハンドラーの設定 {#configure-the-synchronization-handler}

Oak で認証されたユーザーを同期するように少なくとも 1 つの同期ハンドラーを設定する必要があります。 詳しくは、[ この ](https://jackrabbit.apache.org/oak/docs/security/authentication/external/defaultusersync.html) ページを参照してください。

`org.apache.jackrabbit.oak.spi.security.authentication.external.impl.DefaultSyncHandler~azure.cfg.json` という名前のファイルを作成します。**azure** サフィックスは一意の ID である必要があります。 プロパティの設定方法について詳しくは、[Oak ユーザーとグループの同期のドキュメント ](https://jackrabbit.apache.org/oak/docs/security/authentication/external/defaultusersync.html) を参照してください。 以下に設定例を示します。

```
{
  "user.expirationTime":"300s",
  "user.membershipExpTime":"300s",
  "user.propertyMapping":[
    "profile/familyName=profile/familyName",
    "profile/givenName=profile/givenName",
    "rep:fullname=cn",
    "profile/email=profile/email",
    "oauth-tokens"
  ],
  "user.pathPrefix":"azure",
  "handler.name":"azure"
}
```

DefaultSyncHandler で設定する最も関連性の高い属性のいくつかを以下に示します。 動的グループメンバーシップは常に Cloud Services で有効にする必要があることに注意してください。

| プロパティ名 | メモ | 推奨値 |
|---|---|---|
| `user.expirationTime` | 同期されたユーザーが期限切れになるまでの期間 ユーザーは、有効期限が切れた後にのみ同期されます。 | 1 時間 |
| `user.membershipExpTime` | 同期されたユーザーメンバーシップが期限切れになるまでの期間 ユーザーメンバーシップは有効期限が切れた後にのみ同期されます。 | 1 時間 |
| `user.dynamicMembership` | 動的グループメンバーシップを有効にすることをお勧めします | true |
| `user.enforceDynamicMembership` | 動的グループメンバーシップの適用を有効にすることをお勧めします | true |
| `group.dynamicGroups` | 動的グループを有効にすることをお勧めします | true |
| user.propertyMapping | `UserInfoProcessor` の実装では、同期されるプロパティはごくわずかです。 変更やカスタマイズが可能です。 | <code>&quot;profile/givenName=profile/given_name&quot;,</code><br><code>&quot;profile/familyName=profile/family_name&quot;,</code><br><code>&quot;rep:fullname=profile/name&quot;,</code><br><code>&quot;profile/email=profile/email&quot;,</code><br><code>&quot;access_token=access_token&quot;,</code><br><code>&quot;refresh_token=refresh_token&quot;</code> |  |
| `user.membershipNestingDepth` | メンバーシップ関係が同期された場合のグループのネストの最大深さを返します。値 0 を指定すると、グループメンバーシップの参照が実質的に無効化されます。値 1 を指定すると、ユーザーの直接グループのみが追加されます。ユーザーのメンバーシップの上位を同期する場合に限定して個々のグループを同期する場合、この値は無効です。 | 1 |

### 外部ログインモジュールの設定 {#configure-the-external-login-module}

最後に、外部ログインモジュールを設定します。

1. `org.apache.jackrabbit.oak.spi.security.authentication.external.impl.ExternalLoginModuleFactory~azure.cfg.json` という名前のファイルを作成します。以下の設定例を参照してください。

   ```
   {
    "sync.handlerName":"azure",
    "idp.name":"azure-idp"
   }
   ```

1. そのプロパティを次のように設定します。

   * `sync.handlerName`：以前に定義した同期ハンドラーの名前
   * `idp.name`: OIDC 認証ハンドラーで定義されたOAK ID プロバイダー

### オプション：カスタム UserInfoProcessor の実装 {#implement-a-custom-userinfoprocessor}

ユーザーは ID トークンによって認証され、追加の属性は IdP 用に定義された `userInfo` エンドポイントで取得されます。 標準以外の操作を追加で実行する必要がある場合、[UserInfoProcessor](https://github.com/apache/sling-org-apache-sling-auth-oauth-client/blob/master/src/main/java/org/apache/sling/auth/oauth_client/impl/SlingUserInfoProcessorImpl.java) のカスタム実装が Sling のデフォルトの実装です。

## 例：Azure Active Directory を使用した OIDC 認証の設定

### Azure Active Directory での新しいアプリケーションの設定 {#configure-a-new-application-in-azure-ad}

1. [Azure Active Directory のドキュメント ](https://learn.microsoft.com/en-us/power-pages/security/authentication/openid-settings#create-an-app-registration-in-azure) に従って、Azure Active Directory に新しいアプリケーションを作成します。  アプリケーションの概要を説明する画面の見え方を以下に示します。

   ![ アプリケーションの概要 ](/help/security/assets/odic-application-overview.png)

1. グループまたはアプリケーションの役割が必要な場合は、[ ドキュメント ](https://learn.microsoft.com/en-us/entra/external-id/customers/how-to-use-app-roles-customers) に従ってグループまたはアプリケーションの役割を有効にし、ID トークンで送信します。 設定済みグループの例を次に示します。

![OIDC 請求トークン ID](/help/security/assets/oidc-claim-id-token.png)

1. 上記の手順に従って、必要な設定ファイルを作成します。 以下に、Azure AD に固有の例を示します。
   * oidc Connection、Authentication Handler および DefaultSyncHandler の名前は、`azure` のように定義します。
   * Web サイトの URL は `www.mywebsite.com` です。
   * 私たちは道を守 `/content/wknd/us/en/adventures`
   * テナント：`tennat-id`、
   * クライアント ID は `client-id` です。
   * シークレットは次のとおりです：`secret`、
   * グループは、ID トークン内の `groups` というクレームで送信されます。

#### org.apache.sling.auth.oauth_client.impl.OidcConnectionImpl~azure.cfg.json

```
{
  "name":"azure",
  "scopes":[
    openid", "User.Read", "profile", "email
  ],
  "baseUrl":"https://login.microsoftonline.com/tenant-id/v2.0",
  "clientId":"client-id",
  "clientSecret":"secret"
}
```

#### org.apache.sling.auth.oauth_client.impl.OidcAuthenticationHandler~azure.cfg.json

```
{
  "callbackUri":"https://www.mywebsite.com/content/wknd/us/en/adventures/j_security_check",
  "path":[
    "/content/wknd/us/en/adventures"
  ],
  "idp":"azure",
  "defaultConnectionName":"azure"
}
```

#### org.apache.jackrabbit.oak.spi.security.authentication.external.impl.ExternalLoginModuleFactory~azure.cfg.json

```
{
  "sync.handlerName":"azure",
  "idp.name":"azure"
}
```

#### org.apache.jackrabbit.oak.spi.security.authentication.external.impl.DefaultSyncHandler~azure.cfg.json

```
{
  "user.expirationTime":"1s",
  "user.membershipExpTime":"1s",
  "user.propertyMapping":[
    "profile/givenName=profile/given_name",
    "profile/familyName=profile/family_name",
    "rep:fullname=profile/name",
    "profile/email=profile/email",
    "access_token=access_token",
    "refresh_token=refresh_token"
  ],
  "user.pathPrefix":"azure",
  "group.pathPrefix": "oidc",
  "user.membershipNestingDepth": "1",
  "handler.name":"azure"
}
```

#### org.apache.sling.auth.oauth_client.impl.SlingUserInfoProcessorImpl~azure.cfg.json

```
{
  "groupsInIdToken": "true",
  "storeAccessToken": "false",
  "storeRefreshToken": "false",
  "connection": "azure",
  "groupsClaimName": "groups"
}
```

### Azure AD グループに関する追加情報 {#additional-information-about-azure-ad-groups}

Microsoft Azure Portal でエンタープライズアプリケーションのグループをに設定するには、**エンタープライズアプリケーション** でアプリケーションを検索し、グループを追加する必要があります。<!-- Alexandru: this bit cound be clearer-->

![OIDC Group add](/help/security/assets/oidc-ad-additional-info.png)

ID トークンでグループ要求を有効にするには、Microsoft Azure Portal の **トークン設定** セクションに要求を追加します。<!-- Alexandru: this bit cound be clearer as well-->

![OIDC 請求トークン ID](/help/security/assets/oidc-claim-id-token.png)

`SlingUserInfoProcessor` の設定は、次の例のように変更する必要があります。

変更が必要なファイル名は `org.apache.sling.auth.oauth_client.impl.SlingUserInfoProcessorImpl.cfg.json` です。 コンテンツは、次のように設定する必要があります。

```
{
  "connection": "azure",
  "groupsInIdToken": "true",
  "storeAccessToken": "false",
  "storeRefreshToken": "false"
}
```
