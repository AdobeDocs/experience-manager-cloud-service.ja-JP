---
title: オーサリングの基本を学ぶ
description: コンテンツフラグメントを使用したヘッドレスCMS向けコンテンツのオーサリングの概念と仕組みについて説明します。
index: false
hide: true
hidefromtoc: true
source-git-commit: 41ad9e8ee77ae4494d28026b5ad9da45c06eaeaf
workflow-type: tm+mt
source-wordcount: '1683'
ht-degree: 6%

---


# AEMを使用したヘッドレス向けのオーサリングの基本 {#author-headless-basics}

## 今までの話 {#story-so-far}

[AEMヘッドレスコンテンツ作成者ジャーニー](overview.md)の最初に、[はじめに](introduction.md)では、ヘッドレス作成に関連する基本的な概念と用語について説明しました。

この記事はこれらを基に構築され、AEMヘッドレスプロジェクト用に独自のコンテンツを作成する方法を理解できます。

## 目的 {#objective}

* **オーディエンス**：初心者
* **目的**:ヘッドレスCMSオーサリングの基本を紹介します。
   * AEMaCSを使用したオーサリングの概要
   * コンテンツフラグメントの概要

## 基本操作 {#basic-handling}

コンテンツフラグメントの操作方法を理解する前に、AEMの使用方法を簡単に紹介します。.しかし、実際には、ログインしてシステムを使用しようとする経験に代わるものはありません。

### オーサーインスタンスとパブリッシュインスタンス {#author-preview-publish}

AEM インストールは、通常、少なくとも次の 2 つの環境で構成されます。

* 作成者
* 公開

ログインし、オーサー環境を使用してコンテンツを生成します。 準備が整ったら、コンテンツを公開して、一般に利用できるようにします。 ヘッドレスの場合は、他のアプリケーションに対して、Webページの場合は、Web上の読者に対して行われます。

詳しくは、オーサリングの概念を参照してください。

### ログイン {#signing-in}

ほとんどのシステムと同様に、ログインが必要です。 作成者は、次の情報を提供します。

* ユーザー（アカウント）名
* パスワード
* ログイン画面にアクセスするためのリンク

お使いのアカウントは、必要な権限で設定されます。 問題がある場合は、社内プロジェクトサポートチームにお問い合わせください。

### ナビゲーション {#navigation}

小さなオンラインチュートリアルに初めてログインすると、ユーザーインターフェイスの主な機能の一部が強調表示されます。

その後、ナビゲーションパネルを使用して、AEMの主要な領域にアクセスできます。 コンテンツフラグメントの場合は、**アセットコンソール**&#x200B;を使用します。

ナビゲーションパネルを開くには、左上にあるAdobeアイコンを選択し、次に小さなコンパスアイコンを選択します。

![ナビゲーションパネル](/help/journey-headless/author/assets/headless-journey-author-navigation-01.png)

>[!NOTE]
>コンテンツフラグメントはAEM **Sites**&#x200B;の機能ですが、 **Assets**&#x200B;コンソールにあります。 これは技術的な詳細情報で、ユーザーに影響を与えることはありませんが、知っておくと役に立つ場合があります。

コンソール内で、コンテンツフラグメントに移動するフォルダーを選択するか、（ヘッダーの）パンくずリストを使用してツリーの上に移動します。

![パンくずリスト](/help/journey-headless/author/assets/headless-journey-author-navigation-02.png)

### アクション、選択、表示 {#actions-selecting-viewing}

**アセット**&#x200B;コンソールには、専用の&#x200B;**アクションツールバー**&#x200B;と、リソース選択後に使用できる&#x200B;**クイックアクション**（フォルダーやコンテンツフラグメントなど）があります。

クイックアクションは、1つのリソースに対して使用できます。

![クイックアクション](/help/journey-headless/author/assets/headless-journey-author-navigation-05.png)

アクションツールバーを使用して、現在のシナリオに適用できるすべてのアクションにアクセスできます。 使用可能なアクションは変更できます。例えば、場所や、複数のリソースを選択しているかどうかによって異なります。

