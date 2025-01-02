---
title: Cloud Manager のビルド環境
description: Cloud Manager のビルド環境と、コードを作成およびテストする方法について説明します。
exl-id: a4e19c59-ef2c-4683-a1be-3ec6c0d2f435
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
source-git-commit: 3bc9ec12de604818f6be1c0717566a5f16c6a7b9
workflow-type: ht
source-wordcount: '777'
ht-degree: 100%

---


# ビルド環境 {#build-environment}

Cloud Manager のビルド環境と、コードを作成およびテストする方法について説明します。

## ビルド環境の詳細 {#build-environment-details}

Cloud Manager では、専用のビルド環境を使用して、コードのビルドおよびテストを行います。

* ビルド環境は Linux ベースで、Ubuntu 22.04 から派生しています。
* Apache Maven 3.9.4 がインストールされています。
   * アドビでは、ユーザーに [HTTP ではなく HTTPS を使用するように Maven リポジトリを更新](#https-maven)することをお勧めします。
* <!-- OLD --> インストールされる Java バージョンは、Oracle JDK 11.0.22 と Oracle JDK 8u401 です。
<!-- NEW but needed to be removed 12/5/24 * The Java versions installed are Oracle JDK 11.0.22, Oracle JDK 17.0.10, and Oracle JDK 21.0.4. -->
<!-- OLD --> * **重要：**&#x200B;デフォルトでは、JAVA_HOME 環境変数は `/usr/lib/jvm/jdk1.8.0_401` に設定されています。これには、Oracle JDK 8u401 が含まれています。AEM Cloud プロジェクトで JDK 11 を使用するには、このデフォルトを上書きする必要があります。詳しくは、Maven JDK バージョンの設定の節を参照してください。
<!-- NEW but needed to be removed 12/5/24 * **IMPORTANT:** By default, the `JAVA_HOME` environment variable is set to `/usr/lib/jvm/jdk1.8.0_401`, which contains Oracle JDK 8u401. ***This default should be overridden for AEM Cloud Projects to use JDK 21 (preferred), 17, or 11***. See the [Setting the Maven JDK Version](#alternate-maven-jdk-version) section for more details. -->
* 必要に応じてインストールされる追加のシステムパッケージが、次のようにいくつかあります。
   * `bzip2`
   * `unzip`
   * `libpng`
   * `imagemagick`
   * `graphicsmagick`
* [追加のシステムパッケージのインストール](#installing-additional-system-packages)の節で説明されているように、ビルド時にその他のパッケージがインストールされる場合があります。
* 各ビルドはクリーンな環境で実行され、ビルドコンテナは実行間で状態を保持しません。
* Maven は常に次の 3 つのコマンドで実行されます。
   * `mvn --batch-mode org.apache.maven.plugins:maven-dependency-plugin:3.1.2:resolve-plugins`
   * `mvn --batch-mode org.apache.maven.plugins:maven-clean-plugin:3.1.0:clean -Dmaven.clean.failOnError=false`
   * `mvn --batch-mode org.jacoco:jacoco-maven-plugin:prepare-agent package`
* Maven は、`settings.xml` ファイルを使用してシステムレベルで設定されます。このファイルには、`adobe-public` というプロファイルを使用したアドビの公開アーティファクトリポジトリが自動的に含まれています（詳しくは、[アドビの公開 Maven リポジトリ](https://repo1.maven.org/)を参照してください）。

>[!NOTE]
>
>Cloud Manager では、`jacoco-maven-plugin` の特定のバージョンは定義されませんが、`0.7.5.201505241946` 異常のバージョンを使用する必要があります。

## HTTPS Maven リポジトリ {#https-maven}

Cloud Manager [リリース 2023.10.0](/help/implementing/cloud-manager/release-notes/2023/2023-10-0.md) では、Maven 3.8.8 へのアップデートを含む、ビルド環境へのローリングアップデートが開始されました（リリース 2023.12.0 で完了）。Maven 3.8.1 で導入された重要な変更は、潜在的な脆弱性を軽減することを目的としたセキュリティ強化でした。具体的には、[Maven リリースノート](https://maven.apache.org/docs/3.8.1/release-notes.html#cve-2021-26291)で説明するように、Maven では安全でないすべての `http://*` ミラーをデフォルトで無効にするようになりました。

このセキュリティ強化の結果、一部のユーザーには、ビルド手順で、特に安全でない HTTP 接続を使用する Maven リポジトリからアーティファクトをダウンロードする際に問題が発生する場合があります。

アップデートされたバージョンでスムーズなエクスペリエンスを実現するために、アドビでは、ユーザーが Mavenリポジトリを更新して HTTP ではなく HTTPS を使用することをお勧めします。この調整は、業界でセキュアな通信プロトコルへの移行が進むのに合わせて行われ、安全で信頼性の高いビルドプロセスを維持するのに役立ちます。

<!-- OLD below -->

### 特定の Java バージョンの使用

Cloud Manager のビルドプロセスでは、デフォルトで Oracle 8 JDK を使用してプロジェクトを作成しますが、AEM Cloud Service のお客様は Maven 実行 JDK バージョンを 11 に設定する必要があります。

<!-- OLD below -->

#### Maven JDK バージョンの設定

アドビでは、`.cloudmanager/java-version file` で、Maven 実行全体の JDK バージョンを `11` に設定することをお勧めします。

これを行うには、パイプラインで使用される Git リポジトリ分岐に `.cloudmanager/java-version` というファイルを作成します。`11` というテキストのみが含まれるようにファイルを編集します。Cloud Manager は値 `8` も受け入れますが、このバージョンは AEM Cloud Service プロジェクトではサポートされなくなりました。その他の値は無視されます。`11` を指定した場合は、Oracle 11 が使用され、`JAVA_HOME` 環境変数が `/usr/lib/jvm/jdk-11.0.22` に設定されます。

<!-- NEW but needed to be removed 12/5/24 ### Use a specific Java version {#using-java-support}

The Cloud Manager build process uses the Oracle 8 JDK to build projects by default, but AEM Cloud Service customers should set the Maven execution JDK version to 21 (preferred), 17, or 11.

#### Set the Maven JDK version {#alternate-maven-jdk-version}

Adobe recommends setting the Maven execution JDK version to `21` or `17` in a `.cloudmanager/java-version` file.

To do so, create a file named `.cloudmanager/java-version` in the Git repository branch used by the pipeline. Edit the file so that it contains only the text, `21` or `17`. While Cloud Manager also accepts a value of `8`, this version is no longer supported for AEM Cloud Service projects. Any other value is ignored. When `21` or `17` is specified, Oracle Java 21 or Oracle Java 17 is used and the `JAVA_HOME` environment variable is set to `/usr/lib/jvm/jdk-21` or `/usr/lib/jvm/jdk-17`.

#### Prerequisites for migrating to building with Java 21 or Java 17 {#prereq-for-building}

>[!NOTE]
>
>*When migrating your application to a new Java build version and runtime version, thoroughly test in dev and stage environments before deploying to production.
>Of special note, the following features have not yet been formally validated with Java 21 runtime: [Forms](/help/forms/home.md), [Workflows](/help/sites-cloud/authoring/workflows/overview.md), [Inbox](/help/sites-cloud/authoring/inbox.md), and [Projects](/help/sites-cloud/authoring/projects/overview.md). If your application relies on these features, ensure comprehensive testing to verify functionality.*

##### About some translation features {#translation-features}

The following features might not function correctly when building with Java 21 or Java 17, and Adobe expects to resolve them by early 2025:

* `XLIFF` (XML Localization Interchange File Format) fails when using Human Translation.  
* `I18n` (Internationalization) does not properly handle language locales Hebrew (`he`), Indonesian (`in`), and Yiddish (`yi`) due to changes in the Locale constructor in newer Java versions.

#### Runtime requirements {#runtime-requirements}

The Java 21 runtime is used for builds on Java 21, Java 17, and Java 11 starting in February 2025. To ensure compatibility, the following adjustments are necessary. 

Library updates can be applied anytime, as they remain compatible with older Java versions.

* **Minimum version of `org.objectweb.asm`:**
Update the usage of `org.objectweb.asm` to version 9.5 or higher to ensure support for newer JVM runtimes.

* **Minimum version of `org.apache.groovy`:**
Update the usage of `org.apache.groovy` to version 4.0.22 or higher to ensure support for newer JVM runtimes.

  This bundle can be indirectly included by adding third party dependencies such as the AEM Groovy Console.

* **Edit a runtime parameter:**
When running AEM locally with Java 21, the start scripts (`crx-quickstart/bin/start` or `crx-quickstart/bin/start.bat`) fail due to the `MaxPermSize` parameter. As a remedy, either remove `-XX:MaxPermSize=256M` from the script or define the environment variable `CQ_JVM_OPTS`, setting it to `-Xmx1024m -Djava.awt.headless=true`.

  Adobe plans to resolve this issue in a future release.

>[!NOTE]
>
>When `.cloudmanager/java-version` is set to `21` or `17`, the Java 21 runtime is deployed. In February or March 2025, the Java 21 runtime is planned for deployment to all customers, even if Java 11 is used to build your code. 

#### Build time requirements

The following adjustments are required to allow building the project with Java 21 and Java 17. They can be updated at any time as they are compatible with older versions of Java.

* **Minimum version of `bnd-maven-plugin`:**
Update the usage of `bnd-maven-plugin` to version 6.4.0 to ensure support for newer JVM runtimes. 

  Versions 7 or higher are not compatible with Java 11 or lower so an upgrade to that version is not recommended.

* **Minimum version of `aemanalyser-maven-plugin`:**
Update the usage of `aemanalyser-maven-plugin` to version 1.6.6 or higher to ensure support for newer JVM runtimes.

* **Minimum version of `maven-bundle-plugin`:**
Update the usage of `maven-bundle-plugin` to version 5.1.5 or higher to ensure support for newer JVM runtimes. 

  Versions 6 or higher are not compatible with Java 11 or lower so an upgrade to that version is not recommended.

* **Update dependencies in `maven-scr-plugin`:**
The `maven-scr-plugin` is not directly compatible with Java 21 or Java 17. However, descriptor files can be generated by updating the ASM dependency version in the plugin configuration, as shown in the following example:

```XML
<project>
  ...
  <build>
    ...
    <plugins>
      ...
      <plugin>
        <groupId>org.apache.felix</groupId>
        <artifactId>maven-scr-plugin</artifactId>
        <version>1.26.4</version>
        <executions>
          <execution>
            <id>generate-scr-scrdescriptor</id>
            <goals>
              <goal>scr</goal>
            </goals>
          </execution>
        </executions>
        <dependencies>
          <dependency>
            <groupId>org.ow2.asm</groupId>
            <artifactId>asm-analysis</artifactId>
            <version>9.7.1</version>
            <scope>compile</scope>
          </dependency>
        </dependencies>
      </plugin>
      ...
    </plugins>
    ...
  </build>
  ...
</project>
```
-->


## 環境変数 - 標準 {#environment-variables}

場合によっては、プログラムやパイプラインに関する情報に基づいてビルドプロセスを変更する必要があります。

例えば、gulp などのツールを使用してビルド時に JavaScript の縮小が行われる場合、様々な環境で異なる縮小レベルが望ましいことがあります。開発ビルドでは、ステージング環境や実稼動環境と比較して、より軽い縮小レベルが使用される可能性があります。

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

## 環境変数 - パイプライン {#pipeline-variables}

ビルドプロセスでは、Git リポジトリに保存すべきではない特定の設定変数が必要になる可能性があります。または、同じ分岐を使用したパイプライン実行間で、これらの変数の調整が必要になる場合があります。

詳しくは、[パイプライン変数の設定](/help/implementing/cloud-manager/configuring-pipelines/pipeline-variables.md)も参照してください。

## 追加のシステムパッケージのインストール {#installing-additional-system-packages}

すべての機能を実装するにあたり、一部のビルドでは追加のシステムパッケージが必要です。例えば、Python や Ruby のスクリプトが呼び出される可能性のあるビルドでは、適切な言語インタープリターのインストールが必要になります。このインストールプロセスは、`pom.xml` で [`exec-maven-plugin`](https://www.mojohaus.org/exec-maven-plugin/) を呼び出して APT を起動することで、管理できます。この実行は通常、Cloud Manager 専用の Maven プロファイルにラップされます。この例では、Python をインストールしています。

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
