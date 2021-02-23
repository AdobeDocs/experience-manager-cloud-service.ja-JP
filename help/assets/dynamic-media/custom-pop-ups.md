---
title: クイック表示を使用したカスタムポップアップの作成
description: デフォルトのクイック表示はeコマースエクスペリエンスで使用され、eコマースエクスペリエンスでは、購入を促すために製品情報と共にポップアップが表示されます。 このようなポップアップにカスタムコンテンツが表示されるように設定できます。
translation-type: tm+mt
source-git-commit: ad626d9722f1942249197d96aa5fac3d8f7ed947
workflow-type: tm+mt
source-wordcount: '1023'
ht-degree: 39%

---


# クイック表示を使用したカスタムポップアップウィンドウの作成{#using-quickviews-to-create-custom-pop-ups}

デフォルトのクイック表示はeコマースエクスペリエンスで使用され、eコマースエクスペリエンスでは、購入を促すために製品情報と共にポップアップが表示されます。 ただし、このようなポップアップにカスタムコンテンツが表示されるように設定できます。使用するビューアに応じて、ユーザーはホットスポット、サムネール画像、画像マップをタップして、情報や関連するコンテンツを表示できます。

クイック表示は、Dynamic Mediaの次のビューアでサポートされています。

* インタラクティブ画像（クリック可能なホットスポット）
* インタラクティブビデオ（ビデオの再生中にクリック可能なサムネール画像）
* カルーセルバナー（クリック可能なホットスポットまたは画像マップ）

各ビューアの機能は異なりますが、クイック表示の作成プロセスは、サポートされる3つのビューアすべてで同じです。

**クイック表示を使用してカスタムポップアップウィンドウを作成するには**

1. アップロードしたアセットのクイック表示を作成する。

   通常、クイック表示は、使用しているビューアで使用するアセットを編集するのと同時に作成します。

   <table>
    <tbody>
    <tr>
    <td><strong>使用しているビューア</strong></td>
    <td><strong>クイック表示を作成するには、次の手順を実行します</strong></td>
    </tr>
    <tr>
    <td>インタラクティブ画像</td>
    <td><a href="/help/assets/dynamic-media/interactive-images.md#adding-hotspots-to-an-image-banner" target="_blank">画像バナーへのホットスポットの追加</a></td>
    </tr>
    <tr>
    <td>インタラクティブビデオ</td>
    <td><a href="/help/assets/dynamic-media/interactive-videos.md#adding-interactivity-to-your-video" target="_blank">ビデオへのインタラクティブ機能の追加</a>.</td>
    </tr>
    <tr>
    <td>カルーセルバナー</td>
    <td><a href="/help/assets/dynamic-media/carousel-banners.md#adding-hotspots-or-image-maps-to-an-image-banner" target="_blank">バナーへのホットスポットまたは画像マップの追加</a><br /> </td>
    </tr>
    </tbody>
   </table>

1. ビューアの埋め込みコードを取得し、Web サイトにビューアを統合します。

   <table>
    <tbody>
    <tr>
    <td><strong>使用しているビューア</strong><br /> </td>
    <td><strong>ViewerをWebサイトに統合するには、次の手順を実行します</strong></td>
    </tr>
    <tr>
    <td>インタラクティブ画像</td>
    <td><a href="/help/assets/dynamic-media/interactive-images.md#integrating-an-interactive-image-with-your-website" target="_blank">インタラクティブ画像の Web サイトへの統合</a>.<br /> </td>
    </tr>
    <tr>
    <td>インタラクティブビデオ<br /> </td>
    <td><a href="/help/assets/dynamic-media/interactive-videos.md#integrating-an-interactive-video-with-your-website" target="_blank">インタラクティブビデオの Web サイトへの統合</a>.<br /> </td>
    </tr>
    <tr>
    <td>カルーセルバナー</td>
    <td><a href="/help/assets/dynamic-media/carousel-banners.md#adding-a-carousel-banner-to-your-website-page" target="_blank">Web サイトページへのカルーセルバナーの追加</a>.<br /> </td>
    </tr>
    </tbody>
   </table>

