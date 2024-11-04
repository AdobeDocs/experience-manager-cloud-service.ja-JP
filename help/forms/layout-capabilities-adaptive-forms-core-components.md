---
title: コアコンポーネントに基づくアダプティブFormsのレイアウト機能には何がありますか？
description: 各種デバイスごとのアダプティブフォームのレイアウトと外観はレイアウト設定で管理できます。各種レイアウトとレイアウトの適用方法について説明します。
feature: Adaptive Forms, Core Components
keywords: コアコンポーネントに基づくアダプティブフォームのレイアウト、フォームの様々なレイアウト、動的フォームレイアウト AEM、AEM Cloud Service フォームレイアウト、AEM コアコンポーネントのフォームレイアウトタイプ、アダプティブフォームのレイアウト
role: User, Developer, Admin
exl-id: dcc01d84-0d39-4fa8-ac47-71a9aba91b1e
source-git-commit: 3ab7ff01201a7da790fe556bfe68c8c76aff9698
workflow-type: tm+mt
source-wordcount: '2107'
ht-degree: 4%

---

# コアコンポーネントに基づくアダプティブ Formsのレイアウト機能


| バージョン | 記事リンク |
| -------- | ---------------------------- |
| AEM 6.5 | [ここをクリックしてください](https://experienceleague.adobe.com/docs/experience-manager-65/forms/adaptive-forms-basic-authoring/layout-capabilities-adaptive-forms.html?lang=ja#) |
| AEM as a Cloud Service（基盤コンポーネント） | [ここをクリックしてください](/help/forms/layout-capabilities-adaptive-forms.md) |
| AEM as a Cloud Service（コアコンポーネント） | この記事 |

アダプティブFormsは、フォームを効果的にレイアウトおよびデザインするためのファーストクラスのコンポーネントを提供します。 レイアウトは、フォームでのコンポーネントの表示方法を制御します。 アダプティブ Formsでは、パネル、ウィザード、アコーディオン、上部タブ/水平タブのタブ、左/垂直タブのタブなどの様々なレイアウトがサポートされています。

![ レイアウトの種類 ](/help/forms/assets/generic-layout-hero-image.png){align="center"}

## 前提条件

レイアウトの様々な機能を調べる前に、お使いの環境でコアコンポーネントが有効になっていることを確認します。 お使いの環境でコアコンポーネントを有効にする方法について詳しくは、[ ここをクリック ](/help/forms/enable-adaptive-forms-core-components.md) してください。

## アダプティブ Formsのレイアウトタイプ

コアコンポーネントに基づくアダプティブフォームは、次のタイプのレイアウトをサポートしています。
* **パネルレイアウト**
* **ウィザードのレイアウト**
* **垂直方向のレイアウト**
* **水平レイアウト**
* **アコーディオンレイアウト**

>[!BEGINTABS]

>[!TAB  パネルレイアウト ]

パネルレイアウトは、関連するフィールドを整理して、対応するコンテンツを簡単に移動および検索するのに役立ちます。 パネルレイアウトを使用すると、アダプティブフォーム内の個別のパネル、セクションまたはパネル内にフォームコンポーネントを配置できます。

![ パネルレイアウト ](/help/forms/assets/panel-layout.png)

パネルレイアウト

[ パネルコンポーネント ](https://experienceleague.adobe.com/ja/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/panel) を使用して、パネルレイアウトをフォームに追加できます。 パネルコンポーネントの様々なプロパティを設定する方法について詳しくは、[ パネルコンポーネント ](https://experienceleague.adobe.com/ja/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/panel) の記事を参照してください。

>[!TAB  ウィザードのレイアウト ]

ウィザードレイアウトは、複雑なフォームを明確な手順に分割してシンプル化するのに役立ちます。 各手順はプロセスの異なる部分を表し、ユーザーは多くの場合、「次へ **ボタンと** 前へ **ボタンを使用して手順を順番に移動し** す。 ウィザードレイアウトを使用すると、複数のセクションや手順を含むフォームを作成できます。

![ ウィザードのレイアウト ](/help/forms/assets/wizard-layout-compare.gif)

ウィザード レイアウト

[ ウィザードコンポーネント ](https://experienceleague.adobe.com/en/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/wizard) を使用して、フォームにウィザードレイアウトを追加できます。 ウィザードコンポーネントの様々なプロパティを設定する方法について詳しくは、[ ウィザードコンポーネント ](https://experienceleague.adobe.com/en/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/wizard) の記事を参照してください。

>[!TAB  垂直タブのレイアウト ]

垂直タブレイアウトは、左側のレイアウトのタブとも呼ばれます。 垂直タブレイアウトでは、フォームの左側に沿ってパネルまたはセクションが整理されます。 パネルやセクションが縦に積み重ねられたフォームのレイアウトは一般的で、読みやすさやナビゲーションが容易になります。

![ 垂直方向のレイアウト ](/help/forms/assets/vertical-tab.gif)

垂直タブレイアウト

[ 垂直タブコンポーネント ](https://experienceleague.adobe.com/ja/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/vertical-tabs) を使用して、フォームに垂直タブレイアウトを追加できます。 垂直タブコンポーネントの様々なプロパティを設定する方法について詳しくは、[ 垂直タブコンポーネント ](https://experienceleague.adobe.com/ja/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/vertical-tabs) の記事を参照してください。


>[!TAB  水平タブレイアウト ]

水平タブレイアウトは、上部レイアウトのタブとも呼ばれます。 水平タブレイアウトでは、パネルまたはセクションを並べて配置します。 このレイアウトでは、フォームまたはパネルの幅に対して直線的にフォームセクションが表示されます。


![ 水平レイアウト ](/help/forms/assets/horizontal-layout.gif)

水平タブレイアウト

[ 水平タブコンポーネント ](https://experienceleague.adobe.com/en/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/horizontal-tabs) を使用して、フォームに水平タブレイアウトを追加できます。 水平タブコンポーネントの様々なプロパティを設定する方法について詳しくは、[ 水平タブコンポーネント ](https://experienceleague.adobe.com/en/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/horizontal-tabs) の記事を参照してください。


>[!TAB  アコーディオンレイアウト ]

アコーディオンレイアウトでは、アダプティブフォーム内の折りたたみ可能なセクションまたはパネルにコンテンツが表示されます。 セクションを展開すると、内にコンテンツが表示されますが、その他のセクションは折りたたまれたままです。 大量の情報をコンパクトに表示する場合に最適です。

![ アコーディオンレイアウト ](/help/forms/assets/accordion-layout-compare.gif)

アコーディオンレイアウト

[ アコーディオンコンポーネント ](https://experienceleague.adobe.com/en/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/accordion) を使用して、フォームにアコーディオンレイアウトを追加できます。 アコーディオンコンポーネントの様々なプロパティを設定する方法について詳しくは、[ アコーディオンコンポーネント ](https://experienceleague.adobe.com/en/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/accordion) の記事を参照してください。

>[!ENDTABS]

レイアウトを挿入してフォームコンポーネントを追加する方法については、「レイアウトを挿入してフォームコンポーネントを追加する方法 [ というタイトルの節を参照してください。](#how-to-insert-a-layout-and-add-form-components-to-it)

### 適切なアダプティブフォームレイアウトを選択する方法

ユーザーエクスペリエンスとフォームの機能を最適化するには、適切なアダプティブフォームレイアウトを選択することが重要です。 この表を使用すると、使用可能な様々なレイアウトオプションを理解するのに役立ち、特定のニーズとユースケースに基づいて最も適したレイアウトを選択する際にガイドになります。

| 機能 | パネルレイアウト | ウィザード レイアウト | 上部/垂直タブレイアウトのタブ | 左側のタブ/水平タブのレイアウト | アコーディオンレイアウト |
|--------------------------|-----------------------------------------------------|----------------------------------------------------|-----------------------------------------------------|--------------------------------------------------------|--------|
| **目的** | 関連するコンテンツを個別のセクションにグループ化 | 複数の手順から成るプロセスまたはフォームのガイド | 同じページ上のセクション/ビューを切り替えることができます | 上部のタブと同様ですが、左側に垂直に配置されます | コンテンツを折りたたみ可能なセクションに整理します |
| **構造** | 個別セクション | 順次ステップ/ページ | 上部の水平タブ | 左側の垂直タブ | 折りたたみ可能なパネル/セクション |
| **ナビゲーション** | パネルヘッダーをクリックして移動します |  – 進む：「次へ」ボタン <br> – 戻る：「戻る」ボタン <br>- オプションのスキップ手順 | タブをクリックしてセクションを切り替える | タブをクリックしてセクションを切り替える | ヘッダーをクリックしてセクションを展開/折りたたむ |
| **ユーザーエクスペリエンス** | 管理しやすい方法で大量のコンテンツを整理する | ステップバイステップのガイダンス、負担の軽減 | ビュー間の明確でアクセス可能な切り替え | 垂直方向のスペースを効率的に使用し、常にタブを表示 | セクションを展開/折りたたんだ状態のコンパクト ビュー |
| **ユースケース** | セクションが分類された複雑なフォーム | セットアッププロセス、複雑なフォーム | 設定またはコンテンツカテゴリの整理 | ダッシュボード、複雑なデータビュー | FAQ、設定メニュー、詳細なコンテンツセクション |


## レイアウトを挿入し、フォームコンポーネントを追加するにはどうすればよいですか？

次の図は、フォームにレイアウトを挿入し、フォームコンポーネントを追加する手順を示しています。

![ レイアウトおよびフォームコンポーネントを追加するためのワークフロー ](/help/forms/assets/workflow-to-add-component-to-a-layout.png)

「アダプティブFormsのレイアウトタイプ **** の節に示されている [IT リクエストフォーム ](#adaptive-forms-layout-types) について考えてみます。 このフォームは、ネットワークまたはラップトップに関連する技術的な問題を抱えている従業員から情報を収集します。 次の 3 つのパネルがあります。

* **従業員の詳細**：パネルには、従業員に関する情報が収集され、名前、メール ID、部門というラベルの付いた 3 つのテキストボックスが含まれています。

* **問題の詳細**：パネルには、問題に関する詳細が取り込まれます。 ネットワーク、コンピュータ、その他の 3 つのオプションを持つ問題カテゴリのチェックボックスが含まれています。 また、「指定してください」と「コメント」という 2 つのテキストボックスも用意されています。

* **添付ファイル**：このパネルを使用すると、ユーザーは問題に関連するサポートドキュメントをアップロードできます。

レイアウトを挿入し、それにコンポーネントを追加する手順を順を追って説明します。 この例では、水平タブレイアウトをフォームに挿入します。

### 1. レイアウトコンポーネントをフォームに挿入する

1. [!DNL Experience Manager Forms] インスタンスにログインします。
1. 左上隅の「**[!UICONTROL Adobe Experience Manager]**」/「**[!UICONTROL Forms]**」/「**[!UICONTROL Formsとドキュメント]** を選択します。
1. 既存のアダプティブフォームを編集モードで開きます（作成済みの場合）。

   ![ アダプティブフォームを開く ](/help/forms/assets/insert-layout.png)

   または、[ 新しいアダプティブフォームを作成する ](/help/forms/creating-adaptive-form-core-components.md) こともできます。

1. フォームエディターでレイアウトを追加できるセクションを見つけます。

   ![ フォームエディター ](/help/forms/assets/form-editor.png)
1. **追加** アイコンをクリックします。 アイコンは、新しいコンポーネントを追加するオプションを示すプラス記号（+）です。

   ![ レイアウトの挿入 ](/help/forms/assets/insert-layout-add-icon.png)

   **追加** アイコンをクリックすると、**新規コンポーネントの挿入** ダイアログボックスが表示され、挿入する様々なコンポーネントが表示されます。

   >[!NOTE]
   >
   > または、[ レイアウトコンポーネントをドラッグ&amp;ドロップ ](#extra-bytes) することもできます。

1. ダイアログボックスで使用可能なコンポーネントを参照し、リストから目的のレイアウトを選択します。 この場合、水平タブコンポーネントを選択して、水平タブレイアウトを挿入します。

   ![ 水平タブの選択 ](/help/forms/assets/select-horizontal-tab.png)

   水平タブコンポーネントをフォームに追加すると、デフォルトでは、Item1 と Item2 という名前の 2 つの空のパネルで最初に構成されます。 これらのパネルには、手動でフォームコンポーネントを追加する必要があります。

   ![水平タブ](/help/forms/assets/insert-tabs-on-top.png)

1. 水平タブコンポーネントのプロパティを開き、コンポーネントの名前を指定します。
例えば、この場合、水平タブコンポーネントの名前を IT リクエストフォームとして追加します。

   ![ 水平タブの名前を追加 ](/help/forms/assets/change-name-of-horizontal-tabs.png)

1. 「**完了**」をクリックします。

   ![水平タブ](/help/forms/assets/tabs-on-top-rename-component.png)

レイアウトコンポーネントをフォームに追加したら、要件に従ってパネルの数を変更します。

### 2. レイアウトへのパネルの追加

水平タブコンポーネントに新しいパネルを追加します。

1. 水平タブコンポーネントのプロパティを開き、「**項目**」タブをクリックします。

   ![ 水平タブの「項目」タブ ](/help/forms/assets/tabs-on-top-items-tab.png)

1. **追加** アイコンをクリックして、新しいパネルを追加します。

   ![ 新しいパネルを追加 ](/help/forms/assets/tabs-on-top-add-panel.png)

   **追加** アイコンをクリックすると、**新規コンポーネントを挿入** ダイアログボックスが表示されます。

1. パネルコンポーネントを選択します。

   ![ 新しいパネルを追加 ](/help/forms/assets/tabs-on-top-new-panel.png)

   パネルコンポーネントを選択すると、新しいパネルが水平レイアウトに追加されます。

   ![ 新しいパネルを追加 ](/help/forms/assets/tabs-on-top-add-new-panel.png)

   新しいパネルの名前を指定します。指定しない場合、水平タブコンポーネントのプロパティを保存できません。

1. 次の図に示すように、パネルの名前を指定します。

   ![ パネル名 ](/help/forms/assets/tabs-on-tops-panel-name.png)

1. 「**完了**」をクリックします。

   「**完了**」をクリックすると、3 つのパネルが並んで表示されます。 パネル名は、各パネルの見出しとして表示され、各パネルにフォームコンポーネントを追加できます。

   ![ パネル名 ](/help/forms/assets/tabs-on-top-initial-view.png)

   パネルコンポーネントのプロパティを設定できます。 例えば、IT リクエストフォームにパネルタイトルが含まれていない場合は、パネルコンポーネントのプロパティを設定する手順を以下に示します。

1. 最初のパネルのプロパティを開きます。

   ![ パネル 1 のプロパティ ](/help/forms/assets/tabs-on-tops-panel1-properties.png)

1. 「**基本**」タブから「**タイトルを非表示**」チェックボックスを選択します。

   ![タイトルを非表示にする](/help/forms/assets/tabs-on-top-hide-panel.png)

1. 「**完了**」をクリックします。

同様に、他の 2 つのパネルのタイトルを非表示にすることもできます。 完了したら、フォームコンポーネントを各パネルに追加できます。

### 3. パネルへのフォームコンポーネントの追加

<!-- You can employ one of the following method to add form components to the panel:
* [Add components to a layout's panel using the Add icon](#add-components-to-a-layouts-panel-using-the-add-icon)
* [Drag and drop components into a layout's panel](#drag-and-drop-components-into-a-layouts-panel) -->

1. パネル内で、コンポーネントを追加できるセクションを見つけます。
1. **追加** アイコンをクリックします。 アイコンは、新しいコンポーネントを追加するオプションを示すプラス記号（+）です。
   ![ レイアウトの挿入 ](/help/forms/assets/tabs-on-top-add-component.png)

   **追加** アイコンをクリックすると、**新規コンポーネントの挿入** ダイアログボックスが表示され、挿入する様々なコンポーネントが表示されます。

   ![ 新規コンポーネントを挿入ダイアログボックス ](/help/forms/assets/insert-new-component.png)

1. 表示されるダイアログボックスで使用可能なコンポーネントを参照し、目的のコンポーネントを選択します。 この場合は、テキストボックスコンポーネントを選択します。
1. 追加したコンポーネントのプロパティを開き、名前を指定します。 追加したテキストボックスコンポーネントのプロパティを編集し、その名前を指定します。
   ![ レイアウトの挿入 ](/help/forms/assets/tabs-on-top-textbox-component.png)
1. 同様に、さらに 2 つのテキストボックスコンポーネントを追加し、それらのコンポーネントに名前を付けて、メール ID および部門として追加します。\
   ![ 最初のパネル ](/help/forms/assets/tabs-on-tops-first-panel.png)

   最初のパネルのコンポーネントが追加されたので、次に 2 番目のパネルへのコンポーネントの追加に進むことができます。

1. パネルを切り替えるには、ツールバーの **パネルを選択** をクリックします。

   ![ スイッチパネル ](/help/forms/assets/tabs-on-top-select-panel.png)

   **パネルを選択** をクリックすると、水平タブコンポーネントに追加されたパネルのリストが表示されます。

   ![ スイッチパネル ](/help/forms/assets/tabs-on-tops-panel2.png)

1. パネルリストから「**2 パネル**」を選択すると、ビューが 1 番目のパネルから 2 番目のパネルに変更されます。

   ![2 番目のパネル ](/help/forms/assets/tabs-on-top-panel2-component.png)

1. 次の図に示すように、手順 2 から手順 4 までの手順を繰り返して、パネル 2 に目的のコンポーネントを追加します。

   ![2 番目のパネルコンポーネント ](/help/forms/assets/panel-2-components.png)

1. 手順 6 と手順 7 で説明した手順に従って、**3 パネル** に切り替えます。

1. パネル 3 に目的のコンポーネントを追加するには、手順 2 から手順 4 までの手順を繰り返します。

   ![3 番目のパネルコンポーネント ](/help/forms/assets/panel-3-component.png)

1. オーサリング環境の右上隅にある「**[!UICONTROL プレビュー]**」をクリックします。
   ![ 水平レイアウト ](/help/forms/assets/horizontal-layout.gif)

また、[ コンポーネントをドラッグ&amp;ドロップ ](#extra-bytes) して、フォームコンポーネントを各パネルに追加することもできます。


<!-- #### Drag and drop components into a layout's panel 

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



「![ 削除アイコン ](/help/forms/assets/Smock_Delete_18_N.svg) アイコンを使用して、パネルからフォームコンポーネントを削除することもできます。

![コンポーネントの削除](/help/forms/assets/delete-component.png)

必要に応じて、コンポーネントに必要な検証を追加することもできます。

## 既存のレイアウトを新しいレイアウトに置き換える方法

フォームのレイアウトを新しいレイアウトに置き換えることができます。その際、フォーム内でコンポーネントを配置および表示する方法を変更します。

フォームの既存のレイアウトを置き換えるには、次の手順を実行します。

1. レイアウトコンポーネントのツールバーにある置換アイコンをクリックすると、**[!UICONTROL コンポーネントを置換]** ダイアログボックスが表示されます。

   ![ レイアウトの置換 ](/help/forms/assets/replace-layout.png)

1. **[!UICONTROL コンポーネントを置換]** ダイアログボックスから目的のレイアウトを選択します。

   ![ コンポーネントを置換ダイアログボックス ](/help/forms/assets/replace-component.png)

   レイアウトを選択すると、それに応じてレイアウト内のコンポーネントの配置が変わります。 例えば、**[!UICONTROL コンポーネントを置換]** ダイアログボックスで垂直タブコンポーネントを選択すると、パネルの配置が左側のタブに変わります。

   ![ 垂直方向のレイアウト ](/help/forms/assets/vertical-tab.gif)

## 追加バイト

コンポーネントをフォームエディターにドラッグ&amp;ドロップするには、次の手順を実行します。

1. コンポーネントを追加できるセクションを見つけます。
1. オーサリング環境内の左側のパネルに移動し、「**コンポーネント**」をクリックします。

   ![ コンポーネントパネル ](/help/forms/assets/add-new-component.png)

   「**コンポーネント**」オプションをクリックすると、使用可能なコンポーネントのリストが表示されます。

   ![ コンポーネントパネル ](/help/forms/assets/add-new-component2.png)

1. 使用可能なコンポーネントを参照し、目的のコンポーネントを選択します。

1. 選択したコンポーネントをクリックして押したままコンポーネントをドラッグし、パネル領域にドラッグして配置します。

1. マウスを離して、コンポーネントをパネルにドロップします。

## 次の手順

コアコンポーネントに基づくアダプティブフォームの様々なレイアウト機能を理解したら、次の手順に進むことができます。

* [コアコンポーネントに基づく最初のアダプティブフォームの作成](/help/forms/creating-adaptive-form-core-components.md)
* [アダプティブフォームテーマの作成と使用](/help/forms/using-themes-in-core-components.md)



## 関連トピック

{{see-also}}
