---
title: ' [!DNL Adobe Experience Manager]  as a Cloud Service 2025.10.0 リリースのリリースノート。'
description: ' [!DNL Adobe Experience Manager]  as a Cloud Service 2025.10.0 リリースのリリースノート。'
feature: Release Information
role: Admin
exl-id: d5eb6d9e-308f-4a51-8bcf-b8077b5bec82
source-git-commit: fa8035f826a4d08c18bc0d2b7664015c6fc82698
workflow-type: tm+mt
source-wordcount: '1894'
ht-degree: 59%

---

# [!DNL Adobe Experience Manager] as a Cloud Service の 2025.10.0 リリースノート {#release-notes}

以下の節では、[!DNL Experience Manager] as a Cloud Service の 2025.10.0 バージョンの機能リリースノートの概要について説明します。

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

>[!VIDEO](https://video.tv.adobe.com/v/3440920?quality=12)

-->

## [!DNL Experience Manager Sites] as a [!DNL Cloud Service] {#sites}

### Experience Manager Sites の新機能 {#new-sites}

* [&#x200B; コンテンツフラグメントのローンチ &#x200B;](/help/sites-cloud/administering/content-fragments/launches-for-content-fragments.md): コンテンツオーサーは、コンテンツフラグメントのローンチを使用して、構造化コンテンツの今後のバリエーションを作成およびスケジュールできるようになりました。 新しいコンテンツフラグメントコンソールでは、ソースブランチと同期できる将来のコンテンツのブランチとして、コンテンツフラグメントのローンチを作成、編集、管理、スケジュールできます。 新しい差分ビューでは、今後の公開のためにローンチを確定する前に、すべてのコンテンツの変更を明確に把握できます。

* AEM コンテンツフラグメント [の](/help/sites-cloud/administering/content-fragments/content-fragment-models.md) コンテンツモデルエディターは、AEMの他のReact Spectrum ベースのインターフェイスと連携するように最新化されました。 ユーザーインターフェイスの実装と拡張モデルが、コンテンツフラグメントエディターおよびユニバーサルエディターと一貫性を保つようになりました。新しいコンテンツモデル管理 UI から開いた場合、新しいモデルエディターがデフォルトになりました。タッチ UI でコンテンツモデルを開くと、タッチ UI エディターが開き、新しいエディターを試すことができます。

<!--

### New Features in Content Hub {#new-features-content-hub}

**Mark Collections as Favourites**

You can now mark collections as Favorites in Content Hub, making it easier to organize and retrieve them. Once added, your favourite collections are conveniently available from the **Favourites** tab on the Content Hub home page.

**Pin collections for quick access**

Content Hub Administrators can now pin collections in Content Hub for quick access. Pinned collections are displayed in a dedicated **Pinned** section on the Collections home page, making it easier to keep important collections within reach.

>[!NOTE]
>
>These features are available as Limited Availability features. You can [create and submit an Adobe Customer Support case](https://helpx.adobe.com/enterprise/using/support-for-experience-cloud.html) to enable it for your deployment.

-->

## [!DNL Experience Manager Forms] as a [!DNL Cloud Service] {#forms}

### Experience Manager Forms の新機能 {#new-features-forms}

**アダプティブフォームとフォームフラグメント用のユニバーサルエディター**

ユニバーサルエディターは、アダプティブFormsと再利用可能なフォームフラグメントを作成するための統一されたオーサリングエクスペリエンスを提供するようになりました。 制作者は、強力な拡張機能と包括的な送信機能を活用して、直観的なWYSIWYG環境でフォームを視覚的にデザインできます。 このエディターは、セキュリティを強化するためにreCAPTCHA検証を統合し、手作業を減らすための事前入力サービスを提供し、あらゆるデバイスでレスポンシブデザインをサポートします。

**使用可能な拡張機能：**

* **ルールエディター**：視覚的なルールエディターを使用すると、フォーム作成者は、コーディング、イベント駆動型ルールのサポート、即時の検証、エラー処理を行うことなく、フォームフィールドに動的な動作を追加できます。
* **フォームのプロパティ**: ユーザーが送信アクション、事前入力サービス、サンキューメッセージ、その他のフォーム関連の動作をエディター内で直接設定できるようにするためのウィザードです。
* **フォームデータ Sourceとバインド参照**: データソース拡張機能を使用すると、フォーム作成者は、データモデルに関連付けられたコンポーネントをアダプティブフォームに直接追加し、すべてのコンポーネントのツリー選択範囲からバインド参照を選択できます。

**サポートされている送信アクション：**

ユニバーサルエディターは、カスタム送信アクション、Microsoft SharePointへの送信、Microsoft OneDriveへの送信、Azure Blob Storageへの送信、REST エンドポイントへの送信、AEM ワークフローの呼び出し、Power Automate フローの呼び出し、Marketo Engageへの送信、Adobe Experience Platform（AEP）への送信、スプレッドシートへの送信、フォームデータモデル（FDM）を使用した送信、Workfront Fusionへの送信、メール送信など、包括的な送信ワークフローをサポートします。

詳しくは、[Forms用ユニバーサルエディターのドキュメント &#x200B;](/help/edge/docs/forms/universal-editor/overview-universal-editor-for-edge-delivery-services-for-forms.md)を参照してください。 送信アクションの設定について詳しくは、[&#x200B; アダプティブフォーム送信アクション &#x200B;](/help/edge/docs/forms/universal-editor/submit-action.md)を参照してください。

<!--
 ### Pre-Release features in AEM Forms 

**Rule Editor Enhancements**

The Rule Editor now supports enhanced navigation and allows use of function and mathematical expressions in input parameters.

**Enhanced Navigation with Event Payload Support**
 
The `Navigate To` action in the Invoke Service handlers now supports `EVENT_PAYLOAD`, enabling form authors to configure follow-up actions based on event responses. This enhancement offers greater flexibility in designing post-submission workflows, ensuring smoother transitions and more personalized user experiences. For more information, see [Enhanced Navigation with Event Payload Support](/help/forms/invoke-service-enhancements-rule-editor.md#use-case-5-use-event-payload-in-navigate-to-action-in-invoke-service).

**Function and Mathematical Expression Support in Input Parameters**
 
Input parameters now support both function calls and mathematical expressions, enabling form authors to pass dynamically computed values directly. This enhancement streamlines rule configurations, eliminates the need for extra fields, and makes forms more adaptable to complex logic and calculation-driven scenarios. For more information, see [Function and Mathematical Expression Support in Input Parameters](/help/forms/rule-editor-core-components-user-interface.md#function-and-mathematical-expression-support-in-input-parameters).
-->

### AEM Forms の新しい早期アクセス機能 {#forms-new-early-access-features}

AEM Forms 早期アクセスプログラムでは、最先端の革新機能にいち早くアクセスできるだけでなく、その開発に意見を反映させるユニークな機会も提供されます。

これらのリリースノートでは、現在のリリースで提供されるイノベーションのリストを示します。早期アクセスプログラムで利用可能なイノベーションの完全なリストについて詳しくは、[AEM Forms 早期アクセスプログラムのドキュメント](/help/forms/early-access-ea-features.md)を参照してください。

#### インタラクティブ通信の機能強化

##### テンプレートのロック

テンプレート内でコンテンツやレイアウト要素をロックすることで、ブランドの整合性を維持し、不正な変更を防止します。 これにより、あらゆるコミュニケーションでデザインの一貫性を確保できます。

##### コンテンツオーバーフローのサポート

フローしたレイアウトの「コンテンツ内でページ区切りを許可」オプションを導入する。 この機能強化により、複数ページの編集がスムーズになり、複雑なドキュメントのテキスト管理が改善されます。

##### XDP ファイル編集

インタラクティブ通信エディターで、フラグメント統合を含むXDP編集がサポートされるようになりました。 Microsoft Windows デスクトップでのみ動作するForms Designerではなく、ブラウザーでXDP ファイルを編集できるようになりました。

##### 動的なページ番号

マスターページに「ページ番号（##）」を自動的に表示し、複数ページのドキュメント間で明確で一貫性のあるページネーションを実現します。

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

### AEMのその他の配信先へのログ転送 {#log-forwarding}

AEM ログを、Amazon S3、Sumo Logic、Dynatrace、および自分のNew Relic アカウント（Adobeが提供するアカウントではなく）に転送できるようになりました。 AEM ログ（Apache/Dispatcherを含む）は、これらのログ宛先でサポートされますが、CDN ログはサポートされません。

サポートされている[&#x200B; ログ転送先](/help/implementing/developing/introduction/log-forwarding.md)の完全なセットを参照してください。

### Edge Delivery ServicesのConfig Pipeline {#config-pipeline-eds}

Config Pipelinesは、Edge Delivery Servicesで構築されたサイトでサポートされるようになり、AEM オーサーとAEM パブリッシュ配信の枠を超えました。 Config Pipelinesを使用して、トラフィックフィルタールールやオリジンセレクターなどのCDN設定などの設定を管理できます。 詳しくは、[サポートされている設定](/help/operations/config-pipeline.md#configurations)を参照してください。

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

Adobeは、2025年10月14日に&#x200B;**ステージ**&#x200B;および&#x200B;**実稼動**&#x200B;環境を高性能&#x200B;**Java 21 ランタイム**&#x200B;にアップグレードしました。 1月下旬からは、AEM Cloud Service SDKもクラウド環境もJava 11 ランタイムで動作しません。

>[!NOTE]
>
> 最新のパフォーマンス最適化と言語の機能強化を活用するには、Java 17またはJava 21 （推奨）で構築することをお勧めします。 Java 8およびJava 11を使用したビルドは現在サポートされていますが、今後のリリースで非推奨（廃止予定）になります。 非推奨化の前に、別のコミュニケーションが発行されます。 *この記事*&#x200B;の「[&#x200B; ビルド時間の要件](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/build-environment-details.md#runtime-requirements)」セクションを参照してください。
>

### AEM Java ログ設定ポリシーの適用 {#logconfig-policy}

4 月のリリースノートに記載されているように、AEMの Java ログは、すべてのお客様の環境で信頼性の高い監視を確実に行うために、標準に従う必要があります。 ログ形式、出力ファイル、デフォルトログレベルの変更といったカスタムログ設定は、サポートされなくなりました。 ログはデフォルトファイルにダイレクトされ続け、AEM 製品コードのデフォルトログレベルは保持される必要があります。 詳しくは、[ログに関する記事](/help/implementing/developing/introduction/logging.md#configuration-loggers)を参照してください。

**11月20日**&#x200B;以降、サポートされていないカスタムログの上書きは無視されます。 Adobe の分析によると、ほとんどのお客様は影響を受けることはありません。現在の設定が影響を受ける可能性があるお客様にはご連絡済みです。

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


### AIの回答 – AEM Sites向けの、よりスマートでコンテキストに応じた回答（Beta プログラム） {#ai-answers-beta}

AI Answersは、訪問者がコンテンツを操作するための新しい方法を導入します。 AEMで管理されているデータを利用して、検索機能の拡張生成（RAG）機能を活用し、ブランド一貫性のある正確な回答をデジタル体験内で直接提供できます。

アドビでは、AI Answers Betaプログラムを立ち上げる準備を進めており、現在、お客様に関心をお持ちいただくよう呼びかけています。 ベータ版の機能は非常に限られているため、早期サインアップは優先的に検討されます。 ベータ版に参加すると、AEM Cloud Service環境でAIの回答を確認し、パフォーマンスと正確性を検証して、一般公開される前に将来のエクスペリエンスを形作ることができます。

参加をリクエストしたり、更新を受け取ったりするには、[feedback-ai-answers@adobe.com](mailto:feedback-ai-answers@adobe.com)にお問い合わせください。


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
