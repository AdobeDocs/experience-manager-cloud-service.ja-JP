---
title: Site Migration Skill
description: サイト移行スキルは、AI とAdobe Forward Deployed Engineers （FDE）の助けを借りて、web サイトをEdge Delivery Servicesにオンボードします。
feature: Edge Delivery Services, Agentic AI
role: Admin, Architect, Developer
source-git-commit: 67d3081be74a654788eab96ae98f88ef7ce4203c
workflow-type: tm+mt
source-wordcount: '436'
ht-degree: 0%

---


# Site Migration Skill {#site-migration}

サイト移行スキルは、AI とAdobe Forward Deployed Engineers （FDE）の助けを借りて、web サイトをEdge Delivery Servicesにオンボードします。 このスキルは、コンテンツとスタイルの移行を自動化し、コード AEM オーサリングを通じてさらに適応できる作成者対応のEdge Delivery Services実装を準備します。

## 概要 {#overview}

サイト移行スキルは、既存のサイトまたはデザインをEdge Delivery Services プロジェクトに変換します。 スキルを使用した移行には、次のコンポーネントがあります。

* **ソース**：既存の web サイト（AEM Publish を含むすべてのCMS）、デザインシステム、またはデザインモック（Figma など）。
* **出力**：ブロックとスタイルが適用された、実稼動用のEdge Delivery Services リポジトリー
* **Targets**：すべてのEdge Delivery Services プラットフォームおよびオーサリング方法がターゲットとしてサポートされています
* **運用モデル**：質とガバナンスを確保するため、エージェントを運用し、移行をガイドするAdobe Forward のデプロイ済みエンジニアが提供

## 機能 {#capabilities}

サイト移行スキルは、次の大まかなタスクを実行します。

1. **コンテンツ移行** - ページとアセットを、選択したブロックライブラリに合わせたデフォルトコンテンツとブロックを使用して構造化されたEdge Delivery Services コンテンツに変換します。

2. **スタイルアプリケーション** – 次のいずれかの方法でEdge Delivery Servicesのスタイルを作成します。

   * 現在のサイトからの **現状のスタイル移行**
   * 提供されたモック **Figma など）を使用した** 再設計）
   * 既存のEdge Delivery Services実装から **既存のブロックデザインを再利用** できます

典型的な成果物は次のとおりです。

* Edge Delivery Services リポジトリ（ブロック、スタイル、設定）
* 移行されたコンテンツとアセット
* オーサリング設定（ドキュメントオーサリングまたはユニバーサルエディター）
* 移行されたサイトがデプロイされたEdge Delivery Services環境（プレビューとライブ）

その結果、パフォーマンス（Core Web Vitals/Lighthouse）、アクセシビリティ、ブレークポイントをまたいだレスポンシブレイアウトに最適化され、ドキュメントオーサリングまたはユニバーサルエディターを使用して完全に編集可能な、実稼動用に準備された web サイトが得られます。

## 制限事項 {#limitations}

サイト移行スキルでは、コンテンツとスタイルに重点を置いています。 次のユースケースでは、サイト移行のスキルに加えて、追加の実装作業が必要です。

* カスタム統合（コマース、CRM、検索コネクタなど）
* 動的コンテンツまたはレンダリング（非同期に読み込まれたコンテンツ、単一ページアプリケーション、カスタム JavaScript フレームワークなど）
* 移行されたエクスペリエンスに関係のない新しい機能の開発

これらの機能が必要な場合は、Adobe Consulting サービスまたは実装パートナーが、提供されるEdge Delivery プロジェクトを拡張できます。

## エンゲージメントモデル {#engagement}

サイト移行スキルは、現在、Adobe Forward Deployed Engineers が運営するエンゲージメントを通じて利用できます。 各プロジェクトは、ソースの複雑さ、設計目標、コンテンツの規模、ガバナンス要件に基づいたスコーピング演習から始まります。

移行を参照するには：

* スコーピングとスケジュールを設定するには、Adobeの担当者またはアカウントチームにお問い合わせください。
* Adobeは、適格性を確認し、エンゲージメントを推定して、移行プランを提案します。
