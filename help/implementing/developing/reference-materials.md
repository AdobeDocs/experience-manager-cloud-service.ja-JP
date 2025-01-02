---
title: API リファレンス資料
description: AEM には、デジタルエクスペリエンスプロジェクトに使用できる広範で強力な API が用意されています。
exl-id: d4ef3040-5a0a-4149-9e99-09eda9605038
feature: Developing
role: Admin, Architect, Developer
source-git-commit: 4182374ea9d603ed53e75511d34fdfcf69829200
workflow-type: ht
source-wordcount: '660'
ht-degree: 100%

---

# API リファレンス資料 {#api-reference-materials}

Adobe Experience Manager（AEM）では、アプリケーション開発および AEM 拡張用の API を多数提供しています。AEM は、いくつかのオープンソーステクノロジーを基盤として構築されており、それらのテクノロジーも利用できます。

## AEM コア API {#core-aem-apis}

AEM の中核を成す API は次のとおりです。

| API | 説明 |
|---|---|
| [Adobe Experience Manager as a Cloud Service](https://www.adobe.io/experience-manager/reference-materials/cloud-service/javadoc/index.html) | 製品の抽象概念（ページ、アセット、ワークフローなど）。 |
| [Granite UI](https://helpx.adobe.com/jp/experience-manager/6-5/sites/developing/using/reference-materials/granite-ui/api/jcr_root/libs/granite/ui/index.html#) | アドビのオープン web スタック。様々な必須コンポーネントを提供します（6.5 Granite の資料が AEMaaCS に適用されます） |
| [Coral UI](https://opensource.adobe.com/coral-spectrum/documentation/) | アドビのクラウド UI 用のビジュアルスタイル。ユーザーエクスペリエンスの一貫性を保つように設計されています。 |

<!---
|Editor core JavaScript API reference|Provides all the base objects and concepts to support authoring of content resources|
--->

>[!NOTE]
>
>Experience Manager API の最新情報については、[Adobe Experience Manager as a Cloud Service API](https://developer.adobe.com/experience-cloud/experience-manager-apis/) も参照してください。

## その他のフレームワーク {#additional-apis}

AEM は、いくつかの追加オープンソース API を利用しています。

| API | 説明 |
|---|---|
| [Apache Sling](https://sling.apache.org/apidocs/sling11/) | Java コンテンツリポジトリー（JCR）を使用してコンテンツを保存および管理する Web フレームワーク |
| [Apache Jackrabbit Oak](https://jackrabbit.apache.org/oak/docs/oak_api/overview.html) | 最新のワールドクラス Web サイトの基盤として使用する、スケーラブルでパフォーマンスの高い階層型 Java コンテンツリポジトリー（JCR）の実装 |
| [Java コンテンツリポジトリー](https://www.adobe.io/experience-manager/reference-materials/spec/javax.jcr/javadocs/jcr-2.0/index.html) | JCR バージョン 2.0 の仕様 |
| [Apache Felix](https://felix.apache.org) | OSGi（Open Services Gateway イニシアチブ）フレームワークおよびサービスプラットフォームの実装 |

## API 環境設定のガイドライン {#guidelines}

AEM は、優先順に次の 4 つの主要な Java API セットに基づいて構築されています。

| 優先度 | API | 説明 |
|---|---|---|
| 1 | [Adobe Experience Manager as a Cloud Service](https://www.adobe.io/experience-manager/reference-materials/cloud-service/javadoc/index.html) | 製品の抽象概念（ページ、アセット、ワークフローなど）。 |
| 2 | [Apache Sling](https://sling.apache.org/apidocs/sling11/) | REST およびリソースベースの抽象概念（リソース、値マップ、HTTP リクエストなど）。 |
| 3 | [Apache Jackrabbit Oak](https://jackrabbit.apache.org/oak/docs/oak_api/overview.html) | データとコンテンツの抽象概念（ノード、プロパティ、セッションなど）。 |
| 4 | [Apache Felix](https://felix.apache.org/) | OSGi アプリケーションコンテナの抽象概念（サービスや（OSGi）コンポーネントなど）。 |

AEM が API を提供する場合は、それを Sling、JCR、OSGi よりも優先します。AEM が API を提供しない場合は、Sling を JCR や OSGi よりも優先します。

>[!TIP]
>
>これらのガイドラインについて詳しくは、[Java API のベストプラクティスについて](https://experienceleague.adobe.com/docs/experience-manager-learn/foundation/development/understand-java-api-best-practices.html?lang=ja)を参照してください。

## AEM 配信およびコンテンツ管理サービスと API {#delivery-apis}

AEM では、カスタマイズ可能なコンポーネントとコンテンツ配信オプションを提供しています。

| 機能 | 説明 |
|---|---|
| [コアコンポーネント](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html?lang=ja) | AEM で Web サイトの開発時間を短縮しメンテナンスコストを削減するための、標準化された Web コンテンツ管理（WCM）コンポーネント |
| [JSON エクスポーター](/help/implementing/developing/components/json-exporter.md) | 任意の AEM ページのコンテンツを JSON データモデル形式で配信します |
| [コンポーネントの JSON 書き出しの有効化](/help/implementing/developing/components/enabling-json-exporter.md) | モデラーフレームワークに基づいてコンポーネントコンテンツの JSON 書き出しを生成します |
| [コンテンツフラグメントおよびコンテンツフラグメントモデルの OpenAPI](/help/headless/content-fragment-openapis.md) | コンテンツフラグメントおよびコンテンツフラグメントモデルの OpenAPI |
| [コンテンツフラグメント配信用の AEM REST OpenAPI](/help/headless/aem-rest-openapi-content-fragment-delivery.md) | AEM Edge Delivery Services 上の HTTP REST API で、コンテンツフラグメントから構造化コンテンツを JSON 形式で配信するように設計されています。 |
| [コンテンツフラグメント GraphQL API](/help/headless/graphql-api/content-fragments.md) | ヘッドレス CMS 実装の JavaScript クライアントにコンテンツフラグメントを効率的に配信できるようになります |
|  |  |
| [Assets API](/help/assets/mac-api-assets.md) | バイナリ、メタデータ、レンディション、コメントなどのアセットに対して作成、読み出し、更新、削除（CRUD）操作を実行できるようになります。AEM Assets HTTP API を参照してください |
| [コンテンツフラグメント HTTP API](/help/assets/content-fragments/assets-api-content-fragments.md) | CRUD 操作を使用して HTTP API でコンテンツフラグメントのコンテンツに直接アクセスします |
| [コンテンツフラグメントアセット HTTP API](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/assets/admin/mac-api-assets.html?lang=ja) | サポートされている HTTP アセットリクエストの厳密な形式 |

>[!NOTE]
>
>使用可能な様々な API の概要と、関連する概念のいくつかの比較について詳しくは、[構造化コンテンツの配信と管理用の AEM API](/help/headless/apis-headless-and-content-fragments.md) を参照してください。

## SPA 固有の API {#spa-apis}

AEM 単一ページアプリケーション（SPA）エディター SDK フレームワークは特定の JavaScript API リファレンスを提供します。

| API | 説明 |
|---|---|
| [コンポーネントマッピング](https://www.npmjs.com/package/@adobe/aem-spa-component-mapping) | 単一ページアプリケーションがフロントエンドコンポーネントを Adobe Experience Manager リソースタイプ（AEM コンポーネント）にマッピングする手段を提供します |
| [ページモデルマネージャー](https://www.npmjs.com/package/@adobe/aem-spa-page-model-manager) | Adobe Experience Manager エディターと Adobe Experience Manager 単一ページアプリケーション（SPA）エディターの間のインタープリター |
| [React 編集可能コンポーネント](https://www.npmjs.com/package/@adobe/aem-react-editable-components) | Adobe Experience Manager サイトエディターを導入するための React コンポーネントと統合レイヤーを提供します |
| [Angular 編集可能コンポーネント](https://www.npmjs.com/package/@adobe/aem-angular-editable-components) | Adobe Experience Manager サイトエディターを導入するための Angular コンポーネントと統合レイヤーを提供します |

>[!TIP]
>
>単一ページアプリケーションの詳細については、[SPA の概要およびガイド](/help/implementing/developing/hybrid/introduction.md)を参照してください。
