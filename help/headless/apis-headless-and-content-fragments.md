---
title: 構造化コンテンツの配信とコンテンツフラグメント管理用の AEM API
description: 構造化コンテンツの配信とコンテンツフラグメント管理用に使用できる API について説明します。
feature: Headless, Content Fragments, Edge Delivery Services
role: Admin, Developer
exl-id: 95aecd30-566a-42a9-b97a-7efe45fd389c
source-git-commit: d9db32110e1e0aaa5bdc20bd6b4bff6da6a3a3a3
workflow-type: ht
source-wordcount: '591'
ht-degree: 100%

---

# 構造化コンテンツの配信と管理用の AEM API {#aem-apis-structured-content-delivery-and-management}

Adobe Experience Manager（AEM）as a Cloud Service では、コンテンツフラグメントからの構造化コンテンツ配信とコンテンツフラグメント管理の両方に対して複数の API を提供します。特定の API について詳しくは、個々のページを参照してください。

* [OpenAPI を備えた AEM コンテンツフラグメント配信](/help/headless/aem-content-fragment-delivery-with-openapi.md)
   * この API は、AEM のコンテンツフラグメントから構造化コンテンツを配信する JSON 応答を作成します。
   * エンドポイントとしてコンテンツフラグメントへのパスを使用します。
   * この API は REST ベースです。
   * CDN 統合を含むコンテンツ配信用に最適化されています。
* [コンテンツフラグメント配信用の AEM GraphQL API](/help/headless/graphql-api/content-fragments.md)
   * この API はスキーマベースです。API スキーマは、コンテンツ構造を定義するコンテンツフラグメントモデルで表されます。
   * この API は GraphQL ベースです。
* [コンテンツフラグメントおよびコンテンツフラグメントモデルの OpenAPI](/help/headless/content-fragment-openapis.md)
   * これらの API は、構造化コンテンツ管理を目的としています。
   * それぞれの GET 演算子は、コンテンツ配信用に最適化されていません。
   * この API は REST ベースです。
* [AEM Assets HTTP API での コンテンツフラグメントのサポート](/help/assets/content-fragments/assets-api-content-fragments.md)
   * AEM の構造化コンテンツ配信用の JSON 出力の元の API。
      * この API は堅牢で実証済みですが、*完全にハイドレート*&#x200B;された JSON 出力を提供しません。参照はパスとしてのみ出力されるので、さらにコンテンツを取得するには 2 番目の API リクエストが必要になります。
   * また、Assets HTTP API は、コンテンツフラグメントおよびコンテンツフラグメントモデル（CRUD）の管理にも使用できます。
   * この API は REST ベースです。
   * Assets HTTP API のコンテンツフラグメントサポートは、Edge Delivery Services JSON REST API によって継承されるので、今後、廃止される予定です。時間スケールは、まだ決定されていません。

<!--
## JSON vs HTML {#json-vs-HTML}

The content delivery format used is driven by frontend implementation. Unstructured content/HTML for full-stack implementations, structured content/JSON for headless implementations, or a combination of both in hybrid implementations. 

Key considerations include:

* Definition
  * JSON (JavaScript Object Notation) - used to represent, access and process structured data. 
  * HTML (HyperText Markup Language) - a markup language of tags and elements in a hierarchical structure.
* Primary Purpose
  * JSON is often used for transferring structure content between the server and client app.
  * HTML is the standard markup language for creating and rendering web pages in a browser.
-->

## REST と GraphQL {#rest-vs-graphql}

使用する API は、開発者が決定します。AEM は両方をサポートしています。

オンラインで多くの比較が使用可能ですが、REST のハイライトとメリットは次のとおりです。

* シンプルさ

   * 開発者は（多くの場合）HTTP と REST に精通しています。[Postman の API の現状レポート](https://www.postman.com/state-of-api/)によると、REST を使用している開発者の割合が高くなっています。

   * シンプルさには、親しみやすさが伴います。REST では、クエリの所有者やアプリの所有者に関する組織的な質問は発生しませんが、GraphQL ではこれらの質問が発生する可能性があります。

   * 親しみやすさには（通常）幅広いコミュニティとツール環境が伴います。これは GraphQL 固有の欠点ではありませんが、REST ではより広範囲かつ奥深いものとなる可能性があります。

   * また、アプローチがシンプルになると、セキュリティの実装も簡単になります。REST では、レンダリングするコンテンツを決定するフィルタリングはすべてクライアントアプリで実行されます。GraphQL では、これはクライアントとサーバーの間のスキーマベースのクエリで行われます。

* 柔軟性

   * REST を使用すると、開発者は任意のリソースを `GET` できます。GraphQL を使用すると、スキーマ内で定義されたリソースに制限されます。

* キャッシュ

   * REST `GET` リクエストに対する JSON 応答は、本質的にキャッシュ可能です。GraphQL `POST` リクエストは、サーバー上に保存され、REST のような `GET` リクエストでリクエストされる AEM 永続クエリを使用するなどしてキャッシュ可能にしない限り、キャッシュできません。

GraphQL のメリットは次のとおりです。

* コンテンツ配信の効率

   * フォーカス

      * GraphQL を使用すると、クライアントアプリケーションは、レンダリングに必要な正確なコンテンツをリクエストできますが、それ以上のリクエストは必要ありません。このアプローチにより、過度のコンテンツペイロードや不要な帯域幅の消費によるコンテンツの過剰配信が防止されます。

   * 単一のエンドポイント

      * REST ではすべての API リクエストがエンドポイントですが、GraphQL では共通のエンドポイントは 1 つだけで、様々なコンテンツリクエストはその共通のエンドポイントを使用するクエリとして表現されます。

* 迅速なプロトタイプ作成

   * GraphQL では、これが GraphQL クエリに統合された 1 ステップのプロセスとなり、プロトタイプ作成が簡単になります。一方、REST は 2 ステップのプロセスです。

      1. API を使用してコンテンツを取得します。
      2. JSON 応答で、クライアントアプリでのレンダリングに使用する内容を決定します。
