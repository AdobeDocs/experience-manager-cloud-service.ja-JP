---
title: ドメインの確認
description: ドメインの確認
source-git-commit: d2a98cf340dc755407250a9a9649addb75ad87d2
workflow-type: tm+mt
source-wordcount: '171'
ht-degree: 100%

---


# ドメインの確認 {#verify-domain-name}

DNS TXT レコードは、ドメインを CDN サービスでホストすることを許可します。顧客は、Cloud Manager でカスタムドメインを使用した CDN サービスのデプロイとバックエンドサービスとの関連付けを許可する DNS TXT レコードをゾーンに作成する必要があります。この関連付けは完全に顧客の管理下にあり、このサービスからドメインにコンテンツを提供することを Cloud Manager に許可します。その許可は付与されることもあれば、取り消されることもあります。この TXT レコードは、ドメインと Cloud Manager 環境に固有のものです。

1. ドメインホストにログインし、「DNS レコード」セクションにアクセスします。
1. カスタムドメインが存在する DNS ゾーンに、TXT エントリを表示どおりにコピーして貼り付けます。エントリの「名前」が必要な場合は、`@` としてください。

>[!NOTE]
>[UltraTools](https://www.ultratools.com/tools/dnsLookup)、Google DoH などの様々な DNS ルックアップツールを使用して、TXTレコードのエントリをルックアップし、TXT レコードの欠落やエラーがあるかどうかを確認できます。
