---
title: アカウント環境の設定
description: Adobe Experience Manager（AEM）では、アカウントとオーサー環境の特定項目を設定できます。
exl-id: 1b948f0b-85b9-478a-8b7e-61495c1d57b6
source-git-commit: bbd845079cb688dc3e62e2cf6b1a63c49a92f6b4
workflow-type: ht
source-wordcount: '501'
ht-degree: 100%

---

# アカウント環境の設定 {#configuring-your-account-environment}

Adobe Experience Manager（AEM）では、アカウントとオーサー環境の特定項目を設定できます。

[ヘッダー](/help/sites-cloud/authoring/basic-handling.md#the-header)および関連する[環境設定](#my-preferences)ダイアログの「[ユーザー](#user-settings)」オプションを使用すると、ユーザーオプションを変更できます。

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

**環境設定**&#x200B;ダイアログボックスには、ヘッダーの「[ユーザー](#user-settings)」オプションを使用してアクセスします。

各ユーザーは、独自の優先プロパティを設定できます。

![環境設定](/help/sites-cloud/authoring/assets/user-preferences.png)

* **言語**

  これにより、オーサリング環境の UI で使用する言語が定義されます。使用できるリストから必要な言語を選択します。

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

   * カラーブロックをクリックすると、スウォッチセレクターが開き、色を選択できます。
   * または、フィールドに目的のカラーの 16 進コードを入力します。

* **相対的な日付の表示**

  読みやすくするために、AEM では、過去 7 日以内の日付を相対日付（例： 3 日前）で表示し、それ以前の日付を正確な日付（例：2017年3月20日）で表示します。

  このオプションは、システムの日付の表示方法を定義します。以下のオプションが利用できます。

   * **常に正確な日付を表示**：常に正確な日付が表示されます（相対日付は表示されません）。
   * **1 日**：1 日以内の日付に相対日付が表示され、それ以外は正確な日付が表示されます。
   * **7 日（デフォルト）**：7 日以内の日付に相対日付が表示され、それ以外は正確な日付が表示されます。
   * **1 ヶ月**：1 ヶ月以内の日付に相対日付が表示され、それ以外は正確な日付が表示されます。
   * **1 年**：1 年以内の日付に相対日付が表示され、それ以外は正確な日付が表示されます。
   * **常に相対日付を表示**：正確な日付は表示されず、相対日付のみが表示されます。

* **ショートカットを有効にする**

  AEM には、オーサリングをより効率的にする様々なキーボードショートカットがあります。

   * [ページ編集時のキーボードショートカット](/help/sites-cloud/authoring/page-editor/keyboard-shortcuts.md)
   * [コンソールのキーボードショートカット](/help/sites-cloud/authoring/sites-console/keyboard-shortcuts.md)

  このオプションは、キーボードショートカットを有効にします。デフォルトでは有効になっていますが、例えばユーザーに特定のアクセシビリティ要件がある場合は、無効にできます。

* **アセットのホームページを有効にする**

  このオプションは、システム管理者がアセットホームページのエクスペリエンスを組織全体で有効にしている場合にのみ使用できます。

* **Stock 設定**

  このオプションを使用すると、Adobe Stock の優先設定を指定できます。システム管理者が [Adobe Stock との連携](/help/assets/aem-assets-adobe-stock.md)を有効にしている場合にのみ使用できます。
