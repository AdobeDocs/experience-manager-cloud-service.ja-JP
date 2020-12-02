---
title: ' [!DNL Cloud Service]としてのアセットの概要'
description: ' [!DNL Cloud Service]としてのアセットの新機能。'
contentOwner: AG
translation-type: tm+mt
source-git-commit: 5be8ab734306ad1442804b3f030a56be1d3b5dfa
workflow-type: tm+mt
source-wordcount: '465'
ht-degree: 79%

---


# [!DNL Cloud Service] {#assets-cloud-service-introduction}としてアセットを紹介

<!-- Need review information from gklebus -->

[!DNL Cloud Service]クラウドネイティブのPaaSソリューションとしてのAdobe Experience Managerアセットは、デジタルアセット管理とダイナミックメディアの処理を高速かつ影響を与えるだけでなく、常に最新で常に利用可能で、常に学習可能な次世代のスマート機能を利用できます。

大量のアセットや複雑なアセットを同時に取り込む作業は、AEM オーサーインスタンスにとってリソースを消費することになります。アセットの追加、処理、移行時に、プライマリインスタンスは CPU の処理能力、メモリ容量、I/O リソースを大量に消費します。このようなパフォーマンス上の問題は、エンドユーザーのオーサリングおよび閲覧操作に影響を与えます。

企業では、マルチデバイス、地域横断、多言語の使用例について、様々なファイル形式とコンテンツ解像度をサポートする必要があります。アセットの処理とストレージの要件に基づいて必要になるリソースと機能によっては、従来のソリューションに過度の負担がかかるおそれがあります。また、アセット処理の技術的な制限事項によって、望ましい結果が得られないこともあれば、ストレージのコストが利益率の低下を招くこともあります。

まず、[クラウドネイティブな製品／サービスのメリット](#solution-benefits)を理解します。[AEM as a の主な変更点 [!DNL Cloud Service]](/help/release-notes/aem-cloud-changes.md)を確認します。これらの変更は Experience Manager Assets にも影響を及ぼします（[Assets の主な変更点](/help/assets/assets-cloud-changes.md)を参照）。

[新しい Assets の機能の詳細](#whats-new-assets)と[既知の問題](/help/release-notes/known-issues.md)を理解します。本リリースで削除された機能を確認するには、[非推奨（廃止予定）の機能と削除された機能](/help/release-notes/deprecated-removed-features.md)のリストを参照します。また、近日中にリリースされる機能を確認するには、[今後予定されている Assets の機能](/help/release-notes/known-issues.md#upcoming-assets-capabilities)を参照します。最後に、この[用語集](/help/overview/terminology.md)を利用して AEM の用語を理解します。

## ソリューションのメリット {#solution-benefits}

[!DNL Cloud Service]としてのアセットの主な利点は次のとおりです。 詳しくは、[Adobe Experience Manager as a の概要 [!DNL Cloud Service]](/help/overview/introduction.md)を参照してください。

* **最新のアセット処理サービス**:新しいアセットマイクロサービスは、クラウドベースで、拡張性が高く、信頼性が高く、手間のかからないアセット処理サービスです。
* **高い拡張性**：あらゆるタイプのデプロイメントに対応できる柔軟な拡張性があります。必要に応じて、実質的に無制限のリソースをオンデマンドで利用できます。従来のシステムと比較して、必要以上に高機能な設計にならないようにすることで設計のコストを削減できます。
* **最新のソフトウェア**：常に最新で、常に更新されています。すべてのユーザーが、利用できるすべてのパッチ、機能、セキュリティ、バグ修正を含んだ最新のソフトウェアだけを使用します。開発者とインテグレーターは最新の API セットを使用して作業し、マルチバージョンのサポートに関する問題を回避できます。
* **常にオンライン**：バックアップと冗長性を備えたクラスターにデプロイされたインスタンスのおかげで、ダウンタイムなし（0dt）を実現しています。アップグレードも 0dt です。
* **継続的な監視**：システムの監視は自動化され、組み込みのチェックとトリガーがパフォーマンス、可用性、全体的な堅牢性の維持に役立ちます。
* **手間のかからないデプロイメント**：AEM as a Cloud Service の操作は完全に自動化され、手動の介入は不要です。自動デプロイメントをおこなうために、カスタムコードを含んだデプロイ可能な Docker イメージのビルドを Cloud Manager（CM）コンポーネントで自動化します。

## 新しい Assets の機能 {#whats-new-assets}

重要な新機能は次のとおりです。

* [アセットマイクロサービス](/help/assets/asset-microservices-overview.md)
* [アセットのアップロード方法](/help/assets/add-assets.md)
