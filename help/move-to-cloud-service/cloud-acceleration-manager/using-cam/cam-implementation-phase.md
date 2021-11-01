---
title: Cloud Acceleration Manager での実装フェーズ
description: このページでは、Cloud Acceleration Manager における実装フェーズの概要について説明します。
exl-id: 4ea13f12-7251-448f-9f54-c8d710aef2ba
source-git-commit: e786fe40d97294b4ab5e8657920f2ecbb401d8e9
workflow-type: tm+mt
source-wordcount: '674'
ht-degree: 96%

---

# Cloud Acceleration Manager での実装フェーズ {#implementation-phase-cam}

実装フェーズには以下が含まれます。

* [ローカル開発](#local-development)
* [コードリファクタリング](#code-refactoring)
* [AEM as a Cloud Service デプロイメント](#aem-as-a-cloud-service-deployment)
* [コンテンツ転送](#content-transfer)


プロジェクトカードをクリックしてプロジェクトのランディングページを開き、「**実装**」セクションに移動します（下図を参照）。

![画像](/help/move-to-cloud-service/cloud-acceleration-manager/assets/implementation-1.png)

>[!NOTE]
>詳しくは、[Cloud Acceleration Manager でのプロジェクトの作成と管理](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-acceleration-manager/using-cam/getting-started-cam.html?lang=ja#create-project)を参照してください。


## ローカル開発カードの使用 {#local-development}

ローカル開発カードには、移行ジャーニーの実装フェーズを開始する際に、ローカル AEM 開発環境のセットアップに役立つ、すべての関連コンテンツが用意されています。

この節では、「ローカル開発」アクティビティカードについて説明します。

1. **ローカル開発**&#x200B;カードの「**表示**」ボタンをクリックします。

   ![画像](/help/move-to-cloud-service/cloud-acceleration-manager/assets/implementation-2.png)

1. コンテンツカルーセルには、移行ジャーニーのこのフェーズに関係のある情報が表示されます。

   ![画像](/help/move-to-cloud-service/cloud-acceleration-manager/assets/implementation-3.png)


## コードリファクタリングカードの使用 {#code-refactoring}

「コードリファクタリング」アクティビティカードには、すべての関連情報が表示され、AEM as a Cloud Service への移行時に確認して解決する必要があるコードリファクタリング領域がハイライト表示されます。

この節では、「コードリファクタリング」アクティビティカードについて説明します。

1. **コードリファクタリング**&#x200B;アクティビティカードの「**レビュー**」ボタンをクリックします。

   ![画像](/help/move-to-cloud-service/cloud-acceleration-manager/assets/implementation-4.png)

1. このページには、コードリファクタリングアクティビティのリストが重大度レベル別に表示されます。ハイライト表示された 2 つのアイコンをクリックすると、詳細を確認できます。

   このページには、コードリファクタリングの考慮事項が次の 3 つのタブに表示されます。

   * 概要
   * Dispatcher
   * テスト

>[!NOTE]
>これらのタブの内容を確認し、ベストプラクティスアナライザーで扱われないその他の領域を理解してください。

「**Dispatcher**」タブでは、AEM as a Cloud Service の Apache および Dispatcher の設定を構築する方法と、クラウド環境にデプロイする前にローカルで検証および実行する方法に関する情報が表示されます。また、クラウド環境でのデバッグについても説明します。

![画像](/help/move-to-cloud-service/cloud-acceleration-manager/assets/coderefactoring-2.png)

「**テスト**」タブには、機能テスト、エクスペリエンス監査、UI テストに関する情報が表示されます。

![画像](/help/move-to-cloud-service/cloud-acceleration-manager/assets/coderefactoring-3.png)


## AEM as a Cloud Service デプロイメントカードの使用 {#aem-as-a-cloud-service-deployment}

AEM as a Cloud Service デプロイメントカードには、コードを AEM as a Cloud Service にデプロイするのに役立つ、関係のあるすべてのコンテンツが用意されています。

この節では、「AEM as a Cloud Service デプロイメント」アクティビティカードについて説明します。

1. **AEM as a Cloud Service デプロイメント**&#x200B;カードの「**表示**」ボタンをクリックします。

   ![画像](/help/move-to-cloud-service/cloud-acceleration-manager/assets/implementation-6.png)

1. コンテンツカルーセルには、移行ジャーニーのこのフェーズに関係のある情報が表示されます。

   ![画像](/help/move-to-cloud-service/cloud-acceleration-manager/assets/aem-deployment-card.png)


## コンテンツ転送カードの使用 {#content-transfer}

「コンテンツ転送」アクティビティカードには、コンテンツ転送ツールを使用して現在の AEM インスタンスから AEM as a Cloud Service にコンテンツを移動する際に確認する必要があるガイダンスと考慮事項が表示されます。

この節では、「コンテンツ転送」アクティビティカードについて説明します。

1. **コンテンツ転送**&#x200B;アクティビティカードの「**表示**」ボタンをクリックします。

   ![画像](/help/move-to-cloud-service/cloud-acceleration-manager/assets/implementation-8.png)

1. コンテンツカルーセルには、移行ジャーニーのこのフェーズに関係のある情報が表示されます。

   ![画像](/help/move-to-cloud-service/cloud-acceleration-manager/assets/content-transfertool-card.png)

   >[!NOTE]
   >コンテンツ転送ツールを使用する前に、[前提条件](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/prerequisites-content-transfer-tool.html?lang=ja)および[ベストプラクティスとガイドライン](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/overview-content-transfer-tool.html?lang=ja)を確認してください。

### コンテンツ転送時間の推定 {#calculating}

コンテンツ転送アクティビティの完了に要する時間を推定するための新しいコンテンツ転送計算ツールが用意されました。コンテンツリポジトリーのサイズスライダーを使用して、プロジェクトに当てはまるサイズを選択できます。転送時間は、抽出段階と取り込み段階で異なります。

>[!NOTE]
>この時間は推定値に過ぎません。ネットワーク速度やインスタンスの規模拡大に要する時間などの要因は、これらの推定では考慮されていません。

AEM リポジトリーのサイズを推定するには、`http://HOST:PORT/etc/reports/diskusage.html` のディスク使用状況レポートを実行します。

`path` パラメーターを使用して（例：`http://HOST:PORT/etc/reports/diskusage.html?path=/content/dam`）、特定のリポジトリーパスのサイズを推定することもできます。

## 次の手順 {#whats-next}

Cloud Acceleration Manager へのログイン方法と実装フェーズの利用方法を理解したら、次のステップの[運用開始フェーズ](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-acceleration-manager/using-cam/cam-golive-phase.html?lang=ja)に進みます。
