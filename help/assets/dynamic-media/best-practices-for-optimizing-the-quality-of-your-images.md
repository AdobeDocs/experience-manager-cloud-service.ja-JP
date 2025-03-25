---
title: 画質最適化のベストプラクティス
description: Dynamic Media を使用して画像アセットの品質を最適化するためのベストプラクティスについて説明します。
contentOwner: Rick Brough
feature: Asset Management, Best Practices
role: User
exl-id: 2efc4a27-01d7-427f-9701-393497314402
source-git-commit: 36ab36ba7e14962eba3947865545b8a3f29f6bbc
workflow-type: tm+mt
source-wordcount: '1648'
ht-degree: 100%

---

# 画質最適化のベストプラクティス {#best-practices-for-optimizing-the-quality-of-your-images}

{{work-with-dynamic-media}}

許容できる結果のレンダリングには多くの要因が関係するので、画質の最適化には時間がかかることがあります。画質に対する個人の感覚は異なるので、結果は一部主観的なものです。構造化された実験を行うことが重要になります。

Adobe Experience Manager には、画像をチューニングおよび最適化して結果をレンダリングするための、100 を超える Dynamic Media 画像配信コマンドがあります。次のガイドラインは、一部の基本コマンドとベストプラクティスを使用してこのプロセスを効率化し、すぐに良好な結果を得るために活用できます。

<!-- ADDED THE FOLLOWING TOPIC AS PER CQDOC-21594 -->

## Dynamic Media でスマートイメージングを有効にする {#bp-enable-smart-imaging}

**スマートイメージング：**

