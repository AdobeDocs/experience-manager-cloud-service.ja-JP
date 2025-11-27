---
title: HTML5 フォームのための CSS スタイルの作成
description: HTML フォーム要素と関連付けられている CSS クラスを変更して、HTML5 フォームの外観を変更する方法について説明します。
contentOwner: robhagat
content-type: reference
topic-tags: hTML5_forms
discoiquuid: a8d986ab-2a4c-488b-957e-4606f7391bd3
feature: HTML5 Forms,Mobile Forms
exl-id: 8cc90ff7-284e-41cd-bfda-7fa09371e270
solution: Experience Manager, Experience Manager Forms
role: Admin, User, Developer
source-git-commit: 1496d7517d586c99c5f1001fff13d88275e91d09
workflow-type: tm+mt
source-wordcount: '838'
ht-degree: 100%

---

# HTML5 フォームのための CSS スタイルの作成 {#creating-css-styles-for-html-forms}

<span class="preview">HTML5 Forms 機能は、早期アクセスプログラムの一部として提供されています。アクセス権をリクエストするには、公式の（勤務先の）メールアドレスから aem-forms-ea@adobe.com にメールを送信してください。
</span>

XFA ベースのフォームテンプレートの HTML5 レンダリングは、様々な HTML 要素で構成されています。これらの要素は一定の順序で整列されます。すべての要素には、適切に定義された CSS クラスがあります。これらの CSS クラスを使用して、要素の外観を選択し変更することができます。

>[!NOTE]
>
>CSS クラスで、幅、高さ、境界線厚さ、上、左、右、下、パディング、マージン、およびその他の位置とサイズの属性は変更しないでください。位置とサイズの属性を変更すると、フォームのレイアウトが変わります。

## 要素の CSS クラス {#css-classes-nbsp-for-elements-nbsp}

すべての要素には、適切に定義された CSS クラスがあります。これらのクラスを変更して、要素の外観を変更することができます。フィールド要素と描画要素を除くすべての要素は、2 つの CSS クラス（Type クラスと Name クラス）を持ちます。

* **Type クラス**&#x200B;は XFA フィールドのタイプを表します。`type` クラスをオーバーライドして、特定タイプのすべての要素のスタイルを変更できます。

* **Name クラス**&#x200B;は XFA フィールドの名前に対応します。`name` クラスをオーバーライドして、スタイルを変更しカスタムスタイルを要素に適用できます。

>[!NOTE]
>
>一部の XFA 要素には名前がありません。そのようなコンポーネントのスタイルを変更するには、その特定タイプのすべてのコンポーネントを変更してください。

AEM Forms Designer で名付けられていないページでは、HTML5 フォームのページはページ番号順に名付けられます。例えば、2 ページからなる HTML5 フォームの場合、ページは Page1 および Page2 と名付けられます。

## Field 要素 {#field-element}

Field 要素にはネストされた要素が 2 つ（widget と caption）あります。

**Widget 要素**

Widget 要素にはユーザーとやりとりするためのユーザーインターフェイス要素が含まれています。それには 3 つの CSS クラスがあります。

* **Widget**：すべてのウィジェットにこのクラスがあります。
* **name**：AEM とともに出荷されたすべてのウィジェットにはウィジェット名のクラスがあります。カスタムウィジェットでは、ウィジェット開発者がウィジェット名のクラスを提供します。
* **type**：すべてのウィジェットにはユーザーインターフェイス要素があります。このクラスはユーザーインターフェイス要素のタイプを定義します。

```xml
<!--field with caption-->
<div class="field numericfield NumericField3 ">
     <div class="caption">
        caption content
     </div>
     <div class="widget numericfieldwidget numericInput">
       widget content
     </div>
</div>

<!--field without caption-->
<div class="widget numericfieldwidget numericInput">
   widget content
</div>
```

type と name クラスの他に、フィールドコンポーネントにも **subtype** という名前の追加の CSS クラスがあります。subtype はそれがどのフィールドのタイプであるかを識別します。例：NumericField、DateField、TextField。subtype クラスはオーバーライドして、subtype のタイプであるすべてのフィールドのスタイル設定を変更できます。

## 異なるコンポーネントに対する CSS クラス {#css-classes-for-different-components}

<table>
 <tbody>
  <tr>
   <td><strong>コンポーネント</strong></td>
   <td><strong>タイプ</strong></td>
   <td><strong>名前</strong></td>
  </tr>
  <tr>
   <td>ページ</td>
   <td>ページ</td>
   <td>ユーザー定義の名前<br />または<br /> Page&lt;pageNumber&gt;（デフォルト）</td>
  </tr>
  <tr>
   <td>コンテンツ領域</td>
   <td>contentarea</td>
   <td>ユーザー定義の名前</td>
  </tr>
  <tr>
   <td>サブフォーム</td>
   <td>subform</td>
   <td>ユーザー定義の名前</td>
  </tr>
  <tr>
   <td>排他グループ</td>
   <td>exclgroup</td>
   <td>ユーザー定義の名前</td>
  </tr>
  <tr>
   <td>図面</td>
   <td>draw</td>
   <td>ユーザー定義の名前</td>
  </tr>
  <tr>
   <td>フィールド</td>
   <td>field</td>
   <td>ユーザー定義の名前</td>
  </tr>
  <tr>
   <td>キャプション</td>
   <td>caption</td>
   <td>該当なし</td>
  </tr>
  <tr>
   <td>ウィジェット</td>
   <td>widget</td>
   <td>ウィジェット開発者が定義します（ユーザー定義のウィジェットに関しては、以下の節の表を参照してください）</td>
  </tr>
 </tbody>
