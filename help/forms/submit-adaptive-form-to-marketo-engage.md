---
title: Forms 用にMarketo Engageに送信アクションを設定する方法
description: アダプティブフォームの送信アクションを設定して、Marketo Engageにデータを送信する方法を説明します。
keywords: Marketo engage へのデータの送信、「Marketo Engageに送信」として送信アクションを設定する
feature: Adaptive Forms, Form Data Model
role: User, Developer
exl-id: 0683564b-1ac4-42b4-bc08-101c4fdef286
source-git-commit: 1be7bafc1d93a65a81eeb2f7e86cac33cde7aa35
workflow-type: tm+mt
source-wordcount: '772'
ht-degree: 14%

---

# 既存のフォーム用の Marketo Engage に対する送信アクションの設定

<span class="preview">機能は、早期導入プログラムで利用できます。早期導入プログラムに参加し、機能へのアクセスをリクエストするには、公式のメール ID で aem-forms-ea@adobe.com までメールを送信してください。</span>

![ワークフロー](/help/forms/assets/workflow-marketo-3.png)

アダプティブFormsエディターには、アダプティブFormsデータをMarketo Engageに送信して処理するための **Adobe Marketo Engageに送信** 送信アクションが用意されています。 送信時にデータを [Adobe Marketo Engage](https://experienceleague.adobe.com/en/docs/marketo/using/home) に送信するように、既存のアダプティブフォームを設定できます。

フォームの送信を処理するための、すぐに使用できる様々な送信アクションを使用できます。 これらのオプションについて詳しくは、[アダプティブフォーム送信アクション](/help/forms/configure-submit-actions-core-components.md)の記事を参照してください。

## フォーム用にMarketo Engageに送信アクションを設定する際の考慮事項

* フォーム送信時にMarketo Engageにデータを送信するように、アダプティブフォームがMarketo Engage データソースで設定されていることを確認します。 ただし、フォームがMarketo Engage データスキーマで設定されている場合でも、送信アクションを代替アクション（**OneDrive に送信** や **SharePointに送信** などに変更することができます。

## 既存のフォームのMarketo Engageに送信アクションを設定するための前提条件

Marketo Engageへの送信アクションを設定するための前提条件は次のとおりです。

* アダプティブフォームの [Marketo Engage データソースを設定し ](/help/forms/use-marketo-engage-data-source-in-form.md) フォーム要素をMarketo Engage フィールドにバインドします。

## 既存のフォームをMarketo Engageに送信する方法

>[!VIDEO](https://video.tv.adobe.com/v/3442866/submit-action-marketo-engage-marketo-aem-aem-forms-engage)

<span> このビデオは、コアコンポーネントにのみ適用されます。 UE/基盤コンポーネントについては、の記事を参照してください。</span>


>[!BEGINTABS]

>[!TAB 基盤コンポーネント]

基盤コンポーネントに基づくアダプティブフォームの送信アクションを設定して、Adobe Marketo Engageにデータを送信できます。 Marketo Engageへの送信アクションを設定するには、次の手順を実行します。

1. [!DNL Experience Manager Forms] オーサーインスタンスにログインします。
1. 編集用にアダプティブフォームを開き、アダプティブフォームコンテナプロパティの **[!UICONTROL 送信]** セクションに移動して、送信アクションを **Marketo Engageに送信** として選択します。
1. 「**[!UICONTROL 完了]**」をクリックします。

![Marketo送信アクション ](/help/forms/assets/marketo-engage-submit-action-af.png){width=50%, height=50%}

アダプティブフォームの送信アクションを **Adobe Marketo Engageに送信** に設定すると、Marketo Engageにデータを送信して処理できます。 このデータを使用して、マーケティングキャンペーンの分析と最適化、フォローアップメールの自動化、フォーム送信に基づくワークフローのトリガーを行うことができます。

>[!TAB コアコンポーネント]

コアコンポーネントに基づくアダプティブフォームの送信アクションを設定して、Adobe Marketo Engageにデータを送信できます。 Marketo Engageへの送信アクションを設定するには、次の手順を実行します。

1. アダプティブフォームを編集用に開きます。
1. コンテンツツリーを開き、「**[!UICONTROL ガイドコンテナ]**」を選択します。
1. アダプティブフォームコンテナのプロパティ（![アダプティブフォームコンテナのプロパティ](/help/forms/assets/configure-icon.svg) アイコン）をクリックします。送信アクションを設定するための「アダプティブフォームコンテナ」ダイアログボックスが開きます。
1. 「**[!UICONTROL 送信]**」タブを開き、送信アクションを「**Marketo Engageに送信** として選択します。
1. 「**[!UICONTROL 完了]**」をクリックします。

![Marketo送信アクション ](/help/forms/assets/marketo-engage-submit-action.png){width=50%, height=50%}

アダプティブフォームの送信アクションを **Adobe Marketo Engageに送信** に設定すると、Marketo Engageにデータを送信して処理できます。 このデータを使用して、マーケティングキャンペーンの分析と最適化、フォローアップメールの自動化、フォーム送信に基づくワークフローのトリガーを行うことができます。

>[!TAB ユニバーサルエディター]

ユニバーサルエディターで作成されたアダプティブフォームの送信アクションを、Adobe Marketo Engageにデータを送信するように設定できます。 Marketo Engageへの送信アクションを設定するには、次の手順を実行します。

1. アダプティブフォームを編集用に開きます。
1. エディターで **フォームプロパティを編集** 拡張機能をクリックします。
**フォームのプロパティ** ダイアログが表示されます。

   >[!NOTE]
   >
   > * ユニバーサルエディターインターフェイスに **フォームプロパティを編集** アイコンが表示されない場合は、Extension Managerで **フォームプロパティを編集** 拡張機能を有効にします。
   > * ユニバーサルエディターで拡張機能を有効または無効にする方法については [&#128279;](https://developer.adobe.com/uix/docs/extension-manager/feature-highlights/#enablingdisabling-extensions)Extension Manager機能のハイライト &rbrace; の記事を参照してください。

1. 「**送信**」タブをクリックし、「**[!UICONTROL Marketo Engageに送信]**」送信アクションを選択します。

   ![Marketo送信アクション ](/help/forms/assets/marketo-engage-submit-action-ue.png)

1. 「**[!UICONTROL 保存して閉じる]**」をクリックします。

アダプティブフォームの送信アクションを **Adobe Marketo Engageに送信** に設定すると、Marketo Engageにデータを送信して処理できます。 このデータを使用して、マーケティングキャンペーンの分析と最適化、フォローアップメールの自動化、フォーム送信に基づくワークフローのトリガーを行うことができます。

>[!ENDTABS]

## よくある質問（FAQ）

**Q:Marketo Engage スキーマに接続するように設定されたフォームの送信アクションを変更できますか？**
**A:** デフォルトでは、Marketo Engage スキーマと接続するようにフォームが設定されている場合、**Marketoに送信** アクションが選択されています。 ただし、必要に応じて、フォームの送信アクションを変更できます。

## 次の手順

また、アダプティブフォームを [Munchkin ライブラリ ](https://experienceleague.adobe.com/en/docs/marketo/using/product-docs/administration/setup/munchkin) に接続して、訪問数、クリック数、フォーム送信数をトラッキングすることもできます。

## 関連記事

{{af-submit-action}}

## 関連トピック

{{marketo-engage-see-also}}
