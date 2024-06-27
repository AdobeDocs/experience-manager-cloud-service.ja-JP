---
title: Content Hubでのアセットの検索
description: でアセットを検索する方法を説明します [!DNL Content Hub]
role: User
source-git-commit: 15a266ccb6e4117c769d775a5f579fba943389bf
workflow-type: tm+mt
source-wordcount: '623'
ht-degree: 0%

---


# でのAssetsの検索 [!DNL Content Hub] {#search-assets}

![アセットバナー画像の共有](assets/search.png)

リポジトリに多数のアセットがある場合、適切なアセットの検索には時間がかかります。 [!DNL The Content Hub] 検索を使用すると、承認済みアセットを検索できるので、アセットに対して追加のアクション（ダウンロード、共有、コレクションの作成など）を実行できます。 様々な機能を利用して検索結果を絞り込むことができます。例えば、テキストベースの検索、フィルターの使用、タグまたはスマートタグ固有の検索の実行、特定のファイル形式の検索などを行うことができます。

## 検索対象  {#what-you-can-search}

この [!DNL Content Hub] 検索では、次に基づいて結果が得られます。

* **一致するテキスト：** この [!DNL Content Hub] 「検索」を使用すると、名前または説明を使用してアセットを検索できます。 キーワードベースの検索を実行して、アセットのプロパティで使用できるテキストとキーワードを比較できます。

* **一致するコンテキスト :** [!DNL Content Hub] 検索結果リストには、一致するコンテキストに基づいて取得したアセットの近似の結果が含まれます。 例えば、と入力した場合 `cool` 検索バーで、に関連するアセット `winter`, `snow`, `cold surroundings`検索リストに表示されます。

