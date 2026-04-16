---
title: ADOBE EXPERIENCE MANAGER AS A CLOUD SERVICEのHIPAAへの対応
description: HIPAA規則に対するExperience Manager as a Cloud Serviceのサポートと、新しいAEM as a Cloud Service プロジェクトを実装する際に準拠する方法について説明します。
feature: Compliance
role: Admin, Architect, Developer, Leader
source-git-commit: 49721ac71bc2bde10eb5f25db58ee1b07c8a82e5
workflow-type: tm+mt
source-wordcount: '983'
ht-degree: 6%

---

# ADOBE EXPERIENCE MANAGER AS A CLOUD SERVICEのHIPAAへの対応 {#hipaa-readiness-for-adobe-experience-manager-as-a-cloud-service}

>[!WARNING]
>
>このドキュメントの内容は法的な助言にはならず、その代用になるものでもありません。
>
>HIPAA規制に関するアドバイスについては、会社の法務部門に相談してください。

>[!NOTE]
>
>プライバシーの問題に対するAdobeの対応と、これがAdobeのお客様にとって何を意味するかについては、次を参照してください。
>
>* Adobe Trust Centerの[HIPAAおよびAdobeの製品とサービス ](https://www.adobe.com/trust/compliance/hipaa-hds/hipaa-ready.html)
>* [Adobeのプライバシーセンター](https://www.adobe.com/jp/privacy.html)

Adobe Experience Manager（AEM）as a Cloud Serviceの場合、Adobeは、HIPAAへの対応を理解するのに役立つドキュメントを提供します。 これらの規制を遵守するのに役立ちます。

## 健康保険の相互運用性と説明責任に関する法律（HIPAA） {#health-insurance-portability-and-accountability-act-hipaa}

### 健康保険の相互運用性と説明責任に関する法律（HIPAA） {#the-health-insurance-portability-and-accountability-act-hipaa}

HIPAAのプライバシー、セキュリティ、および侵害の通知規則は、保護医療情報（PHI）として知られる個人を特定できる医療情報に対する重要な保護を確立します。

HIPAAでは、対象事業者は、医療提供者、医療計画、または医療クリアリングハウスです。 ビジネスアソシエイトとは、PHIへのアクセスを含む対象事業者にサービスを提供する事業者のことです。 HIPAAのプライバシーとセキュリティ規則は、対象事業者が事業提携契約（BAA）の形式で事業提携事業者から書面による保証を得ることを要求しており、事業提携事業者は対象事業者のPHIのプライバシーとセキュリティを保護する必要があります。

### AdobeへのPHIの提供 {#providing-phi-to-adobe}

Adobeは、[AEM as a Cloud ServiceのHIPAA サービスの準備](#hipaa-readiness-of-services-in-aem-as-a-cloud-service)に記載されているHIPAA対応サービスのビジネスアソシエイトとして機能します。

PHI **を処理するためにAdobe HIPAA対応サービスのライセンスを取得するお客様は、正しいライセンスとAdobeとの署名済みBAAを持っている必要があります。**

>[!IMPORTANT]
>
>お客様は、HIPAA対応サービスとして指定されていない、またはHIPAA対応サービスを使用するための適切なライセンスがないAdobe製品およびサービスを通じて、PHIを作成、受信、管理、または送信することはできません。

### HIPAAの責任の共有 {#hipaa-shared-responsibilities}

Adobe HIPAA対応サービスは、共通の責任セキュリティモデルに依存しており、PHIのセキュリティを維持するための明確な責任をお客様とAdobeがそれぞれ負う必要があります。 この共有セキュリティモデルでは、Adobeはお客様がHIPAAに準拠したHIPAA対応サービスを使用して設定することに依存します。

HIPAA対応サービスに対するAdobe BAAの実行について詳しくは、Adobeの営業担当者またはカスタマーサクセスマネージャーにお問い合わせください。

>[!IMPORTANT]
>
>**免責事項**:
>
>お客様は、Adobe HIPAA対応サービスの使用と、Adobe HIPAA対応サービスがコンプライアンス要件を満たしていることを確認する責任があります。

詳しくは、Adobe Trust Centerの[HIPAAおよびAdobeの製品とサービス ](https://www.adobe.com/trust/compliance/hipaa-hds/hipaa-ready.html)を参照してください。

## HIPAA用語 {#hipaa-terminology}

次の表は、AEM サービスをHIPAA使用に分類する方法を示しています。

| HIPAA対応 | 説明 |
| --- | --- |
| HIPAA対応 | 適切に設定され、BAAで使用される場合にPHIを処理するように設計されています。 |
| HIPAAに対応していない | PHIを処理するように設計されておらず、HIPAA関連のユースケースで使用しないでください。 |

>[!NOTE]
>
>HIPAA対応度の分類は、各サービスの意図した機能に基づいており、時間の経過とともに変化する可能性があります。
>
>顧客は、HIPAA関連のデプロイメントを計画する際に、最新のドキュメントと適用可能な契約条件を参照する必要があります。

## AEM AS A CLOUD SERVICEのHIPAA対応サービス {#hipaa-readiness-of-services-in-aem-as-a-cloud-service}

次の表では、HIPAA対応のAEM サービスと、そのサービスと共に使用できるサービスについて説明します。 HIPAA対応サービスでは、[追加の要件](#additional-requirements)の説明に従って、Extended Security for Healthcareを購入する必要があります。

| 製品/能力 | サービス | HIPAA対応 |
| --- | --- | --- |
| AEM Sites | AEM Sites、AEM Publish、Edge Delivery Services | HIPAA対応 |
| AEM Sites | ユニバーサルエディター | HIPAA対応ではありません<br>[1] PHIが導入されていない場合は、拡張セキュリティプログラムに追加できます。 |
| AEM Sites Optimizer | Sites Optimizer | HIPAA対応ではありません<br>[1] PHIが導入されていない場合は、拡張セキュリティプログラムに追加できます。 |
| AEM Assets | AEM Assets | HIPAA対応 |
| AEM Assets | コンテンツハブ | HIPAA対応ではありません<br>[1] PHIが導入されていない場合は、拡張セキュリティプログラムに追加できます。 |
| AEM Assets | Brand Portal | HIPAAに対応していない |
| AEM Assets | Dynamic Media OpenAPI | HIPAA対応ではありません<br>[1] PHIが導入されていない場合は、拡張セキュリティプログラムに追加できます。 |
| AEM Assets | Dynamic Media Scene 7 | HIPAAに対応していない |
| AEM Forms | AEM Forms、Authentication Facade Service、PDF Utility Service | HIPAA対応 |
| AEM CIF | コマース統合フレームワーク | HIPAAに対応していない |
| AEM Cloud Manager | AEM Cloud Manager、リリースオーケストレーター、リリーストグル、リリースバリデーター | HIPAA対応 |
| AEM Cloud Manager | ソフトウェア配布 | HIPAA対応ではありません<br>[1] PHIが導入されていない場合は、拡張セキュリティプログラムに追加できます。 |
|   |   |   |
| AEM Guides  | AEM Guides  | HIPAAに対応していない |
|   |   |   |
| LLM Optimizer | LLM Optimizer | HIPAA対応ではありません<br>[1] PHIが導入されていない場合は、拡張セキュリティプログラムに追加できます。 |

>[!NOTE]
>
>[1]
>
>拡張セキュリティ プログラムに追加できるHIPAA対応サービスではないとして示されるサービスの場合、お客様は、PHIがこれらのサービスにルーティングされたり保存されたりしないようにしてください。
>
>HIPAAに対応していないサービスにPHIを導入すると、コンプライアンス違反につながる可能性があります。

### 追加要件 {#additional-requirements}

HIPAA対応として[ リストされているサービス ](#hipaa-readiness-of-services-in-aem-as-a-cloud-service)には、Extended Security for Healthcareの購入が必要です。

Extended Security for Healthcareを購入する場合、次の要件があります。

* そのプログラムに選択された製品は、HIPAA対応です（表に示すように）。
* Extended Security for Healthcareは、*個の製品ごとに購入されました。これにより、十分なCloud Manager クレジットが確保されます。*
* Extended Security for Healthcareは、プログラム作成時に適用されます。

要件が満たされた場合は、AEM プログラムの作成時にExtended Security for Healthcareを適用できます。詳しくは、[Setup](#setup)を参照してください。

>[!NOTE]
>
>プロビジョニングと価格設定の詳細については、営業担当者までお問い合わせください。

## 環境 {#environments}

*HIPAA対応*&#x200B;は、RDE （迅速な開発環境）、開発環境、またはステージ環境には適用されません。これらの環境ではPHIは許可されていません。

つまり、次のことをおこなう必要があります。

* 開発とテストのためにダミーデータを使用します
* 実稼動環境のPHIのみを処理

次の表は、環境タイプをHIPAA対応としてサポートできる場所を示しています。

| | RDE | 開発 | ステージ  | 製品 |
| --- | --- | --- | --- | --- |
| 環境タイプ  | いいえ  | いいえ  | いいえ  | はい  |

## セットアップ {#setup}

[実稼動プログラムを作成](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/creating-production-programs.md)すると、「[ セキュリティ」タブに、HIPAA保護を有効にするオプションが表示されます](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/creating-production-programs.md#security)。