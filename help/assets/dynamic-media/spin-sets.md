---
title: スピンセット
description: ダイナミックメディアでスピンセットを操作する方法を説明します。
translation-type: tm+mt
source-git-commit: 6224d193adfb87bd9b080f48937e0af1f03386d6

---


# スピンセット{#spin-sets}

スピンセットは、物体を回転させて調べるという現実世界の操作をシミュレートしたものです。スピンセットによって、あらゆる角度からアイテムを表示して、あらゆる角度から重要な細部を目で確認できます。

スピンセットは、360 度の閲覧エクスペリエンスをシミュレートします。Dynamic Media は、ビューアがアイテムを回転できる単一軸のスピンセットを提供します。さらに、ユーザーは「自由形式」のズームを実行し、マウスを数回クリックするだけで任意のビューをパンできます。このようにして、ユーザーは特定の視点からより詳しくアイテムを調べることができます。

Spin Sets are designated by a banner with the word **[!UICONTROL SPINSET]**. In addition, if the Spin Set is published, then the publish date, indicated by the **[!UICONTROL World]** icon is on the banner along with the last modification date, indicated by the **[!UICONTROL Pencil]** icon displays.

![chlimage_1-](assets/chlimage_1-380.png)

>[!NOTE]
>
>アセットユーザーインターフェイスについて詳しくは、[タッチ UI を使用したアセットの管理](/help/assets/manage-digital-assets.md)を参照してください。

## クイックスタート：スピンセット {#quick-start-spin-sets}

スピンセットをすぐに使い始めるには、次の手順を実行します。

