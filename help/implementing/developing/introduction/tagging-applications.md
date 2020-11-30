---
title: AEMアプリケーションへのタグ付けの構築
description: カスタム AEM アプリケーション内のタグまたは拡張タグをプログラムで操作します
translation-type: tm+mt
source-git-commit: ce55065c3ae6a2350ed06811af76477df7c11291
workflow-type: tm+mt
source-wordcount: '769'
ht-degree: 30%

---


# AEMアプリケーションへのタグ付けの構築 {#building-tagging-into-aem-applications}

このドキュメントでは、タグをプログラムで使用したり、カスタムAEMアプリケーション内でタグを拡張したりする目的で、

* [タグ付け API](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/tagging/package-summary.html)

が

* [タグフレームワーク](tagging-framework.md)

タグ付けに関する関連情報：

* コンテンツ作成者としてのコンテンツのタグ付けについて詳しくは、 [](/help/sites-cloud/authoring/features/tags.md) タグの使用を参照してください。
* タグの作成と管理、および適用されたコンテンツタグについては、管理者の観点から、「タグの管理」を参照してください。

## タグ付け API の概要 {#overview-of-the-tagging-api}

AEM の[タグフレームワーク](tagging-framework.md)の実装により、JCR API を使用してタグおよびタグコンテンツを管理できます。`TagManager` 文字列配列プロパティで値として入力したタグが重複しないようにするため、既存でないタグ `cq:tags` を指すタグは削除され、移動されたタグや結合されたタグ `TagID``TagID`は更新されます。 `TagManager` は、間違った変更を元に戻す JCR 監視リスナーを使用します。メインクラスは [com.day.cq.tagging](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/index.html?com/day/cq/tagging/package-summary.html) パッケージ内にあります。

* `JcrTagManagerFactory`  — のJCRベースの実装を返し `TagManager`ます。 タグ付け API のリファレンス実装です。
* `TagManager`  — パスと名前によるタグの解決と作成を可能にします。
* `Tag`  — タグオブジェクトを定義します。

### JCR ベースの TagManager の取得 {#getting-a-jcr-based-tagmanager}

To retrieve a `TagManager` instance, you need to have a JCR `Session` and to call `getTagManager(Session)`:

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

For the JCR-based implementation, which maps `Tags` onto JCR `Nodes`, you can directly use Sling&#39;s `adaptTo` mechanism if you have the resource (e.g. such as `/content/cq:tags/default/my/tag`):

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
>Directly adapting from `Node` to `Tag` is not possible, because `Node` does not implement the Sling `Adaptable.adaptTo(Class)` method.

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

タグガベージコレクターは、非表示で未使用のタグをクリーンアップするバックグラウンドサービスです。 非表示および未使用のタグは、下のタグ `/content/cq:tags` にプロパティがあり、コンテンツノードでは使用されません `cq:movedTo` 。 0の数があります。 この遅延削除プロセスを使用すると、移動または結合操作の一環としてコンテンツノード( `cq:tags` プロパティ)を更新する必要がありません。 ページプロパティダイアログなどで `cq:tags` プロパティが更新されると、 `cq:tags` プロパティ内の参照が自動的に更新されます。

タグガベージコレクターは、デフォルトで1日に1回実行されます。 これは、次の場所で設定できます。

`http://<host>:<port>/system/console/configMgr/com.day.cq.tagging.impl.TagGarbageCollector`

## タグ検索およびタグリスト {#tag-search-and-tag-listing}

タグおよびタグ一覧の検索は次のように動作します。

* The search for `TagID` searches for the tags that have the property `cq:movedTo` set to `TagID` and follows through the `cq:movedTo` `TagID`s.
* The search for tag title only searches the tags that do not have a `cq:movedTo` property.

## 他の言語のタグ {#tags-in-different-languages}

タグは異なる言語で定義 `title` できます。 次に、言語に依存するプロパティがタグノードに追加されます。 このプロパティは、例えばフランス語 `jcr:title.<locale>`の翻訳の場合 `jcr:title.fr` などの形式を持ちます。 `<locale>` は、小文字のISOロケール文字列である必要があります。次に例を示すように、ハイフン/ダッシュ(`_`)の代わりにアンダースコア(`-`)を使用します。 `de_ch`.

For example when the **Animals** tag is added to the **Products** page, the value `stockphotography:animals` is added to the property `cq:tags` of the node `/content/wknd/en/products/jcr:content`. 翻訳は、タグノードから参照されます。

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

次の手順では、 **タグ編集** ダイアログに新しい言語（フィンランド語など）を追加する方法を説明します。

1. CRXDE **で**、ノードの複数値プロパティ `languages` を編集し `/content/cq:tags`ます。
1. フィンランド語追加のロケールを表す。変更を保存します。 `fi_fi`

ページプロパティのタグダイアログと、タグ **付け** コンソールでタグを編集する際のタグの **編集** ダイアログで、フィンランド語が使用できるようになりました。

>[!NOTE]
>
>The new language needs to be one of the AEM recognized languages, i.e. it needs to be available as a node below `/libs/wcm/core/resources/languages`.
