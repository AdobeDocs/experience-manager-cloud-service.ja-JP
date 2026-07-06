---
title: OpenAPI機能を備えたDynamic Mediaを使用して画像を最適化する
description: OpenAPI機能を備えたDynamic Mediaの画像最適化機能を使用して、公開前に即座に画像を最適化する方法を説明します
role: Admin
feature: Asset Management, Publishing, Collaboration, Asset Processing
badgeSaas: label="AEM Assets" type="Positive" tooltip="AEM Assetsに適用）。"
exl-id: 7822732b-e2b9-4b35-b92b-cb7b31d84489
source-git-commit: 230ca753bd5f3d5b26b30a962a526dc0edfc9bd4
workflow-type: tm+mt
source-wordcount: '1627'
ht-degree: 7%

---

# OpenAPI機能を備えたDynamic Mediaを使用して画像を最適化する{#Optimize-images-using-Dynamic-Media-with-OpenAPI-Capabilities}

[!DNL Dynamic Media with OpenAPI capabilities]は、[!DNL Smart Crop]、[!DNL Image Presets]、[!DNL Smart Imaging]などの画像最適化機能を提供しています。 これらの機能により、異なるデバイスやネットワークをまたいで、高速に読み込む高品質なレスポンシブ画像を提供できます。

## スマート切り抜き{#smart-crop-using-dynamic-media-with-openapi-capabilities}

