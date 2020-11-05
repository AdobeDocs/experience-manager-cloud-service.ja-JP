---
title: ドメインの確認
description: ドメインの確認
translation-type: tm+mt
source-git-commit: d2a98cf340dc755407250a9a9649addb75ad87d2
workflow-type: tm+mt
source-wordcount: '171'
ht-degree: 0%

---


# ドメインの確認 {#verify-domain-name}

DNS TXTレコードは、ドメインをCDNサービスでホストすることを許可します。 顧客は、Cloud Managerでカスタムドメインを使用したCDNサービスの展開とバックエンドサービスとの関連付けを許可するDNS TXTレコードをゾーンに作成する必要があります。 この関連付けは、お客様の管理下にあり、Cloud Managerでサービスからドメインにコンテンツを提供することを強く承認します。 その認可は，取り下げられるのと同じく，取り下げられる。 TXTレコードは、ドメインとCloud Managerの環境に固有です。

1. ドメインホストにログインし、「DNSレコード」セクションにアクセスします。
1. カスタムドメインが存在するDNSゾーンに、表示されるとおりにTXTエントリをコピーして貼り付けます。 エントリに「名前」が必要な場合は、名前を付け `@`ます。

>[!NOTE]
>DNSルックアップツール [](https://www.ultratools.com/tools/dnsLookup)、Google DoHなど、様々なDNSルックアップツールを使用して、TXTレコードのエントリを参照し、TXTレコードが存在しないか、またはエラーがあるかを識別できます。
