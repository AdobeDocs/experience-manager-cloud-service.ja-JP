---
title: Cloud Manager 2026.6.0のリリースノート
description: Adobe Experience Manager as a Cloud ServiceのCloud Manager 2026.6.0のリリースについて説明します。
feature: Release Information
role: Admin
exl-id: 24d9fc6f-462d-417b-a728-c18157b23bbe
source-git-commit: 61101046e4383acb534b04f467bef1b0313c4ef5
workflow-type: tm+mt
source-wordcount: '726'
ht-degree: 4%

---

# Adobe Experience Manager as a Cloud ServiceのCloud Manager 2026.6.0のリリースノート {#release-notes}

<!-- 
https://wiki.corp.adobe.com/display/DMSArchitecture/%5BKT%5D+Cloud+Manager+2025.08.0+Release 
-->

AEM（Adobe Experience Manager）as a Cloud ServiceのCloud Manager 2026.6.0のリリースについて説明します。

[Adobe Experience Manager as a Cloud Service の最新のリリースノート](/help/release-notes/release-notes-cloud/release-notes-current.md)も参照してください。

## リリース日 {#release-date}

AEM as a Cloud ServiceのCloud Manager 2026.6.0のリリース日は2026年6月4日木曜日です。

次回のリリース予定は2026年7月9日木曜日（木）です。


## 新機能 – Cloud Manager {#cloud-manager-whats-new}

* **顧客管理キー（CMK）のセルフサービス**
お客様は、Adobe サポートの関与を必要とせずに、Cloud Managerから直接顧客管理キーを設定できるようになりました。 新しいCMK オプションは、プログラムの作成中、プログラムの編集設定、および環境の詳細ページで使用できます。

  CMK ステータスは、マイプログラムカードおよびライセンスダッシュボードに表示され、管理者はすべての環境で暗号化設定を明確に把握できます。 このアプローチにより、独自の暗号化キーの制御が必要な組織のコンプライアンスワークフローが簡素化されます。

  ![顧客管理キーのアイコンを表示しているマイ プログラム カード ](/help/implementing/cloud-manager/release-notes/assets/cmk-status-on-program-card.png)
  *自分のプログラム カード*


  ![実稼動用に設定ダイアログボックスに、「顧客が管理するキー」オプションが選択された「セキュリティ」タブが表示されている](/help/implementing/cloud-manager/release-notes/assets/cmk-security-tab-in-set-up-for-production-dlg.png)
  実稼動用に設定ダイアログボックスの「セキュリティ」タブで&#x200B;*顧客管理キーが選択されました*

  ![ ライセンスダッシュボードで使用可能な顧客管理キーの数を表示](/help/implementing/cloud-manager/release-notes/assets/cmk-license-dashboard.png)
  *ライセンスダッシュボードで使用可能な顧客管理キーの数を表示*

* **環境変数の制限が400に増加**
Cloud Managerでは、1つの環境につき最大400個の環境変数をサポートするようになりました。これは、以前の制限である200個から2倍になります。

  パイプライン変数の上限は200のままです。 UIは、コンテキストごとに正しい制限を適用し、許可されたしきい値を超える追加を防ぎます。

  この変更は、より多くの環境固有の設定を必要とする、より複雑なデプロイメント設定を持つお客様をサポートします。

<!--CMGR-76755 · CMGR-76753 -->


## Beta プログラム {#private-beta-program}

一般リリースの前に、今後の機能に限定でアクセスするには、Cloud Managerのベータ版プログラムに参加してください。

>[!IMPORTANT]
>
>Beta リリースには欠陥が含まれており、いかなる保証もなしに「現状のまま」提供されます。 Adobeは、ベータ版リリースの保守、修正、更新、変更、その他のサポートを行う義務を負いません。 お客様は、独自のリスクでベータリリースを使用し、ベータリリースの正しい機能やパフォーマンス、または付随するドキュメントや資料に依存しないでください。 ベータ版の機能およびAPIは、予告なく変更される場合があります。 ベータ版リリースの使用は、完全にお客様の責任で行います。

