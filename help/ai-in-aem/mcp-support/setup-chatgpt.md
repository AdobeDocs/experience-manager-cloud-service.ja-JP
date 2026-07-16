---
title: AEM MCPを使用したOpenAI ChatGPTの設定
description: AEM MCP サーバーに接続するようにOpenAI ChatGPTを設定する方法を説明します
feature: Edge Delivery Services, Agentic AI
role: User, Admin, Developer
exl-id: 1f116225-168b-483c-9df6-c752a573b57b
source-git-commit: e5eceb1e540a85aab03b7b856af36276291745f6
workflow-type: tm+mt
source-wordcount: '614'
ht-degree: 0%

---

# AEM MCPを使用したOpenAI ChatGPTの設定 {#setup-chatgpt}

この記事では、AEMでOpenAI ChatGPTを使用する2つの異なる方法について説明します。

- ChatGPTで1つ以上のAEMのMCP サーバーを手動で設定します（[MCPとAEM as a Cloud Serviceの使用 – MCP サーバー](/help/ai-in-aem/mcp-support/using-mcp-with-aem-as-a-cloud-service.md#mcp-servers)で説明されているサーバー）。
- ChatGPT プラグインマーケットプレイスからAdobe Experience Manager プラグインをインストールします。 現在、Content MCP Serverと同等の機能を備えており、AEMのMCP サーバーで利用可能なツールのサブセットを拡大する予定です。

## ChatGPTでAEMのMCP サーバーを手動で設定する {#manual-configure-aems-mcp-servers-in-chatgpt}

この節では、**手動設定**&#x200B;のアプローチについて説明します。このアプローチでは、1つ以上のAEM MCP サーバーをカスタムアプリまたはコネクタとしてChatGPTに追加します。

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

   ![ChatGPTのアプリとコネクタの詳細設定パネル ](assets/chatgpt-2.png)

1. **アプリとコネクタ**&#x200B;で&#x200B;**開発者モード**&#x200B;を有効にして、カスタムプラグインを追加および設定できるようにします。

   ![ アプリとコネクタ セクションで開発者モードを有効にしています。](assets/chatgpt-3.png)

1. **新しいアプリを作成** （または同等のコントロール）を開始して、AEM MCP サーバーのアプリエントリを追加します。

   ![ChatGPTで新しいアプリを作成するためのダイアログ。](assets/chatgpt-4.png)

1. **新しいアプリ** フォームに入力します。例えば、アプリに名前を付け、AEM MCP サーバーのURLおよびその他の必須フィールドを入力してから、**保存**&#x200B;します。

   ![ChatGPTの新しいアプリ設定フォーム。](assets/chatgpt-5.png)

1. **アプリとコネクタ**&#x200B;に&#x200B;**AEM Content MCP Service** （または設定済みのアプリ）が表示されていることを確認して、ChatGPTで使用できるようにします。

   ![ アプリとコネクタにリストされているAEM Content MCP サービス。](assets/chatgpt-6.png)

1. チャットで、設定された&#x200B;**AEM ツール**&#x200B;を使用するようにChatGPTに指示するプロンプトを書きます（例えば、作成者のコンテンツやサイトを照会します）。

   ![ChatGPTにAEM Content MCP サービスの使用を促しています。](assets/chatgpt-7.png)

## Adobe Experience Manager プラグイン（ChatGPT プラグインマーケットプレイス）のインストール {#install-adobe-experience-manager-plugin}

この節では、ChatGPT プラグインマーケットプレイスの&#x200B;**インストール可能なプラグイン**&#x200B;について説明します（カスタム MCP サーバーURLを追加するのではなく）。 これには、AEMのMCP サーバーで使用可能なツールのサブセットが含まれます。

>[!NOTE]
>
>OpenAI ChatGPT ユーザーインターフェイスは変更される可能性があり、決定的ではありません。 これらの手順は例示の目的で使用します。

Adobe Experience Manager プラグインには、次の2つの方法があります。 どちらか便利なものを使用してから、次のサインインステップに進みます。

**オプション 1: プラグインページを直接開く**

[https://chatgpt.com/plugins/plugin_asdk_app_6a35d3c1258081919c084a1fd22cd02d](https://chatgpt.com/plugins/plugin_asdk_app_6a35d3c1258081919c084a1fd22cd02d)に移動し、**プラグインのインストール**&#x200B;を選択します。

![ プラグインのインストール ボタンが表示されているAdobe Experience Manager プラグイン ページ。](assets/chatgpt-plugin-install.png)

**オプション 2: マーケットプレイスでプラグインを検索する**

1. **設定**&#x200B;から「**プラグイン**」を選択し、リストの下部にある「**プラグインを参照**」を選択します。

   ![参照プラグインを使用したChatGPT設定のプラグインページ。](assets/chatgpt-plugin-1.png)

1. **Adobe Experience Manager**&#x200B;を検索し、選択します。

   ![ プラグインマーケットプレイスでAdobe Experience Manager プラグインを検索しています。](assets/chatgpt-plugin-2.png)

**ログインして確認**

上記のいずれかのオプションを使用してプラグインを見つけるかインストールしたら、接続を完了します。

1. 「**Adobe Experience Managerでログイン**」を選択し、リダイレクト時にAEMにログインします。

   ![Adobe Experience Managerでログインした状態でAdobe Experience ManagerをChatGPTに追加ダイアログ。](assets/chatgpt-plugin-3.png)

1. 緑色のバナーを確認すると、Adobe Experience Managerが接続されていることを示します。

   ![Adobe Experience Manager プラグインを確認する緑色のバナーが接続されています。](assets/chatgpt-plugin-4.png)
