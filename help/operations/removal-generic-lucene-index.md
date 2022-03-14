---
title: 汎用 Lucene インデックスの削除
description: 汎用 Lucene インデックスの計画的な削除と、影響を受ける可能性のある方法について説明します。
exl-id: 3b966d4f-6897-406d-ad6e-cd5cda020076
source-git-commit: 940a01cd3b9e4804bfab1a5970699271f624f087
workflow-type: tm+mt
source-wordcount: '1349'
ht-degree: 0%

---

# 汎用 Lucene インデックスの削除 {#generic-lucene-index-removal}

Adobeは、「汎用 Lucene」インデックス (`/oak:index/lucene-*`) をAdobe Experience Manager as a Cloud Serviceから。 このインデックスはAEM 6.5 以降で非推奨となりました。このドキュメントでは、この決定の影響と、AEMインスタンスが影響を受けるかどうかを調べる方法の詳細を説明します。 また、クエリを変更する方法も含まれているので、汎用の Lucene インデックスなしでもクエリが引き続き機能します。

## 背景 {#background}

AEMでは、フルテキストクエリは次の関数を使用します。

* `jcr:contains()` JCR XPATH 内
* `CONTAINS` JCR-SQL2 の

このようなクエリでは、インデックスを使用しないと結果を返すことはできません。 パスまたはプロパティの制限のみを含むクエリとは異なり、インデックスが見つからない（したがってトラバーサルが実行される）フルテキスト制限を含むクエリは、常にゼロの結果を返します。

汎用の Lucene インデックス (`/oak:index/lucene-*`) は、ほとんどのリポジトリ階層に対してフルテキスト検索を提供するためにAEM 6.0/Oak 1.0 以降に存在しています（ただし、次のようなパスもあります）。 `/jcr:system` および `/var` は常にこのから除外されています。 ただし、このインデックスは、より具体的なノードタイプのインデックスに大きく置き換えられています ( 例： `damAssetLucene-*` の `dam:Asset` ノードタイプ ) で、フルテキスト検索とプロパティ検索の両方をサポートします。

AEM 6.5 では、汎用 Lucene インデックスは非推奨とマークされ、将来のバージョンで削除されることを示していました。 それ以降、次のログスニペットで示すようにインデックスが使用された場合に、WARN が記録されます。

```text
org.apache.jackrabbit.oak.plugins.index.lucene.LucenePropertyIndex This index is deprecated: /oak:index/lucene-2; it is used for query Filter(query=select [jcr:path], [jcr:score], * from [nt:base] as a where contains(*, 'search term') and isdescendantnode(a, '/content/mysite') /* xpath: /jcr:root/content/mysite//*[jcr:contains(.,"search term")] */ fullText="search" "term", path=/content/mysite//*). Please change the query or the index definitions.
```

最近のAEMバージョンでは、汎用 Lucene インデックスがごく少数の機能をサポートするために使用されています。 他のインデックスを使用するように修正されているか、このインデックスへの依存を削除するために変更されています。

例えば、次の例のような参照参照クエリでは、 `/oak:index/pathreference`（インデックスのみ） `String` JCR パスを検索する正規表現に一致するプロパティ値。

```text
//*[jcr:contains(., '"/content/dam/mysite"')]
```

