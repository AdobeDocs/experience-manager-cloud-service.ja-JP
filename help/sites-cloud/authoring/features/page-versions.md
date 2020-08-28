---
title: ページバージョンの処理
description: ページのバージョンを作成、比較および復元します
translation-type: tm+mt
source-git-commit: 87da152f21abe379d70e0a8d04f3155901f013dd
workflow-type: tm+mt
source-wordcount: '1510'
ht-degree: 67%

---


# ページバージョンの処理 {#working-with-page-versions}

バージョン管理では、特定の時点でのページの「スナップショット」が作成されます。バージョン管理を使用すると、以下の操作を実行できます。

* ページのバージョンを作成する。
* 1つ以上のページの以前のバージョンを次の場所に復元：
   * ページに対して行った変更を元に戻します。
   * 削除したページを復元します。
   * ツリーを（指定した日時に）復元します。
* バージョンのプレビュー。
* ページの現在のバージョンと以前のバージョンを比較します。
   * テキストと画像の違いがハイライトされます。
* Timewarpは、ページのバージョンを使用して公開環境の状態を決定します。

## 新しいバージョンの作成 {#creating-a-new-version}

リソースのバージョンは、次の場所から作成できます。

* [タイムラインパネル](#creating-a-new-version-timeline)
* 「[作成](#creating-a-new-version-create-with-a-selected-resource)」オプション（リソースが選択されている場合）

### 新しいバージョンの作成 - タイムライン {#creating-a-new-version-timeline}

1. バージョンを作成するページに移動して、そのページを表示します。
1. [選択モード](/help/sites-cloud/authoring/getting-started/basic-handling.md#viewing-and-selecting-resources)でページを選択します。
1. **タイムライン**&#x200B;パネルを開きます。
1. コメントフィールドの横の省略記号をクリックまたはタップして、オプションを表示します。

   ![タイムラインパネルに表示されるバージョン](/help/sites-cloud/authoring/assets/versions-timeline-rail.png)

1. 「**バージョンとして保存**」を選択します。
1. 必要に応じて、「**ラベル**」と「**コメント**」を入力します。

   ![バージョンのラベルの追加](/help/sites-cloud/authoring/assets/versions-add-label.png)

1. 「**作成**」で新しいバージョンを確定します。

   タイムラインの情報が、新しいバージョンを示すように更新されます。

### 新しいバージョンの作成 - 選択したリソースで作成 {#creating-a-new-version-create-with-a-selected-resource}

1. バージョンを作成するページに移動して、そのページを表示します。
1. [選択モード](/help/sites-cloud/authoring/getting-started/basic-handling.md#viewing-and-selecting-resources)でページを選択します。
1. ツールバーの「**作成**」オプションを選択します。
1. 同じダイアログが開きます。必要に応じて、「**ラベル**」と「**コメント**」を入力します。
1. 「**作成**」で新しいバージョンを確定します。

タイムラインが開き、新しいバージョンを示すように情報が更新されます。

## バージョンの復元 {#reinstating-versions}

ページのバージョンを作成した後、以前のバージョンを復元する様々な方法があります。

* タイ **ムラインパネルの「このバージョンに** 戻す [](/help/sites-cloud/authoring/getting-started/basic-handling.md#timeline) 」オプション

   選択したページの以前のバージョンを復元します。

* 上部のアク **ションツールバーの「復元** 」 [オプション](/help/sites-cloud/authoring/getting-started/basic-handling.md#actions-toolbar)

   * **バージョンを復元**

      現在選択されているフォルダー内の指定されたページのバージョンを復元します。これには、以前削除したページの復元も含まれます。

   * **ツリーの復元**

      ツリー全体のバージョンを指定した日時に復元する。これには、以前削除したページが含まれる場合があります。

>[!NOTE]
>
>ページを復元すると、作成されたバージョンは新しいブランチの一部になります。
>
>この処理は次のようになります。
>
>1. 任意のページのバージョンを作成します。
>1. 最初のラベルおよびバージョンノードの名前は 1.0、1.1、1.2 などです。
>1. 最初のバージョンを復元する。例：1.0
>1. 新しいバージョンを再度作成します。
>1. 生成されるラベルおよびノードの名前は 1.0.0、1.0.1、1.0.2 などです。


### Revert to a Version {#revert-to-a-version}

選択したページを **以前のバージョンに戻すには** :

1. 以前のバージョンに戻すページに移動して、そのページを表示します。
1. [選択モード](/help/sites-cloud/authoring/getting-started/basic-handling.md#viewing-and-selecting-resources)でページを選択します。
1. 「**タイムライン**」列を開き、「**すべて表示**」または「**バージョン**」を選択します。選択したページのページバージョンが表示されます。
1. 戻すバージョンを選択します。選択可能なオプションが表示されます。

   ![このバージョンに戻る](/help/sites-cloud/authoring/assets/versions-revert.png)

1. 「**このバージョンに戻る**」を選択します。選択したバージョンが復元され、タイムラインの情報が更新されます。

### バージョンを復元 {#restore-version}

このメソッドは、現在のフォルダー内の指定されたページのバージョンを復元するために使用できます。これには、以前削除したページの復元も含まれます。

1. Navigate to, and [select](/help/sites-cloud/authoring/getting-started/basic-handling.md#viewing-and-selecting-resources), the required folder.

1. 「 **復元**」を選択し、上部の **アクションツールバーで** 「バージョンを復元 [](/help/sites-cloud/authoring/getting-started/basic-handling.md#actions-toolbar)」を選択します。

   >[!NOTE]
   >
   >次の場合：
   >* 子ページを持たない単一のページを選択した場合、
   >* または、フォルダー内のどのページにもバージョンがない場合、

   >
   >この場合、該当するバージョンがないため、表示は空になります。

1. 利用可能なバージョンが表示されます。

   ![バージョンを復元 — フォルダ内のすべてのページのリスト](/help/sites-cloud/authoring/assets/versions-restore-version-01.png)

1. 特定のページに対して、「 **RESTORE TO VERSION** 」のドロップダウンセレクターを使用して、そのページに必要なバージョンを選択します。

   ![Restore Version - Select Version](/help/sites-cloud/authoring/assets/versions-restore-version-02.png)

1. メインディスプレイで、復元する必要のあるページを選択します。

   ![バージョンの復元 — ページの選択](/help/sites-cloud/authoring/assets/versions-restore-version-03.png)

1. 選択したページの選択したバージョンを **現在のバージョンに復元するには** 、「 *Restore* （復元）」を選択します。

>[!NOTE]
>
>必要なページと関連するバージョンを選択する順序は入れ替えが可能です。

### ツリーの復元 {#restore-tree}

このメソッドは、指定した日時に、ツリーのバージョンを復元する場合に使用できます。これには、以前削除したページが含まれる場合があります。

1. Navigate to, and [select](/help/sites-cloud/authoring/getting-started/basic-handling.md#viewing-and-selecting-resources), the required folder.

1. 「 **リストア**」を選択し、トップ・ **アクション・ツールバーから「ツリーのリストア** 」を選択し [](/help/sites-cloud/authoring/getting-started/basic-handling.md#actions-toolbar)ます。 ツリーの最新バージョンが表示されます。

   ![ツリーの復元](/help/sites-cloud/authoring/assets/versions-restore-tree-01.png)

1. 「 **最新バージョンの日付での日付と時刻の選択」を使用して** 、復元するツリーの別のバージョンを選択します。

1. 必要に応じて、「 **保持されたバージョン付きでないページ** 」フラグを設定します。

   * アクティブ（選択）の場合、バージョン管理されていないページはすべて維持され、復元の影響を受けません。

   * 非アクティブ（選択されていない）場合、バージョン管理されていないページは、バージョン管理されたツリーに存在しないので削除されます。

1. 選択したバージョンのツリーを **現在のバージョンとしてリストアする場合は** 、「Restore *」を選択し* ます。

## バージョンのプレビュー {#previewing-a-version}

次の手順で特定のバージョンをプレビューできます。

1. 比較するページに移動して、そのページを表示します。
1. [選択モード](/help/sites-cloud/authoring/getting-started/basic-handling.md#viewing-and-selecting-resources)でページを選択します。
1. 「**タイムライン**」列を開き、「**すべて表示**」または「**バージョン**」を選択します。
1. ページバージョンがリストに表示されます。次のように、プレビューするバージョンを選択します。

   ![バージョンのプレビュー](/help/sites-cloud/authoring/assets/versions-revert.png)

1. **プレビュー**&#x200B;を選択します。ページが新しいタブに表示されます。

   >[!CAUTION]
   >
   >ページを移動すると、移動前に作成したバージョンのプレビューを実行できなくなります。
   >
   >プレビューで問題が発生した場合は、ページの[タイムライン](/help/sites-cloud/authoring/getting-started/basic-handling.md#timeline)を調べて、ページを移動したかどうかを確認します。

## バージョンと現在のページとの比較 {#comparing-a-version-with-current-page}

以前のバージョンを現在のページと比較するには、次の手順を実行します。

1. 比較するページに移動して、そのページを表示します。
1. [選択モード](/help/sites-cloud/authoring/getting-started/basic-handling.md#viewing-and-selecting-resources)でページを選択します。
1. 「**タイムライン**」列を開き、「**すべて表示**」または「**バージョン**」を選択します。
1. ページバージョンがリストに表示されます。比較するバージョンを選択します。

   ![バージョンの比較](/help/sites-cloud/authoring/assets/versions-revert.png)

1. 「**現在のバージョンと比較**」を選択します。[ページの比較](/help/sites-cloud/authoring/features/page-diff.md)が開き、ページの違いが表示されます。

## タイムワープ {#timewarp}

タイムワープは、過去の特定の時間にページが&#x200B;*公開された*&#x200B;状態をシミュレートするために設計された機能です。

コンテンツの作成は継続的な共同作業プロセスなので、コンテンツの変更内容を把握するために、公開された Web サイトを作成者が経時的に追跡できるようにすることがタイムワープの目的です。この機能では、ページのバージョンを使用してパブリッシュ環境の状態を判断します。

次の手順を実行します。

* システムで、選択した時間にアクティブであったページバージョンが検索されます。
* つまり、タイムワープで選択した時点より前に作成またはアクティベートされたバージョンが表示されます。**
* 移動先が削除済みのページである場合も、このページの古いバージョンがリポジトリ内で有効であれば、ページのレンダリングがおこなわれます。
* 公開されたバージョンが見つからない場合、オーサー環境の現在のページの状態に戻ります（これは、閲覧を妨げるエラー（404）ページが表示されないようにするためです）。

### タイムワープの使用 {#using-timewarp}

タイムワープは、ページエディターの[モード](/help/sites-cloud/authoring/fundamentals/environment-tools.md#page-modes)です。開始するには、他のモードに切り替えるときと同様にタイムワープモードに切り替えます。

1. タイムワープを開始するページのエディターを起動し、モード選択で&#x200B;**タイムワープ**&#x200B;を選択します。

   ![タイムワープモード](/help/sites-cloud/authoring/assets/versions-timewarp-mode.png)

1. ダイアログで、目的の日時を設定して、「**日付を設定**」をクリックまたはタップします。時間を選択しない場合は、現在の時間がデフォルトになります。

   ![タイムワープの目的の日時](/help/sites-cloud/authoring/assets/versions-timewarp-target.png)

1. ページは、日付設定に基づいて表示されます。タイムワープモードは、ウィンドウの上部にある青いステータスバーで示されます。ステータスバーのリンクを使用して、新しい目的の日付を選択したり、タイムワープモードを終了したりします。

   ![タイムワープモードの状態](/help/sites-cloud/authoring/assets/versions-timewarp.png)

### タイムワープの制限事項 {#timewarp-limitations}

タイムワープでは、選択した時点のページを再現するために最大限の努力をします。ただし、AEM でのコンテンツの継続的なオーサリングは複雑な作業なので、これが常に可能とは限りません。タイムワープを使用する際は、以下の制限事項に留意してください。

* **タイムワープは、公開されたページに基づいて機能する** - タイムワープは対象のページが既に公開されている場合にのみ完全に機能します。まだ公開されていない場合は、オーサー環境の現在のページが表示されます。
* **タイムワープではページのバージョンを使用する** - リポジトリから削除されたページに移動する場合、このページの古いバージョンがリポジトリ内でまだ有効であれば正しくレンダリングされます。
* **削除されたバージョンがタイムワープに影響を及ぼす** - バージョンがリポジトリから削除された場合、タイムワープで正しい表示をおこなうことができません。
* **タイムワープは読み取り専用** - ページの古いバージョンを編集することはできません。古いバージョンは表示のみ可能です。古いバージョンを復元する場合は、[復元](#revert-to-a-version)を使用して手動でおこなう必要があります。
* **タイムワープはページのコンテンツにのみ基づく** - Web サイトのレンダリングに使用する要素（コード、CSS、アセット／画像など）を変更した場合、これらのアイテムはリポジトリ内でバージョン化されないので、元の表示と異なる表示になります。

>[!CAUTION]
>
>タイムワープは、作成者によるコンテンツの把握と作成を支援するツールとして設計されています。監査ログや法的な目的のためのものではありません。
