---
title: 画像の編集
description: ' [!DNL Adobe Photoshop Express]  を利用したオプションを使用して画像を編集し、更新した画像をバージョンとして保存します。'
role: User
source-git-commit: c3076ce35128c147ce2056d11d9305d9a9456636
workflow-type: tm+mt
source-wordcount: '1251'
ht-degree: 80%

---

# [!DNL Assets view] での画像の編集  {#edit-images}

[!DNL Assets view] には、[!DNL Adobe Express] と [!DNL Adobe Photoshop Express] を利用した使いやすい編集オプションが用意されています。次を使用して使用可能な編集アクション： [!DNL Adobe Express] は、画像のサイズ変更、背景の削除、画像の切り抜き、JPEGの PNG への変換（またはその逆）です。

画像の編集後、新しい画像を新しいバージョンとして保存できます。バージョン管理を使用すると、必要に応じて後で元のアセットに戻すことができます。また、バージョン管理は、PNG ファイルタイプでのみ使用できます。つまり、JPGファイルタイプから背景を削除しようとすると、JPGは自動的に PNG に変換されます。 画像を編集するには、[プレビューを開き](navigate-assets-view.md)、「**[!UICONTROL 画像を編集]**」をクリックします。

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

1. 次の場所から画像を選択： [!DNL Experience Manager] Assets リポジトリを開き、 **編集**.
2. 左側のパネルにあるクイックアクションから「**[!UICONTROL 画像のサイズを変更]**」をクリックします。
3. **[!UICONTROL サイズを変更]**&#x200B;ドロップダウンリストから適切なソーシャルメディアプラットフォームを選択し、表示されるオプションから画像サイズを選択します。
4. 必要に応じて、「**[!UICONTROL 画像の拡大・縮小]**」フィールドを使用して画像を拡大・縮小します。
5. 「**[!UICONTROL 適用]**」をクリックし、変更を適用します。
   ![Adobe Express を使用した画像の編集](assets/adobe-express-resize-image.png)

   編集した画像はダウンロードできます。編集したアセットを同じアセットの新しいバージョンとして保存するか、新しいアセットとして保存することができます。
   ![Adobe Express を使用した画像の保存](assets/adobe-express-resize-save.png)

### 背景を削除 {#remove-background-using-express}

以下に示すように、いくつかの簡単な手順で画像から背景を削除できます。

1. 次の場所から画像を選択： [!DNL Experience Manager] Assets リポジトリを開き、 **編集**.
2. 左側のパネルにあるクイックアクションから「**[!UICONTROL 背景を削除]**」をクリックします。Experience Manager Assets では、背景のない画像が表示されます。
3. 「**[!UICONTROL 適用]**」をクリックし、変更を適用します。
   ![Adobe Express を使用した画像の保存](assets/adobe-express-remove-background.png)

### 画像を切り抜き {#crop-image-using-express}

埋め込まれた [!DNL Adobe Express] クイックアクションを使用すると、画像を完璧なサイズに簡単に変換できます。

1. 次の場所から画像を選択： [!DNL Experience Manager] Assets リポジトリを開き、 **編集**.
2. 左側のパネルにあるクイックアクションから「**[!UICONTROL 画像を切り抜き]**」をクリックします。
3. 画像の隅にあるハンドルをドラッグして、目的の切り抜きを作成します。
4. 「**[!UICONTROL 適用]**」をクリックします。
   ![Adobe Express を使用した画像の保存](assets/adobe-express-crop-image.png)
切り抜いた画像はダウンロードできます。編集したアセットを同じアセットの新しいバージョンとして保存するか、新しいアセットとして保存することができます。

### JPEG を PNG に変換 {#convert-jpeg-to-png-using-express}

Adobe Express を使用すると、JPEG 画像を PNG 形式にすばやく変換できます。以下の手順を実行します。

1. 次の場所から画像を選択： [!DNL Experience Manager] Assets リポジトリを開き、 **編集**.
2. クリック **[!UICONTROL PNG に変換]** 左側のウィンドウで使用できるクイックアクションから。
   <!--![Convert to PNG with Adobe Express](/help/using/assets/adobe-express-convert-image.png)-->
3. 「**[!UICONTROL 適用]**」をクリックします。
4. に移動します。 **[!UICONTROL 右上の「名前を付けて保存」]** をクリックします。 **[!UICONTROL 新しいアセットとして保存]**.

### PNG をJPEGに変換 {#convert-png-to-jpeg-using-express}

Adobe Expressを使用すると、PNG 画像をJPEG形式にすばやく変換できます。 以下の手順を実行します。

