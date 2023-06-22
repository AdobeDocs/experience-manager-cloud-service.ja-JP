---
title: AMS を Adobe Experience Manager as a Cloud Service Dispatcher 設定に変換する方法
description: AMS を Adobe Experience Manager as a Cloud Service Dispatcher 設定に変換する方法
source-git-commit: 1fc57dacbf811070664d5f5aaa591dd705516fa8
workflow-type: tm+mt
source-wordcount: '1275'
ht-degree: 49%

---


# AMS を Adobe Experience Manager（AEM）as a Cloud Service Dispatcher 設定に変換する方法

## はじめに {#introduction}

この節では、AMS 設定を変換する手順を説明します。

>[!NOTE]
>ここでは、[Dispatcher 設定の管理](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/content/getting-started/dispatcher-configurations.html)で説明した構造と同様な構造のアーカイブがあることを前提としています。

## AMS を AEM as a Cloud Service Dispatcher 設定に変換する手順

1. **アーカイブを抽出し、最終的なプレフィックスを削除する**

   アーカイブをフォルダーに抽出し、直下のサブフォルダーが conf、conf.d、conf.dispatcher.d および conf.modules.d で始まっていることを確認します。表示されない場合は、階層の上に移動します。

1. **未使用のサブフォルダーとファイルを削除する**

   サブフォルダー conf および conf.modules.d と、conf.d/*.conf に一致するファイルを削除します。

1. **非公開の仮想ホストをすべて排除する**

1. **仮想ホストファイルを削除する**

   conf.d/enabled_vhosts の中で、名前に author、health、lc、flush のいずれかが含まれているもの。 conf.d/available_vhosts 内の仮想ホストファイルで、どこからもリンクされていないものもすべて削除できます。

1. ポート 80 を参照しない仮想ホストセクションを削除またはコメント化する

   仮想ホストファイルに、ポート 80 以外のポートを排他的に参照するセクションが、次のように残っている場合：

   `<VirtualHost *:443>`
   `...`
   `</VirtualHost>`削除するか、コメント化します。これらのセクションのステートメントは処理されませんが、そのまま使用すると、効果がなく編集されてしまう可能性があり、混乱の原因となります。

1. **書き換えを確認する**

   * conf.d/rewrites ディレクトリに入ります。

   * base_rewrite.rules と xforwarded_forcessl_rewrite.rules という名前のファイルをすべて削除します。また、それらを仮想ホストファイル内で参照している Include ステートメントを削除することを忘れないでください。

   * conf.d/rewrites に 1 つのファイルのみ含まれる場合は、そのファイルの名前を rewrite.rules に変更します。また、仮想ホストファイル内でそのファイルを参照している Include ステートメントも必ず適応させます。

   * ただし、フォルダーに仮想ホスト固有のファイルが複数含まれている場合は、そのファイルの内容を、仮想ホストファイル内のファイルを参照する Include ステートメントにコピーする必要があります。

1. **変数を確認する**

   1. conf.d/variables ディレクトリに入ります。

   1. ams_default.vars という名前のファイルをすべて削除します。また、それらを仮想ホストファイル内で参照している Include ステートメントを削除することを忘れないでください。

   1. conf.d/variables に 1 つのファイルのみ含まれる場合は、そのファイルの名前を custom.vars に変更します。また、そのファイルを仮想ホストファイル内で参照している Include ステートメントも必ず適応させます。

   1. ただし、フォルダーに仮想ホスト固有のファイルが複数含まれている場合は、そのファイルの内容を、仮想ホストファイル内のファイルを参照する Include ステートメントにコピーする必要があります。

1. **ホワイトリストを削除する**

   conf.d/whitelists フォルダーを削除し、そのサブフォルダー内のファイルを仮想ホストファイル内で参照している Include ステートメントを削除します。

1. **使用できなくなった変数を置き換える**

   すべての仮想ホストファイルで以下をおこないます。

   名前 PUBLISH_DOCROOT を DOCROOT に変更します。また、DISP_ID、PUBLISH_FORCE_SSL、PUBLISH_WHITELIST_ENABLED のいずれかの変数を参照しているセクションを削除します。

1. **バリデーターを実行して状態を確認する**

   ディレクトリ内で Dispatcher バリデーターを実行します。その際、次のように httpd サブコマンドを使用します。

   `$ validator httpd`
「include」ファイルが見つからないことに関するエラーが表示される場合は、これらのファイルの名前を正しく変更したかどうかを確認します。

   ホワイトリストに登録されていない Apache ディレクティブが表示された場合は、それらを削除します。

1. **非公開ファームをすべて削除する**

   conf.dispatcher.d/enabled_farms 内のファームファイルで、名前に author、unhealthy、health、lc、flush のいずれかが含まれるものをすべて削除します。 conf.dispatcher.d/available_farms 内のファームファイルで、どこからもリンクされていないものもすべて削除できます。

1. **ファームファイルの名前を変更する**

   conf.dispatcher.d/enabled_farms 内のファームはすべて、*.farm のパターンに合わせて名前を変更する必要があります。 例えば、 `customerX_farm.any` から `customerX.farm`.

1. **キャッシュを確認する**

   conf.dispatcher.d/cache ディレクトリに入ります。

   `ams_` のプレフィックスが付いたファイルを削除します。

   conf.dispatcher.d/cache が空になった場合は、ファイルをコピーします。 `conf.dispatcher.d/cache/rules.any` 標準の Dispatcher 設定からこのフォルダーに移動します。 標準の Dispatcher 設定は、この SDK の src フォルダーにあります。 必ず、 `ams_*_cache.any` ルールファイルをファームファイルに含めることもできます。

   conf.dispatcher.d/cache にサフィックス付きの単一のファイルが含まれるようになった場合 `_cache.any`を呼び出す場合は、名前をに変更します。 `rules.any`. ファームファイル内のそのファイルを参照する$include ステートメントも、必ず適応させます。

   ただし、フォルダーにそのパターンを持つファーム固有のファイルが複数含まれている場合は、そのファイルの内容を、ファームファイル内のファイルを参照する$include ステートメントにコピーする必要があります。

   `_invalidate_allowed.any` サフィックスを持つファイルを削除します。

   その場所に、デフォルトの Dispatcher 設定の conf.dispatcher.d/cache/default_invalidate_any ファイルをコピーします。

   各ファームファイルで、cache/allowedClients セクション内のコンテンツをすべて削除し、次と置き換えます。

   $include &quot;../cache/default_invalidate.any&quot;

1. **クライアントヘッダーを確認する**

   conf.dispatcher.d/clientheaders ディレクトリに入ります。

   `ams_` のプレフィックスが付いたファイルを削除します。

   conf.dispatcher.d/clientheaders にサフィックス付きの単一のファイルが含まれる場合 `_clientheaders.any`、名前をに変更します。 `clientheaders.any`. ファームファイル内のそのファイルを参照する$include ステートメントも、必ず適応させます。

   ただし、フォルダーにそのパターンを持つファーム固有のファイルが複数含まれている場合は、そのファイルの内容を、ファームファイル内のファイルを参照する$include ステートメントにコピーする必要があります。

   ファイルをコピーします。 `conf.dispatcher/clientheaders/default_clientheaders.any` をデフォルトの Dispatcher 設定からその場所に移動します。

   各ファームファイルで、 `clientheader` 次のように表示される「include」ステートメント：

   `$include "/etc/httpd/conf.dispatcher.d/clientheaders/ams_publish_clientheaders.any"`

   `$include "/etc/httpd/conf.dispatcher.d/clientheaders/ams_common_clientheaders.any"`

   次のステートメントに置き換えます。

   `$include "../clientheaders/default_clientheaders.any"`

1. **フィルターを確認する**

   * conf.dispatcher.d/filters ディレクトリに入ります。

   * `ams_` のプレフィックスが付いたファイルを削除します。

   * conf.dispatcher.d/filters に 1 つのファイルのみ含まれる場合は、名前をに変更します。 `filters.any`. ファームファイル内のそのファイルを参照する$include ステートメントも、必ず適応させます。

   * ただし、フォルダーにそのパターンを持つファーム固有のファイルが複数含まれている場合は、そのファイルの内容を、ファームファイル内のファイルを参照する$include ステートメントにコピーする必要があります。

   * ファイルをコピーします。 `conf.dispatcher/filters/default_filters.any` をデフォルトの Dispatcher 設定からその場所に移動します。

   * 各ファームファイルで、次のように表示されるフィルター「include」ステートメントを置き換えます。

   * $include `"/etc/httpd/conf.dispatcher.d/filters/ams_publish_filters.any"`
を次のステートメントに置き換えます。

     `$include "../filters/default_filters.any"`

1. **レンダリングを確認する**

   * conf.dispatcher.d/renders ディレクトリに入ります。

   * フォルダー内のすべてのファイルを削除します。

   * ファイルをコピーします。 `conf.dispatcher.d/renders/default_renders.any` をデフォルトの Dispatcher 設定からその場所に移動します。

   * 各ファームファイルで、renders セクション内のコンテンツをすべて削除し、次と置き換えます。

     `$include "../renders/default_renders.any"`

1. **仮想ホストを確認する**

   * ディレクトリの名前を `conf.dispatcher.d/vhosts to conf.dispatcher.d/virtualhosts` と変更し、そこに入ります。

   * `ams_` のプレフィックスが付いたファイルを削除します。

   * conf.dispatcher.d/virtualhosts に 1 つのファイルのみ含まれる場合は、名前をに変更します。 `virtualhosts.any`. ファームファイル内のそのファイルを参照する$include ステートメントも、必ず適応させます。

   * ただし、フォルダーにそのパターンを持つファーム固有のファイルが複数含まれている場合は、そのファイルの内容を、ファームファイル内のファイルを参照する$include ステートメントにコピーする必要があります。

   * ファイルをコピーします。 `conf.dispatcher/virtualhosts/default_virtualhosts.any` をデフォルトの Dispatcher 設定からその場所に移動します。

   * 各ファームファイルで、次のように表示されるフィルター「include」ステートメントを置き換えます。

     `$include "/etc/httpd/conf.dispatcher.d/vhosts/ams_publish_vhosts.any"`次のステートメントに置き換えます。

     `$include "../virtualhosts/default_virtualhosts.any"`


1. **バリデーターを実行して状態を確認する**

   * ディレクトリ内の Dispatcher バリデーターを、Dispatcher サブコマンドと共に実行します。

     `$ validator dispatcher`

   * 「include」ファイルが見つからないことに関するエラーが表示される場合は、これらのファイルの名前を正しく変更したかどうかを確認します。

   * 未定義の変数 `PUBLISH_DOCROOT` に関するエラーが表示される場合は、名前を `DOCROOT` に変更します。

   * その他のエラーについては、バリデーターツールのドキュメントの「トラブルシューティング」の節を参照してください。

## ローカルデプロイメントでの設定のテスト {#testing-config-local-deployment}

>[!IMPORTANT]
>
>ローカルデプロイメントで設定をテストするには、Docker のインストールが必要です。

Dispatcher SDK の `docker_run.sh` スクリプトを使用して、デプロイのみに表れる他のエラーが設定に含まれていないことをテストできます。

1. バリデーターを使用してデプロイメント情報を生成する。

   `validator full -d out`
設定を完全に検証し、out にデプロイメント情報を生成します。

1. そのデプロイメント情報を使用して、Docker イメージで Dispatcher を起動します。

   AEM パブリッシュサーバーを macOS コンピューター上で実行し、ポート 4503 をリッスンしている場合は、次のように、そのサーバーの前で Dispatcher を実行できます。

   `$ docker_run.sh out docker.for.mac.localhost:4503 8080`

   コンテナを起動し、ローカルポート 8080 で Apache を公開します。

## 新しい Dispatcher 設定の使用 {#using-dispatcher-config}

問題を報告しなくなり、Docker コンテナがエラーや警告を出さずに起動した場合、設定を git リポジトリの d`ispatcher/src` サブディレクトリに移動する準備が整いました。