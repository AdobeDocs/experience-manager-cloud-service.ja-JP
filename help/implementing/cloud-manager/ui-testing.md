---
title: UI テスト
description: カスタム UI テストは、カスタムアプリケーションの UI テストを作成して自動的に実行できるオプション機能です
exl-id: 3009f8cc-da12-4e55-9bce-b564621966dd
source-git-commit: 24796bd7d9c5e726cda13885bc4bd7e4155610dc
workflow-type: tm+mt
source-wordcount: '2238'
ht-degree: 86%

---


# UI テスト {#ui-testing}

>[!CONTEXTUALHELP]
>id="aemcloud_nonbpa_uitesting"
>title="UI テスト"
>abstract="カスタム UI テストは、アプリケーションの UI テストを作成して自動的に実行できるオプション機能です。UI テストは、言語とフレームワークの幅広い選択肢（Java と Maven、Node と WebDriver.io、Selenium に基づいて構築されたその他のフレームワークとテクノロジーなど）を可能にするために Docker イメージにパッケージ化された Selenium ベースのテストです。"

カスタム UI テストは、アプリケーションの UI テストを作成して自動的に実行できるオプション機能です。

## 概要 {#custom-ui-testing}

AEM には、[Cloud Manager 品質ゲート](/help/implementing/cloud-manager/custom-code-quality-rules.md)の統合スイートが用意されており、カスタムアプリケーションをスムーズに更新できるようになっています。特に、IT テストゲートでは、AEM API を使用したカスタムテストの作成と自動化に既に対応しています。

UI テストは、言語とフレームワークの幅広い選択肢（Java と Maven、Node と WebDriver.io、Selenium に基づいて構築されたその他のフレームワークとテクノロジーなど）を可能にするために Docker イメージにパッケージ化された Selenium ベースのテストです。また、 [AEMプロジェクトアーキタイプ](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/overview.html?lang=ja).

UI テストは、Cloud Manager の各パイプラインの特定の品質ゲートの一部として、 [**カスタム UI テスト** 手順](/help/implementing/cloud-manager/deploy-code.md) in [実稼動パイプライン](/help/implementing/cloud-manager/configuring-pipelines/configuring-production-pipelines.md) または [非実稼動パイプライン](/help/implementing/cloud-manager/configuring-pipelines/configuring-non-production-pipelines.md). を含む Cloud Manager パイプラインごとに、特定の品質ゲートの一部として実行されます。リグレッションや新しい機能を含む UI テストでは、エラーの検出とレポートが可能です。

