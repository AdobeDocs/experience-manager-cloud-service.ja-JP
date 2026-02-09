---
title: 外部 ID と動的グループメンバーシップへの移行
description: AEM as a Cloud Serviceの動的グループメンバーシップを使用した、ローカルユーザーとグループの外部 ID モデルへの移行に関するテクニカルガイド
solution: Experience Manager Sites
feature: Security
role: Developer, Admin
source-git-commit: bb4b60523f60b1285c5f2fd2e49f6cc8cff24324
workflow-type: tm+mt
source-wordcount: '2232'
ht-degree: 1%

---

# 外部 ID と動的グループメンバーシップへの移行 {#migrating-to-external-identity}

## 概要 {#overview}

AEM as a Cloud Serviceで [ データ同期 ](/help/sites-cloud/authoring/personalization/user-and-group-sync-for-publish-tier.md#data-synchronization) が有効になっている場合、ユーザーとグループの作成を管理する際に、動的グループメンバーシップで外部 ID に自動的に移行するように SAML 認証ハンドラーを設定できます。 プロジェクトでカスタムコードを使用してユーザーまたはグループを作成する場合は、ローカルユーザーやグループではなく、外部のユーザーやグループを作成するように更新する必要があります。

### 外部ユーザーとグループが必要な理由 {#why-external-required}

動的グループメンバーシップを使用して、ローカルユーザーとグループから外部 ID に移行することは、次のようないくつかの重要な理由で不可欠です。

**パフォーマンスの最適化：**

* **リポジトリ書き込みの削減**：従来のローカルグループメンバーシップでは、グループノードの複数の値を持つ単一のプロパティにリポジトリへのメンバーシップ関係を書き込む必要があります。 動的グループメンバーシップの場合、ユーザーには、すべてのグループプリンシパルを含む単一の `rep:externalPrincipalNames` プロパティが用意されるので、グループノードを同期する必要はありません
* **同期の高速化**：パブリッシュ層ノード間でユーザーを同期する場合、動的グループメンバーシップを持つ外部ユーザーは、従来のグループメンバーシップを持つローカルユーザーと比較して、データ転送が大幅に少なく、書き込み操作が少なくなります
* **スケーラビリティ**：多数のユーザーやグループが存在するシステムでは、リポジトリのオーバーヘッドの削減から大きなメリットが得られます。 動的グループメンバーシップは、非常に大きなグループの場合でも効率的に拡張されます。

このドキュメントでは、次の技術ガイダンスを提供します。

* 外部 ID モデルについて
* カスタムコードを変更した外部ユーザーおよびグループの作成
* 既存のローカルユーザーおよびグループの外部 ID モデルへの移行

## 外部 ID について {#understanding-external-identity}

### 社外ユーザー {#external-users}

外部ユーザーは、`rep:externalId` プロパティによって識別され、このプロパティはユーザーを外部の ID プロバイダーにリンクします。 形式は次のとおりです。

```
userId;idpName
```

例：`john.doe;saml-idp`。

>[!NOTE]
>
> `idpName` は、認証ハンドラー設定で定義されたOak ID プロバイダー（Idp）の名前を指します。 SAML 統合の場合、これは SAML 認証ハンドラーの `idpIdentifier` 属性に設定された値です。

**キープロパティ：**

* `rep:externalId`：ユーザーを外部としてマークする必須プロパティ （例：`john.doe;saml-idp`）
* `rep:externalPrincipalNames`：動的メンバーシップ用の外部グループプリンシパルを含む複数値プロパティ
* `rep:lastSynced`：前回の同期のタイムスタンプ
* `rep:lastDynamicSync`：前回の動的グループメンバーシップ同期のタイムスタンプ

### 外部グループ {#external-groups}

外部グループも `rep:externalId` プロパティによって識別され、プリンシパル名形式を使用します。

```
groupId;idpName
```

例：`content-authors;saml-idp`

### 動的グループメンバーシップ {#dynamic-group-membership}

動的グループメンバーシップは、リポジトリに保存されたユーザーからグループへの直接の関係の代わりに、ユーザーノードの `rep:externalPrincipalNames` プロパティを使用します。 ユーザーが外部グループの ID と一致する外部プリンシパル名を持つ場合、そのユーザーは自動的にそのグループのメンバーになります。 詳しくは、[Apache Oakのドキュメント ](https://jackrabbit.apache.org/oak/docs/security/authentication/external/dynamic.html) を参照してください。

**メリット：**

* リポジトリーへの書き込みの減少（ユーザーがグループに追加/削除されても、グループメンバーシップノードは変更されない）
* パブリッシュ層ノード間の同期の高速化
* スケーラブルなグループメンバーシップ管理
* データ同期要件との互換性

## サービスユーザー設定 {#service-user-configuration}

外部のユーザーやグループを作成または変更するすべての操作は、**プロパティと** プロパティのデフォルトの保護を回避するように適切に設定された `rep:externalId` サービスユーザー `rep:externalPrincipalNames` を使用して実行する必要があります。

### サービスユーザーが必要な理由 {#why-is-a-service-user-required}

Oak セキュリティのデフォルトでは、次のような保護されたプロパティを通常のセッションが変更するのを防ぐことができます。

* `rep:externalId` - ユーザー/グループを外部としてマークします
* `rep:externalPrincipalNames` – 動的グループメンバーシッププリンシパルを格納します

これらのプロパティを変更できるのは、適切に設定されたサービスユーザーのみです。

### サービスユーザーの設定とマッピング {#service-user-configuration-mapping}

外部 ID を管理するサービスユーザーの設定には、次の 3 つの調整された設定が必要です。

1. `repoinit` を使用したサービスユーザーの作成
2. `ExternalPrincipal` 保護の設定
3. サービスユーザーをアプリケーションバンドルにマッピングします。

これらの手順の詳細については、以下を参照してください。

#### 手順 1:Repoinit を使用してサービスユーザーを作成する {#create-the-serviice-user-via-repoinit}

この手順では、`repoinit` スクリプトを使用して、必要な権限を持つサービスユーザーの作成について詳しく説明します。

**構成ファイル：** `org.apache.sling.jcr.repoinit.RepositoryInitializer~group-provisioner.cfg.json`

**例示的な場所：** `ui.config/src/main/content/jcr_root/apps/yourproject/osgiconfig/config.publish/`

```json
{
  "scripts": [
    "create service user group-provisioner with path system/yourproject",
    "set ACL for group-provisioner\n  allow jcr:read,jcr:readAccessControl,jcr:modifyAccessControl,rep:userManagement,rep:write on /home/users\n  allow jcr:read,jcr:readAccessControl,jcr:modifyAccessControl,rep:userManagement,rep:write on /home/groups\nend"
  ]
}
```

**権限の概要**

* `jcr:read`：ユーザーおよびグループの読み取り
* `jcr:readAccessControl`:ACL の読み取り
* `jcr:modifyAccessControl`: ACL を変更します（プロパティの設定に必要）
* `rep:userManagement`：ユーザー/グループの作成と管理
* `rep:write`:`rep:externalId` および `rep:externalPrincipalNames` を含むプロパティの書き込み

>[!NOTE]
>
>サービスユーザーは `/home/users/system/yourproject` の下に作成され、他のシステムユーザーと整理されます。

#### 手順 2：外部プリンシパル保護の設定 {#configure-externalprincipal-protection}

以下は、外部の ID プロパティに適用される保護を回避できるよう、サービスユーザーを許可リストに登録するための設定例です。

**設定ファイル名：** `org.apache.jackrabbit.oak.spi.security.authentication.external.impl.principal.ExternalPrincipalConfiguration.cfg.json`

**場所の例：** `ui.config/src/main/content/jcr_root/apps/yourproject/osgiconfig/config.publish/`

```json
{
  "protectExternalIdentities": "Warn",
  "systemPrincipalNames": [
    "group-provisioner",
    "saml-migration-service"
  ]
}
```

**設定プロパティ：**

* `protectExternalIdentities`：外部 ID プロパティの保護レベルを制御します。
   * `"Strict"`：許可リスト内のシステムプリンシパルのみが、外部プロパティを変更できます。 これは、実稼動で推奨されるレベルです。
   * `"Warn"`：警告をログに記録しますが、変更は許可されます。 開発/テストに役立ちます。
   * `"None"`：保護なし。 お勧めしません。
* `systemPrincipalNames`:`rep:externalId` および `rep:externalPrincipalNames` の変更が許可されているサービスユーザー名のリスト。 外部 ID （`group-provisioner`、`saml-migration-service` など）を管理する必要があるすべてのサービスユーザーを含めます。

>[!IMPORTANT]
>
>`systemPrincipalNames` のサービスユーザー名は、repoinit スクリプトで作成されたサービスユーザー ID と完全に一致する必要があります。

#### 手順 3：サービスユーザーマッピング {#service-user-mapping}

サービスユーザーをアプリケーションバンドルにマッピングして、コードで使用できるようにします。

**構成ファイル：** `org.apache.sling.serviceusermapping.impl.ServiceUserMapperImpl.amended~group-provisioner.cfg.json`

**場所：** `ui.config/src/main/content/jcr_root/apps/yourproject/osgiconfig/config.publish/`

```json
{
  "user.mapping": [
    "yourproject.core:group-provisioner=[group-provisioner]"
  ]
}
```

**マッピング形式：**

* `yourproject.core`：記号バンドル名（`pom.xml` `<Bundle-SymbolicName>` にあります）
* `group-provisioner` （`=` より前）：コードで使用するサブサービス名
* `[group-provisioner]` （`=` 後）:repoinit で作成された実際のサービスユーザー ID

### コードでのサービスユーザーの使用 {#using-the-service-user-in-code}

移行またはユーザー/グループの作成操作を実行するためにセッションを開く場合は、サービスユーザーを使用する必要があります。

```java
import org.apache.sling.jcr.api.SlingRepository;

@Reference
private SlingRepository repository;

// Login as the service user
Session serviceSession = repository.loginService("group-provisioner", null);

try {
    UserManager userManager = ((JackrabbitSession) serviceSession).getUserManager();
    // Perform operations...
    serviceSession.save();
} finally {
    if (serviceSession != null && serviceSession.isLive()) {
        serviceSession.logout();
    }
}
```

>[!IMPORTANT]
>
>適切なサービスユーザー設定がないと、`rep:externalId` または `rep:externalPrincipalNames` を設定しようとすると、権限エラーで失敗します。 移行を試みる前に、`ExternalPrincipal` 設定でサービスユーザーが正しく設定されていることを確認してください。

## 完全な設定の例 {#complete-configuration-example}

以下に、3 つの設定をすべて一緒に示した完全な作業例を示します。

### ファイル構造 {#file-structure}

```
ui.config/src/main/content/jcr_root/apps/yourproject/osgiconfig/
└── config.publish/
    ├── org.apache.sling.jcr.repoinit.RepositoryInitializer~group-provisioner.cfg.json
    ├── org.apache.jackrabbit.oak.spi.security.authentication.external.impl.principal.ExternalPrincipalConfiguration.cfg.json
    └── org.apache.sling.serviceusermapping.impl.ServiceUserMapperImpl.amended~group-provisioner.cfg.json
```

### カスタムコードの変更 {#modifying-custom-code}

#### 外部ユーザーの作成 {#creating-external-users}

**前（ローカルユーザー）:**

```java
UserManager userManager = ((JackrabbitSession) session).getUserManager();
User user = userManager.createUser(userId, password);
```

**後（外部ユーザー）:**

```java
import org.apache.jackrabbit.oak.spi.security.authentication.external.ExternalIdentityRef;

UserManager userManager = ((JackrabbitSession) session).getUserManager();
ValueFactory valueFactory = session.getValueFactory();

// Create user with principal
Principal userPrincipal = new Principal() {
    @Override
    public String getName() {
        return userId;
    }
};

User user = userManager.createUser(userId, null, userPrincipal, null);

// Set rep:externalId
ExternalIdentityRef externalRef = new ExternalIdentityRef(userId, idpName);
String externalId = externalRef.getString(); // Format: userId;idpName
user.setProperty("rep:externalId", valueFactory.createValue(externalId));

// Set sync timestamps to far future (workaround for OAK-12079)
// Set to 10 years in the future to prevent premature cleanup of external group memberships
// See: https://issues.apache.org/jira/browse/OAK-12079
java.util.Calendar future = java.util.Calendar.getInstance();
future.add(java.util.Calendar.YEAR, 10);
user.setProperty("rep:lastSynced", valueFactory.createValue(future));
user.setProperty("rep:lastDynamicSync", valueFactory.createValue(future));

session.save();
```

#### 外部グループの作成 {#creating-external-groups}

**前（ローカル グループ）:**

```java
UserManager userManager = ((JackrabbitSession) session).getUserManager();
Group group = userManager.createGroup(groupId);
```

**後（外部グループ）:**

```java
import org.apache.jackrabbit.oak.spi.security.authentication.external.ExternalIdentityRef;

UserManager userManager = ((JackrabbitSession) session).getUserManager();
ValueFactory valueFactory = session.getValueFactory();

// Create group with principal
Principal groupPrincipal = new Principal() {
    @Override
    public String getName() {
        return groupId;
    }
};

Group group = userManager.createGroup(groupPrincipal);

// Set rep:externalId
ExternalIdentityRef externalRef = new ExternalIdentityRef(groupId, idpName);
String externalId = externalRef.getString(); // Format: groupId;idpName
group.setProperty("rep:externalId", valueFactory.createValue(externalId));

session.save();
```

#### 動的グループメンバーシップの割り当て {#assigning-dynamic-membership}

**前（ダイレクト メンバーシップ）:**

```java
Group group = (Group) userManager.getAuthorizable(groupId);
User user = (User) userManager.getAuthorizable(userId);
group.addMember(user);
```

**後（動的メンバーシップ）:**

```java
User user = (User) userManager.getAuthorizable(userId);
ValueFactory valueFactory = session.getValueFactory();

// Get existing external principal names
Value[] existingValues = user.getProperty("rep:externalPrincipalNames");
List<String> principalNames = new ArrayList<>();

if (existingValues != null) {
    for (Value value : existingValues) {
        principalNames.add(value.getString());
    }
}

// Add new principal name (format: groupId;idpName)
String dynamicGroupPrincipal = groupId + ";" + idpName;
if (!principalNames.contains(dynamicGroupPrincipal)) {
    principalNames.add(dynamicGroupPrincipal);
    
    // Create new Value array
    Value[] newValues = new Value[principalNames.size()];
    for (int i = 0; i < principalNames.size(); i++) {
        newValues[i] = valueFactory.createValue(principalNames.get(i));
    }
    
    // Set the property
    user.setProperty("rep:externalPrincipalNames", newValues);
    
    // Update sync timestamps to far future (workaround for OAK-12079)
    // Set to 10 years in the future to prevent premature cleanup of external group memberships
    // See: https://issues.apache.org/jira/browse/OAK-12079
    java.util.Calendar future = java.util.Calendar.getInstance();
    future.add(java.util.Calendar.YEAR, 10);
    user.setProperty("rep:lastDynamicSync", valueFactory.createValue(future));
    user.setProperty("rep:lastSynced", valueFactory.createValue(future));
}

session.save();
```

## 移行プロセス {#migration-process}

データ同期サービスを有効にする前にカスタムコードが更新された場合、既存のローカルユーザーとグループを外部 ID に移行する必要はありません。

ローカルユーザーとグループが既にリポジトリに保持されていて、環境がアクティブに使用されている場合は、中断や不整合を避けるために、次のような複数の手順による移行を実行することをお勧めします。

>[!IMPORTANT]
>
>すべての移行手順は、`group-provisioner` プロパティと `rep:externalId` プロパティの保護をバイパスする権限が付与された適切に設定されたサービスユーザー（`rep:externalPrincipalNames` など）を使用して実行する必要があります。 詳しくは、[ サービスユーザー設定 ](#service-user-configuration) を参照してください。

### 手順 1：外部グループ構造を作成する {#step-1-create-external-group-structure}

移行する必要がある各ローカルグループに対して、次の操作を行います。

1. プリンシパル名 `<localGroupId>;<idpName>` で、対応する外部グループを作成します。 外部グループをローカルグループにリンクするのに役立つ命名規則を使用します
1. 値を使用して、外部グループの `rep:externalId` プロパティを設定します。`<localGroupId>;<idpName>`
1. 外部グループを元のローカルグループのメンバーとして追加します。

**検証**

* 結果を検証するには、すべてのローカルグループに対応する外部グループがあるかどうかを確認します。 さらに、すべての外部グループは、対応するローカルグループのメンバーになります。

**サーブレットエンドポイントの例：**

```java
@SlingServletPaths("/bin/migration/step1")
public class MigrationStep1Servlet extends SlingAllMethodsServlet {
    
    @Override
    protected void doPost(SlingHttpServletRequest request, 
                          SlingHttpServletResponse response) {
        String groupPath = request.getParameter("groupPath");
        String idpName = request.getParameter("idpName");

        // Check if the caller is authorized to run the servlet
        isAuthorizedCaller(request, response);

        // Get local group
        Authorizable localGroupAuth = userManager.getAuthorizableByPath(groupPath);
        Group localGroup = (Group) localGroupAuth;
        String localGroupId = localGroup.getID();
        
        // Create external group
        String externalGroupPrincipalName = localGroupId + ";" + idpName;
        // The function createExternalGroup performs the following steps:
        // 1. Creates a new external group with the given principal name (format: "<localGroupId>;<idpName>").
        // 2. Sets the 'rep:externalId' property on the group to mark it as an external group (value: "<localGroupId>;<idpName>").
        // 3. Sets the 'rep:principalName' property for the group if required.
        // 4. Assigns any other required group metadata, such as a title or description, if needed.
        // 5. Persists the new group node in the repository at the appropriate path under /home/groups.
        // 6. Returns the created Group object so it can be used for further operations, such as membership assignment.
        Group externalGroup = createExternalGroup(externalGroupPrincipalName, localGroupId, idpName);
        
        // Add external group to local group
        localGroup.addMember(externalGroup);
        
        session.save();
    }
}
```

**使用方法：**

```bash
curl -X POST "http://localhost:4503/bin/migration/step1?groupPath=/home/groups/c/content-authors&idpName=saml-idp"
```

### 手順 2: ユーザーを変換し、動的メンバーシップを割り当てる {#step-2-convert-users-and-assign-dynamic-membership}

ローカルグループのメンバーである各ユーザーに対して、次の操作を行います。

1. `rep:externalId` が設定されていることを確認します（必要に応じて外部ユーザーに変換します）。
1. グループメンバーシップごとに、対応する外部グループプリンシパルを `rep:externalPrincipalNames` に追加します。
1. 同期タイムスタンプを更新します。

>[!IMPORTANT]
>
>このプロセス中は、「全員」などのシステムグループをスキップします。

**サーブレットエンドポイントの例：**

```java
@SlingServletPaths("/bin/migration/step2")
public class MigrationStep2Servlet extends SlingAllMethodsServlet {
    
    @Override
    protected void doPost(SlingHttpServletRequest request, 
                          SlingHttpServletResponse response) {
        String userId = request.getParameter("userId");
        String idpName = request.getParameter("idpName");
        
        // Check if the caller is authorized to run the servlet
        isAuthorizedCaller(request, response);

        // Login as the service user
        Session serviceSession = repository.loginService("group-provisioner", null);

        try {
            UserManager userManager = ((JackrabbitSession) serviceSession).getUserManager();
            User user = (User) userManager.getAuthorizable(userId);
            
            // Ensure user has rep:externalId
            Value[] externalIdValues = user.getProperty("rep:externalId");
            if (externalIdValues == null || externalIdValues.length == 0) {
                ExternalIdentityRef externalRef = new ExternalIdentityRef(userId, idpName);
                user.setProperty("rep:externalId", 
                            valueFactory.createValue(externalRef.getString()));
            }
            
            // Get all group memberships
            Iterator<Group> groupIterator = user.declaredMemberOf();
            List<String> principalNames = new ArrayList<>();
            
            while (groupIterator.hasNext()) {
                Group group = groupIterator.next();
                String groupId = group.getID();
                
                // Skip system groups
                if ("everyone".equals(groupId)) {
                    continue;
                }
                
                // Add dynamic group principal
                String dynamicGroupPrincipal = groupId + ";" + idpName;
                principalNames.add(dynamicGroupPrincipal);
            }
            
            // Set rep:externalPrincipalNames
            if (!principalNames.isEmpty()) {
                Value[] newValues = new Value[principalNames.size()];
                for (int i = 0; i < principalNames.size(); i++) {
                    newValues[i] = valueFactory.createValue(principalNames.get(i));
                }
                user.setProperty("rep:externalPrincipalNames", newValues);
            }
            
            // Update timestamps to far future (workaround for OAK-12079)
            // Set to 10 years in the future to prevent premature cleanup of external group memberships
            // See: https://issues.apache.org/jira/browse/OAK-12079
            java.util.Calendar future = java.util.Calendar.getInstance();
            future.add(java.util.Calendar.YEAR, 10);
            user.setProperty("rep:lastDynamicSync", valueFactory.createValue(future));
            user.setProperty("rep:lastSynced", valueFactory.createValue(future));
        
        // Perform operations...
        serviceSession.save();
    } finally {
        if (serviceSession != null && serviceSession.isLive()) {
            serviceSession.logout();
        }
}    }
}
```

**使用方法：**

```bash
curl -X POST "http://localhost:4503/bin/migration/step2?userId=john.doe&idpName=saml-idp"
```

**検証**

これを検証するには、すべてのユーザーが `rep:externalId` 属性と `rep:externalPrincipalName` 属性を、すべての外部グループの `principalName` で持っていることを確認します。 ユーザーは、外部グループのローカルグループ *および* のメンバーです。

### 手順 3：ダイレクトユーザーメンバーシップの削除 {#step-3-remove-direct-user-memberships}

ユーザーが動的グループメンバーシップを設定した後：

1. ローカルグループからダイレクトユーザーメンバーシップを削除
1. グループ間メンバーシップ（外部グループメンバーシップを含む）を維持する

**サーブレットエンドポイントの例：**

```java
@SlingServletPaths("/bin/migration/step3")
public class MigrationStep3Servlet extends SlingAllMethodsServlet {
    
    @Override
    protected void doPost(SlingHttpServletRequest request, 
                          SlingHttpServletResponse response) {

        // Check if the caller is authorized to run the servlet
        isAuthorizedCaller(request, response);

        String groupPath = request.getParameter("groupPath");
        
        Authorizable localGroupAuth = userManager.getAuthorizableByPath(groupPath);
        Group localGroup = (Group) localGroupAuth;
        
        // Process each member
        Iterator<Authorizable> members = localGroup.getDeclaredMembers();
        
        while (members.hasNext()) {
            Authorizable member = members.next();
            
            // Remove only user members, keep group members
            if (!member.isGroup()) {
                localGroup.removeMember(member);
            }
        }
        
        session.save();
    }
}
```

**使用方法：**

```bash
curl -X POST "http://localhost:4503/bin/migration/step3?groupPath=/home/groups/c/content-authors"
```

**検証**

* これを検証するには、すべてのローカルグループが、対応する外部グループまたは他のグループのみをメンバーとして持っていることを確認します。


## 移行ワークフロー {#migration-workflow}

### 移行前のチェックリスト {#pre-migration-checklist}

* [ ]**サービスユーザーの設定**：適切な権限を持つサービスユーザー（`group-provisioner` など）を作成し設定します。
* [ ] **ExternalPrincipal 設定の確認**: `rep:externalId` および `rep:externalPrincipalNames` の保護をバイパスするようにサービスユーザーが設定されていることを確認します
* [ ]**サービスユーザー権限のテスト**：サービスユーザーが開発で外部 ID プロパティを設定できることを確認します
* [ ] ユーザーまたはグループを作成するすべてのカスタムコードを特定する
* [ ] カスタムコードを確認および更新して、外部 ID モデルを使用する
* [ ] 開発環境での更新済みコードのテスト
* [ 移行するすべての既存のローカルユーザーおよびグループを ] でインベントリします。
* [ ] 下位環境での移行プロセスのテスト

### 実行手順 {#execution-steps}

1. **更新されたコードをデプロイ**：カスタムコードの変更をデプロイして、外部ユーザー/グループを作成します

1. **外部グループの作成** （各ローカルグループに対して）:

   ```bash
   curl -X POST "http://localhost:4503/bin/migration/step1?groupPath=/home/groups/g/my-group&idpName=saml-idp"
   ```

1. **ユーザーを移行** （ユーザーごとに実行）:

   ```bash
   curl -X POST "http://localhost:4503/bin/migration/step2?userId=username&idpName=saml-idp"
   ```

1. **クリーンアップ** （移行した各グループに対して）:

   ```bash
   curl -X POST "http://localhost:4503/bin/migration/step3?groupPath=/home/groups/g/my-group"
   ```

1. **確認**: ユーザーグループのメンバーシップを確認し、アクセス権限をテストします

1. **データ同期を有効にする**：機能を有効にする場合は、カスタマーサポートにお問い合わせください

### 移行後の検証 {#post-migration-validation}

移行を確認します。

1. **ユーザープロパティの確認**:

   ユーザーノードで、以下の存在を確認します。

   * `rep:externalId`：形式は `userId;idpName` にしてください
   * `rep:externalPrincipalNames`:`groupId;idpName` 形式のグループプリンシパルの配列
   * `rep:lastSynced`：遠い将来（移行日から約 10 年）に設定されたタイムスタンプ
   * `rep:lastDynamicSync`：遠い将来（移行日から約 10 年）に設定されたタイムスタンプ

   **メモ**:OAK-12079 の回避策として、タイムスタンプは意図的に遠い将来の日付に設定されています。 これは予期された動作です。

1. **グループのプロパティを確認**:

   ローカルグループノードで、以下の存在を確認します。

   * 形式が `groupId;idpName` の外部グループ メンバー
   * 直接のユーザーメンバーなし（手順 3 の後のみ）

1. **ユーザーログインをテスト**: ユーザーがログインでき、正しい権限を持っていることを確認します

1. **アクセス制御のテスト**:CUG/ACL で保護されたコンテンツにユーザーがアクセスできることを確認します

## トラブルシューティング {#troubleshooting}

### よくある問題 {#common-issues}

**問題：`rep:externalId` または`rep:externalPrincipalNames`** を設定する際に、権限エラーが発生する

**エラーメッセージ：**

* `javax.jcr.AccessDeniedException: Access denied`
* `OakAccess0000: Access denied`
* `Cannot set property 'rep:externalId'`

**解決策**：外部の ID プロパティの保護をバイパスする権限を付与された適切に設定されたサービスユーザーを使用して、セッションを開く必要があります。

**解決手順：**

1. **サービスユーザーが存在することを確認**：サービスユーザー（`group-provisioner` など）が repoinit を使用して作成されていることを確認します
1. **サービスユーザーマッピングの確認**: サーブレットまたはサービスが `repository.loginService("group-provisioner", null)` を使用していることを確認します
1. **ExternalPrincipal 設定の検証**:`org.apache.jackrabbit.oak.spi.security.authentication.external.impl.principal.ExternalPrincipalConfiguration` が正しく設定されていることを確認します
1. **サービスユーザー権限の確認**：サービスユーザーには、`rep:write` および `rep:userManagement` に対する `/home/users` 権限と `/home/groups` 権限が必要です

設定手順について詳しくは、[ サービスユーザー設定 ](#service-user-configuration) を参照してください。

**問題：`OakConstraint0072: Property 'rep:externalPrincipalNames' requires 'rep:externalId' to be present`**

**解決策**: ユーザーは、`rep:externalId` を設定する前に `rep:externalPrincipalNames` を設定する必要があります。 最初に、手順 2 でユーザーが外部ユーザーに変換されることを確認します。

**問題：移行後、ユーザーがグループメンバーシップを失う**

**解決策**：次のことを確認します。

* 正しいプリンシパル名形式（`groupId;idpName`）で外部グループが作成されました
* 外部グループがローカル グループのメンバーとして追加されました（手順 1）
* `rep:externalPrincipalNames` でユーザーが正しい外部プリンシパル名を持っている（手順 2）
* 手順 3 のクリーンアップは、手順 1 と 2 が完了した後にのみ実行されました

**問題：ユーザーのログイン後に、外部グループメンバーシップが予期せず削除される（OAK-12079）**

**問題**: Oakのバグ [OAK-12079](https://issues.apache.org/jira/browse/OAK-12079) が原因で、Oak同期メカニズムが `rep:lastSynced` および `rep:lastDynamicSync` のタイムスタンプに基づいて外部グループメンバーシップを早めにクリーンアップする可能性があります。

**解決策**:`rep:lastSynced` および `rep:lastDynamicSync` タイムスタンプを、現在の時刻ではなく、遠い将来の日付（今から 10 年後）に設定します。 これにより、同期のクリーンアッププロセスによって外部グループメンバーシップが削除されるのを防ぐことができます。

**実装：**

```java
// Workaround for OAK-12079
// Set to 10 years in the future to prevent premature cleanup
// See: https://issues.apache.org/jira/browse/OAK-12079
java.util.Calendar future = java.util.Calendar.getInstance();
future.add(java.util.Calendar.YEAR, 10);
user.setProperty("rep:lastSynced", valueFactory.createValue(future));
user.setProperty("rep:lastDynamicSync", valueFactory.createValue(future));
```

**これが機能する理由**:Oakの同期ロジックでは、タイムスタンプを遠い将来の日付に設定することで、これらのユーザーが「最近同期された」とみなされ、外部プリンシパル名とグループメンバーシップを削除するクリーンアッププロセスはトリガーされません。

**メモ**：これは、今後のOak リリースでOAK-12079 が解決されるまで、一時的な回避策です。 このドキュメントのすべてのコード例には、この回避策が既に含まれています。

**問題：システムグループ「everyone」がエラーを引き起こす**

**解決策**：ユーザーの移行中は、常に「everyone」システムグループをスキップします（手順 2）。 このグループはAEMによって自動的に管理されます。

### ロールバック手順 {#rollback-procedure}

移行で問題が発生した場合：

1. 移行プロセスを停止
1. 重要なデータが影響を受けた場合にバックアップからリストア
1. コードの変更をロールバックして、動的グループメンバーシップを持つ外部ユーザーおよびグループを作成します
1. 移行を再試行する前に、問題を確認して修正してください。

## ベストプラクティス {#best-practices}

* **十分にテストする**：実稼動環境の前に、常に開発環境とステージング環境で移行をテストします
* **バッチ処理**：大規模なユーザーベースの場合、タイムアウトの問題を回避するために移行をバッチで処理します
* **パフォーマンスの監視**：移行中のリポジトリのパフォーマンスを監視します
* **監査記録の管理**：すべての移行操作をトラブルシューティングのために記録します
* **サービスユーザーの権限**：移行サーブレットで、必要な権限を持つ適切なサービスユーザーを使用させます。 `rep:externalId` および `rep:externalPrincipalNames` プロパティの保護をバイパスするには、サービス ユーザーが ExternalPrincipal 構成で構成されている必要があります
* **べき等の操作**：安全に再実行できるように移行コードを設計します
* **各手順での検証**：続行する前に、各移行手順の後で結果を確認してください

## 移行サーブレットの保護 {#securing-migration-servlets}

移行サーブレットは、ユーザーおよびグループを作成および変更するための管理者特権を持っています。 不正アクセスを防ぐには、これらのエンドポイントへのアクセスを制限することが重要です。

### 推奨されるアプローチ：IMS テクニカルアカウント認証 {#recommended-approach-ims-technical-account}

推奨されるアプローチは、Adobe IMS統合を使用してこれらのサーブレットを保護し、許可されたテクニカルアカウントのみがアクセスできるようにすることです。

#### 手順 1:AEM Developer Consoleでテクニカルアカウントを作成する {#create-a-technical-account-in-aem-developer-console}

1. [Experience Manager](https://experience.adobe.com/) 次に **Cloud Manager** に移動します
1. プログラムを選択し、テクニカルアカウントを作成する環境をクリックします
1. 環境の省略記号メニューで **0}Developer Console} をクリックします**
1. AEM Developer Consoleで、「**統合** タブに移動します。
1. 「**新しいテクニカルアカウントを作成**」をクリックします。
1. 統合の名前を指定します（例：「移行サービスアカウント」）
1. 「**作成**」をクリックします。
1. 作成された統合の次の値に注意してください。
   * **クライアント ID**
   * **クライアントの秘密鍵**
   * **テクニカルアカウント ID** （これは、サーブレットにアクセスするユーザー ID です – 形式：`XXXXXXXXXXXXXXXXXXXXXXXX@techacct.adobe.com`）

詳しい手順については、[ サーバーサイド API 用アクセストークンの生成ドキュメント ](/help/implementing/developing/introduction/generating-access-tokens-for-server-side-apis.md) を参照してください。

呼び出し元が認証されているかどうかを確認するためのサンプルコード：

```
    private boolean isAuthorizedCaller(SlingHttpServletRequest request, 
                                       SlingHttpServletResponse response) {

        Session session = request.getResourceResolver().adaptTo(Session.class);
        String callerId = session != null ? session.getUserID() : null;
               
        if (!ALLOWED_TECHNICAL_ACCOUNT.equals(callerId)) {
            LOG.warn("Unauthorized access attempt by user: '{}' (expected: '{}')", callerId,   ALLOWED_TECHNICAL_ACCOUNT);
            response.setStatus(SlingHttpServletResponse.SC_FORBIDDEN);
            return false;
        }
        
        return true;
    }
```

### 詳細な防御：IP ベースの制限 {#defense-in-depth-ip-based-restrictions}

セキュリティの追加のレイヤーとして、IP アドレスで移行エンドポイントへのアクセスを制限するように CDN ルールを設定できます。 これは、既知のインフラストラクチャから移行を実行する場合に役立ちます。

>[!NOTE]
>
>IP 制限だけでは不十分です。 常に、上記のように認証チェックを組み合わせます。

### セキュリティチェックリスト {#security-checklist}

移行サーブレットを実稼動環境にデプロイする前に、次の手順に従います。

* [ AEM Developer Consoleでの ] Create IMS integration
* [ テクニカルアカウント ID を検証するためのサーブレットの設定を ] 照してください
* [ ] 開発/ステージング環境での認証フローのテスト
* [ ] CDN レベルで追加の IP ベースの制限を検討する
* [ ] 移行の完了後に移行サーブレットの無効化または削除を計画
* [ ] 移行エンドポイントへのすべてのアクセスを監査して記録します

>[!IMPORTANT]
>
>移行が完了したら、潜在的なセキュリティリスクを排除するために、移行サーブレットのデプロイメントからの無効化または削除を検討してください。

## その他のリソース {#additional-resources}

* [パブリッシュ層のユーザーとグループの同期](/help/sites-cloud/authoring/personalization/user-and-group-sync-for-publish-tier.md)
* [SAML 2.0 認証ハンドラー](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/authentication/saml-2-0.html?lang=ja)
* [ 外部 ID プロバイダー ](https://jackrabbit.apache.org/oak/docs/security/authentication/externalloginmodule.html)
* [ 動的グループメンバーシップ ](https://jackrabbit.apache.org/oak/docs/security/authentication/external/dynamic.html)
