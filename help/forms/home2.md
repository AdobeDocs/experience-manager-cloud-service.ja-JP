---
title: AEM Forms as a Cloud Service の概要
description: アダプティブフォームの作成、ワークフローの自動化、デジタルドキュメントの管理を行うAEM Formsの機能について説明します。 フォーム主導のビジネスプロセスのための完全なプラットフォーム。
landing-page-description: アダプティブフォームの作成、ドキュメントの処理、ビジネスワークフローの自動化にAEM Forms as a Cloud Serviceを使用する方法を説明します。
keywords: AEM Forms, アダプティブフォーム，フォームビルダー，デジタルフォーム，ワークフロー自動化，ドキュメントサービス，フォームデータモデル
role: Admin, Developer, User
feature: Adaptive Forms, Release Information
hide: true
hidefromtoc: true
index: false
exl-id: 50d7ce19-7d76-4ea1-a54c-8ca0e5379982
source-git-commit: eca09e1bf2ba4466f54e915e01218cc89cf5b116
workflow-type: tm+mt
source-wordcount: '2323'
ht-degree: 1%

---

# AEM Forms as a Cloud Service の概要 {#introduction}



Adobe Experience Manager Forms as a Cloud Serviceは、デジタルフォームエクスペリエンスを作成、管理および最適化するための包括的なプラットフォームを提供します。 AEM Formsを使用すると、紙ベースのプロセスのデジタル化、レスポンシブな web フォームの作成、ドキュメントワークフローの自動化、パーソナライズされたコミュニケーションの大規模な提供を行うことができます。

このプラットフォームは、フォームオーサリング機能と堅牢なバックエンドサービスを組み合わせており、シンプルな連絡先フォームから複雑な複数ステップのビジネスアプリケーションまで、すべてを構築できます。 クラウドネイティブアーキテクチャを使用すると、インフラストラクチャを管理することなく、自動更新、柔軟な拡張、エンタープライズクラスのセキュリティを実現できます。

このガイドでは、最初のデザインから継続的な最適化まで、フォームのライフサイクル全体にわたって整理されたコア機能について説明します。

## AEM Forms の新機能 {#whats-new}

**最新リリースのハイライト：**

- **日付と時刻の入力コンポーネント** - カレンダーと時計のインターフェイスを使用したユーザー入力が強化され、日付と時刻を正確に選択できます。
- **ファイルアップロードセキュリティの強化** - サポートされていないファイル形式を防ぐための自動検証とコンテンツタイプチェック
- **エラー処理の改善** - カスタム送信アクションの特定のエラーコードによるデバッグが向上しました。
- **レコードのドキュメントの機能強化** - クリーンなドキュメント生成用に非表示フィールドを除外するオプション

**プレリリース機能：**

- **AFP 形式のサポート** – 通信 API を使用したエンタープライズクラスの印刷機能
- **ルールエディターの機能強化** – 最新のJavaScript サポート、動的変数およびコンテキスト対応パネルルール
- **強化された検証方法** - パネル、フィールド、フォームレベルの検証が強化され、柔軟性が向上しました

