---
title: パブリッシュ層での AEM as a Cloud Service の Open ID Connect のサポート
description: パブリッシュ層で AEM as a Cloud Service の Open ID Connect（OIDC）を設定する方法について説明します
feature: Security
role: Admin
exl-id: d2f30406-546c-4a2f-ba88-8046dee3e09b
source-git-commit: 70687e4f2ea0df923e44237bc20635745c46323a
workflow-type: tm+mt
source-wordcount: '2610'
ht-degree: 53%

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
    "baseUrl":"<https://login.microsoftonline.com/tenant-id/v2.0>",
    "clientId":"client-id-from-idp",
    "clientSecret":"xxxxxx"
   }
   ```

一部の環境では、ID プロバイダー（IdP）が有効な`.well-known` エンドポイントを公開しない場合があります。
この場合、設定ファイルで次のプロパティを指定することで、必要なエンドポイントを手動で定義できます。
この設定モードでは、`baseUrl` プロパティを設定しないでください。

```
"authorizationEndpoint": "https://idp-url/oauth2/v1/authorize",
"tokenEndpoint": "https://idp-url/oauth2/v1/token",
"jwkSetURL":"https://idp-url/oauth2/v1/keys",
"issuer": "https://idp-url"
```

1. そのプロパティを次のように設定します。
   * **「name」**&#x200B;は、ユーザーが定義できます。
   * `baseUrl`、`clientid` および `clientSecret` は、IdP から取得される設定値です。
   * scopes には、少なくとも `openid` の値を含める必要があります。

### OIDC 認証ハンドラーの設定 {#configure-oidc-authentication-handler}

次に、OIDC 認証ハンドラーを設定します。 複数の OIDC 接続を設定できます。 それぞれに異なる名前を付ける必要があります。 同じ [OAK 外部 ID プロバイダー](https://jackrabbit.apache.org/oak/docs/security/authentication/identitymanagement.html)を共有する場合は、ユーザーを共有できます。

1. 設定ファイルを作成します。 この例では、`org.apache.sling.auth.oauth_client.impl.OidcAuthenticationHandler~azure.cfg.json` を使用します。 `azure` サフィックスは、一意の ID にする必要があります。 以下の設定ファイルの例を参照してください。

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
   * `callbackUri`：保護するパス。サフィックスを追加します：`/j_security_check`。 同じcallbackUriをリモート IdPでリダイレクト URLとして設定する必要があります。
   * `defaultConnectionName`：前の手順で OIDC 接続に定義したのと同じ名前で設定します+
   * `pkceEnabled`: `true`：認証コードフローでの Proof Key for Code Exchange（PKCE）
   * `idp`：[OAK 外部 ID プロバイダー](https://jackrabbit.apache.org/oak/docs/security/authentication/identitymanagement.html)の名前。 異なる OAK IDP では、ユーザーまたはグループを共有できません

### SlingUserInfoProcessor の設定 {#configure-slinguserinfoprocessor}

1. 設定ファイルを作成します。 この例では、`org.apache.sling.auth.oauth_client.impl.SlingUserInfoProcessorImpl~azure.cfg.json` を使用します。 `azure` サフィックスは、一意の ID にする必要があります。 以下の設定ファイルの例を参照してください。

   ```
   {
      "groupsInIdToken":true,
      "groupsClaimName": "groups",
      "connection":"azure",
      "storeAccessToken": false,
      "storeRefreshToken": false,
      "idpNameInPrincipals": true
   }
   ```

1. その後、そのプロパティを次のように設定します。
   * `groupsInIdToken`：グループが ID トークンで送信される場合は、true に設定します。 値が false の場合や指定されていない場合、グループは UserInfo エンドポイントから読み取られます。
   * `groupsClaimName`：要求の名前には、AEM で同期されるグループが含まれます。
   * `connection`：前の手順で OIDC 接続に定義したのと同じ名前で設定します
   * `storeAccessToken`：アクセストークンをリポジトリに保存する必要がある場合は、true。 デフォルトでは、これは false です。 同じ IdP で保護されている外部サーバーに保存されているユーザーの代わりに、AEM がリソースにアクセスする必要がある場合にのみ、true に設定します。
   * `storeRefreshToken`：更新トークンをリポジトリに保存する必要がある場合は、true。 デフォルトでは、これは false です。 同じIdPで保護されている外部サーバーに保存されているユーザーの代わりにAEMがリソースにアクセスする必要があり、IdPからトークンを更新する必要がある場合にのみ、trueに設定します。
   * `idpNameInPrincipals`: trueに設定すると、IdPの名前がユーザーおよびグループ プリンシパルのサフィックスとして「;」で区切られて追加されます。 例えば、IdP名が`azure-idp`、ユーザー名が`john.doe`の場合、oakに保存されているプリンシパルは`john.doe;azure-idp`になります。 これは、複数のIdPがoakで設定されている場合に、異なるIdPから取得された同じ名前を持つユーザーまたはグループ間の競合を回避するのに役立ちます。 また、Samlなどの他の認証ハンドラーで作成されたユーザーやグループとの競合を回避するためにも設定できます。
アクセストークンと更新トークンは、AEM マスターキーで暗号化されて保存されます。


### 同期ハンドラーの設定 {#configure-the-synchronization-handler}

oak で認証されたユーザーを同期するには、1 つ以上の同期ハンドラーを設定する必要があります。 詳しくは、[この](https://jackrabbit.apache.org/oak/docs/security/authentication/external/defaultusersync.html)ページを参照してください。

`org.apache.jackrabbit.oak.spi.security.authentication.external.impl.DefaultSyncHandler~azure.cfg.json` という名前のファイルを作成します。 **azure** サフィックスは、一意の ID にする必要があります。 プロパティの設定方法について詳しくは、[Oak ユーザーとグループの同期ドキュメント](https://jackrabbit.apache.org/oak/docs/security/authentication/external/defaultusersync.html)を参照してください。 以下の設定の例を参照してください。

```
{
  "user.expirationTime":"1h",
  "user.membershipExpTime":"1h",
  "group.expirationTime": "1d"
  "user.propertyMapping":[
    "profile/givenName=profile/given_name",
    "profile/familyName=profile/family_name",
    "rep:fullname=profile/name",
    "profile/email=profile/email",
    "access_token=access_token",
    "refresh_token=refresh_token"
  ],
  "user.pathPrefix":"azure",
  "handler.name":"azure"
}
```

開発時には、有効期限を小さい値（例：1s）に短縮して、oakでのユーザーとグループの同期のテストを迅速化できます。
DefaultSyncHandler で設定する最も関連性の高い属性の一部を以下に示します。 Cloud Service では、動的グループメンバーシップを常に有効にする必要があります。

| プロパティ名 | メモ | 推奨値 |
|---|---|---|
| `user.expirationTime` | 同期されたユーザーが期限切れになるまでの期間。 ユーザーは、期限切れになった後にのみ同期されます。 | 1h |
| `user.membershipExpTime` | 同期されたユーザーメンバーシップが期限切れになるまでの期間。 ユーザーメンバーシップは、期限切れになった後にのみ同期されます。 | 1h |
| `user.dynamicMembership` | 動的グループメンバーシップを有効にすることをお勧めします | true |
| `user.enforceDynamicMembership` | 動的グループメンバーシップの適用を有効にすることをお勧めします | true |
| `group.dynamicGroups` | 動的グループを有効にすることをお勧めします | true |
| user.propertyMapping | 提供されている `UserInfoProcessor` の実装では、いくつかのプロパティのみが同期されます。 変更やカスタマイズが可能です。 | <code>&quot;profile/givenName=profile/given_name&quot;,</code><br><code>&quot;profile/familyName=profile/family_name&quot;,</code><br><code>&quot;rep:fullname=profile/name&quot;,</code><br><code>&quot;profile/email=profile/email&quot;,</code><br><code>&quot;access_token=access_token&quot;,</code><br><code>&quot;refresh_token=refresh_token&quot;</code> |
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

ユーザーはID トークンによって認証され、追加の属性はIdPに定義された`userInfo` エンドポイントから取得されます。 `UserInfoProcessor`は、ID プロバイダーから受信したデータを、AEMがユーザーの同期に使用できる資格情報と属性に変換する責任があります。

#### カスタム UserInfoProcessorの作成時 {#when-to-create-custom-userinfoprocessor}

デフォルトの[SlingUserInfoProcessorImpl](https://github.com/apache/sling-org-apache-sling-auth-oauth-client/blob/master/src/main/java/org/apache/sling/auth/oauth_client/impl/SlingUserInfoProcessorImpl.java)は、標準のOIDC要求とグループ同期を処理します。 必要に応じて、カスタム実装が必要になる場合があります。

* ID トークンまたはUserInfo応答からカスタムクレームを抽出して処理します
* 異なる属性名にクレームを変換またはマッピングする
* ネストされた要求からグループ抽出するためのカスタムロジックを実装する
* 標準OIDC プロファイルに含まれていないユーザー属性を追加する
* 特定のユースケースに対して、アクセストークンまたは更新トークンを処理
* 外部システムと統合し、認証中に利用者データを拡充

#### UserInfoProcessor インターフェイスについて {#understanding-userinfoprocessor-interface}

`UserInfoProcessor` パッケージの`org.apache.sling.auth.oauth_client.spi` インターフェイスでは、次の2つのメソッドが定義されています。

```java
public interface UserInfoProcessor {
    /**
     * Process the UserInfo and token response to create OIDC credentials
     *
     * @param userInfo - JSON response from the UserInfo endpoint (may be null)
     * @param tokenResponse - JSON response from the token endpoint
     * @param oidcSubject - The subject claim from the ID token
     * @param idp - The configured IDP name
     * @return OidcAuthCredentials containing user attributes and group memberships
     */
    @NotNull OidcAuthCredentials process(
        @Nullable String userInfo,
        @NotNull String tokenResponse,
        @NotNull String oidcSubject,
        @NotNull String idp
    );

