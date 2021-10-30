---
title: Screens as a Cloud Service でのビデオレンディションの作成
description: ここでは、Screens as a Cloud Service でビデオレンディションを作成する方法について説明します。
source-git-commit: e24c368811f0c3e61dc0a48c32ef7368f5fc00f5
workflow-type: ht
source-wordcount: '346'
ht-degree: 100%

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
   >詳しくは、[Screens コンテンツプロバイダーの使用](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/screens-as-cloud-service/configure-screens-cloud/using-screens-content-provider.html?lang=ja#screens-content-provider)を参照してください。

1. 左側のナビゲーションバーの「ツール」セクションをクリックして、「**アセット**」をクリックし、「**処理プロファイル**」をクリックします。

   ![](/help/screens-cloud/assets/configure/screens-cp-3.png)

1. 「**作成**」をクリックして、新しい処理プロファイルを作成します。

   ![](/help/screens-cloud/assets/configure/screens-video-2.png)

1. 「**名前**」に「**ScreensProcessingProfile**」などと入力します。

   ![](/help/screens-cloud/assets/configure/screens-video-3.png)

1. 「**ビデオ**」タブに移動してビデオエンコーディングを追加し、「**新規追加**」をクリックします。

   ![](/help/screens-cloud/assets/configure/screens-video-4a.png)

1. 「**エンコード名**」に「**screens-fullhd**」などと入力し、「**ビットレート**」に「**2500**」と入力します。

   ![](/help/screens-cloud/assets/configure/screens-video-4.png)

   >[!IMPORTANT]
   >必ず「screens-」で始まるエンコード名を使用してください。Screens as a Cloud Service では、これらのビデオレンディションのみが再生されます。ビデオに適したビットレートを入力します（720 px ビデオの場合は 2500 kbps、1080 px の場合は 5000 kbps）。

   >[!NOTE]
   >ビデオに適した様々な幅／高さ／ビットレートの複数のビデオレンディションを追加できます。Screens デバイスがビデオレンディションのみ再生する場合でも、すべての「screens-」レンディションがデバイスによってダウンロードされることに注意してください。

1. 「**保存**」をクリックします。

1. 処理プロファイルを選択し、「**プロファイルをフォルダーに適用**」をクリックします。

   ![](/help/screens-cloud/assets/configure/screens-video-5.png)

1. Screens ビデオを保存するフォルダーを選択し、「**適用**」をクリックします。

   ![](/help/screens-cloud/assets/configure/screens-video-6.png)

   >[!NOTE]
   >* 複数の処理プロファイルを作成して、それぞれ対応するフォルダーに適用することで、それらのフォルダー内のビデオが特定のビデオレンディションを取得できるようになります。
   >* 処理プロファイルが適用されるフォルダーにビデオをアップロードすると、ビデオが処理され、設定されたレンディションが作成されます。これらのレンディションは、Screens デバイスでのビデオの再生に使用されます。


