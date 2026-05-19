---
title: Cloud Manager 2026.5.0のリリースノート
description: Adobe Experience Manager as a Cloud ServiceのCloud Manager 2026.5.0のリリースについて説明します。
feature: Release Information
role: Admin
exl-id: 24d9fc6f-462d-417b-a728-c18157b23bbe
source-git-commit: 93e633b8c9ac2f0bc03df70d3419b70d7b2ea7ba
workflow-type: tm+mt
source-wordcount: '496'
ht-degree: 10%

---

# Adobe Experience Manager as a Cloud ServiceのCloud Manager 2026.5.0のリリースノート {#release-notes}

<!-- https://wiki.corp.adobe.com/display/DMSArchitecture/%5BKT%5D+Cloud+Manager+2025.08.0+Release -->

AEM（Adobe Experience Manager）as a Cloud ServiceのCloud Manager 2026.5.0のリリースについて説明します。

[Adobe Experience Manager as a Cloud Service の最新のリリースノート](/help/release-notes/release-notes-cloud/release-notes-current.md)も参照してください。

## リリース日 {#release-date}

AEM as a Cloud ServiceのCloud Manager 2026.5.0のリリース日は2026年5月7日木曜日です。

次回のリリース予定は2026年6月4日木曜日（木）です。


## 新機能 – Cloud Manager {#cloud-manager-whats-new}

* 実稼動プログラムの&#x200B;**ソフト削除**

  Cloud Managerでは、ソフト削除ワークフローを使用して実稼動プログラムを削除できるようになりました。 削除されたプログラムは30日以内に復元でき、永久的な削除の前に追加の安全ウィンドウが提供されます。 この機能は5月を通して段階的に展開されています。

  [削除する実稼動プログラムのマークを付ける](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/editing-programs.md#delete-production-program)を参照してください。

## Beta プログラム {#private-beta-program}

Cloud Manager の Beta プログラムに参加すると、一般リリース前の新機能に特別アクセスできます。

>[!IMPORTANT]
>
>Beta リリースには欠陥が含まれている場合があり、いかなる保証もなしに「現状のまま」提供されます。 Adobeは、ベータ版のリリースを（Adobe サポートサービスまたはその他の方法により）維持、修正、更新、変更、またはその他の方法でサポートする義務を負いません。 Adobeでは、ベータ版リリースの正しい機能やパフォーマンス、または付随するドキュメントや資料に依存しないように注意することをお勧めします。 ベータ版の機能およびAPIは、予告なく変更される場合があります。 したがって、ベータ版リリースの使用は、完全にお客様の責任で行います。

[AEM Beta プログラム ](/help/release-notes/release-notes-cloud/release-notes-current.md#aem-beta-programs)も参照

現在、次のベータプログラムの機会が利用可能です。

### Edge Delivery ServicesとAEMのオーサリングおよび柔軟なパブリッシュ層設定 {#eds-with-aem-authoring}

Cloud Managerには、最新の配信アーキテクチャをサポートするように設計された2つの機能が搭載されています。

* AEM オーサリング機能を備えた&#x200B;**Edge Delivery Services**
Edge Delivery Servicesを使用して、AEM オーサーモードで引き続きコンテンツをオーサリングしながらサイトを配信できるようになりました。 ワークフローの環境設定に応じて、次のオーサリングアプローチから選択できます。

   * ドキュメントベースのオーサリング
   * AEM オーサーベースのオーサリング

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

2026年5月のCloud Manager リリースには、重大なバグ修正はありません。

<!-- ## Known issues {#known-issues} -->

