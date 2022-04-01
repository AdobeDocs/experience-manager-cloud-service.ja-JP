---
title: GraphQL のコンテンツフラグメントを使用したヘッドレスコンテンツ配信
description: Learn the basic concepts of realizing an AEM Headless CMS using Content Fragments with GraphQL for headless content delivery.
feature: Content Fragments, GraphQL API
topic: Headless
role: User
exl-id: 4a3b030d-ed59-4920-bf94-e00a45f85b51
source-git-commit: f296e8cbc12c9426e0fefe6f5342374ba9b21291
workflow-type: tm+mt
source-wordcount: '739'
ht-degree: 90%

---

# GraphQL のコンテンツフラグメントを使用したヘッドレスコンテンツ配信 {#headless-content-delivery-using-content-fragments-with-graphQL}

With Content Fragments and the GraphQL API you can use Adobe Experience Manager (AEM) as a Cloud Service as a Headless Content Management System (CMS).

This is achieved using Content Fragments, together with the AEM GraphQL API (a customized implementation, based on standard GraphQL), to headlessly deliver structured content for use in your applications. 単一の API クエリをカスタマイズする機能により、レンダリングする特定のコンテンツを（単一の API クエリに対する応答として）取得して配信できます。

>[!NOTE]
>
>AEM Sites as a Cloud Service 向けヘッドレス開発の概要については、[AEM Sites as a Cloud Service 向けヘッドレス開発](/help/headless/introduction.md)を参照してください。

>[!NOTE]
>
>GraphQL は現在、Adobe Experience Manager（AEM）as a Cloud Service の、2 つの（個別の）シナリオで使用されています。
>
>* [AEM コマースは、GraphQL 経由でコマースプラットフォームのデータを使用します](/help/commerce-cloud/integrating/magento.md)。
>* [AEM コンテンツフラグメントは、AEM GraphQL API（標準の GraphQL に基づいてカスタマイズされた実装）と連携して、アプリケーションで使用する構造化コンテンツを配信します](/help/headless/graphql-api/content-fragments.md)。


## ヘッドレス CMS {#headless-cms}

ヘッドレスコンテンツ管理システム（CMS）とは次のことを意味します。

* 「*ヘッドレスコンテンツ管理システム（ヘッドレス CMS）は、バックエンド専用のコンテンツ管理システム（CMS）であり、API 経由でコンテンツにアクセスして、任意のデバイスに表示できます。*」

   [ウィキペディア](https://en.wikipedia.org/wiki/Headless_content_management_system)を参照してください。

AEM のコンテンツフラグメントのオーサリングとは、次のことを意味します。

* コンテンツフラグメントを使用すると、主にフォーマットされたページに直接公開することを目的としていない（1:1）コンテンツを作成できます。

* コンテンツフラグメントのコンテンツは、コンテンツフラグメントモデルに従って、あらかじめ決められた方法で構造化されます。これにより、アプリケーションへのアクセスが簡素化され、コンテンツの処理が促進されます。

## GraphQL - 概要 {#graphql-overview}

GraphQL とは次のことを意味します。

* 「*...API のクエリ言語と、既存のデータを使用してこれらのクエリを満たすランタイムです。*」

   [GraphQL.org](https://graphql.org) を参照

[AEM GraphQL API](#aem-graphql-api) を使用すると、[コンテンツフラグメント](/help/assets/content-fragments/content-fragments.md)で（複雑な）クエリを実行できます。各クエリは、特定のモデルタイプに従っています。返されたコンテンツは、アプリケーションで使用できます。

## AEM GraphQL API {#aem-graphql-api}

Adobe Experience as a Cloud Experience には、標準の GraphQL API のカスタマイズ実装が開発されています。詳しくは、「[コンテンツフラグメントと共に使用する AEM GraphQL API](/help/headless/graphql-api/content-fragments.md)」を参照してください。

AEM GraphQL API の実装は、[GraphQL Java ライブラリ](https://graphql.org/code/#java)に基づいています。

## AEM GraphQL API で使用するコンテンツフラグメント {#content-fragments-use-with-aem-graphql-api}

[コンテンツフラグメント](#content-fragments)は、AEM クエリの GraphQL の基盤として次のように使用できます。

* ページに依存しないコンテンツをデザイン、作成、キュレーションおよび公開できます。
* [コンテンツフラグメントモデル](#content-fragments-models)は、定義されたデータタイプを使用して、必要な構造を提供します。
* モデルの定義時に使用できる[フラグメント参照](#fragment-references)を使用して、構造の追加のレイヤーを定義できます。

![GraphQL と共に使用するコンテンツフラグメント](assets/cfm-nested-01.png " GraphQL と共に使用するコンテンツフラグメント")

### コンテンツフラグメント {#content-fragments}

コンテンツフラグメント：

* 構造化コンテンツを含みます。

* 作成されるフラグメントの構造を事前定義する[コンテンツフラグメントモデル](#content-fragments-models)に基づいています。

### コンテンツフラグメントモデル {#content-fragments-models}

[コンテンツフラグメントモデル](/help/assets/content-fragments/content-fragments-models.md)は、

* **有効**&#x200B;にされると、[スキーマ](https://graphql.org/learn/schema/)の生成に使用されます。

* GraphQL に必要なデータタイプとフィールドを提供します。アプリケーションが、可能なことだけを要求して期待するものを受け取るようにします。

* データタイプ&#x200B;**[フラグメント参照](#fragment-references)**&#x200B;は、別のコンテンツフラグメントを参照するためにモデル内で使用できるので、構造レベルを追加します。

### フラグメント参照 {#fragment-references}

**[フラグメント参照](/help/assets/content-fragments/content-fragments-models.md#fragment-reference-nested-fragments)**&#x200B;は、

* GraphQL との関連で特に興味深いものです。

* コンテンツフラグメントモデルの定義時に使用できる特定のデータタイプです。

* 特定のコンテンツフラグメントモデルに依存する別のフラグメントを参照します。

* 構造化データを取得できます。

   * **マルチフィード**&#x200B;として定義した場合、複数のサブフラグメントをプライムフラグメントで参照（取得）できます。

### JSON プレビュー {#json-preview}

コンテンツフラグメントモデルの設計と開発に役立つように、[JSON 出力](/help/assets/content-fragments/content-fragments-json-preview.md)をプレビューできます。

## AEM での GraphQL の使用方法 - サンプルコンテンツとサンプルクエリ {#learn-graphql-with-aem-sample-content-queries}

AEM GraphQL API の使い方の紹介は、「[AEM での GraphQL の使用方法 - コンテンツとクエリの例](/help/headless/graphql-api/sample-queries.md)」を参照してください。

## チュートリアル - AEM ヘッドレスと GraphQL をはじめる前に

実践的なチュートリアルを探している場合は、AEM の GraphQL API を使用し、外部アプリで使用するコンテンツをヘッドレス CMS シナリオで構築して公開する方法を示す「[AEM ヘッドレスと GraphQL をはじめる前に](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/graphql/overview.html?lang=ja)」のエンドツーエンドのチュートリアルをご覧ください。
