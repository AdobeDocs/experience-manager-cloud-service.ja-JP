---
title: ビルド環境
description: Cloud Manager のビルド環境と、そこでコードがどのようにビルドされテストされるかを説明します。
exl-id: a4e19c59-ef2c-4683-a1be-3ec6c0d2f435
source-git-commit: 5f344682aa0427d46dc6ca75fe83b0071348ad83
workflow-type: ht
source-wordcount: '831'
ht-degree: 100%

---

# ビルド環境 {#build-environment}

Cloud Manager のビルド環境と、そこでコードがどのようにビルドされテストされるかを説明します。

## ビルド環境の詳細 {#build-environment-details}

Cloud Manager では、専用のビルド環境を使用して、コードのビルドおよびテストを行います。

* ビルド環境は Linux ベースで、Ubuntu 18.04 から派生しています。
* Apache Maven 3.6.0 がインストールされています。
* インストールされる Java バージョンは Oracle JDK 8u202 と Oracle JDK 11.0.2 です。
* デフォルトでは、`JAVA_HOME` 環境変数は `/usr/lib/jvm/jdk1.8.0_202` に設定されています。これには、Oracle JDK 8u202 が含まれています。詳しくは、[Maven 実行の代替 JDK バージョン](#alternate-maven-jdk-version)の節を参照してください。
* 必要に応じてインストールされる追加のシステムパッケージが、次のようにいくつかあります。

   * `bzip2`
   * `unzip`
   * `libpng`
   * `imagemagick`
   * `graphicsmagick`

* [追加のシステムパッケージのインストール](#installing-additional-system-packages)の節で説明されているように、ビルド時にその他のパッケージがインストールされる場合があります。
* すべてのビルドは、Pristine 環境で実行されます。ビルドコンテナは実行から次回の実行までの間、状態を保持しません。
* Maven は常に次の 3 つのコマンドで実行されます。

* `mvn --batch-mode org.apache.maven.plugins:maven-dependency-plugin:3.1.2:resolve-plugins`
* `mvn --batch-mode org.apache.maven.plugins:maven-clean-plugin:3.1.0:clean -Dmaven.clean.failOnError=false`
* `mvn --batch-mode org.jacoco:jacoco-maven-plugin:prepare-agent packageco-maven-plugin:prepare-agent package`
* Maven は、`settings.xml` ファイルを使用してシステムレベルで設定されます。このファイルには、`adobe-public` というプロファイルを使用したアドビの公開アーティファクトリポジトリが自動的に含まれています（詳しくは、[アドビの公開 Maven リポジトリ](https://repo1.maven.org/)を参照してください）。

>[!NOTE]
>
>Cloud Manager では、`jacoco-maven-plugin` の特定のバージョンは定義されませんが、`0.7.5.201505241946` 異常のバージョンを使用する必要があります。

### 特定の Java バージョンの使用 {#using-java-support}

デフォルトでは、プロジェクトは、Oracle 8 JDK を使用して Cloud Manager ビルドプロセスでビルドされます。代替 JDK を使用する場合は、次の 2 つの選択肢があります。

* [Maven ツールチェーンを使用する](#maven-toolchains)
* [Maven 実行プロセス全体で使用する代替 JDK バージョンを選択する](#alternate-maven-jdk-version)

#### Maven ツールチェーン {#maven-toolchains}

[Maven ツールチェーンプラグイン](https://maven.apache.org/plugins/maven-toolchains-plugin/)では、ツールチェーン対応の Maven プラグインのコンテキストで使用する特定の JDK（またはツールチェーン）をプロジェクトで選択できます。それには、プロジェクトの `pom.xml` ファイルでベンダーとバージョン値を指定します。

```xml
<plugin>
    <groupId>org.apache.maven.plugins</groupId>
    <artifactId>maven-toolchains-plugin</artifactId>
    <version>1.1</version>
    <executions>
        <execution>
            <goals>
                <goal>toolchain</goal>
            </goals>
        </execution>
    </executions>
    <configuration>
        <toolchains>
            <jdk>
                <version>11</version>
                <vendor>oracle</vendor>
            </jdk>
        </toolchains>
    </configuration>
</plugin>
```

これにより、すべてのツールチェーン対応 Maven プラグインで Oracle JDK バージョン 11 が使用されるようになります。

この方法を使用する場合、Maven 自体は引き続きデフォルト JDK（Oracle 8）を使用して実行され、`JAVA_HOME` 環境変数は変更されません。したがって、Apache Maven Enforcer Plugin などのプラグインによる Java バージョンの確認や強制は機能しないので、そのようなプラグインは使用しないでください。

現在利用可能なベンダー／バージョンの組み合わせは次のとおりです。

| ベンダー | バージョン |
|---|---|
| `oracle` | `1.8` |
| `oracle` | `1.11` |
| `oracle` | `11` |
| `sun` | `1.8` |
| `sun` | `1.11` |
| `sun` | `11` |

>[!NOTE]
>
>2022年4月以降、Oracle JDK は、AEM アプリケーションの開発と運用のためのデフォルト JDK になります。Cloud Manager のビルドプロセスは、Maven ツールチェーンで代替オプションを明示的に選択した場合でも、Oracle JDK の使用に自動的に切り替わります。詳しくは、公開後の 4月のリリースノートを参照してください。

## 環境変数 {#environment-variables}

### 標準環境変数 {#standard-environ-variables}

場合によっては、プログラムやパイプラインに関する情報に基づいてビルドプロセスを変更する必要があります。

例えば、gulp のようなツールを使用してビルド時の JavaScript の縮小が行われている場合、開発環境用にビルドする際には、ステージングや実稼働用にビルドする際とは異なる縮小レベルを使用したいことがあります。

これをサポートするために、Cloud Manager は、これらの標準環境変数を各実行のビルドコンテナに追加します。

| 変数名 | 定義 |
|---|---|
| `CM_BUILD` | 常に `true` に設定 |
| `BRANCH` | 実行用に設定されたブランチ |
| `CM_PIPELINE_ID` | 数値パイプライン識別子 |
| `CM_PIPELINE_NAME` | パイプライン名 |
| `CM_PROGRAM_ID` | 数値プログラム識別子 |
| `CM_PROGRAM_NAME` | プログラム名 |
| `ARTIFACTS_VERSION` | ステージまたは実稼動パイプラインの場合、Cloud Manager で生成された合成バージョン |
| `CM_AEM_PRODUCT_VERSION` | リリースバージョン |

### パイプライン変数 {#pipeline-variables}

お使いのビルドプロセスが、Git リポジトリに配置するのに適さない特定の設定変数に基づいている場合や、同じブランチを使用するパイプライン実行間で環境変数を変えることが必要になる場合があります。

Cloud Manager では、これらの変数を Cloud Manager API または Cloud Manager CLI を介してパイプラインごとに設定できます。変数は、プレーンテキストとして保存することも、保存時に暗号化することもできます。どちらの場合も、変数はビルド環境内で環境変数として使用可能になり、変数は `pom.xml` ファイル内または他のビルドスクリプト内から参照できます。

この CLI コマンドは変数を設定します。

```shell
$ aio cloudmanager:set-pipeline-variables PIPELINEID --variable MY_CUSTOM_VARIABLE test
```

このコマンドは、変数を一覧表示します。

```shell
$ aio cloudmanager:list-pipeline-variables PIPELINEID
```

変数名は、次の規則に従う必要があります。

* 変数には、英数字とアンダースコア（`_`）のみ使用できます。
* 名前はすべて大文字にします。
* 変数の数はパイプラインあたり最大 200 個までです。
* 名前は 100 文字未満にする必要があります。
* `string` 型変数の値は 2048 文字未満にする必要があります。
* `secretString` 型変数の値は 500 文字未満にする必要があります。

Maven `pom.xml` ファイル内で使用する場合は、通常、次のような構文を使用して、これらの変数を Maven プロパティにマッピングすると便利です。

```xml
        <profile>
            <id>cmBuild</id>
            <activation>
                <property>
                    <name>env.CM_BUILD</name>
                </property>
            </activation>
            <properties>
                <my.custom.property>${env.MY_CUSTOM_VARIABLE}</my.custom.property> 
            </properties>
        </profile>
```

## 追加のシステムパッケージのインストール {#installing-additional-system-packages}

すべての機能を実装するにあたり、一部のビルドでは追加のシステムパッケージをインストールする必要があります。例えば、Python や Ruby のスクリプトが呼び出される可能性のあるビルドでは、適切な言語インタープリターのインストールが必要になります。その場合は、`pom.xml` で [`exec-maven-plugin`](https://www.mojohaus.org/exec-maven-plugin/) を呼び出して、APT を起動します。この実行は通常、Cloud Manager 専用の Maven プロファイルにラップされます。この例では、Python をインストールしています。

```xml
        <profile>
            <id>install-python</id>
            <activation>
                <property>
                        <name>env.CM_BUILD</name>
                </property>
            </activation>
            <build>
                <plugins>
                    <plugin>
                        <groupId>org.codehaus.mojo</groupId>
                        <artifactId>exec-maven-plugin</artifactId>
                        <version>1.6.0</version>
                        <executions>
                            <execution>
                                <id>apt-get-update</id>
                                <phase>validate</phase>
                                <goals>
                                    <goal>exec</goal>
                                </goals>
                                <configuration>
                                    <executable>apt-get</executable>
                                    <arguments>
                                        <argument>update</argument>
                                    </arguments>
                                </configuration>
                            </execution>
                            <execution>
                                <id>install-python</id>
                                <phase>validate</phase>
                                <goals>
                                    <goal>exec</goal>
                                </goals>
                                <configuration>
                                    <executable>apt-get</executable>
                                    <arguments>
                                        <argument>install</argument>
                                        <argument>-y</argument>
                                        <argument>--no-install-recommends</argument>
                                        <argument>python</argument>
                                    </arguments>
                                </configuration>
                            </execution>
                        </executions>
                    </plugin>
                </plugins>
            </build>
        </profile>
```

同じ方法を、言語固有のパッケージ（RubyGems 用の `gem` や Python パッケージ用の `pip` など）のインストールにも使用できます。

>[!NOTE]
>
>この方法でシステムパッケージをインストールしても、Adobe Experience Manager の実行に使用されているランタイム環境にはインストールされません。AEM 環境にシステムパッケージをインストールする必要がある場合は、アドビ担当者にお問い合わせください。
