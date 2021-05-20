---
title: インタラクティブ画像
description: Dynamic Media でのインタラクティブ画像の使用方法について説明します。
feature: インタラクティブ画像
role: Business Practitioner
exl-id: 89eef5e6-d508-4f33-b54e-24d4df49f8c3
source-git-commit: d3ee23917eba4a2e4ae1f2bd44f5476d2ff7dce1
workflow-type: tm+mt
source-wordcount: '4263'
ht-degree: 40%

---

# インタラクティブ画像 {#interactive-images}

「ショッパブル」ホットスポットを画像にドラッグ&amp;ドロップすることで、静的画像をリッチで魅力的なエクスペリエンスを簡単に作成できます。ショッパブルホットスポットは、製品やサービスに関する追加情報と、直接販売時点管理機能の「買い物かごに追加」または「購入」機能を組み合わせます。 顧客は、製品やサービスに直接リンクするこれらのホットスポットをタップしたり、買い物かごに追加したり、Webページにリンクしたりできます。 このような直接的なエクスペリエンスにより、Webサイトでの顧客エンゲージメントやコンバージョンが向上します。

次に、クイックビューポップアップウィンドウを含むショッパブルバナーを示します。 モデル上の円または「ホットスポット」をタップして、クイックビューをアクティブにします。

![chlimage_1-152](assets/chlimage_1-368.png)

