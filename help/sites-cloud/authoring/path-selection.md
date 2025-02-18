---
title: パスブラウザーを使用したパスの選択
description: パスブラウザーを使用して AEM でリソースを選択する方法について説明します。
exl-id: 8eb52793-b709-4e66-832d-533ef06bc0e1
solution: Experience Manager Sites
feature: Authoring
role: User
source-git-commit: 10580c1b045c86d76ab2b871ca3c0b7de6683044
workflow-type: ht
source-wordcount: '322'
ht-degree: 100%

---

# パスの選択 {#path-selection}

オーサリング時に、別のリソースを選択する必要がある場合がよくあります（別のページへのリンクを定義する場合、画像を選択する場合など）。パスの選択を簡単にするために、[パスフィールド](#path-fields)にはオートコンプリート機能があり、[パスブラウザー](#path-browser)ではより堅牢な選択が可能になっています。

## パスフィールド {#path-fields}

説明のためにここで使用する例は、画像コンポーネントです。コンポーネントの使用および編集について詳しくは、[ページオーサリング用コンポーネント](/help/sites-cloud/authoring/page-editor/components.md)を参照してください。

パスフィールドには、オートコンプリート機能とルックアヘッド機能があり、リソースを見つけやすくなっています。

パスフィールドで「**選択ダイアログを開く**」ボタンをクリックすると、[パスブラウザー](#path-browser)ダイアログが開き、より詳細な選択オプションが表示されます。

![「選択ダイアログを開く」ボタン](assets/path-selection-open-selection-dialog.png)

または、パスフィールドで入力を開始すると、入力した内容と一致するパスが表示されます。

![「選択ダイアログを開く」ボタン](assets/path-selection-open-selection-dialog.png)

## パスブラウザー {#path-browser}

パスブラウザーは、[**Sites** コンソール](/help/sites-cloud/authoring/sites-console/introduction.md)の[列表示](/help/sites-cloud/authoring/basic-handling.md#column-view)のように整理されており、リソースをより詳細に選択できます。

![パスブラウザー](/help/sites-cloud/authoring/assets/path-browser.png)

* リソースを選択すると、ダイアログボックスの右上にある「**選択**」ボタンがアクティブになります。
   * 選択して選択内容を確定するか、「**キャンセル**」を選択して中止します。
* コンテキストで複数のリソースを選択できる場合、リソースを選択すると「**選択**」ボタンがアクティブ化され、選択したリソースの数がウィンドウの右上に表示されます。
   * すべての選択を解除するには、数字の横にある **X** をクリックします。
* ツリー内を移動すると、ダイアログ上部のパンくずリストに現在の場所が反映されます。
   * これらのパンくずリストを使用すると、リソース階層内で素早くジャンプすることもできます。
* ダイアログボックスの上部にある検索フィールドは、いつでも使用できます。
   * 検索フィールドの「**X**」をクリックして、検索をクリアします。
* 検索を絞り込むには、フィルターオプションを表示して、特定のパスに基づいて結果をフィルターできます。

![フィルターオプション](assets/path-selection-filters.png)
