---
title: Dynamic Media の一般設定
description: Dynamic Media で一般設定を管理する方法を説明します。ここで公開先サーバー名と公開元サーバー名を設定し、画像の上書きオプションを設定できます。また、画像のアンシャープマスク用のデフォルトのアップロードオプションや、PostScript、Adobe Photoshop、PDF、Adobe Illustrator の各ファイルを処理する方法に関するアップロードオプションも用意されています。
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
ht-degree: 100%

---

# Dynamic Media の一般設定

<!-- hide: yes
hidefromtoc: yes -->

**[!UICONTROL Dynamic Media 一般設定]** は、次の場合にのみ使用できます。

* Adobe Experience Manager as a Cloud Service の *既存* の **[!UICONTROL Dynamic Media 設定]**（**[!UICONTROL Cloud Services]** 内）を使用している。[Cloud Services での Dynamic Media 設定の作成](/help/assets/dynamic-media/config-dm.md#configuring-dynamic-media-cloud-services) を参照してください。
* 管理者権限を持つ Experience Manager システム管理者である。

Dynamic Media 一般設定は、経験豊富な web サイト開発者やプログラマーが使用することを目的としています。Adobe Dynamic Media では、これらの公開設定を変更するユーザーは、Adobe Experience Manager 上の Dynamic Media と基本的な画像技術に精通していることをお勧めします。

アカウントの作成時に、会社に割り当てられているサーバーが Adobe Dynamic Media によって自動的に提供されます。これらのサーバーは、web サイトとアプリケーションの URL 文字列を生成するのに使用されます。これらの URL 呼び出しは、アカウントに固有です。

Dynamic Media の公開設定ページでは、Adobe Dynamic Media サーバーから web サイトやアプリケーションにアセットを配信する方法を決定するデフォルト設定を指定します。設定が指定されていない場合、Adobe Dynamic Media サーバーは、Dynamic Media 公開設定ページで設定されたデフォルト設定に従ってアセットを配信します。

その他のオプションの設定タスクについては、 [オプション - Dynamic Media 設定のセットアップと設定](/help/assets/dynamic-media/config-dm.md#optional-setup-and-configuration-of-dynamic-media-scene-mode-settings) も参照してください。

>[!NOTE]
>
>Adobe Experience Manager で Dynamic Media Classic から Dynamic Media にアップグレードしますか？Dynamic Media の一般設定ページと [公開設定](/help/assets/dynamic-media/dm-publish-settings.md) ページには、Dynamic Media Classic アカウントから取得した値が事前に入力されています。例外は、一般設定ページの **[!UICONTROL デフォルトのアップロードオプション]** 領域にリストされているすべての値です。これらの値は、Experience Manager に既に存在します。そのため、Experience Manager ユーザーインターフェイスを介して 5 つのタブのいずれかで **[!UICONTROL デフォルトのアップロードオプション]** で行った変更は、Dynamic Media Classic ではなく Dynamic Media に反映されます。一般設定ページと [公開設定](/help/assets/dynamic-media/dm-publish-settings.md) ページの他のすべての設定と値は、Experience Manager の Dynamic Media Classic と Dynamic Media の間で維持されます。

**Dynamic Media の一般設定を指定するには：**

1. Experience Manager 作成者モードで、Experience Manager ロゴを選択して、グローバルナビゲーションコンソールにアクセスします。
1. 左側のパネルで「ツール」アイコンを選択し、**[!UICONTROL アセット]**／**[!UICONTROL Dynamic Media 一般設定]**&#x200B;に移動します。
1. サーバーページで **[!UICONTROL 公開先サーバー名]** と **[!UICONTROL 公開元サーバー名]** を設定し、5 つのタブを使用して、画像編集、Postscript、Photoshop、PDF、Illustrator ファイル用のデフォルトのアップロードオプションを設定します。

   * [サーバー](#server-general-setting)
   * [アプリケーションへのアップロード](#upload-to-application)
   * 「[画像編集](#image-editing-tab)」タブ
   * 「[PostScript](#postscript-tab)」タブ
   * 「[Photoshop](#photoshop-tab)」タブ
   * 「[PDF](#pdf-tab)」タブ
   * 「[Illustrator](#illustrator-tab)」タブ

   ![Dynamic Media 一般設定ページ](/help/assets/assets-dm/dm-general-settings.png)
   *Dynamic Media 一般設定ページ、「**[!UICONTROL 画像編集]**」タブが選択されています。*<br><br>

1. 作業が完了したら、ページの右上隅付近にある「**[!UICONTROL 保存]**」を選択します。

## サーバー {#server-general-setting}

アカウントの作成時に、会社に割り当てられているサーバーが Adobe Dynamic Media によって自動的に提供されます。これらのサーバーは、web サイトとアプリケーションの URL 文字列を生成するのに使用されます。これらの URL 呼び出しは、アカウントに固有です。

| オプション | 説明 |
| --- | --- |
| **[!UICONTROL 公開先サーバー名]** | 必須。<br>名前はパスで `https://` を使用する必要があります。<br>このサーバーは、アカウントに固有のすべてのシステム生成 URL 呼び出しで使用されるライブ CDN（コンテンツ配信ネットワーク）サーバーです。Adobe テクニカルサポートから指示されない限り、このサーバー名は変更しないでください。 |
| **[!UICONTROL 公開元サーバー名]** | 必須。<br>このサーバーは、品質保証テストにのみ使用されます。Adobe テクニカルサポートから指示がない限り、このサーバー名を変更しないでください。 |

## アプリケーションへのアップロード {#upload-to-application}

* **[!UICONTROL 画像を上書き]**

   Adobe Dynamic Media では、2 つのファイルが同じ名前を持つことが許可されません。各項目の Adobe Dynamic Media ID（画像名からファイル名拡張子を取り除いた部分）は一意である必要があります。このルールのため、 **[!UICONTROL アプリケーションへのアップロード]** には上書き機能があります。このオプションの正確な効果は、選択した「画像を上書き」オプションによって異なります。これらのオプションは、置き換える画像のアップロード方法、つまり元の画像を置き換えるか、重複させるかを指定します。重複する画像の名前は `-1` に変更されます。例えば、`chair.tif` の名前は `chair-1.tif` に変更されます。これらのオプションは、元の画像とは別のフォルダーにアップロードされる画像や、元の画像と異なるファイル名拡張子（JPG、TIF、PNG など）を持つ画像に影響を与えます。

   >[!NOTE]
   >
   >Experience Manager との一貫性を維持するには、「画像を上書き」オプションの **[!UICONTROL 現在のフォルダーにあるベース名と拡張子が同じファイルを上書き]** を選択します。

   | 「画像を上書き」オプション | 説明 |
   | --- | --- |
   | **[!UICONTROL 現在のフォルダーにあるベース名と拡張子が同じファイルを上書き]** | 新しい Dynamic Media アカウントのみ *デフォルト*。<br>このオプションは、置き換えの最も厳しいルールです。 置き換え画像を元の画像と同じフォルダーにアップロードし、置き換え画像と元の画像のファイル名拡張子が同じになっている必要があります。これらの要件が満たされない場合は、重複する画像が作成されます。<br>*Experience Manager との一貫性を維持するには、このオプションを選択します*。 |
   | **[!UICONTROL 現在のフォルダーにある、ベース名が同じファイルを拡張子に関わらず上書き]** | 置き換え画像を元の画像と同じフォルダーにアップロードする必要がありますが、ファイル名の拡張子は元の画像と異なっても構いません。例えば、chair.tif は chair.jpg と置き換えます。 |
   | **[!UICONTROL 任意のフォルダーにある、ベース名と拡張子が同じファイルを上書き]** | 置き換え画像のファイル名の拡張子が元の画像と同じである必要があります（例えば、chair.jpg は chair.tif ではなく chair.jpg と置き代わる必要があります）。ただし、置き換え画像を、元の画像と別のフォルダーにアップロードできます。更新された画像は新しいフォルダーにあり、元の場所のファイルはなくなります。 |
   | **[!UICONTROL 任意のフォルダーにある、ベース名が同じファイルを拡張子に関わらず上書き]** | このオプションは、最も包括的な置き換えルールです。 置き換え画像を、元の画像と別のフォルダーにアップロードでき、ファイル名の拡張子が異なるファイルをアップロードして、元のファイルと置き換えることができます。元のファイルが別のフォルダーにある場合、置き換え画像は、アップロード先の新しいフォルダーに存在します。 |

* **[!UICONTROL 切り抜きを保持]**

   既存の手動切り抜き定義の保存を制御します。

   Dynamic Media ビューアリファレンスガイドの [UploadPostJob](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-production-api/data-types/r-upload-post-job.html?lang=ja) および [ReprocessAssetsJob](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-production-api/data-types/r-reprocess-assets-job.html?lang=ja) の `preserveCrop` も参照してください。

## デフォルトのアップロードオプション {#default-upload-options}

### 「画像編集」タブ {#image-editing-tab}

このフィルターを使用すると、ダウンサンプリングされた最終的な画像に対するシャープフィルター効果を微調整できます。効果の強さ、効果の半径（ピクセル単位）、無視されるコントラストのしきい値を制御するのに役立ちます。

アンシャープマスク効果では、Photoshop のアンシャープマスクフィルターと同じオプションが使用されます。名前から連想される機能と違い、アンシャープマスクとはシャープニングフィルターのことです。

| 「アンシャープマスク」オプション | 説明 |
| --- | --- |
| **[!UICONTROL 量]** | 必須。<br>端のピクセルに適用するコントラストの量を制御します。<br>この量は、効果の強さと考えることができます。Adobe Dynamic Media での「アンシャープマスク」の値と Adobe Photoshop の値の主な違いは、Photoshop では値の範囲が 1% ～ 500% である点です。一方、Adobe Dynamic Media では、値の範囲は `0.0` から `5.0` です。Adobe Dynamic Media の値が 5.0 の場合、おおよそ Photoshop の 500% に相当します。値が 0.9 の場合は 90% に相当します。 |
| **[!UICONTROL 半径]** | 必須。<br>効果の半径を制御します。<br>値の範囲は `0` ～ `250` です。効果は画像内の全ピクセルに切れ目なく続き、すべてのピクセルから全方向に放射されます。半径の単位はピクセルです。例えば、2000 x 2000 ピクセルの画像と 500 x 500 ピクセルの画像で同様のシャープ効果を得るには、2000 x 2000 ピクセルの画像で 2 ピクセルの半径を設定します。次に、500 x 500 ピクセルの画像上で 1 ピクセルの半径値を設定します。ピクセル数の多い画像には大きい値を使用します。 |
| **[!UICONTROL しきい値]** | 必須。<br>しきい値とは、アンシャープマスクフィルターの適用時に無視されるコントラストの範囲です。このフィルターの使用中に画像に「ノイズ」が加わるのを防ぐために重要です。値の範囲は `0` ～ `255` で、グレースケール画像の明るさのステップ数です。`0`=黒、`128`=50% グレー、`255`=白です。<br>例えば、しきい値の値を `12` にした場合、肌のトーンの明るさにわずかな差があっても無視してノイズが加わるのを防ぎながら、まつげと肌が隣り合う場所など、コントラストの高い領域に対してエッジコントラストを追加することができます。<br>人の顔写真であれば、アンシャープマスクは画像のコントラストが強い部分に作用します。例えば、まつ毛と肌の境目でコントラストが強く出る部分や、なめらかな肌そのものの部分などです。非常に滑らかな肌でも、明るさの値はわずかに変化しています。しきい値を使用しないと、このフィルターはこのような肌部分のピクセルのわずかな変化を強調します。同様に、まつげのコントラストを強めてシャープさを強調し、ノイズのある望ましくない効果を生み出してしまいます。<br>しきい値はこの問題を解決するために導入されたものであり、なめらかな肌のようにコントラストが大きく変化しないピクセルは無視するようフィルターに指示します。<br>先ほど示したファスナーのグラフィックで、ファスナーの横の生地に注目してください。しきい値が低すぎてノイズを抑制できなかったので、画像ノイズが発生しています。 |
| **[!UICONTROL モノクロ]** | 選択すると、画像の明るさ（強さ）にアンシャープマスクが適用されます。<br>選択を解除すると、それぞれの色成分に別々にアンシャープマスクが適用されます。 |

[Adobe Dynamic Media および Image Server での画像のシャープニング](https://experienceleague.adobe.com/docs/experience-manager-65/assets/sharpening_images.pdf?lang=ja) も参照してください。

### 「PostScript」タブ {#postscript-tab}

Adobe PostScript® ファイルのラスタライズ、透明背景の維持、解像度の選択、カラースペースの選択を行うことができます。

Adobe PostScript®（EPS）ファイルは、Adobe Dynamic Media で使用できます。Adobe Dynamic Media には、アップロード時にこれらのファイルを設定するためのコマンドが用意されています。

PostScript（EPS）画像ファイルのアップロード時に、様々な方法でファイルをフォーマットできます。ファイルのラスタライズ、透明背景の維持、解像度の選択、カラースペースの選択ができます。

| 「PostScript」オプション | 説明 |
| --- | --- |
| **[!UICONTROL 処理]** | ラスタライズを選択して、ファイル内のベクターグラフィックスをビットマップ形式に変換します。 |
| **[!UICONTROL レンダリング済みの画像で透明な背景を維持]** | ファイルの背景の透明度を維持します。 |
| **[!UICONTROL 解像度（ピクセル／インチ）]** | 解像度設定を決定します。この設定により、ファイル内の 1 inch あたりに表示するピクセル数を決定します。 |
| **[!UICONTROL カラースペース]** | • **[!UICONTROL 自動検出]** - ファイルのカラースペースを保持します。<br>• **[!UICONTROL RGB として強制]** - RGB カラースペースに変換します。<br>• **[!UICONTROL CMYK として強制]** - CMYK カラースペースに変換します。<br>• **[!UICONTROL グレースケールとして強制]** - グレースケールカラースペースに変換します。 |

### 「Photoshop」タブ {#photoshop-tab}

Adobe® Photoshop® ファイルからのテンプレート作成、レイヤーの維持、レイヤーの命名方法の指定、テキストの抽出、テンプレートへの画像のアンカー方法の指定を行うことができます。

| 「Photoshop」オプション | 説明 |
| --- | --- |
| **[!UICONTROL レイヤーを維持]** | PSD にレイヤーがあれば切り離して個別のアセットにします。アセットレイヤーは PSD に関連付けられたまま維持されます。詳細ビューで PSD ファイルを開き、レイヤーパネルを選択すると、これらを確認できます。PSD ファイルでのレイヤーの表示と編集を参照してください。 |
| **[!UICONTROL テンプレートを作成]** | PSD ファイル内のレイヤーからテンプレートを作成します。 |
| **[!UICONTROL テキストを抽出]** | テキストを抽出して、ユーザーがビューア内でテキストを検索できるようにします。 |
| **[!UICONTROL レイヤーを背景サイズに拡大]** | 切り離した画像レイヤーのサイズを、背景レイヤーのサイズに拡大します。 |
| **[!UICONTROL レイヤーの命名]** | 切り離した画像レイヤーのサイズを、背景レイヤーのサイズに拡大します。<br>• **[!UICONTROL レイヤー名]** - PSD ファイル内のレイヤー名に従って画像に名前を付けます。例えば、元の PSD ファイルに Price Tag という名前のレイヤーがある場合、Price Tag という名前の画像になります。ただし、PSD ファイル内のレイヤー名がデフォルトの Photoshop レイヤー名（背景、レイヤー 1、レイヤー 2 など）である場合、画像の名前は PSD ファイル内のレイヤー番号に従って付けられます。<br>• **[!UICONTROL Photoshop とレイヤー番号]** - PSD ファイル内のレイヤー番号に従って画像の名前を付け、元のレイヤー名は無視します。Photoshop ファイル名の後にレイヤー番号を付けたものが画像の名前になります。例えば、`Spring Ad.psd` というファイルの 2 番目のレイヤーは、Photoshop でデフォルト以外の名前が付いていたとしても `Spring Ad_2` という名前になります。<br>• **[!UICONTROL Photoshop とレイヤー名]** - PSD ファイルの後にレイヤー名またはレイヤー番号を付けた名前になります。PSD ファイル内のレイヤー名がデフォルトの Photoshop レイヤー名である場合、レイヤー番号が使用されます。例えば、`SpringAd` という名前の PSD ファイルに `Price Tag` という名前のレイヤーがある場合、`Spring Ad_Price Tag` という名前になります。レイヤー 2 というデフォルト名のレイヤーは `Spring Ad_2` となります。 |
| **[!UICONTROL アンカー]** | PSD ファイルから作成されたレイヤーコンポジションから生成されたテンプレートに画像がどのようにアンカーされるのかを指定します。デフォルトで、アンカーは中央です。中央アンカーにより、置換画像の縦横比に関わらず、置換画像で同じ領域をより適切に埋めることができます。この画像を置換する縦横比が異なる画像が、テンプレートの参照時やパラメーターの置き換えの使用時に、同じ領域を効果的に専有します。アプリケーションでテンプレート内の割り当てられた領域を置換画像で埋める必要がある場合、別の設定に変更してください。 |

### 「PDF」タブ {#pdf-tab}

ファイルのラスタライズ、検索語とリンクの抽出、解像度の設定、カラースペースの選択を行うことができます。

| 「PDF」オプション | 説明 |
| --- | --- |
| **[!UICONTROL 処理]** | • **[!UICONTROL なし]** - PDF の処理は行われません。<br>• **[!UICONTROL サムネール]** - PDFファイルの各ページをリッピングし、サムネール画像に変換します。<br> • **[!UICONTROL ラスタライズ]** - PDF ファイルのページをリッピングし、ベクターグラフィックスをビットマップ画像に変換します。eCatalog を作成するには、このオプションを選択します。 |
| **[!UICONTROL 抽出]** | • **[!UICONTROL なし]** - 検索語やリンクは、PDFから抽出されません。<br>• **[!UICONTROL 検索語]** - PDF ファイルから検索語を抽出し、eCatalog ビューア内でこのファイルをキーワード検索できるようにします。<br>• **[!UICONTROL リンク]** - PDF ファイルからリンクを抽出し、eCatalog ビューアで使用できる画像マップに変換します。<br>• **[!UICONTROL 検索語とリンク]** - eCatalog ビューアで使用する検索語とリンクの両方を抽出します。 |
| **[!UICONTROL 解像度（ピクセル／インチ）]** | 解像度設定を決定します。この設定により、PDF ファイル内の 1 inch あたりに表示するピクセル数を決定します。デフォルトは 150 です。 |
| **[!UICONTROL カラースペース]** | • **[!UICONTROL 自動検出]** - PDF ファイルのカラースペースを維持します。<br>• **[!UICONTROL RGB として強制]** - RGB カラースペースに変換します。<br>• **[!UICONTROL CMYK として強制]** - CMYK カラースペースに変換します。<br>• **[!UICONTROL グレースケールとして強制]** - グレースケールカラースペースに変換します。 |

### 「Illustrator」タブ {#illustrator-tab}

Adobe Illustrator® ファイルのラスタライズ、透明背景の維持、解像度の選択、カラースペースの選択を行うことができます。

Adobe Dynamic Media で Adobe® Illustrator®（AI）のファイルを使用できます。Adobe Dynamic Media には、アップロード時にこれらのファイルを設定するためのコマンドが用意されています。

Illustrator（AI）画像ファイルのアップロード時に、様々な方法でファイルをフォーマットできます。ファイルのラスタライズ、透明背景の維持、解像度の選択、カラースペースの選択ができます。PostScript ファイルと Illustrator ファイルをフォーマットするためのオプションは、アップロード画面の PostScript オプションと Illustrator オプションの「アップロードジョブオプション」ボックスで使用できます。


| 「Illustrator」オプション | 説明 |
| --- | --- |
| **[!UICONTROL 処理]** | ラスタライズを選択して、ファイル内のベクターグラフィックスをビットマップ形式に変換します。 |
| **[!UICONTROL レンダリング済みの画像で透明な背景を維持]** | ファイルの背景の透明度を維持します。 |
| **[!UICONTROL 解像度（ピクセル／インチ）]** | 解像度設定を決定します。この設定により、ファイル内の 1 inch あたりに表示するピクセル数を決定します。 |
| **[!UICONTROL カラースペース]** | • **[!UICONTROL 自動検出]** - ファイルのカラースペースを保持します。<br>• **[!UICONTROL RGB として強制]** - RGB カラースペースに変換します。<br>• **[!UICONTROL CMYK として強制]** - CMYK カラースペースに変換します。<br>• **[!UICONTROL グレースケールとして強制]** - グレースケールカラースペースに変換します。 |
