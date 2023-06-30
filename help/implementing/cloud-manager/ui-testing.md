---
title: UI テスト
description: カスタム UI テストは、カスタムアプリケーションの UI テストを作成して自動的に実行できるオプション機能です
exl-id: 3009f8cc-da12-4e55-9bce-b564621966dd
source-git-commit: 1994b90e3876f03efa571a9ce65b9fb8b3c90ec4
workflow-type: tm+mt
source-wordcount: '2389'
ht-degree: 74%

---


# UI テスト {#ui-testing}

>[!CONTEXTUALHELP]
>id="aemcloud_nonbpa_uitesting"
>title="UI テスト"
>abstract="カスタム UI テストは、アプリケーションの UI テストを作成して自動的に実行できるオプション機能です。UI テストは、言語とフレームワークの幅広い選択肢（Java と Maven、Node と WebDriver.io、Selenium に基づいて構築されたその他のフレームワークとテクノロジーなど）を可能にするために Docker イメージにパッケージ化された Selenium ベースのテストです。"

カスタム UI テストは、アプリケーションの UI テストを作成して自動的に実行できるオプション機能です。

## 概要 {#custom-ui-testing}

AEM には、[Cloud Manager 品質ゲート](/help/implementing/cloud-manager/custom-code-quality-rules.md)の統合スイートが用意されており、カスタムアプリケーションをスムーズに更新できるようになっています。特に、IT テストゲートでは、AEM API を使用したカスタムテストの作成と自動化に既に対応しています。

UI テストは、言語およびフレームワーク（Cypress、Selenium、Java および Maven、JavaScript など）の幅広い選択を可能にするために、Docker イメージでパッケージ化されています。 また、[AEM プロジェクトアーキタイプ](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/overview.html?lang=ja)を使用すると、UI テストプロジェクトを容易に生成できます。

Adobeは、リアルタイムの再読み込みと自動待ちを提供するので、Cypress を使用することを推奨します。これにより、時間を節約し、テスト中の生産性を向上させることができます。 Cypress は、簡単で直感的な構文を提供し、テストを初めて行うユーザーでも簡単に学習し、使用できます。

UI テストは、[実稼動パイプライン](/help/implementing/cloud-manager/configuring-pipelines/configuring-production-pipelines.md)またはオプションで[非実稼動パイプライン](/help/implementing/cloud-manager/configuring-pipelines/configuring-non-production-pipelines.md)の&#x200B;[**カスタム UI テスト**&#x200B;手順](/help/implementing/cloud-manager/deploy-code.md)で、各 Cloud Manager パイプラインの特定の品質ゲートの一部として実行します。回帰や新しい機能を含む UI テストでは、エラーの検出とレポートが可能です。

