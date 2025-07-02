---
title: この記事では、コアコンポーネントに基づくアダプティブフォームのカスタム機能の様々なユースケースについて概要を説明します。
description: この記事では、コアコンポーネントに基づくアダプティブフォームのカスタム機能の様々なユースケースについて説明します。 カスタム関数は、ルールエディターでフォームのカスタムルールを作成するために使用されます。
feature: Adaptive Forms, Core Components
role: User, Developer
level: Beginner, Intermediate
exl-id: df92b91e-f3b0-4a08-bd40-e99edc9a50a5
source-git-commit: 5b5b44f8dffc01a75eda464cd7759cf03028c2c6
workflow-type: tm+mt
source-wordcount: '2184'
ht-degree: 34%

---

# カスタム関数の開発と使用の例

この記事では、コアコンポーネントに基づくアダプティブフォームのカスタム関数の詳細な例を示し、様々なシナリオでの効果的な実装に関する貴重なインサイトを提供します。 カスタム関数は、AEM Formsのルールエディターで使用されます。これにより、開発者は、フォームの動作を制御するロジックを定義および制御できます。
この記事では、カスタム関数の様々な実装について説明し、特定の要件に合わせてフォームをカスタマイズし、全体的な機能を強化する方法を示します。

## カスタム関数を使用したドロップダウンリストのオプションへの入力

コアコンポーネントのルールエディターは、実行時にドロップダウンリストのオプションに動的に値を入力する **オプションを設定** プロパティをサポートしていません。 ただし、カスタム関数を使用してドロップダウンリストのオプションに値を入力することにより、特定のロジックに基づいてオプションを取得できます。 カスタム関数を使用すると、ドロップダウンオプションの入力方法とタイミングをより柔軟に制御でき、ユーザーエクスペリエンスが向上します。

カスタム関数を使用してドロップダウンリストのオプションに値を入力するには、「[create-custom-function](/help/forms/custom-function-core-component-create-function.md)」セクションで説明されているように、次のコードを追加します。


```javascript
    /**
    * @name setEnums
    * @returns {string[]}
    **/
    function setEnums() {
    return ["0","1","2","3","4","5","6"];   
    }

    /**
    * @name setEnumNames
    * @returns {string[]}
    **/
    function setEnumNames() {
    return ["Sunday","Monday", "Tuesday", "Wednesday", "Thursday", "Friday", "Saturday"];
    }
```

上記のコードでは、`setEnums` を使用して `enum` プロパティを設定し、`setEnumNames` を使用してドロップダウンの `enumNames` プロパティを設定しています。

ユーザーが「`Next`」ボタンをクリックしたときにドロップダウンリストの値オプションを設定する「`Next`」ボタン用のルールを作成してみましょう。

![ ドロップダウンリストのオプション ](/help/forms/assets/drop-down-list-options.png)

「表示」ボタンをクリックしたときにドロップダウンリストのオプションが設定される場所を示すには、次の図を参照してください。

![ ルールエディターのドロップダウンオプション ](/help/forms/assets/drop-down-option-rule-editor.png)

## `SetProperty` ルールを使用したパネルの表示

カスタム関数でフィールドおよびグローバルオブジェクトを使用する方法を、`Contact Us` フォームを使用して説明します。

![お問い合わせフォーム](/help/forms/assets/contact-us-form.png)

フォームフィールドを `Required` として設定するには、[カスタム関数の作成](/help/forms/custom-function-core-component-create-function.md)の節の説明に従って、カスタム関数に次のコードを追加します。

```javascript
    
    /**
    * enablePanel
    * @name enablePanel
    * @param {object} field1
    * @param {object} field2
    * @param {scope} globals 
    */

    function enablePanel(field1,field2, globals)
    {
       if(globals.functions.validate(field1).length === 0)
       {
       globals.functions.setProperty(field2, {visible: true});
       }
    }
```

>[!NOTE]
>
> * `[form-path]/jcr:content/guideContainer.model.json` にある使用可能なプロパティを使用して、フィールドプロパティを設定できます。
> * Globals オブジェクトの `setProperty` メソッドを使用してフォームに行った変更は、本質的に非同期で、カスタム関数の実行中には反映されません。

この例では、ボタンをクリックすると `personaldetails` パネルの検証が行われます。パネルでエラーが検出されない場合は、ボタンをクリックすると別のパネルである `feedback` パネルが表示されます。

