---
title: ログ
description: 一元的なログサービスのグローバルパラメーターの設定、個々のサービスに特有の設定、またはデータのログ記録の要求をおこなう方法を学習します。
translation-type: tm+mt
source-git-commit: 86103b40e931ec00e0c15e9dbcbdf396c8eb05c9
workflow-type: tm+mt
source-wordcount: '2212'
ht-degree: 100%

---


# ログ {#logging}

AEM as a Cloud Service は、カスタムコードを含めて、顧客ベースに独自のエクスペリエンスを作成する顧客のためのプラットフォームです。このことを念頭に置いた上で、ログは、ローカル開発およびクラウド環境、特に AEM as a Cloud Service の開発環境をデバッグし、実行されるコードを理解するための重要な機能です。

AEM のログとログレベルは、AEM プロジェクトの一部として Git に保存され、AEM プロジェクトの一部として Cloud Manager を介してデプロイされる構成ファイルで管理されます。AEM as a Cloud Service のログは、次の 2 つの論理セットに分割できます。

* AEM ログ。AEM アプリケーションレベルでログを実行します。
* Apache HTTPD Web サーバー／Dispatcher ログ。パブリッシュ層で Web サーバーと Dispatcher のログを実行します。

## AEM ログ {#aem-loggin}

AEM アプリケーションレベルでのログは、次の 3 つのログで処理されます。

1. AEM Java ログ。AEM アプリケーションの Java ログステートメントをレンダリングします。
1. HTTP リクエストログ。HTTP リクエストと AEM が提供する応答に関する情報をログに記録します。
1. HTTP アクセスログ。AEM が提供する要約された情報と HTTP リクエストをログに記録します。

>[!NOTE]
>
>パブリッシュ層の Dispatcher キャッシュまたはアップストリーム CDN から提供される HTTP リクエストは、これらのログに反映されません。

## AEM Java ログ {#aem-java-logging}

AEM as a Cloud Service は Java ログステートメントにアクセスできます。AEM 向けアプリケーションの開発者は、次のログレベルで、一般的な Java ログのベストプラクティス、カスタムコードの実行に関連するステートメントのログ記録に従う必要があります。

<table>
<tr>
<td>
<b>AEM 環境</b></td>
<td>
<b>ログレベル</b></td>
<td>
<b>説明</b></td>
<td>
<b>ログステートメントの可用性</b></td>
</tr>
<tr>
<td>
開発</td>
<td>
DEBUG</td>
<td>
アプリケーションでの出来事について説明します。<br>
DEBUG ログがアクティブになっている場合、発生したアクティビティと処理に影響を与える主要パラメーターの明確な内容を提供するステートメントがログに記録されます。</td>
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
WARN ログがアクティブになっている場合は、次善となりつつある条件を示すステートメントのみがログに記録されます。</td>
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
ERROR ログがアクティブになっている場合は、エラーを示すステートメントのみがログに記録されます。ERROR ログステートメントは、重大な問題を示しており、できるだけ早く解決する必要があります。</td>
<td>
<ul>
<li> ローカル開発</li>
<li>開発</li>
<li>ステージ</li>
<li>実稼動</li>
</ul></td>
</tr>
</table>

Java ログはその他にも複数レベルのログ精度をサポートしていますが、AEM as a Cloud Service では、上記の 3 つのレベルを使用することをお勧めします。

AEM ログレベルは、OSGi 設定を介して環境の種類ごとに設定され、次に Git にコミットされて、Cloud Manager を介して AEM as a Cloud Service にデプロイされます。そのため、ログレベルの設定を更新した環境を再デプロイせずに、AEM as a Cloud Service 経由で利用可能なログを最適なログレベルで確実に使用できるように、ログステートメントの一貫性と既知の環境の種類を保つことをお勧めします。

**ログ出力の例**

