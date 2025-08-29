---
title: ' [!DNL Adobe Experience Manager] as a Cloud Service の最新のリリースノート。'
description: ' [!DNL Adobe Experience Manager]  as a Cloud Service の最新のリリースノート。'
mini-toc-levels: 1
exl-id: a2d56721-502c-4f4e-9b72-5ca790df75c5
feature: Release Information
role: Admin
source-git-commit: 4a1dcc9f069bdf8f5cf8abaa3f784f5ebd4922cc
workflow-type: tm+mt
source-wordcount: '1903'
ht-degree: 47%

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

[!DNL Adobe Experience Manager] as a [!DNL Cloud Service] の最新の機能リリース（2025.8.0）のリリース日は 2025年8月28日（PT）です。次回の機能リリース（2025.9.0）は、2025年9月25日（PT）に予定されています。

## メンテナンスリリースノート {#maintenance}

最新のメンテナンスリリースノートについては、[こちら](/help/release-notes/maintenance/latest.md)をご覧ください。

<!-- 

## Release Video {#release-video}

Have a look at the July 2025 Release Overview video for a summary of the features added in the 2025.7.0 release:

>[!VIDEO](https://video.tv.adobe.com/v/3440920?quality=12)

-->

## Experience Hub {#experience-hub}

[Experience Hub](/help/experience-hub.md) は、すべてのAEM機能にアクセスするための一元的な出発点となります。 ユーザーのペルソナと使用可能なライセンスに基づいてパーソナライズされるため、各ユーザーは結果を効率的に達成できます。

## AEMの AI アシスタント {#AI-assistant}

AEM用 [AI アシスタント ](/help/implementing/cloud-manager/ai-assistant-in-aem.md) は、AEM製品に関する質問に即座に回答し（** すべてのユーザーが利用できます）、サポートチケットの作成を自動化するように設計された対話型インターフェイスを提供します（*管理者をサポートする場合に利用できます*）。 AEMに直接埋め込まれ、AEM Experience Hub、Cloud Managerおよびオーサー UI からアクセスできます。

## [!DNL Experience Manager Sites] as a [!DNL Cloud Service] {#sites}

### Experience Manager Sites の新機能 {#enhancements-sites}

* コンテンツフラグメント管理 UI では、コンテンツフラグメントのワークフローステータスと、選択したフラグメントの過去および現在実行中のワークフローの詳細情報を表示できるようになりました。
* 新しいコンテンツフラグメントエディターでコンテンツフラグメントを開くパフォーマンスは、パスではなく UUID を使用してフラグメントを開くことで、一般的なシナリオで 25% 向上しました。
* 参照フラグメントを使用してコンテンツフラグメントをコピーする際、参照フラグメントのコピーが、親フラグメントコピーと同じ場所に保存されるようになりました。
* フォルダー設定でカスタムワークスペースを設定して、コンテンツフラグメントをAdobe Targetの設定済みワークスペースに書き出すことができるようになりました。

## [!DNL Experience Manager Assets] as a [!DNL Cloud Service] {#assets}

### コンテンツハブの新機能 {#new-features-content-hub}

**フィルタープロパティを使用した一括検索**

Content Hubを使用すると、必要なアセットをより迅速に見つけることができます。 新しい一括検索機能を使用すると、任意のフィルタープロパティに複数の値を区切り文字で区切って入力し（複数の SKU ID など）、一致するすべてのアセットを 1 回の検索で即座に取得できます。

### OpenAPI 機能を備えた Dynamic Media の新機能 {#new-features-dynamic-media-with-openapi}

**OpenAPI URL を使用した SEO に対応した DM**

OpenAPI を使用して DM でアセット配信用のバニティー URL を作成し、長いシステム生成 UUID を短い読み取り可能な識別子に置き換えます。 これにより、リンクが SEO に適し、ブランドやキャンペーンとより適切に連携するようになります。 バニティ URL は、既存のワークフローを中断することなく、実行時に元のアセット UUID に自動的に解決されます。

>[!NOTE]
>
>この機能は、9 月 10 日（PT）に限定提供（LA）機能として提供されます。 [Adobe カスタマーサポートケースを作成して送信する ](https://helpx.adobe.com/jp/enterprise/using/support-for-experience-cloud.html) ことで、のデプロイメントでケースを有効にすることができます。

## [!DNL Experience Manager Forms] as a [!DNL Cloud Service] {#forms}

* [ 日付と時刻の入力コンポーネント ](https://experienceleague.adobe.com/en/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/date-time-component)：日付と時刻のコンポーネントが使用できるようになり、カレンダーと時計のインターフェイスを使用して、またはサポートされている形式で手動で値を入力して、日付と時刻の両方を選択できるようになりました。
* [ ファイルのアップロードのエラー処理の強化 ](https://experienceleague.adobe.com/ja/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/file-attachment#basic-tab)：ファイル添付コンポーネントは、アップロードされたファイルタイプを許可リストと照合して自動的に検証するようになりました。 サポートされていない形式のファイルをユーザーがアップロードすると、フォームの送信中にエラーが表示されます。 また、このコンポーネントはファイルコンテンツをチェックして、そのタイプを検証するので、フォームの全体的なセキュリティが強化されます。
* [ カスタム送信アクションに対して指定されたエラー応答 ](/help/forms/custom-submit-action-troubleshooting.md)：カスタム送信アクションで未処理のエラーが発生した場合は、エラーコード 502 が返されます。 これは、問題がカスタム送信アクションに関連していることを識別するのに役立ち、デバッグを容易にします。
* [ レコードのドキュメントからの非表示フィールドの除外 ](/help/forms/generate-document-of-record-core-components.md#document-of-record-settings)：レコードのドキュメントから非表示フィールドを除外できるように、新しいプロパティが追加されました。 デフォルトでは、このオプションは選択されておらず、すべてのフォームフィールドに適用されます。

### AEM Formsのプレリリース機能

* [AFP レンディションの生成と同期 ](/help/forms/document-generation-afp-api.md): AEM Forms Communication API を使用して、XDP ファイルを AFP 形式に変換できるようになりました。 AFP は、大規模企業の印刷で広く使用されている高性能フォーマットです。
* **ルールエディターの機能強化**
   * [ 関数リスト内の Validate メソッド ](/help/forms/rule-editor-enhancements-use-cases.md#validate-method-in-function-list):validate メソッドと reset メソッドで、パネルレベル、フィールドレベル、フォームレベルでの実行がサポートされるようになりました。 以前は、フォームレベルでのみサポートされていました。
   * [ 最新のJavaScriptのサポート ](/help/forms/rule-editor-core-components-difference-tables.md):ECMAScript 2019 以降の機能がカスタム関数に対してサポートされ、より効率的なモジュール型で再利用可能なコードを記述できるようになりました
   * [ ルールエディターの「DoR をダウンロード」オプション ](/help/forms/rule-editor-enhancements-use-cases.md#downloaddor-as-ootb-fuction-in-rule-editor)：レコードのドキュメント（DoR）をダウンロードする機能がルールエディターの標準（OOTB）オプションとして追加されました。
     ![ レコードのドキュメント ](/help/forms/assets/document-of-record-rn.gif)
   * [ ルールエディターの動的変数 ](/help/forms/rule-editor-enhancements-use-cases.md#support-for-dynamic-variables-in-rules)：ルールエディターで動的（一時的）変数を使用して、条件とアクションをより柔軟に定義できるようになりました。 非表示のフィールドは、一時的な値を格納する必要がなくなりました。
   * [ カスタムイベントベースのルールのサポート ](/help/forms/rule-editor-enhancements-use-cases.md#custom-event-based-rules-support)：カスタムイベントと、それらのイベントに基づくトリガールールを定義できるようになりました。
   * [ コンテキスト対応の繰り返し可能なパネルルール ](/help/forms/rule-editor-enhancements-use-cases.md#context-based-rule-execution-for-repeatable-panels)：繰り返し可能なパネルでは、ルールが最後のパネルインスタンスのみに適用されるのではなく、コンテキストに基づいて実行されるようになりました。
   * [ パラメーターによってトリガーされるルール ](/help/forms/rule-editor-enhancements-use-cases.md#url-and-browser-parameter-based-rules-in-adaptive-forms)：ルールエディターで、クエリパラメーター、UTM パラメーターまたはブラウザーパラメーターに基づくルール実行がサポートされるようになりました。
   * [ フォーム固有のカスタム関数 ](/help/edge/docs/forms/universal-editor/rule-editor-universal-editor.md#organizing-custom-functions-across-different-forms):Edge Delivery Services Formsでは、フォーム固有のカスタム関数スクリプトがサポートされるようになり、再利用可能なロジックをより柔軟に管理できるようになりました。
   * [ カスタム関数の静的インポート ](/help/edge/docs/forms/universal-editor/rule-editor-universal-editor.md#static-imports-for-custom-functions)：ユニバーサルエディターのルールエディターで静的インポートがサポートされるようになり、開発者は関数を整理、共有、複数のフォームで再利用できるようになりました。

### AEM Forms の早期導入機能

* [ 手書き署名コンポーネント ](https://experienceleague.adobe.com/en/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/scribble-signature)：手書き署名コンポーネントを使用して、契約書フォームなどのフォームにユーザーの署名を追加できるようになりました。 このコンポーネントを使用すると、ユーザーはマウス、スタイラスまたはタッチスクリーンを使用してフォーム内に直接署名を描画できます。
* [ ルールエディターでの直接 API 統合 ](/help/forms/api-integration-in-rule-editor.md)：アダプティブFormsでは、フォームデータモデルを必要とせずに、ビジュアルルールエディターでの直接 API 統合をサポートするようになりました。 作成者は、URL または cURL インポートを使用して API を設定し、入力/出力パラメーターをマッピングし、認証で安全な呼び出しを行うことができます。

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

デフォルトのクライアントサイドライブラリ（clientlibs）JavaScriptのコンパイルは、ECMASCRIPT5 ではなく ECMASCRIPT_2018 をターゲットとするようになりました。 この更新は以前は上書きできますが、デフォルトではパフォーマンスの向上、最新のJavaScript構文および機能が有効になっています。

### 今後の Java API の廃止 {#java-api-deprecation}

一部の非推奨 API は、8 月 31 日の削除をターゲットにしているので、参照できなくなりました。 API の使用が検出された場合、9 月上旬にアクションセンターから通知が送信されます。また、9 月 25 日（PT）以降、Cloud Managerのビルド中に通知が表示され、使用を削除することが重要になります。 詳しくは、[ 非推奨の記事 ](/help/release-notes/deprecated-removed-features.md#aem-apis) を参照してください。ただし、便宜上、これらの API は次のとおりです。

<details>
  <summary>展開して Java API の非推奨（廃止予定）を確認</summary>

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

サポートされていない依存関係が原因で環境をアップグレードできなかった場合 ([Java 21 ランタイム要件](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/build-environment-details.md#runtime-requirements)を参照) は、次の具体的な手順を記載したメールが Adobeから届いているはずです。**2025 年 10 月 1 日** までに必要な更新がすべて完了していることを確認してください。これにより、中断することなく環境をアップグレードできます。

注：ランタイムバージョンは、コードのビルドバージョンとは別のものです。Java 21 を使用してビルドすることをお勧めしますが、Java 11 ビルドは引き続きサポートされています。Java 11 ビルドの廃止に関する通知は、今後共有される予定です。

### AEM Java ログ設定ポリシーの適用 {#logconfig-policy}

4 月のリリースノートに記載されているように、AEMの Java ログは、すべてのお客様の環境で信頼性の高い監視を確実に行うために、標準に従う必要があります。ログ形式、出力ファイル、デフォルトログレベルの変更といったカスタムログ設定は、サポートされなくなりました。ログはデフォルトファイルにダイレクトされ続け、AEM 製品コードのデフォルトログレベルは保持される必要があります。 詳しくは、[ログに関する記事](/help/implementing/developing/introduction/logging.md#configuration-loggers)を参照してください。

**9 月 25 日** 以降、サポートされていないカスタムログの上書きは無視されます。 Adobe の分析によると、ほとんどのお客様は影響を受けることはありません。現在の設定が影響を受ける可能性があるお客様にはご連絡済みです。

カスタムログ動作に依存するダウンストリームプロセスを確認し、更新してください。例：

* ログ転送システムでカスタムログ形式が想定されている場合は、取り込みルールを調整する必要がある可能性があります。
* 以前にログレベルを変更してログの冗長性を削減したことがある場合は、デフォルトレベルに戻すとログのボリュームが増える可能性があることに注意してください。

### Edge Computing （Beta プログラム） {#edge-computing}

Edge コンピューティングを使用すると、CDN レイヤーで JavaScript を実行し、データ処理をエンドユーザーに近づけることができます。これにより待ち時間が短縮され、エッジでレスポンシブな動的エクスペリエンスが実現します。

一般的なユースケースを次に示します。

* コンテンツへのアクセスを許可する前に、ID プロバイダーを使用してユーザーを認証する
* 位置情報、デバイスタイプまたはユーザー属性に基づくコンテンツのパーソナライズ
* CDN と接触チャネルの間のミドルウェアとして機能させる
* ブラウザーに配信する前に、サードパーティ API からの応答を再フォーマットする（および複数の API 応答を集計する）
* 様々なバックエンドからステッチされたコンテンツを使用し、サーバーレンダリングされた HTML をエッジで作成および提供
* ChatGPT や Claude などの LLM がカスタムツールにアクセスできるように MCP サーバーを公開する

AEM パブリッシュ配信またはライブ実稼動サイトのEdge Delivery Services プロジェクトで利用できる機会の数は限られています。参加に関心がある場合や、詳細を確認したい場合は、ユースケースの簡単な説明を添えて [aemcs-edgecompute-feedback@adobe.com](mailto:aemcs-edgecompute-feedback@adobe.com)までメールでご連絡ください。

### Edge Delivery Servicesの CDN 設定 (Beta プログラム) {#cdn-eds-beta}

Adobe が管理する CDN では、[設定パイプラインの記事](/help/operations/config-pipeline.md#configurations)で説明されているように、柔軟な設定オプションが提供されます。

ベータ版では、CDN オリジンセレクター、応答およびリクエスト変換、CDN ログ転送などの機能に対する設定パイプラインをデプロイできます。 ユースケースについて詳しくは、[aemcs-cdn-config-adopter@adobe.com](mailto:aemcs-cdn-config-adopter@adobe.com) にお問い合わせください。

### RDE のスナップショット（Alpha プログラム） {#rde-snapshot-program}

Alpha では、高速開発環境（RDE）で、コードとコンテンツの現在の状態のスナップショットを取得し、後で復元できる機能がサポートされるようになりました。これは、元に戻す必要がある場合のあるコードを同期する場合や、異なる機能の開発を切り替える場合に役立つことがあります。また、テストの既知の開始点として、可変コンテンツのみを復元することもできます。

この機能に関するフィードバックをお送りいただく場合は、[aemcs-rde-support@adobe.com](mailto:aemcs-rde-support@adobe.com) までメールでお問い合わせください。

### その他の宛先への AEM ログ転送 (Beta プログラム) {#log-forwarding-beta}

ログは Cloud Manager からダウンロードできますが、多くの組織では、これらのログを優先されるログの宛先にストリーミングすると役立ちます。AEM では、Azure Blob Storage、Datadog、HTTPS、Elasticsearch (および OpenSearch)、Splunk への AEM および CDN ログ転送をサポートしています。この機能は、セルフサービス方式で設定し、設定パイプラインを使用してデプロイします。

Beta では、Amazon S3、Sumo Logic、Dynatrace および独自のNew Relic アカウント（Adobe が提供するアカウントではありません）に AEM ログを転送できます。AEM ログ (Apache／Dispatcher など) はサポートされていますが、CDN ログはサポートされていません。アクセスについて詳しくは、[aemcs-logforwarding-beta@adobe.com](mailto:aemcs-logforwarding-beta@adobe.com) までメールで送信してください。

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
