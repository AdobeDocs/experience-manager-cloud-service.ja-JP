---
title: クラウド内の Dispatcher
description: クラウド内の Dispatcher
feature: Dispatcher
exl-id: 6d78026b-687e-434e-b59d-9d101349a707
source-git-commit: 98eff568686c72c626d2bf77d82e8c3f224eda42
workflow-type: tm+mt
source-wordcount: '983'
ht-degree: 72%

---

# クラウド内の Dispatcher {#Dispatcher-in-the-cloud}

>[!CONTEXTUALHELP]
>id="aemcloud_nonbpa_dispoverview"
>title="クラウド内の Dispatcher"
>abstract="このページでは、Dispatcher ツール（サポートされる Apache モジュール）のダウンロードと抽出の方法と、レガシーおよび柔軟なモードの概要について説明します。"

## はじめに {#apache-and-dispatcher-configuration-and-testing}

このページでは、Dispatcher ツールと、サポートされる Apache モジュールのダウンロードおよび抽出方法について説明し、従来の柔軟なモードの概要を示します。 また、検証とデバッグ、および Dispatcher 設定の AMS からAEMへの移行に関する詳細な参照もあります。 <!-- ERROR: NOT FOUND (HTTP ERROR 404) Also, see [this video](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/cloud-5/cloud5-aem-dispatcher-cloud.html) for additional details about deploying dispatcher files in a cloud service environment. -->

## Dispatcher ツール {#dispatcher-sdk}

Dispatcher ツールは、AEM as a Cloud Service の SDK の一部で、以下を提供します。

* Dispatcher 用の Maven プロジェクトにインクルードする設定ファイルを含んだバニラファイル構造。
* Dispatcher 設定にAEMas a Cloud Serviceサポートディレクティブのみが含まれていることを検証するためのツール。 また、ツールでは、Apache が正常に起動できるように、構文が正しいかを検証します。
* Dispatcher をローカルで実行する Docker イメージ。

## ツールのダウンロードと抽出 {#extracting-the-sdk}

[AEM as a Cloud Service SDK](/help/implementing/developing/introduction/aem-as-a-cloud-service-sdk.md) に含まれている Dispatcher ツールは、[ソフトウェア配布](https://downloads.experiencecloud.adobe.com/content/software-distribution/en/aemcloud.html)ポータルで zip ファイルとしてダウンロードできます。新しい Dispatcher ツールバージョンで利用可能な新しい設定は、そのバージョン以降の AEM が実行されているクラウド環境にデプロイするときに使用できます。

SDK を解凍します。この SDK は、macOS、Linux®および Windows 用の Dispatcher ツールをバンドルしています。

**macOS／Linux の場合**：Dispatcher ツールのアーティファクトを実行可能にして実行します。保存先のディレクトリ ( ここでは `version` は、Dispatcher ツールのバージョンです )。

```bash
$ chmod +x aem-sdk-dispatcher-tools-<version>-unix.sh
$ ./aem-sdk-dispatcher-tools-<version>-unix.sh
Verifying archive integrity...  100%   All good.
Uncompressing aem-sdk-dispatcher-tools-<version>-unix.sh 100%
```

**Windows の場合**：Dispatcher ツールの zip アーカイブを解凍します。

## Dispatcher ツールを使用した検証とデバッグ {#validation-debug}

Dispatcher ツールは、プロジェクトの Dispatcher 設定を検証およびデバッグするために使用されます。 プロジェクトの Dispatcher 設定が柔軟モードとレガシーモードのどちらで構造化されているかに基づいて、以下で参照するページでこれらのツールを使用する方法について詳しく説明します。

* **フレキシブルモード** - [AEM アーキタイプ 28](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/overview.html?lang=ja) 以降の推奨モードであり、デフォルトです。Cloud Manager 2021.7.0 リリース以降に作成された新しい環境用に Cloud Manager でも使用されます。このモードを有効にするには、フォルダーおよびファイル `opt-in/USE_SOURCES_DIRECTLY` を追加します。より柔軟性の高いこのモードを使用する場合は、rewrites フォルダー下のファイル構造に制限はありません。レガシーモードでは、このフォルダーに 1 つの `rewrite.rules` ファイルが必要でした。また、追加できるルールの数に制限はありません。フォルダー構造とローカル検証について詳しくは、 [Dispatcher ツールを使用した検証とデバッグ](/help/implementing/dispatcher/validation-debug.md).

* **レガシーモード**  — フォルダー構造と、Dispatcher 設定のレガシーモードのローカル検証について詳しくは、 [Dispatcher ツール（レガシー）を使用した検証とデバッグ](/help/implementing/dispatcher/validation-debug-legacy.md)

従来の設定モデルからより柔軟性の高い設定モデル（AEM アーキタイプ 28 以降に付属）に移行する方法について詳しくは、[このドキュメント](/help/implementing/dispatcher/validation-debug.md#migrating)を参照してください。

## Content-Disposition {#content-disposition}

パブリッシュ層では、BLOB のデフォルトの配信方法は添付ファイルです。 標準の [コンテンツ配置ヘッダー](https://developer.mozilla.org/ja-JP/docs/Web/HTTP/Headers/Content-Disposition) Dispatcher 内で使用する必要があります。

どのような設定になるかを次の例で示します。

```
<LocationMatch "^\/content\/dam.*\.(pdf).*">
 Header unset Content-Disposition
 Header set Content-Disposition inline
</LocationMatch>
```

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
| `mod_macro` | [https://httpd.apache.org/docs/2.4/mod/mod_macro.html](https://httpd.apache.org/docs/2.4/mod/mod_macro.html) |
| `mod_include (no directives supported)` | [https://httpd.apache.org/docs/2.4/mod/mod_include.html](https://httpd.apache.org/docs/2.4/mod/mod_include.html) |


お客様が任意のモジュールを追加することはできませんが、今後、上記の表にある以外のモジュールが追加で組み込まれる可能性があります。お客様は、SDK でバリデーターの allowlist コマンドを実行することにより、特定の Dispatcher バージョンで使用可能なディレクティブのリストを見つけることができます。

Apache の設定ファイルで許可されているディレクティブは、バリデーターの allowlist コマンドを実行すると表示できます。

```
$ validator allowlist
Cloud manager validator 2.0.4
 
Allowlisted directives:
  <Directory>
  ...
  
```

## フォルダー構造 {#folder-structure}

プロジェクトの Apache フォルダー構造と Dispatcher フォルダー構造は、プロジェクトで使用するモードに応じて若干異なります。詳しくは、 [Dispatcher ツールを使用した検証とデバッグ](#validation-debug) 」の節を参照してください。

## AMS からの Dispatcher 設定の移行 {#ams-aem}

Dispatcher 設定を AMS から AEM as a Cloud Service に移行する方法について詳しくは、[AMS から AEM as a Cloud Service への Dispatcher 設定の移行](/help/implementing/dispatcher/ams-aem.md)を参照してください。
