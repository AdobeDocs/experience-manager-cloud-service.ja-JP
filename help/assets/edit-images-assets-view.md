---
title: 画像の編集
description: ' [!DNL Adobe Express]  を利用したオプションを使用して画像を編集し、更新した画像をバージョンとして保存します。'
role: User
exl-id: cfc4c7b7-da8c-4902-9935-0e3d4388b975
feature: Best Practices, Interactive Images, Smart Crop, Smart Imaging
source-git-commit: ab2cf8007546f538ce54ff3e0b92bb0ef399c758
workflow-type: ht
source-wordcount: '900'
ht-degree: 100%

---

# [!DNL Assets view] での画像の編集  {#edit-images}

[!DNL Assets view] には、[!DNL Adobe Express] を利用した使いやすい編集オプションが用意されています。[!DNL Adobe Express] を使用すると、画像のサイズ変更、背景の削除、画像の切り抜き、JPEG から PNG への変換、またはその逆といった編集アクションを使用できます。

画像の編集後、新しい画像を新しいバージョンとして保存できます。バージョン管理を使用すると、必要に応じて後で元のアセットに戻すことができます。また、バージョン管理は、PNG ファイルタイプでのみ使用できます。つまり、JPG ファイルファイルタイプから背景を削除しようとすると、JPG は自動的に PNG に変換されます。画像を編集するには、[プレビューを開き](navigate-assets-view.md)、「**[!UICONTROL 画像を編集]**」をクリックします。

>[!NOTE]
>
>[!DNL Adobe Express] を使用すると、PNG および JPEG ファイルタイプの画像を編集できます。

<!--The editing actions that are available are Spot healing, Crop and straighten, Resize image, and Adjust image.-->

## Adobe Express を使用した画像の編集 {#edit-using-express}

>[!CONTEXTUALHELP]
>id="assets_express_integration"
>title="Adobe Express の統合"
>abstract="AEM Assets 内で直接使用できる Adobe Express を活用した、簡単で直感的な画像編集ツールにより、コンテンツの再利用性を高め、コンテンツの速度を向上させます。"

### 画像のサイズ変更 {#resize-image-using-express}

画像を特定のサイズに変更するのが一般的なユースケースです。[!DNL Assets view] では、特定の写真サイズに対応する新しい解像度を事前に計算しておくことで、一般的な写真サイズに合わせて画像のサイズをすばやく変更できます。[!DNL Assets view] を使用して画像のサイズを変更するには、次の手順に従います。

1. [!DNL Experience Manager] アセットリポジトリから画像を選択し、「**編集**」をクリックします。
2. 左側のパネルにあるクイックアクションから「**[!UICONTROL 画像のサイズを変更]**」をクリックします。
3. **[!UICONTROL サイズを変更]**&#x200B;ドロップダウンリストから適切なソーシャルメディアプラットフォームを選択し、表示されるオプションから画像サイズを選択します。
4. 必要に応じて、「**[!UICONTROL 画像の拡大・縮小]**」フィールドを使用して画像を拡大・縮小します。
5. 「**[!UICONTROL 適用]**」をクリックし、変更を適用します。
   ![Adobe Express を使用した画像の編集](assets/adobe-express-resize-image.png)

   編集した画像はダウンロードできます。編集したアセットを同じアセットの新しいバージョンとして保存するか、新しいアセットとして保存することができます。
   ![Adobe Express を使用した画像の保存](assets/adobe-express-resize-save.png)

### 背景を削除 {#remove-background-using-express}

以下に示すように、いくつかの簡単な手順で画像から背景を削除できます。

1. [!DNL Experience Manager] アセットリポジトリから画像を選択し、「**編集**」をクリックします。
2. 左側のパネルにあるクイックアクションから「**[!UICONTROL 背景を削除]**」をクリックします。Experience Manager Assets では、背景のない画像が表示されます。
3. 「**[!UICONTROL 適用]**」をクリックし、変更を適用します。
   ![Adobe Express を使用した画像の保存](assets/adobe-express-remove-background.png)

### 画像を切り抜き {#crop-image-using-express}

埋め込まれた [!DNL Adobe Express] クイックアクションを使用すると、画像を完璧なサイズに簡単に変換できます。

1. [!DNL Experience Manager] アセットリポジトリから画像を選択し、「**編集**」をクリックします。
2. 左側のパネルにあるクイックアクションから「**[!UICONTROL 画像を切り抜き]**」をクリックします。
3. 画像の隅にあるハンドルをドラッグして、目的の切り抜きを作成します。
4. 「**[!UICONTROL 適用]**」をクリックします。
   ![Adobe Express を使用した画像の保存](assets/adobe-express-crop-image.png)
切り抜いた画像はダウンロードできます。編集したアセットを同じアセットの新しいバージョンとして保存するか、新しいアセットとして保存することができます。

