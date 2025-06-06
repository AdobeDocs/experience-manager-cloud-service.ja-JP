---
title: AEM Forms用Edge Delivery Servicesのテーマとスタイルのカスタマイズ
description: AEM Forms用Edge Delivery Servicesのテーマとスタイルのカスタマイズ
feature: Edge Delivery Services
exl-id: c214711c-979b-4833-9541-8e35b2aa8e09
role: Admin, Architect, Developer
source-git-commit: babddee34b486960536ce7075684bbe660b6e120
workflow-type: tm+mt
source-wordcount: '1909'
ht-degree: 72%

---


# フォームの外観をカスタマイズ

フォームは、web サイトでのユーザーのインタラクションに不可欠で、データを入力できるようにします。カスケーディングスタイルシート（CSS）を使用してフォームフィールドのスタイルを設定し、フォームの視覚的表現を強化し、ユーザーエクスペリエンスを向上させることができます。

アダプティブフォームブロックを使用すると、すべてのフォームフィールドで一貫した構造を作成できます。この一貫した構造により、CSS セレクターを開発しやすくなります。これにより、フィールドタイプとフィールド名に基づいてフォームフィールドを選択し、スタイルを設定することができます。

このドキュメントでは、様々なフォームコンポーネントのHTML構造の概要を説明し、様々なフォームフィールド用の CSS セレクターを作成してアダプティブFormsブロックのフォームフィールドのスタイルを設定する方法の理解を深めるのに役立ちます。

この記事を読み終えると、以下を達成できます。

* アダプティブFormsブロックに含まれるデフォルト CSS ファイルの構造に関する理解を深める
* 一般的なコンポーネントと、ドロップダウン、ラジオグループ、チェックボックスグループなどの特定のコンポーネントを含め、アダプティブ Forms ブロックによって提供されるフォームコンポーネントのHTML構造の理解を深めます
* CSS セレクターを使用してフィールドタイプとフィールド名に基づいてフォームフィールドのスタイルを設定し、要件に基づいて一貫性のある一意のスタイルを設定する方法を説明します


## フォームフィールドタイプについて

スタイル設定を開始する前に、アダプティブフォームブロックでサポートされている一般的なフォームの[フィールドタイプ](/help/edge/docs/forms/form-components.md)を確認します。

* 入力フィールド：これには、テキスト入力、メール入力、パスワード入力などが含まれます
* チェックボックスグループ：複数のオプションの選択に使用します
* ラジオグループ：グループから 1 つのオプションのみを選択する場合に使用します
* ドロップダウン：セレクトボックスとも呼ばれ、リストから 1 つのオプションを選択するために使用します
* パネル/コンテナ：関連するフォーム要素をグループ化するために使用します

## 基本的なスタイル設定の原則

