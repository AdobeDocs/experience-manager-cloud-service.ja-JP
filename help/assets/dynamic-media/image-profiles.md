---
title: Dynamic Media 画像プロファイル
description: アンシャープマスクの設定、スマート切り抜きとスマートスウォッチのいずれかまたは両方の設定を含む Dynamic Media 画像プロファイルを作成する方法について説明します。次に、画像アセットのフォルダーにプロファイルを適用します。
contentOwner: Rick Brough
feature: Asset Management,Image Profiles,Renditions,Best Practices
role: User
exl-id: 0856f8a1-e0a9-4994-b338-14016d2d67bd
source-git-commit: c82f84fe99d8a196adebe504fef78ed8f0b747a9
workflow-type: tm+mt
source-wordcount: '3564'
ht-degree: 99%

---

# Dynamic Media 画像プロファイル {#image-profiles}

<table>
    <tr>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i> 新規 </i></sup>Dynamic Media Prime<a href="/help/assets/dynamic-media/dm-prime-ultimate.md"><b>Ultimate</b></a>
        </td>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i> 新規 </i></sup> <a href="/help/assets/assets-ultimate-overview.md"><b>AEM AssetsUltimate</b></a>
        </td>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i> 新規 </i></sup> <a href="/help/assets/integrate-aem-assets-edge-delivery-services.md"><b>AEM AssetsとEdge Delivery Servicesの統合 </b></a>
        </td>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i> 新規 </i></sup><a href="/help/assets/aem-assets-view-ui-extensibility.md"><b>UI 拡張機能 </b></a>
        </td>
          <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>Dynamic Media Prime</i></sup>Ultimateの新 <a href="/help/assets/dynamic-media/enable-dynamic-media-prime-and-ultimate.md"><b> 能 </b></a>
        </td>
    </tr>
    <tr>
        <td>
            <a href="/help/assets/search-best-practices.md"><b>検索のベストプラクティス</b></a>
        </td>
        <td>
            <a href="/help/assets/metadata-best-practices.md"><b>メタデータのベストプラクティス</b></a>
        </td>
        <td>
            <a href="/help/assets/product-overview.md"><b>コンテンツハブ</b></a>
        </td>
        <td>
            <a href="/help/assets/dynamic-media-open-apis-overview.md"><b>OpenAPI 機能を備えた Dynamic Media</b></a>
        </td>
        <td>
            <a href="https://developer.adobe.com/experience-cloud/experience-manager-apis/"><b>AEM Assets 開発者向けドキュメント</b></a>
        </td>
    </tr>
</table>

画像をアップロードするときに、フォルダーにイメージプロファイルを適用することで、アップロード時に自動的に画像を切り抜くことができます。

>[!IMPORTANT]
>
>画像プロファイルは、PDF ファイル、アニメーション GIF ファイル、INDD（Adobe InDesign）ファイルには適用されません。

## 「アンシャープマスク」オプション {#unsharp-mask}

画像プロファイルを作成する場合は、「**[!UICONTROL アンシャープマスク]**」オプションを使用すると、最終的なダウンサンプリングに対する画像のシャープニングフィルター効果を微調整できます。エフェクトの強さ、エフェクトの半径（ピクセル単位）、無視されるコントラストのしきい値を調整できます。このエフェクトは、Adobe Photoshop の「アンシャープマスク」フィルターと同じオプションを使用します。

>[!NOTE]
>
>アンシャープマスクは、PTIFF（Pyramid TIFF）内のダウンスケールされたレンディション（50％以上ダウンサンプルされたもの）にのみ適用されます。アンシャープマスクは、ptiff 内の最大サイズのレンディションには影響しません。一方、サムネールなど、小さいサイズのレンディションは変更されます（アンシャープマスクが表示されます）。

「**[!UICONTROL アンシャープマスク]**」には次のフィルタリングオプションがあります。

