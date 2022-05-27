---
title: クライアント側デバイスのピクセル比でのスマートイメージングの使用
description: Dynamic MediaでAdobe Experience Manager as a Cloud Serviceのスマートイメージングでクライアント側のデバイスのピクセル比を使用する方法について説明します。
role: Admin,User
source-git-commit: 1dabecfc878ad674d071fb47063326b073b0866e
workflow-type: tm+mt
source-wordcount: '323'
ht-degree: 0%

---

# クライアントサイドデバイスのピクセル比 (DPR) を使用したスマートイメージングについて {#client-side-dpr}

現在のスマートイメージングソリューションでは、ユーザーエージェント文字列を使用して、使用されているデバイス（デスクトップ、タブレット、モバイルなど）の種類を判断します。

特にAppleデバイスでは、デバイス検出機能（ユーザーエージェント文字列に基づく DPR）が不正確な場合が多くあります。 また、新しいデバイスが起動されるたびに、そのデバイスを検証する必要があります。

クライアント側の DPR では、100%の正確な値が提供され、Appleか、それ以外の新しいデバイスが起動されたかに関わらず、あらゆるデバイスで機能します。

<!-- See also [About network bandwidth optimization](/help/assets/dynamic-media/imaging-faq.md#network-bandwidth-optimization). -->

## クライアント側の DPR コードを使用する

**サーバーサイドレンダリングアプリ**

1. サービスワーカーの初期 (`srvinit.js`) を使用する場合は、次のスクリプトをHTMLページのヘッダーセクションに追加します。

   ```javascript
   <script type="text/javascript" src="srvinit.js"></script>
   ```

   Adobeでは、このスクリプトを読み込むことをお勧めします _前_ サービスワーカーがすぐに初期化を開始するための他のスクリプト。

1. 次の DPR イメージタグコードを、タグページの body セクションの上部にHTMLします。

   ```html
   <img src="aem_dm_dpr_1x.jpg" style="width:1px;height:1px;display:none"
       srcset="aem_dm_dpr_1x.jpg 1x, aem_dm_dpr_1.1x.jpg 1.1x, aem_dm_dpr_1.2x.jpg 1.2x, aem_dm_dpr_1.3x.jpg 1.3x, aem_dm_dpr_1.4x.jpg 1.4x, aem_dm_dpr_1.5x.jpg 1.5x, aem_dm_dpr_1.6x.jpg 1.6x,          aem_dm_dpr_1.7x.jpg 1.7x, aem_dm_dpr_1.8x.jpg 1.8x, aem_dm_dpr_1.9x.jpg 1.9x,
       aem_dm_dpr_2x.jpg 2x, aem_dm_dpr_2.1x.jpg 2.1x, aem_dm_dpr_2.2x.jpg 2.2x, aem_dm_dpr_2.3x.jpg 2.3x, aem_dm_dpr_2.4x.jpg 2.4x, aem_dm_dpr_2.5x.jpg 2.5x, aem_dm_dpr_2.6x.jpg 2.6x, aem_dm_dpr_2.7x.jpg 2.7x, aem_dm_dpr_2.8x.jpg 2.8x, aem_dm_dpr_2.9x.jpg 2.9x,
       aem_dm_dpr_3x.jpg 3x, aem_dm_dpr_3.1x.jpg 3.1x, aem_dm_dpr_3.2x.jpg 3.2x, aem_dm_dpr_3.3x.jpg 3.3x, aem_dm_dpr_3.4x.jpg 3.4x, aem_dm_dpr_3.5x.jpg 3.5x, aem_dm_dpr_3.6x.jpg 3.6x, aem_dm_dpr_3.7x.jpg 3.7x, aem_dm_dpr_3.8x.jpg 3.8x, aem_dm_dpr_3.9x.jpg 3.9x,
       aem_dm_dpr_4x.jpg 4x, aem_dm_dpr_4.1x.jpg 4.1x, aem_dm_dpr_4.2x.jpg 4.2x, aem_dm_dpr_4.3x.jpg 4.3x, aem_dm_dpr_4.4x.jpg 4.4x, aem_dm_dpr_4.5x.jpg 4.5x, aem_dm_dpr_4.6x.jpg 4.6x, aem_dm_dpr_4.7x.jpg 4.7x, aem_dm_dpr_4.8x.jpg 4.8x, aem_dm_dpr_4.9x.jpg 4.9x,
       aem_dm_dpr_5x.jpg 5x">
   ```

   この DPR イメージタグコードを含める必要があります _前_ HTMLページ内のすべての静的画像。

**クライアントサイドレンダリングアプリ**

1. 次の DPR スクリプトを、ヘッダーページのヘッダーセクションにHTMLします。

   ```javascript
   <script type="text/javascript" src="srvinit.js"></script>
   <script type="text/javascript" src="dprImageInjection.js"></script>
   ```

   両方の DPR スクリプトを 1 つに組み合わせて、複数のネットワークリクエストを回避できます。

   Adobeでは、次のスクリプトを読み込むことをお勧めします _前_ 「HTML」ページの他の任意のスクリプト。
また、Adobeでは、body 要素ではなく、diffHTMLタグでアプリをBootstrapすることをお勧めします。 理由は、 `dprImageInjection.js` は、画像ページの body セクションの上部にある画像タグを動的に挿入します。HTML

## JavaScript ファイルのダウンロード {#client-side-dpr-script}

次のダウンロード用 JavaScript ファイルは、サンプル参照としてのみ提供されています。 これらのファイルをHTMLページで使用する場合は、各ファイルのコードを独自の要件に合うように必ず編集してください。

* `dprImageInjection.js`
* `srvinit.js`
* `srvwrk.js`

[JavaScript ファイルのダウンロード](/help/assets/dynamic-media/assets/aem-dynamicmedia-smartimaging-dpr.zip)

>[!MORELIKETHIS]
>
>* [スマートイメージング](/help/assets/dynamic-media/imaging-faq.md)