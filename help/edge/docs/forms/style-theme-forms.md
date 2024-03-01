---
title: AEM Forms Edge Delivery Service フォームのテーマとスタイルのカスタマイズ
description: AEM Forms Edge Delivery Service フォームのテーマとスタイルのカスタマイズ
feature: Edge Delivery Services
hide: true
hidefromtoc: true
source-git-commit: e2970c7a141025222c6b119787142e7c39d453af
workflow-type: tm+mt
source-wordcount: '1271'
ht-degree: 0%

---


# フォームフィールドのスタイル設定

Formsは、Web サイトでのユーザーのインタラクションに不可欠で、データを入力できるようにします。 このガイドでは、 [アダプティブフォームブロック](/help/edge/docs/forms/create-forms.md)を使用すると、視覚的に魅力的でユーザーにわかりやすいフォームを作成できます。

## フォームフィールドタイプについて

スタイル設定を開始する前に、アダプティブフォームブロックでサポートされる一般的なフォームフィールドタイプを確認してみましょう。

* 入力フィールド：テキスト入力、E メール入力、パスワード入力などが含まれます。
* チェックボックスグループ：複数のオプションを選択するために使用します。
* ラジオグループ：グループから 1 つのオプションのみを選択する場合に使用します。
* ドロップダウン：選択ボックスとも呼ばれ、リストから 1 つのオプションを選択するために使用されます。
* パネル/コンテナ：関連するフォーム要素をグループ化するために使用します。

## 基本的なスタイル設定原則

特定のフォームフィールドをスタイル設定する前に、CSS の基本概念を理解することが重要です。

* セレクター： CSS セレクターを使用すると、特定のHTML要素をスタイル設定の対象にできます。 要素セレクター、クラスセレクターまたは ID セレクターを使用できます。
* プロパティ： CSS プロパティは、要素の外観を定義します。 フォームフィールドのスタイル設定に関する一般的なプロパティには、color、background-color、border、padding、margin などがあります。
* ボックスモデル： CSS ボックスモデルは、HTML要素の構造を、パディング、境界線、余白で囲まれたコンテンツ領域として記述します。
* フレックスボックス/グリッド： CSS フレックスボックスおよびグリッドレイアウトは、レスポンシブで柔軟なデザインを作成するための強力なツールです。

## アダプティブフォームブロックのフォームのスタイル設定

フォームブロックは、標準化されたHTML構造を提供し、フォームコンポーネントの選択とスタイル設定のプロセスを簡単にします。

* **デフォルトのスタイルを更新**：フォームのデフォルトスタイルを変更するには、 `/blocks/form/form.css file`. このファイルでは、複数手順のウィザードフォームをサポートする、フォームの包括的なスタイル設定を提供します。 この例では、カスタム CSS 変数を使用することを重視しており、フォーム間でのカスタマイズ、メンテナンス、統一されたスタイル設定が容易になります。 フォームブロックをプロジェクトに追加する手順については、 [フォームの作成](/help/edge/docs/forms/create-forms.md).

* **カスタマイズ**：デフォルトの `forms.css` をベースとしてカスタマイズし、フォームコンポーネントのルックアンドフィールを変更して、視覚的に魅力的でユーザーにわかりやすくします。 このファイルの構造は、Web サイト全体で一貫したデザインを推進し、フォームのスタイルを編成および維持することを推奨します。

## forms.css の構造の分類

* **グローバル変数：** 次の場所で定義： `:root` レベル、これらの変数 (`--variable-name`) は、スタイルシート全体で一貫性を保ち、更新を容易にするために使用される値を保存します。 これらの変数は、色、フォントサイズ、パディングおよびその他のプロパティを定義します。 独自のグローバル変数を宣言したり、既存の変数を変更してフォームのスタイルを変更したりできます。

* **ユニバーサルセレクタースタイル：** The `*` セレクターは、フォーム内のすべての要素に一致し、スタイルがデフォルトですべてのコンポーネントに適用されます。これには、 `box-sizing` プロパティを `border-box`.

* **フォームのスタイル設定：** ここでは、セレクターを使用して特定のHTML要素をターゲットにするフォームコンポーネントのスタイル設定に焦点を当てます。 入力フィールド、テキスト領域、チェックボックス、ラジオボタン、ファイル入力、フォームラベル、説明のスタイルを定義します。

* **ウィザードのスタイル設定（該当する場合）:** この節では、ウィザードのレイアウトのスタイル設定について説明します。複数の手順を含むフォームで、各手順が 1 つずつ表示されます。 ウィザードコンテナ、フィールドセット、凡例、ナビゲーションボタン、レスポンシブレイアウトのスタイルを定義します。

* **メディアクエリ：** これらは、異なる画面サイズのスタイルを提供し、それに応じてレイアウトとスタイルを調整します。

