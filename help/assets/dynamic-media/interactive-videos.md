---
title: インタラクティブビデオ
description: Dynamic Media でインタラクティブビデオとショッパブルビデオを使用する方法を説明します。
feature: インタラクティブビデオ
topic: 業務担当者
role: Business Practitioner
exl-id: e4859223-91de-47a1-a789-c2a9447e5f71
translation-type: tm+mt
source-git-commit: 6b232ab512a6faaf075faa55c238dfb10c00b100
workflow-type: tm+mt
source-wordcount: '6066'
ht-degree: 49%

---

# インタラクティブビデオ {#interactive-videos}


インタラクティブなビデオは、ショッパブルビデオとも呼ばれ、ビデオから直接コンバージョンを推進するものを簡単に作成できます。ビデオに対する顧客エンゲージメントは、ビデオプレーヤーの隣のパネルでおこなわれ、関連するサービス、情報または製品のサムネールが、ビデオの特集に基づいてスクロール表示されます。顧客はサムネールをタップして、サービスを直接参照したり、買い物かごに商品を追加して即時に購入したり、Web ページを参照して詳細を確認したりできます。

ビデオが終了すると、すべてのオファーの視覚的な概要が表示され、誘い文句（CTA、コールトゥアクション）が実行されます。顧客は、必要な品目をタップする別のオポチュニティがあります。 これらのような実用的で特定のエクスペリエンスにより、顧客の関与やコンバージョンを増やすことができます。

[インタラクティブ画像](/help/assets/dynamic-media/interactive-images.md)も参照してください。

## インタラクティブビデオの使用例  {#interactive-video-in-action}

