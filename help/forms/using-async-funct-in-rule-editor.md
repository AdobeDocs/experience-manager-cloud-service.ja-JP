---
title: ビジュアルルールエディターで非同期関数呼び出しを使用する方法
description: ビジュアルルールエディターでの非同期関数呼び出し
feature: Adaptive Forms, Core Components
role: User, Developer
level: Beginner, Intermediate
exl-id: a240ba26-a6d8-4643-8acb-1d8812dac61f
source-git-commit: 2cae8bb1050bc4538f4645d9f064b227fb947d75
workflow-type: tm+mt
source-wordcount: '1409'
ht-degree: 7%

---

# コアコンポーネントに基づくアダプティブフォームでの非同期関数の使用

アダプティブFormsの [ ルールエディター ](/help/forms/rule-editor-core-components.md) では、非同期機能をサポートしており、ユーザーのフォームとのやり取りを中断することなく、外部プロセスやデータ取得を待つ必要がある操作を統合および管理できます。

## 非同期関数または同期関数の使用を決定する要因は何ですか。

スムーズなエクスペリエンスを作成するには、ユーザーインタラクションを効果的に管理することが重要です。 操作を処理する一般的な方法には、同期関数と非同期関数の 2 つがあります。

**同期関数** タスクを順番に実行します。これにより、各操作が完了するまでアプリケーションは待機してから処理を続行します。 これにより、特に、タスクにファイルのアップロードやデータの取得などの外部リソースの待機が含まれる場合、遅延が発生し、ユーザーエクスペリエンスが魅力的ではなくなる可能性があります。

例えば、ユーザーが画像をアップロードすると、フォーム全体が停止し、アップロードが完了するのを待つシナリオについて考えてみます。 この一時停止により、ユーザーは他のフィールドとやり取りできなくなり、フラストレーションや遅延が生じます。 画像が処理されるのを待っている間に、ユーザーが移動したり忍耐力を失ったりすると、入力した情報が失われる可能性があり、エクスペリエンスが面倒で非効率的になります。

**非同期関数** を使用すると、タスクを同時に実行できます。 つまり、ユーザーはバックグラウンドプロセスの実行中もアプリケーションの操作を続行できます。 非同期操作により応答性が向上し、ユーザーは即座にフィードバックを受け取り、中断することなくエンゲージメントを維持できます。

逆に、非同期アプローチを使用すると、ユーザーはフォームの残りの部分をシームレスに入力し続けながら、バックグラウンドで画像をアップロードできます。 インターフェイスの応答性が維持され、アップロードの進行に応じて、リアルタイムの更新や迅速なフィードバックが可能です。 ユーザーエンゲージメントを強化し、中断のないスムーズなエクスペリエンスを確保します。

![ 非同期関数と同期関数 ](/help/forms/assets/sync-async.png){align=center}

## アダプティブFormsの非同期関数の実装

アダプティブFormsの非同期関数は、ルールエディターで次のルールタイプを使用して実装できます。

