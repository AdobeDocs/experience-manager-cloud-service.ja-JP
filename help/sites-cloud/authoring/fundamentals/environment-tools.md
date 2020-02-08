---
title: オーサリング環境とツール
description: AEM のオーサリング環境は、コンテンツを構造化および編集するための様々なメカニズムを提供しています
translation-type: tm+mt
source-git-commit: 16725342c1a14231025bbc1bafb4c97f0d7cfce8

---


# オーサリング環境とツール {#authoring-the-environment-and-tools}

AEMのオーサリング環境では、コンテンツを編成および編集するための様々なメカニズムが提供されます。提供されるツールは、様々なコンソールやページエディターからアクセスできます。

## サイトの管理 {#managing-your-site}

The **Sites** console allows you to navigate and manage your website, using the header bar, toolbar, action icons (applicable for the selected resource), breadcrumbs, and, when selected, secondary rails (for example, timeline and references).

例えば、列表示では次のようになります。

![列表示](/help/sites-cloud/authoring/assets/column-view.png)

## ページのコンテンツの編集 {#editing-page-content}

ページはページエディターで編集できます。次に例を示します。

`http://<host>:<port>/editor.html/content/wknd/en/sports/la-skateparks.html`

![ページエディター](/help/sites-cloud/authoring/assets/page-editor.png)

>[!NOTE]
>
>編集対象のページを初めて開くと、機能を紹介する一連のスライドが表示されます。
>
>必要がない場合は、このツアーをスキップすることができます。このツアーは、**ページ情報**&#x200B;メニューからいつでも表示できます。

## ヘルプへのアクセス {#accessing-help}

ページの編集中、**ヘルプ**&#x200B;には次の場所からアクセスできます。

