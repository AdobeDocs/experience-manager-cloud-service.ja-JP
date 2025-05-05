---
title: AEM Forms の Edge Delivery Services のテーマとスタイルのカスタマイズ
description: Edge Delivery Services 経由で配信される AEM Forms のテーマとスタイルを効果的にカスタマイズし、一貫性のあるブランド化されたユーザーエクスペリエンスを実現します。
feature: Edge Delivery Services
role: Admin, Architect, Developer
exl-id: ac780399-34fe-457d-aaf4-b675656c024d
source-git-commit: 9127c58a72dc4942312907f9e8f0cdcc8de9aa4b
workflow-type: tm+mt
source-wordcount: '1876'
ht-degree: 98%

---

# フォームの外観をカスタマイズ

<span class="preview">この機能は、早期アクセスプログラムを通じて使用できます。アクセスをリクエストするには、GitHub 組織名とリポジトリ名を記載したメールを公式アドレスから <a href="mailto:aem-forms-ea@adobe.com">aem-forms-ea@adobe.com</a> に送信してください。 例えば、リポジトリ URL が https://github.com/adobe/abc の場合、組織名は adobe で、リポジトリ名は abc になります。</span>


フォームは、web サイトでのユーザーのインタラクションに不可欠で、データを入力できるようにします。カスケーディングスタイルシート（CSS）を使用すると、フォームのフィールドのスタイル設定、フォームの視覚的表現の強化、ユーザーエクスペリエンスの向上を行うことができます。

アダプティブフォームブロックを使用すると、すべてのフォームフィールドで一貫した構造を作成できます。一貫性のある構造により、フィールドタイプとフィールド名に基づいてフォームフィールドの選択とスタイル設定を行う、CSS セレクターの開発が容易になります。

このドキュメントでは、様々なフォームコンポーネントの HTML 構造の概要を説明し、アダプティブフォームブロックのフォームフィールドのスタイルを設定する、様々なフォームフィールドの CSS セレクターの作成方法を理解するのに役立ちます。

記事を最後まで読むと、次の内容を理解できます。

* アダプティブフォームブロックに含まれているデフォルトの CSS ファイルの構造を理解できます。
* 一般的なコンポーネントや、特定のコンポーネント（ドロップダウン、ラジオグループ、チェックボックスグループなど）を含め、アダプティブフォームブロックが提供するフォームコンポーネントの HTML 構造を理解できます。
* CSS セレクターを使用して、フィールドタイプとフィールド名に基づいてフォームフィールドのスタイルを設定し、要件に基づいて一貫したスタイルを設定したり、独自のスタイルを設定したりする方法を学びます。

## フォームフィールドタイプについて

