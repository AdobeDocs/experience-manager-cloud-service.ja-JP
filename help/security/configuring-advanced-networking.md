---
title: AEM as a Cloud Service の高度なネットワーク機能の設定
description: AEM as a Cloud Service の高度なネットワーク機能（VPN やフレキシブルエグレス IP アドレスまたは専用エグレス IP アドレスなど）を設定する方法を説明します
exl-id: 968cb7be-4ed5-47e5-8586-440710e4aaa9
source-git-commit: a284c0139b45e618749866385cdcc81d1ceb61e7
workflow-type: tm+mt
source-wordcount: '5145'
ht-degree: 44%

---


# AEM as a Cloud Service の高度なネットワーク機能の設定 {#configuring-advanced-networking}

この記事では、AEMas a Cloud Serviceの様々な高度なネットワーク機能（VPN のセルフサービスと API プロビジョニング、非標準ポート、専用の出力 IP アドレスなど）を紹介します。

>[!TIP]
>
>このドキュメントに加えて、このドキュメントの各高度なネットワークオプションについて順を追って説明するための一連のチュートリアルも用意されています [場所。](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/networking/advanced-networking.html)

## 概要 {#overview}

AEM as a Cloud Serviceでは、次の高度なネットワークオプションを提供しています。

* [柔軟なポートエグレス](#flexible-port-egress)  — 非標準ポートからの送信トラフィックを許可するようにAEMをas a Cloud Service的に設定します。
* [出力専用 IP アドレス](#dedicated-egress-ip-address)  — 固有の IP から発信されるようにAEM as a Cloud Serviceからのトラフィックを設定します。
* [仮想プライベートネットワーク (VPN)](#vpn) - VPN を使用している場合、インフラストラクチャとAEMas a Cloud Service間のトラフィックを保護します。

この記事では、まず、これらの各オプションの詳細と使用理由を説明し、Cloud Manager UI を使用した設定方法と API を使用した設定方法を説明し、高度な使用例で締めくくります。

>[!CAUTION]
>
>既にレガシー専用の出力テクノロジーがプロビジョニングされていて、次の高度なネットワークオプションのいずれかを設定したい場合は、 [まず、AdobeClientCare にお問い合わせください。](https://experienceleague.adobe.com/?support-solution=Experience+Manager&amp;lang=ja#home)
>
>レガシーエグレステクノロジーを使用した高度なネットワークを設定しようとすると、サイトの接続に影響を与える可能性があります。

### 要件と制限事項 {#requirements}

高度なネットワーク機能を設定する場合、次の制限が適用されます。

* プログラムは、単一の高度なネットワークオプション（柔軟なポートエグレス、専用のエグレス IP アドレス、または VPN）をプロビジョニングできます。
* には高度なネットワーク機能がありません [サンドボックスプログラム。](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/program-types.md)
* のユーザーは、 **管理者** の役割を追加し、プログラムにネットワークインフラストラクチャを設定します。
* 実稼動環境は、ネットワークインフラストラクチャをプログラムに追加する前に作成する必要があります。
* ネットワークインフラストラクチャは、実稼動環境のプライマリ領域と同じ領域に存在する必要があります。
   * 実稼動環境に [その他の公開地域](/help/implementing/cloud-manager/manage-environments.md#multiple-regions) 追加の地域ごとに、ネットワークインフラストラクチャのミラーリングを追加で作成できます。
   * 実稼動環境で設定された最大地域数を超えるネットワークインフラストラクチャを作成することはできません。
   * ネットワークインフラストラクチャは、実稼動環境で利用可能な地域と同じ数だけ定義できますが、新しいインフラストラクチャは、以前に作成したインフラストラクチャと同じタイプである必要があります。
   * 複数のインフラストラクチャを作成する場合、高度なネットワークインフラストラクチャが作成されていない地域のみから選択できます。

### アドバンスネットワークの構成と有効化 {#configuring-enabling}

高度なネットワーク機能を使用するには、次の 2 つの手順が必要です。

1. アドバンスドネットワークオプションの設定 ( [柔軟なポートエグレス](#flexible-port-egress) [出力専用 IP アドレス](#dedicated-egress-ip-address) または [VPN](#vpn) は、まずプログラムレベルでおこなう必要があります。
1. 使用するには、環境レベルで [ 詳細ネットワーク ] オプションを有効にする必要があります。

両方の手順は、Cloud Manager UI または Cloud Manager API を使用して実行できます。

* Cloud Manager UI を使用する場合、プログラムレベルのウィザードを使用して高度なネットワーク設定を作成し、設定を有効にする各環境を編集します。

* Cloud Manager API を使用する場合、 `/networkInfrastructures` API エンドポイントは、プログラムレベルで呼び出され、必要な種類の高度なネットワークを宣言した後、 `/advancedNetworking` エンドポイントを使用して、インフラストラクチャを有効にし、環境固有のパラメーターを設定します。

## フレキシブルポートエグレス {#flexible-port-egress}

高度なネットワーク機能を使用すると、デフォルトで開いている HTTP（ポート 80）と HTTPS（ポート 443）以外のポートからトラフィックを送信するように、AEM as a Cloud Service を設定することができます。

>[!TIP]
>
>フレキシブルポートエグレス IP アドレスと専用エグレス IP アドレスのどちらを選択する場合は、特定の IP アドレスが必要なければ、フレキシブルポートエグレスを選択することをお勧めします。アドビ側でフレキシブルポートエグレストラフィックのパフォーマンスを最適化できるからです。

>[!NOTE]
>
>作成後は、柔軟なポートエグレスインフラストラクチャタイプは編集できません。 設定値を変更する唯一の方法は、設定値を削除して再作成することです。

### UI 設定 {#configuring-flexible-port-egress-provision-ui}

1. [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) で Cloud Manager にログインし、適切な組織を選択します。

1. 次の日： **[マイプログラム](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/editing-programs.md#my-programs)** 画面で、プログラムを選択します。

1. 次から： **プログラムの概要** ページで、 **環境** 「 」タブで「 」を選択します。 **ネットワークインフラストラクチャ** をクリックします。

   ![ネットワークインフラストラクチャの追加](assets/advanced-networking-ui-network-infrastructure.png)

1. Adobe Analytics の **ネットワークインフラストラクチャの追加** ウィザードを開始し、「 」を選択します。 **柔軟なポートエグレス** また、 **地域** ドロップダウンメニューでタップまたはクリック **続行**.

   ![フレキシブルポートエグレスの設定](assets/advanced-networking-ui-flexible-port-egress.png)

1. The **確認** 「 」タブに、選択内容と次の手順の概要が表示されます。 タップまたはクリック **保存** インフラストラクチャを作成する。

   ![フレキシブルポートエグレスの設定の確認](assets/advanced-networking-ui-flexible-port-egress-confirmation.png)

新しいレコードが **ネットワークインフラストラクチャ** サイドパネルの見出し（インフラストラクチャのタイプ、ステータス、地域、有効にされた環境の詳細を含む）。

![ネットワークインフラストラクチャの新しいエントリ](assets/advanced-networking-ui-flexible-port-egress-new-entry.png)

>[!NOTE]
>
>柔軟なポートエグレス用のインフラストラクチャの作成には、環境レベルで構成できるようになるまで、最大 1 時間かかる場合があります。

### API 設定 {#configuring-flexible-port-egress-provision-api}

プログラムごとに 1 回、POST `/program/<programId>/networkInfrastructures` エンドポイントが呼び出され、`kind` パラメーターの `flexiblePortEgress` の値とリージョンが渡されます。エンドポイントは、 `network_id`、およびステータスを含むその他の情報。

呼び出しの後、ネットワークインフラストラクチャがプロビジョニングされるまで、通常は 15 分ほどかかります。Cloud Manager の [ネットワークインフラストラクチャGETエンドポイント](https://developer.adobe.com/experience-cloud/cloud-manager/reference/api/#operation/getNetworkInfrastructure) 次のステータスを示す **準備完了**.

>[!TIP]
>
>パラメーターの完全なセット、正確な構文、および後で変更できないパラメーターなどの重要な情報。 [は API ドキュメントで参照できます。](https://developer.adobe.com/experience-cloud/cloud-manager/reference/api/#operation/createNetworkInfrastructure)

### トラフィックルーティング {#flexible-port-egress-traffic-routing}

80 または 443 以外のポートに送信される http または https トラフィックの場合、次のホストおよびポート環境変数を使用してプロキシを設定する必要があります。

* HTTP の場合： `AEM_PROXY_HOST`／`AEM_HTTP_PROXY_PORT `（AEM リリース 6094 未満では、デフォルトは `proxy.tunnel:3128`）
* HTTPS の場合： `AEM_PROXY_HOST`／`AEM_HTTPS_PROXY_PORT `（AEM リリース 6094 未満では、デフォルトは `proxy.tunnel:3128`）

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

`portForwards` パラメーターで宣言したポートで宛先とやり取りする HTTP/HTTPS 以外のトラフィックは、マッピングされたポートと共に、`AEM_PROXY_HOST` というプロパティを参照する必要があります。次に例を示します。

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
    <td>次の環境変数とプロキシポート番号を使用して設定された http プロキシを介した（80 または 443 以外の他のポートでの）非標準トラフィック。Cloud Manager API 呼び出しの portForwards パラメーターで宛先ポートを宣言しないでください。<br><ul>
     <li>AEM_PROXY_HOST（AEM リリース 6094 未満では、デフォルトは `proxy.tunnel`）</li>
     <li>AEM_HTTPS_PROXY_PORT（AEM リリース 6094 未満では、デフォルトはポート 3128）</li>
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

#### Apache/Dispatcher 設定 {#apache-dispatcher}

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

## 出力専用 IP アドレス {#dedicated-egress-ip-address}

専用 IP アドレスを使用すると、SaaS ベンダー（CRM ベンダーなど）との統合や、IP アドレスのAEMを提供するas a Cloud Service以外との統合により、セキュリティを強化できま許可リストに加えるす。 専用 IP アドレスを許可リストに追加することで、顧客の AEM Cloud Service からのトラフィックのみが外部サービスに送信されるようになります。これは、その他の許可されている IP からのトラフィックに加えられるものです。

同じ専用 IP が、Adobe組織内のすべてのプログラムと、各プログラム内のすべての環境に適用されます。 オーサーサービスとパブリッシュサービスの両方に適用されます。

専用 IP アドレス機能を有効にしない場合、AEMから出てくるトラフィックは、他のAEMas a Cloud Serviceのお客様と共有される一連の IP を流れます。

専用の出力 IP アドレスの設定は、 [フレキシブルポートエグレス。](#flexible-port-egress) 主な違いは、設定後、トラフィックは常に専用の一意の IP から出てくるという点です。 その IP を確認するには、DNS リゾルバーを使用して、`p{PROGRAM_ID}.external.adobeaemcloud.com` に関連付けられている IP アドレスを特定します。IP アドレスは変更されるとは想定されていませんが、変更が必要な場合は、詳細な通知が表示されます。

>[!TIP]
>
>フレキシブルポートエグレス IP アドレスと専用エグレス IP アドレスのどちらを選択する場合は、特定の IP アドレスが必要なければ、フレキシブルポートエグレスを選択することをお勧めします。アドビ側でフレキシブルポートエグレストラフィックのパフォーマンスを最適化できるからです。

>[!NOTE]
>
>2021.09.30より前（2021 年 9 月リリースより前）に、専用のエグレス IP がプロビジョニングされていた場合、専用のエグレス IP 機能は HTTP ポートと HTTPS ポートのみをサポートします。
>
>これには、HTTP/1.1 と HTTP/2（暗号化時）が含まれます。また、1 つの専用の出力エンドポイントは、それぞれポート 80／443 の HTTP／HTTPS 経由でのみ任意のターゲットと通信できます。

>[!NOTE]
>
>作成後は、専用の出力 IP アドレスインフラストラクチャタイプは編集できません。 設定値を変更する唯一の方法は、設定値を削除して再作成することです。

>[!INFO]
>
>Splunk 転送機能は専用エグレス IP アドレスからは使用できません。

### UI 設定 {#configuring-dedicated-egress-provision-ui}

1. [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) で Cloud Manager にログインし、適切な組織を選択します。

1. 次の日： **[マイプログラム](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/editing-programs.md#my-programs)** 画面で、プログラムを選択します。

1. 次から： **プログラムの概要** ページで、 **環境** 「 」タブで「 」を選択します。 **ネットワークインフラストラクチャ** をクリックします。

   ![ネットワークインフラストラクチャの追加](assets/advanced-networking-ui-network-infrastructure.png)

1. Adobe Analytics の **ネットワークインフラストラクチャの追加** ウィザードを開始し、「 」を選択します。 **出力専用 IP アドレス** また、 **地域** ドロップダウンメニューでタップまたはクリック **続行**.

   ![出力専用 IP アドレスの設定](assets/advanced-networking-ui-dedicated-egress.png)

1. The **確認** 「 」タブに、選択内容と次の手順の概要が表示されます。 タップまたはクリック **保存** インフラストラクチャを作成する。

   ![フレキシブルポートエグレスの設定の確認](assets/advanced-networking-ui-dedicated-egress-confirmation.png)

新しいレコードが **ネットワークインフラストラクチャ** サイドパネルの見出し（インフラストラクチャのタイプ、ステータス、地域、有効にされた環境の詳細を含む）。

![ネットワークインフラストラクチャの新しいエントリ](assets/advanced-networking-ui-flexible-port-egress-new-entry.png)

>[!NOTE]
>
>柔軟なポートエグレス用のインフラストラクチャの作成には、環境レベルで構成できるようになるまで、最大 1 時間かかる場合があります。

### API 設定 {#configuring-dedicated-egress-provision-api}

プログラムごとに 1 回、POST `/program/<programId>/networkInfrastructures` エンドポイントが呼び出され、`kind` パラメーターの `dedicatedEgressIp` の値とリージョンが渡されます。エンドポイントは、 `network_id`、およびステータスを含むその他の情報。

呼び出しの後、ネットワークインフラストラクチャがプロビジョニングされるまで、通常は 15 分ほどかかります。Cloud Manager の [ネットワークインフラストラクチャGETエンドポイント](https://developer.adobe.com/experience-cloud/cloud-manager/reference/api/#operation/getNetworkInfrastructure) 次のステータスを示す **準備完了**.

>[!TIP]
>
>パラメーターの完全なセット、正確な構文、および後で変更できないパラメーターなどの重要な情報。 [は API ドキュメントで参照できます。](https://developer.adobe.com/experience-cloud/cloud-manager/reference/api/#operation/createNetworkInfrastructure)

### トラフィックルーティング {#dedicated-egress-ip-traffic-routing}

プロキシ設定に標準の Java システムプロパティを使用する場合、http や https のトラフィックは事前に設定されたプロキシを経由します。

`portForwards` パラメーターで宣言したポートで宛先とやり取りする HTTP/HTTPS 以外のトラフィックは、マッピングされたポートと共に、`AEM_PROXY_HOST` というプロパティを参照する必要があります。次に例を示します。

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

### デバッグの考慮事項 {#debugging-considerations}

期待される専用 IP アドレスでトラフィックが実際に発信されていることを検証するには、目的のサービスでログを確認します（可能な場合）。それ以外の場合は、呼び出し元の IP アドレスを返す [https://ifconfig.me/IP](https://ifconfig.me/IP) などのデバッグサービスを呼び出すと便利です。

## 仮想プライベートネットワーク（VPN） {#vpn}

VPN を使用すると、オーサーインスタンス、パブリッシュインスタンス、プレビューインスタンスからオンプレミスのインフラストラクチャまたはデータセンターに接続できます。 これは、例えば、データベースへの安全なアクセスに役立ちます。 また、VPN をサポートする CRM ベンダーや、企業ネットワークからAEMas a Cloud Serviceの作成者、プレビュー、パブリッシュインスタンスに接続する CRM ベンダーなど、SaaS ベンダーへの接続も可能です。

IPSec 技術を搭載したほとんどの VPN デバイスがサポートされています。詳しくは、 **RouteBased 設定手順** 列 [このデバイスのリスト。](https://docs.microsoft.com/ja-jp/azure/vpn-gateway/vpn-gateway-about-vpn-devices#devicetable) 表の説明に従って、デバイスを設定します。

>[!NOTE]
>
>VPN インフラストラクチャに対する次の制限事項に注意してください。
>
>* サポートは 1 つの VPN 接続に制限されています。
>* Splunk 転送機能は VPN 接続では使用できません。
>* プライベートホスト名を解決するには、DNS リゾルバをゲートウェイアドレス空間にリストする必要があります。

### UI 設定 {#configuring-vpn-ui}

1. [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) で Cloud Manager にログインし、適切な組織を選択します。

1. 次の日： **[マイプログラム](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/editing-programs.md#my-programs)** 画面で、プログラムを選択します。

1. 次から： **プログラムの概要** ページで、 **環境** 「 」タブで「 」を選択します。 **ネットワークインフラストラクチャ** をクリックします。

   ![ネットワークインフラストラクチャの追加](assets/advanced-networking-ui-network-infrastructure.png)

1. Adobe Analytics の **ネットワークインフラストラクチャの追加** ウィザードを開始し、「 」を選択します。 **仮想プライベートネットワーク** をタップまたはクリックする前に、必要な情報を入力します。 **続行**.

   * **地域**  — インフラストラクチャを作成する必要がある地域です。
   * **アドレス空間**  — アドレス空間は、顧客空間の IP 範囲の 1/26 CIDR（64 IP アドレス）以上にする必要があります。
      * この値は後から変更できません。
   * **DNS 情報**  — これはリモート DNS リゾルバのリストです。
      * 押す `Enter` DNS サーバーアドレスを入力して別のアドレスを追加した後。
      * をタップまたはクリックします。 `X` 削除するアドレスの後に。
   * **共有キー**  — これは VPN の事前共有キーです。
      * 選択 **共有キーを表示** をクリックして、値を再確認するためのキーを表示します。

   ![vpn の設定](assets/advanced-networking-ui-vpn.png)

1. 次の日： **接続** ウィザードの「 」タブで、 **接続名** VPN 接続を識別するには、をタップまたはクリックします。 **接続を追加**.

   ![接続を追加](assets/advanced-networking-ui-vpn-add-connection.png)

1. Adobe Analytics の **接続を追加** ダイアログで、VPN 接続を定義し、をタップまたはクリックします。 **保存**.

   * **接続名**  — これは、前の手順で指定した VPN 接続のわかりやすい名前で、ここで更新できます。
   * **住所**  — これは VPN デバイスの IP アドレスです。
   * **アドレス空間** - VPN 経由でルーティングする IP アドレス範囲です。
      * 押す `Enter` 範囲を入力して別の範囲を追加した後。
      * をタップまたはクリックします。 `X` 範囲の後に削除します。
   * **IP セキュリティポリシー**  — 必要に応じてデフォルト値から調整

   ![VPN 接続の追加](assets/advanced-networking-ui-vpn-adding-connection.png)

1. ダイアログが閉じ、 **接続** 」タブをクリックします。 「**続行**」をタップまたはクリックします。

   ![VPN 接続が追加されます](assets/advanced-networking-ui-vpn-connection-added.png)

1. The **確認** 「 」タブに、選択内容と次の手順の概要が表示されます。 タップまたはクリック **保存** インフラストラクチャを作成する。

   ![フレキシブルポートエグレスの設定の確認](assets/advanced-networking-ui-vpn-confirm.png)

新しいレコードが **ネットワークインフラストラクチャ** サイドパネルの見出し（インフラストラクチャのタイプ、ステータス、地域、有効にされた環境の詳細を含む）。

### API 設定 {#configuring-vpn-api}

プログラムごとに 1 回、POST `/program/<programId>/networkInfrastructures` エンドポイントが呼び出され、次の値を含む設定情報のペイロードを渡します。 **vpn** （の） `kind` パラメーター、地域、アドレス空間（CIDR のリスト — 後で変更することはできません）、DNS リゾルバー（顧客のネットワーク内の名前を解決するため）、VPN 接続情報（ゲートウェイ設定、共有 VPN キー、IP セキュリティポリシーなど）。 エンドポイントは、 `network_id`、およびステータスを含むその他の情報。

この呼び出しの後、ネットワークインフラストラクチャがプロビジョニングされるまで、通常は 45～60 分かかります。API の GET メソッドを呼び出して、現在のステータスを返すことができます。このステータスは、最終的に `creating` から `ready` に変わります。すべてのステータスについては、 API ドキュメントを参照してください。

>[!TIP]
>
>パラメーターの完全なセット、正確な構文、および後で変更できないパラメーターなどの重要な情報。 [は API ドキュメントで参照できます。](https://developer.adobe.com/experience-cloud/cloud-manager/reference/api/#operation/createNetworkInfrastructure)

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
    <td><code>10.0.0.1:443</code><br>ホスト名を指定することもできます。</td>
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
    <td><code>10.0.0.1:3306</code><br>ホスト名を指定することもできます。</td>
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

### 設定に役立つドメイン {#vpn-useful-domains-for-configuration}

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
    <td><code>p{PROGRAM_ID}.{REGION}-gateway.external.adobeaemcloud.com</code></td>
    <td>該当なし</td>
    <td>AEM 側の VPN ゲートウェイの IP。顧客のネットワークエンジニアリングチームでは、これを使用して、特定の IP アドレスから VPN ゲートウェイへの VPN 接続のみを許可することができます。 </td>
  </tr>
  <tr>
    <td><code>p{PROGRAM_ID}.{REGION}.inner.adobeaemcloud.net</code></td>
    <td>VPN の AEM 側から顧客側に送信されるトラフィックの IP。これを顧客の設定で許可リストに登録して、AEM からのみ接続できるようにすることが可能です。</td>
    <td>AEM への VPN アクセスを許可する場合は、CNAME DNS エントリを設定して、これにカスタムドメインや <code>author-p{PROGRAM_ID}-e{ENVIRONMENT_ID}.adobeaemcloud.com</code> や <code>publish-p{PROGRAM_ID}-e{ENVIRONMENT_ID}.adobeaemcloud.com</code> をマッピングする必要があります。</td>
  </tr>
</tbody>
</table>

### VPN をイングレス接続に限定する方法 {#restrict-vpn-to-ingress-connections}

AEM への VPN アクセスのみを許可する場合は、`p{PROGRAM_ID}.external.adobeaemcloud.com` で定義された IP のみが環境と通信できるように、環境の許可リストを Cloud Manager で設定します。これは、Cloud Manager で他の IP ベースの許可リストと同じように行うことができます。

パスベースのルールにする必要がある場合は、標準の http ディレクティブを Dispatcher レベルで使用して、特定の IP を拒否または許可します。リクエストが常にオリジンに到達するように、目的のパスを CDN でキャッシュできないようにする必要もあります。

#### Httpd 設定の例 {#httpd-example}

```
Order deny,allow
Deny from all
Allow from 192.168.0.1
Header always set Cache-Control private
```

## 環境での高度なネットワーク構成の有効化 {#enabling}

プログラムの高度なネットワークオプションを設定したら、 [柔軟なポートエグレス](#flexible-port-egress) [出力専用 IP アドレス](#dedicated-egress-ip-address) または [VPN](#vpn) 使用するには、環境レベルで有効にする必要があります。

環境の高度なネットワーク設定を有効にすると、オプションのポート転送と非プロキシホストを有効にできます。 柔軟性を持たせるために、パラメーターは環境ごとに設定できます。

* **ポート転送**  — ポート転送規則は、80/443以外の宛先ポートに対して宣言する必要がありますが、http または https プロトコルを使用しない場合にのみ宣言します。
   * ポート転送規則は、宛先ホスト（名前または IP、ポート）のセットを指定することで定義されます。
   * HTTP/HTTPS 経由のポート80/443を使用するクライアント接続では、接続でプロキシ設定を使用して、高度なネットワークのプロパティを接続に適用する必要があります。
   * 宛先ホストごとに、宛先ポートを 30000～30999 のポートにマッピングする必要があります。
   * ポート転送規則は、すべての高度なネットワークタイプで使用できます。

* **非プロキシホスト**  — 非プロキシホストでは、専用 IP ではなく、共有 IP アドレス範囲を経由してルーティングするホストのセットを宣言できます。
   * 共有 IP を介したトラフィックのエグレス化をさらに最適化できるので、これは便利です。
   * 非プロキシホストは、専用の出力 IP アドレスと VPN の詳細ネットワークタイプに対してのみ使用できます。

>[!NOTE]
>
>環境が **更新中** ステータス。

### UI の使用の有効化 {#enabling-ui}

1. [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) で Cloud Manager にログインし、適切な組織を選択します。

1. 次の日： **[マイプログラム](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/editing-programs.md#my-programs)** 画面で、プログラムを選択します。

1. 次から： **プログラムの概要** ページで、 **環境** 」タブをクリックし、「 **環境** 見出しを左側のパネルに表示します。 次に、 **高度なネットワーク設定** 選択した環境の「 」タブをタップまたはクリックし、 **ネットワークインフラストラクチャの有効化**.

   ![高度なネットワークを有効にする環境を選択しています](assets/advanced-networking-ui-enable-environments.png)

1. The **高度なネットワークの構成** ダイアログが開きます。

1. 次の日： **非プロキシホスト** 専用の出力 IP アドレスと VPN に対して、オプションでホストのセットを定義できます。このホストは、専用 IP ではなく、共有 IP アドレスの範囲を通じてルーティングされる必要があります。 **非プロキシホスト** フィールドとタップまたはクリック **追加**.

   * ホストが「 」タブのホストのリストに追加されます。
   * 複数のホストを追加するには、この手順を繰り返します。
   * ホストを削除するには、行の右側の「 X 」をタップまたはクリックします。
   * このタブは、柔軟なポートエグレス設定には使用できません。

   ![非プロキシホストの追加](assets/advanced-networking-ui-enable-non-proxy-hosts.png)

1. 次の日： **ポート転送数** 「 」タブでは、HTTP または HTTPS を使用しない場合、80/443以外の任意の宛先ポートに対してポート転送規則を任意で定義できます。 次を提供： **名前**, **ポートオリグ**、および **ポートの宛先** をタップまたはクリックします。 **追加**.

   * ルールが「 」タブのルールのリストに追加されます。
   * 複数のルールを追加するには、この手順を繰り返します。
   * ルールを削除するには、行の右側にある X をタップまたはクリックします。

   ![オプションのポート転送の定義](assets/advanced-networking-ui-port-forwards.png)

1. タップまたはクリック **保存** 環境に設定を適用するためのダイアログ。

詳細なネットワーク構成が、選択した環境に適用されます。 次に戻る **環境** 「 」タブには、選択した環境に適用された設定とそのステータスの詳細が表示されます。

![高度なネットワークで構成された環境](assets/advanced-networking-ui-configured-environment.png)

### API の使用を有効にする {#enabling-api}

環境の高度なネットワーク構成を有効にするには、 `PUT /program/<program_id>/environment/<environment_id>/advancedNetworking` エンドポイントは、環境ごとに呼び出す必要があります。

API が数秒以内に応答して「`updating`」のステータスを返し、約 10 分後に、Cloud Manager の環境 GET エンドポイントの呼び出しで「`ready`」のステータスが返されます。これは、環境のアップデートが適用されたことを示します。

環境ごとにポート転送ルールを更新するには、 `PUT /program/{programId}/environment/{environmentId}/advancedNetworking` エンドポイントに含まれ、サブセットではなく設定パラメーターの完全なセットが含まれます。

専用の出力 IP アドレスと VPN の高度なネットワークタイプは、 `nonProxyHosts` パラメーター。 これにより、専用 IP ではなく共有 IP アドレス範囲を経由してルーティングするホストのセットを宣言できます。 `nonProxyHost` URL は `example.com` または `*.example.com` のパターンに従う場合があります（このパターンでは、ワイルドカードはドメインの先頭でのみ使用できます）。

環境のトラフィックルーティングルール（ホストまたはバイパス）がない場合でも、空のペイロードを渡して `PUT /program/<program_id>/environment/<environment_id>/advancedNetworking` を呼び出す必要があります。

>[!TIP]
>
>パラメーターの完全なセット、正確な構文、および後で変更できないパラメーターなどの重要な情報。 [は API ドキュメントで参照できます。](https://developer.adobe.com/experience-cloud/cloud-manager/reference/api/#operation/createNetworkInfrastructure)

## 環境での高度なネットワーク構成の編集と削除 {#editing-deleting-environments}

後 [環境に対する高度なネットワーク設定の有効化](#enabling) これらの設定の詳細を更新したり、削除したりできます。

>[!NOTE]
>
>ステータスが「 」の場合、ネットワークインフラストラクチャは編集できません **作成中**, **更新中**&#x200B;または **削除中**.

### UI を使用した編集または削除 {#editing-ui}

1. [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) で Cloud Manager にログインし、適切な組織を選択します。

1. 次の日： **[マイプログラム](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/editing-programs.md#my-programs)** 画面で、プログラムを選択します。

1. 次から： **プログラムの概要** ページで、 **環境** 」タブをクリックし、「 **環境** 見出しを左側のパネルに表示します。 次に、 **高度なネットワーク設定** 選択した環境の「 」タブに移動し、省略記号ボタンをタップまたはクリックします。

   ![プログラムレベルでの高度なネットワークの編集または削除の選択](assets/advanced-networking-ui-edit-delete.png)

1. 省略記号メニューで、 **編集** または **削除**.

   * 次を選択した場合： **編集**&#x200B;で、前の節で説明した手順に従って情報を更新します。 [UI の使用の有効化，](#enabling-ui) をタップまたはクリックします。 **保存**.
   * 次を選択した場合： **削除**」をクリックし、 **ネットワーク設定を削除** ～との対話 **削除** または中止 **キャンセル**.

変更は、 **環境** タブをクリックします。

### API を使用した編集または削除 {#editing-api}

特定の環境の高度なネットワークを削除するには、を呼び出します。 `DELETE [/program/{programId}/environment/{environmentId}/advancedNetworking]()`.

>[!TIP]
>
>パラメーターの完全なセット、正確な構文、および後で変更できないパラメーターなどの重要な情報。 [は API ドキュメントで参照できます。](https://developer.adobe.com/experience-cloud/cloud-manager/reference/api/#operation/createNetworkInfrastructure)

## プログラムのネットワークインフラストラクチャの編集と削除 {#editing-deleting-program}

プログラムに対してネットワークインフラストラクチャを作成した後は、限られたプロパティのみを編集できます。 不要になった場合は、プログラム全体の高度なネットワークインフラストラクチャを削除できます。

>[!NOTE]
>
>ネットワークインフラストラクチャの編集と削除に関する次の制限事項に注意してください。
>
>* 削除では、すべての環境の高度なネットワークが無効になっている場合にのみ、インフラストラクチャが削除されます。
>* ステータスが「 」の場合、ネットワークインフラストラクチャは編集できません **作成中**, **更新中**&#x200B;または **削除中**.
>* 作成後は、VPN の高度なネットワークインフラストラクチャタイプのみを編集でき、その後は限られたフィールドのみを編集できます。
>* セキュリティ上の理由から、 **共有キー** キー自体を編集していない場合でも、VPN の高度なネットワークインフラストラクチャを編集する際には、必ず指定する必要があります。

### UI を使用した編集と削除 {#delete-ui}

1. Cloud Manager( ) にログインします。 [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) 適切な組織を選択します。

1. 次の日： **[マイプログラム](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/editing-programs.md#my-programs)** 画面で、プログラムを選択します。

1. 次から： **プログラムの概要** ページで、 **環境** 「 」タブで「 」を選択します。 **ネットワークインフラストラクチャ** 見出しを左側のパネルに表示します。 次に、削除するインフラストラクチャの横にある省略記号ボタンをタップまたはクリックします。

   ![プログラムレベルでの高度なネットワークの編集または削除の選択](assets/advanced-networking-ui-delete-infrastructure.png)

1. 省略記号メニューで、 **編集** または **削除**.

1. 次を選択した場合： **編集**、 **ネットワークインフラストラクチャの編集** ウィザードが開きます。 必要に応じて、インフラストラクチャを作成する際に説明した手順に従って編集します。

1. 次を選択した場合： **削除**」をクリックし、 **ネットワーク設定を削除** ～との対話 **削除** または中止 **キャンセル**.

変更は、 **環境** タブをクリックします。

### API を使用した編集と削除 {#delete-api}

プログラムのネットワークインフラストラクチャを&#x200B;**削除**&#x200B;するには、`DELETE /program/{program ID}/networkinfrastructure/{networkinfrastructureID}`.を呼び出します。

## プログラムの高度なネットワークインフラストラクチャタイプの変更 {#changing-program}

プログラムに対して一度に 1 種類の高度なネットワークインフラストラクチャを設定できるのは、フレキシブルポートエグレス、専用エグレス IP アドレス、VPN のいずれかのみです。

既に構成したものとは異なる、別の高度なネットワークインフラストラクチャタイプが必要と判断した場合は、既存のインフラストラクチャを削除し、新しく作成する必要があります。 次の手順に従います。

1. [すべての環境で高度なネットワークを削除します。](#editing-deleting-environments)
1. [高度なネットワークインフラストラクチャを削除します。](#editing-deleting-program)
1. 必要な高度なネットワークインフラストラクチャタイプを作成します。 [柔軟なポートエグレス](#flexible-port-egress) [出力専用 IP アドレス](#dedicated-egress-ip-address) または [VPN。](#vpn)
1. [環境レベルで高度なネットワークを再度有効にします。](#enabling)

>[!WARNING]
>
> この手順を実行すると、削除と再作成の間に高度なネットワークサービスのダウンタイムが発生します
> ダウンタイムがビジネスに大きな影響を与える場合は、カスタマーサポートにお問い合わせください。既に作成された内容と変更の理由を説明します。

## 追加の公開地域の詳細なネットワーク設定 {#advanced-networking-configuration-for-additional-publish-regions}

高度なネットワークが既に設定されている環境にさらに地域が追加されると、高度なネットワークルールに一致する追加の公開地域からのトラフィックは、デフォルトでプライマリ地域を経由します。ただし、プライマリ地域が使用できなくなった場合、その他の地域で詳細ネットワークが有効になっていないと、高度なネットワークトラフィックは破棄されます。いずれかの地域で障害が発生した場合に、待ち時間を最適化して可用性を高めるには、追加の公開地域の高度なネットワークを有効にする必要があります。次の節では、2 つの異なるシナリオについて説明します。

>[!NOTE]
>
>すべての地域が同じ[環境の高度なネットワーク設定](https://developer.adobe.com/experience-cloud/cloud-manager/reference/api/#tag/Environment-Advanced-Networking-Configuration)を共有するので、トラフィックが出てくる地域に基づいて、別の宛先にトラフィックを送ることはできません。

### 専用エグレス IP アドレス {#additional-publish-regions-dedicated-egress}

#### プライマリ地域で既に有効になっている高度なネットワーク {#already-enabled}

プライマリ地域で既に高度なネットワーク設定が有効になっている場合は、次の手順に従います。

1. 専用の AEM IP アドレスが許可リストに表示されるようにインフラストラクチャをロックダウンした場合は、そのインフラストラクチャ内の拒否ルールを一時的に無効にすることをお勧めします。これが行われない場合、新しい地域の IP アドレスからのリクエストが、使用するインフラストラクチャによって拒否される短い期間があります。すべての AEM 地域は同じ完全修飾ドメイン名（FQDN）からの高度なネットワークトラフィックを引き出すので、FQDN を介してインフラストラクチャをロックダウンしている場合（例えば、`p1234.external.adobeaemcloud.com`）、これは必要ありません
1. 高度なネットワークのドキュメントに記載されるように、Cloud Manager Create Network Infrastructure API への POST 呼び出しを通じて、セカンダリ地域のプログラム範囲のネットワークインフラストラクチャを作成します。ペイロードの JSON 設定のプライマリ地域に対する唯一の違いは、地域プロパティです
1. AEM トラフィックを許可するために、インフラストラクチャを IP でロックダウンする必要がある場合は、`p1234.external.adobeaemcloud.com` に一致する IP を追加します。地域ごとに 1 つ必要です。

#### どの地域にもまだ設定されていない高度なネットワーク {#not-yet-configured}

手順は、前述の手順とほとんど同じです。ただし、実稼動環境でまだ高度なネットワークが有効にされていない場合は、まずステージング環境で有効にして設定をテストできます。

1. [Cloud Manager Create Network Infrastructure API](https://developer.adobe.com/experience-cloud/cloud-manager/reference/api/#tag/Network-infrastructure/operation/createNetworkInfrastructure) への POST 呼び出しを通して、すべての地域のネットワークインフラストラクチャを作成します。ペイロードの JSON 設定のプライマリ地域に対する唯一の違いは、地域プロパティです。
1. ステージング環境の場合は、`PUT api/program/{programId}/environment/{environmentId}/advancedNetworking` を実行して、環境範囲を指定した高度なネットワークを有効にし、設定します。詳しくは、[こちら](https://developer.adobe.com/experience-cloud/cloud-manager/reference/api/#tag/Environment-Advanced-Networking-Configuration/operation/enableEnvironmentAdvancedNetworkingConfiguration)の API ドキュメントを参照してください。
1. 必要に応じて、できれば FQDN（例えば `p1234.external.adobeaemcloud.com`）で、外部インフラストラクチャをロックダウンします。それ以外の場合は、IP アドレスで行うことができます
1. ステージング環境が期待どおりに動作する場合は、実稼動環境用に環境範囲を定めた高度なネットワーク設定を有効にして設定します。

#### VPN {#vpn-regions}

手順は、専用のエグレス IP アドレスの手順とほとんど同じです。唯一の違いは、プライマリ地域とは異なる設定で地域プロパティが設定される点に加えて、「`connections.gateway`」フィールドは、オプションで組織が運用する別の VPN エンドポイント（地理的に新しい地域に近い場合もあります）にルーティングするように設定できます。
