---
title: アセットの透かしの設定
description: デジタルアセットへの透かしの追加。
contentOwner: AG
feature: Asset Management,Publishing
role: User,Admin
exl-id: 210f8925-bd15-4b4a-8714-5a1486eeb49e
source-git-commit: 8f7dc67a8335822b51e4c7796ab55244199fb214
workflow-type: tm+mt
source-wordcount: '276'
ht-degree: 55%

---

# アセットの透かしの設定 {#watermark-assets}

[!DNL Adobe Experience Manager Assets] では、画像に電子透かしを追加できます。[!DNL Assets] は、他の画像ファイルへの透かしとしての画像の適用をサポートしています。透かしは、アセットの信頼性と著作権の所有権を確認するのに役立ちます。また、透かしを使用して、機密、ドラフト、有効性などのドキュメントの状態も示せます。

>[!NOTE]
>
>この機能は、プレリリースチャネルで使用できます。 詳しくは、 [プレリリースチャネルドキュメント](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/release-notes/prerelease.html?lang=en#enable-prerelease) 」を参照してください。

を設定するには、以下を実行します。 [!DNL Experience Manager] アセットに透かしを追加するには：

1. 透かしとして PNG ファイルが適用されます。このファイルを DAM リポジトリにアップロードします。

1. に移動します。 **[!UICONTROL ツール/アセット/アセット設定]**.

1. クリック **[!UICONTROL システム透かしプロファイル]**.

1. の [!UICONTROL システム透かしプロファイルページ]で、手順 1 で DAM リポジトリーにアップロードする画像のパスを指定します。

1. 透かしの尺度を、レンディションの幅を基準に 0.0 ～ 1.0 の範囲で指定します ( **[!UICONTROL 拡大・縮小]** フィールドに入力します。

1. 「**[!UICONTROL 保存]**」をクリックします。

   ![Asset Duplication Detector](assets/system-watermarking-profile.png)

   >[!NOTE]
   >
   >を使用してシステム透かしプロファイルを設定した場合 `com.adobe.cq.assetcompute.impl.profile.WatermarkingProfileServiceImpl.cfg.json` 設定ファイル（OSGi 設定）を使用する場合は引き続き使用できますが、Adobeでは新しいメソッドを使用することをお勧めします。


1. 透かしを適用する際にアセットマイクロサービスを利用する[処理プロファイルを作成します](/help/assets/asset-microservices-configure-and-use.md#create-custom-profile)。

   ![透かしを作成するアセット処理プロファイル](assets/watermark-processing-profile.png)

   必ず **[!UICONTROL 透かし]** 処理プロファイルの作成時に切り替えます。

1. [フォルダーに処理プロファイルを適用して](/help/assets/asset-microservices-configure-and-use.md#use-profiles)、透かし付きのアセットを作成します。

## ヒントと制限事項 {#tips-limitations-bestpractices}

* 単一の設定を使用して、すべてのアセットに透かしを付けることができます。透かしに使用される画像は 1 つだけで、幅は固定されます。
* 透かしはタイルを適用せずに中央に配置できます。
* テキストベースの透かしはサポートされていません。

>[!MORELIKETHIS]
>
>* [アセットマイクロサービスの概要](/help/assets/asset-microservices-overview.md)。
>* [処理プロファイルでアセットマイクロサービスを使用します](/help/assets/asset-microservices-configure-and-use.md)。

