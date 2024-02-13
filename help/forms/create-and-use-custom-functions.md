---
title: アダプティブフォームでのカスタム関数の作成と追加
description: AEM Formsは、ユーザーがルールエディター内で独自の関数を作成して使用できるカスタム関数をサポートしています。
keywords: カスタム関数の追加、カスタム関数の使用、カスタム関数の作成、ルールエディターでのカスタム関数の使用を行います。
contentOwner: Ruchita Srivastav
content-type: reference
feature: Adaptive Forms, Core Components
source-git-commit: 94a290964a92f8c6ed353d9c77f3dd3b8a5598a4
workflow-type: tm+mt
source-wordcount: '778'
ht-degree: 21%

---


# アダプティブForms（コアコンポーネント）のカスタム関数

## はじめに

AEM Formsはカスタム関数をサポートし、複雑なビジネスルールを実装するための JavaScript 関数を定義できます。 これらのカスタム関数は、入力されたデータを指定された要件を満たすように操作および処理することで、フォームの機能を拡張します。 また、事前定義された条件に基づいて、フォームの動作を動的に変更することもできます。
アダプティブFormsでは、 [アダプティブフォームのルールエディター](/help/forms/rule-editor.md#custom-functions) をクリックして、フォームフィールドに対する特定の検証ルールを作成します。

ユーザーが電子メールアドレスを入力するカスタム機能の使用方法を理解し、入力した電子メールアドレスが特定の形式（「@」記号とドメイン名を含む）に従うようにしたい場合。 電子メールアドレスを入力として取り、有効な場合は true を返し、それ以外の場合は false を返す「ValidateEmail」というカスタム関数を作成します。

```javascript
function ValidateEmail(inputText)
{
    var email = /^\w+([\.-]?\w+)*@\w+([\.-]?\w+)*(\.\w{2,3})+$/;
    if(inputText.value.match(email))
        {
            alert("Valid email address!");
            return true;
        }
    else
    {
        alert("Invalid email address!");
        return false;
    }
}
```

上記の例では、ユーザーがフォームを送信しようとすると、カスタム関数「ValidateEmail」が呼び出され、入力された電子メールアドレスが有効かどうかが確認されます。

### カスタム関数の使用 {#uses-of-custom-function}

アダプティブFormsでカスタム関数を使用する利点の一部を次に示します。

* **データの操作**：カスタム関数は、フォームフィールドに入力されたデータを操作し、処理します。
* **データの検証**：カスタム関数を使用すると、フォーム入力に対してカスタムチェックを実行し、指定したエラーメッセージを指定できます。
* **動的動作**：カスタム関数を使用すると、特定の条件に基づいてフォームの動的動作を制御できます。 例えば、フィールドの表示/非表示、フィールド値の変更、フォームロジックの動的な調整を行うことができます。
* **統合**：カスタム関数を使用して、外部の API やサービスと統合できます。 外部ソースからデータを取得したり、外部の Rest エンドポイントにデータを送信したり、外部イベントに基づいてカスタムアクションを実行したりするのに役立ちます。

## カスタム関数を作成する際の考慮事項 {#considerations}

ルールエディターにカスタム関数を一覧表示するには、次のいずれかの形式でカスタム関数を宣言します。

* **jsdoc コメント付きまたはなしの Function ステートメント**

カスタム関数は、 jsdoc コメントを付けても付けずにも作成できます。

```javascript
    function functionName(parameters) 
        {
            // code to be executed
        }
```

* **必須の jsdoc コメントを含む矢印関数**

矢印関数を作成する例を次に示します。

```javascript
    /**
    * test function
    * @name testFunction test function
    * @param {string} a some parameter description
    * @param {string} b another parameter description
    * @return {string}
    */
    testFunction = (a, b) => {
    return a + b;
    };
```

<!-- 
    * @param {string=} b another parameter description
      /** */
    testFunction1=(a) => (return a)
    /** */
    testFunction2 = a => a + 100;-->

* **必須の jsdoc コメントを含む関数式**

次の形式でカスタム関数を作成し、アダプティブフォームのルールエディターに一覧表示します。 次に例を示します。

```javascript
    /**
    * test function
    * @name testFunction test function
    * @param {string} input1 parameter description
    * @param {string} input2 another parameter description
    * @return {string}
    */
    testFunction = function(input1,input2)
        {
            // code to be executed
        }
```

<!--
* @param {string=} input2 another parameter description
The functions that are not supported in the custom function list are:
* Generator functions
* Async/Await functions 
* Method definitions
* Class methods
* Default parameters
* Rest parameters -->

>[!NOTE]
>
> 次の項目を確認できます。 `error.log` ファイル内にカスタム関数などのエラーが発生した場合、ルールエディターに表示されない問題を修正しました。

<!--The `error.log` file also displays the methods and parameters that are not supported for custom functions. -->


## カスタム関数の作成 {#create-custom-function}

クライアントライブラリを作成し、ルールエディターでカスタム関数を呼び出します。 詳しくは、「[クライアント側ライブラリの使用](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/developing/full-stack/clientlibs.html?lang=ja#developing)」を参照してください。

カスタム関数を作成する手順は次のとおりです。
1. [クライアントライブラリの作成](#create-client-library)
1. [アダプティブフォームにクライアントライブラリを追加する](#use-custom-function)

### クライアントライブラリの作成 {#create-client-library}

クライアントライブラリを追加することで、カスタム関数を追加できます。 クライアントライブラリを作成するには、次の手順を実行します。

1. [AEM Forms as a Cloud Service リポジトリを複製](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/onboarding/journey/developers.html?lang=jp#accessing-git).
1. の下にフォルダーを作成します。 `[AEM Forms as a Cloud Service repository folder]/apps/` フォルダー。 例えば、という名前のフォルダーを作成します。 `experience-league`
1. に移動します。 `[AEM Forms as a Cloud Service repository folder]/apps/[AEM Project Folder]/experience-league/` をクリックし、 `ClientLibraryFolder` as `es6clientlibs`.
1. プロパティを追加する `categories`文字列タイプの値を次に設定： `es6customfunctions` から `es6clientlibs` フォルダー。

   >[!NOTE]
   >
   >`es6customfunctions`はカテゴリの例です。カテゴリには任意の名前を選択できます。

1. `js` という名前のフォルダーを作成します。
1. `[AEM Forms as a Cloud Service repository folder]/apps/[AEM Project Folder]/es6clientlibs/js` フォルダーに移動します。
1. JavaScript ファイル（例：`function.js`）を追加します。このファイルは、カスタム関数のコードで構成されます。

   >[!NOTE]
   >
   >* カスタム関数のコードを含む JavaScript ファイルにエラーがある場合、そのカスタム関数はアダプティブフォームのルールエディターに表示されません。 また、 `error.log` ファイルにエラーが含まれています。

   <!-- 
    >* AEM Adaptive Form supports the caching of custom functions. If the JavaScript is modified, the caching becomes invalidated, and it is parsed. You can see a message as `Fetched following custom functions list from cache` in the `error.log` file.  -->

1. `function.js` ファイルを保存します。
1. `[AEM Forms as a Cloud Service repository folder]/apps/[AEM Project Folder]/es6clientlibs/js` フォルダーに移動します。
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

1. [パイプラインを実行します。](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/onboarding/journey/developers.html?lang=ja#setup-pipeline)

パイプラインが正常に実行されると、クライアントライブラリに追加されたカスタム関数が [アダプティブフォームのルールエディター](/help/forms/rule-editor.md).

### アダプティブフォームにクライアントライブラリを追加する{#use-custom-function}

クライアントライブラリを追加した後、アダプティブフォーム内で使用します。 これにより、 [フォーム内のルールとしてのカスタム関数](/help/forms/rule-editor.md#custom-functions). アダプティブフォームにクライアントライブラリを追加するには、次の手順を実行します。

1. フォームを編集モードで開きます。
フォームを編集モードで開くには、フォームを選択し、「**[!UICONTROL 開く]**」を選択します。
1. 編集モードで、コンポーネントを選択し、![field-level](assets/select_parent_icon.svg)／**[!UICONTROL アダプティブフォームコンテナ]**、![cmppr](assets/configure-icon.svg) の順にクリックします。
1. サイドバーの「クライアントライブラリの名前」の下から、クライアントライブラリを追加します。（この例では、「`es6customfunctions`」）。

   ![カスタム関数をクライアントライブラリを追加する](/help/forms/assets/clientlib-custom-function.png)

ルールエディターでカスタム関数を使用するルールを作成します。

<!--

### Support for the optional parameters in custom functions{#support-for-optional-parameter}

AEM supports including optional parameters in JSDocs. These parameters are displayed as optional in the rule editor. There are two ways to add optional parameters in JSDocs:
*  `@param {string=abc} b -- some description for b which is optional`

    In the above line of code, `b` is an optional parameter with the default value set to `abc`. 
    Alternatively, you can define `b` as an optional parameter without assigning any default value as `@param {string=} b -- some description for b which is optional`

* `@param {array} [z=[def,xyz]] - - some description for z which is optional`

    In the above line of code, `z` is an optional parameter of array type with the default value set to `[def , xyz]`. 
    Alternatively, you can define `z` as an optional parameter without assigning any default value as `@param {array} [z=] - - some description for z which is optional`

>[!NOTE]
>
> Ensure that the parameter name is enclosed in square brackets [] and the parameter type is enclosed in curly brackets {}. 

To learn more about how to define optional parameters in JSDocs, [click here](https://jsdoc.app/tags-param).

In the rule editor of an Adaptive Form, the parameters are displayed as `required`. By default the parameters are `required`, if not defined as optional in JSDocs.

  ![Optional or required parameters](/help/forms/assets/optional-default-params.png) 

  You can save the rule without specifying a value for required parameters, but the rule is not executed and displays a warning message as:

  ![incomplete rule warning message](/help/forms/assets/incomplete-rule.png) 
  
  The rule is executed even if you do not specify a value for optional parameters. Undefined values are passed for optional parameters on executing the rule.

  ### Support for field and globals objects in custom functions {#support-field-and-global-objects}

  needs to be discussed

  -->

## 関連トピック {#see-also}

{{see-also}}





