---
title: テスト結果について - Cloud Services
description: テスト結果について - Cloud Services
translation-type: tm+mt
source-git-commit: ff9823f3d083ebc1dc5d130919144fe3678a13ed
workflow-type: tm+mt
source-wordcount: '1614'
ht-degree: 59%

---


# テスト結果について {#understand-test-results}

Cloud Services 用 Cloud Manager のパイプライン実行では、ステージ環境に対するテストの実行をサポートしています。これは、ビルドおよびユニットテストステップ中に実行されるテスト（オフラインで実行され、動作中の AEM 環境にはアクセスしない）とは対照的です。

Cloud ManagerのCloud Servicesパイプラインでサポートされるテストには、次の3つの大きなカテゴリがあります。

1. [コード品質テスト](#code-quality-testing)
1. [機能テスト](#functional-testing)
1. [コンテンツ監査テスト](#content-audit-testing)

次のテストが可能です。

* お客様が書いた
* Adobeで書かれた
* Powered by Lighthouse from Google as a open source tool

   >[!NOTE]
   > お客様が作成したテストとAdobeが作成したテストは、どちらも、これらのタイプのテストを実行するために設計されたコンテナ化されたインフラストラクチャで実行されます。


## コード品質テスト {#code-quality-testing}

パイプラインの一環として、ソースコードをスキャンし、デプロイメントが特定の品質条件を満たしているかどうかを確認します。現在、これは SonarQube と、OakPAL を使用したコンテンツパッケージレベルの調査を組み合わせて実装されています。汎用の Java ルールと AEM 固有のルールを組み合わせた 100 以上のルールがあります。テスト条件の評価の概要を次の表に示します。

| 名前 | 定義 | カテゴリ | 不合格のしきい値 |
|--- |--- |--- |--- |
| セキュリティ評価 | A = 脆弱性なし <br/>B = 軽度の脆弱性が 1 つ以上 <br/>C = 重要な脆弱性が 1 つ以上 <br/>C = の重大な脆弱性が 1 つ以上 <br/>E = 致命的な脆弱性が 1 つ以上 | 重大 | &lt; B |
| 信頼性評価 | A = バグなし <br/>B = 軽度のバグが 1 つ以上 <br/>C = 重要なバグが 1 つ以上 <br/>D = 重大なバグが 1 つ以上 E = 致命的なバグが 1 つ以上 | 重要 | &lt; C |
| 保守性評価 | コードスメルに対する未処理の修正コスト：<br/><ul><li>アプリケーションに既に投入された時間の 5％以下であれば、評価は A </li><li>上記時間の 6～10％であれば、評価は B </li><li>上記時間の 11～20％であれば、評価は C </li><li>上記時間の 21～50％であれば、評価は D</li><li>上記時間の 50％を超えれば、評価は E</li></ul> | 重要 | &lt; A |
| カバレッジ | ユニットテストのラインカバレッジと条件カバレッジを次の式で計算した結果：<br/>`Coverage = (CT + CF + LC)/(2*B + EL)`<br/> CT = ユニットテスト実行中に 1 回以上「真」と評価された条件の数 <br/>CF = ユニットテスト実行中に 1 回以上「偽」と評価された条件の数 <br/>LC = 実行された行の数 = lines_to_cover - uncovered_lines <br/><br/> B = 条件の合計数 <br/>EL = 実効行の合計数（lines_to_cover） | 重要 | &lt; 50％ |
| スキップした単体テスト | スキップした単体テストの数。 | 情報 | > 1 |
| 未解決の問題 | 問題の全体的なタイプ - 脆弱性、バグ、コードスメル | 情報 | > 0 |
| 重複行 | 重複しているブロックに含まれている行の数。<br/>コードブロックが重複していると見なされるための条件：<br/><ul><li>**Java 以外のプロジェクトの場合：**</li><li>100 個以上の連続した重複トークンが必要です。</li><li>これらのトークンは、少なくとも次の場所に分散している必要があります。 </li><li>30 行の COBOL コード </li><li>20 行の ABAP コード </li><li>10 行の他言語コード</li><li>**Java プロジェクトの場合：**</li><li> トークンと行の数にかかわらず、10 個以上の連続した重複ステートメントが必要です。</li></ul> <br/>重複を検出する際は、インデントの違いと文字列リテラルの違いは無視されます。 | 情報 | > 1％ |
| Cloud Service の互換性 | 識別された Cloud Service の互換性に関する問題の数です。 | 情報 | > 0 |


>[!NOTE]
>
>詳しくは、[指標の定義](https://docs.sonarqube.org/display/SONAR/Metric+Definitions)を参照してください。

ここでルールのリスト [code-quality-rules.xlsx](/help/implementing/cloud-manager/assets/CodeQuality-rules-latest.xlsx) をダウンロードできます。

>[!NOTE]
>
>[!UICONTROL Cloud Manager] で実行されるカスタムコード品質ルールについて詳しくは、[カスタムコード品質ルール](/help/implementing/cloud-manager/custom-code-quality-rules.md)を参照してください。

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

>[!NOTE]
>明示的なセキュリティテスト手順はありませんが、コード品質手順の間に評価されるセキュリティ関連のコード品質ルールはあります。 Refer to [Security Overview for AEM as a Cloud Service](/help/security/cloud-service-security-overview.md) for more details.

## 機能テスト {#functional-testing}

機能テストは、次の2つのタイプに分類されます。

* 製品機能テスト
* カスタム機能テスト

### 製品機能テスト {#product-functional-testing}

製品機能テストは、オーサリング、レプリケーションに関する安定したHTTP統合テスト(IT)のセットです。AEMのコア機能に障害が発生した場合に、アプリケーションコードに対する変更がデプロイされるのを防ぎます。
ユーザーがCloud Managerに新しいコードをデプロイすると、常に自動的に実行されます。

パイプライン内の製品機能のテスト手順は常に存在し、スキップすることはできません。この手順は、ステージ展開の直後に実行されます。

### カスタム機能テスト {#custom-functional-testing}

パイプライン内のカスタム機能テストステップは常に存在し、スキップできません。

ただし、ビルドでテスト JAR が生成されない場合、テストはデフォルトで合格します。

>[!NOTE]
>「**ログをダウンロード**」ボタンを使用すると、テスト実行詳細フォームのログを格納した ZIP ファイルにアクセスできます。これらのログには、実際の AEM ランタイムプロセスのログは含まれていません。それらについては、通常のダウンロードログまたはテールログ機能を使用してアクセスできます。Refer to [Accessing and Managing Logs](/help/implementing/cloud-manager/manage-logs.md) for more details.


#### 機能テストの作成 {#writing-functional-tests}

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

## コンテンツ監査テスト {#content-audit-testing}

コンテンツ監査は、GoogleのオープンソースツールであるLighthouseが提供するCloud Manager Sites Productionパイプラインで使用できる機能です。 この機能は、すべてのCloud Manager実稼働パイプラインで有効になります。

これにより、デプロイメントプロセスが検証され、次の変更がデプロイされていることを確認できます。

1. パフォーマンス、アクセシビリティ、ベストプラクティス、SEO（検索エンジンの最適化）、PWA（プログレッシブWebアプリ）の基準を満たします。

1. これらのディメンションに回帰を含めないでください。

Content Audit in Cloud Managerを使用すると、エンドユーザーのサイトでのデジタルエクスペリエンスを最高の基準に維持できます。 結果は情報提供であり、ユーザーはスコアおよび現在のスコアと以前のスコアの変化を確認できます。 この洞察は、現在のデプロイメントで導入される回帰があるかどうかを判断するのに役立ちます。

### コンテンツ監査結果について {#understanding-content-audit-results}

コンテンツ監査は、実稼働パイプラインの実行ページで集計と詳細なページレベルのテスト結果を提供します。

* 集計レベルの指標は、監査されたページ全体の平均スコアを測定します。
* 個々のページレベルスコアは、ドリルダウンでも使用できます。
* スコアの詳細を確認して、個々のテストの結果を確認し、コンテンツ監査中に特定された問題の是正方法に関するガイダンスを確認できます。
* テスト結果の履歴はCloud Manager内に保持されるので、パイプライン実行で発生する変更に以前の実行からの回帰が含まれているかどうかをお客様が確認できます。

#### 集計スコア {#aggregate-scores}

各テストタイプ(パフォーマンス、アクセシビリティ、SEO、ベストプラクティス、PWA)に対して集計レベルのスコアが割り当てられます。

集計レベルのスコアは、実行に含まれるページの平均スコアを取ります。 集計レベルでの変更は、含めるように設定されたページのコレクションが実行間で変更された場合でも、現在の実行中のページの平均スコアを、前回の実行時のスコアの平均と比較して表します。

「変更」指標の値は、次のいずれかになります。

* **正の値** — 前回の実稼動パイプライン実行以降、選択したテストのページが改善されました。

* **負の値** — 前回の実稼動パイプライン実行以降、選択したテストでページが退行した。

* **変更なし** — 前回の実稼動パイプライン実行以降、ページに同じスコアが割り当てられています。

* **該当なし** — 比較できる以前のスコアはありません。

   ![](assets/content-audit-test1.png)

#### ページレベルのスコア {#page-level-scores}

任意のテストにドリルダウンすると、より詳細なページレベルのスコアリングを確認できます。 ユーザーは、特定のテストで個々のページがどのようにスコアされたかと、前回のテスト実行時の変更を確認できます。

個々のページの詳細をクリックすると、評価されたページの要素に関する情報が表示され、改善の機会が検出された場合の問題の修正に関するガイダンスが示されます。 テストと関連ガイダンスの詳細は、Google Lighthouseから提供されます。

![](assets/page-level-scores.png)

## ローカルテストの実行 {#local-test-execution}

テストクラスは JUnit テストなので、Eclipse、IntelliJ、NetBeans などの主要な Java IDE から実行できます。

ただし、これらのテストを必ず実行する場合は、aem-testing-clients（およびそのベースとなる Sling Testing Client）で想定している様々なシステムプロパティを設定する必要があります。

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

