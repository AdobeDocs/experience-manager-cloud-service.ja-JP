---
title: UIテスト —Cloud Services
description: UIテスト —Cloud Services
translation-type: tm+mt
source-git-commit: bf3fb5178bc2ae72e19ecc1de82b08fac5089ecf
workflow-type: tm+mt
source-wordcount: '971'
ht-degree: 0%

---


# UIテスト{#ui-testing}

>[!CAUTION]
>
>この機能はまだ一般には利用できません。


UIテストは、言語とフレームワーク（JavaとMaven、NodeとWebDriver.io、またはSeleniumに基づいて構築されたその他のフレームワークとテクノロジーなど）で幅広い選択を可能にするために、Dockerイメージにパッケージ化されたSeleniumベースのテストです。 Dockerイメージは、標準ツールを使用して作成できますが、実行時には特定の規則に従う必要があります。 Dockerイメージを実行すると、Seleniumサーバーが自動的にプロビジョニングされます。 以下に説明するランタイム規則に従って、テストコードでSeleniumサーバーとテスト対象のAEMインスタンスの両方にアクセスできます。

## UIテストの構築{#building-ui-tests}

UIテストは、Mavenプロジェクトで生成されたDockerビルドコンテキストから作成されます。 Cloud Managerは、Dockerのビルドコンテキストを使用して、実際のUIテストを含むDocker画像を生成します。 要約すると、MavenプロジェクトでDockerビルドコンテキストが生成され、Dockerビルドコンテキストでは、UIテストを含むDockerイメージの作成方法が説明されます。

