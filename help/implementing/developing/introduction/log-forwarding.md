---
title: AEM as a Cloud Serviceのログ転送
description: AEM as a Cloud Serviceでの Splunk およびその他のログベンダーへのログの転送について説明します
exl-id: 27cdf2e7-192d-4cb2-be7f-8991a72f606d
feature: Developing
role: Admin, Architect, Developer
source-git-commit: 17d195f18055ebd3a1c4a8dfe1f9f6bc35ebaf37
workflow-type: tm+mt
source-wordcount: '1362'
ht-degree: 3%

---

# ログ転送 {#log-forwarding}

>[!NOTE]
>
>この機能はまだリリースされておらず、一部のログ宛先はリリース時には使用できない場合があります。 それまでの間、サポートチケットを開いて、**AEM as a Cloud Serviceのログ** に記載されているように、[Splunk](/help/implementing/developing/introduction/logging.md) にログを転送できます。

ログベンダーのライセンスまたはログ製品のホストのライセンスを持つお客様は、AEM ログ（Apache/Dispatcherを含む）および CDN ログを、関連するログ出力先に転送できます。 AEM as a Cloud Serviceは、次のログ出力先をサポートしています。

* Azure Blob ストレージ
* DataDog
* Elasticsearchまたは OpenSearch
* HTTPS
* Splunk

ログ転送は、Git で設定を宣言し、Cloud Manager設定パイプラインを介して実稼動（サンドボックス以外）プログラムの開発、ステージング、実稼動環境タイプにデプロイすることで、セルフサービス方式で設定されます。

AEMと Apache/Dispatcherのログを、専用のエグレス IP などのAEMの高度なネットワークインフラストラクチャ経由でルーティングするオプションがあります。

ログの宛先に送信されたログに関連付けられているネットワーク帯域幅は、組織のネットワーク I/O 使用の一部と見なされることに注意してください。


## この記事の編成方法 {#how-organized}

この記事は、次のように構成されています。

* 設定 – すべてのログ宛先に共通
* 宛先設定のログ記録 – 各宛先の形式は若干異なります
* ログエントリ形式 – ログエントリ形式に関する情報
* 高度なネットワーク – 専用のエグレスまたは VPN 経由でのAEMおよび Apache/Dispatcher ログの送信


## 設定 {#setup}

