---
title: Sites コンソールからのページの公開
description: Sites コンソールを使用してページを公開および非公開にする方法について説明します。
exl-id: 89f2363c-7922-4ca5-92cb-cbee6a393ee3
solution: Experience Manager Sites
feature: Authoring
role: User
source-git-commit: 5ad91a32d705ef61e8b9799bf7fb1e136bb8bfa0
workflow-type: tm+mt
source-wordcount: '1635'
ht-degree: 89%

---


# Sites コンソールからのページの公開 {#publishing-pages}

オーサー環境でコンテンツを作成およびレビューした後は、[公開 web サイト（パブリッシュ環境）でコンテンツを利用できるようにする](/help/sites-cloud/authoring/author-publish.md)ことが目標となります。

この操作は、ページの公開と呼ばれます。パブリッシュ環境からページを削除する場合は、ページの非公開と呼ばれます。ページは、公開／非公開を切り替えても、削除するまでは、さらなる変更に備えてオーサー環境で使用できます。

[**Sites** コンソール ](/help/sites-cloud/authoring/sites-console/introduction.md) を使用して、ページを直ちに公開/非公開にすることも、後で事前定義済みの日時に公開/非公開にすることもできます。

>[!TIP]
>
>Sites コンソール以外の場所から公開できます。
>
>* [ ページエディターから ](/help/sites-cloud/authoring/page-editor/publishing.md)
>* [ ユニバーサルエディターから ](/help/sites-cloud/authoring/universal-editor/publishing.md)
>* [ エクスペリエンスフラグメントから ](/help/sites-cloud/authoring/fragments/experience-fragments.md) コンソールまたはエディター
>
>これらの場所から公開する場合は、提供されるオプションは異なりますが、ここで説明する同様の手順と一般的なアイデアに従います。

## 用語 {#terminology}

Adobe Experience Manager（AEM）as a Cloud Service を使用する場合、公開に関連する様々な用語を目にするかもしれません。

* **公開／非公開**
   * パブリッシュ環境やプレビュー環境でコンテンツを公開する（または非公開にする）アクションに対して主に使用される用語です。
   * これらは AEM のドキュメントで使用される用語です。
* **アクティブ化／非アクティブ化**
   * 公開／非公開と同義です。
   * これらの用語は、以前のバージョンの AEM で使用されていました。
* **レプリケート／レプリケーション**
   * ページを公開する際（例：オーサーからプレビューへ）に行われる、環境間でのデータ（ページコンテンツ、ファイル、コード、ユーザーコメントなど）の移動を表す技術用語です。
   * これらの用語は主に開発者が使用します。

>[!NOTE]
>
>特定のページを公開するために必要な特権がない場合。
>
>* ワークフローがトリガーされて、公開リクエストの適切なユーザーに通知されます。
>* このワークフローは、開発チームによってカスタマイズされていることがあります。
>* ワークフローがトリガーされたことを通知するメッセージが少しの間表示されます。

