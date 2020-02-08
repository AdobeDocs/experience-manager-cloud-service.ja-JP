---
title: 画質最適化のベストプラクティス
description: ダイナミックメディアの画質を最適化するためのベストプラクティスを紹介します。
translation-type: tm+mt
source-git-commit: 21b2541b6a3c5011b6eca7edf85299291c361147

---


# 画質最適化のベストプラクティス {#best-practices-for-optimizing-the-quality-of-your-images}

許容できる結果のレンダリングには多くの要因が関係するので、画質の最適化には時間がかかることがあります。画質に対する個人の感覚は異なるので、結果は一部主観的なものです。構造化された実験をおこなうことが重要になります。

AEMには、画像の調整と最適化、結果のレンダリングを行うための、100を超えるダイナミックメディア画像配信コマンドが含まれています。次のガイドラインは、いくつかの重要なコマンドとベストプラクティスを使用して、プロセスを合理化し、良い結果をすばやく得るのに役立ちます。

## Best practices for image format (`&fmt=`) {#best-practices-for-image-format-fmt}

* JPG または PNG は、管理しやすいサイズと重さで良い画質の画像を配信するための最適な選択肢です。
* URL に format コマンドが含まれていない場合、Dynamic Media 画像配信のデフォルトは JPG の配信になります。
* JPG は 10:1 の比率で圧縮をおこない、通常は比較的小さい画像ファイルサイズになります。PNG は約 2:1 の比率で圧縮をおこないますが、画像に白の背景が含まれている場合など、一部のケースではこの比率になりません。ただし、通常は PNG ファイルのサイズは JPG ファイルよりも大きくなります。
* JPG では非可逆圧縮が使用されます。非可逆圧縮では、圧縮中に画素（ピクセル）が失われます。これに対して、PNG では可逆圧縮が使用されます。
* JPG では多くの場合、写真画像が、エッジやコントラストがシャープな合成画像よりも高い忠実度で圧縮されます。
* 画像に透明部が含まれている場合は PNG を使用します。JPG では透明化がサポートされていません。

As a best practice for image format, start with the most common setting `&fmt=JPG`.

## 画像サイズのベストプラクティス {#best-practices-for-image-size}

画像サイズを動的に縮小することは、ごく一般的なタスクの 1 つです。サイズを指定し、さらにオプションでどのダウンサンプリングモードを使用して画像をダウンスケールするかを指定します。

* For image sizing, the best and most straightforward approach is to use `&wid=<value>` and `&hei=<value>,`or just `&hei=<value>`. これらのパラメーターによって、画像の幅が縦横比に合わせて自動的に設定されます。
* `&resMode=<value>`ダウンサンプリングに使用するアルゴリズムを制御します。 で始めま `&resMode=sharp2`す。 この値によって最適な画質が設定されます。While using the downsampling `value =bilin` is faster, it often results in the aliasing of artifacts.

画像サイズ変更のベストプラクティスとして、 `&wid=<value>&hei=<value>&resMode=sharp2` または `&hei=<value>&resMode=sharp2`

## 画像のシャープニングに関するベストプラクティス {#best-practices-for-image-sharpening}

画像のシャープニングは、Web サイト上の画像を管理するうえで最も難しい操作であり、多くの誤りが発生するところです。次の補助的なリソースを参照して、AEM でのシャープニングおよびアンシャープニングマスクの仕組みについて詳しく確認してください。

Best practices white paper [Sharpening images in Adobe Scene7 Publishing System and on Image Server](/help/assets/dynamic-media/assets/s7_sharpening_images.pdf) applies to AEM as well.

