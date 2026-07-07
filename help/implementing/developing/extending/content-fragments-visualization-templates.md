---
title: コンテンツフラグメントのビジュアライゼーションテンプレートの作成
description: ビジュアライゼーションテンプレートを使用したコンテンツフラグメントのプレビューと公開 テンプレートの作成およびカスタマイズ方法について説明します。
feature: Developing, Content Fragments
role: Admin, Developer
source-git-commit: b0a32380b028ff230ec4904a86b55b8ba0f4558f
workflow-type: tm+mt
source-wordcount: '2134'
ht-degree: 4%

---

# ビジュアルコンテンツフラグメント – テンプレート {#visual-content-fragments-templates}

Adobe Experience Manager（AEM）as a Cloud Serviceでは、HTML テンプレートを使用してコンテンツフラグメントを視覚化し、HTML形式で配信できます。

HTML テンプレートを使用すると、コンテンツフラグメントの表示方法を制御できます。 任意のコードエディターでHTML テンプレートを作成し、AEMのコンテンツフラグメントモデルにアップロードして割り当てることができます。  Handlebars.jsを使用したコンテンツプレースホルダーを使用すると、テンプレートをコンテンツフラグメントモデルのデータタイプにマッピングできます。 モデルに割り当てられたテンプレートは、モデルに基づいて任意のコンテンツフラグメントと共に使用して、フラグメントを視覚化したり、HTML形式のモジュラーエクスペリエンスとしてweb、電子メール、モバイルアプリケーションなどの任意のチャネルに配信したりできます。

この記事では、ビジュアルコンテンツフラグメントをレンダリングするためのHandlebars構文を使用したカスタム HTML テンプレートの作成方法について説明します。

テンプレートを作成すると、次のことが可能になります。

