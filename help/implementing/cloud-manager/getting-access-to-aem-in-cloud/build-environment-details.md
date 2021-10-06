---
title: ビルド環境の詳細
description: ビルド環境の詳細 - Cloud Services
exl-id: a4e19c59-ef2c-4683-a1be-3ec6c0d2f435
source-git-commit: 9ae940fb0149a76277aba49a75abfb8b83305788
workflow-type: tm+mt
source-wordcount: '957'
ht-degree: 98%

---

# ビルド環境について {#understanding-build-environment}

## ビルド環境の詳細 {#build-environment-details}

Cloud Manager では、専用のビルド環境を使用して、コードのビルドおよびテストを行います。この環境には次のような特性があります。

* ビルド環境は Linux ベースで、Ubuntu 18.04 から派生しています。
* Apache Maven 3.6.0 がインストールされています。
* インストールされる Java のバージョンは、Oracle JDK 8u202、Azul Zulu 8u292、Oracle JDK 11.0.2 および Azul Zulu 11.0.11 です。
* 必要な追加のシステムパッケージが、次のようにいくつかインストールされています。

   * bzip2
   * unzip
   * libpng
   * imagemagick
   * graphicsmagick

* [後述されている通り](#installing-additional-system-packages)、これ以外にも、ビルド時にパッケージがインストールされる場合があります。
* すべてのビルドは、Pristine 環境で実行されます。ビルドコンテナは実行から次回の実行までの間、状態を保持しません。
* Maven は常に次の 3 つのコマンドで実行します。

   * `mvn --batch-mode org.apache.maven.plugins:maven-dependency-plugin:3.1.2:resolve-plugins`
   * `mvn --batch-mode org.apache.maven.plugins:maven-clean-plugin:3.1.0:clean -Dmaven.clean.failOnError=false`
   * `mvn --batch-mode org.jacoco:jacoco-maven-plugin:prepare-agent packageco-maven-plugin:prepare-agent package`
* Maven は、settings.xml ファイルを使用してシステムレベルで設定されます。このファイルには、`adobe-public` というプロファイルを使用したアドビの公開&#x200B;**アーティファクト**&#x200B;リポジトリーが自動的に含まれています（詳しくは、[アドビの公開 Maven リポジトリー](https://repo1.maven.org/)を参照してください）。

>[!NOTE]
>Cloud Manager では、`jacoco-maven-plugin` の特定のバージョンは定義されませんが、`0.7.5.201505241946` 異常のバージョンを使用する必要があります。

### 特定の Java バージョンの使用 {#using-java-support}

デフォルトでは、プロジェクトは、Oracle 8 JDK を使用して Cloud Manager ビルドプロセスでビルドされます。代替 JDK を使用する場合は、2 つの選択肢があります。Maven ツールチェーンを使用する方法と、Maven 実行プロセス全体で代替 JDK バージョンを選択する方法です。

#### Maven ツールチェーン {#maven-toolchains}

[Maven ツールチェーンプラグイン](https://maven.apache.org/plugins/maven-toolchains-plugin/)では、ツールチェーン対応の Maven プラグインのコンテキストで使用する特定の JDK（または&#x200B;*ツールチェーン*）をプロジェクトで選択できます。それには、プロジェクトの `pom.xml` ファイルでベンダーとバージョン値を指定します。`pom.xml` ファイルのサンプルセクションは次のとおりです。

```
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

この方法を使用する場合、Maven 自体は引き続きデフォルトの JDK（Oracle 8）を使用して実行されます。したがって、Apache Maven Enforcer Plugin などのプラグインによる Java バージョンの確認や強制は機能しないので、そのようなプラグインは使用しないでください。

現在利用可能なベンダー／バージョンの組み合わせは次のとおりです。

* oracle 1.8
* oracle 1.11
* oracle 11
* sun 1.8
* sun 1.11
* sun 11
* azul 1.8
* azul 1.11
* azul 8

#### Maven 実行の代替 JDK バージョン {#alternate-maven-jdk-version}

また、Maven 実行全体の JDK として Azul 8 または Azul 11 を選択することもできます。この場合は、ツールチェーンオプションとは異なり、ツールチェーン設定も指定される場合を除き、すべてのプラグインに使用される JDK が変更されます。ツールチェーン設定が指定される場合は、そのツールチェーン設定が引き続きツールチェーン対応 Maven プラグインに適用されます。その結果、[Apache Maven Enforcer Plugin](https://maven.apache.org/enforcer/maven-enforcer-plugin/) を使用して Java バージョンを確認および強制することができます。

これをおこなうには、パイプラインで使用される Git リポジトリブランチに `.cloudmanager/java-version` という名前のファイルを作成します。 このファイルの内容は 11 か 8 のどちらかにすることができます。その他の値は無視されます。11 を指定した場合は、Azul 11 が使用されます。8 を指定した場合は、Azul 8 が使用されます。

>[!NOTE]
>Cloud Manager の今後のリリース（現時点では 2021 年 10 月の見込み）で、デフォルトの JDK が Azul 11 に変更されます。Java 11 と互換性のないプロジェクトでは、この切り替えの影響を受けないように、できるだけ早く、このファイルの内容を 8 にしてください。


## 環境変数 {#environment-variables}

### 標準環境変数 {#standard-environ-variables}

場合によっては、プログラムやパイプラインに関する情報に基づいてビルドプロセスを変更する必要があります。

例えば、gulp のようなツールを使用して、ビルド時の JavaScript の縮小が行われている場合、ステージと実稼働用とは異なる、開発環境用のビルド時の縮小レベルを使用したくなる場合があります。

これをサポートするために、Cloud Manager は、これらの標準環境変数を各実行のビルドコンテナに追加します。

| **変数名** | **定義** |
|---|---|
| CM_BUILD | 常に「true」に設定 |
| ブランチ | 実行用に設定されたブランチ |
| CM_PIPELINE_ID | 数値パイプライン識別子 |
| CM_PIPELINE_NAME | パイプライン名 |
| CM_PROGRAM_ID | 数値プログラム識別子 |
| CM_PROGRAM_NAME | プログラム名 |
| ARTIFACTS_VERSION | ステージまたは実稼動パイプラインの場合、Cloud Manager で生成された合成バージョン |
| CM_AEM_PRODUCT_VERSION | リリース名 |

### パイプライン変数 {#pipeline-variables}

場合によっては、顧客のビルドプロセスが、特定の設定変数に依存している可能性があります。これらの変数は Git リポジトリーに配置するのに適していない場合や、同じブランチを使用するパイプライン実行間で変える必要が出る場合があります。

Cloud Manager では、これらの変数を Cloud Manager API または Cloud Manager CLI を介してパイプラインごとに設定できます。変数は、プレーンテキストとして保存することも、保存時に暗号化することもできます。どちらの場合も、変数はビルド環境内で環境変数として使用可能になり、変数は `pom.xml` ファイル内または他のビルドスクリプト内から参照できます。

CLI を使用して変数を設定するには、次のようなコマンドを実行します。

`$ aio cloudmanager:set-pipeline-variables PIPELINEID --variable MY_CUSTOM_VARIABLE test`

現在の変数は次のとおりです。

`$ aio cloudmanager:list-pipeline-variables PIPELINEID`

変数名に使用できるのは、英数字と下線（_）のみです。慣例では、名前はすべて大文字である必要があります。パイプラインあたりの変数は最大 200 個という制限があります。それぞれの名前は 100 文字未満、それぞれの値は文字列型変数の場合は 2048 文字未満、secretString 型変数の場合は 500 文字未満にする必要があります。

通常、`Maven pom.xml` ファイル内で使用する場合は、次のような構文を使用して、これらの変数を Maven プロパティにマップすると便利です。

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

すべての機能を実装するにあたり、一部のビルドでは追加のシステムパッケージをインストールする必要があります。例えば、Python や Ruby のスクリプトが呼び出されるビルドでは、当然、適切な言語インタープリターをインストールすることが必要となります。これを行うには、[exec-maven-plugin](https://www.mojohaus.org/exec-maven-plugin/) を呼び出して、APT を起動します。この実行は通常、Cloud Manager 専用の Maven プロファイルにラップされます。例えば、Python は次のようにインストールします：

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

同じ方法を、RubyGems の `gem` や Python パッケージの `pip` など、特定の言語用のパッケージのインストールにも使用できます。

>[!NOTE]
>この方法でシステムパッケージをインストールしても、Adobe Experience Manager の実行に使用されているランタイム環境にはインストール&#x200B;**されません**。AEM 環境にシステムパッケージをインストールする必要がある場合は、アドビ担当者にお問い合わせください。
