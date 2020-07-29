---
title: ログ
description: 一元的なログサービスのグローバルパラメーターの設定、個々のサービスに特有の設定、またはデータのログ記録の要求をおこなう方法を学習します。
translation-type: tm+mt
source-git-commit: 0bb5ff11762a4a3a158d211f8bba2ff77d1d3201
workflow-type: tm+mt
source-wordcount: '2053'
ht-degree: 6%

---


# ログ {#logging}

AEM as a Cloud Service は、カスタムコードを含めて、顧客ベースに独自のエクスペリエンスを作成する顧客のためのプラットフォームです。このことを念頭に置いた上で、ログは、ローカル開発およびクラウド環境、特にAEMをCloud Serviceの開発環境としてデバッグし、コード実行を理解するための重要な機能です。

AEMのログとログレベルは、AEMプロジェクトの一部としてGitに保存され、AEMプロジェクトの一部としてCloud Managerを介してデプロイされる構成ファイルで管理されます。 AEMにCloud Serviceとしてログインすると、次の2つの論理セットに分割できます。

* AEMログ。AEMアプリケーションレベルでログを実行します。
* Apache HTTPD Webサーバー/Dispatcherログ。Apache HTTPD Webサーバー/サーバーログは、WebサーバーとDispatcherのログを発行層で実行します。

## AEMログ {#aem-loggin}

AEMアプリケーションレベルでのログは、次の3つのログで処理されます。

1. AEM Javaログ。AEMアプリケーションのJavaログ文をレンダリングします。
1. HTTP要求ログ。HTTP要求とAEMが提供する応答に関する情報をログに記録します。
1. HTTPアクセスログ。要約された情報とAEMが提供するHTTP要求をログに記録します。

> [!NOTE]
> 
> 公開層のDispatcherキャッシュまたはアップストリームCDNから提供されるHTTP要求は、これらのログに反映されません。

## AEM Javaログ {#aem-java-logging}

AEMは、Cloud Serviceのログ文にアクセスできます。 AEM用アプリケーションの開発者は、次のログレベルで、一般的なJavaログのベストプラクティス、カスタムコードの実行に関連する文のログ記録に従う必要があります。

<table>
<tr>
<td>
<b>AEM環境</b></td>
<td>
<b>ログレベル</b></td>
<td>
<b>説明</b></td>
<td>
<b>ログ文の可用性</b></td>
</tr>
<tr>
<td>
開発</td>
<td>
DEBUG</td>
<td>
アプリケーションで発生している操作について説明します。<br>
DEBUGログがアクティブな場合、発生したアクティビティと処理に影響を与える主要パラメータの明確な内容を提供する文がログに記録されます。</td>
<td>
<ul>
<li> ローカル開発</li>
<li>開発</li>
</ul></td>
</tr>
<tr>
<td>
ステージ</td>
<td>
WARN</td>
<td>
エラーになる可能性のある条件を説明します。<br>
WARNログがアクティブな場合は、最適化に近づいている条件を示す文のみがログに記録されます。</td>
<td>
<ul>
<li> ローカル開発</li>
<li>開発</li>
<li>ステージ</li>
</ul></td>
</tr>
<tr>
<td>
実稼動</td>
<td>
ERROR</td>
<td>
エラーを示す条件と解決する必要がある状態を説明します。<br>
ERRORログがアクティブな場合は、エラーを示す文のみがログに記録されます。 ERRORログ文は、重大な問題を示しており、できるだけ早く解決する必要があります。</td>
<td>
<ul>
<li> ローカル開発</li>
<li>開発</li>
<li>ステージ</li>
<li>実稼動</li>
</ul></td>
</tr>
</table>

Javaログでは、他の複数レベルのログ精度をサポートしていますが、AEMでは、上記の3つのレベルを使用することをCloud Serviceにお勧めします。

AEMログレベルは、OSGi設定を介して環境の種類ごとに設定され、OSGi設定はGitにコミットされ、Cloud Managerを介してAEMにCloud Serviceとしてデプロイされます。 このため、ログレベルの設定を更新した環境を再デプロイする必要なく、AEM経由で利用可能なログを最適なログレベルで確実に使用できるように、ログ文の一貫性とCloud Serviceタイプの既知を保つことをお勧めします。

