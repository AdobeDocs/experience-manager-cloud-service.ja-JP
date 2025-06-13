---
title: ページエディターとユニバーサルエディター
description: ページエディターは引き続きAdobeでサポートされますが、ユニバーサルエディターは新しいプロジェクトに魅力的な可能性をもたらします。
feature: Developing
role: Admin, Architect, Developer
exl-id: 0a13fb52-623e-4aff-b254-186d8d117e4d
source-git-commit: 9da4c90c56b7a82a41604173100ad6503a4a06d0
workflow-type: tm+mt
source-wordcount: '1069'
ht-degree: 16%

---

# ページエディターとユニバーサルエディター {#page-editor-universal-editor}

ページエディターは引き続きAdobeでサポートされますが、ユニバーサルエディターは新しいプロジェクトに魅力的な可能性をもたらします。

## 背景 {#background}

Adobeは、最新の JavaScript ベースの開発アプローチを取り入れた合理化されたエディターとして、2024 年に [ ユニバーサルエディター ](/help/implementing/universal-editor/introduction.md) を導入しました。 ユニバーサルエディターは、シームレスで拡張性の高いビジュアルコンテンツオーサリングエクスペリエンスを実現するためのAdobeのビジョンです。

AEMの長い歴史の中で [ ページエディター ](/help/sites-cloud/authoring/page-editor/introduction.md) の豊富な機能セットと無数のプロジェクトに投資してきたことを認識し、Adobeはページエディターを引き続き完全にサポートしていますが、技術革新はユニバーサルエディターに焦点を当てます。

## レコメンデーション {#recommendation}

