---
title: オーサリングの基本
description: コンテンツフラグメントを使用したヘッドレス CMS のコンテンツオーサリングの概念と仕組みについて説明します。
exl-id: 3eca973f-b210-41bb-98da-ecbd2bae9803
source-git-commit: 1473c1ffccc87cb3a0033750ee26d53baf62872f
workflow-type: tm+mt
source-wordcount: '1715'
ht-degree: 85%

---

# AEM を使用したヘッドレスのオーサリングの基本 {#author-headless-basics}

## これまでの説明内容 {#story-so-far}

[AEM ヘッドレスコンテンツ作成者ジャーニー](overview.md)の冒頭の[はじめに](introduction.md)で、ヘッドレス向けのオーサリングに関連する基本概念と用語について説明しました。

この記事では、これらに基づいて、AEM ヘッドレスプロジェクト用に独自のコンテンツをオーサリングする方法を説明します。

## 目的 {#objective}

* **対象読者**：初心者
* **目的**：ヘッドレス CMS オーサリングの基本を紹介します。
   * AEMaaCS を使用したオーサリングの概要
   * コンテンツフラグメントの概要

## 基本操作 {#basic-handling}

コンテンツフラグメントについて理解する前に、AEM の使用方法を簡単に説明します。実際には、ログインしてシステムを実際に使用してみるのが一番です。

### オーサー、プレビュー、パブリッシュ {#author-preview-publish}

AEMのインストールは、通常、次の 3 つの環境で構成されます。

* 作成者
* 公開
* プレビュー

ログインし、オーサー環境を使用してコンテンツを生成します。準備が整ったら、コンテンツを公開して、一般に利用できるようにします。ヘッドレスの場合は、他のアプリケーションに対して行われ、web ページの場合は、web 上の読者に対して行われます。

詳しくは、「オーサリングに関する概念」を参照してください。

次の **コンテンツフラグメント** コンソールで、 **プレビューサービス**（公開前のテストおよびプレビュー用） 詳しくは、フラグメントの公開とプレビューを参照してください。

### ログイン {#signing-in}

ほとんどのシステムと同様に、ログオンする必要があります。 作成者は、次の情報を提供します。

* ユーザー（アカウント）名
* パスワード
* ログイン画面にアクセスするためのリンク

アカウントには、必要な権限が前もって設定されています。問題がある場合は、社内のプロジェクトサポートチームに問い合わせることをお勧めします。

### ナビゲーション {#navigation}

初めてログインすると、簡単なオンラインチュートリアルでユーザーインターフェイスの主な機能がいくつか紹介されます。

その後、ナビゲーションパネルを使用して、AEMの主要な領域にアクセスできます。コンテンツフラグメントの場合は、 **コンテンツフラグメント** コンソール ( 一部のアクションに対しては、 **Assets** コンソール )。

ナビゲーションパネルを開くには、左上の Adobe アイコンを選択し、次に小さいコンパスアイコンを選択します。

<!--
The Navigation Panel can be opened by selecting Adobe icon at the top left, followed by the small compass icon:

![Navigation panel](/help/journey-headless/author/assets/headless-journey-author-navigation-01.png)
-->

>[!NOTE]
>コンテンツフラグメントは AEM **Sites** の機能ですが、**Assets** として保存されます。これは技術的なことでユーザーには関係ありませんが、知っておくと役に立つ場合があります。

コンソール内では、左側のパネルでフォルダーを選択して、コンテンツフラグメントに移動できます。また、フィルターや検索も可能です。

![コンテンツフラグメントコンソール](/help/sites-cloud/administering/content-fragments/assets/cfc-console-filter.png)

### アクション、選択、表示 {#actions-selecting-viewing}

**コンテンツフラグメント**&#x200B;コンソールでは、ツールバーからコンテンツフラグメントに対して様々なアクションを実行できます。

<!-- ![Console actions](assets/cfm-managing-cf-console-01.png) -->

* **Assets で開く**
* **作成**
* **参照元**&#x200B;列には、そのフラグメントのすべての親参照を表示するための直接リンクもあります。コンテンツフラグメント、エクスペリエンスフラグメントおよびページの参照が含まれます。
* フォルダー名にカーソルを合わせると、JCR パスが表示されます。

フラグメントを選択すると、該当するすべてのアクションを使用できるようになります。

<!-- ![Console actions - fragment selected](assets/cfm-managing-cf-console-selected-01.png) -->

* **開く**
* **公開**（および **非公開**）
* **コピー**
* **移動**
* **名前を変更**
* **削除**

