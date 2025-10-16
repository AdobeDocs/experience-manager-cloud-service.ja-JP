---
title: AEM ヘッドレス CMS デベロッパージャーニー
description: Adobe Experience Manager（AEM）をヘッドレス CMS として使用したヘッドレス開発について説明します。コンテンツモデル、コンテンツフラグメント、GraphQL API などの機能を使用してヘッドレスなコンテンツ配信を強化する方法について説明します。
landing-page-description: ヘッドレスコンテンツの配信と実装について理解します。企業内での戦略の策定について詳しく説明します。
exl-id: d14a1e30-dd04-49a8-8cda-27c80a4bb0f5
solution: Experience Manager
feature: Headless, Content Fragments,GraphQL API
role: Admin, Architect, Developer
source-git-commit: 2ccca86a0e611b93c273e37abb6e0fd7870421d4
workflow-type: tm+mt
source-wordcount: '930'
ht-degree: 95%

---

# AEM ヘッドレス CMS デベロッパージャーニー {#aem-headless-developer-journey}

Adobe Experience Manager ヘッドレス CMS を初めて使用する開発者向けドキュメントへようこそ。

強力かつ柔軟なヘッドレス機能とその特長および最初のヘッドレス開発プロジェクトでの活用方法を説明します。このジャーニーでは、最初のヘッドレスアプリケーションの開発に必要なあらゆる情報を提供します。

>[!CONTEXTUALHELP]
>id="aemcloud_headless_developer_resources"
>title="AEM ヘッドレス開発者向けリソースとドキュメント"
>abstract="AEM ヘッドレス CMS の概要と、優れたアプリケーションを構築および提供し、より迅速なエクスペリエンスを実現する方法を包括的に解説します。"
>additional-url="https://experienceleague.adobe.com/landing/experience-manager/headless/developer.html?lang=ja" text="AEM ヘッドレス開発者向けリソース"


## はじめに {#introduction}

AEM のヘッドレス実装では、コンテンツフラグメントモデルとコンテンツフラグメントを使用して、構造化され、チャネルに依存しない、再利用可能なコンテンツフラグメントの作成とそれらのクロスチャネル配信に重点を置いています。これを実現するために、フルスタックソリューションにおける従来のようなページおよびコンポーネント管理は採用していません。これは、デジタルエクスペリエンスを実装するための最新の動的な開発パターンです。

このガイドでは、AEM のヘッドレス実装に関するトピックを順を追って説明します。完了時には次のことができるようになります。

* ヘッドレスなコンテンツ配信の概要とそのメリットを十分に理解する。
* AEM ヘッドレス機能と、それらが連携してヘッドレスなエクスペリエンスを提供する仕組みを理解する。
* 最初の AEM ヘッドレスプロジェクトを実装する最初の手順を実行します。

## オーディエンス {#audience}

このジャーニーは、デベロッパーのペルソナ向けに設計され、デベロッパーの視点から AEM ヘッドレスプロジェクトの要件、手順およびアプローチをレイアウトします。プロジェクトを成功させるためにデベロッパーがやり取りする必要がある追加のペルソナが定義されますが、ジャーニーの視点はデベロッパーのものです。

このジャーニーで相互にやり取りするペルソナの一覧を以下に示します。

| ペルソナ | 説明 | このジャーニーでの役割 |
|---|---|---|
| 開発者（ターゲットオーディエンス） | 様々なソースのコンテンツを消費するヘッドレスアプリケーションの開発経験があります | このジャーニーのターゲットオーディエンス |
| コンテンツ作成者 | ヘッドレスに配信されるコンテンツを作成し管理します | コンテンツ作成者は、ヘッドレスに配信されるコンテンツを作成します。 |
| 管理者 | AEM の基本セットアップと設定を管理します。 | 開発者は管理者と協力して、開発に必要な設定変更を行います。 |
| コンテンツアーキテクト | ヘッドレスで配信する必要があるデータの要件を分析し、そのデータの構造を定義します。 | 開発者はコンテンツアーキテクトと協力して、データの構造と、データをヘッドレスに配信するための要件を把握します。 |

## ヘッドレスデベロッパージャーニー {#the-journey}

このジャーニーでは、多くのトピックを取り上げ、AEM のヘッドレスに関する基本的な知識を説明します。

ジャーニーの特定の部分に直接移動することもできますが、多くの概念は、それまでの記事で紹介された概念に基づいています。最初から順に進めることをお勧めします。