![アクションツールバー](/help/journey-headless/author/assets/headless-journey-author-navigation-06.png)

表示セレクターを使用して、リソースを表示する形式を選択できます。

![表示セレクター](/help/journey-headless/author/assets/headless-journey-author-navigation-03.png)

パネルセレクターを使用して、項目に関する追加情報を表示できます。 追加のアクションにアクセスすることもできます。

![左レール](/help/journey-headless/author/assets/headless-journey-author-navigation-04.png)

## コンテンツフラグメントのオーサリング {#authoring-content-fragments}

これはAEMユーザーインターフェイス(UI)の簡単な紹介でしたが、ぜひ試してみてください。 次に、本当の関心を引きます — ヘッドレス用のコンテンツフラグメント。

最初から最後まで調べる必要がありますが、お使いのインスタンスには既にフォルダーやフラグメントが作成されていて、それらが別の場所にある可能性があります。 原理は同じ。

### 整理とナビゲーション {#organizing-and-navigating}

コンテンツフラグメントがほとんどない場合を除き、コンテンツフラグメントを整理して、コンテンツフラグメントを（および他のユーザーが）再度見つけられるようにします。

#### フォルダーの作成 {#creating-folder}

これをおこなうには、アセットコンソールの「**ファイル**」セクションに一連のフォルダーを作成します。 **「**&#x200B;を作成」オプション（右上）を選択し、「**フォルダーを作成**」を選択します。

![「フォルダーを作成」オプション](/help/journey-headless/author/assets/headless-journey-author-folder-01.png)

詳細を入力し、**作成**&#x200B;で確認できるダイアログが開きます。

![フォルダーを作成ダイアログ](/help/journey-headless/author/assets/headless-journey-author-folder-02.png)

#### パスとタグを使用したフォルダーで使用可能なコンテンツフラグメントモデルの制限 {#tags-paths-for-models-in-folder}

この節は、少し進んでいます。 単に始めて試してみるだけでは必要ありませんが、フラグメントが多い場合は&#x200B;*非常に*&#x200B;便利です。 だから、まだ使っていなくても、知っておくのが良い。

コンテンツアーキテクトが、現在のプロジェクトに必要なすべてのコンテンツフラグメントモデルを作成し、他のプロジェクトも作成します。 作成者が作業を簡単にするために、特定のフォルダーで使用できるモデルのリストを制限できます。

フォルダーを作成したら、**Properties**&#x200B;フォルダーを開くことができます。 ここでは、フォルダーに関する情報と設定の詳細を含む様々なタブを示します。 特に、コンテンツフラグメントの場合は、「**ポリシー**」タブを使用して、このフォルダーの特定のパスやタグを定義できます。 これにより、フォルダーで使用できるコンテンツフラグメントモデルが制限されます。つまり、コンテンツフラグメントモデルをこのフォルダーでフラグメントを生成するために使用する前に、これらの要件を満たす必要があります。

![フォルダーのプロパティの作成 — ポリシー](/help/journey-headless/author/assets/headless-journey-author-folder-04.png)

>[!NOTE]
>
>詳しくは、アセットフォルダーでのコンテンツフラグメントモデルの許可を参照してください。

次に、これらのフォルダー内を移動して、コンテンツフラグメントを作成および編集します。

#### 念のため — フォルダーCloud Servicesの設定 {#cloud-services-folder}

念のため…

フォルダーを作成できる初期フォルダーが与えられる可能性があります。 これは、一部の設定の詳細（通常は開発者またはシステム管理者が）をルートフォルダーに適用する必要があるためです。 これは興味を持たないでしょうが、必要に応じて、**Properties**&#x200B;フォルダーの&#x200B;**Cloud Services**&#x200B;の&#x200B;**Configuration**&#x200B;を確認できます。

![フォルダーのプロパティの作成 — 設定](/help/journey-headless/author/assets/headless-journey-author-folder-03.png)

