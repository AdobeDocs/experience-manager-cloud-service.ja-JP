---
title: Experience Manager Assetsでのレンディションの表示と管理
description: AEM AssetsとDynamic Mediaが、静的および動的な画像レンディションを使用して効果的な画像管理を簡素化する仕組みについて説明します。
exl-id: 006dc493-c400-4d0f-b314-c1978582b7fb
feature: Renditions
role: User
source-git-commit: a3a6456dec178c36c9fe8acfb6f98915fc86e490
workflow-type: tm+mt
source-wordcount: '600'
ht-degree: 4%

---

# Experience Manager Assetsでのレンディションの表示と管理{#renditions}

| [検索のベストプラクティス](/help/assets/search-best-practices.md) | [メタデータのベストプラクティス](/help/assets/metadata-best-practices.md) | [コンテンツハブ](/help/assets/product-overview.md) | [OpenAPI 機能を備えた Dynamic Media](/help/assets/dynamic-media-open-apis-overview.md) | [AEM Assets 開発者向けドキュメント](https://developer.adobe.com/experience-cloud/experience-manager-apis/) |
| ------------- | --------------------------- |---------|----|-----|

Adobe Experience Manager（AEM）のレンディションは、画像などのデジタルアセットのカスタマイズバージョンで、最適なパフォーマンスを確保するために様々なデバイスやプラットフォーム向けに設計されています。 AEMを使用すると、これらのレンディションを簡単に作成および管理でき、ユーザーエクスペリエンスが向上します。 サムネールの作成、web またはモバイル用の画像の最適化、透かしの追加、動的レンディションやスマート切り抜きレンディションの表示とダウンロードなどを行うことができます。

Dynamic Media画像プリセットおよびスマート切り抜きレンディションは、ブランド標準に準拠した体系的な画像管理を促進し、ブランドの結束を最大限に高めます。 これにより、管理者アクセス権を持たずに、必要に応じて動的画像レンディションをすばやく見つけて使用するプロセスが簡略化されます。

レンディションは静的レンディションと動的レンディションに分類され、それぞれのタイプは独自の機能を提供しますが、これらについてさらに詳しく説明します。

## 静的レンディション {#static-renditions}

静的レンディションは、デジタルアセットの事前生成バージョンで、通常はアセットの取り込みまたは変更時に作成されます。 これらのレンディションは、web サムネール、レスポンシブデザイン用のモバイルに対応した形式、印刷用の高解像度バージョンなど、特定の目的とプラットフォーム用に最適化され、効率的で一貫したエクスペリエンスを確保します。
[!DNL Experience Manager Assets] の静的レンディション [ 表示およびダウンロード方法 ](#view-dynamic-renditions) について説明します。

## 動的レンディション {#dynamic-renditions}

動的レンディションは、特定のニーズを満たすためにリアルタイムで作成されるアセットのカスタマイズバージョンです。例えば、デバイスの解像度に基づく画像のサイズ変更や、様々な縦横比に合わせた切り抜きなどです。
これらのレンディションにより、組織は、パーソナライズされ最適化されたエクスペリエンスを、様々なオーディエンスのニーズに提供できます。 [!DNL Experience Manager Assets] で動的レンディションを表示およびダウンロードできます。

## Dynamic Media レンディション {#dynamic-media-renditions}

### 事前準備

* ライセンスを取得したAEM Dynamic Media ユーザーである必要があります。
* [!UICONTROL  管理者ビュー ] を使用して、次の設定を行います。
   * [ スマート切り抜き画像プロファイル ](/help/assets/dynamic-media/image-profiles.md#creating-image-profiles)
   * [画像プリセット](/help/assets/dynamic-media/managing-image-presets.md)

  後で [ ビューを切り替えて ](/help/assets/assets-view-introduction.md#how-to-access-assets-view)Assets ビューで動的レンディションをプレビューできます。
* Publish assets をDynamic Mediaに追加して、Dynamic Media レンディションをAssets ビューで使用できるようにします。 詳しくは、[AEMおよびDynamic MediaへのPublish Assets](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/assets/assets-view/publish-assets-to-aem-and-dm) を参照してください。


### Dynamic Media レンディションの表示とダウンロード {#view-download-dm-renditions}

Experience Manager Assetsで画像の動的レンディションを表示またはダウンロードするには、次の手順に従います。

1. **[!UICONTROL Assets Management]** / **[!UICONTROL Assets]** に移動します。

1. 該当するアセットフォルダーに移動します。

1. 表示するアセットをクリックし、「**[!UICONTROL 詳細]**」をクリックします。

1. 右側のメニューで、「**[!UICONTROL Dynamic Media]**」アイコンをクリックします。 **[!UICONTROL Dynamic Media]** パネルには、Dynamic Mediaとスマート切り抜きのレンディションが表示されます。

   ![ 動的レンディション ](/help/assets/assets/dm-scene7-renditions.png)
   <!-- ![dynamic renditions](assets/preset_smart_crop_view.png) -->

1. プレビューするレンディションを選択し、「**URL をコピー**」をクリックして、選択したレンディションの URL をコピーします。 **レンディションをダウンロード** をクリックして、画像アセットのレンディションをダウンロードします。
1. プレビューするスマート切り抜きレンディションを選択し、「**URL をコピー**」をクリックして、選択したレンディションの URL をコピーします。
1. ![ ダウンロードアイコン ](assets/do-not-localize/download-icon.png) をクリックして、使用可能なすべてのスマート切り抜きレンディションを単一の zip ファイルとしてダウンロードします。
   ![ ダウンロードアイコン ](/help/assets/assets/smartcrop-rendition.png)

   >[!NOTE]
   >
   >これらのレンディションは、画像アセットに対してのみ使用できます。

## OpenAPI 機能レンディションを使用したDynamic Media {#dm-with-openapi-renditions}

### 事前準備

* ライセンスを取得したAEM Dynamic Media ユーザーである必要があります。
* Dynamic Mediaに OpenAPI 機能レンディションを表示するには、Assetsの承認が必要です。 詳しくは、「[Experience Managerでアセットを承認 ](/help/assets/approve-assets.md#copy-delivery-url-approved-assets)」を参照してください
* OpenAPI 機能を備えたDynamic MediaをAEM as a Cloud Service インスタンスで有効にする必要があります。

### OpenAPI 機能のレンディションを使用したDynamic Mediaの表示 {#view-download-dm-with-openapi-renditions}

1. アセットを選択し、「**詳細**」をクリックします。
1. 右側のパネルに表示されている「Dynamic Media」アイコンをクリックします。 Dynamic Media パネルには、すべてのアセットタイプに対応する OpenAPI 機能レンディションを含むDynamic Mediaが表示されます。
   ![ ダウンロードアイコン ](/help/assets/assets/dm-with-open-api-copy-url.png)
1. 「**OpenAPI でDynamic Media**」オプションを選択し、「**URL をコピー**」をクリックして、アセットの配信 URL をコピーします。


