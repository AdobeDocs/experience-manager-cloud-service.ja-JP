---
title: Cloud Manager 2026.3.0 のリリースノート
description: Adobe Experience Manager as a Cloud Service の Cloud Manager 2026.3.0 のリリースについて説明します。
feature: Release Information
role: Admin
exl-id: 24d9fc6f-462d-417b-a728-c18157b23bbe
source-git-commit: eb3e826e27e14b8b1da534440f11d43e973130ec
workflow-type: tm+mt
source-wordcount: '715'
ht-degree: 23%

---

# Adobe Experience Manager as a Cloud Service の Cloud Manager 2026.3.0 のリリースノート {#release-notes}

<!-- https://wiki.corp.adobe.com/display/DMSArchitecture/%5BKT%5D+Cloud+Manager+2025.08.0+Release -->

AEM（Adobe Experience Manager）as a Cloud Service の Cloud Manager 2026.3.0 のリリースについて説明します。

[Adobe Experience Manager as a Cloud Service の最新のリリースノート](/help/release-notes/release-notes-cloud/release-notes-current.md)も参照してください。

## リリース日 {#release-date}

AEM as a Cloud Service の Cloud Manager 2026.3.0 のリリース日は 2026年3月5日木曜日（PT）です。

次回のリリース予定は 2026年4月2日木曜日（PT）です。


## 新機能 – Cloud Manager {#cloud-manager-whats-new}