### JPEG を PNG に変換 {#convert-jpeg-to-png-using-express}

Adobe Express を使用すると、JPEG 画像を PNG 形式にすばやく変換できます。以下の手順を実行します。

1. [!DNL Experience Manager] アセットリポジトリから画像を選択し、「**編集**」をクリックします。
2. 左側のパネルにあるクイックアクションから「**[!UICONTROL JPEG を PNG に変換]**」をクリックします。
   <!--![Convert to PNG with Adobe Express](/help/using/assets/adobe-express-convert-image.png)-->
3. 「**[!UICONTROL 適用]**」をクリックします。
4. **[!UICONTROL 右上の「名前を付けて保存」]**&#x200B;に移動し、「**[!UICONTROL 新しいアセットとして保存]**」をクリックします。

### PNG を JPEG に変換する {#convert-png-to-jpeg-using-express}

Adobe Express を使用すると、JPEG 画像を PNG 形式にすばやく変換できます。以下の手順を実行します。

1. [!DNL Experience Manager] アセットリポジトリから画像を選択し、「**編集**」をクリックします。
2. 左側のパネルにあるクイックアクションから「**[!UICONTROL JPEG に変換]**」をクリックします。
3. 「**[!UICONTROL 適用]**」をクリックします。
4. **[!UICONTROL 右上の「名前を付けて保存」]**&#x200B;に移動し、「**[!UICONTROL 新しいアセットとして保存]**」をクリックします。

### 制限事項 {#limitations-adobe-express}

* サポートされる画像解像度：最小 - 50 ピクセル、最大 - ディメンションあたり 6000 ピクセル。

* サポートされるファイルの最大サイズ：17 MB。

## Adobe Express 埋め込みエディターを使用した画像の編集 {#edit-using-embedded-editor}

Adobe Express へのアクセス権を持つ組織は、Adobe Express と Adobe Firefly の統合された画像編集および作成ツールを Assets ビュー内で直接利用できるようになり、コンテンツの再利用を改善し、コンテンツの速度を向上させることができます。また、定義済みの要素を使用して、アセットの見栄えを良くしたり、数回クリックするだけで画像を編集するクイックアクションを実行したりすることもできます。

[!DNL Adobe Express] 埋め込みエディターを使用して画像を編集するには、次の手順に従います。

