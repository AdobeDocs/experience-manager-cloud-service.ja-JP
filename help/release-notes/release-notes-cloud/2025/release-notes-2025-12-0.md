---
title: ' [!DNL Adobe Experience Manager]  as a Cloud Service 2025.12.0 リリースのリリースノート。'
description: ' [!DNL Adobe Experience Manager]  as a Cloud Service 2025.12.0 リリースのリリースノート。'
feature: Release Information
role: Admin
source-git-commit: 9e81e0f3ed4b3e4ac02655cf4203191c61007b1d
workflow-type: tm+mt
source-wordcount: '1951'
ht-degree: 48%

---

# [!DNL Adobe Experience Manager] as a Cloud Service の 2025.12.0 リリースノート {#release-notes}

以下の節では、[!DNL Experience Manager] as a Cloud Service の 2025.12.0 バージョンの機能リリースノートの概要について説明します。

>[!NOTE]
>
>ここから、以前のバージョン（例えば、2023年、2024年）のリリースノートに移動できます。
>
>[!DNL Experience Manager] as a Cloud Service の今後の機能のアクティベーションについての詳細は、[Experience Manager リリースロードマップ](https://experienceleague.adobe.com/ja/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap)をご覧ください。

>[!NOTE]
>
>Experience Cloud リリースノートの更新に関するメール通知を毎月受信するには、[アドビ製品アップデートの優先通知](https://www.adobe.com/subscription/priority-product-update.html)を購読してください。

## リリース日 {#release-date}

[!DNL Adobe Experience Manager] as a [!DNL Cloud Service] の最新の機能リリース（2025.12.0）の公開日は 2025年12月11日（PT）です。次回の機能リリース（2026.1.0）は 2026年1月29日（PT）に予定されています。

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
次の節では、アクティブなベータプログラムを示します。

### AEMのエージェント（Beta プログラム） {#agents-in-aem-beta-program}

実稼働、ガバナンス、最適化、検出、開発全体にわたる、強力な新しいAEMエージェンティック機能に早期にアクセスできます。 お客様からのフィードバックによって、Adobeのロードマップと最終的な機能が直接形作られます。 詳しくは、[AEMでのエージェントの概要 ](/help/ai-in-aem/agents/overview.md) を参照してください。

このプログラムは通常 4～6 週間続きますが、積極的に参加する能力に合わせて柔軟に調整できます。

このプログラムへの参加をオプトインするには、[aemagentsteam@adobe.comに電子メールを送信し ](mailto:aemagentsteam@adobe.com) 可能な限り次の詳細を含めてください。

* エージェントを積極的に使用するチームメンバーの名前とAdobe ID。
* 自分または自分のチームが使用する特定のエージェントのリスト。 または、単に「すべてのエージェント」と言います。

### AEM財団（Beta プログラム） {#aem-foundation-beta-programs}

[AEM Foundation ベータプログラム ](#foundation-early-adopter) を参照してください。

### Cloud Manager（Beta プログラム） {#cloud-manager-beta-programs}

[Cloud Manager ベータプログラム ](/help/implementing/cloud-manager/release-notes/current.md) を参照してください。


## [!DNL Experience Manager Assets] as a [!DNL Cloud Service] {#assets}

**AEM Assetsと統合するための Figma プラグインの新しいバージョンが利用可能です**

* AEM リポジトリから Figma ドキュメントにアセットを読み込む際の、ビデオファイル（MP4、MOV、WebM）、アニメーションファイル（GIF）、ベクターファイル（SVG）のサポート。

* AEM リポジトリ内のアセットと比較して、Figma ドキュメントで使用されているアセットに更新があるかどうかの確認、および更新がある場合のアセットの最新バージョンの取得のサポート。

* PNG （scale）およびJPG（image scale and quality）ファイル形式の書き出し時の書き出し設定のサポート。

  ![Figma プラグイン ](/help/assets/assets/figma-v2-plugin.png)

**アップロードされたアセットのマルウェア検出**

AEM Assetsには、アップロードされたファイルの自動マルウェアスキャンが含まれるようになりました。これにより、リポジトリを脅威から保護するために、DAM に入る前に疑わしいアセットが確実に隔離されます。 管理者は、スキャン設定と強制隔離の保持ポリシーを設定して、セキュリティ制御を効率化できます。

**AI が生成したメタデータ – 実施要件の更新**

AEM Assetsで AI によって生成されたメタデータを有効にするために、GenAI Rider に署名する必要がなくなりました。 この機能は、GenAI Rider に署名したお客様と、まだ検証されていないお客様の両方が利用できるようになりました。 GenAI の使用を明示的にオプトアウトした顧客は、引き続き機能を無効にできます。 環境レベルで機能イネーブルメントを管理するには、[AI 生成メタデータの無効化 ](/help/assets/enhance-content-discovery-with-ai-generated-metadata.md#disable-ai-generated-metadata) を参照してください。 この変更は、リリースバージョン 23482 以降のお客様に対して行われます。

## [!DNL Experience Manager Forms] as a [!DNL Cloud Service] {#forms}

<!-- ### Pre-Release features in AEM Forms 

**Rule Editor Enhancements**

The Rule Editor now supports enhanced navigation and allows use of function and mathematical expressions in input parameters.

**Enhanced Navigation with Event Payload Support**
 
The `Navigate To` action in the Invoke Service handlers now supports `EVENT_PAYLOAD`, enabling form authors to configure follow-up actions based on event responses. This enhancement offers greater flexibility in designing post-submission workflows, ensuring smoother transitions and more personalized user experiences. For more information, see [Enhanced Navigation with Event Payload Support](/help/forms/invoke-service-enhancements-rule-editor.md#use-case-5-use-event-payload-in-navigate-to-action-in-invoke-service).

**Function and Mathematical Expression Support in Input Parameters**
 
Input parameters now support both function calls and mathematical expressions, enabling form authors to pass dynamically computed values directly. This enhancement streamlines rule configurations, eliminates the need for extra fields, and makes forms more adaptable to complex logic and calculation-driven scenarios. For more information, see [Function and Mathematical Expression Support in Input Parameters](/help/forms/rule-editor-core-components-user-interface.md#function-and-mathematical-expression-support-in-input-parameters). -->

### AEM Forms の新しい早期アクセス機能 {#forms-new-early-access-features}

AEM Forms 早期アクセスプログラムでは、最先端の革新機能にいち早くアクセスできるだけでなく、その開発に意見を反映させるユニークな機会も提供されます。

これらのリリースノートでは、現在のリリースで提供されるイノベーションのリストを示します。早期アクセスプログラムで利用可能なイノベーションの完全なリストについて詳しくは、[AEM Forms 早期アクセスプログラムのドキュメント](/help/forms/early-access-ea-features.md)を参照してください。

#### インタラクティブ通信の機能強化

##### テンプレートのロック

テンプレート内のコンテンツおよびレイアウト要素をロックして、ブランドの整合性を維持し、不正な変更を防ぎます。 これにより、すべての通信でデザインの一貫性が確保されます。

##### コンテンツオーバーフローのサポート

フローレイアウト用の「コンテンツ内の改ページを許可」オプションの導入。 この機能強化により、複数ページの編集がスムーズになり、複雑なドキュメントのテキスト管理が向上します。

##### XDP ファイル編集

インタラクティブ通信エディターで、フラグメント統合を含む XDP の編集がサポートされるようになりました。 Microsoft Windows デスクトップでのみ動作するForms Designerの代わりに、ブラウザーで XDP ファイルを編集できるようになりました。

##### 動的ページ番号

複数ページのドキュメントにわたって明確で一貫性のあるページネーションを行うために、マスターページに「Page # of ##」を自動的に表示します。

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

### [!DNL Experience Manager] as a [!DNL Cloud Service] Foundation の新機能 {#foundation-new}

#### 今後の Java API の非推奨（廃止予定） {#java-api-deprecation}

一部の非推奨（廃止予定）API は、8月31日（PT）の削除としてマークされたので、参照できなくなります。コードに非推奨の API の使用が検出された場合は、アクションセンターから通知が届きます。1.29 日以降は、Cloud Manager ビルド中に通知が表示され、使用を削除することが重要になります。 詳しくは、[非推奨（廃止予定）に関する記事](/help/release-notes/deprecated-removed-features.md#aem-apis)を参照してください。便宜上、これらの API を次に示します。

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

Adobeは 2025 年 10 月 14 日に **ステージング** 環境と **実稼動** 環境を高性能の **Java 21 ランタイム** にアップグレードしました。 **2 月 9 日** 以降、AEM Cloud Service SDKおよびすべてのクラウド環境は、Java 11 ランタイムでは動作しません。

>[!NOTE]
>
> 最新のパフォーマンス最適化と言語強化を活用するには、Java 17 または Java 21 （推奨）を使用してビルドすることをお勧めします。 Java 8 および Java 11 を使用したビルドは、現時点ではサポートされていますが、今後のリリースで非推奨（廃止予定）になります。 廃止に先立ち、別途お知らせいたします。 *この記事* の [ ビルド時間要件 ](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/build-environment-details.md#runtime-requirements) の節を参照してください。
>

#### AEM Java ログ設定ポリシーの適用 {#logconfig-policy}

4 月のリリースノートに記載されているように、AEMの Java ログは、すべてのお客様の環境で信頼性の高い監視を確実に行うために、標準に従う必要があります。 ログ形式、出力ファイル、デフォルトログレベルの変更といったカスタムログ設定は、サポートされなくなりました。 ログはデフォルトファイルにダイレクトされ続け、AEM 製品コードのデフォルトログレベルは保持される必要があります。 詳しくは、[ログに関する記事](/help/implementing/developing/introduction/logging.md#configuration-loggers)を参照してください。

**1 月 29 日** 以降、サポートされていないカスタムログの上書きは無視されます。 Adobe の分析によると、ほとんどのお客様は影響を受けることはありません。現在の設定が影響を受ける可能性があるお客様にはご連絡済みです。

カスタムログ動作に依存するダウンストリームプロセスを確認し、更新してください。 例：

* ログ転送システムでカスタムログ形式が想定されている場合は、取り込みルールを調整する必要がある可能性があります。
* 以前にログレベルを変更してログの冗長性を削減したことがある場合は、デフォルトレベルに戻すとログのボリュームが増える可能性があることに注意してください。

### [!DNL Experience Manager] as a [!DNL Cloud Service] 基盤の早期導入者の機能 {#foundation-early-adopter}

#### 自動メンテナンスアップデートの一時停止 {#pause-updates}

運用開始日、ライブイベント、ピーク時の売上といった瞬間を逃すことはできません。[ 新しいセルフサービス機能 ](/help/implementing/deploying/quiet-hours-update-free-periods.md)により、重要な場合に自動メンテナンスアップデートを停止し、チームが集中できるようにします。

* 静かな時間：毎日設定された時間に自動メンテナンスをブロックします。勤務時間、夜間の実行や朝の切り替え時などに最適です。
* 更新不要の期間：自動メンテナンスを 1 週間ブロックします。ローンチ、プロモーションまたは年次フリーズに使用します。

>[!NOTE]
>
>9月25日（PT）に限定提供機能として提供を開始します。
>プログラムでアクティブ化するには、[aemcs-update-free@adobe.com](mailto:aemcs-update-free@adobe.com) にメールを送信してください。
>

#### Edge コンピューティング（Beta プログラム）

Edge コンピューティングを使用すると、CDN レイヤーで JavaScript を実行し、データ処理をエンドユーザーに近づけることができます。 これにより待ち時間が短縮され、エッジでレスポンシブな動的エクスペリエンスが実現します。

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


#### AI 回答 – AEM Sitesに対する、よりスマートでコンテキスト対応の応答（Beta プログラム） {#ai-answers-beta}

AI Answers は、訪問者がコンテンツを操作する新しい方法を導入します。 Retrieval-Augmented Generation （RAG）テクノロジーを活用し、AEMが管理するデータを使用して、デジタルエクスペリエンス内で直接、正確でブランドに一貫性のある回答を提供します。

AI AnswersBetaプログラムの立ち上げに備え、お客様の関心を登録する招待を開始しています。 ベータ版の容量は非常に限られているので、早期サインアップは優先的に考慮されます。 ベータ版に参加すると、AEM Cloud Service 環境で AI の回答を調べ、パフォーマンスと精度を検証し、利用可能になる前に将来のエクスペリエンスを形成するのに役立ちます。

参加をリクエストしたり、更新情報を受け取ったりするには、[feedback-ai-answers@adobe.com](mailto:feedback-ai-answers@adobe.com) にお問い合わせください。

#### RDE のスナップショット（Betaプログラム） {#rde-snapshot-program}

ベータ版の迅速な開発環境（RDE）で、現在のコードとコンテンツの状態をスナップショットとして取り、後で復元できる機能がサポートされるようになりました。 これは、元に戻す必要がある場合のあるコードを同期する場合や、異なる機能の開発を切り替える場合に役立つことがあります。 また、テストの既知の開始点として、可変コンテンツのみを復元することもできます。

この機能の使用やフィードバックの提供に関心がある場合は、[aemcs-rde-support@adobe.com](mailto:aemcs-rde-support@adobe.com) にメールを送信してください。

#### AI を使用したAEM開発の高速化（Alpha プログラム） {#ai-dev-alpha}

AEM Java スタックチームは、Cursor、Cloud Code、Visual Studio、IntelliJ などのツールで AI を利用した開発を行い、機能の配信を高速化し、コード品質を向上させています。 Adobeがサポートする将来の AI 機能を形成するのに役立つ、実際のエクスペリエンスを収集しています。

[aemcs-java-adopter@adobe.com](mailto:aemcs-java-adopter@adobe.com) に電子メールを送信して、チームの活動内容やAdobeからの情報提供内容を共有します。

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