* **Cloud Managerでは、{ コンテンツのコピー** 読み込みに対して **ワイプ** オプションをサポートするよう **なりました**

  **ワイプ** を有効にすると、Cloud Managerは、読み込みを開始する前に宛先にある既存のコンテンツを削除するので、新しい状態から開始して、既存のコンテンツとの競合を避けることができます。 **ワイプ** を無効にしたままにすると、Cloud Managerでは、既存のコピー先コンテンツの上に新しいコンテンツがインポートされます。 ワイプが開始される前に確認プロンプトが表示され、Cloud Managerはトレーサビリティのためにワイプ操作と読み込みの詳細をログに記録します。

  [ コンテンツをコピー ](/help/implementing/developing/tools/content-copy.md#copy-content) も参照してください。

* **AEM Experience Hubでの UI 拡張機能のサポート**
[AEM Experience Hub](https://experience.adobe.com/experiencemanager) で UI 拡張機能がサポートされるようになり、開発者はAdobe App Builderを使用して作成されたカスタム機能やウィジェットを使用してインターフェイスを拡張できるようになりました。

  詳しくは、[AEM Experience Hub](https://developer.adobe.com/uix/docs/services/aem-experience-hub/) を参照してください。

* **安定性、パフォーマンス、信頼性の向上**

  このリリースには、Cloud Managerの安定性、パフォーマンス、信頼性を向上させる最適化およびメンテナンスの更新が含まれています。


## Beta プログラム {#private-beta-program}

Cloud Manager の Beta プログラムに参加すると、一般リリース前の新機能に特別アクセスできます。

>[!IMPORTANT]
>
>Beta リリースには不具合が含まれている場合があり、いかなる保証もなく「現状のまま」提供されます。 Adobeは、ベータ版リリースの保守、修正、更新、変更、またはその他のサポート（Adobe サポートサービスを通じてまたはその他の方法で）を行う義務を負いません。 Adobeでは、お客様に対して、ベータ版リリースが正しく機能するか、パフォーマンスが向上するか、あるいはこれらに付随するドキュメントや資料を使用しないよう、注意して助言しています。 ベータ版の機能と API は、予告なく変更される場合があります。 したがって、ベータ版リリースの使用は、完全にお客様自身の責任で行います。

[AEM Beta プログラム ](/help/release-notes/release-notes-cloud/release-notes-current.md#aem-beta-programs) も参照してください。

現在、次の機能が利用できます。
<!--
### Support for Custom Author Domains in Cloud Service

AEM Cloud Service is going to soon support one custom domain per Author environment.-->

### AI を利用した IDE 向けCloud Manager MCP サーバー{#mcp-server-for-cm}

Cloud Manager Public API を AI 対応 IDE のツール（Cursor など）として公開する MCP （Model Context Protocol）サーバーを試すことができるようになりました。 接続すると、対話型プロンプトを使用してプログラム、パイプライン、環境、リポジトリを一覧表示および管理できるようになり、エディターを離れることなく迅速に移動できます。

[AEM as a Cloud Serviceでの MCP の使用 ](/help/ai-in-aem/mcp-support/using-mcp-with-aem-as-a-cloud-service.md) のドキュメントを参照してください。

チュートリアル [Cloud Manager MCP Server](https://experienceleague.adobe.com/en/docs/experience-manager-learn/cloud-service/ai/mcp-server/cloud-manager#) を参照してください。

ベータ版にご興味がありますか？Adobeの OrgID とプログラム ID を記載したメール [0}GRP-AEM-CM-MCP-FEEDBACK@adobe.com} を送信します。](mailto:GRP-AEM-CM-MCP-FEEDBACK@adobe.com)


<!--
### Experience Hub Extensibility and Customization {#exp-hub-extensibility}

[Experience Hub](/help/experience-hub.md) serves as your entry point to AEM, customized for your organization's needs. Tell Adobe about your existing AEM UI Extensions so they can help you enable them in Experience Hub with minimal effort.

![Diagram of Experience Hub extensibility and customization workflow](/help/implementing/cloud-manager/release-notes/assets/experience-hub-extensibility-customization.png)

Embed custom experiences in Experience Hub to extend and personalize your organization's dashboard. In addition to Adobe's built-in widgets, add your own using the [UI Extensibility](https://developer.adobe.com/uix/docs/) framework. Build JavaScript-based UI apps and surface them to your users to meet business-specific requirements and workflows. 

Interested in the beta? Email [beta_exphubextensibility@adobe.com](mailto:beta_exphubextensibility@adobe.com) with your Adobe OrgID and a short description of the customization you intend to create.
-->

### モジュールのキャッシュによるビルドの高速化 {#quick-build-cm-pipelines}

新しいビルドモデルでは、（リポジトリ全体ではなく）変更されたモジュールのみを、モジュールレベルのキャッシュを使用してコンパイルし、ビルド時間を短縮します。これは、コード品質、フルスタック、ステージ専用のパイプラインに適用されます。

![ フルビルドとスマートビルドの 2 つのビルド戦略オプションが表示されている実稼動以外のパイプラインを編集ダイアログボックス ](/help/implementing/cloud-manager/release-notes/assets/non-production-pipeline-edit.png)
*フルビルドとスマートビルドの 2 つのビルド戦略オプションが表示されている実稼動以外のパイプラインを編集ダイアログボックス。*

**パイプラインを追加/編集** ダイアログボックスの「**Sourceコード**」タブにある新しい **ビルド方法** セクションで、次のいずれかのビルドオプションを選択できます。

* **フルビルド** – 実行ごとにリポジトリ内のすべてのモジュールをビルドします。
* **スマートビルド** – 前回のコミット以降に変更されたモジュールのみをビルドし、全体的なビルド時間を短縮します。

使用するパイプラインを制御できます **スマートビルド**。 ベータ版では、このオプションは **コード品質** パイプラインと **開発デプロイメント** パイプラインにのみ表示されます。

ご興味がある場合Adobe OrgID とプログラム ID を記載して [beta_quickbuild_cmpipelines@adobe.com](mailto:beta_quickbuild_cmpipelines@adobe.com) にメールでお問い合わせください。

<!-- You can deactivate incremental builds at the pipeline level by setting the property `CM_BUILD_DISABLE_MODULE_CACHING` to `true` (effective during the `BUILD` step). For how to add pipeline variables, see [Pipeline Variables in Cloud Manager](/help/implementing/cloud-manager/configuring-pipelines/pipeline-variables.md).-->

## バグ修正 {#bug-fixes}

* 復元ポイントを取得する際に、Restore Points API が 500 エラーを返す可能性がある問題を修正しました。 エンドポイントで null 値が正しく処理されるようになり、一貫性と信頼性の高い応答が保証されるようになりました。 （CMGR-72963）
* Cloud Managerは、`.git` サフィックスの付いた GitHub リポジトリ URL または付いていない GitHub リポジトリ URL を受け入れるようになり、API の動作を UI に合わせ、リポジトリのオンボーディングをより柔軟にします。 （CMGR-73296）
* 製品プロファイル名の検証で大文字と小文字が区別されなくなり、大文字とのみ異なる名前のプロファイルを作成する際のエラーを防ぐようになりました。 （CMGR-74075）
* 同じパイプライン実行から複数の復元操作を実行できるようになりました。これにより、新しいパイプラインの実行を必要とせずに、ステージング環境や実稼動環境などの環境を順次復元できます。 （CMGR-73538）


<!-- ## Known issues {#known-issues} -->