スタイル設定を開始する前に、アダプティブフォームブロックでサポートされている一般的なフォームの[フィールドタイプ](/help/edge/docs/forms/universal-editor/create-custom-component.md#supported-fieldtypes)を確認します。

* 入力フィールド：テキスト入力、メール入力、パスワード入力などが含まれます。
* チェックボックスグループ：複数のオプションを選択するために使用します。
* ラジオグループ：グループから 1 つのオプションのみを選択する場合に使用します。
* ドロップダウン：選択ボックスとも呼ばれ、リストから 1 つのオプションを選択するのに使用します。
* パネル／コンテナ：関連するフォーム要素をグループ化するのに使用します。

## 基本的なスタイル設定の原則

特定のフォームフィールドのスタイルを設定する前に、[CSS の基本概念](https://www.w3schools.com/css/css_intro.asp)を理解することが重要です。

* [セレクター](https://www.w3schools.com/css/css_selectors.asp)：CSS セレクターを使用すると、特定の HTML 要素をスタイル設定の対象にできます。要素セレクター、クラスセレクターまたは ID セレクターを使用できます。
* [プロパティ](https://www.w3schools.com/css/css_syntax.asp)：CSS プロパティは、要素の外観を定義します。フォームフィールドのスタイル設定に関する一般的なプロパティには、色、背景色、境界線、パディング、余白などがあります。
* [ボックスモデル](https://www.w3schools.com/css/css_boxmodel.asp)：CSS ボックスモデルは、パディング、境界線、余白で囲まれたコンテンツ領域として、HTML 要素の構造を記述します。
* フレックスボックス／グリッド：CSS [フレックスボックス](https://www.w3schools.com/css/css3_flexbox.asp)および[グリッドレイアウト](https://www.w3schools.com/css/css_grid.asp)は、レスポンシブで柔軟なデザインを作成するのに強力なツールです。


## アダプティブフォームブロックのフォームのスタイル設定

アダプティブフォームブロックは、標準化された HTML 構造を提供し、フォームコンポーネントの選択とスタイル設定のプロセスを簡素化します。

* **デフォルトのスタイルを更新**：`/blocks/form/form.css file` を編集することで、フォームのデフォルトのスタイルを変更できます。このファイルでは、複数手順のウィザードフォームをサポートする、フォームの包括的なスタイル設定を提供します。この例では、カスタム CSS 変数を使用することを重視しており、フォーム間でのカスタマイズ、メンテナンス、統一されたスタイル設定が容易になります。

* **Forms の CSS スタイル設定**：スタイルが正しく適用されるようにするには、フォーム固有の CSS を`main .form form` セレクター内に含めます。これにより、スタイルがメインコンテンツ領域内のフォーム要素のみをターゲットにし、web サイトの他の部分との競合を回避できます。
例：

  ```css
    main .form form input {
        /* Add styles specific to input fields inside the form */
    }
  
    main .form form button {
        /* Add styles specific to buttons inside the form */
    }
  
    main .form form label {
        /* Add styles specific to labels inside the form */
    }
  
## コンポーネント構造

アダプティブフォームブロックは、様々なフォーム要素に対して一貫した HTML 構造を提供し、スタイルと管理を簡単にします。スタイル設定の目的で CSS を使用してコンポーネントを操作できます。

### 一般コンポーネント（ドロップダウン、ラジオグループ、チェックボックスグループを除く）：

ドロップダウン、ラジオグループ、チェックボックスグループを除くすべてのフォームフィールドには、次の HTML 構造があります。

+++ 一般コンポーネントの HTML 構造

```HTML

  <div class="{Type}-wrapper field-{Name}   field-wrapper" data-required={Required}>
     &lt;label for="{FieldId}" class="field-label">First   Name&lt;/label>
     &lt;input type="{Type}" placeholder="{Placeholder}"   maxlength="{Max}" id={FieldId}" name="{Name}"   aria-describedby="{FieldId}-description">
     <div class="field-description" aria-live="polite"  id="{FieldId}-description">
      Hint - First name should be minimum 3 characters  and a maximum of 10 characters.
     </div>
  </div>

```

* クラス：div 要素には、特定の要素とスタイル設定をターゲットにする、いくつかのクラスがあります。フォームフィールドをスタイル設定する CSS セレクターを開発するには、`{Type}-wrapper` または `field-{Name}` クラスが必要です。
* {Type}：フィールドタイプ別にコンポーネントを識別します。例えば、テキスト（text-wrapper）、数値（number-wrapper）、日付（date-wrapper）です。
* {Name}：名前別にコンポーネントを識別します。フィールドの名前に使用できる文字は英数字のみで、名前内の複数の連続するダッシュは 1 つのダッシュ `(-)` に置き換えられ、フィールド名の開始ダッシュと終了ダッシュは削除されます。例えば、名（field-first-name field-wrapper）です。
* {FieldId}：フィールドの一意の ID で、自動的に生成されます。
* {Required}：フィールドが必須かどうかを示すブール値です。
* ラベル：`label` 要素はフィールドの説明テキストを提供し、`for` 属性を使用して入力要素に関連付けます。
* 入力：`input` 要素は、入力するデータのタイプを定義します。例えば、テキスト、番号、メールです。
* 説明（オプション）：クラス `field-description` の `div` は、ユーザーに追加情報または手順を提供します。

**HTML 構造の例**

```HTML

<div class="text-wrapper field-first-name field-wrapper" data-required="true">
  &lt;label for="firstName" class="field-label">First Name&lt;/label>
  &lt;input type="text" placeholder="Enter your first name" maxlength="50" id="firstName" name="firstName" aria-describedby="firstName-description">
  <div class="field-description" aria-live="polite" id="firstName-description">
    Please enter your legal first name.
  </div>
</div>

```

+++

+++ 一般コンポーネントの CSS セレクター

```CSS

  
  /* Target all input fields within any .{Type}-wrapper  */
  main .form form .{Type}-wrapper  &lbrace;
    /* Add your styles here */
    border: 1px solid #ccc;
    padding: 8px;
    border-radius: 4px;
  &rbrace;
  
  /* Target all input fields within any .{Type}-wrapper  */
  main .form form .{Type}-wrapper input &lbrace;
    /* Add your styles here */
    border: 1px solid #ccc;
    padding: 8px;
    border-radius: 4px;
  &rbrace;
  
  /* Target any element with the class field-{Name}  */
  main .form form .field-{Name} &lbrace;
    /* Add your styles here */
    /* This could be used for styles specific to all elements with   field-{Name} class, not just inputs */
  &rbrace;
  
```
* `.{Type}-wrapper`：フィールドタイプに基づいて、外側の `div` 要素をターゲットにします。例えば、`.text-wrapper` はすべてのテキストフィールドをターゲットにします。
* `.field-{Name}`：さらに、特定のフィールド名に基づいて要素を選択します。例えば、`.field-first-name` は「名」テキストフィールドをターゲットにします。このセレクターは、field-{Name} クラスを持つ要素をターゲットにするのに使用できますが、注意することが重要です。この特定のケースでは、入力自体だけでなくラベルや説明要素もターゲットにするので、入力フィールドのスタイル設定には役に立ちません。テキスト入力フィールド（.text-wrapper input）をターゲットにするセレクターなど、より具体的なセレクターを使用することをお勧めします。

**一般コンポーネントの CSS セレクターの例**

```CSS

/*Target all text input fields */
main .form form .text-wrapper input &lbrace;
  border: 1px solid #ccc;
  padding: 8px;
  border-radius: 4px;
  color: red;
&rbrace;

/*Target all fields with name first-name*/
main .form form .field-first-name input &lbrace;
  border: 1px solid #ccc;
  padding: 8px;
  border-radius: 4px;
&rbrace;

```

+++

### ドロップダウンコンポーネント

ドロップダウンメニューの場合、`input` 要素の代わりに `select` 要素を使用します。

+++ ドロップダウンコンポーネントの HTML 構造

```HTML

<div class="{Type}-wrapper field-{Name} field-wrapper" data-required={Required}>
   &lt;label for="{FieldId}" class="field-label">First Name&lt;/label>
   &lt;input type="{Type}" placeholder="{Placeholder}" maxlength="{Max}" id={FieldId}" name="{Name}" aria-describedby="{FieldId}-description">
   <div class="field-description" aria-live="polite" id="{FieldId}-description">
    Hint - First name should be minimum 3 characters and a maximum of 10 characters.
   </div>
</div>

```

**HTML 構造の例**

```HTML

<div class="drop-down-wrapper field-country field-wrapper" data-required="true">
  &lt;label for="country" class="field-label">Country&lt;/label>
  &lt;select id="country" name="country">
    &lt;option value="">Select Country&lt;/option>
    &lt;option value="US">United States&lt;/option>
    &lt;option value="CA">Canada&lt;/option>
  &lt;/select>
  <div class="field-description" aria-live="polite" id="country-description">
    Please select your country of residence.
  </div>
</div>

```

+++

+++ ドロップダウンコンポーネントの CSS セレクター

次の CSS に、ドロップダウンコンポーネントの CSS セレクターの例をいくつか示します。

```CSS

/* Target the outer wrapper */
main .form form .drop-down-wrapper &lbrace;
  /* Add your styles here */
  display: flex;
  flex-direction: column;
  margin-bottom: 15px;
&rbrace;

/* Style the label */
main .form form .drop-down-wrapper .field-label &lbrace;
  margin-bottom: 5px;
  font-weight: bold;
&rbrace;

```
* ラッパーをターゲットにする：最初のセレクター（`.drop-down-wrapper`）は外側のラッパー要素をターゲットにし、スタイルがドロップダウンコンポーネント全体に適用されるようにします。
* Flexbox レイアウト：Flexbox は、ラベル、ドロップダウン、説明を垂直に配置して、すっきりとしたレイアウトを実現します。
* ラベルのスタイル設定：ラベルは太字のフォントとわずかな余白で目立ちます。
* ドロップダウンのスタイル設定：`select` 要素には、境界線、パディング、丸い角が追加され、洗練された外観が得られます。
* 背景色：視覚的な調和を図るために、一貫した背景色を設定します。
* 矢印のカスタマイズ：オプションのスタイルでは、デフォルトのドロップダウン矢印を非表示にし、Unicode 文字と位置を使用してカスタム矢印を作成します。

+++

---

### ラジオグループ

ドロップダウンコンポーネントと同様に、ラジオグループにも独自の HTML 構造と CSS 構造があります。

+++ ラジオグループの HTML 構造

```HTML

&lt;fieldset class="radio-group-wrapper field-{Name} field-wrapper" id="{FieldId}" name="{Name}" data-required="{Required}">
   &lt;legend for="{FieldId}" class="field-label">....&lt;/legend>
   <% for each radio in Group %>
   <div class="radio-wrapper field-{Name}">
      &lt;input type="radio" value="" id="{UniqueId}" data-field-type="radio-group" name="{FieldId}">
      &lt;label for="{UniqueId}" class="field-label">...&lt;/label>
   </div>
   <% end for %>
&lt;/fieldset>

```

**HTML 構造の例**

```HTML

&lt;fieldset class="radio-group-wrapper field-color field-wrapper" id="color_preference" name="color_preference" data-required="true">
  &lt;legend for="color_preference" class="field-label">Favorite Color:&lt;/legend>
  <% for each radio in Group %>
    <div class="radio-wrapper field-color">
      &lt;input type="radio" value="red" id="color_red" data-field-type="radio-group" name="color_preference">
      &lt;label for="color_red" class="field-label">Red&lt;/label>
    </div>
    <div class="radio-wrapper field-color">
      &lt;input type="radio" value="green" id="color_green" data-field-type="radio-group" name="color_preference">
      &lt;label for="color_green" class="field-label">Green&lt;/label>
    </div>
    <div class="radio-wrapper field-color">
      &lt;input type="radio" value="blue" id="color_blue" data-field-type="radio-group" name="color_preference">
      &lt;label for="color_blue" class="field-label">Blue&lt;/label>
    </div>
  <% end for %>
&lt;/fieldset>

```

+++

+++ ラジオグループの CSS セレクター

* フィールドセットのターゲティング

```CSS

  main .form form .radio-group-wrapper &lbrace;
    border: 1px solid #ccc;
    padding: 10px;
  &rbrace;

```
このセレクターは、クラス radio-group-wrapper を持つフィールドセットをターゲットにします。これは、ラジオグループ全体に一般的なスタイルを適用する場合に便利です。

* ラジオボタンラベルのターゲティング

```CSS

main .form form .radio-wrapper label &lbrace;
    font-weight: normal;
    margin-right: 10px;
  &rbrace;

```

* 名前に基づいて、特定のフィールドセット内のすべてのラジオボタンラベルをターゲットにする

```CSS

main .form form .field-color .radio-wrapper label &lbrace;
  /* Your styles here */
&rbrace;

```

+++

### チェックボックスグループ

+++ チェックボックスグループの HTML 構造

```HTML

&lt;fieldset class="checkbox-group-wrapper field-{Name} field-wrapper" id="{FieldId}" name="{Name}" data-required="{Required}">
   &lt;legend for="{FieldId}" class="field-label">....&lt;/legend>
   <% for each radio in Group %>
   <div class="radio-wrapper field-{Name}">
      &lt;input type="checkbox" value="" id="{UniqueId}" data-field-type="checkbox-group" name="{FieldId}">
      &lt;label for="{UniqueId}" class="field-label">...&lt;/label>
   </div>
   <% end for %>
&lt;/fieldset>

```

**HTML 構造の例**

```HTML

&lt;fieldset class="checkbox-group-wrapper field-topping field-wrapper" id="topping_preference" name="topping_preference" data-required="false">
  &lt;legend for="topping_preference" class="field-label">Pizza Toppings:&lt;/legend>
  <div class="checkbox-wrapper field-topping">
    &lt;input type="checkbox" value="pepperoni" id="topping_pepperoni" data-field-type="checkbox-group" name="topping_preference">
    &lt;label for="topping_pepperoni" class="field-label">Pepperoni&lt;/label>
  </div>
  <div class="checkbox-wrapper field-topping">
    &lt;input type="checkbox" value="mushrooms" id="topping_mushrooms" data-field-type="checkbox-group" name="topping_preference">
    &lt;label for="topping_mushrooms" class="field-label">Mushrooms&lt;/label>
  </div>
  <div class="checkbox-wrapper field-topping">
    &lt;input type="checkbox" value="onions" id="topping_onions" data-field-type="checkbox-group" name="topping_preference">
    &lt;label for="topping_onions" class="field-label">Onions&lt;/label>
  </div>
&lt;/fieldset>

```

+++

+++ チェックボックスグループの CSS セレクター

* 外側のラッパーのターゲティング：これらのセレクターは、ラジオグループとチェックボックスグループの両方の最も外側にあるコンテナをターゲットにし、グループ構造全体に一般的なスタイルを適用できます。これは、間隔、整列、その他のレイアウト関連のプロパティを設定する場合に便利です。

```CSS

  
  /* Targets radio group wrappers */
  main .form form .radio-group-wrapper &lbrace;
    margin-bottom: 20px; /* Adds space between radio groups */  
  &rbrace;

  /* Targets checkbox group wrappers */
  main .form form .checkbox-group-wrapper &lbrace;
    margin-bottom: 20px; /* Adds space between checkbox groups */
  &rbrace;

```

* ターゲットグループラベル：このセレクターは、ラジオとチェックボックスの両方のグループラッパー内の`.field-label` 要素をターゲットとします。これにより、これらのグループ専用のラベルのスタイルを設定でき、グループがさらに目立つようになります。

```CSS

main .form form .radio-group-wrapper legend,
main .form form .checkbox-group-wrapper legend &lbrace;
  font-weight: bold; /* Makes the group label bold */
&rbrace;

```

* 個々の入力とラベルのターゲティング：これらのセレクターは、個々のラジオボタン、チェックボックスおよび関連するラベルをより詳細に制御できます。これらを使用して、サイズ調整や間隔の調整を行ったり、より明確な視覚スタイルを適用したりできます。

```CSS

/* Styling radio buttons */
main .form form .radio-group-wrapper input[type="radio"] &lbrace;
  margin-right: 5px; /* Adds space between the input and its label */
&rbrace;

/* Styling radio button labels */
main .form form .radio-group-wrapper label &lbrace;
  font-size: 15px; /* Changes the label font size */
&rbrace;

/* Styling checkboxes */
main .form form .checkbox-group-wrapper input[type="checkbox"] &lbrace;
  margin-right: 5px; /* Adds space between the input and its label */
&rbrace;

/* Styling checkbox labels */
main .form form .checkbox-group-wrapper label &lbrace;
  font-size: 15px; /* Changes the label font size */
&rbrace;

```

* ラジオボタンとチェックボックスの外観のカスタマイズ：この方法では、デフォルトの入力を非表示にし、`:before` および `:after` 擬似要素を使用して、「チェック済み」状態に基づいて外観を変更するカスタムビジュアルを作成します。

```CSS

/* Hide the default radio button or checkbox */
main .form form .radio-group-wrapper input[type="radio"],
main .form form .checkbox-group-wrapper input[type="checkbox"] &lbrace;
  opacity: 0;
  position: absolute;
&rbrace;

/* Create a custom radio button */
main .form form .radio-group-wrapper input[type="radio"] + label::before &lbrace;
  /* ... styles for custom radio button ... */
&rbrace;

main .form form .radio-group-wrapper input[type="radio"]:checked + label::before &lbrace;
  /* ... styles for checked radio button ... */
&rbrace;

/* Create a custom checkbox */
main .form form .checkbox-group-wrapper input[type="checkbox"] + label::before &lbrace;
  /* ... styles for custom checkbox ... */
&rbrace;

main .form form .checkbox-group-wrapper input[type="checkbox"]:checked + label::before &lbrace;
  /* ... styles for checked checkbox ... */
&rbrace;

```

+++

### パネル／コンテナコンポーネント

+++ パネル／コンテナコンポーネントの HTML 構造

```HTML

&lt;fieldset class="panel-wrapper field-{PanelName} field-wrapper">
  &lt;legend for="{id}" class="field-label" data-visible="false">bannerComponent&lt;/legend>
  <div class="{Type}-wrapper field-{Name} field-wrapper">
    &lt;label for="{FieldId}" class="field-label">First Name&lt;/label>
    &lt;input type="{Type}" placeholder="{Placeholder}" maxlength="{Max}" id={FieldId}" name="{Name}">
    <div class="field-description" aria-live="polite" id="{FieldId}-description">
      Hint - First name should be minimum 3 characters and a maximum of 10 characters.
    </div>
  </div>
&lt;/fieldset>

```

**HTML 構造の例**

```HTML

&lt;fieldset class="panel-wrapper field-login field-wrapper">
  &lt;legend for="login" class="field-label" data-visible="false">Login Information&lt;/legend>
  <div class="text-wrapper field-username field-wrapper">
    &lt;label for="username" class="field-label">Username&lt;/label>
    &lt;input type="text" placeholder="Enter your username" maxlength="50" id="username" name="username">
    <div class="field-description" aria-live="polite" id="username-description">
      Please enter your username or email address.
    </div>
  </div>
  <div class="password-wrapper field-password field-wrapper">
    &lt;label for="password" class="field-label">Password&lt;/label>
    &lt;input type="password" placeholder="Enter your password" maxlength="20" id="password" name="password">
    <div class="field-description" aria-live="polite" id="password-description">
      Your password must be at least 8 characters long.
    </div>
  </div>
&lt;/fieldset>

```

* fieldset 要素は、パネルコンテナとして機能し、クラス panel-wrapper と、パネル名（field-login）に基づいてスタイル設定する追加クラスがあります。
* 凡例要素（<legend>）は、「ログイン情報」というテキストとクラスフィールドラベルを持つパネルタイトルとして機能します。data-visible=&quot;false&quot; 属性を JavaScript で使用すると、タイトルの表示／非表示を制御できます。
* フィールドセット内では、複数。.{Type}-wrapper 要素（この場合は .text-wrapper と .password-wrapper）がパネル内の個々のフォームフィールドを表します。
* 各ラッパーには、前の例と同様にラベル、入力フィールド、説明が含まれています。

+++

+++ パネル／コンテナコンポーネントの CSS セレクターの例

1. パネルのターゲティング：

```CSS

  /* Target the entire panel container */
  main .form form .panel-wrapper &lbrace;
    /* Add your styles here (e.g., border, padding, background color) */
    border: 1px solid #ccc;
    padding: 15px;
    border-radius: 4px;
    margin-bottom: 20px;
 &rbrace;

```

* `.panel-wrapper` セレクターは、クラス panel-wrapper を使用してすべての要素のスタイルを設定し、すべてのパネルに一貫した外観を作成します。

1. パネルタイトルのターゲティング：

```CSS

  /* Target the legend element (panel title) */
  .panel-wrapper legend &lbrace;
    /* Add your styles here (e.g., font-weight, font-size) */
    font-weight: bold;
    font-size: 16px;
    padding-bottom: 5px;
    margin-bottom: 10px;
    border-bottom: 1px solid #ddd; /* Optional: create a separation line */
  &rbrace;

```

* `.panel-wrapper legend` セレクターは、パネル内の凡例要素のスタイルを設定し、タイトルを視覚的に目立たせます。


1. パネル内の個々のフィールドのターゲティング：　

```CSS

/* Target all form field wrappers within a panel */
main .form form .panel-wrapper .{Type}-wrapper &lbrace;
  /* Add your styles here (e.g., margin) */
  margin-bottom: 10px;
&rbrace;

```

* `.panel-wrapper .{Type}-wrapper` セレクターは、パネル内の `.{Type}-wrapper` クラスを使用してすべてのラッパーをターゲットにし、フォームフィールド間の間隔をスタイル設定できるようにします。

1. 特定のフィールドのターゲティング（オプション）：

```CSS

  /* Target the username field wrapper */
  main .form form .panel-wrapper .text-wrapper.field-username &lbrace;
    /* Add your styles here (specific to username field) */
  &rbrace;

  /* Target the password field wrapper */
  main .form form .panel-wrapper .password-wrapper.field-password &lbrace;
    /* Add your styles here (specific to password field) */
  &rbrace;

```

* これらのオプションのセレクターを使用すると、パネル内の特定のフィールドラッパーをターゲットにして、ユーザー名フィールドをハイライト表示するなど、独自のスタイルを設定できます。

+++

### 繰り返し可能なパネル

+++ 繰り返し可能なパネルの HTML 構造

```HTML

&lt;fieldset class="panel-wrapper field-{PanelName} field-wrapper">
  &lt;legend for="{id}" class="field-label" data-visible="false">bannerComponent&lt;/legend>
  <div class="{Type}-wrapper field-{Name} field-wrapper">
    &lt;label for="{FieldId}" class="field-label">First Name&lt;/label>
    &lt;input type="{Type}" placeholder="{Placeholder}" maxlength="{Max}" id={FieldId}" name="{Name}">
    <div class="field-description" aria-live="polite" id="{FieldId}-description">
      Hint - First name should be minimum 3 characters and a maximum of 10 characters.
    </div>
&lt;/fieldset>

```

**HTML 構造の例**

```HTML

&lt;fieldset class="panel-wrapper field-contact field-wrapper" data-repeatable="true">
  &lt;legend for="contact-1" class="field-label" data-visible="false">Contact Information&lt;/legend>
  <div class="text-wrapper field-name field-wrapper">
    &lt;label for="name-1" class="field-label">Name&lt;/label>
    &lt;input type="text" placeholder="Enter your name" maxlength="50" id="name-1" name="contacts[0].name">
    <div class="field-description" aria-live="polite" id="name-1-description">
      Please enter your full name.
    </div>
  </div>
  <div class="email-wrapper field-email field-wrapper">
    &lt;label for="email-1" class="field-label">Email&lt;/label>
    &lt;input type="email" placeholder="Enter your email address" maxlength="100" id="email-1" name="contacts[0].email">
    <div class="field-description" aria-live="polite" id="email-1-description">
      Please enter a valid email address.
    </div>
  </div>
&lt;/fieldset>

&lt;fieldset class="panel-wrapper field-contact field-wrapper" data-repeatable="true">
  &lt;legend for="contact-2" class="field-label" data-visible="false">Contact Information&lt;/legend>
  <div class="text-wrapper field-name field-wrapper">
    &lt;label for="name-2" class="field-label">Name&lt;/label>
    &lt;input type="text" placeholder="Enter your name" maxlength="50" id="name-2" name="contacts[1].name">
    <div class="field-description" aria-live="polite" id="name-2-description">
      Please enter your full name.
    </div>
  </div>
  <div class="email-wrapper field-email field-wrapper">
    &lt;label for="email-2" class="field-label">Email&lt;/label>
    &lt;input type="email" placeholder="Enter your email address" maxlength="100" id="email-2" name="contacts[1].email">
    <div class="field-description" aria-live="polite" id="email-2-description">
      Please enter a valid email address.
    </div>
  </div>
&lt;/fieldset>

```

各パネルの構造は単一パネルの例と同じですが、次の追加の属性があります。

* data-repeatable=&quot;true&quot;：この属性は、JavaScript またはフレームワークを使用して、パネルを動的に繰り返すことができることを示します。

* 一意の ID と名前：パネル内の各要素には、パネルのインデックスに基づく一意の ID（例：name-1、email-1）と name 属性（例：name=&quot;contacts[0].name&quot;）があります。これにより、複数のパネルが送信された場合に適切なデータ収集ができるようになります。

+++

+++ 繰り返し可能なパネルの CSS セレクター

* すべての繰り返し可能なパネルのターゲティング：

```CSS

  /* Target all panels with the repeatable attribute */
 main .form form .panel-wrapper[data-repeatable="true"] &lbrace;
    /* Add your styles here (e.g., border, margin) */
    border: 1px solid #ccc;
    padding: 15px;
    border-radius: 4px;
    margin-bottom: 20px;
  &rbrace;

```

セレクターを使用すると、繰り返し可能なすべてのパネルのスタイルが設定され、一貫したルックアンドフィールが保証されます。


* パネル内の個々のフィールドのターゲティング：

```CSS

/* Target all form field wrappers within a repeatable panel */
main .form form .panel-wrapper[data-repeatable="true"] .{Type}-wrapper &lbrace;
  /* Add your styles here (e.g., margin) */
  margin-bottom: 10px;
&rbrace;

```
このセレクターを使用すると、繰り返し可能なパネル内のすべてのフィールドラッパーのスタイルが設定され、フィールド間の一貫した間隔が維持されます。

* （パネル内の）特定のフィールドのターゲティング：

```CSS

/* Target the name field wrapper within the first panel */
main .form form .panel-wrapper[data-repeatable="true"][data-index="0"] .text-wrapper.field-name &lbrace;
  /* Add your styles here (specific to first name field) */
&rbrace;

/* Target all

```

+++

### ファイル添付

+++ 添付ファイルの HTML 構造

```HTML

<div class="file-wrapper field-{FileName} field-wrapper">
  &lt;legend for="{id}" class="field-label" data-visible="false"> File Attachment &lt;/legend>
  <div class="file-drag-area">
    <div class="file-dragIcon"></div>
    <div class="file-dragText">Drag and Drop To Upload</div>
    &lt;button class="file-attachButton" type="button">Attach&lt;/button>
    &lt;input type="file" accept="audio/*, video/*, image/*, text/*, application/pdf" id="{id}" name="{FileName}" autocomplete="off" multiple="" required="required">
  </div>
  <div class="files-list">
    <div data-index="0" class="file-description">
      <span class="file-description-name">ClaimForm.pdf</span>
      <span class="file-description-size">26 kb</span>
      &lt;button class="file-description-remove" type="button">&lt;/button>
    </div>
  </div>
</div>

```

**HTML 構造の例**


```HTML

<div class="file-wrapper field-claim_form field-wrapper">
  &lt;legend for="claim_form" class="field-label" data-visible="false">File Attachment&lt;/legend>
  <div class="file-drag-area">
    <div class="file-dragIcon"></div>
    <div class="file-dragText">Drag and Drop To Upload</div>
    &lt;button class="file-attachButton" type="button">Attach&lt;/button>
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
main .form form .file-wrapper &lbrace;
  /* Add your styles here (e.g., border, padding) */
  border: 1px solid #ccc;
  padding: 15px;
  border-radius: 4px;
  margin-bottom: 20px;
&rbrace;

```

このセレクターでは、凡例、ドラッグ領域、入力フィールド、リストを含む添付ファイルコンポーネント全体をスタイル設定します。

* 特定の要素のターゲティング：

```CSS

/* Target the drag and drop area */
main .form form .file-wrapper .file-drag-area &lbrace;
  /* Add your styles here (e.g., background color, border) */
  background-color: #f0f0f0;
  border: 1px dashed #ddd;
  padding: 10px;
  text-align: center;
&rbrace;

/* Target the file input element */
main .form form .file-wrapper input[type="file"] &lbrace;
  /* Add your styles here (e.g., hide the default input) */
  display: none;
&rbrace;

/* Target individual file descriptions within the list (populated dynamically) */
main .form form .file-wrapper .files-list .file-description &lbrace;
  /* Add your styles here (e.g., margin, display) */
  display: flex;
  justify-content: space-between;
  margin-bottom: 5px;
&rbrace;

/* Target the file name within the description */
main .form form .file-wrapper .files-list .file-description .file-description-name &lbrace;
  /* Add your styles here (e.g., font-weight) */
  font-weight: bold;
&rbrace;

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
   &lt;label for="{FieldId}" class="field-label">First Name&lt;/label>
   &lt;input type="{Type}" placeholder="{Placeholder}" maxlength="{Max}" id={FieldId}" name="{Name}" aria-describedby="{FieldId}-description">
   <div class="field-description" aria-live="polite" id="{FieldId}-description">
    Hint - First name should be minimum 3 characters and a maximum of 10 characters.
   </div>
</div>

```

**HTML 構造の例**

```HTML

<div class="text-wrapper field-name field-wrapper" data-required="true">
  &lt;label for="name" class="field-label">Name&lt;/label>
  &lt;input type="text" placeholder="Enter your name" maxlength="50" id="name" name="name">
</div>

<div class="number-wrapper field-age field-wrapper" data-required="true">
  &lt;label for="age" class="field-label">Age&lt;/label>
  &lt;input type="number" placeholder="Enter your age" id="age" name="age">
</div>

<div class="email-wrapper field-email field-wrapper" data-required="true">
  &lt;label for="email" class="field-label">Email Address&lt;/label>
  &lt;input type="email" placeholder="Enter your email" id="email" name="email">
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
main .form form .text-wrapper input &lbrace;
  /* Add your styles here */
&rbrace;

/* Target all number input fields */
main .form form .number-wrapper input &lbrace;
  /* Add your styles here */
  letter-spacing: 2px; /* Example for adding letter spacing to all number fields */
&rbrace;

```

+++

### フィールド名に基づくスタイル設定

また、個々のフィールドを名前でターゲットにして、一意のスタイルを適用することもできます。

+++ HTML 構造

```HTML

<div class="{Type}-wrapper field-{Name} field-wrapper" data-required={Required}>
   &lt;label for="{FieldId}" class="field-label">First Name&lt;/label>
   &lt;input type="{Type}" placeholder="{Placeholder}" maxlength="{Max}" id="{FieldId}" name="{Name}" aria-describedby="{FieldId}-description">
   <div class="field-description" aria-live="polite" id="{FieldId}-description">
    Hint - Enter the 6 digit number sent to your mobile number.
   </div>
</div>

```

**HTML 構造の例**

```HTML

<div class="number-wrapper field-otp field-wrapper" data-required="true">
  &lt;label for="otp" class="field-label">OTP&lt;/label>
  &lt;input type="number" placeholder="Enter your OTP" maxlength="6" id="otp" name="otp" aria-describedby="otp-description">
  <div class="field-description" aria-live="polite" id="otp-description">
    Hint - Enter the 6 digit number sent to your mobile number.
   </div>
</div>

```

+++

+++ CSS セレクターの例

```CSS

main .form form .field-otp input &lbrace;
   letter-spacing: 2px
&rbrace;

```

この CSS は、クラス `field-otp` を持つ要素内にあるすべての入力要素をターゲットとします。フォームの HTML 構造はアダプティブフォームブロックの規則に従います。つまり、クラス「field-otp」でマークされたコンテナが「otp」という名前のフィールドを保持します。

+++




## 関連トピック

{{universal-editor-see-also}}
