---
title: UI テスト - Cloud Services
description: UI テスト - Cloud Services
exl-id: 3009f8cc-da12-4e55-9bce-b564621966dd
source-git-commit: f6c700f82bc5a1a3edf05911a29a6e4d32dd3f72
workflow-type: ht
source-wordcount: '1087'
ht-degree: 100%

---

# UI テスト {#ui-testing}

>[!CONTEXTUALHELP]
>id="aemcloud_nonbpa_uitesting"
>title="UI テスト"
>abstract="UI テストは、言語とフレームワークの幅広い選択肢（Java と Maven、Node と WebDriver.io、Selenium に基づいて構築されたその他のフレームワークとテクノロジーなど）を可能にするために Docker イメージにパッケージ化された Selenium ベースのテストです。Docker イメージは、標準ツールを使用して作成できますが、実行時には特定の規則に従う必要があります。Docker イメージを実行すると、Selenium サーバーが自動的にプロビジョニングされます。以下に説明する実行時規則に従うと、テストコードが Selenium サーバーにもテスト対象の AEM インスタンスにもアクセスできます。"

UI テストは、言語とフレームワークの幅広い選択肢（Java と Maven、Node と WebDriver.io、Selenium に基づいて構築されたその他のフレームワークとテクノロジーなど）を可能にするために Docker イメージにパッケージ化された Selenium ベースのテストです。Docker イメージは、標準ツールを使用して作成できますが、実行時には特定の規則に従う必要があります。Docker イメージを実行すると、Selenium サーバーが自動的にプロビジョニングされます。以下に説明する実行時規則に従うと、テストコードが Selenium サーバーにもテスト対象の AEM インスタンスにもアクセスできます。

>[!NOTE]
> このページで説明する UI テストを、2021 年 2 月 10 日より前に作成されたステージパイプラインと実稼動パイプラインで使用するには更新が必要となります。
> パイプラインの設定については、[CI/CD パイプラインの設定](/help/implementing/cloud-manager/configure-pipeline.md)を参照してください。

## UI テストの作成 {#building-ui-tests}

UI テストは、Maven プロジェクトで生成された Docker ビルドコンテキストから作成されます。Cloud Manager は、Docker ビルドコンテキストを使用して、実際の UI テストを含んだ Docker イメージを生成します。手短に言えば、Maven プロジェクトでは Docker ビルドコンテキストが生成され、Docker ビルドコンテキストでは、UI テストを含んだ Docker イメージの作成方法が記述されます。

この節では、UI テストプロジェクトをリポジトリーに追加するために必要な手順について説明します。時間がない場合やプログラミング言語の特別な要件がない場合は、[AEM プロジェクトアーキタイプ](https://github.com/adobe/aem-project-archetype)で UI テストプロジェクトを自動的に生成できます。

### Docker ビルドコンテキストの生成 {#generate-docker-build-context}

Docker ビルドコンテキストを生成するには、次の処理を行う Maven モジュールが必要です。

- `Dockerfile`と、テストを含んだ Docker イメージの作成に必要なその他のすべてのファイルを格納したアーカイブを作成する。
- アーカイブに `ui-test-docker-context` 分類子をタグ付けする。

これを行うには、[Maven アセンブリプラグイン](http://maven.apache.org/plugins/maven-assembly-plugin/)を設定して Docker ビルドコンテキストアーカイブを作成し、それに適切な分類子を割り当てるのが最も簡単です。

様々なテクノロジーとフレームワークを使用して UI テストを作成できますが、この節では、プロジェクトが次のようにレイアウトされていることを前提としています。

```
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

この実行は、`assembly-ui-test-docker-context.xml` に含まれている命令（プラグインの専門用語では「アセンブリ記述子」と呼ばれます）に基づいてアーカイブを作成するように Maven アセンブリプラグインに指示します。アセンブリ記述子では、アーカイブに含める必要のあるすべてのファイルがリストアップされます。

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

- `Dockerfile`：Docker イメージの作成に必須。
- `wait-for-grid.sh` スクリプト：目的は後述のとおり。
- 実際の UI テスト：`test-module` フォルダー内に Node.js プロジェクトで実装。

また、アセンブリ記述子は、UI テストのローカル実行中に生成される可能性のある一部のファイルを除外します。これにより、アーカイブのサイズが小さくなり、ビルドが高速になります。

Docker ビルドコンテキストを含んだアーカイブが Cloud Manager で自動的に選択され、テストを含んだ Docker イメージがデプロイメントパイプライン中に作成されます。最終的に、Cloud Manager は Docker イメージを実行して、アプリケーションに対する UI テストを実行します。

## UI テストの書き込み {#writing-ui-tests}

この節では、UI テストを含んだ Docker イメージが従う必要がある規則について説明します。Docker イメージは、前の節で説明した Docker ビルドコンテキストから作成されます。

### 環境変数 {#environment-variables}

実行時に次の環境変数が Docker イメージに渡されます。

| 変数 | 例 | 説明 |
|---|---|---|
| `SELENIUM_BASE_URL` | `http://my-ip:4444` | Selenium サーバーの URL |
| `SELENIUM_BROWSER` | `chrome`、`firefox` | Selenium サーバーで使用されるブラウザー実装 |
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
2. Selenium API で公開されている[ステータスエンドポイント](https://github.com/SeleniumHQ/docker-selenium/#waiting-for-the-grid-to-be-ready)に対して定期的にポーリングを行います。

Selenium のステータスエンドポイントが肯定的な応答を返したら、いよいよテストを開始できます。

### テストレポートの生成 {#generate-test-reports}

Docker イメージは、テストレポートを JUnit XML 形式で生成して、環境変数 `REPORTS_PATH` で指定されたパスに保存する必要があります。JUnit XML 形式は、テスト結果のレポートに広く使用されている形式です。Docker イメージで Java と Maven が使用される場合、[Maven Surefire プラグイン](https://maven.apache.org/surefire/maven-surefire-plugin/)と [Maven Failsafe プラグイン](https://maven.apache.org/surefire/maven-failsafe-plugin/)の両方が使用されます。Docker イメージが他のプログラミング言語またはテストランナーで実装されている場合は、選択したツールのドキュメントを参照して、JUnit XML レポートの生成方法を確認してください。

### ファイルのアップロード {#upload-files}

テストでは、場合によって、テスト対象のアプリケーションにファイルをアップロードする必要があります。テストに対する Selenium デプロイメントの柔軟性を維持するため、Selenium に直接アセットをアップロードすることはできません。代わりに、以下の中間手順を経て、ファイルをアップロードします。

1. `UPLOAD_URL` 環境変数で指定された URL にファイルをアップロードします。アップロードは、マルチパートフォームを含んだ 1 つの POST リクエストで実行する必要があります。このマルチパートフォームには、1 つのファイルフィールドが必要です。これは `curl -X POST ${UPLOAD_URL} -F "data=@file.txt"` と同等です。このような HTTP リクエストを実行する方法については、Docker イメージで使用されているプログラミング言語のドキュメントやライブラリを参照してください。
2. アップロードが成功した場合、リクエストは `text/plain` タイプの `200 OK` 応答を返します。この応答の内容は不透明なファイルハンドルです。`<input>` 要素のファイルパスの代わりにこのハンドルを使用して、アプリケーション内のアップロードファイルをテストできます。
