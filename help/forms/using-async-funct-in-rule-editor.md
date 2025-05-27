---
title: ビジュアルルールエディターで非同期関数呼び出しを使用する方法
description: ビジュアルルールエディターでの非同期関数呼び出し
feature: Adaptive Forms, Core Components
role: User, Developer
level: Beginner, Intermediate
exl-id: a240ba26-a6d8-4643-8acb-1d8812dac61f
source-git-commit: 2cae8bb1050bc4538f4645d9f064b227fb947d75
workflow-type: ht
source-wordcount: '1409'
ht-degree: 100%

---

# コアコンポーネントに基づくアダプティブフォームでの非同期関数の使用

[アダプティブフォームのルールエディター](/help/forms/rule-editor-core-components.md)では非同期関数をサポートしています。このため、フォームでのユーザーのインタラクションを中断することなく、外部プロセスやデータ取得を待つ必要がある操作を統合および管理できます。

## 非同期関数または同期関数の使用を決定する要因

スムーズなエクスペリエンスを作成するには、ユーザーインタラクションを効果的に管理することが重要です。操作を処理する一般的な方法には、同期関数と非同期関数の 2 つがあります。

**同期関数**&#x200B;は、タスクを順番に実行します。そのため、アプリケーションは各操作が完了するまで待機してから次の処理に進みます。これにより、遅延が発生し、ユーザーエクスペリエンスの評価が下がる可能性があります。特に、タスクにファイルのアップロードやデータの取得などの外部リソースの待機が含まれる場合にこの傾向が顕著です。

例えば、ユーザーが画像をアップロードするときにフォーム全体が停止し、アップロードが完了するのを待つシナリオを考えてみましょう。この停止により、ユーザーは他のフィールドでのインスタクションができなくなり、不満や遅延が生じます。画像が処理されるのを待っている間に、ユーザーが別の場所に移動したりイライラしたりした場合には、入力した情報が失われる可能性があり、面倒で非効率的な操作体験になります。

一方で、**非同期関数**&#x200B;を使用すると、タスクを同時に実行できます。つまり、ユーザーはバックグラウンドプロセスの実行中もアプリケーションの操作を続行できます。非同期操作により応答性が向上し、ユーザーは即座にフィードバックを受け取り、中断することなくエンゲージメントを維持できます。

逆に、非同期アプローチを使用すると、ユーザーはフォームの残りの部分をシームレスに入力し続けながら、バックグラウンドで画像をアップロードできます。インターフェイスの応答性が維持され、アップロードの進行に応じたリアルタイムの更新や迅速なフィードバックが可能となります。ユーザーエンゲージメントが強化され、中断のないスムーズなエクスペリエンスが実現します。

![非同期関数と同期関数](/help/forms/assets/sync-async.png){align=center}

## アダプティブフォームの非同期関数の実装

アダプティブフォームの非同期関数は、ルールエディターで次のルールタイプを使用して実装できます。

