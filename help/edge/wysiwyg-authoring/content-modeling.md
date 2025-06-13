---
title: Edge Delivery Services プロジェクトを使用した WYSIWYG オーサリング用のコンテンツモデリング
description: Edge Delivery Services プロジェクトを使用した WYSIWYG オーサリングにおけるコンテンツモデリングの仕組みと独自のコンテンツをモデル化する方法について説明します。
exl-id: e68b09c5-4778-4932-8c40-84693db892fd
feature: Edge Delivery Services
role: Admin, Architect, Developer
index: false
hide: true
hidefromtoc: true
source-git-commit: fecbebde808c545a84889da5610a79c088f2f459
workflow-type: tm+mt
source-wordcount: '2160'
ht-degree: 100%

---


# Edge Delivery Services プロジェクトを使用した WYSIWYG オーサリング用のコンテンツモデリング {#content-modeling}

Edge Delivery Services プロジェクトを使用した WYSIWYG オーサリングにおけるコンテンツモデリングの仕組みと独自のコンテンツをモデル化する方法について説明します。

## 前提条件 {#prerequisites}

Edge Delivery Services で WYSIWYG オーサリングを行うプロジェクトは、コンテンツソースまたは[オーサリングメソッド](/help/edge/wysiwyg-authoring/authoring.md)とは独立して、他の Edge Delivery Services プロジェクトの大半の仕組みを継承します。

プロジェクトのコンテンツをモデル化する前に、まず、次のドキュメントをお読みください。

* [はじめに - 開発者向けチュートリアル](/help/edge/developer/tutorial.md)
* [マークアップ、セクション、ブロック、自動ブロック](/help/edge/developer/markup-sections-blocks.md)
* [ブロックコレクション](/help/edge/developer/block-collection.md)

コンテンツのソースに依存しない方法で機能するような、説得力のあるコンテンツモデルを考え出すには、これらの概念を理解することが不可欠です。このドキュメントでは、WYSIWYG オーサリング用に特化して実装されている仕組みについて詳細を説明します。

## デフォルトコンテンツ {#default-content}

**デフォルトコンテンツ**&#x200B;は、作成者が追加のセマンティックを追加することなく、直感的にページ上に配置されるコンテンツです。これには、テキスト、見出し、リンク、画像が含まれます。そのようなコンテンツは、その機能や目的が一目瞭然です。

AEM では、このコンテンツは非常にシンプルで、事前定義済みのモデルを使用したコンポーネントとして実装され、Markdown や HTML でシリアル化できるすべての機能が含まれます。

* **テキスト**：リッチテキスト（リスト要素と、強調文字または斜体文字を含む）
* **タイトル**：テキスト、タイプ（h1 - h6）
* **画像**：ソース、説明
* **ボタン**：テキスト、タイトル、URL、タイプ（デフォルト、プライマリ、セカンダリ）

