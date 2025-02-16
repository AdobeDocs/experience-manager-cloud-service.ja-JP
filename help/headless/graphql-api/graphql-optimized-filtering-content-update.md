---
title: 最適化された GraphQL フィルタリング用コンテンツフラグメントの更新
description: ヘッドレスコンテンツ配信のために、Adobe Experience Manager as a Cloud Service で最適化された GraphQL フィルタリング用にコンテンツフラグメントを更新する方法について説明します。
exl-id: 211f079e-d129-4905-a56a-4fddc11551cc
feature: Headless, Content Fragments,GraphQL API
role: Admin, Developer
source-git-commit: 8d14936ad21dc5879c72383defc3db22ce9a24ef
workflow-type: ht
source-wordcount: '867'
ht-degree: 100%

---

# 最適化された GraphQL フィルタリング用コンテンツフラグメントの更新 {#updating-content-fragments-for-optimized-graphql-filtering}

GraphQL フィルターのパフォーマンスを最適化するには、コンテンツフラグメントを更新する手順を実行する必要があります。

>[!NOTE]
>
>コンテンツフラグメントを更新した後、[GraphQL クエリの最適化](/help/headless/graphql-api/graphql-optimization.md)についての推奨事項に従うことができます。


## 前提条件 {#prerequisites}

このタスクの前提条件は次のとおりです。

1. 2023.1.0 リリース以降の AEM as a Cloud Service があることを確認します。

1. タスクを実行するユーザーに次の必要な権限があることを確認します。

   * 少なくとも Cloud Manager で `Deployment Manager` の役割が必要です。

## コンテンツフラグメントの更新 {#updating-content-fragments}

1. Cloud Manager UI を使用し、インスタンスに次の変数を設定して更新を有効にします。

   ![Cloud Manager 環境の設定](assets/cfm-graphql-update-01.png "Cloud Manager 環境の設定")

   使用できる変数は以下のとおりです。

   | | 名前 | 値 | デフォルト値 | サービス | 適用済み | タイプ | メモ |
   |---|---|---|---|---|---|---|---|
   | 1 | `CF_MIGRATION_ENABLED` | `1` | `0` | すべて | | 変数 | コンテンツ移行ジョブのトリガーを有効（!=0）または無効（0）にします。 |
   | 2 | `CF_MIGRATION_ENFORCE` | `1` | `0` | すべて | | 変数 | コンテンツフラグメントの再移行を実施（!=0）。このフラグを 0 に設定すると、CF の増分移行が行われます。つまり、何らかの理由でジョブが終了した場合、ジョブの次回の実行ではジョブが終了した時点から移行が開始されます。最初の移行の実施をお勧めします（値= 1）。 |
   | 3 | `CF_MIGRATION_BATCH` | `50` | `50` | すべて | | 変数 | 移行後にコンテンツフラグメント数を保存するためのバッチのサイズ。1 つのバッチでリポジトリに保存される CF の数に関連し、リポジトリへの書き込み数を最適化するために使用できます。 |
   | 4 | `CF_MIGRATION_LIMIT` | `1000` | `1000` | すべて | | 変数 | 一度に処理するコンテンツフラグメントの最大数。`CF_MIGRATION_INTERVAL` に関する注意事項も参照してください。 |
   | 5 | `CF_MIGRATION_INTERVAL` | `60` | `600` | すべて | | 変数 | 次の制限まで残りのコンテンツフラグメントを処理する間隔（秒）。この間隔は、ジョブを開始する前の待機時間と、後続の CF_MIGRATION_LIMIT 数の各 CF の処理間の遅延の両方とも考えられます。(*) |

   >[!NOTE]
   >
   >(*)
   >
   >`CF_MIGRATION_INTERVAL` の値は、移行ジョブの合計実行時間を概算するのにも役立ちます。
   >
   >次に例を示します。
   >
   >* コンテンツフラグメントの合計数 = 20,000
   >* CF_MIGRATION_LIMIT = 1000
   >* CF_MIGRATION_INTERNAL = 60（秒）
   >* 移行完了に要する概算時間 = 60 + (20,000÷1000 x 60) = 1,260 秒 = 21 分
   >  開始時に追加される「60」秒は、ジョブの開始時の初期遅延によるものです。
   >
   >また、これはジョブの完了に必要な&#x200B;*最短*&#x200B;時間であって、I/O 時間は含まれません。実際の所要時間は、この推定値よりも長くなる場合があります。

