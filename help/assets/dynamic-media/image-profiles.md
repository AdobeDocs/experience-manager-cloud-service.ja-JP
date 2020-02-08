---
title: ダイナミックメディア画像プロファイル
description: アンシャープマスクのほか、スマート切り抜きとスマートスウォッチのどちらか一方または両方の設定を含むイメージプロファイルを作成し、そのプロファイルを画像アセットのフォルダーに適用します。
translation-type: tm+mt
source-git-commit: 6224d193adfb87bd9b080f48937e0af1f03386d6

---


# ダイナミックメディア画像プロファイル {#image-profiles}

画像をアップロードする際に、画像プロファイルをフォルダーに適用すると、アップロード時に画像を自動的に切り抜くことができます。

## Crop options {#crop-options}

選択可能な 2 つの画像切り抜きオプションと、カラーおよび画像スウォッチの作成を自動化するためのオプションがあります。

<table>
 <tbody>
  <tr>
   <td><strong>Option</strong></td>
   <td><strong>用途</strong></td>
   <td><strong>説明</strong></td>
  </tr>
  <tr>
   <td>ピクセル切り抜き</td>
   <td>画像サイズにのみ基づいて画像を一括で切り抜きます。</td>
   <td><p>このオプションを使用するには、「切り抜きオプション」ドロップダウンリストで「<strong>ピクセル切り抜き</strong>」を選択します。</p> <p>画像の各辺から切り抜くには、画像の任意の辺または四辺からの切り抜きのサイズ（ピクセル数）を入力します。画像がどれだけ切り抜かれるかは、画像ファイル内の ppi（1 インチあたりのピクセル数）の設定によって変わります。</p> <p>イメージプロファイルのピクセル切り抜きは以下の方法で実行されます。<br /> </p>
    <ul>
     <li>値は「上」、「下」、「左」、「右」です。</li>
     <li>左上隅が 0,0 とみなされ、ここからピクセル切り抜きが計算されます。</li>
     <li>切り抜きの開始点：「左」が X、「上」が Y です。</li>
     <li>水平方向の計算：元の画像の水平方向のピクセルサイズから「左」と「右」を差し引きます。</li>
     <li>垂直方向の計算：垂直方向の高さ（ピクセル）から「上」と「下」を差し引きます。</li>
    </ul> <p>例えば、4000 x 3000 ピクセルの画像があるとします。値として「上」= 250、「下」= 500、「左」= 300、「右」= 700 を使用します。</p> <p>左上 (300,250) から、(4000-300-700, 3000-250-500) つまり (3000,2250) のフィルスペースを使って切り抜きます。</p> </td>
  </tr>
  <tr>
   <td>スマート切り抜き</td>
   <td>視焦点位置に基づいて画像を一括で切り抜きます。</td>
   <td><p>スマート切り抜きでは、Adobe Sensei の人工知能の能力を利用して、自動的に画像を一括ですばやく切り抜きます。画面サイズに関係なく、あらゆる画像の焦点位置を自動的に検出して切り抜き、目的の箇所を抜き出します。</p> <p>スマート切り抜きを使用するには、「切り抜きオプション」ドロップダウンリストで「<strong>スマート切り抜き</strong>」を選択し、「レスポンシブ画像の切り抜き」の右側で、この機能を有効（オン）にします。</p> <p>大、中および小のデフォルトのブレークポイントサイズでは、通常、モバイル、タブレットデバイス、デスクトップおよびバナーで使用されるほとんどの画像のすべてのサイズに対応できます。大、中および小のデフォルト値は、必要に応じて編集できます。</p> <p>ブレークポイントを追加するには、「<strong>切り抜きを追加</strong>」をクリックします。切り抜きを削除するには、ごみ箱アイコンをクリックします。</p> </td>
  </tr>
  <tr>
   <td>カラーおよび画像スウォッチ</td>
   <td>各画像の画像スウォッチを一括で生成します。</td>
   <td><p><strong>注意</strong>：Dynamic Media Classic ではスマートスウォッチはサポートされません。</p> <p>商品画像から色やテクスチャを示す高品質のスウォッチを自動的に検出して生成します。</p> <p>カラーおよび画像スウォッチを使用するには、「切り抜きオプション」ドロップダウンリストで「<strong>スマート切り抜き</strong>」を選択し、「カラーおよび画像スウォッチ」の右側で、この機能を有効（オン）にします。「幅」と「高さ」テキストフィールドにピクセル値を入力します。</p> <p>画像の切り抜きはすべてレンディションレールから使用できますが、スウォッチを使用するには URL をコピー機能を利用しなければなりません。サイトでスウォッチをレンダリングするには、独自の表示コンポーネントを使用する必要があります（カルーセルバナーは例外です。カルーセルバナーで使用されるスウォッチについては、Dynamic Media が表示コンポーネントを提供します）。</p> <p><strong>画像スウォッチの使用</strong></p> <p>画像スウォッチの URL は簡単です。次のとおりです。</p> <p><code>/is/image/company/&lt;asset_name&gt;:Swatch</code></p> <p>where <code>:Swatch</code> is appended to the asset request.</p> <p><strong>カラースウォッチの使用</strong></p> <p>カラースウォッチを使用するには、次のように <code>req=userdata</code> 要求を作成します。</p> <p><code>/is/image/&lt;company_name&gt;/&lt;swatch_asset_name&gt;:Swatch?req=userdata</code></p> <p>例えば、Dynamic Media Classic（Scene7）のスウォッチアセットは次のとおりです。</p> <p><code>https://my.company.com:8080/is/image/DemoCo/Sleek:Swatch</code></p> <p>and here is the swatch asset's corresponding <code>req=userdata</code> URL:</p> <p><code>https://my.company.com:8080/is/image/DemoCo/Sleek:Swatch?req=userdata</code></p> <p>The <code>req=userdata</code> response is as follows:</p> <p><code class="code">SmartCropDef=Swatch
       SmartCropHeight=200.0
       SmartCropRect=0.421671,0.389815,0.0848564,0.0592593,200,200
       SmartCropType=Swatch
       SmartCropWidth=200.0
       SmartSwatchColor=0xA56DB2</code></p> <p>次の URL の例のように、XML 形式または JSON 形式の <code>req=userdata</code> 応答を要求することもできます。</p> <p><code>https://my.company.com:8080/is/image/DemoCo/Sleek:Swatch?req=userdata,xml</code></p><p><code>SmartSwatchColor</code></p><p></p></td></tr></tbody></table>

