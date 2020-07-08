---
title: 非同期ジョブ
description: Adobe Experience Managerは、リソースを大量に消費する一部のタスクを非同期に完了して、パフォーマンスを最適化します。
translation-type: tm+mt
source-git-commit: be817ff8265d9d45a80557c0e44949ba6562993c
workflow-type: tm+mt
source-wordcount: '882'
ht-degree: 26%

---


# 非同期操作 {#asynchronous-operations}

Adobe Experience Mangerでは、パフォーマンスに悪影響を与えないように、長時間かつリソースを大量に消費する特定の操作を非同期に処理します。 非同期処理では、複数のジョブをエンキューし、システムリソースの可用性に左右されないように連続して実行します。

このような操作には以下のようなものがあります。

* 多数のアセットの削除
* 多数のアセットまたは多数の参照があるアセットの移動
* アセットメタデータの一括書き出し/読み込み
* リモートExperience Managerのデプロイメントから、設定したしきい値制限を超えるアセットを取得しています
* ページの移動
* ライブコピーのロールアウト

非同期ジョブの状態は、 **[!UICONTROL Async Job]** ダッシュボード **グローバルナビゲーション** -> Tools **> Operations** Operations Jobs> Jobsステータスで表示できます。非同期ジョブの状態は、Async Job **Navigation -> Global Navigation** -> Tools > Operations **** Jobsステータスでできます。

