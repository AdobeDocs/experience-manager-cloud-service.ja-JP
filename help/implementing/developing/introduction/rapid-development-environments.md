---
title: 迅速な開発環境
description: クラウド環境で迅速な開発反復処理を行うために、高速開発環境を活用する方法を説明します。
source-git-commit: 6f6cf5657bf745a2e392a8bfd02572aa864cc69c
workflow-type: tm+mt
source-wordcount: '2903'
ht-degree: 6%

---


# 迅速な開発環境 {#rapid-development-environments}

>[!AVAILABILITY]
>
>この機能は、2 月を通じて徐々にお客様に提供される予定です。

変更をデプロイするために、現在のクラウド開発環境では、CI/CD パイプラインと呼ばれる広範なコードセキュリティと品質ルールを採用したプロセスを使用する必要があります。 迅速で反復的な変更が必要な状況では、Adobeが迅速な開発環境 (RDE) を導入しました。

RDE を使用すると、ローカル開発環境で動作すると証明された機能のテストに必要な時間を最小限に抑え、変更を迅速にデプロイおよび確認できます。

変更が RDE でテストされたら、Cloud Manager パイプラインを通じて通常のクラウド開発環境にデプロイできます。

## はじめに {#introduction}

RDE は、コード、コンテンツ、Apache または Dispatcher の設定に使用できます。 通常のクラウド開発環境とは異なり、開発者はローカルのコマンドラインツールを使用して、ローカルで作成されたコードを RDE に同期できます。

すべてのプログラムには RDE がプロビジョニングされます。 Sandbox アカウントの場合、数時間使用されなかった後に休止状態になります。

通常、特定の機能のテストとデバッグには、特定の時点で 1 人の開発者が RDE を使用します。 開発セッションが完了すると、RDE は次の使用時にデフォルトの状態にリセットできます。

追加の RDE は、実稼動（サンドボックス以外）プログラムのライセンスを受ける場合があります。

## プログラムでの RDE の有効化 {#enabling-rde-in-a-program}

Cloud Manager を使用してプログラムの RDE を作成するには、次の手順に従います。

1. [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) で Cloud Manager にログインし、適切な組織を選択します。

1. RDE を追加するプログラムをクリックして詳細を表示します。

   * RDE は両方に追加できます [サンドボックスプログラム](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/creating-sandbox-programs.md) および [実稼働プログラム。](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/introduction-production-programs.md)

1. **プログラムの概要**&#x200B;ページで、**環境**&#x200B;カードの「**環境を追加**」をクリックして環境を追加します。

   ![環境カード](/help/implementing/cloud-manager/assets/no-environments.png)

   * 「**環境を追加**」オプションは「**環境**」タブでも使用できます。

      ![「環境」タブ](/help/implementing/cloud-manager/assets/environments-tab.png)

   * 「**環境を追加**」オプションは、権限がない場合やライセンスされているリソースによっては、無効になっている場合があります。

1. 表示される&#x200B;**環境を追加**&#x200B;ダイアログで以下を行います。

   * 選択 **急速な開発** の下に **環境タイプを選択** 見出し。
      * 使用可能な環境または使用中の環境の数は、環境タイプの後ろの括弧で囲まれて表示されます。
   * 次を提供： **名前** 環境の
   * オプション **説明** 環境の
   * 「**クラウドリージョン**」を選択します。

   ![環境を追加ダイアログ](/help/implementing/cloud-manager/assets/add-environment-wizard.png)

1. 「**保存**」をクリックして、指定された環境を追加します。

これで、**概要**&#x200B;画面の&#x200B;**環境**&#x200B;カードに新しい環境が表示されます。

Cloud Manager を使用した環境の作成、環境へのアクセス権のあるユーザーの管理、カスタムドメインの割り当てについて詳しくは、 [Cloud Manager のドキュメント。](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/program-types.md)

## RDE コマンドラインツールのインストール {#installing-the-rde-command-line-tools}

Cloud Manager を使用してプログラムに RDE を追加したら、次の手順に従ってコマンドラインツールを設定して、RDE を操作できます。

