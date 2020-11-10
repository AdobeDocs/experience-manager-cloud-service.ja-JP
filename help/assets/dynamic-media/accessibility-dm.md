---
title: アクセシビリティ [!DNL Dynamic Media]
description: ダイナミックメディアビューアおよびダイナミックメディアビューアのアクセシビリティについて説明します。
contentOwner: Rick Brough
topic-tags: introduction
content-type: reference
translation-type: tm+mt
source-git-commit: 97c53ec4317657beeb3619b2f56915a1e649dd9b
workflow-type: tm+mt
source-wordcount: '618'
ht-degree: 1%

---


# ダイナミックメディアでのアクセシビリティ {#working-with-three-d-assets-dm}

ダイナミックメディアは、オーサリングユーザーインターフェイス全体で、JAWSやNVDAスクリーンリーダーなどのキーボード制御および支援テクノロジーをサポートしています。

## ダイナミックメディアでのキーボードのアクセシビリティのサポート

ダイナミックメディアはAEM Assetsのプラグインなので、キーボードコントロールの動作のほとんどはAEM Assetsの動作とまったく同じです。 例えば、ダイナミックメディアの `Cancel` ボタンは、AEM Assetsと同じフォーカスハイライトを持ち、AEM Assetsと同じ `Spacebar` キーに反応します。 アセットの [キーボードショートカットを参照してください](/help/assets/accessibility.md#keyboard-shortcuts)。

ダイナミックメディアの個々のユーザーインターフェイス要素でサポートされているキーストロークは、ほとんどの場合、明確で見つけやすいものです。 ダイナミックメディアのキーボードコントロールは、次の点について説明します。

* ページ上のインタラクティブな要素間を移動する際に、キーストローク `Tab``Shift+Tab` とキーストロークを使用する機能。
入力フォーカスを使用すると、タブ順序内の次のユーザーインターフェイス要素に進みます。 `Tab` を使用す `Shift+Tab` ると、入力フォーカスが前のユーザーインターフェイス要素に戻ります。
フォーカストラバーサルは、画面上の自然なユーザインターフェイス要素の位置に従い、左から右、上から下の順に移動します。 また、エラーのあるフィールドがある場合は、を押してフォーカス `Tab` をそのフィールドに移動できます。
* ボタン、ドロップダウンリストなどの標準的なユーザインターフェイス要素をアクティブにするために、 `Spacebar` および `Enter` キーを使用できます。
* アクティブな要素でキーボードのフォーカスハイライトを確認する機能。 入力フォーカスを有するユーザインターフェイス要素は、ユーザインターフェイス要素の周りにレンダリングされた境界として視覚的なフォーカス表示を受け取ることができる。
* ホットスポットエディタでは、矢印キーなどのカスタムキーストロークを使用して複雑なユーザインターフェイス要素を操作し、ホットスポットの位置を変更できます。
* インタラクティブビデオエディタで、を使用して画像 `Spacebar` を選択し、セグメントに追加できます。 また、 `Backspace` キーを使用して、「 **[!UICONTROL コンテンツ]** 」タブから選択したアイテムを削除できます。 また、必要に応じて `Tab` 機能を押し、ページ上のインタラクティブ要素間を移動します。
* 画像切り抜き/スマート切り抜きエディタでは、次の操作を実行できます。
   * フレームサイズを切り抜く、画像の位置を変更する、またはその両方には矢印キーを使用します。
   * 最初の `Tab` 停止ボタンで、画像フレーム全体がハイライトされます。 その後、キーボードの矢印キーを使用してフレームの位置を変更できます。
   * 次の4つの `Tab` ストップは、フレームの四隅です。 フレームの隅にフォーカスを置くと、隅がハイライトされます。 キーボードの矢印キーを使用して、フォーカスを移動できます。
See [Editing the smart crop or smart swatch of a single image](/help/assets/dynamic-media/image-profiles.md#editing-the-smart-crop-or-smart-swatch-of-a-single-image)

<!-- Keyboarding is the same because Dynamic Media is using the same UI library (Coral 3 (AEM 6.5) or Coral Spectrum (in Skyline)) as entire AEM Assets.  -->

<!-- In the Hotspot editor, Dynamic Media lets you use arrow keys to control the position of a hot spot. See [Carousel Banners](/help/assets/dynamic-media/carousel-banners.md##adding-hotspots-or-image-maps-to-an-image-banner) or [Interactive Images](/help/assets/dynamic-media/interactive-images.md#adding-hotspots-to-an-image-banner)  -->

<!-- I think we should definitely mention this in the DM-specific area of documentation for keyboard support. -->

<!-- I would not get into much of details of specific keyboard support logic of these editors. One of the reasons - chances are that accessibility support will receive Phase2-like attention, with more holistic approach. -->

## ダイナミックメディアでの支援テクノロジーのサポート {#assistive-technology=support-for-dm}

ダイナミックメディアのユーザインターフェイス要素は、スクリーンリーダーなどの支援テクノロジーと連携します。 例えば、キーボードショートカットを使用してランドマークをナビゲートしたとき、またはキーボードショートカットを使用して領域を移動したときに、ページのランドマーク `D` が認識され `R`ます。 また、見出しのキーボードショートカットを使用して移動する際に、見出しのナレーションも行 `H`います。

## ダイナミックメディアビューアでのキーボードのアクセシビリティのサポート {#keyboard-accessibility-for-dm-viewers}

すべての標準搭載のダイナミックメディアビューアコンポーネントは、ユーザーにとってキーボードのアクセシビリティをサポートします。

詳しくは、『Dynamic Media Viewersリファレンスガイド』の [キーボードのアクセシビリティとナビゲーション](https://docs.adobe.com/content/help/en/dynamic-media-developer-resources/library/c-keyboard-accessibility.html) （英語のみ）を参照してください。

## Dynamic Media Viewerでの支援テクノロジーのサポート {#assistive-technology=support-for-dm-viewers}

すべてのダイナミックメディアビューアコンポーネントは、ARIA(Accessible Rich Internet Applications)の役割と属性をサポートしており、スクリーンリーダーなどの支援テクノロジーとの統合を強化します。
Dynamic Media Viewersリファレンスガイドの **Viewerのカスタマイズに関するトピックで、** 支援テクノロジーサポート・ヘルプ・トピックを参照してください。 例えば、ビデオビューアの [支援技術サポート](https://docs.adobe.com/content/help/en/dynamic-media-developer-resources/library/viewers-aem-assets-dmc/video/r-html5-video-viewer-20-assistive.html) （英語）またはインタラクティブ画像ビューアの [支援技術サポート](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/viewers-for-aem-assets-only/interactive-images/c-html5-aem-interactive-image-assistive.html?lang=en#viewers-for-aem-assets-only) （英語）を参照してください。

>[!MORELIKETHIS]
>
>* [Adobeソリューションのアクセシビリティ](https://www.adobe.com/accessibility.html)
>* [Experience Managerアセット内のアクセシビリティ](/help/assets/dynamic-media/accessibility-dm.md)

