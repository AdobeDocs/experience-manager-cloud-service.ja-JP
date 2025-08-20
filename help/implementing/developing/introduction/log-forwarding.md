---
title: AEM as a Cloud Serviceのログ転送
description: AEM as a Cloud Serviceでのログのベンダーへの転送について説明します
exl-id: 27cdf2e7-192d-4cb2-be7f-8991a72f606d
feature: Developing
role: Admin, Architect, Developer
source-git-commit: 2e136117508d7bd17993bf0e64b41aa860d71ab1
workflow-type: tm+mt
source-wordcount: '2409'
ht-degree: 5%

---

# ログ転送 {#log-forwarding}

>[!NOTE]
>
>ログ転送は、従来の方法ではAdobe サポートチケットの送信が必要でしたが、セルフサービス方式で設定されるようになりました。 ログ転送がAdobeによって設定されている場合は、[ 移行 ](#legacy-migration) の節を参照してください。

ログベンダーのライセンスを持つお客様、またはログ製品をホストするお客様は、AEM ログ（Apache/Dispatcherを含む）および CDN ログを、関連するログ出力先に転送することができます。 AEM as a Cloud Serviceは、次のログ出力先をサポートしています。

<table>
  <tbody>
    <tr>
      <th>ログ技術</th>
      <th>Private Beta*</th>
      <th>AEM</th>
      <th>Dispatcher</th>
      <th>CDN</th>
    </tr>
    <tr>
      <td>Amazon S3</td>
      <td style="background-color: #ffb3b3;">はい</td>
      <td>はい</td>
      <td>はい</td>
      <td style="background-color: #ffb3b3;">いいえ</td>
    </tr>
    <tr>
      <td>Azure Blob Storage</td>
      <td>いいえ</td>
      <td>はい</td>
      <td>はい</td>
      <td>はい</td>
    </tr>
    <tr>
      <td>DataDog</td>
      <td>いいえ</td>
      <td>はい</td>
      <td>はい</td>
      <td>はい</td>
    </tr>
    <tr>
      <td>Dynatrace</td>
      <td style="background-color: #ffb3b3;">はい</td>
      <td>はい</td>
      <td>はい</td>
      <td style="background-color: #ffb3b3;">いいえ</td>
    </tr>
    <tr>
      <td>Elasticsearch<br>OpenSearch</td>
      <td>いいえ</td>
      <td>はい</td>
      <td>はい</td>
      <td>はい</td>
    </tr>
    <tr>
      <td>HTTPS</td>
      <td>いいえ</td>
      <td>はい</td>
      <td>はい</td>
      <td>はい</td>
    </tr>
    <tr>
      <td>New Relic</td>
      <td style="background-color: #ffb3b3;">はい</td>
      <td>はい</td>
      <td>はい</td>
      <td style="background-color: #ffb3b3;">いいえ</td>
    </tr>
    <tr>
      <td>Splunk</td>
      <td>いいえ</td>
      <td>はい</td>
      <td>はい</td>
      <td>はい</td>
    </tr>
    <tr>
      <td>相撲論理</td>
      <td style="background-color: #ffb3b3;">はい</td>
      <td>はい</td>
      <td>はい</td>
      <td style="background-color: #ffb3b3;">いいえ</td>
    </tr>
  </tbody>
</table>

>[!NOTE]
>
> Private Betaのテクノロジーについては、[aemcs-logforwarding-beta@adobe.com](mailto:aemcs-logforwarding-beta@adobe.com) にメールを送信してアクセスをリクエストしてください。

ログ転送は、Git で設定を宣言することでセルフサービス方式で設定され、Cloud Manager設定パイプラインを介して開発環境、ステージング環境、実稼動環境の各タイプにデプロイできます。 設定ファイルは、コマンドラインツールを使用して迅速な開発環境（RDE）にデプロイできます。

AEMと Apache/DispatcherAEMのログを、専用のエグレス IP などの高度なネットワークインフラストラクチャを介してルーティングするオプションがあります。

ログの宛先に送信されたログに関連付けられているネットワーク帯域幅は、組織のネットワーク I/O 使用の一部と見なされることに注意してください。

## この記事の編成方法 {#how-organized}

この記事は、次のように構成されています。

* 設定 – すべてのログ宛先に共通
* トランスポートと高度なネットワーク – ログ設定を作成する前に、ネットワーク設定を考慮する必要があります
* 宛先設定のログ記録 – 各宛先の形式は若干異なります
* ログエントリ形式 – ログエントリ形式に関する情報
* 従来のログ転送からの移行 – Adobeで以前設定したログ転送からセルフサービスアプローチに移行する方法

## 設定 {#setup}

1. `logForwarding.yaml` という名前のファイルを作成します。[ 設定パイプライン ](/help/operations/config-pipeline.md#common-syntax) の記事（**kind** は `LogForwarding` に、バージョンは「1」に設定する必要があります）で説明しているように、次のような設定でメタデータが含まれている必要があります（例として Splunk を使用）。

   ```yaml
   kind: "LogForwarding"
   version: "1"
   metadata:
     envTypes: ["dev"]
   data:
     splunk:
       default:
         enabled: true
         host: "splunk-host.example.com"
         token: "${{SPLUNK_TOKEN}}"
         index: "AEMaaCS"
   ```

1. [設定パイプラインの使用](/help/operations/config-pipeline.md#folder-structure)で説明されているように、*config* または類似の名前の最上位フォルダーの下のどこかにファイルを配置します。

1. コマンドラインツールを使用する RDE 以外の環境タイプの場合は、[ この節 ](/help/operations/config-pipeline.md#creating-and-managing) で参照されているように、Cloud Managerでターゲット設定パイプラインを作成します。フルスタックパイプラインと web 階層設定パイプラインでは設定ファイルをデプロイしません。

1. 設定をデプロイします。

設定内のトークン（`${{SPLUNK_TOKEN}}` など）は秘密鍵を表しているので、Git に保存しないでください。 代わりに、Cloud Manager[ シークレット環境変数 ](/help/operations/config-pipeline.md#secret-env-vars) として宣言します。 ログをオーサー層、パブリッシュ層およびプレビュー層に転送できるように、「適用されるサービス」フィールドのドロップダウン値として **すべて** を必ず選択してください。

**default** ブロックの後に追加の **cdn** や **aem** ブロックを含めることで、CDN ログとAEM ログ（Apache/Dispatcherを含む）に異なる値を設定できます。このブロックでは、プロパティを **default** ブロックで定義された値より優先できます。必要なのは enabled プロパティのみです。 以下の例に示すように、CDN ログに別の Splunk インデックスを使用する使用例が考えられます。

```yaml
   kind: "LogForwarding"
   version: "1"
   metadata:
     envTypes: ["dev"]
   data:
     splunk:
       default:
         enabled: true
         host: "splunk-host.example.com"
         token: "${{SPLUNK_TOKEN}}"
         index: "AEMaaCS"
       cdn:
         enabled: true
         token: "${{SPLUNK_TOKEN_CDN}}"
         index: "AEMaaCS_CDN"   
```

別のシナリオとして、CDN ログまたはAEM ログ（Apache/Dispatcherを含む）の転送を無効にする場合もあります。 例えば、CDN ログのみを転送するには、次を設定します。

```yaml
   kind: "LogForwarding"
   version: "1"
   metadata:
     envTypes: ["dev"]
   data:
     splunk:
       default:
         enabled: true
         host: "splunk-host.example.com"
         token: "${{SPLUNK_TOKEN}}"
         index: "AEMaaCS"
       aem:
         enabled: false
```

## トランスポートと高度なネットワーク {#transport-advancednetworking}

一部の組織は、ログ宛先で受信できるトラフィックを制限し、他の組織は HTTPS （443）以外のポートを使用する必要がある場合があります。  その場合は、ログ転送設定をデプロイする前に [ 詳細ネットワーク ](/help/security/configuring-advanced-networking.md) を設定する必要があります。

次の表を使用して、ポート 443 を使用しているかどうか、および固定 IP アドレスからログを表示する必要があるかどうかに基づいて、高度なネットワーク設定とログ設定の要件を確認してください。

<table>
  <tbody>
    <tr>
      <th>宛先ポート</th>
      <th>固定 IP からログを表示するための要件</th>
      <th>高度なネットワークが必要</th>
      <th>LogForwarding.yaml ポート定義が必要です</th>
    </tr>
    <tr>
      <td rowspan="2" ro>HTTPS （443）</td>
      <td>いいえ</td>
      <td>いいえ</td>
      <td>いいえ</td>
    </tr>
    <tr>
      <td>はい</td>
      <td>対応 <a href="/help/security/configuring-advanced-networking.md#dedicated-egress-ip-address-dedicated-egress-ip-address"> 専用エグレス </a></td>
      <td>いいえ</td>
    <tr>
    <tr>
      <td rowspan="2">非標準ポート （例：8088）</td>
      <td>いいえ</td>
      <td>対応 <a href="/help/security/configuring-advanced-networking.md#flexible-port-egress-flexible-port-egress"> 柔軟なエグレス </a></td>
      <td>はい</td>
    </tr>
    <tr>
      <td>はい</td>
      <td>対応 <a href="/help/security/configuring-advanced-networking.md#dedicated-egress-ip-address-dedicated-egress-ip-address"> 専用エグレス </a></td>
      <td>はい</td>
  </tbody>
</table>

>[!NOTE]
>ログが 1 つの IP アドレスから表示されるかどうかは、高度なネットワーク設定の選択によって決まります。  これを容易にするには、専用のエグレスを使用する必要があります。
>
> 高度なネットワーク設定は [2 段階のプロセス ](/help/security/configuring-advanced-networking.md#configuring-and-enabling-advanced-networking-configuring-enabling) で、プログラムおよび環境レベルでイネーブルメントを行う必要があります。

AEM ログ（Apache/Dispatcherを含む）の場合、[ 高度なネットワーク ](/help/security/configuring-advanced-networking.md) を設定している場合は、`aem.advancedNetworking` プロパティを使用して、専用のエグレス IP アドレスから、または VPN 経由で転送できます。

次の例は、高度なネットワークを使用して標準の HTTPS ポートに対してログを設定する方法を示しています。

```yaml
kind: "LogForwarding"
version: "1"
metadata:
  envTypes: ["dev"]
data:
  splunk:
    default:
      enabled: true
      host: "splunk-host.example.com"
      port: 443
      token: "${{SPLUNK_TOKEN}}"
      index: "aemaacs"
    aem:
      advancedNetworking: true
```

CDN ログの場合は、[Fastly ドキュメント – 公開 IP リスト ](https://www.fastly.com/documentation/reference/api/utils/public-ip-list/) で説明しているように、IP アドレスを許可リストに登録できます。 その共有 IP アドレスのリストが大きすぎる場合は、https サーバーまたは（Adobe以外の） Azure Blob Store にトラフィックを送信し、そこで既知の IP から最終的な宛先にログを送信するロジックを記述することを検討します。

>[!NOTE]
>
>CDN ログが、AEM Cloud Service ではなく Fastly から直接送信されることが原因で、AEM ログと同じ IP アドレスから表示することはできません。

## 宛先設定のログ記録 {#logging-destinations}

サポートされるログの宛先の設定を、具体的な考慮事項と共に以下に示します。

### Amazon S3 {#amazons3}

Amazon S3 へのログ転送では、AEMとDispatcherのログがサポートされていますが、CDN ログはまだサポートされていません。

>[!NOTE]
>
>S3 に定期的に書き込まれるログ。ログ ファイルの種類ごとに 10 分ごとに書き込まれます。  これにより、機能を切り替えると、ログが S3 に書き込まれるまでの初期遅延が発生する可能性があります。  [ この動作に関する詳細情報 ](https://docs.fluentbit.io/manual/pipeline/outputs/s3#differences-between-s3-and-other-fluent-bit-outputs)。

```yaml
kind: "LogForwarding"
version: "1.0"
metadata:
  envTypes: ["dev"]
data:
  awsS3:
    default:
      enabled: true
      region: "your-bucket-region"
      bucket: "your_bucket_name"
      accessKey: "${{AWS_S3_ACCESS_KEY}}"
      secretAccessKey: "${{AWS_S3_SECRET_ACCESS_KEY}}"
```

S3 ログフォワーダーを使用するには、AWS IAM ユーザーに S3 バケットにアクセスするための適切なポリシーを事前設定する必要があります。  IAM ユーザー資格情報の作成方法については、[AWS IAM ユーザードキュメント ](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_credentials_access-keys.html) を参照してください。

IAM ポリシーでは、ユーザーが `s3:putObject` を使用できるようにする必要があります。  例：

```json
 {
    "Version": "2012-10-17",
    "Statement": [{
        "Effect": "Allow",
        "Action": [
            "s3:PutObject"
        ],
        "Resource": "arn:aws:s3:::your_bucket_name/*"
    }]
}
```

実装方法について詳しくは、[AWS バケットポリシーのドキュメント ](https://docs.aws.amazon.com/AmazonS3/latest/userguide/bucket-policies.html) を参照してください。

### Azure Blob Storage {#azureblob}

```yaml
kind: "LogForwarding"
version: "1"
metadata:
  envTypes: ["dev"]
data:
  azureBlob:
    default:
      enabled: true       
      storageAccountName: "example_acc"
      container: "aem_logs"
      sasToken: "${{AZURE_BLOB_SAS_TOKEN}}
      
```

認証には SAS トークンを使用する必要があります。 共有アクセストークンページではなく、共有アクセス署名ページから作成し、次の設定で設定する必要があります。

* 許可されたサービス : BLOB を選択する必要があります。
* 許可されたリソース：オブジェクトを選択する必要があります。
* 許可された権限：書き込み、追加、作成を選択する必要があります。
* 有効な開始日と有効期限。

サンプルの SAS トークン設定のスクリーンショットを次に示します。

![Azure Blob SAS トークン設定 ](/help/implementing/developing/introduction/assets/azureblob-sas-token-config.png)

以前に正しく機能していた後にログの配信が停止した場合は、設定した SAS トークンが期限切れの可能性があるので、まだ有効かどうかを確認します。

#### Azure Blob Storage CDN ログ {#azureblob-cdn}

グローバルに分散された各ログサーバーは、`aemcdn` フォルダーの下で、数秒ごとに新しいファイルを生成します。 作成したファイルは、に追加されなくなります。 ファイル名の形式は YYYY-MM-DDThh:mm:ss.sss-uniqueid.log です。 例：2024-03-04T10:00:00.000-WnFWYN9BpOUs2aOVn4ee.log

例えば、ある時点で次のようになります。

```text
aemcdn/
   2024-03-04T10:00:00.000-abc.log
   2024-03-04T10:00:00.000-def.log
```

30 秒後には、

```text
aemcdn/
   2024-03-04T10:00:00.000-abc.log
   2024-03-04T10:00:00.000-def.log
   2024-03-04T10:00:30.000-ghi.log
   2024-03-04T10:00:30.000-jkl.log
   2024-03-04T10:00:30.000-mno.log
```

各ファイルには、それぞれ別の行に記述された複数の JSON ログエントリが含まれます。 ログエントリの形式については、[AEM as a Cloud Serviceのログ ](/help/implementing/developing/introduction/logging.md) を参照してください。各ログエントリには、以下の [ ログエントリの形式 ](#log-formats) の節で説明しているその他のプロパティも含まれています。

#### Azure Blob Storage AEM ログ {#azureblob-aem}

AEM ログ（Apache/Dispatcherを含む）は、次の命名規則でフォルダーの下に表示されます。

* aemaccess
* aemerror
* aemrequest
* aemdispatcher
* aemhttpdaccess
* aemhttpderror

各フォルダーに 1 つのファイルが作成され、に追加されます。 お客様は、このファイルが大きくなりすぎないよう、ファイルの処理と管理を行います。

[AEM as a Cloud Service のログ ](/help/implementing/developing/introduction/logging.md) のログエントリ形式を参照してください。 ログエントリには、以下の [ ログエントリの形式 ](#log-formats) の節で説明する追加のプロパティも含まれます。

### Datadog {#datadog}

```yaml
kind: "LogForwarding"
version: "1"
metadata:
  envTypes: ["dev"]
data:
  datadog:
    default:
      enabled: true       
      host: "http-intake.logs.datadoghq.eu"
      token: "${{DATADOG_API_KEY}}"
      tags:
         tag1: value1
         tag2: value2
      
```

#### 考慮事項

* 特定のクラウドプロバイダーとの統合を行わずに、API キーを作成します。
* タグプロパティはオプションです
* AEM ログの場合、Datadog ソース タグは `aemaccess`、`aemerror`、`aemrequest`、`aemdispatcher`、`aemhttpdaccess`、`aemhttpderror` のいずれかに設定されます
* CDN ログの場合、Datadog ソース タグは `aemcdn` に設定されます
* Datadog サービスタグは `adobeaemcloud` に設定されていますが、タグセクションで上書きできます
* 取り込みパイプラインで Datadog タグを使用してログを転送するための適切なインデックスを決定する場合は、ログ転送 YAML ファイルでこれらのタグが正しく設定されていることを確認します。 タグが見つからない場合、パイプラインがタグに依存していると、ログの取り込みに成功しない可能性があります。

### Elasticsearchと OpenSearch {#elastic}

```yaml
kind: "LogForwarding"
version: "1"
metadata:
  envTypes: ["dev"]
data:
  elasticsearch:
    default:
      enabled: true
      host: "example.com"
      user: "${{ELASTICSEARCH_USER}}"
      password: "${{ELASTICSEARCH_PASSWORD}}"
      pipeline: "ingest pipeline name"
```

#### 考慮事項

* デフォルトでは、ポートは 443 です。 オプションで、`port` というプロパティで上書きすることもできます
* 資格情報には、アカウントの資格情報ではなく、必ずデプロイメントの資格情報を使用します。 これらは、次の画像に似た画面で生成される資格情報です。

![Elastic デプロイメント資格情報 ](/help/implementing/developing/introduction/assets/ec-creds.png)

* AEM ログの場合、`index` は `aemaccess`、`aemerror`、`aemrequest`、`aemdispatcher`、`aemhttpdaccess` または `aemhttpderror` のいずれかに設定されます
* オプションのパイプラインプロパティは、Elasticsearchまたは OpenSearch 取り込みパイプラインの名前に設定する必要があります。この名前は、ログエントリを適切なインデックスにルーティングするように設定できます。 パイプラインのプロセッサタイプは *スクリプト* に設定し、スクリプト言語は *痛みなし* に設定する必要があります。 次に、ログエントリを aemaccess_dev_26_06_2024 などのインデックスにルーティングするスクリプトスニペットの例を示します。

```text
def envType = ctx.aem_env_type != null ? ctx.aem_env_type : 'unknown';
def sourceType = ctx._index;
def date = new SimpleDateFormat('dd_MM_yyyy').format(new Date());
ctx._index = sourceType + "_" + envType + "_" + date;
```

### HTTPS {#https}

```yaml
kind: "LogForwarding"
version: "1"
metadata:
  envTypes: ["dev"]
data:
  https:
    default:
      enabled: true
      url: "https://example.com/aem_logs/aem"
      authHeaderName: "X-AEMaaCS-Log-Forwarding-Token"
      authHeaderValue: "${{HTTPS_LOG_FORWARDING_TOKEN}}"
```

#### 考慮事項

* URL 文字列には **https://** を含める必要があります。含めない場合、検証が失敗します。
* URL にはポートを含めることができます。 例えば、`https://example.com:8443/aem_logs/aem` のようになります。 URL 文字列にポートが含まれていない場合、ポート 443 （デフォルトの HTTPS ポート）が想定されます。

#### HTTPS CDN ログ {#https-cdn}

Web リクエスト（POST）は、ログエントリの配列である json ペイロードを使用して継続的に送信されます。ログエントリの形式については、「[AEM as a Cloud Serviceのログ ](/help/implementing/developing/introduction/logging.md#cdn-log) を参照してください。 その他のプロパティについては、以下の「[ ログエントリの形式 ](#log-formats) の節で説明します。

また、`sourcetype` という名前のプロパティもあり、`aemcdn` という値に設定されています。

>[!NOTE]
>
> 最初の CDN ログエントリが送信される前に、HTTP サーバーは、1 回限りのチャレンジを正常に完了する必要があります。つまり、パスに送信され ``/.well-known/fastly/logging/challenge`` リクエストは、本文にアスタリスクの ``*`` と 200 個のステータスコードで応答する必要があります。

#### HTTPS AEM ログ {#https-aem}

AEM ログ（apache/dispatcher を含む）の場合、web リクエスト（POST）は、[AEM as a Cloud Serviceのログ ](/help/implementing/developing/introduction/logging.md) で説明されているように、様々なログエントリ形式でログエントリの配列である json ペイロードで継続的に送信されます。 その他のプロパティについては、以下の「[ ログエントリの形式 ](#log-formats) の節で説明します。

`Source-Type` という名前のプロパティもあり、次のいずれかの値に設定されます。

* aemaccess
* aemerror
* aemrequest
* aemdispatcher
* aemhttpdaccess
* aemhttpderror

### New Relic ログ API {#newrelic-https}

New Relicへのログ転送では、New Relic HTTPS API を取り込みに利用します。  現在は、AEMとDispatcherからのログのみをサポートしています。CDN ログはまだサポートされていません。

```yaml
  kind: "LogForwarding"
  version: "1"
  metadata:
    envTypes: ["dev"]
  data:
    newRelic:
      default:
        enabled: true
        uri: "https://log-api.newrelic.com/log/v1"
        apiKey: "${{NR_API_KEY}}"
```

>[!NOTE]
>
>New Relicへのログ転送は、顧客が所有するNew Relic アカウントでのみ使用できます。
>
>アクセスをリクエストするには、[aemcs-logforwarding-beta@adobe.com](mailto:aemcs-logforwarding-beta@adobe.com) にメールを送信します。
>
>New Relicは、New Relic アカウントがプロビジョニングされている場所に基づいて、地域固有のエンドポイントを提供します。  詳しくは、[New Relic ドキュメント ](https://docs.newrelic.com/docs/logs/log-api/introduction-log-api/#endpoint) を参照してください。

### Dynatrace ログ API {#dynatrace-https}

Dynatraceへのログ転送では、Dynatrace HTTPS API を取り込みに利用します。  現在は、AEMとDispatcherからのログのみをサポートしています。CDN ログはまだサポートされていません。

トークンには、「ログの取り込み」スコープ属性が必要です。

```yaml
  kind: "LogForwarding"
  version: "1"
  metadata:
    envTypes: ["dev"]
  data:
    dynatrace:
      default:
        enabled: true
        environmentId: "${{DYNATRACE_ENVID}}"
        token: "${{DYNATRACE_TOKEN}}"  
```

>[!NOTE]
>
> アクセスをリクエストするには、[aemcs-logforwarding-beta@adobe.com](mailto:aemcs-logforwarding-beta@adobe.com) にメールを送信します。

### Splunk {#splunk}

```yaml
kind: "LogForwarding"
version: "1"
metadata:
  envTypes: ["dev"]
data:
  splunk:
    default:
      enabled: true
      host: "splunk-host.example.com"
      token: "${{SPLUNK_TOKEN}}"
      index: "aemaacs"
```

#### 考慮事項

* デフォルトでは、ポートは 443 です。 オプションで、`port` という名前のプロパティで上書きできます。
* sourcetype フィールドには、特定のログに応じて、*aemaccess*、*aemerror* のいずれかの値が表示されます。
  *aemrequest*、*aemdispatcher*、*aemhttpdaccess*、*aemhttpderror*、*aemcdn*
* 必要な IP が許可リストに加えるされたにもかかわらずログが配信されない場合は、Splunk トークンの検証を強制するファイアウォールルールがないことを確認します。 無効な Splunk トークンが意図的に送信される最初の検証ステップを Fastly が実行します。 無効な Splunk トークンを使用して接続を終了するようにファイアウォールが設定されている場合、検証プロセスが失敗し、Fastly が Splunk インスタンスにログを配信できなくなります。

>[!NOTE]
>
> 従来のログ転送からこのセルフサービスモデルに [ 移行する場合 ](#legacy-migration)、Splunk インデックスに送信される `sourcetype` フィールドの値が変更された可能性があるので、それに応じて調整します。

### 相撲論理 {#sumologic}

Sumo Logic へのログ転送では、AEMとDispatcherのログがサポートされています。CDN ログはまだサポートされていません。

データ取得のために Sumo ロジックを設定すると、host、receiverURI、および private key を 1 つの文字列で提供する「HTTP Source アドレス」が表示されます。  例：

`https://collectors.de.sumologic.com/receiver/v1/http/ZaVnC...`

URL の最後のセクション（先頭の `/` を除く）をコピーし、それを前述の [ 設定 ](/help/operations/config-pipeline.md#secret-env-vars) の節で説明されているように [](#setup)CloudManager シークレット環境変数）として追加してから、設定でその変数を参照する必要があります。  以下に例を示します。

```yaml
kind: "LogForwarding"
version: "1"
metadata:
  envTypes: ["dev"]
data:
  sumoLogic:
    default:
      enabled: true
      collectorURL: "https://collectors.de.sumologic.com/receiver/v1/http"
      privateKey: "${{SUMOLOGIC_PRIVATE_KEY}}"
      index: "aem-logs"
```

>[!NOTE]
> 「インデックス」フィールド機能を利用するには、Sumo Logic Enterprise サブスクリプションが必要です。  エンタープライズ以外のサブスクリプションの場合、ログは標準として `sumologic_default` パーティションにルーティングされます。  詳しくは、[Sumo Logic Partitioning ドキュメント ](https://help.sumologic.com/docs/search/optimize-search-partitions/) を参照してください。

## ログエントリの形式 {#log-formats}

各ログタイプ（CDN ログおよびAEM as a Cloud Serviceを含むAEM ログ）の形式については、[Dispatcherのログ ](/help/implementing/developing/introduction/logging.md) を参照してください。

複数のプログラムおよび環境からのログは、ログ記事で説明されている出力に加えて、同じログ宛先に転送される場合があるので、次のプロパティが各ログエントリに含まれます。

* aem_env_id
* aem_env_type
* aem_program_id
* aem_tier

例えば、プロパティには次の値を含めることができます。

```text
aem_env_id: 1242
aem_env_type: dev
aem_program_id: 12314
aem_tier: author
```

## レガシーログ転送からの移行 {#legacy-migration}

セルフサービスモデルを通じてログ転送の設定を行う前は、お客様は、Adobeが統合を開始するサポートチケットを開くようリクエストされていました。

Adobeによってそのように設定されたお客様は、都合のよいときにセルフサービスモデルに適応していただければ幸いです。 この移行には、いくつかの理由があります。

* 新しい環境（新しい開発環境や RDE など）がプロビジョニングされた。
* 既存の Splunk エンドポイントまたは資格情報に対する変更。
* Adobeは、CDN ログが使用可能になる前にログ転送を設定しており、CDN ログを受け取りたいと考えています。
* 時間に敏感な変更が必要になる前であっても組織が知識を持つように、セルフサービスモデルに積極的に適応することを意識的に決定する。

移行の準備が整ったら、前の節で説明したように YAML ファイルを設定するだけです。 Cloud Manager設定パイプラインを使用して、設定を適用する必要がある各環境にデプロイします。

設定をすべての環境にデプロイして、すべての環境をセルフサービスで制御できるようにすることをお勧めしますが、必須ではありません。 そうしないと、Adobeで設定された環境と、セルフサービス方式で設定された環境を忘れてしまう可能性があります。

>[!NOTE]
>
>Splunk インデックスに送信された `sourcetype` フィールドの値が変更された可能性があるので、それに応じて調整します。
>
>Adobe サポートが以前に設定した環境にログ転送をデプロイすると、最大で数時間ログの重複が発生する場合があります。 これは最終的に自動解決されます。
