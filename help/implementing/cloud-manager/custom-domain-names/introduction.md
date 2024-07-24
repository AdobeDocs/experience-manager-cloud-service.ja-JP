---
title: カスタムドメイン名の概要
description: Cloud Manager の UI では、セルフサービス方式でカスタムドメインを追加して、サイトを独自のブランド名で特定できます。
exl-id: ed03bff9-dfcc-4dfe-a501-a7facd24aa7d
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
source-git-commit: 1c9924b4477d53d86bb72eda8597a02304450195
workflow-type: tm+mt
source-wordcount: '722'
ht-degree: 67%

---


# カスタムドメイン名の概要 {#introduction}

>[!CONTEXTUALHELP]
>id="aemcloud_golive_domains"
>title="カスタムドメイン名の管理"
>abstract="Cloud Manager の UI では、セルフサービス方式でカスタムドメインを追加して、サイトを独自のブランド名で特定できます。"
>additional-url="https://experienceleague.adobe.com/ja/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/custom-domain-names/add-custom-domain-name" text="カスタムドメイン名の追加"
>additional-url="https://experienceleague.adobe.com/ja/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/custom-domain-names/managing-custom-domain-names" text="カスタムドメイン名の表示と更新"

Adobe Experience Manager as a Cloud Service には、`*.adobeaemcloud.com` で終わるデフォルトのドメイン名がプロビジョニングされます。Cloud Managerの UI を使用すると、セルフサービス方式でカスタムドメインを追加して、サイトを独自のブランド名で識別することができます。 カスタムドメイン名を web サイトに関連付けた後も、デフォルトの `*.adobeaemcloud.com` ドメイン名は残ります。

## カスタムドメイン名とは {#what-are-custom-domain-names}

各 web サイトには、`184.33.123.64` のような、機械で読み取り可能な一意の数値アドレスが関連付けられています。ドメインネームシステム（DNS）を使用すると、数値アドレスを、`wknd.com` のような覚えやすいアドレスに変換することで、web サイトにカスタムのブランドドメインを付加できます。

顧客が覚えやすく、ブランドを反映したサイトのドメイン名を付けることをお勧めします。

ドメイン名は、ドメイン名登録機関、会社、またはドメイン名を管理および販売する組織から購入できます。ドメイン名登録者は、DNS サーバー上のドメイン名を管理します。

>[!IMPORTANT]
>
>Cloud Manager はドメイン名登録機関ではないため、DNS サービスを提供しません。

## カスタムドメイン名と BYO CDN {#byo-cdn}

AEM as a Cloud Service にはビルトインのコンテンツ配信ネットワーク（CDN）サービスが用意されていますが、独自の（BYO）CDN を AEM とともに使用することもできます。カスタムドメインは、AEM が管理する CDN か、自分が管理している CDN のいずれかにインストールできます。

* AEM が管理する CDN にインストールされるカスタムドメイン名（および証明書）は、Cloud Manager で管理されます。
* 独自の CDN にインストールされているカスタムドメイン名（および証明書）は、その特定の CDN で管理されます。

**独自の CDN で管理するドメインは、Cloud Managerを介してインストールする必要はありません。** X-Forwarded-Host を介してAEMで使用可能になり、Dispatcherで定義された vhost と一致します。 [CDN ドキュメント ](/help/implementing/dispatcher/cdn.md) を参照してください。

1 つの環境で、AEM が管理する CDN にインストールされたドメインと、独自の CDN にインストールされたドメインの両方を持つことができます。

## ワークフロー {#workflow}

カスタムドメイン名を追加するには、DNS サービスと Cloud Manager 間のやり取りが必要です。このため、カスタムドメイン名のインストール、設定および検証には、いくつかの手順が必要です。 次の表に、必要な手順の概要を示します。これには、これらの手順を完了するためのドキュメントリソースへのリンクも含まれます。

| 手順 | 説明 | ドキュメント化 |
|---|---|---|
| 1 | Cloud Manager への SSL 証明書の追加 | [SSL 証明書の追加](/help/implementing/cloud-manager/managing-ssl-certifications/add-ssl-certificate.md) |
| 2 | Cloud Managerへのカスタムドメインの追加 | [カスタムドメイン名の追加](/help/implementing/cloud-manager/custom-domain-names/add-custom-domain-name.md) |
| 3 | TXT レコードを追加してドメインを検証 | [TXT レコードの追加](/help/implementing/cloud-manager/custom-domain-names/add-text-record.md) |
| 4 | ドメイン検証ステータスを確認 | [ドメイン名ステータスの確認](/help/implementing/cloud-manager/custom-domain-names/check-domain-name-status.md) |
| 5 | AEM as a Cloud Service を指す DNS CNAME または APEX レコードを追加して、DNS 設定を構成します | [DNS 設定の指定](/help/implementing/cloud-manager/custom-domain-names/configure-dns-settings.md) |
| 6 | DNS レコードのステータスを確認 | [DNS レコードのステータスの確認](/help/implementing/cloud-manager/custom-domain-names/check-dns-record-status.md) |

>[!TIP]
>
>通常、AEM as a Cloud Service でのカスタムドメイン名の設定手順は簡単です。 ただし、ドメインのデリゲーションに関する問題が発生することがあり、その場合は解決に 1～2 営業日かかる可能性があります。 そのため、運用開始日の前にドメインを適切にインストールしておくことを強くお勧めします。 詳しくは、[ドメイン名のステータスの確認](/help/implementing/cloud-manager/custom-domain-names/check-domain-name-status.md)のドキュメントを参照してください。

## 制限事項 {#limitations}

AEMaaCS でカスタムドメイン名を使用する場合は、いくつかの制限があります。

* Cloud Managerでは、Sites プログラムの公開サービスおよびプレビューサービスでのみカスタムドメイン名がサポートされています。
   * オーサーサービスでは、カスタムドメインがサポートされていません。
* 各 Cloud Manager 環境は、1 つの環境につき最大 500 個のカスタムドメインをホストできます。
* 現在実行中のパイプラインが環境に接続されている間は、その環境にドメイン名を追加することはできません。
* 同じドメイン名を複数の環境で使用することはできません。
* 一度に追加できるドメイン名は 1 つだけです。
* AEM as a Cloud Service では、`*.example.com` のようなワイルドカードドメインをサポートしていません。
* カスタムドメイン名を追加する前に、カスタムドメイン名を含んだ有効な SSL 証明書（ワイルドカード証明書が有効）をプログラムにインストールする必要があります。

## 始めましょう。 {#get-started}

* [SSL 証明書の追加 ](/help/implementing/cloud-manager/managing-ssl-certifications/add-ssl-certificate.md) を行って、プロジェクトの新しいカスタムドメイン名の設定を開始します。
* [ カスタムドメイン名の管理 ](/help/implementing/cloud-manager/custom-domain-names/managing-custom-domain-names.md) ドキュメントを確認して、既存のドメイン名を管理します。