## アンシャープマスク {#unsharp-mask}

You use **[!UICONTROL Unsharp mask]** to fine-tune a sharpening filter effect on the final downsampled image. You can control intensity of effect, radius of the effect (measured in pixels), and a threshold of contrast that will be ignored. This effect uses the same options as Adobe Photoshop’s “Unsharp Mask” filter.

>[!NOTE]
>
>アンシャープマスクは、PTIFF（Pyramid TIFF）内のダウンスケールされたレンディション（50 ％以上ダウンサンプルされたもの）にのみ適用されます。つまり、ptiff 内の最大サイズのレンディションはアンシャープマスクの影響を受けませんが、サムネールのような小さいサイズのレンディションは変更されます（そしてアンシャープマスクを表示します）。

「**[!UICONTROL アンシャープマスク]**」には次のフィルタリングオプションがあります。

<table>
 <tbody>
  <tr>
   <td><strong>Option</strong></td>
   <td><strong>説明</strong></td>
  </tr>
  <tr>
   <td>量</td>
   <td>端のピクセルに適用するコントラストを制御します。デフォルトは 1.75 です。高解像度の画像ではこの値を 5 まで増やすことができます。「量」は、フィルター強度の尺度だと考えてください。範囲は 0～5 です。</td>
  </tr>
  <tr>
   <td>半径</td>
   <td>シャープに作用する端のピクセル周辺のピクセル数を決定します。高解像度の画像の場合は、1～2 を入力します。小さい値は端のピクセルのみをシャープにし、大きい値は広範囲のピクセルをシャープにします。適切な値は画像のサイズによって異なります。デフォルト値は 0.2 です。範囲は 0～250 です。</td>
  </tr>
  <tr>
   <td>しきい値</td>
   <td><p>アンシャープマスクフィルターが適用される場合のコントラストの範囲を指定します。つまり、このオプションは、シャープされるピクセルが周囲の領域とどの程度違えば、そのピクセルをエッジのピクセルと見なしてシャープするかを決定するものです。ノイズが入らないように、0～255 の範囲で様々な整数値を試してください。</p> </td>
  </tr>
 </tbody>
