---
title: リダイレクトページまたは「ありがとうございます」メッセージの設定方法は？
description: ユーザーが「ありがとうございます」メッセージを表示したり、フォームの作成時にフォーム作成者が設定できる Web ページにリダイレクトしたりする方法を説明します。
feature: Adaptive Forms
role: User
level: Intermediate
source-git-commit: b104c7ddd102b3600384bf7472b166131e334c35
workflow-type: tm+mt
source-wordcount: '233'
ht-degree: 12%

---


# リダイレクトページの設定 {#configuring-redirect-page}

の送信時 [コアコンポーネントベースのアダプティブフォーム](creating-adaptive-form-core-components.md)を使用すると、ユーザーを別の web ページにリダイレクトしたり、メッセージを表示したりできます。 リダイレクトページまたは「ありがとうございます」メッセージを設定するには、次の手順を実行します。

1. アダプティブフォームを編集用に開きます。
1. コンテンツツリーを開き、「 **[!UICONTROL ガイドコンテナ]**.
1. アダプティブフォームコンテナのプロパティをクリックします。 ![アダプティブフォームコンテナのプロパティ](/help/forms/assets/configure-icon.svg) アイコン データモデルを設定するためのアダプティブフォームコンテナダイアログボックスが開きます。
1. を開きます。 **[!UICONTROL 送信]** タブをクリックします。 リダイレクトページまたはメッセージを設定するためのオプションが表示されます。

   ![リダイレクトページまたはメッセージを設定するための Guide Contaner の送信ダイアログ](/help/forms/assets/adaptive-forms-core-components-redirect-page-or-thank-you-message.png)

   * リダイレクト URL を設定するには、「送信時」オプションで、 **[!UICONTROL URL にリダイレクトオプション]**&#x200B;を指定し、AEM Sitesページの絶対アドレス、リダイレクト URL または相対パスを指定します。

   * カスタムまたは「ありがとうございます」メッセージを設定するには、 **[!UICONTROL メッセージを表示]** 」オプションを選択し、「メッセージコンテンツ」ボックスにメッセージを入力します。 これはリッチテキストボックスで、全画面表示オプションを使用して、使用可能なすべてのリッチテキスト項目を表示できます。

フォーム作成者は、フォーム送信後にユーザーがリダイレクトされるページを各フォームに設定することができます。

**関連**

* [リダイレクトページの設定 (Foundation Forms)](configuring-redirect-page.md)
