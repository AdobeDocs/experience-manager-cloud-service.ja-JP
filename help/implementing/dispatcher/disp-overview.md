---
title: クラウド内の Dispatcher
description: 'クラウド内の Dispatcher '
feature: Dispatcher
exl-id: 6d78026b-687e-434e-b59d-9d101349a707
source-git-commit: 5545f7c271137050d522904bfa94e20f0286e059
workflow-type: tm+mt
source-wordcount: '917'
ht-degree: 47%

---

# クラウド内の Dispatcher {#Dispatcher-in-the-cloud}

>[!CONTEXTUALHELP]
>id="aemcloud_nonbpa_dispoverview"
>title="クラウド内の Dispatcher"
>abstract="このページでは、Dispatcherツール、サポートされるApacheモジュールをダウンロードして抽出する方法と、レガシーモードと柔軟モードの概要について説明します。"

## はじめに {#apache-and-dispatcher-configuration-and-testing}

このページでは、Dispatcherツールと、サポートされるApacheモジュールのダウンロードおよび抽出方法について説明し、レガシーおよび柔軟なモードの概要を示します。 さらに、検証とデバッグ、およびDispatcher設定のAMSからAEM as aCloud Serviceへの移行に関する詳細な参照もあります

## Dispatcher ツール {#dispatcher-sdk}

Dispatcher ツールは、AEM as a Cloud Service の SDK の一部で、以下を提供します。

* Dispatcher 用の Maven プロジェクトにインクルードする設定ファイルを含んだバニラファイル構造。
* AEM as a Cloud Service でサポートされているディレクティブのみ Dispatcher 設定に含まれていることを顧客が検証するためのツール。また、ツールでは、Apache を開始が正常に起動できるように、構文が正しいかどうかも検証されます。
* Dispatcher をローカルで実行する Docker イメージ。

## ツールのダウンロードと抽出 {#extracting-the-sdk}

[AEM as a Cloud Service SDK](/help/implementing/developing/introduction/aem-as-a-cloud-service-sdk.md) に含まれている Dispatcher ツールは、[ソフトウェア配布](https://downloads.experiencecloud.adobe.com/content/software-distribution/en/aemcloud.html)ポータルで zip ファイルとしてダウンロードできます。新しいDispatcherツールバージョンで使用可能な新しい設定は、そのバージョン以降のAEMを実行するクラウド環境にデプロイするために使用できます。

SDKを解凍します。このSDKは、macOS、Linux、Windowsの両方のDispatcherツールをバンドルします。

**macOS／Linux の場合**：Dispatcher ツールのアーティファクトを実行可能にして実行します。保存先のディレクトリ（`version` は Dispatcher ツールのバージョン）の下にある、Dispatcher ツールファイルが自己-解凍されます。

```bash
$ chmod +x aem-sdk-dispatcher-tools-<version>-unix.sh
$ ./aem-sdk-dispatcher-tools-<version>-unix.sh
Verifying archive integrity...  100%   All good.
Uncompressing aem-sdk-dispatcher-tools-<version>-unix.sh 100%
```

**Windows の場合**：Dispatcher ツールの zip アーカイブを解凍します。

## Dispatcherツールを使用した検証とデバッグ {#validation-debug}

Dispatcherツールは、プロジェクトのDispatcher設定を検証およびデバッグするために使用されます。 プロジェクトのDispatcher設定がフレキシブルモードとレガシーモードのどちらで構造化されているかに基づいて、以下で説明するページでこれらのツールを使用する方法について詳しく説明します。

* **柔軟なモード**  -  [AEMアーキタイプ28以降の推奨モードとデフォルト](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/overview.html?lang=en) 。Cloud Manager 2021.7.0リリース以降に作成された新しい環境用にCloud Managerでも使用されます。ユーザーは、フォルダーとファイル`opt-in/USE_SOURCES_DIRECTLY`を追加して、このモードを有効にできます。 この柔軟なモードを使用することで、rewritesフォルダーの下のファイル構造に制限はなく、レガシーモードでは1つの`rewrite.rules`ファイルが必要でした。 また、追加できるルールの数に制限はありません。 フォルダー構造とローカル検証について詳しくは、[Dispatcherツール](/help/implementing/dispatcher/validation-debug.md)を使用した検証とデバッグを参照してください。

* **レガシーモード**  - Dispatcher設定のレガシーモードのフォルダー構造とローカル検証について詳しくは、 Dispatcherツール（レガシー）を使用した検証とデバッグを参照してくださ [い。](/help/implementing/dispatcher/validation-debug-legacy.md)

AEMアーキタイプ28以降に付属する、従来の設定モデルからより柔軟な設定モデルに移行する方法について詳しくは、[このドキュメント](/help/implementing/dispatcher/validation-debug.md#migrating)を参照してください。

## サポートされるApacheモジュール {#supported-directives}

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

お客様は任意のモジュールを追加することはできませんが、今後追加のモジュールが組み込まれる可能性があります。 SDKでバリデーターの設定コマンドを実行すると、特定のDispatcherバージョンで使用できるディレクティブのリストを確認できま許可リストす。

Apache設定ファイルで許可されているディレクティブは、バリデーターの「 許可リスト 」コマンドを実行すると表示できます。

```
$ validator allowlist
Cloud manager validator 2.0.4
 
Allowlisted directives:
  <Directory>
  ...
  
```

## フォルダー構造 {#folder-structure}

上記の[Dispatcherツール](#validation-debug)を使用した検証とデバッグの節で説明したように、プロジェクトのApacheフォルダー構造とDispatcherフォルダー構造は、プロジェクトで使用しているモードに応じて若干異なります。

## AMSからのDispatcher設定の移行 {#ams-aem}

Dispatcher設定をAMSからAEM as aCloud ServiceにCloud Serviceする方法について詳しくは、 [AMSからAEM](/help/implementing/dispatcher/ams-aem.md)へのDispatcher設定の移行を移行ページとして参照してください。
