---
title: Dynamic Media でのアクセシビリティ
description: Dynamic Media および Dynamic Media ビューアでのアクセシビリティについて説明します。
contentOwner: Rick Brough
topic-tags: introduction
content-type: reference
translation-type: tm+mt
source-git-commit: cf607bd27463f23de29d0d6770940a01f3e36c87
workflow-type: tm+mt
source-wordcount: '0'
ht-degree: 0%

---


# Dynamic Media でのアクセシビリティ {#accessibility-in-dm}

Dynamic Media では、オーサリングユーザーインターフェイス全体でキーボードコントロールおよび支援テクノロジー（JAWS スクリーンリーダーや NVDA スクリーンリーダーなど）をサポートしています。

## Dynamic Media でのキーボードアクセシビリティのサポート {#keyboard-support-in-dm}

Dynamic MediaはExperience Managerアセットのプラグインなので、キーボードコントロールの動作のほとんどはExperience Managerアセットの動作と同じです。 例えば、Dynamic Mediaの`Cancel`ボタンは、Experience Managerアセットと同じフォーカスハイライトを持ちます。 また、Experience Managerアセットと同様に`Spacebar`キーにも対応します。 アセット](/help/assets/accessibility.md#keyboard-shortcuts)の[キーボードショートカットを参照してください。

Dynamic Mediaの個々のユーザーインターフェイス要素でサポートされているキーストロークは、ほとんどの場合、明確で見つけやすいものです。 Dynamic Media のキーボードコントロールは、以下の機能があります。

* `Tab` と `Shift+Tab` のキー操作を使用して、ページ上のインタラクティブ要素間を移動できます。`Tab` を使用すると、タブ順序における次のユーザーインターフェイス要素に入力フォーカスが進みます。`Shift+Tab` を使用すると、入力フォーカスが前のユーザーインターフェイス要素に戻ります。フォーカストラバーサルは、画面上のユーザーインターフェイス要素の自然な位置に従い、左から右、上から下の順に移動します。また、フィールドにエラーがある場合は、`Tab` を押して、そのフィールドにフォーカスを移動できます。
* `Spacebar`キーと`Enter`キーを使用して、ボタンやドロップダウンリストなどの標準的なユーザインターフェイス要素をアクティブにする機能。
* アクティブな要素にキーボードフォーカスのハイライト表示をおこなえます。入力フォーカスを有するユーザインターフェイス要素は、ユーザインターフェイス要素の周りにレンダリングされた境界として視覚的なフォーカス表示を受け取る。
* ホットスポットエディターでは、矢印キーなどのいくつかのカスタムキー操作を使用して複雑なユーザインターフェイス要素を操作し、ホットスポットの位置を変更できます。
* インタラクティブビデオエディターでは、`Spacebar` を使用して画像を選択し、それをセグメントに追加できます。また、`Backspace`キーを使用して、「**[!UICONTROL コンテンツ]**」タブから選択したアイテムを削除できます。 また、必要に応じて `Tab` キーを押して、ページ上のインタラクティブ要素間を移動できます。
* 画像切り抜き/スマート切り抜きエディタで、次の操作を実行できます。
   * 矢印キーを使用して、フレームサイズを切り抜いたり、画像の位置を変更したりします。
   * 最初の `Tab` ストップで画像フレーム全体がハイライト表示されます。その後、キーボードの矢印キーを使用してフレームの位置を変更できます。
   * その次の 4 つの `Tab` ストップはフレームの四隅です。フレームの隅をフォーカスすると、その隅がハイライト表示されます。この場合も、キーボードの矢印キーを使用して、フォーカスされた隅を移動できます。詳しくは、[単一の画像のスマート切り抜きまたはスマートスウォッチの編集](/help/assets/dynamic-media/image-profiles.md#editing-the-smart-crop-or-smart-swatch-of-a-single-image)を参照してください。

<!-- Keyboarding is the same because Dynamic Media is using the same UI library (Coral 3 (AEM 6.5) or Coral Spectrum (in Skyline)) as entire AEM Assets.  -->

<!-- In the Hotspot editor, Dynamic Media lets you use arrow keys to control the position of a hot spot. See [Carousel Banners](/help/assets/dynamic-media/carousel-banners.md##adding-hotspots-or-image-maps-to-an-image-banner) or [Interactive Images](/help/assets/dynamic-media/interactive-images.md#adding-hotspots-to-an-image-banner)  -->

<!-- I think we should definitely mention this in the DM-specific area of documentation for keyboard support. -->

<!-- I would not get into much of details of specific keyboard support logic of these editors. One of the reasons - chances are that accessibility support will receive Phase2-like attention, with more holistic approach. -->

## Dynamic Media での支援テクノロジーのサポート {#assistive-technology=support-for-dm}

Dynamic Media のユーザーインターフェイス要素は、スクリーンリーダーなどの支援テクノロジーと連携動作します。例えば、キーボードショートカット`D`を使用してランドマークを移動したとき、またはキーボードショートカット`R`を使用して領域を移動したときに、ページのランドマークが認識されます。 また、見出しのキーボードショートカット `H` を使用して移動する際に、見出しの読み上げもおこなわれます。

## Dynamic Media ビューアでのキーボードアクセシビリティのサポート {#keyboard-accessibility-for-dm-viewers}

標準で用意されているすべての Dynamic Media ビューアコンポーネントでは、顧客向けのキーボードアクセシビリティをサポートしています。

『Dynamic Mediaビューアリファレンスガイド』の「[キーボードのアクセシビリティとナビゲーション](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/c-keyboard-accessibility.html)」を参照してください。

## Dynamic Media ビューアでの支援テクノロジーのサポート {#assistive-technology=support-for-dm-viewers}

すべての Dynamic Media ビューアコンポーネントでは、ARIA（アクセシブルリッチインターネットアプリケーション）の役割と属性をサポートして、スクリーンリーダーなどの支援テクノロジーとの統合を強化しています。詳しくは、『Dynamic Media ビューアリファレンスガイド』の「ビューアのカスタマイズ」のトピックで、**支援テクノロジーのサポート**&#x200B;に関するヘルプトピックを参照してください。例えば、ビデオビューアの[支援テクノロジーのサポート](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/viewers-aem-assets-dmc/video/r-html5-video-viewer-20-assistive.html)や、インタラクティブ画像ビューアの[支援テクノロジーのサポート](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/viewers-for-aem-assets-only/interactive-images/c-html5-aem-interactive-image-assistive.html?lang=ja#viewers-for-aem-assets-only)を参照してください。

>[!MORELIKETHIS]
>
>* [アドビソリューションのアクセシビリティ](https://www.adobe.com/accessibility.html)
>* [Adobe Experience Manager Assets でのアクセシビリティ](/help/assets/dynamic-media/accessibility-dm.md)

