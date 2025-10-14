---
title: コード品質テスト
description: パイプラインのコード品質テストの仕組みと、デプロイメントの品質を向上させる方法について説明します。
exl-id: e2981be9-fb14-451c-ad1e-97c487e6dc46
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
source-git-commit: 91a1fb46d4300540eeecf38f7f049a2991513d29
workflow-type: tm+mt
source-wordcount: '1166'
ht-degree: 97%

---

# コード品質テスト {#code-quality-testing}

パイプラインのコード品質テストの仕組みと、デプロイメントの品質を向上させる方法について説明します。

>[!CONTEXTUALHELP]
>id="aemcloud_nonbpa_codequalitytests"
>title="コード品質テスト"
>abstract="コード品質テストは、一連の品質ルールに基づいてアプリケーションコードを評価します。これはコード品質のみのパイプラインの主な目的であり、実稼動および非実稼動のすべてのパイプラインで、ビルド手順の直後に実行されます。"

## はじめに {#introduction}

コード品質テストは、一連の品質ルールに基づいてアプリケーションコードを評価します。これはコード品質のみのパイプラインの主な目的であり、実稼動および非実稼動のすべてのパイプラインで、ビルド手順の直後に実行されます。

様々なタイプのパイプラインの詳細については、[CI/CD パイプラインの設定](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md)を参照してください。

## コード品質ルール {#understanding-code-quality-rules}

