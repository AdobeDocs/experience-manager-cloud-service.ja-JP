---
title: Dynamic Media を操作する
description: Dynamic Mediaの概要と、Dynamic Mediaを使用して、web、モバイルおよびソーシャルサイトで使用するためにアセットを配信する方法について説明します。
contentOwner: Rick Brough
feature: Dynamic Media,Asset Management
role: Admin,User
exl-id: 3ec3cb85-88ce-4277-a45c-30e52c75ed42
source-git-commit: 57fb7a011cb2da853cdca4f3233cd56775f4a459
workflow-type: tm+mt
source-wordcount: '655'
ht-degree: 56%

---

# Dynamic Media を操作する  {#working-with-dynamic-media}

[Dynamic Media](https://business.adobe.com/jp/products/experience-manager/assets/dynamic-media.html) は、マーチャンダイジングおよびマーケティング用のリッチなビジュアルアセットをオンデマンドで配信するもので、これらのアセットは、Web、モバイルおよびソーシャルサイトでの利用に合わせて自動的に拡大縮小されます。Dynamic Media は、一連のプライマリソースアセットを使用し、パフォーマンスが最適化されスケーラビリティに優れたグローバルネットワーク経由で、複数のリッチコンテンツのバリエーションをリアルタイムで生成および配信します。

Dynamic Media は、ズーム、360 度スピン、ビデオなどのインタラクティブな閲覧エクスペリエンスを提供します。Dynamic Media は Adobe Experience Manager デジタルアセット管理（AEM Assets）ソリューションのワークフローを独自に取り込むことで、デジタルキャンペーン管理プロセスを簡易化し、効率化します。

<!-- >[!NOTE]
>
>A Community article is available on [Working with Adobe Experience Manager and Dynamic Media](https://helpx.adobe.com/experience-manager/using/aem_dynamic_media.html). -->

## Dynamic Mediaとは

Adobe Experience Manager（AEM）のDynamic Mediaas a Cloud Serviceは、あらゆるデジタルプラットフォームにわたって画像やビデオなどのリッチメディアアセットを管理、配信および最適化することを支援するように設計された、強力なソリューションです。 ユーザーのデバイスや画面サイズに基づくサイズ変更、切り抜き、品質の調整などのリアルタイム修正を可能にすることで、静的メディアを動的で魅力的なエクスペリエンスに変換します。 Dynamic Mediaを使用すると、デスクトップ、モバイル、タブレットのいずれを使用している場合でも、アセットは最適なビジュアルエクスペリエンスを提供するように自動的に適応します。

Dynamic Mediaの主なメリットの 1 つは、メディア管理を合理化できることです。 Dynamic Mediaは、それぞれの状況に最も適したフォーマットを提供することですべてを処理します。 例えば、e コマース企業は 360 度の製品表示やズーム可能な画像を利用してインタラクティブなエクスペリエンスを作成できますが、コンテンツ量の多い web サイトでは高速で高品質なビデオストリーミングを確保できます。 その結果、読み込み時間が短縮され、より魅力的なユーザーエクスペリエンスが得られ、最終的には顧客満足度の向上とコンバージョン率の向上につながります。

Dynamic Mediaは、AEMのデジタルアセット管理（DAM）システムとシームレスに統合され、メディアを保存、整理、デプロイするための単一のプラットフォームを提供します。 この一元化されたアプローチにより、チーム間の共同作業が簡素化され、アセットのパフォーマンスに関するリアルタイムのインサイトが提供されます。 魅力的なビジュアルの提供に重点を置く場合でも、メディア主導のユーザーインタラクションを強化する場合でも、Dynamic Mediaは、あらゆるチャネルでコンテンツを最適化するのに役立ちます。そのため、デジタルプレゼンスを高めようとしている企業にとって不可欠なツールになります。

## Dynamic Media の機能 {#what-you-can-do-with-dynamic-media}

Dynamic Media を使用すると、アセットを公開する前に管理できます。一般的なアセットの操作方法について詳しくはは、[デジタルアセットの操作](/help/assets/manage-digital-assets.md)を参照してください。一般的なトピックには、アセットのアップロード、ダウンロード、編集、公開と、プロパティの表示、編集、アセットの検索が含まれます。

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

### Dynamic Media画像セット、スピンセット、混在メディアセット {#image-sets-spins-sets-mixed-media-sets}

画像セット、スピンセットおよび混在メディアセットは、Dynamic Media が有効な場合に使用できます。

![chlimage_1-359](assets/chlimage_1-359.png)

### Dynamic Media対応 PTIFF レンディション {#ptiff-renditions}

Dynamic Media 対応のアセットには `pyramid.tiffs` が含まれます。

![chlimage_1-360](assets/chlimage_1-360.png)

### Dynamic Mediaのアセットのビューの変化 {#asset-views-change}

Dynamic Media を有効にした場合、`+` および `-` ボタンをクリックして、ズームインおよびズームアウトできます。また、特定のエリアにズームインすることもできます。「元に戻す」を選択すると元のバージョンに戻り、斜めの矢印をクリックして画像を全画面表示にすることができます。Dynamic Media を有効にした場合の画面は次のようになります。

![chlimage_1-361](assets/chlimage_1-361.png)

Dynamic Media を無効にした場合は、次のようにズームイン、ズームアウトおよび元のサイズに戻す操作が可能です。

![chlimage_1-362](assets/chlimage_1-362.png)
