---
title: Dynamic Media でホットリンク保護を有効化する
description: Dynamic Media でホットリンク保護を有効化する方法について説明します。
contentOwner: Rick Brough
feature: Asset Management
role: User
exl-id: 0198b3a3-173e-46ca-a845-3f58f8eab769
source-git-commit: 36ab36ba7e14962eba3947865545b8a3f29f6bbc
workflow-type: tm+mt
source-wordcount: '188'
ht-degree: 100%

---

# Dynamic Media でホットリンク保護を有効化する {#activating-hotlink-protection-in-dynamic-media}

ホットリンクは、サードパーティの Web サイトで HTML コードを使用して自社 Web サイト内の画像を表示する場合に行われます。訪問者のブラウザーが自社サーバーから画像に直接アクセスするので、画像が要求されるたびに帯域幅が消費されます。ホットリンク&#x200B;*保護*&#x200B;は、自社 Web サイト上の画像、CSS、JavaScript などに他の Web サイトが直接リンクできないようにするための方法です。このような保護により、Dynamic Media アカウントでの不要な帯域幅使用を減らすことができます。

[アドビカスタマーサポート](https://experienceleague.adobe.com/?support-solution=Experience+Manager&amp;lang=ja#home)では、CDN レベルでリファラーフィルターを設定できます。これにより、Dynamic Media のコンテンツが、ドメインで許可された Web サイトのリストにある Web サイトにのみ提供されるようにします。

>[!NOTE]
>
>この機能を使用するには、Adobe Experience Manager Dynamic Media にバンドルされている標準搭載の CDN を使用する必要があります。この機能では、その他のカスタム CDN はサポートされません。ホットリンク保護を有効化するには、Dynamic Media アカウントの設定変更を要求するサポートチケットを管理者が作成する必要があります。ホットリンク保護を有効化するための追加費用は発生しません。
