---
title: コンテンツフラグメント配信用のAEM REST OpenAPI
description: コンテンツフラグメント配信用AEM REST OpenAPI について説明します
feature: Headless, Content Fragments, Edge Delivery Services
role: Admin, Developer
source-git-commit: d98aa9d206486022d465ca19c8888088562d56c3
workflow-type: tm+mt
source-wordcount: '346'
ht-degree: 0%

---


# コンテンツフラグメント配信用のAEM REST OpenAPI {#aem-rest-openapi-for-content-fragment-delivery}

>[!IMPORTANT]
>
>この API は、早期導入プログラムを通じて利用できます。
>
>ステータスと、関心のあるユーザーへの適用方法を確認するには、[ リリースノート ](/help/release-notes/release-notes-cloud/release-notes-current.md) を確認してください。

Adobe Experience Manager（AEM）as a Cloud Serviceでは、コンテンツフラグメント配信用のAEM REST OpenAPI は次のようになります。

* は [AEM Edge Delivery Services](/help/edge/overview.md) 上の HTTP REST API であり、JSON 形式でコンテンツフラグメントから構造化コンテンツを配信するように設計されています
* は、アクティブコンテンツの無効化を可能にする最新の CDN 統合を提供します
* コンテンツ配信（パフォーマンス、スケーラビリティ、CDN 統合、最適化された JSON 制御および出力）に重点を置いています
* には、参照されるフラグメントとアセットの JSON を改善する機能が含まれます

この API:

* は、[AEM Assets HTTP API でのコンテンツフラグメントのサポート ](/help/assets/content-fragments/assets-api-content-fragments.md) の後継です。

* [ コンテンツフラグメントおよびコンテンツフラグメントモデルの OpenAPI](/help/headless/content-fragment-openapis.md) を補完し、コンテンツフラグメントおよびコンテンツフラグメントモデル（CRUD）を管理できるようにします

* は、コンテンツフラグメントで使用する、[AEM GraphQL API の代わりの HTTP REST です ](/help/headless/graphql-api/content-fragments.md)

完全なドキュメントについては、[AEM Sites API スキーマ – コンテンツフラグメント配信 API （2024.07 – 試行用） ](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/experimental/sites/delivery/) を参照してください。

>[!NOTE]
>
>使用可能な様々な API の概要および関連する概念の一部の比較については ](/help/headless/apis-headless-and-content-fragments.md)[ 構造化コンテンツ配信および管理用のAEM API} を参照してください。

## キャッシュ {#caching}

AEMはAEM CDN Fastly と統合されています。 つまり、パブリッシュ層で提供される JSON 応答は、Fastly レベルでキャッシュされます。

その後、事前定義されたキャッシュヘッダーに基づいて、応答がキャッシュされます（設定できません）。

* 応答は、ブラウザー/クライアントキャッシュに 5 分間キャッシュされます
   * `max-age`=`300`
* 応答は、CDN キャッシュで 1 時間キャッシュされます
   * `s-maxage`=`3600`
* 新しいリクエストを最大 1 時間再検証する際に、古いコンテンツを提供できる
   * `stale-while-revalidate`=`3600`
* 古いコンテンツは、エラーによって最大 1 日間提供されます
   * `stale-on-error`=`86400`

AEMには、アクティブな CDN キャッシュの無効化も付属しています。 つまり、コンテンツが更新または公開されるたびに、対応する JSON OpenAPI 応答が Fastly へのソフトパージリクエストを通じて自動的に無効化されます。 これにより、実際の CDN キャッシュページ（`s-maxage`）に達する前に、JSON 出力に反映された変更を確認できます。