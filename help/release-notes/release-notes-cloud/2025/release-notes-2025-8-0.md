---
title: ' [!DNL Adobe Experience Manager]  as a Cloud Service 2025.8.0 リリースのリリースノート。'
description: ' [!DNL Adobe Experience Manager]  as a Cloud Service 2025.8.0 リリースのリリースノート。'
feature: Release Information
role: Admin
source-git-commit: 245ad07ba6abbf18e2011cb71a15948c9b92f80f
workflow-type: tm+mt
source-wordcount: '1934'
ht-degree: 86%

---

# [!DNL Adobe Experience Manager] as a Cloud Service の 2025.8.0 リリースノート {#release-notes}

以下の節では、[!DNL Experience Manager] as a Cloud Service の 2025.8.0 バージョンの機能リリースノートの概要について説明します。

>[!NOTE]
>
>ここから、以前のバージョン（例えば、2023年、2024年）のリリースノートに移動できます。
>
>[!DNL Experience Manager] as a Cloud Service の今後の機能のアクティベーションについての詳細は、[Experience Manager リリースロードマップ](https://experienceleague.adobe.com/ja/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap)をご覧ください。

>[!NOTE]
>
>Experience Cloud リリースノートの更新に関するメール通知を毎月受信するには、[アドビ製品アップデートの優先通知](https://www.adobe.com/subscription/priority-product-update.html)を購読してください。

## リリース日 {#release-date}

[!DNL Adobe Experience Manager] as a [!DNL Cloud Service] の最新の機能リリース（2025.8.0）のリリース日は 2025年8月28日（PT）です。次回の機能リリース（2025.9.0）は、2025年9月25日（PT）に予定されています。

## メンテナンスリリースノート {#maintenance}

最新のメンテナンスリリースノートについては、[こちら](/help/release-notes/maintenance/latest.md)をご覧ください。

<!-- 

## Release Video {#release-video}

Have a look at the July 2025 Release Overview video for a summary of the features added in the 2025.7.0 release:

>[!VIDEO](https://video.tv.adobe.com/v/3440920?quality=12)

-->

## Experience Hub {#experience-hub}

[Experience Hub](/help/experience-hub.md) は、すべての AEM 機能にアクセスするための一元的な開始点です。ユーザーのペルソナと使用可能なライセンスに基づいてパーソナライズされるので、各ユーザーは結果を効率的に達成できます。

## AEM の AI アシスタント {#AI-assistant}

AEM 用 [AI アシスタント](/help/implementing/cloud-manager/ai-assistant-in-aem.md)は、AEM 製品関連の質問に即座に回答（*すべてのユーザーが使用可能*）し、サポートチケットの作成を自動化（*サポート管理者が使用可能*）するためにデザインされた対話型インターフェイスを提供します。AEM に直接埋め込まれ、AEM Experience Hub、Cloud Manager、オーサー UI からアクセスできます。

## [!DNL Experience Manager Sites] as a [!DNL Cloud Service] {#sites}

### Experience Manager Sites の新機能 {#enhancements-sites}

* コンテンツフラグメント管理 UI では、コンテンツフラグメントのワークフローステータスと、選択したフラグメントの過去および現在実行中のワークフローの詳細情報を表示できるようになりました。
* 新しいコンテンツフラグメントエディターでコンテンツフラグメントを開くパフォーマンスは、パスの代わりに UUID 経由でフラグメントを開くことで、一般的なシナリオで 25％向上しました。
* 参照フラグメントを含むコンテンツフラグメントをコピーする際、参照フラグメントのコピーが親フラグメントのコピーと同じ場所に保存されるようになりました。
* フォルダー設定でカスタムワークスペースを設定して、コンテンツフラグメントを Adobe Target で設定されたワークスペースに書き出すことができるようになりました。

## [!DNL Experience Manager Assets] as a [!DNL Cloud Service] {#assets}

### コンテンツハブの新機能 {#new-features-content-hub}

**フィルタープロパティ経由の一括検索**

コンテンツハブでは、必要なアセットをすばやく見つけることができるようになりました。新しい一括検索機能を使用すると、任意のフィルタープロパティに複数の値（区切り文字で区切られた値、例えば、複数の SKU ID）を入力し、1 回の検索で一致するすべてのアセットを即座に取得できます。

### OpenAPI 機能を備えた Dynamic Media の新機能 {#new-features-dynamic-media-with-openapi}

**ブランド化され、読み取り可能なアセット配信 URL**

OpenAPI を使用して Dynamic Media でバニティ URL を活用することで、OpenAPI URL を使用した Dynamic Media をより人間が読みやすいものにします。 バニティー URL を使用すると、アセット配信 URL に含まれる、システムで生成され、記憶が困難な長い UUID を、ブランドで制御される短い識別子に置き換えることができます。 これにより、バニティー URL が短くなり、読みやすく、共有が容易になり、ブランドやキャンペーンとのより良い関連付けが可能になります。 バニティ URL は、既存のワークフローを中断することなく、実行時に元のアセット UUID に自動的に解決されます。

>[!NOTE]
>
>この機能は、9月10日（PT）に限定提供機能として提供されます。[アドビカスタマーサポートケースを作成および送信](https://helpx.adobe.com/jp/enterprise/using/support-for-experience-cloud.html)し、デプロイメントで有効にすることができます。

## [!DNL Experience Manager Forms] as a [!DNL Cloud Service] {#forms}

* [&#x200B; 日付と時刻の入力コンポーネント &#x200B;](https://experienceleague.adobe.com/ja/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/date-time-component)：日付と時刻のコンポーネントが使用できるようになり、カレンダーと時計のインターフェイスを使用して、またはサポートされている形式で手動で値を入力して、日付と時刻の両方を選択できるようになりました。
* [&#x200B; ファイルのアップロードのエラー処理の強化 &#x200B;](https://experienceleague.adobe.com/ja/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/file-attachment#basic-tab)：ファイル添付コンポーネントは、アップロードされたファイルタイプを許可リストと照合して自動的に検証するようになりました。 ユーザーがサポートされていない形式のファイルをアップロードすると、送信中にフォームにエラーが表示されます。また、このコンポーネントはファイルコンテンツをチェックして、そのタイプを検証するので、フォームの全体的なセキュリティが強化されます。
* [&#x200B; カスタム送信アクションに対して指定されたエラー応答 &#x200B;](/help/forms/custom-submit-action-troubleshooting.md)：カスタム送信アクションで未処理のエラーが発生した場合は、エラーコード 502 が返されます。 これにより、問題がカスタム送信アクションに関連していることを識別でき、デバッグが簡単になります。
* [&#x200B; レコードのドキュメントからの非表示フィールドの除外 &#x200B;](/help/forms/generate-document-of-record-core-components.md#document-of-record-settings)：レコードのドキュメントから非表示フィールドを除外できるように、新しいプロパティが追加されました。 デフォルトでは、このオプションは選択されておらず、すべてのフォームフィールドに適用されます。

### AEM Forms のプレリリース機能

* [AFP レンディションの生成と同期 &#x200B;](/help/forms/document-generation-afp-api.md): AEM Forms Communication API を使用して、XDP ファイルを AFP 形式に変換できるようになりました。 AFP は、大規模なエンタープライズ印刷で広く使用されている、高性能な形式です。
* **ルールエディターの機能強化**
   * [&#x200B; 関数リストの Validate メソッド](/help/forms/rule-editor-enhancements-use-cases.md#validate-method-in-function-list)：validate メソッドと reset メソッドでは、パネル、フィールド、フォームの各レベルでの実行がサポートされるようになりました。以前は、フォームレベルでのみサポートされていました。
   * [&#x200B; 最新のJavaScriptのサポート &#x200B;](/help/forms/rule-editor-core-components-difference-tables.md):ECMAScript 2019 以降の機能がカスタム関数に対してサポートされ、より効率的なモジュール型で再利用可能なコードを記述できるようになりました
   * [ルールエディターの「DoR をダウンロード」オプション](/help/forms/rule-editor-enhancements-use-cases.md#downloaddor-as-ootb-fuction-in-rule-editor)：ルールエディターにレコードのドキュメント（DoR）をダウンロードする機能が、標準（OOTB）オプションとして追加されました。
     ![レコードのドキュメント](/help/forms/assets/document-of-record-rn.gif)
   * [ルールエディターの動的変数](/help/forms/rule-editor-enhancements-use-cases.md#support-for-dynamic-variables-in-rules)：ルールエディターで動的（一時）変数を使用できるようになりました。これにより、条件とアクションをより柔軟に定義できます。一時的な値を保存するために非表示フィールドを使用する必要がなくなりました。
   * [カスタムイベントベースのルールのサポート](/help/forms/rule-editor-enhancements-use-cases.md#custom-event-based-rules-support)：カスタムイベントを定義し、これらのイベントに基づいてルールをトリガーできるようになりました。
   * [コンテキスト対応の繰り返し可能なパネルルール](/help/forms/rule-editor-enhancements-use-cases.md#context-based-rule-execution-for-repeatable-panels)：繰り返し可能なパネルでは、ルールは最後のパネルインスタンスにのみ適用される代わりに、コンテキストに基づいて実行されるようになりました。
   * [パラメーターによってトリガーされるルール](/help/forms/rule-editor-enhancements-use-cases.md#url-and-browser-parameter-based-rules-in-adaptive-forms)：ルールエディターでは、クエリパラメーター、UTM パラメーター、ブラウザーパラメーターに基づくルール実行がサポートされるようになりました。
   * [フォーム固有のカスタム関数](/help/edge/docs/forms/universal-editor/rule-editor-universal-editor.md#organizing-custom-functions-across-different-forms)：Edge Delivery Services Forms では、フォーム固有のカスタム関数スクリプトがサポートされ、再利用可能なロジックをより柔軟に管理できるようになりました。
   * [カスタム関数の静的読み込み](/help/edge/docs/forms/universal-editor/rule-editor-universal-editor.md#static-imports-for-custom-functions)：ユニバーサルエディターのルールエディターで静的読み込みがサポートされ、開発者は複数のフォームをまたいで関数を整理、共有、再利用できるようになりました。

### AEM Forms の早期導入機能

* [&#x200B; 手書き署名コンポーネント &#x200B;](https://experienceleague.adobe.com/ja/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/scribble-signature)：手書き署名コンポーネントを使用して、契約書フォームなどのフォームにユーザーの署名を追加できるようになりました。 コンポーネントを使用すると、ユーザーはマウス、スタイラス、タッチスクリーンを使用してフォーム内に直接署名を入力できます。
* [&#x200B; ルールエディターでの直接 API 統合 &#x200B;](/help/forms/api-integration-in-rule-editor.md)：アダプティブFormsでは、フォームデータモデルを必要とせずに、ビジュアルルールエディターでの直接 API 統合をサポートするようになりました。 作成者は、URL または cURL 読み込みを使用して API を設定し、入力／出力パラメーターをマッピングし、認証を使用して安全な呼び出しを行うことができます。

<!--
**Forms Optimization opportunities**

Forms Optimization uses AI to analyze your forms and suggest improvements for better performance. It highlights forms with low engagement, flags accessibility issues, and generates AI-powered variations to help increase conversion rates and compliance with WCAG standards.

>[!VIDEO](https://video.tv.adobe.com/v/3469472/) 

Key optimization opportunities include:

* Increasing visibility for forms with low views
* Improving completion rates for forms with low conversions
* Addressing accessibility compliance issues
* Streamlining navigation to enhance user experience

With Forms Optimization, you get automated, data-driven recommendations and variations, making it easier to boost engagement and ensure your forms are effective and inclusive. -->

## [!DNL Experience Manager] as a [!DNL Cloud Service] の基盤 {#foundation}

### JavaScript コンパイルの更新 {#javascript-compilation}

デフォルトのクライアントサイドライブラリ（clientlibs）の JavaScript コンパイルでは、ECMASCRIPT5 の代わりに、ECMASCRIPT_2018 をターゲットにするようになりました。これまでは上書き可能でしたが、今回の更新により、パフォーマンスの向上、最新の JavaScript 構文および機能がデフォルトで有効になります。

### 今後の Java API の非推奨（廃止予定） {#java-api-deprecation}

一部の非推奨（廃止予定）API は、8月31日（PT）の削除をターゲットにしているので、参照できなくなります。9月上旬には、API の使用が検出されるとアクションセンター通知が送信され、9月25日（PT）以降は、使用を削除することの重要性を強調する通知が Cloud Manager ビルド中に表示されます。詳しくは、[非推奨（廃止予定）に関する記事](/help/release-notes/deprecated-removed-features.md#aem-apis)を参照してください。便宜上、これらの API を次に示します。

<details>
  <summary>展開して Java API の非推奨（廃止予定）について確認</summary>

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
</details>

<!--
OSGi properties:

* `org.apache.sling.commons.log.LogManager` (all properties)
* `org.apache.sling.commons.log.LogManager.factory.config` (`org.apache.sling.commons.log.file`, `org.apache.sling.commons.log.pattern`)
* 

-->

### Java 11 ランタイムのデプロイメント {#java11-runtime-deprecation}

*Java 11 ランタイム* は廃止となり、大半の環境はよりパフォーマンスの高い **Java 21 ランタイム**&#x200B;にアップグレードされています。

サポートされていない依存関係が原因で環境をアップグレードできなかった場合 ([Java 21 ランタイム要件](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/build-environment-details.md#runtime-requirements)を参照) は、次の具体的な手順を記載したメールが Adobeから届いているはずです。**2025年10月1日（PT）**&#x200B;までに必要な更新がすべて完了していることを確認してください。これにより、中断することなく環境をアップグレードできます。

注：ランタイムバージョンは、コードのビルドバージョンとは別のものです。 Java 21 を使用してビルドすることをお勧めしますが、Java 11 ビルドは引き続きサポートされています。 Java 11 ビルドの廃止に関する通知は、今後共有される予定です。

### AEM Java ログ設定ポリシーの適用 {#logconfig-policy}

4 月のリリースノートに記載されているように、AEMの Java ログは、すべてのお客様の環境で信頼性の高い監視を確実に行うために、標準に従う必要があります。 ログ形式、出力ファイル、デフォルトログレベルの変更といったカスタムログ設定は、サポートされなくなりました。 ログはデフォルトファイルにダイレクトされ続け、AEM 製品コードのデフォルトログレベルは保持される必要があります。 詳しくは、[ログに関する記事](/help/implementing/developing/introduction/logging.md#configuration-loggers)を参照してください。

**9月25日（PT）**&#x200B;から、サポートされていないカスタムログの上書きは無視されるようになります。Adobe の分析によると、ほとんどのお客様は影響を受けることはありません。現在の設定が影響を受ける可能性があるお客様にはご連絡済みです。

カスタムログ動作に依存するダウンストリームプロセスを確認し、更新してください。 例：

* ログ転送システムでカスタムログ形式が想定されている場合は、取り込みルールを調整する必要がある可能性があります。
* 以前にログレベルを変更してログの冗長性を削減したことがある場合は、デフォルトレベルに戻すとログのボリュームが増える可能性があることに注意してください。

### Edge コンピューティング（Beta プログラム） {#edge-computing}

Edge コンピューティングを使用すると、CDN レイヤーで JavaScript を実行し、データ処理をエンドユーザーに近づけることができます。 これにより待ち時間が短縮され、エッジでレスポンシブな動的エクスペリエンスが実現します。

一般的なユースケースを次に示します。

* コンテンツへのアクセスを許可する前に、ID プロバイダーを使用してユーザーを認証する
* 位置情報、デバイスタイプまたはユーザー属性に基づくコンテンツのパーソナライズ
* CDN と接触チャネルの間のミドルウェアとして機能させる
* サードパーティの API からの応答をブラウザーに配信する前に再フォーマットする（および複数の API 応答を集計する）
* 様々なバックエンドからステッチされたコンテンツを使用し、サーバーレンダリングされた HTML をエッジで作成および提供
* ChatGPT や Claude などの LLM がカスタムツールにアクセスできるように MCP サーバーを公開する

AEM パブリッシュ配信またはライブ実稼動サイトのEdge Delivery Services プロジェクトで利用できる機会の数は限られています。 参加に関心がある場合や、詳細を確認したい場合は、ユースケースの簡単な説明を添えて [aemcs-edgecompute-feedback@adobe.com](mailto:aemcs-edgecompute-feedback@adobe.com)までメールでご連絡ください。

### Edge Delivery Servicesの CDN 設定 (Beta プログラム) {#cdn-eds-beta}

Adobe が管理する CDN では、[設定パイプラインの記事](/help/operations/config-pipeline.md#configurations)で説明されているように、柔軟な設定オプションが提供されます。

ベータ版では、CDN オリジンセレクター、応答とリクエストの変換、CDN ログ転送などの機能に対して設定パイプラインをデプロイします。ユースケースについて詳しくは、[aemcs-cdn-config-adopter@adobe.com](mailto:aemcs-cdn-config-adopter@adobe.com) にお問い合わせください。

### RDE のスナップショット（Alpha プログラム） {#rde-snapshot-program}

Alpha では、高速開発環境（RDE）で、コードとコンテンツの現在の状態のスナップショットを取得し、後で復元できる機能がサポートされるようになりました。 これは、元に戻す必要がある場合のあるコードを同期する場合や、異なる機能の開発を切り替える場合に役立つことがあります。 また、テストの既知の開始点として、可変コンテンツのみを復元することもできます。

この機能に関するフィードバックをお送りいただく場合は、[aemcs-rde-support@adobe.com](mailto:aemcs-rde-support@adobe.com) までメールでお問い合わせください。

### その他の宛先への AEM ログ転送 (Beta プログラム) {#log-forwarding-beta}

ログは Cloud Manager からダウンロードできますが、多くの組織では、これらのログを優先されるログの宛先にストリーミングすると役立ちます。 AEM では、Azure Blob Storage、Datadog、HTTPS、Elasticsearch (および OpenSearch)、Splunk への AEM および CDN ログ転送をサポートしています。 この機能は、セルフサービス方式で設定し、設定パイプラインを使用してデプロイします。

Beta では、Amazon S3、Sumo Logic、Dynatrace および独自のNew Relic アカウント（Adobe が提供するアカウントではありません）に AEM ログを転送できます。 AEM ログ (Apache／Dispatcher など) はサポートされていますが、CDN ログはサポートされていません。 アクセスについて詳しくは、[aemcs-logforwarding-beta@adobe.com](mailto:aemcs-logforwarding-beta@adobe.com) までメールで送信してください。

詳しくは、[ログ転送ドキュメント](/help/implementing/developing/introduction/log-forwarding.md)を参照してください。

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
