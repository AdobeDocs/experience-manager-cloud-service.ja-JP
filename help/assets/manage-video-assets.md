---
title: ビデオアセットの管理
description: ビデオアセットをアップロード、プレビュー、注釈付け、公開する方法について説明します。
contentOwner: AG
translation-type: ht
source-git-commit: 0686acbc61b3902c6c926eaa6424828db0a6421a
workflow-type: ht
source-wordcount: '403'
ht-degree: 100%

---


# ビデオアセットの管理{#manage-video-assets}

Adobe Experience Manager（AEM）Assets でビデオアセットを管理および編集する方法について説明します。ビデオのエンコーディングとトランスコード（例えば、Fmpeg トランスコード）は、Dynamic Media 統合でのみ可能です。Dynamic Media を使用しないと、ビデオの基本的なサポートを利用できます。例えば、サポートされているファイル形式のプレビューサムネールの抽出や、ブラウザーでの直接の再生に対応した形式のプレビューが可能です。

<!-- Also, if you are licensed to use Dynamic Media, see the [Dynamic Media video documentation](/help/assets/dynamic-media/video.md). -->

## ビデオアセットのアップロードとプレビュー {#upload-and-preview-video-assets}

Adobe Experience Manager Assets は、拡張子が MP4 のビデオアセットのプレビューを生成します。これらのレンディションは、AEM Assets ユーザーインターフェイスでプレビューすることができます。

1. デジタルアセットフォルダー（またはサブフォルダー）で、デジタルアセットを追加する場所に移動します。
1. アセットをアップロードするには、ツールバーの「**[!UICONTROL 作成]**」をクリックまたはタップして、「**[!UICONTROL ファイル]**」を選択します。または、ユーザーインターフェイス上でファイルをドラッグします。詳しくは、[アセットのアップロード](manage-digital-assets.md#uploading-assets)を参照してください。
1. カード表示でビデオをプレビューするには、ビデオアセットの&#x200B;**[!UICONTROL 再生]**&#x200B;ボタンをタップします。ビデオの一時停止や再生は、カード表示でのみ可能です。リスト表示では、[!UICONTROL 再生]および[!UICONTROL 一時停止]ボタンを使用できません。
1. アセットの詳細ページでビデオをプレビューするには、カードの&#x200B;**[!UICONTROL 編集]**&#x200B;アイコンをクリックまたはタップします。ビデオは、ブラウザーのネイティブなビデオプレーヤーで再生されます。再生、一時停止、音量の調節およびビデオの全画面表示をおこなうことができます。

## ビデオアセットを公開する {#publish-video-assets}

ビデオアセットを公開すると、URL として Web ページに含めることや、Web ページに埋め込むことができます。[アセットの公開](/help/assets/dynamic-media/publishing-dynamicmedia-assets.md)を参照してください。

## ビデオアセットに注釈を付ける {#annotate-video-assets}

1. Assets コンソールで、Assets カードの「[!UICONTROL 編集]」アイコンをクリックまたはタップして、アセットの詳細ページを表示します。
1. ビデオを再生するには、[!UICONTROL プレビュー]アイコンをクリックまたはタップします。
1. ビデオに注釈を付けるには、「**[!UICONTROL 注釈]**」ボタンをクリックします。注釈がビデオ内の特定の時点（フレーム）に追加されます。注釈を付ける際に、キャンバスに描画して、その画像をコメントと一緒に含めることができます。コメントは自動保存されます。注釈ウィザードを終了するには、「**[!UICONTROL 閉じる]**」をクリックします。
1. ビデオ内の特定のポイントを探すには、**テキスト**&#x200B;フィールドに時刻（秒）を指定して、「**ジャンプ**」をクリックします。例えば、ビデオの最初の 20 秒をスキップするには、テキストフィールドに「10」と入力します。
1. タイムラインで表示するには、注釈をクリックします。タイムラインから注釈を削除するには、「**[!UICONTROL 削除]**」をクリックします。
