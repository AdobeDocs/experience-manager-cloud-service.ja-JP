---
title: ユニバーサルエディターを使用したAEM FormsのEdge Delivery Servicesの概要
description: ユニバーサルエディターのWYSIWYG オーサリングで、Edge Delivery Servicesを使用して高パフォーマンスのフォームを作成して公開する方法を説明します。
feature: Edge Delivery Services
role: Admin, Architect, Developer
level: Intermediate
exl-id: 24a23d98-1819-4d6b-b823-3f1ccb66dbd8
source-git-commit: 6400662cb1c7a504f69db7091091452e99dd6ce9
workflow-type: tm+mt
source-wordcount: '2117'
ht-degree: 2%

---


# ユニバーサルエディターを使用したAEM FormsのEdge Delivery Servicesの概要

| オーサリング方法 | ガイド |
|---------------------------------|-----------------------------------------------------------------------|
| **ユニバーサルエディター（WYSIWYG）** | この記事 |
| **ドキュメントベースのオーサリング** | [ ドキュメントベースのチュートリアル ](/help/edge/docs/forms/tutorial.md) |

AEM Forms用Edge Delivery Servicesは、高性能の web 配信と、ユニバーサルエディターでのWYSIWYG オーサリングを組み合わせます。 このガイドでは、高速読み込みフォームの作成、カスタマイズ、公開について説明します。

## 達成する内容

このチュートリアルを終了すると、次のことができるようになります。

- アダプティブ Forms ブロックを使用して GitHub リポジトリを設定します
- Edge Delivery Servicesと統合したAEM サイトの作成
- ユニバーサルエディターを使用したフォームの作成と公開
- ローカル開発環境の設定

## パスを選択

シナリオに合致するアプローチを選択します。

![ パス決定ガイドを選択 ](/help/edge/docs/forms/universal-editor/assets/choose-your-path.svg)
*図：適切な実装パスを選択するのに役立つビジュアルガイド*

