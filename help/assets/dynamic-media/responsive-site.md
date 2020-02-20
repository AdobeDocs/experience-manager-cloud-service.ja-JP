---
title: レスポンシブサイト用に最適化された画像の配信
description: レスポンシブコード機能を使用して、最適化された画像を配信する方法
translation-type: tm+mt
source-git-commit: d6e92a433e61c2a959c62080fcd52fe0ebe67c4f

---


# レスポンシブサイト用に最適化された画像の配信 {#delivering-optimized-images-for-a-responsive-site}

レスポンシブサービング用のコードを Web 開発者と共有する場合は、レスポンシブコード機能を使用します。You copy the responsive (**[!UICONTROL RESS]**) code to the clipboard so you can share it with the web developer.

この機能は、Web サイトがサードパーティの WCM で稼動する場合に有効です。ただし、Web サイトが AEM で稼働する場合は、オフサイトの画像サーバーが画像をレンダリングして Web ページに提供します。

[Web ページへのビデオビューアの埋め込み](embed-code.md)も参照してください。

[Web アプリケーションへの URL のリンク](linking-urls-to-yourwebapplication.md)も参照してください。

**レスポンシブサイト用に最適化された画像を配信するには**:

1. Navigate to the image you want supply responsive code for and in the drop-down menu, tap **[!UICONTROL Renditions]**.

   ![chlimage_1-408](assets/chlimage_1-408.png)

1. レスポンシブ画像プリセットを選択します。The **[!UICONTROL URL]** and **[!UICONTROL RESS]** buttons appear.

   ![chlimage_1-409](assets/chlimage_1-409.png)

   >[!NOTE]
   >
   >The selected asset *and* the selected image preset or viewer preset must be published to make the **[!UICONTROL URL]** or **[!UICONTROL RESS]** buttons available.
   >
   >画像プリセットは自動的に公開されます。

1. 「RESS」をタ **[!UICONTROL ップします]**。

   ![chlimage_1-410](assets/chlimage_1-410.png)

1. レスポンシブ **[!UICONTROL 画像を埋め込みダイアログボックスで]** 、レスポンシブコードテキストを選択してコピーし、Webサイトに貼り付けて、レスポンシブアセットにアクセスします。
1. 埋め込みコード内でデフォルトのブレークポイントを編集して、コード内で直接、レスポンシブ Web サイトのブレークポイントに合わせます。また、異なるページのブレークポイントで、異なる解像度の画像が配信されることをテストします。

## HTTP/2 による Dynamic Media アセットの配信 {#using-http-to-delivery-your-dynamic-media-assets}

HTTP/2 は、ブラウザーとサーバーの交信を強化する、新しく更新された Web プロトコルです。このプロトコルを使用すれば、情報の伝送を高速化し、必要な処理能力を抑えることができます。Dynamic Media アセットの配信は HTTP/2 を使用しておこなうことができ、応答時間と読み込み時間を短縮できます。

Dynamic Media アカウントでの HTTP/2 の使用方法について詳しくは、[コンテンツの HTTP2 配信](http2faq.md)を参照してください。
