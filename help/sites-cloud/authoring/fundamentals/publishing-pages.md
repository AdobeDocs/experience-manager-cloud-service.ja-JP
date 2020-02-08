---
title: ページの公開
description: AEMを使用してページを公開および非公開する方法
translation-type: tm+mt
source-git-commit: e88a814a901d7fa0da2675fa6017c66d61a73445

---


# ページの公開 {#publishing-pages}

オーサー環境でコンテンツを作成およびレビューした後は、[公開 Web サイト（パブリッシュ環境）でコンテンツを利用できるようにする](/help/sites-cloud/authoring/getting-started/concepts.md)ことが目標となります。

この操作は、ページの公開と呼ばれます。パブリッシュ環境からページを削除する場合は、非公開と呼びます。ページは、公開／非公開を切り替えても、削除するまでは、さらなる変更に備えてオーサー環境で使用できます。

ページは直ちに公開したり非公開にしたりできます。また、事前に定義された日時に公開することもできます。

## 用語 {#terminology}

AEMを使用する際に、発行に関連する様々な用語が発生する場合があります。

* **発行／非公開**
   * コンテンツを公開環境で公開できる（または公開できない）アクションの主な用語は次のとおりです。
   * これらはAEMドキュメントで使用される用語です。
* **アクティブ化/非アクティブ化**
   * これらの用語は、発行/非公開と同義語です。
   * これらの用語は、以前のバージョンのAEMで使用されていました。
* **レプリケート／レプリケーション**
   * ページを公開する際に、ある環境から別の環境へのデータの移動（ページコンテンツ、ファイル、コード、ユーザーコメントなど）を説明する技術用語です。
   * これらの用語は主に開発者が使用します。

## ページの公開 {#publishing-pages-1}

場所に応じて、次から公開できます。

