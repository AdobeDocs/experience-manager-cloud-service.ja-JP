---
title: AEM Forms as a Cloud Service - デジタルフォームプラットフォーム
description: モジュラー型コンポーネントを使用して、デジタルフォームを構築、統合および最適化します。 アダプティブフォーム、データコネクタ、ワークフロー自動化、分析、管理ツールから選択して、強力なフォームエクスペリエンスを作成します。
landing-page-description: フォームの作成、データの統合、プロセスの自動化、分析、ガバナンスのための独立したコンポーネントを備えたモジュラー型デジタルフォームプラットフォーム。
keywords: AEM Forms, デジタルフォーム，フォームビルダー，アダプティブフォーム，フォーム統合，ワークフロー自動化，フォーム分析，ドキュメントサービス
role: Admin, Developer, User
feature: Adaptive Forms, Release Information
hide: true
hidefromtoc: true
index: false
exl-id: e8c37209-4d8e-4eaf-9e29-ffe32b841eb1
source-git-commit: eca09e1bf2ba4466f54e915e01218cc89cf5b116
workflow-type: tm+mt
source-wordcount: '1932'
ht-degree: 2%

---

# AEM Forms as a Cloud Service {#aem-forms-platform}

モジュラー型コンポーネントを使用して、デジタルフォームを構築、統合および最適化します。 AEM Formsは、連携またはスタンドアロンして、あらゆるビジネスニーズに対応する強力なフォームエクスペリエンスを作成する独立した製品を提供します。

シンプルなフォーム作成から複雑なドキュメントワークフロー、データ統合、アドバンス分析まで、必要なコンポーネントを選択します。

## 新機能 {#whats-new}

**最新リリースのハイライト：**

- **日時入力コンポーネント** - カレンダーおよび時計インターフェイスによるユーザー入力の強化
- **ファイルのアップロードセキュリティの強化** – 自動検証とコンテンツタイプのチェック
- **エラー処理の改善** - カスタム送信アクションの特定のエラーコードによるデバッグが向上しました。
- **レコードのドキュメントの機能強化** - クリーンなドキュメント生成用に非表示フィールドを除外するオプション

**プレリリース機能：**

- **AFP 形式のサポート** – 通信 API を使用したエンタープライズクラスの印刷機能
- **ルールエディターの機能強化** – 最新のJavaScript サポートと動的変数
- **強化された検証方法** - パネル、フィールド、フォームレベルの検証の改善

