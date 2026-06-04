---
title: Experience Modernization Agentの概要
description: Experience Modernization Agentが、AIを活用して新しいWeb サイトをEdge Delivery Servicesにオンボーディングする方法について説明します。
feature: Edge Delivery Services, Agentic AI
role: User, Admin, Developer
exl-id: c23a6f55-2ba8-4290-b7e8-06cad5de0fc8
source-git-commit: 30037f08d5caeab878b6cf89b936308d16ae3e8d
workflow-type: tm+mt
source-wordcount: '1269'
ht-degree: 0%

---


# Experience Modernization Agentの概要 {#experience-modernization-agent}

Experience Modernization Agentが、AIを活用してweb サイトをEdge Delivery Servicesにオンボーディングする方法をご紹介します。

## はじめに {#introduction}

[Brand Experience Agentの一部として、](/help/ai-in-aem/agents/brand-experience/overview.md)Experience Modernization Agentは、web サイトの移行と基本サイトの設定を自動化することで、Edge Delivery Servicesへのオンボーディングを高速化します。

初期web サイトのオンボーディング用に[ サイトの作成と移行のスキル ](#creation-migration)を、サイトの作成と移行のワークフローをサポートするために[ ブロック開発機能](#block-development)を組み合わせています。 また、Web ベースのAI支援による開発環境として、[Experience Modernization Console](#console)を直接利用できます。 ユーザーはそのコンソールを通じて直接エージェントを操作できますが、開発者は出荷内容を完全に制御できます。

複雑または優先度の高い移行の場合、Adobeでは、[Agentic Outcome Engineer （AOE）配信モデル、](#aoe-delivery)Experience Modernization Agentを使用して本番環境に対応したEdge Delivery サイトを配信するように設計されたエンジニアリング主導のサービスを提供します。

## メリット {#benefits}

Experience Modernization Agentは、[Edge Delivery Services](/help/edge/overview.md)導入の価値実現までの時間を短縮し、ブランドのweb体験を適応させる俊敏性を提供します。

* **高速**: AI オートメーションは、反復的な移行作業（コンテンツの読み込み、ブロックマッピング、デザインシステム アプリケーション）を処理し、従来のアプローチと比較して移行タイムラインを圧縮します
* **効率性に重点を置く**：自動化によって反復的な作業が削減されるため、チームはより価値の高い実装作業に集中できるようになります
* **誰でもアクセス可能**：自然言語のリクエストにより、技術的な知識を持たないユーザーでもweb サイトの変更にアクセスできるようになり、ライブプレビューで変更をすぐに検証できます
* **エンタープライズガバナンス**：開発者は、GitHubと統合されたレビューワークフローを通じて、公開される内容に対する完全な権限を維持します
* **移行後の柔軟性**:Edge Delivery Services パターンを使用して、移行されたサイトを拡張および改良できます

## サイトの作成と移行のスキル {#creation-migration}

Experience Modernization Agentは、新しいEdge Delivery Services サイトを作成し、既存のweb サイトを移行するためのスキルを提供します。 新しいEdge Delivery Services サイトまたは移行では、これらのスキルを活用することをお勧めします。

* Edge Delivery Servicesを導入することで、web サイトの構築と移行を数か月から数週間、数日に短縮し、価値実現までの時間を大幅に短縮できます
* CMS プラットフォーム、レガシーAEM、デザインシステム（Figmaなど）の幅広い範囲からの実稼動対応のEdge Delivery Services プロジェクトへの移行をサポートします
* Edge Delivery Services ガイダンスに沿ったパフォーマンス、アクセシビリティ、レスポンシブデザインのベストプラクティスをサポートしています

詳細なスキルには、ページの移行、一括読み込み、デザイン抽出、ナビゲーション設定、web スクレイピングなどがあります。

## Figma ベースの移行とページ作成 {#figma}

Experience Modernization Agentは、ライブサイトの移行に加えて、Figmaをデザインソースとして使用できます。 これらの機能を使用するには、[Experience Modernization ConsoleでFigmaの詳細を設定します。](/help/ai-in-aem/agents/brand-experience/modernization/console.md)

### Figma派生ブロックを使用した移行の再設計 {#figma-redesign}

既存のweb サイトを再設計されたエクスペリエンスに移行する場合、エージェント [は最初にFigma コンポーネントから再設計されたブロック コレクションを確立し、](/help/ai-in-aem/agents/brand-experience/modernization/prompting-guide.md#figma-redesign-migration)その後、ライブ ソース web サイトに対してサイト移行を実行し、ソース コンテンツをそれらのFigma派生ブロックにマッピングします。

* **Figma**&#x200B;は、ターゲットデザインおよびブロックライブラリソースです。
* **ライブ web サイト**&#x200B;はコンテンツのソースのままです。
* コンテンツはソース web サイトに対して検証され、ビジュアル出力はFigma派生デザインシステムに対して検証されます。

### Figmaから新しいページを作成する {#figma-new-page}

ソース web サイトにページが既に存在しない場合、エージェント [は、Figma フレームまたはページから新しいEdge Delivery Services ページを直接生成し、Figma セクションを既存のブロック、デフォルトコンテンツ、または新しいバリエーションにマッピングします](/help/ai-in-aem/agents/brand-experience/modernization/prompting-guide.md#figma-new-page-from-figma)。 テキストとアセットはFigmaから来ています。

これらのワークフロー、個々のFigma ブロックの移行、プロンプトのヒントについて詳しくは、「[Experience Modernization Agentのプロンプト ガイド ](/help/ai-in-aem/agents/brand-experience/modernization/prompting-guide.md)」を参照してください。

## ブロック開発機能 {#block-development}

Experience Modernization Agentは、様々な開発作業に対応する一般的なEdge Delivery Services開発機能を活用し、初期のサイト作成や移行にとどまらない継続的な価値を提供します。

* 作成者にとって使いやすいコンテンツモデルのためのコンテンツ駆動開発（CDD）手法に従います
* [ ブロックコレクション ](https://www.aem.live/developer/block-collection)および[ ブロックパーティ ](https://www.aem.live/developer/block-party/)を利用して、参照実装とベストプラクティスを見つけます
* デプロイメント前に変更を検証するためのワークフローのテストとデバッグをサポート

詳細な機能には、ブロック開発、コンテンツモデリング、参照ブロックの発見、テスト、デバッグなどがあります。

## Experience Modernization Console {#console}

Experience Modernization Agentは、Edge Delivery Servicesのweb ベースのAI支援による開発環境を提供し、[`aemcoder.adobe.io`にweb インターフェイスとして公開します。](https://aemcoder.adobe.io)

* コンソールでは、ユーザーが自然言語ですぐに変更を求めるプロンプトを開始するためのローカル設定は必要ありません。
* AEMのライブプレビューを使用してエクスペリエンス開発タスクをプレビューし、コンテンツをAEMに同期しながら、日々の作業を迅速に完了。
* コンソールは、標準のGitHub レビューワークフローによるエンタープライズガバナンスをサポートしています。

セルフサービスのExperience Modernization Consoleが一般に利用可能です。 興味のあるユーザーは、スムーズなオンボーディング体験を実現するために、利用申請できます。

Experience Modernization Consoleの基本を学ぶ

* ドキュメント作成をターゲットにしてサイトを最新化する場合は、[こちらから始めてください。](/help/ai-in-aem/agents/brand-experience/modernization/getting-started.md)
* AEM オーサリングをターゲットにしてサイトを最新化する場合は、[こちらから始めてください。](/help/ai-in-aem/agents/brand-experience/modernization/getting-started-aem-authoring.md)

## プロジェクト文書作成スキル {#project-documentation}

プロジェクトの引き継ぎには時間がかかる性質があるため、[ オーサリングと開発作業が完了すると、プロジェクトドキュメントスキル ](/help/ai-in-aem/agents/brand-experience/modernization/project-documentation.md)は包括的なドキュメントを自動的に生成できます。

## サイトカタログスキル {#site-catalog}

サイトカタログスキルは、既存のweb サイトをクロールし、ページテンプレートとブロックのバリエーションをすべてカタログ化し、あらゆるテンプレートとブロックのスクリーンショットを取得して、レビュー用のインタラクティブなHTMLレポートバンドルを生成します。 このスキルは、次のような場合に役立ちます。

* **移行プロジェクトを開始するあらゆるユーザー**&#x200B;は、コードを記述する前にページレイアウト、ブロックバリアント、ロケール、ページごとのテンプレートの完全なインベントリを取得するため、正確な計画を立てて複雑さを早期に確認できます
* **一括読み込みを行う** チームが、同じレイアウトを共有するページを特定し、最初に代表ページを手動で読み込んで完成させ、そのテンプレートの残りのすべてのページを一括インポートします
* **プロジェクトのリードと関係者**&#x200B;による取り組みの範囲の把握

詳しくは、[ サイトカタログスキル ](/help/ai-in-aem/agents/brand-experience/modernization/site-catalog.md)のドキュメントを参照してください。

## Agentic Outcome Engineer （AOE）による配信 {#aoe-delivery}

複雑な移行や迅速な移行の場合、AdobeはAOE （エージェンティックアウトカムエンジニア）機能を提供します。 これは、AdobeのエンジニアがExperience Modernization Agentを担当し、AIによる自動化と専門家のガイダンスを組み合わせて、本番環境での使用に対応した結果を大規模に提供するオプションサービスです。 AOE配信について詳しくは、「[Experience Modernization AgentのAOE配信](/help/ai-in-aem/agents/brand-experience/modernization/aoe-delivery.md)」のドキュメントを参照してください。

次の移行のAOE モデルに興味がある場合：

* スコーピングとスケジュール設定については、Adobeの担当者またはアカウントチームにお問い合わせください。
* Adobeが利用条件を確認し、エンゲージメントを見積もり、エンゲージメントプランを提案します。

## 制限事項 {#limitations}

次のユースケースでは、Experience Modernization Agentのスキルに加えて、追加の実装の労力が必要です。

スクレイピングスキルは、次のソースをサポートしていません。

* 認証、VPN、ファイアウォールなどの背後にあるコンテンツにアクセスできない、イントラネットまたは保護されたソース
   * 代わりに、ブラウザーの認証コンテキストを利用して保護されたソースにアクセスできる[SLICC](https://www.sliccy.com)を使用します。
* 複雑な動的コンテンツ（例えば、高度なユーザーインタラクションを必要とするコンテンツなど）がDOMに表示される。
   * クライアント側でレンダリングされたコンテンツは、特定のURLを介してコンテンツにアクセスできる場合にサポートされます。
   * CSSで非表示になっている要素も、タブ、アコーディオン、カルーセルなどDOMに存在する要素もサポートされています。

エージェントは次のターゲットをサポートしていません。

* サイトがHTL ベースの配信を使用するAEM パブリッシュ環境
   * このスキルは、Edge Delivery Servicesのみを対象としています。
* APIのみの配信やSPA ベースの配信（Next.jsなど）などのヘッドレス配信パターン

次の要件は、専用の自動化スキルではカバーされないため、手作業が必要です。

* 厳密なピクセルの完全性
   * 実用的な設計忠実度のみが自動化されます
* サーバーまたはクライアントサイドのサードパーティデータ/サービスの統合
* コマースや検索機能の統合
* マーテクのデータレイヤーまたはターゲティング/実験
* コンテンツ/エクスペリエンスフラグメントの分離
* マルチサイト継承（MSM）
* カスタム機能（例：計算機、コンフィギュレーター）
* カスタムビジネスロジック

## 次の手順 {#next-steps}

ドキュメント [Experience Modernization Agentの概要](/help/ai-in-aem/agents/brand-experience/modernization/getting-started.md)を使用してサイトを移行することから始めます。

