---
title: アダプティブFormsのテーマの作成方法と使用方法？
description: テーマとコアコンポーネントを使用して、アダプティブフォームのスタイルを設定し、視覚的に表現できます。任意の数のアダプティブフォームで、テーマを共有できます。
keywords: フォームビルダーテーマ、アダプティブフォームのスタイル設定コアコンポーネント、フォームテーマビルダー、アダプティブフォームのスタイル設定、テーマのカスタマイズ、フォームテーマの作成
feature: Adaptive Forms, Core Components
role: User, Developer
exl-id: 11c52b66-dbb1-4c47-a94d-322950cbdac1
source-git-commit: ab84a96d0e206395063442457a61f274ad9bed23
workflow-type: tm+mt
source-wordcount: '2806'
ht-degree: 99%

---

# テーマを使用したコアコンポーネントベースのアダプティブフォームのスタイル設定{#themes-for-af-using-core-components}

| バージョン | 記事リンク |
| -------- | ---------------------------- |
| AEM 6.5 | [ここをクリックしてください](https://experienceleague.adobe.com/docs/experience-manager-65/forms/adaptive-forms-core-components/create-or-customize-themes-for-adaptive-forms-core-components.html?lang=ja) |
| AEM as a Cloud Service | この記事 |

アダプティブフォームのスタイル設定にテーマを作成して適用できます。テーマには、コンポーネントとパネルのスタイルを設定するための詳細情報が含まれています。スタイルには、背景カラー、ステートカラー、透明度、配置、サイズなどのプロパティが含まれます。テーマを適用すると、指定したスタイルが対応するコンポーネントに反映されます。テーマは、アダプティブフォームを参照せずに独立して管理され、複数のアダプティブフォームで再利用できます。

この記事では、テーマを使用してコアコンポーネントベースのアダプティブフォームのカスタム外観を設計する方法について説明します。

## コアコンポーネントのスタイル設定に使用できるテーマ

Forms as Cloud Service が提供する、コアコンポーネントベースのアダプティブフォームのテーマを以下に示します。

* [キャンバステーマ](https://github.com/adobe/aem-forms-theme-canvas)
* [WKND テーマ](https://github.com/adobe/aem-forms-theme-wknd)
* [イーゼルテーマ](https://github.com/adobe/aem-forms-theme-easel)

## テーマの構造について

テーマは、アダプティブフォームのスタイルを定義する CSS ファイル、JavaScript ファイル、リソース（アイコンなど）などのスタイル設定コンポーネントが含まれたパッケージです。アダプティブフォームのテーマは、次のコンポーネントで構成される特定の組織に従います。

* `src/theme.scss`：このフォルダーには、テーマ全体に大きな影響を与える CSS ファイルが含まれます。テーマのスタイル設定と動作を一元的に定義および管理できます。このファイルを編集するとテーマ全体で共通して適用され、アダプティブフォームと AEM Sites の両方のページの外観と機能を変更することができます。

* `src/site`：このフォルダーには、AEM Sites のページ全体に適用される CSS ファイルが含まれます。これらのファイルは、AEM Sites のページの全体的な機能やレイアウトを対象とするコードとスタイルで構成されています。ここで行った変更は、サイトのすべてのページに反映されます。[使用するタイミング]

* `src/components`：このフォルダーの CSS ファイルは、AEM の個々のコアコンポーネント用に設計されています。コンポーネント用の各専用フォルダーには、アダプティブフォーム内の特定のコンポーネントのスタイルを設定する `.scss` ファイルが含まれています。例えば、/src/components/accordion/_accordion.scss ファイルには、アダプティブフォームのアコーディオンコンポーネント向けのスタイル情報が含まれています。

  ![アダプティブフォームベースのテーマ構造](/help/forms/assets/theme_structure.png)

* `src/resources`：このフォルダーには、アイコン、ロゴ、フォントなどの静的ファイルが含まれています。これらのリソースは、テーマの視覚的要素と全体的なデザインを強化するために使用されます。

## テーマの作成

Forms as Cloud Service が提供する、コアコンポーネントベースのアダプティブフォームのアダプティブフォームスタイル設定テーマを以下に示します。

* [キャンバステーマ](https://github.com/adobe/aem-forms-theme-canvas)
* [WKND テーマ](https://github.com/adobe/aem-forms-theme-wknd)
* [イーゼルテーマ](https://github.com/adobe/aem-forms-theme-easel)

[これらのテーマをカスタマイズしてテーマを作成](#customize-a-theme-core-components)することができます。

![テーマのカスタマイズのワークフロー](/help/forms/assets/workflow-of-customization-of-theme.png)

## テーマのカスタマイズ {#customize-a-theme-core-components}

テーマのカスタマイズとは、テーマのアピアランスを変更し、スタイル設定し、パーソナライズするプロセスを指します。テーマをカスタマイズすると、デザイン要素、レイアウト、色、テキスト編集、基になるコードに変更を加えることができます。それにより、テーマで提供される基本的な構造と機能を維持しながら、web サイトやアプリケーションに独自のカスタマイズされたアピアランスを作成できます。

### 前提条件 {#prerequisites-to-customize}

* [Cloud Manager でのパイプラインの設定](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/onboarding/journey/developers.html?lang=ja#setup-pipeline)に慣れてください。また、パイプラインの設定方法に関する基本的な知識を持つことで、テーマのカスタマイズを効率的に管理およびデプロイできます。
* [投稿者の役割を持つユーザーを設定する](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/onboarding/journey/assign-profiles-aem.html?lang=ja)方法を説明します。投稿者の役割を持つユーザーを設定する方法を理解すると、テーマのカスタマイズに必要な権限を付与できます。
* [Apache Maven](https://maven.apache.org/download.cgi) の最新リリースのインストール。Apache Maven は、主に Java™ プロジェクトで使用されるビルド自動化ツールです。最新のリリースをインストールすると、テーマのカスタマイズに必要な依存関係が確保されます。
* プレーンテキストエディターをインストールします。例えば Microsoft® Visual Studio Code などです。Microsoft® Visual Studio Code などのプレーンテキストエディターを使用すると、テーマファイルの編集と変更を行う際に使いやすい環境を利用できます。

### 環境の設定

* お使いの AEM Cloud Service 環境でアダプティブフォームコアコンポーネントを有効にするには、最新版をインストールします。
* Cloud Service 環境用に[フロントエンドデプロイメントパイプライン](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-wknd-tutorial-develop/enable-frontend-pipeline-devops/create-frontend-pipeline.html?lang=ja)を設定します。または、後でパイプラインを設定することもできるため、デプロイメントパイプラインを設定する前に、テーマのテストと調整に優先順位を付けることができます。

<!-- 
To deploy your themes to a Forms as a Cloud Service environment, first test theme on a local development environment to address any issues. Once the theme is tested, configure the front-end deployment pipeline, which is responsible for deploying the themes.

These themes are deployed to a Forms as a Cloud Service environment via the front-end pipeline. You can configure the pipeline later also, after testing the theme on a local development environment. 

-->

前提条件を把握し、開発環境を設定したら、具体的な要件に従ってテーマをカスタマイズまたはスタイル設定する準備が整います。

### テーマのカスタマイズ {#steps-to-customize-a-theme-core-components}

テーマのカスタマイズは複数の手順で行います。テーマをカスタマイズするには、次の手順を順に実行します。

1. [テーマの複製](#download-a-theme-core-components)
1. [テーマの名前の設定](#set-name-of-theme)
1. [テーマのカスタマイズ](#customize-the-theme)
1. [テーマのテスト](#test-the-theme)
1. [テーマのデプロイ](#deploy-the-theme)

このドキュメントで示す例は、**カンバス**&#x200B;テーマに基づいていますが、同じ手順を使用して任意のテーマを複製し、カスタマイズできることに注意してください。これらの手順はどのテーマにも適用でき、特定のニーズに応じてテーマを変更できます。

まず、テーマを使用して、コアコンポーネントベースのアダプティブフォームのブランドエクスペリエンスを作成するプロセスから始めましょう。

#### &#x200B;1. テーマの複製 {#download-a-theme-core-components}

コアコンポーネントベースのアダプティブフォームのテーマを複製するには、次のいずれかのテーマを選択します。

* [キャンバステーマ](https://github.com/adobe/aem-forms-theme-canvas)
* [WKND テーマ](https://github.com/adobe/aem-forms-theme-wknd)
* [イーゼルテーマ](https://github.com/adobe/aem-forms-theme-easel)

テーマをコピーするには、次の手順を実行します。

1. コマンドプロンプトまたはターミナルウィンドウをローカル開発環境で開きます。

1. `git clone` コマンドを実行して、テーマを複製します。

   ```
      git clone [Path of Git Repository of the theme]
   ```

   [テーマの Git リポジトリのパス]を、テーマの対応する Git リポジトリの実際の URL に置き換えます。

   例えば、キャンバステーマを複製するには、次のコマンドを実行します。

   ```
      git clone https://github.com/adobe/aem-forms-theme-canvas
   ```

   コマンドを正常に実行すると、マシンの `aem-forms-theme-canvas` フォルダーにテーマのローカルコピーが作成されます。


#### &#x200B;2. テーマの名前の設定 {#set-name-of-theme}

1. IDE でテーマフォルダーを開きます。例えば、Visual Studio Code Editor の `aem-forms-theme-canvas` フォルダーを開きます。

1. `aem-forms-theme-canvas` フォルダーに移動します。

1. 次のコマンドを実行します。

   ```
      code .
   ```

   ![テーマフォルダーをプレーンテキストエディターで開く](/help/forms/assets/aem-forms-theme-folder-in-vs-code.png)

   Visual Studio Code でフォルダーが開きます。

1. `package.json` ファイルを編集用に開きます。

1. `name` および `version` 属性の値を設定します。

   ![キャンバステーマ名の変更画像](/help/forms/assets/changename_canvastheme.png)

   >[!NOTE]
   >
   > * name 属性は、テーマを一意に識別するのに使用され、指定した名前が&#x200B;**フォーム作成ウィザード**&#x200B;の「**スタイル**」タブに表示されます。
   > * 選択に応じて、テーマの名前を選択できます（`mytheme` または `customtheme` など）。ここでは、名前を `aem-forms-wknd-theme` に指定します。

1. `package-lock.json` ファイルを編集用に開きます。
1. `name` および `version` の属性の値を設定します。`Package-lock`.json ファイルの `name` および `version` の属性の値は、`Package.json` ファイルの値と一致する必要があります。

   ![キャンバステーマ名の変更画像](/help/forms/assets/changename_canvastheme-package-lock.png)

1. （オプション）`ReadMe` ファイルを編集用に開いて、テーマの名前を更新します。

   ![キャンバステーマ名の変更画像](/help/forms/assets/changename_canvastheme-readme-file.png)

1. ファイルを保存して閉じます。

**テーマの名前を設定する際の考慮事項**

* `Package.json` ファイルと `Package-lock.json` ファイルのテーマの名前から `@aemforms` を削除する必要があります。カスタマイズしたテーマの名前から `@aemforms` を削除できない場合は、テーマのデプロイメント中にフロントエンドパイプラインが失敗します。
* テーマに対する時間の経過に伴う変更や機能強化が正確に反映されるよう、`Package.json` ファイルと `Package-lock.json` ファイルのテーマ `version` を更新することをお勧めします。
* 使用方法、インストール手順、その他の関連する詳細についての重要な情報は、`ReadMe` ファイルでテーマ名を更新することをお勧めします。

#### &#x200B;3. テーマのカスタマイズ {#customize-the-theme}

個々のコンポーネントをカスタマイズしたり、テーマのグローバル変数を使用してテーマのレベルを変更したりすることができます。グローバル変数に対して行った変更は、すべての個々のコンポーネントに影響を与えます。例えば、グローバル変数を使用してアダプティブフォームのすべてのコンポーネントの境界線の色を変更したり、明るい塗りつぶしの色とボタンコンポーネントを使用して CTA（コールトゥアクション）を設定したりできます。

* [テーマレベルのスタイルの設定](#theme-customization-global-level)

* [コンポーネントレベルのスタイルの設定](#component-based-customization)

##### テーマレベルのスタイルの設定{#theme-customization-global-level}

`variable.scss` ファイルには、テーマのグローバル変数が含まれます。これらの変数を更新すると、テーマレベルでスタイル関連の変更を行うことができます。テーマレベルのスタイルを適用するには、次の手順に従います。

1. `<your-theme-sources>/src/site/_variables.scss` ファイルを編集用に開きます。
1. 任意のプロパティの値を変更します。例えば、エラーのデフォルトの色は `red` ですが、これを `red` から `blue` に変更する場合は、`$errorvariable` の16 進数カラーコードを変更します。例：`$error: #196ee5`。
1. ファイルを保存して閉じます。

   ![テーマを編集](/help/forms/assets/edit_theme.png)

同様に `variable.scss` ファイルを使って、複数のアダプティブフォームコンポーネントに影響を与えるフォントのファミリーと種類、テーマとフォントの色、フォントのサイズ、テーマの間隔、エラーアイコン、テーマの境界線のスタイル、その他の変数を設定します。

##### コンポーネントレベルのスタイルの設定 {#component-based-customization}

また、アダプティブフォームの特定のコアコンポーネントのフォント、色、サイズ、およびその他の CSS プロパティを変更することもできます（ボタン、チェックボックス、コンテナ、フッターなど）。組織のスタイルに合わせて特定のコンポーネントの CSS ファイルを編集して、ボタンやチェックボックスのスタイルを設定できます。コンポーネントのスタイルをカスタマイズするには：

1. 編集するために `<your-theme-sources>/src/components/<component>/<component.scss>` ファイルを開きます。例えば、ボタンコンポーネントのフォントの色を変更するには、`<your-theme-sources>/src/components/button/button.scss` ファイルを開きます。
1. 必要に応じて値を変更します。例えば、マウスポインターを置いたときのボタンコンポーネントの色を `green` に変更するには、`cmp-adaptiveform-button__widget:hover` クラスの `color: $white` プロパティの値を 16 進数コードコードの `#12B453`、またはその他の `green` の色に変更します。最終的なコードは次のようになります。

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
   > テーマレベルとコンポーネントレベルの両方でスタイルを定義する場合は、コンポーネントレベルで定義されたスタイルが優先されます。

#### &#x200B;4. カスタマイズされたテーマのテスト {#test-the-theme}

ローカル環境で変更をプレビューおよびテストし、様々な AEM コンポーネントの要件に応じてテーマをカスタマイズするには、次の手順を実行します。

* 4.1 [テスト用のローカル環境の設定](#rename-env-file-theme-folder)
* 4.2 [ローカル環境を使用してテーマをテストする](#start-a-local-proxy-server)

##### 4.1. テスト用のローカル環境の設定 {#rename-env-file-theme-folder}

1. IDE でテーマフォルダーを開きます。例えば、Visual Studio Code エディターの `aem-forms-theme-canvas` フォルダーを開きます。
1. テーマフォルダーで `env_template` ファイルの名前を `.env` ファイルに変更し、次のパラメーターを追加します。

   ```
   * **AEM url**
   AEM_URL=https://[author-instance] 
   
   * **AEM Adaptive form name**
   AEM_ADAPTIVE_FORM=Form_name
   
   * **AEM proxy port**
   AEM_PROXY_PORT=7000
   ```

   例えば、フォームの URL が `http://localhost:4502/editor.html/content/forms/af/contactusform.html` です。したがって、次の値：

   * AEM_URL = `http://localhost:4502/`
   * AEM_ADAPTIVE_FORM = `contactusform`

1. ファイルを保存します。

   ![キャンバステーマの構造](/help/forms/assets/env-file-canvas-theme.png)

##### 4.2 ローカル環境を使用したテーマのテスト {#start-a-local-proxy-server}

1. テーマフォルダーのルートに移動します。この場合、テーマのフォルダー名は `aem-forms-theme-canvas` です。
1. コマンドプロンプトまたはターミナルを開きます。
1. `npm install` を実行して依存関係をインストールします。
1. `npm run live` を実行して、更新されたテーマを使用したフォームをローカルブラウザーでプレビューする場合。

   >[!NOTE]
   >
   > `npm run live` コマンドの実行中にエラーが発生した場合、`npm run live` コマンドの前に次のコマンドを実行します。
   >
   > * `npm install parcel --save-dev`
   > * `npm i @parcel/transformer-sass`

これはホットデプロイメントです。したがって、変更を加えて `_variables.scss` および `button.scss` ファイルを保存すると、サーバーは自動的に変更を選択し、最新の出力をプレビューします。行 `[Browsersync] File event [change]` は、サーバが最新の変更を認識し、ローカル環境に変更をデプロイしていることを示します。

![プロキシブラウザー同期](/help/forms/assets/browser_sync.png)

テーマのカスタマイズに関して、テーマレベルとコンポーネントレベルの両方でアダプティブフォーム（コアコンポーネント）のスタイル設定の例に従うと、アダプティブフォームのエラーメッセージの色は `blue` に変わりますが、ボタンコンポーネントのラベルの色はカーソルを合わせると `green` になります。

**テーマレベルスタイルのプレビュー**

![例：エラーを青色に設定](/help/forms/assets/theme-level-changes.png)

**コンポーネントレベルスタイルのプレビュー**

![例：カーソルを合わせるときのカラーを緑色に設定](/help/forms/assets/button-customization.png)

テーマをカスタマイズすると、組織の要件に応じて、コアコンポーネントベースのアダプティブフォームのカスタム外観を設計するのに役立ちます。

###### Cloud Service 環境でホストされるフォームのテーマをテストする

また、AEM Forms as a Cloud Serviceインスタンスでホストされるアダプティブフォームのテーマをテストすることもできます。クラウドインスタンス上でホストされるアダプティブフォームを使用して、テーマをテストするためのローカル環境を設定するには、次の手順を実行します。

1. IDE でテーマフォルダーを開きます。例えば、Visual Studio Code エディターの `aem-forms-theme-canvas` フォルダーを開きます。
1. `env_template` ファイルを `.env` ファイルに名前を変更し、次のパラメーターを追加します。

   ```
   * **AEM url**
   AEM_URL=https://[author-instance] 
   
   * **AEM Adaptive form name**
   AEM_ADAPTIVE_FORM=Form_name
   
   * **AEM proxy port**
   AEM_PROXY_PORT=7000
   ```

   例えば、クラウド環境のフォームの URLは `https://author-XXXX.adobeaemcloud.com/editor.html/content/forms/af/contactusform.html` です。したがって、次の値：

   * AEM_URL = `https://author-XXXX-cmstg.adobeaemcloud.com/`
   * AEM_ADAPTIVE_FORM = `contactusform`
1. ファイルを保存します。
1. ローカルユーザーを作成します。

   >[!NOTE]
   >
   > ローカルユーザーを作成するには、以下の手順に従います。
   >
   > * **[!UICONTROL AEM ホーム]**／**[!UICONTROL ツール]**／**[!UICONTROL セキュリティ]**／**[!UICONTROL ユーザー]**&#x200B;に移動します。
   > * ユーザーが `forms-users` グループのメンバーであることを確認してください。

1. テーマフォルダーのルートに移動します。この場合、テーマのフォルダー名は `aem-forms-theme-canvas` です。
1. `npm run live` を実行すると、ローカルブラウザーにリダイレクトされます。
1. `SIGN IN LOCALLY (ADMIN TASKS ONLY)` をクリックして、ローカルユーザーの資格情報を使用してログインします。

最新の変更を含むアダプティブフォームをプレビューできます。テーマフォルダーでの変更内容が完了したら、フロントエンドパイプラインを使用して、AEM Cloud Service 環境にテーマをデプロイします。

#### &#x200B;5. テーマのデプロイ {#deploy-the-theme}

フロントエンドパイプラインを使用して Cloud Service 環境にテーマをデプロイするには、以下を行います。

* 5.1 [テーマのリポジトリを作成](#create-a-new-theme-repo)
* 5.2 [リポジトリへの変更のプッシュ](#committing-the-changes)
* 5.3. [フロントエンドパイプラインの実行](#run-a-frontend-pipeline)

##### 5.1 テーマのリポジトリを作成{#create-a-new-theme-repo}

テーマをデプロイするには、リポジトリが必要です。[AEM Cloud Manager のリポジトリ](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/onboarding/journey/developers.html?lang=ja#accessing-git)にログインして、テーマの新しいリポジトリを追加します。

1. テーマの新しいリポジトリを作成するには、**[!UICONTROL リポジトリ]**／**[!UICONTROL リポジトリを追加]**&#x200B;をクリックします。

   ![新しいテーマリポジトリを作成](/help/forms/assets/createrepo_canvastheme.png)


1. **リポジトリを追加**&#x200B;ダイアログボックスで「**リポジトリの名前**」を指定します。例えば、`custom-canvas-theme-repo` などと指定します。
1. 「**[!UICONTROL 保存]**」をクリックします。

   ![キャンバステーマリポジトリの追加](/help/forms/assets/addcanvasthemerepo.png)

1. 「**[!UICONTROL リポジトリ URL をコピー]**」をクリックし、リポジトリの URL をコピーします。

   ![キャンバステーマの URL](/help/forms/assets/copyurl_canvastheme.png)

   >[!NOTE]
   > 
   > * 1 つのリポジトリを複数のテーマに使用できます。
   > * 異なるテーマをデプロイするには、別々のフロントエンドパイプラインを作成する必要があります。
   >* 例えば、キャンバステーマ、WKND テーマ、イーゼルテーマ用に `custom-canvas-theme-repo` という同じレポジトリを使用できます。ただし、テーマをデプロイするには、別々のフロントエンドパイプラインを作成する必要があります。特定のテーマに対する今後のカスタマイズは、対応するフロントエンドパイプラインを使用してデプロイされます。

##### 5.2. リポジトリへの変更のプッシュ {#committing-the-changes}

次に、変更を AEM Forms Cloud Service のテーマリポジトリにプッシュします。

1. テーマフォルダーのルートに移動します。ここでは、テーマのフォルダー名は `aem-forms-theme-canvas` です。
1. コマンドプロンプトまたはターミナルを開きます。
1. 次のコマンドをリストされている順序で実行します。

   ```
   git remote add [alias-name-for-repository] [URL of repository]
   git add .
   git commit
   git push [name-for-createdrepository]
   ```

   例：

   ```
   git remote add canvascloudthemerepo https://git.cloudmanager.adobe.com/stage-aemformsdev/customcanvastheme/
   git add .
   git commit
   git push canvascloudthemerepo 
   ```

   ![コミット済みの変更](/help/forms/assets/cmd_git_push.png)



##### 5.3. フロントエンドパイプラインの実行 {#run-a-frontend-pipeline}

テーマは、[フロントエンドパイプライン](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-wknd-tutorial-develop/enable-frontend-pipeline-devops/create-frontend-pipeline.html?lang=ja)を使用してデプロイします。テーマをデプロイするには、次の手順を実行します。

1. AEM Cloud Manager リポジトリにログインします。
1. 「**[!UICONTROL パイプライン]**」セクションの「**[!UICONTROL 追加]**」ボタンをクリックします。
1. Cloud Service 環境に応じて、「**[!UICONTROL 実稼動以外のパイプラインを追加]**」または「**[!UICONTROL 実稼動パイプラインを追加]**」を選択します。ここでは「**[!UICONTROL 実稼動パイプラインを追加]**」を選択します。
1. **[!UICONTROL 設定]**&#x200B;手順に含まれる「**[!UICONTROL 実稼動パイプラインを追加]**」ダイアログで、パイプラインの名前を指定します。例えば、`customcanvastheme` という名前にします。
1. 「**[!UICONTROL 続行]**」をクリックします。
1. **[!UICONTROL ソースコード]**&#x200B;の手順で、
**[!UICONTROL ターゲットデプロイメント]**／**[!UICONTROL フロントエンドコード]**&#x200B;オプションを選択します。
1. 最新の変更を含む&#x200B;**[!UICONTROL リポジトリ]**&#x200B;と **[!UICONTROL Git ブランチ]**&#x200B;の値を選択します。ここで選択したリポジトリ名は `custom-canvas-theme-repo` で、Git ブランチは `main` です。
1. 変更がルートフォルダーにある場合は、`/` として「**[!UICONTROL コードの場所]**」を選択します。
1. 「**[!UICONTROL 保存]**」をクリックします。
   ![フロントエンドパイプラインを作成](/help/forms/assets/canvas-theme-frontendpipeline.gif)

   パイプラインの設定が完了したら、コールトゥアクションカードが更新されます。

1. 作成したパイプラインを右クリックします。
1. 「**[!UICONTROL 実行]**」をクリックします。

   ![run-a-pipleine](/help/forms/assets/canvas-theme-run-pipeline.png)

作成が完了すると、オーサーインスタンスでテーマを使用できるようになります。これは、アダプティブフォームの作成中に作成ウィザードの「**[!UICONTROL スタイル]**」タブに表示されます。

![「スタイル」タブで使用可能なカスタムのテーマ](/help/forms/assets/custom-theme-style-tab.png)

カスタマイズされたテーマは、コアコンポーネントベースのアダプティブフォームでブランドエクスペリエンスを作成する際に役立ちます。

## アダプティブフォームにテーマを適用 {#using-theme-in-adaptive-form}

アダプティブフォームにテーマを適用するには、次の手順を実行します。

1. AEM Forms オーサーインスタンスにログインします。

1. **Adobe Experience Manager**／**Forms**／**フォームとドキュメント**&#x200B;を選択します。

1. **作成**／**アダプティブフォーム**&#x200B;の順にクリックします。アダプティブフォームを作成するためのウィザードが開きます。

1. 「**ソース**」タブでコアコンポーネントテンプレートを選択します。
1. 「**スタイル**」タブでテーマを選択します。
1. 「**作成**」をクリックします。

アダプティブフォームのテーマは、アダプティブフォームの作成時にスタイルを定義する、アダプティブフォームテンプレートの一部として使用されます。

## ベストプラクティス {#best-practices}

* **別のテーマに属するアセットの回避**

  テーマを編集する際、アセット（画像など）を他のテーマから参照して追加することができます。例えば、ページの背景を編集しているとします。例えば、**[!UICONTROL ページ]** ![edit-button](assets/edit-button.png)／**[!UICONTROL 背景]**／**[!UICONTROL 追加]**／**[!UICONTROL 画像]**&#x200B;を選択すると、他のテーマの画像を参照して追加することが可能なダイアログが表示されます。

  アセットを別のテーマから追加し、そのテーマが移動または削除されると、現在のテーマに問題が生じる場合があります。他のテーマからアセットを参照して追加しないようにすることをお勧めします。

* **コンテナパネルのレイアウト幅の変更**

  コンテナパネルのレイアウト幅の変更はお勧めしません。コンテナパネルの幅を指定すると、幅が静的になり、様々なディスプレイに合わせて調整されません。

## よくある質問 {#faq}

**Q**：テーマフォルダーのカスタマイズをグローバルレベルとコンポーネントレベルの両方で行う場合、どちらのカスタマイズが優先されますか？

**A**：グローバルレベルとコンポーネントレベルの両方でカスタマイズが行われる場合は、コンポーネントレベルでのカスタマイズが優先されます。

<!--

## See next

* [Set layout of forms for different screen sizes and device types](/help/sites-cloud/authoring/page-editor/responsive-layout.md)
* [Generate Document of Record for Adaptive Forms (Core Components](/help/forms/generate-document-of-record-for-non-xfa-based-adaptive-forms.md)
* [Create an Adaptive Forms with Repeatable sections](/help/forms/create-forms-repeatable-sections.md)
* [Sample themes templates and form data models](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/sample-themes-templates-form-data-models-core-components.html?lang=ja)

-->


## 関連トピック {#see-also}

{{see-also}}

* [画面サイズやデバイスタイプに応じてフォームのレイアウトを設定する](/help/sites-cloud/authoring/page-editor/responsive-layout.md)
* [アダプティブフォーム（コアコンポーネント）におけるレコードのドキュメントを生成する](/help/forms/generate-document-of-record-for-non-xfa-based-adaptive-forms.md)
* [繰り返し可能なセクションを使用してアダプティブフォームを作成する](/help/forms/create-forms-repeatable-sections.md)
* [サンプルのテーマテンプレートおよびフォームデータモデル](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/sample-themes-templates-form-data-models-core-components.html?lang=ja)
