---
title: AEMのインフラストラクチャとサービスの監視のas a Cloud Service
description: AEMのインフラストラクチャとサービスの監視のas a Cloud Service
source-git-commit: 8121d2e9cd98b4cc6e848f6cd6c3fa4359988053
workflow-type: tm+mt
source-wordcount: '575'
ht-degree: 0%

---


# AEMのインフラストラクチャとサービスの監視のas a Cloud Service {#monitoring-in-aem-as-a-cloud-service}

Adobe Experience Manager as a Cloud Serviceは、次の項目の監視と監視を提供します。インフラストラクチャ、サービス、ユーザーエクスペリエンス。 様々なソリューションが使用され、監視のレイヤーが複数あるので、このページは次の 3 つのセクションに分かれています。

* [外部の可用性](#external-availability)
* [内部モジュールの監視](#module-monitoring)
* [顧客の観察性](#customer-observability)

AEM as a Cloud Serviceでは、数百のクラウドネイティブモニターを使用して、各環境の状態を年間 365 日間継続的にレポートします(24/7)。 モニタの定義は静的ではなく、早期検出機能を改善するために継続的に確認されます。 さらに、Adobeは、アラートに対応するためのオンコール手順を設定しています。

Cloud Manager を使用したログや監視など、他の種類の監視に関する情報が必要な場合は、 [その他のリソース](#resources) 」セクションに入力します。

## 外部の可用性 {#external-availability}

外部の可用性は、次の 2 つの部分で構成されます。サービスエッジおよびカスタム監視。

### サービスエッジ {#service-edge}

すべてのAEMas a Cloud Service環境の可用性が監視されます。 ただし、サービスエッジ監視は実稼動環境に対してのみ設定され、指標は顧客の SLA の計算に使用されます。 環境のランタイムとAEMas a Cloud ServiceCDN を考慮に入れます。 Service Edge Monitoring では、選択した地域に近い 5 つの異なる場所を採用し、定期的に可用性を確認します。 サイトが利用できない場合は、警告がトリガーされ、Adobeのオンコールサポートチームおよびプロセスが関与します。

### カスタム監視 {#custom-monitoring}

カスタム監視機能を使用すると、以前に最大 5 つの異なる Web プロパティ URL を指定できます。 [運行中](/help/journey-migration/go-live.md). これらの URL は有効で、HTTP 200 応答コードを返す必要があります。 これらのモニタは、 [独自の CDN を持ち込む](/help/implementing/dispatcher/cdn.md#point-to-point-CDN) Adobeの管理下にないAEMas a Cloud Serviceの前で使用される、AdobeCDN と外部トラフィックルーティングの前に。 カスタム監視チェックで生成されるアラートは、Adobeのサポートチームとプロセスを引き起こします。

## 内部モジュールの監視 {#module-monitoring}

外部の可用性はエンドユーザーの監視に焦点を当てていますが、内部モジュールの監視では、アーキテクチャサブシステムが機能やパフォーマンスの低下を伴わずに通常動作しているかどうかを監視します。 問題が発生した場合は、アラートがトリガーされるので、修復は自動的に実行するか、オペレーションチームの関与を通じて実行できます。この目的は、問題が発生した可用性を防ぐことです。 モニタには様々なカテゴリがあり、次にチェックの例を示します。

* CPU iowait の割合が特定のしきい値を超えていません。
* インスタンスの再デプロイメントが一定の頻度を超えない。
* ディスク使用量が特定のしきい値を下回っています。
* 作成者リポジトリのサイズが特定の範囲内です。
* バックアップ操作が正常に完了しました。
* データベースの正常性とパフォーマンスが監視されます。
* AEM Cloud Services は、ブロックされたレプリケーションキューや整合性の取れたデータ、パフォーマンスの高いクエリを含め、期待どおりに動作しています。

Forms用にプロビジョニングされた環境に対して、追加のチェックが追加されます。 チェックの定義は静的ではなく、変更や更新の対象となることに注意してください。

## 顧客の観察性 {#customer-observability}

お客様は、 [New Relic アプリケーションのパフォーマンス監視](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/user-access-new-relic.html) 分析やトラブルシューティングのために収集され、グラフ化されたリアルタイムのパフォーマンスデータを提供するスイート。 監視スイートを使用すると、お客様は次のような様々な指標を直接監視できます。JVM パフォーマンス指標、Java のトランザクション時間、バックグラウンド外部呼び出しおよびデータベース呼び出し。

## その他のリソース {#resources}

* [New Relic アプリケーションのパフォーマンス監視](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/user-access-new-relic.html)
* [AEMas a Cloud Serviceのログ](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/developing/logging.html)
* [環境の監視](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/content/using/monitoring-environments.html)
