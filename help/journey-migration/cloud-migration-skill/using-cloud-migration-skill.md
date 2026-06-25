---
title: AEM Cloud Migration Skillの使用
description: OSGi設定の変換、BPA ソースオプション、セッション管理ガイダンスなど、AEM Cloud Migration Skillでサポートされている各移行パターンのリファレンスです。
feature: Migration
role: Developer
source-git-commit: 7ea634871fc1655e5f0ec5b3fb88edbb0f317249
workflow-type: tm+mt
source-wordcount: '890'
ht-degree: 0%

---


# AEM Cloud Migration Skillの使用 {#using-cloud-migration-skill}

このリファレンスでは、サポートされている各移行パターン、BPAの調査結果の提供方法、大規模なプロジェクト全体でのセッションの管理方法について説明します。 概要と設定の手順については、[概要](/help/journey-migration/cloud-migration-skill/overview-cloud-migration-skill.md)を参照してください。

## セッションの仕組み {#workflow-overview}

すべての移行セッションは、次の順序に従います。

1. **パターンに名前を付ける**:1つのパターンを指定します（例：`scheduler`）
2. **調査結果を提供**: BPA CSV ファイル、MCP経由のCAM、または特定のファイル パスから
3. **エージェントが変換ルールを読み取ります**: スキルは、コードを変更する前に、関連する変換ルールをコンパニオン `code-assessment` スキルから読み取ります
4. **5人の最初のバッチ**: エージェントは、最大5人の調査結果を変換し、変更された内容を報告します
5. **確認して続行**：各バッチを確認したら、`continue`に返信して次のバッチに進みます

エージェントは一度に1つのパターンと1つのバッチを処理します。 自動的には処理されません。各バッチには確認が必要です。

## 移行パターン {#patterns}

### スケジューラー {#scheduler}

AEMaaCSのステートレスでコンテナ化されたランタイムと互換性のない`sling.commons.scheduler`または`Scheduler` インジェクションを使用するJava クラスをターゲットにします。

**BPA パターン ID:** `scheduler`

エージェントは、コンストラクターベースのスケジューラー登録を`@Activate` / `@Deactivate`のライフサイクルメソッドに置き換えて、`@Designate`を使用して`Scheduler`注入されたジョブを`Runnable`実装の`@Component`に変換します。

### ResourceChangeListener {#resource-change-listener}

AEMaaCSの更新が必要な`ResourceChangeListener`または`ResourceChange`個のリスナー実装をターゲットにします。

**BPA パターン ID:** `resourceChangeListener`

### レプリケーション {#replication}

AEMaaCSではサポートされていない`com.day.cq.replication.Replicator`または関連するレプリケーション APIを読み込むクラスをターゲットにします。 エージェントは、それらを`ContentDistribution` ベースの同等のものに置き換え、対応するOSGi サービス参照を更新します。

**BPA パターン ID:** `replication`

### イベントリスナー {#event-listener}

AEMaaCS イベント処理セマンティクスのために更新する必要があるOSGi `EventListener`または`EventHandler`実装をターゲットにします。

**BPA パターン ID:** `eventListener`

### イベントハンドラー {#event-handler}

AEMaaCSに適応させる必要がある同期OSGi `EventHandler` サービスをターゲットにします。

**BPA パターン ID:** `eventHandler`

### Asset API {#asset-api}

非推奨の`AssetManager`、`DAMEvent`、またはサポートされていないDAM APIを使用してクラスをターゲットにします。 Agentは、サポートされているAEM Assets API同等の機能に置き換えます。

**BPA パターン ID:** `assetApi`

### HTL Lint （data-sly-test） {#htl-lint}

`data-sly-test: redundant constant value comparison`回のプリント警告を生成する`ui.apps`以下のHTL テンプレートをターゲットにします。 エージェントは、コンテンツパッケージを直接スキャンすることで、影響を受けるテンプレートを検出します。このパターンでは、BPA CSVまたはCAM接続は必要ありません。

**BPA パターン ID:** `htlLint`

>[!NOTE]
>`htlLint`件の調査結果がBPA CSV書き出しに表示されません。 このパターンのセッションを開始すると、エージェントはダイレクトファイルスキャンを通じてこれらのパターンを検出します。

### CLOUD MANAGERへのOSGi設定 {#osgi-cloud-manager}

