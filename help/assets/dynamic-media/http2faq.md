---
title: コンテンツの HTTP/2 配信の FAQ
description: HTTP2 コンテンツ配信について説明します。
translation-type: tm+mt
source-git-commit: d6e92a433e61c2a959c62080fcd52fe0ebe67c4f

---


# コンテンツの HTTP/2 配信の FAQ{#http-delivery-of-content-faq}

コンテンツの HTTP/2 配信が可能になったことをお知らせします。HTTP/2 を使用すると、パフォーマンスが全体的に向上します。

## What is HTTP/2? {#what-is-http}

HTTP/2 ではブラウザーとサーバーの通信方法が改善され、より少ない処理能力で情報の転送が高速化されます。

HTTP/2 とその利点については、次の Web サイトで簡潔に説明されています。

[https://www.engadget.com/2015/02/24/what-you-need-to-know-about-http-2/](https://www.engadget.com/2015/02/24/what-you-need-to-know-about-http-2/)

## What are the key benefits of moving to HTTP/2 for content delivery? {#what-are-the-key-benefits-of-moving-to-http-for-content-delivery}

パフォーマンスの向上は、Web サイトのコード、Scene7 の使用方法、顧客のデバイス、画面、場所などの要因によって大きく異なります。

アドビ独自のテストによって、以下の結果が得られました。

* 画像の場合、デバイスおよびブラウザーに応じて、応答時間が 7 ％～ 28 ％向上しました。パフォーマンスの向上は、iOS デバイスにおいて最も顕著でした。
* ビューアの場合、読み込み時間のパフォーマンスが 15 ％向上しました。

以下のデモは、HTTP/1 と HTTP/2 の読み込みの差異を示しています。

[https://http2.akamai.com/demo](https://http2.akamai.com/demo)

## HTTP/2 に切り替えるには {#am-i-eligible-to-switch-over-to-http}

HTTP/2 を使用するには、以下の要件を満たしている必要があります。

* リッチメディアリクエストでは、セキュリティで保護された HTTPS を使用します。
* Dynamic Media Classicライセンスの一部として、AdobeバンドルCDN（コンテンツ配信ネットワーク）を使用します。
* 汎用のダイナミックメディアクラシックドメイン( `images.company.com` 、、ま `mycompany.scene7.com`たは)ではなく、専用ドメイン(または `s7d1.scene7.com`)を `s7d2.scene7.com`使用し `s7d13.scene7.com`ます。

   ドメインを確認するには、各会社アカウントの [Scene7 Publishing System のインスタンスにログイン](https://www.adobe.com/marketing-cloud/experience-manager/scene7-login.html)します。

   **[!UICONTROL 設定／アプリケーション設定／一般設定]**&#x200B;をクリックします。「**公開先サーバー名**」というラベルの付いたフィールドを見つけます。現在汎用 Scene7 ドメインを使用している場合は、この切り替えの一部として、独自のカスタムドメインへの移行を要求できます。

## What is the process for enabling HTTP/2 for my Dynamic Media Classic account? {#what-is-the-process-for-enabling-http-for-my-scene-account}

You must initiate an Adobe Technical Support (`s7support@adobe.com`) request to switch over to HTTP/2; it is not automatically done for you.

1. サポートリクエストで以下の情報を提供します。

   * 主要連絡先名、電子メールおよび電話番号。
   * HTTP/2 への移行が必要なすべてのドメイン。すなわち、 `images.company.com` または `mycompany.scene7.com`。
   ドメインを確認するには、各会社アカウントの [Scene7 Publishing System のインスタンスにログイン](https://www.adobe.com/marketing-cloud/experience-manager/scene7-login.html)します。

   **[!UICONTROL 設定／アプリケーション設定／一般設定]**&#x200B;をクリックします。「**[!UICONTROL 公開先サーバー名]**」というラベルの付いたフィールドを見つけます。

   * リッチメディアリクエストについて、セキュリティで保護された HTTPS を使用していることを確認します。
   * 直接的関係で管理するのではなく、アドビを介して CDN を使用していることを確認します。
   * 専用ドメインを使用していることの確認。つまり、、 `images.company.com` など `mycompany.scene7.com`の汎用Scene7ドメインではな `s7d1.scene7.com`く、ま `s7d2.scene7.com`たは `s7d13.scene7.com`。
   ドメインを確認するには、各会社アカウントの [Scene7 Publishing System のインスタンスにログイン](https://www.adobe.com/marketing-cloud/experience-manager/scene7-login.html)します。

   **[!UICONTROL 設定／アプリケーション設定／一般設定]**&#x200B;をクリックします。「**[!UICONTROL 公開先サーバー名]**」というラベルの付いたフィールドを見つけます。現在汎用 Scene7 ドメインを使用している場合は、この切り替えの一部として、独自のカスタムドメインへの移行を要求できます。

   1. テクニカルサポートでは、リクエストが送信された順序に基づいて、HTTP/2顧客のウェイトリストに追加されます。
   1. アドビでリクエストを処理する準備が整うと、サポートから連絡があり、切り替えについての調整および完了予定日の設定がおこなわれます。
   1. 完了後に通知があり、HTTP2 への正常な切り替えを確認できます。



## When can I expect to be transitioned over to HTTP/2? {#when-can-i-expect-to-be-transitioned-over-to-http}

リクエストは、テクニカルサポートが受け取った順に処理されます。

>[!NOTE]
>
>HTTP/2 への切り替えにはキャッシュのクリアが含まれるので、リードタイムが長くなる場合があります。そのため、一度に処理できる顧客の切り替えは数件のみとなります。

## HTTP/2 への移行に伴うリスク {#what-are-the-risks-with-moving-to-http}

HTTP/2 への切り替えには、新しい CDN 設定への移行が伴うので、CDN でキャッシュがクリアされます。

キャッシュが再作成されるまで、キャッシュされていないコンテンツはアドビの元のサーバーに直接アクセスして取得されます。このため、元のサーバーからリクエストをプルするときに許容できるパフォーマンスが維持されるように、アドビでは一度に少数の顧客の切り替えを処理するよう計画します。

## URL または Web サイトが HTTP/2 を使用してアクティベートされているかどうかは、どのように確認できますか。 {#how-can-you-verify-whether-a-url-or-website-is-activated-with-http}

Web ブラウザーで使用する拡張機能をダウンロードする必要があります。For Firefox and Chrome there is an extension called **[!UICONTROL HTTP/2 and SPDY Indicator]**. ブラウザーでは HTTP/2 のみが安全にサポートされるので、HTTPS の URL を呼び出して確認する必要があります。HTTP/2がサポートされている場合、この拡張子は青いFlashシンボルの形式で示され、ヘッダーは「X-Firefox-Spdy」です。&quot;h2&quot;。
