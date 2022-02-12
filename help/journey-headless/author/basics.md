---
title: オーサリングの基本
description: コンテンツフラグメントを使用したヘッドレス CMS のコンテンツオーサリングの概念と仕組みについて説明します。
exl-id: 3eca973f-b210-41bb-98da-ecbd2bae9803
source-git-commit: e304b49b44cf871f3c47120fad7899407c573234
workflow-type: tm+mt
source-wordcount: '1696'
ht-degree: 99%

---

# AEM を使用したヘッドレスのオーサリングの基本 {#author-headless-basics}

## これまでの説明内容 {#story-so-far}

[AEM ヘッドレスコンテンツ作成者ジャーニー](overview.md)の冒頭の[はじめに](introduction.md)で、ヘッドレスのオーサリングに関連する基本概念と用語について説明しました。

この記事では、これらに基づいて、AEM ヘッドレスプロジェクト用に独自のコンテンツをオーサリングする方法を説明します。

## 目的 {#objective}

* **対象読者**：初心者
* **目的**：ヘッドレス CMS オーサリングの基本を紹介します。
   * AEMaaCS を使用したオーサリングの概要
   * コンテンツフラグメントの概要

## 基本操作 {#basic-handling}

コンテンツフラグメントについて理解する前に、AEM の使用方法を簡単に説明します。実際には、ログインしてシステムを実際に使用してみるのが一番です。

### オーサーとパブリッシュ {#author-preview-publish}

AEM インストールは、通常、少なくとも次の 2 つの環境で構成されます。

* 作成者
* 公開

ログインし、オーサー環境を使用してコンテンツを生成します。準備が整ったら、コンテンツを公開して、一般に利用できるようにします。ヘッドレスの場合は、他のアプリケーションに対して行われ、web ページの場合は、web 上の読者に対して行われます。

詳しくは、「オーサリングに関する概念」を参照してください。

### ログイン {#signing-in}

ほとんどのシステムと同様に、ログインが必要です。作成者には、次の情報が提供されます。

* ユーザー（アカウント）名
* パスワード
* ログイン画面にアクセスするためのリンク

アカウントには、必要な権限が前もって設定されています。問題がある場合は、社内のプロジェクトサポートチームに問い合わせることをお勧めします。

### ナビゲーション {#navigation}

初めてログインすると、簡単なオンラインチュートリアルでユーザーインターフェイスの主な機能がいくつか紹介されます。

その後、ナビゲーションパネルを使用して、AEMの主要な領域にアクセスできます。コンテンツフラグメントの場合は、**Assets コンソール**&#x200B;を使用します。

ナビゲーションパネルを開くには、左上の Adobe アイコンを選択し、次に小さいコンパスアイコンを選択します。

![ナビゲーションパネル](/help/journey-headless/author/assets/headless-journey-author-navigation-01.png)

>[!NOTE]
>コンテンツフラグメントは AEM **Sites** の機能ですが、**Assets** コンソールからアクセスできます。これは技術的なことでユーザーには関係ありませんが、知っておくと役に立つ場合があります。

コンソール内では、フォルダーを選択してコンテンツフラグメントに移動したり、（ヘッダー内の）パンくずリストを選択してツリーの上に戻ることができます。

![パンくずリスト](/help/journey-headless/author/assets/headless-journey-author-navigation-02.png)

### アクション、選択、表示 {#actions-selecting-viewing}

**Assets** コンソールには、リソース（フォルダーやコンテンツフラグメントなど）を選択した後で使用できる専用の&#x200B;**アクションツールバー**&#x200B;および&#x200B;**クイックアクション**&#x200B;があります。

クイックアクションは、1 つのリソースに対して使用できます。下の **Basel** を参照してください。

![クイックアクション](/help/journey-headless/author/assets/headless-journey-author-navigation-05.png)

アクションツールバーでは、現在のシナリオに適用できるすべてのアクションにアクセスできます。使用可能なアクションは、場所や選択したリソース数（１ つまたは複数）によって変わることがあります。

![アクションツールバー](/help/journey-headless/author/assets/headless-journey-author-navigation-06.png)

リソースの表示形式を表示セレクターで選択できます。

![表示セレクター](/help/journey-headless/author/assets/headless-journey-author-navigation-03.png)

項目に関する追加情報をパネルセレクター表示できます。追加のアクションにもアクセスできます。

![左レール](/help/journey-headless/author/assets/headless-journey-author-navigation-04.png)

## コンテンツフラグメントのオーサリング {#authoring-content-fragments}

以上、AEM ユーザーインターフェイス（UI）について簡単に説明しました。実際に UI を試してみる機会があれば幸いです。ここからは、実際の関心事である、ヘッドレスのコンテンツフラグメンについて説明します。

最初から最後まで説明する必要がありますが、お使いのインスタンスにはフォルダーやフラグメントが既に作成されていて、それらが様々な場所に存在している可能性があります。原則はすべて同じです。

### 整理とナビゲーション {#organizing-and-navigating}

コンテンツフラグメントがほとんどない場合を除き、コンテンツフラグメントを整理して、作成者（および他のユーザー）が見つけやすくします。

#### フォルダーの作成 {#creating-folder}

