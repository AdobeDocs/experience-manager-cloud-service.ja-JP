---
title: ' [!DNL Adobe Experience Manager] で PDF ドキュメントを管理します。'
description: ' [!DNL Adobe Experience Manager] as a [!DNL Cloud Service] で PDF ドキュメントを管理します。'
feature: Asset Management
role: User, Admin
exl-id: 29660869-6902-4093-845b-cd629be59d4d
source-git-commit: e22e4e530c2d023724b360c488cab2b59ec22fc4
workflow-type: tm+mt
source-wordcount: '853'
ht-degree: 97%

---

# Experience Manager Assets as a Cloud Service での PDF ドキュメントの管理 {#add-assets-to-experience-manager}

| [検索のベストプラクティス](/help/assets/search-best-practices.md) | [メタデータのベストプラクティス](/help/assets/metadata-best-practices.md) | [コンテンツハブ](/help/assets/product-overview.md) | [OpenAPI 機能を備えた Dynamic Media](/help/assets/dynamic-media-open-apis-overview.md) | [AEM Assets 開発者向けドキュメント](https://developer.adobe.com/experience-cloud/experience-manager-apis/) |
| ------------- | --------------------------- |---------|----|-----|

Experience Manager Assets は、Document Cloud PDF ビューアとシームレスに統合され、PDF ドキュメントの複数ページをプレビューできます。 さらに、注釈、テキストの検索、ブックマークやサムネールを使用した PDF ドキュメント内の移動など、高度な Document Cloud PDF ビューア機能も使用できます。Experience Manager Assets では、サポートされている他の形式でドキュメントをアップロードし、PDF 形式でプレビューすることもできます。

Document Cloud PDF ビューアは、AEM Assets に次のようなメリットをもたらします。

* [PDF Document Cloud ビューアコンポーネントのサポート](#pdf-doc-cloud)
* [PDF アセットでの複数ページのプレビューと注釈のサポート](#multi-page)
* [他の形式のドキュメントへの複数ページプレビューのサポート](#multi-format)

>[!TIP]
>
> 以前にアップロードしたPDFドキュメントの複数ページのプレビューを取得できない場合は、PDFを選択し、![ 再処理 ](/help/assets/assets/Reprocess.svg)**Assetsを再処理** をクリックします。

## PDF Document Cloud ビューアコンポーネントのサポート {#pdf-doc-cloud}

ネイティブの PDF Doc Cloud ビューアには、AEM Assets 内に次のコンポーネントがあります。

* **ページサムネールを使用した PDF ビューア** サムネール表示とは、PDF ドキュメントのページの小さなプレビューです。 サムネールを使用して、目的のページに直接ジャンプできます。 選択した PDF ドキュメントのサムネールには、左側のペインの![サムネール](/help/assets/assets/thumbnail.svg)からアクセスできます。

* **ブックマークを使用した PDF ビューア** ブックマークは、ドキュメント内のコンテンツに移動するための直接リンクです。 選択した PDF ドキュメントのブックマークには、左側のペインの![ブックマーク](/help/assets/assets/bookmark.svg)からアクセスできます。

* **PDF 内を検索** ![検索](/help/assets/assets/Search.svg)を使用して、PDF ドキュメント内のテキストを検索できます。 

* **ページアップ／ページダウン** ドキュメントをスクロールするには、ページアップ ![Page Up](/help/assets/assets/ArrowUp.svg) またはページダウン ![Page Down](/help/assets/assets/ArrowDown.svg) を使用します。

* **ズームアウト／ズームイン** ズームアウト![ズームアウト](/help/assets/assets/ZoomOut.svg)またはズームイン![ズームイン](/help/assets/assets/ZoomIn.svg)を使用して、ドキュメントを素早く確認します。

* **全体表示** 幅または高さの寸法を使用して、画面サイズに合わせてドキュメントを表示します。

* **PDF のドッキング／ドッキング解除** このオプションを使用して、ネイティブ PDF ビューアのコンポーネントをドッキングまたはドッキング解除できます。

## PDF アセットでの複数ページのプレビューと注釈のサポート {#multi-page}

Adobe Experience Manager Assets では、複数のページで構成される PDF ドキュメントをプレビューできます。PDF ドキュメントの複数ページをプレビューするには、次の手順を検討してください。

1. [AEM でアセットをアップロード](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/manage/add-assets.html?lang=ja)する手順に従います。
1. アップロードしてプレビューする PDF ドキュメントを参照します。
1. ドキュメントを開きます。
1. デフォルトで、PDF ドキュメントビューアが読み込まれます。 レンディションパネルの下で、PDF レンディションを選択することもできます。
1. 「レンディション」ドロップダウンで、「**すべてのレンディション**」を選択します。

また、複数ページのプレビューで、PDF ドキュメントに[注釈](#pdf-annotations)を適用することもできます。

>[!NOTE]
>
> プレビューできるアセットの最大サイズは 100 MB です。

>[!VIDEO](https://video.tv.adobe.com/v/3409355)

<!--
![Multi-page Preview](/help/assets/assets/multi-page.png)
-->

**PDF 注釈{#pdf-annotations}**

Experience Manager Assets では、PDF ドキュメントにコメントを追加できます。 1 つの PDF ドキュメントに複数の注釈を付けることができます。

PDF ドキュメントに注釈を付けるには、次の手順を実行します。

1. Assets インターフェイスに移動し、注釈を付ける PDF ドキュメントに移動します。 ネイティブ PDF ビューアが右側に開き、選択した PDF ドキュメントのプレビューが表示されます。
1. トップメニューから「**注釈**」をクリックします。
以下は、PDF ドキュメントに適用できる注釈です。

<table>
        <tr>
             <th> 注釈 </th>
            <th> 説明 </th>
        </tr>
        <tr>
           <td> <img src="/help/assets/assets/Comment.svg"> コメント </td>
            <td> 選択してコメントを記入します。 </td>
        </tr>
        <tr>
            <td> <img src="/help/assets/assets/Text.svg"> テキストボックス </td>
            <td> 「テキストボックス」を選択してテキストを入力します。 </td>
        </tr>
        <tr>
            <td> <img src="/help/assets/assets/Note.svg"> 付箋 </td>
            <td> PDF の特定の領域に追加できる小さなテキストまたはリマインダーを追加します。 </td>
        </tr>
        <tr>
            <td> <img src="/help/assets/assets/Comment.svg"> テキストハイライター </td>
            <td> 異なる色でハイライト表示するテキストを選択します。 </td>
        </tr>
        <tr>
            <td> <img src="/help/assets/assets/TextUnderline.svg"> テキスト下線 </td>
            <td> 下線を引くテキストを選択します。 </td>
        </tr>
        <tr>
            <td> <img src="/help/assets/assets/TextStrikethrough.svg"> 打ち消し線 </td>
            <td> 打ち消し線を引くテキストを選択します。 </td>
        </tr>
        <tr>
            <td> <img src="/help/assets/assets/Draw.svg"> 描画 </td>
            <td> ビジュアルアートを PDF に挿入します。 </td>
        </tr>
        <tr>
            <td> <img src="/help/assets/assets/Erase.svg"> 描画を消去 </td>
             <td> 描画を削除または取り消します。 </td>
        </tr>
    </table>

>[!NOTE]
>
>注釈ドキュメントに追加した注釈は、PDFモードで使用できます。 ただし、注釈ドキュメントをダウンロードまたは印刷する際には、PDFは表示されません。

## 他の形式のドキュメントに対する複数ページプレビューのサポート {#multi-format}

PDF ドキュメントに加えて、他の形式のドキュメントを複数ページにわたってプレビューすることもできます。サポート対象となっているドキュメント形式のタイプは、TXT、RTF、DOC、DOCX、PPT、PPTX、XLS、XLSX です。Experience Manager Assets では、これらのドキュメント形式が PDF 形式に自動的に変換され、プレビューできるようになります。

![他の形式のドキュメントに対する複数ページプレビュー](/help/assets/assets/multi-page-other-formats.png)

サポートされている他のドキュメント形式を複数ページにわたりプレビュー表示するには、次の手順を実行します。

1. [AEM にアセットをアップロードする](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/manage/add-assets.html?lang=ja)手順に従います。
1. アップロードおよびプレビュー対象のドキュメントを参照します。
1. ドキュメントを開きます。
1. 左側のパネルの静的セクションの下にある PDF を選択します。右側のパネルには、アセットの複数ページのプレビューが表示されます。左側のパネルでサムネールを選択し、プレビューするページを選びます。

>[!NOTE]
>
> * プレビューできるアセットの最大サイズは 100 MB です。
> * プレビューできる XLS または XLSX ファイルの最大サイズは 20 MB です。

**関連情報**

* [アセットを翻訳](translate-assets.md)
* [Assets HTTP API](mac-api-assets.md)
* [AEM Assets as a Cloud Service でサポートされているファイル形式](file-format-support.md)
* [アセットを検索](search-assets.md)
* [接続されたアセット](use-assets-across-connected-assets-instances.md)
* [アセットレポート](asset-reports.md)
* [メタデータスキーマ](metadata-schemas.md)
* [アセットをダウンロード](download-assets-from-aem.md)
* [メタデータを管理](manage-metadata.md)
* [検索ファセット](search-facets.md)
* [コレクションを管理](manage-collections.md)
* [メタデータの一括読み込み](metadata-import-export.md)
* [AEM および Dynamic Media へのアセットの公開](/help/assets/publish-assets-to-aem-and-dm.md)
