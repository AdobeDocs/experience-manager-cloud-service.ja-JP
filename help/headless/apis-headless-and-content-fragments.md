---
title: 構造化コンテンツ配信およびコンテンツフラグメント管理のためのAEM API
description: 構造化コンテンツ配信およびコンテンツフラグメント管理に使用できる API について説明します
feature: Headless, Content Fragments, Edge Delivery Services
role: Admin, Developer
source-git-commit: 21599676916068f3529976410a93951b02f750b0
workflow-type: tm+mt
source-wordcount: '592'
ht-degree: 3%

---


# 構造化コンテンツ配信および管理用のAEM API {#aem-apis-structured-content-delivery-and-management}

Adobe Experience Manager（AEM）as a Cloud Serviceでは、コンテンツフラグメントからの構造化コンテンツ配信とコンテンツフラグメント管理の両方に対して複数の API を提供しています。 特定の API について詳しくは、個々のページを参照してください。

* [ コンテンツフラグメント配信用AEM REST OpenAPI](/help/headless/aem-rest-openapi-content-fragment-delivery.md)
   * この API は、AEMのコンテンツフラグメントから構造化コンテンツを配信するための JSON 応答を作成します。
   * エンドポイントとしてコンテンツフラグメントへのパスを使用します。
   * この API は REST ベースです。
   * CDN 統合を含むコンテンツ配信用に最適化されています。
* [コンテンツフラグメント配信用のAEM GraphQL API](/help/headless/graphql-api/content-fragments.md)
   * この API はスキーマベースです。 API スキーマは、コンテンツ構造を定義するコンテンツフラグメントモデルで表されます。
   * この API はGraphQL ベースです。
* [コンテンツフラグメントおよびコンテンツフラグメントモデルの OpenAPI](/help/headless/content-fragment-openapis.md)
   * これらの API は、構造化コンテンツ管理を目的としています。
   * それぞれのGET演算子は、コンテンツ配信用に最適化されていません。
   * この API は REST ベースです。
* [AEM Assets HTTP API での コンテンツフラグメントのサポート](/help/assets/content-fragments/assets-api-content-fragments.md)
   * AEMの構造化コンテンツ配信用の JSON 出力のオリジナル API。
      * 堅牢で実証済みですが、この API では JSON 出力を *完全にハイドレート* することはできません。 参照はパスとしてのみ出力され、それ以上のコンテンツを取得するにはセカンダリ API リクエストが必要です。
   * Assets HTTP API は、コンテンツフラグメントとコンテンツフラグメントモデル（CRUD）の管理にも使用できます。
   * この API は REST ベースです。
   * Assets HTTP API でのコンテンツフラグメントのサポートは、今後、廃止される予定です。これは、Edge Delivery Services JSON REST API によって継承されるためです。 タイムスケールはまだ決まっていません。

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

## REST とGraphQL {#rest-vs-graphql}

使用する API は、開発者向けの決定です。AEMは、両方をサポートしています。

多くの比較をオンラインで利用できますが、REST のハイライトとメリットには次のようなものがあります。

* シンプル

   * 開発者は（多くの場合） HTTP と REST に精通しています。 [API レポートのPostmanの状況 ](https://www.postman.com/state-of-api/) によると、REST を使用している開発者の割合が高くなっています。

   * シンプルさは、親しみやすさをもたらします。 REST の場合、誰がクエリを所有し、誰がアプリを所有するかという組織的な質問はありませんが、これらの質問はGraphQLで発生する可能性があります。

   * （通常は）慣れることで、幅広いコミュニティとツールの風景が得られます。 GraphQL固有の欠点ではありませんが、REST にとってより広く、より深い可能性があります。

   * また、よりシンプルなアプローチにより、セキュリティの実装も容易になります。 REST では、レンダリングするコンテンツを決定するフィルタリングはすべてクライアントアプリで行われます。 GraphQLでは、これはクライアントとサーバーの間のスキーマベースのクエリで行われます。

* 柔軟性

   * REST を使用すると、開発者は任意のリソース `GET` 使用できます。 GraphQLを使用すると、スキーマ内で定義されたリソースに制限されます。

* キャッシュ

   * REST `GET` リクエストに対する JSON 応答は、本質的にキャッシュ可能です。 GraphQL `POST` リクエストは、作成されない限りキャッシュできません。例えば、サーバーに保存され、REST のような `GET` リクエストでリクエストされるAEM永続クエリを使用する場合などです。

GraphQLの利点は次のとおりです。

* コンテンツ配信の効率

   * フォーカス

      * GraphQLを使用すると、クライアントアプリケーションは、レンダリングに必要な正確なコンテンツをリクエストでき、それ以上はリクエストできなくなります。 このアプローチは、コンテンツの過剰配信、過剰なコンテンツペイロードおよび不要な帯域幅消費を防ぎます。

   * 単一のエンドポイント

      * REST では、すべての API リクエストがエンドポイントですが、GraphQLでは共通のエンドポイントは 1 つだけで、異なるコンテンツリクエストがその共通のエンドポイントを使用したクエリとして表現されます。

* ラピッドプロトタイピング

   * GraphQLの場合、これは 1 つの手順でGraphQLのクエリと統合されたプロセスであり、プロトタイプ作成が容易になります。 一方、REST のプロセスは 2 ステップです。

      1. API を使用してコンテンツを取得します。
      2. JSON 応答で、クライアントアプリでのレンダリングに使用する内容を決定します。
