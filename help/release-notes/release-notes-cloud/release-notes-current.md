---
title: ' [!DNL Adobe Experience Manager] as a Cloud Service の最新のリリースノート。'
description: ' [!DNL Adobe Experience Manager]  as a Cloud Service の最新のリリースノート。'
mini-toc-levels: 1
exl-id: a2d56721-502c-4f4e-9b72-5ca790df75c5
feature: Release Information
role: Admin
source-git-commit: 247a501660475d2f3ae9cff735a1845094d02c82
workflow-type: tm+mt
source-wordcount: '1628'
ht-degree: 69%

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

[!DNL Adobe Experience Manager] as a [!DNL Cloud Service] の最新の機能リリース（2025.10.0）のリリース日は、2025年10月30日（PT）です。次回の機能リリース（2025.11.0）は 2025年11月20日（PT）に予定されています。

## メンテナンスリリースノート {#maintenance}

最新のメンテナンスリリースノートについては、[こちら](/help/release-notes/maintenance/latest.md)をご覧ください。

<!-- 

## Release Video {#release-video}

Have a look at the July 2025 Release Overview video for a summary of the features added in the 2025.7.0 release:

>[!VIDEO](https://video.tv.adobe.com/v/3440921?captions=jpn&quality=12)

-->

## [!DNL Experience Manager Sites] as a [!DNL Cloud Service] {#sites}

### Experience Manager Sites の新機能 {#new-sites}

* AEM コンテンツフラグメント用の [&#x200B; コンテンツモデルエディター &#x200B;](/help/sites-cloud/administering/content-fragments/content-fragment-models.md) は、AEMの他の React スペクトルベースのインターフェイスと連携するように最新化されました。 ユーザーインターフェイスの実装と拡張モデルが、コンテンツフラグメントエディターおよびユニバーサルエディターと一貫性を保つようになりました。新しいコンテンツモデル管理 UI から開いた場合、新しいモデルエディターがデフォルトになりました。タッチ UI でコンテンツモデルを開くと、タッチ UI エディターが開き、新しいエディターを試すことができます。

* [&#x200B; コンテンツフラグメントのローンチ &#x200B;](/help/sites-cloud/administering/content-fragments/launches-for-content-fragments.md)：コンテンツフラグメントコンソールの「ローンチ」タブでは、ローンチの作成、既存のすべてのローンチの一覧表示、主要なプロパティの表示、ローンチに対するアクションの実行ができます。

<!--

### New Features in Content Hub {#new-features-content-hub}

**Mark Collections as Favourites**

You can now mark collections as Favorites in Content Hub, making it easier to organize and retrieve them. Once added, your favourite collections are conveniently available from the **Favourites** tab on the Content Hub home page.

**Pin collections for quick access**

Content Hub Administrators can now pin collections in Content Hub for quick access. Pinned collections are displayed in a dedicated **Pinned** section on the Collections home page, making it easier to keep important collections within reach.

>[!NOTE]
>
>These features are available as Limited Availability features. You can [create and submit an Adobe Customer Support case](https://helpx.adobe.com/jp/enterprise/using/support-for-experience-cloud.html) to enable it for your deployment.

-->

## [!DNL Experience Manager Forms] as a [!DNL Cloud Service] {#forms}

### Experience Manager Forms の新機能 {#new-features-forms}

**アダプティブフォームとフォームフラグメント用のユニバーサルエディター**

ユニバーサルエディターは、アダプティブFormsと再利用可能なフォームフラグメントを作成するための統一されたオーサリングエクスペリエンスを提供するようになりました。 作成者は、フォームの視覚的なデザイン、送信アクションの設定および reCAPTCHA 検証の統合を、直感的なWYSIWYG環境内で行えます。

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

### リリース管理の新機能 {#new-features-release-management}

**自動メンテナンスアップデートの一時停止**

運用開始日、ライブイベント、ピーク時の売上といった瞬間を逃すことはできません。[&#x200B; 新しいセルフサービス機能 &#x200B;](/help/implementing/deploying/quiet-hours-update-free-periods.md)により、重要な場合に自動メンテナンスアップデートを停止し、チームが集中できるようにします。

* 静かな時間：毎日設定された時間に自動メンテナンスをブロックします。勤務時間、夜間の実行や朝の切り替え時などに最適です。
* 更新不要の期間：自動メンテナンスを 1 週間ブロックします。ローンチ、プロモーションまたは年次フリーズに使用します。

>[!NOTE]
>
>9月25日（PT）に限定提供機能として提供を開始します。
>プログラムでアクティブ化するには、[aemcs-update-free@adobe.com](mailto:aemcs-update-free@adobe.com) にメールを送信してください。

### その他の宛先へのAEM ログ転送 {#log-forwarding}

AEM ログを、Amazon S3、Sumo Logic、Dynatraceおよび（Adobeが提供するアカウントではなく）独自のNew Relic アカウントに転送できるようになりました。 なお、これらのログ先ではAEM ログ（Apache/Dispatcherを含む）がサポートされていますが、CDN ログはサポートされていません。

すべての [&#x200B; サポートされるログ転送宛先 &#x200B;](/help/implementing/developing/introduction/log-forwarding.md) を参照してください。

### Edge Delivery Servicesの設定パイプライン {#config-pipeline-eds}

Edge Delivery Servicesで作成されたサイトで Config パイプラインがサポートされるようになり、この機能がAEM オーサーおよびAEM パブリッシュ配信のみに拡張されました。 設定パイプラインを使用して、トラフィックフィルタールールや接触チャネルセレクターなどの CDN 設定を管理できます。 詳しくは、[サポートされている設定](/help/operations/config-pipeline.md#configurations)を参照してください。

Edge Delivery 設定パイプラインは、Cloud Manager パイプライン変数を通じて秘密鍵もサポートします。

[Edge Delivery パイプラインを追加する](/help/implementing/cloud-manager/configuring-pipelines/configuring-edge-delivery-pipeline.md)を参照してください。

### 今後の Java API の非推奨（廃止予定） {#java-api-deprecation}

一部の非推奨（廃止予定）API は、8月31日（PT）の削除としてマークされたので、参照できなくなります。コード内に非推奨の API の使用が検出された場合はアクションセンターから通知が届きます。11月13日（PT）以降は、使用を削除することの重要性を強調する通知が Cloud Manager ビルド中に表示されます。詳しくは、[非推奨（廃止予定）に関する記事](/help/release-notes/deprecated-removed-features.md#aem-apis)を参照してください。便宜上、これらの API を次に示します。

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

### Java 11 ランタイムの非推奨（廃止予定） {#java11-runtime-deprecation}

Adobeは 2025 年 10 月 14 日に **ステージング** 環境と **実稼動** 環境を高性能の **Java 21 ランタイム** にアップグレードしました。 1 月下旬からは、AEM Cloud Service SDKもどのクラウド環境も Java 11 ランタイムで動作しなくなります。

>[!NOTE]
>
> 最新のパフォーマンス最適化と言語強化を活用するには、Java 17 または Java 21 （推奨）を使用してビルドすることをお勧めします。 Java 8 および Java 11 を使用したビルドは、現時点ではサポートされていますが、今後のリリースで非推奨（廃止予定）になります。 廃止に先立ち、別途お知らせいたします。 *この記事* の [&#x200B; ビルド時間要件 &#x200B;](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/build-environment-details.md#runtime-requirements) の節を参照してください。
>

### AEM Java ログ設定ポリシーの適用 {#logconfig-policy}

4 月のリリースノートに記載されているように、AEMの Java ログは、すべてのお客様の環境で信頼性の高い監視を確実に行うために、標準に従う必要があります。 ログ形式、出力ファイル、デフォルトログレベルの変更といったカスタムログ設定は、サポートされなくなりました。 ログはデフォルトファイルにダイレクトされ続け、AEM 製品コードのデフォルトログレベルは保持される必要があります。 詳しくは、[ログに関する記事](/help/implementing/developing/introduction/logging.md#configuration-loggers)を参照してください。

**11 月 20 日** 以降、サポートされていないカスタム記録の上書きは無視されます。 Adobe の分析によると、ほとんどのお客様は影響を受けることはありません。現在の設定が影響を受ける可能性があるお客様にはご連絡済みです。

カスタムログ動作に依存するダウンストリームプロセスを確認し、更新してください。 例：

* ログ転送システムでカスタムログ形式が想定されている場合は、取り込みルールを調整する必要がある可能性があります。
* 以前にログレベルを変更してログの冗長性を削減したことがある場合は、デフォルトレベルに戻すとログのボリュームが増える可能性があることに注意してください。

### Edge コンピューティング（Beta プログラム） {#edge-computing}

Edge コンピューティングを使用すると、CDN レイヤーで JavaScript を実行し、データ処理をエンドユーザーに近づけることができます。 これにより待ち時間が短縮され、エッジでレスポンシブな動的エクスペリエンスが実現します。

一般的なユースケースを次に示します。

* 位置情報、デバイスタイプまたはユーザー属性に基づくコンテンツのパーソナライズ
* CDN と接触チャネルの間のミドルウェアとして機能させる
* サードパーティの API からの応答をブラウザーに配信する前に再フォーマットする（および複数の API 応答を集計する）
* 様々なバックエンドからステッチされたコンテンツを使用し、サーバーレンダリングされた HTML をエッジで作成および提供
* ChatGPT や Claude などの LLM がカスタムツールにアクセスできるように MCP サーバーを公開する

AEM パブリッシュ配信またはライブ実稼動サイトのEdge Delivery Services プロジェクトで利用できる機会の数は限られています。 参加に関心がある場合や、詳細を確認したい場合は、ユースケースの簡単な説明を添えて [aemcs-edgecompute-feedback@adobe.com](mailto:aemcs-edgecompute-feedback@adobe.com)までメールでご連絡ください。

### Edge Delivery Services の Edge 認証（Beta プログラム） {#edge-authentication}

Edge 認証を使用すると、Edge Delivery Services ページへのアクセスを、ID プロバイダー（IdP）で認証されたユーザーのみに制限できます。これを実現するには、OpenID Connect（OIDC）設定の YAML ファイルをデプロイします。

ご興味がある場合は、ユースケースの簡単な説明とご質問を [aemcs-edgecompute-feedback@adobe.com](mailto:aemcs-edgecompute-feedback@adobe.com) までお問い合わせください。

<!--
### CDN Configuration for Edge Delivery Services (Beta Program) {#cdn-eds-beta}

The Adobe-Managed CDN offers flexible configuration options, as described in the [Config Pipeline article](/help/operations/config-pipeline.md#configurations). 

Now in beta, youcan deploy a config pipeline for features including CDN origin selectors, response and request transformations, CDN log forwarding and more. Please reach out to [aemcs-cdn-config-adopter@adobe.com](mailto:aemcs-cdn-config-adopter@adobe.com) with the details of your use case.

-->

### ライブトラフィックを受け入れる前にコードをテストするための Canary 実稼動デプロイメント（Beta プログラム） {#canary-beta}

エンドユーザーに公開する前に、内部専用テストトラフィックを使用して実稼動ビルドを検証します。実稼動環境に出荷し、Canary トラフィックのみをルーティング（特別なヘッダーを使用）し、動作を監視してから、顧客に影響を与えることなく、ライブトラフィックに昇格するか、ロールバックします。

コードリリースを実稼動環境にデプロイしますが、ライブトラフィックを受け入れるかロールバックするかを決定する前に、内部テストトラフィックのみに制限します。

アクセスをリクエストしてフィードバックを共有するには、[aemcs-canary-deployments-beta@adobe.com](mailto:aemcs-canary-deployments-beta@adobe.com) にメールを送信してください。


### AI 回答 – AEM Sitesに対する、よりスマートでコンテキスト対応の応答（Beta プログラム） {#ai-answers-beta}

AI Answers は、訪問者がコンテンツを操作する新しい方法を導入します。 Retrieval-Augmented Generation （RAG）テクノロジーを活用し、AEMが管理するデータを使用して、デジタルエクスペリエンス内で直接、正確でブランドに一貫性のある回答を提供します。

このベータ版の一部として、AEM Cloud Service 環境で AI の回答を安全に調べることができます。 このアプローチにより、パフォーマンス、精度および全体的なエクスペリエンスをライブオーディエンスに提供する前に検証できます。 検証が完了したら、AI Answers エクスペリエンスを完全な実稼動環境に昇格できます。

ベータ版へのアクセスをリクエストしたり、フィードバックを共有したりするには、[feedback-ai-answers@adobe.com](mailto:feedback-ai-answers@adobe.com) にお問い合わせください。


### RDE のスナップショット（Alpha プログラム） {#rde-snapshot-program}

Alpha では、高速開発環境（RDE）で、コードとコンテンツの現在の状態のスナップショットを取得し、後で復元できる機能がサポートされるようになりました。 これは、元に戻す必要がある場合のあるコードを同期する場合や、異なる機能の開発を切り替える場合に役立つことがあります。 また、テストの既知の開始点として、可変コンテンツのみを復元することもできます。

この機能に関するフィードバックをお送りいただく場合は、[aemcs-rde-support@adobe.com](mailto:aemcs-rde-support@adobe.com) までメールでお問い合わせください。

### アプリケーションパフォーマンスモニタリング（APM）の拡張（Alpha プログラム） {#apm-alpha}

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
