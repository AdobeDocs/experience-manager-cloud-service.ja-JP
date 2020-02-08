---
title: テスト結果の把握 — クラウドサービス
description: テスト結果の理解 — クラウドサービス
translation-type: tm+mt
source-git-commit: 57206e36725e28051b2468d47da726e318bd763b

---


# Understanding your Test Results {#understand-test-results}

クラウドサービス用のCloud Managerのパイプライン実行は、ステージ環境に対して実行するテストの実行をサポートします。 これは、実行中のAEM環境にアクセスせずに、オフラインで実行されるビルドとユニットのテストのステップ中に実行されるテストとは対照的です。
このコンテキストでは、次の2種類のテストが実行されます。
* お客様が作成したテスト
* アドビが作成したテスト

両方のタイプのテストは、これらのタイプのテストを実行するために設計されたコンテナ化されたインフラストラクチャで実行されます。


## コード品質テスト {#code-quality-testing}

パイプラインの一環として、ソースコードをスキャンし、デプロイメントが特定の品質条件を満たしているかどうかを確認します現在、これは SonarQube と、OakPAL を使用したコンテンツパッケージレベルの調査を組み合わせて実装されています。汎用の Java ルールと AEM 固有のルールを組み合わせた 100 以上のルールがあります。テスト条件の評価の概要を次の表に示します。

| 名前 | 定義 | カテゴリ | 不合格のしきい値 |
|--- |--- |--- |--- |
| セキュリティ評価 | A = 脆弱性なし <br/>B = 軽度の脆弱性が 1 つ以上<br/>C = 重要な脆弱性が 1 つ以上 <br/>C = の重大な脆弱性が 1 つ以上 <br/>E = 致命的な脆弱性が 1 つ以上 | 重大 | &lt; B |
| 信頼性評価 | A = バグなし <br/>B = 軽度のバグが 1 つ以上 <br/>C = 重要なバグが 1 つ以上 <br/>D = 重大なバグが 1 つ以上 E = 致命的なバグが 1 つ以上 | 重要 | &lt; C |
| 保守性評価 | コードスメルに対する未処理の修正コスト：<br/><ul><li>アプリケーションに既に投入された時間の 5% 以下であれば、評価は A </li><li>上記時間の 6 ～ 10% であれば、評価は B </li><li>上記時間の 11 ～ 20% であれば、評価は C </li><li>上記時間の 21 ～ 50% であれば、評価は D</li><li>上記時間の 50% を超えれば、評価は E</li></ul> | 重要 | &lt; A |
| カバレッジ | ユニットテストのラインカバレッジと条件カバレッジを次の式で計算した結果：<br/>`Coverage = (CT + CF + LC)/(2*B + EL)`<br/> CT = ユニットテスト実行中に 1 回以上「真」と評価された条件の数 <br/>CF = ユニットテスト実行中に 1 回以上「偽」と評価された条件の数 <br/>LC = 実行された行の数 = lines_to_cover - uncovered_lines <br/><br/> B = 条件の合計数 <br/>EL = 実効行の合計数（lines_to_cover） | 重要 | &lt; 50% |
| スキップした単体テスト | スキップした単体テストの数。 | 情報 | > 1 |
| 未解決の問題 | 問題の全体的なタイプ - 脆弱性、バグ、コードスメル | 情報 | > 1 |
| 重複行 | 重複しているブロックに含まれている行の数。<br/>コードブロックが重複していると見なされるための条件：<br/><ul><li>**Java 以外のプロジェクトの場合：**</li><li>100 個以上の連続した重複トークンが必要です。</li><li>これらのトークンは、少なくとも次の場所に分散している必要があります。 </li><li>30 行の COBOL コード </li><li>20 行の ABAP コード </li><li>10 行の他言語コード</li><li>**Java プロジェクトの場合：**</li><li> トークンと行の数にかかわらず、10 個以上の連続した重複ステートメントが必要です。</li></ul> <br/>重複を検出する際は、インデントの違いと文字列リテラルの違いは無視されます。 | 情報 | > 1% |


