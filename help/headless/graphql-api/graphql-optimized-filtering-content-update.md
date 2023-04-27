---
title: 最適化された GraphQL フィルタリング用コンテンツフラグメントの更新
description: ヘッドレスコンテンツ配信のために、Adobe Experience Manager as a Cloud Service で最適化された GraphQL フィルタリング用にコンテンツフラグメントを更新する方法について説明します。
exl-id: 211f079e-d129-4905-a56a-4fddc11551cc
source-git-commit: e18a60197aab3866b839ff7b923f1aa135c594cc
workflow-type: tm+mt
source-wordcount: '738'
ht-degree: 100%

---

# 最適化された GraphQL フィルタリング用コンテンツフラグメントの更新 {#updating-content-fragments-for-optimized-graphql-filtering}

GraphQL フィルターのパフォーマンスを最適化するには、コンテンツフラグメントを更新する手順を実行する必要があります。

>[!NOTE]
>
>コンテンツフラグメントを更新した後、[GraphQL クエリの最適化](/help/headless/graphql-api/graphql-optimization.md)についての推奨事項に従うことができます。


## 前提条件 {#prerequisites}

2023.1.0 リリース以降の AEM as a Cloud Service があることを確認します。

## コンテンツフラグメントの更新 {#updating-content-fragments}

以下の手順を実行します。

1. Cloud Manager UI を使用し、インスタンスに次の変数を設定して更新を有効にします。

   ![Cloud Manager 環境の設定](assets/cfm-graphql-update-01.png "Cloud Manager 環境の設定")

   使用できる変数は以下のとおりです。

   <table style="table-layout:auto">
    <tbody>
     <tr>
      <th> </th>
      <th>名前</th>
      <th>値</th>
      <th>デフォルト値</th>
      <th>サービス</th>
      <th>適用済み</th>
      <th>タイプ</th>
      <th>メモ</th>
     </tr>
     <tr>
      <td>1</td>
      <td>`AEM_RELEASE_CHANNEL` </td>
      <td>`prerelease` </td>
      <td> </td>
      <td>すべて </td>
      <td> </td>
      <td>変数 </td>
      <td>この機能を有効にするのに必須です。 </td>
     </tr>
     <tr>
      <td>2</td>
      <td>`CF_MIGRATION_ENABLED` </td>
      <td>`1` </td>
      <td>`0` </td>
      <td>すべて </td>
      <td> </td>
      <td>変数 </td>
      <td>コンテンツ移行ジョブのトリガーを有効（!=0）または無効（0）にします。 </td>
     </tr>
     <tr>
      <td>3</td>
      <td>`CF_MIGRATION_ENFORCE` </td>
      <td>`1` </td>
      <td>`0` </td>
      <td>すべて </td>
      <td> </td>
      <td>変数 </td>
      <td>コンテンツフラグメントの再移行を実施（!=0）します。<br>このフラグを 0 に設定すると、CF の増分移行が行われます。つまり、何らかの理由でジョブが終了した場合、ジョブの次回の実行ではジョブが終了した時点から移行が開始されます。最初の移行を適用することをお勧めします（値 = 1）。 </td>
     </tr>
     <tr>
      <td>4</td>
      <td>`CF_MIGRATION_BATCH` </td>
      <td>`50` </td>
      <td>`50` </td>
      <td>すべて </td>
      <td> </td>
      <td>変数 </td>
      <td>移行後にコンテンツフラグメント数を保存するためのバッチのサイズ。<br>1 つのバッチでリポジトリに保存される CF の数に関連し、リポジトリへの書き込み数を最適化するために使用できます。 </td>
     </tr>
     <tr>
      <td>5</td>
      <td>`CF_MIGRATION_LIMIT` </td>
      <td>`1000` </td>
      <td>`1000` </td>
      <td>すべて </td>
      <td> </td>
      <td>変数 </td>
      <td>一度に処理するコンテンツフラグメントの最大数。<br>`CF_MIGRATION_INTERVAL` に関する注意事項も参照してください。 </td>
     </tr>
     <tr>
      <td>6</td>
      <td>`CF_MIGRATION_INTERVAL` </td>
      <td>`60` </td>
      <td>`600` </td>
      <td>すべて </td>
      <td> </td>
      <td>変数 </td>
      <td>次の制限までの残りのコンテンツフラグメントの処理間隔（秒）<br>この間隔は、ジョブを開始する前の待機時間と、後続の CF_MIGRATION_LIMIT の各 CF の処理間の遅延とも考えられます。<br>（*）</td>
     </tr>
    </tbody>
   </table>

   >[!NOTE]
   >
   >（*）
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
   >また、これはジョブの完了に必要な&#x200B;*最小*&#x200B;時間であって、I/O 時間は含まれないことにも注意してください。実際の所要時間は、この推定値よりも大幅に長くなる場合があります。

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

1. 更新手順を無効にします。

   >[!IMPORTANT]
   >
   >この手順は、アップグレードを完了するために必要です。

   更新手順を実行した後、クラウド環境変数をリセットします。`CF_MIGRATION_ENABLED` を「0」に変更して、すべてのポッドのリサイクルをトリガーします。

   <table style="table-layout:auto">
    <tbody>
     <tr>
      <th> </th>
      <th>名前</th>
      <th>値</th>
      <th>デフォルト値</th>
      <th>サービス</th>
      <th>適用済み</th>
      <th>タイプ</th>
      <th>メモ</th>
     </tr>
     <tr>
      <td></td>
      <td>`CF_MIGRATION_ENABLED` </td>
      <td>`0` </td>
      <td>`0` </td>
      <td>すべて </td>
      <td> </td>
      <td>変数 </td>
      <td>コンテンツフラグメント移行ジョブの移行のトリガーを無効（0）（または有効（!=0））にします。 </td>
     </tr>
    </tbody>
   </table>

   >[!NOTE]
   >
   >コンテンツの更新は golden-publish でのみ行われ、ポッドを再利用する場合、通常の公開ポッドはすべて golden-publish に基づくため、パブリッシュ層では特に重要です。

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
      >したがって、*少なくとも* 1 つのオーサーインスタンス&#x200B;*と* 1 つのパブリッシュインスタンスについては、リポジトリブラウザーを介して検証を実行することをお勧めします。


## 制限事項 {#limitations}

次の制限事項に注意してください。

* GraphQL フィルターのパフォーマンスの最適化は、すべてのコンテンツフラグメントを完全に更新した後にのみ可能です（JCR ノード `/content/dam` の `cfGlobalVersion` のプロパティが存在することで示される）

* コンテンツフラグメントをコンテンツパッケージから読み込む場合（`crx/de` を使用）、更新手順を実行してから、更新手順が再実行されるまで、これらのコンテンツフラグメントは GraphQL クエリ結果で考慮されません。
