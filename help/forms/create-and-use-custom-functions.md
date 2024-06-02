---
title: アダプティブフォームでのカスタム関数の作成と追加
description: AEM Formsはカスタム関数をサポートしており、ルールエディター内で独自の関数を作成および使用できます。
keywords: ルールエディターでカスタム関数を使用して、カスタム関数の追加、カスタム関数の使用、カスタム関数の作成をおこないます。
contentOwner: Ruchita Srivastav
content-type: reference
feature: Adaptive Forms, Core Components
mini-toc-levels: 4
exl-id: 24607dd1-2d65-480b-a831-9071e20c473d
source-git-commit: 8f33174ac6b699af34ca8af14387eaca5cae969c
workflow-type: tm+mt
source-wordcount: '3522'
ht-degree: 4%

---


<span class="preview"> この記事には次が含まれます `Override form submission success and error handlers` をプレリリース機能として使用できます。 プレリリース機能には、 [プレリリースチャネル](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/release-notes/prerelease.html?lang=ja#new-features).

# アダプティブForms（コアコンポーネント）のカスタム関数

| バージョン | 記事リンク |
| -------- | ---------------------------- |
| AEM 6.5 | [ここをクリックしてください](https://experienceleague.adobe.com/en/docs/experience-manager-65/content/forms/adaptive-forms-core-components/create-and-use-custom-functions) |
| AEM as a Cloud Service | この記事 |

## はじめに

AEM Formsでは、複雑なビジネスルールを実装するための JavaScript 関数を定義できるカスタム関数をサポートしています。 これらのカスタム関数は、入力されたデータの操作や処理を容易にし、指定された要件を満たすことで、フォームの機能を拡張します。 定義済みの条件に基づいてフォームの動作を動的に変更することもできます。

>[!NOTE]
>
> 必ずを [コアコンポーネント](https://github.com/adobe/aem-core-forms-components) は、最新の機能を使用するために最新バージョンに設定されています。

### カスタム関数の使用 {#uses-of-custom-function}

アダプティブFormsでカスタム関数を使用するメリットは次のとおりです。
* **データの処理**：カスタム関数は、フォームフィールドに入力されたデータの処理に役立ちます。
* **データの検証**：カスタム関数を使用すると、フォームの入力に対してカスタムチェックを実行し、指定したエラーメッセージを提供できます。
* **動的動作**：カスタム関数を使用すると、特定の条件に基づいてフォームの動的な動作を制御できます。 例えば、フィールドの表示/非表示、フィールド値の変更、フォームロジックの調整を動的に行うことができます。
* **統合**：カスタム関数を使用して外部の API やサービスと統合できます。 外部ソースからのデータの取得、外部 Rest エンドポイントへのデータの送信、外部イベントに基づくカスタムアクションの実行に役立ちます。

カスタム関数は基本的に、JavaScript ファイルに追加されるクライアントライブラリです。 カスタム関数を作成すると、ルールエディターで使用できるようになり、アダプティブフォーム内のユーザーが選択できるようになります。 カスタム関数は、ルールエディターの JavaScript アノテーションによって識別されます。

### カスタム関数でサポートされる JavaScript 注釈 {#js-annotations}

JavaScript アノテーションは、JavaScript コードのメタデータを提供するために使用されます。 /**や@など、特定の記号で始まるコメントが含まれます。 注釈は、コード内の関数、変数、その他の要素に関する重要な情報を提供します。 アダプティブフォームは、カスタム関数に対して次の JavaScript 注釈をサポートしています。

#### 名前

この名前は、アダプティブフォームのルールエディターでカスタム関数を識別するために使用されます。 次の構文を使用して、カスタム関数に名前を付けます。

* `@name [functionName] <Function Name>`
* `@function [functionName] <Function Name>`
* `@func [functionName] <Function Name>`。
  `functionName` は、関数の名前です。 スペースは使用できません。
  `<Function Name>` は、アダプティブフォームのルールエディターにある関数の表示名です。
関数名が関数自体の名前と同じ場合は、を省略できます `[functionName]` 構文から変更します。

#### パラメーター

パラメーターは、カスタム関数で使用される引数のリストです。 1 つの関数は、複数のパラメーターをサポートできます。 次の構文を使用して、カスタム関数でパラメーターを定義します。

* `@param {type} name <Parameter Description>`
* `@argument` `{type} name <Parameter Description>`
* `@arg` `{type}` `name <Parameter Description>`.
  `{type}` は、パラメータータイプを表します。  使用できるパラメーターのタイプは次のとおりです。

   * string：単一の文字列値を表します。
   * 数値：1 つの数値を表します。
   * ブール値：単一のブール値（true または false）を表します。
   * string[]：文字列値の配列を表します。
   * 数値[]：数値の配列を表します。
   * ブール型[]：ブール値の配列を表します。
   * 日付：単一の日付値を表します。
   * 日付[]：日付値の配列を表します。
   * 配列：様々なタイプの値を含む汎用の配列を表します。
   * オブジェクト：値を直接渡す代わりに、カスタム関数に渡されるフォームオブジェクトを表します。
   * scope: globals オブジェクトを表します。このオブジェクトには、フォームインスタンス、ターゲットフィールドインスタンス、カスタム関数内でフォームの変更を実行するためのメソッドなどの読み取り専用変数が含まれています。 これは JavaScript 注釈の最後のパラメーターとして宣言され、アダプティブフォームのルールエディターには表示されません。 scope パラメーターは、フォームまたはコンポーネントのオブジェクトにアクセスして、フォームの処理に必要なルールまたはイベントをトリガーします。 Globals オブジェクトの詳細と使用方法については、を参照してください。 [ここをクリック](/help/forms/create-and-use-custom-functions.md#support-field-and-global-objects).

パラメータータイプでは大文字と小文字が区別されず、パラメーター名にはスペースを使用できません。

`<Parameter Description>` パラメーターの目的に関する詳細が含まれます。 複数の単語を含めることができます。

**オプションのパラメーター**
デフォルトでは、すべてのパラメーターが必須です。 次のいずれかを追加して、パラメーターをオプションとして定義できます `=` パラメーターの後にまたはを含むパラメーター名  `[]`. JavaScript 注釈でオプションとして定義されたパラメーターは、ルールエディターでオプションとして表示されます。
変数をオプションのパラメーターとして定義するには、次の構文のいずれかを使用します。

* `@param {type=} Input1`

上記のコード行では、 `Input1` は、デフォルト値を持たないオプションのパラメーターです。 デフォルト値を使用してオプションのパラメーターを宣言するには：
`@param {string=<value>} input1`

`input1` デフォルト値がに設定されたオプションパラメーターとして `value`.

* `@param {type} [Input1]`

上記のコード行では、 `Input1` は、デフォルト値を持たないオプションのパラメーターです。 デフォルト値を使用してオプションのパラメーターを宣言するには：
`@param {array} [input1=<value>]`
`input1` は、デフォルト値がに設定された配列型のオプションのパラメーターです `value`.
パラメータータイプが中括弧で囲まれていることを確認します {} また、パラメーター名は角括弧で囲まれています [].

次のコードスニペットについて考えてみます。input2 はオプションのパラメーターとして定義されています。

```javascript
        /**
         * optional parameter function
         * @name OptionalParameterFunction
         * @param {string} input1 
         * @param {string=} input2 
         * @return {string}
        */
        function OptionalParameterFunction(input1, input2) {
        let result = "Result: ";
        result += input1;
        if (input2 !== null) {
            result += " " + input2;
        }
        return result;
        }
```

次の図は、を使用した場合を示しています `OptionalParameterFunction` ルールエディターでのカスタム関数：

![オプションまたは必須のパラメーター ](/help/forms/assets/optional-default-params.png)

必須パラメーターの値を指定せずにルールを保存できますが、ルールは実行されず、次のような警告メッセージが表示されます。

![不完全なルールの警告](/help/forms/assets/incomplete-rule.png)

ユーザーがオプションパラメーターを空のままにすると、「未定義」の値がオプションパラメーターのカスタム関数に渡されます。

JSDocs でオプションのパラメータを定義する方法の詳細については、 [ここをクリック](https://jsdoc.app/tags-param).

#### 戻り値タイプ

戻り値のタイプは、実行後にカスタム関数が返す値のタイプを指定します。 次の構文を使用して、カスタム関数で戻り値のタイプを定義します。

* `@return {type}`
* `@returns {type}`
  `{type}` は、関数の戻り値のタイプを表します。 使用できる戻り値のタイプは次のとおりです。
   * string：単一の文字列値を表します。
   * 数値：1 つの数値を表します。
   * ブール値：単一のブール値（true または false）を表します。
   * string[]：文字列値の配列を表します。
   * 数値[]：数値の配列を表します。
   * ブール型[]：ブール値の配列を表します。
   * 日付：単一の日付値を表します。
   * 日付[]：日付値の配列を表します。
   * 配列：様々なタイプの値を含む汎用の配列を表します。
   * object：値を直接表すのではなく、フォームオブジェクトを表します。

  戻り値のタイプでは、大文字と小文字が区別されません。

#### 非公開

プライベートとして宣言されたカスタム関数は、アダプティブフォームのルールエディターのカスタム関数のリストに表示されません。 デフォルトでは、カスタム関数はパブリックです。 カスタム関数をプライベートとして宣言する構文を以下に示します。 `@private`.


## カスタム関数の作成時のガイドライン

ルールエディターにカスタム関数を一覧表示するには、次のいずれかの形式を使用できます。

### Jsdoc コメント付きまたは付きでない Function ステートメント

カスタム関数を作成する際に、jsdoc コメントを含めることも、含めないこともできます。

```javascript
    function functionName(parameters) 
        {
            // code to be executed
        }
```
ユーザーがカスタム関数に JavaScript 注釈を追加しない場合は、ルールエディターの関数名で表示されます。 ただし、カスタム関数を読みやすくするために、JavaScript 注釈を含めることをお勧めします。

### 必須の JavaScript 注釈またはコメントを含む矢印関数

矢印関数の構文を使用して、カスタム関数を作成できます。

```javascript
    /**
    * test function
    * @name testFunction 
    * @param {string} a parameter description
    * @param {string=} b parameter description
    * @return {string}
    */
    testFunction = (a, b) => {
    return a + b;
    };
    /** */
    testFunction1=(a) => (return a)
    /** */
    testFunction2 = a => a + 100;
    
```

ユーザーがカスタム関数に JavaScript 注釈を追加しない場合、カスタム関数はアダプティブフォームのルールエディターに表示されません。

### 必須の JavaScript 注釈またはコメントを含む関数式

アダプティブフォームのルールエディターにカスタム関数をリストするには、次の形式でカスタム関数を作成します。

```javascript
    /**
    * test function
    * @name testFunction 
    * @param {string} input1 parameter description
    * @param {string=} input2 parameter description
    * @return {string}
    */
    testFunction = function(input1,input2)
        {
            // code to be executed
        }
```

ユーザーがカスタム関数に JavaScript 注釈を追加しない場合、カスタム関数はアダプティブフォームのルールエディターに表示されません。

## カスタム関数の作成 {#create-custom-function}

ルールエディターでカスタム関数を呼び出すクライアントライブラリを作成します。 詳しくは、「[クライアント側ライブラリの使用](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/developing/full-stack/clientlibs.html?lang=ja#developing)」を参照してください。

カスタム関数の作成手順は次のとおりです。
1. [クライアントライブラリの作成](#create-client-library)
1. [アダプティブフォームへのクライアントライブラリの追加](#use-custom-function)

### クライアントライブラリの作成 {#create-client-library}

クライアントライブラリを追加することで、カスタム関数を追加できます。 クライアントライブラリを作成するには、次の手順を実行します。

1. [AEM Forms as a Cloud Service リポジトリを複製](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/onboarding/journey/developers.html?lang=jp#accessing-git).
1. `[AEM Forms as a Cloud Service repository folder]/apps/` フォルダーの下にフォルダーを作成します。例えば、`experience-league` という名前のフォルダーを作成します。
1. に移動します。 `[AEM Forms as a Cloud Service repository folder]/apps/[AEM Project Folder]/experience-league/` およびを作成 `ClientLibraryFolder`. 例えば、次のようにクライアントライブラリフォルダーを作成します `customclientlibs`.
1. プロパティを追加 `categories` 文字列タイプの値を使用。 例えば、の値を `customfunctionscategory` に `categories` のプロパティ `customclientlibs` フォルダー。

   >[!NOTE]
   >
   > には任意の名前を付けることができます `client library folder` および `categories` プロパティ。

1. `js` という名前のフォルダーを作成します。
1. `[AEM Forms as a Cloud Service repository folder]/apps/[AEM Project Folder]/customclientlibs/js` フォルダーに移動します。
1. JavaScript ファイル（例：`function.js`）を追加します。ファイルは、カスタム関数のコードを含みます。
1. `function.js` ファイルを保存します。
1. `[AEM Forms as a Cloud Service repository folder]/apps/[AEM Project Folder]/customclientlibs/js` フォルダーに移動します。
1. `js.txt` というテキストファイルを追加します。ファイルには次が含まれます。

   ```javascript
       #base=js
       functions.js
   ```

1. `js.txt` ファイルを保存します。
1. 次のコマンドを使用して、リポジトリに変更を追加、コミット、プッシュします。

   ```javascript
       git add .
       git commit -a -m "Adding custom functions"
       git push
   ```

1. [パイプラインを実行](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/onboarding/journey/developers.html?lang=ja#setup-pipeline) をクリックして、カスタム関数をデプロイします。

パイプラインが正常に実行されると、クライアントライブラリに追加されたカスタム関数を [アダプティブフォームのルールエディター](/help/forms/rule-editor-core-components.md).

### アダプティブフォームへのクライアントライブラリの追加{#use-custom-function}

クライアントライブラリをForms CS 環境にデプロイしたら、アダプティブフォームでその機能を使用します。 アダプティブフォームにクライアントライブラリを追加するには、次の手順に従います

1. フォームを編集モードで開きます。フォームを編集モードで開くには、フォームを選択し、以下を選択します。 **[!UICONTROL 編集]**.
1. コンテンツブラウザーを開き、アダプティブフォームの&#x200B;**[!UICONTROL ガイドコンテナ]**&#x200B;コンポーネントを選択します。
1. ガイドコンテナプロパティ ![ガイドプロパティ](/help/forms/assets/configure-icon.svg) アイコンをクリックします。アダプティブフォームコンテナダイアログボックスが開きます。
1. を開きます **[!UICONTROL 基本]** タブをクリックして、の名前を選択 **[!UICONTROL クライアントライブラリカテゴリ]** ドロップダウンリストから（この場合は、 `customfunctionscategory`）に設定します。

   ![カスタム関数をクライアントライブラリを追加する](/help/forms/assets/clientlib-custom-function.png)

   >[!NOTE]
   >
   > 内でコンマ区切りのリストを指定することで、複数のカテゴリを追加できます **[!UICONTROL クライアントライブラリカテゴリ]** フィールド。

1. 「**[!UICONTROL 完了]**」をクリックします。

カスタム関数は、 [アダプティブフォームのルールエディター](/help/forms/rule-editor-core-components.md) の使用 [JavaScript アノテーション](##js-annotations).

## アダプティブフォームでのカスタム関数の使用

アダプティブフォームでは、以下を使用できます [ルールエディター内のカスタム関数](/help/forms/rule-editor-core-components.md). 次のコードを JavaScript ファイル（`Function.js` ファイル）を選択し、生年月日（YYYY-MM-DD）に基づいて年齢を計算します。 カスタム関数を次のように作成 `calculateAge()` 生年月日を入力として、年齢を返します。

```javascript
    /**
        * Calculates Age
        * @name calculateAge
        * @param {object} field
        * @return {string} 
    */

    function calculateAge(field) {
    var dob = new Date(field);
    var now = new Date();

    var age = now.getFullYear() - dob.getFullYear();
    var monthDiff = now.getMonth() - dob.getMonth();

    if (monthDiff < 0 || (monthDiff === 0 && now.getDate() < dob.getDate())) {
    age--;
    }

    return age;
    }
```

上記の例では、ユーザーが誕生日を（YYYY-MM-DD）形式で入力した場合、カスタム関数は次のようになります `calculateAge` を呼び出し、年齢を返します。

![ルールエディター内の Agae カスタム関数の計算](/help/forms/assets/custom-function-calculate-age.png)

フォームをプレビューして、ルールエディターを介してカスタム関数がどのように実装されているかを確認します。

![ルールエディターフォームのプレビューでの Agae カスタム関数の計算](/help/forms/assets/custom-function-age-calculate-form.png)

>[!NOTE]
>
> 次を参照してください。 [カスタム関数](/help/forms/assets//customfunctions.zip) フォルダー。 次を使用して、このフォルダーをダウンロードし、AEM インスタンスにインストールします [パッケージマネージャー](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/implementing/developer-tools/package-manager).


### カスタム関数を使用したドロップダウンリストのオプションの設定

コアコンポーネントのルールエディターは、 **オプションを設定** 実行時にドロップダウンリストのオプションを設定するプロパティ。 ただし、カスタム関数を使用してドロップダウンリストのオプションを設定できます。

以下のコードを見て、カスタム関数を使用してドロップダウンリストのオプションを設定する方法を確認してください。

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

上記のコードでは、 `setEnums` を使用して、 `enum` プロパティと `setEnumNames` を使用して、 `enumNames` ドロップダウンのプロパティ。

のルールを作成しましょう `Next` ボタン。ユーザーがボタンをクリックしたときに、ドロップダウンリストのオプションの値を設定します。 `Next` ボタン：

![ドロップダウンリストのオプション](/help/forms/assets/drop-down-list-options.png)

「表示」ボタンをクリックしたときにドロップダウンリストのオプションが設定される場所を示すには、次の図を参照してください。

![ルールエディターのドロップダウンオプション](/help/forms/assets/drop-down-option-rule-editor.png)



### カスタム関数での非同期関数のサポート {#support-of-async-functions}

非同期カスタム関数がルールエディターリストに表示されない。 ただし、同期関数式を使用して作成されたカスタム関数内で、非同期関数を呼び出すことができます。

![Sync および async カスタム関数](/help/forms/assets/workflow-for-sync-async-custom-fumction.png)

>[!NOTE]
>
> カスタム関数で非同期関数を呼び出す利点は、非同期関数を使用すると、複数のタスクを同時に実行でき、カスタム関数内で各関数の結果を使用できる点です。

カスタム関数を使用して非同期関数を呼び出す方法については、以下のコードを参照してください。

```javascript
    
    async function asyncFunction() {
    const response = await fetch('https://petstore.swagger.io/v2/store/inventory');
    const data = await response.json();
    return data;
    }

    /**
    * callAsyncFunction
    * @name callAsyncFunction callAsyncFunction
    */
    function callAsyncFunction() {
    asyncFunction()
        .then(responseData => {
        console.log('Response data:', responseData);
        })
        .catch(error => {
         console.error('Error:', error);
    });
}
```

上記の例では、asyncFunction 関数は `asynchronous function`. 非同期操作を実行するには、 `GET` リクエスト先 `https://petstore.swagger.io/v2/store/inventory`. 次を使用して応答を待ちます `await`は、次を使用して応答本文を JSON として解析します `response.json()`データを返します。 この `callAsyncFunction` 関数は、を呼び出す同期カスタム関数です `asyncFunction` 関数を実行し、応答データをコンソールに表示します。 ただし、 `callAsyncFunction` 関数は同期で、非同期の asyncFunction 関数を呼び出し、その結果を `then` および `catch` ステートメント。

動作を確認するには、ボタンを追加し、ボタンクリック時に非同期関数を呼び出すボタンのルールを作成します。

![async 関数のルールを作成中](/help/forms/assets/rule-for-async-funct.png)

ユーザーがをクリックしたときの動作を示すには、以下のコンソールウィンドウの図を参照してください `Fetch` ボタン、カスタム関数 `callAsyncFunction` を呼び出し、非同期関数を呼び出す `asyncFunction`. コンソールウィンドウをInspectして、ボタンクリックに対する応答を表示します。

![コンソールウィンドウ](/help/forms/assets/async-custom-funct-console.png)

カスタム関数の機能について説明します。

## カスタム関数の様々な機能

カスタム関数を使用すると、パーソナライズされた機能をフォームに追加できます。 これらの関数は、特定フィールドの操作、グローバルフィールドの使用、キャッシュなど、様々な機能をサポートします。 この柔軟性により、組織の要件に応じてフォームをカスタマイズできます。

### カスタム関数のフィールド オブジェクトとグローバル スコープ オブジェクト {#support-field-and-global-objects}

フィールドオブジェクトは、テキストフィールド、チェックボックスなど、フォーム内の個々のコンポーネントまたは要素を参照します。 Globals オブジェクトには、フォームインスタンス、ターゲットフィールドインスタンス、カスタム関数内でフォームの変更を実行するメソッドなどの読み取り専用変数が含まれています。

>[!NOTE]
>
> この `param {scope} globals` が最後のパラメーターである必要があり、アダプティブフォームのルールエディターに表示されません。

<!-- Let us look at the following code snippet:

```JavaScript
   
    /**
    * updateDateTime
    * @name updateDateTime
    * @param {object} field
    * @param {scope} globals
    */
    function updateDateTime(field, globals) {
    // Accessing the Date object from the global scope
    var currentDate = new Date();
    // Formatting the date and time
    var formattedDateTime = currentDate.toLocaleString();
    // Updating the field value with the formatted date and time using setProperty.
    globals.functions.setProperty(field, {value: formattedDateTime});
    }
```

In the above code snippet, a custom function named `updateDateTime` takes parameters such as a field object and a global object. The field represents the textbox object where the formatted date and time value is displayed within the form. -->

カスタム関数でフィールドおよびグローバルオブジェクトを使用する方法を、 `Contact Us` 様々なユースケースを使用したフォーム

![お問い合わせフォーム](/help/forms/assets/contact-us-form.png)

#### ユースケース：SetProperty ルールを使用したパネルの表示

の説明に従って、カスタム関数に次のコードを追加します。 [create-custom-function](#create-custom-function) セクションで、フォームフィールドをに設定します `Required`.

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
> * にある使用可能なプロパティを使用して、フィールドのプロパティを設定できます。 `[form-path]/jcr:content/guideContainer.model.json`.
> * を使用してフォームに加えた変更 `setProperty` globals オブジェクトのメソッドは、本質的に非同期であり、カスタム関数の実行中には反映されません。

この例では、 `personaldetails` パネルは、ボタンをクリックすると発生します。 パネルでエラーが検出されなかった場合、別のパネルでは、 `feedback` ボタンをクリックするとパネルが表示されます。

のルールを作成しましょう `Next` ボタン。検証します。 `personaldetails` パネル化し、 `feedback`  ユーザーがクリックすると表示されるパネル `Next` ボタン。

![プロパティを設定](/help/forms/assets/custom-function-set-property.png)

次の図を参照して、各コンポーネントの配置場所を確認してください `personaldetails` パネルは、 `Next` ボタン。 内のすべてのフィールドに適用する場合 `personaldetails` が検証され、 `feedback` パネルが表示されます。

![プロパティのフォームプレビューを設定](/help/forms/assets/set-property-form-preview.png)

のフィールドにエラーがある場合 `personaldetails` パネルの場合、 `Next` ボタン、および `feedback` パネルは非表示のままになります。

![プロパティのフォームプレビューを設定](/help/forms/assets/set-property-panel.png)


#### ユースケース：フィールドを検証します。

の説明に従って、カスタム関数に次のコードを追加します。 [create-custom-function](#create-custom-function) セクションに移動し、フィールドを検証します。

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
> で引数が渡されない場合、 `validate()` 関数を使用すると、フォームを検証します。

この例では、カスタムの検証パターンが `contact` フィールド。 ユーザーは、で始まる電話番号を入力する必要があります `10` 続いて `8` 数字。 ユーザーがから始まらない電話番号を入力した場合 `10` 含まれる数が多い、または含まれない `8` 数字、ボタンをクリックすると検証エラーメッセージが表示されます。

![メールアドレスの検証パターン](/help/forms/assets/custom-function-validation-pattern.png)

次に、のルールを作成します `Next` を検証するボタン `contact` ボタンクリックのフィールド。

![検証パターン](/help/forms/assets/custom-function-validate.png)

次の図を参照して、ユーザーがで始まらない電話番号を入力した場合を示してください `10`すると、エラーメッセージがフィールドレベルに表示されます。

![メールアドレスの検証パターン](/help/forms/assets/custom-function-validate-error-message.png)

ユーザーが有効な電話番号と、そのすべてのフィールドをに入力した場合 `personaldetails` パネルが検証され、 `feedback` パネルが画面に表示されます。

![メールアドレスの検証パターン](/help/forms/assets/validate-form-preview-form.png)



#### ユースケース：パネルのリセット

の説明に従って、カスタム関数に次のコードを追加します。 [create-custom-function](#create-custom-function) セクションで、パネルをリセットします。

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
> で引数が渡されない場合、 `reset()` 関数を使用すると、フォームを検証します。

この例では、 `personaldetails` をクリックするとパネルがリセットされる `Clear` ボタン。 次に、のルールを作成します `Clear` ボタンをクリックしたときにパネルをリセットするボタン。

![「消去」ボタン](/help/forms/assets/custom-function-reset-field.png)

ユーザーがをクリックした場合に表示される方法については、次の図を参照してください `clear` ボタン、 `personaldetails` パネルのリセット：

![フォームをリセット](/help/forms/assets/custom-function-reset-form.png)



#### ユースケース：フィールドレベルでカスタムメッセージを表示し、フィールドを無効としてマークする

を使用できます `markFieldAsInvalid()` フィールドを無効として定義し、フィールドレベルでカスタムエラーメッセージを設定する関数。 この `fieldIdentifier` 値は `fieldId`、または `field qualifiedName`、または `field dataRef`. という名前のオブジェクトの値 `option` 次になることができます `{useId: true}`, `{useQualifiedName: true}`、または `{useDataRef: true}`.
フィールドを無効としてマークし、カスタムメッセージを設定するために使用される構文は次のとおりです。

* `globals.functions.markFieldAsInvalid(field.$id,"[custom message]",{useId: true});`
* `globals.functions.markFieldAsInvalid(field.$qualifiedName, "[custom message]", {useQualifiedName: true});`
* `globals.functions.markFieldAsInvalid(field.$dataRef, "[custom message]", {useDataRef: true});`

の説明に従って、カスタム関数に次のコードを追加します。 [create-custom-function](#create-custom-function) フィールドレベルでカスタムメッセージを有効にする場合は、「」をクリックします。

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

この例では、ユーザーがコメント テキストボックスに 15 文字未満で入力すると、カスタムメッセージがフィールドレベルに表示されます。

次に、のルールを作成します `comments` フィールド :

![フィールドを無効としてマーク](/help/forms/assets/custom-function-invalid-field.png)

で負のフィードバックを入力したことを表示するには、以下のデモを参照してください。 `comments` フィールドトリガー フィールドレベルでのカスタムメッセージの表示を設定します。

![フィールドを無効なプレビューフォームとしてマーク](/help/forms/assets/custom-function-invalidfield-form.png)

ユーザーが「コメント」テキストボックスに 15 文字を超えて入力すると、フィールドが検証され、フォームが送信されます。

![フィールドを有効なプレビューフォームとしてマーク](/help/forms/assets/custom-function-validfield-form.png)



#### ユースケース：変更されたデータのサーバーへの送信

次のコード行：
`globals.functions.submitForm(globals.functions.exportData(), false);` を使用して、操作後にフォームデータを送信します。
* 最初の引数は、送信するデータです。
* 2 番目の引数は、送信前にフォームを検証するかどうかを表します。 このプロパティは `optional` およびをに設定しました `true` デフォルトでは。
* 3 番目の引数は `contentType` 送信の（デフォルト値を使用する場合もオプション） `multipart/form-data`. その他の値は以下のとおりです。 `application/json` および `application/x-www-form-urlencoded`.

の説明に従って、カスタム関数に次のコードを追加します。 [create-custom-function](#create-custom-function) セクションで、サーバーで操作されたデータを送信するには：

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

この例では、ユーザーがを離れた場合、 `comments` テキストボックスが空、 `NA` は、フォームの送信時にサーバーに送信されます。

次に、のルールを作成します `Submit` データを送信するボタン：

![データを送信](/help/forms/assets/custom-function-submit-data.png)

の図を参照してください `console window` 以下に、ユーザーがを離れたかどうかを示します `comments` テキストボックスが空の場合、値は `NA` 次のサーバーで送信される：

![コンソールウィンドウでのデータの送信](/help/forms/assets/custom-function-submit-data-form.png)

また、コンソールウィンドウを調べて、サーバーに送信されたデータを表示することもできます。

![コンソールウィンドウでのInspect データ](/help/forms/assets/custom-function-submit-data-console-data.png)



#### ユースケース：フォーム送信の成功およびエラーハンドラーの上書き

で説明されているように、次のコード行を追加します。 [create-custom-function](#create-custom-function) セクションを使用して、フォーム送信の送信メッセージまたは失敗メッセージをカスタマイズし、フォーム送信メッセージをモーダルボックスに表示するには：

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

この例では、ユーザーがパラメーター `customSubmitSuccessHandler` および `customSubmitErrorHandler` カスタム関数の場合、成功メッセージと失敗メッセージはモーダルに表示されます。 JavaScript 関数 `showModal(type, message)` を使用すると、モーダルダイアログボックスを動的に作成し、画面に表示できます。

次に、フォーム送信が成功するためのルールを作成します。

![フォーム送信成功](/help/forms/assets/form-submission-success.png)

フォームが正常に送信されると成功メッセージがモーダルに表示されることを示すには、以下の図を参照してください。

![フォーム送信成功メッセージ](/help/forms/assets/form-submission-success-message.png)

同様に、失敗したフォーム送信に対するルールを作成します。

![フォーム送信の失敗](/help/forms/assets/form-submission-fail.png)

フォームの送信に失敗したときにエラーメッセージがモーダルに表示されることを示すには、次の図を参照してください。

![フォーム送信失敗メッセージ](/help/forms/assets/form-submission-fail-message.png)

フォーム送信の成功と失敗をデフォルトで表示するには、 `Default submit Form Success Handler` および `Default submit Form Error Handler` 関数は標準で使用できます。

既存のAEM プロジェクトまたはフォームでカスタム送信ハンドラーが期待どおりに動作しない場合は、を参照してください。 [トラブルシューティング](#troubleshooting) セクション。

<!--


#### Use Case:  Perform actions in a specific instance of the repeatable panel 

Rules created using the visual rule editor on a repeatable panel apply to the last instance of the repeatable panel. To write a rule for a specific instance of the repeatable panel, we can use a custom function.

Let's create a form to collect information about travelers heading to a destination. A traveler panel is added as a repeatable panel, where the user can add details for 5 travelers using the Add button.

Add the following line of code as explained in the [create-custom-function](#create-custom-function) section, to perform actions in a specific instance of the repeatable panel, other than the last one:

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
 
In this example, the `hidePanelInRepeatablePanel` custom function performs action in a specific instance of the repeatable panel. In the above code, `travelerinfo` represents the repeatable panel. The `repeatablePanel[1].traveler, {visible: false}` code hides the panel in the second instance of the repeatable panel. 
Let us add a button labeled `Hide` to add a rule to hide a specific panel.

![Hide Panel rule](/help/forms/assets/custom-function-hidepanel-rule.png)

Refer to the video below to demonstrate that when the `Hide` is clicked, the panel in the second repeatable instance hides:




#### **Usecase**: Pre-fill the field with a value when the form loads

Add the following line of code, as explained in the [create-custom-function](#create-custom-function) section, to load the pre-filled value in a field when the form is initialized:

```javascript
/**
 * @name importData
 * @param {scope} globals
 */
function importData(globals)
{
    globals.functions.importData(Object.fromEntries([['amount',200000]]));
} 
```

In the aforementioned code, the `importData` function updates the value in the `amount` textbox field when the form loads.

Let us create a rule for the `Submit` button, where the value in the `amount` textbox field changes to specified value when the form loads:

![Import Data Rule](/help/forms/assets/custom-function-import-data.png)

Refer to the screenshot below, which demonstrates that when the form loads, the value in the amount textbox is pre-filled with a specified value:

![Import Data Rule](/help/forms/assets/cg)



#### **Usecase**: Set focus on the specific field

Add the following line of code, as explained in the [create-custom-function](#create-custom-function) section, to set focus on the specified field when the `Submit` button is clicked.:

```javascript
/**
 * @name setFocus
 * @param {object} field
 * @param {scope} globals
 */
function setFocus(field, globals)
{
    globals.functions.setFocus(field);
}
```

Let us add a rule to the `Submit` button to set focus on the `email` field when it is clicked:

![Set Focus Rule](/help/forms/assets/custom-function-set-focus.png)

Refer to the screenshot below, which demonstrates that when the `Submit` button is clicked, the focus is set on the `email` field:

![Set Focus Rule](/help/forms/assets/custom-function-set-focus-form.png)

>[!NOTE]
>
> You can use the optional `$focusOption` parameter, if you want to focus on the next or previous field relative to the `email` field.

+++

+++ **Usecase**: Add or delete repeatable panel using the `dispatchEvent` property

Add the following line of code, as explained in the [create-custom-function](#create-custom-function) section, to add a panel when the `Add Traveler` button is clicked using the `dispatchEvent` property:

```javascript
/**
 
 * @name addInstance
 * @param {scope} globals
 */
function addInstance(globals)
{
    var repeatablePanel = globals.form.traveler;
    globals.functions.dispatchEvent(repeatablePanel, 'addInstance');
} 

```

Let us add a rule to the `Add Traveler` button to add the repeatable panel when it is clicked:

![Add Panel Rule](/help/forms/assets/custom-function-add-panel.png)

Refer to the screenshot below, which demonstrates that when the `Add Traveler` button is clicked, the traveler panel is added using the `dispatchEvent` property:

![Add Panel](/help/forms/assets/customg)

Similarly, add a button labeled `Delete Traveler` to delete a panel. Add the following line of code, as explained in the [create-custom-function](#create-custom-function) section, to delete a panel when the `Delete Traveler` button is clicked using the `dispatchEvent` property:

```javascript

/**
 
 * @name removeInstance
 * @param {scope} globals
 */
function removeInstance(globals)
{
    var repeatablePanel = globals.form.traveler;
    globals.functions.dispatchEvent(repeatablePanel, 'removeInstance');
} 

```
Let us add a rule to the `Delete Traveler` button to delete the repeatable panel when it is clicked:

![Delete Panel Rule](/help/forms/assets/custom-function-delete-panel.png)

Refer to the screenshot below, which demonstrates that when the `Delete Traveler` button is clicked, the traveler panel is deleted using the `dispatchEvent` property:

![Delete Panel](/help/forms/assets/customg)
-->

## カスタム関数のキャッシュサポート

アダプティブFormsは、カスタム関数のキャッシュを実装して、ルールエディターでカスタム関数のリストを取得する際の応答時間を短縮します。 メッセージ： `Fetched following custom functions list from cache` 次に表示： `error.log` ファイル。

![キャッシュをサポートするカスタム関数](/help/forms/assets/custom-function-cache-error.png)

カスタム関数が変更されると、キャッシュが無効化され、解析されます。

## トラブルシューティング {#troubleshooting}

* 既存のAEM プロジェクトまたはフォームでカスタム送信ハンドラーが期待どおりに実行できない場合は、次の手順を実行します。
   * 必ずを [コアコンポーネントのバージョンが 3.0.18 以降に更新されました](https://github.com/adobe/aem-core-forms-components). ただし、既存のAEM プロジェクトとフォームの場合は、さらに次の手順に従う必要があります。

   * AEM プロジェクトの場合、のインスタンスをすべて置き換える必要があります `submitForm('custom:submitSuccess', 'custom:submitError')` （を使用） `submitForm()` Cloud Manager パイプラインを通じてプロジェクトをデプロイします。

   * 既存のフォームで、カスタム送信ハンドラーが正しく機能しない場合は、を開いて保存する必要があります。 `submitForm` に関するルール **Submit** ルールエディターを使用してボタンをクリックします。 既存のルールを置き換えます。 `submitForm('custom:submitSuccess', 'custom:submitError')` （を使用） `submitForm()` フォームで。


* カスタム関数のコードを含んだ JavaScript ファイルにエラーがある場合、カスタム関数はアダプティブフォームのルールエディターに表示されません。 カスタム関数のリストを確認するには、に移動します。 `error.log` エラーのファイル。 エラーが発生すると、カスタム関数のリストは空で表示されます。

  ![エラーログファイル](/help/forms/assets/custom-function-list-error-file.png)

  エラーがない場合、カスタム関数が取得され、に表示されます。 `error.log` ファイル。 メッセージ： `Fetched following custom functions list` 次に表示： `error.log` ファイル：

  ![適切なカスタム関数を持つエラーログファイル](/help/forms/assets/custom-function-list-fetched-in-error.png)

## 考慮事項

* この `parameter type` および `return type` サポートしない `None`.

* カスタム関数リストでサポートされていない関数は次のとおりです。
   * ジェネレーター関数
   * 非同期/待機関数
   * メソッドの定義
   * クラスメソッド
   * デフォルトのパラメーター
   * REST パラメーター

## 関連トピック {#see-also}

{{see-also}}


