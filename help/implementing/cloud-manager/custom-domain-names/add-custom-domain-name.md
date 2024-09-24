---
title: カスタムドメイン名の追加
description: Cloud Manager を使用してカスタムドメイン名を追加する方法を説明します。
exl-id: 0fc427b9-560f-4f6e-ac57-32cdf09ec623
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
source-git-commit: 2d1382c84d872719332986baa5829d1623d9d9a6
workflow-type: tm+mt
source-wordcount: '1489'
ht-degree: 93%

---


# カスタムドメイン名の追加 {#adding-cdn}

Cloud Manager を使用してカスタムドメイン名を追加する方法を説明します。

## 要件 {#requirements}

Cloud Manager でカスタムドメイン名を追加する前に、次の要件を満たす必要があります。

* [SSL 証明書の追加 ](/help/implementing/cloud-manager/managing-ssl-certifications/add-ssl-certificate.md) のドキュメントに記載されているように、カスタムドメイン名を追加する前に、追加するドメインのドメイン SSL 証明書を追加する必要があります。
* Cloud Manager でカスタムドメイン名を追加するには、**ビジネスオーナー**&#x200B;または&#x200B;**デプロイメントマネージャー**&#x200B;の役割が必要です。
* Fastly または他の CDN （コンテンツ配信ネットワーク）を使用している。

>[!IMPORTANT]
>
>アドビ以外の CDN を使用する場合でも、ドメインを Cloud Manager に追加する必要があります。

## カスタムドメイン名の追加先 {#where-to-add-cdn}

カスタムドメイン名は、Cloud Managerの次の 2 つの場所から追加できます。

