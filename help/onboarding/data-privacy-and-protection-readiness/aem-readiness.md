---
title: データ保護とデータのプライバシーに関する規制 — Adobe Experience Manager as a Cloud Service Readiness
description: '様々なデータ保護およびデータのプライバシーに関する規則に対するクラウドサービスのサポートとしてのAdobe Experience Managerについて説明します。 EU General Data Protection Regulation(GDPR)、California Consumer Privacy Act、およびクラウドサービスとして新しいAEMを導入する際の準拠方法を含む。 '
translation-type: tm+mt
source-git-commit: 2b7ee2b7b0ce351ed48aeb2f3135c947eafe7247
workflow-type: tm+mt
source-wordcount: '733'
ht-degree: 1%

---


# Adobe Experience Manager(Adobe Experience Manager as a Cloud Service Readiness for Data Protection and Data Privacy Regulations) {#aem-readiness-for-data-protection-and-data-privacy-regulations}

>[!WARNING]
>
>このドキュメントの内容は法律上の助言とはならず、法律上の助言の代わりとしての意味も持たない。
>
>データ保護およびデータのプライバシーに関する規制に関するアドバイスについては、会社の法務部にお問い合わせください。

>[!NOTE]
>
>プライバシーに関する問題に対するアドビの対応、およびアドビのお客様にとっての意味について詳しくは、アドビのプライバシーセンター [を参照してください](https://www.adobe.com/privacy.html)。

アドビは、お客様のプライバシー管理者またはAEM管理者がデータ保護とデータのプライバシーの要請を処理し、お客様がこれらの規則に準拠できるように支援するため、ドキュメントと手順（利用可能な場合はAPIを使用）を提供しています。 ドキュメントに記載された手順により、顧客は手動で、または、可能な場合は外部のポータルやサービスからAPIに呼び出すことで、規制要求を実行できます。

>[!CAUTION]
>
>ここに記載される詳細は、クラウドサービスとしてのAdobe Experience Managerに制限されています。
>
>別のAdobeオンデマンドサービスのデータは、関連するプライバシー要求と共に、そのサービスでの処置が必要になります。
>
>詳しくは、 [アドビのプライバシーセンターを参照してください](https://www.adobe.com/privacy.html)。

## 概要 {#introduction}

クラウドサービスとしてのAdobe Experience Managerのインスタンスと、それらで実行されるアプリケーションは、アドビのお客様が所有および運用します。

その結果、GDPR、CCPAなどのデータ保護に関する規制は、お客様の責任が大きく左右されます。

簡単に説明すると、データのプライバシーと保護に関する規則には、次の役割を果たす新しい規則が含まれます。

* CCPA(Business Entities)および/またはGDPR(Data Controller)

* サービスプロバイダー(CCPA)および/またはGDPR(Data Processor)

この規則の主な規定は次の通りである。

1. 個人データの定義が拡張され、一意のIDがすべて含まれるようになりました。 を直接または間接的に識別可能なデータとして扱う場合と同様です。

2. 同意要件を強化しました。

3. 削除権限（データ消去）に対する焦点を高めました。

4. データ販売のオプトアウトを参照してください。

クラウドサービスとしてのAdobe Experience Managerの場合：

* インスタンスと、それらに対して実行されるアプリケーションは、顧客が所有し、操作します。

   * つまり、ビジネス・エンティティやサービスプロバイダー、データ・コントローラ、データ・プロセッサなど、規制上の役割をお客様が管理するということです。

   * 次の図に示すように、Adobe Experience Platformプライバシーサービスは、AEMのワークフローには含まれません。

* AEMには、お客様のプライバシー管理者またはAEM管理者がプライバシー規制の要請を実行するためのドキュメントと手順が含まれています。 手動で、またはAPI経由で（使用可能な場合）。

* 新しいサービスまたはUIが追加されていません。

   * 代わりに、プライバシー規制の要求を処理するお客様のUI/ポータルでの使用に関する手順とAPIについて説明しています。

* AEMには、プライバシー要求のワークフローをサポートする標準ツールは含まれません。

   * アドビは、お客様のプライバシー管理者またはAEM管理者、あるいはその両方に関するドキュメントと手順を提供し、お客様がプライバシー規制に関連する要求を手動で実行できるようにします。

アドビは、Adobe Experience Managerのクラウドサービスとしてのアクセス、削除、オプトアウトに関するプライバシー要求を処理する手順を提供しています。 場合によっては、自動化を支援するために、お客様が開発したポータルまたはスクリプトから呼び出すことのできるAPIがあります。

次の図に、プライバシーリクエストワークフローの例を示します（Adobe Experience Manager 6.5を使用した図）。

![データ保護とプライバシー](assets/data-protection-and-privacy-01.png)

## クラウドサービスと規制対応におけるAdobe Experience Manager {#aem-as-a-cloud-service-and-regulatory-readiness}

クラウドサービスとしてのAEMの製品領域に関する規制に関するドキュメントについては、以下の節を参照してください。

## Adobe Experience Manager as a Cloud Service Foundation {#aem-foundation}

See [AEM Foundation Readiness for Data Protection and Data Privacy Regulations](/help/onboarding/data-privacy-and-protection-readiness/foundation-readiness.md).

## Adobe Experience Manager Sites as a Cloud Service {#aem-sites}

See [AEM Sites Readiness for Data Protection and Data Privacy Regulations.](/help/onboarding/data-privacy-and-protection-readiness/sites-readiness.md)

## クラウドサービスとしてのAdobe Experience ManagerとAdobeターゲットおよびAdobe Analyticsとの統合 {#aem-integration-with-adobe-target-adobe-analytics}

クラウドサービス統合としてのAdobe Experience Managerは、データ保護とプライバシー（GDPRなど）に対応したサービスと連携しています。 AdobeターゲットまたはAdobe Analyticsの個人データは、統合に関連してAEMに保存されません。
詳しくは、次のセクションを参照してください。

* [アドビターゲット — プライバシーの概要](https://docs.adobe.com/content/help/en/target/using/implement-target/before-implement/privacy/privacy.html)

* [Adobe Analyticsデータプライバシーワークフロー](https://docs.adobe.com/content/help/en/analytics/admin/data-governance/an-gdpr-workflow.html)
