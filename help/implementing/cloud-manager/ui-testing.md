---
title: UI テスト
description: カスタム UI テストは、カスタムアプリケーションの UI テストを作成して自動的に実行できるオプション機能です
exl-id: 3009f8cc-da12-4e55-9bce-b564621966dd
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Developer
source-git-commit: 7d86ec9cd7cc283082da44111ad897a5aa548f58
workflow-type: tm+mt
source-wordcount: '2664'
ht-degree: 69%

---


# UI テスト {#ui-testing}

>[!CONTEXTUALHELP]
>id="aemcloud_nonbpa_uitesting"
>title="UI テスト"
>abstract="カスタム UI テストは、アプリケーションの UI テストを作成して自動的に実行できるオプション機能です。UI テストは、言語とフレームワークを幅広く選択できるように Docker イメージにパッケージ化された Selenium ベースのテストです。 Java や Maven、Node や WebDriver.io、Selenium に基づいて構築されたその他のフレームワークやテクノロジーなど。"

カスタム UI テストは、アプリケーションの UI テストを作成して自動的に実行できるオプション機能です。

## 概要 {#custom-ui-testing}

AEM には、[Cloud Manager 品質ゲート](/help/implementing/cloud-manager/custom-code-quality-rules.md)の統合スイートが用意されており、カスタムアプリケーションをスムーズに更新できるようになっています。特に、IT テストゲートでは、AEM API を使用したカスタムテストの作成と自動化に既に対応しています。

