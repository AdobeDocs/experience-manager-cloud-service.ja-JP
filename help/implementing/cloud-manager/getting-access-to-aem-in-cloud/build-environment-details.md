---
title: Cloud Manager のビルド環境
description: Cloud Manager のビルド環境と、コードを作成およびテストする方法について説明します。
exl-id: a4e19c59-ef2c-4683-a1be-3ec6c0d2f435
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
source-git-commit: 7b9b9f3b957b27812c4a7e8f2dbcf96d8786b73e
workflow-type: tm+mt
source-wordcount: '1277'
ht-degree: 52%

---


# ビルド環境 {#build-environment}

Cloud Manager のビルド環境と、コードを作成およびテストする方法について説明します。

## ビルド環境の詳細 {#build-environment-details}

Cloud Manager では、専用のビルド環境を使用して、コードのビルドおよびテストを行います。

* ビルド環境は Linux ベースで、Ubuntu 22.04 から派生しています。
* Apache Maven 3.9.4 がインストールされています。
   * アドビでは、ユーザーに [HTTP ではなく HTTPS を使用するように Maven リポジトリを更新](#https-maven)することをお勧めします。
* インストールされる Java バージョンは、Oracle JDK 11.0.22、Oracle JDK 17.0.10 およびOracle JDK 21.0.4 です。
* **重要：** デフォルトでは、`JAVA_HOME` 環境変数は `/usr/lib/jvm/jdk1.8.0_401` に設定されています。これには、OracleJDK 8u401 が含まれています。 ***AEM Cloud Projects で JDK 21 （推奨）、17 または 11 を使用する場合は、このデフォルトを上書きする必要があります***。 詳しくは、[Maven JDK バージョンの設定](#alternate-maven-jdk-version)の節を参照してください。
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

### 特定の Java バージョンの使用 {#using-java-support}

Cloud Managerのビルドプロセスでは、デフォルトでOracle 8 JDK を使用してプロジェクトをビルドしますが、AEM Cloud Serviceのお客様は、Maven 実行 JDK バージョンを 21 （推奨）、17 または 11 に設定する必要があります。

#### Maven JDK バージョンの設定 {#alternate-maven-jdk-version}

Adobeでは、Maven 実行 JDK バージョンを `.cloudmanager/java-version` ファイルで `21` または `17` に設定することをお勧めします。

それには、パイプラインで使用される Git リポジトリーブランチに `.cloudmanager/java-version` というファイルを作成します。 ファイルを編集して、テキスト、`21` または `17` のみが含まれるようにします。 Cloud Manager は値 `8` も受け入れますが、このバージョンは AEM Cloud Service プロジェクトではサポートされなくなりました。その他の値は無視されます。`21` または `17` を指定した場合は、Oracle Java 21 またはOracle Java 17 が使用され、`JAVA_HOME` 環境変数が `/usr/lib/jvm/jdk-21` または `/usr/lib/jvm/jdk-17` に設定されます。

#### Java 21 または Java 17 を使用してビルドへの移行の前提条件 {#prereq-for-building}

>[!NOTE]
>
>*アプリケーションを新しい Java ビルドバージョンおよびランタイムバージョンに移行する場合は、実稼動環境にデプロイする前に、開発環境とステージ環境で十分にテストします。
>特に、次の機能は Java 21 ランタイムでまだ正式に検証されていません。[Forms](/help/forms/home.md)、[ ワークフロー ](/help/sites-cloud/authoring/workflows/overview.md)、[ インボックス ](/help/sites-cloud/authoring/inbox.md)、[ プロジェクト ](/help/sites-cloud/authoring/projects/overview.md)。 アプリケーションがこれらの機能を利用している場合は、機能を検証するための包括的なテストを行ってください。*

##### 一部の翻訳機能 {#translation-features}

以下の機能は、Java 21 または Java 17 でビルドすると正しく機能しない場合があり、Adobeでは、2025 年初頭までに解決される予定です。

* 人間翻訳を使用すると、`XLIFF` （XML Localization Interchange File Format）が失敗する。
* 新しいバージョンの Java ではロケール・コンストラクタが変更されているため、`I18n` （国際化）で言語ロケールのヘブライ語（`he`）、インドネシア語（`in`）、イディッシュ語（`yi`）が適切に処理されません。

#### ランタイム要件 {#runtime-requirements}

Java 21 ランタイムは、2025 年 2 月以降、Java 21、Java 17、Java 11 上のビルドに使用されます。 互換性を確保するには、次の調整が必要です。

ライブラリのアップデートは、古い Java バージョンとの互換性が維持されるので、いつでも適用できます。

* **`org.objectweb.asm` の最小バージョン：**
`org.objectweb.asm` の使用状況をバージョン 9.5 以降に更新して、新しい JVM ランタイムがサポートされるようにします。

* **`org.apache.groovy` の最小バージョン：**
`org.apache.groovy` の使用状況をバージョン 4.0.22 以降に更新して、新しい JVM ランタイムがサポートされるようにします。

  このバンドルは、AEM Groovy コンソールなどのサードパーティの依存関係を追加することで間接的に含めることができます。

* **ランタイムパラメーターの編集：**
Java 21 を使用してAEMをローカルで実行すると、`MaxPermSize` パラメーターが原因で開始スクリプト（`crx-quickstart/bin/start` または `crx-quickstart/bin/start.bat`）が失敗します。 対処方法としては、スクリプトから `-XX:MaxPermSize=256M` を削除するか、環境変数 `CQ_JVM_OPTS` を定義して `-Xmx1024m -Djava.awt.headless=true` に設定します。

  Adobeでは、今後のリリースでこの問題を解決する予定です。

>[!NOTE]
>
>`.cloudmanager/java-version` を `21` または `17` に設定すると、Java 21 ランタイムがデプロイされます。 コードの構築に Java 11 を使用している場合でも、2025 年 2 月または 3 月に、Java 21 ランタイムをすべての顧客にデプロイする予定です。

#### ビルド時間の要件

Java 21 および Java 17 でプロジェクトを構築するには、次の調整が必要です。 古いバージョンの Java と互換性があるので、いつでも更新できます。

* **`bnd-maven-plugin` の最小バージョン：**
`bnd-maven-plugin` の使用状況をバージョン 6.4.0 に更新して、新しい JVM ランタイムがサポートされるようにします。

  バージョン 7 以降は Java 11 以前と互換性がないので、そのバージョンへのアップグレードはお勧めしません。

* **`aemanalyser-maven-plugin` の最小バージョン：**
`aemanalyser-maven-plugin` の使用状況をバージョン 1.6.6 以降に更新して、新しい JVM ランタイムがサポートされるようにします。

* **`maven-bundle-plugin` の最小バージョン：**
`maven-bundle-plugin` の使用状況をバージョン 5.1.5 以降に更新して、新しい JVM ランタイムがサポートされるようにします。

  バージョン 6 以降は Java 11 以前と互換性がないので、そのバージョンへのアップグレードはお勧めしません。

* **`maven-scr-plugin` の依存関係の更新：**
`maven-scr-plugin` は、Java 21 または Java 17 と直接互換性がありません。 ただし、次の例に示すように、プラグイン設定で ASM 依存関係バージョンを更新することで、記述子ファイルを生成できます。

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