`personaldetails` パネルを検証し、ユーザーが `Next` ボタンをクリックした際に `feedback` パネルが表示されるようにする `Next` ボタンのルールを作成しましょう。

![プロパティの設定](/help/forms/assets/custom-function-set-property.png)

`Next` ボタンをクリックすると、`personaldetails` パネルが検証される場所を示す次のイラストを参照してください。`personaldetails` 内のすべてのフィールドを検証すると、`feedback` パネルが表示されます。

![プロパティフォームのプレビューを設定](/help/forms/assets/set-property-form-preview.png)

`personaldetails` パネルのフィールドにエラーがある場合は、`Next` ボタンをクリックする際にフィールドレベルでエラーが表示され、`feedback` パネルは非表示のままになります。

![プロパティフォームのプレビューを設定](/help/forms/assets/set-property-panel.png)

## フィールドを検証

カスタム関数がフィールドオブジェクトとグローバルオブジェクトを使用して、`Contact Us` フォームを使用してフィールドを検証する方法を説明します。

フィールドを検証するには、[カスタム関数の作成](/help/forms/custom-function-core-component-create-function.md)の節の説明に従って、カスタム関数に次のコードを追加します。

```javascript
    /**
    * validateField
    * @name validateField
    * @param {object} field
    * @param {scope} globals
    */
    function validateField(field,globals)
    {
    
        globals.functions.validate(field);
    
    }   
```

>[!NOTE]
>
> `validate()` 関数に引数が渡されない場合は、フォームが検証されます。

この例では、カスタム検証パターンが `contact` フィールドに適用されます。ユーザーは、`10` で始まり `8` 桁の電話番号を入力する必要があります。ユーザーが `10` で始まらない電話番号、または `8` 桁以上または未満の電話番号を入力した場合、ボタンをクリックすると検証エラーメッセージが表示されます。

![メールアドレスの検証パターン](/help/forms/assets/custom-function-validation-pattern.png)

次の手順では、ボタンのクリック時に `contact` フィールドを検証する `Next` ボタンのルールを作成します。

![検証パターン](/help/forms/assets/custom-function-validate.png)

ユーザーが `10` で始まらない電話番号を入力すると、フィールドレベルでエラーメッセージが表示されることを示す次のイラストを参照してください。

![メールアドレスの検証パターン](/help/forms/assets/custom-function-validate-error-message.png)

ユーザーが有効な電話番号を入力し、`personaldetails` パネルのすべてのフィールドが検証されると、`feedback` パネルが画面に表示されます。

![メールアドレスの検証パターン](/help/forms/assets/validate-form-preview-form.png)

## パネルのリセット

カスタム関数がフィールドとグローバルオブジェクトを使用して、`Contact Us` フォームを使用してフィールドをリセットする方法を説明します。

パネルをリセットするには、[カスタム関数の作成](/help/forms/custom-function-core-component-create-function.md)の節の説明に従って、カスタム関数に次のコードを追加します。

```javascript
    /**
    * resetField
    * @name  resetField
    * @param {string} input1
    * @param {object} field
    * @param {scope} globals 
    */
    function  resetField(field,globals)
    {
    
        globals.functions.reset(field);
    
    }
```

>[!NOTE]
>
> `reset()` 関数で引数を渡さない場合は、フォームが検証されます。

この例では、`Clear` ボタンをクリックすると `personaldetails` パネルがリセットされます。次のステップでは、ボタンのクリック時にパネルをリセットする `Clear` ボタンのルールを作成します。

![クリアボタン](/help/forms/assets/custom-function-reset-field.png)

ユーザーが `clear` ボタンをクリックすると、`personaldetails` パネルがリセットされることを示す次のイラストを参照してください。

![フォームをリセット](/help/forms/assets/custom-function-reset-form.png)

## フィールドレベルでカスタムメッセージを表示し、フィールドを無効としてマークするには

カスタム関数で、フィールドとグローバルオブジェクトを使用して、フィールドレベルでカスタムメッセージを表示し、`Contact Us` フォームを使用してフィールドを無効としてマークする方法を説明します。

