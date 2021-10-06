---
title: AEM as a Cloud Service用のアドバンスドネットワークの設定
description: VPN やAEM as a Cloud Service用の専用の出力 IP アドレスなど、高度なネットワーク機能を設定する方法を説明します
source-git-commit: e9fa68869ca92945c44a79b783fbc8a53a875e81
workflow-type: tm+mt
source-wordcount: '2797'
ht-degree: 7%

---


# AEM as a Cloud Service用のアドバンスドネットワークの設定 {#configuring-advanced-networking}

>[!INFO]
>
>高度なネットワーク機能は 2021.9.0 リリースの一部で、10 月中旬にお客様向けに有効になります。

AEM as a Cloud Serviceには、Cloud Manager API を使用して設定できる、いくつかのタイプの高度なネットワーク機能が用意されています。 有効なタイプには以下が含まれます。

* [柔軟なポートエグレス](#flexible-port-egress)  — 非標準ポートからの送信トラフィックを許可するようにAEMをas a Cloud Service的に設定
* [専用のエグレス IP アドレス](#dedicated-egress-IP-address)  — 一意の IP から発信されるようにAEM as a Cloud Serviceからのトラフィックを設定します。
* [仮想プライベートネットワーク](#vpn) :VPN テクノロジーを持つお客様向けの、お客様のインフラストラクチャとAEM as a Cloud Service間のトラフィックを保護

この記事では、これらの各オプションの設定方法などについて詳しく説明します。 一般的な設定戦略として、`/networkInfrastructures` API エンドポイントをプログラムレベルで呼び出し、必要な高度なネットワークタイプを宣言し、各環境の `/advancedNetworking` エンドポイントを呼び出して、インフラストラクチャを有効にし、環境固有のパラメータを設定します。 各形式の構文、リクエスト例、応答例については、Cloud Manager API ドキュメントの適切なエンドポイントを参照してください。

Adobeはフレキシブルポートエグレストラフィックのパフォーマンスを最適化できるので、特定の IP アドレスが不要な場合は、フレキシブルポートエグレスと専用のエグレス IP アドレスを決定することをお勧めします。

>[!INFO]
>
>サンドボックスプログラムでは、高度なネットワークは使用できません。

>[!NOTE]
>
>既にレガシー専用のエグレステクノロジーをプロビジョニング済みで、これらのオプションの 1 つを設定する必要があるお客様は、そうしないでください。そうしないと、サイト接続に影響が出る場合があります。 不明な点は、Adobeサポートにお問い合わせください。

## フレキシブルポートエグレス {#flexible-port-egress}

この高度なネットワーク機能を使用すると、AEM as a Cloud Serviceを設定して、HTTP（ポート 80）および HTTPS（ポート 443）以外のポート（デフォルトで開いている）を介してトラフィックを出力できます。

### 検討事項 {#flexible-port-egress-considerations}

VPN が不要で、専用のエグレスに依存しないトラフィックは高いスループットを達成できるので、専用のエグレス IP アドレスが不要な場合は、柔軟なポートエグレスを選択することをお勧めします。

### 設定 {#configuring-flexible-port-egress-provision}

プログラムごとにPOST`/program/<programId>/networkInfrastructures` エンドポイントが呼び出され、`kind` パラメーターと領域に対して `flexiblePortEgress` の値が渡されます。 エンドポイントは `network_id` と、ステータスを含む他の情報で応答します。 パラメーターの完全なセットと正確な構文は、 API ドキュメントで参照する必要があります。

この呼び出し後、通常、ネットワークインフラストラクチャがプロビジョニングされるまで約 15 分かかります。 Cloud Manager の [ 環境GETエンドポイント ](https://developer.adobe.com/experience-cloud/cloud-manager/reference/api/#operation/getEnvironment) を呼び出すと、ステータスは「準備完了」と表示されます。

プログラムスコープのフレキシブルポートエグレス設定が準備できた場合、環境レベルでネットワークを有効にし、ポート転送規則を宣言するには、環境ごとに `PUT /program/<program_id>/environment/<environment_id>/advancedNetworking` エンドポイントを呼び出す必要があります。 柔軟性を提供するために、環境ごとにパラメーターを設定できます。

ポート転送規則は、宛先ホストのセット（名前または IP、およびポートを含む）を指定することで、80/443以外のポートに対して宣言する必要があります。 各宛先ホストに対して、お客様は、目的の宛先ポートを30000 ～ 30999のポートにマッピングする必要があります。

API は数秒で応答し、更新のステータスを示し、約 10 分後にエンドポイントの `GET` メソッドで、高度なネットワークが有効になっていることを示す必要があります。

### アップデート {#updating-flexible-port-egress-provision}

プログラムレベルの設定は、`PUT /api/program/<program_id>/network/<network_id>` エンドポイントを呼び出すことで更新でき、数分以内に有効になります。

>[!NOTE]
>
> 「kind」パラメーター (`flexiblePortEgress`、`dedicatedEgressIP`、`VPN`) は変更できません。 作成済みの情報と変更の理由を説明したサポートについては、カスタマーサポートにお問い合わせください。

`PUT /program/{programId}/environment/{environmentId}/advancedNetworking` エンドポイントを再度呼び出して、環境ごとのポート転送ルールを更新し、設定パラメーターの完全なセットをサブセットではなく必ず含めます。

### フレキシブルポートエグレスの削除または無効化 {#deleting-disabling-flexible-port-egress-provision}

ネットワークインフラストラクチャを **削除** するには、作成された内容と削除する必要がある理由を説明したカスタマーサポートチケットを送信します。

**特定の環境からの** 柔軟なポート出力を無効にするには、`DELETE [/program/{programId}/environment/{environmentId}/advancedNetworking]()` を呼び出します。

詳しくは、[Cloud Manager API ドキュメント ](https://developer.adobe.com/experience-cloud/cloud-manager/reference/api/#operation/disableEnvironmentAdvancedNetworkingConfiguration) を参照してください。

### トラフィックルーティング {#flexible-port-egress-traffic-routing}

ポート 80 または 443 を介して宛先に送られる HTTP トラフィックまたは HTTPS トラフィックは、標準の Java ネットワークライブラリが使用される場合、事前に設定されたプロキシを経由します。 他のポートを経由する http トラフィックまたは https トラフィックの場合は、次のプロパティを使用してプロキシを設定する必要があります。

* `AEM_HTTP_PROXY_HOST / AEM_HTTPS_PROXY_HOST`
* `AEM_HTTP_PROXY_PORT / AEM_HTTPS_PROXY_PORT`

例えば、`www.example.com:8443` に要求を送信するコード例を次に示します。

```java
HttpsHost target = new HttpsHost("example.com", 8443, "https");
 
HttpHost proxy = new HttpHost(System.getenv("AEM_HTTPS_PROXY_HOST"),
                              Integer.parseInt(System.getenv("AEM_HTTPS_PROXY_PORT")),
                              "https");
 
RequestConfig config = RequestConfig.custom().setProxy(proxy).build();
 
HttpGet request = new HttpGet("/");
request.setConfig(config);
CloseableHttpResponse response = httpclient.execute(target, request);
```

非標準の Java ネットワークライブラリを使用する場合は、上記のプロパティを使用して、すべてのトラフィックにプロキシを設定します。

`portForwards` パラメーターで宣言されたポートを介して、宛先との間の非 http/s トラフィックでは、`AEM_PROXY_HOST` と呼ばれるプロパティと、マッピングされたポートを参照する必要があります。 例えば、次の操作が可能です。

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
    <td>80 または 443 外のポート</td>
    <td>許可</td>
  </tr>
  <tr>
    <td></td>
    <td>非標準トラフィック（ポート 80 または 443 以外の他のポートで）は http プロキシを使用しない</td>
    <td>80 または 443 外のポート</td>
    <td>ブロック</td>
    <td></td>
  </tr>
  <tr>
    <td><b>非 http または非 https</b></td>
    <td>クライアントは、 <code>portForwards</code> API パラメーターで宣言された <code>portOrig</code> を使用して <code>AEM_PROXY_HOST</code> 環境変数に接続します。</td>
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

**Apache/Dispatcher の設定**

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
>2021 年 9 月リリース (10/6/21) より前に、専用のエグレス IP がプロビジョニングされている場合は、[ 従来の専用エグレスアドレスのお客様 ](#legacy-dedicated-egress-address-customers) を参照してください。

### メリット {#benefits}

この専用 IP アドレスは、SaaS ベンダー（CRM ベンダーなど）との統合や、IP アドレスの許可リストをオファーする AEM as a Cloud Service 以外と統合する場合のセキュリティを強化します。専用 IP アドレスをに追加す許可リストることで、お客様のAEM Cloud Serviceからのトラフィックのみが外部サービスに送られるようにします。 これは、その他の許可されている IP からのトラフィックに加えられるものです。

専用 IP アドレス機能を有効にしない場合、AEM as a Cloud Service から出ていくトラフィックは、他の顧客と共有する一連の IP を流れていきます。

### 設定 {#configuring-dedicated-egress-provision}

>[!INFO]
>
>専用のエグレス IP アドレスからは、Splunk 転送機能は使用できません。

専用の出力 IP アドレスの設定は、[ フレキシブルポートの出力 ](#configuring-flexible-port-egress-provision) と同じです。

主な違いは、トラフィックが常に専用の一意の IP から抜け出すということです。 この IP を見つけるには、DNS リゾルバを使用して `p{PROGRAM_ID}.external.adobeaemcloud.com` に関連付けられた IP アドレスを特定します。 IP アドレスは変更されるとは限りませんが、将来変更が必要になる場合は、詳細な通知が表示されます。

`PUT /program/<program_id>/environment/<environment_id>/advancedNetworking` エンドポイントのフレキシブルポートエグレスでサポートされるルーティングルールに加えて、専用のエグレス IP アドレスは `nonProxyHosts` パラメータをサポートします。 これにより、専用 IP ではなく共有 IP アドレス範囲を経由してルーティングするホストのセットを宣言できます。これは、共有 IP を介してエグスするトラフィックをさらに最適化できるので便利です。 `nonProxyHost` URL は、`example.com` または `*.example.com` のパターンに従うことができます。この場合、ワイルドカードはドメインの開始時にのみサポートされます。

Adobeはフレキシブルポートエグレストラフィックのパフォーマンスを最適化できるので、フレキシブルポートエグレスと専用エグレス IP アドレスを決定する際には、特定の IP アドレスが不要な場合は、フレキシブルポートエグレスを選択する必要があります。

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
    <td>（専用 IP ではなく）共有クラスタ IP を使用</td>
    <td>adobe.io<br>api.windows.net</td>
  </tr>
  <tr>
    <td></td>
    <td><code>nonProxyHosts</code> パラメーターと一致するホスト</td>
    <td>80 または 443</td>
    <td>共有クラスター IP を使用</td>
    <td></td>
  </tr>
  <tr>
    <td></td>
    <td><code>nonProxyHosts</code> パラメーターと一致するホスト</td>
    <td>80 または 443 外のポート</td>
    <td>ブロック</td>
    <td></td>
  </tr>
  <tr>
    <td></td>
    <td>HTTP プロキシ設定を使用。標準の Java HTTP クライアントライブラリを使用する HTTP/s トラフィックにはデフォルトで設定されます。</td>
    <td>任意</td>
    <td>出力専用 IP を使用</td>
    <td></td>
  </tr>
  <tr>
    <td></td>
    <td>http プロキシ設定を無視する（例えば、標準の Java HTTP クライアントライブラリから明示的に削除された場合や、標準のプロキシ設定を無視する Java ライブラリが使用されている場合）</td>
    <td>80 または 443</td>
    <td>共有クラスター IP を使用</td>
    <td></td>
  </tr>
  <tr>
    <td></td>
    <td>http プロキシ設定を無視する（例えば、標準の Java HTTP クライアントライブラリから明示的に削除された場合や、標準のプロキシ設定を無視する Java ライブラリが使用されている場合）</td>
    <td>80 または 443 外のポート</td>
    <td>ブロック</td>
    <td></td>
  </tr>
  <tr>
    <td><b>非 http または非 https</b></td>
    <td>クライアントは、 <code>portForwards</code> API パラメーターで宣言された <code>portOrig</code> を使用して <code>AEM_PROXY_HOST</code> env 変数に接続します</td>
    <td>任意</td>
    <td>出力専用 IP を使用</td>
    <td><code>mysql.example.com:3306</code></td>
  </tr>
  <tr>
    <td></td>
    <td>その他</td>
    <td></td>
    <td>ブロック</td>
    <td></td>
  </tr>
</tbody>
</table>

## レガシーの出力専用アドレスのお客様 {#legacy-dedicated-egress-address-customers}

2021.09.30以前に専用のエグレス IP がプロビジョニングされている場合は、専用のエグレス IP 機能は以下の説明どおりに動作します。

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

一部のライブラリでは、プロキシ設定に標準の Java システムプロパティを使用するために明示的な設定が必要です。

Apache HttpClient を使用する例で、
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

期待される専用 IP アドレスでトラフィックが実際に送信されていることを検証するには、目的のサービスでログを確認します（可能な場合）。それ以外の場合は、[https://ifconfig.me/IP](https://ifconfig.me/IP) などのデバッグサービスを呼び出すと、呼び出し元の IP アドレスが返されるので便利です。

## 仮想プライベートネットワーク (VPN) {#vpn}

VPN を使用すると、オーサー、パブリッシュ、またはプレビューからオンプレミスのインフラストラクチャまたはデータセンターに接続できます。 例えば、データベースにアクセスする方法の場合です。

また、VPN をサポートする CRM ベンダーや、企業ネットワークからAEMas a Cloud Serviceの作成者、プレビュー、パブリッシュに接続するなど、SaaS ベンダーに接続することもできます。

IPSec テクノロジを備えたほとんどの VPN デバイスがサポートされています。 **RouteBased configuration instructions** 列の情報に基づいて、[ このページ ](https://docs.microsoft.com/en-us/azure/vpn-gateway/vpn-gateway-about-vpn-devices#devicetable) にあるデバイスのリストを参照してください。 表の説明に従って、デバイスを設定します。

### 一般的な考慮事項 {#general-vpn-considerations}

* サポートは単一の VPN 接続に制限されています
* VPN 接続を介して Splunk 転送機能を実行することはできません。

### 作品 {#vpn-creation}

プログラムごとにPOST`/program/<programId>/networkInfrastructures` エンドポイントが呼び出され、次のような設定情報のペイロードが渡されます。`kind` パラメータ、地域、アドレス空間（CIDR の一覧）、DNS リゾルバ（お客様のネットワークで名前を解決するため）、VPN 接続情報（ゲートウェイ設定、共有 VPN キー、IP セキュリティポリシーなど）の「vpn」の値。 エンドポイントは `network_id` と、ステータスを含む他の情報で応答します。 パラメーターの完全なセットと正確な構文は、[API のドキュメント ](https://developer.adobe.com/experience-cloud/cloud-manager/reference/api/#operation/createNetworkInfrastructure) を参照してください。

呼び出されると、通常、ネットワークインフラストラクチャがプロビジョニングされるまでに 45 ～ 60 分かかります。 API のGETメソッドを呼び出して、現在のステータスを返すことができます。このステータスは、最終的に `creating` から `ready` に反転します。 すべての状態については、 API のドキュメントを参照してください。

プログラム範囲の VPN 設定が準備できている場合は、環境レベルでネットワークを有効にし、ポート転送規則を宣言するには、環境ごとに `PUT /program/<program_id>/environment/<environment_id>/advancedNetworking` エンドポイントを呼び出す必要があります。 柔軟性を提供するために、環境ごとにパラメーターを設定できます。

詳しくは、[API のドキュメント ](https://developer.adobe.com/experience-cloud/cloud-manager/reference/api/#operation/enableEnvironmentAdvancedNetworkingConfiguration) を参照してください。

VPN 経由でルーティングする必要がある非 HTTP/s プロトコル TCP トラフィックに対して、ポート転送規則を宣言する必要があります。宛先ホストのセット（名前または IP、およびポート）を指定します。 各宛先ホストに対して、お客様は、目的の宛先ポートを30000から30999のポートにマッピングする必要があります。このポートでは、値はプログラム内の環境間で一意である必要があります。 また、`nonProxyHosts` パラメーターに URL のセットをリストすることもできます。このパラメーターは、トラフィックが VPN ルーティングをバイパスする必要があるが、共有 IP 範囲を通じて URL を宣言します。 `example.com` または `*.example.com` のパターンに従います。この場合、ワイルドカードはドメインの開始時にのみサポートされます。

API が数秒で応答し、ステータスが `updating` で、約 10 分後に Cloud Manager の環境GETエンドポイントへの呼び出しで、ステータスが `ready` と表示され、環境への更新が適用されたことを示します。

環境トラフィックルーティングルール（ホストまたはバイパス）がない場合でも、空のペイロードを使用して `PUT /program/<program_id>/environment/<environment_id>/advancedNetworking` を引き続き呼び出す必要があります。

### VPN の更新 {#updating-the-vpn}

`PUT /api/program/<program_id>/network/<network_id>` エンドポイントを呼び出すことで、プログラムレベルの VPN 設定を更新できます。

最初の VPN プロビジョニングの後は、アドレス空間を変更できないことに注意してください。 必要な場合は、カスタマーサポートにお問い合わせください。 また、`kind` パラメーター (`flexiblePortEgress`、`dedicatedEgressIP`、`VPN`) は変更できません。 作成済みの情報と変更の理由を説明したサポートについては、カスタマーサポートにお問い合わせください。

環境ごとのルーティングルールを更新するには、`PUT /program/{programId}/environment/{environmentId}/advancedNetworking` エンドポイントを再度呼び出し、設定パラメーターの完全なセットをサブセットではなく必ず含めます。 環境の更新は、通常、適用されるまでに 5 ～ 10 分かかります。

### VPN の削除または無効化 {#deleting-or-disabling-the-vpn}

ネットワークインフラストラクチャを削除するには、作成された内容と削除する必要がある理由を説明したカスタマーサポートチケットを送信します。

特定の環境で VPN を無効にするには、`DELETE /program/{programId}/environment/{environmentId}/advancedNetworking` を呼び出します。 詳しくは、[API ドキュメント ](https://developer.adobe.com/experience-cloud/cloud-manager/reference/api/#operation/disableEnvironmentAdvancedNetworkingConfiguration) を参照してください。

### トラフィックルーティング {#vpn-traffic-routing}

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
    <td>Azure へのトラフィックまたはAdobe サービス</td>
    <td>任意</td>
    <td>（専用 IP ではなく）共有クラスタ IP を使用</td>
    <td>adobe.io<br>api.windows.net</td>
  </tr>
  <tr>
    <td></td>
    <td><code>nonProxyHosts</code> パラメーターと一致するホスト</td>
    <td>80 または 443</td>
    <td>共有クラスター IP を使用</td>
    <td></td>
  </tr>
  <tr>
    <td></td>
    <td><code>nonProxyHosts</code> パラメーターと一致するホスト</td>
    <td>80 または 443 外のポート</td>
    <td>ブロック</td>
    <td></td>
  </tr>
  <tr>
    <td></td>
    <td>IP が <i>VPN ゲートウェイアドレス </i> の領域範囲にあり、HTTP プロキシ設定を使用する場合（標準の Java HTTP クライアントライブラリを使用する http/s トラフィックの場合は、デフォルトで設定）。</td>
    <td>任意</td>
    <td>VPN 経由</td>
    <td><code>10.0.0.1:443</code>ホスト名を指定することもできます。</td>
  </tr>
  <tr>
    <td></td>
    <td>IP が <i>VPN ゲートウェイアドレス空間 </i> の範囲に含まれず、HTTP プロキシ設定を使用する場合（標準の Java HTTP クライアントライブラリを使用する http/s トラフィックの場合は、デフォルトで設定されます）。</td>
    <td>任意</td>
    <td>出力専用 IP を使用</td>
    <td></td>
  </tr>
  <tr>
    <td></td>
    <td>HTTP プロキシ設定を無視する（例えば、標準の Java HTTP クライアントライブラリから明示的に削除された場合や、標準のプロキシ設定を無視する Java ライブラリを使用している場合）
</td>
    <td>80 または 443</td>
    <td>共有クラスター IP を使用</td>
    <td></td>
  </tr>
  <tr>
    <td></td>
    <td>HTTP プロキシ設定を無視する（例えば、標準の Java HTTP クライアントライブラリから明示的に削除された場合や、標準のプロキシ設定を無視する Java ライブラリを使用している場合）</td>
    <td>80 または 443 外のポート</td>
    <td>ブロック</td>
    <td></td>
  </tr>
  <tr>
    <td><b>非 http または非 https</b></td>
    <td>IP が <i>VPN ゲートウェイアドレス空間 </i> の範囲に該当し、クライアントが <code>portForwards</code> API パラメータで宣言された <code>portOrig</code> を使用して <code>AEM_PROXY_HOST</code> env 変数に接続する場合</td>
    <td>任意</td>
    <td>VPN 経由</td>
    <td><code>10.0.0.1:3306</code>ホスト名を指定することもできます。</td>
  </tr>
  <tr>
    <td></td>
    <td>IP が <i>VPN ゲートウェイアドレス空間 </i> の範囲に含まれず、クライアントが <code>portForwards</code> API パラメータで宣言された <code>portOrig</code> を使用して <code>AEM_PROXY_HOST</code>env 変数に接続する場合</td>
    <td>任意</td>
    <td>出力専用 IP を使用</td>
    <td></td>
  </tr>
  <tr>
    <td></td>
    <td>その他</td>
    <td>任意</td>
    <td>ブロック</td>
    <td></td>
  </tr>
</tbody>
</table>

### 設定に役立つドメイン{#vpn-useful-domains-for-configuration}

次の図は、設定と開発に役立つ一連のドメインと関連する IP を視覚的に表したものです。 次の表に、これらのドメインと IP を示します。

![VPN ドメインの設定](/help/security/assets/AdvancedNetworking.jpg)

<table>
<thead>
  <tr>
    <th>ドメインパターン</th>
    <th>出口 (AEMから ) の意味</th>
    <th>入力 (AEM) の意味</th>
  </tr>
</thead>
<tbody>
  <tr>
    <td><code>p{PROGRAM_ID}.external.adobeaemcloud.com</code></td>
    <td>プライベートネットワーク経由ではなく、インターネットへのトラフィックに対する専用の出力 IP アドレス </td>
    <td>VPN からの接続は、CDN でこの IP からの接続として表示されます。 VPN からの接続のみをAEMに送信するには、Cloud Manager を設定して、この IP のみを許可し、その他すべてをブロックします。 詳細は、「VPN 接続への入力の制限」の節を参照してください。</td>
  </tr>
  <tr>
    <td><code>p{PROGRAM_ID}-gateway.external.adobeaemcloud.com</code></td>
    <td>該当なし</td>
    <td>AEM側の VPN ゲートウェイの IP。 お客様のネットワークエンジニアリングチームは、これを使用して、特定の IP アドレスから VPN ゲートウェイへの VPN 接続のみを許可できます。 </td>
  </tr>
  <tr>
    <td><code>p{PROGRAM_ID}.inner.adobeaemcloud.net</code></td>
    <td>VPN のAEM側から顧客側に向かうトラフィックの IP。 これを顧客の設定で許可リストに加えるして、接続をAEMからのみ確立できます。</td>
    <td>AEMへの VPN アクセスのみを許可する場合は、<code>author-p{PROGRAM_ID}-e{ENVIRONMENT_ID}.adobeaemcloud.com</code> や <code>publish-p{PROGRAM_ID}-e{ENVIRONMENT_ID}.adobeaemcloud.com</code> をこれにマッピングするように CNAME DNS エントリを設定する必要があります。</td>
  </tr>
</tbody>
</table>

### VPN を入力接続に制限する {#restrict-vpn-to-ingress-connections}

AEMへの VPN アクセスのみを許可する場合許可リストは、`p{PROGRAM_ID}.external.adobeaemcloud.com` で定義された IP のみが環境と通信できるように、Cloud Manager で環境を設定できます。 これは、Cloud Manager の他の IP ベースのと同じ許可リスト方法で実行できます。

ルールをパスベースにする必要がある場合は、Dispatcher レベルで標準の http ディレクティブを使用して、特定の IP を拒否または許可します。 リクエストが常に接触チャネルに到達するように、CDN で目的のパスもキャッシュできないようにする必要があります。

**Httpd 設定の例**

```
Order deny,allow
Deny from all
Allow from 192.168.0.1
Header always set Cache-Control private
```

## 高度なネットワークタイプ間の移行 {#transitioning-between-advanced-networking-types}

`kind` パラメーターは変更できないので、カスタマーサポートにお問い合わせください。作成済みの情報と変更の理由を説明します。