</table>

## 異なるフィールドに対する CSS クラス {#css-classes-for-different-fields}

AEM Forms Designer はフォームで NumericField、DecimalField、および Date Field などの異なるタイプのフィールドをサポートしています。HTML ですべてのこれらのフィールドには上記の CSS クラスがあります。また、それらにはフィールドのタイプによっては、いくつかの追加のクラスがあります。

すべてのフィールドには UI 要素を示す、関連するウィジェットがあります。各フィールドのクラス、および各フィールドに関連するウィジェットを以下に示します。

<table>
 <tbody>
  <tr>
   <td><strong>フィールドタイプ</strong></td>
   <td><strong>サブタイプ</strong></td>
   <td><strong>ウィジェット名</strong></td>
   <td><strong>ウィジェットタイプ</strong></td>
   <td><strong>HTML UI タグ</strong></td>
  </tr>
  <tr>
   <td>ボタン<br type="_moz" /> </td>
   <td>該当なし</td>
   <td>xfaButton<br type="_moz" /> </td>
   <td>buttonfieldwidget<br type="_moz" /> </td>
   <td>input type=button<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>CheckButton<br type="_moz" /> </td>
   <td>checkboxfield<br /> </td>
   <td>XfaCheckBox<br type="_moz" /> </td>
   <td>checkboxfieldwidget<br type="_moz" /> </td>
   <td>input type=checkbox<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>DateField<br type="_moz" /> </td>
   <td>datefield<br type="_moz" /> </td>
   <td>dateField<br type="_moz" /> </td>
   <td>datefieldwidget<br type="_moz" /> </td>
   <td>inputtype = text<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>DateTimeField<br type="_moz" /> </td>
   <td>textfield<br type="_moz" /> </td>
   <td>textField<br type="_moz" /> </td>
   <td>textfieldwidget</td>
   <td>inputtype = text<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>DecimalField<br type="_moz" /> </td>
   <td>numericfield<br type="_moz" /> </td>
   <td>numericInput<br type="_moz" /> </td>
   <td>numericfieldwidget<br type="_moz" /> </td>
   <td>inputtype = text<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>DropDown<br type="_moz" /> </td>
   <td>choicelist<br type="_moz" /> </td>
   <td>dropDownListWidget<br type="_moz" /> </td>
   <td>choicelistwidget<br type="_moz" /> </td>
   <td>select</td>
  </tr>
  <tr>
   <td>ListBox<br type="_moz" /> </td>
   <td>choicelist<br type="_moz" /> </td>
   <td>listBoxWidget<br type="_moz" /> </td>
   <td>choicelistwidget<br type="_moz" /> </td>
   <td>ol</td>
  </tr>
  <tr>
   <td>NumericField<br type="_moz" /> </td>
   <td>numericfield<br type="_moz" /> </td>
   <td>numericInput<br type="_moz" /> </td>
   <td>numericfieldwidget<br type="_moz" /> </td>
   <td>inputtype = text<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>PasswordField<br type="_moz" /> </td>
   <td>passwordfield<br type="_moz" /> </td>
   <td>defaultWidget<br type="_moz" /> </td>
   <td>passwordfieldwidget<br type="_moz" /> </td>
   <td>input type=password<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>RadioButton<br type="_moz" /> </td>
   <td>radiofield<br type="_moz" /> </td>
   <td>XfaCheckBox<br type="_moz" /> </td>
   <td>radiofieldwidget<br type="_moz" /> </td>
   <td>input type=radio<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>TextField<br type="_moz" /> </td>
   <td>textfield<br type="_moz" /> </td>
   <td>textField<br type="_moz" /> </td>
   <td>textfieldwidget<br type="_moz" /> </td>
   <td>inputtype = text<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>TimeField<br type="_moz" /> </td>
   <td>textfield<br type="_moz" /> </td>
   <td>textField<br type="_moz" /> </td>
   <td>textfieldwidget<br type="_moz" /> </td>
   <td>inputtype = text<br type="_moz" /> </td>
  </tr>
 </tbody>
</table>

## 異なる Draw 要素に対する CSS クラス {#css-classes-for-different-draw-elements}

AEM Forms Designer を使用して、テキスト、画像など、スタティックの描画要素を挿入できます。それぞれの描画要素に対し、別の CSS クラスがそれらの要素に関連しています。描画要素の CSS クラスのリストを以下に示します。それぞれの描画要素には、それに関連する draw クラスがあります。

| **描画タイプ** | **CSS クラス** |
|---|---|
| テキスト | text |
| 画像 | image |
| 長方形 | rectangle |
| 線 | line |

## フォームにおける他の部分のスタイル設定 {#styling-other-parts-of-the-form}

HTML フォームでの UI コンポーネントの外観の以外に、インラインエラー、インライン警告および検証エラーのあるフィールドなどの要素のスタイルを変更できます。

`Styling Inline Errors`

フィールドの検証によりエラーが発生した場合、フィールドがアクティブのときにインラインエラーが表示されます。インラインエラーのスタイルを変更するには、CSS ID **error-msg** をオーバーライドします。

`Styling Inline Warnings`

フィールドの検証により警告が発生した場合、フィールドがアクティブのときにインライン警告が表示されます。これらのインライン警告のスタイルを変更するには、CSS ID **warning-msg** をオーバーライドします。

`Styling Fields with Validation Errors`

フィールドの検証に失敗すると、ウィジェットのスタイルが変更されます。このスタイルの変更はウィジェットコンポーネントに **widgetError **&#x200B;の CSS クラスを適用することにより実施されます。デフォルトのスタイル設定を変更するには、**widgetError** クラスをオーバーライドします。