```
22.06.2020 18:33:30.120 [cm-p12345-e6789-aem-author-86657cbb55-xrnzq] *ERROR* [qtp501076283-1809] io.prometheus.client.dropwizard.DropwizardExports Failed to get value from Gauge
22.06.2020 18:33:30.229 [cm-p12345-e6789-aem-author-86657cbb55-xrnzq] *INFO* [qtp501076283-1805] org.apache.sling.auth.core.impl.SlingAuthenticator getAnonymousResolver: Anonymous access not allowed by configuration - requesting credentials
22.06.2020 18:33:30.370 [cm-p12345-e6789-aem-author-86657cbb55-xrnzq] *INFO* [73.91.59.34 [1592850810364] GET /libs/granite/core/content/login.html HTTP/1.1] org.apache.sling.i18n.impl.JcrResourceBundle Finished loading 0 entries for 'en_US' (basename: <none>) in 4ms
22.06.2020 18:33:30.372 [cm-p12345-e6789-aem-author-86657cbb55-xrnzq] *INFO* [FelixLogListener] org.apache.sling.i18n Service [5126, [java.util.ResourceBundle]] ServiceEvent REGISTERED
22.06.2020 18:33:30.372 [cm-p12345-e6789-aem-author-86657cbb55-xrnzq] *WARN* [73.91.59.34 [1592850810364] GET /libs/granite/core/content/login.html HTTP/1.1] libs.granite.core.components.login.login$jsp j_reason param value 'unknown' cannot be mapped to a valid reason message: ignoring
```

**ログ形式**

<table>
<tbody>
<tr>
<td>日時</td>
<td>29.04.2020 21:50:13.398</td>
</tr>
<tr>
<td>AEM as a Cloud Service のノード ID</td>
<td>[cm-p1234-e5678-aem-author-59555cb5b8-q7l9s]</td>
</tr>
<tr>
<td>ログレベル</td>
<td>DEBUG</td>
</tr>
<tr>
<td>スレッド</td>
<td>qtp2130572036-1472</td>
</tr>
<tr>
<td>Java クラス</td>
<td>com.example.approval.workflow.impl.CustomApprovalWorkflow</td>
</tr>
<tr>
<td>ログメッセージ</td>
<td>No specified approver, defaulting to [ Creative Approvers user group ]</td>
</tr>
</tbody>
</table>

### ログ設定 {#configuration-loggers}

AEM Java ログは OSGi 設定として定義されるので、ターゲット固有の AEM as a Cloud Service 環境は実行モードのフォルダーを使用します。

Sling LogManager ファクトリの OSGi 設定を使用して、カスタム Java パッケージの Java ログを設定します。次の 2 つの設定プロパティがサポートされています。

| OSGi 設定プロパティ | 説明 |
|---|---|
| org.apache.sling.commons.log.names | ログステートメントを収集する Java パッケージです。 |
| org.apache.sling.commons.log.level | Java パッケージをログに記録するログレベルです（org.apache.sling.commons.log.names で指定）。 |

その他の LogManager OSGi 設定プロパティを変更すると、AEM as a Cloud Service での可用性の問題が発生する場合があります。

3 つの AEM as a Cloud Service 環境で推奨されるログの設定（Java パッケージ `com.example` のプレースホルダーを使用）の例を次に示します。

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

## AEM HTTP リクエストログ {#aem-http-request-logging}

AEM as a Cloud Service の HTTP リクエストログは、AEM に対しておこなわれた HTTP リクエストと、それに対する HTTP レスポンスに関する情報を時系列で提供します。このログは、AEM に対しておこなわれる HTTP リクエストと、それらの要求が処理され応答される順序を理解するのに役立ちます。

このログを理解するための鍵は、HTTP リクエストとレスポンスのペアを、括弧内の数値で示される ID でマッピングすることです。多くの場合、リクエストと対応するレスポンスには、その他の HTTP リクエストとレスポンスがログ内に差し込まれています。

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

**ログ形式**

