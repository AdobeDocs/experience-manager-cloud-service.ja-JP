---
title: ユニバーサルエディターのRTEの設定
description: ユニバーサルエディターでのリッチテキストエディター（RTE）の設定方法について説明します。
feature: Developing
role: Admin, Developer
exl-id: 350eab0a-f5bc-49c0-8e4d-4a36a12030a1
source-git-commit: 8fcad5e212b1c64d3939065ab277e426935cb5ec
workflow-type: tm+mt
source-wordcount: '1094'
ht-degree: 1%

---


# ユニバーサルエディターのRTEの設定 {#configure-rte}

ユニバーサルエディターでのリッチテキストエディター（RTE）の設定方法について説明します。

## 概要 {#overview}

ユニバーサルエディターは、リッチテキストエディター（RTE）を配置してプロパティパネルに表示し、作成者がテキストを編集する際に書式変更を適用できるようにします。

このRTEは、[&#x200B; コンポーネントフィルターを使用して設定できます。](/help/implementing/universal-editor/filtering.md)このドキュメントでは、使用可能な設定オプションと例について説明します。

>[!NOTE]
>
>ユニバーサルエディタープロジェクトを開始すると、バックエンドがサポートするすべてのリッチテキスト機能（Edge Deliveryまたはヘッドレス実装を備えたAEM）が自動的にアクティブになり、RTEのモーダルエディターウィンドウ [で利用できます。](/help/sites-cloud/authoring/universal-editor/authoring.md#modal-editor)
>
>* 不要なオプションを無効にすることができます。
>* プロジェクトの種類と互換性のないオプションのアクティブ化はサポートされていません。

## 構成構造 {#structure}

RTE設定は、次の2つの部分で構成されています。

* [`toolbar`](#toolbar): ツールバーの設定では、UIで使用できる編集オプションとその構成方法を制御します。
* [`actions`](#actions): アクション設定を使用すると、個々の編集アクションの動作と外観をカスタマイズできます。

これらの設定は、プロパティ [を持つ](/help/implementing/universal-editor/filtering.md) コンポーネントフィルター`rte`の一部として定義できます。

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

ツールバー設定では、UIで使用できる編集オプションとその構成方法を制御します。 これらのセクションは

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
    "insert": ["link", "unlink", "image", "special_characters"],
    // Superscript/subscript
    "sr_script": ["superscript", "subscript"],
    // Editor utilities
    "editor": ["removeformat"],
    // Section ordering (optional)
    "sections": ["format", "alignment", "list"]
  }
}
```

## アクション設定 {#action}

アクション設定を使用すると、個々の編集アクションの動作と外観をカスタマイズできます。 使用可能なセクションを以下に示します。

### 共通のアクションオプション {#common-action-options}

ほとんどのアクションは、次の一般的なオプションをサポートしています。

* `shortcut?`：文字列 – アクションのデフォルトのキーボードショートカットを上書きします（存在する場合）
* `label?`：文字列 – UIのアクションに使用されるラベルを上書きします
* `hideInline?`: ブール値 – `true`の場合、インコンテクスト （インライン） RTE エディターツールバーからこのアクションを非表示にします

```json
{
  "actions": {
    "bold": {
      "label": "Bold",
      "shortcut": "Mod-B",
      "hideInline": true
    }
  }
}
```

### アクションの書式設定 {#format}

書式設定アクションを使用して書式設定を適用し、HTMLのタグ切り替えをサポートしてセマンティックバリアントを選択します。 次のセクションを使用できます。

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

### アクションのリスト {#list}

リストアクションは、HTML構造を制御するコンテンツラッピングをサポートしています。 次のセクションを使用できます。

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

### テーブルのアクション {#table-actions}

テーブルアクションは、テーブルセル内のHTML構造を制御するためのコンテンツラッピングをサポートしています。

```json
{
  "actions": {
    "table": {
      "wrapInParagraphs": false, // <td>content</td> (default)
      "shortcut": "Mod-Alt-T",   // Custom shortcut
      "label": "Insert Table"    // Custom label
    }
  }
}
```

#### テーブル設定オプション {#table-configuration-options}

* `wrapInParagraphs`: `false` （既定値） – テーブル セルにラップされていないテキスト コンテンツが含まれています
* `wrapInParagraphs`: `true` – 表セルは段落タグでコンテンツをラップします

サンプル：

`wrapInParagraphs`の場合：`false`

```html
<!-- Single line -->
<td>Cell content</td>

<!-- Multiple paragraphs get <br> separation -->
<td>Line 1<br />Line 2</td>
```

`wrapInParagraphs`の場合：`true`

```html
<!-- Single paragraph -->
<td><p>Cell content</p></td>

<!-- Multiple paragraphs preserved -->
<td>
  <p>Line 1</p>
  <p>Line 2</p>
</td>
```

>[!NOTE]
>
>段落（`wrapInParagraphs`: `false`）をラップ解除すると、サニタイザーは複数の段落間に`<br>` タグを自動的に挿入して、視覚的な改行を保持します。 これは、主要なリッチテキストエディターでHTMLの標準と一般的な方法に従っています。

### アクションをリンク {#link}

リンクアクションは、リンク動作を管理するためのターゲット属性コントロールをサポートします。 次のセクションを使用できます。

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

* `hideTarget`: `false` （既定値） – リンクにターゲット属性を含め、`_self`、`_blank`などを許可します。
* `hideTarget`: `true` - リンクからターゲット属性を完全に除外

`unlink` アクションは、カーソルが既存のリンク内に配置されている場合にのみ表示されます。 テキストコンテンツを保持しながら、リンクの書式設定を削除します。

### 画像のアクション {#image}

画像アクションは、画像要素のラッピングをサポートして、レスポンシブ画像マークアップを生成します。 次のセクションを使用できます。

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

* `wrapInPicture`: `false` （デフォルト） – 単純な`<img>`要素を生成します
* `wrapInPicture`: `true` - レスポンシブデザイン用に`<picture>`要素で画像をラップ

### インデント設定 {#indentation}

インデントには、インデント動作の範囲を制御する機能レベルの設定に加えて、ショートカットとラベルの個々のアクション設定があります。

```json
{
  "actions": {
    // Feature-level configuration
    "indentation": {
      "scope": "all"  // Controls what content can be indented (default: "all")
    },

    // Individual action configurations
    "indent": {
      "shortcut": "Tab",           // Custom keyboard shortcut
      "label": "Increase Indent"   // Custom button label
    },
    "outdent": {
      "shortcut": "Shift-Tab",     // Custom keyboard shortcut
      "label": "Decrease Indent"   // Custom button label
    }
  }
}
```

#### インデント範囲オプション {#indentation-options}

* `scope`: `all` （デフォルト） – インデント/アウトデントはすべてのコンテンツに適用されます：
   * リスト：リスト項目のネスト/ネスト解除
   * 段落と見出し：一般的なインデントレベルの増減
* `scope`: `lists` - インデント/アウトデントはリスト項目にのみ適用されます：
   * リスト：リスト項目のネスト/ネスト解除
   * 段落と見出し：インデントなし（これらのボタンは無効）

>[!NOTE]
>
>Tab/Shift+Tab キーによるリストのネストは、一般的なインデント設定とは独立して機能します。

### 特殊文字 {#special-characters}

`special_characters`挿入アクションは、カーソル位置に特殊文字（記号、数式演算子、通貨記号、句読点、矢印など）を挿入するための文字選択ポップオーバーを開きます。

```json
{
  "toolbar": {
    "insert": ["link", "unlink", "image", "table", "special_characters"],
    "sections": ["insert"],
  },
  "actions": {
    "special_characters": {
      "label": "Special Characters"
    }
  }
}
```

44の一般的に使用される文字のデフォルトのセットが標準で含まれています。 文字リストは、次の2つの設定オプションでカスタマイズできます。

* `appendCharacters` - デフォルトセットに文字を追加
* `characters` – 既定のセットを完全に置き換えます

各文字エントリには、`character` （Unicode文字）と`title` （ツールチップ/アクセス可能な名前）があります。

#### デフォルトへの文字の追加 {#append-special-characters}

```json
{
  "actions": {
    "special_characters": {
      "appendCharacters": [
        { "character": "\u2605", "title": "Black star" },
        { "character": "\u2764", "title": "Heavy black heart" },
      ];
    }
  }
}
```

#### デフォルトの特殊文字を置換 {#replace-special-characters}

```json
{
  "actions": {
    "special_characters": {
      "characters": [
        { "character": "\u00A9", "title": "Copyright sign" },
        { "character": "\u00AE", "title": "Registered sign" },
        { "character": "\u2122", "title": "Trade mark sign" },
      ];
    }
  }
}
```

#### 両方のオプションを同時に {#both-special-character-options}

この例では、`characters`をベースとして使用し、`appendCharacters`を使用して追加の文字を追加します。

```json
{
  "actions": {
    "special_characters": {
      "characters": [
        { "character": "\u00A9", "title": "Copyright sign" },
        { "character": "\u00AE", "title": "Registered sign" }
      ],
      "appendCharacters": [
        { "character": "\u2605", "title": "Black star" }
      ]
    }
  }
}
```

### テキストとして貼り付け {#paste-as-text}

`paste_text` エディターアクションを使用すると、標準のプレーンテキストとして貼り付けワークフローが有効になります。

* **既定のショートカット：** Mod-Shift-v （macOSではCmd+Shift+V、Windows/LinuxではCtrl+Shift+V）
* **ビヘイビアー：** テキスト/プレーンからのペースト （ソースの書式設定は無視されます）
   * リストでは、改行によって新しいリスト項目が作成されます。

```json
{
  "toolbar": {
    "editor": ["removeformat", "paste_text"]
  },
  "actions": {
    "paste_text": {
      "shortcut": "Mod-Shift-v",
      "label": "Paste as Text"
    }
  }
}
```

### その他のアクション {#other}

他のすべてのアクションは、基本的なカスタマイズをサポートしています。 次のセクションを使用できます。

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
          "unlink",
          "image",
          "special_characters"
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
        // Image actions with picture wrapping
        "image": {
          "wrapInPicture": false, // Use <img> tag instead of <picture>
          "shortcut": "Mod-Shift-I",
          "label": "Insert Image",
        },
        // Special characters with custom additions
        "special_characters": {
          "label": "Special Characters",
          "appendCharacters": [{ "character": "\u2605", "title": "Black star" }],
        },
        // Other actions with basic customization
        "h1": {
          "shortcut": "Mod-Alt-1",
          "label": "Main Heading"
        }
      }
    }
  }
]
```

## アクションオプションの詳細 {#action-details}

いくつかのオプションでは、重要な詳細情報を提供しています。

### `wrapInParagraphs` {#wrapInParagraphs}

リストの`wrapInParagraphs` オプションは、HTML構造を制御します。

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

必要な場合は`wrapInParagraphs: true`を使用してください：

* リスト項目内の豊富な書式設定
* リスト項目ごとに複数の段落
* 一貫性のあるブロックレベルのスタイル設定

### `wrapInPicture`{#wrapinpicture}

画像の`wrapInPicture` オプションは、画像コンテンツ用に生成されるHTML構造を制御します。

#### wrapInPicture: false （デフォルト） {#wrapinpicture-false}

```html
<img src="image.jpg" alt="Description" />
```

#### wrapInPicture: true {#wrapinpicture-true}

```html
<picture>
  <img src="image.jpg" alt="Description" />
</picture>
```

必要な場合は`wrapInPicture: true`を使用してください：

* `<source>`要素によるレスポンシブ画像のサポート。
* アートディレクション機能：
* 将来性のある高度な画像機能。
* 一貫した画像要素の構造：

>[!NOTE]
>
>`wrapInPicture: true`が有効になっている場合、異なるメディアクエリと形式に対して追加の`<source>`要素を使用して画像を強化できるため、レスポンシブデザインに対してより柔軟に対応できます。

### ターゲットオプションのリンク {#link-target}

リンクの`hideTarget` オプションは、生成されたリンクに`target`属性を含めるか、リンク作成用のダイアログにターゲット選択用のフィールドを含めるかを制御します。

#### `hideTarget: false`（デフォルト） {#hideTarget-false}

```html
<a href="https://example.com" target="_self">Link text</a>
<a href="https://example.com" target="_blank">External link</a>
```

#### `hideTarget: true` {#hideTarget-true}

```html
<a href="https://example.com">Link text</a>
```

### 画像上のリンクの無効化 {#disableforimages}

リンクの`disableForImages` オプションは、ユーザーが画像および画像要素にリンクを作成できるかどうかを制御します。 これは、インライン `<img>`要素とブロックレベル `<picture>`要素の両方に適用されます。

#### `disableForImages: false`（デフォルト） {#disableforimages-false}

ユーザーは画像を選択し、リンクに折り返すことができます。

```html
<!-- Inline image with link -->
<a href="https://example.com">
  <img src="image.jpg" alt="Description" />
</a>

<!-- Block-level picture with link -->
<a href="https://example.com">
  <picture>
    <img src="image.jpg" alt="Description" />
  </picture>
</a>
```

#### disableForImages: true {#disableforimages-true}

画像または画像が選択されている場合、リンクボタンは無効になります。 ユーザーが作成できるのは、テキストコンテンツ上のリンクのみです。

```html
<!-- Images remain standalone without links -->
<img src="image.jpg" alt="Description" />

<picture>
  <img src="image.jpg" alt="Description" />
</picture>

<!-- Links work normally on text -->
<a href="https://example.com">Link text</a>
```

`disableForImages: true`は、次の場合に使用します。

* リンクされた画像を防ぎ、視覚的な一貫性を維持します。
* 画像をナビゲーションから分離して、コンテンツ構造を簡素化する。
* 画像のリンクを制限するコンテンツポリシーを適用できます。
* コンテンツ内のアクセシビリティの複雑さを軽減。

>[!NOTE]
>
>この設定は、画像に新しいリンクを作成する機能にのみ影響します。 コンテンツ内の画像から既存のリンクは削除されません。

### タグオプション {#tag}

書式設定アクションを使用すると、HTMLのバリエーションを切り替えることができます。

| アクション | デフォルトタグ | 代替タグ | ユースケース |
|---|---|---|---|
| `bold` | `<strong>` | `<b>` | セマンティックと視覚的強調 |
| `italic` | `<em>` | `<i>` | セマンティックとビジュアルスタイルの違い |
| `strike` | `<del>` | `<s>` | ビジュアル削除とセマンティック削除 |

アクセシビリティとSEOを向上させるために、セマンティックタグ （`<strong>`、`<em>`、`<del>`）を選択してください。

### キーボードショートカット {#keyboard-shortcuts}

ショートカットでは、次の形式`Mod-Key`を使用します。

* `Mod` = Macの`Cmd`、Windows/Linuxの`Ctrl`
* 例：`Mod-B`, `Mod-Shift-8`, `Mod-Alt-1`

## サポートされていないHTML {#unsupported-html}

デフォルトでは、未知のHTML タグは、エディターによって解析されると削除されます。 これらを保持するには、`unsupportedHtml`設定オプションを使用してオプトインします。

```javascript
const rteConfig = {
  unsupportedHtml: true, // preserve unknown HTML tags (default: false)
};
```

| 値 | 動作 |
|---|---|
| `false`（デフォルト） | 不明なHTML タグは、解析中にドロップされます。 |
| `true` | 不明なHTML タグは、サポートされていないカスタムブロックノードでラップされるため、コンテンツを安全にラウンドトリップできます。 |

有効にすると、エディターはサポートされていないノードを`rte-unsupported-block` クラスでレンダリングします。 コンシューマーアプリでは、このクラスのスタイル設定（例：境界線、パディング、背景）を指定する必要があります。 ブロック内のタグラベルは`rte-unsupported-label`を使用しており、これもカスタマイズできます。
