---
title: コンテンツの HTTP/2 配信
description: HTTP/2 によりブラウザーとサーバーの通信が改善され、必要な処理能力を抑えながら情報をより高速に転送できます。
translation-type: tm+mt
source-git-commit: 6224d193adfb87bd9b080f48937e0af1f03386d6

---


# コンテンツの HTTP/2 配信 {#http-delivery-of-content}

アドビは、パフォーマンスの向上という全体的な利点をもたらすコンテンツの HTTP/2 配信に対応しました。

## What is HTTP/2? {#what-is-http}

HTTP/2 によりブラウザーとサーバーの通信が改善され、必要な処理能力を抑えながら情報をより高速に転送できます。

以下の Web サイトは、HTTP/2 の概要と利点について簡潔に説明しています。

[https://www.engadget.com/2015/02/24/what-you-need-to-know-about-http-2/](https://www.engadget.com/2015/02/24/what-you-need-to-know-about-http-2/)

## What are the key benefits of moving to HTTP/2 for content delivery? {#what-are-the-key-benefits-of-moving-to-http-for-content-delivery}

パフォーマンスがどれくらい向上するかは、Web サイトのコード、Dynamic Media の使用方法、消費者のデバイス、画面と場所などに応じて異なります。

アドビ独自のテストでは、以下の結果が出ています。

* 画像の場合、デバイスおよびブラウザーに応じて、応答時間が 7 ％～ 28 ％向上しました。パフォーマンスの向上は、iOS デバイスにおいて最も顕著でした。
* ビューアの場合、読み込み時間のパフォーマンスが 15 ％向上しました。

以下のデモは、HTTP/1 と HTTP/2 の読み込みの差異を示しています。

[https://http2.akamai.com/demo](https://http2.akamai.com/demo)

## HTTP/2 に切り替えるには {#am-i-eligible-to-switch-over-to-http}

HTTP/2 を使用するには、以下の要件を満たしている必要があります。

* リッチメディアリクエストにセキュア HTTPS を使用している。
* アドビ製品にバンドルされたコンテンツ配信ネットワーク（CDN）を Dynamic Media ライセンスの一部として使用している。
* 専用ドメイン（company-h.assetsadobe#.com 以外）を使用している。

    既に専用ドメインがある場合、テクニカルサポート経由でオプトインしていただけます。

    専用ドメインがない場合、アドビが 2018 年にお客様の HTTP/2 への移行をスケジュールいたします。

## What is the process for enabling HTTP/2 for my Dynamic Media account? {#what-is-the-process-for-enabling-http-for-my-dynamic-media-account}

HTTP/2 に切り替えるためのリクエストを開始する必要があります。自動的にはおこなわれません。

1. HTTP2 に切り替えるためのテクニカルサポートリクエストを開始します。[AEM サポートポータルへのアクセス](https://helpx.adobe.com/experience-manager/kb/accessing-aem-support-portal.html)を参照してください。

   1. サポートリクエストには、以下の情報を記入してください。

      1. 主要連絡先の氏名、電子メールアドレス、電話番号。
      1. HTTP/2 への移行が必要なすべてのドメイン。
      1. リッチメディアリクエストにセキュア HTTPS を使用していることの確認。
      1. アドビの CDN を使用しており、直接の関係で管理していないことの確認。
      1. 専用ドメインを使用していることの確認。Dynamic Media を使用しているお客様であれば、既に専用ドメインを使用しています。
   1. テクニカルサポートが、リクエストを送信された順に、お客様を HTTP/2 待機リストに追加いたします。
   1. アドビがお客様のリクエストに対応する用意ができ次第、サポートがお客様にお知らせして、移行をコーディネートし、目標日を設定します。
   1. お客様は、完了後の通知で HTTP/2 への移行が成功したことを確認できます。

      ブラウザーにはこのことが表示されないので、拡張機能をダウンロードする必要があります。

      Firefox と Chrome の場合、「HTTP/2 and SPDY Indicator」という拡張があります。ブラウザーは HTTP/2 をセキュア接続でのみサポートするので、確認するには https の付いた URL を呼び出す必要があります。この拡張では、HTTP/2 がサポートされている場合、青い稲妻マークおよび「X-Firefox-Spdy: h2」というヘッダーによって示されます。


## When can I expect to be transitioned over to HTTP/2? {#when-can-i-expect-to-be-transitioned-over-to-http}

リクエストは、テクニカルサポートによって受信された順に処理されます。

>[!NOTE]
>
>HTTP/2 への切り替えにはキャッシュのクリアが含まれるので、リードタイムが長くなる場合があります。そのため、一度に処理できる顧客の切り替えは数件のみとなります。

## HTTP/2 への移行に伴うリスク {#what-are-the-risks-with-moving-to-http}

HTTP/2 への切り替えには、新しい CDN 設定への移行が伴うので、CDN でキャッシュがクリアされます。

キャッシュが再作成されるまで、キャッシュされていないコンテンツはアドビの元のサーバーに直接アクセスして取得されます。このため、元のサーバーからリクエストをプルするときに許容できるパフォーマンスが維持されるように、アドビでは一度に少数の顧客の切り替えを処理するよう計画します。

## URL または Web サイトが HTTP/2 を使用してアクティベートされているかどうかは、どのように確認できますか。 {#how-can-you-verify-whether-a-url-or-website-is-activated-with-http}

ブラウザーにはこのことが表示されないので、拡張機能をダウンロードする必要があります。

Firefox と Chrome の場合、「HTTP/2 and SPDY Indicator」という拡張があります。ブラウザーは HTTP/2 をセキュア接続でのみサポートするので、確認するには https の付いた URL を呼び出す必要があります。この拡張では、HTTP/2 がサポートされている場合、青い稲妻マークおよび「X-Firefox-Spdy: h2」というヘッダーによって示されます。