`ui.config`のOSGi設定を、完全な環境固有の処理を使用して、Cloud Manager互換の`.cfg.json`形式に変換します。 これには、次の2つの関連タスクが含まれます。

**形式の変換**&#x200B;を構成

AEMaaCSでは、OSGi設定を`.cfg.json` ファイルとして保存し、環境固有の設定を実行モードでスコープ設定されたフォルダー（`config.author/`、`config.publish/`、`config.dev/`など）に格納する必要があります。 エージェント：

* 既存の`.config`、`.cfg`、およびXML形式のOSGi設定を`.cfg.json`に変換します
* オーサー固有の値とパブリッシュ固有の値の両方を含む設定を、実行モードでスコープ設定されたファイルに分割します
* OSGi メタタイプの仕様（文字列、整数、ブール値、配列）に対してプロパティタイプを検証します
* Adobeが所有するPIDを自動変換するのではなく、手作業によるレビュー用にフラグを付けます

**秘密鍵と環境変数**

コミットされた設定ファイルからプレーンテキストシークレットと環境固有の値を移動し、Cloud Managerのプレースホルダーに置き換えます。

* `$[secret:NAME]`: パスワード、トークン、その他の機密値の場合
* `$[env:NAME]`：環境ごとに異なる機密性のない値（サービス URLなど）の場合

対応する変数とシークレットはCloud Managerに適用され、実行時に挿入されます。値はソースコントロールに保存されません。

>[!IMPORTANT]
>エージェントは会話で秘密値を出力しません。 機密データはすべてデジタル化されたハンドオフファイルに書き込まれ、Cloud Manager APIまたはUIを介して適用されます。

**このパターンでは、BPA CSVまたはCAMは使用されません。** 次の内容でセッションを開始：

```
Scan my config files and create Cloud Manager environment secrets or variables.
```

## BPA Source オプション {#bpa-source}

| ソース | 用途 |
|--------|------------|
| **BPA CSV ファイル** | AEM インスタンスまたはCloud Acceleration ManagerからCSVを書き出しました。 セッションの開始時にファイルパスを指定します。 |
| **MCP経由のCAM** | AEM Cloud Migration MCPが設定されています。 エージェントはCAM プロジェクトをリストし、どのプロジェクトを使用するかを確認し、調査結果を直接取得します。 [ クラウド移行MCPの使用](/help/journey-migration/cloud-migration-skill/using-cloud-migration-mcp.md)を参照してください。 |
| **手動ファイル パス** | BPA レポートなしで特定のファイルを移行する場合。 プロンプトで直接パスを指定します。 |

### MCP エラー処理 {#mcp-errors}

MCP接続がエラー（プロジェクトが見つからないエラーや認証エラーを含む）を返した場合、エージェントは停止し、エラーを表示します。 自動的に別のソースに切り替わることはありません。 停止した状態から、次のことができます。

* 表示されたエージェントのリストから正しいプロジェクトを確認します
* 代替としてBPA CSV パスを指定します
* 手動による移行用に特定のJava ファイルパスを指定する

## 大規模なレポートをまたいだセッション管理 {#large-reports}

多くの発見があるBPA レポートの場合、バッチによるバッチ処理のアプローチにより、次の段階的な検証が可能になります。

1. 各バッチの差分の確認
2. パターン範囲のコミットメッセージでバッチをコミットする
3. 次のバッチを開始するには、`continue`に返信してください
4. パターンのすべての調査結果が完了したことをエージェントが報告するまで繰り返します

コミットごとに&#x200B;**1つのパターン**&#x200B;を使用すると、Git履歴を読み取り可能な状態に保つことができ、必要に応じて個々のパターン変換を簡単に元に戻すことができます。

>[!NOTE]
>すべての調査結果が処理される前にセッションを終了した場合は、新しいセッションで同じパターンとBPA ソースで再起動します。 エージェントは中断したところから再開します。

## Workspace範囲 {#workspace-scope}

エージェントは、開いているIDE ワークスペースフォルダー内でのみファイルを検索および編集します。 親ディレクトリ、兄弟フォルダー、またはディスク上の他の場所はスキャンしません。

BPA検索がワークスペースに存在しないファイルパスを参照する場合、エージェントは停止し、欠落しているパスを通知します。 正しいプロジェクトフォルダーを開くか、パスを明示的に指定して続行します。