これらのコンポーネントのモデルは、[Edge Delivery Services を使用した WYSIWYG オーサリング用のボイラープレート](https://github.com/adobe-rnd/aem-boilerplate-xwalk/blob/main/component-models.json#L2-L112)の一部です。

## ブロック {#blocks}

ブロックは、特定のスタイルや機能を使用して豊富なコンテンツを作成するために使用します。デフォルトコンテンツとは異なり、ブロックには追加のセマンティックが必要です。

ブロックは基本的に、JavaScript で装飾され、スタイルシートでスタイル設定されたコンテンツの要素です。

### ブロックモデルの定義 {#model-definition}

Edge Delivery Servicesで WYSIWYG オーサリングを使用する場合、作成者がコンテンツ作成に使用するインターフェイスを提供できるように、ブロックのコンテンツを明示的にモデル化する必要があります。基本的には、モデルを作成して、オーサリング UI がブロックに基づいて作成者に提示するオプションを理解できるようにする必要があります。

[`component-models.json`](https://github.com/adobe-rnd/aem-boilerplate-xwalk/blob/main/component-models.json) ファイルは、ブロックのモデルを定義します。コンポーネントモデルで定義されたフィールドは、AEM 内でプロパティとして保持され、ブロックを構成するテーブル内のセルとしてレンダリングされます。

```json
{
  "id": "hero",
  "fields": [
    {
      "component": "reference",
      "valueType": "string",
      "name": "image",
      "label": "Image",
      "multi": false
    },
    {
      "component": "text-input",
      "valueType": "string",
      "name": "imageAlt",
      "label": "Alt",
      "value": ""
    },
    {
      "component": "text-area",
      "name": "text",
      "value": "",
      "label": "Text",
      "valueType": "string"
    }
  ]
}
```

すべてのブロックにモデルが必要となるわけではありません。一部のブロックは、子のリスト用の単純な[コンテナ](#container)であり、それぞれの子には独自のモデルがあります。

また、ユニバーサルエディターを使用して、どのブロックが存在し、どのブロックをページに追加できるのか定義する必要もあります。[`component-definitions.json`](/help/implementing/universal-editor/component-definition.md) ファイルには、ユニバーサルエディターで使用できるようになったコンポーネントの一覧が表示されます。

```json
{
  "title": "Hero",
  "id": "hero",
  "plugins": {
    "xwalk": {
      "page": {
        "resourceType": "core/franklin/components/block/v1/block",
        "template": {
          "name": "Hero",
          "model": "hero"
        }
      }
    }
  }
}
```

多くのブロックに対して 1 つのモデルを使用できます。例えば、一部のブロックは、テキストと画像を定義するモデルを共有します。

ブロックごとに、開発者は以下を実行します。

* `core/franklin/components/block/v1/block` リソースタイプを使用する必要があります。これは、AEM のブロックロジックの汎用実装です。
* ブロック名を定義する必要があります。ブロック名は、ブロックのテーブルヘッダーにレンダリングされます。
   * ブロック名は、ブロックを修飾する適切なスタイルとスクリプトを取得するために使用します。
* [モデル ID](/help/implementing/universal-editor/field-types.md#model-structure) を定義できます。
   * モデル ID は、コンポーネントのモデルへの参照です。作成者がプロパティパネルで使用できるフィールドを定義します。
* [フィルター ID](/help/implementing/universal-editor/filtering.md) を定義できます。
   * フィルター ID はコンポーネントのフィルターへの参照です。これにより、ブロックやセクションに追加できる子を制限したり、有効にする RTE 機能を制限したりするなど、オーサリング動作を変更できます。

ブロックがページに追加されると、この情報はすべて AEM に保存されます。リソースタイプまたはブロック名のいずれかが見つからない場合、そのブロックはページ上にレンダリングされません。

>[!WARNING]
>
>カスタム AEM コンポーネントを実装することは、可能ですが、必須ではなく、推奨もされません。AEM により提供される Edge Delivery Services 用コンポーネントは十分であり、開発を容易にするために一定のガードレールを提供しています。
>
>AEM が提供するコンポーネントは、Edge Delivery Services に公開時に [helix-html2md](https://github.com/adobe/helix-html2md) によって、ユニバーサルエディターでページ読み込み時に [aem.js](https://github.com/adobe/aem-boilerplate/blob/main/scripts/aem.js) によって使用できるマークアップをレンダリングします。マークアップは、AEM とシステムの他の部分との間の安定した契約であり、カスタマイズはできません。このため、プロジェクトではコンポーネントを変更したり、カスタムコンポーネントを使用したりしないでください。

### ブロック構造 {#block-structure}

ブロックのプロパティは、[コンポーネントモデルで定義され](#model-definition)、AEM ではそのまま保持されます。プロパティは、ブロックのテーブルに似た構造内のセルとしてレンダリングされます。

#### シンプルなブロック {#simple}

最もシンプルな形式では、ブロックは各プロパティを 1 行または 1 列に、モデル内でプロパティが定義されている順序でレンダリングします。

次の例では、モデル内で最初に画像を定義し、その次にテキストを定義しています。したがって、最初に画像、2 番目にテキストでレンダリングされます。

>[!BEGINTABS]

>[!TAB データ]

```json
{
  "name": "Hero",
  "model": "hero",
  "image": "/content/dam/image.png",
  "imageAlt": "Helix - a shape like a corkscrew",
  "text": "<h1>Welcome to AEM</h1>"
}
```

>[!TAB マークアップ]

```html
<div class="hero">
  <div>
    <div>
      <picture>
        <img src="/content/dam/image.png" alt="Helix - a shape like a corkscrew">
      </picture>
    </div>
  </div>
  <div>
    <div>
      <h1>Welcome to AEM</h1>
    </div>
  </div>
</div>
```

>[!TAB テーブル]

```text
+---------------------------------------------+
| Hero                                        |
+=============================================+
| ![Helix - a shape like a corkscrew][image0] |
+---------------------------------------------+
| # Welcome to AEM                            |
+---------------------------------------------+
```

>[!ENDTABS]

値のタイプによっては、マークアップ内のセマンティックを推定でき、プロパティが単一のセルに結合されます。この動作については、[型推論](#type-inference)の節で説明します。

#### キーと値のブロック {#key-value}

多くの場合、レンダリングされたセマンティックマークアップの修飾、CSS クラス名の追加、新しいノードの追加、DOM 内での移動、スタイルの適用をお勧めします。

ただし、その他の場合は、ブロックはキー値ペアのような設定として読み取られます。

この例として、[セクションのメタデータ](/help/edge/developer/markup-sections-blocks.md#sections)があります。このユースケースでは、ブロックをキー値ペアテーブルとしてレンダリングするように設定できます。詳しくは、[セクションとセクションのメタデータ](#sections-metadata)の節を参照してください。

>[!BEGINTABS]

>[!TAB データ]

```json
{
  "name": "Featured Articles",
  "model": "spreadsheet-input",
  "key-value": true,
  "source": "/content/site/articles.json",
  "keywords": ['Developer','Courses'],
  "limit": 4
}
```

>[!TAB マークアップ]

```html
<div class="featured-articles">
  <div>
    <div>source</div>
    <div><a href="/content/site/articles.json">/content/site/articles.json</a></div>
  </div>
  <div>
    <div>keywords</div>
    <div>Developer,Courses</div>
  <div>
  <div>
    <div>limit</div>
    <div>4</div>
  </div>
</div>
```

>[!TAB テーブル]

```text
+-----------------------------------------------------------------------+
| Featured Articles                                                     |
+=======================================================================+
| source   | [/content/site/articles.json](/content/site/articles.json) |
+-----------------------------------------------------------------------+
| keywords | Developer,Courses                                          |
+-----------------------------------------------------------------------+
| limit    | 4                                                          |
+-----------------------------------------------------------------------+
```

>[!ENDTABS]

#### コンテナブロック {#container}

前述の構造は両方とも、プロパティのリストという 1 つの次元を持ちます。コンテナブロックを使用すると、子（通常は、同じタイプまたはモデル）を追加できるので、2 次元になります。これらのブロックは、最初に 1 つの列を持つ行としてレンダリングされる独自のプロパティを引き続きサポートします。また、子も追加できます。この場合、各項目は行としてレンダリングされ、各プロパティはその行内の列としてレンダリングされます。

次の例では、ブロックは、リンクされたアイコンのリストを子として受け入れます。それぞれのリンクされたアイコンには、画像とリンクが含まれています。フィルター設定を参照するために、ブロックのデータに[フィルター ID](/help/implementing/universal-editor/filtering.md) が設定される点に注意してください。

>[!BEGINTABS]

>[!TAB データ]

```json
{
  "name": "Our Partners",
  "model": "text-only",
  "filter": "our-partners",
  "text": "<p>Our community of partners is ...</p>",
  "item_0": {
    "model": "linked-icon",
    "image": "/content/dam/partners/foo.png",
    "imageAlt": "Icon of Foo",
    "link": "https://foo.com/"
  },
  "item_1": {
    "model": "linked-icon"
    "image": "/content/dam/partners/bar.png",
    "imageAlt": "Icon of Bar",
    "link": "https://bar.com"
  }
}
```

>[!TAB マークアップ]

```html
<div class="our-partners">
  <div>
    <div>
        Our community of partners is ...
    </div>
  </div>
  <div>
    <div>
      <picture>
         <img src="/content/dam/partners/foo.png" alt="Icon of Foo">
      </picture>
    </div>
    <div>
      <a href="https://foo.com">https://foo.com</a>
    </div>
  </div>
  <div>
    <div>
      <picture>
         <img src="/content/dam/partners/bar.png" alt="Icon of Bar">
      </picture>
    </div>
    <div>
      <a href="https://bar.com">https://bar.com</a>
    </div>
  </div>
</div>
```

>[!TAB テーブル]

```text
+------------------------------------------------------------ +
| Our Partners                                                |
+=============================================================+
| Our community of partners is ...                            |
+-------------------------------------------------------------+
| ![Icon of Foo][image0] | [https://foo.com](https://foo.com) |
+-------------------------------------------------------------+
| ![Icon of Bar][image1] | [https://bar.com](https://bar.com) |
+-------------------------------------------------------------+
```

>[!ENDTABS]

### ブロックのセマンティックコンテンツモデルの作成 {#creating-content-models}

[ブロック構造の仕組み](#block-structure)がわかれば、AEMで 1 対 1 で保持されるコンテンツを配信層にマッピングするコンテンツモデルを作成できます。

どのプロジェクトでも初期段階で、すべてのブロックについて、コンテンツモデルを慎重に検討する必要があります。作成者がブロックの実装やスタイルを再利用しながら、切り替えたり組み合わせたりできるようにするには、コンテンツソースやオーサリングエクスペリエンスに依存しないようにする必要があります。詳細と一般的なガイダンスについては、[David のモデル（テイク 2）](https://www.aem.live/docs/davidsmodel)を参照してください。具体的には、[ブロックコレクション](/help/edge/developer/block-collection.md)は、一般的なユーザーインターフェイスのパターンにおける特定の使用例に対応する、広範なコンテンツモデルのセットを含んでいます。

Edge Delivery Services を使用した WYSIWYG オーサリングでは、リッチテキストのようにコンテキスト内でセマンティックマークアップを編集するのではなく、複数のフィールドで構成されるフォームを使用して情報がオーサリングされる場合に、魅力的なセマンティックコンテンツモデルをどのように提供するかという問題が生じます。

この問題を解決するには、魅力的なコンテンツモデルを容易に作成できる 3 つの方法があります。

* [型推論](#type-inference)
* [フィールドの折りたたみ](#field-collapse)
* [要素のグループ化](#element-grouping)

>[!NOTE]
>
>ブロック実装は、コンテンツを分解し、ブロックをクライアント側でレンダリングされた DOM に置き換えることができます。これは、開発者にとっては可能であり、直感的ですが、Edge Delivery Services にはベストプラクティスではありません。

#### 型推論 {#type-inference}

一部の値については、値自体からセマンティックの意味を推測できます。次のような値が含まれます。

* **画像** - AEM のリソースへの参照が `image/` で始まる MIME タイプのアセットである場合、その参照は `<picture><img src="${reference}"></picture>` としてレンダリングされます。
* **リンク** - AEM 内に存在している参照が画像ではない場合、または値が `https?://` または `#` で始まる場合、参照は `<a href="${reference}">${reference}</a>` としてレンダリングされます。
* **リッチテキスト** - トリミングされた値が段落（`p`、`ul`、`ol`、`h1` - `h6` など）で始まる場合、値はリッチテキストとしてレンダリングされます。
* **クラス名** - `classes` プロパティは[ブロックオプション](/help/edge/developer/markup-sections-blocks.md#block-options)として扱われ、[単純なブロック](#simple)ではテーブルヘッダーに（[コンテナブロック](#container)内にある項目の値リストとして）レンダリングされます。[ブロックを別のスタイルに設定](/help/edge/wysiwyg-authoring/create-block.md#block-options)する際、完全に新しいブロックを作成する必要はない場合に役立ちます。
* **値リスト** - 値が複数値プロパティで、最初の値が以前の値でない場合、すべての値がコンマ区切りリストとして連結されます。

それ以外の部分はすべてプレーンテキストとしてレンダリングされます。

#### フィールドの折りたたみ {#field-collapse}

フィールドの折りたたみは、サフィックスの `Title`、`Type`、`MimeType`、`Alt`、`Text`（すべて大文字と小文字を区別）を使用する命名規則に基づいて、複数のフィールド値を 1 つのセマンティック要素に組み合わせるメカニズムです。これらのサフィックスで終わるプロパティは、値と見なされず、別のプロパティの属性と見なされます。

##### 画像 {#image-collapse}

>[!BEGINTABS]

>[!TAB データ]

```json
{
  "image": "/content/dam/red-car.png",
  "imageAlt: "A red card on a road"
}
```

>[!TAB マークアップ]

```html
<picture>
  <img src="/content/dam/red-car.png" alt="A red car on a road">
</picture>
```

>[!TAB テーブル]

```text
![A red car on a road][image0]
```

>[!ENDTABS]

##### リンクとボタン {#links-buttons-collapse}

>[!BEGINTABS]

>[!TAB データ]

```json
{
  "link": "https://www.adobe.com",
  "linkTitle": "Navigate to adobe.com",
  "linkText": "adobe.com",
  "linkType": "primary"
}
```

>[!TAB マークアップ]

`linkType` なし、または `linkType=default`

```html
<a href="https://www.adobe.com" title="Navigate to adobe.com">adobe.com</a>
```

`linkType=primary`

```html
<strong>
  <a href="https://www.adobe.com" title="Navigate to adobe.com">adobe.com</a>
</strong>
```

`linkType=secondary`

```html
<em>
  <a href="https://www.adobe.com" title="Navigate to adobe.com">adobe.com</a>
</em>
```

>[!TAB テーブル]

```text
[adobe.com](https://www.adobe.com "Navigate to adobe.com")
**[adobe.com](https://www.adobe.com "Navigate to adobe.com")**
_[adobe.com](https://www.adobe.com "Navigate to adobe.com")_
```

>[!ENDTABS]

##### 見出し {#headings-collapse}

>[!BEGINTABS]

>[!TAB データ]

```json
{
  "heading": "Getting started",
  "headingType": "h2"
}
```

>[!TAB マークアップ]

```html
<h2>Getting started</h2>
```

>[!TAB テーブル]

```text
## Getting started
```

>[!ENDTABS]

#### 要素のグループ化 {#element-grouping}

[フィールドの折りたたみ](#field-collapse)は、複数のプロパティを単一のセマンティック要素に組み合わせることですが、要素のグループ化とは、複数のセマンティック要素を 1 つのセルに連結することです。これは、作成者が作成できる要素のタイプと数を制限する必要がある使用例で特に役立ちます。

例えば、ティーザーコンポーネントを使用すると、作成者は、サブタイトル、タイトル、最大 2 つのコールトゥアクションボタンと組み合わせた 1 つの段落の説明のみを作成できます。これらの要素をグループ化すると、セマンティックマークアップが生成され、追加の操作を行わずにスタイルを設定できます。

要素のグループ化では、グループ名がグループ内の各プロパティからアンダースコアで区切られる命名規則が使用されます。グループ内のプロパティのフィールドの折りたたみは、前述のように機能します。

>[!BEGINTABS]

>[!TAB データ]

```json
{
  "name": "teaser",
  "model": "teaser",
  "image": "/content/dam/teaser-background.png",
  "imageAlt": "A group of people sitting on a stage",
  "teaserText_subtitle": "Adobe Experience Cloud"
  "teaserText_title": "Meet the Experts"
  "teaserText_titleType": "h2"
  "teaserText_description": "<p>Join us in this ask me everything session...</p>"
  "teaserText_cta1": "https://link.to/more-details",
  "teaserText_cta1Text": "More Details"
  "teaserText_cta2": "https://link.to/sign-up",
  "teaserText_cta2Text": "RSVP",
  "teaserText_cta2Type": "primary"
}
```

>[!TAB マークアップ]

```html
<div class="teaser">
  <div>
    <div>
      <picture>
        <img src="/content/dam/teaser-background.png" alt="A group of people sitting on a stage">
      </picture>
    </div>
  </div>
  <div>
    <div>
      <p>Adobe Experience Cloud</p>
      <h2>Meet the Experts</h2>
      <p>Join us in this ask me everything session ...</p>
      <p><a href="https://link.to/more-details">More Details</a></p>
      <p><strong><a href="https://link.to/sign-up">RSVP</a></strong></p>
    </div>
  </div>
</div>
```

>[!TAB テーブル]

```text
+-------------------------------------------------+
| Teaser                                          |
+=================================================+
| ![A group of people sitting on a stage][image0] |
+-------------------------------------------------+
| Adobe Experience Cloud                          |
| ## Meet the Experts                             |
| Join us in this ask me everything session ...   |
| [More Details](https://link.to/more-details)    |
| [RSVP](https://link.to/sign-up)                 |
+-------------------------------------------------+
```

>[!ENDTABS]

## セクションとセクションのメタデータ {#sections-metadata}

開発者は複数の[ブロック](#blocks)を定義およびモデル化するのと同じ方法で、異なるセクションを定義できます。

Edge 配信サービスのコンテンツモデルでは、セクションに含まれるデフォルトのコンテンツまたはブロックである1 レベルのネストのみを意図的に許可します。つまり、他のコンポーネントを含む、より複雑なビジュアルコンポーネントを持つには、セクションとしてモデル化し、自動ブロッククライアント側を使用して組み合わせる必要があります。これの一般的な例としては、タブや、アコーディオンのような折りたたみ可能なセクションがあります。

セクションは、ブロックと同じ方法で定義できますが、リソースタイプは `core/franklin/components/section/v1/section` となります。セクションには、名前と[フィルター ID](/help/implementing/universal-editor/filtering.md)（[ユニバーサルエディター](/help/implementing/universal-editor/introduction.md)のみでのみ使用）、および[モデル ID](/help/implementing/universal-editor/field-types.md#model-structure)（セクションのメタデータをレンダリングするのに使用される）を指定できます。モデルはこのようにして、セクションメタデータブロックのモデルとなります。空でない場合、このモデルは自動的にキーと値のブロックとしてセクションに追加されます。

デフォルトのセクションの[モデル ID](/help/implementing/universal-editor/field-types.md#model-structure) および[フィルター ID](/help/implementing/universal-editor/filtering.md) は `section` です。これを使用して、デフォルトのセクションの動作を変更できます。次の使用例は、いくつかのスタイルと背景画像をセクションメタデータモデルに追加します。

```json
{
  "id": "section",
  "fields": [
    {
      "component": "multiselect",
      "name": "style",
      "value": "",
      "label": "Style",
      "valueType": "string",
      "options": [
        {
          "name": "Fade in Background",
          "value": "fade-in"
        },
        {
          "name": "Highlight",
          "value": "highlight"
        }
      ]
    },
    {
      "component": "reference",
      "valueType": "string",
      "name": "background",
      "label": "Image",
      "multi": false
    }
  ]
}
```

次の例では、タブセクションを定義します。これを使用すると、自動ブロック中にタブタイトルデータ属性を持つ連続セクションをタブブロックに結合して、タブブロックを作成できます。

```json
{
  "title": "Tab",
  "id": "tab",
  "plugins": {
    "xwalk": {
      "page": {
        "resourceType": "core/franklin/components/section/v1/section",
        "template": {
          "name": "Tab",
          "model": "tab",
          "filter": "section"
        }
      }
    }
  }
}
```

## ページメタデータ {#page-metadata}

ドキュメントには、ページの `<head>` でどの `<meta>` 要素がレンダリングされるかを定義するのに使用されるページ[メタデータブロック](https://www.aem.live/developer/block-collection/metadata)を含めることができます。AEM as a Cloud Service のページのプロパティは、`title`、`description`、`keywords` などの Edge 配信サービスですぐに使用できるプロパティにマッピングされます。

独自のメタデータの定義方法を詳しく学ぶ前に、次のドキュメントを参照して、最初にページメタデータの概念を理解してください。

* [メタデータ](https://www.aem.live/developer/block-collection/metadata)
* [一括メタデータ](/help/edge/docs/bulk-metadata.md)

追加のページメタデータを 2 つの方法で定義することもできます。

### メタデータスプレッドシート {#metadata-spreadsheets}

AEM as a Cloud Service では、パスごとまたはパスパターンごとにテーブルのような方法でメタデータを定義できます。Excel や Google スプレッドシートに似た、表のようなデータ用のオーサリング UI が利用可能です。

詳しくは、[スプレッドシートを使用した表形式データの管理](/help/edge/wysiwyg-authoring/tabular-data.md)ドキュメントを参照してください。

### ページプロパティ {#page-properties}

AEM で使用できるデフォルトのページプロパティの多くは、ドキュメント内の各ページのメタデータにマッピングされます。これには、`title`、`description`、`robots`、`canonical url` または `keywords` などが含まれます。次の AEM 固有のプロパティもいくつか使用できます。

* ISO8601 形式の `modified-time` としての `cq:lastModified`
* ISO8601 形式の `published-time` としてドキュメントが最後に公開された時刻
* `cq-tags` としての `cq:tags`、タグ ID のコンマ区切りリスト。

また、カスタムページメタデータのコンポーネントモデルを定義することもできます。このモデルは、ユニバーサルエディターで作成者が使用できます。

これを行うには、ID `page-metadata` を持つコンポーネントモデルを作成します。

```json
{
  "id": "page-metadata",
  "fields": [
    {
      "component": "text",
      "name": "theme",
      "label": "Theme"
    }
  ]
}
```

## 次の手順 {#next-steps}

これで、コンテンツをモデル化する方法を理解できたので、WYSIWYG オーサリングプロジェクトを使用して独自の Edge Delivery Services のブロックを作成できます。

Edge Delivery Services プロジェクトを使用した WYSIWYG オーサリングで、ユニバーサルエディターで使用するために実装されたブロックを作成する方法について詳しくは、[ユニバーサルエディターで使用するために実装されたブロックの作成](/help/edge/wysiwyg-authoring/create-block.md)ドキュメントを参照してください。

ブロックの作成に慣れている場合は、[Edge Delivery Services を使用した WYSIWYG オーサリングの開発者向け入門ガイド](/help/edge/wysiwyg-authoring/edge-dev-getting-started.md)ドキュメントを参照して、Edge Delivery Services とコンテンツオーサリング用のユニバーサルエディターを使用し、新しい Adobe Experience Manager サイトを立ち上げて実行します。