* [非同期関数呼び出し](#using-asynchronous-function-calls-in-the-visual-rule-editor)
* [関数の出力](#how-to-use-function-output-rule-type)

## 非同期関数呼び出しルールタイプの使用方法

非同期操作の[カスタム関数](/help/forms/custom-function-core-component-create-function.md)を記述し、ルールエディターで&#x200B;**[!UICONTROL 非同期関数呼び出し]**&#x200B;ルールタイプを使用して非同期関数を設定できます。

### ユースケースによる非同期関数呼び出しルールタイプの確認

ユーザーがワンタイムパスワード（OTP）を入力する web サイトの登録フォームについて考えてみます。ユーザーの詳細情報を追加するパネルは、正しい OTP を入力した後にのみ表示されます。OTP が正しくない場合、パネルは非表示のままになり、エラーメッセージが画面に表示されます。

![Login-form](/help/forms/assets/rule-editor-login-form.png) {width-50%}

登録フォームでは、ユーザーが「**確認**」ボタンをクリックすると `matchOTP()` 関数が非同期で呼び出され、入力した OTP が検証されます。`matchOTP()` 関数は[カスタム関数](/help/forms/custom-function-core-component-create-function.md)として実装されます。ルールエディターで&#x200B;**[!UICONTROL 非同期関数呼び出し]**&#x200B;ルールタイプを使用すると、アダプティブフォームのルールエディターで `matchOTP()` 関数を設定できます。また、成功コールバックと失敗コールバックをルールエディターで実装することもできます。

次の図は、**[!UICONTROL 非同期関数呼び出し]**&#x200B;ルールタイプを使用してアダプティブフォームの非同期関数を呼び出す手順を示しています。

![非同期関数を追加するワークフロー](/help/forms/assets/workflow-to-add-async-func.png){width=50%, align=center}

### 1. JS ファイルに非同期操作のカスタム関数を記述

>[!NOTE]
>
> * **非同期関数呼び出し**&#x200B;ルールタイプを選択すると、フォームのルールエディターに表示されるのは、戻り値の型が `Promise` の関数のみです。
> * カスタム関数の作成方法については、「[コアコンポーネントに基づくアダプティブフォームのカスタム関数の作成](/help/forms/custom-function-core-component-create-function.md)」の記事を参照してください。

`matchOTP()` 関数は、カスタム関数として実装されます。カスタム関数の JS ファイルに以下のコードが追加されます。

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

このコードは、ワンタイムパスワード（OTP）を非同期で検証するプロミスを生成する関数 `matchOTP()` を定義します。関数 `asyncOperationForOTPMatch()` を使用して、OTP 照合プロセスをシミュレートします。この関数は、指定された OTP が `111` と等しいかどうかを確認します。入力した OTP が正しい場合は、エラーに対する null と OTP が有効であることを示すオブジェクト `({'valid':'true'})` が指定されたコールバックを呼び出します。OTP が有効でない場合は、エラーオブジェクト `({'valid':'false'})` と結果に対する null が指定されたコールバックを呼び出します。

### 2. ルールエディターでの非同期関数の設定

ルールエディターで非同期関数を設定するには、次の手順を実行します。

1. [非同期関数呼び出しルールタイプを使用して、非同期関数を使用するルールを作成](#21-create-a-rule-to-use-asynchronous-function-using-the-async-function-call-rule-type)
1. [非同期関数のコールバックを実装](#22-implement-the-callbacks-for-asynchronous-function)

#### 2.1 非同期関数呼び出しルールタイプを使用して、非同期関数を使用するルールを作成

非同期操作を使用するルールを作成するには、**[!UICONTROL 非同期関数呼び出し]**&#x200B;ルールタイプを使用して、次の手順を実行します。

1. アダプティブフォームをオーサリングモードで開き、フォームコンポーネントを選択してから、**[!UICONTROL ルールエディター]**&#x200B;を選択してルールエディターを開きます。
1. 「**[!UICONTROL 作成]**」を選択します。
1. ボタンをクリックするための条件をルールの「**When**」セクションで作成します。例えば、「**When：[確認]**&#x200B;をクリック」のようになります。
1. 「**THEN**」セクションの&#x200B;**アクションを選択**&#x200B;ドロップダウンリストで「**[!UICONTROL 非同期関数呼び出し]**」を選択します。「**[!UICONTROL 非同期関数呼び出し]**」を選択すると、戻り値の型が `Promise` である関数が表示されます。
1. リストから非同期関数を選択します。例えば、`matchOTP()` 関数を選択すると、そのコールバックとして `Add success callback` および `add failure callback` が表示されます。
1. 次に、**[!UICONTROL 入力]**&#x200B;バインディングを選択します。例えば、**[!UICONTROL 入力]**&#x200B;として `Form Object` を選択し、「`OTP`」フィールドと比較します。

このルールは次のスクリーンショットのようになります。

![ルールタイプ](/help/forms/assets/asyn-function-rule-type.png)

これで、`matchOTP` 関数のコールバック `Success` と `Failure` を実装できるようになります。

#### 2.2 非同期関数のコールバックの実装

ビジュアルルールエディターを使用して、非同期関数の success および failure コールバックメソッドを実装します。

**`Add Success callback` メソッドのルールの作成**

OTP が値 `111` と一致する場合に `userdetails` パネルを表示するルールを作成します。

1. 「**[!UICONTROL 成功コールバックを追加]**」をクリックします。
1. 「**[!UICONTROL ステートメントを追加]**」をクリックして、ルールを作成します。
1. ルールの「**When**」セクションで条件を作成します。
1. **[!UICONTROL 関数の出力]**／**[!UICONTROL イベントペイロードを取得]**&#x200B;を選択します。

   >[!NOTE]
   >
   > 「**[!UICONTROL イベントペイロードを取得]**」関数は、特定のイベントに関連付けられたデータを取得して、ユーザーのインタラクションを動的に管理します。

1. 「**入力**」セクションから、対応するバインディングを選択します。例えば、「**[!UICONTROL 文字列]**」を選択して `valid` と入力します。入力した文字列を `true` と比較します。
1. 「**THEN**」セクションの&#x200B;**アクションを選択**&#x200B;ドロップダウンリストで「**[!UICONTROL 表示]**」を選択します。例えば、`userdetails` パネルを表示します。
1. 「**[!UICONTROL ステートメントを追加]**」をクリックします。
1. **[!UICONTROL アクションを選択]**&#x200B;ドロップダウンリストから「**非表示**」を選択します。例えば、「`error message`」テキストボックスを非表示にします。
1. 「**[!UICONTROL 完了]**」をクリックします。

![成功時の呼び出し](/help/forms/assets/rule-editor-success-callback.png){width=50%, height=50%}

以下のスクリーンショットを参照してください。ユーザーが OTP として `111` を入力し、「`Confirm`」ボタンをクリックすると、`User Details` パネルが表示されます。

![成功](/help/forms/assets/success.gif)

**`Add Failure callback` メソッドのルールの作成**

OTP が値 `111` と一致しない場合に失敗メッセージを表示するルールを作成しましょう。

1. 「**[!UICONTROL 失敗コールバックを追加]**」をクリックします。

1. 「**[!UICONTROL ステートメントを追加]**」をクリックして、ルールを作成します。
1. ルールの「**When**」セクションで条件を作成します。
1. **[!UICONTROL 関数の出力]**／**[!UICONTROL イベントペイロードを取得]**&#x200B;を選択します。
1. 「**入力**」セクションから、対応するバインディングを選択します。例えば、「**[!UICONTROL 文字列]**」を選択して `valid` と入力します。入力した文字列を `false` と比較します。
1. 「**THEN**」セクションの&#x200B;**アクションを選択**&#x200B;ドロップダウンリストで「**[!UICONTROL 表示]**」を選択します。例えば、`error message` テキストボックスを表示します。
1. 「**[!UICONTROL ステートメントを追加]**」をクリックします。
1. **[!UICONTROL アクションを選択]**&#x200B;ドロップダウンリストから「**非表示**」を選択します。例えば、`userdetails` パネルを非表示にします。
1. 「**[!UICONTROL 完了]**」をクリックします。

![失敗コールバックメソッド](/help/forms/assets/rule-editor-failure-callback.png){width=50%, height=50%}

以下のスクリーンショットを参照してください。ユーザーが OTP として `123` を入力し、「`Confirm`」ボタンをクリックすると、エラーメッセージが表示されます。

![失敗](/help/forms/assets/failure.gif)

以下のスクリーンショットは、非同期関数を実装するための&#x200B;**[!UICONTROL 非同期関数呼び出し]**&#x200B;を使用する際の完全なルールを示しています。

![非同期関数呼び出しのルール](/help/forms/assets/rule-editor-async-callbacks.png)

「**[!UICONTROL 成功コールバックを編集]**」および「**[!UICONTROL 失敗コールバックを編集]**」をクリックして、コールバックを編集することもできます。

## 関数の出力ルールタイプの使用方法は

また、同期関数を使用して、非同期関数を間接的に呼び出すこともできます。 同期関数は、アダプティブフォームのルールエディターで&#x200B;**[!UICONTROL 関数の出力]**&#x200B;ルールタイプを使用して実行されます。

**[!UICONTROL 関数の出力]**&#x200B;ルールタイプを使用して非同期関数を呼び出す方法については、以下のコードを参照してください。

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

動作を確認するために、ボタンを追加し、ボタンのクリック時に非同期関数を呼び出すボタンのルールを作成しましょう。

![非同期関数のルールの作成](/help/forms/assets/rule-for-async-funct.png){width=50%}

次のコンソールウィンドウのスクリーンショットを参照してください。ユーザーが `Fetch` ボタンをクリックすると、カスタム関数 `callAsyncFunction` が呼び出され、次に非同期関数 `asyncFunction` が呼び出されます。コンソールウィンドウを調べて、ボタンをクリックした際の応答を確認します。

![コンソールウィンドウ](/help/forms/assets/async-custom-funct-console.png)

## 関連トピック

{{see-also-rule-editor}}
