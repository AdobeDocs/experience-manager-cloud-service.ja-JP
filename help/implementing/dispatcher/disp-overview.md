---
title: クラウド内の Dispatcher
description: 'クラウド内の Dispatcher '
feature: Dispatcher
exl-id: 6d78026b-687e-434e-b59d-9d101349a707
source-git-commit: 4be76f19c27aeab84de388106a440434a99a738c
workflow-type: tm+mt
source-wordcount: '916'
ht-degree: 100%

---

# クラウド内の Dispatcher {#Dispatcher-in-the-cloud}

>[!CONTEXTUALHELP]
>id="aemcloud_nonbpa_dispoverview"
>title="クラウド内の Dispatcher"
>abstract="ここでは、Dispatcher ツールのダウンロードおよび抽出方法、サポートされている Apache モジュール、レガシーモードとフレキシブルモードの概要について説明します。"

## はじめに {#apache-and-dispatcher-configuration-and-testing}

ここでは、Dispatcher ツールとそのダウンロードおよび抽出方法、サポートされている Apache モジュール、レガシーモードとフレキシブルモードの概要について説明します。さらに、検証とデバッグ、AMS から AEM as a Cloud Service への Dispatcher 設定の移行についても説明します。

## Dispatcher ツール {#dispatcher-sdk}

Dispatcher ツールは、AEM as a Cloud Service の SDK の一部で、以下を提供します。

* Dispatcher 用の Maven プロジェクトにインクルードする設定ファイルを含んだバニラファイル構造。
* AEM as a Cloud Service でサポートされているディレクティブのみ Dispatcher 設定に含まれていることを顧客が検証するためのツール。また、ツールでは、Apache を開始が正常に起動できるように、構文が正しいかどうかも検証されます。
* Dispatcher をローカルで実行する Docker イメージ。

## ツールのダウンロードと抽出 {#extracting-the-sdk}

