---
title: AMS を Adobe Experience Manager as a Cloud Service Dispatcher 設定に変換する方法
description: AMS を Adobe Experience Manager as a Cloud Service Dispatcher 設定に変換する方法
translation-type: tm+mt
source-git-commit: 23349f3350631f61f80b54b69104e5a19841272f
workflow-type: tm+mt
source-wordcount: '1342'
ht-degree: 100%

---


# AMS を Adobe Experience Manager（AEM）as a Cloud Service Dispatcher 設定に変換する方法

## 概要 {#introduction}

この節では、AMS 設定を変換する方法を順を追って説明します。

>[!NOTE]
>ここでは、[Dispatcher 設定の管理](https://docs.adobe.com/content/help/ja-JP/experience-manager-cloud-manager/using/getting-started/dispatcher-configurations.html)で説明した構造と同様な構造のアーカイブがあることを前提としています。

## AMS を AEM as a Cloud Service Dispatcher 設定に変換する手順

1. **アーカイブを抽出し、最終的なプレフィックスを削除する**

   アーカイブをフォルダーに解凍し、直下のサブフォルダーとして conf、conf.d、conf.dispatcher.d、conf.modules.d が含まれていることを確認します。そのようになっていない場合は、これらのサブフォルダーを階層の上のレベルに移動します。

1. **未使用のサブフォルダーとファイルを削除する**

   サブフォルダー conf および conf.modules.d と、conf.d/*.conf のパターンに一致するファイルを削除します。

1. **非公開の仮想ホストをすべて排除する**

1. **仮想ホストファイルを削除する**

   対象となるのは、conf.d/enabled_vhosts の中で、名前に author、health、lc、flush のいずれかが含まれているファイルです。conf.d/available_vhosts 内の仮想ホストファイルで、どこからもリンクされていないものもすべて削除できます。

1. ポート 80 を参照しない仮想ホストセクションを削除またはコメント化する

   仮想ホストファイルに、ポート 80 以外のポートを排他的に参照するセクションが、次のように残っている場合：

   `<VirtualHost *:443>`
   `...`
   `</VirtualHost>`削除するか、コメント化します。これらのセクションのステートメントは処理されませんが、そのままにしておくと、効果がないのに編集してしまう可能性があり、混乱の元になります。

1. **書き換えを確認する**

   * conf.d/rewrites ディレクトリに入ります。

   * base_rewrite.rules と xforwarded_forcessl_rewrite.rules という名前のファイルをすべて削除します。また、それらを仮想ホストファイル内で参照している Include ステートメントを削除することを忘れないでください。

   * conf.d/rewrites に 1 つのファイルのみ含まれる場合は、そのファイルの名前を rewrite.rules に変更します。また、仮想ホストファイル内でそのファイルを参照している Include ステートメントも必ず適応させます。

   * ただし、フォルダーに仮想ホスト固有のファイルが複数含まれている場合は、それらのファイルを仮想ホストファイル内で参照している Include ステートメントに、それらのファイルの内容をコピーする必要があります。

1. **変数を確認する**

   1. conf.d/variables ディレクトリに入ります。

   1. ams_default.vars という名前のファイルをすべて削除します。また、それらを仮想ホストファイル内で参照している Include ステートメントを削除することを忘れないでください。

   1. conf.d/variables に 1 つのファイルのみ含まれる場合は、そのファイルの名前を custom.vars に変更します。また、そのファイルを仮想ホストファイル内で参照している Include ステートメントも必ず適応させます。

   1. ただし、フォルダーに仮想ホスト固有のファイルが複数含まれている場合は、それらのファイルを仮想ホストファイル内で参照している Include ステートメントに、それらのファイルの内容をコピーする必要があります。

1. **ホワイトリストを削除する**

   conf.d/whitelists フォルダーを削除し、そのサブフォルダー内のファイルを仮想ホストファイル内で参照している Include ステートメントを削除します。

1. **使用できなくなった変数を置き換える**

   すべての仮想ホストファイルで以下をおこないます。

   名前 PUBLISH_DOCROOT を DOCROOT に変更します。また、DISP_ID、PUBLISH_FORCE_SSL、PUBLISH_WHITELIST_ENABLED のいずれかの変数を参照しているセクションを削除します。

1. **バリデーターを実行して状態を確認する**

   ディレクトリ内で Dispatcher バリデーターを実行します。その際、

   `$ validator httpd` のように、httpd サブコマンドを付けます。インクルードファイルが見つからないことに関するエラーが表示される場合は、それらのファイルの名前を正しく変更したかどうかを確認します。

   ホワイトリストに登録されていない Apache ディレクティブが表示された場合は、それらを削除します。

1. **非公開ファームをすべて削除する**

   conf.dispatcher.d/enabled_farms 内のファームファイルで、名前に author、unhealthy、health、lc、flush のいずれかが含まれるものをすべて削除します。conf.dispatcher.d/available_farms 内のファームファイルで、どこからもリンクされていないものもすべて削除できます。

1. **ファームファイルの名前を変更する**

   conf.dispatcher.d/enabled_farms 内のファームファイルはすべて、*.farm というパターンに一致するように名前を変更する必要があります。例えば、customerX_farm.any というファームファイルは、customerX.farm という名前に変更します。

1. **キャッシュを確認する**

   conf.dispatcher.d/cache ディレクトリに入ります。

   ams_ のプレフィックスが付いたファイルをすべて削除します。

   conf.dispatcher.d/cache が空になった場合は、conf.dispatcher.d/cache/rules.any ファイルを標準の Dispatcher 設定からこのフォルダーにコピーします。標準の Dispatcher 設定は、この SDK の src フォルダーにあります。ファームファイル内の ams_*_cache.any ルールファイルを参照している $include ステートメントも、必ず適応させます。

   _cache.any サフィックスの付いた 1 つのファイルのみ conf.dispatcher.d/cache に含まれている場合は、名前を rules.any に変更し、ファームファイル内のそのファイルを参照している $include ステートメントも必ず適応させます。

   ただし、フォルダーにそのパターンを持つファーム固有のファイルが複数含まれている場合は、そのファイルの内容を、ファームファイル内でそれらのファイルを参照している $include ステートメントにコピーする必要があります。

   _invalidate_allowed.any というサフィックスの付いたファイルをすべて削除します。

   その場所に、デフォルトの Dispatcher 設定の conf.dispatcher.d/cache/default_invalidate_any ファイルをコピーします。

   各ファームファイルで、cache/allowedClients セクション内のコンテンツをすべて削除し、次と置き換えます。

   $include &quot;../cache/default_invalidate.any&quot;

1. **クライアントヘッダーを確認する**

   conf.dispatcher.d/clientheaders ディレクトリに入ります。

   ams_ のプレフィックスが付いたファイルをすべて削除します。

   _clientheaders.any サフィックスの付いた 1 つのファイルのみ conf.dispatcher.d/clientheaders に含まれている場合は、名前を clientheaders.any に変更し、ファームファイル内のそのファイルを参照している $include ステートメントも必ず適応させます。

   ただし、フォルダーにそのパターンを持つファーム固有のファイルが複数含まれている場合は、そのファイルの内容を、ファームファイル内でそれらのファイルを参照している $include ステートメントにコピーする必要があります。

   その場所に、デフォルトの Dispatcher 設定の conf.dispatcher/clientheaders/default_clientheaders.any ファイルをコピーします。

   各ファームファイルで、次のような clientheader インクルードステートメントを置き換えます。

   `$include "/etc/httpd/conf.dispatcher.d/clientheaders/ams_publish_clientheaders.any"`

   `$include "/etc/httpd/conf.dispatcher.d/clientheaders/ams_common_clientheaders.any"`

   次のステートメントに置き換えます。

   `$include "../clientheaders/default_clientheaders.any"`

1. **フィルターを確認する**

   * conf.dispatcher.d/filters ディレクトリに入ります。

   * ams_ のプレフィックスが付いたファイルをすべて削除します。

   * conf.dispatcher.d/filters に 1 つのファイルのみ含まれる場合は、そのファイルの名前を filters.any に変更します。また、ファームファイル内でそのファイルを参照している $include ステートメントも必ず適応させます。

   * ただし、フォルダーにそのパターンを持つファーム固有のファイルが複数含まれている場合は、そのファイルの内容を、ファームファイル内でそれらのファイルを参照している $include ステートメントにコピーする必要があります。

   * その場所に、デフォルトの Dispatcher 設定の conf.dispatcher/filters/default_filters.any ファイルをコピーします。

   * 各ファームファイルで、次のようなフィルターインクルードステートメントを

   * $include `"/etc/httpd/conf.dispatcher.d/filters/ams_publish_filters.any"`
を次のステートメントに置き換えます。

      `$include "../filters/default_filters.any"`

1. **レンダリングを確認する**

   * conf.dispatcher.d/renders ディレクトリに入ります。

   * フォルダー内のすべてのファイルを削除します。

   * その場所に、デフォルトの Dispatcher 設定の conf.dispatcher.d/renders/default_renders.any ファイルをコピーします。

   * 各ファームファイルで、renders セクション内のコンテンツをすべて削除し、次と置き換えます。

      `$include "../renders/default_renders.any"`

1. **仮想ホストを確認する**

   * ディレクトリの名前を `conf.dispatcher.d/vhosts to conf.dispatcher.d/virtualhosts` と変更し、そこに入ります。

   * `ams_` のプレフィックスが付いたファイルを削除します。

   * conf.dispatcher.d/virtualhosts に 1 つのファイルのみ含まれる場合は、そのファイルの名前を virtualhosts.any に変更します。また、ファームファイル内でそのファイルを参照している $include ステートメントも必ず適応させます。

   * ただし、フォルダーにそのパターンを持つファーム固有のファイルが複数含まれている場合は、そのファイルの内容を、ファームファイル内でそれらのファイルを参照している $include ステートメントにコピーする必要があります。

   * その場所に、デフォルトの Dispatcher 設定の conf.dispatcher/virtualhosts/default_virtualhosts.any ファイルをコピーします。

   * 各ファームファイルで、次のようなフィルターインクルードステートメントを

      `$include "/etc/httpd/conf.dispatcher.d/vhosts/ams_publish_vhosts.any"`次のステートメントに置き換えます。

      `$include "../virtualhosts/default_virtualhosts.any"`


1. **バリデーターを実行して状態を確認する**

   * ディレクトリ内で Dispatcher バリデーターを実行します。その際、次のように dispatcher サブコマンドを付けます。

      `$ validator dispatcher`

   * インクルードファイルが見つからないことに関するエラーが表示される場合は、それらのファイルの名前を正しく変更したかどうかを確認します。

   * 未定義の変数 `PUBLISH_DOCROOT` に関するエラーが表示される場合は、名前を `DOCROOT` に変更します。

   * その他のエラーについては、バリデーターツールのドキュメントの「トラブルシューティング」の節を参照してください。

## ローカルデプロイメントでの設定のテスト {#testing-config-local-deployment}

>[!IMPORTANT]
>
>ローカルデプロイメントで設定をテストするには、Docker のインストールが必要です。

Dispatcher SDK の `docker_run.sh` スクリプトを使用して、デプロイのみに表れる他のエラーが設定に含まれていないことをテストできます。

1. バリデーターを使用してデプロイメント情報を生成する

   `validator full -d out`設定を完全に検証し、out にデプロイメント情報が生成されます。

1. 生成されたデプロイメント情報を使用して、Docker イメージで Dispatcher を起動する

   AEM パブリッシュサーバーを macOS コンピューター上で実行し、ポート 4503 をリッスンしている場合は、次のように、そのサーバーの前で Dispatcher を実行できます。

   `$ docker_run.sh out docker.for.mac.localhost:4503 8080`

   これにより、コンテナが起動し、ローカルポート 8080 で Apache が公開されます。

## 新しい Dispatcher 設定の使用 {#using-dispatcher-config}

問題を報告しなくなり、Docker コンテナがエラーや警告を出さずに起動した場合、設定を git リポジトリの d`ispatcher/src` サブディレクトリに移動する準備が整いました。