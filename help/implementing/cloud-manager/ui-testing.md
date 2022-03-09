---
title: UI テスト
description: カスタム UI テストは、カスタムアプリケーションの UI テストを作成して自動的に実行できるオプションの機能です
exl-id: 3009f8cc-da12-4e55-9bce-b564621966dd
source-git-commit: a7555507f4fb0fb231e27d7c7a6413b4ec6b94e6
workflow-type: tm+mt
source-wordcount: '1401'
ht-degree: 49%

---


# UI テスト {#ui-testing}

>[!CONTEXTUALHELP]
>id="aemcloud_nonbpa_uitesting"
>title="UI テスト"
>abstract="カスタム UI テストは、アプリケーションの UI テストを作成して自動的に実行できるオプションの機能です。 UI テストは、言語とフレームワークの幅広い選択肢（Java と Maven、Node と WebDriver.io、Selenium に基づいて構築されたその他のフレームワークとテクノロジーなど）を可能にするために Docker イメージにパッケージ化された Selenium ベースのテストです。"

カスタム UI テストは、アプリケーションの UI テストを作成して自動的に実行できるオプションの機能です。

>[!NOTE]
> このページで説明する UI テストを、2021 年 2 月 10 日より前に作成されたステージパイプラインと実稼動パイプラインで使用するには更新が必要となります。
> 詳しくは、 [Cloud Manager の CI/CD パイプライン](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md) パイプラインの設定について詳しくは、を参照してください。

## 概要 {#custom-ui-testing}

AEMは、 [Cloud Manager の品質ゲート](/help/implementing/cloud-manager/custom-code-quality-rules.md) カスタムアプリケーションのスムーズな更新を確保する。 特に、AEM API を使用したカスタムテストの作成と自動化を IT テストゲートで実行しています。

UI テストは、言語とフレームワークの幅広い選択肢（Java と Maven、Node と WebDriver.io、Selenium に基づいて構築されたその他のフレームワークとテクノロジーなど）を可能にするために Docker イメージにパッケージ化された Selenium ベースのテストです。さらに、 [AEMプロジェクトアーキタイプ](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/overview.html?lang=ja)

UI テストは、Cloud Manager の各パイプラインの特定の品質ゲートの一部として、 [専用 **カスタム UI テスト** 手順](/help/implementing/cloud-manager/deploy-code.md) 回帰や新しい機能を含む UI テストでは、エラーの検出とレポートが可能です。

