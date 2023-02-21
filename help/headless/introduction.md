---
title: AEMのヘッドレスの概要
description: 詳細なドキュメントとヘッドレスジャーニーを組み合わせたAdobe Experience Manager(AEM) のヘッドレスについて説明します。 コンテンツモデル、コンテンツフラグメント、GraphQL API などの機能を使用してヘッドレスエクスペリエンスを強化する方法について説明します。
landing-page-description: Adobe Experience Manager as a Cloud Serviceでヘッドレスを使用および管理する方法について説明します。
exl-id: 24300499-ae9c-49d0-aa25-f51e14d9cf79
source-git-commit: 58a7886e32664dddfd3ca9c888717452ed5d362a
workflow-type: tm+mt
source-wordcount: '675'
ht-degree: 94%

---


# Adobe Experience Manager as a Headless CMS の概要 {#introduction-aem-headless}

コンテンツモデル、コンテンツフラグメント、ヘッドレスエクスペリエンスを大規模に強化する GraphQL API などの機能を備えた Adobe Experience Manager（AEM）as a Headless CMS の使用方法について説明します。

関係する様々な機能の詳細なドキュメントを読んだり、[最初のステップの概要を把握するためのヘッドレスジャーニー](#first-steps)に従うことができます。

>[!NOTE]
>
>ヘッドレスの概念と用語の概要については、[ヘッドレスとは](/help/headless/what-is-headless.md)を参照してください。

## 概要 {#overview}

AEM ヘッドレスは、AEM 内の構造化コンテンツ（コンテンツフラグメント）を、GraphQL を使用して HTTP 経由で任意のアプリで使用できるようにする、Experience Manager の CMS ソリューションです。ヘッドレス実装により、複数のプラットフォームやチャネルにわたって、大規模なエクスペリエンスを提供できます。

ヘッドレス実装は、フルスタックおよびハイブリッドソリューションにおける従来のようなページおよびコンポーネント管理ではなく、チャネルに依存しない再利用可能なコンテンツフラグメントの作成とそのクロスチャネル配信に重点を置いています。これは、web エクスペリエンスを実装するための最新の動的な開発パターンです。

![AEM 実装モデル](assets/aem-implementation-models.png)

## 機能 {#aem-headless-features}

AEM as a Cloud Service は、次の 3 つの強力な機能を提供することで、ヘッドレス実装モデルの柔軟なツールになっています。

1. **コンテンツモデル**
   * コンテンツモデルはコンテンツの構造化表現です。
   * コンテンツモデルは、情報アーキテクトが AEM コンテンツフラグメントモデルエディターで定義します。
   * コンテンツモデルはコンテンツフラグメントの基盤となります。
1. **コンテンツフラグメント**
   * コンテンツフラグメントは、コンテンツフラグメントモデルに基づいて作成されます。
   * コンテンツ作成者が AEM コンテンツフラグメントエディターで作成します。
   * コンテンツフラグメントは AEM Assets に保存され、AEM Assets 管理 UI で管理されます。
1. **配信用のコンテンツ API**
   * AEM GraphQL API では、コンテンツフラグメント配信をサポートしています。
   * AEM Assets REST API では、コンテンツフラグメントの CRUD 操作をサポートしています。
   * ダイレクトコンテンツ配信は、[コンテンツフラグメントコアコンポーネントの JSON 書き出し](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/components/content-fragment-component.html?lang=ja)を使用して実行することもできます。

## 最初の手順 {#first-steps}

AEM ヘッドレス機能を使い始めるためのリソースがいくつか用意されています。各ガイドは、様々な使用例やオーディエンス向けにカスタマイズされています。

| リソース | 説明 | タイプ | 対象読者 | 予測時刻 |
|---|---|---|---|---|
| [ヘッドレスデベロッパージャーニー](/help/journey-headless/developer/overview.md) | **AEM とヘッドレステクノロジーを初めて使用する開発者**&#x200B;の場合は、まずここから始めて、ヘッドレスの基本概念から初めてのヘッドレスプロジェクトの運用開始まで、AEM とそのヘッドレス機能の概要を包括的に理解してください。 | ガイド | **AEM とヘッドレスを初めて使用する**&#x200B;開発者 | 1 時間 |
| [ヘッドレスの設定](/help/headless/setup/introduction.md) | **AEM の経験豊富なユーザー**&#x200B;が主な AEM ヘッドレス機能の概要を知りたい場合は、このクイックスタート概要を確認してください。 | 参照の設定 | **AEM エクスペリエンス**&#x200B;の開発者、管理者 | 20 分 |
| [ヘッドレス実践チュートリアル](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/graphql/multi-step/overview.html?lang=ja) | **AEM を熟知していて実践的なアプローチを希望する場合**&#x200B;は、このチュートリアルでシンプルなヘッドレスアプリの実装に取り組んでください。 | チュートリアル | デベロッパー向け | 2 時間 |
| [ヘッドレスアーキテクトジャーニー](/help/journey-headless/architect/overview.md) | **AEM とヘッドレステクノロジーを初めて使用するアーキテクト**&#x200B;の場合は、まずここから始めて、Adobe Experience Manager as a Cloud Service の強力で柔軟なヘッドレス機能と、プロジェクトのコンテンツをモデル化する方法の概要を理解してください。 | ガイド | アーキテクト | 1 時間 |
| [ヘッドレスオーサリングジャーニー](/help/journey-headless/author/overview.md) | **AEM とヘッドレステクノロジーを初めて使用するビジネスユーザー**&#x200B;の場合は、まずここから始めて、Adobe Experience Manager as a Cloud Service の強力で柔軟なヘッドレス機能と、プロジェクトのコンテンツをモデル化する方法の概要を理解してください。 | ガイド | コンテンツ作成者 | 1 時間 |
| [ヘッドレス翻訳ジャーニー](/help/journey-headless/translation/overview.md) | **ヘッドレスへの AEM 翻訳アプローチに関心がある**&#x200B;ユーザー向け。ヘッドレステクノロジーと、AEM で翻訳プロジェクトを作成および更新する方法を一から十まで説明します。 | ガイド | 翻訳スペシャリスト | 1 時間 |

## ヘッドフルとヘッドレスの比較 {#headful-headless}

このガイドでは、AEM の完全なヘッドレス実装モデルを重点的に説明します。ただし、AEM でヘッドフルとヘッドレスは二者択一である必要はありません。ヘッドレス機能を使用すると、コンテンツを管理し、複数のタッチポイントに配信できると同時に、コンテンツ作成者が単一ページアプリケーションを編集できるようになります。すべてが AEM にあります。

>[!TIP]
>
>詳しくは、[AEM におけるヘッドフルとヘッドレス](/help/implementing/developing/headful-headless.md)を参照してください。