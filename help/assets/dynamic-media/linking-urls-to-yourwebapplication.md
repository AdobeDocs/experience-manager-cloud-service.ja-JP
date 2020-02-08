---
title: Web アプリケーションへの URL のリンク
description: Dynamic Media で Web アプリケーションに URL をリンクする方法
translation-type: tm+mt
source-git-commit: 6224d193adfb87bd9b080f48937e0af1f03386d6

---


# Web アプリケーションへの URL のリンク {#linking-urls-to-your-web-application}

Webサイトやアプリケーションは、URL呼び出しを介してダイナミックメディアサービスにアクセスします。 アセットの公開後、Dynamic Media によって、そのアセットを参照する URL 文字列がアクティベートされます。これらの URL を Web ブラウザーに貼り付けてテストすることができます。

AEM を WCM として使用&#x200B;*していない*&#x200B;場合に限り、URL へのリンクを使用します。リンクと埋め込みの違いは、ビデオプレーヤーをポップアップウィンドウまたはモーダルウィンドウとして配信する場合に使用します。 AEM を WCM として使用している場合は、[ページに直接アセットを追加します。](adding-dynamic-media-assets-to-pages.md)

Web ページやアプリケーションにこれらの URL 文字列を配置するには、Dynamic Media からコピーします。

>[!NOTE]
>
>URL 文字列は、アセットの動的レンディションでのみ使用できます。現時点では、Dynamic Media サーバーではなく DAM に存在する静的アセットには URL 文字列を使用できません。静的なレンディションに対しては「URL」ボタンが表示されません。

[Web ページへのビデオビューアまたは画像ビューアの埋め込み](embed-code.md)も参照してください。

[Web アプリケーションへの YouTube URL のリンク](video.md)も参照してください。

[レスポンシブサイト用に最適化された画像の配信](responsive-site.md)も参照してください。

