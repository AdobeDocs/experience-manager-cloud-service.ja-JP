---
title: ページのオーサリングのクイックスタートガイド
description: ページコンテンツのオーサリングに初めて取り組む際に役立つ概要レベルのクイックガイドです。
exl-id: d37c9b61-7382-4bf6-8b90-59726b871264
source-git-commit: 07702fbebc768ee877d68219eff5551b09c7ff3e
workflow-type: tm+mt
source-wordcount: '1585'
ht-degree: 70%

---

# ページのオーサリングのクイックスタートガイド {#quick-guide-to-authoring-pages}

このドキュメントは、AEM での主要なページオーサリングアクションの概要を説明するクイックスタートガイドとして用意されています。このドキュメントでは、

* すべての内容を網羅しているわけではありません。
* 詳細なドキュメントへのリンクを示しています。

AEM によるオーサリングについて詳しくは、以下を参照してください。

* [オーサリングの概念](/help/sites-cloud/authoring/getting-started/concepts.md)
* [基本操作](/help/sites-cloud/authoring/getting-started/basic-handling.md)

## クイックヒント {#a-few-quick-hints}

このクイックスタートガイドを始める前に、オーサリングシステムの各領域に分けて、覚えておくべき一般的なヒントをいくつか以下に示します。

### サイトコンソール内 {#sites-console}

* 「作成」ボタン

   * このボタンは多くのコンソールで使用できます。表示されるオプションはコンテキストに依存するので、シナリオによって変わることがあります。