`markFieldAsInvalid()` 関数を使用すると、フィールドを無効として定義し、フィールドレベルでカスタムエラーメッセージを設定できます。`fieldIdentifier` の値は、`fieldId`、`field qualifiedName` または `field dataRef` に指定できます。`option` という名前のオブジェクトの値は、`{useId: true}`、`{useQualifiedName: true}` または `{useDataRef: true}` に指定できます。
フィールドを無効としてマークし、カスタムメッセージを設定するために使用される構文は次のとおりです。

* `globals.functions.markFieldAsInvalid(field.$id,"[custom message]",{useId: true});`
* `globals.functions.markFieldAsInvalid(field.$qualifiedName, "[custom message]", {useQualifiedName: true});`
* `globals.functions.markFieldAsInvalid(field.$dataRef, "[custom message]", {useDataRef: true});`

[create-custom-function](/help/forms/custom-function-core-component-create-function.md) の節で説明したように、カスタム関数に次のコードを追加して、フィールドレベルでカスタムメッセージを有効にします。

```javascript
    /**
    * customMessage
    * @name customMessage
    * @param {object} field
    * @param {scope} globals 
    */
    function customMessage(field, globals) {
    const minLength = 15;
    const comments = field.$value.trim();
    if (comments.length < minLength) {
        globals.functions.markFieldAsInvalid(field.$id, "Comments must be at least 15 characters long.", { useId: true });
    }
}
```

この例では、ユーザーがコメントテキストボックスに 15 文字未満を入力すると、フィールドレベルでカスタムメッセージが表示されます。

次の手順では、`comments` フィールドのルールを作成します。

![フィールドを無効としてマーク](/help/forms/assets/custom-function-invalid-field.png)

`comments` フィールドに否定的なフィードバックを入力すると、フィールドレベルでカスタムメッセージが表示されることを示す次のデモを参照してください。

![フィールドを無効なプレビューフォームとしてマーク](/help/forms/assets/custom-function-invalidfield-form.png)

ユーザーが「コメント」テキストボックスに 15 文字を超えて入力すると、フィールドが検証され、フォームが送信されます。

![フィールドを有効なプレビューフォームとしてマーク](/help/forms/assets/custom-function-validfield-form.png)

## 変更したデータをサーバーに送信

カスタム関数がフィールドとグローバルオブジェクトを使用して、`Contact Us` フォームを使用してサーバーで操作データを送信する方法を説明します。

次のコード行：
`globals.functions.submitForm(globals.functions.exportData(), false);` は、操作後にフォームデータを送信するために使用されます。
* 最初の引数は、送信するデータです。
* 2 番目の引数は、フォームを送信する前に検証するかどうかを表します。これは `optional` であり、デフォルトでは `true` に設定されています。
* 3 番目の引数は送信の `contentType` です。これもオプションで、デフォルト値は `multipart/form-data` です。その他の値は、`application/json` と `application/x-www-form-urlencoded` に指定できます。

操作したデータをサーバーに送信するには、[カスタム関数の作成](/help/forms/custom-function-core-component-create-function.md)の節の説明に従って、カスタム関数に次のコードを追加します。

```javascript
    /**
    * submitData
    * @name submitData
    * @param {object} field
    * @param {scope} globals 
    */
    function submitData(globals)
    {
    
    var data = globals.functions.exportData();
    if(!data.comments) {
    data.comments = 'NA';
    }
    console.log('After update:{}',data);
    globals.functions.submitForm(data, false);
    }
```

この例では、ユーザーが `comments` テキストボックスを空のままにすると、フォームの送信時に `NA` がサーバーに送信されます。

次に、データを送信する `Submit` ボタンのルールを作成します。

![データを送信](/help/forms/assets/custom-function-submit-data.png)

ユーザーが `comments` テキストボックスを空のままにすると、サーバーに `NA` の値が送信されることを示す次の `console window` のイラストを参照してください。

![コンソールウィンドウでデータを送信](/help/forms/assets/custom-function-submit-data-form.png)

また、コンソールウィンドウを調べて、サーバーに送信されたデータを表示することもできます。

![ コンソール ウィンドウのデータを調べる](/help/forms/assets/custom-function-submit-data-console-data.png)

## フォーム送信の成功およびエラーハンドラーのオーバーライド

カスタム関数でフィールドおよびグローバルオブジェクトを使用して、`Contact Us` フォームを利用して送信ハンドラーを上書きする方法を説明します。

