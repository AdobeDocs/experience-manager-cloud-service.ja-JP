---
title: AEM MCPでのAnthropic Claudeの設定
description: AEM MCP サーバーに接続するようにAnthropic Cloudを設定する方法を説明します
feature: Edge Delivery Services, Agentic AI
role: User, Admin, Developer
exl-id: 2b90b2b2-cdd0-4f1e-890f-2f58f578face
source-git-commit: 81f85045212ca6fd92f2b665aeceaa0d4b92318c
workflow-type: tm+mt
source-wordcount: '149'
ht-degree: 0%

---

# AEM MCPでのAnthropic Claudeの設定 {#setup-claude}

Anthropic CloudをAEMのMCP サーバーに接続するには、次の手順に従います。

* ClaudeのMCP設定で、1つ以上のAEM MCP サーバーURLを登録します。
* Adobe ログインフローを実行します。
* オプションで、設定領域の特定のツールに対して自動確認を有効にします。 このオプションは、検索操作または読み取り専用操作に使用することをお勧めします。
* 会話を開始する前に、MCP サーバーが選択されていることを確認します。
* ClaudeにAEM関連のタスクを実行するように依頼します。 Claudeは、プロンプトに基づいて、MCP サーバーが公開するAEM ツールを選択します。

![&#x200B; クラウド設定ダイアログ。](assets/claude-1.png)

![Claudeのコネクタ パネル。](assets/claude-2.png)

![Claudeでカスタムコネクタを追加しています。](assets/claude-3.png)

![Claudeでカスタムコネクタを接続しています。](assets/claude-4.png)

![Claudeのカスタムコネクタ設定フォーム。](assets/claude-5.png)

![&#x200B; カスタムコネクタのツール権限ダイアログ。](assets/claude-6.png)

![AEM Content MCP サービスを使用するようにClaudeに促します。](assets/claude-7.png)
