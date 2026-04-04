---
title: AEM MCPを使用したOpenAI ChatGPTの設定
description: AEM MCP サーバーに接続するようにOpenAI ChatGPTを設定する方法を説明します
feature: Edge Delivery Services, Agentic AI
role: User, Admin, Developer
exl-id: 1f116225-168b-483c-9df6-c752a573b57b
source-git-commit: 81f85045212ca6fd92f2b665aeceaa0d4b92318c
workflow-type: tm+mt
source-wordcount: '137'
ht-degree: 0%

---

# AEM MCPを使用したOpenAI ChatGPTの設定 {#setup-chatgpt}

OpenAI ChatGPTをAEMのMCP サーバーに接続するには、次の手順に従います。

* MCP接続またはツールが設定されている領域に、1つ以上のAEM MCP サーバーURLを追加します。
* リダイレクトされたら、接続をトリガーし、Adobe IDでログインします。
* チャットでは、プロンプトで設定されたAEM ツールを参照します。次に例を示します。

  ```
  "Using the configured AEM MCP tools, list all sites in the author environment."
  ```

![ChatGPT設定ダイアログ。](assets/chatgpt-1.png)

![ChatGPTのアプリとコネクタの詳細設定パネル &#x200B;](assets/chatgpt-2.png)

![&#x200B; アプリとコネクタ セクションで開発者モードを有効にしています。](assets/chatgpt-3.png)

![ChatGPTで新しいアプリを作成するためのダイアログ。](assets/chatgpt-4.png)

![ChatGPTの新しいアプリ設定フォーム。](assets/chatgpt-5.png)

![&#x200B; アプリとコネクタにリストされているAEM Content MCP サービス。](assets/chatgpt-6.png)

![ChatGPTにAEM Content MCP サービスの使用を促しています。](assets/chatgpt-7.png)
