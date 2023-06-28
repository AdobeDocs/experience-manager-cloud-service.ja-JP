---
title: ページの公開
description: AEM を使用してページを公開および非公開にする方法
exl-id: 89f2363c-7922-4ca5-92cb-cbee6a393ee3
source-git-commit: 1994b90e3876f03efa571a9ce65b9fb8b3c90ec4
workflow-type: tm+mt
source-wordcount: '1802'
ht-degree: 68%

---

# ページの公開 {#publishing-pages}

オーサー環境でコンテンツを作成およびレビューしたら、目標は次のとおりです。 [公開 Web サイトで利用できるようにする](/help/sites-cloud/authoring/getting-started/concepts.md) （パブリッシュ環境）。

これは、ページの公開と呼ばれます。 パブリッシュ環境からページを削除する場合は、ページの非公開と呼ばれます。ページの公開と非公開を行う場合、ページを削除するまで、オーサー環境では引き続き変更を加えることができます。

ページの公開または非公開は、即座に行うことも、後で事前定義済みの日時に行うことができます。

>[!NOTE]
>
>エクスペリエンスフラグメントを公開する手順は、エクスペリエンスフラグメントコンソールまたはエディターを使用しますが、基本的にはページ公開する場合と同じです。

## 用語 {#terminology}

Adobe Experience Manager（AEM）as a Cloud Service を使用する場合、公開に関連する様々な用語を目にするかもしれません。

* **公開／非公開**
   * 環境でコンテンツを公開する（または非公開にする）アクションに対して主に使用される用語です。
   * これらは AEM のドキュメントで使用される用語です。
* **アクティブ化／非アクティブ化**
   * 公開／非公開と同義です。
   * これらの用語は、以前のバージョンの AEM で使用されていました。
* **レプリケート／レプリケーション**
   * ページを公開する際に行われる、環境間でのデータ（ページコンテンツ、ファイル、コード、ユーザーコメントなど）の移動を表す技術用語です。
   * これらの用語は主に開発者が使用します。

## ページの公開 {#publishing-pages-1}

場所に応じて、次から公開できます。

