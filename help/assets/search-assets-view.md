---
title: ' [!DNL Assets view] でのアセットの検索と検出の方法を学ぶ'
description: 詳しくは、AEM Assets ビューでアセットを検索および検出する方法を参照してください。この強力な検索機能を使用すると、適切なアセットをすばやく発見できるので、コンテンツベロシティ（コンテンツ創出の速度）の向上に役立ちます。
role: User
exl-id: abfe6a91-1699-436f-8bf4-0d0bf2369f46
source-git-commit: 62be3c6e98df9002cdfbeef50dd5475c4daa1576
workflow-type: tm+mt
source-wordcount: '1543'
ht-degree: 100%

---

# [!DNL Assets view] でアセットを検索 {#search-assets}

>[!CONTEXTUALHELP]
>id="assets_search"
>title="アセットの検索"
>abstract="検索バーでキーワードを指定するか、ステータス、ファイルタイプ、MIME タイプ、サイズ、作成日、変更日および有効期限に基づいてアセットをフィルタリングして、アセットを検索します。標準フィルターに加えて、カスタムフィルターを適用することもできます。フィルタリングした結果は、保存した検索条件またはスマートコレクションとして保存できます。"
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-assets-essentials/help/manage-collections.html?lang=ja#manage-smart-collection" text="スマートコレクションを作成"

[!DNL Assets view] では効果的な検索が可能です。この検索はデフォルトで機能します。フルテキスト検索なので、網羅的に検索できます。この強力な検索機能を使用すると、適切なアセットをすばやく発見できるので、コンテンツベロシティ（コンテンツ創出の速度）の向上に役立ちます。[!DNL Assets view] では、フルテキスト検索を行えるほか、スマートタグ、タイトル、作成日、著作権などのメタデータを検索することもできます。

アセットを検索するには、

* ページ上部の検索ボックスをクリックします。デフォルトでは、現在参照しているフォルダー内を検索します。次のいずれかの操作を行います。

  ![検索ボックス](assets/search-box.png)

   * キーワードを使用して検索します。オプションで、フォルダーを変更することもできます。Return キーを押します。

   * 最近表示されたアセットを直接検索して、操作を開始します。検索ボックス内をクリックし、最近表示されたアセットを候補から選択します。

## 検索結果のフィルタリング {#refine-search-results}

以下のパラメーターに基づいて検索結果をフィルタリングできます。

![検索フィルター](assets/filters1.png)

*図：検索したアセットを様々なパラメーターに基づいてフィルタリング*

* アセットステータス：`Approved`、`Rejected`、または `No Status` アセットステータスを使用した検索結果のフィルタリング。

* ファイルタイプ：サポートされているファイルタイプ（`Images`、`Documents`、`Videos`）で検索結果をフィルタリングします。
* MIME タイプ：サポートされている 1 つ以上のファイル形式でフィルタリングします。<!-- TBD:  [supported file formats](/help/assets/supported-file-formats-assets-view.md). -->
* 画像サイズ：画像をフィルタリングするための最小サイズと最大サイズのどちらか一方または両方を指定します。サイズはピクセル単位で指定され、画像のファイルサイズではありません。
* 作成日：アセットの作成日（メタデータで指定されたもの）。標準の日付形式は `yyyy-mm-dd` です。
* 変更日：アセットの最終変更日。標準の日付形式は `yyyy-mm-dd` です。

* 有効期限：アセットの `Expired` ステータスに基づいて検索結果をフィルタリングできます。また、アセットの有効期限の日付範囲を指定して、検索結果をさらにフィルタリングすることもできます。