Java で記述された HTTP テストであるカスタム機能テストとは異なり、UI テストは、の節で定義された規則に従う限り、任意の言語で記述されたテストを含む Docker イメージにすることができます [UI テストを構築しています。](#building-ui-tests)

>[!TIP]
>
>Adobeでは、 [AEMプロジェクトアーキタイプ。](https://github.com/adobe/aem-project-archetype/tree/master/src/main/archetype/ui.tests)

### 顧客オプトイン {#customer-opt-in}

Cloud Manager で UI テストを作成して実行するには、リポジトリにファイルを追加して、この機能をオプトインする必要があります。

* ファイル名は `testing.properties` にする必要があります。

* ファイルの内容は、 `ui-tests.version=1`.
* ファイルは、UI テスト用の Maven サブモジュールの下で、 `pom.xml` UI テストサブモジュールのファイル。
* ファイルは、ビルドのルートにある必要があります `tar.gz` ファイル。

このファイルが存在しない場合、UI テストの作成と実行はスキップされます。

を含めるには、以下を実行します。 `testing.properties` ファイルをビルドアーティファクトに追加し、 `include` 内の `assembly-ui-test-docker-context.xml` ファイル。

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
>プロジェクトにこの行が含まれていない場合、UI テストをオプトインするには、このファイルを編集する必要があります。 ファイルに編集しないように指示する行がある場合は、そのアドバイスを無視してください。

>[!NOTE]
>
>2021 年 2 月 10 日より前に作成された実稼動用パイプラインの場合、ここで説明した UI テストを使用するには、更新が必要となります。つまり、変更がない場合でも、実稼動パイプラインを編集し、UI から「**保存**」をクリックする必要があります。
>様々なタイプのパイプライン設定の詳細については、[CI/CD パイプラインの設定](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/configure-pipeline.html?lang=ja#using-cloud-manager)を参照してください。

## UI テストの作成 {#building-ui-tests}

Maven プロジェクトは、Docker ビルドコンテキストを生成します。 この Docker ビルドコンテキストでは、UI テストを含む Docker 画像を作成する方法を説明します。Cloud Manager ユーザーは、実際の UI テストを含む Docker 画像を生成するためにこの UI テストを含む Docker 画像を作成します。

この節では、UI テストプロジェクトをリポジトリに追加するために必要な手順について説明します。

>[!TIP]
>
>この [AEM Project Archetype](https://github.com/adobe/aem-project-archetype) では、プログラミング言語に関する特別な要件を持たない UI テストプロジェクトを生成できます。

### Docker ビルドコンテキストの生成 {#generate-docker-build-context}

Docker ビルドコンテキストを生成するには、次の処理を行う Maven モジュールが必要です。

* `Dockerfile`と、テストを含んだ Docker イメージの作成に必要なその他のすべてのファイルを格納したアーカイブを作成する。
* アーカイブに `ui-test-docker-context` 分類子をタグ付けする。

これをおこなう最も簡単な方法は、 [Maven Assembly Plugin](http://maven.apache.org/plugins/maven-assembly-plugin/) Docker ビルドコンテキストアーカイブを作成し、それに適切な分類子を割り当てるため。

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

この実行は、Maven Assembly Plugin に対し、 `assembly-ui-test-docker-context.xml`と呼ばれる **アセンブリ記述子** プラグインの用語。 アセンブリ記述子では、アーカイブに含める必要のあるすべてのファイルがリストアップされます。

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

アセンブリ記述子は、`.tar.gz` タイプのアーカイブを作成するようにプラグインに指示し、そのアーカイブに `ui-test-docker-context` 分類子を割り当てます。さらに、アーカイブに含める必要があるファイルのリストが次のように表示されます。

* A `Dockerfile`（Docker イメージの作成に必須）
* この `wait-for-grid.sh` 以下に説明するスクリプト
* 実際の UI テスト。 `test-module` フォルダー

また、アセンブリ記述子は、UI テストのローカル実行中に生成される可能性のある一部のファイルを除外します。これにより、アーカイブのサイズが小さくなり、ビルドが高速になります。

Docker ビルドコンテキストを含むアーカイブは、Cloud Manager によって自動的に取得され、デプロイメントパイプライン中のテストを含む Docker イメージが作成されます。 最終的に、Cloud Manager は Docker イメージを実行して、アプリケーションに対する UI テストを実行します。

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
| `AEM_AUTHOR_USERNAME` | `admin` | AEMオーサーインスタンスにログインするためのユーザー名 |
| `AEM_AUTHOR_PASSWORD` | `admin` | AEM オーサーインスタンスにログインするためのパスワード |
| `AEM_PUBLISH_URL` | `http://my-ip:4503/context-path` | AEM パブリッシュインスタンスの URL |
| `AEM_PUBLISH_USERNAME` | `admin` | AEMパブリッシュインスタンスにログインするためのユーザー名 |
| `AEM_PUBLISH_PASSWORD` | `admin` | AEM パブリッシュインスタンスにログインするためのパスワード |
| `REPORTS_PATH` | `/usr/src/app/reports` | テスト結果の XML レポートの保存先となるパス |
| `UPLOAD_URL` | `http://upload-host:9090/upload` | Selenium からファイルにアクセスできるようにするためのファイルアップロード先の URL |

### Selenium の準備が完了するのを待機中 {#waiting-for-selenium}

テストを開始する前に、Selenium サーバーが実行状態にあることを Docker イメージ側で確認する必要があります。Selenium サービスの待機は、2 段階のプロセスです。

1. `SELENIUM_BASE_URL` 環境変数から Selenium サービスの URL を読み取ります。
1. Selenium API で公開されている[ステータスエンドポイント](https://github.com/SeleniumHQ/docker-selenium/#waiting-for-the-grid-to-be-ready)に対して定期的にポーリングを行います。

Selenium のステータスエンドポイントが肯定的な応答で応答すると、テストを開始できます。

### テストレポートの生成 {#generate-test-reports}

Docker イメージは、テストレポートを JUnit XML 形式で生成して、環境変数 `REPORTS_PATH` で指定されたパスに保存する必要があります。JUnit XML 形式は、テストの結果を報告するために広く使用されている形式です。 Docker イメージで Java と Maven が使用される場合、[Maven Surefire プラグイン](https://maven.apache.org/surefire/maven-surefire-plugin/)と [Maven Failsafe プラグイン](https://maven.apache.org/surefire/maven-failsafe-plugin/)の両方が使用されます。

Docker イメージが他のプログラミング言語やテストランナーで実装されている場合は、JUnit XML レポートの生成方法に関して、選択したツールのドキュメントを参照してください。

### ファイルをアップロード {#upload-files}

テストでは、テスト対象のアプリケーションにファイルをアップロードする必要が生じる場合があります。 テストに対する Selenium のデプロイメントを柔軟に保つために、Selenium に直接アセットをアップロードすることはできません。 ファイルをアップロードするには、代わりに次の手順を実行する必要があります。

1. `UPLOAD_URL` 環境変数で指定された URL にファイルをアップロードします。
   * アップロードは、マルチパートフォームを含んだ 1 つの POST リクエストで実行する必要があります。
   * このマルチパートフォームには、1 つのファイルフィールドが必要です。
   * これは `curl -X POST ${UPLOAD_URL} -F "data=@file.txt"` と同等です。
   * このような HTTP リクエストを実行する方法については、Docker イメージで使用されているプログラミング言語のドキュメントやライブラリを参照してください。
1. アップロードが成功した場合、リクエストは `200 OK` タイプの `text/plain` 応答を返します。
   * この応答の内容は不透明なファイルハンドルです。
   * `<input>` 要素のファイルパスの代わりにこのハンドルを使用して、アプリケーション内のアップロードファイルをテストできます。
