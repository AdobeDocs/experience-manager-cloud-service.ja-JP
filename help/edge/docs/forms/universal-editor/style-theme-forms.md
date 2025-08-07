---
title: AEM Forms の Edge Delivery Services のテーマとスタイルのカスタマイズ
description: Edge Delivery Services 経由で配信される AEM Forms のテーマとスタイルを効果的にカスタマイズし、一貫性のあるブランド化されたユーザーエクスペリエンスを実現します。
feature: Edge Delivery Services
role: Admin, Architect, Developer
exl-id: ac780399-34fe-457d-aaf4-b675656c024d
source-git-commit: 3b6d75b13730e920a10bc623947bc8b2d46dc5a9
workflow-type: tm+mt
source-wordcount: '1916'
ht-degree: 83%

---

# フォームの外観をカスタマイズ

フォームは、web サイトでのユーザーのインタラクションに不可欠で、データを入力できるようにします。カスケーディングスタイルシート（CSS）を使用すると、フォームのフィールドのスタイル設定、フォームの視覚的表現の強化、ユーザーエクスペリエンスの向上を行うことができます。

アダプティブフォームブロックを使用すると、すべてのフォームフィールドで一貫した構造を作成できます。一貫性のある構造により、フィールドタイプとフィールド名に基づいてフォームフィールドの選択とスタイル設定を行う、CSS セレクターの開発が容易になります。

このドキュメントでは、様々なフォームコンポーネントの HTML 構造の概要を説明し、アダプティブフォームブロックのフォームフィールドのスタイルを設定する、様々なフォームフィールドの CSS セレクターの作成方法を理解するのに役立ちます。

記事を最後まで読むと、次の内容を理解できます。

- アダプティブフォームブロックに含まれているデフォルトの CSS ファイルの構造を理解できます。
- 一般的なコンポーネントや、特定のコンポーネント（ドロップダウン、ラジオグループ、チェックボックスグループなど）を含め、アダプティブフォームブロックが提供するフォームコンポーネントの HTML 構造を理解できます。
- CSS セレクターを使用して、フィールドタイプとフィールド名に基づいてフォームフィールドのスタイルを設定し、要件に基づいて一貫したスタイルを設定したり、独自のスタイルを設定したりする方法を学びます。

## フォームフィールドタイプについて

