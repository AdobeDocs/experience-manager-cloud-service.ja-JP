---
title: AEMアプリケーションへのタグ付けの構築
description: カスタム AEM アプリケーション内のタグまたは拡張タグをプログラムで操作します
translation-type: tm+mt
source-git-commit: ce55065c3ae6a2350ed06811af76477df7c11291
workflow-type: tm+mt
source-wordcount: '769'
ht-degree: 30%

---


# AEMアプリケーションへのタグ付けの構築{#building-tagging-into-aem-applications}

このドキュメントでは、タグをプログラムで使用したり、カスタムAEMアプリケーション内でタグを拡張したりする目的で、

* [タグ付け API](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/tagging/package-summary.html)

が

* [タグフレームワーク](tagging-framework.md)

タグ付けに関する関連情報：

* コンテンツ作成者としてのタグ付けについて詳しくは、[タグ](/help/sites-cloud/authoring/features/tags.md)の使用を参照してください。
* タグの作成と管理、および適用されたコンテンツタグについては、管理者の観点から、「タグの管理」を参照してください。

## タグ付け API の概要 {#overview-of-the-tagging-api}

AEM の[タグフレームワーク](tagging-framework.md)の実装により、JCR API を使用してタグおよびタグコンテンツを管理できます。`TagManager` 値として `cq:tags` 文字列配列プロパティに入力したタグが重複しないように、既存でないタグを指す `TagID`タグは削除され、移動したタグや結合されたタグ `TagID`は更新されます。`TagManager` は、間違った変更を元に戻す JCR 監視リスナーを使用します。メインクラスは [com.day.cq.tagging](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/index.html?com/day/cq/tagging/package-summary.html) パッケージ内にあります。

* `JcrTagManagerFactory`  — のJCRベースの実装を返し `TagManager`ます。タグ付け API のリファレンス実装です。
* `TagManager`  — パスと名前によるタグの解決と作成を可能にします。
* `Tag`  — タグオブジェクトを定義します。

### JCR ベースの TagManager の取得 {#getting-a-jcr-based-tagmanager}

`TagManager`インスタンスを取得するには、JCR `Session`があり、`getTagManager(Session)`を呼び出す必要があります。

```java
@Reference
JcrTagManagerFactory jcrTagManagerFactory;

TagManager tagManager = jcrTagManagerFactory.getTagManager(session);
```

通常の Sling コンテキストでは、`TagManager` を `ResourceResolver` に適合させることもできます。

```java
TagManager tagManager = resourceResolver.adaptTo(TagManager.class);
```

### Tag オブジェクトの取得 {#retrieving-a-tag-object}

`Tag` は、既存のタグを解決するか新しいタグを作成することにより、`TagManager` を介して取得できます。

```java
Tag tag = tagManager.resolve("my/tag"); // for existing tags

Tag tag = tagManager.createTag("my/tag"); // for new tags
```

`Tags`をJCR `Nodes`にマッピングするJCRベースの実装の場合、リソース（例：`/content/cq:tags/default/my/tag`）がある場合は、Slingの`adaptTo`メカニズムを直接使用できます。

```java
Tag tag = resource.adaptTo(Tag.class);
```

タグは（ノードではなく）リソースから変換のみされることがありますが&#x200B;**、タグは、**&#x200B;ノードとリソースの両方に変換できます。

```java
Node node = tag.adaptTo(Node.class);
Resource node = tag.adaptTo(Resource.class);
```

>[!NOTE]
>
>`Node`はSling `Adaptable.adaptTo(Class)`メソッドを実装していないので、`Node`から`Tag`に直接適応させることはできません。

### タグの取得と設定 {#getting-and-setting-tags}

```java
// Getting the tags of a Resource:
Tag[] tags = tagManager.getTags(resource);

// Setting tags to a Resource:
tagManager.setTags(resource, tags);
```

### タグの検索 {#searching-for-tags}

```java
// Searching for the Resource objects that are tagged with the tag object:
Iterator<Resource> it = tag.find();

// Retrieving the usage count of the tag object:
long count = tag.getCount();

// Searching for the Resource objects that are tagged with the tagID String:
 RangeIterator<Resource> it = tagManager.find(tagID);
```

>[!NOTE]
>
>使用可能な `RangeIterator` を次に示します。
>
>`com.day.cq.commons.RangeIterator`

