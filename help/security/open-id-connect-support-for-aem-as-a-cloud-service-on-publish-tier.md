---
title: パブリッシュ層での AEM as a Cloud Service の Open ID Connect のサポート
description: パブリッシュ層で AEM as a Cloud Service の Open ID Connect（OIDC）を設定する方法について説明します
feature: Security
role: Admin
exl-id: d2f30406-546c-4a2f-ba88-8046dee3e09b
source-git-commit: f3cd1bc761c513ebb85351185e7aa0b6f6eb6f33
workflow-type: ht
source-wordcount: '1469'
ht-degree: 100%

---

# パブリッシュ層での AEM as a Cloud Service の Open ID Connect のサポート {#open-id-connect-support-for-aem-as-a-cloud-service-on-publish-tier}

## はじめに {#introduction}

組織がデジタルエクスペリエンスを最新化する際に、安全で拡張性の高い ID 管理は基本的な要件になります。 組織がデジタルエクスペリエンスを最新化する際に、安全で拡張性の高い ID 管理が基本的な要件になります。 Adobe Experience Manager（AEM）Cloud Service は、パブリッシュ層で OpenID Connect（OIDC）をサポートするようになりました。これにより、Entra ID（Azure AD）、Google、Okta、Auth0、Ping Identity、ForgeRock、OIDC でサポートされる IDP など、主要な ID プロバイダー（IdP）とのシームレスで標準ベースの統合が可能になります。

OIDC は、OAuth 2.0 プロトコルの上にある ID レイヤーで、開発者のシンプルさを維持しながら、堅牢なユーザー認証を可能にします。 これは、安全なユーザーログインと ID フェデレーションが必要な、B2C、イントラネット、パートナーポータルのシナリオで広く採用されています。

これまで、AEM のお客様は、パブリッシュ層に独自のカスタムログインロジックを実装する責任がありました。これにより、開発時間が長くなり、長期的なメンテナンスとセキュリティの課題が発生していました。 AEM Cloud Service では、OIDC のネイティブサポートにより、パブリッシュ環境にアクセスするエンドユーザー向けに、安全で拡張可能な、アドビでサポートされる認証メカニズムを提供することで、この負担を軽減します。

パーソナライズされた消費者向け web サイトを提供する場合でも、認証済みの内部ポータルを提供する場合でも、パブリッシュでの OIDC は ID フェデレーションを簡素化し、一元化された ID ガバナンスを通じてリスクを軽減します。 また、組織が俊敏性を犠牲にすることなく、最新のコンプライアンスとセキュリティ標準を満たすのにも役立ちます。

## OIDC 認証用の AEM の設定 {#configure-aem-oidc-authentication}

### 前提条件 {#prerequisits}

次の情報が使用可能または定義済みであることを前提としています。

1. AEM リポジトリで保護されるコンテンツのパス
1. 設定する IdP の識別子。 これは、任意の文字列を指定できます

Idp 設定からの情報：

1. IdP で設定されたクライアント ID
1. Idp で設定されたクライアント秘密鍵。 PKCE が Idp で設定されている場合、クライアント秘密鍵は使用できません。 設定ファイルにプレーンテキスト値を保存しないでください。 CM 秘密鍵を使用して参照します
1. Idp で設定された範囲。 少なくとも `openid` 範囲を指定する必要があります
1. PKCE が IdP で有効になっているかどうか
1. `callbackUrl` は、ポイント 1 で定義された設定済みパスの 1 つを使用し、サフィックス `/j_security_check` を追加して定義されます。
1. 標準の `.well-known` ファイルにアクセスするための `baseUrl`。 例えば、よく知られている URL が `https://login.microsoftonline.com/53279d7a-438f-41cd-a6a0-fdb09efc8891/v2.0/.well-known/openid-configuration` の場合、`baseUrl` は `https://login.microsoftonline.com/53279d7a-438f-41cd-a6a0-fdb09efc8891` です。