    /**
     * @return The name of the OIDC connection this processor is associated with
     */
    @NotNull String connection();
}
```

返された`OidcAuthCredentials` オブジェクトを使用すると、次のことが可能になります。
* `setAttribute(key, value)`を介してユーザー属性を設定 – これらは`DefaultSyncHandler` プロパティ マッピングに基づいて同期されます
* `addGroup(groupName)`経由でグループメンバーシップを追加 – これらのグループはAEMで作成/同期されます

#### 例：UserInfoProcessorのカスタム実装 {#custom-userinfoprocessor-implementation}

カスタム `UserInfoProcessor`を実装する方法を示す完全な例を以下に示します。

```java
package com.mycompany.aem.auth;

import java.nio.charset.StandardCharsets;
import java.util.Base64;

import org.apache.sling.auth.oauth_client.spi.OidcAuthCredentials;
import org.apache.sling.auth.oauth_client.spi.UserInfoProcessor;
import org.jetbrains.annotations.NotNull;
import org.jetbrains.annotations.Nullable;
import org.osgi.service.component.annotations.Activate;
import org.osgi.service.component.annotations.Component;
import org.osgi.service.metatype.annotations.AttributeDefinition;
import org.osgi.service.metatype.annotations.Designate;
import org.osgi.service.metatype.annotations.ObjectClassDefinition;
import org.slf4j.Logger;
import org.slf4j.LoggerFactory;

