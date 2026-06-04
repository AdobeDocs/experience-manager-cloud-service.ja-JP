---
title: サイトカタログスキル
description: Experience Modernization Agentのサイトカタログスキルを使用して、既存のweb サイトを自動分析し、Edge Delivery Services移行計画をサポートする方法について説明します。
feature: Edge Delivery Services, Agentic AI
role: User, Admin, Developer
source-git-commit: 30037f08d5caeab878b6cf89b936308d16ae3e8d
workflow-type: tm+mt
source-wordcount: '776'
ht-degree: 1%

---


# サイトカタログスキル {#site-catalog-skill}

Experience Modernization Agentのサイトカタログスキルを使用して、既存のweb サイトを自動分析し、Edge Delivery Services移行計画をサポートする方法について説明します。

## 概要 {#overview}

サイトカタログスキルは、サイト上のあらゆるページを検出し、使用中のページテンプレートとブロックバリエーションを特定し、それぞれのスクリーンショットをキャプチャし、コンソールの「プレビュー」タブで参照するか、ローカルでダウンロードして開くことができるインタラクティブなHTML レポートバンドルを生成します。

このスキルは、次の方法で既存のプロジェクトをEdge Delivery Servicesに移行する際に役立ちます。

* **移行プロジェクトの開始** – 作業が始まる前にスキルを実行すると、ページ数、テンプレート、ブロックバリエーション、ロケールなど、サイトの規模が理解されます。 下流のあらゆる決定が依存する際に、ベースラインインベントリが確立される。
* **労力の見積もりと計画** – 提案、スプリント計画、リソースをサポートするための定量化指標を取得します。
* **一括読み込みの準備** — `template-catalog.json`を使用して、同じレイアウトを共有するページを特定し、テンプレートごとの一括読み込みを計画します。
* **関係者向けレポート** — プロジェクト管理者、アーキテクト、ビジネス関係者とインタラクティブなHTML レポートバンドルを共有します。

## 起動する {#invoking}

[Experience Modernization Consoleで、](/help/ai-in-aem/agents/brand-experience/modernization/console.md)は自然言語を使用して、エージェントにサイトのカタログ化を依頼します。 次に、プロンプトの例を示します。

* `scope site https://www.example.com`
* `site scope https://www.example.com`
* `analyze https://www.example.com`
* `find templates on https://www.example.com`
* `discover templates on https://www.example.com`
* `catalog site https://www.example.com`
* `how many page types are there on https://www.example.com`
* `what are the layouts on https://www.example.com`
* `analyze site structure of https://www.example.com`

スキルのワークフローには、次の4つのフェーズが順番に実行されます。

1. 分析
1. テンプレート
1. チューニング
1. カタログ化をブロック

任意のフェーズを再生すると、エージェントはそのフェーズの出力とすべてのダウンストリームの出力をクリアし、その時点から再開します。 フェーズを再生するプロンプトの例を次に示します。

* `Repeat analyzing` / `Redo page analysis` / `Rerun analyze pages`
* `Repeat templating` / `Redo the template discovery step` / `Restart the templating step`
* `Repeat tuning` / `Rerun tune templates` / `Redo template tuning`
* `Repeat block cataloging` / `Restart catalog block variants`

フェーズを再生する場合、前のフェーズは保持されます。

## 出力 {#output}

スキルがサイトのカタログ化を完了すると、3種類の出力が表示されます。

1. **合計（ページ、テンプレート、EDS マップされたブロック バリエーションとカスタム分類の比較）、ロケールの内訳、カバレッジ率、全体的なレポートステータス（完全/不完全/失敗）を含む、チャット**&#x200B;の完了概要
1. **メインの成果物として** インタラクティブ HTML レポート バンドルを`catalog/template-catalog-report-bundle.zip`に保存しました
   * このバンドルには、`template-catalog-report.html`に加えて、参照されているすべてのスクリーンショットとアセットが含まれています。
   * バンドルをダウンロードしてローカルに表示するか、共有できます。
   * または、エージェントに`Move template-catalog-report-bundle.zip to the /content folder to render it in the preview tab. Update all references as needed.`にコンソールでレポートを表示するように依頼できます。
1. `summary.json`、`template-catalog.json`、`block-catalog.json`、`urls-all.json`、`urls-grouped.json`、`urls-checklist.json`、`.pages/`、`.blocks/`を含む、下流のスキルおよびプログラムでの使用に対する`catalog/`の&#x200B;**構造化JSON アーティファクト**