### タグの削除 {#deleting-tags}

```java
tagManager.deleteTag(tag);
```

### タグの複製 {#replicating-tags}

タグのタイプは `Replicator` なので、タグで複製サービス（`nt:hierarchyNode`）を使用できます。

```java
replicator.replicate(session, replicationActionType, tagPath);
```

## タグのガベージコレクター {#the-tag-garbage-collector}

タグガベージコレクターは、非表示で未使用のタグをクリーンアップするバックグラウンドサービスです。 非表示および未使用のタグは、`/content/cq:tags`の下のタグで、`cq:movedTo`プロパティを持ち、コンテンツノードでは使用されません。 0の数があります。 この遅延削除プロセスを使用すると、移動や結合操作の一環としてコンテンツノード（`cq:tags`プロパティ）を更新する必要がありません。 `cq:tags`プロパティの参照は、`cq:tags`プロパティが更新されると自動的に更新されます。例えば、ページプロパティダイアログを使用します。

タグガベージコレクターは、デフォルトで1日に1回実行されます。 これは、次の場所で設定できます。

`http://<host>:<port>/system/console/configMgr/com.day.cq.tagging.impl.TagGarbageCollector`

## タグ検索およびタグリスト {#tag-search-and-tag-listing}

タグおよびタグ一覧の検索は次のように動作します。

* `TagID`は、`cq:movedTo`プロパティ`TagID`が&lt;a2/>に設定され、`cq:movedTo` `TagID`をたどるタグを検索します。
* タグタイトルの検索では、`cq:movedTo`プロパティを持たないタグのみが検索されます。

## 他の言語のタグ {#tags-in-different-languages}

タグ`title`は異なる言語で定義できます。 次に、言語に依存するプロパティがタグノードに追加されます。 このプロパティは`jcr:title.<locale>`の形式を持ちます。例：`jcr:title.fr`（フランス語訳） `<locale>` は、小文字のISOロケール文字列である必要があります。次に例を示すように、ハイフン/ダッシュ(`_`)の代わりにアンダースコア(`-`)を使用します。 `de_ch`.

例えば、**Animals**&#x200B;タグを&#x200B;**Products**&#x200B;ページに追加すると、`stockphotography:animals`の値がノード`/content/wknd/en/products/jcr:content`のプロパティ`cq:tags`に追加されます。 翻訳は、タグノードから参照されます。

サーバー側 API には、ローカライズされた `title` 関連のメソッドがあります。

* [`com.day.cq.tagging.Tag`](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/index.html?com/day/cq/tagging/Tag.html)
   * `getLocalizedTitle(Locale locale)`
   * `getLocalizedTitlePaths()`
   * `getLocalizedTitles()`
   * `getTitle(Locale locale)`
   * `getTitlePath(Locale locale)`
* [`com.day.cq.tagging.TagManager`](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/index.html?com/day/cq/tagging/TagManager.html)
   * `canCreateTagByTitle(String tagTitlePath, Locale locale)`
   * `createTagByTitle(String tagTitlePath, Locale locale)`
   * `resolveByTitle(String tagTitlePath, Locale locale)`

AEMでは、ページ言語またはユーザー言語から言語を取得できます。

タグ付けの場合、ローカライズはコンテキストに依存します。タグの `titles` はページ言語、ユーザー言語またはそれ以外の任意の言語で表示することができます。

### タグを編集ダイアログへの新しい言語の追加 {#adding-a-new-language-to-the-edit-tag-dialog}

次の手順では、新しい言語（フィンランド語など）を&#x200B;**タグ編集**&#x200B;ダイアログに追加する方法を説明します。

1. **CRXDE**&#x200B;で、ノード`/content/cq:tags`の複数値のプロパティ`languages`を編集します。
1. 追加`fi_fi`。これはフィンランド語のロケールを表し、変更を保存します。

ページプロパティのタグダイアログと、**タグ付け**&#x200B;コンソールでタグを編集する際の&#x200B;**タグ**&#x200B;を編集ダイアログで、フィンランド語を使用できるようになりました。

>[!NOTE]
>
>新しい言語は、AEMで認識される言語の1つである必要があります。つまり、`/libs/wcm/core/resources/languages`の下のノードとして使用できる必要があります。
