---
title: ルールエディターを使用してルールをフォームフィールドに適用し、WYSIWYG オーサリングで作成されたフォームの動的な動作と複雑なロジックを有効にする方法
description: ユニバーサルエディターのルールエディターを使用すると、コーディングやスクリプトを使用せずに、動的な動作を追加し、複雑なロジックをフォームに組み込むことができます。
feature: Edge Delivery Services
role: Admin, Architect, Developer
exl-id: 846f56e1-3a98-4a69-b4f7-40ec99ceb348
source-git-commit: 9127c58a72dc4942312907f9e8f0cdcc8de9aa4b
workflow-type: tm+mt
source-wordcount: '2214'
ht-degree: 99%

---


# WYSIWYG オーサリングのルールエディターの概要

<span class="preview">この機能は、早期アクセスプログラムを通じて使用できます。アクセスをリクエストするには、GitHub 組織名とリポジトリ名を記載したメールを公式アドレスから <a href="mailto:aem-forms-ea@adobe.com">aem-forms-ea@adobe.com</a> に送信してください。 例えば、リポジトリ URL が https://github.com/adobe/abc の場合、組織名は adobe で、リポジトリ名は abc になります。</span>


ルールを作成できるルールエディターを使用して、動的なフォームの動作を追加できます。これらのルールにより、条件付きフィールドの表示が有効になり、ユーザー入力に基づいて計算が自動化され、全体的なユーザーエクスペリエンスが向上します。ルールエディターは、フォーム入力プロセスを効率化することで、正確性と効率性の両方を確保するのに役立ちます。

ルールエディターには、ルールを作成および管理する直感的で視覚的なインターフェイスが用意されています。わかりやすいアプローチにより、広範な技術的専門知識を持たないユーザーも含め、すべてのユーザーがアクセスでき、フォーム内にロジックを簡単に実装できます。

## ルールについて

ルールは、特定の条件下でユーザーが実行するアクションをガイドする手順です。

* **条件**：条件とは、対象が true または false かどうかを評価する確認またはルールです。「これは要件を満たしていますか？」という質問にに回答します。

* **アクション**：アクションとは、条件が true の場合に実行される動作を示します。条件の評価に基づいてトリガーされるタスクまたは動作です。

一般的なルールは、次のいずれかの構文に従います。

* **条件=アクション**：最初に条件を確認してから、アクションを実行します。ルールエディターで `When` ルールタイプを使用することで、`condition-action` の構文が適用されます。
* **アクション=条件**：最初にアクションを実行してから、条件を確認します。ルールエディターの `Set Value Of` と `Validate` のルールタイプでは、`action-condition` 構文が適用されます。
* **アクション=条件=代替アクション**：アクションを実行し、条件を確認してから、条件に基づいてメインアクションまたは代替アクションを実行します。例えば、デフォルトでは、`Show` の代替アクションは `Hide`、`Enable` の代替アクションは `Disable` です。

例えば、条件では、ユーザーがフィールドに特定の値を入力したかどうかを確認し、アクションではフィールドを表示または非表示にすることができます。
* **条件**：収入が 50,000 ドルを超えているかどうかを確認します。
* **アクション**：条件が true の場合は、`Additional Deduction` フィールドを表示します。それ以外の場合は、代替アクションを実行して、`Additional Deduction` フィールドを非表示にします。

