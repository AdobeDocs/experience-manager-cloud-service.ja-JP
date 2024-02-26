---
title: サイトコンソールのサイドパネル
description: AEMサイトコンソールのサイドパネルを使用して、コンテンツをより深く理解し、ナビゲートする方法を説明します。
source-git-commit: bbd845079cb688dc3e62e2cf6b1a63c49a92f6b4
workflow-type: tm+mt
source-wordcount: '827'
ht-degree: 26%

---


# サイトコンソールのサイドパネル {#side-panel}

AEMのサイドパネルの使用方法を説明します。 **Sites** コンソールを使用して、コンテンツをより深く理解し、ナビゲートします。

## 向き {#orientation}

サイドパネルは、 **Sites** コンソール。 この方法では、画面はコンテンツ専用です。

をタップまたはクリックします。 **サイドパネル** アイコン **Sites** コンソールツールバーを使用してサイドパネルをアクティブにし、コンテンツの表示を選択します。

* [コンテンツのみ](#content-only)
* [コンテンツツリー](#content-tree)
* [タイムライン](#timeline)
* [参照](#references)
* [サイト](#site)
* [フィルター](#filter)
* [Analytics を設定](#setup-analytics)

![サイトコンソールのサイドパネル表示](assets/sites-console-side-panel-views.png)

選択した現在のビューはドロップダウンで青いチェックマークで示され、ツールバーのサイドパネルアイコンが選択したビューの名前で更新されます。

## コンテンツのみ {#content-only}

このサイドパネルの表示は、効果的にオフになっています。つまり、サイトのコンテンツのみが表示されます。

>[!TIP]
>
>抑音符付き/逆目盛りを使用 `´` サイドパネルのコンテンツのみの表示に切り替えるキーボードショートカット。

## コンテンツツリー {#content-tree}

サイドパネルのこの表示では、コンテンツがツリー階層で表示されます。 コンテンツツリーを使用すると、サイドパネル内のサイト階層をすばやく移動して、現在のフォルダー内のページに関する多くの情報を表示できます。

![サイドパネルのコンテンツツリー表示](assets/console-side-panel-content-tree.png)

ツリー内の項目の横にある右向きの山形記号は、ノードを展開して子を表示できることを示します。 山形をタップまたはクリックすると、子が表示されます。

コンソールには、コンテンツツリーで現在選択されている項目のコンテンツが表示されます。

コンテンツツリーサイドパネルをリストビューやカードビューと組み合わせて使用すると、プロジェクトの階層構造を簡単に確認し、コンテンツツリーサイドパネルを使用してコンテンツ構造全体を容易に移動し、詳細なページ情報をリストビューで表示できます。

>[!TIP]
>
>* 以下を使用します。 `Alt+1` サイドパネルのコンテンツツリー表示に切り替えるキーボードショートカット。
>* 階層表示のエントリを選択すると、矢印キーを使用して階層をすばやく移動できます。
>* 詳しくは、[キーボードショートカット](/help/sites-cloud/authoring/sites-console/keyboard-shortcuts.md)を参照してください。

## タイムライン {#timeline}

タイムラインを使用して、選択したリソースに影響を与えたイベントを表示できます。 また、ワークフローやバージョンなどの特定のイベントを開始する場合にも使用できます。

![タイムラインの詳細](/help/sites-cloud/authoring/assets/timeline-detail.png)

The **タイムライン** サイドパネルでは、選択したアイテムに関連する様々なイベントをドロップダウンリストからタイプとして選択できます。

* コメント
* [注釈](/help/sites-cloud/authoring/page-editor/annotations.md)
* [アクティビティ](/help/sites-cloud/authoring/personalization/activities.md)
* [ローンチ](/help/sites-cloud/authoring/launches/overview.md)
* [バージョン](/help/sites-cloud/authoring/sites-console/page-versions.md)
* [ワークフロー](/help/sites-cloud/authoring/workflows/overview.md)
   * 履歴情報が保存されないので、一時的なワークフローに関する情報は表示されません。<!--With the exception of [transient workflows](/help/sites-developing/workflows.md#transient-workflows) as no history information is saved for these-->
* すべて表示

また、選択した項目に関するコメントを追加または表示するには、 **コメント** 」ボックスが表示されます。 コメントを入力してから `Return` コメントを登録します。 「**コメント**」または「**すべてを表示**」が選択されている場合に表示されます。

Adobe Analytics の **Sites** コンソールでは、「 **コメント** フィールドに入力します。

* [バージョンの保存](/help/sites-cloud/authoring/sites-console/page-versions.md)
* [ワークフローを開始](/help/sites-cloud/authoring/workflows/applying.md)

![サイトコンソールのコメントフィールド](assets/sites-console-comment-ellipsis.png)

>[!TIP]
>
>* 以下を使用します。 `Alt+2` サイドパネルのタイムライン表示に切り替えるキーボードショートカット。
>* 詳しくは、[キーボードショートカット](/help/sites-cloud/authoring/sites-console/keyboard-shortcuts.md)を参照してください。

## 参照 {#references}

The **参照** ビューには、コンソールで選択したリソースに対する参照タイプのリスト、またはコンソールで選択したリソースに対する参照タイプのリストが表示されます。

![参照の詳細](assets/console-side-panel-references-detail.png)

適切な参照タイプを選択すると、詳細情報が表示されます。状況によっては、特定の参照を選択すると、次のような追加のアクションが使用可能です。

* **被リンク**&#x200B;は、当該ページを参照するページのリストと、特定のリンクを選択したときにそれらのページのいずれかを&#x200B;**編集**&#x200B;できる直接アクセスを提供します。
   * この場合は、静的リンクのみが表示され、リストコンポーネントからのように動的に生成されるリンクは表示されません。
* [ローンチ](/help/sites-cloud/authoring/launches/overview.md)（関連するローンチへのアクセスを提供）
* [ライブコピー](/help/sites-cloud/administering/msm/overview.md)（選択したリソースに基づくすべてのライブコピーのパスを表示）
* [ブループリント](/help/sites-cloud/administering/msm/best-practices.md)（詳細と各種アクションを提供）
* [言語コピー](/help/sites-cloud/administering/translation/managing-projects.md#creating-translation-projects-using-the-references-panel)（詳細と各種アクションを提供）

## サイト {#site}

The **サイト** サイドパネルの表示には、サイトの詳細が表示されます [サイトテンプレートを使用して作成された。](/help/sites-cloud/administering/site-creation/create-site.md)

![サイトパネル](assets/console-side-panel-site-paenl.png)

ドキュメントを見る [サイトパネルを使用したサイトテーマの管理](/help/sites-cloud/administering/site-creation/site-rail.md) パネルを使用して [サイトのテーマ。](/help/sites-cloud/administering/site-creation/site-themes.md).

テーマベースのサイトの作成を有効にするフロントエンドパイプラインをまだ設定していない場合、サイドパネルにはそのオプションが表示されます。

![サイドパネルでフロントエンドパイプラインを有効にするオプション](assets/sites-console-side-panel-site.png)

>[!TIP]
>
>テンプレートからサイトを作成し、そのテーマをカスタマイズするプロセスに関するエンドツーエンドの説明については、 [クイックサイト作成ジャーニー](/help/journey-sites/quick-site/overview.md) を参照してください。

## フィルター {#filter}

The **フィルター** パネルは、 [検索機能](/help/sites-cloud/authoring/search.md) 適切な場所のフィルターが既に設定されているので、表示するコンテンツをさらにフィルターできます。

![フィルターの例](assets/console-side-panel-filter.png)

サイドパネルの他のビューとは異なり、別のビューに切り替えるには、 `X` 」と入力します。

## Analytics を設定 {#setup-analytics}

このビューを使用すると、選択したサイトに対してAdobe Analyticsをすばやく設定できます。

![Analytics を設定](assets/sites-console-side-panel-setup-analytics.png)
