---
title: 非同期操作
description: AEM Assets では、リソースを集中的に消費する一部のタスクを非同期的に処理することでパフォーマンスを最適化します。
contentOwner: AG
translation-type: tm+mt
source-git-commit: 26833f59f21efa4de33969b7ae2e782fe5db8a14

---


# 非同期操作 {#asynchronous-operations}

Adobe Experience Manager (AEM) Assets では、パフォーマンスを悪化させないために、長時間実行され、リソースを集中的に消費する特定のアセット操作は、非同期的に処理されます。

このような操作には以下のようなものがあります。

* 多数のアセットの削除
* 多数のアセットまたは多数の参照があるアセットの移動
* アセットメタデータの一括での書き出しまたは読み込み
* しきい値制限セットを超えるアセットのリモート AEM デプロイメントからの取得

非同期処理では複数のジョブがエンキューされ、システムリソースの可用性に応じた順序でジョブが実行されます。

非同期ジョブのステータスは、**[!UICONTROL 非同期ジョブステータス]**&#x200B;ページで確認できます。

>[!NOTE]
>
>デフォルトでは、AEM Assets でのジョブは並行して実行されます。N を CPU コアの数とすると、デフォルトでは N/2 のジョブを並行して実行できます。ジョブキューのカスタム設定を使用するには、Web コンソールで「**Async Operation Default Queue**」設定を変更します。詳しくは、[キューの設定](https://sling.apache.org/documentation/bundles/apache-sling-eventing-and-job-handling.html#queue-configurations)を参照してください。

## 非同期操作のステータスの監視 {#monitoring-the-status-of-asynchronous-operations}

Whenever AEM Assets processes an operation asynchronously, you receive a notification at your inbox <!-- and through email -->.

非同期操作のステータスの詳細を表示するには、**[!UICONTROL 非同期ジョブステータス]**&#x200B;ページに移動します。

1. AEM のロゴをタップまたはクリックし、**[!UICONTROL アセット]**／**[!UICONTROL ジョブ]**&#x200B;に移動します。
1. **[!UICONTROL 非同期ジョブステータス]**&#x200B;ページで、操作の詳細をレビューします。

   ![job_status](assets/job_status.png)

   特定の操作の進行状況を確認するには、「**[!UICONTROL ステータス]**」列の値を参照します。進行状況に応じて、以下のいずれかのステータスが表示されます。

   **[!UICONTROL アクティブ]**：操作は処理中です。

   **[!UICONTROL 成功]**：操作は完了しました。

   **[!UICONTROL 失敗]**&#x200B;または&#x200B;**[!UICONTROL エラー]**：操作を処理できませんでした。

   **[!UICONTROL スケジュール済み]**：操作は後で処理するためにスケジュールされています。

1. アクティブな操作を停止するには、リストから対象の操作を選択し、ツールバーの「**[!UICONTROL 停止]**」アイコンをタップまたはクリックします。

   ![stop_icon](assets/stop_icon.png)

1. 説明やログなど、その他の詳細を表示するには、操作を選択し、ツールバーの「**[!UICONTROL 開く]**」アイコンをタップまたはクリックします。

   ![open_icon](assets/open_icon.png)

   ジョブの詳細ページが表示されます。

   ![job_details](assets/job_details.png)

1. リストから操作を削除するには、ツールバーの「**[!UICONTROL 削除]**」を選択します。詳細を CSV ファイルでダウンロードするには、「**[!UICONTROL ダウンロード]**」アイコンをタップまたはクリックします。

   >[!NOTE]
   >
   >ステータスがアクティブまたは待機中のジョブは削除できません。

## 完了済みジョブのパージ {#purging-completed-jobs}

AEM Assets は、毎日午前 1 時にパージジョブを実行して、1 日以上経過した完了済みの非同期ジョブを削除します。

パージジョブのスケジュールと、完了済みジョブの詳細を削除するまでの保持期間を変更できます。また、任意の時点での詳細を保持する、完了済みジョブの最大数を設定することもできます。

1. AEM のロゴをタップまたはクリックし、**[!UICONTROL ツール]**／**[!UICONTROL 運営]**／**[!UICONTROL Web コンソール]**&#x200B;に移動します。
1. 「**[!UICONTROL Adobe CQ DAM Async Jobs Purge Scheduled]**」ジョブを開きます。
1. 完了済みジョブを削除するまでの日数のしきい値と、詳細を履歴に保持するジョブの最大数を指定します。

   ![非同期ジョブのパージをスケジュールするための設定](assets/configmgr_purge_asyncjobs.png)
   *図：非同期ジョブのパージをスケジュールするための設定*

1. 変更内容を保存します。

## 非同期処理のしきい値の設定 {#configuring-thresholds-for-asynchronous-processing}

AEM Assets が特定の操作を非同期的に処理する際の、アセットまたは参照の数のしきい値を設定できます。

### 非同期削除操作のしきい値の設定 {#configuring-thresholds-for-asynchronous-delete-operations}

削除するアセットまたはフォルダーの数がしきい値を超えると、削除操作が非同期的に実行されます。

1. AEM のロゴをタップまたはクリックし、**[!UICONTROL ツール]**／**[!UICONTROL 運営]**／**[!UICONTROL Web コンソール]**&#x200B;に移動します。
1. Web コンソールで、「**[!UICONTROL Async Delete Operation Job Processing]**」設定を開きます。
1. 「**[!UICONTROL Threshold number of assets]**」ボックスで、削除操作の非同期処理に関するアセットまたはフォルダー数のしきい値を指定します。

   ![delete_threshold](assets/delete_threshold.png)

1. 変更内容を保存します。

### 非同期移動操作のしきい値の設定 {#configuring-thresholds-for-asynchronous-move-operations}

移動するアセットやフォルダーまたは参照の数がしきい値を超えると、移動操作が非同期的に実行されます。

1. AEM のロゴをタップまたはクリックし、**[!UICONTROL ツール]**／**[!UICONTROL 運営]**／**[!UICONTROL Web コンソール]**&#x200B;に移動します。
1. Web コンソールで、「**[!UICONTROL Async Move Operation Job Processing]**」設定を開きます。
1. 「**[!UICONTROL Threshold number of assets/references]**」ボックスで、移動操作の非同期処理に関するアセットやフォルダーまたは参照の数のしきい値を指定します。

   ![move_threshold](assets/move_threshold.png)

1. 変更内容を保存します。
