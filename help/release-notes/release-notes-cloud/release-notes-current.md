---
title: ' [!DNL Adobe Experience Manager] as a Cloud Serviceの最新のリリースノート'
description: ' [!DNL Adobe Experience Manager]  as a Cloud Service の最新のリリースノート。'
mini-toc-levels: 1
exl-id: a2d56721-502c-4f4e-9b72-5ca790df75c5
feature: Release Information
role: Admin
source-git-commit: eae7609f3f35f17a6c31cf242b6b0cc2d464a3fb
workflow-type: tm+mt
source-wordcount: '1961'
ht-degree: 35%

---

# [!DNL Adobe Experience Manager] as a Cloud Service の最新のリリースノート {#release-notes}

以下のセクションでは、[!DNL Experience Manager] as a Cloud Service の現在（最新）のバージョンの機能リリースノートの概要について説明します。

>[!NOTE]
>
>ここから、以前のバージョン（例えば、2023年、2024年）のリリースノートに移動できます。
>
>[!DNL Experience Manager] as a Cloud Service の今後の機能のアクティベーションについての詳細は、[Experience Manager リリースロードマップ](https://experienceleague.adobe.com/ja/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap)をご覧ください。

>[!NOTE]
>
>Experience Cloud リリースノートの更新に関するメール通知を毎月受信するには、[アドビ製品アップデートの優先通知](https://www.adobe.com/subscription/priority-product-update.html)を購読してください。

## リリース日 {#release-date}

[!DNL Adobe Experience Manager] as a [!DNL Cloud Service] の最新の機能リリース（2026.2.0）のリリース日は、2026年3月3日（PT）です。次回の機能リリース（2026.3.0）は 2026年3月26日（PT）に予定されています。

## メンテナンスリリースノート {#maintenance}

最新のメンテナンスリリースノートについては、[こちら](/help/release-notes/maintenance/latest.md)をご覧ください。

## リリースビデオ {#release-video}

2026.2.0 リリースで追加された機能の概要については、2026年2月リリースの概要ビデオをご覧ください。

>[!VIDEO](https://video.tv.adobe.com/v/3480399/?quality=12)


## AEM Beta プログラム {#aem-beta-programs}

Adobe Experience Manager（AEM）ベータプログラムを使用すると、プレリリース機能やコードにアクセスし、フィードバックを提供し、AEMの将来を導くことができます。

>[!IMPORTANT]
>
>Beta リリースには不具合が含まれている場合があり、いかなる保証もなく「現状のまま」提供されます。 Adobeは、ベータ版リリースの保守、修正、更新、変更、またはその他のサポート（Adobe サポートサービスを通じてまたはその他の方法で）を行う義務を負いません。 Adobeでは、お客様に対して、ベータ版リリースが正しく機能するか、パフォーマンスが向上するか、あるいはこれらに付随するドキュメントや資料を使用しないよう、注意して助言しています。 ベータ版の機能と API は、予告なく変更される場合があります。 したがって、ベータ版リリースの使用は、完全にお客様自身の責任で行います。

**参加のメリット**
Adobeが開発中の機能に早期にアクセスすることで、お客様およびパートナーはフィードバックを提供し、製品開発を具体化できます。 また、GA 前に新しい機能を導入する準備をするのに役立ちます。

**現在のベータ版プログラム**
次の節では、アクティブなベータプログラムを示します。

### AEMのエージェント {#agents-in-aem}

実稼働、ガバナンス、最適化、検出、開発にわたる、強力な新しいAEMエージェンティック機能を探索したい場合は、[ こちらからアクセスする方法をご覧ください ](/help/ai-in-aem/agents/overview.md)。

<!--
### Agents in AEM (Explorer program) {#agents-in-aem-beta-program}

Gain early access to powerful, new AEM agentic capabilities across production, governance, optimization, discovery, and development. Your feedback directly shapes Adobe's roadmap and final features. See [Overview of Agents in AEM](/help/ai-in-aem/agents/overview.md) to learn more.

This program typically lasts 4-6 weeks, but can be tailored to be flexible around your ability to actively participate. 

To opt in to participate in this program, email [aemagentsteam@adobe.com](mailto:aemagentsteam@adobe.com) and include the following details to the extent possible:

* Names and Adobe ID's of team members who will actively use agents.
* List Specific agents that you or your team will want to use. Or simply say "All Agents."

Customers selected for participation will be notified directly by Adobe. Participation is subject to eligibility considerations, including customer licensing and limited program capacity. While not all requests can be accommodated initially, additional customers may be considered in future beta waves.
-->

### AEM財団（Beta プログラム） {#aem-foundation-beta-programs}

[AEM Foundation ベータプログラム ](#foundation-early-adopter) を参照してください。

### Cloud Manager（Beta プログラム） {#cloud-manager-beta-programs}

[Cloud Manager ベータプログラム ](/help/implementing/cloud-manager/release-notes/current.md) を参照してください。

## [!DNL Experience Manager Assets] as a [!DNL Cloud Service] {#assets}

**Adobe ExpressでAEM Assetsにアクセスするためのコンテンツアドバイザー**

[ コンテンツアドバイザーがAdobe Expressで利用できるようになりました ](/help/assets/native-integration-adobe-express.md)。Express インターフェイス内で直接AEM Assets用のインテリジェントなアセット検出が導入されます。 コンテンツアドバイザーは、キャンバスコンテンツとキャンペーン概要に基づいて、コンテキストに対応したレコメンデーションを提供し、AI を利用した検索をサポートします。また、Dynamic Media などを活用した、チャネル対応のオンザフライ レンディションのネイティブサポートを有効にします。 コンテンツアドバイザーは、ユーザーが承認済みアセットを検出して使用する方法を変換し、適切なコンテンツをすばやく見つけてクリエイティブワークフローを合理化するのに役立ちます。

### OpenAPI を使用した Dynamic Media の新機能 {#dynamic-media-openAPI-new-features}

**OpenAPI を使用した Dynamic Media の属性ベースのアクセス制御（ABAC）**

属性ベースのアクセス制御（ABAC）を使用すると、管理者は、メタデータ駆動型ルールを使用して、OpenAPI アセットを使用して Dynamic Media へのアクセスを制御できます。 管理者は、アセットのメタデータに基づいてユーザーグループのルールを定義し、特定のグループに表示するアセットを決定することができます。 アセットのメタデータが定義済みの条件に一致すると、アクセスが自動的に許可されます。 この機能は、組織がより良いガバナンスを実施するのに役立ち、ユーザーが自分の役割や権限に関連する OpenAPI アセットを使用して Dynamic Media のみを表示および操作できるようにします。

>[!NOTE]
>
>OpenAPI を使用した Dynamic Media の属性ベースのアクセス制御（ABAC）は、使用制限機能です。 [ サポートチケット ](https://helpx.adobe.com/jp/enterprise/using/support-for-experience-cloud.html) を作成することで、有効にすることができます。

## [!DNL Experience Manager Forms] as a [!DNL Cloud Service] {#forms}

### AEM Forms の早期アクセス機能 {#forms-early-access-features}

**送信PDFでの複数選択ドロップダウンのラベルの表示**
アダプティブFormsの複数選択ドロップダウンコンポーネントで、選択した表示ラベルが [ 生成された送信PDF](/help/forms/generate-document-of-record-core-components.md) でレンダリングされるようになり、フォームで表示される内容がドキュメントに正確に反映されるようになりました。

**チェックボックス、ラジオボタン、パネルコンポーネントのアクセシビリティの強化**
アダプティブ Forms コアコンポーネントでは、[ チェックボックスグループ（v2） ](https://experienceleague.adobe.com/en/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/checkbox-group)、[ ラジオボタングループ（v2） ](https://experienceleague.adobe.com/en/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/radio-button) および [ パネルコンポーネント ](https://experienceleague.adobe.com/ja/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/panel) に WCAG 2.2 準拠のセマンティックマークアップが導入されています。 これらのコンポーネントは、`<fieldset>` と `<legend>` HTMLの要素を活用して、グループラベルとそのオプションとの間に有意義な関係を確立し、スクリーンリーダーやその他の支援テクノロジーによって正確な解釈を可能にします。

**Forms Manager でのバージョン管理のサポート**
Forms Manager では [ アダプティブ Forms（コアコンポーネントと基盤コンポーネント） ](/help/forms/manage-form-versions-forms-manager.md) フォームフラグメント、テーマ、XDP テンプレート、バイナリアセットのバージョン管理をサポートするようになりました。 Formsとドキュメント コンソールを使用して、バージョンを作成したり、完全なバージョン履歴を表示したり、フォームアセットの以前の状態を復元したりできます。

## [!DNL Experience Manager] as a [!DNL Cloud Service] の基盤 {#foundation}

### [!DNL Experience Manager] as a [!DNL Cloud Service] Foundation の新機能 {#foundation-new}

#### 自動メンテナンスアップデートの一時停止 {#pause-updates}

運用開始日、ライブイベント、ピーク時の売上といった瞬間を逃すことはできません。[ 新しいセルフサービス機能 ](/help/implementing/deploying/quiet-hours-update-free-periods.md)により、重要な場合に自動メンテナンスアップデートを停止し、チームが集中できるようにします。

* 静かな時間：毎日設定された時間に自動メンテナンスをブロックします。勤務時間、夜間の実行や朝の切り替え時などに最適です。
* 更新不要の期間：自動メンテナンスを 1 週間ブロックします。ローンチ、プロモーションまたは年次フリーズに使用します。

#### 開発エージェントを使用したコード品質パイプラインのトラブルシューティング {#devagent-codequality}

開発エージェントのパイプライントラブルシューティング機能を使用すると、デベロッパーはAEM as a Cloud Serviceのデプロイメントの問題をより効率的に診断し解決できます。

以前は **ビルドと単体テスト** の手順に重点を置いていましたが、パイプラインのトラブルシューティングでは、フルスタックデプロイメントおよびコード品質パイプラインの **コードスキャン** の手順もサポートするようになりました。

コードスキャン ステップは、品質ルールに照らしてコードを評価し、セキュリティの脆弱性を検出して、詳細な品質レポートを生成します。 この手順が失敗した場合は、AI アシスタントを使用して、開発エージェントに対して、推奨される修正ガイダンスと共に根本原因分析を求めることができます。

[ 開発エージェント ](/help/ai-in-aem/agents/brand-experience/development/development.md) とパイプラインのトラブルシューティングについて詳しく説明します。

### [!DNL Experience Manager] as a [!DNL Cloud Service] Foundation に関する重要な注意事項 {#foundation-notices}

#### Java API の非推奨化 {#java-api-deprecation}

2026 年 2 月 26 日（PT）の削除をターゲットにした非推奨の API は、コードでは使用されなくなります。 デプロイメントブロックを防ぐには、2026 年 3 月 30 日（PT）より前に、API の使用を削除します。 重要な日付：

* **2026 年 1 月 26 日以降**：これらの API の使用を削除するためのリマインダーとして、アクションセンターの通知メールが送信されます。
* **2026 年 2 月 26 日（PT）**：これらの API を使用したコードを含むCloud Manager パイプラインは、**コード品質** ステップ中に **一時停止** されます。 デプロイメントマネージャー、プロジェクトマネージャーまたはビジネスオーナーは、問題をオーバーライドしてパイプラインを続行できます。 *これにより、コードの変更を検証してリリースする機能が低下する可能性があります。*
* **2026 年 3 月 30 日（PT）**：これらの API を使用したコードを含むCloud Manager パイプラインは、**コード品質** ステップ中に **失敗** します。 非推奨（廃止予定）の API の使用が削除されるまで、デプロイメントはブロックされます。 *これにより、時間に依存する更新をリリースできなくなる可能性があり、ビジネス運営に影響を与える可能性があります。*
* **2026 年 5 月 4 日（PT）**：非推奨（廃止予定）の API をまだ使用している環境 **Adobeの重要なリリースアップデートを受け取ることはありません** また、パフォーマンスと可用性に関するAdobeの標準コミットメントには従いません。 その結果、新機能やバグ修正を受け取ることができず、アプリケーションの安定性と稼働時間に悪影響が及ぶ可能性があり、セキュリティリスクのリスクがさらに高まる可能性があります。

詳しくは、[非推奨（廃止予定）に関する記事](/help/release-notes/deprecated-removed-features.md#aem-apis)を参照してください。便宜上、これらの API を次に示します。

+++ 展開して Java API の非推奨（廃止予定）について確認

* `org.apache.sling.commons.auth`
* `org.apache.felix.webconsole`
* `org.eclipse.jetty`
* `com.mongodb`
* `org.apache.abdera`
* `org.apache.felix.http.whiteboard`
* `org.apache.cocoon.xml`
* `ch.qos.logback`
* `org.slf4j.spi`
* `org.slf4j.event`
* `org.apache.log4j`
* `com.google.common`
* `com.drew`
* `org.apache.jackrabbit.oak.plugins.memory`

+++

<!--
OSGi properties:

* `org.apache.sling.commons.log.LogManager` (all properties)
* `org.apache.sling.commons.log.LogManager.factory.config` (`org.apache.sling.commons.log.file`, `org.apache.sling.commons.log.pattern`)
* 

-->

### [!DNL Experience Manager] as a [!DNL Cloud Service] 基盤の早期導入者の機能 {#foundation-early-adopter}

#### AEM Edge関数（Beta プログラム） {#edge-functions}

AEM Edge関数を使用すると、CDN レイヤーでJavaScriptを実行し、データ処理をエンドユーザーに近づけることができます。 これにより待ち時間が短縮され、エッジでレスポンシブな動的エクスペリエンスが実現します。

一般的なユースケースを次に示します。

* 位置情報、デバイスタイプまたはユーザー属性に基づくコンテンツのパーソナライズ
* CDN と接触チャネルの間のミドルウェアとして機能させる
* サードパーティの API からの応答をブラウザーに配信する前に再フォーマットする（および複数の API 応答を集計する）
* 様々なバックエンドからステッチされたコンテンツを使用し、サーバーレンダリングされた HTML をエッジで作成および提供
* ChatGPT や Claude などの LLM がカスタムツールにアクセスできるように MCP サーバーを公開する

AEM パブリッシュ配信またはライブ実稼動サイトのEdge Delivery Services プロジェクトで利用できる機会の数は限られています。 参加に関心がある場合や、詳細を確認したい場合は、ユースケースの簡単な説明を添えて [aemcs-edgecompute-feedback@adobe.com](mailto:aemcs-edgecompute-feedback@adobe.com)までメールでご連絡ください。

#### Cloud Manager MCP サーバー（Beta プログラム） {#cm-mcp-server}

>[!VIDEO](https://video.tv.adobe.com/v/3480340/?quality=12)

最新の IDE では、Model Context Protocol （MCP）を使用して、大規模な言語モデル（LLM）が MCP サーバーによって公開されたツールを呼び出せるようにします。 開発者は、低レベルの API 仕様に直接統合するのではなく、自然言語で意図を簡単に説明できます。

ベータ版が利用可能になったCloud Manager MCP サーバーでは、プロンプトを使用して、IDE から直接Cloud Manager API を操作できます。 サポートされるシナリオには、パイプラインの実行、環境ステータスの確認などがあります。

[AEM MCP サーバー ](/help/ai-in-aem/mcp-support/using-mcp-with-aem-as-a-cloud-service.md) の詳細情報。 Cloud Manager MCP サーバーのベータ版へのアクセスをリクエストするには、[aemcs-mcp-feedback@adobe.comにメールを送信し ](mailto:aemcs-mcp-feedback@adobe.com) ユースケースの説明を含めます。

#### 開発エージェント（Beta プログラム）を使用した web 階層設定パイプラインのトラブルシューティング {#devagent-webtier}

開発エージェントの [ パイプライントラブルシューティング ](/help/ai-in-aem/agents/brand-experience/development/development.md) 機能は、開発者がAEM as a Cloud Serviceのデプロイメントの問題を効率的に診断し解決するのに役立ちます。 開発エージェントは、フルスタックパイプライン（デプロイメントとコード品質）のサポートに加えて、ベータ版プログラムの一部として **web 階層設定パイプライン** のトラブルシューティングをサポートするようになりました。

ベータ版へのアクセスをリクエストするには、[aem-devagent@adobe.com](mailto:aem-devagent@adobe.com) にメールを送信します。 AEMのエージェントに対する既存のアクセスが必要です。

>[!NOTE]
>
>9 月 25 日に不具合機能として使用可能になります。
>プログラムでアクティブ化するには、[aemcs-update-free@adobe.com](mailto:aemcs-update-free@adobe.com) にメールを送信してください。
>

#### AEM Java およびDispatcher開発用の IDE AI ツール（Beta プログラム） {#ai-dev-beta}

Java スタックチームは、Cursor、Cloud Code、Visual Studio、IntelliJ などのツールで AI を利用した開発を使用して、機能の配信を高速化し、コード品質を向上させています。 ベータ版に参加して、次のことを行います。

* Adobeでサポートされる将来の AI 機能の形成に役立つ、実際のエクスペリエンスを共有する
* AI エージェントでAEM コードおよび Dispatcher 設定の生成とデバッグに使用できる IDE ツールを試す

詳しくは、[aemcs-java-adopter@adobe.com](mailto:aemcs-java-adopter@adobe.com) にメールを送信してください。

#### AEM 6.5 から AEM Cloud Service への移行に対応する IDE AI ツール（Alpha プログラム） {#cm-ide-migration}

IDE AI ツールを使用して、[ ベストプラクティスアナライザーレポート ](/help/journey-migration/best-practices-analyzer/overview-best-practices-analyzer.md) の推奨事項に従って行動することで、AEM 6.5 からAEM as a Cloud Service（Java スタック）への移行を高速化します。

詳しくは、[aem-devagent@adobe.com](mailto:aem-devagent@adobe.com) にメールを送信してください。

#### Edge Delivery Services の Edge 認証（Beta プログラム） {#edge-authentication}

Edge 認証を使用すると、Edge Delivery Services ページへのアクセスを、ID プロバイダー（IdP）で認証されたユーザーのみに制限できます。これを実現するには、OpenID Connect（OIDC）設定の YAML ファイルをデプロイします。

ご興味がある場合は、ユースケースの簡単な説明とご質問を [aemcs-edgecompute-feedback@adobe.com](mailto:aemcs-edgecompute-feedback@adobe.com) までお問い合わせください。

#### ライブトラフィックを受け入れる前にコードをテストするための Canary 実稼動デプロイメント（Beta プログラム） {#canary-beta}

エンドユーザーに公開する前に、内部専用テストトラフィックを使用して実稼動ビルドを検証します。実稼動環境に出荷し、Canary トラフィックのみをルーティング（特別なヘッダーを使用）し、動作を監視してから、顧客に影響を与えることなく、ライブトラフィックに昇格するか、ロールバックします。

コードリリースを実稼動環境にデプロイしますが、ライブトラフィックを受け入れるかロールバックするかを決定する前に、内部テストトラフィックのみに制限します。

アクセスをリクエストしてフィードバックを共有するには、[aemcs-canary-deployments-beta@adobe.com](mailto:aemcs-canary-deployments-beta@adobe.com) にメールを送信してください。

#### RDE のスナップショット（Betaプログラム） {#rde-snapshot-program}

ベータ版の迅速な開発環境（RDE）で、現在のコードとコンテンツの状態をスナップショットとして取り、後で復元できる機能がサポートされるようになりました。 これは、元に戻す必要がある場合のあるコードを同期する場合や、異なる機能の開発を切り替える場合に役立つことがあります。 また、テストの既知の開始点として、可変コンテンツのみを復元することもできます。

この機能の使用やフィードバックの提供に関心がある場合は、[aemcs-rde-support@adobe.com](mailto:aemcs-rde-support@adobe.com) にメールを送信してください。

#### アプリケーションパフォーマンスモニタリング（APM）の拡張（Alpha プログラム） {#apm-alpha}

観測性のために、AEM Cloud Service は現在、アドビ提供の [New Relic One](https://experienceleague.adobe.com/ja/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/user-access-new-relic)と顧客管理の [Dynatrace](https://experienceleague.adobe.com/ja/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/dynatrace) をサポートしています。追加の APM オプションのサポートを検討中ですので、ユースケースと共に、ご希望のベンダーまたはテクノロジーを記載したメールを [aemcs-apm-beta@adobe.com](mailto:aemcs-apm-beta@adobe.com) までお送りください。

## [!DNL Experience Manager] ガイド {#guides}

Adobe Experience Manager Guides の最新リリースの新機能と強化機能の完全なリストについては、[こちら](https://experienceleague.adobe.com/ja/docs/experience-manager-guides/using/release-info/aem-guides-releases-roadmap)を参照してください。

## Cloud Manager {#cloud-manager}

Cloud Manager の月次リリースの完全なリストは、[こちら](/help/implementing/cloud-manager/release-notes/current.md)で確認できます。

## 移行ツール {#migration-tools}

移行ツールのリリースの完全なリストは、[こちら](/help/journey-migration/release-notes/release-notes-migration-tools-current.md)で確認できます

## ユニバーサルエディター {#universal-editor}

ユニバーサルエディターのリリースの完全なリストは、[こちら](/help/release-notes/universal-editor/current.md)で確認できます。

## バリエーションの生成 {#generate-variations}

バリエーションの生成のリリースの完全なリストは、[こちら](/help/generative-ai/release-notes-generate-variations.md)で確認できます。

## Experience Cloud のリリースノート {#experience-cloud}

他の Experience Cloud アプリケーションのリリースについて詳しくは、[こちら](https://experienceleague.adobe.com/ja/docs/release-notes/experience-cloud/current)を参照してください。
