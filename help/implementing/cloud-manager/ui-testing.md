---
title: UI テスト
description: カスタム UI テストは、カスタムアプリケーションの UI テストを作成して自動的に実行できるオプション機能です
exl-id: 3009f8cc-da12-4e55-9bce-b564621966dd
source-git-commit: 305098c7ebcb6145129b146d60538b5177b4f26d
workflow-type: tm+mt
source-wordcount: '2610'
ht-degree: 80%

---


# UI テスト {#ui-testing}

>[!CONTEXTUALHELP]
>id="aemcloud_nonbpa_uitesting"
>title="UI テスト"
>abstract="カスタム UI テストは、アプリケーションの UI テストを作成して自動的に実行できるオプション機能です。UI テストは、言語とフレームワークの幅広い選択肢（Java と Maven、Node と WebDriver.io、Selenium に基づいて構築されたその他のフレームワークとテクノロジーなど）を可能にするために Docker イメージにパッケージ化された Selenium ベースのテストです。"

カスタム UI テストは、アプリケーションの UI テストを作成して自動的に実行できるオプション機能です。

## 概要 {#custom-ui-testing}

AEM には、[Cloud Manager 品質ゲート](/help/implementing/cloud-manager/custom-code-quality-rules.md)の統合スイートが用意されており、カスタムアプリケーションをスムーズに更新できるようになっています。特に、IT テストゲートでは、AEM API を使用したカスタムテストの作成と自動化に既に対応しています。

UI テストは、言語とフレームワーク（Cypress、Selenium、Java と Maven、JavaScript など）を幅広く選択できるように、Docker イメージにパッケージ化されています。また、[AEM プロジェクトアーキタイプ](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/overview.html?lang=ja)を使用すると、UI テストプロジェクトを容易に生成できます。

アドビでは、リアルタイムの再読み込みと自動待機が利用でき、時間の節約やテスト中の生産性の向上に役立つ、Cypress の使用をお勧めします。Cypress は、簡単で直感的な構文を提供し、テストを初めて行うユーザーでも学習や使用が簡単にできます。

UI テストは、[実稼動パイプライン](/help/implementing/cloud-manager/configuring-pipelines/configuring-production-pipelines.md)またはオプションで[非実稼動パイプライン](/help/implementing/cloud-manager/configuring-pipelines/configuring-non-production-pipelines.md)の&#x200B;[**カスタム UI テスト**&#x200B;手順](/help/implementing/cloud-manager/deploy-code.md)で、各 Cloud Manager パイプラインの特定の品質ゲートの一部として実行します。回帰や新しい機能を含む UI テストでは、エラーが検出、報告されます。

