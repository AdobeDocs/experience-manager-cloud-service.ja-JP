---
title: DNS 設定の指定
description: カスタムドメイン名の DNS 設定を指定する方法を説明します。
exl-id: 6e294f0b-52cb-40dd-bc42-ddbcffdf5600
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
source-git-commit: 646ca4f4a441bf1565558002dcd6f96d3e228563
workflow-type: tm+mt
source-wordcount: '337'
ht-degree: 100%

---

# DNS 設定の指定 {#configure-dns}

カスタムドメイン名が正常に検証されデプロイされたら、使用する DNS プロバイダーをカスタムドメイン名の DNS レコードに反映させる準備が整います。この作業を行うと、サイトで訪問者にサービスを提供できます。したがって、このアクティビティは通常、運用開始より前に行われます。

## DNS 設定とは {#dns-settings}

`CNAME` または A レコードがプロビジョニングされると、ドメインのすべてのインターネットトラフィックが、そのレコードが指している場所にルーティングされます。その場所がトラフィックを処理するようにプロビジョニングされていない場合は、機能が一時的に停止します。テストされていない場合は、コンテンツにエラーがある可能性があります。テストが完了し、運用開始の準備が整った後は、この手順が常に実行されるのは、このためです。

これらの設定を行うには、カスタムドメイン名が Cloud Manager ドメイン名を指すように、`CNAME` または Apex レコードを設定する必要があるかどうかを判断する必要があります。この後の節は、DNS 設定に適したレコードタイプを判断するうえで役に立ちます。

>[!NOTE]
>
>組織内の担当者が、DNS プロバイダー（ドメインの購入元の会社）にログインまたは問い合わせを行ったり、DNS 設定を更新したりできる必要があります。

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
