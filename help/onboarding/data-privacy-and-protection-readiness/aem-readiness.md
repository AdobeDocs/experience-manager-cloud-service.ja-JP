---
title: データ保護とデータプライバシーに関する規制 — Adobe Experience Manager as a Cloud Service対応
description: 様々なデータ保護およびデータプライバシー規制のCloud ServiceサポートとしてのAdobe Experience Managerについて説明します。EU一般データ保護規則(GDPR)、カリフォルニア州消費者プライバシー法、新しいAEM as a Cloud Serviceプロジェクトを実装する際の準拠方法を含みます。
exl-id: 5dfa353b-84c5-4b07-bfcd-b03c2d361553
source-git-commit: 856266faf4cb99056b1763383d611e9b2c3c13ea
workflow-type: tm+mt
source-wordcount: '729'
ht-degree: 2%

---

# データ保護およびデータプライバシーに関する規制に対するCloud Service対応としてのAdobe Experience Manager {#aem-readiness-for-data-protection-and-data-privacy-regulations}

>[!WARNING]
>
>このドキュメントの内容は法的な助言にはならず、その代用になるものでもありません。
>
>データ保護およびデータプライバシー規制に関するアドバイスについては、貴社の法務部門にお問い合わせください。

>[!NOTE]
>
>Adobeのプライバシーに関する問題への対応と、Adobeのお客様への影響について詳しくは、[Adobeのプライバシーセンター](https://www.adobe.com/privacy.html)を参照してください。

Adobeは、お客様のプライバシー管理者またはAEM管理者がデータ保護およびデータプライバシー要求を処理し、お客様がこれらの規制に準拠できるよう支援するために、ドキュメントと手順（APIが利用可能な場合）を提供しています。 ドキュメントに記載されている手順を使用すると、お客様は、手動で、または（利用可能な場合は）外部のポータルやサービスからAPIを呼び出すことで、規制リクエストを実行できます。

>[!CAUTION]
>
>ここで説明する詳細は、Adobe Experience Manager as aCloud Serviceに制限されています。
>
>別のAdobeオンデマンドサービスのデータと、関連するプライバシーリクエストは、そのサービスで実行する必要があるアクションを必要とします。
>
>詳しくは、[Adobeのプライバシーセンター](https://www.adobe.com/privacy.html)を参照してください。

## はじめに {#introduction}

Adobe Experience Manager as aCloud Serviceと、それらで実行されるアプリケーションのインスタンスは、アドビのお客様が所有および操作します。

その結果、GDPR、CCPAなどのデータ保護規制は、お客様の責任が大きくなります。

簡単な紹介として、データのプライバシーと保護に関する規制には、次の役割が適用される新しいルールが含まれます。

* ビジネスエンティティ(CCPA)やデータ管理者(GDPR)

* サービスプロバイダー(CCPA)およびデータプロセッサー(GDPR)

この規則の主な規定は次の通りである。

1. すべての一意のIDを含むように個人データの定義を拡張。を直接的および間接的に特定できるデータに含める場合と同様です。

2. 同意に関する要件を強化しました。

3. 削除権限（データ消去）に重点を置きます。

4. データの販売のオプトアウト。

Adobe Experience Manager as aCloud Serviceの場合：

* インスタンスと、それらに対して実行されるアプリケーションは、顧客が所有および操作します。

   * これは、お客様が、ビジネス・エンティティやサービス・プロバイダ、データ管理者、データ処理者などの規制上の役割を効果的に管理することを意味します。

   * 次の図に示すように、Adobe Experience Platform Privacy ServiceはAEMのワークフローに含まれません。

* AEMには、お客様のプライバシー管理者やAEM管理者がプライバシー規制リクエストを実行するためのドキュメントと手順が含まれています。手動で、またはAPIを使用して（使用可能な場合）。

* 新しいサービスやUIが追加されていません。

   * 代わりに、プライバシー規制要求を処理する顧客UI/ポータルで使用する手順とAPIについて説明しています。

* AEMには、プライバシーリクエストワークフローをサポートする標準のツールは含まれません。

   * Adobeは、お客様のプライバシー管理者やAEM管理者向けのドキュメントや手順を提供し、プライバシー規制に関連するリクエストを手動で実行できるようにします。

Adobeは、Adobe Experience Managerのアクセス、削除、オプトアウトに関するプライバシーリクエストをCloud Serviceとして処理する手順を提供しています。 場合によっては、自動化に役立つように、顧客が開発したポータルまたはスクリプトから呼び出すことができるAPIが存在します。

次の図に、プライバシーリクエストワークフローがどのようになるかを示します(Adobe Experience Manager 6.5を使用した例)。

![データ保護とプライバシー](assets/data-protection-and-privacy-01.png)

## Adobe Experience Manager as aCloud Serviceと規制への対応{#aem-as-a-cloud-service-and-regulatory-readiness}

AEM as aCloud Serviceの製品領域に関する規制ドキュメントについては、以下の節を参照してください。

## Adobe Experience Manager as a Cloud Service の基盤 {#aem-foundation}

[データ保護およびデータプライバシー規制に対するAEM Foundationの対応](/help/onboarding/data-privacy-and-protection-readiness/foundation-readiness.md)を参照してください。

## Adobe Experience Manager Sites as a Cloud Service {#aem-sites}

[データ保護およびデータプライバシー規制に対するAEM Sitesの対応を参照してください。](/help/onboarding/data-privacy-and-protection-readiness/sites-readiness.md)

## Adobe Experience Manager as a Adobe TargetとAdobe AnalyticsのCloud Service統合{#aem-integration-with-adobe-target-adobe-analytics}

これらのAdobe Experience Manager as aCloud Service統合は、データ保護およびプライバシー（GDPRなど）に対応したサービスと連携しています。 Adobe TargetやAdobe Analyticsの個人データは、統合に関連してAEMに保存されません。
詳しくは、次のセクションを参照してください。

* [Adobe Target — プライバシーの概要](https://experienceleague.adobe.com/docs/target/using/implement-target/before-implement/privacy/privacy.html)

* [Adobe Analytics Data Privacy Workflow](https://experienceleague.adobe.com/docs/analytics/admin/data-governance/an-gdpr-workflow.html)