</table>

シャープの適用については、画像へ [のシャープの適用](/help/assets/dynamic-media/assets/s7_sharpening_images.pdf)を参照してください。

## ダイナミックメディア画像プロファイルの作成 {#creating-image-profiles}

他のアセットタイプへの高度な処理パラメーターの定義については、[アセット処理の設定](config-dm.md#configuring-asset-processing)を参照してください。

See [Profiles for Processing Metadata, Images, and Videos](/help/assets/dynamic-media/processing-profiles.md).

[処理プロファイルを使用するためのデジタルアセットの編成のベストプラクティス](/help/assets/dynamic-media/best-practices-for-file-management.md)を参照してください。

**ダイナミックメディアイメージプロファイルを作成するには**

1. Tap the AEM logo and navigate to **[!UICONTROL Tools > Assets > Image Profiles]**.
1. Tap **[!UICONTROL Create]** to add a new image profile.
1. プロファイル名を入力し、アンシャープマスクのほか、切り抜きとスウォッチのいずれかまたは両方の値を入力します。

   目的を具体的に表すプロファイル名を使用すると便利です。例えば、スウォッチのみを生成するプロファイルを作成する（つまり、スマート切り抜きが無効（オフ）になっていて、カラーと画像スウォッチが有効（オン）になっている）場合、「スマートスウォッチ」というプロファイル名を使用できます。

   [スマート切り抜きとスマートスウォッチオプション](#crop-options)および[アンシャープマスク](#unsharp-mask)も参照してください。

   ![作物](assets/crop.png)

1. 「**[!UICONTROL 保存]**」をタップします。新しく作成されたプロファイルが、使用可能なプロファイルのリストに表示されます。

## ダイナミックメディア画像プロファイルの編集または削除 {#editing-or-deleting-image-profiles}

1. Tap the AEM logo and navigate to **[!UICONTROL Tools > Assets > Image Profiles]**.
1. 編集または削除するイメージプロファイルを選択します。編集するには、「**[!UICONTROL 画像処理プロファイルを編集]**」を選択します。削除するには、「**[!UICONTROL 画像処理プロファイルを削除]**」を選択します。

   ![chlimage_1-254](assets/chlimage_1-254.png)

1. 編集の場合は、変更内容を保存します。削除の場合は、プロファイルの削除を確定します。

## ダイナミックメディア画像プロファイルのフォルダーへの適用 {#applying-an-image-profile-to-folders}

フォルダーにイメージプロファイルを割り当てると、サブフォルダーは自動的に親フォルダーのプロファイルを継承します。つまり、フォルダーに 1 つのイメージプロファイルのみを適用すればよいことになります。そのため、アセットをアップロード、保存、使用およびアーカイブする場所のフォルダー構造については入念に検討してください。

フォルダーに異なるイメージプロファイルを割り当てた場合、新しいプロファイルが以前のプロファイルよりも優先されます。以前に存在していたフォルダーのアセットは変更されずに維持されます。新しいプロファイルは、その後にフォルダーに追加されるアセットに対して適用されます。

プロファイルが割り当てられているフォルダーには、ユーザーインターフェイス上でカード内に表示されたときに、そのプロファイルの名前が示されます。

<!-- When you add smart crop to an existing image profile, you need to re-trigger the [DAM Update Asset workflow](assets-workflow.md) if you want to generate crops for existing assets in your asset repository. -->

イメージプロファイルは、特定のフォルダーに適用することも、全アセットにグローバルに適用することもできます。

後で変更した既存の画像プロファイルが既に存在するフォルダー内のアセットを再処理できます。 [処理プロファイルを編集した後のフォルダー内のアセットの再処理](/help/assets/dynamic-media/processing-profiles.md#reprocessing-assets)を参照してください。

### ダイナミックメディア画像プロファイルの特定のフォルダーへの適用 {#applying-image-profiles-to-specific-folders}

You can apply an image profile to a folder from within the **[!UICONTROL Tools]** menu or if you are in the folder, from **[!UICONTROL Properties]**. このセクションでは、イメージプロファイルをフォルダーに適用するための方法を両方とも説明します。

既にプロファイルが割り当てられているフォルダーには、フォルダー名のすぐ下にプロファイルの名前が表示されます。

後で変更した既存のビデオプロファイルが既に存在するフォルダー内のアセットを再処理できます。 [処理プロファイルを編集した後のフォルダー内のアセットの再処理](/help/assets/dynamic-media/processing-profiles.md#reprocessing-assets)を参照してください。

#### Applying Dynamic Media image profiles to folders from Profiles user interface {#applying-image-profiles-to-folders-from-profiles-user-interface}

1. Tap the AEM logo and navigate to **[!UICONTROL Tools > Assets > Image Profiles]**.
1. 1 つ以上のフォルダーに適用するイメージプロファイルを選択します。

   ![chlimage_1-255](assets/chlimage_1-255.png)

1. Tap **[!UICONTROL Apply Processing Profile to Folder(s)]** and select the folder or multiple folders you want use to receive the newly uploaded assets and tap/click **[!UICONTROL Apply]**. 既にプロファイルが割り当てられているフォルダーには、フォルダー名のすぐ下にプロファイルの名前が表示されます。

#### Applying Dynamic Media image profiles to folders from Properties {#applying-image-profiles-to-folders-from-properties}

1. Tap the AEM logo and navigate to **[!UICONTROL Assets]** and then to the folder that you want to apply an image profile to.
1. On the folder, tap the check mark to select it and then tap **[!UICONTROL Properties]**.
1. 「**[!UICONTROL イメージプロファイル]**」タブをタップします。From the **[!UICONTROL Profile Name]** drop-down list, select the profile, then tap **[!UICONTROL Save &amp; Close]**. 既にプロファイルが割り当てられているフォルダーには、フォルダー名のすぐ下にプロファイルの名前が表示されます。

   ![chlimage_1-256](assets/chlimage_1-256.png)

### ダイナミックメディア画像プロファイルのグローバルな適用 {#applying-an-image-profile-globally}

特定のフォルダーにプロファイルを適用できるだけでなく、グローバルにプロファイルを適用することもできます。これにより、AEM アセットにアップロードされている、すべてのフォルダー内にあるすべてのコンテンツに、選択したプロファイルを適用できます。

後で変更した既存のビデオプロファイルが既に存在するフォルダー内のアセットを再処理できます。 [処理プロファイルを編集した後のフォルダー内のアセットの再処理](/help/assets/dynamic-media/processing-profiles.md#reprocessing-assets)を参照してください。

**ダイナミックメディア画像プロファイルをグローバルに適用するには**:

1. 次のいずれかの操作をおこないます。

   * 適切なプロフ `https://&lt;AEM server&gt;/mnt/overlay/dam/gui/content/assets/foldersharewizard.html/content/dam` ァイルに移動して適用し、「保存」をタッ **[!UICONTROL プします]**。

      ![chlimage_1-257](assets/chlimage_1-257.png)

   * Navigate to CRXDE Lite to the following node: `/content/dam/jcr:content`.

      プロパティを追加し、「す `imageProfile:/conf/global/settings/dam/adminui-extension/imageprofile/<name of image profile>` べて保存」 **[!UICONTROL をタップしま]**&#x200B;す。

      ![configure_image_profiles](assets/configure_image_profiles.png)

## 単一の画像のスマート切り抜きまたはスマートスウォッチの編集 {#editing-the-smart-crop-or-smart-swatch-of-a-single-image}

画像のスマート切り抜きウィンドウの位置の再調整またはサイズの変更を手動でおこなって、焦点位置を細かく調整することができます。

スマート切り抜きを編集して保存すると、その画像の切り抜きを使用しているすべての場所で変更が反映されます。

必要に応じてスマート切り抜きを再実行して、追加の切り抜きを再度生成することができます。

[複数の画像のスマート切り抜きまたはスマートスウォッチの編集](#editing-the-smart-crop-or-smart-swatch-of-multiple-images)も参照してください。

**1つの画像のスマート切り抜きまたはスマートスウォッチを編集するには**:

1. Tap the AEM logo and navigate to **[!UICONTROL Assets]**, then to the folder that has a smart crop or smart swatch image profile applied to it.

1. フォルダーをタップして、内容を開きます。
1. スマート切り抜きまたはスマートスウォッチを調整する画像をタップします。
1. On the toolbar, tap **[!UICONTROL Smart Crop]**.

1. 次のいずれかの操作をおこないます。

   * ページの右上隅にあるスライダーバーを左右にドラッグして画像表示を拡大または縮小します。
   * 画像のコーナーハンドルをドラッグして、切り抜きまたはスウォッチの表示可能領域のサイズを調整します。
   * 画像上のボックスまたはスウォッチを新しい場所にドラッグします。画像スウォッチは編集できますが、カラースウォッチは静的です。
   * Above the image, tap  **[!UICONTROL Revert]** to undo all your edits and restore the original crop or swatch.

1. Near the upper-right corner of the page, tap **[!UICONTROL Save]**, then tap **[!UICONTROL Close]** to return to the folder of assets.

## 複数の画像のスマート切り抜きまたはスマートスウォッチの編集 {#editing-the-smart-crop-or-smart-swatch-of-multiple-images}

スマート切り抜きを含む画像プロファイルをフォルダーに適用すると、そのフォルダー内のすべての画像に切り抜きが適用されます。 If desired, you can *manually* realign or resize the smart crop window in multiple images to further refine their focal point.

スマート切り抜きを編集して保存すると、その画像の切り抜きを使用しているすべての場所で変更が反映されます。

必要に応じてスマート切り抜きを再実行して、追加の切り抜きを再度生成することができます。

**複数の画像のスマート切り抜きまたはスマートスウォッチを編集するには**:

1. Tap the AEM logo and navigate to **[!UICONTROL Assets]**, then to a folder that has a smart crop or smart swatch image profile applied to it.
1. On the folder, tap the **[!UICONTROL More Actions]** (...) icon, then tap **[!UICONTROL Smart Crop]**.

1. On the **[!UICONTROL Edit Smart Crops]** page, do any of the following:

   * ページ上の画像の表示サイズを調整します。

       ブレークポイント名のドロップダウンリストの右側にあるスライダーバーを左右にドラッグして表示可能な画像表示のサイズを変更します。

      ![edit_smart_cropps-sliderbar](assets/edit_smart_crops-sliderbar.png)

   * ブレークポイント名に基づいて表示可能な画像のリストを絞り込みます。以下の例では、「中」というブレークポイント名で画像を絞り込んでいます。

       ページの右上隅にあるドロップダウンリストから、ブレークポイント名を選択して、表示する画像を絞り込みます（上記の画像を参照してください）。

      ![edit_smart_cropps-dropdownlist](assets/edit_smart_crops-dropdownlist.png)

   * スマート切り抜きボックスのサイズを変更します。次のいずれかの操作をおこないます。

      * 画像にスマート切り抜きまたはスマートスウォッチのみが適用されている場合は、画像の切り抜きボックスのコーナーハンドルをドラッグして、切り抜きの表示可能領域のサイズを調整します。
      * 画像にスマート切り抜きとスマートスウォッチの両方が適用されている場合は、画像の切り抜きボックスのコーナーハンドルをドラッグして、切り抜きの表示可能領域のサイズを調整します。または、画像の下部にあるスマートスウォッチをタップまたはクリックしてから（カラースウォッチは静的です）、切り抜きボックスのコーナーハンドルをドラッグして、スウォッチの表示可能領域のサイズを調整します。
      ![画像のスマート切り抜きのサイズ変更。](assets/edit_smart_crops-resize.png)

   * スマート切り抜きボックスを移動します。次のいずれかの操作をおこないます。

      * 画像にスマート切り抜きまたはスマートスウォッチのみが適用されている場合は、画像の切り抜きボックスを新しい場所にドラッグします。
      * 画像にスマート切り抜きとスマートスウォッチの両方が適用されている場合は、画像の切り抜きボックスを新しい場所にドラッグします。または、画像の下部にあるスマートスウォッチをタップまたはクリックしてから（カラースウォッチは静的です）、スマートスウォッチの切り抜きボックスを新しい場所にドラッグします。
      ![edit_smart_cropps-move](assets/edit_smart_crops-move.png)

   * すべての編集作業を取り消し、元のスマート切り抜きまたはスマートスウォッチを復元します（現在の編集セッションにのみ適用されます）。

      画像の上 **[!UICONTROL の]** 「復帰」をタップします。

      ![edit_smart_crops-revert](assets/edit_smart_crops-revert.png)



1. ページの右上隅にある「**[!UICONTROL 保存]**」をタップします。then tap **[!UICONTROL Close]** to return to the folder of assets.

## フォルダーからのイメージプロファイルの削除 {#removing-an-image-profile-from-folders}

フォルダーからイメージプロファイルを削除すると、サブフォルダーは自動的に親フォルダーのプロファイルの削除状態を継承します。ただし、フォルダー内で実行されたファイルの処理はそのまま維持されます。

You can remove an image profile from a folder from within the **[!UICONTROL Tools]** menu or if you are in the folder, from **[!UICONTROL Properties]**. このセクションでは、イメージプロファイルをフォルダーから削除するための方法を両方とも説明します。

### プロファイルユーザーインターフェイスを使用したフォルダーからのダイナミックメディア画像プロファイルの削除 {#removing-image-profiles-from-folders-via-profiles-user-interface}

1. Tap the AEM logo and navigate to **[!UICONTROL Tools > Assets > Image Profiles]**.
1. 1 つ以上のフォルダーから削除するイメージプロファイルを選択します。
1. Tap **[!UICONTROL Remove Processing Profile from Folder(s)]** and select the folder or multiple folders you want use to remove the profile from and tap **[!UICONTROL Remove]**.

   名前がフォルダー名の下に表示されなくなっていることで、イメージプロファイルがフォルダーに適用されていないことを確認できます。

### プロパティを使用したフォルダーからのダイナミックメディア画像プロファイルの削除 {#removing-image-profiles-from-folders-via-properties}

1. Tap the AEM logo and navigate **[!UICONTROL Assets]** and then to the folder that you want to remove an image profile from.
1. On the folder, tap the check mark to select it, then tap **[!UICONTROL Properties]**.
1. Select the **[!UICONTROL Image Profiles]** tab.
1. 「プロファ **[!UICONTROL イル名]** 」ドロップダウンメニューで「なし **[!UICONTROL 」を選択し、「保存して閉]**&#x200B;じる」をタップします ****。

   既にプロファイルが割り当てられているフォルダーには、フォルダー名のすぐ下にプロファイルの名前が表示されます。
