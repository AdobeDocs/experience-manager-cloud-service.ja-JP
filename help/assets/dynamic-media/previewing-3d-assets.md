---
title: 3Dアセットのプレビュー
description: 3Dアセットのプレビュー方法を学びます。
translation-type: tm+mt
source-git-commit: 6224d193adfb87bd9b080f48937e0af1f03386d6

---


# 3Dアセットのプレビュー{#previewing-3d-assets}

Experience Managerは、オーサリングプロセスの一環として、3Dアセットのアップロード、配信およびインタラクティブなプレビューをサポートします。

AEM のアセットの詳細ページから、インタラクティブ 3D ビューアを使用できます。このビューアには、3D アセットをオービット、ズームおよびパンできるインタラクティブなカメラコントロールのコレクションが含まれます。

## 3Dプレビューでサポートされる形式{#supported-3d-previewing-assets}

インタラクティブ3Dプレビューでは、次のファイル形式をサポートしています。

| 3Dファイル拡張子 | ファイル形式 | MIME type | メモ |
|---|---|---|---|
| GLB | バイナリGL伝送 | model/gltf-binary |  |
| GLTF | GL転送形式 | model/gltf+json | 下記の注 **意を参照** 。 |
| OBJ | WaveFront 3Dオブジェクトファイル | application/x-tgif |  |
| STL | 立体リソグラフィ | application/vnd.ms-pki.stl |  |
| DN | Adobe Dimension | model/x-adobe-dn | 取り込みのみのサポートプレビューは使用できません。 |
| USDZ | ユニバーサルシーン説明Zipアーカイブ | model/vnd.usdz+zip | 取り込みのみのサポートプレビューは使用できません。 |

**注意**:gLTFモデルのプレビューでマテリアルがレンダリングされない場合は、次のように、マテリアルが正しく名前付けされ、モデルと同じルートフォルダ内のフォルダに配置されていることを確認します。 `textures`

    Asset (folder)
    model.
    gltfmodel.
    bintextures (folder)
    material_0_baseColor.
    jpegmaterial_0_normal.jpeg

## Performance considerations when you preview 3D assets{#performance-3d-previewing-assets}

アセットの詳細表示ページで3Dアセットを開くのにかかる時間は、サーバーの帯域幅、画像の複雑さ、待ち時間など、様々な要因に依存します。

また、ワークステーション、ノートブック、モバイルタッチデバイスなどのクライアントコンピュータの機能も、カメラをインタラクティブに操作する際に考慮する必要があります。 グラフィック性能に優れ、ある程度パワフルなシステムなら、インタラクティブな 3D 表示をよりスムーズで満足なものにすることができます。

**3Dアセットをプレビューするには**

1. 3D アセットが AEM にアップロードされていることを確認します。詳しくは、 [3Dプレビューでサポートされる形式とアセットのアップロードを参](#supported-3d-previewing-assets) 照してくださ [](/help/assets/manage-digital-assets.md#uploading-assets)い。
1. AEMのナビゲーションページで **[!UICONTROL 、アセット]** /ファイ **[!UICONTROL ルをタップします]**。

   ![ナビゲーションページ](/help/assets/dynamic-media/assets/navigation-assets.png)

1. ページの右上隅近くにある「表示」ドロップダウンリストで「カード表示 ****」をタップし、プレビューする3Dアセットに移動します。

   ![3Dカードの選択](/help/assets/dynamic-media/assets/3d-card-select.png)
   _カード表示で、プレビューする3Dアセットのカードをタップします。_

1. 3Dアセットのカードをタップして、アセットの詳細表示ページで開きます。

   ![インタラクティブ3Dプレビュー](/help/assets/dynamic-media/assets/3d-preview.png)
   _アセットの詳細ビューページでの3Dアセットのインタラクティブプレビュー。_
1. 3Dアセットのアセットの詳細ビューページで、次のいずれかの操作を行います。
   * **「カメラを回転**」(Turn your camera) - 3Dシーンとオブジェクトの周りを回転します。
      * _マウス_:左クリックしながらドラッグします。
      * _タッチスクリーン_:一本指で押しながらドラッグします。
   * **カメラをパン**— ビューを左、右、上または下にパンします。
      * _マウス_:右クリックしながらドラッグします。
      * _タッチスクリーン_:2本指で押しながらドラッグします。
   * **「カメラをズーム**」(Zoom your camera) - 3Dシーンの領域をズームして、移動します。
      * _マウス_:スクロールホイール
      * _タッチスクリーン_:2本指のピンチ。
   * **「カメラを中心**」(Recenter your camera) - 3Dシーン内のオブジェクト上の点にカメラを中心します。
      * _マウス_:ダブルクリックします。
      * _タッチスクリーン_:ダブルタップします。
   * **「リセット**」(Reset) — ページ右下隅近くで、「リセット」(Reset)アイコンをタップして、ビューターゲット点を3Dアセットの中心に戻します。 リセットでも、アセット全体を表示したり、適切な表示サイズで表示するために、カメラを近づけたり遠ざけたりします。
   * **フルスクリーンモード**— フルスクリーンモードに入るには、ページの右下隅にあるフルスクリーンアイコンをタップします。

1. When you are finished, near the upper-right corner of the page, tap **[!UICONTROL Close]**.
