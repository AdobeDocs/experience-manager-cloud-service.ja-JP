---
title: Forms Experience Builder
description: フォームフラグメントを使用した強力なフォームの迅速な作成
feature: Edge Delivery Services
hide: true
index: false
hidefromtoc: true
role: Admin, Architect, Developer
source-git-commit: 9996bc602ae6169dd1aade622d5dbc5b1addeb54
workflow-type: tm+mt
source-wordcount: '1113'
ht-degree: 3%

---


# Forms Experience Builder の概要

>[!IMPORTANT]
>
> **ドキュメントは変更される場合があります**：このドキュメントは現在製品に対してテスト中であり、更新および改訂される可能性があります。Forms Experience Builder が早期導入プログラム中に進化し続けると、機能、コマンド、例が変わる場合があります。

Forms Experience Builder は、Adobe Experience Manager（AEM）Formsに人工知能の機能を導入します。 この革新的なソリューションは、組織が自然言語のやり取りとインテリジェントな自動化を通じて、デジタルフォームをどのように作成、管理、最適化するかを変えます。

最新の web テクノロジーに基づき、高度な AI サービスを活用して構築されたForms Experience Builder を使用すると、技術ユーザーとそれ以外のユーザーの両方が、対話型インターフェイスを通じて高度なプロフェッショナル向けのフォームを作成できます。 単純な登録フォームを必要とするビジネスアナリストでも、複雑な複数の手順のワークフローを作成する開発者でも、Forms Experience Builder は、フォーム作成プロセス全体を合理化します。

## 対話型インターフェイス

Forms Experience Builder には、会話を開くように簡単にフォームを作成できる直感的なチャットベースのインターフェイスが用意されています。

```
┌─────────────────────────────────────────────────────────┐
│ Forms Experience Builder                               │
├─────────────────────────────────────────────────────────┤
│                                                         │
│  👤 User: Create a customer feedback form              │
│                                                         │
│  🤖 AI: I'll help you create a feedback form. What    │
│       type of feedback do you want to collect?         │
│                                                         │
│  👤 User: Product reviews with ratings and comments    │
│                                                         │
│  🤖 AI: Perfect! I've created a feedback form with:   │
│       * Product rating (1-5 stars)                     │
│       * Comment field                                   │
│       * Customer email (optional)                       │
│       * Submit to email notification                    │
│                                                         │
│  👤 User: Add a field for product category             │
│                                                         │
│  🤖 AI: Added a dropdown field with common categories  │
│                                                         │
└─────────────────────────────────────────────────────────┘
```

## コア機能

### AI を活用したフォームの作成

**自然言語形の生成**

分かりやすい英語の説明を使用して、完全なフォームをゼロから作成します。 「評価スケールとコメントフィールドを含んだカスタマーフィードバックフォームを作成する」などの要件を記述するだけで、Forms Experience Builder が適切なフォーム構造、フィールドタイプ、検証ルールを生成します。

**動的なフィールド管理**

対話型コマンドを使用して、フォームフィールドを追加、変更、削除する。 AI はコンテキストを認識し、要件に基づいて、フィールドタイプ、検証ルールおよびユーザーインターフェイスの改善をインテリジェントに提案できます。

**レイアウトの最適化**

自然言語によるフォームのレイアウトおよび設定の更新。 「フォームをよりモバイルに適したものにする」や「論理フローでフィールドを再編成する」などの変更をリクエストし、Forms Experience Builder が適切なスタイル設定とレイアウトの調整を適用します。

### インテリジェントなインポートと変換

**PDFからフォームへのコンバージョン**

静的なPDF ドキュメントをインタラクティブな動的フォームに変換する。 PDF ドキュメントをアップロードすると、Forms Experience Builder が構造を分析し、適切なフィールドタイプと検証を持つ、対応するデジタルフォームを作成します。

**フォームコンバージョンの URL**

既存の web フォームまたはページをAEM Formsに変換する。 URL を指定するだけで、Forms Experience Builder がフォーム要素を抽出し、ネイティブのAEM Formsとして再作成し、機能を強化します。

**複数形式ファイルのサポート**

PDF、画像、スクリーンショット、既存のフォームテンプレートなど、フォーム作成の様々なファイルタイプを処理します。 Forms Experience Builder は、これらを処理して機能的なAEM Formsに変換できます。

### 高度なフォームロジックと統合

**インテリジェントなルール生成**