[の完全なリリースノート→表示](/help/release-notes/release-notes-cloud/release-notes-current.md#forms)

## アーリーアクセスプログラム {#early-access}

AEM Formsの最新のイノベーションは、一般に利用する前に排他的に利用できます。

**現在のアーリーアクセス機能：**

- **AEM Forms AI アシスタント** - フォームの自動作成、パネルの生成、最適化の推奨事項に対応するジェネレーティブ AI
- **手書き署名コンポーネント** - マウス、スタイラス、タッチスクリーンを使用して、フォーム内で直接署名をキャプチャできます
- **API の直接統合** - フォームデータモデルの設定を必要とせずに、ルールエディターで API に接続する
- **Formsの最適化** - AI を活用したパフォーマンス分析とコンバージョン率の向上に関する提案

**プログラムへの参加：**
イノベーションにアクセスし、AEM Formsの未来を築く最初のユーザーの 1 人になる。

[ アクセス→を要求 ](mailto:aem-forms-ea@adobe.com) | [→細情報 ](/help/forms/early-access-ea-features.md)


## コア機能 {#core-capabilities}

AEM Formsは、初期作成から継続的な最適化まで、デジタルフォームの完全なジャーニーをサポートします。 各フェーズは前のフェーズに基づいており、フォーム駆動型のビジネス・プロセスのための包括的なプラットフォームを作成します。

**AEM Forms ワークフロージャーニー:**

     作成→管理→公開→取得→プロセス→統合→追跡→アーカイブ→改善 
    ↓        ↓        ↓         ↓         ↓         ↓          ↓       ↓        ↓
     デザイン   レビュー   デプロイ   収集   ハンドル   接続   モニターストア   Optimize
    ↑                                                                              ↓
    ←←←←←←←←←←←←←←←継続的な改善ループ←←←←←←←←←←←←←←←←←←←←←←←←←←←←←←←←←←←←

### 作成：フォームのデザインと開発 {#create}

様々なニーズや技術要件に合わせた複数のオーサリングアプローチを使用してアダプティブフォームを作成します。

**ビジュアルフォームビルダー**
[ コアコンポーネント ](/help/forms/creating-adaptive-form-core-components.md)、{ 基盤コンポーネント [、](/help/forms/creating-adaptive-form.md)Edge Delivery Services[ のいずれかを使用して、ドラッグ&amp;ドロップインターフェイスを介してレスポンシブフォームをデザイ ](/help/edge/docs/forms/overview.md) します。 ビジュアルエディターは、デバイスや支援テクノロジーをまたいで機能する、クリーンでセマンティックなマークアップを維持しながら、即座にフィードバックを提供します。

**ドキュメントベースのオーサリング**
[Edge Delivery Services](/help/edge/docs/forms/overview.md) からMicrosoft Excel などの使い慣れたツールを使用してフォームを作成します。 このアプローチにより、コンテンツ作成者は、技術的な専門知識がなくても高パフォーマンスのフォームを作成できると同時に、優れたGoogle Lighthouse スコアを達成できます。

**テンプレートとテーマ**
構造と初期コンテンツを定義する事前定義済みの [ テンプレート ](/help/forms/template-editor-core-components.md) を使用して、フォームの作成を高速化します。 複数のフォームのビジュアルスタイルを制御する [ テーマ ](/help/forms/using-themes-in-core-components.md) を使用して一貫性のあるブランディングを適用し、デザインの一貫性を確保し、開発時間を短縮します。

**データ統合**
設計段階でフォームをバックエンドシステムに接続します。 [ フォームデータモデル ](/help/forms/create-form-data-models.md) は、複数のデータソースに対する統一されたインターフェイスを提供し、[ 事前設定 ](/help/forms/prepopulate-adaptive-form-fields.md)、[ 検証ルール ](/help/forms/rule-editor-core-components.md)、フォームとビジネスシステムの間のシームレスなデータフローを可能にします。

**検証と条件付きロジック**
[ 条件付きロジック ](/help/forms/rule-editor-core-components.md)、プログレッシブ公開、アダプティブ検証を実装して、複雑なプロセスをユーザーに導きます。 [ 保存および再開機能 ](/help/forms/save-core-component-based-form-as-draft.md) を使用すると、ユーザーは複数のセッションにわたってフォームを完了できます。

**HTML5Forms**
モバイルデバイスおよび従来のブラウザー用に、XFA ベースのフォームを [2}HTML5 forms} としてレンダリングします。 ](/help/forms/introductionhtml5.md)HTML5 Formsは、元の XDP テンプレートからのフォームロジックと検証を維持しながら、プラグインなしでネイティブのモバイルエクスペリエンスを提供します。

**インタラクティブ通信**
ビジュアルエディターを使用して、明細書、請求書、通知などのドキュメント中心のコミュニケーションを作成します。 [ インタラクティブ通信 ](/help/forms/interactive-communication/create-interactive-communication.md) 静的コンテンツと動的データを組み合わせて、印刷チャネルとデジタルチャネルをまたいで、パーソナライズされたコミュニケーションを生成します。

### 管理：レビューとコンプライアンス {#govern}

フォームが組織の標準と規制要件を確実に満たすように、監視および承認プロセスを確立します。

**ワークフローベースの承認**
ロールベースの割り当てを使用した複数の手順のレビュープロセスを通じて、フォームのデザインをルーティングします。 関係者は、[AEM ワークフロー ](/help/forms/create-reviews-forms.md) を使用して、公開前にフォームのレビュー [、](/help/forms/add-comments-annotations-versioning-adaptive-form-core-components.md) コメント [ および承認を行い、品質管理とコンプライアンス管理を維持 ](/help/forms/aem-forms-workflow.md) ることができます。

