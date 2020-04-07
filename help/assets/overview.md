---
title: AEM Assets as a Cloud Service の概要
description: AEM Assets as a Cloud Service の新機能。
contentOwner: AG
translation-type: tm+mt
source-git-commit: 26833f59f21efa4de33969b7ae2e782fe5db8a14

---


# AEM Assets as a Cloud Service の概要 {#assets-cloud-service-introduction}

<!-- Need review information from gklebus -->

Adobe Experience Manager Assets as a Cloud Service は、クラウドネイティブな PaaS ソリューションです。企業がデジタルアセット管理と Dynamic Media 操作を迅速かつ効果的におこなうだけでなく、常に最新で常に可用性が高く常に学習可能なシステム内から AI や機械学習などの次世代スマート機能を使用するうえでも役に立ちます。

多くのアセットまたは複雑なアセットを同時に取り込むのは、AEM Authorインスタンスのタスクを大量に消費するものです。 アセットの追加、処理、移行時に、プライマリインスタンスは CPU の処理能力、メモリ容量、I/O リソースを大量に消費します。このようなパフォーマンスの問題は、エンドユーザーのオーサリングと閲覧の操作に影響を与えます。

企業では、マルチデバイス、地域横断、多言語の使用例について、様々なファイル形式とコンテンツ解像度をサポートする必要があります。アセットの処理とストレージの要件に基づいて必要になるリソースと機能によっては、従来のソリューションに過度の負担がかかるおそれがあります。また、アセット処理の技術的な制限事項によって、望ましい結果が得られないこともあれば、ストレージのコストが利益率の低下を招くこともあります。

まず、[クラウドネイティブな製品／サービスのメリット](#solution-benefits)を理解します。Check out the notable [changes to AEM as a Cloud Service](/help/release-notes/aem-cloud-changes.md) that also impact Experience Manager Assets followed up the notable [changes to Assets](/help/assets/assets-cloud-changes.md).

[新しい Assets の機能の詳細](#whats-new-assets)と[既知の問題](/help/release-notes/known-issues.md)を理解します。See a list of [deprecated or removed functionality](/help/release-notes/deprecated-removed-features.md) to know what is removed in this release and see this [list of upcoming capabilities](/help/release-notes/known-issues.md#upcoming-assets-capabilities) to know what&#39;s coming shortly. 最後に、この[用語集](/help/overview/terminology.md)を利用して AEM の用語を理解します。

## ソリューションのメリット {#solution-benefits}

AEM Assets as a Cloud Service の主なメリットは次のとおりです。詳しくは、[Adobe Experience Manager as a Cloud Service の概要](/help/overview/introduction.md)を参照してください。

* **アセット処理のための最新のクラウドサービス**：新しいアセットマイクロサービスは、クラウドベースで、拡張性と信頼性に優れ、手間のかからないアセット処理サービスです。
* **高い拡張性**：あらゆるタイプのデプロイメントに対応できる柔軟な拡張性があります。必要に応じて、実質的に無制限のリソースをオンデマンドで利用できます。従来のシステムと比較して、必要以上に高機能な設計にならないようにすることで設計のコストを削減できます。
* **最新のソフトウェア**：常に最新で、常に更新されています。すべてのユーザーが、利用できるすべてのパッチ、機能、セキュリティ、バグ修正を含んだ最新のソフトウェアだけを使用します。開発者とインテグレーターは最新の API セットを使用して作業し、マルチバージョンのサポートに関する問題を回避できます。
* **常にオンライン**：バックアップと冗長性を備えたクラスターにデプロイされたインスタンスのおかげで、ダウンタイムなし（0dt）を実現しています。アップグレードも 0dt です。
* **継続的な監視**：システムの監視は自動化され、組み込みのチェックとトリガーがパフォーマンス、可用性、全体的な堅牢性の維持に役立ちます。
* **手間のかからない導入**:AEMのクラウド操作は完全に自動化され、手動の介入は不要です。 自動デプロイの場合、Cloud Manager(CM)コンポーネントは、カスタムコードを含むデプロイ可能なDockerイメージのビルドを自動化します。

## 新しい Assets の機能 {#whats-new-assets}

重要な新機能は次のとおりです。

* [アセットマイクロサービス](/help/assets/asset-microservices-overview.md)
* [アセットのアップロード方法](/help/assets/add-assets.md)
