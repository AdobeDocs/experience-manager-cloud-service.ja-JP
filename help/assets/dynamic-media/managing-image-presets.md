---
title: '画像プリセットの管理 '
description: 「画像プリセットの概要と、画像プリセットの作成、変更および管理方法について説明します。」
feature: 画像プリセット，ビューア，レンディション
role: Business Practitioner
exl-id: a53f40ab-0e27-45f8-9142-781c077a04cc
source-git-commit: d3ee23917eba4a2e4ae1f2bd44f5476d2ff7dce1
workflow-type: tm+mt
source-wordcount: '3653'
ht-degree: 69%

---

# 画像プリセットの管理 {#managing-image-presets}

画像プリセットを使用すると、Adobe Experience Manager Assetsは異なるサイズの画像、異なる形式の画像、または動的に生成された他の画像プロパティを使用して動的に画像を配信できます。 各画像プリセットは、画像表示用のサイズやフォーマットに関するコマンドの事前定義済みコレクションを表します。画像プリセットの作成時には、画像配信用のサイズを選択します。またフォーマットコマンドも選択し、表示対象画像の配信時に画像の見た目が最適化されるようにします。

管理者は、アセットを書き出すためのプリセットを作成できます。ユーザーは、画像を書き出す際にプリセットを選択でき、管理者が指定した仕様に合わせて画像を再フォーマットできます。

レスポンシブな画像プリセットを作成することもできます。レスポンシブな画像プリセットをアセットに適用すると、アセットが表示されるデバイスや画面サイズに応じて変わります。 画像プリセットは、RGB またはグレーに加えて CMYK をカラースペースで使用するよう設定できます。

ここでは、画像プリセットを作成、変更および全般的に管理する方法について説明します。作成者は画像をプレビューするときに、いつでも画像プリセットを適用できます。詳しくは、[画像プリセットの適用](/help/assets/dynamic-media/image-presets.md)を参照してください。

>[!NOTE]
>
>スマートイメージングは、既存の画像プリセットで機能し、配信の直前にインテリジェンスを使用して、ブラウザーまたはネットワークの接続速度に基づいて画像のファイルサイズをさらに低減します。詳しくは、[スマートイメージング](/help/assets/dynamic-media/imaging-faq.md)を参照してください。

## 画像プリセットの概要 {#understanding-image-presets}

各画像プリセットはマクロと同様に、サイズおよびフォーマットのコマンドに関する事前定義済みのコレクションが、特定の名前で保存されたものです。画像プリセットの動作を理解するには、Webサイトで、デスクトップとモバイルの配信用に、各製品画像を異なるサイズ、異なる形式、圧縮率で表示する必要があるとします。

デスクトップバージョン（500 x 500 ピクセル）とモバイルバージョン（150 x 150 ピクセル）の 2 つの画像プリセットを作成できます。2 つの画像プリセットを作成します。つまり、500 x 500 ピクセルで画像を表示するための `Enlarge` プリセットとで、150 x 150 ピクセルで画像を表示するための `Thumbnail` プリセットです。`Enlarge`サイズと`Thumbnail`サイズの画像を配信するために、Experience Managerは「拡大画像プリセット」と「サムネール画像プリセット」の定義を探します。 次に、Experience Managerは、各画像プリセットのサイズと形式の仕様に従って画像を動的に生成します。

この場合、動的に配信されるときに画像のサイズを削減すると、シャープさと細部の表現が失われる可能性があります。この理由で、各画像プリセットには、画像を特定のサイズで配信するときに最適化するためのフォーマット用のコントロールが含まれています。これらのコントロールによって、Web サイトまたはアプリケーションに画像が配信されるときに、画像がシャープでクリアに表示されるようになります。

管理者が画像プリセットを作成できます。画像プリセットを作成する際に、最初から作業を始めることも、既存のプリセットから始めて新しい名前で保存することもできます。

## 画像プリセットの管理 {#managing-image-presets-1}

