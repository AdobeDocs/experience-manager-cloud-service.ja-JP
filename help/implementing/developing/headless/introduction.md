---
title: AEM Sites as a Cloud Service 向けヘッドレス開発
description: コンテンツモデル、コンテンツフラグメント、GraphQL APIなど、Cloud Serviceの強力なヘッドレス機能としてのAEMが連携し、エクスペリエンスを一元管理して複数のチャネルで提供する方法を説明します。
exl-id: 24300499-ae9c-49d0-aa25-f51e14d9cf79
source-git-commit: 816c08b9351b3ce2fd4f31974d707e9d4a4eea27
workflow-type: tm+mt
source-wordcount: '489'
ht-degree: 61%

---


# AEM Sites as a Cloud Service 向けヘッドレス開発 {#headless-development}

コンテンツモデル、コンテンツフラグメント、GraphQL APIなど、Cloud Serviceの強力なヘッドレス機能としてのAEMが連携し、エクスペリエンスを一元管理して複数のチャネルで提供する方法を説明します。

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
   * [コンテンツフラグメントコアコンポーネントの JSON エクスポート](https://docs.adobe.com/content/help/ja-JP/experience-manager-core-components/using/components/content-fragment-component.html)を使用すると、直接コンテンツ配信も可能です。

## AEMヘッドレスを使用した最初の手順{#first-steps}

AEMヘッドレス機能を使い始めるには、様々なリソースを利用できます。 これらは様々な使用例を対象としていますが、すべてでAEMヘッドレス機能の明確な概要を示しています。

| リソース | 説明 | タイプ | 対象者 | Est. 時刻 |
|---|---|---|---|---|
| [ヘッドレス開発者ジャーニー](/help/journey-headless/developer/overview.md) | 最初のヘッドレスプロジェクトでの運用を開始するまでのヘッドレス理論のAEMヘッドレス機能の包括的な概要については、まずこちらを参照してください。 | ガイド | 開発者向け | 1時間 |
| [ヘッドレス入門ガイド](/help/implementing/developing/headless/getting-started/introduction.md) | 主なAEMヘッドレス機能の概要については、このクイックスタートの概要を参照してください。 | クイックスタート | 開発者、管理者 | 20 分 |
| [AEMヘッドレス実践チュートリアルの概要](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/graphql/multi-step/overview.html) | 実践的なアプローチをお勧めする場合、このチュートリアルでは、シンプルなヘッドレスプロジェクトの作成に直接取り組みます。 | チュートリアル | 開発者向け | 2時間 |