[AEM Beta プログラム ](/help/release-notes/release-notes-cloud/release-notes-current.md#aem-beta-programs)も参照

現在、次のベータプログラムの機会が利用可能です。

### Edge Delivery ServicesとAEMのオーサリングおよび柔軟なパブリッシュ層設定 {#eds-with-aem-authoring}

Cloud Managerには、最新の配信アーキテクチャをサポートするように設計された2つの機能が搭載されています。

* AEM オーサリング機能を備えた&#x200B;**Edge Delivery Services**
Edge Delivery Servicesを使用して、AEM オーサーモードで引き続きコンテンツをオーサリングしながらサイトを配信できるようになりました。 ワークフローの環境設定に応じて、次のオーサリングアプローチから選択できます。

   * ドキュメントベースのオーサリング
   * AEMベースのオーサリング

詳しくは、[Cloud ManagerでのEdge Delivery サイトの作成](/help/implementing/cloud-manager/edge-delivery/create-edge-delivery-site.md#one-click-edge-delivery-site)を参照してください。

* **柔軟なパブリッシュ階層設定**

Cloud Managerでは、プログラムに公開層が必要かどうかを設定できるようになりました。 この柔軟性により、選択した配信アーキテクチャに適した環境を設定できます。

詳しくは、[柔軟なパブリッシュ層（Beta） ](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/creating-production-programs.md#flexible-publish-tier)を参照してください。

Betaに参加するには、[grp-beta_xwalk-publish_config@adobe.com](mailto:grp-beta_xwalk-publish_config@adobe.com)にAdobeの組織IDとプログラム IDをメールで送信してください。

### モジュールのキャッシュによるビルドの高速化 {#quick-build-cm-pipelines}

新しいビルドモデルでは、モジュールレベルのキャッシュを使用して、変更されたモジュールのみを（リポジトリ全体ではなく）コンパイルし、ビルド時間を短縮します。 本番パイプラインに適用されます。 **スマートビルド**&#x200B;を使用する実稼動パイプラインを制御します。

詳しくは、次を参照してください。

* [実稼動パイプラインでのスマートビルドの使用](/help/implementing/cloud-manager/configuring-pipelines/configuring-non-production-pipelines.md#about-smart-build)。
* [実稼動パイプラインを追加](/help/implementing/cloud-manager/configuring-pipelines/configuring-non-production-pipelines.md#full-stack-code)。

Betaに参加するには、[beta_quickbuild_cmpipelines@adobe.com](mailto:beta_quickbuild_cmpipelines@adobe.com)にAdobeの組織IDとプログラム IDをメールで送信してください。

<!-- 
OLD
### Experience Hub Extensibility and Customization {#exp-hub-extensibility}

[Experience Hub](/help/experience-hub.md) serves as your entry point to AEM, customized for your organization's needs. Tell Adobe about your existing AEM UI Extensions so they can help you enable them in Experience Hub with minimal effort.

![Diagram of Experience Hub extensibility and customization workflow](/help/implementing/cloud-manager/release-notes/assets/experience-hub-extensibility-customization.png)

Embed custom experiences in Experience Hub to extend and personalize your organization's dashboard. In addition to Adobe's built-in widgets, add your own using the [UI Extensibility](https://developer.adobe.com/uix/docs/) framework. Build JavaScript-based UI apps and surface them to your users to meet business-specific requirements and workflows. 

Interested in the beta? Email [beta_exphubextensibility@adobe.com](mailto:beta_exphubextensibility@adobe.com) with your Adobe OrgID and a short description of the customization you intend to create.
-->

<!-- 
OLD
### Support for Custom Author Domains in Cloud Service

AEM Cloud Service is going to soon support one custom domain per Author environment.
-->



## バグ修正 {#bug-fixes}

* アクティブな操作がないので、**環境が更新中に停止しました**
パイプラインの実行や設定の変更が進行中でない場合でも、環境が更新状態で永続的に停止する問題が解決されました。 影響を受ける環境は、Adobe サポートから手動で操作することなく、正常に管理できるようになりました。 （CMGR-77133）
* **アドバンスド ネットワーク – 重複するソース ポートで間違ったポート転送ルールが削除されました**
Advanced Networkingの2つのポート転送ルールが同じソースポート（portOrig）を共有している場合、一方のルールを削除すると、もう一方のルールが誤って削除されます。 Cloud Managerは、意図したルールのみを正しく識別して削除するようになりました。 （CMGR-77019）

<!-- There are no significant bug fixes in the June 2026 Cloud Manager release. -->

<!-- ## Known issues {#known-issues} -->

