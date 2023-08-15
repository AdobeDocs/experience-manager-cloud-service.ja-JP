---
title: カスタムドメイン名の概要
description: Cloud Manager の UI を使用すると、カスタムドメインを追加して、自社サイトをセルフサービス方式で一意のブランド名で識別できます。
exl-id: ed03bff9-dfcc-4dfe-a501-a7facd24aa7d
source-git-commit: 5ad33f0173afd68d8868b088ff5e20fc9f58ad5a
workflow-type: tm+mt
source-wordcount: '757'
ht-degree: 74%

---


# カスタムドメイン名の概要 {#introduction}

>[!CONTEXTUALHELP]
>id="aemcloud_golive_domains"
>title="カスタムドメイン名の管理"
>abstract="Cloud Manager の UI を使用すると、カスタムドメインを追加して、自社サイトをセルフサービス方式で一意のブランド名で識別できます。"
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/custom-domain-names/add-custom-domain-name.html?lang=ja" text="カスタムドメイン名の追加"
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/custom-domain-names/view-update-replace-custom-domain-name.html?lang=ja" text="カスタムドメイン名の表示と更新"

Cloud Manager の UI を使用すると、カスタムドメインを追加して、自社サイトをセルフサービス方式で一意のブランド名で識別できます。 Adobe Experience Manager as a Cloud Service には、`*.adobeaemcloud.com` で終わるデフォルトのドメイン名がプロビジョニングされます。このデフォルトのドメイン名は、web サイトにカスタムドメイン名を関連付けた後でも、そのまま残ります。

## カスタムドメイン名とは {#what-are-custom-domain-names}

各 web サイトには、`184.33.123.64` のような、機械で読み取り可能な一意の数値アドレスが関連付けられています。ドメインネームシステム (DNS) を使用すると、数値アドレスを次のような覚えやすいアドレスに変換することで、Web サイトにカスタムのブランドドメインを付加できます。 `wknd.com`.

顧客が覚えやすく、ブランドを反映したサイトのドメイン名を付けることをお勧めします。

ドメイン名は、ドメイン名登録機関、会社、またはドメイン名を管理および販売する組織から購入できます。ドメイン名登録者は、DNS サーバー上のドメイン名を管理します。

>[!IMPORTANT]
>
>Cloud Manager はドメイン名登録機関ではないため、DNS サービスを提供しません。

## カスタムドメイン名と BYO CDN {#byo-cdn}

AEM as a Cloud Serviceは、組み込みのコンテンツ配信ネットワーク (CDN) サービスを提供しますが、独自の (BYO)CDN をAEMと共に使用することもできます。 カスタムドメインは、AEM が管理する CDN か、自分が管理している CDN のいずれかにインストールできます。

* AEM が管理する CDN にインストールされるカスタムドメイン名（および証明書）は、Cloud Manager で管理されます。
* 独自の CDN にインストールされているカスタムドメイン名（および証明書）は、その特定の CDN で管理されます。

独自の CDN で管理されるドメインは、Cloud Manager を通じてインストールする必要はありません。 X-Forwarded-Host を介してAEMで使用可能になり、Dispatcher で定義された vhosts と一致します。 詳しくは、 [CDN ドキュメント](/help/implementing/dispatcher/cdn.md).

1 つの環境で、AEM が管理する CDN にインストールされたドメインと、独自の CDN にインストールされたドメインの両方を持つことができます。

## ワークフロー {#workflow}

カスタムドメイン名を追加するには、DNS サービスと Cloud Manager 間のやり取りが必要です。このため、カスタムドメイン名のインストール、設定および検証には、いくつかの手順が必要です。次の表に、一般的なエラーが発生した場合の対処方法など、必要な手順の概要を示します。

| 手順 | 説明 | 担当 | 詳細情報 |
|--- |--- |--- |---|
| 1 | Cloud Manager への SSL 証明書の追加 | 顧客 | [SSL 証明書の追加](/help/implementing/cloud-manager/managing-ssl-certifications/add-ssl-certificate.md) |
| 2 | TXT レコードを追加してドメインを検証 | 顧客 | [TXT レコードの追加](/help/implementing/cloud-manager/custom-domain-names/add-text-record.md) |
| 3 | ドメイン検証ステータスを確認 | 顧客 | [ドメイン名ステータスの確認](/help/implementing/cloud-manager/custom-domain-names/check-domain-name-status.md) |
| 3a | ドメインの検証が「`Domain Verification Failure`」ステータスで失敗した場合 | 顧客 | [ドメイン名ステータスの確認](/help/implementing/cloud-manager/custom-domain-names/check-domain-name-status.md) |
| 3b | ドメインの検証が「`Verified, Deployment Failed`」ステータスで失敗した場合、アドビにお問い合わせください | アドビカスタマーケア | [ドメイン名ステータスの確認](/help/implementing/cloud-manager/custom-domain-names/check-domain-name-status.md) |
| 4 | AEM as a Cloud Service を指す DNS CNAME または APEX レコードを追加して、DNS 設定を構成します | 顧客 | [DNS 設定の指定](/help/implementing/cloud-manager/custom-domain-names/configure-dns-settings.md) |
| 5 | DNS レコードのステータスを確認 | 顧客 | [DNS レコードのステータスの確認](/help/implementing/cloud-manager/custom-domain-names/check-dns-record-status.md) |
| 5a | DNS レコードのステータスが次の条件で失敗した場合：`DNS status not detected` | 顧客 | [DNS レコードのステータスの確認](/help/implementing/cloud-manager/custom-domain-names/check-dns-record-status.md) |
| 5b | DNS レコードのステータスが次の条件で失敗した場合：`DNS resolves incorrectly` | 顧客 | [DNS レコードのステータスの確認](/help/implementing/cloud-manager/custom-domain-names/check-dns-record-status.md) |

>[!TIP]
>
>通常、AEM as a Cloud Service でのカスタムドメイン名の設定手順は簡単です。 ただし、ドメインのデリゲーションに関する問題が発生することがあり、その場合は解決に 1～2 営業日かかる可能性があります。そのため、運用開始日の前にドメインを適切にインストールしておくことを強くお勧めします。 詳しくは、[ドメイン名のステータスの確認](/help/implementing/cloud-manager/custom-domain-names/check-domain-name-status.md)のドキュメントを参照してください。

## 制限事項 {#limitations}

AEMaaCS でカスタムドメイン名を使用する場合は、多くの制限があります。

* Cloud Manager では、Sites プログラムの公開サービスおよびプレビューサービスの両方でカスタムドメイン名がサポートされています。オーサーサービスでは、カスタムドメインがサポートされていません。
* 各 Cloud Manager 環境は、1 つの環境につき最大 500 個のカスタムドメインをホストできます。
* 現在実行中のパイプラインが環境に添付されている間は、ドメイン名を環境に追加できません。
* 同じドメイン名を複数の環境で使用することはできません。
* 一度に追加できるドメイン名は 1 つだけです。
* AEM as a Cloud Service では、`*.example.com` のようなワイルドカードドメインをサポートしていません。
* カスタムドメイン名を追加する前に、カスタムドメイン名を含んだ有効な SSL 証明書（ワイルドカード証明書が有効）をプログラムにインストールする必要があります。詳しくは、 [SSL 証明書の追加](/help/implementing/cloud-manager/managing-ssl-certifications/add-ssl-certificate.md) を参照してください。