**バージョン管理**
フォームのバージョンを追跡し、コンプライアンスに関する監査証跡を維持します。 組み込み [ バージョン管理 ](/help/forms/add-comments-annotations-versioning-adaptive-form-core-components.md) により、変更のロールバック、イテレーションの比較、コンプライアンス監査に関する履歴レコードの維持が可能になります。

**アクセス制御と権限**
フォームの作成、編集、公開に関する詳細な権限を定義します。 [ 役割ベースのアクセス ](/help/forms/forms-groups-privileges-tasks.md) により、権限を持つユーザーのみがフォームを変更できるようになり、機密性の高いビジネスプロセスに対する職務の分離が維持されます。

### パブリッシュ：マルチチャネル配布 {#publish}

複数のチャネルとタッチポイントにフォームをデプロイして、どこにいてもユーザーにリーチします。

**オムニチャネル公開**
フォームを [AEM Sites](/help/forms/embed-adaptive-form-aem-sites.md)、スタンドアロン Web ページ、モバイルアプリケーションに公開するか、[ サードパーティシステムに埋め込む ](/help/forms/embed-adaptive-form-core-components-external-web-page.md) ことができます。 単一ソースのパブリッシングにより、様々なチャネル要件に適応しながら、一貫性を確保できます。

**ローカライゼーションとPersonalization**
[ 左から右および右から左の両方の言語 ](/help/forms/using-aem-translation-workflow-to-localize-adaptive-forms-core-components.md) をサポートするAEMの翻訳ワークフロー [ を使用して、フォームを複数の言語で配信 ](/help/forms/right-left-languages.md) ます。 Adobe Targetとの統合により、ユーザーセグメント、行動またはコンテキストデータに基づいてフォームエクスペリエンスをパーソナライズできます。

**パフォーマンスの最適化**
Edge Delivery Servicesを利用すると、フォームの読み込みが非常に高速になり、SEO のパフォーマンスが最適化されます。 コンテンツ配信ネットワークにより、最小限の待ち時間でグローバルなアクセシビリティが確保されます。

**Forms ポータル**
ユーザーがフォームを検出、アクセス、管理できる、一元化されたフォームリポジトリを作成します。 [Forms ポータル ](/help/forms/configure-forms-portal.md) は、検索機能、フォームの分類、ドラフト管理、送信の追跡を統合されたインターフェイスで提供し、ユーザーエクスペリエンスを向上させます。

### キャプチャ：ユーザーエクスペリエンスとデータ収集 {#capture}

フォーム入力エクスペリエンスを最適化して、完了率とデータ品質を最大化します。

**レスポンシブデザイン**
Formsは、様々な画面サイズや入力方式に自動的に対応します。 タッチ操作に最適化されたコントロール、キーボードナビゲーション、スクリーンリーダーの互換性により、あらゆるタイプのユーザーで [ アクセシビリティ ](/help/forms/creating-accessible-adaptive-forms.md) を確保できます。

**電子署名**
[Adobe Sign](/help/forms/working-with-adobe-sign.md) を統合して、フォームエクスペリエンス内で法的拘束力のある電子サインを利用できるようにします。 ユーザーはフォームを離れることなくドキュメントに署名でき、承認プロセスを合理化し、放棄を減らすことができます。

**送信アクション**
[ 送信アクション ](/help/forms/configure-submit-actions-core-components.md) を設定して、ユーザーがフォームに記入して送信したときの動作を定義します。 メール、データベース、ワークフロー、外部システムにデータをルーティングすると同時に、ユーザーにすぐにフィードバックと確認を提供します。

### プロセス：送信の処理とルーティング {#process}

堅牢な処理、検証、ルーティングの機能を使用して、フォーム送信を処理します。

**データの検証と処理**
サーバーサイドの検証と自動処理ルールにより、データの整合性を確保します。 送信されたデータを変換、検証、ルーティングすると同時に、ユーザー向けのレシート、確認、フォローアップ資料を生成します。

**通信 API**
[RESTful API](/help/forms/aem-forms-cloud-service-communications-introduction.md) を使用して、プログラムでドキュメントを生成、操作、保護します。 エンタープライズ規模のドキュメントワークフロー向けに、PDF の作成、印刷可能な形式の作成、ドキュメントのアセンブリ、デジタル署名の適用、大量の [ バッチ操作 ](/help/forms/aem-forms-cloud-service-communications-batch-processing.md) の処理を行います。

**記録の書面**
フォーム送信に関するPDF レコードを自動生成し、準拠とユーザーの確認を行います。 [ レコードのドキュメント ](/help/forms/generate-document-of-record-core-components.md) 送信されたデータを使用して、完成したフォームのフォーマットされ、印刷可能なバージョンを作成し、取引と規制要件に関する公式ドキュメントを提供します。

