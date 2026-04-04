---
title: Cloud Manager 2026.4.0 のリリースノート
description: Adobe Experience Manager as a Cloud Service の Cloud Manager 2026.4.0 のリリースについて説明します。
feature: Release Information
role: Admin
exl-id: 24d9fc6f-462d-417b-a728-c18157b23bbe
source-git-commit: aa8aba7f798e251c8a25ee247402e23517707e88
workflow-type: tm+mt
source-wordcount: '634'
ht-degree: 23%

---

# Adobe Experience Manager as a Cloud Service の Cloud Manager 2026.4.0 のリリースノート {#release-notes}

<!-- https://wiki.corp.adobe.com/display/DMSArchitecture/%5BKT%5D+Cloud+Manager+2025.08.0+Release -->

AEM（Adobe Experience Manager）as a Cloud Service の Cloud Manager 2026.4.0 のリリースについて説明します。

[Adobe Experience Manager as a Cloud Service の最新のリリースノート](/help/release-notes/release-notes-cloud/release-notes-current.md)も参照してください。

## リリース日 {#release-date}

AEM as a Cloud Service の Cloud Manager 2026.4.0 のリリース日は 2026年4月2日木曜日（PT）です。

次回のリリース予定は 2026年5月7日木曜日（PT）です。


## 新機能 – Cloud Manager {#cloud-manager-whats-new}

* **AIを活用したIDE用のCloud Manager MCP サーバー**

  Cloud Manager パブリック APIをAI対応IDE （Cursorなど）のツールとして公開するMCP （Model Context Protocol）サーバーを使用できるようになりました。 接続したら、対話型プロンプトを使用してプログラム、パイプライン、環境、リポジトリを一覧表示および管理し、エディターから離れることなく迅速に移動できます。

  ドキュメント [AEM as a Cloud ServiceでのMCPの使用](/help/ai-in-aem/mcp-support/using-mcp-with-aem-as-a-cloud-service.md)を参照してください。

  チュートリアル [Cloud Manager MCP Server](https://experienceleague.adobe.com/ja/docs/experience-manager-learn/cloud-service/ai/mcp-servers/cloud-manager#)を参照してください。

* **モジュールのキャッシュによるビルドの高速化**

  新しいビルドモデルでは、（リポジトリ全体ではなく）変更されたモジュールのみを、モジュールレベルのキャッシュを使用してコンパイルし、ビルド時間を短縮します。 これは、コード品質の実稼動以外のパイプラインと開発フルスタックの実稼動以外のパイプラインに適用されます。

  [実稼動以外のパイプラインでのスマートビルドの使用について](/help/implementing/cloud-manager/configuring-pipelines/configuring-non-production-pipelines.md#about-smart-build)および[実稼動以外のパイプラインの追加](/help/implementing/cloud-manager/configuring-pipelines/configuring-non-production-pipelines.md#full-stack-code)を参照してください。

* **セルフサービスのホスト接続性チェック**

  Cloud Managerでは、自分の環境からセルフサービスチェックを実行できるようになりました。 これらのチェックは、ホストとポートの到達性を確認し、エグレスを含むプログラムで設定されたネットワークパスを使用してDNS解決を確認します。 この機能により、サポートケースを開いたり、ポッドにアクセスしたりすることなく、高度なネットワークを検証し、統合の問題を迅速に解決することができます。<!-- SKYOPS-23640 -->

  [&#x200B; ネットワーク接続テスト &#x200B;](/help/security/network-connectivity-test.md)を参照してください

* **安定性、パフォーマンス、信頼性の向上**

  このリリースには、Cloud Managerの安定性、パフォーマンス、信頼性を向上させる最適化とメンテナンスのアップデートが含まれています。


## Beta プログラム {#private-beta-program}

Cloud Manager の Beta プログラムに参加すると、一般リリース前の新機能に特別アクセスできます。

>[!IMPORTANT]
>
>Beta リリースには欠陥が含まれている場合があり、いかなる保証もなしに「現状のまま」提供されます。 Adobeは、ベータ版のリリースを（Adobe サポートサービスまたはその他の方法により）維持、修正、更新、変更、またはその他の方法でサポートする義務を負いません。 Adobeでは、ベータ版リリースの正しい機能やパフォーマンス、または付随するドキュメントや資料に依存しないように注意することをお勧めします。 ベータ版の機能およびAPIは、予告なく変更される場合があります。 したがって、ベータ版リリースの使用は、完全にお客様の責任で行います。

[AEM Beta プログラム &#x200B;](/help/release-notes/release-notes-cloud/release-notes-current.md#aem-beta-programs)も参照

現在、次の機能が利用できます。

### Edge Delivery ServicesとAEMのオーサリングおよび柔軟なパブリッシュ層設定 {#eds-with-aem-authoring}

Cloud Managerには、最新の配信アーキテクチャをサポートするように設計された2つの機能が搭載されています。

* **AEM オーサリング機能を備えたEdge Delivery Services**
Edge Delivery Servicesを使用して、AEM オーサーモードで引き続きコンテンツをオーサリングしながらサイトを配信できるようになりました。 ワークフローの環境設定に応じて、次のオーサリングアプローチから選択できます。

   * ドキュメントベースのオーサリング
   * AEM オーサーベースのオーサリング

詳しくは、[Cloud ManagerでのEdge Delivery サイトの作成](/help/implementing/cloud-manager/edge-delivery/create-edge-delivery-site.md#one-click-edge-delivery-site)を参照してください。

* **柔軟なパブリッシュ階層設定**

Cloud Managerでは、プログラムに公開層が必要かどうかを設定できるようになりました。 この柔軟性により、選択した配信アーキテクチャに適した環境を設定できます。

詳しくは、[柔軟なパブリッシュ層（Beta） &#x200B;](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/creating-production-programs.md#flexible-publish-tier)を参照してください。

Betaに参加するには、[grp-beta_xwalk-publish_config@adobe.com](mailto:grp-beta_xwalk-publish_config@adobe.com)にAdobeの組織IDとプログラム IDをメールで送信してください。

### モジュールのキャッシュによるビルドの高速化 {#quick-build-cm-pipelines}

新しいビルドモデルでは、モジュールレベルのキャッシュを使用して、変更されたモジュールのみを（リポジトリ全体ではなく）コンパイルし、ビルド時間を短縮します。 本番パイプラインに適用されます。 **スマートビルド**&#x200B;を使用する実稼動パイプラインを制御します。

詳しくは、以下のトピックを参照してください。

* [実稼動パイプラインでのスマートビルドの使用](/help/implementing/cloud-manager/configuring-pipelines/configuring-non-production-pipelines.md#about-smart-build)。
* [実稼動パイプラインを追加](/help/implementing/cloud-manager/configuring-pipelines/configuring-non-production-pipelines.md#full-stack-code)。

Betaに参加するには、[beta_quickbuild_cmpipelines@adobe.com](mailto:beta_quickbuild_cmpipelines@adobe.com)にAdobe OrgIDとプログラム IDをメールで送信します。

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

2026年4月のCloud Manager リリースには、重大なバグ修正はありません。

<!-- ## Known issues {#known-issues} -->