* [非同期関数呼び出し](#using-asynchronous-function-calls-in-the-visual-rule-editor)
* [関数出力](#how-to-use-function-output-rule-type)

## 非同期関数呼び出しのルールタイプの使用方法は？

非同期操作の [ カスタム関数 ](/help/forms/custom-function-core-component-create-function.md) を記述し、ルールエディターで **[!UICONTROL 非同期関数呼び出し]** ルールタイプを使用して非同期関数を設定できます。

### ユースケースを通した非同期関数呼び出しルールタイプの調査

ユーザーが 1 回限りのパスワード（OTP）を入力する web サイトの登録フォームについて考えてみます。 ユーザー詳細を追加するパネルは、正しい OTP を入力した後にのみ表示されます。 OTP が正しくない場合、パネルは非表示のままになり、エラーメッセージが画面に表示されます。

![ ログインフォーム ](/help/forms/assets/rule-editor-login-form.png) {width-50%}

登録フォームでは、ユーザーが **確認** ボタンをクリックすると、`matchOTP()` 関数が非同期で呼び出され、入力した OTP が検証されます。 `matchOTP()` 関数は、[ カスタム関数 ](/help/forms/custom-function-core-component-create-function.md) として実装されます。 ルールエディターで **[!UICONTROL Async Function Call]** ルールタイプを使用すると、アダプティブフォームのルールエディターで `matchOTP()` 関数を設定できます。 また、成功コールバックと失敗コールバックをルールエディターに実装することもできます。

次の図は、「**[!UICONTROL 非同期関数呼び出し]**」ルールタイプを使用してアダプティブFormsの非同期関数を呼び出す手順を示しています。

![ 非同期関数を追加するワークフロー ](/help/forms/assets/workflow-to-add-async-func.png){width=50%, align=center}

### 1. JS ファイルに非同期操作のカスタム関数を記述する

>[!NOTE]
>
> * **Async 関数呼び出し** 規則の種類を選択すると、フォームのルールエディターに表示されるのは、戻り値の型が `Promise` の関数のみです。
> * カスタム関数の作成方法については、「コアコンポーネントに基づくアダプティブフォームのカスタム関数の作成 [ というタイトルの記事を参照してください ](/help/forms/custom-function-core-component-create-function.md)。

`matchOTP()` 関数は、カスタム関数として実装されます。 以下のコードは、カスタム関数の JS ファイルに追加されます。

```JavaScript
/**
 * generates the otp for success use case
 * @param {string} otp
 * @return {PROMISE}
 */
function matchOTP(otp) {
     return new Promise((resolve, reject) => {
        // Perform some asynchronous operation here
         asyncOperationForOTPMatch(otp, (error, result) => {
            if (error) {
                // On failure, call reject(error)
                reject(error);
            } else {
                // On success, call resolve(result)
                resolve(result);
            }
        });
    });
}

/**
 * generates the otp
 */
function asyncOperationForOTPMatch(otp, callback) {
    setTimeout(() => {
        if(otp === '111') {
            callback( null, {'valid':'true'});    
        } else {
            callback( {'valid':'false'}, null);
        }
    }, 1000);
}
```

このコードは、ワンタイムパスワード（OTP）を非同期で検証するプロミスを生成する関数 `matchOTP()` を定義します。 関数 `asyncOperationForOTPMatch()` を使用して、OTP 照合プロセスをシミュレートします。 関数は、指定された OTP が `111` に等しいかどうかを確認します。 入力した OTP が正しい場合は、エラーに対して null を指定してコールバックを呼び出し、OTP が有効な `({'valid':'true'})` を示すオブジェクトを呼び出します。OTP が有効でない場合は、結果に対して `({'valid':'false'})` と null を指定してコールバックを呼び出します。

### 2. ルールエディターで非同期関数を設定する

ルールエディターで非同期関数を設定するには、次の手順を実行します。

1. [非同期関数呼び出しのルールタイプを使用して、非同期関数を使用するルールを作成します](#21-create-a-rule-to-use-asynchronous-function-using-the-async-function-call-rule-type)
1. [非同期関数のコールバックの実装](#22-implement-the-callbacks-for-asynchronous-function)

#### 2.1 非同期関数呼び出しのルールタイプを使用して、非同期関数を使用するルールを作成する

非同期操作を使用するルールを作成するには、「**[!UICONTROL 非同期関数呼び出し]**」ルールタイプを使用して、次の手順を実行します。

1. アダプティブフォームをオーサリングモードで開き、フォームコンポーネントを選択してから、**[!UICONTROL ルールエディター]**&#x200B;を選択してルールエディターを開きます。
1. 「**[!UICONTROL 作成]**」を選択します。
1. ボタンをクリックするための条件をルールの **When** セクションに作成します。 例えば、「**When[Confirm]** をクリックします。
1. 「**Then**」セクションで、「**[!UICONTROL アクションを選択]**」ドロップダウンリストから「**非同期関数呼び出し**」を選択します。
**[!UICONTROL Async 関数呼び出し]** を選択すると、`Promise` の戻り値の型を持つ関数が表示されます。
1. リストから非同期関数を選択します。 例えば、`matchOTP()` 関数とそのコールバックを `Add success callback` として選択すると、`add failure callback` が表示されます。
1. 次に、「**[!UICONTROL 入力]** バインディングを選択します。 例えば、`Form Object` として **[!UICONTROL 入力]** を選択し、`OTP` フィールドと比較します。

次のスクリーンショットは、ルールを示しています。

![ ルールタイプ ](/help/forms/assets/asyn-function-rule-type.png)

これで、`matchOTP` 関数の `Success` と `Failure` のコールバックの実装に進むことができます。

#### 2.2 非同期関数のコールバックを実装する

ビジュアルルールエディターを使用して、非同期関数の success コールバックメソッドと failure コールバックメソッドを実装します。

**メソッドのルール `Add Success callback` 作成**

OTP が値 `111` と一致する場合に、`userdetails` パネルを表示するルールを作成します。

1. 「**[!UICONTROL 成功コールバックを追加]**」をクリックします。
1. 「**[!UICONTROL ステートメントを追加]**」をクリックして、ルールを作成します。
1. ルールの **条件** セクションで条件を作成します。
1. **[!UICONTROL 関数出力]**/**[!UICONTROL イベントペイロードを取得]** を選択します。

   >[!NOTE]
   >
   > **[!UICONTROL イベントペイロードを取得]** 関数は、特定のイベントに関連付けられたデータを取得して、ユーザーインタラクションを動的に管理します。

1. 「**入力**」セクションから、対応する連結を選択します。 例えば、「**[!UICONTROL String]**」を選択して「`valid`」と入力します。 入力した文字列を `true` と比較します。
1. 「**Then**」セクションで、「**[!UICONTROL アクションを選択]**」ドロップダウンリストから **表示** を選択します。 例えば、`userdetails` パネルを表示します。
1. 「**[!UICONTROL ステートメントを追加]**」をクリックします。
1. **[!UICONTROL アクションを選択]** ドロップダウンリストから **非表示** を選択します。 例えば、`error message` のテキストボックスを非表示にします。
1. 「**[!UICONTROL 完了]**」をクリックします。

![ 成功コール ](/help/forms/assets/rule-editor-success-callback.png){width=50%, height=50%}

以下のスクリーンショットを参照してください。ユーザーが `111` として OTP に入力し、「`Confirm`」ボタンをクリックすると、`User Details` パネルが表示されます。

![ 成功 ](/help/forms/assets/success.gif)

**メソッドのルール `Add Failure callback` 作成**

OTP が値 `111` と一致しない場合に失敗メッセージを表示するルールを作成しましょう。

1. **[!UICONTROL 失敗コールバックを追加]** をクリックします。

1. 「**[!UICONTROL ステートメントを追加]**」をクリックして、ルールを作成します。
1. ルールの **条件** セクションで条件を作成します。
1. **[!UICONTROL 関数出力]**/**[!UICONTROL イベントペイロードを取得]** を選択します。
1. 「**入力**」セクションから、対応する連結を選択します。 例えば、「**[!UICONTROL String]**」を選択して「`valid`」と入力します。 入力した文字列を `false` と比較します。
1. 「**Then**」セクションで、「**[!UICONTROL アクションを選択]**」ドロップダウンリストから **表示** を選択します。 例えば、`error message` テキストボックスを表示します。
1. 「**[!UICONTROL ステートメントを追加]**」をクリックします。
1. **[!UICONTROL アクションを選択]** ドロップダウンリストから **非表示** を選択します。 例えば、`userdetails` パネルを非表示にします。
1. 「**[!UICONTROL 完了]**」をクリックします。

![ 失敗コールバックメソッド ](/help/forms/assets/rule-editor-failure-callback.png){width=50%, height=50%}

以下のスクリーンショットを参照してください。ユーザーが `123` として OTP に入力し、「`Confirm`」ボタンをクリックするとエラーメッセージが表示されます。

![ 失敗 ](/help/forms/assets/failure.gif)

以下のスクリーンショットは、非同期関数を実装するための **[!UICONTROL 非同期関数呼び出し]** を使用する際の完全なルールを示しています。

![ 非同期関数呼び出しのルール ](/help/forms/assets/rule-editor-async-callbacks.png)

**[!UICONTROL 成功コールバックを編集]** および **[!UICONTROL 失敗コールバックを編集]** をクリックして、コールバックを編集することもできます。

## 関数出力のルールタイプの使用方法は？

また、同期関数を使用して、非同期関数を間接的に呼び出すこともできます。 同期関数は、アダプティブフォームのルールエディターで **[!UICONTROL 関数出力]** ルールタイプを使用して実行されます。

**[!UICONTROL 関数出力]** ルールタイプを使用して非同期関数を呼び出す方法については、以下のコードを参照してください。

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

上記の例では、asyncFunction 関数は `asynchronous function` です。`https://petstore.swagger.io/v2/store/inventory` に `GET` リクエストを送信して非同期操作を実行します。`await` を使用して応答を待機し、`response.json()` を使用して応答本文を JSON として解析し、データを返します。`callAsyncFunction` 関数は、`asyncFunction` 関数を呼び出してコンソールに応答データを表示する同期カスタム関数です。`callAsyncFunction` 関数は同期関数ですが、非同期の asyncFunction 関数を呼び出し、その結果を `then` および `catch` ステートメントで処理します。

動作を確認するには、ボタンを追加し、ボタンがクリックされたときに非同期関数を呼び出すボタンのルールを作成します。

![非同期関数のルールの作成](/help/forms/assets/rule-for-async-funct.png){width=50%}

ユーザーが「`Fetch`」ボタンをクリックすると、カスタム関数 `callAsyncFunction` が呼び出され、非同期関数 `asyncFunction` が呼び出されることを示すには、以下のコンソールウィンドウのスクリーンショットを参照してください。 コンソールウィンドウを調べて、ボタンクリックに対する応答を表示します。

![コンソールウィンドウ](/help/forms/assets/async-custom-funct-console.png)

## 関連トピック

{{see-also-rule-editor}}
