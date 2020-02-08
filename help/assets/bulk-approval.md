---
title: フォルダーとコレクション内のアセットの確認
description: フォルダーまたはコレクション内のアセットに対してレビューワークフローを設定し、それをレビュー担当者またはクリエイティブパートナーと共有してフィードバックを得ることができます。
contentOwner: AG
translation-type: tm+mt
source-git-commit: 991d4900862c92684ed92c1afc081f3e2d76c7ff

---


# フォルダーとコレクション内のアセットの確認 {#review-folder-assets-and-collections}

Adobe Experience Manager (AEM) Assetsを使用して、フォルダーまたはコレクション内のアセットに対してアドホックレビューワークフローを設定できます。 レビュー担当者やクリエイティブパートナーと共有して、フィードバックを求めることができます。 レビューワークフローをプロジェクトに関連付けるか、独立したレビュータスクを作成できます。

ユーザーがアセットを共有した後で、レビュー担当者がアセットを承認または拒否できます。ワークフローの様々なステージで、様々なタスクの完了に関する通知が対象の受信者に送られます。例えば、ユーザーがフォルダーまたはコレクションを共有すると、レビュー担当者は、フォルダーまたはコレクションがレビューのために共有されたという通知を受け取ります。

レビュー担当者がレビューを終了（アセットを承認または拒否）すると、ユーザーはレビューが完了したという通知を受け取ります。

## フォルダー用レビュータスクの作成 {#creating-a-review-task-for-folders}

1. Assets ユーザーインターフェイスで、レビュータスクを作成するフォルダーを選択します。
1. From the toolbar, tap/click the **[!UICONTROL Create Review Task]** icon to open the **[!UICONTROL Review Task]** page. ツールバーにこのアイコンが表示されていない場合は、「**[!UICONTROL その他]**」をタップまたはクリックしてアイコンを選択します。

   ![chlimage_1-403](assets/chlimage_1-403.png)

1. (Optional) From the **[!UICONTROL Project]** list, select the project to which you want to associate the review task. By default, the **[!UICONTROL None]** option is selected. If you do not want to associate any project with the review task, retain this selection.

   >[!NOTE]
   >
   >エディターレベルの権限（またはそれ以上）のあるプロジェクトのみが「**[!UICONTROL プロジェクト]**」リストに表示されます。

1. レビュータスクの名前を入力し、「**[!UICONTROL 割り当て先]**」リストから承認者を選択します。

   >[!NOTE]
   >
   >選択されたプロジェクトのメンバーまたはグループが、承認者として「**[!UICONTROL 割り当て先]**」リストに表示されます。

1. レビュータスクの説明、タスクの優先順位および期限を入力します。

   ![task_details](assets/task_details.png)

1. 「詳細」タブで、URI の作成に使用されるラベルを入力します。

   ![review_name](assets/review_name.png)

1. Tap/click **[!UICONTROL Submit]**, and then tap/click **[!UICONTROL Done]** to close the confirmation message. 新しいタスクに関する通知が承認者に送信されます。
1. 承認者として AEM Assets にログインし、Assets UI に移動します。アセットを承認するには、**[!UICONTROL 通知]**&#x200B;アイコンをクリックまたはタップし、リストからレビュータスクを選択します。

   ![通知](assets/notification.png)

1. In the **[!UICONTROL Review Task]** page, examine the details of the review task, and then tap/click **[!UICONTROL Review]**.
1. **[!UICONTROL レビュータスク]**&#x200B;ページでアセットを選択し、必要に応じて「**[!UICONTROL 承認」または「非承認]**」アイコンをタップまたはクリックして、承認するか非承認にします。

   ![review_task](assets/review_task.png)

1. ツールバーの「**[!UICONTROL 完了]**」アイコンをタップまたはクリックします。In the dialog, enter a comment and tap/click  **[!UICONTROL Complete]** to confirm.
1. Assets UI に移動し、フォルダーを開きます。アセットの承認ステータスアイコンは、カード表示とリスト表示の両方に表示されます。

   **カード表示**

   ![chlimage_1-404](assets/chlimage_1-404.png)

   **リスト表示**

   ![review_status_listview](assets/review_status_listview.png)

## コレクション用レビュータスクの作成 {#creating-a-review-task-for-collections}

1. コレクションページで、レビュータスクを作成するコレクションを選択します。
1. From the toolbar, tap/click the **[!UICONTROL Create Review Task]** icon to open the **[!UICONTROL Review Task]** page. ツールバーにこのアイコンが表示されていない場合は、「**[!UICONTROL その他]**」をタップまたはクリックしてアイコンを選択します。

   ![chlimage_1-405](assets/chlimage_1-405.png)

1. (Optional) From the **[!UICONTROL Project]** list, select the project to which you want to associate the review task. By default, the **[!UICONTROL None]** option is selected. If you do not want to associate any project with the review task, retain this selection.

   >[!NOTE]
   >
   >エディターレベルの権限（またはそれ以上）のあるプロジェクトのみが「**[!UICONTROL プロジェクト]**」リストに表示されます。

1. レビュータスクの名前を入力し、「**[!UICONTROL 割り当て先]**」リストから承認者を選択します。

   >[!NOTE]
   >
   >選択されたプロジェクトのメンバーまたはグループが、承認者として「**[!UICONTROL 割り当て先]**」リストに表示されます。

1. レビュータスクの説明、タスクの優先順位および期限を入力します。

   ![task_details-collection](assets/task_details-collection.png)

1. Tap/click **[!UICONTROL Submit]**, and then tap/click **[!UICONTROL Done]** to close the confirmation message. 新しいタスクに関する通知が承認者に送信されます。
1. 承認者として AEM Assets にログインし、アセットコンソールに移動します。To approve assets, tap/click the **[!UICONTROL Notifications]** icon and then select the review task from the list.
1. In the **[!UICONTROL Review Task]** page, examine the details of the review task, and then tap/click **[!UICONTROL Review]**.
1. コレクションのすべてのアセットがレビューページに表示されます。Select the assets and tap/click the **[!UICONTROL Approve/Reject]** icon to approve or reject assets, as appropriate.

   ![review_task_collection](assets/review_task_collection.png)

1. ツールバーの「**[!UICONTROL 完了]**」アイコンをタップまたはクリックします。In the dialog, enter a comment and tap/click **[!UICONTROL Complete]** to confirm.
1. コレクションコンソールに移動して、コレクションを開きます。アセットの承認ステータスアイコンは、カード表示とリスト表示の両方に表示されます。

   **カード表示**

   ![collection_reviewstatuscardview](assets/collection_reviewstatuscardview.png)

   **リスト表示**

   ![collection_reviewstatuslistview](assets/collection_reviewstatuslistview.png)

