---
title: オーサリングの基本
description: コンテンツフラグメントを使用したヘッドレス CMS のコンテンツオーサリングの概念と仕組みについて説明します。
exl-id: 3eca973f-b210-41bb-98da-ecbd2bae9803
solution: Experience Manager
feature: Headless, Content Fragments,GraphQL API
role: Admin, Architect, Developer
source-git-commit: bdf3e0896eee1b3aa6edfc481011f50407835014
workflow-type: tm+mt
source-wordcount: '1727'
ht-degree: 100%

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

AEM のインストールは、通常、次の 3 つの環境で構成されます。

* 作成者
* 公開
* プレビュー

ログインし、オーサー環境を使用してコンテンツを生成します。準備が整ったら、コンテンツを公開して、一般に利用できるようにします。ヘッドレスの場合は、他のアプリケーションに対して行われ、web ページの場合は、web 上の読者に対して行われます。

詳しくは、「オーサリングに関する概念」を参照してください。

**コンテンツフラグメント**&#x200B;コンソールでは、公開前のテストおよびプレビュー用に、**プレビューサービス**&#x200B;に公開することもできます。詳しくは、フラグメントの公開とプレビューを参照してください。

### ログイン {#signing-in}

ほとんどのシステムと同様に、ログオンする必要があります。作成者には、次の情報が提供されます。

* ユーザー（アカウント）名
* パスワード
* ログイン画面にアクセスするためのリンク

アカウントには、必要な権限が前もって設定されています。問題がある場合は、社内のプロジェクトサポートチームに問い合わせることをお勧めします。

### ナビゲーション {#navigation}

初めてログインすると、簡単なオンラインチュートリアルでユーザーインターフェイスの主な機能がいくつか紹介されます。

その後、ナビゲーションパネルを使用して、AEMの主要な領域にアクセスできます。コンテンツフラグメントの場合、**コンテンツフラグメント**&#x200B;コンソールを使用します（一部のアクションに対しては、**Assets** コンソールも使用します）。

ナビゲーションパネルを開くには、左上の Adobe アイコンを選択し、次に小さいコンパスアイコンを選択します。

<!--
The Navigation Panel can be opened by selecting Adobe icon at the top left, followed by the small compass icon:

![Navigation panel](/help/journey-headless/author/assets/headless-journey-author-navigation-01.png)
-->

>[!NOTE]
>コンテンツフラグメントは AEM **Sites** の機能ですが、**Assets** として保存されます。これは技術的なことでユーザーには関係ありませんが、知っておくと役に立つ場合があります。

コンソール内では、左側のパネルでフォルダーを選択して、コンテンツフラグメントに移動できます。また、フィルターや検索も可能です。

![コンテンツフラグメントコンソール](/help/sites-cloud/administering/content-fragments/assets/cf-managing-console-filter.png)

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

以上、AEM ユーザーインターフェイス（UI）について簡単に説明しました。実際に UI を試してみる機会があれば幸いです。ここからは、実際の関心事である、ヘッドレスのコンテンツフラグメンについて説明します。

最初から最後まで説明する必要がありますが、お使いのインスタンスにはフォルダーやフラグメントが既に作成されていて、それらが様々な場所に存在している可能性があります。原則はすべて同じです。

### 整理とナビゲーション {#organizing-and-navigating}

コンテンツフラグメントがほとんどない場合を除き、コンテンツフラグメントを整理して、作成者（および他のユーザー）が見つけやすくします。

#### フォルダーの作成 {#creating-folder}

これを行うには、**Assets** コンソールの「**ファイル**」セクション内に一連のフォルダーを作成します。「**作成**」オプション（右上）を選択したあと、「**フォルダー**」を選択します。

![フォルダー作成オプション](/help/journey-headless/author/assets/headless-journey-author-folder-01.png)

詳細を入力できるダイアログが開くので、入力後、「**作成**」で確定します。

![フォルダー作成ダイアログ](/help/journey-headless/author/assets/headless-journey-author-folder-02.png)

#### フォルダーで使用可能なコンテンツフラグメントモデルをパスとタグで制限する方法 {#tags-paths-for-models-in-folder}