>[!IMPORTANT]
>
>最新バージョンの [Node と NPM がインストールされている](https://nodejs.org/en/download/) Adobe I/OCLI と関連プラグインが正しく機能する。


1. 次の手順に従って、Adobe I/OCLI ツールをインストールします。 [ここ](https://developer.adobe.com/runtime/docs/guides/tools/cli_install/).
1. Adobe I/OCLI ツールの cloud manager プラグインをインストールし、説明に従って設定します。 [ここ](https://github.com/adobe/aio-cli-plugin-cloudmanager).
1. 次のコマンドを実行して、Adobe I/OCLI ツールAEM RDE プラグインをインストールします。

   ```
   aio plugins:install @adobe/aio-cli-plugin-aem-rde
   aio plugins:update
   ```

1. 組織 ID に対して Cloud Manager プラグインを設定します。

   `aio config:set cloudmanager_orgid 4E03EQC05D34GL1A0B49421C@AdobeOrg`

   と英数字を独自の組織 ID に置き換えて、戦略を使用して検索できます。 [ここ](https://experienceleague.adobe.com/docs/core-services/interface/administration/organizations.html#concept_EA8AEE5B02CF46ACBDAD6A8508646255).

1. 次に、プログラム ID を設定します。

   `aio config:set cloudmanager_programid 12345`

1. 次に、RDE が添付される環境 ID を設定します。

   `aio config:set cloudmanager_environmentid 123456`

1. プラグインの設定が完了したら、

   `aio login`

   ログイン成功時の応答は次の出力のようになりますが、表示される値は無視できます。

   ```
   ...
   You are currently in:
   1. Org: <no org selected>
   2. Project: <no project selected>
   3. Workspace: <no workspace selected>
   ```

1. を実行して、ログインが正常に完了したことを確認します。

   `aio cloudmanager:list-programs`

   設定した組織の下にあるすべてのプログラムが一覧表示されます。

   上記の操作を実行するには、Cloud Manager のメンバーである必要があります **開発者 —Cloud Service** 製品プロファイル。 詳しくは、[このページ](/help/journey-onboarding/assign-profiles-cloud-manager.md#assign-developer)を参照してください。

   または、次のコマンドを実行して開発者コンソールにログインできる場合は、この開発者ロールを持っていることを確認できます。

   `aio cloudmanager:environment:open-developer-console`

   >[!TIP]
   >
   >表示された `Warning: cloudmanager:list-programs is not a aio command.` エラーが発生した場合は、 [aio-cli-plugin-cloudmanager](https://github.com/adobe/aio-cli-plugin-cloudmanager) 次のコマンドを実行します。
   >
   >
   ```
   >aio plugins:install @adobe/aio-cli-plugin-cloudmanager
   >```


## 新機能の開発時の RDE の使用 {#using-rde-while-developing-a-new-feature}

Adobeでは、新しい機能を開発する際に、次のワークフローを使用することをお勧めします。

* 中間マイルストーンに達し、AEMas a Cloud ServiceSDK でローカルで正常に検証された場合、コードは、git へのコミットはオプションですが、メイン行にまだ含まれていない git 機能ブランチにコミットする必要があります。 「中間マイルストーン」を構成する要素は、チームの習慣に応じて異なります。 例としては、新しいコード行や、半日の作業、サブ機能の完了などがあります。

* RDE が別の機能で使用されていて、次の操作を行う場合は、RDE をリセットします。 [デフォルトの状態にリセット](#reset-rde). <!-- Alexandru: hiding for now, please don't delete This can be done via [Cloud Manager](#reset-the-rde-cloud-manager) or via the [command line](#reset-the-rde-command-line). -->リセットには数分かかり、既存のコンテンツとコードはすべて削除されます。 RDE ステータスコマンドを使用して、RDE の準備が完了したことを確認できます。

* RDE コマンドラインインターフェイスを使用して、ローカルコードを RDE に同期します。 オプションとしては、コンテンツパッケージ、特定のバンドル、OSGi 設定ファイル、コンテンツファイル、Apache/Dispatcher 設定の zip ファイルのインストールがあります。 リモートコンテンツパッケージの参照も可能です。 詳しくは、 [RDE コマンドラインツール](#rde-cli-commands) 」の節を参照してください。 status コマンドを使用すると、デプロイメントが成功したことを検証できます。 必要に応じて、パッケージマネージャーを使用してコンテンツパッケージをインストールします。

* RDE でコードをテストします。 オーサー URL とパブリッシュ URL は Cloud Manager で使用できます。

* コードが期待どおりに動作しない場合は、標準のデバッグ手法を使用して問題を理解し、適切な変更をおこないます。 コードの変更を git にコミットせず（まだ検証されていないので）、ローカル CLI を使用してコードを RDE に同期します。 問題が解決されるまで繰り返し処理を続けます。

* コードが期待どおりに動作したら、コードを Git 機能ブランチにコミットします。

* RDE に同期したコードは Cloud Manager パイプラインを使用しないので、Cloud Manager 非実稼動パイプラインを使用して、Git 機能ブランチを Cloud Development 環境にデプロイする必要があります。 これにより、コードが Cloud Manager 品質ゲートを渡すかどうかを検証し、後で Cloud Manager 実稼動パイプラインを使用してコードが正常にデプロイされるかを確認できます。

* この機能のすべてのコードが準備でき、RDE とクラウド開発環境の両方で正常に動作するまで、各中間マイルストーンに対して上記の手順を繰り返します。

* Cloud Manager 実稼動パイプラインを使用してコードを実稼動環境にデプロイします。

## RDE を使用した既存の機能のデバッグ {#use-rde-to-debug-an-existing-feature}

このワークフローは、新しい機能の開発と似ています。 違いは、RDE に同期されるコードは、問題が見つかった環境にプッシュされた内容の Git ラベルを反映している点です。 また、アップストリーム環境に合ったコンテンツをデプロイすると便利です。 これは、コンテンツパッケージのエクスポートとインポートを通じて実現できます。

## 複数の開発者が同じ RDE で共同作業 {#multiple-developers-collaborating-on-the-same-rde}

RDE は、一度に 1 つのプロジェクトをサポートします。 コードはローカル開発環境から RDE 環境に同期されるので、1 人の開発者が同時にコードを使用するのが最も自然です。

ただし、慎重に調整をおこなうことで、複数の開発者が特定の機能を検証したり、特定の問題をデバッグしたりできます。 重要なのは、各開発者がローカルプロジェクトの同期を保ち、特定の開発者がおこなったコードの変更が他の開発者に吸収されるためです。そうしないと、1 人の開発者が誤って他の開発者のコードを上書きする可能性があるからです。 推奨される方法は、各開発者が RDE に同期する前に変更を共有 Git ブランチにコミットし、他の開発者が変更を加えてから独自に変更を加えることです。

## RDE コマンドラインツールのコマンド {#rde-cli-commands}

### ヘルプ/一般情報 {#help}

* コマンドのリストには、次のように入力します。

   `aio aem:rde`

* コマンドの詳細なヘルプを表示するには、次のように入力します。

   `aio aem rde <command> --help`

### RDE へのデプロイ {#deploying-to-rde}

この節では、バンドル、OSGi 設定、コンテンツパッケージ、個々のコンテンツファイル、Apache または Dispatcher 設定のデプロイ、インストールまたは更新に RDE CLI を使用する方法について説明します。

一般的な使用パターンは次のとおりです。 `aio aem:rde:install <artifact>`.

以下に例を示します。

<u>コンテンツパッケージのデプロイ</u>

`aio aem:rde:install sample.demo.ui.apps.all-1.0.0-SNAPSHOT.zip`

デプロイメントが成功した場合の応答は、次のようになります。

```
...
#1: deploy completed for content-package sample.demo.ui.apps.all-1.0.0-SNAPSHOT.zip on author,publish - done by 9E072FC75D54FE1A2B49431C@AdobeID at 2022-09-13T11:32:06.229Z
```

オプションで、リモートリポジトリを参照できます。

`aio aem:rde:install -t content-package "https://repo1.maven.org/maven2/com/adobe/aem/guides/aem-guides-wknd.all/2.1.0/aem-guides-wknd.all-2.1.0.zip"`

デフォルトでは、アーティファクトはオーサー層とパブリッシュ層の両方にデプロイされますが、「 —s」フラグを使用して特定の層をターゲットにすることができます。

>[!IMPORTANT]
>
>WKND プロジェクトの Dispatcher 設定は、上記の content-package インストール経由でデプロイされません。 「Apache/Dispatcher 設定のデプロイ」の手順に従って、別途デプロイする必要があります。

<u>OSGi 設定のデプロイ</u>

`aio aem:rde:install com.adobe.granite.demo.MyServlet.cfg.json`

デプロイメントが成功した場合の応答は、次のようになります。

```
...
#2: deploy completed for osgi-config com.adobe.granite.demo.MyServlet.cfg.json on author,publish - done by 9E0725C05D54FE1A0B49431C@AdobeID at 2022-09-13T11:54:36.390Z
```

<u>バンドルのデプロイ</u>

バンドルをデプロイするには、次を使用します。

`aio aem:rde:install ~/.m2/repository/org/apache/felix/org.apache.felix.gogo.jline/1.1.8/org.apache.felix.gogo.jline-1.1.8.jar`

デプロイメントが成功した場合の応答は、次のようになります。

```
...
#3: deploy staged for osgi-bundle org.apache.felix.gogo.jline-1.1.8.jar on author,publish - done by 9E0725C05D53BE1A0B49431C@AdobeID at 2022-09-14T07:54:28.882Z
```

<u>コンテンツファイルのデプロイ</u>

コンテンツファイルをデプロイするには、次を使用します。

`aio aem:rde:install world.txt -p /apps/hello.txt`

デプロイメントが成功した場合の応答は、次のようになります。

```
..
#4: deploy completed for content-file world.txt on author,publish - done by 9E0729C05C54FE1A0B49431C@AdobeID at 2022-09-14T07:49:30.644Z
```

<u>Apache/Dispatcher 設定のデプロイ</u>

このタイプの設定では、フォルダー構造全体を zip ファイルの形式で指定する必要があります。 Dispatcher 設定フォルダーのルートから次のコマンドを実行して、zip ファイルを圧縮できます。

`zip -y -r dispatcher.zip`

次に、次のコマンドで設定をデプロイします。

`aio aem:rde:install -t dispatcher-config dispatcher-wknd-2.1.0.zip`

デプロイメントが成功すると、次のような応答が生成されます。

```
..
#5 deploy completed for dispatcher-config dispatcher.zip on author,publish - done by 9E0735C05T54FE1A0B49431C@AdobeID at 2022-10-03T10:26:31.286Z
Logs:
  Cloud manager validator 2.0.49
  2022/10/03 10:26:37 No issues found
  Syntax OK
```

RDE にデプロイされたコードには、Cloud Manager パイプラインとそれに関連する品質ゲートはありませんが、次のコードサンプルに示すように、コードは一部の分析を経てエラーが報告されます。

```
$ aio aem:rde:install ~/.m2/repository/org/apache/felix/org.apache.felix.gogo.jline/1.1.8/org.apache.felix.gogo.jline-1.1.8.jar
...
#19: deploy staged for osgi-bundle org.apache.felix.gogo.jline-1.1.8.jar on author,publish - done by 9E0725C05D74FR1A0B49431C@AdobeID at 2022-09-14T07:54:28.882Z
Logs:
The analyser found the following errors for author :
[requirements-capabilities] com.adobe.aem.temp:org.apache.felix.gogo.jline:1.1.8: Artifact com.adobe.aem.temp:org.apache.felix.gogo.jline:1.1.8 requires [org.apache.felix.gogo.jline/1.1.8] org.apache.felix.gogo; filter:="(&(org.apache.felix.gogo=command.implementation)(version>=1.0.0)(!(version>=2.0.0)))"; effective:=active in start level 20 but no artifact is providing a matching capability in this start level.
[api-regions-exportsimports] com.adobe.aem.temp:org.apache.felix.gogo.jline:1.1.8: Bundle org.apache.felix.gogo.jline:1.1.8 is importing package(s) [org.jline.builtins, org.jline.utils, org.apache.felix.service.command, org.apache.felix.service.threadio, org.jline.terminal, org.jline.reader, org.apache.felix.gogo.runtime, org.jline.reader.impl] in start level 20 but no bundle is exporting these for that start level.
The analyser found the following errors for publish :
[requirements-capabilities] com.adobe.aem.temp:org.apache.felix.gogo.jline:1.1.8: Artifact com.adobe.aem.temp:org.apache.felix.gogo.jline:1.1.8 requires [org.apache.felix.gogo.jline/1.1.8] org.apache.felix.gogo; filter:="(&(org.apache.felix.gogo=command.implementation)(version>=1.0.0)(!(version>=2.0.0)))"; effective:=active in start level 20 but no artifact is providing a matching capability in this start level.
[api-regions-exportsimports] com.adobe.aem.temp:org.apache.felix.gogo.jline:1.1.8: Bundle org.apache.felix.gogo.jline:1.1.8 is importing package(s) [org.jline.builtins, org.jline.utils, org.apache.felix.service.command, org.apache.felix.service.threadio, org.jline.terminal, org.jline.reader, org.apache.felix.gogo.runtime, org.jline.reader.impl] in start level 20 but no bundle is exporting these for that start level.
```

上記のコード例は、バンドルが解決されない場合の動作を示しています。その場合は「ステージング済み」で、他のコードのインストールを通じて要件（この場合はインポートが不足）が満たされた場合にのみインストールされます。

### RDE のステータスの確認 {#checking-rde-status}

RDE CLI を使用して、RDE プラグインを介して実行されたデプロイメントと同様に、環境のデプロイ先の準備が整っているかどうかを確認できます。

実行中：

`aio aem:rde:status`

は次の値を返します。

```
Info for cm-p12345-e987654
Environment: Ready
- Bundles Author:
 com.adobe.granite.sample.demo-1.0.0.SNAPSHOT
- Bundles Publish:
 com.adobe.granite.sample.demo-1.0.0.SNAPSHOT
- Configurations Author:
 com.adobe.granite.demo.MyServlet
- Configurations Publish:
 com.adobe.granite.demo.MyServlet
```

コマンドがデプロイ中のインスタンスに関するメモを返した場合でも、先に進んで次の更新を実行できますが、最後の更新はまだインスタンス上に表示されない可能性があります。

### デプロイメント履歴を表示 {#show-deployment-history}

RDE に対しておこなわれたデプロイメントの履歴を確認するには、次のコマンドを実行します。

`aio aem:rde:history`

次の形式の応答を返します。

`#1: deploy completed for content-package aem-guides-wknd.all-2.1.0.zip on author,publish - done by 029039A55D4DE16A0A494025@AdobeID at 2022-09-12T14:41:55.393Z`

### RDE からの削除 {#deleting-from-rde}

CLI ツールを使用して、RDE に以前にデプロイされた設定やバンドルを削除できます。 以下を使用： `status` コマンドを使用して、削除可能な項目のリストを取得できます。 `bsn` ( バンドルおよび `pid` を参照し、削除コマンドで参照する設定用。

例えば、 `com.adobe.granite.demo.MyServlet.cfg.json` がインストールされている場合、 `bsn` が `com.adobe.granite.demo.MyServlet`（なし） **cfg.json** サフィックス

コンテンツパッケージまたはコンテンツファイルの削除はサポートされていません。 削除するには、RDE をリセットし、デフォルトの状態に戻す必要があります。

詳しくは、以下の例を参照してください。

```
aio aem:rde:delete com.adobe.granite.csrf.impl.CSRFFilter
#13: delete completed for osgi-config com.adobe.granite.csrf.impl.CSRFFilter on author - done by karl at 2022-09-12T22:01:01.955Z
#14: delete completed for osgi-config com.adobe.granite.csrf.impl.CSRFFilter on publish - done by karl at 2022-09-12T22:01:12.979Z
```

## リセット {#reset-rde}

RDE をリセットすると、オーサーインスタンスとパブリッシュインスタンスの両方から、すべてのカスタムコード、設定およびコンテンツが削除されます。 これは、例えば、RDE を使用して特定の機能をテストしていて、別の機能をテストするためにデフォルトの状態にリセットしたい場合に便利です。

<!-- Alexandru: hiding for now, please don't delete

Resetting can be done via [Cloud Manager](#reset-the-rde-cloud-manager) or via the [command line](#reset-the-rde-command-line). Resetting takes a few minutes and all existing content and code will be deleted from the RDE.

>[NOTE!]
>
>You must be assigned the Cloud Manager Developer role in order to be able to use the reset feature. If not, a reset action will result in an error.

### Reset the RDE via Command Line {#reset-the-rde-command-line}

You can reset the RDE and return it to a default state by running:

`aio aem:rde:reset`

This usually takes a few minutes. Use the [status command](#checking-rde-status) to check when the environment is ready again.

### Reset the RDE in Cloud Manager {#reset-the-rde-cloud-manager} -->

次の手順に従うことで、Cloud Manager を使用して RDE をリセットできます。

1. [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) で Cloud Manager にログインし、適切な組織を選択します。

1. RDE をリセットするプログラムをクリックします。

1. 次の **概要**&#x200B;ページで、画面上部の「**環境**」タブをクリックします。

   ![「環境」タブ](/help/implementing/cloud-manager/assets/environments-tab2.png)

   * または、**環境**&#x200B;カードの「**すべて表示**」ボタンをクリックして、「**環境**」タブに直接ジャンプします。

      ![「すべて表示」オプション](/help/implementing/cloud-manager/assets/environment-showall.png)

1. この **環境** ウィンドウが開き、プログラムのすべての環境が一覧表示されます。

   ![「環境」タブ](/help/implementing/cloud-manager/assets/environments-tab-populated.png)

1. リセットする RDE の省略記号ボタンをクリックし、「 」を選択します。 **リセット**.

   ![環境の詳細を表示](/help/implementing/cloud-manager/assets/rde-reset.png)

1. 「 」をクリックして、RDE をリセットすることを確認します **リセット** をクリックします。

   ![リセットを確認](/help/implementing/cloud-manager/assets/rde-reset-confirm.png)

1. バナー通知で、リセットプロセスが開始したことを確認します。

   ![バナー通知をリセット](/help/implementing/cloud-manager/assets/rde-reset-banner.png)

RDE のリセットプロセスが開始されると、通常は完了し、環境をデフォルトの状態に戻すのに数分かかります。 リセットプロセスのステータスは、 **ステータス** 列 **環境** カードまたは **環境** ウィンドウ

![RDE リセットステータス](/help/implementing/cloud-manager/assets/rde-reset-status-environments-card.png)

省略記号ボタンを使用して、RDE を **環境** カード **概要** ページ。

![環境カードから RDE をリセット](/help/implementing/cloud-manager/assets/rde-reset-environments-card.png)

Cloud Manager を使用した環境の管理方法について詳しくは、 [Cloud Manager のドキュメント。](/help/implementing/cloud-manager/manage-environments.md)

## 実行モード {#runmodes}

以下の例のように、フォルダー名にサフィックスを使用して、RDE 固有の OSGI 設定を適用できます。

* `config.rde`
* `config.author.rde`
* `config.publish.rde`

詳しくは、 [実行モードのドキュメント](/help/implementing/deploying/overview.md#runmodes) 実行モードの一般的な情報については、を参照してください。

>[!NOTE]
>
>RDE OSGI 設定は、バンドルの `dev` 実行モード。

RDE は、/apps の下の install.rde フォルダー（または install.author.rde または install.publish.rde）にコンテンツをインストールできるという点で、他の環境とは異なります。 これにより、コンテンツを Git にコミットし、コマンドラインツールを使用して RDE に配信できます。

## コンテンツを使用した入力 {#populating-content}

RDE がリセットされると、すべてのコンテンツが削除されるので、必要に応じて、コンテンツを追加するために明示的なアクションを実行する必要があります。 ベストプラクティスとして、RDE で機能を検証またはデバッグするためのテストコンテンツとして使用する一連のコンテンツを組み立てることを検討します。 そのコンテンツを RDE に入力する方法としては、次のような方法が考えられます。

1. コマンドラインツールを使用して、コンテンツパッケージを RDE に明示的に同期します。

1. /apps の下の install.rde フォルダー内の git にサンプルコンテンツを配置してコミットし、コマンドラインツールを使用して包括的なコンテンツパッケージを RDE に同期します。

1. パッケージマネージャーを使用

コンテンツパッケージを同期する場合は、1 GB までに制限されます。

## ログ {#logging}

ログレベルは、OSGi 設定を変更することで設定できます。 次を確認します。 [ドキュメント](/help/implementing/developing/introduction/logging.md) を参照してください。

## RDE とクラウド開発環境の違いは何ですか？ {#how-are-rds-different-from-cloud-development-environments}

RDE はクラウド開発環境に似た多くの方法で用意されていますが、コードをすばやく同期できるように、アーキテクチャには若干の小さな違いがあります。 コードを RDE に取得するメカニズムは異なります。RDE の場合はローカル開発環境からコードを同期し、Cloud Development Environments の場合は Cloud Manager を使用してコードをデプロイします。

このような理由から、RDE 環境でコードを検証した後、実稼動以外のパイプラインを使用して Cloud Development Environment にコードをデプロイすることをお勧めします。 最後に、実稼動パイプラインでをデプロイする前に、コードをテストします。

また、次の考慮事項にも注意してください。

* RDE は、現在、Cloud Manager フロントエンドパイプラインを使用してデプロイされたフロントエンドコードの表示とデバッグをサポートしていません。
* RDE は現在、プレリリースチャネルをサポートしていません。


## 必要な RDE の数 {#how-many-rds-do-i-need}

RDE は、ライセンスが必要な各ソリューションで使用でき、Adobeでは追加の RDE も提供されます。RDE は、実稼動（サンドボックス以外）プログラムのライセンスを取得できます。

必要な RDE の数は、組織のメークアップとプロセスによって異なります。 最も柔軟なモデルは、組織がAEM Cloud Service開発者それぞれに対して専用の RDE を購入する場所です。 このモデルでは、各開発者は、RDE 環境が使用可能かどうかに関して他のチームメンバーと調整することなく、RDE でコードをテストできます。

もう 1 つの極端な例では、1 つの RDE を持つチームが内部プロセスを使用して、特定の時間にどの開発者が環境を使用できるかを調整する場合があります。 開発者が中間機能のマイルストーンに達し、必要な変更をすばやくおこなえるクラウド環境で検証する準備が整った場合に、この問題が発生する可能性があります。

中間モデルとは、組織が多数の RDE を購入し、未使用の RDE が使用可能になる可能性が高くなるモデルです。 1 つの戦略は、スクラムチームまたは主要機能ごとに RDE を割り当てることです。 内部プロセスを使用して、環境の使用状況を調整できます。

## AEM FormsCloud Serviceラピッド開発環境 (RDE) は他の環境とどのように異なりますか？ {#how-are-forms-rds-different-from-cloud-development-environments}

Formsの開発者は、AEM FormsCloud Serviceラピッド開発環境を使用して、アダプティブForms、ワークフロー、およびコアコンポーネントのカスタマイズ、サードパーティシステムとの統合などのカスタマイズを迅速に開発できます。 AEM FormsCloud Serviceラピッド開発環境 (RDE) は、アダプティブフォームの送信時にレコードのドキュメントを生成するなど、レコードのドキュメントを必要とする機能をサポートしていません。 以下に示す機能は、レコードのドキュメントを使用します。 これらは、急速開発環境 (RDE) では使用できません。

* アダプティブフォーム用のレコードのドキュメントの設定
* アダプティブフォームの送信時またはワークフローステップでのレコードのドキュメントの生成
* レコードのドキュメントを電子メール送信アクションまたはワークフローの電子メールステップで添付ファイルとして送信
* アダプティブフォームまたはワークフローステップでのAdobe Signの使用
* 通信 API

レコードのドキュメントを必要とする機能の使用時にエラーメッセージが表示されます。

>[!NOTE]
>
> Formsの UI と他の開発環境 (RDE) の間に変更はありません。 レコードのドキュメント関連のすべてのオプション（アダプティブフォームのレコードのドキュメントテンプレートの選択など）は、UI に引き続き表示されます。 これらの環境には、このようなオプションをテストするレコードのドキュメント機能はありません。 したがって、「レコードのドキュメント」オプションを選択した場合、アクションは実行されず、エラーメッセージが表示または返されます。

