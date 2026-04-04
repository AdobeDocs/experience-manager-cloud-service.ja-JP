---
title: アダプティブForms ブロックフィールドのプロパティの習得
description: スプレッドシートとアダプティブなFormsのブロックフィールド属性を使用して、強力なフォームをより迅速に作成できます。 このガイドでは、EDS Forms ブロックでサポートされているすべてのプロパティについて説明します。
feature: Edge Delivery Services
exl-id: e86ccc36-bda0-4e9d-8d65-ae7cb3fa79b7
source-git-commit: fa8035f826a4d08c18bc0d2b7664015c6fc82698
workflow-type: tm+mt
source-wordcount: '930'
ht-degree: 4%

---

# アダプティブ Forms ブロックフィールドのプロパティ

このドキュメントでは、フィールドが識別およびレンダリングされる方法、共通パターン、フィールド固有の違いに焦点を当てて、JSON スキーマが`blocks/form/form.js`のレンダリングされたHTMLにマッピングする方法について説明します。

## フィールド （`fieldType`）はどのように識別されますか？

JSON スキーマの各フィールドには、レンダリング方法を決定する`fieldType` プロパティがあります。 `fieldType` は次になることができます。

- **特殊タイプ**\
  例：`drop-down`、`radio-group`、`checkbox-group`、`panel`、`plain-text`、`image`、`heading`など
- **有効なHTML入力タイプ**\
  例：`text`、`number`、`email`、`date`、`password`、`tel`、`range`、`file`など
- **接尾辞`-input`を持つ型**\
  例：`text-input`、`number-input`など （`text`、`number`などの基本タイプに正規化されます）。

`fieldType`が特殊タイプと一致する場合、**カスタムレンダラー**&#x200B;が使用されます。 それ以外は、**デフォルトの入力タイプ**&#x200B;として扱われます。

