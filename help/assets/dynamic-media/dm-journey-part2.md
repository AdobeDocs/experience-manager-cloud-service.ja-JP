---
title: Dynamic Mediaジャーニー第 2 部
description: Dynamic Mediaジャーニーでは、Dynamic Mediaの基本、仕組み、ユーザーにとって何ができるか、およびユーザーや顧客にとっての価値について説明します。
contentOwner: Rick Brough
products: Experience Manager as a Cloud Service
topic-tags: introduction,administering
content-type: reference
feature: Image Profiles
role: User, Admin
mini-toc-levels: 4
hide: false
hidefromtoc: false
exl-id: cdca41ad-a2cd-4f68-aaa4-5eec33c30f0b
source-git-commit: 94d77e08e5df82f9bb432bb06c4f05301d119f9e
workflow-type: tm+mt
source-wordcount: '2817'
ht-degree: 0%

---

# Dynamic Mediaジャーニー:基礎知識第 2 部  {#dm-journey-part2}

Dynamic Mediaジャーニーへようこそ：基礎知識第 II 部では、次の情報を学ぶことができます。

* Dynamic Media URL の詳細とDynamic Mediaがコンテンツを配信する方法
* アセットをレンダリングするための画像プリセットの作成の基本
* 画像セット、スピンセットおよび混在メディアセット

関連トピック [Dynamic Mediaジャーニー;基本、第 1 部](/help/assets/dynamic-media/dm-journey-part1.md).

>[!TIP]
>
>最も良い結果を得るには、Adobeは、デスクトップコンピューターでDynamic Mediaジャーニーを読み取り、表示することをお勧めします。

## Dynamic Media URL の詳細とDynamic Mediaがコンテンツを配信する方法 {#dm-journey-d}

Dynamic Mediaアセットをアップロードして公開した後、アセットの生成された URL をコピーし、ブラウザーに貼り付けて、アセットが顧客にどのように表示されるかを確認できます。 次に示す監視画像用の URL のコピーは、読みやすく理解しやすくするために、色分けされています。

![Dynamic Media URL の詳細](/help/assets/dynamic-media/assets/dm-colored-url.png)
_Dynamic Media URL の構造。_