UI テストは、Java で記述された HTTP テストであるカスタム機能テストとは異なり、[UI テストの作成](#building-ui-tests)の節で定義されている規則に従う限り、任意の言語で記述されたテストを含む Docker イメージにすることができます。

>[!TIP]
>
>アドビでは、[AEM テストサンプルのリポジトリ](https://github.com/adobe/aem-test-samples/tree/aem-cloud/ui-cypress)で提供されているコードに従って、UI テストに Cypress を使用することをお勧めします。
> 
>アドビでは、JavaScript と WebdriverIO（[AEM プロジェクトアーキタイプ](https://github.com/adobe/aem-project-archetype/tree/master/src/main/archetype/ui.tests)）および Java と WebDriver（[AEM テストサンプルのリポジトリ](https://github.com/adobe/aem-test-samples/tree/aem-cloud/ui-selenium-webdriver)）に基づく UI テストモジュールの例も提供しています。

## UI テストの概要 {#get-started-ui-tests}

この節では、Cloud Manager で実行用の UI テストの設定に必要な手順について説明します。

1. 使用するプログラミング言語を決定します。

   * Cypress の場合は、[AEM テストサンプルのリポジトリ](https://github.com/adobe/aem-test-samples/tree/aem-cloud/ui-cypress)からサンプルコードを使用します。

   * JavaScript と WDIO の場合は、に自動的に生成されるサンプルコードを使用します。 `ui.tests` cloud Manager リポジトリのフォルダー。

     >[!NOTE]
     >
     >Cloud Manager が `ui.tests` フォルダーを自動作成する前にリポジトリが作成された場合は、[AEM プロジェクトアーキタイプ](https://github.com/adobe/aem-project-archetype/tree/master/src/main/archetype/ui.tests)を使用して最新バージョンを生成することもできます。

   * Java および WebDriver の場合は、[AEM テストサンプルのリポジトリ](https://github.com/adobe/aem-test-samples/tree/aem-cloud/ui-selenium-webdriver)からサンプルコードを使用します。

   * その他のプログラミング言語については、このドキュメントの [UI テストの構築](#building-ui-tests)の節を参照して、テストプロジェクトを設定してください。

1. このドキュメントの[顧客オプトイン](#customer-opt-in)の節に従って、UI テストがアクティベートされていることを確認してください。

1. テストケースを作成し、[ローカルでテストを実行します](#run-ui-tests-locally)。

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

アセンブリ記述子は、`.tar.gz` タイプのアーカイブを作成するようにプラグインに指示し、そのアーカイブに `ui-test-docker-context` 分類子を割り当てます。さらに、アーカイブに含める必要がある次のようなファイルが一覧表示されます。

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

`testing.properties` ファイルをビルドアーティファクトに含めるには、`include` ステートメントを `assembly-ui-test-docker-context.xml` ファイルに追加します。

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
>プロジェクトにこの行が含まれていない場合、UI テストをオプトインするには、このファイルを編集します。
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

* Adobeが提供する Cypress および Java Selenium テストサンプルには、既にオプトインフラグが設定されています。

## UI テストの書き込み {#writing-ui-tests}

この節では、UI テストを含んだ Docker イメージが従う必要がある規則について説明します。Docker イメージは、前の節で説明した Docker ビルドコンテキストから作成されます。

### 環境変数 {#environment-variables}

フレームワークに応じて、実行時に次の環境変数が Docker イメージに渡されます。

| 変数 | 例 | 説明 | テストフレームワーク |
|----------------------------|----------------------------------|---------------------------------------------------------------------------------------------------|---------------------|
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
| `PROXY_HOST` | `proxy-host` | テストフレームワークで使用される内部 HTTP プロキシのホスト名 | Selenium を除くすべて |
| `PROXY_HTTPS_PORT` | `8071` | HTTPS 接続のプロキシサーバーのリスニングポート （空にすることができます） | Selenium を除くすべて |
| `PROXY_HTTP_PORT` | `8070` | HTTP 接続のプロキシサーバーのリスニングポート （空にすることができます） | Selenium を除くすべて |
| `PROXY_CA_PATH` | `/path/to/root_ca.pem` | テストフレームワークで使用される CA 証明書へのパス | Selenium を除くすべて |
| `PROXY_OBSERVABILITY_PORT` | `8081` | プロキシサーバーの HTTP ヘルスチェックポート | Selenium を除くすべて |
| `PROXY_RETRY_ATTEMPTS` | `12` | プロキシサーバーの準備待ちの再試行推奨回数 | Selenium を除くすべて |
| `PROXY_RETRY_DELAY` | `5` | プロキシサーバーの準備待ちの再試行間に推奨される遅延 | Selenium を除くすべて |

アドビテストサンプルには、設定パラメーターにアクセスするためのヘルパー関数が用意されています。

* Cypress：標準関数 `Cypress.env('VARIABLE_NAME')` を使用します
* JavaScript：詳しくは、 [`lib/config.js`](https://github.com/adobe/aem-project-archetype/blob/develop/src/main/archetype/ui.tests.wdio/test-module/lib/config.js) モジュール
* Java：詳しくは [`Config`](https://github.com/adobe/aem-test-samples/blob/aem-cloud/ui-selenium-webdriver/test-module/src/main/java/com/adobe/cq/cloud/testing/ui/java/ui/tests/lib/Config.java) クラス

### テストレポートの生成 {#generate-test-reports}

Docker イメージは、テストレポートを JUnit XML 形式で生成して、環境変数 `REPORTS_PATH` で指定されたパスに保存する必要があります。JUnit XML 形式は、テスト結果のレポートに広く使用されている形式です。Docker イメージで Java と Maven を使用する場合、[Maven Surefire プラグイン](https://maven.apache.org/surefire/maven-surefire-plugin/)や [Maven Failsafe プラグイン](https://maven.apache.org/surefire/maven-failsafe-plugin/) などの標準テストモジュールでは、すぐに使用できるレポートを生成できます。

Docker イメージが他のプログラミング言語またはテストランナーで実装されている場合は、選択したツールのドキュメントを参照して、JUnit XML レポートの生成方法を確認してください。

>[!NOTE]
>
>UI テスト手順の結果は、テストレポートに基づいてのみ評価されます。 テストの実行に合わせてレポートを生成するようにしてください。
>
>エラーを STDERR に記録したり、ゼロ以外の終了コードを返すのではなく、アサーションを使用してください。そうしない場合、デプロイメントパイプラインが正常に実行されます。
>
>テストの実行中に HTTP プロキシが使用された場合、結果には次が含まれます `request.log` ファイル。

### 前提条件 {#prerequisites}

* Cloud Manager でのテストは、技術管理者ユーザーを使用して実行されます。

>[!NOTE]
>
>ローカルマシンから機能テストを実行する場合は、管理者のような権限を持つユーザーを作成して、同じ動作を実現します。

* 機能テストの範囲を定義するコンテナ化されたインフラストラクチャは、次の境界によって制限されます。

| タイプ | 値 | 説明 |
|----------------------|-------|-----------------------------------------------------------------------|
| CPU | 2.0 | テスト実行ごとに確保される CPU 時間の量です。 |
| メモリ | 1Gi | テストに割り当てられたメモリの量（値は GB 単位）です。 |
| タイムアウト | 30m | テストが終了するまでの期間。 |
| 推奨期間 | 15m | アドビは、この時間を超えないようにテストを書き込むことをお勧めします。 |

>[!NOTE]
>
> さらに多くのリソースが必要な場合は、カスタマーケアケースを作成し、ユースケースについて説明してください。アドビのチームがお客様のリクエストを確認し、適切な支援を提供します。

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

Docker イメージでは、追加のテスト出力（スクリーンショット、ビデオなど）を生成し、それらを環境変数 `REPORTS_PATH` で指定されたパスに保存する場合があります。`REPORTS_PATH` の下にあるファイルはすべて、テスト結果のアーカイブに含まれます。

デフォルトでアドビが提供するテストサンプルは、失敗したテストのスクリーンショットを作成します。

ヘルパー関数を使用して、テストのスクリーンショットを作成できます。

* JavaScript：[takeScreenshot コマンド](https://github.com/adobe/aem-project-archetype/blob/develop/src/main/archetype/ui.tests/test-module/lib/commons.js)
* Java：[コマンド](https://github.com/adobe/aem-test-samples/blob/aem-cloud/ui-selenium-webdriver/test-module/src/main/java/com/adobe/cq/cloud/testing/ui/java/ui/tests/lib/Commands.java)

UI テストの実行中にテスト結果アーカイブが作成された場合は、[**カスタム UI テスト**&#x200B;手順](/help/implementing/cloud-manager/deploy-code.md)の下にある「`Download Details`」ボタンを使用して、Cloud Manager からダウンロードできます。

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

## Cypress 固有の詳細

>[!NOTE]
>
>この節は、選択されたテストインフラストラクチャが Cypress の場合にのみ適用されます。

### HTTP プロキシの設定

Docker コンテナのエントリポイントは、の値を確認する必要があります `PROXY_HOST` 環境変数。

この値が空の場合は、追加の手順は必要なく、HTTP プロキシを使用せずにテストを実行する必要があります。

空でない場合、エントリポイントスクリプトでは次の処理を行う必要があります。

1. UI テストを実行するための HTTP プロキシ接続を設定する。 これを行うには、 `HTTP_PROXY` 次の値を使用して作成された環境変数。
   * プロキシホスト（が提供） `PROXY_HOST` 変数
   * プロキシポート（が提供） `PROXY_HTTPS_PORT` または `PROXY_HTTP_PORT` 変数（値が空でない変数が使用されます）
2. HTTP プロキシへの接続時に使用する CA 証明書を設定します。 場所は次のように提供されます `PROXY_CA_PATH` 変数。
   * これは、次を書き出すことで実現できます `NODE_EXTRA_CA_CERTS` 環境変数。
3. HTTP プロキシの準備が整うまで待ちます。
   * 準備状況を確認するために、環境変数を確認します。 `PROXY_HOST`, `PROXY_OBSERVABILITY_PORT`, `PROXY_RETRY_ATTEMPTS` および `PROXY_RETRY_DELAY` を使用できます。
   * cURL リクエストを使用して確認できます。その際に、必ず cURL を `Dockerfile`.

実装例は、にある Cypress サンプルテストモジュールのエントリポイントにあります [GitHub。](https://github.com/adobe/aem-test-samples/blob/aem-cloud/ui-cypress/test-module/run.sh)

## 再生者固有の詳細

>[!NOTE]
>
> この節は、選択したテストインフラストラクチャが Playwright の場合にのみ適用されます。

### HTTP プロキシの設定

>[!NOTE]
>
> この例では、Chrome がプロジェクトブラウザーとして使用されていると仮定します。

Cypress と同様、テストでは空でない場合に HTTP プロキシを使用する必要があります `PROXY_HOST` 環境変数が指定されています。

それには、次の変更を行う必要があります。

#### Dockerfile

cURL と `libnss3-tools`。これは次を提供します `certutil.`

```dockerfile
RUN apt -y update \
    && apt -y --no-install-recommends install curl libnss3-tools \
    && rm -rf /var/lib/apt/lists/*
```

#### エントリポイントスクリプト

大文字と小文字を区別して bash スクリプトを含める `PROXY_HOST` 環境変数が提供されており、次の操作を実行します。

1. などのプロキシ関連変数の書き出し `HTTP_PROXY` および `NODE_EXTRA_CA_CERTS`
2. 使用方法 `certutil` chromium のプロキシ CA 証明書をインストールするには
3. HTTP プロキシの準備が整うまで待ちます（または失敗したら終了します）。

実装例：

```bash
# setup proxy environment variables and CA certificate
if [ -n "${PROXY_HOST:-}" ]; then
  if [ -n "${PROXY_HTTPS_PORT:-}" ]; then
    export HTTP_PROXY="https://${PROXY_HOST}:${PROXY_HTTPS_PORT}"
  elif [ -n "${PROXY_HTTP_PORT:-}" ]; then
    export HTTP_PROXY="http://${PROXY_HOST}:${PROXY_HTTP_PORT}"
  fi
  if [ -n "${PROXY_CA_PATH:-}" ]; then
    echo "installing certificate"
    mkdir -p $HOME/.pki/nssdb
    certutil -d sql:$HOME/.pki/nssdb -A -t "CT,c,c" -n "EaaS Client Proxy Root" -i $PROXY_CA_PATH
    export NODE_EXTRA_CA_CERTS=${PROXY_CA_PATH}
  fi
  if [ -n "${PROXY_OBSERVABILITY_PORT:-}" ] && [ -n "${HTTP_PROXY:-}" ]; then
    echo "waiting for proxy"
    curl --silent  --retry ${PROXY_RETRY_ATTEMPTS:-3} --retry-connrefused --retry-delay ${PROXY_RETRY_DELAY:-10} \
      --proxy ${HTTP_PROXY} --proxy-cacert ${PROXY_CA_PATH:-""} \
      ${PROXY_HOST}:${PROXY_OBSERVABILITY_PORT}
    if [ $? -ne 0 ]; then
      echo "proxy is not ready"
      exit 1
    fi
  fi
fi
```

#### 再生の設定

再生設定を変更します（例：）。 `playwright.config.js`）に設定する必要があります。 `HTTP_PROXY` 環境変数が設定されています。

実装例：

```javascript
const proxyServer = process.env.HTTP_PROXY || ''
```

```javascript
// enable proxy if set
if (proxyServer !== '') {
 cfg.use.proxy = {
  server: proxyServer,
 }
}
```

## UI テストのローカルでの実行 {#run-ui-tests-locally}

Cloud Manager パイプラインで UI テストをアクティブ化する前に、UI テストを[AEM as a Cloud Service SDK](/help/implementing/developing/introduction/aem-as-a-cloud-service-sdk.md) に対してローカルで実行するか、実際の AEM as a Cloud Service インスタンスに対してローカルで実行することをお勧めします。

### Cypress テストサンプル {#cypress-sample}

1. シェルを開き、リポジトリ内の `ui.tests/test-module` フォルダーに移動します

1. Cypress およびその他の前提条件のインストール

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

1. 次のいずれかのコマンドでテストを実行します

   ```shell
   npm test              # Using default Cypress browser
   npm run test-chrome   # Using Google Chrome browser
   npm run test-firefox  # Using Firefox browser
   ```

>[!NOTE]
>
>ログファイルは、リポジトリの `target/` フォルダーに保存されます。
>
>詳しくは、[AEM テストサンプルのリポジトリ](https://github.com/adobe/aem-test-samples/blob/aem-cloud/ui-cypress/test-module/README.md)を参照してください。

### JavaScript WebdriverIO テストサンプル {#javascript-sample}

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
>* これにより、スタンドアロンの Selenium インスタンスが起動し、それに対するテストが実行されます。
>* ログファイルは、リポジトリの `target/reports` フォルダーに保存されます。
>* テストでは ChromeDriver の最新リリースがテスト用に自動的にダウンロードされるので、最新バージョンの Chrome を使用していることを確認する必要があります。
>
>詳しくは、[AEM プロジェクトアーキタイプのリポジトリ](https://github.com/adobe/aem-project-archetype/blob/develop/src/main/archetype/ui.tests/README.md)を参照してください。

### Java Selenium WebDriver テストサンプル {#java-sample}

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
>ログファイルは、リポジトリの `target/reports` フォルダーに保存されます。
>
>詳しくは、[AEM テストサンプルのリポジトリ](https://github.com/adobe/aem-test-samples/blob/aem-cloud/ui-selenium-webdriver/README.md)を参照してください。