[&#x200B; スマート切り抜き](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/stable/assets/delivery/#operation/getAssetSeoFormat!in=query&path=smartcrop&t=request)は、[!DNL Dynamic Media with OpenAPI capabilities]の動的サイズ変更機能です。 [!DNL Smart Crop]は、AIを活用したコンテンツに応じた切り抜きを使用して、切り抜きバージョンの視覚的なコンテキストを維持しながら、様々な画面サイズに合わせて画像をインテリジェントに切り抜く高度な画像処理技術です。 AIは画像を分析して焦点または注目すべき点を特定し、画像を自動的に切り抜いて、切り抜かれたすべてのバージョンで焦点を維持します。 レスポンシブデザインの重要な要素である[!DNL Smart Crop]は、費用対効果が高く、時間効率の高い画像の切り抜き方法を提供します。

[Dynamic Media画像プロファイル &#x200B;](https://experienceleague.adobe.com/ja/docs/experience-manager-cloud-service/content/assets/dynamicmedia/image-profiles)の記事を参照して、[!DNL Admin View]で[&#x200B; スマート切り抜きレンディション &#x200B;](https://experienceleague.adobe.com/ja/docs/experience-manager-cloud-service/content/assets/dynamicmedia/image-profiles#creating-image-profiles)を作成する方法、[それらをフォルダー](https://experienceleague.adobe.com/ja/docs/experience-manager-cloud-service/content/assets/dynamicmedia/image-profiles#applying-an-image-profile-to-folders)に適用する方法、または既に画像またはフォルダーに適用されている[&#x200B; レンディションを編集](https://experienceleague.adobe.com/ja/docs/experience-manager-cloud-service/content/assets/dynamicmedia/image-profiles#editing-the-smart-crop-or-smart-swatch-of-a-single-image)する方法について説明します。 この[&#x200B; ビデオ &#x200B;](https://experienceleague.adobe.com/ja/docs/experience-manager-learn/assets/dynamic-media/images/smart-crop-feature-video-use)の手順で[!DNL Smart Crop]を作成する方法を説明します。

[!DNL Smart Crop] パラメーターは、名前付きスマート切り抜きプロファイルが存在し、アセットに適用されていることを想定しています。 [!DNL Smart Crop] パラメーターと名前付き[!DNL Smart Crop] プロファイルの適用方法について詳しくは、[&#x200B; スマート切り抜きプロファイル &#x200B;](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/stable/assets/delivery/#operation/getAssetSeoFormat!in=query&path=smartcrop&t=request)を参照してください。

>[!IMPORTANT]
>
> [!DNL Smart Crop] レンディションは、管理者ビューでのみ作成できます。

## 画像プリセット{#image-presets-using-dynamic-media-with-openapi-capabilities}

[!DNL Dynamic Media with OpenAPI capabilities]の[画像プリセット &#x200B;](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/stable/assets/delivery/#operation/getAssetSeoFormat!in=query&path=preset&t=request)機能を使用して、即座に画像を変換します。 [!DNL image preset]は、出力画像のサイズ設定と書式設定ルールの事前定義済みセットです。

[!DNL Dynamic Media with OpenAPI capabilities]は、プリセット名を使用して画像を即座に変換し、レンディションを即座に生成します。 プリセットパラメーターを含む[!DNL Dynamic Media with OpenAPI]配信URLを介して画像をリクエストすると、[!DNL DM with OpenAPI]はプリセットの変換を適用し、レンディションをオンデマンドで作成してユーザーに配信します。

[!DNL Dynamic Media with OpenAPI]配信URLを使用して、1つのプリセットを複数の画像に適用できます。 これにより、各アセットを手作業で編集することなく、アセット間で一貫性のあるフォーマットを実現できます。

[画像プリセットの管理](https://experienceleague.adobe.com/ja/docs/experience-manager-cloud-service/content/assets/dynamicmedia/managing-image-presets)の記事を参照して、管理者ビュー[&#128279;](https://experienceleague.adobe.com/ja/docs/experience-manager-cloud-service/content/assets/dynamicmedia/managing-image-presets#creating-image-presets)で画像プリセットを作成する[方法と、異なる画面サイズに合わせてアセットを自動的に調整するレスポンシブ画像プリセット &#x200B;](https://experienceleague.adobe.com/ja/docs/experience-manager-cloud-service/content/assets/dynamicmedia/managing-image-presets#creating-a-responsive-image-preset)を作成する方法について学んでください。

### 画像プリセットを使用するメリット{#benefits-of-image-presets}

[!DNL Image Presets]には、[!DNL Dynamic Media with OpenAPI]での画像の管理と配信に関して、いくつかの利点があります。 主な利点には次のようなものがあります。

* プリセットを使用すると、画像配信URLを短くできます。 配信URLを長くする複数の画像修飾子を追加する代わりに、1つのプリセットを使用します。 短いURLは、web サイト、モバイルアプリ、電子メールなどのチャネルをまたいで、容易に管理し、一貫した画像配信を確保します。
* 画像プリセット ソース画像ファイルからジャストインタイムのレンディションを作成します。 このオンデマンドレンディション生成機能により、同じファイルの複数の静的レンディションを作成して保存する必要がなくなり、時間とストレージの両方を節約できます。
* 単一のプリセットを大規模なアセットに一度に適用することで、各アセットの手作業による編集を避け、フォーマットの一貫性を確保し、スケーラビリティを確保できます。
* プリセットのパラメーターを更新すると、そのプリセットを使用するすべての画像が自動的に再フォーマットされます。 これにより、フォーマットを一元的に更新することで編集が合理化され、個々のアセットやweb コードを再編集する必要がなくなります。
* CDNによってキャッシュされた動的レンディションにより、効率性とパフォーマンスが向上し、その結果、読み込みが高速化され、デバイスやネットワークをまたいでパフォーマンスが最適化されます。

### 画像プリセットの使用{#use-image-presets-using-dynamic-media-with-openapi-capabilities}

[!DNL Image Presets]を作成した後、次のワークフローに使用できます。

* [画像配信URLのプリセットを使用して、エンドユーザーに配信する前にレンディションをオンザフライで作成します](#use-presets-in-delivery-urls)
* [AEM Sitesでのオーサリング時にプリセットを使用する](#use-presets-during-authoring-in-aem-sites)

#### 画像配信URLでのプリセットの使用{#use-presets-in-delivery-urls}

プリセットを使用すると、配信URLをより短く簡単に使用できます。  各プリセット名は、配信URLで一意の識別子として機能します。 アセットの配信URLに複数の修飾子を追加する代わりに、プリセット名を参照して、即座にレンディションを生成します。 [画像にDynamic Media画像プリセットを適用する方法を学ぶ](https://experienceleague.adobe.com/ja/docs/experience-manager-cloud-service/content/assets/dynamicmedia/image-presets)。次の例では、プリセットを含むURLと、プリセットを含まないURLを比較します。

プリセットのない&#x200B;**URL （長いURL）**:

```
https://delivery-p30902-e145436-cmstg.adobeaemcloud.com/adobe/assets/urn:aaid:aem:393d5579-5be2-49a5-ac5f-8fed72bfb614/as/AdobeStock_63266433.avif?width=400&height=300&fit=crop&qualit=85&sharpen=true
```

プリセットを含む&#x200B;**URL （短いURL）**:

```
https://delivery-p30902-e145436-cmstg.adobeaemcloud.com/adobe/assets/urn:aaid:aem:393d5579-5be2-49a5-ac5f-8fed72bfb614/as/AdobeStock_63266433.avif?preset=thumbnail
```

プリセットサムネールには、同じ画像修飾子設定がバンドルされます。

#### AEM Sitesでのオーサリング時にプリセットを使用する{#use-presets-during-authoring-in-aem-sites}

作成者は、[!DNL Dynamic Media]のサポートが有効になっている場合、[!DNL AEM Sites]のオーサリングページでページ編集中に[!DNL Image Presets]を選択できます。オーサリングページで画像プリセットを使用するには、次の手順を実行します。

1. Sites オーサリングページに移動します。
1. AEM ページエディター[&#128279;](/help/assets/integrate-remote-approved-assets-with-sites.md#access-remote-assets-in-aem-page-editor) セクションの リモートアセットにアクセスする手順を実行して、[!DNL Asset Selector] パネルを使用してアセットを選択します。
1. [!DNL asset selector] パネルで、**[!UICONTROL プリセットタイプ]**&#x200B;までスクロールし、**[!UICONTROL 画像修飾子]** フィールドに`Preset=Preset Name`を指定して、**[!UICONTROL 完了]**&#x200B;をクリックします。
   ![&#x200B; プリセット &#x200B;](/help/assets/assets/preset-in-asset-selector-panel.png)

## スマートイメージング{#use-smart-imaging-using-dynamic-media-with-openapi-capabilities}

画像配信に[!DNL Dynamic Media with OpenAPI capabilities]を使用すると、[&#x200B; スマートイメージング &#x200B;](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/stable/assets/delivery/)を通じて画像が自動的に最適化されます。 配信の最適化により、画像の読み込みが速くなり、視覚的な品質が最大限に高まり、ファイルサイズが最小限に抑えられます。 その結果、最小限の帯域幅でweb サイトの読み込みを高速化し、応答性を向上させながら、デバイスやネットワークをまたいで一貫して高いビジュアル品質を実現できます。

[!DNL Smart Imaging]には次の機能が含まれています：

* [自動書式変換](#auto-format-conversion)
* [&#x200B; ネットワーク帯域幅の最適化](#network-bandwidth-optimisation)

### 自動書式変換{#auto-format-conversion}

[!DNL Dynamic Media with OpenAPI] [は、AVIFやWEBP](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/stable/assets/delivery/#operation/getAssetSeoFormat!in=query&path=auto-format&t=request)など、最新のweb最適化形式に画像を自動的に変換します。 変換は、要求された形式に関係なく、ブラウザーの機能と[&#x200B; ライセンス使用権限](https://experienceleague.adobe.com/ja/docs/experience-manager-cloud-service/content/assets/dynamicmedia/dm-prime-ultimate)によって異なります。

AVIFおよびWEBP形式では、より優れた圧縮が提供され、画像の配信と読み込みが小さく高速になります。 AVIFは、すべてのブラウザー機能を処理するため、デフォルトの形式として使用されます。

[!DNL Dynamic Media with OpenAPI]は、`auto-format` クエリパラメーターを使用して、最適化された配信のために画像をさまざまな形式に変換するためのブラウザーの動作を制御します。 自動フォーマット変換には、**自動プロモーション**&#x200B;と&#x200B;**自動デモ**&#x200B;が含まれます。 Webに最適化されたフォーマット（AVIFまたはWEBP）をJPEGまたはPNG経由で配信する場合は、自動プロモーションと呼ばれます。

デフォルトでは、`auto-format` クエリパラメーターは`true`に設定されています。 `auto-format`が有効（true）になっている場合、システムは要求された形式を無視し、画像の特徴、ブラウザーの機能、および[&#x200B; ライセンスの使用権限](https://experienceleague.adobe.com/ja/docs/experience-manager-cloud-service/content/assets/dynamicmedia/dm-prime-ultimate)に基づいて、webに最適化された形式（AVIFまたはWEBP）を自動的に選択します。

`auto-format`がtrueの場合、システムは次の順序で画像形式を配信します。

* ***AVIF***: AVIFは、ブラウザーがサポートしており、ライセンスで許可されている場合に配信されます。 これを自動プロモーションと呼びます。
* ***WEBP***: AVIFがサポートされていないか、ライセンスが付与されていない場合は、WEBPが配信されます。 これも自動車プロモーションです。
* ***JPEG***: JPEGは、AVIFおよびWEBPがサポートされておらず、画像にアルファチャンネル（透明度）がない場合にのみ配信されます。 これを自動デモと呼びます。
* ***PNG***: PNGは、ブラウザーが最新の形式をサポートしておらず、画像にアルファチャンネル（透明度）がある場合に配信されます。 これは自動デモとも呼ばれます。

クエリパラメーターを`false`に設定して`auto-format`を無効にし、必要な形式を指定して、その形式で配信される画像を取得します。

### ネットワーク帯域幅の最適化{#network-bandwidth-optimisation}

画像は、クライアントのネットワーク条件に基づいて自動的に最適化され、より迅速な配信とスムーズな読み込みを実現します。 [品質](#quality-parameter)および[最高品質](#max-quality-parameter) パラメーターは、画像圧縮レベルを1 ～ 100の値で制御することで、自動的に画質を調整します。

`quality`および`max-quality` パラメーターの次の主要な動作を参照してください。

* [!DNL quality]と[!DNL max-quality]の両方が指定されている場合、[!DNL quality]が優先されます。
* [!DNL quality]のみが指定されている場合、ネットワーク速度に基づいて、読み込み時間に関係なく品質が配信されます。
* [!DNL max-quality]のみが指定されている場合、ネットワークの状態に基づいて画質が自動的に調整され、指定された[!DNL max-quality]値まで最高の画質が提供されます。
* どちらも指定しない場合、システムはデフォルトの`max-quality`/`85`で動的最適化を適用します。

#### 品質パラメーター{#quality-parameter}

品質パラメーターは、読み込み速度よりも画質を優先します。 出力画質を要求された値（1から100の間）に固定し、ネットワーク条件を無視します。 [品質パラメーター](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/stable/assets/delivery/#operation/getAssetSeoFormat!in=query&path=quality&t=request)について詳しく説明します。

#### 最大品質パラメーター{#max-quality-parameter}

Max-qualityは、クライアントのネットワーク速度に基づいて、画質と読み込み時間をバランスさせます。 特定のネットワーク条件に対して可能な限り高い画質（1～100）を提供しながら、低速ネットワークでの画質を下げることで、より高速な読み込み時間を優先します。 [最高品質パラメーター](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/stable/assets/delivery/#operation/getAssetSeoFormat!in=query&path=quality&t=request)について詳しく説明します。


**関連情報**

* [アセットを翻訳](/help/assets/translate-assets.md)
* [Assets HTTP API](/help/assets/mac-api-assets.md)
* [AEM Assets as a Cloud Service でサポートされているファイル形式](/help/assets/file-format-support.md)
* [アセットを検索](/help/assets/search-assets.md)
* [接続されたアセット](/help/assets/use-assets-across-connected-assets-instances.md)
* [アセットレポート](/help/assets/asset-reports.md)
* [メタデータスキーマ](/help/assets/metadata-schemas.md)
* [アセットをダウンロード](/help/assets/download-assets-from-aem.md)
* [メタデータを管理](/help/assets/manage-metadata.md)
* [Dynamic Media テンプレートの管理](/help/assets/dynamic-media/manage-dynamic-media-templates.md)
* [レポートの管理](/help/assets/manage-reports-assets-view.md)
* [検索ファセット](/help/assets/search-facets.md)
* [コレクションを管理](/help/assets/manage-collections.md)
* [メタデータの一括読み込み](/help/assets/metadata-import-export.md)
* [AEM および Dynamic Media へのアセットの公開](/help/assets/publish-assets-to-aem-and-dm.md)
