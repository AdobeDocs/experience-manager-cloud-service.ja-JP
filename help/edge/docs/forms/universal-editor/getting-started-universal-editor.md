---
title: ユニバーサルエディターでの AEM Forms の Edge Delivery Services の基本を学ぶ - 開発者向けチュートリアル
description: このチュートリアルは、新しい Adobe Experience Manager Forms（AEM）プロジェクトを起動および実行するのに役立ちます。10～20 分で、ユニバーサルエディターで独自の Edge Delivery Services フォームが作成されます。
feature: Edge Delivery Services
role: Admin, Architect, Developer
exl-id: 24a23d98-1819-4d6b-b823-3f1ccb66dbd8
source-git-commit: 95998daf04ae579ca11896953903852e6140c3a4
workflow-type: ht
source-wordcount: '1853'
ht-degree: 100%

---


# ユニバーサルエディター（WYSIWYG）での AEM Forms の Edge Delivery Services の基本を学ぶ

| バージョン | 記事リンク |
| -------- | ---------------------------- |
| ユニバーサルエディターベースのオーサリング | この記事 |
| ドキュメントベースのオーサリング | [ここをクリックしてください](/help/edge/docs/forms/tutorial.md) |


<span class="preview">この機能は、早期アクセスプログラムを通じて使用できます。アクセスをリクエストするには、公式アドレスから <a href="mailto:aem-forms-ea@adobe.com">aem-forms-ea@adobe.com</a> に、GitHub の組織名とリポジトリ名を記載したメールを送信してください。例えば、リポジトリ URL が https://github.com/adobe/abc の場合、組織名は adobe で、リポジトリ名は abc になります。</span>

今日のデジタル時代では、ユーザーにわかりやすいフォームはすべての組織にとって不可欠です。Edge Delivery Services フォームは、WYSIWYG（見たままが得られる）機能を提供するユニバーサルエディターを使用して作成されます。最新の直感的なインターフェイスで、効率的なフォームオーサリングを実現します。

