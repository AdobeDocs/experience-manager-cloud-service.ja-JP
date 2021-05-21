---
title: Dynamic Media でのホットリンク保護の有効化
description: Dynamic Mediaでホットリンク保護を有効にする方法を説明します。
feature: アセット管理
role: Business Practitioner
exl-id: 0198b3a3-173e-46ca-a845-3f58f8eab769
source-git-commit: 1ad89be4ebddec0705c6f557fed3d697b9f1f3a7
workflow-type: tm+mt
source-wordcount: '192'
ht-degree: 83%

---

# Dynamic Media でのホットリンク保護の有効化 {#activating-hotlink-protection-in-dynamic-media}

ホットリンクは、サードパーティの Web サイトで HTML コードを使用して自社 Web サイト内の画像を表示する場合におこなわれます。訪問者のブラウザーが自社サーバーから画像に直接アクセスするので、画像が要求されるたびに帯域幅が消費されます。ホットリンク&#x200B;*保護*&#x200B;は、他のWebサイトがWebページ上の画像、CSS、JavaScript™に直接リンクするのを防ぐ方法です。 このような保護により、Dynamic Media アカウントでの不要な帯域幅使用を減らすことができます。

[Adobe のサポート](https://helpx.adobe.com/jp/support.html)では、CDN レベルでリファラーフィルターを設定できます。これにより、Dynamic Media のコンテンツが、ドメインで許可された Web サイトのリストにある Web サイトにのみ提供されるようにします。

>[!NOTE]
>
>この機能を使用するには、Adobe Experience Manager Dynamic Media にバンドルされている標準搭載の CDN を使用する必要があります。この機能では、その他のカスタム CDN はサポートされません。ホットリンク保護を有効化するには、Dynamic Media アカウントの設定変更を要求するサポートチケットを管理者が作成する必要があります。ホットリンク保護を有効化するための追加費用は発生しません。
