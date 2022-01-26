---
title: 汎用 Lucene インデックスの削除
description: 汎用 Lucene インデックスの削除
exl-id: fe0e00ac-f9c8-43cf-83c2-5a353f5eaeab
source-git-commit: bc7ef6567ad5baa4becd28a7e7d96bd6b579e1ad
workflow-type: tm+mt
source-wordcount: '1305'
ht-degree: 0%

---

# 「汎用 lucene」インデックスの削除

Adobeが「汎用 lucene」インデックス (`/oak:index/lucene-*`) をAdobe Experience Manager as a Cloud Serviceから。 このインデックスはAEM 6.5 以降で非推奨となりました。このドキュメントでは、この決定の影響と、AEMインスタンスが影響を受けるかどうかを調べる方法の詳細な説明を説明します。 最後に、クエリを変更する方法が含まれており、このインデックスが存在しない状態で動作します。

## 背景

AEMでは、次の関数を使用するクエリとして「fulltext」を指定します。

* `jcr:contains()` JCR XPATH 内
* `CONTAINS` JCR-SQL2 の

このようなクエリでは、インデックスを使用しないと結果を返すことはできません。 パスまたはプロパティの制限のみを含むクエリとは異なり、インデックスが見つからない（したがってトラバーサルが実行される）フルテキスト制限を含むクエリは、常に 0 個の結果を返します。

