---
title: Query Builder 用のカスタム述語エバリュエーターの実装
description: AEMオファーのクエリビルダーは、コンテンツリポジトリをクエリするための簡単でカスタマイズ可能な方法です
translation-type: tm+mt
source-git-commit: 21a0e6967a17ea30435d0343c4aa497f54134cda
workflow-type: tm+mt
source-wordcount: '0'
ht-degree: 0%

---


# Query Builder 用のカスタム述語エバリュエーターの実装 {#implementing-a-custom-predicate-evaluator-for-the-query-builder}

このドキュメントでは、カスタム述語評価演算子を実装して[クエリビルダー](query-builder-api.md)を拡張する方法を説明します。

## 概要 {#overview}

[クエリビルダー](query-builder-api.md)オファーを使用すると、コンテンツリポジトリを簡単にクエリできます。 AEMには、データのクエリに役立つ[述語評価演算子](#query-builder-predicates.md)のセットが付属しています。

しかし、カスタム述語エバリュエーターを実装することによって、複雑さを軽減し、セマンティックを向上させて、クエリを単純化することができます。

他にも、カスタム述語では、以下のような XPath では直接実行できないことも実行できます。

* 別のサービスからのデータのクエリ
* 計算に基づくカスタムフィルター

>[!NOTE]
>
>カスタム述語を実装する際は、パフォーマンスの問題を考慮する必要があります。

>[!TIP]
>
>クエリの例は、[クエリビルダー](query-builder-api.md)ドキュメントーにあります。

>[!TIP]
>
>このページのコードは GitHub にあります
>
>* [GitHubでaem-search-custom-predicate-evaluatorプロジェクトを開きます](https://github.com/Adobe-Marketing-Cloud/aem-search-custom-predicate-evaluator)
>* プロジェクトを [ZIP ファイル](https://github.com/Adobe-Marketing-Cloud/aem-search-custom-predicate-evaluator/archive/master.zip)としてダウンロードします


>[!NOTE]
>
>GitHubに関するこのリンクコードと、このドキュメントのコードスニペットは、デモ目的でのみ提供されています。

### 述語エバリュエーターの詳細 {#predicate-evaluator-in-detail}

述語エバリュエーターは、クエリの制約を定義する特定の述語を評価します。

高レベルの検索制約（`width>200`など）を、実際のコンテンツモデルに合う特定のJCRクエリ(例：`metadata/@width > 200`)。 ノードを手動でフィルタリングして、制約をチェックすることもできます。

>[!TIP]
>
>`PredicateEvaluator` および `com.day.cq.search` パッケージについて詳しくは、[Java のドキュメント](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/index.html?com/day/cq/search/package-summary.html)を参照してください。

### レプリケーションメタデータ用のカスタム述語エバリュエーターの実装 {#implementing-a-custom-predicate-evaluator-for-replication-metadata}

例として、レプリケーション・メタデータに基づくデータを支援するカスタム述語評価基準を作成する方法を説明します。

* `cq:lastReplicated`：最終レプリケーションアクションの日付を格納
* `cq:lastReplicatedBy`：最終レプリケーションアクションを呼び出したユーザーの ID を格納
* `cq:lastReplicationAction`：最終レプリケーションアクション（アクティベート、アクティベート解除など）を格納

#### デフォルトの述語エバリュエーターを使用したレプリケーションメタデータのクエリ {#querying-replication-metadata-with-default-predicate-evaluators}

次のクエリは、`admin`が年の初めからアクティブ化した`/content`ブランチのノードのリストを取得します。

```xml
path=/content

1_property=cq:lastReplicatedBy
1_property.value=admin

2_property=cq:lastReplicationAction
2_property.value=Activate

daterange.property=cq:lastReplicated
daterange.lowerBound=2013-01-01T00:00:00.000+01:00
daterange.lowerOperation=>=
```

このクエリは有効ですが、解読しにくく、3 つのレプリケーションプロパティ間の関係が一目ではわかりません。カスタム述語エバリュエーターを実装すると、複雑さが軽減され、このクエリのわかりやすさが向上します。

#### 目的 {#objectives}

`ReplicationPredicateEvaluator` の目的は、以下のような構文を使用して上記のクエリをサポートすることです。

```xml
path=/content

replic.by=admin
replic.since=2013-01-01T00:00:00.000+01:00
replic.action=Activate
```

レプリケーションメタデータ述語をカスタム述語評価子でグループ化すると、意味のあるクエリを作成するのに役立ちます。

#### Maven 依存関係の更新 {#updating-maven-dependencies}

>[!TIP]
>
>mavenを使用するなど、新しいAEMプロジェクトのセットアップは、[WKNDチュートリアルで詳しく説明されています。](develop-wknd-tutorial.md)

まず、プロジェクトの Maven 依存関係を更新する必要があります。`PredicateEvaluator` は `cq-search` アーティファクトの一部なので、Maven の pom ファイルに追加する必要があります。

>[!NOTE]
>
>`cq-search`依存関係の範囲は`provided`に設定されます。これは、`cq-search`が`OSGi`コンテナによって提供されるからです。

次のスニペットは、`pom.xml`ファイルの[unified diff形式](https://ja.wikipedia.org/wiki/Diff#.E3.83.A6.E3.83.8B.E3.83.95.E3.82.A1.E3.82.A4.E3.83.89.E5.BD.A2.E5.BC.8F_.28Unified_format.29)の違いを示しています

```text
@@ -120,6 +120,12 @@
             <scope>provided</scope>
         <dependency>
+            <groupid>com.day.cq</groupid>
+            <artifactid>cq-search</artifactid>
+            <version>5.6.4</version>
+            <scope>provided</scope>
+        </dependency>
+        <dependency>
             <groupid>junit</groupid>
             <artifactid>junit</artifactid>
             <version>3.8.1</version></dependency>
```

#### ReplicationPredicateEvaluator の作成 {#writing-the-replicationpredicateevaluator}

`cq-search`プロジェクトには`AbstractPredicateEvaluator`抽象クラスが含まれています。 これは、独自のカスタム述語評価演算子`(PredicateEvaluator`を実装するためのいくつかの手順で拡張できます)。

>[!NOTE]
>
>次の手順では、データをフィルタリングする `Xpath` 式を作成する方法について説明します。もう1つの方法は、行単位でデータを選択する`includes`メソッドを実装することです。 詳しくは、[Java のドキュメント](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/search/eval/PredicateEvaluator.html#includes28comdaycqsearchpredicatejavaxjcrqueryrowcomdaycqsearchevalevaluationcontext29)を参照してください。

1. `com.day.cq.search.eval.AbstractPredicateEvaluator` を拡張する新しい Java クラスを作成します。
1. [unified diff形式](https://en.wikipedia.org/wiki/Diff#Unified_format)に表示されるようなスニペットを`@Component`付けて、クラスに注釈を付けます。

   ```text
   @@ -19,8 +19,11 @@
     */
    package com.adobe.aem.docs.search;
   
   +import org.apache.felix.scr.annotations.Component;
   +import com.day.cq.search.eval.AbstractPredicateEvaluator;
   
   +@Component(metatype = false, factory = "com.day.cq.search.eval.PredicateEvaluator/repli")
    public class ReplicationPredicateEvaluator extends AbstractPredicateEvaluator {
   
    }
   ```

   >[!NOTE]
   >
   >`factory`は、`com.day.cq.search.eval.PredicateEvaluator/`で始まり、カスタム`PredicateEvaluator`の名前で終わる一意の文字列である必要があります。

   >[!NOTE]
   >
   >`PredicateEvaluator` の名前は述語名で、クエリを組み立てる際に使用されます。

1. オーバーライド：

   ```java
   public String getXPathExpression(Predicate predicate, EvaluationContext context)
   ```

   オーバーライドメソッドでは、引数に指定された `Xpath` に基づいて `Predicate` 式を組み立てます。

### レプリケーションメタデータのカスタム述語評価子の例{#example-of-a-custom-predicate-evaluator-for-replication-metadata}

この `PredicateEvaluator` の完全な実装は、次のクラスのようになります。

```java
/*
 * #%L
 * aem-docs-custom-predicate-evaluator
 * %%
 * Copyright (C) 2013 Adobe Research
 * %%
 * Licensed under the Apache License, Version 2.0 (the "License");
 * you may not use this file except in compliance with the License.
 * You may obtain a copy of the License at
 *
 *      http://www.apache.org/licenses/LICENSE-2.0
 *
 * Unless required by applicable law or agreed to in writing, software
 * distributed under the License is distributed on an "AS IS" BASIS,
 * WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
 * See the License for the specific language governing permissions and
 * limitations under the License.
 * #L%
 */

package com.adobe.aem.docs.search;

import org.apache.felix.scr.annotations.Component;
import org.slf4j.Logger;
import org.slf4j.LoggerFactory;

import com.day.cq.search.Predicate;
import com.day.cq.search.eval.AbstractPredicateEvaluator;
import com.day.cq.search.eval.EvaluationContext;

@Component(metatype = false, factory = "com.day.cq.search.eval.PredicateEvaluator/repli")

public class ReplicationPredicateEvaluator extends AbstractPredicateEvaluator {

    static final String PE_NAME = "replic";


    static final String PN_LAST_REPLICATED_BY = "cq:lastReplicatedBy";
    static final String PN_LAST_REPLICATED = "cq:lastReplicated";
    static final String PN_LAST_REPLICATED_ACTION = "cq:lastReplicationAction";

    static final String PREDICATE_BY = "by";
    static final String PREDICATE_SINCE = "since";
    static final String PREDICATE_SINCE_OP = " >= ";
    static final String PREDICATE_ACTION = "action";

    Logger log = LoggerFactory.getLogger(getClass());

    /**
     * Returns a XPath expression filtering by replication metadata.
     *
     * @see com.day.cq.search.eval.AbstractPredicateEvaluator#getXPathExpression(com.day.cq.search.Predicate,
     *      com.day.cq.search.eval.EvaluationContext)
     */

    @Override

    public String getXPathExpression(Predicate predicate,
            EvaluationContext context) {

        log.debug("predicate {}", predicate);

        String date = predicate.get(PREDICATE_SINCE);
        String user = predicate.get(PREDICATE_BY);
        String action = predicate.get(PREDICATE_ACTION);

        StringBuilder sb = new StringBuilder();

        if (date != null) {

            sb.append(PN_LAST_REPLICATED).append(PREDICATE_SINCE_OP);
            sb.append("xs:dateTime('").append(date).append("')");

        }

        if (user != null) {

            addAndOperator(sb);
            sb.append(PN_LAST_REPLICATED_BY);
            sb.append("='").append(user).append("'");

        }

        if (action != null) {

            addAndOperator(sb);
            sb.append(PN_LAST_REPLICATED_ACTION);
            sb.append("='").append(action).append("'");

        }

        String xpath = sb.toString();

        log.debug("xpath **{}**", xpath);

        return xpath;

    }

    /**
     * Add an and operator if the builder is not empty.
     *
     * @param sb a {@link StringBuilder} containing the query under construction
     */

    private void addAndOperator(StringBuilder sb) {

        if (sb.length() != 0) {

            sb.append(" and ");

        }

    }

}
```
