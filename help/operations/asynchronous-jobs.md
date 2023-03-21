---
title: 非同期ジョブ
description: Adobe Experience Managerは、リソースを集中的に消費する一部のタスクをバックグラウンド操作として非同期的に処理することでパフォーマンスを最適化します。
exl-id: 9c5c4604-1290-4dea-a14d-08f3ab3ef829
source-git-commit: 26ca2addb14f62588035323ce886ae890919b759
workflow-type: tm+mt
source-wordcount: '971'
ht-degree: 65%

---

# 非同期操作 {#asynchronous-operations}

Adobe Experience Manager では、パフォーマンスに悪影響を与えないように、長時間実行されてリソースを集中的に消費する特定の操作は、バックグラウンド操作として非同期的に処理されます。 非同期処理では複数のジョブがキューに入れられ、システムリソースの可用性に応じて順に実行されます。

次の操作が含まれます。

* 多数のアセットの削除
* 多数のアセットまたは多数の参照があるアセットの移動
* アセットメタデータの一括書き出し／読み込み
* しきい値制限セットを超えるアセットのリモート Experience Manager デプロイメントからの取得
* ページの移動
* ライブコピーのロールアウト

非同期ジョブのステータスは、 **[!UICONTROL バックグラウンド操作]** ダッシュボード： **グローバルナビゲーション** -> **ツール** -> **一般** -> **ジョブ**.

