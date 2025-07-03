---
title: フォルダー内およびコレクション内のアセットの確認
description: フォルダー内またはコレクション内のアセットに対してレビューワークフローを設定し、それをレビュー担当者またはクリエイティブパートナーと共有してフィードバックを得ることができます。
contentOwner: AG
feature: Collections, Collaboration
role: User
exl-id: 1e5bdd66-2707-4584-87ed-a0ff1bde3718
source-git-commit: 32fdbf9b4151c949b307d8bd587ade163682b2e5
workflow-type: ht
source-wordcount: '820'
ht-degree: 100%

---

# フォルダー内およびコレクション内のアセットの確認 {#review-folder-assets-and-collections}

| バージョン | 記事リンク |
| -------- | ---------------------------- |
| AEM 6.5 | [ここをクリックしてください](https://experienceleague.adobe.com/docs/experience-manager-65/assets/using/bulk-approval.html?lang=ja) |
| AEM as a Cloud Service | この記事 |

Adobe Experience Manager Assets では、フォルダー内またはコレクション内のアセットに対してアドホックレビューワークフローを設定できます。それをレビュー担当者やクリエイティブパートナーと共有して、フィードバックを得ることができます。レビューワークフローをプロジェクトと関連付けることも、独立したレビュータスクを作成することもできます。

ユーザーがアセットを共有した後で、レビュー担当者がアセットを承認または拒否できます。ワークフローの様々なステージで、様々なタスクの完了に関する通知が対象の受信者に送信されます。例えば、ユーザーがフォルダーまたはコレクションを共有すると、レビュー担当者は、フォルダーまたはコレクションがレビューのために共有されたという通知を受け取ります。

レビュー担当者がレビューを終了（アセットを承認または拒否）すると、ユーザーはレビューが完了したという通知を受け取ります。

## フォルダー用レビュータスクの作成 {#creating-a-review-task-for-folders}

1. Assets ユーザーインターフェイスで、レビュータスクを作成するフォルダーを選択します。
1. ツールバーで「**[!UICONTROL レビュータスクを作成]**」アイコンを選択して、**[!UICONTROL レビュータスク]**&#x200B;ページを開きます。ツールバーにこのアイコンが表示されていない場合は、「**[!UICONTROL その他]**」を選択してアイコンを選択します。

   ![chlimage_1-403](assets/chlimage_1-403.png)

1. （オプション）**[!UICONTROL プロジェクト]**&#x200B;リストから、レビュータスクを関連付けるプロジェクトを選択します。デフォルトでは、「**[!UICONTROL なし]**」オプションが選択されています。レビュータスクにプロジェクトを関連付けない場合は、この選択を保持します。

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

1. 「**[!UICONTROL 送信]**」、「**[!UICONTROL 完了]**」の順に選択して確認メッセージを閉じます。新しいタスクに関する通知が承認者に送信されます。
1. [!DNL Experience Manager Assets] に承認者としてログインし、Assets UI に移動します。アセットを承認するには、「**[!UICONTROL 通知]**」アイコンを選択し、リストからレビュータスクを選択します。

   ![通知](assets/notification.png)

1. **[!UICONTROL レビュータスク]**&#x200B;ページでレビュータスクの詳細を確認し、「**[!UICONTROL レビュー]**」を選択します。
1. **[!UICONTROL レビュータスク]**&#x200B;ページでアセットを選択し、必要に応じて&#x200B;**[!UICONTROL 「承認」または「非承認」]**&#x200B;アイコンを選択して、承認するか非承認にします。

   ![review_task](assets/review_task.png)

1. ツールバーの「**[!UICONTROL 完了]**」アイコンを選択します。ダイアログでコメントを入力し、「**[!UICONTROL 完了]**」を選択して確定します。
1. Assets UI に移動し、フォルダーを開きます。アセットの承認ステータスアイコンは、カード表示とリスト表示の両方に表示されます。

   **カード表示**

   ![chlimage_1-404](assets/chlimage_1-404.png)

   **リスト表示**

   ![review_status_listview](assets/review_status_listview.png)

## コレクション用レビュータスクの作成 {#creating-a-review-task-for-collections}

1. コレクションページで、レビュータスクを作成するコレクションを選択します。
1. ツールバーで「**[!UICONTROL レビュータスクを作成]**」アイコンを選択して、**[!UICONTROL レビュータスク]**&#x200B;ページを開きます。ツールバーにこのアイコンが表示されていない場合は、「**[!UICONTROL その他]**」を選択してアイコンを選択します。

   ![chlimage_1-405](assets/chlimage_1-405.png)

1. （オプション）**[!UICONTROL プロジェクト]**&#x200B;リストから、レビュータスクを関連付けるプロジェクトを選択します。デフォルトでは、「**[!UICONTROL なし]**」オプションが選択されています。レビュータスクにプロジェクトを関連付けない場合は、この選択を保持します。

   >[!NOTE]
   >
   >エディターレベルの権限（またはそれ以上）のあるプロジェクトのみが「**[!UICONTROL プロジェクト]**」リストに表示されます。

1. レビュータスクの名前を入力し、「**[!UICONTROL 割り当て先]**」リストから承認者を選択します。

   >[!NOTE]
   >
   >選択されたプロジェクトのメンバーまたはグループが、承認者として「**[!UICONTROL 割り当て先]**」リストに表示されます。

1. レビュータスクの説明、タスクの優先順位および期限を入力します。

   ![task_details-collection](assets/task_details-collection.png)

1. 「**[!UICONTROL 送信]**」の次に「**[!UICONTROL 完了]**」をクリックして確認メッセージを閉じます。新しいタスクに関する通知が承認者に送信されます。
1. [!DNL Experience Manager Assets] に承認者としてログインし、Assets コンソールに移動します。アセットを承認するには、**[!UICONTROL 通知]**&#x200B;アイコンを選択し、リストからレビュータスクを選択します。
1. 「**[!UICONTROL タスクのレビュー]**」ページでレビュータスクの詳細を確認し、「**[!UICONTROL レビュー]**」をクリックします。
1. コレクションのすべてのアセットがレビューページに表示されます。アセットを選択し、必要に応じて&#x200B;**[!UICONTROL 承認／拒否]**&#x200B;のアイコンを選択して、アセットを承認するか拒否します。

   ![review_task_collection](assets/review_task_collection.png)

1. ツールバーの「**[!UICONTROL 完了]**」アイコンを選択します。ダイアログでコメントを入力し、「**[!UICONTROL 完了]**」をクリックして確定します。
1. コレクションコンソールに移動して、コレクションを開きます。アセットの承認ステータスアイコンは、カード表示とリスト表示の両方に表示されます。

   **カード表示**

   ![collection_reviewstatuscardview](assets/collection_reviewstatuscardview.png)

   **リスト表示**

   ![collection_reviewstatuslistview](assets/collection_reviewstatuslistview.png)

**関連情報**

* [アセットを翻訳](translate-assets.md)
* [Assets HTTP API](mac-api-assets.md)
* [AEM Assets as a Cloud Service でサポートされているファイル形式](file-format-support.md)
* [アセットを検索](search-assets.md)
* [接続されたアセット](use-assets-across-connected-assets-instances.md)
* [アセットレポート](asset-reports.md)
* [メタデータスキーマ](metadata-schemas.md)
* [アセットをダウンロード](download-assets-from-aem.md)
* [メタデータを管理](manage-metadata.md)
* [検索ファセット](search-facets.md)
* [コレクションを管理](manage-collections.md)
* [メタデータの一括読み込み](metadata-import-export.md)
* [AEM および Dynamic Media へのアセットの公開](/help/assets/publish-assets-to-aem-and-dm.md)
