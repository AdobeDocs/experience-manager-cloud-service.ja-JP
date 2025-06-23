---
title: AEM as a Cloud Service 向けのログ
description: AEM as a Cloud Service のログを使用して一元的なログサービスのグローバルパラメーターを設定する方法、個々のサービスに特有の設定またはデータのログ記録をリクエストする方法について説明します。
exl-id: 262939cc-05a5-41c9-86ef-68718d2cd6a9
feature: Log Files, Developing
role: Admin, Architect, Developer
source-git-commit: 5c32a088cf7e334ba6497a595b5176e5389ce9ed
workflow-type: ht
source-wordcount: '2556'
ht-degree: 100%

---

# AEM as a Cloud Service 向けのログ {#logging-for-aem-as-a-cloud-service}

AEM as a Cloud Service は、カスタムコードを含めて、顧客ベースに独自のエクスペリエンスを作成する顧客のためのプラットフォームです。このことを念頭に置いた上で、ログサービスは、ローカル開発およびクラウド環境、特に AEM as a Cloud Service の開発環境をデバッグし、実行されるコードを理解するための重要な機能となります。

AEM as a Cloud Service のログ設定とログレベルは、AEM プロジェクトの一部として Git に保存され、AEM プロジェクトの一部として Cloud Manager を介してデプロイされる構成ファイルで管理されます。AEM as a Cloud Service のログは、次の 3 つの論理セットに分割できます。

* AEM ログ。AEM アプリケーションレベルでログを実行します。
* Apache HTTPD Web サーバー／Dispatcher ログ。パブリッシュ層で Web サーバーと Dispatcher のログを実行します。
* CDN ログは、その名前が示すように、CDN でログを実行します。

## AEM ログ {#aem-logging}

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
デバッグログが有効になっている場合、発生したアクティビティと処理に影響を与える主要パラメーターの明確な内容を提供するステートメントがログに記録されます。</td>
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

AEM ログレベルは、OSGi 設定を介して環境の種類ごとに設定され、次に Git にコミットされて、Cloud Manager を介して AEM as a Cloud Service にデプロイされます。そのため、更新されたログレベル設定でアプリケーションを再デプロイすることなく、AEM as a Cloud Service 経由で利用可能なログを最適なログレベルで使用できるように、ログステートメントの一貫性と環境の種類を把握することをお勧めします。