import com.google.gson.JsonObject;
import com.google.gson.JsonParser;

/**
 * Custom UserInfoProcessor that extracts additional claims from the ID token
 * and adds custom user attributes and group memberships.
 */
@Component(service = UserInfoProcessor.class, property = {"service.ranking:Integer=50"})
@Designate(ocd = CustomUserInfoProcessor.Config.class, factory = true)
public class CustomUserInfoProcessor implements UserInfoProcessor {

    private static final Logger logger = LoggerFactory.getLogger(CustomUserInfoProcessor.class);

    @ObjectClassDefinition(name = "Custom UserInfo Processor")
    @interface Config {
        @AttributeDefinition(name = "Connection Name", description = "OIDC Connection Name")
        String connection();
    }

    private final String connection;

    @Activate
    public CustomUserInfoProcessor(Config config) {
        this.connection = config.connection();
        logger.info("CustomUserInfoProcessor activated for connection: {}", connection);
    }

    @Override
    public @NotNull OidcAuthCredentials process(
            @Nullable String userInfo,
            @NotNull String tokenResponse,
            @NotNull String oidcSubject,
            @NotNull String idp) {

        // Parse the token response to extract tokens
        JsonObject tokenJson = JsonParser.parseString(tokenResponse).getAsJsonObject();
        String accessToken = tokenJson.has("access_token") ?
            tokenJson.get("access_token").getAsString() : null;
        String idToken = tokenJson.has("id_token") ?
            tokenJson.get("id_token").getAsString() : null;

        logger.debug("Processing authentication for subject: {}", oidcSubject);

        // Decode and extract claims from ID Token
        JsonObject claims = null;
        if (idToken != null) {
            claims = decodeJwtPayload(idToken);
            logger.debug("Extracted claims from ID token: {}", claims);
        }

        // Create credentials object
        OidcAuthCredentials credentials = new OidcAuthCredentials(oidcSubject, idp);
        credentials.setAttribute(".token", "");

        // Extract standard profile attributes
        if (claims != null) {
            // Standard OIDC claims
            setAttributeIfPresent(credentials, claims, "given_name", "profile/given_name");
            setAttributeIfPresent(credentials, claims, "family_name", "profile/family_name");
            setAttributeIfPresent(credentials, claims, "email", "profile/email");
            setAttributeIfPresent(credentials, claims, "name", "profile/name");

            // Custom claims from your IdP
            setAttributeIfPresent(credentials, claims, "department", "profile/department");
            setAttributeIfPresent(credentials, claims, "employee_id", "profile/employeeId");
            setAttributeIfPresent(credentials, claims, "job_title", "profile/jobTitle");
        }

        // Extract group memberships from claims
        if (claims != null && claims.has("groups")) {
            if (claims.get("groups").isJsonArray()) {
                claims.get("groups").getAsJsonArray().forEach(group -> {
                    credentials.addGroup(group.getAsString());
                });
            }
        }

        // Optionally store tokens if needed for later API calls
        // Note: Only store tokens if your application needs to call external APIs
        // on behalf of the user. Tokens are encrypted before storage.
        if (accessToken != null) {
            credentials.setAttribute("access_token", accessToken);
        }

        return credentials;
    }

