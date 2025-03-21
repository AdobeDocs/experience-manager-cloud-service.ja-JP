---
title: 3D アセットのプレビュー
description: Experience Manager で 3D アセットをプレビューする方法を学習します。
contentOwner: Rick Brough
feature: 3D Assets
role: User
exl-id: e873bd25-f841-4063-824f-7e48f40bb678
source-git-commit: c82f84fe99d8a196adebe504fef78ed8f0b747a9
workflow-type: tm+mt
source-wordcount: '667'
ht-degree: 95%

---

# Adobe Experience Manager での 3D アセットのプレビュー{#previewing-3d-assets}

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

| バージョン | 記事リンク |
| -------- | ---------------------------- |
| AEM 6.5 | [ここをクリックしてください](https://experienceleague.adobe.com/docs/experience-manager-65/assets/using/previewing-3d-assets.html?lang=ja) |
| AEM as a Cloud Service | この記事 |

Experience Manager Assets は、3D アセットの取り込み、管理、プレビュー、配信をサポートしています。

自動的に生成されたサムネールレンディションまたはインタラクティブ 3D ビューアーを使用して、3D アセットをプレビューできます。Experience Manager のアセットの詳細ページから、インタラクティブ 3D ビューアを使用できます。このビューアーには、3D アセットを回転、ズーム、パンできるインタラクティブなカメラコントロールのコレクションなどが含まれます。

<!-- See also [Working with 3D assets in Dynamic Media](/help/assets/dynamic-media/assets-3d.md). -->

## Experience Manager のサムネールプレビューでサポートされる形式{#supported-thumbnail-previewing-assets}

Experience Managerは、デフォルトで次のファイル形式のサムネールを生成します。

| 3D ファイル拡張子 | ファイル形式 | MIME タイプ | 備考 |
|---|---|---|---|
| GLB | バイナリ GL 伝送 | model/gltf-binary |  |
| FBX | Autodesk FBX | application/octet-stream |  |
| OBJ | WaveFront 3D オブジェクトファイル | application/x-tgif |  |
| 3DS | 3D スタジオモデル | application/x-3ds |  |
| USDz | ユニバーサルシーンの説明 | model/vnd.usdz+zip |  |

## Experience Manager のインタラクティブ 3D プレビューでサポートされる形式{#supported-3d-previewing-assets}

Experience Managerは、次のファイル形式のインタラクティブ 3D プレビューをネイティブでサポートしています。

| 3D ファイル拡張子 | ファイル形式 | MIME タイプ | 備考 |
|---|---|---|---|
| GLB | バイナリ GL 伝送 | model/gltf-binary |  |
| GLTF | GL 伝送形式 | model/gltf+json | 以下の&#x200B;**メモ**&#x200B;を参照してください。 |
| OBJ | WaveFront 3D オブジェクトファイル | application/x-tgif |  |
| STL | ステレオリソグラフィ | application/vnd.ms-pki.stl |  |


>[!NOTE]
>
>gLTF モデルのプレビューでマテリアルがレンダリングされない場合は、次のように、マテリアルに適切に名前を付け、モデルと同じルートフォルダー内の `textures` フォルダーにマテリアルを格納してください。

    Asset（フォルダー）
    model.gltf
    model.bin
    textures（フォルダー）
    material_0_baseColor.jpeg
    material_0_normal.jpeg

## Experience Manager で 3D アセットをプレビューする際のパフォーマンスに関する考慮事項{#performance-3d-previewing-assets}

アセットの詳細表示ページで 3D アセットを開くときにかかる時間は、帯域幅、画像の複雑さ、サーバーの待ち時間など、いくつかの要因によって異なります。

さらに、カメラをインタラクティブに操作する際に、ワークステーション、ノート型コンピューター、モバイルタッチデバイスなどのクライアントコンピューターの性能を考慮することも重要です。グラフィック性能に優れ、ある程度パワフルなシステムなら、インタラクティブな 3D 表示をよりスムーズで満足なものにすることができます。

**Experience Manager で 3D アセットをプレビューするには：**

1. 3D アセットが Experience Manager にアップロードされていることを確認します。詳しくは、[3D プレビューでサポートされるファイル形式](#supported-3d-previewing-assets)と[アセットのアップロード](/help/assets/manage-digital-assets.md#uploading-assets)を参照してください。
1. Experience Manager の&#x200B;**[!UICONTROL ナビゲーション]**&#x200B;ページで&#x200B;**[!UICONTROL アセット]**／**[!UICONTROL ファイル]**&#x200B;に移動します。

   ![ナビゲーションページ](/help/assets/dynamic-media/assets/navigation-assets.png)

1. ページの右上隅付近にある「表示」ドロップダウンリストで「**[!UICONTROL カード表示]**」を選択し、プレビューする 3D アセットに移動します。

   ![3D カードの選択](/help/assets/dynamic-media/assets/3d-card-select.png)
   _カード表示で、プレビューする 3D アセットのカードを選択_

1. 3D アセットのカードを選択します。

   ![インタラクティブ 3D プレビュー](/help/assets/dynamic-media/assets/3d-preview.png)
   _アセット詳細表示ページでの 3D アセットのインタラクティブプレビュー_
1. 3D アセットのアセット詳細表示ページで、次のいずれかの操作を行います。

   | 表示 | 説明 | マウス操作 | タッチスクリーン操作 |
   | --- | --- | --- | --- |
   | **カメラを回転** | 3D シーンとオブジェクトの周囲でビューを周回させます。 | 左クリックしながらドラッグします。 | 1 本指で押しながらドラッグします。 |
   | **カメラをパン** | ビューを左、右、上、下にパンします。 | 右クリックしながらドラッグします。 | 2 本指で押しながらドラッグします。 |
   | **カメラをズーム** | 3D シーンの領域の内外に移動します。 | ホイールをスクロールします。 | 2 本指でピンチします。 |
   | **カメラを中心に戻す** | カメラを中心の位置に戻し、3D シーンのオブジェクトに合わせます。 | ダブルクリックします。 | ダブルクリックします。 |
   | **リセット** | ページの右下隅付近にあるリセットアイコンを選択して、視野のターゲットポイントを 3D アセットの中心に戻します。リセットを使用しても、アセット全体を表示したり、適切な表示サイズで表示するために、カメラを近づけたり遠ざけたりできます。 |   |   |
   | **全画面表示モード** | フルスクリーンモードに入るには、ページの右下隅にあるフルスクリーンアイコンを選択します。 |   |   |

1. 作業が完了したら、ページの右上隅付近にある「**[!UICONTROL 閉じる]**」を選択します。
