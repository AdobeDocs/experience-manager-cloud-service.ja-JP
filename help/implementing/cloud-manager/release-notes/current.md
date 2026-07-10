---
title: Cloud Manager 2026.7.0のリリースノート
description: Adobe Experience Manager as a Cloud ServiceのCloud Manager 2026.7.0のリリースについて説明します。
feature: Release Information
role: Admin
exl-id: 24d9fc6f-462d-417b-a728-c18157b23bbe
source-git-commit: dea8a3df29876df1c97454a97602045eb50121ad
workflow-type: tm+mt
source-wordcount: '932'
ht-degree: 3%

---

# Adobe Experience Manager as a Cloud ServiceのCloud Manager 2026.7.0のリリースノート {#release-notes}

AEM（Adobe Experience Manager）as a Cloud ServiceのCloud Manager 2026.7.0のリリースについて説明します。

[Adobe Experience Manager as a Cloud Service の最新のリリースノート](/help/release-notes/release-notes-cloud/release-notes-current.md)も参照してください。

## リリース日 {#release-date}

AEM as a Cloud ServiceのCloud Manager 2026.7.0のリリース日は2026年7月9日木曜日です。

次回のリリース予定は2026年8月6日木曜日（木）です。


## 新機能 – Cloud Manager {#cloud-manager-whats-new}

