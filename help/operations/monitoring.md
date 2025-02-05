---
title: AEM as a Cloud Service のインフラストラクチャとサービスモニタリング
description: AEM as a Cloud Service のインフラストラクチャとサービスモニタリング
exl-id: 82432c11-37ec-48ac-a52b-487abdc859fa
feature: Operations
role: Admin
source-git-commit: 10580c1b045c86d76ab2b871ca3c0b7de6683044
workflow-type: tm+mt
source-wordcount: '562'
ht-degree: 95%

---

# AEM as a Cloud Service のインフラストラクチャとサービスモニタリング {#monitoring-in-aem-as-a-cloud-service}

Adobe Experience Manager as a Cloud Service は、インフラストラクチャ、サービスおよびユーザーエクスペリエンスの観測と監視を可能にします。様々なソリューションが使用されており、監視には複数のレイヤーがあるので、このページは 3 つのセクションに分かれています。

* [外部可用性](#external-availability)
* [内部モジュールの監視](#module-monitoring)
* [顧客の可観測性](#customer-observability)

AEM as a Cloud Service では、数百ものクラウドネイティブモニターを使用して、各環境の状態を年中無休で継続的にレポートします。モニターの定義は静的ではなく、早期検出機能を向上させるために継続的に見直されます。 さらに、アドビでは、アラートに対応するためのオンコール手順を設定しています。

Cloud Manager を使用したログや監視など、他の種類の監視に関する情報が必要な場合は、[その他のリソース](#resources)のセクションを参照してください。

## 外部可用性 {#external-availability}

外部可用性は、サービスエッジとカスタム監視の 2 つの部分で構成されます。

### サービスエッジ {#service-edge}

すべての AEM as a Cloud Service 環境の可用性が監視されます。ただし、サービスエッジ監視は実稼動環境に対してのみ設定され、指標は顧客の SLA の計算に使用されます。 環境のランタイムと AEM as a Cloud Service CDN を考慮に入れます。 サービスエッジ監視では、選択した地域に近い 5 つの異なる場所を採用し、定期的に可用性を確認します。 サイトが利用できない場合は、アラートがトリガーされ、アドビのオンコールサポートチームおよびプロセスが関与します。

### カスタム監視 {#custom-monitoring}

カスタム監視機能を使用する場合は、[公開](/help/journey-migration/go-live.md)前に最大 5 つの異なる web プロパティ URL を指定できます。これらの URL は有効で、かつ HTTP 200 応答コードを返す必要があります。 これらのモニターでは、Adobe CDN の前に[独自の CDN を導入する](/help/implementing/dispatcher/cdn.md#point-to-point-CDN)顧客や、アドビの管理下にない AEM as a Cloud Service の前での外部トラフィックルーティングの使用をサポートしています。カスタム監視チェックで生成されるアラートによって、アドビのサポートチームとプロセスが関与します。

>[!NOTE]
>
> この機能は、実稼動環境および [ 高度なクラウドサポート ](https://experienceleague.adobe.com/docs/support-resources/data-sheets/overview.html?lang=ja#support-add-ons) を使用するお客様にのみ提供されます。 ご不明な点がある場合は、Adobeアカウントチームにお問い合わせください。

## 内部モジュールの監視 {#module-monitoring}

外部可用性がエンドユーザーの監視に的を絞っているのに対して、内部モジュールの監視では、機能やパフォーマンスが低下することなく、アーキテクチャサブシステムが正常に動作しているかどうかを監視します。問題が発生した場合は、アラートがトリガーされるので、可用性が損なわれないようにすることを目的として、自動的に、または運用チームの関与を通じて修復を実行できます。モニターには様々なカテゴリがあります。以下にチェックの例をいくつか示します。

* CPU iowait の割合が特定のしきい値を超えていません。
* インスタンスの再デプロイメントが一定の頻度を超えていません。
* ディスク使用量が特定のしきい値を下回っています。
* オーサーリポジトリのサイズが特定の範囲内です。
* バックアップ操作が正常に完了しました。
* データベースの正常性とパフォーマンスが監視されています。
* AEM Cloud Services は、レプリケーションキューがブロックされていないこと、データの整合性が取れていること、クエリのパフォーマンスが高いことなど、想定どおりに動作しています。

Forms 用にプロビジョニングされた環境に対して、チェックが追加されます。チェックの定義は静的なものではなく、変更や更新の対象となります。

## 顧客の可観測性 {#customer-observability}

お客様は、分析やトラブルシューティングのために収集およびグラフ化されたリアルタイムのパフォーマンスデータを提供する [New Relic アプリケーションパフォーマンス監視](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/user-access-new-relic.html?lang=ja)スイートを使用できます。監視スイートを使用すると、お客様は、JVM パフォーマンス指標、Java™ のトランザクション時間、バックグラウンド外部呼び出し、データベース呼び出しなど、様々な指標を直接監視できます。

## その他のリソース {#resources}

* [New Relic アプリケーションパフォーマンス監視](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/user-access-new-relic.html?lang=ja)
* [AEM as a Cloud Service のログ](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/developing/logging.html?lang=ja)
* [環境の監視](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/content/using/monitoring-environments.html?lang=ja)
