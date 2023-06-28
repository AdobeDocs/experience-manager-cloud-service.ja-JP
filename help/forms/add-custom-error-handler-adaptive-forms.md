---
title: アダプティブForms for AEM Adaptive Formsにカスタムエラーハンドラーを追加する
seo-title: Error Handlers in Adaptive Forms for AEM Adaptive Forms
description: AEM Formsは、外部サービスを呼び出すように設定された REST エンドポイントを使用して、フォームに対して標準で提供される成功およびエラーハンドラーを提供します。 AEMアダプティブフォームには、デフォルトのエラーハンドラーや、カスタムのエラーハンドラーを追加できます。
seo-description: Error handler function and Rule Editor in Adaptive Forms helps you to effectively manage and customize error handling. You can add a default error handler as well as custom error handler in an AEM Adaptive Form.
keywords: カスタムエラーハンドラーの追加、デフォルトエラーハンドラーの追加、フォームのエラーハンドラーの追加、ルールエディターの呼び出しサービスを使用したカスタムエラーハンドラーの追加、ルールエディターの設定、ルールエディターを使用したカスタムエラーハンドラーの追加
contentOwner: Ruchita Srivastav
content-type: reference
feature: Adaptive Forms
source-git-commit: 66c7b30b8b66bc86d7b83e57e02ed61d426553a2
workflow-type: tm+mt
source-wordcount: '1979'
ht-degree: 8%

---

# アダプティブFormsのエラーハンドラー {#error-handlers-in-adaptive-form}

