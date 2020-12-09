---
title: ' [!DNL Dynamic Media] でのアクセシビリティ'
description: Dynamic MediaおよびDynamic MediaのViewerでのアクセシビリティについて説明します。
contentOwner: Rick Brough
topic-tags: introduction
content-type: reference
translation-type: tm+mt
source-git-commit: fd75af0bf0c16e20c3b98703af14f329ea6c6371
workflow-type: tm+mt
source-wordcount: '622'
ht-degree: 1%

---


# Dynamic Media{#working-with-three-d-assets-dm}でのアクセシビリティ

Dynamic Mediaは、オーサリングユーザーインターフェイス全体で、JAWSやNVDAのスクリーンリーダーなどのキーボード制御および支援テクノロジーをサポートしています。

## Dynamic Mediaでのキーボードのアクセシビリティのサポート

Dynamic MediaはExperience Managerアセットのプラグインなので、キーボードコントロールの動作のほとんどはExperience Managerアセットの動作とまったく同じです。 例えば、Dynamic Mediaの`Cancel`ボタンは、Experience Managerアセットと同じフォーカスハイライトを持ち、Experience Managerアセットと同じ`Spacebar`キーに反応します。 詳しくは、[アセットのキーボードショートカット](/help/assets/accessibility.md#keyboard-shortcuts)を参照してください。

Dynamic Mediaの個々のユーザーインターフェイス要素でサポートされているキーストロークは、ほとんどの場合、明確で見つけやすいものです。 Dynamic Mediaのキーボードコントロールは、次の点に関するものです。

* `Tab`と`Shift+Tab`のキー操作を使用して、ページ上のインタラクティブな要素間を移動する機能。
`Tab`を使用すると、入力フォーカスがタブ順序の次のユーザーインターフェイス要素に進みます。`Shift+Tab`を使用すると、入力フォーカスが前のユーザーインターフェイス要素に戻ります。
フォーカストラバーサルは、画面上の自然なユーザインターフェイス要素の位置に従い、左から右、上から下の順に移動します。 また、エラーのあるフィールドがある場合は、`Tab`を押してフォーカスを移動できます。
* `Spacebar`キーと`Enter`キーを使用して、ボタン、ドロップダウンリストなどの標準的なユーザインターフェイス要素をアクティブにする機能。
* アクティブな要素でキーボードのフォーカスハイライトを確認する機能。 入力フォーカスを有するユーザインターフェイス要素は、ユーザインターフェイス要素の周りにレンダリングされた境界として視覚的なフォーカス表示を受け取ることができる。
* ホットスポットエディタでは、矢印キーなどのカスタムキーストロークを使用して複雑なユーザインターフェイス要素を操作し、ホットスポットの位置を変更できます。
* インタラクティブビデオエディターでは、`Spacebar`を使用して画像を選択し、セグメントに追加できます。 さらに、`Backspace`キーを使用して、「**[!UICONTROL コンテンツ]**」タブから選択したアイテムを削除できます。 また、必要に応じて`Tab`キーを押して、ページ上のインタラクティブ要素間を移動します。
* 画像切り抜き/スマート切り抜きエディタでは、次の操作を実行できます。
   * フレームサイズを切り抜く、画像の位置を変更する、またはその両方には矢印キーを使用します。
   * 最初の`Tab`ストップで画像フレーム全体がハイライトされます。 その後、キーボードの矢印キーを使用してフレームの位置を変更できます。
   * 次の4つの`Tab`ストップは、フレームの四隅です。 フレームの隅にフォーカスを置くと、隅がハイライトされます。 キーボードの矢印キーを使用して、フォーカスを移動できます。
[単一の画像のスマート切り抜きまたはスマートスウォッチの編集](/help/assets/dynamic-media/image-profiles.md#editing-the-smart-crop-or-smart-swatch-of-a-single-image)を参照してください。

<!-- Keyboarding is the same because Dynamic Media is using the same UI library (Coral 3 (AEM 6.5) or Coral Spectrum (in Skyline)) as entire AEM Assets.  -->

<!-- In the Hotspot editor, Dynamic Media lets you use arrow keys to control the position of a hot spot. See [Carousel Banners](/help/assets/dynamic-media/carousel-banners.md##adding-hotspots-or-image-maps-to-an-image-banner) or [Interactive Images](/help/assets/dynamic-media/interactive-images.md#adding-hotspots-to-an-image-banner)  -->

<!-- I think we should definitely mention this in the DM-specific area of documentation for keyboard support. -->

<!-- I would not get into much of details of specific keyboard support logic of these editors. One of the reasons - chances are that accessibility support will receive Phase2-like attention, with more holistic approach. -->

## Dynamic Media{#assistive-technology=support-for-dm}の支援テクノロジーサポート

Dynamic Mediaのユーザインターフェイス要素は、スクリーンリーダーなどの支援テクノロジーと連携します。 例えば、キーボードショートカット`D`を使用してランドマークを移動したとき、またはキーボードショートカット`R`を使用して領域を移動したときに、ページのランドマークが認識されます。 また、見出しのキーボードショートカット`H`を使用してナビゲートする際に、見出しのナレーションも行います。

## Dynamic Mediaビューアでのキーボードのアクセシビリティのサポート{#keyboard-accessibility-for-dm-viewers}

すべての標準搭載のDynamic Mediaビューアコンポーネントは、お客様向けのキーボードアクセシビリティをサポートしています。

『Dynamic Mediaビューアリファレンスガイド』の[キーボードのアクセシビリティとナビゲーション](https://docs.adobe.com/content/help/ja-JP/dynamic-media-developer-resources/library/c-keyboard-accessibility.html)を参照してください。

## Dynamic Mediaビューアで支援テクノロジーがサポート{#assistive-technology=support-for-dm-viewers}

すべてのDynamic Mediaビューアコンポーネントは、ARIA(Accessible Rich Internet Applications)の役割と属性をサポートしており、スクリーンリーダーなどの支援テクノロジーとの統合を強化しています。
『Dynamic Mediaビューアリファレンスガイド』の「ビューアのカスタマイズ」トピックで、**支援テクノロジサポート**&#x200B;ヘルプトピックを参照してください。 例えば、ビデオビューアの場合は[支援テクノロジーのサポート](https://docs.adobe.com/content/help/en/dynamic-media-developer-resources/library/viewers-aem-assets-dmc/video/r-html5-video-viewer-20-assistive.html)を、インタラクティブ画像ビューアの場合は[支援テクノロジーのサポート](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/viewers-for-aem-assets-only/interactive-images/c-html5-aem-interactive-image-assistive.html?lang=en#viewers-for-aem-assets-only)を参照してください。

>[!MORELIKETHIS]
>
>* [Adobeソリューションのアクセシビリティ](https://www.adobe.com/accessibility.html)
>* [Experience Managerアセット内のアクセシビリティ](/help/assets/dynamic-media/accessibility-dm.md)

