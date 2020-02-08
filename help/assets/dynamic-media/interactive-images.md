---
title: インタラクティブ画像
description: ダイナミックメディアでインタラクティブな画像を使用する方法を説明します。
translation-type: tm+mt
source-git-commit: 6224d193adfb87bd9b080f48937e0af1f03386d6

---


# インタラクティブ画像{#interactive-images}

「買い物可能な」ホットスポットを画像にドラッグ&amp;ドロップすることで、顧客の魅力的な魅力を引き出す静的な画像を簡単に作成できます。買い物可能なホットスポットは、製品やサービスに関する追加情報と、直接販売時点情報である「買い物かごに追加」または「購入」機能を組み合わせています。顧客は、これらのホットスポットをタップまたはクリックして、製品やサービスに直接リンクしたり、買い物かごに追加したり、Webページにリンクしたりできます。顧客関与やWebサイト上のコンバージョンの増加など、直接的なエクスペリエンス。

次に、クイックビューポップアップを含むショッパブルバナーを示します。モデルの上の円（「ホットスポット」）をタップすると、クイックビューがアクティブになります。

![chlimage_1-152](assets/chlimage_1-368.png)

上の図 [に示すWebページ上のインタラクティブ](https://marketing.adobe.com/resources/help/en_US/dm/shoppable-banner/we-fashion-QVzoom/index2-shoppable.html) な画像を参照してください。

## インタラクティブ画像バナーの作成方法 {#watch-how-interactive-image-banners-are-created}

[インタラクティブ画像バナーの作成方法](https://s7d5.scene7.com/s7viewers/html5/VideoViewer.html?videoserverurl=https://s7d5.scene7.com/is/content/&emailurl=https://s7d5.scene7.com/s7/emailFriend&serverUrl=https://s7d5.scene7.com/is/image/&config=Scene7SharedAssets/Universal_HTML5_Video_social&contenturl=https://s7d5.scene7.com/skins/&asset=S7tutorials/InteractiveCarouselBanner)を示す 10 分 33 秒のガイドをご覧ください。ここでは、インタラクティブ画像バナーのプレビュー、編集、配信方法も説明します。

## クイックスタート：インタラクティブ画像 {#quick-start-interactive-images}

次のワークフローの手順説明は、AEM Assets 内のインタラクティブ画像をすぐに使い始めることを目的としたものです。

一部のクイックスタートタスク内には「**例**」という見出しがあります。It contains a brief tutorial that is based on a [web page example that does not yet have Interactive Images added to it](https://marketing.adobe.com/resources/help/en_US/dm/shoppable-banner/we-fashion/landing-0.html).



このチュートリアルでは、Web サイトにインタラクティブ画像を統合する手順が説明されています。

インタラクティブ画像の手順：

1. **（オプション）ホットスポット変数の識別** - AEM Assetsとダイナミックメディアスタンドアロンを使用する場合は、まず既存のQuickview実装で使用する動的変数を指定し、インタラクティブイメージの作成時にホットスポットデータを入力できるようにします。 [（オプション）ホットスポットの変数の識別](#optional-identifying-hotspot-variables)を参照してください。 ただし、AEM Sites または AEM eCommerce（あるいは両方）を使用している場合、この手順は必要ありません。

1. **（オプション）インタラクティブ画像ビューアプリセットの作成** — ホットスポットの表現に使用するグラフィック画像をカスタマイズします。 独自のインタラクティブ画像ビューアプリセットの作成は、標準提供のインタラクティブ画像ビューアプリセット `Shoppable_Banner` を使用する場合には必要ありません。 [（オプション）インタラクティブ画像ビューアプリセットの作成](/help/assets/dynamic-media/managing-viewer-presets.md#creating-a-new-viewer-preset)を参照してください。

1. **画像バナーのアップロード** — インタラクティブにする画像バナーをアップロードします。詳しくは、画 [像バナーのアップロードを参照してくださ](#uploading-an-image-banner)い。

1. **イメージバナーへのホットスポットの追加** - 1つ以上のホットスポットをイメージバナーに追加し、各ホットスポットをハイパーリンク、クイックビュー、エクスペリエンスフラグメントなどのアクションに関連付けます。 ホットスポットを追加した後は、インタラクティブ画像を公開するとタスクが終了します。 [画像バナーへのホットスポットの追加](#adding-hotspots-to-an-image-banner)を参照してください。 [（オプション）インタラクティブ画像のプレビュー](#optional-previewing-interactive-images)を参照してください。必要に応じて、ショッパブルバナーの表示を確認して、インタラクティビティをテストすることができます。インタラクティブ画像アセットの公開方法について詳しくは、[アセットの公開](/help/assets/dynamic-media/publishing-dynamicmedia-assets.md)を参照してください。

1. **AEM でのインタラクティブ画像の Web サイトへの追加** AEM Sites または AEM eCommerce（あるいは両方）を使用している場合、AEM でインタラクティブメディアコンポーネントを Web ページにドラッグすることで、インタラクティブ画像を Web ページに直接追加できます。[ページへの Dynamic Media アセットの追加を参照してください。](/help/assets/dynamic-media/adding-dynamic-media-assets-to-pages.md)を参照してください。 AEM Assets と Dynamic Media をスタンドアロンで使用している場合は、埋め込みコードを Web サイトにコピーしてから、既存のクイックビューに統合する必要があります。[インタラクティブ画像の Web サイトへの統合](#integrating-an-interactive-image-with-your-website)を参照してください。 サードパーティの WCM（Web Content Manager）を使用している場合は、新しいインタラクティブビデオを、Web サイトで使用されている既存のクイックビュー実装に統合する必要があります。[インタラクティブ画像の既存のクイックビューへの統合](#integrating-an-interactive-image-with-an-existing-quickview)を参照してください。

## （オプション）ホットスポットの変数の識別{#optional-identifying-hotspot-variables}

>[!NOTE]
>
>このタスクが必要になるのは次に該当する場合のみです。
>
>* クイックビューをトリガーして、画像にインタラクティブ機能を追加する。
>* eCommerce ソリューション（IBM Websphere Commerce、Elastic Path、hybris、Intershop など）から AEM に製品データを取り出すために、AEM の実装が&#x200B;** eCommerce 統合フレームワークを使用していない。
>
>
AEM の実装が eCommerce を使用している場合は、このタスクをスキップして次のタスクに進みます。

まず、既存のクイックビュー実装で使用されている動的変数を識別します。こうすることで、ホットスポットデータを入力してインタラクティブ画像を作成できます。

AEM Assetsのバナー画像にホットスポットを追加する場合は、SKU（Stock Keeping Unit；在庫保管単位）を割り当てる必要があります提供する個々の製品またはサービスの一意の識別子)と、各ホットスポットに対するオプションの追加変数。 そのようなホットスポットの変数は、後でホットスポットとクイックビューコンテンツを対応付けるために使用されます。

重要なのは、ホットスポットデータに関連付けられる変数の数とタイプを正しく識別することです。バナー画像に追加するそれぞれのホットスポットに、既存のバックエンドシステム内で製品を一意に識別するための十分な情報がある必要があります。

ホットスポットデータに使用する一連の変数を識別するには、様々な方法があります。

既存のクイックビュー実装を担当する IT スペシャリストに相談するだけで十分な場合もあります（通常、そのような IT スペシャリストは、システム内のクイックビューを識別するために必要な最小データセットを理解しています）。ただし、ほとんどの場合は、フロントエンドコードの既存の動作を分析するだけでもかまいません。

クイックビュー実装の大部分では、次の枠組みが使用されています。

* ユーザーは Web サイト上の特定のユーザーインターフェイス要素をアクティベートします。例えば、「クイックビュー」ボタンをクリックします。
* Web サイトでは、必要に応じて、クイックビューのデータまたはコンテンツを読み込むための Ajax リクエストをバックエンドに送信します。
* クイックビューのデータは、Web ページでのレンダリングに備えて、コンテンツに変換されます。
* 最後に、フロントエンドコードによってそのコンテンツが画面上に視覚的にレンダリングされます。

次に、クイックビュー機能が実装されている既存の Web サイトの各領域にアクセスしてクイックビューをトリガーし、そのクイックビューのデータまたはコンテンツを読み込むために Web ページから送信される Ajax URL をキャプチャします。

通常、専門のデバッグツールを使用する必要はありません。最新の Web ブラウザーには、十分なタスクを実行できる Web インスペクターが備わっています。Web インスペクターが搭載されている Web ブラウザーの例を次に示します。

* Google Chrome で、ブラウザーから送信されるすべての HTTP リクエストを参照するには、F12 キーを押してデベロッパーツールパネルを開き、「Network」タブをクリックします。Mac の場合、Command + Option + I キーを押してデベロッパーツールパネルを開き、「Network」タブをクリックします。

* Firefox では、F12 キーを押して Firebug プラグインを有効にして「Net」タブを使用するか、組み込みの Inspector ツールとその「Network」タブを使用します。Mac の場合、Command + Option + I キーを押してデベロッパーツールパネルを開き、「Inspector」タブをクリックします。

ブラウザーでネットワーク監視をオンにして、ページ上でクイックビューをトリガーします。

次に、ネットワークログ内でクイックビューの·Ajax·URL·を見つけ、記録された·URL·を今後の分析のためにコピーします。クイックビューをトリガーするとほとんどの場合、大量のリクエストがサーバーに送信されます。クイックビューの·Ajax·URL·は通常、そのリスト内の最初のほうにあります。It has either a complex query string portion or path, and its response MIME type is either `text/html`, `text/xml`, or `text/javascript`.

このプロセスの実行中は、様々な製品カテゴリーや製品タイプが含まれる Web サイトの様々な領域にアクセスすることが重要です。なぜなら、クイックビュー URL には、ある特定の Web サイトカテゴリーに共通するが、Web サイトの異なる領域にアクセスした場合にのみ変化する部分が存在する場合があるからです。

単純なケースでは、クイックビュー URL 内で変化する唯一の部分が製品 SKU となります。その場合、SKU の値が、ホットスポットをバナー画像に追加するために必要になる唯一のデータです。

一方、複雑なケースでは、クイックビュー URL に SKU 以外の様々な要素が含まれます（カテゴリー ID、カラーコード、サイズコードなど）。その場合、各要素は AEM Assets のショッパブルインタラクティブ画像機能において、ホットスポットデータ定義内の個別の変数になります。

次のクイックビュー URL の例と、その結果となるホットスポットの変数について見てみましょう。

<table>
  <tbody>
  <tr>
    <td><p>単一の SKU（クエリ文字列内）</p> </td>
    <td><p>記録されたクイックビューの URL：</p>
    <ul>
      <li><p><code>https://server/json?productId=866558&amp;source=100</code></p> </li>
      <li><p><code>https://server/json?productId=1196184&amp;source=100</code></p> </li>
      <li><p><code>https://server/json?productId=1081492&amp;source=100</code></p> </li>
      <li><p><code>https://server/json?productId=1898294&amp;source=100</code></p> </li>
    </ul> <p>The only variable part in the URL is the value of the productId= query string parameter, and it is clearly a SKU value. Therefore, our hotspots only need SKU fields populated with values like <strong><code>866558</code></strong>, <strong><code>1196184</code></strong>, <strong><code>1081492</code></strong>, <strong><code>1898294</code></strong>.</p> </td>
  </tr>
  <tr>
    <td><p>単一の SKU（URL パス内）</p> </td>
    <td><p>記録されたクイックビューの URL：</p>
    <ul>
      <li><p><code>https://server/product/6422350843</code></p> </li>
      <li><p><code>https://server/product/1607745002</code></p> </li>
      <li><p><code>https://server/product/0086724882</code></p> </li>
    </ul> <p>The variable part is in the last portion of the path, and it becomes the SKU value of the hotspots: <strong><code>6422350843</code></strong>, <strong><code>1607745002</code></strong>, <strong><code>0086724882</code></strong>.</p> </td>
  </tr>
  <tr>
    <td><p>SKU とカテゴリー ID（クエリ文字列内）</p> </td>
    <td><p>記録されたクイックビューの URL：</p>
    <ul>
      <li><p><code>https://server/quickView/product/?category=1100004&amp;prodId=305466</code></p> </li>
      <li><p><code>https://server/quickView/product/?category=1100004&amp;prodId=310181</code></p> </li>
      <li><p><code>https://server/quickView/product/?category=1740148&amp;prodId=308706</code></p> </li>
    </ul> <p>この場合、URLには2つの異なる部分があります。 The SKU is stored in the <code>prodId</code> parameter and the category ID<code></code> is stored in the <code>category=</code> parameter.</p> <p>そのため、ホットスポット定義はペアになります。つまり、SKU 値と、<code>categoryId</code> という追加の変数です。結果のペアは次のようになります。</p>
    <ul>
      <li><p>SKU is <strong><code>305466</code></strong> and <code>categoryId</code> is <code>1100004</code>.</p> </li>
      <li><p>SKU is <strong><code>310181</code></strong> and <code>categoryId</code> is <strong><code>1100004</code></strong>.</p> </li>
      <li><p>SKU is <strong><code>308706</code></strong> and <code>categoryId</code> is <strong><code>1740148</code></strong>.</p> </li>
    </ul> <p> </p> </td>
  </tr>
  </tbody>
</table>

**例**

You can apply the same approach used in the three examples above to the [demo web page](https://marketing.adobe.com/resources/help/en_US/dm/shoppable-banner/we-fashion/landing-0.html).

このデモ Web ページにはいくつかの製品サムネールがあり、それぞれのサムネールには、「See More」というラベルの付いたクイックビューボタンが用意されています。Web ブラウザーのデバッグツールをアクティブにしたまま各ボタンをクリックし、記録されたクイックビュー URL に注目してください。そのページの 4 つの製品クイックビューのすべてをアクティベートすると、バックエンドに対して次のリストのクイックビューリクエストが作成されます。

* `/datafeed/Men-Windbreaker.json`
* `/datafeed/Men-SimpleHenley.json`
* `/datafeed/Men-CamoPullover.json`
* `/datafeed/Women-QuiltedDownJacket.json`

これらのサーバーコールを見ると、製品固有の情報がリクエストパスのみに含まれることがわかります。また、クエリ文字列がまったく使用されていないこと、2 つの異なるタイプのデータが含まれることもわかります。

* 最初のタイプは Men または Women です。これは「製品カテゴリー」と呼ばれます。
* 2 つ目のタイプは製品名（CamoPullover など）です。これは製品 SKU と考えることができます。

この情報に基づいて、全体的なクイックビュー URL は次のようなパターンであることがわかります。

`/datafeed/$categoryId$-$SKU$.json`

このような分析に基づいて、ホットスポットに対して `categoryId` と `SKU` を使用することになります。

これで、画像バナーをアップロードし、AEM Assets のショッパブルインタラクティブ画像機能を使用して画像バナーにホットスポットを追加する準備ができました。

## （オプション）インタラクティブ画像ビューアプリセットの作成 {#optional-creating-an-interactive-image-viewer-preset}

You can choose to use the default, out-of-the-box Interactive Image viewer preset called `Shoppable_Banner` that comes with AEM Assets. また、インタラクティブ画像で使用するカスタムビューアプリセットを独自に作成することもできます。

カスタムのインタラクティブ画像ビューアプリセットを作成する場合、画像バナー上のホットスポットの外観を指定できます。 ビューアプリセットの作成中に、事前定義済みの画像ギャラリーからホットスポットのグラフィックを選択して使用できます。

ビューアプリセットを保存すると、AEM Assetsのビューアプリセットリストページで、ビューアプリセットが自動的にアクティブ化（オンに）されます。 この機能は、インタラクティブメディアコンポーネントに表示され、アセットを表示するときに必ず表示されることを意味します。 ただし、このビューアプリセットを使用してインタラクティブバナーを*配信するには、ビューアプリセットも*公開*する必要があります（カスタムまたは初期設定のビューアプリセットの場合）。

**インタラクティブ画像ビューアのプリセットを作成するには**

1. 左側のレールで、**[!UICONTROL ツール／アセット／ビューアプリセット]**&#x200B;をタップします。
1. ページの右上隅にある「**[!UICONTROL 作成]**」をタップします。
1. 新規ビューアプリセットダイアログボックスで、インタラクティブバナービューアプリセットを表す名前を入力します。

   この名前が、保存後にビューアプリセットリストページに表示されるタイトルです。

1. リッチメディアタイププルダウンメニューで、「**[!UICONTROL インタラクティブ画像]**」を選択します。
1. 「**[!UICONTROL 作成]**」をタップします。
1. ビューアプリセットを編集ページで、「**[!UICONTROL 外観]**」タブをタップします。
1. 次のいずれかの操作をおこないます。

   * 画像上で使用する独自のホットスポット画像をアップロードするには、アセットピッカーアイコンをタップします。コンテンツを選択ページで、使用するホットスポット画像の場所に移動して画像を選択し、右上隅のチェックマークアイコンをタップします。
   * 事前定義済みのホットスポット画像を選択するには、ホットスポットギャラリーアイコンをタップします。ホットスポットギャラリーパレットで、使用するホットスポット画像をタップします。

1. ページの右上隅にある「**[!UICONTROL 保存]**」をタップします。

   新しいビューアプリセットを忘れずに公開してください。

   [ビューアプリセットの公開](/help/assets/dynamic-media/managing-viewer-presets.md#publishing-viewer-presets)を参照してください。

   これで、画像バナーをアップロードできるようになりました。

## 画像バナーのアップロード {#uploading-an-image-banner}

If you have already uploaded the images that you want to use, advance to the next step, [Adding hotspots to an image banner](#adding-hotspots-to-an-image-banner).

**イメージバナーをアップロードするには**

1. インタラクティブにする画像バナーをアップロードします。

   [アセットのアップロード](/help/assets/manage-digital-assets.md#uploading-assets)を参照してください。

   これで、画像バナーにホットスポットを追加する準備が整いました。この後のタスクを参照してください。

## 画像バナーへのホットスポットの追加 {#adding-hotspots-to-an-image-banner}

ホットスポット管理ページのエディターを使用して、画像バナーにホットスポットを追加できます。

ホットスポットを追加する際に、クイックビューポップアップ表示、ハイパーリンクまたはエクスペリエンスフラグメントとして定義することができます。

[エクスペリエンスフラグメント](/help/sites-cloud/authoring/fundamentals/experience-fragments.md)を参照してください。

>[!NOTE]
>
>ビューアをエクスペリエンスフラグメントに埋め込む場合、インタラクティブ画像のソーシャルメディア共有ツールはサポートされないことに注意してください。この問題を回避するには、ソーシャルメディア共有ツールを備えていないビューアプリセットを使用または作成します。 このようなビューアプリセットを使用すると、エクスペリエンスフラグメントに正常に埋め込むことができます。

現在の作成/編集セッションでは、ページの右上隅近くにある「取り消し」と「やり直し」のオプションがサポートされます。

インタラクティブ画像の作成が完了したら、「プレビュー」を使用して、インタラクティブ画像がユーザーにどのように表示されるかを確認できます。

[（オプション）インタラクティブ画像のプレビュー](#optional-previewing-interactive-images)を参照してください。

>[!NOTE]
>
>インタラクティブ画像またはカルーセルバナーの画像にホットスポットを追加すると、インタラクティブ画像かカルーセルバナーかに関わらず、ホットスポット情報が同じメタデータの場所（画像に対して相対的な場所）に格納されます。つまり、どちらのビューアでも、同じ画像を定義済みのホットスポットデータと一緒に簡単に再利用できます。

>  ただし、カルーセルバナーでは、画像上の画像マップ（ホットスポットを含むことができる）がサポートされることに注意してください。インタラクティブ画像ではサポートされません。同じ画像を使用するインタラクティブ画像またはカルーセルバナーを作成する場合には、このことに注意してください。同じ画像の別のコピーを使用してインタラクティブ画像とカルーセルバナーを作成することをお勧めします。
>
>[カルーセルバナー](/help/assets/dynamic-media/carousel-banners.md)も参照してください。

>[!NOTE]
>
>ホットスポットを含むインタラクティブ画像を編集しているときに、画像を切り取ると、ホットスポットは削除されます。

**イメージバナーにホットスポットを追加するには**

1. Assets ビューで、インタラクティブにする画像バナーに移動します。
1. 次のいずれかの操作をおこないます。

   * Hover on the image, then tap **[!UICONTROL Select]** (checkmark icon). ツールバーの「**[!UICONTROL 編集]**」をタップします。

   * Hover on the image, then tap **[!UICONTROL More actions]** (three dots icon) **[!UICONTROL > Edit]**.

   * 画像をタップして、詳細ビューページで画像を開きます。ツールバーの「**[!UICONTROL 編集]**」をタップします。

1. ページの左上隅にある「**[!UICONTROL ホットスポットを追加]**」（指先アイコン）をタップして、ホットスポット管理ページを開きます。
1. ページの左上隅にある「**[!UICONTROL ホットスポット]**」をタップします。

1. ホットスポット管理ページの左上隅にある「**[!UICONTROL ホットスポット]**」をタップします。
1. 画像上で、ホットスポットを表示する場所をタップします。必要に応じて、ホットスポットをドラッグして場所を調整します。
1. 必要に応じて手順 a と b を繰り返し、他のホットスポットを追加します。
1. （オプション）ホットスポットを削除するには、そのホットスポットを画像上で選択した後、「**[!UICONTROL ホットスポット]**」見出しの下にある&#x200B;**[!UICONTROL 削除]**（ごみ箱アイコン）をタップします。

1. 「名前」テキストフィールドにホットスポットの名前を入力します。この名前は、選択したホットスポットドロップダウンリストにも表示されます。
1. 次のいずれかの操作をおこないます。

   * 「**[!UICONTROL クイックビュー]**」をタップします。

      * AEM Sites または eCommerce のユーザーである場合は、製品ピッカーアイコン（虫眼鏡）をタップまたはクリックして、製品を選択ページを開きます。使用する製品をタップまたはクリックし、ページの右上隅にある「**選択**」をタップして、「ホットスポット管理」ページに戻ります。
      * If you are *not* an AEM Sites or eCommerce customer

         * See [Identifying hotspot variables](#optional-identifying-hotspot-variables); you will need to define these variables.
         * 次に、SKU値を手動で入力します。 「SKU値」テキストフィールドに、製品のSKU（在庫保管単位）を入力します。これは、提供する個々の製品またはサービスの一意の識別子です。 入力したSKU値によってクイックビューテンプレートの可変部分が自動的に設定され、タップされたホットスポットを特定のSKUのクイックビューに関連付けることができます。
         * (Optional) If there are other variables within the Quickview that you need to use to further identify a product, tap **[!UICONTROL Add Generic Variable]**. テキストフィールドで、追加の変数を指定します。 例えば、追加の変数として `category=Mens` などと指定します。
   * 「**[!UICONTROL ハイパーリンク]**」をタップします。

      * AEM Sites のユーザーである場合は、サイトセレクターアイコン（フォルダー）をタップまたはクリックして URL に移動します。インタラクティブコンテンツに相対 URL のリンク（特に AEM Sites ページへのリンク）がある場合、URL ベースのリンク方法は使用できません。
      * スタンドアロンユーザーである場合は、「HREF」テキストフィールドに、リンクされる Web ページへの完全な URL パスを指定します。
   このリンクを新しいブラウザータブで開く（推奨のデフォルト）か同じタブで開くかを指定してください。

   詳しくは、[セレクターの操作](/help/assets/dynamic-media/working-with-selectors.md)を参照してください。

   * 「**[!UICONTROL エクスペリエンスフラグメント]**」をタップします。

      * AEM Sites のユーザーである場合は、検索アイコン（虫眼鏡）をタップまたはクリックしてエクスペリエンスフラグメントページを開きます。使用するエクスペリエンスフラグメントをタップまたはクリックし、ページの右上隅にある「選択」をタップして、ホットスポット管理ページに戻ります。[エクスペリエンスフラグメント](/help/sites-cloud/authoring/fundamentals/experience-fragments.md)を参照してください。

      * エクスペリエンスフラグメントがバナーに表示されるときの幅と高さを指定します。

         >[!NOTE]
         >
         >ビューアをエクスペリエンスフラグメントに埋め込む場合、インタラクティブ画像のソーシャルメディア共有ツールはサポートされないことに注意してください。この問題を回避するには、ソーシャルメディア共有ツールを備えていないビューアプリセットを使用または作成します。 このようなビューアプリセットを使用すると、エクスペリエンスフラグメントに正常に埋め込むことができます。



1. 「**[!UICONTROL 保存]**」をタップして作業内容を保存し、参照ページに戻ります。
1. インタラクティブ画像を公開します。公開すると、バナーをクラウドで配信できるようになり、サードパーティの Web サイトに統合する必要がある場合は埋め込みコードが生成されます。

   [アセットの公開](/help/assets/manage-digital-assets.md#publish-assets)を参照してください。

   ホットスポットを追加してインタラクティブ画像を公開したら、次に既存の Web サイトにその画像を追加できます。

   [インタラクティブ画像の Web サイトへの統合](#integrating-an-interactive-image-with-your-website)を参照してください。

   >[!NOTE]
   >
   >ホットスポットを含むインタラクティブ画像を編集しているときに、画像を切り取ると、ホットスポットは削除されます。

### （オプション）インタラクティブ画像のプレビュー {#optional-previewing-interactive-images}

プレビューを使用して、インタラクティブイメージが顧客にどのように表示されるかを確認し、イメージのホットスポットをテストして、期待どおりの動作を示すことができます。

インタラクティブ画像の設定が完了したら、この画像を公開できます。[Web ページへのビデオビューアまたは画像ビューアの埋め込み](/help/assets/dynamic-media/embed-code.md)を参照してください。[Web アプリケーションへの URL のリンク](/help/assets/dynamic-media/linking-urls-to-yourwebapplication.md)を参照してください。インタラクティブコンテンツに相対 URL のリンク（特に AEM Sites ページへのリンク）がある場合、URL ベースのリンク方法は使用できません。See [Adding Dynamic Media Assets to Pages.](/help/assets/dynamic-media/adding-dynamic-media-assets-to-pages.md)

**インタラクティブ画像をプレビューするには**

1. Assets ビューで、作成した既存のインタラクティブ画像の場所に移動し、タップしてプレビューで表示します。
1. Near the upper-left corner of the Preview page, in the Content drop-down list, tap **[!UICONTROL Viewers]**.
1. ビューアリストで「**[!UICONTROL Shoppable_Banner]**」または作成したインタラクティブ画像ビューアプリセットの名前をタップします。
1. 画像上のホットスポットをタップして、関連するアクションをテストします。

## インタラクティブ画像アセットの公開 {#publishing-interactive-image-assets}

インタラクティブ画像アセットの公開方法について詳しくは、[アセットの公開](/help/assets/dynamic-media/publishing-dynamicmedia-assets.md)を参照してください。

## インタラクティブ画像の Web サイトへの統合 {#integrating-an-interactive-image-with-your-website}

バナー画像をアップロードし、ホットスポットを画像に追加してインタラクティブ画像を公開したら、次に Web サイトページにその画像を追加できます。

AEM Sites のユーザーである場合は、インタラクティブメディアコンポーネントをページにドラッグすることによりインタラクティブ画像を追加できます。See [Adding Dynamic Media Assets to Pages.](/help/assets/dynamic-media/adding-dynamic-media-assets-to-pages.md)

スタンドアロン AEM Assets のユーザーである場合は、この節で説明するようにインタラクティブ画像を手動で Web サイトに追加できます。

1. 公開済みのインタラクティブ画像の埋め込みコードをコピーします。[Web ページへのビデオビューアまたは画像ビューアの埋め込み](/help/assets/dynamic-media/embed-code.md)を参照してください。

1. コピーした埋め込みコードを、Web ページ内の必要な場所に追加します。コピーされた埋め込みコードは、割り当てられた領域に自動的に収まるようにレスポンシブ環境用に設定されます。

**例**

デモの [Webサイトの例を見ると](https://marketing.adobe.com/resources/help/en_US/dm/shoppable-banner/we-fashion/landing-0.html)、3人の男性の写真は静的タグで `IMG` す。

```xml
<img class="img-responsive" width="100%" title="Hero Image 2" alt="Hero Image 2" src="images/shoppable-banner.jpg">
```

統合は、タグを削除し、AEM Assetsか `IMG` らコピーした埋め込みコードに置き換えるだけで簡単です。 結果は、3つの円のホットスポ [ットを含むページ上で買い物が可能なインタラクティブ画像を示しています](https://marketing.adobe.com/resources/help/en_US/dm/shoppable-banner/we-fashion/landing-1.html)。

>[!NOTE]
>
>この時点では、デモ Web サイトのショッパブルインタラクティブ画像上のホットスポットは表示用のみで、まだ既存のクイックビューと統合されていません。

レスポンシブ環境向けにショッパブルインタラクティブ画像に「切り抜き」を適用するために、`ZoomView.iscommand` というインタラクティブ画像設定属性をパスに追加できます。ここでの `ZoomView` は呼び出すコンポーネントで、`iscommand` は適用する「crop」画像サービングコマンドです。

[ZoomView.iscommand](https://docs.adobe.com/content/help/en/dynamic-media-developer-resources/library/viewers-for-aem-assets-only/interactive-images/command-reference-configuration-attributes-interactive-images/r-html5-aem-interactive-image-config-attrib-zoomview-iscommand.html) 設定属性を参照してください。

[crop](https://docs.adobe.com/content/help/en/dynamic-media-developer-resources/image-serving-api/image-serving-api/http-protocol-reference/command-reference/r-crop.html) 画像サービングコマンドを参照してください。

これで、インタラクティブ画像を Web サイト上の既存のクイックビューに統合できるようになりました。

## インタラクティブ画像の既存のクイックビューへの統合 {#integrating-an-interactive-image-with-an-existing-quickview}

>[!NOTE]
>
>このタスクはスタンドアロン AEM Assets のユーザーのみに適用されます。

このプロセスの最後の手順は、インタラクティブ画像を Web サイトの既存のクイックビュー実装に統合することです。すべてのケースで機能する統合のソリューションはありません。すべてのクイックビュー実装は固有であり、フロントエンド IT 担当者の支援を受けた特別なアプローチが必要になります。

既存のクイックビュー実装は一般的に、Web ページ上で以下の順に発生する、相互に関連するアクションの連鎖となっています。

1. ユーザーは、Web サイトのユーザーインターフェイス内で、特定の要素を起動します。
1. フロントエンドコードは、手順 1 で起動されたユーザーインターフェイス要素に基づいてクイックビュー URL を取得します。
1. フロントエンドコードは、手順 2 で取得した URL を使用して Ajax リクエストを送信します。
1. バックエンドロジックは、対応するクイックビューのデータまたはコンテンツをフロントコードに送り返します。
1. フロントエンドコードは、そのクイックビューのデータまたはコンテンツを読み込みます。
1. （オプション）フロントエンドコードは、読み込んだクイックビューのデータを HTML 表現に変換します。
1. フロントエンドコードは、モーダルダイアログボックスまたはパネルを表示し、エンドユーザー向けに、画面上に HTML コンテンツをレンダリングします。

これらの呼び出しは、必ずしもそれぞれ独立した、Web ページのロジックから任意の手順で呼び出すことができるパブリックな API 呼び出しを表すわけではありません。むしろ、次の手順がすべて前の手順の最終フェーズ（コールバック）に潜むような連鎖的な呼び出しになっています。

ショッパブルインタラクティブ画像が手順 1 と（部分的に）手順 2 を置き換えるのと同時に、ユーザーがショッパブル画像内のホットスポットをクリックしたときに、そのユーザー操作がビューアによって処理されます。ビューアは、AEM Assets に以前に追加されたすべてのホットスポットデータを含む Web ページに、イベントを返します。

そのようなイベントハンドラーでは、フロントエンドコードは次の処理を実行します。

* ショッパブルインタラクティブ画像から送出されるイベントをリッスンします。
* ホットスポットデータに基づいてクイックビュー URL を作成します。
* バックエンドからクイックビューを読み込み、画面上の表示用にレンダリングするプロセスを起動します。

AEM Assets によって返される埋め込みコードには、次のハイライトされたコードのように、既にすぐに使用可能なイベントハンドラーがコメントアウトされた状態で含まれています。

```xml
        var s7interactiveimageviewer = new s7viewers.InteractiveImage({
            "containerId" : "s7interactiveimage_div",
            "params" : {
                "serverurl" : "https://aodmarketingna.assetsadobe.com/is/image",
                "contenturl" : "https://aodmarketingna.assetsadobe.com/",
                "config" : "/etc/dam/presets/viewer/Shoppable_Media",
                "asset" : "/content/dam/mac/aodmarketingna/shoppable-banner/shoppable-banner.jpg" }
        })
        /* // Example of interactive image event for Quickview.
             s7interactiveimageviewer.setHandlers({
                "quickViewActivate": function(inData) {
                    var sku=inData.sku; //SKU for product ID
                    //To pass other parameter from the hotspot, you will need to add custom parameter during the hotspot setup as parameterName=value
                    loadQuickView(sku); //Replace this call with your Quickview plugin
                    //Please refer to your Quickviewer plugin for the Quickview call
                 },
             });
        */
        s7interactiveimageviewer.init();
```

そのため、必要な処理は、このコードのコメントアウトを解除し、ダミーのハンドラー本体を、特定の Web ページ専用のコードに置き換えることだけです。

クイックビュー URL の作成プロセスは、基本的に先ほど説明したホットスポットの変数を識別するためのプロセスとは逆のプロセスになります。

[ホットスポットの変数の識別](#optional-identifying-hotspot-variables)を参照してください。

以前のクイックビュー URL の例を使用した場合、クイックビュー URL の各ケースでの作成方法は次の例のようになります。

<table>
 <tbody>
  <tr>
   <td><p>単一の SKU（クエリー文字列内）</p> </td>
   <td><code class="code">s7interactiveimageviewer.setHandlers({
      "quickViewActivate": function(inData) {
      var quickViewUrl = "https://server/json?productId=" + inData.sku + "&amp;amp;source=100";
      },
      });</code></td>
  </tr>
  <tr>
   <td><p>単一の SKU（URL パス内）</p> </td>
   <td><code class="code">s7interactiveimageviewer.setHandlers({
      "quickViewActivate": function(inData) {
      var quickViewUrl = "https://server/product/" + inData.sku;
      },
      });</code></td>
  </tr>
  <tr>
   <td><p>SKU とカテゴリ ID（クエリー文字列内）</p> </td>
   <td><code class="code">s7interactiveimageviewer.setHandlers({
      "quickViewActivate": function(inData) {
      var quickViewUrl = "https://server/quickView/product/?category=" + inData.categoryId + "&amp;amp;prodId=" + inData.sku;
      },
      });</code></td>
  </tr>
 </tbody>
</table>

クイックビュー URL をトリガーしてクイックビューパネルをアクティベートするための最後の手順では、おそらく IT 部門のフロントエンド IT 担当者の支援が必要になります。フロントエンド IT 担当者は、すぐに使用できるクイックビュー URL を含め、クイックビュー実装を適切な手順から正しくトリガーするための最適な方法について理解しています。

これらの手順をデモ Web サイトに適用してショッパブルインタラクティブ画像をクイックビューのコードに統合する方法を確認できます。先ほど、クイックビュー URL の構造を次のように識別しました。

```xml
/datafeed/$categoryId$-$SKU$.json
```

この URL を `quickViewActivate` ハンドラー内で再構成するために、ビューアのコードからハンドラーに渡される `categoryId` オブジェクト内の `SKU` フィールドと `inData` フィールドを使用できます。

```xml
var sku=inData.sku;
var categoryId=inData.categoryId;
var quickViewUrl = "datafeed/" + categoryId + "-" + sku + ".json";
```

The demo website is triggering the Quickview dialog box using a simple `loadQuickView()` function call. この関数は、1 つの引数（クイックビューデータの URL）のみを受け取ります。したがって、ショッパブルインタラクティブ画像を統合するために必要な最後の手順は、`quickViewActivate` ハンドラーに次のコード行を追加することです。

```xml
loadQuickView(quickViewUrl);
```

次に、ソースコード全体を示します。

```xml
 var s7interactiveimageviewer = new s7viewers.InteractiveImage({
  "containerId" : "s7interactiveimage_div",
  "params" : {
   "serverurl" : "https://aodmarketingna.assetsadobe.com/is/image",
   "contenturl" : "https://aodmarketingna.assetsadobe.com/",
   "config" : "/etc/dam/presets/viewer/Shoppable_Media",
   "asset" : "/content/dam/mac/aodmarketingna/shoppable-banner/shoppable-banner.jpg" }
 })
   s7interactiveimageviewer.setHandlers({
   "quickViewActivate": function(inData) {
     var sku=inData.sku;
     var categoryId=inData.categoryId;
    var quickViewUrl = "datafeed/" + categoryId + "-" + sku + ".json";
    loadQuickView(quickViewUrl);
    },
   });
 s7interactiveimageviewer.init();
```

完全に統 [合されたインタラクティブ画像を含む最終的なデモWebサイト](https://marketing.adobe.com/resources/help/en_US/dm/shoppable-banner/we-fashion/landing-3.html)。

## クイックビューを使用したカスタムポップアップの作成 {#using-quickviews-to-create-custom-pop-ups}

[クイックビューを使用したカスタムポップアップの作成](/help/assets/dynamic-media/custom-pop-ups.md)を参照してください。