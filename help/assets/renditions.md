---
title: Experience Manager Assets でのレンディションの表示と管理
description: AEM Assets と Dynamic Media が静的および動的な画像レンディションを使用して効果的な画像管理を簡素化する仕組みについて説明します。
exl-id: 006dc493-c400-4d0f-b314-c1978582b7fb
feature: Renditions
role: User
source-git-commit: 32fdbf9b4151c949b307d8bd587ade163682b2e5
workflow-type: ht
source-wordcount: '646'
ht-degree: 100%

---

# Experience Manager Assets でのレンディションの表示と管理{#renditions}

Adobe Experience Manager（AEM）のレンディションは、最適なパフォーマンスを確保することを目的に、様々なデバイスやプラットフォーム向けに設計された、画像などのデジタルアセットのカスタマイズされたバージョンです。AEM を使用すると、これらのレンディションを簡単に作成および管理し、ユーザーエクスペリエンスを向上させることができます。サムネールの作成、web またはモバイル用の画像の最適化、透かしの追加、動的レンディションやスマート切り抜きレンディションの表示とダウンロードなどを行うことができます。

Dynamic Media 画像プリセットおよびスマート切り抜きレンディションは、ブランド標準に準拠した体系的な画像管理を促進し、ブランドの統一性を最大限に高めます。これにより、管理者アクセス権を持たずに、必要に応じて動的画像レンディションをすばやく見つけて使用するプロセスが簡素化されます。

レンディションは静的と動的に分類され、各タイプには独自の機能と能力がありますが、これらについてさらに詳しく説明します。

## 静的レンディション {#static-renditions}

静的レンディションは、デジタルアセットの事前生成されたバージョンで、通常はアセットの取り込みまたは変更中に作成されます。これらのレンディションは、web サムネール、レスポンシブデザイン用のモバイルに対応した形式、印刷用の高解像度バージョンなど、特定の目的とプラットフォーム用に最適化され、効率的で一貫したエクスペリエンスを確保します。
詳しくは、Experience Manager Assets で[静的レンディションの表示とダウンロード](#view-and-download-static-renditions)を行う方法を参照してください。

### 静的レンディションの表示とダウンロード{#view-and-download-static-renditions}

アセットのレンディションを表示してダウンロードするには、次の手順に従います。

1. アセットビューで、「**アセット**」をクリックし、フォルダーに移動してアセットを選択し、「**詳細**」をクリックします。
1. 右側のパネルで使用可能なレンディションのアイコンをクリックします。
1. レンディションを選択してプレビューし、![ダウンロードアイコン](/help/assets/assets/download-icon.svg) をクリックしてダウンロードします。

   ![動的レンディションの表示とダウンロード](/help/assets/assets/view-download-static-rendition.png)

## 動的レンディション {#dynamic-renditions}

動的レンディションは、特定のニーズに合うようにリアルタイムで作成される、カスタマイズされたアセットバージョンです。例えば、デバイスの解像度に基づく画像のサイズ変更や、様々な縦横比に合わせた切り抜きなどです。
これらのレンディションにより、組織は、様々なオーディエンスニーズに合わせて、パーソナライズされ最適化されたエクスペリエンスを提供できます。Experience Manager Assets で動的レンディションを表示およびダウンロードできます。

## Dynamic Media レンディション {#dynamic-media-renditions}

### 始める前に

* ライセンス済み AEM Dynamic Media ユーザーである必要があります。
* [!UICONTROL 管理ビュー]を使用して、以下を設定します。
   * [スマート切り抜き画像プロファイル](/help/assets/dynamic-media/image-profiles.md#creating-image-profiles)
   * [画像プリセット](/help/assets/dynamic-media/managing-image-presets.md)

  後で[ビューを切り替えて](/help/assets/assets-view-introduction.md#how-to-access-assets-view)、アセットビューで動的レンディションをプレビューできます。
* アセットを Dynamic Media に公開すると、アセットビューで Dynamic Media レンディションを使用できます。詳しくは、[AEM および Dynamic Media へのアセットの公開](https://experienceleague.adobe.com/ja/docs/experience-manager-cloud-service/content/assets/assets-view/publish-assets-to-aem-and-dm)を参照してください。


### Dynamic Media レンディションの表示とダウンロード {#view-download-dm-renditions}

Experience Manager Assets で画像の動的レンディションを表示またはダウンロードするには、次の手順に従います。

1. **[!UICONTROL アセット管理]**／**[!UICONTROL アセット]**&#x200B;に移動します。

1. 該当するアセットフォルダーに移動します。

1. 表示する必要があるアセットをクリックし、「**[!UICONTROL 詳細]**」をクリックします。

1. 右側のメニューで、**[!UICONTROL Dynamic Media]** アイコンをクリックします。**[!UICONTROL Dynamic Media]** パネルには、Dynamic Media レンディションとスマート切り抜きレンディションが表示されます。

   ![動的レンディション](/help/assets/assets/dm-scene7-renditions.png)
   <!-- ![dynamic renditions](assets/preset_smart_crop_view.png) -->

1. プレビューするレンディションを選択し、「**URL をコピー**」をクリックして、選択したレンディションの URL をコピーします。「**レンディションをダウンロード**」をクリックして、画像アセットのレンディションをダウンロードします。
1. プレビューするスマート切り抜きレンディションを選択し、「**URL をコピー**」をクリックして、選択したレンディションの URL をコピーします。
1. ![ダウンロードアイコン](assets/do-not-localize/download-icon.png) をクリックして、使用可能なすべてのスマート切り抜きレンディションを 1 つの zip ファイルとしてダウンロードします。
   ![ダウンロードアイコン](/help/assets/assets/smartcrop-rendition.png)

   >[!NOTE]
   >
   >これらのレンディションは、画像アセットに対してのみ使用できます。

## OpenAPI 機能搭載 Dynamic Media レンディション {#dm-with-openapi-renditions}

### 始める前に {#prereqs-dm-with-openapi-renditions}

* ライセンス済み AEM Dynamic Media ユーザーである必要があります。
* OpenAPI 機能搭載 Dynamic Media レンディションを表示するには、アセットを承認する必要があります。詳しくは、[Experience Manager でのアセットの承認](/help/assets/approve-assets.md#copy-delivery-url-approved-assets)を参照してください。
* OpenAPI 機能搭載 Dynamic Media は、AEM as a Cloud Service インスタンスで有効にする必要があります。

### OpenAPI 機能搭載 Dynamic Media レンディションの表示 {#view-download-dm-with-openapi-renditions}

1. アセットを選択し、「**詳細**」をクリックします。
1. 右側のパネルで使用可能な Dynamic Media アイコンをクリックします。Dynamic Media パネルには、すべてのアセットタイプ向けの OpenAPI 機能搭載 Dynamic Media レンディションが表示されます。
   ![ダウンロードアイコン](/help/assets/assets/dm-with-open-api-copy-url.png)
1. 「**OpenAPI 機能搭載 Dynamic Media**」オプションを選択し、「**URL をコピー**」をクリックして、アセットの配信 URL をコピーします。


