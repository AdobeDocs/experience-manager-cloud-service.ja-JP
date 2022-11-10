---
title: でPDFドキュメントを管理 [!DNL Adobe Experience Manager].
description: でのPDFドキュメントの管理 [!DNL Adobe Experience Manager] as a [!DNL Cloud Service].
feature: Asset Management
role: User,Admin
source-git-commit: 9a600fb744c7064274fb4d849a5e01de2b83f575
workflow-type: tm+mt
source-wordcount: '794'
ht-degree: 0%

---

# Experience Manager AssetsでPDFドキュメントをas a Cloud Service {#add-assets-to-experience-manager}

Experience Manager AssetsはDocument CloudPDFビューアとシームレスに統合され、PDFドキュメントの複数ページをプレビューできます。 また、注釈、検索テキストなどの高度なDocument CloudPDFビューア機能を使用したり、しおりとサムネールを使用してPDFドキュメント内を移動したりすることもできます。 また、Experience Manager Assetsでは、サポートされている他の形式のドキュメントをアップロードし、PDF形式でプレビューすることもできます。

Document CloudPDFビューアには、次のようなメリットがあります。AEM Assets
* [PDFDocument Cloudビューアコンポーネントのサポート](#pdf-doc-cloud)
* [PDFアセットでの複数ページのプレビューと注釈のサポート](#multi-page)
* [他の形式のドキュメントでの複数ページのプレビューのサポート](#multi-format)

> ヒント
> 以前にアップロードしたPDFドキュメントの複数ページのプレビューを取得できない場合は、PDFを選択し、 **![再処理](/help/assets/assets/Reprocess.svg) アセットを再処理**.

## PDFDocument Cloudビューアコンポーネントのサポート {#pdf-doc-cloud}

ネイティブPDFの Doc Cloud ビューアは、AEM Assets内に次のコンポーネントを持っています。

* **ページサムネールを使用したPDFビューア** サムネール表示は、PDFドキュメントのページの小さなプレビューです。 サムネールを使用して、目的のページに直接ジャンプできます。 選択したPDFドキュメントのサムネールには、 ![サムネール](/help/assets/assets/thumbnail.svg) をクリックします。

* **ブックマークを使用したPDFビューア** ブックマークは、ドキュメント内のコンテンツに移動するための直接リンクです。 選択したブックマークドキュメントのPDFには、 ![ブックマーク](/help/assets/assets/bookmark.svg) をクリックします。

* **検索PDF** 検索を使用できます ![検索](/help/assets/assets/Search.svg) をクリックして、PDF文書のテキストを検索します。

* **上へ/下へページ** 上のページを使用 ![Page Up](/help/assets/assets/ArrowUp.svg) または Page Down ![Page Down](/help/assets/assets/ArrowDown.svg) をクリックして、ドキュメント内をスクロールします。

* **ズームアウト/ズームイン** ズームアウトを使用 ![ズームアウト](/help/assets/assets/ZoomOut.svg) またはズームイン ![ズームイン](/help/assets/assets/ZoomIn.svg) ドキュメントをストリークします。

* **ページに合わせる** 画面サイズに応じて、幅または高さの寸法を使用してドキュメントに合わせます。

* **ドック/ドック解除PDF** このオプションを使用して、ネイティブPDFビューアのコンポーネントをドッキングまたはドッキング解除できます。

## PDFアセットでの複数ページのプレビューと注釈のサポート {#multi-page}

Adobe Experience Manager Assets では、複数のページで構成されるPDFドキュメントをプレビューできます。 PDF・ドキュメントの複数のページをプレビューするには、次の手順を考慮します。

1. 手順に従って、 [AEMでのアセットのアップロード](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/manage/add-assets.html?lang=en).
1. アップロードするPDFドキュメントを参照し、プレビューします。
1. ドキュメントを開きます。
1. デフォルトでは、PDFドキュメントビューアが読み込まれます。 レンディションパネルの下で、PDFレンディションを選択することもできます。
1. レンディションドロップダウンで、「 **すべてのレンディション**.

また、 [注釈](#pdf-annotations) を複数ページのプレビューでPDFドキュメントに追加します。

> 注意
> プレビューできるアセットの最大サイズは 100 MB です。

>[!VIDEO](https://video.tv.adobe.com/v/3409355)

<!--
![Multi-page Preview](/help/assets/assets/multi-page.png)
-->

**PDF注釈{#pdf-annotations}**

Experience Manager Assetsでは、PDFドキュメントにコメントを追加できます。 1 つのPDFドキュメントに複数の注釈を付けることができます。

注釈ドキュメントにPDFを付けるには、次の手順を実行します。
1. Assets インターフェイスに移動し、注釈を付けるPDFドキュメントに移動します。 ネイティブPDFビューアが右側に開き、選択したPDFドキュメントのプレビューが表示されます。
1. クリック **注釈** をクリックします。
以下は、注釈ドキュメントに適用できるPDFです。

<table>
        <tr>
             <th> 注釈 </th>
            <th> 説明 </th>
        </tr>
        <tr>
           <td> <img src="/help/assets/assets/Comment.svg"> コメント </td>
            <td> 「コメント」を選択して、観察を表します。 </td>
        </tr>
        <tr>
            <td> <img src="/help/assets/assets/Text.svg"> テキストボックス </td>
            <td> 「テキストボックス」を選択して、テキストを入力します。 </td>
        </tr>
        <tr>
            <td> <img src="/help/assets/assets/Note.svg"> 付箋 </td>
            <td> PDFの特定の領域に追加できる小さなテキストまたはリマインダーを追加します。 </td>
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
            <td> クロスアウトするテキストを選択します。 </td>
        </tr>
        <tr>
            <td> <img src="/help/assets/assets/Draw.svg"> 描画 </td>
            <td> ビジュアルアートをPDFに挿入します。 </td>
        </tr>
        <tr>
            <td> <img src="/help/assets/assets/Erase.svg"> 図面を消去 </td>
             <td> 図面を削除または元に戻す。 </td>
        </tr>
    </table>

## 他の形式のドキュメントでの複数ページのプレビューのサポート {#multi-format}

PDFドキュメントに加えて、他の形式のドキュメントに対して複数のページをプレビューすることもできます。 サポートされるドキュメント形式のタイプは、TXT、RTF、DOC、DOCX、PPT、PPTX、XLS、XLSX です。 Experience Manager Assetsでは、これらのドキュメント形式がPDF形式に自動的に変換され、プレビューで使用できるようになります。

![他の形式でのドキュメントの複数ページのプレビュー](/help/assets/assets/multi-page-other-formats.png)

サポートされている他のドキュメント形式の複数ページプレビューを表示するには、次の手順を実行します。
1. 手順に従って、 [AEMでのアセットのアップロード](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/manage/add-assets.html?lang=en).
1. アップロードしてプレビューするドキュメントを参照します。
1. ドキュメントを開きます。
1. 左パネルの静的セクションの下のPDFを選択します。 右側のパネルには、1 つのアセットの複数ページのプレビューが表示されます。 左のパネルから「サムネール」を選択し、プレビューするページを選択します。

> 注意
> * プレビューできるアセットの最大サイズは 100 MB です。
> * プレビューする XLS または XLSX ファイルの最大サイズは 20 MB です。
> 

