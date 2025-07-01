---
title: OpenAPI を備えた AEM コンテンツフラグメント配信
description: OpenAPI を活用した AEM コンテンツフラグメント配信についての詳細情報
feature: Headless, Content Fragments, Edge Delivery Services
role: Admin, Developer
exl-id: b298db37-1033-4849-bc12-7db29fb77777
source-git-commit: 28d0d6bdfd9e6f1c1483bed7c5e65df340e8b559
workflow-type: tm+mt
source-wordcount: '524'
ht-degree: 90%

---


# OpenAPI を備えた AEM コンテンツフラグメント配信 {#aem-content-fragment-delivery-with-openapi}

Adobe Experience Manager（AEM）as a Cloud Service では、コンテンツフラグメント配信用の AEM OpenAPI には次の特徴があります。

* JSON 形式の AEM コンテンツフラグメントのライブ配信用に最適化された OpenAPI です
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
>AEM as a Cloud Service で OpenAPI を使用したコンテンツフラグメント配信を有効にするには、まだ有効になっていないことを確認してから、「**OpenAPI を使用したコンテンツフラグメント配信を有効にする**」というタイトルで次の内容を指定してアドビサポートチケットを送信してください。
>
>* Cloud Service プログラム ID と環境 ID
>* コンテンツフラグメント配信 OpenAPI で解決するユースケースの詳細
>* アドビが対応する必要のあるすべての連絡先の詳細、およびリクエストやプロジェクトについて情報を保持（必要な場合）

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

OpenAPI を使用したコンテンツフラグメント配信では、アクティブな CDN キャッシュの無効化をサポートしています。つまり、コンテンツを更新または公開するたびに、対応する JSON OpenAPI 応答は Fastly へのソフトパージリクエストを通じて自動的に無効化されます。これにより、実際の CDN キャッシュの有効期間（`s-maxage`）に達する前に、JSON 出力に反映された変更を確認できます。

## 入手方法 {#availability}

OpenAPI を使用したコンテンツフラグメント配信は、プレビュー層とパブリッシュ層で使用できます。OpenAPI は、プレビューとライブ配信の両方に JSON 形式でコンテンツフラグメントを配信します。

OpenAPI を使用したコンテンツフラグメント配信をプレビューするには、次の操作を行います。

* プレビューへの公開
* IP 許可リストによるプレビューへのアクセスを有効にする
* プレビュー URL の取得

## CORS {#cors}

[CORS 許可オリジン](/help/headless/deployment/cross-origin-resource-sharing.md)は、API を呼び出すことができるオリジンを定義します。

Dispatcher 設定側で定義された CORS 許可されたオリジン（特に GraphQL 用）は、この API では考慮されません。

## API レート制限 {#api-rate-limits}

この API を使用すると、環境ごとに最大 200 リクエスト/秒のレートで新規リクエストを許可します。

この制限を超えると、API は 429 エラーの送信を開始します。 これらのエラーはクライアントアプリケーションで処理する必要があり、失敗したリクエストは指数バックオフの再試行後に再試行されます。

<!-- 
## Limitations {#limitations}
-->