AEM Forms には、アダプティブフォームブロックと呼ばれるブロックが用意されており、データを取得して保存する Edge Delivery Services フォームを簡単に作成できます。[アダプティブフォームブロックで事前設定済みの新しい AEM プロジェクトを作成](#create-a-new-aem-project-pre-configured-with-adaptive-forms-block)することも、[アダプティブフォームブロックを既存の AEM プロジェクトに追加](#add-adaptive-forms-block-to-your-existing-aem-project)することもできます。

![Github リポジトリのワークフロー](/help/edge/assets/repo-workflow.png){width=auto}

このチュートリアルでは、ユニバーサルエディターの WYSIWYG オーサリングを使用して、新規または既存の Adobe Experience Manager サイトプロジェクトで独自のフォームを作成、プレビュー、公開する方法について説明します。


## 前提条件

* GitHub アカウントを持っており、Git の基本を理解している。
* HTML、CSS、JavaScript の基本を理解している。
* ローカル開発用の Node/npm がインストールされている。

## アダプティブフォームブロックを使用した設定済みの新しい AEM プロジェクトの作成

AEM Forms ボイラープレートテンプレートを使用すると、Adaptive Forms ブロックで設定済みの AEM プロジェクトをすぐに開始できます。 これは、AEM のベストプラクティスに従って、フォームの作成をすぐに開始する最も迅速かつ簡単な方法です。

### AEM Forms ボイラープレートリポジトリテンプレートの基本を学ぶ

1. AEM プロジェクトの GitHub リポジトリを作成します。 リポジトリを作成するには：
   1. [https://github.com/adobe-rnd/aem-boilerplate-forms](https://github.com/adobe-rnd/aem-boilerplate-forms) に移動します。

      ![AEM Forms ボイラープレート](/help/edge/docs/forms/assets/eds-form-boilerplate.png)
   1. 「**このテンプレートを使用**」オプションをクリックし、「**新しいリポジトリを作成**」オプションを選択します。

      ![AEM Forms ボイラープレートを使用して新しいリポジトリを作成](/help/edge/docs/forms/assets/use-eds-form-template.png)

      **新しいリポジトリを作成**&#x200B;画面が開きます。

   1. **新しいリポジトリを作成**&#x200B;画面で、**所有者**&#x200B;を選択し、**リポジトリ名**&#x200B;を指定します。アドビでは、リポジトリを&#x200B;**パブリック**&#x200B;に設定することをお勧めします。したがって、「**パブリック**」オプションを選択し、「**リポジトリを作成**」をクリックします。

      ![リポジトリをパブリックに設定](/help/edge/docs/forms/assets/name-eds-repo.png)

1. AEM Code Sync GitHub アプリをリポジトリにインストールします。 インストールするには：
   1. [https://github.com/apps/aem-code-sync/installations/new](https://github.com/apps/aem-code-sync/installations/new) に移動します。
   1. **AEM Code Sync をインストール**&#x200B;画面で、「**リポジトリのみを選択**」オプションを選択し、新しく作成したリポジトリを選択します。「**保存**」をクリックします。

   ![リポジトリをパブリックに設定](/help/edge/docs/forms/assets/aem-code-sync-up.png)

1. 次に、AEM Forms ボイラープレートを使用して作成した GitHub リポジトリを AEM プロジェクトオーサリング環境にリンクします。接続する手順は、次のとおりです。

   1. AEM Forms ボイラープレートを使用して以前に作成した GitHub リポジトリに移動します。
   1. **fstab.yaml** ファイルを編集用に開きます。

      ![fstab.yaml ファイルを開く](/help/edge/docs/forms/assets/open-fstab.png)

   1. **fstab.yaml** ファイルを編集して、プロジェクトのマウントポイントを更新します。URL を AEM as a Cloud Service オーサリングインスタンスの URL に置き換えます。
      `https://<aem-author>/bin/franklin.delivery/<owner>/<repository>/main`

      ![fstab.yaml ファイルを編集](/help/edge/docs/forms/assets/edit-fstab-file.png)

   1. 参照を更新し、すべてが正しく表示されたら、更新された **fstab.yaml** ファイルをコミットします。

      ![変更をコミット](/help/edge/docs/forms/assets/commit-fstab-changes.png)

      ビルドの問題が発生した場合は、[GitHub ビルド問題のトラブルシューティング](#troubleshooting-github-build-issues)を参照してください。

### 新しい AEM プロジェクトの作成

GitHub プロジェクトが完成したら、AEM as a Cloud Service オーサリングインスタンスで新しい AEM プロジェクトを作成して公開できます。

1. 新しい AEM プロジェクトを作成するには：

   1. AEM as a Cloud Service オーサリングインスタンスにログインし、「**Sites**」を選択します。

      ![「Sites」を選択](/help/edge/assets/select-sites.png)

   1. **作成**／**テンプレートからサイト**&#x200B;をクリックします。

      ![サイトを作成](/help/edge/docs/forms/assets/create-sites.png)

   1. Edge Delivery Services サイトテンプレートを選択し、「**次へ**」をクリックします。

      ![サイトテンプレートを選択](/help/edge/docs/forms/assets/select-site-template.png)

      >[!NOTE]
      >
      > * オーサリングインスタンスで Edge Delivery Services サイトテンプレートが使用できない場合は、「読み込み」ボタンをクリックしてテンプレートをアップロードします。
      > * Edge Delivery Services サイトテンプレートは、[GitHub](https://github.com/adobe-rnd/aem-boilerplate-xwalk/releases) からダウンロードできます。

   1. 新しい AEM プロジェクトを作成するには、次の詳細を入力します。
      * **サイトのタイトル** - サイトを説明するタイトルを追加します。
      * **サイトのタイトル** - 前の手順で定義した `site-name` を使用します。
      * **GitHub URL** - 前の手順で作成した GitHub プロジェクトの URL を使用します。

      ![AEM サイトを作成](/help/edge/docs/forms/assets/create-aem-site.png)

   1. **サイトを作成**&#x200B;ダイアログが表示されたら、「**OK**」をクリックします。

      ![「OK」をクリック](/help/edge/docs/forms/assets/click-ok-aem-site.png)

      わずか数分で、新しい AEM プロジェクトが作成されます。

   1. Sites コンソールで新しく作成した AEM プロジェクトに移動し、「**編集**」をクリックします。
この場合、説明のために `index.html` ページを使用しています。

      ![AEM サイトを編集](/help/edge/docs/forms/assets/edit-site.png)

      AEM プロジェクトがユニバーサルエディターの新しいタブで開き、WYSIWYG オーサリングが可能になります。これで、AEM プロジェクトを編集できます。

      ![ユニバーサルエディターでサイトが開く](/help/edge/docs/forms/assets/site-in-universal-editor.png)

1. 作成した AEM プロジェクトの公開

   AEM プロジェクトの編集が完了したら、プロジェクトを公開します。公開するには：

   1. Sites コンソールで、すべての AEM プロジェクトページを選択し、「**クイック公開**」をクリックします。

      ![AEM Sites プロジェクトを公開](/help/edge/docs/forms/assets/publish-sites.png)

   1. **クイック公開**&#x200B;確認ダイアログが表示されたら、「**公開**」をクリックして公開プロセスを開始します。

      ![クイック公開確認ダイアログ](/help/edge/docs/forms/assets/quick-publish.png)

      または、ユニバーサルエディターのユーザーインターフェイスから AEM プロジェクトページを直接公開することもできます。

      ![クイック公開確認ダイアログ](/help/edge/docs/forms/assets/qui.png)

   これで完了です。 `https://<branch>--<repo>--<owner>.aem.page/content/<site-name>/` で新しい web サイトを実行しています。

   * `<branch>` は、GitHub リポジトリのブランチを指します。
   * `<repository>` は GitHub リポジトリを示します。
   * `<owner>` は、GitHub リポジトリをホストする GitHub アカウントのユーザー名を指します。
   * `<site-name>` は、作成したサイト名の名前を指します。

   例えば、分岐名が `main`、リポジトリが `edsforms`、所有者が `wkndforms`、`site-name` が `eds-forms` の場合、web サイトは `https://main--edsforms--wkndforms.aem.page/content/eds-forms/` で稼動しています。

   >[!NOTE]
   >
   > * AEM プロジェクトの `index.html` ページを表示するには、次の URL を使用します。`https://<branch>--<repo>--<owner>.aem.page/content/<site-name>/`
   > * AEM プロジェクトの `index page` 以外のページを表示するには、次の URL を使用します。`https://<branch>--<repo>--<owner>.aem.page/content/<site-name>/<site-page-name>`

これで、[フォームの作成と AEM プロジェクトへの追加](#add-edge-delivery-services-forms-to-aem-project)を開始できます。

## 既存の AEM プロジェクトへのアダプティブフォームブロックの追加

既存の AEM プロジェクトがある場合は、アダプティブフォームブロックを現在のプロジェクトに統合して、フォームの作成を開始できます。

>[!NOTE]
>
>
> この手順は、[AEM ボイラープレート XWalk](https://github.com/adobe-rnd/aem-boilerplate-xwalk) を使用して作成したプロジェクトに適用されます。[AEM Forms ボイラープレート](https://github.com/adobe-rnd/aem-boilerplate-forms)を使用して AEM プロジェクトを作成した場合は、この手順をスキップできます。

統合するには：

1. ローカルシステム上の AEM プロジェクトリポジトリフォルダーに移動します。

1. 次のフォルダーとファイルを [AEM Forms ボイラープレート](https://github.com/adobe-rnd/aem-boilerplate-forms)から AEM プロジェクトにコピー＆ペーストします。

   * [フォームブロック](https://github.com/adobe-rnd/aem-boilerplate-forms/tree/main/blocks/form)フォルダー
   * [form-editor-support.js](https://github.com/adobe-rnd/aem-boilerplate-forms/blob/main/scripts/form-editor-support.js) ファイル
   * [form-editor-support.css](https://github.com/adobe-rnd/aem-boilerplate-forms/blob/main/scripts/form-editor-support.css) ファイル
1. AEM プロジェクトの `/scripts/editor-support.js` ファイルに移動し、[AEM Forms ボイラープレート内の editor-support.js ファイル](https://github.com/adobe-rnd/aem-boilerplate-forms/blob/main/scripts/editor-support.js)で更新します。
1. AEM プロジェクトの `/models/_section.json` に移動し、「form」と「embed-adaptive-form」を `filters` オブジェクトのコンポーネント配列に追加します。

   ```
       "filters": [
       {
     "id": "section",
     "components": [
       .
       .
       .
       "form",
       "embed-adaptive-form"
     ]
    }]
   ```

1. （オプション）AEM プロジェクトの `/.eslintignore` に移動し、次のコード行を追加します。

   ```
   blocks/form/rules/formula/*
   blocks/form/rules/model/*
   blocks/form/rules/functions.js
   scripts/editor-support.js
   scripts/editor-support-rte.js
   ```

1. （オプション）AEM プロジェクトの `/.eslintrc.js` に移動して、`rules` オブジェクトに次のコード行を追加します。

   ```
   'xwalk/max-cells': ['error', {
     '*': 4, // default limit for all models
     form: 15,
     wizard: 12,
     'form-button': 7,
     'checkbox-group': 20,
     checkbox: 19,
     'date-input': 21,
     'drop-down': 19,
     email: 22,
     'file-input': 20,
     'form-fragment': 15,
     'form-image': 7,
     'multiline-input': 23,
     'number-input': 22,
     panel: 17,
     'radio-group': 20,
     'form-reset-button': 7,
     'form-submit-button': 7,
     'telephone-input': 20,
     'text-input': 23,
     accordion: 14,
     modal: 11,
     rating: 18,
     password: 20,
     tnc: 12,
   }],
   'xwalk/no-orphan-collapsible-fields': 'off', // Disable until enhancement is done for Forms properties
   ```

1. ターミナルを開き、次のコマンドを実行します。

   ```
   npm i
   npm run build:json
   ```

   >[!NOTE]
   >
   > 変更内容を GitHub の AEM プロジェクトリポジトリにプッシュする前に、AEM プロジェクトのルートレベルにある `component-definition.json`、`component-models.json`、`component-filters.json` の各ファイルがフォーム関連オブジェクトで更新されていることを確認してください。

1. これらの変更を GitHub 上の AEM プロジェクトリポジトリにコミットしてプッシュします。

   <!--
    1. **Update ESLint configuration file**
    2. Navigate to the `../.eslintignore` file in your AEM Project and add the following line of codes to prevent errors related to the Form Block rule engine:
        
            blocks/form/rules/formula/*
            blocks/form/rules/model/*
       * [form-common](https://github.com/adobe-rnd/aem-boilerplate-forms/tree/main/models/form-common)  folder
       * [form-components](https://github.com/adobe-rnd/aem-boilerplate-forms/tree/main/models/form-components) folder
    
     3. **Update component definitions and models files**
       1. Navigate to the `../models/_component-definition.json` file in your AEM Project and update it with the changes from the [_component-definition.json file in the AEM Forms Boilerplate](https://github.com/adobe-rnd/aem-boilerplate-forms/blob/main/models/_component-definition.json#L39-L48).
    
    3. Navigate to the `../models/_component-models.json` file in your AEM Project and update it with the changes from the [_component-models.json file in the AEM Forms Boilerplate](https://github.com/adobe-rnd/aem-boilerplate-forms/blob/main/models/_component-models.json#L24-L26) -->

これで作業は完了です。アダプティブフォームブロックが AEM プロジェクトの一部になりました。[フォームの作成と AEM プロジェクトへの追加を開始](#add-edge-delivery-services-forms-to-aem-site-project)できます。

## WYSIWYG を使用した Forms の作成

WYSIWYG オーサリング用のユニバーサルエディターで AEM プロジェクトを開き、プロジェクトを編集し、AEM プロジェクトページに Edge Delivery Services フォームを含める「アダプティブフォーム」セクションを追加できます。

1. AEM プロジェクトページに「アダプティブフォーム」セクションを追加します。追加するには：
   1. Sites コンソールで AEM プロジェクトに移動し、編集するサイトページを選択して、「**編集**」をクリックします。編集用にユニバーサルエディターで AEM プロジェクトページが開きます。
この場合、説明のために `index.html` ページを使用しています。
   1. コンテンツツリーを開き、「アダプティブフォーム」セクションを追加するセクションに移動します。
   1. 「**[!UICONTROL 追加]**」アイコンをクリックし、コンポーネントリストから&#x200B;**[!UICONTROL アダプティブフォーム]**&#x200B;コンポーネントを選択します。

   ![コンテンツツリー](/help/edge/docs/forms/assets/add-adaptive-form-block.png)

   「アダプティブフォーム」セクションが追加されます。これで、AEM プロジェクトページへのフォームコンポーネントの追加を開始できます。

1. 追加した「アダプティブフォーム」セクションにフォームコンポーネントを追加します。フォームコンポーネントを追加するには：
   1. コンテンツツリーで、追加した「アダプティブフォーム」セクションに移動します。

      ![追加したアダプティブフォームブロック](/help/edge/docs/forms/assets/adative-form-block.png)


   1. 「**[!UICONTROL 追加]**」アイコンをクリックし、**アダプティブフォームコンポーネント**&#x200B;リストから目的のコンポーネントを追加します。

      ![コンポーネントを追加](/help/edge/docs/forms/assets/add-component.png)

      また、ユニバーサルエディターには直感的なドラッグ＆ドロップ機能が用意されているので、必要なアダプティブフォームコンポーネントをドラッグ＆ドロップすることもできます。

   1. 追加したアダプティブフォームコンポーネントを選択し、**[!UICONTROL プロパティ]**&#x200B;を使用して、そのプロパティを更新します。

      ![プロパティを開く](/help/edge/docs/forms/assets/component-properties.png)

   1. フォームをプレビューします。
以下のスクリーンショットは、WYSIWYG オーサリングを使用して AEM プロジェクトで作成されたフォームを示しています。

      ![追加したフォーム](/help/edge/docs/forms/assets/added-form-aem-sites.png)

      プレビューが完了したら、ユーザーはページの公開に進むことができます。

      >[!NOTE]
      >
      > 変更を行った後は、AEM プロジェクトページを再度公開することが重要です。そうしないと、更新がブラウザーに表示されません。

1. AEM プロジェクトページを再公開します。

   1. フォームを追加した後、「**公開**」をクリックして AEM プロジェクトページを再度公開します。

      ![フォームを公開](/help/edge/docs/forms/assets/publish-form.png)

   1. 画面に&#x200B;**公開**&#x200B;確認ダイアログが表示されたら、「**公開**」をクリックして公開を開始します。

      ![form1 を公開](/help/edge/docs/forms/assets/publish-form1.png)

      「**公開**」ボタンをクリックすると、`Publish started successfully` メッセージが表示されます。

      ![form2 を公開](/help/edge/docs/forms/assets/publish-form2.png)

   これで、次の URL で Edge Delivery Services フォームが追加された AEM プロジェクトページを表示できます。
   `https://<branch>--<repo>--<owner>.aem.page/content/<site-name>/`。

   例えば、分岐名が `main`、リポジトリが `edsforms`、所有者が `wkndforms`、サイト名が `eds-forms` の場合、URL は次のようになります。
   `https://main--edsforms--wkndforms.aem.page/content/eds-forms/`

   ![インデックスページ](/help/edge/docs/forms/assets/publish-index-page.png)

アダプティブフォームブロックの `.css` ファイルと `.js` ファイルを編集し、[ローカル AEM 開発環境を設定](#set-up-local-aem-development-environment)して Edge Delivery Services フォームをスタイル設定すると、変更がブラウザーで即座に表示できます。

>[!NOTE]
>
> また、[ユニバーサルエディターでスタンドアロンフォームを作成し、Edge Delivery Services に公開](/help/edge/docs/forms/universal-editor/create-forms.md)することもできます。

## ローカル AEM 開発環境の設定

カスタムスタイルとコンポーネントをローカルで開発するローカル AEM 開発環境を設定できます。ローカル AEM 開発環境をすぐに起動して実行するには：

1. **AEM CLI をインストールします**。AEM CLI により、開発タスクが簡素化されます。npm を使用してグローバルにインストールしましょう。

   ```Bash
       npm install -g @adobe/aem-cli
   ```

1. **GitHub プロジェクトのクローンを作成します**。次のコマンドを使用して、GitHub から AEM プロジェクトリポジトリのクローンを作成します。 <owner> リポジトリの所有者と <repo> リポジトリ名を置き換えます。

   ```
   git clone https://github.com/<owner>/<repo>
   ```

1. **ローカル環境を起動します**。プロジェクトディレクトリに移動し、次の 1 つのコマンドでローカル AEM インスタンスを起動します。

   ```
   cd <repo>
   aem up
   ```

フォームのスタイル設定とコーディングについては、アダプティブフォームブロックの `blocks/form` フォルダーでローカルの変更を行うことができます。このディレクトリ内の `.css` または `.js` ファイルを編集すると、変更がブラウザーに即座に反映されることがわかります。

変更が完了したら、Git コマンドを使用して変更をコミットおよびプッシュします。これにより、次の URL からアクセスできるプレビュー環境と実稼動環境が更新されます（プレースホルダーをプロジェクトの詳細に置き換えます）。

プレビュー：`https://<branch>--<repo>--<owner>.aem.page/content/<site-name>`

実稼動：`https://<branch>--<repo>--<owner>.aem.live/content/<site-name>`


## GitHub ビルドの問題のトラブルシューティング

潜在的な問題に対処することで、GitHub ビルドプロセスがスムーズに行われるようにします。

* **lint エラーの処理：**
lint エラーが発生した場合は、回避できます。 [EDS プロジェクト]/package.json ファイルを開き、「lint」スクリプトを `"lint": "npm run lint:js && npm run lint:css"` から `"lint": "echo 'skipping linting for now'"` に変更します。 ファイルを保存し、変更を GitHub プロジェクトにコミットします。

* **モジュールパスエラーの解決：**
「モジュール &#39;/scripts/lib-franklin.js&#39; へのパスを解決できません」というエラーが発生した場合は、[EDS プロジェクト]/blocks/forms/form.js ファイルに移動します。lib-franklin.js ファイルを aem.js ファイルに置き換えて、読み込みステートメントを更新します。

## 関連トピック

{{universal-editor-see-also}}
