---
title: ビューアプリセットの管理
description: Dynamic Media でビューアプリセットを作成および管理する方法について説明します。
feature: Viewer Presets,Viewers
role: User
exl-id: da2e1a10-f54b-440e-b70c-f04ad4caeac1
source-git-commit: 1b9864c4532d15068b6edbd187a78a0ee0fdcfb4
workflow-type: tm+mt
source-wordcount: '4194'
ht-degree: 99%

---

# ビューアプリセットの管理{#managing-viewer-presets}

ビューアプリセットは、ユーザーのコンピューター画面やモバイルデバイスでのリッチメディアアセットの表示方法を決定する様々な設定のコレクションです。管理者は、ビューアプリセットを作成できます。設定は、幅広いビューア設定オプションで使用できます。例えば、ビューアの表示サイズやズームの動作を変更できます。

<!-- OBSOLETE SDK withdrawn from public view. Available internally only at `http://staging.scene7.com/s7sdk/3.8/docs/jsdoc/symbols/_s7sdk.html` 

For instructions on creating and customizing your own HTML5 viewer presets, see the *Adobe Scene7 HTML5 Viewer SDK*. The SDK is available on the IS publish server embedded in the SDK itself. Each library version has its own SDK documentation included.

Path: `<scene7_domain>/s7sdk/<library_version>/docs/jsdocs/index.html`.
For example, 3.5 SDK: [https://s7d1.scene7.com/s7sdk/3.5/docs/jsdoc/index.html](https://s7d1.scene7.com/s7sdk/3.5/docs/jsdoc/index.html)

-->

[Dynamic Media ビューアリファレンスガイド](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources.html?lang=ja)も参照してください。

ここでは、ビューアプリセットを作成、編集および管理する方法について説明します。アセットをプレビューする際は、いつでもビューアプリセットを適用できます。詳しくは、[ビューアプリセットの適用](#applying-a-viewer-preset-to-an-asset)を参照してください。

>[!NOTE]
>
>*事前に定義された標準提供ビューアプリセット*&#x200B;を編集するシナリオはサポートされていません。標準提供ビューアプリセットを編集しようとすると、そのビューアプリセットを新しい名前で保存するように指示されます。

## ビューアのキーボードアクセシビリティ {#keyboard-accessibility-for-viewers}

すべての標準提供ビューアでキーボードアクセシビリティがサポートされています。

[キーボードアクセシビリティとナビゲーション](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/c-keyboard-accessibility.html?lang=ja)に関するページも参照してください。

## ビューアプリセットの管理 {#managing-viewer-presets-1}

Adobe Experience Manager でビューアプリセットの追加、編集、削除、公開、非公開およびプレビューを実行できます。そのためには、**[!UICONTROL ツール（ハンマーアイコン）]**／**[!UICONTROL アセット]／[!UICONTROL ビューアプリセット]**&#x200B;に移動します。

![6_5_tools-assets-viewerpresets](assets/6_5_tools-assets-viewerpresets.png)

>[!NOTE]
>
>デフォルトで、アセットの詳細ビューでビューアを選択するときに、15 個のビューアプリセットが表示されます。この制限は増やすことができます。[表示されるビューアプリセットの数の増減](#increasing-the-number-of-viewer-presets-that-display)を参照してください。

### レスポンシブデザイン Web ページのビューアサポート {#viewer-support-for-responsive-designed-web-pages}

Web ページごとに異なるニーズがあります。例えば、個別のブラウザーウィンドウで HTML5 ビューアを開くリンクを示す Web ページが必要な場合や、ホストページ内に直接 HTML5 ビューアを埋め込むことが必要な場合もあります。後者の場合は、Web ページのレイアウトが静的か、「レスポンシブ」かによって、異なるデバイスや異なるブラウザーウィンドウサイズで異なる表示になります。これらのニーズに対応するために、Dynamic Media に付属する事前定義済みの標準提供 HTML5 ビューアはすべて、静的な Web ページとレスポンシブデザイン Web ページの両方をサポートしています。

レスポンシブビューアを Web ページに埋め込む方法について詳しくは、 Dynamic Media 画像サービングおよびレンダリング API ヘルプの[レスポンシブ静的画像ライブラリ](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/responsive-static-image-library/c-about-responsive-static-image-library.html?lang=ja#about-responsive-image-library)を参照してください&#x200B;*。*

>[!NOTE]
>
>あらかじめ用意されている標準のビューアはすべて、使用する前に公開します。
>[ビューアプリセットの公開](#publishing-viewer-presets)を参照してください。

### ビューアプリセットのシステム互換性   {#viewer-preset-system-compatibility}

Dynamic Media に付属するすべての標準提供ビューアプリセットは、次のシステムと完全に互換します。

* デスクトップ
* Apple iPhone
* Apple iPad
* Android™ スマートフォン
* Android™ タブレット

<!-- OUTDATED 2/25/22 * For video, extra support for MP4 playback is provided for [BlackBerry®](https://developer.blackberry.com/devzone/develop/supported_media/bb_media_support_at_a_glance.html#kba1328730952678) and [Windows® Phone](https://docs.microsoft.com/en-us/windows/uwp/audio-video-camera/supported-codecs). -->

### ビューアプリセットのリッチメディアタイプ {#rich-media-types-for-viewer-presets}

管理者は、ビューアプリセットの作成時に次のリッチメディアタイプを追加してカスタマイズすることができます。

<table>
 <tbody>
  <tr>
   <td><strong>カルーセルセット</strong><br /> </td>
   <td><p>ホットスポットや画像マップ、またはその両方が 2 つ以上の一連の画像に追加されます。顧客は画像を左右にパンし、画像のホットスポットを選択してさらに詳細情報を入力したり、Web サイトのランディングページ、カテゴリページまたはホームページから直接購入したりできます。</p> </td>
  </tr>
    <tr>
   <td><strong>ディメンション</strong><br /> </td>
   <td><p>3D シーンが表示され、カメラの回転、パン、ズーム、中心の変更が可能です。</p> </td>
  </tr>
  <tr>
   <td><strong>フライアウトズーム</strong></td>
   <td><p>オリジナル画像の横に、第 2 のズームされた領域の画像を表示します。使用できるコントロールはありません。ユーザーは表示したい領域上に選択範囲を動かします。</p> <p>このビューアの全体的な帯域幅使用量を算出する場合は、メイン画像とフライアウト画像の両方がビューアに配信されることを考慮してください。メイン画像のサイズ（ステージの幅と高さ）とズーム率によってフライアウト画像のサイズが決まります。フライアウトファイルのサイズが大きくなりすぎないようにするには、これら 2 つの値のバランスを取る必要があります。つまり、メイン画像のサイズが大きい場合は、ズーム率の値を小さくします。（フライアウトの幅と高さによってフライアウトウィンドウのサイズが決まりますが、ビューアに配信されるフライアウト画像のサイズが決まるわけではありません）。</p> <p>例えば、メイン画像のサイズが 350 x 350 ピクセルで、ズーム率が 3 の場合、生成されるフライアウト画像は 1,050 x 1,050 ピクセルになります。メインの画像サイズが 300 x 300 ピクセルで、ズーム率が 4 の場合、フライアウト画像は 1,200 x 1,200 ピクセルになります。JPEG 画質の設定（推奨設定は 80～90）によっては、ファイルサイズを大幅に削減できます。推奨されるズーム率は、メイン画像のサイズに応じて 2.5～4 となります。</p> </td>
  </tr>
  <tr>
   <td><strong>インラインズーム</strong></td>
   <td>ズームされた領域の画像を元のビューア内に表示します。使用するコントロールはありません。つまり、ユーザーは表示する領域上に選択範囲を動かします。</td>
  </tr>
  <tr>
   <td><strong>画像セット</strong></td>
   <td>画像セットビューアでは、サムネール画像を選択してアイテムの様々なビューやカラーを表示できます。このビューアは、画像を接近して確認するためのズームツールも提供しています。</td>
  </tr>
  <tr>
   <td><strong>インタラクティブ画像</strong></td>
   <td>ユーザーが選択してさらに詳細情報を入力したり、Web サイトのランディングページ、カテゴリページまたはホームページから直接購入したりするためのホットスポットが画像の一部に追加されます。</td>
  </tr>
  <tr>
   <td><strong>インタラクティブビデオ</strong></td>
   <td>ユーザーが選択してさらに詳細情報を入力したり、Web サイトのランディングページ、カテゴリページまたはホームページから直接購入したりするためのサムネールがビデオ内のタイムラインセグメントに追加されます。</td>
  </tr>
  <tr>
   <td><strong>混在メディア</strong></td>
   <td>1 つのビューアで異なる複数のタイプのメディアを表示します。スピンセット、画像セット、画像およびビデオを含めることができます。</td>
  </tr>
  <tr>
   <td><strong>パノラマ画像</strong></td>
   <td><p>パノラマ画像ビューアと PanoramicVR ビューアは、球パノラマ画像をレンダリングして、室内、物件、場所、風景などをあらゆる角度から見ることができる臨場感あふれる体験をユーザーに提供します。</p> <p>アップロードする画像が球パノラマとして適格となるには、以下の一方または両方の条件を満たしている必要があります。</p>
    <ul>
     <li>縦横比が 2:1 である必要があります。</li>
     <li>キーワード <code>equirectangular</code>、または <code>spherical</code> と <code>panorama</code>、または <code>spherical </code> と <code>panoramic</code> でタグ付けされている必要があります。<a href="/help/sites-cloud/authoring/features/tags.md">タグの使用</a>を参照してください。</li>
    </ul> <p>縦横比とキーワードの両方の条件が、アセットの詳細ページと「パノラマメディア」WCM コンポーネントのパノラマアセットに適用されます。</p></td>
  </tr>
    <tr>
   <td><strong>スマート切り抜きビデオ</strong><br /> </td>
   <td><p>このビューアを使用して、ビデオの焦点を自動的に検出し、切り抜きます。</p> </td>
  </tr>
  <tr>
   <td><strong>スピンセット</strong></td>
   <td>ユーザーがオブジェクトを回転させて、様々な面や角度を確認できるように、複数の画像ビューを提供します。</td>
  </tr>
  <tr>
   <td><strong>360 ビデオ</strong></td>
   <td><p>360/VR ビデオビューアを使用すると、エクイレクタングラー形式でビデオをレンダリングして、室内、物件、場所、風景、医療処置などの臨場感あふれる表示を実現することができます。</p> <p>フラットディスプレイでの再生時に、ユーザーは視野角を制御できます。モバイルデバイスでの再生では、デバイス組み込みのジャイロスコープ制御が使用されます。</p> <p>ビューアでは、360 ビデオアセットの配信をネイティブサポートしています。デフォルトでは、表示または再生するための追加設定は不要です。360 ビデオは、.mp4、.mkv、.mov といった標準のビデオ拡張子を使用して配信されます。最も一般的なコーデックは H.264 です。</p> </td>
  </tr>
  <tr>
   <td><strong>ビデオ</strong></td>
   <td><p>プログレッシブまたはアダプティブビットレートストリーミングを使用してビデオを再生します。アダプティブビットレートストリーミングでは、自動的にデバイスと帯域幅を検出して、適切な画質のビデオを適切な形式で配信します。</p> </td>
  </tr>
  <tr>
   <td><strong>垂直方向ズーム</strong></td>
   <td><p>垂直方向ズームビューアを使用すると、製品画像の閲覧エクスペリエンスを最大限に高めて、ユーザーにとって最適な製品の表示を実現できます。スウォッチを垂直方向に配置することで、次のような利点があります。</p>
    <ul>
     <li>ページを表示したときに、スクロールしなくてもスウォッチが表示されます。<br/>水平方向のスウォッチの場合、ユーザーのデスクトップ画面サイズによっては、ユーザーがページを下にスクロールするまでスウォッチが表示されません。ビューア内に垂直方向にスウォッチを配置することで、ユーザーの画面サイズに関係なく、確実にスウォッチが表示されるようになります。</li>
     <li>メイン画像のサイズが最大化されます。<br />水平方向のスウォッチの場合、スウォッチが表示されるようにページ上にスペースを確保する必要があります。この配置により、メイン画像のサイズが縮小されていました。ただし、スウォッチの垂直方向レイアウトでは、このスペースを確保する必要がありません。そのため、メイン画像のサイズを最大化できます。</li>
    </ul> </td>
  </tr>
  <tr>
   <td><strong>ズーム</strong></td>
   <td>ユーザーが領域を選択してズームインできます。ユーザーは、コントロールを選択して、ズームイン、ズームアウトおよび画像をデフォルトのサイズにリセットすることができます。</td>
  </tr>
 </tbody>
</table>

### 標準提供ビューアプリセットのリスト {#list-of-out-of-the-box-viewer-presets}

次の表に、Dynamic Media に付属するすべての事前定義済みの標準提供ビューアプリセットについて示します。

関連トピック [ライブデモ](https://landing.adobe.com/en/na/dynamic-media/ctir-2755/live-demos.html).

ビューアでサポートされている Web ブラウザーとオペレーティングシステムのバージョンについては、ビューアのリリースノートに記載されています。

『[ビューアリファレンスガイド](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources.html)』の目次の「ビューアのリリースノート」を参照してください。

>[!NOTE]
>
>Dynamic Media の標準提供のビューアプリセットはすべてアクティベート済み（オン）になっていますが、それらを公開する必要があります。
>[ビューアプリセットの公開](#publishing-viewer-presets)を参照してください。
>
>作成および追加した新しいすべてのビューアプリセットは、アクティベートされ公開されている必要があります。
>[ビューアプリセットのアクティベートとアクティベート解除](#activating-or-deactivating-viewer-presets)と[ビューアプリセットの公開](#publishing-viewer-presets)を参照してください。

<table>
 <tbody>
  <tr>
   <td><strong>ビューアプリセットのタイトル</strong></td>
   <td><strong>タイプ</strong></td>
   <td><strong>CSS ファイル名</strong><br /> </td>
  </tr>
  <tr>
   <td>Carousel_Dotted_dark</td>
   <td>カルーセルセット</td>
   <td><code>html5_carouselviewer_dotted_dark.css</code></td>
  </tr>
  <tr>
   <td>Carousel_Dotted_light</td>
   <td>カルーセルセット</td>
   <td><code>html5_carouselviewer_dotted_light.css</code></td>
  </tr>
  <tr>
   <td>Carousel_Numeric_dark</td>
   <td>カルーセルセット</td>
   <td><code>html5_carouselviewer_numeric_dark.css</code></td>
  </tr>
  <tr>
   <td>Carousel_Numeric_light</td>
   <td>カルーセルセット</td>
   <td><code>html5_carouselviewer_numeric_light.css</code></td>
  </tr>
  <tr>
   <td>フライアウト</td>
   <td>フライアウトズーム</td>
   <td><code>html5_flyoutviewer.css</code></td>
  </tr>
  <tr>
   <td>ImageSet_dark</td>
   <td>画像セット</td>
   <td><code>html5_zoomviewer_dark.css</code></td>
  </tr>
  <tr>
   <td>ImageSet_light</td>
   <td>画像セット</td>
   <td><code>html5_zoomviewer_light.css</code></td>
  </tr>
  <tr>
   <td>InlineMixedMedia_dark</td>
   <td>混在メディア</td>
   <td><code>html5_inlinemixedmediaviewer_dark.css</code></td>
  </tr>
  <tr>
   <td>InlineMixedMedia_light</td>
   <td>混在メディア</td>
   <td><code>html5_inlinemixedmediaviewer_light.css</code></td>
  </tr>
  <tr>
   <td>InlineZoom</td>
   <td>フライアウトズーム</td>
   <td><code>html5_inlinezoomviewer.css</code></td>
  </tr>
  <tr>
   <td>MixedMedia_dark</td>
   <td>混在メディア</td>
   <td><code>html5_mixedmediaviewer_dark.css</code></td>
  </tr>
  <tr>
   <td>MixedMedia_light</td>
   <td>混在メディア</td>
   <td><code>html5_mixedmediaviewer_light.css</code></td>
  </tr>
  <tr>
   <td>PanoramicImage</td>
   <td>パノラマ画像</td>
   <td><code>html5_panoramicimage.css</code></td>
  </tr>
  <tr>
   <td>PanoramicImageVR</td>
   <td>パノラマ画像</td>
   <td><code>html5_panoramicimage.css</code></td>
  </tr>
  <tr>
   <td>Shoppable_Banner</td>
   <td>インタラクティブ画像</td>
   <td><code>html5_interactiveimage.css</code></td>
  </tr>
  <tr>
   <td>Shoppable_Video_dark</td>
   <td>インタラクティブビデオ</td>
   <td><code>html5_interactivevideoviewer_dark.css</code></td>
  </tr>
  <tr>
   <td>Shoppable_Video_light</td>
   <td>インタラクティブビデオ</td>
   <td><code>html5_interactivevideovewer_light.css</code></td>
  </tr>
  <tr>
   <td>SpinSet_dark</td>
   <td>スピンセット</td>
   <td><code>html5_spinviewer_dark.css</code></td>
  </tr>
  <tr>
   <td>SpinSet_light</td>
   <td>スピンセット</td>
   <td><code>html5_spinviewer_light.css</code></td>
  </tr>
  <tr>
   <td><p>ビデオ</p> <p>（字幕サポートを含む）</p> </td>
   <td>ビデオ</td>
   <td><code>html5_videoviewer.css</code></td>
  </tr>
  <tr>
   <td><p>Video360_social</p> <p>（基本的なビデオ再生制御を含んでいます。ビデオレンダリングはステレオモードで行われます。手動の視点制御はオフですが、ジャイロスコープ制御はオンです。ソーシャルメディア機能はありません）</p> </td>
   <td>ビデオ 360</td>
   <td><code>html5_video360viewersocial.css</code></td>
  </tr>
  <tr>
   <td><p>Video360VR</p> <p>（仮想現実メガネを使用するエンドユーザー向けに設計されています。基本的なビデオ再生制御とソーシャルメディア機能を含んでいます）</p> </td>
   <td>ビデオ 360</td>
   <td><code>html5_video360viewer.css</code></td>
  </tr>
  <tr>
   <td><p>Video_social</p> <p>（字幕とソーシャルメディアのサポートを含む）</p> </td>
   <td>ビデオ</td>
   <td><code>html5_videoviewersocial.css</code></td>
  </tr>
  <tr>
   <td>Zoom_dark<br /> </td>
   <td>ズーム<br /> </td>
   <td><code>html5_basiczoomviewer_dark.css</code></td>
  </tr>
  <tr>
   <td>Zoom_light<br /> </td>
   <td>ズーム</td>
   <td><code>html5_basiczoomviewer_light.css</code></td>
  </tr>
  <tr>
   <td>ZoomVertical_dark<br /> </td>
   <td>垂直方向ズーム</td>
   <td><code>html5_zoomverticalviewer_dark.css</code></td>
  </tr>
  <tr>
   <td>ZoomVertical_light</td>
   <td>垂直方向ズーム</td>
   <td><code>html5_zoomverticalviewer_light.css</code></td>
  </tr>
 </tbody>
</table>

### サポートされているモバイルビューアのジェスチャーに関する表 {#supported-mobile-viewers-gestures-matrix}

iOS、Android™ 2.x および Android™ 3.x デバイスでサポートされているモバイルビューアジェスチャーを次の表に示します。

<table>
 <tbody>
  <tr>
   <td><strong>ジェスチャー</strong></td>
   <td><strong>フライアウトズーム</strong></td>
   <td><strong>ズーム</strong></td>
   <td><strong>スピン</strong></td>
  </tr>
  <tr>
   <td><p><strong>ドラッグ</strong></p> </td>
   <td><p>パン</p> </td>
   <td><p>パン</p> </td>
   <td><p>パン</p> </td>
  </tr>
  <tr>
   <td><p><strong>タップ</strong></p> </td>
   <td><p>フライアウトウィンドウを表示</p> </td>
   <td><p>ユーザーインターフェイスを表示または非表示</p> </td>
   <td><p>ユーザーインターフェイスを表示または非表示</p> </td>
  </tr>
  <tr>
   <td><p><strong>ダブルタップ</strong></p> </td>
   <td><p>適用なし</p> </td>
   <td><p>ズームインまたはリセット</p> </td>
   <td><p>ズームインまたはリセット</p> </td>
  </tr>
  <tr>
   <td><p><strong>ピンチオープン</strong></p> </td>
   <td><p>適用なし</p> </td>
   <td><p>ズームイン（iOS、Android™ 3x のみ）</p> </td>
   <td><p>ズームイン（iOS、Android™ 3x のみ）</p> </td>
  </tr>
  <tr>
   <td><p><strong>ピンチクローズ</strong></p> </td>
   <td><p>適用なし</p> </td>
   <td><p>ズームアウト（iOS、Android™ 3x のみ）</p> </td>
   <td><p>ズームアウト（iOS、Android™ 3x のみ）</p> </td>
  </tr>
  <tr>
   <td><p><strong>スワイプ</strong></p> </td>
   <td><p>スイッチバーをスクロール</p> </td>
   <td><p>画像をスクロール</p> </td>
   <td><p>スピン</p> </td>
  </tr>
  <tr>
   <td><p><strong>フリック</strong></p> </td>
   <td><p>スイッチバーをスクロール</p> </td>
   <td><p>画像をスクロール</p> </td>
   <td><p>スピン</p> </td>
  </tr>
 </tbody>
</table>

## 表示されるビューアプリセットの数の増減 {#increasing-the-number-of-viewer-presets-that-display}

**[!UICONTROL 詳細ビュー]**／**[!UICONTROL ビューア]**&#x200B;でアセットを表示したとき、Adobe Experience Manager には様々なビューアプリセットが表示されます。表示されるビューアの数を増減できます。

**表示されるビューアプリセットの数を増減させるには：**

1. CRXDE Lite（[https://localhost:4502/crx/de](https://localhost:4502/crx/de)）に移動します。
1. ビューアプリセットリストノード（`/libs/dam/gui/coral/content/commons/sidepanels/viewerpresets/viewerpresetslist`）に移動します。

   ![chlimage_1-221](/help/assets/dynamic-media/assets/chlimage_1-221.png)

1. 「**[!UICONTROL limit]**」プロパティで、「**[!UICONTROL 値]**」（デフォルトで 15 に設定されています）を目的の数に変更します。
1. ビューアプリセットデータソース（`/libs/dam/gui/coral/content/commons/sidepanels/viewerpresets/viewerpresetslist/datasource`）に移動します。

   ![chlimage_1-222](/help/assets/dynamic-media/assets/chlimage_1-222.png)

1. 「limit」プロパティの数を、目的の数（例：`{empty requestPathInfo.selectors[1] ? "20" : requestPathInfo.selectors[1]}`）に変更します。
1. 「**[!UICONTROL すべて保存]**」を選択します。

## ビューアプリセットの作成 {#creating-a-new-viewer-preset}

ビューアプリセットを作成しておくと、アセットの表示やアセットとの対話のための様々な設定を適用できます。ただし、ビューアプリセットを作成する必要はありません。デフォルトの、すぐに使えるビューアプリセットが既に Adobe Experience Manager Assets に付属していますので、これを使用できます。

ビューアプリセットの作成を選んだ場合、ビューアプリセットを保存すると、ビューアプリセットページのそのビューアの状態が自動的にアクティベート済みになります（「**[!UICONTROL オン]**」に設定されます）。この状態は、画像やビデオをプレビューするときは常に Dynamic Media コンポーネントとインタラクティブメディアコンポーネントに表示されることを意味します。

一部のビューアプリセットには、ビューアの全体的な動作に影響する専用の設定があります。作成するビューアプリセットによっては、これらの特別な考慮事項について注意する必要があります。

[インタラクティブビューアプリセットの作成に関する考慮事項](#special-considerations-for-creating-an-interactive-viewer-preset)を参照してください。

[カルーセルバナーのビューアプリセットの作成に関する考慮事項](#special-considerations-for-creating-a-carousel-banner-viewer-preset)を参照してください。

**ビューアプリセットを作成するには：**

1. Adobe Experience Manager の左上隅にある Adobe Experience Manager ロゴを選択し、左のレールで&#x200B;**[!UICONTROL ツール]**（ハンマーのアイコン）／**[!UICONTROL アセット]**／**[!UICONTROL ビューアプリセット]**&#x200B;に移動します。

   ![6_5_viewerpresets](assets/6_5_viewerpresets.png)

1. ビューアプリセットページのツールバーで、「**[!UICONTROL 作成]**」を選択します。
1. **[!UICONTROL 新規ビューアプリセット]**&#x200B;ダイアログボックスで、「**[!UICONTROL プリセット名]**」フィールドに新しいプリセットの名前を入力します。名前は慎重に選択してください。「**[!UICONTROL 作成]**」を選択した後で編集することはできません。

   後述の手順でプリセットを保存すると、この名前がビューアプリセットページの「プリセットのタイトル」列ヘッダーの下に表示されます。

1. 「リッチメディアタイプ」ドロップダウンメニューで、作成するビューアプリセットのタイプを選択し、ページ右上隅の「**[!UICONTROL 作成]**」を選択します。

   [ビューアプリセットのリッチメディアタイプ](#rich-media-types-for-viewer-presets)を参照してください。

1. ビューアプリセットエディターページで、「**[!UICONTROL 外観]**」タブを選択します。
1. 次のいずれかの操作を行います。

   * 「**[!UICONTROL 選択したタイプ]**」プルダウンメニューで、ビジュアルデザインをカスタマイズするコンポーネントを選択します。または、設定するビジュアル要素をビューアで選択することもできます。

      Visual Editor を使用すると、特定のプロパティがスタイルに与える効果を確認できます。プロパティを設定または調整すると、Visual Editor の左にあるサンプルを使用して、ビューア上での効果を瞬時に確認できます。

      ビューアプリセットタイプごとの CSS スタイル設定プロパティについては、『[ビューアリファレンスガイド](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources.html)』の「*`<viewer name>`* ビューアのカスタマイズ」のヘルプトピックを参照してください。例えば、`Mixed_Media` タイプのビューアプリセットを作成している場合、プロパティのリストと各プロパティの説明については、[混在メディアビューアのカスタマイズ](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/viewers-aem-assets-dmc/mixed-media/customing-mixed-media/c-html5-mixedmedia-viewer-customizingviewer.html?lang=ja)を参照してください。

   * スタイル設定を別個の CSS ファイルで定義している場合は、その CSS ファイルを Adobe Experience Manager Assets にアップロードできます。アップロードした CSS ファイルを探してビューアプリセットと関連付けるには、「**[!UICONTROL 選択したタイプ]**」プルダウンメニューの下の「**[!UICONTROL CSS を読み込み]**」を選択します（必要に応じて、ビジュアルエディターを上にスクロールして表示します）。

      CSS ファイルを読み込むと、Visual Editor は、その CSS に正しいビューアマーカーが使用されているかを確認します。例えば、ズームビューアを作成している場合、読み込むすべての CSS ルールが、親のビューアエレメントに定義されているズームビューアのクラス名 `.s7mixedmediaviewer` を使用して定義されている必要があります。

      指定ビューアの CSS マーカーが正しく定義された CSS であれば、自作した任意の CSS を読み込むことができます（CSS マーカーについては、『[ビューアリファレンスガイド](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources.html)』の「*&lt;viewer name>* ビューアのカスタマイズ」のヘルプトピックを参照してください。例えば、ズームビューアの CSS マーカーについては、[ズームビューアのカスタマイズ](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/viewers-aem-assets-dmc/zoom/customizing-zoom/c-html5-20-zoom-viewer-customizingviewer.html?lang=ja)を参照してください）。ただし、Visual Editor が一部の CSS 値を認識できない可能性もあります。そのような場合、Visual Editor は、CSS が正常に機能するように、エラーを上書きしようとします。
   >[!NOTE]
   >
   >RAW 形式で CSS を直接編集する場合は、「選択したタイプ」プルダウンメニューの下の「**[!UICONTROL CSS を表示／非表示]**」を選択します（必要に応じて、ビジュアルエディターを上にスクロールして表示します）。
   >Visual Editor と同様に、CSS でプロパティを直接変更すると、ビューアサンプルにその効果がすぐに反映されます。また、同時に、Visual Editor でもその同じプロパティが自動的に更新されます。このことから、RAW である CSS エディターと、Visual Editor のどちらを使用しても、また交互に使用してもかまいません。

   >[!NOTE]
   >
   >ボタンのアートワークの場合は、2 倍画像を選択し、高解像度のアートワークをアップロードします。インタラクティブ画像やショッパブルバナーを操作する場合は、すぐに使える様々なホットスポットボタンから選択することもできます。

1. （オプション）ビューアプリセットを編集ページの最上部の近くにある「**[!UICONTROL デスクトップ]**」、「**[!UICONTROL タブレット]**」または「**[!UICONTROL 電話]**」を選択して、異なる種類のデバイスや画面のビジュアルスタイルを個別に定義します。
1. ビューアプリセットエディターページで、「**[!UICONTROL ビヘイビアー]**」タブを選択します。または、設定するビジュアル要素をビューアで選択することもできます。
1. 「**[!UICONTROL 選択したタイプ]**」プルダウンメニューで、動作を変更するコンポーネントを選択します。

   Visual Editor 内の多くのコンポーネントには、詳しい説明が関連付けられています。この説明は、コンポーネントを展開して関連パラメーターを表示したときに、青いボックス内に示されます。

   一部のビューアタイプには、「**[!UICONTROL IS コマンド]**」テキストフィールドに画像サービングコマンドを指定できるコンポーネントがあります。使用できるコマンドのリストについては、[画像サービング API リファレンス（英語）](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/c-is-home.html?lang=ja)を参照してください。

   >[!NOTE]
   >
   >**スマートフォンやタブレットなどのタッチデバイスを使用している場合は...**
   >
   >
   >テキストフィールドに値を入力後、ユーザーインターフェイス内を選択すると、変更内容が送信され、仮想キーボードが閉じられます。**[!UICONTROL Enter]** キーを押した場合は、何も実行されません。

1. ページの右上隅にある「**[!UICONTROL 保存]**」を選択します。
1. 新しいビューアプリセットを公開します。プリセットを Web サイトで使用するには、まずそのプリセットを公開する必要があります。

   [ビューアプリセットの公開](#publishing-viewer-presets)を参照してください。

### インタラクティブビデオのビューアプリセットの作成に関する考慮事項 {#special-considerations-for-creating-an-interactive-viewer-preset}

**パネル内の画像サムネールのディスプレイモードについて:**

インタラクティブビデオビューアプリセットを作成または編集する場合は、使用する表示モード設定を選択できます。この選択を行うのは、「**[!UICONTROL 動作]**」タブの「**[!UICONTROL 選択したコンポーネント]**」プルダウンメニューから `InteractiveSwatches` を選択したときです。選択するディスプレイモードは、ビデオの再生中にサムネールを表示する方法とタイミングに影響します。`segment` ディスプレイモード（デフォルト）または `continuous` ディスプレイモードのいずれかを選択できます。

<table>
 <tbody>
  <tr>
   <td><strong>ディスプレイモード</strong></td>
   <td><strong>説明</strong></td>
  </tr>
  <tr>
   <td>セグメント</td>
   <td><p><code>Segment </code>は、既製のインタラクティブビデオビューアプリセット <code>Shoppable_Video_light</code> と <code>Shoppable_Video_dark</code> および自身で作成するすべてのインタラクティブビデオビューアプリセットのデフォルトのディスプレイモードです。</p> <p>このモードで、ビデオセグメントに割り当てられているサムネールの数が、ディスプレイパネルに表示されるスポットの数よりも少ないとします。そのような場合、次または前のサブセグメントのサムネールがパネル内の空白部分を埋めるために取り込まれることは<i>ありません</i>。つまり、特定のビデオセグメントに割り当てられたスウォッチの表示を保持します。</p> </td>
  </tr>
  <tr>
   <td>連続</td>
   <td><p><code>continuous </code> ディスプレイモードで、セグメント内のサムネールの数が、パネルに表示される数より少ないとします。そのような場合、ビューアには、次のセグメントまたは前のセグメント（前回のサムネールが表示された場所）からのサムネールの表示が自動的に含まれます。</p> <p><a href="/help/assets/dynamic-media/interactive-videos.md">このトピックの</a>ビデオは <code>continuous </code> ディスプレイモードの一例です。</p> </td>
  </tr>
 </tbody>
</table>

**インタラクティブビデオビューアの自動スクロール動作について:**

インタラクティブビデオビューア内のサムネールの自動スクロール動作は、選択したディスプレイモードとは独立して機能します。

インタラクティブビデオのビューアプリセットを作成または編集するときは、「ビヘイビアー」タブから自動スクロールにアクセスします。**[!UICONTROL 選択したコンポーネント]**&#x200B;ドロップダウンメニューの「ビヘイビアー」タブで、「**[!UICONTROL InteractiveSwatches]**」を選択します。「自動スクロール」チェックボックスは「IS コマンド」テキストフィールドの下にリストされます。

ビューアプリセットで「**[!UICONTROL 自動スクロール」]**&#x200B;を無効（チェックボックスをオフ）にした場合、ユーザーによるビデオの再生中、パネルにはビデオの全長につき最初のサムネール画像のみが表示されます。ただし、ユーザーは必要に応じて上下の矢印アイコンを使用してサムネール間を手動でスクロールできます。

ビューアプリセットで「**[!UICONTROL 自動スクロール]**」を有効（チェックボックスをオン）にすると、ビデオの再生中、セグメントの開始時に、ビデオセグメントに割り当てられたサムネール画像まで表示がスクロールされます。ただし、セグメントによっては特定のサムネールが前後のサムネールの 2 倍の時間表示されることもあります。この動作は、セグメント内のサムネールの数がパネルに表示される数よりも多く、均等に分割できないことが原因で発生します。

説明のために、30 秒のビデオセグメントが 1 つあるとします。30 秒の間に表示されるサムネールは合計で 9 個です。ブラウザーは 4 つのサムネールがディスプレイパネルに表示できるようにサイズ設定されています。30 秒のビデオの時間セグメントは 3 つのサブセグメントに分割されています。次の表に、指定の時間サブセグメントに表示されるサムネールの内訳を示します。

| **ビデオサブセグメント** | **サブセグメント時間（秒単位）** | **パネルに表示されるサムネール** |
|---|---|---|
| 1 | 0～10 | 1、2、3、4 |
| 2 | 10～20 | 4、5、6、7 |
| 3 | 20～30 | 6、7、8、9 |

ビデオサブセグメント 3 が、割り当てられているサムネールを超えて拡張されることはありません。また、サムネール 4、6、7 は、他のサムネールの 2 倍の時間パネルに表示されます。

ビューアでは次のロジックに従い、サイドパネルに表示できる数に基づいて表示するサムネールの数を決めています。

* サブセグメントの数 = 次のサブセグメントに切り上げ（サムネールの数／サムネールパネル内に表示されるスロットの数（ブラウザー画面のサイズに基づく））前述の表の例では、「9 サムネール / 4 スロット = 2.25」になります（ビューアのロジックにより 2.25 が 3 サブセグメントに切り上げられます）。

* サムネールの数 = 次のサムネールに切り上げ（サムネールの数／ビデオサブセグメントの数）前述の表の例では、「9 サムネール / 3 ビデオサブセグメント = 3 サムネール」になります。

* サブセグメントの表示時間 = ビデオの合計再生時間 / ビデオサブセグメントの数
前述の表の例では、「30 秒 / 3 ビデオサブセグメント = 各ビデオサブセグメントで 10 秒」の再生時間になります。

#### カルーセルバナーのビューアプリセットの作成に関する特別な考慮事項 {#special-considerations-for-creating-a-carousel-banner-viewer-preset}

カルーセルバナーのビューアプリセットを作成するときに、ホットスポットのスタイル変更は次のように実行できます。

|  | **説明** | **アクション** |
|---|---|---|
| **[!UICONTROL ホットスポットアイコン]** | ホットスポットに使用するアイコンを変更する | ホットスポットアイコンの画像を変更するには、「**[!UICONTROL 外観]**」タブで、「**[!UICONTROL 選択したコンポーネント]**」の「**[!UICONTROL ImageMapEffect]**」を選択します。「**[!UICONTROL アイコン]**」で「**[!UICONTROL 背景]**」を選択し、「**[!UICONTROL 画像]**」フィールドで目的に背景画像に移動します。 |

## ビューアプリセットのアクティベートまたはアクティベート解除 {#activating-or-deactivating-viewer-presets}

オーサーモードでビューアプリセットがアクティベートされているかどうかで、ユーザーインターフェイスに表示されるビューアプリセットが変わります。デフォルトでは、ビューアプリセットは作成後に「オン」になります。プリセットをオフにすると、オーサーモードでは表示されなくなります。プリセットを公開する場合は、オン／オフに関係なく、常に公開されます。リストの項目が多すぎる場合や、特定のビューアプリセットを使用できないようにする場合は、ビューアプリセットをアクティベート解除します。

**ビューアプリセットをアクティベートまたはアクティベート解除するには：:**

1. Adobe Experience Manager の左上隅にある Adobe Experience Manager ロゴを選択し、左のレールで&#x200B;**[!UICONTROL ツール]**（ハンマーのアイコン）／**[!UICONTROL アセット]**／**[!UICONTROL ビューアプリセット]**&#x200B;を選択します。
1. ビューアプリセットページの「**[!UICONTROL 状態]**」列ヘッダーの下で、ビューアプリセットのアクティベートとアクティベート解除の切り替えアイコンを選択します。

   アクティベートされたビューアプリセットには、青いボックス内で、右側にトグルしたアイコンが示されます。アクティベート解除されたビューアプリセットには、薄いグレーのボックス内で、左側にトグルしたアイコンが示されます。

## ビューアプリセットの公開 {#publishing-viewer-presets}

ビューアプリセットの状態をアクティベートする（または「オン」に切り替える）と、Dynamic Media コンポーネントとインタラクティブメディアコンポーネント内、およびアセットを表示する際に表示されるようになります。

ただし、ビューアプリセットを使用しているアセットを&#x200B;*配信*&#x200B;するには、そのビューアプリセットも公開する必要があります。URL を取得したりアセットのコードを埋め込むには、すべてのビューアプリセットをアクティベートし、*かつ*&#x200B;公開する必要があります。Dynamic Media に付属しているすべての標準ビューアプリセットをアクティベートして公開します。自分で作成して追加したカスタムビューアプリセットは自動的にアクティベートされますが、やはり手動で公開する必要があります。

[ビューアプリセットのアクティベートとアクティベート解除](#activating-or-deactivating-viewer-presets)を参照してください。

[アセットのプレビュー](/help/assets/dynamic-media/previewing-assets.md)も参照してください。

**ビューアプリセットを公開するには：:**

1. Adobe Experience Manager の左上隅にある Adobe Experience Manager ロゴを選択し、左のレールで&#x200B;**[!UICONTROL ツール]**（ハンマーのアイコン）／**[!UICONTROL アセット]／[!UICONTROL ビューアプリセット]**&#x200B;を選択します。
1. 公開するビューアプリセットを 1 つ以上選択します。
1. ツールバーの&#x200B;**[!UICONTROL 公開]**&#x200B;アイコンを選択します。

## ビューアプリセットの並べ替え {#sorting-viewer-presets}

1. Adobe Experience Manager の左上隅にある Adobe Experience Manager ロゴを選択し、左のレールで&#x200B;**[!UICONTROL ツール]**（ハンマーのアイコン）／**[!UICONTROL アセット]／[!UICONTROL ビューアプリセット]**&#x200B;を選択します。
1. 「**[!UICONTROL プリセットのタイトル]**」、「**[!UICONTROL タイプ]**」、「**[!UICONTROL 公開]**」または「**[!UICONTROL 状態]**」を選択して、その見出しの列でソートします。例えば、「**[!UICONTROL タイプ]**」を選択すると、ビューアプリセットのタイプが、アルファベット順で、またはアルファベットの逆の順序でソートされます。

## ビューアプリセットの編集 {#editing-viewer-presets}

*事前に定義された標準提供ビューアプリセット*&#x200B;を編集するシナリオはサポートされていません。標準提供ビューアプリセットを編集すると、新しい名前で保存するように指示されます。

**ビューアプリセットを編集するには：:**

1. Adobe Experience Manager の左上隅にある Adobe Experience Manager ロゴを選択し、左のレールで&#x200B;**[!UICONTROL ツール]**（ハンマーのアイコン）／**[!UICONTROL アセット]**／**[!UICONTROL ビューアプリセット]**&#x200B;を選択します。
1. ビューアプリセットのタイトルの左側にあるチェックボックスをオンにして、プリセットを選択します。
1. ツールバーの「**[!UICONTROL 編集]**」を選択します。
1. **[!UICONTROL ビューアプリセットエディター]**&#x200B;ページで、「**[!UICONTROL 外観]**」タブと「**[!UICONTROL 動作]**」タブのオプションを使用して、必要な変更をビューアプリセットに加えます。

   「**[!UICONTROL 外観]**」タブで、ビューアプリセットエディターページの左上隅近くにある「**[!UICONTROL デスクトップ]**」、「**[!UICONTROL タブレット]**」、「**[!UICONTROL 電話]**」のいずれかを選択して、アセットの表示モードを変更します。

1. ページの右上隅近くで、次のいずれかの操作を行います。

   * 「**[!UICONTROL 保存]**」を選択して変更内容を保存し、ビューアプリセットページに戻ります。
   * 「**[!UICONTROL キャンセル]**」を選択して変更内容をキャンセルし、ビューアプリセットページに戻ります。

## カスタムビューアプリセットの削除 {#deleting-custom-viewer-presets}

作成して Dynamic Media に追加したビューアプリセットを削除できます。

**カスタムビューアプリセットを削除するには：:**

1. Adobe Experience Manager の左上隅にある Adobe Experience Manager ロゴを選択し、左のレールで&#x200B;**[!UICONTROL ツール]**（ハンマーのアイコン）／**[!UICONTROL アセット]／[!UICONTROL ビューアプリセット]**&#x200B;を選択します。
1. ビューアプリセットページで、「プリセットのタイトル」のチェックボックスをオンにして、**[!UICONTROL ごみ箱]**&#x200B;アイコンを選択します。
1. 「**[!UICONTROL 削除]**」を選択します。

## アセットへのビューアプリセットの適用 {#applying-a-viewer-preset-to-an-asset}

アセットと選択したビューアを既に公開している場合は、ビューアプリセットの選択後に「**[!UICONTROL URL]**」ボタンと「**[!UICONTROL 埋め込み]**」ボタンが表示されます。

**アセットにビューアプリセットを適用するには:**

1. アセットを開き、ページの左上隅付近にあるドロップダウンメニュー選択して、「**[!UICONTROL ビューア]**」を選択します。

   >[!NOTE]
   >
   >アセットと選択したビューアを既に公開している場合は、ビューアプリセットの選択後に「**[!UICONTROL URL]**」ボタンと「**[!UICONTROL 埋め込み]**」ボタンが表示されます。

1. アセットに適用するビューアプリセットを左側のパネルから選択します。

   [この URL をコピー](/help/assets/dynamic-media/linking-urls-to-yourwebapplication.md)して、他のユーザーと共有できます。

## ビューアプリセットを使用するアセットの配信 {#delivering-assets-with-viewer-presets}

ビューアプリセットの URL を取得する方法については、[Web アプリケーションへの URL のリンク](/help/assets/dynamic-media/linking-urls-to-yourwebapplication.md)を参照してください。[Web ページへのビデオビューアの埋め込み](/help/assets/dynamic-media/embed-code.md)も参照してください。

Adobe Experience Manager を WCM として使用している場合は、ビューアプリセットを使用するアセットをページに直接追加できます。[ページへの Dynamic Media アセットの追加](/help/assets/dynamic-media/adding-dynamic-media-assets-to-pages.md)を参照してください。