大規模な顧客データボリュームをサポートするために、Adobeは、新しいAEMas a Cloud Service環境で汎用の Lucene インデックスを作成しなくなります。 さらに、Adobeは既存のリポジトリからインデックスを削除し始めます。 [タイムラインを見る](#timeline) 詳しくは、このドキュメントの末尾を参照してください。

Adobeは、 `costPerEntry` および `costPerExecution` 他のインデックスを確実に作成するためのプロパティ `/oak:index/pathreference` は、可能な限り好みに応じて使用します。

このインデックスに依存するクエリを使用する顧客アプリケーションは、他の既存のインデックスを利用するために即座に更新する必要があります。必要に応じてカスタマイズできます。 または、新しいカスタムインデックスを顧客アプリケーションに追加できます。 AEM as a Cloud Serviceでのインデックス管理の完全な手順については、 [インデックス作成ドキュメント。](/help/operations/indexing.md)

## 影響を受けてる？ {#are-you-affected}

汎用 Lucene インデックスは、現在、他の全文インデックスがクエリに対応できない場合に、フォールバックとして使用されます。 この非推奨のインデックスを使用すると、次のようなメッセージが WARN レベルで記録されます。

```text
org.apache.jackrabbit.oak.plugins.index.lucene.LucenePropertyIndex This index is deprecated: /oak:index/lucene-2; it is used for query Filter(query=select [jcr:path], [jcr:score], * from [nt:base] as a where contains(*, 'test') /* xpath: //*[jcr:contains(.,"test")] */ fullText="test", path=*). Please change the query or the index definitions.
```

状況によっては、Oak が別のフルテキストインデックス ( `/oak:index/pathreference`) を使用してフルテキストクエリをサポートしますが、クエリ文字列がインデックス定義の正規表現と一致しない場合、メッセージは WARN レベルで記録され、クエリは結果を返さない可能性が高くなります。

```text
org.apache.jackrabbit.oak.query.QueryImpl Potentially improper use of index /oak:index/pathReference with queryFilterRegex (["']|^)/ to search for value "test"
```

汎用 Lucene インデックスが削除されると、次に示すメッセージが、フルテキストクエリで適切なインデックス定義を見つけられない場合に、WARN レベルで記録されます。

```text
org.apache.jackrabbit.oak.query.QueryImpl Fulltext query without index for filter Filter(query=select [jcr:path], [jcr:score], * from [nt:base] as a where contains(*, 'test') /* xpath: //*[jcr:contains(.,"test")] */ fullText="test", path=*); no results will be returned
```

>[!IMPORTANT]
>
>**必要な顧客アクション**
>
> 前述の警告メッセージのいずれかがログに記録された場合は、異なるフルテキストインデックスを使用するためにクエリを再作業するか、クエリをサポートする新しいインデックスを指定する必要が生じる場合があります。
>
>次の節では、表示される依存関係のタイプと対処方法の詳細について説明します。

## 汎用 Lucene インデックスに対する潜在的な依存関係 {#potential-dependencies}

アプリケーションやAEMのインストールが、オーサーインスタンスとパブリッシュインスタンスの両方で汎用の Lucene インデックスに依存する場合がある領域は多数あります。

### パブリッシュインスタンス {#publish-instance}

#### カスタムアプリケーションクエリ {#custom-application-queries}

パブリッシュインスタンスで汎用 Lucene インデックスを使用するクエリの最も一般的なソースは、カスタムアプリケーションクエリです。

最も簡単な場合は、これは、次のように指定したノードタイプの指定のないクエリです。 `nt:base` または `nt:base` 次のように、明示的に指定されます。

```text
/jcr:root/content/mysite//*[jcr:contains(., 'search term')]
/jcr:root/content/mysite//element(*, nt:base)[jcr:contains(., 'search term')]
```

>[!IMPORTANT]
>
>**必要な顧客アクション**
>
>次の節で説明する適切なノードタイプを使用するように、前述のクエリを変更する必要があります。

例えば、クエリを変更して、ページに一致する結果や、 `cq:Page node`. クエリは次のようになります。

```text
/jcr:root/content/mysite//element(*, cq:Page)[jcr:contains(., 'search term')]
```

他のフルテキストインデックスでは処理できないフルテキスト制限が含まれている、ノードタイプを指定するクエリが含まれる場合もあります。例えば、次のような場合です。

```text
/jcr:root/content/dam//element(*, dam:Asset)[jcr:contains(jcr:content/metadata/@cq:tags, 'NewsTopics:cateogries/domestic'))]
```

この場合、クエリは `dam:Asset` ノードタイプですが、相対 `jcr:content/metadata/@cq:tags` プロパティ。

このプロパティは、 `damAssetLucene` index：最も一般的に使用されるフルテキストインデックスで、 `dam:Asset` ノードタイプ。 したがって、このインデックスはこのクエリには使用できません。

したがって、クエリは汎用のフルテキストインデックスにフォールバックし、含まれるすべてのプロパティが、ワイルドカードの一致によって分析済みとしてマークされます。 `/oak:index/lucene-2/indexRules/nt:base/properties/prop`.

>[!IMPORTANT]
>
>**必要な顧客アクション**
>
>を `jcr:content/metadata/@cq:tags` カスタムバージョンの `damAssetLucene` インデックスを作成すると、このインデックスでこのクエリが処理され、WARN は記録されません。

### オーサーインスタンス {#author-instance}

顧客アプリケーションサーブレット、OSGi コンポーネント、レンダリングスクリプトのクエリに加えて、汎用の Lucene インデックスには、作成者固有の用途が多数存在する場合があります。

#### 参照検索 {#reference-search}

従来、汎用 Lucene インデックスは、別のコンテンツパスへの参照を含むコンテンツの参照検索または検索をサポートするために使用されていました。 このようなクエリは、新しい `/oak:index/pathreference` 索引

#### パスフィールドピッカー検索 {#picker-search}

AEMには、Sling リソースタイプを持つカスタムダイアログコンポーネントが含まれます `granite/ui/components/coral/foundation/form/pathfield`：別のAEMパスを選択するためのブラウザー/ピッカーを提供します。 デフォルトのパスフィールドピッカー。カスタムパスがない場合に使用されます。 `pickerSrc` プロパティはコンテンツ構造で定義され、ポップアップダイアログボックスで検索バーをレンダリングします。

検索対象のノードタイプは、 `nodeTypes` プロパティ。

現時点で、 `nodeTypes` プロパティが存在する場合、基になる検索クエリは `nt:base` ノードタイプの場合は、一般的な Lucene インデックスを使用し、通常は次のような WARN メッセージをログに記録します。

```text
20.01.2022 18:56:06.412 *WARN* [127.0.0.1 [1642704966377] POST /mnt/overlay/granite/ui/content/coral/foundation/form/pathfield/picker.result.single.html HTTP/1.1] org.apache.jackrabbit.oak.plugins.index.lucene.LucenePropertyIndex This index is deprecated: /oak:index/lucene-2; it is used for query Filter(query=select [jcr:path], [jcr:score], * from [nt:base] as a where contains(*, 'test') and isdescendantnode(a, '/content') /* xpath: /jcr:root/content//element(*, nt:base)[(jcr:contains(., 'test'))] order by @jcr:score descending */ fullText="test", path=/content//*). Please change the query or the index definitions.
```

汎用の Lucene インデックスを削除する前に、 `pathfield` コンポーネントが更新され、デフォルトのピッカーを使用してコンポーネントの検索ボックスが非表示になります。このピッカーは、 `nodeTypes` プロパティ。

| 検索を使用したパスフィールドピッカー | 検索を使用しないパスフィールドピッカー |
|---|---|
| ![検索を使用したパスフィールドピッカー](assets/index-pathfield-picker-with-search.png) | ![検索を使用しないパスフィールドピッカー](assets/index-pathfield-picker-without-search.png) |

>[!IMPORTANT]
>
>**必要な顧客アクション**
>
>パスフィールドピッカー内に検索機能を保持したい場合は、 `nodeTypes` プロパティは、クエリ対象のノードタイプをリストして提供する必要があります。 これらは、 `String` プロパティ。 検索が必要ない場合は、お客様からのアクションは不要です。

>[!NOTE]
>
>コンテンツフラグメントモデルエディターは、Sling リソースタイプを持つ専用のパスフィールドを使用します `dam/cfm/models/editor/components/contentreference`.
> * 現時点では、これらのクエリはノードタイプが指定されていない状態で実行され、汎用の Lucene インデックスの使用が原因で WARN が記録されます。
> * これらのコンポーネントのインスタンスは間もなく、 `cq:Page` および `dam:Asset` 顧客の操作を必要としないノードタイプ
> * この `nodeTypes` プロパティを追加して、これらのデフォルトのノードタイプを上書きできます。


## 一般的な Lucene の削除のタイムライン {#timeline}

Adobeは、汎用の Lucene インデックスを削除する 2 段階アプローチを取ります。

* **フェーズ 1** （2022 年 1 月 31 日予定）:今後は作成しない `/oak:index/lucene-*` 新しいAEMas a Cloud Service環境の場合
* **フェーズ 2** （2022 年 3 月 31 日予定）:削除 `/oak:index/lucene-*` 既存のAEMas a Cloud Service環境からのインデックス

Adobeは上記のログメッセージを監視し、汎用の Lucene インデックスに依存し続けるお客様への連絡を試みます。

短期的な緩和として、Adobeは、カスタムインデックス定義を直接お客様のシステムに追加し、必要に応じて汎用 Lucene インデックスを削除した結果として機能やパフォーマンスの問題を回避します。

このような場合、お客様には更新されたインデックス定義が提供され、Cloud Manager を介してアプリケーションの将来のリリースにこれを含めるようお勧めします。
