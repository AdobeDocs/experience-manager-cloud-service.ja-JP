---
title: 脚注のサポート
description: 脚注の RTE サポート。
source-git-commit: 6f6cf5657bf745a2e392a8bfd02572aa864cc69c
workflow-type: tm+mt
source-wordcount: '369'
ht-degree: 0%

---

# 脚注コンポーネント {#footnotecomponent}

**[!UICONTROL 脚注]** は、ページの最後に表示される追加の情報またはメモです。 [!UICONTROL 脚注] は、テキスト内で数字を上付き文字として示すメモで構成されます。

脚注は、ページ上での表示順に順番に番号が付けられます。 各脚注には、ページの下部に配置される番号に対応する上付き文字として一意の番号が付きます。 番号の横には、補足情報が脚注の説明として表示されます。

![脚注の説明](/help/forms/assets/footnote_description.png)


## 脚注の使用 {#usesoffootnotes}

* 引用を提供するのに役立ちます。
* メイン情報の通常の流れを妨げる可能性のある追加情報を提供します。
* 括弧で囲まれた情報や著作権の権限を提供します。

アダプティブFormsでは、 [!UICONTROL 脚注] を使用して、フォームの入力方法や使用方法に関する情報を表示します。 アダプティブFormsの作成方法について詳しくは、 [アダプティブフォームの作成](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/create-an-adaptive-form/create-an-adaptive-form-on-forms-cs/creating-adaptive-form.html).

## アダプティブFormsの脚注 {#using-footnote-adaptiveforms}

アダプティブFormsに脚注を追加するには、次の手順を実行します。
1. でアダプティブフォームを開く **編集** モード。
1. コンポーネントブラウザーから、 **[!UICONTROL テキスト]** コンポーネントをアダプティブフォームに追加します。
1. を選択します。 **[!UICONTROL テキスト]** 追加したコンポーネントをタップします。 ![cmppr](assets/configure-icon.svg) プロパティを編集します。

   ![アダプティブFormsの脚注](/help/forms/assets/footnote_rte.png)

1. 脚注の説明を追加するテキストを選択し、  ![星](/help/forms/assets/asterisk.svg) ボタンをクリックしてスタイルを設定 **[!UICONTROL 脚注]** コンポーネント。

1. クリック ![check](/help/forms/assets/save_icon.svg) をクリックして、変更とスタイルを保存します。

   >[!NOTE]
   >
   >* 脚注は自動的に番号が付けられ、アダプティブフォーム上で作成された方法で表示されます。
   >* 脚注が重複している場合は、重複しているすべての脚注に対して同じ数字が使用されます。


1. コンポーネントブラウザーから、 **[!UICONTROL 脚注のプレースホルダー]** コンポーネントをアダプティブフォームに追加します。
   >[!NOTE]
   >
   >* パブリッシュインスタンスでは、脚注は **[!UICONTROL 脚注のプレースホルダー]** コンポーネントがアダプティブフォーム上に配置されている。
   >* 異なるパネル間を移動すると、表示されている脚注のみが **[!UICONTROL 脚注のプレースホルダー]** ナビゲーションされたパネル内に存在する


1. 各プロパティを保存します。

実行時に、数値が上付き文字としてテキストに表示され、対応する説明が **[!UICONTROL 脚注]** 位置の構成要素 [!UICONTROL 脚注のプレースホルダー] がアダプティブフォームに配置されていることを確認します。 脚注の説明に直接移動するには、 [!UICONTROL 脚注].