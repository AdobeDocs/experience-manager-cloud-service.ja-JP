---
title: 基本操作
description: AEM のナビゲーションとその基本的な使用方法を習得します
translation-type: tm+mt
source-git-commit: 996a1b49889816d3b887d8d568ec56b72bd99074
workflow-type: tm+mt
source-wordcount: '2864'
ht-degree: 100%

---


# 基本操作 {#basic-handling}

このドキュメントでは、AEM オーサー環境を使用する際の基本操作の概要をまとめています。これは&#x200B;**サイト**&#x200B;コンソールを基礎として使用します。

>[!NOTE]
>
>* 一部の機能はすべてのコンソールでは使用できず、一部のコンソールにしかない機能もあります。個別のコンソールや関連する機能に関する具体的な情報については、他のページで詳しく取り上げます。
>* AEM 全体で（特に、[コンソールを使用する](/help/sites-cloud/authoring/getting-started/keyboard-shortcuts.md)場合と[ページを編集する](/help/sites-cloud/authoring/fundamentals/keyboard-shortcuts.md)場合に）、キーボードショートカットを利用できます。


## タッチ対応 UI {#a-touch-enabled-ui}

AEM のユーザーインターフェイスは、タッチ操作に対応しています。タッチ対応インターフェイスを使用すると、タップ、長押し、スワイプなどのタッチジェスチャーを使用して、ソフトウェアを操作できます。AEM UI はタッチ対応なので、携帯電話やタブレットなどのタッチデバイスでタッチジェスチャーを使用できます。ただし、従来のデスクトップデバイスでのマウス操作も可能で、その場合はコンテンツのオーサリング方法を柔軟に選択できます。

## 最初の手順 {#first-steps}

