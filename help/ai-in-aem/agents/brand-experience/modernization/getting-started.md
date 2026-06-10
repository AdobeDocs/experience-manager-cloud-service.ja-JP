---
title: Experience Modernization Agentの概要
description: Experience Modernization Consoleを使用して、Experience Modernization Agentで迅速に生産性を高めるための最初の手順を説明します。
feature: Edge Delivery Services, Agentic AI
role: User, Admin, Developer
exl-id: 612c211e-43bf-47dc-89a8-9995a960e4d7
source-git-commit: c80a2ad29839eaf4d8ad940f9a90d8575e5230f1
workflow-type: tm+mt
source-wordcount: '1208'
ht-degree: 2%

---


# Experience Modernization Agentの概要 {#getting-started}

Experience Modernization AgentとExperience Modernization Consoleの使用を開始するための最初の手順について説明します。

>[!NOTE]
>
>Experience Modernization Consoleの使用に関心がある場合は、アカウントマネージャーを通じてアクセスをリクエストし、スムーズなオンボーディングエクスペリエンスを実現できます。

## Edge Delivery GitHub リポジトリの準備 {#prepare-repo}

>[!NOTE]
>
>AEM Sitesとユニバーサルエディターを使用する場合 [AEM Sites/ユニバーサルエディターの基本を学ぶ](/help/ai-in-aem/agents/brand-experience/modernization/getting-started-aem-authoring.md)の設定手順に従います。

