---
title: GitHub CopilotとAEM MCPを使用したJetBrainsの設定
description: JetBrains IDEでGitHub Copilotを設定してAEM MCP サーバーに接続する方法を説明します
feature: Edge Delivery Services, Agentic AI
role: User, Admin, Developer
exl-id: e153da42-51e0-49ea-8457-10bb5e77e2de
source-git-commit: 81f85045212ca6fd92f2b665aeceaa0d4b92318c
workflow-type: tm+mt
source-wordcount: '260'
ht-degree: 1%

---

# GitHub CopilotとAEM MCPを使用したJetBrainsの設定 {#setup-jetbrains-copilot}

JetBrains IDE （IntelliJ IDEA、WebStorm、PyCharmなど）のGitHub CopilotをAEMのMCP サーバーに接続するには、次の手順に従います。

1. エディターの右側にある&#x200B;**GitHub Copilot Chat** アイコンをクリックして、JetBrains IDEでGitHub Copilot Chatを開きます。

   ![GitHub Copilot チャットを開いたJetBrains IDE。](assets/jetbrains-copilot-1.png)

1. コパイロット チャット パネルの&#x200B;**settings** アイコンをクリックして、MCP設定を開きます。

   ![設定アイコンがハイライト表示されたGitHub コパイロット チャット パネル。](assets/jetbrains-copilot-2.png)

1. **設定**&#x200B;で、**ツール > GitHub Copilot > Model Context Protocol （MCP）**&#x200B;に移動し、**Configure**&#x200B;をクリックして`mcp.json`設定ファイルを開きます。

   ![JetBrains設定ダイアログに、GitHub コパイロットの下のModel Context Protocol （MCP）設定が表示されます。](assets/jetbrains-copilot-3.png)

1. 1つ以上のAEM MCP サーバーのURLを`mcp.json` ファイルに追加します。 次に例を示します。

   ```json
   {
     "servers": {
       "aem": {
         "url": "https://mcp.adobeaemcloud.com/adobe/mcp/content"
       }
     }
   }
   ```


   ![AEM MCP サーバーのURLを含むmcp.json設定ファイル。](assets/jetbrains-copilot-4.png)


1. ファイルを保存します。GitHub Copilotは、新しいサーバー設定を自動的に検出し、**開始** アクションを表示します。

   ![検出されたツールを含む設定済みのAEM サーバーを示すmcp.json ファイル。](assets/jetbrains-copilot-5.png)

1. 「**開始**」アクションをクリックし、プロンプトが表示されたら、Adobe IDでログインして認証フローを完了します。

1. コパイロット チャット パネルに表示される&#x200B;**ツール** インジケーターをクリックすると、検出されたツールを確認および管理できます。 オプションで、個々のツールを有効または無効にします。


   ![使用可能なAEM MCP ツールを表示するツールの設定ダイアログ。](assets/jetbrains-copilot-6.png)

1. GitHub Copilot Chatを使用すると、開発ワークフローやコンテンツワークフローの一部としてAEM ツールを呼び出すことができます。