| # | 記事 | 説明 |
|---|---|---|
| 0 | AEM ヘッドレスデベロッパージャーニー | このドキュメント |
| 1 | [CMS ヘッドレス開発について](learn-about.md) | ヘッドレステクノロジーとその使用方法の詳細 |
| 2 | [AEM Headless as a Cloud Service - はじめに](getting-started.md) | AEM ヘッドレスの前提条件の詳細 |
| 3 | [AEM ヘッドレス機能を使用した初めてのエクスペリエンスへの道筋](path-to-first-experience.md) | 開発環境を設定して、シンプルなアプリを AEM ヘッドレスと統合する方法について説明します。 |
| 4 | [コンテンツをモデル化する方法](model-your-content.md) | コンテンツ構造をモデル化する方法を説明します。 |
| 5 | [AEM Delivery APIを使用してコンテンツにアクセスする方法](access-your-content.md) | GraphQL クエリを使用してコンテンツフラグメントのコンテンツにアクセスする方法を説明します。 |
| 6 | [AEM Assets API を使用してコンテンツを更新する方法](update-your-content.md) | REST API を使用してコンテンツフラグメントのコンテンツにアクセスし、アップデートする方法を説明します。 |
| 7 | [すべてをまとめる方法 - アプリとコンテンツを AEM ヘッドレスに配置する方法](put-it-all-together.md) | AEM ヘッドレス SDK を使用して AEM プロジェクトを運用する準備をする方法について説明します。 |
| 8 | [ヘッドレスアプリケーションを運用する方法](go-live.md) | アプリケーションをライブでデプロイし、Git でローカル コードを取得して CI/CD パイプライン用の Cloud Manager Git に移動する方法を学びます。 |
| 9 | [オプション - AEM を使用して単一ページアプリケーション（SPA）を作成する方法](create-spa.md) | ヘッドフル配信とヘッドレス配信を組み合わせる方法を探索し、AEM の SPA エディターフレームワークを使用して編集可能な SPA を作成する方法を学びます。 |

{style="table-layout:auto"}

## 次のステップ {#what-is-next}

次の記事、[CMS ヘッドレス開発について学ぶ](learn-about.md)から開始します。

## その他のリソース {#additional-resources}

ドキュメントジャーニーは、関連するプロセスと機能をガイドする説明を提供することで、AEM がビジネス上の問題をどのように解決するかを示します。1 つのジャーニーでは、複数の機能が連携して 1 つのビジネスニーズを満たす方法を示しています。

実践による学習を希望し、AEMに関する十分な知識がある場合は、API とフレームワーク別に整理された実践チュートリアルを利用してください。このチュートリアルでは、AEM ヘッドレスに基づくアプリケーションの作成と使用の詳細を紹介しています。 [AEMのヘッドレスに関するチュートリアル ](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/overview.html?lang=ja) を参照してください。

AEM の強力な機能の連携の仕組みについて詳しくは、次に示すその他のジャーニーを参照してください。

* [AEM 開発者ポータル](https://experienceleague.adobe.com/landing/experience-manager/headless/developer.html?lang=ja)
* [AEM ヘッドレス翻訳ジャーニー](/help/journey-headless/translation/overview.md) - このドキュメントジャーニーでは、ヘッドレステクノロジー、AEM によるヘッドレスコンテンツの提供方法、ヘッドレスコンテンツの翻訳方法について幅広く理解できます。
* [ヘッドレスオーサリングジャーニー](/help/journey-headless/author/overview.md) - AEM の強力で柔軟なヘッドレス機能とその能力および初めてのヘッドレスプロジェクトでコンテンツをモデル化する方法を説明するガイド付きジャーニーは、ここから始めてください。
* [ヘッドレスアーキテクトジャーニー](/help/journey-headless/architect/overview.md) - Adobe Experience Manager as a Cloud Service の強力で柔軟なヘッドレス機能と、プロジェクトのコンテンツをモデル化する方法の入門的解説が必要であれば、ここから始めてください。
* [AEM as a Cloud Service 技術ドキュメント](https://experienceleague.adobe.com/docs/experience-manager-cloud-service.html?lang=ja) - AEM およびヘッドレステクノロジーに対して既に十分な理解がある場合は、アドビの詳細な技術ドキュメントを直接参照してください。
   * [ヘッドレス CMS としての AEM の概要](/help/headless/introduction.md)
