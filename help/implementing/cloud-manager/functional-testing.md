---
title: 機能テスト - Cloud Services
description: 機能テスト - Cloud Services
translation-type: tm+mt
source-git-commit: 25ba5798de175b71be442d909ee5c9c37dcf10d4
workflow-type: tm+mt
source-wordcount: '415'
ht-degree: 100%

---


# 機能テスト {#functional-testing}

機能テストは次の 2 つのタイプに分類されます。

* 製品機能テスト
* カスタム機能テスト

## 製品機能テスト {#product-functional-testing}

製品機能テストは、AEM のコア機能（オーサリングやレプリケーションなど）に関する安定した HTTP 統合テスト（IT）のセットです。これを実行することで、顧客によるアプリケーションコードの変更がこのコア機能に障害が発生させる場合、その変更がデプロイされるのを防ぎます。

製品機能テストは、顧客が新しいコードを Cloud Manager にデプロイするたびに自動的に実行され、省略することはできません。

サンプルテストについては、[製品機能テスト](https://github.com/adobe/aem-test-samples/tree/aem-cloud/smoke)を参照してください。

## カスタム機能テスト {#custom-functional-testing}

パイプライン内のカスタム機能テストステップは常に存在し、スキップできません。

ただし、ビルドでテスト JAR が生成されない場合、テストはデフォルトで合格します。

>[!NOTE]
>「**ログをダウンロード**」ボタンを使用すると、テスト実行詳細フォームのログを格納した ZIP ファイルにアクセスできます。これらのログには、実際の AEM ランタイムプロセスのログは含まれていません。それらについては、通常のダウンロードログまたはテールログ機能を使用してアクセスできます。詳しくは、[ログのアクセスと管理](/help/implementing/cloud-manager/manage-logs.md)を参照してください。


### 機能テストの作成 {#writing-functional-tests}

ユーザーが作成する機能テストは、AEM にデプロイするアーティファクトと同じ Maven ビルドで生成される個別の JAR ファイルとしてパッケージ化する必要があります。一般に、これは別個の Maven モジュールになります。結果として生成される JAR ファイルには、必要な依存関係がすべて含まれている必要があり、通常は jar-with-dependencies 記述子を使用する maven-assembly-plugin で作成されます。

さらに、この JAR では、Cloud-Manager-TestType マニフェストヘッダーが integration-test に設定されている必要があります。今後、追加のヘッダー値がサポートされる予定です。maven-assembly-plugin の設定例を次に示します。

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

この JAR ファイル内で、実行する実際のテストのクラス名は IT で終わる必要があります。

例えば、`com.myco.tests.aem.ExampleIT` という名前のクラスは実行されますが、`com.myco.tests.aem.ExampleTest` という名前のクラスは実行されません。

テストクラスは、通常の JUnit テストにする必要があります。テストインフラストラクチャは、aem-testing-clients テストライブラリで使用される規則との互換性を持つように設計および設定されています。開発者は、このライブラリを使用し、そのライブラリのベストプラクティスに従うことを強くお勧めします。詳しくは、[Git リンク](https://github.com/adobe/aem-testing-clients)を参照してください。

### ローカルテストの実行 {#local-test-execution}

テストクラスは JUnit テストなので、Eclipse、IntelliJ、NetBeans などの主要な Java IDE から実行できます。

ただし、これらのテストを実行する場合は、aem-testing-clients（およびそのベースとなる Sling Testing Client）で想定している様々なシステムプロパティを設定する必要があります。

これらのシステムプロパティは次のとおりです。

* `sling.it.instances - should be set to 2`
* `sling.it.instance.url.1 - should be set to the author URL, for example, http://localhost:4502`
* `sling.it.instance.runmode.1 - should be set to author`
* `sling.it.instance.adminUser.1 - should be set to the author admin user, e.g. admin`
* `sling.it.instance.adminPassword.1 - should be set to the author admin password`
* `sling.it.instance.url.2 - should be set to the author URL, for example, http://localhost:4503`
* `sling.it.instance.runmode.2 - should be set to publish`
* `sling.it.instance.adminUser.2 - should be set to the publish admin user, for example, admin`
* `sling.it.instance.adminPassword.2 - should be set to the publish admin password`

