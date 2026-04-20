---
title: AI ツールを使用したローカル開発
description: プロジェクトのコンテキスト、エージェントスキル、MCP サーバーを使用して、AI コーディングツールを設定し、AEM as a Cloud Serviceの開発を加速する方法を説明します。
feature: Developing
role: Developer
exl-id: 09d6257d-36ad-49e5-831f-c44b356f1800
source-git-commit: 0fb601ee1479bdcbb4932592185c5984d56171ef
workflow-type: tm+mt
source-wordcount: '1423'
ht-degree: 1%

---

# AI ツールを使用したローカル開発 {#local-development-with-ai-tools}

>[!NOTE]
>
>この記事では、**AEM Java スタック開発**&#x200B;のAI ツールを使用したローカル開発に焦点を当てます。 Edge Delivery Servicesについては、[AI ツールを使用した開発](https://www.aem.live/developer/ai-coding-agents)を参照してください。

AI コーディングエージェント（Claude Code、Cursor、GitHub Copilotなどのツール）は、AEMの基盤となるテクノロジー（Java、OSGi、Sling、JCR、HTL）に関する幅広い知識を備えていますが、コードと設定の生成に関するベストプラクティスや、AEM開発に関する一般的な問題のデバッグ方法については、必ずしも知られていません。

これに対応する4つの補完的なコンポーネント：

| コンポーネント | 目的 |
|---|---|
| **AGENTS.md** | AEM Cloud Service プロジェクト内のAIを各セッションに基づくプロジェクト固有のコンテキストファイル |
| **エージェントのスキル** | コンポーネントの作成やDispatcherの設定など、繰り返し実行される開発タスク用に再利用可能な命令セット |
| **AEM クイックスタート ローカル MCP サーバー** | トラブルシューティングをサポートするために、ローカルのAEM SDK インスタンスからライブランタイムデータを公開します |
| **Dispatcher ローカル MCP サーバー** | ローカル Dispatcher インスタンスのランタイム検証と検査を有効にします |

>[!NOTE]
>
> ローカル開発にも便利ですが、この記事では説明しませんが、AEM Cloud Serviceのリモート MCP サーバーです。 詳しくは、[Cloud ServiceでのMCPの使用に関する記事](/help/ai-in-aem/mcp-support/using-mcp-with-aem-as-a-cloud-service.md)を参照してください。

## AGENTS.md {#agentsmd}

`AGENTS.md`は、AEM プロジェクトのルートにあるMarkdown ファイルです。このファイルは、AEM Cloud ServiceのJava スタックドメインに関する基本的な専門知識（AEM 6.5やEdge Delivery Servicesなどの他のAEM ソリューションではなく）を活用するために、AI コーディングツールが各セッションの開始時に自動的に読み込まれます。

`AGENTS.md`は、コピーする静的ファイルではありません。次の節で説明する`ensure-agents-md` スキルによって生成されます。 スキルでは、`pom.xml`を読み取り、プロジェクト名を解決し、モジュールを見つけ出して、インストールされたアドオンを検出し、特定のプロジェクトに合わせたファイルを作成します。

>[!NOTE]
>
>プロジェクト ルートに`AGENTS.md`が存在すると、`ensure-agents-md` スキルは実行されなくなります。 プロジェクト構造が変更された場合は、ファイルを直接編集します。

## エージェントスキル {#agent-skills}

スキルは、マルチステップの開発ワークフローをエンコードする命令セットです。 AIを呼び出すと、一般的な知識のみに依存するのではなく、スキルの手順に従い、一貫した規則に準拠した結果が生成されます。

