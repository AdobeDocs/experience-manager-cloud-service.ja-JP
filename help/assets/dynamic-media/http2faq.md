---
title: コンテンツの HTTP/2 配信の FAQ
description: HTTP2 コンテンツ配信と、ブラウザーとサーバー間の通信を改善して情報を高速に転送する方法について説明します。
contentOwner: Rick Brough
role: Admin,User
exl-id: 0a8a5fd8-a341-4e7f-84a5-409e2de97efe
source-git-commit: 0e452bd94d75609ecc3c20ab6b56ded968ed0a70
workflow-type: tm+mt
source-wordcount: '807'
ht-degree: 86%

---

# コンテンツの HTTP/2 配信の FAQ{#http-delivery-of-content-faq}

コンテンツの HTTP/2 配信が可能になったことをお知らせします。HTTP/2 を使用すると、全体的なパフォーマンスが向上します。

>[!NOTE]
>
>この機能を使用するには、Adobe Experience Manager - Dynamic Media にバンドルされている標準搭載の CDN（コンテンツ配信ネットワーク）を使用する必要があります。この機能では、その他のカスタム CDN はサポートされていません。

## HTTP/2 とは  {#what-is-http}

HTTP/2 によりブラウザーとサーバーの通信が改善され、必要な処理能力を抑えながら情報をより高速に転送できます。

Web サイトの記事 [What you must know about HTTP/2](https://www.engadget.com/2015-02-24-what-you-need-to-know-about-http-2.html)（英語のみ）では、HTTP/2 とその利点を簡単かつ簡潔に説明しています。

## コンテンツ配信を HTTP/2 に移行する主なメリット  {#what-are-the-key-benefits-of-moving-to-http-for-content-delivery}

パフォーマンスの向上は様々な要因に基づいているので、非常に多岐にわたります。例えば、Web サイトのコード、Dynamic Media の使用方法、消費者のデバイス、画面、場所などがあります。

アドビ独自のテストでは、以下の結果が出ています。

* 画像の場合、デバイスおよびブラウザーに応じて、応答時間が 7％～28％向上しました。パフォーマンスの最も顕著な向上は、iOSデバイスでした。
* ビューアの場合、読み込み時間のパフォーマンスが 15％向上しました。

次のデモは、HTTP/1 と HTTP/2 の読み込みの違いを示しています。

[https://http2.akamai.com/demo](https://http2.akamai.com/demo)

## HTTP/2 に切り替える資格はありますか？ {#am-i-eligible-to-switch-over-to-http}

HTTP/2 を使用するには、次の要件を満たす必要があります。

* リッチメディアリクエストにセキュア HTTPS を使用している。
* アドビ製品にバンドルされた CDN（コンテンツ配信ネットワーク）を、Dynamic Media Classic ライセンスの一部として使用している。
* 汎用の Dynamic Media ドメイン（`s7d1.scene7.com`、`s7d2.scene7.com`、`s7d13.scene7.com` のいずれか）ではなく、専用ドメイン（`images.company.com` または `mycompany.scene7.com`）を使用している。

  ドメインを探すには、[Dynamic Media Classic デスクトップアプリケーション](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/getting-started/signing-out.html?lang=ja#getting-started)を開き、アカウントにログインします。

  **[!UICONTROL 設定]**／**[!UICONTROL アプリケーション設定]**／**[!UICONTROL 一般設定]**&#x200B;に移動します。「**公開先サーバー名**」というラベルの付いたフィールドを見つけます。現在、汎用の Dynamic Media ドメインを使用している場合は、この切り替えの一環として独自のカスタムドメインへの移行をリクエストできます。

## Dynamic Media アカウントに対して HTTP/2 を有効にする方法  {#what-is-the-process-for-enabling-http-for-my-dm-account}

[Admin Console を使用してサポートケースを作成](https://helpx.adobe.com/jp/enterprise/using/support-for-experience-cloud.html)し、HTTP/2 に切り替えるように要求します。自動的には切り替わりません。

1. サポートケースには、次の情報を記入してください。

   * 主要連絡先名、メールおよび電話番号。
   * HTTP/2 への切り替えが必要なすべてのドメイン。つまり、`images.company.com` または `mycompany.scene7.com`。

   ドメインを探すには、[Dynamic Media Classic デスクトップアプリケーション](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/getting-started/signing-out.html?lang=ja#getting-started)を開き、アカウントにログインします。

   **[!UICONTROL 設定]**／**[!UICONTROL アプリケーション設定]**／**[!UICONTROL 一般設定]**&#x200B;に移動します。「**[!UICONTROL 公開先サーバー名]**」というラベルの付いたフィールドを見つけます。

   * リッチメディアリクエストにセキュアな HTTPS を使用していることを確認します。
   * 直接の関係で管理されていない、Adobeを通じて CDN を使用していることを確認します。
   * 専用ドメインを使用していることを確認します。つまり、`s7d1.scene7.com`、`s7d2.scene7.com`、`s7d13.scene7.com` などの汎用の Dynamic Media ドメインではなく、`images.company.com` または `mycompany.scene7.com` です。

   ドメインを探すには、[Dynamic Media Classic デスクトップアプリケーション](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/getting-started/signing-out.html?lang=ja#getting-started)を開き、アカウントにログインします。

   **[!UICONTROL 設定]**／**[!UICONTROL アプリケーション設定]**／**[!UICONTROL 一般設定]**&#x200B;に移動します。「**[!UICONTROL 公開先サーバー名]**」というラベルの付いたフィールドを見つけます。現在、汎用の Dynamic Media ドメインを使用している場合は、この切り替えの一環として独自のカスタムドメインへの移行をリクエストできます。

   1. カスタマーサポートによって、リクエストの送信順に基づいて HTTP/2 の顧客待機リストに追加されます。
   1. アドビでリクエストを処理する準備が整うと、移行についての調整や完了予定日の設定のため、カスタマーサポートから連絡が入ります。
   1. 完了後に通知が届き、HTTP/2 への正常な切り替えを確認できます。

## HTTP/2 への切り替え見込み時期  {#when-can-i-expect-to-be-transitioned-over-to-http}

リクエストは、カスタマーサポートに届いた順に処理されます。

>[!NOTE]
>
>HTTP/2 への移行ではキャッシュをクリアするので、リードタイムが長くなる場合があります。そのため、一度に処理できる顧客の移行は数件のみとなります。

## HTTP/2 への切り替えに伴うリスク {#what-are-the-risks-with-moving-to-http}

HTTP/2 への切り替えには、新しい CDN 設定への移行が伴うので、CDN でキャッシュがクリアされます。

キャッシュされていないコンテンツは、キャッシュが再構築されるまで、Adobeの元のサーバーに直接ヒットします。 この措置により、アドビは一度に複数の顧客トランジションを処理する予定です。この方法を使用すると、接触チャネルからリクエストを取り込む際に、許容可能なパフォーマンスが維持されます。

## URL または Web サイトが HTTP/2 でアクティベートされていることを確認する方法 {#how-can-you-verify-whether-a-url-or-website-is-activated-with-http}

Web ブラウザーで使用する拡張機能をダウンロードします。Firefox および Chrome の場合は、「**[!UICONTROL HTTP/2 and SPDY Indicator]**」という拡張機能があります。ブラウザーは HTTP/2 をセキュア接続でのみサポートするので、確認するには https の付いた URL を呼び出す必要があります。この拡張では、HTTP/2 がサポートされている場合、青い稲妻マークおよび「X-Firefox-Spdy: h2」というヘッダーによって示されます。