[の完全なリリースノート→表示](/help/release-notes/release-notes-cloud/release-notes-current.md#forms)

## アーリーアクセスプログラム {#early-access}

最先端のAEM Forms イノベーションに排他的にアクセスできます。

- **🤖AEM Forms AI アシスタント** - フォームの自動作成と最適化のためのジェネレーティブ AI
- 手書 **✍️署名コンポーネント** - フォーム内での直接署名キャプチャ
- **🔗Direct API Integration** - フォームデータモデルの設定を使用せずに API に接続
- **📊Formsの最適化** - AI を活用して、パフォーマンス分析とコンバージョンを改善します

[ アクセス→を要求 ](mailto:aem-forms-ea@adobe.com) | [→細情報 ](/help/forms/early-access-ea-features.md)

## 📋 フォームの作成とオーサリング {#form-creation}

ニーズや技術要件に最適なオーサリングアプローチを使用してフォームを作成します。

### コアコンポーネントForms {#core-components}

| **コアコンポーネントのForms** |
|---|
| 最新の web 標準規格を使用した、最新のレスポンシブフォームの構築。 複数のデバイスで自動的に動作するアダプティブフォームを作成し、API 駆動型配信用のヘッドレスフォームを作成します。 |
| **機能：** 最新のコンポーネント、自動レスポンシブデザイン、組み込みのアクセシビリティ機能を備えた視覚的なドラッグ&amp;ドロップフォームビルダーです。 |
| **用途：** 新規プロジェクト、最新の Web エクスペリエンス、ヘッドレスフォーム配信、モバイルファーストデザイン。 |
| ✅ レスポンシブデザイン ✅ アクセシビリティコンプライアンス ✅ ヘッドレス機能 ✅ 最新の UI コンポーネント |
| [ コアコンポーネント→の基本を学ぶ ](/help/forms/creating-adaptive-form-core-components.md) |

### 基盤コンポーネントのForms {#foundation-components}

| **基盤コンポーネントのForms** |
|---|
| 既存のプロジェクトと従来の統合に対するフォーム作成アプローチの確立。 豊富なカスタマイズオプションを備えた実証済みのコンポーネント。 |
| **機能：** 包括的なコンポーネントライブラリと広範なカスタマイズ機能を備えた、従来のアダプティブフォームの構築。 |
| **用途：** 既存のプロジェクト、従来のシステム統合、特定のカスタマイズ要件、確立されたワークフロー。 |
| ✅ 広範なコンポーネントライブラリ ✅ レガシー互換性 ✅ 高いカスタマイズ ✅ 確かな安定性 |
| [ 基盤コンポーネント→の概要 ](/help/forms/creating-adaptive-form.md) |

### Edge DeliveryForms {#edge-delivery}

| **Edge DeliveryForms** |
|---|
| Microsoft Excel などの使い慣れたツールを使用した、高性能なフォームの作成。 優れた読み込み速度と SEO パフォーマンスを実現します。 |
| **機能：** Excel スプレッドシートを使用してフォームを作成し、最適なGoogle Lighthouse スコアで高性能の Edge 配信ネットワークに公開します。 |
| **用途：** パフォーマンスクリティカルなアプリケーション、SEO に焦点を当てたプロジェクト、コンテンツ作成者によるフォーム作成、グローバルコンテンツ配信。 |
| ⚡ Excel ベースのオーサリング ⚡ 超高速読み込み ⚡ 最適な SEO ⚡ グローバル CDN 配信 |
| [Edge Delivery →の概要 ](/help/edge/docs/forms/overview.md) |

### HTML5 Forms {#html5-forms}

| **HTML5 Forms** |
|---|
| モバイルデバイスおよびレガシーブラウザー用に、XFA ベースのフォームをHTML5 としてレンダリングします。 ネイティブのモバイルエクスペリエンスを提供しながら、フォームロジックを維持します。 |
| **機能：** ネイティブのモバイルエクスペリエンスとクロスブラウザー対応により、XFA フォームテンプレートをHTML5 フォームに変換します。 |
| **使用するタイミング：** XFA フォームの最新化、モバイルの最適化、従来のブラウザーのサポート、既存の XDP 投資。 |
| 📱 XFA 互換性 📱 モバイル最適化 📱 クロスブラウザーサポート 📱 プラグイン要件なし |
| [HTML5 Forms →の概要 ](/help/forms/introductionhtml5.md) |

### インタラクティブ通信 {#interactive-communications}

| **インタラクティブコミュニケーション** |
|---|
| 動的なデータ統合を備えたビジュアルエディターを使用して、明細書、請求書、通知などのドキュメント中心のコミュニケーションを作成します。 |
| **機能：** 静的コンテンツと動的データを組み合わせ、印刷チャネルやデジタルチャネル向けにパーソナライズされたコミュニケーションを設計します。 |
| **用途：** 顧客の明細書、請求書、通知、パーソナライズされたコミュニケーション、大量のドキュメントを扱うワークフロー。 |
| Personalization📄 のマルチチャネル出力 📄Dynamic Data integration を使用した 📄 Visual Document Design 📄 |
| [ インタラクティブ通信→の概要 ](/help/forms/interactive-communication/create-interactive-communication.md) |

## 🔗 Data &amp; Integration {#data-integration}

フォームをバックエンドシステムおよびデータソースに接続して、シームレスな情報フローとリアルタイムのデータ交換を実現します。

### フォームデータモデル {#form-data-model}

| **フォームデータモデル** |
|---|
| 事前生成、検証、送信の機能を備えた、複数のデータソースに対する統合されたインターフェイス。 一貫したモデルの背後にある抽象的統合の複雑さ。 |
| **機能：** 一貫したインターフェイスとデータフロー管理を使用して、フォームを複数のバックエンドシステムに接続する統合データレイヤーを作成します。 |
| **用途：** 複数のデータソースの統合、複雑なデータの関係、事前母集団の要件、ライブデータに対する検証。 |
| データモデリング 🔄 の 🔄 ルチソース統合 🔄 事前母集団 🔄 検証ルール 🔄 統合インターフェイス |
| [ フォームデータモデル→の概要 ](/help/forms/create-form-data-models.md) |

### RESTful コネクタ {#restful-connectors}

| **RESTful コネクタ** |
|---|
| RESTful API を使用した、あらゆる web アクセス可能なサービスとの直接統合。 カスタム API および web サービスへの接続。 |
| **機能：** 送信アクションまたはデータ統合を使用してフォームから直接 API 呼び出しを有効にし、web サービスへのリアルタイム接続を実現します。 |
| **用途：** カスタム API 統合、Web サービス接続、リアルタイムのデータ交換、サードパーティのサービス統合。 |
| リアルタイム接続 🌐 の 🌐 Direct API 呼び出し 🌐 柔軟な統合 🌐 カスタムサービスサポート |
| [REST エンドポイントの設定→](/help/forms/configure-submit-action-restpoint.md) \| [ データ統合設定→](/help/forms/data-integration.md) |

### Salesforce コネクタ {#salesforce-connector}

| **Salesforce コネクタ** |
|---|
| Salesforce CRM とのネイティブ統合により、リード管理、顧客データの同期、セールスプロセスの自動化を実現します。 |
| **機能：** フォームデータの同期、リードの作成、顧客レコードの管理を備えた、Salesforce用の事前定義済みコネクタ。 |
| **用途：** Salesforce CRM 連携、リードジェネレーションフォーム、カスタマーデータ管理、セールスプロセスの自動化。 |
| 🏢 リード管理 🏢 データ同期 🏢 セールス自動化のための事前定義済みコネクタ 🏢 提供 |
| [Salesforce Integration →の設定 ](/help/forms/configure-salesforce.md) |

### Microsoft Dynamics コネクタ {#dynamics-connector}

| **Microsoft Dynamics コネクタ** |
|---|
| 包括的なビジネスプロセスをサポートする、ERP および CRM 接続用のMicrosoft Dynamicsとの大規模法人の統合。 |
| **機能：** 顧客管理、ビジネスプロセス統合、エンタープライズデータフローのために、フォームをMicrosoft Dynamicsに接続します。 |
| **用途：** Microsoft Dynamics統合、エンタープライズワークフロー、カスタマー管理、ビジネスプロセスの自動化。 |
| 🏭 Enterprise 接続 🏭 ビジネスプロセス統合 🏭 顧客管理 🏭 データ同期 |
| [Dynamics 統合→の設定 ](/help/forms/configure-msdynamics.md) |

### SharePoint コネクター {#sharepoint-connector}

| **SharePoint コネクタ** |
|---|
| SharePointとの Document Management の統合により、ファイルストレージ、共同作業、ドキュメントワークフローの自動化を実現。 |
| **機能：** 自動ドキュメント管理および共同作業の機能を使用して、フォーム送信および生成されたドキュメントをSharePointに保存します。 |
| **用途：** Document Management、チームの共同作業、ファイルストレージ、SharePoint ベースのワークフロー。 |
| Collaboration📁 の 📁 ドキュメントストレージ機能 📁 自動ワークフロー 📁SharePoint統合 |
| [SharePoint Integration →の設定 ](/help/forms/connect-forms-to-sharepoint-document-library.md) |

## プロセスとワークフロー {#process-workflow}

包括的なワークフローおよび処理機能により、ビジネス・プロセス、承認、ドキュメント生成を自動化します。

### AEM ワークフロー {#aem-workflows}

複雑なフォーム駆動型ワークフロー向けの複数手順の承認、タスクの割り当て、プロセスのオーケストレーションによるビジネスプロセスの自動化。

**機能：** 承認チェーン、タスクのルーティング、フォーム送信のプロセス監視を使用して、自動化されたビジネスプロセスを作成します。

**用途：** 承認プロセス、ビジネス自動化、タスク管理、複雑なワークフロー、プロセスのオーケストレーション。

**主な機能：** プロセスの自動化、承認チェーン、タスクのルーティング、プロセスの監視、ビジネスルール。

[AEM Workflows →の基本を学ぶ](/help/forms/aem-forms-workflow.md)

### Adobe Sign との統合 {#adobe-sign}

シームレスな署名プロセスを実現するために、フォームエクスペリエンスに直接統合された法的拘束力のあるデジタル署名を使用した電子サインワークフロー。

**機能：** 法的拘束力のある電子署名機能と自動署名ワークフローを使用して、フォーム内でデジタル署名を有効にします。

**用途：** 契約署名、法的文書、承認ワークフロー、コンプライアンス要件、署名の自動化。

**主な機能：** 法的電子サイン、署名ワークフロー、コンプライアンスサポート、自動プロセス。

[Adobe Sign →の設定](/help/forms/working-with-adobe-sign.md)

### 送信アクション {#submit-actions}

メール、データベースストレージ、ワークフロートリガー、カスタム処理など、複数の処理オプションを使用したフォーム送信処理。

**機能：** ユーザーがフォームを送信したときの動作、つまり、メール、データベース、ワークフロー、外部システムへのデータのルーティングを定義します。

**用途：** フォーム送信処理、データルーティング、通知システム、統合トリガー

**主な特長：** 複数の送信オプション、データルーティング、通知システム、統合トリガー。

[送信アクションの設定→](/help/forms/configure-submit-actions-core-components.md)

### 通信 API {#communication-apis}

大量のドキュメント処理と自動化を実現する RESTful API を使用した、プログラムによるドキュメント生成、操作、セキュリティ。

**機能：** PDFの作成、ドキュメントのアセンブリ、バッチ処理のための API を使用して、プログラムでドキュメントを生成、操作、保護します。

**用途：** ドキュメントの自動化、大量の処理、プログラムによる生成、ドキュメントのアセンブリ、バッチ操作。

**主な機能：** ドキュメント生成、バッチ処理、プログラム制御、ドキュメントセキュリティ、API 自動化。

[通信 API の基本を学ぶ→](/help/forms/aem-forms-cloud-service-communications-introduction.md)

## 分析と最適化 {#analytics-optimization}

包括的な分析およびテスト機能により、フォームのパフォーマンスを監視し、ユーザーの行動を理解し、コンバージョン率を最適化します。

### Adobe Analytics との統合 {#adobe-analytics}

データ駆動型最適化の完了率、放棄パターンおよびユーザー行動に関する詳細な分析を使用した、フォームパフォーマンストラッキング。

**機能：** 包括的なレポートを使用して、フォームのインタラクション、完了率、フィールドレベルの分析、ユーザーの行動パターンを追跡します。

**用途：** パフォーマンスの監視、コンバージョンの最適化、ユーザー行動の分析、データ駆動型の改善。

**主な機能：** パフォーマンストラッキング、ユーザー行動分析、コンバージョン指標、詳細レポート。

[Analytics 統合→の設定](/help/forms/integrate-aem-forms-with-adobe-analytics.md)

### トランザクションレポート {#transaction-reports}

デプロイメント全体での API 呼び出し、ドキュメント生成、請求可能なトランザクションに関する詳細なレポートを使用して、使用状況の監視と請求の透明性を確保する。

**機能：** 詳細な消費レポートとコストトラッキングを使用して、API の使用状況、ドキュメント生成量、請求可能なトランザクションを監視します。

**用途：** 使用状況の監視、コストトラッキング、キャパシティの計画、コンプライアンスレポート、リソースの最適化。

**主な機能：** 使用状況の追跡、コストの監視、キャパシティの計画、コンプライアンスのレポート作成など。

[トランザクションレポートの表示→](/help/forms/transaction-reports-billable-apis.md)

### A/B テストの統合 {#ab-testing}

コンバージョン向上のための統計分析を使用して、様々なレイアウト、フィールド配置、ユーザーフローをテストすることで、フォームを最適化します。

**機能：** 様々なフォームバリエーションをテストし、様々なユーザーセグメントやユースケースに最も効果的なアプローチを特定します。

**用途：** コンバージョンの最適化、ユーザーエクスペリエンスのテスト、パフォーマンスの向上、データ駆動型の設計決定。

**主な機能：** フォームテスト、統計分析、コンバージョンの最適化、パフォーマンスの比較。

[フォームの最適化→について学ぶ](/help/forms/view-understand-aem-forms-analytics-reports.md)

## 経営・ガバナンス {#management-governance}

企業規模のフォームのデプロイメントに対応する、一元化されたフォーム管理、ユーザーアクセス制御、ガバナンス機能。

### フォームポータル {#forms-portal}

検索機能、フォームの分類、ドラフト管理、送信の追跡を備えた、一元化されたフォームリポジトリを統一されたインターフェイスで実現します。

**機能：** ユーザーが検索とカテゴリ化を使用して、送信を検出、アクセス、ドラフト管理、追跡できる、一元化されたフォームリポジトリを作成します。

**用途：** フォーム検出、一元管理、ユーザーセルフサービス、ドラフト管理、送信トラッキング。

**主な機能：** フォーム検出、検索機能、ドラフト管理、送信トラッキング、ユーザーインターフェイス

[Forms Portal →の設定](/help/forms/configure-forms-portal.md)

### User Management {#user-management}

組織全体でのフォームの作成、編集、公開、管理に関する詳細な権限を持つ、役割ベースのアクセス制御。

**機能：** 詳細なアクセス制御とセキュリティを使用して、フォーム管理の様々な側面についてユーザーの役割と権限を定義します。

**用途：** アクセス制御、セキュリティ管理、役割定義、権限管理、組織ガバナンス。

**主な機能：** 役割ベースのアクセス、権限管理、セキュリティ制御、組織ガバナンス。

[User Management →の設定](/help/forms/forms-groups-privileges-tasks.md)

### バージョン管理 {#version-control}

バージョン追跡、変更履歴、ロールバック機能、コンプライアンスとガバナンスのための監査証跡を備えたライフサイクル管理を実現します。

**機能：** フォームバージョンの追跡、変更履歴の維持、ロールバックの有効化、コンプライアンスおよびガバナンスの要件に対する監査証跡の提供を行います。

**用途：** 変更管理、コンプライアンス要件、監査証跡、バージョン管理、ガバナンス・プロセス

**主な機能：** バージョン追跡、変更履歴、ロールバック機能、監査証跡、コンプライアンスのサポート。

[バージョン管理→について説明します](/help/forms/add-comments-annotations-versioning-adaptive-form-core-components.md)

## 製品別スタートガイド {#getting-started}

当面のニーズと技術要件に基づいて出発点を選択します。

### フォーム作成のクイックスタート {#form-creation-start}

**最新のプロジェクトの場合：** コアコンポーネントのForms[ から開始 ](/help/forms/creating-adaptive-form-core-components.md)

**高いパフォーマンスを実現する場合：**[Edge Delivery Formsから開始 ](/help/edge/docs/forms/overview.md)

**既存のプロジェクトの場合：** 基盤コンポーネントのForms[ から開始 ](/help/forms/creating-adaptive-form.md)

**XFA 最新化の場合：**[HTML5 Formsから開始 ](/help/forms/introductionhtml5.md)

**ドキュメント通信の場合：** 開始 [ インタラクティブ通信 ](/help/forms/interactive-communication/create-interactive-communication.md)

### データ統合のクイックスタート {#integration-start}

**複数のデータソースの場合：** フォームデータモデル [ から開始 ](/help/forms/create-form-data-models.md)

**Salesforce CRM の場合：**[Salesforce コネクタで開始 ](/help/forms/configure-salesforce.md)

**Microsoft Dynamicsの場合：** Dynamics コネクタ [ から開始 ](/help/forms/configure-msdynamics.md)

**カスタム API の場合：** RESTful コネクタから開始 [ ます ](/help/forms/configure-submit-action-restpoint.md)

**ドキュメントストレージの場合：**[SharePoint コネクタで開始 ](/help/forms/connect-forms-to-sharepoint-document-library.md)

### プロセス自動化のクイックスタート {#workflow-start}

**承認プロセスの場合：**[AEM ワークフローから開始 ](/help/forms/aem-forms-workflow.md)

**電子サインの場合：** Adobe Sign 統合 [ から開始 ](/help/forms/working-with-adobe-sign.md)

**送信処理の場合：** 送信アクション [ から開始 ](/help/forms/configure-submit-actions-core-components.md)

**ドキュメント生成用：** 通信 API[ から開始 ](/help/forms/aem-forms-cloud-service-communications-introduction.md)

### Analytics クイックスタート {#analytics-start}

**パフォーマンストラッキングの場合：**[Adobe Analytics統合から開始 ](/help/forms/integrate-aem-forms-with-adobe-analytics.md)

**使用状況の監視の場合：** トランザクションレポート [ から開始 ](/help/forms/transaction-reports-billable-apis.md)

**最適化に関するインサイトの場合：** [ 分析レポート ](/help/forms/view-understand-aem-forms-analytics-reports.md) から開始

### 管理のクイックスタート {#management-start}

**フォーム検出の場合：** [Forms ポータルから開始 ](/help/forms/configure-forms-portal.md)

**アクセス制御の場合：** User Management[ から開始 ](/help/forms/forms-groups-privileges-tasks.md)

**変更追跡の場合：** [ バージョン管理 ](/help/forms/add-comments-annotations-versioning-adaptive-form-core-components.md) から開始

## アーキテクチャとデプロイメント {#architecture}

包括的な実装ガイダンス：

- **[アーキテクチャパターンのレビュー](/help/forms/aem-forms-cloud-service-architecture.md)** によるスケーラブルな導入
- チーム共同作業のための **[開発環境の設定](/help/forms/setup-local-development-environment.md)**
- 既存のシステムからの **[移行戦略の計画](/help/forms/migrate-to-forms-as-a-cloud-service.md)**

## サポートとリソース {#support}

- **ヘルプセンター** – 実装とトラブルシューティングに関するサポートを受けることができます
- **コミュニティフォーラム** – 他のAEM Forms ユーザーやエキスパートとつながります
- **プロフェッショナルサービス** - Adobe コンサルティングによる大規模導入
- **トレーニングと資格認定** - AEM Forms機能の専門知識を開発します

*強力なフォームエクスペリエンスを構築するために必要なコンポーネントを選択します。 各製品は個別に動作するか、他の製品と組み合わせて、ビジネス要件に合わせた包括的なソリューションを作成します。*