**ワークフローオーケストレーション**
フォーム送信に基づいて複雑なビジネスプロセスをトリガーします。 承認チェーンを通じてデータをルーティングし、特定のユーザーにタスクを割り当て、監査証跡を維持しながら日常的な操作を自動化します。

**エラー処理と回復**
ビルトインの再試行メカニズムとフォールバック処理により、送信が失われないようにします。 包括的なログは、問題のトラブルシューティングと SLA （Service Level Agreement）の維持に役立ちます。

### 統合：バックエンド接続 {#integrate}

フォームを既存のビジネスシステムおよびデータソースに接続して、シームレスな情報フローを実現します。

**事前定義済みコネクタ**
[Salesforce](/help/forms/configure-salesforce.md)、[Microsoft Dynamics](/help/forms/configure-msdynamics.md)、[SharePoint](/help/forms/connect-forms-to-sharepoint-document-library.md) およびAdobe Experience Cloud ソリューションとのネイティブ統合。 事前定義済みのコネクタにより、信頼性の高いデータ同期を確保しながら、開発時間を短縮します。

**RESTful API の統合**
[ 送信アクション ](/help/forms/configure-submit-action-restpoint.md) または [ データ統合 ](/help/forms/data-integration.md) を介した RESTful API を通じて、web でアクセス可能なサービスに接続します。 フォームデータモデルは、統合の複雑さを抽象化し、基になるシステムアーキテクチャに関係なく、一貫したインターフェイスを提供します。

**リアルタイムのデータ交換**
フォームとビジネスシステム間の双方向データフローを有効にします。 包括的な [ データ統合 ](/help/forms/data-integration.md) を通じて、既存のレコードからフォームに事前入力し、ライブデータに照らして検証し、送信時に複数のシステムを同時に更新します。

### 追跡：分析とパフォーマンスの監視 {#track}

包括的な分析と監視を通じて、フォームのパフォーマンスとユーザーの行動を把握します。

**フォーム分析**
[Adobe Analyticsの統合 ](/help/forms/integrate-aem-forms-with-adobe-analytics.md) を通じて、完了率、離脱パターンおよびフィールドレベルのインタラクションを追跡します。 摩擦ポイントを特定し、コンバージョンファネルを測定し、様々なセグメントでのユーザーの行動を理解します。

**パフォーマンス監視**
フォームの読み込み時間、送信の成功率、システムのパフォーマンスを監視します。 リアルタイムダッシュボードは、技術的な正常性とユーザーエクスペリエンスの指標に関するインサイトを提供します。

**Business Intelligence**
フォームの使用状況、送信量、プロセスの効率に関するレポートを生成します。 Analytics は、容量計画、ユーザーエクスペリエンスの最適化、ビジネスプロセスの改善を通知します。

**取引報告書**
AEM Forms デプロイメント全体での API 使用状況、ドキュメント生成ボリューム、および [ 課金対象のトランザクション ](/help/forms/transaction-reports-billable-apis.md) を監視します。 消費パターンの追跡、リソース割り当ての最適化、使用状況ベースのライセンス要件への準拠の維持を行います。

### アーカイブ：ドキュメント管理とコンプライアンス {#archive}

長期保存とコンプライアンスのために、フォーム送信と生成されたドキュメントを安全に保存および管理します。

**ドキュメントストレージ**
生成されたドキュメントとフォーム送信をAEMの Digital Asset Management System に格納するか、[SharePoint](/help/forms/configure-submit-action-sharepoint.md)、[OneDrive](/help/forms/configure-submit-action-onedrive.md)、[Azure Blob Storage](/help/forms/configure-submit-action-azure-blob-storage.md) などの外部ドキュメントリポジトリと統合します。

**遵守状況及び保存**
GDPR、CCPA、HIPAA などの規制要件に準拠したデータ保持ポリシーを実装します。 [ 自動アーカイブ・プロセス ](/help/forms/aem-forms-cloud-service-communications-batch-processing.md) ドキュメントを必要な期間保持し、適切な場合には安全に廃棄します。

**セキュリティとアクセス制御**
アーカイブされたドキュメントに暗号化、デジタル署名、[ 役割ベースのアクセス制御 ](/help/forms/forms-groups-privileges-tasks.md) を適用します。 監査証跡は、コンプライアンスのレポート作成とセキュリティ管理のために、ドキュメントへのアクセスと変更を追跡します。