<table>
 <tbody>
  <tr>
   <td><strong>オプション</strong></td>
   <td><strong>説明</strong></td>
  </tr>
  <tr>
   <td>量</td>
   <td>端のピクセルに適用されるコントラストの量を制御します。デフォルトは 1.75 です。高解像度の画像の場合は、最大で 5 まで増やすことができます。この量は、フィルターの強さを表す尺度と考えてください。範囲は 0～5 です。</td>
  </tr>
  <tr>
   <td>半径</td>
   <td>シャープに作用する端のピクセル周辺のピクセル数を決定します。高解像度の画像の場合は、1～2 を入力します。小さい値は端のピクセルのみをシャープにし、大きい値は広範囲のピクセルをシャープにします。適切な値は画像のサイズによって異なります。デフォルト値は 0.2 で、範囲は 0～250 です。</td>
  </tr>
  <tr>
   <td>しきい値</td>
   <td><p>アンシャープマスクフィルターが適用される場合のコントラストの範囲を指定します。このオプションは、エッジのピクセルと見なされるために、シャープが適用されるピクセルが周囲のピクセルとどの程度異なる必要があるかを制御します。このしきい値を満たすピクセルのみにシャープが適用されます。ノイズが入らないように、0～255 の範囲で様々な整数値を試してください。</p> </td>
  </tr>
 </tbody>
</table>

シャープニングについては、[画像のシャープニング](/help/assets/dynamic-media/assets/sharpening_images.pdf)を参照してください。

## 切り抜きツールオプション {#crop-options}

画像にスマート切り抜きを実装する場合、アドビでは次のベストプラクティスを推奨し、次の制限を適用します。

| アセット - 制限タイプ | ベストプラクティス | 適用される制限 |
| --- | --- | --- |
| **画像** - 画像あたりのスマート切り抜き数 | 5 | 100 |

[Dynamic Media の制限](/help/assets/dynamic-media/limitations.md)も参照してください。

<!-- CQDOC-16069 for the paragraph directly below -->

スマート切り抜きの座標は、アスペクト比に応じて異なります。イメージプロファイルのスマート切り抜き設定で、イメージプロファイルに追加されたサイズの縦横比が同じ場合縦横比が Dynamic Media に送信されます。アドビでは、同じ切り抜き領域を使用することを推奨します。そうすれば、イメージプロファイルで使用される様々なサイズに影響を与えません。

スマート切り抜きを生成するたびに、追加の処理が必要になります。例えば、スマート切り抜きのアスペクト比を 6 つ以上追加すると、アセット取り込み速度が遅くなる可能性があります。また、システムの負荷が増大するおそれもあります。スマート切り抜きはフォルダーレベルで適用できるので、アドビでは必要なフォルダーにのみ使用することをお勧めします。

**画像プロファイルでのスマート切り抜きの定義に関するガイドライン**
スマート切り抜きの使用状況を制御し、切り抜きの処理時間や保存を最適化するには、アドビでは次のガイドラインとヒントを推奨します。

* スマート切り抜きを適用する画像アセットは、少なくとも 50 x 50 ピクセル以上である必要があります。
* 画像あたり 10～15 個のスマート切り抜きを行い、画面の比率と処理時間に合わせて最適化するのが理想的です。
* 最終的な用途ではなく、切り抜きのサイズに基づいてスマート切り抜きに名前を付けます。これにより、単一のディメンションが複数のページで使用される重複を最適化するのに役立ちます。
* すべてのフォルダーやアセットに適用される共通のスマート切り抜きプロファイルではなく、個別のフォルダーやサブフォルダーを対象とするページやアセットタイプごとの画像プロファイルを作成します。
* サブフォルダーに適用した画像プロファイルは、フォルダーに適用した画像プロファイルより優先されます。
* 重複したスマート切り抜きのサイズを含むイメージプロファイルは許可されていません。
* スマート切り抜きオプションが設定されている名前付きイメージプロファイルの重複は、許可されていません。

2 つの画像切り抜きオプション（ピクセル切り抜きとスマート切り抜き）から選択できます。また、カラーおよび画像スウォッチの作成を自動化するか、ターゲットの解像度をまたいで切り抜きコンテンツを保持するかを選択することもできます。

>[!IMPORTANT]
>
>アドビでは、生成される切り抜きやスウォッチを確認し、これらが適切であり、ブランドと価値に関連していることを確認することをお勧めします。