<table>
<tbody>
<tr>
<td>日時</td>
<td>29/Apr/2020:19:14:21 +0000</td>
</tr>
<tr>
<td>リクエストとレスポンスのペア ID</td>
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
<td>AEM as a Cloud Service のノード ID</td>
<td>[cm-p1234-e5678-aem-author-59555cb5b8-q7l9s]</td>
</tr>
</tbody>
</table>

### ログの設定 {#configuring-the-log}

AEM HTTP リクエストログは、AEM as a Cloud Service では設定できません。

## AEM HTTP アクセスログ {#aem-http-access-logging}

AEM as a Cloud Service の HTTP アクセスログは、HTTP リクエストを時系列に表示します。各ログエントリは、AEM にアクセスする HTTP リクエストを表します。

このログは、AEM にどのような HTTP リクエストがおこなわれているか、それに対応する HTTP レスポンスのステータスコードを調べて、リクエストが成功しているか、また HTTP リクエストが完了するまでの時間をすばやく把握するのに役立ちます。このログは、ユーザーでログエントリをフィルタリングして、特定のユーザーのアクティビティをデバッグする場合にも役立ちます。

**ログ出力の例**

```
cm-p1234-e26813-aem-author-59555cb5b8-8kgr2 - example@adobe.com 30/Apr/2020:17:37:14 +0000  "GET /libs/granite/ui/references/clientlibs/references.lc-5188e85840c529149e6cd29d94e74ad5-lc.min.css HTTP/1.1" 200 1141 "https://author-p10711-e26813.adobeaemcloud.com/mnt/overlay/dam/gui/content/assets/metadataeditor.external.html?item=/content/dam/en/images/example.jpeg&_charset_=utf8" "Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_4) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/81.0.4044.122 Safari/537.36"
cm-p1234-e26813-aem-author-59555cb5b8-8kgr2 - example@adobe.com 30/Apr/2020:17:37:14 +0000  "GET /libs/dam/gui/coral/components/admin/customthumb/clientlibs.lc-60e4443805c37afa0c74b674b141f1df-lc.min.css HTTP/1.1" 200 809 "https://author-p10711-e26813.adobeaemcloud.com/mnt/overlay/dam/gui/content/assets/metadataeditor.external.html?item=/content/dam/en/images/example.jpeg&_charset_=utf8" "Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_4) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/81.0.4044.122 Safari/537.36"
cm-p1234-e26813-aem-author-59555cb5b8-8kgr2 - example@adobe.com 30/Apr/2020:17:37:14 +0000  "GET /libs/dam/gui/coral/components/admin/metadataeditor/clientlibs/metadataeditor.lc-4a2226d8232f8b7ab27d24820b9ddd64-lc.min.js HTTP/1.1" 200 7965 "https://author-p10711-e26813.adobeaemcloud.com/mnt/overlay/dam/gui/content/assets/metadataeditor.external.html?item=/content/dam/en/images/example.jpeg&_charset_=utf8" "Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_4) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/81.0.4044.122 Safari/537.36"
```

**ログ形式**

<table>
<tbody>
<tr>
<td>AEM as a Cloud Service のノード ID</td>
<td>cm-p1235-e2644-aem-author-59555cb5b8-8kgr2</td>
</tr>
<tr>
<td>クライアントの IP アドレス</td>
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
<td>HTTP メソッド</td>
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
<td>HTTP レスポンスステータス</td>
<td>200</td>
</tr>
<tr>
<td>HTTP リクエスト時間（ミリ秒）</td>
<td>1141</td>
</tr>
<tr>
<td>リファラー</td>
<td><code>"https://author-p1234-e4444.adobeaemcloud.com/mnt/overlay/dam/gui/content/assets/metadataeditor.external.html?item=/content/dam/wknd/en/adventures/surf-camp-in-costa-rica/adobestock_266405335.jpeg&_charset_=utf8"</code></td>
</tr>
<tr>
<td>ユーザーエージェント</td>
<td>"Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_4) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/81.0.4044.122 Safari/537.36"</td>
</tr>
</tbody>
</table>

### HTTP アクセスログの設定 {#configuring-the-http-access-log}

HTTP アクセスログは、AEM as a Cloud Service では設定できません。

