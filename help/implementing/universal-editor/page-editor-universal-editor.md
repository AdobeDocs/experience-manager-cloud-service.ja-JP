---
title: ページエディターとユニバーサルエディター
description: ページエディターは引き続きアドビでサポートされますが、ユニバーサルエディターにより、新しいプロジェクトに魅力的な可能性がもたらされます。
feature: Developing
role: Admin, Developer
exl-id: 0a13fb52-623e-4aff-b254-186d8d117e4d
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '1067'
ht-degree: 100%

---

# ページエディターとユニバーサルエディター {#page-editor-universal-editor}

ページエディターは引き続きアドビでサポートされますが、ユニバーサルエディターにより、新しいプロジェクトに魅力的な可能性がもたらされます。

## 背景 {#background}

アドビは、最新の JavaScript ベースの開発アプローチを採用した効率化されたエディターとして、2024年に[ユニバーサルエディター](/help/implementing/universal-editor/introduction.md)を導入しました。ユニバーサルエディターは、シームレスで拡張性の高いビジュアルコンテンツオーサリングエクスペリエンスを実現するアドビのビジョンです。

アドビは、AEM の長い歴史を通じて[ページエディター](/help/sites-cloud/authoring/page-editor/introduction.md)のリッチな機能セットとこれに投資してきた無数のプロジェクトを認識し、引き続きページエディターを完全にサポートしますが、イノベーションはユニバーサルエディターに焦点を当てます。

## レコメンデーション {#recommendation}

