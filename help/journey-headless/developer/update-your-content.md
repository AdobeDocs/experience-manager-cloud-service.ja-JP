---
title: AEM API を使用してコンテンツをアップデートする方法
description: AEM ヘッドレスデベロッパージャーニーのこのパートでは、利用可能な API を使用してコンテンツフラグメントのコンテンツにアクセスし、アップデートする方法について説明します。
exl-id: 84120856-fd1d-40f7-8df4-73d4cdfcc43b
solution: Experience Manager
feature: Headless, Content Fragments, GraphQL API
role: Admin, Architect, Developer
source-git-commit: d8e4fdc4f79e40a43a6845ab083dc231444b9c99
workflow-type: tm+mt
source-wordcount: '580'
ht-degree: 78%

---

# AEM API を使用してコンテンツをアップデートする方法 {#update-your-content}

[AEM ヘッドレスデベロッパージャーニー](overview.md) のこのパートでは、使用可能な API を使用してコンテンツフラグメントのコンテンツにアクセスし、アップデートする方法について説明します。

## これまでの説明内容 {#story-so-far}

以前の AEM ヘッドレスジャーニードキュメント（「[AEM Delivery API を使用してコンテンツにアクセスする方法](access-your-content.md)」）では、AEM GraphQL API を介して AEM のヘッドレスコンテンツにアクセスする方法を説明したので、次ができるはずです。

* GraphQL について大まかなレベルで理解する
* AEM GraphQL API の仕組みを理解する
* 実用的なサンプルクエリを理解する

この記事は、これらの基本事項に基づいているので、利用可能な API を使用してAEMの既存のヘッドレスコンテンツを更新する方法を理解できます。

## 目的 {#objective}

* **オーディエンス**：経験者
* **目的**：コンテンツフラグメントのコンテンツにアクセスして更新できる API について説明します。

## コンテンツフラグメントと共に使用するAEM API {#aem-apis-for-use-with-content-fragments}

Adobe Experience Manager（AEM）as a Cloud Service では、コンテンツフラグメントからの構造化コンテンツ配信とコンテンツフラグメント管理の両方に対して複数の API を提供します。特定の API について詳しくは、個々のページを参照してください。

* コンテンツフラグメント配信用の AEM REST OpenAPI
   * この API は、AEM のコンテンツフラグメントから構造化コンテンツを配信する JSON 応答を作成します。
   * エンドポイントとしてコンテンツフラグメントへのパスを使用します。
   * この API は REST ベースです。
   * CDN 統合を含むコンテンツ配信用に最適化されています。
* コンテンツフラグメント配信用の AEM GraphQL API
   * この API はスキーマベースです。API スキーマは、コンテンツ構造を定義するコンテンツフラグメントモデルで表されます。
   * この API は GraphQL ベースです。
* コンテンツフラグメントおよびコンテンツフラグメントモデルの OpenAPI
   * これらの API は、構造化コンテンツ管理を目的としています。
   * それぞれの GET 演算子は、コンテンツ配信用に最適化されていません。
   * この API は REST ベースです。
* AEM Assets HTTP API での コンテンツフラグメントのサポート
   * AEM の構造化コンテンツ配信用の JSON 出力の元の API。
      * この API は堅牢で実証済みですが、*完全にハイドレート*&#x200B;された JSON 出力を提供しません。参照はパスとしてのみ出力されるので、さらにコンテンツを取得するには 2 番目の API リクエストが必要になります。
   * また、Assets HTTP API は、コンテンツフラグメントおよびコンテンツフラグメントモデル（CRUD）の管理にも使用できます。
   * この API は REST ベースです。
   * Assets HTTP API のコンテンツフラグメントサポートは、Edge Delivery Services JSON REST API によって継承されるので、今後、廃止される予定です。時間スケールは、まだ決定されていません。

## 次のステップ {#whats-next}

これで、ここでの AEM ヘッドレスデベロッパージャーニーは完了です。次ができるようになったはずです。

* 使用可能なAEM API について説明します。
* これらの API でコンテンツフラグメントがどのようにサポートされているかを理解する。

AEM ヘッドレスジャーニーを続けるには、[すべてをまとめる方法 - AEM ヘッドレスのアプリとコンテンツ](put-it-all-together.md)ドキュメントを参照して、AEM アーキテクチャの基本と、アプリケーションをまとめるために使用する必要があるツールについて確認してください。

## その他のリソース {#additional-resources}

* [Adobe Experience Manager as a Cloud Service API](https://developer.adobe.com/experience-cloud/experience-manager-apis/)
* [構造化コンテンツの配信と管理用の AEM API](/help/headless/apis-headless-and-content-fragments.md)
* [コンテンツフラグメント配信用の AEM REST OpenAPI](/help/headless/aem-rest-openapi-content-fragment-delivery.md)
* [コンテンツフラグメント配信用の AEM GraphQL API](/help/headless/graphql-api/content-fragments.md)
* [コンテンツフラグメントおよびコンテンツフラグメントモデルの OpenAPI](/help/headless/content-fragment-openapis.md)
* [AEM Assets HTTP API での コンテンツフラグメントのサポート](/help/assets/content-fragments/assets-api-content-fragments.md)
* [コンテンツフラグメントの使用方法](/help/sites-cloud/administering/content-fragments/overview.md)
* [AEM コアコンポーネント](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html?lang=ja)
* [CORS／AEM の説明](https://helpx.adobe.com/jp/experience-manager/kt/platform-repository/using/cors-security-article-understand.html)
* [ビデオ - AEM を使用した CORS 向けの開発](https://helpx.adobe.com/jp/experience-manager/kt/platform-repository/using/cors-security-technical-video-develop.html)
* [ヘッドレス CMS としての AEM の概要](/help/headless/introduction.md)
* [AEM 開発者ポータル](https://experienceleague.adobe.com/landing/experience-manager/headless/developer.html?lang=ja)
* [AEM のヘッドレスに関するチュートリアル](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/overview.html?lang=ja)
