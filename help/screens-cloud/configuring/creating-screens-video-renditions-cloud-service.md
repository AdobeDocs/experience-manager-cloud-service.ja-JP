---
title: Screens as a Cloud Service でのビデオレンディションの作成
description: ここでは、Screens as a Cloud Service でビデオレンディションを作成する方法について説明します。
exl-id: a9c46036-cd29-47fa-81d9-c865cf22c98a
source-git-commit: d361ddc9a50a543cd1d5f260c09920c5a9d6d675
workflow-type: tm+mt
source-wordcount: '343'
ht-degree: 49%

---

# Screens as a Cloud Service でのビデオレンディションの作成 {#creating-screens-video-renditions}

## はじめに {#introduction}

ここでは、Screens Player で使用するビデオレンディションを作成する方法について説明します。

>[!IMPORTANT]
>Screens チャネルでビデオを使用する場合は、この節で示す手順を設定する必要があります。

## Screens as a Cloud Service でビデオレンディションを作成する手順 {#steps-creating-screens-video-renditions}

Screens as a Cloud Service で Screens コンテンツプロバイダーからビデオレンディションを作成するには、次の手順に従います。

1. Screens コンテンツプロバイダーで目的のチャネルに移動します。

   >[!NOTE]
   >詳しくは、[Screens コンテンツプロバイダーの使用](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/screens-as-cloud-service/configure-screens-cloud/using-screens-content-provider.html?lang=en#screens-content-provider)を参照してください。

1. 左側のナビゲーションバーの「ツール」セクションをクリックし、 **Assets** 次に、 **処理プロファイル**.

   ![処理プロファイルをクリック](/help/screens-cloud/assets/configure/screens-cp-3.png)

1. クリック **作成** をクリックして処理プロファイルを作成します。

   ![「作成」をクリックします。](/help/screens-cloud/assets/configure/screens-video-2.png)

1. 「**名前**」に「**ScreensProcessingProfile**」などと入力します。

   ![](/help/screens-cloud/assets/configure/screens-video-3.png)

1. に移動します。 **ビデオ** タブでビデオエンコーディングを追加し、 **新規追加**.

   ![](/help/screens-cloud/assets/configure/screens-video-4a.png)

1. 「**エンコード名**」に「**screens-fullhd**」などと入力し、「**ビットレート**」に「**2500**」と入力します。

   ![](/help/screens-cloud/assets/configure/screens-video-4.png)

   >[!IMPORTANT]
   >「screens — 」で始まるエンコーディング名を使用します。 これらのビデオレンディションのみが、Screens as a Cloud Serviceでのビデオエクスペリエンスの再生と見なされます。 ビデオに使用するビットレートを入力します（720 px ビデオの場合は 2500 kbps、1080 px の場合は 5000 kbps）。

   >[!NOTE]
   >ビデオに適した様々な幅／高さ／ビットレートの複数のビデオレンディションを追加できます。デバイスがビデオレンディションのみを再生する場合でも、すべての画面、レンディションは Screens デバイスでダウンロードされます。

1. 「**保存**」をクリックします。

1. 処理プロファイルを選択し、「 **プロファイルをフォルダーに適用**.

   ![プロファイルをフォルダーに適用](/help/screens-cloud/assets/configure/screens-video-5.png)

1. Screens ビデオが保持されるフォルダーを選択し、 **適用**.

   ![「適用](/help/screens-cloud/assets/configure/screens-video-6.png)」をクリックします。

   >[!NOTE]
   >
   >* 複数の処理プロファイルを作成して、それぞれ対応するフォルダーに適用することで、それらのフォルダー内のビデオが特定のビデオレンディションを取得できるようになります。
   >* 処理プロファイルが適用されるフォルダーにビデオをアップロードすると、ビデオが処理されます。 設定済みのレンディションが作成されます。これは、Screens デバイスでビデオを再生するために使用されます。
