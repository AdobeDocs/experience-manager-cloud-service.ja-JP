---
title: '[!DNL Assets view] ユーザーインターフェイス'
description: ' [!DNL Assets view] のユーザーインターフェイスとナビゲーションについて説明します。'
role: User
exl-id: 1e71ea7d-fee7-4ed0-bb80-d537b57fc823
feature: Asset Management, Publishing, Collaboration, Asset Processing
source-git-commit: 79213bcfe5c5ccf7c60a31e6cb757f60a0ba87a7
workflow-type: tm+mt
source-wordcount: '0'
ht-degree: 0%

---

# ファイルおよびフォルダーへの移動とアセットの表示 {#view-assets-and-details}

<!-- TBD: Give screenshots of all views with many assets. Zoom out to showcase how the thumbnails/tiles flow on the UI in different views. -->

<!-- TBD: The options in left sidebar may change. Shared with me and Shared by me are missing for now. Update this section as UI is updated. -->

## [!DNL Assets view] ユーザーインターフェイスについて  {#understand-interface-navigation}

[!DNL Assets view] は、直観的で使いやすいユーザーインターフェイスを提供しています。すっきりしたインターフェイスのおかげで、アセットや関連情報を見つけやすく覚えやすくなります。

[!DNL Assets view] にログインすると、次のインターフェイスが表示されます。

![[!DNL Assets view] ユーザーインターフェイス](assets/assets-view-interface.png)

 **A**：左側のサイドバーでリポジトリを参照し、他のいくつかのオプションにアクセスできます **B**：左側のサイドバーを表示または折りたたむと、アセットの表示領域が広がります **C**：検索結果をフィルタリングします **D**：選択したフォルダーのすべてのコンテンツを選択します **E**：アセットを並べ替えるオプション **F**：検索ボックス **G**：`Add Assets` ボタンを使用してファイルをアップロードまたはドラッグ＆ドロップします **H**：新しいフォルダーを作成します **I**：異なるビューを切り替えます

<!-- TBD: Need an embedded video here with narration. It has to be hosted on MPC to be embeddable. -->

## アセットとフォルダーの参照と表示 {#browse-repository}

メインユーザーインターフェイスまたは左側のサイドバーからフォルダーを参照できます。Experience Manager Assets で、コンテンツを参照または検索する際に、フォルダーのサムネールにフォルダーのコンテンツの視覚的なプレビューが表示されます。これにより、AEM Assets リポジトリ内で使用可能なアセットの検出性が向上します。このフォルダーのサムネールを確認することで、AEM Assets リポジトリのフォルダー内の特定のアセットの検索にかかる時間を節約できます。
フォルダー内のアセットの参照時には、このインターフェイスを使用してアセットのサムネールを表示し、リポジトリを視覚的に参照したり、アセットの詳細を表示して目的のアセットをすばやく見つけたりできます。左側のサイドバーで使用できるオプションは次のとおりです。

* [マイワークスペース](/help/assets/my-workspace-assets-view.md)：Assets には、ウィジェットを提供するカスタマイズ可能なワークスペースが含まれるようになりました。このワークスペースは、Assets ユーザーインターフェイスの主要な領域と、最も関連性の高い情報に簡単にアクセスできます。このページは、作業項目の概要を示し、主要なワークフローにすばやくアクセスできるワンストップソリューションとして機能します。これらのオプションにより簡単にアクセスできるので、効率とコンテンツ速度が向上します。
* [タスク](/help/assets/my-workspace-assets-view.md)：自分に割り当てられたタスクは、「**マイタスク**」タブで確認できます。一方、自分が作成したタスクは、「**割り当てられたタスク**」タブで表示できます。また、完了したタスクは、「**完了済みタスク**」タブにあります。
* [アセット](/help/assets/manage-organize-assets-view.md)：アクセス可能なすべてのフォルダーのリストがツリー表示されます。
* **最近表示された項目**：最近プレビューしたアセットのリスト。[!DNL Assets view] は、プレビューしたアセットのみを表示します。リポジトリーファイルまたはフォルダーを参照する際にスクロールして通過したアセットは表示されません。
* [コレクション](/help/assets/manage-collections-assets-view.md)：コレクションとは、Adobe Experience Manager アセットビュー内のアセット、フォルダーまたはその他のコレクションのセットです。コレクションを使用して、ユーザー間でアセットを共有します。フォルダーとは異なり、1 つのコレクションに異なる複数の場所のアセットを含めることができます。1 人のユーザーと複数のコレクションを共有できます。各コレクションには、アセットへの参照が含まれます。アセットの参照整合性はコレクション間で維持されます。

<!--

* [Insights](/help/assets/manage-reports-assets-view.md#view-live-statistics): In [!DNL Assets view], you can view real-time insights on your dashboard. Assets view enables you to view real-time data for your Assets view environment with the Insights dashboard. You can view real-time event metrics during the last 30 days or for the last 12 months. 

-->
* **ごみ箱**：ルートの **[!UICONTROL Assets]** フォルダーから削除されたアセットをリストします。ごみ箱フォルダー内のアセットを選択して、元の場所に復元したり、完全に削除したりできます。キーワードの指定、アセットステータス、ファイルタイプ、MIME タイプ、画像サイズ、アセットの作成、変更、有効期限などのフィルターの適用を行えるほか、現在のユーザーが破棄したアセットによるフィルタリングを適用できます。また、カスタムフィルターを適用して、ごみ箱フォルダー内の適切なアセットを検索することもできます。標準フィルターとカスタムフィルターの使用について詳しくは、[アセットビューでのアセットを検索する](/help/assets/search-assets-view.md)方法を参照してください。
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

![アセットをプレビュー](/help/assets/assets/navigate-file-folder-dm.png)

**A**：リポジトリ内の現在のフォルダーまたは現在の検索結果に戻ります **B**：プレビューしているファイルの名前と形式 **C**：タスクを割り当てます **D**：高度なメタデータ **E**：キーワードとスマートタグ **F**：コメントと注釈 **G**：選択したアセットに関連するタスクを表示します **H**：[バージョンを表示および管理します](/help/assets/manage-organize-assets-view.md#versions-of-assets) **I**：画像のレンディションを表示します **J**：画像を編集します **K**：スマート切り抜きレンディションと OpenAPI 機能を備えた Dynamic Media レンディションを含む Dynamic Media レンディションを表示します。**L**：基本メタデータ **M**：高度なメタデータ **N**：キーワードとスマートタグ **O**：フォルダーに戻ることなく、現在のフォルダー内の前または次のアセットに進みます **P**：より詳細にプレビューします。ズーム、全画面表示、その他のオプション。

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

* [カスタマーケア](https://experienceleague.adobe.com/ja?support-solution=General#support)に問い合わせる

>[!MORELIKETHIS]
>
>* [アセットのバージョンの表示](/help/assets/manage-organize-assets-view.md#view-versions)
