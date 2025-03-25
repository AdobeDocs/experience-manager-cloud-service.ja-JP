---
title: Dynamic Media へのジャーニー、パート 2
description: Dynamic Media ジャーニーでは、Dynamic Media の基本的な仕組み、Dynamic Media で可能なこと、仕事や顧客にもたらす価値について説明します。
contentOwner: Rick Brough
products: Experience Manager as a Cloud Service
topic-tags: introduction,administering
content-type: reference
feature: Image Profiles,Best Practices
role: User, Admin
mini-toc-levels: 4
hide: false
hidefromtoc: false
exl-id: cdca41ad-a2cd-4f68-aaa4-5eec33c30f0b
source-git-commit: 36ab36ba7e14962eba3947865545b8a3f29f6bbc
workflow-type: tm+mt
source-wordcount: '2621'
ht-degree: 100%

---

# Dynamic Media ジャーニー：基礎知識、第 2 部  {#dm-journey-part2}

{{see-also-dm}}

Dynamic Media ジャーニー：基礎知識、第 2 部へようこそ。ここでは次のことを学ぶことができます。

* Dynamic Media URL と Dynamic Media のコンテンツ配信方法の詳細。
* アセットをレンダリングするための画像プリセットの作成の基本。
* 画像セット、スピンセット、混在メディアセット。

[Dynamic Media ジャーニー：基礎知識、第 1 部](/help/assets/dynamic-media/dm-journey-part1.md)も参照してください。

>[!TIP]
>
>最良の結果を得るには、デスクトップコンピューターでこの Dynamic Media ジャーニーを表示して読むことをお勧めします。

## Dynamic Media URL の分解と Dynamic Media のコンテンツ配信方法 {#dm-journey-d}

Dynamic Media アセットをアップロードして公開した後、アセットの生成された URL をコピーし、ブラウザーに貼り付けて、アセットが顧客にどのように表示されるかを確認できます。次に示す腕時計画像の URL のコピーは、読みやすく理解しやすくするために、色分けされています。

![Dynamic Media URL の分解](/help/assets/dynamic-media/assets/dm-colored-url.png)
_Dynamic Media URL の分解。_

URL の最初の部分（赤）は、サーバードメイン自体を参照しています。In this case, Dynamic Media is running on a generic server domain, which is `https://s7d1.scene7.com/is/image/`. 一連の画像を見て、サーバードメインを調べるだけで、Dynamic Media で配信されているかどうかを簡単に理解できます。URL はかなり一貫しています。ただし、Dynamic Media のお客様の一部は、`name-of-your-company.scene7.com`.のように、専用のサーバードメインに切り替えている場合もあります。スマートイメージングには専用のサーバードメインが必要です。

アカウント名は紫色の部分です。この場合、アカウントは `jpearldemo` です。

アセット ID または名前 `AdobeStock_28563982` は緑色です。アセットには `.png` または `.jpg` のようなファイル拡張子は&#x200B;_付きません_。アセットが Dynamic Media に取り込まれると、ファイル拡張子が削除され、別の種類のファイル、ピラミッド型 TIFF ファイルが作成されます。ピラミッド型 TIFF を使用すると、Dynamic Media は即座にレンディションを作成できます。

最後に、画像処理パラメーター `?wid=1000&fmt=jpeg&qlt=85` が、末尾の黄色です。

