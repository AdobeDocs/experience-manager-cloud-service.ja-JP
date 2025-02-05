---
title: 非同期ジョブ
description: Adobe Experience Manager では、リソースを集中的に消費する一部のタスクをバックグラウンド操作として非同期に処理することでパフォーマンスを最適化します。
exl-id: 9c5c4604-1290-4dea-a14d-08f3ab3ef829
feature: Operations
role: Admin
source-git-commit: 10580c1b045c86d76ab2b871ca3c0b7de6683044
workflow-type: tm+mt
source-wordcount: '854'
ht-degree: 95%

---

# 非同期操作 {#asynchronous-operations}

Adobe Experience Manager では、パフォーマンスを悪化させないために、長時間実行されてリソースを集中的に消費する特定の操作は、バックグラウンド操作として非同期に処理されます。非同期処理では複数のジョブがキューに入れられ、システムリソースの可用性に応じて順に実行されます。

次のような操作が含まれます。

* 大量のアセットの削除
* 多数のアセットまたは多数の参照があるアセットの移動
* アセットメタデータの一括書き出し／読み込み
* しきい値制限セットを超えるアセットのリモート Experience Manager デプロイメントからの取得
* ライブコピーのロールアウト

非同期ジョブのステータスは、**グローバルナビゲーション**&#x200B;の&#x200B;**[!UICONTROL バックグラウンド操作]**&#x200B;ダッシュボードから、**ツール**／**一般**／**ジョブ**&#x200B;で確認できます。