>[!NOTE]
>
>詳しくは、「設定をアセットフォルダーに適用」を参照してください。

### コンテンツフラグメントの作成 {#creating-fragment}

コンテンツフラグメントの作成は非常に似ています。代わりに&#x200B;**コンテンツフラグメント**&#x200B;オプションを使用します。

![「コンテンツフラグメントを作成」オプション](/help/journey-headless/author/assets/headless-journey-author-content-fragment-01.png)

今度はウィザードが開きます。 最初の手順は、フラグメントの基となるコンテンツフラグメントモデルを選択することです。

![コンテンツフラグメントを作成 — 「モデル」を選択します。](/help/journey-headless/author/assets/headless-journey-author-content-fragment-02.png)

「**次へ**」を続行すると、フラグメントの詳細を指定できます。

![コンテンツフラグメントを作成 — 名前を指定](/help/journey-headless/author/assets/headless-journey-author-content-fragment-03.png)

**「**&#x200B;を作成」で確定すると、エディターでフラグメントを&#x200B;**開く**&#x200B;ことができます。

### フラグメントの編集 {#editing-fragment}

フラグメントは、作成後すぐに開くことも、アセットコンソールから選択することもできます。

エディターが最初に開くと、次の内容が表示されます。

* 左側にあるアイコンのリスト — 様々な機能領域にアクセスできます。 エディターが「**バリエーション**」タブに開きます。このタブで、ほとんどの編集がおこなわれます。 「**注釈**」タブと「**メタデータ**」タブに興味がある場合もあります。

* フラグメントに関する情報と様々なアクションへのアクセスを含むヘッダー。

* メインの編集領域 — フラグメントの作成に使用するモデルによって異なります。

例：

* 複数の情報（一部は特定のタイプを持つ）のみを必要とするフラグメント。 ヘッドレスコンテンツの場合、参照は重要です。これについては、後で学習します。

   ![コンテンツフラグメントエディター — マイフラグメント](/help/journey-headless/author/assets/headless-journey-author-content-fragment-04.png)

* テキストの長いセクションを記述できるフラグメント。 ここでは、テキストの管理および書式設定に関する追加のオプションがあります。 全画面表示エディターで個々のテキストフィールドを開くこともできます（右側の小さな画面のようなアイコンを使用）。

   ![コンテンツフラグメントエディター — Alaska Spirts](/help/journey-headless/author/assets/headless-journey-author-content-fragment-05.png)

>[!NOTE]
>
>作成者が一部のフィールドを正常に入力する方法の詳細を知るには、プロジェクト固有のドキュメントが必要になる場合があります。
>
>一般的な詳細については、コンテンツフラグメントモデル — データタイプとプロパティを参照してください。

「**保存**」または「**保存して閉じる**」で更新内容を確認します。

>[!NOTE]
>
>詳しくは、バリエーション — コンテンツフラグメントのオーサリングを参照してください。

#### （おそらく）心配する必要がないもの {#what-you-probably-do-not-need-to-worry-about}

はい、これは少し奇妙な節に見えるかもしれませんが、コンテンツフラグメントエディターを開いて調査を開始すると、コンテンツ作成者としてヘッドレスなジャーニーに適用されない（おそらく）様々なオプションが表示されます。 つまり、ヘッドレスなコンテキストで無視できる内容について、簡単に説明します。

* **コンテンツフラグメントモデル**

   エディターの上部にある、フラグメント名のすぐ下にコンテンツフラグメントモデルの名前が表示されます。 これは、モデルエディターに移動するリンクでもあります。
コンテンツフラグメントモデルは、使用する構造を定義するので、コンテンツフラグメントにとって実際に重要です。 ただし、コンテンツアーキテクトは、他のペルソナの作成と編集を担当します（通常は）。

   >[!NOTE]
   >
   >詳しくは、 AEMヘッドレスコンテンツアーキテクトのジャーニーを参照してください。

