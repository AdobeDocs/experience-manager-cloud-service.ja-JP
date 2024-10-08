---
title: ビデオの編集
description: を利用したオプションを使用してビデオ  [!DNL Adobe Express]  編集し、更新したビデオをバージョンとして保存します。
role: User
exl-id: 42b25935-e2ff-444f-97c8-b4ed56f3ef9e
feature: Best Practices, Video, Interactive Videos
source-git-commit: e3fd0fe2ee5bad2863812ede2a294dd63864f3e2
workflow-type: tm+mt
source-wordcount: '797'
ht-degree: 19%

---

# [!DNL Assets view] でビデオを編集する {#edit-videos}

| [ 検索のベストプラクティス ](/help/assets/search-best-practices.md) | [ メタデータのベストプラクティス ](/help/assets/metadata-best-practices.md) | [コンテンツハブ](/help/assets/product-overview.md) | [OpenAPI 機能を備えたDynamic Media](/help/assets/dynamic-media-open-apis-overview.md) | [AEM Assets開発者向けドキュメント ](https://developer.adobe.com/experience-cloud/experience-manager-apis/) |
| ------------- | --------------------------- |---------|----|-----|

ビデオ用の埋め込みクイックアクションを使用すると、Assets ユーザーは、ビデオコンテンツのバリエーション [!DNL Adobe Express] 簡単に作成できます。 [!DNL Adobe Express] を利用した [!DNL Assets view] のクイックアクションでは、ビデオの切り抜き、ビデオのサイズ変更、ビデオのトリミング、ビデオのGIFへの変換など、使いやすいビデオ編集オプションが提供されています。

ビデオを編集するには、ビデオの詳細に移動し、「[!UICONTROL  ビデオを編集 ]」をクリックします。 または、アセットを選択して「詳細」をクリックし、右側のパネルにある ![ はさみ ](assets/do-not-localize/cut.svg) アイコンをクリックします。 ビデオの編集後、新しいビデオを新しいバージョンまたは新しいアセットとして保存できます。

## 前提条件 {#prerequisites}

AEM Assets内の [!DNL Adobe Express] および少なくとも 1 つの環境にアクセスするための権限。 環境には、[!DNL Assets as a Cloud Service] または [!DNL Assets view] 内の任意のリポジトリを指定できます。

## Adobe Express を使用したビデオの編集 {#edit-video-using-express}

埋め込みおよ [!DNL Adobe Express] クイックアクションを使用すると、ビデオを最適なサイズと向きに簡単に変換できます。

### ビデオを切り抜く {#crop-video-using-express}

埋め込みまたはクイックアクションを使用して、ビデオから不要な部分 [!DNL Adobe Express] 削除できます。 これを行うには、以下の手順を実行します。

1. ビデオを選択し、「**[!UICONTROL 編集]**」をクリックします。
2. 左側のパネルで使用可能なクイックアクションから **[!UICONTROL ビデオを切り抜き]** をクリックします。
3. ビデオの隅にあるハンドルをドラッグして目的の切り抜きを作成するか、必要に応じて既存の画面サイズから選択します。
4. ビデオのミュートまたはミュート解除を選択できます。
5. 「**[!UICONTROL 適用]**」をクリックします。
   ![Adobe Express を使用したビデオの切り抜き](assets/adobe-express-crop-video.png)

   切り抜いたビデオはダウンロードできます。 編集したアセットは、同じアセットの新しいバージョンとして保存するか、新しいアセットとして保存できます。 ![Adobe Expressでビデオを保存 ](assets/adobe-express-save-video.png)

### ビデオのサイズ変更 {#resize-video-using-express}

特定のチャネルに配信するために、DAM の最終的なビデオコンテンツのサイズを変更する必要が出ることがよくあります。 [!DNL Assets view] を使用すると、一般的なソーシャルチャネルで必要なサイズに合わせてビデオのサイズを簡単に変更できます。また、カスタム解像度に合わせてサイズを変更することもできます。 [!DNL Assets view] を使用してビデオのサイズを変更するには、次の手順を実行します。

1. ビデオを選択し、「**[!UICONTROL 編集]**」をクリックします。
2. 左側のペインで使用可能なクイックアクションから **[!UICONTROL ビデオのサイズ変更]** をクリックします。
3. **[!UICONTROL 次のサイズに変更]** ドロップダウンリストの下のソーシャルメディアプラットフォームから適切なディメンションを選択します。 または、ビデオの隅にあるハンドルをドラッグして、目的の切り抜きを作成します。
4. 必要に応じて、「ビデオスケール **[!UICONTROL フィールドを使用してビデオを拡大・縮小]** ます。
5. ビデオのミュートまたはミュート解除を選択できます。
6. 「**[!UICONTROL 適用]**」をクリックし、変更を適用します。
   ![Adobe Expressを使用したビデオのサイズ変更 ](assets/adobe-express-resize-video.png)

サイズを変更したビデオはダウンロードできます。 編集したアセットを同じアセットの新しいバージョンとして保存するか、新しいアセットとして保存することができます。

### ビデオをトリミング {#trim-video-using-express}

より大きなビデオのクリップを使用する必要がある場合は、**[!UICONTROL ビデオをトリミング]** 機能を使用して、ビデオの一部を選択してトリミングできます。 以下の手順を実行します。

1. ビデオを選択し、「**[!UICONTROL 編集]**」をクリックします。
2. 左側のペインで使用可能なクイックアクションから **[!UICONTROL ビデオをトリミング]** をクリックします。
3. ビデオの特定の部分をトリミングするには、ビデオの開始時間と終了時間を指定します。 または、ビデオの隅にあるハンドルをドラッグして、目的のトリミングを作成します。
4. **[!UICONTROL サイズ]** ドロップダウンリストから適切な寸法を選択します。
5. ビデオのミュートまたはミュート解除を選択できます。
6. 「**[!UICONTROL 適用]**」をクリックし、変更を適用します。
   ![Adobe Expressを使用したビデオのサイズ変更 ](assets/adobe-express-trim-video.png)

トリミングしたビデオをダウンロードできます。 編集したアセットを同じアセットの新しいバージョンとして保存するか、新しいアセットとして保存することができます。

### ビデオをGIFに変換 {#convert-mp4-to-gif-using-express}

Adobe Expressを使用して、MP4 ビデオをGIF形式にすばやく変換できます。 次の手順を実行します。

1. ビデオを選択し、「**[!UICONTROL 編集]**」をクリックします。
2. 左側のペインで使用可能なクイックアクションから **[!UICONTROL GIFに変換]** をクリックします。
3. 画質に応じて適切なファイルサイズを選択します。 さらに、横、縦、正方形の向きを選択します。
4. ビデオの隅にあるハンドルをドラッグして、目的の切り抜きを作成します。
5. 「**[!UICONTROL 適用]**」をクリックします。

   ![Adobe Expressを使用してビデオをGIFに変換 ](assets/adobe-express-convert-video-to-gif.png)

ビデオは、GIF形式でダウンロードできます。 編集したアセットを同じアセットの新しいバージョンとして保存するか、新しいアセットとして保存することができます。

## 制限事項 {#limitations-video-adobe-express}

* 編集には MP4 形式のビデオのみがサポートされます。

* サポートされるソースファイルの最大サイズは 1 GB です。

* サポートされるビデオは、どの側も 46 ピクセルを超え、3840 ピクセル未満です。

* サポートされている web ブラウザーは、Google Chrome、Firefox、Safari、Edgeです。

* 機能は、web ブラウザーの匿名モードでは開けません。

### 次の手順 {#next-steps}

* アセットビューのユーザーインターフェイスの「[!UICONTROL フィードバック]」オプションを使用して製品に関するフィードバックを提供する。

* 右側のサイドバーにある「[!UICONTROL このページを編集]」 ![ページを編集](assets/do-not-localize/edit-page.png) または「[!UICONTROL イシューを記録]」 ![GitHub イシューを作成](assets/do-not-localize/github-issue.png) を使用してドキュメントのフィードバックを提供する

* [カスタマーケア](https://experienceleague.adobe.com/ja?support-solution=General#support)に問い合わせる

>[!MORELIKETHIS]
>
>* [Assets ビューでの画像の編集 ](edit-images-assets-view.md)
>* [ アセットのプレビュー ](navigate-assets-view.md)
