---
title: Dynamic Media での 3D アセットの使用
description: Dynamic Media で 3D アセットを使用する方法について説明します.
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS and Experience Manager as a Cloud Service
topic-tags: introduction
content-type: reference
feature: 3D Assets
role: User
exl-id: 82084ba7-1302-4cbd-8626-d77b3aaa4ed1
source-git-commit: c82f84fe99d8a196adebe504fef78ed8f0b747a9
workflow-type: tm+mt
source-wordcount: '2298'
ht-degree: 98%

---

# Dynamic Media での 3D アセットの使用 {#working-with-three-d-assets-dm}

<table>
    <tr>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i> 新規 </i></sup>Dynamic Media Prime<a href="/help/assets/dynamic-media/dm-prime-ultimate.md"><b>Ultimate</b></a>
        </td>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i> 新規 </i></sup> <a href="/help/assets/assets-ultimate-overview.md"><b>AEM AssetsUltimate</b></a>
        </td>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i> 新規 </i></sup> <a href="/help/assets/integrate-aem-assets-edge-delivery-services.md"><b>AEM AssetsとEdge Delivery Servicesの統合 </b></a>
        </td>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i> 新規 </i></sup><a href="/help/assets/aem-assets-view-ui-extensibility.md"><b>UI 拡張機能 </b></a>
        </td>
          <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>Dynamic Media Prime</i></sup>Ultimateの新 <a href="/help/assets/dynamic-media/enable-dynamic-media-prime-and-ultimate.md"><b> 能 </b></a>
        </td>
    </tr>
    <tr>
        <td>
            <a href="/help/assets/search-best-practices.md"><b>検索のベストプラクティス</b></a>
        </td>
        <td>
            <a href="/help/assets/metadata-best-practices.md"><b>メタデータのベストプラクティス</b></a>
        </td>
        <td>
            <a href="/help/assets/product-overview.md"><b>コンテンツハブ</b></a>
        </td>
        <td>
            <a href="/help/assets/dynamic-media-open-apis-overview.md"><b>OpenAPI 機能を備えた Dynamic Media</b></a>
        </td>
        <td>
            <a href="https://developer.adobe.com/experience-cloud/experience-manager-apis/"><b>AEM Assets 開発者向けドキュメント</b></a>
        </td>
    </tr>
</table>

Dynamic Media を使用すると、3D アセットを、没入感のあるエクスペリエンスとしてアップロード、管理、表示および配信できます。

* 3D アセットをワンクリックで公開（ツールバーの&#x200B;**[!UICONTROL クイック公開]**&#x200B;を使用）して URL を生成。
* Adobe Dimension を使用した、高品質でインタラクティブなディメンショナルビューアプリセットで、3D アセットの表示のサポートを最適化。
* 3D メディア WCM コンポーネントによって、[!DNL Adobe Experience Manager Sites] ページに 3D アセットを簡単に追加可能。

Dynamic Media で 3D アセットを使用するときに、追加のインストールは必要ありません。

![3D の靴](/help/assets/dynamic-media/assets/3d-dimensional-viewer-quickpublish-url-embed2a.png)

<!-- See also [Dynamic Media 3D Release Notes](/help/release-notes/aem3d-release-notes.md). -->

## Dynamic Media でサポートされる 3D 形式 {#supported-three-d-file-formats-in-dm}

Dynamic Media は、次の 3D ファイル形式をサポートしています。

