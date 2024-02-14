---
title: コンテンツプロジェクトを使用したAEMオーサリング用のコンテンツモデリングEdge Delivery Services
description: コンテンツモデリングがEdge Delivery Servicesプロジェクトを使用したAEMオーサリングでどのように機能するか、および独自のコンテンツをモデル化する方法について説明します。
source-git-commit: e9c882926baee001170bad2265a1085e03cdbedf
workflow-type: tm+mt
source-wordcount: '2097'
ht-degree: 1%

---


# コンテンツプロジェクトを使用したAEMオーサリング用のコンテンツモデリングEdge Delivery Services {#content-modeling}

コンテンツモデリングがEdge Delivery Servicesプロジェクトを使用したAEMオーサリングでどのように機能するか、および独自のコンテンツをモデル化する方法について説明します。

{{aem-authoring-edge-early-access}}

## 前提条件 {#prerequisites}

Edge Delivery ServicesでAEMオーサリングを使用するプロジェクトは、コンテンツソースや [オーサリングメソッド。](/help/edge/authoring.md)

プロジェクトのコンテンツのモデリングを開始する前に、まず次のドキュメントをお読みください。

* [はじめに - 開発者向けチュートリアル](/help/edge/developer/tutorial.md)
* [マークアップ、セクション、ブロック、自動ブロック](/help/edge/developer/markup-sections-blocks.md)
* [ブロックコレクション](/help/edge/developer/block-collection.md)

コンテンツのソースに依存しない方法で機能する、説得力のあるコンテンツモデルを考え出すには、これらの概念を理解することが不可欠です。 このドキュメントでは、AEMオーサリング用に特に実装されているメカニックの詳細を説明します。

## デフォルトコンテンツ {#default-content}

**デフォルトコンテンツ** は、作成者が追加のセマンティクスを追加することなく、直感的にページ上に配置されるコンテンツです。 これには、テキスト、見出し、リンク、画像が含まれます。 そのような内容は、その機能や目的に関しては説明が必要です。

AEMでは、このコンテンツは非常にシンプルで事前定義済みのモデルを使用してコンポーネントとして実装され、Markdown やHTMLでシリアル化できるすべての機能が含まれます。

* **テキスト**：リッチテキスト（リスト要素と、強いテキストまたは斜体テキストを含む）
* **タイトル**：テキスト、タイプ (h1 ～ h6)
* **画像**：ソース、説明
* **ボタン**：テキスト、タイトル、URL、タイプ（デフォルト、プライマリ、セカンダリ）

