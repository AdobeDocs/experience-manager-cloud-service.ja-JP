---
title: アダプティブForms用にMarketo Engage データを設定する方法
description: アダプティブFormsでMarketo Engage スキーマを使用する方法について説明します。
keywords: アダプティブFormsでMarketo Engage データソースを使用する場合は、「Marketo インスタンスのデータソースをフォームに接続する方法」を参照してください。 、フォームをMarketoに接続します。
feature: Adaptive Forms, Form Data Model
role: User, Developer
badgeSaas: label="AEM Forms" type="Positive" tooltip="AEM Formsに適用）。"
exl-id: 4656ec65-f1ad-4e97-8d93-25933cdc7f7b
source-git-commit: 08fe79147c81c0a5b319fef3ef7733b6053b399a
workflow-type: tm+mt
source-wordcount: '751'
ht-degree: 11%

---

# 既存のアダプティブフォーム用の Marketo Engage データソースの設定

![ワークフロー](/help/forms/assets/workflow-marketo-2.png)

Marketo Engageを既存のAEM Formsと統合するためのクラウドサービス設定を作成した後、フォームのデータソースを設定できます。

データ統合を設定すると、ユーザーはさまざまなデータソースやスキーマに接続できます。 Marketo Engageのデータソースと統合し、さまざまなフォームで活用することで、データの運用を促進できます。 アダプティブフォームでサポートされているすぐに使用できるデータソースについて詳しくは、[&#x200B; データソースの設定](/help/forms/configure-data-sources.md)の記事を参照してください。

## フォームにMarketo Engage データソースを使用するための前提条件

フォームでMarketo Engage データソースを使用するための前提条件：

* [&#x200B; クラウドサービス設定を作成して、Marketo Engageとforms](/help/forms/integrate-form-to-marketo-engage.md)を統合します。

## Marketo Engage データソース用に既存のアダプティブフォームを設定する方法

>[!VIDEO](https://video.tv.adobe.com/v/3442871/marketo-aem-forms-aem-marketo-engage)

<span>このビデオは、コアコンポーネントのみに適用されます。 UE／基盤コンポーネントについて詳しくは、記事を参照してください。</span>

>[!BEGINTABS]

>[!TAB 基盤コンポーネント]

Marketo Engage データソースを使用して、基盤コンポーネントに基づくアダプティブフォームを設定するには、次の手順を実行します。

1. [!DNL Experience Manager Forms] オーサーインスタンスにログインします。
1. アダプティブフォームを開いて編集し、アダプティブフォームコンテナプロパティの&#x200B;**[!UICONTROL データモデル]** セクションに移動し、フォームモデルを&#x200B;**コネクタ**&#x200B;として選択します。
1. ドロップダウンリストから「**[!UICONTROL コネクタ]**」を選択します。
1. **[!UICONTROL コネクタ]**&#x200B;を選択した後、クラウド設定を選択できます。

   ![Marketo コネクタを選択](/help/forms/assets/select-marketo-connector-af1.png){width=50%, height=50%}

   選択したMarketo Engage設定に基づいて、サイドバーの&#x200B;**[!UICONTROL コンテンツブラウザー]**&#x200B;の「**[!UICONTROL データモデルオブジェクト]**」タブにフォーム要素が表示されます。 これらの要素をドラッグ&amp;ドロップして、アダプティブフォームを作成できます。

   ![Marketo Data Source](/help/forms/assets/marketo-engage-data-source-af1.png){width=50%, height=50%}

1. 「**[!UICONTROL 完了]**」をクリックします。

または、アダプティブフォームのプロパティを編集して、関連する設定を変更することもできます。

アダプティブフォームは、接続されたMarketo Engage インスタンスのデータソースで設定されるようになりました。 次に、Adobe Marketo Engageにデータを送信するように設定します。

>[!TAB コアコンポーネント]

Marketo Engage データソースを使用して、コアコンポーネントに基づくアダプティブフォームを設定するには、次の手順を実行します。

1. [!DNL Experience Manager Forms] オーサーインスタンスにログインします。

1. アダプティブフォームを編集用に開きます。
1. コンテンツツリーを開き、「**[!UICONTROL ガイドコンテナ]**」を選択します。
1. アダプティブフォームコンテナのプロパティ（![アダプティブフォームコンテナのプロパティ](/help/forms/assets/configure-icon.svg) アイコン）をクリックします。 データソースを設定するためのアダプティブフォームコンテナダイアログボックスが開きます。
1. 「**[!UICONTROL データモデル]**」タブを開き、**コネクタ**&#x200B;としてフォームモデルを選択します。
1. ドロップダウンリストから「**[!UICONTROL コネクタ]**」を選択します。

1. **[!UICONTROL コネクタ]**&#x200B;を選択した後、クラウド設定を選択できます。

   ![Marketo コネクタを選択](/help/forms/assets/select-marketo-connector.png){width=50%, height=50%}

   選択したMarketo Engage設定に基づいて、サイドバーの&#x200B;**[!UICONTROL コンテンツブラウザー]**&#x200B;の「**[!UICONTROL データモデルオブジェクト]**」タブにフォーム要素が表示されます。 これらの要素をドラッグ&amp;ドロップして、アダプティブフォームを作成できます。

   ![Marketo Data Source](/help/forms/assets/marketo-engage-data-source.png){width=50%, height=50%}

1. 「**[!UICONTROL 完了]**」をクリックします。

または、アダプティブフォームのプロパティを編集して、関連する設定を変更することもできます。

アダプティブフォームは、接続されたMarketo Engage インスタンスのデータソースで設定されるようになりました。 次に、Adobe Marketo Engageにデータを送信するように設定します。

>[!TAB ユニバーサルエディター]

ユニバーサルエディターで作成されたアダプティブフォームをMarketo Engage データソースで設定するには、次の手順を実行します。

1. フォームのプロパティを開いて編集します。
1. **[!UICONTROL フォームモデル]**&#x200B;を選択します。
1. **[!UICONTROL フォームモデル]**&#x200B;から&#x200B;**コネクタ**&#x200B;を選択します。
1. **[!UICONTROL コネクタ]**&#x200B;を選択した後、クラウド設定を選択できます。

   ![Marketo コネクタを選択](/help/forms/assets/select-marketo-connector-ue.png)

1. 「**[!UICONTROL 保存して閉じる]**」をクリックします。

選択したMarketo Engage設定に基づいて、フォーム要素がプロパティパネルのコンテンツブラウザーの「**[!UICONTROL データソース]**」タブに表示されます。 これらの要素をドラッグ&amp;ドロップして、アダプティブフォームを作成できます。

![Marketo Data Source](/help/forms/assets/marketo-engage-data-source-ue.png)

これで、接続されたMarketo Engage インスタンスのデータソースを使用してフォームが設定されました。 次に、Adobe Marketo Engageにデータを送信するように設定します。

>[!ENDTABS]

## よくある質問（FAQ）

**Q: フォームのコネクタを変更するとどうなりますか？**\
**A:** フォームのコネクタを変更すると、既存のバインディングが無効になります。

**Q: Marketo Engageと統合されたフォームのルールエディターの呼び出しサービスで利用できる3つの操作は何ですか？**

**A:** Marketo Engageと統合されたフォームの&#x200B;**呼び出しサービス**&#x200B;で使用できる3つの標準操作は次のとおりです。

* リードを同期
* リードをIDで取得
* フィルタータイプでリードを取得

## 次の手順

これで、アダプティブForms用にMarketo Engage データソースを設定しました。 次に、[&#x200B; アダプティブフォームを設定して、データをMarketo Engage](/help/forms/submit-adaptive-form-to-marketo-engage.md)に送信できます。

## 関連記事

{{af-submit-action}}

## 関連トピック

{{marketo-engage-see-also}}
