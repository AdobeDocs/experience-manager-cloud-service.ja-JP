---
title: カスタムドメイン名の追加
description: Cloud Manager でドメイン設定を使用してカスタムドメイン名を追加する方法について説明します。
exl-id: 0fc427b9-560f-4f6e-ac57-32cdf09ec623
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
source-git-commit: fa99656e0dd02bb97965e8629d5fa657fbae9424
workflow-type: tm+mt
source-wordcount: '998'
ht-degree: 75%

---


# カスタムドメイン名の追加 {#adding-cdn}

Cloud Manager で&#x200B;**ドメイン設定**&#x200B;を使用してカスタムドメイン名を追加する方法について説明します。

## 要件 {#requirements}

Cloud Manager でカスタムドメイン名を追加する前に、次の要件を満たす必要があります。

* *SSL 証明書の追加 ](/help/implementing/cloud-manager/managing-ssl-certifications/add-ssl-certificate.md) のドキュメントで説明しているように* カスタムドメイン名を追加する前に [ 追加するドメインのドメイン SSL 証明書を追加する必要があります。
* Cloud Manager でカスタムドメイン名を追加するには、**ビジネスオーナー**&#x200B;または&#x200B;**デプロイメントマネージャー**&#x200B;の役割が必要です。
* Fastly または他の CDN（コンテンツ配信ネットワーク）を使用する必要があります。

>[!IMPORTANT]
>
>Adobeが管理する CDN を使用する場合は、ドメインをCloud Managerに追加する必要があります。

## カスタムドメイン名の追加先 {#where-to-add-cdn}

Cloud Manager では、次の 2 つの場所からカスタムドメイン名を追加できます。

* [ドメイン設定ページ](#adding-cdn-settings)
* [環境ページ](#adding-cdn-environments)

カスタムドメイン名を追加する場合、最も具体的で有効な証明書を使用してドメインが提供されます。複数の証明書が同じドメインを持つ場合は、直近に更新されたものが選択されます。重複するドメインがないように証明書を管理することをお勧めします。

このドキュメントで説明するどちらの方法の手順も、Fastly に基づいています。別の CDN（コンテンツ配信ネットワーク）を使用した場合は、使用するように選択した CDN をドメインに設定します。

## カスタムドメイン名の追加 {#adding-cdn-settings}

1. [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) で Cloud Manager にログインし、適切な組織を選択します。

1. **[マイプログラム](/help/implementing/cloud-manager/navigation.md#my-programs)**&#x200B;コンソールで、プログラムを選択します。

1. サイドメニューの **サービス** で、![ 設定アイコン ](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Settings_18_N.svg)**ドメイン設定** をクリックします。

   ![ドメイン設定ウィンドウ](/help/implementing/cloud-manager/assets/cdn/cdn-create.png)

1. **ドメイン設定**&#x200B;ページの右上隅付近にある「**ドメインを追加**」をクリックします。

1. **ドメインを追加**&#x200B;ダイアログボックスの「**ドメイン名**」フィールドに、使用するカスタムドメイン名を入力します。
ドメイン名を入力する際は、`http://`、`https://`、スペースを含めないでください。

1. 「**作成**」をクリックします。

1. **ドメインを検証**&#x200B;ダイアログボックスの&#x200B;**このドメインで使用する予定の証明書タイプは何ですか？**&#x200B;ドロップダウンリストで、次のオプションのいずれかを選択します。

   | 証明書タイプオプション | 説明 |
   | --- | --- |
   | Adobe管理（DV） SSL 証明書 | DV（ドメイン検証）証明書を使用する場合は、この証明書タイプを選択します。このオプションは、ほとんどの場合に最適で、基本的なドメイン検証を提供します。証明書は、アドビによって管理され、自動的に更新されます。 |
   | 顧客管理（OV/EV） SSL 証明書 | EV/OV SSL 証明書を使用してドメインを保護する場合は、この証明書タイプを選択します。 このオプションは、OV （組織検証）または EV （拡張検証）によるセキュリティの強化を提供します。 より厳しい検証、より高い信頼レベル、証明書に対するカスタム管理のいずれかが必要な場合に使用します。 |

1. **ドメインを検証**&#x200B;ダイアログボックスで、選択した証明書タイプに応じて、次のいずれかを行います。

   | 選択した証明書タイプ | 説明 |
   | --- | ---  |
   | アドビが管理する証明書 | a.以下の [Adobeが管理する証明書の手順 ](#adobe-managed-cert-steps) 実行します。 **ドメインの検証** ダイアログボックスの手順を完了したら、「**検証**」をクリックします。<ul><li>DNS の生成遅延が原因で、DNS 検証の処理に数時間かかる場合があります。</li><li>Cloud Managerは最終的にドメイン名の所有権を確認し、「**ドメイン設定**」テーブルのステータスを更新します。 詳しくは、[カスタムドメイン名のステータスの確認](/help/implementing/cloud-manager/custom-domain-names/check-domain-name-status.md)を参照してください。</li>![ ドメインステータスの検証 ](/help/implementing/cloud-manager/assets/domain-settings-verified.png)</li></ul>b. [Adobe管理（DV） SSL 証明書を追加する ](/help/implementing/cloud-manager/managing-ssl-certifications/add-ssl-certificate.md) 準備が整いました。</li></ul> |
   | 顧客が管理する証明書 | a. 「**OK**」をクリックします。<br>b.これで、[ 顧客管理（OV/EV） SSL 証明書を追加 ](/help/implementing/cloud-manager/managing-ssl-certifications/add-ssl-certificate.md) する準備が整いました。<ul><li>証明書を追加すると、ドメイン名が「**ドメイン設定**」テーブルで検証済みとマークされます。 詳しくは、[カスタムドメイン名のステータスの確認](/help/implementing/cloud-manager/custom-domain-names/check-domain-name-status.md)を参照してください。</li></ul><br>![顧客が管理する EV/OV 証明書のドメイン検証](/help/implementing/cloud-manager/assets/verify-domain-customer-managed-step.png) |

   >[!NOTE]
   >
   >顧客管理（OV/EV）の SSL 証明書と顧客管理の CDN プロバイダーを使用する場合は、SSL 証明書の追加をスキップし、準備が整ったら直接 [CDN 設定の追加 ](/help/implementing/cloud-manager/cdn-configurations/add-cdn-config.md) に進むことができます。


### アドビが管理する証明書の手順 {#adobe-managed-cert-steps}

証明書の種類 *Adobeで管理される証明書* を選択した場合は、[ ドメインの検証 **] ダイアログ ボックスで次の手順を実行し** す。

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

>[!TIP]
>
>*CNAME* または *A レコード*&#x200B;を管理する DNS サーバーに設定すると、時間を節約できます。

<!--
![Customer managed certificate steps](/help/implementing/cloud-manager/assets/cdn/cdn-create-customer-cert.png)

To verify the domain in use, you are required to add and verify a TXT record.

A text record (also known as a TXT record) is a type of resource record in the Domain Name System (DNS). It lets you associate arbitrary text with a hostname. This text could include human-readable details like server or network information.

Cloud Manager uses a specific TXT record to authorize a domain to be hosted in a CDN service. Create a DNS TXT record in the zone that authorizes Cloud Manager to deploy the CDN service with the custom domain and associate it with the backend service. This association is entirely under your control and authorizes Cloud Manager to serve content from the service to a domain. This authorization may be granted and withdrawn. The TXT record is specific to the domain and the Cloud Manager environment.

#### Requirements {#customer-managed-cert-requirements}

Fulfill these requirements before adding a TXT record.

* Identify your domain host or registrar if you do not know it already.
* Be able to edit the DNS records for your organization's domain, or contact the appropriate person who can.
* First, add a custom domain name as described earlier in this article.

#### Add a TXT record for verification {#customer-managed-cert-verification}

1. In the **Verify domain** dialog box, Cloud Manager displays the name and TXT value to use for verification. Copy this value.

1. Log in to your DNS service provider and find the DNS records section. 

1. Add `aemverification.[yourdomainname]` as the **Name** of the value and add the TXT value exactly as it appears in the **Domain Name** field.

   **TXT record examples**

   | Domain | Name | TXT Value |
   | --- | --- | --- |
   | `example.com` | `_aemverification.example.com` | Copy the entire value displayed in the Cloud Manager UI. This value is specific to the domain and the environment. For example:<br>`adobe-aem-verification=example.com/[program]/[env]/..*` |
   | `www.example.com` | `_aemverification.www.example.com` | Copy the entire value displayed in the Cloud Manager UI. This value is specific to the domain and the environment. For example:<br>`adobe-aem-verification=www.example.com/[program]/[env]/..*` |

1. Save the TXT record to your domain host.

#### Verify TXT record {#customer-managed-cert-verify}

When you are done, you can verify the result by running the following command.

```shell
dig _aemverification.[yourdomainname] -t txt
```

The expected result should display the TXT value provided on the **Verification** tab of the **Add Domain Name** dialog of the Cloud Manager UI.

For example, if your domain is `example.com`, then run:

```shell
dig TXT _aemverification.example.com -t txt
```


>[!TIP]
>
>There are several [DNS lookup tools](https://www.ultratools.com/tools/dnsLookup) available. Google DoH can be used to look up TXT record entries and identify if the TXT record is missing or erroneous.

-->



<!--
## Next Steps {#next-steps}

Now that you created your TXT entry, you can verify your domain name status. Proceed to the document [Checking Domain Name Status](/help/implementing/cloud-manager/custom-domain-names/check-domain-name-status.md) to continue setting up your custom domain name. -->


><!-- The TXT entry and the CNAME or A Record can be set simultaneously on the governing DNS server, thus saving time. -->
>
><!-- To do this, review the entire process of setting up a custom domain name as detailed in the document [Introduction to custom domain names](/help/implementing/cloud-manager/custom-domain-names/introduction.md) taking special note of the document [help/implementing/cloud-manager/custom-domain-names/configure-dns-settings.md](/help/implementing/cloud-manager/custom-domain-names/configure-dns-settings.md) and update your DNS settings appropriately. -->

