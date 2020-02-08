---
title: 画像プリセットの管理
description: 画像プリセットの概要と、画像プリセットを作成、変更および管理する方法について説明します。
translation-type: tm+mt
source-git-commit: 82dd9bd69fe994f74c7be8a571e386f0e902f6a1

---


# 画像プリセットの管理{#managing-image-presets}

画像プリセットを使用すると、異なるサイズや異なる形式の画像、あるいは動的に生成された他の画像プロパティを設定した画像を動的に配信できます。各画像プリセットは、画像表示用のサイズやフォーマットに関するコマンドの事前定義済みコレクションを表します。画像プリセットの作成時には、画像配信用のサイズを選択します。またフォーマットコマンドも選択し、表示対象画像の配信時に画像の見た目が最適化されるようにします。

管理者は、アセットを書き出すためのプリセットを作成できます。ユーザーは画像を書き出すときにプリセットを選択できます。また、この操作によって、管理者が指定した仕様に合わせて画像が再フォーマットされます。

レスポンシブな画像プリセットを作成することもできます。アセットにレスポンシブな画像プリセットを適用すると、画像が表示するデバイスや画面サイズに応じて変化します。画像プリセットは、RGB またはグレーに加えて CMYK をカラースペースで使用するよう設定できます。

ここでは、画像プリセットを作成、変更および全般的に管理する方法について説明します。作成者は画像をプレビューするときに、いつでも画像プリセットを適用できます。See [Applying Image Presets](/help/assets/dynamic-media/image-presets.md).

>[!NOTE]
>
>スマートイメージングは、既存の画像プリセットで機能し、配信の直前にインテリジェンスを使用して、ブラウザーまたはネットワークの接続速度に基づいて画像のファイルサイズをさらに低減します。See [Smart Imaging](/help/assets/dynamic-media/imaging-faq.md) for more information.

## 画像プリセットの概要 {#understanding-image-presets}

各画像プリセットはマクロと同様に、サイズおよびフォーマットのコマンドに関する事前定義済みのコレクションが、特定の名前で保存されたものです。画像プリセットの仕組みを理解するために、Web サイトで各商品画像を、デスクトップ配信用とモバイル配信用に異なるサイズ、異なる形式および圧縮率で表示する必要があるとします。

次の2つの画像プリセットを作成できます。デスクトップバージョンは500 x 500ピクセル、モバイルバージョンは150 x 150ピクセルです。 2つの画像プリセットを作成します。1つは、 `Enlarge` 500 x 500ピクセルで画像を表示するためのプリセットで、もう1つは、150 x 150 `Thumbnail` ピクセルで画像を表示するためのプリセットです。 画像をサイズとサイズで配信す `Enlarge` るた `Thumbnail` めに、AEMは「拡大画像プリセット」と「サムネール画像プリセット」の定義を調べます。 その後、AEMは各画像プリセットのサイズと形式の指定に従って画像を動的に生成します。

この場合、動的に配信されるときに画像のサイズを削減すると、シャープさと細部の表現が失われる可能性があります。この理由で、各画像プリセットには、画像を特定のサイズで配信するときに最適化するためのフォーマット用のコントロールが含まれています。これらのコントロールによって、Web サイトまたはアプリケーションに画像が配信されるときに、画像がシャープでクリアに表示されるようになります。

管理者が画像プリセットを作成できます。画像プリセットを作成する際に、最初から作業を始めることも、既存のプリセットから始めて新しい名前で保存することもできます。

## 画像プリセットの管理 {#managing-image-presets-1}

You manage your image presets in AEM by tapping or clicking the AEM logo to access the global navigation console and then tapping or clicking the Tools icon and navigating to **[!UICONTROL Assets > Image Presets]**.

![6_5_tools-assets-imagepresets](assets/6_5_tools-assets-imagepresets.png)

