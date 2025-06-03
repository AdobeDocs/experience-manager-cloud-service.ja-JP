---
title: OpenAPI を備えた AEM コンテンツフラグメント配信
description: OpenAPI を活用した AEM コンテンツフラグメント配信についての詳細情報
feature: Headless, Content Fragments, Edge Delivery Services
role: Admin, Developer
exl-id: b298db37-1033-4849-bc12-7db29fb77777
source-git-commit: 163964a7183996226b14f3c803afa4c5bd58f848
workflow-type: tm+mt
source-wordcount: '475'
ht-degree: 60%

---

# OpenAPI を備えた AEM コンテンツフラグメント配信 {#aem-content-fragment-delivery-with-openapi}

Adobe Experience Manager（AEM）as a Cloud Service では、コンテンツフラグメント配信用の AEM OpenAPI には次の特徴があります。

* は、JSON 形式のAEM コンテンツフラグメントのライブ配信用に最適化された OpenAPI です
* アクティブコンテンツの無効化を可能にする最新の CDN 統合を提供します。
* コンテンツ配信（パフォーマンス、スケーラビリティ、CDN 統合、最適化された JSON 制御と出力）に焦点を合わせています。
* 参照されたフラグメントとアセットの JSON を改善する機能が含まれます。

この API には次の特徴があります。

* [AEM Assets HTTP API でのコンテンツフラグメントのサポート](/help/assets/content-fragments/assets-api-content-fragments.md)の後継です。

* [コンテンツフラグメントおよびコンテンツフラグメントモデルの OpenAPI](/help/headless/content-fragment-openapis.md) を補完し、コンテンツフラグメントおよびコンテンツフラグメントモデル（CRUD）を管理できます。

* [コンテンツフラグメントと共に使用する AEM GraphQL API](/help/headless/graphql-api/content-fragments.md) の代替となる HTTP REST です。

詳細なドキュメントについて詳しくは、[OpenAPI を備えた AEM コンテンツフラグメント配信](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/stable/contentfragments/delivery/)を参照してください。

>[!NOTE]
>
>使用可能な様々な API の概要と、関連する概念のいくつかの比較について詳しくは、[構造化コンテンツの配信と管理用の AEM API](/help/headless/apis-headless-and-content-fragments.md) を参照してください。

>[!IMPORTANT]
>
>AEM as a Cloud Serviceで OpenAPI を使用したコンテンツフラグメント配信を有効にするには、まだ有効になっていないことを確認してから、「**OpenAPI を使用してコンテンツフラグメント配信を有効にする** というタイトルを持つAdobe サポートチケットを送信し、次を指定します。
>
>* Cloud Service プログラム ID と環境 ID
>* コンテンツフラグメント配信 OpenAPI で解決するユースケースの詳細
>* Adobeが対応する必要のあるすべての連絡先の詳細、およびリクエストやプロジェクトについて情報を保持（必要な場合）

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

OpenAPI を使用したコンテンツフラグメント配信では、アクティブな CDN キャッシュの無効化をサポートしています。 つまり、コンテンツを更新または公開するたびに、対応する JSON OpenAPI 応答は Fastly へのソフトパージリクエストを通じて自動的に無効化されます。これにより、実際の CDN キャッシュの有効期間（`s-maxage`）に達する前に、JSON 出力に反映された変更を確認できます。

## 入手方法 {#availability}

OpenAPI を使用したコンテンツフラグメント配信は、プレビュー層とパブリッシュ層で使用できます。 OpenAPI は、プレビューとライブ配信の両方に JSON 形式でコンテンツフラグメントを配信します。

OpenAPI を使用したコンテンツフラグメント配信をプレビューするには、次の操作を行います。

* プレビューに公開
* ip許可リストによるプレビューへのアクセスを有効にする
* プレビュー URL を取得

## CORS {#cors}

[CORS 許可オリジン ](/help/headless/deployment/cross-origin-resource-sharing.md) API を呼び出せるオリジンを定義します。

Dispatcher 設定側で定義された CORS 許可されたオリジン（特にGraphQL用）は、この API では考慮されません。

<!-- 
## API Rate Limits {#api-rate-limits}
-->

<!-- 
## Limitations {#limitations}
-->
