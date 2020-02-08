---
title: 画像セット
description: ダイナミックメディアで画像セットを操作する方法について説明します。
translation-type: tm+mt
source-git-commit: 6224d193adfb87bd9b080f48937e0af1f03386d6

---


# 画像セット {#image-sets}

画像セットは、ユーザーに対して統一された閲覧エクスペリエンスを提供します。ユーザーはこのエクスペリエンスで、サムネール画像をクリックしてアイテムの様々なビューを表示できます。画像セットによって、アイテムの代替的なビューを表示でき、ビューアでは画像をより近くで確認するためのズームツールを利用できます。

画像セットのバナーには、「`IMAGESET`」と表示されます。In addition, if the Image Set is published, then the publish date, indicated by the **[!UICONTROL World]** icon is on the banner along with the last modification date, indicated by the **[!UICONTROL Pencil]** icon displays.

![chlimage_1-133](assets/chlimage_1-339.png)

画像セット内でスウォッチを作成するには、画像セットを作成し、サムネールを追加します。

この使い方は、アイテムを異なる色、パターンまたは仕上がりで表示する場合に特に便利です。カラースウォッチを含む画像セットを作成するには、ユーザーに表示する色、パターンまたは仕上がりごとに画像を 1 つずつ用意する必要があります。また、色、パターンまたは仕上がりごとに 1 つのカラースウォッチ、パターンスウォッチまたは仕上がりスウォッチを用意する必要もあります。

例として、つばの色が異なる帽子の画像を表示します。つばの色は、赤、緑、青です。この場合、同じ帽子について 3 つの写真が必要になります。赤のつばの写真、緑のつばの写真、青のつばの写真が必要です。また、赤のカラースウォッチ、緑のカラースウォッチ、青のカラースウォッチも必要になります。カラースウォッチは、ユーザーがスウォッチセットビューアでクリックして、赤のつばの帽子、緑のつばの帽子または青のつばの帽子を表示するためのサムネールとして機能します。

>[!NOTE]
>
>アセットユーザーインターフェイスについて詳しくは、[タッチ UI を使用したアセットの管理](/help/assets/manage-digital-assets.md)を参照してください。

## クイックスタート：画像セット {#quick-start-image-sets}

すぐに使い始めるには：

