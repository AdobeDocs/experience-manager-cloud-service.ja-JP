---
title: 基本操作
description: AEM のナビゲーションとその基本的な使用方法を習得します
translation-type: tm+mt
source-git-commit: 16725342c1a14231025bbc1bafb4c97f0d7cfce8

---


# 基本操作 {#basic-handling}

このドキュメントは、AEMオーサー環境を使用する際の基本的な処理の概要を説明するために作成されています。 これは&#x200B;**サイト**&#x200B;コンソールを基礎として使用します。

>[!NOTE]
>
>* 一部の機能はすべてのコンソールでは使用できず、一部のコンソールにしかない機能もあります。個別のコンソールや関連する機能に関する具体的な情報については、他のページで詳しく取り上げます。
>* AEM 全体で（特に、[コンソールを使用する](/help/sites-cloud/authoring/getting-started/keyboard-shortcuts.md)場合と[ページを編集する](/help/sites-cloud/authoring/fundamentals/keyboard-shortcuts.md)場合に）、キーボードショートカットを利用できます。


## タッチ対応 UI {#a-touch-enabled-ui}

AEMのユーザーインターフェイスでタッチが有効になっています。 タッチ対応インターフェイスを使用すると、タップ、長押し、スワイプなどのタッチジェスチャを使用して、ソフトウェアを操作できます。AEM UIはタッチ対応なので、携帯電話やタブレットなどのタッチデバイスでタッチジェスチャを使用できます。 ただし、従来のデスクトップデバイスではマウス操作も可能で、コンテンツのオーサリング方法を柔軟に選択できます。

## 最初の手順 {#first-steps}

