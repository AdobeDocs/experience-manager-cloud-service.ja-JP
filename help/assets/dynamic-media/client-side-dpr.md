---
title: クライアントサイドのデバイスピクセル比（DPR）を使用したスマートイメージングについて
description: Dynamic Media を含む Adobe Experience Manager as a Cloud Service のスマートイメージングでクライアントサイドのデバイスピクセル比を使用する方法について説明します。
contentOwner: Rick Brough
feature: Device Pixel Ratio,Smart Imaging
role: Admin,User
exl-id: 556710c7-133c-487a-8cd9-009a5912e94c
source-git-commit: c82f84fe99d8a196adebe504fef78ed8f0b747a9
workflow-type: tm+mt
source-wordcount: '368'
ht-degree: 92%

---

# クライアントサイドのデバイスピクセル比（DPR）を使用したスマートイメージングについて {#client-side-dpr}

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

現在のスマートイメージングソリューションでは、ユーザーエージェント文字列を使用して、使用されているデバイスのタイプ（デスクトップ、タブレット、モバイルなど）を判断します。

特に Apple デバイスでは、デバイス検出機能（ユーザーエージェント文字列に基づく DPR）が不正確な場合がよくあります。また、新しいデバイスが起動されるたびに、そのデバイスを検証する必要があります。

クライアントサイド DPR では、100％ 正確な値が提供され、起動されたデバイスが Apple であるか、それ以外の新しいデバイスであるかにかかわらず、あらゆるデバイスで機能します。

<!-- See also [About network bandwidth optimization](/help/assets/dynamic-media/imaging-faq.md#network-bandwidth-optimization). -->

## クライアントサイド DPR コードの使用

**サーバーサイドでレンダリングされるアプリ**

1. HTML ページのヘッダーセクションに次のスクリプトを追加して、サービスワーカーの初期化コード（`srvinit.js`）を読み込みます。

   ```javascript
   <script type="text/javascript" src="srvinit.js"></script>
   ```

   サービスワーカーがすぐに初期化を開始するように、他のあらゆるスクリプトより&#x200B;_前_&#x200B;に、このスクリプトを読み込むことをお勧めします。

1. HTML ページの本文セクションの先頭に次の DPR 画像タグコードを追加します。

   ```html
   <img src="aem_dm_dpr_1x.jpg" style="width:1px;height:1px;display:none"
       srcset="aem_dm_dpr_1x.jpg 1x, aem_dm_dpr_1.1x.jpg 1.1x, aem_dm_dpr_1.2x.jpg 1.2x, aem_dm_dpr_1.3x.jpg 1.3x, aem_dm_dpr_1.4x.jpg 1.4x, aem_dm_dpr_1.5x.jpg 1.5x, aem_dm_dpr_1.6x.jpg 1.6x,          aem_dm_dpr_1.7x.jpg 1.7x, aem_dm_dpr_1.8x.jpg 1.8x, aem_dm_dpr_1.9x.jpg 1.9x,
       aem_dm_dpr_2x.jpg 2x, aem_dm_dpr_2.1x.jpg 2.1x, aem_dm_dpr_2.2x.jpg 2.2x, aem_dm_dpr_2.3x.jpg 2.3x, aem_dm_dpr_2.4x.jpg 2.4x, aem_dm_dpr_2.5x.jpg 2.5x, aem_dm_dpr_2.6x.jpg 2.6x, aem_dm_dpr_2.7x.jpg 2.7x, aem_dm_dpr_2.8x.jpg 2.8x, aem_dm_dpr_2.9x.jpg 2.9x,
       aem_dm_dpr_3x.jpg 3x, aem_dm_dpr_3.1x.jpg 3.1x, aem_dm_dpr_3.2x.jpg 3.2x, aem_dm_dpr_3.3x.jpg 3.3x, aem_dm_dpr_3.4x.jpg 3.4x, aem_dm_dpr_3.5x.jpg 3.5x, aem_dm_dpr_3.6x.jpg 3.6x, aem_dm_dpr_3.7x.jpg 3.7x, aem_dm_dpr_3.8x.jpg 3.8x, aem_dm_dpr_3.9x.jpg 3.9x,
       aem_dm_dpr_4x.jpg 4x, aem_dm_dpr_4.1x.jpg 4.1x, aem_dm_dpr_4.2x.jpg 4.2x, aem_dm_dpr_4.3x.jpg 4.3x, aem_dm_dpr_4.4x.jpg 4.4x, aem_dm_dpr_4.5x.jpg 4.5x, aem_dm_dpr_4.6x.jpg 4.6x, aem_dm_dpr_4.7x.jpg 4.7x, aem_dm_dpr_4.8x.jpg 4.8x, aem_dm_dpr_4.9x.jpg 4.9x,
       aem_dm_dpr_5x.jpg 5x">
   ```

   HTML ページ内のすべての静的画像より&#x200B;_前_ に、この DPR 画像タグコードを含める必要があります。

**クライアントサイドでレンダリングされるアプリ**

1. HTML ページのヘッダーセクションに次の DPR スクリプトを追加します。

   ```javascript
   <script type="text/javascript" src="srvinit.js"></script>
   <script type="text/javascript" src="dprImageInjection.js"></script>
   ```

   両方の DPR スクリプトを 1 つにまとめると、複数のネットワークリクエストになることを回避できます。

   HTML ページの他のどのスクリプトより&#x200B;_前_に、これらのスクリプトを読み込むことをお勧めします。
また、body 要素ではなく diff HTML タグでアプリをブートストラップすることをお勧めします。`dprImageInjection.js` が HTML ページの本文セクションの先頭に画像タグを動的に挿入するからです。

## JavaScript ファイルのダウンロード {#client-side-dpr-script}

ダウンロードに含まれている下記の JavaScript ファイルは、例としての参照用にのみ提供されています。これらのファイルを HTML ページで使用する場合は、各ファイルのコードを独自の要件に合うように必ず編集してください。

* `dprImageInjection.js`
* `srvinit.js`
* `srvwrk.js`

[JavaScript ファイルのダウンロード](/help/assets/dynamic-media/assets/aem-dynamicmedia-smartimaging-dpr.zip)

>[!MORELIKETHIS]
>
>* [スマートイメージング](/help/assets/dynamic-media/imaging-faq.md)
