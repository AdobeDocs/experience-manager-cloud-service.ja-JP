---
title: アダプティブFormsでテーマを作成して使用するにはどうすればよいですか？
description: テーマを使用して、コアコンポーネントを使用してアダプティブフォームのスタイルを設定し、視覚的な ID を付けることができます。 任意の数のアダプティブフォームで、テーマを共有できます。
exl-id: 11c52b66-dbb1-4c47-a94d-322950cbdac1
source-git-commit: 397e7d4f23202b8ae7419b0ad5436a6a10e2efb8
workflow-type: tm+mt
source-wordcount: '2678'
ht-degree: 18%

---

# アダプティブFormsのテーマ {#themes-for-af-using-core-components}

| バージョン | 記事リンク |
| -------- | ---------------------------- |
| AEM 6.5 | [ここをクリックしてください](https://experienceleague.adobe.com/docs/experience-manager-65/forms/adaptive-forms-core-components/create-or-customize-themes-for-adaptive-forms-core-components.html) |
| AEM as a Cloud Service | この記事 |

テーマを作成して適用し、アダプティブフォームのスタイルを設定することができます。 テーマには、コンポーネントとパネルのスタイルを設定するための詳細情報が含まれています。スタイルには、背景カラー、ステートカラー、透明度、配置、サイズなどのプロパティが含まれます。テーマを適用すると、指定したスタイルが対応するコンポーネントに反映されます。テーマは、アダプティブフォームを参照せずに独立して管理され、複数のアダプティブFormsで再利用できます。

## 使用可能なテーマ

Forms as a Cloud Serviceが提供する、コアコンポーネントベースのアダプティブFormsのテーマを以下に示します。

* [キャンバステーマ](https://github.com/adobe/aem-forms-theme-canvas)
* [WKND テーマ](https://github.com/adobe/aem-forms-theme-wknd)
* [EASEL のテーマ](https://github.com/adobe/aem-forms-theme-easel)

## テーマの構造について

テーマは、CSS ファイル、JavaScript ファイル、およびアダプティブFormsのスタイルを定義するリソース（アイコンなど）を含むパッケージです。 アダプティブフォームのテーマは、次のコンポーネントで構成される特定の組織に従います。

* `src/theme.scss`：このフォルダーには、テーマ全体に大きな影響を与える CSS ファイルが含まれます。 テーマのスタイル設定と動作を一元的に定義および管理できます。 このファイルを編集すると、テーマ全体で共通に適用される変更を加え、アダプティブFormsとAEM Sitesの両方のページの外観と機能に影響を与えることができます。

* `src/site`：このフォルダーには、AEMサイトのページ全体に適用される CSS ファイルが含まれます。 これらのファイルは、AEM Site のページの全体的な機能やレイアウトに影響を与えるコードとスタイルで構成されています。 ここで行った変更は、サイトのすべてのページに反映されます。 [使用するタイミング]

* `src/components`：このフォルダーの CSS ファイルは、AEMの個々のコアコンポーネント用に設計されています。 コンポーネント用の各専用フォルダーには、 `.scss` アダプティブフォーム内の特定のコンポーネントのスタイルを設定するファイル。 例えば、 /src/components/accordion/_accordion.scssファイルには、アダプティブFormsアコーディオンコンポーネントのスタイル情報が含まれています。

  ![アダプティブフォームベースのテーマ構造](/help/forms/assets/theme_structure.png)

* `src/resources`：このフォルダーには、アイコン、ロゴ、フォントなどの静的ファイルが含まれています。 これらのリソースは、テーマの視覚的要素と全体的なデザインを強化するために使用されます。

## テーマの作成

Forms as Cloud Serviceが提供する、コアコンポーネントベースのアダプティブFormsのテーマを以下に示します。

* [キャンバステーマ](https://github.com/adobe/aem-forms-theme-canvas)
* [WKND テーマ](https://github.com/adobe/aem-forms-theme-wknd)
* [EASEL のテーマ](https://github.com/adobe/aem-forms-theme-easel)

以下が可能です。 [新しいテーマを作成するために、これらのテーマをカスタマイズします。](#customize-a-theme-core-components).

![テーマのカスタマイズのワークフロー](/help/forms/assets/workflow-of-customization-of-theme.png)

## テーマのカスタマイズ {#customize-a-theme-core-components}

テーマのカスタマイズとは、テーマの外観を変更し、パーソナライズするプロセスを指します。 テーマをカスタマイズすると、デザイン要素、レイアウト、色、タイポグラフィ、および基になるコードが変更される場合があります。 テーマで提供される基本的な構造と機能を維持しながら、Web サイトやアプリケーションを独自のカスタマイズされた外観で作成できます。

### 前提条件 {#prerequisites-to-customize}

* に慣れてください。 [Cloud Manager でのパイプラインの設定](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/onboarding/journey/developers.html#setup-pipeline) また、パイプラインの設定方法に関する基本的な知識を持つことで、テーマのカスタマイズを効率的に管理およびデプロイできます。
* 方法を学ぶ [貢献者の役割を持つユーザーを構成する](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/onboarding/journey/assign-profiles-aem.html). 貢献者の役割を持つユーザーを構成する方法を理解すると、テーマのカスタマイズに必要な権限を付与できます。
* [Apache Maven の最新リリースをインストールします。](https://maven.apache.org/download.cgi) Apache Maven は、Java™プロジェクトで一般的に使用されるビルド自動化ツールです。 最新のリリースをインストールすると、テーマのカスタマイズに必要な依存関係が確保されます。
* プレーンテキストエディターをインストールします。例： Microsoft® Visual Studio Code。 Microsoft® Visual Studio Code などのプレーンテキストエディターを使用すると、テーマファイルの編集と変更を行う際に使いやすい環境を提供します。

### 環境の設定

* [アダプティブFormsコアコンポーネントの有効化](/help/forms/enable-adaptive-forms-core-components.md)  ローカル開発およびCloud Service環境に対して
* 設定 [フロントエンドデプロイメントパイプライン](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-wknd-tutorial-develop/enable-frontend-pipeline-devops/create-frontend-pipeline.html) Cloud Service環境用 または、後でパイプラインを設定し、デプロイメントパイプラインを設定する前に、テストとテーマを柔軟に優先順位付けし、調整することもできます。

<!-- 
To deploy your themes to a Forms as a Cloud Service environment, first test theme on a local development environment to address any issues. Once the theme is tested, configure the front-end deployment pipeline, which is responsible for deploying the themes.

These themes are deployed to a Forms as a Cloud Service environment via the front-end pipeline. You can configure the pipeline later also, after testing the theme on a local development environment. 

-->

前提条件を学習し、開発環境を設定した後、具体的な要件に従ってテーマをカスタマイズする準備が整いました。

### テーマのカスタマイズ {#steps-to-customize-a-theme-core-components}

テーマのカスタマイズは複数の手順で行います。 テーマをカスタマイズするには、次の手順を順に実行します。

1. [テーマの複製](#download-a-theme-core-components)
1. [テーマの名前を設定する](#set-name-of-theme)
1. [テーマのカスタマイズ](#customize-the-theme)
1. [テーマのテスト](#test-the-theme)
1. [テーマのデプロイ](#deploy-the-theme)

このドキュメントで示す例は、 **カンバス** テーマに関しては重要ですが、同じ手順を使用して任意のテーマを複製し、カスタマイズできることに注意してください。 これらの手順はどのテーマにも適用でき、特定のニーズに応じてテーマを変更できます。

#### 1.テーマを複製する {#download-a-theme-core-components}

コアコンポーネントベースのアダプティブFormsのテーマを複製するには、次のいずれかのテーマを選択します。

* [キャンバステーマ](https://github.com/adobe/aem-forms-theme-canvas)
* [WKND テーマ](https://github.com/adobe/aem-forms-theme-wknd)
* [EASEL のテーマ](https://github.com/adobe/aem-forms-theme-easel)

テーマを複製するには、次の手順に従います。

1. コマンドプロンプトまたはターミナルウィンドウをローカル開発環境で開きます。

1. を実行します。 `git clone` コマンドを使用してテーマを複製します。

   ```
      git clone [Path of Git Repository of the theme]
   ```

   次を [テーマの Git リポジトリのパス] を、テーマの対応する Git リポジトリの実際の URL に置き換えます。

   たとえば、キャンバステーマを複製するには、次のコマンドを実行します。

   ```
      git clone https://github.com/adobe/aem-forms-theme-canvas
   ```

   コマンドを正常に実行すると、そのテーマのローカルコピーが  `aem-forms-theme-canvas` フォルダー。


#### 2.テーマの名前を設定する {#set-name-of-theme}

1. テーマフォルダーをプレーンテキストエディターで開きます。 例えば、 `aem-forms-theme-canvas` Visual Studio Code Editor のフォルダー。

1. `aem-forms-theme-canvas` フォルダーに移動します。

1. 次のコマンドを実行します。

   ```
         code .
   ```

   ![テーマフォルダーをプレーンテキストエディターで開く](/help/forms/assets/aem-forms-theme-folder-in-vs-code.png)

   Visual Studio コードでフォルダが開きます。

1. `package.json` ファイルを編集用に開きます。

1. の値を設定します。 `name` および `description` 属性。

   name 属性は、「aem-forms-wknd-theme」などのテーマを一意に識別するために使用され、 **スタイル** タブ **フォーム作成ウィザード**. description 属性は、目的や設計されたシナリオなど、テーマに関する追加の詳細を提供します。 また、テーマのバージョン、説明、ライセンスを指定することもできます。

1. ファイルを保存して閉じます。

![キャンバステーマ名の変更画像](/help/forms/assets/changename_canvastheme.png)


#### 3.テーマをカスタマイズする {#customize-the-theme}

個々のコンポーネントをカスタマイズしたり、テーマのグローバル変数を使用してテーマレベルの変更を行ったりできます。 グローバル変数に対して行った変更は、個々のコンポーネントすべてに影響を与えます。 例えば、グローバル変数を使用してアダプティブフォームのすべてのコンポーネントの境界線の色を変更したり、明るい塗りの色を使用して、ボタンコンポーネントを使用して CTA(Call to action) を設定したりできます。

* [テーマレベルのスタイルを設定する](#theme-customization-global-level)

* [コンポーネントレベルスタイルを設定する](#component-based-customization)

##### テーマレベルのスタイルを設定する{#theme-customization-global-level}

The `variable.scss` ファイルには、テーマのグローバル変数が含まれます。 これらの変数を更新すると、テーマレベルでスタイル関連の変更を行うことができます。 テーマレベルのスタイルを適用するには、次の手順に従います。

1. `<your-theme-sources>/src/site/_variables.scss` ファイルを編集用に開きます。
1. 任意のプロパティの値を変更します。 例えば、デフォルトのエラー色は次のようになります。 `red`. エラーの色を次のように変更するには： `red` から `blue`を変更する場合は、 `$errorvariable`. 例：`$error: #196ee5`
1. ファイルを保存して閉じます。

   ![テーマを編集](/help/forms/assets/edit_theme.png)

同様に、 `variable.scss` ファイル：複数のアダプティブフォームコンポーネントに影響を与えるフォントファミリーと種類、テーマとフォントの色、フォントサイズ、テーマの間隔、エラーアイコン、テーマの境界線のスタイル、その他の変数を設定します。

##### コンポーネントレベルスタイルを設定する {#component-based-customization}

また、特定のアダプティブフォームコアコンポーネントのフォント、色、サイズ、およびその他の CSS プロパティを変更することもできます。 （ボタン、チェックボックス、コンテナ、フッターなど）。 特定のコンポーネントの CSS ファイルを編集して、組織のスタイルに合わせてボタンやチェックボックスのスタイルを設定できます。 コンポーネントのスタイルをカスタマイズするには：

1. ファイルを開きます。 `<your-theme-sources>/src/components/<component>/<component.scss>` （編集用）。 例えば、ボタンコンポーネントのフォントカラーを変更するには、 `<your-theme-sources>/src/components/button/button.scss`、ファイル。
1. 必要に応じて、の値を変更します。 例えば、マウスポインターを置いたときのボタンコンポーネントの色をに変更するには、次のように指定します。 `green`を変更した場合、 `color: $white` プロパティを `cmp-adaptiveform-button__widget:hover` クラスを 16 進コードに `#12B453` その他の幾分かの `green`. 最終的なコードは次のようになります。

   ```
   .cmp-adaptiveform-button__widget:hover {
   background: $dark-gray;
   color: #12B453;
   }
   ```

1. ファイルを保存して閉じます。

   ![テキストボックス CSS の編集](/help/forms/assets/edit_color_textbox.png)

   >
   >
   > テーマレベルとコンポーネントレベルの両方でスタイルを定義する場合、コンポーネントレベルで定義されたスタイルが優先されます。

#### 4.カスタマイズされたテーマをテストする {#test-the-theme}

ローカル環境で変更をプレビューおよびテストし、様々なAEMコンポーネントの要件に応じてテーマをカスタマイズするには、次の手順を実行します。

* 4.1 [テスト用のローカル環境の設定](#rename-env-file-theme-folder)
* 4.2 [ローカル環境を使用したテーマのテスト](#start-a-local-proxy-server)

##### 4.1.テスト用のローカル環境の設定 {#rename-env-file-theme-folder}

1. テーマフォルダーをプレーンテキストエディターで開きます。 例えば、 `aem-forms-theme-canvas` Visual Studio Code Editor のフォルダー。
1. 名前を変更 `env_template` ～にファイルを送る `.env` theme フォルダーにファイルを作成し、次のパラメーターを追加します。

   ```
   * **AEM url**
   AEM_URL=https://[author-instance] 
   
   * **AEM Adaptive form name**
   AEM_ADAPTIVE_FORM=Form_name
   
   * **AEM proxy port**
   AEM_PROXY_PORT=7000
   ```

   例えば、フォームの URL が `http://localhost:4502/editor.html/content/forms/af/contactusform.html`. したがって、次の値が適用されます。

   * AEM_URL = `http://localhost:4502/`
   * AEM_ADAPTIVE_FORM = `contactusform`

1. ファイルを保存します。

   ![キャンバステーマの構造](/help/forms/assets/env-file-canvas-theme.png)

##### 4.2 ローカル環境でテストする {#start-a-local-proxy-server}

1. テーマフォルダーのルートに移動します。 この場合、テーマのフォルダー名は次のようになります。 `aem-forms-theme-canvas`.
1. コマンドプロンプトまたはターミナルを開きます。
1. 実行 `npm install` 依存関係をインストールする。
1. 実行 `npm run live` 更新されたテーマを使用してフォームをローカルブラウザーでプレビューする場合。

   >[!NOTE]
   >
   > の実行中にエラーが発生した場合、 `npm run live` コマンド、前に次のコマンドを実行します。 `npm run live` コマンド：
   >
   > * `npm install parcel --save-dev`
   > * `npm i @parcel/transformer-sass`

これはホットデプロイメントです。 したがって、変更を加えて `_variables.scss` および `button.scss` ファイルを選択すると、サーバーは自動的に変更を選択し、最新の出力をプレビューします。 行 `[Browsersync] File event [change]` は、サーバが最新の変更を認識し、ローカル環境に変更をデプロイしていることを示します。

![プロキシブラウザー同期](/help/forms/assets/browser_sync.png)

テーマのカスタマイズに関して、テーマレベルとコンポーネントレベルの両方で示される例に従った後、アダプティブフォームのエラーメッセージは、 `blue` color ボタンコンポーネントのラベルの色が `green` ホバリングの時に

**テーマレベルスタイルのプレビュー**

![例：エラーの色を青に設定](/help/forms/assets/theme-level-changes.png)

**コンポーネントレベルスタイルのプレビュー**

![例：カーソルを合わせるときのカラーが緑に設定される](/help/forms/assets/button-customization.png)

###### テーマ環境でホストされるフォームのCloud Serviceをテストする

また、AEM Formsas a Cloud Serviceインスタンスでホストされるアダプティブフォームのテーマをテストすることもできます。 クラウドインスタンス上でホストされるアダプティブFormsを使用してテーマをテストするためのローカル環境を設定および設定するには、次の手順を実行します。

1. テーマフォルダーをプレーンテキストエディターで開きます。 例えば、 `aem-forms-theme-canvas` Visual Studio Code Editor のフォルダー。
1. 名前を変更 `env_template` ～にファイルを送る `.env` ファイルを開き、次のパラメーターを追加します。

   ```
   * **AEM url**
   AEM_URL=https://[author-instance] 
   
   * **AEM Adaptive form name**
   AEM_ADAPTIVE_FORM=Form_name
   
   * **AEM proxy port**
   AEM_PROXY_PORT=7000
   ```

   例えば、クラウド環境のフォームの URL が次のようになっているとします。 `https://author-XXXX.adobeaemcloud.com/editor.html/content/forms/af/contactusform.html`. したがって、次の値が適用されます。

   * AEM_URL = `https://author-XXXX-cmstg.adobeaemcloud.com/`
   * AEM_ADAPTIVE_FORM = `contactusform`
1. ファイルを保存します。
1. ローカルユーザーを作成します。

   >[!NOTE]
   >
   > ローカルユーザーを作成するには：
   >
   > * に移動します。 **[!UICONTROL AEM Home]** > **[!UICONTROL ツール]** > **[!UICONTROL セキュリティ]** > **[!UICONTROL ユーザー]** .
   > * ユーザーが `forms-users` グループ化します。

1. テーマフォルダーのルートに移動します。 この場合、テーマのフォルダー名は次のようになります。 `aem-forms-theme-canvas`.
1. 実行 `npm run live` ローカルブラウザーにリダイレクトされます。
1. クリック `SIGN IN LOCALLY (ADMIN TASKS ONLY)` ローカルユーザーの資格情報を使用してログインします。

最新の変更を含むアダプティブフォームをプレビューできます。 テーマフォルダーでの変更内容が完了したら、フロントエンドパイプラインを使用してAEM Cloud Service環境にテーマをデプロイします。

#### 5.テーマをデプロイする {#deploy-the-theme}

フロントエンドパイプラインを使用してCloud Service環境にテーマをデプロイするには：

* 5.1 [テーマのリポジトリを作成する](#create-a-new-theme-repo)
* 5.2 [変更をリポジトリにプッシュ](#committing-the-changes)
* 5.3 [フロントエンドパイプラインの実行](#run-a-frontend-pipeline)

##### 5.1 テーマのリポジトリを作成する{#create-a-new-theme-repo}

テーマをデプロイするには、リポジトリが必要です。 にログインします。 [AEM Cloud Manager リポジトリ](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/onboarding/journey/developers.html#accessing-git) テーマの新しいリポジトリを追加します。

1. テーマの新しいリポジトリを作成するには、 **[!UICONTROL リポジトリ]** > **[!UICONTROL リポジトリを追加]**.

   ![新しいテーマリポジトリの作成](/help/forms/assets/createrepo_canvastheme.png)


1. 次を指定します。 **リポジトリ名** （内） **リポジトリを追加** ダイアログボックス。 例えば、指定した名前は次のようになります。 `custom-canvas-theme-repo`.
1. 「**[!UICONTROL 保存]**」をクリックします。

   ![キャンバステーマリポジトリの追加](/help/forms/assets/addcanvasthemerepo.png)

1. クリック **[!UICONTROL リポジトリ URL をコピー]** をクリックして、リポジトリの URL をコピーします。

   ![キャンバステーマの URL](/help/forms/assets/copyurl_canvastheme.png)

   >[!NOTE]
   > 
   > * 1 つのリポジトリを複数のテーマに使用できます。
   > * 異なるテーマをデプロイするには、別々のフロントエンドパイプラインを作成する必要があります。
   >* 例えば、 `custom-canvas-theme-repo`、キャンバステーマ、WKND テーマ、EASEL テーマ用。 ただし、テーマをデプロイするには、別々のフロントエンドパイプラインを作成する必要があります。 対応するフロントエンドパイプラインを使用して、特定のテーマの将来のカスタマイズがデプロイされます。

##### 5.2.リポジトリに変更をプッシュします。 {#committing-the-changes}

次に、変更をAEM FormsCloud Serviceのテーマリポジトリにプッシュします。.

1. テーマフォルダーのルートに移動します。  この場合、テーマのフォルダー名は次のようになります。 `aem-forms-theme-canvas`.
1. コマンドプロンプトまたはターミナルを開きます。
1. 次のコマンドを一覧の順序で実行します。

   ```
   git remote add [alias-name-for-repository] [URL of repository]
   git add .
   git commit
   git push [name-for-createdrepository]
   ```

   次に例を示します。

   ```
   git remote add canvascloudthemerepo https://git.cloudmanager.adobe.com/stage-aemformsdev/customcanvastheme/
   git add .
   git commit
   git push canvascloudthemerepo 
   ```

   ![コミット済みの変更](/help/forms/assets/cmd_git_push.png)



##### 5.3 フロントエンドパイプラインの実行 {#run-a-frontend-pipeline}

テーマは、 [フロントエンドパイプライン。](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-wknd-tutorial-develop/enable-frontend-pipeline-devops/create-frontend-pipeline.html)。テーマをデプロイするには、次の手順を実行します。

1. AEM Cloud Manager リポジトリにログインします。
1. クリック **[!UICONTROL 追加]** ボタンを **[!UICONTROL パイプライン]** 」セクションに入力します。
1. 選択 **[!UICONTROL 実稼動以外のパイプラインを追加]** または **[!UICONTROL 実稼動パイプラインを追加]** Cloud Service環境に基づく 例えば、次に例を示します。 **[!UICONTROL 実稼動パイプラインを追加]** 」オプションが選択されている。
1. Adobe Analytics の **[!UICONTROL 実稼動パイプラインを追加]** ～の一部としての対話 **[!UICONTROL 設定]** ステップで、パイプラインの名前を指定します。 例えば、パイプラインの名前は `customcanvastheme`.
1. 「**[!UICONTROL 続行]**」をクリックします。
1. を選択します。 **[!UICONTROL ターゲットのデプロイメント]** > **[!UICONTROL フロントエンドコード]** オプション、 **[!UICONTROL ソースコード]** 手順。
1. を選択します。 **[!UICONTROL リポジトリ]** そして **[!UICONTROL Git ブランチ]** 最新の変更を含む値。 例えば、ここで選択したリポジトリ名は次のようになります。 `custom-canvas-theme-repo` また、Git ブランチは `main`.
1. を選択します。 **[!UICONTROL コードの場所]** as `/`変更がルートフォルダーに存在する場合は、をクリックします。
1. 「**[!UICONTROL 保存]**」をクリックします。
   ![フロントエンドパイプラインの作成](/help/forms/assets/canvas-theme-frontendpipeline.gif)

   パイプラインの設定が完了したら、コールトゥアクションカードが更新されます。

1. 作成したパイプラインを右クリックします。
1. 「**[!UICONTROL 実行]**」をクリックします。

   ![ランパイプリン](/help/forms/assets/canvas-theme-run-pipeline.png)

ビルドが完了すると、オーサーインスタンスでテーマを使用できるようになります。 これは、 **[!UICONTROL スタイル]** 新しいアダプティブフォームの作成時に、アダプティブフォーム作成ウィザードのタブをクリックします。

![「スタイル」タブで使用可能なカスタムテーマ](/help/forms/assets/custom-theme-style-tab.png)

## テーマをアダプティブフォームに適用する {#using-theme-in-adaptive-form}

アダプティブフォームにテーマを適用する手順は次のとおりです。

1. AEM Forms オーサーインスタンスにログインします。

1. **Adobe Experience Manager**／**Forms**／**フォームとドキュメント**&#x200B;の順にタップします。

1. **作成**／**アダプティブフォーム**&#x200B;の順にクリックします。アダプティブフォームを作成するためのウィザードが開きます。

1. 「**ソース**」タブでコアコンポーネントテンプレートを選択します。
1. テーマを **スタイル** タブをクリックします。
1. 「**作成**」をクリックします。

アダプティブフォームのテーマは、アダプティブフォームの作成時にスタイルを定義する、アダプティブフォームのテンプレートの一部として使用されます。

## ベストプラクティス {#best-practices}

* **別のテーマに属するアセットの回避**

  テーマを編集する際、アセット（画像など）を他のテーマから参照して追加することができます。例えば、ページの背景を編集しているとします。例えば、**[!UICONTROL ページ]** ![edit-button](assets/edit-button.png)／**[!UICONTROL 背景]**／**[!UICONTROL 追加]**／**[!UICONTROL 画像]**&#x200B;を選択すると、他のテーマの画像を参照して追加することが可能なダイアログが表示されます。

  アセットを別のテーマから追加し、そのテーマが移動または削除されると、現在のテーマに問題が生じる場合があります。他のテーマからアセットを参照して追加しないようにすることをお勧めします。

* **コンテナパネルのレイアウト幅の変更**

  コンテナパネルのレイアウト幅の変更はお勧めしません。コンテナパネルの幅を指定すると、幅が静的になり、様々なディスプレイに合わせて調整されません。

* **ヘッダーとフッターを操作する際のフォームエディターまたはテーマエディターの使用**

  テーマエディターは、フォントスタイル、背景、透明度などのスタイル設定オプションを使用してヘッダーとフッターのスタイルを設定する場合に使用します。
ヘッダーにロゴイメージや企業名などの情報を表示し、フッターに著作権情報を表示する場合は、フォームエディターのオプションを使用します。

## よくある質問 {#faq}

**Q:** テーマフォルダーのカスタマイズをグローバルレベルとコンポーネントレベルの両方で行う場合、どのカスタマイズが優先されますか？

**回答：** グローバルレベルとコンポーネントレベルの両方でカスタマイズが行われる場合は、コンポーネントレベルでのカスタマイズが優先されます。

<!--

## See next

* [Set layout of forms for different screen sizes and device types](/help/sites-cloud/authoring/features/responsive-layout.md)
* [Generate Document of Record for Adaptive Forms (Core Components](/help/forms/generate-document-of-record-for-non-xfa-based-adaptive-forms.md)
* [Create an Adaptive Forms with Repeatable sections](/help/forms/create-forms-repeatable-sections.md)
* [Sample themes templates and form data models](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/sample-themes-templates-form-data-models-core-components.html)


>[!MORELIKETHIS]
>
>* [Enable Adaptive Forms Core Components on AEM Forms as a Cloud Service and local development environment](/help/forms/enable-adaptive-forms-core-components.md)

-->


## 関連トピック {#see-also}

{{see-also}}

* [画面サイズやデバイスタイプに応じてフォームのレイアウトを設定](/help/sites-cloud/authoring/features/responsive-layout.md)
* [アダプティブForms（コアコンポーネント）用のレコードのドキュメントを生成する](/help/forms/generate-document-of-record-for-non-xfa-based-adaptive-forms.md)
* [繰り返し可能なセクションを使用したアダプティブFormsの作成](/help/forms/create-forms-repeatable-sections.md)
* [サンプルのテーマテンプレートとフォームデータモデル](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/sample-themes-templates-form-data-models-core-components.html)
* [AEM Forms as a Cloud Service およびローカル開発環境で、アダプティブフォームのコアコンポーネントを有効にする](/help/forms/enable-adaptive-forms-core-components.md)