特定のフォームフィールドのスタイルを設定する前に、[CSS の基本概念](https://www.w3schools.com/css/css_intro.asp)を理解することが重要です。

* [セレクター](https://www.w3schools.com/css/css_selectors.asp)：CSS セレクターを使用すると、特定の HTML 要素をスタイル設定の対象にできます。要素セレクター、クラスセレクター、ID セレクターのいずれかを使用できます
* [プロパティ](https://www.w3schools.com/css/css_syntax.asp)：CSS プロパティは、要素の外観を定義します。フォームフィールドのスタイル設定に共通のプロパティには、色、背景色、境界線、パディング、余白などがあります
* [ ボックスモデル ](https://www.w3schools.com/css/css_boxmodel.asp):CSS ボックスモデルは、HTML要素の構造を、パディング、境界線、余白で囲まれたコンテンツ領域として表します
* Flexbox/Grid: CSS[Flexbox](https://www.w3schools.com/css/css3_flexbox.asp) および [Grid レイアウト ](https://www.w3schools.com/css/css_grid.asp) は、レスポンシブで柔軟なデザインを作成するための強力なツールです

## アダプティブフォームブロックのフォームのスタイル設定

アダプティブフォームブロックは、標準化された HTML 構造を提供し、フォームコンポーネントの選択とスタイル設定のプロセスを簡素化します。

* **デフォルトスタイルを更新**:`/blocks/form/form.css` ファイルを編集して、フォームのデフォルトスタイルを変更できます。 このファイルでは、複数手順のウィザードフォームをサポートする、フォームの包括的なスタイル設定を提供します。この例では、カスタム CSS 変数を使用することを重視しており、フォーム間でのカスタマイズ、メンテナンス、統一されたスタイル設定が容易になります。アダプティブフォームブロックをプロジェクトに追加する手順について詳しくは、[フォームの作成](/help/edge/docs/forms/create-forms.md)を参照してください。

* **カスタマイズ**：デフォルトの `forms.css` をベースとして使用し、フォームコンポーネントのルックアンドフィールをカスタマイズして、視覚的に訴えかけ、使いやすくします。 このファイルの構造は、web サイト全体で一貫したデザインを推進し、フォームのスタイルを編成および維持することを推奨します。

## forms.css 構造の分類

* **グローバル変数：**`:root` レベルで定義されているこれらの変数（`--variable-name`）には、一貫性を保ち、更新を容易にする、スタイルシート全体で使用される値が保存されます。これらの変数は、色、フォントサイズ、パディングなどのプロパティを定義します。独自のグローバル変数を宣言することも、既存のグローバル変数を変更してフォームのスタイルを変更することもできます。

* **ユニバーサルセレクタースタイル：**`*` セレクターはフォーム内のすべての要素に一致し、`box-sizing` プロパティを `border-box` に設定するなど、スタイルがデフォルトですべてのコンポーネントに適用されます。

* **フォームのスタイル設定：**&#x200B;この節では、セレクターを使用して特定の HTML 要素をターゲットにするフォームコンポーネントのスタイル設定に焦点を当てます。入力フィールド、テキスト領域、チェックボックス、ラジオボタン、ファイル入力、フォームラベル、説明のスタイルを定義します。

* **ウィザードのスタイル設定（該当する場合）：**&#x200B;この節では、ウィザードのレイアウトのスタイル設定に特化しています。複数の手順を含むフォームで、各手順が 1 つずつ表示されます。ウィザードコンテナ、フィールドセット、凡例、ナビゲーションボタン、レスポンシブレイアウトのスタイルを定義します。

* **メディアクエリ：**&#x200B;これらは、様々な画面サイズに合わせてスタイルを提供し、それに応じてレイアウトとスタイルを調整します。

* **その他のスタイル設定：** この節では、成功またはエラーメッセージ、ファイルのアップロード領域、フォームで発生するその他の要素のスタイルについて説明します。


## コンポーネント構造

アダプティブフォームブロックは、様々なフォーム要素に対して一貫した HTML 構造を提供し、スタイルと管理を簡単にします。スタイル設定の目的で CSS を使用してコンポーネントを操作できます。

### 一般コンポーネント（ドロップダウン、ラジオグループ、チェックボックスグループを除く）：

すべてのフォームフィールド（ドロップダウン、ラジオグループ、チェックボックスグループを除く）は、次のHTML構造を持ちます。

+++ 一般コンポーネントの HTML 構造

```HTML
<div class="{Type}-wrapper field-{Name} field-wrapper" data-required={Required}>
   <label for="{FieldId}" class="field-label">First Name</label>
   <input type="{Type}" placeholder="{Placeholder}" maxlength="{Max}" id="{FieldId}" name="{Name}" aria-describedby="{FieldId}-description">
   <div class="field-description" aria-live="polite" id="{FieldId}-description">
    Hint - First name should be a minimum of 3 characters and a maximum of 10 characters.
   </div>
</div>
```

* クラス：div 要素には、特定の要素とスタイル設定をターゲットにする、いくつかのクラスがあります。フォームフィールドをスタイル設定する CSS セレクターを開発するには、`{Type}-wrapper` または `field-{Name}` クラスが必要です。
   * {Type}：フィールドタイプ別にコンポーネントを識別します。例えば、text （テキストラッパー）、number （number-wrapper）、date （date-wrapper）などです
   * {Name}：名前別にコンポーネントを識別します。フィールド名には英数字のみを使用できます。名前に含まれる複数の連続するダッシュは、単一のダッシュ `(-)` に置き換えられ、フィールド名の先頭と末尾のダッシュは削除されます。 例えば、first-name （field-first-name field-wrapper）と指定します。
   * {FieldId}：これは、自動的に生成されるフィールドの一意の ID です
   * {Required}: フィールドが必須かどうかを示すブール値です
* ラベル：`label` 要素は、フィールドの説明テキストを提供し、`for` 属性を使用して入力要素に関連付けます
* 入力：`input` 要素は、入力するデータのタイプを定義します。例：text、number、email
* 説明（オプション）: クラス `field-description` の `div` は、ユーザーに追加情報や手順を提供します

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
/* Target all input fields within any .{Type}-wrapper */
.{Type}-wrapper {
  /* Add your styles here */
  border: 1px solid #ccc;
  padding: 8px;
  border-radius: 4px;
}

/* Target all input fields within any .{Type}-wrapper */
.{Type}-wrapper input {
  /* Add your styles here */
  border: 1px solid #ccc;
  padding: 8px;
  border-radius: 4px;
}

/* Target any element with the class field-{Name} */
.field-{Name} {
  /* Add your styles here */
  /* This could be used for styles specific to all elements with field-{Name} class, not just inputs */
}
```

* `.{Type}-wrapper`：フィールドタイプに基づいて外部 `div` 要素をターゲットに設定します。 例えば、`.text-wrapper` はすべてのテキストフィールドをターゲットにします
* `.field-{Name}`：さらに、特定のフィールド名に基づいて要素を選択します。例えば、`.field-first-name` は「名」テキストフィールドをターゲットにします。このセレクターは、field-{Name} クラスを持つ要素をターゲットにするのに使用できますが、注意することが重要です。この特定のケースでは、入力自体だけでなくラベルや説明要素もターゲットにするので、入力フィールドのスタイル設定には役に立ちません。テキスト入力フィールド（.text-wrapper input）をターゲティングする場合のように、より具体的なセレクターを使用することをお勧めします

**一般コンポーネントの CSS セレクターの例**

```CSS
/* Target all text input fields */
.text-wrapper input {
  border: 1px solid #ccc;
  padding: 8px;
  border-radius: 4px;
}

/* Target all fields with name first-name */
.field-first-name input {
  border: 1px solid #ccc;
  padding: 8px;
  border-radius: 4px;
}
```

+++

### ドロップダウンコンポーネント

ドロップダウンメニューの場合、`input` 要素の代わりに `select` 要素を使用します。

+++ ドロップダウンコンポーネントの HTML 構造

```HTML
<div class="{Type}-wrapper field-{Name} field-wrapper" data-required={Required}>
   <label for="{FieldId}" class="field-label">Country</label>
   <select id="{FieldId}" name="{Name}"><option></option><option></option></select>
   <div class="field-description" aria-live="polite" id="{FieldId}-description">
    Please select your country from the list.
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

```CSS
/* Target the outer wrapper */
.drop-down-wrapper {
  /* Add your styles here */
  display: flex;
  flex-direction: column;
  margin-bottom: 15px;
}

/* Style the label */
.drop-down-wrapper .field-label {
  margin-bottom: 5px;
  font-weight: bold;
}

/* Style the dropdown itself */
.drop-down-wrapper select {
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
.drop-down-wrapper select::-ms-expand {
  display: none; /* Hide the default arrow for IE11 */
}

.drop-down-wrapper select::after {
  content: "\25BC";
}
```

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

#### HTML 構造の例

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

* フィールドセットのターゲティング

```CSS
  .radio-group-wrapper {
    border: 1px solid #ccc;
    padding: 10px;
  }
```

このセレクターは、クラス radio-group-wrapper を持つフィールドセットをターゲットにします。これは、ラジオグループ全体に一般的なスタイルを適用する場合に便利です。

* ラジオボタンラベルのターゲティング

```CSS
.radio-wrapper label {
    font-weight: normal;
    margin-right: 10px;
  }
```

* 名前に基づいて、特定のフィールドセット内のすべてのラジオボタンラベルをターゲットにする

```CSS
.field-color .radio-wrapper label {
  /* Your styles here */
}
```

+++

### チェックボックスグループ

+++ チェックボックスグループの HTML 構造

```HTML
<fieldset class="checkbox-group-wrapper field-{Name} field-wrapper" id="{FieldId}" name="{Name}" data-required="{Required}">
   <legend for="{FieldId}" class="field-label">....</legend>
   <% for each radio in Group %>
   <div class="radio-wrapper field-{Name}">
      <input type="checkbox" value="" id="{UniqueId}" data-field-type="checkbox-group" name="{FieldId}">
      <label for="{UniqueId}" class="field-label">...</label>
   </div>
   <% end for %>
</fieldset>
```

#### HTML 構造の例

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

* 外側のラッパーのターゲティング：これらのセレクターは、ラジオグループとチェックボックスグループの両方の最も外側にあるコンテナをターゲットにし、グループ構造全体に一般的なスタイルを適用できます。これは、間隔、整列、その他のレイアウト関連のプロパティを設定する場合に便利です。


  ```CSS
     /* Targets radio group wrappers */
       .radio-group-wrapper {
       margin-bottom: 20px; /* Adds space between radio groups */  
     }
  
     /* Targets checkbox group wrappers */
     .checkbox-group-wrapper {
     margin-bottom: 20px; /* Adds space between checkbox groups */
     }
  ```


* ターゲットグループラベル：このセレクターは、ラジオとチェックボックスの両方のグループラッパー内の`.field-label` 要素をターゲットとします。これにより、これらのグループ専用のラベルのスタイルを設定でき、グループがさらに目立つようになります。

  ```CSS
   .radio-group-wrapper legend,
   .checkbox-group-wrapper legend {
     font-weight: bold; /* Makes the group label bold */
   }
  ```



* 個々の入力とラベルのターゲティング：これらのセレクターは、個々のラジオボタン、チェックボックスおよび関連するラベルをより詳細に制御できます。これらを使用して、サイズ調整や間隔の調整を行ったり、より明確な視覚スタイルを適用したりできます。

  ```CSS
  /* Styling radio buttons */
   .radio-group-wrapper input[type="radio"] {
     margin-right: 5px; /* Adds space between the input and its label */
   }
  
   /* Styling radio button labels */
   .radio-group-wrapper label {
     font-size: 15px; /* Changes the label font size */
   }
  
  /* Styling checkboxes */
   .checkbox-group-wrapper input[type="checkbox"] {
     margin-right: 5px; /* Adds space between the input and its label */
   }
  
   /* Styling checkbox labels */
   .checkbox-group-wrapper label {
     font-size: 15px; /* Changes the label font size */
   }
  ```




* ラジオボタンとチェックボックスの外観のカスタマイズ：この方法では、デフォルトの入力を非表示にし、`:before` および `:after` 擬似要素を使用して、「チェック済み」状態に基づいて外観を変更するカスタムビジュアルを作成します。

  ```CSS
  /* Hide the default radio button or checkbox */
     .radio-group-wrapper input[type="radio"],
     .checkbox-group-wrapper input[type="checkbox"] {
       opacity: 0;
       position: absolute;
     }
  
     /* Create a custom radio button */
     .radio-group-wrapper input[type="radio"] + label::before {
       /* ... styles for custom radio button ... */
     }
  
     .radio-group-wrapper input[type="radio"]:checked + label::before {
       /* ... styles for checked radio button ... */
     }
  
     /* Create a custom checkbox */
     /* Similar styling as above, with adjustments for a square shape  */
     .checkbox-group-wrapper input[type="checkbox"] + label::before {
       /* ... styles for custom checkbox ... */
     }
  
     .checkbox-group-wrapper input[type="checkbox"]:checked + label::before {
       /* ... styles for checked checkbox ... */
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

* fieldset 要素は、パネルコンテナとして機能し、クラス panel-wrapper と、パネル名（field-login）に基づいてスタイル設定する追加クラスがあります。
* 凡例要素（&lt;legend>）は、「ログイン情報」というテキストとクラスフィールドラベルを持つパネルタイトルとして機能します。data-visible=&quot;false&quot; 属性を JavaScript で使用すると、タイトルの表示／非表示を制御できます。
* フィールドセット内では、複数の.{Type}-wrapper 要素（この場合は .text-wrapper と .password-wrapper）がパネル内の個々のフォームフィールドを表します。
* 各ラッパーには、前の例と同様にラベル、入力フィールド、説明が含まれています。

+++

+++ パネル／コンテナコンポーネントの CSS セレクターの例

1. パネルのターゲティング：

```CSS
  /* Target the entire panel container */
  .panel-wrapper {
    /* Add your styles here (e.g., border, padding, background color) */
    border: 1px solid #ccc;
    padding: 15px;
    border-radius: 4px;
    margin-bottom: 20px;
 }
```

* `.panel-wrapper` セレクターは、クラス panel-wrapper を使用してすべての要素のスタイルを設定し、すべてのパネルに一貫した外観を作成します。

1. パネルタイトルのターゲティング：

```CSS
  /* Target the legend element (panel title) */
  .panel-wrapper legend {
    /* Add your styles here (e.g., font-weight, font-size) */
    font-weight: bold;
    font-size: 16px;
    padding-bottom: 5px;
    margin-bottom: 10px;
    border-bottom: 1px solid #ddd; /* Optional: create a separation line */
  }
```

* `.panel-wrapper legend` セレクターは、パネル内の凡例要素のスタイルを設定し、タイトルを視覚的に目立たせます。


1. パネル内の個々のフィールドのターゲティング：　

```CSS
/* Target all form field wrappers within a panel */
.panel-wrapper .{Type}-wrapper {
  /* Add your styles here (e.g., margin) */
  margin-bottom: 10px;
}
```

* `.panel-wrapper .{Type}-wrapper` セレクターは、パネル内の `.{Type}-wrapper` クラスを使用してすべてのラッパーをターゲットにし、フォームフィールド間の間隔をスタイル設定できるようにします。

1. 特定のフィールドのターゲティング（オプション）：

```CSS
  /* Target the username field wrapper */
  .panel-wrapper .text-wrapper.field-username {
    /* Add your styles here (specific to username field) */
  }

  /* Target the password field wrapper */
  .panel-wrapper .password-wrapper.field-password {
    /* Add your styles here (specific to password field) */
  }
```

* これらのオプションのセレクターを使用すると、パネル内の特定のフィールドラッパーをターゲットにして、ユーザー名フィールドをハイライト表示するなど、独自のスタイルを設定できます。

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

* data-repeatable=&quot;true&quot;：この属性は、JavaScript またはフレームワークを使用して、パネルを動的に繰り返すことができることを示します。

* 一意の ID と名前：パネル内の各要素には、パネルのインデックスに基づく一意の ID（例：name-1、email-1）と name 属性（例：name=&quot;contacts[0].name&quot;）があります。これにより、複数のパネルが送信された場合に適切なデータ収集ができるようになります。

+++

+++ 繰り返し可能なパネルの CSS セレクター

* すべての繰り返し可能なパネルのターゲティング：

```CSS
  /* Target all panels with the repeatable attribute */
  .panel-wrapper[data-repeatable="true"] {
    /* Add your styles here (e.g., border, margin) */
    border: 1px solid #ccc;
    padding: 15px;
    border-radius: 4px;
    margin-bottom: 20px;
  }
```

セレクターを使用すると、繰り返し可能なすべてのパネルのスタイルが設定され、一貫したルックアンドフィールが保証されます。


* パネル内の個々のフィールドのターゲティング：

```CSS
/* Target all form field wrappers within a repeatable panel */
.panel-wrapper[data-repeatable="true"] .{Type}-wrapper {
  /* Add your styles here (e.g., margin) */
  margin-bottom: 10px;
}
```

このセレクターを使用すると、繰り返し可能なパネル内のすべてのフィールドラッパーのスタイルが設定され、フィールド間の一貫した間隔が維持されます。

* （パネル内の）特定のフィールドのターゲティング：

```CSS
/* Target the name field wrapper within the first panel */
.panel-wrapper[data-repeatable="true"][data-index="0"] .text-wrapper.field-name {
  /* Add your styles here (specific to first name field) */
}

/* Target all
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

* class 属性は、添付ファイル（claim_form）の指定された名前を使用します。
* 入力要素の id 属性と name 属性は、添付ファイル名（claim_form）に一致します。
* files-list セクションは、最初は空です。ファイルのアップロード時に JavaScript を使用して動的に設定されます。

+++

+++ 添付ファイルコンポーネントの CSS セレクター

* 添付ファイルコンポーネント全体のターゲティング：

```CSS
/* Target the entire file attachment component */
.file-wrapper {
  /* Add your styles here (e.g., border, padding) */
  border: 1px solid #ccc;
  padding: 15px;
  border-radius: 4px;
  margin-bottom: 20px;
}
```

このセレクターでは、凡例、ドラッグ領域、入力フィールド、リストを含む添付ファイルコンポーネント全体をスタイル設定します。

* 特定の要素のターゲティング：

```CSS
/* Target the drag and drop area */
.file-wrapper .file-drag-area {
  /* Add your styles here (e.g., background color, border) */
  background-color: #f0f0f0;
  border: 1px dashed #ddd;
  padding: 10px;
  text-align: center;
}

/* Target the file input element */
.file-wrapper input[type="file"] {
  /* Add your styles here (e.g., hide the default input) */
  display: none;
}

/* Target individual file descriptions within the list (populated dynamically) */
.file-wrapper .files-list .file-description {
  /* Add your styles here (e.g., margin, display) */
  display: flex;
  justify-content: space-between;
  margin-bottom: 5px;
}

/* Target the file name within the description */
.file-wrapper .files-list .file-description .file-description-name {
  /* Add your styles here (e.g., font-weight) */
  font-weight: bold;
}

/* Target the file size within the description */
.file-wrapper .files-list .file-description .file-description-size {
  /* Add your styles here (e.g., font-size) */
  font-size: 0.8em;
}

/* Target the remove button within the description */
.file-wrapper .files-list .file-description .file-description-remove {
  /* Add your styles here (e.g., background color, hover effect) */
  background-color: transparent;
  border: none;
  cursor: pointer;
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

* 各フィールドは、いくつかのクラスを持つ `div` 要素でラップされます。
   * `{Type}-wrapper`：フィールドのタイプを識別します。例：`form-text-wrapper`、`form-number-wrapper`、`form-email-wrapper`。
   * `field-{Name}`：フィールドを名前で識別します。例：`form-name`、`form-age`、`form-email`。
   * `field-wrapper`：すべてのフィールドラッパーの汎用クラス。
* `data-required` 属性は、フィールドが必須かオプションかを示します。
* 各フィールドには、対応するラベル、入力要素、プレースホルダーや説明などの潜在的な追加要素があります。


+++


+++ CSS セレクターの例

```CSS
/* Target all text input fields */
.text-wrapper input {
  /* Add your styles here */
}

/* Target all number input fields */
.number-wrapper input {
  /* Add your styles here */
  letter-spacing: 2px; /* Example for adding letter spacing to all number fields */
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
.field-otp input {
   letter-spacing: 2px
}
```



この CSS は、クラス `field-otp` を持つ要素内にあるすべての入力要素をターゲットとします。フォームの HTML 構造はアダプティブフォームブロックの規則に従います。つまり、クラス「field-otp」でマークされたコンテナが「otp」という名前のフィールドを保持します。

+++

## 関連トピック

{{see-more-forms-eds}}