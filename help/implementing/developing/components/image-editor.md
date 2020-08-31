---
title: 画像エディター
description: 画像エディタはAEMの中核となる要素で、コンポーネントを利用してコンテンツ作成者が画像を操作しやすくすることができます。
translation-type: tm+mt
source-git-commit: 83c27daae4e8ae2ae6a8f115c9da9527971c6ecb
workflow-type: tm+mt
source-wordcount: '273'
ht-degree: 10%

---


# 画像エディター {#image-editor}

画像エディタはAEMの中核となる要素で、コンポーネントを利用してコンテンツ作成者が画像を操作しやすくすることができます。

## 画像マップの相対的な単位 {#relative-units-for-image-map}

画像マップ領域は、絶対単位と相対単位の両方として画像エディタに保持されます。 相対単位は、レスポンシブ画像コンポーネント内のクライアント側で画像マップのサイズを動的に（画像サイズに対して）変更するデータ属性として指定する場合に役立ちます。

### imageMapプロパティ {#imagemap-property}

画像マップの座標は、画像エディターで `imageMap` プロパティとしてJCRに保持されます。 次の形式で指定します。

このプロパティは、マップ領域を次のように格納します。

`[area1][area2][...]`

面グラフの形式：

`[SHAPE(COORDINATES)"HREF"|"TARGET"|"ALT"|(RELATIVE_COORDINATES)]`

例：

`[rect(0,0,10,10)"https://www.adobe.com"|"_self"|"alt"|(0,0,0.8,0.8)]`
`[circle(10,10,10)"https://www.adobe.com"|"_self"|"alt"|(0.8,0.8,0.8)]`

## SVG画像のサポート {#support-for-svg-images}

Scalable Vector Graphics(SVG)は、画像エディターでサポートされています。

* DAM からの SVG アセットのドラッグ＆ドロップと、ローカルファイルシステムからの SVG ファイルのアップロード、はどちらもサポートされます。

## MIMEタイプによるプラグインの有効化 {#enabling-plugins-by-mime-type}

特定の状況では、サーバーサイドの処理がサポートされないため、特定のMIMEタイプに対してオーサリングアクションを制限する必要があります。 例えば、SVG画像の編集は許可されない場合があります。

画像エディター内のプラグインは、個々のプラグインの設定ノードでプ `supportedMimeTypes` ロパティを設定することで、MIMEタイプによって選択的に有効にすることができます。

### 例 {#example}

例えば、切り抜き機能はGIF、JPEG、PNG、WEBPおよびTIFF画像に対してのみ許可されるとします。

次に、この `supportedMimeTypes` プロパティを、画像コンポーネントのノード上のプラグインの設定ノードで許可されているMIMEタイプの文字列として設定する必要があ `cq:editConfig` ります。

`/apps/core/wcm/components/image/v2/image/cq:editConfig`

```xml
 jcr:primaryType="cq:EditConfig">
     <cq:dropTargets jcr:primaryType="nt:unstructured">
         <image ...>
            ...
         </image>
     </cq:dropTargets>
     <cq:inplaceEditing
         jcr:primaryType="cq:InplaceEditingConfig"
         active="{Boolean}true"
         editorType="image">
         <config jcr:primaryType="nt:unstructured">
             <plugins jcr:primaryType="nt:unstructured">
                 <crop
                     jcr:primaryType="nt:unstructured"
                     supportedMimeTypes="[image/gif,image/jpeg,image/png,image/webp,image/tiff]"
                     features="*">
                     <aspectRatios jcr:primaryType="nt:unstructured">
                        ...
                     </aspectRatios>
                 </crop>
                 ...
             </plugins>
             <ui jcr:primaryType="nt:unstructured">
                 ...
             </ui>
         </config>
     </cq:inplaceEditing>
 </jcr:root>
```
