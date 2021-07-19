---
title: クラウド内の Dispatcher
description: 'クラウド内の Dispatcher '
feature: Dispatcher
exl-id: 6d78026b-687e-434e-b59d-9d101349a707
source-git-commit: 00bea8b6a32bab358dae6a8c30aa807cf4586d84
workflow-type: tm+mt
source-wordcount: '4247'
ht-degree: 97%

---

# クラウド内の Dispatcher {#Dispatcher-in-the-cloud}

>[!CONTEXTUALHELP]
>id="aemcloud_nonbpa_dispoverview"
>title="クラウド内の Dispatcher"
>abstract="ここでは、AEM as a Cloud Service の Apache および Dispatcher の設定を構築する方法と、クラウド環境にデプロイする前にローカルで検証および実行する方法について説明します。また、クラウド環境でのデバッグについても説明します。"

## Apache および Dispatcher の設定とテスト {#apache-and-dispatcher-configuration-and-testing}

ここでは、AEM as a Cloud Service の Apache および Dispatcher の設定を構築する方法と、クラウド環境にデプロイする前にローカルで検証および実行する方法について説明します。また、クラウド環境でのデバッグについても説明します。Dispatcher について詳しくは、[AEM Dispatcher のドキュメント](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/dispatcher.html?lang=ja)を参照してください。

>[!NOTE]
>Windows ユーザーは、Docker をサポートする Windows 10 Professional またはその他のディストリビューションを使用する必要があります。これは、ローカルコンピューターで Dispatcher を実行およびデバッグする場合に必要な前提条件です。以下では、Mac または Linux バージョンの SDK を使用するコマンドについて説明しますが、Windows SDK も同様の方法で使用できます。

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

## ファイル構造 {#file-structure}

プロジェクトの Dispatcher サブフォルダーの構造を以下に示します。これを、Maven プロジェクトの Dispatcher フォルダーにコピーする必要があります。

```bash
./
├── conf.d
│   ├── available_vhosts
│   │   └── default.vhost
│   ├── dispatcher_vhost.conf
│   ├── enabled_vhosts
│   │   ├── README
│   │   └── default.vhost -> ../available_vhosts/default.vhost
│   └── rewrites
│   │   ├── default_rewrite.rules
│   │   └── rewrite.rules
│   └── variables
|       ├── custom.vars
│       └── global.vars
└── conf.dispatcher.d
    ├── available_farms
    │   └── default.farm
    ├── cache
    │   ├── default_invalidate.any
    │   ├── default_rules.any
    │   └── rules.any
    ├── clientheaders
    │   ├── clientheaders.any
    │   └── default_clientheaders.any
    ├── dispatcher.any
    ├── enabled_farms
    │   ├── README
    │   └── default.farm -> ../available_farms/default.farm
    ├── filters
    │   ├── default_filters.any
    │   └── filters.any
    ├── renders
    │   └── default_renders.any
    └── virtualhosts
        ├── default_virtualhosts.any
        └── virtualhosts.any
```

以下に、変更可能な注目すべきファイルを示します。

**カスタマイズ可能なファイル**

以下のファイルはカスタマイズ可能で、デプロイ時にクラウドインスタンスに転送されます。

* `conf.d/available_vhosts/<CUSTOMER_CHOICE>.vhost`

これらのファイルは 1 つ以上持つことができます。ファイルには、ホスト名に一致する `<VirtualHost>` エントリが含まれ、Apache が異なるルールで各ドメイントラフィックを扱うことができます。ファイルは `available_vhosts` ディレクトリ内に作成され、`enabled_vhosts` ディレクトリ内のシンボリックリンクで有効になります。`.vhost` ファイルから、書き換えや変数などその他のファイルがインクルードされます。

* `conf.d/rewrites/rewrite.rules`

このファイルは、`.vhost` ファイル内からインクルードされます。`mod_rewrite` には一連の書き換えルールがあります。

>[!NOTE]
>
>現在は、サイト固有のファイルではなく、単一の書き換えファイルを使用する必要があります。原則として、カスタマイズ可能なファイルの内容は合計 1 MB未満にする必要があります。

* `conf.d/variables/custom.vars`

このファイルは、`.vhost` ファイル内からインクルードされます。この場所に、Apache変数用の定義を追加できます。

* `conf.d/variables/global.vars`

このファイルは、`dispatcher_vhost.conf` ファイル内からインクルードされます。このファイルで Dispatcher の変更とログレベルの書き換えができます。

* `conf.dispatcher.d/available_farms/<CUSTOMER_CHOICE>.farm`

