---
title: AEM配信APIを使用したコンテンツへのアクセス方法
description: AEMヘッドレス開発者ジャーニーのこの部分では、GraphQLクエリを使用してコンテンツフラグメントのコンテンツにアクセスする方法を説明します。
hide: true
hidefromtoc: true
index: false
translation-type: tm+mt
source-git-commit: 6097cb8961f604ec2d3f5f6d602c927efc7344d5
workflow-type: tm+mt
source-wordcount: '734'
ht-degree: 53%

---


# AEM配信APIを使用したコンテンツへのアクセス方法{#access-your-content}

>[!CAUTION]
>
>作業中 — このドキュメントの作成は現在進行中で、完全なもの、最終的なもの、または実稼働目的で使用するものとして理解してはなりません。

[AEMヘッドレス開発者ジャーニーのこの部分では、](#overview.md)がGraphQLクエリを使用してコンテンツフラグメントのコンテンツにアクセスする方法を学びます。

## {#story-so-far}

以前のドキュメントのAEMヘッドレスジャーニーでは、[コンテンツのモデル化方法](model-your-content.md)をAEMで学び、次の作業を行う必要があります。

* コンテンツをデザインする際の重要な計画上の考慮事項を理解します。
* 統合レベルの要件に応じてヘッドレスを実装する手順を理解します。
* 必要なツールとAEM設定を設定します。
* ヘッドレスなジャーニーをスムーズにし、コンテンツ生成を効率的に維持し、コンテンツを迅速に配信するためのベストプラクティスを知っている。

この記事は、これらの基本事項に基づいて構築されているので、APIを使用してAEMの既存のヘッドレスコンテンツにアクセスする方法を理解しています。

* **オーディエンス**:初心者
* **目的**:AEM GraphQLクエリを使用してコンテンツフラグメントのコンテンツにアクセスする方法を説明します。
   * GraphQLの紹介。
   * AEM GraphQL APIの紹介。
   * AEM GraphQL APIの詳細を確認します。
   * 実際の動作を確認するには、サンプルクエリを参照してください。

Adobe Experience Manager(AEM)をCloud Serviceとして使用すると、AEM GraphQL APIと共にコンテンツフラグメントを使用して、アプリケーションで使用する構造化コンテンツをヘッドレスに配信できます。 単一の API クエリをカスタマイズする機能により、レンダリングする特定のコンテンツを（単一の API クエリに対する応答として）取得して配信できます。

>[!NOTE]
>AEM GraphQL APIは、標準のGraphQLに基づいてカスタマイズされた実装です。

## GraphQL — 入門{#graphql-introduction}

GraphQL とは次のことを意味します。

* 「*...API のクエリ言語と、既存のデータを使用してこれらのクエリを満たすランタイムです。*」

   *GraphQL*&#x200B;を参照してください。

### GraphQL — タイプ{#graphql-types}

### GraphQL -スキーマ{#graphql-schemas}

### GraphQL -クエリ{#graphql-queries}

## AEMとGraphQL {#aem-graphql}

GraphQLはAEMの様々な場所で使用されます。

* Commerce
   * プレースホルダー
* コンテンツフラグメント
   * この使用事例用にカスタマイズされたAPIが開発されています。
   * これはAEM GraphQL APIです。

## AEM GraphQL API {#aem-graphql-api}

Adobe Experience as a Cloud Experience には、標準の GraphQL API のカスタマイズ実装が開発されています。

AEM GraphQL API を使用すると、コンテンツフラグメントで（複雑な）クエリを実行できます。各クエリは、特定のモデルタイプに従っています。返されたコンテンツは、アプリケーションで使用できます。

>[!NOTE]
>
>AEM GraphQL API の実装は、GraphQL Java ライブラリに基づいています。

### AEM GraphQL APIとコンテンツフラグメント{#aem-graphql-content-fragments}

## AEM GraphQL API で使用するコンテンツフラグメント {#content-fragments-use-with-aem-graphql-api}

コンテンツフラグメントは、AEM クエリの GraphQL の基盤として次のように使用できます。

* ページに依存しないコンテンツをデザイン、作成、キュレーションおよび公開できます。
* コンテンツフラグメントモデルは、定義されたデータタイプを使用して、必要な構造を提供します。
* モデルの定義時に使用できるフラグメント参照を使用して、構造の追加のレイヤーを定義できます。

### コンテンツフラグメント {#content-fragments}

コンテンツフラグメント：

* 構造化コンテンツを含みます。

* 作成されるフラグメントの構造を事前定義するコンテンツフラグメントモデルに基づいています。

### コンテンツフラグメントモデル {#content-fragments-models}

コンテンツフラグメントモデルは、

* **有効**&#x200B;にされると、スキーマの生成に使用されます。

* GraphQL に必要なデータタイプとフィールドを提供します。アプリケーションが、可能なことだけを要求して期待するものを受け取るようにします。

* データタイプ&#x200B;**フラグメント参照**&#x200B;は、別のコンテンツフラグメントを参照するためにモデル内で使用できるので、構造レベルを追加します。

### フラグメント参照 {#fragment-references}

**フラグメント参照**&#x200B;は、

* GraphQL との関連で特に興味深いものです。

* コンテンツフラグメントモデルの定義時に使用できる特定のデータタイプです。

* 特定のコンテンツフラグメントモデルに依存する別のフラグメントを参照します。

* 構造化データを取得できます。

   * **マルチフィード**&#x200B;として定義した場合、複数のサブフラグメントをプライムフラグメントで参照（取得）できます。

### JSON プレビュー {#json-preview}

コンテンツフラグメントモデルの設計と開発に役立つように、[JSON 出力](/help/assets/content-fragments/content-fragments-json-preview.md)をプレビューできます。

## 次の作業{#whats-next}

[REST APIを使用してコンテンツフラグメントのコンテンツにアクセスし、更新する方法を説明します](/help/implementing/developing/headless-journey/update-your-content.md)。

## その他のリソース {#additional-resources}

* [GraphQL.org](https://graphql.org)
   * [スキーマ](https://graphql.org/learn/schema/)
   * [GraphQL Javaライブラリ](https://graphql.org/code/#java)
* [コンテンツフラグメントと共に使用する AEM GraphQL API](/help/assets/content-fragments/graphql-api-content-fragments.md)
   * [AEM での GraphQL の使用方法 - サンプルコンテンツとサンプルクエリ](/help/assets/content-fragments/content-fragments-graphql-samples.md)
   * [コンテンツフラグメントに対するリモート AEM GraphQL クエリの認証](/help/assets/content-fragments/graphql-authentication-content-fragments.md)
* [コンテンツフラグメントの操作](/help/assets/content-fragments/content-fragments.md)
   * [コンテンツフラグメントモデル](/help/assets/content-fragments/content-fragments-models.md)
   * [JSON 出力](/help/assets/content-fragments/content-fragments-json-preview.md)
