---
title: UI テスト - Cloud Services
description: UI テスト - Cloud Services
exl-id: 3009f8cc-da12-4e55-9bce-b564621966dd
source-git-commit: 02db915e114c2af8329eaddbb868045944a3574d
workflow-type: tm+mt
source-wordcount: '1617'
ht-degree: 92%

---

# UI テスト {#ui-testing}

>[!CONTEXTUALHELP]
>id="aemcloud_nonbpa_uitesting"
>title="UI テスト"
>abstract="UI テストは、言語とフレームワークの幅広い選択肢（Java と Maven、Node と WebDriver.io、Selenium に基づいて構築されたその他のフレームワークとテクノロジーなど）を可能にするために Docker イメージにパッケージ化された Selenium ベースのテストです。Docker イメージは、標準ツールを使用して作成できますが、実行時には特定の規則に従う必要があります。Docker イメージを実行すると、Selenium サーバーが自動的にプロビジョニングされます。以下に説明する実行時規則に従うと、テストコードが Selenium サーバーにもテスト対象の AEM インスタンスにもアクセスできます。"

UI テストは、言語とフレームワークの幅広い選択肢（Java と Maven、Node と WebDriver.io、Selenium に基づいて構築されたその他のフレームワークとテクノロジーなど）を可能にするために Docker イメージにパッケージ化された Selenium ベースのテストです。Docker イメージは、標準ツールを使用して作成できますが、実行時には特定の規則に従う必要があります。Docker イメージを実行すると、Selenium サーバーが自動的にプロビジョニングされます。以下に説明する実行時規則に従うと、テストコードが Selenium サーバーにもテスト対象の AEM インスタンスにもアクセスできます。

>[!NOTE]
> このページで説明する UI テストを、2021 年 2 月 10 日より前に作成されたステージパイプラインと実稼動パイプラインで使用するには更新が必要となります。
> 詳しくは、 [Cloud Manager の CI/CD パイプライン](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md) パイプラインの設定について詳しくは、を参照してください。

## カスタム UI テスト {#custom-ui-testing}

AEM では、Cloud Manager 統合スイートの品質ゲートを顧客に提供して、アプリケーションをスムーズに更新できるようにしています。特に、IT テストゲートを使用すると、AEM API を使用する独自のテストを作成および自動化できます。

カスタム UI テスト機能は [オプション機能](#customer-opt-in) これにより、お客様は、アプリケーションの UI テストを作成し、自動的に実行できます。 UI テストは、言語とフレームワークの幅広い選択肢（Java と Maven、Node と WebDriver.io、Selenium に基づいて構築されたその他のフレームワークとテクノロジーなど）を可能にするために Docker イメージにパッケージ化された Selenium ベースのテストです。UI の構築方法と UI テストの作成方法について詳しく学ぶことができます。また、AEM プロジェクトアーキタイプを使用すると、UI テストプロジェクトを容易に生成できます。

ユーザーは、（GIT 経由で）カスタムテストや、UI のテストスイートを作成できます。UI テストは、各 Cloud Manager パイプラインの特定の品質ゲートの一部として、それぞれの手順およびフィードバック情報を使用して実行されます。リグレッションや新機能を含む UI テストは、顧客の状況に応じてエラーを検出し、報告することができます。

顧客 UI テストは、「カスタム UI テスト」の実稼動パイプラインで自動的に実行されます。

UI テストは、Java で記述された HTTP テストのカスタム機能テストとは異なり、[UI テストの作成](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/test-results/ui-testing.html?lang=ja#building-ui-tests)で定義されている規則に従う限り、任意の言語で記述されたテストを含む Docker イメージにすることができます。

>[!NOTE]
>[AEM プロジェクトのアーキタイプ](https://github.com/adobe/aem-project-archetype/tree/master/src/main/archetype/ui.tests)で提供されている構造と言語&#x200B;*（js と wdio）*&#x200B;を基にして作業を開始することをお勧めします。

### 顧客オプトイン {#customer-opt-in}

UI テストを作成して実行するには、UI テスト用の maven サブモジュール（UI テストサブモジュールの pom.xml ファイルの隣）の下のコードリポジトリーにファイルを追加して「オプトイン」し、構築された `tar.gz` ファイルのルートにこのファイルがあることを確認する必要があります。

*ファイル名*：`testing.properties`

*目次*：`ui-tests.version=1`

これが構築された `tar.gz` ファイルに含まれていない場合、UI テストの構築と実行はスキップされます

追加するには `testing.properties` ビルドアーティファクトにファイルを追加し、 `include` ～に関する声明 `assembly-ui-test-docker-context.xml` ファイル（ UI テストサブモジュール内） プロジェクトにこの行が含まれていない場合、UI テストをオプトインするには、このファイルを編集する必要があります。 ファイルに編集しないように指示する行が含まれている場合は、その通知を無視してください。

    ```
    [...]
    &lt;includes>
    &lt;include>Dockerfile&lt;/include>
    &lt;include>wait-for-grid.sh&lt;/include>
    &lt;include>testing.properties&lt;/include> &lt;! - opt-in test module in Cloud Manager -->
    &lt;/includes>
    [...]
    ```

>[!NOTE]
>2021 年 2 月 10 日より前に作成された実稼動用パイプラインの場合、ここで説明した UI テストを使用するには、更新が必要となります。つまり、変更がない場合でも、実稼動パイプラインを編集し、UI から「**保存**」をクリックする必要があります。
>様々なタイプのパイプライン設定の詳細については、[CI/CD パイプラインの設定](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/configure-pipeline.html?lang=ja#using-cloud-manager)を参照してください。

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

ビルドでは、0 または 1 つのアーカイブが生成されます。 アーカイブがゼロの場合、テストステップはデフォルトで合格します。 ビルドで複数のアーカイブが生成される場合、どのアーカイブが非決定的に選択されます。

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

### ファイルをアップロード {#upload-files}

テストでは、場合によって、テスト対象のアプリケーションにファイルをアップロードする必要があります。テストに対する Selenium デプロイメントの柔軟性を維持するため、Selenium に直接アセットをアップロードすることはできません。代わりに、以下の中間手順を経て、ファイルをアップロードします。

1. `UPLOAD_URL` 環境変数で指定された URL にファイルをアップロードします。アップロードは、マルチパートフォームを含んだ 1 つの POST リクエストで実行する必要があります。このマルチパートフォームには、1 つのファイルフィールドが必要です。これは `curl -X POST ${UPLOAD_URL} -F "data=@file.txt"` と同等です。このような HTTP リクエストを実行する方法については、Docker イメージで使用されているプログラミング言語のドキュメントやライブラリを参照してください。
2. アップロードが成功した場合、リクエストは `text/plain` タイプの `200 OK` 応答を返します。この応答の内容は不透明なファイルハンドルです。`<input>` 要素のファイルパスの代わりにこのハンドルを使用して、アプリケーション内のアップロードファイルをテストできます。
