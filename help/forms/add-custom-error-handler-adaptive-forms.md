---
title: AEM アダプティブフォームのアダプティブフォームにカスタムエラーハンドラーを追加
description: AEM Forms は、外部サービスを呼び出すように設定された REST エンドポイントを使用して、フォームに対して標準で提供される成功ハンドラーとエラーハンドラーを提供します。AEM アダプティブフォームには、デフォルトのエラーハンドラーや、カスタムのエラーハンドラーを追加できます。
keywords: カスタムエラーハンドラーを追加、デフォルトのエラーハンドラーを追加、フォームにエラーハンドラーを追加、ルールエディターのサービス呼び出しを使用してカスタムエラーハンドラーを追加、ルールエディターを設定してカスタムエラーハンドラーを追加、ルールエディターを使用してカスタムエラーハンドラーを追加
contentOwner: Ruchita Srivastav
content-type: reference
feature: Adaptive Forms, Foundation Components
exl-id: 198a26a9-d6bb-457d-aab8-0a5d15177c48
role: User, Developer
source-git-commit: edfefb163e2d48dc9f9ad90fa68809484ce6abb0
workflow-type: ht
source-wordcount: '2308'
ht-degree: 100%

---

# AEM Adaptive Formsにカスタムエラーハンドラーを追加する {#error-handlers-in-adaptive-form}

>[!NOTE]
>
> [新しいアダプティブフォームを作成する](/help/forms/creating-adaptive-form-core-components.md)、または [AEM Sites ページにアダプティブフォームを追加する](/help/forms/create-or-add-an-adaptive-form-to-aem-sites-page.md)際には、最新の拡張可能なデータキャプチャである[コアコンポーネント](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html?lang=ja)を使用することをお勧めします。これらのコンポーネントは、アダプティブフォームの作成における大幅な進歩を示すものであり、優れたユーザーエクスペリエンスを実現します。この記事では、基盤コンポーネントを使用してアダプティブフォームを作成する従来の方法について説明します。

