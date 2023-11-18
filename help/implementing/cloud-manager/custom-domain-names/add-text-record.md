---
title: TXT レコードの追加
description: TXT レコードを追加して、Cloud Manager でカスタムドメイン名を追加する方法を説明します。
exl-id: d441de29-af41-4d3e-9155-531af9702841
source-git-commit: 6bb7b2d056d501d83cf227adb239f7f40f87d0ce
workflow-type: tm+mt
source-wordcount: '326'
ht-degree: 91%

---

# TXT レコードの追加 {#adding-txt}

DNS TXT レコードは、ドメインを CDN サービスでホストすることを許可します。Cloud Manager でカスタムドメインを使用した CDN サービスのデプロイとバックエンドサービスとの関連付けを許可する DNS TXT レコードをゾーンに作成する必要があります。この関連付けは、お客様の管理下にあり、Cloud Manager でサービスからドメインにコンテンツを提供することを認可するものです。この認証は、付与することも、取り下げることもできます。この TXT レコードは、ドメインと Cloud Manager 環境に固有のものです。

TXT レコードを追加する前に、お客様は次の要件を満たす必要があります。

* 組織のドメインの DNS レコードを編集できるか、可能な担当者に問い合わせる必要があります。
* ドメインホストまたは登録機関がわからない場合は、確認する必要があります。

ドメインの検証を開始すると、Cloud Manager で検証に使用する名前と TXT 値が提供されます。指定した名前と値を使用して、ドメインの DNS サーバーに TXT レコードを送信します。

1. ドメインホストにログインし、DNS レコードセクションを見つけます。
1. `_aemverification.[yourdomainname]` を&#x200B;**名前**&#x200B;の値として追加し、TXT 値を表示されるとおりに追加します。

この表の例を参照してください。

| ドメイン | 名前 | TXT 値 |
|--- |--- |---|
| `example.com` | `_aemverification.example.com` | Cloud Manager UI に表示された値全体をコピーします。これは、ドメインと環境に固有のものです。次に例を示します。<br>`adobe-aem-verification=example.com/[program]/[env]/..*` |
| `www.example.com` | `_aemverification.www.example.com` | Cloud Manager UI に表示された値全体をコピーします。これは、ドメインと環境に固有のものです。次に例を示します。<br>`adobe-aem-verification=www.example.com/[program]/[env]/..*` |

完了したら、次のコマンドを実行して結果を確認できます。

```shell
dig _aemverification.[yourdomainname] -t txt
```

期待される結果には、Cloud Manager UI で指定された TXT 値が表示されます。

例えば、ドメインが `example.com` の場合は、次を実行します。

```shell
dig TXT _aemverification.example.com -t txt
```

>[!TIP]
>
>次の項目があります。 [DNS ルックアップツール](https://www.ultratools.com/tools/dnsLookup) 使用可能 Google DoH を使用して、TXT レコードエントリを検索し、TXT レコードが見つからないか、間違っているかを識別できます。