| **パス A：新しいプロジェクト** | **パス B：既存のプロジェクト** |
|----------------------------------------|-------------------------------------------|
| 事前設定済みのテンプレートから開始 | 現在のAEM プロジェクトへのフォームの追加 |
| **最適な対象：** 新規実装 | **最適：** 既存のAEM Sites |
| **結果：** 事前設定済みのForms ブロック | **結果：** Formsが既存のサイトに追加されました |
| **** 手順：Forms→のテンプレート→ース セットアップ | **手順：** Integration → Configuration → Forms |
| [ パス A から開始 ](#path-a-create-new-project-with-forms) | [ パス B から開始 ](#path-b-add-forms-to-existing-project) |

## 前提条件

開始する前に、次の点を確認してください。

### 必要なアクセス

- リポジトリを作成する権限を持つ **GitHub アカウント**
- **AEM as a Cloud Service** へのアクセスのオーサリング

### 技術要件

- **Git 基本**：クローン、コミット、プッシュ操作
- **Web テクノロジー**:HTML、CSS、JavaScriptの基本
- **Node.js** （バージョン 16 以降を推奨）:ローカル開発
- **npm** または **yarn** パッケージマネージャー

### 推奨される知識

- AEM Sitesの概念の基本的な理解
- フォームデザインの原則に精通している
- WYSIWYG エディターの使用経験

>[!TIP]
>
> AEMを初めて使用する場合 [AEM Sites入門ガイド ](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/sites/authoring/getting-started/quick-start.html?lang=ja) から開始します。

## 手順 A:Formsで新しいプロジェクトを作成する

**最適な対象：** 新規実装または概念実証

AEM Forms ボイラープレートは、統合されたアダプティブ Forms ブロックを含む事前設定済みのテンプレートを提供します。

### 手順の概要

1. テンプレートから GitHub リポジトリを設定します
2. AEM コード同期のインストール
3. AEM プロジェクトの連携の設定
4. AEM サイトを作成して公開する
5. ユニバーサルエディターを使用したフォームの追加

次の各手順を実行します。

+++手順 1：テンプレートから GitHub リポジトリを作成する

1. **AEM Forms ボイラープレートテンプレートへのアクセス**
   - [https://github.com/adobe-rnd/aem-boilerplate-forms](https://github.com/adobe-rnd/aem-boilerplate-forms) に移動します

   ![AEM Forms ボイラープレート テンプレート ](/help/edge/docs/forms/assets/eds-form-boilerplate.png)
   *図：事前設定済みのアダプティブ Forms ブロックを含んだAEM Forms ボイラープレートリポジトリ*

2. **リポジトリを作成する**
   - **このテンプレートを使用**/**新しいリポジトリを作成** をクリックします

   ![ テンプレートからリポジトリを作成 ](/help/edge/docs/forms/assets/use-eds-form-template.png)
   *図：テンプレートを使用した新しいリポジトリの作成*

3. **リポジトリ設定の指定**
   - **所有者**:GitHub アカウントまたは組織を選択します
   - **リポジトリ名**：わかりやすい名前（`my-forms-project` など）を選択します
   - **表示**:「**公開**」を選択します（Edge Delivery Servicesの場合に推奨）
   - 「**リポジトリを作成**」をクリックします。

   ![ リポジトリ設定 ](/help/edge/docs/forms/assets/name-eds-repo.png)
   *図：公開表示を使用した新しいリポジトリの設定*

**検証：** AEM Forms ボイラープレートテンプレートに基づいた新しい GitHub リポジトリがあることを確認します。

+++

+++手順 2:AEM Code Sync のインストール

AEM コード同期は、AEM オーサリング環境と GitHub リポジトリの間でコンテンツの変更を自動的に同期します。

1. **GitHub アプリのインストール**
   - [https://github.com/apps/aem-code-sync/installations/new](https://github.com/apps/aem-code-sync/installations/new) に移動します

2. **アクセス権限の設定**
   - 選択 **リポジトリのみを選択**
   - 新しく作成したリポジトリを選択します
   - 「**保存**」をクリックします。

   ![AEM コード同期のインストール ](/help/edge/docs/forms/assets/aem-code-sync-up.png)
   *図：リポジトリ固有の権限を持つAEM Code Sync のインストール*

**チェックポイント：** AEM Code Sync がインストールされ、リポジトリにアクセスできるようになりました。

+++

+++手順 3:AEM統合の設定

`fstab.yaml` ファイルは、コンテンツ同期のために GitHub リポジトリをAEM オーサリング環境に接続します。

1. **リポジトリに移動します**。
   - 新しく作成した GitHub リポジトリに移動します
   - AEM Forms Boilerplate ファイルが表示されます

2. **fstab.yaml ファイルの作成**
   - ルートディレクトリの **ファイルを追加**/**新しいファイルを作成** をクリックします
   - ファイルに「」という名前を付 `fstab.yaml` ます

   ![fstab.yaml ファイルの作成 ](/help/edge/docs/forms/assets/open-fstab.png)
   *図：fstab.yaml 設定ファイルの作成*

3. **AEM接続の詳細を追加する**

   プレースホルダーを置き換えて、次の設定をコピー&amp;ペーストします。

   ```yaml
   mountpoints:
     /: https://<aem-author>/bin/franklin.delivery/<owner>/<repository>/main
   ```

   **置換：**
   - `<aem-author>`:AEM as a Cloud Service オーサー URL （例：`author-p12345-e67890.adobeaemcloud.com`）
   - `<owner>`:GitHub のユーザー名または組織
   - `<repository>`：自分のリポジトリ名

   **例：**

   ```yaml
   mountpoints:
     /: https://author-p12345-e67890.adobeaemcloud.com/bin/franklin.delivery/mycompany/my-forms-project/main
   ```

   ![fstab.yaml ファイルの編集 ](/help/edge/docs/forms/assets/edit-fstab-file.png)
   *図：AEM統合用のマウントポイントの設定*

4. **設定をコミットする**
   - コミットメッセージを追加します。「AEM統合設定を追加」
   - 「**新しいファイルをコミット**」をクリックします

   ![fstab の変更のコミット ](/help/edge/docs/forms/assets/commit-fstab-changes.png)
   *図：fstab.yaml 設定のコミット*

**検証：** AEMへの GitHub リポジトリの接続を確認します。

    >[!NOTE]
    >
>ビルドに問題がありますか？ [GitHub ビルドの問題のトラブルシューティング ](#troubleshooting-github-build-issues) を参照してください。

+++

+++手順 4:GitHub リポジトリに接続したAEM サイトを作成する。

1. **AEM Sites コンソールへのアクセス**
   - AEM as a Cloud Service オーサリングインスタンスにログインします
   - **Sites** に移動します

   ![AEM Sites コンソール ](/help/edge/assets/select-sites.png)
   *図：AEM Sites コンソールへのアクセス*

2. **サイトの作成を開始**
   - **作成**/**テンプレートからのサイト** をクリックします

   ![ サイト作成オプション ](/help/edge/docs/forms/assets/create-sites.png)
   *図：テンプレートからの新しいサイトの作成*

3. **Edge Delivery Services テンプレートを選択します**。
   - **Edge Delivery Services サイト** テンプレートを選択します
   - 「**次へ**」をクリックします。

   ![ サイトテンプレートの選択 ](/help/edge/docs/forms/assets/select-site-template.png)
   *図：Edge Delivery Services サイトテンプレートの選択*

   >[!NOTE]
   >
   >**テンプレートは使用できませんか？** Edge Delivery Services テンプレートが表示されない場合：
   >
   >1. **インポート** をクリックして、テンプレートをアップロードします
   >2. [GitHub リリース ](https://github.com/adobe-rnd/aem-boilerplate-xwalk/releases) からのテンプレートのダウンロード

4. **サイトの設定**

   以下の情報を入力します。

   | フィールド | 値 | 例 |
   |-----------------|-----------------------------|-----------------------------------------|
   | **サイトのタイトル** | サイトのわかりやすい名前 | &quot;My Forms プロジェクト&quot; |
   | **サイト名** | URL にわかりやすい名前 | &quot;my-forms-project&quot; |
   | **GitHub URL** | リポジトリー URL | `https://github.com/mycompany/my-forms-project` |

   ![ サイト設定 ](/help/edge/docs/forms/assets/create-aem-site.png)
   *図：GitHub 統合を使用した新しいAEM サイトの設定*

5. **サイトの作成の完了**
   - 設定を確認
   - 「**作成**」をクリックします

   ![ サイトの作成を確認 ](/help/edge/docs/forms/assets/click-ok-aem-site.png)
   *図：サイト作成の確認*

   **成功しました。** AEM サイトが作成され、GitHub に接続されました。

6. **ユニバーサルエディターで開く**
   - Sites コンソールで、新しいサイトを見つけます
   - `index` ページを選択します。
   - **編集** をクリックします。

   ![ ユニバーサルエディターでサイトを編集 ](/help/edge/docs/forms/assets/edit-site.png)
   *図：編集するためにサイトを開く*

   ユニバーサルエディターが新しいタブで開き、WYSIWYGのオーサリング機能が表示されます。

   ![ ユニバーサルエディターインターフェイス ](/help/edge/docs/forms/assets/site-in-universal-editor.png)
   *図：WYSIWYG編集用にユニバーサルエディターでサイトを開いた*

**検証：** AEM サイトでフォームオーサリングの準備ができていることを確認します。

+++

+++手順 5：サイトを公開する

公開すると、サイトがEdge Delivery Servicesでグローバルにアクセスできるようになります。

1. **Sites コンソールからのクイック公開**
   - AEM Sites コンソールに戻ります
   - サイトページを選択（または Ctrl+A で「すべて」を選択）
   - **クイック公開**」をクリックします

   ![AEM サイトの公開 ](/help/edge/docs/forms/assets/publish-sites.png)
   *図：クイック公開するページの選択*

2. **公開を確認**
   - 確認ダイアログで、「**公開**」をクリックします

   ![ クイック公開ダイアログ ](/help/edge/docs/forms/assets/quick-publish.png)
   *図：公開アクションの確認*

   **代替：** 「公開」ボタンを使用して、ユニバーサルエディターから直接公開することもできます。

   ![ ユニバーサルエディターからの公開 ](/help/edge/docs/forms/assets/qui.png)
   *図：ユニバーサルエディターからの直接公開*

3. **ライブサイトへのアクセス**

   現在、サイトは次の場所で運用されています。

   ```
   https://<branch>--<repo>--<owner>.aem.page/content/<site-name>/
   ```

   **URL 構造の説明：**
   - `<branch>`:GitHub ブランチ（通常は `main`）
   - `<repo>`：自分のリポジトリ名
   - `<owner>`:GitHub のユーザー名または組織
   - `<site-name>`:AEM サイト名

   **例：**

   ```
   https://main--my-forms-project--mycompany.aem.page/content/my-forms-project/
   ```

**検証：** サイトがEdge Delivery Services上で稼働していることを確認します。

>[!TIP]
>
> **URL パターン：**
>
> - **ホームページ：** `https://<branch>--<repo>--<owner>.aem.page/content/<site-name>/`
> - **その他のページ：** `https://<branch>--<repo>--<owner>.aem.page/content/<site-name>/<page-name>`

**次へ：**[ 最初のフォームを作成 ](#create-your-first-form)

+++

## パス B：既存のプロジェクトへのFormsの追加

**最適な対象：** Edge Delivery Servicesを使用した既存のAEM Sites

Edge Delivery Servicesを使用するAEM プロジェクトが既にある場合は、アダプティブ Forms ブロックを統合してフォーム機能を追加できます。

### パス B の前提条件

- [AEM Boilerplate XWalk](https://github.com/adobe-rnd/aem-boilerplate-xwalk) で構築された既存のAEM プロジェクト
- ローカル開発環境の設定
- プロジェクトリポジトリーへの Git アクセス

**AEM Forms ボイラープレートを使用しますか？** [AEM Forms ボイラープレート ](https://github.com/adobe-rnd/aem-boilerplate-forms) でプロジェクトが作成された場合、フォームは既に統合されています。 [ 最初のフォームを作成する ](#create-your-first-form) にスキップします。

次の各手順を実行します。

### 手順の概要

1. アダプティブ Forms ブロックファイルのコピー
2. プロジェクト設定を更新
3. ESLint ルールの構成
4. 変更のビルドとコミット

+++手順 1:Forms ブロックファイルのコピー

1. **ローカルプロジェクトに移動します**

   ```bash
   cd /path/to/your/aem-project
   ```

2. **AEM Forms Boilerplate から必要なファイルをダウンロードします**

   これらのファイルを [AEM Forms Boilerplate リポジトリ ](https://github.com/adobe-rnd/aem-boilerplate-forms) からコピーします。

   | ソース | 公開先 | 目的 |
   |------------------------------------------------------------------------|----------------------------|----------------------------|
   | [`blocks/form/`](https://github.com/adobe-rnd/aem-boilerplate-forms/tree/main/blocks/form) | `blocks/form/` | コアフォーム機能 |
   | [`scripts/form-editor-support.js`](https://github.com/adobe-rnd/aem-boilerplate-forms/blob/main/scripts/form-editor-support.js) | `scripts/form-editor-support.js` | ユニバーサルエディターの統合 |
   | [`scripts/form-editor-support.css`](https://github.com/adobe-rnd/aem-boilerplate-forms/blob/main/scripts/form-editor-support.css) | `scripts/form-editor-support.css` | エディターのスタイル設定 |

3. **更新エディターのサポート**
   - AEM Forms Boilerplate の `/scripts/editor-support.js` ファイルを [editor-support.js に置き換えます ](https://github.com/adobe-rnd/aem-boilerplate-forms/blob/main/scripts/editor-support.js)

**検証：** フォームブロックファイルがプロジェクト内にあることを確認します。

+++

+++手順 2：コンポーネント設定の更新

1. **セクションモデルを更新**

   `/models/_section.json` を開き、フォームコンポーネントをフィルターに追加します。

   ```json
   {
        "filters": [
        {
      "id": "section",
      "components": [
           "text",
           "image",
           "button",
        "form",
        "embed-adaptive-form"
      ]
       }
     ]
   }
   ```

   **機能：** ユニバーサルエディターコンポーネントピッカーのフォームコンポーネントを有効にします。

**検証：** 確認フォームのコンポーネントがユニバーサルエディターに表示される。

+++

+++手順 3:ESLint の設定（オプション）

**この手順を実行する理由：** フォーム固有のファイルからエラーを送信しないようにし、適切な検証ルールを設定します。

1. **.eslintignore の更新**

   `/.eslintignore` に次の行を追加します。

   ```bash
   # Form block rule engine files
   blocks/form/rules/formula/*
   blocks/form/rules/model/*
   blocks/form/rules/functions.js
   scripts/editor-support.js
   scripts/editor-support-rte.js
   ```

2. **.eslintrc.js の更新**

   `rules` の `/.eslintrc.js` オブジェクトに次のルールを追加します。

   ```javascript
   {
     "rules": {
       // Existing rules...
   
       // Form component cell limits
    'xwalk/max-cells': ['error', {
         '*': 4, // default limit
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
         tnc: 12
       }],
   
       // Disable this rule for forms
       'xwalk/no-orphan-collapsible-fields': 'off'
     }
   }
   ```

**検証：** 確認 ESLint はフォームコンポーネントで機能します。

+++

+++手順 4：ビルドとデプロイ

1. **依存関係のインストールとビルド**

   ```bash
   # Install any new dependencies
   npm install
   
   # Build component definitions
   npm run build:json
   ```

   **機能：**
   - フォームコンポーネントを使用して `component-definition.json` を更新します
   - フォームモデルを使用して `component-models.json` を生成します
   - フィルタールールを含む `component-filters.json` を作成

2. **生成されたファイルの検証**

   プロジェクトルートの次のファイルにフォーム関連オブジェクトが含まれていることを確認します。
   - `component-definition.json`
   - `component-models.json`
   - `component-filters.json`

3. **変更のコミットとプッシュ**

   ```bash
   git add .
   git commit -m "Add Adaptive Forms Block integration"
   git push origin main
   ```

**検証：** フォームの機能がプロジェクトに含まれていることを確認します。

+++

**次：**[ 最初のフォームを作成 ](#create-your-first-form)

## 最初のフォームを作成

**適用先：** パス A とパス B の両方のユーザー

プロジェクトにフォーム機能がセットアップされたので、ユニバーサルエディターのWYSIWYG インターフェイスを使用して最初のフォームを作成します。

### フォーム作成プロセスの概要

1. ページに **アダプティブフォームブロックを追加** します
2. **フォームコンポーネントの追加** （テキスト入力、ボタンなど）
3. **コンポーネントのプロパティの設定**
4. フォームの **プレビューとテスト**
5. **公開** 更新されたページ

次の各手順を実行します。

+++手順 1：アダプティブフォームブロックを追加する

1. **ページをユニバーサルエディターで開く**
   - AEMの **Sites** コンソールに移動します
   - フォームを追加するページを選択します（例：`index`）
   - **編集** をクリックします。

   WYSIWYG編集用のユニバーサルエディターでページが開きます。

2. **アダプティブフォームコンポーネントの追加**
   - **コンテンツツリー** パネル（左サイドバー）を開きます。
   - フォームを追加するセクションに移動します
   - **追加** （+）アイコンをクリックします
   - コンポーネントリストから **アダプティブフォーム** を選択します

   ![ アダプティブフォームブロックの追加 ](/help/edge/docs/forms/assets/add-adaptive-form-block.png)
   *図：ページへのアダプティブフォームブロックの追加*

**検証：** 空のフォームコンテナがあることを確認します。

+++

+++手順 2：フォームコンポーネントを追加

1. **フォームブロックに移動**
   - コンテンツツリーで、新しく追加したアダプティブフォーム セクションを見つけます

   ![ 追加されたアダプティブフォームブロック ](/help/edge/docs/forms/assets/adative-form-block.png)
   *図：コンテンツツリーのアダプティブフォームブロック*

2. **フォームコンポーネントの追加**

   コンポーネントは次の 2 つの方法で追加できます。

   **方法 A：クリックして追加**
   - フォームセクションで **追加** （+） アイコンをクリックします
   - **アダプティブフォームコンポーネント** リストからコンポーネントを選択します

   **方法 B：ドラッグ&amp;ドロップ**
   - コンポーネントパネルからフォームに直接コンポーネントをドラッグします

   ![ フォームコンポーネントの追加 ](/help/edge/docs/forms/assets/add-component.png)
   *図：フォームへのコンポーネントの追加*

   **推奨されるスターターコンポーネント：**
   - テキスト入力（名前、メールの場合）
   - テキスト領域（メッセージ用）
   - 送信ボタン

3. **コンポーネントのプロパティの設定**
   - 任意のフォームコンポーネントを選択
   - **プロパティ** パネル（右側のサイドバー）を使用して、以下を設定します。
      - ラベルとプレースホルダ
      - 検証ルール
      - 必須フィールドの設定

   ![ コンポーネントのプロパティパネル ](/help/edge/docs/forms/assets/component-properties.png)
   *図：コンポーネントプロパティの設定*

4. **フォームをプレビューする**

   フォームは次のようになります。

   ![ 完了したフォームプレビュー ](/help/edge/docs/forms/assets/added-form-aem-sites.png)
   *図：ユニバーサルエディターで作成されたフォームの例*

**検証：** フォームの公開準備が整っていることを確認します。

>[!IMPORTANT]
>
> ブラウザーに更新を表示するには、変更を加えた後でページを忘れずに公開してください。

+++

+++手順 3：フォームを公開する

1. **ユニバーサルエディターからの公開**
   - ユニバーサルエディターの **公開** ボタンをクリックします

   ![ 発行フォーム ](/help/edge/docs/forms/assets/publish-form.png)
   *図：ユニバーサルエディターからのフォームの公開*

2. **公開を確認**
   - 確認ダイアログで、「**公開**」をクリックします

   ![ 公開の確認 ](/help/edge/docs/forms/assets/publish-form1.png)
   *図：公開アクションの確認*

   公開を確認する成功メッセージが表示されます。

   ![公開成功](/help/edge/docs/forms/assets/publish-form2.png)
   *図：公開の成功の確認*

3. **ライブフォームを表示する**

   フォームは次の場所に作成されました：

   ```
   https://<branch>--<repo>--<owner>.aem.page/content/<site-name>/
   ```

   **URL の例：**

   ```
   https://main--my-forms-project--mycompany.aem.page/content/my-forms-project/
   ```

   ![ ライブフォームページ ](/help/edge/docs/forms/assets/publish-index-page.png)
   *図：Edge Delivery Servicesに公開されたフォームページ*

**これで完了です。** これでフォームが有効になり、送信を収集する準備が整いました。

+++

### 次の手順

これで作業フォームが作成され、以下を行うことができます。

- **スタイル設定をカスタマイズ** CSS およびJavaScript ファイルの編集による
- **検証ルールや条件付きロジックなど** 高度なフォーム機能の追加
- **ローカル開発を設定** してイテレーションを高速化
- 特定のユースケース向けの **スタンドアロンフォームの作成**

>[!TIP]
>
> **詳細情報：**[ ユニバーサルエディターでのスタンドアロンフォームの作成 ](/help/edge/docs/forms/universal-editor/create-forms.md)

## ローカル開発環境の設定

**最適な対象：** フォームのスタイル設定と動作をカスタマイズする開発者

ローカル開発環境を使用すると、公開サイクルを経ることなく、変更を加えて即座に表示できます。

+++AEM CLI とローカル開発の設定

1. **AEM CLI のインストール**

   AEM CLI を使用すると、ローカル開発タスクを簡略化できます。

   ```bash
       npm install -g @adobe/aem-cli
   ```

2. **リポジトリのクローン**

   ```bash
   git clone https://github.com/<owner>/<repo>
   cd <repo>
   ```

   `<owner>` と `<repo>` を実際の GitHub の詳細に置き換えます。

3. **ローカル開発サーバーの起動**

   ```bash
   aem up
   ```

   これにより、ホットリロード機能を備えたローカルサーバーが起動します。

4. **カスタマイズの実行**

   - フォームのスタイル設定と動作のために、`blocks/form/` ディレクトリのファイルを編集します
   - スタイル設定用に `form.css` を変更
   - 動作の `form.js` を更新

   ブラウザーの **に** 変更をすぐに確認 `http://localhost:3000` します。

5. **変更をデプロイする**

   ```bash
   git add .
   git commit -m "Custom form styling"
   git push origin main
   ```

   変更は、次の場所で利用できます。
   - **プレビュー：** `https://<branch>--<repo>--<owner>.aem.page/content/<site-name>`
   - **実稼働：** `https://<branch>--<repo>--<owner>.aem.live/content/<site-name>`

+++


## トラブルシューティング

### よくある問題と解決策

+++GitHub のビルド問題

**問題：** ビルドの失敗またはエラーのリンティング

**解決策 1：リンティングエラーの処理**

リンティングエラーが発生した場合：

1. プロジェクトルートで `package.json` を開きます
2. `lint` スクリプトを検索します。

   ```json
   "scripts": {
     "lint": "npm run lint:js && npm run lint:css"
   }
   ```

3. リンティングを一時的に無効にする：

   ```json
   "scripts": {
     "lint": "echo 'skipping linting for now'"
   }
   ```

4. 変更をコミットしてプッシュします

**解決策 2：モジュールパスエラー**

「モジュール「/scripts/lib-franklin.js」へのパスを解決できません」と表示される場合：

1. `blocks/form/form.js` に移動します。
2. import 文を更新します。

   ```javascript
   // Change this:
   import { ... } from '/scripts/lib-franklin.js';
   
   // To this:
   import { ... } from '/scripts/aem.js';
   ```

+++

+++ユニバーサルエディターの問題

**問題：** ユニバーサルエディターにフォームコンポーネントが表示されない

**ソリューション：**

- AEM Code Sync がインストールされ、実行されていることを確認します。
- `fstab.yaml` に正しいAEM オーサー URL があることを確認します。
- AEM インスタンスで早期アクセスが有効になっていることを確認します
- 確認 `component-definition.json` にフォームコンポーネントが含まれます

**問題：** 公開後、変更が表示されない

**ソリューション：**

- CDN キャッシュの更新待ち
- ブラウザーキャッシュを確認する（匿名/プライベートモードを試す）
- 正しい URL 形式が使用されていることを確認します

+++

+++フォーム機能の問題

**問題：** フォーム送信が機能しない

**ソリューション：**

- 送信ボタンコンポーネントがあることを確認します
- フォームアクションの URL 設定を確認
- フォーム検証ルールの検証
- 最初にプレビューモードでテストします

**問題：** スタイル設定の問題

**ソリューション：**

- `blocks/form/` での CSS ファイルパスの確認
- ブラウザーキャッシュのクリア
- CSS 構文の検証
- ローカル開発環境でのテスト

+++

