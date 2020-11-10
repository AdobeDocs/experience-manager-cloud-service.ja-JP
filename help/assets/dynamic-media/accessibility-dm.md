---
title: アクセシビリティ [!DNL Dynamic Media]
description: Dynamic Media で 3D アセットを使用する方法について説明します。
contentOwner: Rick Brough
topic-tags: introduction
content-type: reference
translation-type: tm+mt
source-git-commit: d992b68d4a015f8f947167b5b1d5f0a1ac5c09ec
workflow-type: tm+mt
source-wordcount: '469'
ht-degree: 3%

---


# ダイナミックメディアでのアクセシビリティ {#working-with-three-d-assets-dm}

ダイナミックメディアは、オーサリングユーザーインターフェイス全体で、JAWSやNVDAスクリーンリーダーなどのキーボード制御および支援テクノロジーをサポートしています。

## ダイナミックメディアでのキーボードのアクセシビリティのサポート

個々のユーザーインターフェイス要素でサポートされているキーストロークは、ほとんどの場合、明確で見つけやすいものです。 ダイナミックメディアのキーボードコントロールは、次の点について説明します。

* ページ上のインタラクティブな要素間を移動する際に、キーストローク `Tab``Shift+Tab` とキーストロークを使用する機能。
入力フォーカスを使用すると、タブ順序内の次のユーザーインターフェイス要素に進みます。 `Tab` を使用す `Shift+Tab` ると、入力フォーカスが前のユーザーインターフェイス要素に戻ります。
フォーカストラバーサルは、画面上の自然なユーザインターフェイス要素の位置に従い、左から右、上から下の順に移動します。
* ボタン、ドロップダウンリストなどの標準的なユーザインターフェイス要素をアクティブにするために、 `Spacebar` および `Enter` キーを使用できます。
* ホットスポットエディターの矢印キーなど、複雑なUI要素を操作するためにカスタムのキー操作を使用する機能。
* アクティブな要素でキーボードのフォーカスハイライトを確認する機能。 入力フォーカスを有するユーザインターフェイス要素は、ユーザインターフェイス要素の周りにレンダリングされた境界として視覚的なフォーカス表示を受け取ることができる。

ダイナミックメディアはAEM Assetsのプラグインなので、キーボードコントロールの動作のほとんどはAEM Assetsの動作とまったく同じです。 例えば、ダイナミックメディアの `Cancel` ボタンは、AEM Assetsと同じフォーカスハイライトを持ち、AEM Assetsと同じ `Spacebar` キーに反応します。 アセットの [キーボードショートカットを参照してください](/help/assets/accessibility.md#keyboard-shortcuts)。 ただし、ホットスポットエディタや画像切り抜き/スマート切り抜きエディタは例外です。

<!-- Keyboarding is the same because Dynamic Media is using the same UI library (Coral 3 (AEM 6.5) or Coral Spectrum (in Skyline)) as entire AEM Assets.  -->

ホットスポットエディタでは、ダイナミックメディアで矢印キーを使用してホットスポットの位置を制御できます。 カルーセル [バナー](/help/assets/dynamic-media/carousel-banners.md##adding-hotspots-or-image-maps-to-an-image-banner) またはインタラクティブ [画像を参照してください。](/help/assets/dynamic-media/interactive-images.md#adding-hotspots-to-an-image-banner)

画像切り抜き/スマート切り抜きエディタで、矢印キーを使用してフレームサイズを切り抜いたり、画像の位置を変更したりします。 See [Editing the smart crop or smart swatch of a single image](/help/assets/dynamic-media/image-profiles.md#editing-the-smart-crop-or-smart-swatch-of-a-single-image)

<!-- I think we should definitely mention this in the DM-specific area of documentation for keyboard support. -->

<!-- I would not get into much of details of specific keyboard support logic of these editors. One of the reasons - chances are that accessibility support will receive Phase2-like attention, with more holistic approach. -->

## ダイナミックメディアビューアのキーボードアクセシビリティのサポート {#keyboard-accessibility-for-dm-viewers}

すべての標準搭載のダイナミックメディアビューアコンポーネントは、ユーザーにとってキーボードのアクセシビリティをサポートします。

詳しくは、『Dynamic Media Viewersリファレンスガイド』の [キーボードのアクセシビリティとナビゲーション](https://docs.adobe.com/content/help/en/dynamic-media-developer-resources/library/c-keyboard-accessibility.html) （英語のみ）を参照してください。

## Dynamic Media Viewerの支援テクノロジーのサポート {#assistive-technology=support-for-dm-viewers}

ダイナミックメディアのすべてのビューアコンポーネントは、ARIA(Accessible Rich Internet Applications)のロールと属性をサポートしており、スクリーンリーダーなどの支援テクノロジーとの統合を強化します。

Dynamic Media Viewersリファレンスガイドの **Viewerのカスタマイズに関するトピックで、** 支援テクノロジーサポート・ヘルプ・トピックを参照してください。 例えば、ビデオビューアの [支援技術サポート](https://docs.adobe.com/content/help/en/dynamic-media-developer-resources/library/viewers-aem-assets-dmc/video/r-html5-video-viewer-20-assistive.html) （英語）またはインタラクティブ画像ビューアの [支援技術サポート](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/viewers-for-aem-assets-only/interactive-images/c-html5-aem-interactive-image-assistive.html?lang=en#viewers-for-aem-assets-only) （英語）を参照してください。

>[!MORELIKETHIS]
>
>* [Adobeソリューションのアクセシビリティ](https://www.adobe.com/accessibility.html)
>* [Experience Managerアセット内のアクセシビリティ](/help/assets/dynamic-media/accessibility-dm.md)