* **その他のスタイル：**：この節では、成功またはエラーメッセージ、ファイルのアップロード領域、およびフォームで発生する可能性のあるその他の要素のスタイルについて説明します。


## コンポーネントの構造

フォームブロックは、様々なフォーム要素に対して一貫したHTML構造を提供し、スタイル設定と管理を容易にします。 CSS を使用して、スタイル設定の目的でコンポーネントを操作できます。

### 一般的なコンポーネント（ドロップダウン、ラジオグループ、チェックボックスグループを除く）:

ドロップダウン、ラジオグループ、チェックボックスグループを除くすべてのフォームフィールドは、次のHTML構造を持ちます。

#### HTML構造

```HTML
<div class="form-{Type}-wrapper form-{Name} field-wrapper" data-required={Required}>
  <label for="{FieldId}" class="field-label">Field Label</label>
  <input type="{Type}" placeholder="{Placeholder}" maxlength="{Max}" id="{FieldId}" name="{Name}" aria-describedby="{FieldId}-description">
  <div class="field-description" aria-live="polite" id="{FieldId}-description">
    Hint - Description of the field.
  </div>
</div>
```

* クラス： div 要素には、特定の要素とスタイル設定をターゲットにするためのクラスが複数あります。 次が必要です： `form-{Type}-wrapper` または `form-{Name}` CSS セレクターを開発してフォームフィールドのスタイルを設定するためのクラス：
   * {Type}：コンポーネントをフィールドタイプで識別します。 例えば、text(form-text-wrapper)、number(form-number-wrapper)、date(form-date-wrapper) です。
   * {Name}：コンポーネントを名前で識別します。 フィールド名に使用できる文字は英数字のみで、名前の連続するダッシュは 1 つのダッシュに置き換えられます `(-)`フィールド名の先頭と末尾のダッシュは削除されます。 例えば、名 (form-first-name field-wrapper) です。
   * {FieldId}：自動的に生成される、フィールドの一意の識別子です。
   * {Required}：フィールドが必須かどうかを示すブール値です。
* ラベル： `label` 要素は、フィールドの説明テキストを提供し、 `for` 属性。
* 入力： `input` element は、入力するデータのタイプを定義します。 例：テキスト、数値、電子メール。
* 説明（オプション）: `div` クラスで `field-description` には、ユーザーに関する追加情報や手順が記載されています。

**HTML構造の例**

```HTML
<div class="form-text-wrapper form-first-name field-wrapper" data-required="true">
  <label for="firstName" class="field-label">First Name</label>
  <input type="text" placeholder="Enter your first name" maxlength="50" id="firstName" name="firstName" aria-describedby="firstName-description">
  <div class="field-description" aria-live="polite" id="firstName-description">
    Please enter your legal first name.
  </div>
</div>
```

**一般的なコンポーネントの CSS セレクター**

```CSS
.form-{Type}-wrapper input {
  /* Add your styles here */
  border: 1px solid #ccc;
  padding: 8px;
  border-radius: 4px;
}


.form-{Name} input {
  /* Add your styles here */
  border: 1px solid #ccc;
  padding: 8px;
  border-radius: 4px;
}
```

* `.form-{Type}-wrapper`：外側の `div` 要素を選択します。 例： `.form-text-wrapper` は、すべてのテキスト入力フィールドをターゲットにします。
* `.form-{Name}`：さらに、特定のフィールド名に基づいて要素を選択します。 例： `.form-first-name` 「名」テキストフィールドをターゲットに設定します。

**一般的なコンポーネントの CSS セレクターの例**

```CSS
/*Target all text input fields */

.form-text-wrapper input {
  border: 1px solid #ccc;
  padding: 8px;
  border-radius: 4px;
}

/*Target all fields with name first-name*/

.form-first-name input {
  border: 1px solid #ccc;
  padding: 8px;
  border-radius: 4px;
}
```


### ドロップダウンコンポーネント

ドロップダウンメニューの場合、 `select` 要素が `input` 要素：


#### HTML構造

```HTML
<div class="form-drop-down-wrapper form-{Name} field-wrapper" data-required={required}>
  <label for="{FieldId}" class="field-label">First Name</label>
  <select id="{FieldId}" name="{Name}"><option></option><option></option></select>
  <div class="field-description" aria-live="polite" id="{FieldId}-description">
    Hint - First name should be minimum 3 characters and a maximum of 10 characters.
  </div>
</div>
```

**HTML構造の例**

```HTML
    <div class="form-drop-down-wrapper form-country field-wrapper" data-required="true">
      <label for="country" class="field-label">Country</label>
      <select id="country" name="country">
         <option value="">Select Country</option>
         <option value="US">United States</option>
         <option value="CA">Canada</option>
    </select>
   <div class="field-description" aria-live="polite" id="country-description">Please select your country of residence.</div>
   </div>
```

