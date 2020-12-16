---
title: バリエーション - フラグメントコンテンツのオーサリング
description: バリエーションでは、フラグメントのコンテンツをオーサリングし、目的に応じてそのコンテンツのバリエーションを作成できます（必要な場合）。
translation-type: tm+mt
source-git-commit: 0a60687eacf054675205d9a9466473e1f4996db1
workflow-type: tm+mt
source-wordcount: '1742'
ht-degree: 91%

---


# バリエーション - フラグメントコンテンツのオーサリング{#variations-authoring-fragment-content}

<!--
>[!CAUTION]
>
>Certain features for Content Fragments will be released in early 2021.
>
>The related documentation is already available for preview purposes.
>
>Please see the [Release Notes](/help/release-notes/release-notes-cloud/release-notes-current.md) for further details.
-->

[バリエーション](/help/assets/content-fragments/content-fragments.md#constituent-parts-of-a-content-fragment)は、特定のチャネルやシナリオで使用するためにマスターコンテンツのコピーを作成して編集できる、コンテンツフラグメントの重要な機能です。

「**バリエーション**」タブから、次の操作を実行できます。

* フラグメントの[コンテンツの入力](#authoring-your-content)、
* [マスター](#managing-variations)コンテンツの&#x200B;**バリエーションの作成および管理,**
* フラグメントの作成に使用された[コンテンツフラグメントモデル](/help/assets/content-fragments/content-fragments-models.md)の名前を参照してください。上部のツールバーのフラグメント名の下に表示されます。

編集中のデータタイプに応じて他の様々なアクションを実行します。次に例を示します。

* [フラグメントへのビジュアルアセットの挿入](#inserting-assets-into-your-fragment)（画像）

* 編集する[リッチテキスト](#rich-text)、[プレーンテキスト](#plain-text)および [Markdown](#markdown) の選択

* [コンテンツのアップロード](#uploading-content)

* [重要な統計の表示](#viewing-key-statistics)（複数行テキストについて）

* [テキストの要約](#summarizing-text)

* [バリエーションとマスターコンテンツの同期](#synchronizing-with-master)

>[!CAUTION]
>
>フラグメントが公開または参照（あるいは両方）された後に、作成者がフラグメントを開いて編集しようとすると警告が表示され、フラグメントを変更すると、参照されているページにも影響が及ぶことが警告されます。

## コンテンツのオーサリング {#authoring-your-content}

コンテンツフラグメントを編集用に開くと、デフォルトで「**バリエーション**」タブが開きます。このタブで、マスターまたはバリエーション（ある場合）のコンテンツをオーサリングできます。構造化フラグメントには、コンテンツモデルで定義された様々なデータ型の様々なフィールドが含まれています。

以下の操作を実行できます。

* 「**バリエーション**」タブで直接編集します。

   * 各データタイプには、異なる編集オプションがあります

* **複数行のテキスト**&#x200B;フィールドに対しては、[フルスクリーンエディター](#full-screen-editor)を開いて次の操作を行うこともできます。

   * [形式](#formats)の選択
   * その他の編集オプションの表示（[リッチテキスト](#rich-text)形式の場合）
   * 様々な[アクション](#actions)へのアクセス

<!--
For example:

![full screen editor](assets/cfm-variations-02.png)
-->

### フルスクリーンエディタ{#full-screen-editor}

複数行のテキストフィールドを編集する場合は、フルスクリーンエディターを開くことができます。実際のテキスト内でをタップまたはクリックし、次のアクションアイコンを選択します。

![全画面表示エディターアイコン](assets/cfm-variations-03.png)

<!--
This will open the full screen text editor:

![full screen editor icon](assets/cfm-variations-fullscreentexteditor.png)
-->

フルスクリーンテキストエディターには、次の機能があります。

* 様々な[アクション](#actions)へのアクセス
* [形式](#formats)に応じた、その他の書式設定オプション（[リッチテキスト](#rich-text)）

### アクション  {#actions}

全画面表示エディター（複数行テキスト）を開いている場合は、次のアクションも（すべての[形式](#formats)で）使用できます。

* [形式](#formats)（[リッチテキスト](#rich-text)、[プレーンテキスト](#plain-text)、[Markdown](#markdown)）の選択

* [コンテンツのアップロード](#uploading-content)

* [テキスト統計の表示](#viewing-key-statistics)

* [マスターとの同期](#synchronizing-with-master)（バリエーションの編集時）

* [テキストの要約](#summarizing-text)

### 形式 {#formats}

複数行テキストを編集するためのオプションは、選択した形式によって異なります。

* [リッチテキスト](#rich-text)
* [プレーンテキスト](#plain-text)
* [Markdown](#markdown)

全画面表示エディターでの作業時に形式を選択できます。

### リッチテキスト {#rich-text}

リッチテキストの編集では次の形式を設定できます。

* 太字
* 斜体
* 下線
* 整列：左、中央、右
* 箇条書きリスト
* 番号付きリスト
* インデント：増、減
* ハイパーリンクの作成および解除
* テキストを貼り付け／Word から貼り付け
* 表を挿入
* 段落スタイル：段落、見出し 1/2/3
* [アセットを挿入](#inserting-assets-into-your-fragment)
* 全画面表示エディターを開く。次の書式設定オプションを使用できます。
   * 検索
   * 検索と置換
   * スペルチェッカー
   * [注釈](/help/assets/content-fragments/content-fragments-variations.md#annotating-a-content-fragment)

<!--
* [Insert Content Fragment](#inserting-content-fragment-into-your-fragment)
-->

[アクション](#actions)は、全画面表示エディターからアクセスすることもできます。

### プレーンテキスト {#plain-text}

プレーンテキストを使用すると、書式設定または Markdown 情報なしでコンテンツをすばやく入力できます。全画面表示エディターを開いて追加の[アクション](#actions)を使用することもできます。

>[!CAUTION]
>
>「**プレーンテキスト**」を選択すると、**リッチテキスト**&#x200B;または **Markdown** に追加した書式、Markdown やアセットは失われます。

### Markdown {#markdown}

>[!NOTE]
>
>詳しくは、[Markdown](/help/assets/content-fragments/content-fragments-markdown.md) の説明を参照してください。

Markdown を使用してテキストの形式を設定できます。次を定義できます。

* 見出し
* 段落と改行
* リンク
* 画像
* ブロック引用
* リスト
* 強調
* コードブロック
* バックスラッシュエスケープ

全画面表示エディターを開いて追加の[アクション](#actions)を使用することもできます。

>[!CAUTION]
>
>**リッチテキスト**&#x200B;と **Markdown** を切り替えると、ブロック引用やコードブロックに予期しない影響が出ることがあります。ブロック引用とコードブロックの 2 つの形式は処理方法が異なる場合があるからです。

<!--
### Fragment References {#fragment-references}

If the Content Fragment Model contains Fragment References, your fragment authors may have additional options:

* [Edit Content Fragment](#fragment-references-edit-content-fragment)
* [New Content Fragment](#fragment-references-new-content-fragment)

![Fragment References](assets/cfm-variations-12.png)

#### Edit Content Fragment {#fragment-references-edit-content-fragment}

The option **Edit Content Fragment** will open
a new browser tab, with the content fragment open in the content fragment editor.

#### New Content Fragment {#fragment-references-new-content-fragment}

The option **New Content Fragment** will allow you to create a completely new fragment. To achieve this a variation of the create content fragment wizard will open in the editor. 

You will then be able to create a new fragment by:

1. Navigating to, and selecting the required folder.
1. Selecting **Next**.
1. Specifying properties; for example **Title**.
1. Selecting **Create**.
1. Finally:
   1. **Done** will return (to the original fragment) and reference the new fragment.
   1. **Open** will reference the new fragment as well as opening the new fragment, for editing, in a new browser tab.
-->

### 重要な統計の表示 {#viewing-key-statistics}

全画面表示エディターを開くと、「**テキスト統計**」アクションには、テキストに関する様々な情報が表示されます。

次に例を示します。

![統計](assets/cfm-variations-04.png)

### コンテンツのアップロード {#uploading-content}

コンテンツフラグメントのオーサリングのプロセスを簡易化するため、外部エディターで用意したテキストをアップロードしてフラグメントに直接追加できます。

### テキストの要約 {#summarizing-text}

テキストの要約を使用すると、重要ポイントと全体の意味を保ちながら、テキストの長さを規定の単語数に短縮できます。

>[!NOTE]
>
>より技術的に説明すると、特定のアルゴリズムに従って&#x200B;*情報の密度と独自性が最適な比率*&#x200B;であると評価した文章をシステムが保持します。

>[!CAUTION]
>
>コンテンツフラグメントには、親フォルダー（ISO コード）として有効な言語フォルダーが必要です。使用する言語モデルを決定するためにこれが使用されます。
>
>例えば、次のパスの `en/` です。
>
>  `/content/dam/my-brand/en/path-down/my-content-fragment`

>[!CAUTION]
英語版は標準で提供されています。
他の言語版は、パッケージ共有から言語モデルパッケージとして使用できます。
* [フランス語（fr）](https://www.adobeaemcloud.com/content/marketplace/marketplaceProxy.html?packagePath=/content/companies/public/adobe/packages/cq630/product/smartcontent-model-fr)
* [ドイツ語（de）](https://www.adobeaemcloud.com/content/marketplace/marketplaceProxy.html?packagePath=/content/companies/public/adobe/packages/cq630/product/smartcontent-model-de)
* [イタリア語（it）](https://www.adobeaemcloud.com/content/marketplace/marketplaceProxy.html?packagePath=/content/companies/public/adobe/packages/cq630/product/smartcontent-model-it)
* [スペイン語（es）](https://www.adobeaemcloud.com/content/marketplace/marketplaceProxy.html?packagePath=/content/companies/public/adobe/packages/cq630/product/smartcontent-model-es)



1. 「**マスター**」または必要なバリエーションを選択します。
1. 全画面表示エディターを開きます。

1. ツールバーの「**テキストを要約**」を選択します。

   ![要約](assets/cfm-variations-05.png)

1. ターゲットの単語数を指定し、「**開始**」を選択します。
1. 元のテキストが、提案された要約の横に並んで表示されます。

   * 削除される文には取り消し線が付けられ、赤く表示されます。
   * 強調表示された文をクリックすると、その文書はコンテンツの要約に保持されます。
   * 強調表示されていない文をクリックすると、削除されます。

1. 変更を確定するには、「**要約**」を選択します。

<!--
1. The original text is displayed side-by-side with the proposed summarization:

    * Any sentences to be eliminated are highlighted in red, with strike-through.
    * Click on any highlighted sentence to keep it in the summarized content.
    * Click on any non-highlighted sentence to have it eliminated.

   ![summarization comparison](assets/cfm-variations-06.png)
-->

### コンテンツフラグメントへの注釈の追加 {#annotating-a-content-fragment}

フラグメントに注釈を追加するには：

1. 「**マスター**」または必要なバリエーションを選択します。
1. 全画面表示エディターを開きます。
1. 上部のツールバーに、**注釈**&#x200B;アイコンが表示されます。 必要に応じて、一部のテキストを選択できます。

1. ダイアログが開きます。ここで注釈を入力できます。

   ![注釈](assets/cfm-variations-07a.png)

1. ダイアログで「**適用**」を選択します。

   ![注釈](assets/cfm-variations-annotations-apply-icon.png)

   注釈が選択したテキストに適用された場合、そのテキストはハイライトされたままになります。

   ![注釈](assets/cfm-variations-07b.png)

1. フルスクリーンエディターを閉じても、注釈はハイライトされたままになります。 選択すると、ダイアログが開き、注釈をさらに編集できます。

1. 「**保存**」を選択します。

<!--
1. The **Annotate** icon is available in the top toolbar. You can seelect some text if required.

   ![annotate](assets/cfm-variations-07.png)
-->

<!--
1. Close the full-screen editor, annotations are still highlighted. If selected, a dialog will open so that you can edit the annotation further.

   ![annotate](assets/cfm-variations-07c.png)

-->

### 注釈の表示、編集、削除 {#viewing-editing-deleting-annotations}

注釈：

* エディターの全画面表示モードと通常モードのどちらの場合も、注釈はテキストのハイライトとして示されます。注釈の完全な詳細を表示、編集および削除するには、ハイライト表示されたテキストをクリックします。するとダイアログが再度開きます。

   >[!NOTE]
   1 つのテキストに複数の注釈が適用されている場合は、ドロップダウンセレクターが表示されます。

* 注釈が適用されたテキスト全体を削除すると、注釈も削除されます。

* 注釈の一覧表示や削除をおこなうには、フラグメントエディターで「**注釈**」タブを選択します。

* 選択されたフラグメントの[タイムライン](/help/assets/content-fragments/content-fragments-managing.md#timeline-for-content-fragments)で、注釈の表示や削除をおこなえます。

<!--
* Can be listed, and deleted, by selecting the **Annotations** tab in the fragment editor.

  ![annotations](assets/cfm-variations-08.png)
-->

### フラグメントへのアセットの挿入 {#inserting-assets-into-your-fragment}

コンテンツフラグメントのオーサリングプロセスを容易にするには、[アセット](/help/assets/manage-digital-assets.md)（画像）をフラグメントに直接追加します。

アセットは書式設定なしでフラグメントの段落シーケンスに追加されます。[ページでフラグメントを利用、参照](/help/sites-cloud/authoring/fundamentals/content-fragments.md)する際に書式を設定できます。

>[!CAUTION]
参照ページではこれらのアセットの移動や削除はできません。移動や削除にはフラグメントエディターを使用する必要があります。
ただし、アセットの書式設定（サイズなど）は、[ページエディター](/help/sites-cloud/authoring/fundamentals/content-fragments.md)でおこなう必要があります。フラグメントエディターでのアセットの表示は、純粋にコンテンツフローのオーサリング用です。

>[!NOTE]
[画像](/help/assets/content-fragments/content-fragments.md#fragments-with-visual-assets)は様々な方法でフラグメントやページに追加できます。

1. 画像を追加したい位置にカーソルを置きます。
1. **アセットを挿入**&#x200B;アイコンを使用して、検索ダイアログを開きます。

   ![アセット挿入アイコン](assets/cfm-variations-09.png)

1. ダイアログでは以下が可能です。

   * DAM で必要なアセットへの移動
   * DAM でアセットの検索

   必要なアセットが見つかったら、サムネールをクリックしてアセットを選択します。

1. 「**選択**」を使用して、コンテンツフラグメント段落システムの現在の位置にアセットを追加します。

   >[!CAUTION]
   アセットを追加後に形式を変更すると次のようになります。
   * **プレーンテキスト**：アセットはフラグメントから完全に失われます。
   * **Markdown**：アセットは表示されなくなりますが、**リッチテキスト**&#x200B;に戻すとアセットがまた表示されます。


<!--
### Inserting a Content Fragment into your Fragment {#inserting-content-fragment-into-your-fragment}

To ease the process of authoring content fragments you can also add another Content Fragment to your fragment.

They will be added as a reference, in your current location in your fragment.
-->

<!--
>[!CAUTION]
>
>These assets cannot be moved or deleted on a referencing page, this must be done in the fragment editor.
>
>However, formatting of the asset (e.g. size) must be done in the [page editor](/help/sites-cloud/authoring/fundamentals/content-fragments.md). The representation of the asset in the fragment editor is purely for authoring the content flow.

>[!NOTE]
>
>There are various methods of adding [images](/help/assets/content-fragments/content-fragments.md#fragments-with-visual-assets) to the fragment and/or page.
-->

<!--
1. Position the cursor at the position you want to add the fragment.
1. Use the **Insert Content Fragment** icon to open the search dialog.

   ![insert Content Fragment icon](assets/cfm-variations-13.png)

1. In the dialog you can either:

    * navigate to the required fragment in the Assets folder
    * search for the fragment

   Once located, select the required fragment by clicking on the thumbnail.

1. Use **Select** to add a reference to the selected Content Fragment to your current content fragment (at the current location).

   >[!CAUTION]
   >
   >If, after adding an reference to another fragment, you change format to:
   >* **Plain Text**: the reference will be completely lost from the fragment.
   >* **Markdown**: the reference will remain.
-->

## バリエーションの管理  {#managing-variations}

### バリエーションの作成 {#creating-a-variation}

バリエーションでは、**マスター**&#x200B;コンテンツをコピーし、目的に応じて変更を加えることができます（必要な場合）。

新しいバリエーションを作成するには：

1. フラグメントを開き、サイドパネルが表示されていることを確認します。
1. サイドパネルのアイコンバーから「**バリエーション**」を選択します。
1. 「**バリエーションを作成**」を選択します。
1. ダイアログが開きます。新しいバリエーションの&#x200B;**タイトル**&#x200B;と&#x200B;**説明**&#x200B;を指定します。
1. 「**追加**」を選択します。フラグメントの&#x200B;**マスター**&#x200B;が新しいバリエーションにコピーされ、[編集](#editing-a-variation)用に開かれます。

   >[!NOTE]
   新しいバリエーションを作成すると、常に&#x200B;**マスター**&#x200B;がコピーされます（現在開いているバリエーションではありません）。

### バリエーションの編集  {#editing-a-variation}

以下のいずれかを実行した後に、バリエーションコンテンツを変更できます。

* [バリエーションを作成](#creating-a-variation)する。
* 既存のフラグメントを開いた後、サイドパネルから必要なバリエーションを選択する。

![バリエーションの編集](assets/cfm-variations-10.png)

### バリエーションの名前変更 {#renaming-a-variation}

既存のバリエーションの名前を変更するには：

1. フラグメントを開き、サイドパネルから「**バリエーション**」を選択します。
1. 必要なバリエーションを選択します。
1. 「**アクション**」ドロップダウンから「**名前を変更**」を選択します。

1. 表示されたダイアログボックスで新しい「**タイトル**」や「**説明**」を入力します。

1. 「**名前を変更**」アクションを確認します。

>[!NOTE]
この手順はバリエーションの&#x200B;**タイトル**&#x200B;にのみ影響を与えます。

### バリエーションの削除 {#deleting-a-variation}

既存のバリエーションを削除するには：

1. フラグメントを開き、サイドパネルから「**バリエーション**」を選択します。
1. 必要なバリエーションを選択します。
1. 「**アクション**」ドロップダウンから「**削除**」を選択します。

1. ダイアログで「**削除**」アクションを確認します。

>[!NOTE]
**マスター**&#x200B;は削除できません。

### マスターとの同期 {#synchronizing-with-master}

**マスター**&#x200B;はコンテンツフラグメントの必須の部分であり、定義に従ってコンテンツのマスターコピーを保持します。一方、バリエーションはそのコンテンツの更新および適合された個別のバージョンを保持します。マスターを更新した場合、これらの変更はバリエーションにも関連するので、バリエーションに送信する必要があります。

バリエーションの編集時には、バリエーションの現在の要素をマスターと同期させるアクションにアクセスできます。これにより、マスターにおこなわれた変更内容を必要なバリエーションに自動的にコピーできます。

>[!CAUTION]
同期を使用できるのは、変更内容を&#x200B;***マスター**からバリエーションに*&#x200B;コピーする場合のみです。
バリエーションの現在の要素のみが同期されます。
同期は、**複数行テキスト**&#x200B;データタイプに対してのみ機能します。
*バリエーションから&#x200B;**マスター***へ変更内容を転送することはできません。

1. フラグメントエディターでコンテンツフラグメントを開きます。**マスター**&#x200B;が編集されていることを確認します。
1. 特定のバリエーションを選択し、次のいずれかから適切な同期アクションを選択します。

   * 「**アクション**」ドロップダウンセレクター - **現在の要素をマスターと同期**

   * 全画面表示エディターのツールバー - **マスターと同期**

      ![マスターとの同期](assets/cfm-variations-11b.png)

1. マスターとバリエーションが横並びに表示されます。

   * 緑は追加されたコンテンツを示します（バリエーションへの追加）
   * 赤は削除されたコンテンツを示します（バリエーションからの削除）
   * 青は置換されたテキストを示します

   ![マスターとの同期](assets/cfm-variations-11c.png)

1. 「**同期**」を選択すると、バリエーションが更新され、表示されます。

<!--
1. Select a specific variation, then the appropriate synchronization action from either:

   * the **Actions** drop down selector - **Sync current element with master**

      ![synchronizing with master](assets/cfm-variations-11a.png)

   * the toolbar of the full-screen editor - **Sync with master**

      ![synchronizing with master](assets/cfm-variations-11b.png)

1. Master and the variation will be shown side-by-side:

   * green indicates content added (to the variation)
   * red indicates content removed (from the variation)
   * blue indicates replaced text

   ![synchronizing with master](assets/cfm-variations-11c.png)

1. Select **Synchronize**, the variation will updated and shown.

-->