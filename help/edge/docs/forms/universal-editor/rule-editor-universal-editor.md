---
title: ルールエディターを使用してフォームフィールドにルールを適用し、WYSIWYG オーサリングで作成されたフォームの動的な動作と複雑なロジックを有効にする方法
description: ユニバーサルエディターのルールエディターを使用すると、コーディングやスクリプトの作成を行わずに、動的な動作を追加し、複雑なロジックをフォームに組み込むことができます。
feature: Edge Delivery Services
role: Admin, Architect, Developer
hide: true
hidefromtoc: true
source-git-commit: c27b8e413c060de601a72a669d86c4add2a4167d
workflow-type: tm+mt
source-wordcount: '2111'
ht-degree: 11%

---


# ユニバーサルエディターのルールエディターの概要

ルールエディターを使用して動的なフォームの動作を追加し、ルールを作成できます。 これらのルールにより、条件付きフィールドの表示、ユーザー入力に基づく計算の自動化、全体的なユーザーエクスペリエンスの向上が可能になります。 フォーム入力プロセスを合理化することで、ルールエディターは正確性と効率の両方を保証するのに役立ちます。

ルールエディターには、ルールを作成および管理するための直感的で視覚的なインターフェイスが用意されています。 そのユーザーフレンドリーなアプローチにより、広範な技術的専門知識を持たないユーザーも含むすべてのユーザーがアクセスでき、フォーム内にロジックを簡単に実装できます。

## ルールを理解する

ルールは、特定の条件下でどのようなアクションを実行するかをユーザーに指示する手順です。

* **条件**：条件とは、対象が true または false かどうかを評価するチェックまたはルールです。 「これは要件を満たしているか」という質問に対する回答です。

* **アクション**：アクションとは、条件が true の場合に発生することです。 これは、条件の評価に基づいてトリガーされるタスクまたは動作です。

一般的なルールは、次のいずれかの構文に従います。

* **条件 – アクション**：最初に条件を確認してから、アクションを実行します。 ルールエディターで `When` ルールタイプを使用すると、`condition-action` 構文が適用されます。
* **アクション – 条件**：最初にアクションを実行してから、条件を確認します。 ルールエディター内の `Set Value Of` と `Validate` のルールタイプは、`action-condition` 構文を適用します。
* **アクション – 条件 – 代替アクション**：アクションを実行し、条件をチェックして、メイン処理を実行するか、条件に基づいて代替アクションを実行します。 例えば、デフォルトでは、`Show` の代替アクションは `Hide` で、`Enable` の代替アクションは `Disable` です。

例えば、条件では、ユーザーがフィールドに特定の値を入力したかどうかを確認し、アクションではフィールドの表示と非表示を切り替えることができます。
* **条件**：収入が 50,000 ドルを超えているかどうかを確認します。
* **アクション**：条件が true の場合は、`Additional Deduction` フィールドを表示します。それ以外の場合は、代替アクションを実行します（`Additional Deduction` フィールドを非表示にする）。

