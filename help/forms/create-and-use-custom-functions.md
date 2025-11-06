---
title: アダプティブフォームでのカスタム関数の使用
description: AEM Formsはカスタム関数をサポートしており、ルールエディター内で独自の関数を作成および使用できます。
keywords: カスタム関数の追加, カスタム関数の使用, カスタム関数の作成, ルールエディターでのカスタム関数の使用.
contentOwner: Ruchita Srivastav
content-type: reference
feature: Adaptive Forms, Core Components
exl-id: 24607dd1-2d65-480b-a831-9071e20c473d
role: User, Developer
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '1336'
ht-degree: 53%

---


# コアコンポーネントに基づくアダプティブフォームのカスタム関数の概要

| バージョン | 記事リンク |
| -------- | ---------------------------- |
| AEM 6.5 | [ここをクリックしてください](https://experienceleague.adobe.com/en/docs/experience-manager-65/content/forms/adaptive-forms-core-components/create-and-use-custom-functions-core-components) |
| AEM as a Cloud Service | この記事 |

AEM Formsはカスタム関数をサポートし、複雑なビジネスルールを実装するためのJavaScript関数を定義できます。 これらのカスタム関数は、入力されたデータの操作や処理を容易にし、指定された要件を満たすことで、フォームの機能を拡張します。 定義済みの条件に基づいてフォームの動作を動的に変更できます。 また、カスタム関数を使用すると、デベロッパーは、複雑な検証ロジックの適用、動的計算の実行、ユーザーの操作または事前に定義された条件に基づくフォーム要素の表示と動作の制御を行うこともできます。

>[!NOTE]
>
> 最新の機能を使用するには、[&#x200B; コアコンポーネント &#x200B;](https://github.com/adobe/aem-core-forms-components) が最新バージョンに設定されていることを確認してください。

## カスタム関数の使用 {#uses-of-custom-function}

アダプティブフォームでカスタム関数を使用すると、次のようなメリットがあります。

* **データの処理**：カスタム関数は、フォームフィールドに対するエントリ済みデータの処理に役立ちます。
* **データの検証**：カスタム関数を使用すると、フォームの入力に対してカスタムチェックを実行し、指定したエラーメッセージを提供できます。
* **動的な動作**：カスタム関数を使用すると、特定の条件に基づいてフォームの動的な動作を制御できます。例えば、フィールドの表示／非表示、フィールド値の変更、フォームロジックの調整を動的に行うことができます。
* **統合**：カスタム関数を使用して、外部 API またはサービスと統合できます。外部ソースからのデータの取得、外部 Rest エンドポイントへのデータの送信、外部イベントに基づくカスタムアクションの実行に役立ちます。

カスタム関数は、基本的に JavaScript ファイルに追加されるクライアントライブラリです。カスタム関数を作成すると、ルールエディターで使用できるようになり、アダプティブフォーム内のユーザーが選択できるようになります。 カスタム関数は、ルールエディターの JavaScript 注釈によって識別されます。

## カスタム関数でサポートされる JavaScript 注釈 {#js-annotations}

JavaScript注釈は、JavaScript コードのメタデータを提供するために使用されます。 /**や@など、特定の記号で始まるコメントが含まれます。 注釈は、コード内の関数、変数、その他の要素に関する重要な情報を提供します。アダプティブフォームは、カスタム関数に対して次の JavaScript 注釈をサポートしています。

### 名前

この名前は、アダプティブフォームのルールエディターでカスタム関数を識別するために使用されます。 次の構文を使用して、カスタム関数に名前を付けます。

* `@name [functionName] <Function Name>`
* `@function [functionName] <Function Name>`
* `@func [functionName] <Function Name>`。
  `functionName` は関数の名前です。スペースは使用できません。
  `<Function Name>` は、アダプティブフォームのルールエディター内の関数の表示名です。
関数名が関数自体の名前と同じ場合は、構文から `[functionName]` を省略できます。

### パラメーター

パラメーターは、カスタム関数で使用される引数のリストです。 関数は複数のパラメーターをサポートできます。カスタム関数のパラメーターを定義するには、次の構文を使用します。

* `@param {type} name <Parameter Description>`
* `@argument` `{type} name <Parameter Description>`
* `@arg` `{type}` `name <Parameter Description>`。
  `{type}` は、パラメータータイプを表します。  許可されているパラメータータイプは、以下のとおりです。

   * string：単一の文字列値を表します。
   * number：単一の数値を表します。
   * boolean：単一のブール値（true または false）を表します。
   * string[]：文字列値の配列を表します。
   * number[]：数値の配列を表します。
   * boolean[]：ブール値の配列を表します。
   * date：単一の日付値を表します。
   * date[]：日付値の配列を表します。
   * array：様々なタイプの値を含む汎用の配列を表します。
   * object：値を直接渡す代わりに、カスタム関数に渡されるフォームオブジェクトを表します。
   * scope: globals オブジェクトを表します。このオブジェクトには、フォームインスタンス、ターゲットフィールドインスタンス、カスタム関数内でフォームの変更を実行するためのメソッドなどの読み取り専用変数が含まれています。 これはJavaScript注釈の最後のパラメーターとして宣言され、アダプティブフォームのルールエディターには表示されません。 scope パラメーターは、フォームまたはコンポーネントのオブジェクトにアクセスして、フォームの処理に必要なルールまたはイベントをトリガーします。Globals オブジェクトの詳細と使用方法については、[&#x200B; ここをクリック &#x200B;](/help/forms/custom-function-core-component-scope-function.md) してください。

パラメータータイプでは大文字と小文字が区別されず、パラメーター名にはスペースを使用できません。

`<Parameter Description>` には、パラメーターの目的に関する詳細が含まれます。複数の単語を含めることができます。

#### オプションパラメーター

デフォルトでは、すべてのパラメーターが必須です。 パラメーターをオプションとして定義するには、パラメータータイプの後に `=` を追加するか、`[]` でパラメーター名を囲みます。 JavaScript アノテーションでオプションとして定義されたパラメーターは、ルールエディターでオプションとして表示されます。
変数をオプションのパラメーターとして定義するには、次の構文のいずれかを使用します。

* `@param {type=} Input1`

上記のコード行では、`Input1` はオプションのパラメーターで、デフォルト値はありません。 デフォルト値を使用してオプションのパラメーターを宣言するには：
`@param {string=<value>} input1`

デフォルト値を `input1` に設定したオプションのパラメーターとして `value` を指定します。

* `@param {type} [Input1]`

上記のコード行では、`Input1` はオプションのパラメーターで、デフォルト値はありません。 デフォルト値を使用してオプションのパラメーターを宣言するには：
`@param {array} [input1=<value>]`
`input1` は、デフォルト値が `value` に設定された配列型のオプションのパラメーターです。
パラメータ タイプが中括弧 {} で囲まれ、パラメータ名が角括弧で囲まれていることを確認してください。

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

ルールエディターで `OptionalParameterFunction` カスタム関数を使用した例を次に示します。

![&#x200B; オプションまたは必須のパラメーター &#x200B;](/help/forms/assets/optional-default-params.png)

必須パラメーターの値を指定せずにルールを保存できますが、ルールは実行されず、次のような警告メッセージが表示されます。

![&#x200B; 不完全なルールの警告 &#x200B;](/help/forms/assets/incomplete-rule.png)

ユーザーがオプションパラメーターを空のままにすると、「未定義」の値がオプションパラメーターのカスタム関数に渡されます。

JSDocs でオプション パラメータを定義する方法の詳細については、[&#x200B; ここをクリック &#x200B;](https://jsdoc.app/tags-param) してください。

### 戻り値のタイプ

戻り値のタイプは、カスタム関数が実行後に返す値のタイプを指定します。カスタム関数の戻り値のタイプを定義するには、次の構文を使用します。

* `@return {type}`
* `@returns {type}`
  `{type}` は、関数の戻り値のタイプを表します。許可されている戻り値のタイプは、以下のとおりです。
   * string：単一の文字列値を表します。
   * number：単一の数値を表します。
   * boolean：単一のブール値（true または false）を表します。
   * string[]：文字列値の配列を表します。
   * number[]：数値の配列を表します。
   * boolean[]：ブール値の配列を表します。
   * date：単一の日付値を表します。
   * date[]：日付値の配列を表します。
   * array：様々なタイプの値を含む汎用の配列を表します。
   * object：値を直接表す代わりに、フォームオブジェクトを表します。

  戻り値のタイプでは、大文字と小文字は区別されません。

### プライベート

プライベートとして宣言されたカスタム関数は、アダプティブフォームのルールエディターのカスタム関数のリストに表示されません。 デフォルトでは、カスタム関数はパブリックです。カスタム関数をプライベートとして宣言する構文は `@private` です。


## カスタム関数を作成する際のガイドライン

ルールエディターでカスタム関数をリストするには、次のいずれかの形式を使用できます。

### jsdoc コメントを含むまたは含まない関数ステートメント

jsdoc コメントを含むまたは含まないカスタム関数を作成できます。

```javascript
    function functionName(parameters) 
        {
            // code to be executed
        }
```

ユーザーがカスタム関数に JavaScript 注釈を追加しない場合は、ルールエディターに関数名でリストされます。ただし、カスタム関数の読みやすさを向上させるために、JavaScript 注釈を含めることをお勧めします。

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

ユーザーがカスタム関数に JavaScript 注釈を追加しない場合、カスタム関数はアダプティブフォームのルールエディターにリストされません。

### 必須の JavaScript 注釈またはコメントを含む関数式

アダプティブフォームのルールエディターにカスタム関数をリストするには、次の形式でカスタム関数を作成します。アダプティブフォームのルールエディターでカスタム関数をリストするには、次の形式でカスタム関数を作成します。

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

ユーザーがカスタム関数に JavaScript 注釈を追加しない場合、カスタム関数はアダプティブフォームのルールエディターにリストされません。

## 既知の問題

* カスタム関数は、JavaScriptの正規表現リテラルをサポートしていません。 カスタム関数で正規表現リテラルを使用すると、実行中にエラーが発生します。 例：
  `const pattern = /^abc$/;`

  互換性を確保するには、カスタム関数で RegExp コンストラクターを使用します。

  `const pattern = new RegExp("^abc$");`
正規表現をリファクタリングして、RegExp コンストラクターを使用し、一貫性のある信頼性の高い実行を確保します。

## 次の手順

アダプティブフォームでカスタム関数を作成および使用するには、[&#x200B; コアコンポーネントに基づくアダプティブフォームのカスタム関数の作成 &#x200B;](/help/forms/custom-function-core-component-create-function.md) の記事を参照してください。

## 関連トピック

{{see-also-rule-editor}}