>[!NOTE]
>
>ページの順序を保持する場合は、[公開を管理](#manage-publication)を使用して、親ページを子ページと共に 1 回のアクションで公開する必要があります。
>
>次の場合、ページの順序は保証されません:。
>
>* 子ページのみが公開用に選択されている場合（注文情報が親ページに保持されるので）
>* 親ページと子ページが別々のアクションで公開される場合

## Sites コンソールからのページの公開 {#publishing-from-the-sites-console}

**サイト**&#x200B;コンソールには、2 つの公開オプションがあります。

* [クイック公開](#quick-publish)
* [公開を管理](#manage-publication)

### クイック公開 {#quick-publish}

**クイック公開**&#x200B;は単純なケースに使用します。他の操作を行わなくても、選択したページが即座に公開されます。このため、すべての非公開の参照も自動的に公開されます。

クイック公開でページを公開するには、次の手順に従います。

1. サイトコンソールで 1 つ以上のページを選択し、「**クイック公開**」ボタンをクリックします。

   ![公開するページの選択](/help/sites-cloud/authoring/assets/publishing-select-pages.png)

1. クイック公開ダイアログで、「**公開**」をクリックして公開を確認するか、「**キャンセル**」をクリックしてキャンセルします。すべての非公開の参照も自動的に公開されることに注意してください。

   ![クイック公開の確認](/help/sites-cloud/authoring/assets/publishing-quick-publish.png)

1. ページを公開する際、公開を確認するアラートが表示されます。

>[!NOTE]
>
>クイック公開は、浅い公開です。つまり、選択したページだけが公開され、子ページは公開されません。

### 公開を管理 {#manage-publication}

**公開を管理**&#x200B;には、**クイック公開**&#x200B;よりも多くのオプションがあります。子ページの追加、参照のカスタマイズ、プレビューサービスへの公開（使用可能な場合）、該当するワークフローの開始を可能にし、後日公開するオプションを提供します。

公開を管理を使用してページを公開または非公開にするには、次の手順を実行します。

1. サイトコンソールで 1 つまたは複数のページを選択し、「**公開を管理**」ボタンをクリックします。

   ![公開するページの選択](/help/sites-cloud/authoring/assets/publishing-select-pages.png)

1. **公開を管理**&#x200B;ウィザードが起動します。最初の手順では、**オプション**&#x200B;を使用すると、以下のことが可能になります。

   * **アクション**

     選択したページの公開または非公開を選択する。

   * **宛先**

     パブリッシュサービス（デフォルト）またはプレビューサービスのどちらで公開するかを選択します。[プレビューサービスが設定](/help/sites-cloud/authoring/sites-console/previewing-content.md)されている場合にのみ使用できます。

   * **スケジュール設定**

     今すぐ実行するか、後日実行するかを選択します。

     後日公開にすると、選択したページを指定した時間に公開するワークフローが開始します。逆に、後で非公開にすると、特定の時間に選択したページを非公開にするワークフローが開始します。

     >[!TIP]
     >
     >公開／非公開を後からキャンセルする場合は、[ワークフローコンソール](/help/sites-cloud/administering/workflows-administering.md#suspending-resuming-and-terminating-a-workflow-instance)に移動して、対応するワークフローを終了します。

     >[!TIP]
     >
     >公開するコンテンツをスケジュールすると、コンテンツがレプリケートされ、公開ワークフローに従います。 既に公開済みのコンテンツを非公開にせずに一時的に非表示にする場合は、ページプロパティで [**オンタイム** と **オフタイム** を使用できることを検討してください。](/help/sites-cloud/authoring/sites-console/page-properties.md#basic)

   ![公開を管理でのオプション](/help/sites-cloud/authoring/assets/publishing-manage-publication-options.png)

1. 「**次へ**」をクリックして次に進みます。

1. 公開を管理ウィザードの次の手順の&#x200B;**範囲**&#x200B;では、子ページを含めたり、参照を含めたりするなど、公開／非公開の範囲を定義できます。

   ![公開を管理での範囲](/help/sites-cloud/authoring/assets/publishing-manage-publication-scope.png)

   **コンテンツの追加**

   公開を管理ウィザードを開始する前に選択し忘れた場合は、「**コンテンツを追加**」ボタンを使用して、公開するページのリストにページを追加できます。

   「**コンテンツを追加**」ボタンを選択すると、[パスブラウザー](/help/sites-cloud/authoring/path-selection.md)が開き、コンテンツを選択できます。

   必要なページを選択し、「**選択**」をクリックしてコンテンツをウィザードに追加するか、「**キャンセル**」をクリックして選択をキャンセルして、ウィザードに戻ります。

   **選択範囲を削除**

   ウィザードに戻ると、リストの項目を選択して、選択項目から削除できます。

   ![公開を管理でのページ選択](/help/sites-cloud/authoring/assets/publishing-manage-publication-select.png)

   **公開済みの参照**

   ページを選択して「**公開済みの参照**」ボタンをクリックすると、ページに対して公開または非公開にする参照を表示および変更できます。

   ![公開を管理でのオプション](/help/sites-cloud/authoring/assets/publishing-manage-publication-references.png)

   **公開済みの参照**&#x200B;ダイアログに、選択したコンテンツの参照が表示されます。デフォルトでは、それらはすべて選択され、公開／非公開になっていますが、チェックを外して選択を解除すると、アクションに含まれないようになります。

   「**完了**」をクリックして変更を保存するか、「**キャンセル**」をクリックして選択をキャンセルし、ウィザードに戻ります。

   ウィザードに戻ると、「**参照**」列が更新されて、公開または非公開にする参照の選択が反映されます。

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
   >**ワークフロー**&#x200B;手順は、ユーザーの権限に基づいて表示されます。詳しくは、公開権限に関するこのページの前述の注意事項、ワークフローへのアクセスの管理および[ページへのワークフローの適用](/help/sites-cloud/authoring/workflows/applying.md)を参照してください。

   リソースは、トリガーされたワークフローでグループ化され、それぞれに次のオプションが提供されます。

   * ワークフローのタイトルを定義します。
   * ワークフローが複数のリソースをサポートする場合、ワークフローパッケージを維持する。
   * ワークフローパッケージを維持するオプションが選択されている場合、ワークフローパッケージのタイトルを定義する。

1. 「**公開**」または「**後で公開する**」をクリックして、公開を完了します。

## ページを非公開にする {#unpublishing-pages}

ページを非公開にすると、そのページが公開または [ プレビュー ](/help/sites-cloud/authoring/sites-console/previewing-content.md) 環境から削除され、読者からアクセスできなくなります。

[「公開を管理」オプションを使用して公開する](#manage-publication)場合と同様に、「公開を管理」オプションを使用して非公開にできます。

1. Sites コンソールで 1 つまたは複数のページを選択し、「**公開を管理**」ボタンをクリックします。
1. **公開を管理**&#x200B;ウィザードが起動します。最初の手順の&#x200B;**オプション**&#x200B;で、デフォルトオプションの&#x200B;**公開**&#x200B;の代わりに&#x200B;**非公開**&#x200B;を選択します。

   ![非公開 - オプション](/help/sites-cloud/authoring/assets/publishing-unpublish.png)

   後で公開することを選択するとこのバージョンのページを公開するワークフローが指定した時間に開始されるのと同じように、後でアクティベートを解除することを選択すると、選択したページを非公開にするワークフローが特定の時間に開始されます。

   >[!NOTE]
   >
   >公開／非公開を後からキャンセルする場合は、[ワークフローコンソール](/help/sites-cloud/administering/workflows-administering.md#suspending-resuming-and-terminating-a-workflow-instance)に移動して、対応するワークフローを終了します。

   >[!NOTE]
   >[プレビュー](/help/sites-cloud/authoring/sites-console/previewing-content.md)環境がある場合は、公開を管理中に&#x200B;**宛先**&#x200B;を選択できます。

1. 非公開の操作を完了するには、[ページを公開する](#manage-publication)場合と同様にウィザードを続行します。

   ![非公開 - 範囲](/help/sites-cloud/authoring/assets/publishing-unpublish-scope.png)

## ツリーの公開と非公開 {#publishing-and-unpublishing-a-tree}

多数のコンテンツページを入力または更新した場合、これらのページがすべて同じルートページの下にあれば、ツリー全体を 1 回の操作で簡単に公開できます。

サイトコンソールにある「[公開を管理](#manage-publication)」オプションを使用すると、これを行うことができます。

1. サイトコンソールで、公開または非公開するツリーのルートページを選択し、「**公開を管理**」を選択します。
1. **公開を管理**&#x200B;ウィザードが起動します。公開または非公開および実行するタイミングを選択して、「**次へ**」を選択して続行します。
1. **範囲**&#x200B;の手順で、ルートページを選択して、「**子を含める**」を選択します。

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

* [サイトコンソールのリソースの概要情報](/help/sites-cloud/authoring/basic-handling.md#viewing-and-selecting-resources)

  ![カード表示での公開ステータス](/help/sites-cloud/authoring/assets/publishing-status-console-card.png)

  公開ステータスは、サイトコンソールの[カード](/help/sites-cloud/authoring/basic-handling.md#card-view)、[列](/help/sites-cloud/authoring/basic-handling.md#column-view)および[リスト](/help/sites-cloud/authoring/basic-handling.md#list-view)表示に表示されます。

* [タイムライン](/help/sites-cloud/authoring/basic-handling.md#timeline)

  ![タイムライン表示での公開ステータス](/help/sites-cloud/authoring/assets/publishing-status-timeline.png)

* （ページ編集時の）[ページ情報メニュー](/help/sites-cloud/authoring/page-editor/introduction.md#page-information)

  ![ページ情報メニューでの公開ステータス](/help/sites-cloud/authoring/assets/publishing-status-page-information.png)
