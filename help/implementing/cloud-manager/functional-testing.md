---
title: 機能テスト
description: コードの品質と信頼性を確保するために、AEM as a Cloud Service デプロイメントプロセスに組み込まれている 3 種類の機能テストについて説明します。
exl-id: 7eb50225-e638-4c05-a755-4647a00d8357
source-git-commit: cd0b40ffa54eac0d7488b23329c4d2666c992da7
workflow-type: tm+mt
source-wordcount: '1124'
ht-degree: 67%

---


# 機能テスト {#functional-testing}

>[!CONTEXTUALHELP]
>id="aemcloud_nonbpa_functionaltesting"
>title="機能テスト"
>abstract="コードの品質と信頼性を確保するために、AEM as a Cloud Service デプロイメントプロセスに組み込まれている 3 種類の機能テストについて説明します。"

コードの品質と信頼性を確保するために、[AEM as a Cloud Service デプロイメントプロセス](/help/implementing/cloud-manager/deploy-code.md)に組み込まれている 3 種類の機能テストについて説明します。

## 概要 {#overview}

AEM as a Cloud Service には 3 種類の機能テストがあります。

* [製品機能テスト](#product-functional-testing)
* [カスタム機能テスト](#custom-functional-testing)
* [カスタム UI テスト](#custom-ui-testing)

すべての機能テストについて、[デプロイメントプロセス](/help/implementing/cloud-manager/deploy-code.md)の一環としてビルド概要画面の「**ビルドログをダウンロード**」ボタンを使用して、テストの詳細な結果を `.zip` ファイル形式でダウンロードできます。

これらのログには、実際の AEM ランタイムプロセスのログは含まれていません。これらのログへのアクセスについて詳しくは、[ログへのアクセスと管理](/help/implementing/cloud-manager/manage-logs.md) を参照してください。

製品機能テストとサンプルのカスタム機能テストは、どちらも [AEM テストクライアント](https://github.com/adobe/aem-testing-clients)に基づいています。

### 製品機能テスト {#product-functional-testing}

製品機能テストは、オーサリングタスクやレプリケーションタスクなど、AEM のコア機能の安定した HTTP 統合テスト（IT）のセットです。これらのテストは、アドビで管理され、コア機能に障害が発生した場合に、カスタムアプリケーションコードに対する変更がデプロイされるのを防ぐことを目的としています。

* [実稼動パイプライン](/help/implementing/cloud-manager/configuring-pipelines/configuring-production-pipelines.md):製品機能テストは、新しいコードを Cloud Manager にデプロイするたびに自動的に実行され、スキップすることはできません。
* [実稼動以外のパイプライン](/help/implementing/cloud-manager/configuring-pipelines/configuring-non-production-pipelines.md):製品機能テストは、オプションで、実稼動以外のパイプラインを実行する際に実行するように選択できます。

製品機能テストは、オープンソースプロジェクトとして維持されます。 詳しくは、GitHub の[製品機能テスト](https://github.com/adobe/aem-test-samples/tree/aem-cloud/smoke)を参照してください。

### カスタム機能テスト {#custom-functional-testing}

製品機能テストはアドビで定義されますが、独自のアプリケーション用に独自の品質テストを作成することもできます。これは、 [実稼動パイプライン](/help/implementing/cloud-manager/configuring-pipelines/configuring-production-pipelines.md) または [非実稼動パイプライン](/help/implementing/cloud-manager/configuring-pipelines/configuring-non-production-pipelines.md) を使用して、アプリケーションの品質を確保します。

カスタム機能テストは、カスタムコードのデプロイメントとプッシュアップグレードの両方で実行されるので、AEMコードの変更によってアプリケーションコードが破損するのを防ぐ、適切な機能テストを作成することが特に重要です。 カスタム機能テストステップは常に存在し、スキップできません。

### カスタム UI テスト {#custom-ui-testing}

カスタム UI テストは、アプリケーションの UI テストを作成して自動的に実行できるオプション機能です。UI テストは、Java や Maven、Node や WebDriver.io などの幅広い言語とフレームワーク、または Selenium に基づいて構築されたその他のフレームワークとテクノロジーを可能にするために、Docker イメージにパッケージ化された Selenium ベースのテストです。

詳しくは、[カスタム UI テスト](/help/implementing/cloud-manager/ui-testing.md#custom-ui-testing)を参照してください。

## 機能テストの概要 {#getting-started-functional-tests}

Cloud Manager で新しいコードリポジトリを作成すると、 `it.tests` フォルダーがサンプルテストケースで自動的に作成されます。

>[!NOTE]
>
>Cloud Manager が自動的に作成される前にリポジトリが作成された場合 `it.tests` フォルダーの場合は、 [AEMプロジェクトアーキタイプ。](https://github.com/adobe/aem-project-archetype/tree/master/src/main/archetype/it.tests)

次に、 `it.tests` フォルダーに保存されている場合、それを独自のテストの基礎として使用し、次の操作を実行できます。

1. [テストケースを作成します。](#writing-functional-tests)
1. [テストをローカルで実行します。](#local-test-execution)
1. コードを Cloud Manager リポジトリにコミットし、Cloud Manager パイプラインを実行します。

## カスタム機能テストの作成 {#writing-functional-tests}

アドビが製品機能テストの作成に使用するのと同じツールを、カスタム機能テストの作成に使用できます。テストの作成方法の例として、GitHub の[製品機能テスト](https://github.com/adobe/aem-test-samples/tree/aem-cloud/smoke)を参照してください。

カスタム機能テストのコードは、プロジェクトの `it.tests` フォルダーにある Java コードです。すべての機能テストを含んだ 1 つの JAR が生成されます。ビルドで複数のテスト JAR が生成される場合、どの JAR が選択されるかは非決定的です。テスト JAR がゼロになる場合、テスト手順はデフォルトで合格します。テストのサンプルについては、[AEM プロジェクトのアーキタイプ](https://github.com/adobe/aem-project-archetype/tree/develop/src/main/archetype/it.tests)を参照してください。

テストは、少なくとも 2 つのオーサーインスタンス、2 つのパブリッシュインスタンス、Dispatcher 設定など、アドビが維持管理するテストインフラストラクチャで実行されます。つまり、カスタム機能テストは AEM スタック全体に対して実行されます。

### 機能テストの構造 {#functional-tests-structure}

カスタム機能テストは、AEM にデプロイするアーティファクトと同じ Maven ビルドで生成される個別の JAR ファイルとしてパッケージ化する必要があります。一般に、これは別個の Maven モジュールになります。結果として生成される JAR ファイルには、必要な依存関係がすべて含まれている必要があり、通常は `jar-with-dependencies` 記述子を使用する `maven-assembly-plugin` で作成されます。

さらに、この JAR では、`Cloud-Manager-TestType` マニフェストヘッダーが `integration-test` に設定されている必要があります。

以下は `maven-assembly-plugin` の設定例です。

```java
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
```

この JAR ファイル内で、実行する実際のテストのクラス名は `IT` で終わる必要があります。

例えば、`com.myco.tests.aem.it.ExampleIT` という名前のクラスは実行されますが、`com.myco.tests.aem.it.ExampleTest` という名前のクラスは実行されません。

さらに、コードスキャンのカバレッジチェックからテストコードを除外するには、テストコードを `it` という名前のパッケージの下に置く必要があります（カバレッジ除外フィルターは `**/it/**/*.java` です）。

テストクラスは、通常の JUnit テストにする必要があります。テストインフラストラクチャは、`aem-testing-clients` テストライブラリで使用される規則との互換性を持つように設計および設定されています。開発者は、このライブラリを使用し、そのライブラリのベストプラクティスに従うことを強くお勧めします。

詳しくは、[`aem-testing-clients` GitHub リポジトリー](https://github.com/adobe/aem-testing-clients)を参照してください。

>[!TIP]
>
>カスタム機能テストを使用して CI／CD パイプラインの信頼性を向上させる方法については、[このビデオ](https://www.youtube.com/watch?v=yJX6r3xRLHU)をご覧ください。

### ローカルテストの実行 {#local-test-execution}

Cloud Manager パイプラインで機能テストをアクティブ化する前に、 [AEMas a Cloud ServiceSDK](/help/implementing/developing/introduction/aem-as-a-cloud-service-sdk.md) または実際のAEMas a Cloud Serviceインスタンス

#### 前提条件 {#prerequisites}

Cloud Manager のテストは、技術管理者ユーザーを使用して実行されます。

ローカルマシンから機能テストを実行する場合は、同じ動作を実現する管理者のような権限を持つユーザーを作成します。

#### IDE での実行 {#running-in-an-ide}

テストクラスは JUnit テストなので、Eclipse、IntelliJ、NetBeans などの主要な Java IDE から実行できます。 製品機能テストとカスタム機能テストはどちらも同じテクノロジーに基づいているので、製品テストをカスタムテストにコピーすることで、両者をローカルで実行できます。

ただし、これらのテストを実行する際は、`aem-testing-clients`（およびそのベースとなる Sling Testing Client）ライブラリで想定されている様々なシステムプロパティを設定する必要があります。

これらのシステムプロパティは次のとおりです。

* `sling.it.instances - should be set to 2`
* `sling.it.instance.url.1 - should be set to the author URL, for example, http://localhost:4502`
* `sling.it.instance.runmode.1 - should be set to author`
* `sling.it.instance.adminUser.1 - should be set to the author admin user, for example, admin`
* `sling.it.instance.adminPassword.1 - should be set to the author admin password`
* `sling.it.instance.url.2 - should be set to the publish URL, for example, http://localhost:4503`
* `sling.it.instance.runmode.2 - should be set to publish`
* `sling.it.instance.adminUser.2 - should be set to the publish admin user, for example, admin`
* `sling.it.instance.adminPassword.2 - should be set to the publish admin password`

#### Maven を使用したすべてのテストの実行 {#using-maven}

1. シェルを開き、 `it.tests` フォルダー内に保存します。

1. 次のコマンドを実行し、Maven を使用してテストを開始するために必要なパラメーターを指定します。

```shell
mvn verify -Plocal \
    -Dit.author.url=https://author-<program-id>-<environment-id>.adobeaemcloud.com \
    -Dit.author.user=<user> \
    -Dit.author.password=<password> \
    -Dit.publish.url=https://publish-<program-id>-<environment-id>.adobeaemcloud.com \
    -Dit.publish.user=<user> \
    -Dit.publish.password=<password>
```
