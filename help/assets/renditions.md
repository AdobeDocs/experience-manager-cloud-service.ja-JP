---
title: Experience Manager Assetsでのレンディションの表示と管理
description: AEM AssetsとDynamic Mediaが、静的および動的な画像レンディションを使用して効果的な画像管理を簡素化する仕組みについて説明します。
exl-id: 006dc493-c400-4d0f-b314-c1978582b7fb
source-git-commit: 4627eb00ba910d1ad2920db15a87761bd7e4a0c0
workflow-type: tm+mt
source-wordcount: '435'
ht-degree: 1%

---

# Experience Manager Assetsでのレンディションの表示と管理{#renditions}

Adobe Experience Manager（AEM）のレンディションは、画像などのデジタルアセットのカスタマイズバージョンで、最適なパフォーマンスを確保するために様々なデバイスやプラットフォーム向けに設計されています。 AEMを使用すると、これらのレンディションを簡単に作成および管理し、ユーザーエクスペリエンスを向上させることができます。 サムネールの作成、web またはモバイル用の画像の最適化、透かしの追加、動的レンディションやスマート切り抜きレンディションの表示とダウンロードなどを行うことができます。

Dynamic Media画像プリセットおよびスマート切り抜きレンディションは、ブランド標準に準拠した体系的な画像管理を促進し、ブランドの結束を最大限に高めます。 これにより、管理者アクセス権を持たずに、必要に応じて動的画像レンディションをすばやく見つけて使用するプロセスが簡略化されます。

レンディションは静的レンディションと動的レンディションに分類され、それぞれのタイプは独自の機能を提供しますが、これらについてさらに詳しく説明します。

## 静的レンディション {#static-renditions}

静的レンディションは、デジタルアセットの事前生成バージョンで、通常はアセットの取り込みまたは変更時に作成されます。 これらのレンディションは、web サムネール、レスポンシブデザイン用のモバイルに対応した形式、印刷用の高解像度バージョンなど、特定の目的とプラットフォーム用に最適化され、効率的で一貫したエクスペリエンスを確保します。
学ぶ [表示とダウンロード方法](#view-dynamic-renditions) での静的レンディション [!DNL Experience Manager Assets].

## 動的レンディション {#dynamic-renditions}

動的レンディションは、特定のニーズを満たすためにリアルタイムで作成されるアセットのカスタマイズバージョンです。例えば、デバイスの解像度に基づく画像のサイズ変更や、様々な縦横比に合わせた切り抜きなどです。
これらのレンディションにより、組織は、パーソナライズされ最適化されたエクスペリエンスを、様々なオーディエンスのニーズに提供できます。 で動的レンディションの表示とダウンロードを行うことができます [!DNL Experience Manager Assets].

### 事前準備

* ライセンスを取得したAEM Dynamic Media ユーザーである必要があります。

* 使用方法 [!UICONTROL 管理ビュー] 次の手順で設定します。
   * [スマート切り抜きイメージプロファイル](/help/assets/dynamic-media/image-profiles.md#creating-image-profiles)
   * [画像プリセット](/help/assets/dynamic-media/managing-image-presets.md)

  次のことができます [ビューの切り替え](/help/assets/assets-view-introduction.md#how-to-access-assets-view) 後でアセットビューで動的レンディションをプレビューできます。

### 動的レンディションの表示とダウンロード {#view-renditions}

で画像の動的レンディションを表示またはダウンロードするには [!DNL Experience Manager Assets]は、次の手順に従います。

1. に移動 **[!UICONTROL アセット管理]** > **[!UICONTROL アセット]**.

1. 該当するアセットフォルダーに移動します。

1. 表示する画像をクリックし、 **[!UICONTROL 詳細]**.

1. 右側のメニューで、 **[!UICONTROL レンディション]**. <br> この **[!UICONTROL レンディション]** パネルが使用可能な状態で開きます **[!UICONTROL 動的]** および **[!UICONTROL スマート切り抜き]** レンディション。

   ![動的レンディション](assets/preset_smart_crop.png)
   <!-- ![dynamic renditions](assets/preset_smart_crop_view.png) -->

1. 表示またはダウンロードする必要があるレンディションをクリックします。

1. 「」をクリックします ![ダウンロードアイコン](assets/do-not-localize/download-icon.png) ダウンロードする必要がある動的レンディションの横にあるアイコン。 <br> または、画像レンディションを選択して、 **[!UICONTROL レンディションをダウンロード]** 下部にあるオプション。

   「」をクリックすると、 ![ダウンロードアイコン](assets/do-not-localize/download-icon.png) アイコンは上部にあります **[!UICONTROL スマート切り抜き]** 「レンディション」セクションで、そのアセットで使用可能なすべてのスマート切り抜きレンディションをダウンロードします。

>[!NOTE]
>
>動的レンディションは、アセットが管理者表示からアップロードされた場合にのみ表示されます。
