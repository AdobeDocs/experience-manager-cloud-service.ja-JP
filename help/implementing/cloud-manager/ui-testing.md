---
title: UI テスト
description: カスタム UI テストは、カスタムアプリケーションの UI テストを作成して自動的に実行できるオプション機能です
exl-id: 3009f8cc-da12-4e55-9bce-b564621966dd
source-git-commit: 05f9e9de0d5dbcc332466dc964e2d01569d16110
workflow-type: tm+mt
source-wordcount: '1338'
ht-degree: 100%

---


# UI テスト {#ui-testing}

>[!CONTEXTUALHELP]
>id="aemcloud_nonbpa_uitesting"
>title="UI テスト"
>abstract="カスタム UI テストは、アプリケーションの UI テストを作成して自動的に実行できるオプション機能です。UI テストは、言語とフレームワークの幅広い選択肢（Java と Maven、Node と WebDriver.io、Selenium に基づいて構築されたその他のフレームワークとテクノロジーなど）を可能にするために Docker イメージにパッケージ化された Selenium ベースのテストです。"

カスタム UI テストは、アプリケーションの UI テストを作成して自動的に実行できるオプション機能です。

## 概要 {#custom-ui-testing}

AEM には、[Cloud Manager 品質ゲート](/help/implementing/cloud-manager/custom-code-quality-rules.md)の統合スイートが用意されており、カスタムアプリケーションをスムーズに更新できるようになっています。特に、IT テストゲートでは、AEM API を使用したカスタムテストの作成と自動実行が既に行われています。

UI テストは、言語とフレームワークの幅広い選択肢（Java と Maven、Node と WebDriver.io、Selenium に基づいて構築されたその他のフレームワークとテクノロジーなど）を可能にするために Docker イメージにパッケージ化された Selenium ベースのテストです。また、[AEM プロジェクトアーキタイプ](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/overview.html?lang=ja)を使用すると、UI テストプロジェクトを容易に生成できます。

