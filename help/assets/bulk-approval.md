---
title: フォルダー内およびコレクション内のアセットの確認
description: フォルダー内またはコレクション内のアセットに対してレビューワークフローを設定し、それをレビュー担当者またはクリエイティブパートナーと共有してフィードバックを得ることができます。
contentOwner: AG
feature: Collections,Collaboration
role: User
exl-id: 1e5bdd66-2707-4584-87ed-a0ff1bde3718
source-git-commit: 8bdd89f0be5fe7c9d4f6ba891d7d108286f823bb
workflow-type: tm+mt
source-wordcount: '823'
ht-degree: 87%

---

# フォルダー内およびコレクション内のアセットの確認 {#review-folder-assets-and-collections}

Adobe Experience Manager Assets では、フォルダー内またはコレクション内のアセットに対してアドホックレビューワークフローを設定できます。それをレビュー担当者やクリエイティブパートナーと共有して、フィードバックを得ることができます。レビューワークフローをプロジェクトと関連付けることも、独立したレビュータスクを作成することもできます。

ユーザーがアセットを共有した後で、レビュー担当者がアセットを承認または拒否できます。ワークフローの様々な段階で通知が送信され、様々なタスクの完了に関して意図した受信者に通知が送信されます。 例えば、あるフォルダーまたはコレクションを共有した場合、レビュー担当者に、あるフォルダーまたはコレクションがレビュー用に共有されたことを知らせる通知が届きます。

レビュー担当者がレビューを終了（アセットを承認または拒否）すると、ユーザーはレビューが完了したという通知を受け取ります。

## フォルダーのレビュータスクの作成 {#creating-a-review-task-for-folders}

1. Assets ユーザーインターフェイスで、レビュータスクを作成するフォルダーを選択します。
1. ツールバーで「**[!UICONTROL レビュータスクを作成]**」アイコンをタップまたはクリックして、**[!UICONTROL レビュータスク]**&#x200B;ページを開きます。ツールバーにこのアイコンが表示されていない場合は、「**[!UICONTROL その他]**」をタップまたはクリックしてアイコンを選択します。

   ![chlimage_1-403](assets/chlimage_1-403.png)

1. （オプション）「**[!UICONTROL プロジェクト]**」リストから、レビュータスクを関連付けるプロジェクトを選択します。デフォルトでは、「**[!UICONTROL なし]**」オプションが選択されています。レビュータスクにプロジェクトを関連付けない場合は、この選択状態のままにします。

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

1. 「**[!UICONTROL 送信]**」、「**[!UICONTROL 完了]**」の順にタップまたはクリックし、確認メッセージを閉じます。新しいタスクに関する通知が承認者に送信されます。
1. [!DNL Experience Manager Assets] に承認者としてログインし、Assets UI に移動します。アセットを承認するには、**[!UICONTROL 通知]**&#x200B;アイコンをクリックまたはタップし、リストからレビュータスクを選択します。

   ![通知](assets/notification.png)

1. **[!UICONTROL レビュータスク]**&#x200B;ページでレビュータスクの詳細を確認し、「**[!UICONTROL レビュー]**」をタップまたはクリックします。
1. **[!UICONTROL レビュータスク]**&#x200B;ページでアセットを選択し、必要に応じて&#x200B;**[!UICONTROL 「承認」または「非承認」]**&#x200B;アイコンをタップまたはクリックして、承認するか拒否します。

   ![review_task](assets/review_task.png)

1. ツールバーの「**[!UICONTROL 完了]**」アイコンをタップまたはクリックします。ダイアログでコメントを入力し、「**[!UICONTROL 完了]**」をタップまたはクリックして確認します。
1. Assets UI に移動し、フォルダーを開きます。 アセットの承認ステータスアイコンは、カード表示とリスト表示の両方に表示されます。

   **カード表示**

   ![chlimage_1-404](assets/chlimage_1-404.png)

   **リスト表示**

   ![review_status_listview](assets/review_status_listview.png)

## コレクション用レビュータスクの作成 {#creating-a-review-task-for-collections}

1. コレクションページで、レビュータスクを作成するコレクションを選択します。
1. ツールバーで「**[!UICONTROL レビュータスクを作成]**」アイコンをタップまたはクリックして、**[!UICONTROL レビュータスク]**&#x200B;ページを開きます。ツールバーにこのアイコンが表示されていない場合は、「**[!UICONTROL その他]**」をタップまたはクリックしてアイコンを選択します。

   ![chlimage_1-405](assets/chlimage_1-405.png)

1. （オプション）「**[!UICONTROL プロジェクト]**」リストから、レビュータスクを関連付けるプロジェクトを選択します。デフォルトでは、「**[!UICONTROL なし]**」オプションが選択されています。レビュータスクにプロジェクトを関連付けない場合は、この選択状態のままにします。

   >[!NOTE]
   >
   >エディターレベルの権限（またはそれ以上）のあるプロジェクトのみが「**[!UICONTROL プロジェクト]**」リストに表示されます。

1. レビュータスクの名前を入力し、「**[!UICONTROL 割り当て先]**」リストから承認者を選択します。

   >[!NOTE]
   >
   >選択されたプロジェクトのメンバーまたはグループが、承認者として「**[!UICONTROL 割り当て先]**」リストに表示されます。

1. レビュータスクの説明、タスクの優先順位および期限を入力します。

   ![task_details-collection](assets/task_details-collection.png)

1. 「**[!UICONTROL 送信]**」、「**[!UICONTROL 完了]**」の順にタップまたはクリックし、確認メッセージを閉じます。新しいタスクに関する通知が承認者に送信されます。
1. [!DNL Experience Manager Assets] に承認者としてログインし、Assets コンソールに移動します。アセットを承認するには、**[!UICONTROL 通知]**&#x200B;アイコンをタップまたはクリックし、リストからレビュータスクを選択します。
1. **[!UICONTROL レビュータスク]**&#x200B;ページでレビュータスクの詳細を確認し、「**[!UICONTROL レビュー]**」をタップまたはクリックします。
1. コレクションのすべてのアセットがレビューページに表示されます。アセットを選択し、必要に応じて&#x200B;**[!UICONTROL 「承認」または「非承認」]**&#x200B;アイコンをタップまたはクリックして、アセットを承認するか拒否します。

   ![review_task_collection](assets/review_task_collection.png)

1. ツールバーの「**[!UICONTROL 完了]**」アイコンをタップまたはクリックします。ダイアログでコメントを入力し、「**[!UICONTROL 完了]**」をタップまたはクリックして確認します。
1. コレクションコンソールに移動して、コレクションを開きます。 アセットの承認ステータスアイコンは、カード表示とリスト表示の両方に表示されます。

   **カード表示**

   ![collection_reviewstatuscardview](assets/collection_reviewstatuscardview.png)

   **リスト表示**

   ![collection_reviewstatuslistview](assets/collection_reviewstatuslistview.png)

**関連情報**

* [アセットを翻訳](translate-assets.md)
* [Assets HTTP API](mac-api-assets.md)
* [AEM Assets as a Cloud Service でサポートされているファイル形式](file-format-support.md)
* [アセットの検索](search-assets.md)
* [Connected Assets](use-assets-across-connected-assets-instances.md)
* [アセットレポート](asset-reports.md)
* [メタデータスキーマ](metadata-schemas.md)
* [アセットのダウンロード](download-assets-from-aem.md)
* [メタデータの管理](manage-metadata.md)
* [検索ファセット](search-facets.md)
* [コレクションの管理](manage-collections.md)
* [一括メタデータ読み込み](metadata-import-export.md)
