---
title: コアコンポーネントに基づくアダプティブFormsのレイアウト機能は何ですか？
description: 各種デバイスごとのアダプティブフォームのレイアウトと外観はレイアウト設定で管理できます。 各種レイアウトとレイアウトの適用方法について説明します。
feature: Adaptive Forms, Core Components
keywords: コアコンポーネントに基づくアダプティブフォームのレイアウト、フォームのさまざまなレイアウト、ダイナミックフォームレイアウト AEM、AEM Cloud Service フォームレイアウト、AEM コアコンポーネントのフォームレイアウトタイプ、アダプティブフォームレイアウト
role: User, Developer, Admin
badgeSaas: label="AEM Forms" type="Positive" tooltip="AEM Formsに適用）。"
exl-id: dcc01d84-0d39-4fa8-ac47-71a9aba91b1e
source-git-commit: fa8035f826a4d08c18bc0d2b7664015c6fc82698
workflow-type: tm+mt
source-wordcount: '2276'
ht-degree: 25%

---

# コアコンポーネントに基づくアダプティブFormsのレイアウト機能


| バージョン | 記事リンク |
| -------- | ---------------------------- |
| AEM 6.5 | [ここをクリックしてください](https://experienceleague.adobe.com/docs/experience-manager-65/forms/adaptive-forms-basic-authoring/layout-capabilities-adaptive-forms.html?lang=ja#) |
| AEM as a Cloud Service（基盤コンポーネント） | [ここをクリックしてください](/help/forms/layout-capabilities-adaptive-forms.md) |
| AEM as a Cloud Service（コアコンポーネント） | この記事 |

アダプティブ Formsには、効果的なフォームのレイアウトとデザインを実現する優れたコンポーネントが用意されています。 レイアウトは、フォームでのコンポーネントの表示方法を制御します。 アダプティブ Formsでは、パネル、ウィザード、アコーディオン、上/横タブのタブ、左/縦タブのタブなど、様々なレイアウトをサポートしています。

<!-- ![Types of Layout](/help/forms/assets/generic-layout-hero-image.png){align="center"}-->

## 適用性とユースケース

### 保険

## AEM Formsは、マルチステップの保険金請求フォームに対応していますか？

はい。 AEM Formsは、条件付きロジックを使用したガイド付きマルチステップのアダプティブフォームをサポートしています。これにより、保険会社は請求内容の種類とコンテキストに基づいて、請求情報を段階的に収集できます。

## お客様は、AEM Formsを使用して請求書類を安全にアップロードできますか？

はい。 AEM Formsは、フォーム送信の一部として安全なドキュメントのアップロードをサポートしています。エンタープライズのセキュリティ要件に合わせて、アクセス制御と安全なデータ処理を行うことができます。


## アダプティブFormsのレイアウトタイプ

コアコンポーネントに基づくアダプティブフォームでは、次の種類のレイアウトをサポートしています。

* **パネルレイアウト**
* **ウィザードレイアウト**
* **垂直レイアウト**
* **水平レイアウト**
* **アコーディオンレイアウト**

>[!BEGINTABS]

>[!TAB パネルレイアウト]

パネルレイアウトは、関連するフィールドを整理して、対応するコンテンツを簡単に移動および検索するのに役立ちます。 パネルレイアウトは、アダプティブフォーム内の個別のセクションまたはパネル内にフォームコンポーネントを配置します。

![パネルレイアウト](/help/forms/assets/panel-layout.png)

パネルレイアウト

[パネルコンポーネント](https://experienceleague.adobe.com/ja/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/panel)を使用して、フォームにパネルレイアウトをフォームに追加できます。 パネルコンポーネントの様々なプロパティを設定する方法について詳しくは、[パネルコンポーネント](https://experienceleague.adobe.com/ja/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/panel)の記事を参照してください。

>[!TAB ウィザードレイアウト]

ウィザードレイアウトは、複雑なフォームを明確な手順に分割して簡素化するのに役立ちます。 各ステップはプロセスの異なる部分を表し、ユーザーは&#x200B;**次** ボタンと&#x200B;**前** ボタンを使用して順にステップを進みます。 ウィザードレイアウトを使用して、複数のセクションや手順を含むフォームを作成できます。

![ウィザードレイアウト](/help/forms/assets/wizard-layout-compare.gif)

ウィザードレイアウト

[ウィザードコンポーネント](https://experienceleague.adobe.com/ja/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/wizard)を使用して、フォームにウィザードレイアウトを追加できます。 ウィザードコンポーネントの様々なプロパティを設定する方法について詳しくは、[ウィザードコンポーネント](https://experienceleague.adobe.com/ja/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/wizard)の記事を参照してください。

>[!TAB 縦組みタブのレイアウト ]

垂直方向のタブレイアウトは、左側のレイアウトのタブとも呼ばれます。 縦組みタブのレイアウトは、フォームの左側に沿ってパネルまたはセクションを整理します。 パネルやセクションが垂直方向に積み重ねられ、読みやすく、ナビゲーションしやすくなるフォームの一般的なレイアウトです。

![縦レイアウト &#x200B;](/help/forms/assets/vertical-tab.gif)

縦組みタブレイアウト

[縦組みタブ コンポーネント &#x200B;](https://experienceleague.adobe.com/ja/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/vertical-tabs)を使用して、縦組みタブ レイアウトをフォームに追加できます。 縦組みタブコンポーネントの様々なプロパティを設定する方法について詳しくは、[縦組みタブコンポーネント &#x200B;](https://experienceleague.adobe.com/ja/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/vertical-tabs)の記事を参照してください。


>[!TAB 横組みタブのレイアウト ]

水平タブレイアウトは、上部レイアウトのタブとも呼ばれます。 水平タブレイアウトでは、パネルまたはセクションが横に並べて配置されます。 このレイアウトでは、フォームまたはパネルの幅にわたってフォームセクションが直線的に表示されます。


![水平レイアウト &#x200B;](/help/forms/assets/horizontal-layout.gif)

横組みタブレイアウト

[水平タブコンポーネント &#x200B;](https://experienceleague.adobe.com/ja/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/horizontal-tabs)を使用して、フォームに水平タブレイアウトを追加できます。 横組みタブコンポーネントの様々なプロパティを設定する方法について詳しくは、[横組みタブコンポーネント &#x200B;](https://experienceleague.adobe.com/ja/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/horizontal-tabs)の記事を参照してください。


>[!TAB アコーディオンレイアウト]

アコーディオンレイアウトでは、アダプティブフォーム内の折りたたみが可能なセクションまたはパネルにコンテンツが表示されます。 セクションを展開すると、そのセクション内のコンテンツが表示されますが、他のセクションは折りたたまれたままになります。 このレイアウトは、大量の情報をコンパクトなフォームで表示する場合に最適です。

![アコーディオンレイアウト](/help/forms/assets/accordion-layout-compare.gif)

アコーディオンレイアウト

[アコーディオンコンポーネント](https://experienceleague.adobe.com/ja/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/accordion)を使用して、フォームにアコーディオンレイアウトを追加できます。 アコーディオンコンポーネントの様々なプロパティを設定する方法について詳しくは、[アコーディオンコンポーネント](https://experienceleague.adobe.com/ja/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/accordion)の記事を参照してください。

>[!ENDTABS]

レイアウトを挿入してフォームコンポーネントを追加する方法については、「[&#x200B; レイアウトを挿入してフォームコンポーネントを追加する方法は？](#how-to-insert-a-layout-and-add-form-components-to-it)」の節を参照してください。

### 適切なアダプティブフォームのレイアウトを選択する方法

ユーザーエクスペリエンスとフォーム機能を最適化するには、適切なアダプティブフォームのレイアウトを選択することが重要です。 この表は、利用可能な様々なレイアウトオプションを理解するのに役立ち、特定のニーズやユースケースに基づいて最適なレイアウトを選択する際に役立ちます。

| 機能 | パネルレイアウト | ウィザードレイアウト | 上/縦のタブレイアウトのタブ | 左/水平タブレイアウトのタブ | アコーディオンレイアウト |
|--------------------------|-----------------------------------------------------|----------------------------------------------------|-----------------------------------------------------|--------------------------------------------------------|--------|
| **目的** | 関連するコンテンツを個別のセクションにグループ化 | 複数の手順で構成されるプロセスやフォームを通じてユーザーに説明 | 同じページ上のセクションやビューを切り替えることができます | 上のタブに似ていますが、左に垂直に配置されています | コンテンツを折りたたみ可能なセクションに整理 |
| **構造** | 個別のセクション | 順次手順／ページ | 上部の横組みタブ | 左側の垂直タブ | 折りたたみ可能なパネル／セクション |
| **ナビゲーション** | パネルヘッダーをクリックして移動 | - 進む：「次へ」ボタン<br> - 戻る：「戻る」ボタン<br> - オプションのスキップ手順 | タブをクリックしてセクションを切り替える | タブをクリックしてセクションを切り替える | ヘッダーをクリックしてセクションを展開／折りたたむ |
| **ユーザーエクスペリエンス** | 管理しやすい方法で大量のコンテンツを整理 | ステップバイステップのガイダンスで負担を軽減 | ビュー間の明確でアクセスしやすい切り替え | 垂直方向のスペース、常に表示されるタブの効率的な使用 | セクションを展開／折りたたんだ状態のコンパクトビュー |
| **ユースケース** | セクションが分類された複雑なフォーム | 設定プロセス、複雑なフォーム | 設定やコンテンツカテゴリの整理 | ダッシュボード，複雑なデータビュー | よくある質問、設定メニュー、詳細なコンテンツセクション |


## レイアウトを挿入してフォームコンポーネントを追加する方法

次の図は、レイアウトをフォームに挿入し、フォームコンポーネントをフォームに追加する手順を示しています。

![&#x200B; レイアウトとフォームコンポーネントを追加するワークフロー](/help/forms/assets/workflow-to-add-component-to-a-layout.png)

「[&#x200B; アダプティブ Forms レイアウトの種類](#adaptive-forms-layout-types)」セクションに表示されている&#x200B;**IT リクエストフォーム**&#x200B;を検討してください。 このフォームは、ネットワークまたはノートパソコンに関連する技術的な問題を経験している従業員から情報を収集します。 3つのパネルが含まれています。

* **従業員の詳細**: パネルには、従業員に関する情報が収集され、「名前」、「電子メール ID」、「部署」というラベルの3つのテキストボックスが含まれています。

* **問題の詳細**: パネルには、問題に関する詳細が表示されます。 問題カテゴリのチェックボックスが表示され、ネットワーク、コンピューター、その他の3つのオプションが表示されます。 また、「Please Specify」と「Comments」というラベルの付いた2つのテキストボックスも備えています。

* **添付ファイル**: パネルを使用すると、問題に関連するサポートドキュメントをユーザーがアップロードできます。

レイアウトを挿入してコンポーネントを追加する手順を見てみましょう。 この例では、水平タブレイアウトがフォームに挿入されています。

### &#x200B;1. レイアウトコンポーネントのフォームへの挿入

1. [!DNL Experience Manager Forms] インスタンスにログインします。
1. 左上隅で、**[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL Forms]** > **[!UICONTROL Formsとドキュメント]**&#x200B;を選択します。
1. 既存のアダプティブフォームが作成済みの場合は、編集モードで開きます。

   ![&#x200B; アダプティブフォームを開く](/help/forms/assets/insert-layout.png)

   または、[新しいアダプティブフォームを作成](/help/forms/creating-adaptive-form-core-components.md)することもできます。

1. フォームビルダー内で、レイアウトを追加できるセクションを探します。

   ![&#x200B; フォームビルダー](/help/forms/assets/form-editor.png)
1. **追加**&#x200B;アイコンをクリックします。 アイコンはプラス記号（+）で、新しいコンポーネントを追加するオプションを示します。

   ![&#x200B; レイアウトを挿入](/help/forms/assets/insert-layout-add-icon.png)

   **追加**&#x200B;アイコンをクリックすると、**新規コンポーネントを挿入**&#x200B;ダイアログボックスが表示され、挿入する様々なコンポーネントが表示されます。

   >[!NOTE]
   >
   > または、[&#x200B; レイアウトコンポーネント &#x200B;](#extra-bytes)をドラッグ&amp;ドロップすることもできます。

1. ダイアログボックスで使用可能なコンポーネントを参照し、リストから目的のレイアウトを選択します。 この場合は、水平タブコンポーネントを選択して、水平タブレイアウトを挿入します。

   ![横組みタブを選択](/help/forms/assets/select-horizontal-tab.png)

   水平タブコンポーネントをフォームに追加すると、初期設定ではItem1とItem2という名前の2つの空のパネルで構成されます。 これらのパネルにフォームコンポーネントを手動で追加する必要があります。

   ![水平タブ](/help/forms/assets/insert-tabs-on-top.png)

1. 水平タブコンポーネントのプロパティを開き、コンポーネントの名前を指定します。
例えば、この場合、水平タブコンポーネントの名前をIT リクエストフォームとして追加します。

   ![横組みタブの名前を追加](/help/forms/assets/change-name-of-horizontal-tabs.png)

1. 「**完了**」をクリックします。

   ![水平タブ](/help/forms/assets/tabs-on-top-rename-component.png)

レイアウトコンポーネントがフォームに追加されたら、必要に応じてパネルの数を変更します。

### &#x200B;2. レイアウトへのパネルの追加

水平タブコンポーネントに新しいパネルを追加します。

1. 水平タブコンポーネントのプロパティを開き、**項目** タブをクリックします。

   ![横組みタブの「項目」タブ &#x200B;](/help/forms/assets/tabs-on-top-items-tab.png)

1. 「**追加**」アイコンをクリックして、新しいパネルを追加します。

   ![新しいパネルを追加](/help/forms/assets/tabs-on-top-add-panel.png)

   **追加** アイコンをクリックすると、**新しいコンポーネントを挿入** ダイアログボックスが表示されます。

1. パネルコンポーネントを選択します。

   ![新しいパネルを追加](/help/forms/assets/tabs-on-top-new-panel.png)

   パネルコンポーネントを選択すると、新しいパネルが水平レイアウトに追加されます。

   ![新しいパネルを追加](/help/forms/assets/tabs-on-top-add-new-panel.png)

   新しいパネルの名前を指定します。指定しない場合、水平タブコンポーネントのプロパティは保存できません。

1. 次の図に示すように、パネルの名前を指定します。

   ![&#x200B; パネル名](/help/forms/assets/tabs-on-tops-panel-name.png)

1. 「**完了**」をクリックします。

   **完了**&#x200B;をクリックすると、3つのパネルが並べて表示されます。 パネル名は各パネルの見出しとして表示され、各パネルにフォームコンポーネントを追加できます。

   ![&#x200B; パネル名](/help/forms/assets/tabs-on-top-initial-view.png)

   パネルコンポーネントのプロパティを設定できます。 例えば、IT リクエストフォームにはパネルタイトルが含まれていません。パネルコンポーネントのプロパティを設定する手順を次に示します。

1. 最初のパネルのプロパティを開きます。

   ![&#x200B; パネル 1 プロパティ &#x200B;](/help/forms/assets/tabs-on-tops-panel1-properties.png)

1. 「**基本**」タブから「**タイトルを非表示**」チェックボックスを選択します。

   ![タイトルを非表示にする](/help/forms/assets/tabs-on-top-hide-panel.png)

1. 「**完了**」をクリックします。

同様に、他の2つのパネルのタイトルも非表示にできます。 完了したら、各パネルにフォームコンポーネントを追加します。

### &#x200B;3. パネルへのフォームコンポーネントの追加

<!--
 You can employ one of the following method to add form components to the panel:
* [Add components to a layout's panel using the Add icon](#add-components-to-a-layouts-panel-using-the-add-icon)
* [Drag and drop components into a layout's panel](#drag-and-drop-components-into-a-layouts-panel)
-->

1. コンポーネントを追加できるセクションをパネル内で探します。
1. 「**追加**」アイコンをクリックします。アイコンは、新しいコンポーネントを追加するオプションを示すプラス記号（+）です。
   ![&#x200B; レイアウトを挿入](/help/forms/assets/tabs-on-top-add-component.png)

   **追加**&#x200B;アイコンをクリックすると、**新規コンポーネントを挿入**&#x200B;ダイアログボックスが表示され、挿入する様々なコンポーネントが表示されます。

   ![新しいコンポーネントダイアログボックスを挿入](/help/forms/assets/insert-new-component.png)

1. 表示されるダイアログボックスで使用可能なコンポーネントを参照し、目的のコンポーネントを選択します。 この場合は、テキストボックスコンポーネントを選択します。
1. 追加したコンポーネントのプロパティを開き、名前を指定します。追加したテキストボックスコンポーネントのプロパティを編集し、名前を指定します。
   ![&#x200B; レイアウトを挿入](/help/forms/assets/tabs-on-top-textbox-component.png)
1. 同様に、さらに2つのテキストボックスコンポーネントと名前を追加し、コンポーネントをメール IDと部署として追加しました。\
   ![最初のパネル &#x200B;](/help/forms/assets/tabs-on-tops-first-panel.png)

   最初のパネルのコンポーネントが追加されたので、2番目のパネルへのコンポーネントの追加に進むことができます。

1. パネルを切り替えるには、ツールバーの「**パネルを選択**」をクリックします。

   ![&#x200B; パネルを切り替え](/help/forms/assets/tabs-on-top-select-panel.png)

   **パネルを選択**&#x200B;をクリックすると、水平タブコンポーネントに追加されたパネルのリストが表示されます。

   ![&#x200B; パネルを切り替え](/help/forms/assets/tabs-on-tops-panel2.png)

1. パネルリストから「**2 Panel**」を選択すると、表示が最初のパネルから2番目のパネルに変わります。

   ![2番目のパネル &#x200B;](/help/forms/assets/tabs-on-top-panel2-component.png)

1. 次の図に示すように、パネル 2に目的のコンポーネントを追加するために、手順2から手順4の手順を繰り返します。

   ![2番目のパネルコンポーネント &#x200B;](/help/forms/assets/panel-2-components.png)

1. 手順6と手順7で説明した手順に従って、**3 パネル**&#x200B;に切り替えます。

1. パネル 3に目的のコンポーネントを追加するには、手順2から手順4の手順を繰り返します。

   ![3番目のパネルコンポーネント &#x200B;](/help/forms/assets/panel-3-component.png)

1. オーサリング環境の右上隅にある「**[!UICONTROL プレビュー]**」をクリックします。
   ![水平レイアウト &#x200B;](/help/forms/assets/horizontal-layout.gif)

[&#x200B; コンポーネントをドラッグ&amp;ドロップ &#x200B;](#extra-bytes)して、各パネルにフォームコンポーネントを追加することもできます。


<!--
 #### Drag and drop components into a layout's panel 

1. Locate the section within the panel that allows you to add components. 
2. Navigate to the left panel within your authoring environment and click **Components**.

    ![Component Panel](/help/forms/assets/add-new-component.png){width="200" align="center"}

    When you click the **Components** option, the list of the available components appears.   

    ![Component Panel](/help/forms/assets/add-new-component2.png){width="200" align="center"}

3. Browse the available components and select the Text Box component.

4. Drag the component by clicking and holding the selected component, then drag it over to the panel area to place it.

5. Drop the component into the panel by releasing the mouse. 

6. Open the properties of the added Text Box component and specify its name as Name.
    ![Insert layout](/help/forms/assets/tabs-on-top-textbox-component.png){width="200" align="center"}
7. Similarly, add two more Text Box components and name added the components as Email ID and Department.   
    ![First Panel](/help/forms/assets/tabs-on-tops-first-panel.png){width="200" align="center"}

    Now that the components in the first panel have been added, you can proceed with adding the components to the second panel. 

8. To switch the panel, click **Select Panel** from the toolbar. 

    ![Switch Panel](/help/forms/assets/tabs-on-top-select-panel.png){width="200" align="center"}

    When you click the **Select Panel**, the list of the added panels in the Horizontal Tabs component appears.

    ![Switch Panel](/help/forms/assets/tabs-on-tops-panel2.png){width="200" align="center"}

9. Select **2 Panel** from the panel list and the view changes from the first panel to the second panel.

    ![Second Panel](/help/forms/assets/tabs-on-top-panel2-component.png){width="200" align="center"}

10. Repeat the steps outlined from Step 2 to Step 6 for adding the desired components in panel 2 as shown in the below figure:   

     ![Second Panel components](/help/forms/assets/panel-2-components.png){width="200" align="center"}

11. Switch to the **3 Panel** by following the steps outlined in Step 8 and Step 9.

12. Repeat the steps outlined from Step 2 to Step 6 for adding the desired component in panel 3:

    ![Third Panel components](/help/forms/assets/panel-3-component.png){width="200" align="center"} 

    -->



![削除アイコン &#x200B;](/help/forms/assets/Smock_Delete_18_N.svg) アイコンを使用して、パネルからフォームコンポーネントを削除することもできます。

![コンポーネントの削除](/help/forms/assets/delete-component.png)

必要に応じて、コンポーネントに必要な検証を追加することもできます。

## 既存のレイアウトを新しいレイアウトに置き換えるには？

フォームのレイアウトを新しいレイアウトに置き換えて、フォーム内でのコンポーネントの配置方法や表示方法を変更できます。

フォームの既存のレイアウトを置き換えるには、次の手順を実行します。

1. レイアウトコンポーネントのツールバーから「置換」アイコンをクリックすると、**[!UICONTROL コンポーネントの置換]** ダイアログボックスが表示されます。

   ![&#x200B; レイアウトを置換](/help/forms/assets/replace-layout.png)

1. 「**[!UICONTROL コンポーネントを置換]**」ダイアログボックスから目的のレイアウトを選択します。

   ![&#x200B; コンポーネントの置換ダイアログボックス &#x200B;](/help/forms/assets/replace-component.png)

   レイアウトを選択すると、それに応じてレイアウト内のコンポーネントの配置が変更されます。 例えば、**[!UICONTROL コンポーネントを置換]** ダイアログボックスから垂直方向のタブコンポーネントを選択します。パネルの配置は、左側のタブに変わります。

   ![縦レイアウト &#x200B;](/help/forms/assets/vertical-tab.gif)

## 余分なバイト

フォームビルダーにコンポーネントをドラッグ&amp;ドロップするには、次の手順を実行します。

1. コンポーネントを追加できるセクションを見つけます。
1. オーサリング環境内の左側のパネルに移動し、**コンポーネント**&#x200B;をクリックします。

   ![&#x200B; コンポーネントパネル &#x200B;](/help/forms/assets/add-new-component.png)

   「**コンポーネント**」オプションをクリックすると、使用可能なコンポーネントのリストが表示されます。

   ![&#x200B; コンポーネントパネル &#x200B;](/help/forms/assets/add-new-component2.png)

1. 使用可能なコンポーネントを参照し、目的のコンポーネントを選択します。

1. 選択したコンポーネントをクリックして押したままコンポーネントをドラッグし、パネル領域にドラッグして配置します。

1. マウスを放して、コンポーネントをパネルにドロップします。

## 次の手順

コアコンポーネントに基づくアダプティブフォームの様々なレイアウト機能について理解したら、次の手順に進みます。

* [コアコンポーネントに基づく最初のアダプティブフォームの作成](/help/forms/creating-adaptive-form-core-components.md)
* [アダプティブフォームのテーマの作成と使用](/help/forms/using-themes-in-core-components.md)



## 関連トピック

{{see-also}}