URL の最初の部分（赤）は、サーバードメイン自体を参照しています。 この場合、Dynamic Mediaは汎用サーバードメイン ( `https://s7d1.scene7.com/is/image/`. 一連の画像を見て、サーバードメインを調べるだけで、Dynamic Mediaが提供しているかどうかを簡単に理解できます。 URL の一貫性はかなり高くなります。 ただし、Dynamic Mediaの一部のお客様は、専用のサーバードメインに切り替えて、そのドメインが `name-of-your-company.scene7.com`. スマートイメージングには専用のサーバードメインが必要です。

アカウント名は紫色の部分です。 この場合、アカウントはと呼ばれます。 `jpearldemo`.

アセット ID または名前 `AdobeStock_28563982` は緑色です。 アセットには *いいえ* ファイル拡張子： `.png` または `.jpg`. アセットがDynamic Mediaに取り込まれると、ファイル拡張子が削除され、別の種類のファイルが作成されます。ピラミッドTIFFファイル ピラミッドTIFFを使用すると、Dynamic Mediaは即座にレンディションを作成できます。

最後に、いくつかの画像処理パラメータがあります。 `?wid=1000&fmt=jpeg&qlt=85`（末尾が黄色で表示）

URL パス全体がライブです。 [所要時間](https://s7d1.scene7.com/is/image/jpearldemo/AdobeStock_28563982?wid=1000&amp;fmt=jpeg&amp;qlt=85).

ブラウザーウィンドウが引き続きDynamic Media URL と監視画像が開いた状態で、URL を変更するだけで、画像のレンディションを作成する方法を詳しく見てみましょう。

### URL を使用した監視画像のレンダリング

最初に、URL パス内の画像処理ルールのみを手動で削除します。サーバー名、アカウント名、アセット ID または画像名はそのままにします。 [所要時間](https://s7d1.scene7.com/is/image/jpearldemo/AdobeStock_28563982).

次に、URL の末尾に画像処理パラメーターを追加します。 「URL」フィールドで、画像名の右側に「 」と入力します。 `?wid=500`をクリックし、 **[!UICONTROL 入力]**. [所要時間](https://s7d1.scene7.com/is/image/jpearldemo/AdobeStock%5F28563982?wid=500).

ウォッチの新しいレンディションが生成されます。 画像の幅を変更するこの簡単な演習から理解すべき重要な点は、表示される画像が 100%動的に生成される点です。

次に、の幅の値を変更します。 `500` ピクセルから `1000` ピクセルを指定し、 **[!UICONTROL 入力]**. [所要時間](https://s7d1.scene7.com/is/image/jpearldemo/AdobeStock%5F28563982?wid=1000).
押した瞬間 **[!UICONTROL 入力]**&#x200B;ブラウザーがDynamic Media Image Server に戻ります。 入力した新しい幅の値に基づいて、新しいレンディションのウォッチが生成され、新しい画像がブラウザーに配信されてキャッシュされます。

Dynamic Mediaには、Web ページ上の画像アセットを微調整するために使用できる、多数の画像処理パラメーターがあります。 以下が可能です。 [ここにリストを表示](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/http-protocol-reference/command-reference/c-command-reference.html?lang=en).

次に、ウォッチイメージに回転パラメータを追加してみます。 URL パスの末尾（の直後） `wid=1000`, type `&rotate=90`をクリックし、 **[!UICONTROL 入力]**. [所要時間](https://s7d1.scene7.com/is/image/jpearldemo/AdobeStock%5F28563982?wid=1000&amp;rotate=90).

時計はまだ左に少し歪んでいます。 の回転値を変更する `90` から `92`をクリックし、 **[!UICONTROL 入力]**. [所要時間](https://s7d1.scene7.com/is/image/jpearldemo/AdobeStock%5F28563982?wid=1000&amp;rotate=9)

再び、 **[!UICONTROL 入力]**&#x200B;に設定すると、ほぼ瞬時に新しいレンディションの腕時計が生成されます。 取得したパフォーマンスの種類を確認できるので、Dynamic Mediaが 80 万件を超えるイメージリクエストを配信できる理由がわかります。 *秒*&#x200B;忙しい週末や大きな休日。

画像ごとに URL 内の画像処理パラメータを変更できますが、Web サイトを構成する画像が数万個ある場合などは特に効率的な方法ではありません。 画像プリセットを使用する方法がはるかに優れています。

## アセットをレンダリングするための画像プリセットの作成の基本 {#dm-journey-e}

画像を作成する場所、または画像を使用できる場所は複数あります。 従来、クリエイティブはAdobe Photoshopに移動し、これらの各レンディションを静的画像として保存します。

![静的画像](/help/assets/dynamic-media/assets/dm-static-images.png)
_良い：静的な画像（それぞれ手動で作成）_

クリエイティブ・Directorが画像を見てこう言ったとしましょう

_「私は本当にこの写真を欲しかったので、大きな手が 4 を指し、小さな手が 1 を指して時計のダイヤルを見やすくしました。」_

クリエイティブは、これらの新しい静的画像をすべて再撮影する必要があります。

ただし、Dynamic Mediaでは、異なる画像プリセットがある場合、必要な場所でそれらの画像を使用できます。 画像プリセットには標準が適用されます。

![プライマリファイルのアプローチ](/help/assets/dynamic-media/assets/dm-onefile.png)
_最高：画像プリセットを使用して、複数のレンディションがその場で作成された 1 つのファイル ( `Search_Grid` および `Thumbnail`._

| **画像プリセットを使用する理由** |  |
|---|---|
| 標準規格 | 画像プリセットでは、要求された画像に対して、標準的な画像処理処理が適用されます。 |
| 変更管理 | 画像処理を変更する必要がある場合は、既存の画像プリセットのパラメーターを編集するだけです。 更新された定義は、自動的にすべてのリクエストに反映されます。 |

特定のタイプの画像が必要な場所（例： ）

* 製品の詳細ページ
* 検索グリッド
* thumbnail,
* 買い物かご
* ヒーロー画像

画像を使用する場所に対して、同じパラメーターを使用してその画像を配信する場合。

ここで、Dynamic Mediaでの画像プリセットの作成方法を見てみましょう。

![「基本」タブから始まる画像プリセットの作成](/help/assets/dynamic-media/assets/dm-image-preset-basictab.png)
_「基本」タブから始まる画像プリセットの作成_

上の例では、新しい画像プリセットが _中_. Dynamic Mediaでは、標準搭載の画像（バックパック）の例を使用して、画像プリセットの作成時に特性を確認できます。

この _中_ 画像プリセットの幅は 500 ピクセル、高さは 800 ピクセルです。 このジャーニーの第 1 部では、様々な形式でのアセットの配信について説明します。 次の **[!UICONTROL 形式]** プルダウンメニューから、JPEG、PNG、TIFFまたはその他の複数の形式でアセットを配信するよう選択できます。 ここでは柔軟性を持っています。

の選択 **[!UICONTROL 詳細]** 「 」タブには、アセットのカラースペースに関するオプションが表示されます。 選択した形式に応じて、 **[!UICONTROL 基本]** タブ — 上の例では、「JPEG」が選択されています。アセットは、「RGB」、「グレースケール」または「CMYK」で配信できます。 次の **[!UICONTROL カラープロファイル]** プルダウンメニューから、印刷に使用する CMYK 画像アセットの配信方法を選択できます。 また、画像をシャープにするために適用できる追加のパラメーターもあることに注意してください。 この場合、 **[!UICONTROL アンシャープマスク]** が適用された。

![「詳細設定」タブのオプションを選択して画像プリセットを作成する](/help/assets/dynamic-media/assets/dm-image-preset-advancedtab.png)
_「詳細設定」タブのオプションを選択して、画像プリセットを作成します。_

以下の場所で [Dynamic Media URL の詳細](#dm-journey-d) 以前は、 Dynamic Media URL とその構築方法についてお読みいただきました。 この **[!UICONTROL 画像の修飾子]** テキストボックスに、必要な追加の画像処理パラメータを入力できます。 パラメーターは、画像が配信される際に、プリセットを使用して URL のプリセット名に含まれます。 上のスクリーンショットでは、パラメーターは `bgc=451B15` が追加されました。 つまり、濃い茶色の背景色が追加されました。

画像プリセットは、画像のレシピと考えることができます。 プリセットを使用する画像は、常に、一貫性のある方法で配信されます。同じです パラメーター `&op_brightness=+10` また、明るさを少し増やすためにが追加されました。

完了したら、プリセットを保存すると、既存のすべての画像で使用できるようになります。 この場合、 _中_ 液体チョコレートのボウルの画像にプリセットされる画像。

![画像プリセットの適用 *中* 画像のレンディションを生成するには](/help/assets/dynamic-media/assets/dm-medium-image-preset.png)
_画像プリセット「メディア」を適用して、画像のレンディションを生成します。_

URL をコピーし、それをブラウザーに貼り付けて、画像の外観を確認します。 [所要時間](http://s7d1.scene7.com/is/image/jpearldemo/AdobeStock_74043302?$Medium$). ブラウザーに、画像プリセットの名前が表示されます。 _中_ を設定します。

画像に表示される明確さの種類を確認できます。 その品質は、チョコレートのボウルを撃った方法の一部に起因します。 また、これは部分的に、Dynamic Mediaでは、デジタルチャネルに配信される画像よりも大きな画像を保存できるからです。

チョコレートのボウルに関してすべてが満足のいくものに見える場合は、Web ページで画像を表示する場所に URL を貼り付けます。

下の時計の画像を再度見ると、 `Cart` 画像プリセット `Grid` プリセット、 `Large` プリセット、 `PDP-page` （製品の詳細ページ）プリセットなど。

![静的および動的画像プリセット](/help/assets/dynamic-media/assets/dm-image-presets.png)
_静的および動的画像プリセット。 ウォッチイメージは、 `PDP-page` 画像プリセット。_

しかし、Web サイト上の画像を変更する必要がある場合はどうなりますか？ 例えば、テストを完了し、120 x 120 ( `Cart` 画像プリセット ) が予想どおりに受信されていません。 幅を 175 ピクセルに増やし、高さを 175 ピクセルに増やして、画像を大きくする必要があります。 従来は、Adobe Photoshopを開き、これらの買い物かごの画像をすべて再作成する必要がありました。 ただし、Dynamic Mediaでは、次の例に示すように、「幅」と「高さ」の値を 175 に更新して、プリセットを保存することで、画像プリセットを編集します。

![画像プリセットの編集](/help/assets/dynamic-media/assets/dm-edit-image-preset.png)
_の幅と高さの編集 `Cart` 画像プリセット。_

画像プリセットを変更してキャッシュをフラッシュした後、すべての画像が更新され、そのプリセットで使用されているすべての URL が次の操作を行います。 _not_ どこでも変更できます。 つまり、リンク切れや Web ページのリダイレクトは不要です。

## 画像セット、スピンセットおよび混在メディアセット {#dm-journey-f}

Dynamic Mediaをより一般的に使用しているのは、画像セット、スピンセット、混在メディアセットを作成する機能です。

画像セットは、通常、単一のエンティティとして表示される一連の画像アセットで構成されます。 この種のセットは、統合された表示エクスペリエンスを提供し、ユーザーはサムネール画像をクリックしてアイテムの様々なビューを表示できます。 画像セットを使用すると、代替ビューを表示でき、ビューアは画像を詳細に調べるためのズームツールを提供します。 [フライアウトビューアを使用する「実行中」という画像セットを表示します。](https://s7d1.scene7.com/s7viewers/html5/FlyoutViewer.html?asset=jpearldemo/Running).

Dynamic Mediaの中にはランニングシューズの画像がいくつか見えます。 これは、セールスおよびマーケティング部門が、顧客に単一のプレゼンテーションとして表示してもらいたいと考える製品ラインシリーズです。画像セット。

![画像セットの作成](/help/assets/dynamic-media/assets/dm-create-image-set.png)
_画像セットの作成の開始。_

画像セットを作成するには、次を選択します。 **[!UICONTROL 画像セット]** から **[!UICONTROL 作成]** プルダウンメニューを使用します。 メニューには、 **[!UICONTROL 混在メディアセット]**, a **[!UICONTROL スピンセット]**、および **[!UICONTROL カルーセルセット]**. これらのセットは、画像セットと同じ方法で作成します。

混在メディアセットには、画像、スウォッチセット、スピンセット、ビデオおよびアダプティブビデオセットを含めることができます。 [所要時間](https://s7d9.scene7.com/s7viewers/html5/MixedMediaViewer.html?asset=Scene7SharedAssets/Mixed_Media_Set_Sample). スピンセットは、オブジェクトを回転させて調べる実際の動作をシミュレートします。 スピンセットを使用すると、あらゆる角度から主要な視覚的詳細を表示できます。 [所要時間](https://s7d9.scene7.com/s7viewers/html5/SpinViewer.html?asset=Scene7SharedAssets/SpinSet_Sample&amp;stagesize=500,400).

画像セットの作成は簡単です。 セットに含める画像アセットを追加するだけです。

![画像セットの作成](/help/assets/dynamic-media/assets/dm-create-image-set-add-assets.png)
_画像セットエディターを使用すると、画像アセットを追加し、セット内の外観を並べ替えることができます。_

セットに名前を付ける必要があります。 名前は後で編集できないので、慎重に選択してください。 上記の例では、セットはと呼ばれます。 `Running`. 完了したら、セットを保存します。

そして、これが `Running` Experience Manager Assetsの画像セット。

![Experience Manager Assetsの実行中の画像セット、カード表示](/help/assets/dynamic-media/assets/dm-image-set.png)
_この `Running` Experience Manager Assetsのカード表示で設定された画像。_

画像セット、混在メディアセット、スピンセット、その他のインタラクティブメディアを作成した後は、セットの表示方法や動作方法をユーザーに確認する必要があります。 Dynamic Mediaには、数多くの組み込みビューアがあり、それを実現できます。

最初に、組み込みの画像セットを選択し、次の例に示すように、プレビューで開きます。

![「ビューア」オプションが選択された状態でプレビューで設定された実行中の画像](/help/assets/dynamic-media/assets/dm-image-set-viewer.png)
_この `Running` 「ビューア」オプションが選択された状態でプレビューで設定された画像。_

プレビューで、ランニングシューのスウォッチを選択し、シューズをズームインおよびズームアウトできます。 ビューアをセットに適用するには、「 **[!UICONTROL ビューア]** を選択します。

![フライアウトビューアを適用した実行画像セット](/help/assets/dynamic-media/assets/dm-image-set-flyout-viewer.png)
_この `Running` フライアウトビューアを適用した画像セット_

この場合、 `Flyout` ビューアが選択されました。 この時点で、ビューアで画像セットをプレビューできます。 ただし、ブラウザーで表示するのが最適で、顧客がどのように表示するかが最適です。 次を選択します。 **[!UICONTROL URL]** 左下にある URL をコピーし、ブラウザーに貼り付けます。 [所要時間](https://s7d1.scene7.com/s7viewers/html5/FlyoutViewer.html?asset=jpearldemo/Running&amp;config=jpearldemo/Flyout).

単一の URL では、Web サイト上で画像セットとビューアを使用できます。 前の例では **[!UICONTROL 埋め込み]** が「URL」ボタンの右にあることを確認します。 選択 **[!UICONTROL 埋め込み]**&#x200B;を使用すると、この画像セット/ビューアのコードをコピーして、Web ページまたはExperience Manager Sitesコンポーネントに追加できます。

フライアウトビューアは、既定の標準提供ビューアで、プロパティを編集できます。 または、画像プリセットの作成と同様に、独自のカスタムビューアを作成できます。

これで、セールスチームとマーケティングチームがフライアウトビューアを好まないと考えました。 ズーム機能が好きですが、靴の上でズーム効果を直接見てほしいと考えています。 その場合は、InlineZoom ビューアを画像セットに適用し、その URL をブラウザーにコピー&amp;ペーストして、動作を確認します。 [所要時間](https://s7d1.scene7.com/s7viewers/html5/FlyoutViewer.html?asset=jpearldemo/Running&amp;config=jpearldemo/InlineZoom).

マウスポインタを靴の上に移動すると、その画像を拡大表示し、ポインタを動かすと詳細が表示されます。 その理由は、Dynamic Mediaに最初にアップロードされた画像のサイズにすぎません。

消費者として生きているとか日常的な役割を果たしているとか別のウェブサイトに行くとこんな感じがします その仕組みを考えてみてくださいDynamic Mediaの力を自分の仕事や会社の Web サイトでどのように使えるか考えてみてください

画像セットとビューアについて少しお読みください。 他のいくつかのビューアを見て、単一のアセットを試してみましょう。 ビューアをリセットするには、 **[!UICONTROL 更新]** 」ボタンをクリックします。

<!-- LEAVE THIS HIDDEN PATH IN THE DOCUMENTATION FOR DEMO PURPOSES [Flyout viewer with image set](http://www.partycity.com/girls-little-old-lady-costume-P750948.html) -->

* `ZoomVertical_dark` 画像アセットに適用されたビューア [所要時間](https://s7d1.scene7.com/s7viewers/html5/ZoomVerticalViewer.html?asset=jpearldemo/AdobeStock_96311480&amp;config=jpearldemo/ZoomVertical_dark).
* `Zoom_light` 画像に適用されたビューア [所要時間](https://s7d1.scene7.com/s7viewers/html5/BasicZoomViewer.html?asset=jpearldemo/AdobeStock_38827423&amp;config=jpearldemo/Zoom_light).

## 詳細情報

_Dynamic Media_

* [画像プリセットの作成](/help/assets/dynamic-media/image-presets.md)
* リスト [画像処理パラメータ](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/http-protocol-reference/command-reference/c-command-reference.html?lang=ja) 画像プリセットを作成する際に「画像の修飾子」フィールドで使用できる
* [アセットのプレビュー](/help/assets/dynamic-media/previewing-assets.md)
* [3D アセットのプレビュー](/help/assets/dynamic-media/previewing-3d-assets.md)
* [画像セット](/help/assets/dynamic-media/image-sets.md)
* [スピンセット](/help/assets/dynamic-media/spin-sets.md)
* [混在メディアセット](/help/assets/dynamic-media/mixed-media-sets.md)

_Dynamic Mediaチュートリアル_

* [Experience Manager AssetsでのDynamic Mediaの使用](https://experienceleague.adobe.com/docs/experience-manager-learn/assets/dynamic-media/dynamic-media-overview-feature-video-use.html)
* [Adobe Experience Manager Content Library](https://experienceleague.adobe.com/?lang=en#recommended/solutions/experience-manager) ( 検索 _Dynamic Media_)