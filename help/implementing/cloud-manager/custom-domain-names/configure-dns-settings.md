---
title: 'DNS設定の構成 '
description: DNS設定の構成
translation-type: tm+mt
source-git-commit: 1c51560886515e092680c23db3e128758dcd7d99
workflow-type: tm+mt
source-wordcount: '328'
ht-degree: 0%

---


# DNS設定の構成{#configure-dns}

カスタムドメイン名の検証と展開が完了したら、カスタムドメイン名のDNSレコードをDNSプロバイダーで更新する準備が整います。 これにより、サイトで訪問者をサービスできます。 したがって、このアクティビティは通常、Go Liveの前に行われます。

>[!NOTE]
>組織内の適切な担当者が、ログインしたり、DNSプロバイダ(ドメインの購入元の会社)に問い合わせたり、DNS設定で更新を行ったりできる必要があります。

これを行うには、Cloud Managerドメイン名を指すカスタムドメイン名を示す`CNAME`またはApexレコードにDNS設定を設定する必要があるかどうかを決定する必要があります。 `CNAME`またはAレコードがプロビジョニングされると、ドメインのすべてのインターネットトラフィックが、そのドメインがポインティングしている場所にルーティングされます。 その場所がトラフィックを処理するようにプロビジョニングされていない場合は、機能停止が発生します。 テストが済んでいない場合は、コンテンツにエラーがある可能性があります。 このため、テストが完了し、お客様が本番運用を開始できる状態になった後は、常にこの手順を実行します。

## CNAMEレコード{#cname-record}

次のセクションは、DNS構成に適したレコードの種類を判断する際に役立ちます。

「正規名」または「`CNAME`レコード」は、エイリアス名をtrueまたは正規のドメイン名にマップするDNSレコードの一種です。 CNAMEレコードは、通常、`www.example.com`などのサブドメインを、そのサブドメインのコンテンツをホストするドメインにマップするために使用します。

Domain Registrarにログインし、次に示すように、カスタムターゲット名がドメインを指すようにCNAMEレコードを作成します。

| CNAME | Custom Domain Name Point toターゲット |
|--- |--- |
| www.customdomain.com | cdn.adobeaemcloud.com |

## APEXレコード{#apex-record}

apexドメインは、example.comなど、サブドメインを含まないカスタムドメインです。 DNSプロバイダーを通じて、apexドメインは`A`、`ALIAS`、または`ANAME`レコードで構成されます。 Apexドメインは、特定のIPアドレスを指す必要があります。

ドメインプロバイダを追加介して、ドメインのDNS設定に対する次のAレコードすべて：

* `A RECORD`

* `A record for domain @ pointing to IP 151.101.3.10`

* `A record for domain @ pointing to IP 151.101.67.10`

* `A record for domain @ pointing to IP 151.101.131.10`

* `A record for domain @ pointing to IP 151.101.195.10`