* [ページエディターから](#publishing-from-the-editor)
* [サイトコンソールから](#publishing-from-the-console)

>[!NOTE]
>
>特定のページを公開するために必要な特権がない場合。
>
>* ワークフローがトリガーされ、適切な人に公開リクエストが通知されます。
>* このワークフローは、開発チームによってカスタマイズされていることがあります。
>* ワークフローがトリガーされたことを通知するメッセージが短時間表示されます。

>[!NOTE]
>
> その他の可能性については、[ページプロパティの「基本」タブ](/help/sites-cloud/authoring/fundamentals/page-properties.md#basic)の「**オンタイム**」および「**オフタイム**」を参照してください。

### エディターからの公開 {#publishing-from-the-editor}

ページを編集している場合、エディターから直接公開できます。

1. **ページ情報**&#x200B;アイコンを選択してメニューを開き、「**ページを公開**」オプションを選択します。

   ![ページオプションを使用したページの公開](/help/sites-cloud/authoring/assets/publishing-page-options.png)

1. 公開が必要な参照がページに含まれているかどうかに応じて、次の操作を行います。

   * 公開する参照がない場合、ページは直接公開されます。
   * 公開が必要な参照がページに含まれている場合は、それらのリストは **公開** ウィザードでは、次のいずれかを実行できます。
      * ページと一緒に公開するアセットやタグなどを指定し、「**公開**」を使用してプロセスを完了します。
      * 「**キャンセル**」を使用してアクションを中止します。

   ![ページでの参照の公開](/help/sites-cloud/authoring/assets/publishing-references.png)

1. 「**公開**」を選択して、パブリッシュ環境にページをレプリケートします。ページエディターに、公開アクションを確認する情報バナーが表示されます。

   ![公開ステータス情報バナー](/help/sites-cloud/authoring/assets/publishing-info.png)

   コンソールで同じページを表示すると、更新された公開ステータスが表示されます。

   ![サイトコンソールの列表示でのページ公開ステータス](/help/sites-cloud/authoring/assets/publishing-status-console-column.png)

>[!NOTE]
>
>エディターからの公開は、浅い公開です。つまり、選択したページ（複数可）のみが公開され、子ページは公開されません。

>[!NOTE]
>
>エディターで[エイリアス](/help/sites-cloud/authoring/fundamentals/page-properties.md#advanced)を使用してアクセスしたページは公開できません。エディターの「公開」オプションは、実際のパスからアクセスするページでのみ使用できます。

### コンソールからの公開 {#publishing-from-the-console}

サイトコンソールには、2 つの公開オプションがあります。

* [クイック公開](#quick-publish)
* [公開を管理](#manage-publication)

#### クイック公開 {#quick-publish}

**クイック公開** は単純な場合に使用し、選択したページを直ちに公開します。操作は必要ありません。 このため、非公開の参照も自動的に公開されます。

クイック公開でページを公開するには：

1. サイトコンソールで 1 つ以上のページを選択し、「**クイック公開**」ボタンをクリックします。

   ![公開するページの選択](/help/sites-cloud/authoring/assets/publishing-select-pages.png)

1. クイック公開ダイアログで、「**公開**」をクリックして公開を確認するか、「**キャンセル**」をクリックしてキャンセルします。すべての非公開の参照も自動的に公開されることに注意してください。

   ![クイック公開の確認](/help/sites-cloud/authoring/assets/publishing-quick-publish.png)

1. ページが公開されると、公開を確認するアラートが表示されます。

>[!NOTE]
>
>クイック公開は、浅い公開です。つまり、選択したページ（複数可）のみが公開され、子ページは公開されません。

#### 公開の管理 {#manage-publication}

**公開を管理** 次よりも多くのオプションを提供： **クイック公開**&#x200B;を使用すると、子ページを含めたり、参照をカスタマイズしたり、適用可能なワークフローを開始したり、後日公開するオプションを提供したりできます。

「公開を管理」を使用してページを公開または非公開にするには：

1. サイトコンソールで 1 つ以上のページを選択し、 **公開を管理** 」ボタンをクリックします。

   ![公開するページの選択](/help/sites-cloud/authoring/assets/publishing-select-pages.png)

1. **公開を管理**&#x200B;ウィザードが起動します。最初のステップは **オプション**&#x200B;を使用すると、次のことができます。

   * **アクション**

     選択したページの公開または非公開を選択する。

   * **スケジュール設定**

     今すぐ実行するか、後日実行するかを選択します。

     後で公開すると、選択したページを指定した時間に公開するワークフローが開始されます。 逆に、後で非公開にすると、特定の時間に選択したページを非公開にするワークフローが開始されます。

     >[!NOTE]
     >
     >公開／非公開を後からキャンセルする場合は、[ワークフローコンソール](/help/sites-cloud/administering/workflows-administering.md#suspending-resuming-and-terminating-a-workflow-instance)に移動して、対応するワークフローを終了します。

   ![公開を管理でのオプション](/help/sites-cloud/authoring/assets/publishing-manage-publication-options.png)

1. 「**次へ**」をクリックして次に進みます。

1. 公開を管理ウィザードの次の手順の&#x200B;**範囲**&#x200B;では、子ページを含めたり、参照を含めたりするなど、公開／非公開の範囲を定義できます。

   ![公開を管理での範囲](/help/sites-cloud/authoring/assets/publishing-manage-publication-scope.png)

   **コンテンツの追加**

   公開を管理ウィザードを開始する前に選択し忘れた場合は、「**コンテンツを追加**」ボタンを使用して、公開するページのリストにページを追加できます。

   「**コンテンツを追加**」ボタンを選択すると、[パスブラウザー](/help/sites-cloud/authoring/fundamentals/environment-tools.md#path-browser)が開き、コンテンツを選択できます。

   必要なページを選択し、「**選択**」をクリックしてコンテンツをウィザードに追加するか、「**キャンセル**」をクリックして選択をキャンセルして、ウィザードに戻ります。

   **選択範囲を削除**

   ウィザードに戻ると、リストの項目を選択して、選択項目から削除できます。

   ![公開を管理でのページ選択](/help/sites-cloud/authoring/assets/publishing-manage-publication-select.png)

   **公開済みの参照**

   ページを選択して「**公開済みの参照**」ボタンをクリックすると、ページに対して公開または非公開にする参照を表示および変更できます。

   ![公開を管理でのオプション](/help/sites-cloud/authoring/assets/publishing-manage-publication-references.png)

   **公開済みの参照**&#x200B;ダイアログに、選択したコンテンツの参照が表示されます。デフォルトでは、これらはすべて選択され、公開/非公開になりますが、チェックを外して選択を解除し、アクションに含まれないようにすることができます。

   「**完了**」をクリックして変更を保存するか、「**キャンセル**」をクリックして選択をキャンセルし、ウィザードに戻ります。

   ウィザードに戻り、 **参照** 列が更新され、公開または非公開にする参照の選択が反映されます。

   ![公開を管理でのページ選択](/help/sites-cloud/authoring/assets/publishing-manage-publication-select.png)

   **子を含める**

   >[!NOTE]
   >
   >[ツリーの公開と非公開](#publishing-and-unpublishing-a-tree)を参照してください。

   「**子を含める**」をクリックすると、次のことを行えるダイアログボックスが開きます。

   * **子を含める**
   * **直近の子のみを含める**
   * **変更されたページのみを含める**
   * **既に公開済みのページのみを含める**

   必要なオプションを有効にし、「**OK**」で確定すると、選択したオプションに基づいて、公開または非公開にするページのリストに子ページが追加されます。「**キャンセル**」をクリックすると、選択がキャンセルされ、ウィザードに戻ります。

   ![公開を管理での子の包含](/help/sites-cloud/authoring/assets/publishing-include-children.png)

1. 「**公開**」をクリックして完了します。

   サイトコンソールに戻ると、公開を確認する通知メッセージが表示されます。

1. 公開したページがワークフローに関連付けられている場合、公開ウィザードの最後の&#x200B;**ワークフロー**&#x200B;ステップに表示されます。

   ![公開を管理でのページ選択](/help/sites-cloud/authoring/assets/publishing-manage-publication-workflow.png)

   >[!NOTE]
   >
   >この **ワークフロー** ユーザーの権限に基づいて、手順が表示されます。 公開権限およびワークフローへのアクセスの管理および [ページへのワークフローの適用](/help/sites-cloud/authoring/workflows/applying.md) 」を参照してください。

   リソースは、トリガーされたワークフローによってグループ化され、次の各オプションが提供されます。

   * ワークフローのタイトルを定義します。
   * ワークフローが複数のリソースをサポートする場合、ワークフローパッケージを維持する。
   * ワークフローパッケージを維持するオプションが選択されている場合、ワークフローパッケージのタイトルを定義する。

1. 「**公開**」または「**後で公開する**」をクリックして、公開を完了します。

## ページを非公開にする {#unpublishing-pages}

ページを非公開にすると、そのページが公開または[プレビュー](/help/sites-cloud/authoring/fundamentals/previewing-content.md)環境から削除され、読者からアクセスできなくなります。

[公開と同様の方法](#publishing-pages)で、目的の宛先から 1 つ以上のページを非公開にすることができます。

* [ページエディターから](#unpublishing-from-the-editor)
* [サイトコンソールから](#unpublishing-from-the-console)

### エディターから非公開にする {#unpublishing-from-the-editor}

ページの編集時に、そのページを非公開にする場合は、「 **ページを非公開にする** 内 **ページ情報** メニューは、 [ページを公開](#publishing-from-the-editor).

>[!NOTE]
>
>エディターで[エイリアス](/help/sites-cloud/authoring/fundamentals/page-properties.md#advanced)を使用してアクセスしたページは、非公開にすることができません。エディターの「公開」オプションは、実際のパスからアクセスするページでのみ使用できます。

### コンソールから非公開にする {#unpublishing-from-the-console}

[「公開を管理」オプションを使用して公開する](#manage-publication)場合と同様に、「公開を管理」オプションを使用して非公開にできます。

1. サイトコンソールで 1 つ以上のページを選択し、 **公開を管理** 」ボタンをクリックします。
1. **公開を管理**&#x200B;ウィザードが起動します。最初の手順の&#x200B;**オプション**&#x200B;で、デフォルトオプションの&#x200B;**公開**&#x200B;の代わりに&#x200B;**非公開**&#x200B;を選択します。

   ![非公開 - オプション](/help/sites-cloud/authoring/assets/publishing-unpublish.png)

   後で公開することを選択するとこのバージョンのページを公開するワークフローが指定した時間に開始されるのと同じように、後でアクティベートを解除することを選択すると、選択したページを非公開にするワークフローが特定の時間に開始されます。

   >[!NOTE]
   >
   >公開／非公開を後からキャンセルする場合は、[ワークフローコンソール](/help/sites-cloud/administering/workflows-administering.md#suspending-resuming-and-terminating-a-workflow-instance)に移動して、対応するワークフローを終了します。

   >[!NOTE]
   >[プレビュー](/help/sites-cloud/authoring/fundamentals/previewing-content.md)環境がある場合は、公開を管理中に&#x200B;**宛先**&#x200B;を選択できます。

1. 非公開の操作を完了するには、[ページを公開する](#manage-publication)場合と同様にウィザードを続行します。

   ![非公開 - 範囲](/help/sites-cloud/authoring/assets/publishing-unpublish-scope.png)

## ツリーの公開と非公開 {#publishing-and-unpublishing-a-tree}

多数のコンテンツページを入力または更新した場合（すべて同じルートページの下に存在）、ツリー全体を 1 回の操作で簡単に公開できます。

サイトコンソールにある「[公開を管理](#manage-publication)」オプションを使用すると、これを行うことができます。

1. サイトコンソールで、公開または非公開にするツリーのルートページを選択し、「 」を選択します **公開を管理**.
1. **公開を管理**&#x200B;ウィザードが起動します。公開または非公開にするタイミングと、実行するタイミングを選択して、 **次へ** をクリックして続行します。
1. 内 **範囲** ステップで、ルートページを選択し、 **子を含める**.

   ![公開を管理でのページ選択](/help/sites-cloud/authoring/assets/publishing-manage-publication-select.png)

1. **子を含める**&#x200B;ダイアログで、次の操作を行います。

   * 「**子を含める**」を選択する
   * 「**直近の子のみを含める**」を選択解除する
   * 「**既に公開済みのページのみを含める**」を選択解除する
   * **変更されたページのみを含める**&#x200B;を必要に応じて設定する

   これらのオプションは、デフォルトで選択されているので、忘れずに設定する必要があります。「**OK**」をクリックして選択して確定すると、コンテンツが公開／非公開に追加されます。

   ![ツリー公開に子を含める](/help/sites-cloud/authoring/assets/publishing-include-children-tree.png)

1. **公開を管理**&#x200B;ウィザードで、ページを追加したり選択から削除したりして、選択をさらにカスタマイズできます。

   「**公開済みの参照**」オプションを使用して、公開する参照を確認することもできます。

1. [通常どおりに公開を管理ウィザードを続行](#manage-publication)して、ツリーの公開または非公開を完了します。

## 公開ステータスの判別 {#determining-publication-status}

以下のいずれかで、ページの公開ステータスを判別できます。

* [サイトコンソールのリソースの概要情報](/help/sites-cloud/authoring/getting-started/basic-handling.md#viewing-and-selecting-resources)

  ![カード表示での公開ステータス](/help/sites-cloud/authoring/assets/publishing-status-console-card.png)

  公開ステータスは、サイトコンソールの[カード](/help/sites-cloud/authoring/getting-started/basic-handling.md#card-view)、[列](/help/sites-cloud/authoring/getting-started/basic-handling.md#column-view)および[リスト](/help/sites-cloud/authoring/getting-started/basic-handling.md#list-view)表示に表示されます。

* [タイムライン](/help/sites-cloud/authoring/getting-started/basic-handling.md#timeline)

  ![タイムライン表示での公開ステータス](/help/sites-cloud/authoring/assets/publishing-status-timeline.png)

* （ページ編集時の）[ページ情報メニュー](/help/sites-cloud/authoring/fundamentals/environment-tools.md#page-information)

  ![ページ情報メニューでの公開ステータス](/help/sites-cloud/authoring/assets/publishing-status-page-information.png)
