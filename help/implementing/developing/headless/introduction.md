---
title: AEM Sites as a Cloud Service 向けヘッドレス開発
description: コンテンツモデル、コンテンツフラグメント、GraphQL API など、AEM as a Cloud Service の強力なヘッドレス機能が連携する仕組みと、エクスペリエンスあを一元管理して複数のチャネルで提供する方法を説明します。
exl-id: 24300499-ae9c-49d0-aa25-f51e14d9cf79
source-git-commit: 387e75faeccb0671a32a54ff0c12f05219844311
workflow-type: ht
source-wordcount: '515'
ht-degree: 100%

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
   * [コンテンツフラグメントコアコンポーネントの JSON エクスポート](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/components/content-fragment-component.html?lang=ja)を使用すると、直接コンテンツ配信も可能です。

## AEM ヘッドレスを使用した最初の手順 {#first-steps}

AEM ヘッドレス機能を使い始めるためのリソースは多数用意されています。ユースケースはそれぞれ異なりますが、いずれも AEM ヘッドレス機能の概要を明確に説明ｓしています。

| リソース | 説明 | タイプ | 対象読者 | 予測時刻 |
|---|---|---|---|---|
| [ヘッドレスデベロッパージャーニー](/help/journey-headless/developer/overview.md) | **AEM とヘッドレステクノロジーを初めて使用するユーザー**&#x200B;の場合は、まずここから始めて、ヘッドレスの基本概念から初めてのヘッドレスプロジェクトの運用開始まで、AEM とそのヘッドレス機能の概要を包括的に理解してください。 | ガイド | デベロッパー向け&#x200B;**AEM とヘッドレスを初めて使用するユーザー** | 1 時間 |
| [ヘッドレスをはじめる前に](/help/implementing/developing/headless/getting-started/introduction.md) | **AEM の経験豊富なユーザー**&#x200B;が主な AEM ヘッドレス機能の概要を知りたい場合は、このクイックスタート概要を確認してください。 | クイックスタート | デベロッパー、管理者（**AEM の使用経験あり**） | 20 分 |
| [AEM ヘッドレスをはじめる前に：実践チュートリアル](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/graphql/multi-step/overview.html?lang=ja) | **AEM を熟知していて実践的なアプローチを希望する場合は、このチュートリアルでシンプルなヘッドレスプロジェクトの作成に取り組んでください。** | チュートリアル | デベロッパー向け | 2 時間 |