[Experience Manager Assets でサポートされる 3D 形式](/help/assets/file-format-support.md#support-3d-formats) も参照してください

| 3D ファイル拡張子 | ファイル形式 | MIME タイプ | 備考 |
|---|---|---|---|
| GLB | バイナリ GL 伝送 | model/gltf-binary | マテリアルとテクスチャを単一のアセットとして含めます。 |
| OBJ | WaveFront 3D オブジェクトファイル | application/x-tgif |  |
| STL | ステレオリソグラフィ | application/vnd.ms-pki.stl |  |
| USDZ | 汎用シーン記述 Zip アーカイブ | model/vnd.usdz+zip | *取り込みのみサポート。表示やインタラクションは利用不可。* USDZ は独自の 3D 形式で、Safari や iOS でネイティブに表示できます。 |

アセットの詳細ページの 3D メディア WCM コンポーネントと 3D プレビューは、最新バージョンの Chrome（97.x）と互換性がありません。3D アセットを操作するには、代わりに Firefox または Safari を使用するか、以前のバージョンの Chrome（96.x）を使用します。

## クイックスタート：Dynamic Media 内の 3D アセット {#quick-start-three-d}

次のワークフローの手順説明は、Dynamic Media 内の 3D アセットをすぐに使い始めることを目的としたものです。

Dynamic Media で 3D アセットを使用する前に、[!DNL Experience Manager] の管理者が既に Dynamic Media Cloud Services を有効にして設定を完了していることを確認してください。

詳しくは、[Dynamic Media Cloud Services の設定](/help/assets/dynamic-media/config-dm.md#configuring-dynamic-media-cloud-services)を参照してください。

1. **3D アセットのアップロード**

   * [Dynamic Media で使用する 3D アセットのアップロード](/help/assets/add-assets.md#upload-assets)
   * [Dynamic Media のアップロードでサポートされる 3D ファイル形式](#supported-three-d-file-formats-in-dm)

1. **3D アセットの管理**

   * 3D アセットの整理と検索

      * [デジタルアセットの編成](/help/assets/organize-assets.md)
      * [3D アセットの検索](/help/assets/search-assets.md)

   * 3D アセットの表示

      * [3D アセットの表示とインタラクション](#viewing-three-d-assets)
      * [ディメンショナルビューアプリセットの管理](/help/assets/dynamic-media/managing-viewer-presets.md)

   * 3D アセットメタデータの操作

      * [デジタルアセットのメタデータの管理](/help/assets/manage-digital-assets.md#editing-properties)
      * [メタデータスキーマ](/help/assets/metadata-schemas.md)

1. **3D アセットの公開**

   * [静的 Dynamic Media 3D アセットの公開](#publishing-three-d-assets)
   * [ディメンショナルビューアを使用した、Dynamic Media 3D アセットの代替の公開方法](#alternate-publish-methods)

## 3D アセットの表示とインタラクションについて {#viewing-three-d-assets}

この節では、3D アセットの表示およびインタラクション方法を、アセットの詳細ページ内から、または Sites の 3D メディアコンポーネント内からの 2 通り説明します。

このインタラクティブ 3D ビューアには、3D アセットをオービット、ズームおよびパンできる、インタラクティブなカメラコントロールのコレクションが含まれます。

アセットの詳細ページビューで 3D アセットを開くのにかかる時間は、いくつかの要因に依存します。要因には以下のものが含まれます。

* サーバーの帯域幅
* サーバーの待ち時間
* 画像の複雑さ

さらに、カメラをインタラクティブに操作する際に、ワークステーション、ノートパソコン、モバイルタッチデバイスなどのクライアントコンピューターの性能を考慮することも重要です。グラフィック性能に優れ、ある程度パワフルなシステムなら、インタラクティブな 3D 表示をよりスムーズで満足なものにすることができます。

>[!TIP]
>
>ディメンショナルビューアプリセットをビューアプリセットエディターで開いて、3D ファイルをアップロードせずに 3D アセット内を移動する練習ができます。ディメンショナルビューアプリセットには、操作できる組み込みの 3D アセットがあります。
>
>詳しくは、[ビューアプリセットの管理](/help/assets/dynamic-media/managing-viewer-presets.md)を参照してください。

## アセットの詳細ページからの 3D アセットの表示とインタラクション {#viewing-three-d-assets-from-asset-details-page}

[ソフトウェアインターフェイスを使用したアセットのプレビュー](/help/assets/dynamic-media/previewing-assets.md) も参照してください。

**アセットの詳細ページから 3D アセットの表示とインタラクションを行うには：**

1. 3D アセットが [!DNL Experience Manager] にアップロードされていることを確認します。

   詳しくは、[Dynamic Media で使用する 3D アセットのアップロード](/help/assets/add-assets.md#upload-assets)を参照してください。

1. [!DNL Experience Manager] の&#x200B;**[!UICONTROL ナビゲーション]**&#x200B;ページで&#x200B;**[!UICONTROL アセット／ファイル]**&#x200B;を選択します。
1. ページの右上隅付近にある「**[!UICONTROL 表示]**」ドロップダウンリストで「**[!UICONTROL カード表示]**」を選択します。
1. 表示する 3D アセットに移動します。
1. 詳細ページでアセットを開くには、3D アセットのカードを選択します。
1. 3D アセットの詳細ページで、次のいずれかの操作を行います。

   | 表示 | 説明 | マウス操作 | タッチスクリーン操作 |
   | --- | --- | --- | --- |
   | **カメラを回転** | 3D シーンとオブジェクトの周囲でビューを周回させます。 | 左クリックしながらドラッグします。 | 1 本指で押しながらドラッグします。 |
   | **カメラをパン** | ビューを左、右、上、下にパンします。 | 右クリックしながらドラッグします。 | 2 本指で押しながらドラッグします。 |
   | **カメラをズーム** | 3D シーンの領域の内外に移動します。 | ホイールをスクロールします。 | 2 本指でピンチします。 |
   | **カメラを中心に戻す** | カメラを中心の位置に戻し、3D シーンのオブジェクトに合わせます。 | ダブルクリックします。 | ダブルクリックします。 |
   | **リセット** | ページの右下隅付近にあるリセットアイコンを選択して、視野のターゲットポイントを 3D アセットの中心に戻します。リセットを使用しても、アセット全体を表示したり、適切な表示サイズで表示するために、カメラを近づけたり遠ざけたりできます。 |   |   |
   | **全画面表示モード** | フルスクリーンモードに入るには、ページの右下隅にあるフルスクリーンアイコンを選択します。 |   |   |

1. ページの右上隅にある「**[!UICONTROL 閉じる]**」を選択して、アセットページに戻ります。

## 3D メディアコンポーネント内の 3D アセットの表示とインタラクション {#interacting-with-asset-inside-three-d-media-component}

Web ページが&#x200B;**[!UICONTROL 編集]**&#x200B;モードの場合、3D アセットとのインタラクションは行えません。アセットをインタラクティブにするには、**[!UICONTROL プレビュー]**&#x200B;機能を使用して、3D メディアコンポーネントの機能にフルアクセスできるページエディターで Web ページを表示します。

>[!IMPORTANT]
>
>このタスクは、3D メディアコンポーネントを Web ページに追加し、3D アセットをコンポーネントに割り当てた後にのみ実行できます。詳しくは、[Web ページへの 3D メディアコンポーネントの追加](#adding-the-three-d-media-component-to-a-web-page)および [3D メディアコンポーネントへの 3D アセットの割り当て](#assigning-a-three-d-asset-to-the-component)を参照してください。

[ソフトウェアインターフェイスを使用したアセットのプレビュー](/help/assets/dynamic-media/previewing-assets.md) も参照してください。

**3D メディアコンポーネント内の 3D アセットの表示とインタラクションを行うには：**

1. Web ページが&#x200B;**[!UICONTROL 編集]**&#x200B;モードの間に、次のいずれかの操作を行います。

   * ページ右上付近にある「**[!UICONTROL プレビュー]**」をクリックして&#x200B;**[!UICONTROL プレビュー]**&#x200B;モードに入ります。
   * ブラウザーのページ URL から `/editor.html` を削除します。

   ![3D メディアコンポーネント内に表示される 3D アセット](/help/assets/dynamic-media/assets/3d-asset-in-3d-mediaa.png)
**[!UICONTROL プレビュー]**&#x200B;モードで表示された完全にインタラクティブな 3D アセット。

1. **[!UICONTROL プレビュー]**&#x200B;モードの間に、次のいずれかの操作を行います。

   | 表示 | 説明 | マウス操作 | タッチスクリーン操作 |
   | --- | --- | --- | --- |
   | **カメラを回転** | 3D シーンとオブジェクトの周囲でビューを周回させます。 | 左クリックしながらドラッグします。 | 1 本指で押しながらドラッグします。 |
   | **カメラをパン** | ビューを左、右、上、下にパンします。 | 右クリックしながらドラッグします。 | 2 本指で押しながらドラッグします。 |
   | **カメラをズーム** | 3D シーンの領域の内外に移動します。 | ホイールをスクロールします。 | 2 本指でピンチします。 |
   | **カメラを中心に戻す** | カメラを中心の位置に戻し、3D シーンのオブジェクトに合わせます。 | ダブルクリックします。 | ダブルクリックします。 |
   | **リセット** | ページの右下隅付近にあるリセットアイコンを選択して、視野のターゲットポイントを 3D アセットの中心に戻します。リセットを使用しても、アセット全体を表示したり、適切な表示サイズで表示するために、カメラを近づけたり遠ざけたりできます。 |   |   |
   | **全画面表示モード** | フルスクリーンモードに入るには、ページの右下隅にあるフルスクリーンアイコンを選択します。 |   |   |

## 3D メディアコンポーネントの操作について {#working-with-three-d-media-component}

Dynamic Media には、Dynamic Media 3D メディアコンポーネントが含まれており、それを [!DNL Experience Manager Sites] で使用して、Web ページ上で 3D モデルをインタラクティブに表示できます。

* [ページテンプレートへの 3D メディアコンポーネントの追加](#adding-three-d-media-component-to-page-template)
* [Web ページへの 3D メディアコンポーネントの追加](#adding-the-three-d-media-component-to-a-web-page)
   * [オプション - 3D メディアコンポーネントの設定](#configuring-the-three-d-component)
* [3D メディアコンポーネントへの 3D アセットの割り当て](#assigning-a-three-d-asset-to-the-component)

## ページテンプレートへの 3D メディアコンポーネントの追加 {#adding-three-d-media-component-to-page-template}

1. **[!UICONTROL ツール]**／**[!UICONTROL 一般]**／**[!UICONTROL テンプレート]**&#x200B;に移動します。
1. 3D コンポーネントを有効にするページテンプレートに移動し、テンプレートを選択します。
1. テンプレートを開くには、「**[!UICONTROL 編集]**」を選択します。
1. ページの右上付近にあるドロップダウンメニューで、「**[!UICONTROL 構造]**」モードを選択します（まだアクティブでない場合）。

   ![3d-media-component-structure](/help/assets/dynamic-media/assets/3d-media-component-structurea.png)

1. 空の領域を選択し、それに関連するツールバーを開くには、 **[!UICONTROL レイアウトコンテナ]** 領域で空の領域を選択します。
1. ツールバーで、**[!UICONTROL ポリシー]**&#x200B;アイコンを選択し、**[!UICONTROL ポリシーエディターを開きます]**。
1. 「**[!UICONTROL プロパティ]**」セクションの「**[!UICONTROL 許可されたコンポーネント]**」タブで、「**[!UICONTROL Dynamic Media]**」までスクロールし、リストを展開して、「**[!UICONTROL 3D メディア]**」をチェックします。
1. 「**[!UICONTROL 完了]**」を選択して変更を保存し、**[!UICONTROL ポリシーエディター]**&#x200B;を閉じます。

   これで、この Dynamic Media を使用するすべてのページに 3D メディアコンポーネントを配置できます。

## Web ページへの 3D メディアコンポーネントの追加 {#adding-the-three-d-media-component-to-a-web-page}

[!DNL Experience Manager] を Web コンテンツ管理システムとして使用している場合は、3D メディアコンポーネントを使用して Web ページに 3D アセットを追加できます。

[ページへの Dynamic Media アセットの追加](/help/assets/dynamic-media/adding-dynamic-media-assets-to-pages.md) も参照してください。

1. [!DNL Experience Manager Sites] を開き、Dynamic Media 3D メディアコンポーネントを追加する Web ページを選択します。
1. ページをページエディターで開くには、 **[!UICONTROL 編集]** （鉛筆）アイコンを選択します。ページの右上付近で&#x200B;**[!UICONTROL 編集]**&#x200B;モードが選択されていることを確認します。

   ![3d-media-component-add](/help/assets/dynamic-media/assets/3d-media-component-edita.png)

1. ツールバーで、サイドパネルアイコンを選択して、パネルの表示を切り替えるか、「オン」にします。

1. サイドパネルで、プラス記号アイコンを選択し、**[!UICONTROL コンポーネント]**&#x200B;リストを開きます。

   ![3d-media-component-drag-drop](/help/assets/dynamic-media/assets/3d-assets-filtera.png)

1. **[!UICONTROL コンポーネント]**&#x200B;リストから、**[!UICONTROL 3D メディア]**&#x200B;コンポーネントを、3D ビューアを表示するページ上の場所にドラッグします。

これで、3D アセットをコンポーネントに割り当てる準備が整いました。

詳しくは、[3D メディアコンポーネントへの 3D アセットの割り当て](#assigning-a-three-d-asset-to-the-component)を参照してください

### オプション - 3D メディアコンポーネントの設定 {#configuring-the-three-d-component}

1. [!DNL Experience Manager Sites] のページエディターで、前にページに追加した **[!UICONTROL 3D メディアビューア]** コンポーネントを選択します。
1. コンポーネント設定ダイアログボックスを開くには、 **[!UICONTROL 設定]** （レンチ）アイコンを選択します。

   ![3d-media-component-config](/help/assets/dynamic-media/assets/3d-media-component-configa.png)

1. 3D メディアダイアログボックスの「ビューアプリセット」ドロップダウンリストで、「**[!UICONTROL ディメンション]**」を選択して、ディメンショナルビューアプリセットをコンポーネントに割り当てます。

   ![3d-media-component-edit-config](/help/assets/dynamic-media/assets/3d-media-component-edit-configa.png)

1. 右上隅のチェックマークを選択して、変更を保存します。

## 3D メディアコンポーネントへの 3D アセットの割り当て {#assigning-a-three-d-asset-to-the-component}

Web ページに 3D メディアコンポーネントを追加した後、3D アセットを割り当てることができます。

[Web ページへの 3D メディアコンポーネントの追加](#adding-the-three-d-media-component-to-a-web-page)を参照してください。

1. [!DNL Experience Manager Sites] のページエディターで、**[!UICONTROL Assets]** アイコンをクリックして、サイドパネルの **[!UICONTROL Assets]** を開きます。
1. ドロップダウンリストで、「**[!UICONTROL 3D]**」を選択して 3D アセットファイルタイプのみを表示します。
1. サイドパネルで、編集中のページに表示する 3D アセットを検索するか、スクロールして見つけます。
1. 3D アセットを Assets サイドパネルからドラッグし、前にページに追加した **[!UICONTROL 3D メディア]**&#x200B;コンポーネントにドロップします。

   ![3D アセットを 3D メディアコンポーネントに割り当て](/help/assets/dynamic-media/assets/3d-asset-adda.png)

>[!NOTE]
>
>Web ページが [!DNL Experience Manager Sites] **[!UICONTROL 編集]** モードの場合、3D メディアコンポーネントは 3D アセットを表示しますが、アセットとのインタラクションはできません。アセットをインタラクティブにするには、**[!UICONTROL プレビュー]**&#x200B;機能を使用して、3D メディアコンポーネントの機能にフルアクセスできるページエディターで Web ページを表示します。

## 静的 Dynamic Media 3D アセットの公開 {#publishing-three-d-assets}

Dynamic Media では、Dynamic Media で&#x200B;*静的コンテンツ*&#x200B;としてサポートされる様々な 3D ファイル形式を使用できます。静的コンテンツとは、3D アセットをアップロードして公開することはできますが、3D アセットに関連付けられた *Dynamic* Imaging や画像の再編集はサポートされていないことを意味します。これは、Dynamic Media Imaging サーバーが 3D 形式を認識しないためです。したがって、Dynamic Media で 3D アセットを公開すると、インスタント URL をコピーできます。3D アセットの URL は、通常の Dynamic Media の URL 構造に従います。ただし、Dynamic Media 内の従来の画像アセットとは異なり、アセットの URL 内のパラメーターは編集できません。

[静的アセットの URL の取得](/help/assets/dynamic-media/linking-urls-to-yourwebapplication.md#obtaining-a-url-for-a-static-asset) も参照してください。

**[!UICONTROL カード表示]**&#x200B;で、アセット名のすぐ下、アセットが発行されたことを示す日時の左側に、小さな地球アイコンが表示されます。**[!UICONTROL リスト表示]**&#x200B;では、公開されたアセットと公開されていないアセットが「**[!UICONTROL 公開]**」列でわかります。

[!DNL Experience Manager] を WCM として使用している場合は、この公開方法を使用して、Dynamic Media 3D アセットを Web ページに直接追加します。

[Dynamic Media アセットの公開](/help/assets/dynamic-media/publishing-dynamicmedia-assets.md) も参照してください。

[ページの公開](/help/sites-cloud/authoring/sites-console/publishing-pages.md) も参照してください。

**静的 Dynamic Media 3D アセットを公開するには：**

1. 3D アセット（GLB、OBJ、STL のいずれかのファイル形式）を開きます。
1. 詳細ページのツールバーで、「**[!UICONTROL クイック公開]**」を選択します。

   ![3d-asset-quick-publish](/help/assets/dynamic-media/assets/3d-asset-quick-publisha.png)

1. 「**[!UICONTROL 閉じる]**」を選択してダイアログボックスを終了し、アセットの詳細ページに戻ります。
1. 3D アセットのファイル名の左にあるドロップダウンリストから、「**[!UICONTROL レンディション]**」を選択します。

   ![3d-asset-renditions](/help/assets/dynamic-media/assets/3d-asset-renditionsa.png)

1. 「**[!UICONTROL オリジナル]**」を選択します。3D アセットが公開（「アクティブ化」）されると、次の 3D アセットの条件がすべて満たされた場合、「**[!UICONTROL URL]**」ボタンがページの左下隅近くに表示されます。
   * 3D アセットがサポートされている形式（GLB、OBJ、STL、USDZ）。
   * 3D アセットが Dynamic Media 画像制作システム（IPS）に取り込まれている。
   * 3D アセットが公開されている。

   ![3d-asset-url](/help/assets/dynamic-media/assets/3d-asset-urla.png)

1. 3D アセットのダイレクト実稼動 URL（Web ページにコピーして使用可能）を表示するには、「**[!UICONTROL URL]**」を選択します。

### ディメンショナルビューアを使用した、Dynamic Media 3D アセットの代替の公開方法 {#alternate-publish-methods}

 を WCM として使用して&#x200B;*いない*&#x200B;場合は、次の 2 つの方法で Dynamic Media 3D アセットを公開します。[!DNL Experience Manager]

* **[!UICONTROL URL]** - サードパーティの Web コンテンツ管理システムを使用していて、ディメンショナルビューアを使用して Dynamic Media 3D アセットを Web ページにリンクする場合は、「**[!UICONTROL URL]**」を使用します。

  [Web アプリケーションへの URL のリンク](/help/assets/dynamic-media/linking-urls-to-yourwebapplication.md#obtaining-a-url-for-an-asset)を参照してください。

* **[!UICONTROL 埋め込み]** - Web ページに埋め込まれた Dynamic Media 3D アセットをディメンショナルビューアで表示する場合は、「**[!UICONTROL 埋め込み]**」を使用します。埋め込みコードをクリップボードにコピーして、Web ページに貼り付けることができます。**[!UICONTROL 埋め込み]**&#x200B;ダイアログボックスでは、コードの編集はできません。

  [Web ページへの Dynamic Media ビデオ、画像ビューア、またはディメンショナルビューアの埋め込み](/help/assets/dynamic-media/embed-code.md#embedding-the-video-or-image-viewer-on-a-web-page)を参照してください。