1. [複数ビュー用のマスター画像をアップロードします。](#uploading-assets-in-image-sets)

   まずは画像セット用の画像をアップロードします。ユーザーは画像セットビューアで画像をズームできるので、画像を選択する際にはズームを考慮します。最大サイズで 2,000 ピクセル以上の画像を使用してください。AEM Assets では多くの画像ファイル形式がサポートされますが、可逆圧縮 TIFF、PNG および EPS 画像の使用が推奨されます。

1. [画像セットを作成します。](#creating-image-sets)

   画像セットで、画像セットビューア内のサムネール画像をクリックします。

   Assets で画像セットを作成するには、**[!UICONTROL 作成／画像セット]**&#x200B;をタップまたはクリックします。次に、画像を追加して「**[!UICONTROL 保存]**」をクリックします。

   [バッチセットプリセット](/help/assets/dynamic-media/config-dm.md#creating-batch-set-presets-to-auto-generate-image-sets-and-spin-sets)を使用して画像セットを自動的に作成することもできます。

   >[!IMPORTANT]
   >
   >バッチセットは、アセットの取り込みの一部としてIPS(Image Production System)によって作成されます。

   See [Preparing Image Set assets for upload and Uploading your files](#uploading-assets-in-image-sets).

   [セレクターの操作](/help/assets/dynamic-media/working-with-selectors.md)を参照してください。

1. Add [Image Set Viewer presets](/help/assets/dynamic-media/managing-viewer-presets.md), as needed.

   管理者は、画像セットビューアプリセットを作成または編集できます。To see your image set with a viewer preset, select the image set, and in the left-rail drop-down menu, select **[!UICONTROL Viewers]**.

   See **[!UICONTROL Tools > Assets > Viewer Presets]** to create or edit viewer presets.

1. (Optional) [Viewing Image Sets](/help/assets/dynamic-media/image-sets.md#viewing-image-sets) that were created using batch set presets.
1. [画像セットをプレビューします。](/help/assets/dynamic-media/previewing-assets.md)

   画像セットを選択すると、プレビューできます。サムネールアイコンをクリックして、選択したビューアでの画像セットの表示を確認します。You can choose different viewers from the **[!UICONTROL Viewers]** menu, available from the left rail drop-down menu.

1. [画像セットを公開します。](/help/assets/dynamic-media/publishing-dynamicmedia-assets.md)

   画像セットを公開すると、URL と埋め込み文字列がアクティベートされます。In addition, you must [publish any custom viewer preset](/help/assets/dynamic-media/managing-viewer-presets.md) that you have created. 既製のビューアプリセットが既に公開されています。

1. [URL を Web アプリケーションにリンクする](/help/assets/dynamic-media/linking-urls-to-yourwebapplication.md)か、[ビデオビューアまたは画像ビューアを埋め込みます](/help/assets/dynamic-media/embed-code.md)。

   画像セットの URL コールが作成され、画像セットの公開後にそれらの URL コールがアクティベートされます。アセットをプレビューする際に、これらの URL をコピーできます。または、URL を Web サイトに埋め込むこともできます。

   画像セットを選択し、左側のレールのドロップダウンメニューで「**[!UICONTROL ビューア]**」を選択します。

   See [Linking an Image Set to a web page](/help/assets/dynamic-media/linking-urls-to-yourwebapplication.md) and [Embedding the Video or Image Viewer](/help/assets/dynamic-media/embed-code.md).

To edit Image Sets, see [editing Image Sets.](#editing-image-sets) また、画像セットのプロパティを表示および編 [集することもできます](/help/assets/manage-digital-assets.md#editing-properties)。

If you have issues creating sets, see Images and Sets in [Troubleshooting Dynamic Media](/help/assets/dynamic-media/troubleshoot-dm.md#images-and-sets).

## 画像セット内のアセットのアップロード {#uploading-assets-in-image-sets}

まずは画像セット用の画像をアップロードします。ユーザーは画像セットビューアで画像をズームできるので、画像を選択する際にはズームを考慮します。最大サイズで 2,000 ピクセル以上の画像を使用してください。画像セットでは多くの画像ファイル形式がサポートされますが、可逆圧縮 TIFF、PNG および EPS 画像の使用が推奨されます。

画像セット用の画像のアップロードは、[AEM アセットでの他のアセットのアップロード](/help/assets/manage-digital-assets.md#uploading-assets)と同様に実行できます。

### アップロード用の画像セットアセットの準備 {#preparing-image-set-assets-for-upload}

画像セットを作成する前に、画像が適切なサイズと形式であることを確認します。

複数ビューの画像セットを作成するには、異なる視点からアイテムを表示するための画像、または同じアイテムの異なる面を表示するための画像が必要になります。目標は、閲覧者がアイテムの見た目や機能について全体的に把握できるように、アイテムの重要な特徴を際立たせることです。

ユーザーは画像セット内で画像をズームできるので、最大サイズで 2,000 ピクセル以上の画像を使用してください。AEM アセットでは多くの画像ファイル形式がサポートされますが、可逆圧縮 TIFF、PNG および EPS 画像の使用が推奨されます。

>[!NOTE]
>
>さらに、製品スウォッチを示すサムネールを使用する場合は、次のことをおこなう必要があります。
>
>同じ画像を異なる色、パターンまたは仕上がりで表示するためのビネットまたは異なる写真が必要になります。また、それぞれの色、パターンまたは仕上がりに対応するサムネールファイルも必要です。例えば、同じジャケットをブラック、ブラウン、グリーンで表示する画像セットのサムネールを表示するには、次の項目が必要です。
>
>* 同じジャケットのブラック、ブラウンおよびグリーンの写真。
>* ブラック、ブラウンおよびグリーンの色のサムネール。


## 画像セットの作成 {#creating-image-sets}

画像セットは、ユーザーインターフェイスまたは API 経由で作成できます。ここでは、UI で画像セットを作成する方法について説明します。

>[!NOTE]
>
>[バッチセットプリセット](/help/assets/dynamic-media/config-dm.md#creating-batch-set-presets-to-auto-generate-image-sets-and-spin-sets)を使用して画像セットを自動的に作成することもできます。
>****重要：バッチセットは、アセットの取り込みの一部としてIPS(Image Production System)によって作成されます。

画像セットに追加したアセットは、自動的に英数字順で追加されます。追加後に、手動でアセットの順番を変更したり、並べ替えたりすることができます。

>[!NOTE]
>
>ファイル名に「,」（コンマ）が含まれているアセットについては、画像セットはサポートされません。

**画像セットを作成するには**

1. AEM で、AEM のロゴをタップしてグローバルナビゲーションコンソールにアクセスし、**[!UICONTROL ナビゲーション／アセット]**&#x200B;をタップします。画像セットを作成する場所に移動し、**[!UICONTROL 作成／画像セット]**&#x200B;をタップ して、画像セットエディターページを開きます。

   アセットを格納しているフォルダー内からセットを作成することもできます。

   ![6_5_imagesets-createpulldown](assets/6_5_imagesets-createpulldown.png)

1. 画像セットエディターページの「**[!UICONTROL タイトル]**」フィールドに画像セットの名前を入力します。この名前は、画像セット全般のバナーに表示されます。オプションで、説明を入力します。

   ![6_5_imageset-creatingnewset](assets/6_5_imageset-creatingnewset.png)

1. 次のいずれかの操作をおこないます。

   * 画像セットエディターページの左上隅付近にある「**[!UICONTROL アセットを追加]**」をタップします。

   * 画像セットエディターページの中央付近にある「**[!UICONTROL タップしてアセットセレクターを開く]**」をタップします。
   画像セットに含めるアセットをタップして選択しします。選択済みのアセットにはチェックマークアイコンが付いています。作業が完了したら、ページの右上隅付近にある「**[!UICONTROL 選択]**」をタップします。

   アセットセレクターでは、キーワードを入力して **[!UICONTROL Enter]** キーをタップまたはクリックすることで、アセットを検索することができます。フィルターを適用して、検索結果を絞り込むこともできます。パス、コレクション、ファイルタイプおよびタグでフィルタリングできます。Select the filter and then tap the **[!UICONTROL Filter]** icon on the toolbar. 表示アイコンをタップし、**[!UICONTROL 列表示]**、**[!UICONTROL カード表示]**、**[!UICONTROL リスト表示]**&#x200B;のいずれかを選択してビューを変更します。

   [セレクターの操作](/help/assets/dynamic-media/working-with-selectors.md)を参照してください。

   ![6_5_imageset-addingassets](assets/6_5_imageset-addingassets.png)

1. 画像セットに追加したアセットは、自動的に英数字順で追加されます。追加後に、手動でアセットの順番を変更したり、並べ替えたりすることができます。

   必要に応じて、アセットの並べ替えアイコンをアセットのファイル名の右にドラッグして、画像をセットリスト内で上下に並べ替えます。

   ![6_5_imageset-reorderassets](assets/6_5_imageset-reorderassets.png)

   If you want to change a thumbnail or swatch, click the **+** **thumbnail** icon next to the image and navigate to the thumbnail or swatch you want. When done selecting all the images click **[!UICONTROL Save]**.

1. （オプション）次のいずれかの操作をおこないます。

   * 画像を削除するには、画像を選択し、「**[!UICONTROL アセットを削除]**」をタップします。

   * ページの右上隅付近にプリセットを適用するには、「]**プリセット**[!UICONTROL 」をタップした後、すべてのアセットに一度に適用するプリセットを選択します。
   >[!NOTE]
   >
   >画像セットを作成するときに、画像セットのサムネールを変更したり、画像セット内のアセットに基づいて AEM がサムネールを自動的に選択するように設定したりできます。サムネールを選択するには、画像セットエディターページの「タイトル」フィールドの上にある「]**サムネールを変更**[!UICONTROL 」をタップし、任意の画像を選択します（他のフォルダーに移動して画像を検索することもできます）。If you have selected a thumbnail and then decide that you want AEM to generate one from the image set, select **[!UICONTROL Switch to]** **[!UICONTROL Automatic thumbnail]**.

1. 「**[!UICONTROL 保存]**」をクリックします。新しく作成した画像セットが、作成先のフォルダーに表示されます。

## 画像セットの表示 {#viewing-image-sets}

画像セットは、ユーザーインターフェイスで作成することも、[バッチセットプリセット](/help/assets/dynamic-media/config-dm.md#creating-batch-set-presets-to-auto-generate-image-sets-and-spin-sets)を使用して自動的に作成することもできます。

>[!IMPORTANT]
>
>バッチセットは、IPS [Image Production systemによってアセット取り込みの一] 部として作成されます。

However, sets created using batch set presets, do *not* appear in the user interface. これらのセットは、3つの方法で表示できます。 （これらの方法は、画像セットをユーザーインターフェイスで作成した場合も使用できます）。

* 個々のアセットのプロパティを開きます。選択したアセットが参照されている、またはメンバーとして含まれているセットがプロパティで示されます。セットの名前をクリックして、セット全体を表示します。

   ![6_5_imageset-assetproperties](assets/6_5_imageset-assetproperties.png)

* 任意のセットのメンバー画像で、Select the **[!UICONTROL Sets** menu to display the sets that the asset is a member of.

   ![6_5_imageset-setspulldownmenu](assets/6_5_imageset-setspulldownmenu.png)

* From search, you can select **[!UICONTROL Filter**, then expand **[!UICONTROL Dynamic Media** and select **[!UICONTROL Sets]**.

   検索結果として、ユーザーインターフェイスで手動で作成した一致するセットか、バッチセットプリセットを使用して自動的に作成した一致するセットが返されます。自動セットの場合、検索クエリは、AEM での検索とは異なる「次の値で始まる」検索条件を使用して実行されます。AEM での検索は、「次を含む」検索条件に基づいて実行されます。自動セットを検索する唯一 **[!UICONTROL の方法は]** 、フィルターを「セット」に設定する方法です。

   ![chlimage_1-134](assets/chlimage_1-134.png)

>[!NOTE]
>
>[画像セットの編集](#editing-image-sets)の説明に従って、ユーザーインターフェイスを通じて画像セットを表示できます。

## 画像セットの編集 {#editing-image-sets}

画像セットには、次のような様々な編集タスクを実行できます。

* 画像セットへの画像の追加
* 画像セット内の画像の並べ替え
* 画像セットのアセットの削除
* ビューアプリセットの適用
* 画像セットの削除

**画像セットを編集するには**

1. 次のいずれかの操作をおこないます。

   * 画像セットアセット上にマウスポインターを置き、]**編集**[!UICONTROL （鉛筆アイコン）をタップします。
   * 画像セットアセット上にマウスポインターを置き、**[!UICONTROL 選択]**（チェックマークアイコン）をタップした後、ツールバーの「**[!UICONTROL 編集]**」をタップします。
   * 画像セットアセットをタップしてから、ツールバーの&#x200B;]**編集**[!UICONTROL （鉛筆アイコン）をタップします。

1. 画像セット内の画像を編集するには、次のいずれかの操作をおこないます。

   * アセットを並べ替えるには、画像を新しい位置までドラッグします（並べ替えアイコンを選択して項目を移動します）。
   * 項目を昇順または降順に並べ替えるには、列の見出しをクリックします。
   * アセットを追加するか既存のアセットを更新するには、「**[!UICONTROL アセットを追加]**」をクリックします。アセットに移動して選択し、ページの右上隅にある「]**選択**[!UICONTROL 」をタップしますページ。
      >[!NOTE]
      >
      >AEMがサムネールに使用する画像を削除し、別の画像に置き換えても、元のアセットは表示されたままになります。
   * アセットを削除するには、アセットを選択して、「**[!UICONTROL アセットを削除]**」をタップまたはクリックします。
   * プリセットを適用するには、ページの右上隅付近にある「**[!UICONTROL プリセット]**」をタップ し、ビューアプリセットを選択します。
   * サムネールを追加または変更するには、該当するアセットの右横にあるサムネールアイコンを選択します。新しいサムネールまたはスウォッチアセットに移動して選択し、「**[!UICONTROL 選択]**」をタップします。
   * 画像セット全体を削除するには、画像セットの場所に移動して画像セットを選択し、「**[!UICONTROL 削除]**」をタップします。
   >[!NOTE]
   >
   >You can edit the images in an Image Set by navigating to the set, tap **[!UICONTROL Set Members]** in the left rail, and then tap the Pencil icon on an individual asset to open the editing window.

1. 編集が完了したら、「**[!UICONTROL 保存]**」をタップします。

## 画像セットのプレビュー {#previewing-image-sets}

詳しくは、[アセットのプレビュー](/help/assets/dynamic-media/previewing-assets.md)を参照してください。

## 画像セットの公開 {#publishing-image-sets}

[アセットの公開](/help/assets/dynamic-media/publishing-dynamicmedia-assets.md)を参照してください。
