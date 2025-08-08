---
title: アダプティブForms用にMarketo Engage データを設定する方法
description: アダプティブFormsでMarketo Engage スキーマを使用する方法を説明します。
keywords: アダプティブFormsでのMarketo Engage データソースの使用、Marketo インスタンスデータソースとフォームを接続する方法を教えてください。、フォームをMarketoに接続します。
feature: Adaptive Forms, Form Data Model
role: User, Developer
exl-id: 4656ec65-f1ad-4e97-8d93-25933cdc7f7b
source-git-commit: 1be7bafc1d93a65a81eeb2f7e86cac33cde7aa35
workflow-type: tm+mt
source-wordcount: '797'
ht-degree: 12%

---

# 既存のアダプティブフォーム用の Marketo Engage データソースの設定

<span class="preview">機能は、早期導入プログラムで利用できます。早期導入プログラムに参加し、機能へのアクセスをリクエストするには、公式のメール ID で aem-forms-ea@adobe.com までメールを送信してください。</span>

![ワークフロー](/help/forms/assets/workflow-marketo-2.png)

Marketo Engageを既存のAEM Formsと統合するためのクラウドサービス設定を作成したら、フォームのデータソースを設定できます。

データ統合を設定すると、ユーザーは様々なデータソースやスキーマに接続できます。 Marketo Engage データソースと統合し、異なるフォームで使用すると、そのデータに対する操作が容易になります。 アダプティブフォームでサポートされる標準提供データソースを調べるには、[ データソースの設定 ](/help/forms/configure-data-sources.md) の記事を参照してください。

## フォーム用のMarketo Engage データソースの設定に関する考慮事項

フォーム用のMarketo Engage データソースを設定する際の考慮事項は次のとおりです。

* Edge Delivery Services FormsをMarketo Engageに接続することはできません。

## フォームにMarketo Engage データソースを使用するための前提条件

フォームでMarketo Engage データソースを使用するための前提条件は次のとおりです。

* Marketo Engageを forms[ と統合するための ](/help/forms/integrate-form-to-marketo-engage.md) クラウドサービス設定を作成します。

## 既存のアダプティブフォームをMarketo Engage データソース用に設定する方法

