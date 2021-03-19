---
title: インタラクティブ画像
description: Dynamic Media でのインタラクティブ画像の使用方法について説明します。
feature: インタラクティブ画像
topic: 開業医
translation-type: tm+mt
source-git-commit: 0f2b7176b44bb79bdcd1cecf6debf05bd652a1a1
workflow-type: tm+mt
source-wordcount: '4249'
ht-degree: 47%

---


# インタラクティブ画像 {#interactive-images}

「買い物客」のホットスポットを画像にドラッグ&amp;ドロップすることで、静的な画像をリッチで魅力的なエクスペリエンスに簡単にできます。買い物可能なホットスポットは、製品やサービスに関する追加情報と、直接販売時点に関する「買い物かごに追加」機能や「購入」機能を組み合わせています。 顧客は、製品やサービスに直接リンクするこれらのホットスポットをタップしたり、買い物かごに追加したり、Webページにリンクさせたりできます。 このような直接的なエクスペリエンスによって、顧客エンゲージメントやWebサイト上のコンバージョンが向上します。

以下は、クイック表示ポップアップウィンドウを含む買い物可能なバナーです。 ユーザは、モデル上の円または「ホットスポット」をタップして、クイック表示をアクティブにします。

![chlimage_1-152](assets/chlimage_1-368.png)

