---
title: AEM MCP を使用した人類間衝突の設定
description: AEM MCP サーバーに接続するように Anthropic Cloud を設定する方法を説明します
feature: Edge Delivery Services, Agentic AI
role: User, Admin, Architect, Developer
source-git-commit: 8b77b992171623dcf7b065079d72992a5da3a01d
workflow-type: tm+mt
source-wordcount: '149'
ht-degree: 0%

---

# AEM MCP を使用した人類間衝突の設定 {#setup-claude}

次の手順に従って、Anthropic Cloud をAEMの MCP サーバーに接続します。

* Claude の MCP 設定で、1 つ以上のAEM MCP サーバー URL を登録します。
* Adobeのログインフローを完了します。
* オプションで、設定領域で特定のツールの自動確認を有効にします。 検索または読み取り専用操作には、このオプションをお勧めします。
* 会話を開始する前に、MCP サーバーが選択されていることを確認します。
* AEM関連のタスクを実行するように Claude に依頼します。 Claude は、プロンプトに基づいて、MCP サーバーによって公開されるAEM ツールを選択します。

![&#x200B; クラウド設定ダイアログ &#x200B;](assets/claude-1.png)

![&#x200B; クラウドのコネクタパネル &#x200B;](assets/claude-2.png)

![&#x200B; クラウドへのカスタムコネクタの追加 &#x200B;](assets/claude-3.png)

![Claude のカスタムコネクタの接続 &#x200B;](assets/claude-4.png)

![Claude のカスタムコネクタ設定フォーム &#x200B;](assets/claude-5.png)

![&#x200B; カスタムコネクタのツール権限ダイアログ &#x200B;](assets/claude-6.png)

![AEM コンテンツ MCP サービスを使用するようクラウドに促すメッセージ &#x200B;](assets/claude-7.png)
