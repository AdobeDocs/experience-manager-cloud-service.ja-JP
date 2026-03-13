---
title: Experience Modernization Agent の概要
description: Experience Modernization Agent が AI を使用して、新しい web サイトをEdge Delivery Servicesにオンボードする方法を説明します。
feature: Edge Delivery Services, Agentic AI
role: User, Admin, Architect, Developer
exl-id: c23a6f55-2ba8-4290-b7e8-06cad5de0fc8
source-git-commit: 84fed5a82d6c23cd51d9796eb644121c6ef06a29
workflow-type: tm+mt
source-wordcount: '875'
ht-degree: 0%

---


# Experience Modernization Agent の概要 {#experience-modernization-agent}

AI を利用して Experience Modernization Agent が web サイトをEdge Delivery Servicesにオンボードする方法を説明します。

## はじめに {#introduction}

[Experience Modernization Agent は、Brand Experience Agentの一部として &#x200B;](/help/ai-in-aem/agents/brand-experience/overview.md)Web サイトの移行と基本的なサイト設定を自動化することで、Edge Delivery Servicesへのオンボーディングを促進します。

[&#x200B; サイト作成と移行のスキル &#x200B;](#creation-migration) を組み合わせて、最初の web サイトのオンボーディングと [&#x200B; ブロック開発機能 &#x200B;](#block-development) を行い、サイト作成と移行のワークフローをサポートします。 さらに、直接使用できる web ベースの AI 支援開発環境として [Experience Modernization Console](#console) を提供します。 ユーザーはこのコンソールを介してエージェントを直接操作できますが、開発者はどの船を完全に制御できるかについては、引き続き説明します。

複雑な移行や優先度の高い移行の場合、Adobeでは、Experience Modernization Agent を使用して実稼動対応のEdge Delivery サイトを配信するように設計されたエンジニアリング主導のサービスである [Agentic Outcome Engineer （AOE）配信モデル &#x200B;](#aoe-delivery) を提供します。

## メリット {#benefits}

Experience Modernization Agent を使用すると、[Edge Delivery Services](/help/edge/overview.md) の導入の価値を生み出すまでの時間が短縮され、ブランドの web エクスペリエンスを柔軟に調整できるようになります。

* **高速**:AI 自動化は、繰り返しの移行作業（コンテンツの読み込み、ブロックマッピング、設計システムアプリケーション）を処理し、従来のアプローチと比較して移行タイムラインを圧縮します
* **効率化を重視**：自動化によって反復作業が減り、チームはより価値の高い実装作業に集中できます
* **誰でもアクセス可能**：自然言語リクエストでは、技術に詳しくないユーザーでも web サイトの変更にアクセスできるようになり、ライブプレビューで変更を即座に検証できます
* **エンタープライズガバナンス**：デベロッパーは、GitHub と統合されたレビューワークフローを通じて、運用される内容に対する完全な権限を維持します
* **移行後の柔軟性**：チームがEdge Delivery Services パターンを使用して、移行したサイトを拡張および調整できるようになります。

## サイトの作成と移行スキル {#creation-migration}

Experience Modernization Agent は、新しいEdge Delivery Services サイトを作成し、既存の web サイトを移行するためのスキルを備えています。 Edge Delivery Servicesの新しいサイトや移行では、これらのスキルを活用することをお勧めします。

* 数か月から数週間または数日にわたって Web サイトの作成と移行を促進し、Edge Delivery Servicesの導入に要する時間を大幅に短縮
* 様々なCMS プラットフォーム、従来のAEMまたはデザインシステム（Figma など）から実稼動対応のEdge Delivery Services プロジェクトへの移行をサポートします。
* Edge Delivery Servicesのガイダンスに沿ったパフォーマンス、アクセシビリティ、レスポンシブデザインに関するベストプラクティスをサポート

詳細なスキルには、ページ移行、一括読み込み、デザイン抽出、ナビゲーション設定、web スクレーピングが含まれます。

## ブロック開発機能 {#block-development}

Experience Modernization Agent は、様々な開発タスクに対応する一般的なEdge Delivery Services開発機能を利用して、最初のサイトの作成や移行に留まらず、継続的な価値を提供します。

* 作成者にとって使いやすいコンテンツモデルを、コンテンツ駆動開発（CDD）手法に従う
* [&#x200B; ブロックコレクション &#x200B;](https://www.aem.live/developer/block-collection) および [&#x200B; ブロックパーティ &#x200B;](https://www.aem.live/developer/block-party/) を活用して、参照実装とベストプラクティスを見つけます
* デプロイメント前に変更を検証するためのテストワークフローとデバッグワークフローをサポート

詳細な機能には、ブロック開発、コンテンツモデリング、参照ブロック検出、テスト、デバッグが含まれます。

## Experience Modernization コンソール {#console}

Experience Modernization Agent は、[`aemcoder.adobe.io`.](https://aemcoder.adobe.io) で web インターフェイスとして公開される、Edge Delivery Servicesの web ベースの AI 支援開発環境を提供します

* ユーザーが自然言語で変更を促すメッセージをすぐに開始できるように、コンソールをローカルに設定する必要はありません。
* AEMのライブプレビューでプレビューしながら日々のエクスペリエンス開発タスクを迅速に実行し、コンテンツをAEMに同期します。
* コンソールは、標準の GitHub レビューワークフローを通じてエンタープライズガバナンスをサポートしています。

セルフサービス Experience Modernization Console が一般入手可能になりました。 関心のあるユーザーは、スムーズなオンボーディングエクスペリエンスを確保するためにアクセスをリクエストできます。

Experience Modernization Console の基本を学ぶ

* ドキュメントのオーサリングをターゲットにしてサイトを最新化する場合は、[&#x200B; ここから開始 &#x200B;](/help/ai-in-aem/agents/brand-experience/modernization/getting-started.md) してください。
* AEMのオーサリングをターゲットにしてサイトを最新化する場合は、[&#x200B; ここから開始 &#x200B;](/help/ai-in-aem/agents/brand-experience/modernization/getting-started-aem-authoring.md) してください。

## Agentic Outcome Engineer （AOE）による配信 {#aoe-delivery}

複雑な移行や迅速な結果を実現するために、Adobeでは Agentic Outcome Engineer （AOE）を提供しています。 これは、Adobeのエンジニアがお客様に代わって Experience Modernization Agent を操作するオプションのサービスで、AI の自動処理と専門的なガイダンスを組み合わせて、実稼動に対応した結果を大規模に提供します。 AOE 配信について詳しくは、ドキュメント [&#x200B; エクスペリエンス最新化エージェントの AOE 配信 &#x200B;](/help/ai-in-aem/agents/brand-experience/modernization/aoe-delivery.md) を参照してください。

次の移行で AOE モデルに関心がある場合：

* スコーピングとスケジュールを開始するには、Adobeの担当者またはアカウントチームにお問い合わせください。
* Adobeは、実施要件を確認し、エンゲージメントを推定し、エンゲージメントプランを提案します。

## 制限事項 {#limitations}

次のユースケースでは、Experience Modernization Agent のスキルに加えて、追加の実装作業が必要です。

掻き取りスキルは、次のソースをサポートしていません。

* イントラネットまたは保護されたソース （認証、VPN、アクセスできないファイアウォールの背後にあるコンテンツなど）
* 複雑な動的コンテンツ（DOM に表示するために高度なユーザーインタラクションが必要なコンテンツなど）。
   * 特定の URL からコンテンツにアクセスできる場合は、クライアントサイドでレンダリングされたコンテンツがサポートされます。
   * CSS 経由で非表示になっているが、タブ、アコーディオン、カルーセルなど DOM に存在する要素もサポートされます。

エージェントは次のターゲットをサポートしていません。

* サイトが HTL ベースの配信を使用するAEM公開環境
   * このスキルはEdge Delivery Servicesのみを対象としています。
* API のみの配信や SPA ベースの配信などのヘッドレス配信パターン（Next.js など）

以下の要件は、専用の自動化スキルの対象外であり、手動での作業が必要です。

* 厳格なピクセル完全性
   * 実用的な設計忠実さのみが自動化されます
* サーバーまたはクライアントサイドのサードパーティのデータやサービスの統合
* コマースまたは検索機能の統合
* MarTech データレイヤーまたはターゲティング/実験
* コンテンツ/エクスペリエンスフラグメントの分離
* マルチサイト継承（MSM）
* カスタム機能（カリキュレータ、コンフィギュレータなど）
* カスタムビジネスロジック

## 次の手順 {#next-steps}

ドキュメント [Experience Modernization Agent 使用の手引き &#x200B;](/help/ai-in-aem/agents/brand-experience/modernization/getting-started.md) を使用してサイトを移行することから開始します。
