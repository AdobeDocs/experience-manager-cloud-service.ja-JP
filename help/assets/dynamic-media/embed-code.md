---
title: Dynamic Media ビデオビューアまたは画像ビューアを Web ページに埋め込む
description: Web ページに Dynamic Media ビデオまたは画像アセットを埋め込む方法を説明します。
contentOwner: Rick Brough
feature: Asset Management
role: User
exl-id: 76335781-e39f-4aae-967f-5af8634d8f61
source-git-commit: c82f84fe99d8a196adebe504fef78ed8f0b747a9
workflow-type: tm+mt
source-wordcount: '424'
ht-degree: 84%

---

# Web ページに Dynamic Media ビデオ、画像ビューア、またはディメンショナルビューアを埋め込む {#embedding-the-video-or-image-viewer-on-a-web-page}

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

Web ページに埋め込んでビデオを再生したりアセットを表示したりする場合は、**[!UICONTROL 埋め込みコード]** 機能を使用します。埋め込みコードをクリップボードにコピーして、Web ページに貼り付けることができます。 **[!UICONTROL 埋め込みコード]**&#x200B;ダイアログボックスでは、コードの編集はできません。

Adobe Experience Manager を WCM として使用&#x200B;_していない_&#x200B;場合に限り、URL の埋め込みを実行します。Experience Manager を WCM として使用している場合は、[ページに直接アセットを追加します。](adding-dynamic-media-assets-to-pages.md)

[Web アプリケーションに URL をリンクする](linking-urls-to-yourwebapplication.md)を参照してください。

[レスポンシブサイト用に最適化された画像を配信する](responsive-site.md)を参照してください。

>[!NOTE]
>
>埋め込みコードは、選択したアセットを公開するまではコピーできません。また、ビューアプリセットまたは画像プリセットを公開する必要もあります。
>
>[アセットを公開する](publishing-dynamicmedia-assets.md)を参照してください。
>
>[ビューアプリセットを公開する](managing-viewer-presets.md#publishing-viewer-presets)を参照してください。
>
>[画像プリセットを公開する](managing-image-presets.md#publishing-image-presets)を参照してください。

**Dynamic Media ビデオビューアまたは画像ビューアを Web ページに埋め込むには:**

1. 埋め込みコードをコピーする&#x200B;*公開済み*&#x200B;のビデオまたは画像アセットに移動します。

   埋め込みコードを使用するには、その&#x200B;*前に*&#x200B;アセットを&#x200B;*公開*&#x200B;しておく必要があります。また、ビューアプリセットまたは画像プリセットを公開する必要もあります。

   [アセットを公開する](publishing-dynamicmedia-assets.md)を参照してください。

   [ビューアプリセットを公開する](managing-viewer-presets.md#publishing-viewer-presets)を参照してください。

   [画像プリセットを公開する](managing-image-presets.md#publishing-image-presets)を参照してください。

1. 左側のレールでドロップダウンリストを選択して、「**[!UICONTROL ビューア]**」を選択します。
1. 左側のレールで、ビューアプリセット名を選択します。ビューアプリセットがアセットに適用されます。
1. 「**[!UICONTROL 埋め込む]**」を選択します。
1. **[!UICONTROL 埋め込みコード]**&#x200B;ダイアログボックスで、コード全体をクリップボードにコピーしてから、「**[!UICONTROL 閉じる]**」を選択します。
1. 埋め込みコードを Web ページに貼り付けます。

## HTTP/2 を使用した Dynamic Media アセットを配信する {#using-http-to-deliver-your-dynamic-media-assets}

HTTP/2 は、ブラウザーとサーバーの通信方法を改善する、新しく更新された web プロトコルです。情報の転送を高速化し、必要な処理能力を削減します。Dynamic Media アセットの配信は HTTP/2 を使用して行うことができ、応答時間と読み込み時間を短縮できます。

Dynamic Media アカウントでの HTTP/2 の使用方法について詳しくは、[コンテンツの HTTP/2 配信](http2faq.md)を参照してください。