## Apache Web サーバーおよび Dispatcher ログ {#apache-web-server-and-dispatcher-logging}

AEM as a Cloud Service は、パブリッシュ上の Apache Web サーバーと Dispatcher レイヤーに 3 つのログを提供します。

* Apache HTTPD Web サーバーアクセスログ
* Apache HTTPD Web サーバーエラーログ
* Dispatcher ログ

これらのログはパブリッシュ層でのみ使用できます。

これらのログは、AEM アプリケーションに到達する前に、AEM as a Cloud Service のパブリッシュ層に対しておこなわれた HTTP リクエストに関するインサイトを提供します。理想的には、パブリッシュ層サーバーへのほとんどの HTTP リクエストは、Apache HTTPD Web サーバーおよび AEM Dispatcher によってキャッシュされたコンテンツによって処理され、AEM アプリケーション自体には届きません。それを理解することは重要です。したがって、AEM の Java ログ、リクエストログ、アクセスログには、これらのリクエストに対するログステートメントはありません。

### Apache HTTPD Web サーバーアクセスログ {#apache-httpd-web-server-access-log}

Apache HTTP Web Server アクセスログは、パブリッシュ層の Web サーバー／Dispatcher に到達する各 HTTP リクエストのステートメントを提供します。アップストリーム CDN から提供されるリクエストは、これらのログには反映されません。

