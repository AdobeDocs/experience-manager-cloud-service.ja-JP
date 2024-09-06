---
title: TXT レコードの追加
description: Cloud Manager で使用するカスタムドメインの所有権を検証するために、TXT レコードを追加する方法について説明します。
exl-id: d441de29-af41-4d3e-9155-531af9702841
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
source-git-commit: 5d6d3374f2dd95728b2d3ed0cf6fab4092f73568
workflow-type: tm+mt
source-wordcount: '635'
ht-degree: 93%

---


# TXT レコードの追加 {#adding-txt}

Cloud Manager で使用するカスタムドメインの所有権を検証するために、TXT レコードを追加する方法について説明します。

## TXT レコードとは {#what-is}

テキストレコード（TXT レコードとも呼ばれる）は、ドメインネームシステム（DNS）のリソースレコードのタイプです。サーバーやネットワーク情報などのホスト名に関して人が判読できる情報など、任意のテキストをホスト名に関連付ける機能を提供します。

Cloud Manager では、特定の TXT レコードを使用して、ドメインを CDN サービスでホストすることを認証します。Cloud Manager でカスタムドメインを使用した CDN サービスのデプロイとバックエンドサービスとの関連付けを許可する DNS TXT レコードをゾーンに作成する必要があります。この関連付けは、お客様の管理下にあり、Cloud Manager でサービスからドメインにコンテンツを提供することを認可するものです。この認証は、付与することも、取り下げることもできます。TXT レコードは、ドメインと Cloud Manager 環境に固有のものです。

## 要件 {#requirements}

TXT レコードを追加する前に、お客様は次の要件を満たす必要があります。

* ドメインホストまたは登録機関がわからない場合は、確認する必要があります。
* 組織のドメインの DNS レコードを編集できる、またはそれが可能な適切な担当者に連絡できなければなりません。
* 最初に、[ カスタムドメイン名の追加 ](/help/implementing/cloud-manager/custom-domain-names/add-custom-domain-name.md) ドキュメントの説明に従ってカスタムドメイン名を追加する必要があります。

## 検証用の TXT レコードの追加 {#verification}

Cloud Manager で使用されるカスタムドメイン名の検証の一環として、TXT レコードが追加されます。

1. 最初に、[ カスタムドメイン名の追加 ](/help/implementing/cloud-manager/custom-domain-names/add-custom-domain-name.md) ドキュメントの説明に従ってカスタムドメイン名を追加する必要があります。

1. **ドメイン名を追加**&#x200B;ダイアログの「**検証**」タブで、Cloud Manager は検証に使用する名前と TXT 値を表示します。この値をコピーします。

   ![ドメイン名の検証](/help/implementing/cloud-manager/assets/cdn/cdn-create6.png)

1. ドメインホストにログインし、DNS レコードセクションを見つけます。

1. 値の&#x200B;**名前**&#x200B;として `_aemverification.[yourdomainname]` を追加し、**ドメイン名を追加**&#x200B;ダイアログの表示に従って TXT 値を追加します。

   * [ 次の節の例 ](#examples) を参照してください。

1. TXT レコードをドメインホストに保存します。

## TXT レコードの例 {#examples}

| ドメイン | 名前 | TXT 値 |
|--- |--- |---|
| `example.com` | `_aemverification.example.com` | Cloud Manager UI に表示された値全体をコピーします。これは、ドメインと環境に固有のものです。次に例を示します。<br>`adobe-aem-verification=example.com/[program]/[env]/..*` |
| `www.example.com` | `_aemverification.www.example.com` | Cloud Manager UI に表示された値全体をコピーします。これは、ドメインと環境に固有のものです。次に例を示します。<br>`adobe-aem-verification=www.example.com/[program]/[env]/..*` |

## TXT レコードの検証 {#verify}

完了したら、次のコマンドを実行して結果を検証できます。

```shell
dig _aemverification.[yourdomainname] -t txt
```

予期される結果には、Cloud Manager UI の&#x200B;**ドメイン名を追加**&#x200B;ダイアログの「**検証**」タブで指定した TXT 値が表示されます。

例えば、ドメインが `example.com` の場合は、次を実行します。

```shell
dig TXT _aemverification.example.com -t txt
```

>[!TIP]
>
>使用可能な [DNS ルックアップツール](https://www.ultratools.com/tools/dnsLookup)がいくつかあります。Google DoH を使用して、TXT レコードエントリを検索し、TXT レコードが見つからないか、間違っているかを識別できます。

>[!NOTE]
>
>DNS の生成遅延が原因で、DNS 検証の処理に数時間かかる場合があります。
>
>Cloud Manager が所有権を検証し、ドメイン設定テーブルに表示されるステータスを更新します。詳しくは、[カスタムドメイン名のステータスの確認](/help/implementing/cloud-manager/custom-domain-names/check-domain-name-status.md)を参照してください。

## 次の手順 {#next-steps}

TXT エントリを作成したら、ドメイン名のステータスを検証できます。カスタムドメイン名の設定を続行するには、[ドメイン名のステータスの確認](/help/implementing/cloud-manager/custom-domain-names/check-domain-name-status.md)ドキュメントに進んでください。

>[!TIP]
>
>TXT エントリと CNAME または A レコードは、管理する DNS サーバーで同時に設定できるので、時間を節約できます。
>
>これを実行する場合は、まず、[カスタムドメイン名の概要](/help/implementing/cloud-manager/custom-domain-names/introduction.md)ドキュメントに記載されているカスタムドメイン名の設定プロセス全体を確認し、特に [help/implementing/cloud-manager/custom-domain-names/configure-dns-settings.md](/help/implementing/cloud-manager/custom-domain-names/configure-dns-settings.md) ドキュメントに注意して、DNS 設定を適切に更新してください。