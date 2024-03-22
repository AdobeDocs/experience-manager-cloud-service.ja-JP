---
title: Edge Delivery Services を使用した AEM オーサリングの開発者向け入門ガイド
description: このガイドでは、Edge Delivery Services とコンテンツオーサリング用のユニバーサルエディターを使用して、新しい Adobe Experience Manager サイトを導入および実行する方法について説明します
feature: Edge Delivery Services
exl-id: a71184a7-c954-442e-b276-99edc6d2acd8
source-git-commit: bae9a5178c025b3bafa8ac2da75a1203206c16e1
workflow-type: tm+mt
source-wordcount: '989'
ht-degree: 95%

---

# Edge Delivery Services を使用した AEM オーサリング {#edge-dev-getting-started}

このガイドでは、Edge Delivery Services とコンテンツオーサリング用のユニバーサルエディターを使用して、新しい Adobe Experience Manager サイトを導入および実行する方法について説明します。

{{aem-authoring-edge-early-access}}

## 前提条件 {#prerequisites}

このガイドを始める前に、Edge Delivery Services に関する基本事項を理解し、Edge Delivery Services にアクセス可能な状態にしておく必要があります。次の項目について確認してください。

* [Edge Delivery Service のチュートリアル](/help/edge/developer/tutorial.md)を完了していること。
* [AEM Cloud Service サンドボックス](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/introduction-sandbox-programs.md)にアクセスできること。
* [同じサンドボックス環境でユニバーサルエディターが有効になっている](/help/implementing/universal-editor/getting-started.md)こと。

## 適切なエディタを選択 {#editor-choice}

AEM には 2 種類の異なるコンテンツエディターが用意されており、状況に応じて、適切なコンテンツエディターを選択して使用します。

* **ユニバーサルエディター** - 新しいサイトのデフォルトの選択肢です。
* **AEM ページエディター** - 既存の AEM Sites から Edge Delivery Services に移行する場合に選択します。　

このガイドでは、ユニバーサルエディターを活用して、Edge Delivery Services を使用した AEM プロジェクトに焦点を当てます。適切なエディターの選択および既存の AEM Sites の Edge Delivery Services への移行について詳しくは、[Edge Delivery Services 向けの開発](/help/edge/developing.md)ドキュメントを参照してください。

## AEMオーサリングの概要とEdge Delivery Services {#getting-started}

