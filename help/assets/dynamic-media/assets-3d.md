---
title: ダイナミックメディアでの3Dアセットの操作
seo-title: ダイナミックメディアでの3Dアセットの操作
description: ダイナミックメディアで3Dアセットを操作する方法を学びます。
seo-description: ダイナミックメディアで3Dアセットを操作する方法を学びます。
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS and AEM as a Cloud Service
topic-tags: introduction
content-type: reference
translation-type: tm+mt
source-git-commit: 7dae5c0ed82687415719cd2d72f98028cf0a8e64
workflow-type: tm+mt
source-wordcount: '2258'
ht-degree: 13%

---


# ダイナミックメディアでの3Dアセットの操作 {#working-with-three-d-assets-dm}

ダイナミックメディアでは、3Dアセットをイマーシブなエクスペリエンスとしてアップロード、管理、表示および配信できます。

* 3Dアセットのワンクリックで公開(ツールバーの **[!UICONTROL クイック公開]** )してURLを生成
* Adobe Dimensionを使用した高品質でインタラクティブなDimensionalビューアプリセットで、3Dアセットの表示のサポートを最適化しました。
* 3D Media WCMコンポーネントを使用すると、3DアセットをAEMサイトのページに簡単に追加できます。

ダイナミックメディアで3Dアセットを使用する場合、追加のインストールは必要ありません。

![3次元の靴](/help/assets/dynamic-media/assets/3d-dimensional-viewer-quickpublish-url-embed2a.png)

<!-- See also [Dynamic Media 3D Release Notes](/help/release-notes/aem3d-release-notes.md). -->

## ダイナミックメディアでサポートされる3Dファイル形式 {#supported-three-d-file-formats-in-dm}

ダイナミックメディアは、次の3Dファイル形式をサポートしています。

| 3D ファイル拡張子 | ファイル形式 | MIME タイプ | 備考 |
|---|---|---|---|
| GLB | バイナリ GL 伝送 | model/gltf-binary | マテリアルとテクスチャを単一のアセットとして含めます。 |
| OBJ | WaveFront 3D オブジェクトファイル | application/x-tgif |  |
| STL | ステレオリソグラフィ | application/vnd.ms-pki.stl |  |
| USDZ | 汎用シーン記述 Zip アーカイブ | model/vnd.usdz+zip | *取り込みのみのサポート 表示も操作もできません。* USDZは独自の3D形式で、SafariやiOSでネイティブに表示できます。 |

## クイック開始: ダイナミックメディア内の3Dアセット {#quick-start-three-d}

次の順を追ったワークフローに従って、ダイナミックメディアで3Dアセットをすばやく操作できます。

ダイナミックメディアで3Dアセットを操作する前に、AEM管理者が既にDynamic Media Cloud Servicesを有効にし、設定していることを確認します。