* **自分のGitを持ち込む（BYOG） — Git クローンのシークレットベースの認証**

  IMS トークンに加えて、Cloud Managerが生成するbyogit シークレットを使用して、[!DNL Bring Your Own Git] リポジトリへのGit クローン リクエストを認証できるようになりました。 この機能を使用すると、[!DNL Edge Delivery Services]のお客様は、helix-adminが既にコード同期のために保存しているのと同じ資格情報を使用できます。 既存のIMS認証コピーワークフローは影響を受けません。

  [Git クローン要求の認証](/help/implementing/cloud-manager/edge-delivery/config-edge-delivery-site-with-byog.md#authenticate-git-clone-requests)を参照してください。

* **VPN ネットワーク インフラストラクチャ — BGP ルーティングと複数の接続**\
  Advanced Networking VPN ネットワーク インフラストラクチャ APIは、既存のスタティック ルーティングと並行してBGP （Border Gateway Protocol）ダイナミック ルーティングをサポートするようになりました。 お客様側のBGP Autonomous System Numberとピアリングアドレスを指定することで、接続ごとにBGPを設定できます。Cloud Managerは、ルートラーニングを動的に処理します。静的なプレフィックスは必要ありません。

  インフラストラクチャごとに1つのVPN接続の以前の制限も削除されました。 複数の接続が同じインフラストラクチャ内でサポートされるようになり、静的な接続とBGP接続を共存させることができます。 これにより、AEM Cloud Service環境用にVPN トポロジを設計する際に、エンタープライズネットワーキングチームがより柔軟になります。

* **モジュールのキャッシュによるビルド パフォーマンスの向上**
新しいビルドモデルでは、モジュールレベルのキャッシュを使用して、変更されたモジュールのみを（リポジトリ全体ではなく）コンパイルし、ビルドパフォーマンスを向上させます。 本番パイプラインに適用されます。 **スマートビルド**&#x200B;を使用する実稼動パイプラインを制御します。

  詳しくは、次を参照してください。

   * [実稼動パイプラインでのスマートビルドの使用について](/help/implementing/cloud-manager/configuring-pipelines/configuring-non-production-pipelines.md#about-smart-build)および[実稼動以外のパイプラインでのスマートビルドの使用について](/help/implementing/cloud-manager/configuring-pipelines/configuring-non-production-pipelines.md#about-smart-build-non-production-pipeline)
   * [実稼動パイプラインを追加](/help/implementing/cloud-manager/configuring-pipelines/configuring-non-production-pipelines.md#full-stack-code)および[実稼動以外のパイプラインを追加](/help/implementing/cloud-manager/configuring-pipelines/configuring-non-production-pipelines.md#configuring-non-production-pipelines)。

* **コンテンツのコピー：プログラム間および転送フロー**\
  Cloud Manager **Content Copy**&#x200B;では、デプロイメントなしでAEM環境間でコンテンツをコピーできます。この機能には、すべてのプログラムで利用できる2つの機能が含まれています。 プログラム間サポートを使用すると、同じプログラム内だけでなく、複数のCloud Manager プログラム間でコンテンツをコピーできます。 転送フローでは、方向制限が削除され、コンテンツを任意の環境から他の環境（下位環境を含む）にコピーできます。


## Beta プログラム {#private-beta-program}

一般リリースの前に、今後の機能に限定でアクセスするには、Cloud Managerのベータ版プログラムに参加してください。

>[!IMPORTANT]
>
>Beta リリースには欠陥が含まれており、いかなる保証もなしに「現状のまま」提供されます。 Adobeは、ベータ版リリースの保守、修正、更新、変更、その他のサポートを行う義務を負いません。 お客様は、ベータリリースを独自のリスクで使用します。ベータリリースの正しい機能やパフォーマンス、または付随するドキュメントや資料に依存しないでください。 ベータ版の機能およびAPIは、予告なく変更される場合があります。 ベータ版リリースの使用は、完全にお客様の責任で行います。

[AEM Beta プログラム &#x200B;](/help/release-notes/release-notes-cloud/release-notes-current.md#aem-beta-programs)も参照

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

詳しくは、[柔軟なパブリッシュ層（Beta） &#x200B;](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/creating-production-programs.md#flexible-publish-tier)を参照してください。

ベータ版に参加するには、[grp-beta_xwalk-publish_config@adobe.com](mailto:grp-beta_xwalk-publish_config@adobe.com)にAdobeの組織IDとプログラム IDをメールで送信してください。

<!-- 
OLD
### Improved build performance with module caching {#quick-build-cm-pipelines}

A new build model compiles only changed modules (rather than the entire repository) using module-level caching to improve build performance. It applies to production pipelines. You control which production pipelines use **Smart Build**.

For more information, see the following:

* [Using Smart Build in a production pipeline](/help/implementing/cloud-manager/configuring-pipelines/configuring-non-production-pipelines.md#about-smart-build).
* [Add a production pipeline](/help/implementing/cloud-manager/configuring-pipelines/configuring-non-production-pipelines.md#full-stack-code).

To join the Beta, email [beta_quickbuild_cmpipelines@adobe.com](mailto:beta_quickbuild_cmpipelines@adobe.com) with your Adobe Organization ID and Program ID.

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

* 両方の実稼動グループ環境が同時にソフト削除を完了すると、コアクレジットはリリースされません。 この問題は解決されました。 同時削除が完了した順序に関係なく、クレジットが正しくリリースされるようになりました。 （CMGR-77845）

* Content Hub クレジットは、環境のソフト削除後に孤立し、その後ハード削除が続きます。 関連する環境が完全に削除されたときに、Cloud ManagerがContent Hub クレジットを正しくリリースするようになりました。 （CMGR-77585）

* aio cloudmanager:tail-log CLI コマンドは、再接続ではなく、ログローテーション時に切断されます。 ログのローテーションが検出されたときに、コマンドが自動的に再接続されるようになりました。 （CMGR-76557）

* プログラムの概要で完全なダイアログのコンテンツをスクロールできない。 ダイアログボックスが正しくスクロールされるようになり、画面サイズに関係なくすべてのコンテンツにアクセスできるようになりました。 （CMGR-76405）

* 新しく作成されたRDE環境で、カスタムドメインマッピングが失敗する。 新しい高速開発環境（RDE）を作成した後、プロビジョニング直後にカスタムドメインマッピングを追加しようとすると、「環境ステータスがドメイン設定の変更に対して無効です」というエラーが発生しました。Cloud Managerは、ドメインマッピングを試みる前に、環境の「準備完了」ステートを正しく反映するようになりました。 （CMGR-75904）

* DV証明書を削除し、同じドメインに再作成すると、「既存の証明書」エラーが発生して失敗します。 お客様がドメイン検証済み（DV）証明書を削除し、同じドメインに新しい証明書を作成しようとすると、Cloud Managerで「すべてのドメインをカバーする既存の証明書があります」というエラーが返されました。 その結果、新しい証明書の発行がブロックされました。 UIでは削除は成功したように見えましたが、内部的に証明書が完全に削除されず、ドメインがロックされたままになりました。 この問題は解決されました。 （CMGR-72784）

<!-- There are no significant bug fixes in the July 2026 Cloud Manager release. -->

<!-- ## Known issues {#known-issues} -->

