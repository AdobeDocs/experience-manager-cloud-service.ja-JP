---
title: ページの作成と整理
description: AEMでページを作成し、整理する方法
translation-type: tm+mt
source-git-commit: 16725342c1a14231025bbc1bafb4c97f0d7cfce8

---


# ページの作成と整理 {#creating-and-organizing-pages}

This document describes how to create and manage pages with Adobe Experience Manager Cloud Service so that you can then [create content](/help/sites-cloud/authoring/fundamentals/editing-content.md) on those pages.

>[!NOTE]
>
>作成、コピー、移動、編集、削除など、ページに対してアクションを実行するには、アカウントに適切なアクセス権]と権限が必要です。
>
>問題が発生した場合は、システム管理者にお問い合わせください。

<!--
>Your account needs the [appropriate access rights](/help/sites-administering/security.md) and [permissions](/help/sites-administering/security.md#permissions) to take action on pages such as create, copy, move, edit, and delete.
-->

>[!TIP]
>
>Web サイトコンソールから使用できる[キーボードショートカット](/help/sites-cloud/authoring/getting-started/keyboard-shortcuts.md)が多数あり、ページをより効率的に整理できます。

## Web サイトの整理 {#organizing-your-website}

作成者は、AEM 内で Web サイトを構成する必要があります。この作業中に、次の目的でコンテンツページを作成して名前を付けます。

* 作成者がオーサー環境でコンテンツページを容易に検索できるようにする
* サイトへの訪問者がパブリッシュ環境でコンテンツページを容易に閲覧できるようにする

コンテンツの整理に役立つ[フォルダー](#creating-a-new-folder)を使用することもできます。

Webサイトの構造は、コンテンツページを保持するツリーと見なすことができます。 これらのコンテンツページの名前はURLの形成に使用され、ページコンテンツが表示されるとタイトルが表示されます。

次の例は、 [WKND Tutorialサイトの例です。このサイトでは、スケートパーク](https://docs.adobe.com/content/help/en/experience-manager-learn/getting-started-wknd-tutorial-develop/overview.html) ( `la-skateparks`)に関する記事にアクセスします。

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

This structure can be viewed From the **Sites** console, where you can [navigate through the pages of your website](/help/sites-cloud/authoring/getting-started/basic-handling.md#selecting-resources) and perform actions on the pages. 新しいサイトや[新しいページ](#creating-a-new-page)を作成することもできます。

どの地点からでも、ヘッダーバーのパンくず（経路表示）から上位のブランチを確認できます。

![パンくずリストを使用した移動](/help/sites-cloud/authoring/assets/organizing-breadcrumbs.png)

### ページ命名規則 {#page-naming-conventions}

新しいページを作成する際の主要なフィールドは 2 つあります。

* **[タイトル](#title)**:

   * これはコンソール内のユーザーに、編集中のページコンテンツの上部に表示されます。
   * このフィールドは必須です。

* **[名前](#name)**:

   * これは URI の生成に使用されます。
   * このフィールドへの入力はオプションです。指定しない場合、名前はタイトルから派生します。詳しくは、次の節、[ページ名の制限事項とベストプラクティス](#page-name-restrictions-and-best-practices)を参照してください。

#### ページ名の制限事項とベストプラクティス {#page-name-restrictions-and-best-practices}

ページの&#x200B;**タイトル**&#x200B;と&#x200B;**名前**&#x200B;は個別に作成できますが、次のように関連しています。。

* ページを作成するときは、「**タイトル**」フィールドのみ必要です。ページ作成時に&#x200B;**名前**&#x200B;が指定されない場合は、タイトルの最初の 64 文字から名前が生成されます（以下で設定する条件に従う）。ページ名を短くするというベストプラクティスに対応するため、最初の 64 文字のみ使用されます。
* 作成者がページ名を手動で指定する場合は、64 文字の制限は適用されませんが、ページ名の長さに関するその他の技術的制限が適用されることがあります。

>[!TIP]
>
>ページ名を定義するときは、ページ名をできるだけ簡潔にしつつ、読者がわかりやすいようにできるだけ表現力のある覚えやすいものにすることをお勧めします。詳しくは、[ 要素の ](https://www.w3.org/Provider/Style/TITLE.html)W3C スタイルガイド`title`を参照してください。
>
>また、一部のブラウザー（IE の旧バージョンなど）では、特定の長さまでの URL しか受け付けないので、ページ名を短くしておく技術的な理由もあります。

When creating a new page, AEM will validate the page name according to the conventions imposed by AEM and the JCR. <!--When creating a new page, AEM will [validate the page name according to the conventions](/help/sites-developing/naming-conventions.md) imposed by AEM and the JCR.-->

次の文字は使用できます。

* `a` through `z`
* `A` through `Z`
* `0` through `9`
* `_` (アンダースコア)
* `-` （ハイフン/マイナス）

Full details of all characters allowed can be found in the naming conventions. <!--Full details of all characters allowed can be found in [the naming conventions](/help/sites-developing/naming-conventions.md).-->

>[!NOTE]
>
>ページ名は150文字までに制限されます。

#### タイトル {#title}

新しいページを作成するときにページの&#x200B;**タイトル**&#x200B;のみを指定した場合、AEM ではページの&#x200B;**名前**&#x200B;がこの文字列から派生され、AEM と JCR によって課された規則に基づいてページ名が検証されます。<!--If you supply only a page **Title** when creating a new page, AEM will derive the page **Name** from this string and [validate the name according to the conventions](/help/sites-developing/naming-conventions.md) imposed by AEM and JCR.-->

A **Title** field containing invalid characters will be accepted, but the name derived will have the invalid characters substituted. 次に例を示します。

| タイトル | 派生された名前 |
|---|---|
| Schön | `schoen.html` |
| SC%&amp;*ç+ | `sc---c-.html` |

#### 名前 {#name}

新しいページを作成するときにページの&#x200B;**名前**&#x200B;を指定すると、AEM では AEM と JCR によって課された規則に基づいてページ名が検証されます。「**名前**」フィールドに無効な文字は指定できません。AEMが無効な文字を検出すると、フィールドがハイライト表示されます。 <!--When you supply a page **Name** when creating a new page, AEM will [validate the name according to the conventions](/help/sites-developing/naming-conventions.md) imposed by AEM and JCR. You cannot submit invalid characters in the **Name** field. When AEM detects invalid characters the field will be highlighted with an explanatory message.-->

![無効なページ名の入力例](/help/sites-cloud/authoring/assets/organizing-invalid-name.png)

>[!TIP]
>
>ISO-639-1 で定義されている 2 文字コードをページ名として使用することは避けてください（言語ルートの場合を除く）。
>
>詳しくは、翻訳するコンテンツの準備を参照してください。
<!--
>See [Preparing Content for Translation](/help/sites-administering/tc-prep.md) for more information.
-->

### テンプレート {#templates}

AEM では、テンプレートはページの特殊なタイプを指定するものです。テンプレートは、作成中のあらゆる新規ページの基礎として使用されます。

テンプレートによって、サムネイル画像やその他のプロパティなど、ページの構造が定義されます。例えば、商品ページ、サイトマップおよび問い合わせ先に、それぞれ別のテンプレートを使用することができます。テンプレートは、[コンポーネント](#components)で構成されています。

AEM では、複数のテンプレートが標準提供されています。使用可能なテンプレートは個々の Web サイトによって異なります。主なフィールドは次のとおりです。

* **タイトル**
生成される Web ページに表示されるタイトルです。

* **名前**
ページに名前を付ける際に使用されます。

* **テンプレート**
新しいページを生成する際に使用できるテンプレートのリストです。

>[!TIP]
>
>お使いのインスタンスで設定すると、[テンプレートの作成者はテンプレートエディターを使用してテンプレートを作成できます](/help/sites-cloud/authoring/features/templates.md)。

### コンポーネント {#components}

コンポーネントは、AEM で提供される、特定のタイプのコンテンツを追加できる要素です。AEMには、包括的な機能を提供する標準搭載の各種コンポーネントが付属しています。以下が含まれます。

* テキスト
* 画像
* タイトル
* カルーセル
* およびその他のコンポーネント

ページを作成して開いたら、[コンポーネントブラウザー](/help/sites-cloud/authoring/fundamentals/environment-tools.md#components-browser)から取得できる[コンポーネントを使用してコンテンツを追加](/help/sites-cloud/authoring/fundamentals/editing-content.md#inserting-a-component)できます。

>[!TIP]
>
>[コンポーネントコンソール](/help/sites-cloud/authoring/features/components-console.md)は、インスタンス上のコンポーネントの概要を示します。

## ページの管理 {#managing-pages}

### 新しいページの作成 {#creating-a-new-page}

すべてのページが事前に作成されていない限り、コンテンツの作成を開始する前にページを作成する必要があります。

1. Open the Sites console (for example, `https://<host>:<port>/sites.html/content`.
1. 新しいページを作成する場所に移動します。
1. ツールバーの「**作成**」を使用してドロップダウンセレクターを開き、リストから「**ページ**」を選択します。

   ![ページの作成](/help/sites-cloud/authoring/assets/organizing-create-page.png)

1. ウィザードの最初のステージで、次のいずれかを実行できます。

   * 新しいページの作成時に使用するテンプレートを選択し、「**次へ**」をクリックまたはタップして次に進みます。

   * 「**キャンセル**」を使用してプロセスを中止します。
   ![新しいページのテンプレートの選択](/help/sites-cloud/authoring/assets/organizing-create-page-template.png)

1. ウィザードの最後のステージで、次のいずれかを実行できます。

   * 3 つのタブを使用して、新しいページに割り当てる[ページプロパティ](/help/sites-cloud/authoring/fundamentals/page-properties.md)を入力し、「**作成**」をクリックまたはタップしてページを実際に作成します。

   * 「**戻る**」を使用してテンプレートの選択に戻ります。
   主なフィールドは次のとおりです。

   * **タイトル**:

      * ユーザーに表示される必須のフィールドです。
   * **名前**:

      * これは URI の生成に使用されます。指定しない場合、名前はタイトルから派生します。
      * If you supply a page **Name** when creating a new page, AEM will validate the name according to the conventions imposed by AEM and JCR. <!--If you supply a page **Name** when creating a new page, AEM will [validate the name according to the conventions](/help/sites-developing/naming-conventions.md) imposed by AEM and JCR.-->
      * 「**名前**」フィールドに&#x200B;**無効な文字は指定できません**。AEM で無効な文字が検出されると、そのフィールドは強調表示され、対象の文字を削除または置換する必要があることを示す説明メッセージが表示されます。
   >[!TIP]
   >
   >[ページ命名規則](#page-naming-conventions)を参照してください。

   新しいページの作成に必要となる最小限の情報は、「**タイトル**」です。

   ![ページタイトルの指定](/help/sites-cloud/authoring/assets/organizing-create-page-title.png)

1. 「**作成**」を使用してプロセスを完了し、新しいページを作成します。ページをすぐに「**開く**」かコンソールに戻る（「**完了**」する）かを確認するダイアログが表示されます。

   ![ページ作成の成功](/help/sites-cloud/authoring/assets/organizing-create-page-success.png)

   >[!NOTE]
   >
   >ページの作成先に同名のページが既に存在する場合は、その名前のバリエーションが数字を付加して自動的に生成されます。例えば、`beach` が既に存在する場合、新しいページは `beach1` になります。

1. コンソールに戻ると、新しいページが表示されます。

   ![新しいページの作成](/help/sites-cloud/authoring/assets/organizing-create-page-result.png)

>[!CAUTION]
>
>Once a page has been created its template cannot be changed - unless you [create a launch with a new template](/help/sites-cloud/authoring/launches/creating.md#create-launch-with-new-template), though this will lose any existing content.

### ページを開いて編集 {#opening-a-page-for-editing}

ページを作成した後、または（コンソールで）既存のページに移動した後、そのページを開いて編集できます。

1. **サイト**&#x200B;コンソールを開きます。
1. 編集対象のページが表示されるまで移動します。
1. 次のいずれかを使用してページを選択します。

   * [クイックアクション](/help/sites-cloud/authoring/getting-started/basic-handling.md#quick-actions)
   * [選択モード](/help/sites-cloud/authoring/getting-started/basic-handling.md#selecting-resources)とツールバー
   And then select the **Edit** icon:

   「![編集」ボタン](/help/sites-cloud/authoring/assets/edit.png)

1. ページが開き、必要に応じて[編集](/help/sites-cloud/authoring/fundamentals/editing-content.md)できるようになります。

>[!NOTE]
>
>ページエディターから他のページへの移動は、編集モードではリンクがアクティブにならないので、プレビューモードでのみ実行できます。

### ページのコピーと貼り付け {#copying-and-pasting-a-page}

ページとそのすべてのサブページを新しい場所にコピーできます。

1. **サイト**&#x200B;コンソールで、コピー対象のページが表示されるまで移動します。
1. 次のいずれかを使用してページを選択します。

   * [クイックアクション](/help/sites-cloud/authoring/getting-started/basic-handling.md#quick-actions)
   * [選択モード](/help/sites-cloud/authoring/getting-started/basic-handling.md#selecting-resources)とツールバー
   「**コピー**」ページアイコンを選択します。

   ![コピーボタン](/help/sites-cloud/authoring/assets/copy.png)

   >[!NOTE]
   >
   >選択モードの場合は、ページのコピー後に選択モードが自動的に終了します。

1. ページの新しいコピーを配置する場所に移動します。
1. **貼り付け**&#x200B;ページアイコンを使用します。

   ![貼り付けボタン](/help/sites-cloud/authoring/assets/paste.png)

   元のページとサブページのコピーがこの場所に作成されます。

   >[!NOTE]
   >
   >ページのコピー先に同名のページが既に存在する場合は、その名前のバリエーションが数字を付加して自動的に生成されます。例えば、既に存 `beach` 在する場合は、名前を持つ新しいページが `beach` 表示されま `beach1`す。

### ページの移動または名前の変更 {#moving-or-renaming-a-page}

ページの移動手順と名前の変更手順は基本的に同じで、同じウィザードで処理します。このウィザードでは、次の操作をおこなうことができます。

* ページを移動せずに名前を変更する
* 名前を変更せずにページを移動する
* 同時に移動して名前を変更

AEM では、名前変更または移動がおこなわれるページへの内部リンクを更新する機能が用意されています。この機能はページ単位で実行できるので、非常に柔軟性があります。

1. 移動対象のページが表示されるまで移動します。
1. 次のいずれかを使用してページを選択します。

   * [クイックアクション](/help/sites-cloud/authoring/getting-started/basic-handling.md#quick-actions)
   * [選択モード](/help/sites-cloud/authoring/getting-started/basic-handling.md#selecting-resources)とツールバー
   「**移動**」ページアイコンをクリックします。

   ![移動ボタン](/help/sites-cloud/authoring/assets/move.png)

   これにより、ページを移動ウィザードが開きます。

1. ウィザードの&#x200B;**名前を変更**&#x200B;ステージで、次のいずれかを実行できます。

   * 移動後にページに付ける名前を指定し、「**次へ**」をクリックまたはタップして次に進みます。
   * 「**キャンセル**」を使用してプロセスを中止します。
   ![ページの移動と名前の変更](/help/sites-cloud/authoring/assets/move-page-rename.png)

   ページを移動するだけの場合は、ページ名はそのままにできます。

   >[!NOTE]
   >
   >ページの移動先に同名のページが既に存在する場合は、その名前のバリエーションが数字を付加して自動的に生成されます。例えば、既に存 `beach` 在する場合は、名前を持つ新しいページが `beach` 表示されま `beach1`す。

1. ウィザードの&#x200B;**宛先を選択**&#x200B;ステージで、次のいずれかを実行できます。

   * [列表示](/help/sites-cloud/authoring/getting-started/basic-handling.md#column-view)を使用して、ページの新しい場所に移動します。

      * 移動先のサムネイルをクリックして、移動先を選択します。
      * 「**次へ**」をクリックして次に進みます。
   * 「**戻る**」を使用してページ名の指定に戻ります。
   >[!NOTE]
   >
   >デフォルトでは、移動または名前変更するページの親が、移動先として選択されます。

   ![ページ移動先の選択](/help/sites-cloud/authoring/assets/move-page-destination.png)

   >[!NOTE]
   >
   >ページの移動先に同名のページが既に存在する場合は、その名前のバリエーションが数字を付加して自動的に生成されます。例えば、既に存在す `winter` る場合は、 `winter` が表示されま `winter1`す。

1. ページがリンクまたは参照されている場合、またはページが公開されている場合は、詳細が&#x200B;**調整 / 再公開**&#x200B;ステップで一覧表示されます。

   調整または再公開するページを適宜指定できます。

   >[!NOTE]
   >
   >ページがリンクも参照もされていない場合は、このステップは使用できません。

   ![移動時にページを再公開](/help/sites-cloud/authoring/assets/move-page-republish.png)

1. 「**移動**」を選択すると、プロセスが完了し、ページの移動または名前変更が適宜確定されます。

>[!NOTE]
>
>ページが既に公開されている場合、ページを移動すると自動的に非公開になります。By default, it will be republished when the move is complete, but this can changed by un-checking the **Republish** field in the **Adjust/Republish** step.

>[!NOTE]
>
>ページが参照されていない場合は、**調整 / 再公開**&#x200B;手順がスキップされます。

>[!NOTE]
>
>ページ名の変更で新しいページ名を指定する際にも、[ページ命名規則](#page-naming-conventions)に従います。

>[!NOTE]
>
>ページは、ページが基にしているテンプレートが許可される場所にのみ移動できます。詳しくは、テンプレートの利用可能性を参照してください。
<!--
>A page can only be moved to a location where the template upon which the page is based is allowed. See [Template Availability](/help/sites-developing/templates.md#template-availability) for more information.
-->

### ページの削除 {#deleting-a-page}

1. 削除対象のページが表示されるまで移動します。
1. [選択モード](/help/sites-cloud/authoring/getting-started/basic-handling.md#viewing-and-selecting-resources)を使用して必要なページを選択してから、ツールバーの「**削除**」を使用します。

   ![削除ボタン](/help/sites-cloud/authoring/assets/delete.png)

   >[!NOTE]
   >
   >セキュリティ対策のため、**削除**&#x200B;ページアイコンはクイックアクションとしては使用できません。

1. 確認を求めるダイアログが表示されます。次のように実行できます。

   * 「**キャンセル**」で、アクションを中止します。
   * 「**削除**」で、アクションの実行を確定します。

      * ページに参照がない場合は、ページが削除されます。
      * ページに参照がある場合は、メッセージボックスに「**1 つ以上のページが参照されています。**」と表示されます。「**削除を強制**」または「**キャンセル**」を選択できます。

>[!NOTE]
>
>ページが既に公開されている場合は、削除前に自動的に公開が取り消されます。

### ページのロック {#locking-a-page}

コンソールから、または個々のページの編集時に[ページをロック／ロック解除](/help/sites-cloud/authoring/fundamentals/editing-content.md#locking-a-page)できます。ページがロックされているかどうかに関する情報も、両方の場所で示されます。

![ロックボタン](/help/sites-cloud/authoring/assets/lock.png)![ロック解除ボタン](/help/sites-cloud/authoring/assets/unlock.png)

### 新しいフォルダーの作成 {#creating-a-new-folder}

ファイルやページの整理に役立つフォルダーを作成できます。

1. **サイト**&#x200B;コンソールを開いて、必要な場所まで移動します。
1. オプションリストを開くには、ツールバーの「**作成**」を選択します。
1. 「**フォルダー**」を選択してダイアログを開きます。ここで、「**名前**」と「**タイトル**」を入力できます。

   ![フォルダーを作成](/help/sites-cloud/authoring/assets/organizing-create-folder.png)

1. 「**作成**」を選択してフォルダーを作成します。

>[!NOTE]
>
>フォルダーに新しいフォルダー名を指定する際にも、[ページ命名規則](#page-naming-conventions)に従います。

>[!CAUTION]
>
>* フォルダーは、**サイト**&#x200B;直下か、他のフォルダーの下にのみ作成できます。ページの下には作成できません。
>* 標準的なアクションの移動、コピー、貼り付け、削除、発行、非公開、表示/編集の各プロパティは、フォルダーに対して実行できます。
>* ライブコピー内ではフォルダーを選択できません。

