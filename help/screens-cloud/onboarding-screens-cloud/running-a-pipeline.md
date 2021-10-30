---
title: パイプラインの実行
description: ここでは、Cloud Manager で Screens as Cloud Service プロジェクトのパイプラインを実行する方法について説明します。
source-git-commit: b9b27c09b1f4a1799a8c974dfb846295664be998
workflow-type: ht
source-wordcount: '320'
ht-degree: 100%

---


# Cloud Manager での Screens as Cloud Service のパイプラインの実行 {#run-pipeline-screens-cloud}

ここでは、パイプラインを実行し、Cloud Manager でプログラムのコードをデプロイする方法について説明します。

>[!NOTE]
>Cloud Manager でプログラムのパイプラインを実行する方法については、[CD-CD パイプラインの設定](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/configure-pipeline.html?lang=ja)および[コードのデプロイ](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/deploy-code.html?lang=ja)を参照してください。

## 目的 {#objective}

以下の節では、CI/CD パイプラインを設定し、Cloud Manager でプログラムのコードをデプロイする方法について説明します。

## Cloud Manager で Screens プロジェクトのパイプラインを実行する手順 {#steps-branch-creation}

1. 環境の設定が正常に完了したら、Cloud Manager の&#x200B;**概要**&#x200B;ページのコールトゥアクションカードがアップデートされます。

   ![画像](/help/screens-cloud/assets/onboarding/add-environ3.png)

1. **概要**&#x200B;ページで「**パイプラインを設定**」をクリックします。

1. 分岐を選択した後、「**次へ**」をクリックします。

   ![画像](/help/screens-cloud/assets/onboarding/run-pipeline1.png)

1. **パイプラインを設定**&#x200B;ウィザードのオプションを選択します。「**保存**」をクリックします。

   >[!NOTE]
   >パイプラインを設定ウィザードのオプションについて詳しくは、 [Cloud Manager からのパイプライン設定の指定](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/configure-pipeline.html?lang=ja)を参照してください。

   ![画像](/help/screens-cloud/assets/onboarding/run-pipeline2-a.png)

1. セットアップパイプラインが完了すると、コールトゥアクションカードがアップデートされます（下図を参照）。「デプロイ」をクリックします。

   >[!NOTE]
   >Cloud Manager でのデプロイメントの段階について詳しくは、[コードのデプロイ](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/deploy-code.html?lang=ja)を参照してください。

   ![画像](/help/screens-cloud/assets/onboarding/run-pipeline3.png)

1. 「**ビルド**」をクリックしてビルドプロセスを開始します。

   ![画像](/help/screens-cloud/assets/onboarding/run-pipeline4.png)

1. ビルドプロセスが完了すると、Cloud Manager の&#x200B;**概要**&#x200B;ページの&#x200B;**環境**&#x200B;カードにオーサーリンクが表示されます。

   ![画像](/help/screens-cloud/assets/onboarding/run-pipeline5.png)

## 次の手順 {#whats-next}

Cloud Manager でプログラムの環境を設定する方法を学習したら、オンボーディングプロセスの次の手順（[Screens サービスプロバイダー](/help/screens-cloud/configuring/navigating-to-screens-services-provider.md)への移動）に進む準備が整いました。