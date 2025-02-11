---
title: Cloud Manager のビルド環境
description: Cloud Manager のビルド環境と、コードを作成およびテストする方法について説明します。
exl-id: a4e19c59-ef2c-4683-a1be-3ec6c0d2f435
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
source-git-commit: d5461217cfec894a922b2f476aabfc04df45d9d0
workflow-type: tm+mt
source-wordcount: '1488'
ht-degree: 100%

---


# ビルド環境 {#build-environment}

Cloud Manager のビルド環境と、コードを作成およびテストする方法について説明します。

## ビルド環境の詳細 {#build-environment-details}

Cloud Manager では、専用のビルド環境を使用して、コードのビルドおよびテストを行います。

* ビルド環境は Linux ベースで、Ubuntu 22.04 から派生しています。
* Apache Maven 3.9.4 がインストールされています。
   * アドビでは、ユーザーに [HTTP ではなく HTTPS を使用するように Maven リポジトリを更新](#https-maven)することをお勧めします。
<!-- OLD Removed 1/16/25 * The Java versions installed are Oracle JDK 11.0.22 and Oracle JDK 8u401. -->
* インストールされる Java バージョンは、Oracle JDK 11.0.22、Oracle JDK 17.0.10 および Oracle JDK 21.0.4 です。

<!-- OLD Removed 1/16/25 * **IMPORTANT:** By default, the JAVA_HOME environment variable is set to `/usr/lib/jvm/jdk1.8.0_401`, which contains Oracle JDK 8u401. This default should be overridden for AEM Cloud Projects to use JDK 11. See the Setting the Maven JDK Version section for more details. -->
* **重要：**&#x200B;デフォルトでは、`JAVA_HOME` 環境変数は `/usr/lib/jvm/jdk1.8.0_401` に設定されています。これには、Oracle JDK 8u401 が含まれています。***AEM Cloud プロジェクトで JDK 21（推奨）、17、または 11 を使用するには、このデフォルトを上書きする必要があります***。詳しくは、[Maven JDK バージョンの設定](#alternate-maven-jdk-version)の節を参照してください。
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

<!-- OLD below Removed 1/16/25

### Use a specific Java version

The Cloud Manager build process uses the Oracle 8 JDK to build projects by default, but AEM Cloud Service customers should set the Maven execution JDK version to 11. -->

<!-- OLD below Removed 1/16/25

#### Set the Maven JDK version

Adobe recommends that you set the JDK version for the entire Maven execution to `11` in a `.cloudmanager/java-version file`.

To do so, create a file named `.cloudmanager/java-version` in the git repository branch used by the pipeline. Edit the file so that it contains only the text, `11`. While Cloud Manager also accepts a value of `8`, this version is no longer supported for AEM Cloud Service projects. Any other value is ignored. When `11` is specified, Oracle 11 is used and the `JAVA_HOME` environment variable is set to `/usr/lib/jvm/jdk-11.0.22`. -->

### 特定の Java バージョンの使用 {#using-java-support}

Cloud Manager のビルドプロセスでは、デフォルトで Oracle 8 JDK を使用してプロジェクトを作成しますが、AEM Cloud Service のお客様は Maven 実行 JDK バージョンを 21（推奨）、17、または 11 に設定する必要があります。

#### Maven JDK バージョンの設定 {#alternate-maven-jdk-version}

Maven 実行 JDK を設定するには、パイプラインで使用される Git リポジトリ分岐に `.cloudmanager/java-version` というファイルを作成します。`21` または `17` というテキストのみが含まれるようにファイルを編集します。Cloud Manager は値 `8` も受け入れますが、このバージョンは AEM Cloud Service プロジェクトではサポートされなくなりました。その他の値は無視されます。`21` または `17` を指定した場合は、Oracle Java 21 または Oracle Java 17 が使用されます。


#### Java 21 または Java 17 を使用したビルドへの移行の前提条件 {#prereq-for-building}

Java 21 または Java 17 を使用したビルドに移行するには、まず最新の SonarQube バージョンにアップグレードする必要があります。詳しくは、[Cloud Manager 2025.1.0 のリリースノート](/help/implementing/cloud-manager/release-notes/current.md#what-is-new)を参照してください。

アプリケーションを新しい Java ビルドバージョンとランタイムバージョンに移行する場合は、実稼動環境にデプロイする前に、開発環境とステージ環境で徹底的にテストします。

次のデプロイメント戦略をお勧めします。

1. https://experience.adobe.com/#/downloads からダウンロードできる Java 21 を使用してローカル SDK を実行し、アプリケーションをデプロイして機能を検証します。ログを確認して、クラスロードまたはバイトコードウィービングの問題を示すエラーがないことを確認します。
1. Cloud Manager リポジトリ内の分岐を、ビルド時の Java バージョンとして Java 21 を使用するように設定し、この分岐を使用するように開発パイプラインを設定して、パイプラインを実行します。検証テストを実行します。
1. 問題がなければ、ビルド時の Java バージョンとして Java 21 を使用するようにステージ／実稼動パイプラインを設定して、パイプラインを実行します。

##### 一部の翻訳機能について {#translation-features}

Java 21 ランタイムにデプロイすると、次の機能が正しく機能しない可能性があります。アドビでは、2025年初頭までにこれらの問題を解決する予定です。

* `XLIFF`（XML Localization Interchange File Format）は、人による翻訳を使用すると失敗します。
* 新しい Java バージョンでの ロケールコンストラクタの変更により、`I18n`（国際化）では、言語ロケールのヘブライ語（`he`）、インドネシア語（`in`）、イディッシュ語（`yi`）が適切に処理されません。

#### ランタイム要件 {#runtime-requirements}

Java 21 ランタイムは、Java 21 および Java 17 のビルドに使用され、Java 11 ビルドにも段階的に適用される予定です（以下のメモを参照）。Java 21 アップデートを受信するには、環境を AEM リリース 17098 以降にする必要があります。互換性を確保するには、次の調整が必要です。

ライブラリの更新は、古い Java バージョンとの互換性が維持されるので、いつでも適用できます。

* **ASM の最小バージョン：**
新しい JVM ランタイムのサポートを確保するには、多くの場合、`org.ow2.asm.*` アーティファクトにバンドルされている Java パッケージ `org.objectweb.asm` の使用をバージョン 9.5 以降に更新します。

* **Groovy の最小バージョン：**
新しい JVM ランタイムのサポートを確保するには、Java パッケージ `org.apache.groovy` または `org.codehaus.groovy` の使用をバージョン 4.0.22 以降に更新します。

  このバンドルは、AEM Groovy コンソールなどのサードパーティの依存関係を追加することで間接的に含めることができます。

AEM Cloud Service SDKは Java 21 と互換性があり、Cloud Manager パイプラインを実行する前に、プロジェクトと Java 21 の互換性を検証するのに使用できます。

* **ランタイムパラメーターの編集：**
Java 21 を使用して AEM をローカルで実行すると、`MaxPermSize` パラメーターにより起動スクリプト（`crx-quickstart/bin/start` または `crx-quickstart/bin/start.bat`）が失敗します。対処方法としては、スクリプトから `-XX:MaxPermSize=256M` を削除するか、環境変数 `CQ_JVM_OPTS` を定義して `-Xmx1024m -Djava.awt.headless=true` に設定します。

  この問題は、AEM Cloud Service SDK のバージョン 19149 以降で解決されています。

>[!IMPORTANT]
>
>`.cloudmanager/java-version` を `21` または `17` に設定すると、Java 21 ランタイムがデプロイされます。Java 21 ランタイムは、2025年2月4日木曜日（PT）から、すべての環境（コードが Java 11 でビルドされている環境だけでなく）に段階的にロールアウトされる予定です。ロールアウトは、サンドボックスと開発環境から開始され、2025年4月にすべての実稼動環境にロールアウトされます。Java 21 ランタイムを&#x200B;*早期に*&#x200B;導入するお客様は、アドビ（[aemcs-java-adopter@adobe.com](mailto:aemcs-java-adopter@adobe.com)）にお問い合わせください。


#### ビルド時間の要件 {#build-time-reqs}

Java 21 および Java 17 を使用してプロジェクトをビルドできるようにするには、次の調整が必要です。これらは古い Java バージョンと互換性があるので、Java 21 および Java 17 を実行する前でも更新できます。

新しい言語機能を活用するには、AEM Cloud Service のお客様はできるだけ早く Java 21 を使用してプロジェクトを作成することをお勧めします。

* **`bnd-maven-plugin` の最小バージョン：**
新しい JVM ランタイムのサポートを確保するには、`bnd-maven-plugin` の使用をバージョン 6.4.0 に更新します。

  バージョン 7 以降は、Java 11 以下と互換性がないので、そのバージョンへのアップグレードはお勧めしません。

* **`aemanalyser-maven-plugin` の最小バージョン：**
新しい JVM ランタイムのサポートを確保するには、`aemanalyser-maven-plugin` の使用をバージョン 1.6.6 以降に更新します。

* **`maven-bundle-plugin` の最小バージョン：**
新しい JVM ランタイムのサポートを確保するには、`maven-bundle-plugin` の使用をバージョン 5.1.5 以降に更新します。

  バージョン 6 以降は、Java 11 以下と互換性がないので、そのバージョンへのアップグレードはお勧めしません。

* **`maven-scr-plugin` の依存関係の更新：**
`maven-scr-plugin` は、Java 21 または Java 17 と直接互換性がありません。ただし、次の例に示すように、プラグイン設定で ASM 依存関係バージョンを更新して、記述子ファイルを生成できます。

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
