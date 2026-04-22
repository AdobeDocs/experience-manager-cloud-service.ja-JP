---
title: AEM MCPを使用したMicrosoft Copilot Studioの設定
description: AEM MCP サーバーに接続するようにMicrosoft Copilot Studioを設定する方法について説明します
feature: Edge Delivery Services, Agentic AI
role: User, Admin, Developer
exl-id: c8e96fe6-1a05-47c0-8215-0c28705e5e48
source-git-commit: f7a5c43a4a4dd6629225f3628a7c592056d6d144
workflow-type: tm+mt
source-wordcount: '394'
ht-degree: 0%

---

# AEM MCPを使用したMicrosoft Copilot Studioの設定 {#setup-microsoft-copilot-studio}

Microsoft Copilot StudioをAEMのMCP サーバーに接続するには、次の手順に従います。

>[!NOTE]
>
>Microsoft Copilot Studioのユーザーインターフェイスは変更される可能性があり、決定的なものではありません。 これらの手順は例示の目的で使用します。

1. **Agents**&#x200B;で、フローを開始して、AEM MCP ツールを使用するエージェントを追加します。

   * 新しいエージェントを作成します。

   ![Microsoft Copilot Studioのエージェント パネル。](assets/copilot-1.png)

1. そのエージェントのツール領域を開き、外部機能を呼び出す方法を登録します。

   * ツール セクションに移動し、**ツールを追加**&#x200B;をクリックします。

   ![Microsoft Copilot Studioの「ツールを追加」ダイアログ。](assets/copilot-2.png)

1. 既存の統合を再利用するか、新しいMCP対応ツールを定義するかを決定します。

   * 既存のツールを選択するか、新しいツールを作成します。

   ![ ツールタイプとしてモデル コンテキスト プロトコルを選択しています。](assets/copilot-3.png)

1. 新しいMCP ツールを作成する場合は、**Model Context Protocol** サーバーステップを続行し、表示されるプレビューモードを含めます。

   * 1つ以上のAEM MCP サーバー&#x200B;**URL**&#x200B;を指す新しいMCP ツールを設定します。

   ![ プレビューモードでモデル コンテキスト プロトコル サーバーを追加しています。](assets/copilot-4.png)

1. このMCP エンドポイントにアクセスする方法（アクセスが共有されているか専用であるかなど）をエージェントが定義します。

   * エージェント間で&#x200B;**共有**&#x200B;または&#x200B;**専用**&#x200B;できる接続を確立します。

   ![新しい接続を作成するためのダイアログ。](assets/copilot-5.png)

1. **Add and configure**&#x200B;で、MCP ツールの詳細を指定または確認して、担当者がAEM環境にアクセスできるようにします。

   ![MCP ツールの追加と設定パネル。](assets/copilot-6.png)

1. MCP ツールフォームのフィールドを終了します（例：サーバー&#x200B;**URL**&#x200B;および認証関連オプション）。

   * オプションで、**自動確認モード**&#x200B;を有効にするか、すべてのツール操作に&#x200B;**エンドユーザー確認**&#x200B;を必要とします。

   ![MCP ツール設定フォーム。](assets/copilot-7.png)

1. MCP サーバーへの接続を検証します。Copilot Studioがリダイレクトする際に、ブラウザーベースのサインインを完了します。

   * リダイレクト時に&#x200B;**Adobe ID**&#x200B;を使用してログインします。

   ![AEM MCP サーバーへの接続をテストしています。](assets/copilot-8.png)

1. テストを実行する前に、**接続の管理** （または&#x200B;**接続マネージャー**）を開き、適切な接続をセッションに割り当てます。

   * エージェントをテストする際は、最初に&#x200B;**接続マネージャー**&#x200B;を開いて、セッションに接続を割り当てます。

   ![利用可能な接続を表示する接続を管理パネル。](assets/copilot-9.png)

1. テストエクスペリエンスで、AEM MCP接続に対してエージェントを実行します。

   * エージェントをテストする際、**接続マネージャー**&#x200B;で接続を割り当てた後、**再試行**&#x200B;を押します。

   ![AEM MCP接続でエージェントをテストしています。](assets/copilot-10.png)
