---
title: Cloud Acceleration Manager での実装フェーズ
description: このページでは、Cloud Acceleration Manager における実装フェーズの概要について説明します。
exl-id: e6ac88f0-4b3f-43a1-98bc-8c6608713784
feature: Migration
role: Admin
source-git-commit: f86d681c8f8cb6d602058ef30b648c53ff7bad69
workflow-type: tm+mt
source-wordcount: '648'
ht-degree: 93%

---

# Cloud Acceleration Manager での実装フェーズ {#implementation-phase-cam}

実装フェーズには以下が含まれます。

* [ローカル開発](#local-development)
* [コードリファクタリング](#code-refactoring)
* [AEM as a Cloud Service デプロイメント](#aem-as-a-cloud-service-deployment)
* [コンテンツ転送](#content-transfer)


プロジェクトカードをクリックしてプロジェクトのランディングページを開き、「**実装**」セクションに移動します（下図を参照）。

![&#x200B; プロジェクトランディングページ – 実装 &#x200B;](/help/journey-migration/cloud-acceleration-manager/assets/implementation-1.png)

>[!NOTE]
>詳しくは、[Cloud Acceleration Manager でのプロジェクトの作成と管理](getting-started-cam.md#create-project)を参照してください。


## ローカル開発カードの使用 {#local-development}

ローカル開発カードには、移行ジャーニーの実装フェーズを開始する際に、ローカル AEM 開発環境のセットアップに役立つ、すべての関連コンテンツが用意されています。

この節では、「ローカル開発」アクティビティカードについて説明します。

1. **ローカル開発**&#x200B;カードの「**表示**」をクリックします。

   ![ローカル開発カード &#x200B;](/help/journey-migration/cloud-acceleration-manager/assets/implementation-2.png)

1. コンテンツカルーセルには、移行ジャーニーのこのフェーズに関係のある情報が表示されます。

   ![ローカル開発カルーセル &#x200B;](/help/journey-migration/cloud-acceleration-manager/assets/implementation-3.png)


## コードリファクタリングカードの使用 {#code-refactoring}

「コードリファクタリング」アクティビティカードには、すべての関連情報が表示され、AEM as a Cloud Service への移行時に確認して解決する必要があるコードリファクタリング領域がハイライト表示されます。

この節では、「コードリファクタリング」アクティビティカードについて説明します。

1. **コードリファクタリング**&#x200B;アクティビティカードの「**レビュー**」をクリックします。

   ![&#x200B; コードリファクタリングカード &#x200B;](/help/journey-migration/cloud-acceleration-manager/assets/implementation-4.png)

1. このページには、コードリファクタリングアクティビティのリストが重大度レベル別に表示されます。ハイライト表示された 2 つのアイコンをクリックすると、詳細を確認できます。

   このページには、コードリファクタリングの考慮事項が次の 3 つのタブに表示されます。

   * 概要
   * Dispatcher
   * テスト

>[!NOTE]
>これらのタブに表示される内容を確認して、ベストプラクティスアナライザーで扱われていないその他の領域についても把握してください。

「**Dispatcher**」タブでは、AEM as a Cloud Service の Apache および Dispatcher の設定を構築する方法と、クラウド環境にデプロイする前にローカルで検証および実行する方法に関する情報が表示されます。また、クラウド環境でのデバッグについても説明します。

![&#x200B; 「Dispatcher」タブ &#x200B;](/help/journey-migration/cloud-acceleration-manager/assets/coderefactoring-2.png)

「**テスト**」タブには、機能テスト、エクスペリエンス監査、UI テストに関する情報が表示されます。

![&#x200B; 「テスト」タブ &#x200B;](/help/journey-migration/cloud-acceleration-manager/assets/coderefactoring-3.png)


## AEM as a Cloud Service デプロイメントカードの使用 {#aem-as-a-cloud-service-deployment}

AEM as a Cloud Service デプロイメントカードには、コードを AEM as a Cloud Service にデプロイするのに役立つ、関係のあるすべてのコンテンツが用意されています。

この節では、「AEM as a Cloud Service デプロイメント」アクティビティカードについて説明します。

1. **AEM as a Cloud Service デプロイメント**&#x200B;カードの「**表示**」をクリックします。

   ![AEM as a Cloud Service デプロイメント – カード &#x200B;](/help/journey-migration/cloud-acceleration-manager/assets/implementation-6.png)

1. コンテンツカルーセルには、移行ジャーニーのこのフェーズに関係のある情報が表示されます。

   ![AEM as a Cloud Service デプロイメント – カルーセル &#x200B;](/help/journey-migration/cloud-acceleration-manager/assets/aem-deployment-card.png)


## コンテンツ転送カードの使用 {#content-transfer}

コンテンツ転送カードを使用すると、現在の AEM インスタンスから AEM as a Cloud Service へのコンテンツ転送を開始および管理できます。

この節では、「コンテンツ転送」アクティビティカードについて説明します。

1. **コンテンツ転送**&#x200B;アクティビティカードの「**レビュー**」をクリックします。

   ![&#x200B; コンテンツ転送 – レビュー &#x200B;](/help/journey-migration/cloud-acceleration-manager/assets/contenttransfer-1.png)

1. コンテンツの転送を開始するには、移行セットを作成する必要があります。「**移行セットを作成**」をクリックします。移行セットを使用すると、コンテンツを AEM as a Cloud Service に転送できます。

   ![&#x200B; 移行セットを作成 &#x200B;](/help/journey-migration/cloud-acceleration-manager/assets/contenttransfer-2.png)

   >[!NOTE]
   >移行セットは、無操作状態が長時間続くと有効期限が切れます。詳しくは、[移行セットの有効期限](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/overview-content-transfer-tool.md#migration-set-expiry)を参照してください。

   >[!NOTE]
   >コンテンツ転送ツールを使用する前に、[前提条件](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/content-transfer-tool/prerequisites-content-transfer-tool.html?lang=ja)および[ベストプラクティスとガイドライン](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/content-transfer-tool/overview-content-transfer-tool.html?lang=ja)を確認してください。

1. 移行セットに入力し、コンテンツ転送の抽出段階を完了するには、コンテンツ転送ツールをダウンロードしてインストールする必要があります。[コンテンツ転送ツールの概要](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/content-transfer-tool/getting-started-content-transfer-tool.html?lang=ja)を参照して、コンテンツ転送ツールの使用方法を確認してください。

1. 移行セットから AEM as a Cloud Service 上の環境にコンテンツを取り込むには、取り込みを開始する必要があります。**取り込みジョブ**&#x200B;に移動し、「**新しい取り込み**」をクリックします。[Target へのコンテンツの取り込み](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/ingesting-content.md)を参照して、コンテンツ転送の取り込みフェーズを完了する方法を確認してください。

   ![&#x200B; 取り込みジョブ &#x200B;](/help/journey-migration/cloud-acceleration-manager/assets/contenttransfer-3.png)

<!--### Estimating Content Transfer Time {#calculating}

A Content Transfer Tool calculator has been provided to estimate how long it could take to complete the content transfer activity. You can use the content repository size slider to select the size that applies to your project. The transfer times vary for the extraction and ingestion phases. 

   ![Content Transfer Tool calculator](/help/journey-migration/cloud-acceleration-manager/assets/contenttransfer-4.png)

   >[!NOTE]
   >These times are estimates only. Factor such as network speeds and time to scale up instances have not been accounted for in these estimates.

To estimate the size of the AEM Repository, you can run the Disk Usage report under `http://HOST:PORT/etc/reports/diskusage.html`. 

You can also estimate the size of specific repository paths by using the `path` parameter, for example, `http://HOST:PORT/etc/reports/diskusage.html?path=/content/dam`. -->

## 次の手順 {#whats-next}

Cloud Acceleration Manager へのログオン方法と実装フェーズの利用方法を理解したら、次の手順の[運用開始フェーズ](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-acceleration-manager/using-cam/cam-golive-phase.html?lang=ja)に進みます。
