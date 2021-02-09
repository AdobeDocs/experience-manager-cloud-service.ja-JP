---
title: TXT レコードの追加
description: カスタムドメイン名の追加
translation-type: tm+mt
source-git-commit: b76a22469f248dde316dcaa514a906fe4361afd1
workflow-type: tm+mt
source-wordcount: '299'
ht-degree: 89%

---


# TXT レコードの追加 {#adding-txt}

DNS TXT レコードは、ドメインを CDN サービスでホストすることを許可します。顧客は、Cloud Manager でカスタムドメインを使用した CDN サービスのデプロイとバックエンドサービスとの関連付けを許可する DNS TXT レコードをゾーンに作成する必要があります。この関連付けは、顧客の管理下にあり、Cloud Manager でサービスからドメインにコンテンツを提供することを積極的に認可します。その認可は付与することも取り下げることもできます。

TXTレコードを作成する前に、次の手順に従う必要があります。

* 組織のドメインの DNS レコードを変更する権限を持つ、または、持っている担当者に連絡する。
* ドメインホストまたは登録機関がわからない場合は、確認する。

ドメインの検証を開始すると、検証に使用する名前とTXT値がCloud Managerによって提供されます。 指定した名前と値を使用して、ドメインの DNS サーバーに TXT レコードを送信します。

1. ドメインホストにログインし、DNS レコードセクションにアクセスします。
1. `_aemverification.[yourdomainname]`を「名前」として追加し、TXT 値を表示されるとおりに追加します。
次の表の例を参照してください。

| ドメイン | 名前 | TXT 値 |
|--- |--- |---|
| `example.com` | `_aemverification.example.com` | Cloud Manager UI に表示され、ドメインと Cloud Manager 環境に固有 |
| `test.example.com` | `_aemverification.test.example.com` | Cloud Manager UI に表示され、ドメインと Cloud Manager 環境に固有 |

完了したら、`dig _aemverification.[yourdomainname] -t txt` を実行して結果を確認できます。
期待される結果には、Cloud Manager UI で指定された TXT 値が表示されます。

例えば、ドメインが `example.com` の場合は、`dig TXT _aemverification.example.com -t txt` を実行します。

>[!NOTE]
>また、様々な [DNS 検索ツール](https://www.ultratools.com/tools/dnsLookup)があります。Google DoH を使用すると、TXT レコードのエントリを参照し、TXT レコードがないか、エラーがあるかを識別できます。