各フィールドタイプの[完全なHTML構造とプロパティ ](#common-html-structure)については、以下の節を参照してください。

## フィールドで使用される一般的なプロパティ

ほとんどのフィールドで使用されるプロパティを以下に示します。

- `id`：要素IDを指定し、アクセシビリティをサポートします。
- `name`：入力、選択、またはフィールドセット要素の`name`属性を定義します。
- `label.value`、`label.richText`、`label.visible`: ラベル/凡例のテキスト、HTML コンテンツ、および表示を指定します。
- `value`: フィールドの現在の値を表します。
- `required`: `required`属性または検証データを追加します。
- `readOnly`、`enabled`: フィールドが編集可能か無効かを制御します。
- `description`: フィールドの下にヘルプテキストを表示します。
- `tooltip`：入力の`title`属性を設定します。
- `constraintMessages`: カスタム エラーメッセージをデータ属性として提供します。

## 共通のHTML構造

ほとんどのフィールドは、ラベルとオプションのヘルプテキストを含むラッパー内でレンダリングされます。 次のスニペットは、構造を示しています。

```html
<div class="<fieldType>-wrapper field-wrapper field-<name>" data-id="<id>">
<label for="<id>" class="field-label">Label</label>
<!-- Field-specific input/element here -->
<div class="field-description" id="<id>-description">Description or error
message</div>
</div>
```

グループ（ラジオ/チェックボックス）とパネルの場合は、`<fieldset>`の代わりに`<legend>`を持つ`<div>/<label>`が使用されます。 ヘルプテキスト <div> は、説明が設定されている場合にのみ存在します。

## エラーメッセージ表示

エラーメッセージは、ヘルプテキストに使用されるのと同じ`.field-description`要素に表示され、動的に更新されます。

**フィールドが無効な場合**:

- ラッパー（例：`.field-wrapper`）にクラス `.field-invalid`が割り当てられています。
- `.field-description` コンテンツは、対応するエラーメッセージに置き換えられます。

**フィールドが有効になると**:

- `.field-invalid` クラスが削除されました。
- `.field-description`は、元のヘルプテキスト（使用可能な場合）に復元されるか、存在しない場合は削除されます。

カスタムエラーメッセージは、JSONの`constraintMessages` プロパティを使用して定義できます。\
これらは、ラッパーの`data-<constraint>ErrorMessage`属性として追加されます（例：`data-requiredErrorMessage`）。

## 既定の入力タイプ （HTML入力または`*-input`）

`fieldType`が特殊な型でない場合は、標準のHTML入力型として、または`<type>-input`として扱われます（例：`text`、`number`、`email`、`date`、`text-input`、`number-input`）。

- 接尾辞`-input`が削除され、ベース型が入力の`type`属性として使用されます。
- これらの型は、`renderField()`ではデフォルトで処理されます。
一般的なデフォルトの入力タイプは、`text`、`number`、`email`、`date`、`password`、`tel`、`range`、`file`などです。  また、基本タイプに正規化された`text-input`、`number-input`などを受け入れます。

## デフォルト入力タイプの制約

制約は、JSON プロパティに基づいて、入力要素の属性として追加されます。

| JSON プロパティ | HTML属性 | 適用先 |
|--------------|---------------|------------|
| maxLength | maxlength | テキスト、電子メール、パスワード、電話 |
| minLength | minlength | テキスト、電子メール、パスワード、電話 |
| pattern | pattern | テキスト、電子メール、パスワード、電話 |
| maximum | 最大 | 数値、範囲、日付 |
| minimum | 最小値 | 数値、範囲、日付 |
| ステップ | ステップ | 数値、範囲、日付 |
| 同意 | 同意 | ファイル |
| 複数 | 複数 | ファイル |
| maxOccur | data-max | パネル |
| minOccur | data-min | パネル |

>[!NOTE]
>
> `multiple`はブール型プロパティです。 trueの場合、`multiple`属性が追加されます。

これらの属性は、フィールドのJSON定義に基づいて、フォームレンダラーによって自動的に設定されます。

## 例：制約を含むHTML構造

次の例は、検証制約とエラー処理属性を使用して数値フィールドをレンダリングする方法を示しています。

```html
<div class="number-wrapper field-wrapper field-age" data-id="age"
data-required="true"
data-minimumErrorMessage="Too small" data-maximumErrorMessage="Too large">
<label for="age" class="field-label">Age</label>
<input type="number"
id="age" name="age"
value="30" required min="18"
max="99" step="1"
placeholder="Enter your age" />
<div class="field-description" id="age-description"> Description or error message
</div>
</div>
```

HTML構造の各部分は、データのバインディング、検証、ヘルプやエラーメッセージの表示などで役割を果たします。

## フィールド固有のプロパティとHTML構造

### ドロップダウン

**追加プロパティ：**

- `enum` / `enumNames`: ドロップダウンのオプション値とその表示ラベルを定義します。
- `type`: `array`に設定されている場合、複数選択を有効にします。
- `placeholder`：無効なプレースホルダーオプションを追加して、ユーザーを選択前にガイドします。

例：

```html
<div class="drop-down-wrapper field-wrapper field-<name>" data-id="<id>"
data-required="true"
data-requiredErrorMessage="This field is required">
<label for="<id>" class="field-label">Label</label>
<select id="<id>" name="<name>" required title="Tooltip" multiple>
<option disabled selected value="">Placeholder</option>
<option value="opt1">Option 1</option>
<option value="opt2">Option 2</option>
</select>
<div class="field-description" id="<id>-description"> Description or error message
</div>
</div>
```

### プレーンテキスト

**追加プロパティ**:

- `richText`:trueの場合、HTMLは段落内でレンダリングされます。

例：

```html
<div class="plain-text-wrapper field-wrapper field-<name>" data-id="<id>">
<label for="<id>" class="field-label">Label</label>
<p>Text or <a href="..." target="_blank">link</a></p>
</div>
```

### チェックボックス

**追加プロパティ**:

- `enum`: チェックボックスのチェック済み状態とチェックされていない状態の値を定義します。
- `properties.variant / properties.alignment`: スイッチスタイルのチェックボックスの表示スタイルと整列を指定します。

例：

```html
<div class="checkbox-wrapper field-wrapper field-<name>" data-id="<id>"
data-required="true"
data-requiredErrorMessage="Please check this box">
<label for="<id>" class="field-label">Label</label>
<input type="checkbox"
id="<id>"
name="<name>" value="on"
required
data-unchecked-value="off" />
<div class="field-description" id="<id>-description"> Description or error message
</div>
</div>
```

### ボタン

**追加プロパティ**:

- `buttonType`: ボタンの種類（ボタン、送信、またはリセット）を設定して、ボタンの動作を指定します。

例：

```html
<div class="button-wrapper field-wrapper field-<name>" data-id="<id>">
<button id="<id>" name="<name>" type="submit" class="button"> Label
</button>
</div>
```

### 複数行入力

**追加プロパティ**:

- `minLength`: テキストまたはテキストエリア入力で許可される最小文字数を指定します。
- `maxLength`: テキストまたはテキストエリア入力で許可される最大文字数を指定します。
- `pattern`：入力値が有効と見なされるために一致する必要がある正規表現を定義します。
- `placeholder`：値が入力されるまで、入力領域またはテキスト領域内にプレースホルダーテキストを表示します。

例：

```html
<div class="multiline-wrapper field-wrapper field-<name>" data-id="<id>"
data-minLengthErrorMessage="Too short" data-maxLengthErrorMessage="Too long">
<label for="<id>" class="field-label">Label</label>
<textarea id="<id>"
name="<name>" required
minlength="2"
maxlength="100"
pattern="[A-Za-z]+"
placeholder="Type here..."></textarea>
<div class="field-description" id="<id>-description"> Description or error message
</div>
</div>
```

### パネル

**追加プロパティ**:

- `repeatable`: パネルを動的に繰り返すことができるかどうかを指定します。
- `minOccur`：必要なパネルインスタンスの最小数を設定します。   maxOccur：許可されるパネルインスタンスの最大数を設定します。
- `properties.variant`: パネルのビジュアルスタイルまたはバリアントを定義します。
- `properties.colspan`: パネルがグリッド レイアウトに配置される列数を指定します。
- `index`：親コンテナ内でのパネルの位置を示します。
- `fieldset`：凡例またはラベルを持つ`<fieldset>`要素の下に関連するフィールドをグループ化します。

例：

```html
<fieldset class="panel-wrapper field-wrapper field-<name>" data-id="<id>"
name="<name>"
data-repeatable="true" data-index="0">
<legend class="field-label">Label</legend>
<!-- Nested fields here -->
<button type="button" class="add">Add</button>
<button type="button" class="remove">Remove</button>
<div class="field-description" id="<id>-description"> Description or error message
</div>
</fieldset>
```

### ラジオ

**追加プロパティ**:

- `enum`：各ラジオボタンオプションの値属性として使用される、ラジオフィールドで許可される値のセットを定義します。

例：

```html
<div class="radio-wrapper field-wrapper field-<name>" data-id="<id>"
data-required="true">
<label for="<id>" class="field-label">Label</label>
<input type="radio" id="<id>" name="<name>" value="opt1" required />
<div class="field-description" id="<id>-description"> Description or error message
</div>
</div>
```

### ラジオグループ

**追加プロパティ**:

- `enum`：各ラジオボタンの値として使用される、ラジオグループのオプション値のリストを定義します。
- `enumNames`：列挙の順序に一致するラジオボタンの表示ラベルを提供します。

例：

```html
<fieldset class="radio-group-wrapper field-wrapper field-<name>" data-id="<id>"
data-required="true">
<legend class="field-label">Label</legend>
<div>
<input type="radio" id="<id>-0" name="<name>" value="opt1" required />
<label for="<id>-0">Option 1</label>
</div>
<div>
<input type="radio" id="<id>-1" name="<name>" value="opt2" />
<label for="<id>-1">Option 2</label>
</div>
<div class="field-description" id="<id>-description"> Description or error message
</div>
</fieldset>
```

### **チェックボックスグループ**

**追加プロパティ**:

- `enum`: チェックボックスグループのオプション値のリストを定義します。各チェックボックスの値として使用されます。
- `enumNames`: チェックボックスの表示ラベルを列挙の順序と一致させて提供します。
- `minItems`：有効にするために選択する必要があるチェックボックスの最小数を設定します。
- `maxItems`: エラーをトリガーする前に選択できるチェックボックスの最大数を設定します。

例：

```html
<fieldset class="checkbox-group-wrapper field-wrapper field-<name>" data-id="<id>"
data-required="true" data-minItems="1"
data-maxItems="3">
<legend class="field-label">Label</legend>
<div>
<input type="checkbox" id="<id>-0" name="<name>" value="opt1" required />
<label for="<id>-0">Option 1</label>
</div>
<div>
<input type="checkbox" id="<id>-1" name="<name>" value="opt2" />
<label for="<id>-1">Option 2</label>
</div>
<div class="field-description" id="<id>-description"> Description or error message
</div>
</fieldset>
```

### 画像

**追加プロパティ**:

- `value / properties['fd:repoPath']`：画像をレンダリングするための画像ソースパスまたはリポジトリパスを定義します。
- `altText`：アクセシビリティを向上させるために、画像（alt属性）の代替テキストを提供します。

例：

```html
<div class="image-wrapper field-wrapper field-<name>" data-id="<id>">
<picture>
<img src="..." alt="..." />
<!-- Optimized sources -->
</picture>
</div>
```

### 見出し

**追加プロパティ**:

- `value`：見出しエレメント内に表示するテキストコンテンツを指定します（例：`<h2>`）。

例：

```html
<div class="heading-wrapper field-wrapper field-<name>" data-id="<id>">
<h2 id="<id>">Heading Text</h2>
</div>
```

詳細については、`blocks/form/form.js`および`blocks/form/util.js`の実装を参照してください。


<!--
Each form field is represented as a dedicated row in the spreadsheet, analogous to fields in a database table. The column headers act as labels for the various properties supported by the form field block.

Think of your form as a table in a spreadsheet, where each line represents a different question or piece of information you want to collect. The table headings tell you what kind of answers you can expect for each section.

The below table lists all the properties that are supported by the Adaptive Forms Block.

**Master Your Forms with These Adaptive Forms Block Field Properties:**

This table details all the properties you can use to customize your Adaptive Forms Block fields:

| Property | Description | Example |
|---|---|---|
| **Type** | [HTML input type](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/input#input_types) (text, email, number, etc.), [textarea](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/textarea), [select](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/select), [fieldset](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/fieldset) | `text`, `email`, `radio`, `select` |
| **Name** | This defines the unique identifier for submitted data (e.g., 'email' for an email address field).  Choose a clear and unique name for each field, as the name serves as internal field identifier used for data mapping during submission. | `user_name`, `email_address` |
| **Label** | User-friendly field label | `"Full Name"`, `"Choose your country"` |
| **Value** | Default value displayed | `"John Doe"`, `"United States"` |
| **Placeholder** | Hint text within the field | `"Enter your email address"` |
| **Description** | Help text for users | `"Please enter a valid email address"` |
| **Visible** | Show/hide the field initially | `true`, `false` |
| **Mandatory** | Require a value from the user | `true`, `false` |
| **Min/Max** | Set minimum/maximum values (number, date, text length) | `18` (age), `2025-12-31` (date) |
| **Accept** | Allowed file types for file upload | `"image/jpeg,image/png"` |
| **Multiple** | Allow multiple file selections | `true`, `false` |
| **Options** | Comma-separated list for dropdown menus | `"Option 1, Option 2, Option 3"` |
| **Checked** | Default-selected radio button/checkbox | `true`, `false` |
| **Fieldset** | Group fields together | Fieldset name (e.g., `"Personal Information"`) |
-->