これらのファイルは 1 つ以上持つことができます。ファイルにはホスト名と一致するファームが含まれ、Dispatcher モジュールに異なるルールで各ファームを処理することを可能にします。ファイルは `available_farms` ディレクトリ内に作成され、`enabled_farms` ディレクトリ内のシンボリックリンクで有効になります。`.farm` ファイルから、フィルター、キャッシュルールなどその他のファイルがインクルードされます。

* `conf.dispatcher.d/cache/rules.any`

このファイルは、`.farm` ファイル内からインクルードされます。キャッシュの環境設定を指定します。

* `conf.dispatcher.d/clientheaders/clientheaders.any`

このファイルは、`.farm` ファイル内からインクルードされます。バックエンドに転送する必要があるリクエストヘッダーを指定します。

* `conf.dispatcher.d/filters/filters.any`

このファイルは、`.farm` ファイル内からインクルードされます。このルールには、トラフィックを除去してバックエンドに送らないように変更する一連のルールが含まれています。

* `conf.dispatcher.d/virtualhosts/virtualhosts.any`

このファイルは、`.farm` ファイル内からインクルードされます。グロブマッチングで一致するホスト名または URI パスのリストが含まれます。これにより、リクエストの処理に使用するバックエンドが決まります。

上記のファイルは、以下に示す不変設定ファイルを参照します。不変設定ファイルに対する変更は、クラウド環境の Dispatcher によって処理されません。

**不変設定ファイル**

これらのファイルは基本フレームワークの一部であり、標準とベストプラクティスを補強します。ファイルをローカルで変更または削除しても、クラウドインスタンスに転送されず、デプロイメントに影響を与えないので、これらのファイルは不変と見なされます。

上記のファイルは、以下に示す不変ファイルを参照し、その後に追加のステートメントまたはオーバーライドを参照することをお勧めします。Dispatcher 設定をクラウド環境にデプロイすると、ローカル開発で使用されたバージョンに関係なく、不変ファイルの最新バージョンが使用されます。

* `conf.d/available_vhosts/default.vhost`

仮想ホストのサンプルが含まれています。お使いの仮想ホストに対して、このファイルのコピーを作成し、カスタマイズしてから `conf.d/enabled_vhosts` に移動し、カスタマイズしたコピーのシンボリックリンクを作成します。

* `conf.d/dispatcher_vhost.conf`

基本フレームワークの一部です。仮想ホストとグローバル変数のインクルード方法を説明するために使用します。

* `conf.d/rewrites/default_rewrite.rules`

デフォルトの書き換えルールです。標準プロジェクトに適しています。カスタマイズが必要な場合は、`rewrite.rules` を変更します。必要に応じて、カスタマイズの最初にデフォルトのルールをインクルードすることができます。

* `conf.dispatcher.d/available_farms/default.farm`

サンプルの Dispatcher ファームが含まれています。ユーザー自身のファームの場合は、このファイルのコピーを作成してカスタマイズし、`conf.d/enabled_farms` に移動して、カスタマイズしたコピーのシンボリックリンクを作成します。

* `conf.dispatcher.d/cache/default_invalidate.any`

基本フレームワークの一部です。起動時に生成されます。このファイルは、定義したすべてのファームの `cache/allowedClients` セクションにインクルードする&#x200B;**必要があります**。

* `conf.dispatcher.d/cache/default_rules.any`

デフォルトのキャッシュルールです。標準プロジェクトに適しています。カスタマイズが必要な場合は、`conf.dispatcher.d/cache/rules.any` を変更します。必要に応じて、カスタマイズの最初にデフォルトのルールをインクルードすることができます。

* `conf.dispatcher.d/clientheaders/default_clientheaders.any`

バックエンドに転送するデフォルトの要求ヘッダーです。標準プロジェクトに適しています。カスタマイズが必要な場合は、`clientheaders.any` を変更します。カスタマイズでは、必要に応じて、デフォルトのリクエストヘッダーを最初にインクルードすることができます。

* `conf.dispatcher.d/dispatcher.any`

基本フレームワークの一部です。Dispatcher ファームのインクルード方法を説明するために使用します。

* `conf.dispatcher.d/filters/default_filters.any`

デフォルトのフィルターです。標準プロジェクトに適しています。カスタマイズが必要な場合は、`filters.any` を変更します。必要に応じて、カスタマイズの最初にデフォルトのフィルターをインクルードすることができます。

* `conf.dispatcher.d/renders/default_renders.any`

基本フレームワークの一部です。このファイルは起動時に生成されます。このファイルは、定義したすべてのファームの `renders` セクションにインクルードする&#x200B;**必要があります**。

* `conf.dispatcher.d/virtualhosts/default_virtualhosts.any`

デフォルトのホストグロビングです。標準プロジェクトに適しています。カスタマイズが必要な場合は、`virtualhosts.any` を変更します。**すべての**&#x200B;受信リクエストに一致することから、カスタマイズには、デフォルトのホストグロビングをインクルードしないでください。

