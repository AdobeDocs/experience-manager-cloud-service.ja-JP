---
title: GraphQLでのコンテンツフラグメントを使用したヘッドレスコンテンツ配信
description: Adobe Experience Manager(AEM)のコンテンツフラグメントを、ヘッドレスコンテンツ配信用のGraphQLとのCloud Serviceとして使用する方法を説明します。
translation-type: tm+mt
source-git-commit: 54b377c6d98398fd5066dc4a3337a3877b9e3ed7
workflow-type: tm+mt
source-wordcount: '670'
ht-degree: 1%

---


# GraphQLでコンテンツフラグメントを使用したヘッドレスコンテンツ配信{#headless-content-delivery-using-content-fragments-with-graphQL}

Adobe Experience Manager(AEM)をCloud Serviceとして使用すると、AEM GraphQL API（標準GraphQLに基づくカスタマイズされた実装）と共にコンテンツフラグメントを使用して、アプリケーションで使用する構造化されたコンテンツを配信できます。 単一のAPIクエリをカスタマイズする機能により、レンダリングする必要がある/必要な特定のコンテンツを(単一のAPIクエリに対する応答として)取得して配信できます。

>[!NOTE]
>
>Cloud ServiceとしてのAEM Sites向けヘッドレス開発の紹介は、[ヘッドレスとAEM](/help/implementing/developing/headless/introduction.md)を参照。

## ヘッドレスCMS {#headless-cms}

ヘッドレスコンテンツ管理システム(CMS)は次のとおりです。

* &quot;*ヘッドレスコンテンツ管理システム（ヘッドレスCMS）は、バックエンド専用のコンテンツ管理システム(CMS)で、API経由でコンテンツにアクセスし、任意のデバイスに表示できます。*

   [Wikipedia](https://en.wikipedia.org/wiki/Headless_content_management_system)を参照してください。

AEMのコンテンツフラグメントのオーサリングに関しては、次のことを意味します。

* コンテンツフラグメントを使用すると、主に形式設定されたページに直接公開することを目的としていない(1:1)コンテンツを作成できます。

* コンテンツフラグメントのコンテンツは、コンテンツフラグメントモデルに従って、あらかじめ決められた方法で構造化されます。 これにより、アプリケーションへのアクセスが簡素化され、コンテンツの処理がさらに進みます。

## GraphQL — 概要{#graphql-overview}

GraphQLは次のようになります。

* &quot;*...APIのクエリ言語と、既存のデータを使用してこれらのクエリを満たすランタイム。*&quot;

   [GraphQL.org](https://graphql.org)を参照

[AEM GraphQL API](#aem-graphql-api)を使用すると、[コンテンツフラグメント](/help/assets/content-fragments/content-fragments.md)で（複雑な）クエリを実行できます。の各クエリは、特定のモデルタイプに従っています。 返されたコンテンツは、アプリケーションで使用できます。

## AEM GraphQL API {#aem-graphql-api}

クラウドエクスペリエンスとしてのAdobeエクスペリエンスの場合、標準のGraphQL APIのカスタマイズ実装が開発されました。 詳しくは、[AEM GraphQL API for use with Content Fragments](/help/assets/content-fragments/graphql-api-content-fragments.md)を参照してください。

AEM GraphQL APIの実装は、[GraphQL Javaライブラリ](https://graphql.org/code/#java)に基づいています。

## AEM GraphQL API {#content-fragments-use-with-aem-graphql-api}で使用するコンテンツフラグメント

[コンテンツ](#content-fragments) フラグメントは、AEMクエリのGraphQLの基盤として次のように使用できます。

* ページに依存しないコンテンツをデザイン、作成、キュレーションおよび公開できます。
* [コンテンツフラグメントモデル](#content-fragments-models)は、定義されたデータ型を使用して、必要な構造を提供します。
* モデルの定義時に使用できる[フラグメント参照](#fragment-references)を使用して、構造の追加のレイヤーを定義できます。

![GraphQLContent Fragmentsと共に使用する](assets/cfm-nested-01.png "コンテンツフラグメント（GraphQLで使用）")

### コンテンツフラグメント {#content-fragments}

コンテンツフラグメント:

* 構造化コンテンツを含みます。

* これらは、[コンテンツフラグメントモデル](#content-fragments-models)に基づいており、結果のフラグメントの構造を事前に定義します。

### コンテンツフラグメントモデル {#content-fragments-models}

次の[コンテンツフラグメントモデル](/help/assets/content-fragments/content-fragments-models.md):

* [スキーマ](https://graphql.org/learn/schema/)の生成に使用します。1回は&#x200B;**有効**&#x200B;です。

* GraphQLに必要なデータタイプとフィールドを指定します。 アプリケーションが可能なもののみを要求し、期待されるものを受け取るようにします。

* データ型&#x200B;**[フラグメント参照](#fragment-references)**&#x200B;は、別のコンテンツフラグメントを参照するためにモデル内で使用できるので、構造のレベルを追加します。

### フラグメント参照{#fragment-references}

**[フラグメント参照](/help/assets/content-fragments/content-fragments-models.md#fragment-reference-nested-fragments)**:

* は、GraphQLとの関連で特に興味を持ちます。

* は、コンテンツフラグメントモデルの定義時に使用できる特定のデータ型です。

* 特定のコンテンツフラグメントモデルに依存する別のフラグメントを参照します。

* 構造化データを取得できます。

   * **マルチフィード**&#x200B;として定義した場合、複数のサブフラグメントをプライムフラグメントで参照（取得）できます。

### JSONプレビュー{#json-preview}

コンテンツフラグメントモデルの設計と開発に役立つように、[JSON出力](/help/assets/content-fragments/content-fragments-json-preview.md)をプレビューできます。

## AEMでのGraphQLの使用方法 — サンプルコンテンツとクエリ{#learn-graphql-with-aem-sample-content-queries}

AEM GraphQL APIの使い方の紹介は、[AEMでのGraphQLの使い方の学習 — サンプルコンテンツとクエリ](/help/assets/content-fragments/content-fragments-graphql-samples.md)を参照してください。

## チュートリアル — AEM HeadlessとGraphQLの使い始めに

実践チュートリアルを探している場合 AEMのGraphQL APIを使用し、外部アプリで使用するコンテンツを、ヘッドレスCMSシナリオで構築して公開する方法を示す[AEM HeadlessとGraphQL](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/graphql/overview.html)のエンドツーエンドのチュートリアルをご覧ください。