スタイル設定を開始する前に、アダプティブフォームブロックでサポートされている一般的なフォームの[フィールドタイプ](/help/edge/docs/forms/universal-editor/create-custom-component.md#supported-fieldtypes)を確認します。

- 入力フィールド：テキスト入力、メール入力、パスワード入力などが含まれます。
- チェックボックスグループ：複数のオプションを選択するために使用します。
- ラジオグループ：グループから 1 つのオプションのみを選択する場合に使用します。
- ドロップダウン：選択ボックスとも呼ばれ、リストから 1 つのオプションを選択するのに使用します。
- パネル／コンテナ：関連するフォーム要素をグループ化するのに使用します。

## 基本的なスタイル設定の原則

特定のフォームフィールドのスタイルを設定する前に、[CSS の基本概念](https://www.w3schools.com/css/css_intro.asp)を理解することが重要です。

- [セレクター](https://www.w3schools.com/css/css_selectors.asp)：CSS セレクターを使用すると、特定の HTML 要素をスタイル設定の対象にできます。要素セレクター、クラスセレクターまたは ID セレクターを使用できます。
- [プロパティ](https://www.w3schools.com/css/css_syntax.asp)：CSS プロパティは、要素の外観を定義します。フォームフィールドのスタイル設定に関する一般的なプロパティには、色、背景色、境界線、パディング、余白などがあります。
- [ボックスモデル](https://www.w3schools.com/css/css_boxmodel.asp)：CSS ボックスモデルは、パディング、境界線、余白で囲まれたコンテンツ領域として、HTML 要素の構造を記述します。
- フレックスボックス／グリッド：CSS [フレックスボックス](https://www.w3schools.com/css/css3_flexbox.asp)および[グリッドレイアウト](https://www.w3schools.com/css/css_grid.asp)は、レスポンシブで柔軟なデザインを作成するのに強力なツールです。


## アダプティブフォームブロックのフォームのスタイル設定

アダプティブフォームブロックは、標準化された HTML 構造を提供し、フォームコンポーネントの選択とスタイル設定のプロセスを簡素化します。

- **デフォルトスタイルを更新**：フォームのデフォルトスタイルは、フォームの CSS ファイルを編集することで変更できます。 デフォルトのスタイルは、プロジェクトの GitHub リポジトリ（通常は `https://github.com/<your-github-username>/<your-repository>/tree/main/blocks/form/form.css`）で利用できます。 このファイルは、フォームの包括的なスタイル設定を提供し、複数ステップのウィザードフォームをサポートし、カスタマイズを容易にするために CSS カスタムプロパティの使用を強調します。

- **CSS スタイルパターン**:Edge Delivery Servicesでは、ブロックベースの CSS アーキテクチャを使用します。 次の推奨セレクターパターンを使用します。

  **プライマリパターン （推奨）:**

  ```css
  /- Block-level styling - Form container */
  .form {
      /- Styles for the entire form block */
      max-width: 600px;
      margin: 0 auto;
  }
  
  /- Form element styling */
  .form form {
      /- Styles for the actual <form> element */
      padding: 2rem;
  }
  
  /- Field wrapper styling by type */
  .form .{Type}-wrapper input {
      /- Styles for input fields */
      padding: 0.75rem;
      border: 1px solid #ccc;
  }
  ```

  **コンテキスト固有のパターン（特異性がより高い場合）:**

  ```css
  /- When you need higher specificity for main content area */
  main .form .{Type}-wrapper input {
      /- More specific targeting */
      border-color: #007cba;
  }
  ```

## コンポーネント構造

アダプティブフォームブロックは、様々なフォーム要素に対して一貫した HTML 構造を提供し、スタイルと管理を簡単にします。スタイル設定の目的で CSS を使用してコンポーネントを操作できます。

### 一般コンポーネント（ドロップダウン、ラジオグループ、チェックボックスグループを除く）：

ドロップダウン、ラジオグループ、チェックボックスグループを除くすべてのフォームフィールドには、次の HTML 構造があります。

+++ 一般コンポーネントの HTML 構造

```HTML
  <div class="{Type}-wrapper field-{Name}   field-wrapper" data-required={Required}>
     <label for="{FieldId}" class="field-label">First   Name</label>
     <input type="{Type}" placeholder="{Placeholder}"   maxlength="{Max}" id={FieldId}" name="{Name}"   aria-describedby="{FieldId}-description">
     <div class="field-description" aria-live="polite"  id="{FieldId}-description">
      Hint - First name should be minimum 3 characters  and a maximum of 10 characters.
     </div>
  </div>
```

- クラス：div 要素には、特定の要素とスタイル設定をターゲットにする、いくつかのクラスがあります。フォームフィールドをスタイル設定する CSS セレクターを開発するには、`{Type}-wrapper` または `field-{Name}` クラスが必要です。
- {Type}：フィールドタイプ別にコンポーネントを識別します。例えば、テキスト（text-wrapper）、数値（number-wrapper）、日付（date-wrapper）です。
- {Name}：名前別にコンポーネントを識別します。フィールドの名前に使用できる文字は英数字のみで、名前内の複数の連続するダッシュは 1 つのダッシュ `(-)` に置き換えられ、フィールド名の開始ダッシュと終了ダッシュは削除されます。例えば、名（field-first-name field-wrapper）です。
- {FieldId}：フィールドの一意の ID で、自動的に生成されます。
- {Required}：フィールドが必須かどうかを示すブール値です。
- ラベル：`label` 要素はフィールドの説明テキストを提供し、`for` 属性を使用して入力要素に関連付けます。
- 入力：`input` 要素は、入力するデータのタイプを定義します。例えば、テキスト、番号、メールです。
- 説明（オプション）：クラス `field-description` の `div` は、ユーザーに追加情報または手順を提供します。

**HTML 構造の例**

```HTML
<div class="text-wrapper field-first-name field-wrapper" data-required="true">
  <label for="firstName" class="field-label">First Name</label>
  <input type="text" placeholder="Enter your first name" maxlength="50" id="firstName" name="firstName" aria-describedby="firstName-description">
  <div class="field-description" aria-live="polite" id="firstName-description">
    Please enter your legal first name.
  </div>
</div>
```

+++

+++ 一般コンポーネントの CSS セレクター

```CSS
  
  /- Primary Pattern: Target field wrapper by type */
  .form .{Type}-wrapper {
    /- Add your styles here */
    margin-bottom: 1rem;
    border-radius: 4px;
  }
  
  /- Primary Pattern: Target input fields within wrapper */
  .form .{Type}-wrapper input {
    /- Add your styles here */
    border: 1px solid #ccc;
    padding: 8px;
    border-radius: 4px;
    width: 100%;
  }
  
  /- Context-specific: Target element by field name when higher specificity needed */
  .form .field-{Name} input {
    /- Add your styles here */
    /- Use this pattern for specific field customization */
  }
  
```

- `.form .{Type}-wrapper`：フィールドタイプに基づいてフィールドラッパー要素をターゲットに設定します。 例えば、`.form .text-wrapper` は、すべてのテキストフィールドコンテナをターゲットにします。
- `.form .{Type}-wrapper input`：ラッパー内の実際の入力要素をターゲットにします。 これは、フォーム入力のスタイル設定に推奨されるパターンです。
- `.form .field-{Name}`：特定のフィールド名に基づいて要素をターゲット設定します。 例えば、`.form .field-first-name` は「名」フィールドコンテナをターゲットにします。 `.form .field-{Name} input` を使用して、入力要素を具体的にターゲットに設定します。
- **回避**:`main .form form .{Type}-wrapper` – これにより、不要な CSS 特異性が生じ、管理が困難になります。

**一般コンポーネントの CSS セレクターの例**

```CSS
/- Primary Pattern: Target all text input fields */
.form .text-wrapper input {
  border: 1px solid #ccc;
  padding: 8px;
  border-radius: 4px;
  width: 100%;
}

/- Context-specific: Target field by name when higher specificity needed */
.form .field-first-name input {
  text-transform: capitalize;
  border-color: #007cba;
}

/- Alternative with main context if needed */
main .form .text-wrapper input {
  /- Use only when you need higher specificity */
  color: #333;
}
```

+++

### ドロップダウンコンポーネント

ドロップダウンメニューの場合、`input` 要素の代わりに `select` 要素を使用します。

+++ ドロップダウンコンポーネントの HTML 構造

```HTML
<div class="{Type}-wrapper field-{Name} field-wrapper" data-required={Required}>
   <label for="{FieldId}" class="field-label">First Name</label>
   <input type="{Type}" placeholder="{Placeholder}" maxlength="{Max}" id={FieldId}" name="{Name}" aria-describedby="{FieldId}-description">
   <div class="field-description" aria-live="polite" id="{FieldId}-description">
    Hint - First name should be minimum 3 characters and a maximum of 10 characters.
   </div>
</div>
```

**HTML 構造の例**

```HTML
<div class="drop-down-wrapper field-country field-wrapper" data-required="true">
  <label for="country" class="field-label">Country</label>
  <select id="country" name="country">
    <option value="">Select Country</option>
    <option value="US">United States</option>
    <option value="CA">Canada</option>
  </select>
  <div class="field-description" aria-live="polite" id="country-description">
    Please select your country of residence.
  </div>
</div>
```

+++

+++ ドロップダウンコンポーネントの CSS セレクター

次の CSS に、ドロップダウンコンポーネントの CSS セレクターの例をいくつか示します。

```CSS
/- Primary Pattern: Target the dropdown wrapper */
.form .drop-down-wrapper {
  /- Add your styles here */
  display: flex;
  flex-direction: column;
  margin-bottom: 15px;
}

/- Target the select element */
.form .drop-down-wrapper select {
  border: 1px solid #ccc;
  padding: 8px;
  border-radius: 4px;
  background-color: #fff;
}

/- Style the label */
.form .drop-down-wrapper .field-label {
  margin-bottom: 5px;
  font-weight: bold;
}
```

- ラッパーをターゲットにする：最初のセレクター（`.drop-down-wrapper`）は外側のラッパー要素をターゲットにし、スタイルがドロップダウンコンポーネント全体に適用されるようにします。
- Flexbox レイアウト：Flexbox は、ラベル、ドロップダウン、説明を垂直に配置して、すっきりとしたレイアウトを実現します。
- ラベルのスタイル設定：ラベルは太字のフォントとわずかな余白で目立ちます。
- ドロップダウンのスタイル設定：`select` 要素には、境界線、パディング、丸い角が追加され、洗練された外観が得られます。
- 背景色：視覚的な調和を図るために、一貫した背景色を設定します。
- 矢印のカスタマイズ：オプションのスタイルでは、デフォルトのドロップダウン矢印を非表示にし、Unicode 文字と位置を使用してカスタム矢印を作成します。

+++

### ラジオグループ

ドロップダウンコンポーネントと同様に、ラジオグループにも独自の HTML 構造と CSS 構造があります。

+++ ラジオグループの HTML 構造

```HTML
<fieldset class="radio-group-wrapper field-{Name} field-wrapper" id="{FieldId}" name="{Name}" data-required="{Required}">
   <legend for="{FieldId}" class="field-label">....</legend>
   <% for each radio in Group %>
   <div class="radio-wrapper field-{Name}">
      <input type="radio" value="" id="{UniqueId}" data-field-type="radio-group" name="{FieldId}">
      <label for="{UniqueId}" class="field-label">...</label>
   </div>
   <% end for %>
</fieldset>
```

**HTML 構造の例**

```HTML
<fieldset class="radio-group-wrapper field-color field-wrapper" id="color_preference" name="color_preference" data-required="true">
  <legend for="color_preference" class="field-label">Favorite Color:</legend>
  <% for each radio in Group %>
    <div class="radio-wrapper field-color">
      <input type="radio" value="red" id="color_red" data-field-type="radio-group" name="color_preference">
      <label for="color_red" class="field-label">Red</label>
    </div>
    <div class="radio-wrapper field-color">
      <input type="radio" value="green" id="color_green" data-field-type="radio-group" name="color_preference">
      <label for="color_green" class="field-label">Green</label>
    </div>
    <div class="radio-wrapper field-color">
      <input type="radio" value="blue" id="color_blue" data-field-type="radio-group" name="color_preference">
      <label for="color_blue" class="field-label">Blue</label>
    </div>
  <% end for %>
</fieldset>
```

+++

+++ ラジオグループの CSS セレクター

- フィールドセットのターゲティング

```CSS
  main .form form .radio-group-wrapper {
    border: 1px solid #ccc;
    padding: 10px;
  }
```

このセレクターは、クラス radio-group-wrapper を持つフィールドセットをターゲットにします。これは、ラジオグループ全体に一般的なスタイルを適用する場合に便利です。

- ラジオボタンラベルのターゲティング

```CSS
main .form form .radio-wrapper label {
    font-weight: normal;
    margin-right: 10px;
  }
```

- 名前に基づいて、特定のフィールドセット内のすべてのラジオボタンラベルをターゲットにする

```CSS
main .form form .field-color .radio-wrapper label {
  /- Your styles here */
}
```

+++

### チェックボックスグループ

+++ チェックボックスグループの HTML 構造

```HTML
<fieldset class="checkbox-group-wrapper field-{Name} field-wrapper" id="{FieldId}" name="{Name}" data-required="{Required}">
   <legend for="{FieldId}" class="field-label">....</legend>
   <% for each radio in Group %>
   <div class="checkbox-wrapper field-{Name}">
      <input type="checkbox" value="" id="{UniqueId}" data-field-type="checkbox-group" name="{FieldId}">
      <label for="{UniqueId}" class="field-label">...</label>
   </div>
   <% end for %>
</fieldset>
```

**HTML 構造の例**

```HTML
<fieldset class="checkbox-group-wrapper field-topping field-wrapper" id="topping_preference" name="topping_preference" data-required="false">
  <legend for="topping_preference" class="field-label">Pizza Toppings:</legend>
  <div class="checkbox-wrapper field-topping">
    <input type="checkbox" value="pepperoni" id="topping_pepperoni" data-field-type="checkbox-group" name="topping_preference">
    <label for="topping_pepperoni" class="field-label">Pepperoni</label>
  </div>
  <div class="checkbox-wrapper field-topping">
    <input type="checkbox" value="mushrooms" id="topping_mushrooms" data-field-type="checkbox-group" name="topping_preference">
    <label for="topping_mushrooms" class="field-label">Mushrooms</label>
  </div>
  <div class="checkbox-wrapper field-topping">
    <input type="checkbox" value="onions" id="topping_onions" data-field-type="checkbox-group" name="topping_preference">
    <label for="topping_onions" class="field-label">Onions</label>
  </div>
</fieldset>
```

+++

+++ チェックボックスグループの CSS セレクター

- 外側のラッパーのターゲティング：これらのセレクターは、ラジオグループとチェックボックスグループの両方の最も外側にあるコンテナをターゲットにし、グループ構造全体に一般的なスタイルを適用できます。これは、間隔、整列、その他のレイアウト関連のプロパティを設定する場合に便利です。

```CSS
  
  /- Primary Pattern: Targets radio group wrappers */
  .form .radio-group-wrapper {
    margin-bottom: 20px; /- Adds space between radio groups */  
    display: flex;
    flex-direction: column;
  }

  /- Primary Pattern: Targets checkbox group wrappers */
  .form .checkbox-group-wrapper {
    margin-bottom: 20px; /- Adds space between checkbox groups */
    display: flex;
    flex-direction: column;
  }
```

- ターゲットグループラベル：このセレクターは、ラジオとチェックボックスの両方のグループラッパー内の`.field-label` 要素をターゲットとします。これにより、これらのグループ専用のラベルのスタイルを設定でき、グループがさらに目立つようになります。

```CSS
/- Primary Pattern: Target group labels */
.form .radio-group-wrapper legend,
.form .checkbox-group-wrapper legend {
  font-weight: bold; /- Makes the group label bold */
  margin-bottom: 0.5rem;
  font-size: var(--form-font-size-base);
}
```

- 個々の入力とラベルのターゲティング：これらのセレクターは、個々のラジオボタン、チェックボックスおよび関連するラベルをより詳細に制御できます。これらを使用して、サイズ調整や間隔の調整を行ったり、より明確な視覚スタイルを適用したりできます。

```CSS
/- Primary Pattern: Styling radio buttons */
.form .radio-group-wrapper input[type="radio"] {
  margin-right: 8px; /- Adds space between the input and its label */
  margin-bottom: 4px;
}

/- Primary Pattern: Styling radio button labels */
.form .radio-group-wrapper label {
  font-size: var(--form-font-size-base); /- Changes the label font size */
  display: flex;
  align-items: center;
}

/- Primary Pattern: Styling checkboxes */
.form .checkbox-group-wrapper input[type="checkbox"] {
  margin-right: 8px; /- Adds space between the input and its label */
  margin-bottom: 4px;
}

/- Primary Pattern: Styling checkbox labels */
.form .checkbox-group-wrapper label {
  font-size: var(--form-font-size-base); /- Changes the label font size */
  display: flex;
  align-items: center;
}
```

- ラジオボタンとチェックボックスの外観のカスタマイズ：この方法では、デフォルトの入力を非表示にし、`:before` および `:after` 擬似要素を使用して、「チェック済み」状態に基づいて外観を変更するカスタムビジュアルを作成します。

```CSS
/- Hide the default radio button or checkbox */
main .form form .radio-group-wrapper input[type="radio"],
main .form form .checkbox-group-wrapper input[type="checkbox"] {
  opacity: 0;
  position: absolute;
}

/- Create a custom radio button */
main .form form .radio-group-wrapper input[type="radio"] + label::before {
  /- ... styles for custom radio button ... */
}

main .form form .radio-group-wrapper input[type="radio"]:checked + label::before {
  /- ... styles for checked radio button ... */
}

/- Create a custom checkbox */
main .form form .checkbox-group-wrapper input[type="checkbox"] + label::before {
  /- ... styles for custom checkbox ... */
}

main .form form .checkbox-group-wrapper input[type="checkbox"]:checked + label::before {
  /- ... styles for checked checkbox ... */
}
```

+++

### パネル／コンテナコンポーネント

+++ パネル／コンテナコンポーネントの HTML 構造

```HTML
<fieldset class="panel-wrapper field-{PanelName} field-wrapper">
  <legend for="{id}" class="field-label" data-visible="false">bannerComponent</legend>
  <div class="{Type}-wrapper field-{Name} field-wrapper">
    <label for="{FieldId}" class="field-label">First Name</label>
    <input type="{Type}" placeholder="{Placeholder}" maxlength="{Max}" id={FieldId}" name="{Name}">
    <div class="field-description" aria-live="polite" id="{FieldId}-description">
      Hint - First name should be minimum 3 characters and a maximum of 10 characters.
    </div>
  </div>
</fieldset>
```

**HTML 構造の例**

```HTML
<fieldset class="panel-wrapper field-login field-wrapper">
  <legend for="login" class="field-label" data-visible="false">Login Information</legend>
  <div class="text-wrapper field-username field-wrapper">
    <label for="username" class="field-label">Username</label>
    <input type="text" placeholder="Enter your username" maxlength="50" id="username" name="username">
    <div class="field-description" aria-live="polite" id="username-description">
      Please enter your username or email address.
    </div>
  </div>
  <div class="password-wrapper field-password field-wrapper">
    <label for="password" class="field-label">Password</label>
    <input type="password" placeholder="Enter your password" maxlength="20" id="password" name="password">
    <div class="field-description" aria-live="polite" id="password-description">
      Your password must be at least 8 characters long.
    </div>
  </div>
</fieldset>
```

- fieldset 要素は、パネルコンテナとして機能し、クラス panel-wrapper と、パネル名（field-login）に基づいてスタイル設定する追加クラスがあります。
- 凡例要素（`<legend>`）は、「Login Information」というテキストとクラスのフィールドラベルを含むパネルタイトルとして機能します。 data-visible=&quot;false&quot; 属性を JavaScript で使用すると、タイトルの表示／非表示を制御できます。
- フィールドセット内では、複数。{Type}-wrapper 要素（この場合は .text-wrapper と .password-wrapper）がパネル内の個々のフォームフィールドを表します。
- 各ラッパーには、前の例と同様にラベル、入力フィールド、説明が含まれています。

+++

+++ パネル／コンテナコンポーネントの CSS セレクターの例

1. パネルのターゲティング：

```CSS
  /- Target the entire panel container */
  main .form form .panel-wrapper {
    /- Add your styles here (e.g., border, padding, background color) */
    border: 1px solid #ccc;
    padding: 15px;
    border-radius: 4px;
    margin-bottom: 20px;
 }
```

- `.panel-wrapper` セレクターは、クラス panel-wrapper を使用してすべての要素のスタイルを設定し、すべてのパネルに一貫した外観を作成します。

1. パネルタイトルのターゲティング：

```CSS
  /- Target the legend element (panel title) */
  .panel-wrapper legend {
    /- Add your styles here (e.g., font-weight, font-size) */
    font-weight: bold;
    font-size: 16px;
    padding-bottom: 5px;
    margin-bottom: 10px;
    border-bottom: 1px solid #ddd; /- Optional: create a separation line */
  }
```

- `.panel-wrapper legend` セレクターは、パネル内の凡例要素のスタイルを設定し、タイトルを視覚的に目立たせます。


1. パネル内の個々のフィールドのターゲティング：　

```CSS
/- Target all form field wrappers within a panel */
main .form form .panel-wrapper .{Type}-wrapper {
  /- Add your styles here (e.g., margin) */
  margin-bottom: 10px;
}
```

- `.panel-wrapper .{Type}-wrapper` セレクターは、パネル内の `.{Type}-wrapper` クラスを使用してすべてのラッパーをターゲットにし、フォームフィールド間の間隔をスタイル設定できるようにします。

1. 特定のフィールドのターゲティング（オプション）：

```CSS
  /- Target the username field wrapper */
  main .form form .panel-wrapper .text-wrapper.field-username {
    /- Add your styles here (specific to username field) */
  }

  /- Target the password field wrapper */
  main .form form .panel-wrapper .password-wrapper.field-password {
    /- Add your styles here (specific to password field) */
  }
```

- これらのオプションのセレクターを使用すると、パネル内の特定のフィールドラッパーをターゲットにして、ユーザー名フィールドをハイライト表示するなど、独自のスタイルを設定できます。

+++

### 繰り返し可能なパネル

+++ 繰り返し可能なパネルの HTML 構造

```HTML
<fieldset class="panel-wrapper field-{PanelName} field-wrapper">
  <legend for="{id}" class="field-label" data-visible="false">bannerComponent</legend>
  <div class="{Type}-wrapper field-{Name} field-wrapper">
    <label for="{FieldId}" class="field-label">First Name</label>
    <input type="{Type}" placeholder="{Placeholder}" maxlength="{Max}" id={FieldId}" name="{Name}">
    <div class="field-description" aria-live="polite" id="{FieldId}-description">
      Hint - First name should be minimum 3 characters and a maximum of 10 characters.
    </div>
</fieldset>
```

**HTML 構造の例**

```HTML
<fieldset class="panel-wrapper field-contact field-wrapper" data-repeatable="true">
  <legend for="contact-1" class="field-label" data-visible="false">Contact Information</legend>
  <div class="text-wrapper field-name field-wrapper">
    <label for="name-1" class="field-label">Name</label>
    <input type="text" placeholder="Enter your name" maxlength="50" id="name-1" name="contacts[0].name">
    <div class="field-description" aria-live="polite" id="name-1-description">
      Please enter your full name.
    </div>
  </div>
  <div class="email-wrapper field-email field-wrapper">
    <label for="email-1" class="field-label">Email</label>
    <input type="email" placeholder="Enter your email address" maxlength="100" id="email-1" name="contacts[0].email">
    <div class="field-description" aria-live="polite" id="email-1-description">
      Please enter a valid email address.
    </div>
  </div>
</fieldset>

<fieldset class="panel-wrapper field-contact field-wrapper" data-repeatable="true">
  <legend for="contact-2" class="field-label" data-visible="false">Contact Information</legend>
  <div class="text-wrapper field-name field-wrapper">
    <label for="name-2" class="field-label">Name</label>
    <input type="text" placeholder="Enter your name" maxlength="50" id="name-2" name="contacts[1].name">
    <div class="field-description" aria-live="polite" id="name-2-description">
      Please enter your full name.
    </div>
  </div>
  <div class="email-wrapper field-email field-wrapper">
    <label for="email-2" class="field-label">Email</label>
    <input type="email" placeholder="Enter your email address" maxlength="100" id="email-2" name="contacts[1].email">
    <div class="field-description" aria-live="polite" id="email-2-description">
      Please enter a valid email address.
    </div>
  </div>
</fieldset>
```

各パネルの構造は単一パネルの例と同じですが、次の追加の属性があります。

- data-repeatable=&quot;true&quot;：この属性は、JavaScript またはフレームワークを使用して、パネルを動的に繰り返すことができることを示します。

- 一意の ID と名前：パネル内の各要素には、パネルのインデックスに基づく一意の ID（例：name-1、email-1）と name 属性（例：name=&quot;contacts[0].name&quot;）があります。これにより、複数のパネルが送信された場合に適切なデータ収集ができるようになります。

+++

+++ 繰り返し可能なパネルの CSS セレクター

- すべての繰り返し可能なパネルのターゲティング：

```CSS
  /- Target all panels with the repeatable attribute */
 main .form form .panel-wrapper[data-repeatable="true"] {
    /- Add your styles here (e.g., border, margin) */
    border: 1px solid #ccc;
    padding: 15px;
    border-radius: 4px;
    margin-bottom: 20px;
  }
```

セレクターを使用すると、繰り返し可能なすべてのパネルのスタイルが設定され、一貫したルックアンドフィールが保証されます。


- パネル内の個々のフィールドのターゲティング：

```CSS
/- Target all form field wrappers within a repeatable panel */
main .form form .panel-wrapper[data-repeatable="true"] .{Type}-wrapper {
  /- Add your styles here (e.g., margin) */
  margin-bottom: 10px;
}
```

このセレクターを使用すると、繰り返し可能なパネル内のすべてのフィールドラッパーのスタイルが設定され、フィールド間の一貫した間隔が維持されます。

- （パネル内の）特定のフィールドのターゲティング：

```CSS
/- Target the name field wrapper within the first panel */
main .form form .panel-wrapper[data-repeatable="true"][data-index="0"] .text-wrapper.field-name {
  /- Add your styles here (specific to first name field) */
}

/- Target all
```

+++

### ファイル添付

+++ 添付ファイルの HTML 構造

```HTML
<div class="file-wrapper field-{FileName} field-wrapper">
  <legend for="{id}" class="field-label" data-visible="false"> File Attachment </legend>
  <div class="file-drag-area">
    <div class="file-dragIcon"></div>
    <div class="file-dragText">Drag and Drop To Upload</div>
    <button class="file-attachButton" type="button">Attach</button>
    <input type="file" accept="audio/*, video/*, image/*, text/*, application/pdf" id="{id}" name="{FileName}" autocomplete="off" multiple="" required="required">
  </div>
  <div class="files-list">
    <div data-index="0" class="file-description">
      <span class="file-description-name">ClaimForm.pdf</span>
      <span class="file-description-size">26 kb</span>
      <button class="file-description-remove" type="button"></button>
    </div>
  </div>
</div>
```

**HTML 構造の例**


```HTML
<div class="file-wrapper field-claim_form field-wrapper">
  <legend for="claim_form" class="field-label" data-visible="false">File Attachment</legend>
  <div class="file-drag-area">
    <div class="file-dragIcon"></div>
    <div class="file-dragText">Drag and Drop To Upload</div>
    <button class="file-attachButton" type="button">Attach</button>
  </div>
  <input type="file" accept="audio/*, video/*, image/*, text/*, application/pdf" id="claim_form"
         name="claim_form" autocomplete="off" multiple="" required="required" data-max-file-size="2MB">
  <div class="files-list">
    </div>
</div>
```

- class 属性は、添付ファイル（claim_form）の指定された名前を使用します。
- 入力要素の id 属性と name 属性は、添付ファイル名（claim_form）に一致します。
- files-list セクションは、最初は空です。ファイルのアップロード時に JavaScript を使用して動的に設定されます。

+++

+++ 添付ファイルコンポーネントの CSS セレクター

- 添付ファイルコンポーネント全体のターゲティング：

```CSS
/- Target the entire file attachment component */
main .form form .file-wrapper {
  /- Add your styles here (e.g., border, padding) */
  border: 1px solid #ccc;
  padding: 15px;
  border-radius: 4px;
  margin-bottom: 20px;
}
```

このセレクターでは、凡例、ドラッグ領域、入力フィールド、リストを含む添付ファイルコンポーネント全体をスタイル設定します。

- 特定の要素のターゲティング：

```CSS
/- Target the drag and drop area */
main .form form .file-wrapper .file-drag-area {
  /- Add your styles here (e.g., background color, border) */
  background-color: #f0f0f0;
  border: 1px dashed #ddd;
  padding: 10px;
  text-align: center;
}

/- Target the file input element */
main .form form .file-wrapper input[type="file"] {
  /- Add your styles here (e.g., hide the default input) */
  display: none;
}

/- Target individual file descriptions within the list (populated dynamically) */
main .form form .file-wrapper .files-list .file-description {
  /- Add your styles here (e.g., margin, display) */
  display: flex;
  justify-content: space-between;
  margin-bottom: 5px;
}

/- Target the file name within the description */
main .form form .file-wrapper .files-list .file-description .file-description-name {
  /- Add your styles here (e.g., font-weight) */
  font-weight: bold;
}
```

これらのセレクターでは、添付ファイルコンポーネントの様々な部分を個別にスタイル設定できます。スタイルは、デザインの好みに合わせて調整できます。

+++


## コンポーネントのスタイル設定

フォームフィールドは、特定のタイプ（`{Type}-wrapper`）または個人名（`field-{Name}`）に基づいてスタイル設定できます。これにより、フォームの外観をより詳細に制御およびカスタマイズできます。

### フィールドタイプに基づくスタイル設定

CSS セレクターを使用すると、特定のフィールドタイプをターゲットにし、スタイルを一貫して適用できます。

+++ HTML 構造

```HTML
<div class="{Type}-wrapper field-{Name} field-wrapper" data-required={Required}>
   <label for="{FieldId}" class="field-label">First Name</label>
   <input type="{Type}" placeholder="{Placeholder}" maxlength="{Max}" id={FieldId}" name="{Name}" aria-describedby="{FieldId}-description">
   <div class="field-description" aria-live="polite" id="{FieldId}-description">
    Hint - First name should be minimum 3 characters and a maximum of 10 characters.
   </div>
</div>
```

**HTML 構造の例**

```HTML
<div class="text-wrapper field-name field-wrapper" data-required="true">
  <label for="name" class="field-label">Name</label>
  <input type="text" placeholder="Enter your name" maxlength="50" id="name" name="name">
</div>

<div class="number-wrapper field-age field-wrapper" data-required="true">
  <label for="age" class="field-label">Age</label>
  <input type="number" placeholder="Enter your age" id="age" name="age">
</div>

<div class="email-wrapper field-email field-wrapper" data-required="true">
  <label for="email" class="field-label">Email Address</label>
  <input type="email" placeholder="Enter your email" id="email" name="email">
</div>
```

- 各フィールドは、いくつかのクラスを持つ `div` 要素でラップされます。
   - `{Type}-wrapper`：フィールドのタイプを識別します。例：`form-text-wrapper`、`form-number-wrapper`、`form-email-wrapper`。
   - `field-{Name}`：フィールドを名前で識別します。例：`form-name`、`form-age`、`form-email`。
   - `field-wrapper`：すべてのフィールドラッパーの汎用クラス。
- `data-required` 属性は、フィールドが必須かオプションかを示します。
- 各フィールドには、対応するラベル、入力要素、プレースホルダーや説明などの潜在的な追加要素があります。


+++


+++ CSS セレクターの例

```CSS
/- Primary Pattern: Target all text input fields */
.form .text-wrapper input {
  /- Add your styles here */
  width: 100%;
  padding: var(--form-input-padding);
}

/- Primary Pattern: Target all number input fields */
.form .number-wrapper input {
  /- Add your styles here */
  letter-spacing: 2px; /- Example for adding letter spacing to all number fields */
  text-align: center;
}
```

+++

### フィールド名に基づくスタイル設定

また、個々のフィールドを名前でターゲットにして、一意のスタイルを適用することもできます。

+++ HTML 構造

```HTML
<div class="{Type}-wrapper field-{Name} field-wrapper" data-required={Required}>
   <label for="{FieldId}" class="field-label">First Name</label>
   <input type="{Type}" placeholder="{Placeholder}" maxlength="{Max}" id="{FieldId}" name="{Name}" aria-describedby="{FieldId}-description">
   <div class="field-description" aria-live="polite" id="{FieldId}-description">
    Hint - Enter the 6 digit number sent to your mobile number.
   </div>
</div>
```

**HTML 構造の例**

```HTML
<div class="number-wrapper field-otp field-wrapper" data-required="true">
  <label for="otp" class="field-label">OTP</label>
  <input type="number" placeholder="Enter your OTP" maxlength="6" id="otp" name="otp" aria-describedby="otp-description">
  <div class="field-description" aria-live="polite" id="otp-description">
    Hint - Enter the 6 digit number sent to your mobile number.
   </div>
</div>
```

+++

+++ CSS セレクターの例

```CSS
/- Primary Pattern: Target specific field by name */
.form .field-otp input {
   letter-spacing: 2px;
   text-align: center;
   font-family: monospace;
}

/- Context-specific: Use higher specificity when needed */
main .form .field-otp input {
   /- Use only when you need to override other styles */
   font-weight: bold;
}
```

この CSS は、クラス `field-otp` を持つ要素内にあるすべての入力要素をターゲットとします。Edge Delivery Servicesのフォーム構造は、「アダプティブFormsのブロック規則」に従います。この規則では、名前が「otp」のフィールドの「field-otp」のように、コンテナはフィールド固有のクラスでマークされます。

+++

## CSS ファイル構造と参照

### **既定のスタイルの場所**

デフォルトのフォームスタイルは次の場所にあります。

```
https://github.com/adobe-rnd/aem-boilerplate-forms/blob/main/blocks/form/form.css
```

### **ローカルプロジェクト構造**

Edge Delivery Services プロジェクトで：

```
/blocks/form/form.css          // Main form block styles
/styles/styles.css             // Global site styles
/styles/lazy-styles.css        // Additional component styles
```

### **カスタム CSS 統合**

1. **プロジェクトレベルのカスタマイズ**:`/styles/styles.css` にスタイルを追加する
2. **フォーム固有のカスタマイズ**：フ `/blocks/form/form.css` ームの変更
3. **コンポーネントオーバーライド**：カスタム CSS で適切な個別セレクターを使用します

## CSS の問題のトラブルシューティング

### **CSS 特異性の問題**

```css
/- ❌ Problem: Styles not applying */
.text-wrapper input {
  color: red;
}

/- ✅ Solution: Match or exceed existing specificity */
.form .text-wrapper input {
  color: red;
}

/- ✅ Alternative: Use higher specificity when needed */
main .form .text-wrapper input {
  color: red;
}
```

### **CSS 変数の上書きの問題**

```css
/- ❌ Problem: Variables not working */
.form {
  --form-border-color: blue; /- Local scope only */
}

/- ✅ Solution: Define in root scope */
:root {
  --form-border-color: blue; /- Global scope */
}
```

### **一般的なセレクターのエラー**

```css
/- ❌ Incorrect: Assumes direct nesting */
.form form input {
  /- This might miss inputs in wrappers */
}

/- ✅ Correct: Target actual structure */
.form .text-wrapper input {
  /- Targets actual HTML structure */
}

/- ❌ Avoid: Unnecessary specificity */
main .form form .text-wrapper input {
  /- Too specific, harder to override */
}

/- ✅ Preferred: Balanced specificity */
.form .text-wrapper input {
  /- Easier to maintain and override */
}
```

### **フォームステートのスタイル設定**

```css
/- Validation states */
.form .field-wrapper.error input {
  border-color: var(--form-error-color);
}

.form .field-wrapper.success input {
  border-color: var(--form-success-color);
}

/- Loading state */
.form[data-submitting="true"] {
  opacity: 0.7;
  pointer-events: none;
}

/- Disabled state */
.form input:disabled {
  background-color: var(--form-input-disabled-background);
  cursor: not-allowed;
}
```

### **コンポーネント固有のベストプラクティス**

#### **ボタンのスタイル設定**

```css
/- Primary buttons */
.form .button-wrapper button[type="submit"] {
  background-color: var(--form-focus-color);
  color: white;
  border: none;
  padding: var(--form-input-padding);
  border-radius: var(--form-border-radius);
}

/- Secondary buttons */
.form .button-wrapper button[type="reset"] {
  background-color: transparent;
  color: var(--form-text-color);
  border: 1px solid var(--form-border-color);
}
```

#### **レスポンシブフォームデザイン**

```css
/- Mobile-first approach */
.form {
  width: 100%;
  padding: 1rem;
}

/- Tablet and up */
@media (min-width: 768px) {
  .form {
    max-width: var(--form-max-width);
    padding: var(--form-padding);
  }
}
```

## ベストプラクティスのまとめ

1. **CSS カスタムプロパティの使用**：一貫したテーマ設定のために変数を活用する
2. **ブロックベースのアーキテクチャに従う**:`.form` をプライマリブロックセレクターとして使用します
3. **特定性の過剰を避ける**：必要でない限り、`main .form form` を使用しない
4. **ターゲットラッパー**：コンポーネントのターゲティングに `.{Type}-wrapper` パターンを使用します
5. **一貫性の維持**：プロジェクト全体で同じセレクターパターンを使用します
6. **デバイス間でのテスト**：モバイル、タブレット、デスクトップでフォームが適切に機能することを確認します
7. **アクセシビリティを検証**：スタイルがスクリーンリーダーやキーボードナビゲーションに干渉しないようにします


