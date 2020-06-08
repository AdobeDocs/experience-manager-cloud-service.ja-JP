---
title: Assets as a Cloud Service の概要
description: Assets as a Cloud Service の新機能。
contentOwner: AG
translation-type: tm+mt
source-git-commit: 26833f59f21efa4de33969b7ae2e782fe5db8a14
workflow-type: tm+mt
source-wordcount: '479'
ht-degree: 100%

---


# Assets as a Cloud Service の概要 {#assets-cloud-service-introduction}

<!-- Need review information from gklebus -->

Adobe Experience Manager Assets as a Cloud Service は、クラウドネイティブな PaaS ソリューションです。企業がデジタルアセット管理と Dynamic Media 操作を迅速かつ効果的におこなうだけでなく、常に最新で常に可用性が高く常に学習可能なシステム内から AI や機械学習などの次世代スマート機能を使用するうえでも役に立ちます。

大量のアセットや複雑なアセットを同時に取り込む作業は、AEM オーサーインスタンスにとってリソースを消費することになります。アセットの追加、処理、移行時に、プライマリインスタンスは CPU の処理能力、メモリ容量、I/O リソースを大量に消費します。このようなパフォーマンス上の問題は、エンドユーザーのオーサリングおよび閲覧操作に影響を与えます。

企業では、マルチデバイス、地域横断、多言語の使用例について、様々なファイル形式とコンテンツ解像度をサポートする必要があります。アセットの処理とストレージの要件に基づいて必要になるリソースと機能によっては、従来のソリューションに過度の負担がかかるおそれがあります。また、アセット処理の技術的な制限事項によって、望ましい結果が得られないこともあれば、ストレージのコストが利益率の低下を招くこともあります。

まず、[クラウドネイティブな製品／サービスのメリット](#solution-benefits)を理解します。[AEM as a Cloud Service の主な変更点](/help/release-notes/aem-cloud-changes.md)を確認します。これらの変更は Experience Manager Assets にも影響を及ぼします（[Assets の主な変更点](/help/assets/assets-cloud-changes.md)を参照）。

[新しい Assets の機能の詳細](#whats-new-assets)と[既知の問題](/help/release-notes/known-issues.md)を理解します。本リリースで削除された機能を確認するには、[非推奨（廃止予定）の機能と削除された機能](/help/release-notes/deprecated-removed-features.md)のリストを参照します。また、近日中にリリースされる機能を確認するには、[今後予定されている Assets の機能](/help/release-notes/known-issues.md#upcoming-assets-capabilities)を参照します。最後に、この[用語集](/help/overview/terminology.md)を利用して AEM の用語を理解します。

## ソリューションのメリット {#solution-benefits}

AEM Assets as a Cloud Service の主なメリットは次のとおりです。詳しくは、[Adobe Experience Manager as a Cloud Service の概要](/help/overview/introduction.md)を参照してください。

* **アセット処理のための最新の Cloud Service**：新しいアセットマイクロサービスは、クラウドベースで、拡張性と信頼性に優れ、手間のかからないアセット処理サービスです。
* **高い拡張性**：あらゆるタイプのデプロイメントに対応できる柔軟な拡張性があります。必要に応じて、実質的に無制限のリソースをオンデマンドで利用できます。従来のシステムと比較して、必要以上に高機能な設計にならないようにすることで設計のコストを削減できます。
* **最新のソフトウェア**：常に最新で、常に更新されています。すべてのユーザーが、利用できるすべてのパッチ、機能、セキュリティ、バグ修正を含んだ最新のソフトウェアだけを使用します。開発者とインテグレーターは最新の API セットを使用して作業し、マルチバージョンのサポートに関する問題を回避できます。
* **常にオンライン**：バックアップと冗長性を備えたクラスターにデプロイされたインスタンスのおかげで、ダウンタイムなし（0dt）を実現しています。アップグレードも 0dt です。
* **継続的な監視**：システムの監視は自動化され、組み込みのチェックとトリガーがパフォーマンス、可用性、全体的な堅牢性の維持に役立ちます。
* **手間のかからないデプロイメント**：AEM as a Cloud Service の操作は完全に自動化され、手動の介入は不要です。自動デプロイメントをおこなうために、カスタムコードを含んだデプロイ可能な Docker イメージのビルドを Cloud Manager（CM）コンポーネントで自動化します。

## 新しい Assets の機能 {#whats-new-assets}

重要な新機能は次のとおりです。

* [アセットマイクロサービス](/help/assets/asset-microservices-overview.md)
* [アセットのアップロード方法](/help/assets/add-assets.md)