### 改善：最適化と機能強化 {#improve}

データ駆動型のインサイトとテストを通じて、フォームのパフォーマンスとユーザーエクスペリエンスを継続的に最適化します。

**A/B テストの統合**
Adobe Targetを使用して、様々なフォームレイアウト、フィールド配置、ユーザーフローをテストします。 統計分析は、様々なユーザーセグメントやユースケースに対して最も効果的なアプローチを特定するのに役立ちます。

**Analytics 主導の最適化**
ユーザー行動データを分析して、改善の機会を特定します。 [ 分析レポートの表示と理解 ](/help/forms/view-understand-aem-forms-analytics-reports.md) ヒートマッピング、フィールドインタラクション分析、放棄パターン認識について説明し、反復的な設計機能強化を通知します。

**繰り返し機能強化**
ユーザーからのフィードバック、パフォーマンス指標、ビジネス要件に基づいて、継続的な改善プロセスを実装します。 [ バージョン管理 ](/help/forms/add-comments-annotations-versioning-adaptive-form-core-components.md) およびロールバック機能により、安全な実験と迅速なイテレーションが可能になります。

## はじめに {#getting-started}

アプローチは、当面のニーズと長期的な目標に応じて異なります。

### クイックスタート：シンプルなForms {#quick-start}

技術的な背景とパフォーマンス要件に基づいて、好みのオーサリングアプローチを選択します。

**ビジュアルフォームの作成：**

1. 最新のレスポンシブフォーム用に **[コアコンポーネントを使用してアダプティブフォームを作成](/help/forms/creating-adaptive-form-core-components.md)**
2. フォームデータを処理するための **[送信アクションの設定](/help/forms/configure-submit-actions-core-components.md)**
3. **[AEM Sitesへのフォームの埋め込み](/help/forms/embed-adaptive-form-aem-sites.md)** またはダイレクトリンクを使用した共有

**ドキュメントベースのオーサリング：**

1. **[Excel を使用したフォームの作成](/help/edge/docs/forms/create-forms.md)** とEdge Delivery Servicesによる高パフォーマンスのフォームの実現
2. 最適な読み込み速度と SEO のために、**[Edge Deliveryに公開](/help/edge/docs/forms/publish-forms.md)**

**レガシーフォームのサポート：**

- モバイルに最適化された XFA フォームレンダリング用の **[HTML5 Forms](/help/forms/introductionhtml5.md)**

### 高度な実装：ビジネスプロセス {#advanced-implementation}

複数のシステム、ドキュメント生成、承認ワークフローに関する複雑な要件の場合：

**データ統合とワークフロー：**

1. バックエンドシステムを接続するための **[フォームデータモデルの設定](/help/forms/create-form-data-models.md)**
2. 承認とルーティングのための **[ワークフロープロセスの設計](/help/forms/aem-forms-workflow.md)**
3. パフォーマンスを測定するための **[Analytics の設定](/help/forms/integrate-aem-forms-with-adobe-analytics.md)**

**ドキュメントサービスと通信：**

1. ドキュメントの自動生成のための **[通信 API の実装](/help/forms/aem-forms-cloud-service-communications-introduction.md)**
2. パーソナライズされた声明や通知のために、**[インタラクティブ通信を作成](/help/forms/interactive-communication/create-interactive-communication.md)** します
3. フォームを一元的に管理するための **[Forms ポータルの設定](/help/forms/configure-forms-portal.md)**

### 大規模導入：拡張性とガバナンス {#enterprise-deployment}

ガバナンス、コンプライアンス、監視を必要とする組織全体のデプロイメントの場合：

**アーキテクチャとガバナンス：**

1. **[アーキテクチャパターンのレビュー](/help/forms/aem-forms-cloud-service-architecture.md)** によるスケーラブルな導入
2. **[ユーザー管理の設定](/help/forms/forms-groups-privileges-tasks.md)** およびアクセス制御
3. チーム共同作業のための **[開発ワークフローの設定](/help/forms/setup-local-development-environment.md)**

**移行と監視：**

1. 既存のシステムからの **[移行戦略の計画](/help/forms/migrate-to-forms-as-a-cloud-service.md)**
2. 使用状況の追跡とコンプライアンスのための **[トランザクション監視の実装](/help/forms/transaction-reports-billable-apis.md)**

<details>
<summary><strong>❓よくある質問 </strong></summary>

