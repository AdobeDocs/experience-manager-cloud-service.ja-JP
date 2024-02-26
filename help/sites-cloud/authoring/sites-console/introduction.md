---
title: サイトコンソール
description: サイトコンソールを使用してAEMページを管理および整理する方法について説明します。
source-git-commit: bbd845079cb688dc3e62e2cf6b1a63c49a92f6b4
workflow-type: tm+mt
source-wordcount: '1596'
ht-degree: 51%

---


# サイトコンソール {#sites-console}

の使用方法を学ぶ **Sites** コンソールを使用して、AEMページを管理および整理します。

## 向き {#orientation}

The **Sites** コンソールでは、ページ階層を表示できます。

![項目が選択された状態でのサイトコンソールの列表示](assets/sites-console-column-view-selected.png)

ページの管理と整理に役立つ様々なビューとツールバーが用意されています。

* [コンソールツールバー](#toolbar) が常に存在し、操作に役立ちます。
* [3 つの異なるビュー](#views) を使用すると、ページを簡単に見つけて選択できます。
* [アクションツールバー](#action-toolbar) アクションを実行する項目を選択したときに表示されます。
* [サイドパネル](#side-panel) には、選択したページに関する詳細情報を表示するための複数のオプションがあります。

## コンソールツールバー {#console-toolbar}

コンソールツールバーは常にコンソールに表示され、コンテンツの向きを変更したり、コンテンツを移動したりするのに役立ちます。

![サイトコンソールのツールバー](assets/sites-console-toolbar.png)

### サイドパネルセレクター {#side-panel-selector}

サイドパネルセレクターを使用すると、選択した項目に関する追加情報をコンソールに表示できます。

![サイドパネルセレクターボタン](assets/sites-console-side-panel-button.png)

現在のコンソールに応じて表示されるオプションです。例えば、**Sites** では、コンテンツのみ（デフォルト）、タイムライン、参照またはフィルターのサイドパネルを選択できます。

![サイドパネルセレクターの例](assets/sites-console-side-panel-selector.png)

サイドパネルの詳細については、ドキュメントを参照してください。 [サイトコンソールのサイドパネル。](/help/sites-cloud/authoring/sites-console/console-side-panel.md)

### パンくずリスト {#breadcrumbs}

パネルの中央に位置し、常に現在選択されている項目の説明を表示するパンくずリストを使用すると、Web サイトのレベル間を移動できます。

![ナビゲーションバーのパンくずリスト](assets/sites-console-breadcrumbs-navigation.png)


パンくずテキストをタップまたはクリックすると、現在選択されている項目の階層レベルをリストするドロップダウンが表示されます。 エントリをタップまたはクリックすると、その場所にジャンプできます。

![展開したパンくずリストの例](assets/sites-console-breadcrumbs-example.png)

### すべてを選択 {#select-all}

をタップまたはクリックして、 **すべてを選択** ボタンは、コンソールの現在のビュー内のすべての項目を選択します。

![「すべて選択」ボタン](assets/sites-console-select-all.png)

すべての項目を選択した場合、選択した項目の数がツールバーの右上に表示されます。この場合、 **すべてを選択** ボタンが表示されました。

すべての項目の選択を解除して選択モードを終了するには、次の操作を行います。

* をクリックまたはタップする **X** 数の横にある
* の使用 **逃げ出す** キー。

![すべてを選択解除](assets/sites-console-deselect-all.png)

### 「作成」ボタン {#create-button}

The **作成** ボタンを使用すると、サイトに新しいページを追加したり、ライブコピーやローンチなどの追加の Sites オブジェクトを作成したりできます。

![「作成」ボタン](assets/sites-console-create.png)

クリックすると、表示されるオプションはコンソール/コンテキストに適しています。 最も一般的なものは次のとおりです。

* [Page](/help/sites-cloud/authoring/sites-console/creating-pages.md)
* [サイト](/help/sites-cloud/administering/site-creation/create-site.md)
* [ライブコピー](/help/sites-cloud/administering/msm/overview.md)
* [Experience Platform Launch](/help/sites-cloud/authoring/launches/overview.md)
* [言語コピー](/help/sites-cloud/administering/translation/overview.md)
* [CSV レポート](/help/sites-cloud/authoring/sites-console/csv-export.md)

機能の詳細については、これらの機能へのリンクを参照してください。

## ページの表示と選択 {#views}

The **Sites** コンソールは、コンテンツ階層の 3 つの異なるビューを提供します。 使用可能な任意の表示で、リソースを表示、ナビゲーション、および（追加のアクションをおこなうために）選択できます。

* [列表示](#column-view)
* [カード表示](#card-view)
* [リスト表示](#list-view)

The **表示** AEMツールバーの右端にあるアイコンは、現在選択されているビューを示します。

タップまたはクリックすると、別のビューを選択できます。

![表示ボタン](assets/sites-console-views-button.png)

列表示、カード表示、リスト表示を切り替えることができます。リスト表示では、表示設定も表示されます。

![表示](assets/sites-console-view.png)

>[!NOTE]
>
>「**表示設定**」オプションは、**リスト表示**&#x200B;モードでのみ使用できます。

概念上、表示、ナビゲーションおよび選択はすべての表示で同じ操作ですが、使用している表示によって処理がわずかに異なります。

>[!NOTE]
>
>デフォルトでは、AEM Assets のいずれの表示においても、UI のアセットの元のレンディションはサムネールとして表示されません。管理者の場合は、オーバーレイを使用すると、元のレンディションをサムネールとして AEM Assets に表示するように設定できます。

### リソースの選択 {#selecting-resources}

特定のリソースの選択方法は、表示とデバイスの組み合わせによって異なります。

| 表示 | タッチの選択 | デスクトップの選択 | タッチの選択解除 | デスクトップの選択解除 |
|---|---|---|---|---|
| 列 | サムネールを選択 | サムネールをクリック | サムネールを選択 | サムネールをクリック |
| カード | カードを選択＆ホールド | 項目の上にマウスを移動しチェックマークのクイックアクションを使用 | カードを選択 | カードをクリック |
| リスト | サムネールを選択 | サムネールをクリック | サムネールを選択 | サムネールをクリック |

#### 選択の例 {#selecting-example}

1. 例えば、カード表示では次のようになります。

   ![カード表示の選択](assets/sites-console-card-view-select.png)

1. リソースを選択すると、上部のヘッダーの上に[アクションツールバー](#actions-toolbar)が重なって表示され、選択したリソースで現在適用可能なアクションにアクセスできます。

1. 選択モードを終了するには、右上の「**X**」を選択するか、**Esc** キーを使用します。

### 列表示 {#column-view}

列表示では、一連のカスケード列を通じて、コンテンツツリーを視覚的にナビゲーションできます。 この表示では、web サイトのツリー構造を視覚化して移動できます。

![列表示](assets/sites-console-column-view.png)

一番左の列でリソースを選択すると、右の列に子リソースが表示されます。右側の列でリソースを選択すると、さらに右側の列にその子リソースが表示されます。

* リソース名またはその右にある山形記号をタップまたはクリックすると、ツリー内を上下に移動できます。

   * タップまたはクリックするとリソース名と山形記号がハイライト表示されます。
   * クリックまたはタップしたリソースの子は、クリックまたはタップしたリソースの右側の列に表示されます。
   * 子を持たないリソース名を選択すると、その詳細が最後の列に表示されます。

* サムネールをタップまたはクリックすると、リソースが選択されます。

   * すると、チェックマークがサムネールにオーバーレイ表示され、リソース名もハイライト表示されます。
   * 選択されたリソースの詳細が最後の列に表示されます。
   * アクションツールバーが使用可能になります。

* 列表示でページを選択すると、選択したページが次の詳細と共に最後の列に表示されます。

   * ページタイトル
   * ページ名（ページの URL の一部）
   * ページの基になるテンプレート
   * 変更の詳細
   * ページ言語
   * 公開およびプレビューの詳細

### カード表示 {#card-view}

カード表示では、階層の現在のレベルの各項目が大きなカードとして表示されます。

![カードビュー](assets/sites-console-card-view.png)

* カードは次のような情報を提供します。

   * ページの内容を視覚的に表現したもの。
   * ページのタイトル。
   * 重要な日付（最終編集日、最終公開日など）。
   * ページがロックされているか、非表示になっているか、ライブコピーの一部であるか。
   * ワークフローの一部として項目に対する操作が必要な場合は、「指標」を使用します。

カード表示もオファー [クイックアクション](#quick-actions) 項目（選択など）と、編集などの一般的なアクション。

![クイックアクション](assets/sites-console-quick-actions.png)

カードを（クイックアクションをタップしないように慎重に）タップまたはクリックしてツリーの下に移動したり、 [ヘッダーのパンくずリスト](#the-header).

### リスト表示 {#list-view}

リスト表示では、リストの現在のレベルの各リソースの情報が表示されます。

![リスト表示](assets/sites-console-list-view.png)

* リソース名をタップまたはクリックしてツリーの下に移動したり、[ヘッダーのパンくずリスト](#the-header)を使用して上に戻ったりできます。
* リスト内のすべての項目を簡単に選択するには、 [**すべてを選択** 」チェックボックスをオンにします。](#select-all)

* 表示ボタンの下にある「**設定を表示**」オプションを使用して、表示する列を選択します。次の列を表示できます。

   * **名前** - ページ名。ページの URL の一部であり、言語に関係なく変化しないので、多言語オーサリング環境で役立つ場合があります。
   * **更新** - 最終更新日と最終更新者
   * **公開** - 公開ステータス
   * **プレビュー** - プレビューステータス
   * **テンプレート** - ページがベースにしているテンプレート
   * **操作**
   * **ワークフロー** - 現在ページに適用されているワークフロー。ポインタを合わせたり、タイムラインを開いたりすると、詳細情報が表示されます。
   * **翻訳済み**
   * **ページビュー数**
   * **実訪問者数**
   * **ページ滞在時間**

![列を設定](assets/sites-console-select-columns.png)

デフォルトでは、ページの URL の一部を構成する「**名前**」列が表示されます。場合によっては、作成者は、異なる言語のページにアクセスする必要があることがあり、ページの名前（通常は変更なし）を確認することは、作成者がページの言語を知らない場合に非常に役立ちます。

* リストの各項目の右端にある縦の点線マークを使用して項目の順序を変更します。

![列の順序](assets/sites-console-column-order.png)

縦の選択バーを選択して、項目をリストの新しい位置にドラッグします。

![順序のリスト](assets/sites-console-order-list.png)

>[!NOTE]
>
>順序を変更できるのは、`jcr:primaryType` 値が `sling:OrderedFolder` である順序付きフォルダーの内部のみです。

## アクションツールバー {#actions-toolbar}

リソースが選択されている場合は、選択したアイテムに対して様々なアクションを実行できます。 これらのアクションは、アクションツールバーに表示されます。

![アクションツールバー](assets/introduction-actions-toolbar.png)

アクションツールバーは、コンソールでリソースが選択されている場合にのみ表示されます。 アクションツールバーで使用できるアクションは、選択した特定の項目に対して実行できるアクションを反映して変化します。 最も一般的なアクションは次のとおりです。

* [作成](#create-action)  — 新しいコンテンツまたはコンテンツ関連のアクションを作成します
* [編集](/help/sites-cloud/authoring/page-editor/introduction.md)  — ページを編集します
* [プロパティ](/help/sites-cloud/authoring/sites-console/page-properties.md)  — ページのプロパティウィンドウを開きます。
* [ロック](/help/sites-cloud/authoring/sites-console/managing-pages.md#locking-a-page)  — 他のユーザーがページを変更できないようにページをロックします
* [コピー](/help/sites-cloud/authoring/sites-console/managing-pages.md#copying-and-pasting-a-page)  — ページをコピーする
* [移動](/help/sites-cloud/authoring/sites-console/managing-pages.md#moving-or-renaming-a-page)  — ページの移動または名前変更
* [クイック公開](/help/sites-cloud/authoring/sites-console/publishing-pages.md#quick-publish)  — ページを直ちに公開する
* [公開を管理](/help/sites-cloud/authoring/sites-console/publishing-pages.md#manage-publication) - 1 つ以上のページを公開するようにスケジュールを設定する
* [復元](/help/sites-cloud/authoring/sites-console/page-versions.md#restore-version)  — ページまたはページツリーのバージョンを復元します
* [削除](/help/sites-cloud/authoring/sites-console/managing-pages.md#deleting-a-page)  — ページまたはページの削除

一部のウィンドウではスペースが制限されるので、使用可能なスペースよりもツールバーのほうが長くなることがよくあります。この場合は、追加のオプションが表示されます。省略記号 (3 つのドットまたは **...**) をクリックすると、その他のすべてのアクションを含むドロップダウンセレクターが開きます。

![その他のオプション](assets/sites-console-additional-options.png)

### アクションを作成 {#create-action}

「作成」アクションでは、新しいページや類似した項目を作成するためのツールバー作成ボタンと同様のオプションを使用できます。

また、ページ関連のアクションを作成する機能も提供します。

* [ワークフロー](/help/sites-cloud/authoring/workflows/overview.md)  — ページへのワークフローの適用
* [バージョン](/help/sites-cloud/authoring/sites-console/page-versions.md)  — ページのバージョンを作成します

## テンプレート

[列表示](/help/sites-cloud/authoring/basic-handling.md#column-view)または[リスト表示](/help/sites-cloud/authoring/basic-handling.md#list-view)でページを選択するときに、ページが基にしているテンプレートを簡単に確認できます。
