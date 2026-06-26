---
title: Java &trade；機能テスト
description: AEM as a Cloud ServiceのJava &trade；機能テストの書き方を学ぶ
exl-id: e014b8ad-ac9f-446c-bee8-adf05a6b4d70
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Developer
source-git-commit: fe1c1efaa00fc117ae0dc35879662dfd5ed4ecc2
workflow-type: tm+mt
source-wordcount: '876'
ht-degree: 69%

---


# Java™機能テスト

AEM as a Cloud Service 用の Java™ 機能テストの作成方法を説明します

## 機能テストを始める {#getting-started-functional-tests}

Cloud Manager で新しいコードリポジトリを作成すると、サンプルテストケースを含む `it.tests` フォルダーが自動的に作成されます。

>[!NOTE]
>
>Cloud Managerが`it.tests`個のフォルダーを自動作成する前にリポジトリが作成された場合は、[AEM プロジェクトアーキタイプ &#x200B;](https://github.com/adobe/aem-project-archetype/tree/master/src/main/archetype/it.tests)を使用して最新バージョンを生成します。

`it.tests` フォルダーの内容を取得したら、独自のテストのベースとしてそれらを使用し、次の手順を実行できます。

1. [テストケースを作成します](#writing-functional-tests)。
1. [テストをローカルで実行します](#local-test-execution)。
1. コードを Cloud Manager リポジトリにコミットし、Cloud Manager パイプラインを実行します。

## カスタム機能テストの作成 {#writing-functional-tests}

アドビが製品機能テストの作成に使用するのと同じツールを、カスタム機能テストの作成に使用できます。 テストの作成方法の例として、GitHub の[製品機能テスト](https://github.com/adobe/aem-test-samples/tree/aem-cloud/smoke)を参照してください。

カスタム機能テストのコードは、プロジェクトの`it.tests` フォルダー内のJava™ コードです。 すべての機能テストを含む単一のJARを生成します。 ビルドで複数のテスト JARが生成される場合、選択されたJARは決定論的ではありません。 テスト JAR がゼロになる場合、テスト手順はデフォルトで合格します。 サンプルテストについては、[AEM プロジェクトのアーキタイプ](https://github.com/adobe/aem-project-archetype/tree/develop/src/main/archetype/it.tests)を参照してください。

テストは、少なくとも 2 つのオーサーインスタンス、2 つのパブリッシュインスタンス、Dispatcher 設定など、アドビが維持管理するテストインフラストラクチャで実行されます。 この設定により、カスタム機能テストがAEM環境全体に対して実行されます。

### 機能テストの構造 {#functional-tests-structure}

カスタム機能テストは、AEM にデプロイするアーティファクトと同じ Maven ビルドで生成される個別の JAR ファイルとしてパッケージ化する必要があります。 このビルドは別のMaven モジュールです。 結果のJAR ファイルには、必要なすべての依存関係が含まれている必要があり、`jar-with-dependencies`記述子を使用して`maven-assembly-plugin`を使用して作成されます。

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

例えば、`com.myco.tests.aem.it.ExampleIT`という名前のクラスは実行されますが、`com.myco.tests.aem.it.ExampleTest`という名前のクラスは実行されません。

さらに、コードスキャンのカバレッジチェックからテストコードを除外するには、テストコードを `it` という名前のパッケージの下に置く必要があります（カバレッジ除外フィルターは `**/it/**/*.java` です）。

テストクラスは、通常の JUnit テストである必要があります。 テストインフラストラクチャは、`aem-testing-clients` テストライブラリで使用される規則との互換性を持つように設計および設定されています。 開発者は、このライブラリを使用し、そのライブラリのベストプラクティスに従うことをお勧めします。

詳しくは、[`aem-testing-clients`GitHub リポジトリ](https://github.com/adobe/aem-testing-clients)を参照してください。

>[!TIP]
>
>カスタム機能テストを使用してCI/CD パイプラインを改善する方法については、[このビデオ &#x200B;](https://www.youtube.com/watch?v=yJX6r3xRLHU)を参照してください。

### 前提条件 {#prerequisites}

1. Cloud Managerのテストは、テクニカルアドミニストレーターユーザーを使用して実行されます。

>[!NOTE]
>
>ローカルマシンで機能テストを実行する際に同じ動作を保証するには、管理者権限を持つユーザーを作成します。

1. 次の境界により、機能テスト用にスコープ化されたコンテナ化インフラストラクチャが制限されます。

| 種類 | 値 | 説明 |
|----------------------|-------|--------------------------------------------------------------------|
| CPU | 0.5 | テスト実行ごとに確保される CPU 時間の量です。 |
| メモリ | 0.5 Gi | テストに割り当てられたメモリの量（値は GB 単位）です。 |
| タイムアウト | 30 m | テストが停止するまでの時間制限。 |
| 推奨期間 | 15 m | アドビは、この時間を超えないようにテストを作成することをお勧めします。 |

#### 依存関係

* aem-cloud-testing-clients：

機能テストを実行するためのコンテナ化されたインフラストラクチャの今後の変更では、カスタム機能テスト内の [aem-cloud-testing-clients](https://github.com/adobe/aem-testing-clients) ライブラリをバージョン **1.2.1** 以降にアップデートする必要があります。 `it.tests/pom.xml` ファイル内の依存関係が、それに応じてアップデートされていることを確認します。

```
<dependency>
   <groupId>com.adobe.cq</groupId>
   <artifactId>aem-cloud-testing-clients</artifactId>
   <version>1.2.1</version>
</dependency>
```

>[!NOTE]
>
>この変更は、2024年4月6日（PT）より前に実行する必要があります。依存関係ライブラリの更新に失敗すると、「カスタム機能テスト」手順でパイプラインにエラーが発生します。

### ローカルテストの実行 {#local-test-execution}

Cloud Manager パイプラインで機能テストをアクティブ化する前に、[AEM as a Cloud Service SDK](/help/implementing/developing/introduction/aem-as-a-cloud-service-sdk.md) または実際の AEM as a Cloud Service インスタンスを使用して、機能テストをローカルで実行することをお勧めします。

#### 統合開発環境（IDE）で実行 {#running-in-an-ide}

テストクラスは JUnit テストなので、Eclipse、IntelliJ、NetBeans などの主要な Java ™ IDE から実行できます。 製品機能テストとカスタム機能テストはどちらも同じテクノロジーに基づいているので、製品テストをカスタムテストにコピーすることで、両者をローカルで実行できます。

ただし、これらのテストを実行する際は、`aem-testing-clients`（および基礎となる Sling Testing Client）ライブラリで想定される様々なシステムプロパティを設定する必要があります。

これらのシステムプロパティは次のとおりです。

| プロパティ | 説明 | 例 |
|-------------------------------------|------------------------------------------------------------------|-------------------------|
| `sling.it.instances` | インスタンスの数は、クラウドサービスに合わせて `2` に設定する必要があります | `2` |
| `sling.it.instance.url.1` | オーサー URL に設定します。 | `http://localhost:4502` |
| `sling.it.instance.runmode.1` | 最初のインスタンスの実行モード。 `author` に設定します。 | `author` |
| `sling.it.instance.adminUser.1` | オーサー管理者ユーザーに設定します。 | `admin` |
| `sling.it.instance.adminPassword.1` | オーサー管理者パスワードに設定します。 |                         |
| `sling.it.instance.url.2` | パブリッシュ URL に設定します。 | `http://localhost:4503` |
| `sling.it.instance.runmode.2` | 2 番目のインスタンスの実行モード。 `publish` に設定します。 | `publish` |
| `sling.it.instance.adminUser.2` | パブリッシュ管理者ユーザーに設定します。 | `admin` |
| `sling.it.instance.adminPassword.2` | パブリッシュ管理者パスワードに設定します。 |                         |

#### Mavenを使用してすべてのテストを実行 {#using-maven}

1. シェルを開き、リポジトリの `it.tests` フォルダーに移動します。

1. Mavenを使用してテストを開始するために必要なパラメーターを指定して、次のコマンドを実行します。

```shell
mvn verify -Plocal \
    -Dit.author.url=https://author-<program-id>-<environment-id>.adobeaemcloud.com \
    -Dit.author.user=<user> \
    -Dit.author.password=<password> \
    -Dit.publish.url=https://publish-<program-id>-<environment-id>.adobeaemcloud.com \
    -Dit.publish.user=<user> \
    -Dit.publish.password=<password>
```
