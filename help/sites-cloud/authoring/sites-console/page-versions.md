---
title: ページバージョンの処理
description: AEM でページのバージョンを作成、比較および復元する方法について説明します。
exl-id: 33d8e43c-594d-4bba-9631-b2c42a1e910f
solution: Experience Manager Sites
feature: Authoring
role: User
source-git-commit: b39c455c9bd4b50eb3777cd1a4bdbada48786d62
workflow-type: ht
source-wordcount: '1574'
ht-degree: 100%

---

# ページバージョンの処理  {#working-with-page-versions}

バージョン管理では、特定の時点でのページの「スナップショット」を作成します。バージョン管理を使用すると、次の操作を実行できます。

* ページのバージョンを作成します。
* 1 つ以上のページの以前のバージョンを次の場所に回復する。
   * ページに対して行った変更を取り消す。
   * 削除したページを復元する。
   * ツリーを（指定した日時に）復元する。
* バージョンをプレビューする。
* ページの現在のバージョンを以前のバージョンと比較する。
   * テキストと画像の差がハイライトされます。
* タイムワープはページのバージョンを使用して、パブリッシュ環境の状態を判断します。

>[!NOTE]
>
>AEM リポジトリでは、コンテンツのみがバージョン管理されます。コード、CSS、JavaScript などの動的リソースはバージョン管理されません。
>
>* バージョンを表示すると、リポジトリの現在のコード、CSS、JavaScript を使用してコンテンツが表示されます。
>* バージョンを復元すると、コンテンツのみが復元され、リポジトリの現在のコード、CSS、JavaScript が適用されます。

## 新しいバージョンの作成 {#creating-a-new-version}

リソースのバージョンは、次の場所から作成できます。