上の図に示す Web ページの[実際のインタラクティブ画像](https://marketing.adobe.com/resources/help/en_US/dm/shoppable-banner/we-fashion-QVzoom/index2-shoppable.html)を参照してください。

## インタラクティブ画像バナーの作成方法 {#watch-how-interactive-image-banners-are-created}

[インタラクティブ画像バナーの作成方法](https://s7d5.scene7.com/s7viewers/html5/VideoViewer.html?videoserverurl=https://s7d5.scene7.com/is/content/&amp;emailurl=https://s7d5.scene7.com/s7/emailFriend&amp;serverUrl=https://s7d5.scene7.com/is/image/&amp;config=Scene7SharedAssets/Universal_HTML5_Video_social&amp;contenturl=https://s7d5.scene7.com/skins/&amp;asset=S7tutorials/InteractiveCarouselBanner)を示す 10 分 33 秒のガイドをご覧ください。また、インタラクティブな画像バナーのプレビュー、編集、配信の方法も学習します。

## クイックスタート：インタラクティブ画像 {#quick-start-interactive-images}

次のワークフローの手順説明は、AEM Assets 内のインタラクティブ画像をすぐに使い始めることを目的としたものです。

一部のクイックスタートタスク内には「**例**」という見出しがあります。これには、[まだインタラクティブ画像が追加されていないサンプル Web ページ](https://marketing.adobe.com/resources/help/en_US/dm/shoppable-banner/we-fashion/landing-0.html)に基づいた簡単なチュートリアルが含まれています。



このチュートリアルでは、Web サイトにインタラクティブ画像を統合する手順が説明されています。

インタラクティブ画像の手順：

1. **（オプション）ホットスポット変数の識別**。Adobe Experience ManagerアセットとDynamic Mediaスタンドアロンを使用する場合は、既存のクイック表示実装で使用する動的変数を指定します。 これにより、インタラクティブ画像を作成する際に、ホットスポットデータを入力できるようになります。 [（オプション）ホットスポットの変数の識別](#optional-identifying-hotspot-variables)を参照してください。ただし、AEM Sites または AEM eCommerce（あるいは両方）を使用している場合、この手順は必要ありません。

1. **（オプション）インタラクティブ画像ビューアプリセットの作成**。ホットスポットを表すために使用するグラフィックイメージをカスタマイズします。独自のインタラクティブ画像ビューアプリセットの作成は、標準提供のインタラクティブ画像ビューアプリセット `Shoppable_Banner` を使用する場合には必要ありません。[（オプション）インタラクティブ画像ビューアプリセットの作成](/help/assets/dynamic-media/managing-viewer-presets.md#creating-a-new-viewer-preset)を参照してください。

1. **画像バナーのアップロード**。インタラクティブにする画像バナーをアップロードします。詳しくは、画像バナーの [アップロードを参照してください](#uploading-an-image-banner)。

1. **イメージバナーへのホットスポットの追加**。イメ追加ージバナーの1つ以上のホットスポット。各ハイパーリンクを、ハイパーリンク、クイック表示、エクスペリエンスフラグメントなどのアクションに関連付けます。 ホットスポットを追加した後は、インタラクティブ画像を公開するとタスクが終了します。[画像バナーへのホットスポットの追加](#adding-hotspots-to-an-image-banner)を参照してください。[（オプション）インタラクティブ画像のプレビュー](#optional-previewing-interactive-images)を参照してください。必要に応じて、ショッパブルバナーの表示を確認して、インタラクティビティをテストすることができます。インタラクティブ画像アセットの公開方法について詳しくは、[アセットの公開](/help/assets/dynamic-media/publishing-dynamicmedia-assets.md)を参照してください。

1. **WebサイトまたはExperience Managerー内のWebサイトにインタラクティブ画像を追加する**。サイト、eコマース、またはその両方を使用する場合は、インタラクティブExperience ManagerをWebページに直接追加できます。 インタラクティブメディアコンポーネントをページにドラッグします。 [ページへの Dynamic Media アセットの追加を参照してください。](/help/assets/dynamic-media/adding-dynamic-media-assets-to-pages.md)
Experience ManagerAssetsとDynamic Mediaスタンドアロンを使用する場合は、Webサイトの埋め込みコードをコピーします。次に、既存のクイック表示と統合します。 [インタラクティブ画像の Web サイトへの統合](#integrating-an-interactive-image-with-your-website)を参照してください。サードパーティのWCM(Web Content Manager)を使用する場合は、新しいインタラクティブビデオをWebサイトで使用している既存のクイック表示と統合します。 [インタラクティブ表示と既存のクイック画像の統合](#integrating-an-interactive-image-with-an-existing-quickview)を参照してください。

## （オプション）ホットスポットの変数の識別 {#optional-identifying-hotspot-variables}

>[!NOTE]
>
>このタスクが必要になるのは次に該当する場合のみです。
>
>* クイック表示に対してトリガーして、インタラクティブ機能を画像に追加する場合。
>* お使いのExperience Managerの導入では、eCommerce統合フレームワークを&#x200B;*使用せず*、eCommerceソリューションから製品データをExperience Managerに取り込みます。 このようなソリューションには、IBM WebSphere® Commerce、Elastic Path、hybris、Intershopなどがあります。

>
>
AEM の実装で AEM eCommerce を使用している場合は、このタスクをスキップして次のタスクに進みます。

既存のクイック表示の実装で使用される動的変数を識別して、ホットスポットデータを入力してインタラクティブイメージを作成できるように開始します。

Experience Managerアセットのバナー画像にホットスポットを追加する場合は、SKU(Stock Keeping Unit)を割り当てます。 SKUは、オファー対象の個々の製品やサービスに固有の識別子です。 また、各ホットスポットにオプションの変数を追加します。 このようなホットスポット変数は、後でホットスポットとクイック表示のコンテンツを照合するために使用されます。

重要なのは、ホットスポットデータに関連付けられる変数の数とタイプを正しく識別することです。バナー画像に追加するそれぞれのホットスポットに、既存のバックエンドシステム内で製品を一意に識別するための十分な情報がある必要があります。

ホットスポットデータに使用する一連の変数を識別するには、様々な方法があります。

既存のクイック表示の導入を担当するITスペシャリストに相談するのに十分な場合があります。 このようなユーザーは、システム内のクイック表示を識別するために必要な最小データのセットを知ることが多いでしょう。 ただし、フロントエンドコードの既存の動作を単純に分析することもできます。

ほとんどのクイック表示の実装では、次のようなパラダイムが使用されます。

* ユーザーがWebサイト上でユーザーインターフェイス要素をアクティブにします。例えば、「クイック表示」ボタンをクリックします。
* Webサイトは、必要に応じて、クイック表示のデータまたはコンテンツを読み込むために、Ajaxリクエストをバックエンドに送信します。
* クイック表示データは、Webページへのレンダリングに備えてコンテンツに変換されます。
* 最後に、フロントエンドコードによってそのコンテンツが画面上に視覚的にレンダリングされます。

次に、クイック表示機能が実装されている既存のWebサイトの様々な領域を訪問します。 次に、クイック表示をトリガーし、Webページから送信されたAjax URLを取得して、クイック表示のデータまたはコンテンツを読み込みます。

通常、専門のデバッグツールを使用する必要はありません。最新の Web ブラウザーには、十分なタスクを実行できる Web インスペクターが備わっています。Web インスペクターが搭載されている Web ブラウザーの例を次に示します。

* Google Chrome で、ブラウザーから送信されるすべての HTTP リクエストを参照するには、F12 キーを押してデベロッパーツールパネルを開き、「Network」タブをクリックします。Mac の場合、Command + Option + I キーを押してデベロッパーツールパネルを開き、「Network」タブをクリックします。

* FirefoxでF12キーを押して、Firebugプラグインをアクティブ化し、「Net」タブを使用します。 または、組み込みのインスペクタツールと[ネットワーク]タブを使用できます。
Mac の場合、Command + Option + I キーを押してデベロッパーツールパネルを開き、「Inspector」タブをクリックします。

ブラウザーでネットワーク監視を有効にする場合は、ページのクイック表示をトリガーします。

次に、表示ログでクイックネットワークのAjax URLを探し、記録したURLをコピーして、分析を後で行います。 通常、クイック表示をトリガーすると、サーバーに送信される要求が多数あります。 通常、クイック表示のAjax URLはリストの最初のURLの1つです。 この URL には複雑なクエリ文字列部分またはパスが含まれ、その応答の MIME タイプは `text/html`、`text/xml`、`text/javascript` のいずれかになります。

このプロセスでは、製品のカテゴリやタイプを変えて、Webサイトの様々な領域を訪問することが重要です。 クイック表示URLには、特定のWebサイトカテゴリに共通する部分を含めることができるからです。 ただし、変更されるのは、Webサイトの別の領域を訪問した場合のみです。

最も単純なケースでは、クイック表示URLの唯一の変数部分が製品SKUです。この場合、SKU値は、バナー画像にホットスポットを追加するために必要な唯一のデータ要素です。

ただし、複雑な場合は、クイック表示URLにはSKUに加えて様々な要素があります。 例えば、様々な要素には、カテゴリID、カラーコード、サイズコードが含まれます。 このような場合、すべての要素は、Experience Managerアセットのショップ可能なインタラクティブ画像機能のホットスポットデータ定義内の個別の変数になります。

クイック表示URLの次の例と、その結果得られるホットスポット変数を考えてみましょう。

<table>
  <tbody>
  <tr>
    <td><p>単一の SKU（クエリ文字列内）</p> </td>
    <td><p>記録されるクイック表示URLは次のとおりです。</p>
    <ul>
      <li><p><code>https://server/json?productId=866558&amp;source=100</code></p> </li>
      <li><p><code>https://server/json?productId=1196184&amp;source=100</code></p> </li>
      <li><p><code>https://server/json?productId=1081492&amp;source=100</code></p> </li>
      <li><p><code>https://server/json?productId=1898294&amp;source=100</code></p> </li>
    </ul> <p>この URL で変化する唯一の部分は productId= というクエリ文字列パラメーターの値であり、これが SKU 値であることは明白です。したがって、ホットスポットで必要なのは、<strong><code>866558</code></strong>、<strong><code>1196184</code></strong>、<strong><code>1081492</code></strong>、<strong><code>1898294</code></strong>のような値をSKUフィールドに入力することだけです。</p> </td>
  </tr>
  <tr>
    <td><p>単一の SKU（URL パス内）</p> </td>
    <td><p>記録されるクイック表示URLは次のとおりです。</p>
    <ul>
      <li><p><code>https://server/product/6422350843</code></p> </li>
      <li><p><code>https://server/product/1607745002</code></p> </li>
      <li><p><code>https://server/product/0086724882</code></p> </li>
    </ul> <p>パスの最後の要素が変化する部分であり、これがホットスポットの SKU 値（<strong><code>6422350843</code></strong>、<strong><code>1607745002</code></strong>、<strong><code>0086724882</code></strong>）になります。</p> </td>
  </tr>
  <tr>
    <td><p>SKU とカテゴリ ID（クエリ文字列内）</p> </td>
    <td><p>記録されるクイック表示URLは次のとおりです。</p>
    <ul>
      <li><p><code>https://server/quickView/product/?category=1100004&amp;prodId=305466</code></p> </li>
      <li><p><code>https://server/quickView/product/?category=1100004&amp;prodId=310181</code></p> </li>
      <li><p><code>https://server/quickView/product/?category=1740148&amp;prodId=308706</code></p> </li>
    </ul> <p>この場合、URL には変化する部分が 2 つあります。SKU が <code>prodId</code> パラメーターに、カテゴリ ID<code></code> が <code>category=</code> パラメーターに格納されています。</p> <p>そのため、ホットスポット定義はペアになります。つまり、SKU値と<code>categoryId</code>という追加の変数です。 結果のペアは次のようになります。</p>
    <ul>
      <li><p>SKU が <strong><code>305466</code></strong>、<code>categoryId</code> が <code>1100004</code>。</p> </li>
      <li><p>SKU が <strong><code>310181</code></strong>、<code>categoryId</code> が <strong><code>1100004</code></strong>。</p> </li>
      <li><p>SKU が <strong><code>308706</code></strong>、<code>categoryId</code> が <strong><code>1740148</code></strong>。</p> </li>
    </ul> <p> </p> </td>
  </tr>
  </tbody>
</table>

**例**

この 3 つの例で使用されているものと同じアプローチを次の[デモ Web ページ](https://marketing.adobe.com/resources/help/en_US/dm/shoppable-banner/we-fashion/landing-0.html)に適用できます。

デモのWebページには複数の商品サムネールがあり、それぞれ「詳細を表示」というラベルが付いたクイック表示ボタンがあります。Webブラウザーのデバッグツールをアクティブにしたまま、各ボタンをクリックし、記録されたクイック表示URLをメモします。ページ上で使用可能な4つの製品クイック表示をすべてアクティブ化すると、バックエンドに対して行われたクイック表示リクエストのリストは次のとおりです。

* `/datafeed/Men-Windbreaker.json`
* `/datafeed/Men-SimpleHenley.json`
* `/datafeed/Men-CamoPullover.json`
* `/datafeed/Women-QuiltedDownJacket.json`

サーバーコールを見ると、製品固有の情報が要求パスにのみ存在することがわかります。 また、クエリ文字列がまったく使用されていないこと、2 つの異なるタイプのデータが含まれることもわかります。

* 最初のタイプは Men または Women です。これは「製品カテゴリ」と呼ばれます。
* 2つ目のタイプは製品名です（CamoPulloverなど）。これは、おそらく製品のSKUです。

この情報を取得すると、クイック表示URL全体に次のパターンが適用されます。

`/datafeed/$categoryId$-$SKU$.json`

このような分析に基づいて、ホットスポットに対して `categoryId` と `SKU` を使用することになります。

これで、画像バナーをアップロードし、AEM Assets のショッパブルインタラクティブ画像機能を使用して画像バナーにホットスポットを追加する準備ができました。

## （オプション）インタラクティブ画像ビューアプリセットの作成  {#optional-creating-an-interactive-image-viewer-preset}

AEM Assets に含まれる、デフォルトの標準提供インタラクティブ画像ビューアプリセット（`Shoppable_Banner`）を使用するように選択できます。または、インタラクティブ画像で使用するために独自のカスタムビューアプリセットを作成できます。

カスタムインタラクティブ画像ビューアプリセットを作成する場合は、画像バナーのホットスポットの外観を決定できます。ビューアプリセットの作成中に、事前定義済みの画像ギャラリーからホットスポットのグラフィックを選択して使用できます。

ビューアプリセットを保存すると、AEM Assets のビューアプリセットリストページで自動的にアクティベートされます（有効になります）。つまり、そのビューアプリセットは、インタラクティブメディアコンポーネントで、アセットを表示するときに常に表示されます。ただし、*このビューアプリセットを持つインタラクティブバナーを*&#x200B;配信するには、ビューアプリセットも&#x200B;*公開*&#x200B;します。 このルールは、カスタムまたは初期設定のビューアプリセットに対して適用されます。

**インタラクティブ画像ビューアプリセットを作成するには：**

1. 左側のパネルで、**[!UICONTROL ツール／アセット／ビューアプリセット]**&#x200B;をタップします。
1. ページの右上隅にある「**[!UICONTROL 作成]**」をタップします。
1. 新規ビューアプリセットダイアログボックスで、インタラクティブバナービューアプリセットを表す名前を入力します。

   このタイトルは、保存後、ビューアプリセットリストページに表示されます。

1. 「リッチメディアタイプ」プルダウンメニューで、「**[!UICONTROL インタラクティブ画像]**」を選択します。
1. 「**[!UICONTROL 作成]**」をタップします。
1. ビューアプリセットを編集ページで、「**[!UICONTROL 外観]**」タブをタップします。
1. 次のいずれかの操作をおこないます。

   * 画像上で使用する独自のホットスポット画像をアップロードするには、アセットピッカーアイコンをタップします。コンテンツを選択ページで、使用するホットスポット画像に移動し、それを選択します。 右上隅のチェックマークアイコンをタップします。
   * 事前定義済みのホットスポット画像を選択するには、ホットスポットギャラリーアイコンをタップします。ホットスポットギャラリーパレットで、使用するホットスポット画像をタップします。

1. ページの右上隅にある「**[!UICONTROL 保存]**」をタップします。

   新しいビューアプリセットを忘れずに公開してください。

   [ビューアプリセットの公開](/help/assets/dynamic-media/managing-viewer-presets.md#publishing-viewer-presets)を参照してください。

   これで、画像バナーをアップロードできるようになりました。

## 画像バナーのアップロード  {#uploading-an-image-banner}

使用する画像を既にアップロードしている場合は、次の手順（[画像バナーへのホットスポットの追加](#adding-hotspots-to-an-image-banner)）に進んでください。

**画像バナーをアップロードするには：**

1. インタラクティブにする画像バナーをアップロードします。

   [アセットのアップロード](/help/assets/manage-digital-assets.md#uploading-assets)を参照してください。

   これで、画像バナーにホットスポットを追加する準備が整いました。この後のタスクを参照してください。

## 画像バナーへのホットスポットの追加  {#adding-hotspots-to-an-image-banner}

ホットスポット管理ページのエディターを使用して、画像バナーにホットスポットを追加できます。

ホットスポットを追加する際に、それらをクイック表示ポップアップディスプレイ、ハイパーリンクまたはエクスペリエンスフラグメントとして定義できます。

[エクスペリエンスフラグメント](/help/sites-cloud/authoring/fundamentals/experience-fragments.md)を参照してください。

>[!NOTE]
>
>インタラクティブ画像のソーシャルメディア共有ツールは、エクスペリエンスフラグメントにビューアを埋め込む場合はサポートされません。 代わりに、ソーシャルメディア共有ツールを備えていないビューアプリセットを使用または作成します。 このようなビューアプリセットを使用すると、ビューアをエクスペリエンスフラグメントに正常に埋め込むことができます。

ページの右上隅にある「取り消し」および「やり直し」オプションは、現在の作成／編集セッションの間で有効です。

インタラクティブ画像の作成が完了したら、プレビューを使用して、ユーザーに対してインタラクティブ画像がどのように見えるかを確認できます。

[（オプション）インタラクティブ画像のプレビュー](#optional-previewing-interactive-images)を参照してください。

>[!NOTE]
>
>インタラクティブ画像またはカルーセルバナー内の画像にホットスポットを追加すると、ホットスポット情報は同じメタデータの場所に保存されます。 この場所は、インタラクティブ画像かカルーセルバナーかに関係なく、画像の場所に対する相対位置になります。 つまり、どちらのビューアでも、同じ画像と、定義済みのホットスポットデータを簡単に再利用できます。
ただし、カルーセルバナーでは、画像上の画像マップ（ホットスポットを含むことができる）がサポートされることに注意してください。インタラクティブ画像ではサポートされません。同じ画像を使用するインタラクティブ画像またはカルーセルバナーを作成する場合は、この点に注意してください。 代わりに、同じ画像の個別のコピーを使用して、インタラクティブ画像とカルーセルバナーを作成できます。
[カルーセルバナー](/help/assets/dynamic-media/carousel-banners.md)も参照してください。

>[!NOTE]
ホットスポットを含むインタラクティブ画像を編集しているときに、画像を切り取ると、ホットスポットは削除されます。

**画像バナーにホットスポットを追加するには：**

1. Assets ビューで、インタラクティブにする画像バナーに移動します。
1. 次のいずれかの操作をおこないます。

   * 画像の上にマウスポインターを置き、**[!UICONTROL 選択]**（チェックマークアイコン）をタップします。ツールバーの「**[!UICONTROL 編集]**」をタップします。

   * 画像の上にマウスポインターを置き、**[!UICONTROL その他のアクション]**（3 つのドットのアイコン）／**[!UICONTROL 編集]**&#x200B;をタップします。

   * 詳細表示ページで画像を開くには、画像をタップします。 ツールバーで、**[!UICONTROL 編集]**&#x200B;をタップします。

1. ページの左上隅にある「**[!UICONTROL ホットスポットを追加]**」（指先アイコン）をタップして、ホットスポット管理ページを開きます。
1. ページの左上隅にある「**[!UICONTROL ホットスポット]**」をタップします。

   1. ホットスポット管理ページの左上隅にある「**[!UICONTROL ホットスポット]**」をタップします。
   1. 画像上で、ホットスポットを表示する場所をタップします。必要に応じて、ホットスポットをドラッグして場所を調整します。または、キーボードの矢印キーを使用して、選択したホットスポットの位置を制御します。
   1. 必要に応じて、手順aとbを繰り返し追加て、より多くのホットスポットを作成します。
   1. （オプション）ホットスポットを削除するには、画像上でホットスポットを選択し、「**[!UICONTROL ホットスポット]**」見出しの下の「**[!UICONTROL 削除]**（ごみ箱アイコン）」をタップします。

1. 「名前」テキストフィールドにホットスポットの名前を入力します。この名前は、選択したホットスポットドロップダウンリストにも表示されます。
1. 次のいずれかの操作をおこないます。

   * **[!UICONTROL クイック表示]**&#x200B;をタップします。

      * AEM Sites または AEM eCommerce のユーザーである場合は、製品ピッカーアイコン（虫眼鏡）をタップまたはクリックして、製品を選択ページを開きます。使用する製品をタップし、ページの右上隅にある「**選択**」をタップします。 「ホットスポット管理」ページに戻ります。
      * Experience Managerサイトまたはeコマースのお客様では&#x200B;*ない*&#x200B;場合

         * [ホットスポット変数の識別](#optional-identifying-hotspot-variables)を参照してください。これらの変数を定義する必要があります。
         * 次に、SKU 値を手動で入力します。「SKU値」テキストフィールドに、製品のSKUを入力します。 入力したSKU値によって、クイック表示テンプレートの可変部分が自動的に設定されます。 タップされたホットスポットを特定のSKUのクイック表示に関連付けることができます。
         * （オプション）クイック表示内に、製品をさらに識別するために使用される変数が他にある場合は、**[!UICONTROL 追加汎用変数]**&#x200B;をタップします。 テキストフィールドで、追加の変数を指定します。 例えば、追加の変数として `category=Mens` などと指定します。
   * 「**[!UICONTROL ハイパーリンク]**」をタップします。

      * Experience Managerサイトをご利用の場合は、サイトの選択アイコン（フォルダー）をタップします。 URLに移動します。 インタラクティブコンテンツに相対URLを持つリンク(特にExperience Managerサイトページへのリンク)がある場合、URLベースのリンク方法は使用できません。
      * スタンドアロンユーザーである場合は、「HREF」テキストフィールドに、リンクされる Web ページへの完全な URL パスを指定します。

   このリンクを新しいブラウザータブで開く（推奨のデフォルト）か同じタブで開くかを指定してください。

   詳しくは、[セレクターの操作](/help/assets/dynamic-media/working-with-selectors.md)を参照してください。

   * 「**[!UICONTROL エクスペリエンスフラグメント]**」をタップします。

      * AEM Sites のユーザーである場合は、検索アイコン（虫眼鏡）をタップまたはクリックしてエクスペリエンスフラグメントページを開きます。使用するエクスペリエンスフラグメントをタップします。 次に、ページの右上隅にある「**[!UICONTROL 選択]**」をタップします。 「ホットスポット管理」ページに戻ります。
[エクスペリエンスフラグメント](/help/sites-cloud/authoring/fundamentals/experience-fragments.md)を参照してください。

      * エクスペリエンスフラグメントをバナーに表示する場合の幅と高さを指定します。

         >[!NOTE]
         インタラクティブ画像のソーシャルメディア共有ツールは、エクスペリエンスフラグメントにビューアを埋め込む場合はサポートされません。 代わりに、ソーシャルメディア共有ツールを備えていないビューアプリセットを使用または作成します。 このようなビューアプリセットを使用すると、ビューアをエクスペリエンスフラグメントに正常に埋め込むことができます。



1. 「**[!UICONTROL 保存]**」をタップして作業内容を保存し、参照ページに戻ります。
1. インタラクティブ画像を公開します。公開すると、クラウドにバナーが配信され、埋め込みコードが生成されてサードパーティのWebサイトと統合できます。

   [アセットの公開](/help/assets/manage-digital-assets.md#publish-assets)を参照してください。

   ホットスポットを追加してインタラクティブ画像を公開したら、次に既存の Web サイトにその画像を追加できます。

   [インタラクティブ画像の Web サイトへの統合](#integrating-an-interactive-image-with-your-website)を参照してください。

   >[!NOTE]
   ホットスポットを含むインタラクティブ画像を編集しているときに、画像を切り取ると、ホットスポットは削除されます。

### （オプション）インタラクティブ画像のプレビュー  {#optional-previewing-interactive-images}

プレビューを使用すると、インタラクティブ画像がユーザーに対してどのように表示されるかを確認できます。 また、プレビューでは、画像のホットスポットをテストして、期待どおりの動作をするかを確認することもできます。

インタラクティブ画像の設定が完了したら、この画像を公開できます。[Web ページへのビデオビューアまたは画像ビューアの埋め込み](/help/assets/dynamic-media/embed-code.md)を参照してください。[Web アプリケーションへの URL のリンク](/help/assets/dynamic-media/linking-urls-to-yourwebapplication.md)を参照してください。インタラクティブコンテンツに相対 URL のリンク（特に AEM Sites ページへのリンク）がある場合、URL ベースのリンク方法は使用できません。[ページへの Dynamic Media アセットの追加](/help/assets/dynamic-media/adding-dynamic-media-assets-to-pages.md)を参照してください。

**インタラクティブ画像をプレビューするには：**

1. Assets ビューで、作成した既存のインタラクティブ画像の場所に移動し、タップしてプレビューで表示します。
1. プレビューページの左上隅付近にある「コンテンツ」ドロップダウンリストで「**[!UICONTROL ビューア]**」をタップします。
1. ビューアリストで「**[!UICONTROL Shoppable_Banner]**」または作成したインタラクティブ画像ビューアプリセットの名前をタップします。
1. ホットスポットの関連するアクションをテストするには、画像上のホットスポットをタップします。

## インタラクティブ画像アセットの公開 {#publishing-interactive-image-assets}

インタラクティブ画像アセットの公開方法について詳しくは、[アセットの公開](/help/assets/dynamic-media/publishing-dynamicmedia-assets.md)を参照してください。

## インタラクティブ画像の Web サイトへの統合 {#integrating-an-interactive-image-with-your-website}

バナー画像をアップロードし、ホットスポットを追加して、インタラクティブ画像を公開したら、それをWebサイトページに追加する準備が整います。

AEM Sites のユーザーである場合は、インタラクティブメディアコンポーネントをページにドラッグすることによりインタラクティブ画像を追加できます。[ページへの Dynamic Media アセットの追加](/help/assets/dynamic-media/adding-dynamic-media-assets-to-pages.md)を参照してください。

スタンドアロン AEM Assets のユーザーである場合は、この節で説明するようにインタラクティブ画像を手動で Web サイトに追加できます。

1. 公開済みのインタラクティブ画像の埋め込みコードをコピーします。[Web ページへのビデオビューアまたは画像ビューアの埋め込み](/help/assets/dynamic-media/embed-code.md)を参照してください。

1. コピーした埋め込みコードを、Web ページ内の必要な場所に追加します。コピーされた埋め込みコードはレスポンシブ環境用に設定され、割り当てられた領域に合わせて自動的に調整されます。

**例**

[デモのWebサイトを例として使用](https://marketing.adobe.com/resources/help/en_US/dm/shoppable-banner/we-fashion/landing-0.html)すると、3人の個人の写真は静的な`IMG`タグです。

```xml
<img class="img-responsive" width="100%" title="Hero Image 2" alt="Hero Image 2" src="images/shoppable-banner.jpg">
```

統合は、`IMG` タグを削除して AEM Assets からコピーした埋め込みコードに置き換えるだけで簡単にできます。結果[は、3つの円のホットスポット](https://marketing.adobe.com/resources/help/en_US/dm/shoppable-banner/we-fashion/landing-1.html)を持つ買い物可能なインタラクティブ画像をページに表示します。

>[!NOTE]
この時点で、デモWebサイトの買い物可能なインタラクティブ画像のホットスポットは、表示のみを目的としています。まだ既存のクイック表示と統合されていません。

レスポンシブ環境用のショップ可能なインタラクティブ画像に「切り抜き」を適用するには、パスにインタラクティブ画像設定属性`ZoomView.iscommand`を含めます。 この場合、`ZoomView`コンポーネントが呼び出され、`iscommand`は適用する「切り抜き」画像サービングコマンドです。

[ZoomView.iscommand](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/viewers-for-aem-assets-only/interactive-images/command-reference-configuration-attributes-interactive-images/r-html5-aem-interactive-image-config-attrib-zoomview-iscommand.html?lang=ja) 設定属性を参照してください。

[crop](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/http-protocol-reference/command-reference/r-crop.html?lang=ja) 画像サービングコマンドを参照してください。

これで、インタラクティブ画像をWebサイト上の既存のクイック表示と統合する準備が整いました。

## インタラクティブ表示と既存のクイック画像の統合{#integrating-an-interactive-image-with-an-existing-quickview}

>[!NOTE]
このタスクはスタンドアロン AEM Assets のユーザーのみに適用されます。

このプロセスの最後の手順は、インタラクティブ表示をWebサイト上の既存のクイックイメージ実装と統合することです。 すべてのケースで機能する統合のソリューションはありません。クイック表示の実装はすべて一意で、特定のアプローチが必要です。 したがって、フロントエンドのIT担当者の支援が必要な場合に役立ちます。

既存のクイック表示の実装は、通常、Webページ上で発生する相互に関連するアクションのチェーンを次の順序で表します。

1. ユーザーは、Web サイトのユーザーインターフェイス内で、特定の要素を起動します。
1. フロントエンドコードは、手順1でトリガーされた表示インターフェイス要素に基づいて、クイックユーザーURLを取得します。
1. フロントエンドコードは、手順 2 で取得した URL を使用して Ajax リクエストを送信します。
1. バックエンドロジックは、対応するクイック表示データまたはコンテンツをフロントエンドコードに返します。
1. フロントエンドコードは、クイック表示のデータまたはコンテンツを読み込みます。
1. 必要に応じて、フロントエンドコードは、読み込まれたクイック表示データをHTML表現に変換します。
1. フロントエンドコードは、モーダルダイアログボックスまたはパネルを表示し、エンドユーザー向けに、画面上に HTML コンテンツをレンダリングします。

これらの呼び出しは、Webページロジックによって任意の手順から呼び出される、独立したパブリックAPI呼び出しを表すとは限りません。 むしろ、次の手順がすべて前の手順の最終フェーズ（コールバック）に潜むような連鎖的な呼び出しになっています。

ショップ可能なインタラクティブ画像がステップ1を置き換え、ステップ2の一部を置き換えると、ユーザはショップ可能な画像内のホットスポットをタップします。 このようなユーザ操作はビューアで処理されます。 ビューアは、AEM Assets に以前に追加されたすべてのホットスポットデータを含む Web ページに、イベントを返します。

そのようなイベントハンドラーでは、フロントエンドコードは次の処理を実行します。

* ショッパブルインタラクティブ画像から送出されるイベントをリッスンします。
* ホットスポットデータに基づいてクイック表示URLを作成します。
* クイック表示をバックエンドから読み込み、表示用に画面にレンダリングするプロセスをトリガーします。

Experience Managerアセットから返される埋め込みコードには、次のコードスニペットに示すように、使いやすいイベントハンドラーがコメントアウトされています。

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

クイック表示URLを作成するプロセスは、前述のホットスポット変数を識別するプロセスとは逆です。

[ホットスポットの変数の識別](#optional-identifying-hotspot-variables)を参照してください。

前述のクイック表示URLの例を使用して、次の例では、それぞれの場合にクイック表示URLがどのように構成されているかを確認できます。

<table>
 <tbody>
  <tr>
   <td><p>単一の SKU（クエリ文字列内）</p> </td>
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
   <td><p>SKU とカテゴリ ID（クエリ文字列内）</p> </td>
   <td><code class="code">s7interactiveimageviewer.setHandlers({
      "quickViewActivate": function(inData) {
      var quickViewUrl = "https://server/quickView/product/?category=" + inData.categoryId + "&amp;amp;prodId=" + inData.sku;
      },
      });</code></td>
  </tr>
 </tbody>
</table>

クイック表示URLをトリガーし、クイック表示パネルをアクティブにする最後の手順では、お客様のビジネスのフロントエンドIT担当者の支援が必要です。 ユーザーは、クイック表示の導入を正確にトリガーする方法を最もよく理解し、使いやすいクイック表示URLを適切な手順から取得できます。

これらの手順がデモWebサイトにどのように適用されるかを見ると、買い物かごのインタラクティブ表示をクイック画像コードと完全に統合できます。以前は、クイック表示URLの構造は次のように識別されていました。

```xml
/datafeed/$categoryId$-$SKU$.json
```

このURLを`quickViewActivate`ハンドラー内に再構築するには、`categoryId`フィールドと`SKU`フィールドを使用します。 これらのフィールドは、ビューアのコードによってハンドラーに渡される`inData`オブジェクトで使用できます。

```xml
var sku=inData.sku;
var categoryId=inData.categoryId;
var quickViewUrl = "datafeed/" + categoryId + "-" + sku + ".json";
```

デモのWebサイトは、単純な`loadQuickView()`関数呼び出しを使用してクイック表示ダイアログボックスをトリガしています。 この関数は、1つの引数(クイック表示データURL)しか取りません。 そのため、買い物かごの対話画像を統合する最後の手順は、次のコードを`quickViewActivate`ハンドラに追加することです。

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

[完全に統合されたインタラクティブ画像を含んだ最終的なデモ Web サイト](https://marketing.adobe.com/resources/help/en_US/dm/shoppable-banner/we-fashion/landing-3.html)です。

## クイック表示を使用したカスタムポップアップの作成{#using-quickviews-to-create-custom-pop-ups}

「[クイック表示を使用したカスタムポップアップウィンドウの作成](/help/assets/dynamic-media/custom-pop-ups.md)」を参照してください。