手順について詳しくは、[条件付きルールの追加](#2-add-a-conditional-rule)を参照してください。

## ルールエディター拡張機能を有効にする方法

ユニバーサルエディターでは、ルールエディター拡張機能はデフォルトで有効になっていません。ルールエディター拡張機能を有効にするには、公式メール ID から [aem-forms-ea@adobe.com](mailto:aem-forms-ea@adobe.com) までご連絡ください。

お使いの環境でルールエディター拡張機能が有効になると、エディターの右上隅に ![ルールを編集](/help/forms/assets/edit-rules-icon.svg) アイコンが表示されます。

![ユニバーサルエディターのルールエディター](/help/edge/docs/forms/assets/universal-editor-rule-editor.png)

ルールを記述するフォームコンポーネントを選択し、![ルールを編集](/help/forms/assets/edit-rules-icon.svg) アイコンをクリックします。ルールエディターのユーザーインターフェイスが表示されます。

![ルールエディターのユーザーインターフェイス](/help/edge/docs/forms/assets/rule-editor-for-field.png)

この記事では、`form object` と `form component` が同じ意味で使用されています。

これで、[ルールエディターで使用可能なルールタイプ](#available-rule-types-in-rule-editor)を使用して、選択したフォームフィールドのルールまたはビジネスロジックの記述を開始できます。

## ルールエディターのユーザーインターフェイスについて

![ルールを編集](/help/forms/assets/edit-rules-icon.svg) アイコンをクリックすると、ルールエディターのエディターが開きます。

![ルールエディターのユーザーインターフェイス](/help/edge/docs/forms/assets/rule-editor-interface.png)

<table border="1">
  <thead>
    <tr>
      <th>ルールエディターのコンポーネント</th>
      <th>説明</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>1. タイトル</td>
      <td>フォームコンポーネントのタイトルと、選択したルールタイプを表示します。例えば、「総給与を入力」は、「条件」ルールタイプが選択されたテキストボックスコンポーネントです。 </td>
    </tr>
    <tr>
      <td>2. フォームオブジェクトと関数</td>
      <td>「<b>フォームオブジェクト</b>」タブには、フォームに含まれているコンポーネントがすべて階層表示されます。「<b>関数</b>」タブには、ルールエディターの一連の組み込み関数が含まれます。</td>
    </tr>
    <tr>
      <td>3. フォームオブジェクトと関数の切り替え</td>
      <td>切替スイッチボタンを使用すると、フォームオブジェクトパネルと関数パネルが交互に表示または非表示になります。 </td>
    </tr>
    <tr>
      <td>4. ビジュアルルールエディター</td>
      <td>ビジュアルルールエディターは、フォームコンポーネントのルールを作成できるインターフェイスです。</td>
    </tr>
    <tr>
      <td>5. 「完了」ボタンと「キャンセル」ボタン</td>
      <td>ルールを保存するには、「<b>完了</b>」ボタンを押します。「<b>キャンセル</b>」ボタンは、ルールに加えた変更を破棄し、ルールエディターを閉じます。</td>
    </tr>
  </tbody>
</table>

コンポーネントを選択すると、フォームコンポーネント上に既存のルールが一覧表示されます。ルールエディターでタイトルを表示し、ルール概要をプレビューできます。さらに、ルールの順序変更、ルールの編集、ルールの有効化／無効化、ルールの削除を行うことができます。

![フォームオブジェクトの使用可能なルールを表示](/help/edge/docs/forms/assets/rule-editor15.png)

## 使用可能なルールタイプ

ルールエディターでは、以下の表に示すように、ルールを記述する事前定義された一連のルールタイプを利用できます。

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
      <td>指定した条件に応じてフォームコンポーネントの値を設定します。</td>
    </tr>
    <tr>
      <td>次の値をクリア</td>
      <td>指定したフォームコンポーネントの値がクリアします。</td>
    </tr>
    <tr>
      <td>非表示／表示</td>
      <td>条件を満たしているかどうかに基づいて、フォームコンポーネントを表示または非表示にします。</td>
    </tr>
    <tr>
      <td>有効／無効</td>
      <td>条件を満たしているかどうかに基づいて、フォームコンポーネントを有効または無効にします。</td>
    </tr>
    <tr>
      <td>検証</td>
      <td>条件に基づいてフォーム コンポーネントを確認し、条件が満たされない場合はエラーを表示します。 </td>
    </tr>
    <tr>
      <td>条件</td>
      <td>評価の条件を指定し、その後に条件が満たされた場合にトリガーするアクションを指定します。「<i>条件=アクション=代替</i>」アクションのルール構文または「<i>条件=アクション</i>」のルール構文に従います。 </td>
    </tr>
    <tr>
      <td>形式</td>
      <td> フォームコンポーネントの値を変更した際に、指定された式を使用してフォームコンポーネントの表示値を変更します。</td>
    </tr>
    <tr>
      <td>サービスを呼び出す</td>
      <td>外部 API、フォームデータモデルまたは RESTful web サービスを使用して設定されたサービスを呼び出します。</td>
    </tr>
    <tr>
      <td>プロパティを設定</td>
      <td>条件に基づいて、指定したフォームコンポーネントのプロパティの値を設定します。</td>
    </tr>
    <tr>
      <td>フォーカスを設定</td>
      <td>指定したフォームコンポーネントにフォーカスを設定します。</td>
    </tr>
    <tr>
      <td>フォームを保存</td>
      <td>これにより、ユーザーはドラフトと送信フォームポータルコンポーネントを使用してフォームをドラフトとして保存できます。 </td>
    </tr>
    <tr>
      <td>フォームを送信</td>
      <td>フォームを送信します。</td>
    </tr>
    <tr>
      <td>フォームをリセット</td>
      <td>フォームをリセットします。</td>
    </tr>
    <tr>
      <td>インスタンスを追加／削除</td>
      <td>指定した繰り返し可能なパネルまたはテーブル行のインスタンスを追加または削除します。</td>
    </tr>
    <tr>
      <td>次に移動</td>
      <td>他のアダプティブフォーム、画像やドキュメントフラグメントなどの他のアセット、または外部 URL に移動します。</td>
    </tr>
    <tr>
      <td>イベントのディスパッチ</td>
      <td>事前定義済みの条件またはイベントに基づいて、特定のアクションをトリガーします。</td>
    </tr>
    <tr>
      <td>パネル間を移動</td>
      <td>フォーム内の様々なパネル間でフォーカスをシフトできます。</td>
    </tr>
  </tbody>
</table>


次に、[ルールエディターでルールを記述](#write-rules)する方法を見てみましょう。

## ルールの記述

ビジュアルルールエディターでルールを記述する方法を理解するには、税金計算フォームの簡単な例を考えます。

![ルールエディターの例](/help/edge/docs/forms/assets/rule-editor-1.png)

上記のフォームでは、ユーザーは総給与を入力します。この入力に基づいて条件付きフィールドが表示され、支払税が計算されます。

**フォームフィールド：**
* 総給与（ユーザー入力）
* 追加控除（条件付きフィールド）
* 課税所得（計算済みフィールド）
* 支払税（計算済みフィールド）

**条件付きルール：**
* 条件：総給与が 50,000 ドルより上
* アクション：「追加控除」フィールドを表示

**計算ルール：**

* 課税所得 = 総給与 – 追加控除（該当する場合）
* 支払税 = 課税所得 × 税率（簡単にするため、固定税率を 10％と仮定）

ルールを記述するには、次の手順を実行します。

### 1. フォームを作成

ユニバーサルエディターでフォームを作成するには：

1. 編集用にユニバーサルエディターでフォームを開きます。
1. 次のフォームコンポーネントを追加します。
   * 税金計算フォーム（タイトル）
   * 総給与（数値入力）
   * 追加控除（数値入力）
   * 課税所得（数値入力）
   * 支払税（数値入力）
   * 送信（「送信」ボタン）
1. `Properties` を開いて、`Additional Deduction` フォームフィールドを非表示にします。

   ![ルールエディターの例](/help/edge/docs/forms/assets/rule-editor2.png)

### 2. フォームフィールドの条件付きルールを追加

フォームを作成したら、総給与が 50,000 ドルを超える場合にのみ「`Additional Deduction`」フィールドを表示する最初のルールを記述します。条件付きルールを追加するには：

1. 編集用にユニバーサルエディターでフォームを開き、コンテンツツリーで「**[!UICONTROL 総給与]**」フィールドを選択して、「![ルールを編集](/help/forms/assets/edit-rules-icon.svg)」を選択します。または、**[!UICONTROL フォームオブジェクト]**&#x200B;パネルから「**[!UICONTROL 総給与]**」フィールドを直接選択することもできます。
   ![ルールエディターの例 1](/help/edge/docs/forms/assets/rule-editor3.png)
ビジュアルルールエディターのインターフェイスが表示されます。
1. 「**[!UICONTROL 作成]**」をクリックして、ルールを作成します。
   ![ルールエディターの例 2](/help/edge/docs/forms/assets/rule-editor4.png)
デフォルトでは、`Set Value Of` ルールタイプが選択されます。選択したオブジェクトを変更または修正できませんが、ルールドロップダウンを使用して別のルールタイプを選択できます。\
   ![ルールエディターの例 3](/help/edge/docs/forms/assets/rule-editor5.png)
1. ルールタイプドロップダウンリストを開き、**[!UICONTROL When]** ルールタイプを選択します。
   ![ルールエディターの例 4](/help/edge/docs/forms/assets/rule-editor6.png)
1. **[!UICONTROL 状態の選択]**&#x200B;ドロップダウンを選択し、「**[!UICONTROL 次の値より大きい]**」を選択します。「**[!UICONTROL 数値を入力]**」フィールドが表示されます。
   ![ルールエディターの例 5](/help/edge/docs/forms/assets/rule-editor7.png)
1. ルールの「**[!UICONTROL 数値を入力]**」フィールドに `50000` を入力します。
   ![ルールエディターの例 6](/help/edge/docs/forms/assets/rule-editor8.png)
条件を `When Gross Salary is greater than 50000` と定義しました。次に、この条件が `True` の場合に実行するアクションを定義します。
1. `Then` ステートメントで、**[!UICONTROL アクションを選択]**&#x200B;ドロップダウンから「**[!UICONTROL 表示]**」を選択します。
   ![ルールエディターの例 7](/help/edge/docs/forms/assets/rule-editor9.png)
1. 「**[!UICONTROL オブジェクトをドロップするか、または次から選択]**」フィールドの「フォームオブジェクト」タブから「**[!UICONTROL 追加控除]**」フィールドをドラッグ＆ドロップします。あるいは、「**[!UICONTROL オブジェクトをドロップするか、または次から選択]**」フィールドを選択し、ポップアップメニューから「**[!UICONTROL 追加控除]**」フィールドを選択します。この中には、フォーム内のすべてのフォームオブジェクトが一覧表示されます。
   ![ルールエディターの例 8](/help/edge/docs/forms/assets/rule-editor10.png)
1. `50000` 未満の給与を入力した場合は、「**[!UICONTROL Else セクションを追加]**」をクリックして、「**[!UICONTROL 総給与]**」フィールドに別の条件を追加します。
   ![ルールエディターの例 9](/help/edge/docs/forms/assets/rule-editor11.png)
1. `Else` ステートメントの&#x200B;**[!UICONTROL アクションを選択]**&#x200B;ドロップダウンから「**[!UICONTROL 非表示]**」を選択します。
   ![ルールエディターの例 10](/help/edge/docs/forms/assets/rule-editor12.png)
1. 「**[!UICONTROL オブジェクトをドロップするか、または次から選択]**」フィールドの「フォームオブジェクト」タブから「**[!UICONTROL 追加控除]**」フィールドをドラッグ＆ドロップします。あるいは、「**[!UICONTROL オブジェクトをドロップするか、または次から選択]**」フィールドを選択し、ポップアップメニューから「**[!UICONTROL 追加控除]**」フィールドを選択します。この中には、フォーム内のすべてのフォームオブジェクトが一覧表示されます。
   ![ルールエディターの例 11](/help/edge/docs/forms/assets/rule-editor13.png)
1. 「**[!UICONTROL 完了]**」を選択し、ルールを保存します。
ルールエディターでは、ルールが次のように表示されます。
   ![ルールエディターの例 12](/help/edge/docs/forms/assets/rule-editor14.png)

>[!NOTE]
>
> または、「総給与」フィールドに When ルールを記述する代わりに、「追加控除」フィールド上に Show ルールを記述して、同じ動作を実装することもできます。

### 3. フォームフィールドの計算ルールを追加

次に、`Gross Salary` と `Additional Deduction` の差である `Taxable Income` を計算するルールを記述します（該当する場合）。「**[!UICONTROL 課税所得]**」フィールドに計算ルールを追加するには、次の手順を実行します。

1. オーサリングモードで「**[!UICONTROL 課税所得]**」フィールドを選択し、![ルールを編集](/help/forms/assets/edit-rules-icon.svg) アイコンを選択します。または、**[!UICONTROL フォームオブジェクト]**&#x200B;パネルから「**[!UICONTROL 課税所得]**」フィールドを直接選択することもできます。
1. 次に、「**[!UICONTROL 作成]**」を選択して、ルールを作成します。
   ![ルールエディターの例 13](/help/edge/docs/forms/assets/rule-editor16.png)
1. 「**[!UICONTROL オプションの選択]**」を選択し、「**[!UICONTROL 数式]**」を選択します。数式記述用のフィールドが開きます。
   ![ルールエディターの例 14](/help/edge/docs/forms/assets/rule-editor17.png)

1. 数式フィールドで、次の操作を行います。

   * 最初の「**[!UICONTROL オブジェクトをドロップまたは次から選択]**」フィールドの「**[!UICONTROL 総給与]**」フィールドで、「フォームオブジェクト」タブから選択またはドラッグ＆ドロップします。

   * 「**[!UICONTROL 演算子を選択]**」フィールドから「**[!UICONTROL 減算]**」を選択します。

   * 他の「**[!UICONTROL オブジェクトをドロップまたは次から選択]**」フィールドの「**[!UICONTROL 追加控除]**」フィールドで、「フォームオブジェクト」タブから選択またはドラッグ＆ドロップします。

     ![ルールエディターの例 15](/help/edge/docs/forms/assets/rule-editor18.png)

1. 「**[!UICONTROL 完了]**」を選択し、ルールを保存します。

   次に、課税所得に税率を乗算して決定される「`Tax Payable `」フィールドにルールを追加します。簡素化して固定税率を `10%` と仮定します。

1. オーサリングモードで「**[!UICONTROL 支払税]**」フィールドを選択し、![ルールを編集](/help/forms/assets/edit-rules-icon.svg) アイコンを選択します。次に、「**[!UICONTROL 作成]**」を選択して、ルールを作成します。
   ![ルールエディターの例 16](/help/edge/docs/forms/assets/rule-editor19.png)
1. 「**[!UICONTROL オプションの選択]**」を選択し、「**[!UICONTROL 数式]**」を選択します。数式記述用のフィールドが開きます。
   ![ルールエディターの例 17](/help/edge/docs/forms/assets/rule-editor20.png)
1. 数式フィールドで、次の操作を行います。

   * 最初の「**[!UICONTROL オブジェクトをドロップまたは次から選択]**」フィールドの「**[!UICONTROL 課税所得]**」フィールドで、「フォームオブジェクト」タブから選択またはドラッグ＆ドロップします。

   * 「**[!UICONTROL 演算子を選択]**」フィールドから「**[!UICONTROL 乗算]**」を選択します。

   * 「**[!UICONTROL オプションを選択**」フィールドから「**数値]**」を選択し、「**[!UICONTROL 数値を入力]**」フィールドに `10` のように値を入力します。

     ![ルールエディターの例 18](/help/edge/docs/forms/assets/rule-editor21.png)
1. 次に、式フィールドの周りのハイライト表示された領域を選択し、「**[!UICONTROL 拡張式]**」を選択します。
   ![ルールエディターの例 19](/help/edge/docs/forms/assets/rule-editor22.png)
1. 拡張式フィールドでは、「**[!UICONTROL 演算子を選択]**」フィールドから「**[!UICONTROL 割り算]**」を選択し、「**[!UICONTROL オプションを選択]**」フィールドから「**[!UICONTROL 数字]**」を選択します。次に、数値フィールドに `100` を指定します。
   ![ルールエディターの例 20](/help/edge/docs/forms/assets/rule-editor23.png)
1. 「**[!UICONTROL 完了]**」を選択し、ルールを保存します。

### 4. フォームをプレビュー

これで、フォームをプレビューし、**総給与**&#x200B;を `60,000` として入力すると、「**追加控除**」フィールドが表示され、それに応じて「**課税所得**」と「**支払税**」が計算されます。

![フォームをプレビュー](/help/edge/docs/forms/assets/rule-editor-form.png)

「関数出力」の下にリストされている「合計」、「平均」などの標準の関数に加え、[カスタム関数を記述](#create-a-custom-function)して複雑なビジネスロジックを実装することもできます。

## ルールエディターでのカスタム関数

Edge Delivery Services のフォームでは、ユーザーが複雑なビジネスルールを実装する JavaScript 関数を定義できるカスタム関数をサポートしています。カスタム関数は、指定された要件を満たすエントリ済みデータの操作と処理を容易にすることで、フォームの機能を拡張します。

### カスタム関数の作成

カスタム関数を作成するには、`../[blocks]/form/functions.js` ファイルを編集します。作成プロセスには通常、次の手順が含まれます。

* **関数宣言**：関数名とそのパラメーター（受け入れる入力）を定義します。
* **ロジック実装**：関数で実行される特定の計算や操作の概要を説明するコードを書き込みます。
* **関数の書き出し**：関連ファイルから関数を書き出して、ルール内で関数にアクセスできます。


次の例では、`getFullName` と `days` という 2 つのカスタム関数を示します。

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

![カスタム関数の追加](/help/edge/docs/forms/assets/create-custom-function.png)

### ルールエディターでのカスタム関数の使用

ルールエディターでカスタム関数を使用するには：

1. **関数を追加**：カスタム関数を `../[blocks]/form/functions.js` ファイルに含めます。必ず、ファイル内の `export` ステートメントに追加します。
1. **ファイルをデプロイ**：更新された `functions.js` ファイルを GitHub プロジェクトにデプロイし、ビルドが成功したことを確認します。
1. **関数の使用**：「**[!UICONTROL アクションを選択]**」フィールドの「`Function Output`」オプションを選択して、フォームのルールエディター内の関数にアクセスします。

   ![ルールエディターでのカスタム関数](/help/edge/docs/forms/assets/custom-function-rule-editor.png)

1. **フォームをプレビュー**：新しく実装された関数でフォームをプレビューします。

## 追加情報

>[!NOTE]
>
> ユニバーサルエディターでは、カスタム関数スクリプトで静的および動的の読み込みはサポートされません。完全なコードを `../[blocks]/form/functions.js` ファイルに追加する必要があります。

この記事では、ユニバーサルエディターで使用できるルールエディターに関する限定的な情報を提供します。ルールエディターとカスタム関数について詳しくは、次の記事を参照してください。

{{see-also-rule-editor}}

## 関連トピック

{{universal-editor-see-also}}