* [ドメイン設定ページ](#adding-cdn-settings)
* [環境ページ](#adding-cdn-environments)

カスタムドメイン名を追加する場合、最も具体的で有効な証明書を使用してドメインが提供されます。複数の証明書が同じドメインを持つ場合は、直近に更新されたものが選択されます。重複するドメインがないように証明書を管理することをお勧めします。

このドキュメントで説明するどちらの方法の手順も、Fastly に基づいています。別の CDN （コンテンツ配信ネットワーク）を使用している場合は、使用するように選択した CDN でドメインを設定します。

## カスタムドメイン名の追加 {#adding-cdn-settings}

1. [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) で Cloud Manager にログインし、適切な組織を選択します。

1. **[マイプログラム](/help/implementing/cloud-manager/navigation.md#my-programs)**&#x200B;コンソールで、プログラムを選択します。

1. サイドメニューの **サービス** で、**ドメイン設定** を選択します。

   ![ドメイン設定ウィンドウ](/help/implementing/cloud-manager/assets/cdn/cdn-create.png)

1. **ドメイン設定**&#x200B;ページの右上隅付近にある「**ドメインを追加**」をクリックします。

1. **ドメインを追加**&#x200B;ダイアログボックスの「**ドメイン名**」フィールドに、使用するカスタムドメイン名を入力します。
ドメイン名を入力する際は、`http://`、`https://`、スペースを含めないでください。

1. 「**作成**」をクリックします。

1. **ドメインを検証**&#x200B;ダイアログボックスの&#x200B;**このドメインで使用する予定の証明書タイプは何ですか?**&#x200B;ドロップダウンリストで、次のオプションのいずれかを選択します。

   | 証明書の種類オプション | 説明 |
   | --- | --- |
   | アドビが管理する証明書 | DV（ドメイン検証）証明書を使用する場合に選択します。このオプションは、ほとんどの場合に最適で、基本的なドメイン検証を提供します。証明書は、アドビによって管理され、自動的に更新されます。 |
   | 顧客が管理する証明書 | EV または OV 証明書を使用する場合に選択します。このオプションでは、EV（拡張検証）または OV（組織検証）でセキュリティが強化されます。より厳しい検証、より高い信頼レベル、証明書に対するカスタム管理のいずれかが必要な場合に使用します。 |

1. **ドメインを検証**&#x200B;ダイアログボックスで、選択した証明書タイプに応じて、次のいずれかを行います。

   | 選択した証明書タイプ | 説明 |
   | --- | ---  |
   | アドビが管理する証明書 | [アドビが管理する証明書の手順](#adobe-managed-cert-steps)を完了してから、次の手順に進みます。 |
   | 顧客が管理する証明書 | [顧客が管理する証明書の手順](#customer-managed-cert-steps)を完了してから、次の手順に進みます。 |

1. 「**確認**」をクリックします。

1. これで、[SSL 証明書を追加](/help/implementing/cloud-manager/managing-ssl-certifications/add-ssl-certificate.md)する準備が整いました。

   >[!NOTE]
   >
   >自己管理 SSL 証明書と自己管理 CDN プロバイダーを使用している場合は、この手順をスキップして、準備ができたら直接 [CDN 設定の追加](/help/implementing/cloud-manager/cdn-configurations/add-cdn-config.md)に進むことができます。


### アドビが管理する証明書の手順 {#adobe-managed-cert-steps}

証明書タイプとして「*アドビが管理する証明書*」を選択した場合は、**ドメインを検証**&#x200B;ダイアログボックスで次の手順を完了します。

![アドビが管理する証明書の手順](/help/implementing/cloud-manager/assets/cdn/cdn-create-adobe-dv-cert.png)

使用中のドメインを検証するには、CNAME を追加して検証する必要があります。

ある `CNAME` またはレコードがプロビジョニングされると、ドメインのすべてのインターネットトラフィックが、そのレコードが指している場所にルーティングされます。その場所がトラフィックを処理するようにプロビジョニングされていない場合は、機能が一時的に停止します。テストされていない場合は、コンテンツにエラーがある可能性があります。この手順が常にテストが完了し運用開始の準備が整った後に実行されるのは、このためです。

これらの設定を行うには、カスタムドメイン名が Cloud Manager ドメイン名を指すように、`CNAME` または Apex レコードを設定する必要があるかどうかを判断します。このドキュメントの後の節は、DNS 設定に適したレコードタイプを判断するうえで役に立ちます。

>[!NOTE]
>
>アドビが管理する CDN の場合、DV（ドメイン検証）証明書を使用する際は、ACME 検証済みのサイトのみが許可されます。

#### 要件 {#adobe-managed-cert-dv-requirements}

DNS レコードを設定する前に、次の要件を満たす必要があります。

* ドメインホストまたは登録機関がわからない場合は確認します。
* 組織のドメインの DNS レコードを編集できる、またはそれが可能な適切な担当者に連絡できる必要があります。
* [ドメイン名のステータスの確認](/help/implementing/cloud-manager/custom-domain-names/check-domain-name-status.md)ドキュメントの説明に従って、設定済みのカスタムドメイン名の検証をすでに済ませている必要があります。

#### CNAME レコード {#adobe-managed-cert-cname-record}

正規名つまり CNAME レコードは、エイリアス名を真のドメイン名つまり正規ドメイン名にマッピングする DNS レコードタイプです。CNAME レコードは、通常、`www.example.com` などのサブドメインを、そのサブドメインのコンテンツをホストするドメインにマッピングするために使用されます。

DNS サービスプロバイダーにログインし、次のテーブルのように、カスタムドメイン名がターゲットを指すように `CNAME` レコードを作成します。

| CNAME | カスタムドメイン名の参照先 |
| --- | --- |
| `www.customdomain.com` | `cdn.adobeaemcloud.com` |

#### APEX レコード {#adobe-managed-cert-apex-record}

apex ドメインは、サブドメインを含まないカスタムドメイン（例：`example.com` など）です。DNS プロバイダーを通じて、Apex ドメインは `A`、`ALIAS`、`ANAME` のいずれかのレコードで設定されます。Apex ドメインは、特定の IP アドレスを指す必要があります。

ドメインプロバイダーを介してドメインの DNS 設定に次の `A` レコードを追加します。

* `A RECORD`

* `A record for domain @ pointing to IP 151.101.3.10`

* `A record for domain @ pointing to IP 151.101.67.10`

* `A record for domain @ pointing to IP 151.101.131.10`

* `A record for domain @ pointing to IP 151.101.195.10`


### 顧客が管理する証明書の手順 {#customer-managed-cert-steps}

証明書タイプとして「*顧客が管理する証明書*」を選択した場合は、**ドメインを検証**&#x200B;ダイアログボックスで次の手順を完了します。

![顧客が管理する証明書の手順](/help/implementing/cloud-manager/assets/cdn/cdn-create-customer-cert.png)

使用中のドメインを検証するには、TXT レコードを追加して検証する必要があります。

テキストレコード（TXT レコードとも呼ばれる）は、ドメインネームシステム（DNS）のリソースレコードのタイプです。任意のテキストをホスト名に関連付けることができます。このテキストには、サーバーやネットワーク情報など、人間が読み取れる詳細情報を含めることができます。

Cloud Manager では、特定の TXT レコードを使用して、ドメインを CDN サービスでホストすることを認証します。Cloud Manager でカスタムドメインを使用した CDN サービスのデプロイとバックエンドサービスとの関連付けを許可する DNS TXT レコードをゾーンに作成します。この関連付けは、お客様の管理下にあり、Cloud Manager でサービスからドメインにコンテンツを提供することを認可するものです。この認証は、付与することも、取り下げることもできます。TXT レコードは、ドメインと Cloud Manager 環境に固有のものです。

#### 要件 {#customer-managed-cert-requirements}

TXT レコードを追加する前に、次の要件を満たす必要があります。

* ドメインホストまたは登録機関がわからない場合は確認します。
* 組織のドメインの DNS レコードを編集できる、またはそれが可能な適切な担当者に連絡できる必要があります。
* まず、この記事で前述したとおりに、カスタムドメイン名を追加します。

#### 検証用の TXT レコードの追加 {#customer-managed-cert-verification}

1. **ドメインを検証**&#x200B;ダイアログボックスに、検証に使用する名前と TXT 値が表示されます。この値をコピーします。

1. DNS サービスプロバイダーにログインし、DNS レコードセクションを見つけます。

1. 値の「**名前**」として `aemverification.[yourdomainname]` を追加し、「**ドメイン名**」フィールド内の表示どおりに TXT 値を追加します。

   **TXT レコードの例**

   | ドメイン | 名前 | TXT 値 |
   | --- | --- | --- |
   | `example.com` | `_aemverification.example.com` | Cloud Manager UI に表示された値全体をコピーします。この値は、ドメインと環境に固有のものです。次に例を示します。<br>`adobe-aem-verification=example.com/[program]/[env]/..*` |
   | `www.example.com` | `_aemverification.www.example.com` | Cloud Manager UI に表示された値全体をコピーします。この値は、ドメインと環境に固有のものです。次に例を示します。<br>`adobe-aem-verification=www.example.com/[program]/[env]/..*` |

1. TXT レコードをドメインホストに保存します。

#### TXT レコードの検証 {#customer-managed-cert-verify}

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

<!--
## Next Steps {#next-steps}

Now that you created your TXT entry, you can verify your domain name status. Proceed to the document [Checking Domain Name Status](/help/implementing/cloud-manager/custom-domain-names/check-domain-name-status.md) to continue setting up your custom domain name. -->

>[!TIP]
>
>TXT エントリと CNAME または A レコードは、管理する DNS サーバーで同時に設定できるので、時間を節約できます。
>
><!-- To do this, review the entire process of setting up a custom domain name as detailed in the document [Introduction to custom domain names](/help/implementing/cloud-manager/custom-domain-names/introduction.md) taking special note of the document [help/implementing/cloud-manager/custom-domain-names/configure-dns-settings.md](/help/implementing/cloud-manager/custom-domain-names/configure-dns-settings.md) and update your DNS settings appropriately. -->


## 環境ページからのカスタムドメイン名の追加 {#adding-cdn-environments}

<!-- I DON'T SEE THIS ABILITY ANYMORE IN THE UI -->

**環境**&#x200B;ページからカスタムドメイン名を追加する手順は、[ドメイン設定ページからカスタムドメイン名を追加](#adding-cdn-settings)する場合と同じですが、エントリポイントが異なります。**環境**&#x200B;ページからカスタムドメイン名を追加するには、次の手順に従います。

1. [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) で Cloud Manager にログインし、適切な組織とプログラムを選択します。

1. 対象となる環境の、**環境の詳細**&#x200B;ページに移動します。

   ![環境の詳細ページでのドメイン名の入力](/help/implementing/cloud-manager/assets/cdn/cdn-create4.png)

1. **ドメイン名**&#x200B;テーブルを使用してカスタムドメイン名を送信します。

   1. カスタムドメイン名を入力します。
   1. この名前に関連付けられている SSL 証明書をドロップダウンリストから選択します。
   1. 「**+追加**」をクリックします。

   ![カスタムドメイン名の追加](/help/implementing/cloud-manager/assets/cdn/cdn-create3.png)

1. **ドメイン名を追加**&#x200B;ダイアログボックスが開き、「**ドメイン名**」タブが表示されます。[ドメイン設定ページからカスタムドメイン名を追加](#adding-cdn-settings)する場合と同様に続行します。 -->