詳細な手順については、[ 条件付きルールの追加 ](#2-add-a-conditional-rule) を参照してください。

## ルールエディター拡張機能を有効にする方法

ユニバーサルエディターでは、ルールエディターはデフォルトでは有効になっていません。 環境でルールエディター拡張機能を有効にするには、公式アドレスから [aem-forms-ea@adobe.com](mailto:aem-forms-ea@adobe.com) にリクエストをメールで送信します。

環境でルールエディター拡張機能を有効にすると、エディターの右上隅に「![edit-rules](/help/forms/assets/edit-rules-icon.svg)」アイコンが表示されます。

![ ユニバーサルエディターのルールエディター ](/help/edge/docs/forms/assets/universal-editor-rule-editor.png)

ルールを記述するフォームオブジェクトを選択し、![edit-rules](/help/forms/assets/edit-rules-icon.svg) アイコンをクリックします。 ルールエディターのユーザーインターフェイスが表示されます。

![ ルールエディターのユーザーインターフェイス ](/help/edge/docs/forms/assets/rule-editor-for-field.png)

これで、[ ルールエディターで使用可能なルールタイプ ](#available-rule-types-in-rule-editor) を使用して、選択したフォームフィールドのルールまたはビジネスロジックの記述を開始できます。

## ルールエディターのユーザーインターフェイスについて

![edit-rules](/help/forms/assets/edit-rules-icon.svg) アイコンをクリックすると、ルールエディターのビジュアルエディターが開きます。

![ ルールエディターのユーザーインターフェイス ](/help/edge/docs/forms/assets/rule-editor-interface.png)

<table border="1">
  <thead>
    <tr>
      <th>ルールエディターのコンポーネント</th>
      <th>説明</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>1. コンポーネントルールの表示</td>
      <td>ルールエディターを起動したフォームオブジェクトのタイトルと、現在選択されているルールタイプを表示します。</td>
    </tr>
    <tr>
      <td>2. フォームオブジェクトと関数</td>
      <td>「<b>Forms オブジェクト </b>」タブには、フォームに含まれているすべてのオブジェクトの階層ビューが表示されます。 <b> 関数 </b> タブには、一連の組み込み関数が含まれています。</td>
    </tr>
    <tr>
      <td>3. フォームオブジェクトと関数の切り替え</td>
      <td>切り替えボタンをタップすると、フォームオブジェクトと関数ペインが切り替わります。</td>
    </tr>
    <tr>
      <td>4. ビジュアルルールエディター</td>
      <td>ルールを記述するビジュアルエディターユーザーインターフェイスのビジュアルエディターモード内の領域が、ビジュアルルールエディターです。</td>
    </tr>
    <tr>
      <td>5. 「完了」ボタンと「キャンセル」ボタン</td>
      <td>ルールを保存するには、「<b>完了</b>」ボタンを押します。<b> キャンセル </b> ボタンをクリックすると、ルールに対する変更が破棄され、ルールエディターが閉じます。</td>
    </tr>
  </tbody>
</table>

オブジェクトを選択すると、フォームオブジェクトの既存のルールが一覧表示されます。 ビジュアルルールエディターでタイトルを表示し、ルール概要をプレビューできます。 さらに、ルールの順序の変更、ルールの編集、ルールの有効化/無効化、ルールの削除を行うことができます。

![ フォームオブジェクトの使用可能なルールを表示する ](/help/edge/docs/forms/assets/rule-editor15.png)

## 利用可能なルールタイプ

ルールエディターには、次の表に示すように、ルールの記述に使用できる定義済みのルールタイプのセットが用意されています。

<table border="1">
  <thead>
    <tr>
      <th>ルールタイプ</th>
      <th>説明</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>次の値を設定</td>
      <td>指定した条件に応じて、フォームオブジェクトの値を設定します。</td>
    </tr>
    <tr>
      <td>値をクリア</td>
      <td>指定したオブジェクトの値をクリアします。</td>
    </tr>
    <tr>
      <td>非表示/表示</td>
      <td>条件を満たしているかどうかに基づいて、フォームオブジェクトの表示/非表示を切り替えます。</td>
    </tr>
    <tr>
      <td>有効 / 無効</td>
      <td>条件を満たしているかどうかに基づいて、フォームオブジェクトを有効または無効にします。</td>
    </tr>
    <tr>
      <td>Validate（検証）</td>
      <td>フォームまたは指定したオブジェクトを検証します。</td>
    </tr>
    <tr>
      <td>セッションに他のセッション属性 </td>
      <td>「<i> 条件 – アクション – 代替 </i> アクションルール構文または <i> 条件 – アクション </i> ルール構文に従います。 条件を指定し、その条件が満たされた場合に、トリガーを実行するアクションを実行します。</td>
    </tr>
    <tr>
      <td>形式</td>
      <td>関数または正規表現に基づいてフォームオブジェクトを書式設定します。</td>
    </tr>
    <tr>
      <td>サービスを起動</td>
      <td>フォームデータモデル（FDM）で設定されたサービスを呼び出します。</td>
    </tr>
    <tr>
      <td>プロパティを設定</td>
      <td>条件に基づいて、指定されたオブジェクトのプロパティの値を設定します。</td>
    </tr>
    <tr>
      <td>フォーカスを設定</td>
      <td>指定したオブジェクトにフォーカスを設定します。</td>
    </tr>
    <tr>
      <td>フォームを保存</td>
      <td>フォームを保存します。</td>
    </tr>
    <tr>
      <td>送信/リセットフォーム</td>
      <td>フォームを送信またはリセットします。</td>
    </tr>
    <tr>
      <td>インスタンスの追加/削除</td>
      <td>指定した繰り返し可能なパネルまたは表の行のインスタンスを追加または削除します。</td>
    </tr>
    <tr>
      <td>に移動します。</td>
      <td>他のアダプティブForms、画像やドキュメントフラグメントなどの他のアセット、または外部 URL に移動します。</td>
    </tr>
    <tr>
      <td>イベントのディスパッチ</td>
      <td>事前に定義された条件またはイベントに基づいて、特定のアクションをトリガー設定します。</td>
    </tr>
    <tr>
      <td>パネル間の移動</td>
      <td>フォーム内の様々なパネル間でフォーカスをシフトできます。</td>
    </tr>
  </tbody>
</table>


次に、[ ルールエディターでルールを記述 ](#write-rules) する方法を見てみましょう。

## ルールの記述

ビジュアルルールエディターでルールを記述する方法を理解するために、税金計算フォームの簡単な例を見てみましょう。

![ ルールエディターの例 ](/help/edge/docs/forms/assets/rule-editor-1.png)

上記のフォームでは、ユーザーは総給与を入力します。 この入力に基づいて、条件付きフィールドが表示され、買掛税金が計算されます。

**フォームフィールド：**
* 総給与（ユーザー入力）
* 追加控除（条件付きフィールド）
* 課税対象所得（計算フィールド）
* 未払税（計算フィールド）

**条件付きルール：**
* 条件：総給与 > 50,000
* アクション：追加控除フィールドの表示

**計算規則：**

* 課税所得=総給与 – 追加控除（該当する場合）
* 未払税=課税所得*税率（簡単にするため、固定率を 10% と仮定します）

ルールを記述するには、次のステップを実行します。

### 1. フォームの作成

ユニバーサルエディターでフォームを作成するには：

1. フォームをユニバーサルエディターで編集用に開きます。
1. 次のフォームコンポーネントを追加します。
   * 税金計算フォーム（タイトル）
   * 総給与（テキスト入力）
   * 追加控除（テキスト入力）
   * 課税所得（テキスト入力）
   * 支払税（テキスト入力）
   * 送信（送信ボタン）
1. `Properties` を開いて、`Additional Deduction` フォームフィールドを非表示にします。

   ![ ルールエディターの例 ](/help/edge/docs/forms/assets/rule-editor2.png)

### 2. フォームフィールドの条件付きルールを追加する

フォームを作成したら、総給与が$50,000 を超えた場合にのみ `Additional Deduction` フィールドを表示する最初のルールを記述します。 条件付きルールを追加するには：

1. フォームをユニバーサルエディターで編集用に開きます。
1. コンテンツツリーで **[!UICONTROL Gross Salary]** コンポーネントを選択して、![edit-rules](/help/forms/assets/edit-rules-icon.svg) を選択します。
   ![ ルールエディターの例 1](/help/edge/docs/forms/assets/rule-editor3.png)
ルールのビジュアルエディターインターフェイスが表示されます。
1. 「**[!UICONTROL 作成]**」をクリックして、ルールエディターを起動します。
   ![ ルールエディターの例 2](/help/edge/docs/forms/assets/rule-editor4.png)
デフォルトでは、`Set Value Of` のルールタイプが選択されています。 選択したオブジェクトを変更または修正することはできませんが、規則ドロップダウンを使用して別の規則タイプを選択できます。\
   ![ ルールエディターの例 3](/help/edge/docs/forms/assets/rule-editor5.png)
1. ルールタイプ ドロップダウンリストを開き、「**[!UICONTROL When]**」ルールタイプを選択します。
   ![ ルールエディターの例 4](/help/edge/docs/forms/assets/rule-editor6.png)
1. **[!UICONTROL 状態を選択]** ドロップダウンを選択し、「**[!UICONTROL 次の値より大きい]**」を選択します。 **[!UICONTROL 数値を入力]** フィールドが表示されます。
   ![ ルールエディターの例 5](/help/edge/docs/forms/assets/rule-editor7.png)
1. ルール内の **[!UICONTROL 数値を入力]** フィールドに `50000` を入力します。
   ![ ルールエディターの例 6](/help/edge/docs/forms/assets/rule-editor8.png)
条件を `When Gross Salary is greater than 50000` と定義しました。 次に、この条件が `True` の場合に実行するアクションを定義します。
1. `Then` ステートメントで、「**[!UICONTROL アクションを選択]** ドロップダウンから **[!UICONTROL 表示]** を選択します。
   ![ ルールエディターの例 7](/help/edge/docs/forms/assets/rule-editor9.png)
1. 「**[!UICONTROL オブジェクトをドロップまたは次から選択]** フィールドの「フォームオブジェクト」タブから **[!UICONTROL 追加控除]** フィールドをドラッグ&amp;ドロップします。 または、「**[!UICONTROL オブジェクトをドロップするか、または次から選択]**」フィールドを選択し、ポップアップメニューから「**[!UICONTROL 追加控除]**」フィールドを選択します。この中には、フォーム内のすべてのフォームオブジェクトが一覧表示されます。
   ![ ルールエディターの例 8](/help/edge/docs/forms/assets/rule-editor10.png)
1. 「**[!UICONTROL Else セクションの追加]**」をクリックし、`50000` 未満の給与を入力した場合に備えて、「Gross Salary **[!UICONTROL フィールドに別の条件を追加し]** す。
   ![ ルールエディターの例 9](/help/edge/docs/forms/assets/rule-editor11.png)
1. `Else` ステートメントの **[!UICONTROL アクションを選択]** ドロップダウンから **[!UICONTROL 非表示]** を選択します。
   ![ ルールエディターの例 10](/help/edge/docs/forms/assets/rule-editor12.png)
1. 「**[!UICONTROL オブジェクトをドロップまたは次から選択]** フィールドの「フォームオブジェクト」タブから **[!UICONTROL 追加控除]** フィールドをドラッグ&amp;ドロップします。 または、「**[!UICONTROL オブジェクトをドロップするか、または次から選択]**」フィールドを選択し、ポップアップメニューから「**[!UICONTROL 追加控除]**」フィールドを選択します。この中には、フォーム内のすべてのフォームオブジェクトが一覧表示されます。
   ![ ルールエディターの例 11](/help/edge/docs/forms/assets/rule-editor13.png)
1. 「**[!UICONTROL 完了]**」を選択して、ルールを保存します。
ルールエディターでは、ルールが次のように表示されます。
   ![ ルールエディターの例 12](/help/edge/docs/forms/assets/rule-editor14.png)

>[!NOTE]
>
> また、同じ動作を実装する場合は、「総給与」フィールドに「When」ルールを記述する代わりに、「追加控除」フィールドに「表示」ルールを記述することもできます。

### 3. フォームフィールドの計算ルールを追加する

次に、`Taxable Income` を計算するルールを記述します。これは、`Gross Salary` と `Additional Deduction` の違いです（該当する場合）。 「**[!UICONTROL 課税対象所得]** フィールドに計算ルールを追加するには、次の手順を実行します。

1. オーサリングモードで「**[!UICONTROL 課税対象所得]**」フィールドを選択し、「![edit-rules](/help/forms/assets/edit-rules-icon.svg)」アイコンを選択します。 次に、「**[!UICONTROL 作成]** を選択して、ルールエディターを起動します。
   ![ ルールエディターの例 13](/help/edge/docs/forms/assets/rule-editor16.png)
1. 「**[!UICONTROL オプションの選択]**」を選択し、「**[!UICONTROL 数式]**」を選択します。数式記述用のフィールドが表示されます。
   ![ ルールエディターの例 14](/help/edge/docs/forms/assets/rule-editor17.png)

1. 「数式」フィールドで、次の操作を行います。

   * 「Formsオブジェクト」タブから、最初の **[!UICONTROL オブジェクトをドロップまたは次から選択]** フィールドの **[!UICONTROL Gross Salary]** フィールドを選択またはドラッグ&amp;ドロップします。

   * **[!UICONTROL 演算子を選択]** フィールドから **[!UICONTROL マイナス]** を選択します。

   * 「Formsオブジェクト」タブから、他の **[!UICONTROL ドロップオブジェクトまたは次から選択]** フィールドの「**[!UICONTROL 追加の控除]**」フィールドを選択またはドラッグ&amp;ドロップします。
     ![ ルールエディターの例 15](/help/edge/docs/forms/assets/rule-editor18.png)

1. 「**[!UICONTROL 完了]**」を選択し、ルールを保存します。

   次に、課税対象所得に税率を乗算して決定される「`Tax Payable `」フィールドのルールを追加します。 簡単にするために、`10%` の固定税率を想定します。

1. オーサリングモードで、「**[!UICONTROL 納税者]**」フィールドを選択し、「![edit-rules](/help/forms/assets/edit-rules-icon.svg)」アイコンを選択します。 次に、「**[!UICONTROL 作成]** を選択して、ルールエディターを起動します。
   ![ ルールエディターの例 16](/help/edge/docs/forms/assets/rule-editor19.png)
1. 「**[!UICONTROL オプションの選択]**」を選択し、「**[!UICONTROL 数式]**」を選択します。数式記述用のフィールドが表示されます。
   ![ ルールエディターの例 17](/help/edge/docs/forms/assets/rule-editor20.png)
1. 「数式」フィールドで、次の操作を行います。

   * 「Forms オブジェクト」タブから、最初の **[!UICONTROL オブジェクトをドロップまたは次から選択]** フィールドの **[!UICONTROL 課税対象所得]** フィールドを選択またはドラッグ&amp;ドロップします。

   * **[!UICONTROL 演算子を選択]** フィールドから **[!UICONTROL 乗算]** を選択します。

   * **[!UICONTROL オプションを選択** フィールドから **数値]** を選択し、**[!UICONTROL 数値を入力]** フィールドに `10` のように値を入力します。
     ![ ルールエディターの例 18](/help/edge/docs/forms/assets/rule-editor21.png)
1. 次に、式フィールドの周りのハイライト表示された領域を選択し、「**[!UICONTROL 拡張式]**」を選択します。
   ![ ルールエディターの例 19](/help/edge/docs/forms/assets/rule-editor22.png)
1. 拡張式フィールドでは、「**[!UICONTROL 演算子を選択]**」フィールドから「**[!UICONTROL ÷]**」を選択し、「**[!UICONTROL オプションを選択]**」フィールドから「**[!UICONTROL 数字]**」を選択します。次に、数値フィールドに `100` を指定します。
   ![ ルールエディターの例 20](/help/edge/docs/forms/assets/rule-editor23.png)
1. 「**[!UICONTROL 完了]**」を選択し、ルールを保存します。

### 4. フォームをプレビューする

これで、フォームをプレビューして「**総給与**」と入力すると、`60,000` に **追加控除** フィールドが表示され、**課税対象所得** と **課税支払** がそれに応じて計算されます。

![ フォームをプレビューする ](/help/edge/docs/forms/assets/rule-editor-form.png)

「関数出力」の下にリストされている「合計」、「平均」などの既存の関数に加え [ カスタム関数の記述 ](#create-a-custom-function) により、複雑なビジネスロジックを実装することもできます。

## ルールエディターでのカスタム関数

Edge Delivery ServicesFormsでは、複雑なビジネスルールを実装するためのJavaScript関数を定義できるカスタム関数をサポートしています。 カスタム関数は、入力したデータの操作や処理を容易にし、指定された要件を満たすことで、フォームの機能を拡張します。

### カスタム関数の作成

カスタム関数を作成するには、`../[blocks]/form/functions.js` ファイルを編集します。 作成プロセスには通常、次の手順が含まれます。

* **関数宣言**：関数名とそのパラメーター（受け入れる入力）を定義します。
* **ロジック実装**：関数で実行される特定の計算や操作の概要を説明するコードを記述します。
* **関数の書き出し**：関連するファイルから書き出して、ルール内で関数にアクセスできるようにします。


この例では、と `days` の 2 つのカスタム関数 `getFullName` 示しています。

```JavaScript
/**
 * Get Full Name
 * @name getFullName Concats first name and last name
 * @param {string} firstname in Stringformat
 * @param {string} lastname in Stringformat
 * @return {string}
 */
function getFullName(firstname, lastname) {
  return `${firstname} ${lastname}`.trim();
}

/**
 * Calculate the number of days between two dates.
 * @param {*} endDate
 * @param {*} startDate
 * @name days Calculates the numebr of days between two dates
 * @returns {number} returns the number of days between two dates
 */
function days(endDate, startDate) {
  const start = typeof startDate === 'string' ? new Date(startDate) : startDate;
  const end = typeof endDate === 'string' ? new Date(endDate) : endDate;

  // return zero if dates are valid
  if (Number.isNaN(start.getTime()) || Number.isNaN(end.getTime())) {
    return 0;
  }

  const diffInMs = Math.abs(end.getTime() - start.getTime());
  return Math.floor(diffInMs / (1000 * 60 * 60 * 24));
}

// eslint-disable-next-line import/prefer-default-export
export { getFullName, days };
```
![ カスタム関数の追加 ](/help/edge/docs/forms/assets/create-custom-function.png)

### ルールエディターでのカスタム関数の使用

ルールエディターでカスタム関数を使用するには：

1. **関数の追加**：カスタム関数を `../[blocks]/form/functions.js` ファイルに含めます。 ファイル内の `export` ステートメントに必ず追加してください。
1. **ファイルをデプロイ**：更新された `functions.js` ファイルを GitHub プロジェクトにデプロイし、ビルドが成功したことを確認します。
1. **関数の使用法**:「**[!UICONTROL アクションの選択]**」フィールドの「`Function Output`」オプションを選択して、フォームのルールエディター内の関数にアクセスします。

   ![ ルールエディター内のカスタム関数 ](/help/edge/docs/forms/assets/custom-function-rule-editor.png)

1. **フォームのプレビュー**：新しく実装された関数を使用してフォームをプレビューします。

## 関連記事

{{see-also-rule-editor}}

## 関連トピック

* [AEM Forms の Edge Delivery Services の基本を学ぶ](/help/edge/docs/forms/tutorial.md)
* [Google Sheet または Microsoft Excel を使用したフォームの作成](/help/edge/docs/forms/create-forms.md)
* [データの受け入れを開始するための Google Sheets または Microsoft Excel ファイルの設定](/help/edge/docs/forms/submit-forms.md)
* [フォームを公開してデータの収集を開始](/help/edge/docs/forms/publish-forms.md)
* [フォームの外観のカスタマイズ](/help/edge/docs/forms/style-theme-forms.md)
* [繰り返し可能なセクションをフォームに追加する](/help/edge/docs/forms/repeatable-forms.md)
* [フォーム送信後にカスタムのお礼のメッセージを表示](/help/edge/docs/forms/thank-you-page-form.md)
* [アダプティブフォームブロックのコンポーネントとそのプロパティ](/help/edge/docs/forms/form-components.md)
* [実際の使用のモニタリング](https://www.aem.live/developer/rum#authentication)
