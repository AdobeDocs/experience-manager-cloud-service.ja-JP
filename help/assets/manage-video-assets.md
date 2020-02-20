---
title: ビデオアセットの管理
description: ビデオアセットをアップロード、プレビュー、注釈付け、公開する方法について説明します。
contentOwner: AG
translation-type: tm+mt
source-git-commit: 7141e42f53c556c0ac21def6085182ef400f5a71

---


# ビデオアセットの管理 {#manage-video-assets}

Adobe Experience Manager（AEM）Assets でビデオアセットを管理および編集する方法について説明します。ビデオのエンコーディングとトランスコードは、ダイナミックメディア統合でのみ可能です。 ダイナミックメディアを使用しないと、ビデオの基本的なサポートが得られます。例えば、サポートされているファイル形式のプレビューサムネールの抽出や、ブラウザーでの直接の再生に対応した形式のユーザーインターフェイスでのプレビューなどです。

<!-- Also, if you are licensed to use Dynamic Media, see the [Dynamic Media video documentation](/help/assets/dynamic-media/video.md). -->

## Upload and preview video assets {#upload-and-preview-video-assets}

Adobe Experience Manager Assetsは、拡張子がMP4のビデオアセットのプレビューを生成します。 これらのレンディションは、AEM Assets ユーザーインターフェイスでプレビューすることができます。

1. デジタルアセットフォルダー（またはサブフォルダー）で、デジタルアセットを追加する場所に移動します。
1. To upload the asset, click or tap **[!UICONTROL Create]** from the toolbar and choose **[!UICONTROL Files]**. または、ユーザーインターフェイス上でファイルをドラッグします。 詳しくは、ア [セットのアップロード](manage-digital-assets.md#uploading-assets) を参照してください。
1. To preview a video in the Card view, tap the **[!UICONTROL Play]** button on the video asset. ビデオは、カード表示でのみ一時停止または再生できます。 再生ボ [!UICONTROL タン] と一 [!UICONTROL 時停止ボタンは] 、リストビューでは使用できません。
1. To preview the video in the asset details page, click or tap the **[!UICONTROL Edit]** icon on the card. ビデオは、ブラウザーのネイティブなビデオプレーヤーで再生されます。再生、一時停止、音量の調節およびビデオの全画面表示を行うことができます。

## ビデオアセットを公開する {#publish-video-assets}

ビデオアセットを公開すると、URL として Web ページに含めることや、Web ページに埋め込むことができます。See [publishing assets](/help/assets/dynamic-media/publishing-dynamicmedia-assets.md).

## ビデオアセットに注釈を付ける {#annotate-video-assets}

1. From the Assets console, click or tap the [!UICONTROL Edit] icon on the asset card to display the asset details page.
1. To play the video, click or tap the [!UICONTROL Preview] icon.
1. To annotate the video, click the **[!UICONTROL Annotate]** button. 注釈は、ビデオの特定の時点（フレーム）に追加されます。 注釈を作成する場合は、キャンバスに描画し、図面にコメントを含めることができます。 コメントは自動保存されます。 注釈ウィザードを終了するには、「**[!UICONTROL 閉じる]**」をクリックします。
1. Seek to a specific point in the video, specify the time in seconds in the **text** field and click **Jump**. 例えば、ビデオの最初の 20 秒をスキップするには、テキストフィールドに 10 と入力します。
1. タイムラインで表示するには、注釈をクリックします。タイムラインから注釈を削除するには、「**[!UICONTROL 削除]**」をクリックします。