自然言語を使用して、複雑なフォーム検証ルールおよびビジネスロジックルールを作成します。 Forms Experience Builder では、通常コーディングに関する広範な知識が必要になる高度な条件付きロジック、フィールドの依存関係および検証ルールを生成できます。

**包括的な送信アクションの設定**

既存のビジネスシステムと統合するようにフォーム送信を設定します。

- **メール統合**：自動メール通知および確認の設定
- **REST API エンドポイント**：カスタムアプリケーションおよびサービスへの接続
- **クラウドストレージ**:Azure Blob Storage、SharePoint、OneDrive との統合
- **ワークフローの自動処理**: Power Automate とWorkfront Fusion に接続する
- **マーケティングプラットフォーム**:Marketoとの直接統合によるリード管理
- **AEM ワークフロー**：既存のAEM ワークフロー機能の活用

**パフォーマンス分析**

フォーム変換のパフォーマンスとユーザーエンゲージメントのパターンを分析します。 Forms Experience Builder では、フォームの効果に関するインサイトを提供し、完了率とユーザーエクスペリエンスを向上させるための最適化について提案します。

## 仕組み

Forms Experience Builder は、シンプルで対話型のアプローチに従います。

```
┌─────────────────┐    ┌─────────────────┐    ┌─────────────────┐
│  1. Describe    │───▶│  2. AI Creates  │───▶│  3. Refine &    │
│  Your Form      │    │  Initial Form   │    │  Configure      │
│  Requirements   │    │                 │    │                 │
└─────────────────┘    └─────────────────┘    └─────────────────┘
         │                       │                       │
         │                       │                       │
         ▼                       ▼                       ▼
┌─────────────────────────────────────────────────────────────────┐
│  "Create a loan application form"  →  Form with relevant        │
│  "Add conditional logic"           →  fields and basic          │
│  "Connect to CRM system"           →  validation rules          │
└─────────────────────────────────────────────────────────────────┘
```

## 使用例

### ローン申し込みフォーム

```
┌─────────────────────────────────────────────────────────┐
│ Loan Application - Multi-Step Form                    │
├─────────────────────────────────────────────────────────┤
│ Step 1: Personal Information                           │
│  🏠 Property Type: [Primary] [Investment] [Commercial] │
│  💰 Loan Amount: [$_______] (triggers different paths) │
│  📊 Income Verification: [W2] [Self-Employed] [Other]  │
│                                                         │
│ Step 2: Financial Details (conditional based on above) │
│  ↳ If Self-Employed: Show tax returns, profit/loss     │
│  ↳ If W2: Show employment history, pay stubs           │
│  ↳ Complex debt-to-income calculations                 │
│                                                         │
│ Step 3: Compliance & Review                            │
│  📋 Regulatory disclosures, digital signatures         │
│  🔍 Automated eligibility pre-screening                │
└─────────────────────────────────────────────────────────┘
```

### 保険金請求フォーム

```
┌─────────────────────────────────────────────────────────┐
│ Insurance Claim - Adaptive Form                        │
├─────────────────────────────────────────────────────────┤
│ 🚗 Claim Type: [Auto] [Property] [Health] [Business]   │
│                                                         │
│ ↳ Auto Selected: Shows accident details, police report │
│ ↳ Property: Shows damage assessment, repair estimates  │
│ ↳ Health: Shows medical provider network, pre-auth     │
│                                                         │
│ 📎 Dynamic Document Requirements:                       │
│   * Photos/videos of damage                            │
│   * Police reports (auto only)                         │
│   * Medical records (health only)                      │
│   * Repair estimates (property only)                   │
│                                                         │
│ 🔄 Real-time claim status updates                      │
└─────────────────────────────────────────────────────────┘
```

### 移行と変換のシナリオ

AI を活用したコンバージョンで、既存のフォームを強力なデジタルエクスペリエンスに変換します。


#### PDF formsをデジタルFormsに変換

自動計算とモバイルレスポンシブデザインを使用して、複数のフィールドを持つPDF formsを動的なデジタルエクスペリエンスに変換します。

**主なメリット：**

- 自動税金計算とフィールドの依存関係
- デジタル署名と電子ファイルの統合
- モバイルレスポンシブレイアウトの最適化
- 処理エラーを 95 % 削減


#### 最新化のレガシー XFA ベースのフォーム

複雑な XFA アプリケーションを、リアルタイムの検証とアクセシビリティコンプライアンスを備えた最新のマルチステップウィザードに変換できます。

