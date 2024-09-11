---
title: カスタムドメイン名を追加
description: Cloud Manager を使用してカスタムドメイン名を追加する方法を説明します。
exl-id: 0fc427b9-560f-4f6e-ac57-32cdf09ec623
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
source-git-commit: dd696580758e7ab9a5427d47fda4275f9ad7997f
workflow-type: tm+mt
source-wordcount: '1488'
ht-degree: 33%

---


# カスタムドメイン名を追加 {#adding-cdn}

Cloud Manager を使用してカスタムドメイン名を追加する方法を説明します。

## 要件 {#requirements}

Cloud Managerでカスタムドメイン名を追加する前に、次の要件を満たします。

* [SSL 証明書の追加 ](/help/implementing/cloud-manager/managing-ssl-certifications/add-ssl-certificate.md) のドキュメントで説明されているように、カスタムドメイン名を追加する前に、追加するドメインのドメイン SSL 証明書を追加する必要があります。
* Cloud Manager でカスタムドメイン名を追加するには、**ビジネスオーナー**&#x200B;または&#x200B;**デプロイメントマネージャー**&#x200B;の役割が必要です。
* Fastly CDN を使用している。

>[!IMPORTANT]
>
>Adobe以外の CDN を使用している場合でも、ドメインをCloud Managerに追加する必要があります。

## カスタムドメイン名を追加する場所 {#}

Cloud Manager では、次の 2 つの場所からカスタムドメイン名を追加できます。