* ページの順序変更

   * これは[リスト表示](/help/sites-cloud/authoring/getting-started/basic-handling.md#list-view)で実行できます。変更内容が適用され、別の形式で表示できます。

### ページオーサリング {#page-authoring}

* リンクのナビゲーション

   * **リンクはナビゲーションに使用できません** いつ **編集** モード。 リンクを使用するには、 [ページをプレビュー](/help/sites-cloud/authoring/fundamentals/editing-content.md#previewing-pages) 次のいずれかを使用します。

      * [プレビューモード](/help/sites-cloud/authoring/fundamentals/editing-content.md#preview-mode)
      * [公開済みとして表示](/help/sites-cloud/authoring/fundamentals/editing-content.md#view-as-published)

* バージョンは、ページエディターで開始または作成されるわけではありません。（選択したリソースの「**作成**」または「[タイムライン](/help/sites-cloud/authoring/getting-started/basic-handling.md#timeline)」を通じて）**サイト**&#x200B;コンソールでおこなわれるようになりました。

>[!NOTE]
>
>オーサリング作業をより簡単にできる多くのキーボードショートカットがあります。
>
>* [ページ編集時のキーボードショートカット](/help/sites-cloud/authoring/fundamentals/keyboard-shortcuts.md)
>* [コンソールのキーボードショートカット](/help/sites-cloud/authoring/getting-started/keyboard-shortcuts.md)


### ページの検索 {#finding-your-page}

ページの検索には様々な特徴があります。移動や検索をおこなうには、次のようにします。

1. （**グローバルナビゲーション**&#x200B;の「**サイト**」オプションを使用して）[サイト](/help/sites-cloud/authoring/getting-started/basic-handling.md#global-navigation)コンソールを開きます。これは、Adobe Experience Manager リンク（左上）を選択するとトリガー（ドロップダウン）されます。

1. 適切なページをタップまたはクリックしてツリーの下方向に移動します。ページリソースがどのように表されるかは、使用している表示（[カード、リスト、列](/help/sites-cloud/authoring/getting-started/basic-handling.md#viewing-and-selecting-resources)）によって異なります。

   ![表示選択用ドロップダウン](/help/sites-cloud/authoring/assets/views.png)

1. [ヘッダーのパンくず](/help/sites-cloud/authoring/getting-started/basic-handling.md#the-header)を使用してツリーの上に移動します。これにより、選択した場所に戻ることができます。

   ![パンくずドロップダウン](/help/sites-cloud/authoring/assets/breadcrumb.png)

1. また、 [検索](/help/sites-cloud/authoring/getting-started/search.md) ページの 表示された結果からページを選択できます。

   ![検索フィールド](/help/sites-cloud/authoring/assets/search.png)

### 新しいページの作成 {#creating-a-new-page}

[新しいページを作成](/help/sites-cloud/authoring/fundamentals/organizing-pages.md#creating-a-new-page)するには：

1. [新しいページを作成する場所に移動します。](#finding-your-page)
1. 以下を使用： **作成** アイコンをクリックし、 **ページ** リストから：

   ![「作成」ボタン](/help/sites-cloud/authoring/assets/create.png)

1. ウィザードが開き、必要な情報の収集方法が示されます。 [新しいページの作成](/help/sites-cloud/authoring/fundamentals/organizing-pages.md#creating-a-new-page). 画面に表示される指示に従います。

### 追加のアクションを実行するページの選択 {#selecting-your-page-for-further-action}

ページを選択してアクションを実行できます。 ページを選択すると、ツールバーが自動的に更新され、そのリソースに関連するアクションが表示されます。

ページの選択方法は、コンソールで使用している表示によって異なります。

1. 列表示：

   * 必要なリソースのサムネールをタップまたはクリックします。サムネールが選択されていることを示すために、サムネールにチェックマークが付けられます。

1. リスト表示：

   * 必要なリソースのサムネールをタップまたはクリックします。サムネールが選択されていることを示すために、サムネールにチェックマークが付けられます。

1. カード表示：

   * [必要なリソースを選択](/help/sites-cloud/authoring/getting-started/basic-handling.md#viewing-and-selecting-resources)して選択モードに入ります。その方法は、次のようにデバイスによって異なります。

      * モバイルデバイス：カードをタップ＆ホールドする
      * デスクトップデバイス：チェックマークアイコンで表される[クイックアクション](/help/sites-cloud/authoring/getting-started/basic-handling.md#quick-actions)を使用する
   * ページが選択されていることを示すために、カードにチェックマークが付けられます。

   ![カードの例](/help/sites-cloud/authoring/assets/card.png)

### クイックアクション（カード表示／デスクトップのみ） {#quick-actions-card-view-desktop-only}

次のようにして、[クイックアクション](/help/sites-cloud/authoring/getting-started/basic-handling.md#quick-actions)を使用できます。

1. アクションを実行する[ページに移動](#finding-your-page)します。
1. 必要なリソースを表すカードの上にマウスポインターを置きます。クイックアクションが表示されます。

   ![カードのアクション](/help/sites-cloud/authoring/assets/card-actions.png)

### ページコンテンツの編集 {#editing-your-page-content}

ページを編集するには：

1. 編集する[ページに移動します。](#finding-your-page)
1. 編集（鉛筆）アイコンを使用して、[編集するページを開きます](/help/sites-cloud/authoring/fundamentals/organizing-pages.md#opening-a-page-for-editing)。

   ![「編集」ボタン](/help/sites-cloud/authoring/assets/edit.png)

   このアイコンには、次の場所からアクセスできます。

   * 該当するリソースの[クイックアクション（カード表示／デスクトップのみ）](#quick-actions-card-view-desktop-only)
   * ツールバー（[ページが選択されている](#selecting-your-page-for-further-action)場合）

1. エディターが開くと、次の操作を実行できます。

   * 次の方法を使用して、[新しいコンポーネントをページに追加](/help/sites-cloud/authoring/fundamentals/editing-content.md#inserting-a-component)します。

      * サイドパネルを開く。
      * 「コンポーネント」タブを選択する（[コンポーネントブラウザー](/help/sites-cloud/authoring/fundamentals/environment-tools.md#components-browser)）。
      * 必要なコンポーネントをページにドラッグする。

      サイドパネルは、次のアイコンで開く（および閉じる）ことができます。

      ![サイドパネルの切り替えボタン](/help/sites-cloud/authoring/assets/side-panel-toggle.png)

   * [既存のコンポーネントのコンテンツを編集](/help/sites-cloud/authoring/fundamentals/editing-content.md#component-toolbar) ページ上：

      * タップまたはクリックしてコンポーネントツールバーを開きます。以下を使用： **編集** （鉛筆）アイコンをクリックして、ダイアログを開きます。
      * タップ&amp;ホールドまたはダブルスロークリックで、コンポーネントのインプレースエディターを開きます。 使用可能なアクションが表示されます（一部のコンポーネントでは、これは制限付きで選択されます）。
      * 使用可能なすべてのアクションを表示するには、次を使用してフルスクリーンモードに入ります。

         ![全画面表示ボタン](/help/sites-cloud/authoring/assets/full-screen.png)
   * [既存のコンポーネントのプロパティを設定します。](/help/sites-cloud/authoring/fundamentals/editing-content.md#component-edit-dialog)

      * タップまたはクリックしてコンポーネントツールバーを開きます。以下を使用： **設定** （レンチ）アイコンを使用して、ダイアログを開きます。
   * [コンポーネントの移動](/help/sites-cloud/authoring/fundamentals/editing-content.md#moving-a-component) 次のいずれか：

      * 必要なコンポーネントを新しい場所にドラッグします。
      * タップまたはクリックしてコンポーネントツールバーを開きます。必要に応じて、**切り取り**&#x200B;アイコン、続いて&#x200B;**貼り付け**&#x200B;アイコンを使用します。
   * [コピー（および貼り付け）](/help/sites-cloud/authoring/fundamentals/editing-content.md#component-toolbar) 1 つのコンポーネント：

      * タップまたはクリックしてコンポーネントツールバーを開きます。必要に応じて、**コピー**&#x200B;アイコン、続いて&#x200B;**貼り付け**&#x200B;アイコンを使用します。
   >[!NOTE]
   >
   >同じページ、または別のページにコンポーネントを&#x200B;**貼り付ける**&#x200B;ことができます。切り取り／コピー操作を実行する前に開かれていたページに貼り付けるには、そのページを更新する必要があります。

   * コンポーネントを[削除します。](/help/sites-cloud/authoring/fundamentals/editing-content.md#component-toolbar)

      * タップまたはクリックしてコンポーネントツールバーを開き、**削除**&#x200B;アイコンを使用します。
   * [注釈の追加](/help/sites-cloud/authoring/fundamentals/annotations.md#annotations) を次のページに追加します。

      * を選択します。 **注釈** モード（吹き出しアイコン） を使用した注釈の追加 **注釈を追加** （プラス）アイコン 右上の X を使用して注釈モードを終了します。

         ![注釈ボタン](/help/sites-cloud/authoring/assets/annotations.png)
   * [ページのプレビュー](/help/sites-cloud/authoring/fundamentals/editing-content.md#preview-mode) （パブリッシュ環境での表示方法を確認するため）

      * 選択 **プレビュー** をクリックします。
   * を使用して編集モードに戻る（または別のモードを選択する） **編集** ドロップダウンセレクター

   >[!NOTE]
   >
   >コンテンツ内のリンクを使用して移動するには、次を使用する必要があります [プレビューモード](/help/sites-cloud/authoring/fundamentals/editing-content.md#preview-mode).

### ページプロパティの編集 {#editing-the-page-properties}

主に次の 2 つの方法があります。 [ページプロパティの編集](/help/sites-cloud/authoring/fundamentals/page-properties.md):

* **サイト**&#x200B;コンソールから：

   1. [ページに移動します。](#finding-your-page) を公開します。
   1. を選択します。 **プロパティ** アイコン：

      * 該当するリソースの[クイックアクション（カード表示／デスクトップのみ）](#quick-actions-card-view-desktop-only)
      * ツールバー（[ページが選択されている](#selecting-your-page-for-further-action)場合）

      ![「プロパティ」ボタン](/help/sites-cloud/authoring/assets/properties.png)

   1. ページのプロパティが表示されます。必要に応じて変更を加え、「保存」を使用してそれらを保持します。


* 条件 [ページの編集](#editing-your-page-content):

   1. を開きます。 **ページ情報** メニュー
   1. 選択 **プロパティを開く** をクリックして、プロパティを編集するためのダイアログを開きます。

      ![ページ情報ボタン](/help/sites-cloud/authoring/assets/page-information.png)

### ページの公開（または非公開） {#publishing-your-page-or-unpublishing}

主に次の 2 つの方法があります。 [ページのパブリッシュ](/help/sites-cloud/authoring/fundamentals/publishing-pages.md) （および非公開の場合も）:

* **サイト**&#x200B;コンソールから：

   1. [ページに移動します。](#finding-your-page) を公開します。
   1. 次のいずれかで「**クイック公開**」アイコンをクリックします。

      * 該当するリソースの[クイックアクション（カード表示／デスクトップのみ）](#quick-actions-card-view-desktop-only)
      * （[ページが選択されている](#selecting-your-page-for-further-action)場合）ツールバー（「[後で公開する](/help/sites-cloud/authoring/fundamentals/publishing-pages.md)」にアクセスすることもできます）

      ![「クイック公開」ボタン](/help/sites-cloud/authoring/assets/quick-publish.png)


* 条件 [ページの編集](#editing-your-page-content):

   1. を開きます。 **ページ情報** メニュー
   1. 選択 **ページを公開**.

* コンソールからページを非公開にする場合は、「**公開を管理**」オプションからのみおこなうことができます。このオプションは、ツールバーでのみ使用できます（クイックアクションからは使用できません）。

   ![「公開を管理」ボタン](/help/sites-cloud/authoring/assets/manage-publication.png)

   この **ページを非公開にする** オプションは、 **ページ情報** 」メニューが表示されます。

   詳しくは、 [ページの公開](/help/sites-cloud/authoring/fundamentals/publishing-pages.md#unpublishing-pages) を参照してください。

### ページの移動、コピー、貼り付け、削除 {#move-copy-and-paste-or-delete-your-page}

これらのアクションは、すべて次の方法でトリガーできます。

1. [ページに移動します。](#finding-your-page) 移動、コピー&amp;ペースト、または削除する
1. 必要に応じて、次のいずれかを使用して、コピー（続いて貼り付け）、移動または削除のアイコンを選択します。

   * [クイックアクション（カード表示/デスクトップのみ）](#quick-actions-card-view-desktop-only) 必要なリソースの
   * ツールバー（[ページが選択されている](#selecting-your-page-for-further-action)場合）

   以降の操作は、アクションに応じて、次のようになります。

   * [コピー](/help/sites-cloud/authoring/fundamentals/organizing-pages.md#copying-and-pasting-a-page):

      * 新しい場所に移動して、ペーストを行う必要があります。
   * [移動](/help/sites-cloud/authoring/fundamentals/organizing-pages.md#moving-or-renaming-a-page)：

      * ページの移動に必要な情報を収集するためのウィザードが開きます。画面に表示される手順に従ってください。
   * [削除](/help/sites-cloud/authoring/fundamentals/organizing-pages.md#deleting-a-page)：

      * この操作の確認が求められます。
   >[!NOTE]
   >
   >削除は、クイックアクションでは使用できません。

### ページのロック（およびロック解除） {#locking-your-page-then-unlocking}

[ページのロック](/help/sites-cloud/authoring/fundamentals/editing-content.md#locking-a-page)によって、自分の作業中に他の作成者が作業するのを防ぐことができます。ロック（およびロック解除）アイコン／ボタンは次の場所にあります。

* ツールバー（[ページが選択されている](#selecting-your-page-for-further-action)場合）
* （ページの編集時）[ページ情報ドロップダウンメニュー](#editing-the-page-properties)
* （ページの編集時）ページツールバー（ページがロックされている場合）

例えば、「ロック」アイコンは次のように表示されます。

![「ロック」ボタン](/help/sites-cloud/authoring/assets/lock.png)

### ページ参照へのアクセス {#accessing-page-references}

参照レールでは、ページへの（またはページからの）[参照に対するクイックアクセスを使用](/help/sites-cloud/authoring/fundamentals/environment-tools.md#references)できます。

1. （**ページ選択**&#x200B;の前または後に）ツールバーアイコンを使用して「[参照](#selecting-your-page-for-further-action)」を選択します。

   ![「参照」表示オプション](/help/sites-cloud/authoring/assets/references.png)

   参照のタイプのリストが表示されます。

   ![参照表示](/help/sites-cloud/authoring/assets/references-list.png)

1. 必要な参照タイプをタップまたはクリックして詳細を表示し、（必要に応じて）追加のアクションを実行します。

### ページのバージョンの作成 {#creating-a-version-of-your-page}

ページの[バージョン](/help/sites-cloud/authoring/features/page-versions.md)を作成するには：

1. タイムラインレールを開くには、（**[ページ選択](/help/sites-cloud/authoring/getting-started/basic-handling.md#timeline)**&#x200B;の前または後に）ツールバーアイコンを使用して「[タイムライン](#selecting-your-page-for-further-action)」を選択します。

   ![「タイムライン」表示オプション](/help/sites-cloud/authoring/assets/timeline.png)

1. 「タイムライン」列の右下にある省略記号アイコンをタップまたはクリックし、その他のボタン（「**バージョンとして保存**」など）を表示します。

   ![タイムライン表示](/help/sites-cloud/authoring/assets/timeline-view.png)

1. 「**バージョンとして保存**」を選択し、「**作成**」を選択します。

### ページのバージョンの復元と比較 {#restoring-comparing-a-version-of-your-page}

ページのバージョンの復元と比較では、使用する基本的なメカニズムは同じです。

1. （**[ページ選択](/help/sites-cloud/authoring/getting-started/basic-handling.md#timeline)**&#x200B;の前または後に）ツールバーアイコンを使用して「[タイムライン](#selecting-your-page-for-further-action)」を選択します。

   ![「タイムライン」表示オプション](/help/sites-cloud/authoring/assets/timeline.png)

   ページのバージョンが既に保存されている場合、そのバージョンがタイムラインに表示されます。

1. 復元するバージョンをタップまたはクリックします。これにより、追加のアクションボタンが表示されます。

   * **このバージョンに戻る**

      * このバージョンが復元されます。
   * **違いを表示**

      * ページが開き、（2 つのバージョン間の）違いが強調表示されます。
