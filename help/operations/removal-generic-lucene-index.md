---
title: 汎用 Lucene インデックスの削除
description: 汎用 Lucene インデックスの計画的な削除と、それによって受ける可能性がある影響について説明します。
exl-id: 3b966d4f-6897-406d-ad6e-cd5cda020076
source-git-commit: 940a01cd3b9e4804bfab1a5970699271f624f087
workflow-type: ht
source-wordcount: '1349'
ht-degree: 100%

---

# 汎用 Lucene インデックスの削除 {#generic-lucene-index-removal}

アドビでは、Adobe Experience Manager as a Cloud Service から「汎用 Lucene」インデックス（`/oak:index/lucene-*`）を削除する予定です。このインデックスは AEM 6.5 以降で非推奨（廃止予定）となりました。このドキュメントでは、この決定の影響と、AEM インスタンスが影響を受けるかどうかを調べる方法の詳細について説明します。また、汎用の Lucene インデックスなしでもクエリが引き続き機能するようにクエリを変更する方法についても触れます。

## 背景 {#background}

AEM では、フルテキストクエリは次の関数を使用します。

* `jcr:contains()`（JCR XPATH 内）
* `CONTAINS`（JCR-SQL2 内）

このようなクエリでは、インデックスを使用せずに結果を返すことはできません。パスまたはプロパティの制限のみを含んだクエリとは異なり、インデックスが見つからない（したがってトラバーサルが実行される）フルテキスト制限を含んだクエリは、常にゼロの結果を返します。

汎用の Lucene インデックス（`/oak:index/lucene-*`）は、ほとんどのリポジトリ階層に対するフルテキスト検索機能を提供するために AEM 6.0／Oak 1.0 以降に存在してきましたが、`/jcr:system` や `/var` など、一部のパスは常にこの階層から除外されてきました。ただし、このインデックスは、より具体的なノードタイプのインデックス（例：`dam:Asset` ノードタイプの `damAssetLucene-*`）にほとんど置き換わっており、後継のインデックスでは、フルテキスト検索とプロパティ検索の両方をサポートしています。

AEM 6.5 で汎用 Lucene インデックスは非推奨（廃止予定）としてマークされ、今後のバージョンで削除されることが明示されました。それ以降は、次のログスニペットで示すように、このインデックスが使用された場合に、警告が記録されてきました。

```text
org.apache.jackrabbit.oak.plugins.index.lucene.LucenePropertyIndex This index is deprecated: /oak:index/lucene-2; it is used for query Filter(query=select [jcr:path], [jcr:score], * from [nt:base] as a where contains(*, 'search term') and isdescendantnode(a, '/content/mysite') /* xpath: /jcr:root/content/mysite//*[jcr:contains(.,"search term")] */ fullText="search" "term", path=/content/mysite//*). Please change the query or the index definitions.
```

最近の AEM バージョンでは、ごく少数の機能をサポートするために汎用 Lucene インデックスが使用されてきました。これらは、他のインデックスを使用するように修正されつつあるか、このインデックスへの依存をなくすために変更されつつあります。

例えば、次の例にあるような参照ルックアップクエリでは、`/oak:index/pathreference` でインデックスを使用するようになりました。これは、JCR パスを探す正規表現に一致する `String` プロパティ値に対してのみインデックスを作成します。

```text
//*[jcr:contains(., '"/content/dam/mysite"')]
```

