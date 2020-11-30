---
title: 画像エディター
description: 画像エディターは AEM の中核となる要素で、コンポーネントを利用することでコンテンツ作成者は画像を操作しやなります。
translation-type: tm+mt
source-git-commit: 83c27daae4e8ae2ae6a8f115c9da9527971c6ecb
workflow-type: tm+mt
source-wordcount: '273'
ht-degree: 100%

---


# 画像エディター {#image-editor}

画像エディターは AEM の中核となる要素で、コンポーネントを利用することでコンテンツ作成者は画像を操作しやなります。

## 画像マップの相対単位 {#relative-units-for-image-map}

画像マップ領域は、絶対単位および相対単位として画像エディターに保持されます。相対単位は、レスポンシブ画像コンポーネント内のクライアントサイドで画像マップのサイズを（画像サイズに対して）動的に変更するデータ属性として指定する場合に役立ちます。

### imageMap プロパティ {#imagemap-property}

画像マップの座標は、画像エディターで `imageMap` プロパティとして JCR に保持されます。このエディターは、以下の形式から構成されています。

このプロパティは、マップ領域を次のように格納します。

`[area1][area2][...]`

領域の形式：

`[SHAPE(COORDINATES)"HREF"|"TARGET"|"ALT"|(RELATIVE_COORDINATES)]`

例：

`[rect(0,0,10,10)"https://www.adobe.com"|"_self"|"alt"|(0,0,0.8,0.8)]`
`[circle(10,10,10)"https://www.adobe.com"|"_self"|"alt"|(0.8,0.8,0.8)]`

## SVG 画像のサポート {#support-for-svg-images}

画像エディターでは Scalable Vector Graphics（SVG）がサポートされています。

* DAM からの SVG アセットのドラッグ＆ドロップと、ローカルファイルシステムからの SVG ファイルのアップロード、はどちらもサポートされます。

## MIME タイプによるプラグインの有効化 {#enabling-plugins-by-mime-type}

特定の状況では、サーバーサイドの処理がサポートされないため、特定の MIME タイプに対してオーサリングアクションを制限する必要があります。例えば、SVG 画像の編集は許可されない場合があります。

画像エディター内のプラグインは、個々のプラグインの設定ノードで `supportedMimeTypes` プロパティを設定することで、MIME タイプによって選択的に有効にできます。

### 例 {#example}

例えば、切り抜き機能は GIF、JPEG、PNG、WEBP、TIFF 画像に対してのみ許可されるとします。

次に、この `supportedMimeTypes` プロパティを、画像コンポーネントの `cq:editConfig` ノード上のプラグインの設定ノードで許可されている MIME タイプの文字列として設定する必要があります。

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
