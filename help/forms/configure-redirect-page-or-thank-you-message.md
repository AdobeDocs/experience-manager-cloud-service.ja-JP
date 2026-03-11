---
title: リダイレクトページまたはお礼のメッセージの設定方法？
description: ユーザーにお礼のメッセージを表示したり、フォーム作成者がフォームの作成時に設定できる web ページにリダイレクトしたりする方法について説明します。
feature: Adaptive Forms, Core Components
role: User
level: Intermediate
badgeSaas: label="AEM Forms" type="Positive" tooltip="AEM Formsに適用）。"
exl-id: 27decf88-a2ab-4b52-b6ae-babb1d3abdaa
source-git-commit: 89b0f2a8ca9d2f60365a5c3962b0b4e826f79b3e
workflow-type: tm+mt
source-wordcount: '245'
ht-degree: 98%

---

# リダイレクトページの設定 {#configuring-redirect-page}

[コアコンポーネントベースのアダプティブフォーム](creating-adaptive-form-core-components.md)を送信すると、ユーザーを別の web ページにリダイレクトしたり、メッセージを表示したりできます。リダイレクトページまたはお礼のメッセージを設定するには、次の手順を実行します。

1. アダプティブフォームを編集用に開きます。
1. コンテンツツリーを開き、「**[!UICONTROL ガイドコンテナ]**」を選択します。
1. アダプティブフォームコンテナのプロパティ（![アダプティブフォームコンテナのプロパティ](/help/forms/assets/configure-icon.svg) アイコン）をクリックします。データモデルを設定するためのアダプティブフォームコンテナダイアログボックスが開きます。
1. 「**[!UICONTROL 送信]**」タブを開きます。リダイレクトページまたはメッセージを設定するためのオプションが表示されます。

   ![リダイレクトページまたはメッセージを設定するためのガイドコンテナの送信ダイアログ](/help/forms/assets/adaptive-forms-core-components-redirect-page-or-thank-you-message.png)

   * リダイレクト URL を設定するには、「送信」オプションで「**[!UICONTROL URL にリダイレクト]**」オプションを選択し、AEM Sites ページの絶対アドレス、リダイレクト URL、または相対パスを指定します。

   * カスタムメッセージまたはお礼のメッセージを設定するには、「**[!UICONTROL メッセージを表示]**」オプションを選択し、メッセージコンテンツボックスにメッセージを入力します。これはリッチテキストボックスで、全画面表示オプションを使用して、使用可能なすべてのリッチテキスト項目を表示できます。

フォーム作成者は、フォーム送信後にユーザーがリダイレクトされるページを各フォームに設定することができます。

**関連**

* [リダイレクトページの設定（基盤フォーム）](configuring-redirect-page.md)

>[!MORELIKETHIS]
>
>* [リダイレクトページの設定](/help/forms/configuring-redirect-page.md)

## 関連トピック {#see-also}

{{see-also}}