>[!NOTE]
>
>作成した画像プリセットは、アセットをプレビューまたは配信する際の動的レンディションとしても使用できます。
>
>画像プリセットは自動的に公開されるので、手動で公開する必要は&#x200B;*ありません*。
>
>[画像プリセットの公開](#publishing-image-presets)を参照してください。

>[!NOTE]
>
>アセットの詳細表示で「**[!UICONTROL レンディション]**」を選択すると、様々なレンディションがシステムによって表示されます。表示される画像プリセットの数を増減させることができます。[表示される画像プリセット数の引き上げ](#increasing-or-decreasing-the-number-of-image-presets-that-display)を参照してください。

### Adobe Illustrator（AI）、Postscript（EPS）および PDF のファイル形式 {#adobe-illustrator-ai-postscript-eps-and-pdf-file-formats}

AI、EPS および PDF 形式の取り込みをサポートし、これらのファイル形式の動的レンディションを生成する場合、画像プリセットを作成する前に次の情報を確認することをお勧めします。

Adobe Illustrator のファイル形式は PDF のバリアントです。AEM Assets における主な違いは、次のとおりです。

* Adobe Illustrator のドキュメントは複数のレイヤーを持つ単一のページで構成されます。各レイヤーはメインの Illustrator アセットの下に PNG サブアセットとして抽出されます。
* PDF のドキュメントは 1 つ以上のページで構成されます。各ページはメインの複数ページの PDF ドキュメントの下に単一ページの PDF サブアセットとして抽出されます。

サブアセットは、ワークフロー全体内のコンポ `Create Sub Asset process` ーネントによって作成さ `DAM Update Asset` れます。 ワークフローにこのプロセスコンポーネントを表示するには、**[!UICONTROL ツール／ワークフロー／モデル／DAM アセットの更新／編集]**&#x200B;をタップします。

<!-- See also [Viewing pages of a multi-page file](/help/assets/manage-linked-subassets.md#view-pages-of-a-multi-page-file). -->

  サブアセットまたはページは、アセットを開き、コンテキストメニューをタップし、「**[!UICONTROL サブアセット]**」または「**[!UICONTROL ページ]**」を選択して表示できます。サブアセットは実在のアセットです。That is, PDF pages are extracted by the `Create Sub Asset` workflow component. They are then stored as `page1.pdf`, `page2.pdf`, and so on below the main asset. 保存された後、ワークフローはそ `DAM Update Asset` れらを処理します。

  Dynamic Media を使用して AI、EPS または PDF ファイルの動的レンディションを表示および生成するには、次の処理ステップが必要です。

1. ワークフロー `DAM Update Asset` では、プロセ `Rasterize PDF/AI Image Preview Rendition` スコンポーネントは、設定された解像度を使用して、元のアセットの最初のページをレンディションにラスタライズ `cqdam.preview.png` します。

1. The `cqdam.preview.png` rendition is then optimized into a PTIFF by the `Dynamic Media Process Image Assets` process component within the workflow.

>[!NOTE]
>
>DAM アセットの更新ワークフローでは、**[!UICONTROL EPS サムネール]**&#x200B;のステップで EPS ファイルのサムネールが生成されます。

#### PDF／AI／EPS アセットのメタデータプロパティ {#pdf-ai-eps-asset-metadata-properties}

| **メタデータプロパティ** | **説明** |
|---|---|
| dam:Physicalwidthininches | ドキュメントの幅（インチ単位） |
| dam:Physicalheightininches | ドキュメントの高さ（インチ単位） |

プロセスコンポ `Rasterize PDF/AI Image Preview Rendition` ーネントのオプションは、ワークフローを通じてアクセ `DAM Update Asset` スします。

Tap on Adobe Experience Manager in the upper left, navigate to **[!UICONTROL Tools > Workflow > Models]**. ワークフローモデルページで「**[!UICONTROL DAM アセットの更新]**」を選択し、ツールバーの「**[!UICONTROL 編集]**」をタップします。DAMアセットの更新ワークフローページで、プロセスコンポーネントをダブルタッ `Rasterize PDF/AI Image Preview Rendition` プして、ステップのプロパティダイアログボックスを開きます。

#### PDF／AI 画像プレビューレンディションをラスタライズのオプション {#rasterize-pdf-ai-image-preview-rendition-options}

![PDF または AI ワークフローのラスタライズの引数](assets/rasterize_pdf_ai_image_preview.png)

PDF または AI ワークフローのラスタライズの引数

<table>
 <tbody>
  <tr>
   <td><strong>プロセス引数</strong></td>
   <td><strong>デフォルト設定</strong></td>
   <td><strong>説明</strong></td>
  </tr>
  <tr>
   <td>MIME タイプ</td>
   <td><p>application/pdf</p> <p>application/postscript</p> <p>application/illustrator<br /> </p> </td>
   <td>PDF または Illustrator のドキュメントと見なされるドキュメントの MIME タイプのリスト。<br /> </td>
  </tr>
  <tr>
   <td>最大の幅</td>
   <td>2048</td>
   <td>生成されたプレビューレンディションの最大の幅（ピクセル単位）。<br /> </td>
  </tr>
  <tr>
   <td>最大の高さ</td>
   <td>2048</td>
   <td>生成されたプレビューレンディションの最大の高さ（ピクセル単位）。<br /> </td>
  </tr>
  <tr>
   <td>解像度</td>
   <td>72</td>
   <td>最初のページをラスタライズする解像度（ppi（インチあたりピクセル数）単位）</td>
  </tr>
 </tbody>
</table>

デフォルトのプロセス引数を使用して、PDF／AI ドキュメントの最初のページが 72 ppi でラスタライズされ、生成されたプレビュー画像のサイズは 2048 x 2048 ピクセルになります。通常のデプロイメントでは、解像度を 150 ppi 以上に増やす必要がある場合があります。例えば、300 ppi の US Letter サイズのドキュメントの幅と高さにはそれぞれ最大で 2550 x 3300 ピクセルが必要です。

  ラスタライズする解像度を制限する最大の幅と最大の高さ。例えば、最大値が変更されず、解像度が 300 ppi に設定された場合、US Letter のドキュメントは 186 ppi でラスタライズされます。つまり、ドキュメントは 1581 x 2046 ピクセルになります。

The `Rasterize PDF/AI Image Preview Rendition` process component has a maximum defined to ensure that it does not create overly large images in memory. このようなサイズの大きな画像は、JVM（Java Virtual Machine）で提供されているメモリをオーバーフローさせることがあります。それぞれ設定された最大サイズで画像を作成可能なワークフローを、設定した数だけ並行して管理するのに十分なメモリを JVM に提供する必要があります。

### InDesign（INDD）ファイル形式 {#indesign-indd-file-format}

INDD 形式の取り込みをサポートし、これらのファイル形式の動的レンディションを生成する場合、画像プリセットを作成する前に次の情報を確認することをお勧めします。

InDesign ファイルでは、Adobe InDesign サーバーが AEM に統合されている場合にのみサブアセットが抽出されます。参照元のアセットは、メタデータに基づいてリンクされます。リンク設定に InDesign サーバーは不要です。ただし、リンクが InDesign ファイルと参照元のアセットの間に作成されるには、InDesign ファイルが処理される前に参照元のアセットが AEM 内に存在する必要があります。

<!-- See [Integrating AEM Assets with InDesign Server](/help/assets/indesign.md). -->

The Media Extraction process component in the `DAM Update Asset` workflow runs several pre-configured Extend Scripts to process InDesign files.

![メディア抽出プロセスの引数で使用される ExtendScript のパス](/help/assets/dynamic-media/assets/6_5_mediaextractionprocess.png)

DAM アセットの更新ワークフローのメディア抽出プロセスコンポーネントの引数で使用される ExtendScript のパス

Dynamic Media 統合では、以下のスクリプトが使用されます。

<table>
 <tbody>
  <tr>
   <td><strong>拡張スクリプト名</strong></td>
   <td><strong>デフォルト値は</strong></td>
   <td><strong>説明</strong></td>
  </tr>
  <tr>
   <td>ThumbnailExport.jsx</td>
   <td>はい</td>
   <td>最適化された300 ppiのレンディシ <code>thumbnail.jpg</code> ョンを生成し、プロセスコンポーネントによってPTIFFレンディションに <code>Dynamic Media Process Image Assets</code> 変換します。<br /> </td>
  </tr>
  <tr>
   <td>JPEGPagesExport.jsx</td>
   <td>はい</td>
   <td>各ページに 300 ppi の JPEG サブアセットを生成します。JPEG サブアセットは実在のアセットで、InDesign アセットの下に保存されます。It is also optimized and turned into a PTIFF by the <code>DAM Update Asset</code> workflow.<br /> </td>
  </tr>
  <tr>
   <td>PDFPagesExport.jsx</td>
   <td>いいえ</td>
   <td>各ページに PDF サブアセットを生成します。PDF サブアセットは前述のように処理されます。PDF には 1 つのページのみ含まれているので、サブアセットは生成されません。<br /> </td>
  </tr>
 </tbody>
</table>

### Configuring image thumbnail size {#configuring-image-thumbnail-size}

**[!UICONTROL DAM アセットの更新]**&#x200B;ワークフローで設定することにより、サムネールのサイズを設定できます。画像アセットのサムネールサイズの設定にはワークフローで 2 つのステップがあります。1 つ（**[!UICONTROL Dynamic Media プロセスの画像アセット]**）はダイナミック画像アセット用に、もう 1 つは（**[!UICONTROL サムネールを処理]**）は静的サムネール生成または他のすべての処理が失敗した際のサムネール生成に利用されますが、*双方とも*&#x200B;同じ設定になっている必要があります。

**[!UICONTROL Dynamic Media プロセスの画像アセット]**&#x200B;のステップでは、サムネールは画像サーバーで生成されます。この設定は、**[!UICONTROL サムネールを処理]**&#x200B;のステップで適用される設定とは独立した設定です。Generating thumbnails through the **[!UICONTROL Process Thumbnails]** step is the slowest and most memory intensive way to create thumbnails.

サムネールのサイズは次のフォーマットで定義されます。**[!UICONTROL width:height:center]**。例えば *80:80:false* となります。width と height はサムネールのサイズをピクセル単位で定義します。center の値は、false または true で、サムネール画像が設定で指定されたのとまったく同じサイズであることを示します。サイズ変更した画像が小さい場合は、サムネールの中央に配置されます。

>[!NOTE]
>
>* EPS ファイルのサムネールサイズは 「サムネール」の下の「**[!UICONTROL 因数]**」タブにある **[!UICONTROL EPS サムネール]**&#x200B;のステップで設定します。
   >
   >
* ビデオのサムネールサイズは「**[!UICONTROL 因数]**」の下にある「**[!UICONTROL 処理]**」タブの **[!UICONTROL FFmpeg サムネール]**&#x200B;のステップで設定します。
>



**画像サムネールのサイズを設定するには**

1. Tap **[!UICONTROL Tools > Workflow > Models > DAM Update Asset > Edit]**.
1. Tap the **[!UICONTROL Dynamic Media Process Image Assets]** step and tap the **[!UICONTROL Thumbnails]** tab. 必要に応じてサムネールのサイズを変更し、「**[!UICONTROL OK]**」をタップします。

   ![6_5_dynamicmediaprocessimageassets-thumbnailstab](assets/6_5_dynamicmediaprocessimageassets-thumbnailstab.png)

1. Tap the **[!UICONTROL Process Thumbnails]** step, then tap the **[!UICONTROL Thumbnails]** tab. 必要に応じてサムネールのサイズを変更し、「**[!UICONTROL OK]**」をタップします。

   >[!NOTE]
   >
   >**[!UICONTROL サムネールを処理]**&#x200B;ステップのサムネール因数の値が、**[!UICONTROL Dynamic Media プロセスの画像アセット]**&#x200B;ステップのサムネール因数と一致する必要があります。

1. 「**[!UICONTROL 保存]**」をタップしてワークフローに対する変更を保存します。

### 表示される画像プリセット数の増減 {#increasing-or-decreasing-the-number-of-image-presets-that-display}

作成した画像プリセットは、アセットをプレビューする際の動的レンディションとして使用できます。AEM で、**[!UICONTROL 詳細表示／レンディション]**&#x200B;からアセットを表示すると、様々な動的レンディションが表示されます。表示されるレンディション数の制限を増減させることができます。

**表示する画像プリセットの数を増減するには**

1. Navigate to CRXDE Lite ([https://localhost:4502/crx/de](https://localhost:4502/crx/de)).
1. 次の場所にある画像プリセットリストのノードに移動します。 `/libs/dam/gui/coral/content/commons/sidepanels/imagepresetsdetail/imgagepresetslist`

   ![increase_decreasethenumberofimagepresetsthatdisplay](assets/increase_decreasethenumberofimagepresetsthatdisplay.png)

1. 「**[!UICONTROL limit]**」プロパティで、「**[!UICONTROL Value]**」（デフォルトで 15 に設定されています）を目的の数に変更します。
1. 次の場所で画像プリセットデータソースに移動します。 `/libs/dam/gui/coral/content/commons/sidepanels/imagepresetsdetail/imgagepresetslist/datasource`

   ![chlimage_1-495](assets/chlimage_1-495.png)

1. In the limit property, change the number to the desired number, for example `{empty requestPathInfo.selectors[1] ? "20" : requestPathInfo.selectors[1]}`
1. 「**[!UICONTROL すべて保存]**」をタップします。

### Creating an Image Preset {#creating-image-presets}

画像プリセットの作成によって、プレビューや公開の際に任意の画像に設定を適用できます。

>[!NOTE]
>
>Internet Explorer 9 を使用している場合、プリセットを作成しても、保存後すぐにプリセットのリストに表示されません。この問題を回避するには、IE9 のキャッシュを無効にしてください。

AI、PDF および EPS 形式の取り込みをサポートし、これらのファイル形式の動的レンディションを生成する場合、画像プリセットを作成する前に次の情報を確認することをお勧めします。 [Adobe Illustrator（AI）、Postscript（EPS）および PDF ファイル形式](#adobe-illustrator-ai-postscript-eps-and-pdf-file-formats)を参照してください。

INDD 形式の取り込みをサポートし、これらのファイル形式の動的レンディションを生成する場合、画像プリセットを作成する前に次の情報を確認することをお勧めします。 [InDesign（INDD）ファイル形式](#indesign-indd-file-format)を参照してください。

**画像プリセットを作成するには**

1. In AEM, tap the AEM logo to access the global navigation console, then tap **[!UICONTROL Tools > Assets > Image Presets]**.
1. 「**[!UICONTROL 作成]**」をクリックします。**[!UICONTROL 画像プリセットを編集]**&#x200B;ウィンドウが開きます。

   ![chlimage_1-496](assets/chlimage_1-496.png)

   >[!NOTE]
   >
   >この画像プリセットをレスポンシブにするには、「**[!UICONTROL 幅]**」フィールドと「**[!UICONTROL 高さ]**」フィールドの値を消去して空のままにします。

1. 「**[!UICONTROL 基本]**」タブと「**[!UICONTROL 詳細]**」タブに、名前などの値を適宜入力します。オプションの概要については、[画像プリセットオプション](#image-preset-options)で説明しています。プリセットは左側のウィンドウに表示され、他のアセットと共にその場で使用できます。

   ![6_5_imagepreset-edit](assets/6_5_imagepreset-edit.png)

1. [!UICONTROL **[保存]をクリックします**。

### Creating a responsive Image Preset {#creating-a-responsive-image-preset}

レスポンシブな画像プリセットを作成するには、[画像プリセットの作成](#creating-image-presets)の手順を実行します。**[!UICONTROL 画像プリセットを編集]**&#x200B;ウィンドウで高さと幅を入力する際に、これらの値を消去して空のままにします。

空のままにすることで、この画像プリセットがレスポンシブであることを示します。他の値は適宜変更できます。

>[!NOTE]
>
>To see the **[!UICONTROL URL]** and **[!UICONTROL RESS]** buttons when applying an image preset to an asset, the asset must be published.
>
>![chlimage_1-79](assets/chlimage_1-498.png)
>
>画像プリセットと画像アセットは自動的に公開されます。

### Image Preset options {#image-preset-options}

画像プリセットを作成または編集するときに、ここで説明するオプションを使用できます。またアドビは、最初に使用すべきオプションとして、以下の「ベストプラクティス」のオプションをお勧めします。

* **[!UICONTROL形式** ([基本]**[!UICONTROL タブ]** ) - **** JPEG形式または要件を満たす他の形式を選択します。 すべてのWebブラウザーでJPEG画像形式がサポートされています。小さいファイルサイズと画質のバランスがとれています。 ただし、JPEG形式の画像は非可逆圧縮方式を使用しているので、圧縮設定が低すぎると不要な画像のアーティファクトが発生する可能性があります。 このため、アドビは圧縮品質を 75 に設定することをお勧めします。この設定は、画質と小さなファイルサイズのバランスが取れた設定です。

* **[!UICONTROL シンプルシャープを有効にする]** - 「シンプルシャープを有効にする」を **[!UICONTROL 選択しないでください]** （このシャープフィルタは、アンシャープマスキング設定よりも制御が少なくなります）。

* **[!UICONTROL シャープ：リサンプリングモード]** — バイキ **[!UICONTROL ュービック法を選択しま]**&#x200B;す。

#### 「基本」タブオプション{#basic-tab-options}

<table>
 <tbody>
  <tr>
   <td><strong>フィールド</strong></td>
   <td><strong>説明</strong></td>
  </tr>
  <tr>
   <td><strong>名前</strong></td>
   <td>わかりやすい名前を空白なしで入力します。名前に画像サイズの仕様を含めることで、ユーザーがこの画像プリセットを識別しやすくなります。</td>
  </tr>
  <tr>
   <td><strong>「幅」と「高さ」</strong></td>
   <td>画像が配信されるサイズをピクセル単位で入力します。「幅」と「高さ」は 0 ピクセルより大きい値にする必要があります。いずれかの値が 0 の場合、プリセットは作成されません。両方の値が空の場合、レスポンシブな画像プリセットが作成されます。</td>
  </tr>
  <tr>
   <td><strong>形式</strong></td>
   <td><p>メニューから形式を選択します。</p> <p>「<strong>JPEG</strong>」を選択すると、次の追加オプションを入力できます。</p>
    <ul>
     <li><strong>画質</strong> - JPEG圧縮レベルを制御します。この設定は、ファイルサイズと画質の両方に影響します。JPEG画質のスケールは1 ～ 100です。スライダをドラッグするとスケールが表示されます。</li>
     <li><strong>JPGクロミナンスダウンサンプリングを有効にする</strong> — 目は高周波の輝度よりも高周波の色情報に敏感なので、JPEG画像は画像情報を輝度と色のコンポーネントに分割します。JPEG画像を圧縮すると、輝度成分は最大解像度のままになり、カラー成分はピクセルのグループを平均化してダウンサンプリングされます。ダウンサンプリングは、知覚される品質にほとんど影響を与えずに、データ量を1/2または1/3に削減します。ダウンサンプリングは、グレースケール画像には適用されません。この方法は、コントラストの大きい画像（例えば、テキストがオーバーレイされた画像）に役立つ圧縮量を削減します。</li>
    </ul>
    <div>
      「<strong>GIF</strong>」または「<strong>アルファ付き GIF</strong>」を選択すると、以下の追加の「<strong>GIF カラー量子化</strong>」オプションを入力できます。
    </div>
    <ul>
     <li><strong>タイ </strong>プ — 「アダプ <strong>ティブ</strong> （デフォルト）」、「 <strong>Web</strong>」、「 <strong>Macintosh」を選択します</strong>。アルファ付き <strong>GIFを選択した場合</strong>、Macintoshオプションは使用できません。</li>
     <li><strong>ディザ</strong> - [拡散]ま <strong>たは</strong> [オフ <strong>]を選択</strong>。</li>
     <li><strong>色数</strong> - 2 ～ 256 の値を入力します。</li>
     <li><strong>カラーリスト</strong> - コンマ区切りのリストを入力します。例えば、白、グレーおよび黒の場合は、"000000,888888,ffffff" と入力します。</li>
    </ul>
    <div>
      「<strong>PDF</strong>」、「<strong>TIFF</strong>」または「<strong>アルファ付き TIFF</strong>」を選択すると、以下の追加オプションを入力できます。
    </div>
    <ul>
     <li><strong>圧縮</strong> - 圧縮アルゴリズムを選択します。PDF 用のアルゴリズムオプションは、「<strong>なし</strong>」、「<strong>Zip</strong>」および「<strong>JPEG</strong>」です。TIFF の場合は、「<strong>なし</strong>」、「<strong>LZW</strong>」、「<strong>JPEG</strong>」および「<strong>Zip</strong>」です。アルファ付き TIFF の場合は、「<strong>なし</strong>」、「<strong>LZW</strong>」および「<strong>Zip</strong>」です。</li>
    </ul> <p>「<strong>PNG</strong>」、「<strong>アルファ付き PNG</strong>」または「<strong>EPS</strong>」を選択した場合は、追加オプションはありません。</p> </td>
  </tr>
  <tr>
   <td><strong>シャープニング</strong></td>
   <td>「<strong>シンプルシャープを有効にする</strong>」オプションを選択すると、すべての拡大縮小の実行後、画像に対して基本的なシャープフィルターが適用されます。シャープニングにより、画像を異なるサイズで表示した場合に発生するぼかしを補うことができます。 </td>
  </tr>
 </tbody>
</table>

#### 「詳細」タブオプション{#advanced-tab-options}

<table>
 <tbody>
  <tr>
   <td><strong>フィールド</strong></td>
   <td><strong>説明</strong></td>
  </tr>
  <tr>
   <td><strong>カラースペース</strong></td>
   <td>Select <strong>RGB, CMYK,</strong> or <strong>Grayscale</strong> for the color space.</td>
  </tr>
  <tr>
   <td><strong>カラープロファイル</strong></td>
   <td>作業プロファイルと異なる場合にアセットの変換対象となる出力カラースペースプロファイルを選択します。</td>
  </tr>
  <tr>
   <td><strong>レンダリングインテント</strong></td>
   <td>デフォルトのレンダリングインテントを上書きできます。レンダリングインテントは、対象のカラープロファイルでは再現できない（色域外の）色をどうするかを定義します。レンダリングインテントは、ICC プロファイルと互換性がない場合は無視されます。
    <ul>
     <li>「<strong>知覚的</strong>」は、元の画像の 1 つ以上の色が対象のカラースペースの色域外であるときに、一方のカラースペースの全色域をもう一方のカラースペースの色域に圧縮する場合に選択します。</li>
     <li>Select <strong>Relative Colorimetric</strong> when a color in the current color space is out of gamut in the target color space and you want to map it to the closest possible color within the gamut of the target color space without affecting any other colors. </li>
     <li>Select <strong>Saturation</strong> to reproduce the original image color saturation when converting into the target color space. </li>
     <li>「<strong>絶対的な色域を維持</strong>」は、画像の明るさを変える白点と黒点の調整なしで色を完全に一致させる場合に選択します。</li>
    </ul> </td>
  </tr>
  <tr>
   <td><strong>黒点補正</strong></td>
   <td>出力プロファイルでこの機能がサポートされている場合、このオプションを選択します。指定した ICC プロファイルと互換性がない場合、黒点補正は無視されます。</td>
  </tr>
  <tr>
   <td><strong>ディザリング</strong></td>
   <td>このオプションを選択すると、カラーバンディングアーティファクトを回避または軽減できる可能性があります。 </td>
  </tr>
  <tr>
   <td><strong>シャープニングタイプ</strong></td>
   <td><p>「<strong>なし</strong>」、「<strong>シャープ</strong>」または「<strong>アンシャープマスク</strong>」を選択します。 </p>
    <ul>
     <li>「<strong>なし</strong>」を選択すると、シャープニングが無効になります。</li>
     <li>「<strong>シャープ</strong>」を選択すると、すべての拡大縮小の実行後、画像に対して基本的なシャープフィルターが適用されます。シャープニングにより、画像を異なるサイズで表示した場合に発生するぼかしを補うことができます。 </li>
     <li>Select<strong> Unsharp mask</strong> to fine-tune a sharpening filter effect on the final downsampled image. You can control intensity of effect, radius of the effect (measured in pixels) and a threshold of contrast that will be ignored. This effect uses the same options as Photoshop’s “Unsharp Mask” filter.</li>
    </ul> <p>「<strong>アンシャープマスク</strong>」には次のオプションがあります。</p>
    <ul>
     <li><strong>適用量</strong> — 端のピクセルに適用するコントラストの量を制御します。 デフォルトの実数値は 1.0 です。高解像度の画像に対しては、この値を 5.0 まで増やすことができます。「量」は、フィルター強度の尺度だと考えてください。</li>
     <li><strong>Radius</strong> — シャープに影響する端のピクセルを囲むピクセル数を指定します。 解像度の高い画像では、1～2 の実数を入力します。値が小さい場合、エッジのピクセルのみがシャープされます。値が大きい場合、より広い範囲のピクセルがシャープされます。画像のサイズによって適切な値が変わります。</li>
     <li><strong>しきい値</strong> — アンシャープマスクフィルターを適用した場合に無視するコントラストの範囲を指定します。つまり、このオプションは、端のピクセルと見なされてシャープが適用される前に、シャープを適用したピクセルが周囲の領域とどの程度異なるようになるかを指定します。 ノイズの発生を防ぐには、2 ～ 20の整数値を試してください。 </li>
     <li><strong>適用先</strong> — シャープ解除を各色または明るさに適用するかどうかを指定します。</li>
    </ul>
    <div>
      シャープニングについては、<a href="https://docs.adobe.com/content/help/en/dynamic-media-classic/using/assets/s7_sharpening_images.pdf">画像のシャープニング</a>で説明しています。
    </div> </td>
  </tr>
  <tr>
   <td><strong>再サンプリングモード</strong></td>
   <td>「<strong>再サンプリングモード</strong>」オプションを選択します。画像がダウンサンプリングされる場合に、以下のオプションによって画像がシャープされます。
    <ul>
     <li><strong>バイリニア</strong> — 最も高速な再サンプリング方法。一部のエイリアシングアーチファクトが目立ちます。</li>
     <li><strong>バイキュービック法</strong> - CPU使用量は増えますが、エイリアシングアーチファクトが少ないシャープな画像になります。</li>
     <li><strong>シャープ2</strong> — バイキュービック法よりも多少シャープな結果を生成できますが、CPUコストはさらに高くなります。</li>
     <li><strong>バイシャープ</strong> — 画像サイズを小さくするためのPhotoshopの初期設定のリサンプラーを選択します。これは、Adobe Photoshopで <strong>バイキュービックシャープ</strong> と呼ばれます。</li>
     <li><strong>各カラー</strong>、<strong>明るさ</strong> - 色または明るさに基づいた手法です。デフォルトでは、「<strong>各カラー</strong>」が選択されます。</li>
    </ul> </td>
  </tr>
  <tr>
   <td><strong>プリント解像度</strong></td>
   <td>この画像のプリント用解像度を選択します。デフォルトは 72 ピクセルです。</td>
  </tr>
  <tr>
   <td><strong>画像の修飾子</strong></td>
   <td><p>Beyond the common image settings available in the UI, Dynamic Media supports numerous advanced image modifications that you can specify in the <strong>Image Modifiers</strong> field. These parameters are defined in the <a href="https://marketing.adobe.com/resources/help/en_US/s7/is_ir_api/is_api/http_ref/c_command_reference.html">Image Server Protocol command reference</a>.</p> <p>重要：API にリストされている次の関数はサポートされていません。</p>
    <ul>
     <li>基本的なテンプレートおよびテキストレンダリングコマンド： <code>text= textAngle= textAttr= textFlowPath= textFlowXPath= textPath=</code> と <code>textPs=</code></li>
     <li>ローカリゼーションコマンド： <code>locale=</code> と <code>req=xlate</code></li>
     <li><code>req=set</code> は一般的な使用には使用できません。</li>
     <li><code>req=mbrset</code></li>
     <li><code>req=saveToFile</code></li>
     <li><code>req=targets</code></li>
     <li><code>template=</code></li>
     <li>Dynamic Media のノンコアサービス：SVG、画像レンダリングおよび Web-to-Print</li>
    </ul> </td>
  </tr>
 </tbody>
</table>

### 画像の修飾子による画像プリセットオプションの定義 {#defining-image-preset-options-with-image-modifiers}

「基本」タブと「詳細」タブで使用できるオプションに加えて、画像の修飾子を定義して、画像プリセットの定義でより多くのオプションを指定することができます。画像のレンダリングには Scene7 画像レンダリング API が利用されており、詳しくは [HTTP プロトコルリファレンス](https://microsite.omniture.com/t2/help/en_US/s7/is_ir_api/is_api/http_ref/c_http_protocol_reference.html)で定義されています。

画像の修飾子を使用して実行できることについて、以下に基本的な例を示します。

>[!NOTE]
>
>Some image modifiers [cannot be used in AEM](#advanced-tab-options).

* [op_invert](https://microsite.omniture.com/t2/help/en_US/s7/is_ir_api/is_api/http_ref/r_op_invert.html) — 負の画像効果の各カラーコンポーネントを反転します。

   ```xml
   &op_invert=1
   ```

   ![6_5_imagepreset-edit-invert](assets/6_5_imagepreset-edit-invert.png)

* [op_blur](https://microsite.omniture.com/t2/help/en_US/s7/is_ir_api/is_api/http_ref/r_op_blur.html) - 画像にぼかしフィルターを適用します。

   ```xml
   &op_blur=7
   ```

   ![6_5_imagepreset-edit-blur](assets/6_5_imagepreset-edit-blur.png)

* コマンドの組み合わせ - op_blur と op-invert

   ```xml
   &op_invert=1&op_blur=7
   ```

   ![chlimage_1-80](assets/chlimage_1-501.png)

* [op_brightness](https://microsite.omniture.com/t2/help/en_US/s7/is_ir_api/is_api/http_ref/r_op_brightness.html) — 明るさを増減します。

   ```xml
   &op_brightness=58
   ```

   ![6_5_imagepreset-edit-brightness](assets/6_5_imagepreset-edit-brightness.png)

* [opac](https://microsite.omniture.com/t2/help/en_US/s7/is_ir_api/is_api/http_ref/r_opac.html) - 画像の不透明度を調節します。前景の不透明度を減らすことができます。

   ```xml
   opac=29
   ```

   ![6_5_imagepreset-edit-opacity](assets/6_5_imagepreset-edit-opacity.png)

### 画像プリセットの編集 {#modifying-image-presets}

1. In AEM, tap the AEM logo to access the global navigation console, then tap **[!UICONTROL Tools > Assets > Image Presets]**.

   ![6_5_imagepreset-editpreset](assets/6_5_imagepreset-editpreset.png)

1. Select a preset and then click **[!UICONTROL Edit]**. The **[!UICONTROL Edit Image Preset]** window opens.
1. 変更を加え、「**[!UICONTROL 保存]**」をクリックして変更を保存するか、「**[!UICONTROL キャンセル]**」をクリックして変更をキャンセルします。

### 画像プリセットの公開 {#publishing-image-presets}

画像プリセットは自動的に公開されます。

### 画像プリセットの削除 {#deleting-image-presets}

1. In AEM, tap the AEM logo to access the global navigation console and tap or click the Tools icon and navigate to **[!UICONTROL Assets > Image Presets]**.
1. Select a preset, and then click **[!UICONTROL Delete**. プリセットを削除してよいか確認するメッセージが表示されます。Tap **[!UICONTROL Delete]** to delete or tap **[!UICONTROL Cancel]** to abort.
