---
title: 現在の [!DNL Adobe Experience Manager] as a Cloud Service リリースノート
description: ' [!DNL Adobe Experience Manager]  as a Cloud Service の最新のリリースノート。'
mini-toc-levels: 1
exl-id: a2d56721-502c-4f4e-9b72-5ca790df75c5
feature: Release Information
role: Admin
source-git-commit: ccca1d88486ff1c1ac2e9272287ce74bc0ac10b1
workflow-type: tm+mt
source-wordcount: '2225'
ht-degree: 28%

---

# [!DNL Adobe Experience Manager] as a Cloud Service の最新のリリースノート {#release-notes}

以下のセクションでは、[!DNL Experience Manager] as a Cloud Service の現在（最新）のバージョンの機能リリースノートの概要について説明します。

>[!NOTE]
>
>ここから、以前のバージョン（2024年や2025年など）のリリースノートに移動できます。
>
>[!DNL Experience Manager] as a Cloud Service の今後の機能のアクティベーションについての詳細は、[Experience Manager リリースロードマップ](https://experienceleague.adobe.com/ja/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap)をご覧ください。

>[!NOTE]
>
>Experience Cloud リリースノートの更新に関するメール通知を毎月受信するには、[アドビ製品アップデートの優先通知](https://www.adobe.com/subscription/priority-product-update.html)を購読してください。

## リリース日 {#release-date}

現在の機能リリース（2026.5.0）である[!DNL Cloud Service]のリリース日は2026年5月28日（PT）です。 [!DNL Adobe Experience Manager]次回の機能リリース（2026.6.0）は2026年6月25日（PT）に予定されています。

## メンテナンスリリースノート {#maintenance}

最新のメンテナンスリリースノートについては、[こちら](/help/release-notes/maintenance/latest.md)をご覧ください。

<!-- 

## Release Video {#release-video}

Have a look at the May 2026 Release Overview video for a summary of the features added in the 2026.5.0 release:

>[!VIDEO](https://video.tv.adobe.com/v/3491491/?captions=jpn&quality=12)

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

[AEM Foundation ベータプログラム &#x200B;](#foundation-early-adopter)を参照してください。

### Cloud Manager（Beta プログラム） {#cloud-manager-beta-programs}

[Cloud Manager ベータ版プログラム &#x200B;](/help/implementing/cloud-manager/release-notes/current.md)を参照してください。

## [!DNL Experience Manager Assets] as a [!DNL Cloud Service] {#assets}

### コンテンツハブの新機能 {#new-features-content-hub}

**AI 検索**

AEM Assets Content Hubには、高度な検索機能であるAI 検索が搭載されました。これにより、キーワードマッチのみに依存することなく、ユーザークエリの背後にある意味と意図を理解できます。 AI 検索は、単語、概念、ユーザーの意図の間の関係を把握することで、より正確なコンテクストに即した検索結果を提供します。 多言語クエリのサポート、誤字やタイプミスの処理、類義語の理解など、正確なメタデータ用語を使用しない場合でも適切なアセットを表示できます。

例えば、`Woman drinking coffee`を検索すると、`Lady`、`Girl`、`Latte`、`Cappuccino`などの関連用語でタグ付けされたアセットを返すこともできます。

管理者は、AI 検索検索または従来のキーワード検索のいずれかを選択して、「設定」メニューを使用して、Content HubのAI 検索を有効または無効にできます。


**カスタム並べ替えオプション**

Content Hubでは、管理者がContent Hub ホームページでカスタムメタデータフィールドをソートオプションとして有効にできるようになりました。 管理者は、デフォルトの並べ替えオプション（サイズ、変更、名前、関連性）に加えて、チャネル、地域、SKU、Campaignなどのビジネス固有のメタデータフィールドを設定して、ユーザーがより効果的に検索結果を整理できるようにすることができます。

**配信APIのアセット検索とダウンロードイベントのサポート**

AEM Assets Delivery APIは、アセット検索とアセットのダウンロードイベントをサポートするようになり、接続されたアプリケーションやエクスペリエンスをまたいでアセットが検出および使用される方法を追跡し、対応できるようになりました。 これらのイベントは、アセットの使用パターンの可視性を向上し、分析とレポートのワークフローをサポートします。また、外部システムや自動化プロセスとの統合を簡素化します。

イベント駆動型のインサイトにより、コンテンツエンゲージメントをより深く理解し、より連続性のあるデジタルアセットワークフローを構築することができます。 詳しくは、[API ドキュメント &#x200B;](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/stable/assets/delivery/#operation/asset_downloaded)を参照してください。

>[!IMPORTANT]
>
>これらの機能は、制限付き可用性機能として利用できます。 [アドビカスタマーサポートケースを作成および送信](https://helpx.adobe.com/jp/enterprise/using/support-for-experience-cloud.html)し、デプロイメントで有効にすることができます。

### OpenAPI機能を備えたDynamic Mediaの新機能 {#new-features-dynamic-media-openapi}

**ビデオスマート切り抜き**

OpenAPI機能を備えたDynamic Mediaは、AEM Assetsのビデオアセットでビデオスマート切り抜きをサポートするようになりました。 動画のスマート切り抜きは、AIを活用した分析により、異なる縦横比やデバイスをまたいで主要な被写体に自動的に焦点を当て、webやモバイルで最適化された視聴体験を提供するのに役立ちます。 管理者が有効にして設定すると、承認済みアセットに対してスマート切り抜きビデオ出力を生成し、再生中に最適なフレームを動的に配信できます。

**ビデオのマルチキャプションおよびマルチオーディオトラックのサポート**

OpenAPI機能を備えたDynamic Mediaは、ビデオアセット用に複数のキャプションと複数のオーディオトラックをサポートするようになりました。 複数の言語に特化したキャプションやオーディオトラックを1つのプライマリビデオに関連付けることで、グローバルなオーディエンスにローカライズされたアクセス可能なビデオエクスペリエンスを提供することができます。 制作者は、統合インターフェイスからこれらのトラックを効率的に管理し、多言語コンテンツ配信を簡素化し、地域のアクセシビリティ要件に対応することができます。

>[!IMPORTANT]
>
>これらの機能は、制限付き可用性機能として利用できます。 [アドビカスタマーサポートケースを作成および送信](https://helpx.adobe.com/jp/enterprise/using/support-for-experience-cloud.html)し、デプロイメントで有効にすることができます。

## [!DNL Experience Manager Forms] as a [!DNL Cloud Service] {#forms}

### AEM Formsの新機能

* Forms Managerでの&#x200B;**バージョン管理のサポート**
Forms Managerでは、アダプティブ Forms（コアコンポーネントおよび基盤コンポーネント） [&#128279;](/help/forms/manage-form-versions-forms-manager.md)、フォームフラグメント、テーマ、XDP テンプレート、バイナリアセットのバージョン管理が サポートされるようになりました。 Formsとドキュメント コンソールから直接、バージョンを作成し、バージョン履歴を表示したり、フォームアセットの以前の状態を復元したりできます。

* **OSGi**&#x200B;でreCAPTCHA クラウド設定を上書き 
ソースファイルに保持するreCAPTCHA Enterprise プロジェクト ID、サイトキー、およびシークレットは、[Cloud Managerを通じてコンテクストに応じた設定の上書きとデプロイを追加した後、各Cloud Service環境で異なる値に解決できます](/help/forms/captcha-adaptive-forms.md#override-recaptcha-osgi)。

* **証明書ベースの認証** 
Microsoft SharePoint リストに送信するアダプティブ Formsで、OAuth URL認証と共に[証明書ベースの認証](/help/forms/connect-forms-to-sharepoint-list.md#certificate-based-authentication)がサポートされるようになりました。 証明書ベースのサインインの場合は、AEMおよびMicrosoft Azureで証明書エイリアスとテナントの詳細を登録します。

* **ルールエディターの機能強化**

   * アダプティブ Forms ルールエディターは、すぐに使える（OOTB）トリガーおよびカスタムイベント [&#128279;](/help/forms/rule-editor-enhancements-use-cases.md#simplified-grammar-for-ootb-and-custom-events)の ディスパッチイベントおよびトリガーイベント時のルールに関する簡略化された文法をサポートするようになりました。そのため、作成者はカスタムトリガーの文法のみに限定されません。
   * コアコンポーネントに基づくアダプティブ Formsのルールに、ANDまたはOR ロジック [&#128279;](/help/forms/rule-editor-enhancements-use-cases.md#combined-when-conditions-with-the-file-attachment-component)を使用する他の条件と一緒に添付ファイル コンポーネントが含まれるようになったため、添付ファイルの状態と他のチェックがすべて意図したとおりに評価された場合にのみ、ルールがアクションを実行します。

## [!DNL Experience Manager] as a [!DNL Cloud Service] の基盤 {#foundation}

### [!DNL Experience Manager]as a [!DNL Cloud Service]基盤の新機能 {#foundation-new}

#### AEM AS A CLOUD SERVICEへのAIを活用したコードの移行 {#aem-ide-cs-migration}

IDE AI ツールを使用して、ベストプラクティスアナライザーレポートの推奨事項に基づいて動作させることで、AEM 6.5以前のバージョンからAEM as a Cloud Service（Java スタック）への移行を高速化できます。

[&#x200B; クラウドローカル開発用のIDE AI ツール &#x200B;](/help/journey-migration/cloud-migration-skill/overview-cloud-migration-skill.md)と、その他[AI ツールとの移行](/help/ai-in-aem/local-development-with-ai-tools.md) （Agent Skillsとローカル MCP サーバー）について詳しく説明します。

>[!VIDEO](https://video.tv.adobe.com/v/3491439/?captions=jpn&quality=12)

#### レプリケーションキューステータスの表示変更 {#replication-queue-status-display}

オーサーUIで、レプリケーションエージェントに、公開ポッドごとに個別のキューではなく、**永続化**&#x200B;と&#x200B;**完全に公開**&#x200B;の2つの統合キューが表示されるようになりました。これにより、公開層の自動スケーリングを反映しながら複雑さが軽減されます。

[&#x200B; レプリケーションキュー](/help/operations/replication.md#replication-queues)の詳細をご覧ください。

![永続および完全に公開されたレプリケーションキュー](/help/operations/assets/replication-queues.png " レプリケーションキュー")

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

#### AEM AI アシスタントを使用してサイレントアワーを管理し、無料期間を更新する（限定提供） {#quiet-hours-ai}

AEM AI アシスタントを通じて、静止時間数および無料期間を直接表示、作成、編集できるようになりました。
主なメリットは、スケジュール設定のエラーが少ないことです。リクエストを行う際に、アシスタントは可能な限り案内し、適用される制限、例えば3期間の上限、期間の間の必須1週間の間隔、スケジュールできない予定されているメンテナンス除外ウィンドウなどをフラグ付けします。そのため、設定に失敗した後に制約を検出する代わりに、ビジネスオーナーとデプロイメントマネージャーは、同じ会話で有効なスケジュールに誘導されます。これにより、重要なビジネスウィンドウを自動メンテナンス更新から保護し、行き違いや設定ミスを減らすことができます。

#### RDEのスナップショット （*パブリック Beta* プログラム） {#rde-snapshot-program}

パブリックベータ版（6月上旬）では、迅速な開発環境（RDE）が、コードとコンテンツの現在の状態のスナップショット [&#128279;](/help/implementing/developing/introduction/rapid-development-environments.md#snapshots)を取得する機能をサポートするようになりました。これは、後で復元できます。 これは、元に戻す必要がある場合のあるコードを同期する場合や、異なる機能の開発を切り替える場合に役立つことがあります。 また、テストの既知の開始点として、可変コンテンツのみを復元することもできます。

6月上旬には、最新のaio プラグインにアップデートすることで、この機能が有効になります。

*RDE スナップショット Betaを使用することにより、まだ開発中であり、テクノロジーの正しい機能やデータの可用性に頼るべきではないことを認めます。 この機能を広範囲にテストしましたが、RDEが不安定になる可能性は少しあります。 この問題が発生した場合、リセットを実行すると、動作状態に戻ります。*


#### AEM Edge Functions （Beta プログラム） {#edge-functions}

[AEM Edge Functions](/help/implementing/developing/introduction/edge-functions.md)を使用すると、JavaScriptをCDN レイヤーで実行し、データ処理をエンドユーザーに近づけることができます。 これにより待ち時間が短縮され、エッジでレスポンシブな動的エクスペリエンスが実現します。

一般的なユースケースを次に示します。

* 位置情報、デバイスタイプまたはユーザー属性に基づくコンテンツのパーソナライズ
* CDN と接触チャネルの間のミドルウェアとして機能させる
* サードパーティの API からの応答をブラウザーに配信する前に再フォーマットする（および複数の API 応答を集計する）
* 様々なバックエンドからステッチされたコンテンツを使用し、サーバーレンダリングされた HTML をエッジで作成および提供

AEM パブリッシュ配信またはEdge Delivery Services プロジェクトのライブ制作サイトのベータ版に参加します。 参加に関心がある場合や、詳細を確認したい場合は、ユースケースの簡単な説明を添えて [aemcs-edgecompute-feedback@adobe.com](mailto:aemcs-edgecompute-feedback@adobe.com)までメールでご連絡ください。

#### Web階層設定パイプラインのトラブルシューティング（Beta プログラム） {#devagent-webtier}

開発エージェントの[&#x200B; パイプラインのトラブルシューティング &#x200B;](/help/ai-in-aem/agents/brand-experience/development/development.md)機能は、開発者がAEM as a Cloud Service デプロイメントの問題を効率的に診断し、解決するのに役立ちます。 フルスタックパイプライン（デプロイメントとコード品質）のサポートに加えて、開発エージェントは、ベータプログラムの一部として、**Web階層設定パイプライン**&#x200B;のトラブルシューティングをサポートするようになりました。

ベータ版へのアクセスをリクエストするには、[aem-devagent@adobe.com](mailto:aem-devagent@adobe.com)にメールを送信してください。 AEMのAgentsへの既存のアクセスが必要です。

#### レプリケーション AIのトラブルシューティング（Beta プログラム） {#replication-ai-troubleshooting-alpha}

AEM オーサーのAI アシスタントやその他のインターフェイスを使用すると、ブロックされたキューなど、レプリケーションに関連する問題をトラブルシューティングできます。 Beta プログラムに参加するには、[aem-devagent@adobe.com](mailto:aem-devagent@adobe.com)にメールを送信して、興味を説明してください。

#### Edge Delivery Services の Edge 認証（Beta プログラム） {#edge-authentication}

Edge 認証を使用すると、Edge Delivery Services ページへのアクセスを、ID プロバイダー（IdP）で認証されたユーザーのみに制限できます。 これを実現するには、OpenID Connect（OIDC）設定の YAML ファイルをデプロイします。

ご興味がある場合は、ユースケースの簡単な説明とご質問を [aemcs-edgecompute-feedback@adobe.com](mailto:aemcs-edgecompute-feedback@adobe.com) までお問い合わせください。

#### ライブトラフィックを受け入れる前にコードをテストするための Canary 実稼動デプロイメント（Beta プログラム） {#canary-beta}

エンドユーザーに公開する前に、内部専用テストトラフィックを使用して実稼動ビルドを検証します。 実稼動環境に出荷し、Canary トラフィックのみをルーティング（特別なヘッダーを使用）し、動作を監視してから、顧客に影響を与えることなく、ライブトラフィックに昇格するか、ロールバックします。

アクセスをリクエストしてフィードバックを共有するには、[aemcs-canary-deployments-beta@adobe.com](mailto:aemcs-canary-deployments-beta@adobe.com) にメールを送信してください。

#### AEM コードの問題の検出とIDE AI エージェントによる自動修正（Alpha プログラム） {#ide-ai-aemcode-issues}

Cursor、Claude Code、Visual Studio、IntelliJなどのツールで[AI支援による開発](/help/ai-in-aem/local-development-with-ai-tools.md)を使用しているJava スタックチームは、さらに進むことができるようになりました。新しいIDE エージェントスキルにより、AEM コードベース内の問題を直接検出して自動修正し、レビューサイクルを短縮し、開発早い段階で問題を検出しました。

この機能はアルファ版です。 プログラムに参加して試し、[aemcs-ai-ide-tools-feedback@adobe.com](mailto:aemcs-ai-ide-tools-feedback@adobe.com)でチームとフィードバックを共有してください。

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
