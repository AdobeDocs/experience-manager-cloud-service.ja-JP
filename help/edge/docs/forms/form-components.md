---
title: フォームのコンポーネントとプロパティ
description: このドキュメントでは、AEM Forms Edge Delivery Service で使用できるフォームコンポーネントとそのプロパティの概要を説明します。
feature: Edge Delivery Services
hide: true
hidefromtoc: true
exl-id: 7d087d41-9313-482a-a905-8955b0999781
source-git-commit: 2aa70e78764616f41fe64e324c017873cfba1d5b
workflow-type: tm+mt
source-wordcount: '964'
ht-degree: 3%

---

# フォームのコンポーネントとプロパティ：AEM Forms Edge Delivery Service

AEM Forms Edge Delivery Services を使用すると、様々なコンポーネントを使用して、使いやすくインタラクティブなフォームを作成できます。 これらのコンポーネントは、様々なタイプのデータ収集に対応し、特定のニーズに合わせて容易にカスタマイズできます。


![一部のコンポーネントとプロパティを含むサンプルスプレッドシート](/help/edge/assets/sample-form-in-spreadsheet.png)

アダプティブFormsブロックは、 [均一HTML構造](/help/edge/docs/forms/style-theme-forms.md) の一貫性を確保するために、すべてのフィールドタイプおよびコンテナ（パネル）に対して使用できます。 この一貫した構造により、 [フォームのスタイルを設定する](/help/edge/docs/forms/style-theme-forms.md).

## 使用可能なコンポーネント

使用可能なコンポーネントの概要を次に示します。

### 入力フィールド

