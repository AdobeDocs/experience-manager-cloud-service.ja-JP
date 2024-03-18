---
title: Java™ 機能テスト
description: AEM as a Cloud Service 用の Java™ 機能テストの作成方法を説明します
exl-id: e014b8ad-ac9f-446c-bee8-adf05a6b4d70
source-git-commit: 641690f2eca17bbfb47360282e818b6902a36144
workflow-type: tm+mt
source-wordcount: '878'
ht-degree: 94%

---

# Java™ 機能テスト

AEM as a Cloud Service 用の Java™ 機能テストの作成方法を説明します

## 機能テストの概要 {#getting-started-functional-tests}

Cloud Manager で新しいコードリポジトリを作成すると、サンプルテストケースを含む `it.tests` フォルダーが自動的に作成されます。

>[!NOTE]
>
>Cloud Manager が `it.tests` フォルダーを自動作成する前にリポジトリが作成された場合は、[AEM プロジェクトアーキタイプを使用して最新バージョンを生成することもできます。](https://github.com/adobe/aem-project-archetype/tree/master/src/main/archetype/it.tests)

`it.tests` フォルダーの内容を取得したら、それを独自のテストの基礎として使用し、次の操作を実行できます。

1. [テストケースを作成します。](#writing-functional-tests)
1. [テストをローカルで実行します。](#local-test-execution)
1. コードを Cloud Manager リポジトリにコミットし、Cloud Manager パイプラインを実行します。

## カスタム機能テストの作成 {#writing-functional-tests}

アドビが製品機能テストの作成に使用するのと同じツールを、カスタム機能テストの作成に使用できます。テストの作成方法の例として、GitHub の[製品機能テスト](https://github.com/adobe/aem-test-samples/tree/aem-cloud/smoke)を参照してください。

カスタム機能テストのコードは、プロジェクトの `it.tests` フォルダーにある Java™ コードです。すべての機能テストを含んだ 1 つの JAR が生成されます。ビルドで複数のテスト JAR が生成される場合、どの JAR が選択されるかは非決定的です。テスト JAR がゼロになる場合、テスト手順はデフォルトで合格します。テストのサンプルについては、[AEM プロジェクトのアーキタイプ](https://github.com/adobe/aem-project-archetype/tree/develop/src/main/archetype/it.tests)を参照してください。

テストは、少なくとも 2 つのオーサーインスタンス、2 つのパブリッシュインスタンス、Dispatcher 設定など、アドビが維持管理するテストインフラストラクチャで実行されます。つまり、この設定では、カスタム機能テストは AEM スタック全体に対して実行されます。

### 機能テストの構造 {#functional-tests-structure}

カスタム機能テストは、AEM にデプロイするアーティファクトと同じ Maven ビルドで生成される個別の JAR ファイルとしてパッケージ化する必要があります。一般に、このビルドは別個の Maven モジュールになります。結果として生成される JAR ファイルには、必要な依存関係がすべて含まれている必要があり、通常は `jar-with-dependencies` 記述子を使用する `maven-assembly-plugin` で作成されます。

さらに、この JAR では、`Cloud-Manager-TestType` マニフェストヘッダーが `integration-test` に設定されている必要があります。

以下は `maven-assembly-plugin` の設定例です。

```XML
<build>
    <plugins>
        <!-- Create self-contained jar with dependencies -->
        <plugin>
            <groupId>org.apache.maven.plugins</groupId>
            <artifactId>maven-assembly-plugin</artifactId>
            <version>3.1.0</version>
            <configuration>
                <descriptorRefs>
                    <descriptorRef>jar-with-dependencies</descriptorRef>
                </descriptorRefs>
                <archive>
                    <manifestEntries>
                        <Cloud-Manager-TestType>integration-test</Cloud-Manager-TestType>
                    </manifestEntries>
                </archive>
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
    </plugins>
</build>
```

この JAR ファイル内で、実行する実際のテストのクラス名は `IT` で終わる必要があります。

例えば、`com.myco.tests.aem.it.ExampleIT` という名前のクラスは実行されますが、`com.myco.tests.aem.it.ExampleTest` という名前のクラスは実行されません。

さらに、コードスキャンのカバレッジチェックからテストコードを除外するには、テストコードを `it` という名前のパッケージの下に置く必要があります（カバレッジ除外フィルターは `**/it/**/*.java` です）。

テストクラスは、通常の JUnit テストである必要があります。テストインフラストラクチャは、`aem-testing-clients` テストライブラリで使用される規則との互換性を持つように設計および設定されています。開発者は、このライブラリを使用し、そのライブラリのベストプラクティスに従うことをお勧めします。

詳しくは、[`aem-testing-clients`GitHub リポジトリ](https://github.com/adobe/aem-testing-clients)を参照してください。

>[!TIP]
>
>カスタム機能テストを使用して CI／CD パイプラインの信頼性を向上させる方法については、[このビデオ](https://www.youtube.com/watch?v=yJX6r3xRLHU)をご覧ください。

### 前提条件 {#prerequisites}

1. Cloud Manager でのテストは、技術管理者ユーザーを使用して実行されます。

>[!NOTE]
>
>ローカルマシンから機能テストを実行する場合は、管理者のような権限を持つユーザーを作成して、同じ動作を実現します。

1. 機能テストの範囲を定義するコンテナ化されたインフラストラクチャは、次の境界によって制限されます。


| タイプ | 値 | 説明 |
|----------------------|-------|--------------------------------------------------------------------|
| CPU | 0.5 | テスト実行ごとに確保される CPU 時間の量です。 |
| メモリ | 0.5 Gi | テストに割り当てられたメモリの量（値は GiB 単位） |
| タイムアウト | 30 m | テストが終了するまでの期間。 |
| 推奨期間 | 15 m | アドビは、この時間を超えないようにテストを書き込むことをお勧めします。 |

>[!NOTE]
>
> さらにリソースが必要な場合は、カスタマーケアケースを作成し、ユースケースを説明してください。アドビのチームがお客様のリクエストを確認し、適切なサポートを提供します。

#### 依存関係

* aem-cloud-testing-clients:

機能テストの実行に使用されるコンテナ化されたインフラストラクチャの変更に備えて、ライブラリが必要になります [aem-cloud-testing-clients](https://github.com/adobe/aem-testing-clients) カスタム機能テストで少なくともバージョンに更新するために使用されます **1.2.1**
依存関係を `it.tests/pom.xml` が更新されました。

```
<dependency>
   <groupId>com.adobe.cq</groupId>
   <artifactId>aem-cloud-testing-clients</artifactId>
   <version>1.2.1</version>
</dependency>
```

>[!NOTE]
>
>この変更は、2024 年 4 月 7 日より前に実行する必要があります。
>依存関係ライブラリの更新に失敗すると、「カスタム機能テスト」手順でパイプラインにエラーが発生します。

### ローカルテストの実行 {#local-test-execution}

Cloud Manager パイプラインで機能テストをアクティブ化する前に、[AEM as a Cloud Service SDK](/help/implementing/developing/introduction/aem-as-a-cloud-service-sdk.md) または実際の AEM as a Cloud Service インスタンスを使用して、機能テストをローカルで実行することをお勧めします。

#### IDE での実行 {#running-in-an-ide}

テストクラスは JUnit テストなので、Eclipse、IntelliJ、NetBeans などの主要な Java™ IDE から実行できます。製品機能テストとカスタム機能テストはどちらも同じテクノロジーに基づいているので、製品テストをカスタムテストにコピーすることで、両者をローカルで実行できます。

ただし、これらのテストを実行する際は、`aem-testing-clients`（および基礎となる Sling Testing Client）ライブラリで想定される様々なシステムプロパティを設定する必要があります。

これらのシステムプロパティは次のとおりです。

| Property | 説明 | 例 |
|-------------------------------------|------------------------------------------------------------------|-------------------------|
| `sling.it.instances` | インスタンスの数は、クラウドサービスに合わせて `2` に設定する必要があります | `2` |
| `sling.it.instance.url.1` | オーサー URL に設定する必要があります。 | `http://localhost:4502` |
| `sling.it.instance.runmode.1` | 最初のインスタンスの実行モードは、`author` に設定する必要があります | `author` |
| `sling.it.instance.adminUser.1` | 作成者の管理者ユーザーに設定する必要があります。 | `admin` |
| `sling.it.instance.adminPassword.1` | 作成者の管理者パスワードに設定する必要があります。 |                         |
| `sling.it.instance.url.2` | パブリッシュ URL に設定する必要があります。 | `http://localhost:4503` |
| `sling.it.instance.runmode.2` | 2 番目のインスタンスの実行モードは、`publish` に設定する必要があります | `publish` |
| `sling.it.instance.adminUser.2` | パブリッシュの管理者ユーザーに設定する必要があります。 | `admin` |
| `sling.it.instance.adminPassword.2` | パブリッシュの管理者パスワードに設定する必要があります。 |                         |



#### Maven を使用したすべてのテストの実行 {#using-maven}

1. シェルを開き、リポジトリの `it.tests` フォルダーに移動します。

1. Maven を使用してテストを開始する上で必要なパラメーターを指定して、次のコマンドを実行します。

```shell
mvn verify -Plocal \
    -Dit.author.url=https://author-<program-id>-<environment-id>.adobeaemcloud.com \
    -Dit.author.user=<user> \
    -Dit.author.password=<password> \
    -Dit.publish.url=https://publish-<program-id>-<environment-id>.adobeaemcloud.com \
    -Dit.publish.user=<user> \
    -Dit.publish.password=<password>
```

