---
title: ユニバーサルエディターでのAEM FormsのEdge Delivery Servicesの概要 – 開発者向けチュートリアル
description: このチュートリアルは、新しい Adobe Experience Manager Forms（AEM）プロジェクトを起動および実行するのに役立ちます。 10 分から 20 分で、ユニバーサルエディターで独自のEdge Delivery Services Formsを作成できました。
feature: Edge Delivery Services
role: Admin, Architect, Developer
hide: true
hidefromtoc: true
source-git-commit: c27b8e413c060de601a72a669d86c4add2a4167d
workflow-type: tm+mt
source-wordcount: '1623'
ht-degree: 23%

---


# ユニバーサルエディターを使用したAEM FormsのEdge Delivery Servicesの概要（WYSIWYG）

今日のデジタル時代には、すべての組織にとって使いやすいフォームが不可欠です。 Edge Delivery ServicesFormsは、WYSIWYG（見たままが得られる）機能を提供するユニバーサルエディターを使用して作成されます。 これは、効率的なフォームオーサリングのための最新の直感的なインターフェイスを提供します。

AEM Formsには、データを取得および保存するためのEdge Delivery Services Formsを簡単に作成できるアダプティブ Forms ブロックが用意されています。 [ アダプティブFormsブロックで事前設定された新しいAEM プロジェクトを作成する ](#create-a-new-aem-project-pre-configured-with-adaptive-forms-block) または [ アダプティブFormsブロックを既存のAEM プロジェクトに追加する ](#add-adaptive-forms-block-to-your-existing-aem-project) ことができます。

このチュートリアルでは、ユニバーサルエディターのWYSIWYG オーサリングを使用して、新規または既存のAdobe Experience Manager サイトプロジェクトで独自のフォームを作成、プレビューおよび公開する手順について説明します。


## 前提条件

* GitHub アカウントを持っており、Git の基本を理解している。
* Google または Microsoft SharePoint アカウントを持っている。
* HTML、CSS、JavaScript の基本を理解している。
* ローカル開発用の Node/npm がインストールされている。

## アダプティブフォームブロックを使用した設定済みの新しい AEM プロジェクトの作成

AEM Forms ボイラープレートテンプレートを使用すると、Adaptive Forms ブロックで設定済みの AEM プロジェクトをすぐに開始できます。 これは、AEMのベストプラクティスに従ってフォームを作成する最もすばやく簡単な方法です。

### AEM Forms ボイラープレートリポジトリテンプレートの基本を学ぶ

1. AEM プロジェクトの GitHub リポジトリを作成します。 リポジトリを作成するには：
   1. [https://github.com/adobe-rnd/aem-boilerplate-forms](https://github.com/adobe-rnd/aem-boilerplate-forms) に移動します。

      ![AEM Forms ボイラープレート](/help/edge/docs/forms/assets/eds-form-boilerplate.png)
   1. 「**このテンプレートを使用**」オプションをクリックし、「**新しいリポジトリを作成**」オプションを選択します。

      ![AEM Forms ボイラープレートを使用して新しいリポジトリを作成](/help/edge/docs/forms/assets/use-eds-form-template.png)

      **新しいリポジトリを作成** 画面が開きます。

   1. **新しいリポジトリを作成** 画面で、**所有者** を選択し、**リポジトリ名** を指定します。 Adobeは、リポジトリを **公開** に設定することをお勧めします。 したがって、「**パブリック**」オプションを選択し、「**リポジトリを作成**」をクリックします。

      ![リポジトリをパブリックに設定](/help/edge/docs/forms/assets/name-eds-repo.png)

1. AEM Code Sync GitHub アプリをリポジトリにインストールします。 インストールするには：
   1. [https://github.com/apps/aem-code-sync/installations/new](https://github.com/apps/aem-code-sync/installations/new) に移動します。
   1. **AEM コード同期のインストール** 画面で、「**リポジトリのみを選択**」オプションを選択し、新しく作成したリポジトリを選択します。 「**保存**」をクリックします。

   ![リポジトリをパブリックに設定](/help/edge/docs/forms/assets/aem-code-sync-up.png)

1. 次に、AEM Forms Boilerplate を使用して作成した GitHub リポジトリを、AEM プロジェクトのオーサリング環境にリンクします。 接続する手順は、次のとおりです。

   1. AEM Forms ボイラープレートを使用して以前に作成した GitHub リポジトリに移動します。
   1. **fstab.yaml** ファイルを開いて編集します。

      ![fstab.yaml ファイルを開きます ](/help/edge/docs/forms/assets/open-fstab.png)

   1. **fstab.yaml** ファイルを編集して、プロジェクトのマウントポイントを更新します。 この URL をAEM as a Cloud Service オーサリングインスタンスの URL に置き換えます。
      `https://<aem-author>/bin/franklin.delivery/<owner>/<repository>/main`

      ![fstab.yaml ファイルを編集 ](/help/edge/docs/forms/assets/edit-fstab-file.png)

   1. 参照を更新したら、更新した **fstab.yaml** ファイルをコミットすると、問題なく表示されます。

      ![ 変更をコミットする ](/help/edge/docs/forms/assets/commit-fstab-changes.png)

      ビルドの問題が発生した場合は、[GitHub ビルド問題のトラブルシューティング](#troubleshooting-github-build-issues)を参照してください。

### 新規AEM プロジェクトを作成します。

これで GitHub プロジェクトが作成されたので、次に、AEM as a Cloud Service オーサリングインスタンスで新しいAEM プロジェクトを作成して公開できます。
1. 新しいAEM プロジェクトを作成するには：

   1. AEM as a Cloud Service オーサーインスタンスにログインし、「**Sites**」を選択します。

      ![ サイトを選択 ](/help/edge/assets/select-sites.png)

   1. **作成**/**テンプレートからのサイト** をクリックします。

      ![create-sites](/help/edge/docs/forms/assets/create-sites.png)

   1. Edge Delivery Servicesサイト テンプレートを選択して、「**次へ**」をクリックします。

      ![select-site-template](/help/edge/docs/forms/assets/select-site-template.png)

      >[!NOTE]
      >
      > * オーサーインスタンスでEdge Delivery Services サイトテンプレートが使用できない場合は、「読み込み」ボタンをクリックしてテンプレートをアップロードします。
      > * Edge Delivery Servicesのサイトテンプレートは、[GitHub](https://github.com/adobe-rnd/aem-boilerplate-xwalk/releases) からダウンロードできます。

   1. 新しいAEM プロジェクトを作成するには、次の詳細を入力します。
      * **サイトのタイトル** - サイトを説明するタイトルを追加します。
      * **サイトのタイトル** – 前の手順で定義した `site-name` を使用します。
      * **GitHub URL** - 前の手順で作成した GitHub プロジェクトの URL を使用します。

      ![AEM サイトの作成 ](/help/edge/docs/forms/assets/create-aem-site.png)

   1. **サイトを作成** ダイアログが表示されるので、「**OK**」をクリックします。

      ![[ok] をクリック ](/help/edge/docs/forms/assets/click-ok-aem-site.png)

      新しいAEM プロジェクトが数分で作成されます。

   1. Sites コンソールで新しく作成したAEM プロジェクトに移動し、「**編集**」をクリックします。
この場合、`index.html` ページが説明用に使用されます。

      ![AEM サイトを編集 ](/help/edge/docs/forms/assets/edit-site.png)

      AEM プロジェクトがユニバーサルエディターの新しいタブで開き、WYSIWYGのオーサリングが可能になります。 これで、AEM プロジェクトを編集できます。

      ![ ユニバーサルエディターでサイトが開く ](/help/edge/docs/forms/assets/site-in-universal-editor.png)

1. 作成したAEM プロジェクトのPublish

   AEM プロジェクトの編集が完了したら、そのプロジェクトを公開します。 パブリッシュするには：

   1. Sites コンソールで、AEM プロジェクトページをすべて選択して、「**クイックPublish**」をクリックします。

      ![AEM Sites プロジェクトの公開 ](/help/edge/docs/forms/assets/publish-sites.png)

   1. **クイックPublish** 確認ダイアログが表示されるので、**Publish** をクリックして公開プロセスを開始します。

      ![ クイックPublishの確認ダイアログ ](/help/edge/docs/forms/assets/quick-publish.png)

      または、ユニバーサルエディターのユーザーインターフェイスから直接AEM プロジェクトページを公開することもできます。

      ![ クイックPublishの確認ダイアログ ](/help/edge/docs/forms/assets/qui.png)

   これで完了です。 `https://<branch>--<repo>--<owner>.aem.page/content/<site-name>/` で新しい web サイトを実行しています。

   * `<branch>` は、GitHub リポジトリのブランチを指します。
   * `<repository>` は GitHub リポジトリを示します。
   * `<owner>` は、GitHub リポジトリをホストする GitHub アカウントのユーザー名を指します。
   * `<site-name>` は、作成したサイト名の名前を指します。

   例えば、ブランチ名が `main`、リポジトリが `edsforms`、所有者が `wkndforms`、`site-name` が `eds-forms` の場合、web サイトは `https://main--edsforms--wkndforms.aem.page/content/eds-forms/` で稼働します。

   >[!NOTE]
   >
   > * AEM プロジェクトの `index.html` ページを表示するには、次の URL を使用します。`https://<branch>--<repo>--<owner>.aem.page/content/<site-name>/`
   > * AEM プロジェクトの `index page` 以外のページを表示するには、次の URL を使用します。`https://<branch>--<repo>--<owner>.aem.page/content/<site-name>/<site-page-name>`

これで、[ フォームの作成とAEM プロジェクトへの追加 ](#add-edge-delivery-services-forms-to-aem-project) を開始できます。

## 既存のAEM プロジェクトへのアダプティブFormsブロックの追加

既存の AEM プロジェクトがある場合は、アダプティブフォームブロックを現在のプロジェクトに統合して、フォームの作成を開始できます。

>[!NOTE]
>
>
> この手順は、[AEM ボイラープレート](https://github.com/adobe-rnd/aem-boilerplate-xwalk)を使用して作成したプロジェクトに適用されます。 [AEM Forms ボイラープレート](https://github.com/adobe-rnd/aem-boilerplate-forms)を使用して AEM プロジェクトを作成した場合は、この手順をスキップできます。

統合するには：

1. アダプティブ Forms ブロック GitHub リポジトリ：[https://github.com/adobe-rnd/aem-boilerplate-forms](https://github.com/adobe-rnd/aem-boilerplate-forms) をコンピューターに複製します。
1. ダウンロードしたフォルダー内で `blocks/form` フォルダーを見つけて、このフォルダーをコピーします。
1. AEM プロジェクトの GitHub リポジトリをコンピューターにクローンします。
1. 次に、ローカルのAEM プロジェクトリポジトリ内の `blocks` フォルダーに移動して、コピーしたフォームフォルダーをそこに貼り付けます。
1. これらの変更をコミットして GitHub のAEM プロジェクトリポジトリにプッシュします。

これで作業は完了です。 これで、アダプティブ Forms ブロックがAEM プロジェクトの一部になりました。 [ フォームの作成を開始し、AEM プロジェクトに追加する ](#add-edge-delivery-services-forms-to-aem-site-project) ことができます。

## WYSIWYGを使用したAEM Formsのオーサリング

WYSIWYG オーサリング用のユニバーサルエディターでAEM プロジェクトを開き、プロジェクトを編集して「アダプティブフォーム」セクションを追加し、AEM プロジェクトページにEdge Delivery Servicesフォームを含めることができます。

1. 「アダプティブフォーム」セクションをAEM プロジェクトページに追加します。 次の手順を追加します。
   1. Sites コンソールでAEM プロジェクトに移動し、**編集** をクリックします。 ユニバーサルエディターでAEM プロジェクトページが開き、編集できます。
この場合、`index.html` ページが説明用に使用されます。
   1. コンテンツツリーを開き、アダプティブフォーム セクションを追加する場所に移動します。
   1. **[!UICONTROL 追加]** アイコンをクリックし、コンポーネントリストから **[!UICONTROL アダプティブフォーム]** コンポーネントを選択します。

   ![ コンテンツツリー ](/help/edge/docs/forms/assets/add-adaptive-form-block.png)

   アダプティブフォーム セクションが指定された場所に追加されます。 これで、フォームコンポーネントのAEM プロジェクトページへの追加を開始できます。

1. 追加したアダプティブフォーム セクションにフォームコンポーネントを追加します。 フォームコンポーネントを追加するには：
   1. コンテンツツリーで、追加したアダプティブフォーム セクションに移動します。

      ![ 追加されたアダプティブフォームブロック ](/help/edge/docs/forms/assets/adative-form-block.png)


   1. **[!UICONTROL 追加]**&#x200B;アイコンをクリックし、**アダプティブフォームコンポーネント**&#x200B;リストから目的のコンポーネントを追加します。

      ![ コンポーネントを追加 ](/help/edge/docs/forms/assets/add-component.png)

      ユニバーサルエディターには直感的なドラッグ&amp;ドロップ機能があるので、必要なアダプティブ Forms コンポーネントをドラッグ&amp;ドロップすることもできます。

   1. 追加されたアダプティブフォームコンポーネントを選択し、**[!UICONTROL プロパティ]** を使用してプロパティを更新します。

      ![ プロパティを開く ](/help/edge/docs/forms/assets/component-properties.png)

      以下のスクリーンショットは、WYSIWYG オーサリングを使用してAEM プロジェクトで作成されたフォームを示しています。

      ![ 追加されたフォーム ](/help/edge/docs/forms/assets/added-form-aem-sites.png)

   >[!NOTE]
   >
   > 変更を加えた後、AEM プロジェクトページを再度公開することが重要です。そうしないと、更新内容がブラウザーに表示されません。

1. AEM プロジェクトページを再公開します。

   1. フォームを追加した後、**Publish** をクリックしてAEM プロジェクトページを再度公開します。

      ![ フォームを公開 ](/help/edge/docs/forms/assets/publish-form.png)

   1. 画面に **Publish** の確認ダイアログが表示されるので、**Publish** をクリックして公開を開始します。

      ![publish form1](/help/edge/docs/forms/assets/publish-form1.png)

      「**Publish**」ボタンをクリックすると、`Publish started successfully` メッセージが表示されます。

      ![publish form2](/help/edge/docs/forms/assets/publish-form2.png)

   次の URL に、追加されたEdge Delivery Servicesフォームを含むAEM プロジェクトページが表示されるようになりました。
   `https://<branch>--<repo>--<owner>.aem.page/content/<site-name>/`。

   例えば、ブランチ名が `main`、リポジトリが `edsforms`、所有者が `wkndforms`、site-name が `eds-forms` の場合、URL は次のようになります。
   `https://main--edsforms--wkndforms.aem.page/content/eds-forms/`

   ![ インデックスページ ](/help/edge/docs/forms/assets/publish-index-page.png)

Edge Delivery ServicesFormsのスタイルを設定するには、アダプティブFormsブロックの `.css` ファイルと `.js` ファイルを編集し [ ローカル AEM開発環境の設定 ](#set-up-local-aem-development-environment) 変更内容を即座にブラウザーに表示します。

## ローカル AEM開発環境のセットアップ

ローカル AEM開発環境をセットアップして、カスタムスタイルやコンポーネントをローカルで開発できます。 ローカル AEM開発環境で起動して実行するには：

1. **AEM CLI のインストール**:AEM CLI を使用すると、開発タスクが簡単になります。 npm を使用してグローバルにインストールしましょう。

   ```Bash
       npm install -g @adobe/aem-cli
   ```

1. **GitHub プロジェクトの複製**：次のコマンドを使用して、GitHub からAEM プロジェクトリポジトリを複製します。次のコマンドを使用します。 <owner> リポジトリの所有者と <repo> リポジトリ名を置き換えます。

   ```
   git clone https://github.com/<owner>/<repo>
   ```

1. **ローカル環境の開始**: プロジェクトディレクトリに移動し、1 つのコマンドでローカル AEM インスタンスを開始します。

   ```
   cd <repo>
   aem up
   ```

アダプティブFormsブロック `blocks/form` フォルダーでローカルに変更を行い、フォームのスタイル設定とコーディングに使用できます。 このディレクトリ内の `.css` ファイルまたは `.js` ファイルを編集すると、変更がブラウザーにすぐに反映されることを確認できます。

変更が完了したら、Git コマンドを使用して変更をコミットし、プッシュします。 これにより、次の URL でアクセスできる、プレビュー環境と実稼動環境が更新されます（プレースホルダーをプロジェクトの詳細に置き換えます）。

プレビュー環境：`https://<branch>--<repo>--<owner>.aem.page/content/<site-name>`
実稼動環境：`https://<branch>--<repo>--<owner>.aem.live/content/<site-name>`


## GitHub ビルドの問題のトラブルシューティング

潜在的な問題に対処することで、GitHub ビルドプロセスがスムーズに行われるようにします。

* **lint エラーの処理：**
lint エラーが発生した場合は、回避できます。 [EDS プロジェクト]/package.json ファイルを開き、「lint」スクリプトを `"lint": "npm run lint:js && npm run lint:css"` から `"lint": "echo 'skipping linting for now'"` に変更します。 ファイルを保存し、変更を GitHub プロジェクトにコミットします。

<!-- * **Resolve Module Path Error:**
    If you encounter the error "Unable to resolve path to module "'../../scripts/lib-franklin.js'", navigate to the [EDS Project]/blocks/forms/form.js file. Update the import statement by replacing the lib-franklin.js file with the aem.js file. -->
