---
title: AEM オーサリングプロジェクト用Experience Modernization Agentの概要
description: Experience Modernization Consoleを使用してExperience Modernization Agentを使用し始める際に、AEM オーサリングプロジェクトに必要な特定の設定手順について説明します。
feature: Edge Delivery Services, Agentic AI
role: User, Admin, Developer
exl-id: 94a5e40b-af4a-42ed-922b-b1ec9bb82e24
source-git-commit: 7b880e6d776e2eb9c53cef4552b876b051bdc7ba
workflow-type: tm+mt
source-wordcount: '630'
ht-degree: 1%

---

# AEM オーサリングプロジェクト用Experience Modernization Agentの概要 {#getting-started-aem-authoring}

ユニバーサルエディターを使用するAEM オーサリングプロジェクトの場合、Experience Modernization Agentの準備は、標準のEdge Delivery フローとは異なります。 このドキュメントでは、これらの設定の違いについて説明します。 以下の手順が完了したら、メインの[Experience Modernization Agentの概要](getting-started.md) ガイドに従います。

## Edge Delivery Services プロジェクトリポジトリの作成 {#create-repo}

1. [`aem-block-collection-xwalk`](https://github.com/adobe-rnd/aem-block-collection-xwalk) リポジトリをテンプレートとして使用します（標準のEdge Delivery Services ボイラープレートではありません）。
1. `fstab.yaml`がAEM ホスト、Git オーナー、Git リポジトリを指していることを確認し、GitHub アプリを接続する前に`main`に変更をコミットします。
   * 手順については、[ コンテンツソースの設定](/help/implementing/cloud-manager/edge-delivery/configure-content-source.md)を参照してください。
1. [ ユニバーサルエディターのチュートリアル ](https://www.aem.live/developer/ue-tutorial)に従って、リポジトリを設定します。
   * AEMでサイトの作成を求められたら停止します。
1. `paths.json`を削除し、この変更を`main`にコミットします。
1. [AEM Code Connector](https://github.com/apps/aem-code-connector/installations/select_target) アプリをリポジトリに追加します。
   * これにより、コンソールでコードを検査できます。

## AEMでの新しいサイトの作成 {#create-site}

1. AEM Sites コンソールで、テンプレート **から** Create **>** Siteを選択します。
1. Edge Delivery Services テンプレートを含む&#x200B;**AEM サイト**&#x200B;を選択します。
   * 一覧に表示されていないか [ テンプレートをインストールします。](https://github.com/adobe-rnd/aem-boilerplate-xwalk/releases)
1. 指定されたとおりに、サイトの&#x200B;**name**&#x200B;を保持します（タイトルではありません）。
   * サイト名が一意のIDとして使用されます。
   * タイトルは表示用に変更できます。
1. 「**作成**」をクリックします。
   * サイトページにリダイレクトされます。
   * 新しいサイトがすぐに表示されない場合は、ページを更新します。

## 標準の入門ステップに進む {#continue}

上記の手順が完了したら、標準の入門ガイドに進んで、コンテンツの移行を開始できます。

![ コンテンツの読み込み](assets/content-import.png)

標準ガイドの手順に従います。

1. [Edge Delivery GitHub リポジトリの準備](/help/ai-in-aem/agents/brand-experience/modernization/getting-started.md#prepare-repo)
1. [Experience Modernization Consoleを開きます](/help/ai-in-aem/agents/brand-experience/modernization/getting-started.md#open-console)
1. [GitHub リポジトリへの接続](/help/ai-in-aem/agents/brand-experience/modernization/getting-started.md#connect-repo)
1. [プロンプトを開始](/help/ai-in-aem/agents/brand-experience/modernization/getting-started.md#start-prompting)

![ コンテンツがインポートされました](assets/content-imported-aem-authoring.png)

これらの手順を完了してコンテンツを移行したら、次の手順に進みます。

## コンテンツを検証 {#validate-content}

プレビューパネルで、選択したページのコンテンツを検証します。 エラーは、**エラー** ボタンをクリックすると表示されます。
エージェントとのチャット会話を続行して、エラーを修正します。 **チャットに追加**&#x200B;機能を使用して、ページ、パーサーファイル、またはトランスフォーマーファイルの特定の要素に修正を適用します。

![ コンテキストチャット ](assets/contextual-chat.png)

## コンテンツのアップロード {#upload-content}

AEMにコンテンツをアップロードするには：

1. **コンテンツ**&#x200B;表示になっていることを確認し、右上の「**コンテンツをアップロード**」ボタンをクリックします。
1. **コンテンツパッケージを作成** ダイアログで、パッケージに含めるページを選択します。
   * オプションで&#x200B;**パッケージ名**&#x200B;を入力します（空のままにした場合、デフォルトはサイト名）。
   * **すべてを選択**、**選択範囲をクリア**、**すべてを展開**&#x200B;または&#x200B;**すべてを折りたたむ**&#x200B;を使用して、リストを管理します。
1. 「**パッケージを作成**」をクリックします。

   ![ コンテンツパッケージの作成 – ページを選択して作成](assets/content-package.png)

1. パッケージを作成すると、**コンテンツパッケージをアップロード** ダイアログにパッケージの準備ができたことが表示されます。
   1. **パッケージをダウンロード**&#x200B;してローカルに保存するか、アップロードに進むことができます。
   1. 「**AEMにアップロード**」で、**AEM サイト**&#x200B;および&#x200B;**AEM ホスト** （プロジェクト設定から事前入力）を確定します。
      * オプションで、**画像をアップロード**&#x200B;にチェックを入れたままにして、画像を含めます。
   1. 「**AEMにアップロード**」をクリックします。

   ![ パッケージをAEMにアップロードまたはダウンロードする準備ができました](assets/upload-package-start.png)

1. ページとアセットがAEMに送信されると、ダイアログにアップロードの進行状況が表示されます。 アップロードが完了すると、成功メッセージとアップロードログが表示されます。 ダイアログを閉じるには、**閉じる**&#x200B;をクリックします。

   ![AEMで進行状況と完了状況をアップロード ](assets/upload-package-complete.png)

読み込んだコンテンツはAEMに保存されています。 メイン入門ガイドの[ プッシュコードの変更](getting-started.md#push-code-changes)で続行します。

## その他のリソース {#additional-resources}

* [Experience Modernization Agentの概要](getting-started.md) - コンソール、プロンプト、アップロード、プレビューなどの完全なワークフロー
* [Experience Modernization Console](console.md) - コンソール リファレンス
* [ ユニバーサルエディターのチュートリアル ](https://www.aem.live/developer/ue-tutorial) - AEM オーサリングおよびユニバーサルエディタープロジェクトの設定
* [`aem-block-collection-xwalk`](https://github.com/adobe-rnd/aem-block-collection-xwalk) - AEM オーサリングおよびユニバーサルエディタープロジェクト用のテンプレートリポジトリ
