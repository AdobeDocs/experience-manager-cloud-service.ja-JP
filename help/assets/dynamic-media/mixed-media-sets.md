---
title: 混在メディアセット
description: ダイナミックメディアで混在メディアセットを操作する方法を説明します。
translation-type: tm+mt
source-git-commit: 6224d193adfb87bd9b080f48937e0af1f03386d6

---


# 混在メディアセット{#mixed-media-sets}

混在メディアセットは、画像、画像セット、スピンセットおよびビデオを 1 つのプレゼンテーションで混在させて表示するものです。

混在メディアセットのバナーには、「**[!UICONTROL MixedMediaSet]**」と表示されます。また、混在メディアセットが発行されている場合、発行日が&#x200B;**[!UICONTROL 地球]**&#x200B;アイコン付きでバナーに表示され、最終変更日も&#x200B;**[!UICONTROL 鉛筆]**&#x200B;アイコン付きで表示されます。

![chlimage_1-137](assets/chlimage_1-348.png)

>[!NOTE]
>
>アセットユーザーインターフェイスについて詳しくは、[タッチ UI を使用したアセットの管理](/help/assets/manage-digital-assets.md)を参照してください。

## クイックスタート：混在メディアセット {#quick-start-mixed-media-sets}

混在メディアセットをすぐに使い始めるには、次の手順を実行します。