すぐに絞り込まれますが、ユニバーサルエディターとページエディターの間には機能のギャップが残ります（[ 機能の比較については、次の節で確認できます ](#feature-comparison)）。

経験則として、次の操作を行います。

* **新規プロジェクト** は、デフォルトでユニバーサルエディターを活用する必要があります。
* **既存のプロジェクト** は、Edge Deliveryまたはヘッドレスの取り組みを開始する際に、引き続きページエディターを使用し、ユニバーサルエディターを検討する必要があります。

**選択するエディターは、個々のプロジェクトのニーズに完全に応じて決定する必要があります**。

## 機能の比較 {#feature-comparison}

2 つのエディターの機能のギャップは絶えず縮小しているため、最新の開発については、必ず [ ユニバーサルエディターのリリースノート ](/help/release-notes/universal-editor/current.md) を参照してください。

### 配信 {#delivery}

|  | ページエディター | メモ | ユニバーサルエディター | メモ |
|---|---|---|---|---|
| [ 配信を公開 ](/help/sites-cloud/authoring/author-publish.md) | [!BADGE  使用可能 ]{type=Positive} | コアコンポーネントおよび従来のAEM プロジェクトでの使用に推奨 | [!BADGE  利用不可 ]{type=Negative} | 従来のAEM ページは、通常、ユニバーサルエディターでそのままレプリケートするのが難しい、いくつかのページエディター固有の機能に依存します。 |
| [Edge Delivery](/help/edge/overview.md) | [!BADGE  利用不可 ]{type=Negative} |  | [!BADGE  使用可能 ]{type=Positive} |  |
| [ ヘッドレス配信 ](/help/headless/introduction.md) | [!BADGE  一部利用可能 ]{type=Caution} | ユニバーサルエディターに置き換えて [ 非推奨 ](/help/implementing/developing/hybrid/spa-editor-deprecation.md) となった [SPA エディター ](/help/implementing/developing/hybrid/introduction.md) でのみ | [!BADGE  使用可能 ]{type=Positive} | ユニバーサルエディターを使用すると、開発者は、特定のフレームワーク要件や実装制約を課すことなく、独自の web アプリを持ち込むことができます。 |

### 永続性 {#persistence}

|  | ページエディター | メモ | ユニバーサルエディター | メモ |
|---|---|---|---|---|
| ページコンポーネントの編集 | [!BADGE  使用可能 ]{type=Positive} |  | [!BADGE  使用可能 ]{type=Positive} |  |
| 編集 [ コンテンツフラグメント ](/help/assets/content-fragments/content-fragments.md) | [!BADGE  利用不可 ]{type=Negative} |  | [!BADGE  使用可能 ]{type=Positive} | 新しいフラグメントの挿入やフラグメントの並べ替えを含める |

### 機能 {#capabilities}

|  | ページエディター | メモ | ユニバーサルエディター | メモ |
|---|---|---|---|---|
| ページテンプレート | [!BADGE  使用可能 ]{type=Positive} |  | [!BADGE  使用可能 ]{type=Positive} | ユニバーサルエディターは、使用されるテンプレートシステムに依存しません。 ただし、最新のフロントエンドツールでは、開発者がコード内で直接テンプレートロジックを定義および管理しやすくなっているので、通常の実装パターンでは開発者が定義したテンプレートが優先されます。 |
| WYSIWYGの編集 | [!BADGE  使用可能 ]{type=Positive} | ページに制限 | [!BADGE  使用可能 ]{type=Positive} | ページとコンテンツフラグメントのサポート |
| [バリエーションを生成](/help/generative-ai/generate-variations.md) | [!BADGE  利用不可 ]{type=Negative} |  | [!BADGE  使用可能 ]{type=Positive} | [ 拡張機能として使用できます ](/help/implementing/universal-editor/extending.md) |
| 新しいブロックを挿入 | [!BADGE  使用可能 ]{type=Positive} |  | [!BADGE  使用可能 ]{type=Positive} |  |
| ブロックを並べ替え | [!BADGE  使用可能 ]{type=Positive} | コンテキスト内ドラッグ&amp;ドロップでは可能ですが、「ツリー表示」サイドパネルでは不可能です | [!BADGE  使用可能 ]{type=Positive} | 「ツリー表示」サイドパネルでドラッグ&amp;ドロップすることで可能ですが、まだコンテキスト内（予定）ではありません |
| ブロックの切り取り/コピー/貼り付け | [!BADGE  使用可能 ]{type=Positive} |  | [!BADGE  利用不可 ]{type=Negative} | 計画済み |
| スタイルの適用 | [!BADGE  使用可能 ]{type=Positive} | スタイルは、[ スタイルシステム ](/help/sites-cloud/authoring/page-editor/style-system.md) を使用してコンポーネントに適用できます。 | [!BADGE  使用可能 ]{type=Positive} | スタイルは、通常のコンポーネント（またはコンテンツフラグメント）プロパティを使用して適用できます。 ユニバーサルエディターでは同じスタイルピッカーは使用できませんが、複数選択ウィジェットを使用すると、非常に類似した UX を実現できます。 |
| レイアウトの適用 | [!BADGE  使用可能 ]{type=Positive} | サイトでは、[AEM レスポンシブグリッド ](/help/implementing/developing/introduction/responsive-design.md) を実装して、作成者が 3 つの事前定義済みブレークポイントにわたってコンポーネントのサイズを変更できるようにする必要があります。 | [!BADGE  使用可能 ]{type=Positive} | レイアウトは通常のコンポーネント（またはコンテンツフラグメント）プロパティを使用して適用できますが、レスポンシブグリッドはサポートされていません。 |
| 取り消し/やり直し | [!BADGE  使用可能 ]{type=Positive} |  | [!BADGE  利用不可 ]{type=Negative} | 計画済み |
| 公開（プレビューにも対応） | [!BADGE  使用可能 ]{type=Positive} |  | [!BADGE  使用可能 ]{type=Positive} |  |
| [ワークフローを開始](/help/sites-cloud/authoring/workflows/overview.md) | [!BADGE  使用可能 ]{type=Positive} |  | [!BADGE  使用可能 ]{type=Positive} | 拡張機能として使用できます |
| コメント中 | [!BADGE  使用可能 ]{type=Positive} | [ 注釈 ](/help/sites-cloud/authoring/page-editor/annotations.md) の使用 | [!BADGE  利用不可 ]{type=Negative} | 計画済み |
| Workfront の統合 | [!BADGE  利用不可 ]{type=Negative} |  | [!BADGE  使用可能 ]{type=Positive} | 拡張機能として使用できます |
| [MSM とローンチ ](/help/sites-cloud/administering/msm-and-translation.md) | [!BADGE  使用可能 ]{type=Positive} |  | [!BADGE  使用可能 ]{type=Positive} | ページに拡張機能として使用できます |
| 実験とパーソナライゼーション | [!BADGE  使用可能 ]{type=Positive} | [ ターゲットモード ](/help/sites-cloud/authoring/personalization/targeted-content.md) の使用 | [!BADGE  使用可能 ]{type=Positive} | Edge Delivery Servicesの拡張機能として使用できます |
| コンテンツツリー | [!BADGE  使用可能 ]{type=Positive} |  | [!BADGE  使用可能 ]{type=Positive} | ツリー内で並べ替えることもできます |
| 医療機器シミュレーション | [!BADGE  使用可能 ]{type=Positive} | [ 設定されたデバイスをシミュレートできます ](/help/sites-cloud/administering/responsive-layout.md) が、ユーザーがシミュレートするために別の画面サイズを手動で入力することはできません。 | [!BADGE  使用可能 ]{type=Positive} | [ シミュレーションする画面のサイズは手動で入力できますが ](/help/sites-cloud/authoring/universal-editor/navigation.md#emulator) デフォルトのブレークポイントは設定できません。 |
| [ ページロック ](/help/sites-cloud/authoring/sites-console/managing-pages.md) | [!BADGE  使用可能 ]{type=Positive} |  | [!BADGE  使用可能 ]{type=Positive} | エディターでページのロック/ロック解除に使用できる拡張機能を使用して、サイトコンソールのロックステータス設定を尊重します |
| [ ページプロパティ ](/help/sites-cloud/authoring/sites-console/page-properties.md) | [!BADGE  使用可能 ]{type=Positive} |  | [!BADGE  使用可能 ]{type=Positive} | サイト管理から使用でき、エディターからページのプロパティにアクセスすることもできます。 |
| 複数フィールドのプロパティ | [!BADGE  使用可能 ]{type=Positive} |  | [!BADGE  利用不可 ]{type=Negative} | 計画済み |
| [ リモート DAM](/help/assets/dynamic-media-open-apis-overview.md) | [!BADGE  使用可能 ]{type=Positive} |  | [!BADGE  使用可能 ]{type=Positive} |  |
| [ ページバージョン管理 ](/help/sites-cloud/authoring/sites-console/page-versions.md) | [!BADGE  使用可能 ]{type=Positive} |  | [!BADGE  使用可能 ]{type=Positive} |  |
| [TimeWarp](/help/sites-cloud/authoring/sites-console/page-versions.md#timewarp) と [ 差分表示 ](/help/sites-cloud/authoring/sites-console/page-diff.md) | [!BADGE  使用可能 ]{type=Positive} |  | [!BADGE  利用不可 ]{type=Negative} | 計画済み |
| 管理画面で表示 | [!BADGE  使用可能 ]{type=Positive} |  | [!BADGE  使用可能 ]{type=Positive} | ページの拡張機能として使用できます |
| ページステータスの表示 | [!BADGE  使用可能 ]{type=Positive} |  | [!BADGE  利用不可 ]{type=Negative} | サイトコンソールで使用可能 |
| 拡張機能 | [!BADGE  使用可能 ]{type=Positive} | AEMのオーバーレイとして | [!BADGE  使用可能 ]{type=Positive} | App Builderを使用し、AEM固有の知識をほとんど使用せずに、明確に定義された拡張ポイント |

## ユニバーサルエディターの採用 {#adopt-ue}

ユニバーサルエディターには多くの利点があり、新規プロジェクトに最適なソリューションです。

* **ビジュアル編集：** ページエディターと同様に、作成者はプレビュー内でコンテンツを直接編集でき、変更が訪問者エクスペリエンスにどのように影響するかを即座に確認できます。
* **今後の校正：** AEM のロードマップでは、ビジュアルエディターとしてユニバーサルエディターが優先されています。これを採用することで、最新のイノベーションと機能強化にアクセスできます。
* **よりシンプルな統合：**&#x200B;ユニバーサルエディターを使用するのに AEM 固有の SDK は必要ないので、テクニカルスタックのロックインが軽減されます。
* **独自のアプリを導入：**&#x200B;ユニバーサルエディターは任意の web フレームワークやアーキテクチャをサポートしているので、複雑なリファクタリングを必要とせずに導入できます。
* **拡張性：**&#x200B;ユニバーサルエディターは、生成 AI、Workfront などとの統合を含む強力な[拡張フレームワーク](/help/implementing/universal-editor/extending.md)のメリットを受けます。

### ユニバーサルエディターへの移行 {#migrate-ue}

ページエディターからユニバーサルエディターに直接移行するパスはありません。 これは、2 つのテクノロジーの基本的な違いによるものです。

* ユニバーサルエディターでは、テンプレートエディター、スタイルシステム、レスポンシブグリッドなどの機能は再導入されません。
   * Edge Delivery Servicesまたはヘッドレスプロジェクトのリーンフロントエンド CSS と Javascript を使用して、これらのユースケースをより効率的に処理できるようになりました。
* ユニバーサルエディターはサービスとしてのエディターなので、実装者がコンポーネントダイアログに CSS または JS を挿入することはできません。
   * これにより、ページエディターからのコンポーネントダイアログの自動変換を防ぐことができます。
   * これは、カスタムウィジェット、フィールド検証、表示／非表示ルール、テンプレートベースのカスタマイズなど、ダイアログの多くの領域に影響を与えます。
      * そのような機能は引き続き利用可能ですが、ユニバーサルエディターは、ダイアログにデプロイされたカスタム JavaScriptの代わりに、設定を通じて機能を解決します。

ユニバーサルエディターは技術的に従来のAEM プロジェクト（コアコンポーネントを使用して構築など）のページ編集を有効にすることができますが、これらのサイトは通常、スタイルシステム、レスポンシブグリッド、編集可能テンプレート、ダイアログ内のカスタム Javascript など、いくつかのページエディター固有の機能に依存します。

ユニバーサルエディターは、これらの従来の機能をサポートしない、より合理化された最新のアプローチに従うので、そのようなサイトを移行するには、大幅なリファクタリングが必要になります。 このため、**ページエディターサイトのユニバーサルエディターへの移行は、Edge Delivery Servicesに移行するプロジェクトでのみ推奨されます**。
