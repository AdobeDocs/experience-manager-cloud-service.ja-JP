---
title: カスタムドメイン名の追加
description: Cloud Manager でドメイン設定を使用してカスタムドメイン名を追加する方法について説明します。
exl-id: 0fc427b9-560f-4f6e-ac57-32cdf09ec623
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
source-git-commit: 215f4630acb3eca4be501c7c5f5de7c60b550bf8
workflow-type: tm+mt
source-wordcount: '1089'
ht-degree: 91%

---


# カスタムドメイン名の追加 {#adding-custom-domain-name}

Cloud Manager で&#x200B;**ドメイン設定**&#x200B;を使用してカスタムドメイン名を追加する方法について説明します。

## 要件 {#requirements}

Cloud Manager でカスタムドメイン名を追加する前に、次の要件を満たす必要があります。

* カスタムドメイン名を追加する&#x200B;*前*&#x200B;に、[SSL 証明書の追加](/help/implementing/cloud-manager/managing-ssl-certifications/add-ssl-certificate.md)ドキュメントの説明に従って、追加するドメインのドメイン SSL 証明書を追加しておく必要があります。
* Cloud Manager でカスタムドメイン名を追加するには、**ビジネスオーナー**&#x200B;または&#x200B;**デプロイメントマネージャー**&#x200B;の役割が必要です。
* Fastly または他の CDN（コンテンツ配信ネットワーク）を使用する必要があります。

>[!IMPORTANT]
>
>アドビが管理する CDN を使用する場合でも、ドメインを Cloud Manager に追加する必要があります。

## カスタムドメイン名の追加先 {#where-to-add-custom-domain-name}

