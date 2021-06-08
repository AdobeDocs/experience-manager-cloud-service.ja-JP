---
title: パイプラインの実行
description: ここでは、Cloud ManagerでScreensのパイプラインをCloud Serviceプロジェクトとして実行する方法について説明します。
hide: true
hidefromtoc: true
index: false
source-git-commit: 371cfaeb0e526197fdf98dea65ed5bc2ca0481a2
workflow-type: tm+mt
source-wordcount: '320'
ht-degree: 7%

---


# Cloud ManagerでのCloud ServiceプログラムとしてのScreensのパイプラインの実行{#run-pipeline-screens-cloud}

ここでは、パイプラインを実行し、Cloud Managerでプログラムのコードをデプロイする方法について説明します。

>[!NOTE]
>Cloud Managerでプログラムのパイプラインを実行する方法については、 [CD-CDパイプラインの設定](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/configure-pipeline.html?lang=en)および[コードのデプロイ](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/deploy-code.html?lang=ja)を参照してください。

## 目的 {#objective}

以下の節では、CI/CDパイプラインの設定方法と、Cloud Managerでプログラムのコードのデプロイ方法について説明します。

## Cloud ManagerでScreensプロジェクトのパイプラインを実行する手順{#steps-branch-creation}

1. 環境の設定が正常に完了したら、Cloud Managerの&#x200B;**概要**&#x200B;ページにコールトゥアクションカードの更新が表示されます。

   ![画像](/help/screens-cloud/assets/onboarding/add-environ3.png)

1. **概要**&#x200B;ページで「**パイプラインを設定**」をクリックします。

1. 分岐を選択した後、「**次へ**」をクリックします。

   ![画像](/help/screens-cloud/assets/onboarding/run-pipeline1.png)

1. **パイプラインの設定**&#x200B;ウィザードからオプションを選択します。 「**保存**」をクリックします。

   >[!NOTE]
   >パイプラインを設定ウィザードのオプションについて詳しくは、 [Cloud Managerからのパイプライン設定の指定](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/configure-pipeline.html?lang=en)を参照してください。

   ![画像](/help/screens-cloud/assets/onboarding/run-pipeline2-a.png)

1. セットアップパイプラインが完了すると、コールトゥアクションカードが更新されます（下図を参照）。 「デプロイ」をクリックします。

   >[!NOTE]
   >Cloud Managerでのデプロイメントの段階について詳しくは、 [コードのデプロイ](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/deploy-code.html?lang=en)を参照してください。

   ![画像](/help/screens-cloud/assets/onboarding/run-pipeline3.png)

1. 「**ビルド**」をクリックして、ビルドプロセスを開始します。

   ![画像](/help/screens-cloud/assets/onboarding/run-pipeline4.png)

1. ビルドプロセスが完了すると、Cloud Managerの&#x200B;**概要**&#x200B;ページの&#x200B;**環境**&#x200B;カードからオーサーリンクが表示されます。

   ![画像](/help/screens-cloud/assets/onboarding/run-pipeline5.png)

## 次の手順{#whats-next}

Cloud Managerでプログラムのパイプラインを実行する方法を学習したら、次の手順に進む準備が整いました。 次の手順は、 Screensプロジェクトの設定と設定です。