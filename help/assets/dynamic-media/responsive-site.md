---
title: レスポンシブサイト用に最適化された画像の配信
description: レスポンシブコード機能を使用して、最適化された画像を Dynamic Media から配信する方法を説明します。
contentOwner: Rick Brough
feature: Asset Management
role: User
exl-id: 62af6f3f-9c86-44ad-870d-140f572f99c5
source-git-commit: c82f84fe99d8a196adebe504fef78ed8f0b747a9
workflow-type: tm+mt
source-wordcount: '378'
ht-degree: 92%

---

# レスポンシブサイト用に最適化された画像の配信 {#delivering-optimized-images-for-a-responsive-site}

<table>
    <tr>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i> 新規 </i></sup>Dynamic Media Prime<a href="/help/assets/dynamic-media/dm-prime-ultimate.md"><b>Ultimate</b></a>
        </td>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i> 新規 </i></sup> <a href="/help/assets/assets-ultimate-overview.md"><b>AEM AssetsUltimate</b></a>
        </td>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i> 新規 </i></sup> <a href="/help/assets/integrate-aem-assets-edge-delivery-services.md"><b>AEM AssetsとEdge Delivery Servicesの統合 </b></a>
        </td>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i> 新規 </i></sup><a href="/help/assets/aem-assets-view-ui-extensibility.md"><b>UI 拡張機能 </b></a>
        </td>
          <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>Dynamic Media Prime</i></sup>Ultimateの新 <a href="/help/assets/dynamic-media/enable-dynamic-media-prime-and-ultimate.md"><b> 能 </b></a>
        </td>
    </tr>
    <tr>
        <td>
            <a href="/help/assets/search-best-practices.md"><b>検索のベストプラクティス</b></a>
        </td>
        <td>
            <a href="/help/assets/metadata-best-practices.md"><b>メタデータのベストプラクティス</b></a>
        </td>
        <td>
            <a href="/help/assets/product-overview.md"><b>コンテンツハブ</b></a>
        </td>
        <td>
            <a href="/help/assets/dynamic-media-open-apis-overview.md"><b>OpenAPI 機能を備えた Dynamic Media</b></a>
        </td>
        <td>
            <a href="https://developer.adobe.com/experience-cloud/experience-manager-apis/"><b>AEM Assets 開発者向けドキュメント</b></a>
        </td>
    </tr>
</table>

レスポンシブサービング用のコードを Web 開発者と共有する場合は、レスポンシブコード機能を使用します。レスポンシブ（**[!UICONTROL RESS]**）コードをクリップボードにコピーして、Web 開発者と共有することができます。

この機能は、Web サイトがサードパーティの WCM で稼動する場合に有効です。ただし、Web サイトが Adobe Experience Manager で稼動する場合は、オフサイトの画像サーバーが画像をレンダリングして Web ページに提供します。

[Web ページへのビデオビューアの埋め込み](embed-code.md)も参照してください。

[Web アプリケーションへの URL のリンク](linking-urls-to-yourwebapplication.md)も参照してください。

**レスポンシブサイトに最適化された画像を配信するには：**

1. レスポンシブコードを提供する画像の場所に移動して、ドロップダウンメニューで「**[!UICONTROL レンディション]**」を選択します。

   ![chlimage_1-408](assets/chlimage_1-408.png)

1. レスポンシブ画像プリセットを選択します。「**[!UICONTROL URL]**」ボタンと「**[!UICONTROL RESS]**」ボタンが表示されます。

   ![chlimage_1-409](assets/chlimage_1-409.png)

   >[!NOTE]
   >
   >「**[!UICONTROL URL]**」ボタンまたは「**[!UICONTROL RESS]**」ボタンを使用可能にするには、選択したアセット&#x200B;*と*&#x200B;選択した画像プリセットまたはビューアプリセットを公開する必要があります。
   >
   >画像プリセットは自動的に公開されます。

1. 「**[!UICONTROL RESS]**」を選択します。

   ![chlimage_1-410](assets/chlimage_1-410.png)

1. **[!UICONTROL レスポンシブ画像を埋め込み]**&#x200B;ダイアログボックスで、レスポンシブコードテキストを選択してコピーし Web サイトに貼り付けて、レスポンシブアセットにアクセスします。
1. 埋め込みコード内でデフォルトのブレークポイントを編集して、コード内で直接、レスポンシブ Web サイトのブレークポイントに合わせます。また、異なるページのブレークポイントで、異なる解像度の画像が配信されることをテストします。

## HTTP/2 による Dynamic Media アセットの配信 {#using-http-to-delivery-your-dynamic-media-assets}

HTTP/2 は、ブラウザーとサーバーの通信方法を改善する、新しく更新された web プロトコルです。情報の転送を高速化し、必要な処理能力を削減します。Dynamic Media アセットの配信は HTTP/2 を使用して行うことができ、応答時間と読み込み時間を短縮できます。

Dynamic Media アカウントでの HTTP/2 の使用方法について詳しくは、[コンテンツの HTTP/2 配信](http2faq.md)を参照してください。
