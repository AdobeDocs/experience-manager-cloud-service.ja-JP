---
title: Dynamic Media を操作する
description: Dynamic Media を使用して、Web、モバイルおよびソーシャルサイトで使用するためにアセットを配信する方法を学習します。
role: Admin,User
exl-id: 3ec3cb85-88ce-4277-a45c-30e52c75ed42
source-git-commit: fa6de4e383b4de628938fce455f321911cad452c
workflow-type: tm+mt
source-wordcount: '398'
ht-degree: 100%

---

# Dynamic Media を操作する  {#working-with-dynamic-media}

[Dynamic Media](https://business.adobe.com/jp/products/experience-manager/assets/dynamic-media.html) は、マーチャンダイジングおよびマーケティング用のリッチなビジュアルアセットをオンデマンドで配信するもので、これらのアセットは、Web、モバイルおよびソーシャルサイトでの利用に合わせて自動的に拡大縮小されます。Dynamic Media は、一連のプライマリソースアセットを使用し、パフォーマンスが最適化されスケーラビリティに優れたグローバルネットワーク経由で、複数のリッチコンテンツのバリエーションをリアルタイムで生成および配信します。

Dynamic Media は、ズーム、360 度スピン、ビデオなどのインタラクティブな閲覧エクスペリエンスを提供します。Dynamic Media は Adobe Experience Manager デジタルアセット管理（AEM Assets）ソリューションのワークフローを独自に取り込むことで、デジタルキャンペーン管理プロセスを簡易化し、効率化します。

<!-- >[!NOTE]
>
>A Community article is available on [Working with Adobe Experience Manager and Dynamic Media](https://helpx.adobe.com/experience-manager/using/aem_dynamic_media.html). -->

## Dynamic Media の機能 {#what-you-can-do-with-dynamic-media}

Dynamic Media では、公開前のアセットを管理できます。一般的なアセットの操作方法については、[デジタルアセットの操作](/help/assets/manage-digital-assets.md)で詳しく説明しています。一般的なトピックには、アセットのアップロード、ダウンロード、編集および公開、プロパティの表示と編集、アセットの検索が含まれます。

Dynamic Media 限定の機能は次のとおりです。

* [カルーセルバナー](carousel-banners.md)
* [画像セット](image-sets.md)
* [インタラクティブ画像](interactive-images.md)
* [インタラクティブビデオ](interactive-videos.md)
* [混在メディアセット](mixed-media-sets.md)
* [パノラマ画像](panoramic-images.md)

* [スピンセット](spin-sets.md)
* [ビデオ](video.md)
* [Dynamic Media アセットの配信](delivering-dynamic-media-assets.md)
* [アセットの管理](managing-assets.md)
* [クイックビューを使用したカスタムポップアップウィンドウの作成](custom-pop-ups.md)

[Dynamic Media の設定](administering-dynamic-media.md)も参照してください。

<!-- 

OBSOLETE UNTIL INTEGRATING SCENE7 TOPIC GETS A MAJOR UPDATE
>[!NOTE]
>
>To understand the differences between using Dynamic Media and integrating Dynamic Media Classic with AEM, see [Dynamic Media Classic integration versus Dynamic Media](/help/sites-cloud/administering/integrating-scene7.md#aem-scene-integration-versus-dynamic-media).

-->

## Dynamic Media が有効な場合と無効な場合の比較 {#dynamic-media-on-versus-dynamic-media-off}

Dynamic Media が有効（オン）になっているかどうかは、次の特徴から判断できます。

* アセットのダウンロードやプレビューで動的レンディションを使用できる。
* 画像セット、スピンセット、混在メディアセットを使用できる。
* PTIFF レンディションが作成されている。

Dynamic Media を有効にしている場合、画像アセットをクリックしたときのアセットのビューが異なります。Dynamic Media では、オンデマンドの HTML5 ビューアが使用されます。

### 動的レンディション {#dynamic-renditions}

「**[!UICONTROL 動的]**」の下にある画像プリセットやビューアプリセットなどの動的レンディションは、Dynamic Media が有効な場合に使用できます。

![chlimage_1-358](assets/chlimage_1-358.png)

### 画像セット、スピンセット、混在メディアセット {#image-sets-spins-sets-mixed-media-sets}

画像セット、スピンセットおよび混在メディアセットは、Dynamic Media が有効な場合に使用できます。

![chlimage_1-359](assets/chlimage_1-359.png)

### PTIFF レンディション {#ptiff-renditions}

Dynamic Media 対応のアセットには `pyramid.tiffs` が含まれています。

![chlimage_1-360](assets/chlimage_1-360.png)

### アセットのビューの変化 {#asset-views-change}

Dynamic Media を有効にすると、「`+`」ボタンをクリックしてズームインし、「`-`」ボタンをクリックしてズームアウトすることができます。クリックまたはタップして、特定の領域にズームインすることもできます。元に戻すアイコンをクリックすると元のバージョンに戻ります。また、斜めの矢印をクリックすると、画像を全画面表示にすることができます。Dynamic Media を有効にした場合の画面は次のようになります。

![chlimage_1-361](assets/chlimage_1-361.png)

Dynamic Media を無効にした場合は、次のようにズームイン、ズームアウトおよび元のサイズに戻す操作が可能です。

![chlimage_1-362](assets/chlimage_1-362.png)
