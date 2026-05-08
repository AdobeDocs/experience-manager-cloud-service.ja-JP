---
title: AEM MCPでのAnthropic Claudeの設定
description: AEMのMCP サーバーに接続するようにAnthropic Cloudを設定する方法を説明します
feature: Edge Delivery Services, Agentic AI
role: User, Admin, Developer
exl-id: 2b90b2b2-cdd0-4f1e-890f-2f58f578face
source-git-commit: 07a7aa5f02d7bfa992df825f3b8a19e18d569d5b
workflow-type: tm+mt
source-wordcount: '500'
ht-degree: 0%

---

# AEM MCPでのAnthropic Claudeの設定 {#setup-claude}

この記事では、AEMでAnthropic Claudeを使用する2つの方法について説明します。

- Claudeで1つ以上のAEMのMCP サーバーを手動で設定します（[AEM as a Cloud ServiceでのMCPの使用 – MCP サーバー](/help/ai-in-aem/mcp-support/using-mcp-with-aem-as-a-cloud-service.md#mcp-servers)で説明されているサーバー）。
- AnthropicのコネクタマーケットプレイスからAdobe Experience Manager コネクタをインストールします。 現在、Content MCP Serverと同等の機能を備えており、AEMのMCP サーバーで利用可能なツールのサブセットを拡大する予定です。



## ClaudeでのAEMのMCP サーバーの手動設定 {#manual-configure-aems-mcp-servers-in-claude}

この節では、**手動設定**&#x200B;のアプローチについて説明します。このアプローチでは、1つ以上のAEM MCP サーバーをカスタムコネクタとしてClaudeに追加します。

>[!NOTE]
>
>Claude ユーザーインターフェイスは変更される可能性があり、決定的ではありません。 これらの手順は例示の目的で使用します。

1. Claude web アプリの左下隅にあるアカウントメニューを開き、**設定**&#x200B;を選択して設定領域を開きます。

   ![設定が選択されたクラウドのアカウントメニュー。](assets/claude-1.png)

1. 設定サイドバーで、**コネクタ**&#x200B;を選択します。 コネクタ ページで、**カスタムコネクタを追加**&#x200B;を選択して、カスタム MCP エンドポイントを登録します。

   カスタムコネクタを追加した設定の![ コネクタ ページ。](assets/claude-2.png)

1. **カスタムコネクタを追加** ダイアログで、表示名（**AEM Content MCP Service**&#x200B;など）とMCP サーバーのURLを入力し、**Add**&#x200B;を選択します。 展開に追加オプションが必要な場合にのみ&#x200B;**詳細設定**&#x200B;を使用してください。

   ![名前とMCP URLを含むカスタムコネクタダイアログを追加します。](assets/claude-3.png)

1. コネクタリストで、カスタムコネクタエントリ（**CUSTOM** ラベルが表示されています）を見つけ、**Connect**&#x200B;を選択してログインし、コネクタをClaude アカウントにリンクします。

   AEM Content MCP Service用にConnectが選択された![Connectors リスト。](assets/claude-4.png)

1. コネクタがURLを含むリストに表示されたら、**AEM Content MCP Service**&#x200B;の横にある&#x200B;**Configure**&#x200B;を選択して、コネクタの詳細を開き、セットアップを続行します。

   AEM Content MCP Service用にConfigureが選択された![Connectors リスト。](assets/claude-5.png)

1. **ツールの権限** ページで、デフォルト値（**Needs approval**&#x200B;など）を確認し、各AEM ツールを&#x200B;**Always allow**、**Ask for permission**、または&#x200B;**Never allow**&#x200B;にセキュリティポリシーに従って設定します。

   ![AEM Content MCP サービスのツール権限。](assets/claude-6.png)

1. 会話を開きます。 メッセージフィールドの左側にある「ツールとモデル」メニュー（スライダーアイコン）を選択し、「コネクタ」で「**AEM Content MCP Service**」を有効にし、プロンプトを入力して、ClaudeがそのチャットにMCP ツールを使用できるようにします。

   ![ ツールメニューでAEM Content MCP サービスを有効にしたチャットコンポーザー。](assets/claude-7.png)

## Adobe Experience Manager コネクタ（Anthropic コネクタマーケットプレイス）のインストール {#install-adobe-experience-manager-connector}

この節では、（カスタムコネクタ URLを追加するのではなく） Anthropicのコネクタマーケットプレイスから&#x200B;**インストール可能なコネクタ**&#x200B;について説明します。 これには、AEMのMCP サーバーで使用可能なツールのサブセットが含まれます。

**Adobe Experience Manager Connector**&#x200B;をインストールするには、Claudeで&#x200B;**Settings** > **Connectors**&#x200B;を開きます。 また、[https://claude.ai/settings/connectors](https://claude.ai/settings/connectors)でコネクタ ページを直接開くこともできます。 コネクターは、AEM ワークフロー用のツールのセットを公開するMCP サーバーを登録します。

![Connectors ディレクトリからAdobe Experience Manager Cloud Connectorをインストールしています。](assets/claude-connector.png)