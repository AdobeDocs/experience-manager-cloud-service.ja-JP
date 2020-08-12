---
title: Dynamic Media アセットの配信
description: Dynamic Media アセットの配信方法を学習します
translation-type: tm+mt
source-git-commit: ea6a1bddaab6819d1f89268ceba3c4d4981729a2
workflow-type: tm+mt
source-wordcount: '315'
ht-degree: 93%

---


# Dynamic Media アセットの配信{#delivering-dynamic-media-assets}

ビデオでも画像でも、Dynamic Media アセットの配信方法は、Web サイトの実装方法によって異なります。

Dynamic Media を使用する場合、次の複数のオプションがあります。

* Web サイトが AEM 上にホストされている場合は、Dynamic Media アセットを直接ページに追加します。
* Web サイトが AEM 上にない場合は、次のいずれかの方法を選択します。

   * ビデオまたは画像を Web サイトに埋め込みます。
   * Web アプリケーションに URL をリンクします。ビデオプレーヤーをポップアップウィンドウまたはモーダルウィンドウとして配信する場合には、リンク機能を使用します。
   * レスポンシブサイトの場合は、[最適化された画像を配信できます。](/help/assets/dynamic-media/responsive-site.md)

>[!NOTE]
>
>スマートイメージングは、既存の画像プリセットで機能し、配信の直前にインテリジェンスを使用して、ブラウザーまたはネットワークの接続速度に基づいて画像のファイルサイズをさらに低減します。詳しくは、[スマートイメージング](/help/assets/dynamic-media/imaging-faq.md)を参照してください。

詳しくは、次のトピックを参照してください。

* [Web ページへの Dynamic Media アセットの追加](/help/assets/dynamic-media/adding-dynamic-media-assets-to-pages.md)
* [Web ページへのビデオビューアまたは画像ビューアの埋め込み](/help/assets/dynamic-media/embed-code.md)
* [Dynamic Media でのホットリンク保護の有効化](/help/assets/dynamic-media/hotlink-protection.md)
* [Web アプリケーションへの URL のリンク](/help/assets/dynamic-media/linking-urls-to-yourwebapplication.md)
* [レスポンシブサイト用に最適化された画像の配信](/help/assets/dynamic-media/responsive-site.md)
* [コンテンツの HTTP/2 配信](/help/assets/dynamic-media/http2faq.md)
* [ダイナミックメディアを使用したCDNキャッシュの無効化](/help/assets/dynamic-media/invalidate-cdn-cache-dynamic-media.md)
* [Dynamic Media Classicを使用したCDNキャッシュの無効化](/help/assets/dynamic-media/invalidate-cdn-cache-dm-classic.md)
* [ルールセットを使用した URL の変換](/help/assets/dynamic-media/using-rulesets-to-transform-urls.md)

## Dynamic Media アセットの HTTP/2 配信 {#http-delivery-of-dynamic-media-assets}

AEM は現在、HTTP/2 上でのすべての Dynamic Media コンテンツ（画像とビデオ）の配信をサポートしています。つまり、画像やビデオの公開済み URL や埋め込みコードは、ホストされるアセットを受け取るアプリケーションとの統合に使用できます。その公開済みアセットは、その後、HTTP/2 プロトコルで配信されます。この配信方法により、ブラウザーとサーバーの通信が向上し、すべての Dynamic Media アセットの応答時間と読み込み時間が短くなります。

詳しくは、[コンテンツの HTTP/2 配信に関する FAQ](/help/assets/dynamic-media/http2faq.md) を参照してください。
