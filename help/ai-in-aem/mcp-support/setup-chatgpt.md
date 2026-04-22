---
title: AEM MCPを使用したOpenAI ChatGPTの設定
description: AEM MCP サーバーに接続するようにOpenAI ChatGPTを設定する方法を説明します
feature: Edge Delivery Services, Agentic AI
role: User, Admin, Developer
exl-id: 1f116225-168b-483c-9df6-c752a573b57b
source-git-commit: f7a5c43a4a4dd6629225f3628a7c592056d6d144
workflow-type: tm+mt
source-wordcount: '283'
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

>[!NOTE]
>
>OpenAI ChatGPT ユーザーインターフェイスは変更される可能性があり、決定的ではありません。 これらの手順は例示の目的で使用します。

1. **設定**&#x200B;を開いて、MCP接続またはツールが設定されている領域にアクセスできるようにします。

   ![ChatGPT設定ダイアログ。](assets/chatgpt-1.png)

1. **アプリとコネクタ**&#x200B;で、**詳細設定**&#x200B;を開いて、コネクタとMCP関連のオプションを管理します。

   ![ChatGPTのアプリとコネクタの詳細設定パネル &#x200B;](assets/chatgpt-2.png)

1. **アプリとコネクタ**&#x200B;で&#x200B;**開発者モード**&#x200B;を有効にして、カスタムアプリまたはコネクタを追加および設定できるようにします。

   ![&#x200B; アプリとコネクタ セクションで開発者モードを有効にしています。](assets/chatgpt-3.png)

1. **新しいアプリを作成** （または同等のコントロール）を開始して、AEM MCP サーバーのアプリエントリを追加します。

   ![ChatGPTで新しいアプリを作成するためのダイアログ。](assets/chatgpt-4.png)

1. **新しいアプリ** フォームに入力します。例えば、アプリに名前を付け、AEM MCP サーバーのURLおよびその他の必須フィールドを入力してから、**保存**&#x200B;します。

   ![ChatGPTの新しいアプリ設定フォーム。](assets/chatgpt-5.png)

1. **アプリとコネクタ**&#x200B;に&#x200B;**AEM Content MCP Service** （または設定済みのアプリ）が表示されていることを確認して、ChatGPTで使用できるようにします。

   ![&#x200B; アプリとコネクタにリストされているAEM Content MCP サービス。](assets/chatgpt-6.png)

1. チャットで、設定された&#x200B;**AEM ツール**&#x200B;を使用するようにChatGPTに指示するプロンプトを書きます（例えば、作成者のコンテンツやサイトを照会します）。

   ![ChatGPTにAEM Content MCP サービスの使用を促しています。](assets/chatgpt-7.png)
