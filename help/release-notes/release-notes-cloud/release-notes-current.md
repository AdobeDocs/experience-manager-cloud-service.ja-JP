---
title: ' [!DNL Adobe Experience Manager] as a Cloud Serviceの最新のリリースノート'
description: ' [!DNL Adobe Experience Manager]  as a Cloud Service の最新のリリースノート。'
mini-toc-levels: 1
exl-id: a2d56721-502c-4f4e-9b72-5ca790df75c5
feature: Release Information
role: Admin
source-git-commit: 1c5cbed1ea9e8beda14ed3c66f14a446941cd9cf
workflow-type: tm+mt
source-wordcount: '2011'
ht-degree: 39%

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

[!DNL Adobe Experience Manager] as a [!DNL Cloud Service] の最新の機能リリース（2026.1.0）のリリース日は、2026年1月29日（PT）です。次回の機能リリース（2026.2.0）は、2026年2月26日（PT）に予定されています。

## メンテナンスリリースノート {#maintenance}

最新のメンテナンスリリースノートについては、[こちら](/help/release-notes/maintenance/latest.md)をご覧ください。

<!-- 

## Release Video {#release-video}

Have a look at the July 2025 Release Overview video for a summary of the features added in the 2025.7.0 release:

>[!VIDEO](https://video.tv.adobe.com/v/3440920?quality=12)

-->

## AEM Beta プログラム {#aem-beta-programs}

Adobe Experience Manager（AEM）ベータプログラムを使用すると、プレリリース機能やコードにアクセスし、フィードバックを提供し、AEMの将来を導くことができます。

>[!IMPORTANT]
>
>Beta リリースには不具合が含まれている場合があり、いかなる保証もなく「現状のまま」提供されます。 Adobeは、ベータ版リリースの保守、修正、更新、変更、またはその他のサポート（Adobe サポートサービスを通じてまたはその他の方法で）を行う義務を負いません。 Adobeでは、お客様に対して、ベータ版リリースが正しく機能するか、パフォーマンスが向上するか、あるいはこれらに付随するドキュメントや資料を使用しないよう、注意して助言しています。 ベータ版の機能と API は、予告なく変更される場合があります。 したがって、ベータ版リリースの使用は、完全にお客様自身の責任で行います。

**参加のメリット**
Adobeが開発中の機能に早期にアクセスすることで、お客様およびパートナーはフィードバックを提供し、製品開発を具体化できます。 また、GA 前に新しい機能を導入する準備をするのに役立ちます。

**現在のベータ版プログラム**
次の節では、アクティブなベータ版プログラムとエクスプローラープログラムを示します。

### AEMのエージェント（エクスプローラープログラム） {#agents-in-aem-beta-program}

実稼働、ガバナンス、最適化、検出、開発全体にわたる、強力な新しいAEMエージェンティック機能に早期にアクセスできます。 お客様からのフィードバックによって、Adobeのロードマップと最終的な機能が直接形作られます。 詳しくは、[AEMでのエージェントの概要 &#x200B;](/help/ai-in-aem/agents/overview.md) を参照してください。

このプログラムは通常 4～6 週間続きますが、積極的に参加する能力に合わせて柔軟に調整できます。

このプログラムへの参加をオプトインするには、[aemagentsteam@adobe.comに電子メールを送信し &#x200B;](mailto:aemagentsteam@adobe.com) 可能な限り次の詳細を含めてください。

* エージェントを積極的に使用するチームメンバーの名前とAdobe ID。
* 自分または自分のチームが使用する特定のエージェントのリスト。 または、単に「すべてのエージェント」と言います。

参加者として選択されたお客様には、Adobeから直接通知が届きます。 参加には、顧客のライセンスや限定的なプログラム処理能力など、実施要件に関する考慮事項が必要です。 最初にすべてのリクエストに対応できるわけではありませんが、今後のベータ版では、追加のお客様の対応が検討される可能性があります。

### AEM財団（Beta プログラム） {#aem-foundation-beta-programs}

[AEM Foundation ベータプログラム &#x200B;](#foundation-early-adopter) を参照してください。

### Cloud Manager（Beta プログラム） {#cloud-manager-beta-programs}

[Cloud Manager ベータプログラム &#x200B;](/help/implementing/cloud-manager/release-notes/current.md) を参照してください。

## [!DNL Experience Manager Sites] as a [!DNL Cloud Service] {#sites}

### Content MCP サーバー {#content-MCP}

AEM Cloud Service に **コンテンツ MCP サーバー** が含まれるようになり、AI を活用したエクスペリエンスが MCP 互換ツールを通じてAEM コンテンツで動作するための標準化された方法が提供されます。

チャットアプリやエージェントプラットフォームで作業する開発者やパワーユーザーは、AEMをカスタムコパイロットや自動化に接続できるので、コンテンツ作業はエンドツーエンドのビジネスワークフローの一部になります。

AEMには、次の 2 つのサーバーがあります。

1. **読み取り専用 Content MCP Server** - コンテンツを安全に取得します。
1. **コンテンツ MCP サーバーの読み取り/書き込み** - コンテンツを変更します。

これらの MCP サーバーには、**Pages**、**Content Fragments**、および **Assets** を操作するためのツールが含まれており、**ChatGPT**、**Claude**、**Cursor**、**Microsoft Copilot Studio** の MCP クライアントから使用できます。

詳しくは、[AEM Cloud Service での MCP の使用 &#x200B;](/help/ai-in-aem/mcp-support/using-mcp-with-aem-as-a-cloud-service.md) を参照してください。 ご質問やご意見については、[aemcs-mcp-feedback@adobe.com](mailto:aemcs-mcp-feedback@adobe.com) までお問い合わせください。

## [!DNL Experience Manager Assets] as a [!DNL Cloud Service] {#assets}

**AI 検索**

AI 検索は、ユーザークエリの背後にある意味と意図を理解することで、従来のキーワードマッチングを超えた、インテリジェントなコンテキスト認識型検索エクスペリエンスを提供します。 AI と機械学習を活用することで、クエリの言葉遣いが異なる場合、スペルミスが含まれている場合、同義語を使用する場合、異なる言語で送信された場合でも、より正確な結果が得られ、ユーザーが関連性の高いコンテンツを少ない労力でより迅速に見つけることができます。

詳しくは、「[Assets ビュー &#x200B;](/help/assets/search-assets-view.md#ai-search)」および「&lbrace; 管理者ビュー [&#x200B; のAI 検索](/help/assets/search-assets.md#ai-search) を参照してください。

**デスクトップアプリケーション 3.0.1 リリース**

[&#x200B; デスクトップアプリ 3.0.1 （2025 年 12 月 20 日（PT）） &#x200B;](https://experienceleague.adobe.com/ja/docs/experience-manager-desktop-app/using/release-notes) 主要なワークフロー全体で信頼性、パフォーマンス、安定性を向上させます。 このリリースでは、AEM オーサーとの同期の問題を修正することで一貫したフォルダー名が保証され、アクティブな転送中のアプリの中断のない使用が可能になり、非同期処理による UI の応答性が向上し、ページネーションを使用した大きなファイル転送が最適化され、大きなフォルダーのアップロードおよびダウンロード中のオーサーサーバーの再起動やクラッシュなどの安定性の問題が解決されます。

**Adobe Asset Link CEP 2026.01.0 リリース**

[Adobe Asset Link CEP 2026.01.0](https://helpx.adobe.com/jp/enterprise/using/adobe-asset-link.html)InDesignに、同じAEM フォルダーから他の欠落しているアセットを自動的に再リンクする新しい「欠落しているリンクを再リンク」オプションが導入されました。 この機能は、ファイル名に基づいてアセットを照合し、壊れたリンクを復元する際の手動での作業を大幅に削減します。


## [!DNL Experience Manager Forms] as a [!DNL Cloud Service] {#forms}

**アダプティブForms（基盤コンポーネント）の脚注プレースホルダーの機能強化**

* [&#x200B; 改行による複数行サポート &#x200B;](/help/forms/footnotes-richtextsupport.md) が追加され、脚注コンテンツをより明確かつ表現力豊かに表示できるようになりました。
* 脚注は、関連するパネルの表示に関係なく、脚注プレースホルダー内で永続的に表示されるようになり、重要な情報に一貫してアクセスできるようになりました。
  ![脚注の説明](/help/forms/assets/footnote-description.png){height=50%}

### AEM Forms の新しい早期アクセス機能 {#forms-new-early-access-features}

**JSON 配列から値を取得**

API 呼び出しを介して受信した [JSON 配列から値を抽出 &#x200B;](/help/forms/invoke-service-enhancements-rule-editor.md#retrieve-property-values-from-a-json-array) し、アダプティブフォームフィールドに直接バインドするカスタム関数機能を拡張しました。 最小限の手動でのデータマッピングで、ビジネスロジックとルールを開発できるようになりました。

**パブリッシュインスタンスで関連付け UI を実行する**

パブリッシュインスタンスで [UI を関連付け &#x200B;](/help/forms/interactive-communication/associate-ui-in-interactive-communication-editor.md) を直接実行できるようになりました。 これにより、エージェントは関連付け UI にアクセスして、顧客に合わせてコミュニケーションを簡単にパーソナライズできます。

<!--
**Forms Optimization opportunities**

Forms Optimization uses AI to analyze your forms and suggest improvements for better performance. It highlights forms with low engagement, flags accessibility issues, and generates AI-powered variations to help increase conversion rates and compliance with WCAG standards.

>[!VIDEO](https://video.tv.adobe.com/v/3469472/) 

Key optimization opportunities include:

* Increasing visibility for forms with low views
* Improving completion rates for forms with low conversions
* Addressing accessibility compliance issues
* Streamlining navigation to enhance user experience

With Forms Optimization, you get automated, data-driven recommendations and variations, making it easier to boost engagement and ensure your forms are effective and inclusive. 
-->

## [!DNL Experience Manager] as a [!DNL Cloud Service] の基盤 {#foundation}

### [!DNL Experience Manager] as a [!DNL Cloud Service] Foundation に関する重要な注意事項 {#foundation-notices}

#### Java API の非推奨化 {#java-api-deprecation}

2026 年 2 月 26 日（PT）の削除をターゲットにした非推奨の API は、コードでは使用されなくなります。 デプロイメントブロックを防ぐには、2026 年 3 月 26 日（PT）より前に、API の使用を削除します。 重要な日付：

* **2026 年 1 月 26 日以降**：これらの API の使用を削除するためのリマインダーとして、アクションセンターの通知メールが **環境ごとに毎週** 送信されます。
* **2026 年 2 月 26 日（PT）**：これらの API を使用したコードを含むCloud Manager パイプラインは、**コード品質** ステップ中に **一時停止** されます。 デプロイメントマネージャー、プロジェクトマネージャーまたはビジネスオーナーは、問題をオーバーライドしてパイプラインを続行できます。
* **2026 年 3 月 26 日**：これらの API を使用するコードを含んだCloud Manager パイプラインは、新しいコードの **コード品質** ステップ、**デプロイメントのブロック** 中に使用が削除されるまで **失敗** します。
* **2026 年 4 月 30 日**：これらの API をまだ使用している環境は、**Adobe リリースの重要なアップデートを受け取れなくなる** 可能性があります。

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
* `org.bson`
* `org.apache.jackrabbit.oak.plugins.blob`
* `org.apache.jackrabbit.oak.plugins.memory`

+++

<!--
OSGi properties:

* `org.apache.sling.commons.log.LogManager` (all properties)
* `org.apache.sling.commons.log.LogManager.factory.config` (`org.apache.sling.commons.log.file`, `org.apache.sling.commons.log.pattern`)
* 

-->

#### Java 11 ランタイムの非推奨（廃止予定） {#java11-runtime-deprecation}

Adobeは 2025 年 10 月 14 日に **ステージング** 環境と **実稼動** 環境を高性能の **Java 21 ランタイム** にアップグレードしました。 **2 月 9 日（PT）** から（2 月 11 日（PT）まで段階的にロールアウト）、AEM Cloud Service SDKもクラウド環境も Java 11 ランタイムでは動作しません。

>[!NOTE]
>
> 最新のパフォーマンス最適化と言語強化を活用するには、Java 17 または Java 21 （推奨）を使用してビルドすることをお勧めします。 Java 8 および Java 11 を使用したビルドは、現時点ではサポートされていますが、今後のリリースで非推奨（廃止予定）になります。 廃止に先立ち、別途お知らせいたします。 *この記事* の [&#x200B; ビルド時間要件 &#x200B;](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/build-environment-details.md#runtime-requirements) の節を参照してください。
>

#### AEM Java ログ設定ポリシーの適用 {#logconfig-policy}

すべてのお客様の環境で信頼性の高い監視を行うには、AEMの Java ログが標準形式に従う必要があります。 ログ形式、出力ファイル、デフォルトログレベルの変更といったカスタムログ設定は、サポートされなくなりました。 ログはデフォルトファイルにダイレクトされ続け、AEM 製品コードのデフォルトログレベルは保持される必要があります。 詳しくは、[ログに関する記事](/help/implementing/developing/introduction/logging.md#configuration-loggers)を参照してください。

サポートされていないカスタムログの上書き *無視されるようになりました*。 ほとんどのお客様には影響はありませんでした。また、Adobeからは、現在の設定が影響を受ける可能性があるお客様に連絡しています。

カスタムログ動作に依存するダウンストリームプロセスを確認し、更新してください。 例：

* ログ転送システムでカスタムログ形式が想定されている場合は、取り込みルールを調整する必要がある可能性があります。
* 以前にログレベルを変更してログの冗長性を削減したことがある場合は、デフォルトレベルに戻すとログのボリュームが増える可能性があることに注意してください。

### [!DNL Experience Manager] as a [!DNL Cloud Service] 基盤の早期導入者の機能 {#foundation-early-adopter}

#### 自動メンテナンスアップデートの一時停止 {#pause-updates}

運用開始日、ライブイベント、ピーク時の売上といった瞬間を逃すことはできません。[&#x200B; 新しいセルフサービス機能 &#x200B;](/help/implementing/deploying/quiet-hours-update-free-periods.md)により、重要な場合に自動メンテナンスアップデートを停止し、チームが集中できるようにします。

* 静かな時間：毎日設定された時間に自動メンテナンスをブロックします。勤務時間、夜間の実行や朝の切り替え時などに最適です。
* 更新不要の期間：自動メンテナンスを 1 週間ブロックします。ローンチ、プロモーションまたは年次フリーズに使用します。

>[!NOTE]
>
>9月25日（PT）に限定提供機能として提供を開始します。
>プログラムでアクティブ化するには、[aemcs-update-free@adobe.com](mailto:aemcs-update-free@adobe.com) にメールを送信してください。
>

#### AEM Edge関数（Beta プログラム） {#edge-functions}

AEM Edge関数（以前のリリースノートでは *Edge Computing* と呼ばれていました）を使用すると、CDN レイヤーでJavaScriptを実行し、データ処理をエンドユーザーに近づけることができます。 これにより待ち時間が短縮され、エッジでレスポンシブな動的エクスペリエンスが実現します。

一般的なユースケースを次に示します。

* 位置情報、デバイスタイプまたはユーザー属性に基づくコンテンツのパーソナライズ
* CDN と接触チャネルの間のミドルウェアとして機能させる
* サードパーティの API からの応答をブラウザーに配信する前に再フォーマットする（および複数の API 応答を集計する）
* 様々なバックエンドからステッチされたコンテンツを使用し、サーバーレンダリングされた HTML をエッジで作成および提供
* ChatGPT や Claude などの LLM がカスタムツールにアクセスできるように MCP サーバーを公開する

AEM パブリッシュ配信またはライブ実稼動サイトのEdge Delivery Services プロジェクトで利用できる機会の数は限られています。 参加に関心がある場合や、詳細を確認したい場合は、ユースケースの簡単な説明を添えて [aemcs-edgecompute-feedback@adobe.com](mailto:aemcs-edgecompute-feedback@adobe.com)までメールでご連絡ください。

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

#### AEM Java およびDispatcher開発用 IDE の AI ツール（Beta プログラム） {#ai-dev-beta}

Java スタックチームは、Cursor、Cloud Code、Visual Studio、IntelliJ などのツールで AI を利用した開発を使用して、機能の配信を高速化し、コード品質を向上させています。 ベータ版に参加して、次のことを行います。

* Adobeでサポートされる将来の AI 機能の形成に役立つ、実際のエクスペリエンスを共有する
* AI エージェントでAEM コードおよび Dispatcher 設定の生成とデバッグに使用できる IDE ツールを試す

詳しくは、[aemcs-java-adopter@adobe.com](mailto:aemcs-java-adopter@adobe.com) にメールを送信してください。

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