See [Configuring Dynamic Media Cloud Services](/help/assets/dynamic-media/config-dm.md#configuring-dynamic-media-cloud-services).

1. **3Dアセットのアップロード**

   * [ダイナミックメディアで使用する3Dアセットのアップロード](/help/assets/add-assets.md#upload-assets)。
   * [ダイナミックメディアでのアップロードでサポートされる3Dファイル形式](#supported-three-d-file-formats-in-dm)。

1. **3Dアセットの管理**

   * 3Dアセットの整理と検索

      * [デジタルアセットの整理](/help/assets/organize-assets.md)。
      * [3Dアセットの検索](/help/assets/search-assets.md)。
   * 表示3Dアセット

      * [3Dアセットの表示と操作](#viewing-three-d-assets)。
      * [ディメンションビューアプリセットの管理](/help/assets/dynamic-media/managing-viewer-presets.md)。
   * 3Dアセットメタデータの操作

      * [デジタルアセット用のメタデータの管理](/help/assets/manage-digital-assets.md#editing-properties).
      * [メタデータスキーマ](/help/assets/metadata-schemas.md).



1. **3Dアセットのパブリッシュ**

   * [ダイナミックメディア3Dアセットの公開](#publishing-three-d-assets)

## 3Dアセットの表示と操作について {#viewing-three-d-assets}

この節では、3Dアセットの表示方法と操作方法を2通り説明します。 アセットの詳細ページ内、およびサイトの3Dメディアコンポーネント内から

インタラクティブ3Dビューアには、3Dアセットの軌道回転、ズーム、パンを行うことができる、インタラクティブカメラコントロールの集まりが含まれます。

アセットの詳細ページの表示で3Dアセットを開くのに要する時間は、いくつかの要因に依存します。 以下の要因が含まれます。

* サーバーへの帯域幅。
* サーバーの待ち時間
* 画像の複雑さ。

また、ワークステーション、ノート、モバイルタッチデバイスなどのクライアントコンピュータの機能も、カメラをインタラクティブに操作する場合には考慮する必要があります。 グラフィック性能に優れ、ある程度パワフルなシステムなら、インタラクティブな 3D 表示をよりスムーズで満足なものにすることができます。

>[!TIP]
>
>次元ビューアプリセットをビューアプリセットエディタで開いて、3Dファイルをアップロードしなくても3Dアセット内を移動する練習をすることができます。 Dimensionalビューアプリセットには、操作できる組み込みの3Dアセットがあります。
>
>See [Managing viewer presets](/help/assets/dynamic-media/managing-viewer-presets.md).

## アセットの詳細ページからの3Dアセットの表示と操作 {#viewing-three-d-assets-from-asset-details-page}

ソフトウェアインターフェイスを使用したアセットの [プレビューも参照してください](/help/assets/dynamic-media/previewing-assets.md)。

**アセットの詳細ページから3Dアセットを表示し、操作するには**

1. 3D アセットが AEM にアップロードされていることを確認します。

   詳しくは、ダイナミックメディアで使用する3Dアセットの [アップロードを参照してください](/help/assets/add-assets.md#upload-assets)。

1. AEM の&#x200B;**[!UICONTROL ナビゲーション]**&#x200B;ページで、**[!UICONTROL アセット／ファイル]**&#x200B;をタップします。
1. Near the upper-right corner of the page, from the **[!UICONTROL View]** drop-down list, tap **[!UICONTROL Card View]**.
1. 表示する 3D アセットに移動します。
1. 3D アセットのカードをタップして、アセットの詳細ページで開きます。
1. 3Dアセットの詳細表示ページで、次のいずれかの操作を行います。

   * **カメラの回転** - 3Dシーンとオブジェクトの周りに表示を回転させます。
      * _マウス_：左クリックしながらドラッグします。
      * _タッチスクリーン_：1 本指で押しながらドラッグします。
   * **カメラのパン** -表示を左、右、上、下にパンします。
      * _マウス_：右クリックしながらドラッグします。
      * _タッチスクリーン_：2 本指で押しながらドラッグします。
   * **カメラのズーム** — カメラをズームして、3Dシーンの領域内外を移動します。
      * _マウス_：ホイールをスクロールします。
      * _タッチスクリーン_：2 本指でピンチします。
   * **カメラを再入力** - 3Dシーン内のオブジェクト上の点にカメラを再入力します。
      * _マウス_：ダブルクリックします。
      * _タッチスクリーン_：ダブルタップします。
   * **リセット** — ページ右下付近のリセットアイコンをタップし、表示ターゲットポイントを3Dアセットの中央に戻します。 リセットを使用しても、アセット全体を表示したり、適切な表示サイズで表示するために、カメラを近づけたり遠ざけたりできます。
   * **フルスクリーンモード** — フルスクリーンモードに切り替えるには、ページ右下隅のフルスクリーンアイコンをタップします。

1. ページの右上隅にある「**[!UICONTROL 閉じる]**」をタップして、アセットページに戻ります。

## 3Dメディアコンポーネント内の3Dアセットの表示と操作 {#interacting-with-asset-inside-three-d-media-component}

Webページが **[!UICONTROL 編集]** モードの場合、3Dアセットとのやり取りはできません。 アセットをインタラクティブにするには、 **[!UICONTROL プレビュー]** 機能を使用して、3D Mediaコンポーネントの機能にフルアクセスして、ページエディターでWebページを表示します。

>[!IMPORTANT]
>
>このタスクは、3DメディアコンポーネントをWebページに追加し、3Dアセットをコンポーネントに割り当てた後にのみ実行できます。 詳しくは、Webページへの3Dメディアコンポーネントの [追加](#adding-the-three-d-media-component-to-a-web-page) 、および3Dメディアコンポーネントへの3Dアセットの [割り当てを参照してください](#assigning-a-three-d-asset-to-the-component)。

ソフトウェアインターフェイスを使用したアセットの [プレビューも参照してください](/help/assets/dynamic-media/previewing-assets.md)。

**3D Mediaコンポーネント内の3Dアセットを表示し、操作するには**

1. Webページが **[!UICONTROL 編集モードの間に]** 、次のいずれかの操作を行います。

   * ページ右上付近にある「 **[!UICONTROL プレビュー]** 」をクリックして **[!UICONTROL プレビュー]** モードに入ります。
   * ブラウザー `/editor.html` のページURLから削除します。

完全にインタラクティブな3Dアセット(    ![3D Mediaコンポーネント内に表示される3Dアセット](/help/assets/dynamic-media/assets/3d-asset-in-3d-mediaa.png)完全にインタラクティブな3Dアセット **[!UICONTROL (]** プレビューモードで表示される)。

1. **[!UICONTROL プレビュー]** ・モードの間に、次のいずれかの操作を行います。

   * **カメラの回転** - 3Dシーンとオブジェクトの周りに表示を回転させます。
      * _マウス_：左クリックしながらドラッグします。
      * _タッチスクリーン_：1 本指で押しながらドラッグします。
   * **カメラのパン** -表示を左、右、上、下にパンします。
      * _マウス_：右クリックしながらドラッグします。
      * _タッチスクリーン_：2 本指で押しながらドラッグします。
   * **カメラのズーム** — カメラをズームして、3Dシーンの領域内外を移動します。
      * _マウス_：ホイールをスクロールします。
      * _タッチスクリーン_：2 本指でピンチします。
   * **カメラを再入力** - 3Dシーン内のオブジェクト上の点にカメラを再入力します。
      * _マウス_：ダブルクリックします。
      * _タッチスクリーン_：ダブルタップします。
   * **リセット** — ページ右下付近のリセットアイコンをタップし、表示ターゲットポイントを3Dアセットの中央に戻します。 リセットを使用しても、アセット全体を表示したり、適切な表示サイズで表示するために、カメラを近づけたり遠ざけたりできます。
   * **フルスクリーンモード** — フルスクリーンモードに切り替えるには、ページ右下隅のフルスクリーンアイコンをタップします。

## 3D Mediaコンポーネントの操作について {#working-with-three-d-media-component}

ダイナミックメディアには、AEMサイトで使用できるダイナミックメディア3Dメディアコンポーネントが含まれており、Webページ上で3Dモデルをインタラクティブに表示できます。

* [ページテンプレートへの3Dメディアコンポーネントの追加](#adding-three-d-media-component-to-page-template)
* [Webページへの3D Mediaコンポーネントの追加](#adding-the-three-d-media-component-to-a-web-page)
   * [オプション — 3Dメディアコンポーネントの設定](#configuring-the-three-d-component)
* [3D Mediaコンポーネントへの3Dアセットの割り当て](#assigning-a-three-d-asset-to-the-component)


## Adding the 3D Media component to the page template {#adding-three-d-media-component-to-page-template}

1. **[!UICONTROL ツール／一般／テンプレート]**&#x200B;に移動します。
1. 3D コンポーネントを有効にするページテンプレートに移動し、テンプレートを選択します。
1. Tap **[!UICONTROL Edit]** to open the template.
1. ページの右上付近にあるドロップダウンメニューで、「 **[!UICONTROL 構造]** 」モードを選択します（まだアクティブでない場合）。

   ![3d-media-component-structure](/help/assets/dynamic-media/assets/3d-media-component-structurea.png)

1. 「 **[!UICONTROL レイアウトコンテナ]** 」領域の空の領域をタップして選択し、関連するツールバーを開きます。
1. ツールバーで、 **[!UICONTROL ポリシー]** アイコンをタップし、 **[!UICONTROL ポリシーエディターを開きます]**。
1. 「 **[!UICONTROL プロパティ]** 」セクションの「 **[!UICONTROL 許可されているコンポーネント]** 」タブで、「 **[!UICONTROL ダイナミックメディア]**」までスクロールし、リストを展開して、「 **** 3Dメディア」を確認します。
1. 「 **[!UICONTROL 完了]** 」をタップして変更を保存し、 **[!UICONTROL ポリシーエディターを閉じます]**。

   これで、このテンプレートを使用するすべてのページに、ダイナミックメディア3Dメディアコンポーネントを配置できます。

## Adding the 3D Media component to a web page {#adding-the-three-d-media-component-to-a-web-page}

Webコンテンツ管理ーシステムとしてAdobe Experience Managerを使用している場合は、3D Mediaコンポーネントを使用してWebページに3Dアセットを追加できます。

See also [Adding Dynamic Media assets to pages](/help/assets/dynamic-media/adding-dynamic-media-assets-to-pages.md).

1. AEMサイトを開き、ダイナミックメディア3Dメディアコンポーネントを追加するWebページを選択します。
1. Tap the **[!UICONTROL Edit]** (pencil) icon to open the page into the page editor. ページの右上付近で **[!UICONTROL 「編集]** 」モードが選択されていることを確認します。

   ![3d-media-component-add](/help/assets/dynamic-media/assets/3d-media-component-edita.png)

1. ツールバーで、サイドパネルアイコンをタップして、パネルの表示を切り替えるか、「オン」にします。

1. サイドパネルで、プラス記号アイコンをタップし、 **[!UICONTROL コンポーネント]** リストを開きます。

   ![3d-media-component-drag-drop](/help/assets/dynamic-media/assets/3d-assets-filtera.png)

1. **[!UICONTROL 3D Media]** コンポーネントをコンポーネント **** リストから、3Dビューアを表示するページ上の場所にドラッグします。

これで、3Dアセットをコンポーネントに割り当てる準備が整いました。

詳しくは、3Dメディアコンポーネントへの3Dアセットの [割り当てを参照してください](#assigning-a-three-d-asset-to-the-component)。

### オプション — 3Dメディアコンポーネントの設定 {#configuring-the-three-d-component}

1. In the AEM Sites page editor, select the **[!UICONTROL 3D Media Viewer]** component that you previously added to the page.
1. Tap the **[!UICONTROL Configuration]** icon (wrench) to open the component configuration dialog box.

   ![3d-media-component-config](/help/assets/dynamic-media/assets/3d-media-component-configa.png)

1. 3Dメディアダイアログボックスの「ビューアプリセット」ドロップダウンリストで、「 **[!UICONTROL 次元]** 」を選択して、次元ビューアプリセットをコンポーネントに割り当てます。

   ![3d-media-component-edit-config](/help/assets/dynamic-media/assets/3d-media-component-edit-configa.png)

1. 右上隅のチェックマークをタップして、変更を保存します。

## 3D Mediaコンポーネントへの3Dアセットの割り当て {#assigning-a-three-d-asset-to-the-component}

Webページに3Dメディアコンポーネントを追加した後、3Dアセットを割り当てることができます。

See [Adding the 3D Media component to a web page](#adding-the-three-d-media-component-to-a-web-page).

1. In the AEM Sites page editor, click the **[!UICONTROL Assets]** icon to open **[!UICONTROL Assets]** in the side panel.
1. ドロップダウンリストで、 **[!UICONTROL 3D]** を選択して3Dアセットファイルタイプのみを表示します。
1. サイドパネルで、編集するページ上で表示する3Dアセットを検索またはスクロールします。
1. 3Dアセットをアセットサイドパネルからドラッグし、前にページに追加した **[!UICONTROL 3D Media]** コンポーネントにドロップします。

   ![3Dアセットを3Dメディアコンポーネントに割り当て](/help/assets/dynamic-media/assets/3d-asset-adda.png)

>[!NOTE]
>
>WebページがAEMサイトの **[!UICONTROL 編集]** モードの場合、3D Mediaコンポーネントは3Dアセットを表示しますが、アセットとのやり取りは不可能です。 アセットをインタラクティブにするには、 **[!UICONTROL プレビュー]** 機能を使用して、3D Mediaコンポーネントの機能にフルアクセスして、ページエディターでWebページを表示します。

## 静的ダイナミックメディア3Dアセットの公開 {#publishing-three-d-assets}

ダイナミックメディアには、ダイナミックメディアで *静的コンテンツとしてサポートされる様々な3Dファイル形式があり* 、 静的コンテンツとは、3Dアセットをアップロードして公開することはできますが、3Dアセットに関連付けられた *ダイナミック* イメージングや画像の再編集はサポートされていないことを意味します。 理由は、Dynamic Media Imaging Serverが3D形式を認識しないからです。 したがって、ダイナミックメディアで3Dアセットを公開すると、インスタントURLをコピーできます。 3DアセットのURLは、通常のダイナミックメディアのURL構造に従います。 ただし、ダイナミックメディアの従来の画像アセットとは異なり、アセットのURL内のパラメーターを編集することはできません。

See also [Obtaining a URL for a static asset](/help/assets/dynamic-media/linking-urls-to-yourwebapplication.md#obtaining-a-url-for-a-static-asset).

カー **[!UICONTROL ド表示では]**、アセット名のすぐ下、アセットが公開されたことを示す日時の左側に、小さなグローブアイコンが表示されます。 **[!UICONTROL リスト表示]**&#x200B;では、公開されたアセットと公開されていないアセットが「**[!UICONTROL 公開]**」列でわかります。

WCMとしてAEMを使用している場合は、この公開方法を使用してダイナミックメディア3DアセットをWebページに直接追加します。

See also [Publishing Dynamic Media assets](/help/assets/dynamic-media/publishing-dynamicmedia-assets.md).

ページの [公開も参照してください](/help/sites-cloud/authoring/fundamentals/publishing-pages.md)。

**ダイナミックメディア3Dアセットを公開するには**

1. 3Dアセット（GLB、OBJ、またはSTLファイル形式）を開き、アセットの詳細ページに表示します。
1. On the toolbar, tap **[!UICONTROL Quick Publish]**.

   ![3d-asset-quick-publish](/help/assets/dynamic-media/assets/3d-asset-quick-publisha.png)

1. 「 **[!UICONTROL 閉じる]** 」をタップしてダイアログボックスを終了し、アセットの詳細ページに戻ります。
1. 3Dアセットのファイル名の左にあるドロップダウンリストから、「 **[!UICONTROL レンディション]**」をタップします。

   ![3d-asset-renditions](/help/assets/dynamic-media/assets/3d-asset-renditionsa.png)

1. 「 **[!UICONTROL オリジナル]**」をタップします。 3Dアセットが公開（「アクティブ化」）されると、次の3Dアセットの条件がすべて満たされた場合、 **[!UICONTROL URL]** ボタンがページの左下隅近くに表示されます。
   * 3Dアセットはサポートされている形式(GLB、OBJ、STL、USDZ)です。
   * 3Dアセットがダイナミックメディアイメージ制作システム(IPS)に取り込まれました。
   * 3Dアセットが公開されます。

   ![3d-asset-url](/help/assets/dynamic-media/assets/3d-asset-urla.png)

1. 「 **[!UICONTROL URL]** 」をタップして3Dアセットの直接実稼動URLを表示し、Webページにコピーして使用できます。

### Dimensionalビューアを使用してダイナミックメディア3Dアセットを公開するための代替方法 {#alternate-publish-methods}

AEMをWCMとして使用していない場合は、ダイナミックメディア3Dアセットを公開するには *、次の* 2つの方法を使用します。

* **[!UICONTROL URL]** — サードパーティのWebコンテンツ管理ーシステムを使用していて、Dimensional Viewerを使用してダイナミックメディア3DアセットをWebページにリンクする場合は、 **** URLを使用します。

   [Web アプリケーションへの URL のリンク](/help/assets/dynamic-media/linking-urls-to-yourwebapplication.md#obtaining-a-url-for-an-asset)を参照してください。

* **[!UICONTROL 埋め込み]** - Webページに埋め込まれたダイナミックメディア3Dアセットを、ディメンションビューアを使用して表示する場合に、「 **[!UICONTROL 埋め込み]** 」を使用します。 埋め込みコードをクリップボードにコピーして、Web ページに貼り付けることができます。Editing of the code is not permitted in the **[!UICONTROL Embed]** dialog box.

   Webページへのダイナミックメディアビデオ、画像ビューアまたはディメンションビューアの [埋め込みを参照してください](/help/assets/dynamic-media/embed-code.md#embedding-the-video-or-image-viewer-on-a-web-page)。
