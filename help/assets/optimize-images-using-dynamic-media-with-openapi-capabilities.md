---
title: OpenAPI 機能を使用した Dynamic Media を使用した画像の最適化
description: OpenAPI 機能を備えた Dynamic Media の画像最適化機能を使用して、公開配信前にその場で画像を最適化する方法を説明します
role: Admin
feature: Asset Management, Publishing, Collaboration, Asset Processing
source-git-commit: 74c5fbda5ee1ad46b5fcab5ba89f0fd96873e3cf
workflow-type: tm+mt
source-wordcount: '1265'
ht-degree: 0%

---


# OpenAPI 機能を使用した Dynamic Media を使用した画像の最適化{#Optimize-images-using-Dynamic-Media-with-OpenAPI-Capabilities}

[!DNL Dynamic Media with OpenAPI capabilities] は、[!DNL Smart Crop]、[!DNL Image Presets]、[!DNL Smart Imaging] などの画像の最適化機能を提供します。 これらの機能は、様々なデバイスやネットワークに高速に読み込まれる、高品質でレスポンシブな画像を配信するのに役立ちます。

## スマート切り抜き{#smart-crop-using-dynamic-media-with-openapi-capabilities}

[ スマート切り抜き ](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/stable/assets/delivery/#operation/getAssetSeoFormat!in=query&path=smartcrop&t=request) は、[!DNL Dynamic Media with OpenAPI capabilities] の動的サイズ設定機能です。 [!DNL Smart Crop] は、AI を活用したコンテンツ対応切り抜きを使用して、切り抜きバージョンでの視覚的なコンテキストを維持しながら、様々な画面サイズの画像をインテリジェントに切り抜く高度な画像処理技術です。 AI が画像を分析して、焦点または注目点を特定し、画像を自動的に切り抜いて、切り抜かれたすべてのバージョンで焦点を保持します。 レスポンシブデザインの重要な要素である [!DNL Smart Crop] は、画像を切り抜くためのコスト効率の高い時間効率の良い方法を提供します。

画像またはフォルダーに既に適用されている [ スマート切り抜きレンディションの作成 ](https://experienceleague.adobe.com/ja/docs/experience-manager-cloud-service/content/assets/dynamicmedia/image-profiles)、[ フォルダーへの適用 ](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/assets/dynamicmedia/image-profiles#creating-image-profiles)、または [!DNL Admin View] レンディションの編集 [ を ](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/assets/dynamicmedia/image-profiles#applying-an-image-profile-to-folders) で行う方法については、[Dynamic Media 画像プロファイル ](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/assets/dynamicmedia/image-profiles#editing-the-smart-crop-or-smart-swatch-of-a-single-image) の記事を参照してください。 この [!DNL Smart Crop] ビデオ [ で、](https://experienceleague.adobe.com/ja/docs/experience-manager-learn/assets/dynamic-media/images/smart-crop-feature-video-use) しい手順を作成する方法を説明します。

[!DNL Smart Crop] パラメーターは、named-smartcrop-profiles が存在し、アセットに適用されていることを想定しています。 [ パラメーターと名前付き ](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/stable/assets/delivery/#operation/getAssetSeoFormat!in=query&path=smartcrop&t=request) プロファイルの適用方法について詳しくは、[!DNL Smart Crop] スマート切り抜きプロファイル [!DNL Smart Crop] を参照してください。

>[!IMPORTANT]
>
> [!DNL Smart Crop] レンディションは、管理者ビューでのみ作成できます。

## 画像プリセット{#image-presets-using-dynamic-media-with-openapi-capabilities}

[ の ](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/stable/assets/delivery/#operation/getAssetSeoFormat!in=query&path=preset&t=request) 画像プリセット [!DNL Dynamic Media with OpenAPI capabilities] 機能を使用して、その場で画像を変換する。 [!DNL image preset] は、出力画像のサイズおよびフォーマット規則の事前定義済みセットです。

プリセット名 [!DNL Dynamic Media with OpenAPI capabilities] 使用して、その場で画像を変換し、そのレンディションを即座に生成します。 プリセットパラメーターを含む [!DNL Dynamic Media with OpenAPI] 配信 URL を使用して画像をリクエスト [!DNL DM with OpenAPI] ると、はプリセットの変換を適用し、オンデマンドでレンディションを作成してユーザーに配信します。

[!DNL Dynamic Media with OpenAPI] しい配信 URL を使用して、1 つのプリセットを複数の画像に適用できます。 これにより、各アセットを手動で編集することなく、アセット間で一貫した書式設定が保証されます。

[ 管理者表示で画像プリセットを作成する方法 ](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/assets/dynamicmedia/managing-image-presets) および [ レスポンシブ画像プリセットを作成する方法 ](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/assets/dynamicmedia/managing-image-presets#creating-image-presets) について詳しくは、[ 画像プリセットの管理 ](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/assets/dynamicmedia/managing-image-presets#creating-a-responsive-image-preset) の記事を参照してください。これらの記事では、様々な画面サイズに合わせてアセットを自動的に適応させます。

### 画像プリセットを使用するメリット{#benefits-of-image-presets}

[!DNL Image Presets][!DNL Dynamic Media with OpenAPI] 画像を管理および配信する場合は、いくつかの利点があります。 主なメリットには、次のようなものがあります。

* プリセットを使用すると、画像配信 URL を短くすることができます。 配信 URL を長くする複数の画像修飾子を追加する代わりに、1 つのプリセットを使用します。 URL を短くすると、web サイト、モバイルアプリ、メール、その他のチャネル全体で、管理が容易になり、一貫した画像配信を確保できます。
* 画像プリセットは、ソース画像ファイルからジャストインタイムレンディションを作成します。 このオンデマンドレンディション生成機能により、同じファイルに対して複数の静的レンディションを作成および保存する必要がなくなり、時間とストレージの両方が節約されます。
* 1 つのプリセットを大量のアセットに一度に適用できるので、各アセットを個別に手動で編集する必要がなくなり、フォーマットの一貫性が確保され、スケーラビリティが確保されます。
* プリセットのパラメーターを更新すると、そのプリセットを使用するすべての画像が自動的に再フォーマットされます。 これにより、書式設定の更新を一元化することで編集が合理化され、個々のアセットや web コードを再編集する必要がなくなります。
* CDN にキャッシュされた動的レンディションにより、効率とパフォーマンスが向上し、デバイスとネットワークをまたいで読み込みが速くなり、パフォーマンスが最適化されます。

### 画像プリセットの使用{#use-image-presets-using-dynamic-media-with-openapi-capabilities}

[!DNL Image Presets] を作成した後、それらを次のワークフローで使用できます。
* [画像配信 URL のプリセットを使用すると、エンドユーザーに配信する前に、その場でレンディションを作成できます](#use-presets-in-delivery-urls)
* [AEM Sitesでのオーサリング時のプリセットの使用](#use-presets-during-authoring-in-aem-sites)

#### 画像配信 URL でのプリセットの使用{#use-presets-in-delivery-urls}

プリセットを使用すると、配信 URL を短く、使いやすくなります。  各プリセット名は、配信 URL の一意の識別子として機能します。 アセットの配信 URL に複数の修飾子を追加する代わりに、プリセット名を参照して、即座にレンディションを生成します。 [ 画像に Dynamic Media 画像プリセットを適用する方法を学ぶ ](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/assets/dynamicmedia/image-presets)。
次の例では、ある URL をプリセットと比較して、プリセットのない URL を特定します。

**プリセットのない URL （長い URL）**:

`https://delivery-p30902-e145436-cmstg.adobeaemcloud.com/adobe/assets/urn:aaid:aem:393d5579-5be2-49a5-ac5f-8fed72bfb614/as/AdobeStock_63266433.avif?width=400&height=300&fit=crop&qualit=85&sharpen=true`

**プリセットを含む URL （短い URL）**:

`https://delivery-p30902-e145436-cmstg.adobeaemcloud.com/adobe/assets/urn:aaid:aem:393d5579-5be2-49a5-ac5f-8fed72bfb614/as/AdobeStock_63266433.avif?preset=thumbnail` などの相対リンクにすることも可能です。
プリセットサムネールには、同じ画像の修飾子の設定がバンドルされています。

#### AEM Sitesでのオーサリング時のプリセットの使用{#use-presets-during-authoring-in-aem-sites}

[!DNL Image Presets] のサポートが有効になっている場合、作成者はオーサリングページでページ [!DNL AEM Sites] 編集中に [!DNL Dynamic Media] を選択できます。
オーサリングページで画像プリセットを使用するには、次の手順を実行します。
1. Sites オーサリングページに移動します。
1. [ パネルを使用してアセットを選択するには、「AEM ページエディターでリモートアセットにアクセス ](/help/assets/integrate-remote-approved-assets-with-sites.md#access-remote-assets-in-aem-page-editor) の節の手順を実行し [!DNL Asset Selector] す。
1. [!DNL asset selector] ントロールパネルで、「プリセット **[!UICONTROL タイプ]** まで下にスクロールし、「`Preset=Preset Name` 画像の修飾子 **[!UICONTROL 」フィールドで]** を指定します。
   ![ プリセット ](/help/assets/assets/preset-in-asset-selector-panel.png)

## スマートイメージング{#use-smart-imaging-using-dynamic-media-with-openapi-capabilities}

画像配信に [!DNL Dynamic Media with OpenAPI capabilities] を使用すると、[ スマートイメージング ](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/stable/assets/delivery/) によって画像が自動的に最適化されます。 最適化された配信により、画像の読み込みが速くなり、最大の画質と最小限のファイルサイズが実現します。 これにより、デバイスやネットワークをまたいでページの読み込みが最速になり、ビジュアル品質が安定して高くなるとともに、帯域幅が最小限に抑えられるので、web サイトがより高速でレスポンシブになります。

[!DNL Smart Imaging] には、次の機能が含まれます。
* [自動フォーマット変換](#auto-format-conversion)
* [ ネットワーク帯域幅の最適化 ](#network-bandwidth-optimisation)

### 自動フォーマット変換{#auto-format-conversion}

[!DNL Dynamic Media with OpenAPI] [ 画像を AVIF や WEBP などの最新の web に最適化された形式に自動的に変換します ](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/stable/assets/delivery/#operation/getAssetSeoFormat!in=query&path=auto-format&t=request)。 コンバージョンは、リクエストされた形式に関係なく、ブラウザーの機能と [ ライセンスの使用権限 ](https://experienceleague.adobe.com/ja/docs/experience-manager-cloud-service/content/assets/dynamicmedia/dm-prime-ultimate) によって異なります。
AVIF 形式と WEBP 形式は、より優れた圧縮を提供し、画像をより小さく、より高速に配信および読み込みます。 AVIF はすべてのブラウザー機能を処理するので、デフォルトの形式として使用されます。
[!DNL Dynamic Media with OpenAPI] では、`auto-format` クエリパラメーターを使用して、配信を最適化するために画像を様々な形式に変換する際のブラウザーの動作を制御します。 自動フォーマット変換には、**自動昇格** および **自動降格** が含まれます。 配信のために、JPEGまたは PNG よりも web に最適化されたフォーマット（AVIF または WEBP）が昇格される場合、自動プロモーションと呼ばれます。

デフォルトでは、`auto-format` クエリパラメーターは `true` に設定されています。 `auto-format` を有効にする（true）と、システムは要求された形式を無視し、画像特性、ブラウザー機能および [ ライセンスの使用権限）に基づいて web に最適化された形式（AVIF または WEBP](https://experienceleague.adobe.com/ja/docs/experience-manager-cloud-service/content/assets/dynamicmedia/dm-prime-ultimate) を自動的に選択します。

`auto-format` が true の場合、システムは次の順序で画像形式を配信します。
* ***AVIF***：ブラウザーがサポートし、ライセンスで許可されている場合は、AVIF が配信されます。 これは自動昇格と呼ばれます。
* ***WEBP***:AVIF がサポートされていないか、ライセンスを取得していない場合、WEBP が配信されます。 これは自動昇格でもあります。
* ***JPEG***: JPEGは、AVIF および WEBP がサポートされておらず、画像にアルファチャンネル（透明度）がない場合にのみ配信されます。 これは自動デモーションと呼ばれます。
* ***PNG***：ブラウザーが最新の形式をサポートしておらず、画像にアルファチャネル（透明度）が含まれている場合に PNG が配信されます。 これは自動デモーションとも呼ばれます。

クエリパラメーターを `auto-format` に設定して `false` を無効にし、画像をその形式で配信するために必要な形式を指定します。

### ネットワーク帯域幅の最適化{#network-bandwidth-optimisation}

画像は、クライアントのネットワーク条件に基づいて自動的に最適化され、配信の高速化とスムーズな読み込みを実現します。 [Quality](#quality-parameter) パラメーターと [Max-quality](#max-quality-parameter) パラメーターでは、画像の圧縮レベル（値の範囲は 1 ～ 100）を制御して画質を自動的に調整します。

次の `quality` および `max-quality `parameters の主な動作を参照してください。

* [!DNL quality] と [!DNL max-quality] の両方を指定した場合は、[!DNL quality] が優先されます。
* [!DNL quality] のみを指定した場合は、ネットワーク速度に基づいて、読み込み時間に関係なく品質が配信されます。
* [!DNL max-quality] のみを指定すると、ネットワークの状態に応じて画質が自動的に調整され、指定した [!DNL max-quality] 値まで可能な限り最高の画質が得られます。
* どちらも指定されていない場合、デフォルト `max-quality` の `85` で動的最適化が適用されます。

#### 品質パラメーター{#quality-parameter}

画質パラメーターは、読み込み速度よりも画質を優先します。 出力画質をリクエストされた値（1～100）に固定し、ネットワーク条件を無視します。 [ 品質パラメーター ](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/stable/assets/delivery/#operation/getAssetSeoFormat!in=query&path=quality&t=request) について詳しくは、こちらを参照してください。

#### 最大品質パラメーター{#max-quality-parameter}

最高品質は、クライアントのネットワーク速度に応じて画質と読み込み時間のバランスを取ります。 低速のネットワークでは画質を低下させて読み込み時間の短縮を優先し、指定されたネットワーク条件で可能な限り最高の品質（1～100）を実現します。 [max-quality パラメーター ](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/stable/assets/delivery/#operation/getAssetSeoFormat!in=query&path=quality&t=request) の詳細情報。