>[!NOTE]
>
>デフォルトでは、非同期ジョブは並行して実行されます。*`n`* を CPU コアの数とすると、デフォルトでは *`n/2`* のジョブを並行して実行できます。ジョブキューのカスタム設定を使用するには、Web コンソールから **[!UICONTROL Async Operation Default Queue Config]** と **Async Operation Page Move and Rollout Config** を変更します。
>
>詳しくは、[キューの設定](https://sling.apache.org/documentation/bundles/apache-sling-eventing-and-job-handling.html#queue-configurations)を参照してください。

## 非同期操作のステータスの監視 {#monitor-the-status-of-asynchronous-operations}

AEM が操作を非同期で処理する場合は常に、[インボックス](/help/sites-cloud/authoring/getting-started/inbox.md)とメール（有効になっている場合）で通知を受信します。

非同期操作のステータスの詳細を表示するには、 **[!UICONTROL バックグラウンド操作]** ページ。

1. 「Experience Manager」インターフェイスで、 **グローバルナビゲーション** -> **ツール** -> **一般** -> **ジョブ**.

1. 内 **[!UICONTROL バックグラウンド操作]** ページで、操作の詳細を確認します。

   ![非同期操作のステータスと詳細](assets/async-operation-status.png)

   特定の操作の進行状況を確認するには、「**[!UICONTROL ステータス]**」列の値を参照します。進行状況に応じて、次のいずれかのステータスが表示されます。

   * **[!UICONTROL アクティブ]**:操作を処理中です

   * **[!UICONTROL 成功]**:操作が完了しました

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

非同期ジョブには、設定できるオプションが多数あります。 次の例は、ローカル開発・システム上で Configuration Manager を使用してこれを行う方法を示しています。

>[!NOTE]
>
>[OSGi 設定](/help/implementing/deploying/configuring-osgi.md#creating-osgi-configurations) は可変コンテンツと見なされ、そのような設定は実稼動環境のコンテンツパッケージとしてデプロイする必要があります。

### 完了したジョブをパージ {#purging-completed-jobs}

AEMは、毎日 01:00 にパージジョブを実行し、1 日以上経過した完了済みの非同期ジョブを削除します。

削除ジョブのスケジュールと、完了したジョブの詳細が削除前に保持される期間を変更できます。 詳細を任意の時点で保持する、完了したジョブの最大数も設定できます。

1. AEM SDK Quickstart Jar のAEM Web コンソール ( ) にログインします。 `https://<host>:<port>/system/console` を管理者ユーザーとして設定します。
1. に移動します。 **OSGi** > **設定**
1. **[!UICONTROL Adobe Granite Async Jobs Purge Scheduled Job]** ジョブを開きます。
1. 以下を指定します。
   * 完了したジョブが削除されるまでの日数のしきい値。
   * 詳細が履歴に保持されるジョブの最大数。
   * パージを実行するタイミングを表す cron 式。

   ![非同期ジョブのパージをスケジュールするための設定](assets/async-purge-job.png)

1. 変更内容を保存します。

### 非同期アセット削除操作を設定 {#configuring-synchronous-delete-operations}

削除するアセットまたはフォルダーの数がしきい値を超えると、削除操作が非同期的に実行されます。

1. AEM SDK Quickstart Jar のAEM Web コンソール ( ) にログインします。 `https://<host>:<port>/system/console` を管理者ユーザーとして設定します。
1. に移動します。 **OSGi** > **設定**
1. Web コンソールから、「**[!UICONTROL Async Process Default Queue Configuration]**」を開きます。
1. 「**[!UICONTROL Threshold number of assets]**」ボックスで、削除操作の非同期処理に関するアセットまたはフォルダー数のしきい値を指定します。

   ![アセット削除しきい値](assets/async-delete-threshold.png)

1. 「**メール通知を有効にする**」オプションを選択すると、このジョブステータスに関するメール通知を受信できます例えば、成功、失敗です。
1. 変更を保存します。

### 非同期アセット移動操作を設定 {#configuring-asynchronous-move-operations}

移動するアセットやフォルダーまたは参照の数がしきい値を超えると、移動操作が非同期的に実行されます。

1. AEM SDK Quickstart Jar のAEM Web コンソール ( ) にログインします。 `https://<host>:<port>/system/console` を管理者ユーザーとして設定します。
1. に移動します。 **OSGi** > **設定**
1. Web コンソールで、「**[!UICONTROL Async Move Operation Job Processing]**」設定を開きます。
1. 「**[!UICONTROL Threshold number of assets/references]**」ボックスで、移動操作の非同期処理に関するアセットやフォルダーまたは参照の数のしきい値を指定します。

   ![アセット移動しきい値](assets/async-move-threshold.png)

1. 「**メール通知を有効にする**」オプションを選択すると、このジョブステータスに関するメール通知を受信できます例えば、成功、失敗です。
1. 変更を保存します。

### 非同期ページ移動操作を設定 {#configuring-asynchronous-page-move-operations}

移動するページへの参照数がしきい値を超えると、移動操作は非同期に実行されます。

1. AEM SDK Quickstart Jar のAEM Web コンソール ( ) にログインします。 `https://<host>:<port>/system/console` を管理者ユーザーとして設定します。
1. に移動します。 **OSGi** > **設定**
1. Web コンソールで、「**[!UICONTROL Async Page Move Operation Job Processing Configuration]**」を開きます。
1. 「**[!UICONTROL Threshold number of references]**」ボックスで、ページ移動操作の非同期処理に関する参照の数のしきい値を指定します。

   ![ページ移動しきい値](assets/async-page-move.png)

1. 「**メール通知を有効にする**」オプションを選択すると、このジョブステータスに関するメール通知を受信できます例えば、成功、失敗です。
1. 変更を保存します。

### 非同期 MSM 操作を設定 {#configuring-asynchronous-msm-operations}

1. AEM SDK Quickstart Jar のAEM Web コンソール ( ) にログインします。 `https://<host>:<port>/system/console` を管理者ユーザーとして設定します。
1. に移動します。 **OSGi** > **設定**
1. Web コンソールで、「**[!UICONTROL Async Page Move Operation Job Processing Configuration]**」を開きます。
1. 「**メール通知を有効にする**」オプションを選択すると、このジョブステータスに関するメール通知を受信できます例えば、成功、失敗です。

   ![MSM 設定](assets/async-msm.png)

1. 変更内容を保存します。

>[!MORELIKETHIS]
>
>* [ページの作成と整理](/help/sites-cloud/authoring/fundamentals/organizing-pages.md)
>* [アセットメタデータの一括読み込みおよび書き出し](/help/assets/metadata-import-export.md)
>* [Connected Assets を使用したリモートデプロイメントからの DAM アセットの共有](/help/assets/use-assets-across-connected-assets-instances.md)

