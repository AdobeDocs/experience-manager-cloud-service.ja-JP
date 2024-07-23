---
title: AEM as a Cloud Serviceのログ転送
description: AEM as a Cloud Serviceでの Splunk およびその他のログベンダーへのログの転送について説明します
exl-id: 27cdf2e7-192d-4cb2-be7f-8991a72f606d
feature: Developing
role: Admin, Architect, Developer
source-git-commit: cb4299be4681b24852a7e991c123814d31f83cad
workflow-type: tm+mt
source-wordcount: '1349'
ht-degree: 1%

---

# ログ転送 {#log-forwarding}

>[!NOTE]
>
>この機能はまだリリースされておらず、一部のログ宛先はリリース時には使用できない場合があります。 それまでの間、サポートチケットを開いて、**ログ記事 [ で説明しているように、ログを** Splunk](/help/implementing/developing/introduction/logging.md) に転送できます。

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

1. Git のプロジェクトの最上位フォルダーに、次のフォルダーとファイル構造を作成します。

   ```
   config/
        logForwarding.yaml
   ```

1. メタデータと、次の形式に類似した設定を含める必要が `logForwarding.yaml` ります（例として Splunk を使用）。

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

   **kind** パラメーターはに設定する必要があります。また `LogForwarding` バージョンはスキーマバージョン（1）に設定する必要があります。

   設定内のトークン（`${{SPLUNK_TOKEN}}` など）は秘密鍵を表しているので、Git に保存しないでください。 代わりに、**secret** 型のCloud Manager[ 環境変数 ](/help/implementing/cloud-manager/environment-variables.md) として宣言します。 ログをオーサー層、パブリッシュ層およびプレビュー層に転送できるように、「適用されるサービス」フィールドのドロップダウン値として **すべて** を必ず選択してください。

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

1. RDE 以外の環境タイプ（現在サポートされていない環境）の場合は、ターゲット設定パイプラインをCloud Managerで作成します。フルスタックパイプラインと web 階層設定パイプラインでは、設定ファイルをデプロイしません。

   * [実稼動パイプラインの設定を参照してください](/help/implementing/cloud-manager/configuring-pipelines/configuring-production-pipelines.md)。
   * [実稼動以外のパイプラインの設定を参照してください](/help/implementing/cloud-manager/configuring-pipelines/configuring-non-production-pipelines.md)。

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