* **アセット情報（タイトル、タグ、スマートタグ）:** [!DNL Content Hub] では、スマート検索アルゴリズムを使用して、検索結果をできるだけ正確に、関連性の高いものにランク付けします。 [メタデータ](#asset-properties.md) は、あるアセットに使用可能なすべてのデータのコレクションですが、必ずしもそのアセットに含まれているとは限りません。 [アセットをさらに分類するのに役立ち、デジタル情報量が多くなるにつれてさらに役に立ちます](/help/assets/configure-content-hub-ui-options.md##configure-metadata-search-content-hub).

* **最終変更日：** 最近変更されたアセットが検索結果リストの上部に表示されます。 また、要件に応じて日付範囲をフィルタリングすることもできます。

* **使用方法：** よく使用されるアセットは、検索リストの上部に表示されます。

* **検索履歴：** 文字を入力せずに検索ボックス内をクリックすると、検索履歴が表示されます。 履歴から特定のキーワードを削除することもできます。 検索履歴は web ブラウザーのキャッシュメモリに保存されます。つまり、 [!DNL Content Hub] 別のブラウザーで検索するか、ブラウザーのキャッシュメモリをクリアすると、検索履歴を表示できなくなります。

* **入力中の検索：** この [!DNL Content Hub] 検索を使用すると、入力を開始する際にオートコンプリート候補が表示されるので、検索操作が向上します。

## 基本検索 {#basic-search}

で基本検索を実行するには [!DNL the Content Hub]で、検索バーに移動し、検索する必要があるキーワードを指定します。 左側のペインで使用可能なフィルターに移動し、それらを適用して検索結果を絞り込みます。

例えば、すべての **[!UICONTROL JPEG]** キーワード付き画像 `architect` その中で、昨年以内に変更されました。 このシナリオを実行するには、次の手順を実行します。

1. を指定 `architect` を検索キーワードとして使用します。

1. フィルターパネルに移動 > **[!UICONTROL 形式]** > を選択 **[!UICONTROL JPEG]**.

1. に移動します。 **[!UICONTROL 変更日]** > 日付範囲を指定します。

   ![基本検索](assets/basic-search.png)

## フィルターを使用して検索結果を絞り込む {#narrow-down-search-results}

フィルターパネルを使用すると、メタデータに基づいてアセットを検索できます。 様々な検索用述語に基づいて検索結果をフィルタリングできます。 適切なすべての述語を選択して、検索結果を最小限に抑えたり、絞り込んだりできます。 フィルター内で複数のオプションを選択すると、Content Hubには、フィルター内で選択されたいずれかのオプションに一致するアセットが表示されます。 ただし、フィルター間で複数のオプションを選択した場合、Content Hubには、検索結果を絞り込むために、フィルター間で選択されたすべてのオプションに一致するアセットのみが表示されます。

デフォルトのフィルターには、ファイル形式、承認者、承認日、期限切れのアセットと期限切れでないアセット、有効期限が含まれます。 管理者は、フィルターのリストに表示されるフィルターを設定することもできます。 詳しくは、を参照してください [Content Hub ユーザーインターフェイスの設定](configure-content-hub-ui-options.md#configure-filters-content-hub).

<!--

<table>
    <tbody>
     <tr>
      <th><strong>Search Predicate</strong></th>
      <th><strong>Description</strong></th>
      <th><strong>Properties</strong></th>
     </tr>
     <tr>
      <td> Campaigns </td>
      <td> Allows you to search using planned activity performed to take any particular action. For example, advertisement campaign run on Ferrari to know the understand the interests of people using number of clicks people perform.</td>
      <td>NA</td>
     </tr>
     <tr>
      <td> Channels </td>
      <td> Helps you to understand the path from where the asset is coming from. For example, web, social media, books, catalog, etc.</td>
      <td>NA</td>
     </tr>
     <tr>
      <td> Region </td>
      <td> Helps you to understand the location where the asset is created. For example, Japan, EMEA, Worldwide, etc.</td>
      <td>NA</td>
     </tr>
     <tr>
      <td> Keywords </td>
      <td> Keyword helps you search using terms or the words that you enter based on the topic. For example, images, low-resolution, etc.</td>
      <td>NA</td>
     </tr>
     <tr>
      <td> Timeframe </td>
      <td> Helps you search assets using timeline. For example, search by year 2024, Q3 2023, etc.</td>
      <td>NA</td>
     </tr>
     <tr>
      <td>File format</td>
      <td>Composition of an asset. The supported assets include image, document, video, printable media, and so on.</td>
      <td>
        <ul>
            <li>[!UICONTROL JPEG]</li> 
            <li>[!UICONTROL Quicktime]</li> 
            <li>[!UICONTROL PNG]</li> 
            <li>[!UICONTROL WebP]</li> 
            <li>[!UICONTROL MP4]</li> 
            <li>[!UICONTROL Plain]</li> 
            <li>[!UICONTROL PDF]</li>
            <li>[!UICONTROL SVG + XML]</li>
        </ul>
      </td>
     </tr>
     <tr>
      <td>Tags</td>
      <td>Tags help you categorize assets that can be browsed and searched more efficiently based on hierarchical taxonomies.</td>
      <td>
        <ul>
            <li>Field label</li>
            <li>Property name</li>
            <li>Path</li>
            <li>Description</li>
        </ul>
      </td>
     </tr>
     <!--<tr>
      <td>Subject</td>
      <td>Classification of assets based on their theme. For example, colorful, hiking, outdoors.</td>
      <td>NA</td>
     </tr>
          <tr>
      <td>Last modified</td>
      <td>Search assets based on their last modification. Specify the date range using the Start date and End date fields.</td>
      <td>
        <ul>
            <li>Range text (From)</li> 
            <li>Range text (To) </li>
        </ul>
      </td>
     </tr>    
     <!--<tr>
      <td>Asset ID</td>
      <td>Unique number that identifies the asset.</td>
      <td>NA</td>
     </tr>
     <tr>
      <td> Colors </td>
      <td> Helps you search assets using colors that are automatically identified in an asset using Adobe's Sensei AI capabilities.</td>
      <td>NA</td>
     </tr>  
    </tbody>
   </table>

-->

## 検索で詳細を確認 {#do-more-with-search}

[!DNL The Content Hub] は検索に限定されず、代わりに、次のような追加のアクションを実行できます [download](download-assets-content-hub.md), [share](share-assets-content-hub.md)、および [コレクションへのアセットの追加](collections-content-hub.md)検索またはプレビューインターフェイスから直接移動できます。 検索結果ページでアセットを選択して、これらのオプションを表示します。
