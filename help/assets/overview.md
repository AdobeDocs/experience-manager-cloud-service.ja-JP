---
title: AEM Assets as a Cloud Service の概要
description: クラウドサービスとしてのアセットの新機能を参照してください。
contentOwner: AG
translation-type: tm+mt
source-git-commit: 068195919c4bf73c41b1156eadb47544e4c41e65

---


# Introducing Assets as a Cloud Service {#assets-cloud-service-introduction}

<!-- Need review information from gklebus -->

クラウドサービスオファーとしてのAdobe Experience Manager Assetsは、デジタルアセット管理とダイナミックメディアの処理を迅速かつ効果的に行うだけでなく、常に最新で常に利用可能で常に学習可能なシステム内でAI/MLなどの次世代のスマート機能を使用する、クラウドネイティブのPaaSソリューションです。

多くのアセットまたは複雑なアセットを同時に取り込むのは、AEM Authorインスタンスのタスクを大量に消費するものです。 アセットが追加、処理または移行された場合、プライマリ・インスタンスは、CPU、メモリ、I/Oリソースを大量に消費します。 このようなパフォーマンスの問題は、エンドユーザーのオーサリングと閲覧の操作に影響を与えます。

複数デバイス、地域間、多言語の使用例では、様々なファイル形式やコンテンツ解像度のサポートが必要です。 資産の処理とストレージの要件は、従来のソリューションに負担をかける可能性のあるリソースと機能を必要とします。 時には、資産処理の技術的な制限が望ましい結果を生み出さず、また、ストレージのコストが利益率の低下を招くこともあります。

まず、クラウドのネイティブ [製品のメリットを理解します](#solution-benefits)。 Experience Manager Assetsにも影響を与え [るクラウドサービスとしてのAEMに対する注目すべき変更を確認し](/help/release-notes/aem-cloud-changes.md) 、その後アセットに対する注目すべき変更 [を確認します](/help/assets/assets-cloud-changes.md)。

新しいアセット機能の詳 [細と既知の問題について](#whats-new-assets) 、以下を [参照します](/help/release-notes/known-issues.md)。 このリリースで削除さ [れた機能のリストを確認するには](/help/release-notes/deprecated-removed-features.md) 、廃止または削除された機能のリストを参照し、今後の機能に関するこの [](/help/release-notes/known-issues.md#upcoming-assets-capabilities) を参照して、近日の予定を確認してください。 最後に、この用語集の助けを借りてAEMの用語を理解し [ます](/help/overview/terminology.md)。

## ソリューションの利点 {#solution-benefits}

アセットをクラウドサービスとして使用する主な利点は、次のとおりです。 詳しくは、Experience Managerの概要をク [ラウドサービスとして参照してください](/help/overview/introduction.md)。

* **最新のアセット処理向けクラウドサービス**:新しいアセットマイクロサービスは、クラウドベースで、拡張性と信頼性に優れ、手間のかからないアセット処理サービスです。
* **高い拡張性**:あらゆるタイプの導入で柔軟な拡張性を実現。 必要に応じて、オンデマンドで利用可能なリソースを実用的に無制限に利用できます。 従来のシステムと比較して、設計のオーバーデザインのコストを節約します。
* **最新のソフトウェア**:常に最新で、常に更新。 すべてのユーザーが使用できるパッチ、機能、セキュリティ、およびバグの修正をすべて備えた最新のソフトウェアのみを持っています。 開発者とインテグレーターは、複数バージョンのサポートの問題を抱えない最新のAPIセットを扱います。
* **常にオンライン**:バックアップと冗長性を備えたクラスターに展開されたインスタンスにより、ダウンタイムがゼロ(0dt)。 アップグレードも0dtです。
* **継続的な監視**:システムの監視は、自動化され、組み込みのチェックとトリガーによって、パフォーマンス、可用性、全体的な堅牢性を維持します。
* **手間のかからない導入**:AEMのクラウド操作は完全に自動化され、手動の介入は不要です。 自動デプロイの場合、Cloud Manager(CM)コンポーネントは、カスタムコードを含むデプロイ可能なDockerイメージのビルドを自動化します。

## 新しいアセット機能 {#whats-new-assets}

重要な新機能は次のとおりです。

* [資産マイクロサービス](/help/assets/asset-microservices-overview.md)
* [アセットのアップロード方法](/help/assets/add-assets.md)
