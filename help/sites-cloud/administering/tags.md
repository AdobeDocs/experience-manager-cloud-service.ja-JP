---
title: タグの管理
description: AEMでタグを管理してコンテンツを整理する方法を説明します。
exl-id: 42480699-b7a7-4678-a763-569a9b7573e2
source-git-commit: bc3c054e781789aa2a2b94f77b0616caec15e2ff
workflow-type: tm+mt
source-wordcount: '2210'
ht-degree: 5%

---

# タグの管理 {#administering-tags}

タグは、コンテンツを分類する直感的な方法です。 これらは、コンテンツをより迅速に見つけるためのキーワードまたはラベル（メタデータ）と考えることができます。

Adobe Experience Manager(AEM) では、タグは次のプロパティになります。

* ページのコンテンツノード
   * ドキュメントを見る [タグの使用](/help/sites-cloud/authoring/features/tags.md) を参照してください。
* アセットのメタデータノード
   * ドキュメントを見る [デジタルアセットのメタデータの管理](/help/assets/manage-metadata.md) を参照してください。

>[!TIP]
>
>同じアイデアに関連するタグの数を最小限に抑えることをお勧めします。 例えば、屋外用品店のコンテンツを管理している場合、両方にタグを付ける必要がない可能性があります **履き物** および **靴**.

## タグ機能 {#tag-features}

タグは、コンテンツを整理および管理するための堅牢な機能を提供します。

* タグは様々な名前空間にグループ化できます。
   * 名前空間は、分類を構築できる階層と考えることができます。
   * これらの分類は、AEM全体でグローバルです。
* 作成者がタグを適用し、サイト訪問者が使用できます。
* 作成者に関係なく、ページに割り当てたとき、または検索時に、すべての形式のタグが選択可能になります。
* タグは、 [リストコンポーネント](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/wcm-components/list.html?lang=ja) 選択したタグに基づいて動的リストを生成します。

## タグ要件 {#requirements}

タグを作成および管理する際に注意すべき技術的な詳細がいくつかあります。

* タグは、特定の名前空間内で一意である必要があります。
* タグの名前にタグ区切り文字を含めることはできません。
   * コロン (`:`) — 名前空間タグを区切ります。
   * スラッシュ (`/`) — サブタグを区切ります。
* タグのタイトルにタグ区切り文字が含まれている場合、UI では省略されます。
* タグを作成し、その分類を `tag-administrators` 変更権限を持つグループおよびメンバー `/content/cq:tags`.
   * 子タグを含むタグは、コンテナタグと呼ばれます。
   * コンテナタグではないタグは、リーフタグと呼ばれます。
   * タグ名前空間は、リーフタグまたはコンテナタグのどちらでもかまいません。

タグの動作方法に関する技術的な詳細については、 [AEM Tagging Framework](/help/implementing/developing/introduction/tagging-framework.md).

## タグ付けコンソール {#tagging-console}

タグ付けコンソールは、タグとその分類の作成および管理に使用します。 タグ付けコンソールを使用すると、次の方法でタグを管理できます。

* 名前空間にグループ化します。
* 新しいタグを作成する前に、既存のタグの使用状況を確認します。
* 現在参照されているコンテンツからタグを切断せずにタグを整理し直す。

タグ付けコンソールにアクセスするには：

1. 管理者権限を使用してオーサリング環境にログインします。
1. グローバルナビゲーションメニューで、 **`Tools`** > **`General`** ->
   **`Tagging`**。

![AEMのタグ付けコンソール](/help/sites-cloud/administering/assets/tagging-console.png)

## 新しいタグの作成 {#creating-new-tags}

タグを作成して使用してコンテンツを整理するには、いくつかの手順があります。

