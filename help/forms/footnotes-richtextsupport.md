---
title: 脚注のサポート
description: 脚注の RTE サポート。
exl-id: f04dae84-daab-42f8-876f-02fe426f62be
source-git-commit: ca0c9f102488c38dbe8c969b54be7404748cbc00
workflow-type: tm+mt
source-wordcount: '426'
ht-degree: 88%

---

# 脚注コンポーネント {#footnotecomponent}

<span class="preview"> Adobeでは、最新の拡張可能なデータキャプチャを使用することをお勧めします [コアコンポーネント](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html?lang=ja) 対象 [新しいアダプティブFormsの作成](/help/forms/creating-adaptive-form-core-components.md) または [AEM SitesページへのアダプティブFormsの追加](/help/forms/create-or-add-an-adaptive-form-to-aem-sites-page.md). これらのコンポーネントは、アダプティブFormsの作成における大幅な進歩を表し、印象的なユーザーエクスペリエンスを実現します。 この記事では、基盤コンポーネントを使用してアダプティブFormsを作成する古い方法について説明します。 </span>

**[!UICONTROL 脚注]**&#x200B;は、ページの最後に表示される追加の情報またはメモです。[!UICONTROL 脚注]は、テキスト内で数字を上付き文字として示すメモで構成されます。

脚注は、ページ上での表示順に番号が付けられます。 各脚注には、ページの下部に配置される番号に対応する上付き文字として一意の番号が付きます。番号の横には、補足情報が脚注の説明として表示されます。

![脚注の説明](/help/forms/assets/footnote_description.png)


## 脚注の使用 {#usesoffootnotes}

* 引用を提供するのに役立ちます。
* メイン情報の通常の流れを妨げる可能性のある追加情報を提供します。
* 括弧で囲まれた情報や著作権の権限を提供します。

アダプティブフォームでは、[!UICONTROL 脚注]を使用してフォームの入力方法や使用方法に関する情報が表示されます。アダプティブFormsの作成方法について詳しくは、[アダプティブフォームの作成](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/create-an-adaptive-form/create-an-adaptive-form-on-forms-cs/creating-adaptive-form.html?lang=ja)をご覧ください。

## アダプティブフォームの脚注 {#using-footnote-adaptiveforms}

アダプティブフォームに脚注を追加するには、次の手順を実行します。
1. アダプティブフォームを「**編集**」モードで開きます。
1. コンポーネントブラウザーから&#x200B;**[!UICONTROL テキスト]**&#x200B;コンポーネントを、アダプティブフォームにドラッグ＆ドロップします。
1. 追加した&#x200B;**[!UICONTROL テキスト]** コンポーネントを選択し、![cmppr](assets/configure-icon.svg) をタップしてプロパティを編集します。

   ![アダプティブフォームの脚注](/help/forms/assets/footnote_rte.png)

1. 脚注の説明を追加するテキストを選択し、![星](/help/forms/assets/asterisk.svg)ボタンをクリックして&#x200B;**[!UICONTROL 脚注]**&#x200B;コンポーネントのスタイルを設定します。

1. 「![チェック項目](/help/forms/assets/save_icon.svg)」をクリックして、変更とスタイルを保存します。

   >[!NOTE]
   >
   >* 脚注には自動的に番号が付けられ、アダプティブフォーム上で作成された方法で表示されます。
   >* 脚注が重複している場合は、重複しているすべての脚注に対して同じ数字が使用されます。

1. コンポーネントブラウザーから、**[!UICONTROL 脚注のプレースホルダー]**&#x200B;コンポーネントをアダプティブフォームにドラッグ＆ドロップします。
   >[!NOTE]
   >
   >* 公開インスタンスでは、**[!UICONTROL 脚注のプレースホルダー]**&#x200B;コンポーネントがアダプティブフォーム上に配置されている位置に脚注が表示されます。
   >* パネル間を移動すると、表示されている脚注のみが、移動したパネル内に存在する&#x200B;**[!UICONTROL 脚注のプレースホルダー]**&#x200B;に表示されます。

1. 各プロパティを保存します。

実行時に、数値が上付き文字としてテキストに表示され、[!UICONTROL 脚注のプレースホルダー]がアダプティブフォームに配置されている位置で&#x200B;**[!UICONTROL 脚注]**&#x200B;コンポーネントに対応する説明が表示されます。脚注の説明に直接移動するには、[!UICONTROL 脚注]で対応する数値をクリックします。
