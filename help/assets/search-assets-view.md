---
title: ' [!DNL Assets view] でのアセットの検索と検出の方法を学ぶ'
description: 詳しくは、AEM Assets ビューでアセットを検索および検出する方法を参照してください。この強力な検索機能を使用すると、適切なアセットをすばやく発見できるので、コンテンツベロシティ（コンテンツ創出の速度）の向上に役立ちます。
role: User
exl-id: abfe6a91-1699-436f-8bf4-0d0bf2369f46
feature: Asset Management, Publishing, Collaboration, Asset Processing
source-git-commit: f83324be68bdab65e5c76ef336eb7e4a2e318dd1
workflow-type: tm+mt
source-wordcount: '1621'
ht-degree: 87%

---

# [!DNL Assets view] でアセットを検索 {#search-assets}

>[!CONTEXTUALHELP]
>id="assets_search"
>title="アセットの検索"
>abstract="検索バーでキーワードを指定するか、ステータス、ファイルタイプ、MIME タイプ、サイズ、作成日、変更日および有効期限に基づいてアセットをフィルタリングして、アセットを検索します。標準フィルターに加えて、カスタムフィルターを適用することもできます。フィルタリングした結果は、保存した検索条件またはスマートコレクションとして保存できます。"
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-assets-essentials/help/manage-collections.html?lang=ja#manage-smart-collection" text="スマートコレクションを作成"

[!DNL Assets view] では効果的な検索が可能です。この検索はデフォルトで機能します。フルテキスト検索なので、網羅的に検索できます。この強力な検索機能を使用すると、適切なアセットをすばやく発見できるので、コンテンツベロシティ（コンテンツ創出の速度）の向上に役立ちます。[!DNL Assets view] では、フルテキスト検索を行えるほか、スマートタグ、タイトル、作成日、著作権などのメタデータを検索することもできます。

アセットを検索するには：

* ページ上部の検索ボックスをクリックします。デフォルトでは、現在参照しているフォルダー内を検索します。次のいずれかの操作を行います。

  ![検索ボックス](assets/search-box.png)

   * キーワードを使用して検索します。オプションで、フォルダーを変更することもできます。Return キーを押します。

   * 最近表示されたアセットを直接検索して、操作を開始します。検索ボックス内をクリックし、最近表示されたアセットを候補から選択します。

## 検索結果のフィルタリング {#refine-search-results}

