---
title: 画像プリセットの管理
description: 画像プリセットと、画像プリセットを作成、変更および管理する方法について説明します。
contentOwner: Rick Brough
feature: Image Presets,Viewers,Renditions
role: User
exl-id: a53f40ab-0e27-45f8-9142-781c077a04cc
source-git-commit: 36ab36ba7e14962eba3947865545b8a3f29f6bbc
workflow-type: tm+mt
source-wordcount: '3550'
ht-degree: 100%

---

# 画像プリセットの管理{#managing-image-presets}

画像プリセットを使用すると、Adobe Experience Manager Assets では異なるサイズ、異なる形式、または動的に生成された他の画像プロパティで、画像を動的に配信できます。各画像プリセットは、画像表示用のサイズやフォーマットに関するコマンドの事前定義済みコレクションを表します。画像プリセットの作成時には、画像配信用のサイズを選択します。また、フォーマットコマンドも選択すると、表示する画像が配信される際に画像の外観が最適化されます。

管理者は、アセットを書き出すためのプリセットを作成できます。ユーザーは画像を書き出すときにプリセットを選択できます。また、この操作によって、管理者が指定した仕様に合わせて画像が再フォーマットされます。

レスポンシブな画像プリセットを作成することもできます。アセットにレスポンシブな画像プリセットを適用すると、画像が表示されるデバイスや画面サイズに応じて変化します。画像プリセットは、RGB またはグレースケールに加えて CMYK をカラースペースで使用するよう設定できます。

この節では、画像プリセットを作成、変更および全般的に管理する方法について説明します。画像プリセットは、画像をプレビューする際にいつでも適用できます。詳しくは、[画像プリセットの適用](/help/assets/dynamic-media/image-presets.md)を参照してください。

>[!NOTE]
>
>スマートイメージングは、既存の画像プリセットで機能し、配信の直前にインテリジェンスを使用して、ブラウザーまたはネットワークの接続速度に基づいて画像のファイルサイズをさらに低減します。詳しくは、[スマートイメージング](/help/assets/dynamic-media/imaging-faq.md)を参照してください。

## 画像プリセットについて {#understanding-image-presets}

各画像プリセットはマクロと同様に、サイズおよびフォーマットのコマンドに関する事前定義済みのコレクションが、特定の名前で保存されたものです。画像プリセットの仕組みを理解するために、Web サイトで各商品画像を、デスクトップ配信用とモバイル配信用に異なるサイズ、異なる形式および圧縮率で表示する必要があるとします。

デスクトップ用に 500 x 500 ピクセル、モバイル用に 150 x 150 ピクセルの 2 つの画像プリセットを作成できます。2 つの画像プリセット（500 x 500 ピクセルで画像を表示する `Enlarge` プリセットおよび 150 x 150 ピクセルで画像を表示する `Thumbnail` プリセット）を作成します。`Enlarge` および `Thumbnail` サイズで画像を配信するには、Experience Manager では `Enlarge Image Preset` と `Thumbnail Image Preset` の定義を検索します。その後、Adobe Experience Manager は各画像プリセットのサイズと形式の仕様に従って画像を動的に生成します。

この場合、動的に配信されるときに画像のサイズを削減すると、シャープさと細部が失われる可能性があります。この理由で、各画像プリセットには、画像を特定のサイズで配信するときに最適化するための形式設定コントロールが含まれています。これらのコントロールによって、web サイトまたはアプリケーションに画像が配信されるときに、画像がシャープでクリアに表示されるようになります。

管理者が画像プリセットを作成できます。画像プリセットを作成する際に、最初から作成することも、既存のプリセットから始めて新しい名前で保存することもできます。

## 画像プリセットの管理 {#managing-image-presets-1}

