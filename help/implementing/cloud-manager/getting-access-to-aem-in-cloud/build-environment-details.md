---
title: ビルド環境
description: Cloud Manager のビルド環境と、そこでコードがどのようにビルドされテストされるかを説明します。
exl-id: a4e19c59-ef2c-4683-a1be-3ec6c0d2f435
source-git-commit: 54135244d7b33ba3682633b455a5538474d3146e
workflow-type: tm+mt
source-wordcount: '788'
ht-degree: 79%

---


# ビルド環境 {#build-environment}

Cloud Manager のビルド環境と、そこでコードがどのようにビルドされテストされるかを説明します。

## ビルド環境の詳細 {#build-environment-details}

Cloud Manager では、専用のビルド環境を使用して、コードのビルドおよびテストを行います。

* ビルド環境は Linux ベースで、Ubuntu 22.04 から派生しています。
* Apache Maven 3.9.4 がインストールされています。
   * アドビでは、ユーザーに [HTTP ではなく HTTPS を使用するように Maven リポジトリを更新](#https-maven)することをお勧めします。
* インストールされる Java のバージョンは、OracleJDK 11.0.22 およびOracleJDK 8u401 です。
* **重要**：デフォルトでは、 `JAVA_HOME` 環境変数はに設定されます。 `/usr/lib/jvm/jdk1.8.0_401` oracleJDK 8u401 を含む *_JDK 11 を使用するには、このデフォルト設定をAEM Cloud Projects で上書きする必要があります。_*. 詳しくは、 [Maven JDK バージョンの設定](#alternate-maven-jdk-version) の節を参照してください。
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
   * `mvn --batch-mode org.jacoco:jacoco-maven-plugin:prepare-agent package`
* Maven は、`settings.xml` ファイルを使用してシステムレベルで設定されます。このファイルには、`adobe-public` というプロファイルを使用したアドビの公開アーティファクトリポジトリが自動的に含まれています（詳しくは、[アドビの公開 Maven リポジトリ](https://repo1.maven.org/)を参照してください）。

>[!NOTE]
>
>Cloud Manager では、`jacoco-maven-plugin` の特定のバージョンは定義されませんが、使用するバージョンは `0.7.5.201505241946` 以上である必要があります。

## HTTPS Maven リポジトリ {#https-maven}

Cloud Manager [リリース 2023.10.0](/help/implementing/cloud-manager/release-notes/2023/2023-10-0.md) では、Maven 3.8.8 へのアップデートを含む、ビルド環境へのローリングアップデートが開始されました（リリース 2023.12.0 で完了）。Maven 3.8.1 で導入された重要な変更は、潜在的な脆弱性を軽減することを目的としたセキュリティ強化でした。具体的には、[Maven リリースノート](http://maven.apache.org/docs/3.8.1/release-notes.html#cve-2021-26291)で説明するように、Maven では安全でないすべての `http://*` ミラーをデフォルトで無効にするようになりました。

このセキュリティ強化の結果、一部のユーザーには、ビルド手順で、特に安全でない HTTP 接続を使用する Maven リポジトリからアーティファクトをダウンロードする際に問題が発生する場合があります。

アップデートされたバージョンでスムーズなエクスペリエンスを実現するために、アドビでは、ユーザーが Mavenリポジトリを更新して HTTP ではなく HTTPS を使用することをお勧めします。この調整は、業界でセキュアな通信プロトコルへの移行が進むのに合わせて行われ、安全で信頼性の高いビルドプロセスを維持するのに役立ちます。

### 特定の Java バージョンの使用 {#using-java-support}

デフォルトでは、プロジェクトはOracle8 JDK を使用して Cloud Manager ビルドプロセスで構築されますが、AEM Cloud Serviceのお客様は、Maven を実行するために使用する JDK バージョンをに設定することを強くお勧めします。 `11`.

#### Maven JDK バージョンの設定 {#alternate-maven-jdk-version}

Maven の実行全体の JDK バージョンをに設定することをお勧めします。 `11` 内 `.cloudmanager/java-version` ファイル。

それには、パイプラインで使用される Git リポジトリーブランチに `.cloudmanager/java-version` というファイルを作成します。ファイルを編集して、テキストのみが含まれるようにします。 `11`. Cloud Manager は `8`の場合、このバージョンはAEM Cloud Serviceプロジェクトでサポートされなくなりました。 その他の値は無視されます。条件 `11` が指定されている場合、Oracle11 が使用され、 `JAVA_HOME` 環境変数はに設定されます。 `/usr/lib/jvm/jdk-11.0.22`.

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

ドキュメントを参照してください [パイプライン変数の設定](/help/implementing/cloud-manager/configuring-pipelines/pipeline-variables.md) 詳細情報

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

これと同じ手法を使用して、言語固有のパッケージをインストールすることができます。例えば、RubyGems には `gem` を使用し、Python パッケージには `pip` を使用します。

>[!NOTE]
>
>この方法でシステムパッケージをインストールしても、Adobe Experience Manager の実行に使用されているランタイム環境にはインストールされません。AEM 環境にシステムパッケージをインストールする必要がある場合は、アドビ担当者にお問い合わせください。

>[!TIP]
>
>フロントエンドビルド環境について詳しくは、[フロントエンドパイプラインを使用したサイトの開発](/help/implementing/developing/introduction/developing-with-front-end-pipelines.md)のドキュメントを参照してください。
