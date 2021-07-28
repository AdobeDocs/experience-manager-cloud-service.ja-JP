---
title: ScreensでのビデオレンディションのCloud Service
description: ここでは、ScreensでビデオレンディションをCloud Serviceとして作成する方法について説明します。
source-git-commit: e24c368811f0c3e61dc0a48c32ef7368f5fc00f5
workflow-type: tm+mt
source-wordcount: '346'
ht-degree: 0%

---


# ScreensでのビデオレンディションのCloud Service {#creating-screens-video-renditions}

## はじめに {#introduction}

ここでは、Screensプレーヤーで使用するビデオレンディションの作成方法について説明します。

>[!IMPORTANT]
>Screensチャネルでビデオを使用する場合は、この節で示す手順を設定する必要があります。

## ScreensでビデオレンディションをCloud Serviceとして作成する手順 {#steps-creating-screens-video-renditions}

次の手順に従って、ScreensコンテンツプロバイダーからビデオレンディションをCloud ServiceとしてScreensに作成します。

1. Screensコンテンツプロバイダー内のチャネルに移動します。

   >[!NOTE]
   >詳しくは、[Screensコンテンツプロバイダーの使用](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/screens-as-cloud-service/configure-screens-cloud/using-screens-content-provider.html?lang=en#screens-content-provider)を参照してください。

1. 左側のナビゲーションバーの「ツール」セクションをクリックし、「**アセット**」をクリックして、「**処理プロファイル**」をクリックします。

   ![](/help/screens-cloud/assets/configure/screens-cp-3.png)

1. 「**作成**」をクリックして、新しい処理プロファイルを作成します。

   ![](/help/screens-cloud/assets/configure/screens-video-2.png)

1. 「**名前**」に、「**ScreensProcessingProfile**」のように入力します。

   ![](/help/screens-cloud/assets/configure/screens-video-3.png)

1. 「**ビデオ**」タブに移動してビデオエンコーディングを追加し、「**新規追加**」をクリックします。

   ![](/help/screens-cloud/assets/configure/screens-video-4a.png)

1. **エンコード名**（例： **screens-fullhd** ）を、**ビットレート**&#x200B;を&#x200B;**2500**&#x200B;と入力します。

   ![](/help/screens-cloud/assets/configure/screens-video-4.png)

   >[!IMPORTANT]
   >「screens — 」で始まるエンコーディング名を使用するようにしてください。これらのビデオレンディションのみが、ScreensでビデオエクスペリエンスをCloud Serviceとして再生すると見なされます。 ビデオに使用するビットレートを入力します（720pxビデオの場合は2,500 kbps、1,080pxの場合は5,000 kbps）。

   >[!NOTE]
   >ビデオを動作させるために、様々な幅/高さ/ビットレートで複数のビデオレンディションを追加できます。 デバイスがビデオレンディションのみを再生する場合でも、すべての画面レンディションがScreensデバイスによってダウンロードされることに注意してください。

1. 「**保存**」をクリックします。

1. 処理プロファイルを選択し、「**プロファイルをフォルダーに適用**」をクリックします。

   ![](/help/screens-cloud/assets/configure/screens-video-5.png)

1. Screensビデオを保存するフォルダーを選択し、「**適用**」をクリックします。

   ![](/help/screens-cloud/assets/configure/screens-video-6.png)

   >[!NOTE]
   >* 複数の処理プロファイルを作成し、対応するフォルダーに適用して、それらのフォルダー内のビデオが特定のビデオレンディションを取得できます。
   >* 処理プロファイルが適用されるフォルダーにビデオをアップロードすると、ビデオが処理され、設定されたレンディションが作成されます。このレンディションは、Screensデバイスでビデオを再生するためにさらに使用されます。