### ログ形式 {#log-format}

**ログ出力の例**

```
22.06.2020 18:33:30.120 [cm-p12345-e6789-aem-author-86657cbb55-xrnzq] *ERROR* [qtp501076283-1809] io.prometheus.client.dropwizard.DropwizardExports Failed to get value from Gauge
22.06.2020 18:33:30.229 [cm-p12345-e6789-aem-author-86657cbb55-xrnzq] *INFO* [qtp501076283-1805] org.apache.sling.auth.core.impl.SlingAuthenticator getAnonymousResolver: Anonymous access not allowed by configuration - requesting credentials
22.06.2020 18:33:30.370 [cm-p12345-e6789-aem-author-86657cbb55-xrnzq] *INFO* [73.91.59.34 [1592850810364] GET /libs/granite/core/content/login.html HTTP/1.1] org.apache.sling.i18n.impl.JcrResourceBundle Finished loading 0 entries for 'en_US' (basename: <none>) in 4ms
22.06.2020 18:33:30.372 [cm-p12345-e6789-aem-author-86657cbb55-xrnzq] *INFO* [FelixLogListener] org.apache.sling.i18n Service [5126, [java.util.ResourceBundle]] ServiceEvent REGISTERED
22.06.2020 18:33:30.372 [cm-p12345-e6789-aem-author-86657cbb55-xrnzq] *WARN* [73.91.59.34 [1592850810364] GET /libs/granite/core/content/login.html HTTP/1.1] libs.granite.core.components.login.login$jsp j_reason param value 'unknown' cannot be mapped to a valid reason message: ignoring
```

<table>
<tbody>
<tr>
<td>日時</td>
<td>29.04.2020 21:50:13.398</td>
</tr>
<tr>
<td>Cloud ServiceノードIDとしてのAEM</td>
<td>[cm-p1234-e5678-aem-author-59555cb5b8-q7l9s]</td>
</tr>
<tr>
<td>ログレベル</td>
<td>DEBUG</td>
</tr>
<tr>
<td>ねじ</td>
<td>qtp2130572036-1472</td>
</tr>
<tr>
<td>Javaクラス</td>
<td>com.example.approval.workflow.impl.CustomApprovalWorkflow</td>
</tr>
<tr>
<td>ログメッセージ</td>
<td>承認者が指定されていません。デフォルトは[ Creative Approversユーザーグループ]です。</td>
</tr>
</tbody>
</table>

### 設定ロガー {#configuration-loggers}

AEM JavaログはOSGi設定として定義されているので、ターゲット固有のAEMは実行モードのフォルダーを使用するCloud Service環境ーとして使用できます。

Sling LogManagerファクトリのOSGi設定を使用して、カスタムJavaパッケージのJavaログを設定します。 次の2つの設定プロパティがサポートされています。

| OSGi設定プロパティ | 説明 |
|---|---|
| org.apache.sling.commons.log.names | ログ文を収集するJavaパッケージです。 |
| org.apache.sling.commons.log.level | Javaパッケージをログに記録するログレベルです（org.apache.sling.commons.log.namesで指定）。 |

その他のLogManager OSGi設定プロパティを変更すると、AEMでCloud Serviceとしての可用性の問題が発生する場合があります。

3つのAEMで推奨されるログの設定（プレースホルダーJavaパッケージのを使用）の例を次に示します。こ `com.example`の場合、Cloud Service環境タイプとして使用されます。

### 開発 {#development}

/apps/my-app/config/org.apache.sling.commons.log.LogManager.factory.config-example.cfg.json

```
{
    "org.apache.sling.commons.log.names": ["com.example"],
    "org.apache.sling.commons.log.level": "debug"
}
```

### ステージ {#stage}

/apps/my-app/config.stage/org.apache.sling.commons.log.LogManager.factory.config-example.cfg.json

```
{
    "org.apache.sling.commons.log.names": ["com.example"],
    "org.apache.sling.commons.log.level": "warn"
}
```

### 実稼動 {#productiomn}