そのためには、Assets コンソールの「**ファイル**」セクション内に一連のフォルダーを作成します。「**作成**」オプション（右上）を選択したあと、「**フォルダー**」を選択します。

![フォルダー作成オプション](/help/journey-headless/author/assets/headless-journey-author-folder-01.png)

詳細を入力できるダイアログが開くので、入力後、「**作成**」で確定します。

![フォルダー作成ダイアログ](/help/journey-headless/author/assets/headless-journey-author-folder-02.png)

#### フォルダーで使用可能なコンテンツフラグメントモデルをパスとタグで制限する方法 {#tags-paths-for-models-in-folder}

この節の内容は少し上級者向けです。使い始めて間もない場合はあまり必要ありませんが、フラグメントが多数ある場合には&#x200B;*非常に*&#x200B;有効な方法です。まだ使わなくても、知っておいて損はありません。

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

コンテンツフラグメントの作成はフォルダーの作成と非常に似ています。代わりに、「**コンテンツフラグメント**」オプションを使用するだけです。

![コンテンツフラグメントオプションの作成](/help/journey-headless/author/assets/headless-journey-author-content-fragment-01.png)

今度は、ウィザードが開きます。最初の手順では、フラグメントの基になるコンテンツフラグメントモデルを選択します。

![コンテンツフラグメント作成 - モデルの選択](/help/journey-headless/author/assets/headless-journey-author-content-fragment-02.png)

「**次へ**」で続行した後、フラグメントの詳細（「**基本**」および「**詳細**」）を指定できます。

![コンテンツフラグメント作成 - 名前の指定](/help/journey-headless/author/assets/headless-journey-author-content-fragment-03.png)

「**作成**」で確定すると、フラグメントをエディターで&#x200B;**開く**&#x200B;ことができます。

### フラグメントの編集 {#editing-fragment}

フラグメントは、作成後すぐに開くことも、Assets コンソールから選択して開くこともできます。

エディターが初めて開くと、以下のものが表示されます。

* 左側のアイコンリスト - 様々な機能領域にアクセスできます。「**バリエーション**」タブにエディターが開きます。編集作業のほとんどは、ここで行います。「**注釈**」タブと「**メタデータ**」タブも必要になるかもしれません。

* フラグメントに関する情報が表示され、様々なアクションにもアクセスできるヘッダー。

* メインの編集領域 - フラグメントの作成に使用したモデルによって異なります。

例：

* 複数の情報（一部は特定のタイプのもの）のみを必要とするフラグメント。ヘッドレスコンテンツの場合、参照は重要です。これについては、後ほどジャーニーで説明します。

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

#### （おそらく）気にする必要がないもの {#what-you-probably-do-not-need-to-worry-about}

やや奇妙なタイトルの節ですが、コンテンツフラグメントエディターを開いて詳細な作業に入ると、コンテンツ作成者のヘッドレスジャーニーに（おそらく）当てはまらない様々なオプションが表示されることになります。そこで、ここでは、ヘッドレスコンテキストで無視できるものについて簡単に説明しておきます。

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

   このアクションは、「**...**」（省略記号）ドロップダウンから使用できます。これはページのオーサリングに関係するものなので、ヘッドレス作成者向けのものではありません。

### 公開 {#publishing}

<!-- needs more details -->

フラグメントが完成したら&#x200B;**公開**&#x200B;して、ヘッドレスアプリケーションで利用できるようにします。

公開アクションは、エディターで（または **Assets** コンソールのツールバーから）実行できます。

![コンテンツフラグメントエディター - マイフラグメント](/help/journey-headless/author/assets/headless-journey-author-content-fragment-06.png)

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

   * 公開

      * [クイック公開](/help/assets/manage-publication.md#quick-publish)

      * [公開を管理](/help/assets/manage-publication.md#manage-publication)

* [コンテンツフラグメントの操作](/help/assets/content-fragments/content-fragments.md)

   * [コンテンツフラグメントの管理](/help/assets/content-fragments/content-fragments-managing.md)

      * [アセットフォルダーへの設定の適用](/help/assets/content-fragments/content-fragments-configuration-browser.md#apply-the-configuration-to-your-assets-folder)

      * [コンテンツフラグメントの作成](/help/assets/content-fragments/content-fragments-managing.md#creating-a-content-fragment)
   * [バリエーション - コンテンツフラグメントのオーサリング](/help/assets/content-fragments/content-fragments-variations.md)

   * [コンテンツフラグメントモデル](/help/assets/content-fragments/content-fragments-models.md)

      * [コンテンツフラグメントモデル - データタイプ](/help/assets/content-fragments/content-fragments-models.md#data-types)

      * [コンテンツフラグメントモデル - プロパティ](/help/assets/content-fragments/content-fragments-models.md#properties)

      * [コンテンツフラグメントモデル - アセットフォルダーでのコンテンツフラグメントモデルの許可](/help/assets/content-fragments/content-fragments-models.md#allowing-content-fragment-models-assets-folder)


* はじめる前に
   * [アセットフォルダーヘッドレス設定の作成](/help/headless/setup/create-assets-folder.md)

* AEM ヘッドレスコンテンツアーキテクトジャーニー

* AEM ヘッドレス翻訳ジャーニー
