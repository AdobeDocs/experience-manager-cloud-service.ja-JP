---
title: ビデオアセットの管理
description: ' [!DNL Adobe Experience Manager] でビデオアセットをアップロード、プレビュー、注釈、公開します。'
contentOwner: AG
translation-type: tm+mt
source-git-commit: deab2183447e64e8a98f3072ceab2ef2216c4528
workflow-type: tm+mt
source-wordcount: '619'
ht-degree: 80%

---


# ビデオアセットの管理 {#manage-video-assets}

ビデオ形式は、組織のデジタルアセットの重要な部分です。[!DNL Adobe Experience Manager] は、ビデオアセットの作成後に、ビデオアセットのライフサイクル全体を管理するための充実した機能を提供しています。

[!DNL Adobe Experience Manager Assets] でビデオアセットを管理および編集する方法について説明します。ビデオのエンコーディングとトランスコーディング、例えば、FFmpeg トランスコーディングは、処理プロファイルを使用し、[!DNL Dynamic Media] 統合を使用しておこなうことができます。[!DNL Experience Manager] は、[!DNL Dynamic Media] ライセンスを使用せずにビデオの基本的なサポートを提供します。例えば、FFmpeg によるトランスコード、サポートされているファイル形式のプレビューサムネールの抽出、ブラウザーでの直接の再生に対応した形式のプレビューなどが可能です。

## ビデオアセットのアップロードとプレビュー {#upload-and-preview-video-assets}

[!DNL Adobe Experience Manager Assets] は、拡張子が MP4 のビデオアセットのプレビューを生成します。これらのレンディションは、[!DNL Assets] ユーザーインターフェイスでプレビューできます。

1. デジタルアセットフォルダー（またはサブフォルダー）で、デジタルアセットを追加する場所に移動します。
1. アセットをアップロードするには、ツールバーの「**[!UICONTROL 作成]**」をクリックして、「**[!UICONTROL ファイル]**」を選択します。または、ユーザーインターフェイス上でファイルをドラッグします。詳しくは、[アセットのアップロード](manage-digital-assets.md#uploading-assets)を参照してください。
1. カード表示でビデオをプレビューするには、ビデオアセットの&#x200B;**[!UICONTROL 再生]**![再生オプション](assets/do-not-localize/play.png)オプションをクリックします。ビデオの一時停止や再生は、カード表示でのみ可能です。リスト表示では、[!UICONTROL 再生]および[!UICONTROL 一時停止]オプションを使用できません。
1. アセットの詳細ページでビデオをプレビューするには、カードの&#x200B;**[!UICONTROL 編集]**&#x200B;アイコンを選択します。ビデオは、ブラウザーのネイティブなビデオプレーヤーで再生されます。再生、一時停止、音量の調節およびビデオの全画面表示をおこなうことができます。

## ビデオアセットを公開する {#publish-video-assets}

公開後、ビデオアセットを URL として Web ページに含めたり、アセットを直接埋め込んだりできます。詳しくは、[発行 [!DNL Dynamic Media] アセット](/help/assets/dynamic-media/publishing-dynamicmedia-assets.md)を参照してください。

## 処理プロファイルを使用したトランスコード {#transcode-video}

[!DNL Experience Manager] as a [!DNL Cloud Service] では、処理プロファイルを使用して MP4 ビデオファイルの基本的なトランスコードを実行できます。この機能により、アップロードだけでなく、MP4 ビデオファイルのプレビューやスケールも可能です。

![ビデオトランスコードの処理プロファイルを  [!DNL Experience Manager]](assets/video-processing-profile-for-mp4.png)

*図：[!DNL Experience Manager] でのビデオトランスコードの処理プロファイル。*

幅または高さのみを指定して、その他のフィールドを空白にした場合、レンディションは縦横比を維持します。H.264ビデオコーデックはトランスコードに使用できます。

処理プロファイルを使用してアセットを処理するには、プロファイルをフォルダーに追加します。詳しくは、[処理プロファイルを使用したアセットの処理](/help/assets/asset-microservices-configure-and-use.md#use-profiles)を参照してください。

## ビデオアセットに注釈を付ける {#annotate-video-assets}

1. [!DNL Assets] コンソールから、アセットカードの「**[!UICONTROL 編集]**」を選択して、アセット詳細ページを表示します。
1. ビデオを再生するには、「**[!UICONTROL プレビュー]**」をクリックします。
1. ビデオに注釈を付けるには、「**[!UICONTROL 注釈]**」をクリックします。注釈がビデオ内の特定の時点（フレーム）に追加されます。注釈を付ける際に、キャンバスに描画して、その画像をコメントと一緒に含めることができます。コメントは自動保存されます。注釈ウィザードを終了するには、「**[!UICONTROL 閉じる]**」をクリックします。
1. ビデオ内の特定のポイントを探すには、**テキスト**&#x200B;フィールドに時刻（秒）を指定して、「**ジャンプ**」をクリックします。例えば、ビデオの最初の 20 秒をスキップするには、テキストフィールドに「20」と入力します。
1. タイムラインで表示するには、注釈をクリックします。タイムラインから注釈を削除するには、「**[!UICONTROL 削除]**」をクリックします。

## ベストプラクティスと制限事項 {#tips-limitations}

* [!DNL Dynamic Media]ライセンスがない場合は、処理プロファイルを使用したMP4ファイルのみを処理できます。
* 処理プロファイルを使用してMP4ファイルをトランスコードする場合、次のガイドラインと制限が適用されます。

   * Apple ProResファイルは、最大解像度1080pにのみトランスコードできます。
   * ソースファイルのビットレートが200 Mbpsを超える場合は、最大解像度1080pにのみトランスコードできます。
   * その後、ソースフレームレート>=60 fpsの場合、使用できるソースファイルの最大サイズは、次のとおりです。

      * 4,000 MB（4,000 MBのトランスコード用）
      * 800 MB（1080pトランスコード用）。
      * 8 GB（720pトランスコード用）
   * 4k解像度にトランスコードできる最大ファイルサイズは、解像度4k、ビットレート12 Mbps、23 fpsの2.55 GB MP4ファイルです。


>[!MORELIKETHIS]
>
>* [Dynamic Media ビデオドキュメント。](/help/assets/dynamic-media/video.md)
>* [処理プロファイルの使用、タイプ、設定について詳しく知る](/help/assets/asset-microservices-configure-and-use.md)。