ユニバーサルエディターとページエディターの間には、急速に縮小してはいますが、依然として機能の格差が存在します（[機能の比較について詳しくは、次の節を参照してください](#feature-comparison)）。

経験則として：

* **新規プロジェクト**&#x200B;では、デフォルトでユニバーサルエディターを活用することをお勧めします。
* **既存のプロジェクト**&#x200B;では、引き続きページエディターを使用し、Edge Delivery やヘッドレス開発を開始する際にはユニバーサルエディターの使用を検討してください。

**選択するエディターは、個々のプロジェクトのニーズに応じて決定する必要があります。**

## 機能の比較 {#feature-comparison}

2 つのエディター間の機能のギャップは常に縮まっているので、最新の開発状況について詳しくは、[ユニバーサルエディターのリリースノート](/help/release-notes/universal-editor/current.md)を必ず参照してください。

### 配信 {#delivery}

|  | ページエディター | メモ | ユニバーサルエディター | メモ |
|---|---|---|---|---|
| [公開配信](/help/sites-cloud/authoring/author-publish.md) | [!BADGE 使用可能]{type=Positive} | コアコンポーネントおよび従来の AEM プロジェクトで使用することをお勧めします。 | [!BADGE 使用不可]{type=Negative} | 従来の AEM ページは通常、ページエディター固有のいくつかの機能に依存し、ユニバーサルエディターではそのままレプリケートすることが困難です。 |
| [Edge Delivery](/help/edge/overview.md) | [!BADGE 使用不可]{type=Negative} |  | [!BADGE 使用可能]{type=Positive} |  |
| [ヘッドレス配信](/help/headless/introduction.md) | [!BADGE 部分的に使用可]{type=Caution} | [SPA エディター](/help/implementing/developing/hybrid/introduction.md)は[非推奨（廃止予定）](/help/implementing/developing/hybrid/spa-editor-deprecation.md)となり、ユニバーサルエディターが導入されました。 | [!BADGE 使用可能]{type=Positive} | ユニバーサルエディターを使用すると、開発者は特定のフレームワーク要件や実装の制約を課すことなく、独自の web アプリを導入できます。 |

### 永続性 {#persistence}

|  | ページエディター | メモ | ユニバーサルエディター | メモ |
|---|---|---|---|---|
| ページコンポーネントの編集 | [!BADGE 使用可能]{type=Positive} |  | [!BADGE 使用可能]{type=Positive} |  |
| [コンテンツフラグメント](/help/assets/content-fragments/content-fragments.md)の編集 | [!BADGE 使用不可]{type=Negative} |  | [!BADGE 使用可能]{type=Positive} | 新しいフラグメントの挿入や並べ替えを含めます。 |

### 機能 {#capabilities}

|  | ページエディター | メモ | ユニバーサルエディター | メモ |
|---|---|---|---|---|
| ページテンプレート | [!BADGE 使用可能]{type=Positive} |  | [!BADGE 使用可能]{type=Positive} | ユニバーサルエディターは、使用されるテンプレートシステムに依存しません。ただし、一般的な実装パターンでは、開発者が定義したテンプレートが優先されます。これは、最新のフロントエンドツールによって、開発者がコード内でテンプレートロジックを直接定義し、維持することがはるかに容易になったからです。 |
| WYSIWYG の編集 | [!BADGE 使用可能]{type=Positive} | ページに制限されます | [!BADGE 使用可能]{type=Positive} | ページとコンテンツフラグメントをサポートします |
| [バリエーションを生成](/help/generative-ai/generate-variations.md) | [!BADGE 使用不可]{type=Negative} |  | [!BADGE 使用可能]{type=Positive} | [拡張機能として使用できます](/help/implementing/universal-editor/extending.md) |
| 新規ブロックを挿入 | [!BADGE 使用可能]{type=Positive} |  | [!BADGE 使用可能]{type=Positive} |  |
| ブロックを並べ替え | [!BADGE 使用可能]{type=Positive} | コンテキスト内のドラッグ＆ドロップでは可能ですが、「ツリービュー」サイドパネルでは不可能です | [!BADGE 使用可能]{type=Positive} | 「ツリービュー」サイドパネルのドラッグ＆ドロップでは可能ですが、コンテキスト内ではまだ不可能です（計画済み） |
| ブロックを切り取り／コピー＆ペースト | [!BADGE 使用可能]{type=Positive} |  | [!BADGE 使用可能]{type=Positive} |  |
| スタイルを適用 | [!BADGE 使用可能]{type=Positive} | スタイルは、[スタイルシステム](/help/sites-cloud/authoring/page-editor/style-system.md)を使用して、コンポーネントに適用できます。 | [!BADGE 使用可能]{type=Positive} | スタイルは、通常のコンポーネント（またはコンテンツフラグメント）のプロパティを使用して適用できます。 ユニバーサルエディターでは同様のスタイルピッカーは使用できませんが、複数選択ウィジェットを使用すると、非常に類似した UX を実現できます。 |
| レイアウトを適用 | [!BADGE 使用可能]{type=Positive} | 作成者が 3 つの定義済みブレークポイントをまたいでコンポーネントのサイズを変更できるようにするには、Sites で [AEM レスポンシブグリッド](/help/implementing/developing/introduction/responsive-design.md)を実装する必要があります。 | [!BADGE 使用可能]{type=Positive} | レイアウトは、通常のコンポーネント（またはコンテンツフラグメント）プロパティを使用して適用できますが、レスポンシブグリッドはサポートされていません。 |
| 取り消し - やり直し | [!BADGE 使用可能]{type=Positive} |  | [!BADGE 使用可能]{type=Positive} |  |
| 公開（プレビューにも） | [!BADGE 使用可能]{type=Positive} |  | [!BADGE 使用可能]{type=Positive} |  |
| [ワークフローを開始](/help/sites-cloud/authoring/workflows/overview.md) | [!BADGE 使用可能]{type=Positive} |  | [!BADGE 使用可能]{type=Positive} | 拡張機能として使用できます |
| コメント | [!BADGE 使用可能]{type=Positive} | [注釈](/help/sites-cloud/authoring/page-editor/annotations.md)の使用 | [!BADGE 使用不可]{type=Negative} | 計画済み |
| Workfront の統合 | [!BADGE 使用不可]{type=Negative} |  | [!BADGE 使用可能]{type=Positive} | 拡張機能として使用できます |
| [MSM とローンチ](/help/sites-cloud/administering/msm-and-translation.md) | [!BADGE 使用可能]{type=Positive} |  | [!BADGE 使用可能]{type=Positive} | ページに拡張機能として使用できます |
| 実験とパーソナライゼーション | [!BADGE 使用可能]{type=Positive} | [ターゲットモード](/help/sites-cloud/authoring/personalization/targeted-content.md)の使用 | [!BADGE 使用可能]{type=Positive} | Edge Delivery Services に拡張機能として使用できます |
| コンテンツツリー | [!BADGE 使用可能]{type=Positive} |  | [!BADGE 使用可能]{type=Positive} | ツリー内で並べ替えることもできます |
| デバイスのシミュレーション | [!BADGE 使用可能]{type=Positive} | [設定されたデバイスはシミュレートできます](/help/sites-cloud/administering/responsive-layout.md)が、ユーザーはシミュレートする異なる画面サイズを手動で入力できません。 | [!BADGE 使用可能]{type=Positive} | [シミュレートする画面サイズは手動で入力できます](/help/sites-cloud/authoring/universal-editor/navigation.md#emulator)が、デフォルトのブレークポイントは設定できません。 |
| [ページのロック](/help/sites-cloud/authoring/sites-console/managing-pages.md) | [!BADGE 使用可能]{type=Positive} |  | [!BADGE 使用可能]{type=Positive} | Sites コンソールで設定されたロックステータスを適用し、エディターからページをロック／ロック解除できる拡張機能が使用できます |
| [ページプロパティ](/help/sites-cloud/authoring/sites-console/edit-page-properties.md) | [!BADGE 使用可能]{type=Positive} |  | [!BADGE 使用可能]{type=Positive} | サイト管理者から使用可能で、エディターからページのプロパティにもアクセスできる拡張機能を備えています |
| 複数フィールドのプロパティ | [!BADGE 使用可能]{type=Positive} |  | [!BADGE 使用不可]{type=Negative} | 計画済み |
| [リモート DAM](/help/assets/dynamic-media-open-apis-overview.md) | [!BADGE 使用可能]{type=Positive} |  | [!BADGE 使用可能]{type=Positive} |  |
| [ページバージョン管理](/help/sites-cloud/authoring/sites-console/page-versions.md) | [!BADGE 使用可能]{type=Positive} |  | [!BADGE 使用可能]{type=Positive} |  |
| [タイムワープ](/help/sites-cloud/authoring/sites-console/page-versions.md#timewarp)と[差分表示](/help/sites-cloud/authoring/sites-console/page-diff.md) | [!BADGE 使用可能]{type=Positive} |  | [!BADGE 使用不可]{type=Negative} | 計画済み |
| 管理画面で表示 | [!BADGE 使用可能]{type=Positive} |  | [!BADGE 使用可能]{type=Positive} | ページに拡張機能として使用できます |
| ページステータスを表示 | [!BADGE 使用可能]{type=Positive} |  | [!BADGE 使用不可]{type=Negative} | Sites コンソールで使用可能 |
| 拡張機能 | [!BADGE 使用可能]{type=Positive} | AEM オーバーレイとして | [!BADGE 使用可能]{type=Positive} | App Builder を使用し、AEM 固有の知識をほとんど必要とせずに、明確に定義された拡張ポイントとして |

## ユニバーサルエディターの導入 {#adopt-ue}

ユニバーサルエディターには多くのメリットがあり、新しいプロジェクトにとって優れたソリューションになります。

* **ビジュアル編集：**&#x200B;ページエディターと同様に、作成者はプレビュー内でコンテンツを直接編集し、訪問者エクスペリエンスに影響する変更を即座に確認できます。
* **今後の校正：** AEM のロードマップでは、ビジュアルエディターとしてユニバーサルエディターが優先されています。これを採用することで、最新のイノベーションと機能強化にアクセスできます。
* **よりシンプルな統合：**&#x200B;ユニバーサルエディターを使用するのに AEM 固有の SDK は必要ないので、テクニカルスタックのロックインが軽減されます。
* **独自のアプリを導入：**&#x200B;ユニバーサルエディターは任意の web フレームワークやアーキテクチャをサポートしているので、複雑なリファクタリングを必要とせずに導入できます。
* **拡張性：**&#x200B;ユニバーサルエディターは、生成 AI、Workfront などとの統合を含む強力な[拡張フレームワーク](/help/implementing/universal-editor/extending.md)のメリットを受けます。

### ユニバーサルエディターへの移行 {#migrate-ue}

ページエディターからユニバーサルエディターへの直接的な移行パスはありません。これは、2 つのテクノロジーの基本的な違いによるものです。

* ユニバーサルエディターでは、テンプレートエディター、スタイルシステム、レスポンシブグリッドなどの機能は再導入されません。
   * これらのユースケースでは、Edge Delivery Services またはヘッドレスプロジェクトの無駄のないフロントエンド CSS と JavaScript を使用して、より効率的に処理できるようになりました。
* ユニバーサルエディターはサービスとしてのエディターなので、実装者がコンポーネントダイアログに CSS または JS を挿入できません。
   * これにより、ページエディターからのコンポーネントダイアログの自動変換を防ぐことができます。
   * これは、カスタムウィジェット、フィールド検証、表示／非表示ルール、テンプレートベースのカスタマイズなど、ダイアログの多くの領域に影響を与えます。
      * このような機能は引き続き使用可能ですが、ユニバーサルエディターでは、ダイアログにデプロイされたカスタム JavaScript の代わりに、設定を通じて解決します。

ユニバーサルエディターでは、従来の AEM プロジェクト（例：コアコンポーネントを使用して作成されたプロジェクト）のページの編集を技術的に有効にすることができますが、これらのサイトは通常、スタイルシステム、レスポンシブグリッド、編集可能なテンプレート、ダイアログ内のカスタム JavaScript など、ページエディター固有のいくつかの機能に依存しています。

ユニバーサルエディターは、これらの従来の機能をサポートしない、より効率化された最新のアプローチを採用しているので、このようなサイトを移行するには大幅なリファクタリングが必要になります。このため、**ページエディターサイトをユニバーサルエディターに移行することは、Edge Delivery Services に移行するプロジェクトにのみ推奨されます。**
