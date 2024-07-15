---
title: アダプティブフォームをレビュー用に送信する方法？AEM アダプティブフォームのレビューを管理する方法？
description: レビューとは、レビュー担当者がタスクの割り当て手順を使用して、アダプティブフォームに対して様々なタスクを実行できるメカニズムです。
feature: Adaptive Forms
hide: true
hidefromtoc: true
source-git-commit: 2d4ffd5518d671a55e45a1ab6f1fc41ac021fd80
workflow-type: tm+mt
source-wordcount: '338'
ht-degree: 100%

---


# アダプティブフォームのレビューの作成と管理 {#review-step-forms-aem-sites-page}

AEM ワークフローの[割り当て手順](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/create-form-centric-workflows/aem-forms-workflow-step-reference.html?lang=ja#assign-task-step)を使用して、レビュー担当者は送信されたフォームをレビューし、それに対してアクションを実行します。タスクを割り当て手順を使用して送信されたフォームをレビューするには、次の手順に従います。

1. [AEM ワークフローを作成](#create-an-aem-workflow)
1. [アダプティブフォームコンテナの送信アクションを設定](#configure-submit-action)
1. [レビュー後のアダプティブフォームを送信](#submit-af-after-review)

## AEM ワークフローを作成 {#create-an-aem-workflow}

1. オーサーインスタンスを編集モードで開きます。
1. **[!UICONTROL ツール]**／**[!UICONTROL ワークフロー]**／**[!UICONTROL モデル]**／**[!UICONTROL 作成]**／**[!UICONTROL モデルを作成]**&#x200B;に移動します。
1. ワークフローのタイトルを指定し、**[タスクを割り当て]**&#x200B;手順を追加します。
1. アクションバーで ![settings_icon](assets/settings_icon.png) を選択します。**[!UICONTROL タスクを割り当て]**&#x200B;ダイアログが開きます。
1. 「[!UICONTROL フォームとドキュメント]」タブを開き、[!UICONTROL 事前入力]ドロップダウンを開いて、次を指定します。

   * 次を使用して入力データファイルを選択
   * 次を使用して入力添付ファイルを選択

   ![レビュー手順](/help/forms/assets/assigntask-review1.gif)

1. 「**[!UICONTROL 担当者]**」タブを開き、[!UICONTROL 事前入力]ドロップダウンを開いて、**[!UICONTROL 割り当てオプション]**&#x200B;を指定します。

   ![レビュー手順](/help/forms/assets/review-assignstep.png)

1. 「**[!UICONTROL 完了]**」をクリックして、変更を保存します。

## 送信アクションを設定 {#configure-submit-action}

次に、サイトのページでアダプティブフォームコンテナコンポーネントの送信アクションを設定します。

1. サイトのページに移動します。
1. アダプティブフォームコンテナの ![settings_icon](assets/settings_icon.png) を選択します。**[!UICONTROL アダプティブフォームコンテナ]**&#x200B;ダイアログが開きます。
1. 「**[!UICONTROL 送信]**」タブを開き、**[!UICONTROL 送信アクション]**&#x200B;から「[AEM ワークフローの呼び出し](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-foundation-components/configure-submit-actions-and-metadata-submission/configuring-submit-actions.html?lang=ja#invoke-an-aem-workflow)」を指定します

1. 「[完了]」をクリックして、設定を保存します。

![submissiontab-reviewstep](/help/forms/assets/submissiontab-reviewstep.gif)

## レビュー後のアダプティブフォームの送信 {#submit-af-after-review}

送信されたアダプティブフォームをレビューし確認するには、次の手順を実行します。

1. [!UICONTROL ツール]／[!UICONTROL ワークフロー]／[!UICONTROL インスタンス]に移動します
1. インボックスを見ると、インスタンスが作成されていることがわかります。
1. インスタンスを選択し、「[!UICONTROL 開く]」をクリックします。
1. これで、送信されたフォームを確認できます。

レビュー担当者は、次のように様々なアクションを実行します。

* **送信**：レビュー担当者は、フォームに入力し、さらなる処理のために送信します。
* **保存**：レビュー担当者は、フォームを送信せずに現在の状態で保存します。
* **リセット**：レビュー担当者は、フォームに加えられた変更をすべてクリアし、元の状態に戻します。
* **デリゲート**：レビュー担当者は、フォームの所有権を他のユーザーに転送して、さらなるアクションやレビューを実行します。
