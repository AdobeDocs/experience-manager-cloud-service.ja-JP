---
title: AEM AS A CLOUD SERVICEへのAIを活用したコードの移行
description: AEM Cloud Migration SkillとMCPの概要。BPAの調査結果を読み取り、AEM 6.x コードをAEM as a Cloud Serviceに移行するAI エージェントソリューションで、パターン別に表示されます。
feature: Migration
role: Developer
source-git-commit: 087017a7c0528f0806dfa8e8bd18a057a1763b14
workflow-type: tm+mt
source-wordcount: '756'
ht-degree: 1%

---


# AEM AS A CLOUD SERVICEへのAIを活用したコードの移行 {#cloud-migration-skill-overview}

**AEM Cloud Migration** ソリューションは、AEM 6.x、AMS、またはオンプレミス Java コードとOSGi設定を&#x200B;**AEM as a Cloud Service （AEMaaCS）**&#x200B;に移行する際に開発者をガイドするエージェントベースのツールセットです。 エージェントスキルとモデルコンテキストプロトコル（MCP）をサポートするAI対応IDE内で動作します。

次のデモビデオでは、AEM Cloud Migration ソリューションの簡単なエンドツーエンドのチュートリアルを紹介します。参照用に含まれています。

>[!VIDEO](https://video.tv.adobe.com/v/3491439?captions=jpn&learn=on)

このソリューションは、次の2つのコンポーネントで構成されています。

| コンポーネント | 役割 |
|-----------|------|
| **移行スキル** | 移行ワークフローのオーケストレーション、ベストプラクティスアナライザー（BPA）の調査結果の取得、プロジェクト内の影響を受けるファイルの特定、パターン別のコード変換パターンの適用を行います。 ローカル BPA CSV エクスポートまたはCloud Migration MCPで動作します（推奨）。 |
| **クラウド移行MCP** | IDE エージェントをCloud Acceleration Manager（CAM）に接続し、CSV エクスポートを行わずにBPA結果を直接取得できるようにします。 最新の結果を得るには、ローカル CSVよりも推奨されます。 |

## 前提条件 {#prerequisites}

- IDEでAEM プロジェクト（MavenまたはGradle）を開く
- 次のBPA検索ソースの1つ（強くお勧めします。手動フローには必要ありません）。
   - AEM インスタンスからの&#x200B;**BPA CSV エクスポート**
   - BPA レポートがアップロードされ、Cloud Migration MCPが設定された&#x200B;**Cloud Acceleration Manager プロジェクト**

## 移行スキル {#migration-skill}

移行スキルは、AI対応IDEのエージェントスキルです。 このワークフローは、**one-pattern-per-session** ワークフローを編成します。修正するパターンに名前を付け、BPAの調査結果にエージェントを指定すると、エージェントは関連する変換ルールを読み取り、プロジェクト内の影響を受けるファイルを見つけ、変更を5つのバッチに適用し、各バッチの後にレビューを一時停止します。

### サポートされるパターン {#supported-patterns}

| パターン | 修正点 |
|---------|--------------|
| `scheduler` | `sling.commons.scheduler` ベースのジョブは、AEMaaCSのステートレスランタイムと互換性がありません |
| `resourceChangeListener` | Cloud Serviceの更新が必要な`ResourceChangeListener`実装 |
| `replication` | 従来の`Replicator` API呼び出しは`ContentDistribution`個の同等のものに置き換えられました |
| `eventListener` | OSGi `EventListener`実装がAEMaaCS イベントセマンティクス用に更新されました |
| `eventHandler` | Cloud Service用に適応された同期OSGi `EventHandler` サービス |
| `assetApi` | 非推奨の`AssetManager`およびDAM API呼び出しは、サポートされている同等のものに置き換えられました |
| `htlLint` | HTL テンプレートの`data-sly-test`個の冗長な定数比較警告 |
| OSGi設定 | `.cfg.json`変換、実行モード スコープ、Cloud Manager シークレット/env-var抽出 |

このスキルは、すべてのコード変換ステップをコンパニオン `code-assessment` スキルに委任します。 両方は`aem-cloud-service` スキルパッケージとして一緒に配布されます。両方を取得するには、パッケージを1回インストールしてください。

### はじめに {#getting-started-skill}

1. [Adobe スキルリポジトリ &#x200B;](https://github.com/adobe/skills)から`aem-cloud-service` スキルパッケージをインストールします。
2. AEM プロジェクトをIDEのワークスペースルートとして開きます。
3. BPA調査結果の取得：BPAからCSVをエクスポートするか、クラウド移行MCPを設定します（以下を参照）。
4. 次のいずれかのプロンプトを使用して、エージェントとのセッションを開始します。

   **BPA CSV:**

   ```
   Use the migration skill: scheduler only, BPA CSV at ./reports/bpa.csv
   ```

   MCP:**経由の** CAM

   ```
   Fix replictaion findings from project <projectname>/<projectId>.
   ```

   **手動（BPAなし）:**

   ```
   Migrate event listener in core/src/main/java/com/example/Listener.java
   ```

   **OSGi設定：**

   ```
   Scan my config files and create Cloud Manager environment secrets or variables.
   ```

   **HTL lint:**

   ```
   Fix htlLint in ui.apps - scan for data-sly-test redundant constant warnings.
   ```

>[!NOTE]
>スキルは、セッションごとに1つのパターンを処理します。 BPA レポートに複数のパターンが含まれる場合、開始する前に1つを選択するように求められます。

完全なパターン参照とセッション管理ガイダンスについては、[&#x200B; クラウド移行スキルの使用](/help/journey-migration/cloud-migration-skill/using-cloud-migration-skill.md)を参照してください。

## クラウド移行MCP {#cloud-migration-mcp}

**AEM Cloud Migration MCP**&#x200B;は、IDE エージェントをCloud Acceleration Managerに接続する[Model Context Protocol](https://modelcontextprotocol.io) サーバーです。 移行スキルを設定すると、CSV ダウンロードを必要とせずに、CAM プロジェクトからBPA結果を直接取得できます。

### MCPの機能 {#mcp-tools}

| ツール | 説明 |
|------|-------------|
| `fetch-cam-bpa-findings-by-pattern` | CAM プロジェクトの最新のBPA レポートから、特定のコード移行パターンのBPA結果を返します。 |
| `fetch-cam-bpa-findings-by-importance` | 指定された重要度（`CRITICAL`、`MAJOR`、`ADVISORY`、`INFO`）のすべてのBPA結果をカウント別に並べ替えて返します。 最初に取り組むパターンを優先するのに便利です。 |

これらのツールは、移行スキルによって自動的に呼び出されます。直接呼び出すことはありません。

### はじめに {#getting-started-mcp}

1. IDEのMCP設定で、クラウド移行MCP サーバーのURL `https://mcp.adobeaemcloud.com/adobe/mcp/cloud-migration`を追加します
2. プロンプトが表示されたら、Adobe IDでログインしてCloud Acceleration Managerに対する認証を行います。
3. 移行スキルは、CAM プロジェクトからBPAの調査結果を直接取得できるようになりました。

セットアップとトラブルシューティングの詳細については、[&#x200B; クラウド移行MCPの使用](/help/journey-migration/cloud-migration-skill/using-cloud-migration-mcp.md)を参照してください。

## どのように移行ジャーニーに組み込むのかを解説します {#migration-journey}

スキルとMCPは、**実装フェーズ**&#x200B;の他のツールを補完します。

- **ベストプラクティスアナライザー**: スキルを促進する調査結果を生成します。 [&#x200B; ベストプラクティスアナライザーの使用](/help/journey-migration/best-practices-analyzer/using-best-practices-analyzer.md)を参照してください。
- **Cloud Acceleration Manager**: BPA レポートをホストし、移行の全体的な進行状況を追跡します。 [CAMの使用を開始するを参照してください](/help/journey-migration/cloud-acceleration-manager/using-cam/getting-started-cam.md)。
- **リファクタリング ツール**: リポジトリ構造とDispatcher設定の近代化を処理します。 [&#x200B; リファクタリング ツールの概要](/help/journey-migration/refactoring-tools/overview-refactoring-tools.md)を参照してください。
- **コンテンツ転送ツール**：リポジトリコンテンツをAEM 6.xからAEMaaCSに移行します。

全体像については、[実装フェーズの概要](/help/journey-migration/implementation.md)を参照してください。