[アセットのアップロード ](/help/assets/manage-digital-assets.md#uploading-assets)も参照してください。

## アセットの URL の取得 {#obtaining-a-url-for-an-asset}

画像プリセットまたはビューアプリセットによって生成された URL 文字列を取得できます。URL をコピーしたらクリップボードに配置されるので、必要に応じて Web サイトのページまたはアプリケーションに貼り付けることができます。

>[!NOTE]
>
>URL は、選択したアセットを公開するまではコピーできません。また、ビューアプリセットまたは画像プリセットを公開する必要もあります。
>
>[アセットの公開](publishing-dynamicmedia-assets.md)を参照してください。
>
>[ビューアプリセットの公開](managing-viewer-presets.md#publishing-viewer-presets)を参照してください。
>
>[画像プリセットの公開](managing-image-presets.md#publishing-image-presets)を参照してください。

URL 文字列を取得するには複数の方法があります。以下の手順では、使用できる方法の 1 つを紹介します。

**アセットのURLを取得するには**

1. Navigate to the *published* asset whose image preset URL or viewer preset URL you want to copy, and tap the asset to open it.

   URL をコピーするには、その前にアセットを公開しておく必要があります。****&#x200B;また、ビューアプリセットまたは画像プリセットを公開する必要もあります。

   [アセットの公開](publishing-dynamicmedia-assets.md)を参照してください。

   [ビューアプリセットの公開](managing-viewer-presets.md#publishing-viewer-presets)を参照してください。

   [画像プリセットの公開](managing-image-presets.md#publishing-image-presets)を参照してください。

1. 選択したアセットに応じて、次のいずれかの操作をおこないます。

   * If you selected an image, in the drop-down menu, tap **[!UICONTROL Renditions]**.

      「**[!UICONTROL 動的]**」ヘッダーの下にあるプリセット名をタップすると、右側のフレームにレンディションが表示されます。「動的」ヘッダーを表示するには、場合によってはレンディションリストをスクロールする必要があります。

      左側のレールの下部にある「**[!UICONTROL URL]**」をタップします。

      ![chlimage_1-270](assets/chlimage_1-270.png)

   * If you selected a spin set, an image set, a carousel set, or a video, in the drop-down menu, tap **[!UICONTROL Viewers]**.

      左側のレールで、ビューアプリセット名をタップします。セットまたはビデオのプレビューが別のページで開きます。

      左側のレールの下部にある「**[!UICONTROL URL]**」をタップします。

      ![chlimage_1-271](assets/chlimage_1-271.png)

1. テキストを選択し、Web ブラウザーにコピーしてアセットをプレビューするか、Web コンテンツページに追加します。

   URLウィンドウを終了するには、「 **[!UICONTROL X]** 」をタップするか、「閉じる」をタ **[!UICONTROL ップします]**。

## 静的アセットの URL の取得 {#obtaining-a-url-for-a-static-asset}

Dynamic Media は静的アセットの配信をサポートします。静的アセットとは、画像やビデオに留まらない追加アセットです。配信がサポートされる静的アセットの形式は以下のとおりです。

* アニメーション GIF
* オーディオファイル
* CSS
* JavaScript（会社が独自ドメインで設定されている場合）
* PDF
* SVG
* XML
* ZIP

**静的アセットのURLを取得するには**

1. URLをコピーする*発行済み*静的アセットに移動し、アセットをタップして開きます。

   Remember that URLs are only available to copy *after* you have first *published* the static asset.

   [アセットの公開](publishing-dynamicmedia-assets.md)を参照してください。

1. 以下のいずれかの方法で、公開済みの静的アセットの URL を取得します。

   * `The URL of the published static is the following:`

      * `https://*<server_name>*/is/content/*<company_name>*/*<static_asset_filename>*.*<extension>*`

         For example, `https://aem.com/is/content/adobe/image.gif`.
   * click **[!UICONTROL Asset > Dynamic Renditions]**, then tap a dynamic rendition of the static asset and copy the URL.

      Change the copied URL to use `is/content` in the path instead of `is/image/`.


## 公開されたビデオレンディションのビデオ URL の取得 {#obtaining-a-video-url-for-a-published-video-rendition}

1. In AEM, navigate to **[!UICONTROL Tools > Deployment > Cloud > Cloud Services]**.
1. On the **[!UICONTROL Cloud Services]** page, scroll down to the **[!UICONTROL Dynamic Media Cloud Services]** heading, then tap **[!UICONTROL Show Configurations]**.
1. Under **[!UICONTROL Available Configurations]**, tap the name of the configuration you want.

1. On the **[!UICONTROL Dynamic Media Cloud Settings]** page, under **[!UICONTROL Video Service URL]**, copy down the entire URL path. コピーした URL パスは後の手順で必要になります。

   例えば、URL パスは、次のように表示されることがあります。

   `https://s7athens.macromedia.com:9090/DMGateway/`

   （このパスは説明のために便宜的に示しています。コピーする実際のパスではありません。）

1. 「**[!UICONTROL 登録 ID]**」の下で、ID の最後の部分にある顧客名をコピーします。

   例えば、登録 ID が `87654321|MyCompany` の場合、顧客名は `MyCompany` です。

1. Near the upper-left corner of the page, tap **[!UICONTROL Cloud Services**, then tap the AEM icon and navigate to **[!UICONTROL General > CRXDE Lite]**.
1. JCR（Java コンテンツリポジトリ）のビデオレンディションパス全体をコピーします。

   例えば、ビデオのレンディションパスは、次のように表示されることがあります。

   `/_renditions_/0bd/0bd28743-a616-4fe6-92aa-6eae7c2112f/avs/Momentum_1080-0x720-2600k.mp4`

   （このパスは説明のために便宜的に示しています。コピーする実際のパスではありません。）

1. コピーした情報を次の順序に並べて、完全な URL パスを作成します。

   `<Video_Service_URL>/public/<Customer_name_from_Registration_ID>/<Video_rendition_path>`

   例えば、上記の手順で示したパス例と顧客名の例を使用すると、完全パスは次のように表示されます。

   `https://s7athens.macromedia.com:9090/DMGateway/public/MyCompany/_renditions_/0bd/0bd28743-a616-4fe6-92aa-6eae7c2112ff/avs/Momentum_1080-0x720-2600k.mp4`

   これは、公開されたビデオレンディションの完全なビデオ URL です。

## アダプティブストリーミング（HLS）用のビデオ URL の取得 {#obtaining-a-video-url-for-adaptive-streaming-hls}

1. In AEM, navigate to **[!UICONTROL Tools > Deployment > Cloud > Cloud Services]**.
1. On the **[!UICONTROL Cloud Services]** page, scroll down to the **[!UICONTROL Dynamic Media Cloud Services]** heading, then tap **[!UICONTROL Show Configurations]**.
1. Under **[!UICONTROL Available Configurations]**, tap the name of the configuration you want.
1. On the **[!UICONTROL Dynamic Media Cloud Services Settings]** page, do the following:

   * 「**[!UICONTROL ビデオサービスの URL]**」の下で、URL パス全体をコピーします。コピーした URL パスは後の手順で必要になります。例えば、URL パスは、次のように表示されることがあります。
   `https://gateway-na.assetsadobe.com/DMGateway/`

   （このパスは説明のために便宜的に示しています。コピーする実際のパスではありません。）

   * 「**[!UICONTROL 登録 ID]**」の下で、ID の最後の部分にある顧客名をコピーします。コピーした顧客名は後の手順で必要になります。

      例えば、登録 ID が `87654321|demoCo` の場合、顧客名は `demoCo` です。


1. 使用しているビデオ配信プロトコルに基づいて、それぞれのプロトコルセレクターをコピーします。コピーしたプロトコルセレクターは後の手順で必要になります。

   <table>
    <tbody>
      <tr>
      <td><strong>使用しているビデオ配信プロトコル</strong></td>
      <td><strong>使用するプロトコルセレクター</strong></td>
      </tr>
      <tr>
      <td><p>HTTP</p> <p>HTTP（セキュアでないビデオ配信）を使用している場合は、前にコピーしたビデ <code>https</code> オサー <code>http</code> ビスのURL値をに変更してください。</p> </td>
      <td><code>public/</code></td>
      </tr>
      <tr>
      <td>HTTPS</td>
      <td><code>public-ssl/</code></td>
      </tr>
    </tbody>
   </table>

1. Dynamic Media で処理される AEM のビデオアセットのフルパスをコピーします。コピーしたビデオアセットのパスは後の手順で必要になります。

   次に例を示します。

   `/content/dam/marketing/MyVideo.mp4`

1. これまでの手順でコピーしたすべての要素を以下の順に組み合わせて、文字列を作成します。

   &lt; `video service URL`>&lt; `protocol selector`>&lt; `customer name`>&lt; `video asset path`>

   例えば、これまでの手順の例からコピーした情報を使用すると、以下のような文字列になります。

   `https://gateway-na.assetsadobe.com/DMGateway/public-ssl/demoCo/content/dam/marketing/MyVideo.mp4`

1. Complete the URL by appending `.m3u8` to the end of the string. For example, appending `.m3u8` to the string from the previous step, the complete URL path would appear as follows:

   `https://gateway-na.assetsadobe.com/DMGateway/public-ssl/demoCo/content/dam/marketing/MyVideo.mp4.m3u8`

## HTTP/2 を使用した Dynamic Media アセットの配信 {#using-http-to-deliver-your-dynamic-media-assets}

HTTP/2 は、ブラウザーとサーバーの交信を強化する、新しく更新された Web プロトコルです。このプロトコルを使用すれば、情報の伝送を高速化し、必要な処理能力を抑えることができます。HTTP/2 上で Dynamic Media アセットの配信が可能になり、応答時間と読み込み時間が短縮されました。

Dynamic Media アカウントでの HTTP/2 の使用方法について詳しくは、[コンテンツの HTTP2 配信](http2.md)を参照してください。