>[!NOTE]
>
>詳しくは、[指標の定義](https://docs.sonarqube.org/display/SONAR/Metric+Definitions)を参照してください。

ここでルールの一覧 [code-quality-rules.xlsx](/help/implementing/cloud-manager/assets/CodeQuality-Rules-new-one.xlsx) をダウンロードできます。

>[!NOTE]
>
>[!UICONTROL Cloud Manager] で実行されるカスタムコード品質ルールについて詳しくは、[カスタムコード品質ルール](custom-code-quality-rules.md)を参照してください。

### 偽陽性の処理 {#dealing-with-false-positives}

品質スキャンプロセスは完璧ではなく、実際には問題がないにもかかわらず問題として誤って特定することもあります。これは「偽陽性」と呼ばれます。

この場合、ルール ID を注釈属性として指定した標準の Java `@SuppressWarnings` 注釈を使用して、ソースコードに注釈を付けることができます。例えば、よくある問題の 1 つとして、ハードコードされたパスワードを検出する SonarQube ルールにおいて、ハードコードされたパスワードの識別方法が強引な場合があります。

具体的な例を見てみましょう、次のコードは、一部の外部サービスに接続するコードを含んだ AEM プロジェクトではかなり一般的なものです。

```java
@Property(label = "Service Password")
private static final String PROP_SERVICE_PASSWORD = "password";
```

この場合、SonarQube は致命的脆弱性を報告します。コードを見直した後、これが脆弱性でないことを確認し、適切なルール ID でこれに注釈を付けることができます。

```java
@SuppressWarnings("squid:S2068")
@Property(label = "Service Password")
private static final String PROP_SERVICE_PASSWORD = "password";
```

一方、コードが実際には次のようになっていた場合は、

```java
@Property(label = "Service Password", value = "mysecretpassword")
private static final String PROP_SERVICE_PASSWORD = "password";
```

ハードコードされたパスワードを削除するのが正しい解決策です。

>[!NOTE]
>
>`@SuppressWarnings` 注釈をできるだけ具体的にすることをお勧めします。つまり、問題の原因となっている特定のステートメントまたはブロックにのみ注釈を付けます。ただし、クラスレベルで注釈を付けることもできます。

## 機能テストの作成 {#writing-functional-tests}

お客様が作成した機能テストは、AEMにデプロイするアーティファクトと同じMavenビルドによって生成される個別のJARファイルとしてパッケージ化する必要があります。 一般に、これは別のMavenモジュールになります。 結果のJARファイルには、必要な依存関係がすべて含まれている必要があり、通常はjar-with-dependencies記述子を使用してmaven-assembly-pluginを使用して作成されます。

さらに、JARには、Cloud-Manager-TestTypeマニフェストヘッダーがintegration-testに設定されている必要があります。 将来は、追加のヘッダー値がサポートされる予定です。 maven-assembly-pluginの設定例を次に示します。

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

このJARファイル内で、実行する実際のテストのクラス名はITで終わる必要があります。

例えば、という名前のクラスは実 `com.myco.tests.aem.ExampleIT` 行されますが、という名前のクラスは実 `com.myco.tests.aem.ExampleTest` 行されません。

テストクラスは、通常のJUnitテストである必要があります。 テストインフラストラクチャは、aem-testing-clientsテストライブラリで使用される規則との互換性を持つように設計および設定されています。 開発者は、このライブラリを使用し、ベストプラクティスに従うことを強くお勧めします。

## カスタム機能テスト {#custom-functional-test}

パイプライン内のカスタム機能のテスト手順は常に存在し、スキップできません。

ただし、ビルドによってテストJARが生成されない場合、テストはデフォルトで成功します。 この手順は、現在、ステージのデプロイメントの直後に実行されます。

> 注意：
>「 **Download Log** 」ボタンを使用すると、テスト実行の詳細フォームのログを含むZIPファイルにアクセスできます。 これらのログには、実際のAEMランタイムプロセスのログは含まれません。上記の通常のダウンロードログまたはテールログ機能を使用してアクセスできます。

## ローカルテストの実行 {#local-test-execution}

テストクラスはJUnitテストなので、Eclipse、IntelliJ、NetBeansなどの主要なJava IDEから実行できます。

ただし、これらのテストを必ず実行する場合は、aem-testing-clients（および基になるSling Testing Client）が期待する様々なシステムプロパティを設定する必要があります。

システムのプロパティは次のとおりです。

* `sling.it.instances - should be set to 2`
* `sling.it.instance.url.1 - should be set to the author URL, for example, http://localhost:4502`
* `sling.it.instance.runmode.1 - should be set to author`
* `sling.it.instance.adminUser.1 - should be set to the author admin user, e.g. admin`
* `sling.it.instance.adminPassword.1 - should be set to the author admin password`
* `sling.it.instance.url.2 - should be set to the author URL, for example, http://localhost:4503`
* `sling.it.instance.runmode.2 - should be set to publish`
* `sling.it.instance.adminUser.2 - should be set to the publish admin user, for example, admin`
* `sling.it.instance.adminPassword.2 - should be set to the publish admin password`