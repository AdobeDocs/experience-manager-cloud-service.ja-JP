---
title: アダプティブフォームのコンポーネントにインラインスタイルを適用する方法
description: アダプティブフォームにカスタムスタイルを適用する方法を学び、アダプティブフォームの個々のコンポーネントにインライン CSS プロパティを適用する方法も説明します。
feature: Adaptive Forms
role: User
level: Intermediate
exl-id: 25adabfb-ff19-4cb2-aef5-0a8086d2e552
source-git-commit: 2d4ffd5518d671a55e45a1ab6f1fc41ac021fd80
workflow-type: tm+mt
source-wordcount: '761'
ht-degree: 56%

---

# アダプティブフォームコンポーネントのインラインスタイル設定 {#inline-styling-of-adaptive-form-components}

<span class="preview"> Adobeでは、最新の拡張可能なデータキャプチャを使用することをお勧めします [コアコンポーネント](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html?lang=ja) 対象： [新しいアダプティブFormsの作成](/help/forms/creating-adaptive-form-core-components.md) または [AEM SitesページへのアダプティブFormsの追加](/help/forms/create-or-add-an-adaptive-form-to-aem-sites-page.md). これらのコンポーネントは、アダプティブフォームの作成における大幅な進歩を示すものであり、優れたユーザーエクスペリエンスを実現します。この記事では、基盤コンポーネントを使用してアダプティブフォームを作成するより従来的な方法について説明します。</span>

