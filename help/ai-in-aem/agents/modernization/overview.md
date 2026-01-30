---
title: Experience Modernization Agent の概要
description: Experience Modernization Agent が AI を使用して、新しい web サイトをEdge Delivery Servicesにオンボードする方法を説明します。
feature: Edge Delivery Services, Agentic AI
role: User, Admin, Architect, Developer
source-git-commit: a19b17517a096c93609cd5637deee9e04eb6ac37
workflow-type: tm+mt
source-wordcount: '891'
ht-degree: 0%

---


# Experience Modernization Agent の概要 {#experience-modernization-agent}

AI を利用して Experience Modernization Agent が web サイトをEdge Delivery Servicesにオンボードする方法を説明します。

>[!NOTE]
>
>Experience Modernization Agent は、以前の [Experience Production Agent](/help/ai-in-aem/agents/production/overview.md) の移行スキルより優先されます。

## はじめに {#introduction}

Experience Modernization Agent は、Web サイトの移行と継続的な進化を迅速かつスムーズに行うことで、Edge Delivery Services（AEM オーサリングを含む）の価値を最大限に引き出します。

[ サイト作成と移行スキル ](#creation-migration) を組み合わせて、最初の web サイトのオンボーディングに使用し、[ ブロック開発機能 ](#block-development) を継続的なエクスペリエンス開発（スタイルの更新、テンプレートの絞り込み、ランディングページの作成）に使用します。 さらに、直接使用できるホストされた AI 支援開発環境として [Experience Modernization Console](#console) を提供します。 ユーザーはこのコンソールを介してエージェントを直接操作できますが、開発者はどの船を完全に制御できるかについては、引き続き説明します。

さらに、複雑な移行を確実に成功させるために、Adobeでは [Agentic Outcome Engineer （AOE）配信モデル ](#delivery-model) を提供しています。 このオプションは、アクセラレータとして、または特定のプロジェクトの課題を取り除くのに役立つ戦術的なサービスとして使用できます。

## メリット {#benefits}

Experience Modernization Agent を使用すると、[Edge Delivery Services](/help/edge/overview.md) の導入の価値を生み出すまでの時間が短縮され、ブランドの web エクスペリエンスを柔軟に調整できるようになります。

* **高速**:AI 自動化により、繰り返しの移行作業（コンテンツの読み込み、ブロックマッピング、設計システムアプリケーション）を処理し、月単位の作業を数週間に圧縮
* **費用対効果**：自動化により反復作業が処理され、統合や戦略的意思決定などの高価値タスクにプロフェッショナルサービスが利用できるようになります
* **誰でもアクセス可能**：自然言語リクエストでは、技術に詳しくないユーザーでも web サイトの変更にアクセスできるようになり、ライブプレビューで変更を即座に検証できます
* **エンタープライズガバナンス**：デベロッパーは、GitHub と統合されたレビューワークフローを通じて、運用される内容に対する完全な権限を維持します
* **継続的な価値**：エージェントは、スタイルの更新、テンプレートの絞り込み、ランディングページの作成など、継続的なサイト進化をサポートします

## サイトの作成と移行スキル {#creation-migration}

Experience Modernization Agent は、新しいEdge Delivery Services サイトを作成し、既存の web サイトを移行するためのスキルを備えています。 Edge Delivery Servicesの新しいサイトや移行では、これらのスキルを活用することをお勧めします。

* 数か月から数週間または数日にわたって Web サイトの作成と移行を促進し、Edge Delivery Servicesの導入に要する時間を大幅に短縮
* Web サイトを、任意のCMS、従来のAEMまたはデザインシステム（Figma など）から、実稼動用のEdge Delivery Services プロジェクトに変換します。
* Edge Delivery Servicesのすべての機能を提供します。つまり、高度な機能に対する AI の対応、高速なパフォーマンス（Core Web Vitals 最適化）、アクセシビリティ（WCAG 2.1 AA）、すべてのブレークポイントにわたるレスポンシブデザイン、コンテンツとコードの俊敏性です。

詳細なスキルには、ページ移行、一括読み込み、デザイン抽出、ナビゲーション設定、web スクレーピングが含まれます。

## ブロック開発機能 {#block-development}

Experience Modernization Agent は、様々な開発タスクに対応する一般的なEdge Delivery Services開発機能を利用して、最初のサイトの作成や移行に留まらず、継続的な価値を提供します。

* 作成者にとって使いやすいコンテンツモデルを、コンテンツ駆動開発（CDD）手法に従う
* [ ブロックコレクション ](https://www.aem.live/developer/block-collection) および [ ブロックパーティ ](https://www.aem.live/developer/block-party/) を活用して、参照実装とベストプラクティスを見つけます
* デプロイメント前に変更を検証するためのテストワークフローとデバッグワークフローをサポート

詳細な機能には、ブロック開発、コンテンツモデリング、参照ブロック検出、テスト、デバッグが含まれます。

## Experience Modernization コンソール {#console}

Experience Modernization Agent は、Edge Delivery Services用にホストされた AI 支援開発環境を提供し、[`aemcoder.adobe.io`.](https://aemcoder.adobe.io) で web インターフェイスとして公開します。

* ユーザーが自然言語で変更を促すメッセージをすぐに開始できるように、コンソールをローカルに設定する必要はありません。
* AEMのライブプレビューでプレビューしながら日々のエクスペリエンス開発タスクを迅速に実行し、コンテンツをAEMに同期します。
* 開発者が通常の GitHub レビューおよび承認プロセスを通じて、どの船を完全に制御できるかに応じて、エンタープライズガバナンスが適用されます。

セルフサービス Experience Modernization Console が一般入手可能になりました。 関心のあるユーザーは、スムーズなオンボーディングエクスペリエンスを確保するためにアクセスをリクエストできます。

## 配信モデル {#delivery-model}

複雑な移行や迅速な結果を実現するために、Adobeでは Agentic Outcome Engineer （AOE）配信モデルを提供しています。 これは、Adobe エンジニアがお客様に代わって AI ツールを操作するオプションのサービスです。

* Adobeの AOE は、AI 自動化と専門家のガイダンスを組み合わせて、エージェントを操作し、実稼動に適した結果を大規模に提供します。
* これにより、実装の停止や従来のモダナイゼーションの課題に直面している企業に対して、戦略的なリセットオプションを提供します。
* AOE モデルは、ガバナンス、品質、成功の成果を確保しながら、AI 自動化を活用する、より迅速でリスクの低い道筋を提供します。

AOE 配信モデルをさらに詳しく調べるには：

* スコーピングとスケジュールを開始するには、Adobeの担当者またはアカウントチームにお問い合わせください。
* Adobeは、実施要件を確認し、エンゲージメントを推定し、エンゲージメントプランを提案します。

## 制限事項 {#limitations}

次のユースケースでは、Experience Modernization Agent のスキルに加えて、追加の実装作業が必要です。

削り取りツールは、次のソースをサポートしていません。

* イントラネットまたは保護されたソース （認証、VPN、アクセスできないファイアウォールの背後にあるコンテンツなど）
* 複雑な動的コンテンツ（DOM に表示するために高度なユーザーインタラクションが必要なコンテンツなど）。
   * 特定の URL からコンテンツにアクセスできる場合は、クライアントサイドでレンダリングされたコンテンツがサポートされます。
   * CSS 経由で非表示になっているが、タブ、アコーディオン、カルーセルなど DOM に存在する要素もサポートされます。

エージェントは次のターゲットをサポートしていません。

* サイトが HTL ベースの配信を使用するAEM公開環境
   * このスキルはEdge Delivery Servicesのみを対象としています。
* API のみの配信や SPA ベースの配信などのヘッドレス配信パターン（Next.js など）

以下の要件は、まだ専用の自動化スキルでカバーされておらず、手動での作業が必要です。

* 厳格なピクセル完全性
   * 実用的な設計忠実さのみが自動化されます
* サーバーまたはクライアントサイドのサードパーティのデータやサービスの統合
* コマースまたは検索機能の統合
* MarTech データレイヤーまたはターゲティング/実験
* コンテンツ/エクスペリエンスフラグメントの分離
* マルチサイト継承（MSM）
* カスタム機能（カリキュレータ、コンフィギュレータなど）
* カスタムビジネスロジック
