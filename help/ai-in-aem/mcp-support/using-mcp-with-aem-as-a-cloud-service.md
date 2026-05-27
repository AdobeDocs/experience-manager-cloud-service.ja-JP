---
title: AEM as a Cloud ServiceでのMCPの使用
description: AEM as a Cloud ServiceでModel Context Protocolを使用する方法を説明します
feature: Edge Delivery Services, Agentic AI
role: User, Admin, Developer
exl-id: ddb7fc8c-affc-4374-8e08-d45d96017109
source-git-commit: 6b354e8c8fe1de2341e7e4630b82a3b61c5a4ee6
workflow-type: tm+mt
source-wordcount: '1938'
ht-degree: 1%

---


# AEM as a Cloud ServiceでのMCPの使用 {#using-mcp-with-aem-as-a-cloud-service}

## はじめに {#introduction}

現在、多くのAdobe Experience Manager（AEM）チームは、統合開発環境（IDE）や、Cursor、OpenAI ChatGPT、Anthropic Claude、Microsoft Copilot Studioなどのチャットベースのアプリケーションで作業しています。 これらのアプリケーションは、モデルコンテキストプロトコル（MCP）をサポートしています。これにより、アプリケーションはバックエンドツールを標準化された方法で大規模言語モデル（LLM）に公開できます。

AEMのMCPとの統合により、様々なペルソナが同じコンテンツを中心に共同作業できるようになります。

* **開発者**&#x200B;は、IDEまたはチャットアプリケーションからコンテンツ操作とワークフローを調整できます。
* **実務担当者**&#x200B;およびコンテンツアーキテクトは、AEMの既存の権限モデル内で、AIの支援を受けながら、サイトとコンテンツフラグメントを管理し、アセットをインポートできます。

>[!IMPORTANT]
>
> コンテンツを変更または削除するシナリオの場合、実務担当者は、MCP ツールを直接呼び出すのではなく、AI アシスタントインターフェイスを使用する必要があります。 AI アシスタントが実行するAEM Agentsには、組み込みのセーフガードが含まれています。

この記事では、AEMのMCP機能の内容、サポートされているMCP アプリケーション、設定方法、および実際の使用方法について説明します。

## MCPがAEMのお客様に役立つ理由 {#why-mcp-is-useful-for-aem-customers}

最新のIDEおよびチャットアプリケーションでは、LLMがMCP サーバーの背後にあるツールを呼び出す方法としてMCPを使用しています。 顧客は、低レベルのAPI仕様に照らしてコードを記述するのではなく、自然言語で意図を説明できます。 例えば、*のようなプロンプトを入力すると、「すべてのページにわたってこのキャンペーンのヒーローバナーを更新する」*&#x200B;と入力すると、LLMは適切なMCP ツールを呼び出し、その後AEMのAPIとやり取りできます。

主なメリットは次のとおりです。

* **API配管の代わりに自然言語による操作** - MCP ツールは、使用可能な操作とその呼び出し方法を説明します。 LLMでは、これらのスキーマを使用して、どのツールをどのパラメーターで呼び出すかを決定します。
* **アプリケーション間で一貫性のあるエクスペリエンス** – 同じAEM MCP ツールを複数のMCP互換アプリケーションから使用できるため、同じ基盤となるAEM機能を呼び出しながら、チームが最も生産的な場所で作業できるようになります。
* **セキュリティとガバナンスを保持** - AEM MCP ツールへのリクエストは、認証済みユーザーのIDで実行され、各ツールはユーザーの既存のAEM権限を適用します。 AIを活用したオペレーションは、AEMでの手作業と同じアクセスルールに従います。

## AEMが提供するMCP サーバー {#mcp-servers-provided-by-aem}

AEMは、MCP サーバーをHTTP エンドポイントとして公開します。 以下に示すエンドポイントは`https://mcp.adobeaemcloud.com/adobe/mcp/`に対する相対パスです。

### MCP サーバー {#mcp-servers}