- すべての有効なHTML5 [入力タイプ](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/input#input_types) および [textarea](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/textarea). 例えば、button、checkbox、color、datetime-local、email、file、hidden、image、month、number、password、radio、range、reset、submit、tel、text、time、url、および week などです。

### 選択コントロール

- [チェックボックスグループ](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/input/checkbox)：複数のオプションを選択する場合。
- [ラジオグループ](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/input/radio)：グループから 1 つのオプションを選択する場合。
- [ドロップダウンメニュー](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/select)：オプションのメニューを表示します。 例えば、ドロップダウンボックスを使用します。

### コンテナ

- パネル/コンテナ：関連するフォーム要素をグループ化し、整理を改善します。 これは、 [fieldset](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/fieldset) および [凡例](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/legend).






## コンポーネントのプロパティ

各フォームコンポーネントには、動作と外観を制御できる様々なプロパティが用意されています。 アダプティブFormsブロックコンポーネントでサポートされるプロパティを次に示します。


| プロパティ | 適用可能なコンポーネント | 詳細 |
|--------------|------------------------------|----------------------------------------------------------------------|
| タイプ | すべて | コンポーネントのタイプを指定します。 このプロパティは、入力フィールドの動作と外観を決定します。 例えば、テキスト入力の場合、タイプは「テキスト」、「電子メール」（電子メール入力）、「パスワード」（パスワード入力）のようになります。 アダプティブFormsブロックのサポート  <a href="https://developer.mozilla.org/en-US/docs/Web/HTML/Element/input#input_types">すべての有効なHTML5 入力タイプ</a>, <a href="https://developer.mozilla.org/en-US/docs/Web/HTML/Element/textarea">textarea</a>, <a href="https://developer.mozilla.org/en-US/docs/Web/HTML/Element/select">選択</a>、および <a href="https://developer.mozilla.org/en-US/docs/Web/HTML/Element/fieldset">fieldset</a> をタイプとして使用します。 |
| タイプ | すべて | コンポーネントのタイプを指定します。 このプロパティは、入力フィールドの動作と外観を決定します。 例えば、テキスト入力の場合、タイプは「テキスト」、「電子メール」（電子メール入力）、「パスワード」（パスワード入力）のようになります。 アダプティブFormsブロックのサポート  <a href="https://developer.mozilla.org/en-US/docs/Web/HTML/Element/input#input_types">すべての有効なHTML5 入力タイプ</a>, <a href="https://developer.mozilla.org/en-US/docs/Web/HTML/Element/textarea">textarea</a>, <a href="https://developer.mozilla.org/en-US/docs/Web/HTML/Element/select">選択</a>、および <a href="https://developer.mozilla.org/en-US/docs/Web/HTML/Element/fieldset">fieldset</a> をタイプとして使用します。 |
| 名前 | すべて | フォーム送信用のコンポーネントを識別します。 name 属性は、フォームデータがサーバーに送信される際に使用され、ユーザー入力が特定のフィールドに関連付けられます。 |
| ラベル | すべて | ユーザーにコンテキスト情報を提供します。 ラベルは、コンポーネントの横に表示されるテキストで、ユーザーが入力する情報に関するガイダンスを提供します。 |
| 値 | テキスト、パスワード、電子メール、数値、範囲、日付およびそのバリエーション (datetime-local、month、week、time)、チェックボックス、ラジオ、非表示、送信、ボタン | コンポーネントの初期値を指定します。 テキスト入力、テキスト領域、および要素の選択の場合、これはデフォルトのテキストまたはオプションとして表示されます。 ラジオおよびチェックボックスコンポーネントの場合、これは選択時に送信される値/データです。 value 属性はオプションですが、チェックボックスとラジオの入力に必須と見なす必要があります。 |
| プレースホルダー | テキスト、Tel、Email、パスワード、日付（および月、週、時間、日時 — ローカルなどのそのバリアント）、数値、範囲 | 期待される入力のヒントを提供します。 placeholder 属性には、入力フィールドの期待値を示す簡単なヒントが表示されます。 ユーザーが入力を開始すると、この属性は消えます。 |
| 説明 | すべて | コンポーネントに関する追加情報を提供し、ヘルプテキストとして機能します。 「説明」フィールドでは、コンポーネントの入力の目的や手順をさらに詳しく説明できます。 これは、ユーザーが入力フィールドのコンテキストを理解するのに役立ちます。 |
| 表示 | すべて | 初期表示を制御します。 visible 属性は、フォームの読み込み時にコンポーネントが最初に表示されるか非表示になるかを決定するブール型プロパティです。 true に設定した場合、フィールドが表示されます。それ以外の場合は非表示になります。 |
| 必須 | テキスト、Tel、Email、パスワード、日付およびそのバリエーション（日時 — ローカル、月、週、時間）、数値、チェックボックス、ラジオ、ファイル、選択（ドロップダウン）、テキスト領域 | 送信前にフィールドに入力する必要があるかどうかを示します。 mandatory 属性は、フォームを送信する前にユーザーがフィールドの入力を提供する必要があるかどうかを指定するために使用される boolean プロパティです。 |
| 最小 | 日付（および月、週、時間、日時 — ローカルなどのバリアント）、数値、範囲 | 最小許容値を指定します。 min 属性は、ユーザーがフィールドに入力できる最小値を設定します。 例えば、数値入力の場合は、許容される最小の数値を定義します。 |
| Max | 日付（および月、週、時間、日時 — ローカルなどのバリアント）、数値、範囲 | 許容される最大値を指定します。 max 属性は、ユーザーがフィールドに入力できる最大値を設定します。 例えば、日付入力の場合は、許容できる最も高い日付を定義します。 |
| 確定 | File | 許可されるファイルタイプを定義します。 accept 属性は、一意のファイルタイプ指定子のコンマ区切りリストで、ユーザーがファイル入力フィールドで選択できるファイルのタイプを制限します。 |
| 複数 | File | 複数の選択を許可します。 multiple 属性は、ファイル入力フィールドで使用されるブール型プロパティです。 true に設定すると、ユーザーは複数のファイルを選択できます。 |
| オプション | ドロップダウン | ドロップダウンメニューの選択肢を指定します。 options プロパティは、ドロップダウンメニューの選択肢のコンマ区切りリストで、ユーザーに表示される選択可能なオプションを定義します。 |
| チェック済み | チェックボックス、ラジオ | フィールドがデフォルトで選択されているかどうかを指定します。 checked 属性は、チェックボックスとラジオの入力で使用されるブール型プロパティです。 true に設定した場合は、フォームの読み込み時に、フィールドがデフォルトで選択されていることを示します。 |
| Fieldset | すべて | フォーム内に視覚的に異なるセクションを作成するためにフィールドをグループ化します。 fieldset 要素は、フォーム内の関連するフィールドを視覚的に分けてグループ化し、組織やユーザーエクスペリエンスを向上させます。 </br> フィールドセット内の一連のフィールドを整理するには、 `fieldset` プロパティを選択し、その名前属性を指定します。 次の例では、組織を改善するために、ラジオボタンを 1 つのフィールドセット内にカプセル化する方法を示します。 ![フィールドセットの例](/help/edge/assets/fieldset-example.png) |



<!--

## Supported HTML 5 input types in Adaptive Forms Block

The Adaptive Forms Block supports a range of HTML 5 input types, and it also seamlessly renders forms created with AEM core components.
Here is the table which outlines how core components correspond to their HTML-5 input types in Edge Delivery:
<table>
 <tbody>
  <tr>
   <td><b>Core Components</b> </td>
   <td><b>HTML 5 input type</b> </td>
   <td><b>Details</b></td>
  </tr>
  <tr>
   <td><a href ="https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/form-container.html">Form Container</a></td>
   <td><a href ="https://developer.mozilla.org/en-US/docs/Web/HTML/Element/input#form">form </td>
   <td> Create a form to capture user inputs.
   </td>
  </tr>
  <tr>
   <td><a herf="https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/text-input.html">Text Input</a></td>
   <td><a href ="https://developer.mozilla.org/en-US/docs/Web/HTML/Element/input/text">text</a></td>
   <td> Defines a single-line text input field. </td>
  </tr>
  <tr>
   <td><a href = "https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/number-input.html">Number Input</a></td>
   <td><a href = "https://developer.mozilla.org/en-US/docs/Web/HTML/Element/input/number">number</a></td>
   <td>Lets user  enter a number input. You can also add built-in validation to reject non-numerical inputs. Lets user  enter a number input. You can also add built-in validation to reject non-numerical inputs. Initially, the input field is displayed as a number input. If a user applies a display pattern, it changes to text to allow the author to apply number formatting, since HTML 5 lacks support for display patterns. However, when the user clicks it, it returns to typing numbers.</td>
  </tr>
  <tr>
   <td><a href ="https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/date-picker.html">Date Picker</a></td>
   <td><a href = "https://developer.mozilla.org/en-US/docs/Web/HTML/Element/input/date">date </a></td>
   <td> Create an input field for entering a date. You have the option to input the date either through a text box, which validates the entry, or through a dedicated date picker interface. Initially, the native date input field is displayed. If a user applies a display pattern, it changes to text to allow the user to apply formatting, since HTML 5 lacks support for display patterns. However, when the user clicks it, it returns to typing a date.</td>
  </tr>
  <tr>
   <td><a href ="https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/file-attachment.html">File Attachment</a></td>
   <td><a href ="https://developer.mozilla.org/en-US/docs/Web/HTML/Element/input/file">file</a></td>
   <td> Allows user to choose one or more files from the device storage. It supports enhanced file input validations, such as accepted file types, file size restrictions, and minimum/maximum file selection limits. </td>
  </tr>
  <tr>
   <td><a href ="https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/drop-down.html"> Dropdown List</a></td>
   <td><a href ="https://developer.mozilla.org/en-US/docs/Web/HTML/Element/select">select</a></td>
   <td> Allows users to select one or more options from a list of predefined options. The options can be of type String, Number, or Boolean.</td>
  </tr>
  <tr>
   <td><a href ="https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/checkbox-group.html">Checkbox Group</a></td>
   <td><a href ="https://developer.mozilla.org/en-US/docs/Web/HTML/Element/input/checkbox">multiple checkbox</a></td>
   <td> Allow users to select one or more options from a list. Multiple checkboxes are generated with identical names, each corresponding to an item in the enum. </td>
  </tr>
  <tr>
   <td><a href ="https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/radio-button.html">Radio Button Group</td>
   <td><a href ="https://developer.mozilla.org/en-US/docs/Web/HTML/Element/input/radio">multiple radio</a></td>
   <td> Allows a user to select one option from a group of related options. Multiple radio buttons are generated with identical names, each corresponding to an item in the enum.</td>
  </tr>
  <tr>
   <td><a href ="https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/button.html">Button</td>
   <td><a href ="https://developer.mozilla.org/en-US/docs/Web/HTML/Element/input/button">button</a></td>
   <td>A UI element that allows users to trigger an action when clicked. </td>
  </tr>
  <tr>
   <td><a href =""https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/panel-container.html">Panel</a></td>
   <td><a href ="https://developer.mozilla.org/en-US/docs/Web/HTML/Element/fieldset">fieldset with legend</a></td>
   <td> Group sections within a form, where a nested *legend* element adds a caption for the form.</td>
  </tr>
   <tr>
   <td><a href ="https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/wizard.html">Wizard</a></td>
   <td><a href ="https://developer.mozilla.org/en-US/docs/Web/HTML/Element/fieldset">fieldset</a></td>
   <td>Groups related sections within a form. It also controls the arrangement, supporting display options for positioning them at the top or at the left side. </td>
  </tr>
    <tr>
   <td><a href ="https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/text.html">Text</a></td>
   <td><a href ="https://developer.mozilla.org/en-US/docs/Web/HTML/Element/p">p</a></td>
   <td>A p tag marks a paragraph. In visual content, paragraphs are chunks of text separated by blank lines or an indented first line</td>
  </tr>
     <tr>
   <td><a href ="https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/submit-button.html">Submit button</td>
   <td><a href ="https://developer.mozilla.org/en-US/docs/Web/HTML/Element/input/submit">submit</a></td>
   <td> A UI element that enables users to submit a form to the server upon clicking. If a user adds a submit rule to a button, it functions as the submit button. </td>
  </tr>
     <tr>
   <td><a href = "https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/reset-button.html">Reset button</a></td>
   <td><a href ="https://developer.mozilla.org/en-US/docs/Web/HTML/Element/input/reset">reset</a></td>
   <td>A UI element that resets a form upon clicking. If a user adds a reset rule to a button, it functions as the reset button. </td>
  </tr>
    <tr>
   <td><a href ="https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/email-input.html">Email Input</td>
   <td><a href ="https://developer.mozilla.org/en-US/docs/Web/HTML/Element/input/email">email</a></td>
   <td> Allows the user to enter and edit an email address. If the user adds the multiple attributes, a list of email addresses can be added or edited.</td>
  </tr>
   <tr>
   <td><a href ="https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/telephone-input.html">Telephone Input</a></td>
   <td><a href ="https://developer.mozilla.org/en-US/docs/Web/HTML/Element/input/tel">tel</a></td>
   <td>Allows user to enter and edit a telephone number.</td>
  </tr>
   <tr>
   <td><a href ="https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/header.html">Header</td>
   <td><a href = "https://developer.mozilla.org/en-US/docs/Web/HTML/Element/header"> header</a></td>
   <td>It includes introductory content, typically a group of introductory or navigational aids. It is supported outside Form container. </td>
  </tr>
  <tr>
   <td><a href ="https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/footer.html">Footer</td>
   <td><a href = "https://developer.mozilla.org/en-US/docs/Web/HTML/Element/footer">footer</a></td>
   <td> Contains information such as copyright data or links to related documents. It is supported outside Form container.</td>
  </tr>
  <tr>
   <td><a href = "https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/accordion.html">Accordion<a></td>
   <td><i>Not yet supported in Adaptive Forms Block</i></td>
   <td> Allows user to create expandable and collapsible sections in a form. </td>
  </tr>
  <tr>
   <td><a href ="https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/horizontal-tabs.html">Horizontal tabs</a></td>
   <td><i>Not yet supported in Adaptive Forms Block</i></td>
   <td>Organizes multiple sections of a form into separate tabs which are displayed horizontally.</td>
  </tr>
  <tr>
   <td><a href = "https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/image.html">Image</a></td>
   <td><i>Not yet supported in Adaptive Forms Block</i></td>
   <td> Allows user to include images in a form.</td>
  </tr><tr>
   <td><a href ="https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/title.html">Title</a></td>
   <td><i>Not yet supported in Adaptive Forms Block</i></td>
   <td> Refers to the text that appears at the top of the form. </td>
  </tr>
  <tr>
   <td><a href = "https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/submit-button.html">Switch</td>
   <td><i>Not yet supported in Adaptive Forms Block</i></td>
   <td> A two-state toggle that allows user to select between two states such as enabling or disabling a feature, setting, or functionality.</td>
  </tr>
 </tbody>
</table> -->

## 詳細を表示する

- [フォームの作成とプレビュー](/help/edge/docs/forms/create-forms.md)
- [フォームからデータを送信できるようにする](/help/edge/docs/forms/submit-forms.md)
- [サイトページにフォームを発行する](/help/edge/docs/forms/publish-forms.md)
- [フォームフィールドに検証機能を追加する](/help/edge/docs/forms/validate-forms.md)
- [フォームのテーマとスタイルを変更する](/help/edge/docs/forms/style-theme-forms.md)
