---
title: パイプラインの実行
description: ここでは、Cloud Manager で Screens as Cloud Service プロジェクトのパイプラインを実行する方法について説明します。
exl-id: 3203cff7-5668-4f50-a2c5-80ae474b439d
source-git-commit: 1994b90e3876f03efa571a9ce65b9fb8b3c90ec4
workflow-type: tm+mt
source-wordcount: '309'
ht-degree: 39%

---

# Cloud Manager での Screens as Cloud Service のパイプラインの実行 {#run-pipeline-screens-cloud}

ここでは、パイプラインを実行し、Cloud Manager でプログラムのコードをデプロイする方法について説明します。

>[!NOTE]
>詳しくは、 [CI/CD パイプラインの設定](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/cicd-pipelines/configuring-production-pipelines.html?lang=en) および [コードのデプロイ](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/deploy-code.html?lang=ja) を参照して、Cloud Manager でプログラムのパイプラインを実行する方法を確認してください。

## 目的 {#objective}

以下の節では、CI/CD パイプラインを設定し、Cloud Manager でプログラムのコードをデプロイする方法について説明します。

## Cloud Manager で Screens プロジェクトのパイプラインを実行する手順 {#steps-branch-creation}

1. 環境の設定が正常に完了すると、Cloud Manager の **概要** ページ。

   ![画像](/help/screens-cloud/assets/onboarding/add-environ3.png)

1. クリック **パイプラインを設定** から **概要** ページ。

1. クリック **次へ** 分岐を選択した後で、

   ![画像](/help/screens-cloud/assets/onboarding/run-pipeline1.png)

1. **パイプラインを設定**&#x200B;ウィザードのオプションを選択します。「**保存**」をクリックします。

   >[!NOTE]
   >パイプライン設定ウィザードのオプションについては、 [Cloud Manager からのパイプライン設定の指定](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/cicd-pipelines/configuring-production-pipelines.html?lang=en) を参照してください。

   ![画像](/help/screens-cloud/assets/onboarding/run-pipeline2-a.png)

1. 設定パイプラインが完了したら、コールトゥアクションカードが更新されます。

   >[!NOTE]
   >Cloud Manager でのデプロイメントのステージについて詳しくは、 [コードのデプロイ](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/deploy-code.html?lang=ja) を参照してください。

   ![画像](/help/screens-cloud/assets/onboarding/run-pipeline3.png)

1. クリック **デプロイ**.

1. クリック **ビルド** をクリックして、ビルドプロセスを開始します。

   ![画像](/help/screens-cloud/assets/onboarding/run-pipeline4.png)

1. ビルドプロセスが完了すると、 **環境** Cloud Manager の **概要** ページ。

   ![画像](/help/screens-cloud/assets/onboarding/run-pipeline5.png)

## 次の手順 {#whats-next}

Cloud Manager でプログラムの環境を設定する方法を学習したら、オンボーディングプロセスの次の手順に進む準備が整いました。 [Screens Services Provider への移動](/help/screens-cloud/configuring/navigating-to-screens-services-provider.md).