| MCP サーバー | エンドポイント | 説明 |
|---|---|---|
| **コンテンツ** | `/content` | ページやコンテンツフラグメントの作成、読み取り、更新、削除（CRUD）などのコンテンツ操作に加えて、アセットの読み込みや検索も可能です。<br>`aemcs-mcp-feedback@adobe.com`に電子メールを送信して、**アセット検索**&#x200B;を有効にします。 組織名とユースケースをメールに含めます。 |
| **コンテンツ（読み取り専用）** | `/content-readonly` | ページとコンテンツフラグメントの読み取り専用コンテンツ操作（取得、リスト/検索）、アセット検索。<br>`aemcs-mcp-feedback@adobe.com`に電子メールを送信して、**アセット検索**&#x200B;を有効にします。 組織名とユースケースをメールに含めます。 |
| **Cloud Manager** | `/cloudmanager` | プログラム、環境、リポジトリ、パイプラインなど、トリガー可能なCloud Manager エンティティを管理します。 |
| **エクスペリエンスガバナンス** | `/experience-governance` | コンテンツ（テキスト、画像、ページ）をブランドガバナンスルールに照らして評価し、ブランドの設定とチェックをリストアップします。<br/>興味がある場合は、Experience Governance MCPにアクセスするには、[ エージェント体験版にサインアップするか、有料ライセンス ](https://experienceleague.adobe.com/en/docs/experience-cloud-ai/experience-cloud-ai/agents/trial)を取得する必要があります。 |
| **クラウド移行** | `/cloud-migration` | 移行パターンまたは重大度レベルによってCloud Acceleration Manager（CAM）からベストプラクティスアナライザー（BPA）の結果を取得し、AI エージェントがAEM 6.xからAEM as a Cloud Serviceへのコード移行を推進できるようにします。 [ クラウド移行MCPの使用](/help/journey-migration/cloud-migration-skill/using-cloud-migration-mcp.md)を参照してください。 |

各MCP サーバーによって公開される特定のツールは、時間の経過とともに進化する可能性があります。 実際には、MCP対応アプリケーションに、次のようなプロンプトを使用してツールを検索するように依頼できます。

```
"List all AEM tools available from this server and describe what they do."
```

MCP クライアントはMCP プロトコルを使用してツールリストとスキーマを取得し、LLMはそれを使用できます。

機能とその使用方法について詳しくは、[Content MCP Server Tutorial](https://experienceleague.adobe.com/en/docs/experience-manager-learn/cloud-service/ai/mcp-servers/accelerate-content-operations-with-aem-mcp-server)および[Cloud Manager MCP Server Video](https://experienceleague.adobe.com/en/docs/experience-manager-learn/cloud-service/ai/mcp-servers/cloud-manager)を参照してください。

## サポートされているMCP アプリケーション {#supported-mcp-applications}

AEMのMCP サーバーは、定義されたMCP互換アプリケーションのセットで動作するように設計されています。 各アプリケーションは独自の設定エクスペリエンスを提供しますが、大まかな手順は似ています。

### チャットアプリケーション（Webおよびデスクトップ） {#chat-applications}

* 人道クロード
* OpenAI ChatGPT

### 開発者用ツール（IDE拡張機能、デスクトップアプリ、CLI） {#developer-tools}

* 人工クロードコード（CLI、JetBrains、VS Code、カーソル）
* 拡張コード（CLI、JetBrains、VS Code、カーソル）
* インデントデスクトップアプリを拡張
* Cline （JetBrains、VS Code、カーソル）
* カーソル
* GitHub Copilot （JetBrains, VS Code）
* Kiro （デスクトップアプリ、CLI）
* OpenAI Codex （デスクトップアプリ）
* OpenAI Codex CLI
* ウィンドサーフ

### エンタープライズプラットフォーム {#enterprise-platforms}

* Microsoft Copilot Studio

## 設定の概要 {#setup-overview}

AEM用のMCPの設定には、次の2つの主要な部分があります。

1. **各MCP クライアント アプリケーション**&#x200B;を構成して、アプリケーションがAEMのMCP サーバーへの接続方法とOAuth ログインの実行方法を認識できるようにします。
1. **MCP クライアントが使用を認識できるように、プロンプトを開始する前にMCP サーバー**&#x200B;を選択します。

両方のステップをカバーするステップバイステップガイドは、次の目的で利用できます。

* [Anthropic Claude （MCP サーバーを手動で設定し、AEM Claude Connectorもインストールする場合）](/help/ai-in-aem/mcp-support/setup-claude.md)
* [OpenAI ChatGPT](/help/ai-in-aem/mcp-support/setup-chatgpt.md)
* [カーソル](/help/ai-in-aem/mcp-support/setup-cursor.md)
* [JetBrainsとGitHub Copilot](/help/ai-in-aem/mcp-support/setup-jetbrains-copilot.md)
* [Microsoft Copilot Studio](/help/ai-in-aem/mcp-support/setup-microsoft-copilot-studio.md)

### AEM の設定 {#aem-configuration}

デフォルトでは、AEM内の個々のユーザーが持つ権限によって、AEMのMCP サーバーへのアクセスが管理されます。 MCP クライアントアプリケーションを介して認証を行う場合、MCP ツールは、AEMの手動操作と同じアクセスルールを適用します。 ユーザーは、既に実行が許可されているアクションのみを実行できます。

#### 許可されているMCP クライアントアプリケーション {#permitted-mcp-client-applications}

[ サポートされているMCP アプリケーション ](#supported-mcp-applications)にリストされているすべてのアプリケーションは、デフォルトで許可されています。

#### MCP サーバーの制限 {#restricting-mcp-servers}

デフォルトでは、すべてのMCP サーバが許可リストに加えるされます。 管理者は、組織、プログラム、または環境レベルで特定のMCP サーバーへのアクセスを制限するオプションを使用できます。 この制限により、組織内のユーザーが利用できるMCP機能を詳細に制御できます。

#### MCP クライアントアクセスの管理 {#managing-mcp-client-access}

管理者は、組織のポリシーでアクセスが必要な場合は、特定のMCP クライアントアプリケーションのアクセスを無効にすることもできます。 Adobeで他のMCP クライアント製品のサポートを有効にする場合は、製品web サイトへのリンクを送信します。 カスタム MCP クライアントを許可リストに加えるする必要がある場合も、連絡してください。

MCP サーバーに関連するすべてのリクエストについては、**`aemcs-mcp-feedback@adobe.com`**&#x200B;でAdobeにお気軽にお問い合わせください

### MCP クライアントアプリケーション設定 {#mcp-client-application-configuration}

各ユーザーがこの手順を実行するか、MCP クライアントアプリケーションの管理者がサポートされている場合に実行できます。 設定の詳細は、アプリケーションによって少し異なります。 MCP クライアントは急速に進化しており、リモート MCP サーバーのサポートが積極的に開発されています。 リモートサーバーを追加する機能にアクセスするには、開発者モードを有効にする必要がある場合がありますが、一般的なプロセスは次のとおりです。

1. 1つ以上のMCP サーバーURLを追加します。
   * 上記の表から1つ以上のMCP エンドポイントを設定します。 例：`https://mcp.adobeaemcloud.com/adobe/mcp/content-readonly`
1. 接続をトリガーします。
   * MCP クライアントアプリケーションがMCP サーバーへの接続を試みるように、設定を保存またはアクティブ化します
1. Adobe IDでログインします。
   * プロンプトが表示されたら、Adobe ログインフローを完了して、アプリケーションがAdobe IDに関連付けられたOAuth トークンを取得できるようにします
1. 検出されたツールを確認します。
   * 認証されると、アプリケーションはサーバーからMCP ツールを検出します。 その後、LLMに対してAEM操作を実行するように求めるプロンプトを開始できます。

サポートされているアプリケーションの完全なリストについては、[ サポートされているMCP アプリケーション ](#supported-mcp-applications)を参照してください。

## 認証 {#authentication}

AdobeでホストされるMCP サーバーは、OAuthを実装し、Adobe ID システムと統合されます。

* MCP クライアントアプリケーションがMCP サーバーに接続すると、Adobe ログインダイアログが表示され、**Adobe ID**&#x200B;で認証されます
* ログインが成功すると、システムはMCP クライアントアプリケーションが組織内で許可され、要求されたMCP サーバーが許可されていることを確認します。 いずれかのチェックが失敗すると、エラーメッセージが表示されます。

![MCP クライアントが許可されていません。エラー](assets/MCP-Client-not-permitted.png)

* 確認が完了すると、MCP サーバーは、アプリケーションが後続のツール呼び出しに使用するトークンを発行します。
* MCP ツールは、ユーザーのAEM権限を尊重します。 AEMでコンテンツフラグメントを変更する権限を持つユーザーのみが、MCPを介してコンテンツフラグメントを変更できます。

このアプローチにより、AIを活用した運用が、既存のAEMのセキュリティおよびガバナンスモデルに準拠できるようになります。

## AEMでのMCPの使用 {#using-mcp-with-aem}

AEMとMCP クライアントアプリケーションを設定したら、任意のアプリケーションで作業し、LLMにAEM操作を実行するように求めることができます。 LLMは、MCP ツールスキーマを読み取り、呼び出すツールを選択し、必要に応じてシーケンス化して、リクエストを処理します。

>[!IMPORTANT]
>
>複数のステップを含むプロンプトや、画像やテキストなど、異なるコンテンツタイプをターゲットにするプロンプトは、思考モデルで最も効果的です。 自動モードに依存する代わりに、MCP クライアントで思考モデルを有効にするか、「思考」オプションを選択します。

### 使用例 {#example-use-cases}

代表的なシナリオには、次のようなものがあります。

* 環境の発見
   * ワークフローを実行する場所を決定するための環境とライセンスのリスト。
* サイト管理
   * サイトの一覧表示
   * ページとページコンテンツを作成、読み取り、更新、削除します。
* コンテンツフラグメント管理
   * コンテンツフラグメントの検索
   * 新しいフラグメントを作成
   * キャンペーンメッセージが変更された場合に既存のフラグメントを更新します。
* アセットの読み込み
   * ステータスチェック付きアセットの読み込み
* アセット検索

  >[!NOTE]
  >
  >`aemcs-mcp-feedback@adobe.com`に電子メールを送信して、アセット検索を有効にします。 組織名とユースケースをメールに含めます。

### ワークフローの例 {#example-workflows}

次の例は、LLMがMCP ツールを連鎖させる方法を示しています。

1. **ページで参照されているコンテンツフラグメントの操作**
   * **ページコンテンツを取得** - `get-aem-page-content`などのツールを呼び出して、ページを取得し、`fragmentPath` プロパティを見つけます。
   * **フラグメントパスを解決** - `resolve_fragment_path`を使用してパスをUUIDに変換します。
   * **フラグメントデータを取得** - `get_fragment`を呼び出して、現在のフィールドを取得します。
   * **フラグメントを更新** - `patch_fragment`を呼び出して、フラグメントコンテンツに変更を適用します。
1. **モデルに基づく新しいコンテンツの作成**
   * **モデルを見つける** - `list_models`を使用して、使用可能なコンテンツフラグメントモデルを確認します。
   * **モデルを検査** - `get_model`を使用して、モデルのフィールドスキーマを理解します。
   * **コンテンツを作成** - `create_fragment`を使用して、プロンプトから派生した値を持つ新しいフラグメントを作成します。
1. **既存のコンテンツを安全に更新する**
   * **現在のデータを読み取る** - `get_fragment`を使用して、既存のデータとETagを取得します。
   * **JSON パッチを適用** - ETagとJSON パッチドキュメントで`patch_fragment`を使用してフラグメントを更新し、楽観的な同時実行をサポートします。

ユーザーの観点からは、次のようなプロンプトを使用してこれらのワークフローを開始できます。

```
"Create a new content fragment for the spring campaign based on our hero banner model and fill in its fields from this brief."
```

LLMは、必要なMCP ツールを自動的に選択して調整します。

## 期待管理 {#expectation-management}

MCPを通じてLLMを使用する場合は、次の点に留意してください。

* **高度な能力を備えているが間違いがない** - LLMは複雑なタスクを実行できますが、エラーが発生する可能性があります。 同じプロンプトでも、明確な理由がなくても、結果やプレゼンテーションが少し異なる場合があります。 本番コンテンツに変更を適用する前に、必ず出力を確認してください。
* **機能の進化** - LLM モデルは継続的に改善されています。 時間の経過とともに、MCP ツールを組み合わせて目標を達成するための新しい方法を見出す能力が高まります。 今日、複数のプロンプトを入力する必要があったタスクは、明日には1つのプロンプトとシームレスに連携する可能性があります。
* **人間による監視は不可欠です** - LLMは、監視を必要とする知識豊富なアシスタントだと考えてください。 幅広い知識を備えており、クリエイティブソリューションを考案することもできますが、ガイダンスとレビューから利点があります。 特に重要な操作について結果を検証し、出力が期待に沿わない場合にフィードバックを提供します。
* **ツールの自動承認に注意する** - Claudeなどの一部のMCP クライアントアプリケーションでは、LLMから要求されたツールの実行を自動承認するオプションが提供されています。 このオプションは、コンテンツの検索や取得などの読み取り専用の操作には便利ですが、コンテンツを更新または削除するツールでは注意が必要です。 AEM環境を変更するアクションを確認する前に、各ツールの実行リクエストを確認します。

## 制限事項 {#limitations}

AEMは現在、[ サポートされているMCP アプリケーション ](#supported-mcp-applications)に記載されているアプリケーションでMCP サーバーの設定をサポートしています。

別のMCP クライアントアプリケーションを使用する場合は、お気軽に&#x200B;**`aemcs-mcp-feedback@adobe.com`**&#x200B;までご連絡いただき、その他のクライアントのサポートをリクエストするか、カスタムクライアントを許可リストに加えるしてください。
