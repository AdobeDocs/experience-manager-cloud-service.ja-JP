---
title: AEM as a Cloud Service の高度なネットワーク機能の設定
description: AEM as a Cloud Service の高度なネットワーク機能（VPN やフレキシブルエグレス IP アドレスまたは専用エグレス IP アドレスなど）を設定する方法を説明します
exl-id: 968cb7be-4ed5-47e5-8586-440710e4aaa9
source-git-commit: a06f81d5ac7f5276acd34415843f084f58f04ba8
workflow-type: tm+mt
source-wordcount: '0'
ht-degree: 0%

---

# AEM as a Cloud Service の高度なネットワーク機能の設定 {#configuring-advanced-networking}

この記事では、AEM as a Cloud Service の高度なネットワーク機能（VPN のセルフサービスプロビジョニング、非標準ポート、専用エグレス IP アドレスなど）を紹介します。

>[!INFO]
>
>また、このページでは、高度なネットワークオプションのそれぞれについて説明する一連の記事を紹介します [場所](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/networking/advanced-networking.html?lang=en).

## 概要 {#overview}

AEM as a Cloud Service には、複数のタイプの高度なネットワーク機能が用意されており、Cloud Manager API を使用してユーザーが設定できます。次の機能が含まれます。

* [柔軟なポート出力](#flexible-port-egress) - 非標準ポートからの送信トラフィックを許可するように AEM as a Cloud Service を設定できます
* [専用エグレス IP アドレス](#dedicated-egress-IP-address) - 一意の IP アドレスから発信するように AEM as a Cloud Service からのトラフィックを設定できます
* [仮想プライベートネットワーク（VPN）](#vpn) - VPN 技術を既に利用している場合は、ユーザーのインフラストラクチャと AEM as a Cloud Service の間で発生するトラフィックのセキュリティを確保できます。

この記事では、これらの各オプションについて、設定方法などを詳しく説明します。一般的な設定戦略としては、`/networkInfrastructures` API エンドポイントをプログラムレベルで呼び出して、目的のタイプの高度なネットワーク機能を宣言したあと、環境ごとに `/advancedNetworking` エンドポイントを呼び出して、インフラストラクチャを有効にし、環境固有のパラメーターを設定します。それぞれの形式的な構文とサンプルリクエストおよび応答については、Cloud Manager API ドキュメントの適切なエンドポイントを参照してください。

プログラムは、単一の高度なネットワークバリエーションをプロビジョニングできます。 フレキシブルポートエグレス IP アドレスと専用エグレス IP アドレスのどちらを選択する場合は、特定の IP アドレスが必要なければ、フレキシブルポートエグレスを選択することをお勧めします。アドビ側でフレキシブルポートエグレストラフィックのパフォーマンスを最適化できるからです。

>[!INFO]
>
>サンドボックスプログラムでは、高度なネットワーク機能は使用できません。
>また、環境はAEMバージョン 5958 以降にアップグレードする必要があります。

>[!NOTE]
>
>従来の専用エグレス技術を既にプロビジョニングしている場合は、必要があっても、これらのオプションを設定しないでください。設定すると、サイト接続に影響が出る可能性があります。サポートが必要な場合は、アドビサポートに問い合わせてください。

## フレキシブルポートエグレス {#flexible-port-egress}

高度なネットワーク機能を使用すると、デフォルトで開いている HTTP（ポート 80）と HTTPS（ポート 443）以外のポートからトラフィックを送信するように、AEM as a Cloud Service を設定することができます。

### 検討事項 {#flexible-port-egress-considerations}

専用エグレスに依存しないトラフィックの方がスループットが高くなるので、VPN の必要がなく、専用エグレス IP アドレスも必要ない場合は、フレキシブルポートエグレスをお勧めします。

### 設定 {#configuring-flexible-port-egress-provision}

プログラムごとに 1 回、POST `/program/<programId>/networkInfrastructures` エンドポイントが呼び出され、`kind` パラメーターの `flexiblePortEgress` の値とリージョンが渡されます。エンドポイントは、応答として `network_id` の他に、ステータスなどの他の情報も返します。パラメーターの一覧と厳密な構文については、API ドキュメントを参照してください。

呼び出しの後、ネットワークインフラストラクチャがプロビジョニングされるまで、通常は 15 分ほどかかります。Cloud Manager の [ネットワークインフラストラクチャGETエンドポイント](https://developer.adobe.com/experience-cloud/cloud-manager/reference/api/#operation/getNetworkInfrastructure) のステータスが「準備完了」になります。

プログラムスコープのフレキシブルポートエグレス設定が準備できている場合、 `PUT /program/<program_id>/environment/<environment_id>/advancedNetworking` 環境レベルでネットワークを有効にし、必要に応じてポート転送規則を宣言するには、エンドポイントを環境ごとに呼び出す必要があります。 柔軟性を持たせるために、パラメーターは環境ごとに設定できます。

80 または 443 以外のポートに対しては、宛先ホストのセット（名前または IP アドレスとポート）を指定してポート転送ルールを宣言する必要があります。宛先ホストごとに、宛先ポートを 30000～30999 のポートにマッピングする必要があります。

API が数秒以内に応答して「更新中」のステータスを返し、約 10 分後に、高度なネットワーク機能が有効であることがエンドポイントの `GET` メソッドで示されます。

### 更新 {#updating-flexible-port-egress-provision}

プログラムレベルの設定は、`PUT /api/program/<program_id>/network/<network_id>` エンドポイントの呼び出しで更新でき、数分以内に有効になります。

>[!NOTE]
>
> 「kind」パラメーターの値（`flexiblePortEgress`、`dedicatedEgressIP`、`VPN` のいずれか）は変更できません。サポートが必要な場合は、作成済みの内容と変更の理由を明記して、カスタマーサポートに問い合わせてください。

環境ごとのポート転送ルールを更新するには、`PUT /program/{programId}/environment/{environmentId}/advancedNetworking` エンドポイントを再度呼び出します。その際に、設定パラメーターは一部ではなく、必ず全部を含めてください。

### フレキシブルポートエグレスの削除または無効化 {#deleting-disabling-flexible-port-egress-provision}

ネットワークインフラストラクチャを&#x200B;**削除**&#x200B;するには、作成済みの内容と削除の理由を明記して、カスタマーサポートチケットを送信します。

特定の環境に対してフレキシブルポートエグレスを&#x200B;**無効**&#x200B;にするには、`DELETE [/program/{programId}/environment/{environmentId}/advancedNetworking]()` を呼び出します。

詳しくは、[Cloud Manager API ドキュメント](https://developer.adobe.com/experience-cloud/cloud-manager/reference/api/#operation/disableEnvironmentAdvancedNetworkingConfiguration)を参照してください。

### トラフィックルーティング {#flexible-port-egress-traffic-routing}

80 または 443 以外のポートに送信される http または https トラフィックの場合、次のホストおよびポート環境変数を使用してプロキシを設定する必要があります。

* HTTP の場合： `AEM_PROXY_HOST` / `AEM_HTTP_PROXY_PORT ` ( デフォルトは `proxy.tunnel:3128` (AEMリリース 6094 未満 )
* HTTPS の場合： `AEM_PROXY_HOST` / `AEM_HTTPS_PROXY_PORT ` ( デフォルトは `proxy.tunnel:3128` (AEMリリース 6094 未満 )

`www.example.com:8443` にリクエストを送信するサンプルコードを以下に示します。

```java
String url = "www.example.com:8443"
String proxyHost = System.getenv().getOrDefault("AEM_PROXY_HOST", "proxy.tunnel");
int proxyPort = Integer.parseInt(System.getenv().getOrDefault("AEM_HTTPS_PROXY_PORT", "3128"));
HttpClient client = HttpClient.newBuilder()
      .proxy(ProxySelector.of(new InetSocketAddress(proxyHost, proxyPort)))
      .build();
 
HttpRequest request = HttpRequest.newBuilder().uri(URI.create(url)).build();
HttpResponse<String> response = client.send(request, BodyHandlers.ofString());
```

非標準の Java ネットワークライブラリを使用する場合は、上記のプロパティを使用して、すべてのトラフィックに対してプロキシを設定します。

`portForwards` パラメーターで宣言したポートで宛先とやり取りする HTTP/HTTPS 以外のトラフィックは、マッピングされたポートと共に、`AEM_PROXY_HOST` というプロパティを参照する必要があります。例えば、次のように参照します。

```java
DriverManager.getConnection("jdbc:mysql://" + System.getenv("AEM_PROXY_HOST") + ":53306/test");
```

次の表にトラフィックルーティングを示します。

<table>
<thead>
  <tr>
    <th>トラフィック</th>
    <th>宛先の条件</th>
    <th>ポート</th>
    <th>接続</th>
    <th>外部宛先の例</th>
  </tr>
</thead>
<tbody>
  <tr>
    <td><b>HTTP または HTTPS プロトコル</b></td>
    <td>標準の HTTP または HTTPS トラフィック</td>
    <td>80 または 443</td>
    <td>許可</td>
    <td></td>
  </tr> 
  <tr>
    <td></td>
    <td>次の環境変数とプロキシポート番号を使用して設定された http プロキシを介した（80 または 443 以外の他のポートでの）非標準トラフィック。 Cloud Manager API 呼び出しの portForwards パラメーターで宛先ポートを宣言しないでください。<br><ul>
     <li>AEM_PROXY_HOST(AEMリリースではデフォルトで「proxy.tunnel」に設定されています。6094 より前 )</li>
     <li>AEM_HTTPS_PROXY_PORT(AEMリリースではデフォルトでポート 3128 に設定され、6094 より前 )</li>
    </ul>
    <td>80 または 443 以外のポート</td>
    <td>許可</td>
    <td>example.com:8443</td>
  </tr>
  <tr>
    <td></td>
    <td>HTTP プロキシを使用しない（80 または 443 以外のポート上の）非標準トラフィック</td>
    <td>80 または 443 以外のポート</td>
    <td>ブロック</td>
    <td></td>
  </tr>
  <tr>
    <td><b>HTTP 以外または HTTPS 以外</b></td>
    <td>クライアントは、<code>portForwards</code> API パラメーターで宣言された <code>portOrig</code> を使用して、<code>AEM_PROXY_HOST</code> 環境変数のプロキシホストに接続</td>
    <td>任意</td>
    <td>許可</td>
    <td><code>mysql.example.com:3306</code></td>
  </tr>
  <tr>
    <td></td>
    <td>その他すべて</td>
    <td>任意</td>
    <td>ブロック</td>
    <td><code>db.example.com:5555</code></td>
  </tr>
</tbody>
</table>

**Apache／Dispatcher 設定**

AEM Cloud Service の Apache／Dispatcher 層の `mod_proxy` ディレクティブは、上記のプロパティを使用して設定できます。

```
ProxyRemote "http://example.com:8080" "http://${AEM_PROXY_HOST}:3128"
ProxyPass "/somepath" "http://example.com:8080"
ProxyPassReverse "/somepath" "http://example.com:8080"
```

```
SSLProxyEngine on //needed for https backends
 
ProxyRemote "https://example.com:8443" "http://${AEM_PROXY_HOST}:3128"
ProxyPass "/somepath" "https://example.com:8443"
ProxyPassReverse "/somepath" "https://example.com:8443"
```

## 出力専用 IP アドレス {#dedicated-egress-IP-address}

>[!NOTE]
>
>2021年9月リリース（2021/10/06）以前に専用エグレス IP がプロビジョニングされている場合は、[従来の専用エグレスアドレスを使用する場合](#legacy-dedicated-egress-address-customers)を参照してください。

### メリット {#benefits}

この専用 IP アドレスは、SaaS ベンダー（CRM ベンダーなど）との統合や、IP アドレスの許可リストを提供する AEM as a Cloud Service 外部のソリューションと統合する場合のセキュリティを強化します。専用 IP アドレスを許可リストに追加することで、顧客の AEM Cloud Service からのトラフィックのみが外部サービスに送信されるようになります。これは、その他の許可されている IP からのトラフィックに加えられるものです。

専用 IP アドレス機能を有効にしない場合、AEM as a Cloud Service から出ていくトラフィックは、他の顧客と共有する一連の IP を流れていきます。

### 設定 {#configuring-dedicated-egress-provision}

>[!INFO]
>
>Splunk 転送機能は専用エグレス IP アドレスからは使用できません。

専用エグレス IP アドレスの設定は、[フレキシブルポートエグレス](#configuring-flexible-port-egress-provision)の場合と同じです。

フレキシブルポートエグレスとの主な違いは、トラフィックが常に専用 の一意の IP アドレスから出ていくことです。その IP を確認するには、DNS リゾルバーを使用して、`p{PROGRAM_ID}.external.adobeaemcloud.com` に関連付けられている IP アドレスを特定します。この IP アドレスが変わることはありませんが、将来変更する必要がある場合は、事前に通知されます。

`PUT /program/<program_id>/environment/<environment_id>/advancedNetworking` エンドポイントのフレキシブルポートエグレスでサポートされているルーティングルールに加えて、専用エグレス IP アドレスでは `nonProxyHosts` パラメーターもサポートしています。これにより、専用 IP ではなく共有 IP アドレス範囲を経由してルーティングされる一連のホストを宣言できます。これは、共有 IP から出ていくトラフィックがさらに最適化される可能性があるので、役に立つことがあります。`nonProxyHost` URL は `example.com` または `*.example.com` のパターンに従う場合があります（このパターンでは、ワイルドカードはドメインの先頭でのみ使用できます）。

フレキシブルポートエグレス IP アドレスと専用エグレス IP アドレスのどちらかを選択する場合は、特定の IP アドレスが必要なければ、フレキシブルポートエグレスを選択してください。アドビ側でフレキシブルポートエグレストラフィックのパフォーマンスを最適化できるからです。

### トラフィックルーティング {#dedcated-egress-ip-traffic-routing}

標準の Java ネットワークライブラリを使用している場合は、ポート 80 または 443 を通じて宛先に送信される HTTP または HTTPS トラフィックは、事前に設定されたプロキシを経由します。他のポートを経由する HTTP または HTTPS トラフィックは、次のプロパティを使用してプロキシを設定してください。

```
AEM_HTTP_PROXY_HOST / AEM_HTTPS_PROXY_HOST
AEM_HTTP_PROXY_PORT / AEM_HTTPS_PROXY_PORT
```

`www.example.com:8443` にリクエストを送信するサンプルコードを以下に示します。

```java
String url = "www.example.com:8443"
String proxyHost = System.getenv("AEM_HTTPS_PROXY_HOST");
int proxyPort = Integer.parseInt(System.getenv("AEM_HTTPS_PROXY_PORT"));

HttpClient client = HttpClient.newBuilder()
      .proxy(ProxySelector.of(new InetSocketAddress(proxyHost, proxyPort)))
      .build();
 
HttpRequest request = HttpRequest.newBuilder().uri(URI.create(url)).build();
HttpResponse<String> response = client.send(request, BodyHandlers.ofString());
```

非標準の Java ネットワークライブラリを使用する場合は、上記のプロパティを使用して、すべてのトラフィックに対してプロキシを設定します。

`portForwards` パラメーターで宣言したポートで宛先とやり取りする HTTP/HTTPS 以外のトラフィックは、マッピングされたポートと共に、`AEM_PROXY_HOST` というプロパティを参照する必要があります。例えば、次のように参照します。

```java
DriverManager.getConnection("jdbc:mysql://" + System.getenv("AEM_PROXY_HOST") + ":53306/test");
```

<table>
<thead>
  <tr>
    <th>トラフィック</th>
    <th>宛先の条件</th>
    <th>ポート</th>
    <th>接続</th>
    <th>外部宛先の例</th>
  </tr>
</thead>
<tbody>
  <tr>
    <td><b>HTTP または HTTPS プロトコル</b></td>
    <td>Azure サービスまたはアドビサービスへのトラフィック</td>
    <td>任意</td>
    <td>（専用 IP ではなく）共有クラスター IP を経由</td>
    <td>adobe.io<br>api.windows.net</td>
  </tr>
  <tr>
    <td></td>
    <td><code>nonProxyHosts</code> パラメーターに一致するホスト</td>
    <td>80 または 443</td>
    <td>共有クラスター IP を経由</td>
    <td></td>
  </tr>
  <tr>
    <td></td>
    <td><code>nonProxyHosts</code> パラメーターに一致するホスト</td>
    <td>80 または 443 以外のポート</td>
    <td>ブロック</td>
    <td></td>
  </tr>
  <tr>
    <td></td>
    <td>HTTP プロキシ設定を使用（標準の Java HTTP クライアントライブラリを使用する HTTP または HTTPS トラフィックにデフォルトで設定済み）</td>
    <td>任意</td>
    <td>専用エグレス IP を経由</td>
    <td></td>
  </tr>
  <tr>
    <td></td>
    <td>HTTP プロキシ設定を無視（例えば、標準の Java HTTP クライアントライブラリから明示的に削除された場合や、標準のプロキシ設定を無視する Java ライブラリが使用されている場合）</td>
    <td>80 または 443</td>
    <td>共有クラスター IP を経由</td>
    <td></td>
  </tr>
  <tr>
    <td></td>
    <td>HTTP プロキシ設定を無視（例えば、標準の Java HTTP クライアントライブラリから明示的に削除された場合や、標準のプロキシ設定を無視する Java ライブラリが使用されている場合）</td>
    <td>80 または 443 以外のポート</td>
    <td>ブロック</td>
    <td></td>
  </tr>
  <tr>
    <td><b>HTTP 以外または HTTPS 以外</b></td>
    <td>クライアントは、<code>portForwards</code> API パラメーターで宣言されている <code>portOrig</code> を使用して、<code>AEM_PROXY_HOST</code> 環境変数のプロキシホストに接続</td>
    <td>任意</td>
    <td>専用エグレス IP を経由</td>
    <td><code>mysql.example.com:3306</code></td>
  </tr>
  <tr>
    <td></td>
    <td>その他すべて</td>
    <td></td>
    <td>ブロック</td>
    <td></td>
  </tr>
</tbody>
</table>

## 機能の使用 {#feature-usage}

この機能は、プロキシ設定に標準の Java システムプロパティを使用する場合、送信トラフィックを発生させる Java コードまたはライブラリと互換性があります。実際には、これには最も一般的なライブラリが含まれる必要があります。

次にコード例を示します。

```java
public JSONObject getJsonObject(String relativePath, String queryString) throws IOException, JSONException {
  String relativeUri = queryString.isEmpty() ? relativePath : (relativePath + '?' + queryString);
  URL finalUrl = endpointUri.resolve(relativeUri).toURL();
  URLConnection connection = finalUrl.openConnection();
  connection.addRequestProperty("Accept", "application/json");
  connection.addRequestProperty("X-API-KEY", apiKey);

  try (InputStream responseStream = connection.getInputStream(); Reader responseReader = new BufferedReader(new InputStreamReader(responseStream, Charsets.UTF_8))) {
    return new JSONObject(new JSONTokener(responseReader));
  }
}
```

一部のライブラリでは、プロキシ設定に標準の Java システムプロパティを使用するために、明示的な設定が必要です。

Apache HttpClient を使用する例を以下に示します。ここでは、[`HttpClientBuilder.useSystemProperties()`](https://hc.apache.org/httpcomponents-client-4.5.x/current/httpclient/apidocs/org/apache/http/impl/client/HttpClientBuilder.html) の明示的な呼び出しまたは [`HttpClients.createSystem()`](https://hc.apache.org/httpcomponents-client-4.5.x/current/httpclient/apidocs/org/apache/http/impl/client/HttpClients.html#createSystem()) の使用が必要です。

```java
public JSONObject getJsonObject(String relativePath, String queryString) throws IOException, JSONException {
  String relativeUri = queryString.isEmpty() ? relativePath : (relativePath + '?' + queryString);
  URL finalUrl = endpointUri.resolve(relativeUri).toURL();

  HttpClient httpClient = HttpClientBuilder.create().useSystemProperties().build();
  HttpGet request = new HttpGet(finalUrl.toURI());
  request.setHeader("Accept", "application/json");
  request.setHeader("X-API-KEY", apiKey);
  HttpResponse response = httpClient.execute(request);
  String result = EntityUtils.toString(response.getEntity());
}
```

同じ専用 IP が、Adobe 組織内のすべての顧客プログラムと、各プログラム内のすべての環境に適用されます。オーサーサービスとパブリッシュサービスの両方に適用されます。

### デバッグの考慮事項 {#debugging-considerations}

想定される専用 IP アドレスでトラフィックが実際に送信されていることを検証するには、送信先のサービスでログを確認します（可能な場合）。それ以外の場合は、呼び出し元の IP アドレスを返す [https://ifconfig.me/IP](https://ifconfig.me/IP) などのデバッグサービスを呼び出すと便利です。

## 従来の専用エグレスアドレスを使用する場合 {#legacy-dedicated-egress-address-customers}

2021.09.30より前に、専用のエグレス IP がプロビジョニングされている場合、専用のエグレス IP 機能は HTTP ポートと HTTPS ポートのみをサポートします。
これには、HTTP/1.1 と HTTP/2（暗号化時）が含まれます。

## 仮想プライベートネットワーク（VPN） {#vpn}

VPN を使用すると、オーサー、パブリッシュ、プレビューからオンプレミスインフラストラクチャまたはデータセンターに接続できます。例えば、データベースにアクセスする手段として使用します。

また、VPN をサポートしている CRM ベンダーなどの SaaS ベンダーへの接続や、企業ネットワークから AEM as a Cloud Service のオーサー、プレビューまたはパブリッシュへの接続も可能になります。

IPSec 技術を搭載したほとんどの VPN デバイスがサポートされています。詳しくは、[このページ](https://docs.microsoft.com/ja-jp/azure/vpn-gateway/vpn-gateway-about-vpn-devices#devicetable)のデバイスリストで「**RouteBased の構成手順**」列の情報を参照してください。表の説明に従って、デバイスを設定します。

### 全般的な考慮事項 {#general-vpn-considerations}

* サポートは 1 つの VPN 接続に制限されています。
* Splunk 転送機能は VPN 接続では使用できません。

### 作成 {#vpn-creation}

POST `/program/<programId>/networkInfrastructures` エンドポイントがプログラムごとに 1 回呼び出され、設定情報のペイロードが渡されます。この設定情報には、`kind` パラメーターの「vpn」の値、リージョン、アドレス空間（CIDR のリスト。これは後で変更できません）、DNS リゾルバー（顧客のネットワーク内で名前を解決するためのもの）、VPN 接続情報（ゲートウェイ設定、共有 VPN キー、IP セキュリティポリシーなど）などが含まれます。エンドポイントは、応答として `network_id` の他に、ステータスなどの他の情報も返します。パラメーターの一覧と厳密な構文については、[API ドキュメント](https://developer.adobe.com/experience-cloud/cloud-manager/reference/api/#operation/createNetworkInfrastructure)を参照してください。

この呼び出しの後、ネットワークインフラストラクチャがプロビジョニングされるまで、通常は 45～60 分かかります。API の GET メソッドを呼び出して、現在のステータスを返すことができます。このステータスは、最終的に `creating` から `ready` に変わります。すべてのステータスについては、 API ドキュメントを参照してください。

プログラムスコープの VPN 設定の準備ができている場合は、環境ごとに `PUT /program/<program_id>/environment/<environment_id>/advancedNetworking` エンドポイントを呼び出して、環境レベルでネットワーク機能を有効にすると共に、ポート転送ルールを必要に応じて宣言する必要があります。柔軟性を持たせるために、パラメーターは環境ごとに設定できます。

詳しくは、[API ドキュメント](https://developer.adobe.com/experience-cloud/cloud-manager/reference/api/#operation/enableEnvironmentAdvancedNetworkingConfiguration)を参照してください。

VPN 経由でのルーティングが必要な HTTP またはHTTPS プロトコル以外の TCP トラフィックについては、宛先ホストのセット（名前または IP アドレスとポート）を指定して、ポート転送ルールを宣言する必要があります。宛先ホストごとに、宛先ポートを 30000～30999 のポートにマッピングする必要があります。この値は、プログラムのあらゆる環境で一意でなければなりません。また、一連の URL を `nonProxyHosts` パラメーターにリストすることもできます。このパラメーターは、どの URL のトラフィックが VPN ルーティングをバイパスして共有 IP 範囲を経由すべきかを宣言するものです。これらの URL は `example.com` または `*.example.com` のパターンに従います（このパターンでは、ワイルドカードはドメインの先頭でのみ使用できます）。

API が数秒以内に応答して「`updating`」のステータスを返し、約 10 分後に、Cloud Manager の環境 GET エンドポイントの呼び出しで「`ready`」のステータスが返されます。これは、環境のアップデートが適用されたことを示します。

環境のトラフィックルーティングルール（ホストまたはバイパス）がない場合でも、空のペイロードを渡して `PUT /program/<program_id>/environment/<environment_id>/advancedNetworking` を呼び出す必要があります。

### VPN の更新 {#updating-the-vpn}

プログラムレベルの VPN 設定は、`PUT /api/program/<program_id>/network/<network_id>` エンドポイントを呼び出して更新することができます。

なお、最初の VPN プロビジョニングの後は、アドレス空間は変更できません。アドレス空間の変更が必要な場合は、カスタマーサポートに問い合わせてください。また、`kind` パラメーターの値（`flexiblePortEgress`、`dedicatedEgressIP`、`VPN` のいずれか）も変更できません。サポートが必要な場合は、作成済みの内容と変更の理由を明記して、カスタマーサポートに問い合わせてください。

環境ごとのルーティングルールを更新するには、`PUT /program/{programId}/environment/{environmentId}/advancedNetworking` エンドポイントを再度呼び出します。その際に、設定パラメーターは一部ではなく、必ず全部を含めてください。環境のアップデートは適用されるまでに通常 5～10 分かかります。

### VPN の削除または無効化 {#deleting-or-disabling-the-vpn}

ネットワークインフラストラクチャを削除するには、作成済みの内容と削除の理由を明記して、カスタマーサポートチケットを送信します。

特定の環境で VPN を無効にするには、`DELETE /program/{programId}/environment/{environmentId}/advancedNetworking` を呼び出します。詳しくは、[API ドキュメント](https://developer.adobe.com/experience-cloud/cloud-manager/reference/api/#operation/disableEnvironmentAdvancedNetworkingConfiguration)を参照してください。

### トラフィックルーティング {#vpn-traffic-routing}

次の表にトラフィックルーティングを示します。

<table>
<thead>
  <tr>
    <th>トラフィック</th>
    <th>宛先の条件</th>
    <th>ポート</th>
    <th>接続</th>
    <th>外部宛先の例</th>
  </tr>
</thead>
<tbody>
  <tr>
    <td><b>HTTP または HTTPS プロトコル</b></td>
    <td>Azure サービスまたはアドビサービスへのトラフィック</td>
    <td>任意</td>
    <td>（専用 IP ではなく）共有クラスター IP を経由</td>
    <td>adobe.io<br>api.windows.net</td>
  </tr>
  <tr>
    <td></td>
    <td><code>nonProxyHosts</code> パラメーターに一致するホスト</td>
    <td>80 または 443</td>
    <td>共有クラスター IP を経由</td>
    <td></td>
  </tr>
  <tr>
    <td></td>
    <td><code>nonProxyHosts</code> パラメーターに一致するホスト</td>
    <td>80 または 443 以外のポート</td>
    <td>ブロック</td>
    <td></td>
  </tr>
  <tr>
    <td></td>
    <td>IP が <i>VPN ゲートウェイアドレス空間</i>の範囲に収まり、（標準の Java HTTP クライアントライブラリを使用する HTTP または HTTPS トラフィックにデフォルトで設定済みの）HTTP プロキシ設定を使用する場合</td>
    <td>任意</td>
    <td>VPN を経由</td>
    <td><code>10.0.0.1:443</code>ホスト名を指定することもできます。</td>
  </tr>
  <tr>
    <td></td>
    <td>IP が <i>VPN ゲートウェイアドレス空間</i>の範囲に収まらず、（標準の Java HTTP クライアントライブラリを使用する HTTP または HTTPS トラフィックにデフォルトで設定済みの）HTTP プロキシ設定を使用する場合</td>
    <td>任意</td>
    <td>専用エグレス IP を経由</td>
    <td></td>
  </tr>
  <tr>
    <td></td>
    <td>HTTP プロキシ設定を無視（例えば、標準の Java HTTP クライアントライブラリから明示的に削除された場合や、標準のプロキシ設定を無視する Java ライブラリを使用する場合）
</td>
    <td>80 または 443</td>
    <td>共有クラスター IP を経由</td>
    <td></td>
  </tr>
  <tr>
    <td></td>
    <td>HTTP プロキシ設定を無視（例えば、標準の Java HTTP クライアントライブラリから明示的に削除された場合や、標準のプロキシ設定を無視する Java ライブラリを使用する場合）</td>
    <td>80 または 443 以外のポート</td>
    <td>ブロック</td>
    <td></td>
  </tr>
  <tr>
    <td><b>HTTP 以外または HTTPS 以外</b></td>
    <td>IP が <i>VPN ゲートウェイアドレス空間</i>の範囲に収まり、<code>portForwards</code> API パラメーターで宣言されている <code>portOrig</code> を使用して <code>AEM_PROXY_HOST</code> 環境変数のプロキシホストにクライアントが接続する場合</td>
    <td>任意</td>
    <td>VPN を経由</td>
    <td><code>10.0.0.1:3306</code>ホスト名を指定することもできます。</td>
  </tr>
  <tr>
    <td></td>
    <td>IP が <i>VPN ゲートウェイアドレス空間</i>の範囲に収まらず、<code>portForwards</code> API パラメーターで宣言されている <code>portOrig</code> を使用して <code>AEM_PROXY_HOST</code> 環境変数のプロキシホストにクライアントが接続する場合</td>
    <td>任意</td>
    <td>専用エグレス IP を経由</td>
    <td></td>
  </tr>
  <tr>
    <td></td>
    <td>その他すべて</td>
    <td>任意</td>
    <td>ブロック</td>
    <td></td>
  </tr>
</tbody>
</table>

### 設定に役立つドメイン{#vpn-useful-domains-for-configuration}

次の図は、設定と開発に役立つ一連のドメインと関連 IP を視覚的に表したものです。図の下の表に、これらのドメインと IP を示します。

![VPN ドメイン設定](/help/security/assets/AdvancedNetworking.jpg)

<table>
<thead>
  <tr>
    <th>ドメインパターン</th>
    <th>エグレス（AEM から送信）の意味</th>
    <th>イングレス（AEM に着信）の意味</th>
  </tr>
</thead>
<tbody>
  <tr>
    <td><code>p{PROGRAM_ID}.external.adobeaemcloud.com</code></td>
    <td>プライベートネットワーク経由ではなくインターネットに送信されるトラフィックの専用エグレス IP アドレス </td>
    <td>VPN からの接続は、CDN ではこの IP からの接続と見なされます。VPN からの接続のみ AEM に着信するように設定するには、この IP のみを許可し、それ以外のすべてをブロックするように、Cloud Manager を設定します。詳しくは、「VPN をイングレス接続に限定する方法」の節を参照してください。</td>
  </tr>
  <tr>
    <td><code>p{PROGRAM_ID}-gateway.external.adobeaemcloud.com</code></td>
    <td>該当なし</td>
    <td>AEM 側の VPN ゲートウェイの IP。顧客のネットワークエンジニアリングチームでは、これを使用して、特定の IP アドレスから VPN ゲートウェイへの VPN 接続のみを許可することができます。 </td>
  </tr>
  <tr>
    <td><code>p{PROGRAM_ID}.inner.adobeaemcloud.net</code></td>
    <td>VPN の AEM 側から顧客側に送信されるトラフィックの IP。これを顧客の設定で許可リストに登録して、AEM からのみ接続できるようにすることが可能です。</td>
    <td>AEM への VPN アクセスのみを許可する場合は、<code>author-p{PROGRAM_ID}-e{ENVIRONMENT_ID}.adobeaemcloud.com</code> と <code>publish-p{PROGRAM_ID}-e{ENVIRONMENT_ID}.adobeaemcloud.com</code> の両方またはどちらか一方をこれにマッピングするように、CNAME DNS エントリを設定する必要があります。</td>
  </tr>
</tbody>
</table>

### VPN をイングレス接続に限定する方法 {#restrict-vpn-to-ingress-connections}

AEM への VPN アクセスのみを許可する場合は、`p{PROGRAM_ID}.external.adobeaemcloud.com` で定義された IP のみが環境と通信できるように、環境の許可リストを Cloud Manager で設定します。これは、Cloud Manager で他の IP ベースの許可リストと同じように行うことができます。

パスベースのルールにする必要がある場合は、標準の http ディレクティブを Dispatcher レベルで使用して、特定の IP を拒否または許可します。リクエストが常にオリジンに到達するように、目的のパスを CDN でキャッシュできないようにする必要もあります。

**httpd 設定の例**

```
Order deny,allow
Deny from all
Allow from 192.168.0.1
Header always set Cache-Control private
```

## 高度なネットワーク機能タイプ間の移行 {#transitioning-between-advanced-networking-types}

`kind` パラメーターは変更できないので、サポートが必要な場合は、作成済みの内容と変更の理由を明記して、カスタマーサポートに問い合わせてください。
