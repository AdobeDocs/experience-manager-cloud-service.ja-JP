---
title: TXT レコードの追加
description: TXT レコードを追加して、Cloud Manager でカスタムドメイン名を追加する方法を説明します。
exl-id: d441de29-af41-4d3e-9155-531af9702841
source-git-commit: 491e710223c5878bfa81c4b0a57d18ec0ec29479
workflow-type: tm+mt
source-wordcount: '332'
ht-degree: 30%

---

# TXT レコードの追加 {#adding-txt}

DNS TXT レコードは、CDN サービスでホストされるドメインを承認します。 Cloud Manager が CDN サービスをカスタムドメインでデプロイし、バックエンドサービスに関連付けることを許可する DNS TXT レコードをゾーンに作成する必要があります。 この関連付けはお客様が管理下に置かれ、Cloud Manager がサービスからドメインにコンテンツを提供することを許可します。 この認可は、取り下げられる場合と同様に、許可される場合があります。 この TXT レコードは、ドメインと Cloud Manager 環境に固有のものです。

TXT レコードを追加する前に、次の要件を満たす必要があります。

* 組織のドメインの DNS レコードを変更する権限を持っているか、または可能な担当者に問い合わせる必要があります。
* ドメインホストまたはレジストラを既に知らない場合は識別する必要があります。

ドメインの検証を開始すると、Cloud Manager で検証に使用する名前と TXT 値が提供されます。指定した名前と値を使用して、ドメインの DNS サーバーに TXT レコードを追加します。

1. ドメインホストにログインし、DNS レコードセクションを見つけます。
1. 追加 `_aemverification.[yourdomainname]` を **名前** の値を入力し、TXT 値を表示されるとおりに追加します。

この表の例を参照してください。

| ドメイン | 名前 | TXT 値 |
|--- |--- |---|
| `example.com` | `_aemverification.example.com` | Cloud Manager UI に表示された値全体をコピーします。 これは、ドメインと環境に固有のものです。 例：<br>`adobe-aem-verification=example.com/[program]/[env]/..*` |
| `www.example.com` | `_aemverification.www.example.com` | Cloud Manager UI に表示された値全体をコピーします。 これは、ドメインと環境に固有のものです。 例：<br>`adobe-aem-verification=www.example.com/[program]/[env]/..*` |

完了したら、次のコマンドを実行して結果を確認できます

```shell
dig _aemverification.[yourdomainname] -t txt
```

期待される結果には、Cloud Manager UI で指定された TXT 値が表示されます。

例えば、ドメインが `example.com`、次にを実行します。

```shell
dig TXT _aemverification.example.com -t txt
```

>[!TIP]
>
>多くの [DNS ルックアップツール](https://www.ultratools.com/tools/dnsLookup) 使用可能 Google DoH を使用して、TXT レコードエントリを検索し、TXT レコードが見つからないか、間違っているかを識別できます。
