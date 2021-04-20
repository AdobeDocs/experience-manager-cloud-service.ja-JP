---
title: コンテンツの HTTP/2 配信の FAQ
description: HTTP/2 コンテンツ配信について説明します。
topic: "Administrator,Business Practitioner"
role: Administrator,Business Practitioner
translation-type: tm+mt
source-git-commit: 8093f6cec446223af58515fd8c91afa5940f9402
workflow-type: tm+mt
source-wordcount: '792'
ht-degree: 72%

---


# コンテンツの HTTP/2 配信の FAQ{#http-delivery-of-content-faq}

コンテンツの HTTP/2 配信が可能になったことをお知らせします。HTTP/2を使用する場合、全体的なパフォーマンスが向上します。

>[!NOTE]
>
>この機能を使用するには、Adobe Experience ManagerDynamic Mediaにバンドルされている標準搭載のCDNを使用する必要があります。 この機能では、その他のカスタムCDNはサポートされません。

## HTTP/2 とは {#what-is-http}

HTTP/2 によりブラウザーとサーバーの通信が改善され、必要な処理能力を抑えながら情報をより高速に転送できます。

HTTP/2 とその利点については、次の Web サイトで簡潔に説明されています。

[https://www.engadget.com/2015/02/24/what-you-need-to-know-about-http-2/](https://www.engadget.com/2015/02/24/what-you-need-to-know-about-http-2/)

## コンテンツ配信を HTTP/2 に移行する主なメリット {#what-are-the-key-benefits-of-moving-to-http-for-content-delivery}

パフォーマンスの向上は様々な要因に基づいているので、様々な要因によって異なります。 例えば、Webサイトのコード、Dynamic Mediaの使用方法、消費者のデバイス、画面、場所などがあります。

アドビ独自のテストでは、以下の結果が出ています。

* 画像の場合、デバイスおよびブラウザーに応じて、応答時間が 7％～28％向上しました。パフォーマンスの向上は、iOS デバイスにおいて最も顕著でした。
* ビューアの場合、読み込み時間のパフォーマンスが 15％向上しました。

以下のデモは、HTTP/1 と HTTP/2 の読み込みの差異を示しています。

[https://http2.akamai.com/demo](https://http2.akamai.com/demo)

## HTTP/2 に切り替えるには  {#am-i-eligible-to-switch-over-to-http}

HTTP/2 を使用するには、以下の要件を満たしている必要があります。

* リッチメディアリクエストにセキュア HTTPS を使用している。
* Dynamic Mediaクラシックライセンスの一部として、AdobeバンドルCDN(コンテンツ配信ネットワーク)を使用します。
* 汎用の Dynamic Media ドメイン（`s7d1.scene7.com`、`s7d2.scene7.com`、`s7d13.scene7.com` のいずれか）ではなく、専用ドメイン（`images.company.com` または `mycompany.scene7.com`）を使用している。

   ドメインを探すには、[Dynamic Media Classic デスクトップアプリケーション](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/getting-started/signing-out.html?lang=ja#getting-started)を開き、アカウントにログインします。

   **[!UICONTROL 設定／アプリケーション設定／一般設定]**&#x200B;をクリックします。「**公開先サーバー名**」というラベルの付いたフィールドを見つけます。現在、汎用の Dynamic Media ドメインを使用している場合は、この切り替えの一環として独自のカスタムドメインへの移行をリクエストできます。

## Dynamic Media アカウントに対して HTTP/2 を有効にする方法 {#what-is-the-process-for-enabling-http-for-my-dm-account}

[Admin Consoleを使用してサポート](https://helpx.adobe.com/jp/enterprise/admin-guide.html/enterprise/using/support-for-experience-cloud.ug.html) ケースを作成し、HTTP/2に切り替えるようリクエストします。自動的には実行されません。

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
   1. Adobeがリクエストを処理する準備が整ったら、カスタマーケアからトランジションの調整とターゲット日の設定を依頼されます。
   1. 完了後に通知があり、HTTP/2 への正常な切り替えを確認できます。



## HTTP/2 への切り替え見込み時期 {#when-can-i-expect-to-be-transitioned-over-to-http}

リクエストは、テクニカルサポートに届いた順に処理されます。

>[!NOTE]
>
>HTTP/2へのトランジションではキャッシュのクリアが行われるので、リードタイムは長くなります。 そのため、一度に処理できる顧客の移行は数件のみとなります。

## HTTP/2 への切り替えに伴うリスク  {#what-are-the-risks-with-moving-to-http}

HTTP/2 への切り替えには、新しい CDN 設定への移行が伴うので、CDN でキャッシュがクリアされます。

キャッシュが再作成されるまで、キャッシュされていないコンテンツはアドビの元のサーバーに直接アクセスして取得されます。この措置により、Adobeは一度に複数の顧客トランジションを処理する予定です。 この方法を使用すると、接触チャネルから要求を取り込む際に、許容可能なパフォーマンスが維持されます。

## URL または Web サイトが HTTP/2 でアクティベートされていることを確認する方法  {#how-can-you-verify-whether-a-url-or-website-is-activated-with-http}

Webブラウザで使用する拡張機能をダウンロードします。 FirefoxおよびChromeには、**[!UICONTROL HTTP/2およびSPDYインジケーター]**&#x200B;という拡張子があります。 ブラウザーは HTTP/2 をセキュア接続でのみサポートするので、確認するには https の付いた URL を呼び出す必要があります。HTTP/2がサポートされている場合、拡張子は青いFlash記号で示され、ヘッダーは「X-Firefox-Spdy」です。&quot;h2&quot;。
