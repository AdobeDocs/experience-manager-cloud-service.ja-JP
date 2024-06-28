---
title: 画像の編集
description: ' [!DNL Adobe Express]  を利用したオプションを使用して画像を編集し、更新した画像をバージョンとして保存します。'
role: User
exl-id: cfc4c7b7-da8c-4902-9935-0e3d4388b975
feature: Best Practices, Interactive Images, Smart Crop, Smart Imaging
source-git-commit: 23b43f22b62451c9d0a5460999fcd43479438d7e
workflow-type: tm+mt
source-wordcount: '1089'
ht-degree: 35%

---

# [!DNL Assets view] での画像の編集  {#edit-images-in-assets-view}

Assets ビューでは、サイズ変更、背景の削除、切り抜き、JPEG形式と PNG 形式の変換などの基本的な画像編集が可能です。 また、Adobe Expressとの連携による高度な編集も可能です。 画像の編集後、新しい画像を新しいバージョンとして保存できます。バージョン管理を使用すると、必要に応じて後で元のアセットに戻すことができます。 画像を編集するには、[プレビューを開き](https://experienceleague.adobe.com/en/docs/experience-manager-assets-essentials/help/navigate-view#preview-assets)、「**画像を編集**」をクリックします。

>[!NOTE]
>
>[!DNL Adobe Express] を使用すると、PNG および JPEG ファイルタイプの画像を編集できます。

<!--The editing actions that are available are Spot healing, Crop and straighten, Resize image, and Adjust image.-->

## 画像を編集 {#edit-image}

次のリンクを使用して、Assets ビューに移動します。 [Assets ビュー](https://experience.adobe.com/#/assets) 適切なリポジトリを選択します。 アクセス権を受け取るには、組織の管理者に問い合わせてください。
その他の参照情報については、次を参照してください。 [Adobe Experience Manager Assets ビューの概要](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/assets/assets-view/get-started-assets-view), [Assets ビューのユーザーインターフェイスについて](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/assets/assets-view/navigate-assets-view#understand-interface-navigation)、および [Assets ビューのユースケース](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/assets/assets-view/get-started-assets-view#use-cases).
<!--
>[!CONTEXTUALHELP]
>id="assets_express_integration"
>title="Adobe Express Integration"
>abstract="Easy and intuitive image-editing tools powered by Adobe Express available directly within AEM Assets to increase content reuse and accelerate content velocity."-->

### Adobe Expressを使用してAssets ビューの画像を編集 {#edit-image-on-assets-view-using-adobe-express}

Assets ビューにランディングしたら、 **Assets**&#x200B;画像を選択し、をクリックします。 **編集** 上のパネルから。 新しい画面には、サイズ変更、背景の削除、切り抜き、JPEG形式と PNG 形式の変換など、使用可能な編集オプションが表示されます。

#### 画像のサイズ変更 {#resize-image-using-express}

画像を特定のサイズに変更するのが一般的なユースケースです。Assets表示では、特定の写真サイズに対応する新しい解像度を事前に計算しておくことで、一般的な写真サイズに合わせて画像のサイズをすばやく変更できます。 Assets ビューを使用して画像のサイズを変更するには、次の手順に従います。

1. クリック **画像のサイズ変更** 左側のウィンドウから。
1. サイズ変更ドロップダウンリストから適切なソーシャルメディアプラットフォームを選択し、表示されるオプションから画像サイズを選択します。
1. 必要に応じて、「**画像の拡大・縮小**」フィールドを使用して画像を拡大・縮小します。
1. 「**[!UICONTROL 適用]**」をクリックし、変更を適用します。
   ![Adobe Express を使用した画像の編集](assets/adobe-express-resize-image.png)

   編集した画像はダウンロードできます。編集したアセットを同じアセットの新しいバージョンとして保存するか、新しいアセットとして保存することができます。
   ![Adobe Express を使用した画像の保存](assets/adobe-express-resize-save.png)

#### 背景を削除 {#remove-background-using-express}

画像から背景を削除するには、次の手順を実行します。

1. クリック **背景の削除** 左側のウィンドウから。 Experience Manager Assets では、背景のない画像が表示されます。
1. 「**[!UICONTROL 適用]**」をクリックし、変更を適用します。
   ![Adobe Express を使用した画像の保存](assets/adobe-express-remove-background.png)

   編集した画像はダウンロードできます。編集したアセットを同じアセットの新しいバージョンとして保存するか、新しいアセットとして保存することができます。

#### 画像を切り抜き {#crop-image-using-express}

埋め込みを使用すれば、画像を完全なサイズに簡単に変換できます [!DNL Adobe Express] クイックアクション。

1. クリック **[!UICONTROL 画像を切り抜き]** 左側のウィンドウから。
2. 画像の隅にあるハンドルをドラッグして、目的の切り抜きを作成します。
3. 「**[!UICONTROL 適用]**」をクリックします。
   ![Adobe Express を使用した画像の保存](assets/adobe-express-crop-image.png)
切り抜いた画像はダウンロードできます。編集したアセットを同じアセットの新しいバージョンとして保存するか、新しいアセットとして保存することができます。

#### 画像ファイルタイプ間の変換 {#convert-image-types-using-express}

Adobe Expressを使用して、JPEG画像フォーマットと PNG 画像フォーマットをすばやく変換できます。 以下の手順を実行します。

1. クリック **PNG にJPEG** または **PNG からJPEG** 左側のウィンドウから。
   <!--![Convert to PNG with Adobe Express](/help/using/assets/adobe-express-convert-image.png)-->
1. 「**[!UICONTROL ダウンロード]**」をクリックします。

#### 制限事項 {#limitations-adobe-express}

* サポートされる画像解像度：最小 - 50 ピクセル、最大 - ディメンションあたり 6000 ピクセル。

* サポートされるファイルの最大サイズ：17 MB。

### Adobe Express埋め込みエディターでの画像の編集 {#edit-images-in-adobe-express-embedded-editor}

Express の使用権限を持つユーザーは、Assets ビュー内から組み込みの Express Editor を使用して、コンテンツを簡単に編集し、Adobe Fireflyから GenAI で新しいコンテンツを作成できます。 これにより、コンテンツの再利用が向上し、コンテンツベロシティ（コンテンツ創出速度）が向上します。 また、事前定義済みの要素を使用して、アセットを美しく見せたり、数回クリックするだけで画像を編集するクイックアクションを実行したりできます。
![essentials UI で表現](/help/assets/assets/express-in-essentials-ui.jpg)
を使用して画像を編集するには [!DNL Adobe Express] 埋め込みエディターでは、次の手順に従います。

1. リンクを使用してAEM Assets ビューに移動します。 [AEM Assets ビュー](https://experience.adobe.com/#/assets) 適切なリポジトリを選択します。
1. クリック **Assets**&#x200B;でフォルダーを入力し、画像を選択します。
1. クリック **Adobe Expressーで開く**. 画像が高速キャンバスで開きます。
1. 画像に対して必要な編集を行います。
1. プロジェクトでページを追加する必要がある場合は、 **追加**&#x200B;を選択し、アセットを選択してフォルダーを入力し、キャンバスページに取り込む画像を選択して、画像に対して必要な編集を実行します。
1. 画像を保存するには、をクリックします **保存**. 保存ダイアログボックスが表示されます。

   >[!NOTE]
   >
   > **1. 単一ページの場合**
   >
   > **バージョンとして保存：** この機能は、単一のアセットの保存のみをサポートします。 このオプションを選択すると、画像を新しいバージョンとして（元の形式を保持して）書き出し、同じフォルダーに保存できます。
   > **新しいアセットとして保存：** 元のアセットとは異なる形式でアセットを書き出し、新しいアセットとして任意のフォルダーに保存するには、このオプションを選択します。
   >  
   > **2. 複数ページの場合**
   >
   > **バージョンとして保存：** この機能は、単一のアセットの保存のみをサポートします。 複数のページから 1 つのページを保存する場合、このオプションを選択して、元の形式と場所でアセットを保存します。\
   > **新しいアセットとして保存：** このオプションを使用すると、複数のアセットまたは単一のアセットを任意のフォルダーに書き出し、それらを元のファイル形式または別のファイル形式で新しいアセットとして保存できます。

1. 保存ダイアログボックスで、次の手順を実行します。
   1. 内のファイルの名前を入力 **名前を付けて保存** フィールド。
   1. 宛先フォルダーを選択します。
   1. オプション：プロジェクトまたはキャンペーンの名前、キーワード、チャネル、期間、地域などの詳細を指定します。
1. クリック **バージョンとして保存** または **新規アセットとして保存** をクリックしてアセットを保存します。

#### Express Editor での画像編集の制限 {#limitations-of-editing-images-in-the-express-editor}

* サポートされているファイルタイプ：JPEGまたは PNG。
* サポートされるファイルの最大サイズ：40 MB。
* サポートされる幅と高さの範囲：50 ～ 8000 ピクセル。
* ページをリロードして、ソースフォルダーに保存された最新の新しいアセットを表示します。

### Adobe Express を使用した新しいアセットの作成 {#create-new-embedded-editor}

[!DNL Assets view] では、[!DNL Adobe Express] 埋め込みエディターを使用して、新しいテンプレートを最初から作成できます。[!DNL Adobe Express] を使用して新しいアセットを作成するには、次の手順を実行します。

1. **[!UICONTROL マイワークスペース]**&#x200B;に移動し、上部に表示される Adobe Express バナー内の「**[!UICONTROL 作成]**」をクリックします。[!DNL Adobe Express] の空白のキャンバスが [!DNL Assets view] ユーザーインターフェイス内に表示されます。
1. [テンプレート](https://helpx.adobe.com/jp/express/using/work-with-templates.html)を使用してコンテンツを作成します。それ以外の場合は、**[!UICONTROL 自分のアイテム]**&#x200B;に移動して既存のコンテンツを変更します。
1. 編集が完了したら、 **[!UICONTROL 保存]**.
1. 作成したアセットの宛先パスを指定し、をクリックします **[!UICONTROL 新規アセットとして保存]**.

#### 制限事項 {#limitations}

* 変更できるのは、`JPEG` および `PNG` 形式タイプの画像のみです。
* アセットサイズは 40 MB 未満にする必要があります。
* 画像は、`PDF`、`JPEG` または `PNG` 形式で保存できます。

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

* を使用して製品に関するフィードバックを提供する [!UICONTROL Feedback] オプションは、Assets ビューのユーザーインターフェイスで使用できます。

* 右側のサイドバーにある「[!UICONTROL このページを編集]」 ![ページを編集](assets/do-not-localize/edit-page.png) または「[!UICONTROL イシューを記録]」 ![GitHub イシューを作成](assets/do-not-localize/github-issue.png) を使用してドキュメントのフィードバックを提供する。

* [カスタマーケア](https://experienceleague.adobe.com/?support-solution=General&amp;lang=ja#support)に問い合わせる

>[!MORELIKETHIS]
>
>* [Adobe Express のクイックアクション](https://helpx.adobe.com/jp/express/using/resize-image.html)
>* [アセットのバージョン履歴を表示](navigate-assets-view.md)
