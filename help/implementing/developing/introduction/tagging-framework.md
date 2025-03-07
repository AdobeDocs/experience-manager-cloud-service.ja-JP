---
title: AEM タグ付けフレームワーク
description: コンテンツにタグを付け、AEM タグ付けインフラストラクチャを使用して分類や整理を行います。
exl-id: 25418d44-aace-4e73-be1a-4b1902f40403
feature: Developing
role: Admin, Architect, Developer
source-git-commit: 10580c1b045c86d76ab2b871ca3c0b7de6683044
workflow-type: ht
source-wordcount: '1562'
ht-degree: 100%

---

# AEM タグ付けフレームワーク {#aem-tagging-framework}

タグ付けにより、コンテンツを分類および整理できますタグの分類には、名前空間と分類を使用できます。タグの使用について詳しくは、以下を参照してください。

* コンテンツ作成者としてのコンテンツのタグ付けについては、[タグの使用](/help/sites-cloud/authoring/sites-console/tags.md)を参照してください。
* タグの作成と管理や、タグが適用されているコンテンツについての管理者の観点については、タグの管理を参照してください。

この記事では、AEM でのタグ付けをサポートしている基盤フレームワークと、それをデベロッパーとして使用する方法を重点的に取り上げます。

## はじめに {#introduction}

コンテンツにタグ付けし、AEM タグ付けインフラストラクチャを使用するには：

