---
title: ユニバーサルエディターでの AEM Forms の Edge Delivery Services の基本を学ぶ
description: ユニバーサルエディターの WYSIWYG オーサリングで Edge Delivery Services を使用して、パフォーマンスの高いフォームを作成および公開する方法について説明します。
feature: Edge Delivery Services
role: Admin, Architect, Developer
level: Intermediate
exl-id: 24a23d98-1819-4d6b-b823-3f1ccb66dbd8
source-git-commit: fd3c53cf5a6d1c097a5ea114a831ff626ae7ad7e
workflow-type: tm+mt
source-wordcount: '2608'
ht-degree: 96%

---


# ユニバーサルエディターでの AEM Forms の Edge Delivery Services の基本を学ぶ

| オーサリング方法 | ガイド |
|---------------------------------|-----------------------------------------------------------------------|
| **ユニバーサルエディター（WYSIWYG）** | この記事 |
| **ドキュメントベースのオーサリング** | [ドキュメントベースのチュートリアル](/help/edge/docs/forms/tutorial.md) |

AEM Forms 向け Edge Delivery Services では、パフォーマンスの高い web 配信とユニバーサルエディターの WYSIWYG オーサリングを組み合わせます。このガイドでは、高速読み込みフォームの作成、カスタマイズ、公開について説明します。

## このチュートリアルでできること

このチュートリアルを完了すると、次のことができるようになります。

- アダプティブフォームブロックを使用して GitHub リポジトリを設定する
- Edge Delivery Services と統合された AEM サイトを作成する
- ユニバーサルエディターを使用してフォームを作成および公開する
- ローカル開発環境を設定する

## パスの選択

シナリオに一致するアプローチを選択します。

![パスの選択の決定ガイド](/help/edge/docs/forms/universal-editor/assets/choose-your-path.svg)
*図：適切な実装パスを選択するのに役立つ視覚的なガイド*

