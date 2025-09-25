---
title: ' [!DNL Adobe Experience Manager] as a Cloud Service の最新のリリースノート。'
description: ' [!DNL Adobe Experience Manager]  as a Cloud Service の最新のリリースノート。'
mini-toc-levels: 1
exl-id: a2d56721-502c-4f4e-9b72-5ca790df75c5
feature: Release Information
role: Admin
source-git-commit: bdc0e7623592efed5270a3cb8322ef22e50cbad9
workflow-type: tm+mt
source-wordcount: '2066'
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

[!DNL Adobe Experience Manager] as a [!DNL Cloud Service] の最新の機能リリース（2025.9.0）の公開日は 2025年9月25日（PT）です。次回の機能リリース（2025.10.0）は、2025年10月30日（PT）に予定されています。

## メンテナンスリリースノート {#maintenance}

最新のメンテナンスリリースノートについては、[こちら](/help/release-notes/maintenance/latest.md)をご覧ください。

<!-- 

## Release Video {#release-video}

Have a look at the July 2025 Release Overview video for a summary of the features added in the 2025.7.0 release:

>[!VIDEO](https://video.tv.adobe.com/v/3440920?quality=12)

-->

## [!DNL Experience Manager Sites] as a [!DNL Cloud Service] {#sites}

### Experience Manager Sites プレリリースの新機能 {#prerelease-sites}

AEM コンテンツフラグメントのコンテンツモデルエディターは、AEMの他の React スペクトルベースのインターフェイスと連携するように最新化されました。 ユーザーインターフェイスの実装と拡張モデルが、コンテンツフラグメントエディターおよびユニバーサルエディターと一致するようになりました。 新しいコンテンツモデル管理 UI から開いた場合、新しいモデルエディターがデフォルトになりました。 タッチ UI でコンテンツモデルを開くと、タッチ UI エディターが開き、新しいエディターを試すことができます。

## [!DNL Experience Manager Assets] as a [!DNL Cloud Service] {#assets}

### Assets ビューの新機能 {#new-features-assets-view}

**Dynamic Media テンプレートの部分文字列を使用した拡張テキスト書式設定**

Dynamic Media テンプレートテキストレイヤー内の部分文字列に書式設定を適用できるようになりました。 選択した単語や語句は別のレイヤーとして扱われ、フォント、フォントサイズ、色などを調整できます。 部分文字列レイヤーは、テンプレートの配信 URL を使用してリアルタイムに更新できるようにパラメーター化されます

### OpenAPI 機能を備えた Dynamic Media の新機能 {#new-features-dynamic-media-with-openapi}

**OpenAPI URL を備えた SEO 対応 DM**

OpenAPI を備えた DM でのアセット配信用のバニティ URL を作成し、システムで生成された長い UUID を短い読み取り可能な識別子に置き換えます。これにより、リンクは SEO 対応になり、ブランドやキャンペーンとの整合性が向上します。バニティ URL は、既存のワークフローを中断することなく、実行時に元のアセット UUID に自動的に解決されます。

>[!NOTE]
>
>この機能は、限定提供（LA）機能として利用できます。 [アドビカスタマーサポートケースを作成および送信](https://helpx.adobe.com/jp/enterprise/using/support-for-experience-cloud.html)し、デプロイメントで有効にすることができます。

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

**日付と時刻の入力コンポーネント**

[日付と時刻コンポーネント](https://experienceleague.adobe.com/ja/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/date-time-component)が使用可能になり、ユーザーはカレンダーと時計のインターフェイスを使用して日付と時刻の両方を選択することや、サポートされている形式で値を手動で入力することができるようになりました。

**ファイルアップロードのエラー処理の強化**

[ファイル添付コンポーネント](https://experienceleague.adobe.com/ja/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/file-attachment#basic-tab)は、アップロードされたファイルタイプを許可リストに対して自動的に検証するようになりました。ユーザーがサポートされていない形式のファイルをアップロードすると、送信中にフォームにエラーが表示されます。また、このコンポーネントはファイルコンテンツをチェックして、そのタイプを検証するので、フォームの全体的なセキュリティが強化されます。

**カスタム送信アクションの指定されたエラー応答**

[カスタム送信アクション](/help/forms/custom-submit-action-troubleshooting.md)で未処理のエラーが発生した際、システムはエラーコード 502 を返します。これにより、問題がカスタム送信アクションに関連していることを識別でき、デバッグが簡単になります。

**レコードのドキュメントからの非表示フィールドの除外**

新しいプロパティにより、[レコードのドキュメント](/help/forms/generate-document-of-record-core-components.md#document-of-record-settings)から非表示フィールドを除外できるようになりました。デフォルトでは、このオプションは選択されておらず、すべてのフォームフィールドに適用されます。


### AEM Forms のプレリリース機能

**AFP レンディションの生成と同期**

[AEM Forms Communication API](/help/forms/document-generation-afp-api.md) を使用して、XDP ファイルを AFP 形式に変換できるようになりました。AFP は、大規模なエンタープライズ印刷で広く使用されている、高性能な形式です。

**ルールエディターの機能強化**

* [ 関数リストの Validate メソッド](/help/forms/rule-editor-enhancements-use-cases.md#validate-method-in-function-list)：validate メソッドと reset メソッドでは、パネル、フィールド、フォームの各レベルでの実行がサポートされるようになりました。以前は、フォームレベルでのみサポートされていました。
* [最新の JavaScript サポート](/help/forms/rule-editor-core-components-difference-tables.md)：カスタム関数に ECMAScript 2019 以降の機能のサポートが追加され、より効率的でモジュール形式の再利用可能なコードを記述できるようになりました。
* [ルールエディターの「DoR をダウンロード」オプション](/help/forms/rule-editor-enhancements-use-cases.md#downloaddor-as-ootb-fuction-in-rule-editor)：ルールエディターにレコードのドキュメント（DoR）をダウンロードする機能が、標準（OOTB）オプションとして追加されました。

  ![レコードのドキュメント](/help/forms/assets/document-of-record-rn.gif)

* [ルールエディターの動的変数](/help/forms/rule-editor-enhancements-use-cases.md#support-for-dynamic-variables-in-rules)：ルールエディターで動的（一時）変数を使用できるようになりました。これにより、条件とアクションをより柔軟に定義できます。一時的な値を保存するために非表示フィールドを使用する必要がなくなりました。
* [カスタムイベントベースのルールのサポート](/help/forms/rule-editor-enhancements-use-cases.md#custom-event-based-rules-support)：カスタムイベントを定義し、これらのイベントに基づいてルールをトリガーできるようになりました。
* [コンテキスト対応の繰り返し可能なパネルルール](/help/forms/rule-editor-enhancements-use-cases.md#context-based-rule-execution-for-repeatable-panels)：繰り返し可能なパネルでは、ルールは最後のパネルインスタンスにのみ適用される代わりに、コンテキストに基づいて実行されるようになりました。
* [パラメーターによってトリガーされるルール](/help/forms/rule-editor-enhancements-use-cases.md#url-and-browser-parameter-based-rules-in-adaptive-forms)：ルールエディターでは、クエリパラメーター、UTM パラメーター、ブラウザーパラメーターに基づくルール実行がサポートされるようになりました。
* [フォーム固有のカスタム関数](/help/edge/docs/forms/universal-editor/rule-editor-universal-editor.md#organizing-custom-functions-across-different-forms)：Edge Delivery Services Forms では、フォーム固有のカスタム関数スクリプトがサポートされ、再利用可能なロジックをより柔軟に管理できるようになりました。
* [カスタム関数の静的読み込み](/help/edge/docs/forms/universal-editor/rule-editor-universal-editor.md#static-imports-for-custom-functions)：ユニバーサルエディターのルールエディターで静的読み込みがサポートされ、開発者は複数のフォームをまたいで関数を整理、共有、再利用できるようになりました。

### AEM Forms の新しい早期アクセス機能 {#forms-new-early-access-features}

AEM Forms 早期アクセスプログラムでは、最先端の革新機能にいち早くアクセスできるだけでなく、その開発に意見を反映させるユニークな機会も提供されます。

これらのリリースノートでは、現在のリリースで提供されるイノベーションのリストを示します。早期アクセスプログラムで利用可能なイノベーションの完全なリストについて詳しくは、[AEM Forms 早期アクセスプログラムのドキュメント](/help/forms/early-access-ea-features.md)を参照してください。

**手書き署名コンポーネント**

[手書き署名コンポーネント](https://experienceleague.adobe.com/ja/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/scribble-signature)を使用して、ユーザーが契約書などのフォームに署名を追加できるようになりました。コンポーネントを使用すると、ユーザーはマウス、スタイラス、タッチスクリーンを使用してフォーム内に直接署名を入力できます。

**ルールエディターでの直接 API 統合**

アダプティブフォームでは、フォームデータモデルを必要とせずに、ビジュアルルールエディターで[直接 API 統合](/help/forms/api-integration-in-rule-editor.md)をサポートするようになりました。作成者は、URL または cURL 読み込みを使用して API を設定し、入力／出力パラメーターをマッピングし、認証を使用して安全な呼び出しを行うことができます。

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

運用開始日、ライブイベント、ピーク時の売上 – これらの瞬間は中断できません。 [ 新しいセルフサービス機能 ](/help/implementing/deploying/quiet-hours-update-free-periods.md) 重要な場合は自動メンテナンスアップデートを停止し、チームが集中できるようにします。

* Quiet Hours: 1 日の設定時間に自動メンテナンスをブロックします。 勤務時間、夜間の実行や朝のカットオーバーに最適です。
* 更新不要の期間：1 週間は自動メンテナンスをブロックします。 ローンチ、プロモーションまたは年次フリーズに使用します。

>[!NOTE]
>
>9 月 25 日（PT）に限定提供機能として提供を開始します。
>&#x200B;>プログラムでアクティブ化するには、[aemcs-update-free@adobe.com](mailto:aemcs-update-free@adobe.com) にメールを送信してください。

### AEM Developer Tools for Eclipse の新しいリリース {#aem-develeper-tools-for-eclipse}

AEM Developer Tools for Eclipse のバージョン 1.4.0 がリリースされました。 このバージョンは、Eclipse IDE 2022-12 以降のサポートを追加し、現在のバージョン（2025-09）で検証されています。 このツールは、最新バージョンのAEM プロジェクトアーキタイプで機能するようになり、Sling IDE Tooling 1.3.0 の改善点が組み込まれています。

[Eclipse Marketplace](https://marketplace.eclipse.org/content/aem-developer-tools-eclipse) からインストールし、[AEM Developer Tools ページ ](https://eclipse.adobe.com) を参照してください。

### 今後の Java API の非推奨（廃止予定） {#java-api-deprecation}

一部の非推奨 API は 8 月 31 日（PT）に削除対象としてマークされたため、参照できなくなりました。 コードに非推奨の API の使用が検出された場合はアクションセンターから通知が届き、11 月 13 日以降は、Cloud Manager ビルド中に通知が表示され、使用を削除することが重要になります。 詳しくは、[非推奨（廃止予定）に関する記事](/help/release-notes/deprecated-removed-features.md#aem-apis)を参照してください。便宜上、これらの API を次に示します。

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

### Java 11 ランタイムのデプロイメント {#java11-runtime-deprecation}

*Java 11 ランタイム* は非推奨（廃止予定）で、ほとんどの環境は既に高パフォーマンスの **Java 21 ランタイム** にアップグレードされています。

サポートされていない依存関係が原因で、環境をアップグレードできなかった場合（[Java 21 ランタイム要件 ](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/build-environment-details.md#runtime-requirements) を参照）、次の手順を記載したメールがAdobeから届いているはずです。 ここで説明しているように、Adobeは **2025 年 9 月 18 日（PT）に** 開発 **環境と** RDE **環境をアップグレードして** サイトとプロセスを検証し、問題に対処できるようにします。 **ステージング** および **実稼動** のアップグレードは、**2025 年 10 月 14 日** に続行されます。

>[!NOTE]
>
>ランタイムバージョンは、コードのビルドバージョンとは別のものです。 Java 21 を使用してビルドすることをお勧めしますが、現時点では、Java 11 ビルドは引き続き受け入れられます。 Java 11 ビルドの廃止に関する通知は、今後共有される予定です。

### AEM Java ログ設定ポリシーの適用 {#logconfig-policy}

4 月のリリースノートに記載されているように、AEMの Java ログは、すべてのお客様の環境で信頼性の高い監視を確実に行うために、標準に従う必要があります。 ログ形式、出力ファイル、デフォルトログレベルの変更といったカスタムログ設定は、サポートされなくなりました。 ログはデフォルトファイルにダイレクトされ続け、AEM 製品コードのデフォルトログレベルは保持される必要があります。 詳しくは、[ログに関する記事](/help/implementing/developing/introduction/logging.md#configuration-loggers)を参照してください。

**10 月 30 日** 以降、サポートされていないカスタムログの上書きは無視されます。 Adobe の分析によると、ほとんどのお客様は影響を受けることはありません。現在の設定が影響を受ける可能性があるお客様にはご連絡済みです。

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

### Edge Delivery ServicesのEdge認証（Beta プログラム） {#edge-authentication}

Edge認証を使用すると、Edge Delivery Services ページへのアクセスを、ID プロバイダー（IdP）で認証されたユーザーのみに制限できます。 これを実現するには、OpenID Connect （OIDC）設定の YAML ファイルをデプロイします。

ご興味がある場合は、ユースケースの簡単な説明とご質問を [0&rbrace;aemcs-edgecompute-feedback@adobe.com&rbrace; までお問い合わせください。](mailto:aemcs-edgecompute-feedback@adobe.com)

Edge Delivery Servicesとは別に、今年初めに、AEM ページを保護するために Open ID Connect[AEM Cloud Service パブリッシュ層プロジェクト用 ](/help/security/open-id-connect-support-for-aem-as-a-cloud-service-on-publish-tier.md) を設定する機能をリリースしました。

<!--
### CDN Configuration for Edge Delivery Services (Beta Program) {#cdn-eds-beta}

The Adobe-Managed CDN offers flexible configuration options, as described in the [Config Pipeline article](/help/operations/config-pipeline.md#configurations). 

Now in beta, youcan deploy a config pipeline for features including CDN origin selectors, response and request transformations, CDN log forwarding and more. Please reach out to [aemcs-cdn-config-adopter@adobe.com](mailto:aemcs-cdn-config-adopter@adobe.com) with the details of your use case.

-->

### RDE のスナップショット（Alpha プログラム） {#rde-snapshot-program}

Alpha では、高速開発環境（RDE）で、コードとコンテンツの現在の状態のスナップショットを取得し、後で復元できる機能がサポートされるようになりました。 これは、元に戻す必要がある場合のあるコードを同期する場合や、異なる機能の開発を切り替える場合に役立つことがあります。 また、テストの既知の開始点として、可変コンテンツのみを復元することもできます。

この機能に関するフィードバックをお送りいただく場合は、[aemcs-rde-support@adobe.com](mailto:aemcs-rde-support@adobe.com) までメールでお問い合わせください。

### その他の宛先への AEM ログ転送 (Beta プログラム) {#log-forwarding-beta}

ログは Cloud Manager からダウンロードできますが、多くの組織では、これらのログを優先されるログの宛先にストリーミングすると役立ちます。 AEM では、Azure Blob Storage、Datadog、HTTPS、Elasticsearch (および OpenSearch)、Splunk への AEM および CDN ログ転送をサポートしています。 この機能は、セルフサービス方式で設定し、設定パイプラインを使用してデプロイします。

Beta では、Amazon S3、Sumo Logic、Dynatrace および独自のNew Relic アカウント（Adobe が提供するアカウントではありません）に AEM ログを転送できます。 AEM ログ (Apache／Dispatcher など) はサポートされていますが、CDN ログはサポートされていません。 アクセスについて詳しくは、[aemcs-logforwarding-beta@adobe.com](mailto:aemcs-logforwarding-beta@adobe.com) までメールで送信してください。

詳しくは、[ログ転送ドキュメント](/help/implementing/developing/introduction/log-forwarding.md)を参照してください。

### APM （Application Performance Monitoring）の拡張（Alpha プログラム） {#apm-alpha}

観測性のために、AEM Cloud Service は現在、Adobe提供の [New Relic Oneおよびお客様が管理する ](https://experienceleague.adobe.com/ja/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/user-access-new-relic)2&rbrace;Dynatrace[ をサポートしています。 ](https://experienceleague.adobe.com/ja/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/dynatrace)追加の APM オプションのサポートについては、ユースケースと共に、お好みのベンダーまたはテクノロジーを記載したメールを [0&rbrace;aemcs-apm-beta@adobe.com&rbrace; までお送りください。](mailto:aemcs-apm-beta@adobe.com)


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