On Adobe TV, watch [Sharpening an image with unsharp mask](https://helpx.adobe.com/photoshop/atv/cs6-tutorials/sharpening-an-image-with-unsharp-mask.html).

AEM を使用すれば、取り込み時、配信時またはその両方で画像をシャープにすることができます。ただし、ほとんどの場合は、両方ではなくどちらか一方の方法のみを使用して画像をシャープにしてください。一般に、配信時に URL 上で画像をシャープにすることで、最適な結果が得られます。

画像のシャープニングでは、次の 2 つの方法を使用できます。

* Simple sharpening ( `&op_sharpen`) – Similar to the sharpen filter used in Photoshop, simple sharpening applies basic sharpening to the final view of the image following dynamic resizing. ただし、この方法ではユーザーによる設定は不可能です。ベストプラクティスは、必要な場合以外は&amp;op_sharpenを使用しないことです。
* Unsharp masking ( `&op_USM`) – Unsharp masking is an industry standard sharpening filter. ベストプラクティスは、以下のガイドラインに従ってアンシャープマスクを使用して画像をシャープニングすることです。アンシャープマスクによって、次の 3 つのパラメーターを制御できます。

   * `&op_sharpen=`量，半径，しきい値

      * **[!UICONTROL amount]** （0 ～ 5、効果の強さ）
      * **[!UICONTROL radius]** (0 ～ 250、シャープを適用したオブジェクトの周囲に描画される「シャープの適用線」の幅（ピクセル単位）

         radiusパラメーターとamountパラメーターは相互に作用することに注意してください。radiusを減らすにはamountを増やします。radiusを指定すると、端のピクセルのみがシャープになり、radiusを指定すると細かい制御が可能になります。高い値を指定すると、幅広い範囲のピクセルがシャープになります。

      * **[!UICONTROL しきい値]** （0 ～ 255、効果の感度）

         このパラメーターは、シャープにされるピクセルが周囲の領域とどの程度違えば、そのピクセルをエッジのピクセルと見なしてフィルターによりシャープにするかを決定するものです。The **[!UICONTROL threshold]** parameter helps to avoid over-sharpening areas with similar colors, such as skin tones. 例えば、threshold の値を 12 にした場合、肌のトーンの明るさにわずかな差があっても無視して「ノイズ」が加わるのを防ぎながら、まつげと肌が隣り合う場所など、コントラストの高い領域に対してエッジコントラストを追加することができます。
      フィルターを使用したベストプラクティスを含む、これら 3 つのパラメーターの設定方法について詳しくは、次のリソースを参照してください。

      画像へのシャープの適用に関するAEMヘルプトピックです。

      Best practices white paper [Sharpening images in Adobe Scene7 Publishing System and on Image Server](/help/assets/dynamic-media/assets/s7_sharpening_images.pdf).

   * AEMでは、4番目のパラメーターを制御することもできます。モノクロ(0,1) このパラメーターは、各カラーコンポーネントにアンシャープマスクを、値0を使用して個別に適用するか、値1を使用して画像の明るさ/強さに適用するかを決定します。


ベストプラクティスとして、まずはアンシャープマスクの radius パラメーターを使用します。手始めに使用できる radius 設定は次のとおりです。

* **[!UICONTROL Webサイト]**:0.2-0.3ピクセル
* **[!UICONTROL 写真印刷(250 ～ 300 ppi)]**:0.3-0.5ピクセル
* **[!UICONTROL オフセット印刷(266 ～ 300 ppi)]**:0.7-1.0ピクセル
* **[!UICONTROL カンバス印刷(150 ppi)]**:1.5 ～ 2.0ピクセル

amount を 1.75 から 4 まで少しずつ増やします。シャープニングの結果に満足できない場合は、radius を小数点以下の単位で増やして、再度 amount を 1.75 から 4 の範囲で実行します。必要に応じてこの手順を繰り返します。

monochrome パラメーター設定は 0 のままにします。

### Best practices for JPEF compression (`&qlt=`) {#best-practices-for-jpef-compression-qlt}

* このパラメーターでは、JPG エンコーディング品質を制御します。値が大きいほど高画質になりますがファイルサイズも大きくなります。逆に、値が小さいほど低画質になりますがファイルサイズは小さくなります。このパラメーターの範囲は 0～100 です。
* 画質を最適化するには、このパラメーターの値を 100 に設定しないでください。90 や 95 の設定と 100 の設定では、画質の差はほとんど感じられませんが、100 に設定することで画像ファイルのサイズが不必要に増加します。Therefore, to optimize for quality but avoid image files becoming too large, set the `qlt= value` to 90 or 95.
* 小さい画像ファイルサイズに最適化し、画質を許容可能なレベルに保つには、を80 `qlt= value` に設定します。 70 ～ 75未満の値を指定すると、画質が大幅に低下します。
* As a best practice, to stay in the middle, set the `qlt= value` to 85 to stay in the middle.
* Using the chroma flag in `qlt=`

   * The `qlt=` parameter has a second setting that lets you turn on RGB chromaticity downsampling using the value `,1` or off using the value `,0`.
   * To keep it simple, start with RGB chromaticity downsampling turned off (`,0`). This setting usually results in better image quality, especially for synthetic images with lots of sharp edges and contrast.

As a best practice for JPG compression use `&qlt=85,0`.

## Best practices for JPEG sizing (`&jpegSize=`) {#best-practices-for-jpeg-sizing-jpegsize}

jpegSizeは、メモリに制限があるデバイスに配信するために画像が特定のサイズを超えないようにする場合に便利なパラメータです。

* This parameter is set in kilobytes (`jpegSize=&lt;size_in_kilobytes&gt;`). It defines the maximum allowed size for image delivery.
* `&jpegSize=` はJPG圧縮パラメーターと相互に作用しま `&qlt=`す。 If the JPG response with the specified JPG compression parameter (`&qlt=`) does not exceed thejpegSize value, the image is returned with `&qlt=` as defined. Otherwise, `&qlt=` is gradually decreased until the image fits in the maximum allowed size, or until the system determines it cannot fit and returns an error.

As a best practice, set `&jpegSize=` and add the parameter `&qlt=` if you are delivering JPG images to devices with limited memory.

## ベストプラクティスのまとめ {#best-practices-summary}

ベストプラクティスとして、ファイルサイズを小さくして高画質を達成するには、次のパラメーターの組み合わせで始めます。

`fmt=jpg&qlt=85,0&resMode=sharp2&op_usm=1.75,0.3,2,0`

この設定の組み合わせによって、ほとんどの状況で優れた結果になります。

画像をさらに最適化する必要がある場合は、シャープニング（アンシャープマスク）のパラメーターを少しずつ微調整します。まずは、radius を 0.2 または 0.3 に設定します。また、amount を 1.75 から最大 4（Photoshop での 400 ％に相当）まで少しずつ増やします。この状態で、求めている結果が得られるかを確認します。

シャープニングの結果でも満足できない場合は、radius の小数点以下を増やします。小数点以下を増やすごとに、amount を 1.75 からやり直し、4 まで少しずつ増やします。求めている結果になるまで、このプロセスを繰り返します。これらの値は、制作スタジオで実際に検証した手法ではありますが、初期値として別の値を使用し、他の戦略に従っても問題ありません。結果が満足できるものであるかは主観的な問題ですので、構造化された実験をおこなうことが重要です。

実験をおこなう際には、ワークフローを最適化するための次の一般的な推奨事項も役に立つでしょう。

* 様々なパラメーターをリアルタイムで試し、URL上で直接テストするか、調整操作のリアルタイムプレビューを提供するScene7 Publishing systemの画像調整機能を使用してテストします。
* ベストプラクティスとして、ダイナミックメディア画像サービングコマンドを画像プリセットにグループ化できます。 An image preset is basically URL command macros with custom preset names such as `$thumb_low$` and `&product_high$`. URL パス内でカスタムプリセット名を指定すると、これらのプリセットがコールされます。この機能によって、Web サイトでの様々な画像使用パターンに応じたコマンドと画質設定を管理でき、URL の全体的な長さを短縮することができます。
* AEM では、取り込み時に画像のシャープニングを適用するなど、高度な画質調整機能を提供しています。For advanced use cases where this may be an option to further tune and optimize rendering results, [Adobe Professional Services](https://www.adobe.com/experience-cloud/consulting-services.html) can help you with customized insight and best practices.

