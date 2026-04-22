---
title: AEM MCPでのカーソルの設定
description: AEM MCP サーバーに接続するようにCursorを設定する方法を説明します
feature: Edge Delivery Services, Agentic AI
role: User, Admin, Developer
exl-id: f0897898-cb1d-4af6-859c-f5a1c0ec6168
source-git-commit: f7a5c43a4a4dd6629225f3628a7c592056d6d144
workflow-type: tm+mt
source-wordcount: '242'
ht-degree: 0%

---

# AEM MCPでのカーソルの設定 {#setup-cursor}

AEMのMCP サーバーにCursorを接続するには、次の手順に従います。

* カーソルのMCP設定で、1つ以上のAEM MCP URLを使用して新しいMCP サーバーエントリを作成します。
* プロンプトが表示されたら、Adobe IDで認証します。
* オプションで、ツール名をクリックして、個々のツールを有効または無効にします。 すべてのツールはデフォルトで有効になっています。
* Cursorのエディターまたはチャットを使用して、開発またはコンテンツワークフローの一部としてAEM ツールを呼び出します。

>[!NOTE]
>
>カーソルのユーザーインターフェイスは変更される可能性があり、決定的ではありません。 これらの手順は例示の目的で使用します。

1. **カーソル設定**&#x200B;を開いて、MCP サーバーにカーソルを接続する方法を設定できます。

   ![&#x200B; カーソル設定ダイアログ。](assets/cursor-1.png)

1. **ツールとMCP**&#x200B;を開き、**カスタム MCP**&#x200B;を追加を選択して、カスタム MCP サーバーエントリを開始します。

   ![&#x200B; カスタム MCP サーバーを追加するオプションを含むツールとMCP パネル。](assets/cursor-2.png)

1. カスタム MCP サーバーフォームに、**名前**、AEM MCP **URL** （またはURL）、およびその他の必須フィールドを入力し、**保存**&#x200B;します。

   ![&#x200B; カーソルのカスタム MCP サーバー設定フォーム。](assets/cursor-3.png)

1. 接続ダイアログが表示されたら、**Connect**&#x200B;を押してサインインを完了し、新しいMCP サーバーが承認されるようにします。

   ![&#x200B; カーソル内の新しいMCP サーバーの接続ダイアログ。](assets/cursor-4.png)

1. **チャット**&#x200B;またはエディターで、**AEM ツール**&#x200B;を呼び出すプロンプトを作成し、設定したMCP サーバーがワークフローに参加できるようにします。

   ![新しいAEM MCP サービスを使用するようにカーソルを促しています。](assets/cursor-5.png)
