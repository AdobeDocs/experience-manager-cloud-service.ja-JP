---
title: 機能テスト
description: コードの品質と信頼性を確保するために、AEMのas a Cloud Service的なデプロイメントプロセスに組み込まれている 3 種類の機能テストについて説明します。
exl-id: 7eb50225-e638-4c05-a755-4647a00d8357
source-git-commit: f8d5b94d176dfbd5bcecf552f974dc77c5afe4e2
workflow-type: tm+mt
source-wordcount: '898'
ht-degree: 20%

---


# 機能テスト {#functional-testing}

>[!CONTEXTUALHELP]
>id="aemcloud_nonbpa_functionaltesting"
>title="機能テスト"
>abstract="コードの品質と信頼性を確保するために、AEMのas a Cloud Service的なデプロイメントプロセスに組み込まれている 3 種類の機能テストについて説明します。"

に組み込まれている 3 種類の機能テストについて説明します。 [AEMas a Cloud Serviceデプロイメントプロセス](/help/implementing/cloud-manager/deploy-code.md) コードの品質と信頼性を確保するため。

## 概要 {#overview}

AEM as a Cloud Serviceには、3 つの異なるタイプの機能テストがあります。

* [製品機能テスト](#product-functional-testing)
* [カスタム機能テスト](#custom-functional-testing)
* [カスタム UI テスト](#custom-ui-testing)

すべての機能テストで、テストの詳細な結果は、 `.zip` ファイルを **ビルドログをダウンロード** ボタンを [デプロイメントプロセスです。](/help/implementing/cloud-manager/deploy-code.md)

これらのログには、実際のAEMランタイムプロセスのログは含まれません。 これらのログにアクセスするには、ドキュメントを参照してください [ログへのアクセスと管理](/help/implementing/cloud-manager/manage-logs.md) を参照してください。

製品機能テストとサンプルのカスタム機能テストは、両方とも、 [AEM Testing Clients を参照してください。](https://github.com/adobe/aem-testing-clients)

## 製品機能テスト {#product-functional-testing}

製品機能テストは、オーサリングタスクやレプリケーションタスクなど、AEMのコア機能の安定した HTTP 統合テスト (IT) のセットです。 これらのテストは、Adobeによって管理され、コア機能に障害が発生した場合に、カスタムアプリケーションコードに対する変更がデプロイされるのを防ぐことを目的としています。

製品機能テストは、新しいコードを Cloud Manager にデプロイするたびに自動的に実行され、スキップすることはできません。

製品機能テストは、オープンソースプロジェクトとして維持されます。 詳しくは、 [製品機能テスト](https://github.com/adobe/aem-test-samples/tree/aem-cloud/smoke) 詳しくは、 GitHub を参照してください。

## カスタム機能テスト {#custom-functional-testing}

製品機能テストはAdobeによって定義されますが、独自のアプリケーション用に独自の品質テストを作成することもできます。 これは、実稼動パイプラインの一部としてカスタム機能テストとして実行され、アプリケーションの品質を確保します。

カスタム機能テストは、カスタムコードのデプロイメントとプッシュアップグレードの両方で実行されます。そのため、AEMコードの変更によってアプリケーションコードが破損するのを防ぐ、適切な機能テストを作成することが特に重要です。 カスタム機能テスト手順は常に存在し、スキップできません。

### カスタム機能テストの作成 {#writing-functional-tests}

Adobeが製品機能テストを作成する際に使用するのと同じツールを、カスタム機能テストの作成に使用できます。 以下を使用： [製品機能テスト](https://github.com/adobe/aem-test-samples/tree/aem-cloud/smoke) （GitHub のテスト書き込み方法の例）

カスタム機能テストのコードは、 `it.tests` プロジェクトのフォルダー。 すべての機能テストを含む 1 つの JAR を生成する必要があります。 ビルドによって複数のテスト JAR が生成される場合、どの JAR が非決定的に選択されるかは非決定的です。 テスト JAR がゼロになる場合、テスト手順はデフォルトで合格します。[「 AEM Project Archetype 」を参照してください。](https://github.com/adobe/aem-project-archetype/tree/develop/src/main/archetype/it.tests) を参照してください。

テストは、少なくとも 2 つのオーサーインスタンス、2 つのパブリッシュインスタンス、Dispatcher 設定など、Adobeが維持するテストインフラストラクチャで実行されます。 つまり、カスタム機能テストはAEMスタック全体に対して実行されます。

カスタム機能テストは、AEMにデプロイするアーティファクトと同じ Maven ビルドで生成される個別の JAR ファイルとしてパッケージ化する必要があります。 一般に、これは別個の Maven モジュールになります。結果の JAR ファイルには、必要な依存関係がすべて含まれている必要があり、通常は `maven-assembly-plugin` の使用 `jar-with-dependencies` 記述子。

さらに、JAR には `Cloud-Manager-TestType` manifest ヘッダーをに設定 `integration-test`.

次に、 `maven-assembly-plugin`.

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

テストクラスは、通常の JUnit テストにする必要があります。テストインフラストラクチャは、 `aem-testing-clients` テストライブラリ。 開発者は、このライブラリを使用し、そのライブラリのベストプラクティスに従うことを強くお勧めします。

詳しくは、 [`aem-testing-clients` GitHub リポジトリ](https://github.com/adobe/aem-testing-clients) を参照してください。

>[!TIP]
>
>[このビデオを見る](https://www.youtube.com/watch?v=yJX6r3xRLHU) カスタム機能テストを使用して CI/CD パイプラインに対する信頼性を向上させる方法について説明します。

## カスタム UI テスト {#custom-ui-testing}

カスタム UI テストは、アプリケーションの UI テストを作成して自動的に実行できるオプションの機能です。 UI テストは、言語とフレームワークの幅広い選択肢（Java と Maven、Node と WebDriver.io、Selenium に基づいて構築されたその他のフレームワークとテクノロジーなど）を可能にするために Docker イメージにパッケージ化された Selenium ベースのテストです。

ドキュメントを参照してください [カスタム UI テスト](/help/implementing/cloud-manager/ui-testing.md#custom-ui-testing) を参照してください。

## ローカルテストの実行 {#local-test-execution}

テストクラスは JUnit テストなので、Eclipse、IntelliJ、NetBeans などの主要な Java IDE から実行できます。 製品機能テストとカスタム機能テストは両方とも同じテクノロジーに基づいているので、製品テストをカスタムテストにコピーすることで、両方をローカルで実行できます。

ただし、これらのテストを実行する場合は、 `aem-testing-clients` （および基になる Sling Testing Clients）ライブラリ。

システムのプロパティは次のとおりです。

* `sling.it.instances - should be set to 2`
* `sling.it.instance.url.1 - should be set to the author URL, for example, http://localhost:4502`
* `sling.it.instance.runmode.1 - should be set to author`
* `sling.it.instance.adminUser.1 - should be set to the author admin user, e.g. admin`
* `sling.it.instance.adminPassword.1 - should be set to the author admin password`
* `sling.it.instance.url.2 - should be set to the publish URL, for example, http://localhost:4503`
* `sling.it.instance.runmode.2 - should be set to publish`
* `sling.it.instance.adminUser.2 - should be set to the publish admin user, for example, admin`
* `sling.it.instance.adminPassword.2 - should be set to the publish admin password`