この節では、UIテストプロジェクトをリポジトリに追加するために必要な手順について説明します。 急いでいる場合、またはプログラミング言語に特別な要件がない場合は、[AEM Project Archetype](https://github.com/adobe/aem-project-archetype)でUIテストプロジェクトを生成できます。

### Dockerビルドコンテキストの生成{#generate-docker-build-context}

Dockerビルドコンテキストを生成するには、次の機能を持つMavenモジュールが必要です。

- `Dockerfile`と、テストでDockerイメージを作成するのに必要なその他すべてのファイルを含むアーカイブを作成します。
- アーカイブに`ui-test-docker-context`分類子のタグを付けます。

これを実行する最も簡単な方法は、[Maven Assembly Plugin](http://maven.apache.org/plugins/maven-assembly-plugin/)を設定してDockerビルドコンテキストアーカイブを作成し、それに適切な分類子を割り当てることです。

様々なテクノロジーとフレームワークを使用してUIテストを作成できますが、この節では、プロジェクトが次のような方法でレイアウトされていることを前提としています。

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

`pom.xml`ファイルはMavenのビルドを処理します。 次追加のようなMavenアセンブリプラグインの実行。

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

この実行は、Maven Assembly Pluginに対し、プラグインの用語で「アセンブリ記述子」と呼ばれる`assembly-ui-test-docker-context.xml`に含まれる命令に基づいてアーカイブを作成するよう指示します。 アセンブリ記述子は、アーカイブに含まれる必要のあるすべてのファイルをリストします。

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

アセンブリ記述子は、プラグインに対して`.tar.gz`型のアーカイブの作成を指示し、`ui-test-docker-context`分類子を割り当てます。 さらに、アーカイブに含める必要のあるファイルがリストされます。

- `Dockerfile`。Dockerイメージの作成に必須です。
- `wait-for-grid.sh`スクリプト。このスクリプトの目的は以下のとおりです。
- `test-module`フォルダー内のNode.jsプロジェクトによって実装された、実際のUIテスト。

アセンブリ記述子は、UIテストをローカルで実行中に生成される可能性のある一部のファイルも除外します。 これにより、アーカイブのサイズが小さくなり、ビルドが高速になります。

Dockerのビルドコンテキストを含むアーカイブはCloud Managerによって自動的に取得され、デプロイメントパイプライン中にテストを含むDockerイメージが作成されます。 最終的に、Cloud ManagerはDocker画像を実行して、アプリケーションに対するUIテストを実行します。

## UIテストの書き込み{#writing-ui-tests}

この節では、UIテストを含むDockerイメージが従う必要がある規則について説明します。 Dockerイメージは、前の節で説明したDockerビルドコンテキストから構築されます。

### 環境変数 {#environment-variables}

実行時に、次の環境変数がDockerイメージに渡されます。

| 変数 | 例 | 説明 |
|---|---|---|
| `SELENIUM_BASE_URL` | `http://my-ip:4444` | SeleniumサーバーのURL |
| `SELENIUM_BROWSER` | `chrome`、`firefox` | Seleniumサーバーで使用されるブラウザー実装 |
| `AEM_AUTHOR_URL` | `http://my-ip:4502/context-path` | AEM作成者インスタンスのURL |
| `AEM_AUTHOR_USERNAME` | `admin` | AEM作成者インスタンスにログインするためのユーザー名 |
| `AEM_AUTHOR_PASSWORD` | `admin` | AEMオーサーインスタンスにログインするためのパスワードです |
| `AEM_PUBLISH_URL` | `http://my-ip:4503/context-path` | AEM発行インスタンスのURL |
| `AEM_PUBLISH_USERNAME` | `admin` | AEM発行インスタンスにログインするユーザー名 |
| `AEM_PUBLISH_PASSWORD` | `admin` | AEM発行インスタンスにログインするためのパスワード |
| `REPORTS_PATH` | `/usr/src/app/reports` | テスト結果のXMLレポートを保存する必要があるパス |
| `UPLOAD_URL` | `http://upload-host:9090/upload` | Seleniumにアクセスできるようにするためにファイルをアップロードする必要があるURL |

### セレンの準備ができるのを待っています{#waiting-for-selenium}

テスト開始を行う前に、Seleniumサーバが起動および実行されていることを確認するのはDockerイメージの責任です。 Seleniumサービスの待機は、次の2つの手順で行います。

1. `SELENIUM_BASE_URL`環境変数からSeleniumサービスのURLを読み取ります。
2. Selenium APIによって公開された[ステータスエンドポイント](https://github.com/SeleniumHQ/docker-selenium/#waiting-for-the-grid-to-be-ready)に対して定期的にポーリングを行います。

Seleniumの状態エンドポイントがポジティブな応答で応答すると、テストは最終的に開始できます。

### テストレポートを生成{#generate-test-reports}

Dockerイメージは、JUnit XML形式のテストレポートを生成し、環境変数`REPORTS_PATH`で指定されたパスに保存する必要があります。 JUnit XML形式は、テストの結果をレポートするための広範な形式です。 DockerイメージがJavaとMavenを使用する場合、[Maven Surefireプラグイン](https://maven.apache.org/surefire/maven-surefire-plugin/)と[Mavenフェールセーフプラグイン](https://maven.apache.org/surefire/maven-failsafe-plugin/)の両方が使用されます。 Dockerイメージが他のプログラミング言語またはテストランナーと共に実装されている場合は、選択したツールのドキュメントを参照し、JUnit XMLレポートの生成方法を確認してください。

### ファイルのアップロード(#upload-files)

テストでは、テスト対象のアプリにファイルをアップロードする必要がある場合があります。 テストに対するSeleniumの導入を柔軟に維持するため、Seleniumに直接アセットをアップロードすることはできません。 代わりに、ファイルのアップロードは次のような中間的な手順に従います。

1. `UPLOAD_URL`環境変数で指定されたURLにファイルをアップロードします。 アップロードは、マルチパート形式の1つのPOST要求で実行する必要があります。 マルチパートフォームには、1つのファイルフィールドが必要です。 これは`curl -X POST ${UPLOAD_URL} -F "data=@file.txt"`と同じです。 このようなHTTP要求を実行する方法については、Dockerイメージで使用されているプログラミング言語のドキュメントとライブラリを参照してください。
2. アップロードが成功した場合、リクエストは`text/plain`型の`200 OK`応答を返します。 応答の内容は不透明なファイルハンドルです。 `<input>`要素のファイルパスの代わりにこのハンドルを使用して、アプリケーション内のファイルのアップロードをテストできます。
