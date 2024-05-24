---
title: AEMas a Cloud Serviceのログ転送
description: AEM as a Cloud Serviceでの Splunk およびその他のログベンダーへのログの転送について説明します
hide: true
hidefromtoc: true
source-git-commit: d41390696383f8e430bb31bd8d56a5e8843f1257
workflow-type: tm+mt
source-wordcount: '583'
ht-degree: 3%

---


# ログ転送 {#log-forwarding}

>[!NOTE]
>
>この機能はまだリリースされておらず、一部のログ宛先はリリース時には使用できない場合があります。 それまでの間、サポートチケットを開いて、にログを転送できます **Splunk**（を参照） [ログ記事](/help/implementing/developing/introduction/logging.md).

ログベンダーのライセンスまたはログ製品のホストを持つお客様は、AEM、Apache/Dispatcher および CDN ログを、関連するログ出力先に転送できます。 AEM as a Cloud Serviceは、次のログ出力先をサポートしています。

* Azure Blob ストレージ
* DataDog
* Elasticsearchまたは OpenSearch
* HTTPS
* Splunk

ログ転送は、Git で設定を宣言し、Cloud Manager 設定パイプラインを介して実稼動（サンドボックス以外）プログラムの開発、ステージング、実稼動環境の各タイプにデプロイすることで、セルフサービス方式で設定されます。

ログの宛先に送信されたログに関連付けられているネットワーク帯域幅は、組織のネットワーク I/O 使用の一部と見なされることに注意してください。


## この記事の編成方法 {#how-organized}

この記事は、次のように構成されています。

* 設定 – すべてのログ宛先に共通
* 宛先設定のログ記録 – 各宛先の形式は若干異なります
* 高度なネットワーク – 専用のエグレスまたは VPN 経由でのAEMおよび Apache/Dispatcher ログの送信


## 設定 {#setup}

1. Git のプロジェクトの最上位フォルダーに、次のフォルダーとファイル構造を作成します。

   ```
   config/
        logForwarding.yaml
   ```

1. logForwarding.yaml には、メタデータと、次の形式に類似した設定が含まれている必要があります（例として Splunk を使用）。

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

   今後の互換性の向上のため、デフォルトノードを含める必要があります。

   kind パラメーターは LogForwarding に設定する必要があります。バージョンはスキーマのバージョン（1）に設定する必要があります。

   設定のトークン（など） `${{SPLUNK_TOKEN}}`）はシークレットを表すもので、Git に保存しないでください。 代わりに、Cloud Manager として宣言します  [環境変数](/help/implementing/cloud-manager/environment-variables.md) タイプ「秘密鍵」の。 必ずを選択してください。 **すべて** 「適用されるサービス」フィールドのドロップダウン値として使用することで、ログを、オーサー層、パブリッシュ層およびプレビュー層に転送できます。

1. RDE 以外の環境タイプ（現在サポートされていない）の場合は、Cloud Manager でターゲットのデプロイメント設定パイプラインを作成します。

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

考慮事項：

* SAS トークンを使用して認証します。SAS トークンには、最小検証期間が必要です。
* SAS トークンは、コンテナページではなく、アカウントページで作成する必要があります。

### Datadog {#datadog}

```
kind: "LogForwarding"
version: "1"
metadata:
  envTypes: ["dev"]
data:
  dataDog:
    default:
      enabled: true       
      host: "http-intake.logs.datadoghq.eu"
      token: "${{DATADOG_API_KEY}}"
      
```

考慮事項：

* 特定のクラウドプロバイダーとの統合を行わずに、API キーを作成します。


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
```

考慮事項：

* 資格情報には、アカウントの資格情報ではなく、必ずデプロイメントの資格情報を使用します。 これらは、次の画像に似た画面で生成される資格情報です。

![Elastic デプロイメント資格情報](/help/implementing/developing/introduction/assets/ec-creds.png)

### HTTPS {#https}

```
kind: "LogForwarding"
version: "1"
metadata:
  envTypes: ["dev"]
data:
  https:
    default:
      url: "https://example.com/aem_logs/aem"
      authHeaderName: "X-AEMaaCS-Log-Forwarding-Token"
      authHeaderValue: "${{HTTPS_LOG_FORWARDING_TOKEN}}"
```

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

## 高度なネットワーク {#advanced-networking}

ログの宛先へのトラフィックをロックダウンする組織要件がある場合は、通過するようにログ転送を設定できます [高度なネットワーク](/help/security/configuring-advanced-networking.md). オプションのを利用した、以下の 3 つの高度なネットワークタイプのパターンを参照してください。 `port` パラメーター、 `host` パラメーター。

### フレキシブルポートエグレス {#flex-port}

ログトラフィックが 443 （以下の 8443 など）以外のポートに送信される場合は、次のように高度なネットワークを設定します。

```
{
    "portForwards": [
        {
            "name": "mylogging.service.logger.com",
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
      host: "proxy.tunnel"
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
            "name": "mylogging.service.com",
            "portDest": 443, # something other than 443
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
      host: "proxy.tunnel"
      token: "${{SomeToken}}"
      port: 30443
      index: "index_name"
```

### VPN {#vpn}

ログトラフィックを VPN 経由で送信する必要がある場合は、次のように高度なネットワークを設定します。

```
{
    "portForwards": [
        {
            "name": "mylogging.service.com",
            "portDest": 443, # something other than 443
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
      host: "mylogging.service.com"
      token: "${{SomeToken}}"
      port: 30443
      index: "index_name"
```