**主なメリット：**

- 合理化された複数手順のウィザードインターフェイス
- コンテキストヘルプを使用したリアルタイム検証
- 政府データベースの統合
- WCAG 2.1 アクセシビリティフルコンプライアンス


#### フォームのスクリーンショットをデジタルフォームに変換する

あらゆる紙のフォームをデジタルエクスペリエンスに変換できます。 AEM Formsは、レイアウトを自動的に最適化し、スクリーンショットから統合対応のデジタルフォームを作成します。

**主なメリット：**

- インテリジェントフィールドタイプの検出
- 最適化されたレスポンシブレイアウトの生成
- オリジナルの紙よりも検証を強化
- 統合対応アーキテクチャ

#### 既存の web フォームの読み込みと拡張

既存の web フォームをインポートし、既存の機能を壊すことなく、高度な検証、条件付きロジックおよびマルチチャネル送信をフォームに追加できます。

**主なメリット：**

- 高度な検証ロジックとルール
- 条件付きフィールドの動作とワークフロー
- マルチチャネル送信オプション
- 組み込みの分析とパフォーマンストラッキング

## Forms Experience Builder と従来の開発の比較

| 項目 | 従来のフォーム作成 | Forms Experience Builder |
|--------|---------------------------|----------------------|
| **作成にかかる時間** | 2 ～ 3 日間 | 2 ～ 3 時間 |
| **技術的知見** | 必須 | 不要 |
| **検認規程** | 手動コーディング | 自然言語 |
| **モバイルの最適化** | 手動の CSS/JS | 自動 |
| **アクセシビリティ** | 手動での実装 | 組み込みコンプライアンス |
| **更新** | コードの変更が必要です | 自然言語 |


## 組織にとってのメリット

### 民主化されたフォームの作成

技術に詳しくないユーザーが、プログラミングの知識を持たずに高度なフォームを作成できるようにします。 ビジネスアナリスト、特定分野の専門家、コンテンツ作成者は、自然言語での会話を通じて、要件を機能的なフォームに直接翻訳できます。

### 価値創出までの時間（TTV）の短縮

フォーム開発を数日から数時間へと大幅に高速化します。 従来、広範な開発サイクルが必要だった作業を、会話型 AI を使用して 1 回のセッションで実行できるようになり、デジタルイニシアティブの市場投入を迅速化できます。

### インターフェイスのシンプルさ

直感的な会話型インターフェイスにより、学習曲線をなくします。 ユーザーは、技術的なフォーム作成ツールを学習する代わりに自然言語を使用して複雑なフォームを作成でき、トレーニング時間を短縮し、採用を増やすことができます。

### 最新化の取り組みの拡大

レガシーフォームポートフォリオを効率的に最新化する。 既存のPDF、XFA およびHTML フォームをレスポンシブなデジタルエクスペリエンスに変換すると同時に、ビジネスロジックを維持し、フォームエコシステム全体でのユーザーエクスペリエンスを強化します。

## はじめに

Forms Experience Builder の使用を開始するには、[Forms Experience Builder ドキュメント ](forms-ai-assistant-getting-started.md) を参照してください。 Forms Experience Builder には、好みのワークフローに応じて、AEM Forms エディターまたはユニバーサルエディターからアクセスできます。

フォーム作成プロセスの変革を目指す企業のために、Forms Experience Builder は、対話型 AI の柔軟性とエンタープライズクラスのフォーム管理の堅牢性を組み合わせた、強力で直感的なソリューションを提供します。

## オンボーディングとアーリーアクセス

Forms Experience Builder は現在、早期アクセス（EA）プログラムの一部として利用できます。 参加してアクセスするには、次の手順に従います。

1. 組織に関連付けられた仕事用の公式メールアドレスを使用していることを確認します。
2. [aem-forms-ea@adobe.com](mailto:aem-forms-ea@adobe.com) にForms Experience Builder へのアクセスをリクエストするメールを送信します。
3. オンボーディングプロセスを迅速に行うために、組織名と関連するプロジェクトの詳細をリクエストに含めます。

>[!NOTE]
>
> Forms Experience Builder へのアクセスは、早期アクセスプログラムで承認された参加者に制限されます。 Adobeはリクエストを確認し、対象となる場合はオンボーディングの詳細な手順を提供します。

Early Access プログラムとその機能について詳しくは、[AEM Forms Early Access ドキュメント ](/help/forms/early-access-ea-features.md) を参照してください。

