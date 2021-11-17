---
title: 機能テスト - Cloud Services
description: 機能テスト - Cloud Services
exl-id: 7eb50225-e638-4c05-a755-4647a00d8357
source-git-commit: 2bb72c591d736dd1fe709abfacf77b02fa195e4c
workflow-type: tm+mt
source-wordcount: '946'
ht-degree: 87%

---

# 機能テスト {#functional-testing}


>[!CONTEXTUALHELP]
>id="aemcloud_nonbpa_functionaltesting"
>title="機能テスト"
>abstract="機能テストは、製品機能テスト、カスタム機能テスト、カスタム UI テストの 3 つのタイプに分類されます。"

機能テストは次の 2 つのタイプに分類されます。


* 製品機能テスト
* カスタム機能テスト
* カスタム UI テスト

## 製品機能テスト {#product-functional-testing}

製品機能テストは、AEM のコア機能（オーサリングやレプリケーションなど）に関する安定した HTTP 統合テスト（IT）のセットです。これを実行することで、顧客によるアプリケーションコードの変更がこのコア機能に障害が発生させる場合、その変更がデプロイされるのを防ぎます。

製品機能テストは、顧客が新しいコードを Cloud Manager にデプロイするたびに自動的に実行され、省略することはできません。

サンプルテストについては、[製品機能テスト](https://github.com/adobe/aem-test-samples/tree/aem-cloud/smoke)を参照してください。

## カスタム機能テスト {#custom-functional-testing}

パイプライン内のカスタム機能テストステップは常に存在し、スキップできません。

ビルドでは、0 または 1 つのテスト JAR を生成する必要があります。 テスト JAR がゼロになる場合、テスト手順はデフォルトで合格します。 ビルドによって複数のテスト JAR が生成される場合、どの JAR が非決定的に選択されるかは非決定的です。

>[!NOTE]
>「**ログをダウンロード**」ボタンを使用すると、テスト実行詳細フォームのログを格納した ZIP ファイルにアクセスできます。これらのログには、実際の AEM ランタイムプロセスのログは含まれていません。それらについては、通常のダウンロードログまたはテールログ機能を使用してアクセスできます。詳しくは、[ログのアクセスと管理](/help/implementing/cloud-manager/manage-logs.md)を参照してください。

## カスタム UI テスト {#custom-ui-testing}

AEM では、Cloud Manager 統合スイートの品質ゲートを顧客に提供して、アプリケーションをスムーズに更新できるようにしています。特に、IT テストゲートを使用すると、AEM API を使用する独自のテストを作成および自動化できます。

カスタム UI テスト機能は [オプション機能](#customer-opt-in) これにより、お客様は、アプリケーションの UI テストを作成し、自動的に実行できます。 UI テストは、言語とフレームワークの幅広い選択肢（Java と Maven、Node と WebDriver.io、Selenium に基づいて構築されたその他のフレームワークとテクノロジーなど）を可能にするために Docker イメージにパッケージ化された Selenium ベースのテストです。UI の構築方法と UI テストの作成方法について詳しく学ぶことができます。また、AEM プロジェクトアーキタイプを使用すると、UI テストプロジェクトを容易に生成できます。

ユーザーは、（GIT 経由で）カスタムテストや、UI のテストスイートを作成できます。UI テストは、各 Cloud Manager パイプラインの特定の品質ゲートの一部として、それぞれの手順およびフィードバック情報を使用して実行されます。リグレッションや新機能を含む UI テストは、顧客の状況に応じてエラーを検出し、報告することができます。

顧客 UI テストは、「カスタム UI テスト」の実稼動パイプラインで自動的に実行されます。

UI テストは、Java で記述された HTTP テストのカスタム機能テストとは異なり、[UI テストの作成](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/test-results/ui-testing.html?lang=ja#building-ui-tests)で定義されている規則に従う限り、任意の言語で記述されたテストを含む Docker イメージにすることができます。

>[!NOTE]
>[AEM プロジェクトのアーキタイプ](https://github.com/adobe/aem-project-archetype/tree/master/src/main/archetype/ui.tests)で提供されている構造と言語&#x200B;*（js と wdio）*&#x200B;を基にして作業を開始することをお勧めします。

### 顧客オプトイン {#customer-opt-in}

UI テストを作成して実行するには、UI テスト用の maven サブモジュール（UI テストサブモジュールの pom.xml ファイルの隣）の下のコードリポジトリーにファイルを追加して「オプトイン」し、構築された `tar.gz` ファイルのルートにこのファイルがあることを確認する必要があります。

*ファイル名*：`testing.properties`

*目次*：`ui-tests.version=1`

これが構築された `tar.gz` ファイルに含まれていない場合、UI テストの構築と実行はスキップされます

構築されたアーティファクトに `testing.properties` ファイルを追加するには、（UI テストサブモジュール内の）`assembly-ui-test-docker-context.xml` ファイルに次の `include` ステートメントを追加します。

    ```
    [...]
    &lt;includes>
    &lt;include>Dockerfile&lt;/include>
    &lt;include>wait-for-grid.sh&lt;/include>
    &lt;include>testing.properties&lt;/include> &lt;! - opt-in test module in Cloud Manager -->
    &lt;/includes>
    [...]
    ```

>[!NOTE]
>2021 年 2 月 10 日より前に作成された実稼動用パイプラインの場合、ここで説明した UI テストを使用するには、更新が必要となります。つまり、変更がない場合でも、実稼動パイプラインを編集し、UI から「**保存**」をクリックする必要があります。
>様々なタイプのパイプライン設定の詳細については、[CI/CD パイプラインの設定](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/configure-pipeline.html?lang=ja#using-cloud-manager)を参照してください。

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

この JAR ファイル内で、実行する実際のテストのクラス名はで終わる必要があります。 `IT`.

例えば、 `com.myco.tests.aem.it.ExampleIT` が実行されますが、 `com.myco.tests.aem.it.ExampleTest` そうではありません。

さらに、コードスキャンのカバレッジチェックからテストコードを除外するには、テストコードをという名前のパッケージの下に置く必要があります。 `it` ( 有効範囲除外フィルターは `**/it/**/*.java`) をクリックします。

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