>[!NOTE]
>
>公開、非公開、削除、移動、名前を変更、コピーなどのアクションは、非同期ジョブをトリガーします。そのジョブの進行状況は、AEM 非同期ジョブ UI で監視できます。

<!--
The **Assets** console has dedicated **Action Toolbars**, and **Quick Actions** that you can use after selecting a resource (for example, a folder or content fragment).

The Quick Actions are available for a single resource, see **Basel** in the example below:

![Quick Actions](/help/journey-headless/author/assets/headless-journey-author-navigation-05.png)

The Actions Toolbar provides access to the full range of actions - applicable for the current scenario. The actions available can change; for example, dependent on your location, or whether you have selected multiple resources:

![Action Toolbar](/help/journey-headless/author/assets/headless-journey-author-navigation-06.png)

You can select the format for viewing your resources with the View Selector:

![View Selector](/help/journey-headless/author/assets/headless-journey-author-navigation-03.png)

You can view additional information about items using the Rail Selector. This also gives access to additional actions.

![Left Rail](/help/journey-headless/author/assets/headless-journey-author-navigation-04.png)
-->

## コンテンツフラグメントのオーサリング {#authoring-content-fragments}

これはAEMユーザーインターフェイス (UI) の簡単な紹介でしたが、ぜひ試してみて欲しいと思います。 ここからは、実際の関心事である、ヘッドレスのコンテンツフラグメンについて説明します。

最初から最後まで説明する必要がありますが、お使いのインスタンスにはフォルダーやフラグメントが既に作成されていて、それらが様々な場所に存在している可能性があります。原則はすべて同じです。

### 整理とナビゲーション {#organizing-and-navigating}

コンテンツフラグメントがほとんどない場合を除き、コンテンツフラグメントを整理して、作成者（および他のユーザー）が見つけやすくします。

#### フォルダーの作成 {#creating-folder}

これを行うには、**Assets** コンソールの「**ファイル**」セクション内に一連のフォルダーを作成します。「**作成**」オプション（右上）を選択したあと、「**フォルダー**」を選択します。

![フォルダー作成オプション](/help/journey-headless/author/assets/headless-journey-author-folder-01.png)

詳細を入力できるダイアログが開くので、入力後、「**作成**」で確定します。

![フォルダー作成ダイアログ](/help/journey-headless/author/assets/headless-journey-author-folder-02.png)

#### フォルダーで使用可能なコンテンツフラグメントモデルをパスとタグで制限する方法 {#tags-paths-for-models-in-folder}

この節の内容は少し上級者向けです。何かを始めて試すだけでは、本当に必要ありませんが、それは *非常に* 多数のフラグメントがある場合に便利です。 だから、まだ使っていなくても、知っておくのが良い。

コンテンツアーキテクトは、現在のプロジェクトや他のプロジェクトに必要なすべてのコンテンツフラグメントモデルを作成しています。自分自身や他の作成者が作業を簡単に行えるように、特定のフォルダーで使用できるモデルのリストを制限できます。

フォルダーを作成したら、そのフォルダーの&#x200B;**プロパティ**&#x200B;を開きます。ここには、フォルダーに関する情報と設定詳細の様々なタブがあります。特に、コンテンツフラグメントの場合は、「**ポリシー**」タブを使用して、このフォルダーに特定のパスやタグを定義できます。これにより、フォルダーで使用できるコンテンツフラグメントモデルが制限されます。つまり、コンテンツフラグメントモデルを使用してこのフォルダーでフラグメントを生成するには、これらの要件を満たす必要があるということです。

![フォルダープロパティの作成 - ポリシー](/help/journey-headless/author/assets/headless-journey-author-folder-04.png)

>[!NOTE]
>
>詳しくは、「コンテンツフラグメントモデル」の「アセットフォルダーでのコンテンツフラグメントモデルの許可」の節を参照してください。

次に、これらのフォルダーを移動して、コンテンツフラグメントの作成と編集を行います。

#### フォルダークラウドサービスの設定（参考まで） {#cloud-services-folder}

以下は参考までに説明しておきます。

フォルダーを作成できる初期フォルダーがあらかじめ用意されているはずです。これは、一部の設定詳細を（通常は開発者またはシステム管理者が）ルートフォルダーに適用する必要があるからです。必要であれば、フォルダーの&#x200B;**プロパティ**&#x200B;の「**クラウドサービス**」タブで「**クラウドサービス設定**」を確認してください。

![フォルダープロパティの作成 - 設定](/help/journey-headless/author/assets/headless-journey-author-folder-03.png)

