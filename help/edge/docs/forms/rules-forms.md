---
title: ルールを使用したフォームへの動的動作の追加
description: AEM Forms Edge Delivery Servicesは最高のパフォーマンスを実現するために構築されており、合理化されたデータ収集とユーザーエンゲージメントの将来を思い描くことができます。 ルールを使用すると、フォームに動的な動作を追加できます。
feature: Edge Delivery Services
exl-id: 58042016-e655-446f-a2bf-83f1811525e3
source-git-commit: 2affe155b285986128487043fcc4f2938fc15842
workflow-type: tm+mt
source-wordcount: '2216'
ht-degree: 0%

---

# ルールを使用したフォームへの動的動作の追加

スプレッドシートを使用してフォームを作成する強力な機能の 1 つは、組み込みのスプレッドシート関数を使用してルールを作成する機能です。この機能を使用すると、フォームフィールドの条件付きの表示と非表示、ユーザー入力に基づく計算の自動化、より動的なユーザーエクスペリエンスの作成が可能になります。

この記事では、主に様々なアダプティブフォームブロックプロパティの使用方法について説明します [`Visible`](#visible-property), [`Visibility Expression`](#visible-expression-property) および [`Value Expression`](#value-expression-property) プロパティと [スプレッドシート関数](#spreadsheet-functions-for-rules) フォームに効果的なルールを作成するため また、これらのルールを実際にどのように実装できるかを説明するいくつかの例も見ていきます。

## ルールの構成を理解する

ルールとは、様々な状況で何をすべきかを教えてくれる指示のようなものです。 一般的なルールの構文を以下に示します。

* 条件：ルールを適用する条件を指定します。 回答が必要な質問（はい、いいえ）と考えてください。

* アクション：条件が満たされた（true）場合と満たされなかった（false）場合の動作を定義します。


例えば、チェックボックスが選択されているときにメールボックスを表示するには、次のようにします。

* 条件：「雑誌とアクティビティを購読しますか？」 チェックボックスが選択されています。 （イエスかノーか）。 この条件は `Visible` フォームのプロパティ。
* アクション（True）：メールボックスが表示されます。 （ある場合はどうなる）。 この `Visibility Expression`  に定義された条件を使用 `visible` フィールドを動的に表示するプロパティ。
* アクション（False）：メールボックスは非表示です。 （ない場合の処理）。 この `Visibility Expression`  に定義された条件を使用 `Value` でフィールドを動的に非表示にします。

詳細な手順については、を参照してください [条件に基づいてメールフィールドを表示/非表示](#example-1-conditional-email-field)


## 値、表示、表示式、値式の各プロパティについて

### Visible プロパティ

フォームフィールドのライトスイッチを想像してみてください。 この `Visible` プロパティはスイッチに似ており、フィールドが最初に読み込まれたときにフォームに最初に表示されるかどうかを制御します。

* True （光スイッチが「オン」の場合と同様）：フィールドがフォームに表示されます。
* False （ライトスイッチが「オフ」の場合と同様）：フィールドがフォーム上で非表示になります。

SpreadSheet 式（= タグを含む）を使用して、スプレッドシートのようなロジックを使用してフィールドの表示を決定する式を記述できます。 フォームの他のフィールドの値を、この数式内で使用できます。 例えば、ユーザーが登録タイプフィールドで「個人」を選択した場合、その値を確認する式を使用して、メールフィールドを非表示にできます。

### Visible Expression プロパティ （フィールドの表示/非表示）

この `Visible Expression` プロパティを使用すると、に追加されたルールを使用できます `Visible` ユーザーの操作に基づいてフィールドを表示するか非表示にするかを決定するプロパティ。

の使用 `=FORMULATEXT("Address of the corresponding Visible property)` に記載されている式を取り入れる `Visible` 文字列としてのプロパティ `Visible Expression` プロパティフィールド。 公開済みフォームでフィールドを動的に表示または非表示にするために必要です。

![Forumaltext](/help/edge/assets/aem-forms-formulatext.png)

### Value プロパティ （初期データを設定）

部屋の照明の調光スイッチに事前に設定された値を想像してください。 この `Value` プロパティは類似しており、ユーザーにフィールドに表示されるデータの初期状態を決定します。  フォームフィールド内に表示されている現在のデータを設定または取得します。

フォームの初回読み込み時、 `Value` プロパティは、ユーザーが変更を加える前にフィールドに表示する内容を指定します。 と異なる `Visible` および `Visible Expression` 表示を制御するプロパティ。Value プロパティはデータ自体に直接影響します。 ユーザーは、フィールドに入力したり、オプションを選択（ドロップダウンメニュー）したり、フィールドを操作したりして、この値を変更できます。

Excel の数式（= タグを含む）を使用して、スプレッドシートのようなロジックを使用して数式を記述し、フィールドに表示される値を決定できます。 フォームの他のフィールドの値を、この数式内で使用できます。 例えば、別のフィールドに入力された注文金額に基づいて割引を自動的に計算できます。


### 値式プロパティ（フィールドに表示される値を計算）

このプロパティを使用すると、表示される式と同様に、式に基づいてフィールドに表示される値を制御できます。 フィールドに組み込まれた電卓を想像してください。

の使用 `=FORMULATEXT("Address of the corresponding Value property)` に記載されている式を取り入れる `Value` 文字列としてのプロパティ `Value Expression` プロパティフィールド。 公開済みフォームで計算値を動的に計算して表示する場合に必要です。

![Forumaltext](/help/edge/assets/aem-forms-formulatext-value.png)

次に、これらの概念を具体化する例を示します。

* 表示：家のような形を想像してください。 「可視」プロパティは、各部屋（フィールド）のライト スイッチに似ています。 誰かが家に入ったとき（フォームを開いたとき）に、部屋が最初は明るい（表示）か暗い（非表示）かを決定します。
* Visible Expression：これはモーション センサのライト スイッチのようなものです。 部屋（フィールド）は最初は暗い（非表示）場合がありますが、誰かが歩いて行く（別のフィールドの値を変更する）と、式（モーションセンサー）がオンにする（フィールドを表示する）ことができます。
* 値：これは、ライト（フィールドの初期データ）の事前設定済みディマースイッチのようなものです。 その後、ユーザーは明るさを調整（値を変更）できます。
* 値の式：これは、家の中の製品の価格タグに組み込まれた高度な計算のようなものです（フォーム）。 価格タグ（フィールド）は、基本価格（別のフィールドからの値）などの他の情報を使用する式（例えば、基本価格に税金を追加するなど）に基づいて最終価格を表示します。

これらのプロパティをと組み合わせることで、 [スプレッドシート関数](#spreadsheet-functions-for-rules)を使用すると、フォーム内で様々な動的動作を実現できます。

## ルールのスプレッドシート関数

アダプティブFormsブロックは、ルールの作成に使用できる様々なスプレッドシート関数をサポートしています。 標準搭載（OOTB）の関数を次に示します。

### 論理関数

* [NOT （）](https://docs.oasis-open.org/office/v1.2/os/OpenDocument-v1.2-os-part2.html#__RefHeading__1018452_715980110)：論理状態を逆にします（TRUE は FALSE になり、その逆も同様です）。
* [AND （）](https://docs.oasis-open.org/office/v1.2/os/OpenDocument-v1.2-os-part2.html#AND)：指定されたすべての条件が TRUE の場合にのみ TRUE を返します。
* [OR （）](https://docs.oasis-open.org/office/v1.2/os/OpenDocument-v1.2-os-part2.html#OR)：指定された条件の少なくとも 1 つが TRUE の場合、TRUE を返します。

### 条件付き関数

* [IF （）](https://docs.oasis-open.org/office/v1.2/os/OpenDocument-v1.2-os-part2.html#__RefHeading__1018446_715980110)：条件を評価し、TRUE の場合は特定の値を返し、FALSE の場合は別の値を返します。

### 数学関数

* [SUM （）](https://docs.oasis-open.org/office/v1.2/os/OpenDocument-v1.2-os-part2.html#SUM)：指定したセル範囲の値を加算します。
* [ROUND （）](https://docs.oasis-open.org/office/v1.2/os/OpenDocument-v1.2-os-part2.html#ROUND)：数値の端数を、指定された小数点以下の桁数に丸めます。
* [MIN （）](https://docs.oasis-open.org/office/v1.2/os/OpenDocument-v1.2-os-part2.html#MIN)：指定したセル範囲の最小値を返します。

## ルールの作成

ルールを使用してフォームを強化する方法を説明するために、実用的な例を見てみましょう。

## 例 1：条件付きメールフィールド

次の例は、チェックボックスが条件として機能する方法を示しています。 選択（条件が true）されると、メールボックスが表示されます（アクションが true の場合）。 選択されていない（条件が false の）場合、メールボックスは非表示のままになります（アクションが false の）。

次の画像に示すように、チェックボックスとメールボックスを使用してフォームを作成します。

![条件付きメールフォーム](/help/edge/assets/aem-forms-conditional-email-form.png)


ルールを使用して、チェックボックスの選択時に「メール」フィールドを表示する方法を以下に示します。

1. を `Value` チェックボックスフィールドのプロパティを `TRUE`.
1. を `Checked` チェックボックスフィールドのプロパティを `FALSE`. これにより、このチェックボックスはデフォルトで選択されなくなります。
1. を `Visible` メールフィールドのプロパティの送信先 `=[address of Checked property of the checkbox field] = true()`. 例えば、`=Q11=TRUE()` です。式は、チェックボックスが選択されているかどうかを評価します。 このチェックボックスが選択されている場合、式は TRUE と評価されます。 チェックボックスが選択されていない場合、式は FALSE と評価されます。



   この `TRUE()` 関数。論理値を返します。 `Checked` プロパティ（の場合） `checked = false` false を返します。 次の場合 `checked=true`を返します。 `true`. これにより、メールフィールドがデフォルトで非表示になります。


1. を `Visible Expression` チェックボックスフィールドのプロパティを `=FORMULATEXT ((address of Visible property of the checkbox field))`. 例えば、`=FORMULATEXT((G12))` のようになります。 FORMULATEXT （）関数は数式を入力として受け取り、数式自体を文字列として返します。 これは、フォーム内で式を使用するのに役立ちます。

   ![条件付きメールフィールド](/help/edge/assets/aem-forms-visible-expression-formula-text.png)

1. フォームをプレビューして公開します。 これで、チェックボックスを選択すると、「メール」フィールドが表示されるのに対して、選択を解除すると「メール」フィールドが非表示になり、動的なユーザーエクスペリエンスが提供されるようになります。

   ![条件付きメール](/help/edge/assets/aem-forms-coditional-email.gif)


## 例 2：自動計算

次の使用例では、フォームでトリップの日付を選択したときに、フォームでトリップの見積原価が自動的に計算される方法を示します。

次の画像に示すように、日付フィールド、部屋予算、推定トリップコストの各フィールドとメールボックスを含むフォームを作成します。

![条件付きメールフォーム](/help/edge/assets/aem-forms-automatic-calculations-form.png)

自動計算を実行してトリップの見積原価を表示する方法を次に示します。

1. を `Value` のプロパティ `amount` フィールド先 `=F6*DAYS(F3,F2)`. この式は、次の式から日数を計算します `Start Date`  および `End Date`、部屋予算と日数を乗算し、結果を次の形式で表示 `Estimated Trip Cost` フィールド。

1. を `Value Expression` のプロパティ `Estimated Trip Cost` フィールド先 `=FORMULATEXT ((address of value property of the amount field))`. 例えば、`=FORMULATEXT(F7)` のようになります。 FORMULATEXT （）関数は数式を入力として受け取り、数式自体を文字列として返します。 これは、フォーム内で式を使用するのに役立ちます。

1. フォームをプレビューして公開します。 ここで、を指定すると、 `Start Date`, `End Date`、および部屋の予算。 この `Estimated Trip Cost` が自動計算されます。

## スプレッドシート関数の例


一般的に使用されるスプレッドシート関数の例を次に示します。

**論理関数：**

* **NOT （）:** 論理状態を反転します（TRUE は FALSE になり、その逆も同様です）。

  例：メールフィールドが空白の場合に「Confirm Email」フィールドを非表示にする

   1. を `Visible` 「Confirm Email」フィールドのプロパティ `=NOT(if('address of email field'=""))`.

      ![AEM Formsの「確認メール」フィールドを非表示](/help/edge/assets/aem-forms-not-function-hide-email-field.png)


   1. 「メールを確認」フィールドの表示可能な式をに設定します `=FORMULATEXT ((address of visible property of the Confirm Email field))`

      ![AEM Formsに表示される式](/help/edge/assets/aem-forms-visible-expression-formula-text.png)


* AND （）：指定したすべての条件が TRUE の場合にのみ TRUE を返します。

   * 例：すべての必須フィールドに値が入力されている場合にのみ「送信」ボタンを有効にする

   1. を `Visible` 「送信」ボタンのプロパティで、次の操作を行います。



      ```JavaScript
      =AND(NOT(address of `value` property of the `name` field = ""), NOT(address of `value` property of the `email` field = ""), NOT(address of `value` property of the `phone` field))
      ```

      例：

      ```JavaScript
      =AND(NOT(F9=""), NOT(F12=""), NOT(F10=""))
      ```

   1. 「メールを確認」フィールドの表示可能な式をに設定します

      ```JavaScript
      =FORMULATEXT ((address of visible property of the Confirm Email field))
      ```

      例：

      ```JavaScript
      =FORMULATEXT(G14)
      ```

      この式は、すべてのフィールド （名前、電子メール、電話）に値が入力されている場合にのみ「送信」ボタン （TRUE）を表示し（NOT （））が各フィールドの TRUE を返す場合）、そうでない場合はボタンを非表示にします（AND （multiple FALSES） = FALSE）。

* OR （）：指定された条件の少なくとも 1 つが TRUE の場合、TRUE を返します。

   * 例：ユーザーが適用可能な割引クーポンコードのいずれかを入力した場合の割引の適用。

   1. を `Visible` 「最終金額」フィールドのプロパティで次の操作を行います。


  ```JavaScript
     =IF(OR(F14="BlackFridaySale", F14="NewYearDiscount"), (F6*DAYS(F3,F2)* 0.7) , (F6*DAYS(F3,F2)))
  ```

   1. 「メールを確認」フィールドの値の式を「」に設定します。

      ```JavaScript
      =FORMULATEXT ((address of value property of the final amount field))
      ```

      例：

      ```JavaScript
      =FORMULATEXT(F7)
      ```

      この数式では、ユーザーがクーポンコード （couponCode = &quot;NewYearDiscount&quot;）または（couponCode = &quot;BlackFridaySale&quot;）を入力した場合に 30% の割引が計算され、入力しなかった場合は割引が 0 に設定されます。

**テキスト関数：**

* IF （）：条件を評価し、TRUE の場合は特定の値を返し、FALSE の場合は別の値を返します。

   * 例：選択した製品カテゴリに基づくカスタムメッセージの表示

   1. を `Value` のプロパティ `message` フィールド先 `Only upto 7 kg check-in lagguage is allowed!`:

   1. を `Visible` のプロパティ `message` フィールドを次に変更：


      ```JavaScript
      =if(address of value property of chosen product category ="Economy", TRUE(), FALSE())
      ```

      例：

      ```JavaScript
      =if(F5="Economy", TRUE(), FALSE())
      ```

   1. の値式を設定します `message` フィールド先

      ```JavaScript
      =FORMULATEXT ((address of value property of the final amount field))
      ```

      例：

      ```JavaScript
      =FORMULATEXT(G15)
      ```

      この式には、「7 kg までのチェックイン荷物のみが許可されています。」というメッセージが表示されます。 選択したクラスが「エコノミー」の場合は、メッセージフィールドは空白のままになります。

**数学関数：**

* SUM （）：指定したセル範囲の値を加算します。

  例：買い物かご内の品目の合計コストの計算。

  「合計金額」フィールドの値の式に SUM （price * quantity）

  この数式では、各品目の「価格」と「数量」に別々のフィールドがあることを前提としています。 この数式に複数の値を乗算し、SUM （）を使用して、買い物かごに入っているすべての商品の合計コストを合計します。

* ROUND （）：数値を指定された小数点以下の桁数に丸めます。

  例：計算済の割引金額を小数第 2 位に丸める。

  「割引額」フィールドの値式（割引が他の場所で計算されると仮定）: ROUND （discount, 2）

  この式では、割引値の端数が小数第 2 位に丸められます。

* MIN （）：指定したセル範囲の最小値を戻します。

  例：選択した国に基づくサインアップフォームの最低必要年齢の検索。

  「最小年齢」フィールドの値式で、MIN （ageLimits[「US」]、ageLimits[&quot;UK&quot;]、ageLimits[「フランス」]）

  この数式では、各国の最低年齢要件を格納した「ageLimits」というテーブルがあることを前提としています。 MIN （）を使用して、これらの中から最小値を検索します。


さらに、アダプティブFormsブロックにより、以下を作成することで、フォームを完全に管理することができます [カスタム関数](#creating-custom-functions). カスタム関数を使用すると、独自のルールとロジックを定義して、フォームの動作を完全に制御できます。


## カスタム関数の作成およびデプロイ

標準（OOTB）のアダプティブ Forms ブロックは、多くの [一般的なスプレッドシート関数](#spreadsheet-functions-for-rules). ただし、フォームをよりきめ細かく制御するには、Microsoft® Excel またはGoogle Sheets で使用できる任意の OOTB 関数を、アダプティブForms ブロック内で使用できます。 アダプティブFormsブロックには、Microsoft® Excel またはGoogle Sheets で使用できるすべての OOTB 関数の実装が含まれていません。 このような関数が必要な場合は、同様の構文でカスタム関数を開発して、Microsoft® Excel またはGoogle Sheets の機能を実現できます。 例えば、 [Microsoft® Excel の Year （）関数](https://support.microsoft.com/en-us/office/calculate-age-113d599f-5fea-448f-a4c3-268927911b37#) 生年月日から年齢を計算します。


### カスタム関数の作成

カスタム関数は、 `[Adaptive form block]/functions.js` ファイル。 作成プロセスには、通常、次の手順が含まれます。

* 関数宣言：関数名とそのパラメーター（受け入れる入力）を定義します。
* ロジック実装：関数で実行される特定の計算や操作の概要を説明するコードを記述します。
* 関数の書き出し：関連するファイルから関数を書き出して、ルール内で関数にアクセスできるようにします。

### 例：Year 関数

この例では、Excel の YEAR （）関数であるMicrosoftを模倣して年齢を計算する 2 つのカスタム関数の例を示し® す。


```JavaScript
/**
 * Get the current date and time
 * @name now
 * @returns {Date} The current date and time as a Date object
 */
function now() {
  const today = new Date();
  return today;
}

/**
 * Get the year from a Date object
 * @name year
 * @param {Date} date The date object
 * @throws {TypeError} If the input is not a Date object
 * @returns {number} The year as a number
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

フォームでカスタム関数を使用するには：

1. **関数の追加**：カスタム関数を `[Adaptive form block]/functions.js` ファイル。 ファイル内の export 文に必ず追加してください。
1. **ファイルのデプロイ**：更新されたをデプロイします `functions.js` github プロジェクトにファイルを提出し、ビルドが成功したことを確認します。
1. **関数の使用**：を使用して、フォームのスプレッドシート内の関数にアクセスします `Value`, `Value Expression`, `Visible`、または `Visible Expression` プロパティ。他のスプレッドシート関数と同様にサポートされている OOTB です。
1. **フォームをプレビューします**:AEM Sidekickを使用して、新しく実装された関数でフォームをプレビューします。

