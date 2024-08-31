---
title: CDN 資格情報および認証の設定
description: 設定ファイルでルールを宣言し、Cloud Manager 設定パイプラインを使用してデプロイして、CDN 資格情報と認証を設定する方法について説明します。
feature: Dispatcher
exl-id: a5a18c41-17bf-4683-9a10-f0387762889b
role: Admin
source-git-commit: c8059260ab0ff13ed85f55eda2e09ca5cb678fa9
workflow-type: tm+mt
source-wordcount: '1379'
ht-degree: 91%

---


# CDN 資格情報および認証の設定 {#cdn-credentials-authentication}

アドビが提供する CDN には様々な機能とサービスがあり、その一部は適切なレベルのエンタープライズセキュリティを確保する資格情報と認証に依存しています。Cloud Manager [設定パイプライン](/help/operations/config-pipeline.md)を使用してデプロイした設定ファイルでルールを宣言すると、お客様はセルフサービス方式で次を設定できます。

* 顧客管理 CDN からのリクエストを検証する Adobe CDN で使用される X-AEM-Edge-Key HTTP ヘッダー値。
* CDN キャッシュ内のリソースのパージに使用される API トークン。
* 基本認証フォームを送信することで、制限されたコンテンツにアクセスできるユーザー名／パスワードの組み合わせのリスト。[この機能は、早期導入者が使用できます。](/help/release-notes/release-notes-cloud/release-notes-current.md#foundation-early-adopter)

上記のそれぞれについては、設定の構文を含めて、以下の該当する節で説明します。

優れたセキュリティ対策である[キーのローテーション](#rotating-secrets)の方法に関する節があります。

## 顧客管理 CDN の HTTP ヘッダー値 {#CDN-HTTP-value}

[AEM as a Cloud Service の CDN](/help/implementing/dispatcher/cdn.md#point-to-point-CDN) ページの説明に従って、お客様は、顧客 CDNと呼ばれる（BYOCDN と呼ばれることもあります）独自の CDN を通じてトラフィックをルーティングすることを選択できます。

設定の一部として、Adobe CDN と顧客 CDN は、`X-AEM-Edge-Key` HTTP ヘッダーの値について合意する必要があります。この値は、リクエストが Adobe CDN にルーティングされる前に、顧客 CDN で各リクエストに対して設定され、Adobe CDN では値が期待どおりであることを検証するので、リクエストを適切な AEM 接触チャネルにルーティングするのに役立つ HTTP ヘッダーを含む他の HTTP ヘッダーを信頼できます。

*X-AEM-Edge-Key* 値は、最上位レベルの `config` フォルダーの下にある `cdn.yaml` または類似の名前のファイル内の `edgeKey1` プロパティと `edgeKey2` プロパティによって参照されます。フォルダー構造と設定のデプロイ方法について詳しくは、[設定パイプラインの使用](/help/operations/config-pipeline.md#folder-structure)を参照してください。

構文は次のとおりです。

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

`data` ノード上のプロパティの説明について詳しくは、[設定パイプラインの使用](/help/operations/config-pipeline.md#common-syntax)を参照してください。`kind` プロパティの値は *CDN* に設定し、`version` プロパティは `1` に設定する必要があります。

その他のプロパティには次が含まれます。

* 子 `authentication` ノードを含む `Data` ノード。
* `authentication` の下には、1 つの `authenticators` ノードと 1 つの `rules` ノードがあり、どちらも配列をなしています。
* オーセンティケーター：トークンまたは資格情報のタイプ（この場合はエッジキー）を宣言できます。次のプロパティが含まれます。
   * name - わかりやすい文字列。
   * type - `edge` にする必要があります。
   * edgeKey1 - *X-AEM-Edge-Key* の値。[Cloud Manager 秘密鍵タイプの環境変数](/help/operations/config-pipeline.md#secret-env-vars)を参照する必要があります。「適用されたサービス」フィールドで、「すべて」を選択します。値（例：`${{CDN_EDGEKEY_052824}}`）は、追加した日を反映することをお勧めします。
   * edgeKey2 - 以下の[秘密鍵のローテーション](#rotating-secrets)の節で説明する、秘密鍵のローテーションに使用します。edgeKey1 と同様に定義します。`edgeKey1` と `edgeKey2` の 1 つ以上を宣言する必要があります。
<!--   * OnFailure - defines the action, either `log` or `block`, when a request doesn't match either `edgeKey1` or `edgeKey2`. For `log`, request processing will continue, while `block` will serve a 403 error. The `log` value is useful when testing a new token on a live site since you can first confirm that the CDN is correctly accepting the new token before changing to `block` mode; it also reduces the chance of lost connectivity between the customer CDN and the Adobe CDN, as a result of an incorrect configuration. -->
* ルール：使用するオーセンティケーターと、パブリッシュ層とプレビュー層のどちらに使用するかを宣言できます。これには以下が含まれます。
   * name - わかりやすい文字列。
   * when - [トラフィックフィルタールール](/help/security/traffic-filter-rules-including-waf.md)の記事の構文に従って、ルールを評価するタイミングを決定する条件。通常、現在の層（例：パブリッシュ）の比較が含まれるので、すべてのライブトラフィックは顧客 CDN を経由するルーティングとして検証されます。
   * action - 対象のオーセンティケーターを参照して、「authenticate」を指定する必要があります。

>[!NOTE]
>参照する設定をデプロイする前に、Edge Key を、[秘密鍵タイプの Cloud Manager 環境変数](/help/operations/config-pipeline.md#secret-env-vars)として設定する必要があります。

### 安全に移行してトラフィックのブロックのリスクを軽減 {#migrating-safely}

サイトがすでに実稼働している場合、設定の誤りが公開トラフィックをブロックする可能性があるので、顧客が管理する CDN への移行には注意が必要です。これは、想定される X-AEM-Edge-Key ヘッダー値を持つリクエストのみがAdobe CDN で受け入れられるからです。 テストヘッダーが含まれる場合にのみリクエストを評価する原因となる、追加の条件が認証ルールに一時的に含まれる場合は、このアプローチをお勧めします。

```
    - name: edge-auth-rule
        when:
          allOf:  
            - { reqProperty: tier, equals: "publish" }
            - { reqHeader: x-edge-test, equals: "test" }
        action:
          type: authenticate
          authenticator: edge-auth
```

次の `curl` リクエストパターンを使用できます。

```
curl https://publish-p<PROGRAM_ID>-e<ENV-ID>.adobeaemcloud.com -H "X-Forwarded-Host: example.com" -H "X-AEM-Edge-Key: <CONFIGURED_EDGE_KEY>" -H "x-edge-test: test"
```

正常にテストされたら、追加の条件を削除して、設定を再デプロイできます。

## API トークンのパージ {#purge-API-token}

お客様は、宣言されたパージ API トークンを使用して [CDN キャッシュをパージ](/help/implementing/dispatcher/cdn-cache-purge.md)できます。トークンは、最上位レベルの `config` フォルダーの下にある `cdn.yaml` または類似の名前のファイルで宣言されます。フォルダー構造と設定のデプロイ方法について詳しくは、[設定パイプラインの使用](/help/operations/config-pipeline.md#folder-structure)を参照してください。

構文は次のとおりです。

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

`data` ノード上のプロパティの説明について詳しくは、[設定パイプラインの使用](/help/operations/config-pipeline.md#common-syntax)を参照してください。`kind` プロパティの値は *CDN* に設定し、`version` プロパティは `1` に設定する必要があります。

その他のプロパティには次が含まれます。

* 子 `authentication` ノードを含む `data` ノード。
* `authentication` の下には、1 つの `authenticators` ノードと 1 つの `rules` ノードがあり、どちらも配列をなしています。
* オーセンティケーター：トークンまたは資格情報のタイプ（この場合はパージキー）を宣言できます。次のプロパティが含まれます。
   * name - わかりやすい文字列。
   * type - パージする必要があります。
   * purgeKey1 - この値は、[Cloud Manager 秘密鍵タイプの環境変数](/help/operations/config-pipeline.md#secret-env-vars)を参照する必要があります。「適用されたサービス」フィールドで、「すべて」を選択します。値（例：`${{CDN_PURGEKEY_031224}}`）は、追加した日を反映することをお勧めします。
   * purgeKey2 - 以下の[秘密鍵のローテーション](#rotating-secrets)の節で説明する、秘密鍵のローテーションに使用します。`purgeKey1` と `purgeKey2` の 1 つ以上を宣言する必要があります。
* ルール：使用するオーセンティケーターと、パブリッシュ層とプレビュー層のどちらに使用するかを宣言できます。これには以下が含まれます。
   * name - わかりやすい文字列
   * when - [トラフィックフィルタールール](/help/security/traffic-filter-rules-including-waf.md)の記事の構文に従って、ルールを評価するタイミングを決定する条件。通常、現在の層（例：パブリッシュ）の比較が含まれます。
   * action - 対象のオーセンティケーターを参照して、「authenticate」を指定する必要があります。

>[!NOTE]
>参照する設定をデプロイする前に、パージキーを、[秘密鍵タイプの Cloud Manager 環境変数](/help/operations/config-pipeline.md#secret-env-vars)として設定する必要があります。

パージキーの設定と CDN キャッシュパージの実行に焦点を当てた [ チュートリアル ](https://experienceleague.adobe.com/en/docs/experience-manager-learn/cloud-service/caching/how-to/purge-cache) を参照してください。

## 基本認証 {#basic-auth}

>[!NOTE]
>この機能はまだ一般提供されていません。早期導入プログラムに参加するには、`aemcs-cdn-config-adopter@adobe.com` にメールを送信します。

ユーザー名とパスワードの入力を求める基本認証ダイアログを表示して、特定のコンテンツリソースを保護します。この機能は、エンドユーザーのアクセス権に対する本格的なソリューションではなく、主にビジネス関係者によるコンテンツのレビューなどの軽い認証ユースケースを対象としています。

エンドユーザーには、次のような基本認証ダイアログがポップアップ表示されます。

![基本認証ダイアログ](/help/implementing/dispatcher/assets/basic-auth-dialog.png)


構文は次のとおりです。

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

`data` ノード上のプロパティの説明について詳しくは、[設定パイプラインの使用](/help/operations/config-pipeline.md#common-syntax)を参照してください。`kind` プロパティの値は *CDN* に、`version` プロパティは `1` に設定する必要があります。

さらに、構文には次のものが含まれます。

* `experimental_authentication` ノードを含む `data` ノード（機能がリリースされると、実験的なプレフィックスは削除されます）。
* `experimental_authentication` の下には、1 つの `authenticators` ノードと 1 つの `rules` ノードがあり、どちらも配列をなしています。
* オーセンティケーター：このシナリオでは、次の構造を持つ基本オーセンティケーターの宣言を行います。
   * name - わかりやすい文字列
   * type - `basic` にする必要があります
   * 資格情報の配列。各資格情報には、次の名前と値のペアが含まれ、エンドユーザーは基本認証ダイアログで入力できます。
      * user - ユーザーの名前
      * password - この値は、サービスフィールドで「**すべて**」が選択された、[Cloud Manager 秘密鍵タイプの環境変数](/help/operations/config-pipeline.md#secret-env-vars)を参照する必要があります。
* ルール：使用するオーセンティケーターと、保護するリソースのどちらに使用するかを宣言できます。各ルールには、以下が含まれます。
   * name - わかりやすい文字列
   * when - [トラフィックフィルタールール](/help/security/traffic-filter-rules-including-waf.md)の記事の構文に従って、ルールを評価するタイミングを決定する条件。通常、パブリッシュ層または特定のパスの比較が含まれます。
   * action - 対象のオーセンティケーター（このシナリオでは basic-auth）を参照して、「authenticate」を指定する必要があります。

>[!NOTE]
>参照する設定をデプロイする前に、パスワードを、[秘密鍵タイプの Cloud Manager 環境変数](/help/operations/config-pipeline.md#secret-env-vars)として設定する必要があります。

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