1. 使用するViewerは、クイック表示の使用方法を知っている必要があります。

   ビューアは`QuickViewActive`という名前のハンドラを使用します。

   **例** Web ページでインタラクティブ画像用に以下のサンプル埋め込みコードを使用しているとします。

   ![chlimage_1-291](assets/chlimage_1-291.png)

   ハンドラーは `setHandlers` を使用してビューアに読み込まれます。

   `*viewerInstance*.setHandlers({ *handler 1*, *handler 2*}, ...`

   **上述のサンプル埋め込みコードの例を使用した場合、次のコードがあります。**

   ```xml
   s7interactiveimageviewer.setHandlers({
       quickViewActivate": function(inData) {
           var sku=inData.sku;
           var genericVariable1=inData.genericVariable1;
           var genericVariable2=inData.genericVariable2;
          loadQuickView(sku,genericVariable1,genericVariable2);
       }
   })
   ```

   `setHandlers()` メソッドについて詳しくは、以下を参照してください。

   * インタラクティブ画像ビューア：[sethandlers](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/viewers-for-aem-assets-only/interactive-images/jsapi-interactive-image/r-html5-aem-int-image-viewer-javascriptapiref-sethandlers.html)
   * インタラクティブビデオビューア：[sethandlers](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/viewers-for-aem-assets-only/interactive-video/jsapi-interactive-video/r-html5-aem-int-video-javascriptapiref-sethandlers.html)

1. 次に`quickViewActivate`ハンドラを設定します。

   `quickViewActivate`ハンドラは、ビューアのクイック表示を制御します。 ハンドラーには、クイック表示で使用する変数リストと関数呼び出しが含まれます。 埋め込みコードは、クイック表示で設定されたSKU変数のマッピングを提供します。 また、サンプルの`loadQuickView`関数呼び出しも行います。

   **Webページで使用する変数**
mappingMap変数と、クイック表示に含まれるSKU値と汎用変数：

   `var *variable1*= inData.*quickviewVariable*`

   提供された埋め込みコードには、SKU 変数用のサンプルマッピングが含まれています。

   `var sku=inData.sku`

   クイック表示から他の変数もマッピングします。次に例を示します。

   ```
   var <i>variable2</i>= inData.<i>quickviewVariable2</i>
    var <i>variable3</i>= inData.<i>quickviewVariable3</i>
   ```

   **関数の**
呼び出しこのハンドラには、クイック表示が動作するための関数の呼び出しも必要です。この関数は、ホストページからアクセスできることが前提となります。埋め込みコードは、サンプル関数呼び出しを提供します。

   `loadQuickView(sku)`

   このサンプル関数呼び出しは、関数 `loadQuickView()` が存在しアクセス可能であることが前提となります。

   `quickViewActivate` メソッドについて詳しくは、以下を参照してください。

   * インタラクティブ画像ビューア ‐ [イベントコールバック](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/viewers-for-aem-assets-only/interactive-images/c-html5-aem-interactive-image-event-callbacks.html)
   * インタラクティブビデオビューア ‐ [イベントコールバック](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/viewers-for-aem-assets-only/interactive-video/c-html5-aem-int-video-event-callbacks.html)
   * インタラクティブビデオビューアでのインタラクティブデータのサポート ‐ [インタラクティブデータのサポート](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/viewers-for-aem-assets-only/interactive-video/c-html5-aem-int-video-int-data-support.html)

1. 以下の操作を実行してください。

   * 埋め込みコードの setHandlers セクションのコメントアウトを解除します。
   * クイック表示に含まれるその他の変数をマップします。

      * 変数を追加する場合は、`loadQuickView(sku,*var1*,*var2*)`呼び出しを更新します。
   * ビューア外でページにシンプルな `loadQuickView` () 関数を作成します。

      例えば、次の例では、SKUの値がブラウザーコンソールに書き込まれます。

   ```xml
   function loadQuickView(sku){
       console.log ("quickview sku value is " + sku);
   }
   ```

   * Web サーバーにテスト HTML ページをアップロードし、開きます。

      クイック表示の変数がマッピングされます。 関数の呼び出しが正しく行われている。 また、ブラウザコンソールは変数値をブラウザコンソールに書き込みます。 これは、提供されたサンプル関数を使用して行います。



1. クイック表示で単純なポップアップを呼び出す関数を使用できるようになりました。 以下の例では、ポップアップに `DIV` を使用しています。
1. ポップアップの `DIV` を以下のようなスタイルにします。必要に応じ追加て追加のスタイル設定を行います。

   ```xml
   <style type="text/css">
       #quickview_div{
           position: absolute;
           z-index: 99999999;
           display: none;
       }
   </style>
   ```