この節の内容は少し上級者向けです。開始したばかりで試している段階ならそれほど必要ではありませんが、多数のフラグメントがある場合に&#x200B;*非常に*&#x200B;便利です。まだ使わなくても、知っておいて損はありません。

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

### フラグメントの編集 {#editing-fragment}

フラグメントは、作成後すぐに開くことも、コンテンツフラグメントコンソール（または Assets コンソール）から選択して開くこともできます。

>[!NOTE]
>
>コンテンツフラグメントは Sites 機能ですが、**Assets** として保存されます。
>
>コンテンツフラグメントをオーサリングするためのエディターは 2 つあります。
>
>* 主に&#x200B;**コンテンツフラグメント**&#x200B;コンソールからアクセスできる新しいエディター。
>* 主に **Assets** コンソールからアクセスされる元のエディター。

エディターが初めて開くと、以下のものが表示されます。

* 上部のツールバー：主要な情報とアクション
   * コンテンツフラグメントコンソールへのリンク（ホームアイコン）
   * モデルとフォルダーに関する情報
   * プレビューへのリンク。モデルにデフォルトのプレビュー URL パターンが設定されている場合。
   * アクションの公開と非公開
   * すべての&#x200B;**親参照**&#x200B;を表示するオプション（リンクアイコン）
   * フラグメント&#x200B;**ステータス**、および最後に保存した情報
   * 元の（アセットベースの）エディターへの切替えスイッチ
* 左側のパネル：コンテンツフラグメント用&#x200B;**バリエーション**&#x200B;とその&#x200B;**フィールド**&#x200B;を表示します。
   * これらのリンクを使用して、コンテンツフラグメント構造をナビゲートできます。
* 右側のパネル：プロパティ（メタデータ）とタグ、バージョン履歴に関する情報、任意の言語コピーに関連する情報を示すタブが表示されます
   * 「**プロパティ**」タブで、フラグメントまたは&#x200B;**バリエーション**&#x200B;の&#x200B;**タイトル**&#x200B;および&#x200B;**説明**&#x200B;を更新できます。
* 中央パネル：選択したバリエーションの実際のフィールドとコンテンツを表示します
   * コンテンツの編集が可能
   * 「**タブプレースホルダー**」フィールドは、ここに表示されるモデル内で定義され、ナビゲーションに使用できます

例えば、フラグメントでは次のことが可能です。

* 複数の情報が必要です。一部の情報は特定のタイプを持ちます。ヘッドレスコンテンツの場合、参照は重要です。これについては、後ほどジャーニーの中で説明します。

* 長いテキスト文を書き込むことができます。ここには、テキストを管理および書式設定するための追加のオプションがあります。個々のテキストフィールドを全画面表示エディターで開くこともできます（右側の小さい画面アイコンを使用）。

![コンテンツフラグメントエディター - Alaska Spirits](/help/sites-cloud/administering/content-fragments/assets/cf-authoring-overview.png)

>[!NOTE]
>
>一部のフィールドへの正しい入力方法の詳細を作成者が理解するたに、プロジェクト固有のドキュメントが必要になる場合があります。
>
>一般的な詳細については、「コンテンツフラグメントモデル」の「データタイプ」と「プロパティ」の節を参照してください。

「**保存**」または「**保存して閉じる**」を使用して、更新を確定します。

>[!NOTE]
>
>詳しくは、「バリエーション - フラグメントコンテンツのオーサリング」を参照してください。

#### （おそらく）気にする必要がないもの {#what-you-probably-do-not-need-to-worry-about}

やや奇妙なタイトルのセクションですが、コンテンツフラグメントエディターを開いて詳細な作業に入ると、コンテンツ作成者のヘッドレスジャーニーに（おそらく）当てはまらない様々なオプションが表示されることになります。そこで、ここでは、ヘッドレスコンテキストで無視できるものについて簡単に説明しておきます。

* **コンテンツフラグメントモデル**

  エディターの右側のパネルにコンテンツフラグメントモデルの名前が表示されます。これは、モデルエディターに移動するリンクでもあります。
