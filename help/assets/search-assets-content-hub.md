---
title: コンテンツハブでのアセットの検索
description: ' [!DNL Content Hub] でアセットを検索する方法を説明します。'
role: User
exl-id: 8578d7d0-32b9-4e5c-80ef-3827e358ac6c
source-git-commit: ed7331647ea2227e6047e42e21444b743ee5ce6d
workflow-type: tm+mt
source-wordcount: '662'
ht-degree: 1%

---

# [!DNL Content Hub] でのAssetsの検索 {#search-assets}

![ アセットを共有のバナー画像 ](assets/search.png)

>[!AVAILABILITY]
>
>Content Hub ガイドがPDF形式で利用できるようになりました。 ガイド全体をダウンロードし、Adobe Acrobat AI アシスタントを使用して質問に答えます。
>
>[!BADGE Content Hub ガイドのPDF]{type=Informative url="https://helpx.adobe.com/content/dam/help/en/experience-manager/aem-assets/content-hub.pdf"}

リポジトリに多数のアセットがある場合、適切なアセットの検索には時間がかかります。 [!DNL The Content Hub] の検索では、承認済みアセットを検索できるので、アセットに対して追加のアクション（ダウンロード、共有、コレクションの作成など）を実行できます。 様々な機能を利用して検索結果を絞り込むことができます。例えば、テキストベースの検索、フィルターの使用、タグまたはスマートタグ固有の検索の実行、特定のファイル形式の検索などを行うことができます。

## 前提条件 {#prerequisites}

[Content Hub ユーザー ](deploy-content-hub.md#onboard-content-hub-users) は、この記事で説明されるアクションを実行できます。

## 検索対象  {#what-you-can-search}

[!DNL Content Hub] の検索は、次に基づいて結果を提供します。

* **一致するテキスト：**[!DNL Content Hub] 検索では、名前または説明を使用してアセットを検索できます。 キーワードベースの検索を実行して、アセットのプロパティで使用できるテキストとキーワードを比較できます。

* **一致するコンテキスト：** 検索結果リスト [!DNL Content Hub] は、一致するコンテキストに基づいて取得するアセットの近接結果が含まれます。 例えば、検索バーに「`cool`」と入力すると、`winter`、`snow`、`cold surroundings` に関連するアセットが検索リストに表示されます。

* **アセット情報（タイトル、タグ、スマートタグ）:** [!DNL Content Hub] では、スマート検索アルゴリズムを使用して、検索結果をできる限り正確に、関連性の高いものとしてランク付けします。 [ メタデータ ](#asset-properties.md) は、対象のアセットに使用できるすべてのデータのコレクションですが、必ずしもそのアセットに含まれているとは限りません。 [ アセットをさらに分類するのに役立ち、デジタル情報量が増えるにつれてさらに役に立ちます ](/help/assets/configure-content-hub-ui-options.md##configure-metadata-search-content-hub)。

* **最終変更日：** 最近変更されたアセットが検索結果リストの上部に表示されます。 また、要件に応じて日付範囲をフィルタリングすることもできます。

* **使用法：** よく使用されるアセットは、検索リストの上部に表示されます。

* **検索履歴：** 文字を入力せずに検索ボックス内をクリックすると、検索履歴を取得できます。 履歴から特定のキーワードを削除することもできます。 検索履歴は web ブラウザーのキャッシュメモリに保存されます。つまり、別のブラウザーで [!DNL Content Hub] 検索にアクセスしたり、ブラウザーのキャッシュメモリをクリアしたりすると、検索履歴を表示できなくなります。

* **入力中に検索：**[!DNL Content Hub] 検索を使用すると、入力を開始する際にオートコンプリート候補が表示されるので、検索機能が強化されます。

## 基本検索 {#basic-search}

[!DNL the Content Hub] で基本検索を実行するには、検索バーに移動し、検索する必要があるキーワードを指定します。 左側のペインで使用可能なフィルターに移動し、それらを適用して検索結果を絞り込みます。

例えば、キーワード `architect` が含まれている **[!UICONTROL JPEG]** 画像をすべて検索します。この画像は、昨年の間に変更されました。 このシナリオを実行するには、次の手順を実行します。

1. 検索キーワードとして `architect` を指定します。

1. フィルターパネル / **[!UICONTROL 形式]** /「**[!UICONTROL JPEG]**」を選択します。

1. **[!UICONTROL 変更]** に移動し、日付範囲を指定します。

   ![ 基本検索 ](assets/basic-search.png)

## フィルターを使用して検索結果を絞り込む {#narrow-down-search-results}

フィルターパネルを使用すると、メタデータに基づいてアセットを検索できます。 様々な検索用述語に基づいて検索結果をフィルタリングできます。 適切なすべての述語を選択して、検索結果を最小限に抑えたり、絞り込んだりできます。 フィルター内で複数のオプションを選択すると、Content Hubには、フィルター内で選択されたいずれかのオプションに一致するアセットが表示されます。 ただし、フィルター間で複数のオプションを選択した場合、Content Hubには、検索結果を絞り込むために、フィルター間で選択されたすべてのオプションに一致するアセットのみが表示されます。

デフォルトのフィルターには、ファイル形式、承認者、承認日、期限切れのアセットと期限切れでないアセット、有効期限が含まれます。 管理者は、フィルターのリストに表示されるフィルターを設定することもできます。 詳しくは、[Content Hub ユーザーインターフェイスの設定 ](configure-content-hub-ui-options.md#configure-filters-content-hub) を参照してください。

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

[!DNL The Content Hub] れは検索に限定されるものではなく、検索またはプレビューインターフェイスから直接、[ ダウンロード ](download-assets-content-hub.md)、[ 共有 ](share-assets-content-hub.md)、[ コレクションへのアセットの追加 ](collections-content-hub.md) などの追加アクションを実行できます。 検索結果ページでアセットを選択して、これらのオプションを表示します。