エラーログの形式に関する情報については、[公式の Apache ドキュメント](https://httpd.apache.org/docs/2.4/logs.html#accesslog)を参照してください。

**ログ出力の例**

```
cm-p1234-e5678-aem-publish-b86c6b466-qpfvp - - 17/Jul/2020:09:14:41 +0000  "GET /etc.clientlibs/wknd/clientlibs/clientlib-site/resources/images/favicons/favicon-32.png HTTP/1.1" 200 715 "-" "Mozilla/5.0 (Macintosh; Intel Mac OS X 10.15; rv:78.0) Gecko/20100101 Firefox/78.0"
cm-p1234-e5678-aem-publish-b86c6b466-qpfvp - - 17/Jul/2020:09:14:41 +0000  "GET /etc.clientlibs/wknd/clientlibs/clientlib-site/resources/images/favicons/favicon-512.png HTTP/1.1" 200 9631 "-" "Mozilla/5.0 (Macintosh; Intel Mac OS X 10.15; rv:78.0) Gecko/20100101 Firefox/78.0"
cm-p1234-e5678-aem-publish-b86c6b466-qpfvp - - 17/Jul/2020:09:14:42 +0000  "GET /etc.clientlibs/wknd/clientlibs/clientlib-site/resources/images/country-flags/US.svg HTTP/1.1" 200 810 "https://publish-p6902-e30226.adobeaemcloud.com/content/wknd/us/en.html" "Mozilla/5.0 (Macintosh; Intel Mac OS X 10.15; rv:78.0) Gecko/20100101 Firefox/78.0"
```

**ログ形式**

<table>
<tbody>
<tr>
<td>AEM as a Cloud Service のノード ID</td>
<td>cm-p1234-e26813-aem-publish-5c787687c-lqlxr</td>
</tr>
<tr>
<td>クライアントの IP アドレス</td>
<td>-</td>
</tr>
<tr>
<td>User</td>
<td>-</td>
</tr>
<tr>
<td>日時</td>
<td>01/May/2020:00:09:46 +0000</td>
</tr>
<tr>
<td>HTTP メソッド</td>
<td>GET</td>
</tr>
<tr>
<td>URL</td>
<td>/content/example.html</td>
</tr>
<tr>
<td>プロトコル</td>
<td>HTTP/1.1</td>
</tr>
<tr>
<td>HTTP レスポンスステータス</td>
<td>200</td>
</tr>
<tr>
<td>サイズ</td>
<td>310</td>
</tr>
<tr>
<td>リファラー</td>
<td>-</td>
</tr>
<tr>
<td>ユーザーエージェント</td>
<td>"Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_4) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/81.0.4044.122 Safari/537.36"</td>
</tr>
</tbody>
</table>

### Apache HTTPD Web サーバーアクセスログの設定 {#configuring-the-apache-httpd-webs-server-access-log}

このログは、AEM as a Cloud Service では設定できません。

## Apache HTTPD Web サーバーエラーログ {#apache-httpd-web-server-error-log}

Apache HTTP Web サーバーエラーログには、パブリッシュ層の Web サーバー／Dispatcher の各エラーに関するステートメントを提供します。

エラーログの形式に関する情報については、[公式の Apache ドキュメント](https://httpd.apache.org/docs/2.4/logs.html#errorlog)を参照してください。

**ログ出力の例**

```
Fri Jul 17 02:19:48.093820 2020 [mpm_worker:notice] [pid 1:tid 140272153361288] [cm-p1234-e30226-aem-publish-b86c6b466-b9427] AH00292: Apache/2.4.43 (Unix) Communique/4.3.4-20200424 mod_qos/11.63 configured -- resuming normal operations
Fri Jul 17 02:19:48.093874 2020 [core:notice] [pid 1:tid 140272153361288] [cm-p1234-e30226-aem-publish-b86c6b466-b9427] AH00094: Command line: 'httpd -d /etc/httpd -f /etc/httpd/conf/httpd.conf -D FOREGROUND -D ENVIRONMENT_PROD'
Fri Jul 17 02:29:34.517189 2020 [mpm_worker:notice] [pid 1:tid 140293638175624] [cm-p1234-e30226-aem-publish-b496f64bf-5vckp] AH00295: caught SIGTERM, shutting down
```

**ログ形式**

<table>
<tbody>
<tr>
<td>日時</td>
<td>Fri Jul 17 02:16:42.608913 2020</td>
</tr>
<tr>
<td>イベントレベル</td>
<td>[mpm_worker:notice]</td>
</tr>
<tr>
<td>プロセス ID</td>
<td>[pid 1:tid 140715149343624]</td>
</tr>
<tr>
<td>ポッド名</td>
<td>[cm-p1234-e56789-aem-publish-b86c6b466-qpfvp]</td>
</tr>
<tr>
<td>メッセージ</td>
<td>AH00094: Command line: 'httpd -d /etc/httpd -f /etc/httpd/conf/httpd.conf -D FOREGROUND -D </td>
</tr>
</tbody>
</table>

### Apache HTTPD Web サーバーエラーログの設定 {#configuring-the-apache-httpd-web-server-error-log}

mod_rewrite ログレベルは、`conf.d/variables/global.var` ファイル内の変数 REWRITE_LOG_LEVEL によって定義されます。

Error、Warn、Info、Debug、および Trace1～Trace8 に設定でき、デフォルト値は Warn です。RewriteRules をデバッグするには、ログレベルを Trace2 に上げることをお勧めします。

詳細は、[mod_rewrite モジュールのドキュメント](https://httpd.apache.org/docs/current/mod/mod_rewrite.html#logging)を参照してください。

環境ごとのログレベルを設定するには、次に示すように、global.var ファイル内で適切な条件付き分岐を使用します。

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

## Dispatcher ログ {#dispatcher-log}

**例**

```
[17/Jul/2020:23:48:06 +0000] [I] [cm-p12904-e25628-aem-publish-6c5f7c9dbd-mzcvr] "GET /content/wknd/us/en/adventures.html" - 475ms [publishfarm/0] [action miss] "publish-p12904-e25628.adobeaemcloud.com"
[17/Jul/2020:23:48:07 +0000] [I] [cm-p12904-e25628-aem-publish-6c5f7c9dbd-mzcvr] "GET /content/wknd/us/en/adventures/climbing-new-zealand/_jcr_content/root/responsivegrid/carousel/item_1571266094599.coreimg.jpeg/1473680817282/sport-climbing.jpeg" 302 10ms [publishfarm/0] [action none] "publish-p12904-e25628.adobeaemcloud.com"
[17/Jul/2020:23:48:07 +0000] [I] [cm-p12904-e25628-aem-publish-6c5f7c9dbd-mzcvr] "GET /content/wknd/us/en/adventures/ski-touring-mont-blanc/_jcr_content/root/responsivegrid/carousel/item_1571168419252.coreimg.jpeg/1572047288089/adobestock-238230356.jpeg" 302 11ms [publishfarm/0] [action none] "publish-p12904-e25628.adobeaemcloud.com"
```

**ログ形式**

<table>
<tbody>
<tr>
<td>日時</td>
<td>[17/Jul/2020:23:48:16 +0000]</td>
</tr>
<tr>
<td>ポッド名</td>
<td>[cm-p12904-e25628-aem-publish-6c5f7c9dbd-mzcvr]</td>
</tr>
<tr>
<td>プロトコル</td>
<td>GET</td>
</tr>
<tr>
<td>URL</td>
<td>/content/experience-fragments/wknd/language-masters/en/contributors/sofia-sjoeberg/master/_jcr_content/root/responsivegrid/image.coreimg.100.500.jpeg/1572236359031/ayo-ogunseinde-237739.jpeg</td>
</tr>
<tr>
<td>Dispatcher レスポンスステータスコード</td>
<td>/content/experience-fragments/wknd/language-masters/en/contributors/sofia-sjoeberg/master/_jcr_content/root/responsivegrid/image.coreimg.100.500.jpeg/1572236359031/ayo-ogunseinde-237739.jpeg</td>
</tr>
<tr>
<td>デュレーション</td>
<td>1949 ms</td>
</tr>
<tr>
<td>ファーム</td>
<td>[publishfarm/0]</td>
</tr>
<tr>
<td>キャッシュの状態</td>
<td>[action miss]</td>
</tr>
<tr>
<td>ホスト</td>
<td>"publish-p12904-e25628.adobeaemcloud.com"</td>
</tr>
</tbody>
</table>

### Dispatcher エラーログの設定 {#configuring-the-dispatcher-error-log}

Dispatcher ログレベルは、`conf.d/variables/global.var` ファイル内の変数 DISP_LOG_LEVEL によって定義されます。

Error、Warn、Info、Debug、および Trace1 に設定でき、デフォルト値は Warn です。

Dispatcher ログはその他にも複数レベルのログ精度をサポートしていますが、AEM as a Cloud Service では、次のレベルを使用することをお勧めします。

環境ごとのログレベルを設定するには、次に示すように、`global.var` ファイル内で適切な条件付き分岐を使用します。

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

## ログのアクセス方法 {#how-to-access-logs}

### クラウド環境 {#cloud-environments}

Cloud Services の AEM as a Cloud Service のログにアクセスするには、Cloud Manager インターフェイスを使用してダウンロードするか、Adobe I/O コマンドラインインターフェイスを使用してコマンドラインでログに対して tail を実行します。詳しくは、[Cloud Manager のログに関するドキュメント](/help/implementing/cloud-manager/manage-logs.md)を参照してください。

### ローカル SDK {#local-sdk}

AEM as a Cloud Service SDK は、ローカル開発をサポートするログファイルを提供します。

AEM ログは `crx-quickstart/logs` フォルダー内にあり、次のログが参照できます。

* AEM Java ログ： `error.log`
* AEM HTTP リクエストログ： `request.log`
* AEM HTTP アクセスログ： `access.log`

Dispatcher を含む Apache レイヤーログは、Dispatcher を保持する Docker コンテナにあります。Dispatcher の開始方法については、[Dispatcher のドキュメント](https://docs.adobe.com/content/help/ja-JP/experience-manager-cloud-service/implementing/content-delivery/disp-overview.translate.html)を参照してください。

ログを取得するには、以下の手順に従います。

1. コマンドラインで、`docker ps` と入力してコンテナを一覧表示します。
1. コンテナにログインするには、「`docker exec -it <container> /bin/sh`」と入力します。`<container>` は前の手順の Dispatcher コンテナ ID です。
1. `/mnt/var/www/html` 下のキャッシュルートに移動します。
1. ログは `/etc/httpd/logs` 下にあります。
1. ログの調査：XYZ フォルダーにアクセスし、次のログを参照できます。
   * Apache HTTPD Web サーバーアクセスログ - `httpd_access.log`
   * Apache HTTPD Web サーバーエラーログ - `httpd_error.log`
   * Dispatcher ログ - `dispatcher.log`

ログは端末の出力にも直接表示できます。ほとんどの場合、これらのログは DEBUG で出力されるもので、Docker の実行時に Debug レベルをパラメーターとして渡すことで実現できます。次に例を示します。

`DISP_LOG_LEVEL=Debug ./bin/docker_run.sh out docker.for.mac.localhost:4503 8080`

## 実稼動環境とステージ環境のデバッグ {#debugging-production-and-stage}

例外的な状況では、ステージまたは実稼動環境でログレベルを変更して、ログをより細かく記録する必要があります。

これは可能ですが、Git の設定ファイルのログレベル Warn と Error を Debug へ変更し、これらの設定の変更を環境に登録するために、AEM as a Cloud Service にデプロイメントを実行する必要があります。

Debug によって書き込まれるログステートメントのトラフィックと量に応じて、環境に悪影響を与える可能性があるため、ステージと実稼動環境のデバッグレベルを変更する場合は、次のことを推奨します。

* 慎重におこない、絶対に必要な場合にのみ実行する
* 可能な限り早く適切なレベルに戻し、再デプロイする

## Splunk ログ {#splunk-logs}

Splunk アカウントを持っている顧客は、カスタマーサポートチケットを介して、AEM Cloud Service のログを適切なインデックスに転送するように依頼できます。ログデータは、Cloud Manager のログのダウンロードで利用できるものと同じですが、Splunk 製品のクエリ機能を利用すると便利です。

Splunk に送信されるログに関連付けられるネットワーク帯域幅は、お客様のネットワーク I/O 使用の一部と見なされます。

### Splunk 転送の有効化 {#enabling-splunk-forwarding}

サポートを依頼するには、顧客は次のことを示す必要があります。

* Splunk のホスト
* Splunk のインデックス
* Splunk のポート
* Splunk の HEC トークン。詳しくは、[こちらのページ](https://docs.splunk.com/Documentation/Splunk/8.0.4/Data/HECExamples)を参照してください。

上記のプロパティは、関連するプログラム／環境タイプの組み合わせごとに指定する必要があります。例えば、開発、ステージング、実稼動の各環境を希望する場合は、次に示す 3 組の情報を提供する必要があります。

>[!NOTE]
>
>サンドボックスプログラム環境の Splunk 転送はサポートされていません。

以下に、カスタマーサポートへの依頼サンプルを示します。

プログラム 123、実稼動環境

* Splunk ホスト：`splunk-hec-ext.acme.com`
* Splunk インデックス：acme_123prod（顧客は任意の命名規則を選択できます）
* Splunk ポート：443
* Splunk HEC トークン：ABC123

プログラム 123、ステージ環境

* Splunk ホスト：`splunk-hec-ext.acme.com`
* Splunk インデックス：acme_123stage
* Splunk ポート：443
* Splunk HEC トークン：ABC123

プログラム 123、開発環境

* Splunk ホスト：`splunk-hec-ext.acme.com`
* Splunk インデックス：acme_123dev
* Splunk ポート：443
* Splunk HEC トークン：ABC123

各環境に同じ Splunk インデックスを使用する場合はこれで十分です。その場合、`aem_env_type` フィールドを使用して、開発、ステージ、実稼動の値に基づいて区別できます。複数の開発環境がある場合は、`aem_env_id` フィールドも使用できます。一部の組織で、関連するインデックスのアクセスが一部の Splunk ユーザーに制限されている場合、実稼動環境のログに対して別のインデックスを選択することも可能です。

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