[前提条件](#prerequisites)を満たし、[ユニバーサルエディターの使用を選択](#editor-choice)したら、独自のプロジェクトを開始できます。

### GitHub プロジェクトを作成 {#create-github-project}

まず、アドビのテンプレートに基づいて、GitHub に新しいプロジェクトを作成する必要があります。

1. [`https://github.com/adobe-rnd/aem-boilerplate-xwalk`](https://github.com/adobe-rnd/aem-boilerplate-xwalk) に移動して「**このテンプレートを使用**」をクリックし、「**新しいリポジトリを作成**」を選択します。

   * このオプションを表示するには、GitHub にログインする必要があります。

   ![リポジトリプロジェクトをコピー](assets/edge-dev-getting-started/use-template-project.png)

1. デフォルトでは、リポジトリが割り当てられます。必要に応じてこれを変更し、リポジトリの名前と説明を入力して、「**リポジトリを作成**」をクリックします。

   ![リポジトリの作成](assets/edge-dev-getting-started/create-repo.png)

1. 同じブラウザーの新しいタブで [`https://github.com/apps/aem-code-sync`](https://github.com/apps/aem-code-sync) に移動し、「**設定**」をクリックします。

   ![Code Sync](assets/edge-dev-getting-started/configure-code-sync.png)

1. 前の手順で新しいリポジトリを作成した組織の「**設定**」をクリックします。

   ![Code Sync の組織の選択](assets/edge-dev-getting-started/code-sync-org.png)

1. AEM Code Sync GitHub ページの&#x200B;**リポジトリアクセス**&#x200B;の下で、「**リポジトリのみを選択**」を選択し、前の手順で作成したリポジトリを選択して、「**保存**」をクリックします。

   ![AEM Code Sync アクセス権の付与](assets/edge-dev-getting-started/grant-code-sync-acces.png)

1. AEM Code Sync がインストールされると、確認画面が表示されます。新しいリポジトリの「ブラウザー」タブに戻ります。

   ![Code Sync のインストールの確認](assets/edge-dev-getting-started/confirmation.png)

1. `fstab.yaml` ファイルをクリックして開き、次に、「**このファイルを編集**」アイコンをクリックしてファイルを編集します。

   ![fstab.yaml](assets/edge-dev-getting-started/fstab.png)

1. `fstab.yaml` ファイルを編集して、プロジェクトのマウントポイントを更新します。デフォルトの Google ドキュメント URL を AEM as a Cloud Service オーサリングインスタンスの URL に置き換えて、「**変更をコミット...**」をクリックします。

   * `https://<aem-author>/bin/franklin.delivery/<owner>/<repository>/main`
   * マウントポイントを変更すると、Edge Delivery Services がサイトのコンテンツの場所を特定します。

   ![fstab の更新](assets/edge-dev-getting-started/fstab-update.png)

1. 必要に応じてコミットメッセージを追加し、「**変更をコミット**」をクリックして、変更を `main` 分岐に直接コミットします。

   ![変更のコミット](assets/edge-dev-getting-started/commit-fstab-changes.png)

1. リポジトリのルートに戻り、`paths.yaml` をクリックして、「**このファイルを編集**」アイコンをクリックします。

   ![paths.yaml](assets/edge-dev-getting-started/paths.png)

1. デフォルトのマッピングを `/content/<site-name>/:/` に置き換え、「**変更をコミット…**」をクリックします。

   * 独自の `<site-name>` を入力します。後の手順で必要になります。
   * マッピングは、Edge Delivery Services に対して、AEM リポジトリ内のコンテンツをサイトの URL にマッピングする方法を指示します。

   ![paths.yaml の更新](assets/edge-dev-getting-started/paths-update.png)

1. 必要に応じてコミットメッセージを追加し、「**変更をコミット**」をクリックして、変更を `main` 分岐に直接コミットします。

   ![変更のコミット](assets/edge-dev-getting-started/commit-fstab-changes.png)

### 新しい AEM サイトの作成と編集 {#create-aem-site}

GitHub プロジェクトが完成したら、プロジェクトで使用できる新しい AEM サイトを作成する必要があります。

>[!NOTE]
>
>ユニバーサルエディターを使用してサイトを編集するには、Chromium ベースのブラウザーを使用する必要があります。

1. [プロジェクトの Slack チャネル](/help/edge/docs/slack.md)経由で、アドビのエンジニアリングからの最新の Edge Delivery Services を使用した AEM オーサリングサイトテンプレートをリクエストします。

1. AEM as a Cloud Service オーサリングインスタンスにログインし、サイトコンソールに移動して、**作成**／**テンプレートからサイト**&#x200B;をタップまたはクリックします。

   ![コンソールから新しいサイトを作成](assets/edge-dev-getting-started/create-site-console.png)

1. サイトの作成ウィザードの「**サイトテンプレートを選択**」タブで、「**読み込み**」ボタンをクリックして、新しいテンプレートを読み込みます。

   ![テンプレートの読み込み](assets/edge-dev-getting-started/site-templates.png)

1. アドビのエンジニアリングから提供される Edge Delivery Services を使用した AEM オーサリングサイトテンプレートをアップロードします。

1. テンプレートが読み込まれると、ウィザードに表示されます。タップまたはクリックして選択し、「**次へ**」をタップまたはクリックします。

   ![テンプレートを選択](assets/edge-dev-getting-started/select-template.png)

1. 次のフィールドを入力し、「**作成**」をタップまたはクリックします。

   * **サイトのタイトル** - サイトを説明するタイトルを追加します。
   * **サイトのタイトル** - [前の手順](#create-github-project)で定義した `<site-name>` を使用します。
   * **GitHub URL** - 前の手順で作成した GitHub プロジェクトの URL を使用します。

   ![サイトの詳細](assets/edge-dev-getting-started/create-site-details.png)

1. AEM にダイアログが表示され、サイトの作成を確認します。「**OK**」をタップまたはクリックして閉じます。

   ![サイトの作成の確認](assets/edge-dev-getting-started/site-creation-confirmation.png)

1. サイトコンソールで、新しく作成したサイトの `index.html` に移動し、ツールバーの「**編集**」をタップまたはクリックします。

   ![新しいサイトの編集](assets/edge-dev-getting-started/new-site.png)

1. ユニバーサルエディターが新しいタブで開きます。ページを編集するには、「**アドビでログイン**」をタップまたはクリックして認証する必要がある場合があります。

   ![ユニバーサルエディター](assets/edge-dev-getting-started/universal-editor.png)

これで、ユニバーサルエディターを使用してサイトを編集できます。詳しくは、[ユニバーサルエディターのドキュメント](/help/sites-cloud/authoring/universal-editor/authoring.md)を参照してください。

### 新しいサイトの公開 {#publishing}

ユニバーサルエディターを使用して新しいサイトの編集が完了したら、コンテンツを公開できます。

1. サイトコンソールで、新しいサイト用に作成したすべてのページを選択し、ツールバーの「**クイック公開**」をタップまたはクリックします。

   ![公開するページの選択](assets/edge-dev-getting-started/publishing.png)

1. 確認ダイアログで「**公開**」をタップまたはクリックして、プロセスを開始します。

   ![公開ダイアログ](assets/edge-dev-getting-started/publish-confirmation.png)

1. 同じブラウザーで新しいタブを開き、新しいサイトの URL に移動します。

   * `https://main--<site-name>--<owner>.hlx.page`

1. 公開されたコンテンツを確認します。

   ![公開されたコンテンツ](assets/edge-dev-getting-started/published-site.png)

## 次の手順 {#next-steps}

これで、Edge Delivery Servicesプロジェクトを使用したAEMの作業が完了し、独自のブロックの作成とスタイル設定を開始できます。

ガイドを参照してください [ユニバーサルエディタで使用するためのブロックの作成](/help/edge/create-block.md) を参照してください。