>[!VIDEO](https://video.tv.adobe.com/v/3442871/marketo-aem-forms-aem-marketo-engage)

<span> このビデオは、コアコンポーネントにのみ適用されます。 UE/基盤コンポーネントについては、の記事を参照してください。</span>

>[!BEGINTABS]

>[!TAB 基盤コンポーネント]

Marketo Engage データソースを使用して基盤コンポーネントに基づくアダプティブフォームを設定するには、次の手順を実行します。

1. [!DNL Experience Manager Forms] オーサーインスタンスにログインします。
1. 編集用にアダプティブフォームを開き、アダプティブフォームコンテナのプロパティの **[!UICONTROL データモデル]** セクションに移動して、フォームモデルを **コネクタ** として選択します。
1. ドロップダウンリストから **[!UICONTROL コネクタ]** を選択します。
1. **[!UICONTROL コネクタ]** を選択したら、クラウド設定を選択できます。

   ![Marketo コネクタの選択 ](/help/forms/assets/select-marketo-connector-af1.png){width=50%, height=50%}

   選択したMarketo Engage設定に基づいて、フォーム要素がサイドバーの **[!UICONTROL コンテンツブラウザー]** の **[!UICONTROL データモデルオブジェクト]** タブに表示されます。 これらの要素をドラッグ&amp;ドロップして、アダプティブフォームを作成できます。

   ![Marketo データSource](/help/forms/assets/marketo-engage-data-source-af1.png){width=50%, height=50%}

1. 「**[!UICONTROL 完了]**」をクリックします。

または、アダプティブフォームのプロパティを編集して、関連する設定を変更することもできます。

これで、接続されたMarketo Engage インスタンスからのデータソースでアダプティブフォームが設定されました。 次に、データをAdobe Marketo Engageに送信するように設定します。

>[!TAB コアコンポーネント]

コアコンポーネントに基づくアダプティブフォームをMarketo Engage データソースで設定するには、次の手順を実行します。

1. [!DNL Experience Manager Forms] オーサーインスタンスにログインします。

1. アダプティブフォームを編集用に開きます。
1. コンテンツツリーを開き、「**[!UICONTROL ガイドコンテナ]**」を選択します。
1. アダプティブフォームコンテナのプロパティ（![アダプティブフォームコンテナのプロパティ](/help/forms/assets/configure-icon.svg) アイコン）をクリックします。データソースを設定するための「アダプティブフォームコンテナ」ダイアログボックスが開きます。
1. 「**[!UICONTROL データモデル]**」タブを開き、フォームモデルを「**コネクタ**」として選択します。
1. ドロップダウンリストから **[!UICONTROL コネクタ]** を選択します。

1. **[!UICONTROL コネクタ]** を選択したら、クラウド設定を選択できます。

   ![Marketo コネクタの選択 ](/help/forms/assets/select-marketo-connector.png){width=50%, height=50%}

   選択したMarketo Engage設定に基づいて、フォーム要素がサイドバーの **[!UICONTROL コンテンツブラウザー]** の **[!UICONTROL データモデルオブジェクト]** タブに表示されます。 これらの要素をドラッグ&amp;ドロップして、アダプティブフォームを作成できます。

   ![Marketo データSource](/help/forms/assets/marketo-engage-data-source.png){width=50%, height=50%}

1. 「**[!UICONTROL 完了]**」をクリックします。

または、アダプティブフォームのプロパティを編集して、関連する設定を変更することもできます。

これで、接続されたMarketo Engage インスタンスからのデータソースでアダプティブフォームが設定されました。 次に、データをAdobe Marketo Engageに送信するように設定します。

>[!TAB ユニバーサルエディター]

ユニバーサルエディターで作成したアダプティブフォームにMarketo Engage データソースを設定するには、次の手順を実行します。

1. フォームのプロパティを編集用に開きます。
1. **[!UICONTROL フォームモデル]** を選択します。
1. **フォームモデル** から **[!UICONTROL コネクタ]** を選択します。
1. **[!UICONTROL コネクタ]** を選択したら、クラウド設定を選択できます。

   ![Marketo コネクタの選択 ](/help/forms/assets/select-marketo-connector-ue.png)

1. 「**[!UICONTROL 保存して閉じる]**」をクリックします。

選択したMarketo Engage設定に基づいて、フォーム要素がプロパティパネルのコンテンツブラウザーの **[!UICONTROL データソース]** タブに表示されます。 これらの要素をドラッグ&amp;ドロップして、アダプティブフォームを作成できます。

![Marketo データSource](/help/forms/assets/marketo-engage-data-source-ue.png)

これで、接続されたMarketo Engage インスタンスからのデータソースでフォームが設定されました。 次に、データをAdobe Marketo Engageに送信するように設定します。

>[!ENDTABS]

## よくある質問（FAQ）

**Q：フォームのコネクタを変更するとどうなりますか？**\
**A:** フォームのコネクタを変更すると、既存の連結が無効になります。

**Q:Marketo Engageと統合されたフォームのルールエディターの呼び出しサービスで使用できる 3 つの操作を教えてください。**\
**A:** Marketo Engageと統合されたフォームの場合、**サービスの呼び出し** で使用できる 3 つの標準の操作は次のとおりです。
* リードを同期
* リードを ID で取得
* フィルタータイプでリードを取得

## 次の手順

これで、アダプティブForms用のMarketo Engage データソースを設定しました。 次に、[ アダプティブフォームを設定して、Marketo Engageにデータを送信する ](/help/forms/submit-adaptive-form-to-marketo-engage.md) ことができます。

## 関連記事

{{af-submit-action}}

## 関連トピック

{{marketo-engage-see-also}}
