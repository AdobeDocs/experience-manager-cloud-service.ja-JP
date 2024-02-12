---
title: 「[!DNL Assets view] ユーザーインターフェイス」
description: ' [!DNL Assets view] のユーザーインターフェイスとナビゲーションについて説明します。'
role: User
exl-id: 534a8084-88f7-410e-b872-719e47e62b10
source-git-commit: 39166f59eb773a149ba28be2b34d0c1aa6c831b4
workflow-type: tm+mt
source-wordcount: '912'
ht-degree: 72%

---

# ファイルおよびフォルダーへの移動とアセットの表示 {#view-assets-and-details}

<!-- TBD: Give screenshots of all views with many assets. Zoom out to showcase how the thumbnails/tiles flow on the UI in different views. -->

<!-- TBD: The options in left sidebar may change. Shared with me and Shared by me are missing for now. Update this section as UI is updated. -->

## [!DNL Assets view] ユーザーインターフェイスについて  {#understand-interface-navigation}

[!DNL Assets view] は、直観的で使いやすいユーザーインターフェイスを提供しています。すっきりしたインターフェイスのおかげで、アセットや関連情報を見つけやすく覚えやすくなります。

[!DNL Assets view] にログインすると、次のインターフェイスが表示されます。

![[!DNL Assets view] ユーザーインターフェイス](assets/assets-view-interface.png)

**A**：左側のサイドバーでリポジトリーを参照し、その他のオプションにアクセスできます。 **B**：左側のサイドバーを表示または折りたたんで、アセット表示領域を拡大します **C**：検索結果のフィルタリング **D**：選択したフォルダーのすべてのコンテンツを選択します **E**：アセットを並べ替えるオプション **金**：検索ボックス **G**：を使用して、ファイルをアップロードまたはドラッグ&amp;ドロップします `Add Assets` ボタン **H**：新しいフォルダーを作成します **I**：別のビューに切り替えます。

<!-- TBD: Need an embedded video here with narration. It has to be hosted on MPC to be embeddable. -->

## アセットとフォルダーの参照と表示 {#browse-repository}

メインユーザーインターフェイスまたは左側のサイドバーからフォルダーを参照できます。参照時には、このインターフェイスを使用してアセットのサムネールを表示し、リポジトリーを視覚的に参照したり、アセットの詳細を表示して目的のアセットをすばやく見つけたりできます。左側のサイドバーで使用できるオプションは次のとおりです。

* [マイワークスペース](/help/assets/my-workspace-assets-view.md)：Assets には、ウィジェットを提供するカスタマイズ可能なワークスペースが含まれるようになりました。このワークスペースは、Assets ユーザーインターフェイスの主要な領域と、最も関連性の高い情報に簡単にアクセスできます。このページは、作業項目の概要を示し、主要なワークフローにすばやくアクセスできるワンストップソリューションとして機能します。これらのオプションにより簡単にアクセスできるので、効率とコンテンツ速度が向上します。
* [タスク](/help/assets/my-workspace-assets-view.md)：自分に割り当てられたタスクは、「**マイタスク**」タブで確認できます。一方、自分が作成したタスクは、「**割り当てられたタスク**」タブで表示できます。また、完了したタスクは、「**完了済みタスク**」タブにあります。
* [アセット](/help/assets/manage-organize-assets-view.md)：アクセス可能なすべてのフォルダーのリストがツリー表示されます。
* **最近表示された項目**：最近プレビューしたアセットのリスト。[!DNL Assets view] は、プレビューしたアセットのみを表示します。リポジトリーファイルまたはフォルダーを参照する際にスクロールして通過したアセットは表示されません。
* [コレクション](/help/assets/manage-collections-assets-view.md)：コレクションとは、Adobe Experience Manager アセットビュー内のアセット、フォルダーまたはその他のコレクションのセットです。コレクションを使用して、ユーザー間でアセットを共有します。フォルダーとは異なり、1 つのコレクションに異なる複数の場所のアセットを含めることができます。1 人のユーザーと複数のコレクションを共有できます。各コレクションには、アセットへの参照が含まれます。アセットの参照整合性はコレクション間で維持されます。

