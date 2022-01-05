---
title: Dispatcher ツールを使用した検証とデバッグ
description: Dispatcher ツールを使用した検証とデバッグ
feature: Dispatcher
exl-id: 9e8cff20-f897-4901-8638-b1dbd85f44bf
source-git-commit: 03fa3601c7819d469bf4d532ff5020aad0ea7ed9
workflow-type: tm+mt
source-wordcount: '2413'
ht-degree: 99%

---

# Dispatcher ツールを使用した検証とデバッグ {#Dispatcher-in-the-cloud}

## はじめに {#apache-and-dispatcher-configuration-and-testing}

>[!NOTE]
>クラウド内の Dispatcher と Dispatcher ツールのダウンロード方法について詳しくは、 [クラウド内の Dispatcher](/help/implementing/dispatcher/disp-overview.md) ページ。 Dispatcher 設定がレガシーモードの場合は、[レガシーモードのドキュメント](/help/implementing/dispatcher/validation-debug-legacy.md)を参照してください。

以降の節では、フレキシブルモードのファイル構造、ローカル検証、デバッグ、レガシーモードからフレキシブルモードへの移行について説明します。

ここでは、プロジェクトの Dispatcher 設定に `opt-in/USE_SOURCES_DIRECTLY` ファイルが含まれていることを前提としています。これにより、ファイルの数とサイズに関する制限がなくなり、SDK とランタイムによる設定の検証とデプロイが、レガシーモードと比べて改善されます。