| バージョン | 記事リンク |
| -------- | ---------------------------- |
| AEM 6.5 | [ここをクリックしてください](https://experienceleague.adobe.com/docs/experience-manager-65/forms/adaptive-forms-advanced-authoring/standard-validation-error-messages-adaptive-forms.html) |
| AEM as a Cloud Service | この記事 |

AEM Formsには、すぐに使用できる、フォーム送信の成功ハンドラーとエラーハンドラーが用意されています。 また、エラーハンドラ関数をカスタマイズする機能も提供します。 例えば、特定のエラーコードに対してバックエンドでカスタムワークフローを呼び出したり、サービスが停止していることを顧客に通知したりできます。 ハンドラーは、サーバー応答に基づいて実行されるクライアントサイド関数です。API を使用して外部サービスが呼び出されると、データが検証用にサーバーに送信され、クライアントに応答を返して送信の成功またはエラーイベントに関する情報を返します。 この情報は、関連するハンドラーにパラメーターとして渡され、関数が実行されます。エラーハンドラーは、発生したエラーや検証の問題を管理および表示するのに役立ちます。

![フォームにカスタムエラーハンドラーを追加する方法を理解するためのエラーハンドラーワークフロー](/help/forms/assets/error-handler-workflow.png)

アダプティブフォームは、事前設定された検証条件に基づいて、フィールドに指定した入力を検証し、外部サービスを呼び出すように設定された REST エンドポイントから返される様々なエラーを確認します。 アダプティブフォームで使用するデータソースに基づいて、検証条件を設定できます。 例えば、RESTful web サービスをデータソースとして使用する場合、Swagger 定義ファイルで検証条件を定義できます。

入力値が検証条件を満たす場合、その値がデータソースの他のデータソースに送信され、アダプティブフォームはエラーハンドラーを使用してエラーメッセージを表示します。 この方法と同様に、Adaptive Formsはカスタムエラーハンドラーと統合され、データの検証を実行します。 入力値が検証条件を満たさない場合、エラーメッセージはアダプティブフォームのフィールドレベルに表示されます。 これは、サーバーから返される検証エラーメッセージが標準メッセージ形式の場合に発生します。


## エラーハンドラーの使用 {#uses-of-error-handler}

エラーハンドラーは、様々な目的で使用されます。 エラーハンドラー関数の使用の一部を以下に示します。
* **検証の実行**:エラー処理は、事前定義されたルールまたは条件に対してユーザー入力を検証することから始まります。 ユーザーがアダプティブフォームに入力すると、エラーハンドラーは入力を検証し、必要な形式、長さ、またはその他の制約を満たすようにします。

* **リアルタイムでのフィードバックの提供**:エラーが検出されると、エラーハンドラーは、対応するフォームフィールドの下のインラインエラーメッセージなど、ユーザーに対する即座のフィードバックを表示します。 このフィードバックは、ユーザーがフォームを送信して応答を待たなくても、エラーを識別して修正するのに役立ちます。


* **エラーメッセージの表示**:アダプティブフォームの送信で検証エラーが発生すると、エラーハンドラーは適切なエラーメッセージを表示します。 エラーメッセージは、明確で簡潔で、注意が必要な特定のフィールドをハイライト表示する必要があります。

* **エラーのあるフィールドをハイライトします**:誤ったフィールドにユーザーの注意を引くために、エラーハンドラーは、対応するフィールドを強調表示するか視覚的に区別します。 この処理は、背景色を変更したり、アイコンや境界線を追加したり、ユーザーがエラーをすばやく見つけて対処するのに役立つその他の視覚的なキューを追加したりすることで実行されます。


## 失敗/エラー応答形式 {#failure-response-format}

サーバーの検証エラーメッセージが次の標準形式の場合、アダプティブフォームは、フィールドレベルでエラーを表示します。
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

* `errorCausedBy` は失敗の理由を説明します.
* `errors` は、検証条件に失敗したフィールドの SOM 式と検証エラーメッセージに言及します.
* `originCode` 外部サービスが返す http ステータスコードを含む、AEMによって追加されたフィールド。
* `originMessage` 外部サービスから返される生のエラーデータを含む、AEMによって追加されたフィールド。

AEM Formsバージョンの機能の改善とその後の更新に伴い、既存の失敗応答構造は、既存の失敗応答構造との下位互換性を持つ RFC7807 に基づいて新しい形式に変更されました。

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
> * エラー応答構造に次のいずれかが含まれていることを確認します。 **fieldName** または **dataRef**.
> * 次を確認します。 **ContentType** ヘッダーは次のとおりです。 **application/problem+json**.

ここで、
* `type (required)` 失敗のタイプを指定します。 次のいずれかの値を指定できます。
   * `SERVER_SIDE_VALIDATION` は、サーバー側の検証が原因でエラーが発生したことを示します。
   * `FORM_SUBMISSION` フォームの送信中にエラーが発生したことを示します
   * `SERVICE_INVOCATION` サードパーティのサービスの呼び出し中にエラーが発生したことを示します。
   * `FAILURE` 一般的なエラーを示します。
   * `VALIDATION_ERROR` は、検証エラーが原因でエラーが発生したことを示します。

* `title (optional)` 失敗のタイトルまたは簡単な説明を示します。
* `detail (optional)` 必要に応じて、失敗に関する追加の詳細を示します。
* `instance (optional)` は、失敗に関連付けられたインスタンスまたは識別子を表し、失敗の特定の発生を追跡したり識別したりするのに役立ちます。
* `validationErrors (required)` には、検証エラーに関する情報が含まれています。 次のフィールドが含まれます。
   * `fieldname` では、検証条件に合わなかったフィールドの SOM 式について言及しています。
   * `dataRef` 検証に失敗したフィールドの JSON パスまたは XPath を表します。
   * `details` には、エラーフィールドを含む検証エラーメッセージが含まれています。
* `originCode (optional)` 外部サービスによって返された http ステータスコードを含む、AEMによって追加されたフィールド
* `originMessage (optional)` 外部サービスから返される生のエラーデータを含む、AEMによって追加されたフィールド。

### サンプルエラー応答形式 {#sample-error-response-format}

エラー応答を表示するオプションの一部を次に示します。

+++

+++  アダプティブフォームの fieldName に基づく


* **`Header:`** `content-type:application/problem+json`
* **`Response:`**

      ``javascript
      {
      &quot;type&quot;:&quot;VALIDATION_ERROR&quot;,
      &quot;validationErrors&quot;:[
      {
      &quot;fieldName&quot;:&quot;guide[0].guide1[0].guideRootPanel[0].textbox1686647736683[0]&quot;,
      &quot;dataRef&quot;:「」
      &quot;details&quot;:[
      「無効な ID が提供されました。 指定された値が正しくありません。」
      ]
      }
      ]}
      &quot;&#39;
  
  アダプティブフォーム内の任意のフィールドの SOM 式を表示するには、フィールドをタップし、 **[!UICONTROL SOM 式を表示]**.

  ![カスタムエラーハンドラーでエラー応答を表示するためのアダプティブフォームフィールドの SOM 式](/help/forms/assets/custom-error-handler-somexpression.png)

+++


+++ アダプティブフォームの dataRef に基づく

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

  ![カスタムエラーハンドラーでエラー応答を表示するためのアダプティブフォームフィールドのデータ参照](/help/forms/assets/custom-errorhandler-dataref.png)

dataRef の値は、 **[!UICONTROL プロパティ]** フォームコンポーネントのウィンドウ。


+++

## ルールエディターを使用してエラーハンドラーを追加 {#add-error-handler-using-rule-editor}

の使用 [ルールエディターの Invoke Service](https://experienceleague.adobe.com/docs/experience-manager-65/forms/adaptive-forms-advanced-authoring/rule-editor.html?lang=en#invoke) 「 」アクションでは、アダプティブフォームで使用するデータソースに基づいて検証条件を定義します。 RESTful Web サービスをデータソースとして使用する場合、Swagger 定義ファイルで検証条件を定義できます。 アダプティブFormsのエラーハンドラー関数とルールエディターを利用すると、エラー処理を効果的に管理およびカスタマイズできます。 ルールエディターを使用して条件を定義し、ルールがトリガーされたときに実行するアクションを設定します。 アダプティブフォームは、事前設定された検証条件に基づいて、フィールドに入力した入力を検証します。 入力値が検証条件を満たさない場合、エラーメッセージはアダプティブフォームのフィールドレベルに表示されます。

>[!NOTE]
>
> * ルールエディターの Invoke サービスアクションでエラーハンドラーを使用するには、フォームデータモデルを使用して Adaptive Formsを設定します。
> * デフォルトのエラーハンドラーは、エラー応答が標準スキーマにある場合にフィールドにエラーメッセージを表示するためにデフォルトで提供されます。 デフォルトのエラーハンドラーは、エラー応答が標準のスキーマに準拠していない場合に、カスタムエラーハンドラーを呼び出すこともできます。

<!-- 
Using Rule Editor, you can:
* [Add default error handler function](#add-default-errror-handler)
* [Add custom error handler function](#add-custom-errror-handler)


### Add default error handler function {#add-default-errror-handler}

A default error handler is supported by default to display error messages on fields if the error response is in standard schema or in server-side validation failure. 
To understand how to use a default error handler using the [Rule Editor's Invoke Service](https://experienceleague.adobe.com/docs/experience-manager-65/forms/adaptive-forms-advanced-authoring/rule-editor.html?lang=en#invoke) action, take an example of a simple Adaptive Form with two fields, **Pet ID** and **Pet Name** and use a default error handler at the **Pet ID** field to check for various errors returned by the REST endpoint configured to invoke an external service, for example, `200 - OK`,`404 - Not Found`, `400 - Bad Request`. To add a default error handler using the Rule Editor's Invoke Service action, execute the following steps:

1. Open an Adaptive Form in authoring mode, select a form component and tap **[!UICONTROL Rule Editor]** to open the rule editor.
1. Tap **[!UICONTROL Create]**.
1. Create a condition in the **When** section of the rule. For example, **When[Name of Pet ID field]** is changed. Select is changed from the **Select State** drop-down list.
1. In the **Then** section, select **[!UICONTROL Invoke Service]** from the **Select Action** drop-down list.
1. Select a **Post service** and its corresponding data bindings from the **Input** section. For example, to validate **Pet ID**, select a **Post service** as **GET /pet/{petId}** and select **Pet ID** in the **Input** section.
1. Select the data bindings from the **Output** section. Select **Pet Name** in the **Output** section.
1. Select **[!UICONTROL Default Error Handler]** from the **Error Handler** section. 
1. Click **[!UICONTROL Done]**.

 ![add a default error handler for a field validation checks in a form](/help/forms/assets/default-error-handler.png)

As a result of this rule, the values you enter for **Pet ID** checks validation for **Pet Name** using external service invoked by REST endpoint. If the validation criteria based on the data source fail, the error messages are displayed at the field level.

 ![display the default error message when you add a default error handler in a form to handle error responses](/help/forms/assets/default-error-message.png)

-->

### カスタムエラーハンドラー関数を追加 {#add-custom-errror-handler}

カスタムエラーハンドラー関数を追加して、次のようなアクションを実行できます。
* 非標準または標準のエラー応答を使用するエラー応答を処理します。 これらの非標準的なエラー応答は、 [エラー応答の標準スキーマ](#failure-response-format).
* analytics イベントを任意の analytics プラットフォームに送信します。 例：Adobe Analytics.
* エラーメッセージが表示されるモーダルダイアログを表示します。

上記のアクションに加えて、カスタムエラーハンドラーを使用して、特定のユーザー要件を満たすカスタマイズされた関数を実行できます。

カスタムエラーハンドラーは、外部サービスから返されたエラーに応答し、カスタマイズされた応答をエンドユーザーに配信するように設計された関数（クライアントライブラリ）です。 注釈付きの任意のクライアントライブラリ `@errorHandler` は、カスタムエラーハンドラー関数と見なされます。 この注釈は、 `.js` ファイル。
を使用してカスタムエラーハンドラーを作成し、使用する方法を理解するには [ルールエディターの Invoke サービス](https://experienceleague.adobe.com/docs/experience-manager-65/forms/adaptive-forms-advanced-authoring/rule-editor.html?lang=en#invoke) 「 」アクションでは、2 つのフィールドを持つアダプティブフォームの例を見てみましょう。 **ペット ID** および **ペット名** を使用し、 **ペット ID** 外部サービスを呼び出すように設定された REST エンドポイントが返す様々なエラーを確認するフィールド。例えば、 `200 - OK`,`404 - Not Found`, `400 - Bad Request`.

アダプティブフォームにカスタムエラーハンドラーを追加して使用するには、次の手順を実行します。
1. [カスタムエラーハンドラーの作成](#create-custom-error-message)
1. [ルールエディターを使用してカスタムエラーハンドラーを設定する](#use-custom-error-handler)

#### 1.カスタムエラーハンドラーを作成する {#create-custom-error-message}

カスタムエラー関数を作成するには、次の手順を実行します。
1. [AEM Formsas a Cloud Serviceリポジトリのクローンを作成します。](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/onboarding/journey/developers.html?lang=jp#accessing-git).
1. `[AEM Forms as a Cloud Service repository folder]/apps/[AEM Project Folder]/clientlibs/` に移動します。
1. `js` という名前のフォルダーを作成します。
1. `[AEM Forms as a Cloud Service repository folder]/apps/[AEM Project Folder]/clientlibs/js` フォルダーに移動します。
1. JavaScript ファイルの追加（例： ） `function.js`. ファイルには、カスタムエラーハンドラーのコードが含まれています。
次のコードを JavaScript ファイルに追加して、REST サービスエンドポイントから受け取った応答とヘッダーをブラウザーコンソールに表示します。

       ``javascript
       /**
       *カスタムエラーハンドラー
       * @name customErrorHandler カスタムエラーハンドラー関数
       * @errorHandler
       */
       function customErrorHandler(response, headers)
       {
       console.log(&quot;Custom Error Handler processing start...&quot;);
       console.log(&quot;response:&quot;+JSON.stringify(response));
       console.log(&quot;headers:&quot;+JSON.stringify(headers));
       console.log(&quot;Custom Error Handler processing end...&quot;);
       }
       &quot;&#39;
   
   <!--  To call the default error handler after the custom error handler, the following line of the sample code is used:
        `guidelib.dataIntegrationUtils.defaultErrorHandler(response, headers) `-->
1. `function.js` ファイルを保存します。
1. `[AEM Forms as a Cloud Service repository folder]/apps/[AEM Project Folder]/clientlibs/js` フォルダーに移動します。
1. テキストファイルを `js.txt`. ファイルには次が含まれます。

   ```javascript
       #base=js
       functions.js
   ```

1. `js.txt` ファイルを保存します。

   >[!NOTE]
   >
   > カスタム関数の作成方法の詳細については、 [ルールエディターのカスタム関数](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-foundation-components/add-rules-and-use-expressions-in-an-adaptive-form/rule-editor.html?lang=en#write-rules).

1. 次のコマンドを使用して、リポジトリに変更を追加、コミット、プッシュします。

   ```javascript
       git add .
       git commit -a -m "Adding error handling files"
       git push
   ```

1. [パイプラインを実行.](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/onboarding/journey/developers.html?lang=ja#setup-pipeline)

パイプラインが正常に実行されると、カスタムエラーハンドラーがアダプティブフォームのルールエディターで使用できるようになります。 次に、AEM Formsのルールエディターの Invoke サービスを使用して、カスタムエラーハンドラーを設定して使用する方法を説明します。

#### 2.ルールエディターを使用して、カスタムエラーハンドラーを設定します {#use-custom-error-handler}

カスタムエラーハンドラーを使用するには、 **[!UICONTROL ルールエディターの Invoke Service]** アクション：

1. アダプティブフォームをオーサリングモードで開き、フォームコンポーネントを選択して、 **[!UICONTROL ルールエディター]** をクリックして、ルールエディターを開きます。
1. 「**[!UICONTROL 作成]**」をタップします。
1. ルールの&#x200B;**条件**&#x200B;セクションで条件を作成します。例： **[ペット ID フィールドの名前]** が変更された場合は、「 **変更済み** から **状態を選択** 」ドロップダウンリストから選択できます。
1. 「**Then**」セクションの&#x200B;**[!UICONTROL アクションの選択]**&#x200B;ドロップダウンリストで「**サービスの呼び出し**」を選択します。
1. を選択します。 **ポストサービス** と、対応するデータバインディングが **入力** 」セクションに入力します。 例えば、検証する場合は、次のようにします。 **ペット ID**&#x200B;を選択し、 **ポストサービス** as **GET/pet/{petId}** を選択し、 **ペット ID** 内 **入力** 」セクションに入力します。
1. からデータ連結を選択します。 **出力** 」セクションに入力します。 例えば、「 **ペット名** 内 **出力** 」セクションに入力します。
1. 選択 **[!UICONTROL カスタムエラーハンドラー]** から **[!UICONTROL エラーハンドラー]** 」セクションに入力します。
1. 「**[!UICONTROL 完了]**」をクリックします。

![エラー応答を処理するためのカスタムエラーハンドラーをフォームに追加します](/help/forms/assets/custom-error-handler.png)


このルールの結果、 **ペット ID** 検証を確認 **ペット名** REST エンドポイントによって呼び出された外部サービスを使用する。 データソースに基づく検証条件が失敗した場合は、エラーメッセージがフィールドレベルで表示されます。


![エラー応答を処理するためのカスタムエラーハンドラーをフォームに追加します](/help/forms/assets/custom-error-handler-message.png)

ブラウザーコンソールを開き、REST サービスエンドポイントから受け取った応答とヘッダーで、検証エラーメッセージを確認します。


カスタムエラーハンドラー関数は、エラー応答に基づいて、モーダルダイアログの表示や Analytics イベントの送信など、追加のアクションを実行します。 カスタムエラーハンドラー関数を使用すると、特定のユーザー要件に合わせて柔軟にエラー処理をカスタマイズできます。

<!-- 

## Configure Adaptive Form submission to add custom handlers {#configure-adaptive-form-submission}

If the server validation error message does not display in the standard format, you can enable asynchronous submission and add a custom error handler on Adaptive Form submission to convert the message into a standard format.

### Configure asynchronous Adaptive Form submission {#configure-asynchronous-adaptive-form-submission}

Before adding custom handler, you must configure the adaptive form for asynchronous submission. Execute the following steps:

1. In adaptive form authoring mode, select the Form Container object and tap ![adaptive form properties](assets/configure_icon.png) to open its properties.
1. In the **[!UICONTROL Submission]** properties section, enable **[!UICONTROL Use asynchronous submission]**.
1. Select **[!UICONTROL Revalidate on server]** to validate the input field values on server before submission.
1. Select the Submit Action:

    * Select **[!UICONTROL Submit using Form Data Model]** and select the appropriate data model, if you are using RESTful web service based [form data model](work-with-form-data-model.md) as the data source.
    * Select **[!UICONTROL Submit to REST Service endpoint]** and specify the **[!UICONTROL Redirect URL/Path]**, if you are using RESTful web services as the data source.

    ![adaptive form submission properties](assets/af_submission_properties.png)

1. Tap ![Save](assets/save_icon.png) to save the properties.

### Add custom error handler on Adaptive Form submission {#add-custom-error-handler-af-submission}

AEM Forms provides out-of-the-box success and error handlers for form submissions. Handlers are client-side functions that execute based on the server response. When an Adaptive Form is submitted, the data is transmitted to the server for validation, which returns a response to the client with information about the success or error event for the submission. The information is passed as parameters to the relevant handler to execute the function.

Execute the following steps to add custom error handler on Adaptive Form submission:

1. Open an Adaptive Form in authoring mode, select any form object, and tap  to open the rule editor.
1. Select **[!UICONTROL Form]** in the Form Objects tree and tap **[!UICONTROL Create]**.
1. Select **[!UICONTROL Error in Submission]** from the Event drop-down list.
1. Write a rule to convert custom error structure to the standard error structure and tap **[!UICONTROL Done]** to save the rule.

The following is a sample code to convert a custom error structure to the standard error structure:

```javascript
var data = $event.data;
var som_map = {
    "id": "guide[0].guide1[0].guideRootPanel[0].Pet[0].id_1[0]",
    "name": "guide[0].guide1[0].guideRootPanel[0].Pet[0].name_2[0]",
    "status": "guide[0].guide1[0].guideRootPanel[0].Pet[0].status[0]"
};

var errorJson = {};
errorJson.errors = [];

if (data) {
    if (data.originMessage) {
        var errorData;
        try {
            errorData = JSON.parse(data.originMessage);
        } catch (err) {
            // not in json format
        }

        if (errorData) {
            Object.keys(errorData).forEach(function(key) {
                var som_key = som_map[key];
                if (som_key) {
                    var error = {};
                    error.somExpression = som_key;
                    error.errorMessage = errorData[key];
                    errorJson.errors.push(error);
                }
            });
        }
        window.guideBridge.handleServerValidationError(errorJson);
    } else {
        window.guideBridge.handleServerValidationError(data);
    }
}
```

The `var som_map` lists the SOM expression of the Adaptive Form fields that you want to transform into the standard format. You can view the SOM expression of any field in an adaptive form by tapping the field and selecting **[!UICONTROL View SOM Expression]**.

Using this custom error handler, the adaptive form converts the fields listed in `var som_map` to standard error message format. As a result, the validation error messages display at field-level in the adaptive form.

 -->