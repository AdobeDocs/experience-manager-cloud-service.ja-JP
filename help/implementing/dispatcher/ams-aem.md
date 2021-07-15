---
title: AMSからAEM as aCloud ServiceへのDispatcher設定の移行
description: 'AMSからAEM as aCloud ServiceへのDispatcher設定の移行 '
feature: Dispatcher
source-git-commit: 19444aacbb86f93e7a5ea8bda2ca3c03a0a44f98
workflow-type: tm+mt
source-wordcount: '1447'
ht-degree: 95%

---

# AMSからAEM as aCloud ServiceへのDispatcher設定の移行 {#Dispatcher-in-the-cloud}

## AMS Dispatcher と AEM as a Cloud Service の主な違い {#main-differences-between-ams-dispatcher-configuration-and-aem-as-a-cloud-service}

AEM as aCloud ServiceのApacheおよびDispatcherの設定は、AMSの設定と非常に似ています。 主な違いは次のとおりです。

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