>[!NOTE]
>
>デフォルトでは、非同期ジョブは並行して実行されます。 If *`n`* is the number of CPU cores, *`n/2`* jobs can run in parallel, by default. ジョブキューのカスタム設定を使用するには、Webコンソールから **[!UICONTROL Async Operation Default Queue Config]** と **Async Operation Page Move and Rollout Config** を変更します。
>
>For more information, see [queue configurations](https://sling.apache.org/documentation/bundles/apache-sling-eventing-and-job-handling.html#queue-configurations).

## Monitor the Status of Asynchronous Operations {#monitor-the-status-of-asynchronous-operations}

AEMが操作を非同期で処理する場合は常に、イン [ボックス](/help/sites-cloud/authoring/getting-started/inbox.md) と電子メール（有効になっている場合）で通知が受信されます。

非同期操作のステータスの詳細を表示するには、**[!UICONTROL 非同期ジョブステータス]**&#x200B;ページに移動します。

1. Experience Managerインターフェイスで、 **[!UICONTROL 操作]** / **[!UICONTROL ジョブ]**&#x200B;をクリックします。

1. **[!UICONTROL 非同期ジョブステータス]**&#x200B;ページで、操作の詳細をレビューします。

   ![非同期操作のステータスと詳細](assets/async-operation-status.png)

   To determine the progress of a particular operation, see the value in the **[!UICONTROL Status]** column. 進行状況に応じて、以下のいずれかのステータスが表示されます。

   * **[!UICONTROL アクティブ]**：操作は処理中です。

   * **[!UICONTROL 成功]**：操作は完了しました。

   * **[!UICONTROL 失敗]**&#x200B;または&#x200B;**[!UICONTROL エラー]**：操作を処理できませんでした。

   * **[!UICONTROL スケジュール済み]**：操作は後で処理するためにスケジュールされています。

1. To stop an active operation, select it from the list and click **[!UICONTROL Stop]** from the toolbar.

   ![stop_icon](assets/async-stop-icon.png)

1. To view extra details, for example description and logs, select the operation and click **[!UICONTROL Open]** from the toolbar.

   ![open_icon](assets/async-open-icon.png)

   ジョブの詳細ページが表示されます。

   ![job_details](assets/async-job-details.png)

1. リストから操作を削除するには、ツールバーの「**[!UICONTROL 削除]**」を選択します。To download the details in a CSV file, click **[!UICONTROL Download]**.

   >[!NOTE]
   >
   >You cannot delete a job if its status is either **Active** or **Queued**.

## 完了したジョブの削除 {#purging-completed-jobs}

AEMは毎日01:00に削除ジョブを実行し、1日以上経過している完了済みの非同期ジョブを削除します。

パージジョブのスケジュールと、完了済みジョブの詳細を削除するまでの保持期間を変更できます。また、任意の時点での詳細を保持する、完了済みジョブの最大数を設定することもできます。

1. グローバルナビゲーションで、 **[!UICONTROL ツール]** / **[!UICONTROL 操作]** / **[!UICONTROL Webコンソールをクリックします]**。
1. Adobe Granite Async Jobs Purge Scheduled Job **** ジョブを開きます。
1. 以下を指定します。
   * 完了したジョブが削除されてからの日数のしきい値。
   * 詳細が履歴に保持されるジョブの最大数。
   * 削除を実行するタイミングのcron式。
   ![非同期ジョブのパージをスケジュールするための設定](assets/async-purge-job.png)

1. 変更内容を保存します。

## 非同期処理の設定 {#configuring-asynchronous-processing}

特定の操作を非同期に処理するためのAEMのアセット、ページまたは参照のしきい値を設定したり、ジョブの処理時に関する電子メール通知を切り替えたりできます。

### 非同期アセット削除操作の設定 {#configuring-synchronous-delete-operations}

削除するアセットまたはフォルダーの数がしきい値を超える場合は、非同期に削除操作が実行されます。

1. グローバルナビゲーションで、 **[!UICONTROL ツール]** / **[!UICONTROL 操作]** / **[!UICONTROL Webコンソールをクリックします]**。
1. Webコンソールから、「 **[!UICONTROL Async Process Default Queue Configuration」を開きます。]**
1. 「**[!UICONTROL Threshold number of assets]**」ボックスで、削除操作の非同期処理に関するアセットまたはフォルダー数のしきい値を指定します。

   ![アセット削除しきい値](assets/async-delete-threshold.png)

1. 「電子メール通知を **有効にする** 」オプションを選択すると、このジョブステータスに関する電子メール通知を受信できます。 例：成功、失敗
1. 変更内容を保存します。

### 非同期アセット移動操作の設定 {#configuring-asynchronous-move-operations}

移動するアセット/フォルダーまたは参照の数がしきい値を超える場合は、非同期に移動操作が実行されます。

1. グローバルナビゲーションで、 **[!UICONTROL ツール]** / **[!UICONTROL 操作]** / **[!UICONTROL Webコンソールをクリックします]**。
1. From the web console, open the **[!UICONTROL Async Move Operation Job Processing Configuration.]**
1. 「**[!UICONTROL Threshold number of assets/references]**」ボックスで、移動操作の非同期処理に関するアセットやフォルダーまたは参照の数のしきい値を指定します。

   ![アセット移動しきい値](assets/async-move-threshold.png)

1. 「電子メール通知を **有効にする** 」オプションを選択すると、このジョブステータスに関する電子メール通知を受信できます。 例：成功、失敗
1. 変更内容を保存します。

### 非同期ページ移動操作の設定 {#configuring-asynchronous-page-move-operations}

移動するページへの参照数がしきい値を超えると、移動操作は非同期に実行される。

1. グローバルナビゲーションで、 **[!UICONTROL ツール]** / **[!UICONTROL 操作]** / **[!UICONTROL Webコンソールをクリックします]**。
1. From the web console, open the **[!UICONTROL Async Page Move Operation Job Processing Configuration.]**
1. In the **[!UICONTROL Threshold number of references]** field, specify the threshold number of references for asynchronous processing of page move operations.

   ![ページ移動しきい値](assets/async-page-move.png)

1. 「電子メール通知を **有効にする** 」オプションを選択すると、このジョブステータスに関する電子メール通知を受信できます。 例：成功、失敗
1. 変更内容を保存します。

### 非同期MSM操作の設定 {#configuring-asynchronous-msm-operations}

1. グローバルナビゲーションで、 **[!UICONTROL ツール]** / **[!UICONTROL 操作]** / **[!UICONTROL Webコンソールをクリックします]**。
1. From the web console, open the **[!UICONTROL Async Page Move Operation Job Processing Configuration.]**
1. 「電子メール通知を **有効にする** 」オプションを選択すると、このジョブステータスに関する電子メール通知を受信できます。 例：成功、失敗

   ![MSM設定](assets/async-msm.png)

1. 変更内容を保存します。

>[!MORELIKETHIS]
>
>* [ページの作成と整理](/help/sites-cloud/authoring/fundamentals/organizing-pages.md)
>* [アセットメタデータの一括読み込みおよび書き出し](/help/assets/metadata-import-export.md).
>* [「接続されたアセット」を使用して、リモートデプロイメントからDAMアセットを共有します](/help/assets/use-assets-across-connected-assets-instances.md)。