したがって、Dispatcher 設定に前述のファイルが含まれていない場合は、[レガシーモードからフレキシブルモードへの移行](#migrating)の節の説明に従って、レガシーモードからフレキシブルモードへ移行することを&#x200B;**強くお勧め**&#x200B;します。

## ファイル構造 {#flexible-mode-file-structure}

プロジェクトの Dispatcher サブフォルダーの構造は次のとおりです。

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
│── opt-in
│   └── USE_SOURCES_DIRECTLY
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
    │   ├── default_virtualhosts.any
    │   └── virtualhosts.any
    
```

以下に、変更可能な注目すべきファイルを示します。

**カスタマイズ可能なファイル**

以下のファイルはカスタマイズ可能で、デプロイ時にクラウドインスタンスに転送されます。

* `conf.d/available_vhosts/<CUSTOMER_CHOICE>.vhost`

これらのファイルは 1 つ以上持つことができます。ファイルには、ホスト名に一致する `<VirtualHost>` エントリが含まれ、Apache が異なるルールで各ドメイントラフィックを扱うことができます。ファイルは `available_vhosts` ディレクトリ内に作成され、`enabled_vhosts` ディレクトリ内のシンボリックリンクで有効になります。`.vhost` ファイルから、書き換えや変数などその他のファイルがインクルードされます。

* `conf.d/rewrites/rewrite.rules`

このファイルは、`.vhost` ファイル内からインクルードされます。`mod_rewrite` には一連の書き換えルールがあります。

* `conf.d/variables/custom.vars`

このファイルは、`.vhost` ファイル内からインクルードされます。Apache 変数用の定義をこの場所に追加できます。

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

* `opt-in/USE_SOURCES_DIRECTLY`

このファイルにより、より柔軟な Dispatcher 設定が可能になり、ファイルの数とサイズに関する以前の制限がなくなります。また、SDK とランタイムによる設定の検証とデプロイも改善されます。

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

## サポートされている Apache モジュール {#apache-modules}

[サポートされている Apache モジュール](/help/implementing/dispatcher/disp-overview.md#supported-directives)を参照してください。

## ローカル検証 {#local-validation-flexible-mode}

>[!NOTE]
>
>以下では、Mac バージョンまたは Linux バージョンの SDK を使用した場合のコマンドについて説明しますが、Windows バージョンの SDK の場合でも同様の方法で使用できます。

`validate.sh` スクリプトを次のように使用します。

```
$ validate.sh src/dispatcher
opt-in USE_SOURCES_DIRECTLY marker file detected
Phase 1: Dispatcher validator
Cloud manager validator 2.0.32
Phase 1 finished
Phase 2: httpd -t validation in docker image
values.csv not found in deployment folder: /Users/foo/src - using files in 'conf.d' and 'conf.dispatcher.d' subfolders directly
processing configuration subfolder: conf.d
processing configuration subfolder: conf.dispatcher.d
Running script /docker_entrypoint.d/10-check-environment.sh
Running script /docker_entrypoint.d/20-create-docroots.sh
Running script /docker_entrypoint.d/30-wait-for-backend.sh
Waiting until localhost is available
localhost resolves to ::1
Running script /docker_entrypoint.d/40-generate-allowed-clients.sh
Running script /docker_entrypoint.d/50-check-expiration.sh
Running script /docker_entrypoint.d/60-check-loglevel.sh
Running script /docker_entrypoint.d/70-check-forwarded-host-secret.sh
# Dispatcher configuration: (/etc/httpd/conf.dispatcher.d/dispatcher.any)
/farms {

... 

}
Syntax OK
Phase 2 finished
Phase 3: Immutability check
reading immutable file list from /etc/httpd/immutable.files.txt

...

no immutable file has been changed - check is SUCCESSFUL
Phase 3 finished
```

スクリプトには次の 3 つのフェーズがあります。

1. バリデーターを実行します。設定が有効でない場合、スクリプトは失敗します。
2. Apache httpd を起動できるように、`httpd -t` コマンドを実行して、構文が正しいかどうかをテストします。テストが成功した場合は、設定をデプロイする準備が整っています.
3. 「[ファイル構造](##flexible-mode-file-structure)」節で説明されているようにで不変であることが意図されている、Dispatcher SDK 設定ファイルのサブセットが変更されていないことを確認します。

Cloud Manager によるデプロイ中に、`httpd -t` の構文チェックも実行され、エラーは Cloud Manager の `Build Images step failure` ログに記録されます。

### フェーズ 1 {#first-phase}

ディレクティブが許可リストに登録されていない場合、ツールはエラーをログに記録し、ゼロ以外の終了コードを返します。また、`conf.dispatcher.d/enabled_farms/*.farm` のパターンに合うすべてのファイルをさらにスキャンし、次の内容を確認します。

* `/glob` 経由の許可を使用するフィルタールールが存在しないこと（詳しくは、[CVE-2016-0957](https://nvd.nist.gov/vuln/detail/CVE-2016-0957) を参照）。
* 管理機能が公開されないこと。例えば、`/crx/de or /system/console` などのパスへのアクセス。

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

このメッセージは、非推奨（廃止予定）のバージョン 1 レイアウトが設定に含まれ、完全な Apache 設定と `ams_` プレフィックス付きのファイルが含まれていることを示します。これは下位互換性のために引き続きサポートされますが、新しいレイアウトに切り替える必要があります。

フェーズ 1 は、ラッパースクリプト `validate.sh` からではなく、**個別に実行**&#x200B;することもできます。

Maven アーティファクトまたは `dispatcher/src` サブディレクトリに対して実行すると、検証エラーが報告されます。

```
$ validator full -relaxed dispatcher/src
Cloud manager validator 1.0.4
2019/06/19 15:41:37 Apache configuration uses non-allowlisted directives:
  conf.d/enabled_vhosts/aem_publish.vhost:46: LogLevel
2019/06/19 15:41:37 Dispatcher configuration validation failed:
  conf.dispatcher.d/enabled_farms/999_ams_publish_farm.any: filter allows access to CRXDE
```

Windows の場合、Dispatcher バリデーターでは大文字と小文字が区別されます。そのため、次のように、設定が存在するパスの大文字と小文字を区別しない場合は、設定の検証に失敗する可能性があります。

```
bin\validator.exe -relaxed full src
Cloud manager validator 2.0.xx
2021/03/15 18:15:40 Dispatcher configuration validation failed:
  conf.dispatcher.d\available_farms\default.farm:15: parent directory outside server root: c:\k\a\aem-dispatcher-sdk-windows-symlinks-testing3\dispatcher\src
```

このエラーを回避するには、Windows エクスプローラでパスをコピーし、コマンドプロンプトで `cd` コマンドを使用してそのパスに貼り付けます。

### フェーズ 2 {#second-phase}

このフェーズでは、イメージで Docker を起動して Apache 構文をチェックします。Docker をローカルにインストールする必要がありますが、AEM を実行する必要はありません。

>[!NOTE]
>
>Windows ユーザーは、Docker をサポートする Windows 10 Professional またはその他のディストリビューションを使用する必要があります。これは、ローカルコンピューターで Dispatcher を実行およびデバッグする場合に必要な前提条件です。

このフェーズは、`bin/docker_run.sh src/dispatcher host.internal.docker:4503 8080` を使用して独立に実行することもできます。

Cloud Manager によるデプロイ中に、`httpd -t` の構文チェックも実行され、エラーは Cloud Manager の「イメージのビルド」ステップのエラーログに記録されます。

### フェーズ 3 {#third-phase}

このフェーズでエラーが発生した場合は、アドビが 1 つ以上の不変ファイルを変更したことを示しているので、対応する不変ファイルを、SDK の `src` ディレクトリで提供されている新しいバージョンに置き換える必要があります。以下のログサンプルは、この問題を示しています。

```
Phase 3: Immutability check
reading immutable file list from /etc/httpd/immutable.files.txt
(...)
checking existing 'conf.dispatcher.d/clientheaders/default_clientheaders.any' for changes
immutable file 'conf.dispatcher.d/clientheaders/default_clientheaders.any' has been changed:
--- /etc/httpd/conf.dispatcher.d/clientheaders/default_clientheaders.any
+++ /etc/httpd-actual/conf.dispatcher.d/clientheaders/default_clientheaders.any
@@ -40,4 +40,3 @@
"Sling-uploadmode"
"x-requested-with"
"If-Modified-Since"
-"Authorization"
** error: immutable file 'conf.dispatcher.d/clientheaders/default_clientheaders.any' has been changed!
  
```

このフェーズは、`bin/docker_immutability_check.sh src/dispatcher` を使用して独立に実行することもできます。

## Apache および Dispatcher 設定のデバッグ {#debugging-apache-and-dispatcher-configuration}

`./bin/docker_run.sh src/dispatcher docker.for.mac.localhost:4503 8080` を使用すれば、Apache Dispatcher をローカルで実行できます。

前述のとおり、Docker をローカルにインストールする必要がありますが、AEM を実行する必要はありません。Windows ユーザーは、Docker をサポートする Windows 10 Professional またはその他のディストリビューションを使用する必要があります。これは、ローカルコンピューターで Dispatcher を実行およびデバッグする場合に必要な前提条件です。

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

Dispatcher をローカルで実行すると、ログが端末に直接出力されます。ほとんどの場合、これらのログは DEBUG モードで出力すべきもので、それには、Docker の実行時にデバッグレベルをパラメーターとして渡します。（例：`DISP_LOG_LEVEL=Debug ./bin/docker_run.sh src docker.for.mac.localhost:4503 8080`）。

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
$ DISP_RUN_MODE=stage docker_run.sh src docker.for.mac.localhost:4503 8080
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

## レガシーモードからフレキシブルモードへの移行 {#migrating}

Cloud Manager 2021.7.0 リリースでは、新しい Cloud Manager プログラムは、[AEM アーキタイプ 28](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/overview.html?lang=ja) 以降を使用した Maven プロジェクト構造を生成します。これには **opt-in/USE_SOURCES_DIRECTLY** ファイルが含まれています。これにより、ファイルの数とサイズに関する[レガシーモード](/help/implementing/dispatcher/validation-debug-legacy.md)の以前の制限事項がなくなるので、SDK とランタイムによる設定の検証とデプロイも改善されます。Dispatcher 設定にこのファイルがない場合は、移行することを強くお勧めします。安全な移行を確実に行うには、次の手順に従います。

1. **ローカルテスト：**&#x200B;最新の Dispatcher ツール SDKを使用して、フォルダーおよびファイル `opt-in/USE_SOURCES_DIRECTLY` を追加します。この記事の「ローカル検証」の手順に従って、Dispatcher がローカルで動作するかどうかをテストします。
2. **クラウド開発テスト：**
   * 実稼動以外のパイプラインでクラウドの開発環境にデプロイされたファイル `opt-in/USE_SOURCES_DIRECTLY` を Git ブランチにコミットします。
   * Cloud Manager を使用して、クラウド開発環境にデプロイします。
   * 十分にテストします。変更内容を上位の環境にデプロイする前に、Apache および Dispatcher 設定が想定どおりに動作することを検証することが不可欠です。カスタム設定に関係するすべての動作を確認します。デプロイした Dispatcher 設定がカスタム設定を反映していないと思われる場合は、カスタマーサポートチケットを提出します。
3. **実稼動へのデプロイ：**
   * 実稼動パイプラインでクラウドのステージング環境および実稼動環境にデプロイされたファイル `opt-in/USE_SOURCES_DIRECTLY` を Git ブランチにコミットします。
   * Cloud Manager を使用してステージング環境にデプロイします。
   * 十分にテストします。変更内容を上位の環境にデプロイする前に、Apache および Dispatcher 設定が想定どおりに動作することを検証することが不可欠です。カスタム設定に関係するすべての動作を確認します。デプロイした Dispatcher 設定がカスタム設定を反映していないと思われる場合は、カスタマーサポートチケットを提出します。
   * Cloud Manager を使用して、実稼動環境へのデプロイメントを続行します。
