---
title: ユニバーサルエディターの概要
description: ユニバーサルエディターは、マーケティング組織が効果的な web エクスペリエンスを作成できるように設計された最新のビジュアルオーサリングツールです。
exl-id: d4fc2384-a0f5-4a6f-9572-62749786be4c
feature: Developing
role: Admin, Architect, Developer
source-git-commit: 08997c760bf1d609dce1dd17de0c549a26083917
workflow-type: tm+mt
source-wordcount: '948'
ht-degree: 96%

---


# ユニバーサルエディターの概要 {#introduction}

ユニバーサルエディターは、マーケティング組織が効果的な web エクスペリエンスを作成できるように設計された最新のビジュアルオーサリングツールです。

## 概要 {#overview}

ユニバーサルエディターは、Adobe Experience Manager Sites の一部である多用途のビジュアルエディターです。作成者が、任意のヘッドレスエクスペリエンスまたはヘッドフルエクスペリエンスを見たとおりに編集できる（WYSIWYG）機能です。次の機能があります。

* **即時編集**：作成者はプレビューエクスペリエンス内でコンテンツを直接編集できるので、個々のコンテンツソースを見つけて移動する必要がなくなります。
* **ビジュアル編集**：変更を行っている間、作成者は実際の訪問者エクスペリエンスに影響を与える変更を即座に確認できるので、摩擦が最小限に抑えられます。
* **検出可能なオプション**：明確にラベル付けされたオプションと直感的な UI により、作成者はメタデータを設定し、レイアウトを簡単に作成できます。
* **技術者以外**：編集には専門知識は必要ありませんが、企業のブランドガイドラインが自動的に適用されるので、組織全体でのコンテンツタスクの拡張が容易になります。
* **統合と拡張**：AEM と完全に統合されたユニバーサルエディターの柔軟な[拡張ポイント](#extensibility)により、すべての重要なツールを 1 つの包括的なインターフェイス内に統合できます。AI を活用した機能から、独自のビジネスニーズに合わせたカスタム拡張機能まで、チームがワークフローを効率化し、生産性を簡単に向上できるようにします。

概要：

* ユニバーサルエディターはあらゆる形式の AEM コンテンツに対して同じ一貫したビジュアル編集をサポートしているので、**作成者はその柔軟性の恩恵を受けることができます**。
* ユニバーサルエディターは実装の真の分離をサポートしているので、**開発者はユニバーサルエディターの汎用性の恩恵を受けることができます**。

ユニバーサルエディターは、サービスとしてのエディターの役割を真の意味で果たしており、全体的に柔軟性が向上しているので、最終的には[ページエディター](/help/sites-cloud/authoring/page-editor/introduction.md)に取って代わる予定です。

## サポートされているアーキテクチャ {#supported-architectures}

ユニバーサルエディターは、次の 2 つのプライマリ AEM 設定をサポートしています。

1. **[Edge Delivery Services](/help/edge/overview.md)**：これは、シンプルさ、価値実現までの時間の短縮、およびパフォーマンスの向上という点で推奨されるアプローチです。
1. **[ヘッドレス実装](/help/headless/introduction.md)**：既存のヘッドレスプロジェクトがある場合や、分離されたレンダリングの特定の要件がある場合、ユニバーサルエディターを使用すると、プロジェクト全体をリファクタリングすることなく、エンタープライズグレードのビジュアル編集が可能になります。ほとんどすべてのアーキテクチャ（SSR、CSR）、web フレームワーク（Next.js、React、Astro など）、ホスティングモデル（「独自導入のアプリ」）と互換性があります。

>[!TIP]
>
>サポートされているアーキテクチャについて詳しくは、[ユニバーサルエディターのユースケースと学習パス](/help/implementing/universal-editor/use-cases.md)ドキュメントを参照してください。

## サポートされている AEM バージョン {#aem-versions}

ユニバーサルエディターは、以下でサポートされています。

* AEM as a Cloud Service（リリース `2023.8.13099` 以降）
* [AEM 6.5 LTS](https://experienceleague.adobe.com/ja/docs/experience-manager-65-lts/content/implementing/developing/headless/universal-editor/introduction)
   * オンプレミスと AMS ホスティングの両方がサポートされています。
* [AEM 6.5](https://experienceleague.adobe.com/ja/docs/experience-manager-65/content/implementing/developing/headless/universal-editor/introduction)
   * オンプレミスと AMS ホスティングの両方がサポートされています。

このドキュメントは、AEM as a Cloud Serviceでユニバーサルエディターを使用する場合に使用します。

## 機能 {#features}

ユニバーサルエディターには、効率的なコンテンツ管理を行う様々なユースケースをサポートする多くの機能が用意されています。

* **[WYSIWYG](/help/sites-cloud/authoring/universal-editor/authoring.md)**：プレーンテキスト、リッチテキスト、メディア、メタデータなど、あらゆる形式の web コンテンツに対して、見たとおりの編集を実行します。
* **[構成](/help/sites-cloud/authoring/universal-editor/authoring.md#editing-content)**：様々なタイプのコンテンツブロック（タイトル、ボタン、ティーザー、セクション、埋め込みなど）を作成、編集、並べ替え、ネストまたは削除します。
* **[レイアウト](/help/sites-cloud/authoring/universal-editor/templates.md)**：ページテンプレートを利用し、ビジュアルスタイルを適用し、列、カルーセル、アコーディオンなどのブロックを使用してレイアウトを作成します。
* **[デバイスシミュレーション](/help/sites-cloud/authoring/universal-editor/navigation.md#emulator)**：編集中に、様々な訪問者のデバイスに合わせてコンテンツをプレビューおよび最適化します。
* **オムニチャネル**：構造化コンテンツと非構造化コンテンツの両方を複数のチャネルで再利用します。
* **[ローカライゼーション](/help/sites-cloud/authoring/universal-editor/inheritance.md)**：Multi-Site Manager を使用して、コンテンツ翻訳ワークフローを効率化し、ローカライズされたコンテンツの継承を効率的に処理します。
* **一貫性**：ブランドガイドラインに準拠し、すべてのコンテンツにわたって一貫性を維持します。
* **セキュリティ**：[堅牢なバージョン管理](/help/sites-cloud/authoring/sites-console/page-versions.md)により、[アクセス制御を適用](/help/implementing/universal-editor/authentication.md)し、コンテンツの整合性を保護し、変更を追跡します。
* **[公開](/help/sites-cloud/authoring/universal-editor/publishing.md)**：レビュー、承認および公開ワークフローをエディター内に直接統合します。
* **統合**：[Sites コンソール](/help/sites-cloud/authoring/sites-console/introduction.md)、[コンテンツフラグメントエディター](/help/sites-cloud/administering/content-fragments/overview.md)などの AEM ツールと完全に統合され、統一されたオーサリングエクスペリエンスを提供します。

## 拡張機能 {#extensibility}

ユニバーサルエディターは、標準の優れた機能を備えているだけでなく、様々な拡張機能も提供します。

* **拡張機能**&#x200B;は数多くあり、ワークフローのサポート、バリエーションの生成、実験の有効化などの要件をサポートするのにすぐに使用できます。
* **拡張可能な UI** を使用すると、既製の拡張機能が活用する同じ基盤フレームワークを使用して独自の拡張機能を作成できるので、プロジェクトのニーズに適応する究極の柔軟性が得られます。
* ブロック、カスタムデータタイプ、イベントなどの&#x200B;**拡張ポイント**&#x200B;により、UI を超えたカスタムビジネス要件のシームレスな統合が可能になります。

>[!TIP]
>
>ユニバーサルエディターの拡張機能について詳しくは、[ユニバーサルエディターの拡張](/help/implementing/universal-editor/extending.md)ドキュメントを参照してください。

## ユニバーサルエディターとコンテンツフラグメントエディター {#universal-editor-content-fragment-editor}

一見すると、ユニバーサルエディターとコンテンツフラグメントエディターは、同様の編集機能が用意されているように思えるかもしれません。しかし、これらのエディターは極めて異なる機能を提供し、それぞれマーケティング実施者の異なる仕事を達成するのに使用されます。

### コンテンツフラグメントエディター {#content-fragment-editor}

マーケティング実施者は、レイアウトを気にすることなくコンテンツを作成したいので、コンテンツはエクスペリエンスの多くのコンテキストで再利用できます。

* 基本的な作業は、コンテンツ戦略を拡大することです。

### ユニバーサルエディター {#universal-editor}

マーケティング実施者は、特定のコンテキストのレイアウトに合わせたコンテンツを作成して、優れたエクスペリエンスを提供したいと考えています。

* 達成すべき基本的な仕事は、説得力を持って読者とつながることです。

## 制限事項 {#limitations}

ユニバーサルエディターを探索し、独自のプロジェクトへの実装を進める際には、次の制限事項に留意してください。

* 単一ページの実装として参照できる AEM リソース（コンテンツフラグメント、ページ、エクスペリエンスフラグメント、アセットなど）は 25 個以下にする必要があります。
* AEM as a Cloud Service、[AEM 6.5 LTS](https://experienceleague.adobe.com/ja/docs/experience-manager-65-lts/content/implementing/developing/headless/universal-editor/introduction) および [AEM 6.5](https://experienceleague.adobe.com/ja/docs/experience-manager-65/content/implementing/developing/headless/universal-editor/introduction) が、サポートされているAEM バックエンドです。
* AEM as a Cloud Service にはリリース `2023.8.13099` 以降が必要です。
* コンテンツ作成者は、独自の Experience Cloud アカウントを持つ必要があります。
* AEM の一部として、ユニバーサルエディターは [AEM と同じデスクトップブラウザーをサポート](/help/overview/supported-platforms.md)します。
   * これらのブラウザーのモバイルバージョンはサポートされていません。

{{ip-allow-lists-ue}}

## 次の手順 {#next-steps}

ユニバーサルエディターの一般的なユースケースの詳細と、プロジェクトをサポートする適切なドキュメントリソースを見つけるには、[ユニバーサルエディターのユースケースと学習パス](/help/implementing/universal-editor/use-cases.md)のドキュメントを参照してください。