| **パス A：新規プロジェクト** | **パス B：既存のプロジェクト** |
|----------------------------------------|-------------------------------------------|
| 事前設定済みのテンプレートから開始する | 現在の AEM プロジェクトにフォームを追加する |
| **最適な用途：**&#x200B;新規実装 | **最適な用途：**&#x200B;既存の AEM Sites |
| **結果：**&#x200B;事前設定済みのフォームをブロックする | **結果：**&#x200B;既存のサイトに追加されたフォームが追加される |
| **手順：**&#x200B;テンプレート → 設定 → Forms | **手順：**&#x200B;統合→ 設定 → Forms |
| [パス A から開始](#path-a-create-new-project-with-forms) | [パス B から開始](#path-b-add-forms-to-existing-project) |

## 前提条件

ユニバーサルエディターを使用して AEM Forms 向け Edge Delivery Services をスムーズかつ正常に使用するには、先に進む前に次の前提条件を確認します。

### アクセス要件

- **GitHub アカウント**：新しいリポジトリを作成する権限を持つ GitHub アカウントが必要です。このアカウントは、プロジェクトのソースコードの管理やチームとの共同作業に不可欠です。
- **AEM as a Cloud Service オーサリングアクセス**：AEM as a Cloud Service 環境へのオーサーレベルのアクセス権があることを確認します。このアクセス権は、フォームの作成、編集、公開に必要です。

### 技術要件

- **Git の知識**：リポジトリの複製、変更のコミット、更新のプッシュなど、基本的な Git 操作を問題なく実行できる必要があります。これらのスキルは、ソース管理とプロジェクトの共同作業の基本です。
- **Web テクノロジーの理解**：HTML、CSS、JavaScript の実用的な知識をお勧めします。これらのテクノロジーは、フォームのカスタマイズとトラブルシューティングの基盤です。
- **Node.js（バージョン 16 以上）**：ローカル開発とビルドツールの実行には Node.js が必要です。システムにバージョン 16 以降がインストールされていることを確認します。
- **パッケージマネージャー（npm または yarn）**：プロジェクトの依存関係とスクリプトを管理するには、npm（ノードパッケージマネージャー）または yarn が必要です。

### 推奨される背景

- **AEM Sites の概念**：サイト構造やコンテンツのオーサリングを含む AEM Sites の基本を理解しておくと、フォームを効果的に操作および統合できます。
- **フォームデザインの原則**：ユーザビリティ、アクセシビリティ、データ検証など、フォームデザインのベストプラクティスに精通していると、効果的で使いやすいフォームを作成できます。
- **WYSIWYG エディターのエクスペリエンス**：以前に WYSIWYG（What You See Is What You Get）エディターを使用したことがある場合は、ユニバーサルエディターの視覚的なオーサリング機能をより効率的に活用できます。

>[!TIP]
>
> AEM を初めて使用する方[AEM Sites 入門ガイド](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/sites/authoring/getting-started/quick-start.html?lang=ja)から開始します。

## パス A：Forms で新規プロジェクトを作成

**推奨：**&#x200B;新規プロジェクト、パイロット、概念実証イニシアチブ

AEM Forms ボイラープレートを活用して、プロジェクトの設定を高速化します。このボイラープレートは、アダプティブフォームブロックをシームレスに統合するすぐに使用できるテンプレートを提供し、AEM サイト内でフォームを迅速に作成およびデプロイできます。

### 概要

統合フォームを使用して新規プロジェクトを正常に起動するには、次の操作が必要です。

1. AEM Forms ボイラープレートテンプレートを使用して、GitHub リポジトリを作成します。
2. AEM コード同期を設定して、AEM とリポジトリ間のコンテンツ同期を自動処理します。
3. GitHub プロジェクトと AEM 環境間の接続を設定します。
4. 新しい AEM サイトを確立して公開します。
5. ユニバーサルエディターを使用してフォームを追加および管理します。

次の節では、各手順を詳細にガイドし、スムーズで効率的なプロジェクト設定エクスペリエンスを実現します。

+++手順 1：テンプレートから GitHub リポジトリを作成する

1. **AEM Forms ボイラープレートテンプレートにアクセス**
   - [https://github.com/adobe-rnd/aem-boilerplate-forms](https://github.com/adobe-rnd/aem-boilerplate-forms) に移動します

   ![AEM Forms ボイラープレートテンプレート](/help/edge/docs/forms/assets/eds-form-boilerplate.png)
   *図：事前設定済みのアダプティブフォームブロックを使用した AEM Forms ボイラープレートリポジトリ*

2. **リポジトリを作成**
   - **このテンプレートを使用**／**新規リポジトリを作成**&#x200B;をクリックします

   ![テンプレートからリポジトリを作成](/help/edge/docs/forms/assets/use-eds-form-template.png)
   *図：テンプレートを使用した新規リポジトリの作成*

3. **リポジトリ設定を指定**
   - **所有者**：GitHub アカウントまたは組織を選択します
   - **リポジトリ名**：わかりやすい名前（例：`my-forms-project`）を選択します
   - **表示**：「**パブリック**」（Edge Delivery Services の場合に推奨）を選択します
   - 「**リポジトリを作成**」をクリックします

   ![リポジトリ設定](/help/edge/docs/forms/assets/name-eds-repo.png)
   *図：パブリック表示を使用した新規リポジトリの設定*

**検証：** AEM Forms ボイラープレートテンプレートに基づく新規 GitHub リポジトリがあることを確認します。

+++

+++手順 2:AEM Code Sync のインストール

AEM コード同期は、AEM オーサリング環境と GitHub リポジトリ間でコンテンツの変更を自動的に同期します。

1. **GitHub アプリをインストール**
   - [https://github.com/apps/aem-code-sync/installations/new](https://github.com/apps/aem-code-sync/installations/new) に移動します

2. **アクセス権限を設定**
   - 「**選択したリポジトリのみ**」を選択します
   - 新しく作成したリポジトリを選択します
   - 「**保存**」をクリックします。

   ![AEM コード同期のインストール](/help/edge/docs/forms/assets/aem-code-sync-up.png)
   *図：リポジトリ固有の権限を持つ AEM コード同期のインストール*

**チェックポイント：** AEM コード同期がインストールされ、リポジトリにアクセスできるようになりました。

+++

+++手順 3:AEM統合の設定

`fstab.yaml` ファイルは、GitHub リポジトリを AEM オーサリング環境に接続し、コンテンツを同期します。

1. **リポジトリに移動**
   - 新しく作成した GitHub リポジトリに移動します
   - AEM Forms ボイラープレートファイルが表示されます

2. **fstab.yaml ファイルを作成**
   - ルートディレクトリで&#x200B;**ファイルを追加**／**新規ファイルを作成**&#x200B;をクリックします
   - ファイル名を `fstab.yaml` にします

   ![fstab.yaml ファイルの作成](/help/edge/docs/forms/assets/open-fstab.png)
   *図：fstab.yaml 設定ファイルの作成*

3. **AEM 接続の詳細を追加**

   次の設定をコピー＆ペーストして、プレースホルダーを置き換えます。

   ```yaml
   mountpoints:
     /: 
     url: https://<aem-author>/bin/franklin.delivery/<owner>/<repository>/main
     type: "markup" 
     suffix: ".html" 
   ```

   **置換：**
   - `<aem-author>`：AEM as a Cloud Service オーサー URL（例：`author-p12345-e67890.adobeaemcloud.com`）
   - `<owner>`：GitHub ユーザー名または組織
   - `<repository>`：自分のリポジトリ名

   **例：**

   ```yaml
   mountpoints:
     /: https://author-p12345-e67890.adobeaemcloud.com/bin/franklin.delivery/mycompany/my-forms-project/main
   ```

   ![fstab.yaml ファイルの編集](/help/edge/docs/forms/assets/edit-fstab-file.png)
   *図：AEM 統合用のマウントポイントの設定*

4. **設定をコミット**
   - 「AEM 統合設定を追加」コミットメッセージを追加します
   - 「**新規ファイルをコミット**」をクリックします

   ![fstab の変更のコミット](/help/edge/docs/forms/assets/commit-fstab-changes.png)
   *図：fstab.yaml 設定のコミット*

**検証：** AEM への GitHub リポジトリ接続を確認します。

>[!NOTE]
>
> ビルドに問題がありますか？ [GitHub ビルドの問題のトラブルシューティング](#troubleshooting-github-build-issues)を参照してください。

+++

+++手順 4:GitHub リポジトリに接続したAEM サイトを作成する。

1. **AEM Sites コンソールにアクセス**
   - AEM as a Cloud Service オーサリングインスタンスにログインします
   - **Sites** に移動します

   ![AEM Sites コンソール](/help/edge/assets/select-sites.png)
   *図：AEM Sites コンソールへのアクセス*

2. **サイトの作成を開始**
   - **作成**／**テンプレートからサイト**&#x200B;をクリックします

   ![「サイトを作成」オプション](/help/edge/docs/forms/assets/create-sites.png)
   *図：テンプレートからの新しいサイトの作成*

3. **Edge Delivery Services テンプレートを選択**
   - **Edge Delivery Services サイト**&#x200B;テンプレートを選択します
   - 「**次へ**」をクリックします。

   ![サイトテンプレートの選択](/help/edge/docs/forms/assets/select-site-template.png)
   *図：Edge Delivery Services サイトテンプレートの選択*

   >[!NOTE]
   >
   >**テンプレートが使用できませんか？** Edge Delivery Services テンプレートが表示されない場合は、次の手順に従います。
   >
   >1. 「**読み込み**」をクリックして、テンプレートをアップロードします
   >2. [GitHub リリース](https://github.com/adobe-rnd/aem-boilerplate-xwalk/releases)からテンプレートをダウンロードします

4. **サイトを設定**

   次の情報を入力します。

   | フィールド | 値 | 例 |
   |-----------------|-----------------------------|-----------------------------------------|
   | **サイトのタイトル** | サイトのわかりやすい名前 | 「マイ Forms プロジェクト」 |
   | **サイト名** | URL のわかりやすい名前 | 「my-forms-project」 |
   | **GitHub URL** | 自分のリポジトリ URL | `https://github.com/mycompany/my-forms-project` |

   ![サイト設定](/help/edge/docs/forms/assets/create-aem-site.png)
   *図：GitHub 統合を使用した新しい AEM サイトの設定*

5. **サイト作成を完了**
   - 設定をレビューします
   - 「**作成**」をクリックします。

   ![サイト作成を確認](/help/edge/docs/forms/assets/click-ok-aem-site.png)
   *図：サイト作成の確認*

   **成功です。** AEM サイトが作成され、GitHub に接続されました。

6. **ユニバーサルエディターで開く**
   - Sites コンソールで、新しいサイトを見つけます
   - `index` ページを選択します。
   - 「**編集**」をクリックします

   ![ユニバーサルエディターでサイトを編集](/help/edge/docs/forms/assets/edit-site.png)
   *図：編集用にサイトを開く*

   ユニバーサルエディターが新しいタブで開き、WYSIWYG オーサリング機能が表示されます。

   ![ユニバーサルエディターインターフェイス](/help/edge/docs/forms/assets/site-in-universal-editor.png)
   *図：WYSIWYG 編集用にユニバーサルエディターで開いたサイト*

**検証：** AEM サイトでフォームオーサリングの準備が整ったことを確認します。

+++

+++手順 5：サイトの公開

公開すると、サイトがグローバルアクセス用の Edge Delivery Services で使用できます。

1. **Sites コンソールからクイック公開**
   - AEM Sites コンソールに戻ります
   - サイトページを選択します（または Ctrl+A キーですべて選択します）
   - 「**クイック公開**」をクリックします

   ![AEM サイトを公開](/help/edge/docs/forms/assets/publish-sites.png)
   *図：クイック公開用のページの選択*

2. **公開を確認**
   - 確認ダイアログで「**公開**」をクリックします

   ![クイック公開ダイアログ](/help/edge/docs/forms/assets/quick-publish.png)
   *図：公開アクションの確認*

   **代替：**「公開」ボタンを使用して、ユニバーサルエディターから直接公開することもできます。

   ![ユニバーサルエディターから公開](/help/edge/docs/forms/assets/qui.png)
   *図：ユニバーサルエディターからの直接公開*

3. **ライブサイトにアクセス**

   現在、サイトは次の場所で運用されています。

   ```
   https://<branch>--<repo>--<owner>.aem.page/content/<site-name>/
   ```

   **URL 構造の説明：**
   - `<branch>`：GitHub 分岐（通常は `main`）
   - `<repo>`：自分のリポジトリ名
   - `<owner>`：GitHub ユーザー名または組織
   - `<site-name>`：自分の AEM サイト名

   **例：**

   ```
   https://main--my-forms-project--mycompany.aem.page/content/my-forms-project/
   ```

**検証：**&#x200B;サイトが Edge Delivery Services で運用されていることを確認します。

>[!TIP]
>
> **URL パターン：**
>
> - **ホームページ：** `https://<branch>--<repo>--<owner>.aem.page/content/<site-name>/`
> - **その他のページ：** `https://<branch>--<repo>--<owner>.aem.page/content/<site-name>/<page-name>`

**次へ：**[最初のフォームの作成](#create-your-first-form)

+++

## パス B：既存のプロジェクトへの Forms の追加

**次に最適：** Edge Delivery Services を使用した既存の AEM Sites

Edge Delivery Services を使用した AEM プロジェクトが既にある場合は、アダプティブフォームブロックを統合してフォーム機能を追加できます。

### パス B の前提条件

既存の AEM プロジェクトにフォームを統合するには、次の前提条件を満たしていることを確認します。

- [AEM ボイラープレート XWalk](https://github.com/adobe-rnd/aem-boilerplate-xwalk) を使用して作成された既存の AEM プロジェクトがある。
- [ローカル開発環境](#set-up-local-development-environment)が設定されている
- プロジェクトリポジトリへの Git アクセス権があり、必要に応じて複製、変更、プッシュできる。

>[!NOTE]
>
> プロジェクトが最初に [AEM Forms ボイラープレート](https://github.com/adobe-rnd/aem-boilerplate-forms)を使用して設定されている場合は、フォーム機能が既に含まれています。 その場合は、[最初のフォームの作成](#create-your-first-form)の節に進みます。

次のガイドでは、既存のプロジェクトにフォーム機能を追加するための構造化されたアプローチについて説明します。各手順は、ユニバーサルエディター環境内でシームレスな統合と最適な機能を確保するように設計されています。

### 概要

次の高度な手順を完了します。

1. アダプティブフォームブロックファイルをプロジェクトにコピーします。
2. フォームコンポーネントを認識してサポートするように、プロジェクトの設定を更新します。
3. 新しいファイルとコーディングパターンに対応するように、ESLint ルールを調整します。
4. プロジェクトを作成し、変更をリポジトリにコミットします。

+++手順 1:Forms ブロックファイルのコピー

1. **ローカルプロジェクトに移動**

   ```bash
   cd /path/to/your/aem-project
   ```

2. **AEM Forms ボイラープレートから必要なファイルをダウンロード**

   これらのファイルを [AEM Forms ボイラープレートリポジトリ](https://github.com/adobe-rnd/aem-boilerplate-forms)からコピーします。

   | ソース | 宛先 | 目的 |
   |------------------------------------------------------------------------|----------------------------|----------------------------|
   | [`blocks/form/`](https://github.com/adobe-rnd/aem-boilerplate-forms/tree/main/blocks/form) | `blocks/form/` | コアフォーム機能 |
   | [`scripts/form-editor-support.js`](https://github.com/adobe-rnd/aem-boilerplate-forms/blob/main/scripts/form-editor-support.js) | `scripts/form-editor-support.js` | ユニバーサルエディターの統合 |
   | [`scripts/form-editor-support.css`](https://github.com/adobe-rnd/aem-boilerplate-forms/blob/main/scripts/form-editor-support.css) | `scripts/form-editor-support.css` | エディターのスタイル設定 |

3. **エディターのサポートを更新**
   - `/scripts/editor-support.js` ファイルを [AEM Forms ボイラープレートの editor-support.js](https://github.com/adobe-rnd/aem-boilerplate-forms/blob/main/scripts/editor-support.js) に置き換えます

**検証：**&#x200B;フォームブロックファイルがプロジェクト内にあることを確認します。

+++

+++手順 2：コンポーネント設定の更新

1. **セクションモデルを更新**

   `/models/_section.json` を開き、フィルターにフォームコンポーネントを追加します。

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

   **この処理の内容：**&#x200B;ユニバーサルエディターのコンポーネントピッカーでフォームコンポーネントを有効にします。

**検証：**&#x200B;フォームコンポーネントがユニバーサルエディターに表示されることを確認します。

+++

+++手順 3:ESLint の構成（オプション）

**この手順の理由：**&#x200B;フォーム固有のファイルからのリンティングエラーを防ぎ、適切な検証ルールを設定します。

1. **.eslintignore を更新**

   `/.eslintignore` に次の行を追加します。

   ```bash
   # Form block rule engine files
   blocks/form/rules/formula/*
   blocks/form/rules/model/*
   blocks/form/rules/functions.js
   scripts/editor-support.js
   scripts/editor-support-rte.js
   ```

2. **.eslintrc.js を更新**

   `/.eslintrc.js` の `rules` オブジェクトに次のルールを追加します。

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

**検証：** ESLint がフォームコンポーネントで動作することを確認します。

+++

+++手順 4：ビルドとデプロイ

1. **依存関係をインストールおよびビルド**

   ```bash
   # Install any new dependencies
   npm install
   
   # Build component definitions
   npm run build:json
   ```

   **この処理の内容：**
   - フォームコンポーネントを使用して `component-definition.json` を更新します
   - フォームモデルを使用して `component-models.json` を生成します
   - フィルタリングルールを使用して `component-filters.json` を作成します

2. **生成されたファイルを検証**

   プロジェクトルート内の次のファイルにフォーム関連オブジェクトが含まれていることを確認します。
   - `component-definition.json`
   - `component-models.json`
   - `component-filters.json`

3. **変更のコミットとプッシュ**

   ```bash
   git add .
   git commit -m "Add Adaptive Forms Block integration"
   git push origin main
   ```

**検証：**&#x200B;フォームの機能がプロジェクトに含まれていることを確認します。

+++

**次へ：**[最初のフォームの作成](#create-your-first-form)

## 最初のフォームの作成

**この節の対象読者：**\
この節は、パス A（新規プロジェクト）またはパス B（既存のプロジェクト）のいずれかのユーザーに関連します。

これで、プロジェクトにフォーム作成機能が追加され、ユニバーサルエディターの直感的な WYSIWYG オーサリング環境を使用して最初のフォームを作成する準備が整いました。次の手順では、AEM サイト内でフォームを設計、設定、公開するための構造化されたアプローチを示します。

### 概要

ユニバーサルエディターでフォームを作成するプロセスは、次のいくつかの主要なステージで構成されています。

1. **アダプティブフォームブロックを挿入**\
   まず、選択したページにアダプティブフォームブロックを追加します。

2. **フォームコンポーネントを追加**\
   テキストフィールド、ボタン、その他の入力要素などのコンポーネントを挿入して、フォームに入力します。

3. **コンポーネントのプロパティを設定**\
   フォームの要件に合わせて、各コンポーネントの設定とプロパティを調整します。

4. **フォームをプレビューおよびテスト**\
   プレビュー機能を使用して、公開前にフォームの外観と動作を検証します。

5. **更新したページを公開**\
   問題がなければ、ページを公開して、エンドユーザーがフォームを使用できるようにします。

次の節では、各手順を詳しく説明し、スムーズで効果的なフォーム作成エクスペリエンスを実現します。

+++手順 1：アダプティブフォームブロックを追加する

1. **ユニバーサルエディターでページを開く**
   - AEM の **Sites** コンソールに移動します
   - フォームを追加するページ（例：`index`）を選択します
   - 「**編集**」をクリックします

   WYSIWYG 編集用にユニバーサルエディターでページが開きます。

2. **アダプティブフォームコンポーネントを追加**
   - **コンテンツツリー**&#x200B;パネル（左側のサイドバー）を開きます
   - フォームを追加するセクションに移動します
   - **追加**（+）アイコンをクリックします
   - コンポーネントリストから&#x200B;**アダプティブフォーム**&#x200B;を選択します

   ![アダプティブフォームブロックの追加](/help/edge/docs/forms/assets/add-adaptive-form-block.png)
   *図：ページへのアダプティブフォームブロックの追加*

**検証：** 空のフォームコンテナがあることを確認します。

+++

+++手順 2：フォームコンポーネントを追加

1. **フォームブロックに移動**
   - コンテンツツリーで、新しく追加したアダプティブフォームセクションを見つけます

   ![追加したアダプティブフォームブロック](/help/edge/docs/forms/assets/adative-form-block.png)
   *図：コンテンツツリーのアダプティブフォームブロック*

2. **フォームコンポーネントを追加**

   コンポーネントを追加するには、次の 2 つの方法があります。

   **方法 A：クリックして追加**
   - フォームセクションの&#x200B;**追加**（+）アイコンをクリックします
   - **アダプティブフォームコンポーネント**&#x200B;リストからコンポーネントを選択します

   **方法 B：ドラッグ＆ドロップ**
   - コンポーネントパネルからフォームに直接コンポーネントをドラッグします

   ![フォームコンポーネントの追加](/help/edge/docs/forms/assets/add-component.png)
   *図：フォームへのコンポーネントの追加*

   **推奨されるスターターコンポーネント：**
   - テキスト入力（名前、メール用）
   - テキスト領域（メッセージ用）
   - 送信ボタン

3. **コンポーネントのプロパティを設定**
   - 任意のフォームコンポーネントを選択します
   - **プロパティ**&#x200B;パネル（右側のサイドバー）を使用して、次を設定します。
      - ラベルとプレースホルダー
      - 検証ルール
      - 必須のフィールド設定

   ![コンポーネントのプロパティパネル](/help/edge/docs/forms/assets/component-properties.png)
   *図：コンポーネントのプロパティの設定*

4. **フォームをプレビュー**

   フォームは次のようになります。

   ![完了したフォームプレビュー](/help/edge/docs/forms/assets/added-form-aem-sites.png)
   *図：ユニバーサルエディターで作成されたフォームの例*

**検証：**&#x200B;フォームの公開準備が整っていることを確認します。

>[!IMPORTANT]
>
> 変更を行ったらページを公開して、ブラウザーで更新を確認します。

+++

+++手順 3：フォームを公開する

1. **ユニバーサルエディターから公開**
   - ユニバーサルエディターの「**公開**」ボタンをクリックします

   ![フォームの公開](/help/edge/docs/forms/assets/publish-form.png)
   *図：ユニバーサルエディターからのフォームの公開*

2. **公開を確認**
   - 確認ダイアログで「**公開**」をクリックします

   ![公開の確認](/help/edge/docs/forms/assets/publish-form1.png)
   *図：公開の確認アクション*

   公開を確認する成功メッセージが表示されます。

   ![公開成功](/help/edge/docs/forms/assets/publish-form2.png)
   *図：成功した公開の確認*

3. **ライブフォームを表示**

   現在、フォームは次の場所で運用されています。

   ```
   https://<branch>--<repo>--<owner>.aem.live/content/<site-name>/
   ```

   **URL の例：**

   ```
   https://main--my-forms-project--mycompany.aem.live/content/my-forms-project/
   ```

   ![ライブフォームページ](/help/edge/docs/forms/assets/publish-index-page.png)
   *図：Edge Delivery Services で公開されたフォームページ*

**おめでとうございます。**&#x200B;これで、フォームが運用され、送信を収集する準備が整いました。

+++

### 次の手順

これで、作業用フォームが作成されたので、次の操作を行うことができます。

- CSS および JavaScript ファイルを編集して&#x200B;**スタイルをカスタマイズ**
- 検証ルールや条件付きロジックなどの&#x200B;**高度なフォーム機能を追加**
- 反復作業を高速化するために&#x200B;**ローカル開発環境を設定**
- 特定のユースケース向けに&#x200B;**スタンドアロンフォームを作成**

>[!TIP]
>
> **詳細情報：**[ユニバーサルエディターでのスタンドアロンフォームの作成](/help/edge/docs/forms/universal-editor/create-forms.md)

## ローカル開発環境の設定

**次に最適：**&#x200B;フォームのスタイルと動作をカスタマイズする開発者

ローカル開発環境を使用すると、公開サイクルを経由することなく、変更を行ってすぐに結果を確認できます。

+++AEM CLI とローカル開発の設定

1. **AEM CLI をインストール**

   AEM CLI は、ローカル開発タスクを簡素化します。

   ```bash
       npm install -g @adobe/aem-cli
   ```

2. **リポジトリを複製**

   ```bash
   git clone https://github.com/<owner>/<repo>
   cd <repo>
   ```

   `<owner>` と `<repo>` を実際の GitHub の詳細に置き換えます。

3. **ローカル開発サーバーを起動**

   ```bash
   aem up
   ```

   これにより、ホットリロード機能を備えたローカル サーバーが起動します。

4. **カスタマイズを実行**

   - フォームのスタイルと動作については、`blocks/form/` ディレクトリ内のファイルを編集します
   - スタイルについては、`form.css` を変更します
   - 動作については、`form.js` を更新します

   ブラウザーで `http://localhost:3000` にアクセスして、**変更をすぐに確認**&#x200B;します

5. **変更をデプロイ**

   ```bash
   git add .
   git commit -m "Custom form styling"
   git push origin main
   ```

   変更は、次の場所で確認できます。
   - **プレビュー：** `https://<branch>--<repo>--<owner>.aem.page/content/<site-name>`
   - **実稼動環境：** `https://<branch>--<repo>--<owner>.aem.live/content/<site-name>`

+++


## トラブルシューティング

### よくある問題と解決策

+++GitHub のビルドの問題

**問題：**&#x200B;ビルドの失敗またはリンティングエラー

**解決策 1：リンティングエラーを処理**

リンティングエラーが発生した場合：

1. プロジェクトルートにある `package.json` を開きます
2. 次の `lint` スクリプトを見つけます。

   ```json
   "scripts": {
     "lint": "npm run lint:js && npm run lint:css"
   }
   ```

3. 一時的に次のリンティングを無効にします。

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

+++フォーム機能の問題

**問題：**&#x200B;フォーム送信が機能しない

**解決策：**

- 送信ボタンコンポーネントがあることを確認します
- フォームアクションの URL 設定を確認します
- フォームの検証ルールを確認します
- 最初にプレビューモードでテストします

**問題：** スタイルの問題

**解決策：**

- `blocks/form/` 内の CSS ファイルパスを確認します
- ブラウザーキャッシュを消去します
- CSS 構文を検証します
- ローカル開発環境でテストします

+++

+++ユニバーサルエディターの問題

**問題：**&#x200B;ユニバーサルエディターにフォームコンポーネントが表示されない

**解決策：**

- AEM コード同期がインストールおよび実行されていることを検証します
- `fstab.yaml` に正しい AEM オーサー URL が含まれていることを確認します
- AEM インスタンスで早期アクセスが有効になっていることを確認します
- `component-definition.json` にフォームコンポーネントが含まれていることを確認します

**問題：**&#x200B;公開後に変更が表示されない

**解決策：**

- CDN キャッシュの更新を待機します
- ブラウザーキャッシュを確認します（匿名／プライベートモードを試します）
- 正しい URL 形式が使用されていることを検証します

+++



