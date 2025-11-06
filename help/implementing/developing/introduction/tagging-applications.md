---
title: AEM アプリケーションへのタグ付けの構築
description: カスタム AEM アプリケーション内のタグまたは拡張タグをプログラムで操作します
exl-id: a106dce1-5d51-406a-a563-4dea83987343
feature: Developing
role: Admin, Developer
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '717'
ht-degree: 100%

---

# AEM アプリケーションへのタグ付けの構築 {#building-tagging-into-aem-applications}

カスタム AEM アプリケーション内のタグまたは拡張タグをプログラムで操作するために、このドキュメントでは、次の使用方法を説明します。

* [タグ付け API](https://www.adobe.io/experience-manager/reference-materials/cloud-service/javadoc/com/day/cq/tagging/package-summary.html)

これは、次とやり取りします。

* [タグ付けフレームワーク](tagging-framework.md)

タグ付けに関する関連情報については、次を参照してください。

* コンテンツ作成者としてのタグ付けについて詳しくは、「[タグの使用](/help/sites-cloud/authoring/sites-console/tags.md)」を参照してください。
* タグの作成と管理や、タグが適用されているコンテンツについての管理者の観点については、タグの管理を参照してください。

## タグ付け API の概要 {#overview-of-the-tagging-api}

AEM の[タグ付けフレームワーク](tagging-framework.md)の実装により、JCR API を使用してタグおよびタグコンテンツを管理できます。`TagManager` は、`cq:tags` 文字列配列プロパティに値として入力されたタグが重複しないように、存在しないタグを指している `TagID` を削除し、移動または結合されたタグの `TagID` を更新します。`TagManager` は、間違った変更を元に戻す JCR 監視リスナーを使用します。メインクラスは [com.day.cq.tagging](https://www.adobe.io/experience-manager/reference-materials/cloud-service/javadoc/com/day/cq/tagging/package-summary.html) パッケージ内にあります。

* `JcrTagManagerFactory``TagManager` の JCR ベースの実装を返します。タグ付け API のリファレンス実装です。
* `TagManager` - パスと名前を使用して、タグを解決して作成できます。
* `Tag` - タグオブジェクトを定義します。

### JCR ベースの TagManager の取得 {#getting-a-jcr-based-tagmanager}

`TagManager` インスタンスを取得するには、JCR `Session` を取得して `getTagManager(Session)` を呼び出す必要があります。

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

`Tags` を JCR `Nodes` にマップする JCR ベースの実装の場合、リソースがあれば（例：`/content/cq:tags/default/my/tag`）、Sling の `adaptTo` メカニズムを直接使用できます。

```java
Tag tag = resource.adaptTo(Tag.class);
```

タグは、（ノードではなく）リソース&#x200B;*からのみ*&#x200B;変換できますが、ノードとリソースの両方&#x200B;*に*&#x200B;変換できます。

```java
Node node = tag.adaptTo(Node.class);
Resource node = tag.adaptTo(Resource.class);
```

>[!NOTE]
>
>`Node` は Sling の `Adaptable.adaptTo(Class)` メソッドを実装しないので、`Node` を `Tag` に直接適合させることはできません。

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
>次の有効な `RangeIterator` を使用できます。
>
>`com.day.cq.commons.RangeIterator`

### タグの削除 {#deleting-tags}

```java
tagManager.deleteTag(tag);
```

### タグの複製 {#replicating-tags}

タグのタイプは `Replicator` なので、タグでレプリケーションサービス（`nt:hierarchyNode`）を使用できます。

```java
replicator.replicate(session, replicationActionType, tagPath);
```

## タグのガベージコレクター {#the-tag-garbage-collector}

タグのガベージコレクターは、非表示および未使用のタグをクリーンアップするバックグラウンドサービスです。非表示および未使用のタグは、`/content/cq:tags` の下のタグで、`cq:movedTo` プロパティを持ち、コンテンツノードでは使用されません。これらのタグのカウントはゼロです。この遅延削除プロセスを使用すると、移動や結合操作の一環としてコンテンツノード（`cq:tags` プロパティ）をアップデートする必要がありません。`cq:tags` プロパティの参照は、`cq:tags` プロパティがアップデートされると自動的にアップデートされます（例：ページプロパティダイアログを介して）。

タグのガベージコレクターは、デフォルトで 1 日に 1 回実行されます。これは、次の場所で設定できます。

`http://<host>:<port>/system/console/configMgr/com.day.cq.tagging.impl.TagGarbageCollector`

## タグ検索およびタグ一覧 {#tag-search-and-tag-listing}

タグ検索およびタグ一覧は次のように動作します。

* `TagID` の検索は、`cq:movedTo` プロパティが `TagID` に設定されているタグを検索します（`cq:movedTo` `TagID` をすべて検索します）。
* タグタイトルの検索は、`cq:movedTo` プロパティのないタグのみを検索します。

## 他の言語のタグ {#tags-in-different-languages}

タグ `title` は異なる言語で定義できます。言語に依存するプロパティがタグノードに追加されます。このプロパティは `jcr:title.<locale>` の形式を持ちます（例：フランス語訳は `jcr:title.fr`）`<locale>` は、小文字の ISO ロケール文字列で、ハイフン／ダッシュ（`-`）ではなくアンダースコア（`_`）を使用します（例：`de_ch`）。

例：**Animals** タグが **Products** ページに追加されると、値 `stockphotography:animals` は `/content/wknd/en/products/jcr:content` ノードの `cq:tags` プロパティに追加されます。翻訳は、タグノードから参照されます。

サーバーサイド API には、ローカライズされた `title` 関連のメソッドがあります。

* [`com.day.cq.tagging.Tag`](https://www.adobe.io/experience-manager/reference-materials/cloud-service/javadoc/com/day/cq/tagging/Tag.html)
   * `getLocalizedTitle(Locale locale)`
   * `getLocalizedTitlePaths()`
   * `getLocalizedTitles()`
   * `getTitle(Locale locale)`
   * `getTitlePath(Locale locale)`
* [`com.day.cq.tagging.TagManager`](https://www.adobe.io/experience-manager/reference-materials/cloud-service/javadoc/com/day/cq/tagging/TagManager.html)
   * `canCreateTagByTitle(String tagTitlePath, Locale locale)`
   * `createTagByTitle(String tagTitlePath, Locale locale)`
   * `resolveByTitle(String tagTitlePath, Locale locale)`

AEM では、言語はページ言語またはユーザー言語のどちらかから取得できます。

タグ付けの場合、ローカライズはコンテキストに依存します。タグの `titles` はページ言語、ユーザー言語またはそれ以外の任意の言語で表示することができます。

### タグを編集ダイアログへの新しい言語の追加 {#adding-a-new-language-to-the-edit-tag-dialog}

次の手順では、新しい言語（例：フィンランド語）を&#x200B;**タグを編集**&#x200B;ダイアログに追加する方法を説明します。

1. **CRXDE** で、ノード `/content/cq:tags` の複数値プロパティ `languages` を編集します。
1. フィンランド語のロケールを表す `fi_fi` を追加して、変更を保存します。

**タグ付け**&#x200B;コンソールでタグを編集する際に、ページプロパティのタグダイアログと&#x200B;**タグを編集**&#x200B;ダイアログで、フィンランド語を使用できるようになりました。

>[!NOTE]
>
>新しい言語は、AEM で認識される言語のいずれかである必要があります。つまり、`/libs/wcm/core/resources/languages` の下のノードとして使用できる必要があります。