Java で記述された HTTP テストであるカスタム機能テストとは異なり、UI テストは、の節で定義された規則に従う限り、任意の言語で記述されたテストを含む Docker イメージにすることができます [UI テストの構築](#building-ui-tests).

>[!TIP]
>
>Adobeでは、 [AEM Project Archetype](https://github.com/adobe/aem-project-archetype/tree/master/src/main/archetype/ui.tests).
>
>アドビは、Java および WebDriver に基づく UI テストモジュールの例も提供しています。 詳しくは、[AEM テストサンプルのリポジトリ](https://github.com/adobe/aem-test-samples/tree/aem-cloud/ui-selenium-webdriver)を参照してください。

## UI テストの概要 {#get-started-ui-tests}

この節では、Cloud Manager で実行用の UI テストの設定に必要な手順について説明します。

1. 使用するプログラミング言語を決定します。

   * JavaScript と WDIO の場合は、Cloud Manager リポジトリの `ui.tests` フォルダーに自動的に生成されるサンプルコードを使用します。

      >[!NOTE]
      >
      >Cloud Manager が自動的に作成される前にリポジトリが作成された場合 `it.tests` フォルダーの場合は、 [AEM Project Archetype](https://github.com/adobe/aem-project-archetype/tree/master/src/main/archetype/it.tests).

   * Java および WebDriver の場合は、 [AEM Test Samples リポジトリ](https://github.com/adobe/aem-test-samples/tree/aem-cloud/ui-selenium-webdriver).

   * その他のプログラミング言語については、このドキュメントの [UI テストの構築](#building-ui-tests)の節を参照して、テストプロジェクトを設定してください。

1. このドキュメントの[顧客オプトイン](#customer-opt-in)の節に従って、UI テストがアクティベートされていることを確認してください。

1. テストケースを作成し、 [ローカルでテストを実行](#run-ui-tests-locally).

1. コードを Cloud Manager リポジトリにコミットし、Cloud Manager パイプラインを実行します。

## UI テストの作成 {#building-ui-tests}

Maven プロジェクトでは、Docker ビルドコンテキストを生成します。この Docker ビルドコンテキストでは、UI テストを含む Docker イメージを作成する方法を説明します。Cloud Manager はこれを使用して、実際の UI テストを含む Docker イメージを生成します。

この節では、UI テストプロジェクトをリポジトリーに追加するために必要な手順について説明します。

>[!TIP]
>
>[AEM プロジェクトアーキタイプ](https://github.com/adobe/aem-project-archetype)では、プログラミング言語に特別な要件がない場合、次の説明に準拠した UI テストプロジェクトを生成できます。

### Docker ビルドコンテキストの生成 {#generate-docker-build-context}

Docker ビルドコンテキストを生成するには、次の処理を行う Maven モジュールが必要です。

* `Dockerfile`と、テストを含んだ Docker イメージの作成に必要なその他のすべてのファイルを格納したアーカイブを作成する。
* アーカイブに `ui-test-docker-context` 分類子をタグ付けする。

これを行うには、[Maven アセンブリプラグイン](https://maven.apache.org/plugins/maven-assembly-plugin/)を設定して Docker ビルドコンテキストアーカイブを作成し、それに適切な分類子を割り当てるのが最も簡単です。

様々なテクノロジーとフレームワークを使用して UI テストを作成できますが、この節では、プロジェクトが次のようにレイアウトされていることを前提としています。

```text
├── Dockerfile
├── assembly-ui-test-docker-context.xml
├── pom.xml
├── test-module
│   ├── package.json
│   ├── index.js
│   └── wdio.conf.js
└── wait-for-grid.sh
```

`pom.xml` ファイルは Maven ビルドを扱います。次のような Maven アセンブリプラグインに実行を追加します。

```xml
<plugin>
    <groupId>org.apache.maven.plugins</groupId>
    <artifactId>maven-assembly-plugin</artifactId>
    <configuration>
        <descriptors>
            <descriptor>${project.basedir}/assembly-ui-test-docker-context.xml</descriptor>
        </descriptors>
        <tarLongFileMode>gnu</tarLongFileMode>
    </configuration>
    <executions>
        <execution>
            <id>make-assembly</id>
            <phase>package</phase>
            <goals>
                <goal>single</goal>
            </goals>
        </execution>
    </executions>
</plugin>
```

この実行は、`assembly-ui-test-docker-context.xml` に含まれている命令（プラグインの専門用語では&#x200B;**アセンブリ記述子**&#x200B;と呼ばれます）に基づいてアーカイブを作成するように Maven アセンブリプラグインに指示します。アセンブリ記述子では、アーカイブに含める必要のあるすべてのファイルがリストアップされます。

```xml
<assembly>
    <id>ui-test-docker-context</id>
    <includeBaseDirectory>false</includeBaseDirectory>
    <formats>
        <format>tar.gz</format>
    </formats>
    <fileSets>
        <fileSet>
            <directory>${basedir}</directory>
            <includes>
                <include>Dockerfile</include>
                <include>wait-for-grid.sh</include>
            </includes>
        </fileSet>
        <fileSet>
            <directory>${basedir}/test-module</directory>
            <excludes>
                <exclude>node/**</exclude>
                <exclude>node_modules/**</exclude>
                <exclude>reports/**</exclude>
            </excludes>
        </fileSet>
    </fileSets>
</assembly>
```

アセンブリ記述子は、`.tar.gz` タイプのアーカイブを作成するようにプラグインに指示し、そのアーカイブに `ui-test-docker-context` 分類子を割り当てます。さらに、そのアーカイブに含める必要のある次のファイルがリストアップされます。

* `Dockerfile`：Docker イメージの作成に必須
* `wait-for-grid.sh` スクリプト：目的は後述のとおり
* 実際の UI テスト：`test-module` フォルダー内に Node.js プロジェクトで実装

また、アセンブリ記述子は、UI テストのローカル実行中に生成される可能性のある一部のファイルを除外します。これにより、アーカイブのサイズが小さくなり、ビルドが高速になります。

Docker ビルドコンテキストを含んだアーカイブが Cloud Manager で自動的に選択され、テストを含んだ Docker イメージがデプロイメントパイプライン中に作成されます。最終的に、Cloud Manager は Docker イメージを実行して、アプリケーションに対する UI テストを実行します。

ビルドでは、0 または 1 つのアーカイブが生成されます。アーカイブが 0 の場合、テストステップはデフォルトで通過します。ビルドで複数のアーカイブが生成される場合、どのアーカイブが選択されるかは非決定的です。

### 顧客オプトイン {#customer-opt-in}

Cloud Manager で UI テストを作成して実行するには、リポジトリにファイルを追加して、この機能をオプトインする必要があります。

* ファイル名は `testing.properties` にする必要があります。
* ファイルの内容は `ui-tests.version=1` にする必要があります。
* このファイルは、UI テストサブモジュールの `pom.xml` ファイルの横にある UI テスト用 Maven サブモジュールの下にある必要があります。
* ファイルは、作成された `tar.gz` ファイルのルートに必要です。

このファイルが存在しない場合、UI テストの作成と実行はスキップされます。

`testing.properties` ファイルをビルドアーティファクトに含めるには、`include` ステートメントを `assembly-ui-test-docker-context.xml` ファイルを追加します。

```xml
[...]
<includes>
    <include>Dockerfile</include>
    <include>wait-for-grid.sh</include>
    <include>testing.properties</include> <!-- opt-in test module in Cloud Manager -->
</includes>
[...]
```

>[!NOTE]
>
>プロジェクトにこの行が含まれていない場合、UI テストをオプトインするには、このファイルを編集する必要があります。
>
>このファイルには、編集しないように指示する行が含まれている場合があります。これは、このファイルが、オプトイン UI テストが導入される前にプロジェクトに導入され、クライアントがファイルを編集することが想定さていなかったためです。これは無視してかまいません。

アドビが指定したサンプルを使用する場合：

* [AEM プロジェクトアーキタイプ](https://github.com/adobe/aem-project-archetype/tree/master/src/main/archetype/ui.tests)に基づいて生成された JavaScript ベースの `ui.tests` フォルダーの場合、以下のコマンドを実行して必要な設定を追加できます。

   ```shell
   echo "ui-tests.version=1" > testing.properties
   
   if ! grep -q "testing.properties" "assembly-ui-test-docker-context.xml"; then
     awk -v line='                <include>testing.properties</include>' '/<include>wait-for-grid.sh<\/include>/ { printf "%s\n%s\n", $0, line; next }; 1' assembly-ui-test-docker-context.xml > assembly-ui-test-docker-context.xml.new && mv assembly-ui-test-docker-context.xml.new assembly-ui-test-docker-context.xml
   fi
   ```

* 提供済みの Java テストサンプルでは、既にオプトインフラグが設定されています。

## UI テストの書き込み {#writing-ui-tests}

この節では、UI テストを含んだ Docker イメージが従う必要がある規則について説明します。Docker イメージは、前の節で説明した Docker ビルドコンテキストから作成されます。

### 環境変数 {#environment-variables}

実行時に次の環境変数が Docker イメージに渡されます。

| 変数 | 例 | 説明 |
|---|---|---|
| `SELENIUM_BASE_URL` | `http://my-ip:4444` | Selenium サーバーの URL |
| `SELENIUM_BROWSER` | `chrome` | Selenium サーバーで使用されるブラウザー実装 |
| `AEM_AUTHOR_URL` | `http://my-ip:4502/context-path` | AEM オーサーインスタンスの URL |
| `AEM_AUTHOR_USERNAME` | `admin` | AEM オーサーインスタンスにログインするためのユーザー名 |
| `AEM_AUTHOR_PASSWORD` | `admin` | AEM オーサーインスタンスにログインするためのパスワード |
| `AEM_PUBLISH_URL` | `http://my-ip:4503/context-path` | AEM パブリッシュインスタンスの URL |
| `AEM_PUBLISH_USERNAME` | `admin` | AEM パブリッシュインスタンスにログインするためのユーザー名 |
| `AEM_PUBLISH_PASSWORD` | `admin` | AEM パブリッシュインスタンスにログインするためのパスワード |
| `REPORTS_PATH` | `/usr/src/app/reports` | テスト結果の XML レポートの保存先となるパス |
| `UPLOAD_URL` | `http://upload-host:9090/upload` | Selenium からファイルにアクセスできるようにするためのファイルアップロード先の URL |

アドビテストサンプルには、設定パラメーターにアクセスするためのヘルパー関数が用意されています。

* JavaScript：詳しくは、[lib/config.js](https://github.com/adobe/aem-project-archetype/blob/develop/src/main/archetype/ui.tests/test-module/lib/config.js) モジュールを参照してください
* Java：詳しくは、[Config](https://github.com/adobe/aem-test-samples/blob/aem-cloud/ui-selenium-webdriver/test-module/src/main/java/com/adobe/cq/cloud/testing/ui/java/ui/tests/lib/Config.java) クラスを参照してください

### Selenium の準備完了までの待機 {#waiting-for-selenium}

テストを開始する前に、Selenium サーバーが実行状態にあることを Docker イメージ側で確認する必要があります。Selenium サービスの準備が完了するまで、次の 2 段階の手順で待機します。

1. `SELENIUM_BASE_URL` 環境変数から Selenium サービスの URL を読み取ります。
1. Selenium API で公開されている[ステータスエンドポイント](https://github.com/SeleniumHQ/docker-selenium/#waiting-for-the-grid-to-be-ready)に対して定期的にポーリングを行います。

Selenium のステータスエンドポイントが肯定的な応答を返したら、テストを開始できます。

Adobe UI のテストサンプルでは、これをスクリプト `wait-for-grid.sh` で処理します。Docker の起動時に実行され、グリッドの準備が整った場合にのみ、実際のテストが実行されます。

### テストレポートの生成 {#generate-test-reports}

Docker イメージは、テストレポートを JUnit XML 形式で生成して、環境変数 `REPORTS_PATH` で指定されたパスに保存する必要があります。JUnit XML 形式は、テスト結果のレポートに広く使用されている形式です。Docker イメージで Java と Maven を使用する場合、[Maven Surefire プラグイン](https://maven.apache.org/surefire/maven-surefire-plugin/)や [Maven Failsafe プラグイン](https://maven.apache.org/surefire/maven-failsafe-plugin/) などの標準テストモジュールでは、すぐに使用できるレポートを生成できます。

Docker イメージが他のプログラミング言語またはテストランナーで実装されている場合は、選択したツールのドキュメントを参照して、JUnit XML レポートの生成方法を確認してください。

>[!NOTE]
>
>UI テスト手順の結果は、テストレポートに基づいてのみ評価されます。 テストの実行に合わせてレポートを生成するようにしてください。
>
>エラーを STDERR に記録したり、ゼロ以外の終了コードを返すのではなく、アサーションを使用してください。そうしない場合、デプロイメントパイプラインが正常に実行されます。

### スクリーンショットとビデオのキャプチャ {#capture-screenshots}

Docker イメージでは、追加のテスト出力（スクリーンショット、ビデオなど）を生成し、それらを環境変数 `REPORTS_PATH` で指定されたパスに保存する場合があります。`REPORTS_PATH` の下にあるファイルはすべて、テスト結果のアーカイブに含まれます。

デフォルトでアドビが提供するテストサンプルは、失敗したテストのスクリーンショットを作成します。

ヘルパー関数を使用して、テストのスクリーンショットを作成できます。

* JavaScript：[takeScreenshot コマンド](https://github.com/adobe/aem-project-archetype/blob/develop/src/main/archetype/ui.tests/test-module/lib/commons.js)
* Java：[コマンド](https://github.com/adobe/aem-test-samples/blob/aem-cloud/ui-selenium-webdriver/test-module/src/main/java/com/adobe/cq/cloud/testing/ui/java/ui/tests/lib/Commands.java)

UI テストの実行中にテスト結果アーカイブが作成された場合は、Cloud Manager から、 `Download Details` ボタン [**カスタム UI テスト** 手順](/help/implementing/cloud-manager/deploy-code.md).

### ファイルのアップロード {#upload-files}

テストでは、場合によって、テスト中のアプリケーションにファイルをアップロードする必要があります。テストに対する Selenium デプロイメントの柔軟性を維持するため、Selenium に直接アセットをアップロードすることはできません。ファイルをアップロードするには、代わりに次の手順を実行する必要があります。

1. `UPLOAD_URL` 環境変数で指定された URL にファイルをアップロードします。
   * アップロードは、マルチパートフォームを含んだ 1 つの POST リクエストで実行する必要があります。
   * このマルチパートフォームには、1 つのファイルフィールドが必要です。
   * これは `curl -X POST ${UPLOAD_URL} -F "data=@file.txt"` と同等です。
   * このような HTTP リクエストを実行する方法については、Docker イメージで使用されているプログラミング言語のドキュメントやライブラリを参照してください。
   * アドビテストサンプルには、ファイルをアップロードするためのヘルパー関数が用意されています。
      * JavaScript：[getFileHandleForUpload](https://github.com/adobe/aem-project-archetype/blob/develop/src/main/archetype/ui.tests/test-module/lib/wdio.commands.js) コマンドを参照してください。
      * Java：[FileHandler](https://github.com/adobe/aem-test-samples/blob/aem-cloud/ui-selenium-webdriver/test-module/src/main/java/com/adobe/cq/cloud/testing/ui/java/ui/tests/lib/FileHandler.java) クラスを参照してください。
1. アップロードが成功した場合、リクエストは `200 OK` タイプの `text/plain` 応答を返します。
   * この応答の内容は不透明なファイルハンドルです。
   * `<input>` 要素のファイルパスの代わりにこのハンドルを使用して、アプリケーション内のアップロードファイルをテストできます。

### 前提条件 {#prerequisites}

1. Cloud Manager でのテストは、技術管理者ユーザーを使用して実行されます。

>[!NOTE]
>
>ローカルマシンから機能テストを実行する場合は、管理者のような権限を持つユーザーを作成して、同じ動作を実現します。

1. 機能テストの範囲を定義するコンテナ化されたインフラストラクチャは、次の境界によって制限されます。

| タイプ | 値 | 説明 |
|----------------------|-------|--------------------------------------------------------------------|
| CPU | 2.0 | テスト実行ごとに予約される CPU 時間の量 |
| メモリ | 1Gi | テストに割り当てられたメモリの量（GB 単位の値） |
| タイムアウト | 30m | テストを終了するまでの期間。 |
| 推奨期間 | 15m | この時間を超えないようにテストを書き込むことをお勧めします。 |

>[!NOTE]
>
> より多くのリソースが必要な場合は、カスタマーケアケースを作成し、使用例を説明してください。アドビのチームがお客様のリクエストを確認し、適切な支援を提供します。


## UI テストのローカルでの実行 {#run-ui-tests-locally}

Cloud Manager パイプラインで UI テストをアクティブ化する前に、UI テストを [AEMas a Cloud ServiceSDK](/help/implementing/developing/introduction/aem-as-a-cloud-service-sdk.md)
実際のAEM as a Cloud Serviceインスタンスに対して

### JavaScript テストの例 {#javascript-sample}

1. シェルを開き、リポジトリ内の `ui.tests` フォルダーに移動します

1. Maven を使用してテストを開始するには、次のコマンドを実行します

   ```shell
   mvn verify -Pui-tests-local-execution \
   -DAEM_AUTHOR_URL=https://author-<program-id>-<environment-id>.adobeaemcloud.com \
   -DAEM_AUTHOR_USERNAME=<user> \
   -DAEM_AUTHOR_PASSWORD=<password> \
   -DAEM_PUBLISH_URL=https://publish-<program-id>-<environment-id>.adobeaemcloud.com \
   -DAEM_PUBLISH_USERNAME=<user> \
   -DAEM_PUBLISH_PASSWORD=<password> \
   -DHEADLESS_BROWSER=true \
   -DSELENIUM_BROWSER=chrome
   ```

>[!NOTE]
>
>* これにより、スタンドアロンの Selenium インスタンスが起動し、それに対するテストが実行されます。
>* ログファイルは、リポジトリの `target/reports` フォルダーに保存されます。
>* テストでは ChromeDriver の最新リリースがテスト用に自動的にダウンロードされるので、最新バージョンの Chrome を使用していることを確認する必要があります。
>
>詳しくは、 [AEM Project Archetype リポジトリ](https://github.com/adobe/aem-project-archetype/blob/develop/src/main/archetype/ui.tests/README.md).

### Java テストの例 {#java-sample}

1. シェルを開き、リポジトリ内の `ui.tests/test-module` フォルダーに移動します

1. Maven を使用してテストを開始するには、次のコマンドを実行します

   ```shell
   # Start selenium docker image (for x64 CPUs)
   docker run --platform linux/amd64 -d -p 4444:4444 selenium/standalone-chrome-debug:latest
   
   # Start selenium docker image (for ARM CPUs)
   docker run -d -p 4444:4444 seleniarm/standalone-chromium
   
   # Run the tests using the previously started Selenium instance
   mvn verify -Pui-tests-local-execution -DSELENIUM_BASE_URL=http://<server>:<port>
   ```

>[!NOTE]
>
>* ログファイルは、リポジトリの `target/reports` フォルダーに保存されます。
>
>詳しくは、 [AEM Test Samples リポジトリ](https://github.com/adobe/aem-test-samples/blob/aem-cloud/ui-selenium-webdriver/README.md).
