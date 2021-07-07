---
title: APIリファレンス資料
description: AEMには、デジタルエクスペリエンスプロジェクトに活用できる広範で強力なAPIが用意されています。
source-git-commit: f8d16e515de5ce740398d45a30038793fe021b69
workflow-type: tm+mt
source-wordcount: '665'
ht-degree: 30%

---

# APIリファレンス資料 {#api-reference-materials}

Adobe Experience Manager(AEM)は、アプリケーションの開発とAEMの拡張に多くのAPIを備えています。 AEMは、様々なオープンソーステクノロジーを基盤として構築されており、利用することもできます。

## AEM Core API {#core-aem-apis}

以下のAPIはAEMの中核となります。

| API | 説明 |
|---|---|
| [Adobe Experience Manager as aCloud Service](https://docs.adobe.com/content/help/ja-JP/experience-manager-cloud-service-javadoc/index.html) | ページ、アセット、ワークフローなどの製品の抽象概念 |
| [Granite UI](https://helpx.adobe.com/jp/experience-manager/6-5/sites/developing/using/reference-materials/granite-ui/api/jcr_root/libs/granite/ui/index.html#) | AdobeのオープンWebスタック。様々な必須コンポーネントを提供します（6.5 GraniteのマテリアルはAEMaaCSに適用されます）。 |
| [Coral UI](https://opensource.adobe.com/coral-spectrum/documentation/) | AdobeのクラウドUI用の視覚スタイル。ユーザーエクスペリエンスの一貫性を保つように設計されています。 |

<!---
|Editor core JavaScript API reference|Provides all the base objects and concepts to support authoring of content resources|
--->

## その他のフレームワーク {#additional-apis}

AEMは、追加のオープンソースAPIを利用しています。

| API | 説明 |
|---|---|
| [Apache Sling](https://sling.apache.org/apidocs/sling11/) | Javaコンテンツリポジトリ(JCR)を使用してコンテンツを保存および管理するWebフレームワーク |
| [Apache Jackrabbit Oak](http://jackrabbit.apache.org/oak/docs/oak_api/overview.html) | 最新の世界クラスのWebサイトの基盤として使用する、スケーラブルで高パフォーマンスの階層Java Content Repository(JCR)の実装 |
| [Java コンテンツリポジトリー](https://docs.adobe.com/content/docs/en/spec/javax.jcr/javadocs/jcr-2.0/index.html) | JCRバージョン2.0の仕様 |
| [Apache Felix](https://felix.apache.org) | Open Services Gatewayイニシアチブ(OSGi)フレームワークおよびサービスプラットフォームの実装 |

## API環境設定のガイドライン {#guidelines}

AEM は、優先順に次の 4 つの主要な Java API セットに基づいて構築されています。

| 優先度 | API | 説明 |
|---|---|---|
| 1 | [Adobe Experience Manager as aCloud Service](https://docs.adobe.com/content/help/en/experience-manager-cloud-service-javadoc/index.html) | ページ、アセット、ワークフローなどの製品の抽象概念 |
| 2 | [Apache Sling](https://sling.apache.org/apidocs/sling11/) | リソース、値マップ、HTTP要求など、RESTおよびリソースベースの抽象概念。 |
| 3 | [Apache Jackrabbit Oak](http://jackrabbit.apache.org/oak/docs/oak_api/overview.html) | ノード、プロパティ、セッションなどのデータとコンテンツの抽象化。 |
| 4 | [Apache Felix](https://felix.apache.org／) | サービスや(OSGi)コンポーネントなどのOSGiアプリケーションコンテナの抽象概念。 |

AEM が API を提供する場合は、それを Sling、JCR、OSGi よりも優先します。AEM が API を提供しない場合は、Sling を JCR や OSGi よりも優先します。

>[!TIP]
>
>これらのガイドラインについて詳しくは、[Java API のベストプラクティスについて](https://experienceleague.adobe.com/docs/experience-manager-learn/foundation/development/understand-java-api-best-practices.html?lang=ja)を参照してください。

## AEM配信およびコンテンツ管理サービスとAPI {#delivery-apis}

AEMは、カスタマイズ可能なコンポーネントとコンテンツ配信オプションを提供します。

| 機能 | 説明 |
|---|---|
| [コアコンポーネント](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html?lang=ja) | AEM向けの標準化されたWebコンテンツ管理(WCM)コンポーネントにより、Webサイトの開発時間を短縮し、メンテナンスコストを削減 |
| [JSON エクスポーター](/help/implementing/developing/components/json-exporter.md) | 任意のAEMページのコンテンツをJSONデータモデル形式で配信する |
| [コンポーネントの JSON 書き出しの有効化](/help/implementing/developing/components/enabling-json-exporter.md) | モデラーフレームワークに基づいてコンポーネントコンテンツのJSON書き出しを生成する |
| [Assets API](/help/assets/mac-api-assets.md) | バイナリ、メタデータ、レンディション、コメントなど、アセットに対する作成、読み取り、更新、削除(CRUD)操作を許可します。 AEM Assets HTTP API を参照してください。 |
| [コンテンツフラグメントHTTP API](/help/assets/content-fragments/assets-api-content-fragments.md) | CRUD操作を介して、HTTP API経由でコンテンツフラグメントコンテンツに直接アクセスする |
| [コンテンツフラグメントGraphQL API](/help/assets/content-fragments/graphql-api-content-fragments.md) | ヘッドレスCMS実装でJavaScriptクライアントに対してコンテンツフラグメントを効率的に配信可能 |
| [コンテンツフラグメントAssets HTTP API](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/assets/admin/mac-api-assets.html?lang=ja) | サポートされるHTTPアセットリクエストの正確な形式 |

## SPA固有のAPI {#spa-apis}

AEMシングルページアプリケーション(SPA)エディターSDKフレームワークは、特定のJavaScript API参照を提供します。

| API | 説明 |
|---|---|
| [コンポーネントのマッピング](https://www.npmjs.com/package/@adobe/aem-spa-component-mapping) | シングルページアプリケーションがフロントエンドコンポーネントをAdobe Experience Managerリソースタイプ(AEMコンポーネント)にマッピングする方法を提供します |
| [ページモデルマネージャー](https://www.npmjs.com/package/@adobe/aem-spa-page-model-manager) | Adobe Experience Manager EditorとAdobe Experience Manager Single Page Application (SPA) Editorの間のインタープリター |
| [React 編集可能コンポーネント](https://www.npmjs.com/package/@adobe/aem-react-editable-components) | Adobe Experience Manager Site Editorの使用を開始するためのReactコンポーネントと統合レイヤーを提供します。 |
| [編集可能な Angular コンポーネント](https://www.npmjs.com/package/@adobe/aem-angular-editable-components) | Adobe Experience Managerサイトエディターの使用を開始するためのAngularコンポーネントと統合レイヤーを提供します。 |

>[!TIP]
>
>シングルページアプリケーションの詳細については、「[SPAの概要とガイド](/help/implementing/developing/hybrid/introduction.md)」を参照してください。
