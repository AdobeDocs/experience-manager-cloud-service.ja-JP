---
title: AEM as a Cloud Service のインフラストラクチャとサービスモニタリング
description: AEM as a Cloud Service のインフラストラクチャとサービスモニタリング
exl-id: 82432c11-37ec-48ac-a52b-487abdc859fa
source-git-commit: 1994b90e3876f03efa571a9ce65b9fb8b3c90ec4
workflow-type: tm+mt
source-wordcount: '588'
ht-degree: 46%

---

# AEM as a Cloud Service のインフラストラクチャとサービスモニタリング {#monitoring-in-aem-as-a-cloud-service}

Adobe Experience Manager as a Cloud Serviceは、次の項目の監視と監視を提供します。インフラストラクチャ、サービス、ユーザーエクスペリエンス。 様々なソリューションが使用されており、監視には複数のレイヤーがあるので、このページは 3 つのセクションに分かれています。

* [外部可用性](#external-availability)
* [内部モジュールの監視](#module-monitoring)
* [顧客の可観測性](#customer-observability)

AEM as a Cloud Service では、数百ものクラウドネイティブモニターを使用して、各環境の状態を年中無休で継続的にレポートします。モニターの定義は静的ではなく、早期検出機能を向上させるために継続的に見直されます。 また、Adobeは、アラートに対応するためのオンコール手順を設定しています。

Cloud Manager を使用したログや監視など、他の種類の監視に関する情報が必要な場合は、 [その他のリソース](#resources).

## 外部可用性 {#external-availability}

外部の可用性は、次の 2 つの部分で構成されています。サービスエッジおよびカスタム監視。

### サービスエッジ {#service-edge}

AEMのすべての環境が使用可能かどうかを監視します。 ただし、サービスエッジ監視は実稼動環境に対してのみ設定され、指標は顧客の SLA の計算に使用されます。 環境のランタイムと AEM as a Cloud Service CDN を考慮に入れます。 サービスエッジ監視では、選択した地域に近い 5 つの異なる場所を採用し、定期的に可用性を確認します。 サイトの利用不能トリガーが警告を発し、Adobeのオンコールサポートチームとプロセスに関与します。

### カスタム監視 {#custom-monitoring}

カスタム監視機能を使用すると、お客様はオプションで以前に最大 5 つの個別 Web プロパティ URL を指定できます。 [運行中](/help/journey-migration/go-live.md). これらの URL は有効で、かつ HTTP 200 応答コードを返す必要があります。 これらのモニタは、 [独自の CDN を持ち込む](/help/implementing/dispatcher/cdn.md#point-to-point-CDN) Adobeの管理下にないAEMas a Cloud Serviceの前で使用される、AdobeCDN と外部トラフィックルーティングの前に。 カスタム監視チェックから生じるアラートは、Adobeのサポートチームとプロセスを引き起こします。

>[!NOTE]
>
> この機能は、 [高度なクラウドサポート。](https://experienceleague.adobe.com/docs/support-resources/data-sheets/overview.html#support-add-ons) ご質問がある場合は、担当のAdobeアカウントチームにお問い合わせください。

## 内部モジュールの監視 {#module-monitoring}

外部可用性はエンドユーザーの監視に焦点を当てていますが、内部モジュールの監視では、アーキテクチャサブシステムが機能やパフォーマンスの低下を伴わずに通常動作しているかどうかを監視します。 問題が発生した場合は、アラートがトリガーされ、障害が発生した可用性を防ぐために、自動的にまたはオペレーションチームの関与を通じて修復を実行できます。 モニターには様々なカテゴリがあります。以下にチェックの例をいくつか示します。

* CPU iowait の割合が特定のしきい値を超えていません。
* インスタンスの再デプロイメントが一定の頻度を超えていません。
* ディスク使用量が特定のしきい値を下回っています。
* オーサーリポジトリのサイズが特定の範囲内です。
* バックアップ操作が正常に完了しました。
* データベースの正常性とパフォーマンスが監視されます。
* AEM Cloud Services は、ブロックされたレプリケーションキューや整合性の取れたデータ、パフォーマンスの高いクエリを含め、期待どおりに動作しています。

Forms 用にプロビジョニングされた環境に対して、チェックが追加されます。 チェック定義は静的ではなく、変更や更新の対象となります。

## 顧客の可観測性 {#customer-observability}

お客様は、 [New Relic Application Performance Monitoring](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/user-access-new-relic.html?lang=ja) 分析やトラブルシューティングのために収集され、グラフ化されたリアルタイムのパフォーマンスデータを提供するスイート。 監視スイートを使用すると、お客様は次のような様々な指標を直接監視できます。JVM パフォーマンス指標、Java™のトランザクション時間、バックグラウンド外部呼び出し、およびデータベース呼び出し。

## その他のリソース {#resources}

* [New Relic アプリケーションパフォーマンス監視](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/user-access-new-relic.html?lang=ja)
* [AEM as a Cloud Service のログ](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/developing/logging.html?lang=ja)
* [環境の監視](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/content/using/monitoring-environments.html?lang=ja)
