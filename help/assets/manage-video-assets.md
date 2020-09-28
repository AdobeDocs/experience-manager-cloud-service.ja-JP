---
title: ビデオアセットの管理
description: でビデオアセットをアップロード、プレビュー、注釈、公開します [!DNL Adobe Experience Manager]。
contentOwner: AG
translation-type: tm+mt
source-git-commit: 8b1cc8af67c6d12d7e222e12ac4ff77e32ec7e0e
workflow-type: tm+mt
source-wordcount: '539'
ht-degree: 27%

---


# ビデオアセットの管理 {#manage-video-assets}

ビデオ形式は、組織のデジタルアセットの重要な部分です。 [!DNL Adobe Experience Manager] 成熟したオファーは、ビデオアセットの作成後に、ビデオアセットのライフサイクル全体を管理するための製品と機能を提供しています。

Learn how to manage and edit the video assets in [!DNL Adobe Experience Manager Assets]. ビデオのエンコーディングとトランスコーディング、例えば、Fmpegトランスコーディングは、処理プロファイルを使用し、 [!DNL Dynamic Media] 統合を使用して行うことができます。 Without [!DNL Dynamic Media] license, [!DNL Experience Manager] provides basic support for videos, such as transcoding using FFmpeg, extraction of preview thumbnails for the supported file formats, and preview in the user interface for formats that are supported for playback in the browser directly.

## ビデオアセットのアップロードとプレビュー {#upload-and-preview-video-assets}

[!DNL Adobe Experience Manager Assets] 拡張子がMP4のビデオアセットのプレビューを生成します。 You can preview the renditions in the [!DNL Assets] user interface.

1. デジタルアセットフォルダーまたはサブフォルダーで、デジタルアセットを追加する場所に移動します。
1. To upload the asset, click **[!UICONTROL Create]** from the toolbar and choose **[!UICONTROL Files]**. または、ユーザーインターフェイス上でファイルをドラッグします。詳しくは、[アセットのアップロード](manage-digital-assets.md#uploading-assets)を参照してください。
1. To preview a video in the card view, click the **[!UICONTROL Play]** ![play option](assets/do-not-localize/play.png) option on the video asset. ビデオの一時停止や再生は、カード表示でのみ可能です。The [!UICONTROL Play] and [!UICONTROL Pause] options are not available in the list view.
1. To preview the video in the asset details page, select **[!UICONTROL Edit]** on the card. ビデオは、ブラウザーのネイティブなビデオプレーヤーで再生されます。再生、一時停止、音量の調節およびビデオの全画面表示をおこなうことができます。

## ビデオアセットを公開する {#publish-video-assets}

公開後、ビデオアセットをURLとしてWebページに含めたり、アセットを直接埋め込んだりできます。 詳しくは、ダイナミックメディアアセットの [公開を参照してください](/help/assets/dynamic-media/publishing-dynamicmedia-assets.md)。

## 処理プロファイルを使用したトランスコード {#transcode-video}

[!DNL Experience Manager] をCloud Serviceとして使用すると、処理プロファイルを使用してMP4ビデオファイルの基本的なトランスコードを実行できます。 この機能により、アップロードだけでなく、MP4ビデオファイルのプレビューやスケールも可能です。

![Experience Managerでのビデオトランスコードの処理プロファイルの作成](assets/video-processing-profile-for-mp4.png)

*図：でのビデオトランスコードの処理プロファイル[!DNL Experience Manager]です。*

幅のみまたは高さのみを指定し、他のフィールドを空白にした場合、レンディションは縦横比を維持します。 現在、トランスコードに使用できるのはh264コーデックのみです。

処理プロファイルを使用してアセットを処理するには、プロファイルーをフォルダーに追加します。 詳しくは、処理プロファイルを [使用したアセットの処理を参照してください](/help/assets/asset-microservices-configure-and-use.md#use-profiles)。

## ビデオアセットに注釈を付ける {#annotate-video-assets}

1. コン [!DNL Assets] ソールから、アセットカードの「 **[!UICONTROL 編集]** 」を選択して、アセットの詳細ページを表示します。
1. ビデオを再生するには、「 **[!UICONTROL プレビュー]**」をクリックします。
1. To annotate the video, click **[!UICONTROL Annotate]**. ビデオの特定の時間（フレーム）に注釈が追加されます。 注釈を付ける際に、キャンバスに描画して、その画像をコメントと一緒に含めることができます。コメントは自動保存されます。注釈ウィザードを終了するには、「**[!UICONTROL 閉じる]**」をクリックします。
1. ビデオ内の特定のポイントを探すには、**テキスト**&#x200B;フィールドに時刻（秒）を指定して、「**ジャンプ**」をクリックします。例えば、ビデオの最初の 20 秒をスキップするには、テキストフィールドに「20」と入力します。
1. タイムラインで表示するには、注釈をクリックします。タイムラインから注釈を削除するには、「**[!UICONTROL 削除]**」をクリックします。

## ベストプラクティスと制限事項 {#tips-limitations}

* Dynamic Mediaライセンスがない場合、処理プロファイルを使用してMP4ファイルを処理することしかできません。
* を使用した基本的なトランスコード

>[!MORELIKETHIS]
>
>* [ダイナミックメディアビデオドキュメント](/help/assets/dynamic-media/video.md)。
>* [処理プロファイルの使用、タイプ、設定について詳しく知る](/help/assets/asset-microservices-configure-and-use.md)。

