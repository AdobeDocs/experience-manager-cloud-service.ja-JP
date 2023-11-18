---
title: オーサリング環境とツール
description: AEM のオーサリング環境は、コンテンツを編成および編集するための様々なメカニズムを提供しています
exl-id: cc3bd4cf-93bd-429d-9a2a-4a02a7b42f7c
source-git-commit: 6bb7b2d056d501d83cf227adb239f7f40f87d0ce
workflow-type: tm+mt
source-wordcount: '2161'
ht-degree: 87%

---


# オーサリング環境とツール {#authoring-the-environment-and-tools}

AEM のオーサリング環境は、コンテンツを編成および編集するための様々なメカニズムを提供しています. 提供されるツールには、様々なコンソールおよびページエディターからアクセスします。

{{edge-delivery-authoring}}

## サイトの管理 {#managing-your-site}

The **Sites** コンソールを使用すると、ヘッダーバー、ツールバー、アクションアイコン（選択したリソースに適用）、パンくずリストおよび選択時にセカンダリレール（タイムラインや参照など）を使用して、Web サイトの移動と管理をおこなえます。

例えば、列表示では次のようになります。

![列表示](/help/sites-cloud/authoring/assets/column-view.png)

## ページのコンテンツの編集 {#editing-page-content}

ページの編集は、ページエディターで行えます。次に例を示します。

`http://<host>:<port>/editor.html/content/wknd/en/sports/la-skateparks.html`

![ページエディター](/help/sites-cloud/authoring/assets/page-editor.png)

>[!NOTE]
>
>編集対象のページを初めて開くと、機能を紹介する一連のスライドが表示されます。
>
>必要がない場合は、このツアーをスキップすることができます。このツアーは、**ページ情報**&#x200B;メニューからいつでも表示できます。

## ヘルプへのアクセス {#accessing-help}

ページの編集中、**ヘルプ**&#x200B;には次の場所からアクセスできます。