### カタログフォルダーの内容 {#contents}

構造化されたJSON アーティファクトは、スキルによって`catalog/`に保存されます。

| ファイル | 説明 |
|---|---|
| `template-catalog-report-bundle.zip` | インタラクティブ HTML レポートバンドル（プライマリ成果物） |
| `summary.json` | ロールアップ指標と[ レポートの状態](#status) |
| `template-catalog.json` | それぞれに使用するURLを持つすべての固有テンプレート（一括読み込みに使用） |
| `block-catalog.json` | メタデータとスクリーンショット参照を含むあらゆるブロックバリエーション |
| `urls-all.json` | 検出されたすべてのURL |
| `urls-grouped.json` | パターンとロケールでグループ化されたURL |
| `urls-sample.json` | 分析用にサンプリングされた代表的なURL |
| `urls-checklist.json` | URLごとの分析ステータス |
| `catalog.log` | 実行ログ |
| `.pages/<page-slug>/page-catalog.json` | ページレベルの分析出力 |
| `.pages/<page-slug>/full-page.jpg` | ページ全体のスクリーンショット |
| `.pages/<page-slug>/blocks/<block-name>.jpg` | ブロックごとのスクリーンショット |
| `.pages/_global/header.json + header.jpg` | グローバルヘッダー分析とスクリーンショット |
| `.pages/_global/footer.json + footer.jpg` | グローバルフッター分析とスクリーンショット |
| `.blocks/<variantId>/metadata.json` | バリアントメタデータをブロック |
| `.blocks/<variantId>/screenshots/<name>.jpg` | バリアントスクリーンショットをブロック |

### レポートのステータス {#status}

[`summary.json`](#contents)の`status` フィールドには、次の値を指定できます。

| ステータス | 意味 |
|---|---|
| `complete` | すべてのページが正常に分析されました（または10%以下の失敗率がありました）。 |
| `incomplete` | 10%以上のページでエラーが発生するか、50%以上のページでブロック検出がクラッシュしました。 出力は引き続き使用できますが、部分的です。 |
| `failed` | ページの分析に成功しました。 |

## 大規模サイト向けのサンプリング {#sampling}

デフォルトでは、スキルはディープページ分析を1000 URLに制限します。 最大1000個のURLを含むサイトの場合、すべてのページが分析されます。

URLが1000を超えるサイトの場合、エージェントは一時停止し、次の手順を実行する方法を尋ねます。

* サンプリングキャップを増やします（最大4000 URL）
* 特定のグループのみを分析（例：`/products/*`または`/blog/*`のみ）
* すべてのURLを分析し、サンプリングなしでサイト全体を実行します

URLの検出は、サンプルの制限に関係なく、常にサイト全体をカバーします。 ディープのページごとの分析フェーズのみが制限されます。

すべてのページを上書きして分析するには、担当者に次の情報を伝えます。

* `analyze all URLs`
* `analyze everything`
* `analyze every page`
* `run the full site`

## 一括読み込みワークフロー {#bulk-import}

サイト カタログ スキルは、サイト全体を移行する際に推奨されるアプローチの一部です。

1. サイトカタログスキルを実行して、完全なテンプレートカタログとブロックカタログを取得します。
1. [HTML レポートバンドル ](#output)を開いて、エージェントが識別したテンプレートを視覚的に確認します。
1. 各テンプレートについて、（[`template-catalog.json`](#output)に記載されている）代表ページを手動で読み込み、出力が正しいまで読み込みを調整します。
1. `template-catalog.json`のURL リストを使用して、そのテンプレートの残りのページを一括インポートします。
1. サイト全体が移行されるまで、各テンプレートに対してこれを繰り返します。

## 制限事項 {#limitations}

サイトカタログのスキルには、次の制限があります。

* **公開サイトのみ** — ターゲットは公開されている必要があります（認証、VPN、またはファイアウォールは使用できません）。
* **動的コンテンツはサポートされていません** — ユーザーによる操作を必要とするコンテンツがDOMに表示されない可能性があります。
* **デフォルトの1000 URL制限** - ディープ分析フェーズは、デフォルトで1000 URLに制限されており、最大4000 URLまで](#sampling)上書きできる[URLに制限されています。