1. [アセットをアップロードします](#uploading-assets)。

   まずは混在メディアセット用の画像およびビデオをアップロードします。必要に応じて、[画像セット](/help/assets/dynamic-media/image-sets.md)と[スピンセット](/help/assets/dynamic-media/spin-sets.md)を作成します。ユーザーは混在メディアセットビューアで画像をズームできるので、画像を選択する際にはズームを考慮します。最大サイズで 2,000 ピクセル以上の画像を使用してください。

1. [混在メディアセットを作成します。](#creating-mixed-media-sets)

   To create a Mixed Media Set, from the Assets page, tap **[!UICONTROL Create > Mixed Media Set]** and then name the set, choose the assets, and choose the order the images appear.

   [セレクターの操作](/help/assets/dynamic-media/working-with-selectors.md)を参照してください。

1. Set up [Mixed Media Viewer presets](/help/assets/dynamic-media/managing-viewer-presets.md), as needed.

   管理者は、混在メディアセットビューアプリセットを作成または編集できます。To see your mixed media with a viewer preset, select the mixed media set, and in the left-rail drop-down menu, select **[!UICONTROL Viewers]**.

   See **[!UICONTROL Tools > Assets > Viewer Presets]** to create or edit viewer presets.

   See [Adding and editing viewer presets.](/help/assets/dynamic-media/managing-viewer-presets.md)

1. [混在メディアセットをプレビューします。](#previewing-mixed-media-sets)

   混在メディアセットを選択すると、プレビューできます。サムネールアイコンをクリックして、選択したビューアでの混在メディアセットの表示を確認します。You can choose different Viewers from the **[!UICONTROL Viewers]** menu, available from the left rail drop-down menu.

1. [混在メディアセットを公開します。](#publishing-mixed-media-sets)

   混在メディアセットを公開すると、URL と埋め込み文字列がアクティベートされます。In addition, you must [publish the viewer preset](/help/assets/dynamic-media/managing-viewer-presets.md#publishing-viewer-presets).

1. [URL を Web アプリケーションにリンクする](/help/assets/dynamic-media/linking-urls-to-yourwebapplication.md)か、[ビデオビューアまたは画像ビューアを埋め込みます](/help/assets/dynamic-media/embed-code.md)。

   混在メディアセットの URL コールが作成され、混在メディアセットの公開後にそれらの URL コールがアクティベートされます。アセットをプレビューする際に、これらの URL をコピーできます。または、URL を Web サイトに埋め込むこともできます。

   Select the Mixed Media Set, then in the left rail drop-down menu, select **[!UICONTROL Viewers]**.

   See [Linking a Mixed Media Set to a web page](/help/assets/dynamic-media/linking-urls-to-yourwebapplication.md) and [Embedding the Video or Image Viewer](/help/assets/dynamic-media/embed-code.md).

必要に応じて、[混在メディアセット](#editing-mixed-media-sets)を編集できます。In addition, you can view and modify [Mixed Media Set properties](/help/assets/manage-digital-assets.md#editing-properties).

>[!NOTE]
>
>If you have issues creating sets, see [Troubleshooting Dynamic Media](/help/assets/dynamic-media/troubleshoot-dm.md).

## アセットのアップロード {#uploading-assets}

まずは混在メディアセット用の画像およびビデオをアップロードします。ユーザーは混在メディアセットビューアで画像をズームできるので、画像を選択する際には必ずズームを考慮してください。最大サイズで 2,000 ピクセル以上の画像を使用してください。

また、混在メディアセットにスピンセットまたは画像セットを追加する場合は、それらのセットも作成します。

## 混在メディアセットの作成 {#creating-mixed-media-sets}

混在メディアセットには画像、画像セット、スピンセットおよびビデオを追加できます。ファイル、画像セットおよびスピンセットを公開できる状態にしてから、混在メディアセットに追加するようにしてください。

画像セットに追加したアセットは、自動的に英数字順で追加されます。追加後に、手動でアセットの順番を変更したり、並べ替えたりすることができます。

**混在メディアセットを作成するには**

1. In Assets, navigate to where you want to create a mixed media set, and click **[!UICONTROL Create]**, and select **[!UICONTROL Mixed Media Set]**. アセットを格納しているフォルダー内からセットを作成することもできます。混在メディアセットエディターが表示されます。

   ![chlimage_1-138](assets/chlimage_1-349.png)

1. 混在メディアセットエディターで、「**[!UICONTROL タイトル]**」に混在メディアセットの名前を入力します。この名前は、混在メディアセット全般のバナーに表示されます。オプションで、説明を入力します。

   ![chlimage_1-139](assets/chlimage_1-350.png)

   >[!NOTE]
   >
   >混在メディアセットを作成する際に、混在メディアセットのサムネールを変更したり、AEMが混在メディアセット内のアセットに基づいて自動的にサムネールを選択できるようにしたりできます。 To select a thumbnail, click **[!UICONTROL Change thumbnail]** and select any image (you can navigate to other folders to find images as well). If you have selected a thumbnail and then decide that you want AEM to generate one from the mixed media set, select **[!UICONTROL Switch to Automatic thumbnail]**.

1. 「アセットセレクタ」をタップして、混在メディアセットに含めるアセットを選択します。 アセットを選択し、「**[!UICONTROL 選択]**」をクリックします。

   With the Asset Selector, you can search for assets by typing in a keyword and tapping **[!UICONTROL Return]**. フィルターを適用して、検索結果を絞り込むこともできます。パス、コレクション、ファイルタイプおよびタグでフィルタリングできます。Select the filter and then tap the **[!UICONTROL Filter]** icon from the toolbar. Change the view by selecting the **[!UICONTROL View]** icon and selecting **[!UICONTROL List View]**, **[!UICONTROL Column View]**, or **[!UICONTROL Card View]**.

   [セレクターの操作](/help/assets/dynamic-media/working-with-selectors.md)を参照してください。

   ![chlimage_1-140](assets/chlimage_1-351.png)

1. Re-order the assets by dragging them up or down the list (must select the **[!UICONTROL Reorder]** icon), as necessary.

   ![chlimage_1-141](assets/chlimage_1-352.png)

   If you want to add thumbnails, click the **+** **[!UICONTROL thumbnail]** icon next to the image and navigate to the thumbnail you want. When done selecting all the thumbnail images click **[!UICONTROL Save]**.

   >[!NOTE]
   >
   >If you want to add assets, tap **[!UICONTROL Add Asset]**.

1. To delete an asset, select the corresponding check box and tap **[!UICONTROL Delete Asset]**.
1. To apply a preset, tap **[!UICONTROL Preset]** in the upper right corner and select a preset to apply to the assets.
1. 「**[!UICONTROL 保存]**」をクリックします。新しく作成した混在メディアセットが、作成先のフォルダーに表示されます。

## 混在メディアセットの編集 {#editing-mixed-media-sets}

[アセットの編集と同じように](/help/assets/manage-digital-assets.md)、ユーザーインターフェイスで直接、混在メディアセット内のアセットに対して様々な編集タスクを実行できます。また、混在メディアセットでは次のアクションも実行できます。

* 混在メディアセットへのアセットの追加
* 混在メディアセット内のアセットの並べ替え
* 混在メディアセット内のアセットの削除
* ビューアプリセットの適用
* デフォルトサムネールの変更

**混在メディアセットを編集するには**

1. 次のいずれかの操作をおこないます。

   * 混在メディアセットアセットの上にマウスポインターを置き、**[!UICONTROL 編集]**（鉛筆アイコン）をタップします。
   * 混在メディアセットアセットの上にマウスポインターを置き、**[!UICONTROL 選択]**（チェックマークアイコン）をタップしてからツールバーの「**[!UICONTROL 編集]**」をタップします。

   * 混在メディアセットアセットをタップし、ツールバーの「**[!UICONTROL 編集]**」（鉛筆アイコン）をタップします。

1. 混在メディアセットエディターで、次のいずれかをおこないます。

   * アセットを並べ替えるには - 左側のパネルで「**[!UICONTROL アセット]**」（写真アイコン）をタップし、アセットを新しい位置にドラッグします。
   * アセットを追加するには - ツールバーの「**[!UICONTROL アセットを追加]**」をタップします。アセットに移動します。追加するアセットごとに、（アセットの名前ではなく）アセットの画像の上にマウスポインターを置き、チェックマークアイコンをタップします。右上隅にある「**[!UICONTROL 選択]**」をタップします。

   * アセットを削除するには - 左側のパネルで「**[!UICONTROL アセット]**」（写真アイコン）をタップし、アセットを選択します。ツールバーの「**[!UICONTROL アセットを削除]**」をタップします。

   * アセットを名前の昇順または降順に並べ替えるには、左側のパネルで「**[!UICONTROL アセット]**」（写真アイコン）をタップします。「**[!UICONTROL アセット]**」見出しの右側にある上向きまたは下向きキャレットアイコンをタップします。

      >[!NOTE]
      >
      >    * To delete an entire Mixed Media Set, from any viewing mode (such as **[!UICONTROL Card View]** or **[!UICONTROL Column View]**) navigate to the Mixed Media Set. アセットの上にマウスポインターを置き、チェックマークアイコンをタップして選択します。キーボードの **[!UICONTROL Backspace]** キーを押すか、ツールバーの「**[!UICONTROL 詳細]**」（3 つのドット）をクリックしてから「**[!UICONTROL 削除]**」をタップします。
         >
         >    
      * You can edit the assets in a Mixed Media Set by navigating to the set, clicking **Set Members]** in the left rail, and then tapping the **[!UICONTROL Pencil]** icon on an individual asset to open the editing window.


1. 編集が完了したら、「**[!UICONTROL 保存]**」をタップします。

   >[!NOTE]
   >
   >* 混在メディアセット内のアセットを編集するには - 混在メディアセットに移動します。セットを（選択ではなく）タップして、AEM プレビューを設定ページでセットを開きます。左側のレールで、下向きキャレットをクリックしてドロップダウンリストを開き、「**[!UICONTROL メンバーを設定]**」をタップします。メンバーを設定ページで、アセットの上にマウスポインターを置き、「**[!UICONTROL 編集]**」（鉛筆アイコン）をタップして編集ページを開きます。
      >
      >
   * 混在メディアセット全体を削除するには - 任意の表示モード（カード表示や列表示など）から混在メディアセットに移動します。Hover on the set, then tap **Select]** (checkmark icon). キーボードの **[!UICONTROL Backspace]** キーを押すか、「**[!UICONTROL 詳細]**」（連続する 3 つのドット）をタップしてから「**[!UICONTROL 削除]**」をタップします。


## 混在メディアセットのプレビュー {#previewing-mixed-media-sets}

混在メディアセットのプレビュー方法について詳しくは、[アセットのプレビュー](/help/assets/dynamic-media/previewing-assets.md)を参照してください。

## 混在メディアセットの公開 {#publishing-mixed-media-sets}

混在メディアセットの公開方法について詳しくは、[アセットの公開](/help/assets/dynamic-media/publishing-dynamicmedia-assets.md)を参照してください。

>[!NOTE]
>
>混在メディアセットが最初の公開時に配信サービスに完全に送信されなかった場合は、混在メディアセットを 2 回公開する必要があります。

