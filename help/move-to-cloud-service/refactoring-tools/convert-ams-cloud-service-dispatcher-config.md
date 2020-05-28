---
title: AMSのクラウドサービスディスパッチャー設定としてのAdobe Experience Managerへの変換
description: AMSのクラウドサービスディスパッチャー設定としてのAdobe Experience Managerへの変換
translation-type: tm+mt
source-git-commit: 3478827949356c4a4f5133b54c6cf809f416efef
workflow-type: tm+mt
source-wordcount: '1342'
ht-degree: 22%

---


# AMSのクラウドサービスディスパッチャー設定としてのAdobe Experience Manager (AEM)への変換

## 概要 {#introduction}

このセクションでは、AMSコンフィギュレーションを変換する手順を順を追って説明します。

>[!NOTE]
>It assumes that you have an archive with a structure similar to the one described in [Manage your Dispatcher Configurations](https://docs.adobe.com/content/help/ja-JP/experience-manager-cloud-manager/using/getting-started/dispatcher-configurations.html).

## AMSをクラウドサービスディスパッチャー設定としてAEMに変換する手順

1. **アーカイブを抽出し、最終的なプレフィックスを削除する**

   アーカイブをフォルダーに展開し、conf、conf.d、conf.dispatcher.dおよびconf.modules.dを使用して、サブフォルダーのすぐ下の開始ーを確認します。 上に移動しない場合は、階層内で上に移動します。

1. **未使用のサブフォルダーとファイルを削除する**

   サブフォルダconfとconf.modules.d、およびconf.d/*.confに一致するファイルを削除します。

1. **非公開の仮想ホストをすべて排除する**

1. **仮想ホストファイルの削除**

   conf.d/enabled_vhostsの中で、author、health、lcまたはflushが名前に含まれている。 conf.d/available_vhosts内の、リンクされていない仮想ホストファイルもすべて削除できます。

1. ポート 80 を参照しない仮想ホストセクションを削除またはコメント化する

   仮想ホストファイルに、ポート 80 以外のポートを排他的に参照するセクションが、次のように残っている場合：

   `<VirtualHost *:443>`
   `...`
   `</VirtualHost>`削除するか、コメント化します。これらのセクションのステートメントは処理されませんが、そのままにしておくと、効果がないのに編集してしまう可能性があり、混乱の元になります。

1. **書き換えを確認する**

   * ディレクトリconf.d/rewritesを入力します。

   * base_rewrite.rulesとxforwarded_forcessl_rewrite.rulesという名前のファイルを削除し、それらを参照する仮想ホストファイル内のIncludeステートメントを忘れずに削除してください。

   * conf.d/rewritesに単一のファイルが含まれる場合は、rewrite.rulesという名前に変更する必要があります。また、仮想ホストファイル内のそのファイルを参照するInclude文も、必ず適用してください。

   * ただし、フォルダに複数の仮想ホスト固有のファイルが含まれる場合は、そのファイルの内容を仮想ホストファイル内のファイルを参照する「含める」文にコピーする必要があります。

1. **変数を確認する**

   1. ディレクトリconf.d/variablesを入力します。

   1. ams_default.varsという名前のファイルを削除し、それらを参照する仮想ホストファイル内の「含める」文を必ず削除してください。

   1. conf.d/variablesに単一のファイルが含まれる場合は、そのファイルの名前をcustom.varsに変更し、仮想ホストファイル内のそのファイルを参照するInclude文も適用することを忘れないでください。

   1. ただし、フォルダに複数の仮想ホスト固有のファイルが含まれる場合は、そのファイルの内容を仮想ホストファイル内のファイルを参照する「含める」文にコピーする必要があります。

1. **ホワイトリストを削除する**

   フォルダーconf.d/whitelistsを削除し、そのサブフォルダー内の一部のファイルを参照する仮想ホストファイル内のIncludeステートメントを削除します。

1. **使用できなくなった変数を置き換える**

   すべての仮想ホストファイル内：

   PUBLISH_DOCROOTの名前をDOCROOTRemoveセクションに変更し、DISP_ID、PUBLISH_FORCE_SSLまたはPUBLISH_WHITELIST_ENABLEDという名前の変数を参照します。

1. **バリデーターを実行して状態を確認する**

   ディレクトリ内のディスパッチャーバリデーターを実行し、httpdサブコマンドを使用します。

   `$ validator httpd`インクルードファイルが見つからないことに関するエラーが表示される場合は、それらのファイルの名前を正しく変更したかどうかを確認します。

   ホワイトリストに登録されていない Apache ディレクティブが表示された場合は、それらを削除します。

1. **非公開ファームをすべて削除する**

   conf.dispatcher.d/enabled_farms内の、名前にauthor、health、lcまたはflushが含まれるファームファイルを削除します。 conf.dispatcher.d/available_farms内の、リンクされていないファームファイルもすべて削除できます。

1. **ファームファイルの名前を変更する**

   conf.dispatcher.d/enabled_farms内のすべてのファームは、*.farmというパターンに合わせて名前を変更する必要があります。例えば、customerX_farm.anyというファームファイルは、customerX.farmという名前に変更する必要があります。

1. **キャッシュを確認する**

   conf.dispatcher.d/cacheディレクトリを入力します。

   先頭にams_が付いたファイルを削除します。

   conf.dispatcher.d/cacheが空になった場合は、conf.dispatcher.d/cache/rules.anyファイルを標準のディスパッチャー設定からこのフォルダーにコピーします。 標準のディスパッチャー設定は、このSDKのフォルダーsrcにあります。 ファームファイル内のams_*_cache.anyルールファイルも参照し、$include文を適用することを忘れないでください。

   conf.dispatcher.d/cacheに_cache.anyというサフィックスを持つ単一のファイルが含まれる場合は、そのファイルの名前をrules.anyに変更し、ファームファイル内のそのファイルを参照する$include文も必ず適用してください。

   そのパターンを持つ複数のファーム固有のファイルがフォルダーに含まれている場合は、そのファームファイル内のファイルを参照するコンテンツを$includeステートメントにコピーする必要があります。

   _invalidate_allowed.anyというサフィックスを持つファイルをすべて削除します。

   デフォルトのディスパッチャー設定のconf.dispatcher.d/cache/default_invalidate_anyファイルをその場所にコピーします。

   各ファームファイルで、cache/allowedClientsセクションの内容を削除し、次のファイルに置き換えます。

   $include &quot;../cache/default_invalidate.any&quot;

1. **クライアントヘッダーを確認する**

   conf.dispatcher.d/clientheadersディレクトリを入力します。

   先頭にams_が付いたファイルを削除します。

   conf.dispatcher.d/clientheadersに_clientheaders.anyというサフィックスを持つ単一のファイルが含まれる場合、ファームファイル内のそのファイルを参照する$include文も、clientheaders.anyに変更する必要があります。

   そのパターンを持つ複数のファーム固有のファイルがフォルダーに含まれている場合は、そのファームファイル内のファイルを参照するコンテンツを$includeステートメントにコピーする必要があります。

   デフォルトのディスパッチャー設定からその場所に、conf.dispatcher/clientheaders/default_clientheaders.anyファイルをコピーします。

   各ファームファイルで、次のような clientheader インクルードステートメントを置き換えます。

   `$include "/etc/httpd/conf.dispatcher.d/clientheaders/ams_publish_clientheaders.any"`

   `$include "/etc/httpd/conf.dispatcher.d/clientheaders/ams_common_clientheaders.any"`

   次のステートメントに置き換えます。

   `$include "../clientheaders/default_clientheaders.any"`

1. **フィルターを確認する**

   * ディレクトリconf.dispatcher.d/フィルターを入力します。

   * 先頭にams_が付いたファイルを削除します。

   * conf.dispatcher.d/フィルターに単一のファイルが含まれる場合は、そのファイルの名前をフィルターに変更する必要があります。また、ファームファイル内のそのファイルを参照する$include文も、必ず適用してください。

   * そのパターンを持つ複数のファーム固有のファイルがフォルダーに含まれている場合は、そのファームファイル内のファイルを参照するコンテンツを$includeステートメントにコピーする必要があります。

   * デフォルトのディスパッチャー設定からその場所に、conf.dispatcher/filters/default_filters.anyファイルをコピーします。

   * 各ファームファイルで、次のようなフィルターインクルードステートメントを置き換えます。

   * $include `"/etc/httpd/conf.dispatcher.d/filters/ams_publish_filters.any"`with the statement:

      `$include "../filters/default_filters.any"`

1. **レンダリングを確認する**

   * conf.dispatcher.d/rendersディレクトリを入力します。

   * フォルダー内のすべてのファイルを削除します。

   * conf.dispatcher.d/renders/default_renders.anyファイルをデフォルトのディスパッチャー設定からその場所にコピーします。

   * 各ファームファイルで、レンダリングセクションの内容を削除し、次のファイルに置き換えます。

      `$include "../renders/default_renders.any"`

1. **仮想ホストを確認する**

   * Rename the directory `conf.dispatcher.d/vhosts to conf.dispatcher.d/virtualhosts` and enter it.

   * `ams_` のプレフィックスが付いたファイルを削除します。

   * conf.dispatcher.d/virtualhostsが単一のファイルを含む場合は、virtualhosts.anyに名前を変更し、ファームファイル内のそのファイルを参照する$include文も必ず適用してください。

   * そのパターンを持つ複数のファーム固有のファイルがフォルダーに含まれている場合は、そのファームファイル内のファイルを参照するコンテンツを$includeステートメントにコピーする必要があります。

   * デフォルトのディスパッチャー設定からその場所に、conf.dispatcher/virtualhosts/default_virtualhosts.anyファイルをコピーします。

   * 各ファームファイルで、次のようなフィルターインクルードステートメントを置き換えます。

      `$include "/etc/httpd/conf.dispatcher.d/vhosts/ams_publish_vhosts.any"`次のステートメントに置き換えます。

      `$include "../virtualhosts/default_virtualhosts.any"`


1. **バリデーターを実行して状態を確認する**

   * dispatcherサブコマンドを使用して、ディレクトリ内のディスパッチャーバリデーターを実行します。

      `$ validator dispatcher`

   * インクルードファイルが見つからないことに関するエラーが表示される場合は、それらのファイルの名前を正しく変更したかどうかを確認します。

   * 未定義の変数 `PUBLISH_DOCROOT` に関するエラーが表示される場合は、名前を `DOCROOT` に変更します。

   * その他のエラーについては、バリデーターツールのドキュメントの「トラブルシューティング」の節を参照してください。

## ローカルデプロイメントでの設定のテスト {#testing-config-local-deployment}

>[!IMPORTANT]
> ローカル展開で構成をテストするには、Dockerのインストールが必要です。

Using the script `docker_run.sh` in the Dispatcher SDK, you can test that your configuration does not contain any other error that would only show up in deployment:

1. バリデーターを使用した導入情報の生成

   `validator full -d out`
これにより、完全な構成が検証され、デプロイメント情報が生成されます

1. ドッカーイメージ内のディスパッチャーとそのデプロイメント情報との開始

   AEM パブリッシュサーバーを macOS コンピューター上で実行し、ポート 4503 をリッスンしている場合は、次のように、そのサーバーの前で Dispatcher を実行できます。

   `$ docker_run.sh out docker.for.mac.localhost:4503 8080`

   これにより、コンテナが起動し、ローカルポート 8080 で Apache が公開されます。

## Using your new dispatcher configuration {#using-dispatcher-config}

If the validator no longer reports any issue and the docker container starts up without any failures or warnings, you are ready to move your configuration to a d`ispatcher/src` subdirectory of your git repository.