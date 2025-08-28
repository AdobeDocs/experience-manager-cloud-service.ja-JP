---
title: ルールを使用してフォームに動的な動作を追加
description: AEM Forms の Edge Delivery Services は、ピークパフォーマンスを発揮するように構築されており、ユーザーは合理化されたデータ収集とユーザーエンゲージメントの今後を思い描くことができます。ルールを使用してフォームに動的な動作を追加
feature: Edge Delivery Services
exl-id: 58042016-e655-446f-a2bf-83f1811525e3
role: Admin, Architect, Developer
source-git-commit: 2e2a0bdb7604168f0e3eb1672af4c2bc9b12d652
workflow-type: ht
source-wordcount: '2218'
ht-degree: 100%

---

# ルールを使用してフォームに動的な動作を追加

スプレッドシートを使用してフォームを作成する強力な機能の 1 つは、ビルトインのスプレッドシート関数を使用してルールを作成できることです。これにより、フォームフィールドの条件付きの表示と非表示、ユーザー入力に基づく計算の自動化、より動的なユーザーエクスペリエンスの作成が可能になります。

この記事では、様々なアダプティブフォームブロックプロパティ、主に[`Visible`](#visible-property)、[`Visibility Expression`](#visible-expression-property)、[`Value Expression`](#value-expression-property) プロパティと[スプレッドシート関数](#spreadsheet-functions-for-rules)を使用して、フォームに効果的なルールを作成する方法を説明します。また、これらのルールを実際にどのように実装できるかを説明するいくつかの例も見ていきます。

## ルールの構成について

ルールとは、様々な状況で何をすべきかを教えてくれる手順のようなものです。一般的なルールの構文を以下に示します。

- 条件：ルールを適用する条件を指定します。回答（はい／いいえ）が必要な質問と考えてください。

- アクション：条件が満たされた場合（true）と満たされなかった場合（false）の動作を定義します。


例えば、チェックボックスが選択されているときにメールボックスを表示するには、次のようにします。

- 条件：「雑誌やアクティビティの購読を希望しますか？」チェックボックスが選択されている（はい／いいえ）。この条件はフォームの `Visible` プロパティで設定されます。
- アクション（True）：メールボックスが表示される（はいの場合）。`Visibility Expression` は、`visible` プロパティに定義された条件を使用してフィールドを動的に表示します。
- アクション（False）：メールボックスは非表示（いいえの場合）。`Visibility Expression` は、`Value` に定義された条件を使用してフィールドを動的に非表示にします。

詳細な手順については、[条件に基づくメールフィールドの表示/非表示](#example-1-conditional-email-field)を参照してください。


## Value、Visible、Visibility Expression、および Value Expression のプロパティについて

### Visible プロパティ

フォームフィールドの照明スイッチを想像してみてください。`Visible` プロパティはスイッチに似ており、フィールドが最初に読み込まれたときにフォーム上に最初に表示されるかどうかを制御します。

- True（照明スイッチが「オン」になっている場合など）：フィールドがフォームに表示される。
- False（照明スイッチが「オフ」になっている場合など）：フィールドがフォーム上で非表示になる。

SpreadSheet 式（= タグを含む）を使用すると、スプレッドシートのようなロジックを用いてフィールドの表示／非表示を決定する式を作成できます。この数式内では、フォーム内の他のフィールドの値を使用できます。例えば、ユーザーが登録タイプフィールドで「個人」を選択した場合、その値を確認する式を使用して、メールフィールドを非表示にできます。

### Visible Expression プロパティ（フィールドの表示／非表示）

`Visible Expression` プロパティを使用すると、`Visible`プロパティに追加されたルールを使って、ユーザーの操作に基づいてフィールドを表示するか非表示にするかを決定できます。

`=FORMULATEXT("Address of the corresponding Visible property)` を使用して、`Visible` プロパティで指定された式を文字列として `Visible Expression` プロパティフィールドに取り込みます。公開済みフォームでフィールドを動的に表示または非表示にするために必要です。

![Forumaltext](/help/edge/assets/aem-forms-formulatext.png)

### Value プロパティ（初期データの設定）

部屋の照明の調光スイッチに事前に設定された値を想像してください。`Value` プロパティも同様で、ユーザーがフィールドに表示するデータの初期状態を決定します。フォームフィールド内に表示する現在のデータを設定または取得します。

フォームの初回読み込み時、`Value` プロパティは、ユーザーが変更を行う前にフィールドに表示する内容を決定します。表示を制御する `Visible` プロパティや `Visible Expression` プロパティとは異なり、値プロパティはデータ自体に直接影響します。ユーザーは、入力するか、オプション（ドロップダウンメニュー）を選択するか、フィールドを操作して、この値を変更できます。

Excel の数式（= タグを含む）を使用すると、スプレッドシートのようなロジックを使用して数式を書き込み、フィールドに表示する値を決定できます。この数式内では、フォーム内の他のフィールドの値を使用できます。例えば、別のフィールドに入力した注文数量に基づいて割引を自動的に計算できます。


### 値式プロパティ（フィールドに表示する値の計算）

このプロパティを使用すると、表示式と同様に、数式に基づいてフィールド内に表示する値を制御できます。フィールドに組み込まれた計算機を想像してください。

`=FORMULATEXT("Address of the corresponding Value property)` を使用して、`Value` プロパティに記載されている数式を文字列として `Value Expression` プロパティフィールドに取り込みます。これは、動的に計算し、計算した値を公開済みフォームに表示するために必要です。

![Forumaltext](/help/edge/assets/aem-forms-formulatext-value.png)

これらの概念を具体化する例を次に示します。

- 表示：家のような形を想像してください。「表示」プロパティは、各部屋（フィールド）のライトスイッチに似ています。別のユーザーが家に入った際（フォームを開いた際）、最初に部屋を明るくする（表示する）か暗くする（非表示にする）かを決定します。
- 表示式：モーションセンサーのライトスイッチに似ています。部屋（フィールド）は最初は暗い（非表示の）可能性がありますが、別のユーザーが通りかかる（別のフィールドの値を変更する）と、数式（モーションセンサー）によってオンになる（フィールドが表示される）ことがあります。
- 値：ライトの事前設定済み調光スイッチ（フィールドの初期データ）に似ています。ユーザーは明るさを調整（値を変更）できます。
- 値式：家の中にある製品の価格タグに組み込まれた高度な計算機（フォーム）に似ています。価格タグ（フィールド）には、基本価格（別のフィールドの値）などの他の情報を使用する数式（例えば、基本価格への税金の加算）に基づいた最終価格が表示されます。

これらのプロパティを[スプレッドシート関数](#spreadsheet-functions-for-rules)と組み合わせて、フォーム内で様々な動的動作を実現できます。

## ルールのスプレッドシート関数

アダプティブフォームブロックは、ルールの作成に使用できる様々なスプレッドシート関数をサポートします。標準（OOTB）の関数を次に示します。

### 論理関数

- [NOT()](https://docs.oasis-open.org/office/v1.2/os/OpenDocument-v1.2-os-part2.html#__RefHeading__1018452_715980110)：論理状態を逆にします（TRUE は FALSE になり、その逆も同様です）。
- [AND()](https://docs.oasis-open.org/office/v1.2/os/OpenDocument-v1.2-os-part2.html#AND)：指定したすべての条件が TRUE の場合にのみ TRUE を返します。
- [OR()](https://docs.oasis-open.org/office/v1.2/os/OpenDocument-v1.2-os-part2.html#OR)：指定した条件の少なくとも 1 つが TRUE の場合、TRUE を返します。

### 条件付き関数

- [IF()](https://docs.oasis-open.org/office/v1.2/os/OpenDocument-v1.2-os-part2.html#__RefHeading__1018446_715980110)：条件を評価し、TRUE の場合は特定の値を返し、FALSE の場合は別の値を返します。

### 数学関数

- [SUM()](https://docs.oasis-open.org/office/v1.2/os/OpenDocument-v1.2-os-part2.html#SUM)：指定したセル範囲から値を加算します。
- [ROUND()](https://docs.oasis-open.org/office/v1.2/os/OpenDocument-v1.2-os-part2.html#ROUND)：数値を指定した小数点の桁数に四捨五入します。
- [MIN()](https://docs.oasis-open.org/office/v1.2/os/OpenDocument-v1.2-os-part2.html#MIN)：指定したセル範囲から最小値を返します。

## ルールの作成

ルールを使用してフォームを強化する方法を説明するために、実用的な例を見てみましょう。

## 例 1：条件付きメールフィールド

次の例に、チェックボックスが条件として機能する方法を示します。選択すると（条件が true）、メールボックスが表示されます（アクションが true の場合）。選択しないと（条件が false）、メールボックスは非表示のままになります（アクションが false の場合）。

次の画像に示すように、チェックボックスとメールボックスを含むフォームを作成します。

![条件付きメールフォーム](/help/edge/assets/aem-forms-conditional-email-form.png)


ルールを使用して、チェックボックスの選択時に「メール」フィールドを表示する方法を次に示します。

1. 「チェックボックス」フィールドの `Value` プロパティを `TRUE` に設定します。
1. 「チェックボックス」フィールドの `Checked` プロパティを `FALSE` に設定します。これにより、デフォルトではチェックボックスが選択されなくなります。
1. 「メール」フィールドの `Visible` プロパティを `=[address of Checked property of the checkbox field] = true()` に設定します。例えば、`=Q11=TRUE()` です。式はチェックボックスが選択されているかどうかを評価します。チェックボックスが選択されている場合、式は TRUE と評価します。チェックボックスが選択されていない場合、式は FALSE と評価します。



   `TRUE()` 関数は、`Checked` プロパティを指すように設定されている場合に論理値を返し、`checked = false` の場合は FALSE を返します。`checked=true` の場合は `true` を返します。これにより、「メール」フィールドがデフォルトで非表示になります。


1. 「チェックボックス」フィールドの `Visible Expression` プロパティを `=FORMULATEXT ((address of Visible property of the checkbox field))` に設定します。例えば、`=FORMULATEXT((G12))` のようになります。FORMULATEXT() 関数は式を入力として取り、式自体を文字列として返します。これは、フォーム内で式を使用するのに役立ちます。

   ![条件付き「メール」フィールド](/help/edge/assets/aem-forms-visible-expression-formula-text.png)

1. フォームをプレビューおよび公開します。これで、チェックボックスを選択すると「メール」フィールドが表示される一方で、選択を解除すると「メール」フィールドが非表示になり、動的なユーザーエクスペリエンスが提供されるようになります。

   ![条件付きメール](/help/edge/assets/aem-forms-coditional-email.gif)


## 例 2：自動計算

この例では、フォームで旅行の日付を選択する際に、旅費の見積もりが自動的に計算される方法を示します。

以下の画像に示されるように、日付フィールド、部屋の予算、旅費の見積もりの各フィールドとメールボックスを含むフォームを作成します。

![条件付きメールフォーム](/help/edge/assets/aem-forms-automatic-calculations-form.png)

これは、旅費の見積もりが自動的に計算される方法を示します。

1. 「`amount`」フィールドの `Value` プロパティを `=F6*DAYS(F3,F2)` に設定します。この式は、`Start Date` と `End Date` から日数を計算し、部屋の予算と日数を掛け合わせ、結果を「`Estimated Trip Cost`」フィールドに表示します。

1. 「`Estimated Trip Cost`」フィールドの `Value Expression` プロパティを `=FORMULATEXT ((address of value property of the amount field))` に設定します。例えば、`=FORMULATEXT(F7)` のようになります。FORMULATEXT() 関数は式を入力として取り、式自体を文字列として返します。これは、フォーム内で式を使用するのに役立ちます。

1. フォームをプレビューおよび公開します。ここで、`Start Date`、`End Date` および部屋の予算を指定します。`Estimated Trip Cost` が自動的に計算されます。

## スプレッドシート関数の例


一般的に使用されるスプレッドシート関数の例を次に示します。

**論理関数：**

- **NOT()：** 論理状態を反転させます（TRUE は FALSE になり、FALSE は TRUE になります）。

  例：「メール」フィールドが空白の場合に「メールを確認」フィールドを非表示にします。

   1. 「メールを確認」フィールドの `Visible` プロパティを `=NOT(if('address of email field'=""))` に設定します。

      ![AEM Forms での「メールを確認」フィールドの非表示](/help/edge/assets/aem-forms-not-function-hide-email-field.png)


   1. 「メールを確認」フィールドの表示される式を `=FORMULATEXT ((address of visible property of the Confirm Email field))` に設定します。

      ![AEM Formsに表示される式](/help/edge/assets/aem-forms-visible-expression-formula-text.png)


- AND()：指定したすべての条件が TRUE の場合にのみ TRUE を返します。

   - 例：すべての必須フィールドに値が入力されている場合にのみ「送信」ボタンを有効にします。

   1. 「送信」ボタンの `Visible` プロパティを次のように設定します。



      ```JavaScript
      =AND(NOT(address of `value` property of the `name` field = ""), NOT(address of `value` property of the `email` field = ""), NOT(address of `value` property of the `phone` field))
      ```

      例：

      ```JavaScript
      =AND(NOT(F9=""), NOT(F12=""), NOT(F10=""))
      ```

   1. 「メールを確認」フィールドの表示される式を次のように設定します。

      ```JavaScript
      =FORMULATEXT ((address of visible property of the Confirm Email field))
      ```

      例：

      ```JavaScript
      =FORMULATEXT(G14)
      ```

      この式は、すべてのフィールド（名前、メール、電話）に値が入力されている場合にのみ「送信」ボタン（TRUE）を表示し（NOT(()) がそれぞれに TRUE を返す）、そうでない場合はボタンを非表示にします（AND(multiple FALSES) = FALSE）。

- OR()：指定された条件の少なくとも 1 つが TRUE の場合に TRUE を返します。

   - 例：ユーザーが適用可能な割引クーポンコードのいずれかを入力した場合に割引を適用します。

   1. 「最終金額」フィールドの `Visible` プロパティを次のように設定します。


  ```JavaScript
     =IF(OR(F14="BlackFridaySale", F14="NewYearDiscount"), (F6*DAYS(F3,F2)* 0.7) , (F6*DAYS(F3,F2)))
  ```

   1. 「メールを確認」フィールドの値式を次のように設定します。

      ```JavaScript
      =FORMULATEXT ((address of value property of the final amount field))
      ```

      例：

      ```JavaScript
      =FORMULATEXT(F7)
      ```

      この数式では、ユーザーがクーポンコード（couponCode = &quot;New YearDiscount&quot;）または（couponCode = &quot;BlackFridaySale&quot;）を入力した場合は 30％の割引を計算し、それ以外の場合は割引を 0 に設定します。

**テキスト関数：**

- IF()：条件を評価し、TRUE の場合は特定の値を返し、FALSE の場合は別の値を返します。

   - 例：選択した製品カテゴリに基づいてカスタムメッセージを表示します。

   1. 「`message`」フィールドの `Value` プロパティを `Only upto 7 kg check-in lagguage is allowed!` に設定します。

   1. 「`message`」フィールドの `Visible` プロパティを次のように設定します。


      ```JavaScript
      =if(address of value property of chosen product category ="Economy", TRUE(), FALSE())
      ```

      例：

      ```JavaScript
      =if(F5="Economy", TRUE(), FALSE())
      ```

   1. 「`message`」フィールドの値式を次のように設定します。

      ```JavaScript
      =FORMULATEXT ((address of value property of the final amount field))
      ```

      例：

      ```JavaScript
      =FORMULATEXT(G15)
      ```

      この数式では、選択したクラスが「エコノミー」の場合は「7 kg までのチェックイン荷物のみが許可されています」というメッセージが表示され、それ以外の場合は「メッセージ」フィールドが空白のままになります。

**数学関数：**

- SUM()：指定したセル範囲から値を加算します。

  例：買い物かご内の商品の合計コストを計算します。

  「合計コスト」フィールドの値式：
SUM(価格 * 数量)

  この数式は、各商品の「価格」と「数量」に個別のフィールドがあることを前提としています。これらを乗算し、SUM() を使用して買い物かご内のすべての商品の合計コストを合計します。

- ROUND()：数値を指定した小数点の桁数に四捨五入します。

  例：計算された割引額を小数点以下第 2 位に四捨五入します。

  「割引額」フィールドの値式（割引が別の場所で計算されると仮定）：
ROUND(discount, 2)

  この数式は、割引値を小数点以下第 2 位にに四捨五入します。

- MIN()：指定したセル範囲から最小値を返します。

  例：選択した国に基づいて、サインアップフォームに必要な最低年齢を検索します。

  「最低年齢」フィールドの値式：
MIN(ageLimits[&quot;米国&quot;], ageLimits[&quot;英国&quot;], ageLimits[&quot;フランス&quot;])

  この数式は、様々な国の最低年齢要件を格納する「ageLimits」という名前のテーブルがあることを前提としています。MIN() を使用すると、これらの中から最小値を検索できます。


さらに、アダプティブフォームブロックを使用すると、[カスタム関数](#creating-custom-functions)を作成してフォームを完全に管理できます。カスタム関数を使用すると、独自のルールとロジックを定義して、フォームの動作を完全に制御できます。


## カスタム関数の作成およびデプロイ

標準（OOTB）のアダプティブフォームブロックでは、多くの[一般的なスプレッドシート関数](#spreadsheet-functions-for-rules)の実装を提供します。ただし、フォームをより詳細に制御するには、アダプティブフォームブロック内で Microsoft® Excel または Google Sheets で使用できる OOTB 関数のいずれかを使用できます。アダプティブフォームブロックには、Microsoft® Excel または Google Sheets で使用できるすべての OOTB 関数の実装が含まれていません。このような関数が必要な場合は、同様の構文を使用してカスタム関数を開発し、Microsoft® Excel または Google Sheets が提供する機能を実現できます。例えば、[Microsoft® Excel の Year() 関数](https://support.microsoft.com/en-us/office/calculate-age-113d599f-5fea-448f-a4c3-268927911b37#)を実装して、生年月日から年齢を計算できます。


### カスタム関数の作成

カスタム関数は `[Adaptive form block]/functions.js` ファイルにあります。作成プロセスには通常、次の手順が含まれます。

- 関数宣言：関数名とそのパラメーター（受け入れる入力）を定義します。
- ロジック実装：関数で実行される特定の計算や操作の概要を説明するコードを書き込みます。
- 関数の書き出し：関連ファイルから関数を書き出して、ルール内で関数にアクセスできます。

### 例：Year 関数

この例では、Microsoft® Excel の YEAR() 関数を模倣して年齢を計算する 2 つのカスタム関数を示します。


```JavaScript
/**
 - Get the current date and time
 - @name now
 - @returns {Date} The current date and time as a Date object
 */
function now() {
  const today = new Date();
  return today;
}

/**
 - Get the year from a Date object
 - @name year
 - @param {Date} date The date object
 - @throws {TypeError} If the input is not a Date object
 - @returns {number} The year as a number
 */
function year(date) {
  let inputDate = new Date(date)

  if (!(inputDate instanceof Date)) {
    throw new TypeError("Input must be a Date object");
  }

  const year = inputDate.getFullYear();

  return year;
}

// Make the function accessible for use in rules
export { now, year };
```

### フォームでのカスタム関数の使用

フォームでカスタム関数を使用するには、次の手順に従います。

1. **関数を追加**：カスタム関数を `[Adaptive form block]/functions.js` ファイルに含めます。必ず、ファイル内の export ステートメントに追加します。
1. **ファイルをデプロイ**：更新された `functions.js` ファイルを GitHub プロジェクトにデプロイし、ビルドが成功したことを確認します。
1. **関数の使用**：OOTB をサポートする他のスプレッドシート関数と同様に、`Value`、`Value Expression`、`Visible` または `Visible Expression` プロパティを使用してフォームのスプレッドシート内の関数にアクセスします。
1. **フォームをプレビュー**：AEM Sidekick を使用して、新しく実装された関数でフォームをプレビューします。