[create-custom-functionas](/help/forms/custom-function-core-component-create-function.md) の節で説明したように、次のコード行を追加して、フォーム送信の送信メッセージまたは失敗メッセージをカスタマイズし、フォーム送信メッセージをモーダルボックスに表示します。

```javascript
/**
 * Handles the success response after a form submission.
 *
 * @param {scope} globals - This object contains a read-only form instance, target field instance, triggered event, and methods for performing form modifications within custom functions.
 * @returns {void}
 */
function customSubmitSuccessHandler(globals) {
    var event = globals.event;
    var submitSuccessResponse = event.payload.body;
    var form = globals.form;

    if (submitSuccessResponse) {
        if (submitSuccessResponse.redirectUrl) {
            window.location.href = encodeURI(submitSuccessResponse.redirectUrl);
        } else if (submitSuccessResponse.thankYouMessage) {
            showModal("success", submitSuccessResponse.thankYouMessage);
        }
    }
}

/**
 * Handles the error response after a form submission.
 *
 * @param {string} customSubmitErrorMessage - The custom error message.
 * @param {scope} globals - This object contains a read-only form instance, target field instance, triggered event, and methods for performing form modifications within custom functions.
 * @returns {void}
 */
function customSubmitErrorHandler(customSubmitErrorMessage, globals) {
    showModal("error", customSubmitErrorMessage);
}
function showModal(type, message) {
    // Remove any existing modals
    var existingModal = document.getElementById("modal");
    if (existingModal) {
        existingModal.remove();
    }

    // Create the modal dialog
    var modal = document.createElement("div");
    modal.setAttribute("id", "modal");
    modal.setAttribute("class", "modal");

    // Create the modal content
    var modalContent = document.createElement("div");
    modalContent.setAttribute("class", "modal-content");

    // Create the modal header
    var modalHeader = document.createElement("div");
    modalHeader.setAttribute("class", "modal-header");
    modalHeader.innerHTML = "<h2>" + (type === "success" ? "Thank You" : "Error") + "</h2>";

    // Create the modal body
    var modalBody = document.createElement("div");
    modalBody.setAttribute("class", "modal-body");
    modalBody.innerHTML = "<p class='" + type + "-message'>" + message + "</p>";

    // Create the modal footer
    var modalFooter = document.createElement("div");
    modalFooter.setAttribute("class", "modal-footer");

    // Create the close button
    var closeButton = document.createElement("button");
    closeButton.setAttribute("class", "close-button");
    closeButton.innerHTML = "Close";
    closeButton.onclick = function() {
        modal.remove();
    };

    // Append the elements to the modal content
    modalFooter.appendChild(closeButton);
    modalContent.appendChild(modalHeader);
    modalContent.appendChild(modalBody);
    modalContent.appendChild(modalFooter);

    // Append the modal content to the modal
    modal.appendChild(modalContent);

    // Append the modal to the document body
    document.body.appendChild(modal);
}
```

この例では、ユーザーが `customSubmitSuccessHandler` 関数および `customSubmitErrorHandler` のカスタム関数を使用する場合、成功メッセージと失敗メッセージがモーダルに表示されます。 JavaScript関数 `showModal(type, message)` は、モーダルダイアログボックスを動的に作成して画面に表示するために使用されます。

次に、フォーム送信が成功するためのルールを作成します。

![ フォーム送信成功 ](/help/forms/assets/form-submission-success.png)

フォームが正常に送信されると成功メッセージがモーダルに表示されることを示すには、以下の図を参照してください。

![ フォーム送信成功メッセージ ](/help/forms/assets/form-submission-success-message.png)

同様に、失敗したフォーム送信に対するルールを作成します。

![ フォーム送信に失敗 ](/help/forms/assets/form-submission-fail.png)

フォームの送信に失敗したときにエラーメッセージがモーダルに表示されることを示すには、次の図を参照してください。

![ フォーム送信の失敗メッセージ ](/help/forms/assets/form-submission-fail-message.png)

フォーム送信の成功と失敗をデフォルトの方法で表示するには、`Default submit Form Success Handler` 関数と `Default submit Form Error Handler` 関数を標準で使用できます。

