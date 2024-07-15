---
title: アダプティブフォームでのカスタム関数の作成と追加
description: AEM Formsはカスタム関数をサポートしており、ルールエディター内で独自の関数を作成および使用できます。
keywords: ルールエディターでカスタム関数を使用して、カスタム関数の追加、カスタム関数の使用、カスタム関数の作成をおこないます。
contentOwner: Ruchita Srivastav
content-type: reference
feature: Adaptive Forms, Core Components
exl-id: 24607dd1-2d65-480b-a831-9071e20c473d
role: User, Developer
source-git-commit: 52b87073cad84705b5dc0c6530aff44d1e686609
workflow-type: tm+mt
source-wordcount: '4333'
ht-degree: 4%

---


# アダプティブForms（コアコンポーネント）のカスタム関数

| バージョン | 記事リンク |
| -------- | ---------------------------- |
| AEM 6.5 | [ここをクリックしてください](https://experienceleague.adobe.com/en/docs/experience-manager-65/content/forms/adaptive-forms-core-components/create-and-use-custom-functions) |
| AEM as a Cloud Service | この記事 |

## はじめに

AEM Formsはカスタム関数をサポートし、複雑なビジネスルールを実装するためのJavaScript関数を定義できます。 これらのカスタム関数は、入力されたデータの操作や処理を容易にし、指定された要件を満たすことで、フォームの機能を拡張します。 定義済みの条件に基づいてフォームの動作を動的に変更することもできます。

>[!NOTE]
>
> 最新の機能を使用するには、[ コアコンポーネント ](https://github.com/adobe/aem-core-forms-components) が最新バージョンに設定されていることを確認してください。

### カスタム関数の使用 {#uses-of-custom-function}

アダプティブFormsでカスタム関数を使用するメリットは次のとおりです。
* **データの処理**：カスタム関数は、フォームフィールドに入力されたデータの処理に役立ちます。
* **データの検証**：カスタム関数を使用すると、フォームの入力に対してカスタムチェックを実行し、指定したエラーメッセージを提供できます。
* **動的な動作**：カスタム関数を使用すると、特定の条件に基づいてフォームの動的な動作を制御できます。 例えば、フィールドの表示/非表示、フィールド値の変更、フォームロジックの調整を動的に行うことができます。
* **統合**：カスタム関数を使用して外部の API やサービスと統合できます。 外部ソースからのデータの取得、外部 Rest エンドポイントへのデータの送信、外部イベントに基づくカスタムアクションの実行に役立ちます。

カスタム関数は基本的に、JavaScript ファイルに追加されるクライアントライブラリです。 カスタム関数を作成すると、ルールエディターで使用できるようになり、アダプティブフォーム内のユーザーが選択できるようになります。 カスタム関数は、ルールエディターのJavaScript アノテーションによって識別されます。

### カスタム関数でサポートされるJavaScript注釈 {#js-annotations}

JavaScript注釈は、JavaScript コードのメタデータを提供するために使用されます。 /**や@など、特定の記号で始まるコメントが含まれます。 注釈は、コード内の関数、変数、その他の要素に関する重要な情報を提供します。 アダプティブフォームは、カスタム関数に対して次のJavaScript注釈をサポートしています。

#### 名前

この名前は、アダプティブフォームのルールエディターでカスタム関数を識別するために使用されます。 次の構文を使用して、カスタム関数に名前を付けます。

* `@name [functionName] <Function Name>`
* `@function [functionName] <Function Name>`
* `@func [functionName] <Function Name>`。
  `functionName` は、関数の名前です。 スペースは使用できません。
  `<Function Name>` は、アダプティブフォームのルールエディター内の関数の表示名です。
関数名が関数自体の名前と同じ場合は、構文から `[functionName]` を省略できます。

#### パラメーター

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
   * scope: globals オブジェクトを表します。このオブジェクトには、フォームインスタンス、ターゲットフィールドインスタンス、カスタム関数内でフォームの変更を実行するためのメソッドなどの読み取り専用変数が含まれています。 これはJavaScript注釈の最後のパラメーターとして宣言され、アダプティブフォームのルールエディターには表示されません。 scope パラメーターは、フォームまたはコンポーネントのオブジェクトにアクセスして、フォームの処理に必要なルールまたはイベントをトリガーします。 Globals オブジェクトの詳細と使用方法については、[ ここをクリック ](/help/forms/create-and-use-custom-functions.md#support-field-and-global-objects) してください。

パラメータータイプでは大文字と小文字が区別されず、パラメーター名にはスペースを使用できません。

パラメ `<Parameter Description>` ターの目的に関する詳細が含まれています。 複数の単語を含めることができます。

**オプションのパラメーター**
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

#### 戻り値タイプ

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

#### 非公開

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

## カスタム関数の作成 {#create-custom-function}

ルールエディターでカスタム関数を呼び出すクライアントライブラリを作成します。 詳しくは、「[クライアント側ライブラリの使用](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/developing/full-stack/clientlibs.html?lang=ja#developing)」を参照してください。

カスタム関数の作成手順は次のとおりです。
1. [クライアントライブラリの作成](#create-client-library)
1. [アダプティブフォームへのクライアントライブラリの追加](#use-custom-function)


### カスタム関数を作成するための前提条件

アダプティブFormsへのカスタム関数の追加を開始する前に、次のことを確認してください。

**ソフトウェア：**

* **プレーンテキストエディター（IDE）**：任意のプレーンテキストエディターも使用できますが、Microsoft Visual Studio Code などの統合開発環境（IDE）は、編集を容易にする高度な機能を提供します。

* **Git:** このバージョン管理システムは、コードの変更を管理するために必要です。 インストールされていない場合は、https://git-scm.comからダウンロードします。

### クライアントライブラリの作成 {#create-client-library}

クライアントライブラリを追加することで、カスタム関数を追加できます。 クライアントライブラリを作成するには、次の手順を実行します。

**リポジトリのクローンを作成**

[AEM Formsas a Cloud Serviceリポジトリ ](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/onboarding/journey/developers.html?lang=jp#accessing-git) のクローン：

1. コマンドラインまたはターミナルウィンドウを開きます。

1. リポジトリを保存するマシン上の目的の場所に移動します。

1. 次のコマンドを実行して、リポジトリのクローンを作成します。

   `git clone [Git Repository URL]`

このコマンドは、リポジトリをダウンロードし、複製されたリポジトリのローカルフォルダーをコンピューターに作成します。 このガイド全体では、このフォルダーを [AEMaaCS プロジェクトディレクトリ ] と呼びます。

**クライアントライブラリフォルダーの追加**

[AEMaaCS プロジェクトディレクトリ ] に新しいクライアントライブラリフォルダーを追加するには、次の手順に従います。

1. [AEMaaCS プロジェクトディレクトリ ] をエディターで開きます。

   ![ カスタム関数のフォルダー構造 ](/help/forms/assets/custom-library-folder-structure.png)

1. `ui.apps` を見つけます。
1. 新規フォルダーを追加します。 例えば、`experience-league` というフォルダーを追加します。
1. フォルダー `/experience-league/` 移動し、`ClientLibraryFolder` を追加します。 例えば、`customclientlibs` という名前のクライアントライブラリフォルダーを作成します。

   `Location is: [AEMaaCS project directory]/ui.apps/src/main/content/jcr_root/apps/`

**クライアントライブラリフォルダーへのファイルとフォルダーの追加**

追加したクライアントライブラリフォルダーに次の内容を追加します。

* .content.xml ファイル
* js.txt ファイル
* js フォルダー

`Location is: [AEMaaCS project directory]/ui.apps/src/main/content/jcr_root/apps/experience-league/customclientlibs/`

1. `.content.xml` で次のコード行を追加します。

   ```javascript
   <?xml version="1.0" encoding="UTF-8"?>
   <jcr:root xmlns:cq="http://www.day.com/jcr/cq/1.0" xmlns:jcr="http://www.jcp.org/jcr/1.0"
   jcr:primaryType="cq:ClientLibraryFolder"
   categories="[customfunctionscategory]"/>
   ```

   >[!NOTE]
   >
   > `client library folder` および `categories` プロパティには、任意の名前を付けることができます。

1. `js.txt` で次のコード行を追加します。

   ```javascript
         #base=js
       function.js
   ```
1. `js` フォルダーに、Javascript ファイルをとして追加します。これには、カスタム関数が含まれ `function.js` います。

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
1. ファイルを保存します。

![ カスタム関数のフォルダー構造 ](/help/forms/assets/custom-function-added-files.png)

**新規フォルダーを filter.xml に含めます**:

1. [AEMaaCS プロジェクトディレクトリ]内の `/ui.apps/src/main/content/META-INF/vault/filter.xml` ファイルに移動します。

1. ファイルを開き、最後に次の行を追加します。

   `<filter root="/apps/experience-league" />`
1. ファイルを保存します。

![ カスタム関数フィルター xml](/help/forms/assets/custom-function-filterxml.png)

**新しく作成したクライアントライブラリフォルダーをAEM環境にデプロイします**。

AEM as a Cloud Service の [AEMaaCS プロジェクトディレクトリ]を Cloud Service 環境にデプロイします。Cloud Service 環境にデプロイするには：

1. 変更をコミットする

   1. 次のコマンドを使用して、リポジトリに変更を追加、コミット、プッシュします。

   ```javascript
       git add .
       git commit -a -m "Adding custom functions"
       git push
   ```

1. 更新されたコードをデプロイします。

   1. 既存のフルスタックパイプラインを使用してコードのデプロイメントをトリガーします。 これにより、更新されたコードが自動的にビルドおよびデプロイされます。

パイプラインをまだ設定していない場合は、[AEM Forms as a Cloud Service のパイプラインの設定方法](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/onboarding/journey/developers.html?lang=ja#setup-pipeline)のガイドを参照してください。

パイプラインが正常に実行されると、クライアントライブラリに追加されたカスタム関数が [ アダプティブフォームのルールエディター ](/help/forms/rule-editor-core-components.md) で使用できるようになります。

### アダプティブフォームへのクライアントライブラリの追加{#use-custom-function}

クライアントライブラリをForms CS 環境にデプロイしたら、アダプティブフォームでその機能を使用します。 アダプティブフォームにクライアントライブラリを追加するには、次の手順に従います

1. フォームを編集モードで開きます。フォームを編集モードで開くには、フォームを選択し、「**[!UICONTROL 編集]**」を選択します。
1. コンテンツブラウザーを開き、アダプティブフォームの&#x200B;**[!UICONTROL ガイドコンテナ]**&#x200B;コンポーネントを選択します。
1. ガイドコンテナプロパティ ![ガイドプロパティ](/help/forms/assets/configure-icon.svg) アイコンをクリックします。アダプティブフォームコンテナダイアログボックスが開きます。
1. 「**[!UICONTROL 基本]**」タブを開き、ドロップダウンリストから **[!UICONTROL クライアントライブラリカテゴリ]** の名前を選択します（この場合は「`customfunctionscategory`」を選択します）。

   ![カスタム関数をクライアントライブラリを追加する](/help/forms/assets/clientlib-custom-function.png)

   >[!NOTE]
   >
   > 「**[!UICONTROL クライアントライブラリカテゴリ]**」フィールドにコンマ区切りのリストを指定することで、複数のカテゴリを追加できます。

1. 「**[!UICONTROL 完了]**」をクリックします。

カスタム関数は、[JavaScript注釈 [ を使用して ](/help/forms/rule-editor-core-components.md) アダプティブフォームのルールエディター ](##js-annotations) で使用できます。

## アダプティブフォームでのカスタム関数の使用

アダプティブフォームでは、[ ルールエディター内のカスタム関数 ](/help/forms/rule-editor-core-components.md) を使用できます。 JavaScriptのファイル（`Function.js` ファイル）に次のコードを追加して、生年月日（YYYY-MM-DD）に基づいて年齢を計算しましょう。 生年月日を入力として取得し、年齢を返すカスタム関数を `calculateAge()` として作成します。

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

上記の例では、ユーザーが誕生日を（YYYY-MM-DD）形式で入力すると、カスタム関数 `calculateAge` が呼び出され、年齢が返されます。

![ ルールエディター内の Calcualte Agae カスタム関数 ](/help/forms/assets/custom-function-calculate-age.png)

フォームをプレビューして、ルールエディターを介してカスタム関数がどのように実装されているかを確認します。

![ ルールエディターフォームプレビューでの Agae カスタム関数の計算 ](/help/forms/assets/custom-function-age-calculate-form.png)

>[!NOTE]
>
> 次の [ カスタム関数 ](/help/forms/assets//customfunctions.zip) フォルダーを参照できます。 [ パッケージマネージャー ](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/implementing/developer-tools/package-manager) を使用して、このフォルダーをダウンロードし、AEM インスタンスにインストールします。


### カスタム関数を使用したドロップダウンリストのオプションの設定

コアコンポーネントのルールエディターが、実行時にドロップダウンリストのオプションを設定する **オプションを設定** プロパティをサポートしていません。 ただし、カスタム関数を使用してドロップダウンリストのオプションを設定できます。

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

上記のコードでは、`setEnums` を使用して `enum` プロパティを設定し、`setEnumNames` を使用してドロップダウンの `enumNames` プロパティを設定しています。

ユーザーが「`Next`」ボタンをクリックしたときにドロップダウンリストの値オプションを設定する「`Next`」ボタン用のルールを作成してみましょう。

![ ドロップダウンリストのオプション ](/help/forms/assets/drop-down-list-options.png)

「表示」ボタンをクリックしたときにドロップダウンリストのオプションが設定される場所を示すには、次の図を参照してください。

![ ルールエディターのドロップダウンオプション ](/help/forms/assets/drop-down-option-rule-editor.png)



### カスタム関数での非同期関数のサポート {#support-of-async-functions}

非同期カスタム関数がルールエディターリストに表示されない。 ただし、同期関数式を使用して作成されたカスタム関数内で、非同期関数を呼び出すことができます。

![Sync および async カスタム関数 ](/help/forms/assets/workflow-for-sync-async-custom-fumction.png)

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

上記の例では、asyncFunction 関数は `asynchronous function` です。 `https://petstore.swagger.io/v2/store/inventory` に対して `GET` リクエストを実行することで、非同期操作を実行します。 `await` を使用して応答を待ち、`response.json()` を使用して応答本文を JSON として解析し、データを返します。 `callAsyncFunction` 関数は、`asyncFunction` 関数を呼び出してコンソールに応答データを表示する同期カスタム関数です。 `callAsyncFunction` 関数は同期していますが、非同期の asyncFunction 関数を呼び出し、`then` 文と `catch` 文で結果を処理します。

動作を確認するには、ボタンを追加し、ボタンクリック時に非同期関数を呼び出すボタンのルールを作成します。

![async 関数のルールを作成しています ](/help/forms/assets/rule-for-async-funct.png)

ユーザーが「`Fetch`」ボタンをクリックすると、カスタム関数 `callAsyncFunction` が呼び出され、非同期関数 `asyncFunction` が呼び出されることを示すには、以下のコンソールウィンドウの図を参照してください。 コンソールウィンドウをInspectして、ボタンクリックに対する応答を表示します。

![ コンソールウィンドウ ](/help/forms/assets/async-custom-funct-console.png)

カスタム関数の機能について説明します。

## カスタム関数の様々な機能

カスタム関数を使用すると、パーソナライズされた機能をフォームに追加できます。 これらの関数は、特定フィールドの操作、グローバルフィールドの使用、キャッシュなど、様々な機能をサポートします。 この柔軟性により、組織の要件に応じてフォームをカスタマイズできます。

### カスタム関数のフィールド オブジェクトとグローバル スコープ オブジェクト {#support-field-and-global-objects}

フィールドオブジェクトは、テキストフィールド、チェックボックスなど、フォーム内の個々のコンポーネントまたは要素を参照します。 Globals オブジェクトには、フォームインスタンス、ターゲットフィールドインスタンス、カスタム関数内でフォームの変更を実行するメソッドなどの読み取り専用変数が含まれています。

>[!NOTE]
>
> `param {scope} globals` は最後のパラメーターである必要があり、アダプティブフォームのルールエディターには表示されません。

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

様々なユースケースを使用しながら、カスタム関数でフィールドおよびグローバルオブジェクトを `Contact Us` フォームでどのように使用するかを説明します。

![ お問い合わせフォーム ](/help/forms/assets/contact-us-form.png)

+++ **ユースケース**:`SetProperty` ルールを使用したパネルの表示

[create-custom-function](#create-custom-function) の節で説明したように、カスタム関数に次のコードを追加して、フォームフィールドを `Required` として設定します。

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
> * `[form-path]/jcr:content/guideContainer.model.json` にある使用可能なプロパティを使用して、フィールドのプロパティを設定できます。
> * Globals オブジェクトの `setProperty` メソッドを使用してフォームに加えられた変更は、本質的に非同期であり、カスタム関数の実行中には反映されません。

この例では、ボタンをクリックすると `personaldetails` パネルの検証が行われます。 パネルでエラーが検出されない場合は、ボタンをクリックすると、`feedback` のパネルが表示されます。

`Next` ボタンのルールを作成してみましょう。このルールは、`personaldetails` パネルを検証し、ユーザーが `Next` ボタンをクリックすると `feedback` パネルが表示されるようにします。

![プロパティを設定](/help/forms/assets/custom-function-set-property.png)

「`Next`」ボタンをクリックしたときに `personaldetails` パネルが検証される場所を示すには、以下の図を参照してください。 `personaldetails` ージ内のすべてのフィールドが検証されると、`feedback` のパネルが表示されます。

![ プロパティを設定フォームのプレビュー ](/help/forms/assets/set-property-form-preview.png)

`personaldetails` パネルのフィールドにエラーがある場合、エラーは「`Next`」ボタンをクリックするとフィールドレベルに表示され、`feedback` パネルは非表示のままになります。

![ プロパティを設定フォームのプレビュー ](/help/forms/assets/set-property-panel.png)

+++

+++ **ユースケース**：フィールドを検証します。

[create-custom-function](#create-custom-function) の節で説明したように、カスタム関数に次のコードを追加して、フィールドを検証します。

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
> `validate()` 関数で引数が渡されない場合は、フォームが検証されます。

この例では、「`contact`」フィールドにカスタムの検証パターンが適用されます。 ユーザーは、`10` で始まり、その後 `8` 桁が続く電話番号を入力する必要があります。 ユーザーが `10` で始まらない電話番号や、`8` 桁以下の電話番号を入力した場合、ボタンをクリックすると検証エラーメッセージが表示されます。

![ メールアドレスの検証パターン ](/help/forms/assets/custom-function-validation-pattern.png)

次の手順では、ボタンクリック時に `contact` フィールドを検証する `Next` ボタンのルールを作成します。

![ 検証パターン ](/help/forms/assets/custom-function-validate.png)

次の図を参照して、ユーザーが `10` で始まらない電話番号を入力した場合、フィールドレベルにエラーメッセージが表示されることを示してください。

![ メールアドレスの検証パターン ](/help/forms/assets/custom-function-validate-error-message.png)

ユーザーが有効な電話番号を入力し、`personaldetails` ントロールパネル内のすべてのフィールドが検証されると、`feedback` ントロールパネルが画面に表示されます。

![ メールアドレスの検証パターン ](/help/forms/assets/validate-form-preview-form.png)

+++

+++ **ユースケース**：パネルのリセット

[create-custom-function](#create-custom-function) の節で説明したように、カスタム関数に次のコードを追加して、パネルをリセットします。

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
> `reset()` 関数で引数が渡されない場合は、フォームが検証されます。

この例では、「`Clear`」ボタンをクリックすると、`personaldetails` パネルがリセットされます。 次の手順では、ボタンクリック時にパネルをリセットする `Clear` ボタンのルールを作成します。

![ 消去ボタン ](/help/forms/assets/custom-function-reset-field.png)

ユーザーが「`clear`」ボタンをクリックすると、`personaldetails` パネルがリセットされることを示す次の図を参照してください。

![ リセットフォーム ](/help/forms/assets/custom-function-reset-form.png)

+++

+++ **ユースケース**：フィールドレベルでカスタムメッセージを表示し、フィールドを無効としてマークする

`markFieldAsInvalid()` 関数を使用して、フィールドを無効として定義し、フィールドレベルでカスタムのエラーメッセージを設定できます。 `fieldIdentifier` の値は、`fieldId`、`field qualifiedName`、`field dataRef` のいずれかです。 `option` という名前のオブジェクトの値は、`{useId: true}`、`{useQualifiedName: true}`、`{useDataRef: true}` のいずれかです。
フィールドを無効としてマークし、カスタムメッセージを設定するために使用される構文は次のとおりです。

* `globals.functions.markFieldAsInvalid(field.$id,"[custom message]",{useId: true});`
* `globals.functions.markFieldAsInvalid(field.$qualifiedName, "[custom message]", {useQualifiedName: true});`
* `globals.functions.markFieldAsInvalid(field.$dataRef, "[custom message]", {useDataRef: true});`

[create-custom-function](#create-custom-function) の節で説明したように、カスタム関数に次のコードを追加して、フィールドレベルでカスタムメッセージを有効にします。

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

次に、`comments` フィールドのルールを作成します。

![ フィールドを無効としてマーク ](/help/forms/assets/custom-function-invalid-field.png)

`comments` のフィールドに負のフィードバックを入力すると、フィールドレベルでのカスタムメッセージの表示がトリガーされることを示す、以下のデモを参照してください。

![ フィールドを無効なプレビューフォームとしてマーク ](/help/forms/assets/custom-function-invalidfield-form.png)

ユーザーが「コメント」テキストボックスに 15 文字を超えて入力すると、フィールドが検証され、フォームが送信されます。

![ フィールドを有効なプレビューフォームとしてマーク ](/help/forms/assets/custom-function-validfield-form.png)

+++

+++ **ユースケース**：変更されたデータのサーバーへの送信

次のコード行：
`globals.functions.submitForm(globals.functions.exportData(), false);` は、操作後にフォームデータを送信するために使用されます。
* 最初の引数は、送信するデータです。
* 2 番目の引数は、送信前にフォームを検証するかどうかを表します。 このプロパティは `optional` であり、デフォルトでは `true` として設定されます。
* 3 番目の引数は送信 `contentType` です。デフォルト値を `multipart/form-data` にした場合もオプションとなります。 その他の値は、`application/json` と `application/x-www-form-urlencoded` です。

[create-custom-function](#create-custom-function) の節で説明したように、カスタム関数に次のコードを追加して、操作されたデータをサーバーで送信します。

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

この例では、ユーザーが `comments` テキストボックスを空のままにした場合、`NA` ータはフォームの送信時にサーバーに送信されます。

次に、データを送信する `Submit` ボタンのルールを作成します。

![ データの送信 ](/help/forms/assets/custom-function-submit-data.png)

ユーザーが `comments` テキストボックスを空のままにした場合、`NA` の値がサーバーで送信されることを示すには、以下の `console window` の図を参照してください。

![ コンソールウィンドウでのデータの送信 ](/help/forms/assets/custom-function-submit-data-form.png)

また、コンソールウィンドウを調べて、サーバーに送信されたデータを表示することもできます。

![ コンソール ウィンドウのInspect データ ](/help/forms/assets/custom-function-submit-data-console-data.png)

+++

+++ **ユースケース**：フォーム送信の成功およびエラーハンドラーの上書き

[create-custom-function](#create-custom-function) の節で説明したように、次のコード行を追加して、フォーム送信の送信メッセージまたは失敗メッセージをカスタマイズし、フォーム送信メッセージをモーダルボックスに表示します。

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

既存のAEM プロジェクトまたはフォームでカスタム送信ハンドラーが期待どおりに実行されない場合は、[ トラブルシューティング ](#troubleshooting) の節を参照してください。

+++

+++ **ユースケース**：繰り返し可能なパネルの特定のインスタンスでアクションを実行する

繰り返し可能なパネル上でビジュアルルールエディターを使用して作成されたルールは、繰り返し可能なパネルの最後のインスタンスに適用されます。 繰り返し可能なパネルの特定のインスタンスに対するルールを作成するには、カスタム関数を使用します。

宛先に向かう旅行者に関する情報を収集する別のフォームを作成しましょう。 旅行者パネルは、繰り返し可能なパネルとして追加され、ユーザーは「`Add Traveler`」ボタンを使用して 5 人の旅行者の詳細を追加できます。

![ 旅行者情報 ](/help/forms/assets/traveler-info-form.png)

[create-custom-function](#create-custom-function) の節で説明したように、次のコード行を追加して、最後のコード行以外の繰り返し可能なパネルの特定のインスタンスでアクションを実行します。

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

+++

+++ **ユースケース**：フォームの読み込み時に、フィールドに値を事前入力する

[create-custom-function](#create-custom-function) の節で説明したように、次のコード行を追加して、フォームの初期化時にフィールドに事前入力された値を読み込みます。

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

+++

+++ **ユースケース**：特定のフィールドにフォーカスを設定する

[create-custom-function](#create-custom-function) の節で説明しているように、次のコード行を追加して、「`Submit`」ボタンがクリックされたときに指定されたフィールドにフォーカスを設定します。

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

+++

+++ **ユースケース**:`dispatchEvent` プロパティを使用して、繰り返し可能なパネルを追加または削除する

[create-custom-function](#create-custom-function) の節で説明しているように、`dispatchEvent` プロパティを使用して「`Add Traveler`」ボタンがクリックされたときにパネルを追加するコードの行を追加します。

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

+++

## カスタム関数のキャッシュサポート

アダプティブFormsは、カスタム関数のキャッシュを実装して、ルールエディターでカスタム関数のリストを取得する際の応答時間を短縮します。 `error.log` ファイルに `Fetched following custom functions list from cache` のようなメッセージが表示されます。

![ キャッシュをサポートするカスタム関数 ](/help/forms/assets/custom-function-cache-error.png)

カスタム関数が変更されると、キャッシュが無効化され、解析されます。

## トラブルシューティング {#troubleshooting}

* 既存のAEM プロジェクトまたはフォームでカスタム送信ハンドラーが期待どおりに実行できない場合は、次の手順を実行します。
   * [ コアコンポーネントのバージョンが 3.0.18 以降 ](https://github.com/adobe/aem-core-forms-components) に更新されていることを確認します。 ただし、既存のAEM プロジェクトとフォームの場合は、さらに次の手順に従う必要があります。

   * AEM プロジェクトの場合、`submitForm('custom:submitSuccess', 'custom:submitError')` のすべてのインスタンスを `submitForm()` に置き換え、Cloud Manager パイプラインを通じてプロジェクトをデプロイする必要があります。

   * 既存のフォームで、カスタム送信ハンドラーが正しく機能しない場合は、ユーザーがルールエディターを使用して **送信** ボタンで `submitForm` ルールを開いて保存する必要があります。 この操作を実行すると、既存のルールが `submitForm('custom:submitSuccess', 'custom:submitError')` からフォーム内の `submitForm()` に置き換えられます。


* カスタム関数のコードを含んだJavaScript ファイルにエラーがある場合、カスタム関数はアダプティブフォームのルールエディターに表示されません。 カスタム関数のリストを確認するには、エラーの `error.log` ファイルに移動します。 エラーが発生すると、カスタム関数のリストは空で表示されます。

  ![ エラーログファイル ](/help/forms/assets/custom-function-list-error-file.png)

  エラーがない場合、カスタム関数が取得され、`error.log` ファイルに表示されます。 `error.log` ファイルに `Fetched following custom functions list` のようなメッセージが表示されます。

  ![ 適切なカスタム関数を持つエラーログファイル ](/help/forms/assets/custom-function-list-fetched-in-error.png)

## 考慮事項

* `parameter type` と `return type` は `None` をサポートしていません。

* カスタム関数リストでサポートされていない関数は次のとおりです。
   * ジェネレーター関数
   * 非同期/待機関数
   * メソッドの定義
   * クラスメソッド
   * デフォルトのパラメーター
   * REST パラメーター

## 関連トピック {#see-also}

{{see-also}}


