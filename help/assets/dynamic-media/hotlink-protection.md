---
title: Dynamic Media でのホットリンク保護の有効化
description: Dynamic Mediaでホットリンク保護を有効にする方法を説明します。
feature: Asset Management
topic: Business Practitioner
role: Business Practitioner
translation-type: tm+mt
source-git-commit: 497952b1b6679eca301839d1435924e16a2e2438
workflow-type: tm+mt
source-wordcount: '196'
ht-degree: 27%

---


# Dynamic Media でのホットリンク保護の有効化 {#activating-hotlink-protection-in-dynamic-media}

ホットリンクとは、サードパーティのWebサイトがHTMLコードを使用してWebサイトの画像を表示する場合です。 訪問者のブラウザーが自社サーバーから画像に直接アクセスするので、画像が要求されるたびに帯域幅が消費されます。ホットリンク&#x200B;*保護*&#x200B;は、他のWebサイトがWebページ上の画像、CSS、またはJavaScriptに直接リンクするのを防ぐ方法です。 このような保護により、Dynamic Media アカウントでの不要な帯域幅使用を減らすことができます。

[Adobe](https://helpx.adobe.com/jp/support.html) のお客様は、CDNレベルで転送者フィルタを設定できます。これにより、ドメインで許可されたWebサイトのリスト上のWebサイトにのみDynamic Mediaのコンテンツが提供されます。

>[!NOTE]
>
>この機能を使用するには、Adobe Experience ManagerDynamic Mediaにバンドルされている標準搭載のCDNを使用する必要があります。 この機能では、その他のカスタムCDNはサポートされません。 ホットリンク保護を有効にするには、管理者がサポートチケットを作成して、Dynamic Mediaアカウントの設定変更をリクエストする必要があります。 ホットリンク保護を有効にするための追加費用は発生しません。