* カスタムフィルター：アセットビューのユーザーインターフェイスに[カスタムフィルターを追加](#custom-filters)できます。標準フィルターに加えて、カスタムフィルターを適用し、検索結果を絞り込むことができます。

検索したアセットを、`Name`、`Relevancy`、`Size`、`Modified` および `Created` の昇順または降順に並べ替えることができます。

## カスタムフィルターの管理 {#custom-filters}

**必要な権限：** `Can Edit`、`Owner` または管理者。

また、アセットビューで、ユーザーインターフェイスにカスタムフィルターを追加できます。[標準フィルター](#refine-search-results)に加えて、カスタムフィルターを適用し、検索結果を絞り込むことができます。

アセットビューが提供するカスタムフィルターは次のとおりです。

<table>
    <tbody>
     <tr>
      <th><strong>カスタムフィルター名</strong></th>
      <th><strong>説明</strong></th>
     </tr>
     <tr>
      <td>タイトル</td>
      <td>アセットタイトルを使用してアセットをフィルタリングします。大文字と小文字を区別する検索条件で指定するタイトルは、結果に表示されるアセットの正確なタイトルと一致する必要があります。</td>
     </tr>
     <tr>
      <td>名前</td>
      <td>アセットファイル名を使用してアセットをフィルタリングします。大文字と小文字を区別する検索条件で指定する名前は、結果に表示されるアセットの正確なファイル名と一致する必要があります。</td>
     </tr>
     <tr>
      <td>アセットサイズ</td>
      <td>アセットをフィルタリングするには、検索条件でアセットに表示するサイズ範囲をバイト単位で指定します。</td>
     </tr>
     <tr>
      <td>予測されるタグ</td>
      <td>アセットスマートタグを使用してアセットをフィルタリングします。大文字と小文字を区別する検索条件で指定するスマートタグ名は、結果に表示されるアセットの正確なスマートタグ名と一致する必要があります。検索条件に複数のスマートタグを指定することはできません。</td>
     </tr>    
    </tbody>
   </table>

<!--
   You can use a wildcard operator (*) to enable Assets view to display assets in the results that partially match the search criteria. For example, if you define <b>ma*</b> as the search criteria, Assets view displays assets with title, such as, market, marketing, man, manchester, and so on in the results.

   You can use a wildcard operator (*) to enable Assets view to display assets in the results that partially match the search criteria.

   You can use a wildcard operator (*) to enable Assets view to display assets in the results that partially match the search criteria. You can specify multiple smart tags separated by a comma in the search criteria.

   -->

### カスタムフィルターの追加 {#add-custom-filters}

カスタムプロパティを追加する手順は次のとおりです。

1. 「**[!UICONTROL フィルター]**」をクリックします。

1. 「**[!UICONTROL カスタムフィルター]**」セクションで、「**[!UICONTROL 編集]**」または「**[!UICONTROL フィルターを追加]**」をクリックします。

   ![カスタムフィルターの追加](assets/add-custom-filters.png)

1. **[!UICONTROL カスタムフィルター管理]**&#x200B;ダイアログボックスで、既存のフィルターのリストに追加するフィルターを選択します。「**[!UICONTROL カスタムフィルター]**」を選択して、すべてのフィルターを選択します。

1. 「**[!UICONTROL 確認]**」をクリックして、ユーザーインターフェイスにフィルターを追加します。

### カスタムフィルターの削除 {#remove-custom-filters}

カスタムフィルターを削除する手順は次のとおりです。

1. 「**[!UICONTROL フィルター]**」をクリックします。

1. 「**[!UICONTROL カスタムフィルター]**」セクションで、「**[!UICONTROL 編集]**」をクリックします。

1. **[!UICONTROL カスタムフィルター管理]**&#x200B;ダイアログボックスで、既存のフィルターのリストから削除するフィルターを選択解除します。

1. 「**[!UICONTROL 確認]**」をクリックして、ユーザーインターフェイスからフィルターを削除します。

## [!DNL Adobe Firefly] を使用したアセット検索 {#search-firefly}

[!DNL Experience Manager Assets] 内の [!DNL Adobe Firefly] アセット検索機能を利用して、どのアセットフォルダーにもないアセットを検索できます。これにより、アセットフォルダーに保存されていないアセットをリアルタイムで効率的に生成できます。

### 事前準備

アクティブな [!DNL Adobe Express] サブスクリプションが必要です。

### アセットの生成

[!DNL Adobe Firefly] を使用して新しいアセットを生成するには、次の手順に従います。

1. [!DNL AEM Assets] ワークスペースに移動します。
1. ページ上部の検索バーにアセット名を入力します。<br>
例えば、キーワード `Bugatti Type 57` を使用してアセットを検索できます。アセットを検索する際に、どのアセットフォルダーにもアセットが存在しないので、結果は見つかりません。
1. ページ中央の検索バーにアセット名を入力し、「**[!UICONTROL 生成]**」をクリックします。
   ![Firefly の統合](assets/firefly-integration.jpg)
   *図：アセットフォルダー内に Bugatti Type 57 に関する結果が見つかりませんでした。* <br>
新しいアセットが正常に生成されました。
   ![Firefly の統合](assets/bugatti-type-57.jpg)
   *図：[!DNL Adobe Firefly] アセット検索機能を使用して、参照アセットが検索されました。* <br>
これらのアセットを適切なフォルダーにアップロードすると、簡単にアクセスできます。

### アセットのアップロード

生成したアセットをアセットリポジトリにアップロードするには、次の手順に従います。

1. 「**[!UICONTROL アップロード]**」をクリックします。
1. アセットをアップロードする必要があるアセットフォルダーを選択し、「**[!UICONTROL フォルダーを選択]**」をクリックします。
   ![アセットをアップロード](assets/upload-asset-firefly.jpg)
   *図：アセットのアップロード先となるフォルダーを選択します。*

## 保存済みの検索 {#saved-search}

[!DNL Assets view] の検索機能は非常に使いやすくなっています。検索ボックス内に、キーワードを入力し、Return キーを押せば結果を表示できるます。あるいは、最近検索したキーワードを 1 回クリックするだけですばやく再検索することができます。

また、アセットのメタデータやタイプに関する特定の条件に基づいて検索結果をフィルタリングすることもできます。特定のフィルターを頻繁に使用する場合、[!DNL Assets view] では、検索性を向上させるために、検索パラメーターを保存できます。その場合、保存済みの検索を選択し、1 回クリックするだけで検索してフィルターを適用することができます。

保存した検索条件を作成するには、アセットを検索し、1 つ以上のフィルターを適用して、[!UICONTROL フィルター]パネルの&#x200B;**[!UICONTROL 別名で保存]**／**[!UICONTROL 保存した検索条件]**&#x200B;をクリックします。また、「**[!UICONTROL 別名で保存]**」をクリックし、「**[!UICONTROL スマートコレクション]**」を選択して、結果をスマートコレクションとして保存することもできます。詳しくは、[スマートコレクションの作成](manage-collections-assets-view.md#create-a-smart-collection)を参照してください。

![スマートコレクションの作成](assets/create-smart-collection.png)

<!-- TBD: Search behavior. Full-text search. Ranking and rank boosts. Hidden assets.
Report poor UX that users can only save a filtered search and not a simple search.
.
Are other supported files fully indexed and support full-text search? Eg. audio/videos files can at best have metadata indexed.
Anything about ranking of assets displayed in search results?

What about temporarily hiding an asset (suspending search on it) from the search results? If an asset is undergoing review collaboration, should it be used by others? Should it be hidden in search?

When userA is searching and userB add an asset that matches search results, will the asset display in search as soon as userA refreshes the page? Assuming indexing is near real-time. May not be so for bulk uploads.
-->

## 検索結果の操作 {#work-with-search-results}

検索結果に表示するアセットを選択し、次の操作を実行できます。

* **類似検索画像**：Assets UI で、メタデータとスマートタグに基づいて類似の画像アセットを検索します。

* **詳細**：アセットのプロパティを表示および編集します。

* **ダウンロード**：アセットをダウンロードします。

* **コレクションに追加**：選択したアセットをコレクションに追加します。

* **クイックアクセスにピン留め**：[アセットをピン留め](my-workspace-assets-view.md)すると、後で必要になった際に、すばやくアクセスできるようになります。ピン留めしたすべての項目は、マイワークスペースの「**クイックアクセス**」セクションに表示されます。

* **Adobe Express で開く**：Experience Manager Assets 画面から統合された Adobe Express で画像を編集します。

* **編集**：Adobe Express を使用して画像を編集します。

* **リンクを共有**：他のユーザーとアセットの[リンクを共有](share-links-for-assets-view.md)して、アセットにアクセスしてダウンロードできるようにします。

* **削除**：アセットを削除します。

* **コピー**：別のフォルダーの場所にアセットをコピーします。

* **移動**：アセットを別のフォルダーの場所に移動します。

* **名前を変更**：アセットの名前を変更します。

* **ライブラリにコピー**：アセットをライブラリに追加します。

* **タスクを割り当て**：アセットのユーザーにタスクを割り当てます。

* **監視**：アセットに対して実行される[操作を監視](manage-notifications-assets-view.md)します。

## 最初に検索するホームページの設定 {#configuring-search-first-homepage}

Experience Manager Assets を使用すると、組織のデフォルトのランディングページを選択できます。最初に検索をホームページとして使用する場合、ブランドに合わせて背景画像とロゴ画像を設定し、ページのブランディングを調整するオプションもあります。

最初に検索するホームページを設定するには、次の手順を実行します。

1. **[!UICONTROL 設定]**／**[!UICONTROL 一般設定]**&#x200B;に移動します。
1. 「**[!UICONTROL 最初に検索]**」を選択します。これにより、最初の検索に関連する設定が開きます。ホームページの[位置](#setting-alignment-search-bar)または[背景画像とロゴ画像の設定](#setting-background-image-and-logo)を設定できます。

### 検索バーの位置の設定 {#setting-alignment-search-bar}

[!DNL Assets view] を使用すると、検索バーの位置を変更できます。検索バーは中央または上部に表示できます。適切な位置を選択し、「**[!UICONTROL 保存]**」をクリックします。

![最初に検索するホームページの位置](assets/search-first-alignment.png)

### ホームページの背景画像とロゴ画像の設定 {#setting-background-image-and-logo}

最初に検索するホームページにブランドのロゴ画像と背景画像を追加できます。以下の手順を実行します。

1. **[!UICONTROL ホームページ]**&#x200B;の「**[!UICONTROL 背景画像とロゴ画像]**」セクションに移動します。
1. 「**[!UICONTROL 置換]**」をクリックして、既存のアセットリポジトリから画像を参照します。
1. 「**[!UICONTROL 保存]**」をクリックします。変更を[プレビュー](#preview-configured-homepage)して、変更内容を確認します。

### 設定済みのホームページのプレビュー {#preview-configured-homepage}

最初に検索するホームページのレイアウトと書式設定をプレビューして確認できます。**[!UICONTROL プレビュー]**&#x200B;を使用すると、レイアウトを修正したり、要件に応じて変更を加えたりできます。設定済みのホームページをプレビューするには、次の手順を実行します。

1. 「**[!UICONTROL 一般設定]**」をクリックし、「**[!UICONTROL 最初に検索]**」を選択します。
1. **[!UICONTROL 最初に検索するホームページをカスタマイズ]**&#x200B;に移動し、「**[!UICONTROL プレビュー]**」をクリックします。「**[!UICONTROL ダークテーマ]**」ボタンを切り替えて、ダークテーマまたはライトテーマでホームページをプレビューします。
1. 「**[!UICONTROL 閉じる]**」をクリックし、プレビュー画面を閉じます。

   ![最初に検索するホームページのプレビュー](assets/search-first-preview.gif)

## 次の手順 {#next-steps}

* [ビデオを試聴してアセットビューでのアセットの検索を学ぶ](https://experienceleague.adobe.com/docs/experience-manager-learn/assets-essentials/basics/using.html?lang=ja)

* アセットビューのユーザーインターフェイスの「[!UICONTROL フィードバック]」オプションを使用して製品に関するフィードバックを提供する

* 右側のサイドバーにある「[!UICONTROL このページを編集]」（![ページを編集](assets/do-not-localize/edit-page.png)）または「[!UICONTROL 問題を記録] 」（![GitHub イシューを作成](assets/do-not-localize/github-issue.png)）を使用してドキュメントに関するフィードバックを提供する

* [カスタマーケア](https://experienceleague.adobe.com/?support-solution=General&amp;lang=ja#support)に問い合わせる
