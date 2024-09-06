---
title: DNS 設定の指定
description: カスタムドメイン名の DNS 設定を指定して、サイトで訪問者にサービスを提供できるようにする方法について説明します。
exl-id: 6e294f0b-52cb-40dd-bc42-ddbcffdf5600
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
source-git-commit: 5d6d3374f2dd95728b2d3ed0cf6fab4092f73568
workflow-type: tm+mt
source-wordcount: '416'
ht-degree: 95%

---


# DNS 設定の指定 {#configure-dns}

カスタムドメイン名が正常に[検証され、デプロイ](/help/implementing/cloud-manager/custom-domain-names/check-domain-name-status.md)されたら、DNS プロバイダーを使用してカスタムドメイン名の DNS レコードを更新する準備が整います。この作業を行うと、サイトで訪問者にサービスを提供できます。したがって、このアクティビティは通常、運用開始より前に行われます。

## DNS 設定とは {#dns-settings}

`CNAME` または A レコードがプロビジョニングされると、ドメインのすべてのインターネットトラフィックが、そのレコードが指している場所にルーティングされます。その場所がトラフィックを処理するようにプロビジョニングされていない場合は、機能が一時的に停止します。テストされていない場合は、コンテンツにエラーがある可能性があります。テストが完了し、運用開始の準備が整った後は、この手順が常に実行されるのは、このためです。

これらの設定を行うには、カスタムドメイン名が Cloud Manager ドメイン名を指すように、`CNAME` または apex レコードを設定する必要があるかどうかを判断する必要があります。このドキュメントの後の節は、DNS 設定に適したレコードタイプを判断するうえで役に立ちます。

## 要件 {#requirements}

DNS レコードを設定する前に、次の要件を満たす必要があります。

* ドメインホストまたは登録機関がわからない場合は、確認する必要があります。
* 組織のドメインの DNS レコードを編集できる、またはそれが可能な適切な担当者に連絡できなければなりません。
* [ ドメイン名ステータスの確認 ](/help/implementing/cloud-manager/custom-domain-names/check-domain-name-status.md) ドキュメントに記載されているように、設定されたカスタムドメイン名は既に検証されている必要があります。

## CNAME レコード {#cname-record}

正規名つまり CNAME レコードは、エイリアス名を真のドメイン名つまり正規ドメイン名にマッピングする DNS レコードタイプです。CNAME レコードは、通常、`www.example.com` などのサブドメインを、そのサブドメインのコンテンツをホストするドメインにマッピングするために使用されます。

ドメイン登録機関にログインし、次のテーブルのように、カスタムドメイン名がターゲットを指すように `CNAME` レコードを作成します。

| CNAME | カスタムドメイン名の参照先 |
|--- |--- |
| `www.customdomain.com` | `cdn.adobeaemcloud.com` |

## APEX レコード {#apex-record}

apex ドメインは、サブドメインを含まないカスタムドメイン（例：`example.com` など）です。DNS プロバイダーを通じて、Apex ドメインは `A`、`ALIAS`、`ANAME` のいずれかのレコードで設定されます。Apex ドメインは、特定の IP アドレスを指す必要があります。

ドメインプロバイダーを介してドメインの DNS 設定に次の `A` レコードを追加します。

* `A RECORD`

* `A record for domain @ pointing to IP 151.101.3.10`

* `A record for domain @ pointing to IP 151.101.67.10`

* `A record for domain @ pointing to IP 151.101.131.10`

* `A record for domain @ pointing to IP 151.101.195.10`

## 次の手順 {#next-steps}

カスタムドメイン名の DNS レコードを設定したら、Cloud Manager でこれらの設定を検証する必要があります。カスタムドメイン名を完成するには、[DNS レコードのステータスの確認](/help/implementing/cloud-manager/custom-domain-names/check-dns-record-status.md)ドキュメントに進んでください。