1. [!DNL Experience Manager] Assets リポジトリから画像を選択します。
1. 「**[!UICONTROL Adobe Express で開く]**」をクリックします。

   ![Adobe Express 埋め込みエディター](assets/embedded-editor.png)

   [!DNL Adobe Express] の機能を活用して、[画像のサイズを変更](https://helpx.adobe.com/jp/express/using/resize-image.html)、[背景色を削除または変更](https://helpx.adobe.com/jp/express/using/remove-background.html)、[画像を切り抜き](https://helpx.adobe.com/jp/express/using/crop-image.html)など、画像編集に関連するすべてのアクションを実行できます。

1. 画像の編集が完了したら、アセットを新しいアセットとしてダウンロードしたり、アセットを新しいバージョンとして保存したりできます。

## Adobe Express を使用した新しいアセットの作成 {#create-new-embedded-editor}

[!DNL Assets view] では、[!DNL Adobe Express] 埋め込みエディターを使用して、新しいテンプレートを最初から作成できます。[!DNL Adobe Express] を使用して新しいアセットを作成するには、次の手順を実行します。

1. **[!UICONTROL マイワークスペース]**&#x200B;に移動し、上部に表示される Adobe Express バナー内の「**[!UICONTROL 作成]**」をクリックします。[!DNL Adobe Express] の空白のキャンバスが [!DNL Assets view] ユーザーインターフェイス内に表示されます。
1. [テンプレート](https://helpx.adobe.com/jp/express/using/work-with-templates.html)を使用してコンテンツを作成します。それ以外の場合は、**[!UICONTROL 自分のアイテム]**&#x200B;に移動して既存のコンテンツを変更します。
1. 編集が完了したら、「**[!UICONTROL 新しいアセットとして保存]**」をクリックします。
1. 作成したアセットの宛先パスを指定し、「**[!UICONTROL 保存]**」をクリックします。

>[!NOTE]
>
>* 変更できるのは、`JPEG` および `PNG` 形式タイプの画像のみです。
>* アセットサイズは 17 MB 未満にする必要があります。
>* `PDF`、`JPEG` または `PNG` 形式の画像を保存できます。つまり、複数のページがある場合は、それらを `PDF` として保存できます。

<!--
## Edit images using [!DNL Adobe Photoshop Express] {#edit-using-photoshop-express}

<!--
After editing an image, you can save the new image as a new version. Versioning helps you to revert to the original asset later, if needed. To edit an image, [open its preview](navigate-assets-view.md#preview-assets) and click **[!UICONTROL Edit Image]** ![edit icon](assets/do-not-localize/edit-icon.png) from the rail on the right.

![Options to edit an image](assets/edit-image2.png)

*Figure: The options to edit images are powered by [!DNL Adobe Photoshop Express].*
-->
<!--
### Touch up images {#spot-heal-images-using-photoshop-express}

If there are minor spots or small objects on an image, you can edit and remove the spots using the spot healing feature provided by Adobe Photoshop.

The brush samples the retouched area and makes the repaired pixels blend seamlessly into the rest of the image. Use a brush size that is only slightly larger than the spot you want to fix.

![Spot healing edit option](assets/edit-spot-healing.png)

<!-- 
TBD: See if we should give backlinks to PS docs for these concepts.
For more information about how Spot Healing works in Photoshop, see [retouching and repairing photos](https://helpx.adobe.com/photoshop/using/retouching-repairing-images.html). 
-->
<!-- 
### Crop and straighten images {#crop-straighten-images-using-photoshop-express}

Using the crop and straighten option that you can do basic cropping, rotate image, flip it horizontally or vertically, and crop it to dimensions suitable for popular social media websites.

To save your edits, click **[!UICONTROL Crop Image]**. After editing, you can save the new image as a version.

![Option to crop and straighten](assets/edit-crop-straighten.png)

Many default options let you crop your image to the best proportions that fit various social media profiles and posts.

### Resize image {#resize-image-using-photoshop-express}

You can view the common photo sizes in centimeters or inches to know the dimensions. By default, the resizing method retains the aspect ratio. To manually override the aspect ratio, click ![](assets/do-not-localize/lock-closed-icon.png).

Enter the dimensions and click **[!UICONTROL Resize Image]** to resize the image. Before you save the changes as a version, you can either undo all the changes done before saving by clicking [!UICONTROL Undo] or you can change the specific step in the editing process by clicking [!UICONTROL Revert].

![Options when resizing an image](assets/resize-image.png)

### Adjust image {#adjust-image-using-photoshop-express}

[!DNL Assets view] lets you adjust the color, tone, contrast, and more, with just a few clicks. Click **[!UICONTROL Adjust image]** in the edit window. The following options are available in the right sidebar:

* **Popular**: [!UICONTROL High Contrast & Detail], [!UICONTROL Desaturated Contrast], [!UICONTROL Aged Photo], [!UICONTROL B&W Soft], and [!UICONTROL B&W Sepia Tone].
* **Color**: [!UICONTROL Natural], [!UICONTROL Bright], [!UICONTROL High Contrast], [!UICONTROL High Contrast & Detail], [!UICONTROL Vivid], and [!UICONTROL Matte].
* **Creative**: [!UICONTROL Desaturated Contrast], [!UICONTROL Cool Light], [!UICONTROL Turquoise & Red], [!UICONTROL Soft Mist], [!UICONTROL Vintage Instant], [!UICONTROL Warm Contrast], [!UICONTROL Flat & Green], [!UICONTROL Red Lift Matte], [!UICONTROL Warm Shadows], and [!UICONTROL Aged Photo].
* **B&W**: [!UICONTROL B&W Landscape], [!UICONTROL B&W High Contrast], [!UICONTROL B&W Punch], [!UICONTROL B&W Low Contrast], [!UICONTROL B&W Flat], [!UICONTROL B&W Soft], [!UICONTROL B&W Infrared], [!UICONTROL B&W Selenium Tone], [!UICONTROL B&W Sepia Tone], and [!UICONTROL B&W Split Tone].
* **Vignetting**: [!UICONTROL None], [!UICONTROL Light], [!UICONTROL Medium], and [!UICONTROL Heavy].

![Adjust image by editing](assets/adjust-image.png)

<!--
TBD: Insert a video of the available social media options.
-->

### 次の手順 {#next-steps}

* アセットビューユーザーインターフェイスの「[!UICONTROL フィードバック]」オプションを使用して、製品に関するフィードバックを提供する

* 右側のサイドバーにある「[!UICONTROL このページを編集]」（![ページを編集](assets/do-not-localize/edit-page.png)）または「[!UICONTROL 問題を記録] 」（![GitHub イシューを作成](assets/do-not-localize/github-issue.png)）を使用してドキュメントに関するフィードバックを提供する

* [カスタマーケア](https://experienceleague.adobe.com/?support-solution=General&amp;lang=ja#support)に問い合わせる

>[!MORELIKETHIS]
>
>* [Adobe Express のクイックアクション](https://helpx.adobe.com/jp/express/using/resize-image.html)
>* [アセットのバージョン履歴を表示](navigate-assets-view.md)
