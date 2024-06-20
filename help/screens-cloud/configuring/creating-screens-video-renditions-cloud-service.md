---
title: Screens as a Cloud Service でのビデオレンディションの作成
description: ここでは、Screens as a Cloud Service でビデオレンディションを作成する方法について説明します。
exl-id: a9c46036-cd29-47fa-81d9-c865cf22c98a
feature: Administering Screens
role: Admin, Developer, User
source-git-commit: f9ba9fefc61876a60567a40000ed6303740032e1
workflow-type: tm+mt
source-wordcount: '360'
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
   >詳しくは、[Screens コンテンツプロバイダーの使用](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/screens-as-cloud-service/configure-screens-cloud/using-screens-content-provider.html?lang=ja#screens-content-provider)を参照してください。

1. 左側のナビゲーションバーの「ツール」セクションをクリックして、「**アセット**」をクリックし、「**処理プロファイル**」をクリックします。

   ![処理プロファイルをクリック](/help/screens-cloud/assets/configure/screens-cp-3.png)

1. 「**作成**」をクリックして、処理プロファイルを作成します。

   ![「作成」をクリック](/help/screens-cloud/assets/configure/screens-video-2.png)

1. 「**名前**」に「**ScreensProcessingProfile**」などと入力します。

   ![「名前」フィールドがハイライト表示された処理プロファイルダイアログボックス](/help/screens-cloud/assets/configure/screens-video-3.png)

1. 「**ビデオ**」タブでに移動してビデオエンコーディングを追加し、「**新規追加**」をクリックします。

   ![「新規追加」ボタンがハイライト表示された処理プロファイルダイアログボックス](/help/screens-cloud/assets/configure/screens-video-4a.png)

1. 「**エンコード名**」に「**screens-fullhd**」などと入力し、「**ビットレート**」に「**2500**」と入力します。

   ![「保存」ボタンがハイライト表示された処理プロファイルダイアログボックス](/help/screens-cloud/assets/configure/screens-video-4.png)

   >[!IMPORTANT]
   >「screens-」で始まるエンコーディング名を使用します。これらのビデオレンディションのみが、Screens as a Cloud Serviceでのビデオエクスペリエンス再生が考慮されます。ビデオに適したビットレートを入力します（720 ピクセルのビデオの場合は 2500 kbps、1080 ピクセルの場合は 5000 kbps）。

   >[!NOTE]
   >ビデオに適した様々な幅／高さ／ビットレートの複数のビデオレンディションを追加できます。すべてのスクリーン、レンディションは Screens デバイスによってダウンロードされますが、Screens デバイスはビデオレンディションのみ再生します。

1. 「**保存**」をクリックします。

1. 処理プロファイルを選択し、「**プロファイルをフォルダーに適用**」をクリックします。

   ![プロファイルをフォルダーに適用](/help/screens-cloud/assets/configure/screens-video-5.png)

1. Screens ビデオを保存するフォルダーを選択し、「**適用**」をクリックします。

   ![「適用](/help/screens-cloud/assets/configure/screens-video-6.png)」をクリックします。

   >[!NOTE]
   >
   >* 複数の処理プロファイルを作成して、それぞれ対応するフォルダーに適用することで、それらのフォルダー内のビデオが特定のビデオレンディションを取得できるようになります。
   >* 処理プロファイルが適用されるフォルダーにビデオをアップロードすると、ビデオが処理されます。設定済みのレンディションが作成されます。これは、Screens デバイスでビデオを再生するために使用されます。