>[!NOTE]
>
>AEM as a Cloud Service の Maven アーキタイプは、同じ Dispatcher 設定ファイル構造を生成します。

以下では、内部リリースのデプロイ時に Cloud Manager で関連付けられた品質ゲートを渡せるように、設定をローカルで検証する方法について説明します。

## Dispatcher 設定でサポートされているディレクティブのローカル検証 {#local-validation-of-dispatcher-configuration}

検証ツールは、Mac OS、Linux または Windows バイナリとして `bin/validator` の SDK で使用可能で、リリースのビルドとデプロイ時に Cloud Manager が実行する検証と同じものが実行できます。

次のように呼び出します：`validator full [-d folder] [-w allowlist] zip-file | src folder`

このツールでは、パターン `conf.d/enabled_vhosts/*.vhost` に一致するすべてのファイルをスキャンして、AEM as a Cloud Service でサポートされている適切なディレクティブが Dispatcher 設定で使用されているかどうかを検証します。

Windows の場合、Dispatcher バリデーターでは大文字と小文字が区別されます。そのため、次のように、設定が存在するパスの大文字と小文字を区別しない場合は、設定の検証に失敗する可能性があります。

```
bin\validator.exe full src
Cloud manager validator 2.0.xx
2021/03/15 18:15:40 Dispatcher configuration validation failed:
  conf.dispatcher.d\available_farms\default.farm:15: parent directory outside server root: c:\k\a\aem-dispatcher-sdk-windows-symlinks-testing3\dispatcher\src
  
```

このエラーを回避するには、Windows エクスプローラでパスをコピーし、コマンドプロンプトで `cd` コマンドを使用してそのパスに貼り付けます。

Apache の設定ファイルで許可されているディレクティブは、バリデーターの許可リストコマンドを実行すると表示できます。

```
$ validator allowlist
Cloud manager validator 2.0.4
 
Allowlisted directives:
  <Directory>
  ...
  
```

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

お客様が任意のモジュールを追加することはできませんが、今後、上述の表にある以外のモジュールが追加で製品に組み込まれる可能性があります。前述のように、SDK でバリデーターの許可リストコマンドを実行すると、特定の Dispatcher バージョンで使用できるディレクティブのリストを確認できます。

許可リストには、お客様の設定で許可される Apache ディレクティブのリストが含まれています。ディレクティブが許可リストに登録されていない場合、ツールはエラーをログに記録し、ゼロ以外の終了コードを返します。（ツール実行時の）コマンドラインに許可リストが設定されていない場合、デフォルトの許可リストが使用されます。これは、クラウド環境にデプロイする前に Cloud Manager が検証に使用するものです。

また、`conf.dispatcher.d/enabled_farms/*.farm` のパターンに合うすべてのファイルをさらにスキャンし、次の内容を確認します。

