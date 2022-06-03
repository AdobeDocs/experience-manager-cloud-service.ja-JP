---
title: Cloud Acceleration Manager での実装フェーズ
description: このページでは、Cloud Acceleration Manager における実装フェーズの概要について説明します。
exl-id: e6ac88f0-4b3f-43a1-98bc-8c6608713784
source-git-commit: f2cad442ba85d1d889eda669502e120406a4380b
workflow-type: tm+mt
source-wordcount: '793'
ht-degree: 75%

---

# Cloud Acceleration Manager での実装フェーズ {#implementation-phase-cam}

実装フェーズには以下が含まれます。

* [ローカル開発](#local-development)
* [コードリファクタリング](#code-refactoring)
* [AEM as a Cloud Service デプロイメント](#aem-as-a-cloud-service-deployment)
* [コンテンツ転送](#content-transfer)


プロジェクトカードをクリックしてプロジェクトのランディングページを開き、「**実装**」セクションに移動します（下図を参照）。

![画像](/help/journey-migration/cloud-acceleration-manager/assets/implementation-1.png)

>[!NOTE]
>詳しくは、[Cloud Acceleration Manager でのプロジェクトの作成と管理](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-acceleration-manager/using-cam/getting-started-cam.html?lang=ja#create-project)を参照してください。


## ローカル開発カードの使用 {#local-development}

ローカル開発カードには、移行ジャーニーの実装フェーズを開始する際に、ローカル AEM 開発環境のセットアップに役立つ、すべての関連コンテンツが用意されています。

この節では、「ローカル開発」アクティビティカードについて説明します。

1. **ローカル開発**&#x200B;カードの「**表示**」ボタンをクリックします。

   ![画像](/help/journey-migration/cloud-acceleration-manager/assets/implementation-2.png)

1. コンテンツカルーセルには、移行ジャーニーのこのフェーズに関係のある情報が表示されます。

   ![画像](/help/journey-migration/cloud-acceleration-manager/assets/implementation-3.png)


## コードリファクタリングカードの使用 {#code-refactoring}

「コードリファクタリング」アクティビティカードには、すべての関連情報が表示され、AEM as a Cloud Service への移行時に確認して解決する必要があるコードリファクタリング領域がハイライト表示されます。

この節では、「コードリファクタリング」アクティビティカードについて説明します。

1. **コードリファクタリング**&#x200B;アクティビティカードの「**レビュー**」ボタンをクリックします。

   ![画像](/help/journey-migration/cloud-acceleration-manager/assets/implementation-4.png)

1. このページには、コードリファクタリングアクティビティのリストが重大度レベル別に表示されます。ハイライト表示された 2 つのアイコンをクリックすると、詳細を確認できます。

   このページには、コードリファクタリングの考慮事項が次の 3 つのタブに表示されます。

   * 概要
   * Dispatcher
   * テスト

>[!NOTE]
>これらのタブに表示される内容を確認して、ベストプラクティスアナライザーで扱われていないその他の領域についても把握してください。

「**Dispatcher**」タブでは、AEM as a Cloud Service の Apache および Dispatcher の設定を構築する方法と、クラウド環境にデプロイする前にローカルで検証および実行する方法に関する情報が表示されます。また、クラウド環境でのデバッグについても説明します。

![画像](/help/journey-migration/cloud-acceleration-manager/assets/coderefactoring-2.png)

「**テスト**」タブには、機能テスト、エクスペリエンス監査、UI テストに関する情報が表示されます。

![画像](/help/journey-migration/cloud-acceleration-manager/assets/coderefactoring-3.png)


## AEM as a Cloud Service デプロイメントカードの使用 {#aem-as-a-cloud-service-deployment}

AEM as a Cloud Service デプロイメントカードには、コードを AEM as a Cloud Service にデプロイするのに役立つ、関係のあるすべてのコンテンツが用意されています。

この節では、「AEM as a Cloud Service デプロイメント」アクティビティカードについて説明します。

1. **AEM as a Cloud Service デプロイメント**&#x200B;カードの「**表示**」ボタンをクリックします。

   ![画像](/help/journey-migration/cloud-acceleration-manager/assets/implementation-6.png)

1. コンテンツカルーセルには、移行ジャーニーのこのフェーズに関係のある情報が表示されます。

   ![画像](/help/journey-migration/cloud-acceleration-manager/assets/aem-deployment-card.png)


## コンテンツ転送カードの使用 {#content-transfer}

「コンテンツ転送」カードを使用すると、現在のAEMインスタンスからAEM as a Cloud Serviceへのコンテンツ転送を開始および管理できます。

この節では、「コンテンツ転送」アクティビティカードについて説明します。

1. をクリックします。 **レビュー** ボタン **コンテンツ転送** アクティビティカード。

   ![画像](/help/journey-migration/cloud-acceleration-manager/assets/contenttransfer-1.png)

1. コンテンツの転送を開始するには、移行セットを作成する必要があります。 クリック **移行セットを作成**. 移行セットを使用すると、コンテンツをAEM as a Cloud Serviceに転送できます。

   ![画像](/help/journey-migration/cloud-acceleration-manager/assets/contenttransfer-2.png)

   >[!NOTE]
   >コンテンツ転送ツールを使用する前に、[前提条件](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/prerequisites-content-transfer-tool.html?lang=ja)および[ベストプラクティスとガイドライン](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/overview-content-transfer-tool.html?lang=ja)を確認してください。

1. 移行セットに入力し、コンテンツ転送の抽出段階を完了するには、コンテンツ転送ツールをダウンロードしてインストールする必要があります。 レビュー [コンテンツ転送ツールの概要](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/content-transfer-tool/getting-started-content-transfer-tool.html?lang=en) を参照して、コンテンツ転送ツールの使用方法を確認してください。

1. 移行セットからAEM as a Cloud Service上の環境にコンテンツを取り込むには、取り込みを開始する必要があります。 に移動します。 **取り込みジョブ** をクリックし、 **新しい取り込み**. レビュー [Target へのコンテンツの取り込み](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/content-transfer-tool/ingesting-content.html?lang=en) を参照して、コンテンツ転送のインジェスト段階を完了する方法を確認してください。

   ![画像](/help/journey-migration/cloud-acceleration-manager/assets/contenttransfer-3.png)

### コンテンツ転送時間の推定 {#calculating}

コンテンツ転送ツールの計算ツールが提供され、コンテンツ転送アクティビティの完了に要する時間を見積もることができます。 コンテンツリポジトリーのサイズスライダーを使用して、プロジェクトに当てはまるサイズを選択できます。転送時間は、抽出段階と取り込み段階で異なります。

![画像](/help/journey-migration/cloud-acceleration-manager/assets/contenttransfer-4.png)

>[!NOTE]
>この時間は推定値に過ぎません。ネットワーク速度やインスタンスの規模拡大に要する時間などの要因は、これらの推定では考慮されていません。

AEM リポジトリーのサイズを推定するには、`http://HOST:PORT/etc/reports/diskusage.html` のディスク使用状況レポートを実行します。

`path` パラメーターを使用して（例：`http://HOST:PORT/etc/reports/diskusage.html?path=/content/dam`）、特定のリポジトリーパスのサイズを推定することもできます。

## 次の手順 {#whats-next}

Cloud Acceleration Manager へのログイン方法と実装フェーズの利用方法を理解したら、次のステップの[運用開始フェーズ](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-acceleration-manager/using-cam/cam-golive-phase.html?lang=ja)に進みます。
