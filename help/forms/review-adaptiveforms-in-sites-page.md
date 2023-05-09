---
title: サイトページに埋め込まれた、または作成されたアダプティブFormsのレビューの作成と管理
seo-title: Review is a mechanism that allows reviewer to perform different tasks for adaptive forms using Assign Task step
description: レビューとは、レビュー担当者がタスクの割り当て手順を使用してアダプティブフォームに対して様々なタスクを実行できるメカニズムです
feature: Adaptive Forms
hide: true
hidefromtoc: true
source-git-commit: daeb407e27b9f1d390fe40151ca16ec0196712e6
workflow-type: tm+mt
source-wordcount: '355'
ht-degree: 6%

---


# Site のページでFormsの手順を確認する {#review-step-forms-aem-sites-page}

の使用 [ステップを割り当て](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/create-form-centric-workflows/aem-forms-workflow-step-reference.html#assign-task-step) レビュー担当者は、AEMワークフローの送信済みフォームをレビューし、それに対してアクションを実行します。 タスクの割り当て手順を使用して送信済みフォームをレビューするには、次の手順に従います。

1. [AEMワークフローの作成](#create-an-aem-workflow)
1. [アダプティブフォームコンテナの送信アクションを設定する](#configure-submit-action)
1. [レビュー後にアダプティブフォームを送信する](#submit-af-after-review)

## AEMワークフローの作成 {#create-an-aem-workflow}

1. オーサーインスタンスを編集モードで開きます。
1. に移動します。 **[!UICONTROL ツール]** >  **[!UICONTROL ワークフロー]** >  **[!UICONTROL モデル]** > **[!UICONTROL 作成]** > **[!UICONTROL モデルを作成]**
1. ワークフローのタイトルを指定し、 **[タスクを割り当て]** 手順
1. タップ ![settings_icon](assets/settings_icon.png) をクリックします。 この **[!UICONTROL タスクを割り当て]** ダイアログが開きます。
1. 開く [!UICONTROL フォームとドキュメント] タブと開く [!UICONTROL 事前入力済み] ドロップダウンして次を指定します。

   * 次を使用して入力データファイルを選択
   * 次を使用して入力添付ファイルを選択

   ![レビューステップ](/help/forms/assets/assigntask-review1.gif)

1. 開く **[!UICONTROL 担当者]** タブと開く [!UICONTROL 事前入力済み] ドロップダウンで **[!UICONTROL 割り当てオプション]**:

   ![レビューステップ](/help/forms/assets/review-assignstep.png)

1. 「**[!UICONTROL 完了]**」をクリックして、変更を保存します。

## 送信アクションの設定 {#configure-submit-action}

次に、サイトのページでアダプティブフォームコンテナコンポーネントの送信アクションを設定します。

1. サイトのページに移動します。
1. タップ ![settings_icon](assets/settings_icon.png) を作成します。 この **[!UICONTROL アダプティブフォームコンテナ]** ダイアログが開きます。
1. を開きます。 **[!UICONTROL 送信]** タブと指定 **[!UICONTROL 送信アクション]** から [AEMワークフローを起動](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-foundation-components/configure-submit-actions-and-metadata-submission/configuring-submit-actions.html?lang=en#invoke-an-aem-workflow)

1. 「[完了]」をクリックして、設定を保存します。

![submissiontab-reviewstep](/help/forms/assets/submissiontab-reviewstep.gif)

## レビュー後にアダプティブフォームを送信する {#submit-af-after-review}

送信されたアダプティブフォームを確認するには、次の手順を実行します。

1. に移動します。 [!UICONTROL ツール] >  [!UICONTROL ワークフロー] >  [!UICONTROL インスタンス]
1. インボックスに、インスタンスが作成中であることがわかります。
1. インスタンスを選択し、 [!UICONTROL 開く].
1. これで、送信されたフォームを確認できます。

レビュー担当者は、次のように様々なアクションを実行します。

* **送信**:レビュー担当者は、フォームに入力し、後で処理するために送信します。
* **保存**:レビュー担当者は、フォームを送信せずに現在の状態で保存します。
* **リセット**:レビュー担当者は、フォームに加えた変更をすべてクリアし、元の状態に戻します。
* **委任**:レビュー担当者は、フォームの所有権を他のユーザーに転送して、さらなるアクションやレビューを実行します。