上の図に示す Web ページの[実際のインタラクティブ画像](https://marketing.adobe.com/resources/help/en_US/dm/shoppable-banner/we-fashion-QVzoom/index2-shoppable.html)を参照してください。

## インタラクティブ画像バナーの作成方法 {#watch-how-interactive-image-banners-are-created}

[インタラクティブ画像バナーの作成方法](https://s7d5.scene7.com/s7viewers/html5/VideoViewer.html?videoserverurl=https://s7d5.scene7.com/is/content/&amp;emailurl=https://s7d5.scene7.com/s7/emailFriend&amp;serverUrl=https://s7d5.scene7.com/is/image/&amp;config=Scene7SharedAssets/Universal_HTML5_Video_social&amp;contenturl=https://s7d5.scene7.com/skins/&amp;asset=S7tutorials/InteractiveCarouselBanner)（10分33秒）に関する説明を視聴します。 また、インタラクティブ画像バナーをプレビュー、編集、配信する方法についても説明します。

## クイックスタート：インタラクティブ画像 {#quick-start-interactive-images}

次のワークフローの手順説明は、Adobe Experience Manager Assetsのインタラクティブ画像をすばやく使い始めるのに役立ちます。

一部のクイックスタートタスク内には「**例**」という見出しがあります。これには、[まだインタラクティブ画像が追加されていないサンプル Web ページ](https://marketing.adobe.com/resources/help/en_US/dm/shoppable-banner/we-fashion/landing-0.html)に基づいた簡単なチュートリアルが含まれています。



このチュートリアルでは、Web サイトにインタラクティブ画像を統合する手順が説明されています。

インタラクティブ画像の手順：

1. **（オプション）ホットスポットの変数の識別**。Adobe Experience Manager AssetsとDynamic Mediaをスタンドアロンで使用する場合は、既存のクイックビュー実装で使用する動的変数を特定します。 これにより、インタラクティブ画像の作成時にホットスポットデータを入力できるようになります。 [（オプション）ホットスポットの変数の識別](#optional-identifying-hotspot-variables)を参照してください。ただし、Experience Managerサイト、Experience Managereコマース、またはその両方を使用する場合、この手順は不要です。

1. **（オプション）インタラクティブ画像ビューアプリセットの作成**&#x200B;を参照してください。ホットスポットを表すために使用するグラフィック画像をカスタマイズします。独自のインタラクティブ画像ビューアプリセットの作成は、標準提供のインタラクティブ画像ビューアプリセット `Shoppable_Banner` を使用する場合には必要ありません。[（オプション）インタラクティブ画像ビューアプリセットの作成](/help/assets/dynamic-media/managing-viewer-presets.md#creating-a-new-viewer-preset)を参照してください。

1. **画像バナーのアップロード**&#x200B;を参照してください。インタラクティブにする画像バナーをアップロードします。画像バナ [ーのアップロード](#uploading-an-image-banner)を参照してください。

1. **画像バナーへのホットスポットの追加**&#x200B;を参照してください。画像バナーに1つ以上のホットスポットを追加します。各アクションに、ハイパーリンク、クイックビュー、エクスペリエンスフラグメントなどのアクションを関連付けます。 ホットスポットを追加した後は、インタラクティブ画像を公開するとタスクが終了します。[画像バナーへのホットスポットの追加](#adding-hotspots-to-an-image-banner)を参照してください。[（オプション）インタラクティブ画像のプレビュー](#optional-previewing-interactive-images)を参照してください。必要に応じて、ショッパブルバナーの表示を確認して、インタラクティビティをテストすることができます。インタラクティブ画像アセットの公開方法について詳しくは、[アセットの公開](/help/assets/dynamic-media/publishing-dynamicmedia-assets.md)を参照してください。

1. **WebサイトまたはWebサイトへのインタラクティブ画像の追加(Experience Manager**)サイト、eコマースまたはその両方を使用する場合は、Webページにインタラクティブ画像をExperience Managerで直接追加できます。 インタラクティブメディアコンポーネントをページにドラッグします。 [ページへの Dynamic Media アセットの追加](/help/assets/dynamic-media/adding-dynamic-media-assets-to-pages.md)を参照してください。Adobe Experience Manager AssetsとDynamic Mediaをスタンドアロンで使用している場合は、Webサイト上で埋め込みコードをコピーします。 次に、既存のクイックビューに統合します。 [インタラクティブ画像の Web サイトへの統合](#integrating-an-interactive-image-with-your-website)を参照してください。サードパーティのWCM(Web Content Manager)を使用する場合は、新しいインタラクティブビデオを、Webサイトで使用されている既存のクイックビューに統合します。 [インタラクティブ画像の既存のクイックビューへの統合](#integrating-an-interactive-image-with-an-existing-quickview)を参照してください。

## （オプション）ホットスポットの変数の識別 {#optional-identifying-hotspot-variables}

>[!NOTE]
>
>このタスクが必要になるのは次に該当する場合のみです。
>
>* クイックビューをトリガーして、画像にインタラクティビティを追加する。
>* Experience Managerの実装では、eコマース統合フレームワークを使用して、eコマースソリューションから製品データをExperience Managerに取り込みません。** このようなソリューションには、IBM® WebSphere® Commerce、Elastic Path、SAP Hybris、Intershopなどがあります。

>
>
eコマースを使用するExperience Managerの実装の場合は、このタスクをスキップして次のタスクに進むことができます。

まず、既存のクイックビュー実装で使用されている動的変数を識別します。これにより、ホットスポットデータを入力してインタラクティブ画像を作成できます。

Experience Managerアセットのバナー画像にホットスポットを追加する場合は、SKU(Stock Keeping Unit)を割り当てます。 SKUは、提供する個々の製品またはサービスの一意の識別子です。 さらに、各ホットスポットにオプションの変数を追加します。 このようなホットスポットの変数は、後でホットスポットとクイックビューコンテンツを照合するために使用されます。

重要なのは、ホットスポットデータに関連付けられる変数の数とタイプを正しく識別することです。バナー画像に追加するそれぞれのホットスポットに、既存のバックエンドシステム内で製品を一意に識別するための十分な情報がある必要があります。

ホットスポットデータに使用する一連の変数を識別するには、様々な方法があります。

既存のクイックビュー実装を担当するIT担当者に相談するだけで十分な場合もあります。 このようなユーザーは、システム内のクイックビューを識別するために必要な最小のデータセットを把握することができます。 ただし、フロントエンドコードの既存の動作を簡単に分析することもできます。

ほとんどのクイックビュー実装では、次のパラダイムを使用します。

* ユーザーはWebサイト上の特定のユーザーインターフェイス要素をアクティベートします。例えば、「クイックビュー」ボタンをクリックします。
* Webサイトは、必要に応じて、クイックビューのデータまたはコンテンツを読み込むためのAjaxリクエストをバックエンドに送信します。
* クイックビューのデータは、Webページでのレンダリングに備えて、コンテンツに変換されます。
* 最後に、フロントエンドコードによってそのコンテンツが画面上に視覚的にレンダリングされます。

次に、クイックビュー機能が実装されている既存のWebサイトの様々な領域にアクセスする方法を示します。 次に、クイックビューをトリガーし、Webページから送信されたクイックビューのデータまたはコンテンツを読み込むためのAjax URLを取得します。

通常、専門のデバッグツールを使用する必要はありません。最新の Web ブラウザーには、十分なタスクを実行できる Web インスペクターが備わっています。Web インスペクターが搭載されている Web ブラウザーの例を次に示します。

* Google Chrome で、ブラウザーから送信されるすべての HTTP リクエストを参照するには、F12 キーを押してデベロッパーツールパネルを開き、「Network」タブをクリックします。Mac の場合、Command + Option + I キーを押してデベロッパーツールパネルを開き、「Network」タブをクリックします。

* Firefoxでは、F12キーを押してFirebugプラグインを有効にし、「Net」タブを使用します。 または、組み込みのインスペクターツールとその「ネットワーク」タブを使用できます。
Mac の場合、Command + Option + I キーを押してデベロッパーツールパネルを開き、「Inspector」タブをクリックします。

ブラウザーでネットワーク監視が有効になっている場合は、ページのクイックビューをトリガーします。

次に、ネットワークログでクイックビューのAjax URLを探し、記録したURLをコピーして、後で分析できるようにします。 通常、クイックビューをトリガーすると、サーバーに送信される多数のリクエストがあります。 通常、クイックビューのAjax URLはリストの最初のURLの1つです。 この URL には複雑なクエリ文字列部分またはパスが含まれ、その応答の MIME タイプは `text/html`、`text/xml`、`text/javascript` のいずれかになります。

このプロセスの間、様々な製品カテゴリや製品タイプを使用して、Webサイトの様々な領域にアクセスすることが重要です。 なぜなら、クイックビューURLには、特定のWebサイトカテゴリに共通する部分を含めることができるからです。 ただし、Webサイトの別の領域を訪問した場合にのみ変更されます。

最も簡単なケースでは、クイックビューURLで変化する唯一の部分が製品SKUです。この場合、SKU値は、バナー画像にホットスポットを追加するために必要な唯一のデータです。

ただし、複雑なケースでは、クイックビューURLにSKU以外に様々な要素が含まれます。 例えば、様々な要素には、カテゴリID、カラーコード、サイズコードを含めることができます。 その場合、各要素は、Experience Managerアセットのショッパブルインタラクティブ画像機能のホットスポットデータ定義内の個別の変数になります。

次のクイックビューURLの例と、その結果として生成されるホットスポット変数について考えてみましょう。

<table>
  <tbody>
  <tr>
    <td><p>単一の SKU（クエリ文字列内）</p> </td>
    <td><p>記録されたクイックビューのURLは次のとおりです。</p>
    <ul>
      <li><p><code>https://server/json?productId=866558&amp;source=100</code></p> </li>
      <li><p><code>https://server/json?productId=1196184&amp;source=100</code></p> </li>
      <li><p><code>https://server/json?productId=1081492&amp;source=100</code></p> </li>
      <li><p><code>https://server/json?productId=1898294&amp;source=100</code></p> </li>
    </ul> <p>この URL で変化する唯一の部分は productId= というクエリ文字列パラメーターの値であり、これが SKU 値であることは明白です。したがって、ホットスポットでは、<strong><code>866558</code></strong>、<strong><code>1196184</code></strong>、<strong><code>1081492</code></strong>、<strong><code>1898294</code></strong>などの値が設定されたSKUフィールドのみが必要になります。</p> </td>
  </tr>
  <tr>
    <td><p>単一の SKU（URL パス内）</p> </td>
    <td><p>記録されたクイックビューのURLは次のとおりです。</p>
    <ul>
      <li><p><code>https://server/product/6422350843</code></p> </li>
      <li><p><code>https://server/product/1607745002</code></p> </li>
      <li><p><code>https://server/product/0086724882</code></p> </li>
    </ul> <p>パスの最後の要素が変化する部分であり、これがホットスポットの SKU 値（<strong><code>6422350843</code></strong>、<strong><code>1607745002</code></strong>、<strong><code>0086724882</code></strong>）になります。</p> </td>
  </tr>
  <tr>
    <td><p>SKU とカテゴリ ID（クエリ文字列内）</p> </td>
    <td><p>記録されたクイックビューのURLは次のとおりです。</p>
    <ul>
      <li><p><code>https://server/quickView/product/?category=1100004&amp;prodId=305466</code></p> </li>
      <li><p><code>https://server/quickView/product/?category=1100004&amp;prodId=310181</code></p> </li>
      <li><p><code>https://server/quickView/product/?category=1740148&amp;prodId=308706</code></p> </li>
    </ul> <p>この場合、URL には変化する部分が 2 つあります。SKU が <code>prodId</code> パラメーターに、カテゴリ ID<code></code> が <code>category=</code> パラメーターに格納されています。</p> <p>そのため、ホットスポット定義はペアになります。つまり、SKU値と、<code>categoryId</code>という追加の変数です。 結果のペアは次のようになります。</p>
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

デモWebページには複数の製品サムネールがあり、それぞれに「詳細を表示」というラベルの付いたクイックビューボタンがあります。Webブラウザーのデバッグツールを有効にしたまま、各ボタンをクリックし、記録されたクイックビューのURLをメモします。ページで使用可能な4つの製品クイックビューをすべてアクティブ化すると、バックエンドに対して次のリストのクイックビューリクエストが実行されます。

* `/datafeed/Men-Windbreaker.json`
* `/datafeed/Men-SimpleHenley.json`
* `/datafeed/Men-CamoPullover.json`
* `/datafeed/Women-QuiltedDownJacket.json`

サーバー呼び出しを見ると、製品固有の情報がリクエストパスにのみ存在することがわかります。 また、クエリ文字列がまったく使用されていないこと、2 つの異なるタイプのデータが含まれることもわかります。

* 最初のタイプは Men または Women です。これは「製品カテゴリ」と呼ばれます。
* 2つ目のタイプは製品名（CamoPulloverなど）で、これは製品SKUである可能性が高くなります。

この情報を考えると、クイックビューURL全体は次のパターンになります。

`/datafeed/$categoryId$-$SKU$.json`

このような分析に基づいて、ホットスポットに対して `categoryId` と `SKU` を使用することになります。

これで、Experience Managerアセットのショッパブルインタラクティブ画像機能を使用して、画像バナーをアップロードし、ホットスポットを追加する準備が整いました。

## （オプション）インタラクティブ画像ビューアプリセットの作成{#optional-creating-an-interactive-image-viewer-preset}

Experience Managerアセットに付属する、デフォルトの標準提供インタラクティブ画像ビューアプリセット(`Shoppable_Banner`)を使用するように選択できます。 または、インタラクティブ画像で使用するために独自のカスタムビューアプリセットを作成できます。

カスタムインタラクティブ画像ビューアプリセットを作成する場合は、画像バナーのホットスポットの外観を決定できます。ビューアプリセットの作成中に、事前定義済みの画像ギャラリーからホットスポットのグラフィックを選択して使用できます。

ビューアプリセットを保存すると、Experience Managerアセットのビューアプリセットリストページで自動的にアクティベートされます（オンになります）。 つまり、そのビューアプリセットは、インタラクティブメディアコンポーネントで、アセットを表示するときに常に表示されます。ただし、*このビューアプリセットを含むインタラクティブバナーを*&#x200B;配信するには、*公開*&#x200B;するビューアプリセットも公開します。 このルールは、カスタムまたは標準提供のビューアプリセットの場合に当てはまります。

**インタラクティブ画像ビューアプリセットを作成するには：**

1. 左側のパネルで、**[!UICONTROL ツール／アセット／ビューアプリセット]**&#x200B;をタップします。
1. ページの右上隅にある「**[!UICONTROL 作成]**」をタップします。
1. 新規ビューアプリセットダイアログボックスで、インタラクティブバナービューアプリセットを表す名前を入力します。

   保存すると、このタイトルがビューアプリセットリストページに表示されます。

1. 「リッチメディアタイプ」プルダウンメニューで、「**[!UICONTROL インタラクティブ画像]**」を選択します。
1. 「**[!UICONTROL 作成]**」をタップします。
1. ビューアプリセットを編集ページで、「**[!UICONTROL 外観]**」タブをタップします。
1. 次のいずれかの操作をおこないます。

   * 画像上で使用する独自のホットスポット画像をアップロードするには、アセットピッカーアイコンをタップします。コンテンツを選択ページで、使用するホットスポット画像に移動し、その画像を選択します。 右上隅のチェックマークアイコンをタップします。
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

ホットスポットを追加する際に、クイックビューポップアップディスプレイ、ハイパーリンク、エクスペリエンスフラグメントのいずれかとして定義できます。

[エクスペリエンスフラグメント](/help/sites-cloud/authoring/fundamentals/experience-fragments.md)を参照してください。

>[!NOTE]
>
>インタラクティブ画像のソーシャルメディア共有ツールは、エクスペリエンスフラグメントにビューアを埋め込む場合はサポートされません。 代わりに、ソーシャルメディア共有ツールを持たないビューアプリセットを使用または作成します。 このようなビューアプリセットを使用すると、ビューアをエクスペリエンスフラグメントに正常に埋め込むことができます。

ページの右上隅にある「取り消し」および「やり直し」オプションは、現在の作成／編集セッションの間で有効です。

インタラクティブ画像の作成が完了したら、プレビューを使用して、インタラクティブ画像が顧客にどのように表示されるかを確認できます。

[（オプション）インタラクティブ画像のプレビュー](#optional-previewing-interactive-images)を参照してください。

>[!NOTE]
>
>インタラクティブ画像またはカルーセルバナーの画像にホットスポットを追加すると、ホットスポット情報は同じメタデータの場所に保存されます。 この場所は、インタラクティブ画像かカルーセルバナーかに関係なく、画像の場所に対する相対位置です。 つまり、どちらのビューアでも、同じ画像を定義済みのホットスポットデータと共に簡単に再利用できます。
ただし、カルーセルバナーでは、画像上の画像マップ（ホットスポットを含むことができる）がサポートされることに注意してください。インタラクティブ画像ではサポートされません。同じ画像を使用するインタラクティブ画像またはカルーセルバナーを作成する場合は、この点に注意してください。 同じ画像のコピーを別々に使用して、インタラクティブ画像とカルーセルバナーを作成できます。
[カルーセルバナー](/help/assets/dynamic-media/carousel-banners.md)も参照してください。

>[!NOTE]
ホットスポットを含むインタラクティブ画像を編集しているときに、画像を切り取ると、ホットスポットは削除されます。

**画像バナーにホットスポットを追加するには：**

1. Assets ビューで、インタラクティブにする画像バナーに移動します。
1. 次のいずれかの操作をおこないます。

   * 画像の上にマウスポインターを置き、**[!UICONTROL 選択]**（チェックマークアイコン）をタップします。ツールバーの「**[!UICONTROL 編集]**」をタップします。

   * 画像の上にマウスポインターを置き、**[!UICONTROL その他のアクション]**（3 つのドットのアイコン）／**[!UICONTROL 編集]**&#x200B;をタップします。

   * 詳細ビューページで画像を開くには、画像をタップします。 ツールバーの「**[!UICONTROL 編集]**」をタップします。

1. ページの左上隅にある「**[!UICONTROL ホットスポットを追加]**」（指先アイコン）をタップして、ホットスポット管理ページを開きます。
1. ページの左上隅にある「**[!UICONTROL ホットスポット]**」をタップします。

   1. ホットスポット管理ページの左上隅にある「**[!UICONTROL ホットスポット]**」をタップします。
   1. 画像上で、ホットスポットを表示する場所をタップします。必要に応じて、ホットスポットをドラッグして場所を調整します。または、キーボードの矢印キーを使用して、選択したホットスポットの位置を制御します。
   1. 必要に応じて、手順aおよびbを繰り返して、さらにホットスポットを追加します。
   1. （オプション）ホットスポットを削除するには、画像上でそのホットスポットを選択し、「**[!UICONTROL ホットスポット]**」見出しの下にある「**[!UICONTROL 削除]**」（ごみ箱アイコン）をタップします。

1. 「名前」テキストフィールドにホットスポットの名前を入力します。この名前は、選択したホットスポットドロップダウンリストにも表示されます。
1. 次のいずれかの操作をおこないます。

   * **[!UICONTROL クイックビュー]**&#x200B;をタップします。

      * Experience Managerサイトまたはeコマースのユーザーである場合は、製品ピッカーアイコン（虫眼鏡）をタップまたはクリックして、製品を選択ページを開きます。 使用する製品をタップし、ページの右上隅にある「**選択**」をタップします。 ホットスポット管理ページに戻ります。
      * Experience Managerサイトまたはeコマースの顧客で&#x200B;*ない*&#x200B;場合

         * [ホットスポットの変数の識別](#optional-identifying-hotspot-variables)を参照してください。これらの変数を定義する必要があります。
         * 次に、SKU 値を手動で入力します。「SKU値」テキストフィールドに、製品のSKUを入力します。 入力したSKU値によって、クイックビューテンプレートの変数部分が自動的に入力されます。 これにより、タップされたホットスポットを特定のSKUのクイックビューに関連付けることができます。
         * （オプション）クイックビュー内で製品をさらに識別するために使用される他の変数がある場合は、「**[!UICONTROL 汎用変数を追加]**」をタップします。 テキストフィールドで、追加の変数を指定します。 例えば、追加の変数として `category=Mens` などと指定します。
   * 「**[!UICONTROL ハイパーリンク]**」をタップします。

      * Sitesのユーザーである場合は、Experience Managerセレクターアイコン（フォルダー）をタップします。 URLに移動します。 インタラクティブコンテンツに相対URLのリンク(特にExperience Managerサイトページへのリンク)がある場合、URLベースのリンク方法は使用できません。
      * スタンドアロンユーザーである場合は、「HREF」テキストフィールドに、リンクされる Web ページへの完全な URL パスを指定します。

   このリンクを新しいブラウザータブで開く（推奨のデフォルト）か同じタブで開くかを指定してください。

   詳しくは、[セレクターの操作](/help/assets/dynamic-media/working-with-selectors.md)を参照してください。

   * 「**[!UICONTROL エクスペリエンスフラグメント]**」をタップします。

      * Sitesのユーザーである場合は、検索アイコン（虫眼鏡）をタップまたはクリックしてExperience Managerフラグメントページを開きます。 使用するエクスペリエンスフラグメントをタップします。 次に、ページの右上隅にある「**[!UICONTROL 選択]**」をタップします。 ホットスポット管理ページに戻ります。
[エクスペリエンスフラグメント](/help/sites-cloud/authoring/fundamentals/experience-fragments.md)を参照してください。

      * エクスペリエンスフラグメントをバナーに表示する際の幅と高さを指定します。

         >[!NOTE]
         インタラクティブ画像のソーシャルメディア共有ツールは、エクスペリエンスフラグメントにビューアを埋め込む場合はサポートされません。 代わりに、ソーシャルメディア共有ツールを持たないビューアプリセットを使用または作成します。 このようなビューアプリセットを使用すると、ビューアをエクスペリエンスフラグメントに正常に埋め込むことができます。



1. 「**[!UICONTROL 保存]**」をタップして作業内容を保存し、参照ページに戻ります。
1. インタラクティブ画像を公開します。公開すると、クラウドを通じてバナーが配信され、サードパーティのWebサイトと統合できる埋め込みコードも生成されます。

   [アセットの公開](/help/assets/manage-digital-assets.md#publish-assets)を参照してください。

   ホットスポットを追加してインタラクティブ画像を公開したら、次に既存の Web サイトにその画像を追加できます。

   [インタラクティブ画像の Web サイトへの統合](#integrating-an-interactive-image-with-your-website)を参照してください。

   >[!NOTE]
   ホットスポットを含むインタラクティブ画像を編集しているときに、画像を切り取ると、ホットスポットは削除されます。

### （オプション）インタラクティブ画像のプレビュー  {#optional-previewing-interactive-images}

プレビューを使用して、顧客に対してインタラクティブ画像がどのように表示されるかを確認できます。 また、プレビューを使用すると、画像のホットスポットをテストして、期待どおりに動作することを確認できます。

インタラクティブ画像の設定が完了したら、この画像を公開できます。[Web ページへのビデオビューアまたは画像ビューアの埋め込み](/help/assets/dynamic-media/embed-code.md)を参照してください。[Web アプリケーションへの URL のリンク](/help/assets/dynamic-media/linking-urls-to-yourwebapplication.md)を参照してください。インタラクティブコンテンツに相対URLのリンク(特にExperience Managerサイトページへのリンク)がある場合、URLベースのリンク方法は使用できません。
[ページへの Dynamic Media アセットの追加](/help/assets/dynamic-media/adding-dynamic-media-assets-to-pages.md)を参照してください。

**インタラクティブ画像をプレビューするには：**

1. Assets ビューで、作成した既存のインタラクティブ画像の場所に移動し、タップしてプレビューで表示します。
1. プレビューページの左上隅付近にある「コンテンツ」ドロップダウンリストで「**[!UICONTROL ビューア]**」をタップします。
1. ビューアリストで「**[!UICONTROL Shoppable_Banner]**」または作成したインタラクティブ画像ビューアプリセットの名前をタップします。
1. ホットスポットの関連アクションをテストするには、画像上のホットスポットをタップします。

## インタラクティブ画像アセットの公開 {#publishing-interactive-image-assets}

インタラクティブ画像アセットの公開方法について詳しくは、[アセットの公開](/help/assets/dynamic-media/publishing-dynamicmedia-assets.md)を参照してください。

## インタラクティブ画像の Web サイトへの統合 {#integrating-an-interactive-image-with-your-website}

バナー画像をアップロードし、ホットスポットを追加して、インタラクティブ画像を公開したら、次にWebサイトページにその画像を追加します。

Sitesのユーザーである場合は、Experience Managerメディアコンポーネントをページにドラッグして、インタラクティブ画像を追加できます。 [ページへの Dynamic Media アセットの追加](/help/assets/dynamic-media/adding-dynamic-media-assets-to-pages.md)を参照してください。

スタンドアロンのExperience ManagerAssetsのユーザーである場合は、この節で説明するようにインタラクティブ画像を手動でWebサイトに追加できます。

1. 公開済みのインタラクティブ画像の埋め込みコードをコピーします。[Web ページへのビデオビューアまたは画像ビューアの埋め込み](/help/assets/dynamic-media/embed-code.md)を参照してください。

1. コピーした埋め込みコードを、Web ページ内の必要な場所に追加します。コピーされた埋め込みコードはレスポンシブ環境用に設定され、割り当てられた領域に自動的に適応します。

**例**

[デモWebサイトを例](https://marketing.adobe.com/resources/help/en_US/dm/shoppable-banner/we-fashion/landing-0.html)として使用すると、3人の個人の写真が静的な`IMG`タグであることに注意してください。

```xml
<img class="img-responsive" width="100%" title="Hero Image 2" alt="Hero Image 2" src="images/shoppable-banner.jpg">
```

統合は、 `IMG`タグを削除して、Experience ManagerAssetsからコピーした埋め込みコードに置き換えるだけで簡単にできます。 結果[は、3つの円のホットスポット](https://marketing.adobe.com/resources/help/en_US/dm/shoppable-banner/we-fashion/landing-1.html)を含むページ上でショッパブルインタラクティブ画像を表示しています。

>[!NOTE]
この時点で、デモWebサイトのショッパブルインタラクティブ画像上のホットスポットは表示専用です。まだ既存のクイックビューと統合されていません。

レスポンシブ環境用のショッパブルインタラクティブ画像に「切り抜き」を適用するには、パスにインタラクティブ画像設定属性`ZoomView.iscommand`を含めます。 この場合、 `ZoomView`コンポーネントが呼び出され、 `iscommand`が適用する「crop」画像サービングコマンドです。

[ZoomView.iscommand](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/viewers-for-aem-assets-only/interactive-images/command-reference-configuration-attributes-interactive-images/r-html5-aem-interactive-image-config-attrib-zoomview-iscommand.html?lang=ja) 設定属性を参照してください。

[crop](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/http-protocol-reference/command-reference/r-crop.html?lang=ja) 画像サービングコマンドを参照してください。

これで、インタラクティブ画像をWebサイト上の既存のクイックビューに統合する準備が整いました。

## インタラクティブ画像の既存のクイックビューへの統合{#integrating-an-interactive-image-with-an-existing-quickview}

>[!NOTE]
このタスクは、スタンドアロンのExperience ManagerAssetsのユーザーの場合にのみ適用されます。

このプロセスの最後の手順は、インタラクティブ画像をWebサイト上の既存のクイックビュー実装に統合することです。 すべてのケースで機能する統合のソリューションはありません。すべてのクイックビュー実装は固有で、具体的なアプローチが必要です。 そのため、フロントエンドIT担当者の支援を受けることが役立ちます。

既存のクイックビュー実装は通常、Webページ上で次の順序で発生する、相互に関連するアクションの連鎖を表します。

1. ユーザーは、Web サイトのユーザーインターフェイス内で、特定の要素を起動します。
1. フロントエンドコードは、手順1でトリガーされたユーザーインターフェイス要素に基づいてクイックビューURLを取得します。
1. フロントエンドコードは、手順 2 で取得した URL を使用して Ajax リクエストを送信します。
1. バックエンドロジックは、対応するクイックビューのデータまたはコンテンツをフロントエンドコードに返します。
1. フロントエンドコードは、クイックビューのデータまたはコンテンツを読み込みます。
1. オプションで、フロントエンドコードは、読み込んだクイックビューのデータをHTML表現に変換します。
1. フロントエンドコードは、モーダルダイアログボックスまたはパネルを表示し、エンドユーザー向けに、画面上に HTML コンテンツをレンダリングします。

これらの呼び出しは、必ずしも、Webページロジックによって任意の手順から呼び出される、独立したパブリックAPI呼び出しを表すわけではありません。 むしろ、次の手順がすべて前の手順の最終フェーズ（コールバック）に潜むような連鎖的な呼び出しになっています。

ショッパブルインタラクティブ画像が手順1と手順2の一部を置き換えると、ユーザーはショッパブル画像内のホットスポットをタップします。 このようなユーザ操作は、ビューアで処理されます。 ビューアは、以前にホットスポットアセットに追加されたすべてのホットスポットデータを含むWebページにExperience Managerを返します。

そのようなイベントハンドラーでは、フロントエンドコードは次の処理を実行します。

* ショッパブルインタラクティブ画像から送出されるイベントをリッスンします。
* ホットスポットデータに基づいてクイックビューURLを作成します。
* バックエンドからクイックビューを読み込み、画面に表示用にレンダリングするプロセスをトリガーします。

Experience ManagerAssetsから返される埋め込みコードには、次のハイライトされたコードスニペットのように、コメントアウトされた、使いやすいイベントハンドラーが含まれています。

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

クイックビューURLを作成するプロセスは、前述のホットスポットの変数を識別するプロセスとは反対です。

[ホットスポットの変数の識別](#optional-identifying-hotspot-variables)を参照してください。

前のクイックビューURLの例を使用して、次の例では、クイックビューURLの各ケースでの作成方法を示します。

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

クイックビューURLをトリガーし、クイックビューパネルをアクティブにする最後の手順では、作業のフロントエンドIT担当者の支援が必要です。 ユーザーは、クイックビュー実装を適切な手順から正確にトリガーし、すぐに使用できるクイックビューURLを使用する方法を最もよく理解しています。

これらの手順をデモWebサイトに適用してショッパブルインタラクティブ画像をクイックビューのコードに完全に統合する方法を確認できます。以前は、クイックビューURLの構造は次のように識別されていました。

```xml
/datafeed/$categoryId$-$SKU$.json
```

このURLを`quickViewActivate`ハンドラー内で再構成するために、`categoryId`フィールドと`SKU`フィールドを使用できます。 これらのフィールドは、ビューアのコードからハンドラーに渡される`inData`オブジェクト内で使用できます。

```xml
var sku=inData.sku;
var categoryId=inData.categoryId;
var quickViewUrl = "datafeed/" + categoryId + "-" + sku + ".json";
```

このデモWebサイトは、単純な`loadQuickView()`関数呼び出しを使用してクイックビューダイアログボックスを起動しています。 この関数は、1つの引数（クイックビューデータのURL）のみを受け取ります。 したがって、ショッパブルインタラクティブ画像を統合する最後の手順は、`quickViewActivate`ハンドラーに次のコード行を追加することです。

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

## クイックビューを使用したカスタムポップアップの作成{#using-quickviews-to-create-custom-pop-ups}

[クイックビューを使用したカスタムポップアップWindows®](/help/assets/dynamic-media/custom-pop-ups.md)の作成を参照してください。