* [タイムラインパネル](#creating-a-new-version-timeline)
* 「[作成](#creating-a-new-version-create-with-a-selected-resource)」オプション（リソースが選択されている場合）

### 新しいバージョンの作成 - タイムライン {#creating-a-new-version-timeline}

1. バージョンを作成するページに移動して、そのページを表示します。
1. [選択モード](/help/sites-cloud/authoring/basic-handling.md#viewing-and-selecting-resources)でページを選択します。
1. **タイムライン**&#x200B;パネルを開きます。
1. コメントフィールドの横の省略記号を選択して、オプションを表示します。

   ![タイムラインパネルに表示されるバージョン](/help/sites-cloud/authoring/assets/versions-timeline-rail.png)

1. 「**バージョンとして保存**」を選択します。
1. 必要に応じて、「**ラベル**」および「**コメント**」を入力します。

   ![バージョンのラベルの追加](/help/sites-cloud/authoring/assets/versions-add-label.png)

1. 「**作成**」で新しいバージョンを確定します。

   タイムラインの情報が、新しいバージョンを示すように更新されます。

### 新しいバージョンの作成 - 選択したリソースで作成 {#creating-a-new-version-create-with-a-selected-resource}

1. バージョンを作成するページに移動して、そのページを表示します。
1. [選択モード](/help/sites-cloud/authoring/basic-handling.md#viewing-and-selecting-resources)でページを選択します。
1. ツールバーで「**作成**」オプションを選択します。
1. 同じダイアログボックスが開きます。必要に応じて、「**ラベル**」および「**コメント**」を入力します。
1. 「**作成**」で新しいバージョンを確定します。

タイムラインが開き、新しいバージョンを示すように情報が更新されます。

## バージョンの回復 {#reinstating-versions}

ページのバージョンを作成した後、以前のバージョンを回復する様々な方法があります。

* [タイムライン](/help/sites-cloud/authoring/basic-handling.md#timeline)パネルの「**このバージョンに戻る**」オプション

  選択したページの以前のバージョンを回復します。

* 上部の[アクションツールバー](/help/sites-cloud/authoring/basic-handling.md#actions-toolbar)の「**復元**」オプション

   * **バージョンを復元**

     現在選択されているフォルダー内の指定されたページのバージョンを復元します。また、以前削除したページの復元も含めることができます。

   * **ツリーを復元**

     ツリー全体のバージョンを指定した日時に復元します。また、以前に削除したページを含めることもできます。

>[!NOTE]
>
>ページを復元する場合、作成されたバージョンが新しい分岐の一部になります。
>
>この処理は次のようになります。
>
>1. 任意のページのバージョンを作成します。
>1. 最初のラベルおよびバージョンノードの名前は 1.0、1.1、1.2 などです。
>1. 最初のバージョン、つまり、1.0 を復元します。
>1. バージョンを再度作成します。
>1. 生成されるラベルおよびノードの名前は、1.0.0、1.0.1、1.0.2 などになりました。

### 特定のバージョンに戻す {#revert-to-a-version}

選択したページの以前のバージョンを&#x200B;**復帰**&#x200B;させるには、次の手順に従います。

1. 以前のバージョンに戻すページに移動して、そのページを表示します。
1. [選択モード](/help/sites-cloud/authoring/basic-handling.md#viewing-and-selecting-resources)でページを選択します。
1. 「**タイムライン**」列を開き、「**すべて表示**」または「**バージョン**」を選択します。選択したページのページバージョンが一覧表示されます。
1. 戻すバージョンを選択します。選択可能なオプションは次のとおりです。

   ![このバージョンに戻る](/help/sites-cloud/authoring/assets/versions-revert.png)

1. 「**このバージョンに戻る**」を選択します。選択したバージョンが復元され、タイムラインの情報が更新されます。

### バージョンを復元 {#restore-version}

このメソッドを使用して、現在のフォルダー内で指定したページのバージョンを復元できます。また、以前削除したページの復元も含めることができます。

1. 必要なフォルダーに移動して[選択](/help/sites-cloud/authoring/basic-handling.md#viewing-and-selecting-resources)します。

1. 「**復元**」を選択し、上部の[アクションツールバー&#x200B;**で「**&#x200B;バージョンを復元](/help/sites-cloud/authoring/basic-handling.md#actions-toolbar)」を選択します。

   >[!NOTE]
   >
   >次のいずれかの場合：
   >
   >* 子ページを持たない単一のページを選択
   >* フォルダー内のどのページにもバージョンがない
   >
   >該当するバージョンがないので、表示が空になります。

1. 使用可能なバージョンが表示されます。

   ![バージョンを復元 - フォルダー内のすべてのページのリスト](/help/sites-cloud/authoring/assets/versions-restore-version-01.png)

1. 特定のページに対して、「**復元後のバージョン**」ドロップダウンセレクターを使用して、そのページに必要なバージョンを選択します。

   ![バージョンを復元 - バージョンの選択](/help/sites-cloud/authoring/assets/versions-restore-version-02.png)

1. メインディスプレイで、復元する必要のあるページを選択します。

   ![バージョンを復元 - ページの選択](/help/sites-cloud/authoring/assets/versions-restore-version-03.png)

1. 選択したページの選択したバージョンを現在のバージョンとして復元するには、「**復元**」を選択します。

>[!NOTE]
>
>必要なページと関連するバージョンを選択する順序は入れ替え可能です。

### ツリーの復元 {#restore-tree}

このメソッドを使用して、指定した日時にツリーのバージョンを復元できます。以前に削除したページを含めることができます。

1. 必要なフォルダーに移動して[選択](/help/sites-cloud/authoring/basic-handling.md#viewing-and-selecting-resources)します。

1. 「**復元**」を選択し、上部の[アクションツールバー](/help/sites-cloud/authoring/basic-handling.md#actions-toolbar)から「**ツリーを復元**」を選択します。ツリーの最新バージョンが表示されます。

   ![ツリーを復元](/help/sites-cloud/authoring/assets/versions-restore-tree-01.png)

1. 「**最新バージョンの日付**」で、日時セレクターを使用して、復元するツリーの別のバージョンを選択します。

1. 必要に応じて、「**バージョン管理されないページを維持**」フラグを設定します。

   * アクティブな（選択されている）場合、バージョン管理されないページはすべて維持され、復元の影響を受けません。

   * 非アクティブな（選択されていない）場合、バージョン管理されないページは、バージョン管理されたツリーに存在しないため、削除されます。

1. 選択したバージョンのツリーを&#x200B;**現在**&#x200B;のバージョンとして復元する場合は、「*復元*」を選択します。

## バージョンのプレビュー {#previewing-a-version}

次の手順で特定のバージョンをプレビューできます。

1. 比較するページに移動して、そのページを表示します。
1. [選択モード](/help/sites-cloud/authoring/basic-handling.md#viewing-and-selecting-resources)でページを選択します。
1. 「**タイムライン**」列を開き、「**すべて表示**」または「**バージョン**」を選択します。
1. ページのバージョンが表示されます。プレビューするバージョンを選択します。

   ![バージョンのプレビュー](/help/sites-cloud/authoring/assets/versions-revert.png)

1. 「**プレビュー**」を選択します。ページが新しいタブに表示されます。

   >[!CAUTION]
   >
   >ページを移動すると、移動前に作成したバージョンのプレビューを実行できなくなります。
   >
   >プレビューで問題が発生した場合は、ページの [タイムライン](/help/sites-cloud/authoring/basic-handling.md#timeline)を調べて、ページを移動したかどうかを確認します。

## 特定のバージョンと現在のページとの比較 {#comparing-a-version-with-current-page}

以前のバージョンを現在のページと比較するには、次の手順を実行します。

1. 比較するページに移動して、そのページを表示します。
1. [選択モード](/help/sites-cloud/authoring/basic-handling.md#viewing-and-selecting-resources)でページを選択します。
1. 「**タイムライン**」列を開き、「**すべて表示**」または「**バージョン**」を選択します。
1. ページのバージョンが表示されます。比較するバージョンを選択します。

   ![バージョンの比較](/help/sites-cloud/authoring/assets/versions-revert.png)

1. 「**現在のバージョンと比較**」を選択します。[ページの差分](/help/sites-cloud/authoring/sites-console/page-diff.md)が開き、違いが表示されます。

## タイムワープ {#timewarp}

タイムワープは、過去の特定の時間にページが&#x200B;*公開された*&#x200B;状態をシミュレートするために設計された機能です。

>[!TIP]
>
>[タイムワープは、未来をプレビューするローンチと組み合わせて使用することもできます](/help/sites-cloud/authoring/launches/preview.md)。

コンテンツの作成は継続的な共同作業プロセスなので、タイムワープの目的は、公開された web サイトを作成者が経時的に追跡することで、コンテンツの変更内容を把握することです。この機能では、ページのバージョンを使用してパブリッシュ環境の状態を判断します。

この機能を使用するには：

* 選択した時間にアクティブであったページバージョンが検索されます。
* つまり、タイムワープで選択した時点より&#x200B;*前*&#x200B;に作成またはアクティベートされたバージョンが表示されます。
* 削除済みのページに移動する場合、ページの古いバージョンがリポジトリ内にある限り、ページのレンダリングされます。
* 公開されたバージョンが見つからない場合、タイムワープはオーサー環境の現在のページの状態に戻します（これは、閲覧を妨げるエラーや 404 ページが表示されないようにするためです）。

### タイムワープの使用 {#using-timewarp}

タイムワープは、ページエディターの[モード](/help/sites-cloud/authoring/page-editor/introduction.md#page-modes)です。開始するには、他のモードに切り替えるときと同様にタイムワープモードに切り替えます。

1. タイムワープを開始するページのエディターを起動し、モード選択で「**タイムワープ**」を選択します。

   ![タイムワープモード](/help/sites-cloud/authoring/assets/versions-timewarp-mode.png)

1. ダイアログボックスで、目的の日時を設定して、「**日付を設定**」をクリックします。時間を選択しない場合は、デフォルトで現在の時間が使用されます。

   ![タイムワープの目的の日時](/help/sites-cloud/authoring/assets/versions-timewarp-target.png)

1. ページは、日付設定に基づいて表示されます。タイムワープモードは、ウィンドウの上部にある青いステータスバーで示されます。ステータスバーのリンクを使用すると、対象とする新しい日付を選択したり、タイムワープモードを終了したりできます。

   ![タイムワープモードの状態](/help/sites-cloud/authoring/assets/versions-timewarp.png)

### タイムワープの制限事項 {#timewarp-limitations}

タイムワープでは、選択した時点のページを再現するために最大限の努力をします。ただし、AEM でのコンテンツの継続的なオーサリングは複雑な作業なので、この再現が常に可能とは限りません。タイムワープを使用する際は、次の制限事項を考慮してください。

* **タイムワープは、公開されたページに基づいて機能する** - タイムワープは事前にページを公開した場合にのみ完全に機能します。まだ公開されていない場合は、オーサー環境の現在のページがタイムワープに表示されます。
* **タイムワープはページのバージョンを使用する** - リポジトリから削除されたページに移動する場合、このページの古いバージョンがリポジトリ内でまだ有効であれば、正しくレンダリングされます。
* **削除されたバージョンがタイムワープに影響を及ぼす** - バージョンがリポジトリーから削除された場合、タイムワープで正しい表示を行うことができません。
* **タイムワープは読み取り専用** - ページの古いバージョンを編集することはできません。古いバージョンは表示のみ可能です。古いバージョンを復元する場合は、[復元](#revert-to-a-version)を使用して手動で行う必要があります。
* **タイムワープはページのコンテンツに基づく** - web サイトのレンダリング要素が変更された場合（コード、CSS、アセットなど）、ビューは元のものとは異なります。これらの項目は、リポジトリ内でバージョン管理されません。

>[!CAUTION]
>
>タイムワープは、作成者によるコンテンツの把握と作成を支援するツールとして設計されています。監査ログや法的な目的のためのものではありません。