    @Override
    public @NotNull String connection() {
        return connection;
    }

    /**
     * Helper method to set attribute if present in claims
     */
    private void setAttributeIfPresent(OidcAuthCredentials credentials,
                                      JsonObject claims,
                                      String claimName,
                                      String attributeName) {
        if (claims.has(claimName) && !claims.get(claimName).isJsonNull()) {
            String value = claims.get(claimName).getAsString();
            if (value != null && !value.isEmpty()) {
                credentials.setAttribute(attributeName, value);
            }
        }
    }

    /**
     * Decode JWT payload (middle part) to extract claims
     */
    private JsonObject decodeJwtPayload(String jwt) {
        try {
            String[] parts = jwt.split("\\.");
            if (parts.length != 3) {
                logger.warn("Invalid JWT format");
                return null;
            }

            // Decode the payload (second part)
            String payload = parts[1];
            // Add padding if needed
            payload = payload + "====".substring(0, (4 - payload.length() % 4) % 4);
            // Replace URL-safe characters
            payload = payload.replace('-', '+').replace('_', '/');

            byte[] decoded = Base64.getDecoder().decode(payload);
            String json = new String(decoded, StandardCharsets.UTF_8);
            return JsonParser.parseString(json).getAsJsonObject();
        } catch (Exception e) {
            logger.error("Failed to decode JWT payload", e);
            return null;
        }
    }
}
```

#### 設定 {#custom-userinfoprocessor-configuration}

カスタム `UserInfoProcessor`の設定ファイルを`ui.config/src/main/content/jcr_root/apps/myapp/osgiconfig/config.publish/`の下のAEM プロジェクトに作成します。

**com.mycompany.aem.auth.CustomUserInfoProcessor～azure.cfg.json**

```json
{
  "connection": "azure"
}
```

設定は、`OidcConnectionImpl`設定で定義された接続名と一致する必要があります。 `service.ranking`注釈の`@Component` プロパティ（例では`50`に設定）は、複数のプロセッサが同じ接続に登録されている場合の優先度を決定します。 より高いランキングは、デフォルトの`SlingUserInfoProcessorImpl` （ランキングが`0`である）よりも優先されます。

#### 依存関係 {#custom-userinfoprocessor-dependencies}

コアモジュールの`pom.xml`に次の依存関係を追加します。

```xml
<dependency>
    <groupId>org.apache.sling</groupId>
    <artifactId>org.apache.sling.auth.oauth-client</artifactId>
    <version>0.1.7</version>
    <scope>provided</scope>
