---
title: AEM Forms の Edge Delivery Services の基本を学ぶ - 開発者向けチュートリアル
description: このチュートリアルは、新しい Adobe Experience Manager Forms（AEM）プロジェクトを起動および実行するのに役立ちます。 10 分から 20 分で、独自のフォームを作成できます。
feature: Edge Delivery Services
exl-id: bb7e93ee-0575-44e1-9c5e-023284c19490
role: Admin, Architect, Developer
source-git-commit: e2259e542df5a12748705af901d073e4486292c4
workflow-type: tm+mt
source-wordcount: '1907'
ht-degree: 99%

---

# はじめに - 開発者向けチュートリアル

今日のデジタル時代では、ユーザーにわかりやすいフォームを作成することはどの組織にとっても不可欠です。 AEM Forms の Edge Delivery Services を使用すると、Google Docs や Microsoft Office などの使い慣れたツールを使用してフォームを作成できます。

これらのフォームは、Microsoft Excel または Google Sheets ファイルに直接データを送信します。これにより、Google Sheets、Microsoft Excel、Microsoft SharePoint の活発なエコシステムと堅牢な API を使用して、送信されたデータを簡単に処理したり、既存のビジネスワークフローを開始したりできます。

AEM Forms には、アダプティブフォームブロックと呼ばれるブロックが用意されており、データを取得して保存するフォームを簡単に作成できます。 [アダプティブフォームブロックを使用して設定済みの新しい AEM プロジェクトを作成](#create-a-new-aem-project-pre-configured-with-adaptive-forms-block)<!--or [add the Adaptive Forms Block to an existing AEM project](#add-adaptive-forms-block-to-your-existing-aem-project)-->できます。

この AEM Forms チュートリアルでは、新しい Adobe Experience Manager（AEM）Forms プロジェクトを使用して独自のカスタムフォームを作成、プレビュー、公開する方法について説明します。

## 前提条件

* GitHub アカウントを持っており、Git の基本を理解している。
* Google または Microsoft SharePoint アカウントを持っている。
* HTML、CSS、JavaScript の基本を理解している。
* ローカル開発用の Node/npm がインストールされている。

**警告** このチュートリアルでは、macOS、Chrome および Visual Studio Code を使用します。 この手順は他の設定にも適用できますが、スクリーンショットと特定の UI 要素は、選択したオペレーティングシステム、ブラウザー、コードエディターによって異なる場合があります。


## アダプティブフォームブロックを使用した設定済みの新しい AEM プロジェクトの作成

AEM Forms ボイラープレートテンプレートを使用すると、Adaptive Forms ブロックで設定済みの AEM プロジェクトをすぐに開始できます。 これは、AEM のベストプラクティスに従って、フォームの作成をすぐに開始するための最も迅速かつ簡単な方法です。

### AEM Forms ボイラープレートリポジトリテンプレートの基本を学ぶ

1. AEM プロジェクトの GitHub リポジトリを作成します。 リポジトリを作成するには：
   1. [https://github.com/adobe-rnd/aem-boilerplate-forms](https://github.com/adobe-rnd/aem-boilerplate-forms) に移動します。

      ![AEM Forms ボイラープレート](/help/edge/assets/aem-forms-boilerplate.png)
   1. 「**このテンプレートを使用**」オプションをクリックし、「**新しいリポジトリを作成**」オプションを選択します。 新しいリポジトリを作成画面が開きます。

      ![AEM Forms ボイラープレートを使用して新しいリポジトリを作成](/help/edge/assets/create-new-repository-using-aem-forms-boilerplate.png)

   1. 新しいリポジトリを作成画面で、**所有者**&#x200B;を選択し、**リポジトリ名**&#x200B;を指定します。 アドビでは、リポジトリを&#x200B;**パブリック**&#x200B;に設定することをお勧めします。 したがって、「**パブリック**」オプションを選択し、「**リポジトリを作成**」をクリックします。

   ![リポジトリをパブリックに設定](/help/edge/assets/create-a-new-repo-keep-it-public.png)


1. AEM Code Sync GitHub アプリをリポジトリにインストールします。 インストールするには：
   1. [https://github.com/apps/aem-code-sync/installations/new](https://github.com/apps/aem-code-sync/installations/new) に移動します。
   1. AEM Code Sync をインストール画面で、「**リポジトリのみを選択**」オプションを選択し、新しく作成したリポジトリを選択します。 「保存」をクリックします。

   ![リポジトリをパブリックに設定](/help/edge/assets/install-aem-code-sync-app-for-your-repo.png)

   >[!NOTE]
   >
   >
   > GitHub Enterprise で IP フィルタリングを使用している場合は、IP（3.227.118.73）を許可リストに追加できます。

   これで完了です。 `https://<branch>--<repo>--<owner>.aem.page/` で新しい web サイトを実行しています。

   * `<branch>` は、GitHub リポジトリのブランチを指します。
   * `<repository>` は GitHub リポジトリを示します。
   * `<owner>` は、GitHub リポジトリをホストする GitHub アカウントのユーザー名を指します。

   例えば、分岐名が `main`、リポジトリが `wefinance`、所有者が `wkndforms` の場合、web サイトは `https://main--wefinance--wkndforms.aem.page` で稼動しています。
&lt;!--(https://main--wefinance--wkndform.aem.page)-->

### 独自のコンテンツソースのリンク

<!--Your newly created GitHub repository points to [example content stored in a Google Drive folder](https://drive.google.com/drive/folders/1bvjfi6TqpYA7DvbX6kKc-m7FgHuJ4RUQ). This read-only content provides a great starting point for your forms. Feel free to copy it into your own Google Drive and customize it to fit your needs.

![Sample Content on Google Drive](/help/edge/assets/folder-with-sample-content.png)-->

サンプルコンテンツを自身のコンテンツフォルダーにコピーし、GitHub リポジトリが自身のコンテンツフォルダーを指すようにするには、次の手順を実行します。

1. Google Drive または Microsoft SharePoint で、AEM コンテンツ専用の新しいフォルダーを作成します。 このドキュメントでは、Microsoft SharePoint で作成されたフォルダーを使用します。

1. Adobe Experience Manager ユーザー（forms@adobe.com）とフォルダーを共有します。

   ![「アクセスを管理」オプションを使用して、AEM ユーザーとフォルダーを共有する（SharePoint）](/help/edge/assets/share-folder-with-aem-user.png)

   ![「アクセスを管理」オプションを使用して、AEM ユーザーとフォルダーを共有する（Google Drive）](/help/edge/assets/share-google-drive-folder.png)


   フォルダーに対する編集権限が Adobe Experience Manager ユーザーに付与されていることを確認します。

   ![AEM ユーザーとフォルダーを共有し、編集権限を付与する（SharePoint）](/help/edge/assets/share-folder-with-aem-user-provide-editing-access.png){width=50%}

   ![AEM ユーザーとフォルダーを共有し、編集権限を付与する（Google Drive）](/help/edge/assets/add-aem-user-google-folder.png){width=50%}

1. [サンプルコンテンツ](/help/edge/assets/wefinance1.zip)をフォルダーにコピーします。 コピーする手順は、次のとおりです。

   1. ダウンロードしたフォルダーを解凍し、コンテンツをコピーします。

      ![サンプルコンテンツのダウンロード](/help/edge/assets/download-sample-content.png)

      `nav` および `footer` ファイルはページの基本レイアウトを定義し、プロジェクト全体で変更されることはほとんどありません。 また、他のほとんどのコンテンツファイルとは異なる特定の構造を持っています。 これらのファイルを調べると、AEM プロジェクトでコンテンツがどのように編成されているかがわかります。


   1. これらのファイルを Microsoft SharePoint または Google Drive フォルダーにアップロードします。

      ![Google Drive のサンプルコンテンツ](/help/edge/assets/upload-sample-files-to-your-content-folder.png)

      必ず、サンプルコンテンツの `enquiry` シートを Google Drive または Microsoft SharePoint のフォルダーにコピーしてください。 サンプルフォームの構造が含まれています。

1. コンテンツフォルダーの設定が完了したので、以前に AEM Forms ボイラープレートを使用して作成した GitHub 上のプロジェクトにリンクします。 接続する手順は、次のとおりです。

   1. AEM Forms ボイラープレートを使用して以前に作成した GitHub リポジトリに移動します。
   1. `fstab.yaml` を開いて編集します。
   1. 既存の参照を、AEM ユーザー（forms@adobe.com）と共有したフォルダーのパスに置き換えます。

      ![Google Drive のサンプルコンテンツ](/help/edge/assets/replace-path-in-fstab-yaml-with-your-content-folder.png)


      Microsoft SharePoint を使用する場合、フォルダーパスは次の形式を使用します。

      ```HTML
      https://<tenant>.SharePoint.com/sites/<sp-site>/Shared%20Documents/<folder-name>
      ```

      例：

      ```HTML
      https://adobe.SharePoint.com/sites/wkndforms/Shared%20Documents/wefinance
      ```

      Microsoft SharePoint でのファイル管理について詳しくは、[Adobe SharePoint の使用方法](https://www.aem.live/docs/setup-customer-sharepoint)を参照してください。


   1. 参照を更新し、すべてが正しく表示されたら、更新された `fsatb.yaml` ファイルをコミットします。 ビルドの問題が発生した場合は、[GitHub ビルド問題のトラブルシューティング](#troubleshooting-github-build-issues)を参照してください。

      ![更新された fsatab.yaml ファイルのコミット](/help/edge/assets/commit-updated-fstab-yaml.png)

      これにより、コンテンツフォルダーが web サイトに接続されます。 参照を更新した後、最初に「404 Not Found」というエラーが発生する場合があります。 これは、コンテンツがまだプレビューされていないためです。 次の節では、コンテンツのオーサリングとプレビューを開始する方法について説明します。

### コンテンツのプレビューと公開

最後の手順を完了しても、新しいコンテンツソースは空にはなりませんが、プレビューまたはライブステージに昇格されるまで、web サイトには表示されません。 現在、これにより 404 エラーが発生する場合があります。

非公開のコンテンツをプレビューするには：

1. [AEM Sidekick](https://chrome.google.com/webstore/detail/helix-sidekick-beta/ccfggkjabjahcjoljmgmklhpaccedipo) という Chrome 拡張機能をインストールします。

   ![AEM SideKick をインストール](/help/edge/assets/install-aem-sidekick.png)

   拡張機能を Chrome にインストールした後、ピン留めしておくと、見つけやすくなります。

   ![AEM Sidekick をピン留め](/help/edge/assets/pin-aem-sidekick.png)

1. Sidekick Chrome 拡張機能を設定するには、以前に共有した Google Drive または Microsoft SharePoint フォルダーに移動し、ブラウザのツールバーにある拡張機能アイコンを右クリックして、「`Add this project`」を選択します。

   ![AEM Sidekick - プロジェクトを追加](/help/edge/assets/aem-sidekick-add-a-project.png)

   拡張機能がインストールされ、プロジェクトが追加されると、Google Drive からコンテンツをプレビューして公開する準備が整います。

1. Microsoft SharePoint または Google Drive フォルダー内のすべてのドキュメントを選択します。 Ctrl キー（Windows／Linux）または Cmd キー（Mac）を押しながらクリックすると、複数のドキュメントを選択できます。

   ![すべてのファイルを選択](/help/edge/assets/select-all-files.png)

1. Chrome 拡張機能バーにピン留めされている AEM Sidekick アイコンをクリックします。 画面にツールバーが表示されます。 コンテンツのプレビューまたは公開を選択できます。

   `index`、`nav`、`footer` および `enquiry` ファイルをコピーした場合、これらはすべて独自のプレビューおよび公開サイクルを持つ別個のドキュメントになるので、すべてをプレビュー（および公開）します。

   ファイルをプレビューすると、新しいブラウザータブにドキュメントが表示されます。 サンプルフォームをプレビューするには、次の URL に移動します。


   ```HTML
   https://<branch>--<repository>--<owner>.aem.live
   ```

   * `<branch>` は、GitHub リポジトリのブランチを参照します。
   * `<repository>` は GitHub リポジトリを示します。
   * `<owner>` は、GitHub リポジトリをホストする GitHub アカウントのユーザー名を参照します。


   `https://<branch>--<repo>--<owner>.aem.page/enquiry` の URL。

   例えば、プロジェクトのリポジトリの名前が「wefinance」で、アカウント所有者「wkndform」の下にあり、「main」分岐とフォーム名を `enquiry` として使用している場合、URL は次のようになります。`https://main--wefinance--wkndform.aem.live/enquiry`
&lt;! --(https://main--wefinance--wkndform.aem.live/enquiry).-->

### フォームの作成

サンプルコンテンツには、「お問い合わせ」フォームのテンプレートとなる「お問い合わせ」シートが含まれます。 シートの各行は[フォームフィールド](/help/edge/docs/forms/form-components.md#available-components)を表し、列ヘッダーでは[フィールドのプロパティ](/help/edge/docs/forms/form-components.md#available-components)を定義します。 このサンプルフォームを使用すると、フォームの作成を素早く開始できます。

![お問い合わせフォーム](/help/edge/docs/forms/assets/enquiry-form-microsoft-sharepoint.png)

まず、フィールドラベルの更新から始めましょう。 編集用に「お問い合わせ」シートを開き、送信ボタンのラベルを「`Let's Talk`」に変更し、AEM Sidekick を使用してファイルをプレビューして公開します。

![お問い合わせフォーム](/help/edge/assets/enquiry-form-preview-publish.png)

ファイルをプレビューまたは公開すると、ファイルの JSON バージョンが新しいタブに表示されます。 ファイルのプレビュー（.aem.page）または公開（.aem.live）の URL をコピーします。

![フォームスプレッドシートの JSON](/help/edge/assets/preview-and-publish-enquiry-form.png)

`enquiry` ファイルを開き、フォームブロック内の URL を、前の手順でコピーしたファイルの URL に置き換えます。 URL がハイパーリンクであることを確認します。

![スプレッドシートの URL の .json URL を使用したお問い合わせファイル](/help/edge/assets/enquiry-doc-to-embed-form.png)

AEM Sidekick を使用して、お問い合わせドキュメントをプレビューおよび公開します。

![スプレッドシートの URL の .json URL を使用したお問い合わせファイル](/help/edge/assets/preview-and-publish-enquiry-document.png)


更新されたお問い合わせフォームをプレビューするには、次の URL に移動します。


```HTML
    https://<branch>--<repository>--<owner>.aem.page/enquiry
       
```

送信ボタンのラベルが `Let's Talk` に更新されます。

![お問い合わせフォーム](/help/edge/assets/updated-form.png)

&lt;!--(https://main--wefinance--wkndform.aem.live/enquiry)-->

URL：`https://main--wefinance--wkndform.aem.live/enquiry`
&lt;!--(https://main--wefinance--wkndform.aem.live/enquiry)-->


新しいフォームの作成と公開について詳しくは、[フォームの作成](/help/edge/docs/forms/create-forms.md)ガイドを参照してください。

### スタイル設定と機能の開発の開始


ローカル AEM 開発環境をすぐに起動して実行するには、次の手順を実行します。

1. AEM CLI をインストールします。AEM CLI により、開発タスクが簡素化されます。 npm を使用してグローバルにインストールしましょう。

   ```Bash
       npm install -g @adobe/aem-cli
   ```

1. GitHub プロジェクトのクローンを作成します。次のコマンドを使用して、GitHub からプロジェクトリポジトリのクローンを作成します。 &lt;owner> リポジトリの所有者と &lt;repo> リポジトリ名を置き換えます。

   ```
   git clone https://github.com/<owner>/<repo>
   ```

1. ローカル環境を起動します。プロジェクトディレクトリに移動し、次の 1 つのコマンドでローカル AEM インスタンスを起動します。

   ```
   cd <repo>
   aem up
   ```

アダプティブフォームブロックの `blocks/form` フォルダーは、フォームのスタイル設定とコードのプレイグラウンドです。 このディレクトリ内の `.css` または `.js` ファイルを編集すると、変更がブラウザーに即座に反映されることがわかります。

成果を公開る準備は整いましたか？ Git を使用して変更をコミットし、プッシュします。 これにより、次の URL からアクセスできるプレビュー環境と実稼動環境が更新されます（プレースホルダーをプロジェクトの詳細に置き換えます）。

プレビュー環境：`https://<branch>--<repo>--<owner>.aem.page/`
実稼動環境：`https://<branch>--<repo>--<owner>.aem.live/`

これで完了です。 ローカル開発環境が正常に設定され、変更がデプロイされました。

## 既存の AEM プロジェクトへのアダプティブフォームブロックの追加

<!--
>[!VIDEO](https://video.tv.adobe.com/v/3427789)-->

既存の AEM プロジェクトがある場合は、アダプティブフォームブロックを現在のプロジェクトに統合して、フォームの作成を開始できます。

>[!NOTE]
>
>
> この手順は、[AEM ボイラープレート](https://github.com/adobe/aem-boilerplate)を使用して作成したプロジェクトに適用されます。 [AEM Forms ボイラープレート](https://github.com/adobe-rnd/aem-boilerplate-forms)を使用して AEM プロジェクトを作成した場合は、この手順をスキップできます。

統合するには：

1. **必要なファイルとフォルダーを追加**
   1. 次のフォルダーとファイルを [AEM Forms ボイラープレート](https://github.com/adobe-rnd/aem-boilerplate-forms)から AEM プロジェクトにコピー＆ペーストします。

      * [フォームブロック](https://github.com/adobe-rnd/aem-boilerplate-forms/tree/main/blocks/form)フォルダー
      * [form-common](https://github.com/adobe-rnd/aem-boilerplate-forms/tree/main/models/form-common) フォルダー
      * [form-components](https://github.com/adobe-rnd/aem-boilerplate-forms/tree/main/models/form-components) フォルダー
      * [form-editor-support.js](https://github.com/adobe-rnd/aem-boilerplate-forms/blob/main/scripts/form-editor-support.js) ファイル
      * [form-editor-support.css](https://github.com/adobe-rnd/aem-boilerplate-forms/blob/main/scripts/form-editor-support.css) ファイル

1. **コンポーネント定義とモデルファイルを更新**
   1. AEM プロジェクト内の `../models/_component-definition.json` ファイルに移動し、[AEM Forms ボイラープレート内の _component-definition.json ファイル](https://github.com/adobe-rnd/aem-boilerplate-forms/blob/main/models/_component-definition.json#L39-L48)からの変更を使用して更新します。

   1. AEM プロジェクト内の `../models/_component-models.json` ファイルに移動し、[AEM Forms ボイラープレート内の _component-models.json ファイル](https://github.com/adobe-rnd/aem-boilerplate-forms/blob/main/models/_component-models.json#L24-L26)からの変更を使用して更新します。

1. **エディタースクリプトにフォームエディターを追加**
   1. AEM プロジェクト内の `../scripts/editor-support.js` ファイルに移動し、[AEM Forms ボイラープレート内の editor-support.js file ファイル](https://github.com/adobe-rnd/aem-boilerplate-forms/blob/main/scripts/editor-support.js#L105-L106)からの変更を使用して更新します。
1. **ESLint 設定ファイルを更新**
   1. AEM プロジェクトの `../.eslintignore` ファイルに移動し、次のコード行を追加して、フォームブロックルールエンジンに関連するエラーを防ぎます。

      ```
          blocks/form/rules/formula/*
          blocks/form/rules/model/*
      ```

1. これらの変更を GitHub 上の AEM プロジェクトリポジトリにコミットしてプッシュします。

これで作業は完了です。アダプティブフォームブロックが AEM プロジェクトの一部になりました。 フォームの作成と AEM ページへの追加を開始できます。

## GitHub ビルドの問題のトラブルシューティング

潜在的な問題に対処することで、GitHub ビルドプロセスがスムーズに行われるようにします。

* **モジュールパスエラーの解決：**
「モジュール &#39;…/…/scripts/lib-franklin.js&#39; へのパスを解決できません」というエラーが発生した場合は、[EDS プロジェクト]/blocks/forms/form.js ファイルに移動します。 lib-franklin.js ファイルを aem.js ファイルに置き換えて、読み込みステートメントを更新します。

* **lint エラーの処理：**
lint エラーが発生した場合は、回避できます。 [EDS プロジェクト]/package.json ファイルを開き、「lint」スクリプトを `"lint": "npm run lint:js && npm run lint:css"` から `"lint": "echo 'skipping linting for now'"` に変更します。 ファイルを保存し、変更を GitHub プロジェクトにコミットします。


## 関連トピック

{{see-more-forms-eds}}
