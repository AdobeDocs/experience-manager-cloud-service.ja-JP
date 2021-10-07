---
title: API リファレンス資料
description: AEMには、デジタルエクスペリエンスプロジェクトに活用できる、広範で強力な API があります。
exl-id: d4ef3040-5a0a-4149-9e99-09eda9605038
source-git-commit: 08559417c8047c592f2db54321afe68836b75bd1
workflow-type: tm+mt
source-wordcount: '664'
ht-degree: 30%

---

# API リファレンス資料 {#api-reference-materials}

Adobe Experience Manager(AEM) は、アプリケーションの開発とAEMの拡張に多くの API を提供します。 AEMは、様々なオープンソーステクノロジーを基盤として構築されており、利用することもできます。

## AEM Core API {#core-aem-apis}

以下の API はAEMの中核です。

| API | 説明 |
|---|---|
| [Adobe Experience Manager as a Cloud Service](https://docs.adobe.com/content/help/ja-JP/experience-manager-cloud-service-javadoc/index.html) | ページ、アセット、ワークフローなどの製品の抽象概念 |
| [Granite UI](https://helpx.adobe.com/jp/experience-manager/6-5/sites/developing/using/reference-materials/granite-ui/api/jcr_root/libs/granite/ui/index.html#) | Adobeのオープン Web スタック。様々な必須コンポーネントを提供（6.5 Granite マテリアルは AEMaaCS に適用されます） |
| [Coral UI](https://opensource.adobe.com/coral-spectrum/documentation/) | ユーザーエクスペリエンスの一貫性を提供する、クラウド UI 用のAdobeスタイル |

<!---
|Editor core JavaScript API reference|Provides all the base objects and concepts to support authoring of content resources|
--->

## その他のフレームワーク {#additional-apis}

AEMは、追加のオープンソース API を多数利用しています。

| API | 説明 |
|---|---|
| [Apache Sling](https://sling.apache.org/apidocs/sling11/) | Java コンテンツリポジトリ (JCR) を使用してコンテンツを保存および管理する Web フレームワーク |
| [Apache Jackrabbit Oak](http://jackrabbit.apache.org/oak/docs/oak_api/overview.html) | 最新の世界クラスの Web サイトの基盤として使用する、拡張性とパフォーマンスに優れた階層 Java Content Repository(JCR) の実装 |
| [Java コンテンツリポジトリー](https://www.adobe.io/experience-manager/reference-materials/spec/javax.jcr/javadocs/jcr-2.0/index.html) | JCR バージョン 2.0 の仕様 |
| [Apache Felix](https://felix.apache.org) | Open Services Gateway イニシアティブ (OSGi) フレームワークおよびサービスプラットフォームの実装 |

## API 環境設定のガイドライン {#guidelines}

AEM は、優先順に次の 4 つの主要な Java API セットに基づいて構築されています。

| 優先度 | API | 説明 |
|---|---|---|
| 1 | [Adobe Experience Manager as a Cloud Service](https://docs.adobe.com/content/help/en/experience-manager-cloud-service-javadoc/index.html) | ページ、アセット、ワークフローなどの製品の抽象概念 |
| 2 | [Apache Sling](https://sling.apache.org/apidocs/sling11/) | リソース、値マップ、HTTP 要求など、REST およびリソースベースの抽象概念。 |
| 3 | [Apache Jackrabbit Oak](http://jackrabbit.apache.org/oak/docs/oak_api/overview.html) | ノード、プロパティ、セッションなどのデータとコンテンツの抽象化。 |
| 4 | [Apache Felix](https://felix.apache.org／) | サービスや (OSGi) コンポーネントなどの OSGi アプリケーションコンテナの抽象概念。 |

AEM が API を提供する場合は、それを Sling、JCR、OSGi よりも優先します。AEM が API を提供しない場合は、Sling を JCR や OSGi よりも優先します。

>[!TIP]
>
>これらのガイドラインについて詳しくは、[Java API のベストプラクティスについて](https://experienceleague.adobe.com/docs/experience-manager-learn/foundation/development/understand-java-api-best-practices.html?lang=ja)を参照してください。

## AEM Delivery および Content Management Services と API {#delivery-apis}

AEMは、カスタマイズ可能なコンポーネントとコンテンツ配信オプションを提供します。

| 機能 | 説明 |
|---|---|
| [コアコンポーネント](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html?lang=ja) | AEM向けの標準化された Web コンテンツ管理 (WCM) コンポーネントにより、Web サイトの開発時間を短縮し、メンテナンスコストを削減 |
| [JSON エクスポーター](/help/implementing/developing/components/json-exporter.md) | 任意のAEMページのコンテンツを JSON データモデル形式で配信する |
| [コンポーネントの JSON 書き出しの有効化](/help/implementing/developing/components/enabling-json-exporter.md) | モデラーフレームワークに基づいてコンポーネントコンテンツの JSON 書き出しを生成 |
| [Assets API](/help/assets/mac-api-assets.md) | バイナリ、メタデータ、レンディション、コメントなどのアセットに対して作成、読み取り、更新、削除 (CRUD) 操作を実行できます。 AEM Assets HTTP API を参照してください。 |
| [コンテンツフラグメント HTTP API](/help/assets/content-fragments/assets-api-content-fragments.md) | CRUD 操作を介して、HTTP API 経由でコンテンツフラグメントコンテンツに直接アクセスする |
| [コンテンツフラグメント GraphQL API](/help/assets/content-fragments/graphql-api-content-fragments.md) | ヘッドレス CMS 実装で JavaScript クライアントに対してコンテンツフラグメントを効率的に配信できるようにする |
| [コンテンツフラグメント Assets HTTP API](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/assets/admin/mac-api-assets.html?lang=ja) | サポートされる HTTP アセットリクエストの正確な形式 |

## SPA固有の API {#spa-apis}

AEM Single-Page Application(SPA)Editor SDK フレームワークは、特定の JavaScript API リファレンスを提供します。

| API | 説明 |
|---|---|
| [コンポーネントのマッピング](https://www.npmjs.com/package/@adobe/aem-spa-component-mapping) | シングルページアプリケーションがフロントエンドコンポーネントをAdobe Experience Managerリソースタイプ (AEM Components) にマッピングする方法を提供します |
| [ページモデルマネージャー](https://www.npmjs.com/package/@adobe/aem-spa-page-model-manager) | Adobe Experience Manager Editor とAdobe Experience Manager Single Page Application(SPA)Editor の間のインタープリター |
| [React 編集可能コンポーネント](https://www.npmjs.com/package/@adobe/aem-react-editable-components) | Adobe Experience Manager Site Editor の使用を開始するための React コンポーネントと統合レイヤーを提供します。 |
| [編集可能な Angular コンポーネント](https://www.npmjs.com/package/@adobe/aem-angular-editable-components) | Adobe Experience Managerサイトエディターの使用を開始するためのAngularコンポーネントと統合レイヤーを提供します。 |

>[!TIP]
>
>シングルページアプリケーションの詳細については、「[SPAの概要およびガイド ](/help/implementing/developing/hybrid/introduction.md)」を参照してください。
