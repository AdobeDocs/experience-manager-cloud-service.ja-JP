---
title: ページの作成と整理
description: AEMでページを作成および管理して、Web サイトを整理する方法について説明します。
exl-id: c57096ca-34fe-4b19-98e0-8f3cd43cf24e
source-git-commit: bc3c054e781789aa2a2b94f77b0616caec15e2ff
workflow-type: tm+mt
source-wordcount: '2429'
ht-degree: 86%

---


# ページの作成と整理 {#creating-and-organizing-pages}

このドキュメントでは、Adobe Experience Manager as a Cloud Service でページを作成および管理して、それらのページの[コンテンツを作成](/help/sites-cloud/authoring/fundamentals/editing-content.md)できるようにする方法について説明します。

>[!NOTE]
>
>ページに対して実行する適切なアクセス権と権限（作成、コピー、移動、編集、削除など）を持つアカウントが必要です。
>
>問題が発生した場合は、システム管理者にお問い合わせください。

<!--
>Your account needs the [appropriate access rights](/help/sites-administering/security.md) and [permissions](/help/sites-administering/security.md#permissions) to act on pages such as create, copy, move, edit, and delete.
-->

>[!TIP]
>
>次の項目があります。 [キーボードショートカット](/help/sites-cloud/authoring/getting-started/keyboard-shortcuts.md) ページをより効率的に整理するために、web サイトコンソールから使用できます。

{{edge-delivery-authoring}}

## Web サイトの整理 {#organizing-your-website}

作成者は、AEM内で Web サイトを整理する必要があります。 この作業中に、次の目的でコンテンツページを作成して名前を付けます。

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

ページを作成する際の主なフィールドは 2 つあります。

* **[タイトル](#title)**：

   * これはコンソール内のユーザーに、編集中のページコンテンツの上部に表示されます。
   * このフィールドは必須です。

* **[名前](#name)**：

   * これは URI の生成に使用されます。
   * このフィールドへの入力はオプションです。指定しない場合、名前はタイトルから派生します。詳しくは、次の節、[ページ名の制限事項とベストプラクティス](#page-name-restrictions-and-best-practices)を参照してください。

#### ページ名の制限事項とベストプラクティス {#page-name-restrictions-and-best-practices}

ページの&#x200B;**タイトル**&#x200B;と&#x200B;**名前**&#x200B;は個別に作成できますが、次のように関連しています。

* ページを作成する場合、「**タイトル**」フィールドは必須です。ページの作成時に&#x200B;**名前**&#x200B;が指定されない場合、AEM はタイトルの最初の 64 文字から名前を生成します（以下で設定する条件に従う）。ページ名を短くするというベストプラクティスに対応するため、最初の 64 文字のみが使用されます。
* 作成者がページ名を手動で指定する場合は、64 文字の制限は適用されませんが、ページ名の長さに関するその他の技術的制限が適用されることがあります。

>[!TIP]
>
>ページ名を定義するときは、ページ名をできるだけ簡潔にしつつ、読者がわかりやすいようにできるだけ表現力のある覚えやすいものにすることをお勧めします。詳しくは、[ 要素の ](https://www.w3.org/Provider/Style/TITLE.html)W3C スタイルガイド`title`を参照してください。
>
>また、一部のブラウザー（旧バージョンの IE など）では、特定の長さまでの URL しか受け付けないので、ページ名を短くするには技術的な理由もあります。

ページを作成する際に、AEM [の規則に従ってページ名を検証します。](/help/implementing/developing/introduction/naming-conventions.md) AEMと JCR によって課せられます。

使用できる最低限の文字は次のとおりです。

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

ページのみを指定する場合 **タイトル** ページを作成する場合、AEMはページを派生します **名前** この文字列から、および [規則に従って名前を検証する](/help/implementing/developing/introduction/naming-conventions.md) AEMと JCR によって課せられます。

「**タイトル**」フィールドに無効な文字が含まれていてもエラーにはなりませんが、派生された名前では、無効な文字が別の文字に置き換えられます。次に例を示します。

| タイトル | 派生した名前 |
|---|---|
| Schön | `schoen.html` |
| SC%&amp;&#42;ç+ | `sc---c-.html` |

#### 名前 {#name}

ページを指定する場合 **名前** ページを作成する際に、AEM [の規則に従って名前を検証します。](/help/implementing/developing/introduction/naming-conventions.md) AEMと JCR によって課せられます。 「**名前**」フィールドに無効な文字は指定できません。AEM で無効な文字が検出されると、フィールドが強調表示され、説明メッセージが表示されます。

![無効なページ名の入力例](/help/sites-cloud/authoring/assets/organizing-invalid-name.png)

>[!TIP]
>
>ISO-639-1 で定義されている 2 文字コードをページ名として使用することは避けてください（言語ルートの場合を除く）。
>
>詳しくは、[翻訳するコンテンツの準備](/help/sites-cloud/administering/translation/preparation.md)を参照してください。

### テンプレート {#templates}

AEM では、テンプレートはページの特殊なタイプを指定します。テンプレートは、作成中のあらゆる新規ページの基礎として使用されます。

テンプレートによって、サムネール画像やその他のプロパティなど、ページの構造が定義されます。例えば、商品ページ、サイトマップおよび問い合わせ先に、それぞれ別のテンプレートを使用することができます。テンプレートは、[コンポーネント](#components)で構成されています。

AEM では、複数のテンプレートが標準提供されています。使用できるテンプレートは、個々の web サイトによって異なります。主なフィールドは次のとおりです。

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

ページを作成して開くと、[コンポーネントブラウザー](/help/sites-cloud/authoring/fundamentals/environment-tools.md#components-browser)から使用可能な[コンポーネントを使用してコンテンツを追加](/help/sites-cloud/authoring/fundamentals/editing-content.md#inserting-a-component)できます。

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

1. ウィザードの最初のステージで、次のいずれかを実行できます。

   * 新しいページの作成に使用するテンプレートを選択し、「 」を選択します。 **次へ** をクリックして続行します。

   * 「**キャンセル**」を使用してプロセスを中止します。

   ![新しいページのテンプレートの選択](/help/sites-cloud/authoring/assets/organizing-create-page-template.png)

1. ウィザードの最後のステージで、次のいずれかを実行できます。

   * 3 つのタブを使用して、 [ページのプロパティ](/help/sites-cloud/authoring/fundamentals/page-properties.md) 新しいページに割り当てる場合は、「 」を選択します。 **作成** をクリックして、実際にページを作成します。

   * 「**戻る**」を使用してテンプレートの選択に戻ります。

   主なフィールドは次のとおりです。

   * **タイトル**：

      * ユーザーに表示される、必須のフィールドです。

   * **名前**：

      * これは URI の生成に使用されます。指定しない場合、名前はタイトルから派生します。
      * ページを指定する場合 **名前** ページを作成する際に、AEM [の規則に従って名前を検証します。](/help/implementing/developing/introduction/naming-conventions.md) AEMと JCR によって課せられます。
      * 「**名前**」フィールドに&#x200B;**無効な文字は指定できません**。AEM で無効な文字が検出されると、そのフィールドは強調表示され、対象の文字を削除または置換する必要があることを示す説明メッセージが表示されます。

   >[!TIP]
   >
   > [ページ命名規則](#page-naming-conventions)を参照してください。

   ページの作成に最低限必要な情報は、 **タイトル**.

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
1. 編集対象のページが表示されるまで移動します。
1. 次のいずれかを使用してページを選択します。

   * [クイックアクション](/help/sites-cloud/authoring/getting-started/basic-handling.md#quick-actions)
   * [選択モード](/help/sites-cloud/authoring/getting-started/basic-handling.md#selecting-resources)とツールバー

   その後、「**編集**」アイコンを選択します。

   ![「編集」ボタン](/help/sites-cloud/authoring/assets/edit.png)

1. ページが開き、必要に応じて[ページを編集](/help/sites-cloud/authoring/fundamentals/editing-content.md)できます。

>[!NOTE]
>
>ページエディターから他のページへの移動は、編集モードではリンクがアクティブにならないので、プレビューモードでのみ実行できます。

### ページのコピーと貼り付け {#copying-and-pasting-a-page}

ページとそのすべてのサブページを新しい場所にコピーできます。

1. **Sites** コンソールで、コピー対象のページが表示されるまで移動します。
1. 次のいずれかを使用してページを選択します。

   * [クイックアクション](/help/sites-cloud/authoring/getting-started/basic-handling.md#quick-actions)
   * [選択モード](/help/sites-cloud/authoring/getting-started/basic-handling.md#selecting-resources)とツールバー

   「**コピー**」ページアイコンを選択します。

   ![コピー](/help/sites-cloud/authoring/assets/copy.png)

1. ページの新しいコピーを配置する場所に移動します。
1. を選択します。 **貼り付け** アイコンが表示されます。

   ![貼り付け](/help/sites-cloud/authoring/assets/paste.png)

1. 貼り付けダイアログには、貼り付けトランザクションの概要のほか、次の機能が表示されます。
   * **新規サイト名**：貼り付けたページの名前を変更します。
   * **子を含めずに貼り付け**：貼り付け時に、選択したページの子ページを除外します（デフォルトでは子ページも貼り付けられます）。

   ![貼り付けダイアログ](/help/sites-cloud/authoring/assets/paste-dialog.png)

1. を選択します。 **貼り付け** ボタンをクリックして貼り付けトランザクションを確定し、新しいページを作成します。

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

AEM では、名前変更または移動が行われるページへの内部リンクを更新する機能が用意されています。この機能はページ単位で実行できるので、非常に柔軟性があります。

1. 移動対象のページが表示されるまで移動します。
1. 次のいずれかを使用してページを選択します。

   * [クイックアクション](/help/sites-cloud/authoring/getting-started/basic-handling.md#quick-actions)
   * [選択モード](/help/sites-cloud/authoring/getting-started/basic-handling.md#selecting-resources)とツールバー

   次に、「**移動**」ページアイコンを選択します。

   ![「移動」ボタン](/help/sites-cloud/authoring/assets/move.png)

   ページの移動ウィザードが開きます。

1. ウィザードの&#x200B;**名前の変更**&#x200B;ステージで、次のいずれかを実行できます。

   * 移動後にページに表示する名前を指定し、「 **次へ** をクリックして続行します。
   * 「**キャンセル**」を使用してプロセスを中止します。

   ![ページの移動と名前変更](/help/sites-cloud/authoring/assets/move-page-rename.png)

   ページを移動するだけの場合は、ページ名はそのままにできます。

   >[!NOTE]
   >
   >ページの移動先に同名のページが既に存在する場合は、その名前のバリエーションが数字を付加して自動的に生成されます。例えば、`beach` が既に存在する場合は、`beach` という名前の新しいページは `beach1` になります。

1. ウィザードの&#x200B;**宛先を選択**&#x200B;ステージで、次のいずれかを実行できます。

   * [列表示](/help/sites-cloud/authoring/getting-started/basic-handling.md#column-view)を使用して、次のようにページの新しい場所に移動します。

      * 移動先のサムネールをクリックして、移動先を選択します。
      * 「**次へ**」をクリックして次に進みます。

   * 「**戻る**」を使用してページ名の指定に戻ります。

   >[!NOTE]
   >
   >デフォルトでは、移動または名前変更するページの親が、移動先として選択されます。

   ![ページの移動先の選択](/help/sites-cloud/authoring/assets/move-page-destination.png)

   >[!NOTE]
   >
   >ページの移動先に同名のページが既に存在する場合は、その名前のバリエーションが数字を付加して自動的に生成されます。例えば、`winter` が既に存在する場合、`winter` は `winter1` になります。

1. ページがリンクまたは参照されている場合、またはページが公開されている場合は、詳細が&#x200B;**調整／再公開**&#x200B;手順で一覧表示されます。

   調整または再公開するページを適宜指定できます。

   >[!NOTE]
   >
   >ページがリンクも参照もされていない場合は、このステップは使用できません。

   ![移動時のページ再公開](/help/sites-cloud/authoring/assets/move-page-republish.png)

1. 「**移動**」を選択するとプロセスが完了し、必要に応じてページを移動または名前変更します。

>[!NOTE]
>
>ページを既に公開している場合、ページを移動すると自動的に非公開になります。デフォルトでは、移動が完了すると再公開されますが、**調整／再公開**&#x200B;手順の「**再公開**」フィールドをオフにすることによって変更できます。

>[!NOTE]
>
>ページがまったく参照されていない場合は、**調整／再公開**&#x200B;手順がスキップされます。

>[!NOTE]
>
>ページ名の変更で新しいページ名を指定する際にも、[ページ命名規則](#page-naming-conventions)に従います。

>[!NOTE]
>
>ページは、ページの基となるテンプレートが許可されている場所にのみ移動できます。詳しくは、[使用可能なテンプレート](/help/implementing/developing/components/templates.md#template-availability)を参照してください。

#### 非同期アクション {#asynchronous-actions}

ページ移動アクションは常に非同期で処理されるので、ユーザーは UI でオーサリングを妨げずに続行できます。

* ユーザーは、非同期操作を実行するタイミングを定義する必要があります
   * **今すぐ**：非同期ジョブの実行を今すぐ開始します。
   * **後で**：非同期ジョブを開始するタイミングをユーザーが定義できます。

<!--
  ![Asynchronous page move](assets/asynchronous-page-move.png)
-->

非同期ジョブのステータスは、 [**非同期ジョブステータス** dashboard](/help/operations/asynchronous-jobs.md#monitor-the-status-of-asynchronous-operations) 時刻 **グローバルナビゲーション** > **ツール** > **運用** > **ジョブ**

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
      * [バージョンは、後日復元できます](/help/sites-cloud/authoring/features/page-versions.md)。
      * 以前のバージョンがない場合は、ページを復元できません。
   * **キャンセル**：アクションを停止します。
   * **削除**：アクションの実行を確定します。

      * ページに参照がない場合、ページは削除されます。
      * ページに参照がある場合は、メッセージボックスに「**1 つ以上のページが参照されています。**」と表示されます。「**削除を強制**」または「**キャンセル**」を選択できます。

>[!NOTE]
>
>ページが既に公開されている場合は、削除する前に自動的に非公開になります。

### ページのロック {#locking-a-page}

コンソールから、または個々のページの編集時に[ページをロック／ロック解除](/help/sites-cloud/authoring/fundamentals/editing-content.md#locking-a-page)できます。ページがロックされているかどうかに関する情報も、両方の場所で示されます。

![「ロック」ボタン](/help/sites-cloud/authoring/assets/lock.png)![「ロック解除」ボタン](/help/sites-cloud/authoring/assets/unlock.png)

### 新しいフォルダーの作成 {#creating-a-new-folder}

ファイルやページの整理に役立つフォルダーを作成できます。

1. **Sites** コンソールを開いて、必要な場所まで移動します。
1. オプションリストを開くには、ツールバーの「**作成**」を選択します。
1. 「**フォルダー**」を選択して、ダイアログを開きます。ここで、「**名前**」と「**タイトル**」を入力できます。

   ![フォルダーを作成](/help/sites-cloud/authoring/assets/organizing-create-folder.png)

1. 「**作成**」を選択してフォルダーを作成します。

>[!NOTE]
>
>フォルダーに新しいフォルダー名を指定する際にも、[ページ命名規則](#page-naming-conventions)に従います。

>[!CAUTION]
>
>* フォルダーは、**Sites** 直下か、他のフォルダーの下にのみ作成できます。ページの下には作成できません。
>* 標準のアクション（移動、コピー、貼り付け、削除、公開、非公開、プロパティの表示／編集）は、フォルダーに対して実行できます。
>* ライブコピー内ではフォルダーを選択できません。