* [**ページ情報**](/help/sites-cloud/authoring/fundamentals/page-properties.md#page-properties)&#x200B;セレクター。（エディターに初めてアクセスしたときに表示される）紹介用のスライドが表示されます。
* 特定のコンポーネントの[設定](/help/sites-cloud/authoring/fundamentals/editing-content.md#component-toolbar)ダイアログ（ダイアログツールバーの「？」アイコンを使用）。コンテキスト依存のヘルプが表示されます。

それ以外の[ヘルプ関連リソースは、コンソールから表示できます](/help/sites-cloud/authoring/getting-started/basic-handling.md#accessing-help)。

## コンポーネントブラウザー {#components-browser}

コンポーネントは AEM コンテンツの構成要素です。AEM でコンテンツページを作成するには、ページ上に複数のコンポーネントを配置し、そのオプションを設定します。

コンポーネントブラウザーには、現在のページで使用可能なすべてのコンポーネントが表示されます。これらのコンポーネントを適切な場所にドラッグして編集することで、コンテンツを追加できます。

コンポーネントブラウザーはサイドパネル内のタブです（[アセットブラウザー](#assets-browser)と[コンテンツツリー](#content-tree)も同じ場所にあります）。サイドパネルを開く（または閉じる）には、ツールバーの左上にある次のアイコンを使用します。

![サイドパネルの切り替え](/help/sites-cloud/authoring/assets/side-panel-toggle.png)

サイドパネルを開く際、パネルは（左側から）スライドして開きます。必要に応じて「**コンポーネント**」タブを選択します。開いたら、ページで使用可能なすべてのコンポーネントを参照できます。

実際の外観や処理は、使用しているデバイスの種類によって異なります。

* **モバイルデバイス（例：iPad）**

  コンポーネントブラウザーには、編集中のページ全体が表示されます。

  ページにコンポーネントを追加する場合は、必要なコンポーネントをタッチ＆ホールドして右側に移動します。コンポーネントブラウザーが閉じてページが再度表示されます。このページにコンポーネントを配置できます。

  ![モバイル版のコンポーネントブラウザー](/help/sites-cloud/authoring/assets/component-browser-mobile.png)

* **デスクトップデバイス**

  ウィンドウの左側にコンポーネントブラウザーが開きます。

  ページにコンポーネントを追加するには、必要なコンポーネントをクリックし、必要な場所までドラッグします。

  ![デスクトップデバイス上のコンポーネントブラウザー](/help/sites-cloud/authoring/assets/component-browser-desktop.png)

  コンポーネントは次のもので表されます。

   * コンポーネント名
   * コンポーネントグループ（グレー）
   * アイコンまたは略語
      * 標準コンポーネントのアイコンはモノクロです。
      * 略語は常にコンポーネント名の最初の 2 文字です。

  **コンポーネント**&#x200B;ブラウザーの上部のツールバーでは、次の操作を実行できます。

   * コンポーネントを名前でフィルターします。
   * ドロップダウンから選択して特定のグループのみを表示します。

  コンポーネントについて詳しくは、 **コンポーネント** ブラウザー（使用可能な場合） 例えば、**コンテンツフラグメント**&#x200B;の場合は、次のようになります。

  ![コンポーネントブラウザーに表示される情報](/help/sites-cloud/authoring/assets/component-browser-information.png)

  使用可能なコンポーネントについて詳しくは、[コンポーネントコンソール](/help/sites-cloud/authoring/features/components-console.md)を参照してください。

>[!NOTE]
>
>モバイルデバイスは、幅が 1,024 px 未満の場合に検出されます。このことは、デスクトップの小さいウィンドウの場合にも当てはまります。

## アセットブラウザー {#assets-browser}

アセットブラウザーには、現在のページ上で直接使用できるすべての[アセット](/help/assets/home.md)が表示されます。

アセットブラウザーはサイドパネル内のタブであり、[コンポーネントブラウザー](#components-browser)と[コンテンツツリー](#content-tree)も同じ場所にあります。サイドパネルを開く（または閉じる）には、ツールバーの左上にある次のアイコンを使用します。

![サイドパネルの切り替え](/help/sites-cloud/authoring/assets/side-panel-toggle.png)

サイドパネルを開く際、パネルは（左側から）スライドして開きます。必要に応じて「**アセット**」タブを選択します。

![アセットブラウザーボタン](/help/sites-cloud/authoring/assets/assets-browser-button.png)

アセットブラウザーが開くと、ページで使用可能なすべてのアセットを参照できます。必要に応じて、無限スクロールを使用してリストを展開できます。

![アセットブラウザー](/help/sites-cloud/authoring/assets/assets-browser.png)

ページにアセットを追加するには、アセットを選択して必要な場所までドラッグします。次のことが考えられます。

* 適切なタイプの既存のコンポーネント。
   * 例えば、画像タイプのアセットを画像コンポーネントにドラッグできます。
* A [プレースホルダー](/help/sites-cloud/authoring/fundamentals/editing-content.md#component-placeholder) を使用して、適切なタイプのコンポーネントを作成します。
   * 例えば、画像タイプのアセットを段落システムにドラッグして画像コンポーネントを作成できます。

>[!NOTE]
>
>特定のタイプのアセットとコンポーネントで使用できます。詳しくは、[アセットブラウザーを使用したコンポーネントの挿入](/help/sites-cloud/authoring/fundamentals/editing-content.md#inserting-a-component-using-the-assets-browser)を参照してください。

アセットブラウザーの上部のツールバーでは、アセットを次の項目でフィルタリングできます。

* 名前
* パス
* アセットタイプ（画像、ビデオ、ドキュメント、段落、コンテンツフラグメント、エクスペリエンスフラグメントなど）
* アセットの特性（向きやスタイルなど）
   * 特定のアセットタイプに対してのみ使用可能

実際の外観や処理は、使用しているデバイスの種類によって異なります。

* **モバイルデバイス**

  アセットブラウザーには、編集中のページ全体が表示されます。

  ページにアセットを追加するには、必要なアセットをタッチ＆ホールドし、右側に移動します。アセットブラウザーが閉じて、ページが再度表示されます。このページで、必要なコンポーネントにアセットを追加できます。

  ![モバイル版のアセットブラウザー](/help/sites-cloud/authoring/assets/assets-browser-mobile.png)

* **デスクトップデバイス**

  アセットブラウザーがウィンドウの左側に開きます。

  ページにアセットを追加するには、必要なアセットをクリックし、必要なコンポーネントまたは場所にドラッグします。

  ![デスクトップ版のアセットブラウザー](/help/sites-cloud/authoring/assets/assets-browser-desktop.png)

>[!NOTE]
>
>モバイルデバイスは、幅が 1,024 px 未満の場合に検出されます。つまり、画面の小さいデスクトップも検出されます。

アセットをすばやく変更する必要がある場合は、アセット名の横にある編集アイコンをクリックして、アセットブラウザーから直接[アセットエディター](/help/assets/manage-digital-assets.md)を開始できます。

![アセット編集ボタン](/help/sites-cloud/authoring/assets/asset-edit-button.png)

## コンテンツツリー {#content-tree}

The **コンテンツツリー** では、ページ上のすべてのコンポーネントの概要を階層で表示し、ページの構成を一目で確認できます。

コンテンツツリーは、サイドパネル内のタブです（コンポーネントブラウザーとアセットブラウザーも同じ場所にあります）。サイドパネルを開く（または閉じる）には、ツールバーの左上にある次のアイコンを使用します。

![コンテンツツリーボタン](/help/sites-cloud/authoring/assets/content-tree-button.png)

サイドパネルを開く際、パネルは（左側から）スライドして開きます。必要に応じて「**コンテンツツリー**」タブを選択します。このタブを開くと、ページやテンプレートがツリー形式で表示されるので、コンテンツの階層構造を理解しやすくなります。また、複雑なページでは、ページのコンポーネント間をジャンプしやすくなります。

![コンテンツツリー](/help/sites-cloud/authoring/assets/content-tree-editor.png)

ページは同じタイプの多数のコンポーネントで簡単に構成できます。コンテンツ（コンポーネント）ツリーには、コンポーネントタイプの名前（黒色）の後に説明テキスト（グレー）が表示されます。説明テキストは、コンポーネントの一般的なプロパティ（タイトルやテキストなど）から得られます。

コンポーネントタイプがユーザーの言語で表示されるのに対して、コンポーネントの説明テキストはページの言語で表示されます。

コンポーネントの横にある山形をクリックすると、そのレベルが折りたたまれたり展開されたりします。

![山形アイコンを使用したコンテンツツリーの展開](/help/sites-cloud/authoring/assets/content-tree-chevron.png)

コンポーネントをクリックすると、ページエディターでそのコンポーネントがハイライト表示されます。使用可能なアクションは、ページの状態によって異なります。

* 基本ページの例を次に示します。

  ![強調表示されたコンテンツツリー](/help/sites-cloud/authoring/assets/content-tree-highlighted.png)

  基本ページのコンポーネントには通常のオプションがあります。

  ツリー内でクリックしたコンポーネントが編集可能な場合は、レンチアイコンが名前の右側に表示されます。このアイコンをクリックすると、コンポーネントの編集ダイアログボックスが開きます。

  ![コンテンツツリー編集ボタン](/help/sites-cloud/authoring/assets/content-tree-edit.png)

* または、[ライブコピー](/help/sites-cloud/administering/msm/overview.md)の一部を構成するページが開かれます。ここではコンポーネントが別のページから継承されます。

>[!NOTE]
>
>ページをモバイルデバイス（ブラウザーの幅が 1,024 px より小さい場合）で編集している場合、コンテンツツリーは表示されません。

## フラグメント - 関連コンテンツブラウザー {#fragments-associated-content-browser}

ページにコンテンツフラグメントが含まれている場合、[関連コンテンツのブラウザー](/help/sites-cloud/authoring/fundamentals/content-fragments.md#using-associated-content)にもアクセスできます。

## 参照 {#references}

**参照**&#x200B;には、選択したページへの接続が表示されます。

* ブループリント
* ローンチ
* ライブコピー
* 言語コピー
* 被リンク
* 参照コンポーネントの使用：借りたコンテンツと貸したコンテンツ

必要なコンソールを開いたら、必要なリソースに移動し、次を使用して「**参照**」を開きます。

![参照オプション](/help/sites-cloud/authoring/assets/references.png)

[必要なリソースを選択](/help/sites-cloud/authoring/getting-started/basic-handling.md#viewing-and-selecting-resources)し、そのリソースに関連する参照タイプのリストを表示します。

![参照の詳細](/help/sites-cloud/authoring/assets/references-detail.png)

適切な参照タイプを選択すると、詳細情報が表示されます。状況によっては、特定の参照を選択すると、次のような追加のアクションが使用可能です。

* **被リンク**（当該ページを参照するページのリストと、特定のリンクを選択したときにそれらのページのいずれかを&#x200B;**編集**&#x200B;できる直接アクセスを提供）.

   * これにより、静的リンクのみが表示され、動的に生成されるリンク（例えば、リストコンポーネントからのリンク）は表示されません。

* **参照**&#x200B;コンポーネントを使用した借りたコンテンツおよび貸したコンテンツのインスタンス（ここから参照元／参照先ページに移動可能）
* [ローンチ](/help/sites-cloud/authoring/launches/overview.md)（関連するローンチへのアクセスを提供）
* [ライブコピー](/help/sites-cloud/administering/msm/overview.md)（選択したリソースに基づくすべてのライブコピーのパスを表示）
* [ブループリント](/help/sites-cloud/administering/msm/best-practices.md)（詳細と各種アクションを提供）
* [言語コピー](/help/sites-cloud/administering/translation/managing-projects.md#creating-translation-projects-using-the-references-panel)（詳細と各種アクションを提供）

## イベント - タイムライン {#events-timeline}

適切なリソース（例：**Sites** コンソールからのページ、**アセット**&#x200B;コンソールからのアセット）では、[タイムラインを使用して、選択した項目に対する最近のアクティビティを表示できます](/help/sites-cloud/authoring/getting-started/basic-handling.md#timeline)。

必要なコンソールを開いたら、必要なリソースに移動し、次を使用して「**タイムライン**」を開きます。

![タイムラインオプション](/help/sites-cloud/authoring/assets/timeline.png)

[必要なリソースを選択](/help/sites-cloud/authoring/getting-started/basic-handling.md#viewing-and-selecting-resources)し、「**すべて表示**」または「**アクティビティ**」を選択すると、選択したリソースに対する最近のアクションが一覧表示されます。

![タイムラインの詳細](/help/sites-cloud/authoring/assets/timeline-detail.png)

## ページ情報 {#page-information}

ページ情報（イコライザーアイコン）をクリックするとメニューが開き、最後の編集および最後の公開に関する詳細も表示されます。ページ、そのページのサイト、使用しているインスタンスの特性に応じて、使用できるオプションの数は異なります。

![ページ情報オプション](/help/sites-cloud/authoring/assets/page-information.png)

* [プロパティを開く](/help/sites-cloud/authoring/fundamentals/page-properties.md)
* [ページをロールアウト](/help/sites-cloud/administering/msm/overview.md#msm-from-the-ui)
* [ワークフローを開始](/help/sites-cloud/authoring/workflows/applying.md#starting-a-workflow-from-the-page-editor)
* [ページをロック](/help/sites-cloud/authoring/fundamentals/editing-content.md#locking-a-page)
* [ページを公開](/help/sites-cloud/authoring/fundamentals/publishing-pages.md#publishing-pages-1)
* [ページを非公開](/help/sites-cloud/authoring/fundamentals/publishing-pages.md#unpublishing-pages)
* [テンプレートを編集](/help/sites-cloud/authoring/features/templates.md)
* [公開済みとして表示](/help/sites-cloud/authoring/fundamentals/editing-content.md#view-as-published)
* [管理画面で表示](/help/sites-cloud/authoring/getting-started/basic-handling.md#viewing-and-selecting-resources)
* [ヘルプ](/help/sites-cloud/authoring/getting-started/basic-handling.md#accessing-help)
* [ローンチを昇格](/help/sites-cloud/authoring/launches/promoting.md)（ページがローンチの場合のみ）

該当する場合、**ページ情報**&#x200B;から分析やレコメンデーションを確認することもできます。

## ページモード {#page-modes}

ページの編集時には様々なモードがあり、異なるアクションを行うことができます。

* [編集](/help/sites-cloud/authoring/fundamentals/editing-content.md) - ページコンテンツの編集時に使用するモード。
* [レイアウト](/help/sites-cloud/authoring/features/responsive-layout.md)  — デバイスに応じたレスポンシブレイアウトを作成および編集できます（ページがレイアウトコンテナに基づいている場合）
* [ターゲット設定](/help/sites-cloud/authoring/personalization/targeted-content.md) - すべてのチャネルにわたるターゲティングと測定で、コンテンツの関連性を高めます。
* [タイムワープ](/help/sites-cloud/authoring/features/page-versions.md#timewarp) ：特定の時点のページの状態を表示できます。
* [ライブコピーステータス](/help/sites-cloud/authoring/fundamentals/editing-content.md#live-copy-status) - ライブコピーのステータスと継承される（または継承されない）コンポーネントの概要を素早く確認できます。
* [開発者モード](/help/implementing/developing/tools/developer-mode.md)
* [プレビュー](/help/sites-cloud/authoring/fundamentals/editing-content.md#previewing-pages) - パブリッシュ環境で表示されるページの表示、またはコンテンツ内のリンクを使用して移動するために使用します。
* [注釈](/help/sites-cloud/authoring/fundamentals/annotations.md) - ページで注釈の追加または表示を行う場合に使用するモード。

これらのモードには右上のアイコンを使用してアクセスできます。実際のアイコンは、現在利用中のモードに合わせて変化します。

![ページモード](/help/sites-cloud/authoring/assets/page-modes.png)

>[!NOTE]
>
>* ページの特性によっては、一部のモードを使用できない場合があります。
>* 一部のモードにアクセスするには、適切な権限または特権が必要です。
>* モバイルデバイスでは、スペースの制約により、開発者モードを使用できません。
>* ここに [キーボードショートカット](/help/sites-cloud/authoring/getting-started/keyboard-shortcuts.md) ( `Ctrl-Shift-M`) を切り替えます。 **プレビュー** 現在選択されているモード ( 例： **編集**, **レイアウト**&#x200B;など )。
>

## パスの選択 {#path-selection}

オーサリング時に、別のリソースを選択する必要が生じる場合がよくあります（別のページまたはリソースへのリンクを定義する場合、画像を選択する場合など）。パスの選択を簡単にするために、[パスフィールド](#path-fields)にはオートコンプリート機能があり、[パスブラウザー](#path-browser)ではより堅牢な選択が可能になっています。

### パスフィールド {#path-fields}

説明のためにここで使用する例は、画像コンポーネントです。コンポーネントの使用および編集について詳しくは、[ページオーサリング用コンポーネント](/help/sites-cloud/authoring/fundamentals/components.md)を参照してください。

パスフィールドには、オートコンプリート機能とルックアヘッド機能があり、リソースを見つけやすくなりました。

パスフィールドで「**選択ダイアログを開く**」ボタンをクリックすると、[パスブラウザー](#path-browser)ダイアログが開き、より詳細な選択オプションが表示されます。

![「選択ダイアログを開く」ボタン](/help/sites-cloud/authoring/assets/open-selection-dialog-button.png)

または、パスフィールドで入力を開始すると、入力した内容と一致するパスが表示されます。

![「選択ダイアログを開く」ボタン](/help/sites-cloud/authoring/assets/path-selection-completion.png)

### パスブラウザー {#path-browser}

パスブラウザーは、サイトコンソールの[列表示](/help/sites-cloud/authoring/getting-started/basic-handling.md#column-view)のように整理されており、リソースをより詳細に選択できます。

![パスブラウザー](/help/sites-cloud/authoring/assets/path-browser.png)

* リソースを選択すると、 **選択** ボタンがアクティブになります。 「選択」を選択して選択を確定するか、 **キャンセル** を中止します。
* コンテキストで複数のリソースを選択できる場合、リソースを選択すると「**選択**」ボタンがアクティブ化され、選択したリソースの数がウィンドウの右上に表示されます。すべての選択を解除するには、数字の横にある **X** をクリックします。
* ツリー内を移動すると、ダイアログ上部のパンくずリストに現在の位置が反映されます。これらのパンくずリストを使用すると、リソース階層内で素早くジャンプすることもできます。
* ダイアログボックスの上部にある検索フィールドは、いつでも使用できます。 検索フィールドの「**X**」をクリックして、検索をクリアします。
* 検索を絞り込むには、フィルターオプションを表示して、特定のパスに基づいて結果をフィルターできます。

  ![フィルターオプション](/help/sites-cloud/authoring/assets/filters-option.png)

## キーボードショートカット {#keyboard-shortcuts}

様々な[キーボードショートカット](/help/sites-cloud/authoring/getting-started/keyboard-shortcuts.md)を利用できます。
