---
title: OpenAPI を使用したAEM コンテンツフラグメント配信
description: OpenAPI を使用した AEM コンテンツフラグメント配信について説明します
feature: Headless, Content Fragments, Edge Delivery Services
role: Admin, Developer
exl-id: b298db37-1033-4849-bc12-7db29fb77777
source-git-commit: 4f58a52c5ccc8178e768f9072e7b2047cbe3fb20
workflow-type: tm+mt
source-wordcount: '313'
ht-degree: 84%

---

# OpenAPI を使用したAEM コンテンツフラグメント配信 {#aem-content-fragment-delivery-with-openapi}

Adobe Experience Manager（AEM）as a Cloud Serviceで、コンテンツフラグメント配信用のAEM OpenAPI を使用すると、

* [AEM Edge Delivery Services](/help/edge/overview.md) 上の HTTP REST API で、コンテンツフラグメントから構造化コンテンツを JSON 形式で配信するように設計されています。
* アクティブコンテンツの無効化を可能にする最新の CDN 統合を提供します。
* コンテンツ配信（パフォーマンス、スケーラビリティ、CDN 統合、最適化された JSON 制御と出力）に焦点を合わせています。
* 参照されたフラグメントとアセットの JSON を改善する機能が含まれます。

この API には次の特徴があります。

* [AEM Assets HTTP API でのコンテンツフラグメントのサポート](/help/assets/content-fragments/assets-api-content-fragments.md)の後継です。

* [コンテンツフラグメントおよびコンテンツフラグメントモデルの OpenAPI](/help/headless/content-fragment-openapis.md) を補完し、コンテンツフラグメントおよびコンテンツフラグメントモデル（CRUD）を管理できます。

* [コンテンツフラグメントと共に使用する AEM GraphQL API](/help/headless/graphql-api/content-fragments.md) の代替となる HTTP REST です。

完全なドキュメントについては、[OpenAPI を使用したAEM コンテンツフラグメント配信 ](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/stable/contentfragments/delivery/) を参照してください。

>[!NOTE]
>
>使用可能な様々な API の概要と、関連する概念のいくつかの比較について詳しくは、[構造化コンテンツの配信と管理用の AEM API](/help/headless/apis-headless-and-content-fragments.md) を参照してください。

## キャッシュ {#caching}

AEM は AEM CDN Fastly と統合されます。つまり、パブリッシュ層で提供される JSON 応答は Fastly レベルでキャッシュされます。

応答は、事前定義されたキャッシュヘッダーに基づいてキャッシュされます（設定できません）。

* 応答は、ブラウザー／クライアントのキャッシュで 5 分間キャッシュされます。
   * `max-age`=`300`
* 応答は、CDN キャッシュで 1 時間キャッシュされます。
   * `s-maxage`=`3600`
* 新しいリクエストを再検証している間、最大 1 時間、古いコンテンツが提供される場合があります。
   * `stale-while-revalidate`=`3600`
* 古いコンテンツは、エラーにより最大 1 日間提供される場合があります。
   * `stale-on-error`=`86400`

AEM には、アクティブな CDN キャッシュ無効化機能も備わっています。つまり、コンテンツを更新または公開するたびに、対応する JSON OpenAPI 応答は Fastly へのソフトパージリクエストを通じて自動的に無効化されます。これにより、実際の CDN キャッシュの有効期間（`s-maxage`）に達する前に、JSON 出力に反映された変更を確認できます。