UI テストは、[専用の&#x200B;**カスタム UI テスト**&#x200B;ステップ](/help/implementing/cloud-manager/deploy-code.md)を含む Cloud Manager パイプラインごとに、特定の品質ゲートの一部として実行されます。リグレッションや新しい機能を含む UI テストでは、エラーの検出とレポートが可能です。

UI テストは、Java で記述された HTTP テストであるカスタム機能テストとは異なり、[UI テストの作成](#building-ui-tests)の節で定義されている規則に従う限り、任意の言語で記述されたテストを含む Docker イメージにすることができます。

>[!TIP]
>
>[AEM プロジェクトアーキタイプ](https://github.com/adobe/aem-project-archetype/tree/master/src/main/archetype/ui.tests)で提供される構造と言語（JavaScript および WDIO）に従うことをお勧めします。

### 顧客オプトイン {#customer-opt-in}

Cloud Manager で UI テストを作成して実行するには、リポジトリーにファイルを追加して、この機能をオプトインする必要があります。

* ファイル名は `testing.properties` にする必要があります。
* ファイルの内容は `ui-tests.version=1` にする必要があります。
* ファイルは、UI テストサブモジュールの `pom.xml` ファイルの次にある UI テストの Maven サブモジュールの下に必要です。
* ファイルは、作成された `tar.gz` ファイルのルートに必要です。

このファイルが存在しない場合、UI テストの作成と実行はスキップされます。

`testing.properties` ファイルをビルドアーティファクトに含めるには、`include` ステートメントを `assembly-ui-test-docker-context.xml` ファイルを追加します。

```xml
[...]
<includes>
    <include>Dockerfile</include>
    <include>wait-for-grid.sh</include>
    <include>testing.properties</include> <!- opt-in test module in Cloud Manager -->
</includes>
[...]
```

>[!NOTE]
>
>プロジェクトにこの行が含まれていない場合、UI テストをオプトインするには、このファイルを編集する必要があります。
>
>このファイルには、編集しないように指示する行が含まれている場合があります。これは、このファイルが、オプトイン UI テストが導入される前にプロジェクトに導入され、クライアントがファイルを編集することが想定さていなかったためです。これは無視してかまいません。

## UI テストの作成 {#building-ui-tests}

Maven プロジェクトでは、Docker ビルドコンテキストを生成します。この Docker ビルドコンテキストでは、UI テストを含んだ Docker イメージを作成する方法が記述されています。Cloud Manager はこれを使用して、実際の UI テストを含んだ Docker イメージを生成します。

この節では、UI テストプロジェクトをリポジトリーに追加するために必要な手順について説明します。

>[!TIP]
>
>[AEM プロジェクトアーキタイプ](https://github.com/adobe/aem-project-archetype)では、プログラミング言語の特別な要件がない UI テストプロジェクトを生成できます。

### Docker ビルドコンテキストの生成 {#generate-docker-build-context}

Docker ビルドコンテキストを生成するには、次の処理を行う Maven モジュールが必要です。

* `Dockerfile`と、テストを含んだ Docker イメージの作成に必要なその他のすべてのファイルを格納したアーカイブを作成する。
* アーカイブに `ui-test-docker-context` 分類子をタグ付けする。

これを行うには、[Maven アセンブリプラグイン](http://maven.apache.org/plugins/maven-assembly-plugin/)を設定して Docker ビルドコンテキストアーカイブを作成し、それに適切な分類子を割り当てるのが最も簡単です。

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

### Selenium の準備完了までの待機 {#waiting-for-selenium}

テストを開始する前に、Selenium サーバーが実行状態にあることを Docker イメージ側で確認する必要があります。Selenium サービスの準備が完了するまで、次の 2 段階の手順で待機します。

1. `SELENIUM_BASE_URL` 環境変数から Selenium サービスの URL を読み取ります。
1. Selenium API で公開されている[ステータスエンドポイント](https://github.com/SeleniumHQ/docker-selenium/#waiting-for-the-grid-to-be-ready)に対して定期的にポーリングを行います。

Selenium のステータスエンドポイントが肯定的な応答を返したら、テストを開始できます。

### テストレポートの生成 {#generate-test-reports}

Docker イメージは、テストレポートを JUnit XML 形式で生成して、環境変数 `REPORTS_PATH` で指定されたパスに保存する必要があります。JUnit XML 形式は、テスト結果のレポートに広く使用されている形式です。Docker イメージで Java と Maven を使用する場合、[Maven Surefire プラグイン](https://maven.apache.org/surefire/maven-surefire-plugin/)や [Maven Failsafe プラグイン](https://maven.apache.org/surefire/maven-failsafe-plugin/) などの標準テストモジュールでは、すぐに使用できるレポートを生成できます。

Docker イメージが他のプログラミング言語またはテストランナーで実装されている場合は、選択したツールのドキュメントを参照して、JUnit XML レポートの生成方法を確認してください。

### ファイルのアップロード {#upload-files}

テストでは、場合によって、テスト中のアプリケーションにファイルをアップロードする必要があります。テストに対する Selenium デプロイメントの柔軟性を維持するため、Selenium に直接アセットをアップロードすることはできません。ファイルをアップロードするには、代わりに次の手順を実行する必要があります。

1. `UPLOAD_URL` 環境変数で指定された URL にファイルをアップロードします。
   * アップロードは、マルチパートフォームを含んだ 1 つの POST リクエストで実行する必要があります。
   * このマルチパートフォームには、1 つのファイルフィールドが必要です。
   * これは `curl -X POST ${UPLOAD_URL} -F "data=@file.txt"` と同等です。
   * このような HTTP リクエストを実行する方法については、Docker イメージで使用されているプログラミング言語のドキュメントやライブラリを参照してください。
1. アップロードが成功した場合、リクエストは `200 OK` タイプの `text/plain` 応答を返します。
   * この応答の内容は不透明なファイルハンドルです。
   * `<input>` 要素のファイルパスの代わりにこのハンドルを使用して、アプリケーション内のアップロードファイルをテストできます。
