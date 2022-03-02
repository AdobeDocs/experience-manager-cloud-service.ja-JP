---
title: 'DNS 設定の指定 '
description: DNS 設定の指定
exl-id: 6e294f0b-52cb-40dd-bc42-ddbcffdf5600
source-git-commit: 016954bc712a135886a6031deba05d92e7d5099c
workflow-type: tm+mt
source-wordcount: '508'
ht-degree: 100%

---

# DNS 設定の指定 {#configure-dns}

カスタムドメイン名が正常に検証されデプロイされたら、使用する DNS プロバイダーをカスタムドメイン名の DNS レコードに反映させる準備が整います。この作業を行うと、サイトで訪問者にサービスを提供できます。したがって、このアクティビティは通常、運用開始より前に行われます。

>[!NOTE]
>組織内の担当者が、DNS プロバイダー（ドメインの購入元の会社）にログインまたは問い合わせを行ったり、DNS 設定を更新したりできる必要があります。

それには、カスタムドメイン名が Cloud Manager ドメイン名を指すように `CNAME` または Apex レコードに DNS 設定を指定する必要があるかどうかを決定する必要があります。`CNAME` または A レコードがプロビジョニングされると、ドメインのすべてのインターネットトラフィックが、そのレコードが指している場所にルーティングされます。その場所がトラフィックを処理するようにプロビジョニングされていない場合は、機能が一時的に停止します。テストされていない場合は、コンテンツにエラーがある可能性があります。このため、テストが完了し、顧客が運用を開始できる状態になったら、必ずこの手順を実行します。

次の表に示す手順を完了する必要があります。

| 手順 |  | 担当 | 詳細情報 |
|--- |--- |--- |---|
| SSL 証明書を追加 | SSL 証明書を追加 | 顧客 | [SSL 証明書の追加](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/manage-ssl-certificates/add-ssl-certificate.html?lang=ja) |
| ドメイン検証 | TXT レコードを追加 | 顧客 | [TXT レコードの追加](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/custom-domain-names/add-text-record.html?lang=ja) |
| ドメイン検証ステータスを確認 |  | 顧客 |  |
|  | ステータス：ドメイン検証エラー | 顧客 | [ドメイン名ステータスの確認](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/custom-domain-names/check-domain-name-status.html?lang=ja) |
|  | ステータス：検証済み、デプロイメントに失敗 | アドビ担当者に問い合わせ | [ドメイン名ステータスの確認](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/custom-domain-names/check-domain-name-status.html?lang=en) |
| CNAME または APEX レコードを追加して、AEM as a Cloud Service を指す DNS レコードを追加 | DNS 設定を指定 | 顧客 | [DNS 設定の指定](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/custom-domain-names/configure-dns-settings.html?lang=ja) |
| DNS レコードのステータスを確認 |  | 顧客 | [DNS レコードのステータスの確認](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/custom-domain-names/check-dns-record-status.html?lang=ja) |
|  | ステータス：DNS ステータスが検出されない | 顧客 | [DNS レコードのステータスの確認](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/custom-domain-names/check-dns-record-status.html?lang=en) |
|  | ステータス：DNS が正しく解決されない | 顧客 |  |


## CNAME レコード {#cname-record}

この後の節は、DNS 設定に適したレコードタイプを判断するうえで役に立ちます。

正規名つまり `CNAME` レコードは、エイリアス名を真のドメイン名つまり正規ドメイン名にマッピングする DNS レコードタイプです。CNAME レコードは、通常、`www.example.com` などのサブドメインを、そのサブドメインのコンテンツをホストするドメインにマッピングするために使用されます。

ドメイン登録機関にログインし、カスタムドメイン名が下記のターゲットを指すように CNAME レコードを作成します。

| CNAME | カスタムドメイン名の参照先 |
|--- |--- |
| www.customdomain.com | cdn.adobeaemcloud.com |

## APEX レコード {#apex-record}

apex ドメインは、サブドメインを含まないカスタムドメイン（例：example.com など）です。DNS プロバイダーを通じて、Apex ドメインは `A`、`ALIAS`、`ANAME` のいずれかのレコードで設定されます。Apex ドメインは、特定の IP アドレスを指す必要があります。

ドメインプロバイダーを通じて、ドメインの DNS 設定に次の A レコードをすべて追加します。

* `A RECORD`

* `A record for domain @ pointing to IP 151.101.3.10`

* `A record for domain @ pointing to IP 151.101.67.10`

* `A record for domain @ pointing to IP 151.101.131.10`

* `A record for domain @ pointing to IP 151.101.195.10`