「汎用 lucene」インデックス (`/oak:index/lucene-*`) は、ほとんどのリポジトリ階層で全文検索を提供するためにAEM 6.0/Oak 1.0 以降に存在しています ( 例えば、 `/jcr:system` および `/var` 常にこのインデックスから除外されている ) が、このインデックスは、より具体的なノード型 ( 例えば、 `damAssetLucene-*` （「dam:Asset」ノードタイプ）のフルテキスト検索とプロパティ検索の両方をサポートします。

AEM 6.5 では、「汎用 lucene」インデックスは非推奨（今後のバージョンで削除されることを示）とマークされ、それ以降、インデックスが使用された際に WARN が記録されます。

```
org.apache.jackrabbit.oak.plugins.index.lucene.LucenePropertyIndex This index is deprecated: /oak:index/lucene-2; it is used for query Filter(query=select [jcr:path], [jcr:score], * from [nt:base] as a where contains(*, 'search term') and isdescendantnode(a, '/content/mysite') /* xpath: /jcr:root/content/mysite//*[jcr:contains(.,"search term")] */ fullText="search" "term", path=/content/mysite//*). Please change the query or the index definitions.
```

最近のAEMバージョンでは、「汎用 lucene」インデックスがごく少数の機能のサポートに使用されています。 他のインデックスを使用するように修正されているか、このインデックスへの依存を削除するために変更されています。
例えば、以下に示すフォームの「参照参照」クエリでは、「/oak:index/pathreference」（JCR パスを検索する正規表現に一致する String プロパティ値のみをインデックスとする）のインデックスを使用する必要があります。 

```
//*[jcr:contains(., '"/content/dam/mysite"')]
```

大規模な顧客データボリュームをサポートするために、Adobeは新しいAEMas a Cloud Service環境で「汎用 lucene」インデックスを作成しなくなり、その後、既存のリポジトリからインデックスを削除し始めます。 他のインデックス ( `/oak:index/pathreference`) は、 `/oak:index/lucene-*` 可能な限り 

このインデックスに依存するクエリを使用する顧客アプリケーションは、他の既存のインデックス（必要に応じてカスタマイズ可能）を利用するために直ちに更新するか、新しいカスタムインデックスを顧客アプリケーションに追加する必要があります。 AEM as a Cloud Serviceでのインデックス管理の完全な手順については、 [インデックス作成ドキュメント](/help/operations/indexing.md).

## アプリケーションが「汎用 Lucene」インデックスに依存しているかどうかを確認する方法

他のフルテキストインデックスがクエリに対してサービスを実行できない場合、「汎用 lucene」インデックスは現在「フォールバック」として使用されています。 この非推奨のインデックスを使用すると、次のようなメッセージが WARN レベルで記録されます。

```
org.apache.jackrabbit.oak.plugins.index.lucene.LucenePropertyIndex This index is deprecated: /oak:index/lucene-2; it is used for query Filter(query=select [jcr:path], [jcr:score], * from [nt:base] as a where contains(*, 'test') /* xpath: //*[jcr:contains(.,"test")] */ fullText="test", path=*). Please change the query or the index definitions.
```

状況によっては、Oak が別のフルテキストインデックス ( `/oak:index/pathreference`) を使用してフルテキストクエリをサポートしますが、クエリ文字列がインデックス定義の正規表現と一致しない場合、メッセージは WARN レベルで記録され、クエリは結果を返さない可能性が高くなります。

```
org.apache.jackrabbit.oak.query.QueryImpl Potentially improper use of index /oak:index/pathReference with queryFilterRegex (["']|^)/ to search for value "test"
```

「汎用 lucene」インデックスが削除されると、以下に示すメッセージが、フルテキストクエリで適切なインデックス定義を見つけられない場合、WARN レベルで記録されます。

```
org.apache.jackrabbit.oak.query.QueryImpl Fulltext query without index for filter Filter(query=select [jcr:path], [jcr:score], * from [nt:base] as a where contains(*, 'test') /* xpath: //*[jcr:contains(.,"test")] */ fullText="test", path=*); no results will be returned
```

これらのいずれかがログに記録される場合は、別のフルテキストインデックスを使用するためにクエリを再作業するか、クエリをサポートする新しいインデックスを指定する必要があります。 表示される依存関係のタイプと対処方法の詳細を以下に示します。

## 「汎用 lucene」インデックスに対する潜在的な依存関係

### 公開

#### カスタムアプリケーションクエリ

パブリッシュで「汎用 lucene」インデックスを使用するクエリの最も一般的なソースは、カスタムアプリケーションクエリです。

最も簡単なケースでは、次のようなノードタイプが指定されていないクエリ（「nt:base」を意味するクエリ）や nt:base が明示的に指定されているクエリが考えられます。

```
/jcr:root/content/mysite//*[jcr:contains(., 'search term')]
/jcr:root/content/mysite//element(*, nt:base)[jcr:contains(., 'search term')]
```

必要なアクション：これらのクエリは、適切なノードタイプを使用するように変更できます。例えば、一致するページ（または cq:Page ノードの下の「集計」のいずれか）を返す場合、クエリは次のようになります。

```
/jcr:root/content/mysite//element(*, cq:Page)[jcr:contains(., 'search term')]
```

他の場合は、クエリはノードタイプを指定しますが、次のような別のフルテキストインデックスで処理できないフルテキスト制限を含めることができます。

```
/jcr:root/content/dam//element(*, dam:Asset)[jcr:contains(jcr:content/metadata/@cq:tags, 'NewsTopics:cateogries/domestic'))]
```

この場合、クエリには「dam:Asset」ノードタイプが含まれますが、相対 `jcr:content/metadata/@cq:tags` プロパティ。

damAssetLucene インデックス（「dam:Asset」ノードタイプに対するクエリで最も一般的に使用されるフルテキストインデックス）では、このプロパティは「analysized」とマークされていないので、このクエリではこのインデックスを使用できません。

したがって、クエリは「汎用フルテキスト」インデックスにフォールバックし、含まれるすべてのプロパティが、ワイルドカードの一致で分析済みとしてマークされます。 `/oak:index/lucene-2/indexRules/nt:base/properties/prop`.

必要な顧客アクション：マーク `jcr:content/metadata/@cq:tags` プロパティをカスタムバージョンの damAssetLucene インデックスで「analysized」として指定すると、このクエリがこのインデックスで処理され、WARN が記録されなくなります。

### 作成者 

顧客アプリケーションサーブレット、OSGi コンポーネント、レンダリングスクリプトのクエリに加えて、「汎用 lucene」インデックスの作成者固有の使用方法も多数あります。 

#### 参照検索

従来、「汎用 lucene」インデックスは「参照検索」（別のコンテンツパスへの参照を含むコンテンツの検索）をサポートするために使用されていました。 このようなクエリは、新しい&#39;/oak:index/pathreference&#39;インデックスを使用するように既に移動しているはずです。
必要な顧客アクション：お客様の操作は不要です。


#### パスフィールドピッカー検索

AEMには、別のAEMパスを選択するためのブラウザー（ピッカー）を提供するカスタムダイアログコンポーネント（Sling リソースタイプ「granite/ui/components/coral/foundation/form/pathfield」）が含まれています。  デフォルトのパスフィールドピッカー（コンテンツ構造でカスタムの「pickerSrc」プロパティが定義されていない場合に使用）は、ポップアップダイアログボックスに検索バーをレンダリングします。
検索対象のノードタイプは、「nodeTypes」プロパティを使用して指定できます。

現時点では、「nodeTypes」プロパティが存在しない場合、基になる検索クエリは「nt:base」ノードタイプを使用するので、「generic lucene」インデックス（通常は以下に示す WARN メッセージをログに記録）を使用する可能性が高くなります。

```
20.01.2022 18:56:06.412 *WARN* [127.0.0.1 [1642704966377] POST /mnt/overlay/granite/ui/content/coral/foundation/form/pathfield/picker.result.single.html HTTP/1.1] org.apache.jackrabbit.oak.plugins.index.lucene.LucenePropertyIndex This index is deprecated: /oak:index/lucene-2; it is used for query Filter(query=select [jcr:path], [jcr:score], * from [nt:base] as a where contains(*, 'test') and isdescendantnode(a, '/content') /* xpath: /jcr:root/content//element(*, nt:base)[(jcr:contains(., 'test'))] order by @jcr:score descending */ fullText="test", path=/content//*). Please change the query or the index definitions.
```

「汎用 lucene」を削除する前に、「nodeTypes」プロパティを提供しないデフォルトのピッカーを使用してコンポーネントの検索ボックスが非表示になるように、パスフィールドコンポーネントが更新されます。

| 検索を使用したパスフィールドピッカー | 検索なしのパスフィールドピッカー |
|---|---|
| ![検索を使用したパスフィールドピッカー](assets/index-pathfield-picker-with-search.png) | ![検索なしのパスフィールドピッカー](assets/index-pathfield-picker-without-search.png) |


必要な顧客アクション：検索が必要ない場合は、お客様からのアクションは不要です。

顧客がパスフィールドピッカー内で検索機能を保持したい場合は、クエリ対象のノードタイプをリストするプロパティ「nodeTypes」を提供する必要があります。 これらは、String プロパティのノードタイプのコンマ区切りリストとして指定できます。


>[!NOTE]
>コンテンツフラグメントモデルエディターは、Sling リソースタイプ「dam/cfm/models/editor/components/contentreference」を持つ専用のパスフィールドを使用します。
> * 現時点では、これらのクエリはノードタイプが指定されていない状態で実行され、「汎用 lucene」インデックスの使用が原因で WARN が記録されます。
> * これらのコンポーネントのインスタンスは、近日中に、追加の顧客アクションがなくても、「cq:Page」と「dam:Asset」ノードタイプを使用するデフォルト設定が自動的に行われます。
> * 「nodeTypes」プロパティを追加して、これらのデフォルトのノードタイプを上書きできます。 





## 「汎用 lucene」を削除するタイムライン

Adobeは、「汎用 lucene」インデックスの削除に対して 2 段階アプローチを取る予定です。

**フェーズ 1** （2022 年 1 月 31 日予定）:新しいAEMas a Cloud Service環境で「/oak:index/lucene-*」を作成しなくなりました。

**フェーズ 2** （2022 年 3 月 31 日予定） :新しいAEMas a Cloud Service環境から「/oak:index/lucene-*」インデックスを削除します。

Adobeは上記のログメッセージを監視し、「汎用 lucene」インデックスに依存したままの顧客への連絡を試みます。

短期的な緩和として、必要に応じて、カスタムインデックス定義を顧客システムに直接追加し、「汎用 Lucene」インデックスの削除に伴う機能上またはパフォーマンス上の問題を防ぎます。

このような場合、お客様には更新されたインデックス定義が提供され、Cloud Manager を介してアプリケーションの将来のリリースにこれを含めるようお勧めします。