コンテンツフラグメントモデルは、使用する構造を定義するものなので、実際にはコンテンツフラグメントにとってきわめて重要です。ただし、コンテンツフラグメントモデルの作成と編集を担当するのは、（通常は）別のペルソナであるコンテンツアーキテクトです。

  >[!NOTE]
  >
  >詳しくは、「AEM ヘッドレスコンテンツアーキテクトジャーニー」を参照してください。

### 公開 {#publishing}

<!-- needs more details -->

フラグメントが完成したら&#x200B;**公開**&#x200B;して、ヘッドレスアプリケーションで利用できるようにします。

公開アクションはエディターで使用できます。

![コンテンツフラグメントエディター - マイフラグメント](/help/journey-headless/author/assets/headless-journey-author-content-fragment-06.png)

>[!NOTE]
>
>また、**Assets** コンソールや&#x200B;**コンテンツフラグメント**&#x200B;コンソールからもフラグメントを公開できます。

## 次の手順 {#whats-next}

これで基本を説明したので、次のステップは[コンテンツフラグメントでの参照の使用について](references.md)です。ここでは、使用可能な様々な参照を紹介し、ヘッドレス向けオーサリングの重要な部分であるフラグメント参照を使用した構造レベルの作成方法について説明します。

## その他のリソース {#additional-resources}

* [オーサリングに関する概念](/help/sites-cloud/authoring/author-publish.md)

* [基本操作](/help/sites-cloud/authoring/basic-handling.md) - このページは主に **Sites** コンソールに基づいていますが、多くの／ほとんどの機能は **Assets** コンソールでの&#x200B;**コンテンツフラグメント**&#x200B;のオーサリングにも関連しています。

   * [ナビゲーションパネル](/help/sites-cloud/authoring/basic-handling.md#navigation-panel)

   * [ヘッダー](/help/sites-cloud/authoring/basic-handling.md#the-header)

   * [アクションツールバー](/help/sites-cloud/authoring/basic-handling.md#actions-toolbar)

   * [クイックアクション](/help/sites-cloud/authoring/basic-handling.md#quick-actions)

   * [リソースの表示と選択](/help/sites-cloud/authoring/basic-handling.md#viewing-and-selecting-resources)

   * [パネルセレクター](/help/sites-cloud/authoring/basic-handling.md#rail-selector)

* [コンテンツフラグメントの使用方法](/help/sites-cloud/administering/content-fragments/overview.md)

   * [コンテンツフラグメントの管理](/help/sites-cloud/administering/content-fragments/managing.md)

   * [アセットフォルダーへの設定の適用](/help/sites-cloud/administering/content-fragments/setup.md#apply-the-configuration-to-your-folder)

   * [コンテンツフラグメントの作成](/help/sites-cloud/administering/content-fragments/managing.md#creating-a-content-fragment)

   * [コンテンツフラグメントのオーサリング](/help/sites-cloud/administering/content-fragments/authoring.md)

   * 公開

      * エディターまたは **Assets** コンソールから

         * [クイック公開](/help/assets/manage-publication.md#quick-publish)

         * [公開を管理](/help/assets/manage-publication.md#manage-publication)

      * **コンテンツフラグメント**&#x200B;コンソールから

         * [コンテンツフラグメントの公開とプレビュー](/help/sites-cloud/administering/content-fragments/managing.md#publishing-and-previewing-a-fragment)

   * [コンテンツフラグメントモデル](/help/sites-cloud/administering/content-fragments/content-fragment-models.md)

      * [コンテンツフラグメントモデル - データタイプ](/help/sites-cloud/administering/content-fragments/content-fragment-models.md#data-types)

      * [コンテンツフラグメントモデル - プロパティ](/help/sites-cloud/administering/content-fragments/content-fragment-models.md#properties)

      * [コンテンツフラグメントモデル - アセットフォルダーでのコンテンツフラグメントモデルの許可](/help/sites-cloud/administering/content-fragments/content-fragment-models.md#allowing-content-fragment-models-assets-folder)

* [コンテンツフラグメント - アセットコンソールからの元のエディター](/help/assets/content-fragments/content-fragments-variations.md)

* はじめる前に
   * [アセットフォルダーの作成 - ヘッドレスセットアップ](/help/headless/setup/create-assets-folder.md)

* AEM ヘッドレスコンテンツアーキテクトジャーニー

* AEM ヘッドレス翻訳ジャーニー