**フォームビルダーとは？**
フォームビルダーは、コーディングせずにデジタルフォームを作成できるツールです。 ドラッグ&amp;ドロップインターフェイスを使用してフォームをデザインしたり、テキストボックスやドロップダウンなどのフィールドを追加してオンラインに公開し、ユーザーからデータを収集したりできます。

**オンラインフォームを作成するにはどうすればよいですか？**
AEM Formsを使用すると、視覚的なドラッグ&amp;ドロップエディターを通じてコアコンポーネントを使用してアダプティブフォームを作成したり、Edge Delivery Servicesで高パフォーマンスのフォームを作成したり、確立されたワークフローに基盤コンポーネントを使用したりできます。 まずテンプレートを選択し、フォームフィールドを追加し、データ接続を設定し、複数のチャネルにわたって公開します。

**優れたオンラインフォームの理由**
優れたオンラインフォームは、モバイル対応、迅速な読み込み、明確なラベル付け、論理的なフィールド順序の使用、エラーを防ぐための検証の組み込み、送信時のユーザーへの即時フィードバックの提供です。

**フォームを他のビジネスシステムと統合できますか？**
はい、最新のフォームビルダーは、広範な統合機能を提供します。 CRM システム、メールマーケティングプラットフォーム、データベース、クラウドストレージ、ワークフロー自動化ツールにフォームを接続して、ビジネスプロセスを合理化できます。

**オンラインフォームは安全ですか？**
プロフェッショナルなフォームビルダーには、データ暗号化、安全なデータ送信、アクセス制御、GDPR、HIPAA、CCPA などの規制へのコンプライアンスなど、エンタープライズクラスのセキュリティ機能が含まれ、機密情報を保護できます。

**フォームに電子サインを追加するにはどうすればよいですか？**
デジタル署名は、Adobe Sign やその他の電子サインプロバイダーを使用して、フォームに直接統合することができます。 これにより、ユーザーはフォームエクスペリエンス内でドキュメントに署名できるので、個別の署名ワークフローが不要になり、フォームの放棄が減ります。

**フォームでPDF ドキュメントを自動生成できますか？**
はい。最新のフォームプラットフォームでは、フォームの送信時に、PDFの受信、確認またはレコードのドキュメントを自動的に生成できます。 これは、コンプライアンス、記録保持、ユーザーへの即時確認に不可欠です。

**フォームのパフォーマンスと分析を追跡するにはどうすればよいですか？**
フォーム分析は、完了率、離脱パターンおよびユーザー行動を理解するのに役立ちます。 Adobe Analyticsなどの分析プラットフォームと統合すると、摩擦の原因となるフィールドはどれか、およびコンバージョン率を最適化する方法に関するインサイトが得られます。

**フォームワークフロー自動化とは何ですか？**
フォームワークフローオートメーションは、承認プロセスを通じて送信をルーティングし、チームメンバーにタスクを割り当て、他のビジネスシステムでトリガーアクションを実行します。 これにより、手動での処理が不要になり、フォームデータの一貫性のある処理が保証されます。

**障がいのあるユーザーがフォームにアクセスできるようにするには、どうすればよいですか？**
[ アクセシブルなフォーム ](/help/forms/creating-accessible-adaptive-forms.md) には、適切なラベル付け、キーボードナビゲーション、スクリーンリーダーの互換性、WCAG ガイドラインへの準拠などが含まれます。 これにより、ユーザーの能力や支援テクノロジーに関係なく、すべてのユーザーがフォームに入力できるようになります。

**フォームビルダーのコストはどれくらいですか？**
AEM Forms as a Cloud Serviceの価格は、具体的な要件、使用量、機能のニーズに応じて異なります。 詳細な価格情報や、お客様の組織に合わせたソリューションについては、Adobe営業担当またはAdobe担当者にお問い合わせください。

</details>

## 次の手順 {#next-steps}

現在の優先度に合った機能を見ていきましょう。

- **[最初のフォームを作成](/help/forms/creating-adaptive-form-core-components.md)** して、オーサリング環境を体験します
- **[アーキテクチャ オプションの確認](/help/forms/aem-forms-cloud-service-architecture.md)** 展開計画
- チームコラボレーションのための **[開発環境の設定](/help/forms/setup-local-development-environment.md)**
- 既存のシステムを接続するための **[統合オプションの参照](/help/forms/data-integration.md)**

包括的な実装ガイダンスについては、Adobe Professional Servicesを検討して、デプロイメントを迅速に行い、最初からベストプラクティスを確実におこなってください。