* [ドメイン設定ページから](#adding-cdn-settings)
* [環境ページから](#adding-cdn-environments)

カスタムドメイン名を追加する場合、ドメインは最も具体的で有効な証明書を使用して提供されます。 複数の証明書が同じドメインを持つ場合は、直近に更新されたものが選択されます。重複するドメインがないように証明書を管理することをお勧めします。

このドキュメントで説明するどちらの方法でも、手順は Fastly に基づいています。 別の CDN を使用していた場合は、使用するように選択した CDN でドメインを設定します。

## ドメイン設定ページからカスタムドメイン名を追加します {#adding-cdn-settings}

1. [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) で Cloud Manager にログインし、適切な組織を選択します。

1. **[マイプログラム](/help/implementing/cloud-manager/navigation.md#my-programs)**&#x200B;コンソールで、プログラムを選択します。

1. 左側のナビゲーションパネルで、「**ドメイン設定**」タブを選択します。

   ![ドメイン設定ウィンドウ](/help/implementing/cloud-manager/assets/cdn/cdn-create.png)

1. **ドメイン設定** ページの右上隅付近にある「**ドメインを追加**」をクリックします。

1. **ドメインを追加** ダイアログボックスの **ドメイン名** フィールドに、使用するカスタムドメイン名を入力します。
ドメイン名を入力する際は、`http://`、`https://`、スペースを含めないでください。

1. 「**作成**」をクリックします。

1. **ドメインの検証** ダイアログボックスの **このドメインで使用する証明書の種類を選択してください。ドロップダウンリスト**、次のいずれかのオプションを選択します。

   | 証明書の種類 | 説明 |
   | --- | --- |
   | アドビが管理する証明書 | DV （ドメイン検証）証明書を使用する場合に選択します。 このオプションは、ほとんどの場合に最適で、基本的なドメイン検証を提供します。 Adobeは、証明書を自動的に管理および更新します。 |
   | 顧客が管理する証明書 | EV/OV 証明書を使用する場合に選択します。 このオプションは、EV （拡張検証）または OV （組織検証）によるセキュリティの強化を提供します。 より厳しい検証、より高い信頼レベル、または証明書に対するカスタム制御が必要な場合は、を使用します。 |

1. **ドメインの検証** ダイアログボックスで、選択した証明書の種類に応じて、次のいずれかの操作を行います。

   | 証明書の種類を選択した場合 | 説明 |
   | --- | ---  |
   | アドビが管理する証明書 | 次の手順に進む前に ](#abobe-managed-cert-steps)[Adobe管理の証明書の手順を完了してください。 |
   | 顧客が管理する証明書 | 次の手順に進む前に、[ 顧客が管理する証明書の手順 ](#customer-managed-cert-steps) を完了してください。 |

1. **確認** をクリックします。

1. これで、[SSL 証明書を追加 ](/help/implementing/cloud-manager/managing-ssl-certifications/add-ssl-certificate.md) する準備が整いました。

   >[!NOTE]
   >
   >自己管理 SSL 証明書と自己管理 CDN プロバイダーを使用している場合は、準備ができたら、この手順をスキップして、直接 [CDN 設定の追加 ](/help/implementing/cloud-manager/cdn-configurations/add-cdn-config.md) に進むことができます。



### Adobe管理証明書の手順 {#adobe-managed-cert-steps}

証明書の種類 *Adobe管理証明書* を選択した場合は、[ ドメインの検証 **] ダイアログ ボックスで次の手順を実行し** す。

![Adobe管理証明書の手順 ](/help/implementing/cloud-manager/assets/cdn/cdn-create-adobe-dv-cert.png)

使用中のドメインを確認するには、CNAME を追加して確認する必要があります。

`CNAME` または A レコードは、プロビジョニングされると、ドメインのすべてのインターネットトラフィックを、ポインティングしている場所にルーティングします。 その場所がトラフィックを処理するようにプロビジョニングされていない場合は、機能が一時的に停止します。テストされていない場合は、コンテンツにエラーがある可能性があります。テストが完了し、運用開始の準備が整った後は、この手順が常に実行されるのは、このためです。

これらの設定を行うには、`CNAME` または apex レコードを設定して、カスタムドメイン名がCloud Managerのドメイン名を指すようにする必要があるかどうかを決定します。 このドキュメントの次の節は、DNS 設定に適したレコードタイプを判断するのに役立ちます。

>[!NOTE]
>
>Adobeが管理する CDN の場合、DV （Domain Validation）証明書を使用する場合、ACME 検証が設定されているサイトのみ許可されます。

#### 要件 {#dv-requirements}

DNS レコードを設定する前に、次の要件を満たします。

* ドメインホストまたは登録機関がわからない場合は、確認する。
* 組織のドメインの DNS レコードを編集する、または適切な担当者に連絡できる。
* [ ドメイン名ステータスの確認 ](/help/implementing/cloud-manager/custom-domain-names/check-domain-name-status.md) ドキュメントに記載されているように、設定されたカスタムドメイン名は既に検証されている必要があります。

#### CNAME レコード {#cname-record}

正規名つまり CNAME レコードは、エイリアス名を真のドメイン名つまり正規ドメイン名にマッピングする DNS レコードタイプです。CNAME レコードは、通常、`www.example.com` などのサブドメインを、そのサブドメインのコンテンツをホストするドメインにマッピングするために使用されます。

DNS サービスプロバイダーにログインし、次の表のように、カスタムドメイン名がターゲットを指すように `CNAME` レコードを作成します。

| CNAME | カスタムドメイン名がターゲットを指している |
| --- | --- |
| `www.customdomain.com` | `cdn.adobeaemcloud.com` |

#### APEX レコード {#apex-record}

apex ドメインは、サブドメインを含まないカスタムドメイン（例：`example.com` など）です。DNS プロバイダーを通じて、Apex ドメインは `A`、`ALIAS` または `ANAME` レコードで設定されます。 Apex ドメインは、特定の IP アドレスを指す必要があります。

ドメインプロバイダーを介してドメインの DNS 設定に次の `A` レコードを追加します。

* `A RECORD`

* `A record for domain @ pointing to IP 151.101.3.10`

* `A record for domain @ pointing to IP 151.101.67.10`

* `A record for domain @ pointing to IP 151.101.131.10`

* `A record for domain @ pointing to IP 151.101.195.10`



### 顧客管理証明書の手順 {#customer-managed-cert-steps}

証明書の種類 *顧客が管理する証明書* を選択した場合は、**ドメインの検証** ダイアログボックスで次の手順を実行します。

![ 顧客管理証明書の手順 ](/help/implementing/cloud-manager/assets/cdn/cdn-create-customer-cert.png)

使用中のドメインを確認するには、TXT レコードを追加して検証する必要があります。

テキストレコード（TXT レコードとも呼ばれる）は、ドメインネームシステム（DNS）のリソースレコードのタイプです。任意のテキストをホスト名に関連付けることができます。 このテキストには、サーバーやネットワーク情報など、人間が読み取れる詳細が含まれている場合があります。

Cloud Manager では、特定の TXT レコードを使用して、ドメインを CDN サービスでホストすることを認証します。Cloud Managerにカスタムドメインを使用した CDN サービスのデプロイとバックエンドサービスとの関連付けを許可する DNS TXT レコードをゾーンに作成します。 この関連付けは、お客様の管理下にあり、Cloud Manager でサービスからドメインにコンテンツを提供することを認可するものです。この認証は、付与することも、取り下げることもできます。TXT レコードは、ドメインと Cloud Manager 環境に固有のものです。

## 要件 {#requirements-customer-cert}

TXT レコードを追加する前に、次の要件を満たします。

* ドメインホストまたは登録機関がわからない場合は、確認する。
* 組織のドメインの DNS レコードを編集する、または適切な担当者に連絡できる。
* まず、この記事で前述したように、カスタムドメイン名を追加します。

## 検証用の TXT レコードを追加 {#verification}

1. **ドメインを検証** ダイアログボックスで、Cloud Managerは検証に使用する名前と TXT 値を表示します。 この値をコピーします。

1. DNS サービスプロバイダーにログインし、「DNS レコード」セクションを見つけます。

1. `aemverification.[yourdomainname]` を値の **名前** として追加し、TXT 値を「**ドメイン名**」フィールドに表示されるとおりに追加します。

   **TXT レコードの例**

   | ドメイン | 名前 | TXT 値 |
   | --- | --- | --- |
   | `example.com` | `_aemverification.example.com` | Cloud Manager UI に表示された値全体をコピーします。 この値は、ドメインと環境に固有の値です。 次に例を示します。<br>`adobe-aem-verification=example.com/[program]/[env]/..*` |
   | `www.example.com` | `_aemverification.www.example.com` | Cloud Manager UI に表示された値全体をコピーします。 この値は、ドメインと環境に固有の値です。 次に例を示します。<br>`adobe-aem-verification=www.example.com/[program]/[env]/..*` |

1. TXT レコードをドメインホストに保存します。

## TXT レコードを検証 {#verify}

完了したら、次のコマンドを実行して結果を確認できます。

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
>使用可能な [DNS ルックアップツール](https://www.ultratools.com/tools/dnsLookup)がいくつかあります。Google DoH を使用すると、TXT レコードエントリを検索し、TXT レコードが見つからないか、間違っているかを識別できます。

>[!NOTE]
>
>DNS の生成遅延が原因で、DNS 検証の処理に数時間かかる場合があります。
>
>Cloud Managerは、所有権を確認し、ステータスを更新します。これらのステータスは、「ドメイン設定」テーブルに表示されます。 詳しくは [ カスタムドメイン名のステータスの確認 ](/help/implementing/cloud-manager/custom-domain-names/check-domain-name-status.md) を参照してください。

<!--
## Next Steps {#next-steps}

Now that you created your TXT entry, you can verify your domain name status. Proceed to the document [Checking Domain Name Status](/help/implementing/cloud-manager/custom-domain-names/check-domain-name-status.md) to continue setting up your custom domain name. -->

>[!TIP]
>
>TXT エントリと CNAME または A レコードは、管理する DNS サーバ上で同時に設定できるため、時間を節約できます。
>
><!-- To do this, review the entire process of setting up a custom domain name as detailed in the document [Introduction to custom domain names](/help/implementing/cloud-manager/custom-domain-names/introduction.md) taking special note of the document [help/implementing/cloud-manager/custom-domain-names/configure-dns-settings.md](/help/implementing/cloud-manager/custom-domain-names/configure-dns-settings.md) and update your DNS settings appropriately. -->


## 環境ページからのカスタムドメイン名の追加 {#adding-cdn-environments}

**環境** ページからカスタムドメイン名を追加する手順は、[ ドメイン設定ページからカスタムドメイン名を追加する ](#adding-cdn-settings) 場合と同じですが、エントリポイントが異なります。 **環境**&#x200B;ページからカスタムドメイン名を追加するには、次の手順に従います。

1. [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) で Cloud Manager にログインし、適切な組織とプログラムを選択します。

1. 対象となる環境の **環境の詳細** 詳細ページに移動します。

   ![環境の詳細ページでのドメイン名の入力](/help/implementing/cloud-manager/assets/cdn/cdn-create4.png)

1. **ドメイン名**&#x200B;テーブルを使用してカスタムドメイン名を送信します。

   1. カスタムドメイン名を入力します。
   1. この名前に関連付けられている SSL 証明書をドロップダウンリストから選択します。
   1. 「**+追加**」をクリックします。

   ![ カスタムドメイン名の追加 ](/help/implementing/cloud-manager/assets/cdn/cdn-create3.png)

1. **ドメイン名を追加** ダイアログボックスが開き、「**ドメイン名**」タブが表示されます。 [ ドメイン設定ページからのカスタムドメイン名の追加 ](#adding-cdn-settings) の場合と同様に続行します。—>