1. [複数ビュー用の画像をアップロードします。](#uploading-assets-for-spin-sets)

   1次元スピンセットには少なくとも8 ～ 12枚の写真が必要で、2次元スピンセットには16 ～ 24枚の写真が必要です。アイテムが回転して反転しているように見せるには、一定の間隔でアイテムを撮影する必要があります。例えば、1次元スピンセットに12枚の写真が含まれる場合、アイテムを30°(360°/12)単位で回転させます。

1. [スピンセットを作成します。](#creating-spin-sets)

   To create a Spin Set, select **[!UICONTROL Create > Spin Set]** and then name the set, choose the assets, and choose the order the images appear.

   [セレクターの操作](/help/assets/dynamic-media/working-with-selectors.md)を参照してください。

   >[!NOTE]
   >
   >[バッチセットプリセット](/help/assets/dynamic-media/config-dm.md#creating-batch-set-presets-to-auto-generate-image-sets-and-spin-sets)を使用してスピンセットを自動的に作成することもできます。**** 重要：バッチセットは、アセットの取り込みの一部としてIPS(Image Production System)によって作成されます。

1. 必要に応じて[スピンセットビューアプリセット](/help/assets/dynamic-media/managing-viewer-presets.md)を設定します。

   管理者は、スピンセットビューアプリセットを作成または編集できます。To see your spin set with a viewer preset, select the spin set, and in the left-rail drop-down menu, select **Viewers**.

   See **[!UICONTROL Tools > Assets > Viewer Presets]** to create or edit viewer presets.

   See [Adding and editing viewer presets.](/help/assets/dynamic-media/managing-viewer-presets.md)

   バッチセットプリセットを使用して作成したセットを表示したり、それらのセットにアクセスしたりするには、3 つの方法があります(Sets created using batch set presets, do *not* appear in the user interface.)

1. [スピンセットをプレビューします。](/help/assets/dynamic-media/previewing-assets.md)

   スピンセットを選択すると、プレビューできます。スピンセットを回転します。You can choose different viewers from the **[!UICONTROL Viewers]** menu, available from the left rail drop-down menu.

1. [スピンセットを公開します。](/help/assets/dynamic-media/publishing-dynamicmedia-assets.md)

   スピンセットを公開すると、URL と埋め込み文字列がアクティベートされます。In addition, you must [publish the viewer preset](/help/assets/dynamic-media/managing-viewer-presets.md).

1. [URL を Web アプリケーションにリンクする](/help/assets/dynamic-media/linking-urls-to-yourwebapplication.md)か、[ビデオビューアまたは画像ビューアを埋め込みます](/help/assets/dynamic-media/embed-code.md)。

   スピンセットの URL コールが作成され、スピンセットの公開後にそれらの URL コールがアクティベートされます。アセットをプレビューする際に、これらの URL をコピーできます。または、URL を Web サイトに埋め込むこともできます。

   Select the Spin Set, then in the left rail drop-down menu, select **[!UICONTROL Viewers]**.

   See [Linking a Spin Set to a web page](/help/assets/dynamic-media/linking-urls-to-yourwebapplication.md) and [Embedding the Video or Image Viewer](/help/assets/dynamic-media/embed-code.md).

If you need to, you can [edit Spin Sets](#editing-spin-sets). In addition, you can view and modify [Spin Set properties](/help/assets/manage-digital-assets.md#editing-properties).

## スピンセット用のアセットのアップロード {#uploading-assets-for-spin-sets}

1次元スピンセットには少なくとも8 ～ 12枚の写真が必要で、2次元スピンセットには16 ～ 24枚の写真が必要です。アイテムが回転して反転しているように見せるには、一定の間隔でアイテムを撮影する必要があります。例えば、1次元スピンセットに12枚の写真が含まれる場合、アイテムを30°(360°/12)単位で回転させます。

スピンセット用の画像のアップロードは、[AEM Assets での他のアセットのアップロード](/help/assets/manage-digital-assets.md)と同様に実行できます。

### スピンセット用の画像のキャプチャに関するガイドライン {#guidelines-for-shooting-spin-set-images}

ここでは、スピンセット画像に関するベストプラクティスを説明します。一般に、スピンセット内の画像が多いほど、画像のスピン効果が向上します。ただし、セット内に多くの画像を追加すると、画像の読み込みにかかる時間も長くなります。AEM では、スピンセットで使用する画像の撮影について、次のガイドラインに従うことを推奨します。

* 1次元スピンセットでは少なくとも8 ～ 12枚の画像を使用し、2次元スピンセットでは16 ～ 24枚の画像を使用します。360度回転するには、最低8枚の画像が必要です。2次元スピンセットの作成には労力が必要なので、1次元スピンセットの方が一般的です。
* 可逆圧縮形式を使用します。TIFF および PNG が推奨されます。
* 真っ白または他の高コントラストの背景上にアイテムが表示されるように、すべての画像をマスクします。オプションで、シャドウを追加します。
* 製品の細部に十分に光を当て、ピントを合わせるようにします。
* ファッション衣料の場合は、マネキンやモデルに着せてスピン画像を撮影します。多くの場合、ガラス製のマネキンを使用してマネキンを完全にマスクするか、画像内に定型化されたマネキンを表示します。角度を定義することで、モデルによるスピンセットを作成できます。床にテープを貼って角度をマークし、モデルが撮影ごとに動いて向きを変えるための手助けをします。

## スピンセットの作成 {#creating-spin-sets}

ここでは、スピンセットを作成する方法について説明します。

>[!NOTE]
>
>[バッチセットプリセット](/help/assets/dynamic-media/config-dm.md)を使用してスピンセットを自動的に作成することもできます。**** 重要：バッチセットは、アセットの取り込みの一部としてIPS(Image Production System)によって作成されます。
>
>See &quot;Creating batch set presets to auto-generate Image Sets and Spin Sets&quot; in [Configuring Dynamic Media](/help/assets/dynamic-media/config-dm.md).

>[!NOTE]
>
>スピンセット内での画像の表示順は重要です。スピンがスムーズに 360 度のビューを描けるように画像を並べてください。

**スピンセットを作成するには**

1. In Assets, navigate to where you want to create a spin set, click **[!UICONTROL Create]**, and select **[!UICONTROL Spin Set]**. アセットを格納しているフォルダー内からセットを作成することもできます。スピンセットエディターが表示されます。

   ![6_5_spinset-createpulldownmenu](assets/6_5_spinset-createpulldownmenu.png)

1. スピンセットエディターの「**[!UICONTROL タイトル]**」フィールドにスピンセットの名前を入力します。この名前は、スピンセット全般のバナーに表示されます。オプションで、説明を入力します。

   ![6_5_spinset-spinseteditortitle](assets/6_5_spinset-spinseteditortitle.png)

   >[!NOTE]
   >
   >スピンセットを作成するときに、スピンセットのサムネールを変更したり、AEM でスピンセット内のアセットに基づいてサムネールを自動的に選択したりすることができます。To select a thumbnail, click **[!UICONTROL Change thumbnail]** and select any image (you can navigate to other folders to find images as well). If you have selected a thumbnail and then decide that you want AEM to generate one from the spin set, select **[!UICONTROL Switch to Automatic thumbnail]**.

1. 次のいずれかの操作をおこないます。

   * スピンセットエディターページの左上隅にある「**[!UICONTROL アセットを追加]**」をタップします。

   * スピンセットエディターページの中央付近にある「**[!UICONTROL タップしてアセットセレクターを開く]**」をタップします。
   スピンセットに含めるアセットをタップして選択しします。選択済みのアセットにはチェックマークアイコンが付いています。作業が完了したら、ページの右上隅付近にある「**[!UICONTROL 選択]**」をタップします。

   With the Asset Selector, you can search for assets by typing in a keyword and tapping **[!UICONTROL Return**. フィルターを適用して、検索結果を絞り込むこともできます。パス、コレクション、ファイルタイプおよびタグでフィルタリングできます。Select the filter and then tap the **[!UICONTROL Filter]** icon on the toolbar. 表示アイコンをタップし、**[!UICONTROL 列表示]**、**[!UICONTROL カード表示]**、**[!UICONTROL リスト表示]**&#x200B;のいずれかを選択してビューを変更します。

   [セレクターの操作](/help/assets/dynamic-media/working-with-selectors.md)を参照してください。

   ![chlimage_1-383](assets/chlimage_1-383.png)

1. 画像セットに追加したアセットは、自動的に英数字順で追加されます。追加後に、手動でアセットの順番を変更したり、並べ替えたりすることができます。

   必要に応じて、アセットの並べ替えアイコンをアセットのファイル名の右にドラッグして、画像をセットリスト内で上下に並べ替えます。

   ![スピンセットのフレーム 11 を新しい位置にドラッグして並べ替える](assets/6_5_spinset-reorderassets.png)

   スピンセットのフレーム 11 を新しい位置にドラッグして並べ替える

1. （オプション）次のいずれかの操作をおこないます。

   * 画像を削除するには、画像を選択し、「**[!UICONTROL アセットを削除]**」をタップします。

   * ページの右上隅付近にプリセットを適用するには、「]**プリセット**[!UICONTROL 」をタップした後、すべてのアセットに一度に適用するプリセットを選択します。

1. 「**[!UICONTROL 保存]**」をクリックします。新しく作成したスピンセットが、作成先のフォルダーに表示されます。

## スピンセットの表示 {#viewing-spin-sets}

スピンセットは、ユーザーインターフェイスで作成することも、[バッチセットプリセット](/help/assets/dynamic-media/config-dm.md)を使用して自動的に作成することもできます。However, sets created using batch set presets, do *not* appear in the user interface. バッチセットプリセットを使用して作成されたセットには、3つの方法でアクセスできます。 （これらの方法は、スピンセットをユーザーインターフェイスで作成した場合も使用できます）。

>[!NOTE]
>
>You can also view sets by way of the user interface as described in [Editing Spin Sets](#editing-spin-sets).

**スピンセットを表示するには**

1. 個々のアセットのプロパティを開きます。（「**[!UICONTROL セットのメンバー]**」の下に）選択したアセットがメンバーとして含まれるセットが表示されます。セットの名前をクリックして、セット全体を表示します。

   ![chlimage_1-156](assets/chlimage_1-384.png)

1. 任意のセットのメンバー画像で、Select the **[!UICONTROL Sets]** menu to display the sets that the asset is a member of.

   ![chlimage_1-157](assets/chlimage_1-385.png)

1. 検索で、「**[!UICONTROL フィルター]**」を選択し、「**[!UICONTROL Dynamic Media]**」を展開して「**[!UICONTROL セット]**」を選択します。

   検索結果として、ユーザーインターフェイスで手動で作成した一致するセットか、バッチセットプリセットを使用して自動的に作成した一致するセットが返されます。For automated sets, the search query is conducted using `Starts with` search criteria which is different from AEM search which is based on using `Contains` search criteria. Setting the filter to **[!UICONTROL Sets]** is the only way to search automated sets.

   ![chlimage_1-158](assets/chlimage_1-386.png)

## スピンセットの編集 {#editing-spin-sets}

スピンセットには、次のような様々な編集タスクを実行できます。

* スピンセットへの画像の追加
* スピンセット内の画像の並べ替え
* スピンセットのアセットの削除
* ビューアプリセットの適用
* スピンセットの削除

**スピンセットを編集するには**

1. 次のいずれかの操作をおこないます。

   * スピンセットアセット上にマウスポインターを置き、]**編集**[!UICONTROL （鉛筆アイコン）をタップします。
   * スピンセットアセット上にマウスポインターを置き、**[!UICONTROL 選択]**（チェックマークアイコン）をタップした後、ツールバーの「**[!UICONTROL 編集]**」をタップします。

   * スピンセットアセットをタップしてから、ツールバーの&#x200B;]**編集**[!UICONTROL （鉛筆アイコン）をタップします。

1. スピンセットを編集するには、次のいずれかの操作をおこないます。

   * 画像を並べ替えるには、画像を新しい位置までドラッグします（並べ替えアイコンを選択して項目を移動します）。
   * 項目を昇順または降順に並べ替えるには、列の見出しをクリックします。
   * To add an asset or update an existing asset, click **[!UICONTROL Add Asset]**. アセットに移動して選択し、右上隅の「]**選択**[!UICONTROL 」をタップします。AEMがサムネールに使用する画像を削除し、別の画像に置き換えても、元のアセットは表示されたままになります。
   * To delete an asset, select it and click or tap **[!UICONTROL Delete Asset]**.
   * プリセットを適用するには、「プリセット」アイコンをタップまたはクリックし、プリセットを選択します。
   * スピンセット全体を削除するには、スピンセットに移動して選択し、「**[!UICONTROL 削除]**」を選択します
   >[!NOTE]
   >
   >スピンセットの画像を編集するには、スピンセットに移動し、左側のレールの「**[!UICONTROL メンバーを設定]**」をタップしてから、個々のアセットの鉛筆アイコンをタップして編集ウィンドウを開きます。

1. 編集が完了したら、「**[!UICONTROL 保存]**」をクリックします。

## スピンセットのプレビュー {#previewing-spin-sets}

詳しくは、[アセットのプレビュー](/help/assets/dynamic-media/previewing-assets.md)を参照してください。

## スピンセットの公開 {#publishing-spin-sets}

[アセットの公開](/help/assets/dynamic-media/publishing-dynamicmedia-assets.md)を参照してください。