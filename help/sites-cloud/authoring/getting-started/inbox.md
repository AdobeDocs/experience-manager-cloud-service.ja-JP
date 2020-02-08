---
title: インボックス
description: インボックスを使用したタスクの管理
translation-type: tm+mt
source-git-commit: 16725342c1a14231025bbc1bafb4c97f0d7cfce8

---


# インボックス {#your-inbox}

ワークフローやプロジェクトなど、AEMの様々な領域から通知を受け取ることができます。 例えば、次の通知を受け取ることができます。

* タスク：
   * These can also be created at various points within the AEM UI, for example, under **Projects**.
   * These can be the product of a workflow **Create Task** or **Create Project Task** step.
* ワークフロー：
   * ページコンテンツに対して実行する必要があるアクションを表す作業項目
      * These are the product of workflow **Participant** steps.
   * 管理者が失敗したステップを再試行できる失敗項目

これらの通知は、自分のインボックスで受け取り、それらを表示して対処できます。

>[!NOTE]
>
>項目タイプについて詳しくは、次の項目も参照してください。
>
>* [プロジェクト](/help/sites-cloud/authoring/projects/overview.md)
>* [プロジェクト - タスクの操作](/help/sites-cloud/authoring/projects/tasks.md)
>* [ワークフロー](/help/sites-cloud/authoring/workflows/overview.md)


## ヘッダーのインボックス {#inbox-in-the-header}

すべてのコンソールでインボックスの現在の項目数がヘッダーに表示されます。また、インジケーターを開いて、アクションが必要なページに簡単にアクセスしたり、インボックスにアクセスしたりすることもできます。

![ヘッダーのインボックスの概要](/help/sites-cloud/authoring/assets/inbox-header.png)