#### ドロップダウンコンポーネントの CSS セレクターの例

```CSS
/* Target the outer wrapper */
.form-drop-down-wrapper {
  /* Add your styles here */
  display: flex;
  flex-direction: column;
  margin-bottom: 15px;
}

/* Style the label */
.form-drop-down-wrapper .field-label {
  margin-bottom: 5px;
  font-weight: bold;
}

/* Style the dropdown itself */
.form-drop-down-wrapper select {
  border: 1px solid #ccc;
  padding: 8px;
  border-radius: 4px;
  background-color: white; /* Ensure a consistent background */
  /* Adjust arrow appearance as needed */
  -webkit-appearance: none;
  -moz-appearance: none;
  appearance: none;
}

/* Optional: Style the dropdown arrow */
.form-drop-down-wrapper select::-ms-expand {
  display: none; /* Hide the default arrow for IE11 */
}

.form-drop-down-wrapper select::after {
  content: "\25BC";
  font-size: 12px;
  color: #ccc;
  /* Adjust positioning as needed */
  position: absolute;
  right: 10px;
  top: 50%;
  transform: translateY(-50%);
}
```

* ラッパーをターゲットにする：最初のセレクター (`.form-drop-down-wrapper`) は外側のラッパー要素をターゲットにし、スタイルがドロップダウンコンポーネント全体に適用されるようにします。
* フレックスボックス・レイアウト：フレックスボックスでは、クリーンなレイアウトでラベル、ドロップダウンおよび摘要を垂直に配置します。
* ラベルのスタイル設定：ラベルは、より太いフォントの太さとわずかな余白で目立ちます。
* ドロップダウンのスタイル設定：選択した要素に、研磨された外観の境界線、パディング、丸い角が付きます。
* 背景色：視覚的に調和するために、一貫した背景色が設定されます。
* 矢印のカスタマイズ：オプションのスタイルでは、デフォルトのドロップダウン矢印が非表示になり、Unicode 文字と位置を使用してカスタム矢印が作成されます。

### ラジオおよびチェックボックスグループ

ドロップダウンコンポーネントと同様に、ラジオグループとチェックボックスグループにも、独自のHTML構造と CSS に関する考慮事項があります。

#### ラジオグループHTML構造

```HTML
<div class="form-checkbox-group-wrapper form-{Name} field-wrapper" data-required={required}>
  <label class="field-label">{Label Text}</label>
  <div class="checkbox-group">
    <input type="checkbox" id="{FieldId}-1" name="{Name}" value="{Value1}">
    <label for="{FieldId}-1">{Option 1 Text}</label>
    <input type="checkbox" id="{FieldId}-2" name="{Name}" value="{Value2}">
    <label for="{FieldId}-2">{Option 2 Text}</label>
    </div>
  <div class="field-description" aria-live="polite" id="{FieldId}-description">
    Hint - Select multiple options (if applicable).
  </div>
</div>
```


#### チェックボックスグループのHTML構造

```HTML
<div class="form-checkbox-group-wrapper form-{Name} field-wrapper" data-required={required}>
  <label class="field-label">{Label Text}</label>
  <div class="checkbox-group">
    <input type="checkbox" id="{FieldId}-1" name="{Name}" value="{Value1}">
    <label for="{FieldId}-1">{Option 1 Text}</label>
    <input type="checkbox" id="{FieldId}-2" name="{Name}" value="{Value2}">
    <label for="{FieldId}-2">{Option 2 Text}</label>
    </div>
  <div class="field-description" aria-live="polite" id="{FieldId}-description">
    Hint - Select multiple options (if applicable).
  </div>
</div>
```

**ラジオおよびチェックボックスグループの CSS セレクターの例**

* 外側のラッパーのターゲティング：これらのセレクターは、ラジオグループとチェックボックスグループの両方の最も外側にあるコンテナをターゲットにし、グループ構造全体に一般的なスタイルを適用できます。 これは、間隔、整列、またはその他のレイアウト関連のプロパティを設定する場合に便利です。


  ```CSS
     /* Targets all radio group wrappers */
  .form-radio-group-wrapper {
    margin-bottom: 20px; /* Adds space between radio groups */
  }
  
  /* Targets all checkbox group wrappers */
  .form-checkbox-group-wrapper {
    margin-bottom: 20px; /* Adds space between checkbox groups */
  }
  ```


* ターゲットグループラベル：このセレクターは、 `.field-label` 要素をラジオとチェックボックスの両方のグループラッパーに含めます。 これにより、これらのグループ専用のラベルのスタイルを設定でき、場合によっては、ラベルがより目立つようになります。

  ```CSS
  .form-radio-group-wrapper .field-label,
  .form-checkbox-group-wrapper .field-label {
   font-weight: bold; /* Makes the group label bold */
  }
  ```