| オプション | 用途 | 説明 |
| --- | --- | --- |
| **[!UICONTROL ピクセル切り抜き]** | 画像サイズにのみ基づいて画像を一括で切り抜きます。 | **[!UICONTROL 切り抜きオプション]** ドロップダウンリストから、「**[!UICONTROL ピクセル切り抜き]**」を選択します。<br>画像の各辺から切り抜くには、画像の任意の辺または四辺からの切り抜きのサイズ（ピクセル数）を入力します。画像がどれだけ切り抜かれるかは、画像ファイル内の ppi（1 インチあたりのピクセル数）の設定によって変わります。<br>画像プロファイルのピクセル切り抜きは次の方法で実行されます。画像プロファイルのピクセル切り抜きは、次のようにレンダリングされます。<br>• 値は「上」、「下」、「左」、「右」です。<br>・左上が `0,0` と見なされ、そこからピクセル切り抜きが計算されます。<br>・切り抜きの開始点：左は X、上は Y<br>・水平方向の計算：元の画像の水平方向のピクセルサイズから「左」を引いた後、「右」を引いた値。<br>・垂直方向の計算：垂直方向の高さ（ピクセル）から「上」と「下」を差し引きます。<br>例えば、4000 x 3000 ピクセルの画像があるとします。値として「上」= 250、「下」= 500、「左」= 300、「右」= 700 を使用します。<br>左上 (300,250) から、(4000-300-700, 3000-250-500) つまり (3000,2250) のフィルスペースを使って切り抜きます。 |
| **[!UICONTROL スマート切り抜き]** | 視焦点位置に基づいて画像を一括で切り抜きます。 | スマート切り抜きでは、Adobe Sensei の人工知能の力を活用して、自動的に画像を一括ですばやく切り抜きます。画面サイズに関係なく、あらゆる画像の焦点位置を自動的に検出して切り抜き、目的の箇所を取得します。<br>「**[!UICONTROL 切り抜きオプション]**」ドロップダウンリストで、「**[!UICONTROL スマート切り抜き]**」を選択し、「**[!UICONTROL レスポンシブ画像の切り抜き]**」の右側で、この機能を有効（オン）にします。<br>デフォルトのブレークポイントサイズ（**[!UICONTROL 大]**、**[!UICONTROL 中]**、**[!UICONTROL 小]**）は、ほとんどの画像がモバイルやタブレットデバイス、デスクトップ、バナーで使用されるサイズをすべてカバーしています。大、中、小のデフォルト値は、必要に応じて編集できます。<br>ブレークポイントを追加するには、「**[!UICONTROL 切り抜きを追加]**」を選択します。切り抜きを削除するには、ごみ箱アイコンを選択します。 |
| **[!UICONTROL カラーおよび画像スウォッチ]** | 各画像の画像スウォッチを一括で生成します。 | **注意**：Dynamic Media Classic ではスマートスウォッチはサポートされません。<br>商品画像から色やテクスチャを示す高品質のスウォッチを自動的に検出して生成します。<br>「**[!UICONTROL 切り抜きオプション]**」ドロップダウンリストで、「**[!UICONTROL スマート切り抜き]**」を選択します。 次に、 **[!UICONTROL カラーおよび画像スウォッチ]** の右側で、この機能を有効（オン）にします。「**[!UICONTROL 幅]**」と「**[!UICONTROL 高さ]**」テキストフィールドにピクセル値を入力します。<br>画像の切り抜きはすべてレンディションパネルから使用できますが、スウォッチを使用するには **[!UICONTROL URL のコピー]** 機能を利用しなければなりません。独自のビューコンポーネントを使用して、サイトにスウォッチをレンダリングします。カルーセルバナーはこのルールの例外です。カルーセルバナーで使用されるスウォッチについては、Dynamic Media が表示コンポーネントを提供します。<br><br>**画像スウォッチの使用**<br>&#x200B;画像スウォッチの URL は簡単です。<br>`/is/image/company/&lt;asset_name&gt;:Swatch`<br>ここで、`:Swatch` がアセットリクエストに追加されます。<br><br>**カラースウォッチの使用**<br>&#x200B;カラースウォッチを使用するには、次のように `req=userdata` リクエストを行います。<br>`/is/image/&lt;company_name&gt;/&lt;swatch_asset_name&gt;:Swatch?req=userdata`<br><br>例えば、Dynamic Media Classic のスウォッチアセットは次のとおりです。<br>`https://my.company.com:8080/is/image/DemoCo/Sleek:Swatch`<br>そして、これがスウォッチアセットの対応する `req=userdata` URLです。<br>`https://my.company.com:8080/is/image/DemoCo/Sleek:Swatch?req=userdata`<br>`req=userdata` の応答は次のとおりです。<br>`SmartCropDef=Swatch`<br>`SmartCropHeight=200.0`<br>`SmartCropRect=0.421671,0.389815,0.0848564,0.0592593,200,200`<br>`SmartCropType=Swatch`<br>`SmartCropWidth=200.0`<br>`SmartSwatchColor=0xA56DB2`<br>次のそれぞれの URL の例のように、XML または JSON 形式で `req=userdata` 応答を要求することもできます。<br>•`https://my.company.com</code>:8080/is/image/DemoCo/Sleek:Swatch?req=userdata,json`<br>•`https://my.company.com:8080/is/image/DemoCo/Sleek:Swatch?req=userdata,xml`<br><br>**注意**：カラースウォッチを要求し、24 ビット RGB 16 進値で表される `SmartSwatchColor` 属性を解析するには、独自の WCM コンポーネントを作成する必要があります。<br>ビューアリファレンスガイドの「[`userdata`](https://experienceleague.adobe.com/ja/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/http-protocol-reference/command-reference/req/r-userdata)」も参照してください。 |
| **[!UICONTROL ターゲット解像度全体で切り抜きコンテンツを保持する]** | 同じ縦横比で切り抜きコンテンツを維持するには | スマート切り抜きプロファイルを作成する際に使用します。<br>様々な解像度の特定の縦横比に対して、焦点を維持したまま、新しい切り抜きコンテンツを生成するには、このオプションのチェックを外します<br>このチェックボックスをオフにする場合は、元の画像の解像度が、スマート切り抜きプロファイルに定義した解像度よりも大きいことを確認します。<br><br>例えば、縦横比を 600 x 600（大）、400 x 400（中）、300 x 300（小）に設定したとします。<br>「**[!UICONTROL ターゲット解像度全体で切り抜きコンテンツを保持する]**」オプションを&#x200B;*オン*&#x200B;にすると、次の画像の出力例のように、3 つの解像度すべてで同じ切り抜きが表示されます（説明のみを目的としています）。<br>![オプションがオン](/help/assets/dynamic-media/assets/preserve-checked.png)<br><br>「**[!UICONTROL ターゲット解像度全体で切り抜きコンテンツを保持する]**」オプションを&#x200B;*オフ*&#x200B;にすると、次の画像の出力例のように、3 つの解像度すべてで切り抜きコンテンツが新しくなります（説明のみを目的としています）。<br>![オプションがオフ](/help/assets/dynamic-media/assets/preserve-unchecked.png) |

