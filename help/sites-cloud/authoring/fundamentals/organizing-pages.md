---
title: ページの作成と整理
description: AEM でページを作成および整理する方法
exl-id: c57096ca-34fe-4b19-98e0-8f3cd43cf24e
source-git-commit: 47910a27118a11a8add6cbcba6a614c6314ffe2a
workflow-type: tm+mt
source-wordcount: '2561'
ht-degree: 77%

---

# ページの作成と整理 {#creating-and-organizing-pages}

このドキュメントでは、Adobe Experience Manager as a Cloud Service でページを作成および管理して、それらのページの[コンテンツを作成](/help/sites-cloud/authoring/fundamentals/editing-content.md)できるようにする方法について説明します。

>[!NOTE]
>
>適切なアクセス権と、ページに対するアクション（作成、コピー、移動、編集、削除など）を実行するための権限を持つアカウントが必要です。
>
>問題が発生した場合は、システム管理者にお問い合わせください。

<!--
>Your account needs the [appropriate access rights](/help/sites-administering/security.md) and [permissions](/help/sites-administering/security.md#permissions) to take action on pages such as create, copy, move, edit, and delete.
-->

>[!TIP]
>
>Web サイトコンソールから使用できる[キーボードショートカット](/help/sites-cloud/authoring/getting-started/keyboard-shortcuts.md)が多数あり、ページをより効率的に整理できます。

## Web サイトの整理 {#organizing-your-website}

作成者は、AEM内で Web サイトを整理する必要があります。 これには、次の目的でコンテンツページを作成し、名前を付ける必要があります。

* 作成者がオーサー環境でコンテンツページを容易に検索できるようにする
* サイトへの訪問者がパブリッシュ環境でコンテンツページを容易に閲覧できるようにする

コンテンツの整理に役立つ[フォルダー](#creating-a-new-folder)を使用することもできます。

Web サイトの構造は、コンテンツページを保持するツリーと見なすことができます。これらのコンテンツページの名前は、URL の作成に使用されます。一方、タイトルは、ページコンテンツを表示したときに表示されます。

以下に、[WKND チュートリアル](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-wknd-tutorial-develop/overview.html?lang=ja)サイトの例です。このサイトでは、スケートボード場（`la-skateparks`）に関する記事にアクセスします。

`http://<host>:<port>/editor.html/content/wknd/en/sports/la-skateparks.html`

```xml
 /content
 /wknd
  /en
   /music
    /...
   /sports
    /la-skateparks
    /five-gyms-la
    /mountain-bike-routes
   /shopping
    /...
   /art
    /...
   /...
```

この構造は **Sites** コンソールから表示でき、[Web サイトのページ間を移動したり](/help/sites-cloud/authoring/getting-started/basic-handling.md#selecting-resources)、ページ上でアクションを実行したりできます。新しいサイトや[新しいページ](#creating-a-new-page)を作成することもできます。

どの地点からでも、ヘッダーバーのパンくず（経路表示）から上位のブランチを確認できます。

![パンくずリストを使用した移動](/help/sites-cloud/authoring/assets/organizing-breadcrumbs.png)

### ページ命名規則 {#page-naming-conventions}

新しいページを作成する際の主要なフィールドは 2 つあります。

* **[タイトル](#title)**：

   * これはコンソール内のユーザーに、編集中のページコンテンツの上部に表示されます。
   * このフィールドは必須です。

* **[名前](#name)**：

   * これは URI の生成に使用されます。
   * このフィールドへの入力はオプションです。指定しなかった場合、名前はタイトルから派生します。 詳しくは、次の節、[ページ名の制限事項とベストプラクティス](#page-name-restrictions-and-best-practices)を参照してください。

#### ページ名の制限事項とベストプラクティス {#page-name-restrictions-and-best-practices}

ページの&#x200B;**タイトル**&#x200B;と&#x200B;**名前**&#x200B;は個別に作成できますが、次のように関連しています。

* ページを作成する場合、 **タイトル** フィールドは必須です。 指定しない場合 **名前** がページの作成時に提供されるので、AEMはタイトルの最初の 64 文字から名前を生成します（以下で設定する検証内容に従います）。 ページ名を短くするというベストプラクティスに対応するため、最初の 64 文字のみ使用されます。
* 作成者がページ名を手動で指定する場合は、64 文字の制限は適用されませんが、ページ名の長さに関するその他の技術的制限が適用されることがあります。

>[!TIP]
>
>ページ名を定義するときは、ページ名をできるだけ簡潔にしつつ、読者がわかりやすいようにできるだけ表現力のある覚えやすいものにすることをお勧めします。詳しくは、[ 要素の ](https://www.w3.org/Provider/Style/TITLE.html)W3C スタイルガイド`title`を参照してください。
>
>また、一部のブラウザー（旧バージョンの IE など）では、特定の長さまでの URL しか受け付けないので、ページ名を短くするには技術的な理由もあります。

[新しいページを作成するとき、AEM では AEM と JCR によって課された規則に基づいてページ名が検証されます。](/help/implementing/developing/introduction/naming-conventions.md)

使用できる最小限の文字は次のとおりです。

* `a` から `z` まで
* `A` から `Z` まで
* `0` から `9` まで
* `_`（アンダースコア）
* `-`（ハイフン／マイナス記号）

許可されるすべての文字について詳しくは、[命名規則](/help/implementing/developing/introduction/naming-conventions.md)を参照してください。

>[!NOTE]
>
>ページ名は 150 文字までに制限されています。

#### タイトル {#title}

新しいページを作成するときにページの&#x200B;**タイトル**&#x200B;のみを指定した場合、AEM ではページの&#x200B;**名前**&#x200B;がこの文字列から派生され、AEM と JCR [によって課された規則に基づいてページ名が検証されます](/help/implementing/developing/introduction/naming-conventions.md)。

「**タイトル**」フィールドに無効な文字が含まれていてもエラーにはなりませんが、派生された名前では、無効な文字が別の文字に置き換えられます。次に例を示します。

| タイトル | 派生名 |
|---|---|
| シェン | `schoen.html` |
| SC%&amp;&#42;ç+ | `sc---c-.html` |

#### 名前 {#name}

新しいページを作成するときにページの&#x200B;**名前**&#x200B;を指定すると、AEM では AEM と JCR [によって課された規則に基づいてページ名が検証されます](/help/implementing/developing/introduction/naming-conventions.md)。「**名前**」フィールドに無効な文字は指定できません。AEMで無効な文字が検出されると、フィールドが強調表示され、説明メッセージが表示されます。

![無効なページ名の入力例](/help/sites-cloud/authoring/assets/organizing-invalid-name.png)

>[!TIP]
>
>ISO-639-1 で定義されている 2 文字コードをページ名として使用することは避けてください（言語ルートの場合を除く）。
>
>詳しくは、 [翻訳するコンテンツの準備](/help/sites-cloud/administering/translation/preparation.md) を参照してください。

### テンプレート {#templates}

AEMでは、テンプレートはページの特殊なタイプを指定します。 テンプレートは、作成される新しいページの基礎として使用されます。

テンプレートによって、サムネール画像やその他のプロパティなど、ページの構造が定義されます。例えば、商品ページ、サイトマップおよび問い合わせ先に、それぞれ別のテンプレートを使用することができます。テンプレートは、[コンポーネント](#components)で構成されています。

AEMには、すぐに使用できる複数のテンプレートが用意されています。 使用できるテンプレートは、個々の Web サイトによって異なります。 主なフィールドは次のとおりです。

* **タイトル**：生成される Web ページに表示されるタイトルです。

* **名前**：ページに名前を付ける際に使用されます。

* **テンプレート**：新しいページを生成する際に使用できるテンプレートのリストです。

>[!TIP]
>
>お使いのインスタンスで設定すると、[テンプレートの作成者はテンプレートエディターを使用してテンプレートを作成できます](/help/sites-cloud/authoring/features/templates.md)。

### コンポーネント {#components}

コンポーネントは、AEM で提供される、特定のタイプのコンテンツを追加できる要素です。AEM には、すぐに使用できる様々なコンポーネントが付属しており、包括的な機能を提供します。次のようなコンポーネントがあります。

* テキスト
* 画像
* タイトル
* カルーセル
* その他多数

ページを作成して開いたら、次の操作を実行できます。 [コンポーネントを使用してコンテンツを追加](/help/sites-cloud/authoring/fundamentals/editing-content.md#inserting-a-component): [コンポーネントブラウザー](/help/sites-cloud/authoring/fundamentals/environment-tools.md#components-browser).

>[!TIP]
>
>[コンポーネントコンソール](/help/sites-cloud/authoring/features/components-console.md)は、インスタンス上のコンポーネントの概要を示します。

## ページの管理 {#managing-pages}

### 新しいページの作成 {#creating-a-new-page}

すべてのページが事前に作成されていない限り、コンテンツの作成を開始するには、まずページを作成する必要があります。

1. Sites コンソール（例：`https://<host>:<port>/sites.html/content`）を開きます。
1. 新しいページを作成する場所に移動します。
1. ツールバーの「**作成**」を使用してドロップダウンセレクターを開き、リストから「**ページ**」を選択します。

   ![ページの作成](/help/sites-cloud/authoring/assets/organizing-create-page.png)

1. ウィザードの最初の段階で、次のいずれかを実行できます。

   * 新しいページの作成に使用するテンプレートを選択し、「 」をクリックまたはタップします **次へ** をクリックして続行します。

   * **キャンセル** をクリックしてプロセスを中止します。

   ![新しいページのテンプレートの選択](/help/sites-cloud/authoring/assets/organizing-create-page-template.png)

1. ウィザードの最後のステージで、次のいずれかを実行できます。

   * 3 つのタブを使用して、新しいページに割り当てる[ページプロパティ](/help/sites-cloud/authoring/fundamentals/page-properties.md)を入力し、「**作成**」をクリックまたはタップしてページを実際に作成します。

   * 用途 **戻る** をクリックして、テンプレートの選択に戻ります。

   主なフィールドは次のとおりです。

   * **タイトル**：

      * これはユーザーに表示され、必須です。
   * **名前**：

      * これは URI の生成に使用されます。指定しなかった場合、名前はタイトルから派生します。
      * 新しいページを作成するときにページの「**名前**」を指定すると、AEM では AEM と JCR [の規則に基づいてページ名が検証されます](/help/implementing/developing/introduction/naming-conventions.md)。
      * あなた **無効な文字を送信できません** 内 **名前** フィールドに入力します。 AEM で無効な文字が検出されると、そのフィールドは強調表示され、対象の文字を削除または置換する必要があることを示す説明メッセージが表示されます。

   >[!TIP]
   >
   >詳しくは、 [ページ命名規則](#page-naming-conventions).

   新しいページを作成するために必要な最小の情報は、 **タイトル**.

   ![ページタイトルの指定](/help/sites-cloud/authoring/assets/organizing-create-page-title.png)

1. 「**作成**」を使用してプロセスを完了し、新しいページを作成します。ページをすぐに「**開く**」かコンソールに戻る（「**完了**」する）かを確認するダイアログが表示されます。

   ![ページ作成の成功](/help/sites-cloud/authoring/assets/organizing-create-page-success.png)

   >[!NOTE]
   >
   >ページの作成先に同名のページが既に存在する場合は、その名前のバリエーションが数字を付加して自動的に生成されます。例えば、`beach` が既に存在する場合、新しいページは `beach1` になります。

1. コンソールに戻ると、新しいページが表示されます。

   ![作成された新しいページ](/help/sites-cloud/authoring/assets/organizing-create-page-result.png)

>[!CAUTION]
>
>作成済みのページのテンプレートは変更できません。ただし、[新しいテンプレートでローンチを作成](/help/sites-cloud/authoring/launches/creating.md#create-launch-with-new-template)する場合を除きます。ただしその場合、既存のコンテンツはすべて失われます。

### ページを開いて編集 {#opening-a-page-for-editing}

ページを作成するか、（コンソール内の）既存ページに移動した後、そのページを開いて編集できます。

1. **Sites** コンソールを開きます。
1. 編集するページが表示されるまで移動します。
1. 次のいずれかを使用して、ページを選択します。

   * [クイックアクション](/help/sites-cloud/authoring/getting-started/basic-handling.md#quick-actions)
   * [選択モード](/help/sites-cloud/authoring/getting-started/basic-handling.md#selecting-resources)とツールバー

   その後、「**編集**」アイコンを選択します。

   ![「編集」ボタン](/help/sites-cloud/authoring/assets/edit.png)

1. ページが開き、必要に応じて[編集](/help/sites-cloud/authoring/fundamentals/editing-content.md)できるようになります。

>[!NOTE]
>
>ページエディターから他のページに移動する操作は、編集モードではリンクがアクティブにならないので、プレビューモードでのみ可能です。

### ページのコピーと貼り付け {#copying-and-pasting-a-page}

ページとそのすべてのサブページを新しい場所にコピーできます。

1. **Sites** コンソールで、コピー対象のページが表示されるまで移動します。
1. 次のいずれかを使用してページを選択します。

   * [クイックアクション](/help/sites-cloud/authoring/getting-started/basic-handling.md#quick-actions)
   * [選択モード](/help/sites-cloud/authoring/getting-started/basic-handling.md#selecting-resources)とツールバー

   そして、 **コピー** ページアイコン：

   ![コピー](/help/sites-cloud/authoring/assets/copy.png)

1. ページの新しいコピーを配置する場所に移動します。
1. 使用可能になった「**貼り付け**」アイコンをタップまたはクリックします。

   ![貼り付け](/help/sites-cloud/authoring/assets/paste.png)

1. 貼り付けダイアログには、貼り付けトランザクションの概要のほか、次の機能が表示されます。
   * **新規サイト名**：貼り付けたページの名前を変更します。
   * **子を含めずに貼り付け**：貼り付け時に、選択したページの子ページを除外します（デフォルトでは子ページも貼り付けられます）。

   ![貼り付けダイアログ](/help/sites-cloud/authoring/assets/paste-dialog.png)

1. 「**貼り付け**」ボタンをタップまたはクリックして、貼り付けトランザクションを確定し、新しいページを作成します。

>[!NOTE]
>
>ページのコピー先に同名のページが既に存在する場合は、その名前のバリエーションが数字を付加して自動的に生成されます。例えば、`beach` が既に存在する場合は、`beach` という名前の新しいページは `beach1` になります。

>[!NOTE]
>
>貼り付けアクションを選択モードで開始した場合は、ページがコピーされ次第、選択モードが自動的に終了します。

### ページの移動または名前の変更 {#moving-or-renaming-a-page}

ページの移動手順と名前の変更手順は基本的に同じで、どちらのアクションもページを移動ウィザードで処理されます。このウィザードでは、次の操作を行うことができます。

* ページを移動せずに名前変更する
* ページを名前変更せずに移動する
* 移動と名前変更を同時に行う

AEM では、名前変更または移動が行われるページへの内部リンクを更新する機能が用意されています。これは、ページごとに実行できるので、最大限の柔軟性を提供します。

1. 移動するページが表示されるまで移動します。
1. 次のいずれかを使用してページを選択します。

   * [クイックアクション](/help/sites-cloud/authoring/getting-started/basic-handling.md#quick-actions)
   * [選択モード](/help/sites-cloud/authoring/getting-started/basic-handling.md#selecting-resources)とツールバー

   次に、 **移動** ページアイコン：

   ![「移動」ボタン](/help/sites-cloud/authoring/assets/move.png)

   これにより、ページの移動ウィザードが開きます。

1. 次の **名前を変更** ウィザードのステージでは、次のいずれかを実行できます。

   * 移動後にページに表示する名前を指定し、「 」をクリックまたはタップします **次へ** をクリックして続行します。
   * **キャンセル** をクリックしてプロセスを中止します。

   ![ページの移動と名前変更](/help/sites-cloud/authoring/assets/move-page-rename.png)

   ページを移動するだけの場合、ページ名は変わらない場合があります。

   >[!NOTE]
   >
   >ページの移動先に同名のページが既に存在する場合は、その名前のバリエーションが数字を付加して自動的に生成されます。例えば、`beach` が既に存在する場合は、`beach` という名前の新しいページは `beach1` になります。

1. 次の **宛先を選択** ウィザードのステージでは、次のいずれかを実行できます。

   * 以下を使用： [列表示](/help/sites-cloud/authoring/getting-started/basic-handling.md#column-view) ページの新しい場所に移動するには、次の手順に従います。

      * 移動先のサムネールをクリックして、移動先を選択します。
      * 「**次へ**」をクリックして次に進みます。
   * 用途 **戻る** ページ名の指定に戻る

   >[!NOTE]
   >
   >デフォルトでは、移動または名前を変更するページの親が宛先として選択されます。

   ![ページの移動先の選択](/help/sites-cloud/authoring/assets/move-page-destination.png)

   >[!NOTE]
   >
   >ページの移動先に同名のページが既に存在する場合は、その名前のバリエーションが数字を付加して自動的に生成されます。例えば、`winter` が既に存在する場合、`winter` は `winter1` になります。

1. ページがリンクまたは参照されている場合、またはページが公開されている場合は、詳細が&#x200B;**調整 / 再公開**&#x200B;ステップで一覧表示されます。

   調整または再公開するページを適宜指定できます。

   >[!NOTE]
   >
   >ページがリンクも参照もされていない場合は、このステップは使用できません。

   ![移動時のページ再公開](/help/sites-cloud/authoring/assets/move-page-republish.png)

1. 選択 **移動** プロセスを完了し、必要に応じてページを移動または名前変更します。

>[!NOTE]
>
>ページを既に公開している場合、ページを移動すると自動的に非公開になります。デフォルトでは、移動が完了すると再公開されますが、**調整 / 再公開**&#x200B;ステップの「**再公開**」フィールドをオフにすると、この動作を変更できます。

>[!NOTE]
>
>ページが参照されていない場合は、**調整 / 再公開**&#x200B;手順がスキップされます。

>[!NOTE]
>
>ページ名の変更は、 [ページ命名規則](#page-naming-conventions) 新しいページ名を指定する場合。

>[!NOTE]
>
>ページは、ページの基となるテンプレートが許可されている場所にのみ移動できます。 詳しくは、[使用可能なテンプレート](/help/implementing/developing/components/templates.md#template-availability)を参照してください。

#### 非同期アクション {#asynchronous-actions}

通常、ページの移動または名前変更操作は直ちに実行されます。これは同期処理と見なされ、アクションが完了するまで、UI 内のそれ以上のアクションはブロックされます。

ただし、影響を受けるページ数が定義された制限を超える場合は、アクションは非同期に処理され、ページの移動や名前の変更の操作によって妨げられない UI でオーサリングを続行できます。

* 上の最後の手順で「**移動**」をクリックすると、AEM は設定されている制限を確認します。
* 影響を受けるページ数が制限を下回る場合は、同期操作が実行されます。
* 影響を受けるページ数が上限を超える場合は、非同期操作が実行されます。
   * ユーザーは、非同期操作を実行するタイミングを定義する必要があります
      * **今すぐ**：非同期ジョブの実行を今すぐ開始します。
      * **後で**：非同期ジョブを開始するタイミングをユーザーが定義できます。

         ![非同期ページ移動](/help/sites-cloud/authoring/assets/asynchronous-page-move.png)

非同期ジョブの状態は、[**非同期ジョブステータス**&#x200B;ダッシュボード](/help/operations/asynchronous-jobs.md#monitor-the-status-of-asynchronous-operations)（**グローバルナビゲーション**／**ツール**／**操作**／**ジョブ**）で確認できます。

>[!NOTE]
>
>非同期ジョブ処理の詳細およびページ移動や名前変更アクションの制限の設定方法については、運用ユーザーガイドの[非同期ジョブ](/help/operations/asynchronous-jobs.md)を参照してください。

### ページの削除 {#deleting-a-page}

1. 削除対象のページが表示されるまで移動します。
1. [選択モード](/help/sites-cloud/authoring/getting-started/basic-handling.md#viewing-and-selecting-resources)を使用して必要なページを選択してから、ツールバーの「**削除**」を使用します。

   ![削除ボタン](/help/sites-cloud/authoring/assets/delete.png)

   >[!NOTE]
   >
   >セキュリティ対策のため、**削除**&#x200B;ページアイコンはクイックアクションとしては使用できません。

1. 確認を求めるダイアログが表示されます。

   ![削除ダイアログ](/help/sites-cloud/authoring/assets/delete-page.png)

   * **削除する前にページをアーカイブしますか？** - 選択すると、削除対象として選択したページのバージョンが削除時に作成されます。
      * [バージョンは、後日復元できます。](/help/sites-cloud/authoring/features/page-versions.md)
      * 以前のバージョンがない場合は、ページを復元できません。
   * **キャンセル**：アクションを停止します。
   * **削除**：アクションの実行を確定します。

      * ページに参照がない場合、ページは削除されます。
      * ページに参照がある場合は、メッセージボックスに「**1 つ以上のページが参照されています。**」と表示されます。「**削除を強制**」または「**キャンセル**」を選択できます。

>[!NOTE]
>
>ページが既に公開されている場合は、削除する前に自動的に非公開になります。

### ページのロック {#locking-a-page}

以下が可能です。 [ページのロック/ロック解除](/help/sites-cloud/authoring/fundamentals/editing-content.md#locking-a-page) コンソールから、または個々のページを編集する際に、 ページがロックされているかどうかに関する情報も、両方の場所に表示されます。

![「ロック」ボタン](/help/sites-cloud/authoring/assets/lock.png)![「ロック解除」ボタン](/help/sites-cloud/authoring/assets/unlock.png)

### 新しいフォルダーの作成 {#creating-a-new-folder}

ファイルやページの整理に役立つフォルダーを作成できます。

1. **Sites** コンソールを開いて、必要な場所まで移動します。
1. オプションリストを開くには、 **作成** ツールバーから
1. 選択 **フォルダー** をクリックしてダイアログを開きます。 ここで、「**名前**」と「**タイトル**」を入力できます。

   ![フォルダーを作成](/help/sites-cloud/authoring/assets/organizing-create-folder.png)

1. 「**作成**」を選択してフォルダーを作成します。

>[!NOTE]
>
>フォルダーは [ページ命名規則](#page-naming-conventions) 新しいフォルダ名を指定する場合。

>[!CAUTION]
>
>* フォルダーは、**Sites** 直下か、他のフォルダーの下にのみ作成できます。ページの下に作成することはできません。
>* 標準のアクション（移動、コピー、貼り付け、削除、公開、非公開、プロパティの表示／編集）は、フォルダーに対して実行できます。
>* ライブコピー内ではフォルダーを選択できません。