コード品質テストでは、ソースコードをスキャンし、一定の品質基準を満たしていることを確認します。このステップは、SonarQube と、OakPAL を使用したコンテンツパッケージレベルの調査の組み合わせによって実装されます。汎用の Java ルールとAEM固有のルールを組み合わせたルールは 100 以上あります。 AEM固有のルールの一部は、AEM エンジニアリングのベストプラクティスに基づいており、[&#x200B; カスタムコード品質ルール &#x200B;](/help/implementing/cloud-manager/custom-code-quality-rules.md) と呼ばれます。

現在のルールの完全なリストをダウンロードするには、[このリンクを使用](/help/implementing/cloud-manager/assets/CodeQuality-rules-latest-CS.xlsx)します。

>[!IMPORTANT]
>
>2025年2月13日木曜日（PT）（Cloud Manager 2025.2.0）以降、Cloud Manager コード品質では、更新された SonarQube 9.9 バージョンと、[ここからダウンロード](/help/implementing/cloud-manager/assets/CodeQuality-rules-latest-CS-2024-12-0.xlsx)できる更新されたルールのリストが使用されます。

### 3 層評価 {#three-tiered-gate}

コード品質テストによって特定された問題は、3 つのカテゴリーのいずれかに分類されます。

* **重大** - パイプラインの即時失敗を引き起こす問題です。

* **重要** - パイプラインの一時停止状態を引き起こす問題です。 デプロイメントマネージャー、プロジェクトマネージャーまたはビジネスオーナーは、問題を無視して、パイプラインを続行することができます。または、問題を受け入れることもできますが、それによってエラーが発生した際にパイプラインが停止する可能性があります。

* **情報** - 情報提供だけを目的とした問題です。パイプライン実行には影響しません。

>[!NOTE]
>
>コード品質専用パイプラインでは、コード品質テストステップがパイプラインの最終ステップであるため、コード品質ゲートでの重要なエラーはオーバーライドできません。

### 評価 {#ratings}

このステップの結果は、**評価**&#x200B;として提供されます。

次の表に、重大、重要、情報の各カテゴリの評価と失敗のしきい値を示します。

| 名前 | 定義 | カテゴリ | 不合格のしきい値 |
|--- |--- |--- |--- |
| セキュリティ評価 | A = 脆弱性なし <br/>B = 軽度の脆弱性が 1 つ以上 <br/>C = 重要な脆弱性が 1 つ以上 <br/>D = 重大な脆弱性が 1 つ以上 <br/>E = 致命的な脆弱性が 1 つ以上 | 重大 | &lt; B |
| 信頼性評価 | A = バグなし <br/>B = 軽度のバグが 1 つ以上 <br/>C = 重要なバグが 1 つ以上 <br/>D = 重大なバグが 1 つ以上 <br>E = 致命的なバグが 1 つ以上 | 重大 | &lt; D |
| 保守性評価 | コードスメルの未処理の修正コストによって、アプリケーションに既に投入された時間の割合として定義されます。<br/><ul><li>A = &lt;=5%</li><li>B = 6～10%</li><li>C = 11～20%</li><li>D = 21～50%</li><li>E = >50%</li></ul> | 重要 | &lt; A |
| カバレッジ | 次の式を使用して、単体テストラインのカバレッジと条件のカバレッジを組み合わせて定義します。<br/>`Coverage = (CT + CF + LC)/(2*B + EL)`  <ul><li>`CT` = 単体テストの実行中に少なくとも 1 回は `true` と評価された条件</li><li>`CF` = 単体テストの実行中に少なくとも 1 回は `false` と評価された条件</li><li>`LC` = 被覆線 = lines_to_cover - uncovered_lines</li><li>`B` = 条件の合計数</li><li>`EL` = 実行可能な行の総数 (lines_to_cover)</li></ul> | 重要 | &lt; 50％ |
| スキップした単体テスト | スキップした単体テストの数 | 情報 | > 1 |
| 未解決の問題 | 問題の全体的なタイプ - 脆弱性、バグ、コードスメル | 情報 | > 0 |
| 重複行 | 重複したブロックに含まれる行の数として定義されます。 コードブロックは、次の条件下で重複していると見なされます。<br>Java 以外のプロジェクト：<ul><li>100 個以上の連続した重複トークンが必要です。</li><li>これらのトークンは、少なくとも次の場所に分散している必要があります。 </li><li>30 行の COBOL コード </li><li>20 行の ABAP コード </li><li>10 行の他言語コード</li></ul>Java プロジェクト：<ul></li><li> トークンと行の数にかかわらず、10 個以上の連続した重複ステートメントが必要です。</li></ul>重複を検出する際は、インデントの違いと文字列リテラルの違いは無視されます。 | 情報 | > 1％ |
| Cloud Service の互換性 | 特定された Cloud Service の互換性に関する問題の数 | 情報 | > 0 |

>[!NOTE]
>
>詳しくは、[SonarQube の指標の定義](https://docs.sonarsource.com/sonarqube-server/latest/user-guide/code-metrics/metrics-definition/)を参照してください。

>[!NOTE]
>
>[!UICONTROL Cloud Manager] で実行されるカスタムコード品質ルールについて詳しくは、[カスタムコード品質ルール](/help/implementing/cloud-manager/custom-code-quality-rules.md)を参照してください。

## 誤検出の処理 {#dealing-with-false-positives}

品質スキャンプロセスは完璧ではありません。実際には問題がないにもかかわらず、誤って問題として特定することもあります。この状態は&#x200B;**偽陽性**&#x200B;と呼ばれます。

この場合、ルール ID を注釈属性として指定した標準の Java `@SuppressWarnings` 注釈を使用して、ソースコードに注釈を付けることができます。 例えば、よくある問題の 1 つとして、ハードコードされたパスワードを検出する SonarQube ルールにおいて、ハードコードされたパスワードの識別方法が強引な場合があります。

次のコードは、AEM プロジェクトではかなり一般的です。AEM プロジェクトには、一部の外部サービスに接続するコードが含まれています。

```java
@Property(label = "Service Password")
private static final String PROP_SERVICE_PASSWORD = "password";
```

SonarQube は致命的脆弱性を報告します。コードを見直した後、この問題が脆弱性でないことを確認し、適切なルール ID でコードに注釈を付けることができます。

```java
@SuppressWarnings("squid:S2068")
@Property(label = "Service Password")
private static final String PROP_SERVICE_PASSWORD = "password";
```

ただし、コードが実際には次のような場合は、

```java
@Property(label = "Service Password", value = "mysecretpassword")
private static final String PROP_SERVICE_PASSWORD = "password";
```

ハードコードされたパスワードを削除するのが正しい解決策です。

>[!NOTE]
>
>`@SuppressWarnings` 注釈をできるだけ具体的なものにする（問題の原因となっている特定のステートメントやブロックにのみ注釈を付ける）ことをお勧めしますが、クラスレベルで注釈を付けることもできます。

>[!NOTE]
>明示的なセキュリティテスト手順はありませんが、コード品質手順の間に評価されるセキュリティ関連のコード品質ルールはあります。Cloud Service でのセキュリティの詳細については、[AEM as a Cloud Service のセキュリティの概要](/help/security/cloud-service-security-overview.md)を参照してください。

## コンテンツパッケージスキャンの最適化 {#content-package-scanning-optimization}

Cloud Manager は、品質分析プロセスの一環として、Maven ビルドで生成されたコンテンツパッケージの分析を実行します。Cloud Manager は、このプロセスを高速化するための最適化を提供します。この最適化は、特定のパッケージ化の制約が観察された場合に有効です。最も重要な最適化は、ビルドからの複数のコンテンツパッケージ（スキップ済みとしてマークされる）を含む単一の「すべて」のパッケージを生成するプロジェクトをターゲットにします。Cloud Manager がこのシナリオを検出すると、「すべて」のパッケージを展開するのではなく、個々のコンテンツパッケージを直接スキャンし、依存関係に基づいて並べ替えます。 例えば、次のビルド出力について考えてみましょう。

* `all/myco-all-1.0.0-SNAPSHOT.zip`（コンテンツパッケージ）
* `ui.apps/myco-ui.apps-1.0.0-SNAPSHOT.zip`（スキップされたコンテンツパッケージ）
* `ui.content/myco-ui.content-1.0.0-SNAPSHOT.zip`（スキップされたコンテンツパッケージ）

`myco-all-1.0.0-SNAPSHOT.zip` 内の唯一のアイテムがスキップされた 2 つのコンテンツパッケージである場合、「すべて」のコンテンツパッケージの代わりに 2 つの埋め込みパッケージがスキャンされます。

数十の埋め込みパッケージを生成するプロジェクトの場合、この最適化により、パイプライン実行あたり 10 分以上の時間を節約できることが示されています。

「すべて」のコンテンツパッケージに、スキップされたコンテンツパッケージと OSGi バンドルの組み合わせが含まれている場合は、特殊なケースが発生する場合があります。 例えば、`myco-all-1.0.0-SNAPSHOT.zip` に前述の 2 つの埋め込みパッケージと 1 つ以上の OSGi バンドルが含まれている場合、新しい最小限のコンテンツパッケージは OSGi バンドルのみで構築されます。 このパッケージは常に `cloudmanager-synthetic-jar-package` という名前で、含まれているバンドルは `/apps/cloudmanager-synthetic-installer/install` に配置されます。

>[!NOTE]
>
>* この最適化は、AEM にデプロイされるパッケージには影響しません。
>* 埋め込みコンテンツパッケージとスキップされたコンテンツパッケージの照合はファイル名に依存します。複数のスキップされたパッケージが同じファイル名を共有する場合や、埋め込み中にファイル名が変更された場合、この最適化は実行できません。
