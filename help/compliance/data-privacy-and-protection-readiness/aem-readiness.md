---
title: データ保護とデータプライバシーに関する規制 - Adobe Experience Manager as a Cloud Service の対応
description: さまざまなデータ保護およびデータプライバシー規則に対する Adobe Experience Manager as a Cloud Service のサポートについて説明します。これには、EU 一般データ保護規則（GDPR）、カリフォルニア州消費者プライバシー法、および新しい AEM as a Cloud Service プロジェクトを実装する際に準拠する方法が含まれます。
exl-id: 5dfa353b-84c5-4b07-bfcd-b03c2d361553
source-git-commit: e9c1ec6807f86ab00f89ef292a89a0c8efdf802b
workflow-type: tm+mt
source-wordcount: '729'
ht-degree: 97%

---

# データ保護およびデータプライバシーに関する規制に対する Adobe Experience Manager as a Cloud Service の対応 {#aem-readiness-for-data-protection-and-data-privacy-regulations}

>[!WARNING]
>
>このドキュメントの内容は法的な助言にはならず、その代用になるものでもありません。
>
>データ保護およびデータプライバシー規制に関するアドバイスについては、自社の法務部門にお問い合わせください。

>[!NOTE]
>
>アドビのプライバシーに関する問題への対応と、アドビのお客様への影響について詳しくは、[アドビのプライバシーセンター](https://www.adobe.com/jp/privacy.html)をご覧ください。

アドビは、お客様のプライバシー管理者または AEM 管理者がデータ保護およびデータプライバシーリクエストを処理するためのドキュメントおよび手順（利用可能な場合は API も）を提供しており、お客様がこれらの規則に準拠できるように支援をしています。ドキュメントに記載された手順を参照すれば、外部のポータルやサービスから手動で、または API が利用可能な場合は API を呼び出して、規制のリクエストを実行することができます。

>[!CAUTION]
>
>ここで説明する内容は、Adobe Experience Manager as a Cloud Service に限定されます。
>
>別のアドビオンデマンドサービスからのデータは、関連するプライバシー要求とともに、そのサービスでの対応が必要となります。
>
>詳しくは、[アドビのプライバシーセンター](https://www.adobe.com/privacy.html)を参照してください。

## はじめに {#introduction}

Adobe Experience Manager as a Cloud Service のインスタンスと、それらで実行されるアプリケーションは、アドビの顧客が所有および操作します。

その結果、GDPR、CCPA などのデータ保護規制は、主に顧客の責任となります。

簡単に紹介すると、データのプライバシーと保護に関する規制には、次の役割を担う者が従うべき新しいルールが含まれます。

* 事業体（CCPA）および／またはデータ管理者（GDPR）

* サービスプロバイダー（CCPA）および／またはデータ処理者（GDPR）

このような規則の主な条項は次の通りです。

1. 個人データの定義を拡大してすべての固有の ID を含むようにし、直接および間接的に識別可能なデータとする。

2. 同意に関する要件の強化。

3. 削除権（データ消去）への重点的な取り組み。

4. データの販売のオプトアウト。

Adobe Experience Manager as a Cloud Service の場合：

* インスタンスと、それらに対して実行されるアプリケーションは、顧客が所有および運用します。

   * これは、顧客が、事業体やサービスプロバイダー、データ管理者、データ処理者などの規制上の役割を効果的に管理することを意味します。

   * 次の図に示すように、Adobe Experience Platform Privacy Service は AEM のワークフローには含まれていません。

* AEM には、顧客のプライバシー管理者や AEM 管理者が、手動または API を使用して（使用可能な場合）、プライバシー規制のリクエストを実行するためのドキュメントと手順が含まれています。

* 新しいサービスや UI は追加されていません。

   * 代わりに、プライバシー規制のリクエストを処理する顧客 UI／ポータルで使用する手順と API が文書化されています。

* AEM には、プライバシーリクエストワークフローをサポートする標準のツールは含まれません。

   * アドビは、顧客のプライバシー管理者や AEM 管理者向けのドキュメントや手順を提供し、プライバシー規制に関連するリクエストを手動で実行できるようにします。

アドビは、Adobe Experience Manager as a Cloud Service のアクセス、削除、オプトアウトに関するプライバシーリクエストを処理する手順を提供しています。場合によっては、自動化に役立つように、顧客が開発したポータルまたはスクリプトから呼び出すことができる API が存在します。

次の図に、プライバシーリクエストワークフローを示します（Adobe Experience Manager 6.5 を使用した例）。

![データ保護とプライバシー](assets/data-protection-and-privacy-01.png)

## Adobe Experience Manager as a Cloud Service と規制への対応 {#aem-as-a-cloud-service-and-regulatory-readiness}

AEM as a Cloud Service の製品範囲に関する規制ドキュメントについては、以下の節を参照してください。

## Adobe Experience Manager as a Cloud Service の基盤 {#aem-foundation}

「[データ保護およびデータプライバシーに関する規制に対する AEM Foundation の対応](/help/compliance/data-privacy-and-protection-readiness/foundation-readiness.md)」を参照してください

## Adobe Experience Manager Sites as a Cloud Service {#aem-sites}

「[データ保護およびデータプライバシーに関する規制に対する AEM Sites の対応](/help/compliance/data-privacy-and-protection-readiness/sites-readiness.md)」を参照してください。

## Adobe Experience Manager as a Cloud Service と Adobe Target と Adobe Analytics の統合 {#aem-integration-with-adobe-target-adobe-analytics}

これらの Adobe Experience Manager as a Cloud Service 統合は、データ保護およびプライバシー（GDPR など）に対応したサービスと連携しています。Adobe Target や Adobe Analytics の個人データは、統合に関連して AEM に保存されません。
詳しくは、次のセクションを参照してください。

* [Adobe Target - プライバシーの概要](https://experienceleague.adobe.com/docs/target/using/implement-target/before-implement/privacy/privacy.html)

* [Adobe Analytics データプライバシーのワークフロー](https://experienceleague.adobe.com/docs/analytics/admin/data-governance/an-gdpr-workflow.html)