* [ページエディターから](#publishing-from-the-editor)
* [サイトコンソールから](#publishing-from-the-console)

>[!NOTE]
>
>特定のページを公開するために必要な権限がない場合。
>
>* ワークフローがトリガーされ、公開リクエストの適切なユーザーに通知されます。
>* このワークフローは、開発チームによってカスタマイズされていることがあります。
>* ワークフローがトリガーされたことを通知するメッセージが少しの間表示されます。

<!--
>* This [workflow may have been customized](/help/sites-developing/workflows-models.md#main-pars-procedure-6fe6) by your development team.
>* A message will be displayed briefly to notify you that the workflow was triggered.
-->

### エディターからの公開 {#publishing-from-the-editor}

ページを編集している場合、エディターから直接公開できます。

1. Select the **Page Information** icon to open the menu and then the **Publish Page** option.

   ![ページオプションを使用したページの公開](/help/sites-cloud/authoring/assets/publishing-page-options.png)

1. 公開が必要な参照がページに含まれているかどうかに応じて、次の操作をおこないます。

   * 公開する参照がない場合、ページが直接公開されます。
   * 公開が必要な参照がページに含まれている場合は、それらのリストが&#x200B;**発行**&#x200B;ウィザードに表示され、ウィザードで次のいずれかを実行できます。
      * Specify which of the assets/tags/etc. you want to publish together with the page, then use **Publish** to complete the process.
      * 「**キャンセル**」を使用してアクションを中止します。
   ![ページでの参照の公開](/help/sites-cloud/authoring/assets/publishing-references.png)

1. Selecting **Publish** will replicate the page to the publish environment. ページエディターに、公開アクションを確認する情報バナーが表示されます。

   ![公開ステータス情報バナー](/help/sites-cloud/authoring/assets/publishing-info.png)

   コンソールで同じページを表示すると、更新された公開ステータスが表示されます。

   ![サイトコンソールの列ビューでのページパブリケーションの状態](/help/sites-cloud/authoring/assets/publishing-status-console-column.png)

>[!NOTE]
>
>エディターからの投稿は浅い投稿です。つまり、選択したページ/ページのみが発行され、子ページは発行されない/しないのです。

### コンソールからの公開 {#publishing-from-the-console}

サイトコンソールには、2 つの公開オプションがあります。

* [クイック公開](#quick-publish)
* [公開を管理](#manage-publication)

#### クイック公開 {#quick-publish}

**クイック公開**&#x200B;は、単純な場合のためのもので、選択したページが即座に公開されます。他に何か操作する必要はありません。このため、すべての非公開の参照も自動的に公開されます。

クイック公開でページを公開するには、次の手順を実行します。

1. Select the page or pages in the sites console and click on the **Quick Publish** button.

   ![公開するページの選択](/help/sites-cloud/authoring/assets/publishing-select-pages.png)

1. In the Quick Publish dialog, confirm the publication by clicking on **Publish** or cancel by clicking on **Cancel**. すべての非公開の参照も自動的に公開されることに注意してください。

   ![クイック公開の確認](/help/sites-cloud/authoring/assets/publishing-quick-publish.png)

1. ページが公開される際に、公開を確認するアラートが表示されます。

>[!NOTE]
>
>クイック公開は、浅い公開です。つまり、選択したページだけが公開され、子ページは公開されません。

#### 公開を管理 {#manage-publication}

**「パブリケーションの管理** 」には、「クイック発行」よりも多くのオプションが用意されており、子ページを含めたり、参照をカスタマイズしたり、該当するワークフローを開始したり、後日公開するオプションを提供したりできます。

公開を管理を使用してページを公開または非公開にするには、次の手順を実行します。

1. サイトコンソールで 1 つまたは複数のページを選択し、「**公開を管理**」ボタンをクリックします。

   ![公開するページの選択](/help/sites-cloud/authoring/assets/publishing-select-pages.png)

1. **公開を管理**&#x200B;ウィザードが起動します。最初の手順の&#x200B;**オプション**&#x200B;では、次のことができます。

   * 選択したページの公開または非公開を選択する。
   * そのアクションを今すぐ実行するか後日実行するかを選択する。
   後で公開することを選択すると、指定した時間に選択したページを公開するワークフローが開始されます。逆に、後で非公開にすることを選択すると、特定の時間に選択したページを非公開にするワークフローが開始されます。

   If you want to cancel a publish/unpublish later, go to the Workflow Console to terminate the corresponding workflow. <!--If you want to cancel a publish/unpublish later, go to the [Workflow Console](/help/sites-administering/workflows.md) to terminate the corresponding workflow.-->

   ![パブリケーションオプションの管理](/help/sites-cloud/authoring/assets/publishing-manage-publication-options.png)

   「**次へ**」をクリックして次に進みます。

1. In the next step of the Manage Publication wizard, **Scope**, you can define the scope of the publication/un-publication such as including to include child pages and/or including references.

   ![パブリケーション範囲の管理](/help/sites-cloud/authoring/assets/publishing-manage-publication-scope.png)

   You can use the **Add Content** button to add additional pages to the list of pages to be published in case you neglected to select one before starting the Manage Publication wizard.

   「コンテンツを追加」ボタンをクリックすると、[パスブラウザー](/help/sites-cloud/authoring/fundamentals/environment-tools.md#path-browser)が開き、コンテンツを選択できます。

   Select the required pages and then click **Select** to add the content to the wizard or **Cancel **to cancel the selection and return to the wizard.

   ウィザードに戻ると、リストの項目を選択して、次のような追加のオプションを設定できます。

   * その子を含める。
   * 選択から削除する。
   * その公開済みの参照を管理する。
   ![選択ページのパブリケーションの管理](/help/sites-cloud/authoring/assets/publishing-manage-publication-select.png)

   「**子を含める**」をクリックすると、次のことができるダイアログが開きます。

   * 直近の子のみを含める。
   * 変更されたページのみを含める。
   * 既に公開済みのページのみを含める。
   「**追加**」をクリックして、選択オプションに基づいて公開または非公開にするページのリストに子ページを追加します。「**キャンセル**」をクリックして選択をキャンセルし、ウィザードに戻ります。

   ![子を含むパブリケーションの管理](/help/sites-cloud/authoring/assets/publishing-include-children.png)

   ウィザードに戻ると、子を含めるダイアログでのオプションの選択に基づいて、ページが追加されていることを確認できます。

   ページを選択して「**公開済みの参照**」ボタンをクリックすると、ページに対して公開または非公開にする参照を表示および変更できます。

   ![パブリケーションオプションの管理](/help/sites-cloud/authoring/assets/publishing-manage-publication-references.png)

   The **Published References** dialog displays the references for the selected content. 初期設定では、すべて選択され、公開/非公開になりますが、選択を解除して、アクションに含まれないようにすることができます。

   Click **Done** to save your changes or **Cancel** to cancel the selection and return to the wizard.

   ウィザードに戻ると、「**参照**」列が更新されて、公開または非公開にする参照の選択が反映されます。

   ![選択ページのパブリケーションの管理](/help/sites-cloud/authoring/assets/publishing-manage-publication-select.png)

1. Click **Publish** to complete.

   サイトコンソールに戻ると、公開を確認する通知メッセージが表示されます。

1. If the published pages are associated with workflows, they may be shown in a final **Workflows** step of the publication wizard.

   >[!NOTE]
   >
   >**ワークフロー**&#x200B;手順は、ユーザーの権限に基づいて表示されます。See the previous note on this page regarding publishing privileges as well as Managing Access to Workflows and [Applying Workflows to Pages](/help/sites-cloud/authoring/workflows/applying.md) for details.
   <!--
   >The **Workflows** step will be shown based on what rights your user may or may not have. See the previous note on this page regarding publishing privileges as well as [Managing Access to Workflows](/help/sites-administering/workflows-managing.md) and [Applying Workflows to Pages](/help/sites-cloud/authoring/workflows/applying.md) for details.
   -->

   リソースは、トリガーされたワークフローでグループ化され、それぞれに次のオプションがあります。

   * ワークフローのタイトルを定義する。
   * Keep the workflow package, provided that the workflow has multi-resource support. <!--Keep the workflow package, provided that the workflow has [multi-resource support](/help/sites-developing/workflows-models.md#configuring-a-workflow-for-multi-resource-support).-->
   * ワークフローパッケージを維持するオプションが選択されている場合、ワークフローパッケージのタイトルを定義する。
   Click **Publish** or **Publish Later** to complete the publication.

## ページを非公開にする {#unpublishing-pages}

ページを非公開にすると、そのページがパブリッシュ環境から削除され、読者に公開されなくなります。

In a [manner similar to publishing](#publishing-pages), one or more pages can be unpublished:

* [ページエディターから](#unpublishing-from-the-editor)
* [サイトコンソールから](#unpublishing-from-the-console)

### エディターから非公開にする {#unpublishing-from-the-editor}

ページを編集する際に、そのページを非公開にする場合、[ページを公開](#publishing-from-the-editor)するときと同じように、**ページ情報**&#x200B;メニューで「**ページを非公開にする**」を選択します。

### コンソールから非公開にする {#unpublishing-from-the-console}

[「公開を管理」オプションを使用して公開する](#manage-publication)場合と同様に、「公開を管理」オプションを使用して非公開にできます。

1. サイトコンソールで 1 つまたは複数のページを選択し、「**公開を管理**」ボタンをクリックします。
1. **公開を管理**&#x200B;ウィザードが起動します。In the first step, **Options**, select to **Unpublish** instead of the default option of **Publish**.

   ![非公開中](/help/sites-cloud/authoring/assets/publishing-unpublish.png)

   後で公開することを選択するとこのバージョンのページを公開するワークフローが指定した時間に開始されるのと同じように、後でアクティベートを解除することを選択すると、選択したページを非公開にするワークフローが特定の時間に開始されます。

   If you want to cancel a publish/unpublish later, go to the Workflow Console to terminate the corresponding workflow. <!--If you want to cancel a publish/unpublish later, go to the [Workflow Console](/help/sites-administering/workflows.md) to terminate the corresponding workflow.-->

1. To complete the un-publication, continue through the wizard as you would to [publish the page](#manage-publication).

## ツリーの公開と非公開 {#publishing-and-unpublishing-a-tree}

多数のコンテンツページを入力または更新した場合、これらのページがすべて同じルートページの下にあれば、ツリー全体を 1 回の操作で簡単に公開できます。

サイトコンソールにある「[公開を管理](#manage-publication)」オプションを使用すると、これをおこなうことができます。

1. サイトコンソールで、公開または非公開するツリーのルートページを選択し、「**公開を管理**」を選択します。
1. **公開を管理**&#x200B;ウィザードが起動します。公開または非公開と実行するタイミングを選択して、「**次へ**」を選択して続行します。
1. **範囲**&#x200B;の手順で、ルートページを選択して、「**子を含める**」を選択します。

   ![選択ページのパブリケーションの管理](/help/sites-cloud/authoring/assets/publishing-manage-publication-select.png)

1. In the **Include Children** dialogue, un-check the options:

   * 直近の子のみを含める
   * 既に公開済みのページのみを含める
   これらのオプションは、デフォルトで選択されているので、忘れずに選択解除する必要があります。Click **Add** to confirm and add the content to the publication/un-publication.

   ![公開取り消し時に子を含める](/help/sites-cloud/authoring/assets/publishing-tree-children.png)

1. **公開を管理**&#x200B;ウィザードにツリーのコンテンツがリストされていることを確認します。ページを追加したりそれらの選択を削除したりすることで、選択をさらにカスタマイズできます。

   ![パブリケーションの管理オプション](/help/sites-cloud/authoring/assets/publishing-tree-select.png)

   Remember that you can also review the references to be published via the **Published References** option.

1. [通常どおり[パブリケーションの管理](#manage-publication) ]ウィザードを続行して、ツリーのパブリケーションまたは非パブリケーションを完了します。

## 公開ステータスの判別 {#determining-publication-status}

ページの公開ステータスは、次のように指定できます。

* [サイトコンソールのリソースの概要情報](/help/sites-cloud/authoring/getting-started/basic-handling.md#viewing-and-selecting-resources)

   ![カード表示でのパブリケーションの状態](/help/sites-cloud/authoring/assets/publishing-status-console-card.png)

   公開ステータスは、サイトコンソールの[カード](/help/sites-cloud/authoring/getting-started/basic-handling.md#card-view)、[列](/help/sites-cloud/authoring/getting-started/basic-handling.md#column-view)および[リスト](/help/sites-cloud/authoring/getting-started/basic-handling.md#list-view)表示に表示されます。

* In the [timeline](/help/sites-cloud/authoring/getting-started/basic-handling.md#timeline)

   ![タイムラインビューでのパブリケーションの状態](/help/sites-cloud/authoring/assets/publishing-status-timeline.png)

* In the [Page Information menu](/help/sites-cloud/authoring/fundamentals/environment-tools.md#page-information) when editing a page

   ![ページ情報メニューのパブリケーションの状態](/help/sites-cloud/authoring/assets/publishing-status-page-information.png)
