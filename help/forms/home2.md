---
title: AEM Forms as a Cloud Service の概要
description: アダプティブフォームの作成、ワークフローの自動化、デジタルドキュメントの管理など、AEM Formsのさまざまな機能をご確認ください。 フォーム駆動型ビジネスプロセスのための包括的なプラットフォーム。
landing-page-description: AEM Forms as a Cloud Serviceを使用して、アダプティブフォームの作成、ドキュメントの処理、ビジネスワークフローの自動化を行う方法について説明します。
keywords: AEM Forms, アダプティブフォーム，フォームビルダー，デジタルフォーム，ワークフローオートメーション，ドキュメントサービス，フォームデータモデル
role: Admin, Developer, User
feature: Adaptive Forms, Release Information
hide: true
hidefromtoc: true
index: false
badgeSaas: label="AEM Forms" type="Positive" tooltip="AEM Formsに適用）。"
exl-id: 50d7ce19-7d76-4ea1-a54c-8ca0e5379982
source-git-commit: cc3cd74ad87f4213a200f36745ab3d335edca02d
workflow-type: tm+mt
source-wordcount: '2397'
ht-degree: 1%

---

# AEM Forms as a Cloud Service の概要 {#introduction}



Adobe Experience Manager Forms as a Cloud Serviceは、デジタルフォーム体験を構築、管理、最適化するための包括的な基盤を提供します。 企業は、AEM Formsを利用して、紙ベースのプロセスのデジタル化、レスポンシブ web フォームの作成、ドキュメントワークフローの自動化、パーソナライズされたコミュニケーションの大規模な提供を実現しています。

このプラットフォームは、フォームのオーサリング機能と堅牢なバックエンドサービスを組み合わせたもので、シンプルな問い合わせフォームから複雑なマルチステップのビジネスアプリケーションに至るまで、あらゆる機能を構築することができます。 クラウドネイティブのアーキテクチャにより、インフラストラクチャを管理することなく、自動更新、柔軟な拡張、エンタープライズレベルのセキュリティを実現できます。

このガイドでは、最初の設計から継続的な最適化に至るまで、フォームのライフサイクル全体を中心に構成された主要機能について説明します。

## AEM Forms の新機能 {#whats-new}

**最新のリリースのハイライト：**

- **日付と時刻の入力コンポーネント** – 正確な日付と時刻の選択のために、カレンダーと時計のインターフェイスを使用してユーザー入力を強化しました
- **強化されたファイル アップロード セキュリティ** - サポートされていないファイル形式を防ぐための自動検証とコンテンツ タイプのチェック
- **エラー処理の改善** - カスタム送信アクション用の特定のエラーコードを使用したデバッグの改善
- **レコードのドキュメントの機能強化** – よりクリーンなドキュメント生成用の非表示フィールドを除外するオプション

**プレリリース機能：**

- **AFP形式のサポート** – 通信APIを備えたエンタープライズグレードの印刷機能
- **ルールエディターの機能強化** – 最新のJavaScriptのサポート、動的変数、コンテクスト対応パネルルール
- **拡張検証方法** - パネル、フィールド、およびフォームレベルの検証の柔軟性を向上

