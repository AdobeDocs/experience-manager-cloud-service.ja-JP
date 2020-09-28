---
title: アセットの透かしの設定
description: デジタルアセットへの透かしの追加.
contentOwner: AG
translation-type: tm+mt
source-git-commit: 8b1cc8af67c6d12d7e222e12ac4ff77e32ec7e0e
workflow-type: tm+mt
source-wordcount: '206'
ht-degree: 2%

---


# アセットの透かしの設定 {#watermark-assets}

[!DNL Adobe Experience Manager Assets] 画像に電子透かしを追加できます。 [!DNL Assets] は、他の画像ファイルへの透かしとしての画像の適用をサポートしています。 透かしは、アセットの信頼性と著作権の所有権を確認するのに役立ちます。 また、透かしを使用して、機密、ドラフト、有効性などのドキュメントの状態を示すこともできます。

アセットに透かしを設定するExperience Managerを設定するには、次の手順に従います。

1. 透かしとしてPNGファイルが適用されます。 このファイルをDAMリポジトリにアップロードします。

1. 環境に関連付けられたCloud Manager Gitリポジトリにアクセスします。 Cloud Manager Gitリポジトリ `com.adobe.cq.assetcompute.impl.profile.WatermarkingProfileServiceImpl.json` にあるという名前のファイルを、次の内容でコミットします。 詳しくは、「Cloud ServiceとしてExperience ManagerでOSGi設定を行う [方法](/help/implementing/deploying/configuring-osgi.md)」を参照してください。

   ```json
   {
   "watermark": "/content/dam/<path-to-watermark-image.png>",
    "width": 100
   }
   ```

1. [透かしを適用する際にアセットのマイクロサービスを利用する処理プロファイル](/help/assets/asset-microservices-configure-and-use.md#create-custom-profile) を作成します。

   ![透かしを作成するアセット処理プロファイル](assets/watermark-processing-profile.png)

1. [フォルダーに処理プロファイルーを適用して](/help/assets/asset-microservices-configure-and-use.md#use-profiles) 、ウォーターマーク付きのアセットを作成します。

## ヒントと制限事項 {#tips-limitations-bestpractices}

* 1つの設定を使用して、すべてのアセットに透かしを付けることができます。 透かしに使用される画像は1つだけで、幅は固定されます。
* 透かしは、タイルを適用せずに中央に配置できます。
* テキストベースの透かしはサポートされていません。

>[!MORELIKETHIS]
>
>* [Asset Microservicesの概要](/help/assets/asset-microservices-overview.md)。
>* [処理プロファイルでアセットマイクロサービスを使用します](/help/assets/asset-microservices-configure-and-use.md)。

