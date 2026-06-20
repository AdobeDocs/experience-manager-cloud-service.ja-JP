---
title: Cloud Manager のビルド環境
description: Cloud Manager のビルド環境と、コードを作成およびテストする方法について説明します。
exl-id: a4e19c59-ef2c-4683-a1be-3ec6c0d2f435
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Developer
source-git-commit: 4dd6a9576092c2389f1416377b8e936360a7c7f8
workflow-type: tm+mt
source-wordcount: '1522'
ht-degree: 54%

---


# Cloud Managerのビルド環境 {#build-environment}

Cloud Manager のビルド環境と、コードを作成およびテストする方法について説明します。

>[!TIP]
>
>このドキュメントでは、AEM as a Cloud Service プロジェクトを開発する Cloud Manager のビルド環境について説明します。 コンテンツのオーサリング用にAEM as a Cloud Serviceでサポートされているクライアントプラットフォームについて詳しくは、[&#x200B; サポートされているクライアントプラットフォーム &#x200B;](/help/overview/supported-platforms.md)を参照してください。

## ビルド環境の詳細 {#build-environment-details}

Cloud Manager では、専用のビルド環境を使用して、コードのビルドおよびテストを行います。

* ビルド環境は Linux ベースで、Ubuntu 22.04 から派生しています。
* Apache Maven 3.9.4 がインストールされています。
   * アドビでは、ユーザーに [HTTP ではなく HTTPS を使用するように Maven リポジトリを更新](#https-maven)することをお勧めします。
<!-- OLD Removed 1/16/25 * The Java versions installed are Oracle JDK 11.0.22 and Oracle JDK 8u401. -->
* インストールされる Java バージョンは、Oracle JDK 11.0.22、Oracle JDK 17.0.10 および Oracle JDK 21.0.4 です。

<!-- OLD Removed 1/16/25 * **IMPORTANT:** By default, the JAVA_HOME environment variable is set to `/usr/lib/jvm/jdk1.8.0_401`, which contains Oracle JDK 8u401. This default should be overridden for AEM Cloud Projects to use JDK 11. See the Setting the Maven JDK Version section for more details. -->
* **重要：**&#x200B;デフォルトでは、`JAVA_HOME` 環境変数は `/usr/lib/jvm/jdk1.8.0_401` に設定されています。これには、Oracle JDK 8u401 が含まれています。 ***AEM Cloud プロジェクトのこのデフォルトを上書きして、JDK 21 （推奨）、17、または11***&#x200B;を使用します。 詳しくは、[Maven JDK バージョンの設定](#alternate-maven-jdk-version)の節を参照してください。
* 必要なシステムパッケージが追加でインストールされています。
   * `bzip2`
   * `unzip`
   * `libpng`
   * `imagemagick`
   * `graphicsmagick`
* その他のパッケージは、[追加システムパッケージのインストール &#x200B;](#installing-additional-system-packages)の節で説明されているように、ビルド時にインストールされます。
* 各ビルドは新しい環境で実行されます。ビルドコンテナは、実行間でデータを保持しません。
* Maven は常に次の 3 つのコマンドで実行されます。
   * `mvn --batch-mode org.apache.maven.plugins:maven-dependency-plugin:3.1.2:resolve-plugins`
   * `mvn --batch-mode org.apache.maven.plugins:maven-clean-plugin:3.1.0:clean -Dmaven.clean.failOnError=false`
   * `mvn --batch-mode org.jacoco:jacoco-maven-plugin:prepare-agent package`
* Maven は、`settings.xml` ファイルを使用してシステムレベルで設定されます。このファイルには、`adobe-public` というプロファイルを使用したアドビの公開アーティファクトリポジトリが自動的に含まれています （詳しくは、[アドビの公開 Maven リポジトリ](https://repo1.maven.org/)を参照してください）。

>[!NOTE]
>
>Cloud Manager では、`jacoco-maven-plugin` の特定のバージョンは指定されませんが、必要なバージョンはプロジェクトの Java バージョンによって異なります。 Java 8の場合、プラグインバージョンは少なくとも`0.7.5.201505241946`である必要がありますが、新しいJava バージョンでは、より新しいリリースが必要です。

## HTTPS Maven リポジトリ {#https-maven}

Cloud Manager [&#x200B; リリース 2023.10.0](/help/implementing/cloud-manager/release-notes/2023/2023-10-0.md)では、ビルド環境のローリングアップデート（リリース 2023.12.0で完了）が開始され、これにはMaven 3.8.8へのアップデートが含まれています。 Maven 3.8.1で導入された大きな変更は、潜在的な脆弱性を軽減するためのセキュリティ強化でした。 具体的には、[Maven リリースノート](https://maven.apache.org/docs/3.8.1/release-notes.html#cve-2021-26291)で説明するように、Maven では安全でないすべての `http://*` ミラーをデフォルトで無効にするようになりました。

一部のユーザーは、安全でないHTTP接続を使用するMaven リポジトリからアーティファクトをダウンロードする際に、ビルド手順で問題が発生します。

アップデートされたバージョンでスムーズなエクスペリエンスを実現するために、アドビでは、ユーザーが Mavenリポジトリを更新して HTTP ではなく HTTPS を使用することをお勧めします。 この調整は、業界の安全な通信プロトコルへの移行と一致し、安全で信頼性の高いビルドプロセスを維持するのに役立ちます。

<!--
 OLD below Removed 1/16/25

### Use a specific Java version

The Cloud Manager build process uses the Oracle 8 JDK to build projects by default, but AEM Cloud Service customers should set the Maven execution JDK version to 11.
-->

<!--
 OLD below Removed 1/16/25

#### Set the Maven JDK version

Adobe recommends that you set the JDK version for the entire Maven execution to `11` in a `.cloudmanager/java-version file`.

To do so, create a file named `.cloudmanager/java-version` in the git repository branch used by the pipeline. Edit the file so that it contains only the text, `11`. While Cloud Manager also accepts a value of `8`, this version is no longer supported for AEM Cloud Service projects. Any other value is ignored. When `11` is specified, Oracle 11 is used and the `JAVA_HOME` environment variable is set to `/usr/lib/jvm/jdk-11.0.22`.
-->

### 特定の Java バージョンの使用 {#using-java-support}

Cloud Manager ビルドプロセスでは、デフォルトでOracle 8 JDKを使用してプロジェクトをビルドしますが、AEM Cloud Serviceのお客様は、Maven実行JDK バージョンを21 （推奨）、17、または11に設定します。

#### Maven JDK バージョンの設定 {#alternate-maven-jdk-version}

Maven 実行 JDK を設定するには、パイプラインで使用される Git リポジトリ分岐に `.cloudmanager/java-version` というファイルを作成します。 `21` または `17` というテキストのみが含まれるようにファイルを編集します。 Cloud Manager は値 `8` も受け入れますが、このバージョンは AEM Cloud Service プロジェクトではサポートされなくなりました。 その他の値は無視されます。 `21` または `17` を指定した場合は、Oracle Java 21 または Oracle Java 17 が使用されます。


#### Java 21 または Java 17 を使用したビルドへの移行の前提条件 {#prereq-for-building}

Java 21 または Java 17 でビルドするために、Cloud Manager は、これらの Java バージョンと互換性のある SonarQube 9.9 を使用するようになりました。 この変更は、Cloud Manager リリース 2025.1.0で導入されました。 SonarQubeをアップグレードするために顧客の操作は必要ありません。 詳細および変更点については、[Cloud Manager 2025.1.0 のリリースノート](/help/implementing/cloud-manager/release-notes/2025/2025-1-0.md)を参照してください。

アプリケーションを新しい Java ビルドバージョンとランタイムバージョンに移行する場合は、実稼動環境にデプロイする前に、開発環境とステージ環境で徹底的にテストします。

次のデプロイメント戦略をお勧めします。

1. https://experience.adobe.com/#/downloadsからダウンロードできるJava 21でローカル SDKを実行し、アプリケーションをデプロイして、その機能を検証します。 クラスの読み込みやバイトコードの織り込みに関する問題を示すエラーがないことを確認するには、ログを確認します。
1. Java 21をビルド時間Java バージョンとして使用するには、Cloud Manager リポジトリでブランチを設定し、このブランチを使用するようにDEV パイプラインを設定してパイプラインを実行します。 検証テストを実行します。
1. Java 21をビルド時間Java バージョンとして使用する場合に結果が良好である場合は、ステージ/実稼動パイプラインを設定してパイプラインを実行します。

##### 翻訳機能 {#translation-features}

Java 21 ランタイムにデプロイすると、次の機能が正しく機能せず、Adobeでは2025年初頭までにそれらを解決する予定です。

* `XLIFF`（XML Localization Interchange File Format）は、人による翻訳を使用すると失敗します。
* 新しいJava バージョンでロケールコンストラクターが変更されたため、`I18n` （国際化）は、ヘブライ語（`he`）、インドネシア語（`in`）、およびイディッシュ語（`yi`）の言語ロケールを適切に処理できません。

#### ランタイム要件 {#runtime-requirements}

Java 21 ランタイムは、以下の条件を満たすAEM リリース 17098以降の環境である、すべての対象環境に適用されました。 環境が条件を満たさない場合は、パフォーマンス、可用性、セキュリティを確保するために調整を行うことが重要です。

* **ASMの最小バージョン：**
新しいJVM ランタイムのサポートを確保するために、Java パッケージ `org.objectweb.asm`の使用状況をバージョン 9.5以降に更新します（多くの場合、`org.ow2.asm.*` アーティファクトにバンドルされています）。

* **Groovyの最小バージョン：**
Java パッケージ `org.apache.groovy`または`org.codehaus.groovy`の使用方法をバージョン 4.0.22以降に更新して、新しいJVM ランタイムをサポートするようにします。

  このバンドルは、AEM Groovy コンソールなどのサードパーティの依存関係を追加することで間接的に含めることができます。

* **Aries SPIFlyの最小バージョン：**
新しいJVM ランタイムのサポートを確保するために、Java パッケージ `org.apache.aries.spifly.dynamic.bundle`の使用方法をバージョン 1.3.6以降に更新します。

AEM Cloud Service SDK は、Java 21 をサポートしています。これにより、Cloud Manager パイプラインを実行する前にプロジェクトと Java 21 の互換性を確認できます。

* **ランタイム パラメーターを編集：**
Java 21でAEMをローカルで実行すると、`MaxPermSize` パラメーターが原因で開始スクリプト （`crx-quickstart/bin/start`または`crx-quickstart/bin/start.bat`）が失敗します。 または、スクリプトから`-XX:MaxPermSize=256M`を削除するか、環境変数`CQ_JVM_OPTS`を定義して`-Xmx1024m -Djava.awt.headless=true`に設定します。

  この問題は、AEM Cloud Service SDK のバージョン 19149 以降で解決されています。

>[!IMPORTANT]
>
>環境が Java 21 ランタイムにまだ自動更新されていない場合は、Java 17 または 21 を使用してビルドすれば、トリガーできます。 この設定は、`.cloudmanager/java-version`を`21`または`17`に設定することによって行います。 ご不明な点については、アドビ（[aemcs-java-adopter@adobe.com](mailto:aemcs-java-adopter@adobe.com)）までお問い合わせください。

#### ビルド時間の要件 {#build-time-reqs}

Java 21 および Java 17 を使用してプロジェクトをビルドできるようにするには、次の調整が必要です。 これらは古い Java バージョンと互換性があるので、Java 21 および Java 17 を実行する前でも更新できます。

新しい言語機能を活用するには、AEM Cloud Service のお客様はできるだけ早く Java 21 を使用してプロジェクトを作成することをお勧めします。

* **最小バージョンの`bnd-maven-plugin`:**
新しいJVM ランタイムのサポートを確保するために、`bnd-maven-plugin`の使用方法をバージョン 6.4.0に更新します。

  バージョン 7 以降は、Java 11 以下と互換性がないので、そのバージョンへのアップグレードはお勧めしません。

* **最小バージョンの`aemanalyser-maven-plugin`:**
新しいJVM ランタイムのサポートを確保するために、`aemanalyser-maven-plugin`の使用方法をバージョン 1.6.16以降に更新します。

* **最小バージョンの`maven-bundle-plugin`:**
新しいJVM ランタイムのサポートを確保するために、`maven-bundle-plugin`の使用方法をバージョン 5.1.5以降に更新します。

  バージョン 6 以降は、Java 11 以下と互換性がないので、そのバージョンへのアップグレードはお勧めしません。

* **`maven-scr-plugin`の依存関係を更新：**
`maven-scr-plugin`は、Java 21またはJava 17と直接互換性がありません。 ただし、次の例に示すように、プラグイン設定で ASM 依存関係バージョンを更新して、記述子ファイルを生成できます。

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

プログラムまたはパイプラインに関する情報に基づいてビルドプロセスを設定します。

例えば、gulpなどのツールを使用してビルド時にJavaScriptの縮小が行われる場合、様々な環境に対して異なる縮小レベルが推奨されます。 開発ビルドでは、ステージングや実稼動と比較して、より軽い縮小レベルを使用します。

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

ビルドプロセスには、Git リポジトリに保存されていない特定の設定変数が必要です。 さらに、同じブランチを使用するパイプライン実行間でこれらの変数を調整する必要があります。

詳しくは、[パイプライン変数の設定](/help/implementing/cloud-manager/configuring-pipelines/pipeline-variables.md)も参照してください。

## 追加のシステムパッケージのインストール {#installing-additional-system-packages}

すべての機能を実装するにあたり、一部のビルドでは追加のシステムパッケージが必要です。 例えば、ビルドはPythonまたはRuby スクリプトを呼び出し、適切な言語インタープリターがインストールされている必要があります。 このインストールプロセスは、`pom.xml` で [`exec-maven-plugin`](https://www.mojohaus.org/exec-maven-plugin/) を呼び出して APT を起動することで、管理できます。 この実行は、Cloud Manager固有のMaven プロファイルでラップされます。 この例では、Python をインストールしています。

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
>この方法でシステムパッケージをインストールしても、Adobe Experience Manager の実行に使用されているランタイム環境にはインストールされません。 AEM環境にシステムパッケージをインストールする必要がある場合は、Adobe担当者にお問い合わせください。

>[!TIP]
>
>フロントエンドビルド環境について詳しくは、[フロントエンドパイプラインを使用したサイトの開発](/help/implementing/developing/introduction/developing-with-front-end-pipelines.md)のドキュメントを参照してください。