| バージョン | 記事リンク |
| -------- | ---------------------------- |
| AEM 6.5 | [ここをクリックしてください](https://experienceleague.adobe.com/docs/experience-manager-65/forms/adaptive-forms-basic-authoring/inline-style-adaptive-forms.html) |
| AEM as a Cloud Service | この記事 |

アダプティブフォームの全体的な外観とスタイルは、[テーマエディター](themes.md)でスタイルを指定して定義できます。また、アダプティブフォームの個々のコンポーネントにインライン CSS スタイルを適用し、即座に変更をプレビューすることもできます。インラインスタイルは、テーマで設定されたスタイルよりも優先されます。

## インライン CSS プロパティを適用 {#apply-inline-css-properties}

コンポーネントにインラインスタイルを追加するには、次の手順を実行します。

1. フォームエディターでフォームを開き、モードをスタイルモードに変更します。 モードをスタイルモードに変更するには、ページツールバーで、 ![キャンバスドロップダウン](assets/Smock_ChevronDown.svg) > **[!UICONTROL スタイル]**.
1. ページ内のコンポーネントを選択し、「編集」ボタンを選択します。 ![edit-button](assets/edit.svg). スタイル設定プロパティがサイドバーに開きます。

   サイドバーのフォーム階層ツリーからコンポーネントを選択することもできます。 フォーム階層ツリーは、サイドバーでフォームオブジェクトとして使用できます。

   [!UICONTROL スタイル]モードでは、フォームオブジェクトの下にコンポーネントが表示されます。ただし、サイドバーのフォームオブジェクトリストには、フィールドやパネルなどのコンポーネントが一覧表示されます。 フィールドとパネルは、テキストボックスやラジオボタンなどのコンポーネントを含むことができる汎用コンポーネントです。

   サイドバーからコンポーネントを選択すると、選択したコンポーネントのすべてのサブコンポーネントのリストと選択したコンポーネントのプロパティが表示されます。特定のサブコンポーネントを選択して、そのスタイルを設定できます。

1. サイドバーのタブをクリックして、CSS プロパティを指定します。 次のようなプロパティを指定できます。

   * [!UICONTROL 寸法と位置]（表示設定、パディング、高さ、幅、余白、位置、z インデックス、フロート、クリア、オーバーフロー）
   * [!UICONTROL テキスト]（フォントファミリー、太さ、色、サイズ、行の高さ、整列）
   * [!UICONTROL 背景]（画像とグラデーション、背景色）
   * [!UICONTROL 境界線]（幅、スタイル、色、半径）
   * [!UICONTROL 効果]（シャドウ、不透明度）
   * [!UICONTROL 詳細]（コンポーネントのカスタム CSS を作成できます）

1. 同様に、コンポーネントの他の部分（[!UICONTROL ウィジェット]、[!UICONTROL キャプション]、[!UICONTROL ヘルプ]など）のスタイルを適用できます。
1. 選択 **[!UICONTROL 完了]** 変更を確定するか、 **[!UICONTROL キャンセル]** 変更を破棄します。

## 例：フィールドコンポーネントのインラインスタイル {#example-inline-styles-for-a-field-component}

以下の図は、インラインスタイルが適用される前後のテキストフィールドを示しています。

![インラインスタイルが適用される前のテキストボックスコンポーネント](assets/no-style.png)

インラインスタイルプロパティを適用する前のテキストボックスコンポーネント

次の画像に示すように、次の CSS プロパティを適用した後のテキストボックススタイルの変更に注意してください。

<table>
 <tbody>
  <tr>
   <td><p>セレクター</p> </td>
   <td><p>CSS プロパティ</p> </td>
   <td><p>値</p> </td>
   <td><p>効果</p> </td>
  </tr>
  <tr>
   <td><p>フィールド</p> </td>
   <td><p>境界線</p> </td>
   <td><p>境界線の幅=2px</p> <p>境界線のスタイル=実線</p> <p>境界線のカラー=#1111</p> </td>
   <td><p>フィールドの周囲に黒色の 2px 幅の境界線を作成</p> </td>
  </tr>
  <tr>
   <td><p>テキストボックス</p> </td>
   <td><p>背景色</p> </td>
   <td><p>#6495ED</p> </td>
   <td><p>背景色を CornflowerBlue (#6495ED) に変更します。</p> <p>注：値フィールドには、カラーの名前または 16 進数コードを指定できます。</p> </td>
  </tr>
  <tr>
   <td><p>ラベル</p> </td>
   <td><p>寸法と位置／幅</p> </td>
   <td><p>100px</p> </td>
   <td><p>ラベルの幅を 100 px に固定します</p> </td>
  </tr>
  <tr>
   <td>フィールドヘルプアイコン</td>
   <td>テキスト/フォントカラー</td>
   <td>#2ECC40</td>
   <td>ヘルプアイコンの色を変更します。</td>
  </tr>
  <tr>
   <td><p>詳細な説明</p> </td>
   <td><p>text-align</p> </td>
   <td><p>中央</p> </td>
   <td><p>ヘルプの長い説明を中央に揃えます</p> </td>
  </tr>
 </tbody>
</table>

![インラインスタイルが適用された後のテキストボックスのスタイル](assets/applied-style.png)

インラインスタイルプロパティを適用した後のテキストボックスコンポーネント

上記の手順に従って、パネル、送信ボタン、ラジオボタンなど、他のコンポーネントを選択してスタイルを設定できます。

>[!NOTE]
>
>スタイルのプロパティは、選択したコンポーネントにより異なります。

## スタイルをコピー＆ペースト {#copy-paste-styles}

アダプティブフォーム内のあるコンポーネントから別のコンポーネントにスタイルをコピーして貼り付けることもできます。Adobe Analytics の **[!UICONTROL スタイル]** モードで、コンポーネントを選択し、コピーアイコンを選択します。 ![コピー](assets/property-copy-icon.svg).

同じタイプの他のコンポーネントを選択し、貼り付けアイコンを選択します。 ![コピー](assets/Smock_Paste_18_N.svg) コピーしたスタイルを貼り付けます。 また、「スタイルをクリア」アイコンを選択することもできます ![コピー](assets/clear-style-icon.svg) をクリックして、適用されたスタイルをクリアします。

## コンポーネントの異なる状態にスタイルを設定 {#set-styles-for-states}

コンポーネントタイプの状態ごとにスタイルを設定できます。状態には、[!UICONTROL フォーカス]、[!UICONTROL 無効]、[!UICONTROL ホバー]、[!UICONTROL エラー]、[!UICONTROL 成功]、[!UICONTROL 必須]が含まれます。

コンポーネントの状態のスタイル設定を定義するには、次の手順を実行します。

1. Adobe Analytics の **[!UICONTROL スタイル]** モードで、コンポーネントを選択し、編集アイコンを選択します。 ![編集](assets/Smock_Edit_18_N.svg).

1. 「**[!UICONTROL 状態]**」ドロップダウンリストを使用して、コンポーネントの状態を選択します。

   ![状態を選択](assets/select-state.png)

1. コンポーネントの選択状態のスタイル設定を定義し、「 」を選択します。 ![保存](assets/save_icon.svg) をクリックしてプロパティを保存します。

成功状態とエラー状態をシミュレートすることもできます。展開アイコンを選択して、 **[!UICONTROL 成功をシミュレート]** および **[!UICONTROL エラーをシミュレート]** オプション。

![状態をシミュレート](assets/simulate-states.png)


## 関連トピック {#see-also}

{{see-also}}


<!--

>[!MORELIKETHIS]
>
>* [Use themes in Adaptive Form Core Components ](/help/forms/using-themes-in-core-components.md)

-->