ログインするとすぐに、[ナビゲーションパネル](#navigation-panel)が表示されます。いずれかのオプションを選択すると、対応するコンソールが開きます。

![ナビゲーションパネル](/help/sites-cloud/authoring/assets/navigation.png)

AEM の基本的な使用方法を適切に理解できるように、このドキュメントでは&#x200B;**サイト**&#x200B;コンソールに基づいて説明します。「**サイト**」をクリックまたはタップして開始します。

## 製品ナビゲーション {#product-navigation}

ユーザーが最初にコンソールにアクセスするといつでも、製品ナビゲーションチュートリアルが開始されます。ここで時間を割いて、ひととおりクリックまたはタップし、AEM の基本操作の概要を把握してください。

![ナビゲーションチュートリアル](/help/sites-cloud/authoring/assets/tutorial.png)

「**次へ**」をクリックまたはタップして、概要の次のページに進みます。Click or tap **Close** or click or tap outside of the overview dialog to close.

The overview will restart the next time you access a console unless you either view all slides or check the option **Don&#39;t show this again**.

## グローバルナビゲーション {#global-navigation}

グローバルナビゲーションパネルを使用してコンソール間を移動できます。これは、画面の左上にある Adobe Experience Manager リンクをクリックまたはタップすると、フルスクリーンのドロップダウンとしてトリガーされます。

You can close the global navigation panel by clicking or tapping **Close** to return to your previous location.

![ナビゲーションパネルの上部バー](/help/sites-cloud/authoring/assets/navigation-bar.png)

グローバルナビゲーションには、2 つのパネルがあり、画面の左余白にアイコンで表示されます。

* **[ナビゲーション](#navigation-panel)**- コンパスで表される AEMにログインしたときのデフォルトのパネル
* **[ツール](#tools-panel)**- ハンマーで表される

次に、これらのパネルで使用できるオプションについて説明します。

### ナビゲーションパネル {#navigation-panel}

ナビゲーションパネル：

![ナビゲーションパネル](/help/sites-cloud/authoring/assets/navigation.png)

ナビゲーションから利用可能なコンソールは次のとおりです。

| console | 目的 |
|---|---|
| プロジェクト | プロジェクトコンソールを使用すると、プロジェクトに直接アクセスできます。 [プロジェクトは](/help/sites-cloud/authoring/projects/overview.md) 、チームの構築に使用できる仮想ダッシュボードです。 その後、そのチームにリソース、ワークフロー、タスクへのアクセス権を与えて、ユーザーが共通の目標に向かって作業できるようにします。 |
| Sites | The Sites consoles let you [create, view, and manage sites](/help/sites-cloud/authoring/fundamentals/organizing-pages.md) running on your AEM instance. このコンソールを使用して、ページの作成、編集、コピー、移動および削除、ワークフローの開始、ページの公開を行うことができます。 |
| エクスペリエンスフラグメント | An [Experience Fragment](/help/sites-cloud/authoring/fundamentals/experience-fragments.md) is a stand-alone experience that can be re-used across channels and have variations, saving the trouble of repeatedly copying and pasting experiences or parts of experiences. |
| Assets | アセットコンソールでは、画像、ビデオ、ドキュメント、オーディオファイルなどのデジタルアセットの読み込みと管理を行うことができます。 These assets can then be used by any site running on the same AEM instance.<!--add some kind of assets link--> |
| パーソナライゼーション | This console provides a framework of tools for [authoring targeted content and presenting personalized experiences.](/help/sites-cloud/authoring/personalization/overview.md) |

## ツールパネル {#tools-panel}

ツールパネルには、様々なカテゴリを含むサイドパネルがあり、同様のツールコンソールをグループ化します。 The Tools consoles provide access to a number of specialized tools and consoles that help you administer your websites, digital assets, and other aspects of your content repository. <!--The [Tools consoles](/help/sites-administering/tools-consoles.md) provide access to a number of specialized tools and consoles that help you administer your websites, digital assets, and other aspects of your content repository.-->

![ツールパネル](/help/sites-cloud/authoring/assets/tools-panel.png)

## ヘッダー {#the-header}

ヘッダーは、画面の上部に常に表示されます。ヘッダーのほとんどのオプションはシステムのどこにいても同じですが、一部はコンテキスト固有です。

![ナビゲーションヘッダー](/help/sites-cloud/authoring/assets/navigation-bar.png)

* [グローバルナビゲーション](#global-navigation)

   Select the **Adobe Experience Manager** link to navigate between consoles.

   ![グローバルナビゲーション](/help/sites-cloud/authoring/assets/global-navigation.png)

* [検索](/help/sites-cloud/authoring/getting-started/search.md)

   ![検索ボタン](/help/sites-cloud/authoring/assets/search-button.png)

   You can also use the [shortcut key](/help/sites-cloud/authoring/getting-started/keyboard-shortcuts.md) `/` (forward slash) to invoke search from any console.

* [ソリューション](https://www.adobe.com/experience-cloud.html)

   ![ソリューションボタン](/help/sites-cloud/authoring/assets/solutions.png)

* [ヘルプ](#accessing-help)

   ![ヘルプボタン](/help/sites-cloud/authoring/assets/help.png)

* [通知](/help/sites-cloud/authoring/getting-started/inbox.md)

   ![通知ボタン](/help/sites-cloud/authoring/assets/notifications.png)

   このアイコンには、現在割り当てられている未完了の通知の数を示すバッジがつきます。

* [ユーザープロパティ](/help/sites-cloud/authoring/getting-started/account-environment.md)

   ![ユーザープロパティボタン](/help/sites-cloud/authoring/assets/user-properties.png)

* [レールセレクター](#rail-selector)

   ![パネルの選択ボタン](/help/sites-cloud/authoring/assets/rail-selector.png)

   現在のコンソールに応じて表示されるオプションです。For example, in **Sites** you can select content only (the default), the timeline, references, or filter side panel.

   ![レールセレクターの例](/help/sites-cloud/authoring/assets/rail-selector-example.png)

* パンくずリスト

   ![ナビゲーションバーのパンくずリスト](/help/sites-cloud/authoring/assets/breadcrumbs-navigation.png)

   レールの中央に位置し、常に現在選択している項目の説明を表示するパンくずリストを使用すると、特定のコンソール内を移動できます。In the **Sites** console, you can navigate through the levels of your website.

   パンくずリストのテキストをクリックするだけで、現在選択している項目の階層のレベルをリストするドロップダウンが表示されます。エントリをクリックすると、その場所にジャンプします。

   ![パンくずリストの例](/help/sites-cloud/authoring/assets/breadcrumbs-example.png)

* **作成ボタン**

   ![作成ボタン](/help/sites-cloud/authoring/assets/create.png)

   クリックすると、コンソール／コンテキストに適したオプションが表示されます。

* [表示](#viewing-and-selecting-resources)

   表示アイコンは AEM ツールバーの右端にあります。このアイコンは、そのときの表示に応じて随時変化します。例えば、デフォルト表示では、次のように&#x200B;**列表示**&#x200B;が表示されます。

   ![ビューボタン](/help/sites-cloud/authoring/assets/views-button.png)

   列表示、カード表示、リスト表示を切り替えることができます。リストビューでは、ビュー設定も表示されます。

   ![表示](/help/sites-cloud/authoring/assets/view.png)

   >[!NOTE]
   >
   >「設定 **を表示** 」オプションは、リスト表示モード **でのみ使用できます** 。

## ヘルプへのアクセス {#accessing-help}

様々なヘルプリソースを使用できます。

* **コンソールツールバー**

   「**ヘルプ**」アイコンにより、現在の場所に応じた適切なリソースが開きます。

   ![ヘルプアイコン](/help/sites-cloud/authoring/assets/help-console.png)

* **ナビゲーション**

   初めてシステムを操作する際に、[AEM の操作を紹介するスライドが表示されます](#product-navigation)。

   ![チュートリアル](/help/sites-cloud/authoring/assets/tutorial.png)

* **ページエディター**

   ページを初めて編集する場合は、ページエディターについて説明する一連のスライドが表示されます。

   ![エディタのチュートリアル](/help/sites-cloud/authoring/assets/editor-tutorial.png)

   コンソールに最初にアクセスしたときの[製品ナビゲーションの概要](#product-navigation)と同様に、この概要をナビゲートします。

   このスライドをもう一度表示するには、[**ページ情報&#x200B;**メニューの「**&#x200B;ヘルプ&#x200B;**](/help/sites-cloud/authoring/fundamentals/environment-tools.md#accessing-help)」を選択します。

* **ツールコンソール**

   **ツール**&#x200B;コンソールから外部&#x200B;**リソース**&#x200B;にアクセスすることもできます。

   * **ドキュメント** - Web Experience Managementのドキュメントを表示します。
   * **開発者向けリソース** — 開発者向けリソースとダウンロード
   >[!NOTE]
   >
   >コンソールでは、ホットキー（疑問符）を使用して、いつでも使用でき `?` るショートカットキーの概要にアクセスできます。
   >
   >すべてのキーボードショートカットの概要については、次のドキュメントを参照してください。
   >
   >* [ページ編集時のキーボードショートカット](/help/sites-cloud/authoring/fundamentals/keyboard-shortcuts.md)
   >* [コンソールのキーボードショートカット](/help/sites-cloud/authoring/getting-started/keyboard-shortcuts.md)


## アクションツールバー {#actions-toolbar}

リソース（ページやアセットなど）を選択するたびに、様々なアクションがアイコンで示され、ツールバーに説明テキストが表示されます。これらのアクションは、次によって決まります。

* 現在のコンソール
* 現在のコンテキスト
* Whether you are in [selection mode](#viewing-and-selecting-resources)

ツールバーで使用できるアクションは、選択した特定の項目に対して取ることのできるアクションを反映して変化します。

How you [select a resource](#viewing-and-selecting-resources) depends on the view.

一部のウィンドウではスペースが制限されるので、使用可能なスペースよりもツールバーのほうが長くなることがよくあります。この場合は、追加のオプションが表示されます。省略記号（三点リーダーまたは「**...**」）をクリックまたはタップすると、その他のすべてのアクションを含むドロップダウンセレクターが開きます。例えば、**サイト**&#x200B;コンソールでページを選択すると、次のように表示されます。

![その他のオプション](/help/sites-cloud/authoring/assets/additional-options.png)

>[!NOTE]
>
>利用可能な個々のアイコンについては、それぞれのコンソール、機能、シナリオに関連するページで説明しています。

## クイックアクション {#quick-actions}

[カード表示](#card-view)では、特定のアクションがクイックアクションアイコンとして使用できます。クイックアクションアイコンはツールバーにも表示されます。クイックアクションのアイコンは、一度に 1 つの項目に対してのみ利用できます。このアイコンを使用すると、事前に選択する必要がありません。

クイックアクションは、リソースカードをマウスオーバー（デスクトップデバイスの場合）したときに表示されます。使用できるクイックアクションは、コンソールおよびコンテキストによって異なります。例えば、**サイト**&#x200B;コンソールのページのクイックアクションを次に示します。

![その他のオプション](/help/sites-cloud/authoring/assets/quick-actions.png)

## リソースの表示と選択 {#viewing-and-selecting-resources}

概念上、表示、ナビゲーションおよび選択はすべての表示で同じ操作ですが、使用している表示によって処理がわずかに異なります。

使用可能な任意の表示方法で、リソースを表示、ナビゲーションおよび（追加のアクションをおこなうために）選択できます。表示を選択するには、右上のアイコンを使用します。

* [列表示](#column-view)
* [カード表示](#card-view)
* [リスト表示](#list-view)

>[!NOTE]
>
>デフォルトでは、AEM Assets は、UI のどの表示でもアセットの元のレンディションをサムネールとして表示しません。管理者の場合、オーバーレイを使用して AEM Assets で元のレンディションをサムネールとして表示するように設定できます。

### リソースの選択 {#selecting-resources}

特定のリソースの選択方法は、表示とデバイスの組み合わせによって異なります。

| 表示 | タッチを選択 | デスクトップの選択 | タッチの選択を解除 | デスクトップの選択を解除 |
|---|---|---|---|---|
| 列 | サムネールをタップします | サムネールをクリック | サムネールをタップします | サムネールをクリック |
| カード | カードをタップして押し続ける | マウスを移動し、チェックマークのクイックアクションを使用します。 | カードをタップします | カードをクリックします |
| リスト | サムネールをタップします | サムネールをクリック | サムネールをタップします | サムネールをクリック |

#### すべてを選択 {#select-all}

コンソールの右上隅にある「**すべてを選択**」オプションをクリックすると、あらゆる表示のすべての項目を選択できます。

* **カード表示**&#x200B;では、すべてのカードが選択されます。
* In **List View** all items in the list are selected.
* **列表示**&#x200B;では、一番左の列にあるすべての項目が選択されます。

![すべて選択](/help/sites-cloud/authoring/assets/select-all.png)

#### すべて選択解除 {#deselecting-all}

どのような場合でも、項目を選択すると、選択された項目の数がツールバーの右上に表示されます。

すべての項目の選択を解除し、選択モードを終了するには、次の操作を行います。

* Clicking or tapping the **X** next to the count
* Escapeキー **の使** 用

![すべて選択解除](/help/sites-cloud/authoring/assets/deselect-all.png)

デスクトップデバイスを使用している場合は、すべてのビューで、キーボードのEscキーをタップして、すべての項目の選択を解除できます。

#### 選択の例 {#selecting-example}

1. 例えば、カード表示では次のようになります。

   ![カード表示の選択](/help/sites-cloud/authoring/assets/card-view-select.png)

1. リソースを選択すると、上部のヘッダーの上に[アクションツールバー](#actions-toolbar)が重なって表示され、選択したリソースで現在適用可能なアクションにアクセスできます。

   To exit selection mode select the **X** to the top-right, or use **escape**.

### 列表示 {#column-view}

![列表示](/help/sites-cloud/authoring/assets/column-view.png)

列表示を使用すると、一連のカスケード表示された列によってコンテンツツリーをビジュアルにナビゲーションできます。この表示では、Web サイトのツリー構造を目で見て確認しながら移動できます。

一番左の列のリソースを選択すると、右側の列に子リソースが表示されます。右側の列のリソースを選択すると、さらに右側の列に子リソースが表示されます。

* リソース名かリソース名の右にある山形記号をタップまたはクリックすることで、ツリーを上下に移動できます。

   * リソース名と山形記号は、タップまたはクリックするとハイライト表示されます。
   * クリック／タップしたリソースの子は、クリック／タップしたリソースの右側の列に表示されます。
   * 子を持たないリソース名をタップまたはクリックすると、その詳細が最後の列に表示されます。

* サムネールをタップまたはクリックして、リソースを選択します。

   * 選択すると、サムネールにチェックマークが重ねて表示され、リソース名もハイライト表示されます。
   * 選択されたリソースの詳細が最後の列に表示されます。
   * アクションツールバーが使用可能になります。
   列表示でページが選択されると、選択したページが次の詳細と共に最後の列に表示されます。

   * ページタイトル
   * ページ名（ページの URL の一部）
   * ページがベースにするテンプレート
   * 変更の詳細
   * ページの言語
   * 公開の詳細


### カード表示 {#card-view}

![カード表示](/help/sites-cloud/authoring/assets/card-view.png)

* カード表示では、現在のレベルの各項目の情報カードを表示します。次のような情報が提供されます。

   * ページコンテンツの視覚的表現
   * ページタイトル
   * 重要な日付（最終編集日、最終発行日など）
   * ページがロック、非表示またはライブコピーの一部である場合
   * 必要に応じて、ワークフローの一部としてアクションを実行する必要がある場合
      * 必要なアクションを示すマーカーは、[インボックス](/help/sites-cloud/authoring/getting-started/inbox.md)のエントリに関連している場合があります。

* また、この表示では、選択などの[クイックアクション](#quick-actions)や編集などの共通アクションも使用できます。

   ![クイックアクション](/help/sites-cloud/authoring/assets/quick-actions.png)

* カードを（クイックアクションを回避するために慎重に）タップまたはクリックしてツリーの下に移動したり、[ヘッダーのパンくずリスト](#the-header)を使用して再び上に移動したりできます。

### リスト表示 {#list-view}

![リスト表示](/help/sites-cloud/authoring/assets/list-view.png)

* リスト表示では、現在のレベルの各リソースの情報が表示されます。
* リソース名をタップまたはクリックしてツリーの下に移動したり、[ヘッダーのパンくずリスト](#the-header)を使用して上に戻ったりできます。
* リストですべての項目を簡単に選択するには、リストの左上にあるチェックボックスを使用します。

   ![リストビューですべて選択](/help/sites-cloud/authoring/assets/list-view-select-all.png)

   * リストのすべての項目が選択されると、このチェックボックスがオンになります。

      * すべてを選択解除するには、チェックボックスをクリックまたはタップします。
   * 一部の項目のみが選択された場合、マイナス記号が表示されます。

      * すべてを選択するには、チェックボックスをクリックまたはタップします。
      * すべてを選択解除するには、再度チェックボックスをクリックまたはタップします。


* 表示ボタンの下にある「**設定を表示**」オプションを使用して、表示する列を選択します。次の列を表示できます。

   * **名前** - ページ名。ページの URL の一部で、言語にかかわらず変更されないので、多言語オーサリング環境で便利です
   * **変更** - 最終変更日および最終変更者
   * **公開** - 公開ステータス
   * **テンプレート** - ページがベースにしているテンプレート
   * **ワークフロー** - 現在ページに適用されているワークフローマウスオーバーしたりタイムラインを開いたりすると、詳細情報が表示されます。
   * **ページ分析**
   * **個別訪問者数**
   * **ページ滞在時間**

      ![列の選択](/help/sites-cloud/authoring/assets/select-columns.png)
   By default the **Name** column is shown, which makes up part of the URL for the page. 場合によっては、異なる言語のページにアクセスし、ページの名前を確認する必要があります（通常は変更されません）。作成者がページの言語を知らない場合は、非常に役立ちます。

* リストの各項目の右端にある縦の点線マークを使用して項目の順序を変更します。

   >[!NOTE]
   >
   >Changing the order works only within an ordered folder that has `jcr:primaryType` value as `sling:OrderedFolder`.

   ![列の順序](/help/sites-cloud/authoring/assets/column-order.png)

   縦の選択バーをクリックまたはタップして、項目をリストの新しい位置にドラッグします。

   ![注文リスト](/help/sites-cloud/authoring/assets/order-list.png)

## レールセレクター {#rail-selector}

The **Rail Selector** is available at the top-left of the window and displays options depending on your current consoles.

![パネルセレクターを展開](/help/sites-cloud/authoring/assets/rail-selector-expanded.png)

For example, in **Sites** you can select content only (the default), content tree, the timeline, references, or filter side panel.

コンテンツのみが選択されている場合は、レールアイコンのみが表示されます。他のオプションが選択されている場合は、レールアイコンの隣にオプション名が表示されます。

>[!NOTE]
>
>[キーボードショートカット](/help/sites-cloud/authoring/getting-started/keyboard-shortcuts.md)を使用してレール表示オプションをすばやく切り替えることができます。

### コンテンツツリー {#content-tree}

コンテンツツリーを使用して、サイドパネル内でサイト階層をすばやく移動したり、現在のフォルダーのページに関する多くの情報を表示したりできます。

コンテンツツリーサイドパネルをリスト表示またはカード表示と共に使用すると、ユーザーはプロジェクトの階層構造を簡単に確認したり、コンテンツツリーサイドパネルを使用して、コンテンツ構造を簡単に移動したり、リスト表示で詳細なページ情報を表示したりできます。

![コンテンツツリー](/help/sites-cloud/authoring/assets/content-tree.png)

>[!NOTE]
>
>階層表示でエントリを選択すると、矢印キーを使用して階層をすばやく移動できます。
>
>詳しくは、[キーボードショートカット](/help/sites-cloud/authoring/getting-started/keyboard-shortcuts.md)を参照してください。

### タイムライン {#timeline}

タイムラインは、選択したリソースで発生したイベントを表示または開始するために使用できます。 「タイムライン」列を開くには、レールセレクターを使用します。

![タイムラインツリー](/help/sites-cloud/authoring/assets/timeline.png)

「タイムライン」列では、次の操作を実行できます。

* 選択した項目に関連する様々なイベントを表示します。

   * ドロップダウンリストからイベントタイプを選択できます。

      * コメント
      * [注釈](/help/sites-cloud/authoring/fundamentals/annotations.md)
      * [アクティビティ](/help/sites-cloud/authoring/personalization/activities.md)
      * [ローンチ](/help/sites-cloud/authoring/launches/overview.md)
      * [バージョン](/help/sites-cloud/authoring/features/page-versions.md)
      * [ワークフロー](/help/sites-cloud/authoring/workflows/overview.md)
         * With the exception of transient workflows as no history information is saved for these <!--With the exception of [transient workflows](/help/sites-developing/workflows.md#transient-workflows) as no history information is saved for these-->
      * すべて表示

* 選択した項目に関するコメントを追加または表示します。イベントのリストの下部に「**コメント**」ボックスが表示されます。コメントを入力して Return キーを押すと、コメントが登録されます。コメントは「**コメント**」または「**すべて表示**」を選択すると表示されます。

* 特定のコンソールには追加機能が用意されています。例えば、サイトコンソールでは次のアクションを実行できます。

   * [バージョンの保存](/help/sites-cloud/authoring/features/page-versions.md)
   * [ワークフローを開始](/help/sites-cloud/authoring/workflows/applying.md)

These options accessible via the chevron next to the **Comment** field.

![コメントフィールド](/help/sites-cloud/authoring/assets/comments.png)

### 参照 {#references}

**参照**&#x200B;には、選択したリソースへの関係が表示されます。例えば、**サイト**&#x200B;コンソールでは、ページの[参照](/help/sites-cloud/authoring/fundamentals/environment-tools.md#references)には次が表示されます。

* [ローンチ](/help/sites-cloud/authoring/launches/overview.md#launches-in-references-sites-console)
* ライブコピー<!--[Live copies](/help/sites-administering/msm-livecopy-overview.md#openingthelivecopyoverviewfromreferences)-->
* 言語コピー<!--[Language copies](/help/sites-administering/tc-prep.md#seeing-the-status-of-language-roots)-->
* コンテンツ参照：

   * 他のページから選択したページへのリンク
   * 参照コンポーネントによって選択したページから借用または貸与されたコンテンツ

![リファレンスの例](/help/sites-cloud/authoring/assets/references-example.png)

### フィルター {#filter}

これを使用すると、適切な場所フィルターが既に設定された状態で[検索](/help/sites-cloud/authoring/getting-started/search.md)と同じようにパネルが開き、表示したいコンテンツをさらにフィルタリングできます。

![フィルターの例](/help/sites-cloud/authoring/assets/filter.png)
