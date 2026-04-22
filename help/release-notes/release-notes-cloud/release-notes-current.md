---
title: 現在の [!DNL Adobe Experience Manager] as a Cloud Service リリースノート
description: ' [!DNL Adobe Experience Manager]  as a Cloud Service の最新のリリースノート。'
mini-toc-levels: 1
exl-id: a2d56721-502c-4f4e-9b72-5ca790df75c5
feature: Release Information
role: Admin
source-git-commit: a10a4bf02d5e006e6c151b48606c4e9412193a14
workflow-type: tm+mt
source-wordcount: '2180'
ht-degree: 29%

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

[!DNL Adobe Experience Manager] as a [!DNL Cloud Service] の最新の機能リリース（2026.3.0）のリリース日は、2026年3月26日（PT）です。次回の機能リリース（2026.4.0）は 2026年4月30日（PT）に予定されています。

## メンテナンスリリースノート {#maintenance}

最新のメンテナンスリリースノートについては、[こちら](/help/release-notes/maintenance/latest.md)をご覧ください。

## リリースビデオ {#release-video}

2026.3.0 リリースで追加された機能の概要については、2026年3月のリリースに関する概要ビデオをご覧ください。

>[!VIDEO](https://video.tv.adobe.com/v/3483060/?quality=12)

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

[AEM Foundation ベータプログラム &#x200B;](#foundation-early-adopter)を参照してください。

### Cloud Manager（Beta プログラム） {#cloud-manager-beta-programs}

[Cloud Manager ベータ版プログラム &#x200B;](/help/implementing/cloud-manager/release-notes/current.md)を参照してください。

## [!DNL Experience Manager Sites] as a [!DNL Cloud Service] {#sites}

### コンテンツフラグメントのチェックアウト/イン {#cf-checkout-in}

AEM Touch UIとのパリティを向上させるために、新しいコンテンツフラグメント管理UIを使用して、コンテンツフラグメントをチェックアウトし、再びチェックインできるようになりました。 チェックアウト機能は変更されず、チェックアウトされたコンテンツフラグメントは効果的にロックされ、他のユーザーがコンテンツフラグメントエディターで編集できなくなります。 コンテンツフラグメントを所有しているユーザーと管理者は、フラグメントをチェックアウトして再びチェックインできます。 フラグメントをチェックアウトしても、参照されている子フラグメントまたはアセットには影響しません。

### コンテンツフラグメントがジョブパネルを起動 {#cf-launches-jobs}

コンテンツフラグメントの起動の非同期ジョブを、コンテンツフラグメントの起動の管理UIのプロパティパネルで表示できるようになりました。これにより、ジョブがまだ実行中、完了、または中止されている場合に、ジョブに関する関連詳細情報とともに、ステータスを確認できます。

### コンテンツフラグメントエディターのRTEに更新します {#cf-rte-update}

コンテンツフラグメントエディターのリッチテキストエディター（RTE）が、TinyMCEからTipTapに移行されました。 この変化には、多くの利点があります。

* ユニバーサルエディターとコンテンツフラグメントエディターで、同じRTE テクノロジースタックが使用されるようになりました。
   * つまり、両方のエディターで同じHTMLが生成されるようになりました。
   * 拡張機能を再利用できるようになりました。
   * 両方のエディターを使用して、同じ関数とメソッドを使用できるようになりました（ヘッドレスユースケースの場合）。
   * 最終的な目標は、ひとつの設定を両方のエディターで統合されたエクスペリエンスにつなげることです。
* Spectrum 2 スタイルの新しいルックアンドフィールが追加されました。
* コンテンツフラグメントエディターで、検索と置換、コンテンツアドバイザーの準備など、新しい機能を利用できます。

## [!DNL Experience Manager Assets] as a [!DNL Cloud Service] {#assets}

**AEM SitesのContent Advisor**

Content AdvisorがAEM Sitesで利用可能になり、AEM Assetsからインテリジェントなアセット検出を直接導入できます。 これにより、ユーザーはワークフロー内で最適なアセットを簡単に見つけ、参照、再利用できるようになり、コンテキストを切り替える必要がなくなります。

Content Advisorは、キャンペーンの概要、ベースの提案、コンテキストの提案、Dynamic Mediaのレンディションへのアクセス、詳細なアセットメタデータなどのアセットにインテリジェントな機能を提供します。

近日リリース予定 – Content Advisorで、Adobe WorkfrontおよびAJO B2C アプリケーションがサポートされ、コンテンツフラグメントの検出機能も含まれます

### Dynamic Media の新機能 {#dynamic-media-new-features}

#### Dynamic Media テンプレートエディターの更新 {#dynamic-media-template-editor-updates}

**レイヤー管理の機能強化**

* ドラッグ&amp;ドロップ操作によるレイヤーの並べ替え：レイヤーをドラッグしてレイヤーパネルで直接並べ替えることができるようになりました。これにより、既存の「前に移動」または「後ろに移動」アクションを超えて、レイヤーの重なり順をより迅速かつ直感的に整理できるようになりました。
* コピー、ペースト、複製：キーボードショートカット（Cmd/Ctrl+C、V、D）またはコンテキストメニューを使用したレイヤーのコピー、ペースト、複製を完全にサポートし、マルチレイヤー選択もサポートしています。
* レイヤーのプロパティを分離ボタン：レイヤー設定に簡単に移動するための専用のレイヤープロパティボタンを追加し、レイヤーをダブルクリックして素早くアクセスできるようにしました。

**テキスト書式設定機能**

* 行間の制御：新しい行間スライダーを使用すると、テキストレイヤーの行高さを正確に制御でき、取り消し/やり直しやテンプレートの保存/読み込みなどのエンドツーエンドのサポートを完全に備えています。
* すべての大文字の書式設定：テキストレイヤーは、フォントスタイルツールバーの「すべての大文字」書式設定オプションを、太字、斜体、下線と並べてサポートするようになりました。
* 垂直方向の整列オプション：テキストレイヤーに垂直方向の整列コントロールを追加し、テキストボックス内でより正確なテキストの配置を実現しました。

**サイズとDimension コントロール**

* 縦横比のロック解除：サイズのプロパティを調整する際に、縦横比をロック解除できるようになりました。これにより、幅と高さの調整を個別に行うことができ、より柔軟なレイヤーサイズに変更できます。
* コピーフィット行の設定：テキストのコピーフィット プロパティで`copyfitlines`および`copyfitmaxlines`設定のサポートを追加し、テキストのフィッティング動作をより細かく制御できるようになりました。

**ビジュアルポリッシュ**

* スペクトラム 2 （S2）デザインシステムアイコンが洗練されたタイマーおよびシェイプレイヤーのアイコンを更新しました。

## [!DNL Experience Manager Forms] as a [!DNL Cloud Service] {#forms}

### AEM Forms の早期アクセス機能 {#forms-early-access-features}

**複数選択ドロップダウンのラベルを送信PDFに表示**
アダプティブFormsの複数選択ドロップダウンコンポーネントが、選択した表示ラベルを[生成された送信PDF](/help/forms/generate-document-of-record-core-components.md)でレンダリングするようになり、ユーザーがフォームに表示する内容を正確にドキュメントに反映できるようになりました。

**チェックボックス、ラジオボタン、パネルコンポーネントのアクセシビリティが強化されました**
アダプティブ Forms コアコンポーネントでは、[&#x200B; チェックボックスグループ（v2） &#x200B;](https://experienceleague.adobe.com/en/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/checkbox-group)、[&#x200B; ラジオボタングループ（v2） &#x200B;](https://experienceleague.adobe.com/en/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/radio-button)、[&#x200B; パネルコンポーネント &#x200B;](https://experienceleague.adobe.com/ja/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/panel)に対して、WCAG 2.2に準拠したセマンティックマークアップが導入されています。 これらのコンポーネントは、`<fieldset>`および`<legend>`個のHTML要素を活用して、グループラベルとそのオプションとの間に有意義な関係を確立し、スクリーンリーダーやその他の支援テクノロジーによる正確な解釈を可能にします。

**Forms Managerでのバージョン管理のサポート**
Forms Managerは、アダプティブ Forms（コアコンポーネントおよび基盤コンポーネント） [のバージョン管理、フォームフラグメント、テーマ、XDP テンプレート、バイナリアセットをサポートするようになりました](/help/forms/manage-form-versions-forms-manager.md)。 Formsとドキュメント コンソールから直接、バージョンを作成し、バージョン履歴を表示したり、フォームアセットの以前の状態を復元したりできます。

## [!DNL Experience Manager] as a [!DNL Cloud Service] の基盤 {#foundation}

### [!DNL Experience Manager]as a [!DNL Cloud Service]基盤の新機能 {#foundation-new}

#### シンプルなインデックス管理 {#simplified-index-management}

[簡易インデックス管理](https://oak-indexing.github.io/oakTools/simplified.html)は、完全な定義をコピーしたり、バージョンを手動で管理したりすることなく、1つのJSON ファイルを使用してカスタムインデックスを定義し、すぐに使用できる（OOTB）インデックスをカスタマイズする簡単な方法を提供します。 カスタマイズは最新のOOTB インデックスと結合され、必要に応じて新しいインデックス バージョンが作成されます。

#### Cloud Manager MCP Server {#cm-mcp-server}

>[!VIDEO](https://video.tv.adobe.com/v/3480340/?quality=12)

最新のIDEでは、モデルコンテキストプロトコル（MCP）を使用して、大規模言語モデル（LLM）がMCP サーバーによって公開されたツールを呼び出せるようにします。 開発者は、低レベルのAPI仕様に直接統合するのではなく、自然言語で意図を記述することができます。

Cloud Manager MCP Serverでは、プロンプトを使用して、IDEからCloud Manager APIと直接やり取りできます。 サポートされているシナリオには、パイプラインの実行、環境ステータスの確認などがあります。

[AEM MCP Server](/help/ai-in-aem/mcp-support/using-mcp-with-aem-as-a-cloud-service.md)の詳細をご覧ください。

### [!DNL Experience Manager] as a [!DNL Cloud Service] Foundationの重要なお知らせ {#foundation-notices}

#### Java APIの非推奨化 {#java-api-deprecation}

2026年2月26日（PT）の削除をターゲットとする非推奨（廃止予定）のAPIは、コードで使用しないでください。 デプロイメントブロックを防ぐには、**2026年3月30日**&#x200B;までにAPIの使用を削除してください。 重要な日付：

* **2026年1月26日以降**：アクション センターの通知メールは、これらのAPIの使用を削除するためのリマインダーとして送信されます。
* **2026年2月26日**：これらのAPIを使用するコードを含むCloud Manager パイプラインは、**コード品質**&#x200B;の手順で&#x200B;**一時停止**&#x200B;します。 デプロイメントマネージャー、プロジェクトマネージャー、ビジネスオーナーは、問題を上書きして、パイプラインを続行できます。 *コードの変更を検証およびリリースする機能が遅くなる可能性があります。*
* **2026年3月30日**：これらのAPIを使用するコードを含むCloud Manager パイプラインは、**コード品質**&#x200B;の手順で&#x200B;**失敗**&#x200B;します。 非推奨のAPI使用が削除されるまで、デプロイメントはブロックされます。 *これにより、時間の制約を受ける更新プログラムをリリースできなくなり、ビジネス運営に影響を与える可能性があります。*
* **2026年5月4日**：まだ非推奨のAPI **を使用している環境では、Adobeの重要なリリースアップデート**&#x200B;を受け取ることができず、パフォーマンスと可用性に関するAdobeの標準的なコミットメントの対象にはなりません。 その結果、新しい機能やバグ修正が提供されず、アプリケーションの安定性とアップタイムが悪影響を受ける可能性があり、セキュリティリスクにさらされる可能性があります。

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

#### AEM JavaおよびDispatcher開発向けIDE AI ツール（パブリック Beta プログラム） {#ai-dev-beta}

Java スタックチームでは、Cursor、Claude Code、Visual Studio、IntelliJなどのツールでAI支援による開発を利用して、機能の配信を高速化し、コード品質を向上させています。

パブリックベータ版に参加して（サインアップは必要ありません）、コーディングエージェントがAEM コードとDispatcher設定を生成およびデバッグするために使用できるIDE ツールを試してください。

詳しくは、[AI ツールを使用したローカル開発](/help/ai-in-aem/local-development-with-ai-tools.md) ベータ版のドキュメントおよび質問やフィードバックを含むメール [aemcs-ai-ide-tools-feedback@adobe.com](mailto:aemcs-ai-ide-tools-feedback@adobe.com)を参照してください。

#### AEM Edge Functions （Beta プログラム） {#edge-functions}

[AEM Edge Functions](/help/implementing/developing/introduction/edge-functions.md)を使用すると、JavaScriptをCDN レイヤーで実行し、データ処理をエンドユーザーに近づけることができます。 これにより待ち時間が短縮され、エッジでレスポンシブな動的エクスペリエンスが実現します。

一般的なユースケースを次に示します。

* 位置情報、デバイスタイプまたはユーザー属性に基づくコンテンツのパーソナライズ
* CDN と接触チャネルの間のミドルウェアとして機能させる
* サードパーティの API からの応答をブラウザーに配信する前に再フォーマットする（および複数の API 応答を集計する）
* 様々なバックエンドからステッチされたコンテンツを使用し、サーバーレンダリングされた HTML をエッジで作成および提供
* ChatGPT や Claude などの LLM がカスタムツールにアクセスできるように MCP サーバーを公開する

AEM パブリッシュ配信またはライブ実稼動サイトのEdge Delivery Services プロジェクトで利用できる機会の数は限られています。 参加に関心がある場合や、詳細を確認したい場合は、ユースケースの簡単な説明を添えて [aemcs-edgecompute-feedback@adobe.com](mailto:aemcs-edgecompute-feedback@adobe.com)までメールでご連絡ください。

#### Development Agent （Beta プログラム）を使用したWeb Tier Config Pipelineのトラブルシューティング {#devagent-webtier}

開発エージェントの[&#x200B; パイプラインのトラブルシューティング &#x200B;](/help/ai-in-aem/agents/brand-experience/development/development.md)機能は、開発者がAEM as a Cloud Service デプロイメントの問題を効率的に診断し、解決するのに役立ちます。 フルスタックパイプライン（デプロイメントとコード品質）のサポートに加えて、開発エージェントは、ベータプログラムの一部として、**Web階層設定パイプライン**&#x200B;のトラブルシューティングをサポートするようになりました。

ベータ版へのアクセスをリクエストするには、[aem-devagent@adobe.com](mailto:aem-devagent@adobe.com)にメールを送信してください。 AEMのAgentsへの既存のアクセスが必要です。

#### AEM 6.5からAEM Cloud Serviceへの移行（Alpha プログラム）用のIDE AI ツール {#cm-ide-migration}

IDE AI ツールを使用して、[&#x200B; ベストプラクティスアナライザーレポート &#x200B;](/help/journey-migration/best-practices-analyzer/overview-best-practices-analyzer.md)の推奨事項に基づいて動作させることで、AEM 6.5からAEM as a Cloud Service（Java スタック）への移行を高速化できます。

詳細については、[aemcs-ai-ide-tools-feedback@adobe.com](mailto:aemcs-ai-ide-tools-feedback@adobe.com)に電子メールを送信してください。

#### Edge Delivery Services の Edge 認証（Beta プログラム） {#edge-authentication}

Edge 認証を使用すると、Edge Delivery Services ページへのアクセスを、ID プロバイダー（IdP）で認証されたユーザーのみに制限できます。これを実現するには、OpenID Connect（OIDC）設定の YAML ファイルをデプロイします。

ご興味がある場合は、ユースケースの簡単な説明とご質問を [aemcs-edgecompute-feedback@adobe.com](mailto:aemcs-edgecompute-feedback@adobe.com) までお問い合わせください。

#### ライブトラフィックを受け入れる前にコードをテストするための Canary 実稼動デプロイメント（Beta プログラム） {#canary-beta}

エンドユーザーに公開する前に、内部専用テストトラフィックを使用して実稼動ビルドを検証します。実稼動環境に出荷し、Canary トラフィックのみをルーティング（特別なヘッダーを使用）し、動作を監視してから、顧客に影響を与えることなく、ライブトラフィックに昇格するか、ロールバックします。

コードリリースを実稼動環境にデプロイしますが、ライブトラフィックを受け入れるかロールバックするかを決定する前に、内部テストトラフィックのみに制限します。

アクセスをリクエストしてフィードバックを共有するには、[aemcs-canary-deployments-beta@adobe.com](mailto:aemcs-canary-deployments-beta@adobe.com) にメールを送信してください。

#### RDEのスナップショット（Beta プログラム） {#rde-snapshot-program}

ベータ版では、迅速な開発環境（RDE）が、コードとコンテンツの現在の状態のスナップショットを取得する機能をサポートするようになりました。これは、後で復元できます。 これは、元に戻す必要がある場合のあるコードを同期する場合や、異なる機能の開発を切り替える場合に役立つことがあります。 また、テストの既知の開始点として、可変コンテンツのみを復元することもできます。

この機能を使用してフィードバックを提供することに関心がある場合は、[aemcs-rde-support@adobe.com](mailto:aemcs-rde-support@adobe.com)にメールを送信してください。

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