[リリースノートを見る→](/help/release-notes/release-notes-cloud/release-notes-current.md#forms)

## 早期アクセスプログラム {#early-access}

AEM Formsの最先端イノベーションが一般公開される前に、独占的に利用できます。

**現在の早期アクセス機能：**

- **AEM Forms AI アシスタント** – 自動フォーム作成、パネル生成、最適化レコメンデーション用の生成AI
- **手書き署名コンポーネント** - マウス、スタイラス、またはタッチスクリーンを使用して、フォーム内で直接署名キャプチャします
- **直接API統合** - フォームデータモデルの設定を必要とせずに、ルールエディターのAPIに接続します
- **Forms Optimization** - AIを活用したパフォーマンス分析とコンバージョン率の改善提案

**プログラムに参加：**
イノベーションをいち早く活用し、AEM Formsの未来を形作るお手伝いをしましょう。

[ アクセスを要求→](mailto:aem-forms-ea@adobe.com) | [詳細情報→](/help/forms/early-access-ea-features.md)


## コア機能 {#core-capabilities}

AEM Formsは、最初の制作から継続的な最適化に至るまで、デジタルフォームのあらゆるプロセスをサポートします。 各段階は、それ以前の段階の基盤の上に構築され、フォーム主導のビジネスプロセスのための包括的なプラットフォームを構築します。

**AEM Forms ワークフロージャーニー:**

    作成→管理→公開→ キャプチャ → プロセス→統合→ TRACK → アーカイブ → IMPROVE
    ↓ ↓ ↓ ↓ ↓ ↓ ↓ ↓
     デザイン レビュー展開コレクトハンドル Connect Monitor Store Optimize
    ↑ ↓
    ←←←←←←←←←←←←←←←←←←←←←←←←←←←←←←←←←←←←←←←←←←←←←←←←←←←継続的改善ループ ↓

### 作成：フォームデザインと開発 {#create}

異なるニーズや技術要件に合わせた、複数のオーサリングアプローチを利用して、アダプティブフォームを構築できます。

**ビジュアルフォームビルダー**
[ コアコンポーネント ](/help/forms/creating-adaptive-form-core-components.md)、[基盤コンポーネント ](/help/forms/creating-adaptive-form.md)、[Edge Delivery Services](/help/edge/docs/forms/overview.md)を使用して、ドラッグ&amp;ドロップのインターフェイスでレスポンシブフォームをデザインします。 ビジュアルエディターは、デバイスや支援テクノロジーをまたいで機能する、クリーンでセマンティックなマークアップを維持しながら、即座にフィードバックを提供します。

**ドキュメントベースのオーサリング**
[Edge Delivery Services](/help/edge/docs/forms/overview.md)経由でMicrosoft Excelなどの使い慣れたツールを使用してフォームを作成します。 このアプローチにより、Google Lighthouseの優れたスコアを達成しながら、技術的な専門知識がなくてもパフォーマンスの高いフォームを作成できます。

**テンプレートとテーマ**
構造と初期コンテンツを定義する事前定義済みの[ テンプレート ](/help/forms/template-editor-core-components.md)を使用して、フォーム作成を高速化します。 複数のフォームをまたいでビジュアルスタイルを制御する[ テーマ ](/help/forms/using-themes-in-core-components.md)を使用して、一貫性のあるブランディングを適用することで、デザインの一貫性を確保し、開発時間を短縮できます。

**データ統合**
デザイン段階で、フォームをバックエンドシステムに接続します。 [ フォームデータモデル ](/help/forms/create-form-data-models.md)は、複数のデータソースに対する統合インターフェイスを提供し、[事前入力](/help/forms/prepopulate-adaptive-form-fields.md)、[検証ルール ](/help/forms/rule-editor-core-components.md)、およびフォームとビジネスシステム間のシームレスなデータフローを実現します。

**検証と条件ロジック**
[条件付きロジック ](/help/forms/rule-editor-core-components.md)、プログレッシブ公開、アダプティブ検証を実装して、ユーザーを複雑なプロセスに誘導します。 [保存と再開の機能](/help/forms/save-core-component-based-form-as-draft.md)を使用すると、ユーザーは複数のセッションでフォームに記入できます。

**HTML5 Forms**
モバイルデバイスとレガシーブラウザー用に、XFA ベースのフォームを[HTML5 forms](/help/forms/introductionhtml5.md)としてレンダリングします。 HTML5 Formsは、オリジナルのXDP テンプレートからのフォームロジックと検証を維持しながら、プラグインを使用しないネイティブモバイルエクスペリエンスを提供します。

**インタラクティブ通信**
ビジュアルエディターを使用して、明細書、請求書、通知など、ドキュメント中心のコミュニケーションを作成できます。 [ インタラクティブ コミュニケーション ](/help/forms/interactive-communication/create-interactive-communication.md)は、静的なコンテンツと動的なデータを組み合わせて、印刷物とデジタル チャネル全体でパーソナライズされたコミュニケーションを生成します。

### 管理：レビューとコンプライアンス {#govern}

フォームが組織の基準と規制要件を満たしていることを確認するために、監視と承認のプロセスを確立します。

**ワークフローベースの承認**
ロールベースの割り当てによるマルチステップのレビュープロセスを通じて、フォームのデザインをルーティングできます。 関係者は、[AEM ワークフロー](/help/forms/aem-forms-workflow.md)を使用して、品質管理とコンプライアンス監視を維持しながら、公開前に[ レビュー](/help/forms/create-reviews-forms.md)、[ コメント ](/help/forms/add-comments-annotations-versioning-adaptive-form-core-components.md)および承認フォームを確認できます。

**バージョン管理**
フォームのバージョンを追跡し、監査証跡を維持することで、規制遵守を実現。 組み込みの[ バージョン管理](/help/forms/add-comments-annotations-versioning-adaptive-form-core-components.md)により、変更をロールバックし、イテレーションを比較し、コンプライアンス監査の履歴レコードを維持することができます。

**アクセス制御と権限**
フォームの作成、編集、公開に対して詳細な権限を定義できます。 [役割ベースのアクセス ](/help/forms/forms-groups-privileges-tasks.md)は、機密性の高いビジネスプロセスの担当者分離を維持しながら、承認済みのユーザーのみがフォームを変更できることを保証します。

### パブリッシュ：マルチチャネル配信 {#publish}

複数のチャネルや顧客接点にフォームを展開し、利用者がどこにいてもリーチできます。

**オムニチャネル公開**
[AEM Sites](/help/forms/embed-adaptive-form-aem-sites.md)、スタンドアロン web ページ、モバイルアプリケーション、または[ サードパーティシステムに埋め込む](/help/forms/embed-adaptive-form-core-components-external-web-page.md)にフォームを公開します。 シングルソースパブリッシングにより、様々なチャネル要件に適応しながら、一貫性を確保。

**ローカライズとPersonalization**
[AEMの翻訳ワークフロー](/help/forms/using-aem-translation-workflow-to-localize-adaptive-forms-core-components.md)を使用して、複数の言語でフォームを配信します。また、[左から右、右から左の両方の言語](/help/forms/right-left-languages.md)をサポートします。 Adobe Targetと連携し、顧客セグメント、行動、コンテクストに関するデータにもとづいて、フォームのエクスペリエンスをパーソナライズできます。

**パフォーマンス最適化**
Edge Delivery Servicesを活用して、フォームの読み込みを高速化し、SEO パフォーマンスを最適化できます。 コンテンツ配信ネットワークにより、最小限の遅延でグローバルなアクセシビリティを確保。

**Forms ポータル**
ユーザーがフォームを検索、アクセス、管理できる一元化されたフォームリポジトリを作成します。 [Forms ポータル ](/help/forms/configure-forms-portal.md)は、ユーザーエクスペリエンスを向上させるために、統一されたインターフェイスで検索機能、フォーム分類、ドラフト管理、送信トラッキングを提供します。

### キャプチャ：ユーザーエクスペリエンスとデータ収集 {#capture}

フォーム入力のエクスペリエンスを最適化して、完了率とデータ品質を最大化します。

**レスポンシブデザイン**
Formsは、さまざまな画面サイズや入力方法に自動的に適応します。 タッチ操作向けのコントロール、キーボードナビゲーション、スクリーンリーダーの互換性により、すべてのユーザータイプで[ アクセシビリティ ](/help/forms/creating-accessible-adaptive-forms.md)が確保されます。

**デジタル署名**
[Adobe Sign](/help/forms/working-with-adobe-sign.md)を統合して、法的拘束力のある電子サインをフォームエクスペリエンス内で行うことができます。 利用者はフォームを離れることなくドキュメントに署名できるため、承認プロセスを効率化し、放棄を減らすことができます。

**送信アクション**
[送信アクション ](/help/forms/configure-submit-actions-core-components.md)を設定して、ユーザーがフォームに入力して送信するときの動作を定義します。 データをメール、データベース、ワークフロー、外部システムに振り分けながら、ユーザーに即座にフィードバックと確認を提供できます。

### プロセス：送信処理とルーティング {#process}

堅牢な処理、検証、ルーティング機能により、フォームの送信を処理できます。

**データの検証と処理**
サーバーサイドの検証と自動処理ルールにより、データの整合性を確保。 領収書、確認、またはユーザー向けのフォローアップ資料を生成しながら、送信されたデータを変換、検証、ルーティングします。

**通信API**
[RESTful API](/help/forms/aem-forms-cloud-service-communications-introduction.md)を使用して、プログラムでドキュメントを生成、操作、保護します。 企業規模のドキュメントワークフロー向けに、PDFの作成、印刷可能な形式の作成、ドキュメントの組み立て、デジタル署名の適用、大量の[ バッチ操作](/help/forms/aem-forms-cloud-service-communications-batch-processing.md)の処理を行います。

**レコードのドキュメント**
コンプライアンスとユーザー確認のために、フォーム送信のPDFレコードを自動的に生成します。 [ レコードのドキュメント ](/help/forms/generate-document-of-record-core-components.md)は、送信されたデータを使用して、完成したフォームの書式設定された印刷可能なバージョンを作成し、トランザクションと規制要件に関する公式ドキュメントを提供します。

**ワークフローオーケストレーション**
フォームの入力にもとづいて複雑な業務プロセスをトリガーできます。 承認チェーンを通じてデータをルーティングし、特定のユーザーにタスクを割り当て、監査証跡を維持しながらルーティンオペレーションを自動化できます。

**エラーの処理と回復**
組み込みの再試行メカニズムとフォールバック処理により、送信が失われることはありません。 包括的なログ記録は、問題のトラブルシューティングとサービスレベル契約の維持に役立ちます。

### 統合：バックエンド接続 {#integrate}

フォームを既存のビジネスシステムやデータソースに接続し、シームレスな情報フローを実現できます。

**事前定義済みコネクタ**
[Salesforce](/help/forms/configure-salesforce.md)、[Microsoft Dynamics](/help/forms/configure-msdynamics.md)、[SharePoint](/help/forms/connect-forms-to-sharepoint-document-library.md)およびAdobe Experience Cloud ソリューションとのネイティブ統合。 事前定義済みのコネクタにより、信頼できるデータ同期を確保しながら、開発時間を短縮できます。

**RESTful API統合**
[送信アクション ](/help/forms/configure-submit-action-restpoint.md)または[ データ統合](/help/forms/data-integration.md)を介して、RESTful APIを介してweb アクセス可能なサービスに接続します。 フォームデータモデルは、統合の複雑さを抽象化し、基盤となるシステムアーキテクチャに関係なく、一貫したインターフェイスを提供します。

**Real-Time Data Exchange**
フォームとビジネスシステム間の双方向データフローを実現します。 包括的な[ データ統合](/help/forms/data-integration.md)を通じて、既存のレコードからフォームを事前入力し、ライブデータに対して検証し、送信時に複数のシステムを同時に更新します。

### トラック：分析とパフォーマンスの監視 {#track}

包括的な分析とモニタリングにより、フォームのパフォーマンスとユーザーの行動を把握できます。

**フォーム分析**
[Adobe Analyticsとの統合](/help/forms/integrate-aem-forms-with-adobe-analytics.md)により、完了率、放棄パターン、フィールドレベルのインタラクションを追跡します。 顧客がつまずきやすいポイントを特定し、コンバージョンファネルを測定し、さまざまなセグメントをまたいで顧客の行動を把握できます。

**パフォーマンス監視**
フォームの読み込み時間、送信の成功率、システムのパフォーマンスを監視します。 リアルタイムのダッシュボードでは、技術的な健全性とユーザーエクスペリエンスの指標に関するインサイトを獲得できます。

**Business Intelligence**
フォームの使用状況、送信ボリューム、プロセスの効率性に関するレポートを生成します。 分析は、キャパシティプランニング、ユーザーエクスペリエンスの最適化、ビジネスプロセスの改善に役立ちます。

**トランザクションレポート**
AEM Formsのデプロイメント全体で、APIの使用状況、ドキュメント作成ボリューム、請求可能トランザクション [を監視します。 ](/help/forms/transaction-reports-billable-apis.md)使用パターンを追跡し、リソースの割り当てを最適化して、使用状況に応じたライセンス要件へのコンプライアンスを維持できます。

### アーカイブ：文書管理とコンプライアンス {#archive}

フォーム送信や生成されたドキュメントを安全に保存、管理し、長期的な保持とコンプライアンスに対応。

**ドキュメントストレージ**
生成されたドキュメントとフォーム送信をAEMのDigital Asset Management システムに保存するか、[SharePoint](/help/forms/configure-submit-action-sharepoint.md)、[OneDrive](/help/forms/configure-submit-action-onedrive.md)、[Azure Blob Storage](/help/forms/configure-submit-action-azure-blob-storage.md)などの外部ドキュメントリポジトリと統合します。

**コンプライアンスとリテンション**
GDPR、CCPA、HIPAAなどの規制要件に準拠したデータ保持ポリシーを実装できます。 [自動アーカイブプロセス ](/help/forms/aem-forms-cloud-service-communications-batch-processing.md)は、ドキュメントが必要な期間にわたって保持され、適切な場合に安全に破棄されることを保証します。

**セキュリティとアクセス制御**
暗号化、デジタル署名、および[役割ベースのアクセス制御](/help/forms/forms-groups-privileges-tasks.md)をアーカイブされたドキュメントに適用します。 監査証跡は、コンプライアンスのレポートとセキュリティ監視のためのドキュメントへのアクセスと変更を追跡します。

### 改善：最適化と強化 {#improve}

データ主導のインサイトとテストを通じて、フォームのパフォーマンスとユーザーエクスペリエンスを継続的に最適化します。

**A/B テスト統合**
Adobe Targetでフォームレイアウト、フィールド配置、ユーザーフローをテストし、 統計分析は、さまざまなユーザーセグメントやユースケースに対する最も効果的なアプローチを特定するのに役立ちます。

**Analytics主導の最適化**
ユーザー行動データを分析して改善機会を特定する。 [ ヒートマッピング、フィールドインタラクション分析、放棄パターン認識に関する分析レポート ](/help/forms/view-understand-aem-forms-analytics-reports.md)を表示して理解し、反復的なデザインの強化を確認します。

**反復的な機能強化**
ユーザーのフィードバック、パフォーマンス指標、ビジネス要件にもとづいて、継続的な改善プロセスを実装します。 [ バージョン管理](/help/forms/add-comments-annotations-versioning-adaptive-form-core-components.md)とロールバック機能により、安全な実験と迅速な反復が可能になります。

## はじめに {#getting-started}

直面しているニーズと、長期的な目標によってアプローチは異なります。

### クイックスタート：シンプルなForms {#quick-start}

技術的な背景とパフォーマンス要件にもとづいて、好みのオーサリングアプローチを選択します。

**ビジュアルフォームの作成：**

1. **[コアコンポーネント](/help/forms/creating-adaptive-form-core-components.md)**&#x200B;を使用してアダプティブフォームを作成し、最新のレスポンシブフォームを作成する
2. **[フォームデータを処理するための送信アクション](/help/forms/configure-submit-actions-core-components.md)**&#x200B;の設定
3. **[AEM Sitesにフォームを埋め込む](/help/forms/embed-adaptive-form-aem-sites.md)**、またはダイレクトリンクを介して共有

**ドキュメントベースのオーサリング：**

1. **[Excel](/help/edge/docs/forms/create-forms.md)**&#x200B;とEdge Delivery Servicesを使用してフォームを作成し、高性能なフォームを作成する
2. 最適な読み込み速度とSEOを実現する&#x200B;**[Edge Delivery](/help/edge/docs/forms/publish-forms.md)**&#x200B;への公開

**従来のフォームのサポート：**

- モバイル向けに最適化されたXFA フォーム レンダリング用の&#x200B;**[HTML5 Forms](/help/forms/introductionhtml5.md)**

### 高度な実装：ビジネスプロセス {#advanced-implementation}

複数のシステム、ドキュメント生成、承認ワークフローを含む複雑な要件の場合：

**データ統合とワークフロー：**

1. **[バックエンドシステムを接続するためのフォームデータモデル](/help/forms/create-form-data-models.md)**&#x200B;の設定
2. 承認とルーティング用の&#x200B;**[デザインワークフロープロセス](/help/forms/aem-forms-workflow.md)**
3. パフォーマンスを測定するための&#x200B;**[Analytics](/help/forms/integrate-aem-forms-with-adobe-analytics.md)**&#x200B;の設定

**Document Services &amp; Communications:**

1. **[自動化されたドキュメント生成用の通信API](/help/forms/aem-forms-cloud-service-communications-introduction.md)**&#x200B;の実装
2. パーソナライズされた明細書と通知の&#x200B;**[インタラクティブ通信の作成](/help/forms/interactive-communication/create-interactive-communication.md)**
3. **[一元化されたフォーム管理用にForms ポータル](/help/forms/configure-forms-portal.md)**&#x200B;を設定する

### 大規模な展開：規模の拡大とガバナンス {#enterprise-deployment}

ガバナンス、コンプライアンス、監視が必要な組織全体のデプロイメントの場合：

**アーキテクチャとガバナンス：**

1. **[スケーラブルなデプロイメントのためのアーキテクチャパターン](/help/forms/aem-forms-cloud-service-architecture.md)**&#x200B;の確認
2. **[ユーザー管理](/help/forms/forms-groups-privileges-tasks.md)**&#x200B;とアクセス制御の設定
3. **[チームの共同作業のための開発ワークフローの設定](/help/forms/setup-local-development-environment.md)**

**移行と監視：**

1. **[既存システムからの移行戦略を計画](/help/forms/migrate-to-forms-as-a-cloud-service.md)**
2. 使用状況の追跡とコンプライアンスのために&#x200B;**[トランザクションモニタリング](/help/forms/transaction-reports-billable-apis.md)**&#x200B;を実装する

<details>
<summary><strong>❓よくある質問</strong></summary>

**フォームビルダーとは**
フォームビルダーとは、コーディングなしでデジタルフォームを作成できるツールです。 ドラッグ&amp;ドロップ操作のインターフェイスを利用してフォームをデザインし、テキストボックスやドロップダウンなどのフィールドを追加して、オンラインで公開することで、オーディエンスのデータを収集できます。

**オンラインフォームを作成するにはどうすればよいですか？**
AEM Formsなら、コアコンポーネントをドラッグ&amp;ドロップ方式で視覚的に編集できるエディターを利用して、アダプティブフォームを作成できます。また、Edge Delivery Servicesを利用してパフォーマンスの高いフォームを作成したり、基盤コンポーネントを利用して既存のワークフローを構築することも可能です。 まず、テンプレートを選択し、フォームフィールドを追加し、データ接続を設定し、複数のチャネルをまたいで公開します。

**優れたオンラインフォームとは何ですか？**
優れたオンラインフォームは、モバイル対応で読み込みが速く、ラベルが明確になり、論理的なフィールドの順序を使用し、エラーを防ぐために検証を含め、送信時にユーザーにすばやくフィードバックを提供します。

**フォームを他のビジネス システムと統合できますか？**
モダンなフォームビルダーは広範な統合機能を提供します。 フォームをCRM システム、メールマーケティングプラットフォーム、データベース、クラウドストレージ、ワークフローオートメーションツールに接続することで、ビジネスプロセスを合理化できます。

**オンラインフォームは安全ですか？**
プロフェッショナルなフォームビルダーは、データの暗号化や安全なデータ送信、アクセス制御、GDPR、HIPAA、CCPAなどの規制へのコンプライアンスなど、エンタープライズレベルのセキュリティ機能を備えており、機密情報の保護に役立ちます。

**フォームに電子サインを追加するにはどうすればよいですか？**
デジタル署名は、Adobe Signまたはその他の電子サインプロバイダーを使用して、フォームに直接統合できます。 これにより、フォームエクスペリエンス内でドキュメントに署名できるようになり、個別の署名ワークフローの必要がなくなり、フォームの放棄を減らすことができます。

**フォームでPDF ドキュメントを自動生成できますか？**
はい。モダンなフォームプラットフォームでは、フォームが送信されたときに、PDFの領収書、確認書、記録文書を自動的に生成できます。 これはコンプライアンスや記録の管理、ユーザーへの即時確認に欠かせません。

**フォームのパフォーマンスと分析を追跡するにはどうすればよいですか？**
フォーム分析は、完了率、放棄パターン、ユーザーの行動などを把握するのに役立ちます。 Adobe Analyticsなどの分析プラットフォームと連携することで、どのフィールドが顧客の摩擦を引き起こしているのか、コンバージョン率を最適化する方法に関するインサイトを得ることができます。

**フォームワークフローオートメーションとは**
フォームのワークフローを自動化することで、承認プロセスを通じて送信がルーティングされ、チームメンバーにタスクが割り当てられ、他のビジネスシステムでアクションがトリガーされます。 これにより、手作業による処理が不要になり、フォームデータの一貫した処理が可能になります。

**障害のあるユーザーがフォームにアクセスできるようにするにはどうすればよいですか？**
[ アクセス可能なフォーム ](/help/forms/creating-accessible-adaptive-forms.md)には、適切なラベル付け、キーボードナビゲーション、スクリーンリーダーの互換性、WCAG ガイドラインへの準拠が含まれます。 これにより、すべてのユーザーが、能力や支援テクノロジーに関係なく、フォームに記入できるようになります。

**フォームビルダーの費用はいくらですか？**
AEM Forms as a Cloud Serviceの価格は、それぞれの要件、使用量、機能のニーズによって異なります。 価格の詳細と自社に最適なソリューションについては、Adobeの担当者またはAdobeの担当者にお問い合わせください。

</details>

## 次の手順 {#next-steps}

現在の優先順位に一致する機能を確認します。

- **[最初のフォームを作成](/help/forms/creating-adaptive-form-core-components.md)**&#x200B;して、オーサリング環境を体験します
- **[導入計画のためのアーキテクチャオプション](/help/forms/aem-forms-cloud-service-architecture.md)**&#x200B;の確認
- **[チームの共同作業のための開発環境](/help/forms/setup-local-development-environment.md)**&#x200B;の設定
- **[既存システムを接続するための統合オプションを探る](/help/forms/data-integration.md)**

包括的な実装ガイダンスは、Adobe Professional Servicesを利用してデプロイメントを加速し、ベストプラクティスを最初から確立することを検討してください。