Cloud Manager の[ドメイン設定ページ](#adding-cdn-settings)からカスタムドメイン名を追加できます。

カスタムドメイン名を追加する場合、最も具体的で有効な証明書を使用してドメインが提供されます。複数の証明書が同じドメインを持つ場合は、直近に更新されたものが選択されます。重複するドメインがないように証明書を管理することをお勧めします。

このドキュメントで説明するどちらの方法の手順も、Fastly に基づいています。別の CDN（コンテンツ配信ネットワーク）を使用した場合は、使用するように選択した CDN をドメインに設定します。

## カスタムドメイン名の追加 {#adding-custom-domain-name-settings}

1. [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) で Cloud Manager にログインし、適切な組織を選択します。

1. **[マイプログラム](/help/implementing/cloud-manager/navigation.md#my-programs)**&#x200B;コンソールで、プログラムを選択します。

1. サイドメニューの&#x200B;**サービス**&#x200B;で、![設定アイコン](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Settings_18_N.svg)、「**ドメイン設定**」をクリックします。

   ![ドメイン設定ウィンドウ](/help/implementing/cloud-manager/assets/cdn/cdn-create.png)

1. **ドメイン設定**&#x200B;ページの右上隅付近にある「**ドメインを追加**」をクリックします。

1. **ドメインを追加**&#x200B;ダイアログボックスの「**ドメイン名**」フィールドに、使用するカスタムドメイン名を入力します。
ドメイン名を入力する際は、`http://`、`https://`、スペースを含めないでください。

   >[!NOTE]
   >
   >ドメインの `www` バージョンと `non-www` バージョンの両方が必要な場合は、個別に追加する必要があります。例えば、`example.com` と `www.example.com` です。
   <!-- Marius Petria on SLACK tmp-skyline-cdn-certificates - Actually  my opinion is that this option should be explicit in UI (that was present in the initial mocks of the design but for some reason it was dropped). I think when adding a domain there should be a check mark to also add www.domain. When adding example.com Customer should be prompted with the following options: Do you also want to add www.example.com and have a redirect example.com -> www.example.com?Do you also want to add www.example.com and have a redirect www.example.com -> example.com? -->

1. 「**作成**」をクリックします。

1. **ドメインを検証**&#x200B;ダイアログボックスの&#x200B;**このドメインで使用する予定の証明書タイプは何ですか？**&#x200B;ドロップダウンリストで、次のオプションのいずれかを選択します。

   | 証明書タイプオプション | 説明 |
   | --- | --- |
   | アドビが管理する（DV）SSL 証明書 | DV（ドメイン検証）証明書を使用する場合は、この証明書タイプを選択します。このオプションは、ほとんどの場合に最適で、基本的なドメイン検証を提供します。証明書は、アドビによって管理され、自動的に更新されます。 |
   | 顧客が管理する（OV/EV）SSL 証明書 | EV/OV SSL 証明書を使用してドメインを保護する場合は、この証明書タイプを選択します。このオプションでは、OV（組織検証）または EV（拡張検証）でセキュリティが強化されます。より厳しい検証、より高い信頼レベル、証明書に対するカスタム管理のいずれかが必要な場合に使用します。 |

1. **ドメインを検証**&#x200B;ダイアログボックスで、選択した証明書タイプに応じて、次のいずれかを行います。

   | 選択した証明書タイプ | 説明 |
   | --- | ---  |
   | アドビが管理する証明書 | a. 以下の[アドビが管理する証明書の手順](#adobe-managed-cert-steps)を完了します。手順を完了したら、**ドメインを検証**&#x200B;ダイアログボックスで「**検証**」をクリックします。<ul><li>DNS の生成遅延が原因で、DNS 検証の処理に数時間かかる場合があります。</li><li>Cloud Manager は最終的にドメイン名の所有権を確認し、**ドメイン設定**&#x200B;テーブルのステータスを更新します。詳しくは、[カスタムドメイン名のステータスの確認](/help/implementing/cloud-manager/custom-domain-names/check-domain-name-status.md)を参照してください。</li>![ドメインステータスの検証](/help/implementing/cloud-manager/assets/domain-settings-verified.png)</li></ul>b. [アドビが管理する（DV）SSL 証明書を追加](/help/implementing/cloud-manager/managing-ssl-certifications/add-ssl-certificate.md#add-adobe-managed-ssl-cert)する準備が整いました。</li></ul> |
   | 顧客が管理する証明書 | a. 「**OK**」をクリックします。<br>b. これで、[顧客が管理する（OV/EV）SSL 証明書を追加](/help/implementing/cloud-manager/managing-ssl-certifications/add-ssl-certificate.md#add-customer-managed-ssl-cert)する準備が整いました。<br>証明書を追加すると、ドメイン名が&#x200B;**ドメイン設定**&#x200B;テーブルで検証済みとマークされます。詳しくは、[カスタムドメイン名のステータスの確認](/help/implementing/cloud-manager/custom-domain-names/check-domain-name-status.md)を参照してください。</li></ul><br>![顧客が管理する EV/OV 証明書のドメイン検証](/help/implementing/cloud-manager/assets/verify-domain-customer-managed-step.png) |

   >[!NOTE]
   >
   >顧客が管理する自社の（OV/EV または DV）SSL 証明書を使用する場合は、SSL 証明書を追加する必要はありません。このルールは、顧客が管理する CDN（コンテンツ配信ネットワーク）***プロバイダー***&#x200B;を使用する予定の場合にも適用されます。代わりに、準備が整ったら[ドメインマッピングの追加](/help/implementing/cloud-manager/domain-mappings/add-domain-mapping.md)に直接進むことができます。


### アドビが管理する証明書の手順 {#adobe-managed-cert-steps}

証明書タイプとして「*アドビが管理する証明書*」を選択した場合は、**ドメインを検証**&#x200B;ダイアログボックスで次の手順を完了します。

![アドビが管理する証明書の手順](/help/implementing/cloud-manager/assets/cdn/cdn-create-adobe-dv-cert.png)

使用中のドメインを検証するには、CNAME を追加して検証する必要があります。

`CNAME` レコードタイプまたは `A` レコードタイプがプロビジョニングされると、ドメインのすべてのインターネットトラフィックが、そのレコードが指している場所にルーティングされます。その場所がトラフィックを処理するようにプロビジョニングされていない場合は、機能が一時的に停止します。テストされていない場合は、コンテンツにエラーがある可能性があります。この手順が常にテストが完了し運用開始の準備が整った後に実行されるのは、このためです。

これらの設定を行うには、カスタムドメイン名が Cloud Manager ドメイン名を指すように、`CNAME` または Apex レコードを設定する必要があるかどうかを判断します。このドキュメントの後の節は、DNS 設定に適したレコードタイプを判断するうえで役に立ちます。

>[!NOTE]
>
>アドビが管理する CDN の場合、DV（ドメイン検証）証明書を使用する際は、ACME 検証済みのサイトのみが許可されます。


## DNS の設定{#config-dns}

>[!WARNING]
>
>「広告前に登録」の原則はここに適用されます。 つまり、DNS の設定は、ドメインマッピングが正常に追加された *後* にのみ実行する必要があります。 これにより、Cloud Managerが、ドメインに対するリクエストに応答する前に、ドメインが独自の設定に存在することを認識および検証できます。 また、ドメインの乗っ取りが試行されるのを回避します。

DNS レコードを設定する *前に*、次の要件を満たしていることを確認します。

* ドメインホストまたは登録機関がわからない場合は確認します。
* 組織のドメインの DNS レコードを編集できる、またはそれが可能な適切な担当者に連絡できる必要があります。
* [ ドメイン名ステータスの確認 ](/help/implementing/cloud-manager/custom-domain-names/check-domain-name-status.md) ドキュメントに記載されているように、設定されたカスタムドメイン名は既に確認されています。

### CNAME レコード {#adobe-managed-cert-cname-record}

正規名つまり CNAME レコードは、エイリアス名を真のドメイン名つまり正規ドメイン名にマッピングする DNS レコードタイプです。CNAME レコードは、通常、`www.example.com` などのサブドメインを、そのサブドメインのコンテンツをホストするドメインにマッピングするために使用されます。

DNS サービスプロバイダーにログインし、次のテーブルのように、カスタムドメイン名がターゲットを指すように `CNAME` レコードを作成します。

| CNAME | カスタムドメイン名の参照先 |
| --- | --- |
| `www.customdomain.com` | `cdn.adobeaemcloud.com` |

### APEX レコード {#adobe-managed-cert-apex-record}

apex ドメインは、サブドメインを含まないカスタムドメイン（例：`example.com` など）です。DNS プロバイダーを通じて、Apex ドメインは `A`、`ALIAS`、`ANAME` のいずれかのレコードで設定されます。Apex ドメインは、特定の IP アドレスを指す必要があります。

ドメインプロバイダーを介してドメインの DNS 設定に次の `A` レコードを追加します。

* `A RECORD`

* `A record for domain @ pointing to IP 151.101.3.10`

* `A record for domain @ pointing to IP 151.101.67.10`

* `A record for domain @ pointing to IP 151.101.131.10`

* `A record for domain @ pointing to IP 151.101.195.10`

>[!TIP]
>
>*CNAME レコード*&#x200B;または *A レコード*&#x200B;を管理する DNS サーバーに設定すると、時間を節約できます。

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


