---
title: AEM ヘッドレスコンテンツ作成者ジャーニー
description: AEM の強力で柔軟なヘッドレス機能とその能力およびプロジェクトのコンテンツをオーサリングする方法を説明するガイド付きジャーニーは、ここから始めてください。
exl-id: fe124c6b-932a-44fc-a87b-12691aefea56
solution: Experience Manager
feature: Headless, Content Fragments,GraphQL API
role: Admin, Architect, Developer
source-git-commit: 10580c1b045c86d76ab2b871ca3c0b7de6683044
workflow-type: tm+mt
source-wordcount: '860'
ht-degree: 96%

---

# AEM ヘッドレスコンテンツ作成者ジャーニー {#aem-headless-author-journey}

AEM の強力で柔軟なヘッドレス機能と、ヘッドレスプロジェクトのコンテンツをオーサリングする方法を説明するガイド付きジャーニーは、ここから始めてください。

## はじめに {#introduction}

ヘッドレス実装は、オーディエンスの場所やチャネルに関係なくオーディエンスにエクスペリエンスを提供する上で、ますます重要になってきています。

ヘッドレスコンテンツは、従来のページ構造やコンポーネントに基づいたものではありません。代わりに、チャネルに依存しない再利用可能なコンテンツの断片（フラグメント）の作成と、そのクロスチャネル配信に基づいています。

AEM では、これはコンテンツフラグメントで実現されます。コンテンツを個々のコンテンツフラグメントでオーサリングし、それをアプリケーションで必要に応じて選択して使用できるようにします。

ヘッドレスにはこのような柔軟性があるので、デジタルエクスペリエンスを実装するための最新の動的な開発パターンになります。

このガイドでは、最も重要なトピックを順を追って説明します。完了時には、次のことができるようになります。

* ヘッドレスコンテンツ配信の概要とメリットを基本的に理解する。
* AEM ヘッドレス機能と、それらが連携してヘッドレスなエクスペリエンスを提供する仕組みを理解する。
* AEM ヘッドレスプロジェクトのコンテンツを作成できます。

## AEM ドキュメントジャーニー {#documentation-journeys}

[ドキュメントジャーニー](/help/journey-documentation/documentation-journeys.md)は、前提となる事前のトピックや AEM の知識を最小限に抑えながら、AEM を初めて使用することもある読者がビジネス上の問題全体を把握し解決するのに役立つ説明を提供して、異なる複雑なトピックや機能をひとまとめに扱っています。

ドキュメントジャーニーは、アドビの最新の調査、アドビのコンサルタントによる実装実績、顧客プロジェクトからのフィードバックなどに基づいて、ベストプラクティス原則を軸に設計されています。

AEM を使用してヘッドレスビジネスケースを解決する方法をアドビがどのように推奨しているかを理解するには、[AEM ヘッドレスジャーニー](/help/journey-documentation/documentation-journeys.md)がその出発点になります。

## 対象読者 {#audience}

このジャーニーは、コンテンツ作成者のペルソナ向けに設計されています。コンテンツ作成者として、コンテンツフラグメントで実際のコンテンツを作成します。

このジャーニーは、AEM ヘッドレスプロジェクトのコンテンツをオーサリングするための要件、手順およびアプローチを明確にします。ジャーニーでは、プロジェクトを成功させるためにコンテンツ作成者がやり取りする必要がある追加のペルソナを定義することになりますが、ジャーニー自体はコンテンツ作成者の視点で構成されています。

このジャーニーの情報は、他のペルソナにとっても役に立ちますが、特定の役割には必要ない情報も一部あります。その他の役割に対応するジャーニーが今後公開され次第、随時お知らせします。

## ヘッドレスコンテンツ作成者ジャーニー {#the-journey}

このジャーニーでは、多くのトピックを参照します。以下の記事では、AEM でのヘッドレスに関する基本的な知識と、詳細な技術ドキュメントへのリンクを示します。

ジャーニーの特定の部分に直接移動することもできますが、多くの概念は、それまでの記事で紹介された概念に基づいています。したがって、AEM のヘッドレスを初めて使用する場合は、最初から順に進めることをお勧めします。

