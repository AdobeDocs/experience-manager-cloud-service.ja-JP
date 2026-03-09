---
title: AEM MCP を使用した OpenAI ChatGPT の設定
description: AEM MCP サーバーに接続するように OpenAI ChatGPT を設定する方法を説明します
feature: Edge Delivery Services, Agentic AI
role: User, Admin, Architect, Developer
source-git-commit: 8b77b992171623dcf7b065079d72992a5da3a01d
workflow-type: tm+mt
source-wordcount: '137'
ht-degree: 0%

---

# AEM MCP を使用した OpenAI ChatGPT の設定 {#setup-chatgpt}

OpenAI ChatGPT をAEMの MCP サーバーに接続するには、次の手順に従います。

* MCP 接続またはツールが設定されている領域に、1 つ以上のAEM MCP サーバー URL を追加します。
* 接続をトリガーし、リダイレクトされたらAdobe IDでログインする。
* チャットでは、プロンプトで設定済みのAEM ツールを参照します。例：

  ```
  "Using the configured AEM MCP tools, list all sites in the author environment."
  ```

![ChatGPT 設定ダイアログ ](assets/chatgpt-1.png)

![ChatGPT のアプリとコネクタの詳細設定パネル。](assets/chatgpt-2.png)

![ アプリとコネクタ セクションで開発者モードを有効にする ](assets/chatgpt-3.png)

![ChatGPT で新しいアプリを作成するためのダイアログ ](assets/chatgpt-4.png)

![ChatGPT の新しいアプリ設定フォーム ](assets/chatgpt-5.png)

![ アプリとコネクタにAEM Content MCP サービスのリストが表示されます。](assets/chatgpt-6.png)

![AEM Content MCP Service を使用するよう ChatGPT に促す ](assets/chatgpt-7.png)
