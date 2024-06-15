---
title: CDN 資格情報および認証の設定
description: 設定ファイルでルールを宣言し、Cloud Manager 設定パイプラインを使用してデプロイして、CDN 資格情報と認証を設定する方法について説明します。
feature: Dispatcher
exl-id: a5a18c41-17bf-4683-9a10-f0387762889b
source-git-commit: e6059a1109ca93452f80440744338b809279db9b
workflow-type: tm+mt
source-wordcount: '1065'
ht-degree: 98%

---

# CDN 資格情報および認証の設定 {#cdn-credentials-authentication}

>[!NOTE]
>この機能はまだ一般提供されていません。早期導入プログラムに参加するには、`aemcs-cdn-config-adopter@adobe.com` にメールを送信します。

アドビが提供する CDN には様々な機能とサービスがあり、その一部は適切なレベルのエンタープライズセキュリティを確保するために資格情報と認証に依存しています。[Cloud Manager 設定パイプライン](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md#config-deployment-pipeline)を使用してデプロイした設定ファイルでルールを宣言すると、お客様はセルフサービス方式で以下を設定できます。

* 顧客管理 CDN からのリクエストを検証するために Adobe CDN で使用される HTTP ヘッダー値。
* CDN キャッシュ内のリソースをパージするために使用される API トークン。

上記のそれぞれについては、設定の構文を含めて、以下の該当する節で説明します。[共通設定](#common-setup)の節では、両方に共通する設定とデプロイメントについて説明します。最後に、優れたセキュリティ対策と見なされている[キーのローテーション](#rotating-secrets)の方法に関する節があります。

## 顧客管理 CDN の HTTP ヘッダー値 {#CDN-HTTP-value}

[AEM as a Cloud Service の CDN](/help/implementing/dispatcher/cdn.md#point-to-point-CDN) ページの説明に従って、お客様は、顧客 CDNと呼ばれる（BYOCDN と呼ばれることもあります）独自の CDN を通じてトラフィックをルーティングすることを選択できます。

設定の一部として、Adobe CDN と顧客 CDN は、`X-AEM-Edge-Key` HTTP ヘッダーの値について合意する必要があります。この値は、リクエストが Adobe CDN にルーティングされる前に、顧客 CDN で各リクエストに対して設定され、Adobe CDN では値が期待どおりであることを検証するので、リクエストを適切な AEM 接触チャネルにルーティングするのに役立つ HTTP ヘッダーを含む他の HTTP ヘッダーを信頼できます。

`X-AEM-Edge-Key` 値は、以下の構文で宣言されます。デプロイ方法については、[共通設定](#common-setup)の節を参照してください。

```
kind: "CDN"
version: "1"
metadata:
  envTypes: ["dev"]
data:
  experimental_authentication:
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

`X-AEM-Edge-Key` 値の構文には、以下が含まれます。

* 種類、バージョン、メタデータ。
* 子 `experimental_authentication` ノードを含むデータノード（機能がリリースされると、実験的なプレフィックスは削除されます）。
* experimental_authentication の下には、1 つの認証ノードと 1 つのルールノードがあり、どちらも配列をなしています。
* オーセンティケーター：トークンまたは資格情報のタイプ（この場合はエッジキー）を宣言できます。次のプロパティが含まれます。
   * name - わかりやすい文字列。
   * type - エッジにする必要があります。
   * edgeKey1 - この値は秘密鍵トークンを参照する必要がありますが、これは git に保存するのではなく、タイプが秘密鍵の [Cloud Manager 環境変数](/help/implementing/cloud-manager/environment-variables.md)として宣言する必要があります。「適用されたサービス」フィールドで、「すべて」を選択します。値（例：`${{CDN_EDGEKEY_052824}}`）は、追加した日を反映することをお勧めします。
   * edgeKey2 - 以下の[秘密鍵のローテーション](#rotating-secrets)の節で説明する、秘密鍵のローテーションに使用します。`edgeKey1` と `edgeKey2` の 1 つ以上を宣言する必要があります。
<!--   * OnFailure - defines the action, either `log` or `block`, when a request doesn't match either `edgeKey1` or `edgeKey2`. For `log`, request processing will continue, while `block` will serve a 403 error. The `log` value is useful when testing a new token on a live site since you can first confirm that the CDN is correctly accepting the new token before changing to `block` mode; it also reduces the chance of lost connectivity between the customer CDN and the Adobe CDN, as a result of an incorrect configuration. -->
* ルール：使用するオーセンティケーターと、パブリッシュ層とプレビュー層のどちらに使用するかを宣言できます。これには以下が含まれます。
   * name - わかりやすい文字列。
   * when - [トラフィックフィルタールール](/help/security/traffic-filter-rules-including-waf.md)の記事の構文に従って、ルールを評価するタイミングを決定する条件。通常、現在の層（例：パブリッシュ）の比較が含まれるので、すべてのライブトラフィックは顧客 CDN を経由するルーティングとして検証されます。
   * action - 対象のオーセンティケーターを参照して、「authenticate」を指定する必要があります。

>[!NOTE]
>エッジキーは、参照する設定をデプロイする前に、タイプが `secret` の [Cloud Manager 環境変数](/help/implementing/cloud-manager/environment-variables.md)として設定する必要があります。

## API トークンのパージ {#purge-API-token}

顧客は次のことができます [cdn キャッシュのパージ](/help/implementing/dispatcher/cdn-cache-purge.md) 宣言されたパージ API トークンを使用する。 トークンは、以下の構文で宣言します。デプロイ方法については、[共通設定](#common-setup)の節を参照してください。

```
kind: "CDN"
version: "1"
metadata:
  envTypes: ["dev"]
data:
  experimental_authentication:
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

構文の内容は次のとおりです。

* 種類、バージョン、メタデータ。
* 子 `experimental_authentication` ノードを含むデータノード（機能がリリースされると、実験的なプレフィックスは削除されます）。
* `experimental_authentication` の下に、オーセンティケーターノードが 1 つあります。
* オーセンティケーター：トークンまたは資格情報のタイプ（この場合はパージキー）を宣言できます。次のプロパティが含まれます。
   * name - わかりやすい文字列。
   * type - パージする必要があります。
   * purgeKey1 - この値は秘密鍵トークンを参照する必要がありますが、これは git に保存するのではなく、タイプが `secret` の [Cloud Manager 環境変数](/help/implementing/cloud-manager/environment-variables.md)として宣言する必要があります。
   * 「適用されたサービス」フィールドで、「すべて」を選択します。値（例：`${{CDN_PURGEKEY_031224}}`）は、追加した日を反映することをお勧めします。
   * purgeKey2 - 以下の[秘密鍵のローテーション](#rotating-secrets)の節で説明する、秘密鍵のローテーションに使用します。`purgeKey1` と `purgeKey2` の 1 つ以上を宣言する必要があります。
* ルール：使用するオーセンティケーターと、パブリッシュ層とプレビュー層のどちらに使用するかを宣言できます。これには以下が含まれます。
   * name - わかりやすい文字列
   * when - [トラフィックフィルタールール](/help/security/traffic-filter-rules-including-waf.md)の記事の構文に従って、ルールを評価するタイミングを決定する条件。通常、現在の層（例：パブリッシュ）の比較が含まれます。
   * action - 対象のオーセンティケーターを参照して、「authenticate」を指定する必要があります。

>[!NOTE]
>参照する設定をデプロイする前に、エッジキーを、`secret` タイプの [Cloud Manager 環境変数](/help/implementing/cloud-manager/environment-variables.md)として設定する必要があります。

## 共通設定 {#common-setup}

すべてのオーセンティケーターを次のように設定します。

* まず、Git プロジェクトの最上位フォルダーに次のフォルダーとファイル構造を作成します。

```
config/
     cdn.yaml
```

* 次に、`cdn.yaml` 設定ファイルには、以下の例で説明するノードを含める必要があります。`kind` プロパティは `CDN` に設定し、バージョンはスキーマバージョン（現在 `1`）に設定する必要があります。メタデータノードには「envTypes」プロパティがあり、この設定が評価される環境タイプ（開発、ステージ、実稼動）を示します。

* 最後に、Cloud Manager でターゲットデプロイメント設定パイプラインを作成します。[実稼動パイプラインの設定](/help/implementing/cloud-manager/configuring-pipelines/configuring-production-pipelines.md)および[実稼動以外のパイプラインの設定](/help/implementing/cloud-manager/configuring-pipelines/configuring-non-production-pipelines.md)を参照してください。

以下の点に注意してください。

* RDE は現在、設定パイプラインをサポートしていません。
* `yq` を使用すると、設定ファイル（例：`yq cdn.yaml`）の YAML 形式をローカルで検証できます。

## 秘密鍵のローテーション {#rotating-secrets}

優れたセキュリティ対策として、資格情報を時々変更することをお勧めします。これは、エッジキーの例を使用して以下に示すように実現できますが、パージキーにも同じ戦略が使用されます。

* 最初は `edgeKey1` のみが定義され、この場合は `${{CDN_EDGEKEY_052824}}` として参照されます。これは、推奨される規則として、作成日を反映しています。

```
experimental_authentication:
  authenticators:
    - name: edge-auth
      type: edge
      edgeKey1: ${{CDN_EDGEKEY_052824}}
```

* キーをローテーションする際は、新しい Cloud Manager 秘密鍵（例：`${{CDN_EDGEKEY_041425}}`）を作成します。
* 設定では、`edgeKey2` から参照してデプロイします。

```
experimental_authentication:
  authenticators:
    - name: edge-auth
      type: edge
      edgeKey1: ${{CDN_EDGEKEY_052824}}
      edgeKey2: ${{CDN_EDGEKEY_041425}}
```

* 古いエッジキーが使用されていないことを確認したら、設定から `edgeKey1` を削除してエッジキーを削除します。

```
experimental_authentication:
  authenticators:
    - name: edge-auth
      type: edge
      edgeKey2: ${{CDN_EDGEKEY_041425}}
```

* Cloud Manager から古い秘密鍵参照（`${{CDN_EDGEKEY_052824}}`）を削除してデプロイします。
* 次のローテーションの準備が整ったら、同じ手順に従いますが、今回は `edgeKey1` を設定に追加し、例えば、`${{CDN_EDGEKEY_031426}}` という名前の新しい Cloud Manager 環境の秘密鍵を参照します。

```
experimental_authentication:
  authenticators:
    - name: edge-auth
      type: edge
      edgeKey2: ${{CDN_EDGEKEY_041425}}
      edgeKey1: ${{CDN_EDGEKEY_031426}}
```