| # | 記事 | 説明 |
|---|---|---|
| 0 | AEM ヘッドレスコンテンツ作成者ジャーニー | このドキュメント |
| 1 | [AEM Headless as a Cloud Service 向けオーサリング - 概要](introduction.md) | Adobe Experience Manager as a Cloud Service のヘッドレス機能と、プロジェクトのコンテンツをオーサリングする方法を紹介します。 |
| 2 | [AEM を使用したヘッドレス向けのオーサリングの基本](basics.md) | コンテンツフラグメントを使用したヘッドレス CMS のコンテンツオーサリングの概念と仕組みについて説明します。 |
| 3 | [コンテンツフラグメントでの参照の使用について](references.md) | コンテンツフラグメントでの参照の使用方法について説明します。また、ネストされたフラグメントを使用して、ヘッドレス CMS の複数レベルの構造を作成および管理することもできます。 |
| 4 | [コンテンツフラグメントのメタデータとタグの定義について](metadata-tagging.md) | コンテンツフラグメントのメタデータとタグの定義について説明します。 |

## 次の手順 {#what-is-next}

これで、Adobe ヘッドレスジャーニーを開始する準備が整いました。このジャーニーの次のステップに進み、「[AEM ヘッドレスas a Cloud Serviceのオーサリング – 概要 ](introduction.md) を読むことをお勧めします。

<!--
### Choose Your Own Adventure {#choose-your-path}

However, Adobe wants you to succeed as you get started with your AEM Headless project, regardless of your learning style. So, consider these two options.

* If you prefer to continue to **learn about headless concepts and AEM's headless technologies**, you should continue your AEM headless journey as recommended by next reviewing the document [How to Model Your Content as AEM Content Models](model-your-content.md) where you learn how to model your content structure in AEM.
* If you prefer to **learn by doing**, you can jump to the [Getting Started with AEM Headless hands-on tutorial](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/graphql/multi-step/overview.html) where you will jump directly into AEM Headless development by implementing a simple project to expose AEM headless content.
-->

## その他のリソース {#additional-resources}

ドキュメントジャーニーでは、相互に関連する複雑なプロセスや機能をストーリーに従って読者に説明しながら、ビジネス上の問題を AEM で解決する方法を示します。1 つのジャーニーでは、複数の機能が連携して 1 つのビジネスニーズを満たす方法を示しています。

そのため、ジャーニーは、それぞれが独立して設計されています。ただし、そのいくつかは互いに関連付けられています。AEM の強力な機能の連携の仕組みについて詳しくは、次に示すその他のジャーニーを参照してください。

* [AEM ヘッドレス翻訳ジャーニー](/help/journey-headless/translation/overview.md) - このドキュメントジャーニーでは、ヘッドレステクノロジー、AEM によるヘッドレスコンテンツの提供方法、ヘッドレスコンテンツの翻訳方法について幅広く理解できます。
* [AEM ヘッドレスデベロッパージャーニー](/help/journey-headless/developer/overview.md) - AEM の強力で柔軟なヘッドレス機能、その性能、および初めての開発プロジェクトでの活用方法を説明するガイド付きジャーニーは、ここから始めてください。
* [ヘッドレスアーキテクトジャーニー](/help/journey-headless/architect/overview.md) - Adobe Experience Manager as a Cloud Service の強力で柔軟なヘッドレス機能と、プロジェクトのコンテンツをモデル化する方法の入門的解説が必要であれば、ここから始めてください。
* [AEM as a Cloud Service 技術ドキュメント](https://experienceleague.adobe.com/docs/experience-manager-cloud-service.html?lang=ja) - AEM およびヘッドレステクノロジーを既にしっかり理解している場合は、アドビの詳細な技術ドキュメントを直接参照することをお勧めします。
   * [ヘッドレス CMS としての AEM の概要](/help/headless/introduction.md)
* [AEM 開発者ポータル](https://experienceleague.adobe.com/landing/experience-manager/headless/developer.html?lang=ja)
* [AEM ヘッドレスチュートリアル](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/overview.html?lang=ja) - 技術指向の方が実践による学習を希望する場合は、API とフレームワーク別に整理された実践チュートリアルを利用してください。このチュートリアルでは、AEM ヘッドレスに基づくアプリケーションの作成と使用の詳細を紹介しています。