Experience ManagerでExperience Managerプリセットを管理するには、画像のロゴをタップまたはクリックしてグローバルナビゲーションコンソールにアクセスし、ツールアイコンをタップまたはクリックして&#x200B;**[!UICONTROL アセット]**/**[!UICONTROL 画像プリセット]**&#x200B;の順に移動します。

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
>アセットの詳細表示で「**[!UICONTROL レンディション]**」を選択すると、様々なレンディションが表示されます。 表示される画像プリセットの数を増減させることができます。[表示される画像プリセット数の引き上げ](#increasing-or-decreasing-the-number-of-image-presets-that-display)を参照してください。

### Adobe Illustrator(AI)、PostScript®(EPS)およびPDFファイル形式{#adobe-illustrator-ai-postscript-eps-and-pdf-file-formats}

AI、EPSおよびPDFファイルの取り込みをサポートし、これらのファイル形式の動的レンディションを生成する場合は、画像プリセットを作成する前に次の情報を確認してください。

Adobe Illustrator のファイル形式は PDF のバリアントです。Experience Managerアセットの主な違いは次のとおりです。

* Adobe Illustrator のドキュメントは複数のレイヤーを持つ単一のページで構成されます。各レイヤーは、メインのIllustratorアセットの下にPNGサブアセットとして抽出されます。
* PDF のドキュメントは 1 つ以上のページで構成されます。各ページは、メインの複数ページのPDFドキュメントの下に単一ページのPDFサブアセットとして抽出されます。

サブアセットは、`DAM Update Asset`ワークフロー全体で`Create Sub Asset process`コンポーネントによって作成されます。 ワークフローにこのプロセスコンポーネントを表示するには、**[!UICONTROL ツール]**／**[!UICONTROL ワークフロー]**／**[!UICONTROL モデル]**／**[!UICONTROL DAM アセットの更新]**／**[!UICONTROL 編集]**&#x200B;をタップします。

<!-- See also [Viewing pages of a multi-page file](/help/assets/manage-linked-subassets.md#view-pages-of-a-multi-page-file). -->

アセットを開き、コンテンツメニューをタップして、「**[!UICONTROL サブアセット]**」または「**[!UICONTROL ページ]**」を選択すると、サブアセットまたはページを表示できます。 サブアセットは実際のアセットです。 つまり、PDF ページは `Create Sub Asset` ワークフローコンポーネントによって抽出されます。その後、メインアセットの下に`page1.pdf`、`page2.pdf`などとして保存されます。 保存後、それらは `DAM Update Asset` ワークフローで処理されます。

  Dynamic Media を使用して AI、EPS または PDF ファイルの動的レンディションを表示および生成するには、次の処理ステップが必要です。

1. `DAM Update Asset` ワークフローで、`Rasterize PDF/AI Image Preview Rendition` プロセスコンポーネントが、（設定された解像度で）元のアセットの最初のページを `cqdam.preview.png` レンディションにラスタライズします。

1. その後、ワークフロー内の `Dynamic Media Process Image Assets` プロセスコンポーネントで、`cqdam.preview.png` レンディションが PTIFF に最適化されます。

>[!NOTE]
>
>DAM アセットの更新ワークフローでは、**[!UICONTROL EPS サムネール]**&#x200B;のステップで EPS ファイルのサムネールが生成されます。

#### PDF/AI/EPS アセットのメタデータプロパティ  {#pdf-ai-eps-asset-metadata-properties}

| **メタデータプロパティ** | **説明** |
|---|---|
| dam:Physicalwidthininches | ドキュメントの幅（インチ単位） |
| dam:Physicalheightininches | ドキュメントの高さ（インチ単位） |

`Rasterize PDF/AI Image Preview Rendition` プロセスコンポーネントのオプションには、`DAM Update Asset` ワークフローを通じてアクセスします。

左上のAdobe Experience Managerをタップし、**[!UICONTROL ツール]** / **[!UICONTROL ワークフロー]** / **[!UICONTROL モデル]**&#x200B;に移動します。 ワークフローモデルページで「**[!UICONTROL DAM アセットの更新]**」を選択し、ツールバーの「**[!UICONTROL 編集]**」をタップします。DAM アセットの更新ワークフローページで、`Rasterize PDF/AI Image Preview Rendition` プロセスコンポーネントをダブルタップして、ステップのプロパティダイアログボックスを開きます。

#### PDF/AI 画像プレビューレンディションをラスタライズのオプション {#rasterize-pdf-ai-image-preview-rendition-options}

![PDF または AI ワークフローのラスタライズの引数](assets/rasterize_pdf_ai_image_preview.png)

PDF または AI ワークフローのラスタライズの引数

| プロセス引数 | デフォルト設定 | 説明 |
|---|---|---|
| MIME タイプ | application/pdf<br>application/<br>postscriptapplication/illustrator | PDF または Illustrator のドキュメントと見なされるドキュメントの MIME タイプのリスト。 |
| 最大の幅 | 2048 | 生成されたプレビューレンディションの最大の幅（ピクセル単位）。 |
| 最大の高さ | 2048年 | 生成されたプレビューレンディションの最大の高さ（ピクセル単位）。 |
| 解像度 | 72 | 最初のページをラスタライズする解像度（ppi（インチあたりピクセル数）単位） |

デフォルトのプロセス引数を使用して、PDF/AI ドキュメントの最初のページが 72 ppi でラスタライズされ、生成されたプレビュー画像のサイズは 2048 x 2048 ピクセルになります。通常のデプロイメントでは、解像度を150 ppi以上に増やすことができます。 例えば、300 ppi の US Letter サイズのドキュメントの幅と高さにはそれぞれ最大で 2550 x 3300 ピクセルが必要です。

  ラスタライズする解像度を制限する最大の幅と最大の高さ。例えば、最大値が変更されず、解像度が 300 ppi に設定された場合、US Letter のドキュメントは 186 ppi でラスタライズされます。つまり、ドキュメントは 1581 x 2046 ピクセルになります。

`Rasterize PDF/AI Image Preview Rendition` プロセスコンポーネントには、メモリに過度に大きな画像が作成されないように、最大値が定義されています。このような大きな画像は、JVM(Java™仮想マシン)に提供されるメモリをオーバーフローする可能性があります。 それぞれ設定された最大サイズで画像を作成可能なワークフローを、設定した数だけ並行して管理するのに十分なメモリを JVM に提供する必要があります。

### InDesign（INDD）ファイル形式  {#indesign-indd-file-format}

INDDファイルの取り込みをサポートし、このファイル形式の動的レンディションを生成する場合は、画像プリセットを作成する前に次の情報を確認してください。

InDesignファイルの場合、Adobe InDesign ServerがAdobe Assetsと統合されている場合にのみ、サブExperience Managerが抽出されます。 参照元のアセットは、メタデータに基づいてリンクされます。リンク設定に InDesign サーバーは不要です。ただし、InDesignファイルと参照元のInDesignの間にリンクが作成されるには、参照元のアセットがExperience Manager内に存在してから、アセットファイルを処理する必要があります。

<!-- See [Integrating Experience Manager Assets with InDesign Server](/help/assets/indesign.md). -->

`DAM Update Asset` ワークフローのメディア抽出プロセスコンポーネントでは、事前設定された「スクリプトを拡張」をいくつか実行して InDesign ファイルを処理します。

![メディア抽出プロセスの引数で使用される ExtendScript のパス](/help/assets/dynamic-media/assets/6_5_mediaextractionprocess.png)

DAM アセットの更新ワークフローのメディア抽出プロセスコンポーネントの引数で使用される ExtendScript のパス

Dynamic Media 統合では、以下のスクリプトが使用されます。


| ExtendScript名 | デフォルト | 説明 |
|---|---|---|
| ThumbnailExport.jsx | はい | `thumbnail.jpg` プロセスコンポーネントによって最適化され PTIFF レンディションに変換される 300 ppi の `Dynamic Media Process Image Assets` レンディションを生成します。 |
| JPEGPagesExport.jsx | はい | 各ページに300 ppiのJPEGサブアセットを生成します。 JPEGサブアセットは、アセットアセットの下に保存される実際のInDesignです。 また、`DAM Update Asset` ワークフローで最適化され PTIFF に変換されます。 |
| PDFPagesExport.jsx | いいえ | 各ページに対してPDFサブアセットを生成します。 PDFサブアセットは、前述のように処理されます。 PDFには単一のページのみが含まれるので、サブアセットは生成されません。 |

### 画像のサムネールサイズの設定 {#configuring-image-thumbnail-size}

**[!UICONTROL DAM アセットの更新]**&#x200B;ワークフローで設定することにより、サムネールのサイズを設定できます。画像アセットのサムネールサイズの設定にはワークフローで 2 つのステップがあります。1つ(**[!UICONTROL Dynamic Mediaプロセスの画像アセット]**)が、動的画像アセットに使用されます。 静的なサムネールの生成には、他の（**[!UICONTROL プロセスのサムネール]**）が使用されます。その他のすべてのプロセスでサムネールの生成に失敗した場合も同様です。 *両方*&#x200B;の設定は同じにする必要があります。

**[!UICONTROL Dynamic Media プロセスの画像アセット]**&#x200B;のステップでは、サムネールは Image Server で生成されます。この設定は、**[!UICONTROL サムネールを処理]**&#x200B;のステップで適用される設定とは独立した設定です。**[!UICONTROL サムネールを処理]**&#x200B;のステップでおこなうサムネールの生成は、サムネール生成で最も遅く、最もメモリを使う方法です。

サムネールのサイズは次のフォーマットで定義されます。**[!UICONTROL width:height:center]**。例えば *80:80:false* となります。幅と高さによって、サムネールのサイズがピクセル単位で決まります。中心の値はfalseまたはtrueです。trueに設定した場合は、サムネール画像のサイズが設定で指定したサイズと完全に同じであることを示します。 画像のサイズが小さい場合は、サムネール内で中央揃えされます。

>[!NOTE]
>
>* EPSファイルのサムネールサイズは、「サムネール」の下の「**[!UICONTROL 引数]**」タブの「**[!UICONTROL EPSサムネール]**」ステップで設定します。
   >
   >
* ビデオのサムネールサイズは、**[!UICONTROL 引数]**&#x200B;の下の&#x200B;**[!UICONTROL 「プロセス]**」タブの&#x200B;**[!UICONTROL FFmpegサムネール]**&#x200B;の手順で設定します。

>



**画像のサムネールサイズを設定するには**：

1. **[!UICONTROL ツール]** / **[!UICONTROL ワークフロー]** / **[!UICONTROL モデル]** / **[!UICONTROL DAMアセットの更新]** / **[!UICONTROL 編集]**&#x200B;をタップします。
1. **[!UICONTROL Dynamic Media プロセスの画像アセット]**&#x200B;のステップをタップし、「**[!UICONTROL サムネール]**」タブをタップします。必要に応じてサムネールのサイズを変更し、「**[!UICONTROL OK]**」をタップします。

   ![6_5_dynamicmediaprocessimageassets-thumbnailstab](assets/6_5_dynamicmediaprocessimageassets-thumbnailstab.png)

1. **[!UICONTROL サムネールを処理]**&#x200B;のステップをタップし、「**[!UICONTROL サムネール]**」タブをタップします。必要に応じてサムネールのサイズを変更し、「**[!UICONTROL OK]**」をタップします。

   >[!NOTE]
   >
   >**[!UICONTROL サムネールを処理]**&#x200B;ステップのサムネール引数の値が、**[!UICONTROL Dynamic Media プロセスの画像アセット]**&#x200B;ステップのサムネール引数と一致する必要があります。

1. 「**[!UICONTROL 保存]**」をタップしてワークフローに対する変更を保存します。

### 表示される画像プリセット数の増減  {#increasing-or-decreasing-the-number-of-image-presets-that-display}

作成した画像プリセットは、アセットをプレビューする際の動的レンディションとして使用できます。Experience Managerは、**[!UICONTROL 詳細表示/レンディション]**&#x200B;からアセットを表示すると、様々な動的レンディションを表示します。 表示されるレンディション数の制限を増減させることができます。

**表示される画像プリセット数を増減させるには**：:

1. CRXDE Lite（[https://localhost:4502/crx/de](https://localhost:4502/crx/de)）に移動します。
1. 画像プリセットリストノード（`/libs/dam/gui/coral/content/commons/sidepanels/imagepresetsdetail/imgagepresetslist`）に移動します。

   ![increase_decreasethenumberofimagepresetsthatdisplay](assets/increase_decreasethenumberofimagepresetsthatdisplay.png)

1. 「**[!UICONTROL limit]**」プロパティで、「**[!UICONTROL 値]**」（デフォルトで 15 に設定されています）を目的の数に変更します。
1. 画像プリセットデータソース（`/libs/dam/gui/coral/content/commons/sidepanels/imagepresetsdetail/imgagepresetslist/datasource`）に移動します。

   ![chlimage_1-495](assets/chlimage_1-495.png)

1. 「limit」プロパティの数を、目的の数（例：`{empty requestPathInfo.selectors[1] ? "20" : requestPathInfo.selectors[1]}`）に変更します。
1. 「**[!UICONTROL すべて保存]**」をタップします。

### 画像プリセットの作成 {#creating-image-presets}

画像プリセットの作成によって、プレビューや公開の際に任意の画像に設定を適用できます。

>[!NOTE]
>
>Internet Explorer 9 を使用している場合、プリセットを作成しても、保存後すぐにプリセットのリストに表示されません。この問題を回避するには、IE9 のキャッシュを無効にしてください。

AI、PDFおよびEPSファイルの取り込みをサポートし、これらのファイル形式の動的レンディションを生成する場合は、画像プリセットを作成する前に次の情報を確認してください。

[Adobe Illustrator(AI)、PostScript®(EPS)、PDFファイル形式](#adobe-illustrator-ai-postscript-eps-and-pdf-file-formats)を参照してください。

INDDファイルの取り込みをサポートし、このファイル形式の動的レンディションを生成する場合は、画像プリセットを作成する前に次の情報を確認してください。

[InDesign（INDD）ファイル形式](#indesign-indd-file-format)を参照してください。

**画像プリセットを作成するには**：:

1. Experience Managerで、Experience Managerのロゴをタップしてグローバルナビゲーションコンソールにアクセスし、**[!UICONTROL ツール]** / **[!UICONTROL アセット]** / **[!UICONTROL 画像プリセット]**&#x200B;をタップします。
1. 「**[!UICONTROL 作成]**」をクリックします。**[!UICONTROL 画像プリセットを編集]**&#x200B;ウィンドウが開きます。

   ![chlimage_1-496](assets/chlimage_1-496.png)

   >[!NOTE]
   >
   >この画像プリセットをレスポンシブにするには、「**[!UICONTROL 幅]**」フィールドと「**[!UICONTROL 高さ]**」フィールドの値を消去して空のままにします。

1. 「**[!UICONTROL 基本]**」タブと「**[!UICONTROL 詳細]**」タブに、名前などの値を適宜入力します。オプションの概要については、[画像プリセットオプション](#image-preset-options)で説明しています。プリセットは左側のウィンドウに表示され、他のアセットにすぐに使用できます。

   ![6_5_imagepreset-edit](assets/6_5_imagepreset-edit.png)

1. 「**[!UICONTROL 保存]**」をクリックします。

### レスポンシブな画像プリセットの作成 {#creating-a-responsive-image-preset}

レスポンシブな画像プリセットを作成するには、[画像プリセットの作成](#creating-image-presets)の手順を実行します。**[!UICONTROL 画像プリセットを編集]**&#x200B;ウィンドウで高さと幅を入力する際に、これらの値を消去して空のままにします。

空のままにすると、Experience Managerに、この画像プリセットがレスポンシブであることが示されます。 他の値は適宜変更できます。

>[!NOTE]
>
>画像プリセットをアセットに適用するときに「**[!UICONTROL URL]**」ボタンと「**[!UICONTROL RESS]**」ボタンを表示するには、アセットを公開する必要があります。
>
>![chlimage_1-79](assets/chlimage_1-498.png)
>
>画像プリセットと画像アセットは自動的に公開されます。

### 画像プリセットオプション {#image-preset-options}

画像プリセットを作成または編集するときに、ここで説明するオプションを使用できます。またアドビは、最初に使用すべきオプションとして、以下の「ベストプラクティス」のオプションをお勧めします。

* **[!UICONTROL 形式]**（「**[!UICONTROL 基本]**」タブ） - 「**[!UICONTROL JPEG]**」または要件を満たす他の形式を選択します。JPEG 画像形式はすべての Web ブラウザーでサポートされ、小さなファイルサイズと画質のバランスが良い形式です。ただし、JPEG 形式の画像では非可逆圧縮方式が使用されるので、圧縮設定が低すぎる場合は望ましくない画像アーティファクトが発生する可能性があります。このため、アドビは圧縮品質を 75 に設定することをお勧めします。この設定は、画質と小さなファイルサイズのバランスが取れた設定です。

* **[!UICONTROL シンプルシャープを有効にする]** - 「**[!UICONTROL シンプルシャープを有効にする]**」は選択しません（このシャープフィルターでは、アンシャープマスク設定よりも細かく制御できません）。

* **[!UICONTROL シャープ：再サンプリングモード]** - 「**[!UICONTROL バイキュービック法]**」を選択します。

#### 「基本」タブオプション {#basic-tab-options}

<table>
 <tbody>
  <tr>
   <td><strong>フィールド</strong></td>
   <td><strong>説明</strong></td>
  </tr>
  <tr>
   <td><strong>名前</strong></td>
   <td>わかりやすい名前を空白なしで入力します。ユーザーがこの画像プリセットを特定しやすくするために、名前に画像サイズの仕様を含めます。</td>
  </tr>
  <tr>
   <td><strong>「幅」と「高さ」</strong></td>
   <td>画像が配信されるサイズをピクセル単位で入力します。「幅」と「高さ」は 0 ピクセルより大きい値にする必要があります。いずれかの値が 0 の場合、プリセットは作成されません。両方の値が空の場合、レスポンシブな画像プリセットが作成されます。</td>
  </tr>
  <tr>
   <td><strong>形式</strong></td>
   <td><p>メニューから形式を選択します。</p> <p>「<strong>JPEG</strong>」を選択すると、次の他のオプションを選択できます。</p>
    <ul>
     <li><strong>画質</strong> - JPEG 圧縮レベルを制御します。この設定は、ファイルサイズと画質の両方に影響します。JPEG 画質の尺度は 1～100 です。スライダーをドラッグすると、この尺度が表示されます。</li>
     <li><strong>JPG クロミナンスダウンサンプリングを有効にする</strong> - 目は高周波の色情報よりも高周波の輝度に対して敏感であるので、JPEG 画像は画像情報を輝度成分と色の成分に分けています。JPEG 画像が圧縮されると、輝度成分はフル解像度のまま、色成分がピクセルのグループでまとめて平均化されることでダウンサンプリングされます。ダウンサンプリングによって、知覚される画質にはほぼ影響を与えることなく、データ量を半分から 3 分の 1 程度削減できます。ダウンサンプリングは、グレースケールの画像には適用されません。この技術によって圧縮量が削減されます。これは、高コントラストの画像（オーバーレイされたテキストを含む画像など）で役立ちます。</li>
    </ul>
    <div>
      「<strong>GIF</strong>」または「<strong>アルファ付き GIF</strong>」を選択すると、以下の追加の「<strong>GIF カラー量子化</strong>」オプションを入力できます。
    </div>
    <ul>
     <li><strong>タイプ</strong> - 「<strong>アダプティブ</strong>」（デフォルト）、「<strong>Web</strong>」、「<strong>Macintosh</strong>」のいずれかを選択します。「<strong>アルファ付き GIF</strong>」を選択した場合は、「Macintosh」オプションは選択できません。</li>
     <li><strong>ディザ</strong> - 「<strong>拡散</strong>」または「<strong>オフ</strong>」を選択します。</li>
     <li><strong>色数 —  </strong>2 ～ 256の値を入力します。</li>
     <li><strong>カラーリスト</strong> - コンマ区切りのリストを入力します。例えば、白、グレーおよび黒の場合は、"000000,888888,ffffff" と入力します。</li>
    </ul>
    <div>
      「<strong>PDF</strong>」、「<strong>TIFF</strong>」または「<strong>アルファ付き TIFF</strong>」を選択すると、以下の追加オプションを入力できます。
    </div>
    <ul>
     <li><strong>圧縮</strong> - 圧縮アルゴリズムを選択します。PDFのアルゴリズムオプションは<strong>なし</strong>、<strong>Zip</strong>、<strong>Jpeg</strong>です。TIFFの場合は、<strong>なし</strong>、<strong>LZW</strong>、<strong>Jpeg</strong>、<strong>Zip</strong>です。アルファ付きTIFFの場合、<strong>なし</strong>、<strong>LZW</strong>、<strong>Zip</strong>です。</li>
    </ul> <p>「<strong>PNG</strong>」、「<strong>アルファ付き PNG</strong>」または「<strong>EPS</strong>」を選択した場合は、追加オプションはありません。</p> </td>
  </tr>
  <tr>
   <td><strong>シャープ</strong></td>
   <td>「<strong>シンプルシャープを有効にする</strong>」オプションを選択すると、すべての拡大縮小の実行後、画像に対して基本的なシャープフィルターが適用されます。シャープにより、画像を異なるサイズで表示した場合に発生するぼかしを補うことができます。 </td>
  </tr>
 </tbody>
</table>

#### 「詳細」タブオプション {#advanced-tab-options}

<table>
 <tbody>
  <tr>
   <td><strong>フィールド</strong></td>
   <td><strong>説明</strong></td>
  </tr>
  <tr>
   <td><strong>カラースペース</strong></td>
   <td>カラースペースとして、「<strong>RGB」、「CMYK</strong>」または「<strong>グレースケール</strong>」を選択します。</td>
  </tr>
  <tr>
   <td><strong>カラープロファイル</strong></td>
   <td>作業プロファイルと異なる場合にアセットの変換先となる出力カラースペースプロファイルを選択します。</td>
  </tr>
  <tr>
   <td><strong>レンダリングインテント</strong></td>
   <td>デフォルトのレンダリングインテントを上書きできます。レンダリングインテントは、対象のカラープロファイルでは再現できない（色域外の）色をどうするかを定義します。レンダリングインテントは、ICC プロファイルと互換性がない場合は無視されます。
    <ul>
     <li>「<strong>知覚的</strong>」は、元の画像の 1 つ以上の色が対象のカラースペースの色域外であるときに、一方のカラースペースの全色域をもう一方のカラースペースの色域に圧縮する場合に選択します。</li>
     <li>現在のカラースペースの色がターゲットカラースペースの色域外の場合は、「<strong>相対的な色域を維持</strong>」を選択します。また、他の色に影響を与えることなく、ターゲットカラースペースの色域内で可能な限り近い色にマッピングする必要があります。 </li>
     <li>対象のカラースペースに変換する際に元の画像の色の彩度を再現する場合は、「<strong>彩度</strong>」を選択します。 </li>
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
   <td><strong>シャープタイプ</strong></td>
   <td><p>「<strong>なし</strong>」、「<strong>シャープ</strong>」または「<strong>アンシャープマスク</strong>」を選択します。 </p>
    <ul>
     <li>シャープを無効にする場合は、「<strong>なし</strong>」を選択します。</li>
     <li>「<strong>シャープ</strong>」を選択すると、すべての拡大縮小の実行後、画像に対して基本的なシャープフィルターが適用されます。シャープにより、画像を異なるサイズで表示した場合に発生するぼかしを補うことができます。 </li>
     <li>ダウンサンプリングされた最終的な画像に対するシャープフィルター効果を微調整する場合は、「<strong>アンシャープマスク</strong>」を選択します。 効果の強さ、効果の半径（ピクセル単位）、無視されるコントラストのしきい値を制御できます。 この効果では、Photoshop の「アンシャープマスク」フィルターと同じオプションが使用されます。</li>
    </ul> <p>「<strong>アンシャープマスク</strong>」には次のオプションがあります。</p>
    <ul>
     <li><strong>量</strong> - 端のピクセルに適用されるコントラストを制御します。デフォルトの実数値は 1.0 です。高解像度の画像に対しては、この値を 5.0 まで増やすことができます。「量」は、フィルター強度の尺度だと考えてください。</li>
     <li><strong>半径</strong> - シャープに影響するエッジピクセルの周囲のピクセル数を決定します。解像度の高い画像では、1～2 の実数を入力します。値が小さい場合、エッジのピクセルのみがシャープニングされます。値が大きい場合、より広い範囲のピクセルがシャープニングされます。画像のサイズによって適切な値が変わります。</li>
     <li><strong>しきい値</strong> - アンシャープマスクフィルターが適用される場合のコントラストの範囲を指定します。つまり、このオプションは、シャープニングされるピクセルが周囲の領域とどの程度違えば、そのピクセルをエッジのピクセルと見なしてシャープニングするかを決定するものです。ノイズが入り込まないように、2 ～ 20の整数値を試してみてください。 </li>
     <li><strong>適用先</strong> - アンシャープを各カラーまたは明るさに適用するかを指定します。</li>
    </ul>
    <div>
      シャープニングについては、
     <a href="https://experienceleague.adobe.com/docs/experience-manager-learn/assets/dynamic-media/dynamic-media-image-sharpening-feature-video-use.html#dynamic-media">Experience ManagerDynamic Media</a>ビデオ、<a href="https://experienceleague.adobe.com/docs/dynamic-media-classic/using/master-files/sharpening-image.html#master-files">画像のシャープ</a>オンラインヘルプトピック、および<a href="https://experienceleague.adobe.com/docs/dynamic-media-classic/assets/s7_sharpening_images.pdf">Dynamic Media Classic</a>ダウンロード可能なPDFで画像をシャープにするためのベストプラクティスです。
    </div> </td>
  </tr>
  <tr>
   <td><strong>再サンプリングモード</strong></td>
   <td>「<strong>再サンプリングモード</strong>」オプションを選択します。画像がダウンサンプリングされる場合に、以下のオプションによって画像がシャープニングされます。
    <ul>
     <li><strong>バイリニア法</strong> - 最速の再サンプリング方法。目に見えるエイリアスアーティファクトが一部発生します。</li>
     <li><strong>バイキュービック法</strong> - CPU 使用率は上昇しますが、目に見えるエイリアスアーティファクトが減少した、よりシャープな画像が生成されます。</li>
     <li><strong>シャープ 2</strong> - バイキュービック法よりも少しシャープな画像を生成できますが、CPU コストはさらに大きくなります。</li>
     <li><strong>バイシャープ</strong> - 画像サイズを縮小するための Photoshop のデフォルトの再サンプリング方法を選択します。Adobe Photoshop では「<strong>バイキュービックシャーパー</strong>」と呼ばれています。</li>
     <li><strong>各カラー</strong>、<strong>明るさ</strong> - 色または明るさに基づいた手法です。デフォルトでは、「<strong>各カラー</strong>」が選択されます。</li>
    </ul> </td>
  </tr>
  <tr>
   <td><strong>プリント解像度</strong></td>
   <td>この画像のプリント用解像度を選択します。デフォルトは 72 ピクセルです。</td>
  </tr>
  <tr>
   <td><strong>画像の修飾子</strong></td>
   <td><p>UI で使用できる共通の画像設定のほか、Dynamic Media では「<strong>画像の修飾子</strong>」フィールドで画像の詳細を多数指定できます。これらのパラメーターは、<a href="https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/http-protocol-reference/syntax-and-features/image-serving-http/c-command-overview.html?lang=ja">Image Server プロトコルのコマンドリファレンス（英語）</a>で定義されています。</p> <p>重要：API にリストされている次の関数はサポートされていません。</p>
    <ul>
     <li>基本的なテンプレートコマンドおよびテキストレンダリングコマンド：<code>text= textAngle= textAttr= textFlowPath= textFlowXPath= textPath=</code> および <code>textPs=</code></li>
     <li>ローカライゼーションコマンド：<code>locale=</code> および <code>req=xlate</code></li>
     <li><code>req=set</code> は汎用的には使用できません。</li>
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

「基本」タブと「詳細」タブで使用できるオプションに加えて、画像の修飾子を定義して、画像プリセットの定義でより多くのオプションを指定することができます。画像のレンダリングはDynamic Media Image Rendering APIに依存し、 [HTTPプロトコルリファレンス](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-rendering-api/http-protocol-reference/c-ir-introduction.html?lang=ja#image-rendering-api)で詳しく定義されます。

画像の修飾子を使用して実行できることについて、以下に基本的な例を示します。

>[!NOTE]
>
>一部の画像修飾子[はExperience Manager](#advanced-tab-options)では使用できません。

* [op_invert](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/http-protocol-reference/command-reference/r-op-invert.html?lang=ja) - それぞれの色成分を、画像の効果が反対になるように逆転させます。

   ```xml
   &op_invert=1
   ```

   ![6_5_imagepreset-edit-invert](assets/6_5_imagepreset-edit-invert.png)

* [op_blur](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/http-protocol-reference/command-reference/r-op-blur.html?lang=ja) - 画像にぼかしフィルターを適用します。

   ```xml
   &op_blur=7
   ```

   ![6_5_imagepreset-edit-blur](assets/6_5_imagepreset-edit-blur.png)

* コマンドの組み合わせ - op_blur と op-invert

   ```xml
   &op_invert=1&op_blur=7
   ```

   ![chlimage_1-80](assets/chlimage_1-501.png)

* [op_brightness](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/http-protocol-reference/command-reference/r-op-brightness.html?lang=ja) - 明るさを増減させます。

   ```xml
   &op_brightness=58
   ```

   ![6_5_imagepreset-edit-brightness](assets/6_5_imagepreset-edit-brightness.png)

* [opac](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/http-protocol-reference/command-reference/r-opac.html?lang=ja) - 画像の不透明度を調節します。前景の不透明度を減らすことができます。

   ```xml
   opac=29
   ```

   ![6_5_imagepreset-edit-opacity](assets/6_5_imagepreset-edit-opacity.png)

### 画像プリセットの編集 {#modifying-image-presets}

1. Experience Managerで、Experience Managerのロゴをタップしてグローバルナビゲーションコンソールにアクセスし、**[!UICONTROL ツール]** / **[!UICONTROL アセット]** / **[!UICONTROL 画像プリセット]**&#x200B;をタップします。

   ![6_5_imagepreset-editpreset](assets/6_5_imagepreset-editpreset.png)

1. プリセットを選択し、「**[!UICONTROL 編集]**」をクリックします。**[!UICONTROL 画像プリセットを編集]**&#x200B;ウィンドウが開きます。
1. 変更を加え、「**[!UICONTROL 保存]**」をクリックして変更を保存するか、「**[!UICONTROL キャンセル]**」をクリックして変更をキャンセルします。

### 画像プリセットの公開  {#publishing-image-presets}

画像プリセットは自動的に公開されます。

### 画像プリセットの削除 {#deleting-image-presets}

1. Experience Managerで、Experience Managerのロゴをタップしてグローバルナビゲーションコンソールにアクセスし、ツールアイコンをタップまたはクリックして、**[!UICONTROL アセット]**/**[!UICONTROL 画像プリセット]**&#x200B;の順に移動します。
1. プリセットを選択し、「**[!UICONTROL 削除]**」をクリックします。プリセットを削除してよいか確認するメッセージが表示されます。「**[!UICONTROL 削除]**」をタップして削除するか、「**[!UICONTROL キャンセル]**」をタップして中止します。