>[!NOTE]
>
>デフォルトでは、非同期ジョブは並行して実行されます。*`n`* を CPU コアの数とすると、デフォルトでは *`n/2`* のジョブを並行して実行できます。ジョブキューのカスタム設定を使用するには、Web コンソールから **[!UICONTROL Async Operation Default Queue Config]** と **Async Operation Page Move and Rollout Config** を変更します。
>
>詳しくは、[キューの設定](https://sling.apache.org/documentation/bundles/apache-sling-eventing-and-job-handling.html#queue-configurations)を参照してください。

## 非同期操作のステータスの監視 {#monitor-the-status-of-asynchronous-operations}

AEM が操作を非同期で処理する場合は常に、[インボックス](/help/sites-cloud/authoring/inbox.md)とメール（有効になっている場合）で通知を受信します。

非同期操作のステータスの詳細を表示するには、**[!UICONTROL バックグラウンド操作]**&#x200B;ページに移動します。

1. Experience Manager インターフェイスで、**グローバルナビゲーション**／**ツール**／**一般**／**ジョブ**&#x200B;を選択します。

1. **[!UICONTROL バックグラウンド操作]**&#x200B;ページで、操作の詳細をレビューします。

   ![非同期操作のステータスと詳細](assets/async-operation-status.png)

   特定の操作の進行状況を確認するには、「**[!UICONTROL ステータス]**」列の値を参照します。進行状況に応じて、次のいずれかのステータスが表示されます。

   * **[!UICONTROL アクティブ]**：操作を処理中です

   * **[!UICONTROL 成功]**：操作が完了しました

   * **[!UICONTROL 失敗]**&#x200B;または&#x200B;**[!UICONTROL エラー]**：操作を処理できませんでした。

   * **[!UICONTROL スケジュール済み]**：操作は後で処理するようにスケジュールされています。

1. アクティブな操作を停止するには、リストから対象の操作を選択し、ツールバーの「**[!UICONTROL 停止]**」をクリックします。

   ![stop_icon](assets/async-stop-icon.png)

1. 説明やログなど、その他の詳細を表示するには、操作を選択し、ツールバーの「**[!UICONTROL 開く]**」をクリックします。

   ![open_icon](assets/async-open-icon.png)

   ジョブの詳細ページが表示されます。

   ![job_details](assets/async-job-details.png)

1. リストから操作を削除するには、ツールバーの「**[!UICONTROL 削除]**」を選択します。詳細を CSV ファイルでダウンロードするには、「**[!UICONTROL ダウンロード]**」をクリックします。

   >[!NOTE]
   >
   >ステータスが&#x200B;**アクティブ**&#x200B;または&#x200B;**待機中**&#x200B;のジョブは削除できません。

## 非同期ジョブ処理オプションの設定 {#configure}

非同期ジョブには、設定できるオプションがいくつかあります。次の例で、ローカル開発システム上で設定マネージャーを使用して設定する方法を示します。

>[!NOTE]
>
>[OSGi 設定](/help/implementing/deploying/configuring-osgi.md#creating-osgi-configurations)は可変コンテンツと見なされ、そのような設定は実稼動環境のコンテンツパッケージとしてデプロイする必要があります。

### 完了したジョブをパージ {#purging-completed-jobs}

AEM は、毎日午前 1 時にパージジョブを実行して、1 日以上経過した完了済みの非同期ジョブを削除します。

パージジョブのスケジュールと、完了済みジョブの詳細を削除するまでの保持期間は、変更することができます。任意の時点で詳細を保持する完了済みジョブの最大数を設定することもできます。

1. AEM SDK Quickstart Jar の AEM web コンソール（`https://<host>:<port>/system/console`）に管理者ユーザーとしてログインします。
1. **OSGi**／**設定**&#x200B;に移動します。
1. **[!UICONTROL Adobe Granite Async Jobs Purge Scheduled Job]** ジョブを開きます。
1. 以下を指定します。
   * 完了したジョブが削除されるまでの日数のしきい値。
   * 詳細が履歴に保持されるジョブの最大数。
   * パージを実行するタイミングを表す cron 式。

   ![非同期ジョブのパージをスケジュールするための設定](assets/async-purge-job.png)

1. 変更内容を保存します。

### 非同期アセット削除操作を設定 {#configuring-synchronous-delete-operations}

削除するアセットまたはフォルダーの数がしきい値を超えると、削除操作が非同期的に実行されます。

1. AEM SDK Quickstart Jar の AEM web コンソール（`https://<host>:<port>/system/console`）に管理者ユーザーとしてログインします。
1. **OSGi**／**設定**&#x200B;に移動します。
1. Web コンソールから、**[!UICONTROL 非同期プロセスのデフォルトキュー設定]** を開きます。
1. 「**[!UICONTROL Threshold number of assets]**」ボックスで、削除操作の非同期処理に関するアセットまたはフォルダー数のしきい値を指定します。

   ![アセット削除しきい値](assets/async-delete-threshold.png)

1. 「**メール通知を有効にする**」オプションを選択すると、このジョブステータスに関するメール通知を受信できます例えば、成功、失敗です。
1. 変更を保存します。

### 非同期アセット移動操作を設定 {#configuring-asynchronous-move-operations}

移動するアセットやフォルダーまたは参照の数がしきい値を超えると、移動操作が非同期的に実行されます。

1. AEM SDK Quickstart Jar の AEM web コンソール（`https://<host>:<port>/system/console`）に管理者ユーザーとしてログインします。
1. **OSGi**／**設定**&#x200B;に移動します。
1. Web コンソールから、**[!UICONTROL 非同期移動操作ジョブ処理設定]** を開きます。
1. 「**[!UICONTROL Threshold number of assets/references]**」ボックスで、移動操作の非同期処理に関するアセットやフォルダーまたは参照の数のしきい値を指定します。

   ![アセット移動しきい値](assets/async-move-threshold.png)

1. 「**メール通知を有効にする**」オプションを選択すると、このジョブステータスに関するメール通知を受信できます例えば、成功、失敗です。
1. 変更を保存します。

### 非同期 MSM 操作を設定 {#configuring-asynchronous-msm-operations}

1. AEM SDK Quickstart Jar の AEM web コンソール（`https://<host>:<port>/system/console`）に管理者ユーザーとしてログインします。
1. **OSGi**／**設定**&#x200B;に移動します。
1. Web コンソールから、**[!UICONTROL 非同期ページ移動操作ジョブ処理設定]** を開きます。
1. 「**メール通知を有効にする**」オプションを選択すると、このジョブステータスに関するメール通知を受信できます例えば、成功、失敗です。

   ![MSM 設定](assets/async-msm.png)

1. 変更内容を保存します。

>[!MORELIKETHIS]
>
>* [ページの管理](/help/sites-cloud/authoring/sites-console/managing-pages.md)
>* [アセットメタデータの一括読み込みおよび書き出し](/help/assets/metadata-import-export.md)
>* [Connected Assets を使用したリモートデプロイメントからの DAM アセットの共有](/help/assets/use-assets-across-connected-assets-instances.md)
