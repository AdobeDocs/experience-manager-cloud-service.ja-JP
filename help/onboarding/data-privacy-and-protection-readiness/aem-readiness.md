---
title: データ保護とデータプライバシーに関する規制 — Adobe Experience Manager as a Cloud Service Readiness
description: '様々なデータ保護およびデータプライバシー規制に対するクラウドサービスサポートとしてのAdobe Experience Managerについて説明します。EUのGDPR(General Data Protection Regulation)、カリフォルニア消費者プライバシー法、およびクラウドサービスとして新しいAEMを導入する際の準拠方法を含む。 '
translation-type: tm+mt
source-git-commit: 2b7ee2b7b0ce351ed48aeb2f3135c947eafe7247

---


# Adobe Experience Manager as a Cloud Service Readiness for Data Protection and Data Privacy Regulations {#aem-readiness-for-data-protection-and-data-privacy-regulations}

>[!WARNING]
>
>本書の内容は、法律上の助言とはならず、法律上の助言の代替としての意味も持たない。
>
>データ保護およびデータプライバシー規制に関するアドバイスについては、貴社の法務部にお問い合わせください。

>[!NOTE]
>
>プライバシーに関する問題に対するアドビの対応、およびアドビのお客様にとっての意味について詳しくは、アドビのプライバシーセ [ンターを参照してください](https://www.adobe.com/privacy.html)。

アドビは、お客様のプライバシー管理者またはAEM管理者に対し、データ保護とデータプライバシーの要請を処理し、お客様がこれらの規制に準拠できるよう支援するため、ドキュメントと手順を提供しています。 ドキュメントに記載された手順により、顧客は手動で、または、可能な場合は外部のポータルやサービスからAPIに呼び出すことで、規制要求を実行できます。

>[!CAUTION]
>
>ここで説明する詳細は、クラウドサービスとしてのAdobe Experience Managerに制限されています。
>
>別のアドビオンデマンドサービスのデータは、関連するプライバシーリクエストと共に、そのサービスに対して行う必要があります。
>
>詳しくは、アドビのプライバ [シーセンターを参照してください](https://www.adobe.com/privacy.html)。

## 概要 {#introduction}

クラウドサービスとしてのAdobe Experience Managerのインスタンスと、それらで実行されるアプリケーションは、アドビのお客様が所有および運用します。

その結果、GDPR、CCPAなどのデータ保護に関する規制は、お客様の責任が大きく左右されます。

簡単に説明すると、データのプライバシーと保護に関する規制には、次の役割を果たす新しいルールが含まれます。

* CCPA（ビジネス・エンティティ）およびGDPR（データ・コントローラ）

* CCPA（サービス・プロバイダ）およびGDPR（データ・プロセッサ）

この規則の主な規定は次の通りである。

1. 個人データの定義を拡張し、すべての一意のIDを含める。を直接または間接的に識別可能なデータに含める場合と同様です。

2. 同意要件の強化。

3. 削除権限（データ消去）に重点を置くようになりました。

4. データ販売のオプトアウトを参照してください。

クラウドサービスとしてのAdobe Experience Managerの場合：

* インスタンスとそれら上で実行されるアプリケーションは、顧客が所有し、操作します。

   * つまり、ビジネス・エンティティやサービス・プロバイダ、データ・コントローラ、データ・プロセッサなど、規制上の役割を顧客が効果的に管理できます。

   * 次の図に示すように、Adobe Experience PlatformプライバシーサービスはAEMのワークフローには含まれません。

* AEMには、お客様のプライバシー管理者やAEM管理者がプライバシー規制の要請を実行するためのドキュメントと手順が含まれています。手動で、またはAPIを使用して（可能な場合）。

* 新しいサービスまたはUIが追加されていません。

   * 代わりに、プライバシー規制の要求を処理する顧客UI/ポータルで使用するための手順とAPIについて説明します。

* AEMには、プライバシーリクエストのワークフローをサポートする追加設定なしのツールは含まれません。

   * アドビは、お客様のプライバシー管理者やAEM管理者に対して、プライバシー規制に関連する要求を手動で実行できるようにドキュメントと手順を提供します。

アドビは、Adobe Experience Managerのクラウドサービスとしてのアクセス、削除およびオプトアウトに関するプライバシーリクエストを処理する手順を提供しています。 場合によっては、自動化を支援するために、顧客が開発したポータルまたはスクリプトから呼び出すことのできるAPIが存在します。

次の図に、プライバシーリクエストのワークフローがどのようになるかを示します（Adobe Experience Manager 6.5を使用して図を示します）。

![データ保護とプライバシー](assets/data-protection-and-privacy-01.png)

## クラウドサービスと規制対応 {#aem-as-a-cloud-service-and-regulatory-readiness}

クラウドサービスとしてのAEMの製品領域に関する規制に関するドキュメントについては、以下の節を参照してください。

## クラウドサービス基盤としてのAdobe Experience Manager {#aem-foundation}

『 [AEM Foundation Readiness for Data Protection』および『Data Privacy Regulations』を参照してください](/help/onboarding/data-privacy-and-protection-readiness/foundation-readiness.md)。

## クラウドサービスサイトとしてのAdobe Experience Manager {#aem-sites}

『 [AEM Sites Readiness for Data Protection』および『Data Privacy Regulations』を参照してください。](/help/onboarding/data-privacy-and-protection-readiness/sites-readiness.md)

## Adobe TargetとAdobe Analyticsのクラウドサービス統合としてのAdobe Experience Manager {#aem-integration-with-adobe-target-adobe-analytics}

クラウドサービス統合としてのAdobe Experience Managerは、データ保護とプライバシー（GDPRなど）対応のサービスと連携します。 Adobe targetまたはAdobe Analyticsの個人データは、統合に関連してAEMに保存されません。
詳しくは、次のセクションを参照してください。

* [Adobe Target — プライバシーの概要](https://docs.adobe.com/content/help/en/target/using/implement-target/before-implement/privacy/privacy.html)

* [Adobe Analyticsデータプライバシーワークフロー](https://docs.adobe.com/content/help/en/analytics/admin/data-governance/an-gdpr-workflow.html)
