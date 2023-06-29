---
title: データ保護とデータプライバシーに関する規制 - Adobe Experience Manager as a Cloud Service の対応
description: 様々なデータ保護およびデータプライバシー規制に対するAdobe Experience Manager as a Cloud Serviceのサポートと、新しいAEMas a Cloud Serviceプロジェクトを実装する際の準拠方法について説明します。 これらの規制には、カリフォルニア州消費者プライバシー法 (GDPR) である EU 一般データ保護規則 (GDPR) が含まれます。
exl-id: 5dfa353b-84c5-4b07-bfcd-b03c2d361553
source-git-commit: 1473c1ffccc87cb3a0033750ee26d53baf62872f
workflow-type: tm+mt
source-wordcount: '734'
ht-degree: 43%

---

# データ保護およびデータプライバシーに関する規制に対する Adobe Experience Manager as a Cloud Service の対応 {#aem-readiness-for-data-protection-and-data-privacy-regulations}

>[!WARNING]
>
>このドキュメントの内容は法的な助言にはならず、その代用になるものでもありません。
>
>データ保護およびデータプライバシー規制に関するアドバイスについては、お客様の企業の法務部門にお問い合わせください。

>[!NOTE]
>
>プライバシーに関する問題に対するAdobeの対応と、これらの対応がAdobeのお客様にとってどのような意味を持つかについて詳しくは、 [Adobeプライバシーセンター](https://www.adobe.com/jp/privacy.html).

Adobeをご利用のお客様がこれらの規制に準拠できるよう、Adobeは、お客様のプライバシー管理者およびAEM管理者向けに、ドキュメントと手順（利用可能な場合は API を使用）を提供しています。

* このドキュメントは、管理者がデータ保護やデータプライバシー要求を処理するのに役立ちます。
* この手順に記載されているものを使用すると、お客様は手動で規制リクエストを実行したり、API 呼び出しを（利用可能な場合は）外部のポータルやサービスからおこなったりできます。

>[!CAUTION]
>
>ここで説明する内容は、Adobe Experience Manager as a Cloud Service に限定されます。
>
>別のAdobeオンデマンドサービスのデータと関連するプライバシーリクエストでは、そのサービスに対して行うアクションが必要です。
>
>詳しくは、 [Adobeプライバシーセンター](https://www.adobe.com/jp/privacy.html).

## はじめに {#introduction}

Adobe Experience Manager as a Cloud Serviceのインスタンスと、それらで実行されるアプリケーションは、Adobeの顧客が所有および操作します。

その結果、GDPR、CCPA などのデータ保護規制は、主に顧客の責任となります。

簡単な紹介として、データのプライバシーと保護に関する規制には、次の役割を持つ新しいルールが含まれます。

* 事業体（CCPA）および／またはデータ管理者（GDPR）

* サービスプロバイダー（CCPA）および／またはデータ処理者（GDPR）

このような規則の主な条項は次の通りです。

1. 個人データの定義を拡大してすべての固有の ID を含むようにし、直接および間接的に識別可能なデータとする。

2. 同意に関する要件の強化。

3. 削除権（データ消去）への重点的な取り組み。

4. データの販売のオプトアウト。

Adobe Experience Manager as a Cloud Service の場合：

* インスタンスと、それらに対して実行されるアプリケーションは、顧客が所有および運用します。

   * 所有権とは、お客様が、事業主体やサービス・プロバイダ、データ管理者、データ処理者などの規制上の役割を効果的に管理することを意味します。

   * 次の図に示すように、Adobe Experience Platform Privacy ServiceはAEMのワークフローに含まれていません。

* AEM には、顧客のプライバシー管理者や AEM 管理者が、手動または API を使用して（使用可能な場合）、プライバシー規制のリクエストを実行するためのドキュメントと手順が含まれています。

* 新しいサービスや UI は追加されていません。

   * 代わりに、プライバシー規制のリクエストを処理する顧客 UI／ポータルで使用する手順と API が文書化されています。

* AEMには、プライバシーリクエストワークフローをサポートするための既製のツールは含まれていません。

   * Adobeは、お客様のプライバシー管理者、AEM管理者またはその両方に関するドキュメントと手順を提供し、プライバシー規制に関連するリクエストを手動で実行できるようにします。

Adobeは、Adobe Experience Manager as a Cloud Serviceのアクセス、削除およびオプトアウトに関連するプライバシーリクエストを処理する手順を提供しています。 お客様が開発したポータルから呼び出すことができる API、または自動化に役立つスクリプトが利用できる場合があります。

次の図に、プライバシーリクエストワークフローを示します（Adobe Experience Manager 6.5 を使用した例）。

![データ保護とプライバシー](assets/data-protection-and-privacy-01.png)

## Adobe Experience Manager as a Cloud Service と規制への対応 {#aem-as-a-cloud-service-and-regulatory-readiness}

AEM as a Cloud Serviceの製品領域については、以下の規制ドキュメントの節を参照してください。

## Adobe Experience Manager as a Cloud Service の基盤 {#aem-foundation}

「[データ保護およびデータプライバシーに関する規制に対する AEM Foundation の対応](/help/compliance/data-privacy-and-protection-readiness/foundation-readiness.md)」を参照してください

## Adobe Experience Manager Sites as a Cloud Service {#aem-sites}

詳しくは、 [データ保護およびデータプライバシーに関する規制に対するAEM Sitesの対応](/help/compliance/data-privacy-and-protection-readiness/sites-readiness.md)

## Adobe Experience Manager as a Cloud Service と Adobe Target と Adobe Analytics の統合 {#aem-integration-with-adobe-target-adobe-analytics}

Adobe Experience Manager as a Cloud ServiceとAdobe TargetおよびAdobe Analyticsの統合は、データ保護およびプライバシー（GDPR など）に対応したサービスで実装されています。 Adobe Target や Adobe Analytics の個人データは、統合に関連して AEM に保存されません。
詳しくは、次を参照してください。

* [Adobe Target - プライバシーの概要](https://experienceleague.adobe.com/docs/target-dev/developer/implementation/privacy/cmp-privacy-and-general-data-protection-regulation.html)

* [Adobe Analytics データプライバシーのワークフロー](https://experienceleague.adobe.com/docs/analytics/admin/admin-tools/data-governance/an-gdpr-workflow.html)
