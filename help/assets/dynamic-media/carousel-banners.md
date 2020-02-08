---
title: カルーセルバナー
description: ダイナミックメディアでカルーセルバナーを使用する方法について説明します。
translation-type: tm+mt
source-git-commit: 82dd9bd69fe994f74c7be8a571e386f0e902f6a1

---


# カルーセルバナー{#carousel-banners}

カルーセルバナーを使用すると、回転するインタラクティブなプロモーションコンテンツをマーケティング担当者が簡単に作成して、任意の画面に配信できるようになり、コンバージョンを推進できます。

プロモーションバナーに表示するコンテンツの作成や変更には時間がかかるので、新しいコンテンツをすぐに公開したり、ターゲットを絞り込んだりする際に制約が生じます。カルーセルバナーを使用すると、回転するバナーをすばやく作成または変更したり、製品の詳細や関連リソースにリンクするホットスポットなどのインタラクティブ機能を追加したり、任意の画面に新しいプロモーションコンテンツを迅速に提供できます。

カルーセルバナーには「**[!UICONTROL CAROUSELSET]**」と表示されます。

![chlimage_1-438](assets/chlimage_1-438.png)

Web サイトではカルーセルバナーは次のように表示されます。

![chlimage_1-439](assets/chlimage_1-439.png)

ここで、ユーザーが番号をクリックして画像を切り替えることができます。また、カスタマイズできる間隔に基づいて自動的にスライドを切り替えることもできます。カルーセルバナーに追加する画像は、ホットスポットと画像マップの両方に対応しており、タップするか、ハイパーリンクに移動するか、クイックビューウィンドウにアクセスできます。

この例では、ユーザーは画像マップをタップまたはクリップして、手袋のクイックビューウィンドウにアクセスしました。

![chlimage_1-440](assets/chlimage_1-440.png)

## カルーセルバナーの作成方法の視聴 {#watch-how-carousel-banners-are-created}