### 設定ファイルの概要 {#overview-of-the-configuration-files}

設定する必要があるファイルのリストを以下に示します。

1. **OIDC 接続**：これは、`OidcAuthenticationHandler` がユーザーを認証するために、または他のコンポーネントが [OAuth を使用して IdP によって保護されているリソースへのアクセスを承認](https://github.com/apache/sling-org-apache-sling-auth-oauth-client)するために使用します
1. **OIDC 認証ハンドラー**：これは、設定されたパスにアクセスするユーザーの認証に使用される認証ハンドラーです
1. **UserInfoProcessor**：このコンポーネントは、IdP によって受信された情報を処理します。 顧客が拡張して、カスタムロジックを実装できます
1. [**デフォルトの同期ハンドラー**](https://jackrabbit.apache.org/oak/docs/security/authentication/external/defaultusersync.html)：このコンポーネントは、リポジトリ内にユーザーを作成します
1. [**ExternalLoginModule**](https://jackrabbit.apache.org/oak/docs/security/authentication/externalloginmodule.html)：このコンポーネントは、ローカルの Oak リポジトリ内のユーザーを認証します。

次の図に、前述の設定要素がどのようにリンクされているかを示します。 これらは `ServiceFactory` コンポーネントなので、`~uniqueid` は任意のランダムな一意の文字列にすることができます。

![OIDC の設定図](/help/security/assets/oidc-diagram.png)

### OIDC 接続の設定 {#configure-the-oidc-connection}

まず、OIDC 接続を設定する必要があります。 複数の OIDC 接続を設定でき、それぞれに異なる名前を付ける必要があります。

1. 設定を格納する新しい `.cfg.json` ファイルを作成します。 例えば、`org.apache.sling.auth.oauth_client.impl.OidcConnectionImpl~azure.cfg.json` を使用できます。**azure** サフィックスは、接続の一意の ID にする必要があります。
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
   * **「name」**&#x200B;は、ユーザーが定義できます。
   * `baseUrl`、`clientid` および `clientSecret` は、IdP から取得される設定値です。
   * scopes には、少なくとも `openid` の値を含める必要があります。

### OIDC 認証ハンドラーの設定 {#configure-oidc-authentication-handler}

次に、OIDC 認証ハンドラーを設定します。 複数の OIDC 接続を設定できます。 それぞれに異なる名前を付ける必要があります。 同じ [OAK 外部 ID プロバイダー](https://jackrabbit.apache.org/oak/docs/security/authentication/identitymanagement.html)を共有する場合は、ユーザーを共有できます。

1. 設定ファイルを作成します。 この例では、`org.apache.sling.auth.oauth_client.impl.OidcConnectionImpl~azure.cfg.json` を使用します。 `azure` サフィックスは、一意の ID にする必要があります。 以下の設定ファイルの例を参照してください。

   ```
   {
     "path":"/content/tests/us/en/test-7",
     "callbackUri":"http://localhost:14503/content/tests/us/en/test-7/j_security_check",
     "pkceEnabled":false,
     "defaultConnectionName":"azure"
     "idp": "azure-idp"
   }
   ```

1. その後、そのプロパティを次のように設定します。
   * `path`：保護するパス
   * `callbackUri`：保護するパスにサフィックス `/j_security_check` を追加します
   * `defaultConnectionName`：前の手順で OIDC 接続に定義したのと同じ名前で設定します+
   * `pkceEnabled`: `true`：認証コードフローでの Proof Key for Code Exchange（PKCE）
   * `idp`：[OAK 外部 ID プロバイダー](https://jackrabbit.apache.org/oak/docs/security/authentication/identitymanagement.html)の名前。 異なる OAK IDP では、ユーザーまたはグループを共有できません

### SlingUserInfoProcessor の設定

1. 設定ファイルを作成します。 この例では、`org.apache.sling.auth.oauth_client.impl.SlingUserInfoProcessor~azure.cfg.json` を使用します。 `azure` サフィックスは、一意の ID にする必要があります。 以下の設定ファイルの例を参照してください。

   ```
   {
      "groupsInIdToken":true,
      "groupsClaimName": "groups",
      "connection":"azure",
      "storeAccessToken": false,
      "storeRefreshToken": false
   }
   ```

1. その後、そのプロパティを次のように設定します。
   * `groupsInIdToken`：グループが ID トークンで送信される場合は、true に設定します。 値が false の場合や指定されていない場合、グループは UserInfo エンドポイントから読み取られます。
   * `groupsClaimName`：要求の名前には、AEM で同期されるグループが含まれます。
   * `connection`：前の手順で OIDC 接続に定義したのと同じ名前で設定します
   * `storeAccessToken`：アクセストークンをリポジトリに保存する必要がある場合は、true。 デフォルトでは、これは false です。 同じ IdP で保護されている外部サーバーに保存されているユーザーの代わりに、AEM がリソースにアクセスする必要がある場合にのみ、true に設定します。
   * `storeRefreshToken`：更新トークンをリポジトリに保存する必要がある場合は、true。 デフォルトでは、これは false です。 同じ IdP で保護されている外部サーバーに保存されているユーザーの代わりに、AEM がリソースにアクセスし、IdP からのトークンを更新する必要がある場合にのみ、true に設定します。
アクセストークンと更新トークンは、AEM マスターキーで暗号化されて保存されます。


### 同期ハンドラーの設定 {#configure-the-synchronization-handler}

oak で認証されたユーザーを同期するには、1 つ以上の同期ハンドラーを設定する必要があります。 詳しくは、[この](https://jackrabbit.apache.org/oak/docs/security/authentication/external/defaultusersync.html)ページを参照してください。

`org.apache.jackrabbit.oak.spi.security.authentication.external.impl.DefaultSyncHandler~azure.cfg.json` という名前のファイルを作成します。 **azure** サフィックスは、一意の ID にする必要があります。 プロパティの設定方法について詳しくは、[Oak ユーザーとグループの同期ドキュメント](https://jackrabbit.apache.org/oak/docs/security/authentication/external/defaultusersync.html)を参照してください。 以下の設定の例を参照してください。

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

DefaultSyncHandler で設定する最も関連性の高い属性の一部を以下に示します。 Cloud Service では、動的グループメンバーシップを常に有効にする必要があります。

| プロパティ名 | メモ | 推奨値 |
|---|---|---|
| `user.expirationTime` | 同期されたユーザーが期限切れになるまでの期間。 ユーザーは、期限切れになった後にのみ同期されます。 | 1h |
| `user.membershipExpTime` | 同期されたユーザーメンバーシップが期限切れになるまでの期間。 ユーザーメンバーシップは、期限切れになった後にのみ同期されます。 | 1h |
| `user.dynamicMembership` | 動的グループメンバーシップを有効にすることをお勧めします | true |
| `user.enforceDynamicMembership` | 動的グループメンバーシップの適用を有効にすることをお勧めします | true |
| `group.dynamicGroups` | 動的グループを有効にすることをお勧めします | true |
| user.propertyMapping | 提供されている `UserInfoProcessor` の実装では、いくつかのプロパティのみが同期されます。 変更やカスタマイズが可能です。 | <code>&quot;profile/givenName=profile/given_name&quot;,</code><br><code>&quot;profile/familyName=profile/family_name&quot;,</code><br><code>&quot;rep:fullname=profile/name&quot;,</code><br><code>&quot;profile/email=profile/email&quot;,</code><br><code>&quot;access_token=access_token&quot;,</code><br><code>&quot;refresh_token=refresh_token&quot;</code> |  |
| `user.membershipNestingDepth` | メンバーシップ関係が同期された場合のグループのネストの最大深さを返します。 値 0 を指定すると、グループメンバーシップの参照が実質的に無効化されます。 値 1 を指定すると、ユーザーの直接グループのみが追加されます。 ユーザーのメンバーシップの上位を同期する場合に限定して個々のグループを同期する場合、この値は無効です。 | 1 |

### 外部ログインモジュールの設定 {#configure-the-external-login-module}

最後に、外部ログインモジュールを設定する必要があります。

1. `org.apache.jackrabbit.oak.spi.security.authentication.external.impl.ExternalLoginModuleFactory~azure.cfg.json` という名前のファイルを作成します。 以下の設定の例を参照してください。

   ```
   {
    "sync.handlerName":"azure",
    "idp.name":"azure-idp"
   }
   ```

1. そのプロパティを次のように設定します。

   * `sync.handlerName`：以前に定義した同期ハンドラーの名前
   * `idp.name`：OIDC 認証ハンドラーで定義した OAK ID プロバイダー

### オプション：カスタム UserInfoProcessor の実装 {#implement-a-custom-userinfoprocessor}

ユーザーは ID トークンによって認証され、IdP に対して定義された `userInfo` エンドポイントで追加の属性が取得されます。 追加の標準以外の操作を実行する必要がある場合、[UserInfoProcessor](https://github.com/apache/sling-org-apache-sling-auth-oauth-client/blob/master/src/main/java/org/apache/sling/auth/oauth_client/impl/SlingUserInfoProcessorImpl.java) のカスタム実装が Sling のデフォルト実装です。

## 例：Azure Active Directory を使用した OIDC 認証の設定

### Azure Active Directory での新しいアプリケーションの設定 {#configure-a-new-application-in-azure-ad}

1. [Azure Active Directory ドキュメント](https://learn.microsoft.com/ja-jp/power-pages/security/authentication/openid-settings#create-an-app-registration-in-azure)に従って、Azure Active Directory に新しいアプリケーションを作成します。 アプリケーションの概要を示す画面がどのように表示されるかを以下に示します。

   ![アプリケーションの概要](/help/security/assets/odic-application-overview.png)

1. グループまたはアプリケーションの役割が必要な場合は、[ドキュメント](https://learn.microsoft.com/ja-jp/entra/external-id/customers/how-to-use-app-roles-customers)に従って、アプリケーションに対して有効にし、ID トークンで送信します。 設定したグループの例を以下に示します。

![OIDC 要求トークン ID](/help/security/assets/oidc-claim-id-token.png)

1. 前述の手順に従って、必要な設定ファイルを作成します。 Azure AD に固有の例を以下に示します。
   * oidc 接続、認証ハンドラー、DefaultSyncHandler の名前を `azure` のように定義します
   * Web サイトの URL：`www.mywebsite.com`
   * 保護するパス：`/content/wknd/us/en/adventures`
   * テナント：`tennat-id`
   * クライアント ID：`client-id`
   * 秘密鍵：`secret`
   * 要求の ID トークンで送信したグループ：`groups`

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

Microsoft Azure Portal でエンタープライズアプリケーションのグループを設定するには、**エンタープライズアプリケーション**&#x200B;でアプリケーションを検索し、グループを追加する必要があります。<!-- Alexandru: this bit cound be clearer-->

![OIDC グループの追加](/help/security/assets/oidc-ad-additional-info.png)

ID トークンでグループ要求を有効にするには、Microsoft Azure Portal の「**トークン設定**」セクションで要求を追加します。<!-- Alexandru: this bit cound be clearer as well-->

![OIDC 要求トークン ID](/help/security/assets/oidc-claim-id-token.png)

`SlingUserInfoProcessor` の設定は、以下の例のように変更する必要があります。

変更する必要があるファイル名は、`org.apache.sling.auth.oauth_client.impl.SlingUserInfoProcessorImpl.cfg.json` です。 コンテンツは、次のように設定する必要があります。

```
{
  "connection": "azure",
  "groupsInIdToken": "true",
  "storeAccessToken": "false",
  "storeRefreshToken": "false"
}
```
