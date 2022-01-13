---
title: Dynamic Mediaの一般設定
description: Dynamic Mediaで一般設定を管理する方法を説明します。 ここでパブリッシュサーバー名とオリジンサーバー名を設定し、画像の上書きオプションを設定できます。 また、画像のアンシャープマスク用のデフォルトのアップロードオプションや、PostScript、Adobe Photoshop、PDF、Adobe Illustratorの各ファイルを処理する方法に関するアップロードオプションも用意されています。
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: administering
content-type: reference
feature: Image Profiles
role: User, Admin
mini-toc-levels: 4
exl-id: a4d28786-cffa-42ab-98d3-90a15313e401
source-git-commit: cca950b0a4eed60f82d65779766405ed216111e3
workflow-type: tm+mt
source-wordcount: '2492'
ht-degree: 34%

---

# Dynamic Mediaの一般設定

<!-- hide: yes
hidefromtoc: yes -->

設定 **[!UICONTROL Dynamic Media General Settings]** は、次の場合にのみ使用できます。

* 次のアカウントがある *既存* **[!UICONTROL Dynamic Media Configuration]** ( **[!UICONTROL Cloud Services]**) をAdobe Experience Manager as a Cloud Serviceでクリックします。 詳しくは、 [Cloud ServicesでのDynamic Media設定の作成](/help/assets/dynamic-media/config-dm.md#configuring-dynamic-media-cloud-services).
* 管理者権限を持つExperience Manager・システム管理者です。

Dynamic Mediaの一般設定は、経験豊富な Web サイト開発者やプログラマーが使用することを目的としています。 AdobeDynamic Mediaでは、これらの公開設定を変更するユーザーに、Adobe Experience Manager上のDynamic Mediaと基本的な画像技術に精通していることをお勧めします。

アカウントの作成時に、AdobeDynamic Mediaが会社に割り当てられたサーバーを自動的に提供します。 これらのサーバーは、Web サイトとアプリケーションの URL 文字列を生成するのに使用されます。これらの URL 呼び出しは、アカウントに固有です。

Dynamic Mediaの公開設定ページでは、AdobeDynamic Mediaサーバーから Web サイトやアプリケーションにアセットを配信する方法を決定するデフォルト設定を指定します。 設定が指定されていない場合、AdobeDynamic Mediaサーバーは、Dynamic Media公開設定ページで設定されたデフォルト設定に従ってアセットを配信します。

関連トピック [オプション — Dynamic Media設定のセットアップと設定](/help/assets/dynamic-media/config-dm.md#optional-setup-and-configuration-of-dynamic-media-scene-mode-settings) を参照してください。

>[!NOTE]
>
>Dynamic Media ClassicからAdobe Experience Manager上のDynamic Mediaにアップグレードする場合 一般設定ページおよび [公開設定](/help/assets/dynamic-media/dm-publish-settings.md) Dynamic Mediaのページには、Dynamic Media Classicアカウントから取得した値が事前に設定されています。 例外は、 **[!UICONTROL デフォルトのアップロードオプション]** 」領域に表示されます。 これらの値は既にExperience Manager中です。 したがって、以下で行う変更 **[!UICONTROL デフォルトのアップロードオプション]**&#x200B;では、5 つのタブのいずれかにまたがって、Experience Managerユーザーインターフェイスを介して、Dynamic Media ClassicではなくDynamic Mediaに反映されます。 一般設定ページおよび [公開設定](/help/assets/dynamic-media/dm-publish-settings.md) ページは、Experience Manager時にDynamic Media ClassicとDynamic Mediaの間で管理されます。

**Dynamic Mediaの一般設定を構成するには：**

1. Experience Manager作成モードで、Experience Managerロゴを選択して、グローバルナビゲーションコンソールにアクセスします。
1. 左側のレールでツールアイコンを選択し、に移動します。 **[!UICONTROL Assets]** > **[!UICONTROL Dynamic Media General Settings]**.
1. サーバーページで、 **[!UICONTROL 公開先サーバー名]** および **[!UICONTROL オリジンサーバー名]**&#x200B;画像編集用のデフォルトのアップロードオプションと、Postscript、Photoshop、PDF、Illustratorの各ファイル用のデフォルトのアップロードオプションを設定するには、5 つのタブを使用します。

   * [サーバー](#server-general-setting)
   * [アプリケーションへのアップロード](#upload-to-application)
   * [画像編集](#image-editing-tab) タブ
   * [PostScript](#postscript-tab) タブ
   * [Photoshop](#photoshop-tab) タブ
   * [PDF](#pdf-tab) タブ
   * [Illustrator](#illustrator-tab) タブ

   ![Dynamic Mediaの一般設定ページ](/help/assets/assets-dm/dm-general-settings.png)
   *Dynamic Mediaの一般設定ページ、**[!UICONTROL 画像編集]**」タブが選択されています。*<br><br>

1. 作業が完了したら、ページの右上隅付近にある「 」を選択します。 **[!UICONTROL 保存]**.

## サーバー {#server-general-setting}

アカウントの作成時に、AdobeDynamic Mediaが会社に割り当てられたサーバーを自動的に提供します。 これらのサーバーは、Web サイトとアプリケーションの URL 文字列を生成するのに使用されます。これらの URL 呼び出しは、アカウントに固有です。

| オプション | 説明 |
| --- | --- |
| **[!UICONTROL 公開先サーバー名]** | 必須。<br>名前は `https://` パスに含まれています。<br>このサーバーは、アカウントに固有のすべてのシステム生成 URL 呼び出しで使用されるライブ CDN（コンテンツ配信ネットワーク）サーバーです。 Adobe・テクニカル・サポートから指示されない限り、このサーバ名は変更しないでください。 |
| **[!UICONTROL 公開元サーバー名]** | 必須。<br>このサーバーは、品質保証テストにのみ使用されます。 Adobe・テクニカル・サポートから指示がない限り、このサーバ名を変更しないでください。 |

## アプリケーションへのアップロード {#upload-to-application}

* **[!UICONTROL 画像を上書き]**

   AdobeDynamic Mediaでは、2 つのファイルが同じ名前を持つことを許可していません。 各項目のAdobeDynamic Media ID（画像名からファイル名拡張子を取り除いた部分）は一意である必要があります。 この規則のため、 **[!UICONTROL アプリケーションにアップロード]** は上書きされます。 このオプションの正確な効果は、選択した「画像を上書き」オプションによって異なります。 次のオプションで、置き換え画像のアップロード方法を指定します。元の画像を置き換えるか、重複画像にするかを指定します。 重複する画像の名前は `-1`. 例： `chair.tif` の名前が変更されました `chair-1.tif`. これらのオプションは、元の画像とは別のフォルダにアップロードされた画像や、元の画像とは異なるファイル名拡張子 (JPG、TIF、PNG など ) を持つ画像に影響を与えます。

   >[!NOTE]
   >
   >Experience Managerとの一貫性を維持するには、「画像を上書き」オプションを選択します **[!UICONTROL 現在のフォルダでベース名と拡張子が同じファイルを上書き]**.

   | 「画像を上書き」オプション | 説明 |
   | --- | --- |
   | **[!UICONTROL 現在のフォルダーにあるベース名と拡張子が同じファイルを上書き]** | *デフォルト* 新しいDynamic Mediaアカウントのみ。<br>このオプションは最も厳格な置換規則です。 置き換え画像を元の画像と同じフォルダーにアップロードし、置き換え画像と元の画像のファイル名拡張子が同じになっている必要があります。これらの要件が満たされない場合は、重複する画像が作成されます。<br>*Experience Managerとの一貫性を維持するには、このオプションを選択します*. |
   | **[!UICONTROL 現在のフォルダーにあるベース名が同じファイルを上書き]** | 置き換え画像を元の画像と同じフォルダーにアップロードする必要がありますが、ファイル名の拡張子は元の画像と異なる場合があります。 例えば、chair.tif は chair.jpg を置き換えます。 |
   | **[!UICONTROL 任意のフォルダーにあるベース名と拡張子が同じファイルを上書き]** | 置き換え画像のファイル名拡張子が元の画像と同じである必要があります（例えば、chair.jpg は chair.tif ではなく chair.jpg を置き換える必要があります）。 ただし、置き換え画像を、元の画像と別のフォルダーにアップロードできます。更新された画像は新しいフォルダーにあり、元の場所のファイルはなくなります。  |
   | **[!UICONTROL 任意のフォルダーでベース名が同じファイルを上書き]** | このオプションは、最も包括的な置換規則です。 置き換え画像を、元の画像と別のフォルダーにアップロードでき、ファイル名拡張子が異なるファイルをアップロードして、元のファイルと置き換えることができます。元のファイルが別のフォルダーにある場合、置き換え画像は、アップロード先の新しいフォルダーに存在します。 |

* **[!UICONTROL 切り抜きを保持]**

   既存の手動切り抜き定義の保存をコントロールします。

   関連トピック `preserveCrop` in [UploadPostJob](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-production-api/data-types/r-upload-post-job.html) および [ReprocessAssetsJob](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-production-api/data-types/r-reprocess-assets-job.html)(『Dynamic Mediaビューアリファレンスガイド』の )

## デフォルトのアップロードオプション {#default-upload-options}

### 「画像編集」タブ {#image-editing-tab}

このフィルターを使用すると、ダウンサンプリングされた最終的な画像に対するシャープフィルター効果を微調整できます。 効果の強さ、効果の半径（ピクセル単位）、無視されるコントラストのしきい値を制御するのに役立ちます。

「アンシャープマスク」エフェクトでは、Photoshopのアンシャープマスクフィルターと同じオプションが使用されます。 名前から連想される機能と違い、アンシャープマスクとはシャープニングフィルターのことです。

| アンシャープマスクオプション | 説明 |
| --- | --- |
| **[!UICONTROL 量]** | 必須。<br>端のピクセルに適用するコントラストを制御します。<br>この量は、効果の強さと考えることができます。AdobeDynamic Mediaのアンシャープマスクの量の値とAdobe Photoshopの量の値の主な違いは、Photoshopの量の範囲が 1%～500%である点です。 一方、AdobeDynamic Mediaでは、値の範囲は `0.0` から `5.0`. AdobeDynamic Mediaの値が 5.0 の場合、Photoshopの 500%に相当します。値が 0.9 の場合は 90%と等しくなります。 |
| **[!UICONTROL 半径]** | 必須。<br>効果の半径を制御します。<br>値の範囲は `0` から `250`. 効果は画像内の全ピクセルに切れ目なく続き、すべてのピクセルから全方向に放射されます。半径はピクセル単位です。例えば、2000 x 2000 ピクセルの画像と 500 x 500 ピクセルの画像で同様のシャープ効果を得るには、2000 x 2000 ピクセルの画像で 2 ピクセルの半径を設定します。 次に、500 x 500 ピクセルのイメージ上で 1 ピクセルの半径値を設定します。 ピクセル数の多い画像には大きい値を使用します。 |
| **[!UICONTROL しきい値]** | 必須。<br>しきい値とは、アンシャープマスクフィルターの適用時に無視されるコントラストの範囲です。この効果は、このフィルタを使用する際に画像に「ノイズ」が入り込まないようにするために重要です。 値の範囲は `0` - `255`：グレースケール画像の明るさのステップ数です。 `0`=黒、=50% グレー、=白です。`128``255`<br>しきい値： `12` は、ノイズの追加を避けるために、わずかなバリエーションがスキントーンの明るさであることを無視しますが、まつげがスキンと交わる場所など、コントラストの強い領域にはエッジのコントラストが追加されます。<br>他のユーザーの顔写真がある場合は、アンシャープマスクが画像のコントラストの部分に影響します。 例えば、まつ毛と肌がぶつかり合い、明らかなコントラストの領域を作り出し、滑らかな肌自体を作り出す場所です。 非常に滑らかな肌でも、明るさの値はわずかに変化しています。しきい値を使用しないと、このフィルターはこのような肌部分のピクセルのわずかな変化を強調します。同様に、まつげのコントラストを強めてシャープさを強調し、ノイズのある望ましくない効果を生み出してしまいます。<br>しきい値は、この問題を解決するために導入されたもので、フィルターに対し、滑らかな肌のようにコントラストが大きく変化しないピクセルは無視するよう指示します。<br>先ほど示したファスナーのグラフィックで、ファスナーの横の生地に注目してください。しきい値が低すぎてノイズを抑制できなかったので、画像ノイズが発生しています。 |
| **[!UICONTROL モノクロ]** | 選択すると、画像の明るさ（強さ）にアンシャープマスクが適用されます。<br>選択を解除すると、それぞれの色成分に別々にアンシャープマスクが適用されます。 |

関連トピック [AdobeDynamic Mediaおよび Image Server での画像のシャープニング](https://experienceleague.adobe.com/docs/experience-manager-65/assets/sharpening_images.pdf?lang=en).

### 「PostScript」タブ {#postscript-tab}

Adobe PostScript®ファイルのラスタライズ、透明背景の維持、解像度の選択、カラースペースの選択を行うことができます。

Adobe PostScript® (EPS) ファイルは、AdobeDynamic Mediaで使用できます。 AdobeDynamic Mediaには、アップロード時にこれらのファイルを設定するためのコマンドが用意されています。

PostScript(EPS) 画像ファイルをアップロードする際には、様々な方法で形式を設定できます。 ファイルのラスタライズ、透明背景の維持、解像度の選択、カラースペースの選択ができます。

| PostScript オプション | 説明 |
| --- | --- |
| **[!UICONTROL 処理]** | ラスタライズを選択して、ファイル内のベクターグラフィックスをビットマップ形式に変換します。 |
| **[!UICONTROL レンダリング済みの画像で透明背景色を維持]** | ファイルの背景の透明度を保持します。 |
| **[!UICONTROL 解像度 (ピクセル/インチ)]** | 解像度設定を決定します。この設定により、ファイル内の 1 inch あたりに表示するピクセル数を決定します。 |
| **[!UICONTROL カラースペース]** | ・ **[!UICONTROL 自動検出]**  — ファイルのカラースペースを保持します。<br>・ **[!UICONTROL 強制RGB]**  — をRGBのカラースペースに変換します。<br>・ **[!UICONTROL CMYK としてレンダリング]** - CMYK カラースペースに変換します。<br>・ **[!UICONTROL グレースケールとして強制]**  — グレースケールカラースペースに変換します。 |

### Photoshopタブ {#photoshop-tab}

Adobe® Photoshop® ファイルからのテンプレート作成、レイヤーの維持、レイヤーの命名方法の指定、テキストの抽出、テンプレートへの画像のアンカー方法の指定をおこなうことができます。

| Photoshopオプション | 説明 |
| --- | --- |
| **[!UICONTROL レイヤーを維持]** | PSD にレイヤーがあれば切り離して個別のアセットにします。アセットレイヤーは PSD に関連付けられたまま維持されます。詳細ビューでPSDファイルを開き、画層パネルを選択すると、画層を表示できます。 詳しくは、レイヤーファイルの表示とPSDを参照してください。 |
| **[!UICONTROL テンプレートを作成]** | PSD ファイル内のレイヤーからテンプレートを作成します。 |
| **[!UICONTROL テキストを抽出]** | テキストを抽出して、ユーザーがビューア内でテキストを検索できるようにします。 |
| **[!UICONTROL レイヤーを背景サイズに拡大]** | 切り離した画像レイヤーのサイズを、背景レイヤーのサイズに拡大します。 |
| **[!UICONTROL レイヤーの名前]** | 切り離した画像レイヤーのサイズを、背景レイヤーのサイズに拡大します。<br>・ **[!UICONTROL レイヤー名]**  — イメージファイル内のレイヤー名の後にPSDの名前を付けます。 例えば、元の PSD ファイルに Price Tag という名前のレイヤーがある場合、Price Tag という名前の画像になります。ただし、PSDファイル内のレイヤー名がデフォルトのPhotoshopレイヤー名（背景、レイヤー 1、レイヤー 2 など）の場合、PSDファイル内のレイヤー番号に基づいてイメージの名前が付けられます。 <br>・ **[!UICONTROL Photoshopとレイヤー番号]**  — イメージファイルのレイヤ番号に従ってPSDに名前を付け、元のレイヤ名は無視します。 Photoshop ファイル名の後にレイヤー番号を付けたものが画像の名前になります。例えば、という名前のファイルの 2 番目のレイヤー `Spring Ad.psd` が `Spring Ad_2` (Photoshopでデフォルト以外の名前が付いていた場合でも )<br>・ **[!UICONTROL Photoshopとレイヤー名]**  — イメージファイルの後にPSDの名前を付け、その後にレイヤ名またはレイヤ番号を付けます。 PSD ファイル内のレイヤー名がデフォルトの Photoshop レイヤー名である場合、レイヤー番号が使用されます。例えば、という名前のレイヤー `Price Tag` 次の名前のPSDファイル内： `SpringAd` が `Spring Ad_Price Tag`. 既定の名前が Layer 2 の画層が呼び出されます。 `Spring Ad_2`. |
| **[!UICONTROL アンカー]** | PSD ファイルから作成されたレイヤーコンポジションから生成されたテンプレートに画像がどのようにアンカーされるのかを指定します。デフォルトで、アンカーは中央です。中央アンカーにより、置換画像の縦横比に関わらず、置換画像で同じ領域をより適切に埋めることができます。この画像を置換する縦横比が異なる画像が、テンプレートの参照時やパラメーターの置き換えの使用時に、同じ領域を効果的に専有します。アプリケーションでテンプレート内の割り当てられた領域を置換画像で埋める必要がある場合、別の設定に変更してください。 |

### 「PDF」タブ {#pdf-tab}

ファイルのラスタライズ、検索語とリンクの抽出、解像度の設定、カラースペースの選択を行うことができます。

| PDFオプション | 説明 |
| --- | --- |
| **[!UICONTROL 処理]** | ・ **[!UICONTROL なし]**  — 処理はおこなわれていないPDFです。<br>・ **[!UICONTROL サムネール]** -PDFファイルの各ページをリッピングし、サムネール画像に変換します。<br> ・ **[!UICONTROL ラスタライズ]** -PDFファイル内のページをリッピングし、ベクトルグラフィックをビットマップ画像に変換します。 eCatalog を作成するには、このオプションを選択します。 |
| **[!UICONTROL 抽出]** | ・ **[!UICONTROL なし]**  — 検索語やリンクは、PDFから抽出されません。<br>・ **[!UICONTROL 検索語]** - eCatalog ビューアでPDFで検索できるように、キーワードファイルから検索語を抽出します。<br>・ **[!UICONTROL リンク]** -PDFファイルからリンクを抽出し、eCatalog ビューアで使用される画像マップに変換します。<br>・ **[!UICONTROL 検索単語とリンク]** - eCatalog ビューアで使用する検索語とリンクの両方を抽出します。 |
| **[!UICONTROL 解像度 (ピクセル/インチ)]** | 解像度設定を決定します。この設定により、PDF ファイル内の 1 inch あたりに表示するピクセル数を決定します。デフォルトは 150 です。 |
| **[!UICONTROL カラースペース]** | ・ **[!UICONTROL 自動検出]** -PDF・ファイルのカラー・スペースを維持します。<br>・ **[!UICONTROL 強制RGB]**  — をRGBのカラースペースに変換します。<br>・ **[!UICONTROL CMYK としてレンダリング]** - CMYK カラースペースに変換します。<br>・ **[!UICONTROL グレースケールとして強制]**  — グレースケールカラースペースに変換します。 |

### Illustratorタブ {#illustrator-tab}

Adobe Illustrator® ファイルのラスタライズ、透明背景の維持、解像度の選択、カラースペースの選択をおこなうことができます。

AdobeDynamic MediaでAdobe® Illustrator® (AI) ファイルを使用できます。 AdobeDynamic Mediaには、アップロード時にこれらのファイルを設定するためのコマンドが用意されています。

Illustrator(AI) 画像ファイルをアップロードする際に、様々な形式で書式設定できます。 ファイルのラスタライズ、透明背景の維持、解像度の選択、カラースペースの選択ができます。PostScript ファイルとIllustratorファイルをフォーマットするためのオプションは、アップロード画面の PostScript オプションとIllustratorオプションの Upload Job Options ボックスで使用できます。


| Illustratorオプション | 説明 |
| --- | --- |
| **[!UICONTROL 処理]** | ラスタライズを選択して、ファイル内のベクターグラフィックスをビットマップ形式に変換します。 |
| **[!UICONTROL レンダリング済みの画像で透明背景色を維持]** | ファイルの背景の透明度を保持します。 |
| **[!UICONTROL 解像度 (ピクセル/インチ)]** | 解像度設定を決定します。この設定により、ファイル内の 1 inch あたりに表示するピクセル数を決定します。 |
| **[!UICONTROL カラースペース]** | ・ **[!UICONTROL 自動検出]**  — ファイルのカラースペースを保持します。<br>・ **[!UICONTROL 強制RGB]**  — をRGBのカラースペースに変換します。<br>・ **[!UICONTROL CMYK としてレンダリング]** - CMYK カラースペースに変換します。<br>・ **[!UICONTROL グレースケールとして強制]**  — グレースケールカラースペースに変換します。 |
