---
title: アカウント環境の設定
description: AEM では、アカウントおよびオーサー環境の特定項目を設定できます
translation-type: tm+mt
source-git-commit: fee73b5f5ba69422494efe554ac5aa62c046ad86
workflow-type: tm+mt
source-wordcount: '488'
ht-degree: 100%

---


# アカウント環境の設定  {#configuring-your-account-environment}

AEM では、アカウントおよびオーサー環境の特定項目を設定できます。

[ヘッダー](/help/sites-cloud/authoring/getting-started/basic-handling.md#the-header)および関連する[環境設定](#my-preferences)ダイアログの「[ユーザー](#user-settings)」オプションを使用すると、ユーザーオプションを変更できます。

まず、ヘッダーの「[ユーザー](#user-settings)」オプションにアクセスします。

## ユーザー設定 {#user-settings}

**ユーザー**&#x200B;設定ダイアログでは、次の機能にアクセスできます。

* 次のユーザーとして操作
   * 「次のユーザーとして操作」機能を使用すると、ユーザーは別のユーザーに成り代わって作業をおこなうことができます。<!--With the [Impersonate as](/help/sites-administering/security.md#impersonating-another-user) functionality, a user can work on behalf of another user.-->
* プロファイル
   * ユーザー設定への便利なリンクを提供します。<!--Offers a convenient link to your [user settings](/help/sites-administering/security.md))-->
* [環境設定](#my-preferences)
   * ユーザー独自の様々な環境設定を指定します。

![ユーザー設定](/help/sites-cloud/authoring/assets/user-settings.png)

### 環境設定 {#my-preferences}

**環境設定**&#x200B;ダイアログには、ヘッダーの「[ユーザー](#user-settings)」オプションを使用してアクセスできます。

各ユーザーは、自分の特定のプロパティを設定できます。

![環境設定](/help/sites-cloud/authoring/assets/user-preferences.png)

* **言語**

   オーサリング環境の UI で使用する言語を定義します。使用できるリストから必要な言語を選択します。

* **ウィンドウ管理**

   ウィンドウの動作や開くウィンドウを定義します。次のいずれかを選択します。

   * **複数ウィンドウ**（デフォルト）

      * 新しいウィンドウでページが開きます。
   * **単一ウィンドウ**

      * 現在のウィンドウでページが開きます。


* **アセットのデスクトップアクションを表示**

   このオプションを使用するには、AEM デスクトップアプリケーションが必要です。

* **注釈カラー**

   注釈を作成する際のデフォルトのカラーを定義します。

   * カラーブロックをクリックすると、色を選択するためのスウォッチセレクターが表示されます。
   * または、フィールドに目的のカラーの 16 進コードを入力します。

* **相対的な日付の表示**

   読みやすくするために、AEM では、過去 7 日以内の日付を相対日付（例： 3 日前）で表示し、それ以前の日付を正確な日付（例：2017 年 3 月 20 日）で表示します。

   このオプションは、システムの日付の表示方法を定義します。以下のオプションが利用できます。

   * **常に正確な日付を表示**：常に正確な日付が表示されます（相対日付は表示されません）。
   * **1 日**：1 日以内の日付に相対日付が表示され、それ以外は正確な日付が表示されます。
   * **7 日（デフォルト）**：7 日以内の日付に相対日付が表示され、それ以外は正確な日付が表示されます。
   * **1 ヶ月**：1 ヶ月以内の日付に相対日付が表示され、それ以外は正確な日付が表示されます。
   * **1 年**：1 年以内の日付に相対日付が表示され、それ以外は正確な日付が表示されます。
   * **常に相対日付を表示**：正確な日付は表示されず、相対日付のみが表示されます。

* **ショートカットを有効にする**

   AEM には、オーサリングの効率性を高める多くのキーボードショートカットがあります。

   * [ページ編集時のキーボードショートカット](/help/sites-cloud/authoring/fundamentals/keyboard-shortcuts.md)
   * [コンソールのキーボードショートカット](/help/sites-cloud/authoring/getting-started/keyboard-shortcuts.md)

   このオプションは、キーボードショートカットを有効にします。デフォルトでは有効になっていますが、例えばユーザーに特定のアクセシビリティ要件がある場合に、無効にできます。

* **アセットのホームページを有効にする**

   このオプションは、システム管理者がアセットホームページの使用を組織全体で有効にしている場合にのみ使用できます。

* **Stock 設定**

   このオプションを使用すると、Adobe Stock の優先設定を指定できます。システム管理者が ](/help/assets/aem-assets-adobe-stock.md)Adobe Stock との連携[を有効にしている場合にのみ使用できます。