### スマート切り抜きとカラースウォッチでサポートされる画像ファイル形式

サポートされる入力ファイルの最大サイズ解像度は 16K です。

>[!NOTE]
>
>16K 解像度は、水平方向に約 16,000 ピクセルのディスプレイ解像度です。最も一般的に取り上げられる 16K 解像度は 15360 × 8640 ピクセルで、これは各次元の 8K UHD のピクセル数を 2 倍にし、合計で 4 倍のピクセル数になります。この解像度は 132.7 メガピクセルで、4K 解像度の 16 倍、1080p 解像度の 64 倍のピクセル数になります。

| 画像の形式 | 大文字と小文字を区別しないファイル拡張子 | MIME タイプ | サポートされる入力カラースペース | サポートされる入力ファイルの最大サイズ | サポートされる画像の形式？ |
| --- | --- | --- | --- | --- | --- |
| BMP | `.bmp` | image/bmp | sRGB | 4 GB | はい |
| CMYK | | | | | はい |
| EPS | | | | | いいえ |
| GIF | `.gif` | image/gif | sRGB | 15 GB | 対応。レンディションには、アニメーション GIF の最初のフレームが使用されます。最初のフレームは設定または変更できません。 |
| JPEG | `.jpg` および `.jpeg` | image/jpeg | sRGB | 15 GB | はい |
| PNG | `.png` | image/png | sRGB | 15 GB | はい |
| PSD | `.psd` | image/vnd.adobe.photoshop | sRGB<br>CMYK | 2 GB | はい |
| SVG | | | | | いいえ |
| TIFF | `.tif` および `.tiff` | image/tiff | sRGB<br>CMYK | 4 GB | はい |
| WebP／アニメーション WebP | | | | | いいえ |

## Dynamic Media イメージプロファイルの作成 {#creating-image-profiles}

