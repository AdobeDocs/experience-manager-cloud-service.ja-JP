---
title: TXT レコードの追加
description: TXT レコードを追加して、Cloud Managerで使用するカスタムドメインの所有権を確認する方法を説明します。
exl-id: d441de29-af41-4d3e-9155-531af9702841
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
source-git-commit: 06e961febd7cb2ea1d8fca00cb3dee7f7ca893c9
workflow-type: tm+mt
source-wordcount: '635'
ht-degree: 32%

---


# TXT レコードの追加 {#adding-txt}

TXT レコードを追加して、Cloud Managerで使用するカスタムドメインの所有権を確認する方法を説明します。

## TXT レコードとは {#what-is}

テキストレコード（TXT レコードとも呼ばれます）は、ドメインネームシステム（DNS）のリソースレコードの一種です。 任意のテキストをホスト名に関連付ける機能を提供します。例えば、サーバーやネットワーク情報などのホスト名に関する人間が読み取れる情報などです。

Cloud Managerは、特定の TXT レコードを使用して、ドメインを CDN サービスでホストすることを認証します。 Cloud Managerにカスタムドメインを使用した CDN サービスのデプロイとバックエンドサービスとの関連付けを許可する DNS TXT レコードをゾーンに作成する必要があります。 この関連付けは、お客様の管理下にあり、Cloud Manager でサービスからドメインにコンテンツを提供することを認可するものです。この認証は、付与することも、取り下げることもできます。この TXT レコードは、ドメインとCloud Manager環境に固有のものです。

## 要件 {#requirements}

TXT レコードを追加する前に、お客様は次の要件を満たす必要があります。

* ドメインホストまたは登録機関がわからない場合は、確認する必要があります。
* 組織のドメインの DNS レコードを編集できる、またはそれが可能な適切な担当者に連絡できなければなりません。
* 最初に、[ カスタムドメイン名の追加 ](/help/implementing/cloud-manager/custom-domain-names/add-custom-domain-name.md) ドキュメントの説明に従ってカスタムドメイン名を追加する必要があります。

## 検証用の TXT レコードの追加 {#verification}

TXT レコードは、Cloud Managerで使用するカスタムドメイン名の検証の一環として追加されます。

1. 最初に、[ カスタムドメイン名の追加 ](/help/implementing/cloud-manager/custom-domain-names/add-custom-domain-name.md) ドキュメントの説明に従ってカスタムドメイン名を追加する必要があります。

1. **ドメイン名を追加** ダイアログの **検証** タブで、Cloud Managerは検証に使用する名前と TXT 値を表示します。 この値をコピーします。

   ![ドメイン名の検証](/help/implementing/cloud-manager/assets/cdn/cdn-create6.png)

1. ドメインホストにログインし、DNS レコード セクションを見つけます。

1. `_aemverification.[yourdomainname]` を値の **名前** として追加し、TXT 値を **ドメイン名を追加** ダイアログに表示されるとおりに追加します。

   * [ 次の節の例 ](#examples) を参照してください。

1. TXT レコードをドメインホストに保存します。

## TXT レコードの例 {#examples}

| ドメイン | 名前 | TXT 値 |
|--- |--- |---|
| `example.com` | `_aemverification.example.com` | Cloud Manager UI に表示された値全体をコピーします。これは、ドメインと環境に固有のものです。次に例を示します。<br>`adobe-aem-verification=example.com/[program]/[env]/..*` |
| `www.example.com` | `_aemverification.www.example.com` | Cloud Manager UI に表示された値全体をコピーします。これは、ドメインと環境に固有のものです。次に例を示します。<br>`adobe-aem-verification=www.example.com/[program]/[env]/..*` |

## TXT レコードの検証 {#verify}

完了したら、次のコマンドを実行して結果を確認できます。

```shell
dig _aemverification.[yourdomainname] -t txt
```

期待される結果には、Cloud Manager UI の **ドメイン名を追加** ダイアログの「**検証**」タブで指定された TXT 値が表示されます。

例えば、ドメインが `example.com` の場合は、次を実行します。

```shell
dig TXT _aemverification.example.com -t txt
```

>[!TIP]
>
>使用可能な [DNS ルックアップツール](https://www.ultratools.com/tools/dnsLookup)がいくつかあります。Google DoH を使用して、TXT レコードエントリを検索し、TXT レコードが見つからないか、間違っているかを識別できます。

>[!NOTE]
>
>DNS の伝播遅延が原因で、DNS 検証の処理に数時間かかる場合があります。
>
>Cloud Manager が所有権を検証し、ドメイン設定テーブルに表示されるステータスを更新します。詳しくは、[カスタムドメイン名のステータスの確認](/help/implementing/cloud-manager/custom-domain-names/check-domain-name-status.md)を参照してください。

## 次の手順 {#next-steps}

TXT エントリを作成したので、ドメイン名のステータスを確認できます。 [ ドメイン名ステータスの確認 ](/help/implementing/cloud-manager/custom-domain-names/check-domain-name-status.md) ドキュメントに進んで、カスタムドメイン名の設定を続行します。

>[!TIP]
>
>TXT エントリと CNAME または A レコードは、管理する DNS サーバ上で同時に設定できるため、時間を節約できます。
>
>これを行う場合は、最初に [ カスタムドメイン名の概要 ](/help/implementing/cloud-manager/custom-domain-names/introduction.md) ドキュメント [help/implementing/cloud-manager/custom-domain-names/configure-dns-settings.mdに記載されている通り、カスタムドメイン名を設定するプロセス全体を確認し、適切に DNS 設定を更新してください ](/help/implementing/cloud-manager/custom-domain-names/configure-dns-settings.md)。