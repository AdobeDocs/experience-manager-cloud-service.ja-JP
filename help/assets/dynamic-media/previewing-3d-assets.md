---
title: 3D アセットのプレビュー
description: Dynamic Media の 3D アセットのプレビュー方法について説明します。
source-git-commit: d3ee23917eba4a2e4ae1f2bd44f5476d2ff7dce1
workflow-type: tm+mt
source-wordcount: '562'
ht-degree: 55%

---


# Adobe Experience Manager{#previewing-3d-assets}での3Dアセットのプレビュー

Adobe Experience Manager では、オーサリングプロセスの一環として、3D アセットのアップロード、配信、インタラクティブプレビューをサポートしています。

インタラクティブ3Dビューアは、Experience Managerのアセットの詳細ページから利用できます。 このビューアには、3D アセットをオービット、ズームおよびパンできるインタラクティブなカメラコントロールのコレクションが含まれます。

<!-- See also [Working with 3D assets in Dynamic Media](/help/assets/dynamic-media/assets-3d.md). -->

## Experience Manager{#supported-3d-previewing-assets}の3Dプレビューに対してサポートされている形式

Experience Manager内のインタラクティブ3Dプレビューは、次のファイル形式をサポートしています。

| 3D ファイル拡張子 | ファイル形式 | MIME タイプ | 備考 |
|---|---|---|---|
| GLB | バイナリ GL 伝送 | model/gltf-binary |  |
| GLTF | GL 伝送形式 | model/gltf+json | 下の&#x200B;**注意**&#x200B;を参照してください。 |
| OBJ | WaveFront 3D オブジェクトファイル | application/x-tgif |  |
| STL | ステレオリソグラフィ | application/vnd.ms-pki.stl |  |
| DN | Adobe Dimension | model/x-adobe-dn | 取り込みのみサポート。プレビューは使用できません。 |
| USDZ | 汎用シーン記述 Zip アーカイブ | model/vnd.usdz+zip | 取り込みのみサポート。プレビューは使用できません。 |

>[!NOTE]
>
>gLTFモデルのプレビューでマテリアルがレンダリングされない場合は、次のように、マテリアルが正しく名前付けされ、モデルと同じルートフォルダ内の`textures`フォルダにあることを確認します。

    Asset（フォルダー）
    model.gltf
    model.bin
    textures（フォルダー）
    material_0_baseColor.jpeg
    material_0_normal.jpeg

## Experience Manager{#performance-3d-previewing-assets}内の3Dアセットをプレビューする場合のパフォーマンス上の考慮点

アセットの詳細表示ページで 3D アセットを開くときにかかる時間は、帯域幅、画像の複雑さ、サーバーの待ち時間など、いくつかの要因によって異なります。

また、ワークステーション、ノート、モバイルタッチデバイスなどのクライアントコンピューターの機能も、カメラをインタラクティブに操作する場合に考慮する必要があります。 グラフィック性能に優れ、ある程度パワフルなシステムなら、インタラクティブな 3D 表示をよりスムーズで満足なものにすることができます。

**Experience Manager内の3Dアセットをプレビューするには：**

1. 3D アセットが Experience Manager にアップロードされていることを確認します。詳しくは、[3D プレビューでサポートされるファイル形式](#supported-3d-previewing-assets)と[アセットのアップロード](/help/assets/manage-digital-assets.md#uploading-assets)を参照してください。
1. Experience Managerの&#x200B;**[!UICONTROL ナビゲーション]**&#x200B;ページで、**[!UICONTROL アセット]**/**[!UICONTROL ファイル]**&#x200B;をタップします。

   ![ナビゲーションページ](/help/assets/dynamic-media/assets/navigation-assets.png)

1. ページの右上隅付近にある「表示」ドロップダウンリストで「**[!UICONTROL カード表示]**」をタップし、プレビューする 3D アセットに移動します。

   ![3Dカードの選択](/help/assets/dynamic-media/assets/3d-card-select.png)
   _カード表示で、プレビューする 3D アセットのカードをタップ_

1. 3Dアセットのカードをタップします。

   ![インタラクティブ 3D プレビュー](/help/assets/dynamic-media/assets/3d-preview.png)
   _アセット詳細表示ページでの 3D アセットのインタラクティブプレビュー_
1. 3D アセットのアセット詳細表示ページで、次のいずれかの操作をおこないます。

   | 表示 | 説明 | マウス操作 | タッチスクリーンアクション |
   | --- | --- | --- | --- |
   | **カメラを回す** | 3D シーンとオブジェクトの周囲でビューを周回させます。 | 左クリックしながらドラッグします。 | 一本指で押しながらドラッグします。 |
   | **カメラのパン** | 表示を左、右、上または下にパンします。 | 右クリックしながらドラッグします。 | 2本指で押しながらドラッグします。 |
   | **カメラのズーム** | 3Dシーンの領域の内外を移動します。 | スクロールホイール | 2本指のピンチ。 |
   | **カメラを再入力** | 3Dシーン内のオブジェクト上の点にカメラを再入力します。 | ダブルクリック. | ダブルタップ. |
   | **リセット** | ページ右下隅近くにあるリセットアイコンをタップして、表示ターゲットポイントを3Dアセットの中央に戻します。 リセットを使用しても、アセット全体を表示したり、適切な表示サイズで表示するために、カメラを近づけたり遠ざけたりできます。 |  |  |
   | **全画面表示モード** | フルスクリーンモードに切り替えるには、ページ右下隅のフルスクリーンアイコンをタップします。 |  |  |

1. 作業が完了したら、ページの右上隅付近にある「**[!UICONTROL 閉じる]**」をタップします。