Adobeは、**[adobe/skills](https://github.com/adobe/skills/tree/main/plugins/aem/cloud-service)** リポジトリでAEM as a Cloud Service スキルを公開します。

| スキル | 目的 |
|---|---|
| `ensure-agents-md` | プロジェクトの実際のモジュール構造に合わせたブートストラップ `AGENTS.md`と`CLAUDE.md` |
| `create-component` | 包括的なAEM コンポーネントの基礎を作成します。コンポーネント定義、ダイアログ XML、HTL テンプレート、Sling モデル、単体テスト、およびclientlibs |
| `dispatcher` | AIを活用したDispatcherとApache HTTPDの設定アシスタントにより、設定のオーサリング、技術的なアドバイス、インシデントへの対応、パフォーマンスチューニング、セキュリティの強化をカバーしています |
| `workflow` | AEM as a Cloud Service Workflowのすべてのスキルを習得する。 ワークフローモデルの設計、カスタムプロセスステップおよび参加者の選択者開発、ランチャー設定、ワークフロートリガー、実稼動サポート（停止/失敗したワークフローのデバッグ、Cloud Manager ログを使用したインシデントのトリアージ、スレッドプール分析、Granite Workflow EngineのSling Job Diagnosticsなど）について説明します。 |

### スキルのインストール {#install-skills}

AI コーディングツールに適した方法を選択してください。 スキルを一度インストールすれば、そのスキルをそのマシン上のすべてのプロジェクトで利用できるようになります。

#### クロード・コード {#claude-code}

```bash
# Add the Adobe Skills marketplace (one-time setup)
/plugin marketplace add adobe/skills

# Install all available skills
/plugin install aem-cloud-service@adobe-skills
```

#### Npx Skills {#npx-skills}

```bash
# Install all available skills
npx skills add https://github.com/adobe/skills/tree/main/skills/aem/cloud-service --all
```

#### Upskill （GitHub CLI拡張機能） {#upskill-github-cli-extension}

```bash
# Install the gh-upskill extension (one-time setup)
gh extension install ai-ecoverse/gh-upskill

# Install all available skills
gh upskill adobe/skills --path skills/aem/cloud-service --all
```

### ensure-agents-md スキルの使用 {#use-the-ensure-agents-md-skill}

スキルをインストールしたら、まだ`AGENTS.md`を持っていないAEM Cloud Service プロジェクトでAI アシスタントを開きます。 スキルは、最初のリクエストを処理する前に自動的に実行され、明示的な呼び出しを必要とせずに、両方のファイルをプロジェクトルートに作成します。

### コンポーネント作成スキルの使用 {#use-the-create-component-skill}

最初に使用すると、スキルは`project`と既存のコンポーネントから`package`、`group`、`pom.xml`を自動的に検出し、検出された値を確認するよう求め、プロジェクトのルートに`.aem-skills-config.yaml`を作成します。 最初に使用する前に、手動で設定する必要はありません。

ファイルを事前作成する場合は、次の構造を持つプロジェクト ルートに`.aem-skills-config.yaml`を配置します。

```yaml
configured: true

project: "wknd"                                    # Check /apps/{project}/ or pom.xml
package: "com.adobe.aem.guides.wknd.core"          # Check core/pom.xml
group: "WKND Components"                           # Check existing component .content.xml files
```

ファイルはスキルディレクトリの外側にあり、スキルの更新時に上書きされることはありません。

AI チャットのコンポーネントについて説明します。

```
Create an AEM component called "Hero Banner"

Dialog specification:
Title (title) - Textfield, mandatory
Subtitle (subtitle) - Textfield
Background Image (backgroundImage) - Fileupload
CTA Text (ctaText) - Textfield
CTA Link (ctaLink) - Pathfield
```

エージェントは、確認のためにフィールド仕様をエコーし、すべてのコンポーネントファイルを生成します。 サポートされているパターンには、複合ネストされたアイテムを含むマルチフィールド、条件付き表示/非表示ロジック、Sling Resource Mergerを介したコアコンポーネント拡張機能、AEM Mocksを使用したJUnit 5 テストなどがあります。

### Dispatcher スキルの使用 {#use-the-dispatcher-skill}

DispatcherまたはApache HTTPD設定作業のDispatcher スキルを呼び出します。 このスキルは、リクエストの性質に応じて、リクエストを6つの専門サブスキルのいずれかにルーティングします。

| サブスキル | 目的 |
|---|---|
| `workflow-orchestrator` | 設計、設定の変更、検証、フォローアップに及ぶエンドツーエンドの作業 |
| `config-authoring` | 具体的な設定変更：フィルター、キャッシュルール、書き換え、vhost、ヘッダー、ファーム |
| `technical-advisory` | 概念ガイダンス、ポリシー説明、引用にもとづく推奨 |
| `incident-response` | ランタイムエラー、キャッシュの異常値、リグレッション |
| `performance-tuning` | キャッシュの効率性、レイテンシ、スループットの最適化 |
| `security-hardening` | 露出のレビューと制作の強化 |

幅広いリクエストまたは初めてのリクエストの場合は、`workflow-orchestrator`個のサブスキルから始めます。 ターゲットを絞った作業については、特定の懸念事項と適切な専門家へのスキルルートを説明してください。

Dispatcher スキルは、オーケストレーションとアドバイザリーガイダンスを処理します。 以下に説明するDispatcher MCP サーバーは、スキルがローカルエビデンスを必要とする場合に使用する7つの検証ツールとランタイムツールを提供します。

## AEM Quickstart MCP Server {#aem-quickstart-mcp-server}

Model Context Protocol （MCP）は、AI コーディングツールを外部のデータソースやサービスに接続できるようにする、オープンスタンダードです。 AEM Quickstart MCP サーバーは、ローカルのAEM SDK インスタンスにインストールすると、ランタイムデータを接続されたAI ツールに直接公開するコンテンツパッケージです。これにより、エージェントはIDEから離れることなく、ログを取得し、OSGi エラーを診断し、リクエスト処理を検査できます。

### コンテンツパッケージのインストール {#install-the-content-package}

[&#x200B; ソフトウェア配布ポータル &#x200B;](https://experience.adobe.com/#/downloads/content/software-distribution/en/aemcloud.html?fulltext=mcp*&1_group.propertyvalues.property=.%2Fjcr%3Acontent%2Fmetadata%2Fdc%3AsoftwareType&1_group.propertyvalues.operation=equals&1_group.propertyvalues.0_values=software-type%3Atooling&orderby=%40jcr%3Acontent%2Fjcr%3AlastModified&orderby.sort=desc&layout=list&p.offset=0&p.limit=3)からコンテンツ パッケージをダウンロードし、`com.adobe.aem:com.adobe.aem.mcp-server-contribs-content`のパッケージ マネージャーを使用して`/crx/packmgr`をローカル クイックスタートにインストールします。

**互換性：** AEM SDK `2026.2.24678.20260226T154829Z-260200`以降で検証されました。

### 利用可能なツール {#available-tools}

| ツール | 説明 |
|---|---|
| `aem-logs` | AEMおよびOSGi ログエントリを取得します。正規表現パターン、ログレベル、およびエントリ数でフィルタリング可能です |
| `diagnose-osgi-bundle` | バンドルまたはDS コンポーネントが起動しない理由を診断します。パッケージが見つからない、参照が満たされていない、設定の問題を報告します |
| `recent-requests` | Slingの完全な内部処理トレース（リソース解決、スクリプト解決、フィルターチェーン）を使用して、パス正規表現でフィルタリング可能な最近のHTTP リクエストを返します |

### IDEの設定 {#configure-your-ide}

#### カーソル {#cursor}

カーソル設定で、新しいカスタム MCP サーバーを追加します。

```json
"aem-cs-sdk": {
  "type": "streamable-http",
  "url": "http://localhost:4502/bin/mcp",
  "headers": {
    "Authorization": "Basic YWRtaW46YWRtaW4="
  }
}
```

#### IntelliJ IDEAによるGitHub Copilot {#github-copilot-with-ihtellij-idea}

**ツール/GitHub コパイロット/モデルコンテキストプロトコル（MCP）**&#x200B;に移動し、**設定**&#x200B;をクリックします。 次の行を追加します。

```json
"aem-cs-sdk": {
  "url": "http://localhost:4502/bin/mcp",
  "requestInit": {
    "headers": {
      "Authorization": "Basic YWRtaW46YWRtaW4="
    }
  }
}
```

#### 他のIDE {#other-ides}

任意のMCP クライアントは、`http://localhost:4502/bin/mcp`を`Authorization: Basic YWRtaW46YWRtaW4=` ヘッダーで指定して接続できます。 IDEのMCP設定を使用してカスタムヘッダーを設定します。

>[!NOTE]
>
>値`Basic YWRtaW46YWRtaW4=`は、`admin:admin`のBase64 エンコーディングです。これは、ローカル クイックスタートのデフォルトの資格情報です。 これをローカル以外の環境では使用しないでください。

## Dispatcher MCP Server {#dispatcher-mcp-server}

>[!IMPORTANT]
>
>この機能は&#x200B;**ベータ**&#x200B;です。 Adobeが開発している機能に早期にアクセスすると、お客様やパートナーはフィードバック（[aemcs-ai-ide-tools-feedback@adobe.com](mailto:aemcs-ai-ide-tools-feedback@adobe.com)に電子メールで送信）を提供し、製品開発を形作ることができます。 また、新機能を一般公開する前に導入する準備にも役立ちます。
>
>Beta リリースには欠陥が含まれている場合があり、いかなる保証もなしに「現状のまま」提供されます。 Adobeは、ベータ版のリリースを（Adobe サポートサービスまたはその他の方法により）維持、修正、更新、変更、またはその他の方法でサポートする義務を負いません。 Adobeでは、ベータ版リリースの正しい機能やパフォーマンス、または付随するドキュメントや資料に依存しないように注意することをお勧めします。 ベータ版の機能およびAPIは、予告なく変更される場合があります。 したがって、ベータ版リリースの使用は、完全にお客様の責任で行います。

Dispatcher MCP サーバーは、AEM Dispatcher SDKにバンドルされています。 これにより、AI ツールは、DispatcherとApache HTTPD設定を検証し、リクエスト処理を追跡し、Dockerでローカルに実行されているDispatcher インスタンスに対するキャッシュ動作を調べることができます。

Dispatcher スキルとは異なり、Dispatcher MCP サーバーはツールのみを公開します。7つのMCP ツールとプロンプトやリソースはありません。

### 前提条件 {#prerequisites}

- Docker Desktop 4.x以降がインストールされ、実行されている
- AEM Dispatcher SDKが[Software Distribution Portal](https://experience.adobe.com/#/downloads/content/software-distribution/en/aemcloud.html?fulltext=mcp*&1_group.propertyvalues.property=.%2Fjcr%3Acontent%2Fmetadata%2Fdc%3AsoftwareType&1_group.propertyvalues.operation=equals&1_group.propertyvalues.0_values=software-type%3Atooling&orderby=%40jcr%3Acontent%2Fjcr%3AlastModified&orderby.sort=desc&layout=list&p.offset=0&p.limit=3)からダウンロードされました

>[!NOTE]
>
>`client version 1.43 is too new`が表示される場合は、シェルまたは`DOCKER_API_VERSION=1.41`で`mcp.json`を設定します。

### Dispatcher SDKのインストール {#install-the-dispatcher-sdk}

**macOSとLinux:**

```bash
chmod +x aem-sdk-dispatcher-tools-<version>-unix.sh
./aem-sdk-dispatcher-tools-<version>-unix.sh
cd dispatcher-sdk-<version>
chmod +x ./bin/docker_run_mcp.sh
./bin/docker_run_mcp.sh test
```

**Windows:**

```powershell
Expand-Archive aem-sdk-dispatcher-tools-<version>-windows.zip
```

`./bin/docker_run_mcp.sh help`を実行してコピー&amp;ペーストのIDE設定を取得し、`./bin/docker_run_mcp.sh version`を実行して、バンドルされたMCPとSDKのバージョンを確認します。 `./bin/docker_run_mcp.sh diagnose`を使用して、接続性の問題を調査します。

### カーソルの設定 {#configure-cursor}

`aem-dispatcher-mcp` エントリを`~/.cursor/mcp.json`に追加：

```json
{
  "mcpServers": {
    "aem-dispatcher-mcp": {
      "command": "<path_to_dispatcher_sdk>/bin/docker_run_mcp.sh",
      "env": {
        "DOCKER_API_VERSION": "1.43",
        "AEM_DEPLOYMENT_MODE": "cloud",
        "MCP_LOG_LEVEL": "trace",
        "MCP_LOG_FILE": "/tmp/dispatcher-mcp.log",
        "DISPATCHER_CONFIG_PATH": "<path_to_dispatcher_src>"
      }
    }
  }
}
```

`<path_to_dispatcher_sdk>`を抽出したDispatcher SDKの場所に、`<path_to_dispatcher_src>`をプロジェクトのDispatcher `src` ディレクトリに置き換えます。 `DISPATCHER_CONFIG_PATH`を、`/docroot`が定義されているファイルを含む構成ルートに設定します。 `MCP_LOG_LEVEL`と`MCP_LOG_FILE`はオプションのデバッグ設定です。 `client version 1.43 is too new`が表示される場合は、`DOCKER_API_VERSION`を`1.41`に設定します。 他のMCP サーバーが既に設定されている場合は、置き換えずに`aem-dispatcher-mcp` エントリを追加します。 保存後にカーソルを再起動します。

他のIDEも同様の方法で設定できます。 SDKの`docs/DispatcherMCP.md`には、Claude DesktopとVS Codeの完全な例が含まれています。

### 利用可能なツール {#available-tools-dispatcher}

| ツール | 説明 |
|---|---|
| `validate` | DispatcherおよびApache HTTPD設定を検証します |
| `lint` | モードに応じた静的チェックとベストプラクティス分析を実行 |
| `sdk` | Dispatcher SDK ワークフローを実行：`validate`、`validate-full`、`three-phase-validate`、`docker-test`、`check-files`、`diff-baseline` |
| `trace_request` | 実行時の証拠を使用してリクエストの動作を追跡します |
| `inspect_cache` | ターゲット URLのキャッシュとdocrootの動作を調べます |
| `monitor_metrics` | DispatcherおよびHTTPD ログからランタイム指標を読み取ります |
| `tail_logs` | 関連するDispatcherとHTTPD ランタイムログのテール |

MCP サーフェスでは、意図的にこれらの7つのツールのみを公開します。プロンプトとリソースはスキルレイヤーに残ります。 完全な参照ドキュメントは、抽出されたDispatcher SDK内の`docs/DispatcherMCP.md`で入手できます。
