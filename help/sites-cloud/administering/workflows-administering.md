---
title: ワークフローインスタンスの管理
description: ワークフローコンソールを使用したワークフローインスタンスの管理方法について説明します
feature: Administering
role: Admin
exl-id: d2adb5e8-3f0e-4a3b-b7d0-dbbc5450e45f
solution: Experience Manager Sites
source-git-commit: 372d8969b1939e9a24d7910a1678a17c0dc9f9fd
workflow-type: tm+mt
source-wordcount: '1282'
ht-degree: 92%

---

# ワークフローインスタンスの管理 {#administering-workflow-instances}

ワークフローコンソールには、ワークフローインスタンスを管理し、それらが想定どおりに実行されていることを確認するための複数のツールが用意されています。

ワークフローの管理用に、次の各種コンソールが用意されています。[グローバルナビゲーション](/help/sites-cloud/authoring/basic-handling.md#global-navigation)を使用して&#x200B;**ツール**&#x200B;パネルを開き、その後「**ワークフロー**」を選択します。

* **モデル**：ワークフローの定義を管理します
* **インスタンス**：実行中のワークフローインスタンスを表示および管理します
* **ランチャー**：ワークフローの起動方法を管理します
* **アーカイブ**：正常に完了したワークフローの履歴を表示します
* **失敗**：エラーで終了したワークフローの履歴を表示します
* **自動割り当て**：テンプレートへの自動割り当てワークフローを設定します

## ワークフローインスタンスのステータスの監視 {#monitoring-the-status-of-workflow-instances}

1. ナビゲーションを使用して、**ツール**／**ワークフロー**&#x200B;を選択します。
1. 「**インスタンス**」を選択して現在実行中のワークフローインスタンスのリストを表示します。
1. 上部パネルの右隅で、ワークフローインスタンスに&#x200B;**実行中のワークフロー**、**ステータス**、**詳細**&#x200B;が表示されます。
1. **実行中のワークフロー**：実行中のワークフローの数とステータスを表示します。例えば、以下の画像で表示されているのは、AEMインスタンスの&#x200B;**実行中のワークフロー**&#x200B;の数と&#x200B;**ステータス**&#x200B;です。

   * **ステータス：正常**
     ![status-healthy](/help/sites-cloud/administering/assets/status-healthy.png)

   * **ステータス：正常でない**
     ![status-unhealthy](/help/sites-cloud/administering/assets/status-unhealthy.png)

1. ワークフローインスタンスの&#x200B;**ステータスの詳細**&#x200B;では、「**詳細**」をクリックすると、**実行中のワークフローインスタンス**、**完了したワークフローインスタンス**、**中止されたワークフローインスタンス**、**失敗したワークフローインスタンス**&#x200B;などの数が表示されます。例えば、以下の画像では、**ステータスの詳細**&#x200B;が表示されています。

   * **ステータスの詳細：正常**
     ![status-details-healthy](/help/sites-cloud/administering/assets/status-details-healthy.png)

   * **ステータスの詳細：正常でない**
     ![status-details-healthy](/help/sites-cloud/administering/assets/status-details-unhealthy.png)

   >[!NOTE]
   >
   > ワークフローインスタンスを正常な状態に維持するには、[ワークフローインスタンスの定期的なパージ](#regular-purging-of-workflow-instances)または[ワークフローのベストプラクティス](https://experienceleague.adobe.com/docs/experience-manager-65/developing/extending-aem/extending-workflows/workflows-best-practices.html?lang=ja)に記載されているベストプラクティスに従います。

## ワークフローインスタンスの検索 {#search-workflow-instances}

1. ナビゲーションを使用して、**ツール**／**ワークフロー**&#x200B;を選択します。
1. 「**インスタンス**」を選択して現在進行中のワークフローインスタンスのリストを表示します。上部のパネルの左隅で、「**フィルター**」を選択します。または、alt+1 キーを押します。次のダイアログが開きます。

   ![wf-99-1](/help/sites-cloud/administering/assets/wf-99-1.png)

1. フィルターダイアログで、ワークフローの検索条件を選択します。次の入力に基づいて検索できます。

   * ペイロードパス：特定のパスの選択
   * ワークフローモデル：ワークフローモデルの選択
   * 担当者：ワークフローの担当者の選択
   * タイプ：タスク、ワークフロー項目、またはワークフローの失敗
   * タスクステータス：アクティブ、完了または終了
   * 役割：所有者および担当者、所有者のみ、担当者のみ
   * 開始日：指定した日付の前または後の開始日
   * 終了日：指定した日付の前または後の終了日
   * 期日：指定した日付の前または後の期日
   * 更新日：指定した日付の前または後の更新日

## ワークフローインスタンスの休止、再開および終了 {#suspending-resuming-and-terminating-a-workflow-instance}

1. ナビゲーションを使用して、**ツール**／**ワークフロー**&#x200B;を選択します。
1. 「**インスタンス**」を選択して現在進行中のワークフローインスタンスのリストを表示します。

   ![wf-96-1](/help/sites-cloud/administering/assets/wf-96-1.png)

1. 特定の項目を選択してから、適宜「**終了**」、「**休止**」、または「**再開**」を使用します。この際、確認または詳細（あるいはその両方）を求められます。

   ![wf-97-1](/help/sites-cloud/administering/assets/wf-97-1.png)

   >[!NOTE]
   >
   >
   >ワークフローを終了または中止するには、ユーザーの操作を待機中の状態（参加者ステップなど）である必要があります。現在ジョブを実行中のワークフロー（実行中のアクティブなスレッド）を中止しようとすると、予期した結果が得られない場合があります。


## アーカイブされたワークフローの表示 {#viewing-archived-workflows}

1. ナビゲーションを使用して、**ツール**／**ワークフロー**&#x200B;を選択します。

1. 「**アーカイブ**」を選択して正常に完了したワークフローインスタンスのリストを表示します。

   ![archived-instances](/help/sites-cloud/administering/assets/archived-instances.png)

   >[!NOTE]
   >
   >
   >中止ステータスはユーザーアクションの結果として発生するので、正常終了と見なされます。例えば、次のような場合が当てはまります。
   >
   >* 「**終了**」アクションが使用された場合
   >* ワークフローの対象となるページが（強制的に）削除されたことによって、ワークフローが終了した場合。

1. 特定の項目を選択し、「**履歴を開く**」で詳細を確認します。

   ![wf-99](/help/sites-cloud/administering/assets/wf-99.png)

## ワークフローインスタンスのエラーの修正 {#fixing-workflow-instance-failures}

ワークフローが失敗した場合、AEM の&#x200B;**エラー**&#x200B;コンソールを使用してエラーの原因を調べ、特定された原因に応じて適切なアクションを取ることができます。

* **エラーの詳細**
ウィンドウが開き、**エラーメッセージ**、**ステップ、**&#x200B;エラースタック**&#x200B;が表示されます。

* **履歴を開く**&#x200B;ワークフローの履歴の詳細を表示します。

* **ステップを再試行**&#x200B;スクリプトステップコンポーネントのインスタンスをもう一度実行します。発生したエラーの原因を修正した後に「ステップを再試行」コマンドを使用します。例えば、プロセスステップが実行するスクリプトのバグを修正した後にステップを再試行します。
* **終了**&#x200B;エラーが原因で解決できない問題がワークフローに発生した場合にワークフローを終了します。例は、環境条件（リポジトリー内の情報がワークフローインスタンスで無効になったなど）にワークフローが依存している可能性がある場合です。
* **終了して再試行**&#x200B;は、元のペイロード、タイトルおよび説明を使用して新しいワークフローインスタンスが開始される点を除き、**終了**&#x200B;と同様です。

エラーを調査し、その後ワークフローを再開または終了するには、次のステップに従います。

1. ナビゲーションを使用して、**ツール**／**ワークフロー**&#x200B;を選択します。

1. 「**失敗**」を選択して、正常に完了しなかったワークフローインスタンスのリストを表示します。
1. 特定の項目を選択してから、適切なアクションを選択します。

![workflow-failure](/help/sites-cloud/administering/assets/workflow-failure.png)

## ワークフローインスタンスの定期的なパージ {#regular-purging-of-workflow-instances}

ワークフローインスタンスの数を最小限に抑えるとワークフローエンジンのパフォーマンスが向上します。このため、完了したまたは実行中のワークフローインスタンスをリポジトリーから定期的に削除できます。

有効期間とステータスに応じてワークフローインスタンスをパージするように **Adobe Granite のワークフローのパージ設定**&#x200B;を設定します。また、すべてのモデルまたは特定のモデルのワークフローインスタンスをパージすることもできます。

また、様々な条件を満たすワークフローインスタンスをパージするために、サービスの設定を複数作成することもできます。例えば、予想していた時間よりも大幅に実行時間の長い特定のワークフローモデルのインスタンスをパージする設定を作成します。さらに、リポジトリのサイズを最小限に抑えるために、数日が経過した後に完了したワークフローをすべてパージするもう 1 つの設定を作成します。

サービスを設定するには、OSGi 設定ファイルを設定します。「[OSGi 設定ファイル](/help/implementing/deploying/configuring-osgi.md)」を参照してください。次の表では、どちらの方法でも必要になるプロパティについて説明しています。

>[!NOTE]
>リポジトリーに設定を追加する場合のサービス PID は次のとおりです。
>`com.adobe.granite.workflow.purge.Scheduler`
>このサービスはファクトリサービスなので、`sling:OsgiConfig` ノードの名前には次のような ID サフィックスが必要です。
>`com.adobe.granite.workflow.purge.Scheduler-myidentifier`

| プロパティ名（web コンソール） | OSGi のプロパティ名 | 説明 |
|--- |--- |--- |
| ジョブ名  | `scheduledpurge.name` | スケジュール設定されたパージのわかりやすい名前。 |
| ワークフローのステータス | `scheduledpurge.workflowStatus` | パージするワークフローインスタンスのステータス。次の値が有効です。<br><br>- COMPLETED：完了したワークフローインスタンスはパージされます。<br> – 実行中：実行中のワークフローインスタンスはパージされます。 |
| パージするモデル | `scheduledpurge.modelIds` | パージするワークフローモデルの ID。<br>ID は model ノードのパスで、例は次のようになります。<br> `/conf/global/settings/workflow/models/dam/update_asset/jcr:content/model` <br><br> すべてのワークフローモデルのインスタンスをパージする値を指定しません。<br> 複数のモデルを指定するには、web コンソールの「`+`」ボタンをクリックします。 |
| ワークフロー経過日数 | `scheduledpurge.daysold` | パージするワークフローインスタンスの有効期間（日数）。 |
| ワークフローペイロードパッケージ | `scheduledpurge.purgePackagePayload` | ペイロードパッケージをパージする必要があるかどうかを示します（`true` または `false`）。 |


## インボックスの最大サイズの設定 {#setting-the-maximum-size-of-the-inbox}

インボックスの最大サイズは、**Adobe Granite Workflow Service** を設定することで設定できます。「[リポジトリーへの OSGi 設定の追加](/help/implementing/deploying/configuring-osgi.md)」を参照してください。次の表に、設定可能なプロパティについて説明します。

>[!NOTE]
>リポジトリーに設定を追加する場合のサービス PID は次のとおりです。
>`com.adobe.granite.workflow.core.WorkflowSessionFactory`。

| プロパティ名（web コンソール） | OSGi のプロパティ名 |
|---|---|
| 最大院ボックスクエリサイズ | granite.workflow.inboxQuerySize |

## 顧客所有のデータストアに対するワークフロー変数の使用 {#using-workflow-variables-customer-datastore}

ワークフローで処理されたデータは、アドビ提供のストレージ（JCR）に保存されます。このデータは、本来、機密性が高い可能性があります。ユーザー定義のメタデータ／データをすべて、アドビ提供のストレージではなく、ユーザー管理のストレージに保存することができます。以下の節では、これらの変数を外部ストレージ用に設定する方法について説明します。

### メタデータの外部ストレージを使用するようにモデルの設定 {#set-model-for-external-storage}

ワークフローモデルのレベルでは、モデル（およびそのランタイムインスタンス）にメタデータの外部ストレージが含まれていることを示すフラグが用意されています。外部ストレージ用にマークされたモデルのワークフローインスタンスに対するワークフロー変数は JCR に保持されません。

プロパティ *userMetadataPersistenceEnabled* は、ワークフローモデルの *jcr:content ノード* に格納されます。 このフラグは、ワークフローメタデータに *cq:userMetaDataCustomPersistenceEnabled* として保持されます。

以下の図は、ワークフローにフラグを設定する方法を示しています。

![workflow-externalize-config](/help/sites-cloud/administering/assets/workflow-externalize-config.png)

### 外部ストレージ内のメタデータの API {#apis-for-metadata-external-storage}

変数を外部に保存するには、ワークフローで公開している API を実装する必要があります。

UserMetaDataPersistenceContext

次のサンプルは、API の使用方法を示しています。

```
@ProviderType
public interface UserMetaDataPersistenceContext {
 
    /**
     * Gets the workflow for persistence
     * @return workflow
     */
    Workflow getWorkflow();
 
    /**
     * Gets the workflow id for persistence
     * @return workflowId
     */
    String getWorkflowId();
 
    /**
     * Gets the user metadata persistence id
     * @return userDataId
     */
    String getUserDataId();
}
```

UserMetaDataPersistenceProvider

```
/**
 * This provider can be implemented to store the user defined workflow-data metadata in a custom storage location
 */
@ConsumerType
public interface UserMetaDataPersistenceProvider {
 
   /**
    * Retrieves the metadata using a unique identifier
    * @param userMetaDataPersistenceContext
    * @param metaDataMap of user defined workflow data metaData
    * @throws WorkflowException
    */
   void get(UserMetaDataPersistenceContext userMetaDataPersistenceContext, MetaDataMap metaDataMap) throws WorkflowException;
 
   /**
    * Stores the given metadata to the custom storage location
    * @param userMetaDataPersistenceContext
    * @param metaDataMap metadata map
    * @return the unique identifier that can be used to retrieve metadata. If null is returned, then workflowId is used.
    * @throws WorkflowException
    */
   String put(UserMetaDataPersistenceContext userMetaDataPersistenceContext, MetaDataMap metaDataMap) throws WorkflowException;
 
} 
```
