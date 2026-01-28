---
title: Dynamic Media のアクセシビリティ
description: ビデオのエンコーディング、YouTubeへのビデオの公開に関するベストプラクティスなど、Dynamic Media でビデオを操作する方法について説明します。 また、ビデオにクローズドキャプション、キャプション、チャプターマーカーを追加する方法についても説明します。
contentOwner: Rick Brough
topic-tags: introduction
content-type: reference
feature: Accessibility
role: Admin,User
exl-id: f8d2dcbf-f61a-4b27-a3fc-406e3662adcb
source-git-commit: 4a09e74ae62dba40deb192b1dfe38860bdb43921
workflow-type: tm+mt
source-wordcount: '636'
ht-degree: 91%

---

# Dynamic Media のアクセシビリティ {#accessibility-in-dm}

{{work-with-dynamic-media}}

Dynamic Media では、オーサリングユーザーインターフェイス全体でキーボードコントロールおよび支援テクノロジー（JAWS スクリーンリーダーや NVDA スクリーンリーダーなど）をサポートしています。

## Dynamic Media でのキーボードアクセシビリティのサポート {#keyboard-support-in-dm}

Dynamic Media は Adobe [!DNL Experience Manager Assets] のプラグインなので、キーボードコントロールの動作のほとんどは [!DNL Experience Manager Assets] の場合と同じです。例えば、Dynamic Media の「`Cancel`」ボタンのフォーカスハイライトは [!DNL Experience Manager Assets] と同じです。また、[!DNL Experience Manager Assets] の場合と同様に `Spacebar` キーにも反応します。[Assets のキーボードショートカット](/help/assets/accessibility.md#keyboard-shortcuts)を参照してください。

Dynamic Media の個々のユーザーインターフェイス要素でサポートされているキー操作は、ほとんどの場合、明確で見つけやすくなっています。Dynamic Media のキーボードコントロールは、以下の機能があります。

* `Tab` と `Shift+Tab` のキー操作を使用して、ページ上のインタラクティブ要素間を移動できます。`Tab` を使用すると、タブ順序における次のユーザーインターフェイス要素に入力フォーカスが進みます。`Shift+Tab` を使用すると、入力フォーカスが前のユーザーインターフェイス要素に戻ります。フォーカストラバーサルは、画面上のユーザーインターフェイス要素の自然な位置に従い、左から右、上から下の順序で移動します。また、フィールドにエラーがある場合は、`Tab` を押して、そのフィールドにフォーカスを移動できます。
* `Spacebar` キーと `Enter` キーを使用して、ボタン、ドロップダウンリストなどの標準的なユーザーインターフェイス要素をアクティブにできます。
* アクティブな要素にキーボードフォーカスのハイライト表示を行えます。入力フォーカスのあるユーザーインターフェイス要素には、その要素の周りにボーダーをレンダリングして視覚的なフォーカス表示を行うことができます。
* ホットスポットエディターでは、矢印キーなどのいくつかのカスタムキー操作を使用して複雑なユーザーインターフェイス要素を操作し、ホットスポットの位置を変更できます。
* インタラクティブビデオエディターでは、`Spacebar` を使用して画像を選択し、それをセグメントに追加できます。さらに、`Backspace` キーを使用して、選択した項目を「**[!UICONTROL コンテンツ]**」タブから削除できます。また、必要に応じて `Tab` キーを押して、ページ上のインタラクティブ要素間を移動できます。
* 画像切り抜き／スマート切り抜きエディターで、次の操作を実行できます。
   * 矢印キーを使用して、フレームサイズの切り抜きや画像位置の変更、またはその両方を行います。
   * 最初の `Tab` ストップで画像フレーム全体がハイライト表示されます。その後、キーボードの矢印キーを使用してフレームの位置を変更できます。
   * その次の 4 つの `Tab` ストップはフレームの四隅です。フレームの隅をフォーカスすると、その隅がハイライト表示されます。この場合も、キーボードの矢印キーを使用して、フォーカスされた隅を移動できます。詳しくは、[単一の画像のスマート切り抜きまたはスマートスウォッチの編集](/help/assets/dynamic-media/image-profiles.md#editing-the-smart-crop-or-smart-swatch-of-a-single-image)を参照してください。

<!-- Keyboarding is the same because Dynamic Media is using the same UI library (Coral 3 (Experience Manager 6.5) or Coral Spectrum (in Skyline)) as entire Experience Manager Assets.  -->

<!-- In the Hotspot editor, Dynamic Media lets you use arrow keys to control the position of a hot spot. See [Carousel Banners](/help/assets/dynamic-media/carousel-banners.md#adding-hotspots-or-image-maps-to-an-image-banner) or [Interactive Images](/help/assets/dynamic-media/interactive-images.md#adding-hotspots-to-an-image-banner)  -->

<!-- I think we should definitely mention this in the DM-specific area of documentation for keyboard support. -->

<!-- I would not get into much of details of specific keyboard support logic of these editors. One of the reasons - chances are that accessibility support will receive Phase2-like attention, with more holistic approach. -->

## Dynamic Media での支援テクノロジーのサポート {#assistive-technology=support-for-dm}

Dynamic Media のユーザーインターフェイス要素は、スクリーンリーダーなどの支援テクノロジーと連携動作します。例えば、キーボードショートカット `D` を使用してランドマークを移動するときや、キーボードショートカット `R` を使用して領域を移動するときに、ページのランドマークが認識されます。また、見出しのキーボードショートカット `H` を使用して移動する際に、見出しの読み上げも行われます。

## Dynamic Media ビューアでのキーボードアクセシビリティのサポート {#keyboard-accessibility-for-dm-viewers}

標準で用意されているすべての Dynamic Media ビューアコンポーネントでは、顧客向けのキーボードアクセシビリティをサポートしています。

詳しくは、『Dynamic Media ビューアリファレンスガイド』の[キーボードのアクセシビリティとナビゲーション](https://experienceleague.adobe.com/ja/docs/dynamic-media-developer-resources/library/c-keyboard-accessibility#)を参照してください。

## Dynamic Media ビューアでの支援テクノロジーのサポート {#assistive-technology=support-for-dm-viewers}

すべての Dynamic Media ビューアコンポーネントでは、ARIA（アクセシブルリッチインターネットアプリケーション）の役割と属性をサポートして、スクリーンリーダーなどの支援テクノロジーとの統合を強化しています。詳しくは、『Dynamic Media ビューアリファレンスガイド』の「ビューアのカスタマイズ」のトピックで、**支援テクノロジーのサポート**&#x200B;に関するヘルプトピックを参照してください。例えば、ビデオビューアの[支援テクノロジーのサポート](https://experienceleague.adobe.com/ja/docs/dynamic-media-developer-resources/library/viewers-aem-assets-dmc/video/r-html5-video-viewer-20-assistive#)や、インタラクティブ画像ビューアの[支援テクノロジーのサポート](https://experienceleague.adobe.com/ja/docs/dynamic-media-developer-resources/library/viewers-for-aem-assets-only/interactive-images/c-html5-aem-interactive-image-assistive#viewers-for-aem-assets-only)を参照してください。

## [!DNL Dynamic Media] でのクローズドキャプションのサポート {#closed-caption-support}

Dynamic Media では、クローズドキャプションを使用したビデオとアダプティブビデオセットの配信がサポートされています。キャプションは、ビデオコンテンツの上に表示する必要があります。

[Dynamic Media のビデオ - ビデオへのクローズドキャプションの追加](/help/assets/dynamic-media/video.md#adding-captions-to-video)を参照してください。


>[!MORELIKETHIS]
>
>* [アドビソリューションのアクセシビリティ](https://www.adobe.com/trust/accessibility.html)
>* [Adobe Experience Manager Assets でのアクセシビリティ](/help/assets/dynamic-media/accessibility-dm.md)
