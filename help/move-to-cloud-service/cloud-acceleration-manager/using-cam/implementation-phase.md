---
title: Cloud Acceleration Managerの実装段階
description: このページでは、Cloud Acceleration Managerの実装フェーズの概要を説明します。
hide: true
hidefromtoc: true
index: false
source-git-commit: 8641c14114c5f1f2f69a3a1b51eac38ab6f4f541
workflow-type: tm+mt
source-wordcount: '563'
ht-degree: 2%

---


# Cloud Acceleration Managerの実装フェーズ{#implementation-phase-cam}

実装フェーズには、以下が含まれます。

* [ローカル開発](#local-development)
* [コードリファクタリング](#code-refactoring)
* [AEM as a Cloud Serviceのデプロイメント](#aem-as-a-cloud-service-deployment)
* [コンテンツ転送](#content-transfer)


プロジェクトカードをクリックしてプロジェクトのランディングページを開き、以下の図に示すように、「**実装**」セクションに移動します。

![画像](/help/move-to-cloud-service/cloud-acceleration-manager/assets/implementation-1.png)

>[!NOTE]
>詳しくは、 Cloud Acceleration Managerの[プロジェクトの作成と管理](/help/move-to-cloud-service/cloud-acceleration-manager/using-cam/getting-started-cam.md)を参照してください。


## ローカル開発カード{#local-development}の使用

ローカル開発カードには、移行ジャーニーの実装段階を開始する際に、ローカルAEM開発環境の設定に役立つ、すべての関連コンテンツが用意されています。

この節では、「ローカル開発」アクティビティカードについて説明します。

1. **ローカル開発**&#x200B;カードの&#x200B;**表示**&#x200B;ボタンをクリックします。

   ![画像](/help/move-to-cloud-service/cloud-acceleration-manager/assets/implementation-2.png)

1. 移行ジャーニーのこのフェーズに関連する情報を含むコンテンツカルーセルが表示されます。

   ![画像](/help/move-to-cloud-service/cloud-acceleration-manager/assets/implementation-3.png)


## コードリファクタリングカード{#code-refactoring}の使用

「コードリファクタリング」アクティビティカードは、すべての関連情報を提供し、AEMをCloud Serviceとして移行する際に確認する必要があるコードリファクタリング領域を強調表示します。

この節では、コードリファクタリングアクティビティカードについて説明します。

1. 「**コードリファクタリング**」アクティビティカードの「**レビュー**」ボタンをクリックします。

   ![画像](/help/move-to-cloud-service/cloud-acceleration-manager/assets/implementation-4.png)

1. このページには、重大度レベル別に整理されたコードリファクタリングアクティビティのリストが表示されます。 ハイライト表示された2つのアイコンをクリックすると、詳細を確認できます。

   >[!NOTE]
   >さらに、ページのタブの内容を確認して、ベストプラクティスアナライザーで扱われていないその他の領域について理解してください。

   ![画像](/help/move-to-cloud-service/cloud-acceleration-manager/assets/readiness-5.png)


## AEM as a Cloud Serviceデプロイメントカード{#aem-as-a-cloud-service-deployment}の使用

AEM as a Cloud Serviceデプロイメントカードは、コードをAEM as aCloud Serviceにデプロイするのに役立つ、すべての関連コンテンツを提供します。

この節では、 AEM as a Cloud Serviceデプロイメントカードのアクティビティカードを確認します。

1. **AEM as a Cloud Service Deployment**&#x200B;アクティビティカードの「**View**」ボタンをクリックします。

   ![画像](/help/move-to-cloud-service/cloud-acceleration-manager/assets/implementation-6.png)

1. 移行ジャーニーのこのフェーズに関連する情報を含むコンテンツカルーセルが表示されます。

   ![画像](/help/move-to-cloud-service/cloud-acceleration-manager/assets/implementation-7.png)


## コンテンツ転送カード{#content-transfer}の使用

コンテンツ転送アクティビティカードは、コンテンツ転送ツールを使用して現在のAEMインスタンスからAEMにCloud Serviceとしてコンテンツを移動する場合に確認する必要があるガイダンスと考慮事項を提供します。

この節では、コンテンツ転送アクティビティカードについて説明します。

1. **コンテンツ転送**&#x200B;アクティビティカードの「**表示**」ボタンをクリックします。

   ![画像](/help/move-to-cloud-service/cloud-acceleration-manager/assets/implementation-8.png)

1. 移行ジャーニーのこのフェーズに関連する情報を含むコンテンツカルーセルが表示されます。

   ![画像](/help/move-to-cloud-service/cloud-acceleration-manager/assets/implementation-9.png)

   >[!NOTE]
   >コンテンツ転送ツールを使用する前に、[前提条件](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/prerequisites-content-transfer-tool.html?lang=en)と[ベストプラクティスとガイドライン](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/overview-content-transfer-tool.html?lang=en)を確認してください。

### コンテンツ転送ツールアクティビティの見積もり {#calculating}

コンテンツ転送アクティビティの完了に要する時間を見積もるための新しいコンテンツ転送ツール計算ツールが提供されました。 コンテンツリポジトリのサイズスライダーを使用して、プロジェクトに適用するサイズを選択できます。 転送時間は、抽出段階とインジェスト段階によって異なります。

AEMリポジトリのサイズを見積もるには、`http://HOST:PORT/etc/reports/diskusage.html`の下でDisk Usage Reportを実行します。

`path`パラメーター（例：`http://HOST:PORT/etc/reports/diskusage.html?path=/content/dam`）を使用して、特定のリポジトリパスのサイズを予測することもできます。

## 次の手順{#whats-next}

Cloud Acceleration Managerへのログイン方法と実装段階の利用方法を学習したら、次の手順(GoLive段階の使用)を確認する準備が整いました。