>[!NOTE]
>
>顧客環境を効果的に監視するため、デフォルトのログレベルは変更しないでください。また、デフォルトのログ形式は変更しないでください。ログ出力は、デフォルトのファイルに出力されたままにする必要があります。具体的なガイドラインについては、[以下の節](#configuration-loggers)を参照してください。

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
<td>指定承認者なし。デフォルトで [クリエイティブ承認者ユーザーグループ] に設定されます</td>
</tr>
</tbody>
</table>

### ログ設定 {#configuration-loggers}

AEM Java ログは OSGi 設定として定義されるので、ターゲット固有の AEM as a Cloud Service 環境は実行モードのフォルダーを使用します。

Sling LogManager ファクトリの OSGi 設定を使用して、カスタム Java パッケージの Java ログを設定します。サポートされている設定には、次の 3 つのプロパティがあります。

| OSGi 設定プロパティ | 説明 |
|---|---|
| `org.apache.sling.commons.log.names` | ログステートメントを収集する Java パッケージです。 |
| `org.apache.sling.commons.log.level` | Java パッケージをログに記録するログレベルです（`org.apache.sling.commons.log.names` で指定） |

その他の LogManager OSGi 設定プロパティを変更すると、AEM as a Cloud Service での可用性の問題が発生する場合があります。

前の節で述べたように、顧客環境を効果的に監視するには、次の手順を実行します。
* AEM のデフォルトのログ設定（Apache Sling Logging Configuration）のログレベルを、デフォルト値の「INFO」から変更しないでください。
* 製品コードの個々のパッケージに対して、ログレベルをデバッグに設定しても構いません（「Apache Sling Logging Logger configuration」 OSGi 設定ファクトリのインスタンスを使用）。ただし、パフォーマンスの低下を防ぐために控えめに使用し、不要になったら「INFO」に戻してください。
* 顧客開発コードの場合、ログレベルを調整できます。
* すべてのログ（AEM 製品コードと顧客開発コードの両方）は、デフォルトのログ形式を維持する必要があります。
* ログの出力先はデフォルトのファイル「logs/error.log」のままにする必要があります。

そのため、次の OSGi プロパティは変更しないでください。
* **Apache Sling ログ設定**（PID：`org.apache.sling.commons.log.LogManager`）- *すべてのプロパティ*
* **Apache Sling Logging Logger Configuration**（ファクトリー PID：`org.apache.sling.commons.log.LogManager.factory.config`）：
   * `org.apache.sling.commons.log.file`
   * `org.apache.sling.commons.log.pattern`

3 つの AEM as a Cloud Service 環境で推奨されるログの設定（Java パッケージ `com.example` のプレースホルダーを使用）の例を次に示します。

### 開発 {#development}

/apps/my-app/config/org.apache.sling.commons.log.LogManager.factory.config-example.cfg.json

```
{
    "org.apache.sling.commons.log.names": ["com.example"],
    "org.apache.sling.commons.log.level": "debug"
    "org.apache.sling.commons.log.file": "logs/error.log"
}
```

### ステージ {#stage}

/apps/my-app/config.stage/org.apache.sling.commons.log.LogManager.factory.config-example.cfg.json

```
{
    "org.apache.sling.commons.log.names": ["com.example"],
    "org.apache.sling.commons.log.level": "warn"
    "org.apache.sling.commons.log.file": "logs/error.log"
}
```

### 実稼動 {#productiomn}

/apps/my-app/config.prod/org.apache.sling.commons.log.LogManager.factory.config-example.cfg.json

```
{
    "org.apache.sling.commons.log.names": ["com.example"],
    "org.apache.sling.commons.log.level": "error"
    "org.apache.sling.commons.log.file": "logs/error.log"
}
```

## AEM HTTP リクエストログ {#aem-http-request-logging}

AEM as a Cloud Service の HTTP リクエストログは、AEM に対して行われた HTTP リクエストと、それに対する HTTP レスポンスに関する情報を時系列で提供します。このログは、AEM に対して行われる HTTP リクエストと、それらの要求が処理され応答される順序を理解するのに役立ちます。

このログを理解するための鍵は、HTTP リクエストとレスポンスのペアを、括弧内の数値で示される ID でマッピングすることです。多くの場合、リクエストと対応するレスポンスのログでは、その他の HTTP リクエストとレスポンスが間に挿入されています。

**サンプルログ**

```
29/Apr/2020:19:14:21 +0000 [137] > POST /conf/global/settings/dam/adminui-extension/metadataprofile/ HTTP/1.1 [cm-p1234-e5678-aem-author-59555cb5b8-q7l9s]
...
29/Apr/2020:19:14:22 +0000 [139] > GET /mnt/overlay/dam/gui/content/processingprofilepage/metadataprofiles/editor.html/conf/global/settings/dam/adminui-extension/metadataprofile/main HTTP/1.1 [cm-p1234-e5678-aem-author-59555cb5b8-q7l9s]
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

このログは、AEM にどのような HTTP リクエストが行われているか、それに対応する HTTP レスポンスのステータスコードを調べて、リクエストが成功しているか、また HTTP リクエストが完了するまでの時間をすばやく把握するのに役立ちます。このログは、ユーザーでログエントリをフィルタリングして、特定のユーザーのアクティビティをデバッグする場合にも役立ちます。

**ログ出力の例**

```
cm-p1234-e26813-aem-author-59555cb5b8-8kgr2 - example@adobe.com 30/Apr/2020:17:37:14 +0000  "GET /libs/granite/ui/references/clientlibs/references.lc-5188e85840c529149e6cd29d94e74ad5-lc.min.css HTTP/1.1" 200 1141 "https://author-p10711-e26813.adobeaemcloud.com/mnt/overlay/dam/gui/content/assets/metadataeditor.external.html?item=/content/dam/en/images/example.jpeg&_charset_=utf8" "Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_4) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/81.0.4044.122 Safari/537.36"
cm-p1234-e26813-aem-author-59555cb5b8-8kgr2 - example@adobe.com 30/Apr/2020:17:37:14 +0000  "GET /libs/dam/gui/coral/components/admin/customthumb/clientlibs.lc-60e4443805c37afa0c74b674b141f1df-lc.min.css HTTP/1.1" 200 809 "https://author-p10711-e26813.adobeaemcloud.com/mnt/overlay/dam/gui/content/assets/metadataeditor.external.html?item=/content/dam/en/images/example.jpeg&_charset_=utf8" "Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_4) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/81.0.4044.122 Safari/537.36"
cm-p1234-e26813-aem-author-59555cb5b8-8kgr2 - example@adobe.com 30/Apr/2020:17:37:14 +0000  "GET /libs/dam/gui/coral/components/admin/metadataeditor/clientlibs/metadataeditor.lc-4a2226d8232f8b7ab27d24820b9ddd64-lc.min.js HTTP/1.1" 200 7965 "https://author-p10711-e26813.adobeaemcloud.com/mnt/overlay/dam/gui/content/assets/metadataeditor.external.html?item=/content/dam/en/images/example.jpeg&_charset_=utf8" "Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_4) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/81.0.4044.122 Safari/537.36"
```

| AEM as a Cloud Service のノード ID | cm-p1235-e2644-aem-author-59555cb5b8-8kgr2 |
|---|---|
| クライアントの IP アドレス | - |
| User | myuser@adobe.com |
| 日時 | 30/Apr/2020:17:37:14 +0000 |
| HTTP メソッド | GET |
| URL | `/libs/granite/ui/references/clientlibs/references.lc-5188e85840c529149e6cd29d94e74ad5-lc.min.css` |
| プロトコル | HTTP/1.1 |
| HTTP レスポンスステータス | 200 |
| レスポンス本文のサイズ（バイト単位） | 1141 |
| リファラー | `"https://author-p1234-e4444.adobeaemcloud.com/mnt/overlay/dam/gui/content/assets/metadataeditor.external.html?item=/content/dam/wknd/en/adventures/surf-camp-in-costa-rica/adobestock_266405335.jpeg&_charset_=utf8"` |
| ユーザーエージェント | `"Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_4) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/81.0.4044.122 Safari/537.36"` |

### HTTP アクセスログの設定 {#configuring-the-http-access-log}

HTTP アクセスログは、AEM as a Cloud Service では設定できません。

## Apache Web サーバーおよび Dispatcher ログ {#apache-web-server-and-dispatcher-logging}

AEM as a Cloud Service は、パブリッシュ上の Apache Web サーバーと Dispatcher レイヤーに 3 つのログを提供します。

* Apache HTTPD Web サーバーアクセスログ
* Apache HTTPD Web サーバーエラーログ
* Dispatcher ログ

これらのログはパブリッシュ層でのみ使用できます。

これらのログは、AEM アプリケーションに到達する前に、AEM as a Cloud Service のパブリッシュ層に対して行われた HTTP リクエストに関するインサイトを提供します。理想的には、パブリッシュ層サーバーへのほとんどの HTTP リクエストは、Apache HTTPD Web サーバーおよび AEM Dispatcher によってキャッシュされたコンテンツによって処理され、AEM アプリケーション自体には届きません。それを理解することは重要です。したがって、AEM の Java ログ、リクエストログ、アクセスログには、これらのリクエストに対するログステートメントはありません。

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

Error、Warn、Info、Debug および Trace1～Trace8 に設定でき、デフォルト値は Warn です。RewriteRules をデバッグするには、ログレベルを Trace2 に上げることをお勧めします。書き換えルールのデバッグには、[Dispatcher SDK](../../dispatcher/validation-debug.md) の使用をお勧めします。AEM as a Cloud Service の最大ログレベルは `debug` です。したがって、現在のところ、クラウド内の書き換えルールを効果的にデバッグすることはできません。

詳細は、[mod_rewrite モジュールのドキュメント](https://httpd.apache.org/docs/current/mod/mod_rewrite.html#logging)を参照してください。

環境ごとのログレベルを設定するには、次に示すように、global.var ファイル内で適切な条件付き分岐を使用します。

```
Define REWRITE_LOG_LEVEL debug

<IfDefine ENVIRONMENT_STAGE>
  ...
  Define REWRITE_LOG_LEVEL warn
  ...
</IfDefine>
<IfDefine ENVIRONMENT_PROD>
  ...
  Define REWRITE_LOG_LEVEL error
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

Error、Warn、Info、Debug および 1～Trace に設定でき、デフォルト値は Warn です。

Dispatcher ログはその他にも複数レベルのログ精度をサポートしていますが、AEM as a Cloud Service では、次のレベルを使用することをお勧めします。

環境ごとのログレベルを設定するには、次に示すように、`global.var` ファイル内で適切な条件付き分岐を使用します。

```
Define DISP_LOG_LEVEL debug

<IfDefine ENVIRONMENT_STAGE>
  ...
  Define DISP_LOG_LEVEL warn
  ...
</IfDefine>
<IfDefine ENVIRONMENT_PROD>
  ...
  Define DISP_LOG_LEVEL error
  ...
</IfDefine>
```

>[!NOTE]
>
>AEM as a Cloud Service 環境の場合、デバッグの冗長レベルは最大になります。トレースログレベルはサポートされていないので、クラウド環境で作業する場合は設定しないでください。

## CDN ログ {#cdn-log}

AEM as a Cloud Service では、ユーザーが CDN ログにアクセスできるようになっています。このログは、キャッシュヒット率の最適化などのユースケースに役立ちます。CDN ログ形式はカスタマイズできず、情報、警告、エラーなどの様々なモードに設定する概念もありません。

**例**

```
{
"timestamp": "2023-05-26T09:20:01+0000",
"ttfb": 19,
"cli_ip": "147.160.230.112",
"cli_country": "CH",
"rid": "974e67f6",
"req_ua": "Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_7) AppleWebKit/605.1.15 (KHTML, like Gecko) Version/14.0.3 Safari/605.1.15",
"host": "example.com",
"url": "/content/hello.png",
"method": "GET",
"res_ctype": "image/png",
"cache": "PASS",
"status": 200,
"res_age": 0,
"pop": "PAR",
"rules": "match=Enable-SQL-Injection-and-XSS-waf-rules-globally,waf=SQLI,action=blocked"
}
```

**ログ形式**

CDN ログは、json 形式に準拠しているという点で、他のログとは異なります。

| **フィールド名** | **説明** |
|---|---|
| *timestamp* | TLS 終了後のリクエストの開始時刻です。 |
| *ttfb* | *Time To First Byte* の略称です。リクエストの開始から、応答本文のストリーミングが開始される前の時点までの時間間隔です。 |
| *cli_ip* | クライアントの IP アドレスです。 |
| *cli_country* | クライアント国の 2 文字の [ISO 3166-1](https://ja.wikipedia.org/wiki/ISO_3166-1) alpha-2 国コードです。 |
| *rid* | リクエストを一意に識別するために使用されるリクエストヘッダーの値です。 |
| *req_ua* | 特定の HTTP リクエストの作成を担当するユーザーエージェントです。 |
| *host* | リクエストの対象となる証明機関です。 |
| *URL* | クエリパラメーターを含む完全なパスです。 |
| *method* | 「GET」や「POST」など、クライアントによって送信される HTTP メソッドです。 |
| *res_ctype* | リソースの元のメディアタイプを示すために使用される Content-Type です。 |
| *cache* | キャッシュの状態です。指定できる値は、HIT、MISS、PASS です |
| *status* | 整数値としての HTTP ステータスコードです。 |
| *res_age* | 応答が（すべてのノードで）キャッシュされた時間です（秒単位）。 |
| *pop* | CDN キャッシュサーバーのデータセンターです。 |
| *rules* | [トラフィックフィルタールール](/help/security/traffic-filter-rules-including-waf.md)と WAF フラグに一致する名前。一致がブロックされたかどうかも示します。一致するルールがない場合は空です。 |

CDN ログは、[リクエスト／応答の変換](/help/implementing/dispatcher/cdn-configuring-traffic.md#logproperty)を使用して独自のプロパティで拡張できます。

## ログのアクセス方法 {#how-to-access-logs}

### クラウド環境 {#cloud-environments}

Cloud Services の AEM as a Cloud Service のログにアクセスするには、Cloud Manager インターフェイスを使用してダウンロードするか、Adobe I/O コマンドラインインターフェイスを使用してコマンドラインでログに対して tail を実行します。詳しくは、[Cloud Manager のログに関するドキュメント](/help/implementing/cloud-manager/manage-logs.md)を参照してください。

### 追加の公開地域のログ {#logs-for-additional-publish-regions}

特定の環境で追加の公開地域が有効になっている場合、前述のように、各地域のログを Cloud Manager からダウンロードできます。

追加の公開地域の AEM ログと Dispatcher ログは、次に示すように、環境 ID の後の最初の 3 文字で地域を指定します。以下のサンプルの **nld2** では、オランダにある追加の AEM パブリッシュインスタンスを参照しています。

```
cm-p7613-e12700-nld2-aem-publish-bcbb77549-5qmmt 127.0.0.1 - 07/Nov/2023:23:57:11 +0000 "HEAD /libs/granite/security/currentuser.json HTTP/1.1" 200 - "-" "Java/11.0.19"
```

### ローカル SDK {#local-sdk}

AEM as a Cloud Service SDK は、ローカル開発をサポートするログファイルを提供します。

AEM ログは `crx-quickstart/logs` フォルダー内にあり、次のログが参照できます。

* AEM Java ログ： `error.log`
* AEM HTTP リクエストログ： `request.log`
* AEM HTTP アクセスログ： `access.log`

Dispatcher を含む Apache レイヤーログは、Dispatcher を保持する Docker コンテナにあります。Dispatcher の開始方法については、[Dispatcher のドキュメント](/help/implementing/dispatcher/disp-overview.md)を参照してください。

ログを取得するには、以下の手順に従います。

1. コマンドラインで、`docker ps` と入力してコンテナを一覧表示します。
1. コンテナにログインするには、「`docker exec -it <container> /bin/sh`」と入力します。`<container>` は前の手順の Dispatcher コンテナ ID です。
1. `/mnt/var/www/html` 下のキャッシュルートに移動します。
1. ログは `/etc/httpd/logs` 下にあります。
1. ログの調査：XYZ フォルダーにアクセスし、次のログを参照できます。
   * Apache HTTPD Web サーバーアクセスログ - `httpd_access.log`
   * Apache HTTPD Web サーバーエラーログ - `httpd_error.log`
   * Dispatcher ログ - `dispatcher.log`

ログは端末の出力にも直接表示できます。ほとんどの場合、これらのログは DEBUG で出力されるもので、Docker の実行時に Debug レベルをパラメーターとして渡すことで実現できます。例：

`DISP_LOG_LEVEL=Debug ./bin/docker_run.sh out docker.for.mac.localhost:4503 8080`

## 実稼動環境とステージ環境のデバッグ {#debugging-production-and-stage}

例外的な状況では、ステージまたは実稼動環境でログレベルを変更して、ログをより細かく記録する必要があります。

これは可能ですが、Git の設定ファイルのログレベル Warn と Error を Debug へ変更し、これらの設定の変更を環境に登録するために、AEM as a Cloud Service にデプロイメントを実行する必要があります。

Debug によって書き込まれるログステートメントのトラフィックと量に応じて、環境に悪影響を与える可能性があるため、ステージと実稼動環境のデバッグレベルを変更する場合は、次のことを推奨します。

* 慎重に行い、絶対に必要な場合にのみ実行する
* 可能な限り早く適切なレベルに戻し、再デプロイする

## ログ転送 {#log-forwarding}

ログは Cloud Manager からダウンロードできますが、組織によっては、これらのログを優先されるログの宛先に転送すると役立ちます。AEM では、次の宛先へのログのストリーミングをサポートしています。

* Azure Blob Storage
* Datadog
* HTTPD
* Elasticsearch（および OpenSearch）
* Splunk

この機能の設定方法について詳しくは、[ログ転送の記事](/help/implementing/developing/introduction/log-forwarding.md)を参照してください。

>[!NOTE]
>
>サンドボックスプログラム環境のログ転送はサポートされていません。