1. 次の場所から画像を選択： [!DNL Experience Manager] Assets リポジトリを開き、 **編集**.
2. クリック **[!UICONTROL 変換JPEG]** 左側のウィンドウで使用できるクイックアクションから。
3. 「**[!UICONTROL 適用]**」をクリックします。
4. に移動します。 **[!UICONTROL 右上の「名前を付けて保存」]** をクリックします。 **[!UICONTROL 新しいアセットとして保存]**.

### 制限事項 {#limitations-adobe-express}

* サポートされる画像解像度：最小 - 50 ピクセル、最大 - サイズあたり 6000 ピクセル

* サポートされる最大ファイルサイズ：17 MB

## Adobe Express 埋め込みエディターを使用した画像の編集 {#edit-using-embedded-editor}

Adobe Expressにアクセスできる組織は、Assets ビュー内で直接利用できるAdobe ExpressやAdobe Fireflyの統合画像編集および作成ツールを使用して、コンテンツの再利用を改善し、コンテンツの速度を向上させることができます。 また、定義済みの要素を使用して、アセットの見栄えを良くしたり、数回クリックするだけで画像を編集するクイックアクションを実行したりすることもできます。

[!DNL Adobe Express] 埋め込みエディターを使用して画像を編集するには、次の手順に従います。