/apps/my-app/config.prod/org.apache.sling.commons.log.LogManager.factory.config-example.cfg.json

```
{
    "org.apache.sling.commons.log.names": ["com.example"],
    "org.apache.sling.commons.log.level": "error"
}
```

## AEM HTTP要求ログ {#aem-http-request-logging}

AEMは、Cloud ServiceのHTTPリクエストログとして、AEMに対して行われたHTTPリクエストと、そのHTTPレスポンスに関する情報を時系列で提供します。 このログは、AEMに対して行われるHTTP要求と、それらの要求が処理され応答される順序を理解するのに役立ちます。

このログを理解するための鍵は、HTTPリクエストと応答のペアを、括弧内の数値で示されるIDでマッピングすることです。 多くの場合、リクエストと対応する応答には、他のHTTPリクエストと応答がログ内で相互に作用します。

### ログ形式 {#http-request-logging-format}

**サンプルログ**

```
29/Apr/2020:19:14:21 +0000 [137] -> POST /conf/global/settings/dam/adminui-extension/metadataprofile/ HTTP/1.1 [cm-p1234-e5678-aem-author-59555cb5b8-q7l9s]
...
29/Apr/2020:19:14:22 +0000 [139] -> GET /mnt/overlay/dam/gui/content/processingprofilepage/metadataprofiles/editor.html/conf/global/settings/dam/adminui-extension/metadataprofile/main HTTP/1.1 [cm-p1234-e5678-aem-author-59555cb5b8-q7l9s]
...
29/Apr/2020:19:14:21 +0000 [137] <- 201 text/html 111ms [cm-p1234-e5678-aem-author-59555cb5b8-q7l9s]
...
29/Apr/2020:19:14:22 +0000 [139] <- 200 text/html;charset=utf-8 637ms [cm-p1234-e5678-aem-author-59555cb5b8-q7l9s]
```

<table>
<tbody>
<tr>
<td>日時</td>
<td>29/Apr/2020:19:14:21 +0000</td>
</tr>
<tr>
<td>リクエストと応答のペアID</td>
<td><code>[137]</code></td>
</tr>
<tr>
<td>HTTP メソッド</td>
<td>POST</td>
</tr>
<tr>
<td>URL</td>
<td>/conf/global/settings/dam/adminui-extension/metadataprofile/</td>
</tr>
<tr>
<td>プロトコル</td>
<td>HTTP/1.1
</td>
</tr>
<tr>
<td>Cloud ServiceノードIDとしてのAEM</td>
<td>[cm-p1234-e5678-aem-author-59555cb5b8-q7l9s]</td>
</tr>
</tbody>
</table>

### ログの設定 {#configuring-the-log}

AEM HTTP要求ログは、AEMでCloud Serviceとして設定できません。

## AEM HTTPアクセスログ {#aem-http-access-logging}

AEMのCloud ServiceHTTPアクセスログは、HTTPリクエストを時間順に表示します。 各ログエントリは、AEMにアクセスするHTTP要求を表します。

このログは、AEMに対して行われているHTTP要求が何であるか、それに伴うHTTP応答ステータスコードを調べて成功した場合、およびHTTP要求が完了するまでの時間をすばやく把握するのに役立ちます。 このログは、ユーザーがログエントリをフィルタリングして、特定のユーザーのアクティビティをデバッグする場合にも役立ちます。

### ログ形式 {#access-log-format}

**例**

