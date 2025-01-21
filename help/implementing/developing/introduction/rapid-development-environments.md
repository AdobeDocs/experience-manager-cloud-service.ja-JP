---
title: 迅速な開発環境
description: クラウド環境で迅速な開発反復処理を行うために、迅速な開発環境を活用する方法について説明します。
exl-id: 1e9824f2-d28a-46de-b7b3-9fe2789d9c68
feature: Developing
role: Admin, Architect, Developer
source-git-commit: 24c34daebf7d45d9262181890310eb196c58a7db
workflow-type: tm+mt
source-wordcount: '4990'
ht-degree: 97%

---

# 迅速な開発環境 {#rapid-development-environments}

変更をデプロイするために、現在のクラウド開発環境では、CI／CD パイプラインと呼ばれる広範なコードセキュリティと品質ルールを採用したプロセスを使用する必要があります。迅速かつ反復的な変更が必要な状況に対応するために、アドビは迅速な開発環境（RDE）を導入しました。

RDE を使用すると、デベロッパーは、ローカル開発環境での動作が証明済みの機能に要するテスト時間を最小限に抑え、変更を迅速にデプロイおよび確認できます。

変更を RDE でテストしたら、Cloud Manager パイプラインを通じて通常のクラウド開発環境にデプロイできます。

