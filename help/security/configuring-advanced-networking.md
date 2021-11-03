---
title: AEM as a Cloud Service用のアドバンスドネットワークの設定
description: AEM as a Cloud Serviceの VPN や、柔軟な出力 IP アドレス、または専用の出力 IP アドレスなどの高度なネットワーク機能を設定する方法を説明します
source-git-commit: 2f9ba938d31c289201785de24aca2d617ab9dfca
workflow-type: tm+mt
source-wordcount: '2836'
ht-degree: 7%

---


# AEM as a Cloud Service用のアドバンスドネットワークの設定 {#configuring-advanced-networking}

この記事では、AEMas a Cloud Serviceの様々な高度なネットワーク機能（VPN のセルフサービスプロビジョニング、非標準ポート、専用の出力 IP アドレスなど）を紹介します。

## 概要 {#overview}

AEM as a Cloud Serviceには、Cloud Manager API を使用してユーザーが設定できる、いくつかのタイプの高度なネットワーク機能が用意されています。 有効なタイプには以下が含まれます。

* [柔軟なポート出力](#flexible-port-egress)  — 非標準ポートからの送信トラフィックを許可するようにAEM as a Cloud Serviceを設定します
* [出力専用 IP アドレス](#dedicated-egress-IP-address)  — 固有の IP から発信するAEM as a Cloud Serviceからのトラフィックを設定します
* [仮想プライベートネットワーク (VPN)](#vpn)  — お客様のインフラストラクチャとAEM as a Cloud Service間のトラフィックを保護し、VPN テクノロジーをお持ちのお客様向け

この記事では、各オプションの設定方法など、各オプションについて詳しく説明します。 一般的な設定戦略として、 `/networkInfrastructures` API エンドポイントは、プログラムレベルで呼び出され、必要な種類の高度なネットワークを宣言した後、 `/advancedNetworking` エンドポイントを使用して、インフラストラクチャを有効にし、環境固有のパラメーターを設定します。 各形式の構文、リクエストと応答のサンプルについては、Cloud Manager API ドキュメントの適切なエンドポイントを参照してください。

プログラムは、単一の高度なネットワークバリエーションをプロビジョニングできます。 Adobeはフレキシブルポートエグレストラフィックのパフォーマンスを最適化できるので、フレキシブルポートエグレスと専用エグレス IP アドレスを決定する際に、特定の IP アドレスが不要な場合は、フレキシブルポートエグレスを選択することをお勧めします。

>[!INFO]
>
>サンドボックスプログラムでは、高度なネットワークは使用できません。
>また、環境はAEMバージョン 5958 以降にアップグレードする必要があります。

>[!NOTE]
>
>これらのオプションの 1 つを設定する必要がある、従来の専用エグレステクノロジーを既にプロビジョニングしているお客様は、そうしないでください。そうしないと、サイト接続に影響が出る場合があります。 不明な点はAdobeサポートにお問い合わせください。

## フレキシブルポートエグレス {#flexible-port-egress}

この高度なネットワーク機能を使用すると、AEM as a Cloud Serviceを設定して、HTTP（ポート 80）および HTTPS（ポート 443）以外のポート（デフォルトで開いている）を介してトラフィックを出力することができます。

### 検討事項 {#flexible-port-egress-considerations}

専用の出力に依存しないトラフィックは高いスループットを達成できるので、VPN が不要で、専用の出力 IP アドレスが不要な場合は、柔軟なポート出力が推奨されます。

### 設定 {#configuring-flexible-port-egress-provision}

プログラムごとに 1 回、POST `/program/<programId>/networkInfrastructures` エンドポイントが呼び出され、 `flexiblePortEgress` の `kind` パラメーターと地域。 エンドポイントは、 `network_id`の他に、ステータスを含むその他の情報も含まれます。 パラメーターの完全なセットと正確な構文は、API ドキュメントで参照する必要があります。

この呼び出し後、通常、ネットワークインフラストラクチャがプロビジョニングされるまで約 15 分かかります。 Cloud Manager の [ネットワークインフラストラクチャGETエンドポイント](https://developer.adobe.com/experience-cloud/cloud-manager/reference/api/#operation/getNetworkInfrastructure) のステータスが「準備完了」になります。

プログラムスコープのフレキシブルポートエグレス設定が準備できている場合、 `PUT /program/<program_id>/environment/<environment_id>/advancedNetworking` 環境レベルでネットワークを有効にし、必要に応じてポート転送規則を宣言するには、エンドポイントを環境ごとに呼び出す必要があります。 柔軟性を提供するために、環境ごとにパラメーターを設定できます。

ポート転送規則は、宛先ホストのセット（名前または IP、およびポートを含む）を指定することで、80/443以外のポートに対して宣言する必要があります。 お客様は、宛先ホストごとに、目的の宛先ポートを30000 ～ 30999のポートにマッピングする必要があります。

API は、更新のステータスを示し、約 10 分後にエンドポイントの `GET` メソッドは、アドバンスドネットワークが有効であることを示す必要があります。

### アップデート {#updating-flexible-port-egress-provision}

プログラムレベルの設定は、 `PUT /api/program/<program_id>/network/<network_id>` エンドポイントおよびは、数分以内に有効になります。

>[!NOTE]
>
> 「kind」パラメータ (`flexiblePortEgress`, `dedicatedEgressIP` または `VPN`) は変更できません。 サポートが必要な場合は、作成済みの情報と変更の理由をカスタマーサポートに問い合わせてください。

環境ごとのポート転送ルールを更新するには、 `PUT /program/{programId}/environment/{environmentId}/advancedNetworking` エンドポイントではなく、設定パラメーターの完全なセットを必ず含めてください。

### フレキシブルポートエグレスの削除または無効化 {#deleting-disabling-flexible-port-egress-provision}

次に対して **削除** ネットワークインフラストラクチャで、作成された内容と削除する必要のある理由を説明したカスタマーサポートチケットを送信します。

次に対して **無効** 特定の環境からの柔軟なポート出力、呼び出し `DELETE [/program/{programId}/environment/{environmentId}/advancedNetworking]()`.

詳しくは、 [Cloud Manager API ドキュメント](https://developer.adobe.com/experience-cloud/cloud-manager/reference/api/#operation/disableEnvironmentAdvancedNetworkingConfiguration).

### トラフィックルーティング {#flexible-port-egress-traffic-routing}

ポート 80 または 443 を通じて宛先に送信される HTTP または HTTPS トラフィックは、標準の Java ネットワークライブラリが使用される場合、事前設定済みのプロキシを経由します。 他のポートを経由する http または https トラフィックの場合は、次のプロパティを使用してプロキシを設定する必要があります。

* `AEM_HTTP_PROXY_HOST / AEM_HTTPS_PROXY_HOST`
* `AEM_HTTP_PROXY_PORT / AEM_HTTPS_PROXY_PORT`

例えば、にリクエストを送信するコード例を次に示します。 `www.example.com:8443`:

```java
String url = "www.example.com:8443"
var proxyHost = System.getenv("AEM_HTTPS_PROXY_HOST");
var proxyPort = Integer.parseInt(System.getenv("AEM_HTTPS_PROXY_PORT"));
HttpClient client = HttpClient.newBuilder()
      .proxy(ProxySelector.of(new InetSocketAddress(proxyHost, proxyPort)))
      .build();
 
HttpRequest request = HttpRequest.newBuilder().uri(URI.create(url)).build();
HttpResponse<String> response = client.send(request, BodyHandlers.ofString());
```

非標準の Java ネットワークライブラリを使用する場合、すべてのトラフィックに対して、上記のプロパティを使用してプロキシを設定します。

で宣言されたポートを介した宛先との非 http/s トラフィック `portForwards` パラメーターは、 `AEM_PROXY_HOST`マッピングされたポートと共に使用します。 次に例を示します。

```java
DriverManager.getConnection("jdbc:mysql://" + System.getenv("AEM_PROXY_HOST") + ":53306/test");
```

次の表に、トラフィックルーティングを示します。

<table>
<thead>
  <tr>
    <th>トラフィック</th>
    <th>宛先条件</th>
    <th>ポート</th>
    <th>「接続」</th>
    <th>例</th>
  </tr>
</thead>
<tbody>
  <tr>
    <td><b>HTTP または HTTPS プロトコル</b></td>
    <td>標準の http/s トラフィック</td>
    <td>80 または 443</td>
    <td>許可</td>
    <td></td>
  </tr> 
  <tr>
    <td></td>
    <td>次の環境変数を使用して設定された http プロキシを介した（80 または 443 以外の他のポートでの）非標準トラフィック：<br><ul>
     <li>AEM_HTTP_PROXY_HOST / AEM_HTTPS_PROXY_HOST</li>
     <li>AEM_HTTP_PROXY_PORT / AEM_HTTPS_PROXY_PORT</li>
    </ul>
    <td>80 または 443 以外のポート</td>
    <td>許可</td>
  </tr>
  <tr>
    <td></td>
    <td>非標準トラフィック（ポート 80 または 443 以外の他のポートで）は http プロキシを使用しません</td>
    <td>80 または 443 以外のポート</td>
    <td>ブロック</td>
    <td></td>
  </tr>
  <tr>
    <td><b>HTTP 以外または HTTPS 以外</b></td>
    <td>クライアントが <code>AEM_PROXY_HOST</code> 環境変数を <code>portOrig</code> 宣言された <code>portForwards</code> API パラメーター。</td>
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

**Apache/Dispatcher 設定**

AEM Cloud Service Apache/Dispatcher 層の `mod_proxy` ディレクティブは、上記のプロパティを使用して設定できます。

```
ProxyRemote "http://example.com" "http://${AEM_HTTP_PROXY_HOST}:${AEM_HTTP_PROXY_PORT}"
ProxyPass "/somepath" "http://example.com"
ProxyPassReverse "/somepath" "http://example.com"
```

```
SSLProxyEngine on //needed for https backends
 
ProxyRemote "https://example.com:8443" "http://${AEM_HTTPS_PROXY_HOST}:${AEM_HTTPS_PROXY_PORT}"
ProxyPass "/somepath" "https://example.com:8443"
ProxyPassReverse "/somepath" "https://example.com:8443"
```

## 出力専用 IP アドレス {#dedicated-egress-IP-address}

>[!NOTE]
>
>2021 年 9 月のリリース (10/6/21) 以前に、専用のエグレス IP がプロビジョニングされている場合は、 [レガシーの出口専用アドレスのお客様](#legacy-dedicated-egress-address-customers).

### メリット {#benefits}

この専用 IP アドレスは、SaaS ベンダー（CRM ベンダーなど）との統合や、IP アドレスの許可リストをオファーする AEM as a Cloud Service 以外と統合する場合のセキュリティを強化します。専用 IP アドレスをに追加す許可リストることで、顧客のAEM Cloud Serviceからのトラフィックのみが外部サービスに送られるようになります。 これは、その他の許可されている IP からのトラフィックに加えられるものです。

専用 IP アドレス機能を有効にしない場合、AEM as a Cloud Service から出ていくトラフィックは、他の顧客と共有する一連の IP を流れていきます。

### 設定 {#configuring-dedicated-egress-provision}

>[!INFO]
>
>Splunk 転送機能は、専用の出力 IP アドレスからは使用できません。

専用の出力 IP アドレスの設定は、 [フレキシブルポートエグレス](#configuring-flexible-port-egress-provision).

主な違いは、トラフィックが常に専用の一意の IP から出てくるということです。 その IP を見つけるには、DNS リゾルバを使用して、 `p{PROGRAM_ID}.external.adobeaemcloud.com`. IP アドレスは変更されるとは思われませんが、将来変更する必要がある場合は、詳細な通知が表示されます。

また、 `PUT /program/<program_id>/environment/<environment_id>/advancedNetworking` エンドポイント、専用のエグレス IP アドレスは、 `nonProxyHosts` パラメーター。 これにより、専用 IP ではなく、共有 IP アドレス範囲を経由してルーティングするホストのセットを宣言できます。これは、共有 IP を介したトラフィックのエグレスをさらに最適化する場合に役立ちます。 この `nonProxyHost` URL は、 `example.com` または `*.example.com`：ワイルドカードはドメインの開始時にのみサポートされます。

Adobeはフレキシブルポートエグレストラフィックのパフォーマンスを最適化できるので、フレキシブルポートエグレスと専用エグレス IP アドレスのどちらを決定する場合でも、特定の IP アドレスが必要でない場合は、フレキシブルポートエグレスを選択します。

### トラフィックルーティング {#dedcated-egress-ip-traffic-routing}

<table>
<thead>
  <tr>
    <th>トラフィック</th>
    <th>宛先条件</th>
    <th>ポート</th>
    <th>「接続」</th>
    <th>例</th>
  </tr>
</thead>
<tbody>
  <tr>
    <td><b>HTTP または HTTPS プロトコル</b></td>
    <td>Azure へのトラフィックまたはAdobe サービス</td>
    <td>任意</td>
    <td>（専用 IP ではなく）共有クラスタ IP を介して</td>
    <td>adobe.io<br>api.windows.net</td>
  </tr>
  <tr>
    <td></td>
    <td>次に一致するホスト： <code>nonProxyHosts</code> パラメータ</td>
    <td>80 または 443</td>
    <td>共有クラスタ IP 経由</td>
    <td></td>
  </tr>
  <tr>
    <td></td>
    <td>次に一致するホスト： <code>nonProxyHosts</code> パラメータ</td>
    <td>80 または 443 以外のポート</td>
    <td>ブロック</td>
    <td></td>
  </tr>
  <tr>
    <td></td>
    <td>HTTP プロキシ設定を使用。標準の Java HTTP クライアントライブラリを使用する http/s トラフィックにはデフォルトで設定されます。</td>
    <td>任意</td>
    <td>出力専用 IP を通じて</td>
    <td></td>
  </tr>
  <tr>
    <td></td>
    <td>http プロキシ設定を無視します（例えば、標準の Java HTTP クライアントライブラリから明示的に削除された場合や、標準のプロキシ設定を無視する Java ライブラリが使用されている場合）。</td>
    <td>80 または 443</td>
    <td>共有クラスタ IP 経由</td>
    <td></td>
  </tr>
  <tr>
    <td></td>
    <td>http プロキシ設定を無視します（例えば、標準の Java HTTP クライアントライブラリから明示的に削除された場合や、標準のプロキシ設定を無視する Java ライブラリが使用されている場合）。</td>
    <td>80 または 443 以外のポート</td>
    <td>ブロック</td>
    <td></td>
  </tr>
  <tr>
    <td><b>HTTP 以外または HTTPS 以外</b></td>
    <td>クライアントが <code>AEM_PROXY_HOST</code> を使用した env 変数 <code>portOrig</code> 宣言された <code>portForwards</code> API パラメーター</td>
    <td>任意</td>
    <td>出力専用 IP を通じて</td>
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

## レガシーの出口専用アドレスのお客様 {#legacy-dedicated-egress-address-customers}

2021.09.30以前に専用のエグレス IP がプロビジョニングされている場合、専用のエグレス IP 機能は以下のように動作します。

### 機能の使用 {#feature-usage}

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

Apache HttpClient を使用する例です。この例では、
[`HttpClientBuilder.useSystemProperties()`](https://hc.apache.org/httpcomponents-client-4.5.x/current/httpclient/apidocs/org/apache/http/impl/client/HttpClientBuilder.html) または
[`HttpClients.createSystem()`](https://hc.apache.org/httpcomponents-client-4.5.x/current/httpclient/apidocs/org/apache/http/impl/client/HttpClients.html#createSystem()):

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

HTTP ポートと HTTPS ポートのみがサポートされます。これには、HTTP/1.1 と、暗号化時の HTTP/2 が含まれます。

### デバッグの考慮事項 {#debugging-considerations}

期待される専用 IP アドレスでトラフィックが実際に送信されていることを検証するには、目的のサービスでログを確認します（可能な場合）。それ以外の場合は、次のようなデバッグサービスを呼び出すと便利です。 [https://ifconfig.me/IP](https://ifconfig.me/IP)：呼び出し元の IP アドレスを返します。

## 仮想プライベートネットワーク (VPN) {#vpn}

VPN を使用すると、オーサー、パブリッシュ、プレビューからオンプレミスのインフラストラクチャまたはデータセンターに接続できます。 例えば、データベースにアクセスする手段の場合です。

また、VPN をサポートする CRM ベンダーや、企業ネットワークからAEMas a Cloud Serviceの作成者、プレビュー、パブリッシュに接続する CRM ベンダーなど、SaaS ベンダーへの接続も可能です。

IPSec テクノロジーを備えたほとんどの VPN デバイスがサポートされています。 デバイスのリスト ( ) を参照してください。 [このページ](https://docs.microsoft.com/en-us/azure/vpn-gateway/vpn-gateway-about-vpn-devices#devicetable)( **RouteBased 設定手順** 列。 表の説明に従って、デバイスを設定します。

### 一般的な考慮事項 {#general-vpn-considerations}

* サポートは 1 つの VPN 接続に制限されています
* VPN 接続を介した Splunk 転送機能は不可能です。

### 作品 {#vpn-creation}

プログラムごとに 1 回、POST `/program/<programId>/networkInfrastructures` エンドポイントが呼び出され、次のような設定情報のペイロードを渡します。の「vpn」の値 `kind` パラメーター、地域、アドレス空間（CIDR のリスト — 後で変更することはできません）、DNS リゾルバー（顧客のネットワーク内の名前を解決するため）、VPN 接続情報（ゲートウェイ設定、共有 VPN キー、IP セキュリティポリシーなど）。 エンドポイントは、 `network_id`の他に、ステータスを含むその他の情報も含まれます。 パラメーターの完全なセットと正確な構文は、 [API ドキュメント](https://developer.adobe.com/experience-cloud/cloud-manager/reference/api/#operation/createNetworkInfrastructure).

この呼び出し後、通常、ネットワークインフラストラクチャがプロビジョニングされるまで 45 ～ 60 分かかります。 API のGETメソッドを呼び出して、現在のステータスを返すことができます。このステータスは、最終的に `creating` から `ready`. すべての状態については、 API ドキュメントを参照してください。

プログラムスコープの VPN 設定が準備できている場合、 `PUT /program/<program_id>/environment/<environment_id>/advancedNetworking` 環境レベルでネットワークを有効にし、任意のポート転送規則を宣言するには、エンドポイントを環境ごとに呼び出す必要があります。 柔軟性を提供するために、環境ごとにパラメーターを設定できます。

詳しくは、 [API ドキュメント](https://developer.adobe.com/experience-cloud/cloud-manager/reference/api/#operation/enableEnvironmentAdvancedNetworkingConfiguration) を参照してください。

VPN 経由でルーティングする必要がある非 http/s プロトコル TCP トラフィックに対して、宛先ホスト（名前または IP、およびポート）のセットを指定して、ポート転送規則を宣言する必要があります。 各宛先ホストについて、お客様は、対象の宛先ポートを30000から30999のポートにマッピングする必要があります。このポートで、値はプログラム内の環境間で一意である必要があります。 また、 `nonProxyHosts` パラメータ。トラフィックが VPN ルーティングをバイパスする URL を宣言しますが、代わりに共有 IP 範囲を通じて宣言します。 それは次のパターンに従う `example.com` または `*.example.com`：ワイルドカードはドメインの開始時にのみサポートされます。

API が数秒で応答し、 `updating` 約 10 分後に、Cloud Manager の環境GETエンドポイントへの呼び出しで、「 `ready`：環境の更新が適用されたことを示します。

環境トラフィックルーティングルール（ホストまたはバイパス）がない場合でも、 `PUT /program/<program_id>/environment/<environment_id>/advancedNetworking` は、空のペイロードと同じように、引き続き呼び出す必要があります。

### VPN の更新 {#updating-the-vpn}

プログラムレベルの VPN 設定は、 `PUT /api/program/<program_id>/network/<network_id>` endpoint.

最初の VPN プロビジョニングの後は、アドレス空間を変更できないことに注意してください。 必要に応じて、カスタマーサポートにお問い合わせください。 また、 `kind` パラメータ (`flexiblePortEgress`, `dedicatedEgressIP` または `VPN`) は変更できません。 サポートが必要な場合は、作成済みの情報と変更の理由をカスタマーサポートに問い合わせてください。

環境ごとのルーティングルールを更新するには、 `PUT /program/{programId}/environment/{environmentId}/advancedNetworking` エンドポイントではなく、設定パラメーターの完全なセットを必ず含めてください。 環境のアップデートの適用には通常 5 ～ 10 分かかります。

### VPN の削除または無効化 {#deleting-or-disabling-the-vpn}

ネットワークインフラストラクチャを削除するには、作成された内容と削除する必要がある理由を説明したカスタマーサポートチケットを送信します。

特定の環境で VPN を無効にするには、を呼び出します。 `DELETE /program/{programId}/environment/{environmentId}/advancedNetworking`. 詳細は、 [API ドキュメント](https://developer.adobe.com/experience-cloud/cloud-manager/reference/api/#operation/disableEnvironmentAdvancedNetworkingConfiguration).

### トラフィックルーティング {#vpn-traffic-routing}

次の表に、トラフィックルーティングを示します。

<table>
<thead>
  <tr>
    <th>トラフィック</th>
    <th>宛先の条件</th>
    <th>ポート</th>
    <th>「接続」</th>
    <th>例</th>
  </tr>
</thead>
<tbody>
  <tr>
    <td><b>HTTP または HTTPS プロトコル</b></td>
    <td>Azure へのトラフィックまたはAdobe サービス</td>
    <td>任意</td>
    <td>（専用 IP ではなく）共有クラスタ IP を介して</td>
    <td>adobe.io<br>api.windows.net</td>
  </tr>
  <tr>
    <td></td>
    <td>次に一致するホスト： <code>nonProxyHosts</code> パラメータ</td>
    <td>80 または 443</td>
    <td>共有クラスタ IP 経由</td>
    <td></td>
  </tr>
  <tr>
    <td></td>
    <td>次に一致するホスト： <code>nonProxyHosts</code> パラメータ</td>
    <td>80 または 443 以外のポート</td>
    <td>ブロック</td>
    <td></td>
  </tr>
  <tr>
    <td></td>
    <td>IP が <i>VPN ゲートウェイアドレス</i> スペース範囲、および http プロキシ設定（標準の Java HTTP クライアントライブラリを使用する http/s トラフィックに対してデフォルトで設定）</td>
    <td>任意</td>
    <td>VPN 経由</td>
    <td><code>10.0.0.1:443</code>ホスト名を指定することもできます。</td>
  </tr>
  <tr>
    <td></td>
    <td>IP が <i>VPN ゲートウェイアドレス空間</i> の範囲、および http プロキシ設定（標準の Java HTTP クライアントライブラリを使用する http/s トラフィックの場合はデフォルトで設定）</td>
    <td>任意</td>
    <td>出力専用 IP を通じて</td>
    <td></td>
  </tr>
  <tr>
    <td></td>
    <td>http プロキシ設定を無視します（例えば、標準の Java HTTP クライアントライブラリから明示的に削除された場合や、標準のプロキシ設定を無視する Java ライブラリを使用している場合）。
</td>
    <td>80 または 443</td>
    <td>共有クラスタ IP 経由</td>
    <td></td>
  </tr>
  <tr>
    <td></td>
    <td>http プロキシ設定を無視します（例えば、標準の Java HTTP クライアントライブラリから明示的に削除された場合や、標準のプロキシ設定を無視する Java ライブラリを使用している場合）。</td>
    <td>80 または 443 以外のポート</td>
    <td>ブロック</td>
    <td></td>
  </tr>
  <tr>
    <td><b>HTTP 以外または HTTPS 以外</b></td>
    <td>IP が <i>VPN ゲートウェイアドレス空間</i> 範囲とクライアントが <code>AEM_PROXY_HOST</code> を使用した env 変数 <code>portOrig</code> 宣言された <code>portForwards</code> API パラメーター</td>
    <td>任意</td>
    <td>VPN 経由</td>
    <td><code>10.0.0.1:3306</code>ホスト名を指定することもできます。</td>
  </tr>
  <tr>
    <td></td>
    <td>IP が <i>VPN ゲートウェイアドレス空間</i> 範囲とクライアントの接続 <code>AEM_PROXY_HOST</code> を使用した env 変数 <code>portOrig</code> 宣言された <code>portForwards</code> API パラメーター</td>
    <td>任意</td>
    <td>出力専用 IP を通じて</td>
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

次の図は、設定と開発に役立つ一連のドメインと関連する IP を視覚的に表したものです。 次の表に、これらのドメインと IP を示します。

![VPN ドメインの構成](/help/security/assets/AdvancedNetworking.jpg)

<table>
<thead>
  <tr>
    <th>ドメインパターン</th>
    <th>出力 (AEMから ) の意味</th>
    <th>入力 (AEM) の意味</th>
  </tr>
</thead>
<tbody>
  <tr>
    <td><code>p{PROGRAM_ID}.external.adobeaemcloud.com</code></td>
    <td>プライベートネットワーク経由ではなく、インターネットに送信されるトラフィック用の専用の出力 IP アドレス </td>
    <td>VPN からの接続は、CDN でこの IP からの接続として表示されます。 VPN からの接続のみをAEMに送信するように設定するには、Cloud Manager でこの IP のみを許可し、その他すべてをブロックするように設定します。 詳細は、「VPN 接続への入力の制限」の節を参照してください。</td>
  </tr>
  <tr>
    <td><code>p{PROGRAM_ID}-gateway.external.adobeaemcloud.com</code></td>
    <td>該当なし</td>
    <td>AEM側の VPN ゲートウェイの IP。 お客様のネットワークエンジニアリングチームは、この機能を使用して、特定の IP アドレスから VPN ゲートウェイへの VPN 接続のみを許可できます。 </td>
  </tr>
  <tr>
    <td><code>p{PROGRAM_ID}.inner.adobeaemcloud.net</code></td>
    <td>VPN のAEM側から顧客側に来るトラフィックの IP。 これを顧客の設定に許可リストに加えるして、接続をAEMからのみ行えるようにできます。</td>
    <td>AEMへの VPN アクセスのみを許可する場合は、マッピングするように CNAME DNS エントリを設定する必要があります <code>author-p{PROGRAM_ID}-e{ENVIRONMENT_ID}.adobeaemcloud.com</code>  および/または <code>publish-p{PROGRAM_ID}-e{ENVIRONMENT_ID}.adobeaemcloud.com</code> をこの値に設定します。</td>
  </tr>
</tbody>
</table>

### VPN を入力接続に制限する {#restrict-vpn-to-ingress-connections}

AEMへの VPN アクセスのみを許可する場合許可リストは、Cloud Manager で環境を設定して、 `p{PROGRAM_ID}.external.adobeaemcloud.com` 環境との通信が許可されています。 これは、Cloud Manager の他の IP ベースのと同じ方法許可リストで実行できます。

ルールをパスベースにする必要がある場合は、Dispatcher レベルで標準の http ディレクティブを使用して、特定の IP を拒否または許可します。 リクエストが常に接触チャネルに到達するように、CDN で目的のパスもキャッシュできないようにする必要があります。

**Httpd 設定の例**

```
Order deny,allow
Deny from all
Allow from 192.168.0.1
Header always set Cache-Control private
```

## 高度なネットワークタイプ間の移行 {#transitioning-between-advanced-networking-types}

以降 `kind` パラメーターを変更できません。既に作成された内容と変更の理由を説明し、サポートが必要な場合はカスタマーサポートにお問い合わせください。