* The [**Page Information **](/help/sites-cloud/authoring/fundamentals/page-properties.md#page-properties)selector which shows the introductory slides (as shown the first time you access the editor)
* The [configuration](/help/sites-cloud/authoring/fundamentals/editing-content.md#component-toolbar) dialog for specific components (using the ? アイコンを参照)。状況依存ヘルプを表示します。

その他の[ヘルプ関連リソースは、コンソールから表示できます](/help/sites-cloud/authoring/getting-started/basic-handling.md#accessing-help)。

## コンポーネントブラウザー {#components-browser}

コンポーネントは、AEMコンテンツの構成要素です。 AEMでコンテンツページを作成するには、1つのページに複数のコンポーネントを配置し、そのオプションを設定します。

コンポーネントブラウザーには、現在のページで使用可能なすべてのコンポーネントが表示されます。これらのコンポーネントを適切な場所にドラッグして編集することで、コンテンツを追加できます。

The components browser is a tab within the side panel (together with the [assets browser](#assets-browser) and [content tree](#content-tree)). サイドパネルを開く（または閉じる）には、ツールバーの左上にある次のアイコンを使用します。

![サイドパネル切り替え](/help/sites-cloud/authoring/assets/side-panel-toggle.png)

サイドパネルを開く際、パネルは（左側から）スライドして開きます（必要に応じて「**コンポーネント**」タブを選択）。開いたら、ページで使用可能なすべてのコンポーネントを閲覧することができます。

実際の外観や処理は、使用しているデバイスの種類によって異なります。

* **モバイルデバイス（iPad など）**

   コンポーネントブラウザーは、編集中のページ全体に開かれます。

   ページにコンポーネントを追加するには、目的のコンポーネントをタッチ＆ホールドし、右側に移動します。コンポーネントブラウザーが閉じてページが再表示され、このページ上でコンポーネントを配置できます。

   ![モバイル上のコンポーネントブラウザ](/help/sites-cloud/authoring/assets/component-browser-mobile.png)

* **デスクトップデバイス**

   コンポーネントブラウザーがウィンドウの左側に開きます。

   ページにコンポーネントを追加するには、目的のコンポーネントをクリックして、必要な位置までドラッグします。

   ![デスクトップのコンポーネントブラウザ](/help/sites-cloud/authoring/assets/component-browser-desktop.png)

   コンポーネントは次のものによって表されます。

   * コンポーネント名
   * コンポーネントグループ（グレー）
   * アイコンまたは略語
      * 標準コンポーネントのアイコンはモノクロです。
      * 省略形は、常にコンポーネント名の最初の2文字です。
   **コンポーネント**&#x200B;ブラウザーの上部のツールバーでは、次の操作を実行できます。

   * コンポーネントを名前でフィルターします。
   * ドロップダウンから選択して特定のグループのみを表示します。
   コンポーネントについて詳しくは、**コンポーネント**&#x200B;ブラウザー内のコンポーネントの横にある情報アイコンをクリックまたはタップしてください（使用可能な場合）。例えば、コンテンツフラグメ **ントの場合**:

   ![コンポーネントブラウザ情報](/help/sites-cloud/authoring/assets/component-browser-information.png)

   使用可能なコンポーネントについて詳しくは、[コンポーネントコンソール](/help/sites-cloud/authoring/features/components-console.md)を参照してください。

>[!NOTE]
>
>モバイルデバイスは、幅が 1,024 px 未満の場合に検出されます。これは、デスクトップの小さいウィンドウの場合にも当てはまります。

## アセットブラウザー {#assets-browser}

The assets browser shows all assets that are available for direct use on your current page. <!--The assets browser shows all [assets](/help/assets/home.md) that are available for direct use on your current page.-->

The assets browser is a tab within the side panel along with the [components browser](#components-browser) and [content tree](#content-tree). サイドパネルを開く（または閉じる）には、ツールバーの左上にある次のアイコンを使用します。

![サイドパネル切り替え](/help/sites-cloud/authoring/assets/side-panel-toggle.png)

サイドパネルを開く際、パネルは（左側から）スライドして開きます。必要に応じて「**アセット**」タブを選択します。

![アセットブラウザボタン](/help/sites-cloud/authoring/assets/assets-browser-button.png)

アセットブラウザーが開くと、ページで使用可能なすべてのアセットを参照できます。必要に応じて無限スクロールを使用してリストを拡大できます。

![アセットブラウザー](/help/sites-cloud/authoring/assets/assets-browser.png)

ページにアセットを追加するには、選択して必要な位置までドラッグします。次のアセットを使用できます。

* 適切な種類の既存のコンポーネント。
   * 例えば、画像タイプのアセットを画像コンポーネントにドラッグできます。
* 適切なタイプの新しいコンポーネントを作成するための段落システム内の[プレースホルダー](/help/sites-cloud/authoring/fundamentals/editing-content.md#component-placeholder)。
   * 例えば、imageタイプのアセットを段落システムにドラッグして、imageコンポーネントを作成できます。

>[!NOTE]
>
>これは特定のタイプのアセットとコンポーネントで使用できます。詳しくは、[アセットブラウザーを使用したコンポーネントの挿入](/help/sites-cloud/authoring/fundamentals/editing-content.md#inserting-a-component-using-the-assets-browser)を参照してください。

アセットブラウザーの上部のツールバーでは、アセットを次の項目で検索できます。

* 名前
* パス
* 画像、ビデオ、ドキュメント、段落、コンテンツフラグメント、エクスペリエンスフラグメントなどのアセットタイプ
* 方向やスタイルなどのアセットの特性
   * 特定のアセットタイプでのみ使用可能

実際の外観や処理は、使用しているデバイスの種類によって異なります。

* **モバイルデバイス**

   アセットブラウザーは、編集中のページ全体に表示されます。

   ページにアセットを追加するには、目的のアセットをタッチ＆ホールドし、右側に移動します。アセットブラウザーが閉じてページが再表示され、このページ上で目的のコンポーネントにアセットを追加できます。

   ![モバイル版アセットブラウザー](/help/sites-cloud/authoring/assets/assets-browser-mobile.png)

* **デスクトップデバイス**

   アセットブラウザーがウィンドウの左側に開きます。

   ページにアセットを追加するには、目的のアセットをクリックして、必要なコンポーネントまたは場所までドラッグします。

   ![デスクトップのアセットブラウザー](/help/sites-cloud/authoring/assets/assets-browser-desktop.png)

>[!NOTE]
>
>モバイルデバイスは、幅が 1,024 px 未満の場合に検出されます。つまり、画面の小さいデスクトップも検出されます。

If you need to quickly make a change to an asset, you can start the asset editor directly from the asset browser by clicking the edit icon shown next to the asset&#39;s name. <!--If you need to quickly make a change to an asset, you can start the [asset editor](/help/assets/manage-digital-assets.md) directly from the asset browser by clicking the edit icon shown next to the asset's name.-->

![アセット編集ボタン](/help/sites-cloud/authoring/assets/asset-edit-button.png)

## コンテンツツリー {#content-tree}

**コンテンツツリー**&#x200B;は、ページの構成を一目で確認できるように、ページのすべてのコンポーネントの概要を階層形式で表示します。

コンテンツツリーは、サイドパネル内のタブです（コンポーネントブラウザーとアセットブラウザーも同じ場所にあります）。サイドパネルを開く（または閉じる）には、ツールバーの左上にある次のアイコンを使用します。

![コンテンツツリーボタン](/help/sites-cloud/authoring/assets/content-tree-button.png)

サイドパネルを開く際、パネルは（左側から）スライドして開きます。Select the **Content Tree** tab if necessary. このタブを開くと、ページまたはテンプレートをツリービューで確認でき、コンテンツの階層的な構造を簡単に理解できます。また、複雑なページではページのコンポーネント間をジャンプしやすくなります。

![コンテンツツリー](/help/sites-cloud/authoring/assets/content-tree-editor.png)

ページは、同じタイプの多くのコンポーネントで簡単に構成できるので、コンテンツ（コンポーネント）ツリーには、コンポーネントタイプ名の後に説明テキスト（灰色）が表示されます（黒）。 説明テキストは、コンポーネントの共通プロパティ（タイトル、テキストなど）から取得されます。

コンポーネントタイプはユーザーの言語で表示されますが、コンポーネントの説明テキストはページの言語で表示されます。

コンポーネントの横にある山形アイコンをクリックすると、レベルを折りたたむ、または展開することができます。

![コンテンツツリーの山形展開](/help/sites-cloud/authoring/assets/content-tree-chevron.png)

コンポーネントをクリックすると、ページエディターでそのコンポーネントが強調表示されます。使用可能なアクションは、ページの状態によって異なります。

* 次の基本ページの例を示します。

   ![ハイライトされたコンテンツツリー](/help/sites-cloud/authoring/assets/content-tree-highlighted.png)

   基本ページのコンポーネントには通常のオプションがあります。

   ツリーでクリックしたコンポーネントが編集可能な場合は、スパナアイコンが名前の右側に表示されます。このアイコンをクリックすると、コンポーネントの編集ダイアログが直接開始されます。

   ![コンテンツツリーの編集ボタン](/help/sites-cloud/authoring/assets/content-tree-edit.png)

* ライブコピーの一部であるページで、コンポーネントが別のページから継承される場合、継承オプションを含む選択肢は少なくなります。 <!--A page that is part of a [livecopy](/help/sites-administering/msm.md), where components are inherited from another page:-->

>[!NOTE]
>
>モバイルデバイス上でページを編集している場合（ブラウザーの幅が1024px未満の場合）、コンテンツツリーは使用できません。

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

Open the required console, then navigate to the required resource and open **References** using:

![参照オプション](/help/sites-cloud/authoring/assets/references.png)

[必要なリソースを選択](/help/sites-cloud/authoring/getting-started/basic-handling.md#viewing-and-selecting-resources)し、そのリソースに関連する参照タイプの一覧を表示します。

![参照の詳細](/help/sites-cloud/authoring/assets/references-detail.png)

適切な参照タイプを選択すると、詳細情報が表示されます。状況によっては、次のような特定の参照の選択時にアクションを追加で実行できます。

* **被リンク**（当該ページを参照するページのリストと、特定のリンクを選択したときにそれらのページのいずれかを&#x200B;**編集**&#x200B;できる直接アクセスを提供）
* **参照**&#x200B;コンポーネントを使用した借りたコンテンツおよび貸したコンテンツのインスタンス（ここから参照元／参照先ページに移動可能）
* [起動回数](/help/sites-cloud/authoring/launches/overview.md)。関連する起動にアクセスできます。
* Live Copies displays the paths of all live copies that are based on the selected resource. <!--[Live Copies](/help/sites-administering/msm.md) displays the paths of all live copies that are based on the selected resource.-->
* Blueprint provides details and various actions <!--[Blueprint](/help/sites-administering/msm-best-practices.md), provides details and various actions-->
* Languages Copies provides details and various actions <!--[Languages Copies](/help/sites-administering/tc-manage.md#creating-translation-projects-using-the-references-panel), provides details and various actions-->

## イベント - タイムライン {#events-timeline}

該当するリソース（例：**サイト**&#x200B;コンソールからのページ、**アセット**&#x200B;コンソールからのアセット）では、[タイムラインを使用して、選択した項目に対する最近のアクティビティを表示できます](/help/sites-cloud/authoring/getting-started/basic-handling.md#timeline)。

Open the required console, then navigate to the required resource and open **Timeline**, using:

![タイムラインオプション](/help/sites-cloud/authoring/assets/timeline.png)

[必要なリソースを選択](/help/sites-cloud/authoring/getting-started/basic-handling.md#viewing-and-selecting-resources)し、「**すべて表示**」または「**アクティビティ**」を選択すると、選択したリソースに対する最近のアクションが一覧表示されます。

![タイムラインの詳細](/help/sites-cloud/authoring/assets/timeline-detail.png)

## ページ情報 {#page-information}

ページ情報（イコライザアイコン）は、最後の編集と最後のパブリケーションに関する詳細も提供するメニューを開きます。 ページ、そのページのサイト、使用しているインスタンスの特性に応じて、使用できるオプションの数は異なります。

![ページ情報オプション](/help/sites-cloud/authoring/assets/page-information.png)

* [プロパティを開く](/help/sites-cloud/authoring/fundamentals/page-properties.md)
* ページをロールアウト <!--[Rollout Page](/help/sites-administering/msm.md#msm-from-the-ui)-->
* [ワークフローを開始](/help/sites-cloud/authoring/workflows/applying.md#starting-a-workflow-from-the-page-editor)
* [ページをロック](/help/sites-cloud/authoring/fundamentals/editing-content.md#locking-a-page)
* [ページを公開](/help/sites-cloud/authoring/fundamentals/publishing-pages.md#publishing-pages-1)
* [ページを非公開にする](/help/sites-cloud/authoring/fundamentals/publishing-pages.md#unpublishing-pages)
* [テンプレートを編集](/help/sites-cloud/authoring/features/templates.md)
* [公開済みとして表示](/help/sites-cloud/authoring/fundamentals/editing-content.md#view-as-published)
* [管理画面で表示](/help/sites-cloud/authoring/getting-started/basic-handling.md#viewing-and-selecting-resources)
* [ヘルプ](/help/sites-cloud/authoring/getting-started/basic-handling.md#accessing-help)
* [Promote Launch](/help/sites-cloud/authoring/launches/promoting.md) （ページが起動の場合のみ）

該当する場合、**ページ情報**&#x200B;から分析や推奨を確認することもできます。

## ページモード {#page-modes}

ページの編集時には様々なモードがあり、異なるアクションをおこなうことができます。

* [編集](/help/sites-cloud/authoring/fundamentals/editing-content.md) - ページコンテンツの編集時に使用するモード。
* [レイアウト](/help/sites-cloud/authoring/features/responsive-layout.md) — デバイスに依存するレスポンシブレイアウトを作成および編集できます（ページがレイアウトコンテナに基づいている場合）。
* [ターゲット設定](/help/sites-cloud/authoring/personalization/targeted-content.md) - すべてのチャネルにわたるターゲット設定と測定を通じてコンテンツの関連性を高めます。
* [タイムワープ](/help/sites-cloud/authoring/features/page-versions.md#timewarp) - 特定の時点のページの状態を表示できます。
* [ライブコピーステータス](/help/sites-cloud/authoring/fundamentals/editing-content.md#live-copy-status) - ライブコピーのステータスの簡単な概要および継承される（または継承されない）コンポーネントを示します。
* [プレビュー](/help/sites-cloud/authoring/fundamentals/editing-content.md#previewing-pages) - パブリッシュ環境とまったく同じ形式でページを表示する、またはコンテンツ内のリンクを使用して移動するために使用します。
* [注釈](/help/sites-cloud/authoring/fundamentals/annotations.md) - ページで注釈の追加または表示をおこなう場合に使用するモード。

これらのモードには右上のアイコンを使用してアクセスできます。実際のアイコンは、現在利用中のモードに合わせて変化します。

![ページモード](/help/sites-cloud/authoring/assets/page-modes.png)

>[!NOTE]
>
>* ページの特性によっては、一部のモードを使用できないことがあります。
>* 一部のモードにアクセスするには、適切な権限が必要です。
>* 開発者モードは、スペースの制約により、モバイルデバイスでは利用できません。
>* There is a [keyboard shortcut](/help/sites-cloud/authoring/getting-started/keyboard-shortcuts.md) ( `Ctrl-Shift-M`) to toggle between **Preview** and the currently selected mode (e.g. **Edit**, **Layout**, etc).
>



## パスの選択 {#path-selection}

オーサリング時に、別のリソースを選択する必要がある場合がよくあります（別のページまたはリソースへのリンクを定義する場合、画像を選択する場合など）。簡単にパスを選択するために、[パスフィールド](#path-fields)にはオートコンプリート機能があり、[パスブラウザー](#path-browser)には強力な選択機能があります。

### パスフィールド {#path-fields}

説明のためにここで使用する例は、画像コンポーネントです。コンポーネントの使用および編集について詳しくは、[ページオーサリング用コンポーネント](/help/sites-cloud/authoring/fundamentals/components.md)を参照してください。

パスフィールドには、リソースの検索を容易にするためのオートコンプリート機能とルックアヘッド機能が追加されました。

パスフィールドで「**選択ダイアログを開く**」ボタンをクリックすると、[パスブラウザー](#path-browser)ダイアログが開き、より詳細な選択オプションが表示されます。

![選択ダイアログを開くボタン](/help/sites-cloud/authoring/assets/open-selection-dialog-button.png)

または、パスフィールドで入力を開始すると、入力した内容と一致するパスが表示されます。

![選択ダイアログを開くボタン](/help/sites-cloud/authoring/assets/path-selection-completion.png)

### パスブラウザー {#path-browser}

パスブラウザーは、サイトコンソールの[列表示](/help/sites-cloud/authoring/getting-started/basic-handling.md#column-view)のように整理されており、リソースをより詳細に選択できます。

![パスブラウザー](/help/sites-cloud/authoring/assets/path-browser.png)

* リソースを選択すると、ダイアログの右上にある「**選択**」ボタンがアクティブになります。クリックまたはタップして選択内容を確認するか、「**キャンセル**」をクリックして中止します。
* コンテキストで複数のリソースを選択できる場合、リソースを選択すると「**選択**」ボタンがアクティブ化され、選択したリソースの数がウィンドウの右上に表示されます。すべての選択を解除するには、数値の横にある **X** をクリックします。
* ツリー内を移動すると、ダイアログ上部のパンくずリストに現在の位置が反映されます。これらのパンくずリストを使用すると、リソース階層内ですばやくジャンプすることもできます。
* ダイアログの上部にある検索フィールドはいつでも使用できます。検索をクリアするには、検索フィールドの **X** をクリックします。
* 検索を絞り込むには、フィルターオプションを表示して、特定のパスに基づいて結果をフィルターできます。

   ![フィルターオプション](/help/sites-cloud/authoring/assets/filters-option.png)

## キーボードショートカット {#keyboard-shortcuts}

様々な[キーボードショートカット](/help/sites-cloud/authoring/getting-started/keyboard-shortcuts.md)も利用できます。