アドビは、大規模な顧客データボリュームをサポートするために、新しい AEM as a Cloud Service 環境においては汎用 Lucene インデックスを作成しなくなります。さらに、アドビでは、既存リポジトリからのこのインデックスの削除を開始します。詳しくは、このドキュメントの末尾で示されている[タイムライン](#timeline)を参照してください。

アドビでは、`costPerEntry` および `costPerExecution` プロパティを使用してインデックスコストを既に調整しており、`/oak:index/pathreference` などの他のインデックスが可能な限り環境設定で使用されるようにしています。

このインデックスにまだ依存しているクエリを使用する顧客アプリケーションは、他の既存のインデックスを利用するように直ちに更新してください。必要に応じて、インデックスをカスタマイズできます。または、新しいカスタムインデックスを顧客アプリケーションに追加できます。AEM as a Cloud Service でのインデックス管理の詳しい手順については、[インデックス作成に関するドキュメント](/help/operations/indexing.md)を参照してください。

## 影響を受けるユーザー {#are-you-affected}

汎用 Lucene インデックスは、現在、他のフルテキストインデックスでクエリに対応できない場合のフォールバックとして使用されています。この非推奨インデックスを使用すると、次のようなメッセージが WARN レベルで記録されます。

```text
org.apache.jackrabbit.oak.plugins.index.lucene.LucenePropertyIndex This index is deprecated: /oak:index/lucene-2; it is used for query Filter(query=select [jcr:path], [jcr:score], * from [nt:base] as a where contains(*, 'test') /* xpath: //*[jcr:contains(.,"test")] */ fullText="test", path=*). Please change the query or the index definitions.
```

状況によっては、Oak が別のフルテキストインデックス（`/oak:index/pathreference` など）を使用してフルテキストクエリをサポートしようとする可能性がありますが、クエリ文字列がインデックス定義の正規表現と一致しない場合は、メッセージが WARN レベルで記録され、クエリは結果を返さない可能性があります。

```text
org.apache.jackrabbit.oak.query.QueryImpl Potentially improper use of index /oak:index/pathReference with queryFilterRegex (["']|^)/ to search for value "test"
```

汎用 Lucene インデックスが削除されると、フルテキストクエリで適切なインデックス定義が見つからない場合、次に示すようなメッセージが WARN レベルで記録されます。

```text
org.apache.jackrabbit.oak.query.QueryImpl Fulltext query without index for filter Filter(query=select [jcr:path], [jcr:score], * from [nt:base] as a where contains(*, 'test') /* xpath: //*[jcr:contains(.,"test")] */ fullText="test", path=*); no results will be returned
```

>[!IMPORTANT]
>
>**顧客側で必要な対応**
>
> 前述の警告メッセージのいずれかがログに記録された場合は、別のフルテキストインデックスを使用するようにクエリを修正するか、クエリをサポートする新しいインデックスを指定する必要が生じる可能性があります。
>
>以下の節では、生じる可能性のある依存関係のタイプと対処方法の詳細について説明します。

## 汎用 Lucene インデックスに対する可能性のある依存関係 {#potential-dependencies}

アプリケーションや AEM インストールが、オーサーインスタンスであってもパブリッシュインスタンスであっても、汎用 Lucene インデックスに依存する可能性がある領域は多数あります。

### パブリッシュインスタンス {#publish-instance}

#### カスタムアプリケーションクエリ {#custom-application-queries}

パブリッシュインスタンスで汎用 Lucene インデックスを使用するクエリの最も一般的なソースは、カスタムアプリケーションクエリです。

最も簡単なケースは、例えば、クエリにノードタイプの指定がないので `nt:base` が暗示される場合や、`nt:base` が明示的に指定される場合です。

```text
/jcr:root/content/mysite//*[jcr:contains(., 'search term')]
/jcr:root/content/mysite//element(*, nt:base)[jcr:contains(., 'search term')]
```

>[!IMPORTANT]
>
>**顧客側で必要な対応**
>
>次の節で詳しく説明するように、適切なノードタイプを使用するように前述のクエリを変更する必要があります。

例えば、`cq:Page node` 下のページや任意の集計に一致する結果を返すように、クエリを変更することができます。この場合、クエリは次のようになります。

```text
/jcr:root/content/mysite//element(*, cq:Page)[jcr:contains(., 'search term')]
```

他には、クエリにノードタイプが指定されているものの、別のフルテキストインデックスでは処理できないフルテキスト制限が含まれている場合もあります。例えば、次のような場合です。

```text
/jcr:root/content/dam//element(*, dam:Asset)[jcr:contains(jcr:content/metadata/@cq:tags, 'NewsTopics:cateogries/domestic'))]
```

この場合、クエリはノードタイプが `dam:Asset` ですが、関連する `jcr:content/metadata/@cq:tags` プロパティに対するフルテキスト制限を含んでいます。

このプロパティは、`damAssetLucene` インデックスで分析済みとしてマークされていません。このインデックスは、`dam:Asset` ノードタイプに対するクエリで最も一般的に使用されるフルテキストインデックスです。したがって、このインデックスはこのクエリには使用できません。

その結果、クエリは汎用のフルテキストインデックスにフォールバックし、含まれているすべてのプロパティが、`/oak:index/lucene-2/indexRules/nt:base/properties/prop` のワイルドカード一致によって分析済みとしてマークされます。

>[!IMPORTANT]
>
>**顧客側で必要な対応**
>
>`damAssetLucene` インデックスのカスタムバージョンで `jcr:content/metadata/@cq:tags` プロパティを分析済みとしてマークすると、このクエリがこのインデックスで処理されることになり、WARN はログに記録されません。

### オーサーインスタンス {#author-instance}

顧客アプリケーションサーブレット、OSGi コンポーネントおよびレンダリングスクリプトでのクエリに加えて、汎用 Lucene インデックスには作成者固有の様々な用途が考えられます。

#### 参照検索 {#reference-search}

従来、汎用 Lucene インデックスは、参照検索つまり別のコンテンツパスへの参照を含んだコンテンツの検索をサポートするために使用されてきました。このようなクエリは、新しい `/oak:index/pathreference` インデックスを使用するように既に更新されています。

#### パスフィールドピッカー検索 {#picker-search}

AEM には、`granite/ui/components/coral/foundation/form/pathfield` の Sling リソースタイプを持つカスタムダイアログコンポーネントが含まれています。これは、別の AEM パスを選択するためのブラウザー／ピッカーとなります。デフォルトのパスフィールドピッカーは、カスタムの `pickerSrc` プロパティがコンテンツ構造で定義されていない場合に使用されるもので、ポップアップダイアログボックスに検索バーをレンダリングします。

検索対象となるノードタイプは、`nodeTypes` プロパティを使用して指定できます。

現在のところ、`nodeTypes` プロパティが存在しない場合、基になる検索クエリでは `nt:base` ノードタイプを使用するので、汎用 Lucene インデックスが使用される可能性が高く、通常は、次のような WARN メッセージがログに記録されます。

```text
20.01.2022 18:56:06.412 *WARN* [127.0.0.1 [1642704966377] POST /mnt/overlay/granite/ui/content/coral/foundation/form/pathfield/picker.result.single.html HTTP/1.1] org.apache.jackrabbit.oak.plugins.index.lucene.LucenePropertyIndex This index is deprecated: /oak:index/lucene-2; it is used for query Filter(query=select [jcr:path], [jcr:score], * from [nt:base] as a where contains(*, 'test') and isdescendantnode(a, '/content') /* xpath: /jcr:root/content//element(*, nt:base)[(jcr:contains(., 'test'))] order by @jcr:score descending */ fullText="test", path=/content//*). Please change the query or the index definitions.
```

汎用 Lucene インデックスが削除される前に、デフォルトのピッカーを使用しているコンポーネントに検索ボックスが表示されないように `pathfield` コンポーネントが更新されます。このようなコンポーネントは `nodeTypes` プロパティを提供しません。

| 検索機能を持つパスフィールドピッカー | 検索機能を持たないパスフィールドピッカー |
|---|---|
| ![検索機能を持つパスフィールドピッカー](assets/index-pathfield-picker-with-search.png) | ![検索機能を持たないパスフィールドピッカー](assets/index-pathfield-picker-without-search.png) |

>[!IMPORTANT]
>
>**顧客側で必要な対応**
>
>パスフィールドピッカー内に検索機能を保持したい場合は、クエリ対象となるノードタイプをリストした `nodeTypes` プロパティを提供する必要があります。これらは、ノードタイプのコンマ区切りリストとして `String` プロパティに指定することができます。検索機能が必要ない場合は、顧客側での対応は不要です。

>[!NOTE]
>
>コンテンツフラグメントモデルエディターでは、`dam/cfm/models/editor/components/contentreference` の Sling リソースタイプを持つ専用のパスフィールドを使用します。
> * 現在のところ、これらはノードタイプが指定されていないクエリを実行するので、汎用 Lucene インデックスの使用に起因する WARN がログに記録されます。
> * これらのコンポーネントのインスタンスでは間もなく、自動的に `cq:Page` および `dam:Asset` ノードタイプをデフォルトで使用するようになるので、顧客側でのさらなる対応は必要ありません。
> * `nodeTypes` プロパティを追加して、これらのデフォルトのノードタイプをオーバーライドできます。


## 汎用 Lucene インデックスの削除のタイムライン {#timeline}

アドビでは、2 段階アプローチで汎用 Lucene インデックスを削除します。

* **フェーズ 1**（2022年1月31日開始予定）：新しい AEM as a Cloud Service 環境では `/oak:index/lucene-*` は作成されなくなります。
* **フェーズ 2**（2022年3月31日開始予定）：既存の AEM as a Cloud Service 環境から `/oak:index/lucene-*` インデックスを削除します。

アドビでは前述のログメッセージを監視し、汎用 Lucene インデックスをまだ利用しているお客様への連絡を試みます。

短期的な緩和策として、アドビでは、必要に応じて、カスタムインデックス定義を直接お客様のシステムに追加して、汎用 Lucene インデックスの削除に起因する機能の問題やパフォーマンスの問題を防止します。

このような場合、お客様には、更新されたインデックス定義が提供され、Cloud Manager を使用してアプリケーションの今後のリリースにそれを組み込むように助言されます。