* [AEMでのテンプレートの使用](#using-a-content-fragment-html-template-in-aem)

* ビジュアルコンテンツフラグメントの[公開URLを使用](#using-the-visual-content-fragment-publish-url)

>[!NOTE]
>
>AEMでのテンプレートのアップロード、割り当て、使用については、[ ビジュアルコンテンツフラグメント ](/help/sites-cloud/administering/content-fragments/visual-content-fragments.md)を参照してください。

>[!NOTE]
>
>[Figma to Visual Content Fragments Job](/help/ai-in-aem/agents/brand-experience/experience-production/figma-to-visual-content-fragments.md)を使用して、HTML デザインを自動的に読み込みます。

## 学習すること {#what-you-will-learn}

（非常に迅速な）概要を提供した後：

* AEMでのテンプレートの使用方法
* 公開URLの使用

このページでは、次の項目について説明します（詳細）。

* Handlebars – 構文の必要な基本
* コンテンツフラグメントデータへのアクセス方法
* ネストされたコンテンツフラグメントの操作
* 複数値フィールドの処理
* ループと条件付きロジックの作成
* コンテンツフラグメントのテンプレートデザインのベストプラクティス

## 前提条件 {#prerequisites}

ここで取り上げるテクノロジーについて理解し、使用するには、次の操作を行う必要があります。

* HTMLの基本
* AEM コンテンツフラグメントとコンテンツフラグメントモデルの概要
* コンテンツフラグメントモデルについて

## コンテンツフラグメント HTML テンプレートの使用 {#using-a-content-fragment-html-template}

### AEMでのコンテンツフラグメント HTML テンプレートの使用 {#using-a-content-fragment-html-template-in-aem}

AEMでのテンプレートの使用方法について詳しくは、次を参照してください。

* [ビジュアルコンテンツフラグメント – テンプレートのアップロードと割り当て](/help/sites-cloud/administering/content-fragments/visual-content-fragments.md)
* [選択したフラグメントのプレビューアクション – コンソールから](/help/sites-cloud/administering/content-fragments/managing.md#actions-selected-content-fragment)
* [フラグメントエディターからのフラグメントのプレビュー](/help/sites-cloud/administering/content-fragments/authoring.md#preview-content-fragment)

### ビジュアルコンテンツフラグメントの公開URLの使用 {#using-the-visual-content-fragment-publish-url}

テンプレートを使用してビジュアルコンテンツフラグメントを作成したら、ビジュアルコンテンツフラグメントの[公開URL](/help/implementing/developing/extending/content-fragments-visualization-publish-url.md)を使用できます。

## Handlebars - （非常に）基本 {#handlebars-the-very-basics}

Handlebarsは、動的コンテンツをHTMLに挿入するために、二重中括弧（括弧） `{{ }}`を使用するシンプルなテンプレート言語です。

### 基本的な構文 {#basic-syntax}

基本的なHandlebars構文の例：

```handlebars
<!-- Output a variable (HTML-escaped) -->
{{variableName}}

<!-- Output raw HTML (unescaped) -->
{{{htmlContent}}}

<!-- Comment (not rendered) -->
{{! This is a comment }}
```

### 主な概念 {#key-concepts}

Handlebarsの主な概念：

| 構文 | 説明 | 用途 |
|--- |--- |--- |
| `{{ }}` | HTMLの特殊文字をエスケープ | メタデータ、ラベル、ブール値 |
| `{{{ }}}` | 生のHTMLを出力（エスケープなし） | リッチテキストとアセット出力 |
| `{{! }}` | Handlebars-only コメント | テンプレートドキュメント |

>[!IMPORTANT]
>
> 値は事前にレンダリングされたHTMLであるため、フィールド値には3つの括弧（`{{{ }}}`）を使用します。

## テンプレートのコンテキスト参照 {#template-context-reference}

テンプレートがレンダリングされると、コンテンツフラグメントに関するすべてのデータを含むコンテキストオブジェクトが受け取られます。 主な内容：

* 選択したフラグメントは
* 選択したフラグメントから参照されているすべてのフラグメント

  >[!NOTE]
  >
  >フラグメントは次のように参照できます。
  >
  >* uiの場合：最大の深さ5
  >* apiを使用する場合：深度は設定可能で、最大深度は10です

### コンテンツフラグメント {#content-fragment}

（選択した）コンテンツフラグメントのコンテキストオブジェクトの構造：

| 変数 | 種類 | 説明 |
|--- |--- |--- |
| `properties` | Map | フラグメントメタデータ（[ プロパティ構造](#properties-structure-main-and-referenced-fragments)を参照） |
| `fields` | Map | フィールド値に名前で直接アクセス |
| `allFields` | リスト | 反復用`{name, value}`の配列 |
| `hasFields` | ブーリアン | フラグメントにフィールドがある場合は`true` |

### プロパティ構造 {#properties-structure}

`properties` オブジェクトは、選択したフラグメントと、参照されている各フラグメントに対して同じ構造を持ちます。

| Property | 種類 | 説明 | 例 |
|--- |--- |--- |--- |
| `id` | 文字列 | フラグメントのUID | |
| `title` | 文字列 | フラグメントのタイトル | サイクリング南ユタ |
| `description` | 文字列 | フラグメントの説明 | 冒険… |
| `path` | 文字列 | フラグメントへのJCR パス | `/content/dam/...` |
| `hasDescription` | ブーリアン | 説明が空白でない場合はTrue | `true` |
| `createdDate` | 文字列 | ISO-8601作成日 | |
| `modifiedDate` | 文字列 | ISO-8601変更日 | |
| `publishedDate` | 文字列 | ISO-8601公開日 | |
| `status` | 文字列 | パブリッシュ層のレプリケーションステータス | `DRAFT` |
| `model` | Map | 次を含む：`id`、`path`、`name`、`technicalName`、`description` | |
| `validationStatus` | リスト | `{property, message}`様のエントリ | |
| `previewReplicationStatus` | 文字列 | プレビュー層のレプリケーションステータス | |
| `tags` | リスト | フラグメントレベルのタグ： 各項目：`id`、`title`、`titlePath`、`name`、`path`、`description` | |
| `fieldTags` | リスト | フィールドレベルのタグ： `tags`と同じ構造です。 | |

例：テンプレートへのアクセス

（選択した）コンテンツフラグメントの場合：

```handlebars
{{properties.title}}, {{properties.description}}, {{{fields.field_name}}} 
```

### 参照コンテンツフラグメント {#referenced-content-fragments}

参照されているフラグメントのコンテキストオブジェクトの構造：

| 変数 | 種類 | 説明 |
|--- |--- |--- |
| `hasReferencedFragments` | ブーリアン | 参照が存在する場合は`true` |
| `referencedFragments` | リスト | 参照されるフラグメントオブジェクトの配列 |
| `referencesError` | ブーリアン | 参照の読み込み中にエラーが発生した場合`true` |
| `referencesErrorMessage` | 文字列 | `referencesError`が`true`の場合のエラーメッセージ |

### 参照フラグメント構造 {#referenced-fragment-structure}

`referencedFragments`の各項目には次が含まれます。

| Property | 種類 | 説明 |
|--- |--- |--- |
| `anchorId` | 文字列 | HTMLで保護されたアンカーID （フラグメントレベルで、コンテンツフラグメントプロパティではない） |
| `properties` | Map | フラグメントメタデータ（上記と同じ構造） |
| `hasFields` | ブーリアン | フラグメントにフィールドがある場合はTrue |
| `fields` | Map | このフラグメント内のフィールドへの直接アクセス |
| `allFields` | リスト | 反復用`{name, value}`の配列 |

例：最初に参照されたコンテンツフラグメントのテンプレートアクセス（0 インデックス付きリストの最初の項目）:

```handlebars
{{referencedFragments.[0].anchorId}}, {{referencedFragments.[0].properties.title}}, {{referencedFragments.[0].properties.description}}
```

フィールドマップから：

```handlebars
{{{ fields.referenced_cf_field_name.properties.description }}}
```

## 基本的なフィールドアクセス {#basic-field-access}

必要に応じて、すべてのフィールドを繰り返し使用できる、直接フィールドアクセスをお勧めします。

### ダイレクトフィールドアクセス（推奨） {#direct-field-access-recommended}

フィールドマップを使用して、名前でフィールドに直接アクセスします。

```handlebars
<!DOCTYPE html>
<html>
<head>
  <title>{{properties.title}}</title>
</head>
<body>
  <article>
    <h1>{{{fields.title}}}</h1>
    <p class="subtitle">{{{fields.subtitle}}}</p>
    <div class="content">
      {{{fields.description}}}
    </div>
    <div class="image">
      {{{fields.primaryImage}}}
    </div>
  </article>
</body>
</html>
```

重要な点：

* フィールド値に事前にレンダリングされたHTML（リッチテキスト）が含まれている場合は、3つの括弧`{{{ }}}`を使用します
* フィールド名（タイトル、サブタイトル、説明、primaryImage） **must**&#x200B;は、コンテンツフラグメントモデル **に正確に一致します**
* 見つからないフィールドはレンダリングされません。エラーはスローされず、レンダリングされたHTML フラグメントにHandlebars構文が存在し（表示されたままになります）

### すべてのフィールドに対して繰り返し実行する {#iterate-through-all-fields}

フィールド名が事前にわからない場合は、`allFields`を使用します。

```handlebars
<table>
  <thead>
    <tr>
      <th>Field Name</th>
      <th>Field Value</th>
    </tr>
  </thead>
  <tbody>
    {{#each allFields}}
    <tr>
      <td>{{name}}</td>
      <td>{{{value}}}</td>
    </tr>
    {{/each}}
  </tbody>
</table>
```

重要な点：

* `{{name}}`は二重中括弧（プレーンテキストのラベル）を使用します
* `{{{value}}}`は3つの中括弧を使用します（事前にレンダリングされたHTML値）

## ネストされたコンテンツフラグメント {#nested-content-fragments}

コンテンツフラグメントフィールドが別のコンテンツフラグメントを参照している場合、ドット表記法を使用して、参照されているフラグメントのフィールドに直接アクセスできます。

### 単一レベルのネスト {#single-level-nesting}

単一レベルのネストの例：

```handlebars
<article>
  <h1>{{{fields.title}}}</h1>

  <!-- Access author (a referenced Content Fragment) -->
  <div class="author-info">
    <h3>Author</h3>
    <p>Name: {{{fields.author.name}}}</p>
    <p>Email: {{{fields.author.email}}}</p>
    <p>Bio: {{{fields.author.bio}}}</p>
  </div>

  <div class="content">
    {{{fields.content}}}
  </div>
</article>
```

パターン：`fields.referenceFieldName.nestedFieldName`

### マルチレベルネスト {#multi-level-nesting}

このシステムは、ネスト深度を無制限にサポートします。

```handlebars
<article>
  <h1>{{{fields.title}}}</h1>

  <div class="author-details">
    <!-- Level 1: Author -->
    <p>Author: {{{fields.author.name}}}</p>

    <!-- Level 2: Author's Organization -->
    <p>Organization: {{{fields.author.organization.name}}}</p>
    <p>Website: {{{fields.author.organization.website}}}</p>

    <!-- Level 3: Organization's Address -->
    <p>Located in: {{{fields.author.organization.address.city}}},
    {{{fields.author.organization.address.country}}}</p>
  </div>

  <div class="content">
    {{{fields.content}}}
  </div>
</article>
```

パターン：`fields.level1.level2.level3.fieldName` （深さが制限されています。デフォルトは5で、APIを使用する場合は10に拡張できます）

### API パラメーター要件：ハイドレーション {#api-parameter-requirements}

ネストされたコンテンツフラグメントへのアクセスを有効にするには、API呼び出しに`hydration` クエリパラメーターを含める必要があります。

ハイドレーションを有効にするには：

```http
# Enable hydration with depth=2 for 2 levels of nesting
GET /adobe/sites/cf/fragments/{id}/preview?hydration=%7B%22enabled%22%3Atrue%2C%22maxDepth%22%3A2%7D
```

| `maxDepth` | 読み込まれるもの |
|--- |--- |
| `1` | メインフラグメント + ダイレクト参照 |
| `2` | メインフラグメント +直接参照+その参照 |
| `3+` | 最大10 レベルまで続行 |

## 複数値フィールド {#multi-valued-fields}

複数値フィールドにはいくつかの種類があります。

### 複数値テキストフィールド {#multi-valued-text-fields}

テキスト、[number](#multi-valued-number-fields)、日付、およびその他の単純なフィールドは、複数値の場合に配列になります。

```handlebars
<article>
  <h1>{{{fields.title}}}</h1>

  <!-- Access individual items by index (use dot before bracket) -->
  <div class="tags">
    <span class="tag">{{{fields.tags.[0]}}}</span>
    <span class="tag">{{{fields.tags.[1]}}}</span>
  </div>

  <!-- Better: Iterate through all tags -->
  <div class="tags">
    {{#each fields.tags}}
    <span class="tag">{{{this}}}</span>
    {{/each}}
  </div>
</article>
```

Handlebarsのインデックスで配列項目にアクセスする場合は、次の点に注意してください。

* 使用方法:
   * `.[0]` （角括弧の前のドット）
* なし：
   * `[0]`

### 複数値フィールド {#multi-valued-number-fields}

数値は、レンダリング用に[文字列](#multi-valued-text-fields)に変換されます。

```handlebars
<div class="pricing">
  <h3>Available Prices:</h3>
  {{#each fields.prices}}
  <span class="price">${{{this}}}</span>
  {{/each}}
</div>
```

### 複数値のコンテンツフラグメント参照 {#multi-valued-content-fragment-references}

フィールドが複数のコンテンツフラグメントを参照する場合：

```handlebars
<div class="authors">
  <h3>Authors:</h3>
  {{#each fields.authors}}
  <div class="author">
    <h4>{{{this.name}}}</h4>
    <p>Email: {{{this.email}}}</p>
    {{#if this.bio}}
    <p class="bio">{{{this.bio}}}</p>
    {{/if}}
  </div>
  {{/each}}
</div>
```

### 複数値のアセット参照 {#multi-valued-asset-references}

アセット（画像やドキュメントなど）であるコンテンツタイプ用に設定された[ コンテンツ参照](/help/sites-cloud/administering/content-fragments/content-fragment-models.md#content-reference) フィールドは、HTMLとして事前にレンダリングされます。 複数値のアセットは配列になります。

```handlebars
<!-- Single asset -->
<div class="hero-image">
  {{{fields.heroImage}}}
</div>

<!-- Multi-valued: iterate through all images -->
<div class="gallery">
  {{#each fields.gallery}}
  <div class="image">{{{this}}}</div>
  {{/each}}
</div>
```

### ネストされた複数値参照 {#nested-multi-valued-references}

複数値の参照には、任意の深さで複数値の参照を含めることができます。

```handlebars
{{#each fields.chapters}}
<div class="chapter">
  <h3>Chapter: {{{this.title}}}</h3>

  {{#each this.authors}}
  <p>Author: {{{this.name}}}</p>

  {{#each this.publications}}
  <p>Publication: {{{this.title}}}</p>
  {{/each}}
  {{/each}}
</div>
{{/each}}
```

## ループと反復 {#loops-and-iteration}

Handlebarsは、配列とオブジェクトを反復処理するための`{{#each}}` ヘルパーを提供します。

### 配列の繰り返し {#iterating-over-arrays}

配列を繰り返す例：

```handlebars
<!-- Simple array iteration -->
{{#each fields.tags}}
<span class="tag">{{{this}}}</span>
{{/each}}

<!-- Array of objects -->
{{#each fields.authors}}
<div class="author">
  <h4>{{{this.name}}}</h4>
  <p>{{{this.email}}}</p>
</div>
{{/each}}

<!-- With empty-state fallback -->
{{#each fields.tags}}
<span class="tag">{{{this}}}</span>
{{else}}
<p>No tags available.</p>
{{/each}}
```

### ループ内の特殊変数 {#special-variables-in-loops}

`{{#each}}` ブロック内では、Handlebarsは特殊な変数を提供します。

```handlebars
{{#each fields.items}}
<div class="item">
  <p>Index: {{@index}}</p>     <!-- 0-based index -->
  <p>Number: {{@number}}</p>   <!-- 1-based index -->
  <p>First: {{@first}}</p>     <!-- true for first item -->
  <p>Last: {{@last}}</p>       <!-- true for last item -->
  <p>Value: {{{this}}}</p>     <!-- current item -->
</div>
{{/each}}

<!-- Example: numbered steps with first/last CSS classes -->
<ul>
  {{#each fields.steps}}
  <li class="{{#if @first}}first{{/if}} {{#if @last}}last{{/if}}">
    Step {{@number}}: {{{this}}}
  </li>
  {{/each}}
</ul>
```

### 参照されたフラグメントの繰り返し {#iterating-over-referenced-fragments}

参照されたフラグメントに対する反復の例：

```handlebars
{{#if hasReferencedFragments}}
<section class="references">
  <h2>Related Content</h2>
  {{#each referencedFragments}}
  <article id="{{anchorId}}">
    <h3>{{title}}</h3>
    {{#if hasDescription}}
    <p>{{description}}</p>
    {{/if}}
    {{#if hasFields}}
    <ul>
      {{#each allFields}}
      <li><strong>{{name}}:</strong> {{{value}}}</li>
      {{/each}}
    </ul>
    {{/if}}
  </article>
  {{/each}}
</section>
{{/if}}
```

### ネストされたループ {#nested-loops}

ネストされたループの例：

```handlebars
{{#each fields.categories}}
<section class="category">
  <h2>{{{this.name}}}</h2>

  {{#each this.products}}
  <article class="product">
    <h3>{{{this.name}}}</h3>
    <p>{{{this.description}}}</p>
  </article>
  {{/each}}
</section>
{{/each}}
```

## 条件付きレンダリング {#conditional-rendering}

条件を使用して、データの可用性にもとづいてコンテンツを表示または非表示にします。

### 基本If/Else {#basic-if-else}

基本的なif-else構文の例：

```handlebars
{{#if hasMainDescription}}
<p class="description">{{properties.description}}</p>
{{else}}
<p class="no-description">No description available.</p>
{{/if}}

<!-- Check field existence before rendering -->
{{#if fields.author}}
<div class="author">
  <p>By {{{fields.author.name}}}</p>
</div>
{{/if}}

{{#if fields.publishDate}}
<time>{{{fields.publishDate}}}</time>
{{/if}}
```

### （負の条件）を除く {#unless-negative-conditional}

`unless` ヘルパー：

```handlebars
<!-- Show author unless explicitly hidden -->
{{#unless fields.hideAuthor}}
<div class="author">{{{fields.author.name}}}</div>
{{/unless}}
```

### ネストされた条件 {#nested-conditials}

ネストされた条件の例：

```handlebars
{{#if fields.author}}
<div class="author">
  <h3>{{{fields.author.name}}}</h3>

  {{#if fields.author.bio}}
  <p class="bio">{{{fields.author.bio}}}</p>
  {{/if}}

  {{#if fields.author.website}}
  <a href="{{{fields.author.website}}}">Visit Website</a>
  {{/if}}
</div>
{{/if}}
```

## 組み込みのHandlebars ヘルパー {#built-in-handlebars-helpers}

Handlebarsには、`{{#if}}`と`{{#each}}`を超える複数の組み込みヘルパーが含まれています。

| ヘルパー | 説明 |
|--- |--- |
| `{{#if condition}}` | 条件が真の場合にコンテンツをレンダリングします。 偽の値：`false`、`undefined`、`null`、`0`、`""`、`[]` |
| `{{#unless condition}}` | 条件が偽の場合にコンテンツをレンダリングします（`#if`の逆） |
| `{{#each array}}` | 各アイテムに対してコンテンツを繰り返します。空の配列に対して`{{else}}`をサポートします |
| `{{#with object}}` | ネストされたオブジェクトの新しいスコープを作成し、パスの繰り返しを減らします |
| `{{lookup this "key"}}` | 名前でプロパティを動的に検索する |

### ヘルパーを使用 {#with-helper}

ネストされたオブジェクトの新しいスコープを作成して、繰り返しパスの接頭辞を減らします。

```handlebars
{{#with fields.author}}
<div class="author">
  <h3>{{{name}}}</h3>     <!-- same as fields.author.name -->
  <p>{{{email}}}</p>      <!-- same as fields.author.email -->
  <p>{{{bio}}}</p>        <!-- same as fields.author.bio -->
</div>
{{/with}}

<!-- Useful for deeply nested objects -->
{{#with fields.author.organization}}
<div class="organization">
  <h4>{{{name}}}</h4>
  <p>{{{website}}}</p>
  {{#with address}}
  <address>
    {{{street}}}<br/>
    {{{city}}}, {{{country}}}
  </address>
  {{/with}}
</div>
{{/with}}
```

## 高度なパターン {#advanced-patterns}

高度なパターンの例がいくつかあります。

### ネストされたループでの親コンテキストへのアクセス {#accessing-parent-context-in-nested-loops}

ネストされたループ内から親スコープにアクセスするには、`../`を使用します。

```handlebars
<h1>{{{fields.title}}}</h1>

{{#each fields.chapters}}
<section class="chapter">
  <h2>Chapter {{@number}}: {{{this.title}}}</h2>

  {{#each this.sections}}
  <article>
    <!-- Access parent chapter via ../ -->
    <p>Chapter: {{{../title}}}</p>

    <!-- Access root context via ../../ -->
    <p>Book: {{{../../fields.title}}}</p>

    <h3>{{{this.title}}}</h3>
    <div>{{{this.content}}}</div>
  </article>
  {{/each}}
</section>
{{/each}}
```

### 動的なCSS クラス {#dynamic-css-classes}

動的なCSS クラスの例：

```handlebars
<article class="content-fragment {{#if hasMainDescription}}with-description{{/if}} {{#if hasReferencedFragments}}has-refs{{/if}}">
  <h1>{{properties.title}}</h1>
</article>

<ul class="tag-list">
  {{#each fields.tags}}
  <li class="tag {{#if @first}}first{{/if}} {{#if @last}}last{{/if}}">
    {{{this}}}
  </li>
  {{/each}}
</ul>
```

## 完全な例 {#complete-examples}

いくつかの完全な例が参照のために提供されています。

### 作成者のブログ投稿

著者の詳細を記載したブログ記事：

```handlebars
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>{{properties.title}}</title>
  <style>
    body { font-family: Arial, sans-serif; margin: 40px; }
    .author-card { background: #f5f5f5; padding: 20px; border-radius: 8px; }
    .tags { display: flex; gap: 10px; }
    .tag { background: #007bff; color: white; padding: 5px 10px; border-radius: 4px; }
  </style>
</head>
<body>
  <article>
    <header>
      <h1>{{{fields.title}}}</h1>
      {{#if fields.publishDate}}
      <time datetime="{{{fields.publishDate}}}">{{{fields.publishDate}}}</time>
      {{/if}}
      {{#if fields.tags}}
      <div class="tags">
        {{#each fields.tags}}
        <span class="tag">{{{this}}}</span>
        {{/each}}
      </div>
      {{/if}}
    </header>

    {{#if fields.heroImage}}
    <figure>
      {{{fields.heroImage}}}
      {{#if fields.imageCaption}}
      <figcaption>{{{fields.imageCaption}}}</figcaption>
      {{/if}}
    </figure>
    {{/if}}

    <div class="content">
      {{{fields.content}}}
    </div>

    {{#if fields.author}}
    <aside class="author-card">
      <h3>About the Author</h3>
      <h4>{{{fields.author.name}}}</h4>
      {{#if fields.author.profilePicture}}
      <div class="author-image">{{{fields.author.profilePicture}}}</div>
      {{/if}}
      {{#if fields.author.bio}}
      <p>{{{fields.author.bio}}}</p>
      {{/if}}
      {{#if fields.author.email}}
      <p>Contact: <a href="mailto:{{{fields.author.email}}}">{{{fields.author.email}}}</a></p>
      {{/if}}
    </aside>
    {{/if}}
  </article>
</body>
</html>
```

必要なAPI呼び出し：

```http
GET /adobe/sites/cf/fragments/{id}/preview?hydration=%7B%22enabled%22%3Atrue%2C%22maxDepth%22%3A1%7D
```

### 汎用テーブルビュー（フィールドに関する事前知識なし） {#generic-table-view-no-prior-knowledge-of-fields}

フィールドに関する固有の知識がない汎用的なテーブルビュー。 は、**汎用テンプレート**&#x200B;と似ています。

```handlebars
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>{{properties.title}}</title>
  <style>
    body { font-family: Arial, sans-serif; margin: 40px; }
    table { width: 100%; border-collapse: collapse; margin: 20px 0; }
    th, td { border: 1px solid #ddd; padding: 12px; text-align: left; }
    th { background-color: #f4f4f4; font-weight: bold; }
    .ref-section { background: #f9f9f9; padding: 20px; margin: 20px 0; border-radius: 8px; }
  </style>
</head>
<body>
  <header>
    <h1>{{properties.title}}</h1>
    {{#if properties.description}}<p>{{properties.description}}</p>{{/if}}
    <p><small>Path: {{properties.path}}</small></p>
  </header>

  {{#if hasFields}}
  <section>
    <h2>Fields</h2>
    <table>
      <thead>
        <tr><th>Field Name</th><th>Field Value</th></tr>
      </thead>
      <tbody>
        {{#each allFields}}
        <tr>
          <td><strong>{{name}}</strong></td>
          <td>{{{value}}}</td>
        </tr>
        {{/each}}
      </tbody>
    </table>
  </section>
  {{/if}}

  {{#if hasReferencedFragments}}
  <section class="ref-section">
    <h2>Referenced Content Fragments</h2>
    {{#each referencedFragments}}
    <article id="{{anchorId}}" style="margin-bottom: 30px;">
      <h3>{{title}}</h3>
      {{#if hasDescription}}<p>{{description}}</p>{{/if}}
      <p><small>Path: {{path}}</small></p>
      {{#if hasFields}}
      <table>
        <thead>
          <tr><th>Field Name</th><th>Field Value</th></tr>
        </thead>
        <tbody>
          {{#each allFields}}
          <tr>
            <td><strong>{{name}}</strong></td>
            <td>{{{value}}}</td>
          </tr>
          {{/each}}
        </tbody>
      </table>
      {{/if}}
    </article>
    {{/each}}
  </section>
  {{/if}}
</body>
</html>
```

## ベストプラクティス {#best-practices}

ベストプラクティスには、次のようなものがあります。

1. HTMLのマークアップコンテンツを含むフィールド値には、必ず3つの中括弧を使用してください。

   * フィールド値は、事前にレンダリングされたHTMLです。

     >[!NOTE]
     >
     >ダブルブレースでは、生のHTML タグがプレーンテキストとして表示されます。

   ```handlebars
   <!-- CORRECT -->
   {{{fields.description}}}
   
   <!-- WRONG - displays HTML tags as text -->
   {{fields.description}}
   ```

1. ネストされたフィールドにアクセスする前に、存在を確認します。

   ```handlebars
   <!-- GOOD: check before accessing nested fields -->
   {{#if fields.author}}
   <p>By {{{fields.author.name}}}</p>
   {{/if}}
   
   <!-- RISKY: may render empty if author is not set -->
   <p>By {{{fields.author.name}}}</p>
   ```

1. 可能な限り直接的なフィールドアクセスを確保する。

   * `allFields`を繰り返して名前で照合するよりも、読みやすく、維持しやすくなります。

1. セクションコメント付きの構造テンプレート。

   ```handlebars
   {{! ===== HEADER SECTION ===== }}
   <header>
     <h1>{{properties.title}}</h1>
   </header>
   
   {{! ===== MAIN CONTENT ===== }}
   <main>
     {{#if hasFields}}
     <!-- fields rendering -->
     {{/if}}
   </main>
   
   {{! ===== REFERENCES ===== }}
   {{#if hasReferencedFragments}}
   <!-- references rendering -->
   {{/if}}
   ```

1. フォールバックにより、欠けているデータを適切に処理。

   ```handlebars
   {{#if fields.title}}
   <h1>{{{fields.title}}}</h1>
   {{else}}
   <h1>Untitled</h1>
   {{/if}}
   ```

1. 常に適切なHTML文書構造を使用してください。

   ```handlebars
   <!DOCTYPE html>
   <html lang="en">
   <head>
     <meta charset="UTF-8">
     <meta name="viewport" content="width=device-width, initial-scale=1">
     <title>{{properties.title}}</title>
   </head>
   <body>
     <!-- your content here -->
   </body>
   </html>
   ```

1. 様々なコンテンツシナリオでテストします。

   * すべてのフィールドに情報が入力されました
   * オプションフィールドがありません
   * 空の複数値フィールド
   * ディープネスティング（複数レベル）
   * 読み込みに失敗する参照

1. セマンティック HTML要素を使用します。

   * アクセシビリティを向上させるには、`<article>`、`<header>`、`<main>`、`<footer>`、`<time>`、`<address>`などを使用します。

1. CSSでスタイルを保持します。

   * `<style>`個のタグまたは外部スタイルシートを使用します。
   * インラインスタイルは可能な限り避けます。

1. ドキュメントの複雑なロジック：

   * Handlebars コメント `({{! }})`を使用します。
   * レンダリングされた出力に表示されるHTML コメントは使用しないでください。

## トラブルシューティング {#troubleshooting}

トラブルシューティングのヒントには、次のようなものがあります。

| 問題 | 症状 | ソリューション |
|--- |--- |--- |
| フィールドには、HTML タグがテキストとして表示されます | `<p>Hello World</p>`は文字通り表示されます | 3つの中括弧を使用：`{{{fields.description}}}` |
| ネストされたコンテンツフラグメントフィールドが空であるか、[ オブジェクトオブジェクト ]を表示しています | `{{{fields.author.name}}}`は空白です | API呼び出しでハイドレーションを有効にします。フィールド名のスペルを確認します。`maxDepth`が十分に深いことを確認してください |
| 複数値フィールドには、最初の項目のみが表示されます | 5つの項目を持つ配列は1つだけをレンダリングします | `{{#each fields.tags}}`を使用してすべての項目を繰り返します |
| 配列インデックスアクセスが機能しない | `{{{fields.tags[0]}}}`は空のレンダリングです | ドット区切り記号の構文を使用：`{{{fields.tags.[0]}}}` |
| 参照フラグメントが表示されない | `hasReferencedFragments`は常にfalseです | ハイドレーションを有効にする：`?hydration=%7B%22enabled%22%3Atrue%7D;`も`{{#if referencesError}}`を確認します |
| テンプレートは何もレンダリングしません | 空のページまたは空白の出力 | 閉じられていない`{{#if}}`または`{{#each}}` ブロックを確認してください。診断出力を追加してください：`<pre>hasFields: {{hasFields}} \| title: {{properties.title}}</pre>` |
| レンダリングされたページにコメントが表示される | エンドユーザーに表示されるHTMLのコメントテキスト | HTML `<!-- comment -->`の代わりにHandlebars コメント `{{! comment }}`を使用 |
| 条件は常にtrueと評価されます | `{{#if fields.enabled}}`は常に真実です | 注意：文字列`"false"`はHandlebarsで正しく表示されます。 実際の`false`、`null`、`undefined`、`0`、`""`および`[]`のみが偽装されています。 |
| エンティティとしてレンダリングする特殊文字 | `<`、`&`の代わりに`&lt;`、`&amp;`が表示されます | プレレンダリングされたHTML コンテンツには、3つの中括弧を使用します：`{{{fields.content}}}` |
| 内部ループから外部ループ変数にアクセスできません | 親`#each`の変数が定義されていません | 親スコープに`../`を使用：`{{{../name}}}`、祖父母に`../../`を使用 |
| 空のリストにフォールバックメッセージが表示されない | 項目が0の複数値フィールドは何も表示しません | `{{#each}}`内で`{{else}}`を使用：`{{#each fields.tags}}...{{else}}<p>No tags</p>{{/each}}` |

### アセットの操作 {#working-with-assets}

コンテンツフラグメントから参照されるAssetsは、AEMによってHTMLとして事前にレンダリングされます。 したがって、すべてのアセット参照には3つの中括弧が必須です。

| アセットタイプ | 次のようにレンダリング |
|--- |--- |
| 画像 | `<img src="..." alt="...">` |
| ビデオ | `<video>`要素 |
| ドキュメント | `<a href="...">` リンク |

重要な点：

* アセットフィールドには常に3つの中括弧を使用します。二重中括弧を使用すると、生成されたHTML タグはエスケープされ、画像、ビデオ、リンクをレンダリングするのではなく、生のテキストとして表示されます。

### アセットフィールドの使用状況 {#asset-field-usage}

アセットフィールドの使用例：

```handlebars
<!-- CORRECT - triple braces render the image -->
{{{fields.heroImage}}}
<!-- Output: <img src="path/to/image.jpg" alt="Hero"> -->

<!-- WRONG - double braces escape the tag, showing it as text -->
{{fields.heroImage}}
<!-- Output: &lt;img src="path/to/image.jpg" alt="Hero"&gt; -->
```

## カスタムテンプレートヘルパー {#customer-template-helpers}

このシステムは、カスタム HTML属性を持つHTML要素を生成するためのカスタムハンドルバーのヘルパーを提供します。 これらのヘルパーは、生成されたマークアップを制御すると同時に、事前にレンダリングされたコンテンツからソース URLを抽出する複雑さを処理します。

使用可能なヘルパー：

1. `asset` - カスタム属性を持つ`<img>` タグを生成します
1. `text` - カスタム属性を持つテキストコンテンツをラップする`<span>` タグを生成します

### `asset` ヘルパー {#asset-helper}

構文：

```handlebars
{{{asset fieldValue attribute1="value1" attribute2="value2"}}}
```

重要な点：

* アセットヘルパーには、ダブルブレースではなく、トリプルブレース `{{{ }}}`を使用します。

#### 4つの基本的な例 {#four-basic-examples}

基本的な例は次の4つです。

```handlebars
<!-- Add a CSS class to an image -->
{{{asset fields.heroImage class="hero-image"}}}
<!-- Output: <img src="..." alt="..." class="hero-image"> -->

<!-- Add multiple CSS classes -->
{{{asset fields.productImage class="product-img responsive shadow"}}}

<!-- Add id and class -->
{{{asset fields.logo class="brand-logo" id="main-logo"}}}

<!-- Add data attributes -->
{{{asset fields.thumbnail class="thumb" data-category="product" data-id="123"}}}
```

#### サポートされる属性 {#supported-attributes}

有効なHTML属性を追加できます。

| 属性 |  例 |
|--- |--- |
| `class` | `class="my-class another-class"` |
| `id` | `id="unique-id"` |
| `alt` | `alt="Custom alt text" (overrides existing alt)` |
| `data-*` | `data-index="1" data-type="hero"` |
| `aria-*` | `aria-label="Description" aria-hidden="true"` |
| `width` | `width="300"` |
| `height` | `height="200"` |
| `loading` | `loading="lazy"` |
| `style` | `style="border-radius: 8px;"` |

#### 代替テキストを上書き {#override-alt-text}

元の画像の`alt`属性を上書きできます：

```handlebars
{{{asset fields.photo alt="Custom description for accessibility"}}}
```

#### 複雑な例 {#complex-example}

複雑な例としては、次のようなものがあります。

```handlebars
<article class="blog-post">
<header>
{{{asset fields.featuredImage 
class="featured-image responsive" 
id="post-hero"
loading="lazy"
data-post-id="12345"}}}
</header>
</article>
```

#### ループでの使用 {#using-with-loops}

ループのアセットヘルパー：

```handlebars
{{#each fields.galleryImages}}
{{{asset this class="gallery-item" data-index=@index}}}
{{/each}}
```

### `text` ヘルパー {#text-helper}

テキストヘルパーは、カスタム CSS クラスとHTML属性を含むテキストコンテンツをラッピングする`<span>` タグを生成します。 個々のテキストフィールドのスタイル設定に便利です。

構文：

```handlebars
{{{text fieldValue attribute1="value1" attribute2="value2"}}}
```

重要な点：

* テキストヘルパーには、ダブルブレースではなく、トリプルブレース `{{{ }}}`を使用します。

#### 3つの基本的な例 {#three-basic-examples}

基本的な例は次の3つです。

```handlebars
<!-- Add a CSS class to text -->
{{{text fields.title class="article-title"}}}
<!-- Output: <span class="article-title">The Title Text</span> -->

<!-- Add multiple attributes -->
{{{text fields.price class="price-tag" id="product-price" data-currency="USD"}}}

<!-- Style inline text -->
{{{text fields.highlightedText class="highlighted" style="background: yellow;"}}}
```

#### 一般的なユースケース {#common-use-cases}

一般的なユースケースには、次のようなものがあります。

```handlebars
<!-- Styling article metadata -->
<article>
<header>
{{{text fields.category class="category-badge"}}}
<h1>{{{fields.title}}}</h1>
{{{text fields.author class="byline"}}}
{{{text fields.publishDate class="date"}}}
</header>
</article>

<!-- Creating styled labels -->
<div class="product-card">
{{{text fields.productName class="product-name"}}}
{{{text fields.brand class="brand-label" data-brand-id="abc"}}}
{{{text fields.price class="price" id="main-price"}}}
</div>

<!-- Accessibility enhancements -->
{{{text fields.importantNote class="alert" role="alert" aria-live="polite"}}}
```

#### ループ付き {#with-loops}

ループを使用する一般的なユースケースには、次のようなものがあります。

```handlebars
{{#each fields.tags}}
{{{text this class="tag-badge"}}}
{{/each}}
```

### ヘルパー – 属性検証 {#helpers-attribute-validation}

どちらのヘルパーも、属性名を出力に含める前に検証します。

有効な属性名：

* 文字（a ～ z、A ～ Z）で始める必要があります
* 文字、数字、ハイフン、アンダースコアのみを含めることができます。[命名規則](/help/implementing/developing/introduction/naming-conventions.md)を参照してください。
* 大文字小文字を区別しない
* 次に例を示します。
   * 有効：
      * `class`, `id`, `data-value`, `aria-label`, `my_attr`, `dataIndex1`
   * 無効：
      * `123-attr`, `-class`, `@special`, `$money`

無効な属性名は、ログ内の警告でサイレントにスキップされます。

```handlebars
{{{asset fields.image class="valid" 123-invalid="skipped" id="also-valid"}}}
<!-- Output: <img src="..." alt="..." class="valid" id="also-valid"> -->
<!-- 123-invalid is skipped because it starts with a number -->
```

重要な点：

* サーバーのログで「ブロックされた無効な属性名形式」警告を確認します。

## ヘルパーへの直接出力の比較 {#comparing-direct-output-to-helpers}

直接出力`{{{fields.xxx}}}`をiseする場合：

* カスタムスタイルは必要ありません
* デフォルトの出力をそのまま使用する
* フィールドには、変更しない複雑なHTMLが含まれています

ヘルパーを使用する場合：

* スタイル設定のためにCSS クラスを追加する必要があります
* カスタム HTML属性（`data-*`、`aria-*`など）を追加する必要があります
* 必要なのは、一貫性のある制御されたHTMLの構造です

比較：

```handlebars
<!-- Direct output - uses whatever HTML the system generates -->
{{{fields.heroImage}}}
<!-- Output: <img src="/path/image.jpg" alt="Hero Image"> -->

<!-- With asset helper - full control over attributes -->
{{{asset fields.heroImage class="hero responsive" id="main-hero" loading="lazy"}}}
<!-- Output: <img src="/path/image.jpg" alt="Hero Image" class="hero responsive" id="main-hero" loading="lazy"> -->
```

## クイックリファレンス {#quick-reference}

一部のクイックリファレンス情報は参照用に提供されています。

### コンテキスト変数 {#context-variables}

コンテキスト変数：

```handlebars
{{properties}}                <!-- Main fragment metadata -->
{{fields}}                    <!-- Map keyed by field name to rendered values (such as strings, lists, nested maps for Content Fragment references, commerce maps, HTML, and others) -->
{{allFields}}                 <!-- List of { name, value } maps (uniform iteration) -->
{{hasFields}}.                <!-- Boolean -->
{{hasReferencedFragments}}.   <!-- Boolean -->
{{referencedFragments}}       <!-- List of referenced-fragment maps -->
```

### フィールドアクセス {#field-access}

フィールドへのアクセス方法：

```handlebars
{{{fields.fieldName}}}                    <!-- Direct field -->
{{{fields.author.name}}}                  <!-- Nested Content Fragment field -->
{{{fields.author.org.address.city}}}      <!-- Multi-level nesting -->
{{{fields.tags.[0]}}}                     <!-- Array by index -->
{{#each fields.tags}}...{{/each}}         <!-- Array iteration -->
{{{fields.authors.[0].name}}}             <!-- Multi-valued Content Fragment reference -->
```

### 制御フロー {#control-flow}

制御フロー：

```handlebars
{{#if condition}}...{{/if}}               <!-- Conditional -->
{{#if condition}}...{{else}}...{{/if}}    <!-- If/else -->
{{#unless condition}}...{{/unless}}       <!-- Negative conditional -->
{{#each array}}...{{/each}}               <!-- Iteration -->
{{#each array}}...{{else}}...{{/each}}    <!-- Iteration with fallback -->
{{#with object}}...{{/with}}              <!-- Change scope -->
```

### ループ変数 {#loop-variables}

ループ変数：

```handlebars
{{@index}}        <!-- 0-based index -->
{{@number}}       <!-- 1-based index -->
{{@first}}        <!-- true for first item -->
{{@last}}         <!-- true for last item -->
{{@key}}          <!-- Object property name -->
{{this}}          <!-- Current item -->
{{../parent}}     <!-- Access parent scope -->
```

### カスタムテンプレートヘルパー {#custom-template-helpers}

カスタムテンプレートヘルパー：

```handlebars
{{{asset fields.image class="css-class"}}}                <!-- Image with class -->
{{{asset fields.image class="c1" id="my-id"}}}            <!-- Image with multiple attrs -->
{{{asset fields.image alt="Custom alt text"}}}            <!-- Override alt text -->
{{{asset fields.image loading="lazy" data-x="val"}}}      <!-- Custom attributes -->

{{{text fields.title class="title-class"}}}               <!-- Span with class -->
{{{text fields.price class="price" id="p1"}}}             <!-- Span with multiple attrs -->
{{{text this class="item" data-index=@index}}}            <!-- In loops -->
```

## その他のリソース {#additional-resources}

次のその他のリソースを使用できます。

* [Handlebars ドキュメント](https://handlebarsjs.com/)
* [Handlebars ビルトインヘルパー](https://handlebarsjs.com/guide/builtin-helpers.html)
* [AEM コンテンツフラグメントのドキュメント](/help/sites-cloud/administering/content-fragments/overview.md)
* [コンテンツフラグメント視覚化テンプレート API](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/stable/sites/cvt/)