[AEM as a Cloud Service SDK](/help/implementing/developing/introduction/aem-as-a-cloud-service-sdk.md) に含まれている Dispatcher ツールは、[ソフトウェア配布](https://downloads.experiencecloud.adobe.com/content/software-distribution/en/aemcloud.html)ポータルで zip ファイルとしてダウンロードできます。新しい Dispatcher ツールバージョンで利用可能な新しい設定は、そのバージョン以降の AEM が実行されているクラウド環境にデプロイするときに使用できます。

SDK を解凍します。SDK には、macOS 版、Linux 版および Windows 版の Dispatcher ツールがバンドルされています。

**macOS／Linux の場合**：Dispatcher ツールのアーティファクトを実行可能にして実行します。保存先のディレクトリ（`version` は Dispatcher ツールのバージョン）の下にある、Dispatcher ツールファイルが自己-解凍されます。

```bash
$ chmod +x aem-sdk-dispatcher-tools-<version>-unix.sh
$ ./aem-sdk-dispatcher-tools-<version>-unix.sh
Verifying archive integrity...  100%   All good.
Uncompressing aem-sdk-dispatcher-tools-<version>-unix.sh 100%
```

**Windows の場合**：Dispatcher ツールの zip アーカイブを解凍します。

## Dispatcher ツールを使用した検証とデバッグ {#validation-debug}

Dispatcher ツールは、プロジェクトの Dispatcher 設定の検証とデバッグに使用されます。これらのツールの使用方法について詳しくは、プロジェクトの Dispatcher 設定がフレキシブルモードとレガシーモードのどちらで構造化されているかに応じて、以下で紹介するページを参照してください。

* **フレキシブルモード** - [AEM アーキタイプ 28](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/overview.html?lang=ja) 以降の推奨モードであり、デフォルトです。Cloud Manager 2021.7.0 リリース以降に作成された新しい環境用に Cloud Manager でも使用されます。このモードを有効にするには、フォルダーおよびファイル `opt-in/USE_SOURCES_DIRECTLY` を追加します。より柔軟性の高いこのモードを使用する場合は、rewrites フォルダー下のファイル構造に制限はありません。レガシーモードでは、このフォルダーに 1 つの `rewrite.rules` ファイルが必要でした。また、追加できるルールの数に制限はありません。フォルダー構造とローカル検証について詳しくは、[Dispatcher ツールを使用した検証とデバッグ](/help/implementing/dispatcher/validation-debug.md)を参照してください。

* **レガシーモード** - Dispatcher 設定のレガシーモードでのフォルダー構造とローカル検証について詳しくは、[Dispatcher ツールを使用した検証とデバッグ（レガシー）](/help/implementing/dispatcher/validation-debug-legacy.md)を参照してください。

従来の設定モデルからより柔軟性の高い設定モデル（AEM アーキタイプ 28 以降に付属）に移行する方法について詳しくは、[このドキュメント](/help/implementing/dispatcher/validation-debug.md#migrating)を参照してください。

## サポートされている Apache モジュール {#supported-directives}

次の表に、サポートされる Apache モジュールを示します。

| モジュール名 | 参照ページ |
|---|---|
| `core` | [https://httpd.apache.org/docs/2.4/mod/core.html](https://httpd.apache.org/docs/2.4/mod/core.html) |
| `mod_access_compat` | [https://httpd.apache.org/docs/2.4/mod/mod_access_compat.html](https://httpd.apache.org/docs/2.4/mod/mod_access_compat.html) |
| `mod_alias` | [https://httpd.apache.org/docs/2.4/mod/mod_alias.html](https://httpd.apache.org/docs/2.4/mod/mod_alias.html) |
| `mod_allowmethods` | [https://httpd.apache.org/docs/2.4/mod/mod_allowmethods.html](https://httpd.apache.org/docs/2.4/mod/mod_allowmethods.html) |
| `mod_authn_core` | [https://httpd.apache.org/docs/2.4/mod/mod_authn_core.html](https://httpd.apache.org/docs/2.4/mod/mod_authn_core.html) |
| `mod_authn_file` | [https://httpd.apache.org/docs/2.4/mod/core.html](https://httpd.apache.org/docs/2.4/mod/mod_authn_file.html) |
| `mod_authz_core` | [https://httpd.apache.org/docs/2.4/mod/core.html](https://httpd.apache.org/docs/2.4/mod/mod_authz_core.html) |
| `mod_authz_groupfile` | [https://httpd.apache.org/docs/2.4/mod/mod_authz_groupfile.html](https://httpd.apache.org/docs/2.4/mod/mod_authz_groupfile.html) |
| `mod_deflate` | [https://httpd.apache.org/docs/2.4/mod/mod_deflate.html](https://httpd.apache.org/docs/2.4/mod/mod_deflate.html) |
| `mod_dir` | [https://httpd.apache.org/docs/2.4/mod/mod_dir.html](https://httpd.apache.org/docs/2.4/mod/mod_dir.html) |
| `mod_env` | [https://httpd.apache.org/docs/2.4/mod/mod_env.html](https://httpd.apache.org/docs/2.4/mod/mod_env.html) |
| `mod_filter` | [https://httpd.apache.org/docs/2.4/mod/mod_filter.html](https://httpd.apache.org/docs/2.4/mod/mod_filter.html) |
| `mod_headers` | [https://httpd.apache.org/docs/2.4/mod/mod_headers.html](https://httpd.apache.org/docs/2.4/mod/mod_headers.html) |
| `mod_mime` | [https://httpd.apache.org/docs/2.4/mod/mod_mime.html](https://httpd.apache.org/docs/2.4/mod/mod_mime.html) |
| `mod_proxy` | [https://httpd.apache.org/docs/2.4/mod/mod_proxy.html](https://httpd.apache.org/docs/2.4/mod/mod_proxy.html) |
| `mod_proxy_http` | [https://httpd.apache.org/docs/2.4/mod/mod_proxy_http.html](https://httpd.apache.org/docs/2.4/mod/mod_proxy_http.html) |
| `mod_remoteip` | [https://httpd.apache.org/docs/2.4/mod/mod_remoteip.html](https://httpd.apache.org/docs/2.4/mod/mod_remoteip.html) |
| `mod_reqtimeout` | [https://httpd.apache.org/docs/2.4/mod/mod_reqtimeout.html](https://httpd.apache.org/docs/2.4/mod/mod_reqtimeout.html) |
| `mod_rewrite` | [https://httpd.apache.org/docs/2.4/mod/mod_rewrite.html](https://httpd.apache.org/docs/2.4/mod/mod_rewrite.html) |
| `mod_security` | [https://modsecurity.org/](https://modsecurity.org/) |
| `mod_setenvif` | [https://httpd.apache.org/docs/2.4/mod/mod_setenvif.html](https://httpd.apache.org/docs/2.4/mod/mod_setenvif.html) |
| `mod_ssl (only the SSLProxyEngine directive)` | [https://httpd.apache.org/docs/2.4/mod/mod_ssl.html#sslproxyengine](https://httpd.apache.org/docs/2.4/mod/mod_ssl.html#sslproxyengine) |
| `mod_substitute` | [https://httpd.apache.org/docs/2.4/mod/mod_substitute.html](https://httpd.apache.org/docs/2.4/mod/mod_substitute.html) |
| `mod_userdir` | [https://httpd.apache.org/docs/2.4/mod/mod_userdir.html](https://httpd.apache.org/docs/2.4/mod/mod_userdir.html) |

お客様が任意のモジュールを追加することはできませんが、今後、上述の表にある以外のモジュールが追加で組み込まれる可能性があります。SDK でバリデーターの許可リストコマンドを実行すると、特定の Dispatcher バージョンで使用できるディレクティブのリストを確認できます。

Apache の設定ファイルで許可されているディレクティブは、バリデーターの許可リストコマンドを実行すると表示できます。

```
$ validator allowlist
Cloud manager validator 2.0.4
 
Allowlisted directives:
  <Directory>
  ...
  
```

## フォルダー構造 {#folder-structure}

上記の [Dispatcher ツールを使用した検証とデバッグ](#validation-debug)の節で説明したように、プロジェクトの Apache および Dispatcher フォルダー構造は、プロジェクトで使用しているモードによって若干異なります。

## AMS からの Dispatcher 設定の移行 {#ams-aem}

Dispatcher 設定を AMS から AEM as a Cloud Service に移行する方法について詳しくは、[AMS から AEM as a Cloud Service への Dispatcher 設定の移行](/help/implementing/dispatcher/ams-aem.md)を参照してください。