Experience Manager で画像プリセットを管理するには、Experience Manager ロゴを選択してグローバルナビゲーションコンソールにアクセスし、ツールアイコンを選択して、**[!UICONTROL アセット]**／**[!UICONTROL 画像プリセット]**&#x200B;に移動します。

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
>アセットの詳細表示で「**[!UICONTROL レンディション]**」を選択すると、様々なレンディションが表示されます。表示される画像プリセットの数を増減させることができます。[表示される画像プリセットの数の増減](#increasing-or-decreasing-the-number-of-image-presets-that-display)を参照してください。

### Adobe Illustrator（AI）、PostScript®（EPS）、PDF の各ファイル形式 {#adobe-illustrator-ai-postscript-eps-and-pdf-file-formats}

AI ファイル、EPS ファイル、PDF ファイルの取り込みをサポートして、これらのファイル形式の動的レンディションを生成できるようにする場合は、画像プリセットを作成する前に次の情報を確認します。

Adobe Illustrator&#39;s file format is a variant of PDF. Adobe Illustrator のファイル形式は PDF のバリアントです。Adobe Experience Manager Assets における主な違いは、次のとおりです。

* Adobe Illustrator のドキュメントは複数のレイヤーを持つ単一のページで構成されます。各レイヤーはメインの Illustrator アセットの下に PNG サブアセットとして抽出されます。
* PDF のドキュメントは 1 つ以上のページで構成されます。各ページはメインの複数ページの PDF ドキュメントの下に単一ページの PDF サブアセットとして抽出されます。

`Create Sub Asset process` コンポーネントは、全体的な `DAM Update Asset` ワークフロー内にサブアセットを作成します。ワークフローにこのプロセスコンポーネントを表示するには、**[!UICONTROL ツール]**／**[!UICONTROL ワークフロー]**／**[!UICONTROL モデル]**／**[!UICONTROL DAM アセットの更新]**／**[!UICONTROL 編集]**&#x200B;に移動します。

<!-- See also [Viewing pages of a multi-page file](/help/assets/manage-linked-subassets.md#view-pages-of-a-multi-page-file). -->

サブアセットまたはページは、アセットを開き、コンテキストメニューを選択し、「**[!UICONTROL サブアセット]**」または「**[!UICONTROL ページ]**」を選択して表示できます。サブアセットは実在のアセットです。`Create Sub Asset` ワークフローコンポーネントは、PDF ページを抽出します。その後それらは `page1.pdf` や `page2.pdf` などとして、メインアセットの下に保存されます。保存後、それらは `DAM Update Asset` ワークフローで処理されます。

Dynamic Media を使用して AI、EPS または PDF ファイルの動的レンディションを表示および生成するには、次の処理ステップが必要です。

1. `DAM Update Asset` ワークフローでは、`Rasterize PDF/AI Image Preview Rendition` プロセスコンポーネントが、設定された解像度を使用して、元のアセットの最初のページを `cqdam.preview.png` レンディションにラスタライズします。

1. ワークフロー内の `Dynamic Media Process Image Assets` プロセスコンポーネントは、`cqdam.preview.png` レンディションを PTIFF に最適化します。

>[!NOTE]
>
>DAM アセットの更新ワークフローでは、**[!UICONTROL EPS サムネール]**&#x200B;のステップで EPS ファイルのサムネールが生成されます。

#### PDF/AI/EPS アセットのメタデータプロパティ {#pdf-ai-eps-asset-metadata-properties}

| **メタデータプロパティ** | **説明** |
|---|---|
| `dam:Physicalwidthininches` | ドキュメントの幅（インチ単位） |
| `dam:Physicalheightininches` | ドキュメントの高さ（インチ単位） |

`Rasterize PDF/AI Image Preview Rendition` プロセスコンポーネントのオプションには、`DAM Update Asset` ワークフローを通じてアクセスします。

左上の Adobe Experience Manager を選択し、**[!UICONTROL ツール]**／**[!UICONTROL ワークフロー]**／**[!UICONTROL モデル]**&#x200B;をクリックします。ワークフローモデルページで「**[!UICONTROL DAM アセットの更新]**」を選択し、ツールバーの「**[!UICONTROL 編集]**」を選択します。DAM アセットの更新ワークフローページで、`Rasterize PDF/AI Image Preview Rendition` プロセスコンポーネントをダブルクリックして、ステッププロパティダイアログボックスを開きます。

#### PDF/AI 画像プレビューレンディションをラスタライズのオプション {#rasterize-pdf-ai-image-preview-rendition-options}

![PDF または AI ワークフローのラスタライズの引数](assets/rasterize_pdf_ai_image_preview.png)

PDF または AI ワークフローのラスタライズの引数

| プロセス引数 | デフォルト設定 | 説明 |
|---|---|---|
| MIME タイプ | application/pdf<br>application/postscript<br>application/illustrator | PDF または Illustrator のドキュメントと見なされるドキュメントの MIME タイプのリスト。 |
| 最大の幅 | 2048 | 生成されたプレビューレンディションの最大の幅（ピクセル単位）。 |
| 最大の高さ | 2048 | 生成されたプレビューレンディションの最大の高さ（ピクセル単位）。 |
| 解決策 | 72 | 最初のページをラスタライズする解像度（ppi（インチあたりピクセル数）単位） |

デフォルトのプロセス引数を使用して、PDF/AI ドキュメントの最初のページが 72 ppi でラスタライズされ、生成されたプレビュー画像のサイズは 2048 x 2048 ピクセルになります。通常のデプロイメントでは、解像度を 150 ppi 以上に増やす必要が生じる可能性があります。例えば、300 ppi の US Letter サイズのドキュメントの幅と高さにはそれぞれ最大で 2550 x 3300 ピクセルが必要です。

ラスタライズする解像度を制限する最大の幅と最大の高さ。例えば、最大値が変更されず、解像度が 300 ppi に設定された場合、US Letter のドキュメントは 186 ppi でラスタライズされます。つまり、ドキュメントは 1581 x 2046 ピクセルになります。

`Rasterize PDF/AI Image Preview Rendition` プロセスコンポーネントには、メモリに過度に大きな画像が作成されないように、最大値が定義されています。このようなサイズの大きな画像の場合は、JVM（Java™ 仮想マシン）に提供されているメモリがオーバーフローするおそれがあります。それぞれ設定された最大サイズで画像を作成可能なワークフローを、設定した数だけ並行して管理するのに十分なメモリを JVM に提供する必要があります。

### InDesign（INDD）ファイル形式 {#indesign-indd-file-format}

このファイル形式の動的レンディションを生成できるよう INDD 形式の取り込みをサポートする場合は、画像プリセットを作成する前に次の情報を確認してください。

InDesign ファイルについては、Adobe InDesign Server が AEM Experience Manager に統合されている場合にのみサブアセットが抽出されます。参照元のアセットは、メタデータに基づいてリンクされます。リンク設定に InDesign Server は不要です。ただし、リンクが InDesign ファイルと参照元のアセットの間に作成されるには、InDesign ファイルが処理される前に参照元のアセットが Adobe Experience Manager 内に存在する必要があります。

<!-- See [Integrate Experience Manager Assets with InDesign Server](/help/assets/indesign.md). -->

`DAM Update Asset` ワークフローのメディア抽出プロセスコンポーネントでは、事前設定された「スクリプトを拡張」をいくつか実行して InDesign ファイルを処理します。

![メディア抽出プロセスの引数で使用される ExtendScript のパス](/help/assets/dynamic-media/assets/6_5_mediaextractionprocess.png)

DAM アセットの更新ワークフローのメディア抽出プロセスコンポーネントの引数で使用される ExtendScript のパス。

Dynamic Media 統合では、以下のスクリプトが使用されます。


| ExtendScript 名 | デフォルト | 説明 |
|---|---|---|
| ThumbnailExport.jsx | はい | `Dynamic Media Process Image Assets` プロセスコンポーネントによって最適化され PTIFF レンディションに変換される 300 ppi の `thumbnail.jpg` レンディションを生成します。 |
| JPEGPagesExport.jsx | はい | ページごとに 300 ppi の JPEG サブアセットを生成します。JPEG サブアセットは実在のアセットで、InDesign アセットの下に保存されます。`DAM Update Asset` ワークフローは、これを最適化し、PTIFF に変換します。 |
| PDFPagesExport.jsx | いいえ | ページごとに PDF サブアセットを生成します。PDF サブアセットは前述のように処理されます。PDF には 1 つのページのみ含まれているので、サブアセットは生成されません。 |

### 画像のサムネールサイズの設定 {#configuring-image-thumbnail-size}

**[!UICONTROL DAM アセットの更新]**&#x200B;ワークフローで設定することにより、サムネールのサイズを設定できます。画像アセットのサムネールサイズの設定にはワークフローで 2 つのステップがあります。一方（**[!UICONTROL ダイナミックメディアプロセスの画像アセット]**）は、動的な画像アセットに使用されます。もう一方（**[!UICONTROL サムネールを処理]**）は、静的なサムネールの生成に使用されるか、その他のすべてのプロセスでサムネールを生成できなかった場合に使用されます。いずれにせよ、*両方*&#x200B;とも同じ設定にする必要があります。

**[!UICONTROL Dynamic Media プロセスの画像アセット]**&#x200B;ステップでは、**[!UICONTROL サムネールを処理]**&#x200B;のステップに適用された設定とは関係なく、画像サーバーを使用してサムネールを生成します。**[!UICONTROL サムネールを処理]**&#x200B;のステップで行うサムネールの生成は、サムネール生成で最も遅く、最もメモリを使う方法です。

サムネールのサイズは **[!UICONTROL width:height:center]** の形式で定義されます（例：`80:80:false`）。width と height はサムネールのサイズをピクセル単位で指定します。center の値は false または true で、true に設定した場合は、サムネール画像のサイズが設定で指定されたサイズとまったく同じであることを示します。画像が指定よりも小さいサイズに変更された場合は、サムネール内で中央揃えされます。

>[!NOTE]
>
>* EPS ファイルのサムネールサイズは 「サムネール」の下の「**[!UICONTROL 引数]**」タブにある **[!UICONTROL EPS サムネール]**&#x200B;のステップで設定します。
>
>* ビデオのサムネールサイズは「**[!UICONTROL 引数]**」の下にある「**[!UICONTROL 処理]**」タブの **[!UICONTROL FFmpeg サムネール]**&#x200B;のステップで設定します。
>

**画像のサムネールサイズを設定するには：**

1. **[!UICONTROL ツール]**／**[!UICONTROL ワークフロー]**／**[!UICONTROL モデル]**／**[!UICONTROL DAM アセットの更新]**／**[!UICONTROL 編集]**&#x200B;に移動します。
1. **[!UICONTROL Dynamic Media プロセスの画像アセット]**&#x200B;のステップを選択し、「**[!UICONTROL サムネール]**」タブを選択します。必要に応じてサムネールのサイズを変更し、「**[!UICONTROL OK]**」を選択します。

   ![6_5_dynamicmediaprocessimageassets-thumbnailstab](assets/6_5_dynamicmediaprocessimageassets-thumbnailstab.png)

1. **[!UICONTROL サムネールを処理]**&#x200B;のステップを選択し、「**[!UICONTROL サムネール]**」タブを選択します。必要に応じてサムネールのサイズを変更し、「**[!UICONTROL OK]**」を選択します。

   >[!NOTE]
   >
   >**[!UICONTROL サムネールを処理]**&#x200B;ステップのサムネール引数の値が、**[!UICONTROL Dynamic Media プロセスの画像アセット]**&#x200B;ステップのサムネール引数と一致する必要があります。

1. 「**[!UICONTROL 保存]**」を選択して、ワークフローに対する変更を保存します。

### 表示される画像プリセットの数の増減 {#increasing-or-decreasing-the-number-of-image-presets-that-display}

作成した画像プリセットは、アセットをプレビューする際の動的レンディションとして使用できます。Adobe Experience Manager では、**[!UICONTROL 詳細表示／レンディション]**&#x200B;からアセットを表示すると、様々な動的レンディションが表示されます。表示されるレンディション数の制限を増減させることができます。

**表示される画像プリセットの数を増減させるには：**

1. CRXDE Lite（[https://localhost:4502/crx/de](https://localhost:4502/crx/de)）に移動します。
1. 画像プリセットリストノード（`/libs/dam/gui/coral/content/commons/sidepanels/imagepresetsdetail/imgagepresetslist`）に移動します。

   ![increase_decreasethenumberofimagepresetsthatdisplay](assets/increase_decreasethenumberofimagepresetsthatdisplay.png)

1. 「**[!UICONTROL limit]**」プロパティで、「**[!UICONTROL 値]**」（デフォルトで 15 に設定されています）を目的の数に変更します。
1. 画像プリセットデータソース（`/libs/dam/gui/coral/content/commons/sidepanels/imagepresetsdetail/imgagepresetslist/datasource`）に移動します。

   ![chlimage_1-495](assets/chlimage_1-495.png)

1. 「limit」プロパティの数を、目的の数に変更します。例：`{empty requestPathInfo.selectors[1] ? "20" : requestPathInfo.selectors[1]}`
1. 「**[!UICONTROL すべて保存]**」を選択します。

### 画像プリセットの作成 {#creating-image-presets}

画像プリセットを作成すると、プレビュー時または公開時に画像全体に一貫して設定を適用できます。

>[!NOTE]
>
>Internet Explorer 9 を使用している場合、プリセットを作成しても、保存後すぐにプリセットのリストに表示されません。この問題を回避するには、IE9 のキャッシュを無効にします。

AI ファイル、PDF ファイル、EPS ファイルの取り込みをサポートして、これらのファイル形式の動的レンディションを生成できるようにする場合は、画像プリセットを作成する前に次の情報を確認してください。

詳しくは、[Adobe Illustrator（AI）、PostScript®（EPS）、PDF の各ファイル形式](#adobe-illustrator-ai-postscript-eps-and-pdf-file-formats)を参照してください。

このファイル形式の動的レンディションを生成できるよう INDD 形式の取り込みをサポートする場合は、画像プリセットを作成する前に次の情報を確認してください。

詳しくは、[InDesign（INDD）ファイル形式](#indesign-indd-file-format)を参照してください。

**画像プリセットを作成するには：**

1. Adobe Experience Manager で、Adobe Experience Manager ロゴを選択してグローバルナビゲーションコンソールにアクセスし、**[!UICONTROL ツール]**／**[!UICONTROL アセット]**／**[!UICONTROL 画像プリセット]**&#x200B;に移動します。
1. 「**[!UICONTROL 作成]**」を選択します。

   ![chlimage_1-496](assets/chlimage_1-496.png)

   >[!NOTE]
   >
   >この画像プリセットをレスポンシブにするには、「**[!UICONTROL 幅]**」フィールドと「**[!UICONTROL 高さ]**」フィールドの値を消去して空のままにします。

1. **[!UICONTROL 画像プリセットを編集]**&#x200B;ウィンドウで、「**[!UICONTROL 基本]**」または「**[!UICONTROL 詳細]**」のどちらか該当するタブに、名前などの値を入力します。オプションの概要については、[画像プリセットオプション](#image-preset-options)で説明しています。プリセットは左側のウィンドウに表示され、他のアセットにすぐに使用できます。

   ![6_5_imagepreset-edit](assets/6_5_imagepreset-edit.png)

1. 「**[!UICONTROL 保存]**」を選択します。

### レスポンシブな画像プリセットの作成 {#creating-a-responsive-image-preset}

レスポンシブな画像プリセットを作成するには、[画像プリセットの作成](#creating-image-presets)の手順を実行します。**[!UICONTROL 画像プリセットを編集]**&#x200B;ウィンドウで高さと幅を入力する際に、これらの値を消去して空のままにします。

空のままにすることで、この画像プリセットがレスポンシブであることを Experience Manager に指示します。他の値は、必要に応じて変更できます。

>[!NOTE]
>
>画像プリセットをアセットに適用するときに「**[!UICONTROL URL]**」ボタンと「**[!UICONTROL RESS]**」ボタンを表示するには、アセットを公開する必要があります。
>
>![chlimage_1-79](assets/chlimage_1-498.png)
>
>画像プリセットと画像アセットは自動的に公開されます。

### 画像プリセットオプション {#image-preset-options}

画像プリセットを作成または編集する場合、この節で説明するオプションを使用できます。またアドビは、最初に使用すべきオプションとして、以下の「ベストプラクティス」オプションをお勧めします。

* **[!UICONTROL 形式]**（「**[!UICONTROL 基本]**」タブ）- 「**[!UICONTROL JPEG]**」または要件を満たす他の形式を選択します。JPEG 画像形式はすべての Web ブラウザーでサポートされ、小さなファイルサイズと画質のバランスが良い形式です。ただし、JPEG 形式の画像では非可逆圧縮方式が使用されるので、圧縮設定が低すぎる場合は望ましくない画像アーティファクトが発生する可能性があります。このため、アドビは圧縮品質を 75 に設定することをお勧めします。この設定は、画質と小さなファイルサイズのバランスが取れた設定です。

* **[!UICONTROL シンプルシャープを有効にする]** - 「**[!UICONTROL シンプルシャープを有効にする]**」は選択しません（このシャープフィルターでは、アンシャープマスク設定よりも細かく制御できません）。

* **[!UICONTROL シャープ：再サンプリングモード]** - 「**[!UICONTROL シャープ 2]**」を選択します。

#### 「基本」タブオプション  {#basic-tab-options}

| フィールド | 説明 |
| --- | --- |
| **名前** | わかりやすい名前を空白なしで入力します。この画像プリセットを識別しやすくするには、名前に画像サイズを含めます。 |
| **「幅」と「高さ」** | 画像が配信されるサイズをピクセル単位で入力します。「幅」と「高さ」は 0 ピクセルより大きい値にする必要があります。いずれかの値が 0 の場合、プリセットは作成されません。両方の値が空の場合、レスポンシブな画像プリセットが作成されます。 |
| **形式** | メニューから形式を選択します。<br>「**JPEG**」を選択すると、他に次のオプションが表示されます。<br>• **画質** - JPEG 画質の尺度は 1～100 です。スライダーをドラッグすると、このスケールが表示されます。<br>• **JPG クロミナンスダウンサンプリングを有効にする** - 目は高周波の色情報より高周波の輝度に対して敏感であるので、JPEG 画像では、画像情報が輝度成分と色成分に分けられます。JPEG 画像が圧縮されると、輝度成分はフル解像度のまま、色成分がピクセルのグループでまとめて平均化されることで、ダウンサンプリングされます。ダウンサンプリングによって、知覚される画質への影響を最小限に抑えながら、データ量を半分または 3 分の 1 まで削減できます。ダウンサンプリングはグレースケール画像には適用できません。この技術は高コントラストの画像（オーバーレイされたテキストを含む画像など）で役立つ圧縮量を削減します。<br><br>「**GIF**」または「**アルファ付き GIF**」を選択すると、次の追加の「**GIF カラー量子化**」オプションを入力できます。<br>• **タイプ** - 「**アダプティブ**」（デフォルト）、「**Web**」、「**Macintosh**」のいずれかを選択します。「**アルファ付き GIF**」を選択した場合は、「Macintosh」オプションは使用できません。<br>• **ディザ** - 「**拡散**」または「**オフ**」を選択します。<br>• **色数** - 2～256 の値を入力します。<br>• **カラーリスト** - コンマ区切りのリストを入力します。例えば、白、グレー、黒の場合は、`000000,888888,ffffff` と入力します。<br><br>「**PDF**」、「**TIFF**」または「**アルファ付き TIFF**」を選択すると、次の追加オプションを入力できます。<br>• **圧縮** - 圧縮アルゴリズムを選択します。PDF 用のアルゴリズムオプションは、「**なし**」、「**Zip**」および「**JPEG**」です。TIFF の場合は、「**なし**」、「**LZW**」、「**JPEG**」および「**Zip**」です。また、アルファ付き TIFF の場合は、「**なし**」、「**LZW**」および「**Zip**」です。<br><br>「**PNG**」、「**アルファ付き PNG**」または「**EPS**」を選択した場合は、追加オプションはありません。 |
| **シャープ** | 「**シンプルシャープを有効にする**」を選択すると、すべての拡大縮小の実行後、画像に対して基本的なシャープフィルターが適用されます。シャープにより、画像を異なるサイズで表示した場合に発生するぼかしを補うことができます。 |

#### 「詳細」タブオプション  {#advanced-tab-options}

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
   <td>作業プロファイルと異なる場合にアセットの変換先を表す出力カラースペースプロファイルを選択します。</td>
  </tr>
  <tr>
   <td><strong>レンダリングインテント</strong></td>
   <td>デフォルトのレンダリングインテントを上書きできます。レンダリングインテントは、対象のカラープロファイルでは再現できない（色域外の）色をどうするかを定義します。レンダリングインテントは、ICC プロファイルと互換性がない場合は無視されます。
    <ul>
     <li>「<strong>知覚的</strong>」は、元の画像の 1 つ以上の色が対象のカラースペースの色域外であるときに、一方のカラースペースの全色域をもう一方のカラースペースの色域に圧縮する場合に選択します。</li>
     <li>「<strong>相対的な色域を維持</strong>」は、現在のカラースペースの 1 色が対象のカラースペースの色域外であるときに選択します。また、他の色を変更せずに、最も近い対象の色域にマッピングする必要があります。 </li>
     <li>「<strong>彩度</strong>」は、対象のカラースペースに変換するときに元の画像の色の彩度を再現する場合に選択します。 </li>
     <li>「<strong>絶対的な色域を維持</strong>」は、画像の明るさを変える白点と黒点の調整なしで色を完全に一致させる場合に選択します。</li>
    </ul> </td>
  </tr>
  <tr>
   <td><strong>黒点補正</strong></td>
   <td>出力プロファイルでこの機能がサポートされている場合、このオプションを選択します。指定した ICC プロファイルと互換性がない場合、黒点補正は無視されます。</td>
  </tr>
  <tr>
   <td><strong>ディザリング</strong></td>
   <td>このオプションを選択すると、カラーバンディングアーティファクトを回避または軽減できます。 </td>
  </tr>
  <tr>
   <td><strong>シャープタイプ</strong></td>
   <td><p>「<strong>なし</strong>」、「<strong>シャープ</strong>」または「<strong>アンシャープマスク</strong>」を選択します。 </p>
    <ul>
     <li>シャープを無効にする場合は、「<strong>なし</strong>」を選択します。</li>
     <li>「<strong>シャープ</strong>」を選択すると、すべての拡大縮小の実行後、画像に対して基本的なシャープフィルターが適用されます。シャープにより、画像を異なるサイズで表示した場合に発生するぼかしを補うことができます。 </li>
     <li>ダウンサンプリングされた最終的な画像に対するシャープフィルター効果を細かく調整する場合は、「<strong>アンシャープマスク</strong>」を選択します。エフェクトの強さ、エフェクトの半径（ピクセル単位）、無視されるコントラストのしきい値を調整できます。このエフェクトでは、 Photoshop の「アンシャープマスク」フィルターと同じオプションが使用されます。</li>
    </ul> <p>「<strong>アンシャープマスク</strong>」には次のオプションがあります。</p>
    <ul>
     <li><strong>量</strong> - 端のピクセルに適用されるコントラストを制御します。デフォルトの実数値は 1.0 です。高解像度の画像に対しては、この値を 5.0 まで増やすことができます。「量」は、フィルター強度の尺度だと考えてください。</li>
     <li><strong>半径</strong> - シャープに影響するエッジピクセルの周囲のピクセル数を決定します。解像度の高い画像では、1～2 の実数を入力します。値が小さい場合、エッジのピクセルのみがシャープニングされます。値が大きい場合、より広い範囲のピクセルがシャープニングされます。画像のサイズによって適切な値が変わります。</li>
     <li><strong>しきい値</strong> - アンシャープマスクフィルターが適用される場合のコントラストの範囲を指定します。つまり、このオプションでは、エッジのピクセルと見なされシャープ化されるために、シャープ化されるピクセルが周囲の領域とどの程度異なっていなければならないかを定義します。ノイズが入らないように、2～20 の範囲で様々な整数値を試してください。 </li>
     <li><strong>適用先</strong> - アンシャープを各カラーまたは明るさに適用するかを指定します。</li>
    </ul>
    <div>
      シャープニングについては、<a href="https://experienceleague.adobe.com/ja/docs/experience-manager-learn/assets/dynamic-media/images/dynamic-media-image-sharpening-feature-video-use#dynamic-media">Adobe Experience Manager Dynamic Media での画像シャープニングの使用</a>のビデオ、<a href="https://experienceleague.adobe.com/ja/docs/dynamic-media-classic/using/master-files/sharpening-image#master-files">画像のシャープニングに関するオンラインヘルプトピック</a>、<a href="https://experienceleague.adobe.com/docs/dynamic-media-classic/assets/s7_sharpening_images.pdf?lang=ja">Adobe Dynamic Media Classic (Scene7) Image Quality and Sharpening Best Practices</a> と題するダウンロード可能な PDF を参照してください。
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
     <li><strong>各カラー</strong>と<strong>明るさ</strong> - 色または明るさに基づいた手法です。デフォルトでは、「<strong>各カラー</strong>」が選択されます。</li>
    </ul> </td>
  </tr>
  <tr>
   <td><strong>プリント解像度</strong></td>
   <td>この画像のプリント用解像度を選択します。デフォルトは 72 ピクセルです。</td>
  </tr>
  <tr>
   <td><strong>画像の修飾子</strong></td>
   <td><p>UI で使用できる共通の画像設定のほか、Dynamic Media では「<strong>画像の修飾子</strong>」フィールドで画像の詳細を多数指定できます。これらのパラメーターは、<a href="https://experienceleague.adobe.com/ja/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/http-protocol-reference/syntax-and-features/image-serving-http/c-command-overview">Image Server プロトコルのコマンドリファレンス（英語）</a>で定義されています。</p> <p>重要：API にリストされている次の関数はサポートされていません。</p>
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

「基本」タブと「詳細」タブで使用できるオプションに加えて、画像の修飾子を定義して、画像プリセットの定義でより多くのオプションを指定することができます。画像のレンダリングには Dynamic Media 画像レンダリング API が利用されており、詳しくは [HTTP プロトコルリファレンス](https://experienceleague.adobe.com/ja/docs/dynamic-media-developer-resources/image-serving-api/image-rendering-api/http-protocol-reference/c-ir-introduction#image-rendering-api)で定義されています。

画像の修飾子を使用して実行できることについて、以下に基本的な例を示します。

>[!NOTE]
>
>一部の画像修飾子は、[Adobe Experience Manager では使用できません](#advanced-tab-options)。

* [op_invert](https://experienceleague.adobe.com/ja/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/http-protocol-reference/command-reference/r-op-invert) - それぞれの色成分を、画像の効果が反対になるように逆転させます。

  ```xml {.line-numbers}
  &op_invert=1
  ```

  ![6_5_imagepreset-edit-invert](assets/6_5_imagepreset-edit-invert.png)

* [op_blur](https://experienceleague.adobe.com/ja/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/http-protocol-reference/command-reference/r-op-blur) - 画像にぼかしフィルターを適用します。

  ```xml {.line-numbers}
  &op_blur=7
  ```

  ![6_5_imagepreset-edit-blur](assets/6_5_imagepreset-edit-blur.png)

* コマンドの組み合わせ - op_blur と op-invert

  ```xml {.line-numbers}
  &op_invert=1&op_blur=7
  ```

  ![chlimage_1-80](assets/chlimage_1-501.png)

* [op_brightness](https://experienceleague.adobe.com/ja/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/http-protocol-reference/command-reference/r-op-brightness) - 明るさを増減させます。

  ```xml {.line-numbers}
  &op_brightness=58
  ```

  ![6_5_imagepreset-edit-brightness](assets/6_5_imagepreset-edit-brightness.png)

* [opac](https://experienceleague.adobe.com/ja/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/http-protocol-reference/command-reference/r-opac) - 画像の不透明度を調節します。前景の不透明度を減らすことができます。

  ```xml {.line-numbers}
  opac=29
  ```

  ![6_5_imagepreset-edit-opacity](assets/6_5_imagepreset-edit-opacity.png)

### 画像プリセットの編集 {#modifying-image-presets}

1. Adobe Experience Manager で、Adobe Experience Manager ロゴを選択してグローバルナビゲーションコンソールにアクセスし、**[!UICONTROL ツール]**／**[!UICONTROL アセット]**／**[!UICONTROL 画像プリセット]**&#x200B;に移動します。

   ![6_5_imagepreset-editpreset](assets/6_5_imagepreset-editpreset.png)

1. プリセットを選択してから、「**[!UICONTROL 編集]**」を選択します。**[!UICONTROL 画像プリセットを編集]**&#x200B;ウィンドウが開きます。
1. 変更を加え、「**[!UICONTROL 保存]**」を選択して変更を保存するか、「**[!UICONTROL キャンセル]**」を選択して変更をキャンセルします。

### 画像プリセットの公開 {#publishing-image-presets}

画像プリセットは自動的に公開されます。

### 画像プリセットの削除 {#deleting-image-presets}

1. Adobe Experience Manager で、Adobe Experience Manager ロゴを選択してグローバルナビゲーションコンソールにアクセスし、ツールアイコンを選択します。
1. **[!UICONTROL アセット]**／**[!UICONTROL 画像プリセット]**&#x200B;に移動します。
1. プリセットを選択し、「**[!UICONTROL 削除]**」を選択します。プリセットを削除してよいか確認するメッセージが表示されます。「**[!UICONTROL 削除]**」を選択して削除を実行するか、「**[!UICONTROL キャンセル]**」を選択して画像プリセットに戻ります。