この URL パスは実稼働しています。[試してみる](https://s7d1.scene7.com/is/image/jpearldemo/AdobeStock_28563982?wid=1000&amp;fmt=jpeg&amp;qlt=85){target="_blank"}。

お使いのブラウザーウィンドウで Dynamic Media URL と腕時計の画像を開いたままにしておきます。URL を変更するだけで、画像のレンディションを作成する方法を詳しく見てみます。

### URL を使用した腕時計画像のレンダリング

最初に、URL パス内の画像処理ルールのみを手動で削除します。サーバー名、アカウント名、アセット ID または画像名はそのままにします。[試してみる](https://s7d1.scene7.com/is/image/jpearldemo/AdobeStock_28563982){target="_blank"}。

次に、URL の末尾に画像処理パラメーターを追加します。URL フィールドで、画像名の右側に「`?wid=500`」と入力し、**[!UICONTROL Enter]** キーを押します。[試してみる](https://s7d1.scene7.com/is/image/jpearldemo/AdobeStock%5F28563982?wid=500){target="_blank"}。

時計の新しいレンディションが生成されます。この簡単な演習で理解するべき重要な点は、画像の幅を変更すると、表示される画像が 100% 動的に生成されることです。

次に、幅の値 `500` ピクセルを `1000` ピクセルに変更し、**[!UICONTROL Enter]** キーを押します。[試してみる](https://s7d1.scene7.com/is/image/jpearldemo/AdobeStock%5F28563982?wid=1000){target="_blank}。
**[!UICONTROL Enter]** キーが押された瞬間、ブラウザーは Dynamic Media Image Server に戻ります。入力した新しい幅の値に基づいて、新しいレンディションの時計が生成され、新しい画像がブラウザーに配信されてキャッシュされます。

Dynamic Media には、web ページ上の画像アセットの微調整に使用できる、多数の画像処理パラメーターがあります。[こちらからリストを確認](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/http-protocol-reference/command-reference/c-command-reference.html?lang=ja)できます。

次に、時計の画像に回転パラメーターを追加してみます。URL パスの末尾、`wid=1000` の直後に、`&rotate=90` と入力して **[!UICONTROL Enter]** キーを押します。[試してみる](https://s7d1.scene7.com/is/image/jpearldemo/AdobeStock%5F28563982?wid=1000&amp;rotate=9){target="_blank"}。

時計はまだ少し左に歪んでいます。回転の値を `90` から `92` に変更し、**[!UICONTROL Enter]** キーを押します。[試してみる](https://s7d1.scene7.com/is/image/jpearldemo/AdobeStock%5F28563982?wid=1000&amp;rotate=9){target="_blank"}。

先ほどと同様に、**[!UICONTROL Enter]** キーが押された瞬間に、新しいレンディションの腕時計がほぼ瞬時に生成されます。Dynamic Media が 80 万件を超える画像リクエストを、混雑する週末や主要な休日でも&#x200B;_秒_&#x200B;単位で配信できる理由は、このようなパフォーマンスにあります。

画像ごとに URL 内の画像処理パラメーターを変更できますが、web サイトを構成する画像が数万点ある場合などはあまり効率的な方法ではありません。画像プリセットを使用する方法がはるかに効率的です。

## アセットをレンダリングするための画像プリセットの作成の基本 {#dm-journey-e}

画像を作成する方法と利用可能にする場所は複数あります。従来、クリエイティブは Adobe Photoshop に移動し、各レンディションを静的画像として保存します。

![静的画像](/help/assets/dynamic-media/assets/dm-static-images.png)
_良好：静止画をそれぞれ手動で作成。_

さて、クリエイティブディレクターが画像を見てこう言ったとしましょう。

_「実は、時計の文字盤を見やすくするために、長針が 4 を、短針が 1 を指すように撮りたかったんだ」_

クリエイティブでは、すべての新しい静的画像を再度撮影する必要があります。

しかし、Dynamic Media では、異なる画像プリセットがあれば、必要な場所でそれらの画像を使用できます。画像プリセットには標準が適用されます。

![プライマリファイルのアプローチ](/help/assets/dynamic-media/assets/dm-onefile.png)
_最良：1 つのファイルに、`Search_Grid` や `Thumbnail` などの画像プリセットを使ってその場で作成された複数のレンディション。_

| **画像プリセットを使用する理由** | |
|---|---|
| 標準規格 | 画像プリセットでは、要求された画像に対して標準画像処理が適用されます。 |
| 変更管理 | 画像処理を変更する必要がある場合は、既存の画像プリセットのパラメーターを編集するだけです。更新された定義は、自動的にすべてのリクエストに反映されます。 |

特定のタイプの画像が必要な場所の例を以下に示します。

* 製品の詳細ページ
* 検索グリッド
* サムネイル
* 買い物かご
* ヒーロー画像

画像を使用する場所に対して、同じパラメーターを使用してその画像が配信されます。

ここで、Dynamic Media での画像プリセットの作成方法を見てみましょう。

![「基本」タブから始まる画像プリセットの作成](/help/assets/dynamic-media/assets/dm-image-preset-basictab.png)
_「基本」タブから始まる画像プリセットの作成_

上の例で、「_Medium_」という名前で新しい画像プリセットが作成されたことがわかります。Dynamic Media では、標準搭載の画像（バックパック）の例を使用して、画像プリセットの作成時に特性を確認できます。

この「_Medium_」画像プリセットの幅は 500 ピクセル、高さは 800 ピクセルです。このジャーニーの第 1 部では、様々な形式でのアセットの配信について説明します。「**[!UICONTROL 形式]**」プルダウンメニューから、JPEG、PNG、TIFF またはその他の複数の形式でアセットを配信するよう選択できます。これには柔軟性があります。

「**[!UICONTROL 詳細]**」タブを選択すると、アセットのカラースペースに関するオプションが表示されます。「**[!UICONTROL 基本]**」タブで選択した形式に応じて（上の例では JPEG が選択されています）、アセットを、RGB、グレースケールまたは CMYK で配信できます。「**[!UICONTROL カラープロファイル]**」プルダウンメニューから、印刷に使用する CMYK 画像アセットの配信方法を選択できます。また、画像をシャープにするために適用できる追加のパラメーターもあります。この例では、「**[!UICONTROL アンシャープマスク]**」が適用されました。

![「詳細」タブのオプションを選択して画像プリセットを作成](/help/assets/dynamic-media/assets/dm-image-preset-advancedtab.png)
_「詳細」タブのオプションを選択して画像プリセットを作成。_

先ほどの [Dynamic Media URL の分解](#dm-journey-d)では、Dynamic Media URL とその構成方法について説明しました。この「**[!UICONTROL 画像の修飾子]**」テキストボックスに、必要な追加の画像処理パラメーターを入力できます。パラメーターは、プリセットを使用して画像を配信する際に、URL のプリセット名に含まれます。上のスクリーンショットでは、パラメーター `bgc=451B15` が追加されました。つまり、暗い茶色の背景色が追加されました。

画像プリセットは、画像のレシピと考えることができます。プリセットを使用する画像は、常に、一貫性のある同じ方法で配信されます。また、パラメーター `&op_brightness=+10` が、明るさを少し増やすために追加されました。

完了したら、プリセットを保存すると、既存のすべての画像で使用できるようになります。この例では、_Medium_ 画像プリセットを、液体チョコレートが入ったボウルの画像に適用します。

![画像プリセット *Medium* を適用して、画像のレンディションを生成](/help/assets/dynamic-media/assets/dm-medium-image-preset.png)
_画像プリセット Medium を適用して、画像のレンディションを生成。_

URL をコピーし、それをブラウザーに貼り付けて、画像の外観を確認します。[試してみる](http://s7d1.scene7.com/is/image/jpearldemo/AdobeStock_74043302?$Medium$){target="_blank"}。

ブラウザーで、フル URL パスに画像プリセットの名前 _Medium_ が表示されます。

表示された画像の鮮明さを確認できると思います。この品質は、チョコレートボウルを撮影した方法に一部起因します。また、Dynamic Media では、デジタルチャネルに配信される画像よりも大きな画像を保存できることも一因です。

チョコレートボウルの表示に納得したら、web ページで画像を表示する場所に URL を貼り付けます。

下の時計の画像を再確認する、`Cart` 画像プリセット、`Grid` プリセット、`Large` プリセット、`PDP-page`（製品の詳細ページ）プリセットなどがあります。

![静的および動的画像プリセット](/help/assets/dynamic-media/assets/dm-image-presets.png)
_静的および動的画像プリセット。時計の画像は、`PDP-page` 画像プリセットを使用してレンダリングされました。_

しかし、web サイト上の画像を変更する必要がある場合はどうしますか？例えば、テストを完了し、120 x 120 の画像（`Cart` 画像プリセット）が予想どおりに受信されていないことがわかったとします。幅を 175 ピクセルに、高さを 175 ピクセルに増やして、画像を大きくする必要があります。従来は、Adobe Photoshop を開き、買い物かごの画像をすべて再作成する必要がありました。しかし、Dynamic Media では、画像プリセットを編集するだけです。次の例に示すように、幅と高さの値を 175 に更新して、プリセットを保存します。

![画像プリセットの編集](/help/assets/dynamic-media/assets/dm-edit-image-preset.png)
_`Cart` 画像プリセットの幅と高さの編集。_

画像プリセットを変更してキャッシュをフラッシュした後、すべての画像が更新されますが、そのプリセットで使用されている URL は、どれも&#x200B;_変更されません_。つまり、リンク切れはなく、web ページのリダイレクトも不要です。

## 画像セット、スピンセット、混在メディアセット {#dm-journey-f}

Dynamic Media には、画像セット、スピンセット、混在メディアセットを作成する機能があり、より一般的な使用法です。

画像セットは、通常、一連の画像アセットで構成され、単一のエンティティとして表示されます。このようなセットは、ユーザーに対して統一された視聴エクスペリエンスを提供します。ユーザーはこのエクスペリエンスで、サムネイル画像をクリックしてアイテムの様々なビューを表示できます。画像セットによって、アイテムの別のビューを表示できます。ビューアでは、画像をより詳しく確認するためのズームツールを利用できます。[Flyout ビューアを使用する「Running」という画像セットを表示します](https://s7d1.scene7.com/s7viewers/html5/FlyoutViewer.html?asset=jpearldemo/Running)。

Dynamic Media の中にランニングシューズの画像がいくつかあります。これは、セールスおよびマーケティング部門が、単一のプレゼンテーション、すなわち画像セットとして顧客に表示したい製品シリーズです。

![画像セットの作成](/help/assets/dynamic-media/assets/dm-create-image-set.png)
_画像セットの作成の開始。_

画像セットを作成するには、「**[!UICONTROL 作成]**」プルダウンメニューから&#x200B;**[!UICONTROL 画像セット]**&#x200B;を選択します。メニューには、**[!UICONTROL 混在メディアセット]**、**[!UICONTROL スピンセット]**、**[!UICONTROL カルーセルセット]**&#x200B;を作成するためのオプションもあります。これらのセットは、画像セットと同じ方法で作成します。

混在メディアセットには、画像、見本セット、スピンセット、ビデオおよびアダプティブビデオセットを含めることができます。[試してみる](https://s7d9.scene7.com/s7viewers/html5/MixedMediaViewer.html?asset=Scene7SharedAssets/Mixed_Media_Set_Sample)。スピンセットは、物体を回転させて調べるという現実世界の操作をシミュレートしたものです。スピンセットを使用すると、主要なビジュアルをあらゆる角度から視覚的に確認できます。[試してみる](https://s7d9.scene7.com/s7viewers/html5/SpinViewer.html?asset=Scene7SharedAssets/SpinSet_Sample&amp;stagesize=500,400){target="_blank"}。

画像セットの作成は簡単です。セットに含める画像アセットを追加するだけです。

![画像セットの作成](/help/assets/dynamic-media/assets/dm-create-image-set-add-assets.png)
_画像セットエディターを使用すると、画像アセットを追加し、セット内の外観を並べ替えることができます。_

セットには名前を付ける必要があります。名前は後で編集できないので、慎重に付けてください。上記の例では、このセットは `Running` という名前です。完了したら、セットを保存します。

そして、これが Experience Manager Assets での `Running` の画像セットです。

![Experience Manager Assets での Running 画像セット、カード表示](/help/assets/dynamic-media/assets/dm-image-set.png)
_Experience Manager Assets での `Running` 画像セット、カード表示。_

画像セット、混在メディアセット、スピンセット、その他のインタラクティブメディアを作成した後は、顧客に対してセットがどのように表示され、動作するのかを確認します。Dynamic Media には数多くの組み込みビューアがあるので、それらを使用します。

最初に、組み込みの画像セットを選択し、次の例に示すように、プレビューで開きます。

![「ビューア」オプションを選択した Running 画像セットのプレビュー](/help/assets/dynamic-media/assets/dm-image-set-viewer.png)
_「ビューア」オプションを選択した `Running` 画像セットのプレビュー。_

プレビューで、ランニングシューズの見本を選択し、シューズをズームインおよびズームアウトできます。ビューアをセットに適用するには、プルダウンメニューから「**[!UICONTROL ビューア]**」を選択します。

![Flyout ビューアを適用した Running 画像セット](/help/assets/dynamic-media/assets/dm-image-set-flyout-viewer.png)
_Flyout ビューアを適用した `Running` 画像セット_

ここでは、`Flyout` ビューアが選択されました。この時点で、ビューアで画像セットをプレビューできます。ただし、顧客が表示するときのように、ブラウザーで表示するのが最適です。左下にある **[!UICONTROL URL]** を選択し、URL をコピーしてブラウザーに貼り付けます。[試してみる](https://s7d1.scene7.com/s7viewers/html5/FlyoutViewer.html?asset=jpearldemo/Running&amp;config=jpearldemo/Flyout){target="_blank"}。

単一の URL で、web サイト上で画像セットとビューアが使用できます。前の例で、「URL」ボタンの右に「**[!UICONTROL 埋め込み]**」ボタンがあることに気づいたでしょうか。「**[!UICONTROL 埋め込み]**」を選択すると、この画像セット／ビューアのコードをコピーして、web ページまたは Experience Manager Sites コンポーネントに追加できます。

Flyout ビューアは、既定の標準提供ビューアで、プロパティを編集できます。または、画像プリセットの作成と同様に、独自のカスタムビューアを作成できます。

ここで、セールスチームおよびマーケティングチームがフライアウトビューアが気に入らないとします。ズーム機能は気に入っているのですが、顧客には直接シューズの上でズーム効果を見てほしいと考えています。その場合は、InlineZoom ビューアを画像セットに適用し、その URL をブラウザーにコピー＆ペーストして、動作を確認します。[試してみる](https://s7d1.scene7.com/s7viewers/html5/FlyoutViewer.html?asset=jpearldemo/Running&amp;config=jpearldemo/InlineZoom){target="_blank"}。

マウスポインターをシューズの上に置くと、画像が拡大表示され、ポインターを動かして詳細を確認できます。これが可能な理由は、Dynamic Media に最初にアップロードされた画像のサイズです。

消費者として、あるいは社会人として暮らしているときに、いろいろな web サイトで、この種のものを目にします。Dynamic Media の力を自分の仕事や会社の web サイトでどのように活用できるか、その仕組みを考えてみてください。

画像セットとビューアについて読みました。他にもいくつかのビューアで、アセットを試してみてください。ビューアをリセットするには、左下隅の「**[!UICONTROL 更新]**」ボタンをクリックします。

<!-- LEAVE THIS HIDDEN PATH IN THE DOCUMENTATION FOR DEMO PURPOSES [Flyout viewer with image set](http://www.partycity.com/girls-little-old-lady-costume-P750948.html) -->

* 画像アセットに適用された `ZoomVertical_dark` ビューア。[試してみる](https://s7d1.scene7.com/s7viewers/html5/ZoomVerticalViewer.html?asset=jpearldemo/AdobeStock_96311480&amp;config=jpearldemo/ZoomVertical_dark){target="_blank"}。
* 画像に適用された `Zoom_light` ビューア[試してみる](https://s7d1.scene7.com/s7viewers/html5/BasicZoomViewer.html?asset=jpearldemo/AdobeStock_38827423&amp;config=jpearldemo/Zoom_light){target="_blank"}。

## オプション - 詳細情報

読んだ内容について詳しくは、以下の資料を使って概念をさらに詳しく調べてください。以上で、Dynamic Media ジャーニーは完了です。

<!--
_Dynamic Media Help topics_

* [How to create image presets](/help/assets/dynamic-media/image-presets.md)
* A list of [image processing parameters](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/http-protocol-reference/command-reference/c-command-reference.html) that you can use in the Image Modifier field when you create an image preset
* [How to preview assets](/help/assets/dynamic-media/previewing-assets.md)
* [How to preview 3D assets](/help/assets/dynamic-media/previewing-3d-assets.md)
* [How to create Image sets](/help/assets/dynamic-media/image-sets.md)
* [How to create Spin sets](/help/assets/dynamic-media/spin-sets.md)
* [How to create Mixed Media sets](/help/assets/dynamic-media/mixed-media-sets.md) -->

_Dynamic Media チュートリアル_

* [Experience Manager Assets での Dynamic Media の使用](https://experienceleague.adobe.com/docs/experience-manager-learn/assets/dynamic-media/dynamic-media-overview-feature-video-use.html?lang=pt-BR)
* [Adobe Experience Manager コンテンツライブラリ](https://experienceleague.adobe.com/?lang=ja#recommended/solutions/experience-manager)（_Dynamic Media_ で検索）

_Dynamic Media ビューア_

* 各ビューアの[ライブデモ](https://landing.adobe.com/en/na/dynamic-media/ctir-2755/live-demos.html)

<!-- Live as of April 28 2022. LEAVE IN HERE https://landing.adobe.com/en/na/dynamic-media/ctir-2755/index.html -->