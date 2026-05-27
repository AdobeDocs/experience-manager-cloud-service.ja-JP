---
title: AEM Cloud Migration MCPの使用
description: AEM Cloud Migration MCP サーバーをAI対応IDEに追加し、移行セッション中にCloud Acceleration Managerからベストプラクティスアナライザーの調査結果を取得するために使用する方法について説明します。
feature: Migration
role: Developer
source-git-commit: 5cda629090d9a9d020deca5192b8a89659ec4749
workflow-type: tm+mt
source-wordcount: '488'
ht-degree: 1%

---


# AEM Cloud Migration MCPの使用 {#using-cloud-migration-mcp}

**AEM Cloud Migration MCP**&#x200B;は、IDE エージェントを&#x200B;**Cloud Acceleration Manager （CAM）**&#x200B;に接続するホスト型[Model Context Protocol （MCP） &#x200B;](https://modelcontextprotocol.io) サーバーです。 設定が完了すると、[AEM Cloud Migration Skill](/help/journey-migration/cloud-migration-skill/overview-cloud-migration-skill.md)は、CSV エクスポートを必要とせずに、CAM プロジェクトからベストプラクティスアナライザーの結果を直接取得できます。

## MCP サーバーURL {#server-url}

```
https://mcp.adobeaemcloud.com/adobe/mcp/cloud-migration
```

このURLをIDEのMCP設定に追加して接続します。

## 内容 {#what-it-provides}

MCP サーバーは、移行スキルがセッション中に自動的に呼び出す2つのツールを公開します。

| ツール | 説明 |
|------|-------------|
| `fetch-cam-bpa-findings-by-pattern` | CAM プロジェクトの最新のBPA レポートから、特定の移行パターン （`scheduler`、`assetApi`、`eventListener`、`resourceChangeListener`、`eventHandler`または`all`）のBPA結果を返します。 |
| `fetch-cam-bpa-findings-by-importance` | 最新のBPA レポートから特定の重要度（`CRITICAL`、`MAJOR`、`ADVISORY`、`INFO`）のすべてのBPA結果を、降順カウントで並べ替えて返します。 最初に対処するパターンを優先付けするのに便利です。 |

## 前提条件 {#prerequisites}

* BPA レポートをアップロードした&#x200B;**Cloud Acceleration Manager** プロジェクト。 [CAM対応フェーズ &#x200B;](/help/journey-migration/cloud-acceleration-manager/using-cam/cam-readiness-phase.md)を参照してください。
* そのCAM プロジェクトにアクセスできる&#x200B;**Adobe ID**。
* リモート MCP サーバーをサポートするAI対応IDE。

## セットアップ {#setup}

1. IDEのMCP設定で、URL `https://mcp.adobeaemcloud.com/adobe/mcp/cloud-migration`を持つ新しいMCP サーバーエントリを追加します。
2. IDEがサーバーに接続するように、設定を保存するかアクティブ化します。
3. プロンプトが表示されたら、**Adobe ID**&#x200B;でログインして認証を完了します。
4. 認証されると、IDEは使用可能な移行ツールを検出し、移行スキルはセッションでそれらを使用できます。

IDE固有の設定手順については、[AEMを使用したMCPの設定](/help/ai-in-aem/mcp-support/using-mcp-with-aem-as-a-cloud-service.md)のガイドを参照してください。

>[!NOTE]
>CAM プロジェクトにアクセスできるAdobe IDでログインする必要があります。 認証エラーが表示された場合は、アカウントがCloud Acceleration Managerで適切な権限を持っていることを確認します。

## 移行セッションでのMCPの使用 {#using-in-session}

MCP サーバーを接続した状態で、次のようなプロンプトを入力して、IDEで移行セッションを開始します。

```
Fetch scheduler findings for project <name>/<id>.
```

エージェント：

1. そのプロジェクトのBPA結果を取得します
2. バッチごとの移行ワークフローを続行

>[!IMPORTANT]
>エージェントが続行する前に、必ずリストからプロジェクトを確認してください。 プロジェクトを明示的に選択するまで、検索結果は取得されません。

### 重要度別の優先順位付け {#by-severity}

パターンの移行を開始する前に、BPA レポートの結果をカウントで並べ替えた概要を確認するには、次の手順を実行します。

```
Show me CRITICAL findings from CAM for project <name>/<id>.
```

セッションでどのパターンを優先するかを決めるために使用します。

## トラブルシューティング {#troubleshooting}

**IDEはMCP サーバーに接続できません**

* URLが上記のように正確に入力されていることを確認します。末尾にスラッシュはありません
* MCP設定を保存した後、IDEを再起動します

**認証に失敗しました**

* CAM プロジェクトにアクセスできるAdobe IDでログインしていることを確認します

**BPA レポートが見つかりません**

* 選択したCAM プロジェクトにBPA レポートがアップロードされていることを確認します。 [&#x200B; ベストプラクティスアナライザーの使用](/help/journey-migration/best-practices-analyzer/using-best-practices-analyzer.md)を参照してください。

## 次の手順 {#whats-next}

MCPを設定した状態で、移行パターンとセッション管理について詳しくは、[&#x200B; クラウド移行スキルの使用](/help/journey-migration/cloud-migration-skill/using-cloud-migration-skill.md)を参照してください。

