---
title: ' [!DNL Adobe Experience Manager]  as a Cloud Service 2025.7.0 リリースのリリースノート。'
description: ' [!DNL Adobe Experience Manager]  as a Cloud Service 2025.7.0 リリースのリリースノート。'
feature: Release Information
role: Admin
exl-id: b1d25db0-d4a8-4663-b7fe-2d7381e12567
source-git-commit: 76ccdf13f56d7020ef266bc54bebbcc6eff1067d
workflow-type: tm+mt
source-wordcount: '2273'
ht-degree: 96%

---

# [!DNL Adobe Experience Manager] as a Cloud Service の 2025.7.0 リリースノート {#release-notes}

以下の節では、[!DNL Experience Manager] as a Cloud Service の 2025.7.0 バージョンの機能リリースノートの概要について説明します。

>[!NOTE]
>
>ここから、以前のバージョン（例えば、2023年、2024年）のリリースノートに移動できます。
>
>[!DNL Experience Manager] as a Cloud Service の今後の機能のアクティベーションについての詳細は、[Experience Manager リリースロードマップ](https://experienceleague.adobe.com/ja/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap)をご覧ください。

>[!NOTE]
>
>Experience Cloud リリースノートの更新に関するメール通知を毎月受信するには、[アドビ製品アップデートの優先通知](https://www.adobe.com/subscription/priority-product-update.html)を購読してください。

## リリース日 {#release-date}

[!DNL Adobe Experience Manager] as a [!DNL Cloud Service] の最新の機能リリース（2025.7.0）のリリース日は 2025年8月7日（PT）です。 次回の機能リリース（2025.8.0）は、2025年8月28日（PT）に予定されています。

## メンテナンスリリースノート {#maintenance}

最新のメンテナンスリリースノートについては、[こちら](/help/release-notes/maintenance/latest.md)をご覧ください。

<!-- 

## Release Video {#release-video}

Have a look at the July 2025 Release Overview video for a summary of the features added in the 2025.7.0 release:

>[!VIDEO](https://video.tv.adobe.com/v/3440920?quality=12)

-->

## [!DNL Experience Manager Sites] as a [!DNL Cloud Service] {#sites}

### Experience Manager Sites の新機能 {#enhancements-sites}

* コンテンツフラグメントと参照フラグメント（子フラグメント）を 1 回の操作でコピーできるようになりました。 これにより、既存のコンテンツフラグメント構造を再利用して、新しいコンテンツを作成できます。
* コンテンツフラグメント管理 UI では、コンテンツフラグメントのワークフローステータスと、選択したフラグメントの過去および現在実行中のワークフローの詳細情報を表示できるようになりました。
* ライブコピーのソースページの名前を変更または移動すると、それに応じて名前を変更または移動したライブコピーページの再公開がトリガーされるようになりました。

## [!DNL Experience Manager Assets] as a [!DNL Cloud Service] {#assets}

**Dynamic Media テンプレートへのシェイプの追加**

Experience Manager Assets の [Dynamic Media テンプレートにシェイプレイヤーを追加](/help/assets/dynamic-media/dynamic-media-templates.md#add-shapes-to-the-canvas)できるようになりました。 画像レイヤーやテキストレイヤーと同様に、シェイプレイヤーは、テンプレート URL 経由でリアルタイム更新用のパラメーターをサポートしています。 また、テンプレート内のシェイプに CTA（コールトゥアクション）リンクを含めることもできます。

![Dynamic Media テンプレートへのシェイプの追加](/help/assets/assets/enable-uniform-radius-shape.png)

**AI 生成のメタデータの機能強化**

AEM Assets では、アセットの参照ページの[カード表示またはリスト表示でのアセットタイトルの表示を設定](/help/assets/smart-tags.md#configure-ai-generated-titles)できるようになりました。 自分で定義したアセットタイトル、AI を使用して生成されたタイトルを表示するか、アセットに既存のタイトルがない場合にのみ AI が生成されたタイトルを使用するかを選択できます。

![AI 生成のタイトルの設定](/help/assets/assets/configure-title-ai-generated.png)

フォルダーレベルで AI 生成のメタデータを無効にすることも選択できるようになりました。

### コンテンツハブの新機能 {#new-features-content-hub}

**コンテンツハブでのブランディングの柔軟性の強化**

既存のパーソナライゼーション機能を基に、コンテンツハブでは、管理者がカスタムロゴ画像を追加して、デプロイメントをさらにカスタマイズできるようになりました。 また、バナー画像とロゴ画像の両方で TIFF ファイル形式のサポートが追加され、より柔軟なデザインが可能になります。

**タイトル付きリンクでよりスマートな共有**

共有リンクを生成する際に、アセットの詳細ビューからでも、1 つ以上のアセットを選択した後でも、タイトルを追加できるようになりました。 これにより、受信者は、特に複数の共有アセットを受け取った場合に、各リンクの目的を簡単に識別できます。

![プライベートリンクとパブリックリンク](/help/assets/assets/shared-link-for-assets.png)

**フィルターナビゲーションの改善**

コンテンツハブのフィルター内に「**すべて表示**」オプションが含まれるようになりました。これにより、ユーザーは、最大 10 個のファセットのみの現在の表示制限から使用可能なすべてのファセットとアセット数を表示できます。 各フィルター内の検索機能と並べ替え機能が強化され、アセットをより効率的に検出および管理するのがより簡単になります。

### AEM デスクトップアプリケーションリリース 3.0.0 {#desktop-app-release-3.0.0}

新しいファイルとフォルダーの自動アップロード、強化されたファイル操作、よりスマートなアセット検出、AEM とのシームレスな統合により、コンテンツ管理がより高速、明確、直感的になります。

機能の完全なリストについて詳しくは、[デスクトップアプリケーションリリースノート](https://experienceleague.adobe.com/ja/docs/experience-manager-desktop-app/using/release-notes)を参照してください。

### OpenAPI 機能を備えた Dynamic Media の新機能 {#new-features-dynamic-media-with-openapi}

**公開前にアセットをプレビュー**

[!DNL Dynamic Media with OpenAPI capabilities] では、アセットを公開する前に、[!DNL AEM Sites] のオーサーページ内で直接アセットをプレビューできるようになりました。 プレビュー用ページを関係者と共有し、ビジュアルの品質やコンテキストへの適合性についてフィードバックを収集します。 レビューサイクルでは、公開用にアセットを最終決定する前に、複数のアセットバージョンを作成および管理できます。

**OpenAPI 画像リクエスト用の拡張スマートイメージング**

すべての OpenAPI 画像リクエストで、自動プロモーションとフォールバックロジックによるスマートイメージングを完全に活用できるようになりました。 この機能強化により、デバイスとネットワークの状態に応じて画像が最適化され、視覚的な品質を維持しながら、ページの読み込み速度が向上し、帯域幅の使用量が削減されます。


## [!DNL Experience Manager Forms] as a [!DNL Cloud Service] {#forms}

### AEM Forms の新機能 {#forms-new-features}

**アダプティブフォームとフォームフラグメント用のユニバーサルエディター**

[ユニバーサルエディター](/help/edge/docs/forms/universal-editor/overview-universal-editor-for-edge-delivery-services-for-forms.md)で、アダプティブフォームと再利用可能なフォームフラグメントの両方の作成がサポートされるようになりました。 作成者は、フォームの作成、送信アクションの設定、reCAPTCHA 検証の追加を、すべてシンプルなWYSIWYG オーサリング環境で視覚的に行えます。 この機能により、フォームの作成が迅速化され、一貫性が高まり、ススパムや自動化による悪用からの保護が強化されます。

![ユニバーサルエディター](/help/edge/docs/forms/universal-editor/assets/universal-editor.png){width=80%, align-center}


**Edge Delivery Services Forms 用のForms Submission Service**

詳しくは、[Forms Submission Service](/help/forms/forms-submission-service.md) をご覧ください。を使用すると、アダプティブフォームの送信データを、Google Sheets、Microsoft OneDrive、SharePointなどの一般的なスプレッドシートプラットフォームにシームレスに直接保存できます。この統合により、フォームデータを選択したスプレッドシートに直接送信できるため、手作業によるデータ転送が不要になり、エラーも減らせることでデータ管理が効率化されます。

主なメリットは次のとおりです。

* **直接統合：**&#x200B;フォームを設定して、データを指定したスプレッドシートに直接送信できるようにします。
* **カスタムデータマッピング：**&#x200B;フォームのフィールドを対応するスプレッドシートの列にマッピングし、整理された形で保存できるようにします。
* **アクセス制御：**&#x200B;既存のスプレッドシート権限を活用して、送信されたデータにアクセスしたり変更したりできるユーザーを管理します。

**アダプティブフォームから AFP レンディションの生成と同期**

[AFP Output Sync API](/help/forms/document-generation-afp-api.md) により、管理者やユーザーはアダプティブフォームから AFP（Advanced Function Presentation）出力を生成し、その出力を外部システムやストレージ場所と同期できるようになります。 AFP は印刷に最適化された高性能なドキュメント形式で、大規模なエンタープライズ環境でよく使用されます。

<!-- ### New pre-release features in AEM Forms {#forms-new-pre-release-features}

**Enhancements in Rule Editor**

* The `validate` method in the function list now supports validation at the panel, field, and form levels.
* Client-side custom function parsing now supports ES10+ JavaScript features and static imports.
* The button to download Document of Record (DoR) is now available as an out-of-the-box (OOTB) option in the rule editor.
* Rules now support the use of dynamic variables.
* Custom event-based rules are now supported.
* Repeatable panel rules are now executed based on context, rather than only on the last panel instance.
* Rules can now be triggered based on query parameters, UTM parameters, and browser parameters.
* Form-specific custom function scripts are now supported for Adaptive Forms in Edge Delivery Services.

 -->

### AEM Forms の新しい早期アクセス機能 {#forms-new-early-access-features}

AEM Forms 早期アクセスプログラムでは、最先端の革新機能にいち早くアクセスできるだけでなく、その開発に意見を反映させるユニークな機会も提供されます。

これらのリリースノートでは、現在のリリースで提供されるイノベーションのリストを示します。早期アクセスプログラムで利用可能なイノベーションの完全なリストについて詳しくは、[AEM Forms 早期アクセスプログラムのドキュメント](/help/forms/early-access-ea-features.md)を参照してください。


<!-- **Forms Optimization opportunities**

Forms Optimization uses AI to analyze your forms and suggest improvements for better performance. It highlights forms with low engagement, flags accessibility issues, and generates AI-powered variations to help increase conversion rates and compliance with WCAG standards.

>[!VIDEO](https://video.tv.adobe.com/v/3469472/) 

Key optimization opportunities include:

* Increasing visibility for forms with low views
* Improving completion rates for forms with low conversions
* Addressing accessibility compliance issues
* Streamlining navigation to enhance user experience

With Forms Optimization, you get automated, data-driven recommendations and variations, making it easier to boost engagement and ensure your forms are effective and inclusive. -->

**インタラクティブなコミュニケーションエディター用のルールエディター**

直感的なポイント＆クリックのインターフェイスを使って、ドキュメント内で動的かつデータ駆動型のアクションを直接構築できます。 コードを記述することなく、条件付きロジックの定義、ワークフローの自動化、コンテンツのパーソナライズを簡単に行えます。

**カスタムコンポーネント用の AEM Forms Scaffolder CLI**

>[!VIDEO]（https://video.tv.adobe.com/v/3470514/aem-forms scaffolding-aem-custom component generator-aem-forms cli-aem-forms custom component-aem-forms development tool）

この CLI ツールを使用して、AEM Forms Edge Delivery Services の開発を加速できます。 カスタムコンポーネント開発をすぐに開始するためのコードと接続設定を瞬時に生成できます — 定型コード不要で手間もかかりません。

**動的フォームデータ用 API 統合ツール**

API 統合ツールにより、フォーム作成者は、ユーザーの操作に応じて外部の REST API から自動でデータを取得し入力する、動的でインテリジェントなフォームを作成できます。 このコードなしの統合機能は、静的フォームをレスポンシブなデータ収集インターフェイスに変換します。

## [!DNL Experience Manager] as a [!DNL Cloud Service] の基盤 {#foundation}

### 権限管理のノードビュー {#node-view}

AEM では、ノードビュー権限管理が導入されています。 主な機能は従来の UI と同じですが、よりユーザーフレンドリーで効率的です。 詳しくは、[廃止に関する記事](/help/security/touch-ui-principal-view.md)を参照してください。

### 更新された非推奨プロセス {#updated-deprecation-process}

Adobe は、パフォーマンス、セキュリティ、価値に関する標準を満たすように、機能、ライブラリ、API および設定を定期的に見直しています。 機能がこれらの標準を満たさなくなった場合は廃止とマークされ、指定した削除日までに使用が停止されます。 この日付までに、新しいビルドを進めたりデプロイしたりする前に、お客様にメール通知を届けたり、Cloud Managerで実行する必要があるアクションをお知らせしたりします。 必要な対策を講じないと、AEM の新しいバージョンにアップグレードできなくなる可能性があり、セキュリティ、パフォーマンス、信頼性、可用性に関する影響が潜在します。

詳しくは、[廃止に関する記事](/help/release-notes/deprecated-removed-features.md)を参照してください。

#### 削除日近くの廃止予定の Java API と OSGi の設定 {#deprecated-near-removals}

以下のリストを展開して、使用できなくなった廃止予定の API と OSGi 設定を確認します。 削除のタイムラインなどの詳細については、廃止に関するの記事を参照してください。

<details>
  <summary>展開して廃止について確認</summary>

Java API

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

OSGi プロパティ：

* `org.apache.sling.commons.log.LogManager` (すべてのプロパティ)
* `org.apache.sling.commons.log.LogManager.factory.config` (`org.apache.sling.commons.log.file`、`org.apache.sling.commons.log.pattern`)

</details>

### Java 11 ランタイムのデプロイメント {#java11-runtime-deprecation}

**Java 11 ランタイム*&#x200B;は廃止となり、大半の環境はよりパフォーマンスの高い **Java 21 ランタイム**&#x200B;にアップグレードされています。

サポートされていない依存関係が原因で環境をアップグレードできなかった場合 ([Java 21 ランタイム要件](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/build-environment-details.md#runtime-requirements)を参照) は、次の具体的な手順を記載したメールが Adobeから届いているはずです。 **2025 年 8 月 28 日**&#x200B;までに必要な更新がすべて完了していることを確認してください。これにより、中断することなく環境をアップグレードできます。

注：ランタイムバージョンは、コードのビルドバージョンとは別のものです。 Java 21 を使用してビルドすることをお勧めしますが、Java 11 ビルドは引き続きサポートされています。 Java 11 ビルドの廃止に関する通知は、今後共有される予定です。

### AEM Java ログ設定ポリシーの適用 {#logconfig-policy}

4 月のリリースノートに記載されているように、AEMの Java ログは、すべてのお客様の環境で信頼性の高い監視を確実に行うために、標準に従う必要があります。 ログ形式、出力ファイル、デフォルトログレベルの変更といったカスタムログ設定は、サポートされなくなりました。 ログはデフォルトファイルにダイレクトされ続け、AEM 製品コードのデフォルトログレベルは保持される必要があります。 詳しくは、[ログに関する記事](/help/implementing/developing/introduction/logging.md#configuration-loggers)を参照してください。

**8 月下旬**&#x200B;から、サポートされていないカスタムログの上書きは無視されるようになります。 Adobe の分析によると、ほとんどのお客様は影響を受けることはありません。現在の設定が影響を受ける可能性があるお客様にはご連絡済みです。

カスタムログ動作に依存するダウンストリームプロセスを確認し、更新してください。 例：

* ログ転送システムでカスタムログ形式が想定されている場合は、取り込みルールを調整する必要がある可能性があります。
* 以前にログレベルを変更してログの冗長性を削減したことがある場合は、デフォルトレベルに戻すとログのボリュームが増える可能性があることに注意してください。

### 古いバージョンと監査ログのデフォルトのパージ {#mt-defaults}

現在、コンテンツバージョンおよび監査ログは、関連する&#x200B;*パージメンテナンスタスク*&#x200B;がデフォルトで無効になっているので、明示的に設定されない限り、データは削除されません。

ただし、リポジトリのパフォーマンスを最適化するために、今後の発表日にデフォルトでパージが有効になります。

詳しくは、[メンテナンスタスクに関する記事](/help/operations/maintenance.md#defaults)を参照してください。

#### コンテンツのバージョン {#mt-content}

* **新しい環境** （今後作成され、後で通知されます）:
   * 30 日より古いバージョンは定期的に削除されます。
   * 作成日に関係なく、最新のバージョンと現在のバージョンと共に過去 30 日間の最新の 5 つのバージョンが保持されます。

* **既存の環境** （この日付より前に作成）:
   * 7 年以上前のバージョンは定期的に削除されます。
   * 過去 7 年間のすべてのバージョンが保持されます。
   * このデフォルトの高いしきい値によって、最近のデータが意図せずに削除されるのを防ぎます。 ただし、リポジトリのパフォーマンスを最適化するには、小さい値を設定することをお勧めします。

* これらのデフォルトは、設定パイプラインを使用してデプロイされた YAML 設定を通じて変更できます。

#### 監査ログ {#mt-auditlogs}

* **新しい環境** （今後作成され、個別に通知されます）：
   * 7 日以上前のレプリケーション、DAM およびページ監査ログは、定期的に削除されます。
   * デフォルトでは、すべてのイベントがログに記録されます。

* **既存の環境** (この予定日より前に作成)：
   * 7 年以上経過したレプリケーション、DAM およびページ監査ログは、定期的に削除されます。
   * デフォルトでは、すべてのイベントがログに記録されます。
   * このデフォルトの高いしきい値によって、最近のデータが意図せずに削除されるのを防ぎます。 ただし、リポジトリのパフォーマンスを最適化するには、小さい値を設定することをお勧めします。

* これらのデフォルトは、設定パイプラインを使用してデプロイされた YAML 設定を通じて変更できます。

### Edge コンピューティング (Alpha プログラム) {#edge-computing}

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

Beta 版では、CDN オリジンセレクター、応答とリクエストの変換、CDN ログ転送などの機能に対して設定パイプラインをデプロイします。 ユースケースについて詳しくは、[aemcs-cdn-config-adopter@adobe.com](mailto:aemcs-cdn-config-adopter@adobe.com) にお問い合わせください。

### RDE のスナップショット（Alpha プログラム） {#rde-snapshot-beta}

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