>[!NOTE]
>
>詳しくは、「アセットフォルダーへの設定の適用」を参照してください。

### コンテンツフラグメントの作成 {#creating-fragment}

**コンテンツフラグメント**&#x200B;コンソールでは、「**作成**」を使用して&#x200B;**新しいコンテンツフラグメント**&#x200B;ダイアログを開きます。

![コンテンツフラグメントコンソール - 新しいフラグメントの作成](/help/sites-cloud/administering/content-fragments/assets/cfc-console-create.png)

以下を指定します。

* **場所**
* **コンテンツフラグメントモデル**
* **タイトル**
* **名前**
* **説明**

次に、「**作成**」または「**作成して開く**」で確定します。

<!--
Creating a Content Fragment is very similar - you just use the **Content Fragment** option instead:

![Create Content Fragment option](/help/journey-headless/author/assets/headless-journey-author-content-fragment-01.png)

This time a wizard opens. The first step is to select the Content Fragment Model that your fragment is based on:

![Create Content Fragment - select Model](/help/journey-headless/author/assets/headless-journey-author-content-fragment-02.png)

After continuing with **Next** you can supply the details (**Basic** and **Advanced**) for your fragment:

![Create Content Fragment - provide Name](/help/journey-headless/author/assets/headless-journey-author-content-fragment-03.png)

Confirm with **Create** and you can then **Open** your fragment in the editor.
-->

### フラグメントの編集 {#editing-fragment}

フラグメントは、作成後すぐに開くことも、コンテンツフラグメントコンソール（または Assets コンソール）から選択して開くこともできます。

エディターが最初に開くと、次のように表示されます。

* 左側のアイコンリスト - 様々な機能領域にアクセスできます。「**バリエーション**」タブにエディターが開きます。編集作業のほとんどは、ここで行います。「**注釈**」タブと「**メタデータ**」タブも必要になるかもしれません。

* フラグメントに関する情報が表示され、様々なアクションにもアクセスできるヘッダー。

* メインの編集領域 - フラグメントの作成に使用したモデルによって異なります。

例：

* 複数の情報（一部は特定のタイプのもの）のみを必要とするフラグメント。ヘッドレスコンテンツの場合、参照は重要です（これらについては、後でジャーニーで学びます）。

  ![コンテンツフラグメントエディター - マイフラグメント](/help/journey-headless/author/assets/headless-journey-author-content-fragment-04.png)

* 長いテキストを書き込むことができるフラグメント。ここには、テキストを管理および書式設定するための追加のオプションがあります。個々のテキストフィールドを全画面表示エディターで開くこともできます（右側の小さい画面アイコンを使用）。

  ![コンテンツフラグメントエディター - Alaska Spirits](/help/journey-headless/author/assets/headless-journey-author-content-fragment-05.png)

>[!NOTE]
>
>一部のフィールドへの正しい入力方法の詳細を作成者が理解するたに、プロジェクト固有のドキュメントが必要になる場合があります。
>
>一般的な詳細については、「コンテンツフラグメントモデル」の「データタイプ」と「プロパティ」の節を参照してください。

「**保存**」または「**保存して閉じる**」を使用して、更新を確定します。

>[!NOTE]
>
>詳しくは、「バリエーション - フラグメントコンテンツのオーサリング」を参照してください。

#### （おそらく）心配する必要のないもの {#what-you-probably-do-not-need-to-worry-about}

これは少し奇妙な節に思えるかもしれませんが、コンテンツフラグメントエディターを開いて調査を開始すると、コンテンツ作成者としてヘッドレスジャーニーに適用されない（おそらく）様々なオプションを確認できます。 そこで、ここでは、ヘッドレスコンテキストで無視できるものについて簡単に説明しておきます。

* **コンテンツフラグメントモデル**

  エディター上部のフラグメント名のすぐ下に、コンテンツフラグメントモデルの名前が表示されます。これは、モデルエディターに移動するリンクでもあります。
コンテンツフラグメントモデルは、使用する構造を定義するものなので、実際にはコンテンツフラグメントにとってきわめて重要です。ただし、コンテンツフラグメントモデルの作成と編集を担当するのは、（通常は）別のペルソナであるコンテンツアーキテクトです。

  >[!NOTE]
  >
  >詳しくは、「AEM ヘッドレスコンテンツアーキテクトジャーニー」を参照してください。

