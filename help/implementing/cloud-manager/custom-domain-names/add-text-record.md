---
title: TXTレコードの追加
description: カスタムドメイン名の追加
translation-type: tm+mt
source-git-commit: b76a22469f248dde316dcaa514a906fe4361afd1
workflow-type: tm+mt
source-wordcount: '299'
ht-degree: 0%

---


# TXTレコードの追加{#adding-txt}

DNS TXTレコードは、ドメインをCDNサービスでホストすることを許可します。 顧客は、Cloud Managerでカスタムドメインを使用したCDNサービスの展開とバックエンドサービスとの関連付けを許可するDNS TXTレコードをゾーンに作成する必要があります。 この関連付けは、お客様の管理下にあり、Cloud Managerでサービスからドメインにコンテンツを提供することを強く承認します。 その認可は，取り下げられるのと同じく，取り下げられる。

TXTレコードを作成する前に、次の手順に従う必要があります。

* 組織のドメインのDNSレコードを変更する権限を持つか、または可能な適切な担当者に問い合わせてください。
* ドメインホストまたは登録機関を既に知らない場合は、それを特定します。

ドメインの検証を開始すると、検証に使用する名前とTXT値がCloud Managerによって提供されます。 指定し追加た名前と値を使用して、ドメインのDNSサーバーにTXTレコードを送信します。

1. ドメインホストにログインし、「DNSレコード」セクションにアクセスします。
1. 追加`_aemverification.[yourdomainname]`を名前として指定し、TXT値を表示されるとおりに追加します。
次の表の例を参照してください。

| ドメイン | 名前 | TXT値 |
|--- |--- |---|
| `example.com` | `_aemverification.example.com` | Cloud Manager UIに表示され、ドメインとCloud Manager環境に固有 |
| `test.example.com` | `_aemverification.test.example.com` | Cloud Manager UIに表示され、ドメインとCloud Manager環境に固有 |

完了したら、次を実行して結果を確認できます。`dig _aemverification.[yourdomainname] -t txt`.
期待される結果には、Cloud Manager UIで指定されたTXT値が表示されます。

例えば、ドメインが`example.com`の場合は、次を実行します。`dig TXT _aemverification.example.com -t txt`.

>[!NOTE]
>また、様々な[DNSルックアップツール](https://www.ultratools.com/tools/dnsLookup)があります。Google DoHを使用して、TXTレコードのエントリを参照し、TXTレコードがないか、エラーがあるかを識別できます。