* 個々の入力およびラベルのターゲティング：これらのセレクターは、個々のラジオボタン、チェックボックスおよび関連するラベルをより詳細に制御できます。 これらを使用して、サイズ調整や間隔の調整を行ったり、より明確な表示スタイルを適用したりできます。

  ```CSS
  /* Styling radio buttons */
  .form-radio-group-wrapper input[type="radio"] {
    margin-right: 5px; /* Adds space between the input and its   label */
  } 
  
  /* Styling radio button labels */
  .form-radio-group-wrapper label {
    font-size: 15px; /* Changes the label font size */
  }
  
  /* Styling checkboxes */
  .form-checkbox-group-wrapper input[type="checkbox"] {
    margin-right: 5px;  /* Adds space between the input and its  label */ 
  }
  
  /* Styling checkbox labels */
  .form-checkbox-group-wrapper label {
    font-size: 15px; /* Changes the label font size */
  }
  ```




* ラジオボタンとチェックボックスの外観のカスタマイズ：この方法では、デフォルトの入力を非表示にし、:before と：after 疑似要素を使用して、「checked」状態に基づいて外観を変更するカスタムビジュアルを作成します。

  ```CSS
  /* Hide the default radio button or checkbox */
  .form-radio-group-wrapper input[type="radio"],
  .form-checkbox-group-wrapper input[type="checkbox"] {
    opacity: 0; 
    position: absolute; 
  }
  
  /* Create a custom radio button */
  .form-radio-group-wrapper input[type="radio"] + label::before { 
    content: "";
    display: inline-block;
    width: 16px; 
    height: 16px; 
    border: 2px solid #ccc; 
    border-radius: 50%;
    margin-right: 5px;
  }
  
  .form-radio-group-wrapper input[type="radio"]:checked +  label::before {
    background-color: #007bff; 
  }
  
  /* Create a custom checkbox */
  /* Similar styling as above, with adjustments for a square shape  */
  ```


## コンポーネントのスタイル設定

また、特定のタイプや個々の名前に基づいてフォームフィールドのスタイルを設定することもできます。 これにより、フォームの外観をより詳細に制御し、カスタマイズできます。

### フィールドタイプに基づくスタイル設定

CSS セレクターを使用して、特定のフィールドタイプをターゲットにし、スタイルの一貫性を保つことができます。

**HTML構造の例**

```HTML
<div class="form-text-wrapper form-name field-wrapper" data-required="true">
  <label for="name" class="field-label">Name</label>
  <input type="text" placeholder="Enter your name" maxlength="50" id="name" name="name">
</div>

<div class="form-number-wrapper form-age field-wrapper" data-required="true">
  <label for="age" class="field-label">Age</label>
  <input type="number" placeholder="Enter your age" id="age" name="age">
</div>

<div class="form-email-wrapper form-email field-wrapper" data-required="true">
  <label for="email" class="field-label">Email Address</label>
  <input type="email" placeholder="Enter your email" id="email" name="email">
</div>
```

* 各フィールドは、 `div` 複数のクラスを持つ要素：
   * `form-{Type}-wrapper`：フィールドのタイプを識別します。 例： `form-text-wrapper`, `form-number-wrapper`, `form-email-wrapper`.
   * `form-{Name}`：フィールドを名前で識別します。 例： `form-name`, `form-age`, `form-email`.
   * `field-wrapper`：すべてのフィールドラッパーの汎用クラス。
* The `data-required` 属性は、フィールドが必須かオプションかを示します。
* 各フィールドには、対応するラベル、入力要素、およびプレースホルダーや説明などの追加要素の可能性があります。

**CSS セレクターの例**

```CSS
/* Target all text input fields */
.form-text-wrapper input {
  /* Add your styles here */
}

/* Target all number input fields */
.form-number-wrapper input {
  /* Add your styles here */
  letter-spacing: 2px; /* Example for adding letter spacing to all number fields */
}
```

### フィールド名に基づくスタイル設定

また、個々のフィールドを名前でターゲット設定して、一意のスタイルを適用することもできます。

**HTML構造の例**

```HTML
<div class="form-number-wrapper form-otp field-wrapper" data-required="true">
  <label for="otp" class="field-label">OTP</label>
  <input type="number" placeholder="Enter your OTP" maxlength="6" id="otp" name="otp">
</div>
```

**CSS セレクターの例**

```CSS
.form-otp input {
   letter-spacing: 2px
}
```

この CSS は、クラスを持つ要素内にあるすべての入力要素をターゲットに設定します `form-otp`. フォームのHTML構造は、フォームブロックの規則に従います。これは、「form-otp」というクラスでマークされたコンテナが、「otp」という名前のフィールドを保持していることを意味します。


