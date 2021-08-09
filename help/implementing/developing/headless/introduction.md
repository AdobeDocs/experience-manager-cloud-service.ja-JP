---
title: AEM Sites as a Cloud Service 向けヘッドレス開発
description: コンテンツモデル、コンテンツフラグメント、GraphQL API など、AEM as a Cloud Service の強力なヘッドレス機能が連携する仕組みと、エクスペリエンスあを一元管理して複数のチャネルで提供する方法を説明します。
exl-id: 24300499-ae9c-49d0-aa25-f51e14d9cf79
source-git-commit: 856266faf4cb99056b1763383d611e9b2c3c13ea
workflow-type: tm+mt
source-wordcount: '487'
ht-degree: 98%

---


# AEM Sites as a Cloud Service 向けヘッドレス開発 {#headless-development}

コンテンツモデル、コンテンツフラグメント、GraphQL API など、AEM as a Cloud Service の強力なヘッドレス機能が連携する仕組みと、エクスペリエンスあを一元管理して複数のチャネルで提供する方法を説明します。

## 概要 {#overview}

ヘッドレス実装は、オーディエンスの場所やチャネルに関係なく、オーディエンスにエクスペリエンスを提供する上で、ますます重要になってきています。

ヘッドレス実装は、フルスタックおよびハイブリッドソリューションにおける従来のようなページおよびコンポーネント管理ではなく、チャネルに依存しない再利用可能なコンテンツフラグメントの作成とそのクロスチャネル配信に重点を置いています。これは、Web エクスペリエンスを実装するための最新の動的な開発パターンです。

![AEM 実装モデル](assets/aem-implementation-models.png)

## ヘッドフルとヘッドレスの比較 {#headful-headless}

このドキュメントでは、AEM の完全なヘッドレス実装モデルを重点的に説明します。ただし、AEM でヘッドフルとヘッドレスは二者択一である必要はありません。ヘッドレス機能を使用すると、コンテンツを管理し様々なエンドポイントに配信できると同時に、コンテンツ作成者が単一ページアプリケーションを編集できるようになります。すべてが AEM にあります。

>[!TIP]
>
>詳しくは、[AEM におけるヘッドフルとヘッドレス](/help/implementing/developing/headful-headless.md)を参照してください。

## AEM as a Cloud Service とヘッドレス {#aem-headless}

AEM as a Cloud Service は、次の 3 つの強力なサービスを提供することで、ヘッドレス実装モデルの柔軟なツールになっています。

1. コンテンツモデル
   * コンテンツモデルはコンテンツの構造化表現です。
   * これらは、情報アーキテクトが AEM コンテンツフラグメントモデルエディターで定義します。
   * コンテンツモデルはコンテンツフラグメントの基盤となります。
1. コンテンツフラグメント
   * コンテンツフラグメントは、コンテンツモデルをインスタンス化したものです。
   * これらは、コンテンツ作成者が AEM コンテンツフラグメントエディターで作成します。
   * 作成後は AEM Assets に保存され、AEM Assets 管理 UI で管理されます。
1. 配信用のコンテンツ API
   * AEM GraphQL API では、コンテンツフラグメント配信をサポートしています。
   * AEM Assets REST API では、コンテンツフラグメントの CRUD 操作をサポートしています。
   * [コンテンツフラグメントコアコンポーネントの JSON エクスポート](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/components/content-fragment-component.html)を使用すると、直接コンテンツ配信も可能です。

## AEM ヘッドレスを使用した最初の手順 {#first-steps}

AEM ヘッドレス機能を使い始めるためのリソースは多数用意されています。ユースケースはそれぞれ異なりますが、いずれも AEM ヘッドレス機能の概要を明確に説明ｓしています。

| リソース | 説明 | タイプ | 対象者 | 予測時刻 |
|---|---|---|---|---|
| [ヘッドレスデベロッパージャーニー](/help/journey-headless/developer/overview.md) | ヘッドレス理論からヘッドレスプロジェクトでの運用開始まで、AEM ヘッドレス機能の包括的な概要については、こちらを参照してください。 | ガイド | デベロッパー向け | 1 時間 |
| [ヘッドレスをはじめる前に](/help/implementing/developing/headless/getting-started/introduction.md) | 主な AEM ヘッドレス機能の概要については、このクイックスタートの概要を参照してください。 | クイックスタート | デベロッパー、管理者 | 20 分 |
| [AEM ヘッドレスをはじめる前に：実践チュートリアル](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/graphql/multi-step/overview.html?lang=ja) | 実践的なアプローチをお好みの場合は、このチュートリアルで、シンプルなヘッドレスプロジェクトの作成に取り組んでください。 | チュートリアル | デベロッパー向け | 2 時間 |
