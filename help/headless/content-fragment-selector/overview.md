---
title: Adobe Experience Manager as a Cloud Service 用マイクロフロントエンドコンテンツフラグメントセレクター
description: アプリケーションからコンテンツフラグメントを検索、発見、取得するのにマイクロフロントエンドコンテンツフラグメントセレクターを使用します。
role: Admin, User
exl-id: 5b18fb2c-26c8-4d9d-ba2e-9e53c09f5022
source-git-commit: 84fcdd729bb79096e1a058961c174f9b2b626ba9
workflow-type: ht
source-wordcount: '743'
ht-degree: 100%

---

# マイクロフロントエンドコンテンツフラグメントセレクター {#micro-frontend-content-fragment-selector}

マイクロフロントエンドコンテンツフラグメントセレクターは、Adobe Experience Manager（AEM）as a Cloud Service リポジトリと簡単に統合できるユーザーインターフェイスを提供します。このインターフェイスを使用すると、リポジトリ内のコンテンツフラグメントを参照または検索し、アプリケーションで使用できます。

コンテンツフラグメントセレクターパッケージを使用すると、マイクロフロントエンドのユーザーインターフェイスをアプリケーションで利用できるようになります。パッケージのアップデートはすべて自動的に読み込まれ、アプリケーションに読み込まれます。

![マイクロフロントエンドコンテンツフラグメントセレクター - 概要](/help/headless/assets/content-fragment-selector-overview.png)

コンテンツフラグメントセレクターには、次のような多くの利点があります。

* 任意のアドビアプリケーションとの統合が簡単です。
* コンテンツフラグメントセレクターパッケージのアップデートがアプリケーションで使用可能なコンテンツフラグメントセレクターに自動的にデプロイされるので、管理が簡単です。つまり、アプリケーションで最新の修正内容を読み込むアクションを実行する必要はありません。
* アプリケーション内のコンテンツフラグメントセレクターの表示を制御するプロパティを使用するので、カスタマイズが簡単です。
* フルテキスト検索とカスタマイズ可能なフィルターを併用すると、オーサリングエクスペリエンス内でコンテンツフラグメントをすばやく移動できます。
* IMS 組織内のリポジトリを切り替えて、コンテンツフラグメントを選択できます。
* コンテンツフラグメントを並べ替えたり、選択したビューで表示したりできます。

## 前提条件 {#prerequisites}

### IMS 認証 {#ims-authentication}

IMS 認証ワークフローが必要な場合は、次を確認する必要があります。

* アプリケーションは `HTTPS` で実行されている。
* アプリケーションの URL は、IMS クライアントで許可されるリダイレクト URL のリストにある。
* IMS ログインフローは、web ブラウザーのポップアップを使用して設定およびレンダリングされる。そのため、ターゲットブラウザーでポップアップを有効または許可する必要があります。

または、アプリケーションが IMS ワークフローで既に認証されている場合は、代わりに適切な IMS 情報を追加できます。

## インストール {#installation}

`ContentFragmentSelector` コンポーネントを使用します。いくつかのインストールオプションがあります。

1. NPM レジストリ（プライベート Adobe レジストリ）

   * `.npmrc` に次の内容を追加します。

     ```html
     @aem-sites:registry=https://artifactory.corp.adobe.com/artifactory/api/npm/npm-aem-sites-release/
     ```

   * 次に、以下をインストールします。

     ```html
     npm install @aem-sites/content-fragment-selector
     ```

1. Git リポジトリ

   * `package.json` の依存関係に次の内容を追加します。

     ```html
     "@aem-sites/content-fragment-selector": "git+https://github.com/adobe/<your-private-repo-url>.git#version"
     ```

## コンテンツフラグメントセレクターの使用 {#using-the-Content-Fragment-selector}

コンテンツフラグメントセレクターを設定し、AEM as a Cloud Service アプリケーションでコンテンツフラグメントセレクターの使用が認証されると、コンテンツフラグメントを選択したり、その他の様々な操作を実行してリポジトリ内でフラグメントを検索したりできます。

![コンテンツフラグメントセレクター](/help/headless/assets/content-fragment-selector-using.png)

* 右上の&#x200B;**リポジトリ**&#x200B;セレクターを使用すると、使用するリポジトリを選択できます。
* 左端のパネルでは、次の操作を実行できます。
   * 選択したリポジトリのフォルダーを非表示または表示
   * 特定のフォルダーを選択して、そのフォルダー内のコンテンツフラグメントを表示
* メインパネルでは、次の操作を実行できます。
   * コンテンツフラグメントを選択
   * コンテンツフラグメントを検索
   * 現在のリストを様々な列に従って昇順または降順で並べ替え
   * 表示形式インジケーターを参照
   * フィルターを表示、非表示、指定

### パネルの非表示／表示 {#hide-show-panel}

左側のナビゲーションでフォルダーを非表示にするには、「**フォルダーを非表示**」アイコンをクリックします。変更を元に戻すには、「**フォルダーを非表示**」アイコンを再度クリックします。

### リポジトリスイッチャー {#repository-switcher}

コンテンツフラグメントセレクターを使用すると、フラグメント選択用のリポジトリを選択できます。

メインパネルの上部にある&#x200B;**リポジトリ**&#x200B;ドロップダウンから、目的のリポジトリを選択できます。

![コンテンツフラグメントセレクター](/help/headless/assets/content-fragment-repository-selector.png)

ドロップダウンリストで使用できるリポジトリオプションは、`index.html` ファイルで定義されている `repositoryId` プロパティに基づいています。このプロパティは、現在ログインしているユーザーがアクセスする、選択された IMS 組織の環境に基づいています。

消費者は優先する `repositoryID` を渡して特定のリポジトリからのフラグメントをレンダリングし、リポジトリスイッチャーのレンダリングを停止できます。

### コンテンツフラグメントフォルダー {#content-fragments-folders}

コンテンツフラグメントリポジトリは、操作の実行に使用できるコンテンツフラグメントフォルダーのコレクションです。

### フィルター {#filters}

コンテンツフラグメントセレクターには、検索結果を絞り込む標準のフィルターオプションも用意されています。次のような様々なフィルターを使用できます。

* **フラグメントモデル**
* **ローカライゼーション**
* **ステータス**：フラグメントの現在の状態（`New`、`Draft`、`Published`、`Modified`、`Unpublished`）
* タグ
* ユーザー
* 時刻と日付

![フィルターオプション](/help/headless/assets/content-selector-filters.png)

また、デフォルトの検索フィルターを作成して、後で使用するために保存することもできます。コンテンツフラグメントのカスタム検索フィルターを作成するには、`filterSchema` プロパティを使用できます。

### 検索バー {#search-bar}

コンテンツフラグメントセレクターを使用すると、選択したリポジトリ内のフラグメントに対してフルテキスト検索を実行できます。例えば、検索バーにキーワード「`wave`」を入力すると、メタデータプロパティのいずれかでキーワード「`wave`」が記述されているフラグメントがすべて表示されます。

### 並べ替え {#sorting}

コンテンツフラグメントセレクターでは、様々なプロパティでフラグメントを並べ替えることができます。フラグメントを昇順または降順で並べ替えることもできます。

### 表示タイプ {#view-type}

コンテンツフラグメントセレクターを使用すると、以下でフラグメントを表示できます。

* **テーブル表示**