これらのコンポーネントのモデルは、 [オーサリング用のボイラープレート (Edge Delivery Servicesを使用 )。](https://github.com/adobe-rnd/aem-boilerplate-xwalk/blob/main/component-models.json#L2-L112)

## ブロック {#blocks}

ブロックは、特定のスタイルや機能を使用して豊富なコンテンツを作成するために使用します。 デフォルトコンテンツとは異なり、ブロックには追加のセマンティクスが必要です。 ブロックは、 [コンポーネントをAEMページエディターに表示します。](/help/implementing/developing/components/overview.md)

ブロックは基本的に、JavaScript で装飾され、スタイルシートでスタイル設定されたコンテンツの断片です。

### ブロックモデル定義 {#model-definition}

Edge Delivery ServicesでAEMオーサリングを使用する場合、作成者がコンテンツを作成するためのインターフェイスを提供できるように、ブロックのコンテンツを明示的にモデル化する必要があります。 基本的には、モデルを作成して、オーサリング UI がブロックに基づいて作成者に提示するオプションを把握できるようにする必要があります。

The [`component-models.json`](https://github.com/adobe-rnd/aem-boilerplate-xwalk/blob/main/component-models.json) ファイルは、ブロックのモデルを定義します。 コンポーネントモデルで定義されたフィールドは、AEM内でプロパティとして保持され、ブロックを構成するテーブル内のセルとしてレンダリングされます。

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

すべてのブロックにモデルが必要となるわけではありません。 一部のブロックは、 [コンテナ](#container) 子のリストの場合。各子に独自のモデルがあります。

また、ユニバーサルエディターを使用して、存在しページに追加できるブロックを定義する必要もあります。 The [`component-definitions.json`](https://github.com/adobe-rnd/aem-boilerplate-xwalk/blob/main/component-definition.json) ファイルには、ユニバーサルエディタで使用可能になったコンポーネントの一覧が表示されます。

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

多くのブロックに対して 1 つのモデルを使用できます。 例えば、一部のブロックは、テキストと画像を定義するモデルを共有します。

ブロックごとに、開発者は以下をおこないます。

* を使用する必要があります `core/franklin/components/block/v1/block` リソースタイプ。AEMのブロックロジックの汎用実装です。
* ブロック名を定義する必要があります。ブロック名は、ブロックのテーブルヘッダーにレンダリングされます。
   * ブロック名は、ブロックを修飾する適切なスタイルとスクリプトを取得するために使用されます。
* 次を定義できます： [モデル ID。](/help/implementing/universal-editor/field-types.md#model-structure)
   * モデル ID は、コンポーネントのモデルへの参照で、作成者がプロパティレールで使用できるフィールドを定義します。
* 次を定義できます： [フィルター ID。](/help/implementing/universal-editor/customizing.md#filtering-components)
   * フィルター ID はコンポーネントのフィルターへの参照です。このフィルターを使用すると、例えば、ブロックやセクションに追加できる子や、有効にする RTE 機能を制限するなどして、オーサリング動作を変更できます。

ブロックがページに追加されると、これらの情報はすべてAEMに保存されます。 リソースタイプまたはブロック名が見つからない場合、そのブロックはページ上でレンダリングされません。

>[!WARNING]
>
>可能な限り、カスタムAEMコンポーネントを実装する必要もお勧めもありません。 AEMが提供するEdge Delivery Servicesのコンポーネントで十分で、開発を容易にするために特定のガードレールを提供します。
>
>AEMが提供するコンポーネントは、 [helix-html2md](https://github.com/adobe/helix-html2md) Edge Delivery Servicesおよびで公開する場合 [aem.js](https://github.com/adobe/aem-boilerplate/blob/main/scripts/aem.js) （ユニバーサルエディターでページを読み込む場合） マークアップはAEMとシステムの他の部分との間の安定した契約であり、カスタマイズはできません。 このため、プロジェクトではコンポーネントを変更しないでください。また、カスタムコンポーネントを使用しないでください。

### ブロック構造 {#block-structure}

ブロックのプロパティは次のとおりです。 [コンポーネントモデルで定義される](#model-definition) AEMではそのまま保持されました。 プロパティは、ブロックのテーブルに似た構造内のセルとしてレンダリングされます。

#### 単純なブロック {#simple}

最も簡単な形式では、ブロックは各プロパティを 1 行または 1 列に、モデル内でプロパティが定義されている順序でレンダリングします。

次の例では、モデル内の最初のイメージと、2 番目のテキストを定義します。 したがって、最初の画像と 2 番目のテキストでレンダリングされます。

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

>[!TAB Markup]

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

一部のタイプの値はマークアップ内のセマンティクスを推定でき、プロパティは単一のセルに結合されます。 この動作については、の節で説明します。 [Inference と入力します。](#type-inference)

#### キーと値のブロック {#key-value}

多くの場合、レンダリングされたセマンティックマークアップの修飾、CSS クラス名の追加、新しいノードの追加、DOM 内での移動、スタイルの適用をお勧めします。

ただし、その他の場合は、ブロックはキー値ペアのような設定として読み取られます。

例えば、 [セクションのメタデータ。](/help/edge/developer/markup-sections-blocks.md#sections) この使用例では、ブロックをキー値ペアテーブルとしてレンダリングするように設定できます。 の節を参照してください。 [セクションとセクションのメタデータ](#sections-metadata) を参照してください。

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

>[!TAB Markup]

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

前の構造は両方とも、単一のディメンション、つまりプロパティのリストを持ちます。 コンテナブロックを使用すると、（通常は同じタイプまたはモデルの）子を追加できます。したがって、2 次元になります。 これらのブロックは、1 つの列を先に持つ行としてレンダリングされる独自のプロパティを引き続きサポートします。 また、子も追加できます。この場合、各項目は行としてレンダリングされ、各プロパティはその行内の列としてレンダリングされます。

次の例では、ブロックは、リンクされたアイコンのリストを子として受け入れます。各リンクされたアイコンには、画像とリンクが含まれています。 次の点に注意してください。 [フィルター ID](/help/implementing/universal-editor/customizing.md#filtering-components) フィルター設定を参照するために、ブロックのデータに設定されます。

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

>[!TAB Markup]

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

を使用 [ブロック構造の仕組みを説明した。](#block-structure) AEMで 1 対 1 で保持されるコンテンツを配信層にマッピングするコンテンツモデルを作成できます。

どのプロジェクトでも、すべてのブロックについて、コンテンツモデルを慎重に検討する必要があります。 作成者がブロックの実装やスタイルを再利用しながら切り替えたり組み合わせたりできるようにするには、コンテンツソースやオーサリングエクスペリエンスに依存しない必要があります。 詳細と一般的なガイダンスについては、 [David&#39;s Model (take 2).](https://www.aem.live/docs/davidsmodel) 具体的には、 [ブロックコレクション](/help/edge/developer/block-collection.md) には、一般的なユーザーインターフェイスパターンの特定の使用例に対応する、広範なコンテンツモデルのセットが含まれています。

Edge Delivery Servicesを使用したAEMオーサリングの場合、コンテキスト内のリッチテキストなどのセマンティックマークアップを編集する代わりに、複数のフィールドで構成されるフォームで情報を作成する場合、魅力的なセマンティックコンテンツモデルを提供する方法に関する質問が発生します。

この問題を解決するには、魅力的なコンテンツモデルを容易に作成できる 3 つの方法があります。

* [Type Inference](#type-inference)
* [フィールドの折りたたみ](#field-collapse)
* [要素のグループ化](#element-grouping)

>[!NOTE]
>
>ブロック実装は、コンテンツを分解し、ブロックをクライアント側でレンダリングされた DOM に置き換えることができます。 これは可能で直感的ですが、Edge Delivery Servicesにとってはベストプラクティスではありません。

#### Type Inference {#type-inference}

一部の値については、値自体から意味的意味を推測できます。 次のような値が含まれます。

* **画像** - AEM内のリソースへの参照が、 `image/`の場合、参照は `<picture><img src="${reference}"></picture>`.
* **リンク** - AEMに参照が存在し、画像でない場合、または値が `https?://`  または `#`の場合、参照は `<a href="${reference}">${reference}</a>` .
* **リッチテキスト**  — トリミングされた値が段落 (`p`, `ul`, `ol`, `h1`-`h6`など ) の場合、値はリッチテキストとしてレンダリングされます。
* **クラス名** - `classes` プロパティはブロックオプションとして扱われ、 [単純なブロック、](#simple) または [コンテナブロックを使用します。](#container)
* **値リスト**  — 値が複数値プロパティで、最初の値が以前の値でない場合、すべての値がコンマ区切りリストとして連結されます。

それ以外の部分はすべてプレーンテキストとしてレンダリングされます。

#### フィールドの折りたたみ {#field-collapse}

フィールドの折りたたみは、サフィックスを使用する命名規則に基づいて、複数のフィールド値を 1 つのセマンティック要素に組み合わせるメカニズムです `Title`, `Type`, `Alt`、および `Text` （すべて大文字と小文字を区別）。 これらのサフィックスで終わるプロパティは、値と見なされず、別のプロパティの属性と見なされます。

##### 画像 {#image-collapse}

>[!BEGINTABS]

>[!TAB データ]

```json
{
  "image": "/content/dam/red-car.png",
  "imageAlt: "A red card on a road"
}
```

>[!TAB Markup]

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

>[!TAB Markup]

いいえ `linkType`または `linkType=default`

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

>[!TAB Markup]

```html
<h2>Getting started</h2>
```

>[!TAB テーブル]

```text
## Getting started
```

>[!ENDTABS]

#### 要素のグループ化 {#element-grouping}

While [フィールド折りたたみ](#field-collapse) は、複数のプロパティを単一のセマンティック要素に組み合わせることです。要素のグループ化とは、複数のセマンティック要素を 1 つのセルに連結することです。 これは、作成者が作成できる要素のタイプと数を制限する必要がある使用例で特に役立ちます。

例えば、ティーザーコンポーネントを使用すると、作成者は、サブタイトル、タイトルおよび 1 つの段落の説明のみを作成でき、最大 2 つのコールトゥアクションボタンを組み合わせることができます。 これらの要素をグループ化すると、セマンティックマークアップが生成され、追加の操作をおこなわずにスタイルを設定できます。

要素のグループ化では、命名規則を使用します。グループ名は、グループ内の各プロパティとアンダースコアで区切られます。 グループ内のプロパティのフィールド折りたたみは、前述のように機能します。

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

>[!TAB Markup]

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
| ## Welcome to AEM                               |
| Join us in this ask me everything session ...   |
| [More Details](https://link.to/more-details)    |
| [RSVP](https://link.to/sign-up)                 |
+-------------------------------------------------+
```

>[!ENDTABS]

## セクションとセクションのメタデータ {#sections-metadata}

開発者が複数のを定義およびモデル化するのと同じ方法 [ブロック、](#blocks) 異なるセクションを定義できます。

Edge Delivery Servicesのコンテンツモデルでは、セクションに含まれるデフォルトのコンテンツまたはブロックである、1 レベルのネストのみを意図的に許可します。 つまり、他のコンポーネントを含むより複雑なビジュアルコンポーネントを持つには、セクションとしてモデル化し、自動ブロッククライアント側を使用して組み合わせる必要があります。 一般的な例としては、タブやアコーディオンのような折りたたみ可能なセクションがあります。

セクションは、ブロックと同じ方法で定義できますが、リソースタイプは `core/franklin/components/section/v1/section`. セクションには、名前と [フィルタ ID,](/help/implementing/universal-editor/customizing.md#filtering-components) これは、 [ユニバーサルエディター](/help/implementing/universal-editor/introduction.md) ただ、同じく [モデル ID,](/help/implementing/universal-editor/field-types.md#model-structure) （セクションメタデータのレンダリングに使用） モデルはこのようにして、セクションメタデータブロックのモデルです。空でない場合、このモデルは自動的にキーと値のブロックとしてセクションに追加されます。

The [モデル ID](/help/implementing/universal-editor/field-types.md#model-structure) および [フィルター ID](/help/implementing/universal-editor/customizing.md#filtering-components) のデフォルトのセクションは、 `section`. これを使用して、デフォルトのセクションの動作を変更できます。 次の使用例は、いくつかのスタイルと背景画像を断面メタデータモデルに追加します。

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

次の例では、タブセクションを定義します。タブセクションは、連続するセクションとタブタイトルデータ属性を組み合わせて、自動ブロック中にタブブロックに組み込むことで、タブブロックを作成するのに使用できます。

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

ドキュメントにはページを含めることができます [メタデータブロック](/help/edge/authoring.md#metadata--seo) どれを定義するために使用されるか `<meta>` 要素は、 `<head>` 」という名前に変更されます。 AEM as a Cloud Serviceのページのプロパティは、Edge Delivery Servicesが標準で使用できるページにマッピングされます（例： ） `title`, `description`, `keywords`など

独自のメタデータの定義方法を詳しく学ぶ前に、次のドキュメントを参照して、最初にページメタデータの概念を理解してください。

* [メタデータ](https://www.aem.live/developer/block-collection/metadata)
* [一括メタデータ](/help/edge/docs/bulk-metadata.md)

追加のページメタデータを 2 つの方法で定義することもできます。

### メタデータスプレッドシート {#metadata-spreadsheets}

AEM as a Cloud Serviceでは、テーブルのような方法で、パスごとまたはパスパターンごとにメタデータを定義できます。 Excel やGoogleシートと同様に、テーブルに似たデータのオーサリング UI が用意されています。

このようなテーブルを作成するには、ページを作成し、サイトコンソールのメタデータテンプレートを使用します。

スプレッドシートのページプロパティで、必要なメタデータフィールドと URL を定義します。 次に、ページパスまたはページパスパターンごとにメタデータを追加します。

パスマッピングにスプレッドシートも必ず追加してから、パスマッピングを公開してください。

```json
{
  "mappings": [
    "/content/site/:/",
    "/content/site/metadata:/metadata.json"
  ]
}
```

### ページプロパティ {#page-properties}

また、ページメタデータのコンポーネントモデルを定義することもできます。このモデルは、AEM Sitesのページのプロパティダイアログの「 」タブとして作成者が使用できます。

これをおこなうには、ID を持つコンポーネントモデルを作成します `page-metadata`.

```json
{
  "id": "page-metadata",
  "fields": [
    {
      "component": "text-input",
      "name": "theme",
      "label": "Theme"
    }
  ]
}
```

特別な意味を持つフィールド名がいくつかあり、オーサリングダイアログ UI の提供時にスキップされます。

* **`cq:tags`**  — デフォルトでは、 `cq:tags` はメタデータに追加されません。 これらを `page-metadata` モデルは、タグ ID をコンマ区切りリストとして追加します。 `tags` メタタグを先頭に追加します。
* **`cq:lastModified`** - `cq:lastModified` はデータを `last-modified` 先頭に
