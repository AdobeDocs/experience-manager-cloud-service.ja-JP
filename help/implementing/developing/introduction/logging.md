---
title: ログ
description: 一元的なログサービスのグローバルパラメーターの設定、個々のサービスに特有の設定、またはデータのログ記録の要求をおこなう方法を学習します。
translation-type: tm+mt
source-git-commit: 436b4d05c88ba227144052fdd63ea78cbf1f03ba
workflow-type: tm+mt
source-wordcount: '386'
ht-degree: 17%

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

### AEM Javaログ {#aem-java-logging}

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