</dependency>
<dependency>
    <groupId>com.google.code.gson</groupId>
    <artifactId>gson</artifactId>
    <version>2.8.9</version>
    <scope>provided</scope>
</dependency>
```

#### DefaultSyncHandlerを使用した属性の同期 {#synchronizing-custom-attributes}

カスタム属性がJCRのユーザーノードに保持されるようにするには、プロパティマッピングを含めるように`DefaultSyncHandler`設定を更新します。

**org.apache.jackrabbit.oak.spi.security.authentication.external.impl.DefaultSyncHandler～azure.cfg.json**

```json
{
  "user.expirationTime": "1h",
  "user.membershipExpTime": "1h",
  "user.propertyMapping": [
    "profile/givenName=profile/given_name",
    "profile/familyName=profile/family_name",
    "rep:fullname=profile/name",
    "profile/email=profile/email",
    "profile/department=profile/department",
    "profile/employeeId=profile/employeeId",
    "profile/jobTitle=profile/jobTitle",
    "access_token=access_token"
  ],
  "user.pathPrefix": "azure",
  "handler.name": "azure"
}
```

形式は、`jcrPropertyPath=credentialAttributeName` です。左側は`/home/users`の下のユーザーノードにプロパティが保存されている場所で、右側は`UserInfoProcessor`を使用して`credentials.setAttribute()`で設定した属性名と一致します。

#### 実装とテスト {#custom-userinfoprocessor-deployment}

1. カスタム **を含むAEM プロジェクトを** ビルドして`UserInfoProcessor` デプロイします。

   ```bash
   mvn clean install -PautoInstallPackage
   ```

2. **OSGi コンソールで**&#x200B;の登録を`/system/console/components`で確認します。
   * カスタムプロセッサークラス名を検索します
   * コンポーネントがアクティブであり、接続設定が正しいことを確認します

3. **認証フローをテスト**:
   * `OidcAuthenticationHandler`で設定された保護されたパスにアクセスする
   * 認証が成功したら、CRXDEの`/home/users/<prefix>/<username>`にあるユーザーノードを確認します
   * カスタム属性が同期されていることを確認します
   * `/home/groups`の下のグループ メンバーシップを確認してください

4. **デバッグログを有効にして**&#x200B;問題をトラブルシューティングします。

   ```
   Logger: com.mycompany.aem.auth
   Log Level: DEBUG
   ```

#### ベストプラクティス {#custom-userinfoprocessor-best-practices}

* **トークンストレージの最小化**: アプリケーションがユーザーの代わりに外部サービスにAPI呼び出しを行う必要がある場合にのみ、アクセストークンまたは更新トークンを保存します。 トークンは暗号化されますが、オーバーヘッドが追加されます。
* **要求を検証**：要求が存在し、nullでない場合は必ず確認してから処理してください。
* **エラー処理**：エラーを適切にログに記録しますが、オプションの要求がない場合でも認証フローを完了できるようにします。
* **パフォーマンス**：すべての認証で実行されるので、処理ロジックを軽く保ちます。
* **セキュリティ**：完全なトークンやユーザーパスワードなどの機密情報は絶対に記録しないでください。 デバッグ用のトークンをログに記録する場合は、`substring()`を使用します。
* **テスト**：すべてのクレームのバリエーションが正しく処理されていることを確認するために、IdPのさまざまなユーザープロファイルを使用してテストします。

### 外部グループのACLの設定 {#configure-acl-for-external-groups}

ユーザーがOIDCを通じて認証される場合、通常、グループメンバーシップは外部ID プロバイダーから同期されます。
これらの外部グループは、AEM リポジトリで動的に作成されますが、アクセス制御エントリには自動的に関連付けられません。
ユーザーに適切な権限を付与するには、これらのグループに対してアクセス制御リスト（ACL）を明示的に定義する必要があります。

主に2つの手法が利用可能である。

### オプション 1 - ローカルグループ

外部グループは、既に必要なACLを持つローカルグループのメンバーとして追加できます。

* 外部グループはリポジトリに存在する必要があります。リポジトリは、そのグループに属するユーザーが初めてログインしたときに自動的に発生します。
* このオプションは、クローズドユーザーグループ（CUG）が使用中の場合に一般的に推奨されます。オーサー環境とパブリッシュ環境の両方にローカルグループが存在するからです。

### オプション 2 — RepoInitを介した外部グループ上のダイレクト ACL

ACLは、RepoInit スクリプトを使用して外部グループに直接適用できます。

* このアプローチはより効率的であり、CUGが使用されていない場合に推奨されます。
* 次の例は、読み取り権限を外部グループに割り当てるRepoInit設定を示しています。 オプション `ignoreMissingPrincipal`を使用すると、グループがまだリポジトリに存在しない場合でも、ACLを作成できます。

  ```
  {
    "scripts":[
      "set ACL for \"my-group;my-idp\"  (ACLOptions=ignoreMissingPrincipal)\r\n  allow jcr:read on /content/wknd/us/en/magazine\r\nend"
    ]
  }    
  ```

>[!NOTE]
>AEM権限UIを使用して、グループプリンシパルに割り当てられたACLを調べることができます

## 例：Azure Active Directory を使用した OIDC 認証の設定

### Azure Active Directory での新しいアプリケーションの設定 {#configure-a-new-application-in-azure-ad}

1. [Azure Active Directory ドキュメント](https://learn.microsoft.com/ja-jp/power-pages/security/authentication/openid-settings#create-an-app-registration-in-azure)に従って、Azure Active Directory に新しいアプリケーションを作成します。 アプリケーションの概要を示す画面がどのように表示されるかを以下に示します。

   ![アプリケーションの概要](/help/security/assets/odic-application-overview.png)

1. グループまたはアプリケーションの役割が必要な場合は、[ドキュメント](https://learn.microsoft.com/ja-jp/entra/external-id/customers/how-to-use-app-roles-customers)に従って、アプリケーションに対して有効にし、ID トークンで送信します。 設定したグループの例を以下に示します。

![OIDC 要求トークン ID](/help/security/assets/oidc-claim-id-token.png)

1. 前述の手順に従って、必要な設定ファイルを作成します。 Azure AD に固有の例を以下に示します。
   * oidc 接続、認証ハンドラー、DefaultSyncHandler の名前を `azure` のように定義します
   * Web サイトの URL：`www.mywebsite.com`
   * グループ `/content/wknd/us/en/adventures`の認証済みユーザーのみがアクセスできるパス `adventures`を保護します
   * テナント：`tennat-id`
   * クライアント ID：`client-id`
   * 秘密鍵：`secret`
   * 要求の ID トークンで送信したグループ：`groups`

### org.apache.sling.auth.oauth_client.impl.OidcConnectionImpl~azure.cfg.json

```
{
  "name":"azure",
  "scopes":[
    openid", "User.Read", "profile", "email"
  ],
  "baseUrl":"https://login.microsoftonline.com/tenant-id/v2.0",
  "clientId":"client-id",
  "clientSecret":"secret"
}
```

### org.apache.sling.auth.oauth_client.impl.OidcAuthenticationHandler~azure.cfg.json

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

### org.apache.jackrabbit.oak.spi.security.authentication.external.impl.ExternalLoginModuleFactory~azure.cfg.json

```
{
  "sync.handlerName":"azure",
  "idp.name":"azure"
}
```

### org.apache.jackrabbit.oak.spi.security.authentication.external.impl.DefaultSyncHandler~azure.cfg.json

```
{
  "user.expirationTime":"1h",
  "user.membershipExpTime":"1h",
  "group.expirationTime": "1d"
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

### org.apache.sling.jcr.repoinit.RepositoryInitializer~azure.cfg.json

```
{
  "scripts":[
    "set ACL for \"adventures;azure\"  (ACLOptions=ignoreMissingPrincipal)\r\n  allow jcr:read on /content/wknd/us/en/adventures\r\nend"
  ]
}
```

### org.apache.sling.auth.oauth_client.impl.SlingUserInfoProcessorImpl~azure.cfg.json

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

## 認証後のカスタムリダイレクト {#custom-redirect-after-authentication}

デフォルトでは、OIDC認証が成功すると、ユーザーは最初に要求されたURLにリダイレクトされます。 ただし、この動作は、`redirect` クエリパラメーターを使用してカスタマイズできます。

### リダイレクトパラメーターの使用

認証を開始する際は、認証リクエストに`redirect` パラメーターを追加して、カスタムリダイレクト URLを指定できます。

```
/content/wknd/us/en/adventures?redirect=/content/wknd/us/en/welcome
```

この例では、認証が成功すると、ユーザーは最初に要求されたページではなく`/content/wknd/us/en/welcome`にリダイレクトされます。

### セキュリティの制約

セキュリティ上の理由から、`redirect` パラメーターには次の制限があります。

* **相対パスである必要があります**: リダイレクト URLは`/`で始まる必要があります（例：`/content/mysite/dashboard`）
* **クロスサイトリダイレクトなし**：絶対URL （`https://external-site.com`など）は許可されていません
* **プロトコル相対URLがありません**: `//`で始まるURLは、プロトコル相対リダイレクトを防ぐために拒否されます

無効なリダイレクト URLが指定された場合、認証はエラーで失敗します。

### 使用例

1. **ログイン後のウェルカムページ**：ユーザーを最初のログイン後にパーソナライズされたウェルカムページにリダイレクトします

   ```
   /content/mysite/secure-area?redirect=/content/mysite/welcome
   ```

2. **ダッシュボードのリダイレクト**：認証後、ユーザーを特定のダッシュボードに誘導します

   ```
   /content/mysite/login?redirect=/content/mysite/user/dashboard
   ```

3. **ディープリンク**: ユーザーが認証してから特定のリソースにアクセスできるようにします

   ```
   /content/mysite/protected?redirect=/content/mysite/protected/specific-document
   ```

## Saml認証ハンドラーからOidc認証ハンドラーへの移行方法

AEMが既にSAML Authentication Handlerで設定されており、[data synchronization](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/sites/authoring/personalization/user-and-group-sync-for-publish-tier#data-synchronization)が有効になっているリポジトリにユーザーが存在する場合、元のSAML ユーザーと新しいOIDC ユーザーの間で競合が発生する可能性があります。

1. [OidcAuthenticationHandler](#configure-oidc-authentication-handler)を設定し、`idpNameInPrincipals`SlingUserInfoProcessor[設定で](#configure-slinguserinfoprocessor)を有効にします
1. 外部グループ [の](#configure-acl-for-external-groups)ACLを設定します。
1. ユーザーからログインした後、saml認証ハンドラーで作成された古いユーザーを削除できます。

>[!NOTE]
>SAML認証ハンドラーを無効にし、OIDC認証ハンドラーを有効にすると、[&#x200B; データ同期](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/sites/authoring/personalization/user-and-group-sync-for-publish-tier#data-synchronization)が有効になっていない場合、既存のセッションは無効になります。 ユーザーは再び認証する必要があり、その結果、リポジトリ内に新しいOIDC ユーザーノードが作成されます。