```
cm-p1234-e26813-aem-author-59555cb5b8-8kgr2 - example@adobe.com 30/Apr/2020:17:37:14 +0000  "GET /libs/granite/ui/references/clientlibs/references.lc-5188e85840c529149e6cd29d94e74ad5-lc.min.css HTTP/1.1" 200 1141 "https://author-p10711-e26813.adobeaemcloud.com/mnt/overlay/dam/gui/content/assets/metadataeditor.external.html?item=/content/dam/en/images/example.jpeg&_charset_=utf8" "Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_4) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/81.0.4044.122 Safari/537.36"
cm-p1234-e26813-aem-author-59555cb5b8-8kgr2 - example@adobe.com 30/Apr/2020:17:37:14 +0000  "GET /libs/dam/gui/coral/components/admin/customthumb/clientlibs.lc-60e4443805c37afa0c74b674b141f1df-lc.min.css HTTP/1.1" 200 809 "https://author-p10711-e26813.adobeaemcloud.com/mnt/overlay/dam/gui/content/assets/metadataeditor.external.html?item=/content/dam/en/images/example.jpeg&_charset_=utf8" "Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_4) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/81.0.4044.122 Safari/537.36"
cm-p1234-e26813-aem-author-59555cb5b8-8kgr2 - example@adobe.com 30/Apr/2020:17:37:14 +0000  "GET /libs/dam/gui/coral/components/admin/metadataeditor/clientlibs/metadataeditor.lc-4a2226d8232f8b7ab27d24820b9ddd64-lc.min.js HTTP/1.1" 200 7965 "https://author-p10711-e26813.adobeaemcloud.com/mnt/overlay/dam/gui/content/assets/metadataeditor.external.html?item=/content/dam/en/images/example.jpeg&_charset_=utf8" "Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_4) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/81.0.4044.122 Safari/537.36"
```

<table>
<tbody>
<tr>
<td>Cloud ServiceノードIDとしてのAEM</td>
<td>cm-p1235-e2644-aem-author-5955cb5b8-8kgr2</td>
</tr>
<tr>
<td>クライアントのIPアドレス</td>
<td>-</td>
</tr>
<tr>
<td>User</td>
<td>myuser@adobe.com</td>
</tr>
<tr>
<td>日時</td>
<td>30/Apr/2020:17:37:14 +0000</td>
</tr>
<tr>
<td>HTTPメソッド</td>
<td>GET</td>
</tr>
<tr>
<td>URL</td>
<td>/libs/granite/ui/references/clientlibs/references.lc-5188e85840c529149e6cd29d94e74ad5-lc.min.css</td>
</tr>
<tr>
<td>プロトコル</td>
<td>HTTP/1.1</td>
</tr>
<tr>
<td>HTTP応答ステータス</td>
<td>200</td>
</tr>
<tr>
<td>HTTP要求時間（ミリ秒）</td>
<td>1141</td>
</tr>
<tr>
<td>リファラー</td>
<td><code>"https://author-p1234-e4444.adobeaemcloud.com/mnt/overlay/dam/gui/content/assets/metadataeditor.external.html?item=/content/dam/wknd/en/adventures/surf-camp-in-costa-rica/adobestock_266405335.jpeg&_charset_=utf8"</code></td>
</tr>
<tr>
<td>ユーザーエージェント</td>
<td>"Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_4)AppleWebKit/537.36 （KHTML、Geckoなど） Chrome/81.0.4044.122 Safari/537.36"</td>
</tr>
</tbody>
</table>

### HTTPアクセスログの設定 {#configuring-the-http-access-log}

HTTPアクセスログは、AEMではCloud Serviceとして設定できません。

## Apache Web Server and Dispatcher Logging {#apache-web-server-and-dispatcher-logging}

AEMは、Cloud Serviceとして、「発行」上のApache Webサーバーとディスパッチャーレイヤーの3つのログを提供します。

* Apache HTTPD Webサーバーアクセスログ
* Apache HTTPD Webサーバーエラーログ
* Dispatcherログ

これらのログは発行層でのみ使用できます。

この一連のログは、AEMアプリケーションに到達する前の要求発行層として、AEMに対するHTTP要求に対するインサイトを提供します。 これは重要です。理想的には、発行層サーバーへのほとんどのHTTP要求は、Apache HTTPD WebサーバーおよびAEMDispatcherによってキャッシュされたコンテンツによって処理され、AEMアプリケーション自体には届かないことを理解します。 したがって、AEM Java、要求、またはアクセスのログには、これらの要求に対するログ文はありません。

### Apache HTTPD Webサーバーアクセスログ {#apache-httpd-web-server-access-log}

Apache HTTP Web Serverアクセスログは、公開層のWebサーバー/Dispatcherに到達する各HTTPリクエストの文を提供します。 アップストリームCDNから提供される要求は、これらのログには反映されません。