1. `logForwarding.yaml` という名前のファイルを作成します。[ 設定パイプラインの記事 ](/help/operations/config-pipeline.md#common-syntax) で説明しているように、メタデータ（**kind** を `LogForwarding` に、バージョンを「1」に設定する必要があります）と、次のような設定を含める必要があります（例として Splunk を使用します）。

   ```
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

1. RDE 以外の環境タイプ（現在サポートされていません）の場合は、[ この節 ](/help/operations/config-pipeline.md#creating-and-managing) で参照されているように、Cloud Managerでターゲット設定パイプラインを作成します。フルスタックパイプラインと web 階層設定パイプラインでは設定ファイルをデプロイしません。

1. 設定をデプロイします。

設定内のトークン（`${{SPLUNK_TOKEN}}` など）は秘密鍵を表しているので、Git に保存しないでください。 代わりに、Cloud Manager[ シークレット環境変数 ](/help/operations/config-pipeline.md#secret-env-vars) として宣言します。 ログをオーサー層、パブリッシュ層およびプレビュー層に転送できるように、「適用されるサービス」フィールドのドロップダウン値として **すべて** を必ず選択してください。

**default** ブロックの後に追加の **cdn** ブロックや **aem** ブロックを含めることで、CDN ログとAEM ログ（Apache/Dispatcherを含む）に異なる値を設定できます。このブロックでは、プロパティを **default** ブロックで定義されたプロパティを上書きできます。必要なのは、有効なプロパティのみです。 以下の例に示すように、CDN ログに別の Splunk インデックスを使用する使用例が考えられます。

```
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

```
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

## 宛先設定のログ記録 {#logging-destinations}

サポートされるログの宛先の設定を、具体的な考慮事項と共に以下に示します。

### Azure Blob ストレージ {#azureblob}

```
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

#### Azure Blob Storage CDN ログ {#azureblob-cdn}

グローバルに分散された各ログサーバーは、`aemcdn` フォルダーの下で、数秒ごとに新しいファイルを生成します。 作成したファイルは、に追加されなくなります。 ファイル名の形式は YYYY-MM-DDThh:mm:ss.sss-uniqueid.log です。 例：2024-03-04T10:00:00.000-WnFWYN9BpOUs2aOVn4ee.log

例えば、ある時点で次のようになります。

```
aemcdn/
   2024-03-04T10:00:00.000-abc.log
   2024-03-04T10:00:00.000-def.log
```

30 秒後には、

```
aemcdn/
   2024-03-04T10:00:00.000-abc.log
   2024-03-04T10:00:00.000-def.log
   2024-03-04T10:00:30.000-ghi.log
   2024-03-04T10:00:30.000-jkl.log
   2024-03-04T10:00:30.000-mno.log
```

各ファイルには、それぞれ別の行に記述された複数の JSON ログエントリが含まれます。 ログエントリの形式については、[AEM as a Cloud Serviceのログ ](/help/implementing/developing/introduction/logging.md) を参照してください。各ログエントリには、以下の [ ログエントリの形式 ](#log-format) の節で説明しているその他のプロパティも含まれています。

#### Azure Blob Storage AEM ログ {#azureblob-aem}

AEM ログ（Apache/Dispatcherを含む）は、次の命名規則でフォルダーの下に表示されます。

* aemaccess
* aemerror
* aemrequest
* aemdispatcher
* aemhttpdaccess
* aemhttpderror

各フォルダーに 1 つのファイルが作成され、に追加されます。 お客様は、このファイルが大きくなりすぎないよう、ファイルの処理と管理を行います。

[AEM as a Cloud Serviceのログ ](/help/implementing/developing/introduction/logging.md) のログエントリフォーマットを参照してください。 ログエントリには、以下の [ ログエントリの形式 ](#log-formats) の節で説明する追加のプロパティも含まれます。


### Datadog {#datadog}

```
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

考慮事項：

* 特定のクラウドプロバイダーとの統合を行わずに、API キーを作成します。
* tags プロパティはオプションです
* AEM ログの場合、Datadog ソース タグは `aemaccess`、`aemerror`、`aemrequest`、`aemdispatcher`、`aemhttpdaccess`、`aemhttpderror` のいずれかに設定されます
* CDN ログの場合、Datadog ソース タグは `aemcdn` に設定されます
* datadog サービスタグは `adobeaemcloud` に設定されていますが、タグセクションで上書きできます


### Elasticsearchと OpenSearch {#elastic}

```
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

考慮事項：

* デフォルトでは、ポートは 443 です。 オプションで、`port` というプロパティで上書きすることもできます
* 資格情報には、アカウントの資格情報ではなく、必ずデプロイメントの資格情報を使用します。 これらは、次の画像に似た画面で生成される資格情報です。

![Elastic デプロイメント資格情報 ](/help/implementing/developing/introduction/assets/ec-creds.png)

* AEM ログの場合、`index` は `aemaccess`、`aemerror`、`aemrequest`、`aemdispatcher`、`aemhttpdaccess` または `aemhttpderror` のいずれかに設定されます
* オプションのパイプラインプロパティは、Elasticsearchまたは OpenSearch 取り込みパイプラインの名前に設定する必要があります。この名前は、ログエントリを適切なインデックスにルーティングするように設定できます。 パイプラインのプロセッサタイプは *スクリプト* に設定し、スクリプト言語は *痛みなし* に設定する必要があります。 次に、ログエントリを aemaccess_dev_26_06_2024 などのインデックスにルーティングするスクリプトスニペットの例を示します。

```
def envType = ctx.aem_env_type != null ? ctx.aem_env_type : 'unknown';
def sourceType = ctx._index;
def date = new SimpleDateFormat('dd_MM_yyyy').format(new Date());
ctx._index = sourceType + "_" + envType + "_" + date;
```

### HTTPS {#https}

```
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

考慮事項：

* URL 文字列には **https://** を含める必要があります。含めない場合、検証が失敗します。
* URL にはポートを含めることができます。 例えば、`https://example.com:8443/aem_logs/aem` のようになります。URL 文字列にポートが含まれていない場合、ポート 443 （デフォルトの HTTPS ポート）が想定されます。

#### HTTPS CDN ログ {#https-cdn}

Web リクエスト（POST）は、ログエントリの配列である json ペイロードを使用して継続的に送信されます。ログエントリの形式については、「[AEM as a Cloud Serviceのログ ](/help/implementing/developing/introduction/logging.md#cdn-log) を参照してください。 その他のプロパティについては、以下の「[ ログエントリの形式 ](#log-formats) の節で説明します。

また、`sourcetype` という名前のプロパティもあり、`aemcdn` という値に設定されています。

>[!NOTE]
>
> 最初の CDN ログエントリが送信される前に、HTTP サーバーは、1 回限りのチャレンジを正常に完了する必要があります。つまり、パスに送信され ``/.well-known/fastly/logging/challenge`` リクエストは、本文にアスタリスクの ``*`` と 200 個のステータスコードで応答する必要があります。

#### HTTPS AEM ログ {#https-aem}

AEM ログ（apache/dispatcher を含む）の場合、web リクエスト（POST）は、[AEM as a Cloud Serviceのログ ](/help/implementing/developing/introduction/logging.md) で説明されているように、様々なログエントリ形式でログエントリの配列である json ペイロードで継続的に送信されます。 その他のプロパティについては、以下の「[ ログエントリの形式 ](#log-format) の節で説明します。

`Source-Type` という名前のプロパティもあり、次のいずれかの値に設定されます。

* aemaccess
* aemerror
* aemrequest
* aemdispatcher
* aemhttpdaccess
* aemhttpderror

### Splunk {#splunk}

```
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

考慮事項：

* デフォルトでは、ポートは 443 です。 オプションで、`port` という名前のプロパティで上書きできます。


<!--
### Sumo Logic {#sumologic}

   ```
   kind: "LogForwarding"
   version: "1"
   metadata:
     envTypes: ["dev"]
   data:
     splunk:
       default:
         enabled: true
         host: "https://collectors.de.sumologic.com"
         uri: "/receiver/v1/http"
         privateKey: "${{SomeOtherToken}}"
   
   ```   
-->

## ログエントリの形式 {#log-formats}

各ログタイプ（CDN ログおよび Apache/Dispatcherを含むAEM ログ）の形式については、[AEM as a Cloud Serviceのログ ](/help/implementing/developing/introduction/logging.md) を参照してください。

複数のプログラムおよび環境からのログは、ログ記事で説明されている出力に加えて、同じログ宛先に転送される場合があるので、次のプロパティが各ログエントリに含まれます。

* aem_env_id
* aem_env_type
* aem_program_id
* aem_tier

例えば、プロパティには次の値を含めることができます。

```
aem_env_id: 1242
aem_env_type: dev
aem_program_id: 12314
aem_tier: author
```

## 高度なネットワーク {#advanced-networking}

一部の組織は、ログの宛先で受信できるトラフィックを制限します。

CDN ログの場合は、[fastly ドキュメント – 公開 IP リスト ](https://www.fastly.com/documentation/reference/api/utils/public-ip-list/) で説明しているように、IP アドレスを許可リストに登録できます。 その共有 IP アドレスのリストが大きすぎる場合は、https Adobeまたは（サーバー以外の） Azure Blob Store にトラフィックを送信することを検討してください。そこでは、既知の IP から最終的な宛先にログを送信するロジックを書き込むことができます。

AEM ログ（Apache/Dispatcherを含む）の場合、[ 高度なネットワーク ](/help/security/configuring-advanced-networking.md) を設定している場合は、advancedNetworking プロパティを使用して、専用のエグレス IP アドレスから、または VPN 経由で転送できます。

```
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

