---
title: ユニバーサルエディター用の RTE の設定
description: ユニバーサルエディターでリッチテキストエディター（RTE）を設定する方法を説明します。
feature: Developing
role: Admin, Developer
exl-id: 350eab0a-f5bc-49c0-8e4d-4a36a12030a1
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '497'
ht-degree: 1%

---

# ユニバーサルエディター用の RTE の設定 {#configure-rte}

ユニバーサルエディターでリッチテキストエディター（RTE）を設定する方法を説明します。

>[!NOTE]
>
>このドキュメントは、ユニバーサルエディターの新しい RTE に適用されます。この RTE は早期導入者機能として利用できます。 この新機能のテストに興味がある場合は、[ 詳しくはリリースノートを参照してください ](/help/release-notes/universal-editor/current.md#new-rte)。

## 概要 {#overview}

ユニバーサルエディターには、作成者がテキストの編集時に書式設定の変更を適用できるリッチテキストエディター（RTE）がインプレースおよびプロパティパネルで用意されています。

この RTE は、[ コンポーネントフィルターを使用して設定できます。](/help/implementing/universal-editor/filtering.md) このドキュメントでは、使用可能な設定オプションと例について説明します。

## 設定の構造 {#structure}

RTE 設定は、次の 2 つの部分で構成されます。

* [`toolbar`](#toolbar): ツールバー設定は、UI で使用できる編集オプションとその編成方法を制御します。
* [`actions`](#actions): アクション設定を使用すると、個々の編集アクションの動作と外観をカスタマイズできます。

これらの設定は、プロパティ [ を使用して、](/help/implementing/universal-editor/filtering.md) コンポーネントフィルター `rte` の一部として定義できます。

```json
[
  {
    "id": "richtext",
    "rte": {
      "toolbar": {
        // Toolbar configuration
      },
      "actions": {
        // Action-specific configurations
      }
    },
    "components": [
      "richtext"
    ]
  }
]
```

## ツールバー設定 {#toolbar}

ツールバー設定は、UI で使用できる編集オプションとその編成方法を制御します。 使用可能なセクションは次のとおりです

```json
{
  "toolbar": {
    // Text formatting options
    "format": ["bold", "italic", "underline", "strike"],
    // Text alignment options
    "alignment": ["left", "center", "right", "justify"],
    // Text direction options, right-to-left or left-to-right
    "direction": ["rtl", "ltr"],
    // Indentation controls
    "indentation": ["indent", "outdent"],
    // Block-level elements
    "blocks": ["paragraph", "h1", "h2", "h3", "h4", "h5", "h6", "code_block"],
    // List options
    "list": ["bullet_list", "ordered_list"],
    // Content insertion
    "insert": ["link", "unlink", "image"],
    // Superscript/subscript
    "sr_script": ["superscript", "subscript"],
    // Editor utilities
    "editor": ["removeformat"],
    // Section ordering (optional)
    "sections": ["format", "alignment", "list"]
  }
}
```

## アクションの設定 {#actions}

アクション設定を使用すると、個々の編集アクションの動作と外観をカスタマイズできます。 使用可能なセクションを以下に示します。

### アクションの書式設定 {#format}

フォーマットアクションは、書式設定を適用するために使用され、セマンティックバリアントを選択するためのHTML タグの切り替えをサポートします。 以下の節を使用できます。

```json
{
  "actions": {
    "bold": {
      "tag": "strong",      // Use <strong> instead of <b>
      "shortcut": "Mod-B",  // Custom keyboard shortcut
      "label": "Make Bold"  // Custom button label 
    },
    "italic": {
      "tag": "em",          // Use <em> instead of <i>
      "shortcut": "Mod-I",
      "label": "Italicize"
    },
    "strike": {
      "tag": "del"          // Use <del> instead of <s>
    }
  }
}
```

### リストアクション {#list}

リストアクションは、HTML構造を制御するためのコンテンツラッピングをサポートしています。 以下の節を使用できます。

```json
{
  "actions": {
    "bullet_list": {
      "wrapInParagraphs": true,    // <ul><li><p>content</p></li></ul>
      "shortcut": "Mod-Shift-8",   // Custom shortcut
      "label": "Bullet List"       // Custom label
    },
    "ordered_list": {
      "wrapInParagraphs": false,   // <ol><li>content</li></ol> (default)
      "shortcut": "Mod-Shift-9"
    }
  }
}
```

### リンクアクション {#link}

リンクアクションは、リンクの動作を管理するためのターゲット属性コントロールをサポートしています。 以下の節を使用できます。

```json
{
  "actions": {
    "link": {
      "hideTarget": false,       // Show target attribute options (default)
      "shortcut": "Mod-K",       // Custom keyboard shortcut
      "label": "Insert Link"     // Custom button label
    },
    "unlink": {
      "shortcut": "Mod-Shift-K", // Custom keyboard shortcut
      "label": "Remove Link"     // Custom button label
    }
  }
}
```

#### リンク設定オプション {#link-options}

* `hideTarget`:`false` （デフォルト） – リンクにターゲット属性を含め、`_self`、`_blank` などを許可します。
* `hideTarget`: `true` - リンクからターゲット属性全体を除外します

`unlink` アクションは、カーソルが既存のリンク内に配置されている場合にのみ表示されます。 テキストコンテンツを保持しながら、リンクの書式設定を削除します。

### 画像アクション {#image}

画像アクションは、レスポンシブな画像マークアップを生成するための画像要素のラッピングをサポートしています。 以下の節を使用できます。

```json
{
  "actions": {
    "image": {
      "wrapInPicture": false,     // Use <img> tag (default)
      "shortcut": "Mod-Shift-I",  // Custom keyboard shortcut
      "label": "Insert Image"     // Custom button label
    }
  }
}
```

#### 画像設定オプション {#image-options}

* `wrapInPicture`: `false` （デフォルト） – 単純な `<img>` 要素を生成します
* `wrapInPicture`:`true` - レスポンシブデザイン用に画像を `<picture>` 要素に含める

### その他のアクション {#other}

その他のアクションはすべて、基本のカスタマイズをサポートしています。 以下の節を使用できます。

```json
{
  "actions": {
    "h1": {
      "shortcut": "Mod-Alt-1",
      "label": "Large Heading"
    },
    "paragraph": {
      "shortcut": "Mod-Alt-0",
      "label": "Normal Text"
    },
    "link": {
      "shortcut": "Mod-K",
      "label": "Insert Link",
      "hideTarget": false    // Show target attribute options (default: false)
    }
  }
}
```

## 完全な例 {#example}

次に、完全な設定の例を示します。

```json
[
  {
    "id": "richtext",
    "rte": {
      // Configure which tools appear in toolbar
      "toolbar": {
        "format": [
          "bold",
          "italic"
        ],
        "blocks": [
          "paragraph",
          "h1",
          "h2"
        ],
        "list": [
          "bullet_list",
          "ordered_list"
        ],
        "insert": [
          "link",
          "unlink"
        ],
        "sections": [
          "format",
          "blocks",
          "list",
          "insert"
        ]
      },
      // Customize individual action behavior
      "actions": {
        // Format actions with HTML tag choices
        "bold": {
          "tag": "strong",
          "shortcut": "Mod-B",
          "label": "Bold"
        },
        "italic": {
          "tag": "em",
          "shortcut": "Mod-I"
        },
        // List actions with content wrapping
        "bullet_list": {
          "wrapInParagraphs": true,
          "label": "Bullet List"
        },
        "ordered_list": {
          "wrapInParagraphs": false
        },
        // Link actions with target control
        "link": {
          "hideTarget": false,
          "shortcut": "Mod-K",
          "label": "Add Link"
        },
        "unlink": {
          "label": "Remove Link"
        },
        // Other actions with basic customization
        "h1": {
          "shortcut": "Mod-Alt-1",
          "label": "Main Heading"
        }
      }
    },
    "components": [
      "richtext"
    ]
  }
]
```

## アクションオプションの詳細 {#action-details}

いくつかのオプションには、注意が必要な追加の詳細があります。

### `wrapInParagraphs` {#wrapInParagraphs}

リストの `wrapInParagraphs` のオプションは、HTMLの構造を制御します。

#### `wrapInParagraphs: false`（デフォルト） {#wrapInParagraphs-false}

```html
<ul>
  <li>Simple text content</li>
  <li>Another item</li>
</ul>
```

#### `wrapInParagraphs: true` {#wrapInParagraphs-true}

```html
<ul>
  <li><p>Text wrapped in paragraphs</p></li>
  <li><p>Supports rich formatting within items</p></li>
</ul>
```

必要に応じて、`wrapInParagraphs: true` を使用します。

* リスト項目内の豊富な書式
* リスト項目ごとに複数の段落
* 一貫したブロックレベルのスタイル設定

### リンクターゲットオプション {#link-target}

リンクの `hideTarget` オプションは、生成されるリンクに `target` 属性を含めるかどうか、およびリンク作成用ダイアログにターゲット選択用のフィールドを含めるかどうかを制御します。

#### `hideTarget: false`（デフォルト） {#hideTarget-false}

```html
<a href="https://example.com" target="_self">Link text</a>
<a href="https://example.com" target="_blank">External link</a>
```

### `hideTarget: true` {#hideTarget-true}

```html
<a href="https://example.com">Link text</a>
```

### タグオプション {#tag}

フォーマットアクションを使用すると、HTMLのバリアントを切り替えることができます。

| アクション | 既定のタグ | 代替タグ | ユースケース |
|---|---|---|---|
| `bold` | `<strong>` | `<b>` | 意味論的強調と視覚的強調 |
| `italic` | `<em>` | `<i>` | セマンティックとビジュアルのスタイル設定 |
| `strike` | `<del>` | `<s>` | 視覚的削除と意味的削除 |

アクセシビリティと SEO を向上させるには、セマンティックタグ（`<strong>`、`<em>`、`<del>`）を選択します。

### キーボードショートカット {#keyboard-shortcuts}

ショートカットでは、次の場合に `Mod-Key` の形式が使用されます。

* `Mod` = Macでは `Cmd`、Windows/Linux では `Ctrl`
* 例：`Mod-B`, `Mod-Shift-8`, `Mod-Alt-1`
