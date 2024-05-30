---
title: CDN 資格情報と認証の設定
description: ルールを設定ファイルで宣言し、そのファイルを Cloud Manager 設定パイプラインを使用してデプロイすることで、CDN 資格情報と認証を設定する方法を説明します。
feature: Dispatcher
source-git-commit: ee993798739232da794dbf7ff0a643ca93effa7d
workflow-type: tm+mt
source-wordcount: '1143'
ht-degree: 3%

---

# CDN 資格情報と認証の設定 {#cdn-credentials-authentication}

>[!NOTE]
>この機能はまだ一般提供されていません。早期導入プログラムに参加するには、次のメールを送信します `aemcs-cdn-config-adopter@adobe.com`.

Adobe提供の CDN には、いくつかの機能とサービスがあり、一部は、適切なレベルのエンタープライズセキュリティを確保するために資格情報と認証に依存しています。 を使用してデプロイされた設定ファイルでルールを宣言する [Cloud Manager 設定パイプライン](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md#config-deployment-pipeline)の顧客は、セルフサービス方式で以下を設定できます。

* 顧客が管理する CDN からのリクエストを検証するためにAdobe CDN で使用される HTTP ヘッダー値。
* CDN キャッシュ内のリソースをパージするために使用される API トークン。

設定の構文を含む各オプションについては、以下の該当する節で説明します。 この [共通設定](#common-setup) この節では、両方に共通の設定とデプロイメントを示します。 最後に、その方法について説明します [キーを回転](#rotating-secrets)これは、優れたセキュリティ対策と見なされます。

## 顧客の管理による CDN HTTP ヘッダー値 {#CDN-HTTP-value}

で説明されているように [AEMの CDNas a Cloud Service](/help/implementing/dispatcher/cdn.md#point-to-point-CDN) ページでは、お客様は、顧客 CDN （BYOCDN とも呼ばれます）と呼ばれる独自の CDN を介してトラフィックをルーティングすることを選択できます。

設定の一環として、AdobeCDN と顧客 CDN は、次の値について合意する必要があります `X-AEM-Edge-Key` HTTP ヘッダー。 この値は、AdobeCDN でリクエストごとに設定され、顧客 CDN にルーティングされる前に設定され、その後、値が期待どおりであることを検証するので、リクエストを適切なAEM オリジンにルーティングするのに役立つヘッダーなど、他の HTTP ヘッダーを信頼できます。

この `X-AEM-Edge-Key` 値は、以下の構文で宣言されます。 を参照してください。 [共通設定](#common-setup) デプロイ方法については、を参照してください。

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
        onFailure: log # optional, default: log, enum: log/block
    rules:
      - name: edge-auth-rule
        when: { reqProperty: tier, equals: "publish" }
        action:
          type: authenticate
          authenticator: edge-auth
```

の構文 `X-AEM-Edge-Key` 値には次が含まれます。

* 種類、バージョン、メタデータ。
* 子を含むデータノード `experimental_authentication` ノード（実験的プレフィックスは機能がリリースされると削除されます）。
* experimental_authentication では、1 つの認証ノードと 1 つのルールノードを使用します。どちらも配列です。
* 認証者：トークンまたは認証情報（この場合はエッジキー）の種類を宣言できます。 これには次のプロパティが含まれます。
   * 名前 – わかりやすい文字列。
   * タイプ – エッジである必要があります。
   * edgeKey1 – その値は、秘密鍵トークンを参照する必要があります。これは git に保存してはならず、として宣言する必要があります。 [Cloud Manager 環境変数](/help/implementing/cloud-manager/environment-variables.md) タイプが秘密鍵です。 「適用されたサービス」フィールドで、「すべて」を選択します。 値（例：）を指定することをお勧めします`${{CDN_EDGEKEY_052824}}`）には、追加された日が反映されます。
   * edgeKey2 – 秘密鍵の回転に使用されます。これについては、で説明します。 [回転，シークレット セクション](#rotating-secrets) 下。 次のうち少なくとも 1 つ `edgeKey1` および `edgeKey2` を宣言する必要があります。
   * OnFailure - アクションを定義します。 `log` または `block`、リクエストも一致しない場合 `edgeKey1` または `edgeKey2`. の場合 `log`、リクエスト処理は続行されます。その間は `block` は 403 エラーを返します。 この `log` 値は、ライブサイトで新しいトークンをテストする際に便利です。CDN がに変更される前に、新しいトークンを正しく受け入れていることを最初に確認できるからです `block` また、設定が正しくないために顧客 CDN とAdobe CDN の間の接続が失われる可能性も低くなります。
* ルール：使用する認証システムと、パブリッシュ層とプレビュー層のどちらに使用するかを宣言できます。  これには以下が含まれます。
   * 名前 – わかりやすい文字列。
   * when – 構文に従って、ルールを評価するタイミングを決定する条件 [トラフィックフィルタールール](/help/security/traffic-filter-rules-including-waf.md) 記事。 通常は、現在の層（例：公開）の比較が含まれるので、すべてのライブトラフィックは顧客 CDN を介したルーティングとして検証されます。
   * アクション – 「authenticate」を指定し、対象の認証システムを参照する必要があります。

>[!NOTE]
>エッジキーはとして設定する必要があります [Cloud Manager 環境変数](/help/implementing/cloud-manager/environment-variables.md) タイプの変数 `secret`を参照する設定がデプロイされる前に行います。

## API トークンの削除 {#purge-API-token}

お客様は、宣言されたパージ API トークンを使用して CDN キャッシュをパージできます。 トークンは、以下の構文で宣言します。  を参照してください。 [共通設定](#common-setup) デプロイ方法については、を参照してください。

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
* 子を含むデータノード `experimental_authentication` ノード（実験的プレフィックスは機能がリリースされると削除されます）。
* 次の下 `experimental_authentication`（1 つの authenticators ノードを使用）。
* Authenticators：特定の種類のトークンまたは証明書（この場合はパージキー）を宣言できます。 これには次のプロパティが含まれます。
   * 名前 – わかりやすい文字列。
   * タイプ – パージする必要があります。
   * purgeKey1 – その値は、秘密鍵トークンを参照する必要があります。秘密鍵トークンは Git に保存せず、次のように宣言する必要があります。 [Cloud Manager 環境変数](/help/implementing/cloud-manager/environment-variables.md) タイプの `secret`.
   * 「適用されたサービス」フィールドで、「すべて」を選択します。 値（例：）を指定することをお勧めします `${{CDN_PURGEKEY_031224}}`）には、追加された日が反映されます。
   * purgeKey2 – 秘密鍵の回転に使用されます。これについては、で説明します。 [回転，シークレット セクション](#rotating-secrets) セクションを下にします。 次のうち少なくとも 1 つ `purgeKey1` および `purgeKey2` を宣言する必要があります。
* ルール：使用する認証システムと、パブリッシュ層とプレビュー層のどちらに使用するかを宣言できます。  これには以下が含まれます。
   * 名前 – わかりやすい文字列
   * when – 構文に従って、ルールを評価するタイミングを決定する条件 [トラフィックフィルタールール](/help/security/traffic-filter-rules-including-waf.md) 記事。 通常は、現在の層の比較（パブリッシュなど）が含まれます。
   * アクション – 「authenticate」を指定し、対象の認証システムを参照する必要があります。

>[!NOTE]
>エッジキーはとして設定する必要があります [Cloud Manager 環境変数](/help/implementing/cloud-manager/environment-variables.md) タイプの変数 `secret`を参照する設定がデプロイされる前に行います。

## 共通設定 {#common-setup}

すべてのオーセンティケータは次のように設定されます。

* まず、Git プロジェクトの最上位フォルダーに、次のフォルダーとファイル構造を作成します。

```
config/
     cdn.yaml
```

* 次に、 `cdn.yaml` 設定ファイルには、以下の例で説明するノードが含まれている必要があります。 この `kind` プロパティをに設定する必要があります `CDN` およびのバージョンは、現在のスキーマバージョンに設定する必要があります `1`. メタデータノードには「envTypes」プロパティがあり、この設定が評価される環境のタイプ（開発、ステージ、実稼動）を示します。

* 最後に、Cloud Manager でターゲット設定パイプラインを作成します。 [実稼動パイプラインの設定](/help/implementing/cloud-manager/configuring-pipelines/configuring-production-pipelines.md)および[実稼動以外のパイプラインの設定](/help/implementing/cloud-manager/configuring-pipelines/configuring-non-production-pipelines.md)を参照してください。

以下の点に注意してください。

* RDE は現在、設定パイプラインをサポートしていません。
* `yq` を使用すると、設定ファイル（例：`yq cdn.yaml`）の YAML 形式をローカルで検証できます。

## 秘密鍵の回転 {#rotating-secrets}

セキュリティを確保するために、資格情報を変更することをお勧めします。 これは、エッジキーの例を使用して以下のように実現できますが、パージキーにも同じ方法が使用されます。

* 最初は `edgeKey1` が定義されています。このケースではとして参照されます `${{CDN_EDGEKEY_052824}}`推奨される規則として、には作成日が反映されます。

```
experimental_authentication:
  authenticators:
    - name: edge-auth
      type: edge
      edgeKey1: ${{CDN_EDGEKEY_052824}}
```

* キーを回転させる場合は、新しい Cloud Manager シークレットを作成します。次に例を示します `${{CDN_EDGEKEY_041425}}`.
* 設定で、以下から参照します `edgeKey2` をデプロイします。

```
experimental_authentication:
  authenticators:
    - name: edge-auth
      type: edge
      edgeKey1: ${{CDN_EDGEKEY_052824}}
      edgeKey2: ${{CDN_EDGEKEY_041425}}
```

* 古いエッジキーが使用されていないことがわかったら、を削除して削除します。 `edgeKey1` 設定から。

```
experimental_authentication:
  authenticators:
    - name: edge-auth
      type: edge
      edgeKey2: ${{CDN_EDGEKEY_041425}}
```

* 古い秘密鍵参照（`${{CDN_EDGEKEY_052824}}`）を選択し、デプロイします。
* 次の回転の準備ができたら、同じ手順に従いますが、今回は追加します `edgeKey1` 設定に、という名前の新しい Cloud Manager 環境シークレットを参照します（例：）。 `${{CDN_EDGEKEY_031426}}`.

```
experimental_authentication:
  authenticators:
    - name: edge-auth
      type: edge
      edgeKey2: ${{CDN_EDGEKEY_041425}}
      edgeKey1: ${{CDN_EDGEKEY_031426}}
```
