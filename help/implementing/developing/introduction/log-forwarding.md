---
title: AEM as a Cloud Service のログ転送
description: AEM as a Cloud Service でのログベンダーへのログ転送について説明します。
exl-id: 27cdf2e7-192d-4cb2-be7f-8991a72f606d
feature: Developing
role: Admin, Developer
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '2478'
ht-degree: 95%

---

# ログ転送 {#log-forwarding}

>[!NOTE]
>
>ログ転送は、アドビのサポートチケットの送信を必要とした従来の方法とは異なり、セルフサービス方式で設定されるようになりました。ログ転送がアドビで設定されている場合は、[移行](#legacy-migration)の節を参照してください。

ログベンダーのライセンスを所有しているお客様や、ログ製品をホストしているお客様は、AEM ログ（Apache／Dispatcher を含む）と CDN ログを関連するログの宛先に転送できます。AEM as a Cloud Service は、次のログの宛先をサポートしています。

<table>
  <tbody>
    <tr>
      <th>ログテクノロジー</th>
      <th>AEM</th>
      <th>Dispatcher</th>
      <th>CDN</th>
    </tr>
    <tr>
      <td>Amazon S3</td>
      <td>はい</td>
      <td>はい</td>
      <td style="background-color: #ffb3b3;">未来</td>
    </tr>
    <tr>
      <td>Azure Blob Storage</td>
      <td>はい</td>
      <td>はい</td>
      <td>はい</td>
    </tr>
    <tr>
      <td>DataDog</td>
      <td>はい</td>
      <td>はい</td>
      <td>はい</td>
    </tr>
    <tr>
      <td>Dynatrace</td>
      <td>はい</td>
      <td>はい</td>
      <td style="background-color: #ffb3b3;">未来</td>
    </tr>
    <tr>
      <td>ElasticSearch<br>OpenSearch</td>
      <td>はい</td>
      <td>はい</td>
      <td>はい</td>
    </tr>
    <tr>
      <td>HTTPS</td>
      <td>はい</td>
      <td>はい</td>
      <td>はい</td>
    </tr>
    <tr>
      <td>New Relic</td>
      <td>はい</td>
      <td>はい</td>
      <td style="background-color: #ffb3b3;">未来</td>
    </tr>
    <tr>
      <td>Splunk</td>
      <td>はい</td>
      <td>はい</td>
      <td>はい</td>
    </tr>
    <tr>
      <td>Sumo Logic</td>
      <td>はい</td>
      <td>はい</td>
      <td style="background-color: #ffb3b3;">未来</td>
    </tr>
  </tbody>
</table>

>[!NOTE]
>
> 今後予定されている今後の CDN ログテクノロジーについては、[aemcs-logforwarding-beta@adobe.com](mailto:aemcs-logforwarding-beta@adobe.com) にメールを送信して関心をご登録ください。

ログ転送は、Git で設定を宣言することでセルフサービス方式で設定され、Cloud Manager 設定パイプラインを通じて開発環境、ステージング環境、本番環境の各タイプにデプロイできます。設定ファイルは、コマンドラインツールを使用して高速開発環境（RDE）にデプロイできます。

AEM および Apache／Dispatcher ログを、専用エグレス IP などの AEM の高度なネットワークインフラストラクチャ経由でルーティングするオプションがあります。

ログの宛先に送信されるログに関連付けられるネットワーク帯域幅は、組織のネットワーク I/O 使用の一部と見なされます。

## この記事の編成方法 {#how-organized}

この記事は、次の方法で編成されています。

* 設定 - すべてのログの宛先に共通
* トランスポートと高度なネットワーク - ログ設定を作成する前に、ネットワーク設定を考慮する必要があります。
* ログの宛先設定 - 各宛先の形式はわずかに異なります
* ログエントリ形式 - ログエントリ形式に関する情報
* 従来のログ転送からの移行 - アドビで以前設定したログ転送からセルフサービスアプローチに移行する方法

## 設定 {#setup}

1. `logForwarding.yaml` という名前のファイルを作成します。これには、[設定パイプライン](/help/operations/config-pipeline.md#common-syntax)の記事で説明されているように、メタデータを含める必要があります（**kind** は `LogForwarding` に設定し、version は「1」に設定する必要があります）。設定は次のようになります（例として Splunk を使用します）。

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

1. RDE（コマンドラインツールを使用する環境）以外の環境タイプでは、設定パイプラインの記事の[このセクション](/help/operations/config-pipeline.md#creating-and-managing)で参照されているように、Cloud Manager で対象のデプロイメント設定パイプラインを作成します。フルスタックパイプラインと web 階層設定パイプラインでは、設定ファイルがデプロイされないことに注意してください。

1. 設定をデプロイします。

設定内のトークン（`${{SPLUNK_TOKEN}}` など）は秘密鍵を表すので、Git に保存しないでください。代わりに、Cloud Manager [秘密鍵環境変数](/help/operations/config-pipeline.md#secret-env-vars)として宣言します。ログをオーサー層、パブリッシュ層およびプレビュー層に転送できるように、「適用されるサービス」フィールドのドロップダウン値として「**すべて**」を選択していることを確認します。

**default** ブロックの後に追加の **cdn** ブロックや **aem** ブロックを含めることで、CDN ログと AEM ログ（Apache／Dispatcher を含む）間で異なる値を設定できます。この場合、プロパティは **default** ブロックで定義されたプロパティを上書きできます。必要なのは enabled プロパティのみです。次の例に示すように、CDN ログに別の Splunk インデックスを使用するユースケースが考えられます。

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

もう 1 つのシナリオは、CDN ログまたは AEM ログ（Apache／Dispatcher を含む）のいずれかの転送を無効にすることです。例えば、CDN ログのみを転送するには、次を設定します。

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

 一部の組織では、ログの宛先で受信できるトラフィックを制限することを選択する場合もあれば、HTTPS（443）以外のポートの使用を要求する場合もあります。その場合は、ログ転送設定をデプロイする前に、[高度なネットワーク](/help/security/configuring-advanced-networking.md)を設定する必要があります。

次の表を使用して、ポート 443 を使用しているかどうか、固定 IP アドレスからログを表示する必要があるかどうかに基づいて、高度なネットワークとログの設定の要件を確認します。

<table>
  <tbody>
    <tr>
      <th>宛先ポート</th>
      <th>固定 IP からログを表示するための要件があるか？</th>
      <th>高度なネットワークが必要</th>
      <th>LogForwarding.yaml ポート定義が必要</th>
    </tr>
    <tr>
      <td rowspan="2" ro>HTTPS（443）</td>
      <td>いいえ</td>
      <td>いいえ</td>
      <td>いいえ</td>
    </tr>
    <tr>
      <td>はい</td>
      <td>はい、<a href="/help/security/configuring-advanced-networking.md#dedicated-egress-ip-address-dedicated-egress-ip-address">専用エグレス</a></td>
      <td>いいえ</td>
    <tr>
    <tr>
      <td rowspan="2">標準以外のポート（例：8088）</td>
      <td>いいえ</td>
      <td>はい、<a href="/help/security/configuring-advanced-networking.md#flexible-port-egress-flexible-port-egress">フレキシブルエグレス</a></td>
      <td>はい</td>
    </tr>
    <tr>
      <td>はい</td>
      <td>はい、<a href="/help/security/configuring-advanced-networking.md#dedicated-egress-ip-address-dedicated-egress-ip-address">専用エグレス</a></td>
      <td>はい</td>
  </tbody>
</table>

>[!NOTE]
>ログが単一の IP アドレスから表示されるかどうかは、高度なネットワーク設定の選択によって決まります。これを容易にするには、専用エグレスを使用する必要があります。
>
> 高度なネットワーク設定は、プログラムレベルと環境レベルでのイネーブルメントを必要とする [2 段階のプロセス](/help/security/configuring-advanced-networking.md#configuring-and-enabling-advanced-networking-configuring-enabling)です。

AEM ログ（Apach／Dispatcher を含む）の場合、[高度なネットワーク](/help/security/configuring-advanced-networking.md)を設定している場合は、`aem.advancedNetworking` プロパティを使用して、専用エグレス IP アドレスまたは VPN 経由でログを転送できます。

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

CDN ログの場合、[Fastly ドキュメント - パブリック IP リスト](https://www.fastly.com/documentation/reference/api/utils/public-ip-list/)の説明に従って、IP アドレスを許可リストに登録できます。共有 IP アドレスのリストが大きすぎる場合は、既知の IP から最終的な宛先にログを送信するロジックを記述できる https サーバーまたは（アドビ以外の）Azure Blob Store にトラフィックを送信することを考慮します。

>[!NOTE]
>
>CDN ログが AEM ログと同じ IP アドレスから表示されることはありません。これは、ログが AEM Cloud Service ではなく Fastly から直接送信されるからです。
>
>このため、高度なネットワーク VPN 設定でログ転送を使用することはできません。

## ログの宛先設定 {#logging-destinations}

サポートされているログの宛先の設定と、特定の考慮事項を以下に示します。

### Amazon S3 {#amazons3}

Amazon S3 へのログ転送では、AEM と Dispatcher のログがサポートされていますが、CDN ログはまだサポートされていません。

>[!NOTE]
>
>ログは、ログファイルのタイプごとに 10 分ごとに S3 に定期的に書き込まれます。これにより、機能を切り替えた後は、S3 へのログの書き込みに初期遅延が発生する場合があります。  [この動作の詳細情報](https://docs.fluentbit.io/manual/pipeline/outputs/s3#differences-between-s3-and-other-fluent-bit-outputs)。

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

S3 ログ転送ツールを使用するには、S3 バケットへのアクセスに関する適切なポリシーを AWS IAM ユーザーに事前設定する必要があります。  IAM ユーザー資格情報の作成方法について詳しくは、[AWS IAM ユーザードキュメント](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_credentials_access-keys.html)を参照してください。

IAM ポリシーでは、ユーザーに `s3:putObject` の使用を許可する必要があります。例：

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

実装方法について詳しくは、[AWS バケットポリシードキュメント](https://docs.aws.amazon.com/AmazonS3/latest/userguide/bucket-policies.html)を参照してください。

>[!NOTE]
>AWS S3 の CDN ログのサポートは、今後予定されています。 関心を登録するには、[aemcs-logforwarding-beta@adobe.com](mailto:aemcs-logforwarding-beta@adobe.com) までメールでお問い合わせください。

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

認証には、SAS トークンを使用する必要があります。これは、共有アクセストークンページではなく、共有アクセス署名ページから作成し、次の設定を行う必要があります。

* 許可するサービス：BLOBを選択する必要があります。
* 許可するリソース：オブジェクトを選択する必要があります。
* 許可する権限：書き込み、追加、作成を選択する必要があります。
* 有効な開始日時と有効期限。

サンプル SAS トークン設定のスクリーンショットを次に示します。

![Azure Blob SAS トークン設定](/help/implementing/developing/introduction/assets/azureblob-sas-token-config.png)

以前は正常に機能していたログの配信が停止した場合は、設定した SAS トークンが期限切れになっていることがあるので、まだ有効かどうかを確認します。

#### Azure Blob Storage CDN ログ {#azureblob-cdn}

グローバルに分散された各ログサーバーは、`aemcdn` フォルダーの下に数秒ごとに新しいファイルを生成します。 一度作成したファイルは、それ以降は追加されません。ファイル名の形式は、YYYY-MM-DDThh:mm:ss.sss-uniqueid.log です。例：2024-03-04T10:00:00.000-WnFWYN9BpOUs2aOVn4ee.log.

例えば、ある時点で次のようになります。

```text
aemcdn/
   2024-03-04T10:00:00.000-abc.log
   2024-03-04T10:00:00.000-def.log
```

30 秒後には、次のようになります。

```text
aemcdn/
   2024-03-04T10:00:00.000-abc.log
   2024-03-04T10:00:00.000-def.log
   2024-03-04T10:00:30.000-ghi.log
   2024-03-04T10:00:30.000-jkl.log
   2024-03-04T10:00:30.000-mno.log
```

各ファイルには、それぞれが別の行に記述された複数の JSON ログエントリが含まれます。ログエントリの形式について詳しくは、[AEM as a Cloud Service のログ](/help/implementing/developing/introduction/logging.md)を参照してください。また、各ログエントリには、次の[ログエントリ形式](#log-formats)の節で説明するその他のプロパティも含まれます。

#### Azure Blob Storage AEM ログ {#azureblob-aem}

AEM ログ（Apache／Dispatcher を含む）は、次の命名規則に従ってフォルダーの下に表示されます。

* aemaccess
* aemerror
* aemrequest
* aemdispatcher
* aemhttpdaccess
* aemhttpderror

各フォルダーの下に単一のファイルが作成および追加されます。このファイルが大きくなりすぎないように、処理と管理はお客様の責任となります。

[AEM as a Cloud Service のログ](/help/implementing/developing/introduction/logging.md)のログエントリ形式を参照してください。ログエントリには、次の[ログエントリ形式](#log-formats)の節で説明するその他のプロパティも含まれます。

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
* tags プロパティはオプションです
* AEM ログの場合、Datadog ソースタグは、`aemaccess`、`aemerror`、`aemrequest`、`aemdispatcher`、`aemhttpdaccess` または `aemhttpderror` のいずれかに設定されます
* CDN ログの場合、Datadog ソースタグは、`aemcdn` に設定されます
* Datadog サービスタグは、`adobeaemcloud` に設定されていますが、tags セクションで上書きできます
* ログ転送用の適切なインデックスを決定するために、取り込みパイプラインで Datadog タグを使用している場合は、ログ転送 YAML ファイルでこれらのタグが正しく設定されていることを確認します。タグが欠落していると、パイプラインがタグに依存している場合に、ログの取り込みに成功しないことがあります。

### Elasticsearch および OpenSearch {#elastic}

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

* デフォルトでは、ポートは 443 です。オプションで `port` というプロパティで上書きできます
* 資格情報には、アカウント資格情報ではなく、デプロイメント資格情報を使用します。次の画像のような画面で生成される資格情報を以下に示します。

![Elastic デプロイメント資格情報](/help/implementing/developing/introduction/assets/ec-creds.png)

* AEM ログの場合、`index` は、`aemaccess`、`aemerror`、`aemrequest`、`aemdispatcher`、`aemhttpdaccess` または `aemhttpderror` のいずれかに設定されます
* オプションのパイプラインプロパティは、Elasticsearch または OpenSearch 取り込みパイプラインの名前に設定する必要があります。このパイプラインは、ログエントリを適切なインデックスにルーティングするように設定できます。パイプラインのプロセッサータイプは *script* に設定し、スクリプト言語は *painless* に設定する必要があります。 次に、ログエントリを aemaccess_dev_26_06_2024 などのインデックスにルーティングするサンプルスクリプトスニペットを示します。

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

* URL 文字列には **https://** を含める必要があります。そうしないと検証が失敗します。
* URL にはポートを含めることができます。 例えば、`https://example.com:8443/aem_logs/aem` のようになります。URL 文字列にポートが含まれていない場合、ポート 443（デフォルトの HTTPS ポート）が想定されます。

#### HTTPS CDN ログ {#https-cdn}

Web リクエスト（POST）は、ログエントリの配列である JSON ペイロードを使用して継続的に送信されます。ログエントリ形式について詳しくは、[AEM as a Cloud Service のログ](/help/implementing/developing/introduction/logging.md#cdn-log)を参照してください。 その他のプロパティについて詳しくは、次の[ログエントリ形式](#log-formats)の節を参照してください。

また、`sourcetype` という名前のプロパティもあり、その値は `aemcdn` に設定されています。

>[!NOTE]
>
> 最初の CDN ログエントリが送信される前に、HTTP サーバーは 1 回限りのチャレンジを正常に完了する必要があります。つまり、パス ``/.well-known/fastly/logging/challenge`` に送信されたリクエストは、本文にアスタリスク ``*`` が含まれ、ステータスコード 200 で応答する必要があります。

#### HTTPS AEM ログ {#https-aem}

AEM ログ（apache／dispacher を含む）の場合、web リクエスト（POST） は、ログエントリの配列である JSON ペイロードを使用して継続的に送信されます。様々なログエントリ形式について詳しくは、[AEM as a Cloud Service のログ](/help/implementing/developing/introduction/logging.md)を参照してください。その他のプロパティについて詳しくは、次の[ログエントリ形式](#log-formats)の節を参照してください。

また、`Source-Type` という名前のプロパティもあり、その値は次のいずれかに設定されています。

* aemaccess
* aemerror
* aemrequest
* aemdispatcher
* aemhttpdaccess
* aemhttpderror

### New Relic Log API {#newrelic-https}

New Relic へのログ転送では、New Relic HTTPS API を取り込みに活用します。現在は、AEM と Dispatcher からのログのみがサポートされており、CDN ログはまだサポートされていません。

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
>New Relic へのログ転送は、お客様が所有している New Relic アカウントでのみ使用できます。
>
>New Relic Log API の CDN ログのサポートは、今後予定されています。 関心を登録するには、[aemcs-logforwarding-beta@adobe.com](mailto:aemcs-logforwarding-beta@adobe.com) までメールでお問い合わせください。
>
>New Relic では、New Relic アカウントがプロビジョニングされている場所に基づいて、地域固有のエンドポイントを提供します。詳しくは、[New Relic ドキュメント](https://docs.newrelic.com/docs/logs/log-api/introduction-log-api/#endpoint)を参照してください。

### Dynatrace Log API {#dynatrace-https}

Dynatrace へのログ転送では、Dynatrace HTTPS API を取り込みに活用します。現在は、AEM と Dispatcher からのログのみがサポートされており、CDN ログはまだサポートされていません。

トークンには、「ログを取り込み」スコープ属性が必要です。

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
>Dynatrace Log API の CDN ログのサポートは、今後予定されています。 関心を登録するには、[aemcs-logforwarding-beta@adobe.com](mailto:aemcs-logforwarding-beta@adobe.com) までメールでお問い合わせください。

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

* デフォルトでは、ポートは 443 です。オプションで `port` というプロパティで上書きできます
* sourcetype フィールドには、特定のログに応じて、次のいずれかの値が設定されます。*aemaccess*、*aemerror*、
  *aemrequest*、*aemdispatcher*、*aemhttpdaccess*、*aemhttpderror*、*aemcdn*
* 必要な IP が許可リストに登録されていてもログが配信されない場合は、Splunk トークンの検証を適用するファイアウォールルールがないことを確認します。Fastly は、無効な Splunk トークンが意図的に送信される最初の検証ステップを実行します。ファイアウォールが無効な Splunk トークンとの接続を終了するように設定されている場合、検証プロセスは失敗し、Fastly が Splunk インスタンスにログを配信できなくなります。

>[!NOTE]
>
> 従来のログ転送からこのセルフサービスモデルに[移行する場合](#legacy-migration)、Splunk インデックスに送信される `sourcetype` フィールドの値が変更されていることがあるので、それに応じて調整します。

### Sumo Logic {#sumologic}

Sumo Logic へのログ転送では、AEM と Dispatcher のログがサポートされていますが、CDN ログはまだサポートされていません。

Sumo Logic をデータ取り込み用に設定すると、ホスト、receiverURI、秘密鍵を単一の文字列で提供する「HTTP ソースアドレス」が表示されます。例：

`https://collectors.de.sumologic.com/receiver/v1/http/ZaVnC...`

URL の最後のセクション（先頭の `/` を除く）をコピーし、上記の[設定](#setup)の節で説明したように、[CloudManager 秘密鍵環境変数](/help/operations/config-pipeline.md#secret-env-vars)として追加し、設定でその変数を参照する必要があります。次に例を示します。

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
>SumoLogic の CDN ログのサポートは今後予定されています。 関心を登録するには、[aemcs-logforwarding-beta@adobe.com](mailto:aemcs-logforwarding-beta@adobe.com) までメールでお問い合わせください。
>
> 「index」フィールド機能を利用するには、Sumo Logic Enterprise サブスクリプションが必要です。エンタープライズ以外のサブスクリプションでは、ログは標準として `sumologic_default` パーティションにルーティングされます。詳しくは、[Sumo Logic パーティションドキュメント](https://help.sumologic.com/docs/search/optimize-search-partitions/)を参照してください。

## ログエントリ形式 {#log-formats}

各ログタイプ（CDN ログ、Apache／Dispatcher を含む AEM ログ）の形式について詳しくは、[AEM as a Cloud Service のログ](/help/implementing/developing/introduction/logging.md)を参照してください。

複数のプログラムや環境からのログが同じログの宛先に転送される場合があるので、ログの記事で説明されている出力に加えて、各ログエントリには次のプロパティが含まれます。

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

## 従来のログ転送からの移行 {#legacy-migration}

ログ転送の設定がセルフサービスモデルを通じて実現される前は、お客様がサポートチケットを開くようリクエストされ、アドビが統合を開始していました。

アドビによってそのように設定されたお客様は、都合に合わせてセルフサービスモデルに適応できます。この移行を行う理由がいくつかあります。

* 新しい環境（例：新しい開発環境または RDE）がプロビジョニングされた。
* 既存の Splunk エンドポイントまたは資格情報に対する変更。
* CDN ログが使用可能になる前にアドビがログ転送を設定しており、CDN ログの受信を希望している。
* 時間的な制約のある変更が必要になる前に、組織が知識を得られるよう、セルフサービスモデルにプロアクティブに適応するという意識的な決定。

移行の準備が整ったら、前の節で説明したように YAML ファイルを設定するだけです。Cloud Manager 設定パイプラインを使用して、設定を適用する必要がある各環境にデプロイします。

すべての環境に設定をデプロイし、セルフサービスで制御できるようにすることをお勧めしますが、必須ではありません。そうしないと、アドビが設定した環境とセルフサービスで設定した環境を区別できなくなる場合があります。

>[!NOTE]
>
>Splunk インデックスに送信される `sourcetype` フィールドの値が変更されていることがあるので、それに応じて調整します。
>
>アドビサポートが以前に設定した環境にログ転送をデプロイすると、最大で数時間、重複したログを受信する場合があります。これは最終的には自動的に解決されます。
