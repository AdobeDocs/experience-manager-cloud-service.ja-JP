---
title: 現在の [!DNL Adobe Experience Manager] as a Cloud Service リリースノート
description: ' [!DNL Adobe Experience Manager]  as a Cloud Service の最新のリリースノート。'
mini-toc-levels: 1
exl-id: a2d56721-502c-4f4e-9b72-5ca790df75c5
feature: Release Information
role: Admin
source-git-commit: 687be0c3895cbcd8a9530d25f279100f610efe96
workflow-type: tm+mt
source-wordcount: '2054'
ht-degree: 30%

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

現在の機能リリース（2026.4.0）である[!DNL Cloud Service]のリリース日は2026年4月30日です。 [!DNL Adobe Experience Manager]次回の機能リリース（2026.5.0）は2026年5月28日（PT）に予定されています。

## メンテナンスリリースノート {#maintenance}

最新のメンテナンスリリースノートについては、[こちら](/help/release-notes/maintenance/latest.md)をご覧ください。

<!-- 
## Release Video {#release-video}

Have a look at the April 2026 Release Overview video for a summary of the features added in the 2026.4.0 release:

>[!VIDEO](https://video.tv.adobe.com/v/3483060/?quality=12)
-->

## AEM Beta プログラム {#aem-beta-programs}

Adobe Experience Manager（AEM）ベータプログラムは、お客様がプレリリース機能とコードにアクセスし、フィードバックを提供し、AEMの将来を導く方法です。

>[!IMPORTANT]
>
>Beta リリースには欠陥が含まれている場合があり、いかなる保証もなしに「現状のまま」提供されます。 Adobeは、ベータ版のリリースを（Adobe サポートサービスまたはその他の方法により）維持、修正、更新、変更、またはその他の方法でサポートする義務を負いません。 Adobeでは、ベータ版リリースの正しい機能やパフォーマンス、または付随するドキュメントや資料に依存しないように注意することをお勧めします。 ベータ版の機能およびAPIは、予告なく変更される場合があります。 したがって、ベータ版リリースの使用は、完全にお客様の責任で行います。

**参加のメリット**

Adobeが開発している機能をいち早く利用することで、お客様やパートナーはフィードバックを提供し、商品の開発をサポートできます。 また、新機能を一般公開する前に導入する準備にも役立ちます。

**現在のベータ版プログラム**

以下のセクションでは、アクティブなベータ版プログラムの一覧を示します。

### AEMの担当者 {#agents-in-aem}

本番環境、ガバナンス、最適化、検出、および開発に関する強力な新しいAEM エージェンティック機能を確認する場合は、[こちらからアクセスする方法をご確認ください。](/help/ai-in-aem/agents/overview.md)

<!--
### Agents in AEM (Explorer program) {#agents-in-aem-beta-program}

Gain early access to powerful, new AEM agentic capabilities across production, governance, optimization, discovery, and development. Your feedback directly shapes Adobe's roadmap and final features. See [Overview of Agents in AEM](/help/ai-in-aem/agents/overview.md) to learn more.

This program typically lasts 4-6 weeks, but can be tailored to be flexible around your ability to actively participate. 

To opt in to participate in this program, email [aemagentsteam@adobe.com](mailto:aemagentsteam@adobe.com) and include the following details to the extent possible:

* Names and Adobe ID's of team members who will actively use agents.
* List Specific agents that you or your team will want to use. Or simply say "All Agents."

Customers selected for participation will be notified directly by Adobe. Participation is subject to eligibility considerations, including customer licensing and limited program capacity. While not all requests can be accommodated initially, additional customers may be considered in future beta waves.
-->

### AEM財団（Betaプログラム） {#aem-foundation-beta-programs}

[AEM Foundation ベータプログラム ](#foundation-early-adopter)を参照してください。

### Cloud Manager（Beta プログラム） {#cloud-manager-beta-programs}

[Cloud Manager ベータ版プログラム ](/help/implementing/cloud-manager/release-notes/current.md)を参照してください。

## [!DNL Experience Manager Sites] as a [!DNL Cloud Service] {#sites}

### AI翻訳の統合 {#ai-translation-integration}

AEMユーザーは、コンテンツ翻訳に大規模言語モデル（LLM）を活用し、機械翻訳の速度で人間による翻訳品質を実現できるようになりました。 従来のサードパーティ翻訳サービスと同様に、Azure OpenAIはAEMの翻訳プロバイダーとして設定でき、今後のリリースで予定されている追加のLLMもサポートされます。 顧客は、この機能に独自のLLM ライセンスを使用します。 さらに、企業向け翻訳スタイルガイドをAEMにアップロードして、翻訳ルールを抽出することで、ブランドとスタイルの一貫性を確保できます。 詳しくは、[AI翻訳統合の設定](/help/sites-cloud/administering/translation/ai-translation-integration.md)を参照してください。

### コンテンツフラグメントエディター {#cf-editor}

新しいコンテンツフラグメントエディターで、コンテンツフラグメントのJSON表現をプレビューできるようになりました。 これにより、レンダリングとは独立してコンテンツ構造を検証し、AEM タッチ UIの以前のコンテンツフラグメントエディターとのパリティを復元できます。

## [!DNL Experience Manager Assets] as a [!DNL Cloud Service] {#assets}

**Content AdvisorがAdobe WorkfrontおよびAdobe以外のアプリケーションで利用できるようになりました**

Content Advisorは、Adobe WorkfrontおよびAdobe以外（サードパーティ）のアプリケーションで利用できるようになりました。これにより、Adobe ExpressやAEM Sitesだけでなく、インテリジェントなアセット検索やコンテンツの再利用も可能になります。 このリリースでは、AIを活用した検索、コンテキストに応じたレコメンデーション、キャンペーンブリーフに基づく検出、Dynamic Media レンディションへのアクセス、コンテンツフラグメントの検出、フィルター、Adobe Workfrontのワークフローや外部アプリケーションへのアセットメタデータなど、Content Advisorの包括的なエクスペリエンスを提供します。

Adobe AEM Assetsの承認済みアセットを、目的のアプリケーション内で直接検索、評価、再利用できるようになりました。これにより、AdobeとAdobe以外のアプリケーションの両方で、アセットを一貫して利用し、効率を高め、コンテンツ制作を効率化できます。

## [!DNL Experience Manager Forms] as a [!DNL Cloud Service] {#forms}

### AEM Formsの新機能

* **OSGi**でreCAPTCHA クラウド設定を上書き 
ソースファイルに保持するreCAPTCHA Enterprise プロジェクト ID、サイトキー、およびシークレットは、[Cloud Managerを通じてコンテクストに応じた設定の上書きとデプロイを追加した後、各Cloud Service環境で異なる値に解決できます](/help/forms/captcha-adaptive-forms.md#override-recaptcha-osgi)。

* **証明書ベースの認証** 
Microsoft SharePoint リストに送信するアダプティブ Formsで、OAuth URL認証と共に[証明書ベースの認証](/help/forms/connect-forms-to-sharepoint-list.md#certificate-based-authentication)がサポートされるようになりました。 証明書ベースのサインインの場合は、AEMおよびMicrosoft Azureで証明書エイリアスとテナントの詳細を登録します。

* **ルールエディターの機能強化**

   * アダプティブ Forms ルールエディターは、すぐに使える（OOTB）トリガーおよびカスタムイベント ](/help/forms/rule-editor-enhancements-use-cases.md#simplified-grammar-for-ootb-and-custom-events)の[ ディスパッチイベントおよびトリガーイベント時のルールに関する簡略化された文法をサポートするようになりました。そのため、作成者はカスタムトリガーの文法のみに限定されません。
   * コアコンポーネントに基づくアダプティブ Formsのルールに、ANDまたはOR ロジック ](/help/forms/rule-editor-enhancements-use-cases.md#combined-when-conditions-with-the-file-attachment-component)を使用する他の条件と一緒に[添付ファイル コンポーネントが含まれるようになったため、添付ファイルの状態と他のチェックがすべて意図したとおりに評価された場合にのみ、ルールがアクションを実行します。

## [!DNL Experience Manager] as a [!DNL Cloud Service] の基盤 {#foundation}

### [!DNL Experience Manager]as a [!DNL Cloud Service]基盤の新機能 {#foundation-new}

#### AEM JavaおよびDispatcher開発用のIDE AI ツール {#ai-dev}

Java スタックチームでは、Cursor、Claude Code、Visual Studio、IntelliJなどのツールでAI支援による開発を利用して、機能の配信を高速化し、コード品質を向上させています。

IDE ツールは、コーディングエージェントがAEM コードとDispatcher設定を生成およびデバッグするために使用できます。 一例として、次のビデオチュートリアルでは、Agent Skillsを使用したAEM コンポーネントの構築を示します。

AI ツールを使用した[ローカル開発](/help/ai-in-aem/local-development-with-ai-tools.md)の詳細と、ご質問やご意見をお寄せいただいた[aemcs-ai-ide-tools-feedback@adobe.com](mailto:aemcs-ai-ide-tools-feedback@adobe.com)までお気軽にお問い合わせください。


>[!VIDEO](https://video.tv.adobe.com/v/3484978/?learn=on&enablevpops)

#### Experience Governance MCP Server {#gov-mcp-server}

Experience Governance MCP Serverが一般公開（GA）されました。 MCP （モデルコンテキストプロトコル）をサポートするAI開発者ツールやチャットボットと統合されているため、チャットボットやIDEの自然言語プロンプトを使用して、ブランドの整合性とコンプライアンスを保護できます。 コンテンツ（テキスト、画像、ページ）をブランドガバナンスルールと比較して評価し、ブランド設定や利用可能なガバナンスチェックを取得することができます。

[AEM MCP Server](/help/ai-in-aem/mcp-support/using-mcp-with-aem-as-a-cloud-service.md)と[Governance Agent](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/ai-in-aem/agents/governance/overview)の詳細をご覧ください。

#### Claude コネクタ {#aem-claude-connector}

Claude ユーザーは、Anthropicの[Connector Marketplace](https://claude.ai/settings/connectors)を参照して、[Adobe Experience Manager Connector](/help/ai-in-aem/mcp-support/setup-claude.md#aem-claude-connector)をワンクリックでインストールできます。 このMCP サーバーでは、プロンプトによるコンテンツ編集を含む、AEMと対話するツールのセットが増えています。

#### AEM OIDC on パブリッシュの新機能 {#aem-oidc-on-publish-new-features}

* 修正：元のリクエストのクエリパラメーターは、認証後に失われます
* OIDC認証[ ドキュメント ](/help/security/open-id-connect-support-for-aem-as-a-cloud-service-on-publish-tier.md#custom-redirect-after-authentication)の認証後のカスタムリダイレクト

#### Microsoft Graph APIのメールサービスのサポート {#mail-service-graph-api}

AEM メールサービスが、Microsoft Graph APIを使用してMicrosoft® Outlook （Microsoft 365経由）をサポートするようになりました。 これは、メールサービスで既にサポートされているSMTPを許可していない組織に特に役立ちます。 認証はOAuth 2.0経由です。 [設定の方法について説明します](/help/security/oauth2-support-for-mail-service.md#microsoft-graph-api)。

#### CDN ログはSumo Logicに転送できます {#sumo-cdn-logforwarding}

[ ログ転送機能](/help/implementing/developing/introduction/log-forwarding.md#sumologic)で、CDN ログのSumo Logicへの送信がサポートされるようになりました。 以前、Sumo Logicへのログ転送はAEM ログに限定されていました。

### [!DNL Experience Manager] as a [!DNL Cloud Service] Foundationの重要なお知らせ {#foundation-notices}

#### IMS認証リッチエラー {#ims-auth-rich-errors}

IMS統合のトラブルシューティングを支援するために、`imsauth`は&#x200B;*リッチエラー*&#x200B;のサポートを追加しました。

これらのエラーは、HTTP ステータスコードのみを返す代わりに、認証とアクセスをブロックする可能性のある問題の診断と解決に役立つ追加のコンテキストを提供します。

#### Java APIの非推奨化 {#java-api-deprecation}

非推奨のAPIの使用を削除することが重要です。

**4月14**&#x200B;日以降、2026年2月26日をターゲットとするAPIを使用したコードを含むCloud Manager パイプラインは、コードの品質&#x200B;**のステップ中に**&#x200B;削除に失敗します。 非推奨のAPI使用が削除されるまで、デプロイメントはブロックされます。 *これにより、時間の制約を受ける更新プログラムをリリースできなくなり、ビジネス運営に影響を与える可能性があります。*

**2026年6月11日**&#x200B;以降、非推奨のAPI **をまだ使用している環境には、Adobeの重要なリリースアップデート**&#x200B;が適用されず、パフォーマンスと可用性に関するAdobeの標準的な要件は適用されません。 その結果、新しい機能やバグ修正が提供されず、アプリケーションの安定性とアップタイムが悪影響を受ける可能性があり、セキュリティリスクにさらされる可能性があります。

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

### [!DNL Experience Manager] as a [!DNL Cloud Service] Foundation アーリーアダプター機能 {#foundation-early-adopter}

#### AEM Edge Functions （Beta プログラム） {#edge-functions}

[AEM Edge Functions](/help/implementing/developing/introduction/edge-functions.md)を使用すると、JavaScriptをCDN レイヤーで実行し、データ処理をエンドユーザーに近づけることができます。 これにより待ち時間が短縮され、エッジでレスポンシブな動的エクスペリエンスが実現します。

一般的なユースケースを次に示します。

* 位置情報、デバイスタイプまたはユーザー属性に基づくコンテンツのパーソナライズ
* CDN と接触チャネルの間のミドルウェアとして機能させる
* サードパーティの API からの応答をブラウザーに配信する前に再フォーマットする（および複数の API 応答を集計する）
* 様々なバックエンドからステッチされたコンテンツを使用し、サーバーレンダリングされた HTML をエッジで作成および提供
* ChatGPTやClaudeなどのAI アシスタントがカスタムツールにアクセスするためのMCP サーバーの公開

AEM パブリッシュ配信またはライブ実稼動サイトのEdge Delivery Services プロジェクトで利用できる機会の数は限られています。 参加に関心がある場合や、詳細を確認したい場合は、ユースケースの簡単な説明を添えて [aemcs-edgecompute-feedback@adobe.com](mailto:aemcs-edgecompute-feedback@adobe.com)までメールでご連絡ください。

#### Web階層設定パイプラインのトラブルシューティング（Beta プログラム） {#devagent-webtier}

開発エージェントの[ パイプラインのトラブルシューティング ](/help/ai-in-aem/agents/brand-experience/development/development.md)機能は、開発者がAEM as a Cloud Service デプロイメントの問題を効率的に診断し、解決するのに役立ちます。 フルスタックパイプライン（デプロイメントとコード品質）のサポートに加えて、開発エージェントは、ベータプログラムの一部として、**Web階層設定パイプライン**&#x200B;のトラブルシューティングをサポートするようになりました。

ベータ版へのアクセスをリクエストするには、[aem-devagent@adobe.com](mailto:aem-devagent@adobe.com)にメールを送信してください。 AEMのAgentsへの既存のアクセスが必要です。

#### レプリケーション AIのトラブルシューティング（Alpha プログラム） {#replication-ai-troubleshooting-alpha}

AEM オーサーのAI アシスタントやその他のインターフェイスを使用すると、ブロックされたキューなど、レプリケーションに関連する問題をトラブルシューティングできます。 Alpha プログラムに参加するには、[aem-devagent@adobe.com](mailto:aem-devagent@adobe.com)にメールを送信して、興味を説明してください。

#### AEM 6.5からAEM Cloud Serviceへの移行（Beta プログラム）用のIDE AI ツール {#cm-ide-migration}

IDE AI ツールを使用して、[ ベストプラクティスアナライザーレポート ](/help/journey-migration/best-practices-analyzer/overview-best-practices-analyzer.md)の推奨事項に基づいて動作させることで、AEM 6.5からAEM as a Cloud Service（Java スタック）への移行を高速化できます。

詳細と機能へのアクセスをリクエストするには、[aemcs-ai-ide-tools-feedback@adobe.com](mailto:aemcs-ai-ide-tools-feedback@adobe.com)に電子メールを送信してください。

#### Edge Delivery Services の Edge 認証（Beta プログラム） {#edge-authentication}

Edge 認証を使用すると、Edge Delivery Services ページへのアクセスを、ID プロバイダー（IdP）で認証されたユーザーのみに制限できます。 これを実現するには、OpenID Connect（OIDC）設定の YAML ファイルをデプロイします。

ご興味がある場合は、ユースケースの簡単な説明とご質問を [aemcs-edgecompute-feedback@adobe.com](mailto:aemcs-edgecompute-feedback@adobe.com) までお問い合わせください。

#### ライブトラフィックを受け入れる前にコードをテストするための Canary 実稼動デプロイメント（Beta プログラム） {#canary-beta}

エンドユーザーに公開する前に、内部専用テストトラフィックを使用して実稼動ビルドを検証します。 実稼動環境に出荷し、Canary トラフィックのみをルーティング（特別なヘッダーを使用）し、動作を監視してから、顧客に影響を与えることなく、ライブトラフィックに昇格するか、ロールバックします。

アクセスをリクエストしてフィードバックを共有するには、[aemcs-canary-deployments-beta@adobe.com](mailto:aemcs-canary-deployments-beta@adobe.com) にメールを送信してください。

#### RDEのスナップショット（Beta プログラム） {#rde-snapshot-program}

ベータ版では、迅速な開発環境（RDE）で、コードとコンテンツの現在の状態のスナップショット ](/help/implementing/developing/introduction/rapid-development-environments.md#snapshots)を取得する機能[がサポートされるようになりました。これは、後で復元できます。 これは、元に戻す必要がある場合のあるコードを同期する場合や、異なる機能の開発を切り替える場合に役立つことがあります。 また、テストの既知の開始点として、可変コンテンツのみを復元することもできます。

この機能を使用してフィードバックを提供することに関心がある場合は、[aemcs-rde-support@adobe.com](mailto:aemcs-rde-support@adobe.com)にメールを送信してください。

#### アプリケーションパフォーマンスモニタリング（APM）の拡張（Alpha プログラム） {#apm-alpha}

観測性のために、AEM Cloud Service は現在、アドビ提供の [New Relic One](https://experienceleague.adobe.com/ja/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/user-access-new-relic)と顧客管理の [Dynatrace](https://experienceleague.adobe.com/ja/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/dynatrace) をサポートしています。 追加の APM オプションのサポートを検討中ですので、ユースケースと共に、ご希望のベンダーまたはテクノロジーを記載したメールを [aemcs-apm-beta@adobe.com](mailto:aemcs-apm-beta@adobe.com) までお送りください。

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