1. [タグ用の名前空間を作成する](#creating-namespaces) （または、再利用する既存のものを選択します）。
1. [新しいタグを作成します。](#creating-tags)
1. [タグを公開します。](#publishing-tags)

### 名前空間の作成 {#creating-namespaces}

名前空間は、他のタグの整理に使用されます。 これは最下位レベルのタグと見なすことができ、通常は他のタグをグループ化するために使用されます。

1. 名前空間を作成するには、 [タグ付けコンソール](#tagging-console) をクリックし、 **作成** ボタンをツールバーに追加し、 **名前空間を作成**.

   ![名前空間を追加ダイアログ](/help/sites-cloud/administering/assets/add-namespace.png)

1. 必要な情報を入力します。

   * **タイトル** - UI でユーザーに表示される名前空間のタイトル（オプション）
   * **名前**  — 名前が指定されていない場合、有効なノード名は **タイトル**. ドキュメントを見る [AEM Tagging Framework](/help/implementing/developing/introduction/tagging-framework.md#tagid) を参照してください。
   * **説明**  — 名前空間の説明（オプション）

1. 必要な情報を入力したら、 **作成**.

名前空間が作成されます。 タグ付けコンソールでは、名前空間は最も低いレベル（コンソールの左端の列）にあり、フォルダーアイコンで表され、その特性が「コンテナ」や他のタグのグループ化として反映されます。

次の操作を実行できます。 [新しいタグを作成](#creating-tags) この名前空間または [既存のタグを管理します。](#managing-tags)

名前空間にサブタグを含める必要はありません。 名前空間自体はタグなので、コンテンツを他のタグとして整理するために使用できます。 ただし、構造化タグ付け分類の作成を続けるには、次の操作を行います。 [サブタグの作成](#creating-tags) を、プロジェクト要件に基づく名前空間内に追加します。

### タグの作成 {#creating-tags}

タグは通常、名前空間に追加されます。

1. タグを作成するには、 [タグ付けコンソール。](#tagging-console)

1. タグを作成する名前空間を選択します。 または、別のタグを選択して、その下にサブタグを作成します。

1. を選択します。 **作成** ボタンを使用して、 **タグを作成**.

1. The **タグを作成** ダイアログが開きます。 新しいタグに必要な情報を入力します。

   * **タイトル**  — タグの表示タイトル（必須）
   * **名前**  — タグの名前（必須）。 指定しなかった場合、有効なノード名が **タイトル**. [タグ ID](/help/implementing/developing/introduction/tagging-framework.md#tagid) を参照してください。
   * **説明**  — タグの説明
   * **タグのパス**  — デフォルトは、タグ付けコンソールで選択した名前空間（またはタグ）です。 これは、パスセレクターアイコンをタップまたはクリックして、手動で更新できます。

   ![タグを作成ダイアログ](assets/create-tag.png)

1. 「**送信**」を選択します。

タグが作成され、コンソールが更新されて新しいタグが表示されます。

タグを使用すると、組織のニーズに基づいた独自の分類を柔軟に作成できます。

* 新しいタグを作成する前にコンソールで親タグを選択することで、既存のタグの子タグを作成できます。
* 名前空間や別のタグを選択せずにタグを作成する場合は、名前空間を効果的に作成できます。

### タグの公開 {#publishing-tags}

AEMで他のコンテンツを作成する場合と同様に、タグ（または名前空間）を作成した後は、オーサリング環境にのみ存在します。 タグをユーザーが使用できるようにするには、タグを公開する必要があります。

1. タグを公開するには、 [タグ付けコンソール。](#tagging-console)

1. 公開するタグを 1 つ以上選択し、ツールバーで「 」を選択します。 **公開**.

   ![コンソールでのタグの選択](assets/select-tags.png)

1. The **タグを公開** ダイアログで、選択したタグを公開するかどうかを確認する確認が表示されます。 選択 **公開**.

   ![公開タグの確認モーダル](assets/publish-tag.png)

1. 公開アクションが、 **成功** ダイアログ。

   ![タグの発行成功ダイアログ](assets/publish-tag-success.png)

選択したタグは、パブリッシュ用のキューに入っています。 ページコンテンツと同様、サブタグが付いているかどうかに関係なく、選択したタグのみが公開されます。

分類全体（名前空間とサブタグ）を公開する場合のベストプラクティスは、 [パッケージ](/help/implementing/developing/tools/package-manager.md) 名前空間の ( [分類のルートノード](/help/implementing/developing/introduction/tagging-framework.md#taxonomy-root-node)) をクリックします。

<!--
Be sure to [apply permissions](#setting-tag-permissions) to the namespace before creating the package.
-->

## タグの管理 {#managing-tags}

既存のタグや名前空間を管理および整理するために実行できるアクションがいくつかあります。 タグまたは名前空間を [タグ付けコンソール](#tagging-console) をクリックすると、使用可能なアクションがツールバーに表示されます。

* [プロパティを表示](#viewing-tag-properties)
* [編集](#editing-tags)
* [非公開](#unpublishing-tags)
* [参照](#viewing-tag-references)
* [移動](#moving-tags)
* [結合](#merging-tags)
* [削除](#deleting-tags)

ツールバーに十分なスペースがあるメモが表示された場合は、省略記号アイコンの後ろに追加のオプションが表示されます。

### タグプロパティの表示 {#viewing-tag-properties}

タグ付けコンソールで 1 つのタグまたは名前空間または他のタグを選択すると、最後の編集や最後の公開の時間など、選択したタグの基本的な詳細がタグ列の左側の列に表示されます。

![タグの詳細列](assets/tag-details-column.png)

コンソールを **プロパティ** 表示。

1. タグのプロパティを表示するには、 [タグ付けコンソール。](#tagging-console)

1. プロパティを表示するタグを選択し、左側のレールでを選択します。 **プロパティ**.

   ![プロパティビューの選択](assets/view-tag-properties.png)

1. 選択したタグの詳細なプロパティが左側のパネルに表示されます。

   ![タグプロパティの表示](assets/tag-properties.png)

表示モードとパネルの選択について詳しくは、 [基本操作](/help/sites-cloud/authoring/getting-started/basic-handling.md#rail-selector).

### タグの編集 {#editing-tags}

タグと名前空間は作成後に編集できます。

1. タグを編集するには、 [タグ付けコンソール。](#tagging-console)

1. 編集するタグを選択し、ツールバーでを選択します。 **編集**.

1. 必要な変更を加えます。 次の値を変更できます。

   * **タイトル**
   * **説明**
   * [**ローカライゼーション**](#managing-tags-in-different-languages)

1. 編集が完了したら、「 」を選択します。 **送信**.

言語の翻訳を追加する方法について詳しくは、[他の言語でのタグの管理](#managing-tags-in-different-languages)の節を参照してください。

変更が既に公開済みのタグに対して行われた場合は、 [再公開します。](#publishing-tags)

### タグの非公開 {#unpublishing-tags}

オーサーインスタンスでタグのアクティベートを解除し、パブリッシュインスタンスからタグを削除するには、タグを非公開にします。

1. タグを非公開にするには、 [タグ付けコンソール。](#tagging-console)

1. 非公開にするタグを 1 つ以上選択し、ツールバーでを選択します。 **非公開**.

   ![コンソールでのタグの選択](assets/select-tags.png)

1. The **タグを非公開にする** ダイアログで、選択したタグを公開するかどうかを確認する確認が表示されます。 選択 **公開**.

   ![公開タグの確認モーダル](assets/unpublish-tag.png)

1. 非公開アクションが、 **成功** ダイアログ。

   ![タグの発行成功ダイアログ](assets/unpublish-tag-success.png)

選択したタグは、非公開のキューに入れられています。 選択したタグがコンテナタグの場合、そのすべての子タグはオーサー環境で非アクティブ化され、パブリッシュ環境から削除されます。

### タグ参照の表示 {#viewing-tag-references}

これは、特定のタグが適用されるコンテンツを確認するのに役立ちます。 これをおこなうには、 **参照** タグ付けコンソールで表示します。

1. タグの参照を表示するには、 [タグ付けコンソール。](#tagging-console)

1. 参照を表示するタグを選択し、左側のレールでを選択します。 **参照**.

   ![プロパティビューの選択](assets/view-tag-references.png)

1. 選択したタグの参照の合計数が左側のパネルに表示されます。

   ![タグ参照の表示](assets/tag-references.png)

1. タグ参照の数を選択して、タグに割り当てられているコンテンツの詳細なリストを表示します。

   ![タグの参照の詳細の表示](assets/tag-references-detail.png)

リスト内の参照先のコンテンツにマウスポインターを置くかタップすると、コンテンツのフルパスが表示されます。

表示モードとパネルの選択について詳しくは、 [基本操作](/help/sites-cloud/authoring/getting-started/basic-handling.md#rail-selector).

### タグの移動 {#moving-tags}

タグを新しい場所に移動したり、タグの名前を変更したりして、タグ分類をクリーンアップしたり、整理し直したりする必要があります。

>[!TIP]
>
>タグの移動と名前の変更は、管理者のみが実行できることをお勧めします。

1. タグの移動や名前の変更を行うには、 [タグ付けコンソール。](#tagging-console)

1. 移動または名前を変更するタグを選択し、「 」を選択します。 **移動** 」と入力します。

1. Adobe Analytics の **タグを移動** ダイアログで、変更するプロパティを指定します。

   * **名前をに変更**  — タグに付ける新しい名前
      * このフィールドには、タグの現在の名前が事前に入力されます。
      * タグの移動のみを行い、名前を変更しない場合は、未変更のままにします。
   * **移動先**  — タグを移動する場所
      * このフィールドには、タグの現在の位置が事前に入力されます。
      * タグの名前のみを変更し、移動しない場合は、未変更のままにします。

   ![タグを移動](assets/move-tag.png)

1. 「**送信**」を選択します。

タグの名前が変更されたり、新しい場所に移動したりします。 選択されているタグがコンテナタグの場合、タグを移動すると、そのすべての子タグも移動されます。

### タグの結合 {#merging-tags}

タグ分類に類似した重複やタグがある場合は、それらのタグを結合すると便利です。 When タグ `A` をタグに結合します `B`（タグでタグ付けされたすべてのページ） `A` タグでタグ付けされる `B` およびタグ `A` は、作成者が使用できなくなりました。

1. 2 つのタグを結合するには、 [タグ付けコンソール。](#tagging-console)

1. 別のタグに統合するタグを選択し、「 」を選択します。 **結合** 」と入力します。

1. Adobe Analytics の **タグを結合** ダイアログで、 **参照** アイコン **結合先** フィールドを選択し、選択したタグを結合するタグを指定します。

   ![タグを結合ダイアログ](assets/merge-tag.png)

1. 「**送信**」を選択します。

コンソールで選択したタグが、ダイアログで指定したタグに結合されます。 参照されたタグを移動または結合すると、そのタグは物理的に削除されず、参照を維持できます。 詳しくは、 [AEM Tagging Framework](/help/implementing/developing/introduction/tagging-framework.md#moving-and-merging-tags) を参照してください。

### タグの削除 {#deleting-tags}

タグ分類が変更され、タグや名前空間を不要にした場合は、タグや名前空間を削除できます。

1. タグを削除するには、 [タグ付けコンソール。](#tagging-console)

1. 削除するタグを選択し、「 」を選択します。 **削除** 」と入力します。

1. The **タグを削除** 選択したタグを削除するかどうかを確認するダイアログが表示されます。 「**削除**」を選択します。

   ![タグの削除の確認モーダル](assets/delete-tag.png)

1. AEMは、タグが参照されていないことを確認します。

   1. 参照が見つからない場合、AEMは削除に関する最終確認を求めます。 選択 **削除**

      ![参照が見つかりません](assets/no-references-found.png)

   1. 参照が見つかった場合、AEMはそれらを提示し、削除の最終確認を求めます。

      ![参照が見つかりました](assets/references-found.png)

選択したタグは、オーサー環境から削除され、永久に削除されます。 タグが公開されていた場合は、パブリッシュ環境からも削除されます。選択したタグがコンテナタグの場合、その子タグもすべて削除されます。

<!--

## Setting Tag Permissions {#setting-tag-permissions}

Tag permissions are ['secure (by default)'](/help/sites-administering/production-ready.md); a best practice for the publish environment that requires read permission to be explicitly allowed for tags. Bascially, this is done by creating a package of the Tag Namespace after permissions have been set on author, and installing the package on all publish instances.

* on author instance

    * sign in with administrative privileges
    * access the [Security Console](/help/sites-administering/security.md#accessing-user-administration-with-the-security-console),

        * for example, browse to http://localhost:4502/useradmin

    * in the left pane, select the group (or user) for which [read permission](/help/sites-administering/security.md#permissions) is to be granted
    * in the right pane, locate the **Path **to the Tag Namespace

        * for example, `/content/cq:tags/mycommunity`

    * select the `checkbox`in the **Read** column
    * select **Save**

![chlimage_1-204](assets/chlimage_1-204.png)

* ensure all publish instances have same permissions

    * one approach is to [create a package](/help/sites-administering/package-manager.md#package-manager) of the namespace on author

        * on `Advanced` tab, for `AC Handling` select `Overwrite`

    * replicate the package

        * choose `Replicate` from package manager

-->

## 他の言語でのタグの管理 {#managing-tags-in-different-languages}

タグの `title` プロパティは複数の言語に翻訳できます。翻訳が完了すると、ユーザーまたはコンテンツの言語に応じて適切なタグタイトルを表示できます。

例えば、というタグがあるとします。 `Animals` ドイツ語とフランス語に翻訳したいと

1. を開きます。 [タグ付けコンソール。](#tagging-console)

1. 翻訳するタグを選択し、「 」を選択します。 **編集** 」と入力します。

1. Adobe Analytics の **タグを編集** ダイアログ、 **ローカリゼーション** 列で、ターゲット言語（例：ドイツ語）を選択します。

1. Adobe Analytics の **ドイツ語** 表示されるフィールドに、翻訳されたタイトルを入力します。

1. フランス語に対して、前の 2 つの手順を繰り返します。

   ![タグタイトルの翻訳](assets/translate-tag.png)

1. 「**送信**」を選択します。

コンテンツページの場合、タグに対して選択された言語は、使用可能な場合はページ言語から取得されます。

ただし、オーサリング環境では、AEMはユーザー言語設定を使用します。 タグ付けコンソールで、 `Animals` タグ、 `Animaux` ユーザープロパティで言語をフランス語に設定しているユーザーに対して表示されます。

ダイアログに新しい言語を追加するには、ドキュメントを参照してください [AEM Applications へのタグ付けの構築](/help/implementing/developing/introduction/tagging-applications.md#adding-a-new-language-to-the-edit-tag-dialog)

>[!TIP]
>
>AEMのローカライゼーション機能について詳しくは、 [多言語サイトのコンテンツの翻訳](/help/sites-cloud/administering/translation/overview.md).