UI テストは、Java で記述された HTTP テストであるカスタム機能テストとは異なり、[UI テストの作成](#building-ui-tests)の節で定義されている規則に従う限り、任意の言語で記述されたテストを含む Docker イメージにすることができます。

>[!TIP]
>
>Adobeでは、UI テストに Cypress を使用することをお勧めします ( [AEM Test Samples リポジトリ](https://github.com/adobe/aem-test-samples/tree/aem-cloud/ui-cypress).
> 
>Adobeでは、WebdriverIO を使用した JavaScript に基づく UI テストモジュールの例も提供しています ( [AEM Project Archetype](https://github.com/adobe/aem-project-archetype/tree/master/src/main/archetype/ui.tests)) および Java と WebDriver( [AEM Test Samples リポジトリ](https://github.com/adobe/aem-test-samples/tree/aem-cloud/ui-selenium-webdriver)) をクリックします。

## UI テストの概要 {#get-started-ui-tests}

この節では、Cloud Manager で実行用の UI テストの設定に必要な手順について説明します。

1. 使用するプログラミング言語を決定します。

   * Cypress の場合は、 [AEM Test Samples リポジトリ](https://github.com/adobe/aem-test-samples/tree/aem-cloud/ui-cypress).

   * JavaScript と WDIO の場合は、Cloud Manager リポジトリの `ui.tests` フォルダーに自動的に生成されるサンプルコードを使用します。

     >[!NOTE]
     >
     >Cloud Manager が `ui.tests` フォルダーを自動作成する前にリポジトリが作成された場合は、[AEM プロジェクトアーキタイプ](https://github.com/adobe/aem-project-archetype/tree/master/src/main/archetype/ui.tests)を使用して最新バージョンを生成することもできます。

   * Java および WebDriver の場合は、[AEM テストサンプルのリポジトリ](https://github.com/adobe/aem-test-samples/tree/aem-cloud/ui-selenium-webdriver)からサンプルコードを使用します。

   * その他のプログラミング言語については、 [UI テストの構築](#building-ui-tests) このドキュメントでは、テストプロジェクトを設定します。

1. このドキュメントの[顧客オプトイン](#customer-opt-in)の節に従って、UI テストがアクティベートされていることを確認してください。

1. テストケースを作成し、 [ローカルでテストを実行する](#run-ui-tests-locally).

1. コードを Cloud Manager リポジトリにコミットし、Cloud Manager パイプラインを実行します。

## UI テストの作成 {#building-ui-tests}

Maven プロジェクトでは、Docker ビルドコンテキストを生成します。この Docker ビルドコンテキストでは、UI テストを含む Docker イメージを作成する方法を説明します。Cloud Manager はこれを使用して、実際の UI テストを含む Docker イメージを生成します。

この節では、UI テストプロジェクトをリポジトリーに追加するために必要な手順について説明します。

>[!TIP]
>
>この [AEM Project Archetype](https://github.com/adobe/aem-project-archetype) では、次の説明に準拠した UI テストプロジェクトを生成できます。プログラミング言語に関する特別な要件がない場合は、このプロジェクトが適用されます。

### Docker ビルドコンテキストの生成 {#generate-docker-build-context}

Docker ビルドコンテキストを生成するには、次の Maven モジュールが必要です。

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
>このファイルには、編集しないように指示する行が含まれている場合があります。これは、オプトイン UI テストが導入される前にプロジェクトに導入され、クライアントがファイルを編集する意図がなかったためです。 これは無視してかまいません。

アドビが指定したサンプルを使用する場合：

* [AEM プロジェクトアーキタイプ](https://github.com/adobe/aem-project-archetype/tree/master/src/main/archetype/ui.tests)に基づいて生成された JavaScript ベースの `ui.tests` フォルダーの場合、以下のコマンドを実行して必要な設定を追加できます。

  ```shell
  echo "ui-tests.version=1" > testing.properties
  
  if ! grep -q "testing.properties" "assembly-ui-test-docker-context.xml"; then
    awk -v line='                <include>testing.properties</include>' '/<include>wait-for-grid.sh<\/include>/ { printf "%s\n%s\n", $0, line; next }; 1' assembly-ui-test-docker-context.xml > assembly-ui-test-docker-context.xml.new && mv assembly-ui-test-docker-context.xml.new assembly-ui-test-docker-context.xml
  fi
  ```

* Adobeが提供する Cypress および Java Selenium のテストサンプルには、既にオプトインフラグが設定されています。

## UI テストの書き込み {#writing-ui-tests}

この節では、UI テストを含んだ Docker イメージが従う必要がある規則について説明します。Docker イメージは、前の節で説明した Docker ビルドコンテキストから作成されます。

### 環境変数 {#environment-variables}

フレームワークに応じて、実行時に次の環境変数が Docker イメージに渡されます。

| 変数 | 例 | 説明 | テストフレームワーク |
|---|---|---|---|
| `SELENIUM_BASE_URL` | `http://my-ip:4444` | Selenium サーバーの URL | Selenium のみ |
| `SELENIUM_BROWSER` | `chrome` | Selenium サーバーで使用されるブラウザー実装 | Selenium のみ |
| `AEM_AUTHOR_URL` | `http://my-ip:4502/context-path` | AEM オーサーインスタンスの URL | すべて |
| `AEM_AUTHOR_USERNAME` | `admin` | AEM オーサーインスタンスにログインするためのユーザー名 | すべて |
| `AEM_AUTHOR_PASSWORD` | `admin` | AEM オーサーインスタンスにログインするためのパスワード | すべて |
| `AEM_PUBLISH_URL` | `http://my-ip:4503/context-path` | AEM パブリッシュインスタンスの URL | すべて |
| `AEM_PUBLISH_USERNAME` | `admin` | AEM パブリッシュインスタンスにログインするためのユーザー名 | すべて |
| `AEM_PUBLISH_PASSWORD` | `admin` | AEM パブリッシュインスタンスにログインするためのパスワード | すべて |
| `REPORTS_PATH` | `/usr/src/app/reports` | テスト結果の XML レポートの保存先となるパス | すべて |
| `UPLOAD_URL` | `http://upload-host:9090/upload` | テストフレームワークにアクセスできるようにファイルをアップロードする必要がある URL | すべて |

アドビテストサンプルには、設定パラメーターにアクセスするためのヘルパー関数が用意されています。

* ヒノキ：標準関数を使用 `Cypress.env('VARIABLE_NAME')`
* JavaScript：詳しくは、[lib/config.js](https://github.com/adobe/aem-project-archetype/blob/develop/src/main/archetype/ui.tests/test-module/lib/config.js) モジュールを参照してください
* Java：詳しくは、[Config](https://github.com/adobe/aem-test-samples/blob/aem-cloud/ui-selenium-webdriver/test-module/src/main/java/com/adobe/cq/cloud/testing/ui/java/ui/tests/lib/Config.java) クラスを参照してください

### テストレポートの生成 {#generate-test-reports}

Docker イメージは、テストレポートを JUnit XML 形式で生成して、環境変数 `REPORTS_PATH` で指定されたパスに保存する必要があります。JUnit XML 形式は、テストの結果を報告するために広く使用されている形式です。 Docker イメージで Java と Maven を使用する場合、[Maven Surefire プラグイン](https://maven.apache.org/surefire/maven-surefire-plugin/)や [Maven Failsafe プラグイン](https://maven.apache.org/surefire/maven-failsafe-plugin/) などの標準テストモジュールでは、すぐに使用できるレポートを生成できます。

Docker イメージが他のプログラミング言語またはテストランナーで実装されている場合は、選択したツールのドキュメントを参照して、JUnit XML レポートの生成方法を確認してください。

>[!NOTE]
>
>UI テスト手順の結果は、テストレポートに基づいてのみ評価されます。 テストの実行に合わせてレポートを生成していることを確認します。
>
>エラーを STDERR に記録したり、ゼロ以外の終了コードを返すのではなく、アサーションを使用してください。そうしない場合、デプロイメントパイプラインが正常に実行されます。

### 前提条件 {#prerequisites}

* Cloud Manager のテストは、技術管理者ユーザーを使用して実行されます。

>[!NOTE]
>
>ローカルマシンから機能テストを実行する場合は、管理者のような権限を持つユーザーを作成して、同じ動作を実現します。

* 機能テストの範囲を定義するコンテナ化されたインフラストラクチャは、次の境界によって制限されます。

| タイプ | 値 | 説明 |
|----------------------|-------|-----------------------------------------------------------------------|
| CPU | 2.0 | テスト実行ごとに確保される CPU 時間の量です。 |
| メモリ | 1Gi | テストに割り当てられたメモリ量（GB 単位） |
| タイムアウト | 30m | テストが終了するまでの期間。 |
| 推奨期間 | 15m | Adobeは、この時間を超えないようにテストを書き込むことをお勧めします。 |

>[!NOTE]
>
> さらにリソースが必要な場合は、カスタマーケアケースを作成し、使用例を説明します。Adobeがリクエストを確認し、適切な支援を提供します。

## Selenium 固有の詳細

>[!NOTE]
>
>この節は、選択されたテストインフラストラクチャが Selenium の場合にのみ適用されます。

### Selenium の準備完了までの待機 {#waiting-for-selenium}

テストを開始する前に、Selenium サーバーが実行状態にあることを Docker イメージ側で確認する必要があります。Selenium サービスの準備が完了するまで、次の 2 段階の手順で待機します。

1. `SELENIUM_BASE_URL` 環境変数から Selenium サービスの URL を読み取ります。
1. Selenium API で公開されている[ステータスエンドポイント](https://github.com/SeleniumHQ/docker-selenium/#waiting-for-the-grid-to-be-ready)に対して定期的にポーリングを行います。

Selenium のステータスエンドポイントが肯定的な応答を返したら、テストを開始できます。

Adobe UI のテストサンプルでは、これをスクリプト `wait-for-grid.sh` で処理します。Docker の起動時に実行され、グリッドの準備が整った場合にのみ、実際のテストが実行されます。

### スクリーンショットとビデオのキャプチャ {#capture-screenshots}

Docker イメージでは、追加のテスト出力（スクリーンショットやビデオなど）が生成され、環境変数で指定されたパスに保存される場合があります `REPORTS_PATH`. `REPORTS_PATH` の下にあるファイルはすべて、テスト結果のアーカイブに含まれます。

デフォルトでアドビが提供するテストサンプルは、失敗したテストのスクリーンショットを作成します。

ヘルパー関数を使用して、テストのスクリーンショットを作成できます。

* JavaScript：[takeScreenshot コマンド](https://github.com/adobe/aem-project-archetype/blob/develop/src/main/archetype/ui.tests/test-module/lib/commons.js)
* Java：[コマンド](https://github.com/adobe/aem-test-samples/blob/aem-cloud/ui-selenium-webdriver/test-module/src/main/java/com/adobe/cq/cloud/testing/ui/java/ui/tests/lib/Commands.java)

UI テストの実行中にテスト結果アーカイブが作成された場合は、[**カスタム UI テスト**&#x200B;手順](/help/implementing/cloud-manager/deploy-code.md)の下にある「`Download Details`」ボタンを使用して、Cloud Manager からダウンロードできます。

### ファイルのアップロード {#upload-files}

テストでは、場合によって、テスト中のアプリケーションにファイルをアップロードする必要があります。テストに対する Selenium のデプロイメントを柔軟に保つため、Selenium に直接アセットをアップロードすることはできません。 ファイルをアップロードするには、代わりに次の手順を実行する必要があります。

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

## UI テストのローカルでの実行 {#run-ui-tests-locally}

Cloud Manager パイプラインで UI テストをアクティブ化する前に、UI テストを
[AEM as a Cloud Service SDK](/help/implementing/developing/introduction/aem-as-a-cloud-service-sdk.md) に対してローカルで実行するか、
実際の AEM as a Cloud Service インスタンスに対してローカルで実行することをお勧めします。

### ヒノキ試験サンプル {#cypress-sample}

1. シェルを開き、リポジトリ内の `ui.tests/test-module` フォルダーに移動します

1. Cypress とその他の前提条件のインストール

   ```shell
   npm install
   ```

1. テストの実行に必要な環境変数の設定

   ```shell
   export AEM_AUTHOR_URL=https://author-<program-id>-<environment-id>.adobeaemcloud.com
   export AEM_AUTHOR_USERNAME=<user>
   export AEM_AUTHOR_PASSWORD=<password>
   export AEM_PUBLISH_URL=https://publish-<program-id>-<environment-id>.adobeaemcloud.com
   export AEM_PUBLISH_USERNAME=<user>
   export AEM_PUBLISH_PASSWORD=<password>
   export REPORTS_PATH=target/
   ```

1. 次のいずれかのコマンドでテストを実行します。

   ```shell
   npm test              # Using default Cypress browser
   npm run test-chrome   # Using Google Chrome browser
   npm run test-firefox  # Using Firefox browser
   ```

>[!NOTE]
>
>ログファイルは、 `target/` リポジトリのフォルダー。
>
>詳しくは、 [AEM Test Samples リポジトリ](https://github.com/adobe/aem-test-samples/blob/aem-cloud/ui-cypress/test-module/README.md).

### JavaScript WebdriverIO テストの例 {#javascript-sample}

1. シェルを開き、リポジトリ内の `ui.tests` フォルダーに移動します

1. Maven を使用してテストを開始するには、次のコマンドを実行します

   ```shell
   mvn verify -Pui-tests-local-execution \
    -DAEM_AUTHOR_URL=https://author-<program-id>-<environment-id>.adobeaemcloud.com \
    -DAEM_AUTHOR_USERNAME=<user> \
    -DAEM_AUTHOR_PASSWORD=<password> \
    -DAEM_PUBLISH_URL=https://publish-<program-id>-<environment-id>.adobeaemcloud.com \
    -DAEM_PUBLISH_USERNAME=<user> \
    -DAEM_PUBLISH_PASSWORD=<password>
   ```

>[!NOTE]
>
>* これにより、スタンドアロンの Selenium インスタンスが開始され、それに対するテストが実行されます。
>* ログファイルは、リポジトリの `target/reports` フォルダーに保存されます。
>* テストで ChromeDriver の最新リリースがテスト用に自動的にダウンロードされるので、お使いのコンピューターで最新バージョンの Chrome が実行されていることを確認する必要があります。
>
>詳しくは、 [AEM Project Archetype リポジトリ](https://github.com/adobe/aem-project-archetype/blob/develop/src/main/archetype/ui.tests/README.md).

### Java Selenium WebDriver テストの例 {#java-sample}

1. シェルを開き、リポジトリ内の `ui.tests/test-module` フォルダーに移動します

1. Maven を使用してテストを開始するには、次のコマンドを実行します

   ```shell
   # Start selenium docker image (for x64 CPUs)
   docker run --platform linux/amd64 -d -p 4444:4444 selenium/standalone-chrome-debug:latest
   
   # Start selenium docker image (for ARM CPUs)
   docker run -d -p 4444:4444 seleniarm/standalone-chromium
   
   # Run the tests using the previously started Selenium instance
   mvn verify -Pui-tests-local-execution -DSELENIUM_BASE_URL=http://<server>:4444
   ```

>[!NOTE]
>
>ログファイルは、 `target/reports` リポジトリのフォルダー。
>
>詳しくは、 [AEM Test Samples リポジトリ](https://github.com/adobe/aem-test-samples/blob/aem-cloud/ui-selenium-webdriver/README.md).
