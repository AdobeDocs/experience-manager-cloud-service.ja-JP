---
title: CDN 資格情報および認証の設定
description: ルールを設定ファイルで宣言し、そのファイルをCloud Manager設定パイプラインを使用してデプロイすることで、CDN 資格情報および認証を設定する方法を説明します。
feature: Dispatcher
exl-id: a5a18c41-17bf-4683-9a10-f0387762889b
role: Admin
source-git-commit: 3a10a0b8c89581d97af1a3c69f1236382aa85db0
workflow-type: tm+mt
source-wordcount: '1271'
ht-degree: 66%

---


# CDN 資格情報および認証の設定 {#cdn-credentials-authentication}

アドビが提供する CDN には様々な機能とサービスがあり、その一部は適切なレベルのエンタープライズセキュリティを確保するために資格情報と認証に依存しています。Cloud Manager [config パイプラインを使用してデプロイされた設定ファイルでルールを宣言することで ](/help/operations/config-pipeline.md) お客様は、セルフサービス方式で以下を設定できます。

* 顧客が管理する CDN からのリクエストを検証するためにAdobeCDN で使用される X-AEM-Edge-Key HTTP ヘッダー値。
* CDN キャッシュ内のリソースをパージするために使用される API トークン。
* 基本認証フォームを送信して、制限されたコンテンツにアクセスできるユーザー名とパスワードの組み合わせのリスト。 [ この機能は、早期導入ユーザーが使用できます。](/help/release-notes/release-notes-cloud/release-notes-current.md#foundation-early-adopter)

設定の構文を含む各オプションについては、以下の該当する節で説明します。

[ キーの回転 ](#rotating-secrets) の方法に関する節があり、これは優れたセキュリティ対策です。

## 顧客管理 CDN の HTTP ヘッダー値 {#CDN-HTTP-value}

[AEM as a Cloud Service の CDN](/help/implementing/dispatcher/cdn.md#point-to-point-CDN) ページの説明に従って、お客様は、顧客 CDNと呼ばれる（BYOCDN と呼ばれることもあります）独自の CDN を通じてトラフィックをルーティングすることを選択できます。

設定の一部として、Adobe CDN と顧客 CDN は、`X-AEM-Edge-Key` HTTP ヘッダーの値について合意する必要があります。この値は、リクエストが Adobe CDN にルーティングされる前に、顧客 CDN で各リクエストに対して設定され、Adobe CDN では値が期待どおりであることを検証するので、リクエストを適切な AEM 接触チャネルにルーティングするのに役立つ HTTP ヘッダーを含む他の HTTP ヘッダーを信頼できます。

*X-AEM-Edge-Key* の値は、最上位の `config` フォルダーの下の `cdn.yaml` などの名前のファイル内で、`edgeKey1` プロパティと `edgeKey2` プロパティによって参照されます。 フォルダー構造と設定のデプロイ方法について詳しくは、[ 設定パイプライン ](/help/operations/config-pipeline.md#folder-structure) を参照してください。

構文は以下のとおりです。

```
kind: "CDN"
version: "1"
metadata:
  envTypes: ["dev"]
data:
  authentication:
    authenticators:
      - name: edge-auth
        type: edge
        edgeKey1: ${{CDN_EDGEKEY_052824}}
        edgeKey2: ${{CDN_EDGEKEY_041425}}
    rules:
      - name: edge-auth-rule
        when: { reqProperty: tier, equals: "publish" }
        action:
          type: authenticate
          authenticator: edge-auth
```

`data` ノードの上のプロパティの説明については、[ 設定パイプライン ](/help/operations/config-pipeline.md#common-syntax) の記事を参照してください。 `kind` プロパティの値は *CDN* にし、`version` プロパティは `1` に設定する必要があります。

その他のプロパティは次のとおりです。

* `authentication``Data` 子ノードを含むノード。
* `authentication` の下には、1 つの `authenticators` ノードと 1 つの `rules` ノードがあり、どちらも配列をなしています。
* オーセンティケーター：トークンまたは資格情報のタイプ（この場合はエッジキー）を宣言できます。次のプロパティが含まれます。
   * name - わかりやすい文字列。
   * type - `edge` にする必要があります。
   * edgeKey1 - *X-AEM-Edge-Key* の値。[Cloud Managerの秘密鍵タイプの環境変数 ](/help/operations/config-pipeline.md#secret-env-vars) を参照する必要があります。 「適用されたサービス」フィールドで、「すべて」を選択します。値（例：`${{CDN_EDGEKEY_052824}}`）は、追加した日を反映することをお勧めします。
   * edgeKey2 - 以下の[秘密鍵のローテーション](#rotating-secrets)の節で説明する、秘密鍵のローテーションに使用します。edgeKey1 と同様に定義します。`edgeKey1` と `edgeKey2` の 1 つ以上を宣言する必要があります。
<!--   * OnFailure - defines the action, either `log` or `block`, when a request doesn't match either `edgeKey1` or `edgeKey2`. For `log`, request processing will continue, while `block` will serve a 403 error. The `log` value is useful when testing a new token on a live site since you can first confirm that the CDN is correctly accepting the new token before changing to `block` mode; it also reduces the chance of lost connectivity between the customer CDN and the Adobe CDN, as a result of an incorrect configuration. -->
* ルール：使用するオーセンティケーターと、パブリッシュ層とプレビュー層のどちらに使用するかを宣言できます。これには以下が含まれます。
   * name - わかりやすい文字列。
   * when - [トラフィックフィルタールール](/help/security/traffic-filter-rules-including-waf.md)の記事の構文に従って、ルールを評価するタイミングを決定する条件。通常、現在の層（例：パブリッシュ）の比較が含まれるので、すべてのライブトラフィックは顧客 CDN を経由するルーティングとして検証されます。
   * action - 対象のオーセンティケーターを参照して、「authenticate」を指定する必要があります。

>[!NOTE]
>Edge キーは、それを参照する設定をデプロイする前に、[ 秘密鍵タイプのCloud Manager環境変数 ](/help/operations/config-pipeline.md#secret-env-vars) として設定する必要があります。

## API トークンのパージ {#purge-API-token}

お客様は、宣言されたパージ API トークンを使用して [CDN キャッシュをパージ](/help/implementing/dispatcher/cdn-cache-purge.md)できます。トークンは、`cdn.yaml` などの名前のファイルで、最上位の `config` フォルダーの下のどこかに宣言されます。 フォルダー構造と設定のデプロイ方法について詳しくは、[config パイプライン ](/help/operations/config-pipeline.md#folder-structure) を参照してください。

構文は以下のとおりです。

```
kind: "CDN"
version: "1"
metadata:
  envTypes: ["dev"]
data:
  authentication:
    authenticators:
       - name: purge-auth
         type: purge
         purgeKey1: ${{CDN_PURGEKEY_031224}}
         purgeKey2: ${{CDN_PURGEKEY_021225}}
    rules:
       - name: purge-auth-rule
         when: { reqProperty: tier, equals: "publish" }
         action:
           type: authenticate
           authenticator: purge-auth
```

`data` ノードの上のプロパティの説明については、[config パイプライン ](/help/operations/config-pipeline.md#common-syntax) の記事を参照してください。 `kind` プロパティの値は *CDN* にし、`version` プロパティは `1` に設定する必要があります。

その他のプロパティは次のとおりです。

* `authentication``data` 子ノードを含むノード。
* `authentication` の下には、1 つの `authenticators` ノードと 1 つの `rules` ノードがあり、どちらも配列をなしています。
* オーセンティケーター：トークンまたは資格情報のタイプ（この場合はパージキー）を宣言できます。次のプロパティが含まれます。
   * name - わかりやすい文字列。
   * type - パージする必要があります。
   * purgeKey1 – この値は、[Cloud Manager秘密鍵タイプの環境変数 ](/help/operations/config-pipeline.md#secret-env-vars) を参照する必要があります。 「適用されたサービス」フィールドで、「すべて」を選択します。値（例：`${{CDN_PURGEKEY_031224}}`）は、追加した日を反映することをお勧めします。
   * purgeKey2 - 以下の[秘密鍵のローテーション](#rotating-secrets)の節で説明する、秘密鍵のローテーションに使用します。`purgeKey1` と `purgeKey2` の 1 つ以上を宣言する必要があります。
* ルール：使用するオーセンティケーターと、パブリッシュ層とプレビュー層のどちらに使用するかを宣言できます。これには以下が含まれます。
   * name - わかりやすい文字列
   * when - [トラフィックフィルタールール](/help/security/traffic-filter-rules-including-waf.md)の記事の構文に従って、ルールを評価するタイミングを決定する条件。通常、現在の層（例：パブリッシュ）の比較が含まれます。
   * action - 対象のオーセンティケーターを参照して、「authenticate」を指定する必要があります。

>[!NOTE]
>パージキーは、それを参照する設定をデプロイする前に、[ 秘密鍵タイプのCloud Manager環境変数 ](/help/operations/config-pipeline.md#secret-env-vars) として設定される必要があります。

## 基本認証 {#basic-auth}

>[!NOTE]
>この機能はまだ一般提供されていません。早期導入プログラムに参加するには、`aemcs-cdn-config-adopter@adobe.com` にメールを送信します。

ユーザー名とパスワードの入力を求める基本認証ダイアログを表示して、特定のコンテンツリソースを保護します。この機能は、エンドユーザーのアクセス権に対する本格的なソリューションではなく、主にビジネス関係者によるコンテンツのレビューなどの軽い認証ユースケースを対象としています。

エンドユーザーには、次のような基本認証ダイアログがポップアップ表示されます。

![基本認証ダイアログ](/help/implementing/dispatcher/assets/basic-auth-dialog.png)


構文は次のようになります。

```
kind: "CDN"
version: "1"
metadata:
  envTypes: ["dev"]
data:
  experimental_authentication:
    authenticators:
       - name: my-basic-authenticator
         type: basic
         credentials:
           - user: johndoe
             password: ${{JOHN_DOE_PASSWORD}}
           - user: janedoe
             password: ${{JANE_DOE_PASSWORD}}
    rules:
       - name: basic-auth-rule
         when: { reqProperty: path, like: "/summercampaign" }
         action:
           type: authenticate
           authenticator: my-basic-authenticator
```

`data` ノードの上のプロパティの説明については、[config パイプライン ](/help/operations/config-pipeline.md#common-syntax) の記事を参照してください。 `kind` プロパティの値は *CDN* にし、`version` プロパティは `1` に設定する必要があります。

さらに、構文には次のものが含まれます。

* `experimental_authentication` ノードを含む `data` ノード（実験的プレフィックスは機能がリリースされると削除されます）。
* `experimental_authentication` の下には、1 つの `authenticators` ノードと 1 つの `rules` ノードがあり、どちらも配列をなしています。
* オーセンティケーター：このシナリオでは、次の構造を持つ基本オーセンティケーターの宣言を行います。
   * name - わかりやすい文字列
   * type - `basic` にする必要があります
   * 資格情報の配列。各資格情報には、次の名前と値のペアが含まれ、エンドユーザーは基本認証ダイアログで入力できます。
      * user - ユーザーの名前
      * password – その値は、サービスフィールドとして **All** が選択された [Cloud Managerの秘密鍵タイプの環境変数 ](/help/operations/config-pipeline.md#secret-env-vars) を参照する必要があります。
* ルール：使用するオーセンティケーターと、保護するリソースのどちらに使用するかを宣言できます。各ルールには、以下が含まれます。
   * name - わかりやすい文字列
   * when - [トラフィックフィルタールール](/help/security/traffic-filter-rules-including-waf.md)の記事の構文に従って、ルールを評価するタイミングを決定する条件。通常、パブリッシュ層または特定のパスの比較が含まれます。
   * action - 対象のオーセンティケーター（このシナリオでは basic-auth）を参照して、「authenticate」を指定する必要があります。

>[!NOTE]
>パスワードを参照する設定をデプロイする前に、パスワードを [ 秘密鍵タイプのCloud Manager環境変数 ](/help/operations/config-pipeline.md#secret-env-vars) として設定する必要があります。

## 秘密鍵のローテーション {#rotating-secrets}

1. 優れたセキュリティ対策として、資格情報を時々変更することをお勧めします。これは、エッジキーの例を使用して以下に示すように実現できますが、パージキーにも同じ戦略が使用されます。

1. 最初は `edgeKey1` のみが定義され、この場合は `${{CDN_EDGEKEY_052824}}` として参照されます。これは、推奨される規則として、作成日を反映しています。

   ```
   experimental_authentication:
     authenticators:
       - name: edge-auth
         type: edge
         edgeKey1: ${{CDN_EDGEKEY_052824}}
   ```
1. キーをローテーションする際は、新しい Cloud Manager 秘密鍵（例：`${{CDN_EDGEKEY_041425}}`）を作成します。
1. 設定では、`edgeKey2` から参照してデプロイします。

   ```
   experimental_authentication:
     authenticators:
       - name: edge-auth
         type: edge
         edgeKey1: ${{CDN_EDGEKEY_052824}}
         edgeKey2: ${{CDN_EDGEKEY_041425}}
   ```

1. 古いエッジキーが使用されていないことを確認したら、設定から `edgeKey1` を削除してエッジキーを削除します。

   ```
   experimental_authentication:
     authenticators:
       - name: edge-auth
         type: edge
         edgeKey2: ${{CDN_EDGEKEY_041425}}
   ```
1. Cloud Manager から古い秘密鍵参照（`${{CDN_EDGEKEY_052824}}`）を削除してデプロイします。

1. 次のローテーションの準備が整ったら、同じ手順に従いますが、今回は `edgeKey1` を設定に追加し、例えば、`${{CDN_EDGEKEY_031426}}` という名前の新しい Cloud Manager 環境の秘密鍵を参照します。

   ```
   experimental_authentication:
     authenticators:
       - name: edge-auth
         type: edge
         edgeKey2: ${{CDN_EDGEKEY_041425}}
         edgeKey1: ${{CDN_EDGEKEY_031426}}
   ```