エラーログの形式に関する情報については、 [公式のApacheドキュメントを参照してください](https://httpd.apache.org/docs/2.4/logs.html#accesslog)。

**ログ形式**

<!--blank until prod build finishes-->

**例**

```
cm-p1234-e5678-aem-publish-b86c6b466-qpfvp - - 17/Jul/2020:09:14:41 +0000  "GET /etc.clientlibs/wknd/clientlibs/clientlib-site/resources/images/favicons/favicon-32.png HTTP/1.1" 200 715 "-" "Mozilla/5.0 (Macintosh; Intel Mac OS X 10.15; rv:78.0) Gecko/20100101 Firefox/78.0"
cm-p1234-e5678-aem-publish-b86c6b466-qpfvp - - 17/Jul/2020:09:14:41 +0000  "GET /etc.clientlibs/wknd/clientlibs/clientlib-site/resources/images/favicons/favicon-512.png HTTP/1.1" 200 9631 "-" "Mozilla/5.0 (Macintosh; Intel Mac OS X 10.15; rv:78.0) Gecko/20100101 Firefox/78.0"
cm-p1234-e5678-aem-publish-b86c6b466-qpfvp - - 17/Jul/2020:09:14:42 +0000  "GET /etc.clientlibs/wknd/clientlibs/clientlib-site/resources/images/country-flags/US.svg HTTP/1.1" 200 810 "https://publish-p6902-e30226.adobeaemcloud.com/content/wknd/us/en.html" "Mozilla/5.0 (Macintosh; Intel Mac OS X 10.15; rv:78.0) Gecko/20100101 Firefox/78.0"
```

### Apache HTTPD Webサーバーアクセスログの設定 {#configuring-the-apache-httpd-webs-server-access-log}

このログは、AEMではCloud Serviceとして設定できません。

## Apache HTTPD Webサーバーのエラーログ {#apache-httpd-web-server-error-log}

Apache HTTP Web Serverエラーログには、公開層のWebサーバー/Dispatcherの各エラーに関する文が記載されています。

エラーログの形式に関する情報については、 [公式のApacheドキュメントを参照してください](https://httpd.apache.org/docs/2.4/logs.html#errorlog)。

**ログ形式**

<!--placeholder-->

**例**

```
Fri Jul 17 02:19:48.093820 2020 [mpm_worker:notice] [pid 1:tid 140272153361288] [cm-p1234-e30226-aem-publish-b86c6b466-b9427] AH00292: Apache/2.4.43 (Unix) Communique/4.3.4-20200424 mod_qos/11.63 configured -- resuming normal operations
Fri Jul 17 02:19:48.093874 2020 [core:notice] [pid 1:tid 140272153361288] [cm-p1234-e30226-aem-publish-b86c6b466-b9427] AH00094: Command line: 'httpd -d /etc/httpd -f /etc/httpd/conf/httpd.conf -D FOREGROUND -D ENVIRONMENT_PROD'
Fri Jul 17 02:29:34.517189 2020 [mpm_worker:notice] [pid 1:tid 140293638175624] [cm-p1234-e30226-aem-publish-b496f64bf-5vckp] AH00295: caught SIGTERM, shutting down
```

### Apache HTTPD Webサーバーエラーログの設定 {#configuring-the-apache-httpd-web-server-error-log}

mod_rewriteログレベルは、ファイル内の変数REWRITE_LOG_LEVELによって定義され `conf.d/variables/global.var`ます。

Error、Warn、Info、Debug、およびTrace1 ～ Trace8に設定でき、デフォルト値はWarnです。 RewriteRulesをデバッグするには、ログレベルをTrace2に上げることをお勧めします。

詳細は、 [mod_rewriteモジュールのドキュメント](https://httpd.apache.org/docs/current/mod/mod_rewrite.html#logging) を参照してください。

環境ごとのログレベルを設定するには、次に示すように、global.varファイル内の適切な条件付きブランチを使用します。

```
Define REWRITE_LOG_LEVEL Debug
  
<IfDefine ENVIRONMENT_STAGE>
  ...
  Define REWRITE_LOG_LEVEL Warn
  ...
</IfDefine>
<IfDefine ENVIRONMENT_PROD>
  ...
  Define REWRITE_LOG_LEVEL Error
  ...
</IfDefine>
```

## Dispatcherログ {#dispatcher-log}

<!--de completat-->

**例**

```
[17/Jul/2020:23:48:06 +0000] [I] [cm-p12904-e25628-aem-publish-6c5f7c9dbd-mzcvr] "GET /content/wknd/us/en/adventures.html" - 475ms [publishfarm/0] [action miss] "publish-p12904-e25628.adobeaemcloud.com"
[17/Jul/2020:23:48:07 +0000] [I] [cm-p12904-e25628-aem-publish-6c5f7c9dbd-mzcvr] "GET /content/wknd/us/en/adventures/climbing-new-zealand/_jcr_content/root/responsivegrid/carousel/item_1571266094599.coreimg.jpeg/1473680817282/sport-climbing.jpeg" 302 10ms [publishfarm/0] [action none] "publish-p12904-e25628.adobeaemcloud.com"
[17/Jul/2020:23:48:07 +0000] [I] [cm-p12904-e25628-aem-publish-6c5f7c9dbd-mzcvr] "GET /content/wknd/us/en/adventures/ski-touring-mont-blanc/_jcr_content/root/responsivegrid/carousel/item_1571168419252.coreimg.jpeg/1572047288089/adobestock-238230356.jpeg" 302 11ms [publishfarm/0] [action none] "publish-p12904-e25628.adobeaemcloud.com"
```

### ログ形式 {#dispatcher-log-format}

### Dispatcherエラーログの設定 {#configuring-the-dispatcher-error-log}

ディスパッチャーログレベルは、ファイル内の変数DISP_LOG_LEVELによって定義され `conf.d/variables/global.var`ます。

Error、Warn、Info、Debug、およびTrace1に設定でき、デフォルト値はWarnです。

Dispatcherログでは、他の複数レベルのログ精度をサポートしていますが、AEMは、Cloud Serviceとして以下に示すレベルを使用することをお勧めします。

環境ごとのログレベルを設定するには、以下に示すように、 `global.var` ファイル内で適切な条件付き分岐を使用します。

```
Define DISP_LOG_LEVEL Debug
  
<IfDefine ENVIRONMENT_STAGE>
  ...
  Define DISP_LOG_LEVEL Warn
  ...
</IfDefine>
<IfDefine ENVIRONMENT_PROD>
  ...
  Define DISP_LOG_LEVEL Error
  ...
</IfDefine>
```

## ログにアクセスする方法 {#how-to-access-logs}

### クラウド環境 {#cloud-environments}

クラウドサービスのCloud ServiceログとしてAEMにアクセスするには、Cloud Managerインターフェイスを使用してダウンロードするか、AdobeI/Oコマンドラインインターフェイスを使用してコマンドラインでログをテーリングします。 詳しくは、 [Cloud Managerのログに関するドキュメントを参照してください](/help/implementing/cloud-manager/manage-logs.md)。

### ローカルSDK {#local-sdk}

AEM asCloud ServiceSDKは、ローカル開発をサポートするログファイルを提供します。

AEMログはフォルダー内にあり、次のログを表示でき `crx-quickstart/logs`ます。

* AEM Javaログ： `error.log`
* AEM HTTP要求ログ： `request.log`
* AEM HTTPアクセスログ： `access.log`

ディスパッチャーを含むApacheレイヤーログは、Dispatcherを保持するDockerコンテナにあります。 Dispatcherの開始方法については、 [Dispatcherのドキュメント](https://docs.adobe.com/content/help/en/experience-manager-cloud-service/implementing/content-delivery/disp-overview.html) を参照してください。

ログを取得するには：

1. コマンドラインで、コンテナのリスト `docker ps` を入力します。
1. コンテナにログインするには、「`docker exec -it <container> /bin/sh`」と入力します。ここで、 `<container>` は前の手順のディスパッチャーコンテナIDです。
1. 次の下のキャッシュルートに移動します。 `/mnt/var/www/html`
1. ログは下にある `/etc/httpd/logs`
1. Inspect: XYZフォルダーの下でアクセスでき、次のログを表示できます。
   * Apache HTTPD Webサーバーアクセスログ — `httpd_access.log`
   * Apache HTTPD Webサーバーのエラーログ — `httpd_error.log`
   * Dispatcherログ — `dispatcher.log`

ログも端末出力に直接印刷されます。 ほとんどの場合、これらのログはDEBUGです。これは、Dockerの実行時にDebugレベルをパラメーターとして渡すことで実現できます。 次に例を示します。

`DISP_LOG_LEVEL=Debug ./bin/docker_run.sh out docker.for.mac.localhost:4503 8080`

## 実稼働環境とステージのデバッグ {#debugging-production-and-stage}

例外的な状況では、ステージまたは実稼働環境でログをより細かく記録するには、ログレベルを変更する必要があります。

これは可能ですが、Gitの設定ファイルのログレベルに対する警告とエラーからデバッグへの変更が必要です。また、これらの設定の変更を環境に登録するCloud ServiceとしてAEMへの展開を実行します。

Debugによって書き込まれるログ文のトラフィックと量に応じて、環境に悪影響を与える可能性があるので、StageとProductionのデバッグレベルを変更することをお勧めします。

* 慎重に行い、絶対に必要な場合にのみ行う
* 適切なレベルに戻し、可能な限り早く再デプロイ

## Splunkログ {#splunk-logs}

Splunkアカウントを持っているお客様は、カスタマーサポートチケットを介して、AEMCloud Serviceログを適切なインデックスに転送するようにリクエストする場合があります。 ログデータは、Cloud Managerのログのダウンロードで利用できるものと同じですが、Splunk製品のクエリ機能を利用すると便利です。

Splunkに送信されるログに関連付けられるネットワーク帯域幅は、お客様のネットワークI/O使用の一部と見なされます。

### Splunk転送の有効化 {#enabling-splunk-forwarding}

サポートの要請に応じて、お客様は次のことを示す必要があります。

* Splunkのホスト
* スプランク指数
* スプランク港
* Splunk HECトークン。 詳しくは、[こちらのページ](https://docs.splunk.com/Documentation/Splunk/8.0.4/Data/HECExamples)を参照してください。

上記のプロパティは、関連するプログラム/環境タイプの組み合わせごとに指定する必要があります。  例えば、開発、ステージング、実稼動の各環境を希望する場合は、次に示す3組の情報を提供する必要があります。

> [!NOTE]
>
> サンドボックスプログラム環境のSplunk転送はサポートされていません。

以下に、サンプルのカスタマーサポートの要請を示します。

プログラム123、実稼働環境

* Splunkホスト： `splunk-hec-ext.acme.com`
* Splunkインデックス： acme_123prod（お客様は任意の命名規則を選択できます）
* Splunkポート： 443
* HECトークンの分割： ABC123

プログラム123、ステージ環境

* Splunkホスト： `splunk-hec-ext.acme.com`
* Splunkインデックス： acme_123stage
* Splunkポート： 443
* HECトークンの分割： ABC123

プログラム123、開発エンヴ

* Splunkホスト： `splunk-hec-ext.acme.com`
* Splunkインデックス： acme_123dev
* Splunkポート： 443
* HECトークンの分割： ABC123

各環境に同じSplunkインデックスを使用する場合は十分です。この場合、dev、stage、prodの値に基づいて `aem_env_type` フィールドを区別するために使用できます。 複数の開発環境がある場合は、この `aem_env_id` フィールドも使用できます。 一部の組織では、関連するインデックスで、少数のSplunk環境へのアクセスが制限されている場合、本番ユーザーのログに対して別のインデックスを選択できます。

ログエントリの例を次に示します。

```
aem_env_id: 1242
aem_env_type: dev
aem_program_id: 12314
aem_tier: author
file_path: /var/log/aem/error.log
host: 172.34.200.12 
level: INFO
msg: [FelixLogListener] com.adobe.granite.repository Service [5091, [org.apache.jackrabbit.oak.api.jmx.SessionMBean]] ServiceEvent REGISTERED
orig_time: 16.07.2020 08:35:32.346
pod_name: aemloggingall-aem-author-77797d55d4-74zvt
splunk_customer: true
```
