---
title: コード品質テスト —Cloud Services
description: コード品質テスト —Cloud Services
translation-type: tm+mt
source-git-commit: b3548e3920fed45f6d1de54a49801d3971aa6bba
workflow-type: tm+mt
source-wordcount: '831'
ht-degree: 73%

---


# コード品質テスト {#code-quality-testing}

コード品質テストは、アプリケーションコードの品質を評価します。 これは、コード品質のみのパイプラインの中核となる目的で、実稼働環境と実稼働環境以外のすべてのパイプラインのビルド手順の直後に実行されます。

さまざまなタイプのパイプラインの詳細については、 [『CI-CDパイプラインの](/help/implementing/cloud-manager/configure-pipeline.md) 設定』を参照してください。

## Understanding Code Quality Rules {#understanding-code-quality-rules}

コード品質テストでは、ソースコードが特定の品質基準を満たしていることを確認するためにスキャンされます。 現在、これは SonarQube と、OakPAL を使用したコンテンツパッケージレベルの調査を組み合わせて実装されています。汎用の Java ルールと AEM 固有のルールを組み合わせた 100 以上のルールがあります。AEM固有のルールの一部は、AEM Engineeringのベストプラクティスに基づいて作成され、「 [カスタムコード品質ルール](/help/implementing/cloud-manager/custom-code-quality-rules.md)」と呼ばれます。

>[!NOTE]
>You can download the complete list of rules [here](/help/implementing/cloud-manager/assets/CodeQuality-rules-latest.xlsx).

**三段門**

このコード品質テスト手順では、特定された問題に対して3層の構造を使用します。

* **重大** - これらはゲートで特定される問題のうち、パイプラインの即時失敗につながるものです。

* **重要** - これらはゲートで特定される問題のうち、パイプラインの一時停止につながるものです。デプロイメントマネージャー、プロジェクトマネージャーまたはビジネスオーナーは、問題をオーバーライドできます。この場合、パイプラインは続行されます。または、問題を承認できます。この場合、パイプラインはエラーで停止します。

* **情報**:これらの問題は、ゲートによって識別される問題で、純粋に情報提供の目的で提供され、パイプラインの実行に影響を与えません。

この手順の結果は、 *評価として配信されます*。

次の表に、「重要」、「重要」、「情報」の各カテゴリの評価と失敗のしきい値を示します。

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


>[!NOTE]
>
>[!UICONTROL Cloud Manager] で実行されるカスタムコード品質ルールについて詳しくは、[カスタムコード品質ルール](/help/implementing/cloud-manager/custom-code-quality-rules.md)を参照してください。

## 偽陽性の処理 {#dealing-with-false-positives}

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
>明示的なセキュリティテスト手順はありませんが、コード品質手順の間に評価されるセキュリティ関連のコード品質ルールはあります。 Cloud Serviceでのセキュリティの詳細については、「 [Cloud ServiceとしてのAEMの](/help/security/cloud-service-security-overview.md) セキュリティの概要」を参照してください。
