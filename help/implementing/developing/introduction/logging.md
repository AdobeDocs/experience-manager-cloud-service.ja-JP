---
title: ログ
description: 一元的なログサービスのグローバルパラメーターの設定、個々のサービスに特有の設定、またはデータのログ記録の要求をおこなう方法を学習します。
translation-type: tm+mt
source-git-commit: 1cee93310d84ea21b626f456163de6855056db5b
workflow-type: tm+mt
source-wordcount: '932'
ht-degree: 11%

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

発行層のDispatcherキャッシュまたはアップストリームCDNから提供されるHTTP要求は、これらのログには反映されません。

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

| 日付と時間 | AEMをCloud ServiceーのノードIDとして | ログレベル | ねじ | Java クラス | ログメッセージ |
|---|---|---|---|---|---|
| 29.04.2020 21:50:13.398 | `[cm-p1234-e5678-aem-author-59555cb5b8-q7l9s]` | `*DEBUG*` | qtp2130572036-1472 | com.example.approval.workflow.impl.CustomApprovalWorkflow | `No specified approver, defaulting to [ Creative Approvers user group ]` |

**ログ出力の例**

```
22.06.2020 18:33:30.120 [cm-p12345-e6789-aem-author-86657cbb55-xrnzq] *ERROR* [qtp501076283-1809] io.prometheus.client.dropwizard.DropwizardExports Failed to get value from Gauge
22.06.2020 18:33:30.229 [cm-p12345-e6789-aem-author-86657cbb55-xrnzq] *INFO* [qtp501076283-1805] org.apache.sling.auth.core.impl.SlingAuthenticator getAnonymousResolver: Anonymous access not allowed by configuration - requesting credentials
22.06.2020 18:33:30.370 [cm-p12345-e6789-aem-author-86657cbb55-xrnzq] *INFO* [73.91.59.34 [1592850810364] GET /libs/granite/core/content/login.html HTTP/1.1] org.apache.sling.i18n.impl.JcrResourceBundle Finished loading 0 entries for 'en_US' (basename: <none>) in 4ms
22.06.2020 18:33:30.372 [cm-p12345-e6789-aem-author-86657cbb55-xrnzq] *INFO* [FelixLogListener] org.apache.sling.i18n Service [5126, [java.util.ResourceBundle]] ServiceEvent REGISTERED
22.06.2020 18:33:30.372 [cm-p12345-e6789-aem-author-86657cbb55-xrnzq] *WARN* [73.91.59.34 [1592850810364] GET /libs/granite/core/content/login.html HTTP/1.1] libs.granite.core.components.login.login$jsp j_reason param value 'unknown' cannot be mapped to a valid reason message: ignoring
```

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

| 日付と時間 | リクエストと応答のペアID |  | HTTP メソッド | URL | プロトコル | Cloud ServiceノードIDとしてのAEM |
|---|---|---|---|---|---|---|
| 29/Apr/2020:19:14:21 +0000 | `[137]` | -> | POST | /conf/global/settings/dam/adminui-extension/metadataprofile/ | HTTP/1.1 | `[cm-p1234-e5678-aem-author-59555cb5b8-q7l9s]` |

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

### ログの設定 {#configuring-the-log}

AEM HTTP要求ログは、AEMでCloud Serviceとして設定できません。

## AEM HTTPアクセスログ {#aem-http-access-logging}

AEMのCloud ServiceHTTPアクセスログは、HTTPリクエストを時間順に表示します。 各ログエントリは、AEMにアクセスするHTTP要求を表します。

このログは、AEMに対して行われているHTTP要求が何であるか、それに伴うHTTP応答ステータスコードを調べて成功した場合、およびHTTP要求が完了するまでの時間をすばやく把握するのに役立ちます。 このログは、ユーザーがログエントリをフィルタリングして、特定のユーザーのアクティビティをデバッグする場合にも役立ちます。

### ログ形式 {#access-log-format}

| Cloud ServiceノードIDとしてのAEM | クライアントのIPアドレス | User |  | 日時 |  | HTTPメソッド | URL | プロトコル |  | HTTP応答 | HTTP要求時間（ミリ秒） | リファラー | ユーザーエージェント |
|---|---|---|---|---|---|---|---|---|---|---|---|---|---|
| cm-p1235-e2644-aem-author-5955cb5b8-8kgr2 | - | `myuser@adobe.com` | 30/Apr/2020:17:37:14 +0000 | &quot; | GET | /libs/granite/ui/references/clientlibs/references.lc-5188e85840c529149e6cd29d94e74ad5-lc.min.css |  | HTTP/1.1 | &quot; | 200 | 1141 | `"https://author-p1234-e4444.adobeaemcloud.com/mnt/overlay/dam/gui/content/assets/metadataeditor.external.html?item=/content/dam/wknd/en/adventures/surf-camp-in-costa-rica/adobestock_266405335.jpeg&_charset_=utf8"` | &quot;Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_4)AppleWebKit/537.36 （KHTML、Geckoなど） Chrome/81.0.4044.122 Safari/537.36&quot; |

**例**

```
cm-p1234-e26813-aem-author-59555cb5b8-8kgr2 - example@adobe.com 30/Apr/2020:17:37:14 +0000  "GET /libs/granite/ui/references/clientlibs/references.lc-5188e85840c529149e6cd29d94e74ad5-lc.min.css HTTP/1.1" 200 1141 "https://author-p10711-e26813.adobeaemcloud.com/mnt/overlay/dam/gui/content/assets/metadataeditor.external.html?item=/content/dam/en/images/example.jpeg&_charset_=utf8" "Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_4) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/81.0.4044.122 Safari/537.36"
cm-p1234-e26813-aem-author-59555cb5b8-8kgr2 - example@adobe.com 30/Apr/2020:17:37:14 +0000  "GET /libs/dam/gui/coral/components/admin/customthumb/clientlibs.lc-60e4443805c37afa0c74b674b141f1df-lc.min.css HTTP/1.1" 200 809 "https://author-p10711-e26813.adobeaemcloud.com/mnt/overlay/dam/gui/content/assets/metadataeditor.external.html?item=/content/dam/en/images/example.jpeg&_charset_=utf8" "Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_4) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/81.0.4044.122 Safari/537.36"
cm-p1234-e26813-aem-author-59555cb5b8-8kgr2 - example@adobe.com 30/Apr/2020:17:37:14 +0000  "GET /libs/dam/gui/coral/components/admin/metadataeditor/clientlibs/metadataeditor.lc-4a2226d8232f8b7ab27d24820b9ddd64-lc.min.js HTTP/1.1" 200 7965 "https://author-p10711-e26813.adobeaemcloud.com/mnt/overlay/dam/gui/content/assets/metadataeditor.external.html?item=/content/dam/en/images/example.jpeg&_charset_=utf8" "Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_4) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/81.0.4044.122 Safari/537.36"
```
