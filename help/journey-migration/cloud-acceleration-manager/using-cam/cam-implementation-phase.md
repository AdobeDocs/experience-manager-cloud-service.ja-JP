---
title: Cloud Acceleration Manager での実装フェーズ
description: このページでは、Cloud Acceleration Manager における実装フェーズの概要について説明します。
exl-id: e6ac88f0-4b3f-43a1-98bc-8c6608713784
source-git-commit: 5ad33f0173afd68d8868b088ff5e20fc9f58ad5a
workflow-type: tm+mt
source-wordcount: '661'
ht-degree: 32%

---

# Cloud Acceleration Manager での実装フェーズ {#implementation-phase-cam}

実装フェーズには以下が含まれます。

* [ローカル開発](#local-development)
* [コードリファクタリング](#code-refactoring)
* [AEM as a Cloud Service デプロイメント](#aem-as-a-cloud-service-deployment)
* [コンテンツ転送](#content-transfer)


プロジェクトカードをクリックして、プロジェクトのランディングページを開き、 **実装** を参照してください。

![画像](/help/journey-migration/cloud-acceleration-manager/assets/implementation-1.png)

>[!NOTE]
>詳しくは、 [Cloud Acceleration Manager でのプロジェクトの作成と管理](getting-started-cam.md#create-project) を参照してください。


## ローカル開発カードの使用 {#local-development}

「ローカル開発」カードには、移行ジャーニーの実装段階を開始する際に、ローカルAEM開発環境の設定に役立つ、すべての関連コンテンツが表示されます。

このセクションでは、ローカル開発アクティビティカードを参照できます。

1. クリック **表示** から **ローカル開発** カード。

   ![画像](/help/journey-migration/cloud-acceleration-manager/assets/implementation-2.png)

1. コンテンツカルーセルには、移行ジャーニーのこのフェーズに関係のある情報が表示されます。

   ![画像](/help/journey-migration/cloud-acceleration-manager/assets/implementation-3.png)


## コードリファクタリングカードの使用 {#code-refactoring}

「コードリファクタリング」アクティビティカードは、すべての関連情報を提供し、AEM as a Cloud Serviceに移行する際に確認および解決するコードリファクタリング領域を強調表示します。

この節では、コードリファクタリングアクティビティカードを確認できます。

1. クリック **レビュー** から **コードリファクタリング** アクティビティカード。

   ![画像](/help/journey-migration/cloud-acceleration-manager/assets/implementation-4.png)

1. このページには、コードリファクタリングアクティビティのリストが重大度レベル別に表示されます。ハイライト表示された 2 つのアイコンをクリックすると、詳細を確認できます。

   このページには、コードリファクタリングの考慮事項が次の 3 つのタブに表示されます。

   * 概要
   * Dispatcher
   * テスト

>[!NOTE]
>これらのタブの内容を確認して、ベストプラクティスアナライザーで扱われないその他の領域を理解します。

The **Dispatcher** 「 」タブには、AEMas a Cloud Serviceの Apache および Dispatcher 設定を構築する方法と、クラウド環境にデプロイする前にローカルで検証および実行する方法に関する情報が表示されます。 また、クラウド環境でのデバッグについても説明します。

![画像](/help/journey-migration/cloud-acceleration-manager/assets/coderefactoring-2.png)

「**テスト**」タブには、機能テスト、エクスペリエンス監査、UI テストに関する情報が表示されます。

![画像](/help/journey-migration/cloud-acceleration-manager/assets/coderefactoring-3.png)


## AEM as a Cloud Service デプロイメントカードの使用 {#aem-as-a-cloud-service-deployment}

AEMas a Cloud Service的デプロイメントカードは、コードをAEM as a Cloud Serviceにデプロイする際に役立つ、すべての関連コンテンツを提供します。

この節に従って、AEMas a Cloud Serviceデプロイメントカードのアクティビティカードを参照できます。

1. クリック **表示** から **AEMas a Cloud Serviceデプロイメント** アクティビティカード。

   ![画像](/help/journey-migration/cloud-acceleration-manager/assets/implementation-6.png)

1. コンテンツカルーセルには、移行ジャーニーのこのフェーズに関係のある情報が表示されます。

   ![画像](/help/journey-migration/cloud-acceleration-manager/assets/aem-deployment-card.png)


## コンテンツ転送カードの使用 {#content-transfer}

「コンテンツ転送」カードを使用すると、現在のAEMインスタンスからAEM as a Cloud Serviceへのコンテンツ転送を開始および管理できます。

このセクションに従って、コンテンツ転送アクティビティカードを参照します。

1. クリック **レビュー** から **コンテンツ転送** アクティビティカード。

   ![画像](/help/journey-migration/cloud-acceleration-manager/assets/contenttransfer-1.png)

1. コンテンツの転送を開始するには、移行セットを作成する必要があります。 クリック **移行セットを作成**. 移行セットを使用すると、コンテンツを AEM as a Cloud Service に転送できます。

   ![画像](/help/journey-migration/cloud-acceleration-manager/assets/contenttransfer-2.png)

   >[!NOTE]
   >移行セットは、無操作状態が長時間続くと有効期限が切れます。 詳しくは、 [移行セットの有効期限](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/overview-content-transfer-tool.md#migration-set-expiry) 」を参照してください。

   >[!NOTE]
   >詳しくは、 [前提条件](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/content-transfer-tool/prerequisites-content-transfer-tool.html?lang=ja) そして [ベストプラクティスとガイドライン](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/content-transfer-tool/overview-content-transfer-tool.html?lang=ja) コンテンツ転送ツールを使用する前に

1. コンテンツ転送ツールをダウンロードしてインストールし、移行セットに入力して、コンテンツ転送の抽出段階を完了します。 [コンテンツ転送ツールの概要](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/content-transfer-tool/getting-started-content-transfer-tool.html?lang=ja)を参照して、コンテンツ転送ツールの使用方法を確認してください。

1. 移行セットからAEM as a Cloud Service上の環境にコンテンツを取り込むには、取り込みを開始する必要があります。 に移動します。 **取り込みジョブ** をクリックします。 **新しい取り込み**. レビュー [Target へのコンテンツの取り込み](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/content-transfer-tool/ingesting-content.html?lang=ja) そのため、コンテンツ転送のインジェスト段階を完了する方法を学ぶことができます。

   ![画像](/help/journey-migration/cloud-acceleration-manager/assets/contenttransfer-3.png)

<!--### Estimating Content Transfer Time {#calculating}

A Content Transfer Tool calculator has been provided to estimate how long it could take to complete the content transfer activity. You can use the content repository size slider to select the size that applies to your project. The transfer times vary for the extraction and ingestion phases. 

   ![image](/help/journey-migration/cloud-acceleration-manager/assets/contenttransfer-4.png)

   >[!NOTE]
   >These times are estimates only. Factor such as network speeds and time to scale up instances have not been accounted for in these estimates.

To estimate the size of the AEM Repository, you can run the Disk Usage report under `http://HOST:PORT/etc/reports/diskusage.html`. 

You can also estimate the size of specific repository paths by using the `path` parameter, for example, `http://HOST:PORT/etc/reports/diskusage.html?path=/content/dam`. -->

## 次の手順 {#whats-next}

Cloud Acceleration Manager へのログオン方法と実装段階の使用方法を学習したら、次の手順 ( [Go Live フェーズ](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-acceleration-manager/using-cam/cam-golive-phase.html).