インタラクティブなショッパブルビデオの動作を確認するには、「[ライブデモ](https://landing.adobe.com/en/na/dynamic-media/ctir-2755/live-demos.html)」をクリックし、ページの「**[!UICONTROL ショッパブルメディア]**」見出しまでスクロールして、ショッパブルビデオをクリックして再生を開始します。

* 再生中にビデオ内で製品が使用されると、同じ製品のサムネール画像が右側に表示されます。

* ビデオを一時停止して製品のクイック表示を開くには、サムネールをタップします。 例えば、ビデオ内のKitchenAidサムネール画像をタップすると、360°のスピン表示が発生します。また、ズームインするとミキサーの詳細が表示されます。

[Dynamic Media でのインタラクティブビデオの使用](https://experienceleague.adobe.com/docs/experience-manager-learn/assets/dynamic-media/dynamic-media-interactive-video-feature-video-use.html?lang=en#dynamic-media)も参照してください。

<!-- 

There was a link here that showed the video frame of an interactive video and when the reader clicked the frame the video would play https://marketing.adobe.com/resources/help/en_US/dm/shoppable-video/AXIS/index.html. This now needs to call a new interactive video

-->

<!-- 

[A frame from an interactive, shoppable video](assets/chlimage_1-126.png) *A video frame capture from an interactive, shoppable video.*

-->

>[!NOTE]
>
>ユーザーがサムネール画像をタップしたときにWebページを起動するインタラクティブビデオを作成する場合、デバイスによってはポップアップWebページが開かないようにブロックする場合があります。 このような場合は、デバイスのポップアップブロッカーの設定を変更してください。 例えば、Apple iPhone 6 では&#x200B;**[!UICONTROL 設定／Safari／ポップアップブロック]**&#x200B;をタップして、コントロールを&#x200B;**[!UICONTROL オフ]**&#x200B;にスライドします。こうすると、インタラクティブビデオを再生してサムネールをクリックしたときに、ポップアップを開くかどうかを確認するメッセージが表示されます。同意すると Web ページが開きます。

### インタラクティブビデオの作成方法を見る  {#watch-how-interactive-videos-are-created}

[インタラクティブビデオの作成方法](https://s7d5.scene7.com/s7viewers/html5/VideoViewer.html?videoserverurl=https://s7d5.scene7.com/is/content/&amp;emailurl=https://s7d5.scene7.com/s7/emailFriend&amp;serverUrl=https://s7d5.scene7.com/is/image/&amp;config=Scene7SharedAssets/Universal_HTML5_Video_social&amp;contenturl=https://s7d5.scene7.com/skins/&amp;asset=S7tutorials/InteractiveVideo)[](https://outv.omniture.com?v=s4NHQ2dzqd7hIqWjeG2sIdyNWsTWyupA)を示す 7 分 30 秒のガイドをご覧ください(このビデオチュートリアルはAssets on Demandでブランド化されていますが、原則と手順はAdobe Experience Managerアセットのインタラクティブビデオにも当てはまります)。

### アドビカスタマーサクセスウェビナー {#adobe-customer-success-webinar}

[Experience Managerアセットでのインタラクティブビデオの使用、リンクの共有、YouTubeの共有](https://adobecustomersuccess.adobeconnect.com/p1yxzdo4aec/)ウェビナーでは、インタラクティブビデオや他の機能を使用して、コンバージョンに依存するイベントをビデオマーケティングコンテンツに結び付ける方法について説明します。

## クイックスタート：インタラクティブビデオ {#quick-start-interactive-videos}

次のワークフローの手順説明は、Dynamic Media 内のインタラクティブビデオをすぐに使い始めることを目的としたものです。

一部のクイックスタートタスク内には「**例**」という見出しがあります。これには次の、[まだインタラクティビティが追加されていない最初の状態のデモ *Web* ページ](https://marketing.adobe.com/resources/help/en_US/dm/shoppable-video/john-lewis/landing-0.html)に基づく、簡単なチュートリアルが含まれています。

「**例**」では、Web サイトにインタラクティブビデオを統合する手順が説明されています。

最後の例のセクションでチュートリアルを終えると、完全に統合されたインタラクティブビデオを含む[最後のデモWebページが](https://marketing.adobe.com/resources/help/en_US/dm/shoppable-video/john-lewis/landing-3.html)のように表示されます。



インタラクティブビデオの手順：

1. **（オプション）クイック表示変数の識別**  — 既存のクイック表示で使用される動的変数を識別して開始します。インタラクティブビデオを作成する場合は、変数を使用して、商品のサムネールを対応する商品のクイック表示にマップします。 「[（オプション）クイック表示変数の識別](#optional-identifying-quickview-variables)」を参照してください。
   **この手順は、次のすべてが真の場合にのみ必要です**。・クイック表示をトリガーして、ビデオにインタラクティブ機能を追加する場合。・Experience Managerの導入では、IBM WebSphere® Commerce、Elastic Path、hybris、Intershopなどのeコマースソリューションから製品データをExperience Managerに引き出すためのeCommerce統合フレームワークを&#x200B;*使用しません*。

1. **（オプション）インタラクティブビデオのビューアプリセットの作成** - プレーヤーを構成する様々なコンポーネント（ビデオスクラバーやインタラクティブサムネールなど）の外観と動作をカスタマイズします。独自のインタラクティブビデオビューアプリセットの作成は、標準提供のインタラクティブビデオビューアプリセット（`Shoppable_Video_Light` または `Shoppable_Video_Dark`）を使用する場合には必要ありません。詳しくは、[新しいビューアプリセットの作成](/help/assets/dynamic-media/managing-viewer-presets.md#creating-a-new-viewer-preset)（オプション）および[インタラクティブビューアプリセットを作成する際の特別な考慮点](/help/assets/dynamic-media/managing-viewer-presets.md#special-considerations-for-creating-an-interactive-viewer-preset)を参照してください。

1. **ビデオおよび関連する画像アセットのアップロード** - インタラクティブにするビデオと関連する画像をアップロードします。[ビデオおよび関連するサムネールアセットのアップロード](#uploading-a-video-and-its-associated-thumbnail-assets)を参照してください。

1. **ビデオへのインタラクティビティの追加** - ビデオに 1 つ以上の時間セグメントを追加します。次に、それらの時間セグメント内で画像サムネールを関連付けます。各画像のサムネールを、ハイパーリンク、クイック表示、エクスペリエンスフラグメントなどのアクションに割り当てます。
(インタラクティブコンテンツに相対URLを持つリンク、特にExperience Managerサイトページへのリンクが含まれる場合、URLベースのリンク方式は使用できません)。
インタラクティブビデオアセットを公開して作業は完了です。公開すると、埋め込みコードまたはURLが作成され、最終的にコピーしてWebサイトのランディングページに適用されます。 [ビデオへのインタラクティビティの追加](#adding-interactivity-to-your-video)を参照してください。[アセットの公開](/help/assets/dynamic-media/publishing-dynamicmedia-assets.md)を参照してください。

1. **インタラクティブビデオのWebサイトまたはExperience Manager内のWebサイトへの追加** -Experience Managerサイト、Experience Managereコマースまたはその両方を使用している場合、Experience Manager内のWebページに直接インタラクティブビデオを追加できます。インタラクティブメディアコンポーネントをページにドラッグします。 [ページへの Dynamic Media アセットの追加](/help/assets/dynamic-media/adding-dynamic-media-assets-to-pages.md)を参照してください。
埋め込みコードまたは URL を使用して、インタラクティブビデオを Web サイトエクスペリエンスに統合します。[インタラクティブビデオの Web サイトへの統合](#integrating-an-interactive-video-with-your-website)を参照してください。サードパーティのWCM(Web Content Manager)を使用する場合は、新しいインタラクティブビデオを、Webサイトで使用されている既存のクイック表示実装と統合する必要があります。 詳しくは、[インタラクティブビデオと既存のクイック表示の統合](#integrating-an-interactive-video-with-an-existing-quickview)を参照してください。
   [ページへの Dynamic Media アセットの追加](/help/assets/dynamic-media/adding-dynamic-media-assets-to-pages.md)

## （オプション）クイック表示変数の識別{#optional-identifying-quickview-variables}

>[!NOTE]
このタスクが必要になるのは次に該当する場合のみです。
* クイック表示をトリガーして、ビデオにインタラクティブ機能を追加する場合。
* Experience Managerの導入では、eCommerce統合フレームワークを&#x200B;*使用せず、*、IBM WebSphere® Commerce、Elastic Path、hybris、Intershopなどのeコマースソリューションから製品データをExperience Managerに取り込みます。<!-- See [eCommerce concepts in Experience Manager Assets](/help/sites-administering/concepts.md).-->

Experience Managerの導入でeコマースを使用している場合は、このタスクをスキップして次のタスクに進むことができます。

開始を行うために、既存のクイック表示の実装で使用される動的変数を識別します。これにより、インタラクティブビデオ作成プロセス中に、商品のサムネールを対応する商品のクイック表示にマッピングできます。

ビデオに時間セグメントを追加する場合、SKU(Stock Keeping Unit)と追加の変数をセグメントに追加する各サムネールに割り当てます。 このような変数は、後で適切なクイック表示製品を表示するために使用されます。

製品のクイック表示を一意にトリガーするために必要な変数を適切に識別することが重要です。

お客様の既存のクイック表示導入を担当するITスペシャリストに相談すると十分な場合があります。 システム内のクイック表示を識別する最小のデータセットを知っている可能性が高くなります。 ただし、フロントエンドコードの既存の動作を単純に分析することは可能です。

ほとんどのクイック表示の実装では、次のようなパラダイムが使用されます。

* ユーザーがWebサイト上でユーザーインターフェイス要素をアクティブにします。例えば、「クイック表示」ボタンをクリックします。
* Webサイトは、必要に応じて、クイック表示のデータまたはコンテンツを読み込むために、Ajaxリクエストをバックエンドに送信します。
* クイック表示データは、Webページへのレンダリングに備えてコンテンツに変換されます。
* 最後に、フロントエンドコードによってそのコンテンツが画面上に視覚的にレンダリングされます。

したがって、このアプローチでは、クイック表示が実装されている既存のWebサイトの様々な領域を訪問します。 次に、クイック表示をトリガーし、Webページから送信されたAjax URLを取り込み、クイック表示のデータまたはコンテンツを読み込みます。

通常、専門のデバッグツールを使用する必要はありません。最新の Web ブラウザーには、十分なタスクを実行できる Web インスペクターが備わっています。Web インスペクターが搭載されている Web ブラウザーの例を次に示します。

* Google Chrome で、ブラウザーから送信されるすべての HTTP リクエストを参照するには、**F12** キー（Windows）または **Command + Options + I** キー（Mac）を押してデベロッパーツールパネルを開き、「**Network**」タブをクリックします。

* Firefox では、**F12** キー（Windows）または **Command + Option + I** キー（Mac）を押して Firebug プラグインを有効にして「**[!UICONTROL Net]**」タブを使用するか、組み込みの Inspector ツールとその「Network」タブを使用します。

* Internet Explorerで、**F12**&#x200B;を押してデバッガーツールをアクティブにします。

ブラウザーでネットワーク監視を有効にする場合は、ページのクイック表示をトリガーします。

次に、表示ログでクイックネットワークのAjax URLを探し、記録したURLをコピーして、分析を後で行います。 通常、クイック表示をトリガーすると、サーバーに送信される要求が多数あります。 通常、クイック表示のAjax URLはリストの最初のURLの1つです。 この URL には複雑なクエリ文字列部分またはパスが含まれ、その応答の MIME タイプは `text/html`、`text/xml`、`text/javascript` のいずれかになります。

このプロセスでは、製品のカテゴリやタイプを変えて、Webサイトの様々な領域を訪問することが重要です。 クイック表示URLには、特定のWebサイトカテゴリに共通な部分がありますが、Webサイトの別の領域を訪問した場合にのみ変更されるためです。

最も単純なケースでは、クイック表示URLの唯一の変数部分が製品SKUです。 この場合、Experience Manager内のインタラクティブビデオの時間セグメントにサムネールを追加する際に必要なデータ要素は、product SKU値だけです。

ただし、複雑な場合は、カテゴリIDや色コードなど、表示SKUに加えて、クイック製品URLには様々な要素があります。 この場合、そのような要素はすべて、Experience Managerのサムネールデータ定義で別々の変数になります。

以下のクイック表示URLの例と、その結果得られるサムネール変数を考えてみましょう。

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
    </ul> <p>この URL で変化する唯一の部分は <code>productId=</code> というクエリ文字列パラメーターの値であり、これが SKU 値であることは明白です。したがって、サムネールに必要なのは、<strong><code>866558</code></strong>、<strong><code>1196184</code></strong>、<strong><code>1081492</code></strong>、<strong><code>1898294</code></strong>のような値を含むSKUフィールドだけです。</p> </td>
  </tr>
  <tr>
    <td><p>単一の SKU（URL パス内）</p> </td>
    <td><p>記録されるクイック表示URLは次のとおりです。</p>
    <ul>
      <li><p><code>https://server/product/6422350843</code></p> </li>
      <li><p><code>https://server/product/1607745002</code></p> </li>
      <li><p><code>https://server/product/0086724882</code></p> </li>
    </ul> <p>変数部分はパスの最後の部分にあり、Experience ManagerサムネールのSKU値になります。<strong><code>6422350843</code></strong>、<strong><code>1607745002</code></strong>、<strong><code>0086724882</code></strong>。</p> </td>
  </tr>
  <tr>
    <td><p>SKU とカテゴリ ID（クエリ文字列内）</p> </td>
    <td><p>記録されるクイック表示URLは次のとおりです。</p>
    <ul>
      <li><p><code>https://server/quickView/product/?category=1100004&amp;prodId=305466</code></p> </li>
      <li><p><code>https://server/quickView/product/?category=1100004&amp;prodId=310181</code></p> </li>
      <li><p><code>https://server/quickView/product/?category=1740148&amp;prodId=308706</code></p> </li>
    </ul> <p>この場合、URL には変化する部分が 2 つあります。SKU が <code>prodId</code> パラメーターに、カテゴリ ID が <code>category=</code> パラメーターに格納されています。</p> <p>そのため、サムネール定義はペアになります。つまり、SKU値と<code>categoryId</code>という追加の変数です。 結果のペアは次のようになります。</p>
    <ul>
      <li>SKU が <code>305466</code>、<code>categoryId</code> が  <code>1100004</code></li>
      <li>SKU が <code>310181</code>、<code>categoryId</code> が  <code>1100004</code></li>
      <li>SKU が <code>308706</code>、<code>categoryId</code> が  <code>1740148</code></li>
    </ul> <p> </p> </td>
  </tr>
  </tbody>
</table>

**例**

上記の方法をサンプルのWebサイトに適用した場合、複数の製品サムネールを含むWebページがあり、それぞれに「詳細を表示」ボタンがあります。

[https://marketing.adobe.com/resources/help/en_US/dm/shoppable-video/john-lewis/landing-0.html](https://marketing.adobe.com/resources/help/en_US/dm/shoppable-video/john-lewis/landing-0.html)

ページで使用可能なすべての製品クイック表示をアクティブ化すると、バックエンドに対して行われたクイック表示要求の次のリストが取得されます。

* datafeed/candles-233396346.json
* datafeed/candles-233978050.json
* datafeed/candles-234024346.json
* datafeed/candles-234024356.json
* datafeed/candles-234024359.json
* datafeed/cushions-233939848.json
* datafeed/cushions-234019477.json
* datafeed/cushions-234019483.json
* datafeed/furniture-231747479.json
* datafeed/furniture-232625621.json
* datafeed/furniture-232625626.json
* datafeed/furniture-233939810.json
* datafeed/furniture-233939825.json
* datafeed/furniture-233939828.json
* datafeed/furniture-233939853.json
* datafeed/furniture-233940334.json
* datafeed/glassware-000064007.json
* datafeed/glassware-230722193.json
* datafeed/glassware-233916550.json
* datafeed/glassware-233916597.json

サーバーコールを調べると、製品固有の情報がリクエストパスにのみ存在します。 また、クエリ文字列がまったく使用されていないこと、2 つの異なるタイプのデータが含まれることもわかります。

* 最初のタイプは、candles、cushions、furniture、glassware です。これは「製品カテゴリ」と呼ばれます。
* 2 つ目のタイプは製品コード（233916597 など）です。これは「製品 SKU」と考えることができます。

この情報を取得すると、クイック表示URL全体に次のパターンが適用されます。

`/datafeed/$categoryId$-$SKU$.json`

こうした分析に基づいて、サムネールには `categoryId` と `SKU` の 2 つの変数を使用できるという結論が得られます。

これで、ビデオおよび関連するサムネールアセットをアップロードできます。

## （オプション）インタラクティブビデオのビューアプリセットの作成  {#optional-creating-an-interactive-video-viewer-preset}

デフォルトの標準提供インタラクティブビデオビューアプリセットタイプ（`Shoppable_Video_dark` または `Shoppable_Video_light`）を使用する予定がある場合は、このタスクをスキップして次に進むことができます。

オーサリング環境でサムネールをタップすると、クイック表示ダイアログボックスのプレビューが表示されます。

![chlimage_1-21](assets/chlimage_1-127.png)

オプションで、インタラクティブビデオの独自のカスタムビューアプリセットを作成することもできます。特に、ビデオプレーヤーのスタイル設定、インタラクティブサムネールおよびビデオの最後に表示されるサムネールのグリッドビューを決定できます。

インタラクティブビデオビューアプリセットは、ビデオと、追加したすべてのタイムラインセグメントを適切にレンダリングします。また、プレビューモードで商品のサムネールをクリックしたときに、公開前にインタラクティブ機能をテストできるように、初期設定のクイック表示例も使用されています。

ビューアプリセットを保存すると、ビューアプリセットページでそのプリセットのステータスが自動的にオンに設定されます。このステータスは、そのプリセットが Dynamic Media コンポーネントに表示され、ビデオのプレビュー時に必ず使用されることを意味します。また、新しいビューアプリセットも忘れずに手動で公開してください。

[新しいビューアプリセットの作成](/help/assets/dynamic-media/managing-viewer-presets.md#creating-a-new-viewer-preset)を参照して、独自のインタラクティブビデオのビューアプリセットを作成します。

## ビデオおよび関連するサムネールアセットのアップロード {#uploading-a-video-and-its-associated-thumbnail-assets}

ビデオとサムネールアセットを既にアップロードしている場合は、[ビデオへのインタラクティブ機能の追加](#adding-interactivity-to-your-video)に進んでください。

誤ったビデオや画像をアップロードした場合、または必要でなくなったアップロード済みビデオや画像を削除したい場合は、[アセットの削除](/help/assets/manage-digital-assets.md#delete-assets)を参照してください。

ビデオおよび関連するサムネールアセットをアップロードするには：

1. 目的の 1 つ以上のフォルダーにビデオおよび関連するサムネールアセットをアップロードします。

   [アセットのアップロード](/help/assets/manage-digital-assets.md)を参照してください。
[FTP ジョブスケジューリングを使用したアセットのアップロード](/help/assets/manage-digital-assets.md)を参照してください。

   これで、ビデオにインタラクティブ機能を追加できます。

## ビデオへのインタラクティブ機能の追加 {#adding-interactivity-to-your-video}

「インタラクティブビデオを作成」ページで、インプレース Visual Editor を使用してビデオにタイムラインセグメントを追加します。

タイムラインセグメントを追加した後、各セグメントにサムネール画像を追加します。追加した各サムネールにアクションを適用します。例えば、サムネールにクイック表示を適用したり、サムネールにハイパーリンクを割り当てたり、エクスペリエンスフラグメントを割り当てたりできます。

[エクスペリエンスフラグメント](/help/sites-cloud/authoring/fundamentals/experience-fragments.md)を参照してください。

>[!NOTE]
インタラクティブビデオのソーシャルメディア共有ツールは、エクスペリエンスフラグメントにビューアを埋め込む場合はサポートされません。 代わりに、ソーシャルメディア共有ツールを持たないビューアプリセットを使用または作成できます。 このようなビューアプリセットを使用すると、ビューアをエクスペリエンスフラグメントに正常に埋め込むことができます。

>[!NOTE]
インタラクティブコンテンツに相対URLを持つリンク(特にExperience Managerサイトページへのリンク)がある場合、URLベースのリンク方法は使用できません。

ページの右上隅にある「取り消し」および「やり直し」オプションは、現在の作成／編集セッションの間で有効です。

インタラクティブビデオを保存すると、ビデオはすぐにプレビューに開きます。 ここからインタラクティブビデオビューアのプリセットを選択し、ビデオを再生して、顧客に対してどのように表示されるかをおおよそ確認できます。

**ビデオにインタラクティブ機能を追加するには**:

1. Assets ビューで、インタラクティブにするアップロード済みのビデオに移動します。
1. 次のいずれかの操作をおこないます。

   * 画像の上にマウスポインターを置き、**[!UICONTROL 選択]**（チェックマークアイコン）をタップします。ツールバーの「**[!UICONTROL 編集]**」をタップします。

   * 画像の上にマウスポインターを置き、**[!UICONTROL その他のアクション]**（3 つのドットのアイコン）／**[!UICONTROL 編集]**&#x200B;をタップします。

   * 詳細表示ページで画像を開くには、画像をタップします。 ツールバーで、**[!UICONTROL 編集]**&#x200B;をタップします。

1. インタラクティブビデオを作成ページで、次のいずれかの操作をおこないます。

   * ビデオの再生を開始するには、「**[!UICONTROL 再生]**」ボタンをタップします。 強調したい特定の製品、サービス、または詳細が表示に入ったら、ツールバーの&#x200B;**[!UICONTROL 追加セグメント]**&#x200B;をタップします。 ビデオの最後に到達するまで繰り返します。

      追加する各セグメントに対して、1つ以上のサムネール画像を割り当てることができます。 その後、これらのサムネールをクイック表示の商品ページにリンクして、顧客が購入できるようにしたり、Webページにリンクして詳細を表示したりできます。

   * ビデオの再生を開始するには、「**[!UICONTROL 再生]**」ボタンをタップします。 強調したい特定の製品、サービス、または詳細が表示に入ったら、**[!UICONTROL 一時停止]**&#x200B;をタップします。 「**[!UICONTROL セグメント追加]**」をタップします。

      ビデオの最後に到達するまで、セグメントを追加するタイムラインのポイントで、ビデオの再生と停止を続けます。

1. （オプション）**[!UICONTROL タイムラインスケールスライダ]**&#x200B;の左側のバーをドラッグしてズームインし、右にドラッグしてズームアウトします。 この操作により、追加したセグメントの詳細表示を制御できます。

   ![chlimage_1-22](assets/chlimage_1-128.png)

   ビデオの長さに応じた「セグメントの期間」のデフォルト値を次に示します。

   <table>
      <tbody>
        <tr>
        <td><strong>ビデオの長さ</strong></td>
        <td><strong>「セグメントの期間」のデフォルト値</strong></td>
        </tr>
        <tr>
        <td>3 分以上</td>
        <td>60 秒</td>
        </tr>
        <tr>
        <td>2～3 分</td>
        <td>30 秒</td>
        </tr>
        <tr>
        <td>1～2 分</td>
        <td>20 秒<br /> </td>
        </tr>
        <tr>
        <td>30～60 秒</td>
        <td>10 秒</td>
        </tr>
        <tr>
        <td>30 秒以下</td>
        <td>5 秒</td>
        </tr>
      </tbody>
    </table>

   ビデオのタイムラインは、使用できる最大限の画面領域を使用します。したがって、ブラウザーのサイズを変更しても、追加したセグメントの幅は正しく維持されます。

   説明するために、次の 3 つのスクリーンショットでは同じビデオを使用しています。各セグメントの幅が「タイムラインスケール」の設定に応じて変化することに注意してください。

   ![chlimage_1-23](assets/chlimage_1-129.png)

   スクリーンショット A

   上のスクリーンショットAは、29秒の製品ビデオのデフォルト表示を示しています。 タイムラインスケールはデフォルトの 5 秒に設定されています。

   ![chlimage_1-130](assets/chlimage_1-130.png)

   スクリーンショット B

   上のスクリーンショット B では、タイムスケールスライダーがデフォルトの 5 秒から 3 秒にドラッグされました。個々のタイムラインスケールのタイムスタンプが、すべて3秒の間隔で設定されています。

   ![chlimage_1-25](assets/chlimage_1-131.png)

   スクリーンショット C

   上のスクリーンショット C では、タイムラインスケール設定が 8 秒になっています。製品サムネールを含むセグメントの表示が縮小されていることに注意してください。このような縮小表示が役立つのは、ビデオが長く、通常はページの幅に収まらないセグメントの概要を確認する場合です。

1. （オプション）次のいずれかの操作をおこないます。

   * セグメントの開始時刻と終了時刻を調整します。

        セグメントを選択し、先頭または末尾の青い楕円形をドラッグして、開始時刻または終了時刻をそれぞれ調整します。表示されるビデオフレームは、調整に応じて、ビデオ内の対応する時刻に移動します。タイムラインセグメントの移動は、タイムライン内の隣接するセグメントに基づいて制限されます。調整できる最小セグメント時間は 1 秒です。

        次のナビゲーションショートカットを使用すると、ビデオのセグメントを簡単にチェックして微調整することができます。

      * そのセグメントの先頭にビデオを直接シークするには、先頭の青い楕円をタップします。
      * セグメントの最後までビデオを直接シークするには、末尾の青い楕円をタップします。
      * ビデオ再生をそのセグメントの開始に戻すには、セグメント全体をタップします。

   ![chlimage_1-26](assets/chlimage_1-132.png)

   タイムラインセグメントの末尾の再配置

   * セグメントを削除するには

      タイムライン上にある最後のセグメントを選択し、ツールバーの「**[!UICONTROL セグメントを削除]**」をタップします。2 つ以上のセグメントを選択した場合、「セグメントを削除」機能は使えません。

      削除できるのは最後のセグメントのみです。例えば、タイムライン上のすべてのセグメントを削除したい場合、常に最後のセグメントを選択して「**[!UICONTROL セグメントを削除]**」をタップします。


1. 1 つまたは複数のサムネール画像を関連付ける時間セグメントを選択します。
1. ビデオの右側にある「**[!UICONTROL コンテンツ]**」タブをタップします。
1. 「コンテンツ」タブの下で「**[!UICONTROL アセットを選択]**」をタップし、ビデオで使用するすべての画像アセットを参照して選択します。選択したアセットは「コンテンツ」タブのアセットセレクターパネルに追加されます。

1. 「コンテンツ」タブの下にあるアセットセレクターで、次のいずれかの操作をおこないます。

   <table>
      <tbody>
        <tr>
        <td>選択したタイムラインセグメントにサムネールを関連付けるには</td>
        <td><p>右側のアセットセレクターパネルで画像をタップします。</p> <p>1 つのタイムラインセグメントに好きなだけサムネールを追加できます。選択した各画像について、アセットセレクターの画像の上にチェックマークが表示されます。</p> </td>
        </tr>
        <tr>
        <td>選択したタイムラインセグメントからサムネールを削除するには</td>
        <td><p>次のいずれかの操作をおこないます。</p>
          <ul>
          <li>アセットセレクターパネルで、チェックマークの付いている画像をタップして選択を解除します。画像アセットがタイムラインセグメントから削除されます。<br /> </li>
          <li>選択したタイムラインセグメントで、画像をタップし、ツールバーの「<strong>製品を削除</strong>」をタップします。</li>
          </ul> </td>
        </tr>
      </tbody>
    </table>

   ![アセットピッカー](assets/chlimage_1-133.png)

   アセットセレクターパネルで画像をタップすると、選択したタイムラインセグメントにその画像が追加されます。

1. 1 つのタイムラインセグメント内のサムネール画像を 1 つ選択し、「**[!UICONTROL アクション]**」タブをタップします。
1. 次のいずれかの操作をおこないます。
   <table> 
    <tbody> 
      <tr> 
      <td>選択したサムネール画像をクイック表示に関連付けるには</td> 
      <td><p>「アクションの種類」で、<strong>クイック表示</strong>をタップします。</p> <p>Experience Managerサイトおよびeコマースのお客様の場合：</p> 
       <ul> 
       <li>「SKU値」テキストフィールドには、選択した製品のSKU（在庫保持単位）が事前に設定されています。 SKUは、オファー対象の個々の製品やサービスに固有の識別子です。 このフィールドは、Experience Managerが商取引の商品に関連付けられている場合に自動的に入力されます。</li> 
       <li>設定済みの SKU が正しくない場合は、製品ピッカーアイコン（虫眼鏡）をタップまたはクリックして製品を選択ページを開きます。使用する製品をタップし、ページの右上隅にあるチェックマークをタップします。 インタラクティブビデオエディターに戻ります。</li> 
       </ul> <p> お客様がExperience Managerサイトやeコマースのお客様では<em>ない</em>場合</p> 
       <ul> 
       <li><a href="/help/assets/dynamic-media/carousel-banners.md#identifying-hotspot-and-image-map-variables">ホットスポットの変数の識別</a>を参照してください。これらの変数は定義する必要があります。</li> 
       <li>デフォルトでは、この SKU フィールドでは画像アセットのファイル名を拡張子を付けずに使用します。SKUに基づくファイルの標準的な命名規則に従う場合、通常、このフィールドで追加の編集を行う必要はありません。 </li> 
       <li>それ以外の場合は、デフォルト値を編集して、正しい SKU 値を入力します。「SKU 値」テキストフィールドに、製品の SKU（Stock Keeping Unit）を入力します。SKU は、提供している製品またはサービスごとの一意の識別子です。入力したSKU値によって、クイック表示テンプレートの可変部分が自動的に設定され、タップされた画像と特定のSKUのクイックビューが関連付けられます。</li> 
       </ul> <p>（オプション）クイック表示内に他の変数があり、それを使用して製品をさらに識別する必要がある場合は、<strong>追加汎用変数</strong>をタップします。 テキストフィールドで、追加の変数を指定します。 例えば、追加の変数として <code>category=Womens</code> などと指定します。</p> <p> </p> </td> 
      </tr> 
      <tr> 
      <td>選択したサムネール画像をハイパーリンクに関連付けるには</td> 
      <td><p>「アクションタイプ」の下の「<strong>ハイパーリンク</strong>」をタップして、次のいずれかを実行します。</p> 
       <ul> 
       <li>Experience Managerサイトのお客様の場合は、サイト選択アイコン（フォルダー）をタップしてWebページに移動します。 インタラクティブコンテンツに相対URLを持つリンク(特にExperience Managerサイトページへのリンク)がある場合、URLベースのリンク方法は使用できません。</li> 
       <li>スタンドアロンの Dynamic Media ユーザーである場合は、「HREF」テキストフィールドに、リンクされる Web ページへの完全な URL パスを指定します。</li> 
       </ul> <p>このリンクを新しいブラウザータブで開くか現在のタブで開くかを指定してください。</p> </td> 
      </tr> 
      <tr> 
      <td>選択したサムネール画像をエクスペリエンスフラグメントに関連付けるには</td> 
      <td><p>「アクションタイプ」の下の「<strong>エクスペリエンスフラグメント</strong>」をタップし、次のいずれかを実行します。<p> 
       <ul> 
       <li>Experience Managerサイトのお客様は、検索アイコン（虫めがね）をタップして、エクスペリエンスフラグメントページを開きます。 使用するエクスペリエンスフラグメントをタップまたはクリックし、<strong>「前のページのアクションパネルに戻る」をタップします。ページの右上隅にある</strong>を選択します。<br /><a href="/help/sites-cloud/authoring/fundamentals/experience-fragments.md">エクスペリエンスフラグメント</a>を参照してください。</li> 
      </ul> 
       <ul> 
       <li>ビデオに表示されるエクスペリエンスフラグメントの幅と高さを指定します。</li>
       </ul><strong>注意</strong>:インタラクティブビデオのソーシャルメディア共有ツールは、エクスペリエンスフラグメントにビューアを埋め込む場合はサポートされません。代わりに、ソーシャルメディア共有ツールを持たないビューアプリセットを使用または作成できます。 このようなビューアプリセットを使用すると、ビューアをエクスペリエンスフラグメントに正常に埋め込むことができます。</p></tr>&lt; 
      <tr> 
      <td>既にサムネール画像に割り当てられているアクションを編集するには</td> 
      <td>タイムラインセグメント内で、テキストラベルの右側にチェーンリンクがあるサムネール画像をタップします。チェーンリンクは、アクションが割り当てられていることを示します。 変更を行うには、「<strong>アクション</strong>」タブをタップします。</td> 
      </tr> 
      <tr> 
      <td>サムネール画像のテキストラベルを変更するには</td> 
      <td><p>デフォルトでは、テキストラベルはサムネール画像の <code>Title</code> メタデータフィールドを使用します。<code>Title</code>がない場合は、代わりにサムネール画像のファイル名が使用されますが、拡張子は付きません。</p> <p>サムネール画像のテキストラベルを変更するには、「<strong>アクション</strong>」タブで、表示される画像アセットのすぐ下に目的のテキストを入力します。下の図を参照してください。</p> <p>新しいテキストラベルは、ビデオプレーヤー自体と、タイムラインセグメントに表示されるサムネールテキストでのみ使用されます。 ラベルの変更は、サムネール画像のタイトルメタデータフィールドとファイル名には影響しません。</p> </td> 
      </tr> 
      <tr> 
      <td>加えた変更を元に戻すには</td> 
      <td>ページの右上隅にある「<strong>取り消し</strong>」または「<strong>元に戻す</strong>」をタップします。</td> 
      </tr> 
    </tbody> 
   </table>

   ![experiencefragment_interactivevideos](assets/experiencefragment_interactivevideos.png)

   新しいテキストラベルがサムネール画像に追加されています。

1. 次のいずれかの操作をおこないます。

   * 手順 6～11 を繰り返して、ビデオのタイムラインセグメントに複数のサムネール画像を追加します。
   * オプションの手順 13 をおこないます。

1. （オプション）次のいずれかの操作をおこないます。

   * **[!UICONTROL セグメントを統合]** ‐ 2 つの隣接したセグメントを（製品サムネールが割り当てられているものも割り当てられていないものも）1 つのセグメントに統合できます。

      タイムライン上で、1 つのセグメントに統合する 2 つ以上の連続したセグメントをタップします。下の図で選択した2つのセグメントに青い楕円のドラッグハンドルはありません。

      ツールバーの「**[!UICONTROL セグメントを統合]**」をタップします。
   ![chlimage_1-134](assets/chlimage_1-134.png)

   選択した2つの5秒のセグメントを1つの10秒のセグメントに結合する。

   * **[!UICONTROL セグメントを分割]** ‐ 1 つのセグメントを 2 つの均等な長さのセグメントに分割できます。セグメントに製品サムネールが割り当てられている場合、サムネールは左のセグメントに組み込まれます。

      タイムラインで、半分に分割したいセグメントをタップし、ツールバーで「**[!UICONTROL セグメントを分割]**」をタップします。

      2 つ以上のセグメントを選択すると、「**[!UICONTROL セグメントを分割]**」オプションは無効になります。
   ![chlimage_1-135](assets/chlimage_1-135.png)

   選択した10秒のセグメントを5秒ずつ2つのセグメントに分割する。

1. **[!UICONTROL インタラクティブビデオを作成]**&#x200B;ページの右上隅付近に、現在選択されてビデオで使用されているビューアプリセットの名前が表示されます。別のビューアプリセットを選択するには、名前をタップします。

   例えば、`Shoppable_Video_light`ビューアプリセットを使用すると、ビデオの横に白の表示領域が表示され、ビデオを再生できます。 この表示領域には、クリック可能なサムネール画像が再生中に表示されます。`Shoppable_Video_dark`ビューアプリセットを使用すると、ビデオの横に黒い表示領域が表示されてビデオを再生できます。

   独自のインタラクティブビデオビューアプリセットを作成した場合は、プリセットのリストでそのプリセットを表示できます。

   完了したら、「**[!UICONTROL 保存]**」をタップします。

   >[!NOTE]
   インタラクティブビデオを保存すると、関連付けられた `.vtt` ファイルも自動的に保存されます。`.vtt`ファイルは、**[!UICONTROL Assets]**&#x200B;のルートにある`_VTT`フォルダーに保存されます。 インタラクティブビデオが Web サイト上で正しく再生されるには、それらのファイルとフォルダーが必要です。したがって、`_VTT` フォルダーやフォルダーのコンテンツを移動したり、編集したり削除しないでください。

1. インタラクティブビデオを公開します。 公開すると、埋め込みコードまたは埋め込みURLが作成され、最終的にWebサイトのエクスペリエンスにコピーして貼り付けられます。

   クイック表示を使用してインタラクティブ機能を追加した場合は、埋め込みコードのみを使用します。ハイパーリンクwebページにインタラクティブ機能を追加した場合は、公開済みURLも使用できます。 ただし、インタラクティブコンテンツに相対URLを持つリンク(特にExperience Managerサイトページへのリンク)が含まれる場合、URLベースのリンク方法は使用できません。

   [アセットの公開](publishing-dynamicmedia-assets.md)を参照してください。

   >[!NOTE]
   クイック表示を使用して買い物可能なビデオを公開するには、必ず各ビデオの関連画像アセットをコマースエリアから別々に公開してください。

   タイムラインセグメントを追加し、インタラクティブビデオを公開したので、既存の Web サイトのランディングページにビデオを追加する準備が整いました。[インタラクティブビデオの Web サイトへの統合](#integrating-an-interactive-video-with-your-website)を参照してください。

## インタラクティブビデオアセットの公開 {#publishing-interactive-video-assets}

インタラクティブビデオアセットの公開方法について詳しくは、[アセットの公開](/help/assets/dynamic-media/publishing-dynamicmedia-assets.md)を参照してください。

## インタラクティブビデオの Web サイトへの統合 {#integrating-an-interactive-video-with-your-website}

ビデオをアップロードし、タイムラインセグメントを追加して、インタラクティブビデオを公開したら、既存の Web サイトにビデオを追加する準備は完了です。

Experience Managerサイトのお客様は、インタラクティブビデオを追加できます。追加するには、インタラクティブメディアコンポーネントをページにドラッグします。 [ページへの Dynamic Media アセットの追加](/help/assets/dynamic-media/adding-dynamic-media-assets-to-pages.md)を参照してください。

スタンドアロンのExperience Managerアセットをご利用の場合は、この節で説明するように、インタラクティブビデオをWebサイトに手動で追加できます。

1. 公開済みのインタラクティブビデオの埋め込みコードまたは URL をコピーします。[Web ページへのビデオビューアまたは画像ビューアの埋め込み](/help/assets/dynamic-media/embed-code.md)を参照してください。クイック表示を使用してインタラクティブ機能を追加した場合は、埋め込みコードのみを使用します。ハイパーリンクwebページにインタラクティブ機能を追加した場合は、公開済みURLも使用できます。 ただし、インタラクティブコンテンツに相対URLを持つリンク(特にExperience Managerサイトページへのリンク)が含まれる場合、URLベースのリンク方法は使用できません。

1. ターゲットの Web ページのコードで、静的なビデオの場所を特定します。

1. 静的ビデオを削除し、コードを、Experience Managerアセットからコピーした埋め込みコードまたはURLに置き換えます。
コピーされた埋め込みコードはレスポンシブ環境用に設定されるので、以前静的ビデオが表示されていた領域に合わせて自動的に調整されます。

>[!NOTE]
そのため、ハイパーリンクされた Web ページのみを使用したインタラクティビティを追加した場合は、これで完了です。
ただし、トリガーにクイック表示にインタラクティブ機能を追加した場合、インタラクティブビデオの横のサムネールは表示目的でのみ使用されます。まだ既存のクイック表示と統合されていません。 その場合、インタラクティブビデオをWebサイト上の既存のクイック表示と統合する必要があります。

**例**

次のデモ Web サイトを例として使用します。

[https://marketing.adobe.com/resources/help/en_US/dm/shoppable-video/john-lewis/landing-0.html](https://marketing.adobe.com/resources/help/en_US/dm/shoppable-video/john-lewis/landing-0.html)

ビデオ埋め込みコードは標準です。

```xml
<style type="text/css">
 #s7video_div.s7videoviewer{
   width:100%;
   height:auto;
 }
</style>

<script type="text/javascript" src="https://demos-pub.assetsadobe.com/etc/dam/viewers/s7viewers/html5/js/VideoViewer.js"></script>
<div id="s7video_div"></div>
<script type="text/javascript">
 var s7videoviewer = new s7viewers.VideoViewer({
  "containerId" : "s7video_div",
  "params" : {
   "serverurl" : "https://adobedemo62-h.assetsadobe.com/is/image",
   "contenturl" : "https://demos-pub.assetsadobe.com/",
   "config" : "/etc/dam/presets/viewer/Video",
   "config2": "/etc/dam/presets/analytics",
   "videoserverurl": "https://gateway-na.assetsadobe.com/DMGateway/public/demoCo",
   "posterimage": "/content/dam/marketing/shoppable-video/john-lewis/shoppable-video-john-lewis-2014.mp4",
   "asset" : "/content/dam/marketing/shoppable-video/john-lewis/shoppable-video-john-lewis-2014.mp4" }
 }).init();
</script>
```

統合は、ビデオ埋め込みコードを削除し、Experience Managerからインタラクティブビデオ埋め込みコードに置き換えるだけで簡単です。 次の URL で結果を確認できます。ページにインタラクティブビデオが表示される間、まだ既存のクイック表示に統合されていません。

[https://marketing.adobe.com/resources/help/en_US/dm/shoppable-video/john-lewis/landing-1.html](https://marketing.adobe.com/resources/help/en_US/dm/shoppable-video/john-lewis/landing-1.html)

## インタラクティブビデオと既存のクイック表示の統合{#integrating-an-interactive-video-with-an-existing-quickview}

>[!NOTE]
このタスクは、スタンドアロンのExperience Managerアセットをお使いの場合にのみ適用されます。

このプロセスの最後の手順は、インタラクティブビデオを、Webサイトで使用されている既存のクイック表示実装と統合することです。 すべてのケースで機能する統合のソリューションはありません。クイック表示の実装はすべて一意です。 そのため、フロントエンドのIT担当者の支援を必要とする具体的なアプローチが必要です。

既存のクイック表示の実装は、通常、Webページ上で発生する相互に関連するアクションのチェーンを次の順序で表します。

1. ユーザーは、Web サイトのユーザーインターフェイス内で、特定の要素を起動します。
1. フロントエンドコードは、手順1でトリガーされた表示インターフェイス要素に基づいて、クイックユーザーURLを取得します。
1. フロントエンドコードは、手順 2 で取得した URL を使用して AJAX リクエストを送信します。
1. バックエンドロジックは、対応するクイック表示データまたはコンテンツをフロントエンドコードに返します。
1. フロントエンドコードは、クイック表示のデータまたはコンテンツを読み込みます。
1. 必要に応じて、フロントエンドコードは、読み込まれたクイック表示データをHTML表現に変換します。
1. フロントエンドコードは、モーダルダイアログボックスまたはパネルを表示し、エンドユーザー向けに、画面上に HTML コンテンツをレンダリングします。

これらの呼び出しは、任意の手順からWebページロジックによって呼び出すことのできる、独立したパブリックAPI呼び出しを表すものではありません。 むしろ、次の手順がすべて前の手順の最終フェーズ（コールバック）に潜むような連鎖的な呼び出しになっています。

インタラクティブビデオがステップ1を置き換えるのと同時に、ステップ2の一部が、ユーザがインタラクティブビデオ内のサムネールをタップすると、ユーザインタラクションがビューアによって処理されます。 ビューアは、Experience Managerに以前に追加されたすべてのサムネールデータを含むイベントをWebページに返します。

そのようなイベントハンドラーでは、フロントエンドコードは次の処理を実行します。

* インタラクティブビデオから送出されるイベントをリッスンします。
* サムネールデータに基づいてクイック表示URLを作成します。
* クイック表示をバックエンドから読み込み、表示用に画面にレンダリングするプロセスをトリガーします。

また、インタラクティブビデオビューアでは、全画面操作モードもサポートされます。エンドユーザは、フルスクリーンを閉じずにサムネールをクリックして、クイック表示をトリガーできます。 この機能を実現するには、クイック表示モーダルダイアログボックスがビューアのコンテナに接続されるように、フロントエンドコードを変更します。 ドキュメントの Body またはその他の Web ページ要素（ビューアが全画面モードになっているときに使用できない）を追加しないでください。このジョブを実行するコードは、ビューアがページに読み込まれた後に送信される、1つ以上のビューアコールバックをリッスンします。

Experience Managerが返す埋め込みコードには、既に使用可能なイベントハンドラーが割り当てられています。 次のハイライトされたコードスニペットのように、コメントアウトされています。

```xml
<style type="text/css">
 #s7interactivevideo_div.s7interactivevideoviewer{
   width:100%;
   height:auto;
 }
</style>
<script type="text/javascript" src="https://demos-pub.assetsadobe.com/etc/dam/viewers/s7viewers/html5/js/InteractiveVideoViewer.js"></script>

<div id="s7interactivevideo_div"></div>
<script type="text/javascript">
 var s7interactivevideoviewer = new s7viewers.InteractiveVideoViewer({
  "containerId" : "s7interactivevideo_div",
  "params" : {
   "serverurl" : "https://adobedemo62-h.assetsadobe.com/is/image",
   "contenturl" : "https://demos-pub.assetsadobe.com/",
   "config" : "/etc/dam/presets/viewer/Shoppable_Video_light",
   "config2": "/etc/dam/presets/analytics",
   "videoserverurl": "https://gateway-na.assetsadobe.com/DMGateway/public/demoCo",
   "interactivedata": "content/dam/_VTT/marketing/shoppable-video/john-lewis/shoppable-video-john-lewis-2014.mp4.svideo.vtt",
   "VideoPlayer.contenturl": "https://adobedemo62-h.assetsadobe.com/is/content",
   "asset" : "/content/dam/marketing/shoppable-video/john-lewis/shoppable-video-john-lewis-2014.mp4" }
 })
 /* // Example of interactive video event for quickview.
   s7interactivevideoviewer.setHandlers({
   "quickViewActivate": function(inData) {
     var sku=inData.sku; //SKU for product ID
    //To pass other parameter from the hotspot, you need to add custom parameter during the hotspot setup as parameterName=value
    loadQuickView(sku); //Replace this call with your quickview plugin
    //Please refer to your quickviewer plugin for the quickview call
    },
"initComplete":function() {
    //--- Attach quickview popup to viewer container so popup will work in fullscreen mode ---
    var popup = document.getElementById('quickview_div'); // get custom quickview container
    popup.parentNode.removeChild(popup); // remove it from current DOM
    var sdkContainerId = s7interactivevideoviewer.getComponent("container").getInnerContainerId(); // get viewer container component
    var inner_container = document.getElementById(sdkContainerId);
    inner_container.appendChild(popup); //Attach custom quickview container to viewer
    }
   });
 */
 s7interactivevideoviewer.init();
</script>
```

そのため、必要な処理は、このハイライトされたコードスニペットのコメントアウトを解除し、ダミーのハンドラー本体を、特定の Web ページ専用のコードに置き換えることだけです。

標準の埋め込みコードには、2 つのデフォルトコールバックハンドラー、`quickViewActivate` と `initComplete` が含まれています。`quickViewActivate` ハンドラーがトリガーされるのは、ビューアでサムネールがクリックされるときです。これを使用して、ビューアをクイック表示アクティベーションロジックと統合します。 `initComplete` ハンドラーは、ビューアがページに読み込まれるときに 1 回だけトリガーされます。このハンドラは、WebページのDOM内のクイック表示ダイアログボックスの位置を調整するために使用されます。

クイック表示URLを作成するプロセスは、このトピックで前述したサムネール変数を識別するプロセスとは逆です。 以前に識別したクイック表示URLの例を使用して、各ケースでのクイック表示URLの構成を確認できます。

<table>
  <tbody>
  <tr>
    <td><p>単一の SKU（クエリ文字列内）</p> </td>
    <td><code class="code">s7interactivevideoviewer.setHandlers({
      "quickViewActivate": function(inData) {
      var quickViewUrl = "https://server/json?productId=" + inData.sku + "&amp;source=100";
      },
      });</code></td>
  </tr>
  <tr>
    <td>単一の SKU（URL パス内）</td>
    <td><code class="code">s7interactivevideoviewer.setHandlers({
      "quickViewActivate": function(inData) {
      var quickViewUrl = "https://server/product/" + inData.sku;
      },
      });</code></td>
  </tr>
  <tr>
    <td><p>SKU とカテゴリ ID（クエリ文字列内）</p> </td>
    <td><code class="code">s7interactivevideoviewer.setHandlers({
      "quickViewActivate": function(inData) {
      var quickViewUrl = "https://server/quickView/product/?category=" + inData.categoryId + "&amp;prodId=" + inData.sku;
      },
      });</code></td>
  </tr>
  </tbody>
</table>

クイック表示URLをトリガーし、クイック表示パネルをアクティブにする最後の手順は、おそらく、IT部門のフロントエンドIT担当者の支援が必要です。ユーザーは、クイック表示の導入を正確にトリガーする方法を最もよく理解し、使いやすいクイック表示URLを適切な手順から取得できます。

これらの手順がデモWebサイトにどのように適用され、インタラクティブビデオとクイック表示コードを完全に統合しているかを確認できます。 このトピックで前述したように、クイック表示URLの構造は次のようになっています。

```xml
/datafeed/$CategoryId$-$SKU$.json
```

この URL は `quickViewActivate` ハンドラー内で簡単に再構成できます。次のように、ビューアのコードを介してハンドラーに渡される `categoryId` オブジェクト内の `sku` フィールドと `inData` フィールドを使用します。

```xml
var sku=inData.sku;
var categoryId=inData.categoryId;
var quickViewUrl = "datafeed/" + categoryId + "-" + sku + ".json";
```

デモのWebサイトは、単純な`loadQuickView()`関数呼び出しを使用してクイック表示ダイアログボックスをトリガしています。 この関数は、1つの引数(クイック表示データURL)しか取りません。 インタラクティブビデオを統合する最後の手順は、次のコード行を`quickViewActivate`ハンドラーに追加することです。

```xml
loadQuickView(quickViewUrl);
```

最後に、クイック表示ダイアログボックスがビューアのコンテナ要素に接続されていることを確認します。 デフォルトの埋め込みコードにはこの機能を実現するためのサンプルステップが含まれています。ビューアのコンテナ要素への参照を取得するには、次のコード行を使用できます。

```xml
var sdkContainerId = s7interactivevideoviewer.getComponent("container").getInnerContainerId(); // get viewer container component
var inner_container = document.getElementById(sdkContainerId);
```

ここで、`inner_container` が、ビューアによって管理される `DIV` 要素への参照です。ダイアログボックスをこの `DIV` の子にしようとしています。

モーダルダイアログボックス要素を実際に見つけて、上記のコンテナにアタッチする手順は、大文字と小文字が異なります。 必要なクイック表示の実装に詳しいフロントエンド開発者にお問い合わせください。

サンプルのWebサイトでは、クイック表示モーダルダイアログボックスが`DIV`として実装され、quickview-modal IDがドキュメント`BODY`に直接割り当てられています。 このため、このダイアログをビューアのコンテナに移動するコードは、次のとおり単純です。

```xml
var sdkContainerId = s7interactivevideoviewer.getComponent("container").getInnerContainerId(); // get viewer container component
var inner_container = document.getElementById(sdkContainerId);
inner_container.appendChild(document.getElementById("quickview-modal"));
```

完全なソースコードは以下のようになります。

```xml
<style type="text/css">
 #s7interactivevideo_div.s7interactivevideoviewer{
   width:100%;
   height:auto;
 }
</style>
<script type="text/javascript" src="https://demos-pub.assetsadobe.com/etc/dam/viewers/s7viewers/html5/js/InteractiveVideoViewer.js"></script>

<div id="s7interactivevideo_div"></div>
<script type="text/javascript">
 var s7interactivevideoviewer = new s7viewers.InteractiveVideoViewer({
  "containerId" : "s7interactivevideo_div",
  "params" : {
   "serverurl" : "https://adobedemo62-h.assetsadobe.com/is/image",
   "contenturl" : "https://demos-pub.assetsadobe.com/",
   "config" : "/etc/dam/presets/viewer/Shoppable_Video_light",
   "videoserverurl": "https://gateway-na.assetsadobe.com/DMGateway/public/demoCo",
   "interactivedata": "content/dam/_VTT/marketing/shoppable-video/john-lewis/shoppable-video-john-lewis-2014.mp4.svideo.vtt",
   "VideoPlayer.contenturl": "https://adobedemo62-h.assetsadobe.com/is/content",
   "asset" : "/content/dam/marketing/shoppable-video/john-lewis/shoppable-video-john-lewis-2014.mp4" }
 })
 // Example of interactive video event for quickview.
   s7interactivevideoviewer.setHandlers({
   "quickViewActivate": function(inData) {
     var sku=inData.sku; //SKU for product ID
     var categoryId=inData.categoryId; //categoryId
    var quickViewUrl = "datafeed/" + categoryId + "-" + sku + ".json";
    loadQuickView(quickViewUrl);
    },
   "initComplete":function() {
    //--- Attach quickview popup to viewer container so popup will work in fullscreen mode ---
    var sdkContainerId = s7interactivevideoviewer.getComponent("container").getInnerContainerId(); // get viewer container component
    var inner_container = document.getElementById(sdkContainerId);
    inner_container.appendChild(document.getElementById("quickview-modal"));
    }
   });
 s7interactivevideoviewer.init();
</script>
```

インタラクティブビデオが完全に統合された最終的なデモ Web サイトは次のようになります。

[https://marketing.adobe.com/resources/help/en_US/dm/shoppable-video/john-lewis/landing-3.html](https://marketing.adobe.com/resources/help/en_US/dm/shoppable-video/john-lewis/landing-3.html)

## クイック表示を使用したカスタムポップアップウィンドウの作成{#using-quickviews-to-create-custom-pop-ups}

「[クイック表示を使用したカスタムポップアップウィンドウの作成](/help/assets/dynamic-media/custom-pop-ups.md)」を参照してください。
—>
