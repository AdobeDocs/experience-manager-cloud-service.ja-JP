---
title: Dynamic Media の操作
description: Dynamic Media を使用して、Web、モバイルおよびソーシャルサイトで使用するためにアセットを配信する方法を学習します。
translation-type: tm+mt
source-git-commit: 6224d193adfb87bd9b080f48937e0af1f03386d6

---


# Dynamic Media の操作 {#working-with-dynamic-media}

[Dynamic Media ](https://www.adobe.com/solutions/web-experience-management/dynamic-media.html)は、マーチャンダイジングおよびマーケティング用のリッチなビジュアルアセットをオンデマンドで配信するもので、これらのアセットは、Web、モバイルおよびソーシャルサイトでの利用に合わせて自動的に拡大縮小されます。Dynamic Media は、一連のマスターアセットを使用し、パフォーマンスが最適化されスケーラビリティに優れたグローバルネットワーク経由で、複数のリッチコンテンツのバリエーションをリアルタイムで生成および配信します。

Dynamic Media は、ズーム、360 度スピン、ビデオなどのインタラクティブな閲覧エクスペリエンスを提供します。Dynamic Media は Adobe Experience Manager デジタルアセット管理（AEM アセット）ソリューションのワークフローを独自に取り込むことで、デジタルキャンペーン管理プロセスを簡易化し、効率化します。

>[!NOTE]
>
>[Adobe Experience Manager および Dynamic Media の操作](https://helpx.adobe.com/experience-manager/using/aem_dynamic_media.html)にコミュニティの記事があります。

## Dynamic Media の機能 {#what-you-can-do-with-dynamic-media}

Dynamic Media では、公開前のアセットを管理できます。一般的なアセットの操作方法については、[デジタルアセットの操作](/help/assets/manage-digital-assets.md)で詳しく説明しています。一般的なトピックには、アセットのアップロード、ダウンロード、編集および公開、プロパティの表示と編集、アセットの検索が含まれます。

ダイナミックメディア専用の機能には、次のものがあります。

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
* [クイックビューを使用したカスタムポップアップの作成](custom-pop-ups.md)

[Dynamic Media の設定](administering-dynamic-media.md)も参照してください。

<!-- 

OBSOLETE UNTIL INTEGRATING SCENE7 TOPIC GETS A MAJOR UPDATE
>[!NOTE]
>
>To understand the differences between using Dynamic Media and integrating Dynamic Media Classic with AEM, see [Dynamic Media Classic integration versus Dynamic Media](/help/sites-cloud/administering/integrating-scene7.md#aem-scene-integration-versus-dynamic-media).

-->

## ダイナミックメディアを有効にするか、ダイナミックメディアを無効にするか {#dynamic-media-on-versus-dynamic-media-off}

ダイナミックメディアが有効（オン）になっているかどうかは、次の特性によって判断できます。

* 動的レンディションは、アセットのダウンロード時またはプレビュー時に使用できます。
* 画像セット、スピンセット、混在メディアセットを使用できます。
* PTIFF レンディションが作成されている。

画像アセットをクリックすると、ダイナミックメディアを有効にした場合に、アセットの表示が異なります。 Dynamic Media では、オンデマンドの HTML5 ビューアが使用されます。

### Dynamic renditions {#dynamic-renditions}

「**[!UICONTROL 動的]**」の下にある画像プリセットやビューアプリセットなどの動的レンディションは、Dynamic Media が有効な場合に使用できます。

![chlimage_1-358](assets/chlimage_1-358.png)

### 画像セット、スピンセット、混在メディアセット {#image-sets-spins-sets-mixed-media-sets}

画像セット、スピンセットおよび混在メディアセットは、Dynamic Media が有効な場合に使用できます。

![chlimage_1-359](assets/chlimage_1-359.png)

### PTIFF renditions {#ptiff-renditions}

Dynamic media enabled assets include `pyramid.tiffs`.

![chlimage_1-360](assets/chlimage_1-360.png)

### アセットのビューの変化 {#asset-views-change}

With Dynamic Media enabled, you can zoom in and out by clicking the `+` and `-` buttons. You can also click/tap to zoom into certain area. Revert brings you to the original version and you can make the image full screen by clicking the diagonal arrows. Dynamic Media enabled looks like this:

![chlimage_1-361](assets/chlimage_1-361.png)

ダイナミックメディアを無効にした状態で、ズームインおよびズームアウトを行い、元のサイズに戻すことができます。

![chlimage_1-362](assets/chlimage_1-362.png)
