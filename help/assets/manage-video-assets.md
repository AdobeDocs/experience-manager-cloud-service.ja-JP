---
title: ビデオアセットの管理
description: ビデオアセットをアップロード、プレビュー、注釈付け、公開する方法について説明します。
contentOwner: AG
translation-type: tm+mt
source-git-commit: 991d4900862c92684ed92c1afc081f3e2d76c7ff

---


# ビデオアセットの管理 {#manage-video-assets}

Adobe Experience Manager（AEM）Assets でビデオアセットを管理および編集する方法について説明します。<!-- Also, if you are licensed to use Dynamic Media, see the [Dynamic Media video documentation](/help/assets/dynamic-media/video.md). -->

## Upload and preview video assets {#upload-and-preview-video-assets}

Adobe Experience Manager Assetsは、拡張子がMP4のビデオアセットのプレビューを生成します。アセットの形式がMP4でない場合は、FFMPEGパックをインストールしてプレビューを生成します。FFMPEGは、OGGおよびMP4タイプのビデオレンディションを作成します。 これらのレンディションは、AEM Assets ユーザーインターフェイスでプレビューすることができます。

1. デジタルアセットフォルダー（またはサブフォルダー）で、デジタルアセットを追加する場所に移動します。
1. アセットをアップロードするには、ツールバーの「**[!UICONTROL 作成]**」をクリックまたはタップして、「**[!UICONTROL ファイル]**」を選択します。または、アセット領域に直接ドロップします。See [Uploading assets](manage-digital-assets.md#uploading-assets) for details around the upload operation.
1. To preview a video in the Card view, tap the **[!UICONTROL Play]** button on the video asset. ビデオは、カード表示でのみ一時停止または再生できます。 再生ボ [!UICONTROL タン] と一 [!UICONTROL 時停止ボタンは] 、リストビューでは使用できません。
1. To preview the video in the asset details page, click or tap the **[!UICONTROL Edit]** icon on the card. ビデオは、ブラウザーのネイティブなビデオプレーヤーで再生されます。再生、一時停止、音量の調節およびビデオの全画面表示を行うことができます。

## Configuration to upload assets that are larger than 2 GB {#configuration-to-upload-assets-that-are-larger-than-gb}

デフォルトでは、ファイルサイズの制限により、Experience Manager Assetsでは2 GBを超えるアセットをアップロードできません。 However, you can overwrite this limit by going into CRXDE Lite and creating a node under the `/apps` directory. ノードには、同じノード名とディレクトリ構造および類似した順序のノードプロパティが必要です。

Experience Manager Assets設定に加えて、次の設定を変更し、大きなアセットをアップロードします。

* トークンの有効期限を長くします。 <!-- See [!UICONTROL Adobe Granite CSRF Servlet] in Web Console at `https://[aem_server]:[port]/system/console/configMgr`. For more information, see [CSRF protection](/help/sites-developing/csrf-protection.md). -->
* ディスパッチャ `receiveTimeout` ー設定のを増やします。 詳しくは、 [Experience Manager Dispatcherの設定を参照してください](https://docs.adobe.com/content/help/en/experience-manager-dispatcher/using/configuring/dispatcher-configuration.html#renders-options)。

>[!NOTE]
>
>AEM クラシックユーザーインターフェイスには、2 GB のファイルサイズ上限の制約がありません。また、サイズの大きなビデオでは、エンドツーエンドのワークフローが完全にはサポートされません。

To configure a higher file size limit, perform the following steps in the `/apps` directory.

1. AEM で、**[!UICONTROL ツール]**／**[!UICONTROL 一般]**／**[!UICONTROL CRXDE Lite]** をタップします。
1. In CRXDE Lite, navigate to `/libs/dam/gui/content/assets/jcr:content/actions/secondary/create/items/fileupload`. To see the directory window, touch the `>>` icon.
1. From the toolbar, tap the **[!UICONTROL Overlay Node]**. Alternatively, select **[!UICONTROL Overlay Node]** from the context menu.
1. In the **[!UICONTROL Overlay Node]** dialog, tap **[!UICONTROL OK]**.
1. ブラウザーを更新します。オーバーレイノードが `/jcr_root/apps/dam/gui/content/assets/jcr:content/actions/secondary/create/items/fileupload` 選択されます。
1. In the **[!UICONTROL Properties]** tab, enter the appropriate value in bytes to increase the size limit to the desired size. 例えば、サイズ制限を30 GBに増やすには、値を入力し `{sizeLimit : "32212254720"}` ます。

1. From the toolbar, touch **[!UICONTROL Save All]**.
1. AEM で、**[!UICONTROL ツール]**／**[!UICONTROL 操作]**／**[!UICONTROL Web コンソール]**&#x200B;をタップします。
1. On the Adobe Experience Manager Web Console Bundles page, under the Name column of the table, locate and tap **[!UICONTROL Adobe Granite Workflow External Process Job Handler]**.
1. Adobe Granite Workflow External Process Job Handler ページで、「**[!UICONTROL Default Timeout]**」フィールドと「**[!UICONTROL Max Timeout]**」フィールドの秒数を`18000`（5 時間）に設定します。
1. 「**[!UICONTROL 保存]**」をタップします。
1. AEM で、**[!UICONTROL ツール]**／**[!UICONTROL ワークフロー]**／**[!UICONTROL モデル]**&#x200B;をタップします。
1. ワークフローモデルページで「**[!UICONTROL Dynamic Media エンコーディングビデオ]**」を選択し、「**[!UICONTROL 編集]**」をタップします。
1. ワークフローページで、**[!UICONTROL Dynamic Media ビデオサービスのプロセス]**&#x200B;コンポーネントをダブルタップします。
1. In the [!UICONTROL Step Properties] dialog box, under the **[!UICONTROL Common]** tab, expand **Advanced Settings**.
1. In the **[!UICONTROL Timeout]** field, specify a value of `18000`, then tap **[!UICONTROL OK]** to return to the **[!UICONTROL Dynamic Media Encode Video]** workflow page.
1. ページの上のほうの Dynamic Media エンコーディングビデオページのタイトルの下にある「**[!UICONTROL 保存]**」をタップします。

## ビデオアセットを公開する {#publish-video-assets}

ビデオアセットを公開すると、URL として Web ページに含めることや、Web ページに埋め込むことができます。See [publishing assets](/help/assets/dynamic-media/publishing-dynamicmedia-assets.md).

## ビデオアセットに注釈を付ける {#annotate-video-assets}

1. From the Assets console, click or tap the [!UICONTROL Edit] icon on the asset card to display the asset details page.
1. To play the video, click or tap the [!UICONTROL Preview] icon.
1. To annotate the video, click the **[!UICONTROL Annotate]** button. 注釈は、ビデオの特定の時点（フレーム）に追加されます。 注釈を作成する場合は、キャンバスに描画し、図面にコメントを含めることができます。 コメントは自動保存されます。 注釈ウィザードを終了するには、「**[!UICONTROL 閉じる]**」をクリックします。
1. Seek to a specific point in the video, specify the time in seconds in the **text** field and click **Jump**. 例えば、ビデオの最初の 20 秒をスキップするには、テキストフィールドに 10 と入力します。
1. タイムラインで表示するには、注釈をクリックします。タイムラインから注釈を削除するには、「**[!UICONTROL 削除]**」をクリックします。