1. Experience Modernization Consoleで使用する[Edge Delivery Services](/help/edge/overview.md) リポジトリを選択します。
   * これは、既存のEdge Delivery Services プロジェクトにすることも、[開発者チュートリアル ](https://www.aem.live/developer/tutorial)に従って、[ ボイラープレートリポジトリを使用して新しいプロジェクトを作成することもできます。](https://github.com/adobe/aem-boilerplate)
1. [AEM Code Connector](https://github.com/apps/aem-code-connector)がリポジトリにインストールされていることを確認します。
   * これにより、コンソールでコードを検査できます。
1. [AEM Code Sync GitHub アプリ ](https://github.com/apps/aem-code-sync)がリポジトリにインストールされていることを確認します。
   * これにより、Edge Delivery Servicesでコードを同期できるようになります。
   * リポジトリがチュートリアルに基づいている場合、この手順はすでに完了しています。

## Experience Modernization Consoleを開きます {#open-console}

1. [`aemcoder.adobe.io`.](https://aemcoder.adobe.io)に移動します
1. Adobe IDでログインします。

## デモモード {#demo-mode}

コンソールは、初めてサインインしたときにデモモードで起動します。 このモードを使用すると、既存のサイトを探索して、追加のページの移行を試すことができます。 画面の下部にあるバナーは、デモモードであることを示します。

![ デモモード ](assets/demo-mode.png)

## サイトを接続 {#connect-repo}

独自のサイトで作業を開始する準備ができたら、独自のプロジェクトに接続してデモモードを終了できます。

1. デモモモモードバナーの「**サイトを切り替え**」をクリックします。
1. これにより、GitHub資格情報を使用してAEM Code Connector アプリを認証するように求められます。 「**AEM Code Connectorの認証**」をクリックします。
1. コンソールに戻り、サイトのプレビューURLを指定します。プレビューURLは、サイト内の任意のドキュメントをプレビューするか、ブランチ、サイト名、組織から作成することで取得できます。関連するGithub プロジェクトが自動的に取得されます。または、承認済みのGitHub プロジェクトを検索してサイトを見つけることもできます。
   ![GitHub プロジェクトへの接続](assets/connect-site-and-github.png)
1. サイトが検証されたら、「**ワークスペースにチェックアウト**」をクリックします。
1. **既存のワークスペースを置換**&#x200B;するように求められた場合は、**ワークスペースを置換**をクリックします。
   ![既存のワークスペースを置き換える](assets/replace-existing-workspace.png)

これで、GitHub プロジェクトとサイトがコンソールに接続されました。

デモモードを終了したが、新しいプロジェクトが接続されていない場合、Experience Modernization エージェントに後日訪問すると、最初にサイトが接続されます。

![ サイト接続](assets/first-sign-on.png)

## コンソールホーム {#console-home}

[aemcoder](https://aemcoder.adobe.io)にアクセスすると、チャットの会話が開始されるまでホームページが表示されます。 ホームページでは、最初のプロンプトを入力するか、提案されたプロンプトのいずれかを選択することで、チャットを始めることができます。

![ コンソール ホーム ](assets/console-home.png)

## プロンプトを開始 {#start-prompting}

コンソールでコードにアクセスできるようになったので、プロンプトを開始する準備が整いました。

1. サイトのコンテンツを読み込むことができます。
   * 「ページ `https://wknd-trendsetters.site`を移行します。」
1. これにより、サイトのコンテンツがインポートされます。
   * コンソールは、関心の分離を監視し、コンテンツとプレゼンテーションを個別に処理します。
   * サイトのコンテンツを最初に読み込むのに、数分かかることがあります。
   * コンソールは、作業を開始する際に、計画された手順の概要を含む継続的なフィードバックを表示します。
     ![ コンテンツの読み込み](assets/content-import.png)
1. サイトが読み込まれると、**Workspace** パネルにページが表示されます。ページを選択して、右側のパネルでプレビューします。
   ![ コンテンツがインポートされました](assets/content-imported.png)
1. コンテンツが用意できたので、同じソースからスタイルを読み込むようにプロンプトを表示できます。
   * 「一般スタイルを`https://wknd-trendsetters.site`から読み込む」
1. 最初のコンテンツの読み込みと同様に、読み込みには数分かかる場合があり、コンソールはリクエストを処理し、スタイルを読み込むときにフィードバックを提供します。タスクが完了したら、右側のパネルで「**プレビューを更新**」をクリックして、スタイル設定されたコンテンツを表示します。
   ![ スタイルがインポートされました](assets/styles-imported.png)

これで、コンテンツとスタイルの両方がコンソールに読み込まれました。

>[!TIP]
>
>[担当者にプロンプトを入力する方法とそのスキルに関する詳細なアイデアについては、プロンプト ガイド ](/help/ai-in-aem/agents/brand-experience/modernization/prompting-guide.md)を参照してください。

## コンテンツのアップロード {#upload-content}

コンテンツを[Document Authoring](https://da.live)にアップロードするには：

1. **コンテンツ** ビューであることを確認し、右上の「**コンテンツをアップロード**」ボタンをクリックします。
   * デフォルトでは、コンソールに入ると&#x200B;**コンテンツ**&#x200B;表示になります。
   * ビューは、コンソールのワークスペース領域で選択したビューピッカー項目で示されます。
1. 「**コンテンツをアップロード**」ダイアログが開き、プロジェクト設定から事前に入力された宛先組織とリポジトリが表示されます。
   * 接続されているリポジトリに`fstab.yaml`が存在しない場合は、**組織**&#x200B;と&#x200B;**リポジトリ**&#x200B;を手動で入力する必要があります。
   * ボイラープレートを使用した場合は、`fstab.yaml`が提供されます。
1. アップロードするファイルを選択し、**アップロード**をクリックします。
   ![ コンテンツダイアログのアップロード ](assets/upload-content.png)
1. コンソールは、「**アップロード**」ボタンを無効にすることで、アップロードプロセスを示します。
1. 完了すると、コンソールの下部に通知が表示されます。
   ![AEMで表示](assets/view-in-aem.png)

Document Authoringでアップロードされたコンテンツにアクセスするには、アップロード完了時に通知の&#x200B;**AEMで表示**&#x200B;をクリックするか、`https://da.live/#/{organization}/{repository}`に移動します。

![ ドキュメント作成中のコンテンツ ](assets/content-in-document-authoring.png)

読み込んだコンテンツがドキュメントのオーサリングに追加されました。

>[!TIP]
>
>AEM Sitesとユニバーサルエディターのプロジェクトを使用している場合、AEMへのコンテンツのアップロードの動作は若干異なります。 具体的なアップロード手順については、[AEM Sites/ユニバーサルエディタープロジェクト向けExperience Modernization Agentの概要](/help/ai-in-aem/agents/brand-experience/modernization/getting-started-aem-authoring.md#upload-content)を参照してください。

## プッシュコードの変更 {#push-code-changes}

コードに加えた変更に満足したら、GitHub リポジトリにプッシュできます。

1. **変更** ビュー（ビューピッカーの分岐アイコン）に切り替えます。
   ![ コードビュー](assets/code-view-git-changes.png)
1. 変更されたファイルのリストで、一部のファイルがトラッキングされていない状態で表示される場合は、`+` ボタンをクリックしてステージングします。
1. 右上の「**プッシュ**」ボタンをクリックします。
1. **変更をプッシュ** ダイアログで、変更を新しいPR （デフォルト）または現在のブランチにプッシュすることを選択し、**確認**&#x200B;をクリックしてプッシュします。
   * 少しでも疑問を感じたら、現在のブランチにプッシュして、問題をスムーズに進めることができます。
1. 完了すると、コンソールの下部に通知が表示されます。
   ![PR](assets/view-pr.png)を表示

GitHubのプッシュされた変更に直接アクセスする場合は、プッシュが完了したら、通知の「**PR**&#x200B;を表示」をクリックします。

GitHub](assets/code-in-github.png)の![ コード

コードはGitHubにあります。

## サイトをプレビュー {#preview-site}

プレビュー環境で変更を表示するには：

1. ドキュメント作成に戻ります。
   * コンテンツをアップロードした後、**AEMで表示**&#x200B;をクリックした後に開いたブラウザータブで、まだ開いている可能性があります。
   * または`https://da.live/#/{organization}/{repository}`に移動します
1. 以前にAEMにアップロードしたページの1つを開きます。
1. 紙面アイコン（右上）をクリックし、**プレビュー**を選択します。
   ![ プレビューに公開](assets/publish-to-preview.png)

おめでとうございます。 移行したコンテンツとスタイルは、AEM プレビュー環境で公開されます。

![公開されたプレビューコンテンツ ](assets/published-preview.png)

コードを`main`以外のブランチにプッシュした場合、Document Authoringから開いたプレビューにはスタイルが表示されません。 プレビューのURLを更新してブランチに変更すると、スタイルを確認できます。

## トラブルシューティング {#troubleshooting}

### ・IP アドレスの許可リストに加える {#allowlist-ip-addresses}

サイトがファイアウォールやアクセス制限の内側にある場合は、バックエンドサービスがサイトをスクレイピングできるように、次のIP アドレスを許可リストに加えるできます。

* `34.228.136.112`
* `54.90.51.39`
* `3.224.194.242`

## その他のリソース {#additional-resources}

Experience Modernization エージェントとそのコンソールを引き続き検索する場合は、次のドキュメントが役立つ可能性があります。

* [Experience Modernization Console](/help/ai-in-aem/agents/brand-experience/modernization/console.md) - コンソールの詳細、ビュー、オプション、機能
* [Experience Modernization Agentのプロンプトガイド ](/help/ai-in-aem/agents/brand-experience/modernization/prompting-guide.md) - エージェントをプロンプトする方法とそのスキルの活用方法に関するアイデア
* [Edge Delivery Services開発者向けチュートリアル ](https://www.aem.live/developer/tutorial) - AEMおよびEdge Delivery Services プロジェクトを初めて使用する場合に役立ちます
* [ ドキュメント オーサリング ](https://da.live) - コンテンツ管理のドキュメント オーサリングを初めて使用する場合に役立ちます
