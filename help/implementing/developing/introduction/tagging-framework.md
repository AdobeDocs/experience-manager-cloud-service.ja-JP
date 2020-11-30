---
title: AEM タグ付けフレームワーク
description: コンテンツへのタグ付けと AEM タグ付けインフラストラクチャの利用 分類して整理するために。
translation-type: tm+mt
source-git-commit: 4bf023068aa69fb6b69c6f2443703ea2bbbf7d42
workflow-type: tm+mt
source-wordcount: '1567'
ht-degree: 20%

---


# The AEM Tagging Framework {#aem-tagging-framework}

タグ付けにより、コンテンツを分類および整理できますタグの分類には、名前空間と分類を使用できます。タグの使用に関する詳細は、次のとおりです。

* コンテンツ作成者としてのコンテンツのタグ付けについて詳しくは、 [](/help/sites-cloud/authoring/features/tags.md) タグの使用を参照してください。
* タグの作成と管理、および適用されたコンテンツタグについては、管理者の観点から、「タグの管理」を参照してください。

この記事では、AEMでタグ付けをサポートする基本的なフレームワークと、それを開発者として活用する方法に焦点を当てます。

## 概要 {#introduction}

コンテンツにタグ付けし、AEM タグ付けインフラストラクチャを利用するには：

* The tag must exist as a node of type [`cq:Tag`](#cq-tag-node-type) under the [taxonomy root node.](#taxonomy-root-node)
* The tagged content node&#39;s `NodeType` must include the [`cq:Taggable`](#taggable-content-cq-taggable-mixin) mixin.
* The [`TagID`](#tagid) is added to the content node&#39;s [`cq:tags`](#cq-tags-property) property and resolves to a node of type [`cq:Tag`.](#cq-tag-node-type)

## cq:Tag Node Type {#cq-tag-node-type}

The declaration of a tag is captured in the repository in a node of type `cq:Tag.`

* A tag can be a simple word (e.g. `sky`) or represent a hierarchical taxonomy (e.g. `fruit/apple`, meaning both the generic fruit and the more specific apple).
* Tags are identified by a unique `TagID`.
* タグには、タイトル、ローカライズされたタイトル、説明など、任意のメタ情報があります。The title should be displayed in user interfaces instead of the `TagID`, when present.

タグ付けフレームワークでは、作成者やサイト訪問者に、特定の事前定義されたタグだけを使用するよう制限を設けることもできます。

### タグの特徴 {#tag-characteristics}

* ノードタイプはで `cq:Tag`す。
* The node name is a component of the [`TagID`.](#tagid)
* The [`TagID`](#tagid) always includes a [namespace.](#tag-namespace)
* プ `jcr:title` ロパティ（UIに表示するタイトル）はオプションです。
* The `jcr:description` property is optional.
* When containing child nodes, is referred to as a [container tag.](#container-tags)
* The tag is stored in the repository below a base path called the [taxonomy root node.](#taxonomy-root-node)

### タグ ID {#tagid}

A `TagID` identifies a path which resolves to a tag node in the repository.

Typically, the `TagID` is a shorthand `TagID` starting with the namespace or it can be an absolute `TagID` starting from the [taxonomy root node.](#taxonomy-root-node)

When content is tagged, if it does not yet exist, the [`cq:tags`](#cq-tags-property) property is added to the content node and the `TagID` is added to the property&#39;s `String` array value.

The `TagID` consists of a [namespace](#tag-namespace) followed by the local `TagID`. [コンテナタグ](#container-tags) には、分類内の階層順序を表すサブタグが含まれます。 Sub-tags can be used to reference tags same as any local `TagID`. For example tagging content with `fruit` is allowed, even if it is a container tag with sub-tags, such as `fruit/apple` and `fruit/banana`.

### 分類のルートノード {#taxonomy-root-node}

分類のルートノードは、リポジトリ内にあるすべてのタグの基本パスです。The taxonomy root node must *not* be a node of type `cq:Tag`.

In AEM, the base path is `/content/cq:tags` and the root node is of type `cq:Folder`.

### タグの名前空間 {#tag-namespace}

名前空間を使用するとグループ化をおこなうことができます。最も一般的な使用例は、サイトごとに名前空間（公共用、社内用など）または大規模なアプリケーションごとに名前空間を置くことですが（サイトやアセットなど）、他の様々なニーズに対してはアプリケーションを使用できます。 名前空間は、ユーザーインターフェイスで使用され、現在のコンテンツに適用されるタグのサブセット(特定の名前空間のタグなど)のみを表示します。

タグの名前空間は、分類サブツリーの最初のレベルです。これは、[分類のルートノードの直下のノードです。](#taxonomy-root-node) 名前空間とは、親がノードタイプで `cq:Tag` はないタイプの `cq:Tag` ノードです。

すべてのタグには名前空間があります。名前空間を指定しない場合、タグはデフォルトの名前空間( `TagID` つまり、 `default``/content/cq:tags/default`.  この場合、タイトルはデフォルト `Standard Tags`でに設定されます。

### コンテナタグ {#container-tags}

コンテナタグは、任意の数およびタイプの子ノードを含む、`cq:Tag` タイプのノードです。これにより、カスタムメタデータを使用してタグモデルを強化できます。

Furthermore, container tags (or super-tags) in a taxonomy serve as the sub-summation of all sub-tags: for example content tagged with `fruit/apple` is considered to be tagged with `fruit` as well, i.e. searching for content just tagged with `fruit` would also find the content tagged with `fruit/apple`.

### タグ ID の解決 {#resolving-tagids}

If the tag ID contains a colon (`:`), the colon separates the namespace from the tag or sub-taxonomy, which are then separated with normal slashes (`/`). タグ ID にコロンが含まれていない場合は、デフォルトの名前空間が暗示されます。

The standard and only location of tags is below `/content/cq:tags`.

Tags referencing non-existing paths or paths that do not point to a `cq:Tag` node are considered invalid and are ignored.

The following table shows some sample `TagID`s, their elements, and how the `TagID` resolves to an absolute path in the repository:

| `TagID` | 名前空間 | ローカルID | コンテナタグ | リーフタグ | Repository Absolute Tag Path |
|---|---|---|---|---|---|
| `dam:fruit/apple/braeburn` | `dam` | `fruit/apple/braeburn` | `fruit`,`apple` | `braeburn` | `content/cq:tags/dam/fruit/apple/braeburn` |
| `color/red` | `default` | `color/red` | `color` | `red` | `/content/cq:tags/default/color/red` |
| `sky` | `default` | `sky` | (なし) | `sky` | `/content/cq:tags/default/sky` |
| `dam:` | `dam` | (なし) | (なし) | (なし) | `/content/cq:tags/dam` |
| `content/cq:tags/category/car` | `category` | `car` | `car` | `car` | `content/cq:tags/category/car` |

### タグタイトルのローカリゼーション {#localization-of-tag-title}

When the tag includes the optional title string `jcr:title`, it is possible to localize the title for display by adding the property `jcr:title.<locale>`.

詳しくは、以下を参照してください。

* [様々な言語のタグ](tagging-applications.md#tags-in-different-languages) （APIの開発者としての使用を説明）
* 様々な言語でのタグの管理（管理者としてのタグ付けコンソールの使用を説明）

### アクセス制御 {#access-control}

タグは、リポジトリ内で[分類のルートノードの下にノードとして存在します。](#taxonomy-root-node) 特定の名前空間で作成者やサイト訪問者がタグを作成することを許可または拒否するには、リポジトリで適切なACLを設定します。

特定のタグや名前空間に対する読み取り権限を拒否すると、特定のコンテンツにタグを適用する機能が制御されます。

一般的な方法には以下のものがあります。

* Allowing the `tag-administrators` group/role write access to all namespaces (add/modify under `/content/cq:tags`). このグループは、追加設定なしで使用できる AEM に付属しています。
* 読み取り可能なすべての名前空間（ほとんどすべて）へのアクセスをユーザー/作成者に許可します。
* タグを自由に定義できる名前空間(以下、「`add_node``/content/cq:tags/some_namespace`」)への書き込みアクセスをユーザー/作成者に許可する

## タグ付け可能なコンテンツ：cq:Taggable Mixin {#taggable-content-cq-taggable-mixin}

In order for application developers to attach tagging to a content type, the node&#39;s registration ([CND](https://jackrabbit.apache.org/node-type-notation.html)) must include the `cq:Taggable` mixin or the `cq:OwnerTaggable` mixin.

`cq:OwnerTaggable` mixin は `cq:Taggable` から継承されており、その目的は、所有者または作成者がコンテンツを分類できることを示すことです。In AEM, it is only an attribute of the `cq:PageContent` node. The `cq:OwnerTaggable` mixin is not required by the tagging framework.

>[!NOTE]
>
>It is recommended to only enable tags on the top-level node of an aggregated content item (or on its `jcr:content` node). 次のような例があります。
>
>* ノードのタイプが`cq:Page`Mixinを含むページ( `jcr:content`) `cq:PageContent``cq:Taggable` 。
>* ノードに常にミックスインが含まれるアセット(`cq:Asset``jcr:content/metadata``cq:Taggable` )。


### Node Type Notation (CND) {#node-type-notation-cnd}

ノードタイプの定義は、リポジトリ内に CND ファイルとして存在します。The CND notation is defined as part of the [JCR documentation.](https://jackrabbit.apache.org/node-type-notation.html).

AEM に含まれるノードタイプの基本的な定義は、次のようになります。

```xml
[cq:Tag] > mix:title, nt:base
    orderable
    - * (undefined) multiple
    - * (undefined)
    + * (nt:base) = cq:Tag version

[cq:Taggable]
    mixin
    - cq:tags (string) multiple

[cq:OwnerTaggable] > cq:Taggable
    mixin
```

## cq:tagsプロパティ {#cq-tags-property}

The `cq:tags` property is a `String` array used to store one or more `TagID`s when they are applied to content by authors or site visitors. The property only has meaning when added to a node which is defined with the [`cq:Taggable`](#taggable-content-cq-taggable-mixin) mixin.

>[!NOTE]
>
>To leverage AEM tagging functionality, custom developed applications should not define tag properties other than `cq:tags`.

## タグの移動と統合 {#moving-and-merging-tags}

以下に、タグ管理コンソールを使用してタグを移動または結合する際のリポジトリ内での効果を説明します。

When tag A is moved or merged into tag B under `/content/cq:tags`:

* Tag A is not deleted and receives a `cq:movedTo` property.
   * `cq:movedTo` は、タグBを指します。
   * このプロパティは、タグAがタグBに移動または結合されたことを意味します。
   * タグBを移動すると、それに応じてこのプロパティが更新されます。
   * タグAは非表示になるので、リポジトリに保持されるのは、タグAを指すコンテンツノード内のタグIDを解決するためだけです。
   * タグガベージコレクターは、タグAのようなタグを、コンテンツノードがそれらを参照しない状態で削除します。
   * A special value for the `cq:movedTo` property is `nirvana`, which is applied when the tag is deleted but cannot be removed from the repository because there are subtags with a `cq:movedTo` that must be kept.

      >[!NOTE]
      >
      >次のいずれかの条件を満たす場合にのみ、 `cq:movedTo` プロパティは移動されたタグまたは結合されたタグに追加されます。
      >
      > 1. タグはコンテンツで使用されます（参照が含まれていることを意味します）。 または
      > 1. タグには、既に移動された子が含まれています。


* タグBが作成され（移動の場合）、 `cq:backlinks` プロパティを受け取ります。
   * `cq:backlinks` は、参照を他の方向に保持します。つまり、タグBに移動または結合されたすべてのタグのリストを保持します。
   * これは、タグBが移動/結合/削除されたときやタグBがアクティブになったときに、 `cq:movedTo` プロパティを最新の状態に保つために最も重要です。この場合、すべてのバックリンクタグもアクティブにする必要があります。

      >[!NOTE]
      >
      >次のいずれかの条件を満たす場合にのみ、 `cq:backlinks` プロパティは移動されたタグまたは結合されたタグに追加されます。
      >
      > 1. タグはコンテンツで使用されます（参照が含まれていることを意味します）。 または
      > 1. タグには、既に移動された子が含まれています。


Reading a `cq:tags` property of a content node involves the following resolution:

1. の下に一致がない場合、タグは返され `/content/cq:tags`ません。
1. タグにプロパティが設定されている場合は、参照先のタグIDが使用されます。 `cq:movedTo`
   * これは、その次のタグに `cq:movedTo` プロパティがある限り繰り返されます。
1. 次のタグに `cq:movedTo` プロパティがない場合は、そのタグが読み取られます。

タグを移動または結合したときに変更を発行するには、ノードとそのすべての `cq:Tag` バックリンクを複製する必要があります。 これは、タグ管理コンソールでタグがアクティブ化されたときに自動的に行われます。

Later updates to the page&#39;s `cq:tags` property automatically clean up the old references. 移動したタグを API で解決すると移動先のタグが戻され、移動先のタグ ID が提供されることから、この処理がトリガーされます。
