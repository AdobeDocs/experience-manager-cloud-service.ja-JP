---
title: アダプティブフォームでのカスタム関数の使用
description: AEM Formsはカスタム関数をサポートしており、ルールエディター内で独自の関数を作成および使用できます。
keywords: ルールエディターでカスタム関数を使用して、カスタム関数の追加、カスタム関数の使用、カスタム関数の作成をおこないます。
contentOwner: Ruchita Srivastav
content-type: reference
feature: Adaptive Forms, Core Components
exl-id: 24607dd1-2d65-480b-a831-9071e20c473d
role: User, Developer
source-git-commit: 747203ccd3c7e428e2afe27c56e47c3ec18699f6
workflow-type: tm+mt
source-wordcount: '1286'
ht-degree: 2%

---


# コアコンポーネントに基づくアダプティブフォームのカスタム関数の概要

| バージョン | 記事リンク |
| -------- | ---------------------------- |
| AEM 6.5 | [ここをクリックしてください](https://experienceleague.adobe.com/en/docs/experience-manager-65/content/forms/adaptive-forms-core-components/create-and-use-custom-functions) |
| AEM as a Cloud Service | この記事 |

AEM Formsはカスタム関数をサポートし、複雑なビジネスルールを実装するためのJavaScript関数を定義できます。 これらのカスタム関数は、入力されたデータの操作や処理を容易にし、指定された要件を満たすことで、フォームの機能を拡張します。 定義済みの条件に基づいてフォームの動作を動的に変更できます。 また、カスタム関数を使用すると、デベロッパーは、複雑な検証ロジックの適用、動的計算の実行、ユーザーの操作または事前に定義された条件に基づくフォーム要素の表示と動作の制御を行うこともできます。

>[!NOTE]
>
> 最新の機能を使用するには、[ コアコンポーネント ](https://github.com/adobe/aem-core-forms-components) が最新バージョンに設定されていることを確認してください。

## カスタム関数の使用 {#uses-of-custom-function}

アダプティブFormsでカスタム関数を使用するメリットは次のとおりです。
* **データの処理**：カスタム関数は、フォームフィールドに入力されたデータの処理に役立ちます。
* **データの検証**：カスタム関数を使用すると、フォームの入力に対してカスタムチェックを実行し、指定したエラーメッセージを提供できます。
* **動的な動作**：カスタム関数を使用すると、特定の条件に基づいてフォームの動的な動作を制御できます。 例えば、フィールドの表示/非表示、フィールド値の変更、フォームロジックの調整を動的に行うことができます。
* **統合**：カスタム関数を使用して外部の API やサービスと統合できます。 外部ソースからのデータの取得、外部 Rest エンドポイントへのデータの送信、外部イベントに基づくカスタムアクションの実行に役立ちます。

カスタム関数は基本的に、JavaScript ファイルに追加されるクライアントライブラリです。 カスタム関数を作成すると、ルールエディターで使用できるようになり、アダプティブフォーム内のユーザーが選択できるようになります。 カスタム関数は、ルールエディターのJavaScript アノテーションによって識別されます。

## カスタム関数でサポートされるJavaScript注釈 {#js-annotations}

JavaScript注釈は、JavaScript コードのメタデータを提供するために使用されます。 /**や@など、特定の記号で始まるコメントが含まれます。 注釈は、コード内の関数、変数、その他の要素に関する重要な情報を提供します。 アダプティブフォームは、カスタム関数に対して次のJavaScript注釈をサポートしています。

### 名前

この名前は、アダプティブフォームのルールエディターでカスタム関数を識別するために使用されます。 次の構文を使用して、カスタム関数に名前を付けます。

* `@name [functionName] <Function Name>`
* `@function [functionName] <Function Name>`
* `@func [functionName] <Function Name>`。
  `functionName` は、関数の名前です。 スペースは使用できません。
  `<Function Name>` は、アダプティブフォームのルールエディター内の関数の表示名です。
関数名が関数自体の名前と同じ場合は、構文から `[functionName]` を省略できます。

### パラメーター

パラメーターは、カスタム関数で使用される引数のリストです。 1 つの関数は、複数のパラメーターをサポートできます。 次の構文を使用して、カスタム関数でパラメーターを定義します。

* `@param {type} name <Parameter Description>`
* `@argument` `{type} name <Parameter Description>`
* `@arg` `{type}` `name <Parameter Description>`。
  `{type}` は、パラメータータイプを表します。  使用できるパラメーターのタイプは次のとおりです。

   * string：単一の文字列値を表します。
   * 数値：1 つの数値を表します。
   * ブール値：単一のブール値（true または false）を表します。
   * string[]：文字列値の配列を表します。
   * 数値 []：数値の配列を表します。
   * boolean[]: ブール値の配列を表します。
   * 日付：単一の日付値を表します。
   * date[]：日付値の配列を表します。
   * 配列：様々なタイプの値を含む汎用の配列を表します。
   * オブジェクト：値を直接渡す代わりに、カスタム関数に渡されるフォームオブジェクトを表します。
   * scope: globals オブジェクトを表します。このオブジェクトには、フォームインスタンス、ターゲットフィールドインスタンス、カスタム関数内でフォームの変更を実行するためのメソッドなどの読み取り専用変数が含まれています。 これはJavaScript注釈の最後のパラメーターとして宣言され、アダプティブフォームのルールエディターには表示されません。 scope パラメーターは、フォームまたはコンポーネントのオブジェクトにアクセスして、フォームの処理に必要なルールまたはイベントをトリガーします。 Globals オブジェクトの詳細と使用方法については、[ ここをクリック ](/help/forms/custom-function-core-component-scope-function.md) してください。

パラメータータイプでは大文字と小文字が区別されず、パラメーター名にはスペースを使用できません。

パラメ `<Parameter Description>` ターの目的に関する詳細が含まれています。 複数の単語を含めることができます。

#### オプションパラメーター

デフォルトでは、すべてのパラメーターが必須です。 パラメーターをオプションとして定義するには、パラメータータイプの後に `=` を追加するか、`[]` でパラメーター名を囲みます。 JavaScript アノテーションでオプションとして定義されたパラメーターは、ルールエディターでオプションとして表示されます。
変数をオプションのパラメーターとして定義するには、次の構文のいずれかを使用します。

* `@param {type=} Input1`

上記のコード行では、`Input1` はオプションのパラメーターで、デフォルト値はありません。 デフォルト値を使用してオプションのパラメーターを宣言するには：
`@param {string=<value>} input1`

デフォルト値を `value` に設定したオプションのパラメーターとして `input1` を指定します。

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

![ オプションまたは必須のパラメーター ](/help/forms/assets/optional-default-params.png)

必須パラメーターの値を指定せずにルールを保存できますが、ルールは実行されず、次のような警告メッセージが表示されます。

![ 不完全なルールの警告 ](/help/forms/assets/incomplete-rule.png)

ユーザーがオプションパラメーターを空のままにすると、「未定義」の値がオプションパラメーターのカスタム関数に渡されます。

JSDocs でオプション パラメータを定義する方法の詳細については、[ ここをクリック ](https://jsdoc.app/tags-param) してください。

### 戻り値タイプ

戻り値のタイプは、実行後にカスタム関数が返す値のタイプを指定します。 次の構文を使用して、カスタム関数で戻り値のタイプを定義します。

* `@return {type}`
* `@returns {type}`
  `{type}` は、関数の戻り値のタイプを表します。 使用できる戻り値のタイプは次のとおりです。
   * string：単一の文字列値を表します。
   * 数値：1 つの数値を表します。
   * ブール値：単一のブール値（true または false）を表します。
   * string[]：文字列値の配列を表します。
   * 数値 []：数値の配列を表します。
   * boolean[]: ブール値の配列を表します。
   * 日付：単一の日付値を表します。
   * date[]：日付値の配列を表します。
   * 配列：様々なタイプの値を含む汎用の配列を表します。
   * object：値を直接表すのではなく、フォームオブジェクトを表します。

  戻り値のタイプでは、大文字と小文字が区別されません。

### 非公開

プライベートとして宣言されたカスタム関数は、アダプティブフォームのルールエディターのカスタム関数のリストに表示されません。 デフォルトでは、カスタム関数はパブリックです。 カスタム関数をプライベートとして宣言する構文は `@private` です。


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

ユーザーがカスタム関数にJavaScript アノテーションを追加しない場合は、関数名によってルールエディターに表示されます。 ただし、カスタム関数を読みやすくするために、JavaScript アノテーションを含めることをお勧めします。

### 必須のJavaScript注釈またはコメントを含む矢印関数

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

ユーザーがカスタム関数にJavaScript注釈を追加しない場合、カスタム関数はアダプティブフォームのルールエディターに表示されません。

### 必須のJavaScript注釈またはコメントを含む関数式

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

ユーザーがカスタム関数にJavaScript注釈を追加しない場合、カスタム関数はアダプティブフォームのルールエディターに表示されません。

## 次の手順

アダプティブフォームでカスタム関数を作成および使用するには、[ コアコンポーネントに基づくアダプティブフォームのカスタム関数の作成 ](/help/forms/custom-function-core-component-create-function.md) の記事を参照してください。

## 関連トピック

{{see-also-rule-editor}}