* Dynamic Media でスマートイメージングを有効にすると、クライアントのブラウザーの機能に基づいて、画像の形式、サイズ、画質を自動的に最適化できます。
詳しくは、[スマートイメージング](https://experienceleague.adobe.com/ja/docs/experience-manager-cloud-service/content/assets/dynamicmedia/imaging-faq)を参照してください。
* これらのパラメーターを動的に調整することで、画像配信のパフォーマンスが向上します。
* 自己評価ツールの[スナップショット](https://snapshot.scene7.com/)を使用すると、スマートイメージングを評価できます。

**画像形式：**

* ユースケースで特に必要な場合を除き、URL で明示的な `fmt=webp` または `fmt=avif` コマンドを使用しないでください。
* スマートイメージングでは最適な形式を自動的に選択し、最適な帯域幅の増加を実現します。

**デフォルトの動作：**

* URL に format コマ ンドが指定されておらず、スマートイメージングが有効になっていない場合、Dynamic Media 画像配信ではデフォルトで JPEG 形式が使用されます。

画像形式について十分な情報に基づいて選択し、スマートイメージングを有効にすることで、パフォーマンスとユーザーエクスペリエンスに大きな影響を与えることができます。


<!-- ADDED THE FOLLOWING TOPIC AS PER CQDOC-21594 -->

## ソース画像を選択するためのベストプラクティス {#bp-select-source-image}

ソース画像を操作する際の基本的な考慮事項は次のとおりです。

* **ソース画像の形式：**
   * PNG、TIFF、PSDなどの可逆形式を使用すると、圧縮アーティファクトを発生させずに画質を高品質に保つことができます。
   * これらの形式では、元のデータがすべて保持されるので、編集やさらなる処理に最適です。
* **ソース画像のサイズ：**
   * 高解像度の画像から始めると、より詳細な情報と柔軟性が得られます。
   * 画像を様々なサイズで表示する必要がある場合（例えば、デバイス間や画面解像度間）、ソース画像を大きくすると、拡大／縮小が向上します。
   * ズームをサポートする画像（製品写真など）の場合は、長辺で約 2,000 ピクセル以上を目指します。
   * ズームを必要としないロゴやバナーは、目的に応じて必要な最大サイズでアップロードできます。

ソースレベルでこれらの慎重な選択を行うことで、ビジュアルコンテンツの全体的な画質を大幅に向上させることができます。

<!-- REMOVED TOPIC AS PER CQDOC-21594
## Best practices for image format (`&fmt=`) {#best-practices-for-image-format-fmt}

* JPG or PNG are the best choices to deliver images in good quality and with manageable size and weight.
* If no format command is supplied in the URL, Dynamic Media Image Delivery defaults to JPG for delivery.
* JPG compresses at a ratio of 10:1 and usually produces smaller image file sizes. PNG compresses at a ratio of about 2:1, except when images contain a white background. Typically though, PNG file sizes are larger than JPG files.
* JPG uses lossy compression, meaning that picture elements (pixels) are dropped during compression. PNG on the other hand uses lossless compression.
* JPG often compresses photographic images with better fidelity than synthetic images with sharp edges and contrast.
* If your images contain transparency, use PNG because JPG does not support transparency.

As a best practice for image format, start with the most common setting `&fmt=JPG`. -->

## 画像サイズのベストプラクティス {#best-practices-for-image-size}

画像サイズを動的に縮小することは、ごく一般的なタスクの 1 つです。サイズを指定し、さらにオプションでどのダウンサンプリングモードを使用して画像をダウンスケールするかを指定します。

* 画像のサイズ設定における最も簡単で最適なアプローチは、`&wid=<value>` と `&hei=<value>,` の両方、または `&hei=<value>` のみを使用することです。これらのパラメーターによって、画像の幅が縦横比に合わせて自動的に設定されます。
* `&resMode=<value>` は、ダウンサンプリングに使用するアルゴリズムを制御します。まず手始めに `&resMode=sharp2` を使用します。この値によって最適な画質が設定されます。ダウンサンプリングを使用する場合は `value =bilin` のほうが速くなりますが、この設定では通常、アーティファクトのエイリアシングが実行されます。

画像サイズ設定のベストプラクティスとしては、`&wid=<value>&hei=<value>&resMode=sharp2` または `&hei=<value>&resMode=sharp2` を使用します。

## 画像のシャープニングに関するベストプラクティス {#best-practices-for-image-sharpening}

画像のシャープ処理は、Web サイト上の画像を制御する際の最も複雑な側面で、多くのミスが生じます。次の役立つリソースを参照し、Experience Manager でのシャープおよびアンシャープマスクの仕組みについて詳しく学んでください。

* ベストプラクティスに関するホワイトペーパー『[Adobe Dynamic Media Classic の画質とシャープ処理のベストプラクティス](/help/assets/dynamic-media/assets/sharpening_images.pdf)』は Experience Manager にも当てはまります。

* [Experience Manager - Dynamic Media で画像シャープ処理を使用する](https://experienceleague.adobe.com/ja/docs/experience-manager-learn/assets/dynamic-media/images/dynamic-media-image-sharpening-feature-video-use#dynamic-media)を見る。

Experience Manager を使用すれば、取得時、配信時またはその両方で画像をシャープにすることができます。ただし、通常は、両方の方法ではなくどちらか一方のみを使用して画像をシャープにすることをお勧めします。一般に、配信時に URL 上で画像をシャープにすることで、最適な結果が得られます。

画像のシャープニングでは、次の 2 つの方法を使用できます。

* シンプルシャープニング（`&op_sharpen`）- Photoshop で使用するシャープニングフィルターと同様に、シンプルシャープニングでは、動的なサイズ変更の後に、画像の最終表示形に対して基本的なシャープニングを適用します。ただし、この方法ではユーザーによる設定は不可能です。ベストプラクティスは、必要な場合を除いて `&op_sharpen` を使用しないことです。
* アンシャープマスク（`&op_USM`）- アンシャープマスクは、業界標準のシャープニングフィルターです。ベストプラクティスは、以下のガイドラインに従ってアンシャープマスクを使用して画像をシャープニングすることです。アンシャープマスクによって、次の 3 つのパラメーターを制御できます。

   * `&op_sharpen=`amount,radius,threshold

      * **[!UICONTROL amount]**（0～5、効果の強さ）
      * **[!UICONTROL radius]**（0～250、シャープニングにされるオブジェクトの周囲に描かれる「シャープニングされた線」の幅、ピクセル単位）

     radius パラメーターと amount は互いに反対に作用することに注意してください。radius を減らした場合は、amount を増やして補うことができます。radius を使用すると、よりきめ細かい制御が可能です。値が小さいとエッジ部のピクセルのみがシャープニングされ、値が大きいとより幅広いピクセルがシャープにされます。

      * **[!UICONTROL threshold]**（0～255、効果の感度）

     このパラメーターは、シャープにされるピクセルが周囲の領域とどの程度違えば、そのピクセルをエッジのピクセルと見なしてフィルターによりシャープにするかを決定するものです。この **[!UICONTROL threshold]** パラメーターによって、肌のトーンなど、同じような色の領域を過剰にシャープニングすることを防ぎます。例えば、threshold の値を 12 にすると、肌のトーンの明るさにわずかな差があっても無視して「ノイズ」が加わるのを防ぎながら、まつげと肌の境界など、コントラストの高い領域に対してエッジコントラストを追加することができます。

     フィルターを使用したベストプラクティスを含む、これら 3 つのパラメーターの設定方法について詳しくは、次のリソースを参照してください。

      * ベストプラクティスに関するホワイトペーパー『[Adobe Dynamic Media Classic の画質とシャープ処理のベストプラクティス](/help/assets/dynamic-media/assets/sharpening_images.pdf)』は Experience Manager にも当てはまります。

      * [Experience Manager - Dynamic Media で画像シャープ処理を使用する](https://experienceleague.adobe.com/ja/docs/experience-manager-learn/assets/dynamic-media/images/dynamic-media-image-sharpening-feature-video-use#dynamic-media)を見る。

      * Experience Manager では第 4 パラメーターの monochrome (0,1) も制御できます。このパラメーターでは、アンシャープマスクをそれぞれの色成分に個別に適用するか（値が 0 の場合）、または画像の明るさ／明度に対して適用するか（値が 1 の場合）を指定します。

ベストプラクティスとして、まずはアンシャープマスクの半径パラメーターを使用します。手始めに使用できる半径設定は次のとおりです。

* **[!UICONTROL Web サイト]**：0.2～0.3 ピクセル
* **[!UICONTROL 写真印刷（250～300 ppi）]**：0.3～0.5 ピクセル
* **[!UICONTROL オフセット印刷（266～300 ppi）]**：0.7～1.0 ピクセル
* **[!UICONTROL キャンバス印刷（150 ppi）]**：1.5～2.0 ピクセル

量を 1.75 から 4 まで少しずつ増やします。シャープニングの結果に満足できない場合は、半径を小数点以下の単位で増やして、再度量を 1.75 から 4 の範囲で実行します。必要に応じて繰り返します。

モノクロパラメーターの設定は 0 のままにします。

### JPEF 圧縮（`&qlt=`）のベストプラクティス {#best-practices-for-jpef-compression-qlt}

* このパラメーターでは、JPG エンコーディング品質を制御します。値が大きいほど高画質になりますがファイルサイズも大きくなります。逆に、値が小さいほど低画質になりますがファイルサイズは小さくなります。このパラメーターの範囲は 0～100 です。
* 画質を最適化するには、このパラメーターの値を 100 に設定しないでください。90 や 95 の設定と 100 の設定では、画質にほとんど差はありません。ただし、100 に設定すると画像ファイルのサイズが不必要に増加します。したがって、画質を最適化しながら画像ファイルが大きくなりすぎないようにするために、`qlt= value` を 90 または 95 に設定します。
* 小さい画像ファイルサイズに最適化しつつ、画質を許容できるレベルに保つには、`qlt= value` を 80 に設定します。70～75 未満の値を指定すると、画質が大幅に低下します。
* ベストプラクティスとしては、間を取って `qlt= value` を 85 に設定します。
* `qlt=` での色度フラグの使用

   * `qlt=` パラメーターには、RGB 色度のダウンサンプルを有効にする第 2 の設定があります。この設定を有効にするには値 `,1` を使用し、無効にするには値 `,0` を使用します。
   * 簡易な設定を維持するため、まずは RGB 色度のダウンサンプルを無効にします（`,0`）。この設定により、通常は高画質になります。特に、シャープなエッジやコントラストが多く含まれる合成画像で高画質になります。

JPG 圧縮のベストプラクティスとしては、`&qlt=85,0` を使用します。

## JPEG サイズ設定（`&jpegSize=`）のベストプラクティス {#best-practices-for-jpeg-sizing-jpegsize}

`jpegSize` パラメーターは、メモリ容量が限られているデバイスに配信される画像が特定のサイズを超えないようにしたい場合に便利です。

* このパラメーターはキロバイト単位で設定します（`jpegSize=&lt;size_in_kilobytes&gt;`）。画像配信で許可される最大サイズを定義します。
* `&jpegSize=` は、JPG 圧縮パラメーターである `&qlt=` と相互に作用します。指定された JPG 圧縮パラメーター（`&qlt=`）での JPG 応答が jpegSize の値を上回らない場合、画像は `&qlt=` で定義されたとおりに返されます。jpegSize の値を上回る場合は、`&qlt=` が少しずつ減らされ、画像のサイズが最大許容サイズ内に収められます。または、そのサイズ内に収まらないとシステムによって判断された場合は、エラーが返されます。

ベストプラクティスとしては、`&jpegSize=` を設定し、メモリ容量が限られているデバイスに JPG 画像を配信する場合は `&qlt=` パラメーターを追加します。

## ベストプラクティスのまとめ {#best-practices-summary}

ベストプラクティスとして、ファイルサイズを小さくして高画質を達成するには、次のパラメーターの組み合わせで始めます。

`fmt=jpg&qlt=85,0&resMode=sharp2&op_usm=1.75,0.3,2,0`

設定をこのように組み合わせると、ほとんどの状況において優れた結果になります。

画像をさらに最適化する必要がある場合は、シャープニング（アンシャープマスク）のパラメーターを少しずつ微調整します。まずは、radius を 0.2 または 0.3 に設定します。また、amount を 1.75 から最大 4（Photoshop での 400％に相当）まで少しずつ増やします。この状態で、求めている結果が得られるかを確認します。

シャープニングの結果でも満足できない場合は、半径の小数点以下を増やします。小数点以下を増やすごとに、量を 1.75 からやり直し、4 まで少しずつ増やします。求めている結果になるまで、このプロセスを繰り返します。これらの値は、クリエイティブスタジオで実際に検証した手法ではありますが、初期値として別の値を使用し、他の戦略に従っても問題ありません。結果が満足できるものであるかは主観的な問題ですので、構造化された実験を行うことが重要です。

実験する際には、次の一般的な推奨事項がワークフローの最適化に役に立ちます。

* 様々なパラメーターを直接 URL 上でリアルタイムにテストします。
* ベストプラクティスとしては、Dynamic Media 画像サービングコマンドを画像プリセット内にまとめることができます。画像プリセットは基本的に、`$thumb_low$` や `&product_high$` といったカスタムプリセット名が付けられた URL コマンドマクロです。URL パス内にカスタムプリセット名を指定すると、これらのプリセットが呼び出されます。この機能によって、Web サイトでの様々な画像使用パターンに応じたコマンドと画質設定を管理でき、URL の全体的な長さを短縮することができます。
* Adobe Experience Manager では、取り込み時に画像のシャープニングを適用するなど、高度な画質調整機能も提供しています。レンダリング結果を調整して最適化するために、[アドビのコンサルティングサービス](https://business.adobe.com/customers/consulting-services/main.html)では、カスタマイズされたインサイトとベストプラクティスを提供してユーザーを支援します。
