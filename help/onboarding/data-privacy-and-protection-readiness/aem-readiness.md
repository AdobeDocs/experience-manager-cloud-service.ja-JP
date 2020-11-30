---
title: データ保護とデータのプライバシーに関する規制 —Cloud Service準備に関するAdobe Experience Manager
description: '様々なData Protection and Data Privacy RegulationsのCloud ServiceサポートとしてAdobe Experience Managerについて説明します。EU General Data Protection Regulation(GDPR)、California Consumer Privacy Act（カリフォルニア消費者プライバシー法）、新しいAEMをCloud Serviceプロジェクトとして導入する際の遵守方法を含む。 '
translation-type: tm+mt
source-git-commit: 2b7ee2b7b0ce351ed48aeb2f3135c947eafe7247
workflow-type: tm+mt
source-wordcount: '733'
ht-degree: 2%

---


# データ保護とデータプライバシー規制に対するCloud Service準備としてのAdobe Experience Manager {#aem-readiness-for-data-protection-and-data-privacy-regulations}

>[!WARNING]
>
>このドキュメントの内容は法律上の助言とはならず、法律上の助言の代わりとしての意味も持たない。
>
>データ保護およびデータのプライバシーに関する規制に関するアドバイスについては、会社の法務部にお問い合わせください。

>[!NOTE]
>
>プライバシーに関する問題に対するAdobeの対応、およびAdobeのお客様にとっての意味について詳しくは、 [Adobeのプライバシーセンター](https://www.adobe.com/privacy.html)を参照してください。

Adobeは、お客様のプライバシー管理者またはAEM管理者がデータ保護とデータプライバシーの要請を処理し、お客様がこれらの規制に準拠できるように、ドキュメントと手順を（APIを使用して）提供しています。 ドキュメントに記載された手順により、顧客は手動で、または、可能な場合は外部のポータルやサービスからAPIに呼び出すことで、規制要求を実行できます。

>[!CAUTION]
>
>詳細はCloud ServiceとしてAdobe Experience Managerに限定。
>
>別のAdobeのオンデマンドサービスのデータは、関連するプライバシー要求と共に、そのサービスでの処置が必要になります。
>
>詳しくは、 [Adobeのプライバシーセンターを参照してください](https://www.adobe.com/privacy.html)。

## 概要 {#introduction}

Cloud ServiceとしてのAdobe Experience Managerの事例や、それらで実行されるアプリケーションは、弊社のお客様が所有し、運営しています。

その結果、GDPR、CCPAなどのデータ保護に関する規制は、お客様の責任が大きく左右されます。

簡単に説明すると、データのプライバシーと保護に関する規則には、次の役割を果たす新しい規則が含まれます。

* CCPA(Business Entities)および/またはGDPR(Data Controller)

* サービスプロバイダー(CCPA)および/またはGDPR(Data Processor)

この規則の主な規定は次の通りである。

1. 個人データの定義が拡張され、一意のIDがすべて含まれるようになりました。を直接または間接的に識別可能なデータとして扱う場合と同様です。

2. 同意要件を強化しました。

3. 削除権限（データ消去）に対する焦点を高めました。

4. データ販売のオプトアウトを参照してください。

Cloud ServiceとしてのAdobe Experience Managerの場合：

* インスタンスと、それらに対して実行されるアプリケーションは、顧客が所有し、操作します。

   * つまり、ビジネス・エンティティやサービスプロバイダー、データ・コントローラ、データ・プロセッサなど、規制上の役割をお客様が管理するということです。

   * 下の図に示すように、Adobe Experience Platform Privacy ServiceはAEMのワークフローに含まれません。

* AEMには、お客様のプライバシー管理者およびAEM管理者がプライバシー規制の要請を実行するためのドキュメントと手順が含まれます。手動で、またはAPI経由で（使用可能な場合）。

* 新しいサービスまたはUIが追加されていません。

   * 代わりに、プライバシー規制の要求を処理するお客様のUI/ポータルでの使用に関する手順とAPIについて説明しています。

* AEMには、プライバシー要求のワークフローをサポートする追加設定なしのツールは含まれません。

   * Adobeは、お客様のプライバシー管理者またはAEM管理者に関するドキュメントと手順を提供し、プライバシー規制に関する要求を手動で実行できるようにします。

Adobeは、Adobe Experience Managerのアクセス、削除、およびオプトアウトに関するプライバシー要求をCloud Serviceとして処理する手順を提供しています。 場合によっては、自動化を支援するために、お客様が開発したポータルまたはスクリプトから呼び出すことのできるAPIがあります。

次の図に、プライバシーリクエストワークフローの例を示します(Adobe Experience Manager6.5を使用した図を参照)。

![データ保護とプライバシー](assets/data-protection-and-privacy-01.png)

## Cloud Serviceと規制への対応としてのAdobe Experience Manager {#aem-as-a-cloud-service-and-regulatory-readiness}

Cloud ServiceとしてのAEMの製品領域に関する規制に関するドキュメントについては、以下の節を参照してください。

## Adobe Experience Manager as a Cloud Service の基礎 {#aem-foundation}

See [AEM Foundation Readiness for Data Protection and Data Privacy Regulations](/help/onboarding/data-privacy-and-protection-readiness/foundation-readiness.md).

## Adobe Experience Manager Sites as a Cloud Service {#aem-sites}

See [AEM Sites Readiness for Data Protection and Data Privacy Regulations.](/help/onboarding/data-privacy-and-protection-readiness/sites-readiness.md)

## Adobe Target&amp;Adobe AnalyticsとのCloud Service統合としてのAdobe Experience Manager {#aem-integration-with-adobe-target-adobe-analytics}

Cloud Service統合としてのAdobe Experience Managerは、データ保護とプライバシー（GDPRなど）に対応したサービスを提供します。 統合に関連して、Adobe TargetやAdobe Analyticsからの個人データはAEMに格納されない。
詳しくは、次のセクションを参照してください。

* [Adobe Target — プライバシーの概要](https://docs.adobe.com/content/help/en/target/using/implement-target/before-implement/privacy/privacy.html)

* [Adobe Analyticsデータのプライバシーワークフロー](https://docs.adobe.com/content/help/en/analytics/admin/data-governance/an-gdpr-workflow.html)