1. [!DNL Experience Manager] Assets リポジトリから画像を選択します。
1. 「**[!UICONTROL Adobe Express で開く]**」をクリックします。

   ![Adobe Express 埋め込みエディター](assets/embedded-editor.png)

   [!DNL Adobe Express] の機能を活用して、[画像のサイズを変更](https://helpx.adobe.com/jp/express/using/resize-image.html)、[背景色を削除または変更](https://helpx.adobe.com/jp/express/using/remove-background.html)、[画像を切り抜き](https://helpx.adobe.com/jp/express/using/crop-image.html)など、画像編集に関連するすべてのアクションを実行できます。

1. 画像の編集が完了したら、アセットを新しいアセットとしてダウンロードしたり、アセットを新しいバージョンとして保存したりできます。

## Adobe Express を使用した新しいアセットの作成 {#create-new-embedded-editor}

[!DNL Assets view] では、[!DNL Adobe Express] 埋め込みエディターを使用して、新しいテンプレートを最初から作成できます。[!DNL Adobe Express] を使用して新しいアセットを作成するには、次の手順を実行します。

1. に移動します。 **[!UICONTROL マイワークスペース]** をクリックします。 **[!UICONTROL 作成]** 」をクリックします。 [!DNL Adobe Express] の空白のキャンバスが [!DNL Assets view] ユーザーインターフェイス内に表示されます。
1. [テンプレート](https://helpx.adobe.com/jp/express/using/work-with-templates.html)を使用してコンテンツを作成します。それ以外の場合は、**[!UICONTROL 自分のアイテム]**&#x200B;に移動して既存のコンテンツを変更します。
1. 編集が完了したら、「**[!UICONTROL 新しいアセットとして保存]**」をクリックします。
1. 作成したアセットの宛先パスを指定し、「**[!UICONTROL 保存]**」をクリックします。

>[!NOTE]
>
>* 変更できるのは、`JPEG` および `PNG` 形式タイプの画像のみです。
>* アセットサイズは 17 MB 未満にする必要があります。
>* 画像を `PDF`, `JPEG`または `PNG` 書式。複数のページがある場合は、 `PDF`.

## [!DNL Adobe Photoshop Express] を使用した画像の編集 {#edit-using-photoshop-express}

<!--
After editing an image, you can save the new image as a new version. Versioning helps you to revert to the original asset later, if needed. To edit an image, [open its preview](navigate-assets-view.md#preview-assets) and click **[!UICONTROL Edit Image]** ![edit icon](assets/do-not-localize/edit-icon.png) from the rail on the right.

![Options to edit an image](assets/edit-image2.png)

*Figure: The options to edit images are powered by [!DNL Adobe Photoshop Express].*
-->

### 画像のタッチアップ {#spot-heal-images-using-photoshop-express}

画像に小さな欠点や小さなオブジェクトがある場合は、Adobe Photoshop のスポット修復機能を利用して、その欠点を編集および削除できます。

ブラシが、リタッチした領域をサンプリングし、修復したピクセルを画像の残りの部分にシームレスにブレンドします。修正する部分よりもわずかに大きいブラシサイズを使用します。

![スポット修復編集オプション](assets/edit-spot-healing.png)

<!-- 
TBD: See if we should give backlinks to PS docs for these concepts.
For more information about how Spot Healing works in Photoshop, see [retouching and repairing photos](https://helpx.adobe.com/photoshop/using/retouching-repairing-images.html). 
-->

### 画像の切り抜きと角度補正 {#crop-straighten-images-using-photoshop-express}

切り抜きと角度補正オプションを使用すると、基本的な切り抜き、画像の回転、水平方向または垂直方向の反転を行ったうえで、一般的なソーシャルメディア web サイトに適したサイズに切り抜くことができます。

編集内容を保存するには、「**[!UICONTROL 画像を切り抜き]**」をクリックします。編集後、新しい画像をバージョンとして保存できます。

![切り抜きと角度補正のオプション](assets/edit-crop-straighten.png)

多くのデフォルトオプションを使用すると、様々なソーシャルメディアのプロファイルや投稿に合わせて画像を最適な比率に切り抜くことができます。

### 画像のサイズ変更 {#resize-image-using-photoshop-express}

一般的な写真サイズをセンチまたはインチ単位で表示して、サイズを確認できます。デフォルトでは、サイズ変更時に縦横比が保持されます。縦横比を手動で上書きするには、![](assets/do-not-localize/lock-closed-icon.png) をクリックします。

サイズを入力し、「**[!UICONTROL イメージをサイズ変更]**」をクリックして画像のサイズを変更します。変更内容をバージョンとして保存する前に、「[!UICONTROL 取り消し]」をクリックして保存前に行ったすべての変更を取り消すか、「[!UICONTROL 元に戻す]」をクリックして編集プロセスの特定のステップを変更することができます。

![画像のサイズを変更する際のオプション](assets/resize-image.png)

### 画像の調整 {#adjust-image-using-photoshop-express}

[!DNL Assets view] では、数回クリックするだけでカラー、トーン、コントラストなどを調整できます。編集ウィンドウで「**[!UICONTROL 画像を調整]**」をクリックします。右側のサイドバーでは、次のオプションを使用できます。

* **一般的**：[!UICONTROL コントラスト (高) とディテール]、[!UICONTROL コントラスト (低彩度)]、[!UICONTROL 古い写真]、[!UICONTROL 白黒 ソフト]、[!UICONTROL 白黒 セピア調]
* **カラー**：[!UICONTROL ナチュラル]、[!UICONTROL 鮮明]、[!UICONTROL コントラスト (高)]、[!UICONTROL コントラスト (高) とディテール]、[!UICONTROL ビビッド]、[!UICONTROL マット]
* **クリエイティブ**：[!UICONTROL コントラスト (低彩度)]、[!UICONTROL クールライト]、[!UICONTROL ターコイズとレッド]、[!UICONTROL ソフトミスト]、[!UICONTROL ヴィンテージインスタント]、[!UICONTROL コントラスト (暖色系)]、[!UICONTROL フラットとグリーン]、[!UICONTROL レッドリフトマット]、[!UICONTROL 暖色シャドウ]、[!UICONTROL 古い写真]
* **白黒**：[!UICONTROL 白黒 風景]、[!UICONTROL 白黒 コントラスト (高)]、[!UICONTROL 白黒 型抜き]、[!UICONTROL 白黒 コントラスト (低)]、[!UICONTROL 白黒 フラット]、[!UICONTROL 白黒 ソフト]、[!UICONTROL 白黒 赤外線]、[!UICONTROL 白黒 セレン調]、[!UICONTROL 白黒 セピア調]、[!UICONTROL 白黒 明暗別色補正]
* **周辺光量補正**：[!UICONTROL なし]、[!UICONTROL 軽度]、[!UICONTROL 中度]、[!UICONTROL 重度]

![編集による画像の調整](assets/adjust-image.png)

<!--
TBD: Insert a video of the available social media options.
-->

### 次の手順 {#next-steps}

* アセットビューユーザーインターフェイスの「[!UICONTROL フィードバック]」オプションを使用して、製品に関するフィードバックを提供する

* 右側のサイドバーにある「[!UICONTROL このページを編集]」（![ページを編集](assets/do-not-localize/edit-page.png)）または「[!UICONTROL 問題を記録] 」（![GitHub イシューを作成](assets/do-not-localize/github-issue.png)）を使用してドキュメントに関するフィードバックを提供する

* [カスタマーケア](https://experienceleague.adobe.com/?support-solution=General&amp;lang=ja#support)に問い合わせる

>[!MORELIKETHIS]
>
>* [クイックアクションのAdobe Express](https://helpx.adobe.com/jp/express/using/resize-image.html)
>* [アセットのバージョン履歴の表示](navigate-assets-view.md)
