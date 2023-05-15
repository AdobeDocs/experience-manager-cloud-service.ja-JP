---
title: 迅速な開発環境
description: クラウド環境で迅速な開発反復処理を行うために、迅速な開発環境を活用する方法について説明します。
exl-id: 1e9824f2-d28a-46de-b7b3-9fe2789d9c68
source-git-commit: 0095cb1fff99a52f5a048833b3d5a65643c1056d
workflow-type: tm+mt
source-wordcount: '3325'
ht-degree: 97%

---

# 迅速な開発環境 {#rapid-development-environments}

変更をデプロイするために、現在のクラウド開発環境では、CI／CD パイプラインと呼ばれる広範なコードセキュリティと品質ルールを採用したプロセスを使用する必要があります。 迅速かつ反復的な変更が必要な状況に対応するために、アドビは迅速な開発環境（RDE）を導入しました。

RDE を使用すると、デベロッパーは、ローカル開発環境での動作が証明済みの機能に要するテスト時間を最小限に抑え、変更を迅速にデプロイおよび確認できます。

変更を RDE でテストしたら、Cloud Manager パイプラインを通じて通常のクラウド開発環境にデプロイできます。

>[!VIDEO](https://video.tv.adobe.com/v/3415582/?quality=12&learn=on)


[設定方法](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/developing/rde/how-to-setup.html?lang=ja)、[使用方法](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/developing/rde/how-to-use.html?lang=ja)、RDE を使用した[開発ライフサイクル](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/developing/rde/development-life-cycle.html?lang=ja)を示す追加のビデオを参照できます。

## はじめに {#introduction}

RDE は、コード、コンテンツ、Apache または Dispatcher の設定に使用できます。通常のクラウド開発環境とは異なり、デベロッパーはローカルのコマンドラインツールを使用して、ローカルで作成されたコードを RDE に同期できます。

すべてのプログラムには RDE がプロビジョニングされます。サンドボックスアカウントの場合、数時間使用されなかった後に休止状態になります。

作成時に、RDE は使用可能な最新の AEM バージョンに設定されます。Cloud Manager を使用して実行できる RDE のリセットは、RDE を循環させ、使用可能な最新の AEM バージョンに設定します。

通常、特定の機能のテストとデバッグには、1 人のデベロッパーが任意の時点で RDE を使用します。開発セッションが完了すると、RDE は次の使用時にデフォルトの状態にリセットできます。

追加の RDE は、実稼動（非サンドボックス）プログラム用としてライセンス登録される場合があります。

## プログラムでの RDE の有効化 {#enabling-rde-in-a-program}

Cloud Manager を使用してプログラムの RDE を作成するには、次の手順に従います。

1. [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) で Cloud Manager にログインし、適切な組織を選択します。

1. RDE を追加するプログラムをクリックして詳細を表示します。

   * RDE は、[サンドボックスプログラム](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/creating-sandbox-programs.md)と[実稼動プログラム](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/introduction-production-programs.md)の両方に追加できます。

1. **プログラムの概要**&#x200B;ページで、**環境**&#x200B;カードの「**環境を追加**」をクリックして環境を追加します。

   ![環境カード](/help/implementing/cloud-manager/assets/no-environments.png)

   * 「**環境を追加**」オプションは「**環境**」タブでも使用できます。

      ![「環境」タブ](/help/implementing/cloud-manager/assets/environments-tab.png)

   * 「**環境を追加**」オプションは、権限がない場合やライセンスされているリソースによっては、無効になっている場合があります。

1. 表示される&#x200B;**環境を追加**&#x200B;ダイアログで以下を行います。

   * **環境タイプを選択**&#x200B;見出しの下にある「**迅速な開発**」を選択します。
      * 使用可能な環境または使用中の環境の数は、環境タイプの後ろの括弧内に表示されます。
   * 環境の&#x200B;**名前**&#x200B;を指定します。
   * 環境のオプションの&#x200B;**説明**&#x200B;をオプションで入力します。
   * 「**クラウドリージョン**」を選択します。

   ![環境を追加ダイアログ](/help/implementing/cloud-manager/assets/add-environment-wizard.png)

1. 「**保存**」をクリックして、指定された環境を追加します。

これで、**概要**&#x200B;画面の&#x200B;**環境**&#x200B;カードに新しい環境が表示されるようになりました。

作成時に、RDE は使用可能な最新の AEM バージョンに設定されます。RDE リセット（Cloud Manager を使用して実行することも可能）は、RDE を循環させ、最新の AEM バージョンに設定します。

Cloud Manager を使用した環境の作成、環境へのアクセス権のあるユーザーの管理、カスタムドメインの割り当てについて詳しくは、[Cloud Manager ドキュメント](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/program-types.md)を参照してください。

## RDE コマンドラインツールのインストール {#installing-the-rde-command-line-tools}

Cloud Manager を使用してプログラムに RDE を追加したら、次の手順に従ってコマンドラインツールを設定して、RDE を操作できます。

>[!IMPORTANT]
>
>Adobe I/O CLI と関連プラグインが正しく動作するように、最新バージョンの[ノードと NPM がインストールされている](https://nodejs.org/en/download/)ことを確認してください。


1. [こちら](https://developer.adobe.com/runtime/docs/guides/tools/cli_install/)の手順に従って、Adobe I/O CLI ツールをインストールします。
1. Adobe I/O CLI ツールの Cloud Manager プラグインをインストールし、[こちら](https://github.com/adobe/aio-cli-plugin-cloudmanager)の説明に従って設定します。
1. 次のコマンドを実行して、Adobe I/O CLI ツールの AEM RDE プラグインをインストールします。

   ```
   aio plugins:install @adobe/aio-cli-plugin-aem-rde
   aio plugins:update
   ```

1. 以下の組織 ID に対して Cloud Manager プラグインを設定します。

   `aio config:set cloudmanager_orgid 4E03EQC05D34GL1A0B49421C@AdobeOrg`

   さらに、英数字の文字列を独自の組織 ID に置き換えます。これは、[こちら](https://experienceleague.adobe.com/docs/core-services/interface/administration/organizations.html?lang=ja#concept_EA8AEE5B02CF46ACBDAD6A8508646255)の戦略を使用して検索できます。

1. 次に、以下のプログラム ID を設定します。

   `aio config:set cloudmanager_programid 12345`

1. 次に、RDE がアタッチされる以下の環境 ID を設定します。

   `aio config:set cloudmanager_environmentid 123456`

1. プラグインの設定が完了したら、以下を実行してログインします。

   `aio login`

   ログイン成功時の応答は以下の出力のようになりますが、表示される値は無視できます。

   ```
   ...
   You are currently in:
   1. Org: <no org selected>
   2. Project: <no project selected>
   3. Workspace: <no workspace selected>
   ```

1. 以下を実行して、ログインが正常に完了したことを確認します。

   `aio cloudmanager:list-programs`

   設定した組織の下にあるすべてのプログラムがリストされます。

   上記では、Cloud Manager **デベロッパー - Cloud Service** 製品プロファイルのメンバーである必要があります。詳しくは、[このページ](/help/journey-onboarding/assign-profiles-cloud-manager.md#assign-developer)を参照してください。

   また、このデベロッパーの役割を持っていることを、以下のコマンドを実行して Developer Console にログインすることでも確認できます。

   `aio cloudmanager:environment:open-developer-console`

   >[!TIP]
   >
   >`Warning: cloudmanager:list-programs is not a aio command.` エラーが表示された場合は、以下のコマンドを実行して [aio-cli-plugin-cloudmanager](https://github.com/adobe/aio-cli-plugin-cloudmanager) をインストールする必要があります。
   >
   >
   ```
   >aio plugins:install @adobe/aio-cli-plugin-cloudmanager
   >```

詳細とデモンストレーションについては、[RDE の設定方法](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/developing/rde/how-to-setup.html?lang=ja)のビデオチュートリアルを参照してください。

## 新機能の開発時の RDE の使用 {#using-rde-while-developing-a-new-feature}

アドビでは、新しい機能を開発する際に、次のワークフローを使用することをお勧めします。

* 中間マイルストーンに達し、AEM as a Cloud Service SDK を使用してローカルで正常に検証された場合、コードは、メイン行にまだ含まれていない Git feature ブランチにコミットする必要があります。ただし、Git へのコミットはオプションです。「中間マイルストーン」を構成するものは、チームの習慣に応じて異なります。 例えば、数行の新しいコードや、半日の作業、サブ機能の完了といったものがあります。

* RDE が別の機能で使用されていて、[デフォルトの状態にリセット](#reset-rde)したい場合は、RDE をリセットします。<!-- Alexandru: hiding for now, please don't delete This can be done via [Cloud Manager](#reset-the-rde-cloud-manager) or via the [command line](#reset-the-rde-command-line). -->リセットには数分かかり、既存のコンテンツとコードはすべて削除されます。 RDE ステータスコマンドを使用すると、RDE の準備が完了したことを確認できます。RDE は、最新の AEM リリースバージョンで復活します。

   >[!IMPORTANT]
   >
   > ステージング環境と実稼動環境が AEM リリースの自動更新を受信しておらず、最新の AEM リリースバージョンから大幅に遅れている場合は、RDE で実行されているコードが、ステージング環境と実稼動環境でのコードの機能と一致しない可能性があることに留意してください。その場合、実稼動環境にデプロイする前に、ステージングでコードのテストを徹底的に実行することが特に重要です。


* RDE コマンドラインインターフェイスを使用して、ローカルコードを RDE に同期します。 オプションには、コンテンツパッケージ、特定のバンドル、OSGi 設定ファイル、コンテンツファイル、Apache／Dispatcher 設定の zip ファイルのインストールが含まれます。 リモートコンテンツパッケージの参照も可能です。 詳しくは、[RDE コマンドラインツール](#rde-cli-commands)の節を参照してください。 ステータスコマンドを使用すると、デプロイメントが成功したことを検証できます。必要に応じて、パッケージマネージャーを使用してコンテンツパッケージをインストールします。

* RDE でコードをテストします。 Cloud Manager では、オーサー URL とパブリッシュ URL を使用できます。

* コードが期待どおりに動作しない場合は、標準のデバッグ手法を使用して問題を把握し、適切な変更を行ってください。コードの変更を Git にコミットせずに（変更が検証されていないため）、ローカル CLI を使用してコードを RDE に同期します。 問題が解決するまで繰り返します。

* コードが期待どおりに動作したら、コードを Git feature ブランチにコミットします。

* RDE に同期したコードは Cloud Manager パイプラインを使用しないので、Cloud Manager 非実稼動パイプラインを使用して、Git feature ブランチをクラウド開発環境にデプロイする必要があります。 これにより、コードが Cloud Manager 品質ゲートを通過するかどうかが検証され、後で Cloud Manager 実稼動パイプラインを使用してコードが正常にデプロイされることを確認できます。

* 機能のすべてのコードの準備が整い、RDE とクラウド開発環境の両方で正常に動作するまで、各中間マイルストーンに対して上記の手順を繰り返します。

* Cloud Manager 実稼動パイプラインを使用してコードを実稼動環境にデプロイします。

## RDE を使用した既存機能のデバッグ {#use-rde-to-debug-an-existing-feature}

このワークフローは、新規機能の開発に似ています。 違いは、RDE に同期されるコードは、問題が見つかった環境にプッシュされた内容の Git ラベルを反映している点です。 また、アップストリーム環境に合ったコンテンツをデプロイすると便利です。この操作は、コンテンツパッケージの書き出しと読み込みから行えます。

## 同じ RDE で共同作業する複数のデベロッパー {#multiple-developers-collaborating-on-the-same-rde}

RDE は、一度に 1 つのプロジェクトをサポートします。コードはローカル開発環境から RDE 環境に同期されるので、1 人のデベロッパーが任意の時点で独自に使用するのが最も自然です。

ただし、慎重に調整することで、複数のデベロッパーが特定の機能を検証したり、特定の問題をデバッグしたりできます。重要なのは、特定のデベロッパーが行ったコードの変更を他のデベロッパーが取り込めるように、各デベロッパーがローカルプロジェクトの同期を維持することです。さもないと、あるデベロッパーが誤って他のデベロッパーのコードを上書きしてしまう恐れがあります。 各デベロッパーに推奨される戦略は、RDE に同期する前に共有 Git ブランチに変更をコミットし、他のデベロッパーが変更を取り込んでから独自の変更を行えるようにすることです。

## RDE コマンドラインツールのコマンド {#rde-cli-commands}

### ヘルプ／一般情報 {#help}

* コマンドのリストを表示するには、次のように入力します。

   `aio aem:rde`

* コマンドの詳細なヘルプを表示するには、次のように入力します。

   `aio aem rde <command> --help`

### RDE へのデプロイ {#deploying-to-rde}

この節では、RDE CLI を使用して、バンドル、OSGi 設定、コンテンツパッケージ、個々のコンテンツファイル、Apache または Dispatcher 設定のデプロイ、インストールまたは更新する方法について説明します。

一般的な使用パターンは `aio aem:rde:install <artifact>` です。

以下に例をいくつか示します。

<u>コンテンツパッケージのデプロイ</u>

`aio aem:rde:install sample.demo.ui.apps.all-1.0.0-SNAPSHOT.zip`

デプロイメントが成功した場合の応答は、次のようになります。

```
...
#1: deploy completed for content-package sample.demo.ui.apps.all-1.0.0-SNAPSHOT.zip on author,publish - done by 9E072FC75D54FE1A2B49431C@AdobeID at 2022-09-13T11:32:06.229Z
```

オプションで、リモートリポジトリを参照できます。

`aio aem:rde:install -t content-package "https://repo1.maven.org/maven2/com/adobe/aem/guides/aem-guides-wknd.all/2.1.0/aem-guides-wknd.all-2.1.0.zip"`

デフォルトでは、アーティファクトはオーサー層とパブリッシュ層の両方にデプロイされますが、「-s」フラグを使用して特定の層をターゲットにすることができます。

任意のAEMパッケージをデプロイできます ( コード、コンテンツ、または [コンテナパッケージ](/help/implementing/developing/introduction/aem-project-content-package-structure.md#container-packages) （「all」パッケージとも呼ばれます）。

>[!IMPORTANT]
>
>WKND プロジェクトの Dispatcher 設定は、上記の content-package のインストールではデプロイされません。「Apache／Dispatcher 設定のデプロイ」の手順に従って、別途デプロイする必要があります。

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

<u>Apache／Dispatcher 設定のデプロイ</u>

このタイプの設定では、フォルダー構造全体を zip ファイル形式にする必要があります。 

AEM プロジェクトの `dispatcher` モジュールから、以下の maven コマンドを実行して、Dispatcher 設定を zip 形式で圧縮できます。

`mvn clean package`

または `dispatcher` モジュールの `src` ディレクトリから以下の zip コマンドを使用します。

`zip -y -r dispatcher.zip .`

その後、次のコマンドで設定をデプロイします。

`aio aem:rde:install target/aem-guides-wknd.dispatcher.cloud-X.X.X-SNAPSHOT.zip`

>[!TIP]
>
>上記のコマンドは、[WKND](https://github.com/adobe/aem-guides-wknd) プロジェクトの Dispatcher 設定をデプロイしていることを前提としています。プロジェクトの Dispatcher 設定をデプロイする際には、`X.X.X` を対応する WKND プロジェクトのバージョン番号またはプロジェクト固有のバージョン番号に必ず置き換えてください。

>[!NOTE]
>
>RDE は、「フレキシブルモード」の Dispatcher 設定をサポートしていますが、「レガシーモード」の Dispatcher 設定はサポートしていません。 詳しくは、 [dispatcher ドキュメント](/help/implementing/dispatcher/disp-overview.md#validation-debug) 」を参照してください。 また、 [フレキシブルモードへの移行](/help/implementing/dispatcher/validation-debug.md#migrating)まだおこなっていない場合は、をクリックします。

デプロイメントが成功すると、次のような応答が生成されます。

```
..
#5 deploy completed for dispatcher-config dispatcher.zip on author,publish - done by 9E0735C05T54FE1A0B49431C@AdobeID at 2022-10-03T10:26:31.286Z
Logs:
  Cloud manager validator 2.0.49
  2022/10/03 10:26:37 No issues found
  Syntax OK
```

RDE にデプロイされたコードは、Cloud Manager パイプラインとそれに関連する品質ゲートを通過しませんが、次のコードサンプルに示すように、コードは一部の分析を経てエラーを報告します。

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

上記のコード例は、バンドルが解決されない場合の動作を示しています。この場合、バンドルは「ステージング済み」で、他のコードのインストールによって要件（この場合は、読み込み不足）が満たされた場合にのみインストールされます。

### RDE のステータス確認 {#checking-rde-status}

RDE CLI を使用すると、RDE プラグインを介して実行されたデプロイメントなど、環境にデプロイする準備が整っているかどうかを確認できます。

次のコードを実行すると、

`aio aem:rde:status`

次の値を返します。

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

コマンドがデプロイ中のインスタンスに関するメモを返した場合でも、先に進んで次の更新を実行できますが、最終更新がまだインスタンス上に表示されていない可能性があります。

### デプロイメント履歴の表示 {#show-deployment-history}

RDE に対して行われたデプロイメントの履歴を確認するには、次のコマンドを実行します。

`aio aem:rde:history`

次の形式の応答が返されます。

`#1: deploy completed for content-package aem-guides-wknd.all-2.1.0.zip on author,publish - done by 029039A55D4DE16A0A494025@AdobeID at 2022-09-12T14:41:55.393Z`

### RDE からの削除 {#deleting-from-rde}

CLI ツールを使用すると、RDE に以前にデプロイされた設定やバンドルを削除できます。 `status` コマンドを使用して、削除可能な項目のリストを取得できます。これには、DELETE コマンドで参照するバンドル用の `bsn` と設定用の `pid` が含まれます。

例えば、`com.adobe.granite.demo.MyServlet.cfg.json` がインストールされている場合、`bsn` は `com.adobe.granite.demo.MyServlet` のみ（**cfg.json** サフィックスなし）になります。

コンテンツパッケージまたはコンテンツファイルは削除対象外です。 削除するには、RDE をリセットする必要があります。これにより、デフォルトの状態に戻ります。

詳しくは、以下の例を参照してください。

```
aio aem:rde:delete com.adobe.granite.csrf.impl.CSRFFilter
#13: delete completed for osgi-config com.adobe.granite.csrf.impl.CSRFFilter on author - done by karl at 2022-09-12T22:01:01.955Z
#14: delete completed for osgi-config com.adobe.granite.csrf.impl.CSRFFilter on publish - done by karl at 2022-09-12T22:01:12.979Z
```

詳細とデモンストレーションについては、[RDE コマンドの使用方法](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/developing/rde/how-to-use.html?lang=ja)のビデオ チュートリアルを参照してください。

## リセット {#reset-rde}

RDE をリセットすると、すべてのカスタムコード、設定およびコンテンツが、オーサーインスタンスとパブリッシュインスタンスの両方から削除されます。これは、例えば、RDE を使用して特定の機能をテストしていて、別の機能をテストするためにデフォルトの状態にリセットしたい場合に便利です。

リセットすると、RDE が使用可能な最新の AEM バージョンに設定されます。

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

次の手順に従って、Cloud Manager を使用して RDE をリセットできます。

1. [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) で Cloud Manager にログインし、適切な組織を選択します。

1. RDE をリセットするプログラムをクリックします。

1. 次の **概要**&#x200B;ページで、画面上部の「**環境**」タブをクリックします。

   ![「環境」タブ](/help/implementing/cloud-manager/assets/environments-tab2.png)

   * または、**環境**&#x200B;カードの「**すべて表示**」ボタンをクリックして、「**環境**」タブに直接ジャンプします。

      ![「すべて表示」オプション](/help/implementing/cloud-manager/assets/environment-showall.png)

1. **環境**&#x200B;ウィンドウが開いて、プログラムのすべての環境が一覧表示されます。

   ![「環境」タブ](/help/implementing/cloud-manager/assets/environments-tab-populated.png)

1. リセットする RDE の「...」ボタンをクリックし、「**リセット**」を選択します。

   ![環境の詳細を表示](/help/implementing/cloud-manager/assets/rde-reset.png)

1. ダイアログで「**リセット**」をクリックして、RDE をリセットすることを確認します。

   ![リセットの確認](/help/implementing/cloud-manager/assets/rde-reset-confirm.png)

1. Cloud Manager はバナー通知で、リセットプロセスが開始したことを確認します。

   ![バナー通知のリセット](/help/implementing/cloud-manager/assets/rde-reset-banner.png)

RDE のリセットプロセスが開始されると、通常、完了して環境がデフォルトの状態に戻るまでに数分かかります。リセットプロセスのステータスは、**環境**&#x200B;カードの&#x200B;**ステータス**&#x200B;列、または&#x200B;**環境**&#x200B;ウィンドウでいつでも確認できます。

![RDE リセットステータス](/help/implementing/cloud-manager/assets/rde-reset-status-environments-card.png)

**概要**&#x200B;ページの&#x200B;**環境**&#x200B;カードから直接「...」ボタンを使用して、RDE をリセットすることもできます。

![環境カードからの RDE のリセット](/help/implementing/cloud-manager/assets/rde-reset-environments-card.png)

Cloud Manager を使用した環境の管理方法について詳しくは、[Cloud Manager のドキュメント](/help/implementing/cloud-manager/manage-environments.md)を参照してください。

## 実行モード {#runmodes}

RDE 固有の OSGI 設定は、以下の例のように、フォルダー名にサフィックスを使用して適用できます。

* `config.rde`
* `config.author.rde`
* `config.publish.rde`

実行モードに関する一般的な情報については、[実行モードのドキュメント](/help/implementing/deploying/overview.md#runmodes)を参照してください。

>[!NOTE]
>
>RDE OSGI 設定は、バンドルの `dev` 実行モードによって宣言された OSGI プロパティの値を継承する点でユニークです。

RDE は、/apps の下の install.rde フォルダー（または install.author.rde または install.publish.rde）にコンテンツをインストールできるという点で、他の環境とは異なります。これにより、コンテンツを Git にコミットし、コマンドラインツールを使用して RDE に配信できます。

## コンテンツへの入力 {#populating-content}

RDE がリセットされると、すべてのコンテンツが削除されるため、必要に応じて、コンテンツを追加するための明示的なアクションを実行する必要があります。ベストプラクティスとして、RDE の機能を検証またはデバッグするためのテストコンテンツとして使用する一連のコンテンツを組み立てることを検討してください。 RDE にそのコンテンツを入力する方法はいくつか考えられます。

1. コマンドラインツールを使用したコンテンツパッケージの RDE への明示的な同期化

1. /apps の下の install.rde フォルダー内の Git にサンプルコンテンツを配置してコミットし、コマンドラインツールを使用して包括的なコンテンツパッケージを RDE に同期します。

1. 以下を使用： [コンテンツコピーツール](/help/implementing/developing/tools/content-copy.md) を使用して、実稼動、ステージング、開発環境、または別の RDE から定義済みのコンテンツセットをコピーできます。

1. パッケージマネージャーの使用

コンテンツパッケージを同期する場合は、1 GB までに制限されます。

## ログ {#logging}

OSGi 設定を変更すると、ログレベルを設定できます。 詳しくは、[ドキュメント](/help/implementing/developing/introduction/logging.md)を確認してください。

## RDE とクラウド開発環境の違いは何ですか？ {#how-are-rds-different-from-cloud-development-environments}

RDE は多くの点でクラウド開発環境に似ていますが、コードをすばやく同期できるように、アーキテクチャ上の小さな違いが若干あります。 コードを RDE に取得するメカニズムが異なります。RDE の場合はローカル開発環境からコードを同期し、クラウド開発環境の場合は Cloud Manager を使用してコードをデプロイします。

このような理由から、RDE 環境でコードを検証した後、実稼動以外のパイプラインを使用してコードをクラウド開発環境にデプロイすることをお勧めします。最後に、実稼動パイプラインでデプロイする前に、コードをテストします。

また、次の考慮事項にも注意してください。

* RDE にプレビュー層は含まれない
* RDE は現在、Cloud Manager フロントエンドパイプラインを使用してデプロイされたフロントエンドコードの表示とデバッグをサポートしていません。
* RDE は現在、プレリリースチャネルをサポートしていません。


## 必要な RDE の数 {#how-many-rds-do-i-need}

RDE は、ライセンスが付与されている各ソリューションで使用でき、Adobeでは追加の RDE も提供されます。RDE は実稼動（サンドボックス以外）プログラム用としてライセンス登録できます。

必要な RDE の数は、組織の構成とプロセスによって異なります。最も柔軟なモデルでは、組織が AEM Cloud Service の各デベロッパーに対して専用の RDE を購入できます。各デベロッパーはこのモデルで、RDE 環境が使用可能かどうかに関して他のチームメンバーと調整することなく、RDE でコードをテストできます。

もう 1 つの極端な例としては、1 つの RDE を持つチームが内部プロセスを使用して、特定の時間にどのデベロッパーが環境を使用できるかを調整する場合があります。これは、デベロッパーが中間機能のマイルストーンに達し、必要な変更をすばやく行えるクラウド環境での検証の準備を整えることが条件となります。

中間モデルとは、組織が多数の RDE を購入し、未使用の RDE が使用可能になる可能性が高くなるモデルです。1 つの戦略は、スクラムチームまたは主要機能ごとに RDE を割り当てることです。内部プロセスを使用して、環境の使用状況を調整できます。

## AEM FormsCloud Service の迅速な開発環境（RDE）は他の環境とどのように異なりますか？ {#how-are-forms-rds-different-from-cloud-development-environments}

Forms のデベロッパーは、AEM FormsCloud Service の迅速な開発環境を使用して、アダプティブフォーム、ワークフロー、およびコアコンポーネントのカスタマイズ、サードパーティシステムとの統合などのカスタマイズを迅速に開発できます。AEM Forms Cloud Service の迅速な開発環境 (RDE) は、アダプティブフォームの送信時にレコードのドキュメントを生成するなど、レコードのドキュメントを必要とする機能や通信 API をサポートしていません。以下に示す AEM Forms の機能は、迅速な開発環境（RDE）では使用できません。

* アダプティブフォーム用のレコードのドキュメントの設定
* アダプティブフォームの送信時またはワークフローステップでのレコードのドキュメントの生成
* レコードのドキュメントをメール送信アクションまたはワークフローのメールステップで添付ファイルとして送信
* アダプティブフォームまたはワークフローステップでの Adobe Sign の使用
* 通信 API

>[!NOTE]
>
> 迅速な開発環境（RDE）の UI と Forms 向けの他の Cloud Service 環境の UI に違いはありません。アダプティブフォームのレコードテンプレートのドキュメントの選択など、オプション関連のレコードのすべてのドキュメントは UI に引き続き表示されます。これらの環境には、こうしたオプションをテストするためのレコードのドキュメント機能や通信 API がありません。そのため、通信 API またはレコードのドキュメント機能を必要とするオプションを選択した場合、アクションは実行されず、エラーメッセージが表示または返されます。

## RDE に関するチュートリアル

AEM as a Cloud Serviceでの RDE について詳しくは、[設定方法、使用方法、開発ライフサイクルに関するビデオチュートリアル](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/developing/rde/overview.html?lang=ja)をご覧ください。
