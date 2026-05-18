---
title: AEM Forms as a Cloud Service - デジタルフォームプラットフォーム
description: モジュール式コンポーネントを使用して、デジタルフォームを作成、統合、最適化できます。 アダプティブフォーム、データコネクタ、ワークフロー自動化、分析、管理ツールなどから選択し、強力なフォームエクスペリエンスを作成できます。
landing-page-description: フォームの作成、データ統合、プロセスの自動化、分析、ガバナンスのための独立したコンポーネントを備えたモジュール式のデジタルフォームプラットフォーム。
keywords: AEM Forms, デジタルフォーム，フォームビルダー，アダプティブフォーム，フォーム統合，ワークフローオートメーション，フォーム分析，ドキュメントサービス
role: Admin, Developer, User
feature: Adaptive Forms, Release Information
hide: true
index: false
badgeSaas: label="AEM Forms" type="Positive" tooltip="AEM Formsに適用）。"
exl-id: e8c37209-4d8e-4eaf-9e29-ffe32b841eb1
source-git-commit: 77f7d21eed1322de768ee07e3518638f60e3ae40
workflow-type: tm+mt
source-wordcount: '1990'
ht-degree: 2%

---

# AEM Forms as a Cloud Service {#aem-forms-platform}

モジュール式コンポーネントを使用して、デジタルフォームを作成、統合、最適化できます。 AEM Formsは、独立したアプリケーションを提供します。それらを連携またはスタンドアロンで使用することにより、あらゆるビジネスニーズに対応したパワフルなフォーム体験を実現できます。

シンプルなフォームの作成から複雑なドキュメントワークフロー、データ統合、高度な分析に至るまで、必要なコンポーネントを選択できます。

## 新機能 {#whats-new}

**最新のリリースのハイライト：**

- **日付と時刻の入力コンポーネント** - カレンダーと時計のインターフェイスを使用したユーザー入力の強化
- **強化されたファイル アップロード セキュリティ** – 自動検証とコンテンツ タイプの確認
- **エラー処理の改善** - カスタム送信アクション用の特定のエラーコードを使用したデバッグの改善
- **レコードのドキュメントの機能強化** – よりクリーンなドキュメント生成用の非表示フィールドを除外するオプション

**プレリリース機能：**

- **AFP形式のサポート** – 通信APIを備えたエンタープライズグレードの印刷機能
- **ルールエディターの機能強化** – 最新のJavaScriptのサポートと動的変数
- **強化検証方法** - パネル、フィールド、フォームレベルの検証の改善