各ファイルには、それぞれ別の行に記述された複数の JSON ログエントリが含まれます。 ログエントリの形式については [ ログに関する記事 ](/help/implementing/developing/introduction/logging.md) を参照してください。また、各ログエントリには、以下の [ ログエントリの形式 ](#log-format) の節で説明する追加のプロパティも含まれます。

#### Azure Blob Storage AEM ログ {#azureblob-aem}

AEM ログ（Apache/Dispatcherを含む）は、次の命名規則でフォルダーの下に表示されます。

* aemaccess
* aemerror
* aemdispatcher
* httpdaccess
* httpderror

各フォルダーに 1 つのファイルが作成され、に追加されます。 お客様は、このファイルが大きくなりすぎないよう、ファイルの処理と管理を行います。

[ ログに関する記事 ](/help/implementing/developing/introduction/logging.md) のログエントリ形式を参照してください。 ログエントリには、以下の [ ログエントリの形式 ](#log-formats) の節で説明する追加のプロパティも含まれます。


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

* 資格情報には、アカウントの資格情報ではなく、必ずデプロイメントの資格情報を使用します。 これらは、次の画像に似た画面で生成される資格情報です。

![Elastic デプロイメント資格情報 ](/help/implementing/developing/introduction/assets/ec-creds.png)

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
      url: "https://example.com:8443/aem_logs/aem"
      authHeaderName: "X-AEMaaCS-Log-Forwarding-Token"
      authHeaderValue: "${{HTTPS_LOG_FORWARDING_TOKEN}}"
```

考慮事項：

* URL 文字列には **https://** を含める必要があります。含めない場合、検証が失敗します。 URL 文字列にポートが含まれていない場合、ポート 443 （デフォルトの HTTPS ポート）が想定されます。
* 443 以外のポートを使用したい場合は、URL の一部として指定してください。

#### HTTPS CDN ログ {#https-cdn}

Web リクエスト（POST）は、[ ログ記事 ](/help/implementing/developing/introduction/logging.md#cdn-log) で説明されているログエントリ形式で、ログエントリの配列である json ペイロードを使用して継続的に送信されます。 その他のプロパティについては、以下の「[ ログエントリの形式 ](#log-formats) の節で説明します。

また、`sourcetype` という名前のプロパティもあり、`aemcdn` という値に設定されています。

>[!NOTE]
>
> 最初の CDN ログエントリが送信される前に、HTTP サーバーは、1 回限りのチャレンジを正常に完了する必要があります。つまり、パスに送信され ``/.well-known/fastly/logging/challenge`` リクエストは、本文にアスタリスクの ``*`` と 200 個のステータスコードで応答する必要があります。

#### HTTPS AEM ログ {#https-aem}

AEM ログ（apache/dispatcher を含む）の場合、web リクエスト（POST）は、[ ログ記事 ](/help/implementing/developing/introduction/logging.md) で説明されているように、様々なログエントリ形式で、ログエントリの配列である json ペイロードを使用して継続的に送信されます。 その他のプロパティについては、以下の「[ ログエントリの形式 ](#log-format) の節で説明します。

`sourcetype` という名前のプロパティもあり、次のいずれかの値に設定されます。

* aemaccess
* aemerror
* aemdispatcher
* httpdaccess
* httpderror

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
      index: "AEMaaCS"
```

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

各ログタイプ（CDN ログおよび Apache/Dispatcherを含むAEM ログ）の形式については、一般的な [ ログに関する記事 ](/help/implementing/developing/introduction/logging.md) を参照してください。

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

>[!NOTE]
>
>この機能は、まだ早期導入の準備ができていません。


一部の組織は、ログの宛先で受信できるトラフィックを制限します。

CDN ログの場合は、[ この記事 ](https://www.fastly.com/documentation/reference/api/utils/public-ip-list/) で説明しているように、IP アドレスを許可リストに登録できます。 その共有 IP アドレスのリストが大きすぎる場合は、（Adobe以外の） Azure Blob Store にトラフィックを送信することを検討してください。このストアでは、専用の IP アドレスのログを最終的な送信先に送信するロジックを書き込むことができます。

AEM ログ（Apache/Dispatcherを含む）の場合は、ログ転送を設定して [ 高度なネットワーク機能 ](/help/security/configuring-advanced-networking.md) を実行できます。 オプションの `port` パラメーターと `host` パラメーターを利用する、以下の 3 つの高度なネットワークタイプのパターンを参照してください。

### フレキシブルポートエグレス {#flex-port}

ログトラフィックが 443 （以下の 8443 など）以外のポートに送信される場合は、次のように高度なネットワークを設定します。

```
{
    "portForwards": [
        {
            "name": "splunk-host.example.com",
            "portDest": 8443, # something other than 443
            "portOrig": 30443
        }    
    ]
}
```

次のように yaml ファイルを設定します。

```
kind: "LogForwarding"
version: "1"
data:
  splunk:
    default:
      host: "${{AEM_PROXY_HOST}}"
      token: "${{SomeToken}}"
      port: 30443
      index: "index_name"
```

### 専用エグレス IP {#dedicated-egress}


ログトラフィックを専用のエグレス IP から送信する必要がある場合は、次のように高度なネットワークを設定します。

```
{
    "portForwards": [
        {
            "name": "splunk-host.example.com",
            "portDest": 443, 
            "portOrig": 30443
        }    
    ]
}
```

次のように yaml ファイルを設定します。

```
      
kind: "LogForwarding"
version: "1"
   metadata:
     envTypes: ["dev"]
data:
  splunk:
     default:
       enabled: true
       index: "index_name" 
       token: "${{SPLUNK_TOKEN}}"  
     aem:
       enabled: true
       host: "${{AEM_PROXY_HOST}}"
       port: 30443       
     cdn:
       enabled: true
       host: "splunk-host.example.com"
       port: 443    
```

### VPN {#vpn}

ログトラフィックを VPN 経由で送信する必要がある場合は、次のように高度なネットワークを設定します。

```
{
    "portForwards": [
        {
            "name": "splunk-host.example.com",
            "portDest": 443,
            "portOrig": 30443
        }    
    ]
}

kind: "LogForwarding"
version: "1"
   metadata:
     envTypes: ["dev"]
data:
  splunk:
     default:
       enabled: true
       index: "index_name" 
       token: "${{SPLUNK_TOKEN}}"  
     aem:
       enabled: true
       host: "${{AEM_PROXY_HOST}}"
       port: 30443       
     cdn:
       enabled: true
       host: "splunk-host.example.com"
       port: 443     
```
