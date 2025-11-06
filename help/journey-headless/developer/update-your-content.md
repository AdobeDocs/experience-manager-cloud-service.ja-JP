---
title: AEM API を使用してコンテンツをアップデートする方法
description: AEM ヘッドレスデベロッパージャーニーのこの部分では、使用可能な API を使用してコンテンツフラグメントのコンテンツにアクセスし、アップデートする方法について説明します。
exl-id: 84120856-fd1d-40f7-8df4-73d4cdfcc43b
solution: Experience Manager
feature: Headless, Content Fragments, GraphQL API
role: Admin, Developer
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '503'
ht-degree: 100%

---

# AEM API を使用してコンテンツをアップデートする方法 {#update-your-content}

[AEM ヘッドレスデベロッパージャーニー](overview.md)のこの部分では、使用可能な API を使用してコンテンツフラグメントのコンテンツにアクセスし、アップデートする方法について説明します。

## これまでの説明内容 {#story-so-far}

以前の AEM ヘッドレスジャーニードキュメント（「[AEM Delivery API を使用してコンテンツにアクセスする方法](access-your-content.md)」）では、AEM GraphQL API を介して AEM のヘッドレスコンテンツにアクセスする方法を説明したので、次ができるはずです。

* GraphQL について大まかなレベルで理解する
* AEM GraphQL API の仕組みを理解する
* 実用的なサンプルクエリを理解する

この記事は、これらの基本事項に基づいて構築されているので、使用可能な API を使用して AEM の既存のヘッドレスコンテンツをアップデートする方法を理解できます。

## 目的 {#objective}

* **オーディエンス**：経験者
* **目的**：コンテンツフラグメントのコンテンツにアクセスし、アップデートするのに使用可能な API について説明します。

## コンテンツフラグメントと共に使用する AEM API {#aem-apis-for-use-with-content-fragments}

Adobe Experience Manager（AEM）as a Cloud Service では、コンテンツフラグメントからの構造化コンテンツ配信とコンテンツフラグメント管理の両方に対して複数の API を提供します。特定の API について詳しくは、個々のページを参照してください。

* OpenAPI を備えた AEM コンテンツフラグメント配信
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

>[!NOTE]
>
>[Assets HTTP API でのコンテンツフラグメントのサポート](/help/assets/content-fragments/assets-api-content-fragments.md)が[非推奨](/help/release-notes/deprecated-removed-features.md)になりました。[コンテンツフラグメントとコンテンツフラグメントモデル管理 OpenAPI](/help/headless/content-fragment-openapis.md) が [OpenAPI を使用したコンテンツフラグメント配信](/help/headless/aem-content-fragment-delivery-with-openapi.md)に置き換えられました。

## 次のステップ {#whats-next}

これで、ここでの AEM ヘッドレスデベロッパージャーニーは完了です。次ができるようになったはずです。

* 使用可能な AEM API を理解する。
* これらの API でコンテンツフラグメントがどのようにサポートされているかを理解する。

AEM ヘッドレスジャーニーを続けるには、[すべてをまとめる方法 - AEM ヘッドレスのアプリとコンテンツ](put-it-all-together.md)ドキュメントを参照して、AEM アーキテクチャの基本と、アプリケーションをまとめるために使用する必要があるツールについて確認してください。

## その他のリソース {#additional-resources}

* [Adobe Experience Manager as a Cloud Service API](https://developer.adobe.com/experience-cloud/experience-manager-apis/)
* [構造化コンテンツの配信と管理用の AEM API](/help/headless/apis-headless-and-content-fragments.md)
* [OpenAPI を備えた AEM コンテンツフラグメント配信](/help/headless/aem-content-fragment-delivery-with-openapi.md)
* [コンテンツフラグメント配信用の AEM GraphQL API](/help/headless/graphql-api/content-fragments.md)
* [コンテンツフラグメントおよびコンテンツフラグメントモデルの OpenAPI](/help/headless/content-fragment-openapis.md)
* [AEM Assets HTTP API での コンテンツフラグメントのサポート](/help/assets/content-fragments/assets-api-content-fragments.md)
* [コンテンツフラグメントの使用方法](/help/sites-cloud/administering/content-fragments/overview.md)
* [AEM コアコンポーネント](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html?lang=ja)
* [CORS／AEM の説明](https://experienceleague.adobe.com/docs/experience-manager-learn/foundation/security/understand-cross-origin-resource-sharing.html?lang=ja)
* [ビデオ - AEM を使用した CORS 向けの開発](https://experienceleague.adobe.com/docs/experience-manager-learn/foundation/security/develop-for-cross-origin-resource-sharing.html?lang=ja)
* [ヘッドレス CMS としての AEM の概要](/help/headless/introduction.md)
* [AEM 開発者ポータル](https://experienceleague.adobe.com/landing/experience-manager/headless/developer.html?lang=ja)
* [AEM のヘッドレスに関するチュートリアル](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/overview.html?lang=ja)