1. HTML ページのボディにポップアップの `DIV` を配置します。

   要素の1つにIDが設定され、SKU値で更新されたIDは、ユーザーがクイック表示を呼び出したときに使用されます。 この例にはこれに加え、ポップアップを表示後に再び隠すための単純なボタンも含まれています。

   ```xml
   <div id="quickview_div" >
       <table>
           <tr><td><input id="btnClosePopup" type="button" value="Close"        onclick='document.getElementById("quickview_div").style.display="none"' /><br /></td></tr>
           <tr><td>SKU</td><td><input type="text" id="txtSku" name="txtSku"></td></tr>
       </table>
   </div>
   ```

1. ポップアップウィンドウでSKU値を更新するには、関数を追加します。 手順5で作成した単純な関数を次のように置き換えて、ポップアップウィンドウを表示します。

   ```xml
   <script type="text/javascript">
       function loadQuickView(sku){
           document.getElementById("txtSku").setAttribute("value",sku); // write sku value
           document.getElementById("quickview_div").style.display="block"; // show popup
       }
   </script>
   ```

1. Web サーバーにテスト HTML ページをアップロードし、開きます。ユーザがクイック表示を呼び出すと、ビューアにポップアップ`DIV`が表示されます。
1. **カスタムポップアップウィンドウをフルスクリーンモードで表示する方法**

   インタラクティブビデオビューアなどの一部のビューアでは、全画面表示モードでの表示をサポートしています。ただし、前の手順で説明したポップアップを使用すると、全画面表示モード中はビューアの背後に表示されるようになります。

   標準モードとフルスクリーンモードでポップアップウィンドウを表示するには、ポップアップウィンドウをビューアコンテナに接続します。 この場合は、2番目のハンドラメソッド`initComplete`を使用します。

   `initComplete`ハンドラーは、ビューアの初期化後に呼び出されます。

   ```xml
   "initComplete":function() { code block }
   ```

   `init()` メソッドについて詳しくは、以下を参照してください。

   * インタラクティブ画像ビューア ‐ [init](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/viewers-for-aem-assets-only/interactive-images/jsapi-interactive-image/r-html5-aem-int-image-viewer-javascriptapiref-init.html)
   * インタラクティブビデオビューア ‐ [init](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/viewers-for-aem-assets-only/interactive-video/jsapi-interactive-video/r-html5-aem-int-video-javascriptapiref-init.html)

1. 前の手順で言及したように、ビューアにポップアップをアタッチするには、以下のコードを使用します。

   ```xml
   "initComplete":function() {
       var popup = document.getElementById('quickview_div');
       popup.parentNode.removeChild(popup);
       var sdkContainerId = s7interactivevideoviewer.getComponent("container").getInnerContainerId();
       var inner_container = document.getElementById(sdkContainerId);
       inner_container.appendChild(popup);
   }
   ```

   上記のコードでは、次の操作を行いました。

   * カスタムポップアップウィンドウを特定。
   * DOM からの削除
   * ビューアコンテナの指定
   * ビューアコンテナへのポップアップのアタッチ

1. setHandlersコード全体は次のようになります（インタラクティブビデオビューアを使用）。

   ```xml
   s7interactivevideoviewer.setHandlers({
       "quickViewActivate": function(inData) {
           var sku=inData.sku;
           loadQuickView(sku);
   
       },
       "initComplete":function() {
           var popup = document.getElementById('quickview_div'); // get custom quick view container
           popup.parentNode.removeChild(popup); // remove it from current DOM
           var sdkContainerId = s7interactivevideoviewer.getComponent("container").getInnerContainerId();
           var inner_container = document.getElementById(sdkContainerId);
           inner_container.appendChild(popup);
       }
   });
   ```

1. ハンドラーを読み込んだ後で、ビューアを初期化します。

   `*viewerInstance.*init()`

   **例**：この例では、インタラクティブ画像ビューアを使用します。

   `s7interactiveimageviewer.init()`

   ビューアをホストページに埋め込んだ後は、必ずビューアインスタンスを作成してください。 また、`init()`を使用してビューアを呼び出す前に、ハンドラーが読み込まれていることを確認してください。