ログインするとすぐに、[ナビゲーションパネル](#navigation-panel)が表示されます。いずれかのオプションを選択すると、対応するコンソールが開きます。

![ナビゲーションパネル](/help/sites-cloud/authoring/assets/navigation.png)

AEM の基本的な使用方法を適切に理解できるように、このドキュメントでは&#x200B;**サイト**&#x200B;コンソールに基づいて説明します。「**サイト**」をクリックまたはタップして開始します。

## 製品ナビゲーション {#product-navigation}

ユーザーが最初にコンソールにアクセスするといつでも、製品ナビゲーションチュートリアルが開始されます。ここで時間を割いて、ひととおりクリックまたはタップし、AEM の基本操作の概要を把握してください。

![ナビゲーションチュートリアル](/help/sites-cloud/authoring/assets/tutorial.png)

「**次へ**」をクリックまたはタップして、概要の次のページに進みます。「**閉じる**」をクリックまたはタップするか、概要ダイアログの外側をクリックまたはタップして閉じます。

すべてのスライドを表示するか「**次回から表示しない**」オプションをオンにする場合を除き、概要は、次回コンソールにアクセスすると再び開始します。

## グローバルナビゲーション {#global-navigation}

グローバルナビゲーションパネルを使用してコンソール間を移動できます。これは、画面の左上にある Adobe Experience Manager リンクをクリックまたはタップすると、全画面表示のドロップダウンとしてトリガーされます。

「**閉じる**」をクリックまたはタップすると、グローバルナビゲーションパネルが閉じて、前の場所に戻ることができます。

![ナビゲーションパネルの上部バー](/help/sites-cloud/authoring/assets/navigation-bar.png)

グローバルナビゲーションには、2 つのパネルがあり、画面の左余白にアイコンで表示されます。

* **[ナビゲーション](#navigation-panel)** - コンパスと、AEM にログインしたときのデフォルトパネルで表される
* **[ツール](#tools-panel)** - ハンマーで表される

次に、これらのパネルで使用できるオプションについて説明します。

### ナビゲーションパネル {#navigation-panel}

ナビゲーションパネル：

![ナビゲーションパネル](/help/sites-cloud/authoring/assets/navigation.png)

コンソールやコンテンツ間を移動すると、現在の場所を反映するようにブラウザータブのタイトルが更新されます。

ナビゲーションでは、次のコンソールを使用できます。

| コンソール | 目的 |
|---|---|
| プロジェクト | プロジェクトコンソールでは、プロジェクトに直接アクセスできます。[プロジェクトは、チームの構築に使用できる仮想ダッシュボード](/help/sites-cloud/authoring/projects/overview.md)です。その後、そのチームがリソース、ワークフローおよびタスクにアクセスできるようになるので、チームメンバーが共通の目標に向かって作業できます。 |
| サイト | サイトコンソールでは、AEM インスタンス上で実行される[サイトの作成、表示、管理](/help/sites-cloud/authoring/fundamentals/organizing-pages.md)をおこなえます。このコンソールを通じて、ページの作成、編集、コピー、移動および削除や、ワークフローの開始、ページの公開をおこなうことができます。 |
| エクスペリエンスフラグメント | [エクスペリエンスフラグメント](/help/sites-cloud/authoring/fundamentals/experience-fragments.md)は、チャネル間で再利用でき、バリエーションのあるスタンドアロンエクスペリエンスです。エクスペリエンスやエクスペリエンスの一部を繰り返しコピー＆ペーストする手間を省きます。 |
| Assets | Assets コンソールでは、画像、ビデオ、ドキュメント、オーディオファイルなどのデジタルアセットを読み込んで、それらのデジタルアセットを管理できます。同じ AEM インスタンス上で実行されているどのサイトでも、これらのアセットを使用できます。<!--add some kind of assets link--> |
| パーソナライズ機能 | このコンソールには、[ターゲットとなるコンテンツをオーサリングして、パーソナライズされたエクスペリエンスを提供](/help/sites-cloud/authoring/personalization/overview.md)するためのツールのフレームワークが用意されています。 |

## ツールパネル {#tools-panel}

ツールパネルには、同様のツールコンソールをグループ化した様々なカテゴリを含むサイドパネルがあります。ツールコンソールを使用して、Web サイト、デジタルアセット、およびコンテンツリポジトリのその他の要素の管理に役立つ、数多くの専用ツールおよびコンソールにアクセスできます。<!--The [Tools consoles](/help/sites-administering/tools-consoles.md) provide access to a number of specialized tools and consoles that help you administer your websites, digital assets, and other aspects of your content repository.-->

![ツールパネル](/help/sites-cloud/authoring/assets/tools-panel.png)

## ヘッダー {#the-header}

ヘッダーは、画面の上部に常に表示されます。ヘッダーのほとんどのオプションはシステムのどこにいても同じですが、一部はコンテキスト固有です。

![ナビゲーションヘッダー](/help/sites-cloud/authoring/assets/navigation-bar.png)

* [グローバルナビゲーション](#global-navigation)

   コンソール間を移動するには、**Adobe Experience Manager** リンクを選択します。

   ![グローバルナビゲーション](/help/sites-cloud/authoring/assets/global-navigation.png)

* [検索](/help/sites-cloud/authoring/getting-started/search.md)

   ![検索ボタン](/help/sites-cloud/authoring/assets/search-button.png)

   [ショートカットキー](/help/sites-cloud/authoring/getting-started/keyboard-shortcuts.md) `/`（スラッシュ）を使用して、任意のコンソールから検索を呼び出すこともできます。

* [ソリューション](https://www.adobe.com/jp/experience-cloud.html)

   ![ソリューションボタン](/help/sites-cloud/authoring/assets/solutions.png)

* [ヘルプ](#accessing-help)

   ![ヘルプボタン](/help/sites-cloud/authoring/assets/help.png)

* [通知](/help/sites-cloud/authoring/getting-started/inbox.md)

   ![通知ボタン](/help/sites-cloud/authoring/assets/notifications.png)

   このアイコンには、現在割り当てられている未完了の通知の数を示すバッジがつきます。

* [ユーザープロパティ](/help/sites-cloud/authoring/getting-started/account-environment.md)

   ![ユーザープロパティボタン](/help/sites-cloud/authoring/assets/user-properties.png)

* [パネルセレクター](#rail-selector)

   ![パネルセレクターボタン](/help/sites-cloud/authoring/assets/rail-selector.png)

   現在のコンソールに応じて表示されるオプションです。例えば、**サイト**&#x200B;では、コンテンツのみ（デフォルト）、タイムライン、参照またはフィルターのサイドパネルを選択できます。

   ![パネルセレクターの例](/help/sites-cloud/authoring/assets/rail-selector-example.png)

* パンくずリスト

   ![ナビゲーションバーのパンくずリスト](/help/sites-cloud/authoring/assets/breadcrumbs-navigation.png)

   パネルの中央に位置し、常に現在選択している項目の説明を表示するパンくずリストを使用すると、特定のコンソール内を移動できます。**サイト**&#x200B;コンソールでは、Web サイトのレベル間を移動できます。

   パンくずリストのテキストをクリックするだけで、現在選択している項目の階層のレベルをリストするドロップダウンが表示されます。エントリをクリックすると、その場所にジャンプします。

   ![展開したパンくずリストの例](/help/sites-cloud/authoring/assets/breadcrumbs-example.png)

* 「**作成**」ボタン

   ![「作成」ボタン](/help/sites-cloud/authoring/assets/create.png)

   クリックすると、コンソール／コンテキストに適したオプションが表示されます。

* [表示](#viewing-and-selecting-resources)

   表示アイコンは AEM ツールバーの右端にあります。このアイコンは、そのときの表示に応じて随時変化します。例えば、デフォルト表示では、次のように&#x200B;**列表示**&#x200B;が表示されます。

   ![表示ボタン](/help/sites-cloud/authoring/assets/views-button.png)

   列表示、カード表示、リスト表示を切り替えることができます。リスト表示では、表示設定も表示されます。

   ![表示](/help/sites-cloud/authoring/assets/view.png)

   >[!NOTE]
   >
   >「**表示設定**」オプションは、**リスト表示**&#x200B;モードでのみ使用できます。

* キーボードナビゲーション

   キーボードだけを使用して Web サイト内を移動できます。この場合、**Tab** キー（または **Opt+Tab**）の標準的なブラウザ機能を使用して、ページ上のフォーカス可能な要素間を移動します。

   **Sites** コンソールには、「**メインコンテンツにスキップ**」するためのオプションが追加されています。これは、ヘッダーオプション間をタブで移動すると表示され、（製品）ツールバーの標準要素をスキップしてメインコンテンツに直接移動できるので、ナビゲーションが迅速化されます。

   ![メインコンテンツにスキップ](/help/sites-cloud/authoring/assets/skip-to-main-content.png)

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

   ![エディターのチュートリアル](/help/sites-cloud/authoring/assets/editor-tutorial.png)

   コンソールに最初にアクセスしたときの[製品ナビゲーションの概要](#product-navigation)と同様に、この概要をナビゲートします。

   このスライドをもう一度表示するには、[**ページ情報**&#x200B;メニューの「**ヘルプ**](/help/sites-cloud/authoring/fundamentals/environment-tools.md#accessing-help)」を選択します。

* **ツールコンソール**

   **ツール**&#x200B;コンソールから外部&#x200B;**リソース**&#x200B;にアクセスすることもできます。

   * **文書** - Web Experience Management のドキュメントを表示します。
   * **開発者向けリソース** - 開発者向けリソースおよびダウンロードです。

   >[!NOTE]
   >
   >コンソールでは、ホットキー `?`（疑問符）を使用して、いつでもショートカットキーの概要を確認できます。
   >
   >すべてのキーボードショートカットの概要については、次のドキュメントを参照してください。
   >
   >* [ページ編集時のキーボードショートカット](/help/sites-cloud/authoring/fundamentals/keyboard-shortcuts.md)
   >* [コンソールのキーボードショートカット](/help/sites-cloud/authoring/getting-started/keyboard-shortcuts.md)


## アクションツールバー {#actions-toolbar}

リソース（ページやアセットなど）を選択するたびに、様々なアクションがアイコンで示され、ツールバーに説明テキストが表示されます。これらのアクションは、次によって決まります。

* 現在のコンソール
* 現在のコンテキスト
* [選択モード](#viewing-and-selecting-resources)になっているかどうか

ツールバーで使用できるアクションは、選択した特定の項目に対して取ることのできるアクションを反映して変化します。

[リソースを選択する](#viewing-and-selecting-resources)方法は、表示によって異なります。

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

| 表示 | タッチの選択 | デスクトップの選択 | タッチの選択解除 | デスクトップの選択解除 |
|---|---|---|---|---|
| 列 | サムネールをタップ | サムネールをクリック | サムネールをタップ | サムネールをクリック |
| カード | カードをタップ＆ホールド | 項目の上にマウスを移動しチェックマークのクイックアクションを使用 | カードをタップ | カードをクリック |
| リスト | サムネールをタップ | サムネールをクリック | サムネールをタップ | サムネールをクリック |

#### すべてを選択 {#select-all}

コンソールの右上隅にある「**すべてを選択**」オプションをクリックすると、あらゆる表示のすべての項目を選択できます。

* **カード表示**&#x200B;では、すべてのカードが選択されます。
* **リスト表示**&#x200B;では、リスト内のすべての項目が選択されます。
* **列表示**&#x200B;では、一番左の列にあるすべての項目が選択されます。

![すべてを選択](/help/sites-cloud/authoring/assets/select-all.png)

#### すべて選択解除 {#deselecting-all}

どのような場合でも、項目を選択すると、選択された項目の数がツールバーの右上に表示されます。

すべての項目の選択を解除して選択モードを終了するには、次の操作をおこないます。

* カウントの横にある「**X**」をクリックまたはタップする
* **Esc** キーを使用する

![すべてを選択解除](/help/sites-cloud/authoring/assets/deselect-all.png)

デスクトップデバイスを使用している場合、すべての表示で、キーボードの Esc キーを押すことですべての項目を選択解除できます。

#### 選択の例 {#selecting-example}

1. 例えば、カード表示では次のようになります。

   ![カード表示の選択](/help/sites-cloud/authoring/assets/card-view-select.png)

1. リソースを選択すると、上部のヘッダーの上に[アクションツールバー](#actions-toolbar)が重なって表示され、選択したリソースで現在適用可能なアクションにアクセスできます。

   選択モードを終了するには、右上の「**X**」を選択するか、**Esc** キーを使用します。

### 列表示 {#column-view}

![列表示](/help/sites-cloud/authoring/assets/column-view.png)

列表示を使用すると、一連のカスケード表示された列によってコンテンツツリーをビジュアルにナビゲーションできます。この表示では、Web サイトのツリー構造を目で見て確認しながら移動できます。

一番左の列のリソースを選択すると、右側の列に子リソースが表示されます。右側の列のリソースを選択すると、さらに右側の列に子リソースが表示されます。

* リソース名かリソース名の右にある山形記号をタップまたはクリックすることで、ツリーを上下に移動できます。

   * リソース名と山形記号は、タップまたはクリックするとハイライト表示されます。
   * クリック／タップしたリソースの子は、クリック／タップしたリソースの右側の列に表示されます。
   * 子を持たないリソース名をタップまたはクリックすると、その詳細が最後の列に表示されます。

* サムネールをタップまたはクリックして、リソースを選択します。

   * 選択すると、チェックマークがサムネールにオーバーレイ表示され、リソース名もハイライト表示されます。
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

   * ページの内容を視覚的に表現したもの
   * ページのタイトル
   * 重要な日付（最終編集日、最終公開日など）。
   * ページがロックされているかどうか、非表示になっているかどうか、またはライブコピーの一部であるかどうか
   * 適切な場合、ワークフローの一部としてアクションを実行する必要があるタイミング。
      * 必要なアクションを示すマーカーは、[インボックス](/help/sites-cloud/authoring/getting-started/inbox.md)のエントリに関連している場合があります。

* また、この表示では、選択などの[クイックアクション](#quick-actions)や編集などの共通アクションも使用できます。

   ![クイックアクション](/help/sites-cloud/authoring/assets/quick-actions.png)

* カードを（クイックアクションを回避するために慎重に）タップまたはクリックしてツリーの下に移動したり、[ヘッダーのパンくずリスト](#the-header)を使用して再び上に移動したりできます。

### リスト表示 {#list-view}

![リスト表示](/help/sites-cloud/authoring/assets/list-view.png)

* リスト表示では、現在のレベルの各リソースの情報が表示されます。
* リソース名をタップまたはクリックしてツリーの下に移動したり、[ヘッダーのパンくずリスト](#the-header)を使用して上に戻ったりできます。
* リストですべての項目を簡単に選択するには、リストの左上にあるチェックボックスを使用します。

   ![リスト表示：すべてを選択](/help/sites-cloud/authoring/assets/list-view-select-all.png)

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
   デフォルトでは、ページの URL の一部を構成する「**名前**」列が表示されます。場合によっては、作成者は、異なる言語のページにアクセスする必要があることがあり、ページの名前（通常は変更なし）を確認することは、作成者がページの言語を知らない場合に非常に役立ちます。

* リストの各項目の右端にある縦の点線マークを使用して項目の順序を変更します。

   >[!NOTE]
   >
   >順序を変更できるのは、`jcr:primaryType` 値が `sling:OrderedFolder` である順序付きフォルダーの内部のみです。

   ![列の順序](/help/sites-cloud/authoring/assets/column-order.png)

   縦の選択バーをクリックまたはタップして、項目をリストの新しい位置にドラッグします。

   ![リストの順序変更](/help/sites-cloud/authoring/assets/order-list.png)

## パネルセレクター {#rail-selector}

**パネルセレクター**&#x200B;は、ウィンドウの左上にあり、現在のコンソールに応じてオプションを表示します。

![展開されたパネルセレクター](/help/sites-cloud/authoring/assets/rail-selector-expanded.png)

例えば、**サイト**&#x200B;では、コンテンツのみ（デフォルト）、コンテンツツリー、タイムライン、参照またはフィルターのサイドパネルを選択できます。

コンテンツのみが選択されている場合は、パネルアイコンのみが表示されます。他のオプションが選択されている場合は、パネルアイコンの隣にオプション名が表示されます。

>[!NOTE]
>
>[キーボードショートカット](/help/sites-cloud/authoring/getting-started/keyboard-shortcuts.md)を使用してパネル表示オプションをすばやく切り替えることができます。

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

タイムラインを使用して、選択したリソースで発生したイベントを表示または開始することができます。「タイムライン」列を開くには、パネルセレクターを使用します。

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
         * 履歴情報が保存されないので、一時的なワークフローは除きます <!--With the exception of [transient workflows](/help/sites-developing/workflows.md#transient-workflows) as no history information is saved for these-->
      * すべて表示

* 選択した項目に関するコメントを追加または表示します。イベントのリストの下部に「**コメント**」ボックスが表示されます。コメントを入力して Enter キーを押すと、コメントが登録されます。コメントは「**コメント**」または「**すべて表示**」を選択すると表示されます。

* 特定のコンソールには追加機能が用意されています。例えば、サイトコンソールでは次のアクションを実行できます。

   * [バージョンの保存](/help/sites-cloud/authoring/features/page-versions.md)
   * [ワークフローを開始](/help/sites-cloud/authoring/workflows/applying.md)

これらのオプションには、「**コメント**」フィールドの横にある山形記号からアクセスできます。

![コメントフィールド](/help/sites-cloud/authoring/assets/comments.png)

### 参照 {#references}

**参照**&#x200B;には、選択したリソースへの関係が表示されます。例えば、**サイト**&#x200B;コンソールでは、ページの[参照](/help/sites-cloud/authoring/fundamentals/environment-tools.md#references)には次が表示されます。

* [ローンチ](/help/sites-cloud/authoring/launches/overview.md#launches-in-references-sites-console)
* ライブコピー<!--[Live copies](/help/sites-administering/msm-livecopy-overview.md#openingthelivecopyoverviewfromreferences)-->
* 言語コピー<!--[Language copies](/help/sites-administering/tc-prep.md#seeing-the-status-of-language-roots)-->
* コンテンツ参照：

   * 他のページから選択ページへのリンク
   * 参照コンポーネントで選択したページから借りたコンテンツや、選択したページに貸したコンテンツ

![参照の例](/help/sites-cloud/authoring/assets/references-example.png)

### フィルター {#filter}

これを使用すると、適切な場所フィルターが既に設定された状態で[検索](/help/sites-cloud/authoring/getting-started/search.md)と同じようにパネルが開き、表示したいコンテンツをさらにフィルタリングできます。

![フィルターの例](/help/sites-cloud/authoring/assets/filter.png)