既存のAEM プロジェクトまたはフォームでカスタム送信ハンドラーが期待どおりに動作しない場合は、[ トラブルシューティング ](#troubleshooting) の節を参照してください。

## 繰り返し可能なパネルの特定のインスタンスでのアクションの実行

繰り返し可能なパネル上でビジュアルルールエディターを使用して作成されたルールは、繰り返し可能なパネルの最後のインスタンスに適用されます。 繰り返し可能なパネルの特定のインスタンスに対するルールを作成するには、カスタム関数を使用します。

目的地に向かう旅行者に関する情報を収集するた `Booking Form` に、別のフォームを作成しましょう。 旅行者パネルは、繰り返し可能なパネルとして追加され、ユーザーは「`Add Traveler`」ボタンを使用して 5 人の旅行者の詳細を追加できます。

![ 旅行者情報 ](/help/forms/assets/traveler-info-form.png)

[create-custom-function](/help/forms/custom-function-core-component-create-function.md) の節で説明したように、次のコード行を追加して、最後のコード行以外の繰り返し可能なパネルの特定のインスタンスでアクションを実行します。

```javascript
/**
* @name hidePanelInRepeatablePanel
* @param {scope} globals
*/
function hidePanelInRepeatablePanel(globals)
{    
    var repeatablePanel = globals.form.travelerinfo;
    // hides a panel inside second instance of repeatable panel
    globals.functions.setProperty(repeatablePanel[1].traveler, {visible : false});
}  
```

この例では、`hidePanelInRepeatablePanel` カスタム関数が繰り返し可能なパネルの特定のインスタンスでアクションを実行します。 上記コードの場合、`travelerinfo` は繰り返し可能なパネルを表します。 `repeatablePanel[1].traveler, {visible: false}` のコードは、繰り返し可能なパネルの 2 番目のインスタンスでパネルを非表示にします。

`Hide` というラベルの付いたボタンを追加し、繰り返し可能なパネルの 2 つ目のインスタンスを非表示にするルールを追加します。

![ パネルルールを非表示 ](/help/forms/assets/custom-function-hidepanel-rule.png)

次のビデオを参照して、`Hide` をクリックすると、2 番目の繰り返し可能インスタンス内のパネルが非表示になることを示します。

>[!VIDEO](https://video.tv.adobe.com/v/3429554?quality=12&learn=on)

## フォームの読み込み時に値をフィールドに事前入力

カスタム関数で、フィールドとグローバルオブジェクトを使用して、フ `Booking Form` ームを利用してフィールドに事前入力する方法を説明します。

[create-custom-function](/help/forms/custom-function-core-component-create-function.md) の節で説明したように、次のコード行を追加して、フォームの初期化時にフィールドに事前入力された値を読み込みます。

```javascript
/**
 * Tests import data
 * @name testImportData
 * @param {scope} globals
 */
function testImportData(globals)
{
    globals.functions.importData(Object.fromEntries([['amount','10000']]));
} 
```

上記のコードでは、フォームの読み込み時に、`testImportData` 関数が「`Booking Amount`」テキストフィールドの前に値を設定します。 予約フォームで、最小予約金額を `10,000` 定する必要があるとします。

次に、フォームの初期化時に、フォームの読み込み時に「`Booking Amount`」テキストフィールドの値に、指定した値が事前入力されるルールを作成します。

![ データ ルールのインポート ](/help/forms/assets/custom-function-import-data.png)

以下のスクリーンショットを参照してください。これは、フォームの読み込み時に、`Booking Amount` テキストボックスの値が指定した値で事前入力されることを示しています。

![ データ・ルール・フォームのインポート ](/help/forms/assets/custom-function-prefill-form.png)

## 特定のフィールドにフォーカスを設定する

カスタム関数で field オブジェクトと global オブジェクトを使用して、`Booking Form` を利用して特定のフィールドにフォーカスを設定する方法を説明します。

[create-custom-function](/help/forms/custom-function-core-component-create-function.md) の節で説明しているように、次のコード行を追加して、「`Submit`」ボタンがクリックされたときに指定されたフィールドにフォーカスを設定します。

```javascript
/**
 * @name testSetFocus
 * @param {object} emailField
 * @param {scope} globals
 */
    function testSetFocus(field, globals)
    {
        globals.functions.setFocus(field);
    }
```

`Submit` ボタンにルールを追加して、`Email ID` のテキストボックスがクリックされたときにフィールドにフォーカスを設定します。

![ フォーカスルールの設定 ](/help/forms/assets/custom-function-set-focus.png)

`Submit` ボタンがクリックされると、`Email ID` のフィールドにフォーカスが設定されることを示す、以下のスクリーンショットを参照してください。

![ フォーカスルールの設定 ](/help/forms/assets/custom-function-set-focus-form.png)

>[!NOTE]
>
> `email` フィールドを基準として次または前のフィールドにフォーカスする場合は、オプションの `$focusOption` パラメーターを使用できます。

## `dispatchEvent` プロパティを使用した繰り返し可能なパネルの追加または削除

カスタム関数で、フィールドおよびグローバルオブジェクトを使用して、`dispatchEvent` プロパティを利用し繰り返し可能なパネルを追加または削除する方法を `Booking Form` で説明します。

[create-custom-function](/help/forms/custom-function-core-component-create-function.md) の節で説明しているように、`dispatchEvent` プロパティを使用して「`Add Traveler`」ボタンがクリックされたときにパネルを追加するコードの行を追加します。

```javascript
/**
 * Tests add instance with dispatchEvent
 * @name testAddInstance
 * @param {scope} globals
 */
function testAddInstance(globals)
{
    var repeatablePanel = globals.form.traveler;
    globals.functions.dispatchEvent(repeatablePanel,'addInstance');
}
```

`Add Traveler` ボタンにルールを追加して、繰り返し可能なパネルをクリックして追加します。

![ パネルルールを追加 ](/help/forms/assets/custom-function-add-panel.png)

下の gif を参照してください。これは、「`Add Traveler`」ボタンがクリックされると、`dispatchEvent` プロパティを使用してパネルが追加されることを示しています。

![ パネルを追加 ](/help/forms/assets/custom-function-add-panel.gif)

同様に、「[create-custom-function](#create-custom-function)」の節で説明しているように、`dispatchEvent` プロパティを使用して `Delete Traveler` ボタンがクリックされたときにパネルを削除するコード行を追加します。

```javascript
/**
 
 * @name testRemoveInstance
 * @param {scope} globals
 */
function testRemoveInstance(globals)
{
    var repeatablePanel = globals.form.traveler;
    globals.functions.dispatchEvent(repeatablePanel, 'removeInstance');
} 
```

繰り返し可能なパネルをクリックして削除するルールを「`Delete Traveler`」ボタンに追加しましょう。

![ パネルルールを削除 ](/help/forms/assets/custom-function-delete-panel.png)

下の gif を参照してください。これは、「`Delete Traveler`」ボタンがクリックされると、`dispatchEvent` プロパティを使用してトラベラーパネルが削除されることを示しています。

![ パネルを削除 ](/help/forms/assets/custom-function-delete-panel.gif)

## 既知の問題

* カスタム関数は、JavaScriptの正規表現リテラルをサポートしていません。 カスタム関数で正規表現リテラルを使用すると、実行中にエラーが発生します。 例：
  `const pattern = /^abc$/;`

  互換性を確保するには、カスタム関数で RegExp コンストラクターを使用します。

  `const pattern = new RegExp("^abc$");`
正規表現をリファクタリングして、RegExp コンストラクターを使用し、一貫性のある信頼性の高い実行を確保します。

## トラブルシューティング

* 既存のAEM プロジェクトまたはフォームでカスタム送信ハンドラーが期待どおりに動作しない場合は、次の手順を実行します。
   * [ コアコンポーネントのバージョンが 3.0.18 以降 ](https://github.com/adobe/aem-core-forms-components) に更新されていることを確認します。 ただし、既存のAEM プロジェクトおよびフォームの場合は、さらに次の手順に従う必要があります。

   * AEM プロジェクトの場合、`submitForm('custom:submitSuccess', 'custom:submitError')` のすべてのインスタンスを `submitForm()` に置き換え、Cloud Manager パイプラインを通じてプロジェクトをデプロイする必要があります。

   * 既存のフォームについて、カスタム送信ハンドラーが正しく機能していない場合は、ユーザーはルールエディターを使用して「**送信**」ボタンの `submitForm` ルールを開いて保存する必要があります。このアクションは、フォーム内の既存のルールを `submitForm('custom:submitSuccess', 'custom:submitError')` から `submitForm()` に置き換えます。

## 関連トピック

{{see-also-rule-editor}}