>[!NOTE]
>
>特定のアクションは、[適切なリソースのカード表示](/help/sites-cloud/authoring/getting-started/basic-handling.md#card-view)にも表示されます。

## インボックスを開く {#opening-the-inbox}

AEM 通知インボックスを開くには：

1. ツールバーのインジケーターをクリックまたはタップします。

1. 「**すべて表示**」を選択します。**AEM インボックス**&#x200B;が開きます。インボックスには、ワークフロー、プロジェクトおよびタスクの項目が表示されます。
1. デフォルトの表示は[リスト表示](#inbox-list-view)ですが、[カレンダー表示](#inbox-calendar-view)に切り替えることもできます。これは、表示セレクター（ツールバーの右上部分）を使用しておこないます。

   For both views you can also define [View Settings](#inbox-view-settings). The options available are dependent on the current view.

   ![インボックス表示の設定](/help/sites-cloud/authoring/assets/inbox-view-settings.png)

>[!NOTE]
>
>The Inbox operates as a console, so use [Global Navigation](/help/sites-cloud/authoring/getting-started/basic-handling.md#global-navigation) or [Search](/help/sites-cloud/authoring/getting-started/search.md) to navigate to another location when you are finished.

### インボックス - リスト表示 {#inbox-list-view}

このビューには、すべての項目と関連情報が一覧表示されます。

![インボックスリスト表示](/help/sites-cloud/authoring/assets/inbox-list-view.png)

### インボックス - カレンダー表示 {#inbox-calendar-view}

このビューでは、カレンダー内のアイテムの位置に従ってアイテムが表示されます。

![受信トレイのカレンダー表示](/help/sites-cloud/authoring/assets/inbox-calendar-view.png)

以下の操作を実行できます。

* Select a specific view: **Timeline**, **Column**, **List**
* Specify the tasks to display according to **Schedule**: **All**, **Planned**, **In Progress**, **Due Soon**, **Past Due**
* 品目の詳細情報のドリルダウン
* 日付範囲を選択してビューにフォーカスします。

![受信トレイカレンダーの表示日付範囲](/help/sites-cloud/authoring/assets/inbox-calendar-range.png)

### インボックス - 表示設定 {#inbox-view-settings}

両方の表示（リストとカレンダー）について、設定を定義できます。

* **カレンダー表示**

   **カレンダー表示**&#x200B;の場合は、次の項目を設定できます。

   * **グループ化の条件**
   * **予定**&#x200B;または&#x200B;**なし**
   * **カードサイズ**
   ![インボックスのカレンダー表示の設定](/help/sites-cloud/authoring/assets/inbox-calendar-settings.png)

* **リスト表示**

   **リスト表示**&#x200B;の場合は、並べ替えメカニズムを設定できます。

   * **並べ替えの基準**
   * **並べ替え順序**
   ![インボックスリスト表示の設定](/help/sites-cloud/authoring/assets/inbox-list-settings.png)

   カレンダーを他のユーザーに委任したり、他のユーザーに委任を依頼したり、委任を管理したりすることもできます。

   ![インボックスリスト表示の委任設定](/help/sites-cloud/authoring/assets/inbox-delegation.png)

## 項目に対するアクションの実行 {#taking-action-on-an-item}

1. 項目に対してアクションを実行するには、該当する項目のサムネイルを選択します。その項目に適用可能なアクションのアイコンがツールバーに表示されます。

   ![受信トレイ項目の選択](/help/sites-cloud/authoring/assets/inbox-select-item.png)

   アクションは項目に対応しており、次のアクションがあります。

   * **完了アクション**
   * **項目の** 委任
   * **アイテムを開く** （アイテムのタイプに応じて、このアクションで実行できる操作は次のとおりです）。

      * 項目のプロパティを表示
      * 適切なダッシュボードまたはウィザードを開いて、その他のアクションを実行します
      * 関連ドキュメントを開く
   * **前のステップ** に戻る
   * ワークフローのペイロードの表示
   * アイテムからプロジェクトを作成する
   >[!NOTE]
   >
   >詳しくは、次の節を参照してください。
   >
   >* ワークフローの項目 - [ワークフローへの参加](/help/sites-cloud/authoring/workflows/participating.md)


1. 選択した項目に応じて、次のようにアクションが開始されます。

   * アクションに適したダイアログが開きます
   * アクションウィザードが起動します
   * ドキュメントページが開きます
   For example, **Delegate** will open a dialog:

   ![受信トレイの委任タスク](/help/sites-cloud/authoring/assets/inbox-assign-task.png)

   ダイアログ、ウィザード、ドキュメントページが開いているかどうかに応じて、次の操作をおこなうことができます。

   * 適切なアクション（再割り当てなど）を確認します。
   * アクションのキャンセル
   * [戻る]矢印を選択してインボックスに戻ります。例えば、アクションウィザードやドキュメントページが開いている場合は、[インボックス]に戻ることができます。


## タスクの作成 {#creating-a-task}

インボックスからタスクを作成できます。

1. 「**作成**」、「**タスク**」の順に選択します。
1. Complete the necessary fields in the **Basic** and **Advanced** tabs (only the **Title** is mandatory, all others are optional):

   * **基本**:

      * **タイトル**
      * **プロジェクト**
      * **割り当て先**
      * **コンテンツ**（ペイロードと同様）は、タスクからリポジトリ内の場所への参照です
      * **説明**
      * **タスクの優先度**
      * **開始日**
      * **期限**
   ![受信トレイのタスクの追加](/help/sites-cloud/authoring/assets/inbox-create-task.png)

   * **アドバンス**

      * **名前**:URLを形成するために使用され、空白の場合はタイトルに基づき **ます**。
   ![インボックス追加タスクの詳細オプション](/help/sites-cloud/authoring/assets/inbox-add-task-advanced.png)

1. 「**送信**」を選択します。

## プロジェクトの作成 {#creating-a-project}

特定のタスクでは、そのタスクに基づいて[プロジェクト](/help/sites-cloud/authoring/projects/overview.md)を作成できます。

1. サムネイルをタップまたはクリックして、適切なタスクを選択します。

   >[!NOTE]
   >
   >Only tasks created using the **Create** option of the **Inbox** can be used to create a project.
   >
   >（ワークフローの）作業項目を使用してプロジェクトを作成することはできません。

1. ツールバーの「**プロジェクトを作成**」を選択してウィザードを開きます。
1. 適切なテンプレートを選択して、「**次へ**」を選択します。
1. 必要なプロパティを指定します。

   * **基本**

      * **タイトル**
      * **説明**
      * **開始日**
      * **期限**
      * **ユーザー**&#x200B;と役割
   * **アドバンス**

      * **名前**
   >[!NOTE]
   >
   >詳しくは、[プロジェクトの作成](/help/sites-cloud/authoring/projects/managing.md#creating-a-project)を参照してください。

1. 「**作成**」を選択してアクションを確定します。

## AEM インボックス内の項目のフィルター処理 {#filtering-items-in-the-aem-inbox}

リスト内の項目をフィルター処理できます。

1. **AEM インボックス**&#x200B;を開きます。

1. フィルターセレクターを開きます。

   ![インボックス検索](/help/sites-cloud/authoring/assets/inbox-search.png)

1. 条件の範囲に従ってリストに表示された項目をフィルタリングでき、その多くを絞り込むことができます。例：

   ![インボックス検索フィルター](/help/sites-cloud/authoring/assets/inbox-search-filter.png)

   >[!NOTE]
   >
   >「[設定を表示](#inbox-view-settings)」では、[リスト表示](#inbox-list-view)を使用するときの並べ替え順を設定することもできます。