他のアセットタイプへの高度な処理パラメーターの定義については、[アセット処理の設定](config-dm.md#configuring-asset-processing)を参照してください。

詳しくは、[Dynamic Media のイメージプロファイルとビデオプロファイルについて](/help/assets/dynamic-media/about-image-video-profiles.md)を参照してください。

[処理プロファイルを使用するためのデジタルアセットの編成のベストプラクティス](/help/assets/organize-assets.md)を参照してください。

**Dynamic Media 画像プロファイルを作成するには**：

1. Adobe Experience Manager のロゴを選択し、**[!UICONTROL ツール]**／**[!UICONTROL Assets]**／**[!UICONTROL 画像プロファイル]**&#x200B;に移動します。
1. 画像プロファイルを追加するには、「**[!UICONTROL 作成]**」を選択します。
1. プロファイル名を入力し、アンシャープマスクのほか、切り抜きとスウォッチのいずれかまたは両方の値を入力します。

   >[!TIP]
   >
   >目的に沿ったプロファイル名を使用します。例えば、スウォッチのみを生成するプロファイルを作成するとします。つまり、スマート切り抜きは無効（オフ）に、カラーと画像スウォッチは有効（オン）になります。このような場合は、「スマートスウォッチ」というプロファイル名を使用できます。

   [スマート切り抜きとスマートスウォッチオプション](#crop-options) および [アンシャープマスク](#unsharp-mask) も参照してください。

   ![切り抜き](assets/crop.png)

1. 「**[!UICONTROL 保存]**」を選択します。作成したプロファイルが、使用可能なプロファイルのリストに表示されます。

## Dynamic Media イメージプロファイルの編集または削除 {#editing-or-deleting-image-profiles}

1. Experience Manager ロゴを選択し、**[!UICONTROL ツール]**／**[!UICONTROL Assets]**／**[!UICONTROL 画像プロファイル]**&#x200B;に移動します。
1. 編集または削除する画像プロファイルを選択します。編集するには、「**[!UICONTROL 画像処理プロファイルを編集]**」を選択します。削除するには、「**[!UICONTROL 画像処理プロファイルを削除]**」を選択します。

   ![chlimage_1-254](assets/chlimage_1-254.png)

1. 編集する場合は、変更を保存します。削除する場合は、プロファイルの削除を確定します。

## フォルダーへの Dynamic Media イメージプロファイルの適用 {#applying-an-image-profile-to-folders}

フォルダーに画像プロファイルを割り当てると、サブフォルダーは自動的に親フォルダーのプロファイルを継承します。したがって、1 つのフォルダーに割り当てることができる画像プロファイルは 1 つのみになります。そのため、アセットをアップロード、保存、使用およびアーカイブする場所のフォルダー構造については入念に検討してください。

フォルダーに異なるイメージプロファイルを割り当てた場合、新しいプロファイルが以前のプロファイルよりも優先されます。以前に存在していたフォルダーのアセットは変更されずに維持されます。新しいプロファイルは、その後にフォルダーに追加されるアセットに対して適用されます。

プロファイルが割り当てられているフォルダーには、カードにプロファイルの名前が表示されます。

<!-- When you add smart crop to an existing Image Profile, you need to re-trigger the [DAM Update Asset workflow](assets-workflow.md) if you want to generate crops for existing assets in your asset repository. -->

イメージプロファイルは、特定のフォルダーに適用することも、全アセットにグローバルに適用することもできます。

後で変更した既存のイメージプロファイルが存在するフォルダー内のアセットを再処理できます。[処理プロファイルを編集した後のフォルダー内のアセットの再処理](/help/assets/dynamic-media/about-image-video-profiles.md#reprocessing-assets)を参照してください。

### 特定フォルダーへの Dynamic Media イメージプロファイルの適用 {#applying-image-profiles-to-specific-folders}

**[!UICONTROL ツール]**&#x200B;メニュー内から（またはフォルダー内にいる場合は「**[!UICONTROL プロパティ]**」から）、特定のフォルダーにイメージプロファイルを適用できます。

プロファイルが割り当てられているフォルダーには、フォルダー名のすぐ下にプロファイルの名前が表示されます。

後で変更した既存のビデオプロファイルが存在するフォルダー内のアセットを再処理できます。[処理プロファイルを編集した後のフォルダー内のアセットの再処理](/help/assets/dynamic-media/about-image-video-profiles.md#reprocessing-assets)を参照してください。

#### プロファイルユーザーインターフェイスを使用したフォルダーへの Dynamic Media イメージプロファイルの適用 {#applying-image-profiles-to-folders-from-profiles-user-interface}

1. Experience Manager ロゴを選択し、**[!UICONTROL ツール]**／**[!UICONTROL Assets]**／**[!UICONTROL 画像プロファイル]**&#x200B;に移動します。
1. 1 つ以上のフォルダーに適用するイメージプロファイルを選択します。

   ![chlimage_1-255](assets/chlimage_1-255.png)

1. 「**[!UICONTROL 処理プロファイルをフォルダーに適用]**」を選択し、新しくアップロードされたアセットの保存先となるフォルダーを 1 つ以上選択し、「**[!UICONTROL 適用]**」をクリックします。プロファイルが割り当てられているフォルダーには、フォルダー名のすぐ下にプロファイルの名前が表示されます。

#### プロパティを使用したフォルダーへの Dynamic Media イメージプロファイルの適用 {#applying-image-profiles-to-folders-from-properties}

1. Experience Manager のロゴを選択し、**[!UICONTROL アセット]**&#x200B;に移動します。
1. イメージプロファイルを適用する&#x200B;*フォルダー*（アセットではない）に移動します。
1. 現在の表示に応じて、次のいずれかの操作を行います。
   * カード表示では、フォルダーの上にポインターを置き、チェックマークを選択してフォルダーを選択します。
   * 列表示またはリスト表示では、フォルダー名の左側にあるチェックボックスを選択します。
1. ツールバーの「**[!UICONTROL プロパティ]**」を選択します。
1. 「**[!UICONTROL Dynamic Media 処理]**」タブを選択します。
1. **[!UICONTROL イメージプロファイル]** の下で、適用するプロファイルを「**[!UICONTROL プロファイル名]**」ドロップダウンリストから選択します。
1. ページの右上隅付近にある「**[!UICONTROL 保存して閉じる]**」を選択します。プロファイルが割り当てられているフォルダーには、フォルダー名のすぐ下にプロファイルの名前が表示されます。

   ![chlimage_1-256](assets/chlimage_1-256.png)

### Dynamic Media イメージプロファイルグローバルな適用 {#applying-an-image-profile-globally}

1 つのフォルダーに 1 つのプロファイルを適用する以外に、1 つをグローバルに適用することもできます。任意のフォルダー内の Experience Manager アセットにアップロードされたコンテンツには、選択したプロファイルが適用されます。

後で変更した既存のビデオプロファイルが存在するフォルダー内のアセットを再処理できます。[処理プロファイルを編集した後のフォルダー内のアセットの再処理](/help/assets/dynamic-media/about-image-video-profiles.md#reprocessing-assets)を参照してください。

**Dynamic Media 画像プロファイルをグローバルに適用するには**：

1. 次のいずれかの操作を行います。

   * `https://&lt;AEM server&gt;/mnt/overlay/dam/gui/content/assets/foldersharewizard.html/content/dam` に移動して適切なプロファイル適用し、「**[!UICONTROL 保存]**」を選択します。

     ![chlimage_1-257](assets/chlimage_1-257.png)

   * CRXDE Lite で、`/content/dam/jcr:content` ノードに移動します。

     プロパティ `imageProfile:/conf/global/settings/dam/adminui-extension/imageprofile/<name of image profile>` を追加し、「**[!UICONTROL すべて保存]**」を選択します。

     ![configure_image_profiles](assets/configure_image_profiles.png)

## 単一の画像のスマート切り抜きまたはスマートスウォッチの編集 {#editing-the-smart-crop-or-smart-swatch-of-a-single-image}

>[!IMPORTANT]
>
>アドビでは、生成されるスマート切り抜きやスマートスウォッチを確認し、これらが適切であり、ブランドと価値に関連していることを確認することをお勧めします。

画像の焦点位置を細かく調整するには、手動で位置を調整するか、スマート切り抜きウィンドウのサイズを変更します。

スマート切り抜きを編集して保存すると、その画像の切り抜きを使用しているすべての場所で変更が反映されます。

>[!IMPORTANT]
>
>アセットのスマート切り抜きウィンドウを手動で調整すると、変更内容が保存されます。これらの編集内容は、後でアセットを再処理した場合でもそのまま残ります。ただし、画像プロファイルの「**[!UICONTROL レスポンシブ画像の切り抜き]**」で幅と高さのいずれか、またはその両方を編集した場合、そのアセットは再処理の対象となります。
>[フォルダー内の Dynamic Media アセットの再処理](/help/assets/dynamic-media/about-image-video-profiles.md#reprocessing-assets) を参照してください。

必要に応じてスマート切り抜きを再実行して、追加の切り抜きを再度生成します。

[複数の画像のスマート切り抜きまたはスマートスウォッチの編集](#editing-the-smart-crop-or-smart-swatch-of-multiple-images) も参照してください。

**単一の画像のスマート切り抜きまたはスマートスウォッチの編集:**

1. Experience Manager ロゴを選択し、**[!UICONTROL Assets]** に移動した後、スマート切り抜きまたはスマートスウォッチの画像プロファイルが適用されているフォルダーに移動します。
1. コンテンツを開くには、フォルダーを選択します。
1. スマート切り抜きまたはスマートスウォッチを調整する画像を選択します。
1. ツールバーで、「**[!UICONTROL スマート切り抜き]**」を選択します。

   >[!TIP]
   >
   >ホットキー `s` を使用して、スマート切り抜きまたはスマートスウォッチを編集します。

1. 次のいずれかの操作を行います。

   * ページの右上隅にあるスライダーバーを左右にドラッグして画像表示を拡大または縮小します。
   * 画像のコーナーハンドルをドラッグして、切り抜きまたはスウォッチの表示可能領域のサイズを調整します。
   * 画像上で、ボックスまたはスウォッチを新しい場所にドラッグします。編集できるのは、画像スウォッチのみです。カラースウォッチは静的です。
   * 画像の右上隅近くにある「**[!UICONTROL 元に戻す]**」を選択して、すべての編集作業を取り消し、元の切り抜きまたはスウォッチを復元します。
   * キーボードの矢印キーを使用して、フレームサイズを切り抜いたり、画像の位置を変更したりします。

1. ページの右上付近にある「**[!UICONTROL 保存]**」を選択し、「**[!UICONTROL 閉じる]**」を選択して、アセットのフォルダーに戻ります。

## 複数の画像のスマート切り抜きまたはスマートスウォッチの編集 {#editing-the-smart-crop-or-smart-swatch-of-multiple-images}

>[!IMPORTANT]
>
>アドビでは、生成されるスマート切り抜きやスマートスウォッチを確認し、これらが適切であり、ブランドと価値に関連していることを確認することをお勧めします。

スマート切り抜きを含んだ画像プロファイルをフォルダーに適用すると、そのフォルダー内のすべての画像に切り抜きが適用されます。必要に応じて、複数の画像の位置を手動で調整することや、スマート切り抜きウィンドウのサイズを変更して、焦点位置をさらに細かく調整できます。

スマート切り抜きを編集して保存すると、その画像の切り抜きを使用しているすべての場所で変更が反映されます。

>[!IMPORTANT]
>
>複数のアセットのスマート切り抜きウィンドウを手動で調整すると、変更内容が保存されます。これらの編集内容は、後でアセットを再処理した場合でもそのまま残ります。ただし、画像プロファイルの「**[!UICONTROL レスポンシブ画像の切り抜き]**」で幅と高さのいずれか、またはその両方を編集した場合、それらのアセットは再処理の対象となります。
>[フォルダー内の Dynamic Media アセットの再処理](/help/assets/dynamic-media/about-image-video-profiles.md#reprocessing-assets) を参照してください。

必要に応じてスマート切り抜きを再実行して、追加の切り抜きを再度生成します。

**複数画像のスマート切り抜きまたはスマートスウォッチの編集:**

1. Experience Manager ロゴを選択し、**[!UICONTROL Assets]** に移動した後、スマート切り抜きまたはスマートスウォッチの画像プロファイルが適用されているフォルダーに移動します。
1. フォルダーで、**[!UICONTROL その他のアクション]**（...）アイコンを選択し、「**[!UICONTROL スマート切り抜き]**」を選択します。

1. **[!UICONTROL スマート切り抜きを編集]**&#x200B;ページで、次のいずれかの操作を行います。

   * 画像の表示サイズを調整します。

      ブレークポイント名のドロップダウンリストの右側にあるスライダーバーを左右にドラッグして表示可能な画像表示のサイズを変更します。

     ![edit_smart_crops-sliderbar](assets/edit_smart_crops-sliderbar.png)

   * ブレークポイント名に基づいて、表示可能な画像のリストをフィルタリングします。以下の例では、「中」というブレークポイント名で画像を絞り込んでいます。

      ページの右上隅にあるドロップダウンリストから、ブレークポイント名を選択して、表示する画像を絞り込みます（上記の画像を参照してください）。

     ![edit_smart_crops-dropdownlist](assets/edit_smart_crops-dropdownlist.png)

   * スマート切り抜きボックスのサイズを変更します。次のいずれかの操作を行います。

      * 画像にスマート切り抜きまたはスマートスウォッチのみが適用されている場合は、画像の切り抜きボックスのコーナーハンドルをドラッグして、切り抜きの表示可能領域のサイズを調整します。
      * 画像にスマート切り抜きとスマートスウォッチの両方が適用されている場合は、画像の切り抜きボックスのコーナーハンドルをドラッグして、切り抜きの表示可能領域のサイズを調整します。または、画像の下のスマートスウォッチを選択し（カラースウォッチは静的です）、切り抜きボックスの隅のハンドルをドラッグします。スウォッチの表示可能領域のサイズを調整します。

     ![画像のスマート切り抜きのサイズ変更](assets/edit_smart_crops-resize.png)

   * スマート切り抜きボックスを移動します。次のいずれかの操作を行います。

      * 画像にスマート切り抜きまたはスマートスウォッチのみが適用されている場合は、画像の切り抜きボックスを新しい場所にドラッグします。
      * 画像にスマート切り抜きとスマートスウォッチの両方が含まれている場合は、画像上でスマート切り抜きボックスを新しい場所にドラッグします。または、画像の下部にあるスマートスウォッチを選択してから（カラースウォッチは静的です）、スマートスウォッチの切り抜きボックスを新しい場所にドラッグします。

     ![edit_smart_crops-move](assets/edit_smart_crops-move.png)

   * すべての編集作業を取り消し、元のスマート切り抜きまたはスマートスウォッチを復元します（現在の編集セッションにのみ適用されます）。

     画像の上にある「**[!UICONTROL 元に戻す]**」を選択します。

     ![edit_smart_crops-revert](assets/edit_smart_crops-revert.png)

1. ページの右上付近にある「**[!UICONTROL 保存]**」を選択し、「**[!UICONTROL 閉じる]**」を選択して、アセットのフォルダーに戻ります。

## フォルダーからのイメージプロファイルの削除 {#removing-an-image-profile-from-folders}

フォルダーからイメージプロファイルを削除すると、サブフォルダーは自動的に親フォルダーのプロファイルの削除状態を継承します。ただし、フォルダー内で実行されたファイルの処理はそのまま維持されます。

**[!UICONTROL ツール]**&#x200B;メニュー内から、またはフォルダー内にいる場合は「**[!UICONTROL プロパティ]**」で、特定のフォルダーからイメージプロファイルを削除できます。

### プロファイルユーザーインターフェイスを使用したフォルダーからの Dynamic Media イメージプロファイルの削除 {#removing-image-profiles-from-folders-via-profiles-user-interface}

1. Experience Manager ロゴを選択し、**[!UICONTROL ツール]**／**[!UICONTROL Assets]**／**[!UICONTROL 画像プロファイル]**&#x200B;に移動します。
1. 1 つ以上のフォルダーから削除する画像プロファイルを選択します。
1. 「**[!UICONTROL フォルダーから処理プロファイルを削除]**」を選択し、プロファイルを削除する 1 つまたは複数のフォルダーを選択して、「**[!UICONTROL 削除]**」を選択します。

   名前がフォルダー名の下に表示されなくなっていることで、イメージプロファイルがフォルダーに適用されていないことを確認できます。

### プロパティを使用したフォルダーからの Dynamic Media イメージプロファイルの削除 {#removing-image-profiles-from-folders-via-properties}

1. Experience Manager ロゴを選択して「**[!UICONTROL アセット]**」に移動した後、画像プロファイルを削除するフォルダーに移動します。
1. チェックマークを選択して対象のフォルダーを選択し、「**[!UICONTROL プロパティ]**」を選択します。
1. 「**[!UICONTROL イメージプロファイル]**」タブを選択します。
1. 「**[!UICONTROL プロファイル名]**」ドロップダウンリストから「**[!UICONTROL なし]**」を選択し、「**[!UICONTROL 保存して閉じる]**」を選択します。

   プロファイルが割り当てられているフォルダーには、フォルダー名のすぐ下にプロファイルの名前が表示されます。