1. 更新の進行状況および完了を監視します。

   これを行うには、以下でオーサーと golden-publish のログを監視します。

   * `com.adobe.cq.dam.cfm.impl.upgrade.UpgradeJob`

      * オーサーログの例：

        ```shell
        23.01.2023 13:13:45.926 *INFO* [sling-threadpool-09cbdb47-4d99-4c4c-b6d5-781b635ee21b-(apache-sling-job-thread-pool)-1-Content Fragment Upgrade Job Queue Config(cfm/upgrader)] com.adobe.cq.dam.cfm.impl.upgrade.UpgradeJob This instance<dd9ffdc1-0c28-4d04-9a96-5d4d223e457e> is the leader, will schedule the upgrade schedule job.
        ...
        23.01.2023 13:13:45.941 *INFO* [sling-threadpool-09cbdb47-4d99-4c4c-b6d5-781b635ee21b-(apache-sling-job-thread-pool)-1-Content Fragment Upgrade Job Queue Config(cfm/upgrader)] com.adobe.cq.dam.cfm.impl.upgrade.UpgradeJob Scheduling content fragments upgrade from version 0 to 1, slingJobId: 2023/1/23/13/13/50e1a575-4cd7-497b-adf0-62cb5768eedb_0, enforce: true, limit: 1000, batch: 50, interval: 60s
        
        23.01.2023 13:20:40.960 *INFO* [sling-threadpool-09cbdb47-4d99-4c4c-b6d5-781b635ee21b-(apache-sling-job-thread-pool)-1-Content Fragment Upgrade Job Queue Config(cfm/upgrader)] com.adobe.cq.dam.cfm.impl.upgrade.UpgradeJob Finished content fragments upgrade in 6m, slingJobId: 2023/1/23/13/13/50e1a575-4cd7-497b-adf0-62cb5768eedb_0, status: MaintenanceJobStatus{jobState=SUCCEEDED, statusMessage='Upgrade to version '1' succeeded.', errors=[], successCount=3781, failedCount=0, skippedCount=0}
        ```

      * Golden-publish ログの例：

        ```shell
        23.01.2023 12:35:05.150 *INFO* [sling-threadpool-8abcc1bb-cdcb-46d4-8565-942ad8a73209-(apache-sling-job-thread-pool)-1-Content Fragment Upgrade Job Queue Config(cfm/upgrader)] com.adobe.cq.dam.cfm.impl.upgrade.UpgradeJob This instance<ad1b399e-77be-408e-bc3f-57097498fddb> is the leader, will schedule the upgrade schedule job.
        
        23.01.2023 12:35:05.161 *INFO* [sling-threadpool-8abcc1bb-cdcb-46d4-8565-942ad8a73209-(apache-sling-job-thread-pool)-1-Content Fragment Upgrade Job Queue Config(cfm/upgrader)] com.adobe.cq.dam.cfm.impl.upgrade.UpgradeJob Scheduling content fragments upgrade from version 0 to 1, slingJobId: 2023/1/23/12/34/ad1b399e-77be-408e-bc3f-57097498fddb_0, enforce: true, limit: 1000, batch: 50, interval: 60s
        ...
        23.01.2023 12:40:45.180 *INFO* [sling-threadpool-8abcc1bb-cdcb-46d4-8565-942ad8a73209-(apache-sling-job-thread-pool)-1-Content Fragment Upgrade Job Queue Config(cfm/upgrader)] com.adobe.cq.dam.cfm.impl.upgrade.UpgradeJob Finished content fragments upgrade in 5m, slingJobId: 2023/1/23/12/34/ad1b399e-77be-408e-bc3f-57097498fddb_0, status: MaintenanceJobStatus{jobState=SUCCEEDED, statusMessage='Upgrade to version '1' succeeded.', errors=[], successCount=3781, failedCount=0, skippedCount=0}
        ```

   Splunk を使用して環境ログへのアクセスを有効にしたお客様は、以下のサンプルクエリを使用してアップグレードプロセスを監視できます。Splunk ログの有効化について詳しくは、[実稼動環境とステージ環境のデバッグ](/help/implementing/developing/introduction/logging.md#debugging-production-and-stage)を参照してください。

   ```splunk
   index=<indexName> sourcetype=aemerror aem_envId=<environmentId> msg="*com.adobe.cq.dam.cfm.impl.upgrade.UpgradeJob Finished*" 
   (aem_tier=golden-publish OR aem_tier=author) | table _time aem_tier pod_name msg | sort -_time desc
   ```

   ここで、

   * `environmentId` - 顧客環境識別子（例：`e1234`）
   * `indexName` - 顧客インデックス名、収集 `aemerror` イベント

   出力例：

   <table style="table-layout:auto">
     <thead>
       <tr>
       <th>_time</th>
       <th>aem_tier</th>
       <th>pod_name</th>
       <th>msg</th>
       </tr>
     </thead> 
     <tbody>
       <tr>
         <td>2023-04-21 06:00:35.723</td>
         <td>author</td>
         <td>cm-p1234-e1234-aem-author-76d6dc4b79-8lsb5</td>
         <td>[sling-threadpool-bb5da4dd-6b05-4230-93ea-1d5cd242e24f-(apache-sling-job-thread-pool)-1-Content Fragment Upgrade Job Queue Config(cfm/upgrader)] com.adobe.cq.dam.cfm.impl.upgrade.UpgradeJob Finished content fragments upgrade in 391m, slingJobId: 2023/4/20/23/16/db7963df-e267-489b-b69a-5930b0dadb37_0, status: MaintenanceJobStatus{jobState=SUCCEEDED, statusMessage='Upgrade to version '1' succeeded.', errors=[], successCount=36756, failedCount=0, skippedCount=0}</td>
       </tr>
       <tr>
         <td>2023-04-21 06:05:48.207</td>
         <td>golden-publish</td>
         <td>cm-p1234-e1234-aem-golden-publish-644487c9c5-lvkv2</td>
         <td>[sling-threadpool-284b9a9a-8454-461e-9bdb-44866c6ddfb1-(apache-sling-job-thread-pool)-1-Content Fragment Upgrade Job Queue Config(cfm/upgrader)] com.adobe.cq.dam.cfm.impl.upgrade.UpgradeJob Finished content fragments upgrade in 211m, slingJobId: 2023/4/20/23/15/66c1690a-cdb7-4e66-bc52-90f33394ddfc_0, status: MaintenanceJobStatus{jobState=SUCCEEDED, statusMessage='Upgrade to version '1' succeeded.', errors=[], successCount=19557, failedCount=0, skippedCount=0}</td>
       </tr>
     </tbody>
   <table>

1. 更新手順を無効にします。

   >[!IMPORTANT]
   >
   >この手順は、アップグレードを完了するために必要です。

   更新手順を実行した後、クラウド環境変数をリセットします。`CF_MIGRATION_ENABLED` を「0」に変更して、すべてのポッドのリサイクルをトリガーします。

   | | 名前 | 値 | デフォルト値 | サービス | 適用済み | タイプ | メモ |
   |---|---|---|---|---|---|---|---|
   | | `CF_MIGRATION_ENABLED` | `0` | `0` | すべて | | 変数 | コンテンツフラグメント移行ジョブの移行のトリガーを無効（0）（または有効（!=0））にします。 |

   >[!NOTE]
   >
   >コンテンツの更新は golden-publish でのみ行われ、ポッドを再利用する場合、通常の公開ポッドはすべて golden-publish に基づくため、パブリッシュ層では重要です。

1. 更新手順の完了を確認します。

   Cloud Manager デベロッパーコンソールのリポジトリブラウザーで、更新が正常に完了したことを確認できます。この確認は、コンテンツフラグメントデータをチェックするためのものです。

   * 最初の移行が完了するまでは、`cfGlobalVersion` プロパティは存在しません。
したがって、JCR ノード `/content/dam` 上ににこのプロパティがあり、値が `1` になっている場合、移行が完了したことになります。

   * 個々のコンテンツフラグメントで、次のプロパティも確認できます。

      * `_strucVersion` には `1` の値があるはずです。
      * `indexedData` 構造が存在する必要があります

     >[!NOTE]
     >
     >この手順では、オーサーインスタンスとパブリッシュインスタンスのコンテンツフラグメントを更新します。
     >
     >したがって、アドビでは、*少なくとも* 1 つのオーサーインスタンス&#x200B;*と* 1 つのパブリッシュインスタンスについては、リポジトリブラウザーを介して検証を実行することをお勧めします。

## 制限事項 {#limitations}

次の制限事項に注意してください。

* GraphQL フィルターのパフォーマンスの最適化は、すべてのコンテンツフラグメントを完全に更新した後にのみ可能です（JCR ノード `/content/dam` の `cfGlobalVersion` プロパティが存在することで示される）

* コンテンツフラグメントをコンテンツパッケージから読み込む場合（`crx/de` を使用）、更新手順を実行してから、更新手順が再実行されるまで、これらのコンテンツフラグメントは GraphQL クエリ結果で考慮されません。