[リリースノートを見る→](/help/release-notes/release-notes-cloud/release-notes-current.md#forms)

## 早期アクセスプログラム {#early-access}

AEM Formsの最先端イノベーションに、誰もがアクセスできます。

- **🤖AEM Forms AI アシスタント** – 自動フォーム作成と最適化のための生成AI
- **✍️手書き署名コンポーネント** - フォーム内の直接署名キャプチャ
- **🔗ダイレクト API統合** - フォームデータモデルの設定なしでAPIに接続
- **📊Forms Optimization** - AIを活用したパフォーマンス分析とコンバージョンの改善

[&#x200B; アクセスを要求→](mailto:aem-forms-ea@adobe.com) | [詳細情報→](/help/forms/early-access-ea-features.md)

## 📋 フォーム作成とオーサリング {#form-creation}

ニーズや技術要件に最も適したオーサリングアプローチを使用して、フォームを作成できます。

### コアコンポーネントForms {#core-components}

| **コアコンポーネント Forms** |
|---|
| 最新のweb標準を使用した、モダンなレスポンシブフォーム作成。 デバイスをまたいで自動的に動作するアダプティブフォームを作成し、API ドリブン型の配信用のヘッドレスフォームを作成します。 |
| **機能：**&#x200B;最新のコンポーネント、自動レスポンシブデザイン、組み込みのアクセシビリティ機能を備えた視覚的なドラッグ&amp;ドロップ操作のフォームビルダー。 |
| **使用するタイミング：**&#x200B;新しいプロジェクト、最新のweb エクスペリエンス、ヘッドレスフォーム配信、モバイルファーストのデザイン。 |
| ✅ レスポンシブデザイン ✅ アクセシビリティコンプライアンス ✅ ヘッドレス機能✅ モダン UI コンポーネント |
| [&#x200B; コアコンポーネントの概要→](/help/forms/creating-adaptive-form-core-components.md) |

### 基盤コンポーネント Forms {#foundation-components}

| **基盤コンポーネント Forms** |
|---|
| 既存プロジェクトと従来の統合に対するフォーム構築アプローチを確立。 豊富なカスタマイズオプションを備えた実績のあるコンポーネント。 |
| **機能：**&#x200B;包括的なコンポーネントライブラリと広範なカスタマイズ機能を備えた従来のアダプティブフォームの作成。 |
| **使用するタイミング：**&#x200B;既存プロジェクト、レガシーシステム統合、特定のカスタマイズ要件、確立されたワークフロー。 |
| ✅広範なコンポーネントライブラリ ✅詳細カスタマイズ ✅従来の互換性✅実績のある安定性 |
| [基盤コンポーネントの概要→](/help/forms/creating-adaptive-form.md) |

### Edge Delivery Forms {#edge-delivery}

| **Edge Delivery Forms** |
|---|
| Microsoft Excelなどの使い慣れたツールを使用して、高性能なフォームを作成。 優れた読み込み速度とSEO パフォーマンスを実現。 |
| **機能：** Excel スプレッドシートを使用してフォームを作成し、最適なGoogle Lighthouse スコアを使用して高性能なエッジ配信ネットワークに公開します。 |
| **使用するタイミング：** パフォーマンスに不可欠なアプリケーション、SEO重視のプロジェクト、コンテンツ作成者によるフォーム作成、グローバルなコンテンツ配信。 |
| ⚡ Excel ベースのオーサリング ⚡高速な読み込み⚡最適なSEO ⚡ グローバル CDN配信 |
| [Edge Deliveryの基本を学ぶ→](/help/edge/docs/forms/overview.md) |

### HTML5 Forms {#html5-forms}

| **HTML5 Forms** |
|---|
| XFA ベースのフォームを、モバイルデバイスと従来のブラウザー用にHTML 5としてレンダリングします。 ネイティブなモバイル体験を提供しながら、フォームのロジックを維持。 |
| **機能：** XFA フォームテンプレートを、ネイティブのモバイルエクスペリエンスとブラウザー間の互換性を備えたHTML5 フォームに変換します。 |
| **使用するタイミング：** XFA フォームの近代化、モバイル最適化、従来のブラウザーのサポート、既存のXDPへの投資。 |
| 📱 XFA互換性📱 モバイル最適化📱 クロスブラウザーサポート 📱 プラグインの必要はありません |
| [HTML5 Formsの基本を学ぶ→](/help/forms/introductionhtml5.md) |

### インタラクティブなコミュニケーション {#interactive-communications}

| **インタラクティブなコミュニケーション** |
|---|
| 動的なデータ統合機能を備えたビジュアルエディターを使用して、明細書、請求書、通知などのドキュメント中心のコミュニケーションを作成できます。 |
| **機能：**&#x200B;静的なコンテンツと動的なデータを組み合わせて、印刷チャネルとデジタルチャネル向けにパーソナライズされたコミュニケーションをデザインします。 |
| **使用するタイミング：**&#x200B;顧客の明細書、請求書、通知、パーソナライズされたコミュニケーション、ドキュメントを多用するワークフロー。 |
| 📄 ビジュアルドキュメントデザイン 📄動的データ統合📄 マルチチャネル出力📄 Personalization |
| [&#x200B; インタラクティブ通信の概要→](/help/forms/interactive-communication/create-interactive-communication.md) |

## 🔗 データと統合 {#data-integration}

フォームをバックエンドシステムやデータソースに接続し、シームレスな情報フローとリアルタイムのデータ交換を実現できます。

### フォームデータモデル {#form-data-model}

| **フォームデータモデル** |
|---|
| 事前入力、検証、送信機能により、複数のデータソースへの統合されたインターフェイスを提供します。 一貫性のあるモデルの背後にある抽象的な統合の複雑さ。 |
| **機能：**&#x200B;一貫したインターフェイスとデータフロー管理を使用して、複数のバックエンドシステムにフォームを接続する統合データレイヤーを作成します。 |
| **使用するタイミング：**&#x200B;複数のデータソース統合、複雑なデータ関係、事前母集団要件、ライブデータに対する検証。 |
| 🔄 マルチソース統合🔄 データモデリング 🔄事前入力🔄検証ルール 🔄統合インターフェイス |
| [&#x200B; フォームデータモデルの概要→](/help/forms/create-form-data-models.md) |

### RESTful コネクタ {#restful-connectors}

| **RESTful コネクタ** |
|---|
| RESTful APIを通じて、web アクセス可能なあらゆるサービスとネイティブで統合できます。 カスタム APIとweb サービスへの接続。 |
| **機能：**&#x200B;送信アクションまたはデータ統合を通じてフォームから直接API呼び出しを有効にし、web サービスにリアルタイムで接続します。 |
| **使用するタイミング：** カスタム API統合、web サービス接続、リアルタイム データ交換、サードパーティ サービス統合。 |
| 🌐直接API呼び出し🌐 リアルタイム接続🌐柔軟な統合🌐 カスタムサービスサポート |
| [REST エンドポイントの設定→](/help/forms/configure-submit-action-restpoint.md) \| [&#x200B; データ統合の設定→](/help/forms/data-integration.md) |

### Salesforce Connector {#salesforce-connector}

| **Salesforce コネクタ** |
|---|
| リード管理、顧客データの同期、営業プロセスの自動化など、Salesforce CRMとのネイティブ統合を利用できます。 |
| **機能：** フォームデータの同期、リードの作成、顧客レコードの管理が可能な、Salesforce用の事前定義済みコネクタ。 |
| **使用するタイミング：** Salesforce CRM統合、リードジェネレーションフォーム、顧客データ管理、セールスプロセスの自動化。 |
| 🏢事前定義済みのコネクタ 🏢 リード管理🏢 データ同期🏢 セールスオートメーション |
| [Salesforce統合の設定→](/help/forms/configure-salesforce.md) |

### Microsoft Dynamics Connector {#dynamics-connector}

| **Microsoft Dynamics コネクタ** |
|---|
| 包括的なビジネスプロセスをサポートし、ERPおよびCRM接続に対応する、Microsoft Dynamicsのエンタープライズ統合。 |
| **機能：** フォームをMicrosoft Dynamicsに接続して、顧客管理、ビジネスプロセス統合、エンタープライズデータフローを行います。 |
| **使用するタイミング：** Microsoft Dynamicsとの統合、エンタープライズワークフロー、顧客管理、ビジネスプロセスの自動化 |
| 🏭 エンタープライズ接続🏭 ビジネスプロセス統合🏭顧客管理🏭 データ同期 |
| [Dynamics統合の設定→](/help/forms/configure-msdynamics.md) |

### SharePoint コネクター {#sharepoint-connector}

| **SharePoint コネクタ** |
|---|
| SharePointとのドキュメント管理の統合により、ファイルの保存、共同作業、ドキュメントワークフローの自動化が可能になります。 |
| **機能：** フォーム送信と生成されたドキュメントを、自動ドキュメント管理と共同作業の機能を備えたSharePointに保存します。 |
| **使用するタイミング：** ドキュメント管理、チームコラボレーション、ファイルストレージ、SharePoint ベースのワークフロー。 |
| 📁 ドキュメントストレージ 📁 Collaborationの機能📁自動ワークフロー📁 SharePointとの統合 |
| [SharePoint統合の設定→](/help/forms/connect-forms-to-sharepoint-document-library.md) |

## プロセスとワークフロー {#process-workflow}

包括的なワークフローおよび処理機能により、ビジネスプロセス、承認、ドキュメント生成を自動化できます。

### AEM ワークフロー {#aem-workflows}

マルチステップの承認、タスクの割り当て、複雑なフォーム駆動型ワークフローのプロセスオーケストレーションなど、ビジネスプロセスの自動化を実現します。

**機能：** フォーム送信の承認チェーン、タスクのルーティング、プロセス監視を使用して、自動化されたビジネス プロセスを作成します。

**使用するタイミング：**&#x200B;承認プロセス、ビジネス オートメーション、タスク管理、複雑なワークフロー、プロセス オーケストレーション。

**主な機能：** プロセスの自動化、承認チェーン、タスクのルーティング、プロセスの監視、ビジネスルール。

[AEM Workflowsの基本を学ぶ→](/help/forms/aem-forms-workflow.md)

### Adobe Sign との統合 {#adobe-sign}

法的拘束力のあるデジタル署名を含む電子サインワークフローを、フォーム体験に直接統合して、シームレスな署名プロセスを実現します。

**機能：**&#x200B;法的拘束力のある電子サイン機能と自動署名ワークフローを使用して、フォーム内でデジタル署名を有効にします。

**使用するタイミング：**&#x200B;契約署名、法的文書、承認ワークフロー、コンプライアンス要件、署名の自動化。

**主な機能：**&#x200B;法的な電子サイン、署名ワークフロー、コンプライアンスサポート、自動プロセス。

[Adobe Sign →の設定](/help/forms/working-with-adobe-sign.md)

### 送信アクション {#submit-actions}

電子メール、データベースストレージ、ワークフロートリガー、カスタム処理など、複数の処理オプションを使用したフォーム送信の処理。

**機能：** ユーザーがフォームを送信する際に何が起こるかを定義します。メール、データベース、ワークフロー、または外部システムにデータを送信します。

**使用するタイミング：** フォーム送信処理、データルーティング、通知システム、統合トリガー。

**主な機能：**&#x200B;複数の送信オプション、データルーティング、通知システム、統合トリガー。

[送信アクションの設定→](/help/forms/configure-submit-actions-core-components.md)

### 通信 API {#communication-apis}

RESTful APIを使用したプログラマティックなドキュメント生成、操作、セキュリティにより、大量のドキュメント処理と自動化を実現します。

**機能：** PDFの作成、ドキュメントの組み立て、バッチ処理のためのAPIを使用して、プログラムでドキュメントを生成、操作、保護します。

**使用するタイミング：** ドキュメントの自動処理、大量の処理、プログラムによる生成、ドキュメントのアセンブリ、バッチ処理。

**主な機能：** ドキュメント生成、バッチ処理、プログラマティック制御、ドキュメントセキュリティ、API自動化

[コミュニケーション APIの基本を学ぶ→](/help/forms/aem-forms-cloud-service-communications-introduction.md)

## 分析/最適化 {#analytics-optimization}

包括的な分析およびテスト機能により、フォームのパフォーマンスを監視し、ユーザーの行動を把握して、コンバージョン率を最適化できます。

### Adobe Analytics との統合 {#adobe-analytics}

完了率、放棄パターン、ユーザーの行動に関する詳細な分析を通じて、フォームのパフォーマンスを追跡し、データ主導の最適化を実現します。

**機能：** フォームのインタラクション、完了率、フィールドレベルの分析、ユーザーの行動パターンを包括的なレポートで追跡します。

**使用するタイミング：** パフォーマンスの監視、コンバージョンの最適化、ユーザー行動分析、データ主導の改善。

**主な機能：** パフォーマンスの追跡、ユーザー行動分析、コンバージョン指標、詳細レポート。

[Analytics統合の設定→](/help/forms/integrate-aem-forms-with-adobe-analytics.md)

### トランザクションレポート {#transaction-reports}

API呼び出し、ドキュメント生成、デプロイメント全体の請求可能なトランザクションに関する詳細なレポートにより、使用状況の監視と請求の透明性を実現します。

**機能：** APIの使用状況、ドキュメント生成ボリューム、請求可能トランザクションを、詳細な消費レポートとコスト追跡を使用して監視します。

**使用状況の監視、コストの追跡、キャパシティプランニング、コンプライアンスレポート、リソースの最適化を使用するタイミング：**

**主な機能：**&#x200B;使用状況の追跡、コストの監視、キャパシティプランニング、コンプライアンスレポート。

[トランザクションレポートの表示→](/help/forms/transaction-reports-billable-apis.md)

### A/B テストとの統合 {#ab-testing}

コンバージョンを向上させるために統計分析を行い、様々なレイアウト、フィールド配置、ユーザーフローをテストすることによるフォームの最適化を行います。

**機能：**&#x200B;様々なユーザーセグメントやユースケースに対する最も効果的なアプローチを特定するために、様々なフォームのバリエーションをテストします。

**使用するタイミング：** コンバージョンの最適化、ユーザーエクスペリエンスのテスト、パフォーマンスの向上、データ主導のデザイン決定。

**主な機能：** フォームテスト、統計分析、コンバージョンの最適化、パフォーマンス比較。

[フォームの最適化について詳しく見る→](/help/forms/view-understand-aem-forms-analytics-reports.md)

## Management &amp; Governance {#management-governance}

企業規模のフォーム展開に対応する一元化されたフォーム管理、ユーザーアクセス制御、ガバナンス機能。

### フォームポータル {#forms-portal}

検索機能、フォームの分類、ドラフト管理、送信トラッキングなどの機能を備えた一元化されたフォームリポジトリを統合されたインターフェイスで利用できます。

**機能：** ユーザーが検索と分類を使用して送信を検索、アクセス、管理、および追跡できる一元化されたフォーム リポジトリを作成します。

**使用するタイミング：** フォームの検出、一元管理、ユーザーセルフサービス、ドラフト管理、送信追跡。

**主な機能：** フォームの検索、検索機能、ドラフト管理、送信トラッキング、ユーザーインターフェイス。

[Forms Portal →の設定](/help/forms/configure-forms-portal.md)

### User Management {#user-management}

組織全体でのフォームの作成、編集、公開、管理に対する詳細な権限を備えた、役割ベースのアクセス制御。

**機能：**&#x200B;きめ細かいアクセス制御とセキュリティにより、フォーム管理のさまざまな側面に対するユーザーの役割と権限を定義します。

**使用するタイミング：** アクセス制御、セキュリティ管理、ロール定義、権限管理、組織ガバナンス。

**主な機能：**&#x200B;役割ベースのアクセス、権限管理、セキュリティ制御、組織ガバナンス。

[ユーザー管理→の設定](/help/forms/forms-groups-privileges-tasks.md)

### バージョン管理 {#version-control}

バージョンの追跡、変更履歴、ロールバック機能、コンプライアンスとガバナンスに関する監査証跡により、ライフサイクル管理を強化できます。

**機能：** フォームのバージョンを追跡し、変更履歴を管理し、ロールバックを有効にし、コンプライアンスとガバナンス要件の監査証跡を提供します。

**使用するタイミング：**&#x200B;変更管理、コンプライアンス要件、監査証跡、バージョン追跡、ガバナンスプロセス。

**主な機能：** バージョンの追跡、変更履歴、ロールバック機能、監査証跡、コンプライアンスサポート

[バージョン管理について詳しく見る→](/help/forms/add-comments-annotations-versioning-adaptive-form-core-components.md)

## 製品の概要 {#getting-started}

目先のニーズや技術的な要件にもとづいて、出発点を選択します。

### フォーム作成クイックスタート {#form-creation-start}

**最新のプロジェクトの場合：** [&#x200B; コアコンポーネント Forms](/help/forms/creating-adaptive-form-core-components.md)で開始

**パフォーマンスを高めるために：** [Edge Delivery Forms](/help/edge/docs/forms/overview.md)で開始

**既存のプロジェクトの場合：** [基盤コンポーネント Forms](/help/forms/creating-adaptive-form.md)で開始

**XFA モダナイゼーションの場合：** [HTML5 Forms](/help/forms/introductionhtml5.md)で開始

**ドキュメント通信の場合：** [&#x200B; インタラクティブ通信](/help/forms/interactive-communication/create-interactive-communication.md)で開始

### データ統合クイックスタート {#integration-start}

**複数のデータソースの場合：** [&#x200B; フォームデータモデル &#x200B;](/help/forms/create-form-data-models.md)で開始

**Salesforce CRMの場合：** [Salesforce コネクタ &#x200B;](/help/forms/configure-salesforce.md)で開始

**Microsoft Dynamicsの場合：** [Dynamics Connector](/help/forms/configure-msdynamics.md)で開始

**カスタム APIの場合：** [RESTful Connectors](/help/forms/configure-submit-action-restpoint.md)で開始

**文書ストレージの場合：** [SharePoint コネクタ &#x200B;](/help/forms/connect-forms-to-sharepoint-document-library.md)で開始

### プロセス自動化のクイックスタート {#workflow-start}

**承認プロセスの場合：** [AEM ワークフロー](/help/forms/aem-forms-workflow.md)で開始

**電子サインの場合：** [Adobe Sign統合](/help/forms/working-with-adobe-sign.md)で開始

**送信処理の場合：** [送信アクション &#x200B;](/help/forms/configure-submit-actions-core-components.md)で開始

**ドキュメント生成用：** [通信API](/help/forms/aem-forms-cloud-service-communications-introduction.md)で開始

### Analytics クイックスタート {#analytics-start}

**パフォーマンス トラッキングの場合：** [Adobe Analytics統合](/help/forms/integrate-aem-forms-with-adobe-analytics.md)で開始

**使用状況の監視：** [&#x200B; トランザクションレポート &#x200B;](/help/forms/transaction-reports-billable-apis.md)から開始

**最適化インサイトの場合：** [分析レポート &#x200B;](/help/forms/view-understand-aem-forms-analytics-reports.md)から開始

### 管理クイックスタート {#management-start}

**フォームの検出：** [Forms ポータル &#x200B;](/help/forms/configure-forms-portal.md)から開始

**アクセス制御の場合：** [&#x200B; ユーザー管理](/help/forms/forms-groups-privileges-tasks.md)で開始

**変更追跡の場合：** [&#x200B; バージョン管理](/help/forms/add-comments-annotations-versioning-adaptive-form-core-components.md)で開始

## アーキテクチャと展開 {#architecture}

包括的な導入ガイダンスの場合：

- **[スケーラブルなデプロイメントのためのアーキテクチャパターン](/help/forms/aem-forms-cloud-service-architecture.md)**&#x200B;の確認
- **[チームの共同作業のための開発環境](/help/forms/setup-local-development-environment.md)**&#x200B;の設定
- **[既存システムからの移行戦略を計画](/help/forms/migrate-to-forms-as-a-cloud-service.md)**

## サポートとリソース {#support}

- **ヘルプセンター** – 実装とトラブルシューティングについてサポートを受ける
- **コミュニティフォーラム** – 他のAEM Forms ユーザーやエキスパートとつながる
- **プロフェッショナルサービス** - エンタープライズ版デプロイメント向けAdobe コンサルティング
- **トレーニングと資格認定** - AEM Formsの機能に関する専門知識を開発

*強力なフォームエクスペリエンスを構築するために必要なコンポーネントを選択します。 各製品は独立して動作するか、他の製品と組み合わせて、ビジネス要件に対する包括的なソリューションを作成します。*