| バージョン | 記事リンク |
| -------- | ---------------------------- |
| AEM 6.5 | [ここをクリックしてください](https://experienceleague.adobe.com/docs/experience-manager-65/forms/adaptive-forms-advanced-authoring/standard-validation-error-messages-adaptive-forms.html?lang=ja) |
| AEM as a Cloud Service | この記事 |

AEM Forms には、すぐに使用できる、フォーム送信用のサクセスハンドラーとエラーハンドラーが用意されています。また、エラーハンドラー関数をカスタマイズする機能も提供されています。例えば、特定のエラーコードに対してバックエンドでカスタムワークフローを呼び出したり、サービスが停止していることを顧客に通知したりできます。ハンドラーは、サーバー応答に基づいて実行されるクライアントサイド関数です。API を使用して外部サービスが呼び出されると、データが検証のためにサーバーに送信され、サーバーは送信のサクセスイベントまたはエラーイベントに関する情報を含む応答をクライアントに返します。この情報は、関連するハンドラーにパラメーターとして渡され、関数が実行されます。エラーハンドラーは、発生したエラーや検証の問題を管理および表示するのに役立ちます。

![フォームへのカスタムエラーハンドラーの追加方法を理解するためのエラーハンドラーワークフロー](/help/forms/assets/error-handler-workflow.png)

アダプティブフォームは、事前設定された検証条件に基づいてフィールドに指定された入力を検証し、外部サービスを呼び出すように設定された REST エンドポイントから返される様々なエラーを確認します。アダプティブフォームで使用するデータソースに基づいて、検証条件を設定できます。例えば、RESTful web サービスをデータソースとして使用する場合、Swagger 定義ファイルで検証条件を定義できます。

入力値が検証条件を満たす場合、その値は他のデータソースに送信され、アダプティブフォームはエラーハンドラーを使用してエラーメッセージを表示します。この方法と同様に、アダプティブフォームをカスタムエラーと統合して、データ検証を実行します。入力値が検証条件を満たさない場合、アダプティブフォームのフィールドレベルでエラーメッセージが表示されます。これは、サーバーから返される検証エラーメッセージが標準メッセージ形式である場合に発生します。


## エラーハンドラーの使用 {#uses-of-error-handler}

エラーハンドラーは、様々な目的で使用されます。エラーハンドラー関数の使用例の一部を以下に示します。

* **検証の実行**：事前定義されたルールや条件に対してユーザー入力を検証することで、エラー処理を開始します。ユーザーがアダプティブフォームに入力すると、エラーハンドラーは入力を検証し、必要な形式、長さ、その他の制約が満たされていることを確認します。

* **リアルタイムでのフィードバックの提供**：エラーが検出されると、エラーハンドラーは、対応するフォームフィールドの下にフィードバック（インラインエラーメッセージなど）を、ユーザーに即時に表示します。このフィードバックは、ユーザーがフォームを送信して応答を待つことなく、エラーを特定して修正するのに役立ちます。


* **エラーメッセージの表示**：アダプティブフォームの送信で検証エラーが発生すると、エラーハンドラーは適切なエラーメッセージを表示します。エラーメッセージは、明確かつ簡潔で、注意が必要な特定のフィールドをハイライト表示する必要があります。

* **エラーのあるフィールドのハイライト表示**：特定の誤ったフィールドにユーザーの注意を引くために、エラーハンドラーは対応するフィールドをハイライト表示するか、視覚的に区別します。この処理は、背景色の変更、アイコンや境界線の追加、またはユーザーがエラーを迅速に見つけて対処する上で役立つその他の視覚的なヒントを追加することによって実行されます。


## 失敗／エラー応答形式 {#failure-response-format}

サーバー検証エラーメッセージが次の標準形式の場合、アダプティブフォームはフィールドレベルでエラーを表示します。
次のコードは、既存の失敗応答構造を示しています。

```javascript
   {
    errorCausedBy : "SERVER_SIDE_VALIDATION/SERVICE_INVOCATION_FAILURE"
    errors : [
        {
             somExpression  : <somexpr>
             errorMessage / errorMessages : <validationMsg> / [<validationMsg>, <validationMsg>]
        }
    ]
    originCode : <target error Code>
    originMessage : <unstructured error message returned by service>
    }
```


ここで、

* `errorCausedBy` は失敗の理由を説明します。
* `errors` は、検証条件を満たさなかったフィールドの SOM 式と検証エラーメッセージを示します。
* `originCode` は、AEM によって追加され、外部サービスから返された http ステータスコードを含みます。
* `originMessage` は AEM によって追加されたフィールドで、外部サービスから返された生のエラーデータが含まれています。

AEM Forms バージョンの機能の改善とその後の更新に伴い、既存の失敗応答構造は、既存の失敗応答構造と下位互換性のある RFC7807 に基づく新しい形式に変更されました。

```javascript
    {
        "type": "SERVER_SIDE_VALIDATION/FORM_SUBMISSION/SERVICE_INVOCATION/FAILURE/VALIDATION_ERROR", (required)
        "title": "Server side validation failed/Third party service invocation failed", (optional)
        "detail": "", (optional)
        "instance": "", (optional)
        "validationErrors" : [ (required)
            {
                "fieldName":"<SOM expression of the field whose data sent is invalid>",
                "dataRef":<JSONPath (or XPath) of the data element which is invalid>
                "details": ["Error Message(s) for the field"] (required)
    
            }
        ],
        "originCode": <Origin http status code>, (optional - in case of SERVER_SIDE_VALIDATION)
        "originMessage" : "<unstructured error message returned by service>" (optional - in case of SERVER_SIDE_VALIDATION)
    }
```


>[!NOTE]
>
> * エラー応答構造に **fieldName** または **dataRef** が含まれていることを確認してください。
> * **ContentType** ヘッダーが **application/problem+json** であることを確認します。

ここで、

* `type (required)` は失敗のタイプを指定します。次のいずれかの値になります。
   * `SERVER_SIDE_VALIDATION` は、サーバーサイドの検証が原因でエラーが発生したことを示します。
   * `FORM_SUBMISSION` は、フォームの送信中にエラーが発生したことを示します。
   * `SERVICE_INVOCATION` は、サードパーティのサービスの呼び出し中にエラーが発生したことを示します。
   * `FAILURE` は、一般的なエラーが発生したことを示します。
   * `VALIDATION_ERROR` は、検証エラーが原因でエラーが発生したことを示します。

* `title (optional)` は、エラーのタイトルまたは簡単な説明を示します。
* `detail (optional)` は、必要に応じて、エラーに関する追加の詳細を示します。
* `instance (optional)` は、エラーに関連付けられたインスタンスまたは識別子を表し、特定のエラーの発生を追跡したり識別したりするのに役立ちます。
* `validationErrors (required)` には、検証エラーに関する情報が含まれています。次のフィールドが含まれています。
   * `fieldname` は、検証条件を満たさなかったフィールドの SOM 式に言及します。
   * `dataRef` は、検証に失敗したフィールドの JSON パスまたは XPath を表します。
   * `details` には、検証エラーメッセージとエラーのあるフィールドが含まれています。
* `originCode (optional)` は AEM によって追加されたフィールドで、外部サービスから返された http ステータスコードが含まれています。
* `originMessage (optional)` は AEM によって追加されたフィールドで、外部サービスから返された生のエラーデータが含まれています。

### エラー応答形式のサンプル {#sample-error-response-format}

エラー応答を表示するオプションの一部を次に示します。

+++  アダプティブフォームの fieldName プロパティに基づく場合


* **`Header:`** `content-type:application/problem+json`
* **`Response:`**

  ```javascript
          {
              "type": "VALIDATION_ERROR",
              "validationErrors": [
              {
              "fieldName": "guide[0].guide1[0].guideRootPanel[0].textbox1686647736683[0]",
              "dataRef": "",
              "details": [
              "Invalid ID supplied. Provided value is not correct!"
          ]
          }
          ]}
  ```

  アダプティブフォーム内の任意のフィールドの SOM 式を表示するには、フィールドをタップして、「**[!UICONTROL SOM 式を表示]**」を選択します。

  ![カスタムエラーハンドラーでエラー応答を表示するアダプティブフォームフィールドの SOM 式](/help/forms/assets/custom-error-handler-somexpression.png)

+++


+++ アダプティブフォームの dataRef プロパティに基づく場合

* **`Header:`** `content-type:application/problem+json`
* **`Response:`**

  ```javascript
      {
          "type": "VALIDATION_ERROR",
          "validationErrors": [
          {
              "fieldName": "",
              "dataRef": "/Pet/id",
              "details": [
              "Invalid ID supplied. Provided value is not correct!"
              ]
              }
      ]}
  ```

  ![カスタムエラーハンドラーでエラー応答を表示するアダプティブフォームフィールドのデータ参照](/help/forms/assets/custom-errorhandler-dataref.png)

dataRef の値は、フォームコンポーネントの&#x200B;**[!UICONTROL プロパティ]**&#x200B;ウィンドウで確認できます。

+++


## ルールエディターを使用してエラーハンドラーを追加 {#add-error-handler-using-rule-editor}

[ルールエディターのサービスの呼び出し](https://experienceleague.adobe.com/docs/experience-manager-65/forms/adaptive-forms-advanced-authoring/rule-editor.html?lang=ja#invoke)アクションを使用して、アダプティブフォームで使用するデータソースに基づいて検証条件を定義します。RESTful Web サービスをデータソースとして使用する場合、Swagger 定義ファイルで検証条件を定義できます。アダプティブフォームのエラーハンドラー関数とルールエディターを利用すると、エラー処理を効率的に管理およびカスタマイズできます。ルールエディターを使用して条件を定義し、ルールがトリガーされたときに実行するアクションを設定します。アダプティブフォームは、事前設定された検証条件に基づいて、フィールドに入力した内容を検証します。入力値が検証条件を満たさない場合、アダプティブフォームのフィールドレベルでエラーメッセージが表示されます。

>[!NOTE]
>
> * ルールエディターのサービスの呼び出しアクションでエラーハンドラーを使用するには、フォームデータモデル（FDM）を使用してアダプティブフォームを設定します。
> * デフォルトのエラーハンドラーは、エラー応答が標準スキーマにある場合にフィールドにエラーメッセージを表示するために使用します。デフォルトのエラーハンドラーは、カスタムエラーハンドラー関数から呼び出すこともできます。

ルールエディターを使用して、次のことができます。

* [デフォルトのエラーハンドラー関数を追加](#add-default-errror-handler)
* [カスタムエラーハンドラー関数を追加](#add-custom-error-handler-function)


### デフォルトのエラーハンドラー関数を追加 {#add-default-errror-handler}

デフォルトのエラーハンドラーは、エラー応答が標準スキーマの場合、またはサーバーサイドの検証エラーの場合に、フィールドにエラーメッセージを表示する機能をサポートしています。
[ルールエディターのサービスの呼び出し](https://experienceleague.adobe.com/docs/experience-manager-65/forms/adaptive-forms-advanced-authoring/rule-editor.html?lang=ja#invoke)アクションを使用してデフォルトのエラーハンドラーを使用する方法を理解するために、「**ペット ID**」と「**ペット名**」という 2 つのフィールドがある簡単なアダプティブフォームの例を見てみましょう。「**ペット ID**」フィールドでデフォルトのエラーハンドラーを使用して、外部サービス（`200 - OK`、`404 - Not Found`、`400 - Bad Request` など）を呼び出すように設定された REST エンドポイントが返す様々なエラーを確認します。ルールエディターのサービスの呼び出しアクションを使用してデフォルトのエラーハンドラーを追加するには、次の手順を実行します。

1. アダプティブフォームをオーサリングモードで開き、フォームコンポーネントを選択してから、**[!UICONTROL ルールエディター]**&#x200B;を選択してルールエディターを開きます。
1. 「**[!UICONTROL 作成]**」を選択します。
1. ルールの「**When**」セクションで条件を作成します。例えば、**[ペット ID フィールドの名前]**&#x200B;が変更された場合という条件が考えられます。選択は、**状態を選択**&#x200B;ドロップダウンリストから変更できます。
1. 「**Then**」セクションの&#x200B;**[!UICONTROL アクションの選択]**&#x200B;ドロップダウンリストで「**サービスの呼び出し**」を選択します。
1. **Post サービス**&#x200B;とそれに対応するデータ連結を「**入力**」セクションから選択します。例えば、**ペット ID** を検証する場合は、**Post サービス**&#x200B;を **GET /pet/{petId}** として選択し、「**入力**」セクションで「**ペット ID**」を選択します。
1. 「**出力**」セクションからデータ連結を選択します。「**出力**」セクションで「**ペット名**」を選択します。
1. 「**エラーハンドラー**」セクションから「**[!UICONTROL デフォルトのエラーハンドラー]**」を選択します。
1. 「**[!UICONTROL 完了]**」をクリックします。

![フォーム内のフィールド検証チェック用にデフォルトのエラーハンドラーを追加](/help/forms/assets/default-error-handler.png)

このルールの結果、**ペット ID** に入力した値は、REST エンドポイントによって呼び出された外部サービスを使用して、**ペット名**&#x200B;の検証をチェックします。データソースに基づく検証条件が失敗した場合は、フィールドレベルでエラーメッセージが表示されます。

![エラー応答を処理するフォームにデフォルトのエラーハンドラーを追加したときに、デフォルトのエラーメッセージを表示](/help/forms/assets/default-error-message.png)

### カスタムエラーハンドラー関数を追加

カスタムエラーハンドラー関数を追加すると、次のようなアクションを実行できます。

* 非標準または標準のエラー応答を使用するエラー応答を処理します。これらの非標準のエラー応答は、[エラー応答の標準スキーマ](#failure-response-format)に準拠していないことに注意してください。
* 分析イベントを任意の分析プラットフォームに送信します。例：Adobe Analytics
* エラーメッセージが表示されるモーダルダイアログを表示します。

上記のアクションに加えて、カスタムエラーハンドラーを使用すると、特定のユーザー要件を満たすカスタマイズされた関数を実行できます。

カスタムエラーハンドラーは、外部サービスから返されたエラーに応答し、カスタマイズされた応答をエンドユーザーに配信するように設計された関数（クライアントライブラリ）です。注釈 `@errorHandler` 付きのクライアントライブラリは、カスタムエラーハンドラー関数と見なされます。この注釈は、`.js` ファイルで指定されたエラーハンドラー関数を特定するのに役立ちます。
[ルールエディターのサービスの呼び出し](https://experienceleague.adobe.com/docs/experience-manager-65/forms/adaptive-forms-advanced-authoring/rule-editor.html?lang=ja#invoke)アクションを使用してカスタムエラーハンドラーを作成および使用する方法を理解するために、「**ペット ID**」および「**ペット名**」という 2 つのフィールドを持つアダプティブフォームを例に、「**ペット ID**」でカスタムエラーハンドラーを使用して、`200 - OK`、`404 - Not Found`、`400 - Bad Request` などの外部サービスを呼び出すように設定された REST エンドポイントが返す様々なエラーをチェックしましょう。

アダプティブフォームにカスタムエラーハンドラーを追加して使用するには、次の手順を実行します。

1. [エラーハンドラーのカスタム関数を追加](#1-add-the-custom-function-for-the-error-handler)
2. [ルールエディターを使用してカスタムエラーハンドラーを設定](#use-custom-error-handler)

#### &#x200B;1. エラーハンドラーのカスタム関数を追加

カスタム関数を追加する方法について詳しくは、「[コアコンポーネントに基づくアダプティブフォームのカスタム関数の作成](/help/forms/custom-function-core-component-create-function.md#create-a-custom-function)」をクリックしてください。

<!-- To create a custom error function, perform the following steps:

1. [Clone your AEM Forms as a Cloud Service Repository](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/onboarding/journey/developers.html?lang=ja#accessing-git). 
2. Create a folder under the `[AEM Forms as a Cloud Service repository folder]/apps/` folder. For example, create a folder named as `experience-league`
3. Navigate to `[AEM Forms as a Cloud Service repository folder]/apps/[AEM Project Folder]/experience-league/` and create a `ClientLibraryFolder` as `clientlibs`.
4. Create a folder named `js`.
5. Navigate to the `[AEM Forms as a Cloud Service repository folder]/apps/[AEM Project Folder]/clientlibs/js` folder. -->

1. JavaScript ファイル（例：`function.js`）に、カスタムエラーハンドラーの以下のコードを追加します。ファイルには、カスタムエラーハンドラーのコードが含まれています。
次のコードを JavaScript ファイルに追加して、REST サービスエンドポイントから受け取った応答とヘッダーをブラウザーコンソールに表示します。

   ```javascript
        /**
        * Custom Error handler
        * @name customErrorHandler Custom Error Handler Function
        * @errorHandler
        */
        function customErrorHandler(response, headers)
        {
            console.log("Custom Error Handler processing start...");
            console.log("response:"+JSON.stringify(response));
            console.log("headers:"+JSON.stringify(headers));
            guidelib.dataIntegrationUtils.defaultErrorHandler(response, headers);
            console.log("Custom Error Handler processing end...");
        }
   ```

   >[!NOTE]
   >
   > * カスタムエラーハンドラーからデフォルトのエラーハンドラーを呼び出すには、サンプルコードの次の行が使用されます。`guidelib.dataIntegrationUtils.defaultErrorHandler(response, headers) `
   > * アダプティブフォームでカスタムエラーハンドラークライアントライブラリを使用するには、`.content.xml` ファイルに `allowProxy` プロパティと `categories` プロパティを追加します。
   >
   >   * `allowProxy = [Boolean]true`
   >   * `categories= customfunctionsdemo`
   >       例えば、この場合、 [custom-errorhandler-name] は次のように指定されます。 `customfunctionsdemo`.


1. 変更を追加し、コミットして、リポジトリにプッシュします。

<!--
1. Save the `function.js` file.
1. Navigate to the `[AEM Forms as a Cloud Service repository folder]/apps/[AEM Project Folder]/clientlibs/js` folder.
2. Add a text file as `js.txt`. The file contains:

    ```javascript
        #base=js
        functions.js
    ```

3. Save the `js.txt` file.    
The created folder structure looks like:

    ![Created Client Library Folder Structure](/help/forms/assets/customclientlibrary_folderstructure.png) 
    using the below commands:
         
    ```javascript

        git add .
        git commit -a -m "Adding error handling files"
        git push
    ```
-->

1. [パイプラインを実行](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/onboarding/journey/developers.html?lang=ja#setup-pipeline)します。

パイプラインが正常に実行されると、カスタムエラーハンドラーがアダプティブフォームのルールエディターで使用できるようになります。次に、ルールエディターのサービスの呼び出しを AEM Forms で使用して、カスタムエラーハンドラーを設定して使用する方法を説明します。

#### &#x200B;2. ルールエディターを使用して、カスタムエラーハンドラーを設定 {#use-custom-error-handler}

アダプティブフォームにカスタムエラーハンドラーを実装する前に、クライアントライブラリ名が **[!UICONTROL クライアントライブラリカテゴリ]**&#x200B;のクライアントライブラリ名が、`.content.xml` ファイルのカテゴリオプションで指定された名前と一致していることを確認します。

![アダプティブフォームコンテナ設定へのクライアントライブラリ名の追加](/help/forms/assets/client-library-category-name.png)

この場合、クライアントライブラリ名は `.content.xml` ファイル内の `customfunctionsdemo` として指定されます。

**[!UICONTROL ルールエディターのサービスの呼び出し]**&#x200B;アクションを使用してカスタムエラーハンドラーを使用するには、次の手順を実行します。

1. アダプティブフォームをオーサリングモードで開き、フォームコンポーネントを選択してから、**[!UICONTROL ルールエディター]**&#x200B;を選択してルールエディターを開きます。
1. 「**[!UICONTROL 作成]**」を選択します。
1. ルールの「**When**」セクションで条件を作成します。例えば、**[ペット ID の名前フィールド]**&#x200B;が変更された場合は、「**状態を選択** 」ドロップダウンリストから「**変更済み**」を選択します。
1. 「**Then**」セクションの&#x200B;**[!UICONTROL アクションの選択]**&#x200B;ドロップダウンリストで「**サービスの呼び出し**」を選択します。
1. **Post サービス**&#x200B;とそれに対応するデータ連結を「**入力**」セクションから選択します。例えば、**ペット ID** を検証する場合は、**Post サービス**&#x200B;を **GET /pet/{petId}** として選択し、「**入力**」セクションで「**ペット ID**」を選択します。
1. 「**出力**」セクションからデータ連結を選択します。例えば、「**出力**」セクションで「**ペット名**」を選択します。
1. 「**[!UICONTROL エラーハンドラー]**」セクションから「**[!UICONTROL カスタムエラーハンドラー]**」を選択します。
1. 「**[!UICONTROL 完了]**」をクリックします。

![エラー応答を処理するためのカスタムエラーハンドラーをフォームに追加](/help/forms/assets/custom-error-handler.png)

このルールの結果、REST エンドポイントによって呼び出された外部サービスを使用して、**ペット ID** に入力した値が&#x200B;**ペット名**&#x200B;の検証をチェックします。データソースに基づく検証条件が失敗した場合は、フィールドレベルでエラーメッセージが表示されます。

![エラー応答を処理するためのカスタムエラーハンドラーをフォームに追加](/help/forms/assets/custom-error-handler-message.png)

ブラウザーコンソールを開き、REST サービスエンドポイントから受け取った応答とヘッダーで、検証エラーメッセージを確認します。


カスタムエラーハンドラー関数は、エラー応答に基づいて、モーダルダイアログの表示や Analytics イベントの送信など、追加のアクションを実行します。カスタムエラーハンドラー関数を使用すると、特定のユーザー要件に合わせて柔軟にエラー処理をカスタマイズできます。