* **関連コンテンツ**

  これはエディターのタブなので明らかです。

  コンテンツフラグメント機能は、AEM ではかなり前のバージョンから利用可のです。元々は、ページのオーサリング時に「従来の」用途に使用できるようになっていました。同様の使い方は使用されています。これには、フラグメントに埋め込まれてはいないものの、ページのオーサリング時に作成者が使用できる必要があるアセット（画像など）の関連付けが含まれる場合があります。

* **プレビュー**

  これはエディターの別のタブで、主に開発者向けの技術的な内容を提供します。

* **ページ参照を更新**

  このアクションは、 **...** （省略記号）ドロップダウン これはページのオーサリングに関係するものなので、ヘッドレス作成者向けのものではありません。

### 公開 {#publishing}

<!-- needs more details -->

フラグメントが完成したら&#x200B;**公開**&#x200B;して、ヘッドレスアプリケーションで利用できるようにします。

エディターでは、公開アクションを使用できます。

![コンテンツフラグメントエディター - マイフラグメント](/help/journey-headless/author/assets/headless-journey-author-content-fragment-06.png)

>[!NOTE]
>
>また、 **Assets** または **コンテンツフラグメント** コンソール。

## 次の手順 {#whats-next}

これで基本を説明したので、次のステップは[コンテンツフラグメントでの参照の使用について](references.md)です。ここでは、使用可能な様々な参照を紹介し、ヘッドレス向けオーサリングの重要な部分であるフラグメント参照を使用した構造レベルの作成方法について説明します。

## その他のリソース {#additional-resources}

* [オーサリングに関する概念](/help/sites-cloud/authoring/getting-started/concepts.md)

* [基本操作](/help/sites-cloud/authoring/getting-started/basic-handling.md) - このページは主に **Sites** コンソールに基づいていますが、多くの／ほとんどの機能は **Assets** コンソールでの&#x200B;**コンテンツフラグメント**&#x200B;のオーサリングにも関連しています。

   * [ナビゲーションパネル](/help/sites-cloud/authoring/getting-started/basic-handling.md#navigation-panel)

   * [ヘッダー](/help/sites-cloud/authoring/getting-started/basic-handling.md#the-header)

   * [アクションツールバー](/help/sites-cloud/authoring/getting-started/basic-handling.md#actions-toolbar)

   * [クイックアクション](/help/sites-cloud/authoring/getting-started/basic-handling.md#quick-actions)

   * [リソースの表示と選択](/help/sites-cloud/authoring/getting-started/basic-handling.md#viewing-and-selecting-resources)

   * [パネルセレクター](/help/sites-cloud/authoring/getting-started/basic-handling.md#rail-selector)

* [コンテンツフラグメントの使用方法](/help/sites-cloud/administering/content-fragments/content-fragments.md)

   * [コンテンツフラグメントの管理](/help/sites-cloud/administering/content-fragments/content-fragments-managing.md)

   * [アセットフォルダーへの設定の適用](/help/sites-cloud/administering/content-fragments/content-fragments-configuration-browser.md#apply-the-configuration-to-your-assets-folder)

   * [コンテンツフラグメントの作成](/help/sites-cloud/administering/content-fragments/content-fragments-managing.md#creating-a-content-fragment)

   * [バリエーション - コンテンツフラグメントのオーサリング](/help/sites-cloud/administering/content-fragments/content-fragments-variations.md)

   * 公開

      * エディターから、または **Assets** コンソール

         * [クイック公開](/help/assets/manage-publication.md#quick-publish)

         * [公開を管理](/help/assets/manage-publication.md#manage-publication)

      * 次の **コンテンツフラグメント** コンソール

         * [コンテンツフラグメントの公開とプレビュー](/help/sites-cloud/administering/content-fragments/content-fragments-managing.md#publishing-and-previewing-a-fragment)

   * [コンテンツフラグメントモデル](/help/sites-cloud/administering/content-fragments/content-fragments-models.md)

      * [コンテンツフラグメントモデル - データタイプ](/help/sites-cloud/administering/content-fragments/content-fragments-models.md#data-types)

      * [コンテンツフラグメントモデル - プロパティ](/help/sites-cloud/administering/content-fragments/content-fragments-models.md#properties)

      * [コンテンツフラグメントモデル - アセットフォルダーでのコンテンツフラグメントモデルの許可](/help/sites-cloud/administering/content-fragments/content-fragments-models.md#allowing-content-fragment-models-assets-folder)

* はじめる前に
   * [アセットフォルダーの作成 - ヘッドレスセットアップ](/help/headless/setup/create-assets-folder.md)

* AEM ヘッドレスコンテンツアーキテクトジャーニー

* AEM ヘッドレス翻訳ジャーニー
