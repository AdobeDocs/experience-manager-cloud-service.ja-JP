---
title: コンテンツの HTTP/2 配信の FAQ
description: HTTP/2 コンテンツ配信について説明します。
role: Administrator,Business Practitioner
exl-id: 0a8a5fd8-a341-4e7f-84a5-409e2de97efe
source-git-commit: 1ad89be4ebddec0705c6f557fed3d697b9f1f3a7
workflow-type: tm+mt
source-wordcount: '794'
ht-degree: 69%

---

# コンテンツの HTTP/2 配信の FAQ{#http-delivery-of-content-faq}

コンテンツの HTTP/2 配信が可能になったことをお知らせします。HTTP/2を使用する場合、全体的なパフォーマンスが向上します。

>[!NOTE]
>
>この機能を使用するには、Adobe Experience Manager - Dynamic Mediaにバンドルされている、標準搭載のコンテンツ配信ネットワークを使用する必要があります。 その他のカスタムコンテンツ配信ネットワークは、この機能ではサポートされていません。

## HTTP/2 とは {#what-is-http}

HTTP/2 によりブラウザーとサーバーの通信が改善され、必要な処理能力を抑えながら情報をより高速に転送できます。

Webサイトの記事[HTTP/2](https://www.engadget.com/2015-02-24-what-you-need-to-know-about-http-2.html)について知っておくべきことは、HTTP/2とその利点を簡単かつ簡潔に説明します。

## コンテンツ配信を HTTP/2 に移行する主なメリット {#what-are-the-key-benefits-of-moving-to-http-for-content-delivery}

パフォーマンスの向上は様々な要因に基づいているので、大きく異なります。 例えば、Webサイトのコード、Dynamic Mediaの使用方法、消費者のデバイス、画面、場所などです。

アドビ独自のテストでは、以下の結果が出ています。

* 画像の場合、デバイスおよびブラウザーに応じて、応答時間が 7％～28％向上しました。パフォーマンスの向上は、iOS デバイスにおいて最も顕著でした。
* ビューアの場合、読み込み時間のパフォーマンスが 15％向上しました。

以下のデモは、HTTP/1 と HTTP/2 の読み込みの差異を示しています。

[https://http2.akamai.com/demo](https://http2.akamai.com/demo)

## HTTP/2 に切り替えるには  {#am-i-eligible-to-switch-over-to-http}

HTTP/2 を使用するには、以下の要件を満たしている必要があります。

* リッチメディアリクエストにセキュア HTTPS を使用している。
* Dynamic Media Classicライセンスの一部として、AdobeバンドルのCDN（コンテンツ配信ネットワーク）を使用している。
* 汎用の Dynamic Media ドメイン（`s7d1.scene7.com`、`s7d2.scene7.com`、`s7d13.scene7.com` のいずれか）ではなく、専用ドメイン（`images.company.com` または `mycompany.scene7.com`）を使用している。

   ドメインを探すには、[Dynamic Media Classic デスクトップアプリケーション](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/getting-started/signing-out.html?lang=ja#getting-started)を開き、アカウントにログインします。

   **[!UICONTROL 設定／アプリケーション設定／一般設定]**&#x200B;をクリックします。「**公開先サーバー名**」というラベルの付いたフィールドを見つけます。現在、汎用の Dynamic Media ドメインを使用している場合は、この切り替えの一環として独自のカスタムドメインへの移行をリクエストできます。

## Dynamic Media アカウントに対して HTTP/2 を有効にする方法 {#what-is-the-process-for-enabling-http-for-my-dm-account}

[Admin Consoleを使用してサポートケ](https://helpx.adobe.com/jp/enterprise/admin-guide.html/enterprise/using/support-for-experience-cloud.ug.html) ースを作成し、HTTP/2に切り替えるためのリクエストを実行します。自動的にはおこなわれません。

1. サポートケースには、次の情報を記入してください。

   * 主要連絡先名、電子メールおよび電話番号。
   * HTTP/2 への切り替えが必要なすべてのドメイン。つまり、`images.company.com` または `mycompany.scene7.com`。

   ドメインを探すには、[Dynamic Media Classic デスクトップアプリケーション](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/getting-started/signing-out.html#getting-started)を開き、アカウントにログインします。

   **[!UICONTROL 設定／アプリケーション設定／一般設定]**&#x200B;をクリックします。「**[!UICONTROL 公開先サーバー名]**」というラベルの付いたフィールドを見つけます。

   * リッチメディアリクエストについて、セキュリティで保護された HTTPS を使用していることを確認します。
   * 直接的関係で管理するのではなく、アドビを介して CDN を使用していることを確認します。
   * 専用ドメインを使用していることを確認します。つまり、`s7d1.scene7.com`、`s7d2.scene7.com`、`s7d13.scene7.com` などの汎用の Dynamic Media ドメインではなく、`images.company.com` または `mycompany.scene7.com` です。

   ドメインを探すには、[Dynamic Media Classic デスクトップアプリケーション](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/getting-started/signing-out.html#getting-started)を開き、アカウントにログインします。

   **[!UICONTROL 設定／アプリケーション設定／一般設定]**&#x200B;をクリックします。「**[!UICONTROL 公開先サーバー名]**」というラベルの付いたフィールドを見つけます。現在、汎用の Dynamic Media ドメインを使用している場合は、この切り替えの一環として独自のカスタムドメインへの移行をリクエストできます。

   1. テクニカルサポートによって、リクエストの送信順に基づいて HTTP/2 の顧客待機リストに追加されます。
   1. Adobeでリクエストを処理する準備が整うと、カスタマーケアから連絡があり、移行の調整と目標日の設定がおこなわれます。
   1. 完了後に通知があり、HTTP/2 への正常な切り替えを確認できます。



## HTTP/2 への切り替え見込み時期 {#when-can-i-expect-to-be-transitioned-over-to-http}

リクエストは、テクニカルサポートに届いた順に処理されます。

>[!NOTE]
>
>HTTP/2への切り替えにはキャッシュのクリアが伴うので、リードタイムは長くなります。 そのため、一度に処理できる顧客の移行は数件のみとなります。

## HTTP/2 への切り替えに伴うリスク  {#what-are-the-risks-with-moving-to-http}

HTTP/2 への切り替えには、新しい CDN 設定への移行が伴うので、CDN でキャッシュがクリアされます。

キャッシュが再作成されるまで、キャッシュされていないコンテンツはアドビの元のサーバーに直接アクセスして取得されます。このアクションにより、Adobeは、一度に少数の顧客の移行を処理する予定です。 この方法は、接触チャネルからリクエストをプルする際に、許容可能なパフォーマンスを維持します。

## URL または Web サイトが HTTP/2 でアクティベートされていることを確認する方法  {#how-can-you-verify-whether-a-url-or-website-is-activated-with-http}

Webブラウザーで使用する拡張機能をダウンロードします。 FirefoxおよびChromeの場合、**[!UICONTROL HTTP/2およびSPDY Indicator]**&#x200B;という拡張機能があります。 ブラウザーは HTTP/2 をセキュア接続でのみサポートするので、確認するには https の付いた URL を呼び出す必要があります。HTTP/2がサポートされている場合、拡張機能は青いFlash記号とヘッダー「X-Firefox-Spdy」で示されます。&quot;h2&quot;です。