* [インサイト](/help/assets/manage-reports-assets-view.md#view-live-statistics)：[!DNL Assets view] では、ダッシュボードでリアルタイムのインサイトを表示できます。アセットビューを使用すると、アセットビュー環境のリアルタイムデータをインサイトダッシュボードで表示できます。過去 30 日間または過去 12 か月間のリアルタイムイベント指標を表示できます。
* **ごみ箱**：ルートの **[!UICONTROL Assets]** フォルダーから削除されたアセットをリストします。ごみ箱フォルダ内のアセットを選択して、元の場所に復元したり、完全に削除したりできます。 キーワードを指定したり、アセットのステータス、ファイルタイプ、MIME タイプ、画像サイズ、アセットの作成、変更、有効期限などのフィルターを適用したり、現在のユーザーが破棄したアセットでフィルタリングしたりできます。 また、カスタムフィルターを適用して、ごみ箱フォルダ内の適切なアセットを検索することもできます。 標準フィルターとカスタムフィルターの使用について詳しくは、 [Assets ビューでのアセットの検索](/help/assets/search-assets-view.md).
* **設定**：メタデータフォーム、レポート、分類管理など、**設定**&#x200B;を使用してアセットビューの様々なオプションを設定できます。

<!-- TBD: Not sure if we want to publish these right now. CC Libs are beta as per Greg.
* **Libraries**: Access to [!DNL Adobe Creative Cloud Team] (CCT) Libraries view. This view is visible only if the user is entitled to CCT Libraries.
-->

<!-- TBD: My Work Space shows task inbox and it is not visible on AEM Cloud Demos as of now. It is the source of truth server hence not documenting My Work Space option for now.
-->

左側のサイドバーを開いたり折りたたんだりして、使用可能なアセット表示領域を広げることができます。

[!DNL Assets view] では、アセット、フォルダーおよび検索結果を 4 種類のレイアウトで表示できます。

* ![リスト表示アイコン](assets/do-not-localize/list-view.png) [!UICONTROL リスト表示]
* ![グリッド表示アイコン](assets/do-not-localize/grid-view.png) [!UICONTROL グリッド表示]
* ![ギャラリー表示アイコン](assets/do-not-localize/gallery-view.png) [!UICONTROL ギャラリー表示]
* ![ウォーターフォール表示アイコン](assets/do-not-localize/waterfall-view.png) [!UICONTROL ウォーターフォール表示]

アセットを見つけるには、`Name`、`Relevancy`、`Size`、`Modified` および `Created` の昇順または降順にアセットを並べ替えます。

フォルダー内に移動するには、フォルダーのサムネールをダブルクリックするか、左側のサイドバーからフォルダーを選択します。フォルダーの詳細を表示するには、フォルダーを選択し、上部のツールバーで「詳細」をクリックします。階層を上下に移動するには、左側のサイドバーを使用するか、上部のパンくずリストを使用します。

![フォルダーの参照](assets/browsing-folders.png)

*図：階層を参照するには上部のパンくずリストまたは左側のサイドバー使用*

## アセットのプレビュー {#preview-assets}

アセットを使用、共有またはダウンロードする前に、より詳細に表示できます。プレビュー機能を使用すると、画像だけでなく、サポートされているその他のアセットタイプも表示できます。

アセットをプレビューするには、目的のアセットを選択し、上部のツールバーで[!UICONTROL 詳細]アイコン（![詳細アイコン](assets/do-not-localize/edit-in-icon.png)）をクリックします。アセットを表示できるだけでなく、詳細なメタデータを表示したり、その他のアクションを実行したりできます。

![アセットをプレビュー](assets/preview-asset-2.png)

**A**：現在のフォルダーに戻るか、リポジトリ内の現在の検索結果に戻ります。 **B**：プレビューしているファイルの名前と形式 **C**：タスクの割り当て **D**：高度なメタデータ **E**：キーワードとスマートタグ **金**：コメントと注釈 **G**：選択したアセットに関連するタスクを表示します **H**：バージョンを表示および管理します **I**：画像のレンディションの表示 **J**：画像を編集 **K**：基本メタデータ **L**：高度なメタデータ **M**：キーワードとスマートタグ **N**：より詳細にプレビューします。 ズーム、フルスクリーン、その他のオプション **O**：フォルダーに戻らずに、現在のフォルダー内の前または次のアセットに進みます。

また、ビデオをプレビューすることもできます。

![ビデオのプレビュー](assets/preview-video.png)

アセットを明示的にプレビューすると、[!DNL Assets view] には最近表示したアセットとして表示されます。

<!-- TBD: Describe the options.

Explicitly previewed assets are displayed as recently viewed assets. Give screenshot of this.
Other use cases after previewing.
-->

## 次の手順 {#next-steps}

* アセットビューユーザーインターフェイスの「[!UICONTROL フィードバック]」オプションを使用して、製品に関するフィードバックを提供する

* 右側のサイドバーにある「[!UICONTROL このページを編集]」（![ページを編集](assets/do-not-localize/edit-page.png)）または「[!UICONTROL 問題を記録] 」（![GitHub イシューを作成](assets/do-not-localize/github-issue.png)）を使用してドキュメントに関するフィードバックを提供する

* [カスタマーケア](https://experienceleague.adobe.com/?support-solution=General&amp;lang=ja#support)に問い合わせる

>[!MORELIKETHIS]
>
>* [アセットのバージョンの表示](/help/assets/manage-organize-assets-view.md#view-versions)
