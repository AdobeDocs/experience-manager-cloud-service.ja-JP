---
title: カスタムドメイン名の概要
description: Cloud Manager の UI では、セルフサービス方式でカスタムドメインを追加して、サイトを独自のブランド名で特定できます。
exl-id: ed03bff9-dfcc-4dfe-a501-a7facd24aa7d
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
source-git-commit: 2724eaaaade94be89d33da5eecec4444cf851bd0
workflow-type: tm+mt
source-wordcount: '720'
ht-degree: 97%

---


# カスタムドメイン名の概要 {#introduction}

>[!CONTEXTUALHELP]
>id="aemcloud_golive_domains"
>title="カスタムドメイン名の管理"
>abstract="Cloud Manager の UI では、セルフサービス方式でカスタムドメインを追加して、サイトを独自のブランド名で特定できます。"
>additional-url="https://experienceleague.adobe.com/ja/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/custom-domain-names/add-custom-domain-name" text="カスタムドメイン名の追加"
>additional-url="https://experienceleague.adobe.com/ja/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/custom-domain-names/managing-custom-domain-names" text="カスタムドメイン名の表示と更新"

Adobe Experience Manager as a Cloud Service には、`*.adobeaemcloud.com` で終わるデフォルトのドメイン名がプロビジョニングされます。Cloud Manager の UI を使用すると、カスタムドメインを追加して、セルフサービス方式で独自のブランド名を使用してサイトを特定できます。デフォルトの `*.adobeaemcloud.com` ドメイン名は、web サイトにカスタムドメイン名を関連付けた後でも、そのまま残ります。

## カスタムドメイン名とは {#what-are-custom-domain-names}

各 web サイトには、`184.33.123.64` のような、機械で読み取り可能な一意の数値アドレスが関連付けられています。ドメインネームシステム（DNS）を使用すると、数値アドレスを、`wknd.com` のような覚えやすいアドレスに変換することで、web サイトにカスタムのブランドドメインを付加できます。

顧客が覚えやすく、ブランドを反映したサイトのドメイン名を付けることをお勧めします。

ドメイン名は、ドメイン名登録機関、会社、またはドメイン名を管理および販売する組織から購入できます。ドメイン名登録者は、DNS サーバー上のドメイン名を管理します。

>[!IMPORTANT]
>
>Cloud Manager はドメイン名登録機関ではないため、DNS サービスを提供しません。

## カスタムドメイン名と独自の CDN {#byo-cdn}

AEM as a Cloud Service にはビルトインの CDN（コンテンツ配信ネットワーク）サービスが用意されていますが、BYO（Bring Your Own）の CDN を AEM とともに使用することもできます。カスタムドメインは、AEM が管理する CDN か、自分が管理している CDN のいずれかにインストールできます。

* Cloud Manager は、AEM が管理する CDN にインストールされたカスタムドメイン名と証明書を管理します。
* BYO CDN にインストールされるカスタムドメイン名と証明書は、その CDN 内で直接管理されます。

**独自の CDN で管理されるドメインは、Cloud Manager 経由でのインストールは必要ありません** - X-Forwarded-Host を介して AEM で使用可能になり、Dispatcher で定義された vhosts と一致します。詳しくは、[CDN ドキュメント](/help/implementing/dispatcher/cdn.md)を参照してください。

1 つの環境で、AEM が管理する CDN にインストールされたドメインと、BYO CDN にインストールされたドメインの両方を持つことができます。

## ワークフロー {#workflow}

カスタムドメイン名を追加するには、DNS サービスと Cloud Manager 間のやり取りが必要です。このワークフローでは、カスタムドメイン名のインストール、設定、および検証には、いくつかの手順が必要です。次の表に、必要な手順の概要と、これらの手順を完了するためのドキュメントリソースへのリンクを示します。

| ステップ | 説明 | ドキュメント化 |
| --- | --- | --- |
| 1 | Cloud Manager への SSL 証明書の追加 | [SSL 証明書の追加](/help/implementing/cloud-manager/managing-ssl-certifications/add-ssl-certificate.md) |
| 2 | Cloud Manager へのカスタムドメインの追加 | [カスタムドメイン名の追加](/help/implementing/cloud-manager/custom-domain-names/add-custom-domain-name.md) |
| 3 | AEM as a Cloud Service を指す DNS CNAME または APEX レコードを追加して、DNS 設定を構成する | [カスタムドメイン名の追加](/help/implementing/cloud-manager/custom-domain-names/add-custom-domain-name.md) |
| 4 | ドメイン検証ステータスの確認 | [ドメイン名ステータスの確認](/help/implementing/cloud-manager/custom-domain-names/check-domain-name-status.md) |
| 5 | DNS レコードのステータスの確認 | [DNS レコードのステータスを確認](/help/implementing/cloud-manager/custom-domain-names/check-dns-record-status.md) |

>[!TIP]
>
>通常、AEM as a Cloud Service でのカスタムドメイン名の設定手順は簡単です。ただし、ドメインのデリゲーションに関する問題が発生した場合は、解決に 1～2 営業日かかる可能性があります。そのため、運用開始日の前にドメインを適切にインストールしておくことをお勧めします。詳しくは、[ドメイン名ステータスの確認](/help/implementing/cloud-manager/custom-domain-names/check-domain-name-status.md)のドキュメントを参照してください。

## 制限事項 {#limitations}

AEMaaCS でカスタムドメイン名を使用する場合は、いくつかの制限があります。

* Cloud Manager では、Sites プログラムの公開サービスおよびプレビューサービスに対してのみカスタムドメイン名がサポートされています。
   * オーサーサービスでは、カスタムドメインがサポートされていません。
* 各 Cloud Manager 環境は、1 つの環境につき最大 500 個のカスタムドメインをホストできます。
* 現在実行中のパイプラインが環境に接続されている間は、その環境にドメイン名を追加することはできません。
* 同じドメイン名を複数の環境で使用することはできません。
* 一度に追加できるドメイン名は 1 つだけです。
* AEM as a Cloud Service では、`*.example.com` のようなワイルドカードドメインをサポートしていません。
* カスタムドメイン名を追加する前に、カスタムドメイン名を含んだ有効な SSL 証明書（ワイルドカード証明書が有効）をプログラムにインストールする必要があります。
* [ フロントエンドパイプライン機能 ](/help/sites-cloud/administering/site-creation/enable-front-end-pipeline.md#custom-domains) でカスタムドメイン名を使用するには、追加の設定手順が必要です。

## 今すぐ始める {#get-started}

* プロジェクトに新しいカスタムドメイン名の設定を開始するには、[SSL 証明書の追加](/help/implementing/cloud-manager/managing-ssl-certifications/add-ssl-certificate.md)を参照してください。
* 既存のドメイン名を管理するには、[カスタムドメイン名の管理](/help/implementing/cloud-manager/custom-domain-names/managing-custom-domain-names.md)ドキュメントを参照してください。