UI テストは、言語とフレームワーク（Cypress、Selenium、Java と Maven、JavaScript など）を幅広く選択できるように、Docker イメージにパッケージ化されています。また、[AEM プロジェクトアーキタイプ](https://experienceleague.adobe.com/ja/docs/experience-manager-core-components/using/developing/archetype/overview)を使用すると、UI テストプロジェクトを容易に生成できます。

アドビでは、リアルタイムの再読み込みと自動待機が利用でき、時間の節約やテスト中の生産性の向上に役立つ、Cypress の使用をお勧めします。また、Cypress はシンプルで直感的な構文を提供し、テストを初めて行うユーザーでも学習と使用が容易になります。

UI テストは、[**カスタム UI テスト**](/help/implementing/cloud-manager/deploy-code.md) ステップで品質ゲートとして実行します。[&#x200B; 実稼動パイプライン &#x200B;](/help/implementing/cloud-manager/configuring-pipelines/configuring-production-pipelines.md) では必須で、[&#x200B; 実稼動以外のパイプライン &#x200B;](/help/implementing/cloud-manager/configuring-pipelines/configuring-non-production-pipelines.md) ではオプションです。 回帰や新しい機能を含む UI テストでは、エラーが検出、報告されます。

Java で記述された HTTP テストであるカスタム機能テストとは異なり、UI テストは Docker イメージにすることができます。 テストは、「UI テストの作成 [&#x200B; の節で定義されている規則に従う限り、任意の言語で記述でき &#x200B;](#building-ui-tests) す。

>[!TIP]
>
>アドビでは、[AEM テストサンプルのリポジトリ](https://github.com/adobe/aem-test-samples/tree/aem-cloud/ui-cypress)で提供されているコードに従って、UI テストに Cypress を使用することをお勧めします。
> 
>アドビでは、JavaScript と WebdriverIO（[AEM プロジェクトアーキタイプ](https://github.com/adobe/aem-project-archetype/tree/master/src/main/archetype/ui.tests)）および Java と WebDriver（[AEM テストサンプルのリポジトリ](https://github.com/adobe/aem-test-samples/tree/aem-cloud/ui-selenium-webdriver)）に基づく UI テストモジュールの例も提供しています。

## UI テストの基本を学ぶ {#get-started-ui-tests}

この節では、Cloud Manager で実行用の UI テストの設定に必要な手順について説明します。

1. 使用するテストフレームワークを決定します。

   * Cypress（デフォルト）の場合は、[AEM テストサンプルのリポジトリ](https://github.com/adobe/aem-test-samples/tree/aem-cloud/ui-cypress)のサンプルコードを使用するか、Cloud Manager リポジトリの `ui.tests` フォルダーに自動的に生成されるサンプルコードを使用します。

   * Playwright の場合は、[AEM テストサンプルのリポジトリ](https://github.com/adobe/aem-test-samples/tree/aem-cloud/ui-playwright)からサンプルコードを使用します。

   * Webdriver.IO の場合は、[AEM テストサンプルのリポジトリ](https://github.com/adobe/aem-test-samples/tree/aem-cloud/ui-wdio)からサンプルコードを使用します。

   * Selenium WebDriver の場合は、[AEM テストサンプルのリポジトリ](https://github.com/adobe/aem-test-samples/tree/aem-cloud/ui-selenium-webdriver)からサンプルコードを使用します。

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

最も簡単な方法は、[Maven アセンブリプラグイン &#x200B;](https://maven.apache.org/plugins/maven-assembly-plugin/) を設定して Docker ビルドコンテキストアーカイブを作成し、それに適切な分類子を割り当てることです。

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

アセンブリ記述子は、`.tar.gz` タイプのアーカイブを作成するようにプラグインに指示し、そのアーカイブに `ui-test-docker-context` 分類子を割り当てます。さらに、そのアーカイブに含める必要のある次のファイルがリストされます。

* `Dockerfile`：Docker イメージの作成に必須
* `wait-for-grid.sh` スクリプト：目的は後述のとおり
* 実際の UI テスト：`test-module` フォルダー内に Node.js プロジェクトで実装

また、アセンブリ記述子は、UI テストのローカル実行中に生成される可能性のある一部のファイルを除外します。これにより、アーカイブのサイズが小さくなり、ビルドが高速になります。

Cloud Managerは、デプロイメントパイプライン中に Docker ビルドコンテキストアーカイブを自動的に取得して、テストイメージをビルドします。 最終的に、Cloud Managerは Docker イメージを実行して、アプリケーションに対する UI テストを実行します。

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

>[!IMPORTANT]
>
>プロジェクトにこの行が含まれていない場合、UI テストをオプトインするには、このファイルを編集します。
>
>ファイルには、「DO NOT MODIFY *という行が含まれている場合があ* ます。 これは古いテンプレートやサンプルからの従来の警告であり、Cloud Manager UI テストに必要なオプトイン編集の実行をブロック *しません*。 アドバイスを無視しても問題ありません。 つまり、オプトイン手順に従う場合（例えば、`assembly-ui-test-docker-context.xml` を含める場合 `pom.xml`、*プロジェクトで* と `testing.properties` を編集できます。

アドビが指定したサンプルを使用する場合：

* [AEM プロジェクトアーキタイプ](https://github.com/adobe/aem-project-archetype/tree/master/src/main/archetype/ui.tests)に基づいて生成された JavaScript ベースの `ui.tests` フォルダーの場合、以下のコマンドを実行して必要な設定を追加できます。

  ```shell
  echo "ui-tests.version=1" > testing.properties
  
  if ! grep -q "testing.properties" "assembly-ui-test-docker-context.xml"; then
    awk -v line='                <include>testing.properties</include>' '/<include>wait-for-grid.sh<\/include>/ { printf "%s\n%s\n", $0, line; next }; 1' assembly-ui-test-docker-context.xml > assembly-ui-test-docker-context.xml.new && mv assembly-ui-test-docker-context.xml.new assembly-ui-test-docker-context.xml
  fi
  ```

* アドビが提供する Cypress および Java Selenium のテストサンプルには、既にオプトインフラグが設定されています。

## UI テストの記述 {#writing-ui-tests}

この節では、UI テストを含んだ Docker イメージが従う必要がある規則について説明します。Docker イメージは、前の節で説明した Docker ビルドコンテキストから作成されます。

### 環境変数 {#environment-variables}

フレームワークに応じて、実行時に次の環境変数が Docker イメージに渡されます。

>[!NOTE]
>
> これらの値は、パイプラインの実行中に自動的に設定されるので、パイプライン変数として手動で設定する必要はありません。

| 変数 | 例 | 説明 | テストフレームワーク |
|----------------------------|----------------------------------|----------------------------------------------------------------------------------------------------|---------------------|
| `SELENIUM_BASE_URL` | `http://my-ip:4444` | Selenium サーバーの URL | Selenium のみ |
| `SELENIUM_BROWSER` | `chrome` | Selenium サーバーで使用されるブラウザー実装 | Selenium のみ |
| `AEM_AUTHOR_URL` | `http://my-ip:4502/context-path` | AEM オーサーインスタンスの URL | すべて |
| `AEM_AUTHOR_USERNAME` | `admin` | AEM オーサーインスタンスにログインするためのユーザー名 | すべて |
| `AEM_AUTHOR_PASSWORD` | `admin` | AEM オーサーインスタンスにログインするためのパスワード | すべて |
| `AEM_PUBLISH_URL` | `http://my-ip:4503/context-path` | AEM パブリッシュインスタンスの URL | すべて * |
| `AEM_PUBLISH_USERNAME` | `admin` | AEM パブリッシュインスタンスにログインするためのユーザー名 | すべて * |
| `AEM_PUBLISH_PASSWORD` | `admin` | AEM パブリッシュインスタンスにログインするためのパスワード | すべて * |
| `REPORTS_PATH` | `/usr/src/app/reports` | テスト結果の XML レポートを保存する必要があるパス | すべて |
| `UPLOAD_URL` | `http://upload-host:9090/upload` | テストフレームワークにアクセスできるようにするためのファイルのアップロード先の URL | すべて |
| `PROXY_HOST` | `proxy-host` | テストフレームワークで使用される内部 HTTP プロキシのホスト名 | Selenium を除くすべて |
| `PROXY_HTTPS_PORT` | `8071` | HTTPS 接続のプロキシサーバーリスニングポート （空にすることができます） | Selenium を除くすべて |
| `PROXY_HTTP_PORT` | `8070` | HTTP 接続のプロキシサーバーリスニングポート （空にすることができます） | Selenium を除くすべて |
| `PROXY_CA_PATH` | `/path/to/root_ca.pem` | テストフレームワークで使用される CA 証明書へのパス | Selenium を除くすべて |
| `PROXY_OBSERVABILITY_PORT` | `8081` | プロキシサーバーの HTTP `healthcheck` ポート | Selenium を除くすべて |
| `PROXY_RETRY_ATTEMPTS` | `12` | プロキシサーバーの準備が整うまでの推奨される再試行の試行回数 | Selenium を除くすべて |
| `PROXY_RETRY_DELAY` | `5` | プロキシサーバーの準備が整うまでの推奨される再試行間の遅延 | Selenium を除くすべて |

`* these values will be empty if there is no publish instance`

アドビテストサンプルには、設定パラメーターにアクセスするためのヘルパー関数が用意されています。

Cypress：標準関数 `Cypress.env('VARIABLE_NAME')` を使用します
<!-- BOTH URLs are 404 JavaScript: See the [`lib/config.js`](https://github.com/adobe/aem-project-archetype/blob/develop/src/main/archetype/ui.tests.wdio/test-module/lib/config.js) module
* Java: See the [`Config`](https://github.com/adobe/aem-test-samples/blob/aem-cloud/ui-selenium-webdriver/test-module/src/main/java/com/adobe/cq/cloud/testing/ui/java/ui/tests/lib/Config.java) class -->

### テストレポートの生成 {#generate-test-reports}

Docker イメージは、テストレポートを JUnit XML 形式で生成して、環境変数 `REPORTS_PATH` で指定されたパスに保存する必要があります。JUnit XML 形式は、テスト結果のレポートに広く使用されている形式です。Docker イメージで Java と Maven を使用する場合、[Maven Surefire プラグイン](https://maven.apache.org/surefire/maven-surefire-plugin/)や [Maven Failsafe プラグイン](https://maven.apache.org/surefire/maven-failsafe-plugin/) などの標準テストモジュールでは、すぐに使用できるレポートを生成できます。

Docker イメージが他のプログラミング言語またはテストランナーで実装されている場合は、選択したツールのドキュメントを参照して、JUnit XML レポートの生成方法を確認してください。

>[!NOTE]
>
>UI テスト手順の結果は、テストレポートに基づいてのみ評価されます。 テストの実行に合わせてレポートを生成するようにしてください。
>
>エラーを STDERR に記録したり、ゼロ以外の終了コードを返すのではなく、アサーションを使用してください。そうしない場合、デプロイメントパイプラインが正常に実行されます。
>
>テストの実行中に HTTP プロキシが使用された場合、結果には `request.log` ファイルが含まれます。

### 前提条件 {#prerequisites}

* Cloud Manager でのテストは、技術管理者ユーザーを使用して実行されます。

>[!NOTE]
>
>ローカルマシンから機能テストを実行する場合は、管理者のような権限を持つユーザーを作成して、同じ動作を実現します。

* 機能テストの範囲を定義するコンテナ化されたインフラストラクチャは、次の境界によって制限されます。

| タイプ | 値 | 説明 |
|----------------------|-------|-----------------------------------------------------------------------|
| CPU | 2.0 | テスト実行ごとに確保される CPU 時間の量です。 |
| メモリ | 1Gi | テストに割り当てられたメモリの容量。 値は GB 単位です。 |
| タイムアウト | 30m | テストの実行時間。 |
| 推奨期間 | 15m | Adobeでは、テストをこの制限時間内に保つことをお勧めします。 |

* ターゲットのオーサー/パブリッシュが IP許可リストに加えるで保護されている場合、パイプライン UI テストインフラストラクチャを許可リストに加えるする必要があります。そうしないと、UI テストが 403 Forbidden で失敗する場合があります。
[IP 許可リストに加える許可リストに加えるによる AEMaaCS での UI テストの失敗 &#x200B;](https://experienceleague.adobe.com/ja/docs/experience-cloud-kcs/kbarticles/ka-26654#) および [IP の概要 &#x200B;](/help/implementing/cloud-manager/ip-allow-lists/introduction.md) も参照してください。

>[!NOTE]
>
> さらに多くのリソースが必要な場合は、カスタマーケアケースを作成し、ユースケースについて説明します。Adobeがリクエストを確認し、適切な支援を提供します。

## Selenium 固有の詳細

>[!NOTE]
>
>この節は、選択されたテストインフラストラクチャが Selenium の場合にのみ適用されます。

### Selenium が準備完了するまで待ちます {#waiting-for-selenium}

テストを開始する前に、Selenium サーバーが実行状態にあることを Docker イメージ側で確認する必要があります。Selenium サービスの準備が完了するまで、次の 2 段階の手順で待機します。

1. `SELENIUM_BASE_URL` 環境変数から Selenium サービスの URL を読み取ります。
1. Selenium API で公開されている[ステータスエンドポイント](https://github.com/SeleniumHQ/docker-selenium/#waiting-for-the-grid-to-be-ready)に対して定期的にポーリングを行います。

Selenium のステータスエンドポイントが肯定的な応答を返したら、テストを開始できます。

Adobeの UI テストサンプルでは、`wait-for-grid.sh` を使用します。 Docker の開始時に実行され、グリッドの準備が整った後でのみテストを開始します。


### スクリーンショットとビデオのキャプチャ {#capture-screenshots}

Docker イメージでは、追加のテスト出力（スクリーンショット、ビデオなど）を生成し、それらを環境変数 `REPORTS_PATH` で指定されたパスに保存する場合があります。`REPORTS_PATH` の下にあるファイルはすべて、テスト結果のアーカイブに含まれます。

デフォルトでアドビが提供するテストサンプルは、失敗したテストのスクリーンショットを作成します。

ヘルパー関数を使用して、テストのスクリーンショットを作成できます。

<!-- BOTH URLS ARE 404
* JavaScript: [takeScreenshot command](https://github.com/adobe/aem-project-archetype/blob/develop/src/main/archetype/ui.tests/test-module/lib/commons.js)
* Java: [Commands](https://github.com/adobe/aem-test-samples/blob/aem-cloud/ui-selenium-webdriver/test-module/src/main/java/com/adobe/cq/cloud/testing/ui/java/ui/tests/lib/Commands.java) -->

UI テストの実行中にテスト結果アーカイブが作成された場合は、`Download Details` カスタム UI テスト [**手順** の下の「](/help/implementing/cloud-manager/deploy-code.md) 定」ボタンをクリックして、Cloud Managerからダウンロードできます。

### ファイルのアップロード {#upload-files}

テストでは、場合によって、テスト中のアプリケーションにファイルをアップロードする必要があります。テストに対する Selenium デプロイメントの柔軟性を維持するため、Selenium に直接アセットをアップロードすることはできません。 ファイルをアップロードするには、代わりに次の手順を実行する必要があります。

1. `UPLOAD_URL` 環境変数で指定された URL にファイルをアップロードします。
   * アップロードは、マルチパートフォームを含んだ 1 つの POST リクエストで実行する必要があります。
   * このマルチパートフォームには、1 つのファイルフィールドが必要です。
   * `curl -X POST ${UPLOAD_URL} -F "data=@file.txt"` と同じ。
   * このような HTTP リクエストを実行する方法については、Docker イメージで使用されているプログラミング言語のドキュメントやライブラリを参照してください。

   <!-- BOTH URLS ARE 404
   * The Adobe test samples provide helper functions for uploading files:
     * JavaScript: See the [getFileHandleForUpload](https://github.com/adobe/aem-project-archetype/blob/develop/src/main/archetype/ui.tests/test-module/lib/wdio.commands.js) command.
     * Java: See the [FileHandler](https://github.com/adobe/aem-test-samples/blob/aem-cloud/ui-selenium-webdriver/test-module/src/main/java/com/adobe/cq/cloud/testing/ui/java/ui/tests/lib/FileHandler.java) class. -->

1. アップロードが成功した場合、リクエストは `200 OK` タイプの `text/plain` 応答を返します。
   * この応答の内容は不透明なファイルハンドルです。
   * `<input>` 要素のファイルパスの代わりにこのハンドルを使用して、アプリケーション内のアップロードファイルをテストできます。

## Cypress 固有の詳細

>[!NOTE]
>
>この節は、テストインフラストラクチャとして Cypress を選択した場合にのみ適用されます。

### HTTP プロキシの設定

Docker コンテナのエントリポイントでは、`PROXY_HOST` 環境変数の値を確認する必要があります。

この値が空の場合は、追加の手順は必要なく、HTTP プロキシを使用せずにテストを実行する必要があります。

空でない場合は、エントリポイントスクリプトで次の操作を実行する必要があります。

1. 次の値を使用して構築された `HTTP_PROXY` 環境変数を書き出すことで、UI テストを実行するための HTTP プロキシ接続を設定します。
   * `PROXY_HOST` 変数によって提供されるプロキシホスト
   * プロキシポート。`PROXY_HTTPS_PORT` または変数 `PROXY_HTTP_PORT` よって指定されます（値が空でない変数が使用されます）
2. HTTP プロキシへの接続時に使用する CA 証明書を設定します。 その場所は、`PROXY_CA_PATH` 変数によって提供されます。
   * 環境変数 `NODE_EXTRA_CA_CERTS` 書き出します。
3. HTTP プロキシの準備が整うまで待機します。
   * 準備状況を確認するには、環境変数 `PROXY_HOST`、`PROXY_OBSERVABILITY_PORT`、`PROXY_RETRY_ATTEMPTS` および `PROXY_RETRY_DELAY` を使用できます。
   * cURL リクエストを使用して確認できます。その場合は、必ず `Dockerfile` に cURL をインストールしてください。

実装例は、[GitHub](https://github.com/adobe/aem-test-samples/blob/aem-cloud/ui-cypress/test-module/run.sh) の Cypress サンプルテストモジュールのエントリポイントにあります。

## Playwright 固有の詳細

>[!NOTE]
>
> この節は、選択したテストインフラストラクチャが `Playwright` の場合にのみ適用されます。

### HTTP プロキシの設定

>[!NOTE]
>
> この例では、AdobeはChromeがプロジェクトブラウザーとして使用されていることを前提としています。

Cypress と同様に、空でない `PROXY_HOST` 環境変数が設定されている場合、テストでは HTTP プロキシを使用する必要があります。

その際は、以下の点を編集する必要があります。

#### Dockerfile

`certutil.` を提供する cURL と `libnss3-tools` をインストールします。

```dockerfile
RUN apt -y update \
    && apt -y --no-install-recommends install curl libnss3-tools \
    && rm -rf /var/lib/apt/lists/*
```

#### エントリポイントスクリプト

`PROXY_HOST` 環境変数が設定されている場合は、次の操作を実行する bash スクリプトを含めます。

1. `HTTP_PROXY` や `NODE_EXTRA_CA_CERTS` などのプロキシ関連の変数を書き出します
2. `certutil` を使用して、Chromium™ のプロキシ CA 証明書をインストールします。
3. HTTP プロキシの準備が整うまで待機します（失敗した場合は終了します）。

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

#### Playwright の設定

`HTTP_PROXY` 環境変数が設定されている場合にプロキシを使用するように、playwright 設定（例：`playwright.config.js`）を変更します。

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

>[!NOTE]
>
> 実装例は、[GitHub](https://github.com/adobe/aem-test-samples/tree/aem-cloud/ui-playwright) の Playwright サンプルテストモジュールにあります。


## UI テストのローカルでの実行 {#run-ui-tests-locally}

Cloud Manager パイプラインで UI テストをアクティブ化する前に、Adobeでは、[AEM as a Cloud Service SDK](/help/implementing/developing/introduction/aem-as-a-cloud-service-sdk.md) に対して UI テストをローカルで実行することをお勧めします。 または、実際のAEM as a Cloud Service インスタンスに対して実行します。

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
>詳しくは、[AEM テストサンプルのリポジトリを参照してください &#x200B;](https://github.com/adobe/aem-test-samples/blob/aem-cloud/ui-cypress/test-module/README.md)。

### JavaScript WebdriverIO テストサンプル {#javascript-sample}

1. シェルを開き、リポジトリの `ui.tests` フォルダーに移動します。

1. Maven を使用してテストを開始するには、次のコマンドを実行します。

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
>* このコマンドは、スタンドアロンの Selenium インスタンスを開始し、それに対するテストを実行します。
>* ログファイルは、リポジトリの `target/reports` フォルダーに保存されます。
>* テストでは ChromeDriver の最新リリースがテスト用に自動的にダウンロードされるので、最新バージョンの Chrome を使用していることを確認する必要があります。
>
>詳しくは、[AEM テストサンプルのリポジトリを参照してください &#x200B;](https://github.com/adobe/aem-test-samples/tree/aem-cloud/ui-wdio)。

### 再生テストサンプル {#playwright-sample}

1. シェルを開き、リポジトリ内の `ui.tests` フォルダーに移動します

1. Maven を使用して Docker イメージを作成するには、次のコマンドを実行します

   ```shell
   mvn clean package -Pui-tests-docker-build
   ```

1. Maven を使用してテストを開始するには、次のコマンドを実行します

   ```shell
   mvn verify -Pui-tests-docker-execution \
    -DAEM_AUTHOR_URL=https://author-<program-id>-<environment-id>.adobeaemcloud.com \
    -DAEM_AUTHOR_USERNAME=<user> \
    -DAEM_AUTHOR_PASSWORD=<password> \
    -DAEM_PUBLISH_URL=https://publish-<program-id>-<environment-id>.adobeaemcloud.com \
    -DAEM_PUBLISH_USERNAME=<user> \
    -DAEM_PUBLISH_PASSWORD=<password>
   ```

>[!NOTE]
>
>ログファイルは、リポジトリの `target/` フォルダーに保存されます。
>
>詳しくは、[AEM テストサンプルのリポジトリを参照してください &#x200B;](https://github.com/adobe/aem-test-samples/tree/aem-cloud/ui-playwright)。


### Java Selenium WebDriver テストサンプル {#java-sample}

1. シェルを開き、リポジトリ内の `ui.tests/test-module` フォルダーに移動します

1. Maven を使用してテストを開始するには、次のコマンドを実行します

   ```shell
   # Start selenium docker image
   # we mount /tmp/shared as a shared volume that will be used between selenium and the test module for uploads
   docker run -d -p 4444:4444 -v /tmp/shared:/tmp/shared selenium/standalone-chromium:latest
   
   # Run the tests using the previously started Selenium instance
   mvn verify -Pui-tests-local-execution -DSELENIUM_BASE_URL=http://<server>:4444
   ```

>[!NOTE]
>
>ログファイルは、リポジトリの `target/reports` フォルダーに保存されます。
>
>詳しくは、[AEM テストサンプルのリポジトリを参照してください &#x200B;](https://github.com/adobe/aem-test-samples/blob/aem-cloud/ui-selenium-webdriver/README.md)。
