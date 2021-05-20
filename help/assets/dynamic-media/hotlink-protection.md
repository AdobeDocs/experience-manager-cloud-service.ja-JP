---
title: Dynamic Media でのホットリンク保護の有効化
description: Dynamic Mediaでホットリンク保護を有効にする方法を説明します。
feature: アセット管理
role: Business Practitioner
exl-id: 0198b3a3-173e-46ca-a845-3f58f8eab769
source-git-commit: 1ad89be4ebddec0705c6f557fed3d697b9f1f3a7
workflow-type: tm+mt
source-wordcount: '192'
ht-degree: 26%

---

# Dynamic Media でのホットリンク保護の有効化 {#activating-hotlink-protection-in-dynamic-media}

ホットリンクは、サードパーティのWebサイトがHTMLコードを使用してWebサイトの画像を表示する場合に発生します。 訪問者のブラウザーが自社サーバーから画像に直接アクセスするので、画像が要求されるたびに帯域幅が消費されます。ホットリンク&#x200B;*保護*&#x200B;は、他のWebサイトがWebページ上の画像、CSS、JavaScript™に直接リンクするのを防ぐ方法です。 このような保護により、Dynamic Media アカウントでの不要な帯域幅使用を減らすことができます。

[Adobeのお](https://helpx.adobe.com/jp/support.html) 客様Carecanは、CDNレベルでリファラーフィルターを設定できます。これにより、Dynamic Mediaコンテンツは、ドメインに許可されたWebサイトのリストにあるWebサイトにのみ提供されます。

>[!NOTE]
>
>この機能を使用するには、Adobe Experience Manager Dynamic Mediaに組み込まれている標準搭載のCDNを使用する必要があります。 その他のカスタムCDNは、この機能ではサポートされません。 ホットリンク保護を有効にするには、管理者がサポートチケットを作成して、Dynamic Mediaアカウントに対する設定の変更をリクエストする必要があります。 ホットリンク保護を有効にするための追加費用は発生しません。
