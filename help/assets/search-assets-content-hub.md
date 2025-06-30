---
title: コンテンツハブでアセットを検索する
description: ' [!DNL Content Hub] でのアセットの検索方法について学ぶ'
role: User
exl-id: 8578d7d0-32b9-4e5c-80ef-3827e358ac6c
source-git-commit: 32fdbf9b4151c949b307d8bd587ade163682b2e5
workflow-type: tm+mt
source-wordcount: '630'
ht-degree: 100%

---

# [!DNL Content Hub] でアセットを検索する {#search-assets}

リポジトリ内に多数のアセットがある場合、適切なアセットの検索には時間がかかります。[!DNL The Content Hub] 検索には、承認済みアセットを検索する機能が備わっており、ダウンロード、共有、コレクションの作成などの追加アクションを実行できます。テキストベースの検索、フィルターの使用、タグまたはスマートタグ固有の検索の実行、特定のファイル形式の検索など、様々な機能を使用して検索結果を絞り込むことができます。

## 前提条件 {#prerequisites}

[コンテンツハブユーザー](deploy-content-hub.md#onboard-content-hub-users)は、この記事で説明されているアクションを実行できます。

## 検索対象  {#what-you-can-search}

[!DNL Content Hub] 検索では、以下に基づいて結果が提供されます。

* **一致するテキスト：**[!DNL Content Hub] 検索では、名前または説明を使用してアセットを検索できます。キーワードベースの検索を実行して、キーワードをアセットのプロパティで使用可能なテキストと比較することができます。

* **一致するコンテキスト：**[!DNL Content Hub] の検索結果リストには、一致するコンテキストに基づいて取得されたアセットの近似結果が含まれます。例えば、検索バーに「`cool`」と入力すると、`winter`、`snow`、`cold surroundings` に関連するアセットが検索リストに表示されます。

* **アセット情報（タイトル、タグ、スマートタグ）：**[!DNL Content Hub] は、スマート検索アルゴリズムを使用して、検索結果を正確かつ可能な限り関連性に基づいてランク付けします。[メタデータ](#asset-properties.md)は、アセットに使用可能なすべてのデータのコレクションですが、必ずしもそのアセットに含まれているとは限りません。[アセットをより細かく分類するのに役立ち、デジタル情報量が多くなるにつれて有用になります。](/help/assets/configure-content-hub-ui-options.md##configure-metadata-search-content-hub)

* **最終変更日：**&#x200B;最近変更したアセットが検索結果リストの上部に表示されます。また、要件に応じて、日付範囲をフィルタリングすることもできます。

* **使用状況：**&#x200B;一般的に使用されているアセットが検索リストの上位に表示されます。

* **検索履歴：**&#x200B;検索履歴を取得するには、文字を入力せずに検索ボックス内をクリックします。また、履歴から特定のキーワードを削除することもできます。検索履歴は web ブラウザーのキャッシュメモリに保存されるので、別のブラウザーで [!DNL Content Hub] の検索にアクセスしたり、ブラウザーのキャッシュメモリをクリアしたりすると、検索履歴を表示できなくなります。

* **入力中に検索：**[!DNL Content Hub] 検索では、入力を開始するとオートコンプリートの候補が表示されるので、検索エクスペリエンスが向上します。

## 基本検索 {#basic-search}

[!DNL the Content Hub] で基本検索を実行するには、検索バーに移動し、検索する必要があるキーワードを指定します。左側のパネルで使用可能なフィルターに移動して適用し、検索結果を絞り込みます。

例えば、過去 1 年以内に変更されたキーワード `architect` を含むすべての **[!UICONTROL JPEG]** 画像を検索します。このシナリオを実行するには、次の手順を実行します。

1. 検索キーワードとして `architect` を指定します。

1. フィルターパネル／**[!UICONTROL 形式]**&#x200B;に移動し、「**[!UICONTROL JPEG]**」を選択します。

1. 「**[!UICONTROL 変更]**」に移動し、日付範囲を指定します。

   ![基本検索](assets/basic-search.png)

## フィルターを使用した検索結果の絞り込み {#narrow-down-search-results}

フィルターパネルを使用して、メタデータに基づいてアセットを検索します。様々な検索述語に基づいて、検索結果をフィルタリングできます。適切な述語をすべて選択して、検索結果を最小限に抑えたり、絞り込んだりすることができます。フィルター内で複数のオプションを選択すると、コンテンツハブには、フィルター内で選択したオプションのいずれかに一致するアセットが表示されます。ただし、フィルター全体で複数のオプションを選択した際、コンテンツハブには、フィルター全体で選択したすべてのオプションに一致するアセットのみが表示され、検索結果が絞り込まれます。

デフォルトのフィルターには、ファイル形式、承認者、承認日、有効期限切れのアセットと有効期限切れでないアセット、有効期限が含まれます。また、管理者は、フィルターのリストに表示されるフィルターを設定することもできます。詳しくは、[コンテンツハブユーザーインターフェイスの設定](configure-content-hub-ui-options.md#configure-filters-content-hub)を参照してください。

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

## 検索をさらに活用 {#do-more-with-search}

[!DNL The Content Hub] は検索だけでなく、検索またはプレビューインターフェイスから直接、[ダウンロード](download-assets-content-hub.md)、[共有](share-assets-content-hub.md)、[コレクションへのアセットの追加](collections-content-hub.md)などの追加アクションを実行できます。これらのオプションを表示するには、検索結果ページでアセットを選択します。