* **関連コンテンツ**

   これはエディターのタブなので明らかです

   コンテンツフラグメントは、AEMでは多くのバージョンで利用できます。 元々は、ページのオーサリング時に「従来」の使用で利用できるようになっていました。.そして、この文脈ではまだ使用されている。 これには、フラグメントに埋め込まれていないが、ページのオーサリング時に作成者が使用できる必要があるアセット（画像など）の関連付けが含まれる場合があります。

* **プレビュー**

   これはエディターのもう1つのタブで、主に開発者向けの技術ビューを提供します。

* **ページ参照を更新**

   このアクションは&#x200B;**...から実行できます。**（省略記号）ドロップダウン。 ページのオーサリングに関連するので、ヘッドレスな作成者にとっては興味深いことではありません。

### 公開 {#publishing}

<!-- needs more details -->

フラグメントを完了したら、**公開**&#x200B;して、ヘッドレスアプリケーションで使用できるようにします。

公開アクションは、エディターで（または&#x200B;**アセット**&#x200B;コンソールのツールバーから）使用できます。

![コンテンツフラグメントエディター — マイフラグメント](/help/journey-headless/author/assets/headless-journey-author-content-fragment-06.png)

## 次の手順 {#whats-next}

基本を学んだので、次の手順は[参照](references.md)について学びます。 これにより、使用可能な様々な参照が導入され、そしてフラグメント参照を使用して構造のレベルを作成する方法について説明されます。フラグメント参照はヘッドレスオーサリングの主要な部分です。

## その他のリソース {#additional-resources}

* [オーサリングに関する概念](/help/sites-cloud/authoring/getting-started/concepts.md)

* [基本操作](/help/sites-cloud/authoring/getting-started/basic-handling.md)  — このページは主にサイトコンソールに基づいていま **** すが、多くの機能はアセットコンソール内のコンテンツフラグメントのオーサリングにも **関** 連して **** います。

   * [ナビゲーションパネル](/help/sites-cloud/authoring/getting-started/basic-handling.md#navigation-panel)

   * [ヘッダー](/help/sites-cloud/authoring/getting-started/basic-handling.md#the-header)

   * [アクションツールバー](/help/sites-cloud/authoring/getting-started/basic-handling.md#actions-toolbar)

   * [クイックアクション](/help/sites-cloud/authoring/getting-started/basic-handling.md#quick-actions)

   * [リソースの表示と選択](/help/sites-cloud/authoring/getting-started/basic-handling.md#viewing-and-selecting-resources)

   * [パネルセレクター](/help/sites-cloud/authoring/getting-started/basic-handling.md#rail-selector)

* [コンテンツフラグメントの操作](/help/assets/content-fragments/content-fragments.md)

   * [コンテンツフラグメントの管理](/help/assets/content-fragments/content-fragments-managing.md)

      * [アセットフォルダーへの設定の適用](/help/assets/content-fragments/content-fragments-configuration-browser.md#apply-the-configuration-to-your-assets-folder)

      * [コンテンツフラグメントの作成](/help/assets/content-fragments/content-fragments-managing.md#creating-a-content-fragment)
   * [バリエーション — コンテンツフラグメントのオーサリング](/help/assets/content-fragments/content-fragments-variations.md)

   * [コンテンツフラグメントモデル](/help/assets/content-fragments/content-fragments-models.md)

      * [コンテンツフラグメントモデル — データタイプ](/help/assets/content-fragments/content-fragments-models.md#data-types)

      * [コンテンツフラグメントモデル — プロパティ](/help/assets/content-fragments/content-fragments-models.md#properties)

      * [コンテンツフラグメントモデル — アセットフォルダーでコンテンツフラグメントモデルを許可する](/help/assets/content-fragments/content-fragments-models.md#allowing-content-fragment-models-assets-folder)


* 「はじめる前に」ガイド 
   * [アセットフォルダーのヘッドレス作成のクイック開始ガイド](/help/implementing/developing/headless/getting-started/create-assets-folder.md)

* AEMヘッドレスコンテンツアーキテクトジャーニー

* AEMヘッドレス翻訳ジャーニー