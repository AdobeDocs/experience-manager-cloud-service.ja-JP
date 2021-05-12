---
title: 機能テスト - Cloud Services
description: 機能テスト - Cloud Services
exl-id: 7eb50225-e638-4c05-a755-4647a00d8357
source-git-commit: 006fd74a9c4f4d5321bb3d0b35b5c9d49def7bc4
workflow-type: tm+mt
source-wordcount: '866'
ht-degree: 55%

---

# 機能テスト {#functional-testing}


>[!CONTEXTUALHELP]
>id="aemcloud_nonbpa_functionaltesting"
>title="機能テスト"
>abstract="機能テストは次の3つのタイプに分類されます。製品機能テスト、カスタム機能テスト、カスタムUIテスト"

機能テストは次の3つのタイプに分類されます。


* 製品機能テスト
* カスタム機能テスト
* カスタム UI テスト

## 製品機能テスト {#product-functional-testing}

製品機能テストは、AEM のコア機能（オーサリングやレプリケーションなど）に関する安定した HTTP 統合テスト（IT）のセットです。これを実行することで、顧客によるアプリケーションコードの変更がこのコア機能に障害が発生させる場合、その変更がデプロイされるのを防ぎます。

製品機能テストは、顧客が新しいコードを Cloud Manager にデプロイするたびに自動的に実行され、省略することはできません。

サンプルテストについては、[製品機能テスト](https://github.com/adobe/aem-test-samples/tree/aem-cloud/smoke)を参照してください。

## カスタム機能テスト {#custom-functional-testing}

パイプライン内のカスタム機能テストステップは常に存在し、スキップできません。

ただし、ビルドでテスト JAR が生成されない場合、テストはデフォルトで合格します。

>[!NOTE]
>「**ログをダウンロード**」ボタンを使用すると、テスト実行詳細フォームのログを格納した ZIP ファイルにアクセスできます。これらのログには、実際の AEM ランタイムプロセスのログは含まれていません。それらについては、通常のダウンロードログまたはテールログ機能を使用してアクセスできます。詳しくは、[ログのアクセスと管理](/help/implementing/cloud-manager/manage-logs.md)を参照してください。

## カスタム UI テスト {#custom-ui-testing}

AEMは、Cloud Managerの品質ゲートを統合してお客様に提供し、アプリケーションの更新をスムーズに行います。 特に、ITテストゲートにより、お客様はAEM APIを使用する独自のテストを作成および自動化できます。

カスタムUIテスト機能は、オプションの機能[お客様オプトイン](#customer-opt-in)です。これにより、お客様は、アプリケーションのUIテストを作成し、自動的に実行できます。 UI テストは、言語とフレームワークの幅広い選択肢（Java と Maven、Node と WebDriver.io、Selenium に基づいて構築されたその他のフレームワークとテクノロジーなど）を可能にするために Docker イメージにパッケージ化された Selenium ベースのテストです。UIの作成方法とUIテストの作成方法について詳しくは、こちらを参照してください。 また、AEMプロジェクトアーキタイプを使用すると、UIテストプロジェクトを簡単に生成できます。

ユーザーは、（GIT経由で）カスタムテストを作成し、UIのテストスイートを作成できます。 UIテストは、各Cloud Managerパイプラインの特定の品質ゲートの一部として、それぞれのステップとフィードバック情報と共に実行されます。 回帰や新しい機能を含むすべてのUIテストにより、エラーを検出し、顧客のコンテキスト内でレポートできます。

お客様のUIテストは、「カスタムUIテスト」の手順の下の実稼働パイプラインで自動的に実行されます。

Javaで記述されたHTTPテストであるカスタム機能テストとは異なり、UIテストは、[UIテストの作成](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/test-results/ui-testing.html?lang=en#building-ui-tests)で定義されている規則に従う限り、任意の言語で記述されたテストを含むドッカー画像にすることができます。

>[!NOTE]
>[AEMプロジェクトのアーキタイプ](https://github.com/adobe/aem-project-archetype/tree/master/src/main/archetype/ui.tests)に便利な構造と言語&#x200B;*（jsとwdio）*&#x200B;を基にして作業を開始することをお勧めします。

### お客様オプトイン{#customer-opt-in}

UIテストを作成して実行するには、UIテスト用のmavenサブモジュール（UI testsサブモジュールのpom.xmlファイルの横）の下にファイルを追加し、このファイルが構築された`tar.gz`ファイルのルートにあることを確認して、「オプトイン」する必要があります。

*ファイル名*: `testing.properties`

*目次*: `one line: ui-tests.version=1`

これがビルドされた`tar.gz`ファイルに含まれていない場合、UIテストのビルドと実行はスキップされます

>[!NOTE]
>2021年2月10日より前に作成された実稼働用パイプラインは、この節で説明するUIテストを使用するために更新する必要があります。 つまり、ユーザーは実稼働パイプラインを編集し、変更が行われなかった場合でも、UIから「**保存**」をクリックする必要があります。
>パイプラインの設定の詳細については、[CI-CDパイプラインの設定](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/configure-pipeline.html?lang=ja#using-cloud-manager)を参照してください。

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