* タグは、[`cq:Tag`](#cq-tag-node-type) タイプのノードとして、[分類のルートノード](#taxonomy-root-node)の下に存在する必要があります。
* タグ付けされたコンテンツノードの `NodeType` には、[`cq:Taggable`](#taggable-content-cq-taggable-mixin) mixin が含まれている必要があります。
* [`TagID`](#tagid) がコンテンツノードの [`cq:tags`](#cq-tags-property) プロパティに追加され、[`cq:Tag`](#cq-tag-node-type) タイプのノードに解決されます。

## cq:Tag ノードタイプ {#cq-tag-node-type}

タグの宣言は、リポジトリーにおける `cq:Tag.` タイプのノードにキャプチャされます。

* タグは、単純な単語（`sky` など）や、階層的な分類（一般的な果物とより具体的にリンゴの両方を意味する `fruit/apple` など）にすることができます。
* タグは一意の`TagID` によって識別されます。
* タグには、タイトル、ローカライズされたタイトル、説明など、任意のメタ情報があります。ユーザーインターフェイスには、`TagID` ではなくタイトル（存在する場合）が表示されます。

タグ付けフレームワークでは、作成者やサイト訪問者に、特定の事前定義されたタグだけを使用するよう制限を課します。

### タグの特徴 {#tag-characteristics}

* ノードタイプは `cq:Tag` です。
* ノード名は [`TagID`](#tagid) のコンポーネントです。
* [`TagID`](#tagid) には常に[名前空間](#tag-namespace)が含まれています。
* `jcr:title` プロパティ（UI に表示するタイトル）は省略可能です。
* `jcr:description` プロパティは省略可能です。
* 子ノードが含まれている場合、[コンテナタグ](#container-tags)と呼ばれます。
* タグは、[分類のルートノード](#taxonomy-root-node)と呼ばれるベースパスの下に保存されます。

### タグ ID {#tagid}

`TagID` は、リポジトリー内のタグノードに解決されるパスを識別します。

通常、`TagID` は名前空間で始まる短縮形の `TagID` ですが、[分類のルートノード](#taxonomy-root-node)から始まる絶対 `TagID` にすることもできます。

コンテンツにタグ付けするときに、コンテンツがまだ存在しない場合は、[`cq:tags`](#cq-tags-property) プロパティがコンテンツノードに追加され、`TagID` がこのプロパティの `String` 配列値に追加されます。

`TagID` は、[名前空間](#tag-namespace)とそれに続くローカル`TagID` で構成されます。[コンテナタグ](#container-tags)には、分類における階層順序を表すサブタグがあります。サブタグは、任意のローカル `TagID` と同じタグを参照するのに使用できます。例えば、`fruit` というタグが `fruit/apple` や `fruit/banana` などのサブタグを含むコンテナタグであっても、コンテンツにこのタグを付けることができます。

### 分類のルートノード {#taxonomy-root-node}

分類のルートノードは、リポジトリ内にあるすべてのタグの基本パスです。分類のルートノードは、`cq:Tag` タイプのノードにすることが&#x200B;*できません*。

AEM の基本パスは `/content/cq:tags` であり、ルートノードのタイプは `cq:Folder` です。

### タグの名前空間 {#tag-namespace}

名前空間を使用するとグループ化を行うことができます。サイトごと（例：公開または社内）や大規模なアプリケーションごと（例：Sites または Assets）に名前空間を設けることが最も典型的なユースケースですが、名前空間はその他の様々なニーズにも使用できます。名前空間は、現在のコンテンツに適用されるタグのサブセット（つまり特定の名前空間のタグ）のみを表示するのにユーザーインターフェイスで使用されます。

タグの名前空間は、分類サブツリーの最初のレベルです。これは、[分類のルートノード](#taxonomy-root-node)の直下のノードです。名前空間は `cq:Tag` タイプのノードで、その親は `cq:Tag` ノードタイプではありません。

すべてのタグには名前空間があります。名前空間を指定しない場合、タグはデフォルトの名前空間（`TagID` `default`、つまり `/content/cq:tags/default`）に割り当てられます。この場合、タイトルはデフォルトで `Standard Tags` に設定されます。

### コンテナタグ {#container-tags}

コンテナタグは、任意の数およびタイプの子ノードを含む、`cq:Tag` タイプのノードです。これにより、カスタムメタデータを使用してタグモデルを強化できます。

さらに、分類のコンテナタグ（またはスーパータグ）は、すべてのサブタグを包含するものとして機能します。例えば、`fruit/apple` とタグ付けされているコンテンツは、`fruit` ともタグ付けされていると見なされます。つまり、`fruit` とタグ付けされたコンテンツを検索すると、`fruit/apple` とタグ付けされたコンテンツも検出されます。

### タグ ID の解決 {#resolving-tagids}

タグ ID にコロン（`:`）が含まれている場合、そのコロンによってタグやサブ分類から名前空間が区別された後、タグやサブ分類は通常のスラッシュ（`/`）で区別されます。タグ ID にコロンが含まれていない場合は、デフォルトの名前空間が暗示されます。

タグの標準の場所は `/content/cq:tags` の下のみです。

存在しないパスまたは `cq:Tag` ノードを指していないパスを参照するタグは、無効と見なされて無視されます。

`TagID` の例とその要素、その`TagID` がリポジトリー内の絶対パスにどのように解決されるかを次の表に示します。

| `TagID` | 名前空間 | ローカル ID | コンテナタグ | リーフタグ | リポジトリー内の絶対パス |
|---|---|---|---|---|---|
| `dam:fruit/apple/braeburn` | `dam` | `fruit/apple/braeburn` | `fruit`、`apple` | `braeburn` | `content/cq:tags/dam/fruit/apple/braeburn` |
| `color/red` | `default` | `color/red` | `color` | `red` | `/content/cq:tags/default/color/red` |
| `sky` | `default` | `sky` | （なし） | `sky` | `/content/cq:tags/default/sky` |
| `dam:` | `dam` | （なし） | （なし） | （なし） | `/content/cq:tags/dam` |
| `content/cq:tags/category/car` | `category` | `car` | `car` | `car` | `content/cq:tags/category/car` |

### タグタイトルのローカリゼーション {#localization-of-tag-title}

タグにオプションのタイトル文字列 `jcr:title` が含まれている場合は、`jcr:title.<locale>` プロパティを追加することで、表示用のタイトルをローカライズできます。

詳しくは、以下を参照してください。

* [他の言語でのタグ](tagging-applications.md#tags-in-different-languages) - API の使用についてデベロッパーの観点で説明しています。
* 他の言語でのタグの管理 - タグ付けコンソールの使用について管理者の観点で説明しています。

### アクセス制御 {#access-control}

タグは、リポジトリ内で[分類のルートノード](#taxonomy-root-node)の下にノードとして存在します。作成者やサイト訪問者に対し、特定の名前空間内でのタグの作成を許可または禁止するには、リポジトリに適切な ACL を設定してください。

また、特定のタグまたは名前空間に対する読み取り権限を拒否することで、特定のコンテンツへのタグの適用を制御できます。

一般的な方法には次のものがあります。

* すべての名前空間への書き込みアクセス（`/content/cq:tags` 下への add／modify）を`tag-administrators` グループ／役割に許可する。このグループは、追加設定なしで使用できる AEM に付属しています。
* 読み取り可能にする必要があるすべての名前空間への読み取りアクセスをユーザー／作成者に許可する。
* ユーザー／作成者がタグを自由に定義できる名前空間への書き込みアクセス（`/content/cq:tags/some_namespace` 下への `add_node`）をユーザー／作成者に許可する。

## タグ付け可能なコンテンツ：cq:Taggable Mixin {#taggable-content-cq-taggable-mixin}

アプリケーションデベロッパーがコンテンツタイプにタグ付けを付加するには、ノードの登録（[CND](https://jackrabbit.apache.org/jcr/node-type-notation.html)）に `cq:Taggable` Mixin または `cq:OwnerTaggable` Mixin を含める必要があります。

`cq:OwnerTaggable` Mixin は `cq:Taggable` から継承されており、その目的は、所有者または作成者がコンテンツを分類できることを示すことです。AEM では、`cq:PageContent` ノードの属性にすぎません。`cq:OwnerTaggable` Mixin は、タグ付けフレームワークには必要ありません。

>[!NOTE]
>
>集約されたコンテンツアイテムの最上位ノード（またはその `jcr:content` ノード）では、タグの有効化だけを行うことをお勧めします。以下に例を示します。
>
>* `jcr:content` ノードのタイプが `cq:PageContent` であるページ（`cq:Page`）。`cq:Taggable` Mixin が含まれています。
>* `jcr:content/metadata` ノードに常に `cq:Taggable` Mixin があるアセット（`cq:Asset`）。

### ノードタイプの表記（CND） {#node-type-notation-cnd}

ノードタイプの定義は、リポジトリー内に CND ファイルとして存在します。CND 表記は、[JCR ドキュメント](https://jackrabbit.apache.org/jcr/node-type-notation.html)の一部として定義されています。

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

## cq:tags プロパティ {#cq-tags-property}

`cq:tags` プロパティは、作成者またはサイト訪問者によってコンテンツに 1 つ以上の`TagID` が割り当てられたときにその ID を格納するための `String` 配列です。このプロパティは、[`cq:Taggable`](#taggable-content-cq-taggable-mixin) Mixin で定義されているノードに追加した場合にのみ意味があります。

>[!NOTE]
>
>AEM のタグ付け機能を使用するには、カスタムで開発されたアプリケーションで `cq:tags` 以外のタグプロパティを定義しないでください。

## タグの移動と統合 {#moving-and-merging-tags}

次に、タグ付けコンソールを使用してタグの移動または結合を実行した場合のリポジトリーでの影響について説明します。

タグ A を `/content/cq:tags` 下のタグ B に移動または結合した場合：

* タグ A は削除されず、`cq:movedTo` プロパティを取得します。
   * `cq:movedTo` はタグ B を指します。
   * このプロパティは、タグ A がタグ B に移動または結合されたことを意味します。
   * タグ B を移動すると、それに応じてこのプロパティが更新されます。
   * したがって、タグ A は非表示になり、タグ A を指すコンテンツノード内のタグ ID を解決するためだけにリポジトリに保持されます。
   * タグ A のようなタグは、それを指すコンテンツノードがなくなったら、タグのガベージコレクターによって削除されます。
   * `cq:movedTo` プロパティの特別な値に `nirvana` があります。この値は、タグが削除されたにもかかわらず、保持する必要のある `cq:movedTo` が含まれるサブタブが存在することが原因でそのタグをリポジトリーから削除できない場合に適用されます。

     >[!NOTE]
     >
     >`cq:movedTo` プロパティは、次のいずれかの条件を満たす場合にのみ、移動または結合されたタグに追加されます。
     >
     > 1. タグがコンテンツで使用されている（つまり、参照が含まれている）。または
     > 1. タグが、既に移動された子を持っている。
     >
* タグ B が作成され（移動の場合）、`cq:backlinks` プロパティを取得します。
   * `cq:backlinks` は、参照を別の方向に保持します。つまり、タグ B に移動または結合されたすべてのタグのリストが保持されます。
   * この機能は、タグ B が移動／結合／削除されたとき、またはタグ B がアクティブになったときに、`cq:movedTo` プロパティを最新の状態に保つために通常必要になります。この場合は、すべてのバックリンクタグもアクティブにする必要があります。

     >[!NOTE]
     >
     >`cq:backlinks` プロパティは、次のいずれかの条件を満たす場合にのみ、移動または統合されたタグに追加されます。
     >
     > 1. タグがコンテンツで使用されている（つまり、参照が含まれている）。
     > 1. タグが、既に移動された子を持っている。

コンテンツノードの `cq:tags` プロパティを読み取る場合は、次のように解決されます。

1. `/content/cq:tags` 下で一致するものが見つからない場合、タグは返されません。
1. タグに `cq:movedTo` プロパティが設定されている場合は、参照先のタグ ID が使用されます。
   * これは、その次のタグに `cq:movedTo` プロパティがある限り繰り返されます。
1. 次のタグに `cq:movedTo` プロパティがない場合は、そのタグが読み取られます。

タグを移動または結合したときに変更を発行するには、`cq:Tag` ノードとそのすべてのバックリンクを複製する必要があります。この複製は、タグ管理コンソールでタグがアクティブにされたときに自動的におこなわれます。

後でページの `cq:tags` プロパティに対して更新が行われると、以前の参照が自動的にクリーンアップされます。移動したタグを API で解決すると移動先のタグが戻され、移動先のタグ ID が提供されることから、このクリーンアップ処理がトリガーされます。