複数のフィルターを適用することで、検索結果を絞り込み、関連するアセットを見つけることができます。 管理者が設定するこれらのフィルターは、ファイル、フォルダー、コレクションに基づいています。 [&#x200B; 検索フィルターのカスタマイズ &#x200B;](custom-search-filters.md) を参照してください。

![検索フィルター](assets/filters-panel.gif)

以下のパラメーターに基づいて検索結果をフィルタリングできます。

* アセットステータス：`Approved`、`Rejected`、または `No Status` アセットステータスを使用した検索結果のフィルタリング。
* ファイルタイプ：サポートされているファイルタイプ（`Images`、`Documents`、`Videos`）で検索結果をフィルタリングします。
* MIME タイプ：サポートされている 1 つ以上のファイル形式でフィルタリングします。<!-- TBD:  [supported file formats](/help/using/supported-file-formats.md). -->
* 画像サイズ：画像をフィルタリングするための最小サイズと最大サイズのどちらか一方または両方を指定します。サイズはピクセル単位で指定され、画像のファイルサイズではありません。
* 作成日：アセットの作成日（メタデータで指定されたもの）。標準の日付形式は `yyyy-mm-dd` です。
* 変更日：アセットの最終変更日。標準の日付形式は `yyyy-mm-dd` です。
* 有効期限：アセットの `Expired` ステータスに基づいて検索結果をフィルタリングできます。また、アセットの有効期限の日付範囲を指定して、検索結果をさらにフィルタリングすることもできます。
* カスタムフィルター：アセットビューのユーザーインターフェイスに[カスタムフィルターを追加](#custom-filters)します。標準フィルターに加えて、カスタムフィルターを適用し、検索結果を絞り込むことができます。

検索したアセットを、`Name`、`Relevance`、`Size`、`Modified` および `Created` の昇順または降順に並べ替えることができます。デフォルトでは、検索したアセットは `Relevance` に基づいて並べ替えられます。

<!--
  
## Manage custom filters {#custom-filters}

**Permissions required:**  `Can Edit`, `Owner`, or Administrator.

Assets view also enable you to add custom filters to the user interface. You can then apply those custom filters in addition to the [standard filters](#refine-search-results) to refine your search results.

Assets view provides the following custom filters:

<table>
    <tbody>
     <tr>
      <th><strong>Custom filter name</strong></th>
      <th><strong>Description</strong></th>
     </tr>
     <tr>
      <td>Title</td>
      <td>Filter assets using the asset title. The title that you specify in the case-sensitive search criteria must match the exact title of the asset to display in the results.</td>
     </tr>
     <tr>
      <td>Name</td>
      <td>Filter assets using the asset file name. The name that you specify in the case-sensitive search criteria must match the exact file name of the asset to display in the results.</td>
     </tr>
     <tr>
      <td>Asset Size</td>
      <td>Filter assets by defining a size range, in bytes, in the search criteria for an asset to display in the results.</td>
     </tr>
     <tr>
      <td>Predicted Tags</td>
      <td>Filter assets using the asset smart tag. The smart tag name that you specify in the case-sensitive search criteria must match the exact smart tag name of the asset to display in the results. You cannot specify multiple smart tags in search criteria.</td>
     </tr>    
    </tbody>
   </table>

   <!--
   You can use a wildcard operator (*) to enable Assets view to display assets in the results that partially match the search criteria. For example, if you define <b>ma*</b> as the search criteria, Assets view displays assets with title, such as, market, marketing, man, manchester, and so on in the results.

   You can use a wildcard operator (*) to enable Assets view to display assets in the results that partially match the search criteria.

   You can use a wildcard operator (*) to enable Assets view to display assets in the results that partially match the search criteria. You can specify multiple smart tags separated by a comma in the search criteria.

   

### Add custom filters {#add-custom-filters}

To add custom filters:

1. Click **[!UICONTROL Filters]**. 

1. In the **[!UICONTROL Custom Filters]** section, click **[!UICONTROL Edit]** or **[!UICONTROL Add Filters]**.

   ![Add custom filters](assets/add-custom-filters.png)

1. On the **[!UICONTROL Custom filters management]** dialog box, select the filters that you need to add to the existing list of filters. Select **[!UICONTROL Custom Filters]** to select all filters.

1. Click **[!UICONTROL Confirm]** to add the filters to the user interface.

### Remove custom filters {#remove-custom-filters}

To remove custom filters:

1. Click **[!UICONTROL Filters]**. 

1. In the **[!UICONTROL Custom Filters]** section, click **[!UICONTROL Edit]**.

1. On the **[!UICONTROL Custom filters management]** dialog box, deselect the filters that you need to remove from the existing list of filters.

1. Click **[!UICONTROL Confirm]** to remove the filters from the user interface.

-->

## AI 検索 {#ai-search}

AI 検索は、キーワードの完全一致に依存するのではなく、ユーザーのクエリの意味と意図を理解する高度な検索機能です。 人工知能（AI）と機械学習を使用して、より正確でコンテキストに対応した結果を提供します。

正確な用語を検索する従来のキーワードベースの検索とは異なり、AI 検索は、単語、概念、ユーザー意図の関係を解釈します。 これにより、クエリの表現が異なる場合や、入力ミスが含まれる場合、別の言語である場合でも、ユーザーが探しているものを確実に見つけることができます。

主なメリットには、次のようなものがあります。

* **多言語サポート**：正確な翻訳を必要とせずに複数の言語をまたいで検索します。ユーザーは、クエリ言語に関係なく、関連するコンテンツを見つけることができます。

* **スペルミスに対応**：入力ミスやスペルミスを解釈し、不完全な入力でも正確な結果が得られるようにします。

* **同義語の理解**：関連する用語やフレーズの結果を提供するので、ユーザーは正しいキーワードを推測する必要がありません。

* **コンテキスト対応検索**：完全一致単語だけでなく、クエリの背後にある意図を認識します。

### AI 検索の例 {#examples-ai-search}

**プロンプトの例**：*コーヒーを飲む女性*

従来のキーワードベースの検索では、`Woman`、`drinking`、`Coffee` など、アセットメタデータの完全一致を検索し、メタデータにこれらの用語をすべて含むアセットを返します。

ただし、AI 検索では、`Girl`、`Lady` と `Woman` の場合は `Cappuccino`、`Latte` の場合は `Coffee` など、類似の単語に一致します。

同様に、このプロンプトをスペイン語で指定したり、`Woman` を `Wman` とスペルミスしたりしても、同じ結果が得られます。

![Assets ビューでのセマンティック検索](assets/semantic-search.png)

### Assets ビューでの AI 検索の有効化または無効化 {#enable-disable-ai-search}

AI 検索を有効または無効にするには、次の手順を実行します。

1. **[!UICONTROL 設定]**/**[!UICONTROL 一般設定]** に移動し、「**[!UICONTROL 検索]**」タブを選択します。

1. 「**[!UICONTROL 検索]**」セクションで、「**[!UICONTROL AI 検索]**」を選択して AI 検索を有効にするか、「**[!UICONTROL キーワード]**」を選択して無効にします。

   ![Assets ビューでのセマンティック検索](/help/assets/assets/enable-disable-ai-search.png)

1. 「**[!UICONTROL 保存]**」をクリックします。


## [!DNL Adobe Firefly] を使用したアセット検索 {#search-firefly}

[!DNL Experience Manager Assets] 内の [!DNL Adobe Firefly] アセット検索機能を利用して、どのアセットフォルダーにもないアセットを検索できます。これにより、アセットフォルダーに保存されていないアセットをリアルタイムで効率的に生成できます。

### 事前準備 {#search-assets-firefly-prereqs}

アクティブな [!DNL Adobe Express] サブスクリプションが必要です。

### アセットの生成 {#generate-assets-firefly}

[!DNL Adobe Firefly] を使用して新しいアセットを生成するには、次の手順に従います。

1. [!DNL AEM Assets] ワークスペースに移動します。

1. 検索バーにアセット名を入力します。例えば、キーワード `Bugatti Type 57` を使用してアセットを検索できます。アセットを検索する際に、どのアセットフォルダーにもアセットが存在しないので、結果は見つかりません。AI を使用してアセットを生成するには、「**[!UICONTROL Firefly を使用して生成]**」をクリックします。[!DNL Adobe Firefly] 画面が表示されます。

   ![Firefly の統合](assets/firefly-integration.png)

   新しいアセットが正常に生成されました。さらに、説明ボックスに新しいテキストプロンプトを入力して、画像の説明を変更できます。[優れた AI プロンプトを記述して、高品質で関連性の高いコンテンツを生成する方法を説明します](https://helpx.adobe.com/jp/firefly/using/tips-and-tricks.html)。または、[スタイルの変更や画像のサイズの変更など、他の様々な機能を使用して画像を編集](https://helpx.adobe.com/jp/firefly/using/text-to-image.html)できます。

   ![Firefly の統合](assets/bugatti-type-57.png)

1. 保存する画像を選択します。**[!UICONTROL 保存]**&#x200B;をクリックして、アクセスしやすいようにアセットを目的のフォルダーに保存します。

1. アセットを保存フォームが表示されます。次のフィールドを指定します。

   * 「**名前を付けて保存**」フィールドにファイルの名前を入力します。
   * 宛先フォルダーを選択します。
   * プロジェクトまたはキャンペーンの名前、キーワード、チャネル、時間枠、地域などの詳細を入力します。

   ![Firefly の統合](assets/save-generated-asset.png)

1. 「**新しいアセットとして保存**」をクリックして、アセットを保存します。

<!--

### Upload assets {#upload-assets-firefly}

To upload the generated asset to the assets repository:

1. Click **[!UICONTROL Upload]**.
1. Select the asset folder to which you need to upload the asset and click **[!UICONTROL Select Folder]**.
 ![Upload asset](assets/upload-asset-firefly.jpg)

 -->

## 保存済みの検索 {#saved-search}

[!DNL Assets view] の検索機能は非常に使いやすくなっています。検索ボックス内に、キーワードを入力し、Return キーを押して結果を表示できるだけでなく、最近検索したキーワードを 1 回クリックするだけですばやく再検索することもできます。

また、アセットのメタデータやタイプに関する特定の条件に基づいて検索結果をフィルタリングすることもできます。特定のフィルターを頻繁に使用する場合、[!DNL Assets view] では、検索性を向上させるために、検索パラメーターを保存できます。その場合、保存済みの検索を選択し、1 回クリックするだけで検索してフィルターを適用することができます。

保存した検索条件を作成するには、アセットを検索し、1 つ以上のフィルターを適用して、[!UICONTROL フィルター]パネルの&#x200B;**[!UICONTROL 別名で保存]**／**[!UICONTROL 保存した検索条件]**&#x200B;をクリックします。また、「**[!UICONTROL 別名で保存]**」をクリックし、「**[!UICONTROL スマートコレクション]**」を選択して、結果をスマートコレクションとして保存することもできます。詳しくは、[スマートコレクションの作成](manage-collections.md#create-a-smart-collection)を参照してください。

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

* **類似の画像を検索**：Assets UI で、メタデータとスマートタグに基づいて類似の画像アセットを検索します。

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

* **監視**：アセットに対して実行される[操作を監視](https://experienceleague.adobe.com/ja/docs/experience-manager-cloud-service/content/assets/manage/search-assets)します。

## 最初に検索するホームページの設定 {#configuring-search-first-homepage}

アセットビューを使用すると、組織のデフォルトのランディングページを選択できます。最初に検索をホームページとして使用する場合、ブランドに合わせて背景画像とロゴ画像を設定し、ページのブランディングを調整するオプションもあります。

最初に検索するホームページを設定するには、次の手順を実行します。

1. **[!UICONTROL 設定]**／**[!UICONTROL 一般設定]**&#x200B;に移動します。
1. 「**[!UICONTROL 最初に検索]**」を選択します。これにより、「最初に検索」に関連する設定が開きます。ホームページの[位置](#setting-alignment-search-bar)または[背景画像とロゴ画像の設定](#setting-background-image-and-logo)を設定できます。

### 検索バーの位置の設定 {#setting-alignment-search-bar}

[!DNL Assets view] を使用すると、検索バーの位置を変更できます。検索バーは中央または上部に表示できます。適切な位置を選択し、「**[!UICONTROL 保存]**」をクリックします。

![最初に検索するホームページの位置](assets/search-first-alignment.png)

### ホームページの背景画像とロゴ画像の設定 {#setting-background-image-and-logo}

最初に検索するホームページにブランドのロゴ画像と背景画像を追加できます。次の手順を実行します。

1. **[!UICONTROL ホームページ]**&#x200B;の「**[!UICONTROL 背景画像とロゴ画像]**」セクションに移動します。
1. 「**[!UICONTROL 置換]**」をクリックして、既存のアセットリポジトリから画像を参照します。
1. 「**[!UICONTROL 保存]**」をクリックします。変更を[プレビュー](#preview-configured-homepage)して、変更内容を確認します。

### 設定済みのホームページのプレビュー {#preview-configured-homepage}

最初に検索するホームページのレイアウトと書式設定をプレビューして確認できます。**[!UICONTROL プレビュー]**&#x200B;を使用すると、レイアウトを修正したり、要件に応じて変更を加えたりできます。設定済みのホームページをプレビューするには、次の手順を実行します。

1. 「**[!UICONTROL 一般設定]**」をクリックし、「**[!UICONTROL 最初に検索]**」を選択します。
1. **[!UICONTROL 最初に検索するホームページをカスタマイズ]**&#x200B;に移動し、「**[!UICONTROL プレビュー]**」をクリックします。「**[!UICONTROL ダークテーマ]**」ボタンを切り替えて、ダークテーマまたはライトテーマでホームページをプレビューします。
1. 「**[!UICONTROL 閉じる]**」をクリックし、プレビュー画面を閉じます。

   ![最初に検索するホームページのプレビュー](/help/assets/assets/search-first-preview.gif)


<!--

## Contextual Search {#contextual-search}

You can also search assets available in the repository by defining text prompts. Experience Manager Assets automatically transforms those text prompts to search filters and displays the search results. You can view and modify automatic filters using the Filters Pane to further narrow down the search results.

### Access Contextual Search {#access-contextual-search}

To access Contextual Search in Experience Manager Assets:

1. Click **[!UICONTROL Search]** in the left pane.

   ![Contextual Search](assets/access-contextual-search.png)

1. Define the text prompt in the Search text box and click **[!UICONTROL Contextual Search]**.

   ![Contextual Search text prompt](/help/assets/assets/wknd-contextual-search.png)

   [!DNL Experience Manager Assets] displays the search results.

### Supported filters {#supported-filters}

Contextual Search supports the following filters out-of-the-box. Base your text prompts on these filters to view appropriate search results.

* Image height

* Image width

* File type: image, document, video, or folder.

* MIME type: JPG, PNG, TIFF, GIF, MP4, PDF, PPTX, DOCX or XLSX

* Created date

* Modified date

* Expiration date

* Asset status: Approved, Rejected, or all

* Expired assets

### Examples for the text prompts {#text-prompts-examples}

**Example 1**

**Text Prompt**: Images created this month.

[!DNL Experience Manager Assets] applies the following filters automatically and displays the search results:

![Contextual Search Example 1](assets/contextual-search-example1.png)

**Example 2**

**Text prompt**: Images at least 200px tall and 100px wide with beach and clear sky.

[!DNL Experience Manager Assets] applies the following filters automatically and displays the search results:

![Contextual Search Example 2](assets/contextual-search-example2.png)

**Example 3**

**Text prompt**: I need images of blue sky that are 1500 and 2500 pixel height and created in the past month that is not expired and approved.

[!DNL Experience Manager Assets] applies the following filters automatically and displays the search results:

![Contextual Search Example 3](assets/contextual-search-example3.png)

The following video illustrates the end-to-end process from accessing the Contextual Search User Interface to defining text prompts, and viewing the search results.

>[!VIDEO](https://video.tv.adobe.com/v/3428407)

### Disable Contextual Search {#disable-contextual-search}

Administrators also have the option to disable Contextual Search for users in your organization. To do so, execute the following steps:

1. Navigate to **[!UICONTROL Settings]** > **[!UICONTROL General Settings]**.

1. In the [!UICONTROL Contextual Search] section, turn off the **[!UICONTROL Enable Contextual Search for your organization]** toggle to disable the Contextual Search feature for all users in your organization.  

### Contextual Search feedback {#contextual-search-feedback}

If you need to provide feedback on the Contextual Search feature, click ![Contextual Search icon](assets/do-not-localize/Smock_Help_18_N.svg)  and click the Feedback icon. Select the feedback type, specify the subject and description, and click **[!UICONTROL Submit]**.

![Contextual Search feedback](assets/contextual-search-feedback.png)

-->

## 次の手順 {#next-steps}

* [ビデオを試聴してアセットビューでのアセットの検索を学ぶ](https://experienceleague.adobe.com/docs/experience-manager-learn/assets-essentials/basics/using.html?lang=ja)

* アセットビューのユーザーインターフェイスの「[!UICONTROL フィードバック]」オプションを使用して製品に関するフィードバックを提供する

* 右側のサイドバーにある「[!UICONTROL このページを編集]」 ![ページを編集](assets/do-not-localize/edit-page.png) または「[!UICONTROL イシューを記録]」 ![GitHub イシューを作成](assets/do-not-localize/github-issue.png) を使用してドキュメントのフィードバックを提供する。

* [カスタマーケア](https://experienceleague.adobe.com/ja?support-solution=General&lang=ja#support)に問い合わせる