* `/glob` 経由の許可を使用するフィルタールールが存在しないこと（詳しくは、[CVE-2016-0957](https://nvd.nist.gov/vuln/detail/CVE-2016-0957) を参照）
* 管理機能が公開されないこと。例えば、`/crx/de or /system/console` などのパスへのアクセス。

Maven アーティファクトまたは `dispatcher/src` サブディレクトリに対して実行すると、検証エラーが報告されます。

```
$ validator full dispatcher/src
Cloud manager validator 1.0.4
2019/06/19 15:41:37 Apache configuration uses non-allowlisted directives:
  conf.d/enabled_vhosts/aem_publish.vhost:46: LogLevel
2019/06/19 15:41:37 Dispatcher configuration validation failed:
  conf.dispatcher.d/enabled_farms/999_ams_publish_farm.any: filter allows access to CRXDE
```

検証ツールは、許可リストに登録されていない Apache ディレクティブの使用禁止を報告するのみということに注意してください。Apache 設定の構文や意味の問題は報告されません。この情報は、実行中の環境の Apache モジュールでのみ利用できます。

ツールによって出力される一般的な検証エラーをデバッグする場合のトラブルシューティング手法を次に示します。

**unable to locate a `conf.dispatcher.d` subfolder in the archive**

アーカイブには、`conf.d` フォルダーと `conf.dispatcher.d` フォルダーが含まれている必要があります。アーカイブにはプレフィックス `etc/httpd` を&#x200B;**使用しないでください**。

**unable to find any farm in`conf.dispatcher.d/enabled_farms`**

有効なファームは、前述のサブフォルダーに置く必要があります。

**file included (...) must be named: ...**

ファーム設定には 2 つのセクションがあり、`/cache` セクションに特定のファイル `/renders` と `/allowedClients` をインクルードする&#x200B;**必要があります**。それらのセクションは、次のようになります。

```
/renders {
    $include "../renders/default_renders.any"
}
```

および

```
/allowedClients {
    $include "../cache/default_invalidate.any"
}
```

**file included at unknown location: ...**

ファーム設定には、独自のファイルをインクルードできる 4 つのセクション、`/clientheaders`、`filters`、`/cache` セクションの `/rules`、および `/virtualhosts` があります。インクルードされるファイルの名前は、次のように指定する必要があります。

| セクション | インクルードファイル名 |
|------------------|--------------------------------------|
| `/clientheaders` | `../clientheaders/clientheaders.any` |
| `/filters` | `../filters/filters.any` |
| `/rules` | `../cache/rules.any` |
| `/virtualhosts` | `../virtualhosts/virtualhosts.any` |

また、`../filters/default_filters.any` のように、名前の前に `default_` が付いた&#x200B;**デフォルト**&#x200B;バージョンのファイルをインクルードすることもできます。

**include statement at (...), outside any known location: ...**

上記の 6 つのセクション以外では、`$include` ステートメントを使用できません。例えば、次のような場合に、このエラーが発生します。

```
/invalidate {
    $include "../cache/invalidate.any"
}
```

**allowed clients/renders are not included from: ...**

このエラーは、`/renders` および `/allowedClients` のインクルードを `/cache` セクションで指定しない場合に発生します。**file included (...) must be named: ...** の節を参照してください。

**filter must not use glob pattern to allow requests**

`/glob` スタイルのルールによるリクエストの許可は安全ではありません。このルールはリクエストライン全体に一致します。以下に例を示します。

```
/0100 {
    /type "allow" /glob "GET *.css *"
}
```

このステートメントは、`css` ファイルのリクエストを許可するものですが、クエリ文字列 `?a=.css` の前に付くン&#x200B;**あらゆる**&#x200B;リソースに対するリクエストも許可してしまいます。したがって、このようなフィルターの使用は禁止されています（CVE-2016-0957 も参照してください）。

**included file (...) does not match any known file**

Apache 仮想ホスト設定には、インクルードとして指定できる 2 つのタイプのファイル（書き換えと変数）があります。
インクルードされるファイルの名前は、次のように指定する必要があります。

| タイプ | インクルードファイル名 |
|-----------|---------------------------------|
| 書き換え | `conf.d/rewrites/rewrite.rules` |
| 変数 | `conf.d/variables/custom.vars` |

または、`conf.d/rewrites/default_rewrite.rules` という名前の、書き換えルールの&#x200B;**デフォルト**バージョンをインクルードすることもできます。
変数ファイルにはデフォルトバージョンはありません。

**非推奨の設定レイアウトを検出したので互換モードを有効にします**

このメッセージは、非推奨（廃止予定）のバージョン 1 レイアウトが設定に含まれ、完全な Apache 設定と `ams_` プレフィックス付きのファイルが含まれていることを示します。これは後方向に対して引き続きサポートされますが、
互換性がある場合は、新しいレイアウトに切り替える必要があります。

## Apache httpd を起動するための Dispatcher 設定構文のローカル検証 {#local-validation}

サポートされているディレクティブのみ Dispatcher モジュール設定に含まれていることがわかったら、Apache を起動できるように、構文が正しいことを確認してください。このテストを行うには、Docker をローカルにインストールする必要があります。AEM が動作している必要はありません。

`validate.sh` スクリプトを次のように使用します。

```
$ validate.sh src/dispatcher
Phase 1: Dispatcher validator
2019/06/19 16:02:55 No issues found
Phase 1 finished
Phase 2: httpd -t validation in docker image
Running script /docker_entrypoint.d/10-create-docroots.sh
Running script /docker_entrypoint.d/20-wait-for-backend.sh
Waiting until aemhost is available
aemhost resolves to xx.xx.xx.xx
Running script /docker_entrypoint.d/30-allowed-clients.sh
# Dispatcher configuration: (/etc/httpd/conf.dispatcher.d/dispatcher.any)
/farms {
...
}
Syntax OK
Phase 2 finished
```

このスクリプトは次の処理を行います。

1. 前の節で説明したバリデーターを実行して、サポートされているディレクティブのみ含まれていることを確認します。設定が有効でない場合、スクリプトは失敗します。
2. Apache httpd を起動できるように、`httpd -t command` を実行して、構文が正しいかどうかをテストします。テストが成功した場合は、設定をデプロイする準備が整っています。
3. 「[ファイル構造](#file-structure)」節で説明されているようにで不変であることが意図されている、Dispatcher SDK 設定ファイルのサブセットが変更されていないことを確認します。これは、Dispatcher ツールバージョン 2.0.36 を含む AEM SDK バージョン v2021.1.4738 で導入された新しいチェックです。この更新前には、これらの不変ファイルのローカル SDK での変更がクラウド環境にも適用されると誤って想定されていました。

Cloud Manager によるデプロイ中に、`httpd -t syntax` のチェックも実行され、エラーは Cloud Manager の `Build Images step failure` ログに記録されます。

## Apache および Dispatcher 設定のローカルでのテスト {#testing-apache-and-dispatcher-configuration-locally}

Apache と Dispatcher の設定をローカルでテストすることもできます。前述のように、Docker をローカルにインストールし、設定が検証に合格する必要があります。

すべての Dispatcher 設定ファイルを含んだフォルダーを出力する `-d` パラメーターを使用して、検証ツール（前述の `validator.sh` とは異なります）を実行します。次に、そのフォルダーを引数として渡して `docker_run.sh` スクリプトを実行します。Dispatcher エンドポイントを公開するためのポート番号（ここでは 8080）を指定することで、Docker コンテナが起動され、所定の設定で Dispatcher が実行されます。

```
$ validator full -d out src/dispatcher
2019/06/19 16:02:55 No issues found
$ docker_run.sh out docker.for.mac.localhost:4503 8080
Running script /docker_entrypoint.d/10-create-docroots.sh
Running script /docker_entrypoint.d/20-wait-for-backend.sh
Waiting until aemhost is available
aemhost resolves to xx.xx.xx.xx
Running script /docker_entrypoint.d/30-allowed-clients.sh
Starting httpd server
...
```

これにより、コンテナ内の Dispatcher が開始し、そのバックエンドは、ローカルの Mac OS マシンのポート 4503 で実行される AEM インスタンスを指すようになります。

## Apache および Dispatcher 設定のデバッグ {#debugging-apache-and-dispatcher-configuration}

次の方法を使用して、Dispatcher モジュールのログ出力を増やし、`RewriteRule` 評価の結果をローカル環境とクラウド環境の両方で確認できます。

これらのモジュールのログレベルは、変数の `DISP_LOG_LEVEL` と `REWRITE_LOG_LEVEL` によって定義されます。これらは、`conf.d/variables/global.vars` ファイルに設定できます。関連する箇所は以下のとおりです。

```
# Log level for the dispatcher
#
# Possible values are: Error, Warn, Info, Debug and Trace1
# Default value: Warn
#
# Define DISP_LOG_LEVEL Warn
 
# Log level for mod_rewrite
#
# Possible values are: Error, Warn, Info, Debug and Trace1 - Trace8
# Default value: Warn
#
# To debug your RewriteRules, it is recommended to raise your log
# level to Trace2.
#
# More information can be found at:
# https://httpd.apache.org/docs/current/mod/mod_rewrite.html#logging
#
# Define REWRITE_LOG_LEVEL Warn
```

Dispatcher をローカルで実行すると、ログが端末に直接出力されます。ほとんどの場合、これらのログは DEBUG モードで出力すべきもので、それには、Docker の実行時にデバッグレベルをパラメーターとして渡します。例：`DISP_LOG_LEVEL=Debug ./bin/docker_run.sh out docker.for.mac.localhost:4503 8080`

クラウド環境のログは、Cloud Manager で利用可能なログサービスを通じて公開されます。

## 環境ごとに異なる Dispatcher 設定 {#different-dispatcher-configurations-per-environment}

現時点では、すべての AEM as a Cloud Service 環境に同じ Dispatcher 設定が適用されます。ランタイムには、現在の実行モード（dev、stage または prod）と定義を含む環境変数 `ENVIRONMENT_TYPE` が含まれます。定義は、`ENVIRONMENT_DEV`、`ENVIRONMENT_STAGE`、または `ENVIRONMENT_PROD` のいずれかです。Apache 設定では、変数を式に直接使用できます。または、定義を使用してロジックをビルドできます。

```
# Simple usage of the environment variable
ServerName ${ENVIRONMENT_TYPE}.company.com
 
# When more logic is required
<IfDefine ENVIRONMENT_STAGE>
  # These statements are for stage
  Define VIRTUALHOST stage.example.com
</IfDefine>
<IfDefine ENVIRONMENT_PROD>
  # These statements are for production
  Define VIRTUALHOST prod.example.com
</IfDefine>
```

Dispatcher 設定では、同じ環境変数が使用できます。さらにロジックが必要な場合は、上の例で示すように変数を定義し、Dispatcher 設定セクションで使用します。

```
/virtualhosts {
  { "${VIRTUALHOST}" }
}
```

設定をローカルでテストする場合、`DISP_RUN_MODE` 変数を `docker_run.sh` スクリプトに直接渡すことで、様々な環境タイプをシミュレートできます。

```
$ DISP_RUN_MODE=stage docker_run.sh out docker.for.mac.localhost:4503 8080
```

DISP_RUN_MODE の値を渡さない場合のデフォルトの実行モードは「dev」です。
使用可能なオプションと変数の完全なリストについては、`docker_run.sh` スクリプトを引数なしで実行してください。

## Docker コンテナで使用中の Dispatcher 設定の表示 {#viewing-dispatcher-configuration-in-use-by-docker-container}

環境固有の設定では、実際の Dispatcher 設定がどのようになるのかを判断するのが困難な場合があります。`docker_run.sh` を使用して Docker コンテナを起動したら、次のようにダンプできます。

* 使用中の Docker コンテナ ID を特定します。

```
$ docker ps
CONTAINER ID       IMAGE
d75fbd23b29        adobe/aem-ethos/dispatcher-publish:...
```

* 特定したコンテナ ID で、次のコマンドラインを実行します。

```
$ docker exec d75fbd23b29 httpd-test
# Dispatcher configuration: (/etc/httpd/conf.dispatcher.d/dispatcher.any)
/farms {
  /publishfarm {
    /clientheaders {
...
```

## AMS Dispatcher と AEM as a Cloud Service の主な違い {#main-differences-between-ams-dispatcher-configuration-and-aem-as-a-cloud-service}

上記の参照ページで説明したように、AEM as a Cloud Service の Apache および Dispatcher の設定は、AMS のそれらの設定と非常に似ています。主な違いは次のとおりです。

* AEM as a Cloud Service では、一部の Apache ディレクティブ（例えば、`Listen` または `LogLevel`）が使用されません。
* AEM as a Cloud Service では、Dispatcher 設定の一部のみがインクルードファイルに置かれ、名前付けが重要です。例えば、異なるホスト間で再利用するフィルタールールは、`filters/filters.any` という名前のファイルに入れる必要があります。詳しくは、参照ページを参照してください。
* AEM as a Cloud Service には、セキュリティの問題を防ぐために、`/glob` を使用して記述されたフィルタールールを無効にする、追加の検証があります。（使用できない）`allow *`の代わりに `deny *` が使用されるので、Dispatcher をローカルで実行して、トライアンドエラーを繰り返し、Dispatcher フィルターがブロックしているパスをログから調べて、それらを追加します。

## Dispatcher 設定の AMS から AEM as a Cloud Service への移行に関するガイドライン

Dispatcher 設定の構造は、Managed Services と AEM as a Cloud Service との間に違いがあります。以下に、AMS Dispatcher の設定バージョン 2 から AEM as Cloud Service への移行方法を順を追って示します。

## AMS を AEM as a Cloud service の Dispatcher 設定に変換する方法

AMS 設定を変換する方法を順を追って説明します。ここでは、[Cloud Manager の Dispatcher 設定](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/getting-started/dispatcher-configurations.html)で説明した構造と同様な構造のアーカイブがあることを前提としています。

### アーカイブを抽出し、最終的なプレフィックスを削除する

アーカイブをフォルダーに抽出し、直下のサブフォルダーが、`conf`、`conf.d`、`conf.dispatcher.d` および `conf.modules.d` で始まっていることを確認します。そうでない場合は、それらを階層の上に移動します。

### 未使用のサブフォルダーとファイルを削除する

サブフォルダーの `conf` と `conf.modules.d`、および `conf.d/*.conf` と一致するファイルを削除します。

### 非公開の仮想ホストをすべて排除する

`conf.d/enabled_vhosts` 内の、名前に `author`、`unhealthy`、`health`、`lc` または `flush` が含まれる仮想ホストファイルを削除します。`conf.d/available_vhosts` 内の、リンクされていないすべての仮想ホストファイルも削除できます。

### ポート 80 を参照しない仮想ホストセクションを削除またはコメント化する

仮想ホストファイルに、ポート 80 以外のポートを排他的に参照するセクションが、次の例のように残っている場合：

```
<VirtualHost *:443>
...
</VirtualHost>
```

削除するか、コメント化します。これらのセクションのステートメントは処理されませんが、そのままにしておくと、効果がないのに編集してしまう可能性があり、混乱の元になります。

### 書き換えを確認する

`conf.d/rewrites` ディレクトリに入ります。

`base_rewrite.rules` と `xforwarded_forcessl_rewrite.rules` という名前のファイルをすべて削除します。また、それらを参照する仮想ホストファイル内の `Include` ステートメントを削除することを忘れないでください。

`conf.d/rewrites` に 1 つのファイルのみ含まれる場合は、そのファイルの名前を `rewrite.rules` に変更します。また、仮想ホストファイル内にそのファイルを参照する `Include` ステートメントを必ず追加するようにしてください。

ただし、フォルダーに複数の仮想ホスト固有のファイルが含まれている場合は、そのファイルの内容を、仮想ホストファイル内のファイルを参照する `Include` ステートメントにコピーする必要があります。

### 変数を確認する

`conf.d/variables` ディレクトリに入ります。

`ams_default.vars` という名前のファイルをすべて削除し、それらを参照する仮想ホストファイル内の `Include` ステートメントを忘れずに削除してください。

`conf.d/variables` に 1 つのファイルのみ含まれる場合は、そのファイルの名前を `custom.vars` に変更します。また、仮想ホストファイル内にそのファイルを参照する `Include` ステートメントを必ず追加するようにしてください。

ただし、フォルダーに複数の仮想ホスト固有のファイルが含まれている場合は、そのファイルの内容を、仮想ホストファイル内のファイルを参照する `Include` ステートメントにコピーする必要があります。

### 許可リストの削除

`conf.d/whitelists` フォルダーを削除し、そのサブフォルダー内のファイルを参照する仮想ホストファイル内の `Include` ステートメントを削除します。

### 使用できなくなった変数を置き換える

すべての仮想ホストファイルで以下を行います。

`PUBLISH_DOCROOT` を `DOCROOT` に名前変更して、`DISP_ID`、`PUBLISH_FORCE_SSL`、`PUBLISH_WHITELIST_ENABLED` という名前の変数を参照するセクションを削除します。

### バリデーターを実行して状態を確認する

ディレクトリ内の Dispatcher バリデーターをサブコマンド `httpd` と共に実行します。

```
$ validator httpd .
```

インクルードファイルが見つからないことに関するエラーが表示される場合は、それらのファイルの名前を正しく変更したかどうかを確認します。

許可リストに登録されていない Apache ディレクティブが表示された場合は、それらを削除します。

### 非公開ファームをすべて削除する

`conf.dispatcher.d/enabled_farms` 内の、名前に `author`、`unhealthy`、`health`、`lc` または `flush` が含まれるファームファイルを削除します。`conf.dispatcher.d/available_farms` 内のリンクされていないファームファイルも、すべて削除できます。

### ファームファイルの名前を変更する

`conf.d/enabled_farms` 内のすべてのファーム名は、`*.farm` のパターンに合わせて変更する必要があります。例えば、`customerX_farm.any` という名前のファームファイル名は、`customerX.farm` に変更します。

### キャッシュを確認する

`conf.dispatcher.d/cache` ディレクトリに入ります。

`ams_` のプレフィックスが付いたファイルを削除します。

`conf.dispatcher.d/cache` が空になった場合は、標準の Dispatcher 設定からこのフォルダーに `conf.dispatcher.d/cache/rules.any` ファイルをコピーします。標準の Dispatcher 設定は、この SDK の `src` フォルダーにあります。ファームファイル内の `ams_*_cache.any` ルールファイルを参照する `$include` ステートメントも、必ず適応させます。

`conf.dispatcher.d/cache` ではなく、サフィックス付きの単一のファイル `_cache.any` が含まれている場合、`rules.any` に名前変更し、ファームファイル内のそのファイルを参照する `$include` ステートメントも必ず適応させます。

ただし、フォルダーにそのパターンを持つファーム固有のファイルが複数含まれている場合は、そのファイルの内容を、ファームファイル内のファイルを参照する `$include` ステートメントにコピーする必要があります。

`_invalidate_allowed.any` サフィックスを持つファイルを削除します。

Cloud Dispatcher 設定のデフォルト AEM からその場所に `conf.dispatcher.d/cache/default_invalidate_any` ファイルをコピーします。

各ファームファイルで、`cache/allowedClients` セクション内のコンテンツを削除し、次と置き換えます。

```
$include "../cache/default_invalidate.any"
```

### クライアントヘッダーを確認する

`conf.dispatcher.d/clientheaders` ディレクトリに入ります。

`ams_` のプレフィックスが付いたファイルを削除します。

`conf.dispatcher.d/clientheaders` に、サフィックス付きの単一のファイル `_clientheaders.any` が含まれている場合、`clientheaders.any` に名前変更し、ファームファイル内のそのファイルを参照する `$include` ステートメントも必ず適応させます。

ただし、フォルダーにそのパターンを持つファーム固有のファイルが複数含まれている場合は、そのファイルの内容を、ファームファイル内のファイルを参照する `$include` ステートメントにコピーする必要があります。

デフォルトの AEM as a Cloud Service の Dispatcher 設定からその場所に `conf.dispatcher/clientheaders/default_clientheaders.any` ファイルをコピーします。

各ファームファイルで、次のような clientheader インクルードステートメントを置き換えます。

```
$include "/etc/httpd/conf.dispatcher.d/clientheaders/ams_publish_clientheaders.any"
$include "/etc/httpd/conf.dispatcher.d/clientheaders/ams_common_clientheaders.any"
```

次のステートメントに置き換えます。

```
$include "../clientheaders/default_clientheaders.any"
```

### フィルターを確認する

`conf.dispatcher.d/filters` ディレクトリに入ります。

`ams_` のプレフィックスが付いたファイルを削除します。

`conf.dispatcher.d/filters` に 1 つのファイルのみ含まれる場合は、そのファイルの名前を `filters.any` に変更します。また、ファームファイル内にそのファイルを参照する `$include` ステートメントを必ず追加するようにしてください。

ただし、フォルダーにそのパターンを持つファーム固有のファイルが複数含まれている場合は、そのファイルの内容を、ファームファイル内のファイルを参照する `$include` ステートメントにコピーする必要があります。

デフォルトの AEM as a Cloud Service の Dispatcher 設定からその場所に `conf.dispatcher/filters/default_filters.any` ファイルをコピーします。

各ファームファイルで、次のようなフィルターインクルードステートメントを

```
$include "/etc/httpd/conf.dispatcher.d/filters/ams_publish_filters.any"
```

次のステートメントに置き換えます。

```
$include "../filters/default_filters.any"
```

### レンダリングを確認する

`conf.dispatcher.d/renders` ディレクトリに入ります。

フォルダー内のすべてのファイルを削除します。

デフォルトの AEM as a Cloud Service の Dispatcher 設定からその場所に `conf.dispatcher.d/renders/default_renders.any` ファイルをコピーします。

各ファームファイルで、`renders` セクション内のコンテンツを削除し、次と置き換えます。

```
$include "../renders/default_renders.any"
```

### 仮想ホストを確認する

`conf.dispatcher.d/vhosts` ディレクトリの名前を `conf.dispatcher.d/virtualhosts` に変更し、そこに入ります。

`ams_` のプレフィックスが付いたファイルを削除します。

`conf.dispatcher.d/virtualhosts` に 1 つのファイルのみ含まれる場合は、そのファイルの名前を `virtualhosts.any` に変更します。また、ファームファイル内にそのファイルを参照する `$include` ステートメントを必ず追加するようにしてください。

ただし、フォルダーにそのパターンを持つファーム固有のファイルが複数含まれている場合は、そのファイルの内容を、ファームファイル内のファイルを参照する `$include` ステートメントにコピーする必要があります。

デフォルトの AEM as a Cloud Service の Dispatcher 設定からその場所に `conf.dispatcher/virtualhosts/default_virtualhosts.any` ファイルをコピーします。

各ファームファイルで、次のようなフィルターインクルードステートメントを

```
$include "/etc/httpd/conf.dispatcher.d/vhosts/ams_publish_vhosts.any"
```

次のステートメントに置き換えます。

```
$include "../virtualhosts/default_virtualhosts.any"
```

### バリデーターを実行して状態を確認する

ディレクトリ内の AEM as a Cloud Service Dispatcher バリデーターをサブコマンド `dispatcher` と共に実行します。

```
$ validator dispatcher .
```

インクルードファイルが見つからないことに関するエラーが表示される場合は、それらのファイルの名前を正しく変更したかどうかを確認します。

未定義の変数 `PUBLISH_DOCROOT` に関するエラーが表示される場合は、名前を `DOCROOT` に変更します。

その他のエラーについては、バリデーターツールのドキュメントの「トラブルシューティング」の節を参照してください。

### ローカルデプロイメントで設定をテストする（Docker のインストールが必要）

AEM as a Cloud Service Dispatcher ツールのスクリプト `docker_run.sh` を使用して、デプロイのみに表れる他のエラーが設定に含まれていないことをテストできます。

### 手順 1：バリデーターを使用してデプロイメント情報を生成する

```
validator full -d out .
```

設定を完全に検証し、`out` にデプロイメント情報が生成されます。

### 手順 2：生成されたデプロイメント情報を使用して、Docker イメージで Dispatcher を起動する

AEM パブリッシュサーバーを macOS コンピューター上で実行し、ポート 4503 をリッスンしている場合は、次のように、そのサーバーの前で Dispatcher を実行できます。

```
$ docker_run.sh out docker.for.mac.localhost:4503 8080
```

これにより、コンテナが起動し、ローカルポート 8080 で Apache が公開されます。

### 新しい Dispatcher 設定の使用

バリデーターが問題を報告しなくなり、Docker コンテナがエラーや警告を出さずに起動した場合、設定を Git リポジトリーのサブディレクトリ `dispatcher/src` に移動する準備が整いました。

**AMS Dispatcher 設定のバージョン 1 を使用しているお客様は、カスタマーサポートにお問い合わせください。上記の手順が実施できるように、バージョン 1 からバージョン 2 へ移行できるように支援いたします。**
