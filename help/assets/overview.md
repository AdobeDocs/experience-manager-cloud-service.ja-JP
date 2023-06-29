---
title: Assets as a [!DNL Cloud Service] の概要
description: Assets as a [!DNL Cloud Service] の最新機能
contentOwner: AG
feature: Asset Management
role: User,Leader,Architect
exl-id: 4437f214-d058-4975-8b8f-869a12c8103b
source-git-commit: 5a7938d5e52388516f8b66bbcf8ffdee332a51a3
workflow-type: tm+mt
source-wordcount: '740'
ht-degree: 67%

---

# Assets as a [!DNL Cloud Service] の概要  {#assets-cloud-service-introduction}

<!-- Need review information from gklebus -->

Adobe Experience Manager Assets as a [!DNL Cloud Service] は、クラウドネイティブな PaaS ソリューションです。企業がデジタルアセット管理と Dynamic Media 操作を迅速かつ効果的に行うためだけでなく、常に最新で常に可用性が高く常に学習可能なシステム内から AI や機械学習などの次世代スマート機能を使用するうえでも役に立ちます。

大量のアセットや複雑なアセットを同時に取り込む作業は、Experience Manager オーサーインスタンスにとってリソースを消費することになります。アセットの追加、処理、移行時に、プライマリインスタンスは CPU の処理能力、メモリ容量、I/O リソースを大量に消費します。このようなパフォーマンス上の問題は、エンドユーザーのオーサリングおよび閲覧操作に影響を与えます。

企業では、マルチデバイス、地域横断、多言語の使用例について、様々なファイル形式とコンテンツ解像度をサポートする必要があります。アセットの処理とストレージの要件に基づいて必要になるリソースと機能によっては、従来のソリューションに過度の負担がかかるおそれがあります。また、アセット処理の技術的な制限事項によって、望ましい結果が得られないこともあれば、ストレージのコストが利益率の低下を招くこともあります。

まず、[クラウドネイティブな製品／サービスのメリット](#solution-benefits)を理解します。[Experience Manager as a [!DNL Cloud Service]](/help/release-notes/aem-cloud-changes.md) の主な変更点を確認します。これらの変更は Experience Manager Assets にも影響を及ぼします（[Assets の主な変更点](/help/assets/assets-cloud-changes.md)を参照）。

[新しい Assets の機能の詳細](#whats-new-assets)と[既知の問題](/help/release-notes/maintenance/latest.md)を理解します。[非推奨（廃止予定）または削除された機能](/help/release-notes/deprecated-removed-features.md)リストを参照して、このリリースで削除された機能を確認してください。最後に、この[用語集](/help/overview/terminology.md)を利用して Experience Manager の用語を理解します。

## ソリューションのメリット {#solution-benefits}

AEM Assets as a [!DNL Cloud Service] の主なメリットは次のとおりです。詳しくは、[Adobe Experience Manager as a [!DNL Cloud Service]](/help/overview/introduction.md) の概要を参照してください。

* **アセット処理のための最新のクラウドサービス**：新しいアセットマイクロサービスは、クラウドベースで、拡張性と信頼性に優れ、手間のかからないアセット処理サービスです。
* **高い拡張性**：あらゆるタイプのデプロイメントに対応できる柔軟な拡張性があります。必要に応じて、実質的に無制限のリソースをオンデマンドで利用できます。従来のシステムと比較して、必要以上に高機能な設計にならないようにすることで設計のコストを削減できます。
* **最新のソフトウェア**：常に最新で、常に更新されています。すべてのユーザーが、利用できるすべてのパッチ、機能、セキュリティ、バグ修正を含んだ最新のソフトウェアだけを使用します。開発者とインテグレーターは最新の API セットを使用して作業し、マルチバージョンのサポートに関する問題を回避できます。
* **常にオンライン**：バックアップと冗長性を備えたクラスターにデプロイされたインスタンスのおかげで、ダウンタイムなし（0dt）を実現しています。アップグレードも 0dt です。
* **継続的な監視**：システムの監視は自動化され、組み込みのチェックとトリガーがパフォーマンス、可用性、全体的な堅牢性の維持に役立ちます。
* **手間のかからないデプロイメント**：Experience Manager as a Cloud Service の操作は完全に自動化されており、手動の介入は不要です。自動デプロイメントを行うために、カスタムコードを含んだデプロイ可能な Docker イメージのビルドを Cloud Manager（CM）コンポーネントで自動化します。

## 利用可能なペルソナベースのエクスペリエンス {#persona-based-experiences}

アドビでは、デジタルアセットを最大限に活用するための堅牢なデジタルアセット管理（DAM）ソリューションを提供しています。Adobe Experience Manager Assets には、同じ Assets リポジトリを使用する 2 つの異なるエクスペリエンスがCloud Servicesされます。

* **管理ビュー**:既存の Assets as a Cloud Serviceユーザーインターフェイス。 管理ビューは、統合、ワークフロー、コンテンツの自動化、公開など、すべての高度なアセット管理機能に使用できます。

* **アセット表示**:Adobeの軽量なアセット管理エクスペリエンスで、デジタルアセットの保存、管理、検出、使用が可能です。 合理化されたユーザーインターフェイスに、重要なアセット管理機能が含まれています。 アップロード、メタデータの管理、検索、ダウンロード、共有に重点を置いた軽量な DAM ユーザー向けに設計されています。

管理者表示へのアクセス権を持つユーザーは、 Assets 表示にもアクセスできます。 Assets ビューにはシンプルなユーザーインターフェイスが用意されており、デジタルアセットの管理、検出、配布が容易になります。 クリエイティブ、マーケティング、事業部門のチームを含む、様々な機能を持つ幅広いユーザーは、アセットに関して共同作業を行い、必要に応じて適切な承認済みアセットにアクセスできます。 多くのカジュアルな DAM ユーザーは、機能のサブセットのみを含むので、アセットビューを好みます。 このエクスペリエンスの対象は、クリエイティブ、読み取り専用のアセット消費者、より軽量な DAM ユーザーです。

DAM ライブラリアリント、開発者およびスーパーユーザーは、必要に応じて、引き続き管理者ビューを使用したり、ユーザーインターフェイスを切り替えたりできます。 自分の役割に最適なエクスペリエンスを選択できます。

![add-tags](assets/newui-overview.svg)

Assets ビューへのアクセス方法と、Admin ビューで提供される簡略化について詳しくは、 [Assets ビューの概要](/help/assets/assets-view-introduction.md).

## 新しい Assets の機能 {#whats-new-assets}

重要な新機能は次のとおりです。

* [アセットマイクロサービス](/help/assets/asset-microservices-overview.md)
* [アセットのアップロード方法](/help/assets/add-assets.md)

**関連情報**

* [アセットを翻訳](translate-assets.md)
* [Assets HTTP API](mac-api-assets.md)
* [AEM Assets as a Cloud Service でサポートされているファイル形式](file-format-support.md)
* [アセットの検索](search-assets.md)
* [Connected Assets](use-assets-across-connected-assets-instances.md)
* [アセットレポート](asset-reports.md)
* [メタデータスキーマ](metadata-schemas.md)
* [アセットのダウンロード](download-assets-from-aem.md)
* [メタデータの管理](manage-metadata.md)
* [検索ファセット](search-facets.md)
* [コレクションの管理](manage-collections.md)
* [一括メタデータ読み込み](metadata-import-export.md)
