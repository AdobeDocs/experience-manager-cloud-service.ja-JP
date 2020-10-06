---
title: アセットの透かしの設定
description: デジタルアセットへの透かしの追加.
contentOwner: AG
translation-type: tm+mt
source-git-commit: 7ea7af1cf784b6866f3c2484475a8072ff76be2c
workflow-type: tm+mt
source-wordcount: '198'
ht-degree: 3%

---


# アセットの透かしの設定 {#watermark-assets}

[!DNL Adobe Experience Manager Assets] 画像に電子透かしを追加できます。 [!DNL Assets] は、他の画像ファイルへの透かしとしての画像の適用をサポートしています。 透かしは、アセットの信頼性と著作権の所有権を確認するのに役立ちます。 また、透かしを使用して、機密、ドラフト、有効性などのドキュメントの状態を示すこともできます。

アセットの透かし [!DNL Experience Manager] を設定するには、次の手順に従います。

1. 透かしとしてPNGファイルが適用されます。 このファイルをDAMリポジトリにアップロードします。

1. 環境に関連付けられた [!DNL Cloud Manager] Gitリポジトリにアクセスします。 Gitリポジトリ `com.adobe.cq.assetcompute.impl.profile.WatermarkingProfileServiceImpl.json`[!DNL Cloud Manager] にあるという名前のファイルを、次の内容でコミットします。 詳しくは、「Cloud Service [内でOSGi設定を行う [!DNL Experience Manager] 方法](/help/implementing/deploying/configuring-osgi.md)」を参照してください。

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