10 分 33 秒の[カルーセルバナーの作成方法](https://s7d5.scene7.com/s7viewers/html5/VideoViewer.html?videoserverurl=https://s7d5.scene7.com/is/content/&emailurl=https://s7d5.scene7.com/s7/emailFriend&serverUrl=https://s7d5.scene7.com/is/image/&config=Scene7SharedAssets/Universal_HTML5_Video_social&contenturl=https://s7d5.scene7.com/skins/&asset=S7tutorials/InteractiveCarouselBanner)に関する説明を視聴してください。カルーセルバナーのプレビュー、編集および配信方法についても説明します。

>[!NOTE]
>
>管理者以外のユーザーは、カルーセルバナーを作成または編集できるように、**[!UICONTROL dam-users]** グループに追加される必要があります。If you are having trouble creating or editing, please see your system administrator who can add you to the **d[!UICONTROL am-users ]**group.

## クイックスタート：カルーセルバナー {#quick-start-carousel-banners}

すぐに使い始めるには：

1. [ホットスポット変数と画像マップ変数の特定](#identifying-hotspot-and-image-map-variables) （AEM Assets +ダイナミックメディアを使用するお客様のみ）

   まず、既存のクイックビュー実装で使用されている動的変数を識別します。こうすることで、AEM Assets でのカルーセルバナー作成プロセスでホットスポットと画像マップのデータを適切に入力できます。

<!-- LEAVE; COMMERCE BEING ADDED AGAIN IN THE FUTURE

   >[!NOTE]
   >
   >If you are an AEM Sites or Ecommerce customer, you can use the built-in feature to navigate to product pages and lookup the existing skus in the product catalog. You do not need to manually enter hotspot or image map variables.
   >
   >
   >If you are an AEM Assets and Dynamic Media customer, you will manually enter data for hotspots and image maps, and then integrate the published URL or Embed code with your third-party content management system.

-->

1. Optional: [Create a Carousel Set viewer preset](/help/assets/dynamic-media/managing-viewer-presets.md), as needed.

   管理者は、独自のカルーセルビューアプリセットを作成して、カルーセルの動作と外観をカスタマイズできます。主な利点は、このカスタムビューアプリセットを複数のカルーセルに再利用できることです。 ただし、ユーザーがカルーセルを作成するときに、カルーセルの動作や外観を直接カスタマイズすることもできます。特定のカルーセルに対して非常に具体的なデザインが必要な場合は、この方法をお勧めします。

1. [画像バナーをアップロードします](#uploading-image-banners)。

   インタラクティブにする画像バナーをアップロードします。

1. [カルーセルセットを作成します](#creating-carousel-sets)。

   カルーセルセットでは、ユーザーはバナー画像を切り替え、ホットスポットまたは画像マップをタップして関連するコンテンツにアクセスします。

   To create a Carousel Set in Assets, tap **[!UICONTROL Create]**, then select **[!UICONTROL Carousel Sets]**. Add assets to slides and tap **[!UICONTROL Save]**. エディター内で、カルーセルの外観と動作を直接編集することもできます。

1. [画像バナーにホットスポットまたは画像マップを追加します。](#adding-hotspots-or-image-maps-to-an-image-banner)

   1つ以上のホットスポットまたは画像マップを画像バナーに追加し、各ホットスポットまたは画像マップをリンク、クイックビュー、エクスペリエンスフラグメントなどのアクションに関連付けます。 ホットスポットまたは画像マップを追加した後は、カルーセルセットを公開してタスクを終了します。公開によって埋め込みコードが生成されます。これは、コピーして eb サイトのランディングページに適用するために使用できます。

   [ 詳しくは、カ ](#optional-previewing-carousel-banners)ルーセルバナーのプレビューを参照してください。 — オプション。 必要に応じて、カルーセルセットの表示を確認して、インタラクティビティをテストすることができます。

1. [カルーセルバナーを公開します](#publishing-carousel-banners)。

   他のアセットと同じようにカルーセルセットを公開します。In Assets, navigate to the Carousel Set and select it and tap **[!UICONTROL Publish]**. カルーセルセットを公開すると、URL と埋め込み文字列がアクティベートされます。

1. 次のいずれかの操作をおこないます。

   * [Webサイトページへのカルーセルバナーの追加
      ](#adding-a-carousel-banner-to-your-website-page)Webサイトページには、カルーセルバナーのURLまたはコピーした埋め込みコードを追加できます。

      * [カルーセルバナーを既存のクイックビューに統合します](#integrating-the-carousel-banner-with-an-existing-quickview)。サードパーティの Web コンテンツ管理システムを使用している場合は、新しいカルーセルバナーを、Web サイト上の既存のクイックビュー実装に統合する必要があります。
   * [AEMでWebサイトにカルーセルバナーを追加する
      ](/help/assets/dynamic-media/adding-dynamic-media-assets-to-pages.md)AEMサイトのお客様は、Interactive mediaコンポーネントを使用して、カルーセルセットをAEM内のページに直接追加できます。


If you need to edit Carousel Sets, see [editing Carousel Sets.](#editing-carousel-sets) また、カルーセルセットのプロパティを表示し [たり編集したりできます](/help/assets/manage-digital-assets.md#editing-properties)。

## ホットスポットと画像マップの変数の識別 {#identifying-hotspot-and-image-map-variables}

まず、既存のクイックビュー実装で使用されている動的変数を識別します。こうすることで、AEM Assets でのカルーセルセット作成プロセスでホットスポットまたは画像マップのデータを適切に入力できます。

AEM Assets 内のバナー画像にホットスポットまたは画像マップを追加する際に、各ホットスポットまたは画像マップに SKU とオプションの追加変数を割り当てる必要があります。これらの変数は、後でホットスポットまたは画像マップとクイックビューコンテンツを対応付けるために使用されます。

<!-- LEAVE; COMMERCE BEING ADDED LATER

>[!NOTE]
>
>If you are an AEM Sites and/or AEM Ecommerce customer, skip this step. You do not need to manually identify hotspot or image map variables; you can use the integration with Ecommerce for product integration. See information on [setting up eCommerce](/help/sites-cloud/administering/generic.md). In addition, you can use the Interactive component and add it to your web page.
>
>If you are an AEM Assets or Media customer, you publish the URL or Embed code and then integrate with your third-party content management system and identify hotspots and image maps manually.

-->

重要なのは、ホットスポットまたは画像マップのデータに関連付けられる変数の数とタイプを正しく識別することです。バナー画像に追加するそれぞれのホットスポットまたは画像マップは、既存のバックエンドシステム内で製品を一意に識別するための十分な情報を保持する必要があります。同時に、各ホットスポットまたは画像マップに、必要以上のデータを含めないようにしてください。必要以上のデータを含めると、データ入力プロセスが複雑になり、進行中のホットスポットまたは画像マップの管理でエラーが発生しやすくなるからです。

ホットスポットまたは画像マップのデータに使用する一連の変数を識別するには、様々な方法があります。

既存のクイックビュー実装を担当する IT スペシャリストに相談するだけで十分な場合もあります（通常、そのような IT スペシャリストは、システム内のクイックビューを識別するために必要な最小データセットを理解しています）。ただし、ほとんどの場合は、フロントエンドコードの既存の動作を分析するだけでもかまいません。

クイックビュー実装の大部分では、次の枠組みが使用されています。

* ユーザーは Web サイト上の特定のユーザーインターフェイス要素をアクティベートします。For example, tapping a **[!UICONTROL Quick View]** button.
* Web サイトでは、必要に応じて、クイックビューのデータまたはコンテンツを読み込むための Ajax リクエストをバックエンドに送信します。
* クイックビューのデータは、Web ページでのレンダリングに備えて、コンテンツに変換されます。
* 最後に、フロントエンドコードによってそのコンテンツが画面上に視覚的にレンダリングされます。

次に、クイックビュー機能が実装されている既存の Web サイトの各領域にアクセスしてクイックビューを起動し、そのクイックビューのデータまたはコンテンツを読み込むために Web ページから送信される Ajax URL をキャプチャします。

通常、専門のデバッグツールを使用する必要はありません。最新の Web ブラウザーには、十分なタスクを実行できる Web インスペクターが備わっています。Web インスペクターが搭載されている Web ブラウザーの例を次に示します。

* Google Chromeで送信されるHTTP要求をすべて表示するには、F12キー(Windows)またはCommand-Option-Iキー(Mac)を押してDeveloper toolsパネルを開き、「ネットワーク」タブをタップします。
* Firefox では、F12 キー（Windows）または Command + Option + I キー（Mac）を押して Firebug プラグインを有効にして「Net」タブを使用するか、組み込みの Inspector ツールとその「Network」タブを使用します。

ブラウザーでネットワーク監視をオンにして、ページ上でクイックビューを起動します。

次に、ネットワークログでクイックビューのAjax URLを探し、記録したURLをコピーして、将来の分析に使用します。クイックビューをトリガーする場合、ほとんどの場合、サーバーに送信される要求が多数あります。通常、クイックビューのAjax URLはリストの最初のURLの1つです。 It has either a complex query string portion or path, and its response MIME type is either `text/html`, `text/xml`, or `text/javascript`.

このプロセスの実行中は、Web サイトの異なる領域（異なる製品カテゴリーおよび製品タイプが含まれる領域）にアクセスすることが重要です。なぜなら、クイックビュー URL には、ある特定の Web サイトカテゴリーに共通するが、Web サイトの異なる領域にアクセスした場合にのみ変化する部分が存在することがあるからです。

単純なケースでは、クイックビュー URL 内で変化する唯一の部分が製品 SKU となります。その場合、SKU の値が、ホットスポットまたは画像マップをバナー画像に追加するために必要になる唯一のデータです。

一方、複雑なケースでは、クイックビュー URL に SKU 以外の様々な要素が含まれます（カテゴリー ID、カラーコード、サイズコードなど）。その場合、各要素は、カルーセルバナー機能のホットスポットまたは画像マップのデータ定義内の個別の変数になります。

次のクイックビュー URL の例と、その結果となるホットスポットまたは画像マップの変数について見てみましょう。

<table>
 <tbody>
  <tr>
   <td>単一の SKU（クエリー文字列内）</td>
   <td><p>記録されたクイックビューの URL：</p>
    <ul>
     <li><p><code>https://server/json?productId=866558&amp;source=100</code></p> </li>
     <li><p><code>https://server/json?productId=1196184&amp;source=100</code></p> </li>
     <li><p><code>https://server/json?productId=1081492&amp;source=100</code></p> </li>
     <li><p><code>https://server/json?productId=1898294&amp;source=100</code></p> </li>
    </ul> <p>The only variable part in the URL is the value of the <code>productId=</code> query string parameter, and it is clearly a SKU value. したがって、ホットスポットや画像マップに必要なのは、 <code>866558,</code> <code>1196184,</code> <code>1081492,</code> <code>1898294.</code></p> </td>
  </tr>
  <tr>
   <td>単一の SKU（URL パス内）</td>
   <td><p>記録されたクイックビューの URL：</p>
    <ul>
     <li><p><code>https://server/product/6422350843</code></p> </li>
     <li><p><code>https://server/product/1607745002</code></p> </li>
     <li><p><code>https://server/product/0086724882</code></p> </li>
    </ul> <p>The variable part is in the last portion of the path, and it becomes the SKU value of the hotspots/image maps:<strong><code>6422350843</code>, <code>1607745002,</code> </strong><code>0086724882.</code></p> </td>
  </tr>
  <tr>
   <td>SKU とカテゴリ ID（クエリー文字列内）</td>
   <td><p>記録されたクイックビューの URL：</p>
    <ul>
     <li><p><code>https://server/quickView/product/?category=1100004&amp;prodId=305466</code></p> </li>
     <li><p><code>https://server/quickView/product/?category=1100004&amp;prodId=310181</code></p> </li>
     <li><p><code>https://server/quickView/product/?category=1740148&amp;prodId=308706</code></p> </li>
    </ul> <p>この場合、URLには2つの異なる部分があります。 The SKU is stored in the <code>prodId</code> parameter and the category ID is stored in the <code>category=</code>parameter.</p> <p>そのため、ホットスポット／画像マップ定義はペアになります。つまり、SKU 値と、<code>categoryId</code> という追加の変数です。結果のペアは次のようになります。</p>
    <ul>
     <li><p>SKU is <strong><code>305466</code></strong> and <code>categoryId</code> is <code>1100004</code>.</p> </li>
     <li><p>SKU is <strong><code>310181</code></strong> and <code>categoryId</code> is <strong><code>1100004</code></strong>.</p> </li>
     <li><p>SKU is <strong><code>308706</code></strong> and <code>categoryId</code> is <strong><code>1740148</code></strong>.</p> </li>
    </ul> </td>
  </tr>
 </tbody>
</table>

## 画像バナーのアップロード {#uploading-image-banners}

If you have already uploaded the images that you want to use, advance to the next step, [Creating Carousel Sets](#creating-carousel-sets). カルーセルで使用する画像は、ダイナミックメディアを有効にした後にアップロードする必要があります。

画像バナーをアップロードするには、[アセットのアップロード](/help/assets/manage-digital-assets.md)を参照してください。

## カルーセルセットの作成 {#creating-carousel-sets}

>[!NOTE]
>
>管理者以外のユーザーは、カルーセルバナーを作成または編集できるように、**[!UICONTROL dam-users]** グループに追加される必要があります。作成や編集で問題が発生した場合、**[!UICONTROL dam-users]** グループにユーザーを追加できるシステム管理者に確認してください。

**カルーセルセットを作成するには**

1. In Assets, navigate to the folder where you want to create the Carousel Set and tap **[!UICONTROL Create > Carousel Set]**.
1. カルーセルバナーエディターページで「**[!UICONTROL タップしてアセットセレクターを開く]**」をタップし、最初のスライドの画像を選択します。

   カルーセルバナーエディターページで次のいずれかをおこないます。

   * ページの左上隅付近にある「**[!UICONTROL スライドを追加]**」をタップします。

   * ページの中央付近にある「**[!UICONTROL タップしてアセットセレクターを開く]**」をタップします。
   カルーセルセットに含めるアセットをタップして選択します。選択済みのアセットにはチェックマークアイコンが付いています。When you are finished, near the upper-right corner of the page, tap **[!UICONTROL Select**.

   アセットセレクターでは、キーワードを入力して **[!UICONTROL Enter]** キーをタップまたはクリックすることで、アセットを検索することができます。フィルターを適用して、検索結果を絞り込むこともできます。パス、コレクション、ファイルタイプおよびタグでフィルタリングできます。Select the filter and then tap the **[!UICONTROL Filter]** icon on the toolbar. 表示アイコンをタップし、**[!UICONTROL 列表示]**、**[!UICONTROL カード表示]**、**[!UICONTROL リスト表示]**&#x200B;のいずれかを選択してビューを変更します。

   詳しくは、[セレクターの操作](/help/assets/dynamic-media/working-with-selectors.md)を参照してください。

1. カルーセルセット内で回転させたい画像をすべて追加してしまうまで、スライドを追加し続けます。
1. （オプション）次のいずれかの操作をおこないます。

   * 必要に応じて、スライドをドラッグして、画像をリスト内で並べ替えます。
   * 画像を削除するには、画像を選択し、「**[!UICONTROL スライドを削除]**」をタップします。

   * プリセットを適用するには、ページの右上隅付近にあるプリセットドロップダウンリストをタップし、セットに一度に適用するプリセットを選択します。
   スライドを削除するには、スライドをタップまたはクリックし、ツールバーの「**[!UICONTROL スライドを削除]**」をクリックします。スライドを移動するには、並べ替えアイコンをタップして、希望の場所まで移動します。

1. スライドに画像を追加した後で、ホットスポットまたは画像マップ（または両方）を画像に追加できます。See [adding hotspots or image maps](#adding-hotspots-or-image-maps-to-an-image-banner).
1. カルーセルセットの視覚的デザインと動作を変更するには、「動作」タブと「外観」タブをタップまたはクリックし、カルーセルバナーの外観や特定のコンポーネントの動作を調整します。ビューアエディターの使用方法について詳しくは、[ビューアプリセットの管理](/help/assets/dynamic-media/viewer-presets.md)を参照してください。

   >[!NOTE]
   >
   >カルーセルバナーについて調整できるのは次のような項目です。
   >    * 1 つの画像が表示される時間。デフォルトでは、各画像は 9 秒間表示されます。
   >    * アニメーション.デフォルトでは、各スライドのトランジションはフェードです。これをスライドのトランジションに変更できます。
   >    * ボタンのスタイル。ユーザーは点または番号をタップしてバナーの画像を切り替えることができます。セットインジケーターボタンの表示位置（とスタイルが番号か点か）と大きさを変更できます。
   >    * 画像マップまたはホットスポットに使用されるアイコンのハイライトスタイルを変更します。。
   >    * ビューアプリセットを編集する前に、そのプリセットのベースとして使用するスタイルを選択してください。そうしないと、ビューアプリセットの編集を開始した後、別のプリセットに切り替えることにした場合に、変更内容をすべて失うことになります。


   カルーセルバナーがどのように表示されるかをプレビューすることもできます。[（オプション）カルーセルバナーのプレビュー](#optional-previewing-carousel-banners)を参照してください。

1. Tap **[!UICONTROL Save]** when finished.

## 画像バナーへのホットスポットまたは画像マップの追加 {#adding-hotspots-or-image-maps-to-an-image-banner}

カルーセルセットエディターを使用して、ホットスポットまたは画像マップをバナーに追加できます。

ホットスポットまたは画像マップを追加する際に、クイックビューポップアップ表示、ハイパーリンクまたはエクスペリエンスフラグメントとして定義することができます。

[エクスペリエンスフラグメント](/help/sites-cloud/authoring/fundamentals/experience-fragments.md)を参照してください。

>[!NOTE]
>
>カルーセルバナーのソーシャルメディア共有ツールは、ビューアをエクスペリエンスフラグメントに埋め込む場合はサポートされないことに注意してください。
この問題を回避するには、ソーシャルメディア共有ツールを備えていないビューアプリセットを使用または作成します。 このようなビューアプリセットを使用すると、エクスペリエンスフラグメントに正常に埋め込むことができます。

画像にホットスポットまたは画像マップを追加したら、忘れずに作業内容を保存してください。現在の作成/編集セッションでは、ページの右上隅近くにある「取り消し」と「やり直し」のオプションがサポートされます。

カルーセルバナーの作成が完了したら、オプションで「プレビュー」を使用して、カルーセルバナーが顧客にどのように表示されるかを確認できます。

[（オプション）カルーセルバナーのプレビュー](#optional-previewing-carousel-banners)を参照してください。

>[!NOTE]
>
>When you add hotspots to an image in an [Interactive Image](/help/assets/dynamic-media/interactive-images.md) or a Carousel Banner, the hotspot information is stored in the same metadata location—relative to the image&#39;s location&amp;mdashregardless of whether it is an Interactive Image or a Carousel Banner. この機能により、どちらのビューアでも、同じ画像を定義済みのホットスポットデータと共に簡単に再利用できます。

>  ただし、カルーセルバナーでは、画像上の画像マップ（ホットスポットを含むことができる）がサポートされることに注意してください。インタラクティブ画像ではサポートされません。同じ画像を使用するインタラクティブ画像またはカルーセルバナーを作成する場合には、このことに注意してください。同じ画像の別のコピーを使用してインタラクティブ画像とカルーセルバナーを作成することをお勧めします。

>[!NOTE]
ホットスポットを含むインタラクティブ画像を編集しているときに、画像を切り取ると、ホットスポットは削除されます。

<!-- See also [Adding Image Maps](/help/assets/image-maps.md). -->

**ホットスポットまたは画像マップを画像バナーに追加するには**

1. Assets ビューで、インタラクティブにするカルーセルセットに移動します。
1. Select the carousel set and tap **[!UICONTROL Edit]**. カルーセルビューアエディターが開きます。
1. インタラクティブにするスライドを選択します。
1. Near the upper-left corner of the page, tap **[!UICONTROL Hotspot]** or **[!UICONTROL Image Map]**.
1. 次のいずれかの操作をおこないます。

   * ホットスポットの場合：画像の上で、ホットスポットを表示する場所をタップします。
   * 画像マップの場合：画像上でクリックし、左上から右下にドラッグして画像マップ領域を作成します。画像マップのサイズを調整するには、隅をドラッグします。
   必要に応じて、ホットスポットまたは画像マップを別の場所にドラッグします。必要に応じて、他のホットスポットまたは画像マップを追加します。

   ホットスポットまたは画像マップを削除するには、「**[!UICONTROL アクション]**」タブをタップします。「**[!UICONTROL マップとホットスポット]**」見出しの下にある「**[!UICONTROL 選択したタイプ]**」ドロップダウンメニューから、削除するホットスポットまたは画像マップの名前を選択します。メニューの横にある&#x200B;**[!UICONTROL ごみ箱]**&#x200B;アイコンをタップし、「**[!UICONTROL 削除]**」をタップします。

1. 「名前」テキストフィールドにホットスポットまたは画像マップの名前を入力します。この名前は&#x200B;**[!UICONTROL マップとホットスポット]**&#x200B;ドロップダウンリストにも表示されます。名前を指定すると、将来ホットスポットや画像マップに変更を加える場合に、そのホットスポットや画像マップを簡単に識別できます。
1. 「**[!UICONTROL アクション]**」タブで次のいずれかの操作をおこないます。

   * 「**[!UICONTROL クイックビュー]**」をタップします。

      * If you are an AEM Sites <!-- and Ecommerce customer-->, tap the Product Picker icon (magnifying glass) to open the Select Product page. 使用する製品をタップし、ページの右上隅にあるチェックマークをタップして、カルーセルバナーエディターに戻ります。
      * AEMサイト以外の場合 <!-- or Ecommerce customer -->

         * See [Identifying hotspot variables](#identifying-hotspot-and-image-map-variables) as you may want to define these variables.
         * 次に、SKU値を手動で入力します。 「SKU値」テキストフィールドに、製品のSKU（在庫保管単位）を入力します。これは、提供する個々の製品またはサービスの一意の識別子です。 入力したSKU値によって、クイックビューテンプレートの可変部分が自動的に設定され、タップされたホットスポットを特定のSKUのクイックビューに関連付けることができます。
         * (Optional) If there are other variables within the quick view that you need to use to further identify a product, tap **[!UICONTROL Add Generic Variable]**. In the text field, specify an additional variable. 例えば、追加の変数として category=Mens などと指定します。

         * 詳しくは、[セレクターの操作](/help/assets/dynamic-media/working-with-selectors.md)を参照してください。
   * 「**[!UICONTROL ハイパーリンク]**」をタップします。

      * AEMサイトのお客様の場合は、サイトの選択アイコン（フォルダー）をタップしてURLに移動します。
         >[!NOTE]
         インタラクティブコンテンツに相対 URL のリンク（特に AEM Sites ページへのリンク）がある場合、URL ベースのリンク方法は使用できません。

      * スタンドアロンユーザーである場合は、「HREF」テキストフィールドに、リンクされる Web ページへの完全な URL パスを指定します。
   このリンクを新しいブラウザータブで開く（推奨のデフォルト）か同じタブで開くかを指定してください。

   詳しくは、[セレクターの操作](/help/assets/dynamic-media/working-with-selectors.md)を参照してください。

   * 「**[!UICONTROL エクスペリエンスフラグメント]**」をタップします。

      * AEM Sitesのお客様の場合は、検索アイコン（虫眼鏡）をタップして、エクスペリエンスフラグメントページを開きます。 使用するエクスペリエンスフラグメントをタップまたはクリックし、ページの右上隅にある「選択」をタップして、ホットスポット管理ページに戻ります。[エクスペリエンスフラグメント](/help/sites-cloud/authoring/fundamentals/experience-fragments.md)を参照してください。

      * エクスペリエンスフラグメントがバナーに表示されるときの幅と高さを指定します。

         >[!NOTE]
         カルーセルバナーのソーシャルメディア共有ツールは、ビューアをエクスペリエンスフラグメントに埋め込む場合はサポートされないことに注意してください。
この問題を回避するには、ソーシャルメディア共有ツールを備えていないビューアプリセットを使用または作成します。 このようなビューアプリセットを使用すると、エクスペリエンスフラグメントに正常に埋め込むことができます。
   ![experience_fragment-carouselbanner](assets/experience_fragment-carouselbanner.png)

   カルーセルバナーがどのように表示されるかをプレビューすることもできます。[（オプション）カルーセルバナーのプレビュー](#optional-previewing-carousel-banners)を参照してください。

1. 「**[!UICONTROL 保存]**」をタップします。
1. カルーセルセットを公開します。公開によって、Web サイトのページで使用できる、埋め込みコードまたは URL が生成されます。AEM Sites のユーザーである場合は、カルーセルセットを Web ページに直接追加できます。

   [アセットの公開](/help/assets/dynamic-media/publishing-dynamicmedia-assets.md)を参照してください。

   [Web サイトランディングページへのカルーセルセットの追加](#adding-a-carousel-banner-to-your-website-page)を参照してください。

## カルーセルセットの編集 {#editing-carousel-sets}

>[!NOTE]
管理者以外のユーザーは、カルーセルバナーを作成または編集できるように、**[!UICONTROL dam-users]** グループに追加される必要があります。作成や編集で問題が発生した場合、**[!UICONTROL dam-users]** グループにユーザーを追加できるシステム管理者に確認してください。

カルーセルセットでは、次のような様々な編集タスクを実行できます。

* カルーセルセットにスライドを追加します。See also [Working with Selectors](/help/assets/dynamic-media/working-with-selectors.md).
* カルーセルセット内のスライドを並べ替えます。
* カルーセルセットのアセットを削除します。
* ビューアプリセットを適用します。
* カルーセルセットを削除します。
* ホットスポットや画像マップを追加または編集します。See also [Working with Selectors](/help/assets/dynamic-media/working-with-selectors.md).

**カルーセルセットを編集するには**

1. 次のいずれかの操作をおこないます。

   * カルーセルセットアセットの上にマウスポインターを置き、**[!UICONTROL 編集]**（鉛筆アイコン）をタップします。
   * カルーセルセットアセットの上にマウスポインターを置き、**[!UICONTROL 選択]**（チェックマークアイコン）をタップしてからツールバーの「**[!UICONTROL 編集]**」をタップします。

   * カルーセルセットアセットをタップし、ページの左上隅にある「**[!UICONTROL 編集]**」（鉛筆アイコン）をタップします。

1. カルーセルセットを編集するには、次のいずれかの操作をおこないます。

   * To add a slide, tap the **[!UICONTROL Add Slide]** icon then navigate to the asset you want to add to that slide and tap or click the checkmark.
   * スライドを並べ替えるには、スライドを新しい位置までドラッグします（並べ替えアイコンを選択して項目を移動します）。
   * ホットスポットまたは画像マップを追加するには、ホットスポットまたは画像マップのアイコンをクリックし、[ホットスポットおよび画像マップの追加](#adding-hotspots-or-image-maps-to-an-image-banner)を参照してください。
   * カルーセルセットの外観や動作を編集するには、「**[!UICONTROL 外観]**」タブまたは「**[!UICONTROL 動作]**」タブをタップし、必要なオプションを設定します。
   * ホットスポットまたは画像マップを編集するには、対応するスライドの「**[!UICONTROL アクション]**」タブの下で、ホットスポットまたは画像マップを選択し、必要に応じて変更を加えます。
   * スライドを削除するには、スライドを選択し、ツールバーの「**[!UICONTROL スライドを削除]**」をタップします。
   * To apply a preset, near the upper-right corner of the page, tap the **[!UICONTROL Preset]** drop-down list, then select a viewer preset.
   * カルーセルセット全体を削除するには、カルーセルセットの場所に移動して選択し、「**[!UICONTROL 削除]**」をタップします。
   >[!NOTE]
   ホットスポットを含むインタラクティブ画像を編集しているときに、画像を切り取ると、ホットスポットは削除されます。

## （オプション）カルーセルバナーのプレビュー{#optional-previewing-carousel-banners}

プレビューを使用して、カルーセルバナーが顧客に対してどのように表示されるかを確認し、カルーセルバナーのホットスポットと画像マップをテストして、期待どおりに動作することを確認できます。

カルーセルバナーの設定が完了したら、このカルーセルバナーを公開できます。[Web ページへのビデオビューアまたは画像ビューアの埋め込み](/help/assets/dynamic-media/embed-code.md)を参照してください。[Web アプリケーションへの URL のリンク](/help/assets/dynamic-media/linking-urls-to-yourwebapplication.md)を参照してください。インタラクティブコンテンツに相対 URL のリンク（特に AEM Sites ページへのリンク）がある場合、URL ベースのリンク方法は使用できません。 [ページへの Dynamic Media アセットの追加](/help/assets/dynamic-media/adding-dynamic-media-assets-to-pages.md)を参照してください。

カルーセルバナーは、カルーセルエディター（推奨）または&#x200B;**[!UICONTROL ビューア]**&#x200B;リストでプレビューできます。

**カルーセルバナーをプレビューするには**

1. **[!UICONTROL Assets]** で、作成したカルーセルバナーの場所に移動し、タップして開きます。
1. 「**[!UICONTROL 編集]**」をタップします。
1. ツールバーの右端にあるビューアプリセットリストで、カルーセルバナーをプレビューするビューアを選択します。

   ![experience-fragment-carouselbanner-viewerdropdown](assets/experience_fragment-carouselbanner-viewerdropdown.png)

1. Tap **Preview]**.
1. 画像上のホットスポットまたは画像マップをタップして、関連するアクションをテストします。

**ビューアリストからカルーセルバナーをプレビューするには**

1. **[!UICONTROL Assets]** で、作成したカルーセルバナーの場所に移動し、タップして開きます。
1. プレビューページの左上隅付近にある「コンテンツ」アイコンをクリックします。
1. In the **[!UICONTROL Viewers]** list in the panel on the left side of the page, tap the name of the carousel banner viewer preset you want to use.
1. 画像上のホットスポットまたは画像マップをタップして、関連するアクションをテストします。

## カルーセルバナーの公開 {#publishing-carousel-banners}

カルーセルを使用するには、公開する必要があります。カルーセルセットを公開すると、URLと埋め込みコードがアクティブになります。 これにより、スケーラブルで効率のよい配信を実現するため、CDN と統合された Dynamic Media クラウドにもカルーセルが公開されます。

>[!NOTE]
ホットスポットを含む既存のインタラクティブ画像をカルーセルバナー用として使用する場合は、カルーセルバナーを公開した後で、そのインタラクティブ画像を別に公開する必要があります。
また、カルーセルバナーで使用している公開済みインタラクティブ画像を変更する場合は、そのインタラクティブ画像を公開する必要があります。その後、変更がカルーセルバナーに反映されます。

カルーセルバナーの公開方法に関する情報については、[Dynamic Media アセットの公開](/help/assets/dynamic-media/publishing-dynamicmedia-assets.md)を参照してください。

## Web サイトページへのカルーセルバナーの追加 {#adding-a-carousel-banner-to-your-website-page}

カルーセルを作成するためのバナー画像をアップロードし、ホットスポットや画像マップをバナーに追加して、カルーセルセットを公開したら、既存のWebサイトページに追加する準備が整いました。

>[!NOTE]
AEM Sites のユーザーである場合は、インタラクティブメディアコンポーネントをページにドラッグすることにより、カルーセルバナーをページに直接追加できます。See [Adding Dynamic Media Assets to Pages.](/help/assets/dynamic-media/adding-dynamic-media-assets-to-pages.md)

ただし、スタンドアロン AEM Assets のユーザーである場合は、この節で説明するようにカルーセルバナーを手動で Web サイトのランディングページに追加できます。

1. 公開済みのカルーセルバナーの埋め込みコードをコピーします。[Web ページへのビデオビューアまたは画像ビューアの埋め込み](/help/assets/dynamic-media/embed-code.md)を参照してください。

1. AEM Assets からコピーした埋め込みコードを Web ページに追加します。 コピーされた埋め込みコードはレスポンシブです。つまり、ページの埋め込み領域に自動的に適応します。

## カルーセルバナーと既存のクイックビューの統合 {#integrating-the-carousel-banner-with-an-existing-quickview}

注意：この手順はスタンドアロン AEM Assets のユーザーのみに適用されます。

このプロセスの最後の手順は、カルーセルバナーを Web サイトの既存のクイックビュー実装に統合することです。すべてのクイックビュー実装は固有であり、フロントエンド IT 担当者の支援を受けた特別なアプローチが必要になります。

既存のクイックビュー実装は一般的に、Web ページ上で以下の順に発生する、相互に関連するアクションの連鎖となっています。

1. ユーザーは、Web サイトのユーザーインターフェイス内で、特定の要素を起動します。
1. フロントエンドコードは、手順 1 で起動されたユーザーインターフェイス要素に基づいてクイックビュー URL を取得します。
1. フロントエンドコードは、手順 2 で取得した URL を使用して Ajax リクエストを送信します。
1. バックエンドロジックは、対応するクイックビューのデータまたはコンテンツをフロントコードに送り返します。
1. フロントエンドコードは、そのクイックビューのデータまたはコンテンツを読み込みます。
1. （オプション）フロントエンドコードは、読み込んだクイックビューのデータを HTML 表現に変換します。
1. フロントエンドコードは、モーダルダイアログボックスまたはパネルを表示し、エンドユーザー向けに、画面上に HTML コンテンツをレンダリングします。

これらの呼び出しは、必ずしもそれぞれ独立した、Web ページのロジックから任意の手順で呼び出すことができるパブリックな API 呼び出しを表すわけではありません。むしろ、次の手順がすべて前の手順の最終フェーズ（コールバック）に潜むような連鎖的な呼び出しになっています。

カルーセルバナーが手順 1 と（部分的に）手順 2 を置き換えます。それに加えて、ユーザーがカルーセルバナー内のホットスポットまたは画像マップをクリックしたときに、そのユーザー操作がビューアによって処理されます。ビューアは、以前に追加されたすべてのホットスポットまたは画像マップのデータを含む Web ページにイベントを返します。

そのようなイベントハンドラーでは、フロントエンドコードは次の処理を実行します。

* カルーセルバナーから送出されるイベントをリッスンします。
* ホットスポットまたは画像マップのデータに基づいてクイックビュー URL を作成します。
* バックエンドからクイックビューを読み込み、画面上の表示用にレンダリングするプロセスを起動します。

AEM Assets によって返される埋め込みコードには、すぐに使用可能なイベントハンドラーが既に含まれ、コメントアウトされています。

そのため、必要な処理は、このコードのコメントアウトを解除し、ダミーのハンドラー本体を、特定の Web ページ専用のコードに置き換えることだけです。

クイックビュー URL の作成プロセスは、基本的に先ほど説明したホットスポットと画像マップの変数を識別するためのプロセスとは逆のプロセスになります。

[ホットスポットと画像マップの変数の識別](#identifying-hotspot-and-image-map-variables)を参照してください。

クイックビュー URL を起動してクイックビューパネルをアクティベートするための最後の手順では、おそらく IT 部門のフロントエンド IT 担当者の支援が必要になります。フロントエンド IT 担当者は、すぐに使用できるクイックビュー URL を含め、クイックビュー実装を適切な手順から正しく起動するための最適な方法について理解しています。

## クイックビューを使用したカスタムポップアップの作成 {#using-quickviews-to-create-custom-pop-ups}

[クイックビューを使用したカスタムポップアップの作成](/help/assets/dynamic-media/custom-pop-ups.md)を参照してください。