>[!NOTE]
> [ディスコードチャネル](https://discord.com/channels/1131492224371277874/1245304281184079872)で RDE 開発者に連絡できます。RDE のトピックに関して、自由に質問したり、フィードバックを提供したりしてください。

>[!VIDEO](https://video.tv.adobe.com/v/3415582/?quality=12&learn=on)


[設定方法](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/developing/rde/how-to-setup.html?lang=ja)、[使用方法](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/developing/rde/how-to-use.html?lang=ja)、RDE を使用した[開発ライフサイクル](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/developing/rde/development-life-cycle.html?lang=ja)を示す追加のビデオを参照できます。

## はじめに {#introduction}

RDE は、コード、コンテンツ、Apache または Dispatcher の設定に使用できます。通常のクラウド開発環境とは異なり、デベロッパーはローカルのコマンドラインツールを使用して、ローカルで作成されたコードを RDE に同期できます。

すべてのプログラムには RDE がプロビジョニングされます。サンドボックスアカウントの場合、数時間使用されなかった後に休止状態になります。

作成時に、RDE は使用可能な最新の Adobe Experience Manager（AEM）バージョンに設定されます。Cloud Manager を使用して実行できる RDE のリセットは、RDE を循環させ、使用可能な最新の AEM バージョンに設定します。

通常、特定の機能のテストとデバッグには、1 人のデベロッパーが任意の時点で RDE を使用します。開発セッションが完了すると、RDE は次の使用時にデフォルトの状態にリセットできます。

追加の RDE は、実稼動（非サンドボックス）プログラム用としてライセンス登録される場合があります。

## プログラムでの RDE の有効化 {#enabling-rde-in-a-program}

Cloud Manager を使用してプログラムの RDE を作成するには、次の手順に従います。

1. [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) で Cloud Manager にログインし、適切な組織を選択します。

1. RDE を追加するプログラムをクリックして詳細を表示します。

   * RDE は、[サンドボックスプログラム](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/creating-sandbox-programs.md)および[実稼動プログラム](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/introduction-production-programs.md)の両方に追加できます。

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
>Adobe I/O CLI と関連プラグインが正しく動作するように、バージョン 20 の[ノードと NPM がインストールされている](https://nodejs.org/en/download/)ことを確認してください。


1. こちらの[手順](https://developer.adobe.com/runtime/docs/guides/tools/cli_install/)に従って、Adobe I/O CLI ツールをインストールします。
1. Adobe I/O CLI ツールの AEM RDE プラグインのインストール

   ```
   aio plugins:install @adobe/aio-cli-plugin-aem-rde
   aio plugins:update
   ```

1. aio クライアントを使用してログインします。

   ```
   aio login
   ```

   ログイン情報（トークン）はグローバル aio 設定に保存されるので、1 つのログインと組織のみがサポートされます。異なるログインや組織を必要とする複数の RDE を使用する場合は、次の例に従ってコンテキストを導入します。

   <details><summary>この例に従って、RDE ログインの 1 つにローカルコンテキストを設定します</summary>
   特定のコンテキスト内の現在のディレクトリにある .aio ファイルにログイン情報をローカルに保存するには、次の手順に従います。また、コンテキストは、CI/CD 環境またはスクリプトを設定する賢明な方法です。この機能を利用するには、aio-cli バージョン 10.3.1 以上を使用する必要があります。「npm install -g @adobe/aio-cli」を使用して更新します。

   「mycontext」というコンテキストを作成し、ログインコマンドを呼び出す前に、認証プラグインを使用してデフォルトのコンテキストとして設定します。

   ```
   aio config set --json -l "ims.contexts.mycontext" "{ cli.bare-output: false }"
   aio auth ctx -s mycontext
   aio login --no-open
   ```

   >[!NOTE]
   > `--no-open` オプションを指定したログインコマンドでは、デフォルトのブラウザーを開く代わりに、ターミナルに URL を出力します。このように、ブラウザーの&#x200B;**匿名**&#x200B;ウィンドウでコピーして開くことができます。この方法では、通常のブラウザーウィンドウで現在ログインしているセッションはそのまま残り、コンテキストに必要な特定のログインと組織を使用できます。

   最初のコマンドでは、ローカルの .`.aio` 設定ファイルに、`mycontext` という新しいログインコンテキスト設定を作成します（ファイルは必要に応じて作成されます）。2 番目のコマンドでは、コンテキスト `mycontext` を「現在」のコンテキスト（デフォルト）に設定します。

   この設定を行うと、ログインコマンドではログイントークンをコンテキスト `mycontext` に自動的に保存し、ローカルに保持します。

   ローカル設定を複数のフォルダーに保存することで、複数のコンテキストを管理できます。または、1 つの設定ファイル内に複数のコンテキストを設定し、「現在」のコンテキストを変更することで切り替えることもできます。
   </details>

1. ご自分の組織、プログラムおよび環境を使用するように RDE プラグインを設定します。以下の setup コマンドでは、組織内のプログラムのリストをインタラクティブにユーザーに提示し、そのプログラム内の選択可能な RDE 環境を表示します。

   ```
   aio aem:rde:setup
   ```

   スクリプト環境を使用する場合は、このセットアップ手順をスキップしても構いません。その場合は、組織、プログラムおよび環境の値を各コマンドに含めることができます。[詳しくは、以下の RDE コマンドを参照してください。](#rde-cli-commands)

### インタラクティブセットアップ {#installing-the-rde-command-line-tools-interactive}

setup コマンドは、指定された設定をローカルに保存するかグローバルに保存するかを尋ねます。

```
Setup the CLI configuration necessary to use the RDE commands.
? Do you want to store the information you enter in this setup procedure locally? (y/N)
```

`no` を選択すると、
* お使いの aio 設定に組織、プログラムおよび環境がグローバルに保存されます。
* 単一の RDE のみを操作できます。

`yes` を選択すると、
* 現在のディレクトリ内の `.aio` ファイルに組織、プログラムおよび環境がローカルに保存されます。これは、ファイルをバージョン管理にコミットして、Git リポジトリをクローンする他のユーザーが使用できるようにする場合に便利です。
* 多数の RDE を操作できるので、別のディレクトリに切り替えると、その設定が代わりに使用されます。
* スクリプトのようなプログラムのコンテキストで設定を使用し、参照できます。


ローカル設定またはグローバル設定を選択すると、setup コマンドは現在のログインから組織 ID を読み取り、次に組織のプログラムを読み取ります。組織が見つからない場合は、ガイダンスに従って手動で入力できます。

```
Selected only organization: XYXYXYXYXYXYXYXXYY
retrieving programs of your organization ...
```

プログラムを取得後、ユーザーはリストから選択したり、入力してフィルタリングしたりできます。
プログラムを選択すると、選択可能な RDE 環境のリストが表示されます。
使用可能なプログラムや RDE 環境が 1 つしかない場合は、そのプログラムが自動的に選択されます。

現在の環境コンテキストを確認するには、次のコマンドを実行します。

```aio aem rde setup --show```

コマンドは、次のような結果を返します。

```Current configuration: cm-p1-e1: programName - environmentName (organization: ...@AdobeOrg)```

### 非インタラクティブ環境での手動設定手順 {#manual-setup}

上記のように、ユーザーがインタラクティブに setup コマンドを実行できない環境（CI/CD やスクリプトなど）では、組織、プログラム、環境の 3 つのパラメーターを次の手順に従って手動で設定できます。


<details>
  <summary>展開すると、手動での設定方法の詳細が表示されます</summary>

1. 組織 ID を設定し、英数字の文字列を独自の組織 ID に置き換えます。

   `aio config:set cloudmanager_orgid 4E03EQC05D34GL1A0B49421C@AdobeOrg`

   * 独自の組織 ID は、[組織 ID の表示](https://experienceleague.adobe.com/docs/core-services/interface/administration/organizations.html?lang=ja#concept_EA8AEE5B02CF46ACBDAD6A8508646255)に記載されている方法を使用して検索できます。

1. 次に、以下のプログラム ID を設定します。

   `aio config:set cloudmanager_programid 12345`

1. 次に、RDE がアタッチされる以下の環境 ID を設定します。

   `aio config:set cloudmanager_environmentid 123456`

1. プラグインの設定が完了したら、次の操作を実行してログインします。

   `aio login`

   この手順では、Cloud Manager **デベロッパー - Cloud Service** 製品プロファイルのメンバーである必要があります。詳しくは、[Cloud Manager 製品プロファイルへのチームメンバーの割り当て - 開発者製品プロファイルの割り当て](/help/journey-onboarding/assign-profiles-cloud-manager.md#assign-developer)を参照してください。

詳細とデモンストレーションについては、[RDE の設定方法（06:24）](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/developing/rde/how-to-setup.html?lang=ja)のビデオチュートリアルを参照してください。
</details>

## 新機能の開発時の RDE の使用 {#using-rde-while-developing-a-new-feature}

アドビでは、新しい機能を開発する際に、次のワークフローを使用することをお勧めします。

* 中間マイルストーンに達し、AEM as a Cloud Service SDK を使用してローカルで正常に検証されたら、コードを Git 機能ブランチにコミットします。ブランチは、Git へのコミットはオプションですが、まだメインラインに含めてはいけません。「中間マイルストーン」を構成するものは、チームの習慣に応じて異なります。例えば、数行の新しいコードや、半日の作業、サブ機能の完了といったものがあります。

* RDE が別の機能で使用されていて、[デフォルトの状態にリセット](#reset-rde)したい場合は、RDE をリセットします。<!-- Alexandru: hiding for now, do not delete This can be done by way of [Cloud Manager](#reset-the-rde-cloud-manager) or by way of the [command line](#reset-the-rde-command-line). -->リセットには数分かかり、既存のコンテンツおよびコードはすべて削除されます。RDE ステータスコマンドを使用すると、RDE の準備が完了したことを確認できます。RDE は、最新の AEM リリースバージョンで復活します。

  >[!IMPORTANT]
  >
  > ステージング環境と実稼動環境が AEM リリースの自動更新を受信しておらず、最新の AEM リリースバージョンから遅れている場合は、RDE で実行されているコードが、ステージング環境と実稼動環境でのコードの機能と一致しない可能性があります。その場合、実稼動環境にデプロイする前に、ステージングでコードのテストを徹底的に実行することが特に重要です。


* RDE コマンドラインインターフェイスを使用して、ローカルコードを RDE に同期します。 オプションには、コンテンツパッケージ、特定のバンドル、OSGi 設定ファイル、コンテンツファイル、Apache／Dispatcher 設定の zip ファイルのインストールが含まれます。 リモートコンテンツパッケージの参照も可能です。 詳しくは、[RDE コマンドラインツール](/help/implementing/developing/introduction/rapid-development-environments.md#rde-cli-commands)を参照してください。ステータスコマンドを使用すると、デプロイメントが成功したことを検証できます。必要に応じて、パッケージマネージャーを使用してコンテンツパッケージをインストールします。

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

### グローバルフラグ {#global-flags}

* 詳細度の低い出力には、quiet フラグを使用します。

  `aio aem rde <command> --quiet`

  この場合は、スピナーやプログレスバーなどの特定の要素が削除され、ユーザー入力の必要性が制限されます。

* JSON に対しては、コンソールログ出力の代わりに、json フラグを使用します。

  `aio aem rde <command> --json`

  この場合は、コンソール出力を抑制しながら、有効な JSON を返します。詳しくは、以下の JSON の例を参照してください。

* setup コマンドを使用した RDE 接続情報の設定や aio 設定の作成を避けるには、組織、プログラム、環境の 3 つのフラグを使用します。

  `aio aem rde <command> --organizationId=<value> --programId=<value> --environmentId=<value>`

  この場合もやはり、```aio login``` を実行する必要があります。

### RDE へのデプロイ {#deploying-to-rde}

この節では、RDE CLI を使用して、バンドル、OSGi 設定、コンテンツパッケージ、個々のコンテンツファイル、Apache または Dispatcher 設定のデプロイ、インストールまたは更新する方法について説明します。

一般的な使用パターンは `aio aem:rde:install <artifact>` です。

以下に例をいくつか示します。

#### コンテンツパッケージのデプロイ {#deploy-content-package}

`aio aem:rde:install sample.demo.ui.apps.all-1.0.0-SNAPSHOT.zip`

デプロイメントが成功した場合の応答は、次のようになります。

```
...
#1: deploy completed for content-package sample.demo.ui.apps.all-1.0.0-SNAPSHOT.zip on author,publish - done by 9E072FC75D54FE1A2B49431C@AdobeID at 2022-09-13T11:32:06.229Z
```

オプションで、リモートリポジトリを参照できます。

`aio aem:rde:install -t content-package "https://repo1.maven.org/maven2/com/adobe/aem/guides/aem-guides-wknd.all/2.1.0/aem-guides-wknd.all-2.1.0.zip"`

デフォルトでは、アーティファクトはオーサー層とパブリッシュ層の両方にデプロイされますが、「-s」フラグを使用して特定の層をターゲットにすることができます。

コードやコンテンツを含むパッケージ、[コンテナパッケージ](/help/implementing/developing/introduction/aem-project-content-package-structure.md#container-packages)（「all」パッケージとも呼ばれる）など、どの AEM パッケージもデプロイ可能です。

>[!IMPORTANT]
>
>WKND プロジェクトの Dispatcher 設定は、上記のコンテンツパッケージのインストールではデプロイされません。「Apache／Dispatcher 設定のデプロイ」の手順に従って、別途デプロイします。

#### OSGi 設定のデプロイ {#deploy-OSGI-config}

`aio aem:rde:install com.adobe.granite.demo.MyServlet.cfg.json`

デプロイメントが成功した場合の応答は、次のようになります。

```
...
#2: deploy completed for osgi-config com.adobe.granite.demo.MyServlet.cfg.json on author,publish - done by 9E0725C05D54FE1A0B49431C@AdobeID at 2022-09-13T11:54:36.390Z
```

#### バンドルのデプロイ {#deploy-bundle}

バンドルをデプロイするには、次を使用します。

`aio aem:rde:install ~/.m2/repository/org/apache/felix/org.apache.felix.gogo.jline/1.1.8/org.apache.felix.gogo.jline-1.1.8.jar`

デプロイメントが成功した場合の応答は、次のようになります。

```
...
#3: deploy staged for osgi-bundle org.apache.felix.gogo.jline-1.1.8.jar on author,publish - done by 9E0725C05D53BE1A0B49431C@AdobeID at 2022-09-14T07:54:28.882Z
```

#### コンテンツファイルのデプロイ {#deploy-content-file}

コンテンツファイルをデプロイするには、次を使用します。

`aio aem:rde:install world.txt -p /apps/hello.txt`

デプロイメントが成功した場合の応答は、次のようになります。

```
..
#4: deploy completed for content-file world.txt on author,publish - done by 9E0729C05C54FE1A0B49431C@AdobeID at 2022-09-14T07:49:30.644Z
```

#### Apache／Dispatcher 設定のデプロイ {#deploy-apache-config}

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
>RDE は、「フレキシブルモード」の Dispatcher 設定をサポートしていますが、「レガシーモード」の Dispatcher 設定はサポートしていません。2 つのモードについて詳しくは、[Dispatcher ドキュメント](/help/implementing/dispatcher/disp-overview.md#validation-debug)を参照してください。また、[フレキシブルモードへの移行](/help/implementing/dispatcher/validation-debug.md#migrating)に関するドキュメントをまだ確認していない場合は、そちらも参照してください。

デプロイメントが成功すると、次のような応答が生成されます。

```
..
#5 deploy completed for dispatcher-config dispatcher.zip on author,publish - done by 9E0735C05T54FE1A0B49431C@AdobeID at 2022-10-03T10:26:31.286Z
Logs:
  Cloud manager validator 2.0.49
  2022/10/03 10:26:37 No issues found
  Syntax OK
```

RDE にデプロイされたコードには、Cloud Manager パイプラインとそれに関連する品質ゲートは適用されません。ただし、次のコードサンプルのように、コードは分析を経て、エラーを報告します。

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

上記のコード例は、バンドルが解決されない場合の動作を示しています。この場合、バンドルは「ステージング済み」で、他のコードのインストールを通じて要件（この場合、読み込み不足）が満たされた場合にのみインストールされます。

#### 設定パイプラインに関連する設定のデプロイ（yaml 設定） {#deploy-config-pipeline}

[設定パイプラインの使用](/help/operations/config-pipeline.md)の記事の説明に従って、環境固有の設定（1 つ以上の yaml ファイル）は、次のようにデプロイできます。

`aio aem:rde:install -t env-config ./my-config-folder`
ここで、my-config-folder は yaml 設定を含む親フォルダーです。

または、config フォルダーツリーを含む zip ファイルをインストールすることもできます。

`aio aem:rde:install -t env-config config.zip`

次の例に示すように、yaml ファイルの envTypes 配列には、値 *rde* を含める必要があります。

```
kind: "CDN"
version: "1"
metadata:
  envTypes: ["rde"]
```

### サイトテーマとサイトテンプレートに基づくフロントエンドコードのデプロイ {#deploying-themes-to-rde}

RDE は、[サイトテーマ](/help/sites-cloud/administering/site-creation/site-themes.md)および[サイトテンプレート](/help/sites-cloud/administering/site-creation/site-templates.md)に基づいてフロントエンドコードをサポートします。RDE を使用する場合、これは、他の環境タイプに使用される Cloud Manager [フロントエンドパイプライン](/help/sites-cloud/administering/site-creation/enable-front-end-pipeline.md)ではなく、コマンドラインのディレクティブを使用してフロンエンドパッケージをデプロイします。

通常どおり、npm を使用してフロントエンドパッケージを構築します。

`npm run build`

`dist/` フォルダーが生成され、フロントエンドパッケージフォルダーには、`package.json` ファイルと `dist` フォルダーが含められます。

```
ls ./path-to-frontend-pkg-folder/
...
dist
package.json
```
これで、フロントエンドパッケージフォルダーを指すことで、RDE にフロントエンドパッケージをデプロイする準備が整いました。

```
aio aem:rde:install -t frontend ./path-to-frontend-pkg-folder/
...
#1: deploy completed for frontend frontend-pipeline.zip on author,publish - done by ... at 2024-01-18T15:33:22.898Z
Logs:
> Deployed artifact wknd-1.0.0-1705592008-26e7ec1a
> with workspace hash 692021864642a20d6d298044a927d66c0d9cf2adf42d4cca0c800a378ac3f8d3
```

または、zip 形式で `package.json` ファイルと `dist` フォルダーを保存し、その zip ファイルをデプロイします。

`zip -r frontend-pkg.zip ./path-to-frontend-pkg-folder/dist ./path-to-frontend-pkg-folder/package.json`

```
aio aem:rde:install -t frontend frontend-pkg.zip
...
#1: deploy completed for frontend frontend-pipeline.zip on author,publish - done by ... at 2024-01-18T15:33:22.898Z
Logs:
> Deployed artifact wknd-1.0.0-1705592008-26e7ec1a
> with workspace hash 692021864642a20d6d298044a927d66c0d9cf2adf42d4cca0c800a378ac3f8d3
```

>[!NOTE]
>
>フロントエンドパッケージのファイルの命名は、次の命名規則に従う必要があります。
> * npm ビルド出力パッケージフォルダー用の「dist」フォルダー
> * npm 依存関係パッケージ用の「package.json」ファイル

>[!TIP]
>
> 2023年4月以前に RDE を作成し、フロントエンド機能を初めて試した際に「UNEXPECTED_API_ERROR」エラーが発生した場合は、環境を削除して再度作成してください。

### RDE のステータス確認 {#checking-rde-status}

RDE CLI を使用すると、RDE プラグインを使用して実行されたデプロイメントなど、環境にデプロイする準備が整っているかどうかを確認できます。

次のコードを実行すると、

`aio aem:rde:status`

次を返します。

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

CLI ツールを使用すると、RDE に以前にデプロイされた設定やバンドルを削除できます。`status` コマンドを使用して、削除可能な項目のリストを取得できます。これには、DELETE コマンドで参照するバンドル用の `bsn` と設定用の `pid` が含まれます。

例えば、`com.adobe.granite.demo.MyServlet.cfg.json` がインストールされている場合、`bsn` は `com.adobe.granite.demo.MyServlet` のみ（**cfg.json** サフィックスなし）になります。

コンテンツパッケージまたはコンテンツファイルは削除対象外です。 削除するには、RDE をリセットする必要があります。これにより、デフォルトの状態に戻ります。

詳しくは、以下の例を参照してください。

```
aio aem:rde:delete com.adobe.granite.csrf.impl.CSRFFilter
#13: delete completed for osgi-config com.adobe.granite.csrf.impl.CSRFFilter on author - done by karl at 2022-09-12T22:01:01.955Z
#14: delete completed for osgi-config com.adobe.granite.csrf.impl.CSRFFilter on publish - done by karl at 2022-09-12T22:01:12.979Z
```

詳細とデモンストレーションについては、[RDE コマンドの使用方法（10:01）](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/developing/rde/how-to-use.html?lang=ja)のビデオチュートリアルを参照してください。

## ログ {#rde-logging}

他の環境タイプと同様に、ログレベルは OSGi 設定を変更することで設定できますが、上記のように、RDE のデプロイメントモデルには Cloud Manager のデプロイメントではなくコマンドラインが含まれます。ログの表示、ダウンロード、解釈の方法について詳しくは、[ログに関するドキュメント](/help/implementing/developing/introduction/logging.md)を確認してください。

また、RDE CLI には独自の log コマンドもあり、これを使用して、クラスとパッケージをログレベルでログに記録する方法をすばやく設定できます。これらの設定は、バージョン管理の OSGI プロパティを変更しないので、一時的なものと見なすことができます。この機能は、遠い過去のログを検索するのではなく、リアルタイムでログを追跡することに焦点を当てています。

次の例では、1 つのパッケージをデバッグログレベルに設定し、2 つのパッケージ（スペースで区切る）を情報デバッグレベルに設定して、オーサー層を末尾まで追跡する方法を示します。**認証**&#x200B;パッケージを含む出力がハイライト表示されます。

`aio aem:rde:logs --target=author --debug=org.apache.sling --info=org.apache.sling.commons.threads.impl org.apache.sling.jcr.resource.internal.helper.jcr -H .auth.`

>[!TIP]
>
>オーサーサービスのログコマンドの実行中にエラー `RDECLI:UNEXPECTED_API_ERROR` が表示される場合は、環境をリセットして再試行してください。最新のリセット操作が 2024年5月末より前であった場合、このエラーがスローされます。
>
>```
>aio aem:rde:reset
>```

コマンドラインオプションの完全なセットについては、`aio aem:rde:logs --help` を参照してください。

次のような機能があります。

* パッケージまたはクラスレベルごとのログレベルの宣言
* ログ出力形式のカスタマイズ
* 独自のターミナルにおいてそれぞれ最大 4 つの現在のログ設定を追跡
* 特定のログをハイライト表示

ログは RDE のメモリに保存され、これらのログはリサイクルされるので、末尾が追跡されない場合やネットワークが遅すぎる場合は破棄されます。


## リセット {#reset-rde}

RDE をリセットすると、すべてのカスタムコード、設定およびコンテンツが、オーサーインスタンスとパブリッシュインスタンスの両方から削除されます。このリセットは、例えば、RDE を使用して特定の機能をテストしていて、別の機能をテストするためにデフォルトの状態にリセットする場合に便利です。

リセットすると、RDE が使用可能な最新の AEM バージョンに設定されます。

リセットは、[Cloud Manager](#reset-the-rde-cloud-manager) または [ コマンドライン ](#reset-the-rde-command-line) を使用して行うことができます。 リセットには数分かかり、既存のコンテンツとコードはすべて RDE から削除されます。

>[注意!]
>
>リセット機能を使用するには、Cloud Manager開発者の役割が割り当てられている必要があります。 そうでない場合、リセットアクションはエラーになります。

### コマンドラインを使用した RDE のリセット {#reset-the-rde-command-line}

RDE をリセットし、次のコマンドを実行してデフォルトの状態に戻すことができます。

`aio aem:rde:reset`

この処理には通常数分かかり、処理が成功した場合は ```Environment reset.``` に、エラーが発生した場合は ```Failed to reset the environment.``` に報告されます。 構造化された出力については、以下の出力に関する章 ```--json``` 参照してください。

[status コマンド ](#checking-rde-status) を使用して、環境の準備が再び整ったことを確認します。

### Cloud Managerでの RDE のリセット {#reset-the-rde-cloud-manager}

次の手順に従って、Cloud Manager を使用して RDE をリセットできます。

1. [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) で Cloud Manager にログインし、適切な組織を選択します。

1. RDE をリセットするプログラムをクリックします。

1. **概要**&#x200B;ページで、画面上部の「**環境**」タブをクリックします。

   ![「環境」タブ](/help/implementing/cloud-manager/assets/environments-tab2.png)

   * または、**環境**&#x200B;カードの「**すべて表示**」ボタンをクリックして、「**環境**」タブに直接ジャンプします。

     ![「すべて表示」オプション](/help/implementing/cloud-manager/assets/environment-showall.png)

1. **環境**&#x200B;ウィンドウが開いて、プログラムのすべての環境が一覧表示されます。

   ![「環境」タブ](/help/implementing/cloud-manager/assets/environments-tab-populated.png)

1. リセットする RDE の省略記号ボタンをクリックし、「**リセット**」を選択します。

   ![環境の詳細を表示](/help/implementing/cloud-manager/assets/rde-reset.png)

1. ダイアログで「**リセット**」をクリックして、RDE をリセットすることを確認します。

   ![リセットの確認](/help/implementing/cloud-manager/assets/rde-reset-confirm.png)

1. Cloud Manager はバナー通知で、リセットプロセスが開始したことを確認します。

   ![バナー通知をリセット](/help/implementing/cloud-manager/assets/rde-reset-banner.png)

RDE のリセットプロセスが開始されると、通常、プロセスが完了して環境がデフォルトの状態に戻るまでに数分かかります。リセットプロセスのステータスは、**環境**&#x200B;カードの&#x200B;**ステータス**&#x200B;列、または&#x200B;**環境**&#x200B;ウィンドウでいつでも確認できます。

![RDE リセットステータス](/help/implementing/cloud-manager/assets/rde-reset-status-environments-card.png)

**概要**&#x200B;ページの&#x200B;**環境**&#x200B;カードから直接「...」ボタンを使用して、RDE をリセットすることもできます。

![環境カードからの RDE のリセット](/help/implementing/cloud-manager/assets/rde-reset-environments-card.png)

Cloud Manager を使用した環境の管理方法について詳しくは、[Cloud Manager のドキュメント](/help/implementing/cloud-manager/manage-environments.md)を参照してください。

## JSON 出力をサポートするコマンド {#json-commands}

ほとんどのコマンドでは、コンソール出力を抑制し、スクリプトで処理される有効な JSON を返すグローバル ```--json``` フラグをサポートします。サポートされるコマンドと、JSON 出力の例を以下に示します。

### ステータス {#status}

<details>
  <summary>展開してステータスの例を表示</summary>

#### クリーンな RDE {#clean-rde}

```$ aio aem rde status --json```

```json
{
  "programId": "myProgram",
  "environmentId": "myEnv",
  "status": "Modification in progress | Deployment in progress | Upload in progress | Ready (instances are currently deploying) | Ready",
  "author": {
    "osgiBundles": [],
    "osgiConfigs": []
  },
  "publish": {
    "osgiBundles": [],
    "osgiConfigs": []
  }
}
```

#### いくつかのバンドルがインストールされた RDE {#rde-installed-bundles}

```$ aio aem rde status --json```

```json
{
  "programId": "myProgram",
  "environmentId": "myEnv",
  "status": "Ready",
  "author": {
    "osgiBundles": [
      {
        "id": "author_osgi-bundle_com.adobe.granite.hotdev.demo",
        "updateId": "80",
        "service": "author",
        "type": "osgi-bundle",
        "metadata": {
          "name": "hotdev.demo.ui.apps.all-1.0.0-SNAPSHOT.zip",
          "bundleSymbolicName": "com.adobe.granite.hotdev.demo",
          "bundleName": "HotDev Bundle",
          "bundleVersion": "1.0.0.SNAPSHOT"
        }
      }
    ],
    "osgiConfigs": [
      {
        "id": "publish_osgi-config_com.adobe.granite.demo.MyServlet",
        "updateId": "80",
        "service": "publish",
        "type": "osgi-config",
        "metadata": {
          "name": "hotdev.demo.ui.apps.all-1.0.0-SNAPSHOT.zip",
          "configPid": "com.adobe.granite.demo.MyServlet"
        }
      }
    ]
  },
  "publish": {
    "osgiBundles": [
      {
        "id": "author_osgi-bundle_com.adobe.granite.hotdev.demo",
        "updateId": "80",
        "service": "author",
        "type": "osgi-bundle",
        "metadata": {
          "name": "hotdev.demo.ui.apps.all-1.0.0-SNAPSHOT.zip",
          "bundleSymbolicName": "com.adobe.granite.hotdev.demo",
          "bundleName": "HotDev Bundle",
          "bundleVersion": "1.0.0.SNAPSHOT"
        }
      }
    ],
    "osgiConfigs": [
      {
        "id": "publish_osgi-config_com.adobe.granite.demo.MyServlet",
        "updateId": "80",
        "service": "publish",
        "type": "osgi-config",
        "metadata": {
          "name": "hotdev.demo.ui.apps.all-1.0.0-SNAPSHOT.zip",
          "configPid": "com.adobe.granite.demo.MyServlet"
        }
      }
    ]
  }
}
```

</details>

### インストール {#install}

<details>
  <summary>展開してインストールの例を表示</summary>

```$ aio aem rde install ~/Downloads/hotdev.demo.ui.apps.all-1.0.0-SNAPSHOT.zip --json```

```json
{
  "programId": "myProgram",
  "environmentId": "myEnv",
  "items": [
    {
      "updateId": "4",
      "info": "deploy",
      "action": "deploy",
      "metadata": {
        "name": "hotdev.demo.ui.apps.all-1.0.0-SNAPSHOT.zip"
      },
      "services": [
        "author",
        "publish"
      ],
      "status": "completed",
      "timestamps": {
        "received": "2024-05-21T12:30:44.578Z",
        "processed": "2024-05-21T12:31:07.886468Z"
      },
      "user": "userId",
      "type": "content-package",
      "hash": "2ad73507",
      "logs": [
        "No logs available for this update."
      ]
    }
  ]
}
```

</details>

### 削除 {#delete}

<details>
  <summary>展開して削除の例を表示</summary>

```$ aio aem rde delete com.adobe.granite.hotdev.demo-1.0.0.SNAPSHOT --json```

```json
{
  "programId": "myProgram",
  "environmentId": "myEnv",
  "items": [
    {
      "updateId": "84",
      "info": "delete author_osgi-bundle_com.adobe.granite.hotdev.demo",
      "action": "delete",
      "metadata": {},
      "services": [
        "author"
      ],
      "status": "completed",
      "timestamps": {
        "received": "2024-05-21T11:49:16.889Z",
        "processed": "2024-05-21T11:49:18.188420Z"
      },
      "user": "userId",
      "type": "osgi-bundle",
      "deletedArtifact": {
        "id": "author_osgi-bundle_com.adobe.granite.hotdev.demo",
        "metadata": {
          "name": "hotdev.demo.ui.apps.all-1.0.0-SNAPSHOT.zip",
          "bundleSymbolicName": "com.adobe.granite.hotdev.demo",
          "bundleName": "HotDev Bundle",
          "bundleVersion": "1.0.0.SNAPSHOT"
        },
        "service": "author",
        "type": "osgi-bundle",
        "updateId": "83"
      },
      "hash": "636f6d2e",
      "logs": [
        "No logs available for this update."
      ]
    },
    {
      "updateId": "85",
      "info": "delete publish_osgi-bundle_com.adobe.granite.hotdev.demo",
      "action": "delete",
      "metadata": {},
      "services": [
        "publish"
      ],
      "status": "completed",
      "timestamps": {
        "received": "2024-05-21T11:49:23.857Z",
        "processed": "2024-05-21T11:49:25.237930Z"
      },
      "user": "userId",
      "type": "osgi-bundle",
      "deletedArtifact": {
        "id": "publish_osgi-bundle_com.adobe.granite.hotdev.demo",
        "metadata": {
          "name": "hotdev.demo.ui.apps.all-1.0.0-SNAPSHOT.zip",
          "bundleSymbolicName": "com.adobe.granite.hotdev.demo",
          "bundleName": "HotDev Bundle",
          "bundleVersion": "1.0.0.SNAPSHOT"
        },
        "service": "publish",
        "type": "osgi-bundle",
        "updateId": "83"
      },
      "hash": "636f6d2e",
      "logs": [
        "No logs available for this update."
      ]
    }
  ]
}
```

</details>

### 履歴 {#history}

<details>
  <summary>展開して履歴の例を表示</summary>

```$ aio aem rde history --json```

```json
{
  "programId": "myProgram",
  "environmentId": "myEnv",
  "status": "Ready",
  "items": [
    {
      "updateId": "112",
      "info": "delete publish_osgi-bundle_com.adobe.granite.hotdev.demo",
      "action": "delete",
      "metadata": {},
      "services": [
        "publish"
      ],
      "status": "completed",
      "timestamps": {
        "received": "2024-05-21T12:53:07.934Z",
        "processed": "2024-05-21T12:53:09.118766Z"
      },
      "user": "userId",
      "type": "osgi-bundle",
      "deletedArtifact": {
        "id": "publish_osgi-bundle_com.adobe.granite.hotdev.demo",
        "metadata": {
          "name": "hotdev.demo.ui.apps.all-1.0.0-SNAPSHOT.zip",
          "bundleSymbolicName": "com.adobe.granite.hotdev.demo",
          "bundleName": "HotDev Bundle",
          "bundleVersion": "1.0.0.SNAPSHOT"
        },
        "service": "publish",
        "type": "osgi-bundle",
        "updateId": "110"
      },
      "hash": "636f6d2e"
    },
    {
      "updateId": "111",
      "info": "delete author_osgi-bundle_com.adobe.granite.hotdev.demo",
      "action": "delete",
      "metadata": {},
      "services": [
        "author"
      ],
      "status": "completed",
      "timestamps": {
        "received": "2024-05-21T12:53:00.824Z",
        "processed": "2024-05-21T12:53:02.101560Z"
      },
      "user": "userId",
      "type": "osgi-bundle",
      "deletedArtifact": {
        "id": "author_osgi-bundle_com.adobe.granite.hotdev.demo",
        "metadata": {
          "name": "hotdev.demo.ui.apps.all-1.0.0-SNAPSHOT.zip",
          "bundleSymbolicName": "com.adobe.granite.hotdev.demo",
          "bundleName": "HotDev Bundle",
          "bundleVersion": "1.0.0.SNAPSHOT"
        },
        "service": "author",
        "type": "osgi-bundle",
        "updateId": "110"
      },
      "hash": "636f6d2e"
    },
    {
      "updateId": "110",
      "info": "deploy",
      "action": "deploy",
      "metadata": {
        "name": "hotdev.demo.ui.apps.all-1.0.0-SNAPSHOT.zip"
      },
      "services": [
        "author",
        "publish"
      ],
      "status": "completed",
      "timestamps": {
        "received": "2024-05-21T12:52:12.123Z",
        "processed": "2024-05-21T12:52:31.026147Z"
      },
      "user": "userId",
      "type": "content-package",
      "hash": "2ad73507"
    }
  ]
}
```

</details>

### リセット {#reset}

<details>
  <summary>展開してリセットの例を表示</summary>

#### ファイアアンドフォーゲット、待機不要 {#fire-no-wait}

```$ aio aem rde reset --no-wait --json```

```json
{
  "programId": "myProgram",
  "environmentId": "myEnv",
  "status": "resetting"
}
```

#### 完了するまで待ち、正常にリセットします {#wait-success}

```$ aio aem rde reset --json```

```json
{
  "programId": "myProgram",
  "environmentId": "myEnv",
  "status": "reset"
}
```

#### 完了まで待機、リセットに失敗しました {#wait-failed}

```$ aio aem rde reset --json```

```json
{
  "programId": "myProgram",
  "environmentId": "myEnv",
  "status": "reset_failed"
}
```

</details>

### やり直し {#restart}

<details>
  <summary>展開して再起動の例を表示</summary>

```$ aio aem rde restart --json```

```json
{
  "programId": "myProgram",
  "environmentId": "myEnv",
  "status": "restarted"
}
```

</details>

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

1. [コンテンツコピーツール](/help/implementing/developing/tools/content-copy.md)を使用して、実稼動環境、ステージング環境、開発環境、または別の RDE から定義済みのコンテンツセットをコピーします。

1. パッケージマネージャーを使用

コンテンツパッケージを同期する場合は、1 GB までに制限されます。


## RDE とクラウド開発環境の違いは何ですか？ {#how-are-rds-different-from-cloud-development-environments}

RDE は多くの点でクラウド開発環境に似ていますが、コードを素早く同期できるように、アーキテクチャ上の小さな違いが若干あります。コードを RDE に取得するメカニズムは異なります。RDE の場合はローカル開発環境からコードを同期しますが、クラウド開発環境の場合は Cloud Manager を使用してコードをデプロイします。

このような理由から、RDE 環境でコードを検証した後、実稼動以外のパイプラインを使用してコードをクラウド開発環境にデプロイすることをお勧めします。最後に、実稼動パイプラインでデプロイする前に、コードをテストします。

また、次の考慮事項にも注意してください。

* RDE にプレビュー層は含まれない
* RDE は現在、プレリリースチャネルをサポートしていません。


## 必要な RDE の数 {#how-many-rds-do-i-need}

RDE は、ライセンスが付与されている各ソリューションで使用でき、Adobeでは追加の RDE も提供されます。RDE は実稼動（サンドボックス以外）プログラム用としてライセンス登録できます。

必要な RDE の数は、組織の構成とプロセスによって異なります。最も柔軟なモデルでは、組織が AEM Cloud Service の各デベロッパーに対して専用の RDE を購入できます。各デベロッパーはこのモデルで、RDE 環境が使用可能かどうかに関して他のチームメンバーと調整することなく、RDE でコードをテストできます。

もう 1 つの極端な例としては、1 つの RDE を持つチームが内部プロセスを使用して、特定の時間にどのデベロッパーが環境を使用できるかを調整する場合があります。これは、デベロッパーが中間機能のマイルストーンに達し、必要な変更をすばやく行えるクラウド環境で検証の準備を整えていることが条件となります。

中間モデルとは、組織がいくつかの RDE を購入する場合に、未使用の RDE が使用可能になる可能性が高くなるモデルです。1 つの戦略は、スクラムチームまたは主要機能ごとに RDE を割り当てることです。内部プロセスを使用して、環境の使用状況を調整できます。

## AEM FormsCloud Service の迅速な開発環境（RDE）は他の環境とどのように異なりますか？ {#how-are-forms-rds-different-from-cloud-development-environments}

Forms のデベロッパーは、AEM FormsCloud Service の迅速な開発環境を使用して、アダプティブフォーム、ワークフロー、およびコアコンポーネントのカスタマイズ、サードパーティシステムとの統合などのカスタマイズを迅速に開発できます。AEM Forms Cloud Service の迅速な開発環境（RDE）は、通信 API をサポートしていません。また、アダプティブフォームの送信時にレコードのドキュメントを生成するなど、レコードのドキュメントを必要とする機能もサポートされていません。以下に示す AEM Forms の機能は、迅速な開発環境（RDE）では使用できません。

* アダプティブフォーム用のレコードのドキュメントの設定
* アダプティブフォームの送信時またはワークフローステップでのレコードのドキュメントの生成
* レコードのドキュメントをメール送信アクションまたはワークフローのメールステップで添付ファイルとして送信
* アダプティブフォームまたはワークフローステップでの Adobe Sign の使用
* 通信 API

>[!NOTE]
>
> 迅速な開発環境（RDE）の UI と Forms 向けの他の Cloud Service 環境の UI に違いはありません。アダプティブフォームのレコードテンプレートのドキュメントの選択など、オプション関連のレコードのすべてのドキュメントは UI に引き続き表示されます。これらの環境には、こうしたオプションをテストするためのレコードのドキュメント機能や通信 API がありません。そのため、通信 API またはレコードのドキュメント機能を必要とするオプションを選択した場合、アクションは実行されず、エラーメッセージが表示されます。

## RDE に関するチュートリアル

AEM as a Cloud Service での RDE について詳しくは、[設定方法、使用方法、開発ライフサイクル](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/developing/rde/overview.html?lang=ja)に関するビデオチュートリアル（01:25）を参照してください。

# トラブルシューティング {#troubleshooting}

## RDE のトラブルシューティング（#rde-troubleshooting）

### 既存の RDE に対する最新の AEM バージョンを取得する方法 {#get-latest-aem-version}

作成時に、RDE は使用可能な最新の Adobe Experience Manager（AEM）バージョンに設定されます。Cloud Manager または `aio aem:rde:reset` コマンドを使用して実行できる [RDE のリセット](#reset-rde)は、RDE を循環させ、使用可能な最新の AEM バージョンに設定します。

## aio RDE プラグインのトラブルシューティング {#aio-rde-plugin-troubleshooting}

### 不十分な権限に関するエラー {#insufficient-permissions}

RDE プラグインを使用するには、Cloud Manager **開発者 - Cloud Service** 製品プロファイルのメンバーである必要があります。詳しくは、[Cloud Manager 製品プロファイルへのチームメンバーの割り当て - 開発者製品プロファイルの割り当て](/help/journey-onboarding/assign-profiles-cloud-manager.md#assign-developer)を参照してください。

また、このデベロッパーの役割を持っていることを、以下のコマンドを実行して Developer Console にログインすることでも確認できます。

`aio cloudmanager:environment:open-developer-console`

>[!TIP]
>
>`Warning: cloudmanager:* is not a aio command.` エラーが表示された場合は、以下のコマンドを実行して [aio-cli-plugin-cloudmanager](https://github.com/adobe/aio-cli-plugin-cloudmanager) をインストールする必要があります。
>
>```
>aio plugins:install @adobe/aio-cli-plugin-cloudmanager
>```

以下を実行して、ログインが正常に完了したことを確認します

`aio cloudmanager:list-programs`

これにより、設定した組織の下にあるすべてのプログラムがリストされ、正しい役割が割り当てられていることを確認できます。

### 廃止されたコンテキスト「aio-cli-plugin-cloudmanager」の使用 {#aio-rde-plugin-troubleshooting-deprecatedcontext}

「aio-cli-plugin-aem-rde」の履歴により、コンテキスト名「aio-cli-plugin-cloudmanager」がしばらくの間使用されていました。rde プラグインは、コンテキスト情報の処理に IMS 方式を使用するようになりました。つまり、コンテキスト情報をグローバルまたはローカルに保存するオプションがあり、必要に応じてすべての aio 呼び出しを設定済みのデフォルトにデフォルト設定することもできます。設定済みのデフォルトのコンテキストはローカルに保存され、開発者はフォルダー内の個々のコンテキストとその情報を追跡および使用できます。詳しくは、上記の[ローカルコンテキストの設定例](/help/implementing/developing/introduction/rapid-development-environments.md#installing-the-rde-command-line-tools)を参照してください。

aio-cli-plugin-cloudmanager と aio-cli-plugin-aem-rde の両方のプラグインを使用し、すべての情報を同じコンテキストに保持する開発者は、現時点で次のオプションを選択する必要があります。

#### コンテキスト「aio-cli-plugin-cloudmanager」を引き続き使用

コンテキストは引き続き使用できますが、RDE プラグインに非推奨（廃止予定）の警告が表示されます。この警告は、```--quiet``` モードを使用すると省略できます。RDE プラグインの最新バージョンでは、コンテキスト「aio-cli-plugin-cloudmanager」を読み取るためのフォールバックは提供されません。引き続き利用するには、デフォルトのコンテキストを「aio-cli-plugin-cloudmanager」に設定するだけです。上記の[ローカルコンテキストの設定例](/help/implementing/developing/introduction/rapid-development-environments.md#installing-the-rde-command-line-tools)を参照してください。

#### Cloud Manager プラグインにも他のコンテキスト名を使用

Cloud Manager プラグインには、使用するコンテキストを定義するためのパラメーターが用意されています。IMS のデフォルトのコンテキスト設定は、まだサポートされていません。これを行うには、[ローカルコンテキストの設定例](/help/implementing/developing/introduction/rapid-development-environments.md#installing-the-rde-command-line-tools)を参照して、RDE プラグインを設定し、Cloud Manager プラグインに対して、すべての呼び出しで ```--imsContextName=myContext``` のように「myContext」を使用するように指示します。
